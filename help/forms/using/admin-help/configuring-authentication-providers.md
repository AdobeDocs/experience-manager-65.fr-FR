---
title: Configuration des fournisseurs d’authentification
seo-title: Configuration des fournisseurs d’authentification
description: Ajoutez, modifiez ou supprimez des fournisseurs d’authentification, modifiez les paramètres d’authentification et découvrez l’approvisionnement juste à temps des utilisateurs.
seo-description: Ajoutez, modifiez ou supprimez des fournisseurs d’authentification, modifiez les paramètres d’authentification et découvrez l’approvisionnement juste à temps des utilisateurs.
uuid: 90e7690b-1ce0-4604-b58f-6dca4f2372cf
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 31dd8db3-ddac-429e-82f8-8c5dc4ffc186
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1595'
ht-degree: 83%

---


# Configuration des fournisseurs d’authentification {#configuring-authentication-providers}

Les domaines hybrides requièrent au moins un fournisseur d’authentification et les domaines d’entreprise requièrent au moins un fournisseur d’authentification ou un fournisseur d’annuaires.

Si vous activez la fonction SSO avec le protocole SPNEGO, ajoutez un fournisseur d’authentification Kerberos avec SPNEGO activé et un fournisseur LDAP comme solution de secours. Cette configuration permet l’authentification de l’utilisateur grâce à un ID utilisateur et un mot de passe en cas de défaillance de SPNEGO. Voir [Activation de la fonction SSO à l’aide de SPNEGO ](/help/forms/using/admin-help/enabling-single-sign-on-aem.md#enable-sso-using-spnego).

## Ajout d’un fournisseur d’authentification {#add-an-authentication-provider}

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des domaines.
1. Cliquez sur un domaine existant dans la liste. Si vous ajoutez un fournisseur d’authentification pour un nouveau domaine, voir [Ajout d’un domaine d’entreprise](/help/forms/using/admin-help/adding-domains.md#add-an-enterprise-domain) ou [Ajout d’un domaine hybride](/help/forms/using/admin-help/adding-domains.md#add-a-hybrid-domain).
1. Cliquez sur Ajouter une authentification puis, dans la liste Fournisseur d’authentification, sélectionnez un fournisseur, selon le mécanisme d’authentification utilisé par votre entreprise.
1. Fournissez toutes les autres informations requises dans la page. Voir [Paramètres d’authentification](configuring-authentication-providers.md#authentication-settings).
1. (Facultatif) Cliquez sur Tester pour tester la configuration.
1. Cliquez sur OK, puis de nouveau sur OK.

## Modification d’un fournisseur d’authentification  {#edit-an-existing-authentication-provider}

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des domaines.
1. Sélectionnez le domaine approprié dans la liste.
1. Dans la page qui apparaît, sélectionnez le fournisseur d’authentification approprié dans la liste et appliquez les modifications souhaitées. Voir [Paramètres d’authentification](configuring-authentication-providers.md#authentication-settings).
1. Cliquez sur OK.

## Suppression d’un fournisseur d’authentification  {#delete-an-authentication-provider}

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des domaines.
1. Sélectionnez le domaine approprié dans la liste.
1. Cochez la case correspondant aux fournisseurs d’authentification à supprimer, puis cliquez sur Supprimer.
1. Cliquez sur OK dans la page de confirmation qui s’affiche, puis de nouveau sur OK.

## Paramètres d’authentification {#authentication-settings}

Les paramètres suivants sont disponibles, selon le type de domaine et d’authentification choisis.

### Paramètres LDAP {#ldap-settings}

Si vous configurez une authentification pour un domaine d’entreprise ou hybride et optez pour une authentification LDAP, vous pouvez utiliser le serveur LDAP spécifié dans la configuration de l’annuaire, ou vous pouvez choisir un serveur LDAP différent à utiliser pour l’authentification. Si vous choisissez un serveur différent, les utilisateurs doivent exister sur les deux serveurs LDAP.

Pour utiliser un serveur LDAP spécifié dans la configuration de l’annuaire, sélectionnez LDAP comme fournisseur d’authentification et cliquez sur OK.

Pour utiliser un serveur LDAP différent pour l’authentification, sélectionnez LDAP comme fournisseur d’authentification puis cochez la case Authentification LDAP personnalisée. Les paramètres de configuration suivants s’affichent.

**Serveur :** (obligatoire) nom de domaine complet (FQDN) du serveur d’annuaire. Par exemple, le nom de domaine complet d’un ordinateur appelé x sur le réseau corp.exemple.com est x.corp.exemple.com. Il est possible d’utiliser une adresse IP à la place du nom de domaine complet du serveur.

**Port :** (obligatoire) port utilisé par le serveur d’annuaire. Il s’agit du port 389 ou 636 si les informations d’authentification sont envoyées via le protocole SSL sur le réseau.

**SSL:** (obligatoire) indique si le serveur d’annuaire utilise SSL lors de l’envoi de données sur le réseau. La valeur par défaut est Non. Avec la valeur Oui, le certificat du serveur LDAP correspondant doit être approuvé par l’environnement d’exécution Java™ (JRE) du serveur d’applications.

**Liaison**  (obligatoire) indique comment accéder à l’annuaire.

**Anonyme :** aucun nom d’utilisateur ou mot de passe n’est requis.

**User:** Authentication est requis. Dans le champ Nom, indiquez le nom de l’enregistrement utilisateur qui peut accéder à l’annuaire. Il est généralement conseillé d’entrer le nom distinctif complet (ND) du compte utilisateur, par exemple : cn=Jane Doe, ou=user, dc=can, dc=com. Dans le champ Mot de passe, indiquez le mot de passe associé. Ces paramètres sont obligatoires lorsque vous sélectionnez Utilisateur pour l’option Liaison.

**Récupérer les DN de base :**  (non obligatoire) Récupère les DN de base et les affiche dans la liste déroulante. Ce paramètre est utile lorsque vous avez plusieurs DN de base et que vous devez sélectionner une valeur.

**ND de base:** (obligatoire) utilisé comme point de départ pour la synchronisation des utilisateurs et des groupes à partir de la hiérarchie LDAP. Il est préférable de spécifier un DN de base au niveau inférieur de la hiérarchie, de manière à englober tous les utilisateurs et les groupes à synchroniser pour les services. N’incluez pas le ND de l’utilisateur dans ce paramètre. Pour synchroniser un utilisateur particulier, utilisez le paramètre Filtre de recherche.

**Renseignez la page avec:** (non obligatoire) lorsque cette option est sélectionnée, renseigne les attributs des pages de paramètres Utilisateur et Groupe avec les valeurs LDAP par défaut correspondantes.

**Filtre de recherche :** (obligatoire) filtre de recherche à utiliser pour trouver l’enregistrement associé à l’utilisateur. Voir Syntaxe des filtres de recherche.

### Paramètres Kerberos {#kerberos-settings}

Si vous configurez une authentification pour un domaine d’entreprise ou hybride et optez pour une authentification Kerberos, les paramètres ci-après sont disponibles.

**IP DNS :** l’adresse IP du serveur DNS qui exécute AEM forms. Sous Windows, vous pouvez déterminer cette adresse IP en exécutant ipconfig /all sur la ligne de commande.

**Hôte KDC : nom d’hôte** complet ou adresse IP du serveur Principale Directory utilisé pour l’authentification.

**Utilisateur du service :** si vous utilisez Principale Directory 2003, cette valeur correspond au mappage créé pour le principal de service dans le formulaire  `HTTP/<server name>`. Si vous utilisez Active Directory 2008, cette valeur correspond à l’ID de connexion du nom principal de service. Par exemple, supposons que le nom principal de service soit um spnego, l’ID utilisateur est spnegodemo et le mappage est HTTP/exemple.corp.votreentreprise.com. Avec Active Directory 2003, affectez à Utilisateur du service la valeur HTTP/exemple.corp.votreentreprise.com. Avec Active Directory 2008, affectez à Utilisateur du service la valeur spnegodemo. Voir Activation de la fonction SSO à l’aide de SPNEGO .

**Domaine d’administration du service :** nom de domaine pour Active Directory

**Mot de passe du service :** mot de passe de l’utilisateur du service

**Activer SPNEGO :** active l’utilisation de SPNEGO pour l’authentification unique (SSO). Voir Activation de la fonction SSO à l’aide de SPNEGO .

### Paramètres SAML {#saml-settings}

Si vous configurez une authentification pour un domaine d’entreprise ou hybride et optez pour une authentification SAML, les paramètres ci-après sont disponibles. Pour plus d’informations sur les paramètres SAML supplémentaires, voir [Configuration des paramètres du fournisseur de services SAML](/help/forms/using/admin-help/configure-saml-service-provider-settings.md#configure-saml-service-provider-settings).

**Sélectionnez un fichier de métadonnées du fournisseur d&#39;identité SAML à importer :** cliquez sur Parcourir pour sélectionner un fichier de métadonnées du fournisseur d&#39;identité SAML généré à partir de votre fournisseur d&#39;identité, puis cliquez sur Importer. Les détails relatifs au fournisseur d’identité s’affichent.

**Titre :** alias de l’URL désignée par l’ID d’entité. Le titre s’affiche également sur la page de connexion des utilisateurs d’entreprise et locaux.

**Le fournisseur d’identité prend en charge l’authentification de base du client : l’authentification de base du** client est utilisée lorsque le fournisseur d’identité utilise un profil SAML Artifact Resolution. Dans ce profil, User Management se reconnecte à un service Web s’exécutant au niveau du fournisseur d’identité afin de récupérer l’assertion SAML réelle. Le fournisseur d’identité peut demander une authentification. Si ce n’est pas le cas, sélectionnez cette option et définissez un nom d’utilisateur et un mot de passe dans les champs prévus à cet effet.

**Propriétés personnalisées :** permet de spécifier des propriétés supplémentaires. Ces propriétés sont des paires nom=valeur séparées par des nouvelles lignes.

Les propriétés personnalisées suivantes sont requises en cas d’utilisation de la liaison d’artefact.

* Ajoutez la propriété personnalisée suivante de manière à spécifier un nom d’utilisateur correspondant au fournisseur de services AEM forms, qui sera utilisé pour l’authentification auprès du service IDP Artifact Resolution.
   `saml.idp.resolve.username=<username>`

* Ajoutez la propriété personnalisée suivante afin de spécifier le mot de passe de l’utilisateur spécifié dans `saml.idp.resolve.username`.
   `saml.idp.resolve.password=<password>`

* Ajoutez la propriété personnalisée suivante de manière à autoriser le fournisseur de services à ignorer la validation du certificat lors de la connexion au service Artifact Resolution via SSL.
   `saml.idp.resolve.ignorecert=true`

### Paramètres personnalisés {#custom-settings}

Si vous configurez une authentification pour un domaine d’entreprise ou hybride et optez pour une authentification personnalisée, sélectionnez le nom du fournisseur d’authentification personnalisé.

## Approvisionnement juste à temps des utilisateurs  {#just-in-time-provisioning-of-users}

Après qu’un utilisateur est authentifié par le fournisseur d’authentification, l’approvisionnement juste à temps crée automatiquement cet utilisateur dans la base de données. Les rôles et groupes pertinents sont également affectés automatiquement à ce nouvel utilisateur. Vous pouvez activer l’approvisionnement juste à temps pour les domaines d’entreprise et hybrides.

Cette procédure décrit le fonctionnement général de l’authentification dans AEM Forms :

1. Lorsqu’un utilisateur tente de se connecter à AEM forms, le gestionnaire des utilisateurs transmet les informations d’identification de ce dernier de manière séquentielle à tous les fournisseurs d’authentification disponibles. Les informations d’identification comprennent le nom d’utilisateur et le mot de passe, le ticket Kerberos, la signature PKCS7, etc.
1. Le fournisseur d’authentification valide les informations d’identification.
1. Il vérifie ensuite si l’utilisateur existe dans la base de données User Management. L’un des états suivants s’affiche :

   **** ExistsSi l’utilisateur est en cours et déverrouillé, User Management renvoie la réussite de l’authentification. Toutefois, si l’utilisateur n’est pas en cours ou s’il est verrouillé, User Management signale un échec d’authentification.

   **N&#39;** existe pasUser Management renvoie un échec d&#39;authentification.

   **** InvalidUser Management renvoie un échec d&#39;authentification.

1. L’état indiqué par le fournisseur d’authentification est évalué. Si ce dernier a confirmé l’authentification, l’utilisateur peut alors ouvrir une session. Dans le cas contraire, User Management vérifie auprès du fournisseur d’authentification suivant. (les étapes 2 et 3)
1. Un échec d’authentification est indiqué lorsqu’aucun fournisseur d’authentification disponible n’a pu valider les informations d’identification de l’utilisateur.

Lorsque l’approvisionnement juste à temps est activé, les nouveaux utilisateurs sont créés automatiquement dans User Management si l’un des fournisseurs d’authentification valide leurs informations d’identification (après l’étape 3 de la procédure ci-dessus).

Si l’approvisionnement juste à temps n’est pas activé, lorsque l’authentification d’un utilisateur est confirmée, mais que celui-ci ne se trouve pas dans la base de données User Management, un échec d’authentification est indiqué. L’approvisionnement juste à temps ajoute une étape dans le processus d’authentification pour créer l’utilisateur et lui affecter des rôles et groupes.

### Activation de l’approvisionnement juste à temps pour un domaine  {#enable-just-in-time-provisioning-for-a-domain}

1. Ecrivez un conteneur de services qui implémente les interfaces Créateur d’identité (IdentityCreator) et Fournisseur d’affectation (AssigmentProvider). (Voir [Programmation avec AEM Forms](https://www.adobe.com/go/learn_aemforms_programming_63).)
1. Déployez le conteneur de services sur le serveur Forms.
1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des domaines.

   Sélectionnez un domaine existant ou cliquez sur Nouveau domaine d’entreprise.

1. Pour créer un domaine, cliquez sur Nouveau domaine d’entreprise ou sur Nouveau domaine hybride. Pour modifier un domaine existant, cliquez sur le nom du domaine en question.
1. Sélectionnez Activer l’approvisionnement juste à temps.

   ***Remarque ** : si la case à cocher correspondant à Activer l’approvisionnement juste à temps n’apparaît pas, cliquez sur Accueil > Paramètres > User Management > Configuration > Attributs système avancés, puis sur Recharger.*

1. Ajoutez des fournisseurs d’authentification Lorsque vous ajoutez des fournisseurs d’authentification, dans l’écran Nouvelle authentification, sélectionnez un créateur d’identité et un fournisseur d’affectation répertorié. Voir [Configuration des fournisseurs d’authentification](configuring-authentication-providers.md#configuring-authentication-providers).
1. Enregistrez le domaine.

