---
title: Configuration de l’authentification basée sur OAuth2 pour les protocoles de serveur de messagerie Microsoft&reg ; Office 365
description: Configuration de l’authentification basée sur OAuth2 pour les protocoles de serveur de messagerie Microsoft&reg ; Office 365
exl-id: cd3da71f-892c-4fde-905f-71a64fb5d4e4
source-git-commit: 99808cb38c5d376ccb7fb550c5212138890cec11
workflow-type: tm+mt
source-wordcount: '996'
ht-degree: 62%

---

# Intégration aux protocoles de serveur de messagerie Microsoft® Office 365 {#oauth2-support-for-the-microsoft-mail-server-protocols}

Pour permettre aux entreprises de se conformer aux exigences en matière de messagerie sécurisée, AEM Forms propose la prise en charge OAuth 2.0 pour l’intégration aux protocoles de serveur de messagerie Microsoft® Office 365. Vous pouvez utiliser le service d’authentification OAuth 2.0 d’Azure Active Directory (Azure AD) pour vous connecter à différents protocoles tels que IMAP, POP ou SMTP et accéder aux données d’e-mail des utilisateurs d’Office 365. Vous trouverez ci-dessous des instructions étape par étape pour configurer les protocoles du serveur de messagerie Microsoft® Office 365 afin de les authentifier au moyen du service OAuth 2.0 :

1. Connexion à [https://portal.azure.com/](https://portal.azure.com/) et recherchez **Azure Active Directory** dans la barre de recherche et cliquez sur le résultat.
Vous pouvez également accéder directement à [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview).
1. Cliquez sur **Ajouter** > **Enregistrement de l’application** > **Nouvel enregistrement**

   ![Enregistrement de l’application](/help/forms/using/assets/outh_outlook_microsoft_azure.png)

1. Renseignez les informations selon vos besoins puis cliquez sur **Enregistrement**.
   ![Compte pris en charge](/help/forms/using/assets/azure_suuportedaccountype.png)
Dans le cas ci-dessus, L’option **comptes dans n’importe quel répertoire de l’entreprise (n’importe quel Azure AD Directory - à plusieurs clients) et comptes Microsoft® personnels (par exemple, Skype, Xbox)** est sélectionnée.

   >[!NOTE]
   >
   > * Pour **Comptes dans n’importe quel répertoire d’organisation (n’importe quel répertoire Azure AD - multi-tenant)** , Adobe vous recommande d’utiliser un compte de travail plutôt qu’un compte de messagerie personnel.
   > * L’application **Comptes Microsoft® personnels uniquement** n’est pas prise en charge.
   * Adobe recommande d’utiliser la variable **Compte Microsoft® multi-client et personnel** application.

1. Ensuite, accédez à **Certificats et secrets**, cliquez sur **Nouveau secret client** et suivez les étapes sur l’écran pour créer un secret. Veillez à prendre note de cette valeur de secret pour une utilisation ultérieure.

   ![Clé secrète](/help/forms/using/assets/azure_secretkey.png)

1. Pour ajouter des autorisations, accédez à l’application nouvellement créée, puis sélectionnez **Autorisations d’API** > **Ajouter une autorisation** > **Graphique Microsoft®** > **Autorisations déléguées**
1. Cochez les cases à cocher correspondant aux autorisations ci-dessous pour l’application puis cliquez sur **Ajouter une autorisation** :

   * `IMAP.AccessUser.All`
   * `Mail.Read`
   * `offline_access`
   * `POP.AccessAsUser.All`
   * `SMTP.Send`
   * `User.Read`

   ![Autorisation d’API](/help/forms/using/assets/azure_apipermission.png)

1. Sélectionnez **Authentification** > **Ajouter une plateforme** > **Web**, puis, dans la section **URL de redirection**, ajouter l’une des URI ci-dessous (Universal Resource Identifier) comme suit :
   * `https://login.microsoftonline.com/common/oauth2/nativeclient`
   * `http://localhost`

   Dans ce cas, `https://login.microsoftonline.com/common/oauth2/nativeclient` est utilisée comme URI de redirection.

1. Cliquez sur **Configurer** après avoir ajouté chaque URL et configuré vos paramètres en fonction de vos besoins.
   ![URI de redirection](/help/forms/using/assets/azure_redirecturi.png)

   >[!NOTE]
   >
   Il est obligatoire de sélectionner les cases à cocher **Jetons d’accès** et **Jetons d’ID**.

1. Cliquez sur **Présentation** dans le volet de gauche et copiez les valeurs pour **ID d’application (client)**, **ID de répertoire (client)**, et **Secret client** pour une utilisation ultérieure.

   ![Présentation](/help/forms/using/assets/azure_overview.png)

## Génération du code d’autorisation {#generating-the-authorization-code}

Vous devez ensuite générer le code d’autorisation, comme expliqué dans les étapes suivantes :

1. Ouvrez l’URL suivante dans le navigateur après avoir remplacé `clientID` par le `<client_id>` et `redirect_uri` par l’URI de redirection de votre application :

   ```https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=[clientid]&scope=IMAP.AccessAsUser.All%20POP.AccessAsUser.All%20SMTP.Send%20User.Read%20Mail.Read%20offline_access&response_type=code&redirect_uri=[redirect_uri]&prompt=login```

   >[!NOTE]
   >
   S’il existe une application client unique, remplacez `common` avec votre `[tenantid]` dans l’URL suivante pour générer le code d’autorisation : `https://login.microsoftonline.com/[tenantid]/oauth2/v2.0/authorize?client_id=[[clientid]]&scope=IMAP.AccessAsUser.All%20POP.AccessAsUser.All%20SMTP.Send%20User.Read%20Mail.Read%20openid%20offline_access&response_type=code&redirect_uri=[redirect_uri]&prompt=login`

1. Lorsque vous tapez l’URL ci-dessus, vous êtes redirigé(e) vers l’écran de connexion :
   ![Écran de connexion](/help/forms/using/assets/azure_loginscreen.png)

1. Saisissez l’email, puis cliquez sur **Suivant** et l’écran Droits d’accès de l’application s’affiche :

   ![Permettre les autorisations](/help/forms/using/assets/azure_permission.png)

1. Une fois l’autorisation permise, vous êtes redirigé(e) vers une nouvelle URL en tant que : `https://login.microsoftonline.com/common/oauth2/nativeclient?code=<code>&session_state=[session_id]`

1. Copiez la valeur de `<code>` de l’URL ci-dessus à partir de `0.ASY...` vers `&session_state` dans l’URL ci-dessus.

## Générer le jeton d’actualisation {#generating-the-refresh-token}

Ensuite, vous devez générer le jeton d’actualisation, comme expliqué dans les étapes suivantes :

1. Ouvrez l’invite de commande et utilisez la commande cURL suivante pour obtenir le jeton d’actualisation.

1. Remplacez la variable `clientID`, `client_secret`, et `redirect_uri` avec les valeurs de votre application, ainsi que la valeur de `<code>`:

   `curl -H "ContentType application/x-www-form-urlencoded" -d "client_id=[client-id]&scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FPOP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FSMTP.Send%20https%3A%2F%2Foutlook.office.com%2FUser.Read%20https%3A%2F%2Foutlook.office.com%2FMail.Read%20offline_access&code=[code]&grant_type=authorization_code&redirect_uri=[redirect_uri]&client_secret=[secretkey_value]" -X POST https://login.microsoftonline.com/common/oauth2/v2.0/token`

   >[!NOTE]
   >
   Dans une application à client(e) unique, pour générer un jeton d’actualisation, utilisez la commande cURL suivante et remplacez `common` par le `[tenantid]` dans :
   `curl -H "ContentType application/x-www-form-urlencoded" -d "client_id=[client-id]&scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FPOP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FSMTP.Send%20https%3A%2F%2Foutlook.office.com%2FUser.Read%20https%3A%2F%2Foutlook.office.com%2FMail.Read%20offline_access&code=[code]&grant_type=authorization_code&redirect_uri=[redirect_uri]&client_secret=[secretkey_value]" -X POST https://login.microsoftonline.com/[tenantid]/oauth2/v2.0/token`

1. Prenez note du jeton d’actualisation.

## Configurer le service de messagerie électronique avec prise en charge d’OAuth 2.0 {#configureemailservice}

Maintenant, configurez le service de messagerie sur le dernier serveur JEE en vous connectant à l’interface utilisateur d’administration :

1. Accédez à **Accueil** > **Service** > **Application et services** > **Gestion des services** > **Service de messagerie électronique** ; la fenêtre **Service de messagerie de configuration** s’affiche, configurée pour l’authentification de base.

   >[!NOTE]
   >
   Pour activer le service d’authentification oAuth 2.0, il est obligatoire de cocher la case **Si le serveur SMTP requiert une authentification (authentification SMTP)**.

1. Définir **Paramètres d’authentification oAuth 2.0** sur `True`.
1. Copiez les valeurs de **ID client** et **Secret client** à partir du portail Azure.
1. Copiez la valeur du généré **Actualiser le jeton**.
1. Connectez-vous à **Workbench** et recherchez **Email 1.0** dans **Sélecteur d’activités**.
1. Trois options sont disponibles sous Email 1.0 :
   * **Envoyer avec document** : envoie l’e-mail avec des pièces jointes uniques.
   * **Envoyer avec mappage des pièces jointes** : envoie l’e-mail avec plusieurs pièces jointes.
   * **Recevoir** : reçoit un e-mail de l’IMAP.

   >[!NOTE]
   >
   * Le protocole Transport Security possède les valeurs valides suivantes : &#39;blank&#39;, &#39;SSL&#39; ou &#39;TLS&#39;. Définir les valeurs de **SMTP Transport Security** et **Recevoir Transport Security** to **TLS** pour activer le service d’authentification oAuth.
   * Le **protocole POP3** n’est pas pris en charge pour OAuth lors de l’utilisation de points d’entrée d’e-mail.

   ![Paramètres de connexion](/help/forms/using/assets/oauth_connectionsettings.png)

1. Tester l’application en sélectionnant **Envoyer avec document**.
1. Indiquez les adresses **de destination** et **d’expédition**.
1. Appelez l’application et un courrier électronique est envoyé à l’aide de l’authentification 0 Auth 2.0.

   >[!NOTE]
   >
   Si vous souhaitez modifier le paramètre d’authentification Auth 2.0 en authentification de base pour un processus particulier dans un Workbench, vous pouvez définir la variable **Authentification OAuth 2.0** valeur &quot;False&quot; sous **Utiliser les paramètres globaux** dans le **Paramètres de connexion** .

## Pour activer les notifications de tâche oAuth {#enable_oauth_task}

1. Accédez à **Accueil** > **Services** > **Workflow de formulaire** > **Paramètres du serveur** > **Paramètres d’e-mail**.
1. Pour activer les notifications de tâche oAuth, sélectionnez l’option **Activer oAuth**.
1. Copiez les valeurs de **ID client** et **Secret du client** depuis le portail Azure.
1. Copiez la valeur du généré **Actualiser le jeton**.
1. Cliquez sur **Enregistrer** pour enregistrer les détails.

   ![Notification de tâche](/help/forms/using/assets/task_notification.png)

   >[!NOTE]
   >
   Pour en savoir plus sur les notifications de tâche, [cliquez ici](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/manage-endpoints/configuring-email-endpoints.html?lang=fr#create-an-email-endpoint-for-the-complete-task-service).

## Pour configurer le point d’entrée de l’e-mail, {#configure_email_endpoint}

1. Accédez à **Accueil** > **Services** > **Application et services** > **Gestion des points d’entrée**.
1. Pour configurer le point d’entrée de l’e-mail, définissez les **Paramètres d’authentification oAuth 2.0** sur `True`.
1. Copiez les valeurs d’**ID client** et de **Secret client** à partir d’Azure Portal.
1. Copiez la valeur du généré **Actualiser le jeton**.
1. Cliquez sur **Enregistrer** pour enregistrer les détails.

   ![Paramètres de connexion.](/help/forms/using/assets/oauth_emailendpoint.png)

   >[!NOTE]
   >
   Pour plus d’informations sur la configuration des points de fin de courrier électronique, cliquez sur [Configuration d’un point de fin de courrier électronique](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/manage-endpoints/configuring-email-endpoints.html?lang=fr).

## Résolution des problèmes {#troubleshooting}

* Si le service de messagerie ne fonctionne pas correctement, essayez de régénérer la variable `Refresh Token` comme décrit ci-dessus. Le déploiement de la nouvelle valeur prend quelques minutes.

* Erreur lors de la configuration des détails du serveur de messagerie dans le point de fin de courrier électronique à l’aide de Workbench. Essayez de configurer le point de terminaison au moyen de l’interface utilisateur d’administration au lieu de Workbench.
