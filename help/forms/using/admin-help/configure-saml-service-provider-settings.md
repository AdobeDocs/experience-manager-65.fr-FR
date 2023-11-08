---
title: Configurer les paramètres du fournisseur de services SAML
seo-title: Configure SAML service provider settings
description: Vous pouvez configurer les paramètres du fournisseur de services SAML pour permettre aux utilisateurs de se connecter et de s’authentifier auprès d’AEM forms via un fournisseur d’identité tiers (IDP) spécifié.
seo-description: You can configure SAML service provider settings to allow users to login and authenticate to AEM forms via a specified third-party identity provider (IDP).
uuid: 14c706ad-8b1c-4c03-9cd4-97424f2162bc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 1169d0d1-cbfb-486b-acca-9b9de3d410dc
exl-id: dd302cfb-eae1-4189-aa7b-9f2533ebd164
source-git-commit: c4cd9a61a226ace2a72d60b5b7b7432de12cb873
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 7%

---

# Configurer les paramètres du fournisseur de services SAML{#configure-saml-service-provider-settings}

Le langage SAML (Security Assertion Markup Language) est l’une des options que vous pouvez sélectionner lors de la configuration de l’autorisation d’un domaine d’entreprise ou hybride. SAML est principalement utilisé pour la prise en charge de l’authentification unique sur plusieurs domaines. Lorsque SAML est configuré en tant que fournisseur d’authentification, les utilisateurs se connectent et s’authentifient à AEM forms via un fournisseur d’identité tiers spécifié.

Pour obtenir une explication de SAML, voir [Présentation technique du langage SAML (Security Assertion Markup Language) V2.0](https://www.oasis-open.org/committees/download.php/20645/sstc-saml-tech-overview-2%200-draft-10.pdf).

1. Dans Administration Console, cliquez sur Paramètres > User Management > Configuration > Paramètres du fournisseur de services SAML.
1. Dans la zone ID d’entité du fournisseur de services, saisissez un identifiant unique à utiliser comme identifiant pour l’implémentation du fournisseur de services AEM forms. Vous pouvez également définir cet ID unique lors de la configuration du fournisseur d’identité (par exemple, `um.lc.com`). Vous pouvez également utiliser l’URL d’accès à AEM forms (par exemple, `https://AEMformsserver`).
1. Dans la zone URL de base du fournisseur de services, saisissez l’URL de base de votre serveur Forms (par exemple : `https://AEMformsserver:8080`).
1. (Facultatif) Pour permettre à AEM forms d’envoyer des demandes d’authentification signées au fournisseur d’identité, effectuez les tâches suivantes :

   * Utilisez Trust Manager pour importer des informations d’identification au format PKCS #12 avec des informations d’identification de signature de document sélectionnées comme type de Trust Store. (Voir [Gestion des informations d’identification locales](/help/forms/using/admin-help/local-credentials.md#managing-local-credentials).)
   * Dans la liste Alias de clé d’identification du fournisseur de services, sélectionnez l’alias affecté aux informations d’identification dans Trust Store.
   * Cliquez sur Exporter pour enregistrer le contenu de l’URL dans un fichier , puis importez ce fichier dans votre IDP.

1. (Facultatif) Dans la liste Stratégie d’ID de nom du fournisseur de services, sélectionnez le format de nom utilisé par le fournisseur d’identité pour identifier l’utilisateur dans une assertion SAML. Les options disponibles sont Non spécifié, Email et Nom qualifié de domaine Windows.

   >[!NOTE]
   >
   >Les formats de nom ne sont pas sensibles à la casse.

1. (Facultatif) Sélectionnez Activer l’invite d’authentification pour les utilisateurs locaux. Lorsque cette option est sélectionnée, les utilisateurs voient apparaître deux liens :

   * lien vers la page de connexion du fournisseur d’identité SAML tiers, dans laquelle les utilisateurs appartenant à un domaine d’entreprise peuvent s’authentifier.
   * lien vers la page de connexion d’AEM forms, sur laquelle les utilisateurs appartenant à un domaine local peuvent s’authentifier.

   Lorsque cette option n’est pas sélectionnée, les utilisateurs sont directement redirigés vers la page de connexion du fournisseur d’identité SAML tiers, dans laquelle les utilisateurs appartenant à un domaine d’entreprise peuvent s’authentifier.

1. (Facultatif) Sélectionnez Activer la liaison d’artefact pour activer la prise en charge de la liaison d’artefact. Par défaut, la liaison de POST est utilisée avec SAML. Mais si vous avez configuré la liaison d’artefact, sélectionnez cette option. Lorsque cette option est sélectionnée, l’assertion de l’utilisateur n’est pas transmise par le biais de la requête Navigateur. Au lieu de cela, un pointeur vers l’assertion est passé et l’assertion est récupérée à l’aide d’un appel de service Web principal.
1. (Facultatif) Sélectionnez Activer la liaison de redirection pour prendre en charge les liaisons SAML qui utilisent les redirections.
1. (Facultatif) Dans Propriétés personnalisées, spécifiez des propriétés supplémentaires. Les propriétés supplémentaires sont des paires nom=valeur séparées par de nouvelles lignes.

   * Vous pouvez configurer AEM forms pour émettre une assertion SAML pour une période de validité correspondant à celle d’une assertion tierce. Pour respecter le délai d’expiration de l’assertion SAML tierce, ajoutez la ligne suivante dans Propriétés personnalisées :

     `saml.sp.honour.idp.assertion.expiry=true`

   * Ajoutez la propriété personnalisée suivante pour utiliser RelayState afin de déterminer l’URL vers laquelle l’utilisateur sera redirigé après une authentification réussie.

     `saml.sp.use.relaystate=true`

   * Ajoutez la propriété personnalisée suivante pour configurer l’URL du JSP (Java Server Pages) personnalisé, qui est utilisé pour effectuer le rendu de la liste enregistrée des fournisseurs d’identité. Si vous n’avez pas déployé d’application web personnalisée, la page User Management par défaut sera utilisée pour effectuer le rendu de la liste.

   `saml.sp.discovery.url=/custom/custom.jsp`

1. Cliquez sur Enregistrer.
