---
title: Notifications Push
description: Consultez cette page pour en savoir plus sur l’utilisation des notifications push dans une application Adobe Experience Manager Mobile.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: 375f2f40-1b98-4e21-adee-cbea274e6a2a
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '3135'
ht-degree: 1%

---

# Notifications Push{#push-notifications}

{{ue-over-mobile}}

Être en mesure d’alerter instantanément les utilisateurs et utilisatrices de votre application mobile Adobe Experience Manager (AEM) avec des notifications importantes est essentiel à la valeur d’une application mobile et de ses campagnes marketing. Nous décrivons ici les étapes à suivre pour permettre à votre application de recevoir des notifications push. Vous apprendrez également à configurer et à envoyer des notifications push depuis AEM Mobile vers l’application installée sur le téléphone. En outre, cette section décrit comment configurer la fonction [Lien profond](#deeplinking) pour vos notifications push.

>[!NOTE]
>
>*La diffusion des notifications push n’est pas garantie ; elles ressemblent davantage à des annonces. Nous faisons de notre mieux pour nous assurer que tout le monde les reçoit, mais ce n&#39;est pas un mécanisme de prestation garanti. En outre, le temps de diffusion d’une notification push peut varier de moins d’une seconde à jusqu’à une demi-heure.*

L’utilisation des notifications push avec AEM nécessite quelques technologies différentes. Tout d’abord, un fournisseur de services de notification push doit être utilisé pour gérer les notifications et les appareils (AEM ne le fait pas encore). Deux fournisseurs prêts à l’emploi sont configurés avec AEM : [Amazon Simple Notification Service](https://aws.amazon.com/sns/) (ou SNS) et [Pushwoosh](https://www.pushwoosh.com/). Ensuite, la technologie push pour le système d’exploitation mobile donné doit passer par le service approprié : Apple Push Notification Service (ou APNS) pour les appareils iOS et Google Cloud Messaging (ou GCM) pour les appareils Android™. Bien qu’AEM ne communique pas directement avec ces services spécifiques à la plateforme, certaines informations de configuration associées doivent être fournies par AEM avec les notifications pour que ces services exécutent la notification push.

Une fois installé et configuré (comme expliqué ci-dessous), il fonctionne comme suit :

1. Une notification push est créée dans AEM et envoyée au fournisseur de services (Amazon SNS ou Pushwoosh).
1. Le prestataire le reçoit et l&#39;envoie au prestataire central (APNS ou GCM).
1. Le fournisseur principal envoie la notification à tous les appareils enregistrés pour cette notification push. Pour chaque appareil, il utilise le réseau de données cellulaires ou WiFi, selon ce qui est disponible sur l&#39;appareil.
1. La notification s’affiche sur l’appareil si l’application pour laquelle il est enregistré n’est pas en cours d’exécution. Un utilisateur qui appuie sur la notification démarre l’application et affiche la notification dans l’application. Si l’application est déjà en cours d’exécution, seule la notification in-app s’affiche.

Cette version d’AEM prend en charge les appareils mobiles iOS et Android™.

## Présentation et procédure {#overview-and-procedure}

Pour utiliser les notifications push dans une application AEM Mobile, les étapes générales suivantes doivent être suivies.

En règle générale, un développeur Experience Manager effectue les opérations suivantes :

1. Enregistrement auprès des services de messagerie Apple et Google
1. S’inscrire à un service de messagerie push et le configurer
1. Ajout de la prise en charge des notifications push à l’application
1. Préparer un téléphone pour le test

Lorsqu’un administrateur Experience Manager effectue les opérations suivantes :

1. Configuration des notifications push sur les applications AEM
1. Créer et déployer l’application
1. Envoyer une notification push
1. Configuration des *de lien profond (facultatif)*

### Étape 1 : s’inscrire auprès des services de messagerie Apple et Google {#step-register-with-apple-and-google-messaging-services}

#### Utilisation du service de notification push Apple (APNS) {#using-the-apple-push-notification-service-apns}

Accédez à la page Apple [ici](https://developer.apple.com/documentation/usernotifications#//apple_ref/doc/uid/TP40008194-CH8-SW1) pour vous familiariser avec le service de notification push Apple.

Pour utiliser les APNs, vous avez besoin d’un fichier **Certificate** (un fichier .cer), d’une notification push **Private Key** (un fichier .p12) et d’un **Private Key Password** d’Apple. Les instructions pour ce faire sont disponibles [ici](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/).

#### Utilisation du service Google Cloud Messaging (GCM) {#using-the-google-cloud-messaging-gcm-service}

>[!NOTE]
>
>Google remplace GCM par un service similaire appelé Firebase Cloud Messaging (FCM). Pour plus d&#39;informations sur FCM, cliquez [ici](https://firebase.google.com/docs/cloud-messaging/).

Accédez à la page Google [ici](https://developer.android.com/google/gcm/index.html) pour vous familiariser avec Google Cloud Messaging pour Android™.

[Suivez ces étapes](https://developer.android.com/google/gcm/gs.html) pour **Créer un projet d’API Google**, **Activer le service GCM** et **Obtenir une clé API**. Vous avez besoin de la **clé API** pour envoyer des notifications push aux appareils Android™. Enregistrez également votre **Numéro de projet**, également parfois appelé **ID d’expéditeur GCM**.

Les étapes suivantes présentent une autre méthode de création des clés API GCM :

1. Connectez-vous à Google et accédez à la page du développeur de Google [&#128279;](https://developers.google.com/mobile/add?platform=android&amp;cntapi=gcm).
1. Choisissez votre application dans la liste (ou créez-en une).
1. Sous Nom du package Android™, saisissez votre ID d’application, c’est-à-dire `com.adobe.cq.mobile.weretail.outdoorsapp`. (Si cela ne fonctionne pas, réessayez avec « test.test ».)
1. Cliquez sur **Continuer pour choisir et configurer les services**
1. Sélectionnez Cloud Messaging, puis cliquez sur **Activer Google Cloud Messaging**.
1. La nouvelle clé API du serveur et l’ID d’expéditeur (nouveau ou existant) s’affichent alors.

>[!NOTE]
>
>Enregistrez la clé API du serveur . Cette valeur est saisie sur le site de votre fournisseur de notifications push.

### Étape 2 : enregistrement et configuration d&#39;un service de messagerie push {#step-register-and-configure-a-push-messaging-service}

AEM est configuré pour utiliser l’un des trois services pour les notifications push :

* SNS Amazon
* Pushwoosh
* Adobe Mobile Services

Les configurations *Amazon SNS* et *Pushwoosh* permettent d’envoyer des notifications push depuis les écrans AEM.

La configuration *Adobe Mobile Services* vous permet de configurer et d’envoyer des notifications push depuis Adobe Mobile Services à l’aide d’un compte Adobe Analytics (mais l’application doit être créée avec cette configuration définie pour activer les notifications push AMS).

#### Utilisation du service de messagerie Amazon SNS {#using-the-amazon-sns-messaging-service}

>[!NOTE]
>
>*Vous trouverez des informations sur Amazon SNS et un lien pour créer un compte AWS [ici](https://aws.amazon.com/sns/). Vous pouvez obtenir un compte gratuit pendant un an.*

Si vous ne souhaitez pas utiliser Amazon SNS, vous pouvez ignorer ces étapes.

Pour configurer Amazon SNS pour les notifications push, procédez comme suit :

1. **S’inscrire avec Amazon SNS**

   1. Enregistrez votre ID de compte. Le format doit être de 12 chiffres sans espaces ni tirets, c’est-à-dire « 123456789012 ».
   1. Assurez-vous que vous vous trouvez dans la région « us-east » ou « eu », car une étape ultérieure (création d’un pool d’identités) en requiert un.
   1. Après l&#39;enregistrement, connectez-vous à la console de gestion et sélectionnez [SNS](https://console.aws.amazon.com/sns/) (Push Notification Service). Cliquez sur « Commencer » s’il apparaît.

1. **Créer une clé d’accès et un ID**

   1. Cliquez sur votre nom d’utilisateur dans l’angle supérieur droit de l’écran, puis sélectionnez Informations d’identification de sécurité dans le menu.
   1. Cliquez sur Clés d&#39;accès, puis dans l&#39;espace ci-dessous, cliquez sur **Créer une clé d&#39;accès**.
   1. Cliquez sur **Afficher la clé d’accès**, puis copiez et enregistrez l’ID de clé d’accès et la clé d’accès secrète affichés. Si vous choisissez l’option de téléchargement des clés, vous obtenez un fichier CSV contenant ces mêmes valeurs.
   1. D’autres certificats liés à la sécurité, ainsi que d’autres, peuvent être gérés sur cette page.

   >[!NOTE]
   >
   >Une clé d’accès peut être utilisée pour plusieurs applications.

   Pour les organisations qui utilisent un compte « AWS Sandbox », les étapes sont similaires et décrites ici :

   1. Cliquez sur votre nom d’utilisateur dans l’angle supérieur droit de l’écran, puis sélectionnez Mes informations d’identification de sécurité dans le menu.
   1. Cliquez sur Utilisateurs dans la liste d’actions de gauche, puis choisissez votre nom d’utilisateur.
   1. Cliquez sur l’onglet Informations d’identification de sécurité .
   1. À partir de là, vous pouvez voir vos clés et en créer de nouvelles. Enregistrez les clés pour une utilisation ultérieure.

1. **Créer une rubrique**

   1. Cliquez sur **Créer une rubrique** et choisissez un nom de rubrique. Enregistrez tous les champs tels que ARN de rubrique, Propriétaire de rubrique, Région, Nom d’affichage.
   1. Cliquez sur **Autres actions de rubrique** > **Modifier la politique de rubrique**. Sous **Autoriser ces utilisateurs à s’abonner à cette rubrique**, sélectionnez **Tout le monde.**
   1. Cliquez sur **Mettre à jour la politique**.

   >[!NOTE]
   >
   >Vous pouvez créer plusieurs rubriques pour différents scénarios, tels que le développement, le test et la démonstration. Le reste de la configuration SNS peut rester identique. Créez l’application avec la autre rubrique. Les notifications push envoyées à cette rubrique ne seront reçues que par l’application créée avec cette rubrique.

1. **Créer des applications Platform**

   1. Cliquez sur Applications, puis sur Créer une application Platform. Choisissez un nom et sélectionnez une plateforme (APNS pour iOS, GCM pour Android™). En fonction de la plateforme. les autres champs doivent être renseignés :

      1. Pour APNS, un fichier P12, un mot de passe, un certificat et une clé privée doivent tous être saisis. Ils doivent avoir été obtenus à l’étape *Utilisation du service de notification push Apple (APNS)* ci-dessus.
      1. Pour GCM, une clé API doit être saisie. Cela doit avoir été obtenu à l’étape *Utilisation du service Google Cloud Messaging (GCM)* ci-dessus.

   1. Répétez l’étape ci-dessus une fois pour chaque plateforme prise en charge. Pour pouvoir effectuer des transferts vers iOS et Android™, deux applications Platform doivent être créées.

1. **Créer un pool d’identités**

   1. Utilisez [Cognito](https://console.aws.amazon.com/cognito) pour créer un pool d’identités qui stockera les données de base des utilisateurs non authentifiés. Notez que seules les régions « us-east » et « eu » sont actuellement prises en charge par Amazon Cognito.
   1. Attribuez-lui un nom et cochez la case « Activer l’accès aux identités non authentifiées ».
   1. Sur la page suivante (« *Vos identités Cognito nécessitent l’accès à vos ressources* »), cliquez sur Autoriser.
   1. En haut à droite de la page, cliquez sur le lien « *Modifier le pool d’identités »*. L’ID du pool d’identités s’affiche. Enregistrez ce texte pour plus tard.
   1. Sur la même page, sélectionnez la liste déroulante en regard de « Rôle non authentifié » et assurez-vous que le rôle Cognito_&lt;nom du pool>UnauthRole est sélectionné. Enregistrez vos modifications.

1. **Configurer l’accès**

   1. Connectez-vous à [Gestion des identités et des accès](https://console.aws.amazon.com/iam/home) (IAM).
   1. Sélectionnez Rôles.
   1. Cliquez sur le rôle créé à l’étape précédente, appelé Cognito_&lt;yourIdentityPoolName>Unauth_Role. Enregistrez le « ARN du rôle » affiché.
   1. Ouvrez « Politiques intégrées » si ce n’est pas déjà fait. Une politique portant le nom oneClick_Cognito_&lt;yourIdentityPoolName>Unauth_Role_1234567890123 doit s’afficher à cet endroit.
   1. Cliquez sur « Modifier la politique ». Remplacez le contenu du document de politique par ce fragment de code JSON :

   <table>
    <tbody>
     <tr>
     <td><p> </p> <p>{</p> <p> « Version » : « 2012-10-17 »,</p> <p> « Instruction » : [</p> <p> {</p> <p> « Action » : [</p> <p> « mobileanalytics:PutEvents »,</p> <p> « cognito-sync:* »,</p> <p> « SNS:CreatePlatformEndpoint »,</p> <p> « SNS:Subscribe »</p> <p> ],</p> <p> « Effect » : « Allow »,</p> <p> « Ressource » : [</p> <p> « * »</p> <p> ]</p> <p> }</p> <p> ]</p> <p>}</p> <p> </p> </td>
     </tr>
    </tbody>
    </table>

   1. Cliquez sur **Appliquer la politique**.

#### Utilisation du service de messagerie push {#using-the-pushwoosh-messaging-service}

Si vous ne souhaitez pas utiliser Pushwoosh, vous pouvez ignorer cette étape.

Pour utiliser Pushwoosh :

1. **S&#39;inscrire avec Pushwoosh**

   1. Accédez à pushwoosh.com et créez un compte.

1. **Créer un jeton d’accès API**

   1. Sur le site Pushwoosh, accédez à l’élément de menu Accès à l’API pour générer un jeton d’accès à l’API. Enregistrez ce jeton en toute sécurité.

1. **Créer une application**

   1. Pour la prise en charge d’Android™, vous devez fournir votre clé API GCM.
   1. Lors de la configuration de l’application, choisissez Cordova comme framework.
   1. Pour la prise en charge d’iOS, vous devez fournir le fichier de certificat (.cer), le certificat push (.p12) et le mot de passe de la clé privée ; ceux-ci doivent avoir été obtenus auprès du site APNS d’Apple. Pour Framework, choisissez Cordova.
   1. Pushwoosh génère un ID d’application pour cette application, sous la forme « XXXXX-XXXXX », où chaque X est une valeur hexadécimale (0 à F).

>[!NOTE]
>
>*Si une deuxième application est configurée dans AEM avec le même ID d’application (et d’autres valeurs associées : Jeton d’accès de l’API et ID GCM), toutes les notifications push envoyées via la deuxième application sur AEM seront envoyées à toute autre application avec cet ID d’application.*

### Étape 3 : ajouter la prise en charge des notifications push à l’application {#step-add-push-support-to-the-app}

#### Ajouter une configuration de synchronisation de contenu {#add-contentsync-configuration}

Créez deux nœuds de contenu (l’un dans app-config et l’autre dans app-config-dev) appelés notificationsConfig :

* /content/`<your app>`/shell/jcr:content/pge-app/app-config-dev/notificationsConfig
* /content/`<your app>`/shell/jcr:content/pge-app/app-config/notificationsConfig

Avec ces propriétés (fichiers .content.xml) :
&lt;jcr:root xmlns:jcr= » [https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/1.0/index.html](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/1.0/index.html) » xmlns:nt= » [https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/1.0/index.html](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/1.0/index.html) »
jcr:primaryType=« nt:unstructured »
excludeProperties= »[appAPIAccessToken] »
path= »../../../.. »
targetRootDirectory=« www »
type=« notificationsconfig »/>

>[!NOTE]
>
>Le gestionnaire de synchronisation de contenu recherche ces nœuds, et s’ils n’existent pas, il n’écrit pas le fichier pge-notifications-config.json.

#### Ajout de bibliothèques clientes {#add-client-libraries}

Les bibliothèques clientes des notifications push doivent être ajoutées à l’application en procédant comme suit :

En CRXDE Lite :

1. Accédez à */etc/designs/phonegap/&lt;app name>/clientlibsall.*
1. Double-cliquez sur la section incorporer dans le volet des propriétés.
1. Dans la boîte de dialogue qui s’affiche, ajoutez une bibliothèque cliente en cliquant sur le bouton + .
1. Dans le nouveau champ de texte, ajoutez « cq.mobile.push », puis cliquez sur OK.
1. Ajoutez-en un autre appelé cq.mobile.push.amazon, puis cliquez sur OK.
1. Enregistrez les modifications.

>[!NOTE]
>
>Si les notifications push sont supprimées ou ne sont pas utilisées, pour des raisons d’espace sur l’application et afin d’éviter les messages d’erreur de la console, supprimez ces bibliothèques clientes de votre application.

### Étape 4 : Préparer un téléphone pour les tests {#step-prepare-a-phone-for-testing}

>[!NOTE]
>
>*Pour les notifications push, vous devez effectuer un test sur un appareil réel, car les émulateurs ne sont pas en mesure de recevoir des notifications push.*

#### IOS {#ios}

Pour iOS, utilisez un ordinateur macOS et rejoignez le [Programme de développement iOS](https://developer.apple.com/programs/ios/). Certaines sociétés ont des licences d&#39;entreprise qui peuvent être mises à la disposition de tous les développeurs.

Avec XCode 8.1, avant d’utiliser les notifications push, vous devez accéder à l’onglet Fonctionnalités de votre projet et activer/désactiver le bouton des notifications push.

#### Android™ {#android}

Pour installer l’application sur un téléphone Android™ à l’aide de l’interface de ligne de commande (voir ci-dessous : **Étape 6 - Créer et déployer l’application**), vous devez d’abord placer le téléphone en « mode développeur ». Voir [Activation des options du développeur sur l’appareil](https://developer.android.com/tools/device.html#developer-device-options) pour plus d’informations.

### Étape 5 : configuration des notifications push sur les applications AEM {#step-configure-push-on-aem-apps}

Avant de créer et de déployer sur l’appareil mobile configuré, vous devez configurer les paramètres de notification du service de messagerie que vous avez décidé d’utiliser.

1. Créez les groupes d’autorisations appropriés pour les notifications push.
1. Connectez-vous à AEM en tant qu’utilisateur approprié, puis cliquez sur l’onglet Applications .
1. Cliquez sur l’application .
1. Recherchez la mosaïque Gestion des Cloud Service et cliquez sur le crayon pour modifier vos configurations cloud.
1. Sélectionnez Amazon SNS Connection, Pushwoosh Connection ou Adobe Mobile Services comme configuration de notification.
1. Saisissez les propriétés du fournisseur et cliquez sur Envoyer pour les enregistrer, puis sur Terminé. Ils ne sont pas vérifiés à distance à ce stade, sauf s’il existe AMS.
1. Vous devriez maintenant voir la configuration que vous venez de saisir sur la mosaïque Gestion des Cloud Service .

### Étape 6 : créer et déployer l’application {#step-build-and-deploy-the-app}

**Remarque :** consultez les instructions [ici](/help/mobile/building-app-mobile-phonegap.md) sur la création d’applications PhoneGap.

Il existe deux façons de créer et de déployer votre application à l’aide de PhoneGap.

**Remarque :** pour les tests de notification push, les émulateurs ne suffiront pas, car les notifications push utilisent un protocole distinct entre le fournisseur push (Apple ou Google) et l&#39;appareil. Le matériel et les émulateurs Mac/PC actuels ne prennent pas en charge cette fonctionnalité.

1. *PhoneGap Build* est un service offert par PhoneGap qui créera votre application pour vous sur leurs serveurs, et vous permettra de la télécharger directement sur votre appareil. Consultez la documentation de PhoneGap Build à l’adresse `https://build.phonegap.com/` pour savoir comment configurer et utiliser PhoneGap Build.

1. L’interface de ligne de commande *PhoneGap Command Line Interface* (CLI) vous permet d’utiliser un jeu riche de commandes PhoneGap sur votre ligne de commande pour créer, déboguer et déployer votre application. Reportez-vous à la documentation PhoneGap destinée aux développeurs (`https://docs.phonegap.com/en/edge/guide_cli_index.md.html#The%20Command-Line%20Interface`) pour savoir comment configurer et utiliser l’interface de ligne de commande PhoneGap.

### Étape 7 : envoyer une notification push {#step-send-a-push-notification}

Pour créer une notification et l’envoyer, procédez comme suit.

1. Création d’une notification

   * Dans le tableau de bord de l’application AEM Mobile, recherchez la mosaïque Notifications push .
   * Dans le menu en haut à droite, choisissez « Créer ». Ce bouton n’est pas disponible tant que la configuration cloud n’est pas définie.
   * Dans l’assistant Créer une notification, saisissez un titre et un message, puis cliquez sur le bouton « Créer ». Votre notification est maintenant prête à être envoyée immédiatement ou ultérieurement. Il peut être modifié et le message et/ou le titre peuvent être modifiés et enregistrés.

1. Envoyer la notification

   * Dans le tableau de bord des applications, recherchez la mosaïque Notifications push .
   * Sélectionnez la notification ou cliquez sur le bouton Détails en bas à droite (. . .), pour afficher la liste des notifications. Cette liste indique également si une notification est prête à être envoyée, si elle a déjà été envoyée ou si une erreur s’est produite lors de l’envoi.
   * Cochez la case d’une notification (uniquement) et cliquez sur le bouton « Envoyer la notification » au-dessus de la liste. Vous avez une chance d’« annuler » ou d’« envoyer » la notification dans la boîte de dialogue qui s’affiche.

1. Traitement des résultats

   * Si le service de notification push (Amazon SNS ou Pushwoosh) reçoit la demande d&#39;envoi, la confirme comme valide et l&#39;envoie correctement aux fournisseurs natifs (APNS et GCM), la boîte de dialogue Envoyer se ferme sans message. Dans la liste des notifications, le statut de cette notification est indiqué comme Envoyé.
   * Si l’envoi push échoue, la boîte de dialogue affiche un message indiquant le problème. Dans la liste des notifications, le statut de cette notification est marqué comme Erreur, mais si le problème est corrigé, la notification peut être envoyée à nouveau. En cas d’erreur, des informations supplémentaires sur l’erreur doivent apparaître dans le journal des erreurs du serveur.
   * Notez qu’il existe des différences de plateforme entre les notifications push iOS et Android™. Parmi eux :

      * La création avec l’interface de ligne de commande démarre l’application après son déploiement sur Android™. Sur iOS, vous devez le démarrer manuellement. Comme l’étape d’enregistrement push se produit au démarrage, les applications Android™ peuvent recevoir immédiatement des notifications push (car elles ont déjà démarré et sont enregistrées), contrairement aux applications iOS.
      * Dans Android™, le texte du bouton OK est en majuscules (et dans tout autre bouton ajouté à la notification in-app), ce qui n’est pas le cas dans iOS.

Pour les notifications push AMS, les notifications doivent être composées et envoyées à partir du serveur AMS. AMS fournit des fonctionnalités de notification push supplémentaires en plus de celles fournies par les notifications AEM avec AWS et Pushwoosh.

>[!NOTE]
>
>*La diffusion des notifications push n’est pas garantie ; elles ressemblent davantage à des annonces. Nous faisons de notre mieux pour nous assurer que tout le monde l&#39;entend, mais il ne s&#39;agit pas d&#39;un mécanisme de prestation garanti. En outre, le temps de diffusion d’une notification push peut varier de moins d’une seconde à jusqu’à une demi-heure.*

### Configuration des liens profonds avec les notifications push {#configuring-deep-linking-with-push-notifications}

Qu’est-ce qu’un lien profond ? Dans le contexte d’une notification push, il s’agit d’un moyen d’autoriser l’ouverture ou le redirection d’une application (si elle est ouverte) vers un emplacement spécifié dans l’application.

Comment cela fonctionne-t-il ? L’auteur d’une notification push peut éventuellement ajouter un libellé de bouton (c’est-à-dire « Afficher ! ») vers la notification et sélectionne la page qu’ils souhaitent lier dans la notification, via un navigateur visuel de chemin d’accès. Lorsqu’elle est envoyée, la notification push se produit normalement, sauf que dans le message in-app, le bouton OK est remplacé par un bouton « Ignorer » et le nouveau bouton spécifié (« Afficher ! ») apparaît également. Cliquer sur le nouveau bouton permet à l’application d’accéder à la page spécifiée dans l’application. Cliquez sur Ignorer pour expulser le message.

Si l’application n’est pas ouverte, l’ombre apparaît normalement. Le fait d’agir sur la notification à l’ombre ouvre l’application, puis présente à l’utilisateur les boutons de lien profond en fonction de ce qui a été configuré dans la notification push.

Créez la notification, ajoutez un texte de bouton et le chemin du lien pour le lien profond facultatif :

>[!CAUTION]
>
>Pour accéder à la mosaïque Notification push dans votre tableau de bord, procédez comme suit.

1. Cliquez sur le bouton Modifier dans le coin supérieur droit de la mosaïque **Gérer les Cloud Service**.

   ![chlimage_1-108](assets/chlimage_1-108.png)

1. Sélectionnez l’option **Pushwoosh Connection**. Cliquez sur **Suivant**.

   ![chlimage_1-109](assets/chlimage_1-109.png)

1. Saisissez les détails des propriétés et cliquez sur **Envoyer**.

   ![chlimage_1-110](assets/chlimage_1-110.png)

   Une fois votre configuration envoyée, la mosaïque **Notifications push** s’affiche dans le tableau de bord.

   ![chlimage_1-111](assets/chlimage_1-111.png)

### Assistant de création de notification {#create-notification-wizard}

Une fois que la mosaïque **Notifications push** s’affiche dans votre tableau de bord, utilisez l’assistant de création de notification pour ajouter le contenu :

1. Cliquez sur le symbole d’ajout dans le coin supérieur droit de la mosaïque **Notifications push** pour ouvrir l’**Assistant Créer une notification**.

   ![chlimage_1-112](assets/chlimage_1-112.png)

1. Cliquez sur l’icône de navigation dans le chemin du lien pour présenter à l’utilisateur la structure de contenu de l’application.

   Une fois le chemin sélectionné, cliquez sur l’icône de vérification.

   ![chlimage_1-113](assets/chlimage_1-113.png)

   >[!NOTE]
   >
   >Le texte du bouton Lien est limité à 20 caractères.
   >
   >Si l’utilisateur final ne dispose pas de la dernière version de l’application et que le chemin lié n’est pas disponible, la confirmation de l’action du lien profond l’amène à la page principale de l’application.

1. Saisissez le **Détails du texte** dans l’**Assistant Créer une notification** et cliquez sur **Créer**.

   ![chlimage_1-114](assets/chlimage_1-114.png)

   Ouvrez les détails en cliquant sur la notification push que vous avez créée dans la mosaïque **Notifications push**.

   Vous pouvez modifier les propriétés, envoyer des notifications ou supprimer la notification.

   ![chlimage_1-115](assets/chlimage_1-115.png)

>[!NOTE]
>
>**Informations supplémentaires** :
>
>Pushwoosh et Amazon SNS ne seront pas pris en charge après la version 6.4 et seront disponibles en tant que module complémentaire à partir du partage de packages.

### Les étapes suivantes {#the-next-steps}

Une fois que vous avez compris les détails des notifications push pour votre application, consultez [AEM Mobile Content Personalization](/help/mobile/phonegap-aem-mobile-content-personalization.md).
