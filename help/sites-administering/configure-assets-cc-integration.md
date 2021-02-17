---
title: Configuration de l’intégration d’AEM Assets avec Experience Cloud et Creative Cloud
seo-title: Configuration de l’intégration d’AEM Assets avec Marketing Cloud et Creative Cloud
description: Découvrez comment configurer l’intégration d’AEM Assets avec Marketing Cloud et Creative Cloud.
seo-description: Découvrez comment configurer l’intégration d’AEM Assets avec Marketing Cloud et Creative Cloud.
uuid: ec36ea0e-607f-4c73-89df-e095067fccd4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 82a8e807-a2df-4fe3-a68c-2dabc9328eca
docset: aem65
translation-type: tm+mt
source-git-commit: 0560eb8e3c127964920827609a9982acf07b515f
workflow-type: tm+mt
source-wordcount: '1410'
ht-degree: 68%

---


# Configuration de l’intégration d’AEM Assets avec Experience Cloud et Creative Cloud {#configure-aem-assets-integration-with-experience-cloud-and-creative-cloud}

Si vous êtes un client Adobe Experience Cloud, vous pouvez synchroniser vos ressources dans Adobe Experience Manager Assets avec Adobe Creative Cloud, et vice versa. Vous pouvez également synchroniser vos ressources avec Experience Cloud et vice versa. Vous pouvez configurer cette synchronisation via [!DNL Adobe I/O].

Le workflow pour configurer cette intégration est le suivant :

1. Créez une authentification dans [!DNL Adobe I/O] à l&#39;aide d&#39;une passerelle publique et obtenez un ID de l&#39;application.
1. Créez un profil sur votre instance AEM Assets à l’aide du ID de l&#39;application.
1. Utilisez cette configuration pour synchroniser vos ressources dans AEM Assets avec Creative Cloud.

En arrière-plan, le serveur AEM authentifie votre profil avec la passerelle, puis synchronise les données entre AEM Assets et Marketing Cloud.

>[!CAUTION]
>
>La fonctionnalité de partage de dossiers d’AEM vers Creative Cloud est obsolète dans AEM Assets. En savoir plus et recherchez des remplacements dans [Bonnes pratiques en matière d&#39;intégration AEM et Creative Cloud](/help/assets/aem-cc-integration-best-practices.md).

![Flux des données lorsque AEM Assets et Creative Cloud sont intégrés](assets/chlimage_1-48.png)

Flux des données lorsque AEM Assets et Creative Cloud sont intégrés

>[!NOTE]
>
>Le partage de ressources entre Adobe Experience Cloud et Creative Cloud nécessite des privilèges d’administrateur sur l’instance AEM.

>[!CAUTION]
>
>Adobe Marketing Cloud a été rebaptisé Adobe Experience Cloud. Les procédures ci-dessous mentionnent toujours Marketing Cloud afin de refléter l’interface actuelle. Ces mentions seront modifiées ultérieurement.

## Création d’une application {#create-an-application}

1. Accédez à l&#39;interface de passerelle Adobe Developer en vous connectant à [https://legacy-oauth.cloud.adobe.io](https://legacy-oauth.cloud.adobe.io/).

   >[!NOTE]
   >
   >Vous devez disposer de droits d’administrateur pour créer un ID d’application.

1. Dans le volet de gauche, accédez à **[!UICONTROL Outils de développement]** > **[!UICONTROL Applications]** pour vue d&#39;une liste d&#39;applications.
1. Cliquez sur **[!UICONTROL Ajouter]** ![aem_assets_addcircle_icon](assets/aem_assets_addcircle_icon.png) pour créer une application.
1. Dans la liste **[!UICONTROL Informations d’identification du client]**, sélectionnez **[!UICONTROL Compte de service (déclaration JWT)]**, qui est un service de communication serveur à serveur pour l’authentification de serveur.

   ![chlimage_1-49](assets/chlimage_1-49.png)

1. Spécifiez le nom de l’application et une description facultative.
1. Dans la liste **[!UICONTROL Organisation]**, sélectionnez l’organisation pour laquelle vous souhaitez synchroniser les ressources.
1. Dans la liste **[!UICONTROL Scope]**, sélectionnez **[!UICONTROL dam-read]**, **[!UICONTROL dam-sync]**, **[!UICONTROL dam-write]** et **[!UICONTROL cc-share]**.
1. Cliquez sur **[!UICONTROL Créer]**. Un message indique que l’application a été créée.

   ![Notification de réussite de création de l’application pour intégrer AEM Assets avec Adobe CC](assets/chlimage_1-50.png)

1. Copiez l’**[!UICONTROL ID d’application]** généré pour la nouvelle application.

   >[!CAUTION]
   >
   >Assurez-vous de ne pas copier par inadvertance le **[!UICONTROL secret d’application]** au lieu de l’**[!UICONTROL ID d’application.]**.

## Ajout d’une nouvelle configuration à Marketing Cloud {#add-a-new-configuration-to-marketing-cloud}

1. Cliquez sur le logo AEM sur l’interface utilisateur de votre instance AEM Assets locale et accédez à **[!UICONTROL Outils]** > **[!UICONTROL Déploiement]** > **[!UICONTROL Services cloud hérités]**.

1. Recherchez le service **[!UICONTROL Adobe Marketing Cloud]**. S’il n’existe aucune configuration, cliquez sur **[!UICONTROL Configurer maintenant]**. Si des configurations existent, cliquez sur **[!UICONTROL Afficher les configurations]** et sur `+` pour ajouter une nouvelle configuration.

   >[!NOTE]
   >
   >Utilisez un compte Adobe ID pourvu de droits d’administrateur pour l’organisation.

1. Dans la boîte de dialogue **[!UICONTROL Créer une configuration]**, indiquez un titre et un nom pour la nouvelle configuration et cliquez sur **[!UICONTROL Créer]**.

   ![Définition du nom d’une nouvelle configuration pour intégrer AEM Assets et CC](assets/chlimage_1-51.png)

1. Dans le champ **[!UICONTROL URL du client]**, spécifiez l’URL d’AEM Assets.

   >[!CAUTION]
   >
   >En raison d’une nouvelle identité graphique, si vous avez saisi l’URL du client en tant que `https://<tenant_id>.marketing.adobe.com`, vous devez la remplacer par `https://<tenant_id>.experiencecloud.adobe.com.` Pour ce faire, procédez comme suit :
   >
   >1. Accédez à **Outils > Cloud Services > Ancienne version de Cloud Services**.
   1. Sous Adobe Marketing Cloud, cliquez sur **Afficher les configurations**.
   1. Sélectionnez la configuration créée lors de la configuration de la synchronisation AEM-MAC-CC.
   1. Modifiez la configuration du service de cloud et remplacez **marketing.adobe.com** dans le champ URL du client par **experience.adobe.com**.
   1. Enregistrez la configuration.
   1. Testez les agents de réplication mac-sync.


1. Dans le champ **[!UICONTROL ID client]**, collez l’ID d’application que vous avez copié à la fin de la procédure [Création d’une application](/help/sites-administering/configure-assets-cc-integration.md#create-an-application).

   ![Indication des valeurs d’ID d’application requises pour intégrer AEM Assets et Creative Cloud](assets/cloudservices_tenant_info.png)

1. Sous **[!UICONTROL Synchronisation]** sélectionnez **[!UICONTROL Activé]** pour activer la synchronisation et cliquez sur **[!UICONTROL OK]**.

   >[!NOTE]
   Si vous sélectionnez **Désactivé**, la synchronisation opère dans une seule direction.

1. Sur la page de configuration, cliquez sur **[!UICONTROL Afficher la clé publique]** afin d’afficher la clé publique générée pour votre instance. Vous pouvez également cliquer sur **[!UICONTROL Télécharger la clé publique pour la passerelle OAuth]** pour télécharger le fichier contenant la clé publique. Ouvrez ensuite le fichier pour afficher la clé publique.

## Activation de la synchronisation  {#enable-synchronization}

1. Affichez la clé publique à l&#39;aide de l&#39;une des méthodes suivantes mentionnées à la dernière étape de la procédure [Ajoutez une nouvelle configuration à Marketing Cloud](/help/sites-administering/configure-assets-cc-integration.md#add-a-new-configuration-to-marketing-cloud). Cliquez sur **[!UICONTROL Afficher la clé publique]**.

   ![chlimage_1-52](assets/chlimage_1-52.png)

1. Copiez la clé publique et collez-la dans le champ **[!UICONTROL Clé publique]** de l’interface de configuration de l’application que vous avez créée dans la section [Création d’une application](/help/sites-administering/configure-assets-cc-integration.md#create-an-application).

   ![chlimage_1-53](assets/chlimage_1-53.png)

1. Cliquez sur **[!UICONTROL Mettre à jour]**. Synchronisez vos ressources avec l’instance AEM Assets maintenant.

## Test de la synchronisation {#test-the-synchronization}

1. Cliquez sur le logo de l&#39;AEM dans l&#39;interface utilisateur de votre instance AEM Assets locale et accédez à **[!UICONTROL Outils&lt;a1/&quot;**[!UICONTROL  Déploiement ]****[!UICONTROL Réplication]**pour localiser les profils de réplication créés pour la synchronisation.]**
1. Sur la page **[!UICONTROL Réplication]**, cliquez sur **[!UICONTROL Agents sur author]**.
1. Dans la liste des profils, cliquez sur le profil de réplication par défaut de votre organisation pour l’ouvrir.
1. Dans la boîte de dialogue, cliquez sur **[!UICONTROL Tester la connexion]**.

   ![Test de la connexion et définition du profil de réplication par défaut pour votre organisation](assets/chlimage_1-54.png)

1. Une fois le test de réplication terminé, recherchez le message de réussite à la fin des résultats des tests.

## Ajout d’utilisateurs à Marketing Cloud {#add-users-to-marketing-cloud}

1. Connectez-vous à Marketing Cloud avec les informations d’identification de l’administrateur.
1. A partir des rails, accédez à **[!UICONTROL Administration]**, puis cliquez/appuyez sur **[!UICONTROL Démarrer Enterprise Tableau de bord]**.
1. Sur le rail, cliquez sur **[!UICONTROL Utilisateurs]** pour ouvrir la page **[!UICONTROL Gestion des utilisateurs]**.
1. Dans la barre d’outils, cliquez/appuyez sur **Ajouter** ![aem_assets_add_icon](assets/aem_assets_add_icon.png).
1. Ajoutez un ou plusieurs utilisateurs auxquels vous souhaitez offrir la possibilité de partager des ressources avec Creative Cloud.

   >[!NOTE]
   Seuls les utilisateurs que vous ajoutez à Marketing Cloud peuvent partager des ressources depuis AEM Assets vers Creative Cloud.

## Échange de ressources entre AEM Assets et Marketing Cloud  {#exchange-assets-between-aem-assets-and-marketing-cloud}

1. Connectez-vous à AEM Assets.
1. Dans la console Assets, créez un dossier et téléchargez des ressources vers ce dossier. Par exemple, créez un dossier **mc-demo** et téléchargez une ressource vers ce dossier.
1. Sélectionnez le dossier et cliquez sur **Partager** ![assets_share](assets/assets_share.png).
1. Dans le menu, sélectionnez **[!UICONTROL Adobe Marketing Cloud]**, puis cliquez sur **[!UICONTROL Partagé]**. Un message indique que le dossier est partagé avec Marketing Cloud.

   ![chlimage_1-55](assets/chlimage_1-55.png)

   >[!NOTE]
   Partager un dossier de ressources du type `sling:OrderedFolder` n’est pas pris en charge dans le cadre du partage dans Adobe Marketing Cloud. Si vous souhaitez partager un dossier, lors de sa création dans AEM Assets, ne sélectionnez pas l’option **[!UICONTROL Ordre]**.

1. Actualisez l’interface utilisateur AEM Assets. Le dossier que vous avez créé dans la console Ressources de votre instance AEM Assets locale est copié dans l’interface utilisateur du Marketing Cloud. La ressource que vous téléchargez dans le dossier en AEM Assets s’affiche dans la copie du dossier dans le Marketing Cloud après son traitement par le serveur AEM.
1. Vous pouvez également télécharger une ressource dans la copie répliquée du dossier dans Marketing Cloud. Une fois qu’elle a été traitée, la ressource s’affiche dans le dossier partagé dans AEM Assets.

## Échange de ressources entre AEM Assets et Creative Cloud  {#exchange-assets-between-aem-assets-and-creative-cloud}

>[!CAUTION]
La fonction de partage de dossiers entre AEM et Creative Cloud est obsolète. Il est vivement conseillé aux clients d’utiliser des fonctionnalités plus récentes, telles que [Adobe Asset Link](https://helpx.adobe.com/fr/enterprise/using/adobe-asset-link.html) ou [AEM application de bureau](https://helpx.adobe.com/fr/experience-manager/desktop-app/aem-desktop-app.html). En savoir plus sur les [meilleures pratiques d’intégration d’AEM et de Creative Cloud](/help/assets/aem-cc-integration-best-practices.md).

AEM Assets permet de partager des dossiers comportant des ressources avec les utilisateurs d’Adobe Creative Cloud.

1. Dans la console Assets, sélectionnez le fichier à partager avec Creative Cloud.
1. Dans la barre d’outils, cliquez sur **[!UICONTROL Partager]** ![assets_share](assets/assets_share.png).
1. Dans la liste, sélectionnez l’option **[!UICONTROL Adobe Creative Cloud]**.

   >[!NOTE]
   Les options sont disponibles pour les utilisateurs possédant des autorisations de lecture sur la racine. Les utilisateurs doivent bénéficier de l’autorisation requise pour accéder aux informations de l’agent de réplication de Marketing Cloud.

1. Dans la page **[!UICONTROL Partage de Creative Cloud]**, ajoutez l’utilisateur avec lequel partager le dossier et choisissez un rôle pour l’utilisateur. Cliquez sur **[!UICONTROL Enregistrer]** et sur **[!UICONTROL OK]**.

1. Connectez-vous à Creative Cloud avec les informations d’identification de l’utilisateur avec lequel vous avez partagé le dossier. Le dossier partagé est disponible dans Creative Cloud.

La synchronisation AEM Assets-Marketing Cloud est conçue de manière à ce que l’instance de machine utilisateur à partir de laquelle la ressource est téléchargée conserve le droit de modifier la ressource. Seules ces modifications sont propagées vers l’autre instance.

Par exemple, si une ressource est téléchargée d’une instance AEM Assets (sur site), les modifications apportées à la ressource à partir de cette instance sont propagées à l’instance Marketing Cloud. Cependant, les modifications effectuées de l’instance de Marketing Cloud à la même ressource ne sont pas propagées à l’instance AEM et vice versa pour la ressource téléchargée à partir du Marketing Cloud.

>[!MORELIKETHIS]
* [Meilleures pratiques d’intégration d’AEM et de Creative Cloud](/help/assets/aem-cc-integration-best-practices.md)
* [Meilleures pratiques de partage de dossiers entre AEM et Creative Cloud](/help/assets/aem-cc-folder-sharing-best-practices.md)

