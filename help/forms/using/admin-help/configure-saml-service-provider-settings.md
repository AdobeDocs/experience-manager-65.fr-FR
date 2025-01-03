---
title: Configuration des paramètres du fournisseur de services SAML
description: Vous pouvez configurer les paramètres du fournisseur de services SAML pour permettre aux utilisateurs et utilisatrices de se connecter et de s’authentifier auprès d’AEM Forms via un fournisseur d’identité (IDP) tiers spécifié.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: dd302cfb-eae1-4189-aa7b-9f2533ebd164
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 95%

---

# Configuration des paramètres du fournisseur de services SAML{#configure-saml-service-provider-settings}

>[!NOTE]
> 
> Vérifiez que l’utilisateur ou l’utilisatrice dispose de droits d’administration pour accéder à la console d’administration.

Le langage SAML (Security Assertion Markup Language) est l’une des options que vous pouvez sélectionner lors de la configuration de l’autorisation d’un domaine d’entreprise ou hybride. SAML est principalement utilisé pour la prise en charge de l’authentification unique sur plusieurs domaines. Lorsque SAML est configuré en tant que fournisseur d’authentification, les utilisateurs et utilisatrices se connectent et s’authentifient à AEM Forms via un fournisseur d’identité (IDP) tiers spécifié.

Pour obtenir une explication sur SAML, voir [Présentation technique du langage SAML (Security Assertion Markup Language) V2.0](https://docs.oasis-open.org/security/saml/Post2.0/sstc-saml-tech-overview-2.0.html).

1. Dans la console d’administration, cliquez sur Paramètres > Gestion des utilisateurs et utilisatrices > Configuration > Paramètres du fournisseur de services SAML.
1. Dans la zone ID d’entité du fournisseur de services, saisissez un ID unique à utiliser comme identifiant pour l’implémentation du fournisseur de services AEM Forms. Vous pouvez également définir cet ID unique lors de la configuration du fournisseur d’identité (par exemple, `um.lc.com`). Vous pouvez également utiliser l’URL d’accès à AEM forms (par exemple, `https://AEMformsserver`).
1. Dans le champ URL de base du fournisseur de services, saisissez l’URL de base du serveur Forms (par exemple, `https://AEMformsserver:8080`).
1. (Facultatif) Pour permettre à AEM Forms d’envoyer des demandes d’authentification signées à l’IDP, effectuez les tâches suivantes :

   * Utilisez Trust Manager pour importer des informations d’identification au format PKCS #12 avec des informations d’identification de signature de document sélectionnées comme type de Trust Store. (Voir [Gestion des informations d’identification locales](/help/forms/using/admin-help/local-credentials.md#managing-local-credentials).)
   * Dans la liste Alias de clé d’identification du fournisseur de services, sélectionnez l’alias affecté aux informations d’identification dans Trust Store.
   * Cliquez sur Exporter pour enregistrer le contenu de l’URL dans un fichier et importer ce dernier dans le fournisseur d’identité.

1. (Facultatif) Dans la liste Politique d’ID de nom du fournisseur de services, sélectionnez le format de nom utilisé par l’IDP pour identifier l’utilisateur ou l’utilisatrice dans une assertion SAML. Les options disponibles sont Non spécifié, E-mail et Nom qualifié de domaine Windows.

   >[!NOTE]
   >
   >Les formats de nom ne sont pas sensibles à la casse.

1. (Facultatif) Sélectionnez Activer l’invite d’authentification pour les utilisateurs et utilisatrices locaux. Lorsque cette option est sélectionnée, deux liens s’affichent :

   * un lien vers la page de connexion du fournisseur d’identité SAML tiers, sur laquelle les personnes appartenant à un domaine d’entreprise peuvent s’authentifier.
   * un lien vers la page de connexion d’AEM Forms, sur laquelle les personnes appartenant à un domaine local peuvent s’authentifier.

   Lorsque cette option n’est pas sélectionnée, les utilisateurs et utilisatrices sont directement redirigés vers la page de connexion du fournisseur d’identité SAML tiers, sur laquelle les personnes appartenant à un domaine d’entreprise peuvent s’authentifier.

1. (Facultatif) Sélectionnez Activer la liaison d’artefact pour activer la prise en charge de la liaison d’artefact. Par défaut, c’est la liaison POST qui est utilisée avec SAML. Mais si vous avez configuré la liaison d’artefact, sélectionnez cette option. Lorsque cette option est sélectionnée, l’assertion de la personne n’est pas transmise par le biais de la requête du navigateur. Au lieu de cela, un pointeur vers l’assertion est transmis et l’assertion est récupérée à l’aide d’un appel de service web principal.
1. (Facultatif) Sélectionnez Activer la liaison de redirection pour prendre en charge les liaisons SAML qui utilisent les redirections.
1. (Facultatif) Dans Propriétés personnalisées, spécifiez des propriétés supplémentaires. Les propriétés supplémentaires sont des paires nom=valeur séparées par de nouvelles lignes.

   * Vous pouvez configurer AEM Forms pour qu’il émette une assertion SAML pendant une période de validité correspondant à celle d’une assertion tierce. Pour respecter le délai d’expiration de l’assertion SAML tierce, ajoutez la ligne suivante dans les Propriétés personnalisées :

     `saml.sp.honour.idp.assertion.expiry=true`

   * Ajoutez la propriété personnalisée suivante pour utiliser RelayState afin de déterminer l’URL vers laquelle l’utilisateur ou l’utilisatrice sera redirigé après une authentification réussie.

     `saml.sp.use.relaystate=true`

   * Ajoutez la propriété personnalisée suivante pour pouvoir configurer l’URL du JSP (Java Server Pages) personnalisé, qui est utilisé pour effectuer le rendu de la liste enregistrée des fournisseurs d’identité. Si vous n’avez pas déployé d’application web personnalisée, la page User Management par défaut est utilisée pour effectuer le rendu de la liste.

   `saml.sp.discovery.url=/custom/custom.jsp`

1. Cliquez sur Enregistrer.
