---
title: Prise en charge d’OAuth2 pour le service de messagerie
description: 'Prise en charge d’Oauth2 pour le service de messagerie  '
source-git-commit: 081b0c70ceca0502cb84d7e1b68b0b12dc45a4e7
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 47%

---

# Prise en charge d’OAuth2 pour le service de messagerie {#oauth2-support-for-the-mail-service}

AEM as a Cloud Service offre la prise en charge d’OAuth2 pour son service de messagerie intégré, afin de permettre aux entreprises de se conformer aux exigences en matière de messagerie sécurisée.

Vous pouvez configurer OAuth pour plusieurs fournisseurs de messagerie. Vous trouverez ci-dessous des instructions détaillées pour configurer le service de messagerie d’AEM afin de l’authentifier via OAuth2 avec Microsoft Office 365 Outlook. D’autres fournisseurs peuvent être configurés de la même manière.

## Microsoft Outlook {#microsoft-outlook}

1. Accédez à [https://portal.azure.com/](https://portal.azure.com/) et connectez-vous.
1. Recherchez le **répertoire Azure principal** dans la barre de recherche et cliquez sur le résultat. Vous pouvez également accéder directement à [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)
1. Cliquez sur **Enregistrement de l’application** - **Nouvel enregistrement**

   ![](/help/forms/using/assets/outh_outlook.PNG)

1. Renseignez les informations selon vos besoins, puis cliquez sur **Enregistrer**
1. Accédez à l’application nouvellement créée, puis sélectionnez **Autorisations API**
1. Accédez à **Ajouter une autorisation** - **Autorisation graphique** - **Autorisations déléguées**
1. Sélectionnez les autorisations ci-dessous pour votre application, puis cliquez sur **Ajouter une autorisation** :
   * `SMTP.Send`
   * `Mail.Read`
   * `Mail.Send`
   * `openid`
   * `offline_access`
1. Accédez à **Authentification** - **Ajouter une plateforme** - **Web**, et dans la section **URL de redirection**, ajoutez les URL ci-dessous, une avec et une sans barre oblique :
   * `http://localhost/`
   * `http://localhost`
1. Appuyez sur **Configurer** après avoir ajouté chaque URL et configuré vos paramètres en fonction de vos besoins.
1. Ensuite, accédez à **Certificats et secrets**, cliquez sur **Nouveau secret client** et suivez les étapes à l’écran pour créer un secret. Veillez à prendre note de ce secret pour une utilisation ultérieure.
1. Press **Présentation** dans le volet de gauche et copiez les valeurs pour **ID d’application (client)** pour une utilisation ultérieure.

Pour effectuer une récapitulation, vous avez besoin des informations suivantes pour configurer OAuth2 pour le service de messagerie du côté AEM :

* L’URL d’authentification dans le formulaire : `https://login.microsoftonline.com/<ID>/oauth2/v2.0/authorize`
* URL du jeton sous la forme : `https://login.microsoftonline.com/<ID>/oauth2/v2.0/token`
* L&#39;URL d&#39;actualisation dans le formulaire : `https://login.microsoftonline.com/<ID>/oauth2/v2.0/token`
* L’ID client
* Le secret client

### Génération du jeton d’actualisation {#generating-the-refresh-token}

Vous devez ensuite générer le jeton d’actualisation, comme illustré à l’étape suivante.

Pour ce faire, procédez comme suit :

1. Ouvrez l’URL suivante dans le navigateur après avoir remplacé `clientID` avec les valeurs propres à votre compte :

   ```https://login.microsoftonline.com/common/oauth2/v2/authorize?client_id=<client_id>&scope=IMAP.AccessAsUser.A;;%20POP.AccessAsUser.All%20SMTP.Send%20User.Read&response_type=code&redirect-uri=http://loginmicrosoftonline.com/common/outh2/nativeclient&prompt=login```

1. Autorisation, le cas échéant.
1. L’URL redirige vers un nouvel emplacement, construit au format suivant : `http://localhost/?code=<code>&state=12345&session_state=4f984c6b-cc1f-47b9-81b2-66522ea83f81#`
1. Copiez la valeur de `<code>` dans l’exemple ci-dessus.
1. Utilisez la commande cURL suivante pour obtenir le refreshToken. Remplacez clientID, clientSecret par les valeurs de votre compte et la valeur de `<code>`:

   ```
   curl -H “ContentType application/x-www-form-urlencoded” -d 
   "client_id=<client-id>
   &scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All&code=M.R3_BAY.1bf609bf-25b3-2fcd-d910-02e02c53bc
   &grant_type=authorization_code
   &redirect_uri= https://login.microsoftonline.com/common/oauth2/nativeclient
   &client_secret=~1E8Q~cz-m6vgOb9m~SI.eF9jSVTbFUiP5f0” -X POST https://login.microsoftonline.com/common/oauth2/v2.0/token
   ```

1. Prenez note des éléments refreshToken et accessToken.

### Validation des jetons {#validating-the-tokens}

Avant de poursuivre la configuration d’OAuth côté AEM, veillez à valider les éléments accessToken et refreshToken avec la procédure suivante :

1. Générez l’accessToken à l’aide du refreshToken produit lors de la procédure précédente. Pour ce faire, utilisez l’option curl suivante et remplacez les valeurs de `<client_id>`,`<client_secret>` ainsi que la variable `<refreshToken>`:

   ```
   curl -H “ContentType application/x-www-form-urlencoded” -d 
   "client_id=<client_id>
   &scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All&code=<code>
   &grant_type=authorization_code
   &redirect_uri= https://login.microsoftonline.com/common/oauth2/nativeclient
   &client_secret=<client_secret>
   &refresh_token=<refresh_token” 
   -X POST https://login.microsoftonline.com/common/oauth2/v2.0/token
   ```

1. Envoyez un courrier électronique à l’aide de accessToken pour vérifier s’il fonctionne correctement.

>[!NOTE]
>
> Vous pouvez obtenir la collection d’API Postman à partir de [cet emplacement](https://docs.microsoft.com/fr-fr/azure/active-directory/develop/v2-oauth2-auth-code-flow).

### Configuration du service de messagerie électronique avec prise en charge d’Auth2.0 {#configureemailservice}

Vous devez maintenant configurer le service de messagerie au plus tard sur le serveur JEE en vous connectant à l’interface utilisateur d’administration :

1. Accédez à **Accueil** - **Service** - **Application et services** - **Gestion des services** - **Service de messagerie électronique**
1. **Service de messagerie de configuration** s’affiche, configurez **SMPT** et **IMP** pour une authentification de base.
1. Pour activer le service d’authentification des courriers Outlook, sélectionnez **Paramètres d’authentification oAuth 2.0** .
1. Copiez les valeurs de **ID client** et **Secret du client** à partir d’Azure Portal.
1. Copiez la valeur de la variable générée **Actualiser le jeton**.
1. Cliquez sur **Enregistrer** pour enregistrer les détails.
1. Connexion à Workbench et recherche **Email 1.0** de **Sélecteur d’activités**.
1. Trois options sont disponibles sous Email 1.0 :
   * **Envoyer avec document**: Envoie le courrier électronique avec des pièces jointes uniques.
   * **Envoi avec carte des pièces jointes**: Envoie le courrier électronique avec plusieurs pièces jointes.
   * **Recevoir**: Reçoit un courrier électronique POP3 ou IMAP.
1. Testez l’application en sélectionnant **Envoyer avec document**
1. Fournir **À** et **De** les adresses.
1. Appeler l’application et envoyer le courrier électronique à l’aide de l’authentification oAuth2.0.

>[!NOTE]
>
> Si vous souhaitez modifier le paramètre d’authentification Auth 2.0 en authentification de base pour un processus particulier dans un Workbench, vous pouvez décocher la case **Authentification oAuth2.0** case à cocher sous **Utiliser les paramètres globaux** dans le **Paramètres de connexion** .

### Résolution des problèmes {#troubleshooting}

Si le service de messagerie ne fonctionne pas correctement, régénérez la variable `refreshToken` comme décrit ci-dessus. Le déploiement de la nouvelle valeur prend quelques minutes.


