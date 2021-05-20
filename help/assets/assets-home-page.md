---
title: '[!DNL Assets] Expérience sur la page d’accueil'
description: Personnalisez la  [!DNL Experience Manager Assets] page d’accueil pour une expérience d’écran de bienvenue riche, y compris un instantané des activités récentes concernant les ressources.
contentOwner: AG
feature: Outils de développement, gestion des ressources
role: Administrator, Business Practitioner
exl-id: 042bd959-256a-4794-a34d-0848a6b8840d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 35%

---

# [!DNL Adobe Experience Manager Assets] Expérience de page d’accueil  {#aem-assets-home-page-experience}

Personnalisez la [!DNL Adobe Experience Manager Assets] page d’accueil pour bénéficier d’une expérience d’écran de bienvenue enrichie, y compris un instantané des activités récentes concernant les ressources.

[!DNL Assets] la page d’accueil offre une expérience d’écran de bienvenue riche et personnalisée, qui inclut un instantané des activités récentes, telles que les ressources récemment affichées ou chargées.

La page d’accueil [!DNL Assets] est désactivée par défaut. Pour l’activer, procédez comme suit :

1. Ouvrez [!DNL Experience Manager] Configuration Manager `https://[aem_server]:[port]/system/console/configMgr`.
1. Ouvrez le service **[!UICONTROL Enregistreur d’événements de la gestion des actifs numériques Day CQ]** .
1. Sélectionnez le **[!UICONTROL Activer ce service]** pour activer l’enregistrement des activités.

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. Dans la liste **[!UICONTROL Types d’événement]**, sélectionnez les événements à enregistrer et enregistrez les modifications.

   >[!CAUTION]
   >
   >Activer les options Ressource affichée, Projets affichés et Collections affichées augmente significativement le nombre d’événements enregistrés.

1. Ouvrez le service **[!UICONTROL Indicateur de fonction de page d’accueil des ressources de gestion des actifs numériques]** à partir de Configuration Manager `https://[aem_server]:[port]/system/console/configMgr`.
1. Sélectionnez l’option `isEnabled.name` pour activer la fonction [!DNL Assets] Page d’accueil. Enregistrez les modifications.

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. Ouvrez la boîte de dialogue **[!UICONTROL Préférences utilisateur]**, puis sélectionnez **[!UICONTROL Activer la page d’accueil des ressources]**. Enregistrez les modifications.

   ![Activation de la page d’accueil des ressources dans la boîte de dialogue Préférences utilisateur](assets/Annotation-color.png)

Après avoir activé la [!DNL Assets] page d’accueil, accédez à l’interface utilisateur [!DNL Assets] à partir de la page Navigation ou accédez-y directement à partir de l’URL `https://[aem_server]:[port]/aem/assetshome.html/content/dam`.

![Configuration du lien d’expérience sur l’interface utilisateur d’Assets](assets/config-experience-link.png)

Cliquez sur **[!UICONTROL Cliquez ici pour configurer votre lien d’expérience]** afin d’ajouter votre nom d’utilisateur, votre image d’arrière-plan et votre image de profil.

La [!DNL Assets] page d’accueil comprend les sections suivantes :

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

**Activité** : Dans cette section, le widget  **[!UICONTROL Mon]** activité affiche les activités récentes effectuées par l’utilisateur connecté avec des ressources (y compris des ressources sans rendus), par exemple les chargements de ressources, les téléchargements, la création de ressources, les modifications, les commentaires, les annotations et les partages.

**Récent** : Le widget  **[!UICONTROL Récemment]** affiché sous cette section affiche les entités récemment consultées par l’utilisateur connecté, y compris les dossiers, les collections et les projets.

**Discover** : Le  **** widget situé sous cette section affiche les ressources et les rendus récemment chargés dans le  [!DNL Assets] déploiement.

Pour activer la purge des données d’activité de l’utilisateur, activez le **[!UICONTROL service de purge des événements de gestion des actifs numériques]** à partir de Configuration Manager. Une fois que vous avez activé ce service, les activités de l’utilisateur connecté dépassant le nombre spécifié sont supprimées par le système.

L’écran de bienvenue fournit des outils d’aide à la navigation, comme des icônes sur la barre d’outils afin d’accéder aux dossiers, aux collections et aux catalogues.

>[!NOTE]
>
>L’activation des services [!UICONTROL Day CQ DAM Event Recorder] et [!UICONTROL DAM Event Purge] augmente les opérations d’écriture sur JCR et l’indexation de recherche, ce qui augmente considérablement la charge sur le serveur [!DNL Experience Manager]. La charge supplémentaire sur le serveur [!DNL Experience Manager] peut avoir une incidence sur ses performances.

>[!CAUTION]
>
>La capture, le filtrage et la purge des activités utilisateur requises pour la page d’accueil [!DNL Assets] imposent une surcharge sur les performances. Par conséquent, les administrateurs doivent configurer la page d’accueil de manière efficace pour les utilisateurs cibles.
>
>Adobe recommande que les administrateurs et les utilisateurs qui effectuent des opérations en masse évitent d’utiliser la fonction de la page d’accueil des ressources pour empêcher l’augmentation des activités de l’utilisateur.  De plus, les administrateurs peuvent exclure les activités d’enregistrement de certains utilisateurs en configurant[!UICONTROL  l’enregistreur d’événement Day CQ DAM][!UICONTROL  à partir du gestionnaire de configuration].
>
>Si vous utilisez la fonction, Adobe recommande que vous planifiez la fréquence de purge par rapport à la charge du serveur.
