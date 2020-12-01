---
title: Partage de fichiers à l’aide d’un lien
description: Partagez des fichiers, des dossiers et des collections sous la forme d’une URL.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 1f6da1c69ea3b3c3f07e8ac10fd8e1e9c7208158
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 38%

---


# Partage d’une ressource via un lien {#asset-link-sharing}

[!DNL Adobe Experience Manager Assets] vous permet de partager des ressources, des dossiers et des collections sous forme d’URL avec des collaborateurs dans l’entreprise et des tiers, notamment des partenaires et des fournisseurs. Le partage de ressources au moyen d’un lien est très pratique dans la mesure où il permet à des tiers d’y accéder sans avoir besoin de se connecter au préalable à [!DNL Assets].

>[!PREREQUISITES]
>
>* Vous devez disposer de l’autorisation Modifier l’ACL sur le dossier ou la ressource que vous souhaitez partager en tant que lien.
>* Pour envoyer des courriers électroniques aux utilisateurs, configurez les détails du serveur SMTP dans le service [de messagerie](#configmailservice)Day CQ.


## Partage de ressources {#sharelink}

Pour générer l’URL des fichiers que vous souhaitez partager avec les utilisateurs, utilisez la boîte de dialogue Partage de liens. Les utilisateurs disposant de privilèges d’administrateur ou avec des autorisations de lecture à l’emplacement `/var/dam/share` peuvent afficher les liens partagés avec eux.

1. In the [!DNL Assets] user interface, select the asset to share as a link.
1. From the toolbar, click the **[!UICONTROL Share Link]** ![share assets icon](assets/do-not-localize/assets_share.png).

   Le lien qui sera créé après avoir cliqué sur [!UICONTROL Partager] s’affiche à l’avance dans le champ Lien [!UICONTROL de] partage. Le délai d’expiration par défaut du lien est de 1 jour.

   ![Boîte de dialogue avec le partage de lien](assets/Link-sharing-dialog-box.png)

   *Figure : Boîte de dialogue de partage de fichiers sous forme de lien.*

   >[!NOTE]
   >
   >If you want to share links from your [!DNL Experience Manager] Author deployment to external entities, ensure that you only expose the following URLs (which are used for link sharing) for `GET` requests only. Bloquer d’autres URL pour des raisons de sécurité.
   >
   >* `http://[aem_server]:[port]/linkshare.html`
   >* `http://[aem_server]:[port]/linksharepreview.html`
   >* `http://[aem_server]:[port]/linkexpired.html`


1. Dans [!DNL Experience Manager] l’interface, accédez à **[!UICONTROL Outils]** > **[!UICONTROL Opérations]** > Console **** Web.

1. Open the **[!UICONTROL Day CQ Link Externalizer]** configuration and modify the following properties in the **[!UICONTROL Domains]** field with the values mentioned against `local`, `author`, and `publish`. For the `local` and `author` properties, provide the URL for the local and the author instance respectively. Both `local` and `author` properties have the same value if you run a single [!DNL Experience Manager] author instance. For Publish instances, provide the URL for the [!DNL Experience Manager] publish instance.

1. Dans la zone Adresse électronique de la boîte de dialogue **[!UICONTROL Partage de liens]**, saisissez l’ID de courrier électronique de l’utilisateur avec lequel vous souhaitez partager le lien. Vous pouvez ajouter un ou plusieurs utilisateurs.

   ![Partage de liens vers des ressources directement depuis la boîte de dialogue Partage de lien](assets/Asset-Sharing-LinkShareDialog.png)

   *Figure : Partagez des liens vers des ressources directement à partir de la boîte de dialogue Partage [!UICONTROL de] liens.*

   >[!NOTE]
   >
   >If you enter an email ID of a user that is not a member of your organization, the words [!UICONTROL External User] are prefixed with the email ID of the user.

1. Dans le champ **[!UICONTROL Objet]** , saisissez une ligne d’objet.

1. In the **[!UICONTROL Message]** field, enter an optional message.

1. In the **[!UICONTROL Expiration]** field, specify an expiration date and time for the link to stop working. Par défaut, la date d’expiration est définie sur une semaine à compter de la date à laquelle vous partagez le lien.

   ![Définir la date d’expiration du lien partagé](assets/Set-shared-link-expiration.png)

1. To let users download the original asset along with the renditions, select **[!UICONTROL Allow download of original file]**. Par défaut, les utilisateurs peuvent uniquement télécharger les rendus de la ressource que vous partagez sous forme de lien.

1. Cliquez sur **[!UICONTROL Partager]**. Un message confirme que le lien est partagé avec les utilisateurs par courrier électronique.

1. Pour vue de la ressource partagée, cliquez sur le lien dans le courrier électronique envoyé à l’utilisateur. La ressource partagée s’affiche sur la page **[!UICONTROL Adobe Marketing Cloud]**.

   ![chlimage_1-260](assets/chlimage_1-545.png)

1. Pour générer une prévisualisation de la ressource, cliquez sur la ressource partagée. To close the preview and return to the **[!UICONTROL Marketing Cloud]** page, click **[!UICONTROL Back]** in the toolbar. If you have shared a folder, click **[!UICONTROL Parent Folder]** to return to the parent folder.

   ![chlimage_1-261](assets/chlimage_1-546.png)

   >[!NOTE]
   >
   >[!DNL Experience Manager] prend en charge la génération de la prévisualisation des ressources uniquement pour [les types](/help/assets/assets-formats.md)de fichiers pris en charge. Si d’autres types MIME sont partagés, vous pouvez uniquement télécharger les ressources et ne pouvez pas les prévisualisation.

1. To download the shared asset, click **[!UICONTROL Select]** from the toolbar, click the asset, and then click **[!UICONTROL Download]** from the toolbar.

   ![chlimage_1-262](assets/chlimage_1-547.png)

1. Pour vue des ressources que vous avez partagées en tant que liens, accédez à l’interface [!DNL Assets] utilisateur et cliquez sur le [!DNL Experience Manager] logo. Sélectionnez **[!UICONTROL Navigation]**. In the Navigation pane, choose **[!UICONTROL Shared Links]** to display a list of shared assets.

1. To un-share an asset, select it and click **[!UICONTROL Unshare]** from the toolbar. Voici un message de confirmation. L’entrée de la ressource est supprimée de la liste.

## Configuration du service service de messagerie Day CQ {#configmailservice}

1. Dans la [!DNL Experience Manager] page d&#39;accueil, accédez à **[!UICONTROL Outils]** > **[!UICONTROL Opérations]** > Console **** Web.
1. Dans la liste des services, recherchez le **[!UICONTROL service de messagerie Day CQ]**.
1. Click **[!UICONTROL Edit]** beside the service, and configure the following parameters for **[!UICONTROL Day CQ Mail Service]** with the details mentioned against their names:

   * Nom d’hôte du serveur SMTP : nom d’hôte du serveur de messagerie
   * Port du serveur SMTP : port du serveur de messagerie
   * Utilisateur SMTP : nom d’utilisateur du serveur de messagerie
   * Mot de passe SMTP : mot de passe du serveur de messagerie

   ![chlimage_1-263](assets/chlimage_1-548.png)

1. Cliquez sur **[!UICONTROL Enregistrer]**.

## Configuration de la taille maximale des données  {#maxdatasize}

When you download assets from the link shared using the Link Sharing feature, [!DNL Experience Manager] compresses the asset hierarchy from the repository and then returns the asset in a ZIP file. Toutefois, en l’absence de limite à la quantité de données pouvant être compressées dans un fichier ZIP, il est possible que des volumes de données considérables à compresser entraînent des erreurs d’insuffisance de mémoire dans JVM. Afin de protéger le système contre une potentielle attaque par déni de service (DoS) résultant de cette situation, configurez la taille maximale à l’aide du paramètre **[!UICONTROL Taille max. de contenu (sans compression)]** pour le servlet proxy du partage de ressource adhoc de la gestion des ressources numériques Day CQ dans le gestionnaire de configuration.  Si la taille non compressée de la ressource dépasse la valeur configurée, les demandes de téléchargement sont rejetées. La valeur par défaut est de 100 Mo.

1. Click the [!DNL Experience Manager] logo and then go to **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
1. From the Web Console, locate the **[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]** configuration.
1. Ouvrez la configuration **[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]** en mode d’édition, puis modifiez la valeur du paramètre **[!UICONTROL Taille max. de contenu (sans compression)]**.

   ![chlimage_1-264](assets/chlimage_1-549.png)

1. Enregistrez les modifications.

## Bonnes pratiques et résolution des problèmes {#bestpractices}

* Les collections ou les dossiers de ressources dont le nom contient un espace blanc risquent de ne pas être partagés.
* If users cannot download the shared assets, check with your [!DNL Experience Manager] administrator what the [download limits](#maxdatasize) are.
* If you cannot send email with links to shared assets or if the other users cannot receive your email, check with your [!DNL Experience Manager] administrator if the [email service](#configmailservice) is configured or not.
* Si vous ne pouvez pas partager des fichiers à l’aide de la fonctionnalité de partage de liens, assurez-vous que vous disposez des autorisations appropriées. Voir [Partager des fichiers](#sharelink).
* Si une ressource partagée est déplacée vers un autre emplacement, son lien cesse de fonctionner. Recréez ce lien et partagez-le de nouveau avec les utilisateurs.
