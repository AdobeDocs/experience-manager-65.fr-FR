---
title: Ajout de fonctionnalités Dynamic Media Classic (Scene7) à votre page
description: Adobe Dynamic Media Classic (Scene7) est une solution hébergée pour la gestion, l’amélioration, la publication et la diffusion de contenus multimédias enrichis sur les canaux web, mobiles, par e-mail, sur les appareils connectés à Internet et par impression.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: bc9c864b-8bc3-42b4-ba25-6c5108be4f65
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '3545'
ht-degree: 100%

---

# Ajout de fonctionnalités Dynamic Media Classic (Scene7) à votre page{#adding-scene-features-to-your-page}

[Adobe Dynamic Media Classic (Scene7)](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/home.html?lang=fr) est une solution hébergée pour la gestion, l’amélioration, la publication et la diffusion de contenus multimédias enrichis sur les canaux web, mobiles, par e-mail, sur les appareils connectés à Internet et par impression.

Vous pouvez afficher les ressources de Experience Manager publiées dans Dynamic Media Classic (Scene7) dans différentes visionneuses :

* Zoom
* Fenêtre déroulante
* Vidéo
* Modèle d’image
* Image

Vous pouvez publier des ressources numériques directement depuis Experience Manager vers Dynamic Media Classic (Scene7) et vous pouvez publier des ressources numériques depuis Dynamic Media Classic (Scene7) vers Experience Manager.

Ce document décrit comment publier des ressources numériques d’Experience Manager vers Dynamic Media Classic (Scene7) et inversement. Les visionneuses sont également décrites en détail. Pour plus d’informations sur la configuration d’Experience Manager pour Dynamic Media Classic (Scene7), consultez l’[Intégration de Dynamic Media Classic (Scene7) à Experience Manager](/help/sites-administering/scene7.md).

Consultez également la section [Ajout de zones cliquables](/help/assets/image-maps.md).

Pour plus d’informations sur l’utilisation des composants vidéo avec Experience Manager, voir :

* [Vidéo](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md)

>[!NOTE]
>
>Si les ressources de Dynamic Media Classic (Scene7) ne s’affichent pas correctement, assurez-vous que Dynamic Media est [désactivé](/help/assets/config-dynamic.md#disabling-dynamic-media), puis actualisez la page.

## Publication manuelle dans Dynamic Media Classic (Scene7) à partir d’Assets {#manually-publishing-to-scene-from-assets}

Vous pouvez publier des ressources numériques sur Dynamic Media Classic (Scene7) depuis la console Assets de l’interface utilisateur classique ou directement depuis la ressource.

>[!NOTE]
>
>Experience Manager publie sur Dynamic Media Classic (Scene7) de manière asynchrone. Une fois que vous avez sélectionné **[!UICONTROL Publier]**, il peut s’écouler plusieurs secondes avant que l’élément soit publié sur Dynamic Media Classic (Scene7).
>

### Publication depuis la console Assets {#publishing-from-the-assets-console}

Vous pouvez effectuer une publication sur Dynamic Media Classic (Scene7) à partir de la console Assets si les ressources se trouvent dans un dossier cible Dynamic Media Classic (Scene7).

1. Dans l’interface utilisateur classique d’Experience Manager, sélectionnez **[!UICONTROL Ressources numériques]** pour accéder au gestionnaire de ressources numériques.

1. Sélectionnez, depuis le dossier cible, la ressource (ou les ressources) ou le dossier que vous souhaitez publier sur Dynamic Media Classic (Scene7), puis cliquez avec le bouton droit et sélectionnez **[!UICONTROL Publier sur Dynamic Media Classic (Scene7)]**. Vous pouvez également sélectionner **[!UICONTROL Publier vers Dynamic Media Classic (Scene7)]** à partir du menu **[!UICONTROL Tools]**.

   ![chlimage_1-48](assets/chlimage_1-48.png)

1. Accédez à Dynamic Media Classic (Scene7) et confirmez que les ressources sont disponibles.

   >[!NOTE]
   >
   >Si celles-ci ne figurent pas dans un dossier synchronisé Dynamic Media Classic (Scene7), l’option **[!UICONTROL Publier vers Dynamic Media Classic (Scene7)]** des deux menus est visible mais désactivée.

### Publication depuis une ressource {#publishing-from-an-asset}

Vous pouvez publier manuellement une ressource sous réserve que celle-ci figure dans le dossier Dynamic Media Classic (Scene7) synchronisé.

>[!NOTE]
>
>Si la ressource ne se trouve pas dans le dossier synchronisé de Dynamic Media Classic (Scene7), le lien vers **[!UICONTROL Publication sur Dynamic Media Classic (Scene7)]** n’apparaît pas.

Pour publier sur Dynamic Media Classic (Scene7) directement depuis une ressource numérique, procédez comme suit :

1. Dans Experience Manager, sélectionnez **[!UICONTROL Ressources numériques]** pour accéder au gestionnaire de ressources numériques.

1. Double-cliquez pour ouvrir une ressource.

1. Dans le volet des détails de la ressource, sélectionnez **[!UICONTROL Publier sur Dynamic Media Classic (Scene7)]**.

   ![screen_shot_2012-02-22at34828pm](assets/screen_shot_2012-02-22at34828pm.png)

1. Le lien devient **[!UICONTROL Publication...]**, puis **[!UICONTROL Publié]**. Accédez à Dynamic Media Classic (Scene7) et confirmez que la ressource est disponible.

   >[!NOTE]
   >
   >Si la ressource n’est pas publiée correctement sur Dynamic Media Classic (Scene7), le lien devient **[!UICONTROL Échec de la publication]**. Si la ressource a déjà été publiée sur Dynamic Media Classic (Scene7), le lien est celui-ci : **[!UICONTROL Republication sur Dynamic Media Classic (Scene7)]**. La republication vous permet de modifier des ressources dans Experience Manager et de les republier.

### Publication de ressources depuis un dossier autre que le dossier cible CQ {#publishing-assets-from-outside-the-cq-target-folder}

Adobe recommande de publier des ressources dans Dynamic Media Classic (Scene7) uniquement à partir des ressources du dossier cible Dynamic Media Classic (Scene7). Néanmoins, si vous devez charger des ressources depuis un dossier autre que le dossier cible, cette opération est possible en les téléchargeant dans un dossier à la demande dans Dynamic Media Classic (Scene7). Tout d’abord, configurez la configuration cloud de la page sur laquelle vous souhaitez que la ressource s’affiche. Vous ajoutez ensuite un composant Dynamic Media Classic (Scene7) à la page et faites glisser une ressource sur le composant. Une fois que les propriétés sont définies pour cette page, un lien **[!UICONTROL Publier vers Dynamic Media Classic (Scene7)]** apparaît. Lorsque ce lien est sélectionné, il déclenche le chargement vers Dynamic Media Classic (Scene7).

>[!NOTE]
>
>Les éléments qui figurent dans le dossier à la demande n’apparaissent pas dans le navigateur de contenu Dynamic Media Classic (Scene7).

**Publication de ressources depuis un dossier autre que le dossier cible CQ :**

1. Dans Experience Manager, dans l’interface utilisateur classique, sélectionnez **[!UICONTROL Sites web]** et accédez à la page web à laquelle vous souhaitez ajouter une ressource numérique qui n’est pas encore publiée sur Dynamic Media Classic (Scene7). (Les règles normales d’héritage de la page s’appliquent.)

1. Dans le sidekick, sélectionnez l’icône **[!UICONTROL Page]**, puis **[!UICONTROL Propriétés de la page]**.

1. Sélectionnez **[!UICONTROL Services cloud]**.
1. Sélectionnez **[!UICONTROL Ajout de services]**.
1. Sélectionnez **[!UICONTROL Dynamic Media Classic (Scene7)]**.
1. Dans la liste déroulante **[!UICONTROL Dynamic Media Classic (Scene7)]**, sélectionnez la configuration souhaitée puis **[!UICONTROL OK]**.

   ![chlimage_1-49](assets/chlimage_1-49.png)

1. Sur la page web, ajoutez un composant Dynamic Media Classic (Scene7) à l’emplacement souhaité sur la page.
1. Depuis l’outil de recherche de contenu, faites glisser une ressource numérique vers le composant. Un lien permettant de **[!UICONTROL Vérifier le statut de la publication sur Dynamic Media Classic (Scene7)]** apparaît.

   >[!NOTE]
   >
   >Si la ressource numérique figure dans le dossier cible CQ, le lien permettant de **[!UICONTROL Vérifier le statut de la publication sur Dynamic Media Classic (Scene7)]** n’apparaît pas. Les ressources sont placées dans le composant.

   ![chlimage_1-50](assets/chlimage_1-50.png)

1. Sélectionnez **[!UICONTROL Vérification du statut de publication de Dynamic Media Classic (Scene7)]**. Si les ressources ne sont pas publiées, Experience Manager les publie dans Dynamic Media Classic (Scene7). Une fois téléchargée, la ressource figure dans le dossier à la demande. Par défaut, le dossier à la demande est situé dans le chemin d’accès **[!UICONTROL nom_de_la_société/CQ5_adhoc]**. Vous pouvez [configurer le dossier à la demande, si nécessaire](#configuringtheadhocfolder).

   >[!NOTE]
   >
   >Si l’élément ne figure pas dans un dossier synchronisé Dynamic Media Classic (Scene7) et qu’aucune configuration cloud Dynamic Media Classic (Scene7) n’est associée à la page actuelle, le chargement échoue.

## Composants Dynamic Media Classic (Scene7) {#scene-components}

Les composants Dynamic Media Classic (Scene7) suivants sont disponibles dans Experience Manager :

* Zoom
* Zoom sur la fenêtre déroulante
* Modèle d’image
* Image
* Vidéo

>[!NOTE]
>
>Ces composants ne sont pas disponibles par défaut et doivent être sélectionnés en mode Conception avant leur utilisation.

Une fois qu’ils sont disponibles en mode Conception, vous pouvez les ajouter à votre page comme n’importe quel composant Experience Manager. Les ressources qui ne sont pas encore publiées sur Dynamic Media Classic (Scene7) sont publiées sur Dynamic Media Classic (Scene7) si elles se trouvent dans un dossier synchronisé, sur une page ou avec une configuration cloud Dynamic Media Classic (Scene7).

>[!NOTE]
>
>Si vous créez et développez des visionneuses S7 personnalisées et que vous utilisez l’outil de recherche de contenu, vous devez explicitement ajouter le paramètre `allowfullscreen`.

### Notification de fin de prise en charge de la visionneuse Flash {#flash-viewers-end-of-life-notice}

À compter du 31 janvier 2017, Adobe Dynamic Media Classic (Scene7) a officiellement arrêté la prise en charge de la plateforme de la visionneuse Flash.

### Ajout d’un composant Dynamic Media Classic (Scene7) à une page {#adding-a-scene-component-to-a-page}

L’ajout d’un composant Dynamic Media Classic (Scene7) à une page est identique à l’ajout d’un composant sur n’importe quelle page. Les composants Dynamic Media Classic (Scene7) sont décrits en détail dans les sections suivantes.

Pour ajouter un composant ou une visionneuse Dynamic Media Classic (Scene7) à une page dans l’interface utilisateur classique, procédez comme suit :

1. Dans Experience Manager, ouvrez la page où vous souhaitez ajouter le composant Dynamic Media Classic (Scene7).

1. Si aucun composant Dynamic Media Classic (Scene7) n’est disponible, sélectionnez la règle dans le sidekick pour passer en mode **Conception**, sélectionnez le parsys **[!UICONTROL Modifier]** et sélectionnez tous les composants **[!UICONTROL Dynamic Media Classic (Scene7)]** pour les rendre disponibles.

1. Revenez au mode **Modifier** en cliquant sur le crayon dans le sidekick.

1. Faites glisser un composant du groupe **[!UICONTROL Dynamic Media Classic (Scene7)]** dans le sidekick vers la page à l’emplacement souhaité.

1. Sélectionnez ***[!UICONTROL Modifier]** afin de pouvoir ouvrir le composant.

1. Modifiez le composant comme requis et sélectionnez **[!UICONTROL OK]** pour enregistrer les modifications.

### Ajout d’expériences de visionnage interactif à un site web réactif {#adding-interactive-viewing-experiences-to-a-responsive-website}

Une conception réactive signifie que les éléments s’adaptent selon l’emplacement où ils sont affichés. Avec la conception réactive, les mêmes éléments peuvent être affichés sur plusieurs appareils.

Pour ajouter une expérience de visionnage interactif à un site réactif par l’intermédiaire de l’interface utilisateur classique, procédez comme suit :

1. Connectez-vous à Experience Manager et assurez-vous d’avoir configuré les [services cloud Adobe Dynamic Media Classic (Scene7)](/help/sites-administering/scene7.md#configuring-scene-integration) et que les composants Dynamic Media Classic (Scene7) sont disponibles.

   >[!NOTE]
   >
   >Si les composants de la gestion de contenu web Dynamic Media Classic (Scene7) ne sont pas disponibles, assurez-vous de les activer par l’intermédiaire du mode Conception.

1. Dans un site web dont les composants Dynamic Media Classic (Scene7) sont activés, faites glisser une visionneuse **[!UICONTROL Image]** vers la page.
1. Modifiez le composant et ajustez les points d’arrêt dans l’onglet **[!UICONTROL Paramètres de Dynamic Media Classic (Scene7)]**.

   ![chlimage_1-51](assets/chlimage_1-51.png)

1. Confirmez que les visionneuses se redimensionnent de manière réactive et que toutes les interactions sont optimisées pour les ordinateurs de bureau, les tablettes et les appareils mobiles.

### Paramètres communs à tous les composants Dynamic Media Classic (Scene7) {#settings-common-to-all-scene-components}

Bien que les options de configuration varient, les paramètres suivants sont communs à tous les composants Dynamic Media Classic (Scene7) :

* **Référence du fichier** : accédez à un fichier que vous souhaitez référencer. La référence du fichier affiche l’URL de l’élément, et pas nécessairement l’ensemble de l’URL Dynamic Media Classic (Scene7), notamment les commandes et paramètres d’URL. Vous ne pouvez pas ajouter de commandes et de paramètres d’URL Dynamic Media Classic (Scene7) dans ce champ. Au lieu de cela, ils doivent être ajoutés par l’intermédiaire de la fonctionnalité correspondante du composant.
* **Largeur** - Permet de définir la largeur.
* **Hauteur** - Permet de définir la hauteur.

Vous définissez ces options de configuration en ouvrant (double-cliquant) un composant Dynamic Media Classic (Scene7), par exemple, lorsque vous ouvrez un composant **Zoom** :

![chlimage_1-52](assets/chlimage_1-52.png)

### Zoom {#zoom}

Le composant Zoom HTML5 affiche une image plus grande lorsque vous appuyez sur le bouton +.

L’élément comporte des outils de zoom dans sa partie inférieure. Sélectionnez **[!UICONTROL +]** pour agrandir l’image. Sélectionnez **[!UICONTROL -]** pour réduire l’image. Pour rétablir l’image à sa taille d’origine au moment de son importation, sélectionnez **[!UICONTROL x]** ou cliquez sur la flèche de réinitialisation du zoom. Sélectionnez les flèches diagonales pour l’afficher en plein écran. Sélectionnez **[!UICONTROL Modifier]** pour pouvoir configurer le composant. Avec ce composant, vous pouvez configurer les [paramètres communs à tous les composants Dynamic Media Classic (Scene7)](#settings-common-to-all-scene-components).

![Image de fleurs de tulipes dans le composant Zoom HTML5.](do-not-localize/chlimage_1-3.png)

### Flyout {#flyout}

Dans le composant Fenêtre déroulante HTML5, l’élément s’affiche sous la forme d’un écran partagé : à gauche se trouve l’élément à la taille spécifiée, à droite la partie sur laquelle le zoom a été effectué. Sélectionnez **[!UICONTROL Modifier]** pour pouvoir configurer le composant. Avec ce composant, vous pouvez configurer les [paramètres communs à tous les composants Dynamic Media Classic (Scene7)](/help/sites-administering/scene7.md#settingscommontoallscene7components).

>[!NOTE]
>
>Si le composant Fenêtre déroulante utilise une taille personnalisée, cette taille personnalisée est utilisée et la configuration réactive du composant est désactivée.
>
>Si votre composant Fenêtre déroulante utilise la taille par défaut, comme définie dans la vue Conception, la taille par défaut est utilisée. Le composant s’étire pour s’adapter à la taille de la mise en page avec la configuration réactive du composant activée. Néanmoins, gardez à l’esprit qu’il existe une limite à la configuration réactive du composant. Lorsque vous utilisez le composant Fenêtre déroulante avec la configuration réactive, vous ne devez pas l’utiliser avec l’étirement de pleine page. Sinon, la fenêtre déroulante peut s’étendre au-delà de la bordure droite de la page.

![chlimage_1-53](assets/chlimage_1-53.png)

### Image {#image}

Le composant d’image Dynamic Media Classic (Scene7) vous permet d’ajouter une fonctionnalité Dynamic Media Classic (Scene7) à vos images, comme les modificateurs Dynamic Media Classic (Scene7), les paramètres d’image ou de visionneuse prédéfinis et l’accentuation. Le composant d’image Dynamic Media Classic (Scene7) est similaire aux autres composants d’image dans Experience Manager avec des fonctionnalités spécifiques à Dynamic Media Classic (Scene7). Dans cet exemple, l’image dispose du modificateur d’URL Dynamic Media Classic (Scene7) `&op_invert=1` appliqué.

![Image d’une sphère dans le composant d’image Dynamic Media Classic (Scene7)](do-not-localize/chlimage_1-4.png)

**Titre, Text secondaire** - Dans l’onglet Avancé, ajoutez un titre à l’image et au texte de remplacement destinés aux utilisateurs pour lesquels les graphiques sont désactivés.

**URL, Ouvrir dans** : vous pouvez définir une ressource pour ouvrir un lien. Définissez l’URL, puis dans le champ Ouvrir dans, indiquez si vous souhaitez l’ouvrir dans la même fenêtre ou une nouvelle fenêtre.

![chlimage_1-54](assets/chlimage_1-54.png)

**Paramètre prédéfini de la visionneuse** : sélectionnez un paramètre prédéfini de visionneuse existant. Si le paramètre prédéfini de visionneuse que vous recherchez n’est pas visible, vous devez le rendre visible. Voir Gestion des paramètres prédéfinis de visionneuse. Si vous utilisez un paramètre prédéfini d’image, vous ne pouvez pas sélectionner de paramètre prédéfini de visionneuse, et inversement.

**Configuration de Dynamic Media Classic (Scene7)** - Sélectionnez la configuration Dynamic Media Classic (Scene7) que vous souhaitez utiliser pour récupérer les paramètres prédéfinis d’image principaux à partir de SPS.

**Paramètre prédéfini d’image** : sélectionnez un paramètre prédéfini d’image existant. Si le paramètre prédéfini d’image que vous recherchez n’est pas visible, vous devez le rendre visible. Voir Gestion des paramètres d’image prédéfinis. Si vous utilisez un paramètre prédéfini d’image, vous ne pouvez pas sélectionner de paramètre prédéfini de visionneuse, et inversement.

**Format de sortie** : sélectionnez le format de sortie de l’image, par exemple JPEG. Selon le format de sortie que vous sélectionnez, vous pouvez ajouter des options de configuration supplémentaires. Consultez les Bonnes pratiques relatives aux paramètres prédéfinis d’image.

**Accentuation** - Sélectionnez le mode d’accentuation de l’image. L’accentuation est expliquée en détails dans les rubriques Bonnes pratiques relatives aux paramètres prédéfinis d’image et Bonnes pratiques relatives à l’accentuation.

**Modificateurs d’URL** - Vous pouvez modifier les effets d’image en fournissant des commande d’image S7 supplémentaires. Ces commandes sont décrites dans la section Paramètres prédéfinis d’image et le guide de référence des commandes.

**Points d’arrêt** - Si votre site web est réactif, vous pouvez modifier les points d’arrêt. Les points d’arrêt doivent être séparés par des virgules (,).

### Modèle d’image {#image-template}

Les modèles d’image Dynamic Media Classic (Scene7) sont du contenu Photoshop en couches qui a été importé vers Dynamic Media Classic (Scene7), où le contenu et les propriétés ont été paramétrés pour la variabilité. Le composant **[!UICONTROL Modèle d’image]** permet d’importer des images et de modifier le texte dynamiquement dans Experience Manager. En outre, vous pouvez configurer le composant **[!UICONTROL Modèle d’image]** afin d’utiliser des valeurs provenant de ClientContext de sorte que chaque utilisateur voit l’image d’une manière personnalisée.

Sélectionnez **[!UICONTROL Modifier]** pour configurer le composant. Vous pouvez configurer des [paramètres communs à tous les composants Dynamic Media Classic (Scene7)](/help/sites-administering/scene7.md#settingscommontoallscene7components) et d’autres paramètres décrits dans cette section.

![chlimage_1-55](assets/chlimage_1-55.png)

**Référence du fichier, Largeur, Hauteur** - Consultez [paramètres communs à tous les composants Dynamic Media Classic (Scene7)](/help/sites-administering/scene7.md#settingscommontoallscene7components).

>[!NOTE]
>
>Les commandes et paramètres d’URL Dynamic Media Classic (Scene7) ne peuvent pas être ajoutés directement à l’URL de Référence du fichier. Ils ne peuvent être définis que dans l’interface utilisateur du composant, dans le panneau **[!UICONTROL Paramètre]**.

**Titre, Texte de remplacement** - Dans l’onglet Modèle d’image Dynamic Media Classic (Scene7), ajoutez un titre à l’image et un texte de remplacement destiné aux utilisateurs pour lesquels les graphiques sont désactivés.

**URL, Ouvrir dans** : vous pouvez définir une ressource pour ouvrir un lien. Définissez l’URL, puis dans le champ Ouvrir dans, indiquez si vous souhaitez l’ouvrir dans la même fenêtre ou une nouvelle fenêtre.

![chlimage_1-56](assets/chlimage_1-56.png)

**Panneau Paramètre** - Lors de l’importation d’une image, les paramètres sont préremplis avec les informations provenant de l’image. En l’absence de contenu pouvant être modifié dynamiquement, cette fenêtre est vide.

![chlimage_1-57](assets/chlimage_1-57.png)

#### Modification dynamique du texte {#changing-text-dynamically}

Pour une modification dynamique du texte, saisissez le nouveau texte dans les champs, puis sélectionnez **[!UICONTROL OK]**. Dans cet exemple, le **Prix** est désormais de 50 $ et l’expédition de 99 cents.

![chlimage_1-58](assets/chlimage_1-58.png)

Le texte de l’image change. Vous pouvez réinitialiser le texte sur la valeur d’origine en cliquant sur **[!UICONTROL Réinitialiser]** en regard du champ.

![chlimage_1-59](assets/chlimage_1-59.png)

#### Modification du texte afin de refléter une valeur de contexte client {#changing-text-to-reflect-the-value-of-a-client-context-value}

Pour lier un champ à une valeur de contexte client, sélectionnez **[!UICONTROL Sélectionner]** pour ouvrir le menu de contexte client, sélectionnez le contexte client, puis sélectionnez **[!UICONTROL OK]**. Dans cet exemple, le nom change selon la liaison entre le Nom et le nom formaté du profil.

![chlimage_1-60](assets/chlimage_1-60.png)

Le texte reflète le nom de l’utilisateur actuellement connecté. Vous pouvez réinitialiser le texte sur la valeur d’origine en cliquant sur **[!UICONTROL Réinitialiser]** en regard du champ.

![chlimage_1-61](assets/chlimage_1-61.png)

#### Transformer le modèle d’image Dynamic Media Classic (Scene7) en lien {#making-the-scene-image-template-a-link}

Vous pouvez transformer un composant de modèle d’image Dynamic Media Classic (Scene7) en lien cliquable.

1. Sur la page contenant le composant de modèle d’image Dynamic Media Classic (Scene7), sélectionnez **[!UICONTROL Modifier]**.
1. Dans le champ **[!UICONTROL URL]**, saisissez l’URL à laquelle l’utilisateur accède lorsqu’il clique sur l’image. Dans le champ **[!UICONTROL Ouvrir dans]**, choisissez où vous souhaitez que la cible s’ouvre (une nouvelle fenêtre ou la même fenêtre).

   ![chlimage_1-62](assets/chlimage_1-62.png)

1. Sélectionnez **[!UICONTROL OK]**.

### Composant vidéo {#video-component}

Le composant **[!UICONTROL Vidéo]** de Dynamic Media Classic (Scene7), disponible depuis la section Dynamic Media Classic (Scene7) du sidekick, utilise la détection d’appareil et de bande passante pour diffuser la vidéo adaptée à chaque écran. Ce composant est un lecteur vidéo HTML5. Il s’agit d’une visionneuse unique pouvant être utilisée sur plusieurs canaux.

Il peut être utilisé pour des visionneuses de vidéos adaptatives, une vidéo MP4 unique ou une vidéo F4V unique.

Pour plus d’informations sur le fonctionnement des vidéos avec l’intégration de Dynamic Media Classic (Scene7), consultez [Vidéo](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md). En outre, consultez [le comparatif entre le composant **vidéo Dynamic Media Classic (Scene7)** et le composant **vidéo** de base](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md).

![chlimage_1-63](assets/chlimage_1-63.png)

### Limitations connues du composant vidéo {#known-limitations-for-the-video-component}

La gestion des ressources numériques et la gestion de contenu web d’Adobe indiquent si une vidéo source principale est chargée. Elles n’affichent pas les éléments proxy suivants :

* Rendus codés Dynamic Media Classic (Scene7)
* Visionneuses de vidéos adaptatives Dynamic Media Classic (Scene7)

Lors de l’utilisation d’une visionneuse de vidéos adaptative avec le composant vidéo Dynamic Media Classic (Scene7), le composant doit être redimensionné pour s’adapter aux dimensions de la vidéo.

## Navigateur de contenu Dynamic Media Classic (Scene7) {#scene-content-browser}

Le navigateur de contenu Dynamic Media Classic (Scene7) vous permet d’afficher le contenu de Dynamic Media Classic (Scene7) directement dans Experience Manager. Pour accéder au navigateur de contenu, dans l’outil de recherche de contenu, sélectionnez **Dynamic Media Classic (Scene7)** dans l’interface utilisateur optimisée pour les écrans tactiles, ou l’icône **S7** dans l’interface utilisateur classique. La fonctionnalité est identique pour les deux interfaces utilisateur.

Si vous disposez de plusieurs configurations, Experience Manager affiche la [configuration par défaut](/help/sites-administering/scene7.md#configuring-a-default-configuration). Vous pouvez sélectionner différentes configurations directement dans le navigateur de contenu Dynamic Media Classic (Scene7), depuis le menu déroulant.

>[!NOTE]
>
>* Les ressources figurant dans le dossier à la demande n’apparaissent pas dans le navigateur de contenu Dynamic Media Classic (Scene7)
>* Lorsque l’[aperçu sécurisé est activé](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene), les ressources publiées dans Dynamic Media Classic (Scene7), tout comme les ressources dépubliées, apparaissent dans le navigateur de contenu de Dynamic Media Classic (Scene7).
>* Si **[!UICONTROL Dynamic Media Classic (Scene7)]** ou l’icône **[!UICONTROL S7]** n’apparaît pas comme option dans le navigateur de contenu, vous devez [configurer Dynamic Media Classic (Scene7) pour qu’il fonctionne avec Experience Manager](/help/sites-administering/scene7.md).
>* Pour la vidéo, le navigateur de contenu Dynamic Media Classic (Scene7) prend en charge :
>   * Les visionneuses de vidéos adaptatives : il s’agit de conteneurs de tous les rendus vidéo requis pour lire la vidéo sans difficultés sur plusieurs écrans.
>   * Vidéo MP4 unique
>   * Vidéo F4V unique

### Parcourir le contenu {#browsing-content-in-the-classic-ui}

Parcourez le contenu dans Dynamic Media Classic (Scene7) en sélectionnant l’onglet **[!UICONTROL S7]**.

Vous pouvez modifier la configuration à laquelle vous accédez en la sélectionnant. Les dossiers changent en fonction de la configuration sélectionnée.

![chlimage_1-64](assets/chlimage_1-64.png)

Comme avec l’outil de recherche de contenu pour les ressources, vous pouvez rechercher des ressources et filtrer les résultats. Toutefois, contrairement à l’outil de recherche de ressources, lorsque vous saisissez un mot-clé dans l’onglet **S7**, le nom du fichier **commence par** la chaîne que vous avez saisie, au lieu de **contenir** le mot-clé.

Par défaut, les ressources sont affichées par nom de fichier. Cependant, vous pouvez également filtrer les résultats par type de ressource.

>[!NOTE]
>
>Pour la vidéo, le navigateur de contenu Dynamic Media Classic (Scene7) de la gestion de contenu web prend en charge :
>
>* Les visionneuses de vidéos adaptatives : il s’agit de conteneurs de tous les rendus vidéo requis pour lire la vidéo sans difficultés sur plusieurs écrans.
>* Vidéo MP4 unique
>* Vidéo F4V unique
>

### Recherche de ressources Dynamic Media Classic (Scene7) avec le navigateur de contenu {#searching-for-scene-assets-with-the-content-browser}

La recherche de ressources Dynamic Media Classic (Scene7) est similaire à la recherche de ressources Experience Manager. La seule chose qui change est que lorsque vous effectuez une recherche, une vue distante des ressources s’affiche dans le système Dynamic Media Classic (Scene7), plutôt que d’avoir besoin de les importer directement dans Experience Manager.

Vous pouvez utiliser l’interface utilisateur classique ou l’interface utilisateur optimisée pour les écrans tactiles pour afficher et rechercher des ressources. Selon l’interface, la manière dont vous effectuez des recherches diffère légèrement.

Lors d’une recherche dans l’une ou l’autre des interfaces, vous pouvez filtrer selon les critères suivants (présentés ici dans l’interface utilisateur optimisée pour les écrans tactiles) :

**Entrez des mots-clés** - Vous pouvez rechercher des ressources par nom. Lors de la recherche par mots-clés, vous saisissez le début du nom du fichier. Par exemple, la saisie du mot « swimming » recherche tous les noms de fichier qui commencent par ces lettres, dans cet ordre. Veillez à sélectionner `Enter` après avoir tapé le terme de recherche de la ressource.

![chlimage_1-65](assets/chlimage_1-65.png)

**Dossier/chemin d’accès** - Le nom du dossier qui apparaît est basé sur la configuration que vous avez sélectionnée. Vous pouvez descendre vers des niveaux inférieurs en sélectionnant l’icône du dossier et en sélectionnant un sous-dossier, puis en sélectionnant la coche pour le sélectionner.

Si vous saisissez un mot-clé et sélectionnez un dossier, Experience Manager recherche dans ce dossier et tous les sous-dossiers. Néanmoins, si vous ne saisissez pas de mots-clés lors de la recherche, la sélection du dossier n’affiche que les éléments de ce dossier et n’inclut pas les sous-dossiers.

Par défaut, Experience Manager recherche le dossier sélectionné et tous les sous-dossiers.

![chlimage_1-66](assets/chlimage_1-66.png)

**Type de ressource** - Sélectionnez Dynamic Media Classic (Scene7) pour parcourir le contenu Dynamic Media Classic (Scene7). Cette option n’est disponible que si Dynamic Media Classic (Scene7) a été configuré.

![chlimage_1-67](assets/chlimage_1-67.png)

**Configuration** - Si plusieurs configurations de Dynamic Media Classic (Scene7) sont définies dans les services cloud, vous pouvez en sélectionner une ici. Par conséquent, le dossier change en fonction de la configuration choisie.

![chlimage_1-68](assets/chlimage_1-68.png)

**Type d’élément** - Dans le navigateur Dynamic Media Classic (Scene7), vous pouvez filtrer les résultats afin d’inclure les types d’élément suivants : images, modèles, vidéos et visionneuses de vidéos adaptables. Si vous ne sélectionnez aucun type de ressources, Experience Manager recherche par défaut tous les types de ressources.

![chlimage_1-69](assets/chlimage_1-69.png)

>[!NOTE]
>
>* Dans l’interface utilisateur classique, vous pouvez rechercher des éléments **Flash** et **FXG**. Le filtrage de ces deux éléments n’est pas pris en charge par l’interface utilisateur optimisée pour les écrans tactiles.
>
>* Lors de la recherche de vidéos, vous recherchez un seul rendu. Les résultats retournent le rendu d’origine (uniquement &#42;.mp4) et le rendu codé.
>* La recherche d’une visionneuse de vidéos adaptatives s’étend au dossier et à tous les sous-dossiers mais uniquement si vous avez ajouté un mot-clé à la recherche. Si vous n’avez pas ajouté de mot-clé, Experience Manager ne recherche pas les sous-dossiers.
>

**Statut de publication** - Vous pouvez filtrer les ressources selon leur statut de publication : Publiée ou Dépubliée. Si vous ne sélectionnez aucun statut de publication, Experience Manager recherche par défaut tous les statuts de publication.

![chlimage_1-70](assets/chlimage_1-70.png)
