---
title: Configurer les paramètres généraux de Dynamic Media
description: Découvrez comment gérer les paramètres généraux dans Dynamic Media. Vous pouvez définir ici le nom de votre serveur de publication et le nom du serveur d’origine, puis définir une option de remplacement d’image. Il existe également des options de chargement par défaut pour le masquage des images, ainsi que des options de chargement pour le traitement des fichiers PostScript, Adobe Photoshop, PDF et Adobe Illustrator.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User, Admin
mini-toc-levels: 4
exl-id: 55cc7c57-87a0-4bfb-b226-36d01d36849a
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2506'
ht-degree: 100%

---

# Configurer les paramètres généraux de Dynamic Media

La configuration des **[!UICONTROL paramètres généraux de Dynamic Media]** est disponible uniquement si :

* Vous exécutez Dynamic Media en mode Scene7. Consultez [Activation de Dynamic Media en mode Scene7](/help/assets/config-dms7.md#enabling-dynamic-media-in-scene-mode).
* Vous disposez d’une **[!UICONTROL Configuration Dynamic Media]** *existante* (dans **[!UICONTROL Services cloud]**) dans Adobe Experience Manager, version 6.5.11 ou supérieure. Voir [Création d’une configuration Dynamic Media dans Services cloud](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services).
* Vous êtes un administrateur système d’Experience Manager disposant de droits d’administrateur.

Les paramètres généraux de Dynamic Media sont destinés aux développeurs et programmeurs chevronnés de sites Web. Adobe Dynamic Media recommande aux utilisateurs qui modifient ces paramètres de publication de se familiariser avec Dynamic Media sur Adobe Experience Manager et avec la technologie d’imagerie de base.

Lors de la création du compte, Adobe Dynamic Media fournit automatiquement les serveurs affectés à votre entreprise. Ces serveurs sont utilisés pour construire des chaînes d’URL pour votre site Web et vos applications. Ces appels d’URL sont spécifiques à votre compte.

La page Configuration de la publication Dynamic Media établit les paramètres par défaut qui déterminent la manière dont les ressources sont diffusées des serveurs Dynamic Media d’Adobe vers les sites web ou les applications. Si aucun paramètre n’est spécifié, le serveur Dynamic Media Adobe diffuse une ressource selon un paramètre par défaut configuré sur la page Configuration de la publication Dynamic Media.

Consultez également [Facultatif - Installation et configuration de Dynamic Media - Paramètres du mode Scene7](/help/assets/config-dms7.md#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings) pour plus de tâches de configuration facultatives.

>[!NOTE]
>
>Prêt à passer de Dynamic Media Classic vers Dynamic Media sur Adobe Experience Manager ? Les pages Paramètres généraux et [Configuration de la publication](/help/assets/dm-publish-settings.md) dans Dynamic Media sont préremplies avec les valeurs de votre compte Dynamic Media Classic. Les exceptions sont toutes les valeurs figurant dans la zone **[!UICONTROL Options de chargement par défaut]** de la page Paramètres généraux. Ces valeurs se trouvent déjà dans Experience Manager. Ainsi, toute modification apportée aux **[!UICONTROL Options de chargement par défaut]**, dans l’un des cinq onglets, par le biais de l’interface utilisateur Experience Manager, est répercutée dans Dynamic Media et non dans Dynamic Media Classic. Tous les autres paramètres et valeurs de la page Paramètres généraux et de la page [Configuration de la publication](/help/assets/dm-publish-settings.md) sont conservés entre Dynamic Media Classic et Dynamic Media dans Experience Manager.

**Pour configurer les paramètres généraux de Dynamic Media :**

1. En mode création d’Experience Manager, sélectionnez le logo d’Experience Manager pour accéder à la console de navigation globale.
1. Dans la barre de gauche, sélectionnez l’icône Outils, puis accédez à **[!UICONTROL Ressources]** > **[!UICONTROL Paramètres généraux de Dynamic Media]**.
1. Dans la page Serveur, définissez votre **[!UICONTROL Nom de serveur publié]** et votre **[!UICONTROL Nom de serveur d’origine]**, puis utilisez les cinq onglets pour configurer les options de chargement par défaut pour l’édition d’images et pour les fichiers Postscript, Photoshop, PDF et Illustrator.

   * [Serveur](#server-general-setting)
   * [Charger dans l’application](#upload-to-application)
   * Onglet [Modification d’images](#image-editing-tab)
   * Onglet [PostScript](#postscript-tab)
   * Onglet [Photoshop](#photoshop-tab)
   * Onglet [PDF](#pdf-tab)
   * Onglet [Illustrator](#illustrator-tab)

   ![Page des paramètres généraux de Dynamic Media](/help/assets/assets-dm/dm-general-settings.png)
   *Page des paramètres généraux de Dynamic Media, avec l’onglet **[!UICONTROL Modification d’images]**sélectionné.*<br><br>

1. Lorsque vous avez terminé, près du coin supérieur droit de la page, sélectionnez **[!UICONTROL Enregistrer]**.

## Serveur {#server-general-setting}

Lors de la création du compte, Adobe Dynamic Media fournit automatiquement les serveurs affectés à votre entreprise. Ces serveurs sont utilisés pour construire des chaînes d’URL pour votre site Web et vos applications. Ces appels d’URL sont spécifiques à votre compte.

| Option | Description |
| --- | --- |
| **[!UICONTROL Nom du serveur publié]** | Requis.<br>Le nom doit utiliser `https://` dans le chemin.<br>Ce serveur est le serveur dynamique du réseau CDN (Content Delivery Network) utilisé pour tous les appels d’URL générés par le système et spécifiques à votre compte. Ne modifiez pas le nom de ce serveur à moins que le support technique d’Adobe ne vous le demande. |
| **[!UICONTROL Nom du serveur original]** | Requis.<br>Ce serveur n’est utilisé que pour les tests d’assurance qualité. Ne modifiez pas le nom de ce serveur à moins que le support technique d’Adobe ne vous le demande. |

## Charger dans l’application {#upload-to-application}

* **[!UICONTROL Remplacer les images]**

  Adobe Dynamic Media ne permet pas à deux fichiers d’avoir le même nom. L’identifiant Dynamic Media d’Adobe de chaque élément (le nom de l’image sans l’extension de nom de fichier) doit être unique. En raison de cette règle, **[!UICONTROL Charger dans l’application]** a un remplacement. L’effet exact de cette option dépend de l’option Remplacer les images que vous avez sélectionnée. Ces options spécifient la manière dont les images de remplacement sont chargées : elles peuvent remplacer les images originales ou devenir des images en double. Les images en double sont renommées avec une `-1`. Par exemple : `chair.tif` est renommé `chair-1.tif`. Ces options affectent les images chargées dans un dossier différent de celui de l’original ou les images dont l’extension de nom de fichier est différente de celle de l’original (telle que JPG, TIF ou PNG).

  >[!NOTE]
  >
  >Pour maintenir la cohérence avec Experience Manager, sélectionnez l’option Remplacer les images. **[!UICONTROL Remplacer dans le dossier actuel, même nom/extension de base]**.

  | Option Remplacer les images | Description |
  | --- | --- |
  | **[!UICONTROL Remplacer dans le dossier actuel, même nom/extension de base]** | *Par défaut* pour les nouveaux comptes Dynamic Media uniquement.<br>Cette option est la règle la plus stricte en matière de remplacement. Elle implique que vous chargiez l’image de remplacement dans le même dossier que l’original, et qu’elle ait la même extension que le fichier d’origine. Si ces conditions ne sont pas remplies, un doublon est créé.<br>*Pour maintenir la cohérence avec Experience Manager, sélectionnez cette option.*. |
  | **[!UICONTROL Remplacer dans le dossier actuel, même nom de base, indépendamment de l’extension]** | Nécessite que vous chargiez l’image de remplacement dans le même dossier que l’original, mais l’extension du nom de fichier peut être différente de celle de l’original. Par exemple, chaise.tif remplace chaise.jpg. |
  | **[!UICONTROL Remplacer dans un dossier, même nom/extension de ressource de base]** | Nécessite que l’image de remplacement ait la même extension que l’image originale (par exemple, chaise.jpg doit remplacer chaise.jpg, et non chaise.tif). Vous pouvez toutefois charger l’image de remplacement dans un dossier différent de celui de l’image d’origine. L’image mise à jour se trouve dans le nouveau dossier. Le fichier n’est plus accessible à son emplacement d’origine. |
  | **[!UICONTROL Remplacer dans un dossier, même nom de ressource de base, quelle que soit l’extension]** | Cette option est la règle de remplacement la plus concrète. Elle vous permet de charger une image de remplacement dans un dossier autre que celui de l’image d’origine, de charger un fichier avec une extension de nom de fichier différente et de remplacer le fichier original. Si le fichier d’origine se trouve dans un dossier différent, l’image de remplacement est enregistrée dans le nouveau dossier où elle a été chargée. |

* **[!UICONTROL Conserver le recadrage]**

  Contrôle la conservation de toute définition de recadrage manuel existante.

  Voir aussi `preserveCrop` dans [UploadPostJob](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-upload-post-job.html?lang=fr) et [ReprocessAssetsJob](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-reprocess-assets-job.html?lang=fr), tous deux dans le Guide de référence des visionneuses Dynamic Media.

## Options de chargement par défaut {#default-upload-options}

### Onglet Edition d’images {#image-editing-tab}

Ce filtre permet d’affiner l’effet d’un filtre d’accentuation sur l’image finale à résolution réduite. Il permet de contrôler l’intensité de l’effet, le rayon de l’effet (mesuré en pixels) et un seuil de contraste qui est ignoré.

L’effet d’accentuation utilise les mêmes options que le filtre d’accentuation de Photoshop. Contrairement à ce que suggère son nom, l’accentuation est un filtre d’accentuation.

| Options d’accentuation | Description |
| --- | --- |
| **[!UICONTROL Quantité]** | Requis.<br>Contrôle l’intensité du contraste appliqué aux pixels de contour.<br>Considérez cela comme l’intensité de l’effet. La principale différence entre les valeurs de quantité de l’accentuation dans Adobe Dynamic Media et les valeurs de quantité dans Adobe Photoshop est que Photoshop a une plage de valeurs comprise entre 1 % et 500 %. En revanche, dans Adobe Dynamic Media, la plage de valeurs est comprise entre `0.0` et `5.0`. Une valeur de 5,0 dans Adobe Dynamic Media équivaut environ à 500 % dans Photoshop ; une valeur de 0,9 équivaut à 90 %, et ainsi de suite. |
| **[!UICONTROL Rayon]** | Requis.<br>Contrôle le rayon de l’effet.<br>La plage de valeurs est comprise entre `0` et `250`. L’effet est exécuté sur tous les pixels d’une image et s’étend de tous les pixels dans toutes les directions. Le rayon est mesuré en pixels. Par exemple, pour obtenir un effet d’accentuation similaire pour une image de 2 000 x 2 000 pixels et une image de 500 x 500 pixels, définissez un rayon de deux pixels sur l’image de 2 000 x 2 000 pixels. Définissez ensuite une valeur de rayon d’un pixel sur l’image de 500 x 500 pixels. Utilisez une valeur plus élevée pour une image avec plus de pixels. |
| **[!UICONTROL Seuil]** | Requis.<br>Le seuil est une plage de contraste qui est ignorée lorsque le filtre d’accentuation est appliqué. Cet effet est important pour qu’aucun « bruit » ne soit introduit dans une image lorsque ce filtre est utilisé. La plage de valeurs est comprise entre `0` et `255`, ce qui correspond au nombre d’étapes de luminosité d’une image en niveaux de gris. `0`= noir, `128`= 50 % gris et `255`=blanc.<br>Une valeur de seuil de `12` ignore les légères variations de luminosité de la peau, afin de ne pas ajouter de bruit, mais ajoute un contraste sur les bords dans les zones contrastées, comme la zone où les cils rencontrent la peau.<br>Si vous disposez d’une photo du visage d’une personne, l’accentuation affecte les parties contrastées de l’image. Par exemple, où les cils et la peau se rencontrent pour créer une zone de contraste évidente, et la peau lisse elle-même. Même la peau la plus lisse présente des changements subtils dans les valeurs de luminosité. Si vous n’utilisez pas de valeur de seuil, le filtre accentue ces changements subtils en pixels de peau. En retour, un effet bruyant et indésirable est créé lorsque le contraste sur les cils est augmenté, ce qui améliore la netteté.<br>Pour éviter ce problème, utilisez une valeur de seuil qui indique au filtre d’ignorer les pixels qui ne modifient pas considérablement le contraste, comme la peau lisse.<br>Dans l’image de fermeture éclair présentée plus haut, remarquez la texture en regard des fermetures. Le bruit d’une image est exposé, car les valeurs de seuil étaient trop faibles pour supprimer le bruit. |
| **[!UICONTROL Monochrome]** | Sélectionnez cette option pour appliquer l’accentuation sur la luminosité de l’image (intensité).<br>Désélectionnez-la pour appliquer l’accentuation sur chaque composante de couleur séparément. |

Voir aussi [Accentuer les images dans Adobe Dynamic Media et sur le serveur d’images](/help/assets/assets/sharpening_images.pdf).

### Onglet PostScript {#postscript-tab}

Vous pouvez pixelliser les fichiers Adobe PostScript®, conserver l’arrière-plan transparent, choisir une résolution et sélectionner un espace colorimétrique.

Vous pouvez utiliser des fichiers Adobe PostScript® (EPS) dans Adobe Dynamic Media. Adobe Dynamic Media propose des commandes pour configurer ces fichiers au fur et à mesure de leur chargement.

Lorsque vous chargez des fichiers image PostScript (EPS), vous pouvez les formater de différentes manières. Vous pouvez pixelliser les fichiers, conserver l’arrière-plan transparent, choisir une résolution et sélectionner un espace colorimétrique.

| Option PostScript | Description |
| --- | --- |
| **[!UICONTROL Traitement]** | Sélectionnez Pixelliser pour convertir les graphiques vectoriels du fichier au format bitmap. |
| **[!UICONTROL Conserver l’arrière-plan transparent dans le rendu des images]** | Permet de conserver la transparence en arrière-plan du fichier. |
| **[!UICONTROL Résolution (pixel/pouce)]** | Détermine le paramètre de résolution. Ce paramètre détermine le nombre de pixels affichés par pouce dans le fichier. |
| **[!UICONTROL Espace colorimétrique]** | • **[!UICONTROL Détection automatique]** - Conserve l’espace colorimétrique du fichier.<br>• **[!UICONTROL Forcer comme RGB]** - Convertit vers l’espace colorimétrique RGB.<br>• **[!UICONTROL Forcer comme CMJN]** - Convertit vers l’espace colorimétrique CMJN.<br>• **[!UICONTROL Forcer comme Niveaux de gris]** - Convertit vers l’espace colorimétrique Niveaux de gris. |

### Onglet Photoshop {#photoshop-tab}

Vous pouvez créer des modèles à partir de fichiers Adobe® Photoshop®, conserver les calques, définir la méthode d’attribution des noms de calque, extraire du texte et indiquer le mode d’ancrage des images dans les modèles.

| Option Photoshop | Description |
| --- | --- |
| **[!UICONTROL Conserver les calques]** | Décompose les calques du PSD, le cas échéant, en ressources individuelles. Les calques de ces fichiers restent associés au fichier PSD. Pour les afficher, ouvrez le fichier PSD dans le mode d’affichage Détail et sélectionnez le panneau Calque. Consultez la section Affichage et modification des calques dans un fichier PSD. |
| **[!UICONTROL Créer un modèle]** | Crée un modèle à partir des calques du fichier PSD. |
| **[!UICONTROL Extraire le texte]** | Extrait le texte pour permettre aux utilisateurs de rechercher une chaîne de caractères dans une visionneuse. |
| **[!UICONTROL Étendre les calques à la taille de l’arrière-plan]** | Étend la taille des calques d’image pixellisés à celle du calque en arrière-plan. |
| **[!UICONTROL Affectation d’un nom au calque]** | Étend la taille des calques d’image pixellisés à celle du calque en arrière-plan.<br>• **[!UICONTROL Nom de calque]** : les images adoptent le nom de leur calque dans le fichier PSD. Par exemple, un calque nommé Étiquette de prix dans le fichier PSD d’origine devient une image nommée Étiquette de prix. Cependant, si les calques du fichier PSD portent les noms de calques Photoshop par défaut (Arrière-plan, Calque 1, Calque 2, etc.), les images sont nommées d’après leur numéro de calque dans le fichier PSD. <br>• **[!UICONTROL Photoshop et numéro de calque]** : nomme les images d’après leur numéro de calque dans le fichier PSD, leur nom de calque d’origine étant ignoré. Le nom des images est composé du nom de fichier Photoshop et d’un numéro de calque. Par exemple, le deuxième calque d’un fichier appelé `Spring Ad.psd` est nommé `Spring Ad_2`, même s’il portait un nom personnalisé dans Photoshop.<br>• **[!UICONTROL Photoshop et nom de calque]** : nomme les images en reprenant le nom du fichier PSD, suivi du nom ou du numéro du calque. Le numéro de calque est utilisé si le nom du calque dans le fichier PSD est un nom de calque Photoshop par défaut. Par exemple, un calque nommé `Price Tag` dans un fichier PSD portant le nom `SpringAd` est nommé `Spring Ad_Price Tag`. Un calque portant le nom par défaut Calque 2 est nommé `Spring Ad_2`. |
| **[!UICONTROL Ancre]** | Indiquez le mode d’ancrage des images dans les modèles générés à partir de la composition superposée produite à partir du fichier PSD. Par défaut, l’ancrage est central. Un ancrage central permet aux images de remplacement de remplir au mieux le même espace, quel que soit le format de l’image de remplacement. Les images avec un aspect différent qui remplacent cette image, lors du référencement du modèle et de l’utilisation de la substitution des paramètres, occupent effectivement le même espace. Définissez un autre paramètre si votre application nécessite que les images de remplacement remplissent l’espace alloué dans le modèle. |

### Onglet PDF {#pdf-tab}

Vous pouvez pixelliser les fichiers, extraire des mots de recherche et des liens, définir la résolution et choisir un espace colorimétrique.

| Option PDF | Description |
| --- | --- |
| **[!UICONTROL Traitement]** | • **[!UICONTROL Aucun]** : le fichier PDF ne subit aucun traitement.<br>• **[!UICONTROL Miniature]** : pixellise chaque page du fichier PDF et la convertit en une image miniature.<br> • **[!UICONTROL Pixelliser]** : pixellise les pages du fichier PDF et convertit les graphiques vectoriels en images bitmap. Pour créer un catalogue électronique, sélectionnez cette option. |
| **[!UICONTROL Extraire]** | • **[!UICONTROL Aucun]** : aucun mot de recherche ou lien n’est extrait du fichier PDF.<br>• **[!UICONTROL Mots de recherche]** : extrait les mots de recherche du fichier PDF afin que le fichier puisse être recherché par mot-clé dans une visionneuse de catalogue électronique.<br>• **[!UICONTROL Liens]** : extrait les liens des fichiers PDF et les convertit en zones cliquables utilisées dans une visionneuse de catalogue électronique.<br>• **[!UICONTROL Mots de recherche et liens]** : extrait les mots de recherche et les liens à utiliser dans une visionneuse de catalogue électronique. |
| **[!UICONTROL Résolution (pixel/pouce)]** | Détermine le paramètre de résolution. Ce paramètre détermine le nombre de pixels affichés par pouce dans le fichier PDF. La valeur par défaut est de 150. |
| **[!UICONTROL Espace colorimétrique]** | • **[!UICONTROL Détection automatique]** - Conserve l’espace colorimétrique du fichier PDF.<br>• **[!UICONTROL Forcer comme RVB]** - Convertit vers l’espace colorimétrique RVB.<br>• **[!UICONTROL Forcer comme CMJN]** - Convertit vers l’espace colorimétrique CMJN.<br>• **[!UICONTROL Forcer comme Niveaux de gris]** - Convertit vers l’espace colorimétrique Niveaux de gris. |

### Onglet Illustrator {#illustrator-tab}

Vous pouvez pixelliser les fichiers Adobe Illustrator®, conserver l’arrière-plan transparent, choisir une résolution et sélectionner un espace colorimétrique.

Vous pouvez utiliser des fichiers Adobe® Illustrator® (AI) dans Adobe Dynamic Media. Adobe Dynamic Media propose des commandes pour configurer ces fichiers au fur et à mesure de leur chargement.

Lorsque vous chargez des fichiers image Illustrator (AI), vous pouvez les formater de différentes manières. Vous pouvez pixelliser les fichiers, conserver l’arrière-plan transparent, choisir une résolution et sélectionner un espace colorimétrique. Les options de formatage des fichiers PostScript et Illustrator sont disponibles dans l’écran de téléchargement sous Options PostScript et Options Illustrator dans la zone Télécharger les options de la tâche.


| Option Illustrator | Description |
| --- | --- |
| **[!UICONTROL Traitement]** | Sélectionnez Pixelliser pour convertir les graphiques vectoriels du fichier au format bitmap. |
| **[!UICONTROL Conserver l’arrière-plan transparent dans le rendu des images]** | Permet de conserver la transparence en arrière-plan du fichier. |
| **[!UICONTROL Résolution (pixel/pouce)]** | Détermine le paramètre de résolution. Ce paramètre détermine le nombre de pixels affichés par pouce dans le fichier. |
| **[!UICONTROL Espace colorimétrique]** | • **[!UICONTROL Détection automatique]** - Conserve l’espace colorimétrique du fichier.<br>• **[!UICONTROL Forcer comme RGB]** - Convertit vers l’espace colorimétrique RGB.<br>• **[!UICONTROL Forcer comme CMJN]** - Convertit vers l’espace colorimétrique CMJN.<br>• **[!UICONTROL Forcer comme Niveaux de gris]** - Convertit vers l’espace colorimétrique Niveaux de gris. |
