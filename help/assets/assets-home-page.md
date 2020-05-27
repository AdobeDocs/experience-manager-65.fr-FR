---
title: Adobe Experience Manager Assets Page d'accueil
description: Personnalisez la Page d'accueil Ressources d’Experience Manager pour bénéficier d’une expérience d’écran de bienvenue enrichie, y compris un instantané des dernières activités relatives aux ressources.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 35%

---


# Adobe Experience Manager Assets Page d&#39;accueil {#aem-assets-home-page-experience}

Personnalisez la page d&#39;accueil Ressources d’Adobe Experience Manager pour bénéficier d’une expérience d’écran de bienvenue enrichie, y compris un instantané des activités récentes relatives aux ressources.

La page d&#39;accueil Ressources offre une expérience d’écran de bienvenue riche et personnalisée, qui comprend un instantané des activités récentes, telles que les ressources récemment affichées ou téléchargées.

La page d&#39;accueil Ressources est désactivée par défaut. Pour l’activer, procédez comme suit :

1. Ouvrez Experience Manager Configuration Manager `https://[aem_server]:[port]/system/console/configMgr`.
1. Open the **[!UICONTROL Day CQ DAM Event Recorder]** service.
1. Select the **[!UICONTROL Enable this service]** to enable activity recording.

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. From the **[!UICONTROL Event Types]** list, select the events to be recorded and save the changes.

   >[!CAUTION]
   >
   >Activer les options Ressource affichée, Projets affichés et Collections affichées augmente significativement le nombre d’événements enregistrés.

1. Ouvrez le service **[!UICONTROL DAM Asset Page d&#39;accueil Feature Flag]** à partir de Configuration Manager `https://[aem_server]:[port]/system/console/configMgr`.
1. Select the `isEnabled.name` option to enable the Assets Home page feature. Enregistrez les modifications.

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. Open the **[!UICONTROL User Preferences]** dialog, and select **[!UICONTROL Enable Assets Home Page]**. Enregistrez les modifications.

   ![Activer la page d&#39;accueil de ressources dans la boîte de dialogue Préférences utilisateur](assets/Annotation-color.png)

After enabling the Assets Home page, navigate to the Assets user interface either from the Navigation page or access it directly from the URL `https://[aem_server]:[port]/aem/assetshome.html/content/dam`.

![configurer le lien d’expérience dans l’interface utilisateur Ressources](assets/config-experience-link.png)

Click the **[!UICONTROL Click here to configure your experience link]** to add your username, background image, and profile image.

La page d’accueil des ressources inclut les sections suivantes :

* Section Bienvenue
* Section Widget

**Section Bienvenue**

Si votre profil existe, la section Bienvenue affiche pour vous un message de bienvenue. En outre, il affiche votre image de profil et une image de bienvenue (si elle est déjà configurée).

Si votre profil est incomplet, la section Bienvenue affiche un message de bienvenue générique et un espace réservé pour votre image de profil.

**Section Widget**

Cette section s’affiche sous la section Bienvenue et contient des widgets prêts à l’emploi dans les sections suivantes :

* Activité
* Récent
* Découvrez

**Activité**: Sous cette section, le widget **[!UICONTROL Mon Activité]** affiche les activités récentes effectuées par l’utilisateur connecté avec des ressources (y compris des ressources sans rendus), par exemple les téléchargements, les téléchargements, la création de ressources, les modifications, les commentaires, les annotations et les partages.

**Récent**: Le widget **[!UICONTROL Récemment affiché]** sous cette section affiche les entités récemment consultées par l’utilisateur connecté, y compris les dossiers, les collections et les projets.

**Discover**: Le **[!UICONTROL nouveau]** widget sous cette section affiche les ressources et les rendus récemment transférés vers l’instance Ressources.

To enable purging of user activity data, enable the **[!UICONTROL DAM Event Purge Service]** from Configuration Manager. Une fois que vous avez activé ce service, les activités de l’utilisateur connecté dépassant le nombre spécifié sont supprimées par le système.

L’écran de bienvenue fournit des outils d’aide à la navigation, comme des icônes sur la barre d’outils afin d’accéder aux dossiers, aux collections et aux catalogues.

>[!NOTE]
>
>Enabling the [!UICONTROL Day CQ DAM Event Recorder] and [!UICONTROL DAM Event Purge] services increases write operations to JCR and search indexing, which significantly increases the load on the Experience Manager server. La charge supplémentaire sur le serveur Experience Manager peut avoir un impact sur ses performances.

>[!CAUTION]
>
>La capture, le filtrage et la purge des activités utilisateur requises pour la page d&#39;accueil Ressources imposent des frais généraux sur les performances. Par conséquent, les administrateurs doivent configurer la page d’accueil de manière efficace pour les utilisateurs cibles.
>
>Adobe recommande que les administrateurs et les utilisateurs qui effectuent des opérations en masse évitent d’utiliser la fonction de la page d’accueil des ressources pour empêcher l’augmentation des activités de l’utilisateur.  De plus, les administrateurs peuvent exclure les activités d’enregistrement de certains utilisateurs en configurant[!UICONTROL  l’enregistreur d’événement Day CQ DAM][!UICONTROL  à partir du gestionnaire de configuration].
>
>Si vous utilisez la fonction, Adobe recommande que vous planifiez la fréquence de purge par rapport à la charge du serveur.
