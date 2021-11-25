---
title: Configuration de la configuration de publication Dynamic Media pour Image Server
description: Découvrez comment configurer la publication dans Dynamic Media.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User, Admin
mini-toc-levels: 4
exl-id: null
source-git-commit: b7762a44d7b572d784dda2220530b21f9c46e7ab
workflow-type: tm+mt
source-wordcount: '3459'
ht-degree: 4%

---


# Configuration de la configuration de publication Dynamic Media pour Image Server

La configuration de la publication Dynamic Media n’est disponible que si :

* Vous exécutez Dynamic Media en mode Scene7. Voir [Activation de Dynamic Media en mode Scene7](/help/assets/config-dms7.md#enabling-dynamic-media-in-scene-mode).
* Vous avez une *existant* **[!UICONTROL Configuration Dynamic Media]** (dans **[!UICONTROL Cloud Services]**) dans Adobe Experience Manager 6.5.11 ou version ultérieure. Voir [Création d’une configuration Dynamic Media dans les Cloud Services](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services).
* Vous êtes un administrateur système Experience Manager disposant de droits d’administrateur.

La configuration de la publication Dynamic Media est destinée aux développeurs et programmeurs chevronnés de sites web. Adobe Dynamic Media recommande que les utilisateurs qui modifient ces paramètres de publication soient familiarisés avec Adobe Dynamic Media, les normes et conventions de protocole HTTP et la technologie d’imagerie de base.

La page Configuration de la publication Dynamic Media établit les paramètres par défaut qui déterminent la manière dont les ressources sont diffusées des serveurs Dynamic Media d’Adobe vers les sites web ou les applications. Si aucun paramètre n’est spécifié, le serveur Dynamic Media Adobe diffuse une ressource selon un paramètre par défaut qui a été configuré sur la page Configuration de la publication Dynamic Media .

Voir aussi [Facultatif - Configuration et configuration des paramètres du mode Dynamic Media - Scene7](/help/assets/config-dms7.md#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings) pour d’autres tâches de configuration facultatives.

>[!NOTE]
>
>Mise à niveau de Dynamic Media Classic vers Dynamic Media sur Adobe Experience Manager ? Le [Paramètres généraux](/help/assets/dm-general-settings.md) Les pages Page et Configuration de la publication dans Dynamic Media sont prérenseignées avec les valeurs issues de votre compte Dynamic Media Classic. Les exceptions sont toutes les valeurs répertoriées sous la variable **[!UICONTROL Options de chargement par défaut]** de la page Paramètres généraux. Ces valeurs sont déjà en Experience Manager. Ainsi, les modifications que vous apportez sous **[!UICONTROL Options de chargement par défaut]**, sur l’un des cinq onglets, par le biais de l’interface utilisateur du Experience Manager, sont reflétés dans Dynamic Media et non dans Dynamic Media Classic. Tous les autres paramètres et valeurs de la variable [Paramètres généraux](/help/assets/dm-general-settings.md) et la page Configuration de la publication sont conservées entre Dynamic Media Classic et Dynamic Media sur Experience Manager.

**Pour configurer Dynamic Media Publish Configuration Image Server :**

1. En mode Création Experience Manager , sélectionnez le logo du Experience Manager pour accéder à la console de navigation globale.
1. Dans le rail de gauche, sélectionnez l’icône Outils, puis accédez à **[!UICONTROL Ressources]** > **[!UICONTROL Configuration de la publication Dynamic Media]**.
1. Sur la page Serveur d’images, définissez le contexte de publication Image Server, puis utilisez les cinq onglets pour configurer les paramètres de publication par défaut.

   * [Serveur d’images](#image-server)
   * [Sécurité](#security-tab) tab
   * [Gestion de catalogue](#catalog-management-tab) tab
   * [Attributs de requête](#request-attributes-tab) tab
   * [Attributs de miniature courants](#common-thumbnail-attributes-tab) tab
   * [Attributs de gestion des couleurs](#color-management-attributes-tab) tab

   ![Page Configuration de la publication Dynamic Media](/help/assets/assets-dm/dm-publish-setup.png)
   *Configuration de la publication Dynamic Media, avec la page **[!UICONTROL Attributs de requête]**onglet sélectionné.*<br><br>

1. Lorsque vous avez terminé, près du coin supérieur droit de la page, sélectionnez **[!UICONTROL Enregistrer]**.

## Serveur d’images {#image-server}

La page Serveur d’images définit les paramètres par défaut de la diffusion des images à partir des serveurs d’images. Les paramètres sont disponibles dans cinq catégories.

| Contexte de publication | Description |
| --- | --- |
| Diffusion d’images | Indique le contexte des paramètres de publication. |
| Diffusion d’images test | Spécifie le contexte pour le test des paramètres de publication.<br>Pour les nouveaux comptes Dynamic Media uniquement, la valeur par défaut **[!UICONTROL Adresse du client]** est défini sur `127.0.0.1` automatiquement.<br>Voir [Test des ressources avant de les rendre publiques](#test-assets-before-making-public). |

### Onglet Sécurité {#security-tab}

**[!UICONTROL Adresse du client]** - Permet de spécifier une ou plusieurs adresses IP ou plages d’adresses. Lorsqu’elles sont spécifiées, les demandes adressées à ce catalogue d’images provenant d’un client à une adresse IP non répertoriée sont rejetées. Cette règle s’applique à la fois à la diffusion des images et aux images rendues.

### Onglet Gestion de catalogue {#catalog-management-tab}

**[!UICONTROL Chemin du fichier de définition de l’ensemble de règles]** : spécifie le fichier contenant les définitions de jeu de règles pour le catalogue d’images.

Voir aussi [RuleSetFile](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-rulesetfile.html) dans le guide de référence des visionneuses Dynamic Media.

>[!NOTE]
>
>Si votre compte Dynamic Media Classic comporte déjà un **[!UICONTROL Chemin du fichier de définition de l’ensemble de règles]** sélectionné (comme défini sous **[!UICONTROL Configuration]** > **[!UICONTROL Application]** > **[!UICONTROL Configuration de la publication]**, sous **[!UICONTROL Gestion de catalogue]** ), votre compte Dynamic Media sur Experience Manager récupère le fichier de Dynamic Media Classic. Le fichier est ensuite stocké et rendu disponible dans ce champ, lorsque vous ouvrez la variable **[!UICONTROL Configuration de la publication Dynamic Media]** pour la première fois.

### Onglet Attributs de requête {#request-attributes-tab}

Ces paramètres concernent l’aspect par défaut des images.

| Configuration | Description |
| --- | --- |
| **[!UICONTROL Limite de taille de l’image de réponse]** | Requis.<br>Pour les nouveaux comptes Dynamic Media uniquement, la taille par défaut est automatiquement définie sur Largeur : `3000` et Hauteur : `3000` pour les deux **[!UICONTROL Serveur d’images]** et **[!UICONTROL Test de la diffusion d’images]**.<br>Spécifie la largeur et la hauteur maximales de l’image de réponse renvoyée au client. Le serveur renvoie une erreur si une requête provoque une image de réponse dont la largeur, ou la hauteur, ou les deux, est supérieure à ce paramètre.<br>Voir aussi [MaxPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-maxpix.html) dans le guide de référence des visionneuses Dynamic Media. |
| **[!UICONTROL Mode d’obfuscation de demande]** | Activez cette option si vous souhaitez qu’un codage base64 soit appliqué aux requêtes valides.<br>Voir aussi [RequestObfuscation](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-requestobfuscation.html) dans le guide de référence des visionneuses Dynamic Media. |
| **[!UICONTROL Mode de verrouillage de demande]** | Activez cette option si vous souhaitez qu’un simple verrou de hachage soit inclus dans les requêtes.<br>Voir aussi [RequestLock](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-requestlock.html) dans le guide de référence des visionneuses Dynamic Media. |
| **[!UICONTROL Attributs de demande par défaut]** |  |
| **[!UICONTROL Suffixe de fichier image par défaut]** | Requis.<br>Extension de fichier de données par défaut ajoutée aux valeurs des champs Chemin du catalogue et MaskPath si le chemin n’inclut pas de suffixe de fichier.<br>Voir aussi [DefaultExt](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultext.html) dans le guide de référence des visionneuses Dynamic Media. |
| **[!UICONTROL Nom de police par défaut]** | Indique la police utilisée si aucune police n’est fournie par une requête de calque de texte. S’il est spécifié, il doit s’agir d’une valeur de nom de police valide dans la carte de police de ce catalogue d’images ou dans la carte de police du catalogue par défaut.<br>Voir aussi [DefaultFont](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultfont.html) dans le guide de référence des visionneuses Dynamic Media. |
| **[!UICONTROL Image par défaut]** | Fournit une image par défaut à renvoyer en réponse à une demande pour laquelle l’image demandée est introuvable.<br>Voir aussi [DefaultImage](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-defaultimage.html) dans le guide de référence des visionneuses Dynamic Media.<br>**REMARQUE**: Si votre compte Dynamic Media Classic comporte déjà un **[!UICONTROL Image par défaut]** sélectionné (comme défini sous **[!UICONTROL Configuration]** > **[!UICONTROL Application]** > **[!UICONTROL Configuration de la publication]**, sous **[!UICONTROL Attributs de requête par défaut]** ), votre compte Dynamic Media sur Experience Manager récupère le fichier de Dynamic Media Classic. Le fichier est ensuite stocké et rendu disponible dans ce champ lorsque vous ouvrez la **[!UICONTROL Configuration de la publication Dynamic Media]** pour la première fois. |
| **[!UICONTROL Mode d’image par défaut]** | Lorsque la zone de réglette est activée (réglette sur la droite), la variable **[!UICONTROL Image par défaut]** remplace chaque calque manquant dans l’image source par l’image par défaut et renvoie le composite comme d’habitude. Lorsque le curseur est désactivé (curseur à gauche), l’image par défaut remplace l’ensemble de l’image composite, même si l’image manquante n’est que l’un des calques.<br>Voir aussi [DefaultImageMode](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultimagemode.html) dans le guide de référence des visionneuses Dynamic Media. |
| **[!UICONTROL Taille d’affichage par défaut]** | Requis.<br>Pour les nouveaux comptes Dynamic Media uniquement, la taille d’affichage par défaut est automatiquement définie sur Largeur : `1280` et Hauteur : `1280` pour les deux **[!UICONTROL Serveur d’images]** et **[!UICONTROL Test de la diffusion d’images]**.<br>Le serveur oblige les images de réponse à ne pas dépasser cette largeur et cette hauteur si la requête ne spécifie pas explicitement la taille d’affichage à l’aide de `wid=`, `hei=`ou `scl=`.<br>Voir aussi [DefaultPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultpix.html) dans le guide de référence des visionneuses Dynamic Media. |
| **[!UICONTROL Taille de miniature par défaut]** | Requis.<br>Utilisé à la place de l’attribut **[!UICONTROL Taille d’affichage par défaut]** pour les requêtes de miniature (`req=tmb`). Le serveur oblige les images de réponse à ne pas dépasser cette largeur et cette hauteur si une demande de miniature (`req=tmb`) ne spécifie pas la taille explicitement à l’aide de `wid=`, `hei=`ou `scl=`.<br>Voir aussi [DefaultThumbPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultthumbpix.html) dans le guide de référence des visionneuses Dynamic Media. |
| **[!UICONTROL Couleur d’arrière-plan par défaut]** | Indique la valeur de RGB utilisée pour remplir une zone d’une image de réponse qui ne contient pas de données d’image réelles.<br>Voir aussi [BkgColor](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-bkgcolor.html) dans le guide de référence des visionneuses Dynamic Media. |
| **[!UICONTROL Attributs d’encodage JPEG]** |  |
| **[!UICONTROL Qualité]** | <br>Indique l’attribut par défaut des images de réponse au format JPEG.<br>Pour les nouveaux comptes Dynamic Media uniquement, la variable **[!UICONTROL Qualité]** la valeur par défaut est automatiquement définie sur `80` pour les deux **[!UICONTROL Serveur d’images]** et **[!UICONTROL Test de la diffusion d’images]**.<br>Ce champ est défini entre 1 et 100.<br>Voir aussi [JpegQuality](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-jpegquality.html) dans le guide de référence des visionneuses Dynamic Media. |
| **[!UICONTROL Sous-échantillonnage chromatique]** | Activez ou désactivez le sous-échantillonnage chromatique utilisé par les encodeurs JPEG. |
| **[!UICONTROL Mode de rééchantillonnage par défaut]** | Indique les attributs de rééchantillonnage et d’interpolation par défaut à utiliser pour le redimensionnement des données d’image. Utilisez lorsque `resMode` n’est pas spécifié dans une requête.<br>Pour les nouveaux comptes Dynamic Media uniquement, le mode de rééchantillonnage par défaut est automatiquement défini sur `Sharp2` pour les deux **[!UICONTROL Serveur d’images]** et **[!UICONTROL Test de la diffusion d’images]**.<br>Voir aussi [ResMode](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-resmode.html) dans le guide de référence des visionneuses Dynamic Media. |

### Onglet Attributs de miniature courants {#common-thumbnail-attributes-tab}

Ces paramètres concernent l’aspect par défaut et l’alignement des images miniatures.

| Configuration | Description |
| --- | --- |
| **[!UICONTROL Couleur d’arrière-plan par défaut de la miniature]** | Indique la valeur de RGB utilisée pour remplir la zone d’une miniature de sortie qui ne contient pas de données d’image réelles. Utilisé uniquement pour les demandes de miniature (`req=tmb`) et à quel moment **[!UICONTROL Type de miniature par défaut]** est défini sur **[!UICONTROL Ajuster]** ou **[!UICONTROL Texture]**.<br>Voir aussi [ThumbBkgColor](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbbkgcolor.html) dans le guide de référence des visionneuses Dynamic Media. |
| **[!UICONTROL Alignement horizontal]** | Spécifie l’alignement horizontal de l’image miniature dans le rectangle de l’image de réponse spécifié par `wid=` et `hei=` valeurs.<br>Utilisé uniquement pour les demandes de miniature (`req=tmb`) et à quel moment **[!UICONTROL Type de miniature par défaut]** est défini sur **[!UICONTROL Ajuster]**.<br>Vous avez le choix entre trois alignements horizontaux : **[!UICONTROL Alignement centré]**, **[!UICONTROL Alignement à gauche]**, et **[!UICONTROL Alignement droit]**.<br>Voir aussi [ThumbHorizAlign](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbhorizalign.html) dans le guide de référence des visionneuses Dynamic Media. |
| **[!UICONTROL Alignement vertical]** | Spécifie l’alignement vertical de l’image miniature dans le rectangle de l’image de réponse spécifié par `wid=` et `hei=` valeurs. Utilisé uniquement pour les demandes de miniature (`req=tmb`) et à quel moment **[!UICONTROL Type de miniature par défaut]** est défini sur **[!UICONTROL Ajuster]**.<br>Vous avez le choix entre trois alignements verticaux : **[!UICONTROL Alignement supérieur]**, **[!UICONTROL Alignement centré]**, et **[!UICONTROL Alignement en bas]**.<br>Voir aussi [ThumbVertAlign](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbvertalign.html) dans le guide de référence des visionneuses Dynamic Media. |
| **[!UICONTROL Délai d’expiration par défaut du cache]** | Fournit un intervalle d’expiration par défaut en heures au cas où un enregistrement de catalogue spécifique ne contiendrait pas de valeur d’expiration de catalogue valide. Définissez sur . `-1` pour marquer comme n’ayant jamais expiré. <br>Voir aussi [Expiration](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-expiration.html) dans le guide de référence des visionneuses Dynamic Media. |
| **[!UICONTROL Type de miniature par défaut]** | Fournit une valeur par défaut pour le type de miniature lorsqu’un enregistrement de catalogue particulier ne contient pas de valeur ThumbType de catalogue valide. Utilisé uniquement pour les demandes de miniature (`req=tmb`).<br>Vous avez le choix entre trois types de miniatures : **[!UICONTROL Recadrer]**, **[!UICONTROL Ajuster]**, et **[!UICONTROL Texture]**.<br>Voir aussi [ThumbType](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbtype.html) dans le guide de référence des visionneuses Dynamic Media. |
| **[!UICONTROL Résolution de miniature par défaut]** | Fournit une valeur par défaut pour la résolution de l’objet de miniature lorsqu’un enregistrement de catalogue particulier ne contient pas de valeur ThumbRes de catalogue valide. Utilisé uniquement pour les demandes de miniature (`req=tmb`) et lorsque la variable **[!UICONTROL Type de miniature par défaut]** est défini sur **[!UICONTROL Texture]**.<br>Voir aussi [ThumbRes](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbres.html) dans le guide de référence des visionneuses Dynamic Media. |

### Onglet Attributs de gestion des couleurs {#color-management-attributes-tab}

Ces paramètres déterminent les profils de couleurs ICC utilisés pour les images.

**Mode de rendu de conversion des couleurs**
Un mode de rendu de conversion des couleurs permet de remplacer l’intention de rendu par défaut des profils de travail afin de déterminer comment les couleurs sources sont ajustées. Utilisé lorsque :

1. L’un des profils ICC par défaut est l’espace colorimétrique cible d’une conversion de couleurs.
1. Un périphérique de sortie (imprimante ou moniteur) est caractérisé par ce profil.
1. Et l’intention de rendu spécifiée est valide pour ce profil.

Les différents modes de rendu utilisent des règles différentes pour déterminer comment les couleurs source sont ajustées.

Voir aussi [IccRenderIntent](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccrenderintent.html) dans le guide de référence des visionneuses Dynamic Media.

>[!NOTE]
>
>En règle générale, il est préférable d’utiliser l’intention de rendu par défaut pour le paramètre de couleur sélectionné, qui a été testé par Adobe pour répondre aux normes du secteur. Par exemple, si vous choisissez un paramètre de couleur pour l’Amérique du Nord ou l’Europe, l’intention de rendu de conversion de couleur par défaut est : **[!UICONTROL Colorimétrie relative]**. Si vous choisissez un paramètre de couleur pour le Japon, l’intention de rendu de conversion de couleur par défaut est : **[!UICONTROL Perception]**.

| Configuration | Caractéristiques |
| --- | --- |
| **[!UICONTROL Espace colorimétrique CMJN par défaut]** | Indique le nom du profil de couleurs ICC à utiliser comme profil de travail pour les données CMJN. If **[!UICONTROL Aucun spécifié]** est sélectionné, la gestion des couleurs est désactivée pour ce catalogue d’images lorsque des images source CMJN sont impliquées. Tous les espaces de travail CMJN dépendent des appareils, ce qui signifie qu’ils sont basés sur des combinaisons d’encre et de papier réelles. Les Adobes des espaces de travail CMJN sont basés sur des conditions d’impression commerciales standard.<br> Voir aussi [IccProfileCMJN](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilecmyk.html) dans le guide de référence des visionneuses Dynamic Media. |
| **[!UICONTROL Espace colorimétrique de niveaux de gris par défaut]** | Indique le nom du profil de couleurs ICC à utiliser comme profil de travail pour les données en niveaux de gris. If **[!UICONTROL Aucun spécifié]** est sélectionnée, la gestion des couleurs est désactivée pour ce catalogue d’images lorsque des images source en niveaux de gris sont impliquées.<br>Voir aussi [IccProfileGray](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilegray.html) dans le guide de référence des visionneuses Dynamic Media. |
| **[!UICONTROL Espace colorimétrique RVB par défaut]** | Indique le nom du profil de couleurs ICC à utiliser comme profil de travail pour les données de RGB. If **[!UICONTROL Aucun spécifié]** est sélectionnée, la gestion des couleurs est désactivée pour ce catalogue d’images lorsque des images sources RGB sont impliquées. En général, il est préférable de choisir **[!UICONTROL Adobe RGB]** ou **[!UICONTROL sRVB]**, plutôt que le profil d’un appareil spécifique (tel qu’un profil de moniteur). **[!UICONTROL sRVB]** est recommandé lorsque vous préparez des images pour le web ou les appareils mobiles, car il définit l’espace colorimétrique du moniteur standard utilisé pour afficher les images sur le web. **[!UICONTROL sRVB]** est également un bon choix lorsque vous utilisez des images issues d’appareils photo numériques de niveau consommateur, car la plupart de ces appareils utilisent sRVB comme espace colorimétrique par défaut.<br>Voir aussi [IccProfileRBG](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilergb.html) dans le guide de référence des visionneuses Dynamic Media. |
| **[!UICONTROL Intention de rendu de conversion des couleurs]** | **[!UICONTROL Perception]** - vise à préserver la relation visuelle entre les couleurs afin qu’elles soient perçues comme naturelles pour l’oeil humain, même si les valeurs de couleur elles-mêmes peuvent changer. Cette intention est adaptée aux images photographiques avec de nombreuses couleurs prêtes à l’emploi. Ce paramètre est l’intention de rendu standard pour l’industrie de l’impression japonaise. |
|  | **[!UICONTROL Colorimétrie relative]** - Compare la mise en surbrillance extrême de l’espace colorimétrique source à celle de l’espace colorimétrique de destination et modifie toutes les couleurs en conséquence. Les couleurs hors gamme sont décalées vers la couleur reproductible la plus proche dans l’espace colorimétrique de destination. Le paramètre Colorimétrie relative conserve plus de couleurs d’origine dans une image que le paramètre Perception. Ce paramètre est l’intention de rendu standard pour l’impression en Amérique du Nord et en Europe. |
|  | **[!UICONTROL Saturation]** - Tente de produire des couleurs vives dans une image au détriment de la précision des couleurs. Cette intention de rendu convient aux graphiques professionnels tels que les graphiques ou les graphiques, où les couleurs saturées sont plus importantes que la relation exacte entre les couleurs. |
|  | **[!UICONTROL Colorimétrie absolue]** : laisse inchangées les couleurs qui se trouvent dans la gamme de couleurs de destination. Les couleurs standard sont tronquées. Aucune mise à l’échelle des couleurs n’est effectuée sur le point blanc de destination. Cette intention vise à maintenir la précision des couleurs au détriment de la préservation des relations entre les couleurs et est adaptée à la vérification pour simuler la sortie d’un appareil particulier. Cette intention est utile pour prévisualiser l’impact de la couleur du papier sur les couleurs imprimées. |

## Test des ressources avant de les rendre publiques {#test-assets-before-making-public}

Les tests sécurisés vous aident à définir un environnement de test sécurisé et à créer une solution business-to-business robuste, basée sur un ensemble configurable d’adresses IP et de plages. Cette fonctionnalité vous permet de faire correspondre vos déploiements Dynamic Media Adobe avec l’architecture de votre système de gestion de contenu et de votre système d’entreprise.

Avec Secure Testing, vous pouvez prévisualiser la version intermédiaire du site web avec du contenu non publié.

Si vous le souhaitez, créez un environnement d’évaluation plutôt que de rendre les ressources publiques disponibles pour les raisons suivantes :

* Aperçu des sites web avant le lancement public (site web intermédiaire).
* Servez les ressources qui nécessitent un accès restreint, telles que les catalogues électroniques qui affichent les prix dans une application web B2B.
* Utilisez des ressources derrière un pare-feu dans le cadre du système de gestion des informations sur les produits, de l’application du service client, du site de formation, etc.

>[!NOTE]
>
>Le test sécurisé n’affecte pas l’accès à Adobe Dynamic Media Classic. La sécurité d’Adobe Dynamic Media Classic reste cohérente et requiert les informations d’identification habituelles pour l’accès à Adobe Dynamic Media Classic et aux services Web associés.

### Fonctionnement du test sécurisé {#how-test-assets-works}

La plupart des entreprises tiennent Internet derrière un pare-feu. L’accès à Internet est possible par certaines routes et généralement par une plage limitée d’adresses IP publiques.

À partir du réseau de votre entreprise, vous pouvez déterminer votre adresse IP publique à l’aide de sites web tels que [https://www.whatismyip.com](https://www.whatismyip.com/) ou demandez ces informations à votre entreprise informatique.

Avec les tests sécurisés, Adobe Dynamic Media établit un serveur d’images dédié pour les environnements d’évaluation ou les applications internes. Toute requête à ce serveur vérifie l’adresse IP d’origine. Si la requête entrante ne figure pas dans la liste approuvée des adresses IP, une réponse d’échec est renvoyée. L’administrateur d’entreprise Adobe Dynamic Media configure la liste approuvée des adresses IP pour l’environnement de test sécurisé de l’entreprise.

L’emplacement de la requête d’origine devant être confirmé, le trafic du service Secure Testing n’est pas acheminé via un réseau de distribution de contenu tel que le trafic du serveur d’images Dynamic Media public. Les demandes au service Secure Testing présentent une latence légèrement plus élevée que les serveurs d’images Dynamic Media publics.

Les ressources non publiées sont immédiatement disponibles à partir des services Secure Testing, sans avoir à les publier. Ainsi, vous pouvez exécuter un aperçu avant que les ressources ne soient publiées sur leur serveur d’images public.

>[!NOTE]
>
>Les services de test sécurisé utilisent le serveur de catalogue configuré avec un contexte de publication interne. Par conséquent, si votre entreprise est configurée pour publier sur Secure Testing, toutes les ressources chargées dans Adobe Dynamic Media sont immédiatement disponibles sur les services de test sécurisé. Cette fonctionnalité est vraie que les ressources soient marquées pour publication au moment du téléchargement ou non.

Les services Secure Testing prennent actuellement en charge les types et fonctionnalités de ressources suivants :

* Images.
* Vignettes (demandes de serveur de rendu).
* Requêtes de serveur de rendu (prises en charge, mais doivent être demandées explicitement par le client).
* Visionneuses, notamment visionneuses d’images, catalogue électronique, visionneuses de rendus et de supports.
* Visionneuses de médias riches Dynamic Media standard Adobe.
* Adobe des pages JSP Dynamic Media On Demand.
* Contenu statique, comme des fichiers de PDF et des vidéos diffusées progressivement.
* Diffusion vidéo en continu HTTP.
* Diffusion vidéo progressive en continu.

Les types et fonctionnalités de ressources suivants ne sont actuellement pas pris en charge :

* Adobe Dynamic Media Classic Info ou recherche eCatalog
* Diffusion vidéo en continu RTMP
* Impression en ligne
* Services de contenu généré par l’utilisateur

>[!IMPORTANT]
>
>La prise en charge des ressources d’image vectorielle UGC nouvelles ou existantes dans Adobe Dynamic Media s’est terminée le 30 septembre 2021.

### Test du service Secure Testing {#test-secure-testing-service}

Pour vous assurer que le service Secure Testing fonctionne comme prévu, procédez comme suit :

#### Préparation de votre compte

1. Contactez l’assistance clientèle d’Adobe et demandez-lui d’activer le test sécurisé sur votre compte.
1. Dans Adobe Experience Manager, sélectionnez **[!UICONTROL Outils]** > **[!UICONTROL Ressources]** > **[!UICONTROL Configuration de la publication Dynamic Media]**.
1. Sur la page du serveur d’images, dans la variable **[!UICONTROL Contexte de publication]** liste déroulante, sélectionnez **[!UICONTROL Test de la diffusion d’images]**.
1. Sélectionnez la **[!UICONTROL Sécurité]** .
1. Pour le **[!UICONTROL Adresse du client]** filtrer, sélectionner **[!UICONTROL Ajouter]**.
1. Dans le **[!UICONTROL Adresse IP]** , saisissez une adresse IP.
1. Dans le **[!UICONTROL Masque]** , saisissez un masque de filet.

   >[!NOTE]
   >
   >Si vous ajoutez plusieurs adresses IP et masques de réseau, cela vous permet effectivement de *all* Adresses IP pour effectuer des appels de ressources, et elles s’affichent toutes.

1. Utilisez l’une des méthodes suivantes :

   * Pour ajouter d’autres adresses IP, répétez les trois étapes précédentes.
   * Passez à l’étape suivante.

1. Dans le coin supérieur droit de la page Image Server, sélectionnez **[!UICONTROL Enregistrer]**.
1. Chargez les images souhaitées dans votre compte Dynamic Media Adobe.

<!--    See [Upload files](uploading-files.md#uploading_files). -->

1. Assurez-vous que certaines images sont marquées pour publication et d’autres non marquées, puis envoyez la tâche de publication.

<!--    See [Publish files](publishing-files.md#publishing_files). -->

1. Déterminez le nom de votre service de test sécurisé en accédant à **[!UICONTROL Outils]** > **[!UICONTROL Ressources]** > **[!UICONTROL Paramètre général Dynamic Media]**.
1. Sur le **[!UICONTROL Serveur]** , recherchez le nom du serveur à droite de **[!UICONTROL Nom du serveur publié]**.

Contactez le service à l’Adobe si le nom du serveur est manquant ou si l’URL du serveur ne fonctionne pas.

#### Préparation des variations de site web

Vous avez besoin de deux variantes d’un site web qui lie les ressources publiées et non publiées :

* Version publique : liez les ressources à l’aide de votre syntaxe d’URL Dynamic Media Adobe traditionnelle.
* Version intermédiaire : liez les ressources en utilisant la même syntaxe mais avec le nom du site de test sécurisé.

#### Exécution des tests

Effectuez les tests suivants :

1. Vérifiez si les ressources sont visibles depuis votre réseau d’entreprise.

   Depuis le réseau d’entreprise identifié par la plage d’adresses IP définie précédemment, la version intermédiaire du site web affiche toutes les images, qu’elles soient marquées pour publication ou non. Ainsi, vous pouvez tester sans rendre les images disponibles accidentellement avant l’approbation de l’aperçu ou le lancement du produit.

   Vérifiez que la version publique de votre site affiche les ressources publiées comme vous l’avez déjà fait avec Adobe Dynamic Media.

1. En dehors de votre réseau d’entreprise, vérifiez que les ressources non publiées (c’est-à-dire sans marque pour publication) sont protégées contre l’accès tiers.

   Accédez à votre réseau depuis l’extérieur (depuis votre ordinateur personnel, par exemple, ou via une connexion 4G/5G), puis vérifiez que la version publique du site affiche toutes les ressources publiées, mais pas le contenu non publié.

   Vérifiez que la version intermédiaire n’affiche aucune ressource, car vous accédez au service Secure Testing à partir d’une adresse IP non approuvée.
