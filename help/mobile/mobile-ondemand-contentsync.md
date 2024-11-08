---
title: Mobile avec synchronisation de contenu
description: Consultez cette page pour en savoir plus sur la synchronisation de contenu. Les pages créées dans Adobe Experience Manager (AEM) peuvent être utilisées comme contenu d’application, même lorsque l’appareil est hors ligne. De plus, comme les pages d’AEM sont basées sur des normes web, elles fonctionnent sur plusieurs plateformes et vous permettent de les incorporer dans n’importe quel wrapper natif. Cette stratégie réduit les efforts de développement et vous permet de mettre facilement à jour le contenu de l’application.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: a6e59334-09e2-4bb8-b445-1868035da556
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '2971'
ht-degree: 1%

---

# Mobile avec synchronisation de contenu{#mobile-with-content-sync}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur SPA pour les projets nécessitant un rendu côté client, basé sur un framework, pour une application à une seule page (comme React). [En savoir plus](/help/sites-developing/spa-overview.md).

Utilisez Synchronisation de contenu pour regrouper le contenu afin qu’il puisse être utilisé dans des applications mobiles natives. Les pages créées dans Adobe Experience Manager (AEM) peuvent être utilisées comme contenu d’application, même lorsque l’appareil est hors ligne. De plus, comme les pages d’AEM sont basées sur des normes web, elles fonctionnent sur plusieurs plateformes et vous permettent de les incorporer dans n’importe quel wrapper natif. Cette stratégie réduit les efforts de développement et vous permet de mettre facilement à jour le contenu de l’application.

La structure de synchronisation de contenu crée un fichier d’archive contenant le contenu web. Il peut s’agir de pages simples, d’images et de fichiers de PDF ou d’applications Web complètes. L’API de synchronisation de contenu permet d’accéder au fichier d’archive à partir des applications mobiles ou des processus de création afin que le contenu puisse être récupéré et inclus dans l’application.

La séquence d’étapes suivante illustre un cas d’utilisation typique de la synchronisation de contenu :

1. Le développeur AEM crée une configuration de synchronisation de contenu qui spécifie le contenu à inclure.
1. La structure de synchronisation de contenu collecte et met en cache le contenu.
1. Sur un appareil mobile, l’application mobile est lancée et demande du contenu au serveur, qui est livré dans un fichier ZIP.
1. Le client décompresse le contenu ZIP vers le système de fichiers local. La structure de dossiers dans le fichier ZIP simule les chemins d’accès qu’un client (par exemple, un navigateur) demanderait normalement au serveur.
1. Le client ouvre le contenu dans un navigateur incorporé ou l’utilise d’une autre manière.
1. Par la suite, le client demande du contenu mis à jour au serveur. La structure de synchronisation de contenu fournit des mises à jour incrémentielles afin de réduire la taille et le temps de téléchargement, ce qui peut être important pour les appareils mobiles en raison de la bande passante ou des volumes de données limités.

## Développement des gestionnaires de synchronisation de contenu {#developing-the-content-sync-handlers}

Voici quelques-unes des instructions pour le développement des gestionnaires de synchronisation de contenu :

* Les gestionnaires doivent implémenter *com.day.cq.contentsync.handler.ContentUpdateHandler* (directement ou en étendant une classe qui le fait).
* Les gestionnaires peuvent étendre *com.adobe.cq.mobile.platform.impl.contentsync.handler.AbstractSlingResourceUpdateHandler*
* Le gestionnaire ne doit signaler la valeur true que s’il met à jour le cache ContentSync. La création d’un rapport erroné sur la valeur true a AEM créé une mise à jour lorsqu’une mise à jour n’a pas eu lieu.
* Le gestionnaire ne doit mettre à jour le cache que si le contenu a changé. N’écrivez pas dans le cache si un blanc n’est pas nécessaire. Cela entraîne la création d’une mise à jour inutile.

>[!NOTE]
>
>Activez la *journalisation de débogage de synchronisation de contenu* via les configurations de journalisation OSGI sur le package *com.day.cq.contentsync*. Vous pouvez ainsi effectuer le suivi des gestionnaires exécutés et s’ils ont mis à jour le cache et signalé la mise à jour du cache.

## Configuration du contenu de synchronisation du contenu {#configuring-the-content-sync-content}

Créez une configuration de synchronisation de contenu pour spécifier le contenu du fichier ZIP diffusé au client. Vous pouvez créer un nombre illimité de configurations de synchronisation de contenu. Chaque configuration a un nom à des fins d’identification.

Pour créer une configuration de synchronisation de contenu, ajoutez un noeud `cq:ContentSyncConfig` au référentiel, avec la propriété `sling:resourceType` définie sur `contentsync/config`. Le noeud `cq:ContentSyncConfig` peut se trouver n’importe où dans le référentiel, mais il doit être accessible aux utilisateurs sur l’instance de publication AEM. Par conséquent, vous devez ajouter le noeud sous `/content`.

Pour spécifier le contenu du fichier ZIP de synchronisation de contenu, ajoutez des noeuds enfants au noeud cq:ContentSyncConfig . Les propriétés suivantes de chaque noeud enfant identifient un élément de contenu à inclure et la manière dont il est traité lors de son ajout :

* `path` : emplacement du contenu.
* `type` : nom du type de configuration à utiliser pour le traitement du contenu. Plusieurs types sont disponibles et sont décrits dans la section *Types de configuration*.

Voir *Exemple de configuration de synchronisation de contenu* pour plus d’informations.

Une fois la configuration Synchronisation du contenu créée, elle s’affiche dans la console Synchronisation du contenu .

>[!NOTE]
>
>La structure de synchronisation de contenu ne vérifie pas que les dépendances des ressources et des fichiers liés à la conception sont incluses dans les modules de synchronisation de contenu. Veillez à inclure tous les fichiers requis dans le fichier ZIP.

### Configuration de l’accès aux téléchargements de synchronisation de contenu {#configuring-access-to-content-sync-downloads}

Spécifiez un utilisateur ou un groupe pouvant être téléchargé à partir de la synchronisation de contenu. Vous pouvez configurer l’utilisateur ou le groupe par défaut qui peut être téléchargé à partir de tous les caches de synchronisation de contenu. Vous pouvez également remplacer la valeur par défaut et configurer l’accès pour une configuration de synchronisation de contenu spécifique.

Une fois AEM installé, les membres du groupe de l’administrateur peuvent, par défaut, télécharger depuis Synchronisation du contenu .

#### Définition de l’accès par défaut pour les téléchargements de synchronisation de contenu {#setting-the-default-access-for-content-sync-downloads}

Le service Day CQ Content Sync Manager contrôle l’accès à la synchronisation de contenu. Configurez ce service pour spécifier l’utilisateur ou le groupe pouvant être téléchargé à partir de la synchronisation de contenu par défaut.

Si vous [configurez le service à l’aide de la console web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console), saisissez le nom de l’utilisateur ou du groupe comme valeur de la propriété Fallback Cache Authorizable .

Si vous [configurez dans le référentiel](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository), utilisez les informations suivantes sur le service :

* PID : com.day.cq.contentsync.impl.ContentSyncManagerImpl
* Nom de la propriété : contentsync.fallback.authorizable

#### Remplacement de l’accès au téléchargement pour un cache de synchronisation de contenu {#overriding-download-access-for-a-content-sync-cache}

Pour configurer l’accès au téléchargement pour une configuration de synchronisation de contenu spécifique, ajoutez la propriété suivante au noeud `cq:ContentSyncConfig` :

* Nom : autorisable
* Type : chaîne
* Valeur : nom de l’utilisateur ou du groupe qui peut télécharger.

Par exemple, votre application permet aux utilisateurs d’installer des mises à jour directement à partir de la synchronisation de contenu. Pour permettre à tous les utilisateurs de télécharger la mise à jour, vous définissez la valeur de la propriété autorisable sur `everyone`.

Si le noeud `cq:ContentSyncConfig` ne possède pas de propriété autorisable, l’utilisateur ou le groupe par défaut configuré pour la propriété Fallback Cache Authorizable du service Day CQ Content Sync Manager détermine qui peut effectuer le téléchargement.

### Configuration de l’utilisateur pour la mise à jour d’un cache de synchronisation de contenu {#configuring-the-user-for-updating-a-content-sync-cache}

Lorsqu’un utilisateur effectue une mise à jour du cache de synchronisation de contenu, un compte utilisateur spécifique effectue l’action au nom de l’utilisateur. Par défaut, l’utilisateur anonyme met à jour tous les caches de synchronisation de contenu.

Vous pouvez remplacer l’utilisateur par défaut et spécifier un utilisateur ou un groupe qui met à jour un cache de synchronisation de contenu spécifique.

Pour remplacer l’utilisateur par défaut, spécifiez un utilisateur ou un groupe qui effectue des mises à jour pour une configuration de synchronisation de contenu spécifique en ajoutant la propriété suivante au noeud cq:ContentSyncConfig :

* Nom : `updateuser`
* Type : `String`
* Valeur : nom de l’utilisateur ou du groupe qui peut effectuer les mises à jour.

Si le noeud `cq:ContentSyncConfig` ne possède pas de propriété `updateuser`, l’utilisateur par défaut `anonymous` met à jour le cache.

### Types de configuration {#configuration-types}

Le traitement peut aller du rendu simple JSON au rendu complet des pages, y compris leurs ressources référencées. Cette section répertorie les types de configuration disponibles et leurs paramètres spécifiques :

**copy** - Copier des fichiers et des dossiers.

* **path** - Si le chemin pointe vers un seul fichier, seul le fichier est copié. S’il pointe vers un dossier (y compris les noeuds de page), tous les fichiers et dossiers ci-dessous seront copiés.

**content** Rendu du contenu à l’aide du [traitement de requête Sling](/help/sites-developing/the-basics.md#sling-request-processing) standard.

* **path** - Chemin d’accès à la ressource qui doit être sortie.
* **extension** - Extension qui doit être utilisée dans la requête. *html* et *json* sont des exemples courants, mais toute autre extension est possible.

* **selector** - Sélecteurs facultatifs séparés par un point. Les exemples courants sont *touch* pour le rendu des versions mobiles d’une page ou *infinity* pour la sortie JSON.

**clientlib** - Empaqueter une bibliothèque cliente JavaScript ou CSS.

* **path** - Chemin d’accès à la racine de la bibliothèque cliente.
* **extension** - Type de bibliothèque cliente. Cette valeur doit être définie sur *js* ou *css* pour le moment.

**ressources**

Collectez les rendus originaux des ressources.

* **path** - Chemin d’accès à un dossier de ressources sous /content/dam.

**image** - Collectez une image.

* **path** - Chemin d’accès à une ressource image.

Le type d’image est utilisé pour inclure le logo We Retail dans le fichier zip.

**pages** - Rendu AEM pages et collecte des ressources référencées.

* **path** - Chemin d’accès à une page.
* **extension** - Extension qui doit être utilisée dans la requête. Pour les pages, il s’agit presque toujours de *html*, mais d’autres sont encore possibles.

* **selector** - Sélecteurs facultatifs séparés par un point. *touch* est un exemple courant de rendu des versions mobiles d’une page.

* **deep** - Propriété booléenne facultative déterminant si les pages enfants doivent également être incluses. La valeur par défaut est *true.*

* **includeImages** - Propriété booléenne facultative déterminant si les images doivent être incluses. La valeur par défaut est *true*.

  Par défaut, seuls les composants d’image avec un type de ressource foundation/components/image sont pris en compte pour inclusion. Vous pouvez ajouter d’autres types de ressources en configurant le **gestionnaire de mise à jour des pages WCM Day CQ** dans la console web.

**rewrite** - Le noeud rewrite définit la manière dont les liens sont réécrits dans la page exportée. Les liens réécrits peuvent pointer vers les fichiers inclus dans le fichier compressé ou vers les ressources sur le serveur.

Le noeud `rewrite` doit se trouver sous le noeud `page`.

Le noeud `rewrite` peut avoir une ou plusieurs des propriétés suivantes :

* `clientlibs` : réécrit les chemins clientlibs.

* `images` : réécrit les chemins des images.
* `links` : réécrit les chemins des liens.

Chaque propriété peut avoir l’une des valeurs suivantes :

* `REWRITE_RELATIVE` : réécrit le chemin d’accès avec une position relative dans le fichier .html de la page sur le système de fichiers.

* `REWRITE_EXTERNAL` : réécrit le chemin en pointant vers la ressource du serveur, à l’aide de l’AEM [Externalizer service](/help/sites-developing/externalizer.md).

Le service AEM appelé **PathRewriterTransformerFactory** vous permet de configurer les attributs HTML spécifiques qui seront réécrits. Le service peut être configuré dans la console web et dispose d’une configuration pour chaque propriété du noeud `rewrite` : `clientlibs`, `images` et `links`.

Cette fonctionnalité a été ajoutée à AEM 5.5.

### Exemple de configuration de synchronisation de contenu {#example-content-sync-configuration}

La liste ci-dessous présente un exemple de configuration pour la synchronisation de contenu.

```xml
+ weretail_go [cq:ContentSyncConfig]
  - sling:resourceType = "contentsync/config"

  + etc.designs.default [nt:unstructured]
    - path = "/etc/designs/default"
    - type = "copy"

  + etc.designs.mobile [nt:unstructured]
    - path = "/etc/designs/mobile"
    - type = "copy"

  + events.plist [nt:unstructured]
    - path = "/content/weretail_mobile/en/events/jcr:content/par/events"
    - type = "content"
    - extension = "plist"

  + events.touch.html [nt:unstructured]
    - path = "/content/weretail_mobile/en/events"
    - type = "pages"
    - extension = "html"
    - selector = "touch"

  + logo [nt:unstructured]
    - path = "/etc/designs/mobile/jcr:content/mobilecontentpage/logo"
    - type = "logo"

  + manifest [nt:unstructured]
    - indexPage = "/content/weretail_mobile/en/events.touch.html"
    - metadataPlist = "/content/weretail_mobile/en/events/_jcr_content/par/events.plist"

  + ...
```

**etc.designs.default et etc.designs.mobile** - Les deux premières entrées de la configuration sont évidentes. Comme vous allez inclure plusieurs pages mobiles, vous avez besoin des fichiers de conception associés sous /etc/designs. Et comme aucun traitement supplémentaire n’est nécessaire, la copie est suffisante.

**events.plist** - Cette entrée est un peu spéciale. Comme indiqué dans l’introduction, l’application doit fournir une vue de carte avec les marqueurs des emplacements des événements. Les informations d&#39;emplacement nécessaires seront fournies sous la forme d&#39;un fichier distinct au format PLIST. Pour que cela fonctionne, le composant de liste d’événements utilisé sur la page d’index comporte un script appelé plist.jsp. Ce script est exécuté lorsque la ressource du composant est demandée avec l’extension `.plist`. Comme d’habitude, le chemin d’accès aux composants est indiqué dans la propriété path et le type est défini sur content, car vous souhaitez utiliser le [traitement des requêtes Sling](/help/sites-developing/the-basics.md#sling-request-processing).

**events.touch.html** - Ensuite, les pages réelles affichées dans l’application s’affichent. La propriété path est définie sur la page racine des événements. Toutes les pages d’événement situées sous cette page seront également incluses, car la propriété profonde est définie par défaut sur true. Vous utilisez les pages comme type de configuration, de sorte que toute image ou tout autre fichier pouvant être référencé à partir d’une image ou d’un composant de téléchargement sur une page soit inclus. En outre, le paramétrage du sélecteur tactile nous donne une version mobile des pages. La configuration dans le Feature Pack contient plus d’entrées de ce type, mais elles sont omises pour plus de simplicité ici.

**logo** - Le type de configuration du logo n’a pas été mentionné jusqu’à présent et il n’est pas des types intégrés. Cependant, le framework de synchronisation de contenu est extensible dans une certaine mesure. C’est un exemple de cela, qui sera traité dans la section suivante.

**manifest** - Il est souvent souhaitable d’inclure certains types de métadonnées dans le fichier zip, comme la page de début de votre contenu, par exemple. Cependant, le codage en dur de ces informations vous empêche de les modifier facilement ultérieurement. La structure de synchronisation de contenu prend en charge ce cas d’utilisation en recherchant un noeud manifeste dans la configuration, qui est identifié par son nom et ne nécessite pas de type de configuration. Chaque propriété définie sur ce noeud particulier est ajoutée à un fichier, également appelé manifest et réside à la racine du fichier zip.

Dans cet exemple, la page de liste d’événements est censée être la page initiale. Ces informations sont fournies dans la propriété **indexPage** et peuvent donc être facilement modifiées à tout moment. Une seconde propriété définit le chemin d’accès au fichier *events.plist*. Comme vous le verrez plus tard, l’application cliente peut désormais lire le manifeste et agir en fonction de ce dernier.

Lors de la configuration, le contenu peut être téléchargé avec un navigateur ou tout autre client HTTP. Si vous développez pour iOS, vous pouvez utiliser la bibliothèque cliente WAppKitSync dédiée. L’emplacement de téléchargement est constitué du chemin d’accès de la configuration et de l’extension *.zip*, par exemple lorsque vous utilisez une instance d’AEM locale : *http://localhost:4502/content/weretail_go.zip*

### Console de synchronisation de contenu {#the-content-sync-console}

La console Synchronisation du contenu répertorie toutes les configurations de synchronisation du contenu dans le référentiel (tous les noeuds de type `cq:ContentSyncConfig`) et pour chaque configuration, vous pouvez effectuer les opérations suivantes :

* Mettez à jour le cache.
* Effacez le cache.
* Téléchargez un fichier compressé complet.
* Téléchargez un fichier compressé de comparaison entre maintenant et une date et une heure spécifiques.

Il peut s’avérer utile pour le développement et la résolution des problèmes.

La console est accessible à l’adresse :

`http://localhost:4502/libs/cq/contentsync/content/console.html`

Elle se présente comme suit :

![chlimage_1-50](assets/chlimage_1-50.png)

### Extension de la structure de synchronisation de contenu {#extending-the-content-sync-framework}

Bien que le nombre d’options de configuration soit déjà important, il se peut qu’il ne couvre pas toutes les exigences de votre cas d’utilisation spécifique. Cette section décrit les points d’extension de la structure de synchronisation de contenu et comment créer des types de configuration personnalisés.

Pour chaque type de configuration, il existe un *gestionnaire de mise à jour de contenu*, qui est une fabrique de composants OSGi enregistrée pour ce type spécifique. Ces gestionnaires collectent du contenu, le traitent et l’ajoutent à un cache qui est géré par la structure de synchronisation de contenu. Implémentez l’interface ou la classe de base abstraite suivante :

* `com.day.cq.contentsync.handler.ContentUpdateHandler` - Interface que tous les gestionnaires de mise à jour doivent implémenter
* `com.day.cq.contentsync.handler.AbstractSlingResourceUpdateHandler` - Une classe abstraite qui simplifie le rendu des ressources à l’aide de Sling

Enregistrez votre classe comme fabrique de composants OSGi et déployez-la dans le conteneur OSGi dans un lot. Pour ce faire, utilisez le [module externe Maven SCR](https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/apache-felix-maven-scr-plugin-use.html) en utilisant des balises JavaDoc ou des annotations. L’exemple suivant illustre la version de JavaDoc :

```java
/*
 * @scr.component metatype="no"
 * factory="com.day.cq.contentsync.handler.ContentUpdateHandler/customtype"
 */
public class CustomTypeUpdateHandler implements ContentUpdateHandler {
    // add your code here
}

/*
 * @scr.component metatype="no" inherit="true"
 * factory="com.day.cq.contentsync.handler.ContentUpdateHandler/othertype"
 */
public class OtherTypeUpdateHandler extends AbstractSlingResourceUpdateHandler {
    // add your code here
}
```

Notez que la définition *factory* contient l’interface commune et le type personnalisé séparé par une barre oblique. Cette stratégie permet au framework de synchronisation de contenu de rechercher et de créer une instance de votre classe personnalisée, car elle reconnaît le type personnalisé dans une entrée de configuration. La section suivante fournit un exemple concret de gestionnaire de mise à jour personnalisé.

>[!CAUTION]
>
>Lors de la création de la classe de base AbstractSlingResourceUpdateHandler, vous devez ajouter la définition *inherit*. Sinon, le conteneur OSGi ne définit pas les références requises qui sont déclarées dans la classe de base.

### Mise en oeuvre d’un gestionnaire de mise à jour personnalisé {#implementing-a-custom-update-handler}

Chaque page mobile We.Retail contient un logo dans le coin supérieur gauche qui doit être inclus dans le fichier zip. Toutefois, pour l’optimisation du cache, AEM ne fait pas référence à l’emplacement réel du fichier image dans le référentiel, ce qui nous empêche d’utiliser simplement le type de configuration **copy**. À la place, vous devez fournir votre propre type de configuration **logo** qui rend l’image disponible à l’emplacement demandé par AEM. La liste de code suivante indique l’implémentation complète du gestionnaire de mise à jour du logo :

#### LogoUpdateHandler.java {#logoupdatehandler-java}

```java
package com.day.cq.wcm.apps.weretail.impl;

import javax.jcr.Node;
import javax.jcr.RepositoryException;
import javax.jcr.Session;

import org.apache.sling.api.resource.Resource;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.jcr.resource.JcrResourceResolverFactory;

import com.day.cq.commons.jcr.JcrUtil;
import com.day.cq.contentsync.config.ConfigEntry;
import com.day.cq.contentsync.handler.ContentUpdateHandler;
import com.day.cq.wcm.foundation.Image;
import com.day.text.Text;

/**
 * The <code>LogoUpdateHandler</code> is used to update the content sync cache
 * with a page logo added using a logo component.
 *
 * @scr.component metatype="no"
 * factory="com.day.cq.contentsync.handler.ContentUpdateHandler/logo"
 */
public class LogoUpdateHandler implements ContentUpdateHandler {

    private static final Logger log = LoggerFactory.getLogger(LogoUpdateHandler.class);

    /** @scr.reference policy="static" */
    protected JcrResourceResolverFactory resolverFactory;

    public boolean updateCacheEntry(ConfigEntry configEntry, Long lastUpdated, String configCacheRoot, Session admin, Session session) {
        ResourceResolver resolver = resolverFactory.getResourceResolver(admin);
        Resource resource = resolver.getResource(configEntry.getContentPath());

        Image img = new Image(resource);
        img.setItemName(Image.NN_FILE, "image");
        img.setItemName(Image.PN_REFERENCE, "imageReference");
        img.setSelector("img");

        try {
            if(img.getLastModified() == null || lastUpdated < img.getLastModified().getTime().getTime()) {
                String src = img.getSrc();
                String parentPath = configCacheRoot + Text.getRelativeParent(src, 1);

                Node parent = JcrUtil.createPath(parentPath, "sling:Folder", admin);
                Node image = resolver.getResource(resource.getPath() + "/image").adaptTo(Node.class);
                JcrUtil.copy(image, parent, Text.getName(src));

                admin.save();

                return true;
            }
        } catch (RepositoryException e) {
            log.error("Unexpected error while updating logo: ", e);
        }

        return false;
    }
}
```

La classe `LogoUpdateHandler` met en oeuvre la méthode `updateCacheEntry(ConfigEntry, Long, String, Session, Session)` de l’interface `ContentUpdateHandler`, qui prend plusieurs arguments :

* Une instance `ConfigEntry` qui permet d’accéder à l’entrée de configuration, pour laquelle ce gestionnaire est appelé, et à ses propriétés.
* Un horodatage `lastUpdated` indiquant la dernière fois que la synchronisation de contenu a mis à jour son cache. Le contenu qui n’a pas été modifié après cet horodatage ne doit pas être mis à jour par le gestionnaire.
* Un argument `configCacheRoot` qui spécifie le chemin racine du cache. Tous les fichiers mis à jour doivent être stockés sous ce chemin pour être ajoutés au fichier zip.
* Session d’administration qui doit être utilisée pour toutes les opérations de référentiel liées au cache.
* Session utilisateur pouvant être utilisée pour mettre à jour le contenu dans le contexte d’un utilisateur spécifique et ainsi fournir une sorte de contenu personnalisé.

Pour implémenter le gestionnaire personnalisé, créez d’abord une instance de la classe Image en fonction de la ressource fournie dans l’entrée de configuration. Il s’agit de la même procédure que le composant Logo réel sur nos pages. Il s’assure que le chemin cible de l’image est identique à celui référencé à partir d’une page.

Vérifiez ensuite si la ressource a été modifiée depuis la dernière mise à jour. Les implémentations personnalisées doivent éviter les mises à jour inutiles du cache et renvoyer la valeur false si rien ne change. Si la ressource a été modifiée, copiez l’image vers l’emplacement cible attendu par rapport à la racine du cache. Enfin, `true` est renvoyé pour indiquer à la structure que le cache a été mis à jour.

## Utiliser le contenu sur le client {#using-the-content-on-the-client}

Pour utiliser du contenu dans une application mobile fournie par la synchronisation de contenu, vous devez demander le contenu au moyen d’une connexion HTTP ou HTTPS. Par conséquent, le contenu récupéré (compressé dans un fichier ZIP) peut être extrait et stocké localement sur l’appareil mobile. Le contenu fait non seulement référence à des données, mais aussi à la logique, c’est-à-dire à des applications web complètes. Il permet donc à l’utilisateur mobile d’exécuter des applications web récupérées et les données correspondantes, même sans connectivité réseau.

La synchronisation de contenu permet de diffuser intelligemment le contenu : seules les modifications apportées aux données depuis la dernière synchronisation des données réussie sont diffusées, ce qui réduit le temps nécessaire au transfert des données. Lors de la première exécution d’une application, des modifications de données sont demandées depuis le 1er janvier 1970, tandis que seules les données modifiées depuis la dernière synchronisation réussie sont demandées ultérieurement. AEM utilise une structure de communication client pour iOS afin de simplifier la communication et le transfert des données, de sorte qu’un minimum de code natif est nécessaire pour activer une application web iOS.

Toutes les données transférées peuvent être extraites dans la même structure de répertoires. Aucune étape supplémentaire (par exemple, les contrôles de dépendance) n’est nécessaire lors de l’extraction des données. S’il existe iOS, toutes les données sont stockées dans un sous-dossier du dossier Documents de l’application iOS.

Chemin d’exécution type d’une application AEM Mobile basée sur iOS :

* L’utilisateur démarre l’application sur un appareil iOS.
* L’application tente de se connecter à AEM serveur principal et demande des modifications de données depuis la dernière exécution.
* Le serveur récupère les données en question et les archive dans un fichier.
* Les données sont renvoyées au périphérique client où elles sont extraites dans le dossier documents.
* Le composant UIWebView démarre/actualise.

Si une connexion n’a pas pu être établie précédemment, les données téléchargées s’affichent.

### Ressources supplémentaires {#additional-resources}

Pour en savoir plus sur les rôles et les responsabilités d’un administrateur et d’un auteur, consultez les ressources ci-dessous :

* [Création de contenu AEM pour AEM Mobile On-demand Services](/help/mobile/mobile-apps-ondemand.md)
* [Administration de contenu pour l’utilisation d’AEM Mobile On-demand Services](/help/mobile/aem-mobile.md)
