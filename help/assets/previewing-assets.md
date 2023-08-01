---
title: Prévisualiser des ressources
description: Découvrez comment prévisualiser des ressources, telles que des vidéos et des images, dans Dynamic Media, en appliquant des paramètres d’image prédéfinis et des paramètres de visionneuse prédéfinis.
uuid: 09e97245-373b-4d50-8ba3-5d1034a29988
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: bb8c355c-4475-45ec-9096-0975f0ce2c27
docset: aem65
feature: Asset Management
role: User, Admin
exl-id: 84f0c406-4ab6-48c7-8223-61a8c3ade363
source-git-commit: 7f8cfe155af3b8831e746ced89c11c971e429f69
workflow-type: tm+mt
source-wordcount: '1380'
ht-degree: 85%

---

# Aperçu des ressources à l’aide de l’interface logicielle {#previewing-assets}

Vous pouvez utiliser la fonction Aperçu pour afficher une ressource numérique que vous avez chargée telle qu’elle sera présentée au client dans son navigateur web. La visionneuse par défaut incorporée inter-appareil affectée à la ressource est utilisée pour l’aperçu.

Une visionneuse est un ensemble de différents paramètres ou *paramètres prédéfinis*, comme la taille d’affichage de la visionneuse, le comportement du zoom, les modèles de couleurs, les bordures et les polices. Ces paramètres prédéfinis déterminent la manière dont les utilisateurs voient les ressources multimédias enrichies sur leurs écrans d’ordinateur et appareils mobiles.

Outre l’utilisation de la fonction d’aperçu dédiée pour la vidéo, les visionneuses à 360° et les visionneuses d’images, vous pouvez prévisualiser une ressource à l’aide des paramètres prédéfinis de visionneuse que vous avez créés. Vous pouvez également utiliser des paramètres d’image prédéfinis pour prévisualiser les rendus des images.

* [Application de paramètres prédéfinis d’image](/help/assets/image-presets.md)
* [Application de paramètres prédéfinis de la visionneuse](/help/assets/viewer-presets.md)

>[!NOTE]
>
>Lorsque vous vous trouvez sur une page web (Sites) dans Adobe Experience Manager, vous ne pouvez pas prévisualiser les ressources en mode d’**édition**. Accédez au mode Aperçu en cliquant sur **[!UICONTROL Aperçu]** dans le coin supérieur de la page.

Pour activer ou désactiver les paramètres prédéfinis de visionneuse dans l’interface utilisateur, consultez la section [Gestion des paramètres prédéfinis de visionneuse](/help/assets/managing-viewer-presets.md).

**Pour prévisualiser des ressources à l’aide de l’interface logicielle :**

1. Dans **[!UICONTROL Adobe Experience Manager]**, sur la page **[!UICONTROL Navigation]**, sélectionnez **[!UICONTROL Ressources]**, puis **[!UICONTROL Fichiers]** pour accéder aux ressources.
1. Dans le coin supérieur droit de la page, dans la liste déroulante **[!UICONTROL Afficher]**, sélectionnez **[!UICONTROL Vue Liste]**.
1. (Facultatif) Utilisez la colonne **[!UICONTROL Type]** pour trier les ressources en fonction du type que vous souhaitez prévisualiser.
1. Sous , **[!UICONTROL Titre]** , cliquez sur le nom du titre (et non sur l’image miniature) de la ressource à prévisualiser.
1. Selon le type de ressource sur lequel vous avez cliqué, effectuez l’une des opérations suivantes :


   <table>
    <tbody>
      <tr>
      <td><strong>Type de ressource sur lequel vous avez cliqué</strong><br /> </td>
      <td><strong>Est-il possible d’afficher un aperçu de la ressource dans un rendu particulier ?</strong></td>
      <td><strong>Est-il possible d’afficher un aperçu de la ressource dans une visionneuse ?</strong></td>
      <td> </td>
      </tr>
      <tr>
      <td><p>3D</p> </td>
      <td>Non</td>
      <td>Oui</td>
      <td><p><strong>Pour obtenir un aperçu d’une ressource 3D dans la visionneuse Dimensionnel</strong></p>
      <ul>
      <li>En haut à gauche de la page, cliquez sur l’icône pour afficher la liste déroulante. Sélectionnez <strong>Visionneuses</strong> dans la liste, puis sélectionnez la visionneuse dimensionnelle.</li>
      <li>Sélectionnez <strong>Réinitialiser</strong> si vous souhaitez rétablir l’image sur le zoom d’origine.</li>
      <li>Sélectionnez <strong>Plein écran</strong> pour agrandir la visionneuse sur l’appareil d’affichage.</li>
      </ul>
      <p><strong>Navigation dans la scène 3D</strong></p>
      <ul>
      <li><p><strong>Tournez votre appareil photo</strong> : faites tourner votre angle de vue autour de la scène et des objets 3D.</p> Souris : cliquez avec le bouton gauche et faites glisser </p> Écran tactile : appuyez et faites glisser</p></li>
      <li><p><strong>Panoramique</strong> : basculez votre angle de vue vers la gauche, la droite, le haut et le bas.</p> Souris : cliquez avec le bouton droit et faites glisser </p> Écran tactile : appuyez avec deux doigts et faites glisser</p></li>
      <li><p><strong>Zoom</strong> : permet de zoomer que vous puissiez déplacer l’appareil dans et hors des zones de la scène 3D.</p> Souris : effectuez un défilement à l’aide de la roulette </p> Écran tactile : effectuez un pincement du doigt</p></li>
      <li><p><strong>Recentrez votre appareil photo</strong> : faites tourner votre angle de vue autour de la scène et des objets 3D.</p> Souris : double-cliquez </p> Écran tactile : appuyez deux fois</li></ul></td>
      </tr>
      <tr>
      <td><p>Image</p> </td>
      <td>Oui</td>
      <td>Oui</td>
      <td><p><strong>Pour prévisualiser une ressource dans un rendu particulier</strong></p>
      <ul>
      <li>En haut à gauche de la page, cliquez sur l’icône pour afficher la liste déroulante. Sélectionnez <strong>Rendus</strong> dans la liste, puis sélectionnez un rendu spécifique à prévisualiser.</li>
      </ul> <p><strong>Pour prévisualiser une ressource dans une visionneuse particulière</strong></p>
      <ul>
      <li>En haut à gauche de la page, cliquez sur l’icône pour afficher la liste déroulante. Sélectionnez <strong>Visionneuses</strong> dans la liste, puis sélectionnez une visionneuse à appliquer à la ressource.</li>
      </ul> <p>Utilisez les icônes <strong>+</strong> et <strong>– </strong> pour augmenter ou réduire le zoom de l’image sélectionnée. Sélectionnez <strong>Réinitialiser</strong> si vous souhaitez rétablir l’image sur le zoom d’origine.<br /> Si vous utilisez un écran tactile, appuyez deux fois sur l’image pour effectuer un zoom avant par étapes. Lorsque vous atteignez le zoom maximal, appuyez à nouveau deux fois sur l’image pour réinitialiser l’état du zoom. Faites glisser sur l’image pour effectuer un panoramique.</p> </td>
      </tr>
      <tr>
      <td>Multimédia</td>
      <td>Oui</td>
      <td>Oui</td>
      <td><p><strong>Pour prévisualiser une ressource dans un rendu particulier</strong></p>
      <ul>
      <li>En haut à gauche de la page, cliquez sur l’icône pour afficher la liste déroulante. Sélectionnez <strong>Rendus</strong> dans la liste, puis sélectionnez un rendu spécifique à prévisualiser.</li>
      </ul> <p>La vidéo peut apparaître tronquée si vous sélectionnez une résolution plus élevée pour le rendu vidéo. Cette problématique est due au fait que l’aperçu du rendu vous indique la résolution exacte que vos clients vont voir, le tout dans le contexte de la visionneuse incorporée utilisée pour l’aperçu.</p> <p>Lorsque vous prévisualisez une visionneuse de vidéos adaptatives au niveau des ressources, les rendus sont regroupés dans une seule expérience de lecture. C’est-à-dire que la vidéo adaptable est dimensionnée de manière appropriée pour le visionnage et est lue avec la meilleure résolution possible pour l’appareil de visionnage et la vitesse de connexion utilisés.<br /> </p> <p><strong>Pour prévisualiser une ressource dans une visionneuse particulière</strong></p>
      <ul>
      <li>En haut à gauche de la page, cliquez sur l’icône pour afficher la liste déroulante. Sélectionnez <strong>Visionneuses</strong> dans la liste, puis sélectionnez une visionneuse à appliquer à la ressource.</li>
      </ul> </td>
      </tr>
      <tr>
      <td>Visionneuse d’images</td>
      <td>Non</td>
      <td>Oui</td>
      <td><p><strong>Pour prévisualiser une ressource dans une visionneuse particulière</strong></p>
      <ul>
      <li>En haut à gauche de la page, cliquez sur l’icône pour afficher la liste déroulante. Sélectionnez <strong>Visionneuses</strong> dans la liste, puis sélectionnez une visionneuse à appliquer à la ressource.</li>
      </ul> <p>Utilisez les icônes <strong>+</strong> et <strong>– </strong> afin que vous puissiez augmenter ou réduire le zoom de l’image sélectionnée. Sélectionnez <strong>Réinitialiser</strong> si vous souhaitez rétablir l’image sur le zoom d’origine.<br /> Si vous utilisez un écran tactile, appuyez deux fois sur l’image pour effectuer un zoom avant par étapes. Lorsque vous atteignez le zoom maximal, appuyez à nouveau deux fois sur l’image pour réinitialiser l’état du zoom. Faites glisser sur l’image pour effectuer un panoramique.</p> </td>
      </tr>
      <tr>
      <td>Visionneuse à 360°</td>
      <td>Non</td>
      <td>Oui</td>
      <td><p><strong>Pour prévisualiser une ressource dans une visionneuse particulière</strong></p>
      <ul>
      <li>En haut à gauche de la page, cliquez sur l’icône pour afficher la liste déroulante. Sélectionnez <strong>Visionneuses</strong> dans la liste, puis sélectionnez une visionneuse à appliquer à la ressource.</li>
      </ul> <p>Utilisez les icônes <strong>+</strong> et <strong>– </strong> pour augmenter ou réduire le zoom de l’image sélectionnée. Sélectionnez <strong>Réinitialiser</strong> si vous souhaitez rétablir l’image sur le zoom d’origine.<br /> Si vous utilisez un écran tactile, appuyez deux fois sur l’image pour effectuer un zoom avant par étapes. Lorsque vous atteignez le zoom maximal, appuyez à nouveau deux fois sur l’image pour réinitialiser l’état du zoom. Faites glisser sur l’image pour effectuer un panoramique.</p> </td>
      </tr>
      <tr>
      <td>Visionneuse de supports variés</td>
      <td>Non</td>
      <td>Oui</td>
      <td><p><strong>Pour prévisualiser une ressource dans une visionneuse particulière</strong></p>
      <ul>
      <li>En haut à gauche de la page, cliquez sur l’icône pour afficher la liste déroulante. Sélectionnez <strong>Visionneuses</strong> dans la liste, puis sélectionnez une visionneuse à appliquer à la ressource.</li>
      </ul> <p>Utilisez les icônes <strong>+</strong> et <strong>– </strong> pour augmenter ou réduire le zoom de l’image sélectionnée. Sélectionnez <strong>Réinitialiser</strong> si vous souhaitez rétablir l’image sur le zoom d’origine.<br /> Si vous utilisez un écran tactile, appuyez deux fois sur l’image pour effectuer un zoom avant par étapes. Lorsque vous atteignez le zoom maximal, appuyez à nouveau deux fois sur l’image pour réinitialiser l’état du zoom. Faites glisser sur l’image pour effectuer un panoramique.</p> </td>
      </tr>
      <tr>
      <td>Ensemble de carrousel</td>
      <td>Non</td>
      <td>Oui</td>
      <td><strong>Pour prévisualiser une ressource dans une visionneuse particulière</strong>
      <ul>
      <li>En haut à gauche de la page, cliquez sur l’icône pour afficher la liste déroulante. Sélectionnez une visionneuse à appliquer à la ressource.</li>
      </ul> </td>
      </tr>
      <tr>
      <td>Vidéo à 360°<br /> </td>
      <td>Oui</td>
      <td>Oui</td>
      <td><p><strong>Pour prévisualiser une ressource dans un rendu particulier</strong></p>
      <ul>
      <li>En haut à gauche de la page, sélectionnez l’icône pour afficher la liste déroulante. Sélectionnez <strong>Rendus</strong>, puis sélectionnez le rendu dont vous souhaitez afficher l’aperçu.</li>
      </ul> <p><strong>Pour prévisualiser une ressource dans une visionneuse particulière</strong></p>
      <ul>
      <li>En haut à gauche de la page, sélectionnez l’icône pour afficher la liste déroulante. Sélectionnez <strong>Visionneuses</strong>, puis sélectionnez une visionneuse à appliquer à la ressource.</li>
      </ul> <p>Utilisez les icônes <strong>+</strong> et <strong>– </strong> pour augmenter ou réduire le zoom de l’image sélectionnée. Sélectionnez <strong>Réinitialiser</strong> si vous souhaitez rétablir l’image sur le zoom d’origine.<br /> Si vous utilisez un écran tactile, appuyez deux fois sur l’image pour effectuer un zoom avant par étapes. Lorsque vous atteignez le zoom maximal, appuyez à nouveau deux fois sur l’image pour réinitialiser l’état du zoom. Faites glisser sur l’image pour effectuer un panoramique.</p> </td>
      </tr>
    </tbody>
    </table>

## Aperçu des ressources à l’aide du clavier {#keyboard-navigation-asset-preview}

1. Dans l’interface utilisateur d’Assets, accédez à un dossier contenant une ressource à prévisualiser.

1. Dans le dossier, appuyez sur la touche `<Tab>` ou les touches fléchées du clavier pour sélectionner la ressource.

1. Appuyez sur `<Enter>` pour que vous puissiez ouvrir la ressource sélectionnée en mode Aperçu.

1. Procédez de l’une des manières suivantes :

   * Pour effectuer un zoom avant, appuyez sur `<Tab>` pour déplacer la mise au point sur l’icône de zoom avant (+), puis appuyez une ou plusieurs fois sur `<Enter>` pour exécuter un zoom avant incrémentiel.
   * Pour effectuer un zoom arrière, appuyez sur `<Tab>` pour déplacer la sélection vers l’icône de zoom arrière (-), puis appuyez sur `<Enter>` une ou plusieurs fois pour effectuer un zoom arrière incrémentiel.
   * Pour déplacer la vue d’une ressource *zoomée* horizontalement ou verticalement, appuyez sur les touches fléchées correspondantes.
   * Appuyez sur `<Shift>` + `<Tab>` afin que vous puissiez réinitialiser l’affichage et réactiver la mise au point sur la ressource.
