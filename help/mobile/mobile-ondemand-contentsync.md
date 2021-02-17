---
title: Mobile avec Content Sync
seo-title: Mobile avec Content Sync
description: Suivez cette page pour en savoir plus sur la synchronisation de contenu. Les pages créées dans AEM peuvent être utilisées comme contenu d’application, même lorsque l’appareil est hors ligne. De plus, comme les pages AEM sont basées sur des normes Web, elles fonctionnent sur plusieurs plates-formes et vous permettent de les incorporer dans n’importe quel wrapper natif. Cette stratégie réduit les efforts de développement et vous permet de mettre facilement à jour le contenu de l’application.
seo-description: Suivez cette page pour en savoir plus sur la synchronisation de contenu. Les pages créées dans AEM peuvent être utilisées comme contenu d’application, même lorsque l’appareil est hors ligne. De plus, comme les pages AEM sont basées sur des normes Web, elles fonctionnent sur plusieurs plates-formes et vous permettent de les incorporer dans n’importe quel wrapper natif. Cette stratégie réduit les efforts de développement et vous permet de mettre facilement à jour le contenu de l’application.
uuid: 11f74cc5-99a5-4186-9b60-b19351305432
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: 8fb70ca4-86fc-477d-9773-35b84d5e85a8
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '3057'
ht-degree: 2%

---


# Mobile avec Content Sync{#mobile-with-content-sync}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

Utilisez la synchronisation de contenu pour regrouper le contenu afin de l’utiliser dans des applications mobiles natives. Les pages créées dans AEM peuvent être utilisées comme contenu d’application, même lorsque l’appareil est hors ligne. De plus, comme les pages AEM sont basées sur des normes Web, elles fonctionnent sur plusieurs plates-formes et vous permettent de les incorporer dans n’importe quel wrapper natif. Cette stratégie réduit les efforts de développement et vous permet de mettre facilement à jour le contenu de l’application.

La structure Content Sync crée un fichier d’archive contenant le contenu Web. Le contenu peut provenir de pages simples, d’images et de fichiers PDF, ou d’Applications web entières. L’API de synchronisation de contenu permet d’accéder au fichier d’archive à partir d’applications mobiles ou de créer des processus afin que le contenu puisse être récupéré et inclus dans l’application.

La séquence d’étapes suivante illustre un cas d’utilisation typique de la synchronisation de contenu :

1. Le développeur AEM crée une configuration Content Sync qui spécifie le contenu à inclure.
1. La structure Content Sync collecte et met en cache le contenu.
1. Sur un périphérique mobile, l’application mobile est démarrée et demande du contenu au serveur, qui est diffusé dans un fichier ZIP.
1. Le client décompresse le contenu ZIP vers le système de fichiers local. La structure de dossiers dans le fichier ZIP simule les chemins d’accès qu’un client (navigateur, par exemple) demande normalement au serveur.
1. Le client ouvre le contenu dans un navigateur incorporé ou l’utilise d’une autre manière.
1. Par la suite, le client demande du contenu mis à jour à partir du serveur. La structure Content Sync fournit des mises à jour incrémentielles afin de réduire la taille et le temps de téléchargement, ce qui peut s’avérer important pour les périphériques mobiles en raison d’une bande passante ou de volumes de données limités.

## Développement des gestionnaires de synchronisation de contenu {#developing-the-content-sync-handlers}

Voici quelques-unes des directives pour le développement de gestionnaires de synchronisation de contenu :

* Les gestionnaires doivent implémenter *com.day.cq.contentsync.handler.ContentUpdateHandler* (directement ou en étendant une classe qui le fait).
* Les gestionnaires peuvent étendre *com.adobe.cq.mobile.platform.impl.contentsync.handler.AbstractSlingResourceUpdateHandler*
* Le gestionnaire ne doit signaler la valeur true que s’il met à jour le cache ContentSync. Le rapports erroné true aura AEM créer une mise à jour lorsqu&#39;une mise à jour n&#39;a pas eu lieu.
* Le gestionnaire ne doit mettre à jour le cache que si le contenu a réellement changé. N’écrivez pas dans le cache si un blanc n’est pas nécessaire. Cela entraîne la création d’une mise à jour inutile.

>[!NOTE]
>
>Activez *la journalisation du débogage ContentSync* via les configurations de journalisation OSGI sur le package *com.day.cq.contentsync*. Cela permet de suivre les gestionnaires exécutés et s’ils ont mis à jour le cache et signalé la mise à jour du cache.

## Configuration du contenu de synchronisation de contenu {#configuring-the-content-sync-content}

Créez une configuration Content Sync pour spécifier le contenu du fichier ZIP distribué au client. Vous pouvez créer autant de configurations Content Sync que vous le souhaitez. Chaque configuration a un nom à des fins d’identification.

Pour créer une configuration Content Sync, ajoutez un noeud `cq:ContentSyncConfig` au référentiel, avec la propriété `sling:resourceType` définie sur `contentsync/config`. Le noeud `cq:ContentSyncConfig` peut se trouver n’importe où dans le référentiel, mais il doit être accessible aux utilisateurs de l’instance de publication AEM. Par conséquent, vous devez ajouter le noeud sous `/content`.

Pour spécifier le contenu du fichier ZIP Content Sync, ajoutez des noeuds enfants au noeud cq:ContentSyncConfig. Les propriétés suivantes de chaque noeud enfant identifient un élément de contenu à inclure et comment il est traité lors de son ajout :

* `path`: Emplacement du contenu.
* `type`: Nom du type de configuration à utiliser pour le traitement du contenu. Plusieurs types sont disponibles et sont décrits dans la section *Types de configuration*.

Voir *Exemple de configuration de synchronisation de contenu* pour plus d’informations.

Une fois la configuration de synchronisation de contenu créée, elle s’affiche dans la console de synchronisation de contenu.

>[!NOTE]
>
>La structure Content Sync ne vérifie pas que les dépendances des ressources et des fichiers liés à la conception sont incluses dans les packages Content Sync. Veillez à inclure tous les fichiers requis dans le fichier ZIP.

### Configuration de l’accès aux téléchargements de synchronisation de contenu {#configuring-access-to-content-sync-downloads}

Spécifiez un utilisateur ou un groupe pouvant être téléchargé à partir de la synchronisation de contenu. Vous pouvez configurer l’utilisateur ou le groupe par défaut pouvant être téléchargé à partir de tous les caches de synchronisation de contenu. Vous pouvez également remplacer la valeur par défaut et configurer l’accès pour une configuration de synchronisation de contenu spécifique.

Une fois l’AEM installé, les membres du groupe d’administrateurs peuvent, par défaut, télécharger à partir de Content Sync.

#### Définition de l’accès par défaut pour les téléchargements de synchronisation de contenu {#setting-the-default-access-for-content-sync-downloads}

Le service Day CQ Content Sync Manager contrôle l’accès à Content Sync. Configurez ce service pour spécifier l’utilisateur ou le groupe qui peut télécharger à partir de Content Sync par défaut.

Si vous configurez [le service à l&#39;aide de la console Web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console), entrez le nom de l&#39;utilisateur ou du groupe comme valeur de la propriété Autorisation du cache de secours.

Si vous configurez [dans le référentiel](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository), utilisez les informations suivantes sur le service :

* PID : com.day.cq.contentsync.impl.ContentSyncManagerImpl
* Nom de la propriété : contentsync.fallback.authizable

#### Remplacement de l’accès au téléchargement pour un cache de synchronisation de contenu {#overriding-download-access-for-a-content-sync-cache}

Pour configurer l’accès au téléchargement pour une configuration Content Sync spécifique, ajoutez la propriété suivante au noeud `cq:ContentSyncConfig` :

* Nom : autorisé
* Type : chaîne
* Valeur : Nom de l’utilisateur ou du groupe qui peut télécharger.

Par exemple, votre application permet aux utilisateurs d’installer des mises à jour directement à partir de Content Sync. Pour permettre à tous les utilisateurs de télécharger la mise à jour, définissez la valeur de la propriété autorisée sur `everyone`.

Si le noeud `cq:ContentSyncConfig` ne possède aucune propriété autorisée, l’utilisateur ou le groupe par défaut configuré pour la propriété Autorisable du cache de secours du service Day CQ Content Sync Manager détermine qui peut télécharger.

### Configuration de l’utilisateur pour la mise à jour d’un cache de synchronisation de contenu {#configuring-the-user-for-updating-a-content-sync-cache}

Lorsqu’un utilisateur effectue une mise à jour du cache de synchronisation de contenu, un compte utilisateur spécifique effectue l’action pour le compte de l’utilisateur. Par défaut, l’utilisateur anonyme met à jour tous les caches Content Sync.

Vous pouvez remplacer l’utilisateur par défaut et spécifier un utilisateur ou un groupe qui met à jour un cache Content Sync spécifique.

Pour remplacer l’utilisateur par défaut, spécifiez un utilisateur ou un groupe qui effectue des mises à jour pour une configuration Content Sync spécifique en ajoutant la propriété suivante au noeud cq:ContentSyncConfig :

* Nom : `updateuser`
* Type : `String`
* Valeur : Nom de l’utilisateur ou du groupe qui peut effectuer les mises à jour.

Si le noeud `cq:ContentSyncConfig` ne possède pas de propriété `updateuser`, l’utilisateur `anonymous` par défaut met à jour le cache.

### Types de configuration {#configuration-types}

Le traitement peut aller du rendu JSON simple au rendu complet des pages, y compris leurs ressources référencées. Cette section liste les types de configuration disponibles et leurs paramètres spécifiques :

**** copyCopiez simplement les fichiers et les dossiers.

* **chemin**  - Si le chemin d&#39;accès pointe vers un seul fichier, seul le fichier est copié. S’il pointe vers un dossier (y compris les noeuds de page), tous les fichiers et dossiers ci-dessous seront copiés.

**** contentRender le contenu à l’aide du traitement [ standard des requêtes ](/help/sites-developing/the-basics.md#sling-request-processing)Sling.

* **chemin**  - chemin d&#39;accès à la ressource qui doit être sortie.
* **extension**  - extension qui doit être utilisée dans la demande. Les exemples courants sont *html* et *json*, mais toute autre extension est possible.

* **sélecteur**  : sélecteurs facultatifs séparés par un point. Les exemples courants sont *touch* pour le rendu des versions mobiles d’une page ou *infinity* pour la sortie JSON.

**** clientlibPackage d’une bibliothèque cliente JavaScript ou CSS.

* **chemin**  : chemin d&#39;accès à la racine de la bibliothèque cliente.
* **extension**  - Type de bibliothèque cliente. Il doit être défini sur *js* ou *css* pour le moment.

**ressources**

Collecte des rendus originaux de ressources.

* **chemin**  - Chemin d&#39;accès à un dossier de ressources situé sous /content/dam.

**** imageCollecte d’une image.

* **chemin**  - Chemin d&#39;accès à une ressource d&#39;image.

Le type d’image est utilisé pour inclure le logo We Retail dans le fichier zip.

**** pagesGénérer des pages AEM et collecter des ressources référencées.

* **chemin**  - Chemin d&#39;accès à une page.
* **extension**  - extension qui doit être utilisée dans la demande. Pour les pages, il s’agit presque toujours de *html*, mais d’autres sont encore possibles.

* **sélecteur**  : sélecteurs facultatifs séparés par un point. Les exemples courants sont *touch* pour le rendu des versions mobiles d’une page.

* **deep**  - Propriété booléenne facultative déterminant si les pages enfants doivent également être incluses. La valeur par défaut est *true.*

* **includeImages**  - Propriété booléenne facultative déterminant si les images doivent être incluses. La valeur par défaut est *true*.

   Par défaut, seuls les composants d’image avec un type de ressource de fondation/composants/image sont pris en compte pour l’inclusion. Vous pouvez ajouter d&#39;autres types de ressources en configurant le gestionnaire de mise à jour des pages WCM de **Day CQ** dans la console Web.

**** rewriteLe noeud rewrite définit comment les liens sont réécrits dans la page exportée. Les liens réécrits peuvent pointer vers les fichiers inclus dans le fichier compressé ou vers les ressources sur le serveur.

Le noeud `rewrite` doit être situé sous le noeud `page`.

Le noeud `rewrite` peut avoir une ou plusieurs des propriétés suivantes :

* `clientlibs`: réécrit les chemins clientlibs.

* `images`: réécrit les chemins d’accès aux images.
* `links`: réécrit les chemins des liens.

Chaque propriété peut avoir l’une des valeurs suivantes :

* `REWRITE_RELATIVE`: réécrit le chemin d’accès avec une position relative par rapport au fichier page.html sur le système de fichiers.

* `REWRITE_EXTERNAL`: réécrit le chemin en pointant vers la ressource sur le serveur, à l’aide du service [ Externalizer AEM ](/help/sites-developing/externalizer.md)Externalizer.

Le service AEM appelé **PathRewriterTransformerFactory** vous permet de configurer les attributs html spécifiques qui seront réécrits. Le service peut être configuré dans la console Web et possède une configuration pour chaque propriété du noeud `rewrite` : `clientlibs`, `images` et `links`.

Cette fonctionnalité a été ajoutée à AEM 5.5.

### Exemple de configuration de synchronisation de contenu {#example-content-sync-configuration}

La liste ci-dessous présente un exemple de configuration de Content Sync.

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

**etc.designs.default et etc.designs.** mobileLes deux premières entrées de la configuration doivent être assez évidentes. Comme nous allons inclure un certain nombre de pages mobiles, nous avons besoin des fichiers de conception associés sous /etc/designs. Et comme aucun traitement supplémentaire n&#39;est nécessaire, la copie est suffisante.

**événements.** plistCette entrée est un peu spéciale. Comme indiqué dans l&#39;introduction, l&#39;application devrait fournir une vue cartographique avec les marqueurs des emplacements des événements. Nous allons fournir les renseignements nécessaires sur l&#39;emplacement sous la forme d&#39;un fichier distinct au format PLIST. Pour que cela fonctionne, le composant événement liste utilisé sur la page d’index dispose d’un script appelé plist.jsp. Ce script est exécuté lorsque la ressource du composant est demandée avec l&#39;extension .plist. Comme d’habitude, le chemin d’accès aux composants est indiqué dans la propriété path et le type est défini sur content, car nous voulons exploiter le traitement de la demande [Sling](/help/sites-developing/the-basics.md#sling-request-processing).

**événements.touch.** htmlEnsuite, les pages réelles qui s’afficheront dans l’application sont affichées. La propriété path est définie sur la page racine des événements. Toutes les pages de événement situées en dessous de cette page seront également incluses, car la propriété deep prend par défaut la valeur true. Nous utilisons les pages comme type de configuration, de sorte que toute image ou tout autre fichier qui peut être référencé à partir d&#39;une image ou d&#39;un composant de téléchargement sur une page, soit incluse. En outre, la définition du sélecteur tactile nous donne une version mobile des pages. La configuration du Feature Pack contient plus d&#39;entrées de ce type, mais elles sont laissées pour compte ici pour la simplicité.

**** logoLe type de configuration du logo n&#39;a pas été mentionné jusqu&#39;à présent et il ne s&#39;agit pas des types de connexion. Cependant, la structure Content Sync est extensible dans une certaine mesure et c’est un exemple de cette structure, qui sera traité dans la section suivante.

**** manifestIl est souvent souhaitable que certaines métadonnées soient incluses dans le fichier zip, comme la page de début de votre contenu, par exemple. Cependant, le codage en dur de ces informations vous empêche de facilement les modifier ultérieurement. La structure Content Sync prend en charge cette utilisation en recherchant un noeud manifeste dans la configuration, qui est simplement identifié par son nom et ne nécessite pas de type de configuration. Chaque propriété définie sur ce noeud particulier est ajoutée à un fichier, également appelé manifest et se trouve à la racine du fichier zip.

Dans cet exemple, la page de liste des événements est censée être la page initiale. Ces informations sont fournies dans la propriété **indexPage** et peuvent donc être facilement modifiées à tout moment. Une seconde propriété définit le chemin d’accès du fichier *événements.plist*. Comme nous le verrons plus tard, l’application cliente peut maintenant lire le manifeste et agir en fonction de celui-ci.

Dès que la configuration est configurée, le contenu peut être téléchargé avec un navigateur ou tout autre client HTTP, ou si vous développez pour iOS, vous pouvez utiliser la bibliothèque cliente WppKitSync dédiée. L’emplacement de téléchargement est constitué du chemin d’accès de la configuration et de l’extension *.zip*, par exemple lorsque vous travaillez avec une instance d’AEM locale : *http://localhost:4502/content/weretail_go.zip*

### Console de synchronisation du contenu {#the-content-sync-console}

La console Content Sync liste toutes les configurations Content Sync du référentiel (tous les noeuds de type `cq:ContentSyncConfig`) et pour chaque configuration, vous permet d’effectuer les opérations suivantes :

* Mettez à jour le cache.
* Effacez le cache.
* Téléchargez un fichier zip complet.
* Téléchargez un fichier zip diff entre maintenant et une date et une heure spécifiques.

Il peut être utile pour le développement et le dépannage.

La console est accessible à l&#39;adresse suivante :

`http://localhost:4502/libs/cq/contentsync/content/console.html`

Elle se présente comme suit :

![chlimage_1-50](assets/chlimage_1-50.png)

### Extension de la structure Content Sync {#extending-the-content-sync-framework}

Bien que le nombre d&#39;options de configuration soit déjà assez important, il peut ne pas couvrir toutes les exigences de votre cas d&#39;utilisation spécifique. Cette section décrit les points d’extension de la structure Content Sync et comment créer des types de configuration personnalisés.

Pour chaque type de configuration, il existe un *gestionnaire de mise à jour de contenu*, qui est une fabrique de composants OSGi enregistrée pour ce type spécifique. Ces gestionnaires collectent le contenu, le traitent et l’ajoutent à un cache qui est conservé par la structure Content Sync. Implémentez l’interface ou la classe de base abstraite suivante :

* `com.day.cq.contentsync.handler.ContentUpdateHandler` - Interface que tous les gestionnaires de mise à jour doivent implémenter
* `com.day.cq.contentsync.handler.AbstractSlingResourceUpdateHandler` - Une classe abstraite qui simplifie le rendu des ressources à l&#39;aide de Sling

Enregistrez votre classe en tant que fabrique de composants OSGi et déployez-la dans le conteneur OSGi dans un lot. Pour ce faire, vous pouvez utiliser le [module externe SCR Maven](https://felix.apache.org/site/apache-felix-maven-scr-plugin.html) en utilisant des balises JavaDoc ou des annotations. L’exemple suivant montre la version de JavaDoc :

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

Notez que la définition *usine* contient l’interface commune et le type personnalisé séparé par une barre oblique. Cette stratégie permet à la structure Content Sync de trouver et de créer une instance de votre classe personnalisée, car elle reconnaît le type personnalisé dans une entrée de configuration. La section suivante donne un exemple concret de gestionnaire de mise à jour personnalisé.

>[!CAUTION]
>
>Lors de la création sur la classe de base AbstractSlingResourceUpdateHandler, vous devez ajouter la définition *héritage*. Sinon, le conteneur OSGi ne définira pas les références requises qui sont déclarées dans la classe de base.

### Implémentation d’un gestionnaire de mise à jour personnalisé {#implementing-a-custom-update-handler}

Chaque page Web Web.Retail Mobile contient un logo dans le coin supérieur gauche que nous aimerions inclure dans le fichier zip, bien sûr. Toutefois, pour l&#39;optimisation du cache, AEM ne fait pas référence à l&#39;emplacement réel du fichier image dans le référentiel, ce qui nous empêche d&#39;utiliser simplement le type de configuration **copy**. Nous devons plutôt fournir notre propre type de configuration **logo** qui rend l&#39;image disponible à l&#39;emplacement demandé par AEM. La liste de code suivante indique la mise en oeuvre complète du gestionnaire de mise à jour du logo :

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

La classe `LogoUpdateHandler` implémente la méthode `updateCacheEntry(ConfigEntry, Long, String, Session, Session)` de l&#39;interface `ContentUpdateHandler`, qui prend plusieurs arguments :

* Une instance `ConfigEntry` qui permet d&#39;accéder à l&#39;entrée de configuration, pour laquelle ce gestionnaire est appelé, et à ses propriétés.
* Horodatage `lastUpdated` indiquant la dernière fois que Content Sync a mis à jour son cache. Le contenu qui n’a pas été modifié après cet horodatage ne doit pas être mis à jour par le gestionnaire.
* Argument `configCacheRoot` spécifiant le chemin d&#39;accès racine du cache. Tous les fichiers mis à jour doivent être stockés sous ce chemin pour être ajoutés au fichier zip.
* Session d’administration qui doit être utilisée pour toutes les opérations de référentiel liées au cache.
* Session utilisateur pouvant être utilisée pour mettre à jour le contenu dans le contexte d’un utilisateur donné et, par conséquent, pour fournir un type de contenu personnalisé.

Pour implémenter le gestionnaire personnalisé, vous devez d’abord créer une instance de la classe Image en fonction de la ressource fournie dans l’entrée de configuration. C&#39;est en gros la même procédure que le composant de logo sur nos pages. Il s’assure que le chemin de cible de l’image est identique à celui référencé à partir d’une page.

Ensuite, vérifiez si la ressource a été modifiée depuis la dernière mise à jour. Les implémentations personnalisées doivent éviter les mises à jour inutiles du cache et renvoyer la valeur false si rien ne change. Si la ressource a été modifiée, copiez l’image à l’emplacement de cible attendu par rapport à la racine du cache. Enfin, `true` est renvoyé pour indiquer à la structure que le cache a été mis à jour.

## Utilisation du contenu sur le client {#using-the-content-on-the-client}

Pour utiliser du contenu dans une application mobile fournie par Content Sync, vous devez demander du contenu via une connexion HTTP ou HTTPS. En conséquence, le contenu récupéré (compressé dans un fichier ZIP) peut être extrait et stocké localement sur le périphérique mobile. Notez que le contenu fait non seulement référence aux données mais aussi à la logique, c&#39;est-à-dire aux applications Web complètes ; permettant ainsi à l’utilisateur mobile d’exécuter des applications Web récupérées et des données correspondantes, même sans connectivité réseau.

Content Sync fournit le contenu de manière intelligente : Seules les modifications apportées aux données depuis la dernière synchronisation réussie des données sont distribuées, ce qui réduit le temps nécessaire au transfert des données. Lors de la première exécution d&#39;une application, des modifications de données sont demandées depuis le 1er janvier 1970, tandis que, par la suite, seules les données modifiées depuis la dernière synchronisation réussie sont demandées. AEM utilise un cadre de communication client pour iOS afin de simplifier la communication et le transfert des données, de sorte qu’une quantité minimale de code natif soit nécessaire pour activer une application Web basée sur iOS.

Toutes les données transférées peuvent être extraites dans la même structure de répertoires, aucune étape supplémentaire (par exemple, les contrôles de dépendance) n’est requise lors de l’extraction des données. Dans le cas d’iOS, toutes les données sont stockées dans un sous-dossier du dossier Documents de l’application iOS.

Chemin d’exécution standard d’une application AEM Mobile basée sur iOS :

* Application de débuts utilisateur sur périphérique iOS.
* L’application tente de se connecter à AEM principal et demande des modifications de données depuis la dernière exécution.
* Le serveur récupère les données en question et les zip dans un fichier.
* Les données sont renvoyées au périphérique client où elles sont extraites dans le dossier documents.
* Débuts/actualisations du composant UIWebView.

Si une connexion n&#39;a pas pu être établie, les données précédemment téléchargées s&#39;affichent.

### Ressources supplémentaires {#additional-resources}

Pour en savoir plus sur les rôles et les responsabilités d’un administrateur et d’un auteur, consultez les ressources ci-dessous :

* [Création de contenu AEM pour AEM Mobile On-demand Services](/help/mobile/mobile-apps-ondemand.md)
* [Administration du contenu à utiliser AEM Mobile On-demand Services](/help/mobile/aem-mobile.md)

