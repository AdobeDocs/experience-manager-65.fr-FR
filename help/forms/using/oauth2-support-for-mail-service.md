---
title: Prise en charge d’OAuth2 pour les protocoles de serveur de messagerie Microsoft® Office 365
description: Prise en charge Oauth2 des protocoles de serveur de messagerie Microsoft® Office 365
source-git-commit: 85189a4c35d1409690cbb93946369244e8848340
workflow-type: tm+mt
source-wordcount: '940'
ht-degree: 3%

---

# Prise en charge d’OAuth 2.0 pour les protocoles de serveur de messagerie Microsoft® Office 365 {#oauth2-support-for-the-microsoft-mail-server-protocols}

AEM Forms offre une prise en charge OAuth 2.0 pour l’intégration aux protocoles de serveur de messagerie Microsoft® Office 365, afin de permettre aux entreprises de se conformer aux exigences de messagerie sécurisée. Azure Principale Directory (Azure AD) offre un service d’authentification OAuth 2.0, qui permet à votre application de se connecter à divers protocoles tels que IMAP, POP ou SMTP, et d’accéder aux données d’e-mail pour les utilisateurs d’Office 365.

Vous trouverez ci-dessous des instructions étape par étape pour configurer les protocoles du serveur de messagerie Microsoft® Office 365 pour s’authentifier via le service OAuth 2.0 :

1. Connexion [https://portal.azure.com/](https://portal.azure.com/) et recherchez **Azure Principal Directory** dans la barre de recherche et cliquez sur le résultat.
Vous pouvez également accéder directement à [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)
1. Cliquez sur **Ajouter** > **Enregistrement de l’application** > **Nouvelle inscription**

   ![Enregistrement de l’application](/help/forms/using/assets/outh_outlook_microsoft_azure.png)

1. Renseignez les informations en fonction de vos besoins, puis cliquez sur **Enregistrer**.
   ![Compte pris en charge](/help/forms/using/assets/azure_suuportedaccountype.png)


   Dans le cas ci-dessus, **Comptes dans n’importe quel annuaire de l’entreprise (un annuaire Azure AD - multi-client) et comptes Microsoft® personnels (par exemple, Skype, Xbox)** est sélectionnée.

   >[!NOTE]
   >
   > * Pour **Comptes dans n’importe quel répertoire d’organisation (n’importe quel répertoire Azure AD - multi-tenant)** , il est recommandé d’utiliser un compte de travail plutôt qu’un compte de messagerie personnel.
   > * **Comptes Microsoft® personnels uniquement** et **Client unique** Les applications ne sont pas prises en charge.
   > * Il est recommandé d’utiliser **Compte Microsoft® multi-client et personnel** application.


1. Ensuite, accédez à **Certificats et secrets**, cliquez sur **Nouveau secret client** et suivez les étapes à l’écran pour créer un secret. Veillez à prendre note de cette valeur de secret pour une utilisation ultérieure.

   ![Clé secrète](/help/forms/using/assets/azure_secretkey.png)

1. Pour ajouter des autorisations, accédez à l’application nouvellement créée, puis sélectionnez **Autorisations d’API** > **Ajouter une autorisation** > **Graphique Microsoft®** > **Autorisations déléguées**
1. Cochez les cases correspondant aux autorisations ci-dessous pour l’application, puis cliquez sur **Ajouter une autorisation**:

   * `IMAP.AccessUser.All`
   * `Mail.Read`
   * `offline_access`
   * `POP.AccessAsUser.All`
   * `SMTP.Send`
   * `User.Read`

   ![Autorisation d’API](/help/forms/using/assets/azure_apipermission.png)

1. Sélectionner **Authentification** > **Ajouter une plateforme** > **Web**, et dans le **Url De Redirection** , ajoutez l’un des URI ci-dessous (Universal Resource Identifier) comme suit :
   * `https://login.microsoftonline.com/common/oauth2/nativeclient`
   * `http://localhost`

   Dans ce cas, `https://login.microsoftonline.com/common/oauth2/nativeclient` est utilisé comme URI de redirection.

1. Cliquez sur **Configurer** après avoir ajouté chaque URL et configuré vos paramètres en fonction de vos besoins.
   ![URI de redirection](/help/forms/using/assets/azure_redirecturi.png)

   >[!NOTE]
   >
   > Il est obligatoire de sélectionner **Jetons d’accès** et **Jetons d’ID** des cases à cocher.

1. Cliquez sur **Présentation** dans le volet de gauche et copiez les valeurs pour **ID d’application (client)**, **ID de répertoire (client)**, et **Secret du client** pour une utilisation ultérieure.

   ![Présentation](/help/forms/using/assets/azure_overview.png)

## Génération du code d’autorisation {#generating-the-authorization-code}

Ensuite, vous devez générer le code d’autorisation, comme expliqué dans les étapes suivantes :

1. Ouvrez l’URL suivante dans le navigateur après avoir remplacé `clientID` avec le `<client_id>` et `redirect_uri` avec l’URI de redirection de votre application :

   ```https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=[clientid]&scope=IMAP.AccessAsUser.All%20POP.AccessAsUser.All%20SMTP.Send%20User.Read%20Mail.Read%20offline_access&response_type=code&redirect_uri=[redirect_uri]&prompt=login```

1. Lorsque vous tapez l&#39;URL ci-dessus, vous êtes redirigé vers l&#39;écran de connexion :
   ![Écran de connexion](/help/forms/using/assets/azure_loginscreen.png)

1. Saisissez l’email, puis cliquez sur **Suivant** et l’écran des autorisations d’application s’affiche :

   ![Autorisation autorisée](/help/forms/using/assets/azure_permission.png)

1. Une fois l’autorisation autorisée, vous êtes redirigé vers une nouvelle URL en tant que : `https://login.microsoftonline.com/common/oauth2/nativeclient?code=<code>&session_state=[session_id]`

1. Copiez la valeur de `<code>` de l’URL ci-dessus à partir de `0.ASY...` to `&session_state` dans l’URL ci-dessus.

## Génération du jeton d’actualisation {#generating-the-refresh-token}

Ensuite, vous devez générer le jeton d’actualisation, comme expliqué dans les étapes suivantes :
1. Ouvrez l’invite de commande et utilisez la commande cURL suivante pour obtenir le jeton d’actualisation.
1. Remplacez la variable `clientID`, `client_secret` et `redirect_uri` avec les valeurs de votre application, ainsi que la valeur de `<code>`:

   `curl -H “ContentType application/x-www-form-urlencoded” -d “client_id=[client-id]&scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FPOP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FSMTP.Send%20https%3A%2F%2Foutlook.office.com%2FUser.Read%20https%3A%2F%2Foutlook.office.com%2FMail.Read%20offline_access&code=[code]&grant_type=authorization_code&redirect_uri=[redirect_uri]&client_secret=[secretkey_value]” -X POST https://login.microsoftonline.com/common/oauth2/v2.0/token`

1. Notez le jeton d’actualisation.

## Configuration du service de messagerie électronique avec prise en charge d’OAuth 2.0 {#configureemailservice}

Vous devez maintenant configurer le service de messagerie au plus tard sur le serveur JEE en vous connectant à l’interface utilisateur d’administration :

1. Accédez à **Accueil** > **Service** > **Application et services** > **Gestion des services** > **Service de messagerie électronique**, la variable **Service de messagerie de configuration** s’affiche, configurée pour l’authentification de base.

   >[!NOTE]
   >
   > Pour activer le service d’authentification oAuth 2.0, il est obligatoire de sélectionner **Si le serveur SMTP requiert une authentification (authentification SMTP)** .

1. Définir **Paramètres d’authentification oAuth 2.0** as `True`.
1. Copiez les valeurs de **ID client** et **Secret du client** à partir d’Azure Portal.
1. Copiez la valeur de la variable générée **Actualiser le jeton**.
1. Connectez-vous à **Workbench** et recherche **Email 1.0** de **Sélecteur d’activités**.
1. Trois options sont disponibles sous Email 1.0 :
   * **Envoyer avec document**: Envoie le courrier électronique avec des pièces jointes uniques.
   * **Envoi avec carte des pièces jointes**: Envoie le courrier électronique avec plusieurs pièces jointes.
   * **Recevoir**: Reçoit un courrier électronique de la part de l’IMAP.

   >[!NOTE]
   >
   >* Le protocole Transport Security possède des valeurs valides : &#39;blank&#39;, &#39;SSL&#39; ou &#39;TLS&#39;. Vous devez définir les valeurs de **SMTP Transport Security** et **Recevoir Transport Security** to **TLS** pour activer le service d’authentification oAuth.
   >* **Protocole POP3** n’est pas pris en charge pour OAuth.


   ![Paramètres de connexion](/help/forms/using/assets/oauth_connectionsettings.png)

1. Testez l’application en sélectionnant **Envoyer avec document**.
1. Fournir **À** et **De** les adresses.
1. Appeler l’application et envoyer le courrier électronique à l’aide de l’authentification 0Auth 2.0.

   >[!NOTE]
   >
   >Si vous souhaitez modifier le paramètre d’authentification Auth 2.0 en authentification de base pour un processus particulier dans un Workbench, vous pouvez définir la variable **Authentification OAuth 2.0** valeur &quot;False&quot; sous **Utiliser les paramètres globaux** dans le **Paramètres de connexion** .

## Pour activer les notifications de tâche oAuth {#enable_oauth_task}

1. Accédez à **Accueil** > **Services** > **Processus du formulaire** > **Paramètres du serveur** > **Paramètres de messagerie électronique**
1. Pour activer les notifications de tâche oAuth, sélectionnez l’option **Activer oAuth** .
1. Copiez les valeurs de **ID client** et **Secret du client** à partir d’Azure Portal.
1. Copiez la valeur de la variable générée **Actualiser le jeton**.
1. Cliquez sur **Enregistrer** pour enregistrer les détails.

   ![Notification de tâche](/help/forms/using/assets/task_notification.png)

   >[!NOTE]
   >
   > Pour en savoir plus sur les notifications de tâche, [cliquez ici](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/manage-endpoints/configuring-email-endpoints.html#create-an-email-endpoint-for-the-complete-task-service).

## Pour configurer le point de fin de courrier électronique {#configure_email_endpoint}

1. Accédez à **Accueil** > **Services** > **Application et services** > **Gestion des points de fin**
1. Pour configurer le point de fin de courrier électronique, définissez **Paramètres d’authentification oAuth 2.0** as `True`.
1. Copiez les valeurs de **ID client** et **Secret du client** à partir d’Azure Portal.
1. Copiez la valeur de la variable générée **Actualiser le jeton**.
1. Cliquez sur **Enregistrer** pour enregistrer les détails.

   ![Paramètres de connexion](/help/forms/using/assets/oauth_emailendpoint.png)

   >[!NOTE]
   >
   > Pour plus d’informations sur la configuration des points de fin de courrier électronique, cliquez sur [Configuration d’un point de fin de courrier électronique](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/manage-endpoints/configuring-email-endpoints.html).

## Résolution des problèmes {#troubleshooting}

* Si le service de messagerie ne fonctionne pas correctement. Essayez de régénérer la variable `Refresh Token` comme décrit ci-dessus. Le déploiement de la nouvelle valeur prend quelques minutes.

* Erreur lors de la configuration des détails du serveur de messagerie dans le point de fin de courrier électronique à l’aide de Workbench. Essayez de configurer le point de fin via l’interface utilisateur d’administration au lieu de Workbench.






