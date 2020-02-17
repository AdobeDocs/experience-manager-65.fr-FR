---
title: Création de sites adaptés aux appareils mobiles
seo-title: Création de sites adaptés aux appareils mobiles
description: La création d’un site mobile est similaire à celle d’un site classique en ce sens qu’il faut également créer des modèles et des composants
seo-description: La création d’un site mobile est similaire à celle d’un site classique en ce sens qu’il faut également créer des modèles et des composants
uuid: 6b19042c-03f1-4e33-970e-475f9fb8c5fb
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
discoiquuid: 0aabfb0a-ef9c-4b06-b698-61cad101c3c1
docset: aem65
legacypath: /content/docs/en/aem/6-0/develop/mobile/mobile
translation-type: tm+mt
source-git-commit: b3e1493811176271ead54bae55b1cd0cf759fe71

---


# Création de sites adaptés aux appareils mobiles{#creating-sites-for-mobile-devices}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

La création d’un site mobile est similaire à celle d’un site classique en ce sens qu’il faut également créer des modèles et des composants. Pour plus de détails sur la création de modèles et de composants, reportez-vous aux pages suivantes : [Modèles](/help/sites-developing/templates.md), [Composants](/help/sites-developing/components.md) et [Prise en main du développement de sites AEM](/help/sites-developing/getting-started.md). La principale différence réside dans l’activation des fonctionnalités mobiles intégrées d’AEM au sein du site. Pour ce faire, il convient de créer un modèle qui repose sur le composant de page mobile.

Il est aussi préférable d’utiliser le [responsive design](/help/sites-developing/responsive.md) pour créer un seul site web prenant en charge plusieurs tailles d’écran.

Pour commencer, vous pouvez consulter le **site mobile de démonstration We.Retail** disponible dans AEM.

Pour créer un site adapté aux appareils mobiles, procédez comme suit :

1. Créez le composant de page :

   * Set the `sling:resourceSuperType` property to `wcm/mobile/components/page`
This way the component relies on the mobile page component.

   * Créez le `body.jsp` avec la logique spécifique au projet.

1. Créez le modèle de page :

   * Set the `sling:resourceType` property to the newly created page component.
   * Set the `allowedPaths` property.

1. Créez la page de conception pour le site.
1. Create the site root page below the `/content` node:

   * Set the `cq:allowedTemplates` property.
   * Set the `cq:designPath` property.

1. Dans les propriétés de page de la page racine du site, définissez les groupes d’appareils dans l’onglet **Mobile**.
1. Créez les pages du site en vous servant du nouveau modèle.

Le composant de page mobile ( `/libs/wcm/mobile/components/page`) :

* Ajoute l’onglet **Mobile** à la boîte de dialogue des propriétés de la page.
* Through its `head.jsp`, it retrieves the current mobile device group from the request and if a device group is found, uses the group&#39;s `drawHead()` method to include the device group&#39;s associated emulator init component (only in author mode) and the device group&#39;s rendering CSS.

>[!NOTE]
>
>La page racine du site mobile doit être au niveau 1 de la hiérarchie des nœuds, et il est recommandé de se placer sous le nœud/content.

## Création d’un site mobile avec Multi Site Manager {#creating-a-mobile-site-with-the-multi-site-manager}

Utilisez Multi Site Manager (MSM) pour créer une Live Copy mobile à partir d’un site classique. Celui-ci est automatiquement transformé en site mobile qui possède toutes les fonctionnalités des sites mobiles (par exemple, modification dans un émulateur) et peut être géré en synchronisation avec le site classique. Refer to the section [Creating a Live Copy for different Channels](/help/sites-administering/msm.md) in the Multi Site Manager page.

## API Mobile côté serveur {#server-side-mobile-api}

Les packages Java contenant les classes mobiles sont les suivants :

* [com.day.cq.wcm.mobile.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/api/device/capability/package-summary.html) : définit MobileConstants.
* [com.day.cq.wcm.mobile.api.device](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/api/device/package-summary.html) : définit Device, DeviceGroup et DeviceGroupList.
* [com.day.cq.wcm.mobile.api.device.Capacity](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/api/device/capability/package-summary.html) - définit DeviceCapability.
* [com.day.cq.wcm.mobile.api.wurfl](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/workflow/api/package-summary.html) - définit WurflQueryEngine.
* [com.day.cq.wcm.mobile.core](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/core/package-summary.html) : définit MobileUtil, qui fournit diverses méthodes d’utilitaire tournant autour de WCM Mobile.

### Composants mobiles {#mobile-components}

The **We.Retail Mobile Demo Site** uses the following mobile components which are located below `/libs/foundation/components`:

<table>
 <tbody>
  <tr>
   <td>Nom</td>
   <td>Groupe</td>
   <td>Caractéristiques</td>
  </tr>
  <tr>
   <td>mobilefooter</td>
   <td>hidden</td>
   <td>- pied de page</td>
  </tr>
  <tr>
   <td>Image mobile</td>
   <td>Mobile</td>
   <td>- en fonction du composant<br /> de fondation d’image - rend une image si le périphérique est capable<br /> </td>
  </tr>
  <tr>
   <td>Liste mobile</td>
   <td>Mobile</td>
   <td>- en fonction du composant<br /> de base de liste - listitem_teaser.jsp effectue le rendu d’une image si le périphérique est compatible<br /> </td>
  </tr>
  <tr>
   <td>mobilelogo</td>
   <td>hidden</td>
   <td>- en fonction du composant<br /> de fondation du logo - rend une image si le périphérique est capable<br /> </td>
  </tr>
  <tr>
   <td>Référence mobile</td>
   <td>Mobile</td>
   <td><p>- semblable au composant de base de référence</p> <p>- mappe un composant textimage à un composant mobiletextimage et un composant d’image à un composant mobileimage</p> </td>
  </tr>
  <tr>
   <td>mobiletextimage</td>
   <td>Mobile</td>
   <td>- en fonction du composant<br /> de base textimage - rend une image si le périphérique est capable</td>
  </tr>
  <tr>
   <td>mobiletopnav</td>
   <td>hidden</td>
   <td><p>- en fonction du composant topnav foundation</p> <p>- effectue uniquement le rendu du texte</p> </td>
  </tr>
 </tbody>
</table>

#### Création d’un composant mobile {#creating-a-mobile-component}

Le framework AEM Mobile permet de développer des composants sensibles au type d’appareil émettant la requête. Les exemples de code suivants montrent comment utiliser l’API AEM Mobile dans un composant jsp et en particulier comment : 

* Récupérez le périphérique à partir de la requête :
   `Device device = slingRequest.adaptTo(Device.class);`

* Obtenez le groupe de périphériques :
   `DeviceGroup deviceGroup = device.getDeviceGroup();`

* Obtenez les fonctionnalités du groupe de périphériques :
   `Collection<DeviceCapability> capabilities = deviceGroup.getCapabilities();`

* Récupérez les attributs de l&#39;appareil (clé/valeurs de capacité brute de la base de données WURFL) :
   `Map<String,String> deviceAttributes = device.getAttributes();`

* Obtenez l&#39;agent utilisateur du périphérique :
   `String userAgent = device.getUserAgent();`

* Récupérez la liste des groupes de périphériques (groupes de périphériques affectés au site par l’auteur) à partir de la page active :
   `DeviceGroupList deviceGroupList = currentPage.adaptTo(DeviceGroupList.class);`

* Vérifier si le groupe de périphériques prend en charge les images
   `if (deviceGroup.hasCapability(DeviceCapability.CAPABILITY_IMAGES)) {`
...
OU
   `if MobileUtil.hasCapability(request, DeviceCapability.CAPABILITY_IMAGES) {`
...

>[!NOTE]
>
>In a jsp, `slingRequest` is available through the `<sling:defineObjects>` tag and `currentPage` through the `<cq:defineObjects>` tag.

### Émulateurs {#emulators}

La création basée sur un émulateur permet aux auteurs de créer des pages de contenu destinées aux clients mobiles. La création de contenu mobile suit le même principe que l’édition WYSIWYG locale. Pour que les auteurs puissent faire l’expérience du rendu de la page sur un appareil mobile, une page de contenu mobile est modifiée à l’aide d’un émulateur d’appareil.

Les émulateurs d’appareils mobiles sont basés sur un framework d’émulation générique. Pour plus de détails, reportez-vous à la page [Émulateurs](/help/sites-developing/emulators.md).

L’émulateur affiche l’appareil mobile sur la page pendant que les modifications normales (parsys, composants) sont apportées sur l’écran de l’appareil. Le type d’émulateur dépend des groupes d’appareils configurés pour le site. Plusieurs émulateurs peuvent être affectés à un seul groupe d’appareils. Tous les émulateurs sont alors disponibles sur la page de contenu. Par défaut, le premier émulateur affecté au premier groupe d’appareils attribué au site est affiché. Les émulateurs peuvent être activés au moyen du carrousel d’émulateurs en haut de la page ou avec le bouton de modification du sidekick.

**Création d’un émulateur**

Pour créer un émulateur, reportez-vous à la section [Création d’un émulateur mobile personnalisé](/help/sites-developing/emulators.md) de la page Émulateurs.

**Principales caractéristiques des émulateurs mobiles**

* A device group is composed of one of more emulators: the device group configuration page, e.g. /etc/mobile/groups/touch, contains the `emulators` property below the `jcr:content` node.
Remarque : bien que le même émulateur puisse être affecté à plusieurs groupes d’appareils, ce n’est pas très logique.

* Via the device group&#39;s configuration dialog, the `emulators` property is set with the path of the desired emulator(s). Par exemple: `/libs/wcm/mobile/components/emulators/iPhone4`.

* Les composants de l’émulateur (ex. `/libs/wcm/mobile/components/emulators/iPhone4`) étendez le composant d’émulateur mobile de base ( `/libs/wcm/mobile/components/emulators/base`).

* Chaque composant qui étend l’émulateur mobile de base peut être sélectionné lors de la configuration d’un groupe d’appareils. Les émulateurs personnalisés sont ainsi facilement créés ou étendus.
* Au moment de la requête en mode de modification, l’implémentation de l’émulateur est utilisée pour le rendu de la page.
* Lorsque le modèle de la page repose sur le composant de page mobile, les fonctionnalités de l’émulateur sont automatiquement intégrées dans la page (via le `head.jsp` du composant de page mobile).

### Groupes d’appareils {#device-groups}

Les groupes d’appareils mobiles fournissent une segmentation des appareils mobiles selon les caractéristiques fonctionnelles de chaque appareil. Un groupe d’appareils fournit les informations nécessaires à la création par émulateur sur l’instance de création et au rendu correct sur l’instance de publication : une fois que les auteurs ont ajouté du contenu à la page mobile et l’ont publié, la page peut être demandée sur l’instance de publication. Sur cette instance, au lieu de la vue en mode de modification de l’émulateur, la page de contenu est rendue selon l’un des groupes d’appareils configurés. La sélection du groupe d’appareils se fait en fonction de la [détection des appareils mobiles](#devicedetection). Le groupe d’appareils correspondant fournit alors les informations de style nécessaires.

Device groups are defined as content pages below `/etc/mobile/devices` and use the **Mobile Device Group** template. Celui-ci sert de modèle de configuration pour les définitions de groupe d’appareils sous la forme de pages de contenu. Ses caractéristiques principales sont les suivantes :

* Emplacement: `/libs/wcm/mobile/templates/devicegroup`
* Chemin autorisé : `/etc/mobile/groups/*`
* Composant de page: `wcm/mobile/components/devicegroup`

#### Affectation de groupes d’appareils à votre site {#assigning-device-groups-to-your-site}

Lorsque vous créez un site mobile, vous devez affecter des groupes d’appareils au site. AEM propose trois groupes d’appareils en fonction des capacités de rendu HTML et JavaScript de l’appareil :

* **Téléphones portables** pour les appareils comme le Sony Ericsson W800 avec prise en charge de HTML basique, mais pas des images ni de JavaScript.
* **Smartphones** , pour des appareils comme Blackberry avec prise en charge du code HTML et des images de base, mais pas de JavaScript.

* **Appareils tactiles** pour les tablettes comme l’iPad avec prise en charge complète de HTML, des images, de JavaScript et de la rotation des appareils.

As emulators can be associated with a device group (see the section [Creating a Device Group](#creating-a-device-group)), assigning a device group to a site enables authors to select between the emulators that are associated with the device group to edit the page.

Pour affecter un groupe d’appareils à votre site :

1. Dans votre navigateur, accédez à la console **Site Admin**.
1. Ouvrez la page racine du site pour appareils mobiles sous **Sites web**.
1. Ouvrez les propriétés de la page.
1. Sélectionnez l’onglet **Mobile** :

   * Définissez les groupes d’appareils.
   * Cliquez sur **OK**.

>[!NOTE]
>
>Lorsque les groupes d’appareils sont définis pour un site, ils sont hérités par toutes les pages du site.

#### Filtres de groupe d’appareils {#device-group-filters}

Les filtres de groupe d’appareils définissent des critères fonctionnels pour déterminer si un appareil appartient ou non à un groupe. Lorsque vous créez un groupe d’appareils, vous pouvez sélectionner les filtres à utiliser pour évaluer les appareils.

Au moment de l’exécution, quand AEM reçoit une requête HTTP d’un appareil, chaque filtre associé à un groupe compare les caractéristiques de l’appareil avec des critères spécifiques. L’appareil est considéré comme appartenant au groupe lorsqu’il possède toutes les caractéristiques que le filtre impose. Les caractéristiques sont extraites de la base de données WURFL™.

Les groupes d’appareils peuvent utiliser aucun ou plusieurs filtres pour la détection des caractéristiques. De plus, un filtre peut être utilisé avec plusieurs groupes d’appareils. AEM propose un filtre par défaut qui détermine si l’appareil possède les caractéristiques sélectionnées pour un groupe :

* CSS
* Images JPG et PNG
* JavaScript
* Rotation de l’appareil

Si le groupe d’appareils n’utilise pas de filtre, les caractéristiques sélectionnées configurées pour le groupe sont les seules que l’appareil doit posséder.

Pour plus d’informations, voir [Création de filtres de groupes d’appareils](/help/sites-developing/groupfilters.md).

#### Création d’un groupe d’appareils {#creating-a-device-group}

Créez un groupe d’appareils lorsque les groupes qu’AEM installe ne répondent pas à vos besoins.

1. Dans votre navigateur, accédez à la console **Outils**.
1. Create a new page below **Tools** > **Mobile** > **Device Groups**. Dans la boîte de dialogue **Créer une page** : 

   * As **Title** enter `Special Phones`.

   * As **Name** enter `special`.

   * Sélectionnez un **Modèle de groupe de périphériques mobiles**.
   * Cliquez sur **Créer**.

1. In CRXDE, add a **static.css** file containing the styles for the device group below the `/etc/mobile/groups/special` node.

1. Open the **Special Phones** page.
1. Pour configurer le groupe d’appareils, cliquez sur le bouton **Modifier** à côté de **Paramètres**.
Dans l’onglet **Général** :

   * **Titre**: nom du groupe de périphériques mobiles.
   * **Description** : description du groupe.
   * **User-Agent** : chaîne user-agent avec laquelle les appareils sont mappés. Paramètre facultatif qui peut être une expression régulière. Exemple: `BlackBerryZ10`
   * **Fonctions** : définit si le groupe peut gérer les images, CSS, JavaScript ou la rotation des appareils.
   * **Largeur d’écran minimale** et **Hauteur**
   * **Désactiver l’émulateur** : pour activer/désactiver l’émulateur lors de la modification du contenu.
   Dans l’onglet **Émulateurs** :

   * **Émulateurs** : sélectionnez les émulateurs affectés à ce groupe d’appareils.
   Dans l’onglet **Filtres** :

   * Pour ajouter un filtre, cliquez sur Ajouter un élément et sélectionnez un filtre dans la liste déroulante.
   * Les filtres sont évalués dans l’ordre dans lequel ils apparaissent. Lorsqu’un appareil ne répond pas aux critères d’un filtre, les filtres suivants de la liste ne sont pas évalués.



1. Cliquez sur OK.

La boîte de dialogue de configuration du groupe d’appareils mobiles se présente comme suit :

![screen_shot_2012-02-01at22043pm](assets/screen_shot_2012-02-01at22043pm.png)

#### CSS personnalisé par groupe d’appareils {#custom-css-per-device-group}

Comme décrit précédemment, il est possible d’associer un CSS personnalisé à une page de groupe d’appareils, tout comme avec le CSS d’une page de conception. Ce CSS est utilisé pour influencer le rendu spécifique au groupe d’appareils du contenu de la page sur les instances de création et de publication. Ce CSS est alors automatiquement ajouté :

* dans la page sur l’instance de création pour chaque émulateur utilisé par ce groupe d’appareils ;
* dans la page sur l’instance de publication, si la chaîne User-Agent de la requête correspond à un appareil mobile appartenant à ce groupe d’appareils particulier.

## Détection d’appareils côté serveur {#server-side-device-detection}

Utilisez des filtres et une bibliothèque de caractéristiques d’appareil pour déterminer les fonctions de l’appareil qui effectue la requête HTTP.

### Développez les filtres de groupe d’appareils {#develop-device-group-filters}

Créez un filtre de groupe d’appareils pour définir un ensemble d’exigences en termes de caractéristiques d’appareil. Créez autant de filtres que nécessaire pour cibler les groupes de caractéristiques d’appareils nécessaires.

Concevez vos filtres de sorte à pouvoir utiliser des combinaisons pour définir des groupes de caractéristiques. Généralement, certaines caractéristiques sont communes à différents groupes d’appareils. Par conséquent, vous pouvez utiliser certains filtres avec plusieurs définitions de groupe d’appareils.

Après avoir créé un filtre, vous pouvez l’utiliser dans la configuration du groupe.

Pour plus d’informations, accédez à [Création de filtres de groupe d’appareils](/help/sites-developing/groupfilters.md).

### Utilisation de la base de données WURFL™ {#using-the-wurfl-database}

AEM uses a truncated version of the [WURFL](https://wurfl.sourceforge.net/)™ database to query device capabilities, such as screen resolution or javascript support, based on the device&#39;s User-Agent.

Le code XML de la base de données WURFL™ est représenté sous la forme de noeuds `/var/mobile/devicespecs` en analysant le `wurfl.xml`fichier à `/libs/wcm/mobile/devicespecs/wurfl.xml.` L’extension aux noeuds se produit lors du premier démarrage du `cq-mobile-core` lot.

Les caractéristiques des appareils sont stockées en tant que propriétés de nœud. Les nœuds représentent les modèles d’appareil. Vous pouvez utiliser des requêtes pour récupérer les caractéristiques d’un appareil ou son user-agent.

Puisque la base de données WURFL™ évolue, il faudra peut-être la personnaliser ou la remplacer. Pour mettre à jour la base de données des appareils mobiles, plusieurs options existent :

* Remplacer le fichier par la dernière version, à condition de posséder une licence qui autorise cette utilisation. Voir Installation d’une autre base de données WURFL.
* Utiliser la version disponible dans AEM et configurer une expression régulière qui correspond à vos chaînes User-Agent et pointe vers un appareil WURFL™ existant. See [Adding a regexp-based User-Agent Matching](#adding-a-regexp-based-user-agent-matching).

#### Test du mappage d’un User-Agent avec les fonctionnalités WURFL™{#testing-the-mapping-of-a-user-agent-to-wurfl-capabilities}

Lorsqu’un appareil accède à votre site pour appareils mobiles, AEM le détecte, le mappe à un groupe d’appareils d’après ses fonctions et diffuse un rendu de la page qui est adapté au groupe d’appareils. Le groupe d’appareils correspondant fournit les informations de style nécessaires. Les mappages peuvent être testés sur la page de test Mobile User-Agent :

`https://localhost:4502/etc/mobile/useragent-test.html`

#### Installation d’une autre base de données WURFL™{#installing-a-different-wurfl-database}

La base de données WURFL™ tronquée installée avec AEM est une version antérieure au 30 août 2011. Si votre version de WURFL a été publiée après le 30 août 2011, assurez-vous que l’utilisation que vous en faites est conforme à votre licence.

Pour installer une base de données WURFL™ : 

1. In CRXDE Lite, create the following folder: `/apps/wcm/mobile/devicespecs`
1. Copiez le fichier WURFL™ dans le dossier.
1. Rename the file as `wurfl.xml`.

AEM automatically parses the `wurfl.xml` file and updates the nodes below `/var/mobile/devicespecs`.

>[!NOTE]
>
>Lorsque la base de données WURFL™ complète est activée, l’analyse et l’activation peuvent prendre quelques minutes. Vous pouvez consulter les journaux pour obtenir des informations sur la progression.

#### Ajout d’un mappage User-Agent basé sur une expression régulière {#adding-a-regexp-based-user-agent-matching}

Ajoutez un agent utilisateur en tant qu’expression régulière sous /apps/wcm/mobile/devicespecs/wurfl/regexp pour pointer vers un type de périphérique WURFL™ existant.

1. Dans **CRXDE Lite**, créez un nœud sous /apps/wcm/mobile/devicespecs/regexp, par exemple. apple_ipad_ver1.
1. Ajoutez les propriétés suivantes au nœud  :

   * **regexp**: expression régulière définissant les agents utilisateur, par exemple :.*Mozilla.*iPad.*AppleWebKit.*Safari.*
   * **deviceId**: l’ID de périphérique tel que défini dans le fichier wurfl.xml, par exemple : apple_ipad_ver1

La configuration ci-dessus entraîne le mappage des périphériques pour lesquels User-Agent correspond à l’expression régulière fournie avec l’ID de périphérique apple_ipad_ver1 WURFL™, le cas échéant.

## Détection d’appareils côté client {#client-side-device-detection}

Cette section explique comment utiliser la détection côté client d’AEM afin d’optimiser le rendu des pages ou de proposer au client des versions de site web secondaires.

AEM supports device client-side detection based on `BrowserMap`. `BrowserMap` est envoyée dans AEM en tant que bibliothèque cliente sous `/etc/clientlibs/browsermap`.

`BrowserMap` offre trois alternatives pour fournir un site web secondaire à un client. Elles sont appliquées dans l’ordre suivant :

1. [Des liens secondaires](#providing-alternate-links)
1. [Une URL spécifique au groupe d’appareils](#definingdevicegroupspecificurl)
1. [Une URL basée sur un sélecteur](#defining-selector-based-urls)

>[!NOTE]
>
>Pour plus d’informations sur l’intégration de la bibliothèque cliente, consultez la section [Utilisation de bibliothèques HTML côté client](/help/sites-developing/clientlibs.md).

### Liens secondaires {#providing-alternate-links}

The `PageVariantsProvider` OSGi service is capable of generating alternate links for sites belonging to the same family. Pour configurer les sites concernés par le service, un nœud `cq:siteVariant` doit être ajouté au nœud `jcr:content` à la racine du site.

The `cq:siteVariant` node needs to have the following properties:

* `cq:childNodesMapTo` - détermine l&#39;attribut de l&#39;élément de lien auquel les noeuds enfants seront mappés ; il est recommandé d’organiser le contenu de votre site Web de manière à ce que les enfants du noeud racine représentent la racine d’une variante de langue de votre site Web global (ex. `/content/mysite/en`, `/content/mysite/de`), auquel cas la valeur de la `cq:childNodesMapTo` variable doit être `hreflang`;
* `cq:variantDomain` - indique le domaine `Externalizer` qui sera utilisé pour générer les URL absolues de variantes de page. Si cette valeur n’est pas définie, les variantes de page sont générées avec des liens relatifs.
* `cq:variantFamily` - indique à quelle famille de sites appartient ce site. Plusieurs rendus spécifiques à chaque appareil d’un même site web doivent appartenir à la même famille.
* `media` - stocke les valeurs de l’attribut media de l’élément link. Il est recommandé d’utiliser le nom du `BrowserMap` enregistré avec `DeviceGroups`, de sorte que la bibliothèque `BrowserMap` puisse automatiquement rediriger les clients vers la bonne variante du site web.

#### PageVariantsProvider et Externalizer {#pagevariantsprovider-and-externalizer}

Lorsque la valeur de la propriété `cq:variantDomain` d’un nœud `cq:siteVariant` n’est pas vide, le service `PageVariantsProvider` génère des liens absolus en utilisant cette valeur en tant que domaine configuré pour le service `Externalizer`. Assurez-vous de configurer le service `Externalizer` de manière à tenir compte de votre configuration.

>[!NOTE]
>
>Lorsque vous utilisez AEM, plusieurs méthodes permettent de gérer les paramètres de configuration pour ces services. Voir [Configuration d’OSGi](/help/sites-deploying/configuring-osgi.md) pour avoir plus de détails et connaître les pratiques recommandées.

### Définition d’une URL spécifique à un groupe d’appareils {#defining-a-device-group-specific-url}

Si vous ne souhaitez pas utiliser des liens secondaires, vous pouvez configurer une URL globale pour chaque `DeviceGroup`. Nous vous recommandons de créer votre propre bibliothèque cliente qui intègre la bibliothèque cliente `browsermap.standard`, mais redéfinit les groupes d’appareils.

 est conçu de telle sorte que les définitions de groupes d’appareils peuvent être remplacées en créant et en ajoutant un nouveau groupe d’appareils du même nom à l’objet `BrowserMap`BrowserMap de votre bibliothèque cliente personnalisée.

>[!NOTE]
>
>Pour plus de détails, veuillez lire la section [BrowserMap personnalisé](#creatingacustomisedbrowsermap).

### Définition d’URL basées sur un sélecteur {#defining-selector-based-urls}

Si aucun des mécanismes précédents n’a été utilisé pour indiquer un site secondaire de redirection à `BrowserMap`, les sélecteurs qui utilisent les noms des `DeviceGroups` sont ajoutés aux `URL`, auquel cas vous devez fournir vos propres servlets. Ils géreront les requêtes.

For example a device browsing `www.example.com/index.html` identified as `smartphone` by BrowserMap is forwarded to `www.example.com/index.smartphone.html.`

### Utilisation de BrowserMap dans les pages {#using-browsermap-on-your-pages}

In order to use the standard BrowserMap client library in a page, you have to include the `/libs/wcm/core/browsermap/browsermap.jsp` file using a `cq:include`tag in your page&#39;s `head` section.

```xml
<cq:include script="/libs/wcm/core/browsermap/browsermap.jsp" />
```

Besides adding the `BrowserMap` client library in your `JSP` files, you also have to add a `cq:deviceIdentificationMode` String property set to `client-side` to the `jcr:content` node below the root of your web site.

### Contournement du comportement par défaut de BrowserMap {#overriding-browsermap-s-default-behaviour}

Si vous souhaitez personnaliser `BrowserMap` en remplaçant les `DeviceGroups` ou en ajoutant d’autres sondes, vous devez créer votre propre bibliothèque côté client à laquelle vous incorporez la bibliothèque côté client `browsermap.standard`.

Furthermore, you have to manually call the `BrowserMap.forwardRequest()` method in your `JavaScript` code.

>[!NOTE]
>
>Pour plus d’informations sur l’intégration de la bibliothèque cliente, consultez la section [Utilisation de bibliothèques HTML côté client](/help/sites-developing/clientlibs.md).

Une fois la bibliothèque cliente `BrowserMap` personnalisée créée, nous proposons l’approche suivante :

1. Créez un fichier `browsermap.jsp` dans votre application.

   ```xml
   <%@include file="/libs/foundation/global.jsp" %>
   <%@ taglib prefix="c" uri="https://java.sun.com/jsp/jstl/core" %>
   <%@ page import="
       com.day.cq.wcm.api.variants.PageVariant,
       com.day.cq.wcm.api.variants.PageVariantsProvider,
       com.day.cq.wcm.api.devicedetection.DeviceIdentificationMode,
       com.day.cq.wcm.api.WCMMode"
   %>
   <%
       final PageVariantsProvider p = sling.getService(PageVariantsProvider.class);
       if(p == null) {
           throw new IllegalStateException("Missing PageVariantsProvider service");
       }
       for(PageVariant v : p.getVariants(currentPage, slingRequest)) {
           final String curVar = v.getAttributes().get("data-current-variant");
           String media = v.getAttributes().get("media");
           if (media != null) {
               media = media.replaceAll(" ", "");
           }
   %>
       <link
           rel="alternate"
           data-cq-role="site.variant"
           title="<%= xssAPI.encodeForHTMLAttr(v.getTitle()) %>"
           hreflang="<%= xssAPI.encodeForHTMLAttr(v.getAttributes().get("hreflang")) %>"
           media="<%= xssAPI.encodeForHTMLAttr(media) %>"
           href="<%= xssAPI.getValidHref(v.getURL()) %>"
           <% if(curVar != null) { %> data-current-variant="<%= curVar %>"<% } %>
       />
   <%
       }
       Boolean browserMapEnabled = true;
       final DeviceIdentificationMode dim = sling.getService(DeviceIdentificationMode.class);
       String[] selectors  = slingRequest.getRequestPathInfo().getSelectors();
       boolean isPortletRequest = false;
       for (int i = 0; i < selectors.length; i++) {
           if ("portlet".equals(selectors[i])) {
               isPortletRequest = true;
               break;
           }
       }
       if (isPortletRequest) {
           log.debug("Request was made by a portlet container - BrowserMap will not be embedded");
       } else {
           final WCMMode wcmMode = WCMMode.fromRequest(slingRequest);
           boolean shouldIncludeClientLib = false;
           if (WCMMode.EDIT != wcmMode && WCMMode.PREVIEW != wcmMode && WCMMode.DESIGN != wcmMode) {
               if (dim != null) {
                   final String mode = dim.getDeviceIdentificationModeForPage(currentPage);
                   shouldIncludeClientLib = DeviceIdentificationMode.CLIENT_SIDE.equals(mode);
                   if (shouldIncludeClientLib) {
                       browserMapEnabled = (Boolean) request.getAttribute("browsermap.enabled");
                       if (browserMapEnabled == null) {
                           browserMapEnabled = true;
                       }
                   }
               }
           }
   %>
           <c:if test="<%= !browserMapEnabled %>">
               <meta name="browsermap.enabled" content="false">
           </c:if>
           <c:if test="<%= shouldIncludeClientLib %>">
               <meta name="viewport" content="width=device-width, initial-scale=1.0">
               <cq:includeClientLib categories="browsermap.custom"/>
           </c:if>
   <%
       }
   %>
   ```

1. Ajoutez le fichier `broswermap.jsp` à la section head.

   ```xml
   <cq:include script="browsermap.jsp" />
   ```

### Exclusion de BrowserMap de certaines pages {#excluding-browsermap-from-certain-pages}

Si vous souhaitez exclure la bibliothèque BrowserMap de certaines pages pour lesquelles vous n’avez pas besoin de détection de client, vous pouvez ajouter un attribut de requête :

```xml
<%
request.setAttribute("browsermap.enabled", false);
%>
```

This will make the `/libs/wcm/core/browsermap/browsermap.jsp` script to add a meta tag to the page that will make `BrowserMap` to not perform any detection:

```xml
<meta name="browsermap.enabled" content="false">
```

### Test d’une version spécifique d’un site web {#testing-a-specific-version-of-a-web-site}

En principe, le script BrowserMap redirige toujours les internautes vers la version la mieux adaptée du site web, généralement vers la version bureau ou mobile, selon le cas.

Vous pouvez forcer un type d’appareil, peu importe sa requête, afin de tester une version particulière d’un site web en ajoutant le paramètre `device` à l’URL. L’URL ci-dessous diffuse la version mobile du site web Geometrixx Outdoors.

`https://localhost:4502/content/geometrixx-outdoors/en.html?wcmmode=disabled&device=smartphone`

>[!NOTE]
>
>The `wcmmode` paratemer is set to `disabled` in order to simulate the behavior of a publish instance.

La valeur remplacée est stockée dans un cookie afin que la navigation sur votre site web soit possible sans ajouter le paramètre `device`device à chaque `URL`.

Par conséquent, vous devez appeler la même `URL` avec la valeur `device` définie sur `browser` pour revenir à la version bureau du site web.

>[!NOTE]
>
>BrowserMap stocke la valeur device remplacée dans un cookie appelé `BMAP_device`. La suppression de ce cookie garantit que CQ diffuse la version appropriée du site web en fonction de l’appareil (par exemple, la version bureau ou mobile).

## Traitement de requêtes mobiles {#mobile-request-processing}

AEM traite les requêtes émises par des appareils mobiles appartenant au groupe d’appareils tactiles comme suit : 

1. An iPad sends a request to the AEM publish instance, e.g. `https://localhost:4503/content/geometrixx_mobile/en/products.html`
1. AEM determines whether the site of the requested page is a mobile site (by checking whether the first level page `/content/geometrixx_mobile` extends the mobile page component). Si oui :
1. AEM recherche les fonctionnalités du périphérique en fonction de l’agent utilisateur dans l’en-tête de requête.
1. AEM maps the device capabilities to the device group and sets `touch` as the device group selector.
1. AEM redirige la requête vers `https://localhost:4503/content/geometrixx_mobile/en/products.touch.html.`
1. AEM envoie la réponse à l’iPad :

   * La page `products.touch.html` est diffusée de manière habituelle et peut être mise en cache.
   * Les composants de rendu utilisent des sélecteurs pour adapter la présentation.
   * AEM ajoute automatiquement le sélecteur de mobile à tous les liens internes de la page.

### Statistiques {#statistics}

Vous pouvez obtenir des statistiques sur le nombre de demandes envoyées au serveur AEM par des périphériques mobiles. Le nombre de requêtes peut être décomposé :

* par groupe d’appareils et par appareil
* par année, mois et jour

Pour voir les statistiques :

1. Accédez à la console **Outils**.
1. Ouvrez la page **Statistiques d’appareils** sous **Outils** > **Mobile**.
1. Cliquez sur le lien pour afficher les statistiques d’une année, d’un mois ou d’un jour en particulier.

La page **Statistiques** se présente comme suit :

![screen_shot_2012-02-01at24353pm](assets/screen_shot_2012-02-01at24353pm.png)

>[!NOTE]
>
>The **Statistics** page is created the first time a mobile device accesses AEM and is detected. Avant cela, elle n’est pas disponible.

Si vous devez générer une entrée dans les statistiques, vous pouvez procéder comme suit :

1. Utilisez un périphérique mobile ou un émulateur (par exemple, https://chrispederick.com/work/user-agent-switcher/ sur Firefox).
1. Demandez une page mobile sur l’instance d’auteur en désactivant le mode de création, par exemple :
   `https://localhost:4502/content/geometrixx_mobile/en/products.html?wcmmode=disabled`

La page **Statistiques** est désormais disponible.

### Prise en charge de la mise en cache de page pour les liens « envoyer un lien à un ami »{#supporting-page-caching-for-send-link-to-a-friend-links}

Mobile pages are generally cachable on Dispatcher, because pages that are rendered for a device group are distinguished in the page URL by the device group selector, for example `/content/mobilepage.touch.html`. Une requête vers une page mobile sans sélecteur n’est jamais mise en cache puisque, dans ce cas, la détection d’appareil fonctionne et redirige au final la page vers le groupe d’appareils correspondant (ou « nomatch » plus précisément). Une page mobile diffusée avec un sélecteur de groupe d’appareils est traitée par réécriture des liens. Tous les liens de la page sont réécrits de manière à contenir le sélecteur de groupe, empêchant ainsi la détection pour chaque clic sur une page déjà traitée.

Par conséquent, le cas de figure suivant est possible.

L’utilisateur Alice est redirigé vers `coolpage.feature.html` et envoie cette URL à un ami Robert qui y accède avec un autre client appartenant au groupe d’appareils `touch`.

Si `coolpage.feature.html` est diffusée à partir d’un cache frontal, AEM ne peut pas analyser la requête pour détecter que le sélecteur mobile ne correspond pas au nouveau User-Agent, et Robert accède à un rendu inadéquat de la page.

Pour résoudre ce problème, vous pouvez inclure une interface de sélection simple sur les pages où les utilisateurs finaux peuvent remplacer le groupe d’appareils sélectionné par AEM. Dans l’exemple ci-dessus, un lien (ou une icône) sur la page permet à l’utilisateur final d’accéder à `coolpage.touch.html` s’il pense que cette version de la page est mieux adaptée à son appareil.
