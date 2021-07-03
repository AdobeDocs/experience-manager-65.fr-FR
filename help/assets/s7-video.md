---
title: Vidéo
description: Découvrez la gestion centralisée des ressources vidéo dans Adobe Experience Manager Assets, où vous pouvez télécharger des vidéos pour le codage automatique vers Dynamic Media Classic et accéder directement aux vidéos Dynamic Media Classic à partir de Experience Manager Assets. L’intégration vidéo Dynamic Media Classic étend la portée de la vidéo optimisée à tous les écrans.
uuid: 8b3423f1-d96b-44d9-bdb7-e3b77875b25d
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: managing-assets
content-type: reference
discoiquuid: 2685f9f3-0973-40a9-89b8-e7db0a6a75f2
role: User, Admin
exl-id: 56009925-1a36-48b5-b96c-ec2e468da106
feature: Vidéo
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '1568'
ht-degree: 38%

---

# Vidéo {#video}

Adobe Experience Manager Assets permet une gestion centralisée des ressources vidéo dans laquelle vous pouvez charger des vidéos directement dans Assets pour un codage automatique dans Dynamic Media Classic et accéder aux vidéos Dynamic Media Classic directement à partir de Assets pour la création de pages.

L’intégration vidéo de Dynamic Media Classic étend la portée de la vidéo optimisée à tous les écrans (détection automatique de périphérique et de bande passante).

* Le composant **[!UICONTROL Vidéo Scene7]** détecte automatiquement l’appareil et la bande passante afin de lire la vidéo au format approprié et de qualité optimale sur les ordinateurs de bureau, tablettes et appareils mobiles.
* Ressources - Vous pouvez inclure des ensembles de vidéos adaptables au lieu de contenus vidéo uniques. Une visionneuse de vidéos adaptative contient tous les rendus vidéo nécessaires pour lire la vidéo en toute transparence sur plusieurs écrans. Une visionneuse de vidéos adaptative regroupe les versions d’une même vidéo codées dans des débits et des formats différents, par exemple 400 kbit/s, 800 kbit/s et 1 000 kbit/s. Vous utilisez une visionneuse de vidéos adaptative, ainsi qu’un composant vidéo S7, pour la diffusion en continu de vidéo adaptative sur plusieurs écrans, y compris les appareils mobiles de bureau, iOS, Android™, BlackBerry® et Windows.
<!-- See [Scene7 documentation about adaptive video sets for more information](https://help.adobe.com/en_US/scene7/using/WS53492AE1-6029-45d8-BF80-F4B5CF33EB08.html). -->

## A propos de FFMPEG et Dynamic Media Classic {#about-ffmpeg-and-scene}

Le processus de codage vidéo par défaut est basé sur l’utilisation d’une intégration basée sur FFMPEG aux profils vidéo. De ce fait, le processus d’assimilation de la gestion des actifs numériques prêt à l’emploi contient les deux étapes suivantes du processus basé sur FFMPEG :

* Miniatures FFMPEG
* Codage FFMPEG

L’activation et la configuration de l’intégration de Dynamic Media Classic ne suppriment pas ou ne désactivent pas automatiquement ces deux étapes de processus à partir du workflow d’ingestion DAM prêt à l’emploi. Si vous utilisez déjà le codage vidéo FFMPEG dans Adobe Experience Manager, il est probable que FFMPEG soit installé dans vos environnements de création. Dans ce cas, une nouvelle vidéo ingérée à l’aide de la gestion des ressources numériques est codée deux fois : une fois à partir de l’encodeur FFMPEG et une fois à partir de l’intégration Dynamic Media Classic.

Si le codage vidéo FFMPEG est configuré dans Experience Manager et que FFMPEG est installé, Adobe vous recommande de supprimer les deux processus FFMPEG de vos processus d’ingestion DAM.

## Formats pris en charge {#supported-formats}

Les formats suivants sont pris en charge pour le composant vidéo Scene7 :

* F4V H.264
* MP4 H.264

## Choix de l’emplacement du téléchargement de la vidéo {#deciding-where-to-upload-your-video}

Le choix de l’emplacement du téléchargement du contenu vidéo dépend des éléments suivants :

* Avez-vous besoin d’un worfklow pour le contenu vidéo ?
* Avez-vous besoin d’un contrôle des versions pour le contenu vidéo ?

Si la réponse est « oui » à l’une des questions ou aux deux, téléchargez la vidéo directement dans la gestion des actifs numériques d’Adobe. Si la réponse est &quot;non&quot; aux deux questions, téléchargez directement votre vidéo vers Dynamic Media Classic. Le processus de chaque scénario est décrit dans la section suivante.

### Si vous téléchargez la vidéo directement dans la gestion des actifs numériques d’Adobe {#if-you-are-uploading-your-video-directly-to-adobe-dam}

Si vous avez besoin d’un workflow ou d’un contrôle de version pour vos ressources, téléchargez d’abord vers Adobe DAM. Vous trouverez ci-dessous le worfklow recommandé :

1. Chargez la ressource vidéo pour Adobe la gestion des ressources numériques et codez et publiez automatiquement dans Dynamic Media Classic.
1. Dans Experience Manager, accédez aux ressources vidéo dans la gestion de contenu web dans l’onglet **[!UICONTROL Films]** de l’outil de recherche de contenu.
1. Créez avec le composant **[!UICONTROL Vidéo Scene7]** ou **[!UICONTROL Vidéo de base]**.

### Si vous téléchargez votre vidéo vers Dynamic Media Classic {#if-you-are-uploading-your-video-to-scene}

Si vous n’avez pas besoin d’un workflow ou d’un contrôle de version pour vos ressources, chargez-les dans Scene7. Vous trouverez ci-dessous le worfklow recommandé :

1. Dans Dynamic Media Classic, [configurez un chargement et un codage FTP planifiés dans Scene7 (système automatisé)](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/uploading-files.html#upload-files-using-via-ftp).
1. Dans Experience Manager, accédez aux ressources vidéo dans la gestion de contenu web dans l’onglet **[!UICONTROL Scene7]** de l’outil de recherche de contenu.
1. Créez avec le composant **[!UICONTROL Vidéo Scene7]** .

## Configuration de l’intégration avec la vidéo Scene7 {#configuring-integration-with-scene-video}

Pour configurer les paramètres prédéfinis universaux :

1. Dans **[!UICONTROL Services Cloud]**, accédez à la configuration **[!UICONTROL Scene7]** et cliquez sur **[!UICONTROL Modifier]**.
1. Sélectionnez l’onglet **[!UICONTROL Vidéo]**.

   ![chlimage_1-363](assets/chlimage_1-363.png)

   >[!NOTE]
   >
   >L’onglet **[!UICONTROL Vidéo]** n’apparaît pas si la page ne comporte pas de configuration de cloud.

1. Sélectionnez le profil de codage vidéo adaptative, un profil de codage vidéo unique prêt à l’emploi ou un profil de codage vidéo personnalisé.

   >[!NOTE]
   >
   >Pour plus d’informations sur la signification des paramètres vidéo prédéfinis, consultez la [documentation de Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/setup/application-setup.html#video-presets-for-encoding-video-files).
   >
   >Adobe recommande de sélectionner les deux ensembles de vidéos adaptables lors de la configuration des paramètres prédéfinis ou de sélectionner l’option **[!UICONTROL Codage vidéo adaptative]**.

1. Les profils de codage sélectionnés sont automatiquement appliqués à toutes les vidéos téléchargées dans le dossier cible de la gestion des actifs numériques CQ que vous avez défini pour cette configuration de cloud Scene7. Vous pouvez définir plusieurs configurations de cloud Scene7 avec différents dossiers cibles afin d’appliquer différents profils de codage, selon vos besoins.

## Mise à jour de la visionneuse et des paramètres prédéfinis de codage {#updating-viewer-and-encoding-presets}

Pour mettre à jour la visionneuse et les paramètres prédéfinis de codage pour la vidéo, car ils ont été mis à jour dans Scene7, accédez à la configuration Scene7 dans la configuration cloud et appuyez sur **[!UICONTROL Mettre à jour la visionneuse et les paramètres prédéfinis de codage]**.

![chlimage_1-364](assets/chlimage_1-364.png)

## Chargement de la vidéo source Principale vers Scene7 à partir de la gestion des ressources numériques d’Adobe {#uploading-your-master-video}

1. Accédez au dossier cible de la gestion des actifs numériques CQ dans lequel vous avez défini la configuration de cloud avec les profils de codage Scene7.
1. Cliquez sur **[!UICONTROL Télécharger]** pour charger la vidéo source Principale. Le chargement et le codage des vidéos sont terminés une fois le workflow [!UICONTROL Ressource de mise à jour de gestion des actifs numériques] terminé et une coche s’affiche pour l’option **[!UICONTROL Publier sur Scene7]**.

   >[!NOTE]
   >
   >La génération des miniatures vidéo prend du temps.

   Faire glisser la vidéo source Principale de la gestion des actifs numériques sur le composant vidéo permet d’accéder à *tous* rendus proxy codés Scene7 pour diffusion.

## Comparaison du composant vidéo de base et du composant vidéo Scene7 {#foundation-video-component-versus-scene-video-component}

Lorsque vous utilisez Experience Manager, vous avez accès au composant vidéo disponible dans Sites et au composant vidéo Scene7. Ces composants ne sont pas interchangeables.

Le composant vidéo Scene7 ne fonctionne que pour les vidéos Scene7. Le composant de base fonctionne avec des vidéos stockées à partir de Experience Manager (à l’aide de ffmpeg) et des vidéos Scene7.

Le tableau suivant explique à quel moment utiliser le composant :

![chlimage_1-365](assets/chlimage_1-365.png)

>[!NOTE]
>
>Prêt à l’emploi, le composant vidéo S7 utilise le profil vidéo universel. Vous pouvez toutefois obtenir le lecteur vidéo HTML5 à utiliser par Experience Manager. Dans Scene7, copiez le code incorporé du lecteur vidéo HTML5 prêt à l’emploi et collez-le dans votre page de Experience Manager.

## Composant vidéo Experience Manager {#aem-video-component}

Même si l’utilisation du composant vidéo Scene7 est recommandée pour visionner des vidéos Scene7, cette section décrit l’utilisation de vidéos Scene7 avec le composant vidéo Foundation en Experience Manager, par souci d’exhaustivité.

### Comparaison des vidéos Experience Manager et des vidéos Scene7 {#aem-video-and-scene-video-comparison}

Le tableau suivant fournit une comparaison de haut niveau des fonctionnalités prises en charge entre le composant vidéo Experience Manager Foundation et le composant vidéo Scene7 :

|  | Vidéo de Experience Manager Foundation | Vidéo Scene7 |
|---|---|---|
| Approche | Approche HTML5 en premier lieu. Flash n’est utilisé que pour le secours non HTML5. | Flash sur la plupart des ordinateurs de bureau. HTML5 est utilisé pour les mobiles et les tablettes. |
| Diffusion | Progressive | Adaptative |
| Suivi | Oui | Oui |
| Evolutivité | Oui | Non |
| Vidéo mobile | Oui | Oui |

### Configuration {#setting-up}

#### Création de profils vidéo {#creating-video-profiles}

Les différents codages vidéo sont créés selon les paramètres prédéfinis de codage S7 sélectionnés dans la configuration de cloud S7. Pour que le composant vidéo de base les utilise, un profil vidéo doit être créé pour chaque paramètre prédéfini de codage S7 sélectionné. Cette méthode permet au composant vidéo de sélectionner les rendus DAM en conséquence.

>[!NOTE]
>
>Les nouveaux profils vidéo et leurs modifications doivent être activés pour la publication.

1. Dans Experience Manager, appuyez sur **[!UICONTROL Outils]** > **[!UICONTROL Console de configuration]**.
1. Dans la **[!UICONTROL console de configuration]**, accédez à **[!UICONTROL Outils]** > **[!UICONTROL DAM]** > **[!UICONTROL Profils vidéo]** dans l’arborescence de navigation.
1. Créez un profil vidéo S7. Dans le menu **[!UICONTROL New]**., sélectionnez **[!UICONTROL Créer une page]**, puis sélectionnez le modèle Profil vidéo Scene7 . Attribuez un nom à la nouvelle page de profil vidéo et cliquez sur **[!UICONTROL Créer]**.

   ![chlimage_1-366](assets/chlimage_1-366.png)

1. Modifiez le nouveau profil vidéo. Sélectionnez tout d’abord la configuration de cloud. Puis, sélectionnez le même paramètre prédéfini de codage que celui sélectionné dans la configuration de cloud.

   ![chlimage_1-367](assets/chlimage_1-367.png)

   | Propriété | Description |
   |---|---|
   | Configuration de cloud Scene7 | Configuration de cloud à utiliser pour les paramètres prédéfinis de codage. |
   | Paramètre prédéfini de codage Scene7 | Paramètre prédéfini de codage à associer à ce profil vidéo. |
   | Type de vidéo HTML5 | Cette propriété vous permet de définir la valeur de la propriété type de l’élément de source vidéo HTML5. Ces informations ne sont pas fournies par les paramètres prédéfinis de codage S7 mais requises pour effectuer correctement le rendu des vidéos en utilisant l’élément vidéo HTML5. Une liste des formats courants est fournie mais ils peuvent être remplacés par d’autres formats. |

   Répétez cette étape pour tous les paramètres prédéfinis de codage sélectionnés dans la configuration de cloud que vous voulez utiliser dans le composant vidéo.

#### Configuration de la conception {#configuring-design}

Le composant **[!UICONTROL Vidéo de base]** doit connaître les profils vidéo à utiliser pour créer la liste des sources vidéo. Ouvrez la boîte de dialogue de conception des composants vidéo et configurez la conception des composants pour utiliser les nouveaux profils vidéo.

>[!NOTE]
>
>Si vous utilisez le composant **[!UICONTROL Vidéo de base]** sur une page mobile, répétez ces étapes lors de la conception de la page mobile.

>[!NOTE]
>
>Les modifications apportées à la conception requièrent l’activation de la conception afin qu’elles prennent effet lors de la publication.

1. Ouvrez la boîte de dialogue de conception du composant **[!UICONTROL Vidéo de base]** et modifiez l’onglet **[!UICONTROL Profils]**. Supprimez ensuite les profils d&#39;usine et ajoutez les nouveaux profils vidéo S7. L’ordre de la liste des profils dans la boîte de dialogue de conception définit l’ordre de l’élément de sources vidéo lors du rendu.
1. Pour les navigateurs qui ne prennent pas en charge HTML5, le composant vidéo vous permet de configurer un Flash de secours. Ouvrez la boîte de dialogue de conception des composants vidéo et remplacez-la par l’onglet **[!UICONTROL Flash]** . Configurez les paramètres du lecteur Flash et attribuez un profil de secours au lecteur Flash.

#### Liste de contrôle {#checklist}

1. Créer une configuration de cloud S7. Assurez-vous que les paramètres prédéfinis de codage vidéo sont définis et que l’importateur est en cours d’exécution.
1. Créer un profil vidéo S7 pour chaque paramètre prédéfini de codage vidéo sélectionné dans la configuration de cloud.
1. Les profils vidéo doivent être activés.
1. Configurez la conception du composant **[!UICONTROL Vidéo de base]** sur votre page.
1. Activer la conception une fois que vous avez terminé les modifications de cette dernière.
