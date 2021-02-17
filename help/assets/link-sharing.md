---
title: Partage de fichiers à l’aide d’un lien
description: Partagez des fichiers, des dossiers et des collections sous la forme d’une URL.
contentOwner: AG
translation-type: tm+mt
source-git-commit: e36d08c9ea89e840aecde79ffdd911372c0c54ee
workflow-type: tm+mt
source-wordcount: '1056'
ht-degree: 39%

---


# Partager une ressource via un lien {#asset-link-sharing}

[!DNL Adobe Experience Manager Assets] vous permet de partager des ressources, des dossiers et des collections sous forme d’URL avec des collaborateurs dans l’entreprise et des tiers, notamment des partenaires et des fournisseurs. Le partage de ressources au moyen d’un lien est très pratique dans la mesure où il permet à des tiers d’y accéder sans avoir besoin de se connecter au préalable à [!DNL Assets].

>[!PREREQUISITES]
>
>* Vous devez disposer de l’autorisation Modifier l’ACL sur le dossier ou la ressource que vous souhaitez partager en tant que lien.
>* Pour envoyer des e-mails aux utilisateurs, configurez les détails du serveur SMTP dans [Service de messagerie Day CQ](#configmailservice).


## Partage de ressources {#sharelink}

Pour générer l’URL des fichiers que vous souhaitez partager avec les utilisateurs, utilisez la boîte de dialogue Partage de liens. Les utilisateurs disposant de privilèges d’administrateur ou avec des autorisations de lecture à l’emplacement `/var/dam/share` peuvent afficher les liens partagés avec eux.

1. Dans l&#39;interface utilisateur [!DNL Assets], sélectionnez la ressource à partager en tant que lien.
1. Dans la barre d’outils, cliquez sur l’icône **[!UICONTROL Partager le lien]** ![partager les ressources](assets/do-not-localize/assets_share.png).

   Le lien qui sera créé après avoir cliqué sur [!UICONTROL Partager] s’affiche à l’avance dans le champ [!UICONTROL Partager le lien]. Le délai d’expiration par défaut du lien est de 1 jour.

   ![Boîte de dialogue avec le partage de lien](assets/Link-sharing-dialog-box.png)

   *Figure : Boîte de dialogue de partage de fichiers sous forme de lien.*

   >[!NOTE]
   >
   >Si vous souhaitez partager des liens de votre déploiement d&#39;auteur [!DNL Experience Manager] vers des entités externes, veillez à n&#39;exposer que les URL suivantes (utilisées pour le partage de liens) pour les requêtes `GET`. Bloquer d’autres URL pour des raisons de sécurité.
   >
   >* `http://[aem_server]:[port]/linkshare.html`
   >* `http://[aem_server]:[port]/linksharepreview.html`
   >* `http://[aem_server]:[port]/linkexpired.html`


1. Dans l&#39;interface [!DNL Experience Manager], accédez à **[!UICONTROL Outils]** > **[!UICONTROL Opérations]** > **[!UICONTROL Console Web]**.

1. Ouvrez la configuration de l&#39;**[!UICONTROL Externalisateur de lien Day CQ]** et modifiez les propriétés suivantes dans le champ **[!UICONTROL Domains]** avec les valeurs mentionnées par rapport à `local`, `author` et `publish`. Pour les propriétés `local` et `author`, indiquez l’URL de l’instance locale et de l’instance d’auteur, respectivement. Les propriétés `local` et `author` ont toutes deux la même valeur si vous exécutez une seule instance d’auteur [!DNL Experience Manager]. Pour les instances de publication, indiquez l’URL de l’instance de publication [!DNL Experience Manager].

1. Dans la zone Adresse électronique de la boîte de dialogue **[!UICONTROL Partage de liens]**, saisissez l’ID de courrier électronique de l’utilisateur avec lequel vous souhaitez partager le lien. Vous pouvez ajouter un ou plusieurs utilisateurs.

   ![Partage de liens vers des ressources directement depuis la boîte de dialogue Partage de lien](assets/Asset-Sharing-LinkShareDialog.png)

   *Figure : Partagez des liens vers des ressources directement à partir de la boîte de dialogue  [!UICONTROL Partage de ] liens.*

   >[!NOTE]
   >
   >Si vous saisissez un ID de courrier électronique d’un utilisateur qui n’est pas membre de votre organisation, les mots [!UICONTROL Utilisateur externe] sont précédés de l’ID de courrier électronique de l’utilisateur.

1. Dans le champ **[!UICONTROL Objet]**, indiquez l’objet de la ressource que vous souhaitez partager.

1. Dans le champ **[!UICONTROL Message]**, vous pouvez saisir un message si vous le souhaitez.

1. Dans le champ **[!UICONTROL Expiration]**, indiquez la date et l’heure d’expiration du lien pour qu’il cesse de fonctionner. Par défaut, la date d’expiration est définie sur une semaine à compter de la date à laquelle vous partagez le lien.

   ![Définir la date d’expiration du lien partagé](assets/Set-shared-link-expiration.png)

1. Pour permettre aux utilisateurs de télécharger le fichier d’origine avec les rendus, sélectionnez **[!UICONTROL Autoriser le téléchargement du fichier d’origine]**. Par défaut, les utilisateurs peuvent uniquement télécharger les rendus de la ressource que vous partagez sous forme de lien.

1. Cliquez sur **[!UICONTROL Partager]**. Un message confirme que le lien est partagé avec les utilisateurs par courrier électronique.

1. Pour vue de la ressource partagée, cliquez sur le lien dans le courrier électronique envoyé à l’utilisateur. La ressource partagée s’affiche sur la page [!UICONTROL Adobe Marketing Cloud].

   ![Les ressources partagées sont disponibles dans Adobe Marketing Cloud](assets/chlimage_1-545.png)

1. Pour générer une prévisualisation de la ressource, cliquez sur la ressource partagée. Pour fermer la prévisualisation et revenir à la page **[!UICONTROL Marketing Cloud]**, cliquez sur **[!UICONTROL Précédent]** dans la barre d’outils. Si vous avez partagé un dossier, cliquez sur **[!UICONTROL Dossier parent]** pour revenir au dossier parent.

   ![chlimage_1-261](assets/chlimage_1-546.png)

   >[!NOTE]
   >
   >[!DNL Experience Manager] prend en charge la génération de la prévisualisation des ressources uniquement pour  [les types](/help/assets/assets-formats.md) de fichiers pris en charge. Si d’autres types MIME sont partagés, vous pouvez uniquement télécharger les ressources et ne pouvez pas les prévisualisation.

1. Pour télécharger la ressource partagée, cliquez sur **[!UICONTROL Sélectionner]** dans la barre d’outils, cliquez sur la ressource, puis sur **[!UICONTROL Télécharger]** dans la barre d’outils.

   ![Option de barre d’outils pour télécharger la ressource partagée](assets/chlimage_1-547.png)

1. Pour vue des ressources que vous avez partagées en tant que liens, accédez à l&#39;interface utilisateur [!DNL Assets] et cliquez sur le logo [!DNL Experience Manager]. Sélectionnez **[!UICONTROL Navigation]**. Dans le volet Navigation, choisissez **[!UICONTROL Liens partagés]** pour afficher une liste de ressources partagées.

1. Pour annuler le partage d’une ressource, sélectionnez-la et cliquez sur **[!UICONTROL Annuler le partage]** dans la barre d’outils. Voici un message de confirmation. L’entrée de la ressource est supprimée de la liste.

## Configuration du service service de messagerie Day CQ {#configmailservice}

1. Sur la page d&#39;accueil [!DNL Experience Manager], accédez à **[!UICONTROL Outils]** > **[!UICONTROL Opérations]** > **[!UICONTROL Console Web]**.
1. Dans la liste des services, recherchez le **[!UICONTROL service de messagerie Day CQ]**.
1. Cliquez sur **[!UICONTROL Modifier]** en regard du service et configurez les paramètres suivants pour **[!UICONTROL Service de messagerie Day CQ]** avec les détails indiqués par rapport à leur nom :

   * Nom d’hôte du serveur SMTP : nom d’hôte du serveur de messagerie
   * Port du serveur SMTP : port du serveur de messagerie
   * Utilisateur SMTP : nom d’utilisateur du serveur de messagerie
   * Mot de passe SMTP : mot de passe du serveur de messagerie

   ![chlimage_1-263](assets/chlimage_1-548.png)

1. Cliquez sur **[!UICONTROL Enregistrer]**.

## Configuration de la taille maximale des données {#maxdatasize}

Lorsque vous téléchargez des ressources à partir du lien partagé à l’aide de la fonction de partage de liens, [!DNL Experience Manager] compresse la hiérarchie des ressources à partir du référentiel, puis renvoie la ressource dans un fichier ZIP. Toutefois, en l’absence de limite à la quantité de données pouvant être compressées dans un fichier ZIP, il est possible que des volumes de données considérables à compresser entraînent des erreurs d’insuffisance de mémoire dans JVM. Afin de protéger le système contre une potentielle attaque par déni de service (DoS) résultant de cette situation, configurez la taille maximale à l’aide du paramètre **[!UICONTROL Taille max. de contenu (sans compression)]** pour le servlet proxy du partage de ressource adhoc de la gestion des ressources numériques Day CQ dans le gestionnaire de configuration.  Si la taille non compressée de la ressource dépasse la valeur configurée, les demandes de téléchargement sont rejetées. La valeur par défaut est de 100 Mo.

1. Cliquez sur le logo [!DNL Experience Manager], puis accédez à **[!UICONTROL Outils]** > **[!UICONTROL Opérations]** > **[!UICONTROL Console Web]**.
1. Dans la console Web, recherchez la configuration du serveur proxy de partage de ressources ad hoc **[!UICONTROL Day CQ DAM]**.
1. Ouvrez la configuration **[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]** en mode d’édition, puis modifiez la valeur du paramètre **[!UICONTROL Taille max. de contenu (sans compression)]**.

   ![chlimage_1-264](assets/chlimage_1-549.png)

1. Enregistrez les modifications.

## Bonnes pratiques et résolution des problèmes {#bestpractices}

* Les collections ou les dossiers de ressources dont le nom contient un espace blanc risquent de ne pas être partagés.
* Si les utilisateurs ne peuvent pas télécharger les ressources partagées, vérifiez auprès de votre administrateur [!DNL Experience Manager] quelles sont les [limites de téléchargement](#maxdatasize).
* Si vous ne pouvez pas envoyer de courrier électronique contenant des liens vers des ressources partagées ou si les autres utilisateurs ne peuvent pas recevoir votre courrier électronique, vérifiez auprès de votre administrateur [!DNL Experience Manager] si le service de messagerie [](#configmailservice) est configuré ou non.
* Si vous ne pouvez pas partager des fichiers à l’aide de la fonctionnalité de partage de liens, assurez-vous que vous disposez des autorisations appropriées. Voir [Partager des fichiers](#sharelink).
* Si une ressource partagée est déplacée vers un autre emplacement, son lien cesse de fonctionner. Recréez ce lien et partagez-le de nouveau avec les utilisateurs.
