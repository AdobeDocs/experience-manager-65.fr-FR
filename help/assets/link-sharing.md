---
title: Partage de ressources à l’aide d’un lien
description: Partagez des ressources, des dossiers et des collections sous la forme d’une URL.
contentOwner: AG
role: User
feature: Link Sharing,Asset Management
exl-id: 20370b00-862e-4d04-af2f-7d1c74a842dd
source-git-commit: aa45839c53cb2c0715c9163847351aa2391309e0
workflow-type: tm+mt
source-wordcount: '1043'
ht-degree: 32%

---

# Partage d’une ressource en tant que lien {#asset-link-sharing}

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Cliquez ici](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/share-assets.html?lang=en) |
| AEM 6.5 | Cet article |
| AEM 6.4 | [Cliquez ici](https://experienceleague.adobe.com/docs/experience-manager-64/assets/administer/link-sharing.html?lang=en) |

[!DNL Adobe Experience Manager Assets] vous permet de partager des ressources, des dossiers et des collections sous forme d’URL avec des collaborateurs dans l’entreprise et des tiers, notamment des partenaires et des fournisseurs. Le partage de ressources par le biais d’un lien est un moyen pratique de mettre des ressources à la disposition de tiers sans qu’ils aient à se connecter au préalable à [!DNL Assets].

>[!PREREQUISITES]
>
>* Vous avez besoin de `Edit ACL` autorisation sur le dossier ou la ressource que vous souhaitez partager en tant que lien.
>* Pour envoyer des emails aux utilisateurs, configurez les détails du serveur SMTP dans [Service de messagerie Day CQ](#configmailservice).


## Partager des ressources {#share-assets}

Pour générer l’URL des ressources que vous souhaitez partager avec les utilisateurs, utilisez le [!UICONTROL Partage de liens] boîte de dialogue.

* Utilisateurs disposant de droits d’administrateur ou disposant d’autorisations de lecture sur `/var/dam/share` L’emplacement peut afficher les liens partagés avec eux.
* Les utilisateurs disposant d’autorisations de lecture sur `/var/dam/jobs/download` L’emplacement peut télécharger des ressources à partir du lien partagé.

1. Dans l’interface utilisateur [!DNL Assets], sélectionnez la ressource à partager sous forme de lien.

1. Dans la barre d’outils, cliquez sur le bouton **[!UICONTROL Partager le lien]** ![icône de partage de ressources](assets/do-not-localize/assets_share.png). Lien qui sera créé après avoir cliqué sur **[!UICONTROL Partager]** s’affiche à l’avance dans la variable [!UICONTROL Partager le lien] champ . Le lien n’est pas créé tant que vous n’avez pas sélectionné **[!UICONTROL Envoyer]**.

   ![Boîte de dialogue avec le partage de lien](assets/share-assets-as-link.png)

   *Figure : Boîte de dialogue permettant de partager des ressources sous la forme d’un lien.*

1. Dans la zone Adresse e-mail de la boîte de dialogue **[!UICONTROL Partage de liens]**, saisissez l’ID de courrier électronique de l’utilisateur avec lequel vous souhaitez partager le lien. Vous pouvez ajouter un ou plusieurs utilisateurs.

   >[!NOTE]
   >
   >Si vous saisissez un ID de courrier électronique d’un utilisateur qui n’est pas membre de votre organisation, les mots [!UICONTROL Utilisateur externe] sont précédés de l’e-mail de l’utilisateur.

1. Dans le champ **[!UICONTROL Objet]**, indiquez l’objet de la ressource que vous souhaitez partager.

1. Dans le champ **[!UICONTROL Message]**, vous pouvez saisir un message si vous le souhaitez.

1. Dans le **[!UICONTROL Expiration]** , indiquez une date et une heure d’expiration pour que le lien cesse de fonctionner. Le délai d’expiration par défaut du lien est de 1 jour.

   ![Définition de la date d’expiration du lien partagé](assets/Set-shared-link-expiration.png)

1. Pour permettre aux utilisateurs de télécharger la ressource d’origine, sélectionnez **[!UICONTROL Autoriser le téléchargement du fichier d’origine]**. Pour permettre aux utilisateurs de télécharger uniquement les rendus des ressources partagées, sélectionnez **[!UICONTROL Autorisation du téléchargement des rendus du fichier]**.

1. Cliquez sur **[!UICONTROL Partager]**. Un message confirme le partage du lien avec les utilisateurs par email.

1. Pour afficher la ressource partagée, cliquez sur le lien contenu dans le courrier électronique envoyé à l’utilisateur. Pour générer un aperçu de la ressource, cliquez sur la ressource partagée. Pour fermer l’aperçu, cliquez sur **[!UICONTROL Précédent]**. Si vous avez partagé un dossier, cliquez sur **[!UICONTROL Dossier parent]** pour revenir au dossier parent.

   ![Aperçu de la ressource partagée](assets/chlimage_1-546.png)

   >[!NOTE]
   >
   >[!DNL Experience Manager] prend en charge la génération de l’aperçu des ressources de uniquement [les types de fichiers pris en charge ;](/help/assets/assets-formats.md). Si d’autres types MIME sont partagés, vous ne pouvez télécharger que les ressources et ne pouvez pas les prévisualiser.

1. Pour télécharger la ressource partagée, cliquez sur **[!UICONTROL Sélectionner]** dans la barre d’outils, cliquez sur la ressource, puis sur **[!UICONTROL Télécharger]** dans la barre d’outils.

   ![Option de barre d’outils pour télécharger la ressource partagée](assets/chlimage_1-547.png)

1. Pour afficher les ressources que vous avez partagées en tant que liens, accédez à la [!DNL Assets] de l’interface utilisateur, puis cliquez sur [!DNL Experience Manager] logo. Choisir **[!UICONTROL Navigation]**. Dans le volet de navigation, choisissez **[!UICONTROL Liens partagés]** pour afficher une liste des ressources partagées.

1. Pour annuler le partage d’une ressource, sélectionnez-la et cliquez sur **[!UICONTROL Annuler le partage]** dans la barre d’outils. Voici un message de confirmation. L’entrée de la ressource est supprimée de la liste.

## Configuration du service de messagerie Day CQ {#configure-day-cq-mail-service}

1. Sur le [!DNL Experience Manager] page d’accueil, accédez à **[!UICONTROL Outils]** > **[!UICONTROL Opérations]** > **[!UICONTROL Console web]**.
1. Dans la liste des services, recherchez le **[!UICONTROL service de messagerie Day CQ]**.
1. Cliquez sur **[!UICONTROL Modifier]** en regard du service et configurez les paramètres suivants pour **[!UICONTROL Service de messagerie Day CQ]** avec les détails mentionnés par rapport à leur nom :

   * Nom d’hôte du serveur SMTP : nom d’hôte du serveur de messagerie
   * Port du serveur SMTP : port du serveur de messagerie
   * Utilisateur SMTP : nom d’utilisateur du serveur de messagerie
   * Mot de passe SMTP : mot de passe du serveur de messagerie

   ![chlimage_1-263](assets/chlimage_1-548.png)

1. Cliquez sur **[!UICONTROL Enregistrer]**.

## Configuration de la taille maximale des données {#configure-maximum-data-size}

Lorsque vous téléchargez des ressources à partir du lien partagé à l’aide de la fonction Partage de lien , [!DNL Experience Manager] compresse la hiérarchie des ressources du référentiel, puis renvoie la ressource dans un fichier ZIP. Toutefois, en l’absence de limite à la quantité de données pouvant être compressées dans un fichier ZIP, il est possible que des volumes de données considérables à compresser entraînent des erreurs d’insuffisance de mémoire dans JVM. Afin de protéger le système contre une potentielle attaque par déni de service (DoS) résultant de cette situation, configurez la taille maximale à l’aide du paramètre **[!UICONTROL Taille max. de contenu (sans compression)]** pour le servlet proxy du partage de ressource adhoc de la gestion des ressources numériques Day CQ dans le gestionnaire de configuration. **** Si la taille non compressée de la ressource dépasse la valeur configurée, les demandes de téléchargement sont rejetées. La valeur par défaut est de 100 Mo.

1. Cliquez sur le bouton [!DNL Experience Manager] puis accédez à **[!UICONTROL Outils]** > **[!UICONTROL Opérations]** > **[!UICONTROL Console web]**.
1. Dans la console Web, recherchez la variable **[!UICONTROL Servlet proxy de partage de ressources ad hoc de la gestion des actifs numériques Day CQ]** configuration.
1. Ouvrez la configuration **[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]** en mode d’édition, puis modifiez la valeur du paramètre **[!UICONTROL Taille max. de contenu (sans compression)]**.

   ![chlimage_1-264](assets/chlimage_1-549.png)

1. Enregistrez les modifications.

## Bonnes pratiques et résolution des problèmes {#best-practices-and-troubleshooting}

* Les collections ou les dossiers de ressources dont le nom contient un espace blanc risquent de ne pas être partagés.
* Si les utilisateurs ne peuvent pas télécharger les ressources partagées, contactez votre [!DNL Experience Manager] l’administrateur [limites de téléchargement](#configure-maximum-data-size) sont .
* Si vous ne pouvez pas envoyer de courrier électronique contenant des liens vers des ressources partagées ou si les autres utilisateurs ne peuvent pas recevoir votre courrier électronique, contactez votre [!DNL Experience Manager] Si la variable [service de messagerie électronique](#configure-day-cq-mail-service) est configuré ou non.
* Si vous ne pouvez pas partager des fichiers à l’aide de la fonctionnalité de partage de liens, assurez-vous que vous disposez des autorisations appropriées. Voir [Partager des fichiers](#share-assets).
* Si une ressource partagée est déplacée vers un autre emplacement, son lien cesse de fonctionner. Recréez ce lien et partagez-le de nouveau avec les utilisateurs.

* Si vous souhaitez partager des liens à partir de votre [!DNL Experience Manager] Déploiement de l’auteur vers des entités externes, veillez à n’exposer que les URL suivantes utilisées pour le partage de liens, pour `GET` demandes uniquement. Bloquez d’autres URL pour des raisons de sécurité.

   * `http://[aem_server]:[port]/linkshare.html`
   * `http://[aem_server]:[port]/linksharepreview.html`
   * `http://[aem_server]:[port]/linkexpired.html`
   Dans [!DNL Experience Manager] interface, accès **[!UICONTROL Outils]** > **[!UICONTROL Opérations]** > **[!UICONTROL Console web]**. Ouvrez le **[!UICONTROL Externalisateur de lien Day CQ]** et modifiez les propriétés suivantes dans le **[!UICONTROL Domaines]** avec les valeurs mentionnées par rapport à `local`, `author`, et `publish`. Pour le `local` et `author` , indiquez l’URL des instances locale et d’auteur, respectivement. Si vous exécutez une seule [!DNL Experience Manager] Instance de création, utiliser la même valeur pour `local` et `author` propriétés. Pour les instances de publication, indiquez l’URL de la variable [!DNL Experience Manager] Instance de publication.
