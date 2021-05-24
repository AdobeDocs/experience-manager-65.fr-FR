---
title: Vidéo
seo-title: Vidéo
description: Assets permet une gestion centralisée des ressources vidéo dans laquelle vous pouvez charger des vidéos directement dans Assets pour un codage automatique dans Dynamic Media Classic et accéder aux vidéos Dy directement à partir de Assets pour la création de pages.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
discoiquuid: dfaa4b3f-f65a-4fe3-87a7-f3bc71015e56
exl-id: c540aa49-9981-4e8c-97df-972085b26490
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1698'
ht-degree: 42%

---

# Vidéo{#video}

Assets permet une gestion centralisée des ressources vidéo dans laquelle vous pouvez charger des vidéos directement dans Assets pour un codage automatique dans Dynamic Media Classic et accéder aux vidéos Dynamic Media Classic directement à partir de Assets pour la création de pages.

L’intégration vidéo de Dynamic Media Classic étend la portée de la vidéo optimisée à tous les écrans (détection automatique de périphérique et de bande passante).

* Le composant vidéo Dynamic Media Classic détecte automatiquement l’appareil et la bande passante afin de lire la vidéo au format et à la qualité appropriés sur les ordinateurs de bureau, les tablettes et les appareils mobiles.
* Ressources - Vous pouvez inclure des ensembles de vidéos adaptables au lieu de contenus vidéo uniques. Un ensemble de vidéos adaptables est un conteneur de tous les rendus vidéo requis permettant de lire la vidéo sans heurt sur plusieurs écrans. Une visionneuse de vidéos adaptative regroupe les versions d’une même vidéo codées dans des débits et des formats différents, par exemple 400 kbit/s, 800 kbit/s et 1 000 kbit/s. Vous utilisez un ensemble de vidéos adaptables, accompagné d’un composant vidéo S7, pour la diffusion vidéo en continu adaptative sur plusieurs écrans, notamment des ordinateurs de bureau, des téléphones iOS, Android et Blackberry et des appareils mobiles Windows. Voir [Documentation de Dynamic Media Classic sur les visionneuses de vidéos adaptatives pour plus d’informations](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/video/quick-start-video.html#video).

## A propos de FFMPEG et Dynamic Media Classic {#about-ffmpeg-and-scene}

Le workflow de codage vidéo par défaut est basé sur l’utilisation d’une intégration basée sur FFMPEG aux profils vidéo. Par conséquent, le workflow [!UICONTROL Ressource de mise à jour de gestion des actifs numériques] prêt à l’emploi contient les deux étapes suivantes du workflow basé sur ffmpeg :

* Miniatures FFMPEG
* Codage FFMPEG

Gardez à l’esprit que l’activation et la configuration de l’intégration de Dynamic Media Classic ne suppriment pas ou ne désactivent pas automatiquement ces deux étapes de processus à partir du workflow d’ingestion [!UICONTROL Ressource de mise à jour de gestion des actifs numériques] prêt à l’emploi. Si vous utilisez déjà le codage vidéo FFMPEG dans AEM, il est probable que FFMPEG soit installé dans vos environnements de création. Dans ce cas, une nouvelle vidéo ingérée à l’aide de Ressources est codée deux fois : une fois à partir de l’encodeur FFMPEG et une fois à partir de l’intégration Dynamic Media Classic.

Si le codage vidéo basé sur FFMPEG est configuré dans AEM configuré et que FFMPEG est installé, Adobe vous recommande de supprimer les deux workflows FFMPEG de vos workflows [!UICONTROL Ressource de mise à jour de gestion des actifs numériques] .

### Formats pris en charge {#supported-formats}

Les formats suivants sont pris en charge pour le composant vidéo Dynamic Media Classic :

* F4V H.264
* MP4 H.264

### Choix de l’emplacement du téléchargement de la vidéo {#deciding-where-to-upload-your-video}

Le choix de l’emplacement du téléchargement du contenu vidéo dépend des éléments suivants :

* Avez-vous besoin d’un worfklow pour le contenu vidéo ?
* Avez-vous besoin d’un contrôle des versions pour le contenu vidéo ?

Si la réponse est « oui » à l’une des questions ou aux deux, téléchargez la vidéo directement dans la gestion des actifs numériques d’Adobe. Si la réponse est &quot;non&quot; aux deux questions, téléchargez directement votre vidéo vers Dynamic Media Classic. Le worfklow de chaque scénario est décrit dans la section suivante.

#### Si vous téléchargez la vidéo directement dans Adobe Assets  {#if-you-are-uploading-your-video-directly-to-adobe-assets}

Si vous avez besoin d’un worfklow ou d’une création de versions pour les ressources, vous devez tout d’abord les télécharger dans Adobe Assets. Vous trouverez ci-dessous le worfklow recommandé :

1. Téléchargez la ressource vidéo pour Adobe les ressources et codez et publiez automatiquement dans Dynamic Media Classic.
1. Dans AEM, accédez aux contenus vidéo dans la gestion de contenu web, dans l’onglet **[!UICONTROL Films]** de l’outil de recherche de contenu.
1. Créez avec un composant vidéo Dynamic Media Classic ou vidéo de base.

#### Si vous téléchargez votre vidéo vers Dynamic Media Classic {#if-you-are-uploading-your-video-to-scene}

Si vous n’avez pas besoin d’un workflow ou d’un contrôle de version pour vos ressources, vous devez charger vos ressources dans Dynamic Media Classic. Vous trouverez ci-dessous le worfklow recommandé :

1. Dans l’appli de bureau Dynamic Media Classic, [configurez un chargement et un codage FTP planifiés vers Dynamic Media Classic (système automatisé)](https://help.adobe.com/en_US/scene7/using/WS70B173EC-4CAD-4b4c-BF9C-43A11F3A5950.html).
1. Dans AEM, accédez aux ressources vidéo dans la gestion de contenu web dans l’onglet **[!UICONTROL Dynamic Media Classic]** de l’outil de recherche de contenu.
1. Créez avec le composant vidéo Dynamic Media Classic.

### Configuration de l’intégration avec la vidéo Dynamic Media Classic {#configuring-integration-with-scene-video}

**Pour configurer des paramètres prédéfinis** universels :

1. Dans **[!UICONTROL Cloud Services]**, accédez à votre configuration **[!UICONTROL Dynamic Media Classic]** et cliquez sur **[!UICONTROL Modifier.]**
1. Sélectionnez l’onglet **[!UICONTROL Vidéo]**.

   >[!NOTE]
   >
   >L’onglet **[!UICONTROL Vidéo]** n’apparaît pas si la page ne comporte pas de configuration de cloud. Voir [Activation de Dynamic Media Classic pour WCM](#enablingscene7forwcm).

1. Sélectionnez le profil de codage vidéo adaptative, un profil de codage vidéo unique prêt à l’emploi ou un profil de codage vidéo personnalisé.

   >[!NOTE]
   >
   >Pour plus d’informations sur la signification des paramètres vidéo prédéfinis, voir [Paramètres vidéo prédéfinis pour le codage des fichiers vidéo](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/setup/application-setup.html?lang=en#video-presets-for-encoding-video-files).
   >
   >Adobe recommande de sélectionner les deux ensembles de vidéos adaptables lors de la configuration des paramètres prédéfinis ou de sélectionner l’option **[!UICONTROL Codage vidéo adaptative]**.

1. Les profils de codage sélectionnés sont automatiquement appliqués à toutes les vidéos téléchargées dans le dossier cible de la gestion des actifs numériques CQ que vous configurez pour cette configuration cloud Dynamic Media Classic. Vous pouvez configurer plusieurs configurations de cloud Dynamic Media Classic avec différents dossiers cibles afin d’appliquer différents profils de codage selon vos besoins.

### Mise à jour de la visionneuse et des paramètres prédéfinis de codage {#updating-viewer-and-encoding-presets}

Si vous devez mettre à jour la visionneuse et les paramètres prédéfinis de codage pour la vidéo dans AEM car les paramètres prédéfinis ont été mis à jour dans Dynamic Media Classic, accédez à la configuration Dynamic Media Classic dans la configuration cloud et cliquez sur **Mettre à jour la visionneuse et les paramètres prédéfinis de codage**.

![chlimage_1-131](assets/chlimage_1-131.png)

### Téléchargement de la vidéo source Principale {#uploading-your-master-video}

Pour télécharger votre vidéo source Principale vers Dynamic Media Classic à partir de la gestion des ressources numériques d’Adobe :

1. Accédez au dossier cible de la gestion des actifs numériques CQ dans lequel vous avez configuré votre configuration cloud avec les profils de codage Dynamic Media Classic.
1. Cliquez sur **[!UICONTROL Télécharger]** pour charger la vidéo source Principale. Le chargement et le codage des vidéos sont terminés une fois le workflow [!UICONTROL Ressource de mise à jour de gestion des actifs numériques] terminé et une coche est associée à l’option **[!UICONTROL Publier vers Dynamic Media Classic]**.

   >[!NOTE]
   >
   >La génération des miniatures de vidéo peut prendre du temps.

   Faites glisser la vidéo source Principale de la gestion des actifs numériques vers le composant vidéo pour accéder à *tous* des rendus proxy codés Dynamic Media Classic pour diffusion.

### Composant vidéo de base par rapport au composant vidéo Dynamic Media Classic {#foundation-video-component-versus-scene-video-component}

Lorsque vous utilisez AEM, vous avez accès au composant vidéo disponible dans Sites et au composant vidéo Dynamic Media Classic. Ces composants ne sont pas interchangeables.

Le composant vidéo Dynamic Media Classic ne fonctionne que pour les vidéos Dynamic Media Classic. Le composant de base fonctionne avec des vidéos stockées à partir d’AEM (à l’aide de ffmpeg) et de vidéos Dynamic Media Classic.

Le tableau suivant explique les cas d’utilisation de chaque composant :

![chlimage_1-132](assets/chlimage_1-132.png)

>[!NOTE]
>
>Le composant vidéo Dynamic Media Classic prêt à l’emploi utilise le profil vidéo universel. Vous pouvez toutefois obtenir le lecteur vidéo HTML5 à utiliser par AEM. Dans Dynamic Media Classic, copiez le code incorporé du lecteur vidéo HTML5 prêt à l’emploi et collez-le dans votre page AEM.


## Composant vidéo AEM {#aem-video-component}

Même si l’utilisation du composant vidéo Dynamic Media Classic est recommandée pour l’affichage de vidéos Dynamic Media Classic, cette section décrit l’utilisation des vidéos Dynamic Media Classic avec le [!UICONTROL composant vidéo de base] dans AEM, par souci d’exhaustivité.

### AEM Comparaison des vidéos et des vidéos Dynamic Media Classic {#aem-video-and-scene-video-comparison}

Le tableau suivant fournit une comparaison de haut niveau des fonctionnalités prises en charge entre le composant vidéo AEM Foundation et le composant vidéo Dynamic Media Classic :

|  | Vidéo de base AEM | Vidéo Dynamic Media Classic |
|---|---|---|
| Approche | Approche HTML5 en premier lieu. Flash n’est utilisé que pour le secours non HTML5. | Flash sur la plupart des ordinateurs de bureau. HTML5 est utilisé pour les mobiles et les tablettes. |
| Diffusion | Progressive | Adaptative |
| Suivi | Oui | Oui |
| Evolutivité | Oui | Non |
| Vidéo mobile | Oui | Oui |

### Configuration  {#setting-up}

#### Création de profils vidéo {#creating-video-profiles}

Les différents codages vidéo sont créés selon les paramètres prédéfinis de codage Dynamic Media Classic sélectionnés dans la configuration cloud de Dynamic Media Classic. Pour que le composant vidéo de base les utilise, un profil vidéo doit être créé pour chaque paramètre prédéfini de codage Dynamic Media Classic sélectionné. Cela permet au composant vidéo de sélectionner les rendus de la gestion des actifs numériques en conséquence.

>[!NOTE]
>
>Les nouveaux profils vidéo et leurs modifications doivent être activés pour la publication.

1. Dans AEM, accédez à **[!UICONTROL Outils]**, puis sélectionnez **[!UICONTROL Console de configuration.]** Dans la console de configuration, accédez à  **[!UICONTROL Outils]**  >  **[!UICONTROL Ressources]**  >  **[!UICONTROL Profils]** vidéo dans l’arborescence de navigation.
1. Créez un profil vidéo Dynamic Media Classic. Dans la section **[!UICONTROL Nouveau...]**, sélectionnez **[!UICONTROL Créer une page]**, puis sélectionnez le modèle Profil vidéo Dynamic Media Classic . Attribuez un nom à la nouvelle page de profil vidéo et cliquez sur **[!UICONTROL Créer.]**

   ![chlimage_1-133](assets/chlimage_1-133.png)

1. Modifiez le nouveau profil vidéo. Sélectionnez tout d’abord la configuration de cloud. Puis, sélectionnez le même paramètre prédéfini de codage que celui sélectionné dans la configuration de cloud.

   ![chlimage_1-134](assets/chlimage_1-134.png)

   | Propriété | Description |
   |---|---|
   | Configuration du cloud Dynamic Media Classic | Configuration de cloud à utiliser pour les paramètres prédéfinis de codage. |
   | Paramètre prédéfini de codage Dynamic Media Classic | Paramètre prédéfini de codage à associer à ce profil vidéo. |
   | Type de vidéo HTML5 | Cette propriété permet de définir la valeur de la propriété du type de l’élément source vidéo HTML5. Ces informations ne sont pas fournies par les paramètres prédéfinis de codage Dynamic Media Classic, mais sont requises pour effectuer correctement le rendu des vidéos à l’aide de l’élément vidéo HTML5. Une liste des formats courants est fournie mais ils peuvent être remplacés par d’autres formats. |

   Répétez cette étape pour tous les paramètres prédéfinis de codage sélectionnés dans la configuration de cloud que vous voulez utiliser dans le composant vidéo.

#### Conception de la configuration  {#configuring-design}

Le composant vidéo de base doit connaître les profils vidéo à utiliser afin de créer la liste des sources vidéo. Vous devez ouvrir la boîte de dialogue de conception des composants vidéo et configurer la conception des composants pour l’utilisation des nouveaux profils vidéo.

>[!NOTE]
>
>Si vous utilisez le composant vidéo de base sur une page mobile, vous devrez peut-être répéter ces étapes pour la conception de la page mobile.

>[!NOTE]
>
>Les modifications apportées à la conception requièrent l’activation de la conception afin qu’elles prennent effet lors de la publication.

1. Ouvrez la boîte de dialogue de conception des composants vidéo de base et sélectionnez l’onglet **[!UICONTROL Profils.]** Supprimez ensuite les profils prêts à l’emploi et ajoutez les nouveaux profils vidéo Dynamic Media Classic. L’ordre de la liste des profils dans la boîte de dialogue de conception définit également l’ordre de l’élément de sources vidéo lors du rendu.
1. Pour les navigateurs ne prenant pas en charge HTML5, le composant vidéo permet de configurer un secours Flash. Ouvrez la boîte de dialogue de conception des composants vidéo et sélectionnez l’onglet **[!UICONTROL Flash.]** Configurez les paramètres du lecteur Flash et affectez un profil de secours au lecteur.

#### Liste de contrôle {#checklist}

1. Créez une configuration cloud Dynamic Media Classic. S’assurer que les paramètres prédéfinis de codage vidéo sont définis et que l’importateur fonctionne.
1. Créez un profil vidéo Dynamic Media Classic pour chaque paramètre prédéfini de codage vidéo sélectionné dans la configuration cloud.
1. Les profils vidéo doivent être activés.
1. Configurer la conception du composant vidéo de base sur votre page.
1. Activer la conception une fois que vous avez terminé les modifications de cette dernière.
