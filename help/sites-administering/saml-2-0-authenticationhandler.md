---
title: Gestionnaire d’authentification SAML 2.0
seo-title: SAML 2.0 Authentication Handler
description: Découvrez le gestionnaire d’authentification SAML 2.0 dans AEM.
seo-description: Learn about the SAML 2.0 Authentication Handler in AEM.
uuid: 51f97315-350a-42a4-af2c-2de87307c6ad
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 6ed09b5d-5089-43d2-b9d5-e7db57be5c02
exl-id: 8e54bccf-0ff1-448d-a237-ec42fd3bfa23
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 83%

---

# Gestionnaire d’authentification SAML 2.0 {#saml-authentication-handler}

AEM est livré avec un gestionnaire d’authentification [SAML](https://saml.xml.org/saml-specifications). Ce gestionnaire fournit la prise en charge du protocole de requête d’authentification [SAML](https://saml.xml.org/saml-specifications) 2.0 (profil Web-SSO) à l’aide de la liaison `HTTP POST`.

Il prend en charge :

* signature et cryptage des messages
* la création automatique d’utilisateurs ;
* la synchronisation des groupes avec les groupes existants dans AEM.
* Authentification initiée par le fournisseur et le fournisseur d’identité

Ce gestionnaire stocke le message de réponse SAML chiffré dans le nœud utilisateur (`usernode/samlResponse`) pour faciliter la communication avec un fournisseur tiers.

>[!NOTE]
>
>Consultez [une démonstration de l’intégration d’AEM et de SAML](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17481.html?lang=fr).

## Configurer le gestionnaire d’authentification SAML 2.0 {#configuring-the-saml-authentication-handler}

La [console web](/help/sites-deploying/configuring-osgi.md) permet d’accéder à la configuration de gestionnaire d’authentification [SAML](https://saml.xml.org/saml-specifications) 2.0 appelée **Gestionnaire d’authentification SAML 2.0 Adobe Granite**. Les propriétés suivantes peuvent être définies.

>[!NOTE]
>
>Le gestionnaire d’authentification SAML 2.0 est désactivé par défaut. Définissez au moins l’une des propriétés suivantes pour activer le gestionnaire :
>
>* URL POST du fournisseur d’identité ou URL du fournisseur d’identité.
>* Identifiant d’entité du fournisseur de services.
>

>[!NOTE]
>
>Les assertions SAML sont signées et peuvent éventuellement être chiffrées. Pour que cela fonctionne, vous devez fournir au moins le certificat public du fournisseur d’identité dans TrustStore. Consultez la section [Ajout de certificat IdP à TrustStore](/help/sites-administering/saml-2-0-authenticationhandler.md#add-the-idp-certificate-to-the-aem-truststore) pour plus d’informations.

**Chemin** Chemin du référentiel pour lequel ce gestionnaire d’authentification doit être utilisé par Sling. Si le champ est vide, le gestionnaire d’authentification est désactivé.

**Classements des services** Valeur de classement de service de structure OSGi pour indiquer l’ordre dans lequel appeler ce service. Il s’agit d’un nombre entier, et les valeurs les plus élevées indiquent une priorité plus élevée.

**Alias de certificat IDP** L’alias du certificat IdP dans le TrustStore global. Si cette propriété n’est pas renseignée, le gestionnaire d’authentification est désactivé. Consultez le chapitre &quot;Ajout du certificat IdP à l’AEM TrustStore&quot; ci-dessous sur la manière de le configurer.

**URL du fournisseur d’identité** : URL du fournisseur d’identité où la requête d’authentification SAML doit être envoyée. Si cette propriété n’est pas renseignée, le gestionnaire d’authentification est désactivé.

>[!CAUTION]
>
>Le nom d’hôte du fournisseur d’identité doit être ajouté à la configuration OSGi **Filtre de référents Sling Apache**. Consultez la section [Console web](/help/sites-deploying/configuring-osgi.md) pour plus d’informations.

**ID d’entité du fournisseur de services** Identifiant qui identifie de manière unique ce fournisseur de services auprès du fournisseur d’identité. Si cette propriété n’est pas renseignée, le gestionnaire d’authentification est désactivé.

**Redirection Par défaut** Emplacement par défaut de redirection après une authentification réussie.

>[!NOTE]
>
>Cet emplacement est utilisé uniquement si le cookie `request-path` n’est pas défini. Si vous demandez une page sous le chemin configuré sans jeton de connexion valide, le chemin demandé est stocké dans un cookie
>et le navigateur sera redirigé vers cet emplacement après une authentification réussie.

**Attribut ID de l’utilisateur** Nom de l’attribut contenant l’ID utilisateur utilisé pour authentifier et créer l’utilisateur dans le référentiel CRX.

>[!NOTE]
>
>L’ID utilisateur n’est pas obtenu à partir du nœud `saml:Subject` de l’assertion SAML, mais à partir de ce `saml:Attribute`.

**Utilisation du chiffrage** Si ce gestionnaire d’authentification attend ou non des assertions SAML chiffrées.

**Autocréation d’utilisateurs CRX** Créer automatiquement ou non les utilisateurs non existants dans le référentiel après une authentification réussie.

>[!CAUTION]
>
>Si la création automatique des utilisateurs CRX est désactivée, les utilisateurs doivent être créés manuellement.

**Ajouter aux groupes** Si un utilisateur doit ou non être automatiquement ajouté aux groupes CRX après une authentification réussie.

**Appartenance à un groupe** Nom du saml:Attribute contenant une liste de groupes CRX auxquels cet utilisateur doit être ajouté.

## Ajoutez le certificat IdP au TrustStore AEM {#add-the-idp-certificate-to-the-aem-truststore}

Les assertions SAML sont signées et peuvent éventuellement être chiffrées. Pour que cela fonctionne, vous devez fournir au moins le certificat public de l’IdP dans le référentiel. Pour ce faire, vous devez :

1. Accédez à *http:/serveraddress:serverport/libs/granite/security/content/truststore.html*.
1. Appuyez sur **[!UICONTROL Créer un lien TrustStore]**.
1. Saisissez le mot de passe du TrustStore, puis appuyez sur **[!UICONTROL Enregistrer]**.
1. Cliquez sur **[!UICONTROL Gestion de TrustStore]**.
1. Téléchargez le certificat IdP.
1. Notez l’alias du certificat. L’alias est **[!UICONTROL admin#1436172864930]** dans l’exemple ci-dessous.

   ![chlimage_1-372](assets/chlimage_1-372.png)

## Ajoutez la clé de fournisseur et la chaîne de certificats au KeyStore AEM. {#add-the-service-provider-key-and-certificate-chain-to-the-aem-keystore}

>[!NOTE]
>
>Les étapes ci-dessous sont obligatoires, sinon l’exception suivante sera générée : `com.adobe.granite.keystore.KeyStoreNotInitialisedException: Uninitialised system trust store`.

1. Accédez à [http://localhost:4502/libs/granite/security/content/useradmin.html](http://localhost:4502/libs/granite/security/content/useradmin.html).
1. Modifiez l’utilisateur `authentication-service`.
1. Créez un KeyStore en cliquant sur **Créer le KeyStore** sous **Paramètres du compte**.

>[!NOTE]
>
>Les étapes suivantes ne sont nécessaires que si le gestionnaire doit pouvoir signer ou déchiffrer des messages.

1. Créez le certificat/la paire de clés pour AEM. La commande pour les générer via openssl doit ressembler à l’exemple ci-dessous :

   `openssl req -newkey rsa:2048 -new -x509 -days 3652 -nodes -out certificate.crt -keyout key.pem`

1. Convertissez la clé au format PKCS#8 avec le codage DER. Il s’agit du format requis par le KeyStore AEM.

   `openssl pkcs8 -topk8 -inform PEM -outform DER -in key.pem -out key.der -nocrypt`

1. Téléchargez le fichier de clé privée en cliquant sur **Sélectionner le fichier de clé privée**.
1. Téléchargez le fichier de certificat en cliquant sur **Sélectionner les fichiers de chaîne de certificats**.
1. Attribuez un alias, comme illustré ci-dessous :

   ![chlimage_1-373](assets/chlimage_1-373.png)

## Configuration d’un journal pour SAML {#configure-a-logger-for-saml}

Vous pouvez configurer un enregistreur pour déboguer les problèmes qui peuvent survenir lors d’une mauvaise configuration de SAML. Vous pouvez le faire en procédant comme suit :

1. Accédez à la console web à l’adresse *http://localhost:4502/system/console/configMgr*.
1. Recherchez et cliquez sur l’entrée nommée **Configuration de l’enregistreur de connexion Sling Apache** et cliquez dessus.
1. Créez un journal avec la configuration suivante :

   * **Niveau de journal :** Déboguer
   * **Fichier journal :** logs/saml.log
   * **Enregistreur :** com.adobe.granite.auth.saml
