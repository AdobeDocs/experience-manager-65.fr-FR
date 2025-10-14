---
title: Mobile avec synchronisation de contenu
description: Consultez cette page pour en savoir plus sur la synchronisation du contenu. Les pages créées dans Adobe Experience Manager (AEM) peuvent être utilisées comme contenu d’application, même lorsque l’appareil est hors ligne. En outre, comme les pages AEM sont basées sur des normes web, elles fonctionnent sur plusieurs plateformes, ce qui vous permet de les incorporer dans n’importe quel wrapper natif. Cette stratégie réduit les efforts de développement et vous permet de mettre facilement à jour le contenu de l’application.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: a6e59334-09e2-4bb8-b445-1868035da556
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '2950'
ht-degree: 1%

---

# Mobile avec synchronisation de contenu{#mobile-with-content-sync}

{{ue-over-mobile}}

Utilisez la synchronisation de contenu pour compresser le contenu afin qu’il puisse être utilisé dans les applications mobiles natives. Les pages créées dans Adobe Experience Manager (AEM) peuvent être utilisées comme contenu d’application, même lorsque l’appareil est hors ligne. En outre, comme les pages AEM sont basées sur des normes web, elles fonctionnent sur plusieurs plateformes, ce qui vous permet de les incorporer dans n’importe quel wrapper natif. Cette stratégie réduit les efforts de développement et vous permet de mettre facilement à jour le contenu de l’application.

La structure de synchronisation du contenu crée un fichier d’archive contenant le contenu web. Le contenu peut être constitué de pages simples, d’images, de fichiers de PDF ou d’applications web complètes. L’API de synchronisation du contenu permet d’accéder au fichier d’archive à partir d’applications mobiles ou de processus de création afin que le contenu puisse être récupéré et inclus dans l’application.

La séquence d’étapes suivante illustre un cas d’utilisation type de la synchronisation de contenu :

1. Le développeur AEM crée une configuration de synchronisation du contenu qui spécifie le contenu à inclure.
1. Le framework de synchronisation du contenu collecte et met en cache le contenu.
1. Sur un appareil mobile, l’application mobile est démarrée et demande le contenu au serveur, qui le diffuse dans un fichier ZIP.
1. Le client décompresse le contenu ZIP dans le système de fichiers local. La structure de dossiers dans le fichier ZIP simule les chemins d’accès qu’un client (par exemple, un navigateur) demande normalement au serveur.
1. Le client ou la cliente ouvre le contenu dans un navigateur intégré ou l’utilise d’une autre manière.
1. Par la suite, le client demande du contenu mis à jour au serveur. Le framework de synchronisation du contenu fournit des mises à jour incrémentielles pour réduire la taille et la durée du téléchargement, ce qui peut être important pour les appareils mobiles en raison de la bande passante limitée ou des volumes de données.

## Développement des gestionnaires de synchronisation de contenu {#developing-the-content-sync-handlers}

Voici quelques instructions pour développer des gestionnaires de synchronisation de contenu :

* Les gestionnaires doivent mettre en œuvre *com.day.cq.contentsync.handler.ContentUpdateHandler* (directement ou en étendant une classe qui le fait)
* Les gestionnaires peuvent étendre *com.adobe.cq.mobile.platform.impl.contentsync.handler.AbstractSlingResourceUpdateHandler*
* Le gestionnaire ne doit renvoyer la valeur true que s’il met à jour le cache ContentSync. Si la déclaration est fausse, AEM crée une mise à jour alors qu’aucune mise à jour ne s’est réellement produite.
* Le gestionnaire ne doit mettre à jour le cache que si le contenu a été modifié. N’écrivez pas dans le cache si un blanc n’est pas nécessaire. Cela entraîne la création d’une mise à jour inutile.

>[!NOTE]
>
>Activez la *journalisation du débogage ContentSync* via les configurations de journal OSGI sur le package *com.day.cq.contentsync*. Vous pouvez ainsi suivre les gestionnaires exécutés et s’ils ont mis à jour le cache et signalé la mise à jour du cache.

## Configuration du contenu de synchronisation du contenu {#configuring-the-content-sync-content}

Créez une configuration de synchronisation du contenu pour spécifier le contenu du fichier ZIP envoyé au client. Vous pouvez créer un nombre illimité de configurations de synchronisation de contenu. Chaque configuration possède un nom à des fins d’identification.

Pour créer une configuration de synchronisation du contenu, ajoutez un nœud `cq:ContentSyncConfig` au référentiel, avec la propriété `sling:resourceType` définie sur `contentsync/config`. Le nœud `cq:ContentSyncConfig` peut se trouver n’importe où dans le référentiel, mais il doit être accessible aux utilisateurs de l’instance de publication AEM. Par conséquent, vous devez ajouter le nœud sous `/content`.

Pour spécifier le contenu du fichier ZIP de synchronisation du contenu, ajoutez des nœuds enfants au nœud cq:ContentSyncConfig. Les propriétés suivantes de chaque nœud enfant identifient un élément de contenu à inclure et la manière dont il est traité lors de son ajout :

* `path` : emplacement du contenu.
* `type` : nom du type de configuration à utiliser pour le traitement du contenu. Plusieurs types sont disponibles et sont décrits dans la section *Types de configuration*.

Voir *Exemple de configuration de synchronisation de contenu* pour plus d’informations.

Une fois la configuration de synchronisation du contenu créée, elle s’affiche dans la console de synchronisation du contenu.

>[!NOTE]
>
>Le framework de synchronisation du contenu ne vérifie pas que les dépendances des ressources et des fichiers liés à la conception sont incluses dans les packages de synchronisation du contenu. Veillez à inclure tous les fichiers requis dans le fichier ZIP.

### Configuration de l’accès aux téléchargements de synchronisation de contenu {#configuring-access-to-content-sync-downloads}

Spécifiez un utilisateur ou un groupe pouvant être téléchargé à partir de la synchronisation de contenu. Vous pouvez configurer l’utilisateur ou le groupe par défaut qui peut effectuer le téléchargement à partir de tous les caches de synchronisation de contenu. Vous pouvez également remplacer le paramètre par défaut et configurer l’accès pour une configuration de synchronisation de contenu spécifique.

Lors de l’installation d’AEM, les membres du groupe d’administration peuvent par défaut effectuer des téléchargements à partir de la synchronisation de contenu.

#### Définition de l’accès par défaut aux téléchargements de synchronisation de contenu {#setting-the-default-access-for-content-sync-downloads}

Le service Day CQ Content Sync Manager contrôle l’accès à la synchronisation de contenu. Configurez ce service pour spécifier l’utilisateur, l’utilisatrice ou le groupe qui peut être téléchargé à partir de la synchronisation de contenu par défaut.

Si vous [configurez le service à l’aide de la console web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console), saisissez le nom de l’utilisateur ou du groupe comme valeur de la propriété Autorisable du cache de secours.

Si vous [configurez dans le référentiel](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository), utilisez les informations suivantes sur le service :

* PID : com.day.cq.contentsync.impl.ContentSyncManagerImpl
* Nom de la propriété : contentsync.fallback.authorizable

#### Remplacement de l’accès au téléchargement pour un cache de synchronisation de contenu {#overriding-download-access-for-a-content-sync-cache}

Pour configurer l’accès aux téléchargements pour une configuration de synchronisation de contenu spécifique, ajoutez la propriété suivante au nœud `cq:ContentSyncConfig` :

* Nom : autorisable
* Type : chaîne
* Valeur : nom de l’utilisateur ou du groupe pouvant être téléchargé.

Par exemple, votre application permet aux utilisateurs d’installer des mises à jour directement à partir de la synchronisation de contenu. Pour permettre à tous les utilisateurs de télécharger la mise à jour, définissez la valeur de la propriété autorisable sur `everyone`.

Si le nœud `cq:ContentSyncConfig` ne possède aucune propriété autorisable, l’utilisateur ou le groupe par défaut configuré pour la propriété Autorisable du cache de secours du service Day CQ Content Sync Manager détermine qui peut effectuer le téléchargement.

### Configuration de l’utilisateur pour la mise à jour d’un cache de synchronisation de contenu {#configuring-the-user-for-updating-a-content-sync-cache}

Lorsqu’un utilisateur ou une utilisatrice effectue une mise à jour du cache de synchronisation du contenu, un compte d’utilisateur spécifique effectue l’action au nom de l’utilisateur ou de l’utilisatrice. L’utilisateur anonyme met à jour tous les caches de synchronisation de contenu par défaut.

Vous pouvez remplacer l’utilisateur par défaut et spécifier un utilisateur ou un groupe qui met à jour un cache de synchronisation de contenu spécifique.

Pour remplacer l’utilisateur par défaut, spécifiez un utilisateur ou un groupe qui effectue des mises à jour pour une configuration de synchronisation de contenu spécifique en ajoutant la propriété suivante au nœud cq:ContentSyncConfig :

* Nom : `updateuser`
* Type : `String`
* Valeur : nom de l’utilisateur ou du groupe pouvant effectuer les mises à jour.

Si le nœud `cq:ContentSyncConfig` ne comporte aucune propriété `updateuser`, l’utilisateur `anonymous` par défaut met à jour le cache.

### Types de configuration {#configuration-types}

Le traitement peut aller du rendu JSON simple au rendu complet des pages, y compris leurs ressources référencées. Cette section répertorie les types de configuration disponibles et leurs paramètres spécifiques :

**copy** - Copiez des fichiers et des dossiers.

* **path** - Si le chemin d’accès pointe vers un seul fichier, seul le fichier est copié. S’il pointe vers un dossier (cela inclut les nœuds de page), tous les fichiers et dossiers situés sous seront copiés.

**content** Effectuez le rendu du contenu à l’aide du [traitement des requêtes Sling](/help/sites-developing/the-basics.md#sling-request-processing) standard.

* **path** - Chemin d’accès à la ressource qui doit être générée.
* **extension** - Extension qui doit être utilisée dans la requête. Les exemples les plus courants sont *html* et *json*, mais toute autre extension est possible.

* **selector** - Sélecteurs facultatifs séparés par un point. Les exemples les plus courants sont *tactile* pour le rendu des versions mobiles d’une page ou *infinité* pour la sortie JSON.

**clientlib** - Compressez une bibliothèque cliente JavaScript ou CSS.

* **path** - Chemin d’accès à la racine de la bibliothèque cliente.
* **extension** - Type de bibliothèque cliente. Cette valeur doit être définie sur *js* ou *css* pour le moment.

**ressources**

Collectez les rendus originaux des ressources.

* **path** - Chemin d’accès à un dossier de ressources sous /content/dam.

**image** - Collectez une image.

* **path** - Chemin d’accès à une ressource image.

Le type d’image est utilisé pour inclure le logo We Retail dans le fichier zip.

**pages** - Effectuez le rendu des pages AEM et collectez les ressources référencées.

* **path** - Chemin d’accès à une page.
* **extension** - Extension qui doit être utilisée dans la requête. Pour les pages, cette fonctionnalité est presque toujours *html*, mais d’autres sont toujours possibles.

* **selector** - Sélecteurs facultatifs séparés par un point. Les exemples les plus courants sont *touch* pour le rendu des versions mobiles d’une page.

* **deep** - Propriété booléenne facultative déterminant si les pages enfants doivent également être incluses. La valeur par défaut est *true.*

* **includeImages** - Propriété booléenne facultative déterminant si les images doivent être incluses. La valeur par défaut est *true*.

  Par défaut, seuls les composants d’image dont le type de ressource est foundation/components/image sont pris en compte pour l’inclusion. Vous pouvez ajouter d’autres types de ressources en configurant le **gestionnaire de mise à jour des pages de gestion de contenu web Day CQ** dans la console Web.

**rewrite** - le nœud rewrite définit la façon dont les liens sont réécrits dans la page exportée. Les liens réécrits peuvent pointer vers les fichiers inclus dans le fichier compressé ou vers les ressources sur le serveur.

Le nœud `rewrite` doit se trouver sous le nœud `page` .

Le nœud `rewrite` peut posséder une ou plusieurs des propriétés suivantes :

* `clientlibs` : réécrit les chemins d’accès clientlibs.

* `images` : réécrit les chemins d’accès aux images.
* `links` : réécrit les chemins d’accès aux liens.

Chaque propriété peut avoir l’une des valeurs suivantes :

* `REWRITE_RELATIVE` : réécrit le chemin d’accès avec une position relative dans le fichier .html de la page sur le système de fichiers.

* `REWRITE_EXTERNAL` : réécrit le chemin d’accès en pointant vers la ressource sur le serveur, à l’aide du service AEM [Externalizer](/help/sites-developing/externalizer.md).

Le service AEM nommé **PathRewriterTransformerFactory** vous permet de configurer les attributs html spécifiques qui seront réécrits. Le service peut être configuré dans la console web et comporte une configuration pour chaque propriété du nœud `rewrite` : `clientlibs`, `images` et `links`.

Cette fonctionnalité a été ajoutée dans AEM 5.5.

### Exemple de configuration de synchronisation de contenu {#example-content-sync-configuration}

La liste ci-dessous présente un exemple de configuration de la synchronisation de contenu.

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

**etc.designs.default et etc.designs.mobile** - Les deux premières entrées de la configuration sont évidentes. Comme vous allez inclure plusieurs pages mobiles, vous avez besoin des fichiers de conception associés sous /etc/designs. Et puisqu’aucun traitement supplémentaire n’est requis, la copie est suffisante.

**events.plist** - Cette entrée est un peu spéciale. Comme mentionné en introduction, l’application doit fournir une vue cartographique avec des marqueurs des lieux des événements. Les renseignements nécessaires sur l&#39;emplacement seront fournis dans un fichier distinct au format PLIST. Pour que cela fonctionne, le composant Liste d’événements utilisé sur la page d’index comporte un script appelé plist.jsp. Ce script est exécuté lorsque la ressource du composant est demandée avec l’extension `.plist`. Comme d’habitude, le chemin d’accès aux composants est indiqué dans la propriété path et le type est défini sur content , car vous souhaitez utiliser le traitement des requêtes [&#x200B; Sling &#x200B;](/help/sites-developing/the-basics.md#sling-request-processing).

**events.touch.html** - Viennent ensuite les pages proprement dites qui s’affichent dans l’application. La propriété de chemin est définie sur la page racine des événements. Toutes les pages d’événement situées sous cette page seront également incluses, car la propriété deep est définie par défaut sur true. Vous utilisez les pages comme type de configuration. Ainsi, toutes les images ou autres fichiers pouvant être référencés à partir d’un composant d’image ou de téléchargement sur une page sont inclus. En outre, la définition du sélecteur tactile nous donne une version mobile des pages. La configuration du pack de fonctionnalités contient d’autres entrées de ce type, mais elles sont laissées de côté pour des raisons de simplicité.

**logo** - Le type de configuration du logo n&#39;a pas été mentionné jusqu&#39;à présent et il ne s&#39;agit d&#39;aucun des types intégrés. Cependant, le framework de synchronisation du contenu est extensible dans une certaine mesure. Il s’agit d’un exemple de cela, qui sera traité dans la section suivante.

**manifeste** - Il est souvent souhaitable d’inclure un certain type de métadonnées dans le fichier zip, comme la page de début de votre contenu par exemple. Cependant, le codage en dur de ces informations vous empêche de les modifier facilement ultérieurement. La structure de synchronisation du contenu prend en charge ce cas d’utilisation en recherchant un nœud de manifeste dans la configuration, qui est identifié par son nom et ne nécessite pas de type de configuration. Chaque propriété définie sur ce nœud particulier est ajoutée à un fichier, qui est également appelé manifeste et réside à la racine du fichier zip.

Dans cet exemple, la page de liste des événements est censée être la page initiale. Ces informations sont fournies dans la propriété **indexPage** et peuvent donc être facilement modifiées à tout moment. Une deuxième propriété définit le chemin d’accès du fichier *events.plist*. Comme vous le verrez plus loin, l’application cliente peut désormais lire le manifeste et agir en conséquence.

Lorsque la configuration est terminée, le contenu peut être téléchargé avec un navigateur ou tout autre client HTTP. Si vous développez pour iOS, vous pouvez également utiliser la bibliothèque cliente WAppKitSync dédiée. L’emplacement de téléchargement est constitué du chemin d’accès de la configuration et de l’extension *.zip*, par exemple, lorsque vous utilisez une instance AEM locale : *http://localhost:4502/content/weretail_go.zip*

### Console de synchronisation du contenu {#the-content-sync-console}

La console de synchronisation du contenu répertorie toutes les configurations de synchronisation du contenu dans le référentiel (tous les nœuds de type `cq:ContentSyncConfig`) et, pour chaque configuration, vous pouvez effectuer les opérations suivantes :

* Mettez à jour le cache.
* Effacez le cache.
* Téléchargez un fichier zip complet.
* Téléchargez un fichier zip diff entre maintenant et une date et une heure spécifiques.

Cela peut s’avérer utile pour le développement et le dépannage.

La console est accessible à l’adresse :

`http://localhost:4502/libs/cq/contentsync/content/console.html`

Elle se présente comme suit :

![chlimage_1-50](assets/chlimage_1-50.png)

### Étendre le framework de synchronisation du contenu {#extending-the-content-sync-framework}

Bien que le nombre d’options de configuration soit déjà important, il se peut qu’elles ne couvrent pas toutes les exigences de votre cas d’utilisation spécifique. Cette section décrit les points d’extension du framework de synchronisation de contenu et comment créer des types de configuration personnalisés.

Pour chaque type de configuration, il existe un *gestionnaire de mise à jour de contenu*, qui est une fabrique de composants OSGi enregistrée pour ce type spécifique. Ces gestionnaires collectent le contenu, le traitent et l’ajoutent à un cache géré par le framework de synchronisation de contenu. Implémentez l’interface suivante ou la classe de base abstraite :

* `com.day.cq.contentsync.handler.ContentUpdateHandler` - Interface que tous les gestionnaires de mise à jour doivent implémenter
* `com.day.cq.contentsync.handler.AbstractSlingResourceUpdateHandler` - Classe abstraite qui simplifie le rendu des ressources à l’aide de Sling

Enregistrez votre classe en tant que fabrique de composants OSGi et déployez-la dans le conteneur OSGi d’un lot. Vous pouvez le faire à l’aide du [plug-in Maven SCR](https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/apache-felix-maven-scr-plugin-use.html) à l’aide de balises JavaDoc ou d’annotations. L’exemple suivant illustre la version de JavaDoc :

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

Notez que la définition *factory* contient l&#39;interface commune et le type personnalisé séparés par une barre oblique. Cette stratégie permet au framework de synchronisation du contenu de rechercher et de créer une instance de votre classe personnalisée, car elle reconnaît le type personnalisé dans une entrée de configuration. La section suivante donne un exemple concret de gestionnaire de mise à jour personnalisé.

>[!CAUTION]
>
>Lors de la création sur la classe de base AbstractSlingResourceUpdateHandler, vous devez ajouter la définition *inherit*. Sinon, le conteneur OSGi ne définira pas les références requises qui sont déclarées dans la classe de base.

### Mise en œuvre d’un gestionnaire de mise à jour personnalisé {#implementing-a-custom-update-handler}

Chaque page We.Retail Mobile contient un logo dans le coin supérieur gauche qui doit être inclus dans le fichier zip. Toutefois, pour l’optimisation du cache, AEM ne fait pas référence à l’emplacement réel du fichier image dans le référentiel, ce qui nous empêche d’utiliser simplement le type de configuration **copy**. Vous devez plutôt fournir votre propre type de configuration **logo** qui rend l’image disponible à l’emplacement demandé par AEM. La liste de codes suivante montre l’implémentation complète du gestionnaire de mise à jour du logo :

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

La classe `LogoUpdateHandler` implémente la méthode `updateCacheEntry(ConfigEntry, Long, String, Session, Session)` de l’interface `ContentUpdateHandler`, qui utilise plusieurs arguments :

* Une instance `ConfigEntry` qui permet d’accéder à l’entrée de configuration pour laquelle ce gestionnaire est appelé et à ses propriétés.
* Date et heure `lastUpdated` indiquant la dernière fois que la synchronisation de contenu a mis à jour son cache. Le contenu qui n’a pas été modifié après cette date et heure ne doit pas être mis à jour par le gestionnaire.
* Un argument `configCacheRoot` qui spécifie le chemin d’accès racine du cache. Tous les fichiers mis à jour doivent être stockés sous ce chemin d’accès pour être ajoutés au fichier zip.
* Session administrative qui doit être utilisée pour toutes les opérations de référentiel liées au cache.
* Une session utilisateur qui peut être utilisée pour mettre à jour le contenu dans le contexte d’un certain utilisateur et fournir ainsi un type de contenu personnalisé.

Pour implémenter le gestionnaire personnalisé, commencez par créer une instance de la classe Image en fonction de la ressource fournie dans l’entrée de configuration. Il s’agit de la même procédure que pour le composant Logo proprement dit sur nos pages. Cela permet de s’assurer que le chemin d’accès cible de l’image est identique à celui référencé à partir d’une page.

Ensuite, vérifiez si la ressource a été modifiée depuis la dernière mise à jour. Les implémentations personnalisées doivent éviter les mises à jour inutiles du cache et renvoyer la valeur false si rien ne change. Si la ressource a été modifiée, copiez l’image à l’emplacement cible attendu par rapport à la racine du cache. Enfin, `true` est renvoyée pour indiquer au framework que le cache a été mis à jour.

## Utiliser le contenu sur le client {#using-the-content-on-the-client}

Pour utiliser le contenu dans une application mobile fournie par la synchronisation de contenu, vous devez demander le contenu au moyen d’une connexion HTTP ou HTTPS. Par conséquent, le contenu récupéré (compressé dans un fichier ZIP) peut être extrait et stocké localement sur l’appareil mobile. Le contenu fait non seulement référence aux données, mais également à la logique, c’est-à-dire aux applications web complètes. Par conséquent, il permet à l’utilisateur mobile d’exécuter les applications web récupérées et les données correspondantes, même sans connectivité réseau.

La synchronisation de contenu diffuse le contenu de manière intelligente : seules les données changent depuis la dernière synchronisation de données réussie, ce qui réduit le temps nécessaire au transfert des données. Lors de la première exécution d’une application, les modifications de données sont demandées à partir du 1er janvier 1970, tandis que, par la suite, seules les données modifiées depuis la dernière synchronisation réussie sont demandées. AEM utilise une structure de communication client pour iOS afin de simplifier la communication et le transfert de données, de sorte qu’un minimum de code natif soit nécessaire pour activer une application web basée sur iOS.

Toutes les données transférées peuvent être extraites dans la même structure de répertoires. Aucune étape supplémentaire (par exemple, les contrôles de dépendance) n’est nécessaire lors de l’extraction des données. S’il existe iOS, toutes les données sont stockées dans un sous-dossier au sein du dossier Documents de l’application iOS.

Chemin d’exécution standard d’une application AEM Mobile basée sur iOS :

* L’utilisateur démarre l’application sur l’appareil iOS.
* L’application tente de se connecter au serveur principal AEM et demande des modifications de données depuis la dernière exécution.
* Le serveur récupère les données en question et les compresse dans un fichier.
* Les données sont renvoyées à l’appareil client où elles sont extraites dans le dossier de documents.
* Le composant UIWebView démarre/s’actualise.

Si une connexion n’a pas pu être établie précédemment, les données téléchargées s’affichent.

### Ressources supplémentaires {#additional-resources}

Pour en savoir plus sur les rôles et les responsabilités d’un administrateur et d’un auteur, consultez les ressources ci-dessous :

* [Création de contenu AEM pour AEM Mobile On-demand Services](/help/mobile/mobile-apps-ondemand.md)
* [Administration de contenu pour utiliser AEM Mobile On-demand Services](/help/mobile/aem-mobile.md)
