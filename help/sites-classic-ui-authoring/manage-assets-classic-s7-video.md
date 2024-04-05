---
title: Vidéo dans la création de sites Classic
description: Les ressources fournissent une gestion du contenu vidéo centralisée où vous pouvez charger des vidéos directement dans les ressources pour un codage automatique sur Dynamic Media Classic et accéder aux vidéos Dy directement depuis les Assets à des fins de création de page.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
exl-id: c540aa49-9981-4e8c-97df-972085b26490
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1662'
ht-degree: 100%

---

# Vidéo{#video}

Les ressources fournissent une gestion du contenu vidéo centralisée où vous pouvez charger des vidéos directement dans les ressources pour un codage automatique sur Dynamic Media Classic et accéder aux vidéos Dynamic Media Classic directement depuis Assets à des fins de création de page.

L’intégration vidéo de Dynamic Media Classic étend la portée de la vidéo optimisée à tous les écrans (détection automatique de l’appareil et de la bande passante).

* Le composant vidéo de Dynamic Media Classic procède automatiquement à la détection de l’appareil et de la bande passante afin de lire la vidéo au format adéquat avec la qualité optimale sur des ordinateurs de bureau, des tablettes et des téléphones mobiles.
* Assets - Vous pouvez inclure des visionneuses de vidéos adaptatives au lieu de ressources vidéo uniques. Une visionneuse de vidéos adaptatives est un conteneur de tous les rendus vidéo requis permettant de lire la vidéo sans heurt sur plusieurs écrans. Une visionneuse de vidéos adaptative regroupe les versions d’une même vidéo codées dans des débits et des formats différents, par exemple 400 kbit/s, 800 kbit/s et 1 000 kbit/s. Vous utilisez une visionneuse de vidéos adaptatives, accompagné d’un composant vidéo S7, pour la diffusion vidéo en continu adaptative sur plusieurs écrans, notamment des ordinateurs de bureau, des téléphones iOS, Android™ et BlackBerry® et des appareils mobiles Windows. Pour plus d’informations, consultez la [documentation sur Dynamic Media Classic sur les visionneuses de vidéos adaptatives](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/video/quick-start-video.html?lang=fr#video).

## À propos de FFMPEG et Dynamic Media Classic {#about-ffmpeg-and-scene}

Le workflow de codage vidéo par défaut est basé sur l’utilisation d’une intégration basée sur FFMPEG aux profils vidéo. De ce fait, le workflow de [!UICONTROL mise à jour de la ressource de gestion des DAM] prêt à l’emploi contient les deux étapes suivantes du workflow basé sur FFMPEG :

* Miniatures FFMPEG
* Encodage FFMPEG

Gardez à l’esprit que l’activation et la configuration de l’intégration ne suppriment ou ne désactivent pas automatiquement ces deux étapes du workflow de [!UICONTROL mise à jour de la ressource de gestion des DAM] prêt à l’emploi. Si vous utilisez déjà le codage vidéo FFMPEG dans Adobe Experience Manager, il est probable que FFMPEG soit installé dans vos environnements de création. Dans ce cas, une nouvelle vidéo ingérée à l’aide d’Experience Manager Assets est codée deux fois : une fois à partir de l’encodeur FFMPEG et une fois à partir de l’intégration Dynamic Media Classic.

Si le codage vidéo FFMPEG est configuré dans Experience Manager et que FFMPEG est installé, Adobe recommande de supprimer les deux workflows FFMPEG des workflows de mise à jour des ressources de [!UICONTROL gestion des DAM].

### Formats pris en charge {#supported-formats}

Les formats suivants sont pris en charge pour le composant vidéo Dynamic Media Classic :

* F4V H.264
* MP4 H.264

### Choix de l’emplacement du chargement de la vidéo {#deciding-where-to-upload-your-video}

Le choix de l’emplacement de chargement de vos ressources vidéo dépend des éléments suivants :

* Avez-vous besoin d’un workflow pour la ressource vidéo ?
* Avez-vous besoin d’un contrôle de version pour la ressource vidéo ?

Si la réponse à une ou deux de ces questions est « oui », téléchargez votre vidéo directement dans la gestion des DAM d’Adobe. Si la réponse est « non » aux deux questions, chargez la vidéo directement dans Dynamic Media Classic. Le workflow de chaque scénario est décrit dans la section suivante.

#### Si vous téléchargez la vidéo directement vers Adobe Assets {#if-you-are-uploading-your-video-directly-to-adobe-assets}

Si vous avez besoin d’un workflow ou d’un contrôle de versions pour vos ressources, vous devez tout d’abord les télécharger sur les ressources Adobe. Vous trouverez ci-dessous le workflow recommandé :

1. Chargez la ressource vidéo dans Adobe Assets et codez-la, puis publiez-la automatiquement dans Dynamic Media Classic.
1. Dans Experience Manager, accédez aux contenus vidéo dans la gestion de contenu web, dans l’onglet **[!UICONTROL Films]** de l’outil de recherche de contenu.
1. Créez avec le composant vidéo Dynamic Media Classic ou de base.

#### Si vous chargez la vidéo vers Dynamic Media Classic {#if-you-are-uploading-your-video-to-scene}

Si vous n’avez pas besoin d’un workflow ou d’une création de versions pour les contenus, vous devez charger les contenus dans Dynamic Media Classic. Vous trouverez ci-dessous le workflow recommandé :

1. Dans l’appli de bureau Dynamic Media Classic, [configurez un chargement et un codage FTP planifiés dans Dynamic Media Classic (système automatisé)](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/uploading-files.html?lang=fr#upload-options).
1. Dans Experience Manager, accédez aux ressources vidéo dans la gestion de contenu web dans l’onglet **[!UICONTROL Dynamic Media Classic]** de l’outil de recherche de contenu.
1. Créez avec le composant vidéo Dynamic Media Classic.

### Configuration de l’intégration à Dynamic Media Classic Video {#configuring-integration-with-scene-video}

1. Dans **[!UICONTROL Services cloud]**, accédez à la configuration **[!UICONTROL Dynamic Media Classic]** et sélectionnez **[!UICONTROL Modifier]**.
1. Sélectionnez l’onglet **[!UICONTROL Vidéo]**.

   >[!NOTE]
   >
   >L’onglet **[!UICONTROL Vidéo]** n’apparaît pas si la page ne comporte pas de configuration cloud. Consultez la section [Activation de Dynamic Media Classic pour la gestion de contenu web](#enablingscene7forwcm).

1. Sélectionnez le profil de codage vidéo adaptative, un profil de codage vidéo unique prêt à l’emploi ou un profil de codage vidéo personnalisé.

   >[!NOTE]
   >
   >Pour plus d’informations sur la signification des paramètres vidéo prédéfinis, consultez la section [Paramètres prédéfinis de vidéo pour le codage des fichiers vidéo](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/setup/application-setup.html?lang=fr#video-presets-for-encoding-video-files).
   >
   >Adobe recommande de sélectionner les deux visionneuses de vidéos adaptatives lors de la configuration des paramètres prédéfinis ou de sélectionner l’option **[!UICONTROL Codage vidéo adaptatif]**.

1. Les profils de codage sélectionnés sont automatiquement appliqués à toutes les vidéos téléchargées dans le dossier cible de la gestion des DAM CQ que vous avez défini pour cette configuration cloud de Dynamic Media Classic. Vous pouvez définir plusieurs configurations cloud Dynamic Media Classic avec différents dossiers cibles afin d’appliquer différents profils de codage, selon vos besoins.

### Mise à jour de la visionneuse et des paramètres prédéfinis de codage {#updating-viewer-and-encoding-presets}

Mettez à jour la visionneuse et les paramètres prédéfinis de codage pour la vidéo dans Experience Manager si les paramètres prédéfinis ont été mis à jour dans Dynamic Media Classic. Dans ce cas, accédez à la configuration Dynamic Media Classic dans la configuration cloud et sélectionnez **Mise à jour de la visionneuse et des paramètres prédéfinis de codage**.

![chlimage_1-131](assets/chlimage_1-131.png)

### Chargement de la vidéo source principale {#uploading-your-master-video}

Pour charger votre vidéo source principale vers Dynamic Media Classic à partir de la gestion des DAM d’Adobe, procédez comme suit :

1. Accédez au dossier cible de la gestion des DAM CQ dans lequel vous avez défini la configuration cloud avec les profils de codage Dynamic Media Classic.
1. Sélectionnez **[!UICONTROL Charger]** pour charger une vidéo source principale. Le chargement et le codage de la vidéo sont terminés une fois que le workflow de [!UICONTROL mise à jour des ressources de gestion des DAM] est achevé et que l’option **[!UICONTROL Publier sur Dynamic Media Classic]** comporte une coche.

   >[!NOTE]
   >
   >La génération des miniatures de vidéo peut prendre du temps.

   Lorsque vous faites glisser la vidéo source principale de gestion des DAM sur le composant vidéo, il accède à *tous* les rendus proxy codés de Dynamic Media Classic pour la diffusion.

### Composant vidéo de base par rapport au composant vidéo Dynamic Media Classic {#foundation-video-component-versus-scene-video-component}

Lorsque vous utilisez Experience Manager, vous avez accès à la fois au composant vidéo disponible dans Sites et au composant vidéo Dynamic Media Classic. Ces composants ne sont pas interchangeables.

Le composant vidéo Dynamic Media Classic fonctionne uniquement pour les vidéos Dynamic Media Classic. Le composant de base fonctionne avec des vidéos stockées à partir d’Experience Manager (à l’aide de ffmpeg) et des vidéos Dynamic Media Classic.

Le tableau suivant explique les cas d’utilisation de chaque composant :

![chlimage_1-132](assets/chlimage_1-132.png)

>[!NOTE]
>
>Prêt à l’emploi, le composant vidéo Dynamic Media Classic utilise le profil vidéo universel. Vous pouvez toutefois obtenir le lecteur vidéo HTML5 pour l’utiliser avec Experience Manager. Dans Dynamic Media Classic, copiez le code incorporé du lecteur vidéo HTML5 prêt à l’emploi et placez-le dans votre page Experience Manager.
>

## Composant vidéo Experience Manager {#aem-video-component}

Même si l’utilisation du composant vidéo Dynamic Media Classic est recommandée pour visionner des vidéos Dynamic Media Classic, cette section décrit l’utilisation de vidéos Dynamic Media Classic avec le [!UICONTROL Composant vidéo de base] dans Experience Manager, pour plus d’exhaustivité.

### Comparaison des vidéos Experience Manager et des vidéos Dynamic Media Classic {#aem-video-and-scene-video-comparison}

Le tableau suivant fournit une comparaison de haut niveau des fonctionnalités prises en charge par le composant vidéo Experience Manager Foundation et par le composant vidéo Dynamic Media Classic :

|   | Vidéo de base Experience Manager | Vidéo de Dynamic Media Classic |
|---|---|---|
| Approche | Première approche HTML5. Flash n’est utilisé que pour la version de secours autre que HTML5. | Flash sur la plupart des ordinateurs de bureau. HTML5 est utilisé pour les appareils mobiles et les tablettes. |
| Diffusion | Progressif | Diffusion en continu à débit adaptatif |
| Tracking | Oui | Oui |
| Extensibilité | Oui | Non |
| Vidéo pour mobiles | Oui | Oui |

### Configuration {#setting-up}

#### Création de profils vidéo {#creating-video-profiles}

Les différents codages vidéo sont créés selon les paramètres prédéfinis de codage Dynamic Media Classic sélectionnés dans la configuration cloud Dynamic Media Classic. Pour que le composant vidéo de base les utilise, vous devez créer un profil vidéo pour chaque paramètre prédéfini de codage Dynamic Media Classic sélectionné. Cela permet au composant vidéo de sélectionner les rendus de la gestion des DAM en conséquence.

>[!NOTE]
>
>Les nouveaux profils vidéo et leurs modifications doivent être activés pour la publication.

1. Dans Experience Manager, accédez à **[!UICONTROL Outils]**, puis sélectionnez la **[!UICONTROL Console de configuration]**.
1. Dans la console de configuration, accédez à **[!UICONTROL Outils]** > **[!UICONTROL Ressources]** > **[!UICONTROL Profils vidéo]** dans l’arborescence de navigation.
1. Créez un profil vidéo Dynamic Media Classic. Dans le menu **[!UICONTROL Nouveau]**, sélectionnez **[!UICONTROL Créer une page]**.
1. Sélectionnez le modèle de profil vidéo Dynamic Media Classic. Attribuez un nom à la nouvelle page de profil vidéo et sélectionnez **[!UICONTROL Créer]**.

   ![chlimage_1-133](assets/chlimage_1-133.png)

1. Modifiez le nouveau profil vidéo. Sélectionnez d’abord la configuration cloud. Sélectionnez ensuite le même paramètre prédéfini de codage que celui sélectionné dans la configuration cloud.

   ![chlimage_1-134](assets/chlimage_1-134.png)

   | Propriété | Description |
   |---|---|
   | Configuration cloud Dynamic Media Classic | Configuration cloud à utiliser pour les paramètres prédéfinis de codage. |
   | Paramètre prédéfini de codage Dynamic Media Classic | Paramètre prédéfini de codage avec lequel mapper ce profil vidéo. |
   | Type vidéo HTML5 | Cette propriété vous permet de définir la valeur de la propriété du type de l’élément source vidéo HTML5. Ces informations ne sont pas fournies par les paramètres prédéfinis de codage Dynamic Media Classic mais elles sont requises pour effectuer correctement le rendu des vidéos en utilisant l’élément vidéo HTML5. Une liste des formats courants est fournie mais ils peuvent être remplacés par d’autres formats. |

   Répétez cette étape pour tous les paramètres prédéfinis de codage sélectionnés dans la configuration cloud que vous voulez utiliser dans le composant vidéo.

#### Configuration de la conception {#configuring-design}

Le composant vidéo de base doit connaître les profils vidéo à utiliser afin de créer la liste des sources vidéo. Ouvrez la boîte de dialogue de conception des composants vidéo et configurez la conception des composants pour l’utilisation des nouveaux profils vidéo.

>[!NOTE]
>
>Si vous utilisez le composant vidéo de base sur une page mobile, répétez ces étapes pour la conception de la page mobile.

>[!NOTE]
>
>Les modifications apportées à la conception requièrent l’activation de la conception afin qu’elles prennent effet lors de la publication.

1. Ouvrez la boîte de dialogue de conception des composants vidéo de base et sélectionnez l’onglet **[!UICONTROL Profils]**. Supprimez ensuite les profils prêts à l’emploi et ajoutez les nouveaux profils vidéo Dynamic Media Classic. L’ordre de la liste des profils de la boîte de dialogue de conception définit également l’ordre des sources vidéo lors du rendu.
1. Pour les navigateurs ne prenant pas en charge HTML5, le composant vidéo permet de configurer Flash comme solution de secours. Ouvrez la boîte de dialogue de conception des composants vidéo et sélectionnez l’onglet **[!UICONTROL Flash]**. Configurez les paramètres du lecteur Flash Player et attribuez-lui un profil de secours.

#### Liste de contrôle {#checklist}

1. Créez une configuration cloud Dynamic Media Classic. Assurez-vous que les paramètres prédéfinis de codage vidéo sont définis et que l’importateur fonctionne.
1. Créez un profil vidéo Dynamic Media Classic pour chaque paramètre prédéfini de codage vidéo sélectionné dans la configuration cloud.
1. Les profils vidéo doivent être activés.
1. Configurez la conception du composant vidéo de base sur votre page.
1. Activez la conception une fois que vous avez terminé les modifications sur cette dernière.
