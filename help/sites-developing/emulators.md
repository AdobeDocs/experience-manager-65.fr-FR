---
title: Émulateurs
seo-title: Émulateurs
description: AEM permet aux auteurs d’afficher une page dans un émulateur qui simule l’environnement dans lequel un utilisateur final consulte la page.
seo-description: AEM permet aux auteurs d’afficher une page dans un émulateur qui simule l’environnement dans lequel un utilisateur final consulte la page.
uuid: ee1496a5-be68-4318-b5ce-b11c41e4485c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
discoiquuid: c51fca81-5dfc-4838-9672-acb6de62778b
legacypath: /content/docs/en/aem/6-0/develop/mobile/emulators
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 67%

---


# Émulateurs{#emulators}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

Adobe Experience Manager (AEM) permet aux auteurs d’afficher une page dans un émulateur qui simule l’environnement dans lequel un utilisateur final consulte la page, comme un appareil mobile ou un client de messagerie électronique.

La structure de l’émulateur AEM :

* fournit des fonctions de création de contenu dans une interface utilisateur (IU) simulée, par exemple, un appareil mobile ou un client de messagerie électronique (utilisé pour rédiger des bulletins d’information) ;
* adapte le contenu de la page selon l’IU simulée ;
* permet de créer des émulateurs personnalisés.

>[!CAUTION]
>
>Cette fonction est uniquement prise en charge dans l’IU classique.

## Caractéristiques des émulateurs {#emulators-characteristics}

Un émulateur :

* repose sur ExtJS ;
* fonctionne sur le DOM de la page ;
* a une apparence définie via CSS ;
* prend en charge les modules externes (par exemple, le module externe de rotation sur des appareils mobiles) ;
* est uniquement actif sur l’auteur ;
* Son composant de base est `/libs/wcm/emulator/components/base`.

### Transformation du contenu par l’émulateur {#how-the-emulator-transforms-the-content}

L’émulateur fonctionne en encapsulant les contenus du corps HTML dans des balises div d’émulateurs. Par exemple, le code HTML qui suit :

```xml
<body>
<div id="wrapper" class="page mobilecontentpage ">
    <div class="topnav mobiletopnav">
    ...
    </div>
    ...
</div>
</body>
```

est transformé en code HTML suivant après le lancement de l’émulateur :

```xml
<body>
 <div id="cq-emulator-toolbar">
 ...
 </div>
 <div id="cq-emulator-wrapper">
  <div id="cq-emulator-device">
   <div class=" android vertical" id="cq-emulator">
    ...
    <div class=" android vertical" id="cq-emulator-content">
     ...
     <div id="wrapper" class="page mobilecontentpage">
     ...
     </div>
     ...
    </div>
   </div>
  </div>
 </div>
 ...
</body>
```

Deux balises div ont été ajoutées :

* La balise div avec l’ID `cq-emulator` contenant l’ensemble de l’émulateur.

* La balise div avec l’ID `cq-emulator-content` représentant la zone viewport/screen/content du périphérique où réside le contenu de la page.

De nouvelles classes CSS sont également attribuées aux nouvelles balises div d’émulateurs : elles représentent le nom de l’émulateur actuel.

Les modules externes d’un émulateur peuvent développer la liste des classes CSS attribuées, comme dans l’exemple du module externe de rotation qui insère une classe « vertical » ou «horizontal » en fonction de la rotation du périphérique actif.

De cette manière, l’aspect complet de l’émulateur peut être contrôlé à l’aide de classes CSS correspondant aux ID et classes CSS des balises div d’émulateurs.

>[!NOTE]
>
>Il est recommandé que le projet HTML encapsule le contenu du corps dans une seule balise div, comme dans l’exemple ci-dessus. Si le contenu du corps contient plusieurs balises, les résultats peuvent être imprévisibles.

### Émulateurs mobiles  {#mobile-emulators}

Les émulateurs mobiles existants :

* se trouvent sous /libs/wcm/mobile/components/emulators ;
* Sont disponibles via la servlet JSON à l’adresse :

   http://localhost:4502/bin/wcm/mobile/emulators.json

Lorsque le composant de page repose sur le composant de page mobile ( `/libs/wcm/mobile/components/page`), la fonctionnalité d’émulateur est automatiquement intégrée dans la page par le biais du mécanisme suivant :

* Le composant de page mobile `head.jsp` inclut le composant init de l’émulateur associé au groupe de périphériques (uniquement en mode de création) et le CSS de rendu du groupe de périphériques via : .

   `deviceGroup.drawHead(pageContext);`

* La méthode `DeviceGroup.drawHead(pageContext)` inclut le composant d&#39;initialisation de l&#39;émulateur, c&#39;est-à-dire appelle la `init.html.jsp` du composant d&#39;émulateur. Si le composant d&#39;émulateur ne possède pas son propre `init.html.jsp` et s&#39;appuie sur l&#39;émulateur de base mobile ( `wcm/mobile/components/emulators/base)`), le script d&#39;initialisation de l&#39;émulateur de base mobile est appelé ( `/libs/wcm/mobile/components/emulators/base/init.html.jsp`).

* Le script d’initialisation de l’émulateur de base mobile définit via Javascript :

   * la configuration de tous les émulateurs qui sont définis pour la page (emulatorConfigs) ;
   * Gestionnaire d&#39;émulateurs qui intègre les fonctionnalités de l&#39;émulateur dans la page par :

      `emulatorMgr.launch(config)`;

      Le gestionnaire d&#39;émulateurs est défini par :

      `/libs/wcm/emulator/widgets/source/EmulatorManager.js`

#### Création d’un émulateur mobile personnalisé {#creating-a-custom-mobile-emulator}

Pour créer un émulateur mobile personnalisé :

1. Ci-dessous `/apps/myapp/components/emulators` créez le composant `myemulator` (type de noeud : `cq:Component`).

1. Définissez la propriété `sling:resourceSuperType` sur `/libs/wcm/mobile/components/emulators/base`

1. Définissez une bibliothèque cliente CSS avec la catégorie `cq.wcm.mobile.emulator` pour l’aspect de l’émulateur : name = `css`, node type = `cq:ClientLibrary`

   Par exemple, vous pouvez vous référer au noeud `/libs/wcm/mobile/components/emulators/iPhone/css`

1. Si nécessaire, définissez une bibliothèque cliente JS, par exemple pour définir un module externe spécifique : name = js, node type = cq:ClientLibrary

   Par exemple, vous pouvez vous référer au noeud `/libs/wcm/mobile/components/emulators/base/js`

1. Si l’émulateur prend en charge des fonctionnalités spécifiques définies par des modules externes (comme le défilement tactile), créez un noeud de configuration sous l’émulateur : name = `cq:emulatorConfig`, node type = `nt:unstructured` et ajoutez la propriété qui définit le module externe :

   * Nom = `canRotate`, Type = `Boolean`, Valeur = `true` : pour inclure la fonctionnalité de rotation.

   * Nom = `touchScrolling`, Type = `Boolean`, Valeur = `true` : pour inclure la fonctionnalité de défilement tactile.

   Plus de fonctionnalités peuvent être ajoutées en définissant vos propres modules externes.

