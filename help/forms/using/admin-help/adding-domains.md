---
title: Ajout de domaines
seo-title: Ajout de domaines
description: Découvrez comment ajouter un domaine d’entreprise, local ou hybride à l’aide des paramètres et des remarques générales de Gestion des domaines concernant les noms et les ID de domaine.
seo-description: Découvrez comment ajouter un domaine d’entreprise, local ou hybride à l’aide des paramètres et des remarques générales de Gestion des domaines concernant les noms et les ID de domaine.
uuid: 3ae1e5d4-ea5b-4e0b-be97-3957c3702d5f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d4004ffe-c981-487d-b803-dc4492ae5998
exl-id: c708936d-7aa7-4b92-be2d-d97008f187d2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '946'
ht-degree: 99%

---

# Ajout de domaines {#adding-domains}

## Ajout d’un domaine d’entreprise {#add-an-enterprise-domain}

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des domaines.
1. Cliquez sur Nouveau domaine d’entreprise.
1. Dans la zone ID, saisissez un identifiant unique pour le domaine et dans la zone Nom, saisissez un nom descriptif pour le domaine. Voir [Remarques importantes concernant les noms et les ID de domaine](adding-domains.md#important-considerations-for-domain-names-and-ids).
1. Spécifiez s’il convient ou non d’activer le verrouillage des comptes. Voir [Configuration des paramètres de verrouillage des comptes ](/help/forms/using/admin-help/configure-account-locking-settings.md#configure-account-locking-settings). Par défaut, l’option Activer le verrouillage de compte est sélectionnée.
1. Cliquez sur Ajouter une authentification puis, dans la liste Fournisseur d’authentification, sélectionnez un fournisseur, selon le mécanisme d’authentification utilisé par votre entreprise. Les valeurs possibles sont LDAP, Kerberos, SAML ou un fournisseur d’authentification personnalisé.

   Si vous sélectionnez LDAP, vous pouvez utiliser le serveur LDAP spécifié dans la configuration de l’annuaire, ou vous pouvez choisir un serveur LDAP différent à utiliser pour l’authentification. Si vous choisissez un serveur différent, les utilisateurs doivent exister sur les deux serveurs LDAP.

1. Fournissez toutes les autres informations requises dans la page. Voir [Paramètres d’authentification](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings).
1. Ajoutez un annuaire ou une interface SPI (Service Provider Interface) personnalisée. Voir [Ajout d’annuaires ou d’interfaces SPI personnalisées](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis).
1. Cliquez sur Terminer, puis sur OK.

Après avoir créé un domaine d’entreprise, synchronisez manuellement l’annuaire ou créez un déclencheur à cet effet pour que User Management puisse l’utiliser. Vous pouvez ensuite configurer un calendrier de synchronisation des annuaires et effectuer une synchronisation manuelle, si nécessaire. Voir [Synchronisation des annuaires](/help/forms/using/admin-help/synchronizing-directories.md#synchronizing-directories).

## Ajout d’un domaine local {#add-a-local-domain}

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des domaines.
1. Cliquez sur Nouveau domaine local.
1. Dans la zone ID, saisissez un identifiant unique pour le domaine et, dans la zone Nom, saisissez un nom descriptif pour le domaine. Voir [Remarques importantes concernant les noms et les ID de domaine](adding-domains.md#important-considerations-for-domain-names-and-ids).
1. Spécifiez s’il convient d’activer le verrouillage des comptes, puis cliquez sur OK. Voir [Configuration des paramètres de verrouillage des comptes](/help/forms/using/admin-help/configure-account-locking-settings.md#configure-account-locking-settings). Par défaut, l’option Activer le verrouillage de compte est sélectionnée.

## Ajout d’un domaine hybride  {#add-a-hybrid-domain}

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des domaines.
1. Cliquez sur Nouveau domaine hybride.
1. Dans la zone ID, saisissez un identifiant unique pour le domaine et, dans la zone Nom, saisissez un nom descriptif pour le domaine. Voir [Remarques importantes concernant les noms et les ID de domaine](adding-domains.md#important-considerations-for-domain-names-and-ids).
1. Cliquez sur Ajouter une authentification puis, dans la liste Fournisseur d’authentification, sélectionnez un fournisseur, selon le mécanisme d’authentification utilisé par votre entreprise. Les valeurs possibles sont LDAP, Kerberos, SAML ou un fournisseur d’authentification personnalisé.
1. Fournissez toutes les autres informations requises dans la page. Voir [Paramètres d’authentification](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings).
1. Cliquez sur OK, puis de nouveau sur OK.

## Remarques importantes concernant les noms et les ID de domaine  {#important-considerations-for-domain-names-and-ids}

Gardez à l’esprit les points suivants lors du choix d’un nom et d’un ID de domaine :

### Remarques générales {#general-considerations}

* Lors de l’utilisation de fournisseurs de base de données autres que DB2, l’ID de domaine peut atteindre 50 octets. Si vous utilisez des caractères ASCII sur un octet, la limite est de 50 caractères. Si ce dernier contient des caractères multi-octets, cette limite est réduite. Par exemple, si vous créez un domaine dont l’identificateur contient des caractères sur trois octets, la limite est réduite à 16 caractères. De plus, il n’est pas possible de créer des domaines comportant des caractères sur quatre octets. Si vous créez un ID de domaine dépassant cette limite, AEM forms devient instable. Pour annuler les effets de cette instabilité, voir [Suppression d’un domaine contenant des caractères étendus ou multi-octet](adding-domains.md#remove-a-domain-that-contains-extended-or-multi-byte-characters) sur cette page.
* Le nombre de domaines, locaux ou d’entreprise, pouvant être créés dans AEM forms dépend de la longueur de chacun des ID de domaine. Lors de l’ajout d’un domaine d’entreprise ou hybride, le gestionnaire des utilisateurs met à jour la chaîne configInstance du nœud AuthProviders du fichier de configuration (config.xml) d&#39;AEM forms. La chaîne configInstance contient une liste des chemins d’accès absolus de tous les domaines associés au fournisseur d’autorisations, séparés par des deux-points. La limite de taille de cette chaîne est de 8 192 caractères. Lorsque cette limite est atteinte, vous ne pouvez pas créer de domaine supplémentaire.

### Remarques aux utilisateurs de DB2  {#considerations-when-using-db2}

Lorsque vous utilisez DB2 pour la base de données AEM forms, la longueur maximale d’ID de domaine autorisée dépend des types de caractères utilisés :

* 100 sur un octet (ASCII) (par exemple, les caractères utilisés en anglais, français ou allemand)
* 50 sur deux octets (par exemple, les caractères utilisés en chinois, japonais ou coréen)
* 25 sur quatre octets (par exemple, les caractères utilisés en chinois traditionnel)

### Remarques aux utilisateurs de MySQL  {#considerations-when-using-mysql}

Lors de l’utilisation de MySQL comme base de données AEM forms, les restrictions suivantes s’appliquent :

* N’utilisez que des caractères ASCII (sur un octet) dans l’ID de domaine et le nom de domaine. Si vous utilisez des caractères ASCII étendus, AEM forms devient instable et renvoie parfois une exception lorsque vous tentez de supprimer le domaine. Pour annuler les effets de cette instabilité, voir la section [Suppression d’un domaine contenant des caractères étendus ou multi-octet](adding-domains.md#remove-a-domain-that-contains-extended-or-multi-byte-characters) sur cette page.
* Vous ne pouvez pas créer deux domaines portant le même nom, même si la casse est différente. Par exemple, si vous essayez de créer un domaine nommé *Adobe* alors qu’un domaine nommé *adobe* existe déjà, une erreur se produit.
* User Management n’est pas en mesure de différencier les noms de deux domaines qui ne diffèrent que par l’utilisation de caractères étendus. Par exemple, si vous créez un domaine appelé *abcde* et un autre appelé *âbcdè*, ils sont considérés comme identiques.

### Suppression d’un domaine contenant des caractères étendus ou multi-octet.{#remove-a-domain-that-contains-extended-or-multi-byte-characters}

1. Exportez le fichier de configuration, comme indiqué dans la section [Importation et exportation du fichier de configuration](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).
1. Ouvrez le fichier de configuration et sous le nœud Domains, recherchez le nœud dont l’attribut de nom correspond au nom de domaine créé avec des caractères étendus ou multi-octet. Supprimez la totalité du nœud associé à ce domaine.
1. Dans la base de données, recherchez le domaine dans la table edcprincipaldomainentity :

   * Sélectionnez `*` dans edcprincipaldomainentity.
   * Recherchez le nom de domaine contenant des caractères étendus ou multi-octet et définissez son statut sur OBSOLETE.

1. Importez le fichier de configuration mis à jour, comme indiqué dans la section [Importation et exportation du fichier de configuration](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).
