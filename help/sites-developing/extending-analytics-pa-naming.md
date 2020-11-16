---
title: Implémentation de l’appellation des pages côté serveur pour Analytics
seo-title: Implémentation de l’appellation des pages côté serveur pour Analytics
description: Adobe Analytics utilise la propriété s.pageName pour identifier les pages de façon unique et pour associer les données qui sont collectées pour les pages.
seo-description: Adobe Analytics utilise la propriété s.pageName pour identifier les pages de façon unique et pour associer les données qui sont collectées pour les pages.
uuid: 37b92099-0cce-4b2d-b55c-928f636dbd7e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: be2aa297-5b78-4b1d-8ff1-e6a585a177dd
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 72%

---


# Implémentation de l’appellation des pages côté serveur pour Analytics{#implementing-server-side-page-naming-for-analytics}

Adobe Analytics utilise la propriété `s.pageName` pour identifier les pages de façon unique et pour associer les données qui sont collectées pour les pages. En règle générale, vous effectuez les tâches suivantes dans AEM afin d’attribuer à cette propriété une valeur qu’AEM envoie à Analytics :

* Utilisez la structure de service cloud Analytics pour mapper une variable CQ sur la propriété `s.pageName` d’Analytics (See [Mapping Component Data with Adobe Analytics Properties](/help/sites-administering/adobeanalytics-mapping.md).)

* Créez le composant de page de sorte qu’il contienne la variable CQ que vous mappez sur la propriété `s.pageName` (See [Implementing Adobe Analytics Tracking for Custom Components](/help/sites-developing/extending-analytics-components.md).)

Pour afficher les données de rapport Analytics dans la console Sites et dans Content Insight, AEM nécessite la valeur de la propriété `s.pageName` pour chaque page. The AEM Analytics Java API defines the `AnalyticsPageNameProvider` interface that you implement to provide the Sites console and Content Insights with the value of the `s.pageName` property. Your `AnaltyicsPageNameProvider` service resolves the pageName property on the server for reporting purposes, as it can be dynamically set using Javascript on the client for tracking purposes.

## Service Fournisseur de noms de page Analytics par défaut {#the-default-analytics-page-name-provider-service}

The `DefaultPageNameProvider` service is the default service that determines the value of the `s.pageName` property to use for retrieving Analytics data for a page. The service works in conjunction with the AEM foundation page component ( `/libs/foundation/components/page`). Ce composant de page définit les variables CQ suivantes qui sont censées être mappées sur la propriété `s.pageName` :

* `pagedata.path` : la valeur est définie sur le chemin d’accès de la page.
* `pagedata.title` : la valeur est définie sur le titre de la page.
* `pagedata.navTitle` : la valeur est définie sur le titre de navigation de la page.

The `DefaultPageNameProvider` service determines which of these CQ variables is mapped to the `s.pageName` property in the Analytics cloud service framework. Il détermine ensuite la propriété de page appropriée à utiliser pour récupérer les données de rapport Analytics :

* `pagedata.path`: Le service utilise `page.getPath()`

* `pagedata.title`: Le service utilise `page.getTitle()`

* `pagedata.navTitle`: Le service utilise `page.getNavigationTitle()`

The `page` object is the is the [ `com.day.cq.wcm.api.Page`](https://helpx.adobe.com/experience-manager/6-3/sites-developing/reference-materials/javadoc/com/day/cq/wcm/api/Page.html) Java object for the page.

If you do not map a CQ variable to the `s.pageName` property in the framework, the value for `s.pageName` is generated from the page path. For example, the page with the path `/content/geometrixx/en` uses the value `content:geometrixx:en` for `s.pageName`.

>[!NOTE]
>
>Le service DefaultPageNameProvider utilise un classement de service de 100.

## Maintien de la continuité dans les rapports Analytics {#maintaining-continuity-in-analytics-reporting}

Pour conserver un historique complet des données analytiques d’une page, il faut que la valeur de la propriété s.pageName qui est utilisée pour la page soit invariable. Cependant, les propriétés Analytics définies par le composant de page de base peuvent être facilement modifiées. Ainsi, le fait de déplacer une page change la valeur de `pagedata.path` et interrompt la continuité de l’historique des rapports :

* Les données qui avaient été collectées pour le chemin précédent ne sont alors plus associées à la page.
* Si une page distincte utilise le chemin d’accès qui était utilisé auparavant par une autre page, elle hérite des données relatives à ce chemin.

Pour garantir la continuité des rapports, la valeur de la propriété `s.pageName` doit présenter les caractéristiques suivantes :

* Unique.
* Stable.
* Lisible par un humain.

Par exemple, un composant de page personnalisé peut inclure une propriété de page que les auteurs utilisent pour spécifier un identifiant unique pour la page utilisée comme valeur pour la propriété `s.pageProperties` :

* La page inclut une variable Analytics qui est définie sur la valeur de l’identifiant unique stockée dans la propriété de page.
* La variable Analytics est mappée sur la propriété `s.pageProperties` dans la structure Analytics.
* Votre implémentation de l’interface AnalyticsPageNameProvider récupère la valeur de la propriété de page à utiliser pour interroger les données Analytics de la page.

>[!NOTE]
>
>Demandez l’aide de votre conseiller Analytics pour développer une stratégie efficace pour votre valeur `s.pageName`.

### Mise en œuvre d’un service Fournisseur de noms de page Analytics {#implementing-an-analytics-page-name-provider-service}

Implémentez l’interface `com.day.cq.analytics.sitecatalyst.AnalyticsPageNameProvider``s.pageName` en tant que service OSGi pour personnaliser la logique qui récupère la valeur de la propriété L’analyse des pages Sites et Content Insight utilisent le service pour récupérer des données de rapport d’Analytics.

L’interface AnalyticsPageNameProvider définit deux méthodes que vous devez mettre en œuvre :

* `getPageName`: Renvoie une `String` valeur qui représente la valeur à utiliser comme `s.pageName` propriété.

* `getResource`: Renvoie un objet `org.apache.sling.api.resource.Resource` qui représente la page associée à la `s.pageName` propriété.

Both methods take a `com.day.cq.analytics.sitecatalyst.AnalyticsPageNameContext` object as a parameter. La classe `AnalyticsPageNameContext` fournit des informations sur le contexte des appels Analytics :

* Chemin de base de la ressource de page.
* Objet `Framework` pour la configuration du service cloud Analytics.
* Objet `Resource` pour la page.
* Objet `ResourceResolver` pour la page.

La classe fournit également un setter pour le nom de la page.

### Exemple d’implémentation de l’interface AnalyticsPageNameProvider {#example-analyticspagenameprovider-implementation}

L’exemple d’implémentation `AnalyticsPageNameProvider` suivant prend en charge un composant de page personnalisé :

* Le composant étend le composant de page de base.
* The dialog box includes a field that authors use to specify the value of the `s.pageName` property.
* La valeur de la propriété est stockée dans la propriété pageName du nœud `jcr:content` des instances de la page.
* La propriété Analytics qui stocke la propriété `s.pageName` est appelée `pagedata.pagename`. Elle est mappée sur la propriété `s.pageName` dans la structure Analytics.

L’implémentation suivante de la méthode `getPageName` renvoie la valeur de la propriété du nœud pageName si le mappage de structure est correctement configuré :

```java
public String getPageName(AnalyticsPageNameContext context) {
        String pageName = null;

        Framework framework = context.getFramework();
        Resource resource = context.getResource();

        if (resource != null && framework != null && framework.mapsSCVariable(S_PAGE_NAME)) {
            String cqVar = framework.getMapping(S_PAGE_NAME);
            Page page = resource.adaptTo(Page.class);
            if (cqVar.equals("pagedata.pagename")) {
                pageName = page.getProperties().get("pageName",null);
            }
        }
        return pageName;
    }
```

L’implémentation suivante de la méthode getResource renvoie l’objet Resource de la page :

```java
     public Resource getResource(AnalyticsPageNameContext context) {
        Resource res = null;

        Framework framework = context.getFramework();
        ResourceResolver resolver = context.getResourceResolver();
        String pageName = context.getPageName();
        String basePath = context.getBasePath();

        if (pageName != null && basePath != null && resolver != null
                && framework != null && framework.mapsSCVariable(S_PAGE_NAME)) {
            String cqVar = framework.getMapping(S_PAGE_NAME);
            if (cqVar.equals("pagedata.pagename")) {
             Iterator<Resource>
             hits = resolver.findResources(createQuery(pageName, basePath, "pagename"), Query.JCR_SQL2);
             if (hits.hasNext()) {
              res = hits.next();
              res = res.getParent();
             }
            }
        }
        return res;
    }

    private String createQuery(String pageName, String basePath, String propName) {
        return "SELECT * FROM [cq:PageContent] WHERE ISDESCENDANTNODE(["
                + basePath + "]) and [" + propName + "] = \"" + pageName + "\"";
    }
```

Le code ci-dessous représente l’ensemble de la classe, y compris les annotations SCR qui configurent le service. Notez que le classement de service est de 200, ce qui remplace le service par défaut.

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * __________________
 *
 * Copyright 2019 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and may be covered by U.S. and Foreign Patents,
 * patents in process, and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.day.cq.analytics.sitecatalyst;

import java.util.Iterator;

import javax.jcr.query.Query;

import org.apache.sling.api.resource.Resource;
import org.apache.sling.api.resource.ResourceResolver;
import org.osgi.framework.Constants;
import org.osgi.service.component.annotations.Component;

import com.day.cq.analytics.sitecatalyst.AnalyticsPageNameContext;
import com.day.cq.analytics.sitecatalyst.AnalyticsPageNameProvider;
import com.day.cq.analytics.sitecatalyst.Framework;
import com.day.cq.wcm.api.Page;

import static com.day.cq.analytics.sitecatalyst.AnalyticsPageNameContext.S_PAGE_NAME;

/**
 * Default implementation of {@link AnalyticsPageNameProvider} that resolves
 * page title, path or navTitle if mapped in {@link Framework}.
 */
@Component(
    service = { AnalyticsPageNameProvider.class },
    property = {
        Constants.SERVICE_DESCRIPTION + "=Example Page Name Resolver implementation",
        Constants.SERVICE_RANKING + ":Integer=200"
    }
)
public class ExamplePageNameProvider implements AnalyticsPageNameProvider {
    public String getPageName(AnalyticsPageNameContext context) {
        String pageName = null;

        Framework framework = context.getFramework();
        Resource resource = context.getResource();

        if (resource != null && framework != null && framework.mapsSCVariable(S_PAGE_NAME)) {
            String cqVar = framework.getMapping(S_PAGE_NAME);
            Page page = resource.adaptTo(Page.class);
            if (cqVar.equals("pagedata.path")) {
                pageName = page.getProperties().get("pageName",null);
            }
        }
        return pageName;
    }

    public Resource getResource(AnalyticsPageNameContext context) {
        Resource res = null;

        Framework framework = context.getFramework();
        ResourceResolver resolver = context.getResourceResolver();
        String pageName = context.getPageName();
        String basePath = context.getBasePath();

        if (pageName != null && basePath != null && resolver != null
                && framework != null && framework.mapsSCVariable(S_PAGE_NAME)) {
            String cqVar = framework.getMapping(S_PAGE_NAME);
            if (cqVar.equals("pagedata.pagename")) {
                Iterator<Resource>
                hits = resolver.findResources(createQuery(pageName, basePath, "pagename"), Query.JCR_SQL2);
                if (hits.hasNext()) {
                    res = hits.next();
                    res = res.getParent();
                }
            }
        }
        return res;
    }

    private String createQuery(String pageName, String basePath, String propName) {
        return "SELECT * FROM [cq:PageContent] WHERE ISDESCENDANTNODE(["
                + basePath + "]) and [" + propName + "] = \"" + pageName + "\"";
    }
}
```

