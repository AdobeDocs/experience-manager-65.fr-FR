---
title: Ajouter des domaines
description: Découvrez comment ajouter un domaine d’entreprise, local ou hybride à l’aide des paramètres de gestion des domaines et des considérations générales pour les noms et les identifiants de domaine.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: c708936d-7aa7-4b92-be2d-d97008f187d2
source-git-commit: 3885cc51f7e821cdb352737336a29f9c4f0c2f41
workflow-type: tm+mt
source-wordcount: '922'
ht-degree: 14%

---

# Ajouter des domaines {#adding-domains}

## Ajout d’un domaine d’entreprise {#add-an-enterprise-domain}

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des domaines.
1. Cliquez sur Nouveau domaine d’entreprise.
1. Dans la zone ID, saisissez un identifiant unique pour le domaine et dans la zone Nom, saisissez un nom descriptif pour le domaine. (Voir [Remarques importantes concernant les noms et les ID de domaine](adding-domains.md#important-considerations-for-domain-names-and-ids).)
1. Indiquez si le verrouillage des comptes doit être activé. Voir [Configuration des paramètres de verrouillage des comptes](/help/forms/using/admin-help/configure-account-locking-settings.md#configure-account-locking-settings). Par défaut, l’option Activer le verrouillage de compte est sélectionnée.
1. Cliquez sur Ajouter une authentification et, dans la liste Fournisseur d’authentification , sélectionnez un fournisseur, en fonction du mécanisme d’authentification utilisé par votre organisation. Les valeurs possibles sont LDAP, Kerberos, SAML ou un fournisseur d’authentification personnalisé.

   Si vous sélectionnez LDAP, vous pouvez utiliser le serveur LDAP spécifié dans la configuration de votre annuaire ou vous pouvez choisir un autre serveur LDAP à utiliser pour l’authentification. Si vous choisissez un autre serveur, vos utilisateurs doivent exister sur les deux serveurs LDAP.

1. Fournissez toutes les informations supplémentaires requises sur la page. (Voir [Paramètres d’authentification](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings).)
1. Ajoutez un répertoire ou une interface SPI (Service Provider Interface) personnalisée. (Voir [Ajout d’annuaires ou d’interfaces SPI personnalisées](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis).)
1. Cliquez sur Terminer, puis sur OK.

Après avoir créé un domaine d’entreprise, synchronisez manuellement l’annuaire ou créez un déclencheur pour effectuer une synchronisation avant que User Management puisse l’utiliser. Vous pouvez ensuite configurer un planning de synchronisation des annuaires et effectuer une synchronisation manuelle, si nécessaire. (Voir [Synchronisation des annuaires](/help/forms/using/admin-help/synchronizing-directories.md#synchronizing-directories).)

## Ajout d’un domaine local {#add-a-local-domain}

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des domaines.
1. Cliquez sur Nouveau domaine local.
1. Dans la zone ID, saisissez un identifiant unique pour le domaine et, dans la zone Nom, saisissez un nom descriptif pour le domaine. (Voir [Remarques importantes concernant les noms et les ID de domaine](adding-domains.md#important-considerations-for-domain-names-and-ids).)
1. Indiquez s’il faut activer le verrouillage des comptes, puis cliquez sur OK. Voir [Configuration des paramètres de verrouillage des comptes](/help/forms/using/admin-help/configure-account-locking-settings.md#configure-account-locking-settings). Par défaut, l’option Activer le verrouillage de compte est sélectionnée.

## Ajout d’un domaine hybride {#add-a-hybrid-domain}

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des domaines.
1. Cliquez sur Nouveau domaine hybride.
1. Dans la zone ID, saisissez un identifiant unique pour le domaine et, dans la zone Nom, saisissez un nom descriptif pour le domaine. (Voir [Remarques importantes concernant les noms et les ID de domaine](adding-domains.md#important-considerations-for-domain-names-and-ids).)
1. Cliquez sur Ajouter une authentification et, dans la liste Fournisseur d’authentification , sélectionnez un fournisseur, en fonction du mécanisme d’authentification utilisé par votre organisation. Les valeurs possibles sont LDAP, Kerberos, SAML ou un fournisseur d’authentification personnalisé.
1. Fournissez toutes les informations supplémentaires requises sur la page. (Voir [Paramètres d’authentification](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings).)
1. Cliquez sur OK, puis de nouveau sur OK.

## Remarques importantes concernant les noms et les ID de domaine {#important-considerations-for-domain-names-and-ids}

Tenez compte des points suivants lors du choix d’un nom et d’un identifiant de domaine :

### Remarques générales {#general-considerations}

* Lorsque vous utilisez un fournisseur de base de données autre que DB2, l’ID de domaine peut contenir jusqu’à 50 octets. Si vous utilisez des caractères ASCII sur un octet, la limite est de 50 caractères. Si l’identifiant de domaine contient des caractères à plusieurs octets, cette limite est réduite. Par exemple, si vous créez un domaine dont l’identifiant contient des caractères à 3 octets, la limite est de 16 caractères. En outre, vous ne pouvez pas créer de domaines contenant des caractères à 4 octets. Si vous créez un ID de domaine dépassant cette limite, AEM forms se trouve dans un état instable. Pour annuler les effets de cette instabilité, voir [Suppression d’un domaine contenant des caractères étendus ou multi-octet](adding-domains.md#remove-a-domain-that-contains-extended-or-multi-byte-characters) sur cette page.
* Le nombre de domaines d’entreprise et de domaines locaux pouvant être créés dans AEM forms dépend de la longueur de chacun des ID de domaine. Lors de l’ajout d’un domaine d’entreprise ou hybride, le gestionnaire des utilisateurs met à jour la chaîne configInstance du nœud AuthProviders du fichier de configuration (config.xml) d’AEM forms. La chaîne configInstance contient une liste des chemins absolus de tous les domaines associés au fournisseur d’autorisations, séparés par des deux-points. La taille de cette chaîne est limitée à 8 192 caractères. Lorsque cette limite est atteinte, vous ne pouvez pas créer de domaines supplémentaires.

### Remarques concernant l’utilisation de DB2 {#considerations-when-using-db2}

Lors de l’utilisation de DB2 pour la base de données d’AEM forms, la longueur maximale autorisée pour l’ID de domaine dépend du type de caractères utilisé :

* 100 sur un octet (ASCII) (par exemple, les caractères utilisés en anglais, français ou allemand)
* 50 sur deux octets (par exemple, les caractères utilisés en chinois, japonais ou coréen)
* 25 sur quatre octets (par exemple, les caractères utilisés en chinois traditionnel)

### Remarques concernant l’utilisation de MySQL {#considerations-when-using-mysql}

Lors de l’utilisation de MySQL comme base de données d’AEM forms, les restrictions suivantes s’appliquent :

* Utilisez uniquement des caractères ASCII (sur un octet) pour l’ID de domaine et le nom de domaine. Si vous utilisez des caractères ASCII étendus, AEM forms se trouve dans un état instable et peut générer une exception si vous tentez de supprimer le domaine. Pour annuler les effets de cette instabilité, voir la section [Suppression d’un domaine contenant des caractères étendus ou multi-octet](adding-domains.md#remove-a-domain-that-contains-extended-or-multi-byte-characters) sur cette page.
* Vous ne pouvez pas créer deux domaines portant le même nom, mais dont la casse diffère. Par exemple, en tentant de créer un domaine nommé *Adobe* lorsqu’un domaine nommé *adobe* existe déjà entraîne une erreur.
* User Management ne peut pas différencier deux noms de domaine qui ne diffèrent que par l’utilisation de caractères étendus. Par exemple, si vous créez un domaine appelé *abcde* et un autre appelé *âbcdè*, ils sont considérés comme identiques.

### Suppression d’un domaine contenant des caractères étendus ou multi-octets {#remove-a-domain-that-contains-extended-or-multi-byte-characters}

1. Exportez le fichier de configuration, comme décrit dans la section [Import et export du fichier de configuration](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).
1. Ouvrez le fichier de configuration et, sous le noeud Domains , recherchez le noeud dont l’attribut name correspond au nom du domaine créé avec des caractères étendus ou multi-octets. Supprimez le noeud entier associé à ce domaine.
1. Dans votre base de données, recherchez le domaine dans la table edcprincipaldomainentity :

   * Sélectionnez `*` dans edcprincipaldomainentity.
   * Recherchez le nom de domaine contenant des caractères étendus ou multi-octets et définissez son statut sur OBSOLETE.

1. Importez le fichier de configuration mis à jour, comme décrit dans la section [Import et export du fichier de configuration](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).
