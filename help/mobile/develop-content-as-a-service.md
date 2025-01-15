---
title: Diffusion de contenu
description: Découvrez comment utiliser tout le contenu de Adobe Experience Manager pour offrir l’expérience d’application ciblée.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
exl-id: 85e73679-684e-402f-8186-8b56d8bd9372
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 1%

---

# Diffusion de contenu{#content-delivery}

{{ue-over-mobile}}

Les applications mobiles doivent pouvoir utiliser tout le contenu d’AEM selon les besoins pour offrir l’expérience d’application ciblée.

Cela inclut l’utilisation de ressources, de contenu de site, de contenu CaaS (en direct) et de contenu personnalisé qui peut avoir sa propre structure.

>[!NOTE]
>
>Le **contenu en direct** peut provenir de l’un des éléments ci-dessus par le biais de gestionnaires ContentSync. Il peut être utilisé pour traiter par lots les packages et les diffusions par le biais de fichiers zip, et pour gérer les mises à jour de ces packages.

Il existe trois principaux types de documents fournis par Content Services :

1. **Assets**
1. **Contenu d’HTML empaqueté (HTML/CSS/JS)**
1. **Contenu indépendant du canal**

![chlimage_1-154](assets/chlimage_1-154.png)

## Ressources {#assets}

Les collections de ressources sont des éléments AEM qui contiennent des références à d’autres collections.

Une collection de ressources peut être exposée via Content Services. L’appel d’une collection de ressources dans une requête renvoie un objet qui est une liste des ressources, y compris leurs URL. Les Assets sont accessibles via une URL. L’URL est fournie dans un objet . Par exemple :

* Une entité de page renvoie le JSON (objet de page) qui inclut une référence d’image. La référence de l’image est une URL utilisée pour obtenir le fichier binaire de la ressource pour l’image.
* Une demande de liste de ressources dans un dossier renvoie le fichier JSON avec des détails sur toutes les entités de ce dossier. Cette liste est un objet . Le fichier JSON contient des références d’URL qui sont utilisées pour obtenir le fichier binaire de chaque ressource de ce dossier.

### Optimisation des ressources {#asset-optimization}

L’une des valeurs clés de Content Services est la possibilité de renvoyer des ressources optimisées pour l’appareil. Cela réduit les besoins de stockage de l’appareil local et améliore les performances de l’application.

L’optimisation des ressources est une fonction côté serveur, basée sur les informations fournies dans la requête API. Dans la mesure du possible, les rendus de ressources doivent être mis en cache afin que des requêtes similaires ne nécessitent pas de régénération du rendu de ressources.

### Workflow Assets {#assets-workflow}

Le workflow des ressources se présente comme suit :

1. Référence des ressources disponible dans AEM prêt à l’emploi
1. Créer une entité de référence de ressource en fonction de son modèle
1. Modifier l’entité

   1. Choisir une ressource ou une collection de ressources
   1. Personnaliser le rendu JSON

Le diagramme suivant illustre le workflow de référence **Assets** :

![chlimage_1-155](assets/chlimage_1-155.png)

### Gestion des ressources {#managing-assets}

Content Services permet d’accéder aux ressources gérées par AEM qui ne peuvent pas être référencées par d’autres contenus AEM.

#### Managed Assets existant {#existing-managed-assets}

Un utilisateur d’AEM Sites et d’Assets utilise AEM Assets pour gérer tous ses contenus numériques sur tous les canaux. Ils développent une application mobile native et doivent utiliser plusieurs ressources gérées par AEM Assets. Par exemple, les logos, les images d’arrière-plan et les icônes de bouton.

Actuellement, ils sont répartis autour du référentiel Assets. Les fichiers que l’application doit référencer se trouvent dans les emplacements suivants :

* /content/dam/geometrixx-outdoors/brand/logo_light.png
* /content/dam/geometrixx-outdoors/brand/logo_dark.png
* /content/dam/geometrixx-outdoors/styles/backgrounds/grey_blue.jpg
* /content/dam/geometrixx-outdoors/brand/icons/app/cart.png
* /content/dam/geometrixx-outdoors/brand/icons/app/home.png

#### Accès aux entités de ressources CS {#accessing-cs-asset-entities}

Mettons de côté les étapes de la mise à disposition de la page par le biais de l’API pour l’instant (elle est couverte par la description de l’interface utilisateur d’AEM) et supposons qu’elle a été effectuée. Des entités de ressource ont été créées et ajoutées à l’espace « appImages ». D’autres dossiers ont été créés sous l’espace à des fins d’organisation. Les entités de ressource sont donc stockées dans le JCR AEM sous la forme :

* /content/entities/appImages/logos/logo_light
* /content/entities/appImages/logos/logo_dark
* /content/entities/appImages/bkgnd/gray_blue
* /content/entities/appImages/icons/cart
* /content/entities/appImages/icons/home

#### Obtention d’une liste des entités de ressource disponibles {#getting-a-list-of-available-asset-entities}

Un développeur ou une développeuse d’applications peut obtenir une liste des ressources disponibles en récupérant les entités de ressources. Le point d’entrée de l’espace Content Services peut fournir ces informations via le SDK de l’API de service web.

Le résultat serait un objet au format JSON qui fournirait une liste des ressources dans le dossier « icônes ».

![chlimage_1-156](assets/chlimage_1-156.png)

#### Obtention d’une image {#getting-an-image}

Le fichier JSON fournit une URL pour chaque image générée par Content Services à l’image.

Pour obtenir le fichier binaire de l’image « cart » (panier), la bibliothèque cliente est de nouveau utilisée.

## Contenu d’HTML empaqueté {#packaged-html-content}

Un contenu HTML est nécessaire pour les clients qui doivent conserver la mise en page du contenu. Cela s’avère utile pour les applications natives qui utilisent un conteneur web, tel qu’une vue web Cordova, afin d’afficher le contenu.

AEM Content Services fournit du contenu HTML à l’application mobile au moyen de l’API . Les clients qui souhaitent exposer du contenu AEM en tant qu’HTML peuvent créer une entité de page d’HTML qui pointe vers la source de contenu AEM.

Les options suivantes sont prises en compte :

* **Fichier Zip :** pour optimiser les chances de s’afficher correctement sur l’appareil, les documents référencés de la page, tels que css, JavaScript, assets, etc., sont inclus dans un seul fichier compressé avec la réponse . Les références de la page d’HTML peuvent être ajustées afin d’utiliser un chemin d’accès relatif à ces fichiers.
* **Streaming :** obtention d&#39;un manifeste des fichiers requis d&#39;AEM. Utilisez ensuite ce manifeste pour demander tous les fichiers (HTML, CSS, JS, etc.) avec les requêtes suivantes.

![chlimage_1-157](assets/chlimage_1-157.png)

## Contenu indépendant du canal {#channel-independent-content}

Le contenu indépendant du canal permet de présenter des éléments de contenu AEM, tels que des pages, sans se soucier de la mise en page, des composants ou d’autres informations spécifiques au canal.

Ces entités de contenu sont générées à l’aide d’un modèle de contenu pour traduire les structures AEM au format JSON. Les données JSON obtenues contiennent des informations sur les données du contenu qui sont découplées du référentiel AEM. Cela inclut le renvoi de métadonnées et de liens de référence AEM aux ressources et les relations entre les structures de contenu, y compris la hiérarchie des entités.

### Gestion de contenu indépendant du canal {#managing-channel-independent-content}

Le contenu peut accéder à l’application de plusieurs façons.

1. GET ZIPS par le biais d&#39;AEM Over-the-Air

   * Les gestionnaires de synchronisation de contenu peuvent mettre à jour le package zip directement ou en appelant les moteurs de rendu de contenu existants

      * Gestionnaires de plateforme
      * Gestionnaires AEM
      * Gestionnaires personnalisés

1. GET de contenu directement par le biais de rendus de contenu

   * Rendus Sling par défaut prêts à l’emploi
   * AEM Mobile/Content Services Content Renderers
   * Rendus personnalisés
