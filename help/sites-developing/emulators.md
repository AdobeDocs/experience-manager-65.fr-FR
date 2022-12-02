---
title: Émulateurs
seo-title: Emulators
description: AEM permet aux auteurs d’afficher une page dans un émulateur qui simule l’environnement dans lequel un utilisateur final consulte la page.
seo-description: AEM enables authors to view a page in an emulator that simulates the environment in which an end-user will view the page
uuid: ee1496a5-be68-4318-b5ce-b11c41e4485c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
discoiquuid: c51fca81-5dfc-4838-9672-acb6de62778b
legacypath: /content/docs/en/aem/6-0/develop/mobile/emulators
exl-id: 009b7e2c-ac37-4acc-a656-0a34d3853dfd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '631'
ht-degree: 100%

---

# Émulateurs{#emulators}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

Adobe Experience Manager (AEM) permet aux auteurs d’afficher une page dans un émulateur qui simule l’environnement dans lequel un utilisateur final consulte la page, comme un appareil mobile ou un client de messagerie électronique.

Le framework de l’émulateur AEM :

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
* possède son composant de base à l’adresse `/libs/wcm/emulator/components/base`.

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

Les modules externes d’un émulateur peuvent développer la liste des classes CSS attribuées, comme dans l’exemple du module externe de rotation qui insère une classe « vertical » ou « horizontal » en fonction de la rotation du périphérique actif.

De cette manière, l’aspect complet de l’émulateur peut être contrôlé à l’aide de classes CSS correspondant aux ID et classes CSS des balises div d’émulateurs.

>[!NOTE]
>
>Il est recommandé que le projet HTML encapsule le contenu du corps dans une seule balise div, comme dans l’exemple ci-dessus. Si le contenu du corps contient plusieurs balises, les résultats peuvent être imprévisibles.

### Émulateurs mobiles {#mobile-emulators}

Les émulateurs mobiles existants :

* se trouvent sous /libs/wcm/mobile/components/emulators ;
* sont disponibles par le biais de la servlet JSON à l’adresse :

   http://localhost:4502/bin/wcm/mobile/emulators.json

Lorsque le composant de page s’appuie sur le composant de page mobile (`/libs/wcm/mobile/components/page`), la fonctionnalité d’émulateur est automatiquement intégrée dans la page par le mécanisme suivant :

* Le composant de page mobile `head.jsp` inclut le composant init de l’émulateur associé au groupe de périphériques (uniquement en mode de création) et le CSS de rendu du groupe de périphériques via :

   `deviceGroup.drawHead(pageContext);`

* La méthode `DeviceGroup.drawHead(pageContext)` inclut le composant init de l’émulateur, c’est-à-dire qu’elle appelle le `init.html.jsp` du composant d’émulateur. Si le composant d’émulateur ne possède pas son propre `init.html.jsp` et s’appuie sur l’émulateur mobile de base (`wcm/mobile/components/emulators/base)`, le script init de l’émulateur mobile de base est appelé (`/libs/wcm/mobile/components/emulators/base/init.html.jsp`).

* Le script init de l’émulateur mobile de base définit par le biais d’un code JavaScript :

   * la configuration de tous les émulateurs qui sont définis pour la page (emulatorConfigs) ;
   * le gestionnaire d’émulateur qui intègre la fonctionnalité de l’émulateur dans la page via :

      `emulatorMgr.launch(config)` ;

      Le gestionnaire d’émulateur est défini par :

      `/libs/wcm/emulator/widgets/source/EmulatorManager.js`

#### Création d’un émulateur mobile personnalisé {#creating-a-custom-mobile-emulator}

Pour créer un émulateur mobile personnalisé :

1. En-dessous de `/apps/myapp/components/emulators`, créez le composant ; `myemulator` (type de nœud : `cq:Component`).

1. Définissez la propriété `sling:resourceSuperType` sur `/libs/wcm/mobile/components/emulators/base`.

1. Définition d’une bibliothèque cliente CSS avec une catégorie `cq.wcm.mobile.emulator` pour l’aspect de l’émulateur : nom = `css`, type de nœud = `cq:ClientLibrary`.

   À titre d’exemple, vous pouvez vous reporter au nœud `/libs/wcm/mobile/components/emulators/iPhone/css`.

1. Si nécessaire, définissez une bibliothèque cliente JS, par exemple pour définir un module externe spécifique : nom = js, type de nœud = cq:ClientLibrary.

   À titre d’exemple, vous pouvez vous reporter au nœud `/libs/wcm/mobile/components/emulators/base/js`.

1. Si l’émulateur prend en charge des fonctionnalités spécifiques définies par des modules externes (comme le défilement tactile), créez un nœud de configuration sous l’émulateur : nom = `cq:emulatorConfig`, type de nœud = `nt:unstructured`, et ajoutez la propriété qui définit le module externe :

   * Nom = `canRotate`, Type = `Boolean`, Valeur = `true` : pour inclure la fonctionnalité de rotation.

   * Nom = `touchScrolling`, type = `Boolean`, valeur = `true` : pour inclure la fonctionnalité de défilement tactile.
   Plus de fonctionnalités peuvent être ajoutées en définissant vos propres modules externes.
