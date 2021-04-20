---
title: '[!DNL Assets] Expérience page d''accueil'
description: Personnalisez la  [!DNL Experience Manager Assets] Page d'accueil pour une expérience d’écran de bienvenue enrichie, y compris un instantané des activités récentes relatives aux ressources.
contentOwner: AG
feature: Developer Tools, Asset Management
role: Administrator, Business Practitioner
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 35%

---


# [!DNL Adobe Experience Manager Assets] Expérience de page d&#39;accueil  {#aem-assets-home-page-experience}

Personnalisez la page d&#39;accueil [!DNL Adobe Experience Manager Assets] pour obtenir une expérience d’écran de bienvenue enrichie, y compris un instantané des activités récentes relatives aux ressources.

[!DNL Assets] La page d&#39;accueil offre une expérience d’écran de bienvenue riche et personnalisée, qui comprend un instantané des activités récentes, telles que les ressources récemment affichées ou téléchargées.

La page d&#39;accueil [!DNL Assets] est désactivée par défaut. Pour l’activer, procédez comme suit :

1. Ouvrez [!DNL Experience Manager] Configuration Manager `https://[aem_server]:[port]/system/console/configMgr`.
1. Ouvrez le service **[!UICONTROL Day CQ DAM Événement Recorder]**.
1. Sélectionnez **[!UICONTROL Activer ce service]** pour activer l&#39;enregistrement des activités.

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. Dans la liste **[!UICONTROL Types d&#39;événement]**, sélectionnez les événements à enregistrer et enregistrez les modifications.

   >[!CAUTION]
   >
   >Activer les options Ressource affichée, Projets affichés et Collections affichées augmente significativement le nombre d’événements enregistrés.

1. Ouvrez le service **[!UICONTROL DAM Asset Page d&#39;accueil Feature Flag]** à partir de Configuration Manager `https://[aem_server]:[port]/system/console/configMgr`.
1. Sélectionnez l&#39;option `isEnabled.name` pour activer la fonction de Page d&#39;accueil [!DNL Assets]. Enregistrez les modifications.

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. Ouvrez la boîte de dialogue **[!UICONTROL Préférences utilisateur]**, puis sélectionnez **[!UICONTROL Activer la Page d&#39;accueil des ressources]**. Enregistrez les modifications.

   ![Activer la page d&#39;accueil de ressources dans la boîte de dialogue Préférences utilisateur](assets/Annotation-color.png)

Après avoir activé la Page d&#39;accueil [!DNL Assets], accédez à l&#39;interface utilisateur [!DNL Assets] à partir de la page Navigation ou accédez-y directement à partir de l&#39;URL `https://[aem_server]:[port]/aem/assetshome.html/content/dam`.

![configurer le lien d’expérience dans l’interface utilisateur Ressources](assets/config-experience-link.png)

Cliquez sur **[!UICONTROL Cliquez ici pour configurer votre lien d’expérience]** afin d’ajouter votre nom d’utilisateur, votre image d’arrière-plan et votre image de profil.

La Page d&#39;accueil [!DNL Assets] comprend les sections suivantes :

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

**Activité** : Sous cette section, le  **[!UICONTROL widget]** Mon activité affiche les récentes activités effectuées par l’utilisateur connecté avec des ressources (y compris des ressources sans rendus), par exemple les téléchargements, les téléchargements, la création de ressources, les modifications, les commentaires, les annotations et les partages.

**Récent** : Le widget  **[!UICONTROL Récemment]** affiché sous cette section affiche les entités récemment consultées par l’utilisateur connecté, y compris les dossiers, les collections et les projets.

**Discover** : Le  **** widget de cette section affiche les ressources et les rendus récemment transférés vers le  [!DNL Assets] déploiement.

Pour activer la purge des données d’activité utilisateur, activez le **[!UICONTROL service de purge de Événement DAM]** à partir de Configuration Manager. Une fois que vous avez activé ce service, les activités de l’utilisateur connecté dépassant le nombre spécifié sont supprimées par le système.

L’écran de bienvenue fournit des outils d’aide à la navigation, comme des icônes sur la barre d’outils afin d’accéder aux dossiers, aux collections et aux catalogues.

>[!NOTE]
>
>L&#39;activation des services [!UICONTROL Day CQ DAM Événement Recorder] et [!UICONTROL DAM Événement Purge] augmente les opérations d&#39;écriture sur le JCR et l&#39;indexation de recherche, ce qui augmente significativement la charge sur le serveur [!DNL Experience Manager]. La charge supplémentaire sur le serveur [!DNL Experience Manager] peut affecter ses performances.

>[!CAUTION]
>
>La capture, le filtrage et la purge des activités utilisateur requises pour la page d&#39;accueil [!DNL Assets] imposent une surcharge sur les performances. Par conséquent, les administrateurs doivent configurer la page d’accueil de manière efficace pour les utilisateurs cibles.
>
>Adobe recommande que les administrateurs et les utilisateurs qui effectuent des opérations en masse évitent d’utiliser la fonction de la page d’accueil des ressources pour empêcher l’augmentation des activités de l’utilisateur.  De plus, les administrateurs peuvent exclure les activités d’enregistrement de certains utilisateurs en configurant[!UICONTROL  l’enregistreur d’événement Day CQ DAM][!UICONTROL  à partir du gestionnaire de configuration].
>
>Si vous utilisez la fonction, Adobe recommande que vous planifiez la fréquence de purge par rapport à la charge du serveur.
