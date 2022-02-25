---
title: '"[!DNL Assets] Expérience de page d’accueil"'
description: Personnalisez le [!DNL Experience Manager Assets] Page d’accueil pour une expérience d’écran de bienvenue riche, avec un instantané des activités récentes concernant les ressources.
contentOwner: AG
feature: Developer Tools, Asset Management
role: Admin, User
exl-id: 042bd959-256a-4794-a34d-0848a6b8840d
source-git-commit: e24316cb9495a552960ae0620e4198f10a08b691
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 35%

---

# [!DNL Adobe Experience Manager Assets] Expérience de page d’accueil {#aem-assets-home-page-experience}

Personnalisez le [!DNL Adobe Experience Manager Assets] page d’accueil pour une expérience d’écran de bienvenue riche, y compris un instantané des activités récentes concernant les ressources.

[!DNL Assets] la page d’accueil offre une expérience d’écran de bienvenue riche et personnalisée, qui inclut un instantané des activités récentes, telles que les ressources récemment affichées ou chargées.

Le [!DNL Assets] La page d’accueil est désactivée par défaut. Pour l’activer, procédez comme suit :

1. Ouvrir [!DNL Experience Manager] Configuration Manager `https://[aem_server]:[port]/system/console/configMgr`.
1. Ouvrez le **[!UICONTROL Enregistreur d’événements DAM Day CQ]** service.
1. Sélectionnez la **[!UICONTROL Activer ce service]** pour activer l’enregistrement des activités.

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. Dans la **[!UICONTROL Types d’événement]** sélectionnez les événements à enregistrer et enregistrez les modifications.

   >[!CAUTION]
   >
   >Activer les options Ressource affichée, Projets affichés et Collections affichées augmente significativement le nombre d’événements enregistrés.

1. Ouvrez le **[!UICONTROL Indicateur de fonction de la page d’accueil des ressources DAM]** à partir de Configuration Manager `https://[aem_server]:[port]/system/console/configMgr`.
1. Sélectionnez la `isEnabled.name` pour activer l’option [!DNL Assets] Fonction de page d’accueil. Enregistrez les modifications.

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. Ouvrez le **[!UICONTROL Préférences utilisateur]** et sélectionnez **[!UICONTROL Activer la page d’accueil des ressources]**. Enregistrez les modifications.

   ![Activation de la page d’accueil des ressources dans la boîte de dialogue Préférences utilisateur](assets/Annotation-color.png)

Après avoir activé la variable [!DNL Assets] Page d’accueil, accédez à la [!DNL Assets] l’interface utilisateur soit à partir de la page Navigation, soit à partir de l’URL ; `https://[aem_server]:[port]/aem/assetshome.html/content/dam`.

![Configuration du lien d’expérience sur l’interface utilisateur d’Assets](assets/config-experience-link.png)

Cliquez sur le bouton **[!UICONTROL Cliquez ici pour configurer le lien de votre expérience]** pour ajouter votre nom d’utilisateur, votre image d’arrière-plan et votre image de profil.

Le [!DNL Assets] La page d’accueil comprend les sections suivantes :

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

**Activité**: Dans cette section, la variable **[!UICONTROL Mon activité]** Le widget affiche les activités récentes effectuées par l’utilisateur connecté avec des ressources (y compris des ressources sans rendu), par exemple les chargements, téléchargements, création de ressources, modifications, commentaires, annotations et partages de ressources.

**Récent**: Le **[!UICONTROL Récemment consultés]** sous cette section, le widget affiche les entités récemment consultées par l’utilisateur connecté, y compris les dossiers, les collections et les projets.

**Discover**: Le **[!UICONTROL Nouveau]** Le widget situé sous cette section affiche les ressources et les rendus récemment chargés dans le [!DNL Assets] déploiement.

Pour activer la purge des données d’activité de l’utilisateur, activez l’option **[!UICONTROL Service de purge des événements de la gestion des actifs numériques]** à partir de Configuration Manager. Une fois que vous avez activé ce service, les activités de l’utilisateur connecté dépassant le nombre spécifié sont supprimées par le système.

L’écran de bienvenue fournit des outils d’aide à la navigation, comme des icônes sur la barre d’outils afin d’accéder aux dossiers, aux collections et aux catalogues.

>[!NOTE]
>
>Activation de la variable [!UICONTROL Enregistreur d’événements DAM Day CQ] et [!UICONTROL Purge des événements de la gestion des actifs numériques] Les services augmentent les opérations d’écriture dans JCR et l’indexation de recherche, ce qui augmente considérablement la charge sur la variable [!DNL Experience Manager] serveur. La charge supplémentaire sur le [!DNL Experience Manager] peut avoir un impact sur ses performances.

>[!CAUTION]
>
>Capture, filtrage et purge des activités utilisateur requises pour [!DNL Assets] la page d’accueil impose une surcharge sur les performances. Par conséquent, les administrateurs doivent configurer la page d’accueil de manière efficace pour les utilisateurs cibles.
>
>Adobe recommande que les administrateurs et les utilisateurs qui effectuent des opérations en masse évitent d’utiliser la fonction de la page d’accueil des ressources pour empêcher l’augmentation des activités de l’utilisateur.  De plus, les administrateurs peuvent exclure les activités d’enregistrement de certains utilisateurs en configurant[!UICONTROL  l’enregistreur d’événement Day CQ DAM][!UICONTROL  à partir du gestionnaire de configuration].
>
>Si vous utilisez la fonction, Adobe recommande que vous planifiez la fréquence de purge par rapport à la charge du serveur.
