---
title: Configurer les fournisseurs d’authentification
description: Ajoutez, modifiez ou supprimez des fournisseurs d’authentification, modifiez les paramètres d’authentification et découvrez l’approvisionnement juste à temps des utilisateurs.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: d72a3977-1423-49e0-899b-234bb76be378
source-git-commit: f349c8fd9c370ba589d217cd3b1d0521ae5c5597
workflow-type: tm+mt
source-wordcount: '1580'
ht-degree: 44%

---

# Configurer les fournisseurs d’authentification {#configuring-authentication-providers}

Les domaines hybrides requièrent au moins un fournisseur d’authentification et les domaines d’entreprise requièrent au moins un fournisseur d’authentification ou un fournisseur d’annuaires.

Si vous activez la fonction SSO à l’aide de SPNEGO, ajoutez un fournisseur d’authentification Kerberos avec SPNEGO activé et un fournisseur LDAP comme solution de sauvegarde. Cette configuration permet l’authentification de l’utilisateur avec un identifiant et un mot de passe utilisateur si SPNEGO ne fonctionne pas. Voir [Activation de la fonction SSO à l’aide de SPNEGO](/help/forms/using/admin-help/enabling-single-sign-on-aem.md#enable-sso-using-spnego).

## Ajout d’un fournisseur d’authentification {#add-an-authentication-provider}

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des domaines.
1. Cliquez sur un domaine existant dans la liste. Si vous ajoutez une authentification pour un nouveau domaine, voir [Ajout d’un domaine d’entreprise](/help/forms/using/admin-help/adding-domains.md#add-an-enterprise-domain) ou [Ajout d’un domaine hybride](/help/forms/using/admin-help/adding-domains.md#add-a-hybrid-domain).
1. Cliquez sur Ajouter une authentification et, dans la liste Fournisseur d’authentification , sélectionnez un fournisseur, en fonction du mécanisme d’authentification utilisé par votre organisation.
1. Fournissez toutes les autres informations requises dans la page. (Voir [Paramètres d’authentification](configuring-authentication-providers.md#authentication-settings).)
1. (Facultatif) Cliquez sur Tester pour tester la configuration.
1. Cliquez sur OK, puis de nouveau sur OK.

## Modifier un fournisseur d’authentification existant {#edit-an-existing-authentication-provider}

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des domaines.
1. Cliquez sur le domaine approprié dans la liste.
1. Sur la page qui s’affiche, sélectionnez le fournisseur d’authentification approprié dans la liste et apportez les modifications nécessaires. (Voir [Paramètres d’authentification](configuring-authentication-providers.md#authentication-settings)).
1. Cliquez sur OK.

## Suppression d’un fournisseur d’authentification {#delete-an-authentication-provider}

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des domaines.
1. Cliquez sur le domaine approprié dans la liste.
1. Cochez les cases correspondant aux fournisseurs d’authentification à supprimer, puis cliquez sur Supprimer.
1. Cliquez sur OK dans la page de confirmation qui s’affiche, puis de nouveau sur OK.

## Paramètres d’authentification {#authentication-settings}

Les paramètres suivants sont disponibles, selon le type de domaine et d’authentification que vous avez choisi.

### Paramètres LDAP {#ldap-settings}

Si vous configurez l&#39;authentification pour un domaine d&#39;entreprise ou hybride et sélectionnez l&#39;authentification LDAP, vous pouvez choisir d&#39;utiliser le serveur LDAP spécifié dans la configuration de l&#39;annuaire ou choisir un autre serveur LDAP à utiliser pour l&#39;authentification. Si vous choisissez un serveur différent, les utilisateurs doivent exister sur les deux serveurs LDAP.

Pour utiliser le serveur LDAP spécifié dans la configuration de votre annuaire, sélectionnez LDAP comme fournisseur d&#39;authentification et cliquez sur OK.

Pour utiliser un autre serveur LDAP pour effectuer l’authentification, sélectionnez LDAP comme fournisseur d’authentification, puis cochez la case Authentification LDAP personnalisée . Les paramètres de configuration suivants s’affichent.

**Serveur :** (obligatoire) nom de domaine complet (FQDN) du serveur de répertoire. Par exemple, le nom de domaine complet d’un ordinateur appelé x sur le réseau corp.exemple.com est x.corp.exemple.com. Il est possible d’utiliser une adresse IP à la place du nom de domaine complet du serveur.

**Port :** (obligatoire) port utilisé par le serveur de répertoire. Il s’agit du port 389 ou 636 si les informations d’authentification sont envoyées via le protocole SSL sur le réseau.

**SSL :** (obligatoire) indique si le serveur de répertoire utilise le protocole SSL pour envoyer les données sur le réseau. La valeur par défaut est Non. Lorsque la valeur est définie sur Oui, le certificat du serveur LDAP correspondant doit être approuvé par l’environnement d’exécution Java™ (JRE) du serveur d’applications.

**Binding :** (obligatoire) indique le mode d’accès au répertoire.

**Anonyme :** aucun nom d’utilisateur ni mot de passe requis.

**Utilisateur :** authentification requise. Dans le champ Nom, indiquez le nom de l’enregistrement utilisateur qui peut accéder à l’annuaire. Il est généralement conseillé d’entrer le nom distinctif complet (ND) du compte d’utilisateur, par exemple : cn=Jane Doe, ou=user, dc=can, dc=com. Dans la zone Mot de passe, indiquez le mot de passe associé. Ces paramètres sont requis lorsque vous sélectionnez Utilisateur comme option de liaison.

**Récupérer les noms uniques de base :** (facultatif) permet de récupérer les noms uniques de base et de les afficher dans la liste déroulante. Ce paramètre est utile lorsque vous avez plusieurs DN de base et que vous devez sélectionner une valeur.

**Nom unique de base :** (obligatoire) sert de point de départ pour la synchronisation des utilisateurs et des groupes à partir de la hiérarchie LDAP. Il est préférable de spécifier un DN de base au niveau le plus bas de la hiérarchie qui englobe tous les utilisateurs et groupes devant être synchronisés pour les services. N’incluez pas le ND de l’utilisateur dans ce paramètre. Pour synchroniser un utilisateur spécifique, utilisez le paramètre Filtre de recherche .

**Remplir la page avec :** (facultatif) lorsque cette option est sélectionnée, les attributs des pages contenant les paramètres Utilisateur et Groupe sont renseignés avec les valeurs LDAP par défaut correspondantes.

**Filtre de recherche :** (obligatoire) filtre de recherche à utiliser pour trouver l’enregistrement associé à l’utilisateur. Voir Syntaxe des filtres de recherche.

### Paramètres Kerberos {#kerberos-settings}

Si vous configurez l’authentification pour un domaine d’entreprise ou hybride et sélectionnez l’authentification Kerberos, les paramètres suivants sont disponibles.

**IP DNS :** l’adresse IP du serveur DNS qui exécute AEM forms. Sous Windows, vous pouvez déterminer cette adresse IP en exécutant ipconfig /all sur la ligne de commande.

**Hôte KDC :** nom d’hôte complet ou adresse IP du serveur Active Directory utilisé pour l’authentification.

**Utilisateur du service :** si vous utilisez Active Directory 2003, cette valeur correspond au mappage créé pour le nom principal de service, au format `HTTP/<server name>`. Si vous utilisez Active Directory 2008, cette valeur correspond à l’ID de connexion du nom principal de service. Par exemple, supposons que le nom principal de service soit um spnego, l’identifiant utilisateur est spnegodemo et le mappage est HTTP/exemple.votreentreprise.com. Avec Active Directory 2003, définissez l’Utilisateur du service sur HTTP/exemple.votreentreprise.com. Avec Active Directory 2008, affectez à Utilisateur du service la valeur spnegodemo. Voir Activation de la fonction SSO à l’aide de SPNEGO.

**Domaine d’administration du service :** nom de domaine pour Active Directory

**Mot de passe du service :** mot de passe de l’utilisateur du service

**Activer SPNEGO :** active l’utilisation de SPNEGO pour l’authentification unique (SSO). Voir Activation de la fonction SSO à l’aide de SPNEGO.

### Paramètres SAML {#saml-settings}

Si vous configurez l’authentification pour un domaine d’entreprise ou hybride et sélectionnez l’authentification SAML, les paramètres suivants sont disponibles. Pour plus d’informations sur les paramètres SAML supplémentaires, voir [Configuration des paramètres du fournisseur de services SAML](/help/forms/using/admin-help/configure-saml-service-provider-settings.md#configure-saml-service-provider-settings).

**Sélectionnez un fichier de métadonnées de fournisseur d’identité SAML
à importer :** cliquez sur Parcourir pour sélectionner un fichier de métadonnées de fournisseur d’identité SAML généré à partir du fournisseur d’identité, puis cliquez sur Importer. Les détails relatifs au fournisseur d’identité s’affichent.

**Titre :** alias de l’URL repéré par l’identifiant d’entité. Le titre s’affiche également sur la page de connexion des utilisateurs d’entreprise et locaux.

**Le fournisseur d’identité prend en charge l’authentification de base du client :** l’authentification de base du client est utilisée lorsque le fournisseur d’identité utilise un profil de résolution d’artefacts SAML. Dans ce profil, User Management se connecte à nouveau à un service Web s’exécutant au niveau du fournisseur d’identité pour récupérer l’assertion SAML réelle. Le fournisseur d’identité peut nécessiter une authentification. Si le fournisseur d’identité ne requiert pas d’authentification, sélectionnez cette option et indiquez un nom d’utilisateur et un mot de passe dans les zones fournies.

**Propriétés personnalisées :** permet de spécifier des propriétés supplémentaires. Les propriétés supplémentaires sont des paires nom=valeur séparées par de nouvelles lignes.

Les propriétés personnalisées suivantes sont requises si la liaison d’artefact est utilisée.

* Ajoutez la propriété personnalisée suivante pour spécifier un nom d’utilisateur qui représente le fournisseur de services AEM forms, qui est utilisé pour s’authentifier auprès du service IDP Artifact Resolution.
  `saml.idp.resolve.username=<username>`

* Ajoutez la propriété personnalisée suivante afin de spécifier le mot de passe de l’utilisateur spécifié dans `saml.idp.resolve.username`.
  `saml.idp.resolve.password=<password>`

* Ajoutez la propriété personnalisée suivante de manière à autoriser le fournisseur de services à ignorer la validation du certificat lors de la connexion au service Artifact Resolution via SSL.
  `saml.idp.resolve.ignorecert=true`

### Paramètres personnalisés {#custom-settings}

Si vous configurez l’authentification pour un domaine d’entreprise ou hybride et sélectionnez Authentification personnalisée, sélectionnez le nom du fournisseur d’authentification personnalisé.

## Approvisionnement juste à temps des utilisateurs {#just-in-time-provisioning-of-users}

La mise en service juste à temps crée automatiquement un utilisateur dans la base de données User Management une fois qu’il a été authentifié par le biais d’un fournisseur d’authentification. Les rôles et groupes pertinents sont également affectés dynamiquement au nouvel utilisateur. Vous pouvez activer l’approvisionnement juste à temps pour les domaines d’entreprise et hybrides.

Cette procédure décrit le fonctionnement général de l’authentification dans AEM Forms :

1. Lorsqu’un utilisateur tente de se connecter à AEM forms, User Management transmet ses informations d’identification de manière séquentielle à tous les fournisseurs d’authentification disponibles. (Les informations d’identification comprennent la combinaison nom d’utilisateur/mot de passe, ticket Kerberos, signature PKCS7, etc.)
1. Le fournisseur d’authentification valide les identifiants.
1. Le fournisseur d’authentification vérifie ensuite si l’utilisateur existe dans la base de données User Management. Les états possibles sont les suivants :

   **Existe :** si l’utilisateur est en cours et déverrouillé, User Management confirme son authentification. Toutefois, si l’utilisateur n’est pas en cours ou s’il est verrouillé, User Management signale un échec d’authentification.

   **N’existe pas :** User Management renvoie l’échec d’authentification.

   **Invalide :** User Management signale un échec d’authentification.

1. Le résultat renvoyé par le fournisseur d’authentification est évalué. Si le fournisseur d’authentification a renvoyé une authentification réussie, l’utilisateur est autorisé à se connecter. Sinon, User Management vérifie auprès du fournisseur d’authentification suivant (étapes 2 à 3).
1. L’échec de l’authentification est renvoyé si aucun fournisseur d’authentification disponible ne valide les informations d’identification de l’utilisateur.

Lorsque l’approvisionnement juste à temps est activé, les nouveaux utilisateurs sont créés dynamiquement dans User Management si l’un des fournisseurs d’authentification valide leurs informations d’identification. (Après l’étape 3 de la procédure ci-dessus.)

Sans approvisionnement juste à temps, lorsqu’un utilisateur est authentifié avec succès mais qu’il est introuvable dans la base de données User Management, l’authentification échoue. La mise en service juste à temps ajoute une étape dans la procédure d’authentification pour créer l’utilisateur et lui affecter des rôles et des groupes.

### Activation de l’approvisionnement juste à temps pour un domaine {#enable-just-in-time-provisioning-for-a-domain}

1. Ecrivez un conteneur de services qui implémente les interfaces Créateur d’identité (IdentityCreator) et Fournisseur d’affectation (AssignmentProvider). (Voir [Programmation avec AEM Forms](https://www.adobe.com/go/learn_aemforms_programming_63_fr).)
1. Déployez le conteneur de services sur le serveur Forms.
1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des domaines.

   Sélectionnez un domaine existant ou cliquez sur Nouveau domaine d’entreprise.

1. Pour créer un domaine, cliquez sur Nouveau domaine d’entreprise ou Nouveau domaine hybride. Pour modifier un domaine existant, cliquez sur son nom.
1. Sélectionnez Activer l’approvisionnement juste à temps.

   ***Remarque ** : si la case à cocher correspondant à Activer l’approvisionnement juste à temps n’apparaît pas, cliquez sur Accueil > Paramètres > User Management > Configuration > Attributs système avancés, puis sur Recharger.*

1. Ajoutez des fournisseurs d’authentification. Lors de l’ajout de fournisseurs d’authentification, dans l’écran Nouvelle authentification, sélectionnez un créateur d’identités et un fournisseur d’affectation enregistrés. (Voir [Configuration des fournisseurs d’authentification](configuring-authentication-providers.md#configuring-authentication-providers).)
1. Enregistrez le domaine.
