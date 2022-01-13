---
title: Configuration des paramètres généraux de Dynamic Media
description: Découvrez comment gérer les paramètres généraux dans Dynamic Media. Vous pouvez définir ici le nom de votre serveur de publication et le nom du serveur d’origine, puis définir une option de remplacement d’image. Il existe également des options de transfert par défaut pour le masquage flou des images, ainsi que des options de transfert pour le traitement des fichiers PostScript, Adobe Photoshop, PDF et Adobe Illustrator.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User, Admin
mini-toc-levels: 4
exl-id: 55cc7c57-87a0-4bfb-b226-36d01d36849a
source-git-commit: 9c548dbc0157607adda5ed76cab8ef970588e1e9
workflow-type: tm+mt
source-wordcount: '2498'
ht-degree: 34%

---

# Configuration des paramètres généraux de Dynamic Media

Configuration **[!UICONTROL Paramètres généraux de Dynamic Media]** est disponible uniquement si :

* Vous exécutez Dynamic Media en mode Scene7. Voir [Activation de Dynamic Media en mode Scene7](/help/assets/config-dms7.md#enabling-dynamic-media-in-scene-mode).
* Vous avez une *existant* **[!UICONTROL Configuration Dynamic Media]** (dans **[!UICONTROL Cloud Services]**) dans Adobe Experience Manager 6.5.11 ou version ultérieure. Voir [Création d’une configuration Dynamic Media dans les Cloud Services](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services).
* Vous êtes un administrateur système Experience Manager disposant de droits d’administrateur.

Les paramètres généraux de Dynamic Media sont destinés aux développeurs et programmeurs chevronnés de sites web. Adobe Dynamic Media recommande que les utilisateurs qui modifient ces paramètres de publication connaissent bien Dynamic Media sur Adobe Experience Manager et la technologie d’imagerie de base.

Lors de la création du compte, Adobe Dynamic Media fournit automatiquement les serveurs attribués à votre entreprise. Ces serveurs sont utilisés pour créer des chaînes URL pour votre site web et vos applications. Ces appels d’URL sont spécifiques à votre compte.

La page Configuration de la publication Dynamic Media établit les paramètres par défaut qui déterminent la manière dont les ressources sont diffusées des serveurs Dynamic Media d’Adobe vers les sites web ou les applications. Si aucun paramètre n’est spécifié, le serveur Dynamic Media Adobe diffuse une ressource selon un paramètre par défaut qui a été configuré sur la page Configuration de la publication Dynamic Media .

Voir aussi [Facultatif - Configuration et configuration des paramètres du mode Dynamic Media - Scene7](/help/assets/config-dms7.md#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings) pour d’autres tâches de configuration facultatives.

>[!NOTE]
>
>Mise à niveau de Dynamic Media Classic vers Dynamic Media sur Adobe Experience Manager ? la page Paramètres généraux ; [Configuration de la publication](/help/assets/dm-publish-settings.md) dans Dynamic Media sont prérenseignées avec les valeurs issues de votre compte Dynamic Media Classic. Les exceptions sont toutes les valeurs répertoriées sous la variable **[!UICONTROL Options de chargement par défaut]** de la page Paramètres généraux. Ces valeurs sont déjà en Experience Manager. Ainsi, les modifications que vous apportez sous **[!UICONTROL Options de chargement par défaut]**, sur l’un des cinq onglets, par le biais de l’interface utilisateur du Experience Manager, sont reflétés dans Dynamic Media et non dans Dynamic Media Classic. Tous les autres paramètres et valeurs de la page Paramètres généraux et de la variable [Configuration de la publication](/help/assets/dm-publish-settings.md) sont conservées entre Dynamic Media Classic et Dynamic Media sur Experience Manager.

**Pour configurer les paramètres généraux de Dynamic Media :**

1. En mode Création Experience Manager , sélectionnez le logo du Experience Manager pour accéder à la console de navigation globale.
1. Dans le rail de gauche, sélectionnez l’icône Outils, puis accédez à **[!UICONTROL Ressources]** > **[!UICONTROL Paramètres généraux de Dynamic Media]**.
1. Dans la page Serveur , définissez **[!UICONTROL Nom du serveur publié]** et **[!UICONTROL Nom du serveur d’origine]**, puis utilisez les cinq onglets pour configurer les options de chargement par défaut pour l’édition d’images et pour les fichiers Postscript, Photoshop, PDF et Illustrator.

   * [Serveur](#server-general-setting)
   * [Charger dans l’application](#upload-to-application)
   * [Modification d’images](#image-editing-tab) tab
   * [PostScript](#postscript-tab) tab
   * [Photoshop](#photoshop-tab) tab
   * [PDF](#pdf-tab) tab
   * [Illustrator](#illustrator-tab) tab

   ![Page Paramètres généraux de Dynamic Media](/help/assets/assets-dm/dm-general-settings.png)
   *de la page Paramètres généraux de Dynamic Media, avec la fonction **[!UICONTROL Modification d’images]**onglet sélectionné.*<br><br>

1. Lorsque vous avez terminé, près du coin supérieur droit de la page, sélectionnez **[!UICONTROL Enregistrer]**.

## Serveur {#server-general-setting}

Lors de la création du compte, Adobe Dynamic Media fournit automatiquement les serveurs attribués à votre entreprise. Ces serveurs sont utilisés pour créer des chaînes URL pour votre site web et vos applications. Ces appels d’URL sont spécifiques à votre compte.

| Option | Description |
| --- | --- |
| **[!UICONTROL Nom du serveur publié]** | Requis.<br>Le nom doit utiliser `https://` dans le chemin.<br>Ce serveur est le serveur CDN actif (Content Delivery Network) utilisé dans tous les appels d’URL générés par le système et spécifiques à votre compte. Ne modifiez pas le nom de ce serveur à moins que le support technique d’Adobe vous le demande. |
| **[!UICONTROL Nom du serveur d’origine]** | Requis.<br>Ce serveur n’est utilisé que pour les tests d’assurance qualité. Ne modifiez pas le nom de ce serveur à moins que le support technique par Adobe ne vous le demande. |

## Charger dans l’application {#upload-to-application}

* **[!UICONTROL Remplacer les images]**

   Adobe Dynamic Media ne permet pas que deux fichiers portent le même nom. L’identifiant Dynamic Media d’Adobe de chaque élément (le nom de l’image sans l’extension de nom de fichier) doit être unique. En raison de cette règle, **[!UICONTROL Téléchargement vers l’application]** a un remplacement. L’effet exact de cette option dépend de l’option Écraser les images que vous avez sélectionnée. Ces options indiquent comment les images de remplacement sont téléchargées : s’ils remplacent les images d’origine ou deviennent des doublons. Les images en double sont renommées avec une `-1`. Par exemple : `chair.tif` est renommé `chair-1.tif`. Ces options affectent les images téléchargées dans un dossier différent de celui de l’image d’origine ou les images dont l’extension est différente de celle du fichier d’origine, comme JPG, TIF ou PNG.

   >[!NOTE]
   >
   >Pour maintenir la cohérence avec Experience Manager, sélectionnez l’option Écraser les images . **[!UICONTROL Remplacer dans le dossier actuel, même nom/même extension de base]**.

   | Option Remplacer les images | Description |
   | --- | --- |
   | **[!UICONTROL Remplacer dans le dossier actuel, même nom/extension de base]** | *Par défaut* pour les nouveaux comptes Dynamic Media uniquement.<br>Cette option est la règle la plus stricte pour le remplacement. Elle implique que vous chargiez l’image de remplacement dans le même dossier que l’original, et qu’elle ait la même extension que le fichier d’origine. Si ces conditions ne sont pas remplies, un doublon est créé.<br>*Pour maintenir la cohérence avec Experience Manager, sélectionnez cette option.*. |
   | **[!UICONTROL Remplacer dans le dossier actuel, même nom de base, indépendamment de l’extension]** | Nécessite de charger l’image de remplacement dans le même dossier que l’image d’origine, mais l’extension du nom de fichier peut être différente de celle de l’image d’origine. Par exemple, chaise.tif remplace chaise.jpg. |
   | **[!UICONTROL Remplacer dans un dossier, même nom/extension de ressource de base]** | Nécessite que l’image de remplacement ait la même extension que l’image d’origine (par exemple, chaise.jpg doit remplacer chaise.jpg, et non chaise.tif). Vous pouvez néanmoins télécharger l’image de remplacement dans un dossier différent de celui de l’image d’origine. L’image mise à jour se trouve dans le nouveau dossier ; le fichier d’origine n’est plus disponible à l’emplacement d’origine.. |
   | **[!UICONTROL Écraser dans n’importe quel dossier, même nom de ressource de base, quelle que soit l’extension]** | Cette option est la règle de remplacement la plus inclusive. Elle vous permet de charger une image de remplacement dans un dossier autre que celui de l’image d’origine, de charger un fichier dont l’extension est différente de celle du fichier d’origine et de remplacer le fichier d’origine. Si le fichier d’origine se trouve dans un dossier différent, l’image de remplacement est enregistrée dans le nouveau dossier où elle a été chargée. |

* **[!UICONTROL Conserver le recadrage]**

   Contrôle la conservation de toute définition de recadrage manuel existante.

   Voir aussi `preserveCrop` in [UploadPostJob](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-upload-post-job.html) et [ReprocessAssetsJob](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-reprocess-assets-job.html), dans le Guide de référence des visionneuses Dynamic Media.

## Options de téléchargement par défaut {#default-upload-options}

### Onglet Edition d’images {#image-editing-tab}

Ce filtre permet d’affiner l’effet d’un filtre d’accentuation sur l’image finale à résolution réduite. Il permet de contrôler l’intensité de l’effet, le rayon de l’effet (mesuré en pixels) et un seuil de contraste qui est ignoré.

L’effet Masquage flou utilise les mêmes options que le filtre Masquage flou de Photoshop. Contrairement à ce que suggère le nom, le masquage flou est un filtre d’accentuation.

| Options d’accentuation | Description |
| --- | --- |
| **[!UICONTROL Quantité]** | Requis.<br>Contrôle le degré de contraste appliqué aux pixels de contour.<br>Considérez cela comme l’intensité de l’effet. La principale différence entre les valeurs de quantité du masquage flou dans Adobe Dynamic Media et les valeurs de quantité dans Adobe Photoshop est que Photoshop a une plage de valeurs comprise entre 1 % et 500 %. En revanche, dans Adobe Dynamic Media, la plage de valeurs est `0.0` to `5.0`. Une valeur de 5,0 dans Adobe Dynamic Media équivaut environ à 500 % dans Photoshop ; une valeur de 0,9 équivaut à 90 %, etc. |
| **[!UICONTROL Rayon]** | Requis.<br>Contrôle le rayon de l’effet.<br>La plage de valeurs est `0` to `250`. L’effet est exécuté sur tous les pixels d’une image et s’étend depuis tous les pixels dans toutes les directions. Le rayon est mesuré en pixels. Par exemple, pour obtenir un effet d’accentuation similaire pour une image de 2 000 x 2 000 pixels et une image de 500 x 500 pixels, définissez un rayon de deux pixels sur l’image de 2 000 x 2 000 pixels. Définissez ensuite une valeur de rayon d’un pixel sur l’image de 500 x 500 pixels. Utilisez une valeur plus élevée pour une image avec plus de pixels. |
| **[!UICONTROL Seuil]** | Requis.<br>Le seuil est une plage de contraste qui est ignorée lorsque le filtre de masquage flou est appliqué. Cet effet est important, de sorte qu’aucun &quot;bruit&quot; n’est introduit dans une image lorsque ce filtre est utilisé. La plage de valeurs est `0` - `255`: nombre d’étapes de luminosité d’une image en niveaux de gris. `0` = noir,  = 50 % gris et  = blanc.`128``255`<br>Une valeur seuil de `12` ignore les légères variations de la luminosité de la peau pour éviter d’ajouter du bruit, tout en ajoutant un contraste sur les bords dans les zones contrastées telles que l’endroit où les cils rencontrent la peau.<br>Si vous disposez d’une photo du visage d’une personne, le masquage flou affecte les parties contrastées de l’image. Par exemple, où les cils et la peau se rencontrent pour créer une zone de contraste évidente, et la peau lisse elle-même. Même la peau la plus lisse affiche des variations subtiles de ses valeurs de luminosité. Si vous n’utilisez aucune valeur de seuil, le filtre accentue ces changements subtils dans les pixels de la peau. Un effet de bruit indésirable est alors créé lorsque le contraste sur les cils est augmenté, ce qui améliore la netteté.<br>Pour éviter ce problème, utilisez une valeur de seuil qui indique au filtre d’ignorer les pixels qui ne modifient pas considérablement le contraste, comme la peau lisse.<br>Dans l’image de fermeture éclair présentée plus haut, remarquez la texture en regard des fermetures. Le bruit d’une image est exposé, car les valeurs de seuil étaient trop faibles pour supprimer le bruit. |
| **[!UICONTROL Monochrome]** | Sélectionnez cette option pour appliquer le masquage flou sur la luminosité de l’image (intensité).<br>Désélectionnez-la pour appliquer le masquage flou séparément sur chaque composante de couleur. |

Voir aussi [Accentuer les images dans Adobe Dynamic Media et sur le serveur d’images](/help/assets/assets/sharpening_images.pdf).

### Onglet PostScript {#postscript-tab}

Vous pouvez pixelliser des fichiers Adobe PostScript®, conserver des arrière-plans transparents, choisir une résolution et choisir un espace colorimétrique.

Vous pouvez utiliser des fichiers Adobe PostScript® (EPS) dans Adobe Dynamic Media. Adobe Dynamic Media propose des commandes pour configurer ces fichiers au fur et à mesure de leur chargement.

Lorsque vous chargez des fichiers image PostScript (EPS), vous pouvez les mettre en forme de différentes manières. Vous pouvez pixelliser les fichiers, conserver l’arrière-plan transparent, choisir une résolution et sélectionner un espace colorimétrique.

| Option PostScript | Description |
| --- | --- |
| **[!UICONTROL Traitement]** | Sélectionnez Pixelliser pour convertir les graphiques vectoriels du fichier au format bitmap. |
| **[!UICONTROL Conserver l’arrière-plan transparent dans le rendu des images]** | Permet de conserver la transparence en arrière-plan du fichier. |
| **[!UICONTROL Résolution (pixel/pouce)]** | Détermine le paramètre de résolution. Ce paramètre détermine le nombre de pixels affichés par pouce dans le fichier. |
| **[!UICONTROL Espace colorimétrique]** | ・ **[!UICONTROL Détecter automatiquement]** - Conserve l’espace colorimétrique du fichier.<br>・ **[!UICONTROL Forcer comme RGB]** : convertit l’espace colorimétrique du RGB.<br>・ **[!UICONTROL Forcer comme CMJN]** : convertit l’espace colorimétrique CMJN.<br>・ **[!UICONTROL Forcer comme Niveaux de gris]** - Applique l’espace colorimétrique Niveaux de gris. |

### Onglet Photoshop {#photoshop-tab}

Vous pouvez créer des modèles à partir de fichiers Adobe® Photoshop®, conserver les calques, définir la méthode d’attribution des noms de calque, extraire du texte et indiquer le mode d’ancrage des images dans les modèles.

| Option Photoshop | Description |
| --- | --- |
| **[!UICONTROL Conserver les calques]** | Pixellise les calques du fichier PSD, le cas échéant, dans des fichiers individuels. Les calques de ces fichiers restent associés au fichier PSD. Vous pouvez les afficher en ouvrant le fichier de PSD dans la vue Détails et en sélectionnant le panneau Calque. Voir Affichage et modification de calques dans un fichier de PSD. |
| **[!UICONTROL Créer un modèle]** | Crée un modèle à partir des calques du fichier PSD. |
| **[!UICONTROL Extraire le texte]** | Extrait le texte pour permettre aux utilisateurs de rechercher une chaîne de caractères dans une visionneuse. |
| **[!UICONTROL Étendre les calques à la taille du fond]** | Étend la taille des calques d’image pixellisés à celle du calque en arrière-plan. |
| **[!UICONTROL Affectation d’un nom au calque]** | Étend la taille des calques d’image pixellisés à celle du calque en arrière-plan.<br>・ **[!UICONTROL Nom du calque]** - Nomme les images selon leurs noms de calque dans le fichier de PSD. Par exemple, un calque nommé Étiquette de prix dans le fichier PSD d’origine devient une image nommée Étiquette de prix. Cependant, si les noms de calque dans le fichier de PSD sont des noms de calque Photoshop par défaut (Arrière-plan, Calque 1, Calque 2, etc.), les images sont nommées d’après leur numéro de calque dans le fichier de PSD. <br>・ **[!UICONTROL Photoshop et numéro de calque]** - Nomme les images en fonction de leur numéro de calque dans le fichier de PSD, en ignorant les noms de calque d’origine. Le nom des images est composé du nom de fichier Photoshop et d’un numéro de calque. Par exemple, le deuxième calque d’un fichier appelé `Spring Ad.psd` est nommé `Spring Ad_2` même s’il ne portait pas de nom par défaut dans Photoshop.<br>・ **[!UICONTROL Photoshop et nom du calque]** - Nomme les images après le fichier de PSD suivi du nom ou du numéro de calque. Le numéro de calque est utilisé si le nom du calque dans le fichier PSD est un nom de calque Photoshop par défaut. Par exemple, un calque nommé `Price Tag` dans un fichier de PSD nommé `SpringAd` est nommé `Spring Ad_Price Tag`. Un calque portant le nom par défaut Calque 2 est appelé `Spring Ad_2`. |
| **[!UICONTROL Ancre]** | Indiquez le mode d’ancrage des images dans les modèles qui sont générés à partir de la composition superposée produite à partir du fichier PSD. Par défaut, l’ancrage est au centre. Un ancrage au centre permet aux images de remplacement de remplir de manière optimale le même espace, quelles que soient les proportions de l’image de remplacement. Les images qui remplacent cette image et qui présentent un aspect différent occupent le même espace lorsque le modèle est référencé et le paramètre de substitution utilisé. Changez de paramètre si votre application exige que les images de remplacement occupent l’espace alloué dans le modèle. |

### Onglet PDF {#pdf-tab}

Vous pouvez choisir de pixelliser les fichiers, d’extraire des mots de recherche et des liens, de définir la résolution et de choisir un espace colorimétrique.

| Option PDF | Description |
| --- | --- |
| **[!UICONTROL Traitement]** | ・ **[!UICONTROL Aucun]** - Aucun traitement du PDF n’est effectué.<br>・ **[!UICONTROL Miniature]** - Pixellise chaque page du fichier du PDF et la convertit en image miniature.<br> ・ **[!UICONTROL Pixelliser]** - Pixellise les pages du fichier du PDF et convertit les graphiques vectoriels en images bitmap. Pour créer un catalogue électronique, sélectionnez cette option. |
| **[!UICONTROL Extraire]** | ・ **[!UICONTROL Aucun]** - Aucun mot de recherche ou lien n’est extrait du PDF.<br>・ **[!UICONTROL Mots de recherche]** - Extrait les mots-clés de recherche du fichier du PDF afin que le fichier puisse être recherché par mot-clé dans une visionneuse de catalogue électronique.<br>・ **[!UICONTROL Liens]** - Extrait les liens des fichiers du PDF et les convertit en zones cliquables utilisées dans une visionneuse de catalogue électronique.<br>・ **[!UICONTROL Mots et liens de recherche]** - Extrait les mots de recherche et les liens à utiliser dans une visionneuse de catalogue électronique. |
| **[!UICONTROL Résolution (pixel/pouce)]** | Détermine le paramètre de résolution. Ce paramètre définit le nombre de pixels affichés par pouce dans le fichier PDF. La valeur par défaut est de 150. |
| **[!UICONTROL Espace colorimétrique]** | ・ **[!UICONTROL Détecter automatiquement]** - Conserve l’espace colorimétrique du fichier de PDF.<br>・ **[!UICONTROL Forcer comme RGB]** : convertit l’espace colorimétrique du RGB.<br>・ **[!UICONTROL Forcer comme CMJN]** : convertit l’espace colorimétrique CMJN.<br>・ **[!UICONTROL Forcer comme Niveaux de gris]** - Applique l’espace colorimétrique Niveaux de gris. |

### Onglet Illustrator {#illustrator-tab}

Vous pouvez pixelliser les fichiers Adobe Illustrator®, conserver l’arrière-plan transparent, choisir une résolution et sélectionner un espace de couleurs.

Vous pouvez utiliser des fichiers Adobe® Illustrator® (AI) dans Adobe Dynamic Media. Adobe Dynamic Media propose des commandes pour configurer ces fichiers au fur et à mesure de leur chargement.

Lorsque vous chargez des fichiers image Illustrator (AI), vous pouvez les mettre en forme de différentes manières. Vous pouvez pixelliser les fichiers, conserver l’arrière-plan transparent, choisir une résolution et sélectionner un espace colorimétrique. Les options de formatage des fichiers PostScript et Illustrator sont disponibles dans l’écran de téléchargement sous Options PostScript et Options Illustrator dans la zone Télécharger les options de la tâche.


| Option Illustrator | Description |
| --- | --- |
| **[!UICONTROL Traitement]** | Sélectionnez Pixelliser pour convertir les graphiques vectoriels du fichier au format bitmap. |
| **[!UICONTROL Conserver l’arrière-plan transparent dans le rendu des images]** | Permet de conserver la transparence en arrière-plan du fichier. |
| **[!UICONTROL Résolution (pixel/pouce)]** | Détermine le paramètre de résolution. Ce paramètre détermine le nombre de pixels affichés par pouce dans le fichier. |
| **[!UICONTROL Espace colorimétrique]** | ・ **[!UICONTROL Détecter automatiquement]** - Conserve l’espace colorimétrique du fichier.<br>・ **[!UICONTROL Forcer comme RGB]** : convertit l’espace colorimétrique du RGB.<br>・ **[!UICONTROL Forcer comme CMJN]** : convertit l’espace colorimétrique CMJN.<br>・ **[!UICONTROL Forcer comme Niveaux de gris]** - Applique l’espace colorimétrique Niveaux de gris. |
