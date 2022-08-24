---
title: Ajout de fonctionnalités Dynamic Media Classic (Scene7) à votre page
description: Adobe Dynamic Media Classic (Scene7) est une solution hébergée qui permet de gérer, d’améliorer, de publier et de diffuser des ressources multimédias enrichies sur le Web, les appareils mobiles, les e-mails et les appareils d’impression connectés à Internet.
uuid: dc463e2d-a452-490e-88af-f79bdaa3b089
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
discoiquuid: dc0191d0-f181-4e1e-b3f4-73427aa22073
docset: aem65
exl-id: bc9c864b-8bc3-42b4-ba25-6c5108be4f65
source-git-commit: f4b7566abfa0a8dbb490baa0e849de6c355a3f06
workflow-type: tm+mt
source-wordcount: '3511'
ht-degree: 22%

---

# Ajout de fonctionnalités Dynamic Media Classic (Scene7) à votre page{#adding-scene-features-to-your-page}

[Adobe Dynamic Media Classic (Scene7)](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/home.html) est une solution hébergée permettant de gérer, d’améliorer, de publier et de diffuser des ressources multimédias enrichies sur le Web, les appareils mobiles, les e-mails et les appareils d’impression connectés à Internet.

Vous pouvez afficher les ressources de Experience Manager publiées dans Dynamic Media Classic (Scene7) dans différentes visionneuses :

* Zoom
* Fenêtre déroulante
* Vidéo 
* Modèle d’image
* Image

Vous pouvez publier des ressources numériques directement depuis Experience Manager vers Dynamic Media Classic (Scene7) et vous pouvez publier des ressources numériques depuis Dynamic Media Classic (Scene7) vers Experience Manager.

Ce document décrit comment publier des ressources numériques de Experience Manager vers Dynamic Media Classic (Scene7) et inversement. Les visionneuses sont également décrites en détail. Pour plus d’informations sur la configuration de Experience Manager pour Dynamic Media Classic (Scene7), voir [Intégration de Dynamic Media Classic (Scene7) à Experience Manager](/help/sites-administering/scene7.md).

Voir aussi [Ajout de zones cliquables](/help/assets/image-maps.md).

Pour plus d’informations sur l’utilisation des composants vidéo avec Experience Manager, voir :

* [Vidéo ](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md)

>[!NOTE]
>
>Si les ressources Dynamic Media Classic (Scene7) ne s’affichent pas correctement, veillez à ce que Dynamic Media soit [disabled](/help/assets/config-dynamic.md#disabling-dynamic-media) puis actualisez la page.

## Publication manuelle dans Dynamic Media Classic (Scene7) à partir d’Assets {#manually-publishing-to-scene-from-assets}

Vous pouvez publier des ressources numériques dans Dynamic Media Classic (Scene7) à partir de la console Ressources de l’interface utilisateur classique ou directement à partir de la ressource.

>[!NOTE]
>
>Experience Manager publie sur Dynamic Media Classic (Scene7) de manière asynchrone. Après avoir sélectionné **[!UICONTROL Publier]**, la publication de votre ressource sur Dynamic Media Classic (Scene7) peut prendre plusieurs secondes.

### Publication depuis la console Ressources {#publishing-from-the-assets-console}

Vous pouvez effectuer une publication sur Dynamic Media Classic (Scene7) à partir de la console Ressources si les ressources se trouvent dans un dossier cible Dynamic Media Classic (Scene7).

1. Dans l’IU classique de Experience Manager, sélectionnez **[!UICONTROL Ressources numériques]** pour accéder au gestionnaire des ressources numériques.

1. Sélectionnez la ou les ressources ou le dossier dans le dossier cible que vous souhaitez publier dans Dynamic Media Classic (Scene7), cliquez avec le bouton droit de la souris et sélectionnez **[!UICONTROL Publication sur Dynamic Media Classic (Scene7)]**. Vous pouvez également sélectionner **[!UICONTROL Publication sur Dynamic Media Classic (Scene7)]** de la **[!UICONTROL Outils]** .

   ![chlimage_1-48](assets/chlimage_1-48.png)

1. Accédez à Dynamic Media Classic (Scene7) et vérifiez que les ressources sont disponibles.

   >[!NOTE]
   >
   >Si les ressources ne se trouvent pas dans un dossier synchronisé Dynamic Media Classic (Scene7), **[!UICONTROL Publication sur Dynamic Media Classic (Scene7)]** dans les deux menus est visible, mais désactivé.

### Publication à partir d’une ressource {#publishing-from-an-asset}

Vous pouvez publier manuellement une ressource tant qu’elle se trouve dans le dossier synchronisé Dynamic Media Classic (Scene7).

>[!NOTE]
>
>Si la ressource ne se trouve pas dans le dossier synchronisé de Dynamic Media Classic (Scene7), le lien vers **[!UICONTROL Publication sur Dynamic Media Classic (Scene7)]** n’apparaît pas.

Pour publier sur Dynamic Media Classic (Scene7) directement à partir d’une ressource numérique :

1. Dans Experience Manager, sélectionnez **[!UICONTROL Ressources numériques]** pour accéder au gestionnaire des ressources numériques.

1. Double-cliquez pour ouvrir un élément.

1. Dans le volet des détails de la ressource, sélectionnez **[!UICONTROL Publication sur Dynamic Media Classic (Scene7)]**.

   ![screen_shot_2012-02-22at34828pm](assets/screen_shot_2012-02-22at34828pm.png)

1. Le lien devient **[!UICONTROL Publication...]**, puis **[!UICONTROL Publié]**. Accédez à Dynamic Media Classic (Scene7) et vérifiez que la ressource est disponible.

   >[!NOTE]
   >
   >Si la ressource n’est pas publiée correctement dans Dynamic Media Classic (Scene7), le lien devient **[!UICONTROL Échec de la publication]**. Si la ressource a déjà été publiée sur Dynamic Media Classic (Scene7), le lien se lit comme suit : **[!UICONTROL Republication sur Dynamic Media Classic (Scene7)]**. La republication vous permet de modifier des ressources dans Experience Manager et de les republier.

### Publication de ressources à partir du dossier cible CQ {#publishing-assets-from-outside-the-cq-target-folder}

Adobe recommande de publier des ressources dans Dynamic Media Classic (Scene7) uniquement à partir des ressources du dossier cible Dynamic Media Classic (Scene7). Cependant, si vous devez charger des ressources à partir d’un dossier en dehors du dossier cible, vous pouvez toujours le faire en les chargeant dans un dossier à la demande sur Dynamic Media Classic (Scene7). Tout d’abord, configurez la configuration cloud de la page sur laquelle vous souhaitez que la ressource s’affiche. Vous ajoutez ensuite un composant Dynamic Media Classic (Scene7) à la page, puis faites glisser et déposez une ressource sur le composant. Une fois les propriétés de page définies pour cette page, une **[!UICONTROL Publication sur Dynamic Media Classic (Scene7)]** s’affiche lorsque ce lien est sélectionné, il déclenche le téléchargement vers Dynamic Media Classic (Scene7).

>[!NOTE]
>
>Les ressources qui se trouvent dans le dossier à la demande n’apparaissent pas dans l’explorateur de contenu Dynamic Media Classic (Scene7).

**Pour publier des ressources en dehors du dossier cible CQ :**

1. Dans Experience Manager de l’IU classique, sélectionnez **[!UICONTROL Sites web]** et accédez à la page web à laquelle vous souhaitez ajouter une ressource numérique qui n’est pas encore publiée sur Dynamic Media Classic (Scene7). (Les règles normales d’héritage de la page s’appliquent.)

1. Dans le sidekick, sélectionnez la variable **[!UICONTROL Page]** et sélectionnez **[!UICONTROL Propriétés de la page]**.

1. Sélectionner **[!UICONTROL Cloud Services]**.
1. Sélectionner **[!UICONTROL Ajout de services]**.
1. Sélectionner **[!UICONTROL Dynamic Media Classic (Scene7)]**.
1. Dans le **[!UICONTROL Adobe Dynamic Media Classic (Scene7)]** , sélectionnez la configuration souhaitée, puis **[!UICONTROL OK]**.

   ![chlimage_1-49](assets/chlimage_1-49.png)

1. Sur la page web, ajoutez un composant Dynamic Media Classic (Scene7) à l’emplacement souhaité sur la page.
1. Depuis l’outil de recherche de contenu, faites glisser un élément numérique vers le composant. Vous voyez un lien vers **[!UICONTROL Vérification de l’état de publication de Dynamic Media Classic (Scene7)]**.

   >[!NOTE]
   >
   >Si la ressource numérique se trouve dans le dossier cible CQ, aucun lien vers **[!UICONTROL Vérification de l’état de publication de Dynamic Media Classic (Scene7)]** apparaît. Les ressources sont placées dans le composant.

   ![chlimage_1-50](assets/chlimage_1-50.png)

1. Sélectionner **[!UICONTROL Vérification de l’état de publication de Dynamic Media Classic (Scene7)]**. Si les ressources ne sont pas publiées, Experience Manager les publie dans Dynamic Media Classic (Scene7). Une fois la ressource chargée, elle se trouve dans le dossier à la demande. Par défaut, le dossier à la demande se trouve dans la variable **[!UICONTROL name_of_the_company/CQ5_adhoc]**. Vous pouvez [configurer le dossier à la demande, le cas échéant ;](#configuringtheadhocfolder).

   >[!NOTE]
   >
   >Si la ressource ne se trouve pas dans un dossier synchronisé Dynamic Media Classic (Scene7) et qu’aucune configuration cloud Dynamic Media Classic (Scene7) n’est associée à la page active, le chargement échoue.

## Composants Dynamic Media Classic (Scene7) {#scene-components}

Les composants Dynamic Media Classic (Scene7) suivants sont disponibles dans Experience Manager :

* Zoom
* Fenêtre déroulante (Zoom)
* Modèle d’image
* Image
* Vidéo 

>[!NOTE]
>
>Ces composants ne sont pas disponibles par défaut et doivent être sélectionnés en mode de conception avant utilisation.

Une fois qu’elles sont disponibles en mode de conception, vous pouvez ajouter les composants à votre page comme tout autre composant de Experience Manager. Les ressources qui ne sont pas encore publiées sur Dynamic Media Classic (Scene7) sont publiées sur Dynamic Media Classic (Scene7) si elles se trouvent dans un dossier synchronisé, sur une page ou avec une configuration cloud Dynamic Media Classic (Scene7).

>[!NOTE]
>
>Si vous créez et développez des visionneuses S7 personnalisées et que vous utilisez l’outil de recherche de contenu, vous devez ajouter explicitement la variable `allowfullscreen` .

### Notification de fin de prise en charge de la visionneuse Flash {#flash-viewers-end-of-life-notice}

À compter du 31 janvier 2017, Adobe Dynamic Media Classic (Scene7) a officiellement arrêté la prise en charge de la plate-forme de la visionneuse Flash.

### Ajout d’un composant Dynamic Media Classic (Scene7) à une page {#adding-a-scene-component-to-a-page}

L’ajout d’un composant Dynamic Media Classic (Scene7) à une page est identique à l’ajout d’un composant à n’importe quelle page. Les composants Dynamic Media Classic (Scene7) sont décrits en détail dans les sections suivantes.

Pour ajouter un composant/une visionneuse Dynamic Media Classic (Scene7) à une page dans l’IU classique :

1. Dans Experience Manager, ouvrez la page dans laquelle vous souhaitez ajouter le composant Dynamic Media Classic (Scene7).

1. Si aucun composant Dynamic Media Classic (Scene7) n’est disponible, sélectionnez la règle dans le sidekick à saisir. **Conception** mode, sélectionnez **[!UICONTROL Modifier]** parsys, puis sélectionnez l’ensemble des **[!UICONTROL Dynamic Media Classic (Scene7)]** pour les rendre disponibles.

1. Revenir à **Modifier** en sélectionnant le crayon dans le sidekick.

1. Faites glisser un composant à partir du **[!UICONTROL Dynamic Media Classic (Scene7)]** Regroupez dans le sidekick la page à l’emplacement souhaité.

1. Sélectionner ***[!UICONTROL Modifier]** vous pouvez donc ouvrir le composant.

1. Modifiez le composant selon les besoins, puis sélectionnez **[!UICONTROL OK]** pour enregistrer les modifications.

### Ajout d’expériences d’affichage interactif à un site web réactif {#adding-interactive-viewing-experiences-to-a-responsive-website}

La conception réactive de vos ressources signifie que celles-ci s’adaptent en fonction de l’emplacement d’affichage. Avec la conception réactive, les mêmes éléments peuvent être affichés sur plusieurs appareils.

Pour ajouter une expérience de visionnage interactif à un site réactif par l’intermédiaire de l’interface utilisateur classique, procédez comme suit :

1. Connectez-vous à Experience Manager et assurez-vous d’avoir [Cloud Services Adobe Dynamic Media Classic (Scene7) configurés](/help/sites-administering/scene7.md#configuring-scene-integration) et que les composants Dynamic Media Classic (Scene7) sont disponibles.

   >[!NOTE]
   >
   >Si les composants WCM Dynamic Media Classic (Scene7) ne sont pas disponibles, veillez à les activer via le mode Conception.

1. Dans un site web où les composants Dynamic Media Classic (Scene7) sont activés, faites glisser un **[!UICONTROL Image]** de la page.
1. Modifiez le composant et ajustez les points d’arrêt dans le **[!UICONTROL Paramètres de Dynamic Media Classic (Scene7)]** .

   ![chlimage_1-51](assets/chlimage_1-51.png)

1. Confirmez que les visionneuses se redimensionnent de manière réactive et que toutes les interactions sont optimisées pour les ordinateurs de bureau, les tablettes et les appareils mobiles.

### Paramètres communs à tous les composants Dynamic Media Classic (Scene7) {#settings-common-to-all-scene-components}

Bien que les options de configuration varient, les éléments suivants sont communs à tous les composants Dynamic Media Classic (Scene7) :

* **Référence du fichier** : accédez à un fichier que vous souhaitez référencer. La référence au fichier affiche l’URL de la ressource et pas nécessairement l’URL complète de Dynamic Media Classic (Scene7), y compris les commandes et paramètres d’URL. Vous ne pouvez pas ajouter de commandes d’URL et de paramètres Dynamic Media Classic (Scene7) dans ce champ. Au lieu de cela, ils doivent être ajoutés par le biais de la fonctionnalité correspondante dans le composant.
* **Largeur** : permet de définir la largeur.
* **Hauteur** : permet de définir la hauteur.

Vous définissez ces options de configuration en ouvrant (en double-cliquant) un composant Dynamic Media Classic (Scene7), par exemple lorsque vous ouvrez une **Zoom** component :

![chlimage_1-52](assets/chlimage_1-52.png)

### Zoom {#zoom}

Le composant Zoom HTML5 affiche une image plus grande lorsque vous appuyez sur le bouton +.

L’élément comporte des outils de zoom dans sa partie inférieure. Sélectionner **[!UICONTROL +]** pour agrandir. Sélectionner **[!UICONTROL -]** pour réduire. En sélectionnant le **[!UICONTROL x]** ou la flèche de réinitialisation du zoom rétablit la taille d’origine de l’image importée. Sélectionnez les flèches diagonales pour faire en sorte qu’elles s’affichent en plein écran. Sélectionner **[!UICONTROL Modifier]** vous pouvez configurer le composant. Avec ce composant, vous pouvez configurer [paramètres communs à tous les composants Dynamic Media Classic (Scene7)](#settings-common-to-all-scene-components).

![](do-not-localize/chlimage_1-3.png)

### Fenêtre déroulante {#flyout}

Dans le composant Fenêtre déroulante HTML5, l’élément s’affiche sous la forme d’un écran partagé : à gauche se trouve l’élément à la taille spécifiée, à droite la partie sur laquelle le zoom a été effectué. Sélectionner **[!UICONTROL Modifier]** vous pouvez configurer le composant. Avec ce composant, vous pouvez configurer [paramètres communs à tous les composants Dynamic Media Classic (Scene7)](/help/sites-administering/scene7.md#settingscommontoallscene7components).

>[!NOTE]
>
>Si le composant Fenêtre déroulante utilise une taille personnalisée, cette taille personnalisée est utilisée et la configuration réactive du composant est désactivée.
>
>Si votre composant Fenêtre déroulante utilise la taille par défaut, comme définie dans la vue Conception, la taille par défaut est utilisée. Le composant s’étire pour s’adapter à la taille de la mise en page avec la configuration réactive du composant activée. Sachez toutefois qu’il existe une limitation de la configuration réactive du composant. Lorsque vous utilisez le composant Fenêtre déroulante avec une configuration réactive, vous ne devez pas l’utiliser avec l’extension de page entière. Dans le cas contraire, la fenêtre déroulante peut s’étendre au-delà de la bordure droite de la page.

![chlimage_1-53](assets/chlimage_1-53.png)

### Image {#image}

Le composant d’image Dynamic Media Classic (Scene7) vous permet d’ajouter une fonctionnalité Dynamic Media Classic (Scene7) à vos images, comme les modificateurs Dynamic Media Classic (Scene7), les paramètres d’image ou de visionneuse prédéfinis et l’accentuation. Le composant d’image Dynamic Media Classic (Scene7) est similaire aux autres composants d’image dans Experience Manager avec des fonctionnalités Dynamic Media Classic (Scene7) spéciales. Dans cet exemple, l’image a le modificateur d’URL Dynamic Media Classic (Scene7), `&op_invert=1` appliquée.

![](do-not-localize/chlimage_1-4.png)

**Titre, texte de remplacement** - Dans l’onglet Avancé , ajoutez un titre à l’image et un texte de remplacement pour les utilisateurs pour lesquels les graphiques sont désactivés.

**URL, Ouvrir dans** - Vous pouvez définir une ressource à partir de pour ouvrir un lien. Définissez l’URL, puis dans le champ Ouvrir dans, indiquez si vous souhaitez l’ouvrir dans la même fenêtre ou une nouvelle fenêtre.

![chlimage_1-54](assets/chlimage_1-54.png)

**Paramètre prédéfini de la visionneuse** - Sélectionnez un paramètre prédéfini de visionneuse existant dans le menu déroulant. Si le paramètre prédéfini de visionneuse que vous recherchez n’est pas visible, vous devez le rendre visible. Voir Gestion des paramètres prédéfinis de visionneuse. Si vous utilisez un paramètre prédéfini d’image, vous ne pouvez pas sélectionner de paramètre prédéfini de visionneuse, et inversement.

**Configuration de Dynamic Media Classic (Scene7)** - Sélectionnez la configuration Dynamic Media Classic (Scene7) que vous souhaitez utiliser pour récupérer les paramètres d’image prédéfinis principaux à partir de SPS.

**Paramètre d’image prédéfini** - Sélectionnez un paramètre d’image prédéfini existant dans le menu déroulant. Si le paramètre d’image prédéfini que vous recherchez n’est pas visible, vous devez le rendre visible. Voir Gestion des paramètres d’image prédéfinis. Si vous utilisez un paramètre prédéfini d’image, vous ne pouvez pas sélectionner de paramètre prédéfini de visionneuse, et inversement.

**Format de sortie** - Sélectionnez le format de sortie de l’image, par exemple jpeg. Selon le format de sortie que vous sélectionnez, vous pouvez ajouter des options de configuration supplémentaires. Voir Bonnes pratiques relatives aux paramètres d’image prédéfinis.

**Accentuation** - Sélectionnez le mode d’accentuation de l’image. L’accentuation est expliquée en détails dans les rubriques Bonnes pratiques relatives aux paramètres d’image prédéfinis et Bonnes pratiques relatives à l’accentuation.

**Modificateurs d’URL** - Vous pouvez modifier les effets d’image en fournissant des commandes d’image S7 supplémentaires. Ces commandes sont décrites dans la section Paramètres d’image prédéfinis et la référence des commandes.

**Points d’arrêt** - Si votre site web est réactif, vous souhaitez ajuster les points d’arrêt. Les points d’arrêt doivent être séparés par des virgules (,).

### Modèle d’image {#image-template}

Les modèles d’image Dynamic Media Classic (Scene7) sont du contenu Photoshop superposé qui a été importé dans Dynamic Media Classic (Scene7), où le contenu et les propriétés ont été paramétrés pour la variabilité. Le **[!UICONTROL Modèle d’image]** permet d’importer des images et de modifier dynamiquement le texte en Experience Manager. En outre, vous pouvez configurer le composant **[!UICONTROL Modèle d’image]** afin d’utiliser des valeurs provenant de ClientContext de sorte que chaque utilisateur voit l’image d’une manière personnalisée.

Sélectionner **[!UICONTROL Modifier]** - pour configurer le composant. Vous pouvez configurer [paramètres communs à tous les composants Dynamic Media Classic (Scene7)](/help/sites-administering/scene7.md#settingscommontoallscene7components) et d’autres paramètres décrits dans cette section.

![chlimage_1-55](assets/chlimage_1-55.png)

**Référence du fichier, Largeur, Hauteur** - Voir [paramètres communs à tous les composants Dynamic Media Classic (Scene7)](/help/sites-administering/scene7.md#settingscommontoallscene7components).

>[!NOTE]
>
>Les commandes et paramètres d’URL de Dynamic Media Classic (Scene7) ne peuvent pas être ajoutés directement à l’URL de référence du fichier. Ils ne peuvent être définis que dans l’interface utilisateur du composant, dans le panneau **[!UICONTROL Paramètre]**.

**Titre, texte de remplacement** - Dans l’onglet Modèle d’image Dynamic Media Classic (Scene7) , ajoutez un titre à l’image et un texte de remplacement pour les utilisateurs pour lesquels les graphiques sont désactivés.

**URL, Ouvrir dans** - Vous pouvez définir une ressource à partir de pour ouvrir un lien. Définissez l’URL, puis dans le champ Ouvrir dans, indiquez si vous souhaitez l’ouvrir dans la même fenêtre ou une nouvelle fenêtre.

![chlimage_1-56](assets/chlimage_1-56.png)

**Panneau de paramètres** - Lors de l’importation d’une image, les paramètres sont prérenseignés avec les informations de l’image. En l’absence de contenu pouvant être modifié dynamiquement, cette fenêtre est vide.

![chlimage_1-57](assets/chlimage_1-57.png)

#### Modification dynamique du texte {#changing-text-dynamically}

Pour modifier dynamiquement le texte, saisissez le nouveau texte dans les champs et sélectionnez **[!UICONTROL OK]**. Dans cet exemple, le **Prix** est désormais de 50 $ et l’expédition de 99 cents.

![chlimage_1-58](assets/chlimage_1-58.png)

Le texte de l’image change. Vous pouvez rétablir la valeur d’origine du texte en sélectionnant **[!UICONTROL Réinitialiser]** en regard du champ .

![chlimage_1-59](assets/chlimage_1-59.png)

#### Modifier le texte pour refléter la valeur d’une valeur ClientContext {#changing-text-to-reflect-the-value-of-a-client-context-value}

Pour lier un champ à une valeur de contexte client, sélectionnez **[!UICONTROL Sélectionner]** pour ouvrir le menu client-context, sélectionnez le contexte client, puis sélectionnez **[!UICONTROL OK]**. Dans cet exemple, le nom change selon la liaison entre le Nom et le nom formaté du profil.

![chlimage_1-60](assets/chlimage_1-60.png)

Le texte reflète le nom de l’utilisateur actuellement connecté. Vous pouvez rétablir la valeur d’origine du texte en sélectionnant **[!UICONTROL Réinitialiser]** en regard du champ .

![chlimage_1-61](assets/chlimage_1-61.png)

#### Faire du modèle d’image Dynamic Media Classic (Scene7) un lien {#making-the-scene-image-template-a-link}

Vous pouvez faire du composant de modèle d’image Dynamic Media Classic (Scene7) un lien cliquable.

1. Sur la page contenant le composant de modèle d’image Dynamic Media Classic (Scene7), sélectionnez **[!UICONTROL Modifier]**.
1. Dans le champ **[!UICONTROL URL]**, saisissez l’URL à laquelle l’utilisateur accède lorsqu’il clique sur l’image. Dans le champ **[!UICONTROL Ouvrir dans]**, choisissez où vous souhaitez que la cible s’ouvre (une nouvelle fenêtre ou la même fenêtre).

   ![chlimage_1-62](assets/chlimage_1-62.png)

1. **[!UICONTROL Cliquez sur OK]**.

### Composant vidéo {#video-component}

Dynamic Media Classic (Scene7) **[!UICONTROL Vidéo]** Le composant (disponible à partir de la section Dynamic Media Classic (Scene7) du sidekick) utilise la détection de l’appareil et de la bande passante pour diffuser la vidéo appropriée à chaque écran. Ce composant est un lecteur vidéo HTML5. Il s’agit d’une visionneuse unique pouvant être utilisée sur plusieurs canaux.

Il peut être utilisé pour des ensembles de vidéos adaptables, une vidéo MP4 unique ou une vidéo F4V unique.

Voir [Vidéo](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md) pour plus d’informations sur le fonctionnement des vidéos avec l’intégration de Dynamic Media Classic (Scene7). En outre, voir comment [la valeur **Vidéo Dynamic Media Classic (Scene7)** compare le composant à la base ; **video** component](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md).

![chlimage_1-63](assets/chlimage_1-63.png)

### Limitations connues du composant vidéo {#known-limitations-for-the-video-component}

Adobe DAM et WCM indiquent si une vidéo source Principale est téléchargée. Elles n’affichent pas les éléments proxy suivants :

* Rendus codés Dynamic Media Classic (Scene7)
* Visionneuses de vidéos adaptatives Dynamic Media Classic (Scene7)

Lors de l’utilisation d’une visionneuse de vidéos adaptative avec le composant vidéo Dynamic Media Classic (Scene7), le composant doit être redimensionné pour s’adapter aux dimensions de la vidéo.

## Explorateur de contenu Dynamic Media Classic (Scene7) {#scene-content-browser}

L’explorateur de contenu Dynamic Media Classic (Scene7) vous permet d’afficher le contenu de Dynamic Media Classic (Scene7) directement dans Experience Manager. Pour accéder à l’explorateur de contenu, dans l’outil de recherche de contenu, sélectionnez **Dynamic Media Classic (Scene7)** dans l’interface utilisateur optimisée pour les écrans tactiles ou la fonction **S7** dans l’interface utilisateur classique. La fonctionnalité est identique pour les deux interfaces utilisateur.

Si vous avez plusieurs configurations, Experience Manager affiche par défaut la variable [configuration par défaut](/help/sites-administering/scene7.md#configuring-a-default-configuration). Vous pouvez sélectionner différentes configurations directement dans l’explorateur de contenu Dynamic Media Classic (Scene7) du menu déroulant.

>[!NOTE]
>
>* Les ressources figurant dans le dossier à la demande n’apparaissent pas dans le navigateur de contenu Dynamic Media Classic (Scene7).
>* When [L’aperçu sécurisé est activé](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene), les ressources publiées et non publiées sur Dynamic Media Classic (Scene7) n’apparaissent pas dans le navigateur de contenu Dynamic Media Classic (Scene7).
>* Si vous ne voyez pas **[!UICONTROL Dynamic Media Classic (Scene7)]** ou le **[!UICONTROL S7]** comme option dans l’explorateur de contenu, vous devez [configurer Dynamic Media Classic (Scene7) pour qu’il fonctionne avec Experience Manager](/help/sites-administering/scene7.md).
>* Pour la vidéo, le navigateur de contenu Dynamic Media Classic (Scene7) prend en charge :
   >   * Les ensembles de vidéos adaptables. Il s’agit de conteneurs de tous les rendus vidéo requis pour lire la vidéo sans difficultés sur plusieurs écrans.
   >   * La vidéo MP4 unique
   >   * Vidéo F4V simple


### Parcourir le contenu {#browsing-content-in-the-classic-ui}

Parcourez le contenu dans Dynamic Media Classic (Scene7) en sélectionnant le **[!UICONTROL S7]** .

Vous pouvez modifier la configuration à laquelle vous accédez en la sélectionnant. Les dossiers changent en fonction de la configuration que vous sélectionnez.

![chlimage_1-64](assets/chlimage_1-64.png)

Comme avec l’outil de recherche de contenu des ressources, vous pouvez effectuer une rechercher des éléments et filtrer les résultats. Néanmoins, à la différence de l’outil de recherche de contenu des ressources, lors de la saisie d’un mot-clé dans l’onglet **S7**, le nom du fichier **commence par** la chaîne que vous avez saisie au lieu de **contenir** le mot-clé.

Par défaut, les éléments sont affichés par nom de fichier. Cependant, vous pouvez également filtrer les résultats par type de ressource.

>[!NOTE]
>
>Pour la vidéo, le navigateur de contenu Dynamic Media Classic (Scene7) de la gestion de contenu web prend en charge :
>
>* Les ensembles de vidéos adaptables. Il s’agit de conteneurs de tous les rendus vidéo requis pour lire la vidéo sans difficultés sur plusieurs écrans.
>* La vidéo MP4 unique
>* Vidéo F4V simple
>


### Recherche de ressources Dynamic Media Classic (Scene7) avec l’explorateur de contenu {#searching-for-scene-assets-with-the-content-browser}

La recherche de ressources Dynamic Media Classic (Scene7) est similaire à la recherche de ressources Experience Manager. L’exception est que lorsque vous effectuez une recherche, une vue distante des ressources s’affiche dans le système Dynamic Media Classic (Scene7), plutôt que de les importer directement dans Experience Manager.

Vous pouvez utiliser l’interface utilisateur classique ou l’interface utilisateur optimisée pour les écrans tactiles pour visualiser et rechercher des éléments. Selon l’interface, le mode de recherche est légèrement différent.

Lors d’une recherche dans l’une ou l’autre des interfaces, vous pouvez filtrer selon les critères suivants (présentés ici dans l’interface utilisateur optimisée pour les écrans tactiles) :

**Entrez des mots-clés** - Vous pouvez rechercher des ressources par nom. Lors de la recherche de mots-clés, vous saisissez le nom du fichier. Par exemple, la saisie du mot « swimming » recherche tous les noms de fichier qui commencent par ces lettres, dans cet ordre. Veillez à sélectionner Entrée une fois le terme saisi pour rechercher la ressource.

![chlimage_1-65](assets/chlimage_1-65.png)

**Dossier/chemin** - Le nom du dossier est basé sur la configuration que vous avez sélectionnée. Vous pouvez descendre jusqu’à des niveaux inférieurs en sélectionnant l’icône de dossier et en sélectionnant un sous-dossier, puis en cochant la coche pour le sélectionner.

Si vous saisissez un mot-clé et sélectionnez un dossier, le Experience Manager recherche ce dossier et les sous-dossiers appropriés. Toutefois, si vous ne saisissez aucun mot-clé lors de la recherche, la sélection du dossier affiche uniquement les ressources contenues dans ce dossier et n’inclut aucun sous-dossier.

Par défaut, Experience Manager recherche le dossier sélectionné et tous les sous-dossiers.

![chlimage_1-66](assets/chlimage_1-66.png)

**Type de ressource** - Sélectionnez Dynamic Media Classic (Scene7) pour parcourir le contenu Dynamic Media Classic (Scene7). Cette option n’est disponible que si Dynamic Media Classic (Scene7) a été configuré.

![chlimage_1-67](assets/chlimage_1-67.png)

**Configuration** - Si plusieurs configurations Dynamic Media Classic (Scene7) sont définies en Cloud Services, vous pouvez les sélectionner ici. Par conséquent, le dossier change en fonction de la configuration choisie.

![chlimage_1-68](assets/chlimage_1-68.png)

**Type de ressource** - Dans le navigateur Dynamic Media Classic (Scene7), vous pouvez filtrer les résultats de manière à inclure l’un des éléments suivants : images, modèles, vidéos et ensembles de vidéos adaptatifs. Si vous ne sélectionnez aucun type de ressource, Experience Manager recherche par défaut tous les types de ressource.

![chlimage_1-69](assets/chlimage_1-69.png)

>[!NOTE]
>
>* Dans l’interface utilisateur classique, vous pouvez rechercher des éléments **Flash** et **FXG**. Le filtrage de ces deux termes dans l’IU optimisée pour les écrans tactiles n’est pas pris en charge.
>
>* Lors de la recherche de vidéos, vous recherchez un seul rendu. Les résultats renvoient le rendu d’origine (uniquement &#42;.mp4) et le rendu codé.
>* Lors de la recherche d’une visionneuse de vidéos adaptative, vous effectuez une recherche dans le dossier et tous les sous-dossiers, mais uniquement si vous avez ajouté un mot-clé à la recherche. Si vous n’avez pas ajouté de mot-clé, Experience Manager ne recherche pas les sous-dossiers.
>


**État de publication** - Vous pouvez filtrer les ressources en fonction de l’état de publication : Publication annulée ou publication. Si vous ne sélectionnez aucun état de publication, Experience Manager recherche par défaut tous les états de publication.

![chlimage_1-70](assets/chlimage_1-70.png)
