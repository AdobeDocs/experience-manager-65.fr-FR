---
title: Implémentation de la dénomination des pages côté serveur pour Analytics
seo-title: Implementing Server-Side Page Naming for Analytics
description: Adobe Analytics utilise la propriété s.pageName pour identifier de manière unique les pages et associer les données collectées pour les pages.
seo-description: Adobe Analytics uses the s.pageName property to uniquely identify pages and to associate the data that is collected for the pages
uuid: 37b92099-0cce-4b2d-b55c-928f636dbd7e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: be2aa297-5b78-4b1d-8ff1-e6a585a177dd
exl-id: 17a4e4dc-804e-44a9-9942-c37dbfc8016f
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 73%

---

# Implémentation de la nomination des pages côté serveur pour Analytics{#implementing-server-side-page-naming-for-analytics}

Adobe Analytics utilise la propriété `s.pageName` pour identifier les pages de façon unique et pour associer les données qui sont collectées pour les pages. En règle générale, vous effectuez les tâches suivantes dans AEM afin d’attribuer à cette propriété une valeur qu’AEM envoie à Analytics :

* Utilisez le framework de service cloud Analytics pour mapper une variable CQ sur la propriété `s.pageName` Analytics. (Voir [Mappage des données de composant vers les propriétés Adobe Analytics](/help/sites-administering/adobeanalytics-mapping.md).)

* Créez le composant de page de sorte qu’il contienne la variable CQ que vous mappez sur la propriété `s.pageName` (Voir [Mise en œuvre du suivi Adobe Analytics pour les composants personnalisés](/help/sites-developing/extending-analytics-components.md)).

Pour afficher les données de rapport Analytics dans la console Sites et dans Content Insight, AEM a besoin de la valeur de la propriété `s.pageName` pour chaque page. L’API Java AEM Analytics définit l’interface `AnalyticsPageNameProvider` que vous mettez en œuvre pour fournir la valeur de la propriété `s.pageName` à la console Sites et à Content Insight. Votre `AnaltyicsPageNameProvider` Le service résout la propriété pageName sur le serveur à des fins de création de rapports, car elle peut être définie dynamiquement à l’aide de JavaScript sur le client à des fins de suivi.

## Service Fournisseur de noms de page Analytics par défaut {#the-default-analytics-page-name-provider-service}

Le service `DefaultPageNameProvider` est le service par défaut qui détermine la valeur de la propriété `s.pageName` à utiliser pour récupérer des données Analytics pour une page. Ce service fonctionne de concert avec le composant de page de base AEM (`/libs/foundation/components/page`). Ce composant de page définit les variables CQ suivantes qui sont censées être mappées sur la propriété `s.pageName` :

* `pagedata.path` : la valeur est définie sur le chemin d’accès de la page.
* `pagedata.title` : la valeur est définie sur le titre de la page.
* `pagedata.navTitle` : la valeur est définie sur le titre de navigation de la page.

Le service `DefaultPageNameProvider` détermine laquelle des variables CQ est mappée sur la propriété `s.pageName` dans le framework de service cloud Analytics. Il détermine ensuite la propriété de page appropriée à utiliser pour récupérer les données de rapport Analytics :

* `pagedata.path` : le service utilise `page.getPath()`.

* `pagedata.title` : le service utilise `page.getTitle()`

* `pagedata.navTitle` : le service utilise `page.getNavigationTitle()`

L’objet `page` est l’objet [`com.day.cq.wcm.api.Page`Java ](https://helpx.adobe.com/fr/experience-manager/6-3/sites-developing/reference-materials/javadoc/com/day/cq/wcm/api/Page.html) de la page.

Si vous ne mappez pas de variable CQ sur la propriété `s.pageName` dans le framework, la valeur de `s.pageName` est générée à partir du chemin d’accès de la page. Par exemple, la page dont le chemin d’accès est `/content/geometrixx/en` utilise la valeur `content:geometrixx:en` pour la propriété `s.pageName`.

>[!NOTE]
>
>Le service DefaultPageNameProvider utilise un classement de service de 100.

## Maintien de la continuité dans les rapports Analytics {#maintaining-continuity-in-analytics-reporting}

Pour conserver un historique complet des données d’analyse pour une page, la valeur de la propriété s.pageName utilisée pour une page ne change jamais. Toutefois, les propriétés d’analyse que le composant de page de base définit peuvent être facilement modifiées. Par exemple, le déplacement d’une page modifie la valeur de `pagedata.path` et rompt la continuité de l’historique des rapports :

* Les données collectées pour le chemin précédent ne sont plus associées à la page.
* Si une autre page utilise le chemin d’accès utilisé par une autre page, la autre page hérite des données de ce chemin.

Pour garantir la continuité des rapports, la valeur de la propriété `s.pageName` doit présenter les caractéristiques suivantes :

* Unique.
* Stable.
* Lisible par un humain.

Par exemple, un composant de page personnalisé peut inclure une propriété de page que les auteurs utilisent pour spécifier un identifiant unique pour la page utilisée comme valeur pour la propriété `s.pageProperties` :

* La page inclut une variable Analytics qui est définie sur la valeur de l’identifiant unique stockée dans la propriété de page.
* La variable Analytics est mappée sur la propriété `s.pageProperties` dans le framework Analytics.
* Votre implémentation de l’interface AnalyticsPageNameProvider récupère la valeur de la propriété de page à utiliser pour interroger les données Analytics de la page.

>[!NOTE]
>
>Demandez l’aide de votre conseiller Analytics pour développer une stratégie efficace pour votre valeur `s.pageName`.

### Mise en œuvre d’un service Fournisseur de noms de page Analytics {#implementing-an-analytics-page-name-provider-service}

Implémentez l’interface `com.day.cq.analytics.sitecatalyst.AnalyticsPageNameProvider` en tant que service OSGi pour personnaliser la logique qui récupère la valeur de la propriété `s.pageName`. Les analyses de page Sites et Content Insight utilisent le service pour récupérer les données de rapport d’Analytics.

L’interface AnalyticsPageNameProvider définit deux méthodes que vous devez implémenter :

* `getPageName` : renvoie une valeur `String` qui représente la valeur à utiliser comme propriété `s.pageName`.

* `getResource` : renvoie un objet `org.apache.sling.api.resource.Resource` qui représente la page associée à la propriété `s.pageName`.

Les deux méthodes utilisent un objet `com.day.cq.analytics.sitecatalyst.AnalyticsPageNameContext` comme paramètre. La classe `AnalyticsPageNameContext` fournit des informations sur le contexte des appels Analytics :

* Chemin de base de la ressource de page
* Objet `Framework` pour la configuration du service cloud Analytics
* Objet `Resource` pour la page
* Objet `ResourceResolver` pour la page

La classe fournit également un paramètre pour le nom de page.

### Exemple d’implémentation d’AnalyticsPageNameProvider {#example-analyticspagenameprovider-implementation}

L’exemple d’implémentation d’`AnalyticsPageNameProvider` suivant prend en charge un composant de page personnalisé :

* Le composant étend le composant de page de base.
* La boîte de dialogue contient un champ que les auteurs utilisent pour spécifier la valeur de la propriété `s.pageName`.
* La valeur de la propriété est stockée dans la propriété pageName du nœud `jcr:content` des instances de la page.
* La propriété Analytics qui stocke la propriété `s.pageName` est appelée `pagedata.pagename`. Elle est mappée sur la propriété `s.pageName` dans le framework Analytics.

L’implémentation suivante de la méthode `getPageName` renvoie la valeur de la propriété du nœud pageName si le mappage de framework est correctement configuré :

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

L’implémentation suivante de la méthode getResource renvoie l’objet Resource pour la page :

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

Le code suivant représente la classe entière, y compris les annotations SCR qui configurent le service. Le rang de service est 200, ce qui remplace le service par défaut.

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
