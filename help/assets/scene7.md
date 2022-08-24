---
title: Ajout de fonctionnalités Dynamic Media Classic aux pages
description: Comment ajouter des fonctionnalités et des composants Dynamic Media Classic à une page dans Adobe Experience Manager.
uuid: aa5a4735-bfec-43b8-aec0-a0c32bff134f
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
topic-tags: managing-assets
discoiquuid: e7b95732-a571-48e8-afad-612059cdbde7
feature: Dynamic Media Classic
role: User, Admin
mini-toc-levels: 3
exl-id: 815f577d-4774-4830-8baf-0294bd085b83
source-git-commit: d947bd98b3a0f6fd79cde5b5b2fca23487077da3
workflow-type: tm+mt
source-wordcount: '2845'
ht-degree: 22%

---

# Ajout de fonctionnalités Dynamic Media Classic aux pages {#adding-scene-features-to-your-page}

[Adobe Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/home.html) est une solution hébergée permettant de gérer, d’améliorer, de publier et de diffuser des ressources multimédias enrichies sur le Web, les appareils mobiles, les e-mails et les appareils d’impression connectés à Internet.

Vous pouvez afficher les ressources de Experience Manager publiées dans Dynamic Media Classic dans différentes visionneuses :

* Zoom
* Fenêtre déroulante
* Vidéo 
* Modèle d’image
* Image

Vous pouvez publier des ressources numériques directement depuis Experience Manager vers Dynamic Media Classic et vous pouvez les publier depuis Dynamic Media Classic vers Experience Manager.

Ce document décrit comment publier des ressources numériques de Experience Manager vers Dynamic Media Classic et inversement. Les visionneuses sont également décrites en détail. Pour plus d’informations sur la configuration de Experience Manager pour Dynamic Media Classic, voir [Intégration de Dynamic Media Classic à Experience Manager](/help/sites-administering/scene7.md).

Voir aussi [Ajout de zones cliquables](image-maps.md).

Pour plus d’informations sur l’utilisation des composants vidéo avec Experience Manager, voir [Vidéo](video.md).

>[!NOTE]
>
>Si les ressources Dynamic Media Classic ne s’affichent pas correctement, assurez-vous que Dynamic Media est [disabled](config-dynamic.md#disabling-dynamic-media) puis actualisez la page.

## Publication manuelle dans Dynamic Media Classic à partir de ressources {#manually-publishing-to-scene-from-assets}

Vous pouvez publier des ressources numériques dans Dynamic Media Classic comme suit :

* [Dans l’interface utilisateur classique de la console Ressources](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-from-the-assets-console)
* [Dans l’interface utilisateur classique d’une ressource](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-from-an-asset)
* [Dans l’interface utilisateur classique en dehors du dossier cible CQ](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-assets-from-outside-the-cq-target-folder)

>[!NOTE]
>
>Experience Manager publie sur Dynamic Media Classic de manière asynchrone. Après avoir sélectionné **[!UICONTROL Publier]**, la publication de la ressource sur Dynamic Media Classic prend plusieurs secondes.

## Composants Dynamic Media Classic {#scene-components}

Les composants Dynamic Media Classic suivants sont disponibles dans Experience Manager :

* Zoom
* Fenêtre déroulante (Zoom)
* Modèle d’image
* Image
* Vidéo 

>[!NOTE]
>
>Ces composants ne sont pas disponibles par défaut et doivent être sélectionnés dans **[!UICONTROL Conception]** avant d’utiliser .

Une fois qu’elles sont disponibles dans **[!UICONTROL Conception]** , vous pouvez ajouter les composants à votre page comme tout autre composant de Experience Manager. Les ressources qui n’ont pas encore été publiées sur Dynamic Media Classic le sont sur Dynamic Media Classic si elles se trouvent dans un dossier synchronisé, sur une page ou avec une configuration cloud Dynamic Media Classic.

>[!NOTE]
>
>Si vous créez et développez des visionneuses personnalisées et que vous utilisez l’outil de recherche de contenu, vous devez ajouter explicitement la variable `allowfullscreen` .

### Notification de fin de prise en charge de la visionneuse Flash {#flash-viewers-end-of-life-notice}

À compter du 31 janvier 2017, Adobe Dynamic Media Classic a arrêté la prise en charge de la plate-forme de la visionneuse de Flashs.

### Ajout d’un composant Dynamic Media Classic (Scene7) à une page {#adding-a-scene-component-to-a-page}

L’ajout d’un composant Dynamic Media Classic (Scene7) à une page est identique à l’ajout d’un composant à n’importe quelle page. Les composants Dynamic Media Classic sont décrits en détail dans les sections suivantes.

**Pour ajouter un composant Dynamic Media Classic (Scene7) à une page :**

1. Dans Experience Manager, ouvrez la page dans laquelle vous souhaitez ajouter le **[!UICONTROL Dynamic Media Classic (Scene7)]** composant.

1. Si aucun composant Dynamic Media Classic n’est disponible, sélectionnez **[!UICONTROL Conception]** mode, sélectionnez un composant avec une bordure bleue, puis sélectionnez **[!UICONTROL Parent]** , puis le **[!UICONTROL Configuration]** icône . Dans **[!UICONTROL Parsys (Design)]**, sélectionnez tous les composants Dynamic Media Classic pour les rendre disponibles, puis sélectionnez **[!UICONTROL OK]**.

   ![chlimage_1-224](assets/chlimage_1-224.png)

1. Sélectionner **[!UICONTROL Modifier]** pour que vous puissiez revenir à **[!UICONTROL Modifier]** mode .

1. Faites glisser un composant du groupe Dynamic Media Classic du sidekick vers la page à l’emplacement souhaité.

1. Sélectionnez la **[!UICONTROL Configuration]** pour ouvrir le composant.

1. Modifiez le composant selon les besoins, puis sélectionnez **[!UICONTROL OK]** pour enregistrer les modifications.
1. Faites glisser l’image ou la vidéo de l’explorateur de contenu vers le composant Dynamic Media Classic que vous avez ajouté à la page.

   >[!NOTE]
   >
   >Dans l’interface utilisateur tactile uniquement, vous devez faire glisser l’image ou la vidéo sur le composant Dynamic Media Classic que vous avez placé sur la page. La sélection et la modification du composant Dynamic Media Classic, puis le choix de la ressource ne sont pas pris en charge.

### Ajout d’une expérience de visionnage interactif à un site réactif {#adding-interactive-viewing-experiences-to-a-responsive-website}

La conception réactive de vos ressources signifie que votre ressource s’adapte en fonction de l’endroit où elle s’affiche. Avec la conception réactive, les mêmes éléments peuvent être affichés sur plusieurs appareils.

Voir aussi [Conception réactive pour les pages web](/help/sites-developing/responsive.md).

**Pour ajouter une expérience de visionnage interactif à un site réactif :**

1. Connectez-vous à Experience Manager et assurez-vous d’avoir [Cloud Services Adobe Dynamic Media Classic configurés](/help/sites-administering/scene7.md#configuring-scene-integration) et que les composants Dynamic Media Classic sont disponibles.

   >[!NOTE]
   >
   >Si les composants Dynamic Media Classic ne sont pas disponibles, veillez à [pour les activer au moyen du mode Conception](/help/sites-authoring/default-components-designmode.md).

1. Dans un site web avec la variable **[!UICONTROL Dynamic Media Classic]** composants activés, faites glisser un **[!UICONTROL Image]** du composant à la page.
1. Sélectionnez le composant et cliquez sur l’icône de configuration.
1. Dans le **[!UICONTROL Paramètres Dynamic Media Classic]** ajustez les points d’arrêt.

   ![chlimage_1-225](assets/chlimage_1-225.png)

1. Confirmez que les visionneuses se redimensionnent de manière réactive et que toutes les interactions sont optimisées pour les ordinateurs de bureau, les tablettes et les appareils mobiles.

### Paramètres communs à tous les composants Dynamic Media Classic {#settings-common-to-all-scene-components}

Bien que les options de configuration varient, les éléments suivants sont communs à tous les [!UICONTROL Dynamic Media Classic] composants :

* **[!UICONTROL Référence du fichier]** : accédez à un fichier que vous souhaitez référencer. La référence au fichier affiche l’URL de la ressource et pas nécessairement l’URL Dynamic Media Classic complète, y compris les commandes et paramètres d’URL. Vous ne pouvez pas ajouter de commandes d’URL et de paramètres Dynamic Media Classic dans ce champ. Au lieu de cela, vous pouvez les ajouter via la fonctionnalité correspondante dans le composant.
* **[!UICONTROL Largeur]** : permet de définir la largeur.
* **[!UICONTROL Hauteur]** : permet de définir la hauteur.

Vous définissez ces options de configuration en ouvrant (en double-cliquant) un composant Dynamic Media Classic, par exemple, lorsque vous ouvrez une **[!UICONTROL Zoom]** component :

![chlimage_1-226](assets/chlimage_1-226.png)

### Zoom {#zoom}

Le composant Zoom HTML5 affiche une image plus grande lorsque vous appuyez sur la touche **[!UICONTROL +]** bouton .

L’élément comporte des outils de zoom dans sa partie inférieure. Sélectionner **[!UICONTROL +]** si vous souhaitez agrandir ; select **[!UICONTROL -]** si vous voulez réduire. Appuyez sur le bouton **[!UICONTROL x]** ou la flèche de réinitialisation du zoom rétablit la taille d’origine de l’image importée. Sélectionnez les flèches diagonales pour qu’elles s’affichent en plein écran. Sélectionner **[!UICONTROL Modifier]** vous pouvez configurer le composant. Avec ce composant, vous pouvez configurer [paramètres communs à tous [!UICONTROL Dynamic Media Classic] components](#settings-common-to-all-scene-components).

![chlimage_1-227](/help/assets/assets/do-not-localize/chlimage_1-227.png)

### Fenêtre déroulante {#flyout}

Dans le HTML5 **[!UICONTROL Fenêtre déroulante]** , la ressource s’affiche sous la forme d’un écran partagé ; laissait la ressource à la taille spécifiée ; la partie zoom s’affiche à droite. Sélectionner **[!UICONTROL Modifier]** vous pouvez configurer le composant. Avec ce composant, vous pouvez configurer [paramètres communs à tous les composants Dynamic Media Classic](#settings-common-to-all-scene-components).

>[!NOTE]
>
>Si votre **[!UICONTROL Fenêtre déroulante]** utilise une taille personnalisée, puis cette taille personnalisée est utilisée et la configuration réactive du composant est désactivée.
>
>Si votre **[!UICONTROL Fenêtre déroulante]** utilise la taille par défaut, comme défini dans **[!UICONTROL Vue de conception]**, la taille par défaut est utilisée et le composant s’étire pour s’adapter à la taille de mise en page avec la configuration réactive du composant activée. La configuration réactive du composant est limitée. Lorsque vous utilisez la variable **[!UICONTROL Fenêtre déroulante]** avec une configuration réactive, ne l’utilisez pas avec l’étirement de page complète. Sinon, la variable **[!UICONTROL Fenêtre déroulante]** s’étend au-delà de la bordure droite de la page.

![chlimage_1-228](assets/chlimage_1-228.png)

### Image {#image}

Dynamic Media Classic **[!UICONTROL Image]** vous permet d’ajouter des fonctionnalités Dynamic Media Classic à vos images, telles que les modificateurs Dynamic Media Classic, les paramètres d’image ou de visionneuse prédéfinis et l’accentuation. Dynamic Media Classic **[!UICONTROL Image]** est similaire aux autres composants d’image dans Experience Manager avec des fonctionnalités Dynamic Media Classic spéciales. Dans cet exemple, l’image a le modificateur URL Dynamic Media Classic, `&op_invert=1` appliquée.

![chlimage_1-229](assets/chlimage_1-229.png)

**[!UICONTROL Titre, texte de remplacement]** - Dans le **[!UICONTROL Avancé]** ajoutez un titre à l’image et un texte de remplacement pour les utilisateurs pour lesquels les graphiques sont désactivés.

**[!UICONTROL URL, Ouvrir dans]** - Vous pouvez définir une ressource à partir de pour ouvrir un lien. Définissez l’**[!UICONTROL URL]**, puis dans le champ **[!UICONTROL Ouvrir dans]**, indiquez si vous souhaitez l’ouvrir dans la même fenêtre ou une nouvelle fenêtre.

![chlimage_1-230](assets/chlimage_1-230.png)

**[!UICONTROL Paramètre prédéfini de la visionneuse]** - Sélectionnez un paramètre prédéfini de visionneuse existant dans le menu déroulant. Si le paramètre prédéfini de visionneuse que vous recherchez n’est pas visible, vous devez le rendre visible. Voir [Gestion des paramètres prédéfinis de visionneuse](/help/assets/managing-viewer-presets.md). Si vous utilisez un paramètre prédéfini d’image, vous ne pouvez pas sélectionner de paramètre prédéfini de visionneuse, et inversement.

**[!UICONTROL Configuration Dynamic Media Classic]** - Sélectionnez la configuration Dynamic Media Classic que vous souhaitez utiliser pour récupérer les paramètres d’image prédéfinis principaux à partir de SPS.

**[!UICONTROL Paramètre d’image prédéfini]** - Sélectionnez un paramètre d’image prédéfini existant dans le menu déroulant. Si le paramètre d’image prédéfini que vous recherchez n’est pas visible, vous devez le rendre visible. Voir [Gestion des paramètres d’image prédéfinis](/help/assets/managing-image-presets.md). Si vous utilisez un paramètre prédéfini d’image, vous ne pouvez pas sélectionner de paramètre prédéfini de visionneuse, et inversement.

**[!UICONTROL Format de sortie]** - Sélectionnez le format de sortie de l’image, par exemple jpeg. Selon le format de sortie que vous sélectionnez, d’autres options de configuration sont disponibles. Voir [Bonnes pratiques relatives aux paramètres d’image prédéfinis](/help/assets/managing-image-presets.md#image-preset-options).

**[!UICONTROL Accentuation]** - Sélectionnez le mode d’accentuation de l’image. L’accentuation est expliquée en détails dans les rubriques [Bonnes pratiques relatives aux paramètres d’image prédéfinis](/help/assets/managing-image-presets.md#image-preset-options) et [Bonnes pratiques relatives à l’accentuation](/help/assets/assets/sharpening_images.pdf).

**[!UICONTROL Modificateurs d’URL]** - Vous pouvez modifier les effets d’image en fournissant des commandes d’image Dynamic Media Classic supplémentaires. Ces commandes sont décrites dans la section [Paramètres d’image prédéfinis](/help/assets/managing-image-presets.md) et le [Référence de commande](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html?lang=fr).

**[!UICONTROL Points d’arrêt]** - Si votre site web est réactif, vous souhaitez ajuster les points d’arrêt. Les points d’arrêt doivent être séparés par des virgules ( , ).

### Modèle d’image {#image-template}

[Modèles d’image Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/template-basics/quick-start-template-basics.html) sont du contenu Photoshop superposé importé dans Dynamic Media Classic, où le contenu et les propriétés ont été paramétrés pour la variabilité. Le **[!UICONTROL Modèle d’image]** permet d’importer des images et de modifier dynamiquement le texte en Experience Manager. En outre, vous pouvez configurer le composant **[!UICONTROL Modèle d’image]** afin d’utiliser des valeurs provenant de ClientContext de sorte que chaque utilisateur voit l’image d’une manière personnalisée.

Sélectionner **[!UICONTROL Modifier]** si vous souhaitez configurer le composant. Vous pouvez configurer [paramètres communs à tous les composants Dynamic Media Classic](#settings-common-to-all-scene-components) et d’autres paramètres décrits dans cette section.

![chlimage_1-231](assets/chlimage_1-231.png)

**[!UICONTROL Référence du fichier, Largeur, Hauteur]** - Voir les paramètres communs à tous les composants ScDynamic Media Classic7.

>[!NOTE]
>
>Les commandes et paramètres d’URL Dynamic Media Classic ne peuvent pas être ajoutés directement à l’URL de référence du fichier. Ils ne peuvent être définis que dans l’interface utilisateur du composant, dans le panneau **[!UICONTROL Paramètre]**.

**[!UICONTROL Titre, texte de remplacement]** - Dans l’onglet Modèle d’image Dynamic Media Classic , ajoutez un titre à l’image et un texte de remplacement pour les utilisateurs pour lesquels les graphiques sont désactivés.

**[!UICONTROL URL, Ouvrir dans]** - Vous pouvez définir une ressource à partir de pour ouvrir un lien. Définissez l’URL, puis dans le champ Ouvrir dans, indiquez si vous souhaitez l’ouvrir dans la même fenêtre ou une nouvelle fenêtre.

![chlimage_1-232](assets/chlimage_1-232.png)

**[!UICONTROL Panneau de paramètres]** - Lors de l’importation d’une image, les paramètres sont prérenseignés avec les informations de l’image. En l’absence de contenu pouvant être modifié dynamiquement, cette fenêtre est vide.

![chlimage_1-233](assets/chlimage_1-233.png)

#### Modifier le texte de manière dynamique {#changing-text-dynamically}

Pour modifier dynamiquement le texte, saisissez le nouveau texte dans les champs et sélectionnez **[!UICONTROL OK]**. Dans cet exemple, le **[!UICONTROL Prix]** est désormais de 50 $ et l’expédition de 99 cents.

![chlimage_1-234](assets/chlimage_1-234.png)

Le texte de l’image change. Vous pouvez rétablir la valeur d’origine du texte en appuyant sur **[!UICONTROL Réinitialiser]** en regard du champ .

![chlimage_1-235](assets/chlimage_1-235.png)

#### Modifier le texte pour refléter la valeur d’une valeur ClientContext {#changing-text-to-reflect-the-value-of-a-client-context-value}

Pour lier un champ à une valeur de contexte client, sélectionnez **[!UICONTROL Sélectionner]** pour ouvrir le menu client-context, sélectionnez le contexte client, puis sélectionnez **[!UICONTROL OK]**. Dans cet exemple, le nom change selon la liaison entre le Nom et le nom formaté du profil.

![chlimage_1-236](assets/chlimage_1-236.png)

Le texte reflète le nom de l’utilisateur actuellement connecté. Vous pouvez réinitialiser le texte sur la valeur d’origine en cliquant sur **[!UICONTROL Réinitialiser]** en regard du champ.

![chlimage_1-237](assets/chlimage_1-237.png)

#### Faire du modèle d’image Dynamic Media Classic un lien {#making-the-scene-image-template-a-link}

1. Sur la page avec Dynamic Media Classic **[!UICONTROL Modèle d’image]** component, select **[!UICONTROL Modifier]**.
1. Dans le **[!UICONTROL URL]** , saisissez l’URL à laquelle les utilisateurs accèdent lorsqu’ils cliquent sur l’image. Dans le champ **[!UICONTROL Ouvrir dans]**, choisissez où vous souhaitez que la cible s’ouvre (une nouvelle fenêtre ou la même fenêtre).

   ![chlimage_1-238](assets/chlimage_1-238.png)

1. **[!UICONTROL Cliquez sur OK]**.

### Composant vidéo {#video-component}

Dynamic Media Classic **[!UICONTROL Vidéo]** (disponible dans la section Dynamic Media Classic du sidekick) utilise la détection de l’appareil et de la bande passante pour diffuser la vidéo appropriée à chaque écran. Ce composant est un lecteur vidéo HTML5. Il s’agit d’une visionneuse unique pouvant être utilisée sur plusieurs canaux.

Il peut être utilisé pour des ensembles de vidéos adaptables, une vidéo MP4 unique ou une vidéo F4V unique.

Voir [Vidéo](s7-video.md) pour plus d’informations sur le fonctionnement des vidéos avec l’intégration de Dynamic Media Classic. En outre, voir [Comparaison du composant vidéo Dynamic Media Classic et du composant vidéo Foundation](s7-video.md).

![chlimage_1-239](assets/chlimage_1-239.png)

### Limites connues du composant vidéo {#known-limitations-for-the-video-component}

Adobe DAM et WCM indiquent si une vidéo source Principale est téléchargée. Elles n’affichent pas les éléments proxy suivants :

* Rendus codés Dynamic Media Classic
* Visionneuses de vidéos adaptatives Dynamic Media Classic

Lors de l’utilisation d’une visionneuse de vidéos adaptative avec le composant vidéo Dynamic Media Classic, vous devez redimensionner le composant pour l’adapter aux dimensions de la vidéo.

## Explorateur de contenu Dynamic Media Classic {#scene-content-browser}

L’explorateur de contenu Dynamic Media Classic vous permet d’afficher le contenu de Dynamic Media Classic directement dans Experience Manager. Pour accéder à l’explorateur de contenu, dans le **[!UICONTROL Outil de recherche de contenu]**, sélectionnez **[!UICONTROL Dynamic Media Classic]** dans l’interface utilisateur optimisée pour les écrans tactiles ou la fonction **[!UICONTROL S7]** dans l’interface utilisateur classique. La fonctionnalité est identique pour les deux interfaces utilisateur.

Si vous avez plusieurs configurations, Experience Manager affiche par défaut la variable [configuration par défaut](/help/sites-administering/scene7.md#configuring-a-default-configuration). Vous pouvez sélectionner différentes configurations directement dans l’explorateur de contenu Dynamic Media Classic du menu déroulant.

>[!NOTE]
>
>* Les ressources figurant dans le dossier à la demande n’apparaissent pas dans le navigateur de contenu Dynamic Media Classic.
>* When [L’aperçu sécurisé est activé](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene), les ressources publiées et non publiées sur Dynamic Media Classic n’apparaissent pas dans le navigateur de contenu de Dynamic Media Classic.
>* Si vous ne voyez pas **[!UICONTROL Dynamic Media Classic]** ou le **[!UICONTROL S7]** comme option dans l’explorateur de contenu, vous devez [configurer Dynamic Media Classic pour qu’il fonctionne avec Experience Manager](/help/sites-administering/scene7.md).
>* Pour la vidéo, le navigateur de contenu Dynamic Media Classic prend en charge :
   >
   >   * Les ensembles de vidéos adaptables. Il s’agit de conteneurs de tous les rendus vidéo requis pour lire la vidéo sans difficultés sur plusieurs écrans.
   >   * La vidéo MP4 unique
   >   * Vidéo F4V simple


### Parcourir le contenu dans l’IU optimisée pour les écrans tactiles {#browsing-content-in-the-touch-optimized-ui}

Vous pouvez accéder au navigateur de contenu depuis l’interface utilisateur optimisée pour les écrans tactiles ou l’interface utilisateur classique. A l’heure actuelle, l’interface utilisateur optimisée pour les écrans comporte la limitation suivante :

* Les fichiers FXG et Flash de Dynamic Media Classic ne sont pas pris en charge.

Parcourir les ressources Dynamic Media Classic en sélectionnant **[!UICONTROL Dynamic Media Classic]** dans le troisième menu déroulant. Dynamic Media Classic n’apparaît pas dans la liste si vous n’avez pas configuré l’intégration Dynamic Media Classic/Experience Manager.

>[!NOTE]
>
>* L’explorateur de contenu Dynamic Media Classic charge environ 100 ressources et les trie par nom.
>* Si vous disposez d’un serveur d’aperçu sécurisé, le navigateur utilise ce serveur pour effectuer le rendu des miniatures et des ressources.
>


![chlimage_1-240](assets/chlimage_1-240.png)

En outre, vous pouvez parcourir les informations de résolution, de taille, de nombre de jours depuis la modification et de nom de fichier en pointant la souris sur un élément du navigateur.

![chlimage_1-241](assets/chlimage_1-241.png)

* Pour les ensembles de vidéos adaptables et les modèles, aucune information sur la taille n’est générée pour les miniatures.
* Pour les ensembles de vidéos adaptables, aucune résolution n’est générée pour les miniatures.

### Recherche de ressources Dynamic Media Classic avec l’explorateur de contenu {#searching-for-scene-assets-with-the-content-browser}

La recherche de ressources dans Dynamic Media Classic est similaire à la recherche de ressources dans Experience Manager Assets. Cependant, lorsque vous effectuez une recherche, une vue distante des ressources s’affiche dans le système Dynamic Media Classic, plutôt que de les importer directement dans Experience Manager.

Vous pouvez utiliser l’interface utilisateur classique ou l’interface utilisateur optimisée pour les écrans tactiles pour visualiser et rechercher des éléments. Selon l’interface, le mode de recherche est légèrement différent.

Lors d’une recherche dans l’une ou l’autre des interfaces, vous pouvez filtrer selon les critères suivants (présentés ici dans l’interface utilisateur optimisée pour les écrans tactiles) :

**[!UICONTROL Entrez des mots-clés]** - Vous pouvez rechercher des ressources par nom. Lors de la recherche, les mots-clés que vous saisissez correspondent au nom du fichier. Par exemple, la saisie du mot « swimming » recherche tous les noms de fichier qui commencent par ces lettres, dans cet ordre. Veillez à appuyer sur la touche Entrée après avoir tapé le terme pour rechercher la ressource.

![chlimage_1-242](assets/chlimage_1-242.png)

**[!UICONTROL Dossier/chemin]** - Le nom du dossier affiché dépend de la configuration que vous avez sélectionnée. Vous pouvez descendre jusqu’à des niveaux inférieurs en appuyant sur l’icône de dossier et en sélectionnant un sous-dossier, puis en appuyant sur la coche pour le sélectionner.

Si vous saisissez un mot-clé et sélectionnez un dossier, le Experience Manager recherche ce dossier et les sous-dossiers appropriés. Toutefois, si vous ne saisissez aucun mot-clé lors de la recherche, la sélection du dossier affiche uniquement les ressources contenues dans ce dossier et n’inclut aucun sous-dossier.

Par défaut, Experience Manager recherche le dossier sélectionné et tous les sous-dossiers.

![chlimage_1-243](assets/chlimage_1-243.png)

**[!UICONTROL Type de ressource]** - Sélectionner **[!UICONTROL Dynamic Media Classic]** pour parcourir le contenu Dynamic Media Classic. Cette option n’est disponible que si Dynamic Media Classic a été configuré.

![chlimage_1-244](assets/chlimage_1-244.png)

**[!UICONTROL Configuration]** - Si plusieurs configurations Dynamic Media Classic sont définies dans [!UICONTROL Cloud Services], vous pouvez le sélectionner ici. Par conséquent, le dossier change en fonction de la configuration choisie.

![chlimage_1-245](assets/chlimage_1-245.png)

**[!UICONTROL Type de ressource]** - Dans le navigateur Dynamic Media Classic, vous pouvez filtrer les résultats pour inclure l’un des éléments suivants : images, modèles, vidéos et ensembles de vidéos adaptatifs. Si vous ne sélectionnez aucun type de ressource, Experience Manager recherche tous les types de ressources par défaut.

![chlimage_1-246](assets/chlimage_1-246.png)

>[!NOTE]
>
>* Dans l’interface utilisateur classique, vous pouvez rechercher des éléments **Flash** et **FXG**. Le filtrage de ces types dans l’IU optimisée pour les écrans tactiles n’est pas pris en charge.
>
>* Lors de la recherche de vidéos, vous recherchez un seul rendu. Les résultats renvoient le rendu d’origine (uniquement &amp;ast;.mp4) et le rendu codé.
>* Lors de la recherche d’une visionneuse de vidéos adaptative, vous recherchez le dossier et tous les sous-dossiers, mais uniquement si vous avez ajouté un mot-clé à la recherche. Si vous n’avez pas ajouté de mot-clé, Experience Manager ne recherche pas les sous-dossiers.
>


**[!UICONTROL État de publication]** - Vous pouvez filtrer les ressources en fonction de l’état de publication : **[!UICONTROL Non publié]** ou **[!UICONTROL Publié]**. Si vous ne sélectionnez aucune **[!UICONTROL État de publication]**, Experience Manager recherche par défaut tous les états de publication.

![chlimage_1-247](assets/chlimage_1-247.png)
