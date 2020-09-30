---
title: Connexion aux réseaux sociaux avec Facebook et Twitter
seo-title: Connexion aux réseaux sociaux avec Facebook et Twitter
description: La connexion à Social permet aux visiteurs du site de se connecter à l’aide de leur compte Facebook ou Twitter.
seo-description: La connexion à Social permet aux visiteurs du site de se connecter à l’aide de leur compte Facebook ou Twitter.
uuid: f70e346e-0d8c-41a0-a100-206a420088dc
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: c0a71870-8f95-40c8-9ffd-b7af49723288
translation-type: tm+mt
source-git-commit: 42606e76742fe7698c4c186208e515ed22adc5a4
workflow-type: tm+mt
source-wordcount: '2787'
ht-degree: 2%

---


# Connexion aux réseaux sociaux avec Facebook et Twitter {#social-login-with-facebook-and-twitter}

La connexion sociale permet de présenter à un visiteur de site l’option de connexion avec son compte Facebook ou Twitter. Par conséquent, inclure les données Facebook ou Twitter autorisées dans leur profil membre AEM.

![socialloginweretail](assets/socialloginweretail.png)

## Présentation de la connexion aux réseaux sociaux {#social-login-overview}

Pour inclure la connexion sociale, il est *nécessaire* de créer des applications Facebook et Twitter personnalisées.

Bien que l’exemple de vente au détail Web fournisse des exemples d’applications Facebook et Twitter et de services cloud, ils ne sont pas disponibles sur un site Web [de](../../help/sites-administering/production-ready.md)production.

Les étapes requises sont les suivantes :

1. [Activez l’authentification](#adobe-granite-oauth-authentication-handler) OAuth sur toutes les instances de publication AEM.

   Si OAuth n&#39;est pas activé, les tentatives de connexion échouent.

1. **Créez** une application sociale et un service cloud.

   * Pour prendre en charge la connexion à Facebook :

      * Créez une application [](#create-a-facebook-app)Facebook.
      * Créez et publiez un service [cloud](#create-a-facebook-connect-cloud-service)Facebook Connect.
   * Pour prendre en charge la connexion avec Twitter :

      * Créez une application [](#create-a-twitter-app)Twitter.
      * Créez et publiez un service [cloud](#create-a-twitter-connect-cloud-service)Twitter Connect.


1. [**Activez** la connexion](#enable-social-login) sociale pour un site communautaire.

Il existe deux concepts de base :

1. **L’étendue** (autorisations) spécifie les données que l’application est autorisée à demander.

   * Par défaut, les instances Application OAuth et Fournisseur [Granite de l’Adobe Facebook et Twitter](#adobe-granite-oauth-application-and-provider) incluent les autorisations de base de l’application dans leur étendue.

1. **Les champs** (params) spécifient les données réelles demandées à l’aide des paramètres d’URL.

   * Ces champs sont spécifiés dans [AEM Communities Facebook OAuth Provider](#aem-communities-facebook-oauth-provider) et [AEM Communities Twitter OAuth Provider](#aem-communities-twitter-oauth-provider).
   * Les champs par défaut sont suffisants pour la plupart des cas d’utilisation, mais peuvent être modifiés.

## Facebook Login {#facebook-login}

### Version de l’API Facebook {#facebook-api-version}

La connexion sociale et l’exemple Facebook de la vente au détail ont été développés lorsque l’API graphique Facebook était la version 1.0.A partir de AEM version 6.4 GA et AEM 6.3 SP1 la connexion sociale a été mise à jour pour fonctionner avec la nouvelle version de l’API graphique Facebook 2.5.

>[!NOTE]
>
>Pour les versions AEM plus anciennes, si vous rencontrez une exception dans les journaux **Impossible d’extraire un jeton de cette** version, effectuez la mise à niveau vers le CFP le plus récent pour cette AEM version.


Pour plus d’informations sur la version de l’API de graphique Facebook, voir le fichier de modification [de l’API](https://developers.facebook.com/docs/apps/changelog)Facebook.

### Création d’une application Facebook {#create-a-facebook-app}

Une application Facebook correctement configurée est nécessaire pour activer la connexion sociale Facebook.

Pour créer une application Facebook, suivez les instructions de Facebook à l’adresse [https://developers.facebook.com/apps/](https://developers.facebook.com/apps/). Les modifications apportées à leurs instructions ne sont pas répercutées dans les informations suivantes.

En général, à partir de l’API Facebook v2.7 :

* *ajouter une nouvelle application Facebook*
   * Pour *Plateforme*, sélectionnez Site Web :
      * Pour l’URL ** du site, entrez `  https://<server>:<port>.`
      * Pour Nom ** d’affichage, saisissez un titre à utiliser comme titre du service de connexion Facebook.
      * Pour *la Catégorie*, il est recommandé de choisir *des applications pour les pages*, mais cela peut être tout.
      * *ajouter le produit :  Connexion Facebook*
      * Pour les URI *de redirection OAuth* valides, saisissez `  https://<server>:<port>.`

>[!NOTE]
>
>Pour le développement, http://localhost:4503 fonctionne.


Une fois l’application créée, localisez l’ID **** d’application et les paramètres **[!UICONTROL de secret d’application]** . Ces informations sont requises pour configurer le service [cloud](#createafacebookcloudservice)Facebook.

### Création d’un Cloud Service Facebook Connect {#create-a-facebook-connect-cloud-service}

L’instance Application OAuth et Fournisseur [Granite](#adobe-granite-oauth-application-and-provider) Adobe, instanciée par la création d’une configuration de service cloud, identifie l’application Facebook et le ou les groupes de membres auxquels les nouveaux utilisateurs sont ajoutés.

1. Sur l’instance d’auteur AEM, connectez-vous avec les droits d’administrateur.
1. Dans la navigation globale, sélectionnez **[!UICONTROL Outils]** > **[!UICONTROL Cloud Services]** > Configuration **[!UICONTROL de connexion à]** Facebook Social.
1. Sélectionnez le chemin **[!UICONTROL du]** contexte de configuration.

   **[!UICONTROL Le chemin]** de contexte doit être identique au chemin de configuration du cloud que vous avez sélectionné lors de la création/modification d’un site communautaire.

1. Vérifiez si votre chemin de contexte est activé pour créer des services cloud en dessous.
1. Go to **[!UICONTROL Tools]** > **[!UICONTROL General]** > **[!UICONTROL Configuration Browser]**. Sélectionnez votre contexte et modifiez les propriétés. Activez les Configurations de cloud si elles ne sont pas encore activées.

   ![config-propertiespng](assets/config-propertiespng.png)

1. **Créez/modifiez** la configuration du service cloud Facebook.

   ![fbsocialloginconfigpng](assets/fbsocialloginconfigpng.png)

   * **[!UICONTROL Titre]** (*obligatoire*) Saisissez un titre d’affichage qui identifie l’application Facebook. Il est recommandé d’utiliser le même nom saisi que le nom ** d’affichage pour l’application Facebook.
   * **[!UICONTROL ID d’application/clé]** d’API (*obligatoire*) Saisissez l’ID ***d’*** application pour l’application Facebook. Ceci identifie l’application OAuth de granite [d’Adobe et l’instance de fournisseur](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#AdobeGraniteOAuthApplicationandProvider) créée à partir de la boîte de dialogue.
   * **[!UICONTROL Secret]** de l’application (*Obligatoire*) Saisissez la Secret ***de l’*** application pour l’application Facebook.
   * **[!UICONTROL Créer des utilisateurs]** Si cette case est cochée, la connexion avec un compte Facebook créera une AEM entrée utilisateur et l’ajoutera en tant que membre au ou aux groupes d’utilisateurs sélectionnés.  La valeur par défaut est cochée (fortement recommandé).
   * **[!UICONTROL Masquer les identifiants]** utilisateur : Laissez-le désélectionné.
   * **[!UICONTROL Adresse électronique]** de l&#39;étendue : l’ID d’adresse électronique de l’utilisateur doit être récupéré à partir de Facebook.
   * **[!UICONTROL ajouter aux groupes]** d’utilisateurs sélectionnez Ajouter un groupe d’utilisateurs pour choisir un ou plusieurs groupes [de](https://helpx.adobe.com/experience-manager/6-3/communities/using/users.html) membres pour le site communautaire auquel les utilisateurs seront ajoutés.

   >[!NOTE]
   >
   >Les groupes peuvent être ajoutés ou supprimés à tout moment. Mais les adhésions des utilisateurs existants ne seront pas affectées. L’abonnement automatique s’applique uniquement aux nouveaux utilisateurs créés après la mise à jour de ce champ. Pour les sites où les utilisateurs anonymes sont désactivés, choisissez d’ajouter des utilisateurs au groupe de membres de la communauté correspondant destiné à ce site communautaire fermé.

   * Select **[!UICONTROL SAVE]**.
   * **[!UICONTROL Publier]**.




Le résultat est une instance [Adobe OAuth Application et Provider](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#adobe-granite-oauth-application-and-provider) Granite qui ne nécessite pas de modification supplémentaire à moins d&#39;ajouter une étendue supplémentaire (autorisations). La portée par défaut est les autorisations standard pour la connexion à Facebook. Si une étendue supplémentaire est souhaitée, il est nécessaire de modifier directement la configuration OSGI. Si des modifications sont effectuées directement par le biais du système/de la console, évitez de modifier les configurations du service cloud à partir de l’interface utilisateur tactile afin d’éviter tout remplacement.

### Fournisseur OAuth Facebook AEM Communities {#aem-communities-facebook-oauth-provider}

Le fournisseur AEM Communities étend l’application OAuth Granite [Adobe et l’instance Provider](#adobe-granite-oauth-application-and-provider) .

Ce fournisseur devra être modifié pour :

* Autoriser les mises à jour des utilisateurs
* ajouter des champs supplémentaires [dans la portée](#adobe-granite-oauth-application-and-provider)

   * Tous les champs autorisés par défaut ne sont pas inclus par défaut.

Si des modifications sont nécessaires, sur chaque instance de publication AEM :

1. Connectez-vous avec des droits d’administrateur.
1. Navigate to the [Web Console](../../help/sites-deploying/configuring-osgi.md). Par exemple, http://localhost:4503/system/console/configMgr.
1. Localisez le fournisseur AEM Communities Facebook OAuth.
1. Sélectionnez l&#39;icône représentant un crayon à ouvrir pour modification.

   ![fboauthprov_png](assets/fboauthprov_png.png)

   * **[!UICONTROL ID du fournisseur OAuth]**

      (*Obligatoire*) La valeur par défaut est *soco-facebook*. Ne modifiez pas.

   * **[!UICONTROL Configuration du Cloud Service]**

      La valeur par défaut est `/etc/  cloudservices /  facebookconnect`. Ne modifiez pas.

   * **[!UICONTROL Configuration du service du fournisseur OAuth]**

      La valeur par défaut est `/apps/social/facebookprovider/config/`. Ne modifiez pas.

   * **[!UICONTROL Activer les balises]**

      Ne pas modifier.

   * **[!UICONTROL Chemin d’accès utilisateur]**

      Emplacement dans le référentiel dans lequel les données utilisateur sont stockées. Pour un site communautaire, afin d’assurer aux membres l’autorisation de vue de leur profil, le chemin d’accès doit être le chemin par défaut */domicile/utilisateurs/communauté*.

   * **[!UICONTROL Activer les champs]**

      Si cette case est cochée, les champs répertoriés sont spécifiés dans la demande à Facebook pour l’authentification et les informations de l’utilisateur. La valeur par défaut est désélectionnée.

   * **[!UICONTROL Champs]**

      Lorsque l’option Champs est activée, les champs suivants sont inclus lors de l’appel de l’API graphique Facebook. Les champs doivent être autorisés dans l’étendue définie dans la configuration du service cloud. Les champs supplémentaires peuvent nécessiter l’approbation de Facebook. Reportez-vous à la section Autorisations de connexion Facebook de la documentation Facebook. Les champs par défaut ajoutés en tant que paramètres sont les suivants :

      * id
      * name
      * first_name
      * last_name
      * lien
      * paramètres régionaux
      * picture
      * timezone
      * update_time
      * vérifié
      * email

   Si un champ est ajouté ou modifié, mettez à jour la configuration correspondante du gestionnaire de synchronisation par défaut pour corriger le mappage.

   * **[!UICONTROL Mettre à jour l&#39;utilisateur]**

      Si cette option est cochée, actualise les données utilisateur dans le référentiel à chaque connexion afin de refléter les modifications de profil ou les données supplémentaires demandées. La valeur par défaut est désélectionnée.


#### Étapes suivantes {#next-steps}

Les étapes suivantes sont les mêmes pour Facebook et Twitter :

* [Publication des configurations de service cloud](#publishcloudservices)
* [Activation pour un site communautaire](#enable-social-login)

## Twitter Login {#twitter-login}

### Création d’une application Twitter {#create-a-twitter-app}

Une application Twitter configurée est requise pour activer la connexion sociale Twitter.

Suivez les dernières instructions pour créer une application Twitter à l’adresse [https://apps.twitter.com](https://apps.twitter.com/).

En général :

1. Entrez un *Nom* qui identifiera votre application Twitter aux utilisateurs de votre site Web.
1. Saisissez une *description*.
1. Pour le *site Web* , entrez `https://<server>`.
1. Pour URL *de* rappel, saisissez `https://server`.

   >[!NOTE]
   >
   >Il n&#39;est pas nécessaire de spécifier le port.
   >
   >Pour le développement, https://127.0.0.1/ fonctionne.

1. Une fois l’application créée, localisez la clé **[!UICONTROL Clé]** **[!UICONTROL de consommation (API) et la clé secrète]** consommateur (API). Ces informations seront nécessaires pour configurer le service [cloud](#createatwittercloudservice)Twitter.

#### Autorisations {#permissions}

Dans la section des autorisations de la gestion des applications Twitter, procédez comme suit :

* **[!UICONTROL Accès]**: Sélectionnez `Read only`.

   * Les autres options ne sont pas prises en charge

* **[!UICONTROL Autres autorisations]**: Vous pouvez également choisir `Request email addresses from users`.

   * Si cette option n’est pas sélectionnée, l’profil utilisateur AEM n’inclut pas son adresse électronique.
   * Les instructions de Twitter indiquent les étapes supplémentaires à suivre.

La seule demande REST envoyée pour la connexion sociale consiste à *[GET/vérifier les informations d’identification](https://dev.twitter.com/rest/reference/get/account/verify_credentials)* du compte.

### Création d’un Cloud Service Twitter Connect {#create-a-twitter-connect-cloud-service}

L’instance Application OAuth et Fournisseur [Granite](#adobe-granite-oauth-application-and-provider) Adobe, instanciée par la création d’une configuration de service cloud, identifie l’application Twitter et le ou les groupes de membres auxquels les nouveaux utilisateurs sont ajoutés.

1. Sur l’instance d’auteur, connectez-vous avec les droits d’administrateur.
1. Dans la navigation globale, sélectionnez **[!UICONTROL Outils]** > **[!UICONTROL Cloud Services]** > Configuration **[!UICONTROL de connexion à]** Twitter Social.
1. Sélectionnez la configuration du chemin **[!UICONTROL de]** contexte.

   Le chemin de contexte doit être identique au chemin de configuration du cloud que vous avez sélectionné lors de la création/modification d’un site communautaire.

1. Vérifiez si votre chemin de contexte est activé pour créer des services cloud en dessous.
1. Go to **[!UICONTROL Tools]** > **[!UICONTROL General]** > **[!UICONTROL Configuration Browser]**. Sélectionnez votre contexte et modifiez les propriétés. Activez les Configurations de cloud si elles ne sont pas encore activées.

   ![twitterconfigproppng](assets/twitterconfigproppng.png)

1. Créez/modifiez la configuration du service cloud Twitter.

   ![twittersocialloginpng](assets/twittersocialloginpng.png)

   * **[!UICONTROL Titre]**

      (*Obligatoire*) Saisissez un titre d’affichage qui identifie l’application Twitter. Il est recommandé d’utiliser le même nom saisi que le nom ** d’affichage pour l’application Twitter.

   * **[!UICONTROL Clé du client]**

      (*Obligatoire*) Saisissez la clé **** Consommateur (API) pour l’application Twitter. Ceci identifie l’application OAuth de granite [d’Adobe et l’instance de fournisseur](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#AdobeGraniteOAuthApplicationandProvider) créée à partir de la boîte de dialogue.

   * **[!UICONTROL Secret de consommateur]**

      (*Obligatoire*) Saisissez la clé secrète ****** Consumer(API) pour l’application Twitter.

   * **[!UICONTROL Créer des utilisateurs]**

      Si cette case est cochée, la connexion avec un compte Twitter créera une entrée d’utilisateur AEM et l’ajoutera en tant que membre au ou aux groupes d’utilisateurs sélectionnés. La valeur par défaut est cochée (fortement recommandé).

   * **[!UICONTROL Masquer les identifiants utilisateur]**

      Laissez-le désélectionné.

   * **[!UICONTROL Ajouter aux groupes d’utilisateurs]**

      Sélectionnez Ajouter un groupe d’utilisateurs pour choisir un ou plusieurs groupes [de](https://helpx.adobe.com/experience-manager/6-3/communities/using/users.html) membres pour le site communautaire auquel les utilisateurs seront ajoutés.
   >[!NOTE]
   >
   >Les groupes peuvent être ajoutés ou supprimés à tout moment. Mais les adhésions des utilisateurs existants ne seront pas affectées. L’abonnement automatique s’applique uniquement aux nouveaux utilisateurs créés après la mise à jour de ce champ. Pour les sites sur lesquels les utilisateurs anonymes sont désactivés, ajoutez des utilisateurs au groupe de membres de la communauté correspondant destiné à ce site de la communauté fermé.

1. Sélectionnez **[!UICONTROL ENREGISTRER]** et **[!UICONTROL publier]**.

Le résultat est une instance [Adobe Granite OAuth Application et Provider](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#adobe-granite-oauth-application-and-provider) qui ne nécessite pas de modification supplémentaire. La portée par défaut est les autorisations standard pour la connexion à Twitter.

### Fournisseur OAuth Twitter AEM Communities {#aem-communities-twitter-oauth-provider}

La configuration AEM Communities étend l’ [Adobe Granite OAuth Application et l’instance Provider](#adobe-granite-oauth-application-and-provider) . Ce fournisseur devra être modifié pour autoriser les mises à jour des utilisateurs.

Si des modifications sont nécessaires, sur chaque instance de publication AEM :

1. Connectez-vous avec des droits d’administrateur.
1. Navigate to the [Web Console](../../help/sites-deploying/configuring-osgi.md).

   Par exemple, http://localhost:4503/system/console/configMgr.

1. Localisez le fournisseur OAuth Twitter AEM Communities.
1. Sélectionnez l&#39;icône représentant un crayon à ouvrir pour modification.

   ![twitteroauth_png](assets/twitteroauth_png.png)

   * **[!UICONTROL ID du fournisseur OAuth]**

   (*Obligatoire*) La valeur par défaut est *soco-twitter*. Ne modifiez pas.

   * **[!UICONTROL Configuration du Cloud Service]**

      The default value is *conf.* Ne modifiez pas.

   * **[!UICONTROL Configuration du service du fournisseur OAuth]**

      La valeur par défaut est `/apps/social/twitterprovider/config/`. Ne modifiez pas.

   * **[!UICONTROL Chemin d’accès utilisateur]**

      Emplacement dans le référentiel dans lequel les données utilisateur sont stockées. Pour un site de la communauté, pour s&#39;assurer que les membres disposent des autorisations nécessaires pour vue de leur profil, le chemin d&#39;accès doit être le chemin par défaut `/home/users/community`.

   * **[!UICONTROL Activer les paramètres]** ne pas modifier
   * **[!UICONTROL Les paramètres]** d’URL ne sont pas modifiés
   * **[!UICONTROL Mettre à jour l&#39;utilisateur]**

      Si cette option est cochée, actualise les données utilisateur dans le référentiel à chaque connexion afin de refléter les modifications de profil ou les données supplémentaires demandées. La valeur par défaut est désélectionnée.


#### Étapes suivantes {#next-steps-1}

Les étapes suivantes sont les mêmes pour Facebook et Twitter :

* [Publication des configurations de service cloud](#publishcloudservices)
* [Activation pour un site communautaire](#enable-social-login)

## Activer la connexion aux réseaux sociaux {#enable-social-login}

### Console de sites AEM Communities {#aem-communities-sites-console}

Une fois qu’un service cloud est configuré, il peut être activé pour le paramètre Connexion sociale approprié pour un site communautaire à l’aide du sous-panneau Paramètres de gestion [](https://helpx.adobe.com/experience-manager/6-3/communities/using/sites-console.html#USERMANAGEMENT) utilisateur lors de la [création](https://helpx.adobe.com/experience-manager/6-3/communities/using/sites-console.html#SiteCreation) ou de la [gestion](https://helpx.adobe.com/experience-manager/6-3/communities/using/sites-console.html#ModifyingSiteProperties)d’un site communautaire.

1. Sélectionnez le contexte de configuration de votre site dans lequel vous avez enregistré vos configurations de connexion sociale.

1. Sous l’onglet Général, définissez les configurations de cloud.

   ![managesites_png](assets/managesites_png.png)

1. Sous l’onglet Paramètres, activez **[!UICONTROL Social Logins]** et Save.

   ![usermgmt_png](assets/usermgmt_png.png)

## Test de la connexion aux réseaux sociaux {#test-social-login}

* Assurez-vous que le gestionnaire [d’authentification OAuth Granite](#adobe-granite-oauth-authentication-handler) Adobe a été activé sur toutes les instances de publication.
* Vérifiez que les services cloud ont été publiés.
* Vérifier que le site communautaire a été publié.
* Lancez le site publié dans un navigateur.
Par exemple, http://localhost:4503/content/sites/engage/en.html
* Sélectionnez **[!UICONTROL Connexion]**.
* Sélectionnez **[!UICONTROL Se connecter avec Facebook]** ou **[!UICONTROL Se connecter avec Twitter]**.
* Si vous n’êtes pas encore connecté à Facebook ou Twitter, connectez-vous avec les informations d’identification appropriées.
* Il peut s’avérer nécessaire d’accorder une autorisation en fonction de la boîte de dialogue affichée par l’application Facebook ou Twitter.
* Notez que la barre d’outils située en haut de la page est mise à jour pour refléter la connexion réussie.
* Sélectionner le **[!UICONTROL Profil]**: la page de Profil affiche l’avatar, le prénom et le nom de l’utilisateur. Il affiche également les informations du profil Facebook ou Twitter en fonction des champs/paramètres autorisés.

## AEM Platform OAuth Configurations {#aem-platform-oauth-configurations}

### Adobe Granite OAuth Authentication Handler {#adobe-granite-oauth-authentication-handler}

Par défaut, l’option `Adobe Granite OAuth Authentication Handler` n’est pas activée et ***doit l’être sur toutes les instances de publication AEM.***

Pour activer le gestionnaire d’authentification lors de la publication, il vous suffit d’ouvrir la configuration OSGi et de l’enregistrer :

* Connectez-vous avec des droits d’administrateur.
* Navigate to the [Web Console](../../help/sites-deploying/configuring-osgi.md).
Par exemple, http://localhost:4503/system/console/configMgr
* Localisez `Adobe Granite OAuth Authentication Handler`.
* Sélectionnez cette option pour ouvrir la configuration à modifier.
* Sélectionnez **[!UICONTROL Enregistrer]**.

![chlimage_1-489](assets/chlimage_1-489.png)

>[!CAUTION]
>
>Veillez à ne pas confondre le gestionnaire d’authentification avec une instance Facebook ou Twitter de l’application OAuth et du fournisseur *Granite* Adobe.


![chlimage_1-490](assets/chlimage_1-490.png)

### adobe Granite OAuth Application et fournisseur {#adobe-granite-oauth-application-and-provider}

Lorsqu’un service cloud pour Facebook ou Twitter est créé, une instance de `Adobe Granite OAuth Authentication Handler` est créée.

Pour localiser l’instance créée pour une application Facebook ou Twitter :

1. Connectez-vous avec des droits d’administrateur.
1. Navigate to the [Web Console](../../help/sites-deploying/configuring-osgi.md).

   Par exemple, http://localhost:4503/system/console/configMgr.

1. Localisez l’application et le fournisseur OAuth Granite Adobe.

   * Localisez l’instance où l’ID **** client correspond à l’ID **[!UICONTROL de l’]** application.

      ![chlimage_1-491](assets/chlimage_1-491.png)

      A l’exception des propriétés suivantes, ne modifiez pas les autres propriétés de la configuration :

   * **[!UICONTROL ID de configuration]**

      (*Obligatoire*) Les ID de configuration OAuth doivent être uniques. Généré automatiquement lors de la création du service cloud.

   * **[!UICONTROL ID client]**

      (*Obligatoire*) ID de l&#39;application fourni lors de la création du service cloud.

   * **[!UICONTROL Secret client]**

      (*Obligatoire*) clé secrète fournie lors de la création du service cloud.

   * **[!UICONTROL Portée]**

      (*Facultatif*) Le fournisseur peut demander à un fournisseur d’autres informations sur ce qui est autorisé. La portée par défaut couvre les autorisations nécessaires pour fournir l’authentification sociale et les données de profil.

   * **[!UICONTROL ID du fournisseur]**

      (*Obligatoire*) L’ID de fournisseur pour AEM Communities est défini lors de la création du service cloud. Ne modifiez pas. Pour Facebook Connect, la valeur est *soco-facebook*. Pour Twitter Connect, la valeur est *soco-twitter*.

   * **[!UICONTROL Groupes]**

      (*Recommandé*) Un ou plusieurs groupes de membres auxquels des utilisateurs créés sont ajoutés. Pour AEM Communities, il est recommandé de liste du groupe de membres pour le site communautaire.

   * **[!UICONTROL URL de rappel]**

      (*Facultatif*) URL configurée avec les fournisseurs OAuth pour rediriger le client. Utilisez une URL relative pour utiliser l’hôte de la requête d’origine. Laissez vide pour utiliser l’URL demandée d’origine à la place. Le suffixe &quot;/callback/j_security_check&quot; est automatiquement ajouté à cette URL.
   >[!NOTE]
   >
   >Le domaine du rappel doit être enregistré auprès du fournisseur (Facebook ou Twitter).

Pour chaque configuration du gestionnaire d’authentification OAuth, deux configurations supplémentaires sont créées dans l’instance :

* Gestionnaire de synchronisation par défaut d’Apache Jackrabbit Oak (org.apache.jackrabbit.oak.spi.security.authentication.external.impl.DefaultSyncHandler) - Aucune modification n’est requise, mais vous pouvez examiner les mappages de champs utilisateur comment les champs Facebook sont mappés à un noeud de profil d’utilisateur CQ. Notez également que &quot;Nom du gestionnaire de synchronisation&quot; correspond à l’ID de configuration du fournisseur OAuth.
* Module de connexion externe Apache Jackrabbit Oak (org.apache.jackrabbit.oak.spi.security.authentication.external.impl.ExternalLoginModuleFactory) - Aucune modification n&#39;est requise ici, mais vous pouvez remarquer que &#39;Nom du fournisseur d&#39;identité&#39; et &#39;Nom du gestionnaire de synchronisation&#39; sont identiques et pointent vers les configurations OAuth et de gestionnaire de synchronisation correspondantes, respectivement.

For more information, see [Authentication with Apache Oak External Login Module](https://jackrabbit.apache.org/oak/docs/security/authentication/externalloginmodule.html).

## Performances de conversion des utilisateurs OAuth {#oauth-user-traversal-performance}

Pour les sites de la communauté qui voient des centaines de milliers d’utilisateurs s’inscrire en utilisant leur connexion Facebook ou Twitter, les performances de traversée de la requête effectuée lorsqu’un visiteur du site utilise sa connexion sociale peuvent être améliorées en ajoutant l’index Oak suivant.

Si des avertissements de traversée sont affichés dans les journaux, il est recommandé d’ajouter cet index.

Sur une instance d’auteur, connectée avec des privilèges d’administration :

1. A partir de la navigation globale : sélectionnez **Outils,[CRX/DE Lite](../../help/sites-developing/developing-with-crxde-lite.md).**
1. Créez un index nommé ntBaseLucene-oauth à partir d&#39;une copie de ntBaseLucene :

   * Sous le noeud `/oak:index`
   * Sélectionner un noeud `ntBaseLucene`
   * Sélectionner une **[!UICONTROL copie]**
   * Sélectionner `/oak:index`
   * Sélectionner **[!UICONTROL Coller]**
   * Renommez Copie de ntBaseLucene en `ntBaseLucene-oauth`

1. Modifiez les propriétés du noeud ntBaseLucene-oauth :

   * **[!UICONTROL indexPath]**: `/oak:index/ntBaseLucene-oauth`
   * **[!UICONTROL name]**: `oauthid-123****`
   * **[!UICONTROL réindexer]**: `true`
   * **[!UICONTROL reindexCount]**: `1`

1. Sous le noeud /oak:index/ntBaseLucene-oauth/indexRules/nt:base/properties :

   * Supprimez tous les noeuds enfants, à l’exception de cqTags.
   * Renommer cqTags en `oauthid-123****`
   * Modification des propriétés du noeud `oauthid-123****`

      * **[!UICONTROL name]**: `oauthid-123****`
   * Select **[!UICONTROL Save All]**.


* Pour le **nom** `oauthid-123`, remplacez *123* par l’ID ****** d’application Facebook ou la clé Twitter Consumer (API) Key qui correspond à la valeur de l’ID de client de l’Adobe dans la configuration de l’application OAuth et de l’ Provider Granite.**********[](social-login.md#adobe-granite-oauth-application-and-provider)

   ![chlimage_1-492](assets/chlimage_1-492.png)

Pour plus d&#39;informations et d&#39;outils, reportez-vous aux Requêtes [en chêne et à l&#39;indexation](../../help/sites-deploying/queries-and-indexing.md).

## Configuration du Dispatcher {#dispatcher-configuration}

Voir [Configuration du répartiteur pour les communautés](dispatcher.md).
