---
title: Émulateurs
description: AEM permet aux auteurs et aux autrices d’afficher une page dans un émulateur qui simule l’environnement dans lequel un utilisateur final ou une utilisatrice finale consultera la page.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
legacypath: /content/docs/en/aem/6-0/develop/mobile/emulators
exl-id: 009b7e2c-ac37-4acc-a656-0a34d3853dfd
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: ht
source-wordcount: '609'
ht-degree: 100%

---

# Émulateurs{#emulators}

{{ue-over-mobile}}

Adobe Experience Manager (AEM) permet aux auteurs et aux autrices d’afficher une page dans un émulateur qui simule l’environnement dans lequel un utilisateur final ou une utilisatrice finale consultera la page, par exemple sur un appareil mobile ou dans un client de messagerie.

Le framework de l’émulateur AEM :

* fournit des fonctions de création de contenu dans une interface utilisateur (IU) simulée, par exemple, un appareil mobile ou un client de messagerie électronique (utilisé pour rédiger des newsletters) ;
* adapte le contenu de la page selon l’IU simulée ;
* permet de créer des émulateurs personnalisés.

>[!CAUTION]
>
>Cette fonctionnalité est prise en charge uniquement dans l’interface utilisateur classique.

## Caractéristiques des émulateurs {#emulators-characteristics}

Un émulateur :

* est basé sur ExtJS ;
* fonctionne sur le DOM de la page.
* Son apparence est gérée par du CSS.
* Prend en charge les plug-ins (par exemple, le plug-in de rotation de l’écran d’un appareil mobile).
* Est uniquement actif pour l’auteur ou l’autrice.
* possède son composant de base à l’adresse `/libs/wcm/emulator/components/base`.

### Comment l’émulateur transforme le contenu {#how-the-emulator-transforms-the-content}

L’émulateur fonctionne en encapsulant le contenu du corps du HTML dans des DIV de l’émulateur. Par exemple, le code HTML qui suit :

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

* La balise div avec l’ID `cq-emulator-content` représentant la zone viewport/screen/content de l’appareil où réside le contenu de la page.

De nouvelles classes CSS sont également attribuées aux nouvelles balises div d’émulateurs : elles représentent le nom de l’émulateur actuel.

Les modules externes d’un émulateur peuvent développer la liste des classes CSS attribuées, comme dans l’exemple du module externe de rotation qui insère une classe « vertical » ou « horizontal » en fonction de la rotation de l’appareil actif.

De cette manière, l’aspect complet de l’émulateur peut être contrôlé à l’aide de classes CSS correspondant aux ID et classes CSS des balises div d’émulateurs.

>[!NOTE]
>
>Il est recommandé que le HTML du projet encapsule le contenu du corps dans une seule balise div, comme dans l’exemple ci-dessus. Si le contenu du corps contient plusieurs balises, des résultats imprévisibles peuvent se produire.

### Émulateurs mobiles {#mobile-emulators}

Les émulateurs mobiles existants :

* se trouvent dans /libs/wcm/mobile/components/emulators.
* sont disponibles par le biais de la servlet JSON à l’adresse :

  http://localhost:4502/bin/wcm/mobile/emulators.json

Lorsque le composant de page s’appuie sur le composant de page mobile (`/libs/wcm/mobile/components/page`), la fonctionnalité d’émulateur est automatiquement intégrée dans la page par le mécanisme suivant :

* Le composant de page mobile `head.jsp` inclut le composant init de l’émulateur associé au groupe d’appareils (uniquement en mode de création) et le CSS de rendu du groupe d’appareils via :

  `deviceGroup.drawHead(pageContext);`

* La méthode `DeviceGroup.drawHead(pageContext)` inclut le composant init de l’émulateur, c’est-à-dire qu’elle appelle le `init.html.jsp` du composant de l’émulateur. Si le composant d’émulateur ne possède pas son propre `init.html.jsp` et s’appuie sur l’émulateur mobile de base (`wcm/mobile/components/emulators/base)`, le script init de l’émulateur mobile de base est appelé (`/libs/wcm/mobile/components/emulators/base/init.html.jsp`).

* Le script init de l’émulateur mobile de base définit, via un code JavaScript :

   * la configuration de tous les émulateurs qui sont définis pour la page (emulatorConfigs) ;
   * le gestionnaire d’émulateur qui intègre la fonctionnalité de l’émulateur dans la page via :

     `emulatorMgr.launch(config)` ;

     Le gestionnaire d’émulateur est défini par :

     `/libs/wcm/emulator/widgets/source/EmulatorManager.js`

#### la création d’un émulateur mobile personnalisé. {#creating-a-custom-mobile-emulator}

Pour créer un émulateur mobile personnalisé :

1. En-dessous de `/apps/myapp/components/emulators`, créez le composant ; `myemulator` (type de nœud : `cq:Component`).

1. Définissez la propriété `sling:resourceSuperType` sur `/libs/wcm/mobile/components/emulators/base`.

1. Définition d’une bibliothèque cliente CSS avec une catégorie `cq.wcm.mobile.emulator` pour l’aspect de l’émulateur : nom = `css`, type de nœud = `cq:ClientLibrary`.

   À titre d’exemple, vous pouvez vous reporter au nœud `/libs/wcm/mobile/components/emulators/iPhone/css`.

1. Si nécessaire, définissez une bibliothèque cliente JS, par exemple, pour définir un plug-in externe spécifique : nom = js, type de nœud = cq:ClientLibrary

   À titre d’exemple, vous pouvez vous reporter au nœud `/libs/wcm/mobile/components/emulators/base/js`.

1. Si l’émulateur prend en charge des fonctionnalités spécifiques définies par des modules externes (comme le défilement tactile), créez un nœud de configuration sous l’émulateur : nom = `cq:emulatorConfig`, type de nœud = `nt:unstructured`, et ajoutez la propriété qui définit le module externe :

   * Nom = `canRotate`, Type = `Boolean`, Valeur = `true` : pour inclure la fonctionnalité de rotation.

   * Nom = `touchScrolling`, type = `Boolean`, valeur = `true` : pour inclure la fonctionnalité de défilement tactile.

   Plus de fonctionnalités peuvent être ajoutées en définissant vos propres modules externes.
