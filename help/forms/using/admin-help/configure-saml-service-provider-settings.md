---
title: Configuration des paramètres du fournisseur de services SAML
seo-title: Configuration des paramètres du fournisseur de services SAML
description: Vous pouvez configurer les paramètres du fournisseur de services SAML pour permettre aux utilisateurs de se connecter et de s’authentifier auprès d’AEM forms via un fournisseur d’identité tiers (IDP) spécifié.
seo-description: Vous pouvez configurer les paramètres du fournisseur de services SAML pour permettre aux utilisateurs de se connecter et de s’authentifier auprès d’AEM forms via un fournisseur d’identité tiers (IDP) spécifié.
uuid: 14c706ad-8b1c-4c03-9cd4-97424f2162bc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 1169d0d1-cbfb-486b-acca-9b9de3d410dc
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configuration des paramètres du fournisseur de services SAML{#configure-saml-service-provider-settings}

Security Assertion Markup Language (SAML) est l’une des options que vous pouvez sélectionner lors de la configuration des autorisations relatives aux domaines d’entreprise ou domaines hybrides. Le langage SAML est principalement utilisé pour la prise en charge de l’authentification unique sur plusieurs domaines. Lorsque ce langage est configuré comme fournisseur d’authentification, les utilisateurs se connectent et s’authentifient à AEM forms via un fournisseur d’identité tiers (IDP) spécifié.

Pour de plus amples informations sur le langage SAML, voir [Présentation technique du langage SAML (Security Assertion Markup Language) (en anglais)](https://www.oasis-open.org/committees/download.php/20645/sstc-saml-tech-overview-2%200-draft-10.pdf).

1. Dans Administration Console, cliquez sur Paramètres > User Management > Configuration > Paramètres du fournisseur de services SAML.
1. Dans la zone ID d’entité du fournisseur de services, saisissez un ID univoque qui servira d’identifiant pour la mise en œuvre du fournisseur de services AEM forms. Vous pouvez également définir cet ID unique lors de la configuration du fournisseur d’identité (par exemple, `um.lc.com`). Vous pouvez également utiliser l’URL d’accès à AEM forms (par exemple, `https://AEMformsserver`).
1. Dans le champ URL de base du fournisseur de services, saisissez l’URL de base du serveur Forms (par exemple, `https://AEMformsserver:8080`).
1. (Facultatif) Pour autoriser AEM forms à envoyer des demandes d’authentification signées au fournisseur d’identité, procédez comme suit :

   * Utilisez Trust Manager pour importer des informations d’identification au format PKCS #12 avec Type de Trust Store défini sur Informations d’identification de signature de document (voir [Gestion d’informations d’identification locales](/help/forms/using/admin-help/local-credentials.md#managing-local-credentials)).
   * Dans la liste Alias principal des informations d’identification du fournisseur de services, sélectionnez l’alias affecté aux informations d’identification du Trust Store.
   * Cliquez sur Exporter pour enregistrer le contenu de l’URL dans un fichier et importer ce dernier dans le fournisseur d’identité.

1. (Facultatif) Dans la liste Stratégie d’ID de nom du fournisseur de services, sélectionnez le format de nom utilisé par le fournisseur d’identité pour identifier l’utilisateur dans une assertion SAML. Les options disponibles sont Non spécifié, Adresse électronique et Nom qualifié de domaine Windows.

   >[!NOTE]
   >
   >les formats de nom ne sont pas sensibles à la casse.

1. (Facultatif) Sélectionnez Activer l’invite d’authentification pour les utilisateurs locaux. Lorsque cette option est sélectionnée, deux liens s’affichent :

   * un lien vers la page de connexion du fournisseur d’identité SAML tiers, dans laquelle les utilisateurs appartenant à un domaine d’entreprise peuvent s’authentifier ;
   * un lien vers la page de connexion AEM forms, dans laquelle les utilisateurs appartenant à un domaine local peuvent s’authentifier.
   Lorsque cette option n’est pas sélectionnée, les utilisateurs sont directement dirigés vers la page de connexion du fournisseur d’identité SAML tiers, dans laquelle les utilisateurs appartenant à un domaine d’entreprise peuvent s’authentifier.

1. (Facultatif) Sélectionnez Activer la liaison d’artefact pour activer la prise en charge de la liaison d’artefact. Par défaut, la liaison POST est utilisée avec le langage SAML. Mais si vous avez configuré la liaison d’artefact, sélectionnez cette option. Lorsque cette option est sélectionnée, l’assertion de l’utilisateur ne passe pas par la requête navigateur. C’est un pointeur vers cette assertion qui est passé et cette dernière est récupérée via un appel au service Web du serveur principal.
1. (Facultatif) Sélectionnez Activer Rediriger la liaison, pour la prise en charge des liaisons SAML utilisant les redirections.
1. (Facultatif) Dans Propriétés personnalisées, définissez des propriétés supplémentaires. Ces propriétés sont des paires nom=valeur séparées par des nouvelles lignes.

   * Vous pouvez configurer AEM forms afin d’émettre une assertion SAML pour une période de validité correspondant à la période de validité d’une assertion tierce. Pour respecter le délai d’expiration de l’assertion SAML tierce, ajoutez la ligne suivante dans Propriétés personnalisées :

      `saml.sp.honour.idp.assertion.expiry=true`

   * Ajoutez la propriété personnalisée suivante pour utiliser RelayState afin de déterminer l’URL vers laquelle l’utilisateur sera redirigé après son authentification.

      `saml.sp.use.relaystate=true`

   * Ajoutez la propriété personnalisée suivante afin de configurer l’URL pour le JSP (Java Server Pages) personnalisé, celle-ci sera utilisée pour effectuer le rendu de la liste enregistrée des fournisseurs d’identité. Si vous n’avez pas déployé d’application Web personnalisée, la page User Management par défaut sera utilisée pour effectuer le rendu de la liste.
   `saml.sp.discovery.url=/custom/custom.jsp`

1. Cliquez sur Enregistrer.

