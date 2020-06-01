---
title: Utilisation de fichiers 3D dans Contenu multimédia dynamique
seo-title: Utilisation de fichiers 3D dans Contenu multimédia dynamique
description: Découvrez comment utiliser des ressources 3D dans Contenu multimédia dynamique
seo-description: Découvrez comment utiliser des ressources 3D dans Contenu multimédia dynamique
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS and AEM as a Cloud Service
topic-tags: introduction
content-type: reference
translation-type: tm+mt
source-git-commit: 46848fee0a3f838354ec65f2ea733cf70ac53deb
workflow-type: tm+mt
source-wordcount: '2162'
ht-degree: 13%

---


# Utilisation de fichiers 3D dans Contenu multimédia dynamique {#working-with-three-d-assets-dm}

Contenu multimédia dynamique vous permet de télécharger, de gérer, de vue et de diffuser des fichiers 3D sous la forme d’expériences immersives.

* Publication en un clic (à l’aide de la publication **** rapide sur la barre d’outils) d’images 3D pour générer son URL.
* Prise en charge optimisée de l’affichage de fichiers 3D avec le paramètre prédéfini de visionneuse de dimensions interactive de haute qualité optimisé par Adobe Dimension. Le paramètre prédéfini de la visionneuse comprend, entre autres, un ensemble de commandes de caméra interactives qui vous permettent d’effectuer un zoom en orbite, un zoom et un panoramique.
* Le composant WCM 3D Media vous permet d’ajouter facilement des ressources 3D à vos pages de sites AEM.

Il n’existe aucune installation ou configuration permettant d’utiliser des ressources 3D dans Contenu multimédia dynamique.

![chaussure en 3d](/help/assets/assets-dm/3d-dimensional-viewer-quickpublish-url-embed2.png)

<!-- See also [Dynamic Media 3D Release Notes](/help/release-notes/aem3d-release-notes.md). -->

## Formats de fichiers 3D pris en charge dans Contenu multimédia dynamique {#supported-three-d-file-formats-in-dm}

Dynamic Media prend en charge les formats de fichier 3D suivants :

| Extension de fichier 3D | Format de fichier | Type MIME | Notes |
|---|---|---|---|
| GLB | Transmission GL binaire | model/gltf-binary | Inclut les textures avec le fichier au lieu de les référencer comme des images externes. |
| OBJ | Fichier d’objet 3D WaveFront | application/x-tgif |  |
| STL | Stéréolithographie | application/vnd.ms-pki.stl |  |
| USDZ | Archive zip de description de scène universelle | model/vnd.usdz+zip | *Prise en charge de l&#39;ingestion uniquement ; aucun affichage ou interaction n’est disponible.* USDZ est le format 3D propriétaire d’Apple qui ne peut être vue que par Safari ou iOS. |

## Début rapide : Fichiers 3D dans Contenu multimédia dynamique {#quick-start-three-d}

La description de flux de travaux détaillée suivante est conçue pour vous aider à maîtriser rapidement les opérations liées aux fichiers 3D en mode Contenu multimédia dynamique - Scene7.

>[!NOTE]
>
>Les ressources 3D ne sont pas prises en charge en mode Contenu multimédia dynamique - hybride.

Avant d’utiliser des ressources 3D dans Contenu multimédia dynamique, assurez-vous que votre administrateur AEM a déjà activé et configuré les services Contenu multimédia dynamique dans le mode Contenu multimédia dynamique - Scene7.

Voir [Configuration des services cloud Dynamic Media](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services) dans Configuration de Dynamic Media – mode Scene7 et [Dépannage de Dynamic Media – mode Scene7.](/help/assets/troubleshoot-dms7.md)

1. **Téléchargement de fichiers 3D**

   * [Téléchargement de vos fichiers 3D pour les utiliser dans Contenu multimédia](/help/assets/managing-assets-touch-ui.md#uploading-assets)dynamique.
   * [Formats de fichiers 3D pris en charge pour le téléchargement dans Contenu multimédia](#supported-three-d-file-formats-in-dm)dynamique.

1. **Gestion des fichiers 3D**

   * Organisation et recherche de fichiers 3D

      * [Organisation des ressources](/help/assets/organize-assets.md#organize-digital-assets)numériques.
      * [Recherche de fichiers](/help/assets/search-assets.md)3D.
      * [Utilisation de prédicats personnalisés pour filtrer les résultats](/help/assets/search-assets.md#custompredicates)de la recherche.
   * Fichiers Vue 3D

      * [Affichage et interaction avec des ressources](#viewing-three-d-assets)3D.
      * [Gestion du paramètre prédéfini](/help/assets/managing-viewer-presets.md)de la visionneuse de dimensions.
   * Utilisation des métadonnées de fichier 3D

      * [Gestion des métadonnées des ressources numériques](/help/assets/metadata.md).
      * [Schémas de métadonnées](/help/assets/metadata-schemas.md).



1. **Publication de fichiers 3D**

   * [Publication de fichiers Contenu multimédia dynamique 3D](#publishing-three-d-assets)

## A propos de l&#39;affichage et de l&#39;interaction avec des ressources 3D {#viewing-three-d-assets}

Cette section décrit comment vue et interagir avec des ressources 3D de deux manières différentes : dans la page des détails de la ressource et dans le composant Média 3D des sites.

La visionneuse 3D interactive comprend, entre autres, une série de commandes de caméra interactives qui vous permettent d’effectuer des zooms, des zooms et des panoramiques sur le fichier 3D.

Gardez à l’esprit que le temps nécessaire pour ouvrir un fichier 3D dans la vue de page Détails du fichier dépend de plusieurs facteurs. Ces facteurs sont entre autres :

* Bande passante du serveur.
* Latences au serveur
* Complexité de l’image.

En outre, les capacités de l&#39;ordinateur client (tel qu&#39;une station de travail, un ordinateur portable ou un périphérique tactile mobile) sont également importantes à prendre en compte lorsque vous manipulez la caméra de manière interactive. Un système relativement puissant avec de bonnes capacités graphiques peut rendre l’expérience interactive d’affichage en 3D plus fluide et plus favorable.

>[!TIP]
>
>Vous pouvez ouvrir le paramètre prédéfini de visionneuse de dimensions dans l’éditeur de paramètres prédéfinis de la visionneuse pour vous entraîner à naviguer dans un fichier 3D sans avoir à télécharger au préalable des fichiers 3D. Le paramètre prédéfini de la visionneuse de dimensions comporte un fichier 3D intégré avec lequel vous pouvez interagir.
>
>See [Managing viewer presets](/help/assets/managing-viewer-presets.md).

## Affichage et interaction avec un fichier 3D à partir de la page des détails de l&#39;élément {#viewing-three-d-assets-from-asset-details-page}

Voir aussi [Prévisualisation de fichiers à l’aide de l’interface](/help/assets/previewing-assets.md)logicielle.

**Pour vue et interagir avec un fichier 3D à partir de la page des détails du fichier**

1. Assurez-vous d’avoir chargé des ressources 3D dans AEM.

   Voir [Téléchargement de vos fichiers 3D en vue de les utiliser dans Contenu multimédia](/help/assets/managing-assets-touch-ui.md#uploading-assets)dynamique.

1. Dans AEM, sur la page de **[!UICONTROL navigation]**, appuyez sur **[!UICONTROL Ressources > Fichiers]**.
1. Near the upper-right corner of the page, from the **[!UICONTROL View]** drop-down list, tap **[!UICONTROL Card View]**.
1. Accédez à une ressource 3D que vous souhaitez afficher.
1. Appuyez sur la carte de la ressource 3D pour l’ouvrir sur la page Détails de l’actif.
1. Sur la page de vue des détails de la ressource 3D, effectuez l&#39;une des opérations suivantes :

   * **Tournez votre caméra** - Orblez votre vue autour de la scène et des objets 3D.
      * _Souris_ : cliquez avec le bouton gauche et faites glisser.
      * _Écran tactile_ : appuyez sur un seul doigt et faites glisser.
   * **Panoramique de l&#39;appareil photo** - Panoramique de votre vue à gauche, à droite, vers le haut ou vers le bas.
      * _Souris_ : cliquez avec le bouton droit et faites glisser.
      * _Écran tactile_ : appuyez avec deux doigts et faites glisser.
   * **Zoom sur votre caméra** : effectuez un zoom sur votre caméra pour vous déplacer dans et hors des zones de la scène 3D.
      * _Souris_ : roulette de défilement.
      * _Écran tactile_ : rapprocher les deux doigts.
   * **Recentrer votre appareil photo** : recréer votre appareil photo à un point sur un objet de la scène 3D.
      * _Souris_ : double-cliquez.
      * _Écran_ tactile : appuyez deux fois.
   * **Réinitialiser** - Près du coin inférieur droit de la page, appuyez sur l&#39;icône Réinitialiser pour rétablir le point de cible de la vue au centre de la ressource 3D. De plus, Réinitialiser rapproche ou éloigne l’angle de vue pour afficher la ressource dans son intégralité et à une taille raisonnable.
   * **Mode** plein écran : pour passer en mode plein écran, dans le coin inférieur droit de la page, appuyez sur l&#39;icône Plein écran.

1. Dans le coin supérieur droit de la page, appuyez sur **[!UICONTROL Fermer]** pour revenir à la page Assets.

## Affichage et interaction avec un fichier 3D dans un composant multimédia 3D {#interacting-with-asset-inside-three-d-media-component}

Lorsqu’une page Web est en mode **[!UICONTROL Edition]** , aucune interaction n’est possible avec une ressource 3D. Pour rendre le fichier interactif, vous pouvez utiliser la fonction **[!UICONTROL Prévisualisation]** pour vue de la page Web dans l’éditeur de page avec un accès complet aux fonctionnalités du composant Média 3D.

>[!IMPORTANT]
>
>Vous ne pouvez accomplir cette tâche qu’après avoir ajouté un composant Média 3D à une page Web et y avoir affecté un élément 3D. Voir [Ajouter le composant Média 3D à une page](#adding-the-three-d-media-component-to-a-web-page) Web et [Affecter un fichier 3D à un composant](#assigning-a-three-d-asset-to-the-component)Média 3D.

Voir aussi [Prévisualisation de fichiers à l’aide de l’interface](/help/assets/previewing-assets.md)logicielle.

**Pour vue et interaction avec un fichier 3D dans un composant multimédia 3D**

1. Lorsqu’une page Web est en mode **[!UICONTROL Edition]** , effectuez l’une des opérations suivantes :

   * Près de l’angle supérieur droit de la page, cliquez sur **[!UICONTROL Prévisualisation]** pour passer en mode **[!UICONTROL Prévisualisation]** .
   * Supprimez `/editor.html` de l’URL de la page dans le navigateur.
   ![Ressource 3D affichée dans le composant](/help/assets/assets-dm/3d-asset-in-3d-media.png)Média 3D Ressource 3D entièrement interactive telle qu’elle s’affiche en mode **[!UICONTROL Prévisualisation]** .

1. En mode **[!UICONTROL Prévisualisation]** , effectuez l’une des opérations suivantes :

   * **Tournez votre caméra** - Orblez votre vue autour de la scène et des objets 3D.
      * _Souris_ : cliquez avec le bouton gauche et faites glisser.
      * _Écran tactile_ : appuyez sur un seul doigt et faites glisser.
   * **Panoramique de l&#39;appareil photo** - Panoramique de votre vue à gauche, à droite, vers le haut ou vers le bas.
      * _Souris_ : cliquez avec le bouton droit et faites glisser.
      * _Écran tactile_ : appuyez avec deux doigts et faites glisser.
   * **Zoom sur votre caméra** : effectuez un zoom sur votre caméra pour vous déplacer dans et hors des zones de la scène 3D.
      * _Souris_ : roulette de défilement.
      * _Écran tactile_ : rapprocher les deux doigts.
   * **Recentrer votre appareil photo** : recréer votre appareil photo à un point sur un objet de la scène 3D.
      * _Souris_ : double-cliquez.
      * _Écran_ tactile : appuyez deux fois.
   * **Réinitialiser** - Près du coin inférieur droit de la page, appuyez sur l&#39;icône Réinitialiser pour rétablir le point de cible de la vue au centre de la ressource 3D. De plus, Réinitialiser rapproche ou éloigne l’angle de vue pour afficher la ressource dans son intégralité et à une taille raisonnable.
   * **Mode** plein écran : pour passer en mode plein écran, dans le coin inférieur droit de la page, appuyez sur l&#39;icône Plein écran.

## A propos de l&#39;utilisation du composant Média 3D {#working-with-three-d-media-component}

Contenu multimédia dynamique comprend un composant Contenu multimédia 3D dynamique que vous pouvez utiliser dans les sites AEM pour activer l’affichage interactif de modèles 3D sur vos pages Web.

* [Ajouter le composant Média 3D au modèle de page](#adding-three-d-media-component-to-page-template)
* [Ajouter le composant Média 3D à une page Web](#adding-the-three-d-media-component-to-a-web-page)
   * [Facultatif - Configuration du composant Média 3D](#configuring-the-three-d-component)
* [Affectation d’un fichier 3D au composant Média 3D](#assigning-a-three-d-asset-to-the-component)


## Adding the 3D Media component to the page template {#adding-three-d-media-component-to-page-template}

1. Accédez à **[!UICONTROL Outils > Général > Modèles]**.
1. Accédez au modèle de page dans lequel vous souhaitez activer le composant 3D, puis sélectionnez le modèle.
1. Tap **[!UICONTROL Edit]** to open the template.
1. Près de l’angle supérieur droit de la page, dans le menu déroulant, sélectionnez le mode **[!UICONTROL Structure]** , s’il n’est pas déjà actif.

   ![3d-media-component-structure](/help/assets/assets-dm/3d-media-component-structure.png)

1. Appuyez sur une zone vide de la région Conteneur **[!UICONTROL de]** mise en page pour la sélectionner et ouvrir sa barre d’outils associée.
1. Dans la barre d’outils, appuyez sur l’icône **[!UICONTROL Stratégie]** pour ouvrir l’éditeur **[!UICONTROL de]** stratégie.
1. Dans la section **[!UICONTROL Propriétés]** , sous l’onglet Composants **** autorisés, faites défiler l’écran jusqu’à Contenu multimédia **** dynamique, puis développez la liste et cochez la case Contenu multimédia **[!UICONTROL 3D.]**
1. Appuyez sur **[!UICONTROL Terminé]** pour enregistrer les modifications et fermer l’éditeur **[!UICONTROL de]** stratégies.

   Vous pouvez maintenant placer le composant Contenu multimédia 3D dynamique sur toutes les pages qui utilisent ce modèle.

## Adding the 3D Media component to a web page {#adding-the-three-d-media-component-to-a-web-page}

Si vous utilisez Adobe Experience Manager comme système de gestion de contenu Web, vous pouvez ajouter des ressources 3D à vos pages Web au moyen du composant Média 3D.

See also [Adding Dynamic Media assets to pages](/help/assets/adding-dynamic-media-assets-to-pages.md).

1. Ouvrez Sites AEM et sélectionnez la page Web sur laquelle vous souhaitez ajouter le composant Contenu multimédia 3D Contenu multimédia dynamique.
1. Tap the **[!UICONTROL Edit]** (pencil) icon to open the page into the page editor. Assurez-vous que le mode **[!UICONTROL Modifier]** est sélectionné près de l’angle supérieur droit de la page.

   ![3d-media-component-add](/help/assets/assets-dm/3d-media-component-edit.png)

1. Sur la barre d’outils, appuyez sur l’icône du panneau latéral pour activer ou désactiver l’affichage du panneau.

1. Dans le panneau latéral, appuyez sur l’icône + pour ouvrir la liste **[!UICONTROL Composants]** .

   ![3d-media-component-drag-drop](/help/assets/assets-dm/3d-assets-filter.png)

1. Faites glisser le composant Média **** 3D de la liste **[!UICONTROL Composants]** vers l’emplacement de la page où doit apparaître la visionneuse 3D.

Vous êtes maintenant prêt à affecter une ressource 3D au composant.

Voir [Affectation d’un fichier 3D à un composant](#assigning-a-three-d-asset-to-the-component)multimédia 3D.

### Facultatif - Configuration du composant Média 3D {#configuring-the-three-d-component}

1. In the AEM Sites page editor, select the **[!UICONTROL 3D Media Viewer]** component that you previously added to the page.
1. Tap the **[!UICONTROL Configuration]** icon (wrench) to open the component configuration dialog box.

   ![3d-media-component-config](/help/assets/assets-dm/3d-media-component-config.png)

1. Dans la boîte de dialogue Média 3D, dans la liste déroulante Paramètres prédéfinis de la visionneuse, sélectionnez **[!UICONTROL Dimensionner]** pour affecter le paramètre prédéfini de visionneuse de dimensions au composant.

   ![3d-media-component-edit-config](/help/assets/assets-dm/3d-media-component-edit-config.png)

1. Dans le coin supérieur droit, cochez la case pour enregistrer vos modifications.

## Affectation d’un fichier 3D au composant Média 3D {#assigning-a-three-d-asset-to-the-component}

Après avoir ajouté un composant Média 3D à une page Web, vous pouvez lui affecter un fichier 3D.

See [Adding the 3D Media component to a web page](#adding-the-three-d-media-component-to-a-web-page).

1. In the AEM Sites page editor, click the **[!UICONTROL Assets]** icon to open **[!UICONTROL Assets]** in the side panel.
1. Dans la liste déroulante, sélectionnez **[!UICONTROL 3D]** pour afficher uniquement les types de fichier 3D.
1. Dans le panneau latéral, recherchez ou faites défiler la ressource 3D que vous souhaitez vue sur la page en cours de modification.
1. Faites glisser le fichier 3D du panneau latéral Ressources et déposez-le sur le composant Média **** 3D que vous avez précédemment ajouté à la page.

   ![Affecter un fichier 3d au composant Média 3d](/help/assets/assets-dm/3d-asset-add.png)

>[!NOTE]
>
>Lorsqu’une page Web est en mode **[!UICONTROL Edition]** des sites AEM, le composant Média 3D affiche la ressource 3D, mais aucune interaction avec la ressource n’est possible. Pour rendre le fichier interactif, vous pouvez utiliser la fonction **[!UICONTROL Prévisualisation]** pour vue de la page Web dans l’éditeur de page avec un accès complet aux fonctionnalités du composant Média 3D.

## Publishing Dynamic Media 3D assets {#publishing-three-d-assets}

Contenu multimédia dynamique accepte divers formats de fichier 3D pris en charge en tant que contenu ** statique dans Contenu multimédia dynamique. Le contenu statique signifie que vous pouvez télécharger et publier des fichiers 3D, mais qu’il n’existe aucune prise en charge de l’imagerie *dynamique* ou de la retouche d’image associée à la ressource 3D. La raison en est que Dynamic Media Imaging Server ne reconnaît pas les formats 3D. Ainsi, après avoir publié un fichier 3D dans Contenu multimédia dynamique, vous disposez d’une URL instantanée que vous pouvez copier. L’URL de la ressource 3D suit la structure d’URL de média dynamique habituelle. Cependant, vous ne pouvez pas modifier de paramètres dans l’URL du fichier, contrairement aux fichiers d’image traditionnels dans Contenu multimédia dynamique.

Dans la Vue **** Carte, une petite icône en forme de globe apparaît directement sous le nom d’un fichier et à gauche de sa date et de son heure pour indiquer qu’il est publié. En mode **[!UICONTROL Liste]**, une colonne **[!UICONTROL Publié]** indique les ressources qui sont publiées et celles qui ne le sont pas.

See also [Publishing Dynamic Media assets](publishing-dynamicmedia-assets.md).

Voir aussi [Publication de pages](/help/sites-authoring/publishing-pages.md).

>[!MORELIKETHIS]
>
>Si vous utilisez un système de gestion de contenu Web tiers, vous pouvez lier ou incorporer des ressources 3D à vos pages Web.
>
>Voir [Liaison d’URL à une application web](linking-urls-to-yourwebapplication.md).


**Pour publier des fichiers 3D Contenu multimédia dynamique**

1. Ouvrez une ressource 3D (format de fichier GLB, OBJ ou STL) pour la vue dans la page des détails de la ressource.
1. On the toolbar, tap **[!UICONTROL Quick Publish]**.

   ![3d-asset-quick-publish](/help/assets/assets-dm/3d-asset-quick-publish.png)

1. Appuyez sur **[!UICONTROL Fermer]** pour quitter la boîte de dialogue et revenir à la page des détails de la ressource.
1. Dans la liste déroulante située à gauche du nom de fichier de la ressource 3D, appuyez sur **[!UICONTROL Rendus]**.

   ![3d-asset-renditions](/help/assets/assets-dm/3d-asset-renditions.png)

1. Appuyez sur **[!UICONTROL original]**. Lorsqu’un fichier 3D est publié (ou &quot;activé&quot;), le bouton URL s’affiche dans le coin inférieur gauche de la page si toutes les conditions de ressource 3D suivantes sont remplies :
   * Le fichier 3D est un format pris en charge (GLB, OBJ, STL et USDZ).
   * Le fichier 3D a été assimilé au système IPS (Dynamic Media Image Production System).
   * Le fichier 3D est publié.
   ![3d-asset-url](/help/assets/assets-dm/3d-asset-url.png)

1. Appuyez sur **[!UICONTROL URL]** pour afficher l’URL de production du fichier 3D.
