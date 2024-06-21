---
title: Configuration des annuaires
description: Découvrez comment ajouter, modifier et supprimer des annuaires et comment configurer la gestion des utilisateurs et des utilisatrices afin d’utiliser la vue de liste virtuelle.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 30edcef2-e8fa-403a-9850-b8dfeeb9ac65
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '3229'
ht-degree: 100%

---

# Configuration des annuaires {#configuring-directories}

Pour chaque domaine d’entreprise que vous configurez, indiquez les annuaires que le fournisseur d’authentification interroge pour obtenir les informations utilisateur. Il est possible de configurer plusieurs annuaires par domaine.

## Ajout d’annuaires ou d’interfaces SPI personnalisées {#adding-directories-or-custom-spis}

Pour chaque domaine d’entreprise que vous configurez, indiquez les annuaires que le fournisseur d’authentification interroge pour obtenir les informations utilisateur. Vous pouvez ajouter un annuaire à un domaine d’entreprise existant ou à un nouveau domaine d’entreprise que vous ajoutez. Il est possible de configurer plusieurs annuaires par domaine. Vous pouvez également configurer un domaine afin qu’il utilise une interface SPI personnalisée pour la synchronisation.

### Ajout d’un annuaire {#add-a-directory}

1. Dans la console dʼadministration, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des domaines.
1. Cliquez sur Nouveau domaine d’entreprise ou sélectionnez un domaine d’entreprise existant.
1. Cliquez sur Ajouter un annuaire.
1. Dans la zone Nom du profil, saisissez un nom permettant de distinguer cet annuaire, puis cliquez sur Suivant.
1. Configurez les paramètres du serveur d’annuaire. (Voir [Paramètres d’annuaire](configuring-directories.md#directory-settings).)
1. Cliquez sur Tester pour vérifier qu’il est possible d’établir une connexion avec le serveur LDAP. Si le test échoue, consultez l’exception dans le fichier journal du serveur d’applications pour déterminer la cause initiale de l’échec. Cliquez sur Fermer, puis sur Suivant.
1. Sélectionnez Paramètres utilisateur et configurez les paramètres selon les besoins. (Voir [Paramètres d’annuaire](configuring-directories.md#directory-settings).)
1. Pour vérifier que le nom distinctif de base et les autres attributs configurés collectent le lot correct d’utilisateurs et d’utilisatrices, cliquez sur Tester. LDAP tente de récupérer les 200 premiers enregistrements à l’aide des paramètres fournis (nom distinctif de base, filtre de recherche et tous les attributs).

   Si des utilisateurs et utilisatrices sont renvoyés, les résultats affichent les valeurs affectées à chaque champ conformément au jeu d’attributs. Si le test échoue en raison d’un nom de serveur non existant, d’informations d’identification erronées ou d’attributs incorrects, le message d’erreur suivant apparaît : « Les critères de recherche spécifiés ne renvoient aucun résultat. ». Pour déterminer la cause initiale de l’échec, consultez l’exception dans le fichier journal du serveur d’applications. Cliquez sur Fermer, puis sur Suivant.

1. Sélectionnez Paramètres de groupe et procédez à la configuration requise. (Voir [Paramètres d’annuaire](configuring-directories.md#directory-settings).)
1. Cliquez sur Tester pour vérifier que le nom distinctif de base et que les autres attributs configurés collectent le lot de groupes correct. Si des groupes sont renvoyés, les résultats affichent les valeurs affectées à chaque champ conformément au jeu d’attributs. Cliquez sur Fermer.

### Ajout d’une interface SPI personnalisée {#add-a-custom-spi}

Pour plus d’informations sur la création d’une interface SPI personnalisée, consultez la section « Développement d’interfaces SPI pour AEM Forms » dans [Programmation avec AEM Forms](https://www.adobe.com/go/learn_aemforms_programming_63_fr). Pour rendre une interface SPI personnalisée déployée récemment disponible pour une association au domaine, redémarrez le serveur.

1. Dans la console dʼadministration, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des domaines.
1. Cliquez sur Nouveau domaine d’entreprise ou sélectionnez un domaine d’entreprise existant.
1. Cliquez sur Ajouter un annuaire.
1. Saisissez un nom dans la zone Nom du profil, sélectionnez Fournisseur SPI personnalisé, puis cliquez sur Suivant.
1. Sélectionnez un fournisseur d’utilisateurs et d’utilisatrices personnalisé dans la liste et cliquez sur Suivant.
1. Sélectionnez un fournisseur de groupes personnalisé dans la liste et cliquez sur Terminer.

## Modification d’un annuaire {#edit-a-directory}

Vous pouvez modifier les détails d’un annuaire que vous avez précédemment configuré.

1. Dans la console dʼadministration, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des domaines.
1. Cliquez sur le domaine approprié dans la liste, puis, dans la page qui apparaît, sélectionnez l’annuaire approprié dans la liste.
1. Configurez les paramètres relatifs à l’annuaire, à l’utilisateur ou à l’utilisatrice et au groupe selon les besoins. (Voir [Paramètres d’annuaire](configuring-directories.md#directory-settings).)
1. Cliquez sur OK.

## Suppression d’un annuaire {#delete-a-directory}

Lorsque vous synchronisez vos domaines après la suppression d’un annuaire, l’ensemble des utilisateurs, des utilisatrices et des groupes de cet annuaire sont marqués comme obsolètes dans la base de données. Ils ne sont renvoyés dans aucune recherche effectuée à partir d’Administration Console.

>[!NOTE]
>
>Les domaines d’entreprise requièrent au moins un fournisseur d’authentification et un fournisseur d’annuaires.

1. Dans la console dʼadministration, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des domaines.
1. Cliquez sur le domaine approprié dans la liste.
1. Cochez la case correspondant à l’annuaire approprié, puis cliquez sur Supprimer.
1. Cliquez sur OK dans la page de confirmation qui s’affiche, puis de nouveau sur OK.

## Paramètres d’annuaire {#directory-settings}

Lorsque vous ajoutez un annuaire à un domaine, spécifiez les paramètres d’annuaire suivants.

**Serveur :** (obligatoire) nom de domaine complet (FQDN) du serveur de répertoire. Par exemple, le nom de domaine complet d’un ordinateur appelé x sur le réseau corp.exemple.com est x.corp.exemple.com. Il est possible d’utiliser une adresse IP à la place du nom de domaine complet du serveur.

**Port :** (obligatoire) port utilisé par le serveur d’annuaire. Il s’agit du port 389 ou 636 si les informations d’authentification sont envoyées via le protocole SSL sur le réseau.

**SSL :** (obligatoire) indique si le serveur de répertoire utilise le protocole SSL pour envoyer les données sur le réseau. Le paramètre par défaut est Non. Lorsque la valeur est définie sur Oui, le certificat du serveur LDAP correspondant doit être approuvé par l’environnement d’exécution Java™ (JRE) du serveur d’applications.

**Binding :** (obligatoire) indique le mode d’accès au répertoire.

**Anonyme :** aucun nom d’utilisateur ni mot de passe requis. Une personne anonyme peut ne récupérer qu’une quantité limitée de données. Cette option peut se révéler utile pour le test initial.

**Utilisateur :** authentification requise. Dans le champ Nom, indiquez le nom de l’enregistrement utilisateur qui peut accéder à l’annuaire. Il est généralement conseillé d’entrer le nom distinctif complet (ND) du compte d’utilisateur, par exemple : cn=Jane Doe, ou=user, dc=can, dc=com. Dans le champ Mot de passe, saisissez le mot de passe associé. Ces paramètres sont requis lorsque vous sélectionnez Utilisateur comme option de liaison.

**Nom :** nom pouvant être utilisé pour la connexion à la base de données LDAP lorsque l’accès anonyme n’est pas activé. Pour Active Directory 2003, spécifiez `[domain name]\[userid]`. Pour Sun™ One, eDirectory ou IBM Tivoli Directory Server, spécifiez le nom qualifié complet de l’utilisateur, comme uid=lcuser,ou=it,o=company.com.

**Mot de passe :** mot de passe associé au nom indiqué pour la connexion à la base de données LDAP lorsque l’accès anonyme n’est pas activé.

**Renseigner la page avec :** lorsque cette option est sélectionnée, les attributs des pages contenant les paramètres Utilisateur et Groupe sont renseignés avec les valeurs LDAP par défaut correspondantes.

**Récupérer les ND de base :** permet de récupérer les ND de base et de les afficher dans la liste déroulante. Ce paramètre est utile lorsque vous avez plusieurs DN de base et que vous devez sélectionner une valeur.

**Activer le référentiel :** ce paramètre s’applique si votre entreprise utilise plusieurs domaines Active Directory organisés sous forme hiérarchique et si vous avez spécifié des paramètres d’annuaire pour le domaine parent uniquement. Dans ce cas, lorsque vous sélectionnez cette option, User Management peut accéder aux détails des utilisateurs, des utilisatrices et des groupes à partir des domaines enfants.

>[!NOTE]
>
>Cliquez sur Tester pour vérifier qu’une connexion peut être établie avec le serveur LDAP. Pour déterminer la cause principale de tous les échecs, consultez l’exception dans le fichier journal du serveur d’applications.

### Paramètres utilisateur {#user-settings}

**Identifiant unique :** (obligatoire) attribut unique et constant utilisé pour identifier les utilisateurs. Utilisez un attribut non ND comme identificateur unique, car le ND d’une personne peut changer si cette dernière évolue au sein de l’entreprise. Ce paramètre dépend du serveur d’annuaire. La valeur est objectGUID pour Active Directory 2003, nsuniqueID pour Sun™ One et guid pour eDirectory.

>[!NOTE]
>
>Vérifiez que vous spécifiez un attribut unique au sein de votre organisation. La saisie d’une valeur incorrecte peut en effet entraîner de graves dysfonctionnements au niveau du système.

**ND de base :** défini comme point de départ pour la synchronisation des utilisateurs et des groupes à partir de la hiérarchie LDAP. Il est préférable de spécifier un DN de base au niveau le plus bas de la hiérarchie qui englobe l’ensemble des utilisateurs, des utilisatrices et des groupes devant être synchronisés pour les services.

Si vous avez sélectionné l’option Activer la référence dans les paramètres d’annuaire, définissez l’option ND de base dans le *DC* du ND. Pour que la référence fonctionne, la recherche doit comporter les domaines parents et enfants.

>[!NOTE]
>
>N’incluez pas le ND de l’utilisateur ou de l’utilisatrice dans ce paramètre. Pour synchroniser un utilisateur ou une utilisatrice spécifique, utilisez le paramètre Filtre de recherche.

Bien que le paramètre ND de base soit obligatoire dans la console d’administration, certains serveurs d’annuaire tels que IBM Domino Enterprise Server peuvent requérir un ND de base vide. Pour spécifier un ND de base vide, exportez le fichier config.xml, modifiez le paramètre dans le fichier config.xml, puis réimportez-le. (Voir [Import et export du fichier de configuration](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).)

**Filtre de recherche :** (obligatoire) filtre de recherche à utiliser pour trouver l’enregistrement associé à l’utilisateur. Vous pouvez effectuer une recherche sur un seul niveau ou sur les niveaux inférieurs. (Voir Syntaxe des filtres de recherche, en anglais ou la RFC 2254.) Pour obtenir des informations supplémentaires sur le schéma Microsoft AD, voir Active Directory Schema (en anglais).

**Description :** attribut de schéma pour la description de l’utilisateur.

**Nom complet :** (obligatoire) attribut de schéma pour le nom complet de l’utilisateur.

**ID de connexion :** (obligatoire) attribut de schéma pour l’ID de connexion de l’utilisateur ou de l’utilisatrice.

**Nom :** (obligatoire) attribut de schéma pour le nom de l’utilisateur ou de l’utilisatrice.

**Prénom :** (obligatoire) attribut de schéma pour le prénom de l’utilisateur ou de l’utilisatrice.

**Initiales :** attribut de schéma pour les initiales de l’utilisateur ou de l’utilisatrice.

**Calendrier professionnel :** permet d’associer un calendrier professionnel à un utilisateur, en fonction de la valeur de ce paramètre (clé du calendrier professionnel). Les calendriers professionnels définissent les jours ouvrés et non ouvrés. AEM forms peut faire appel à des calendriers professionnels lors du calcul des dates et heures futures associées à des événements, tels que rappels, échéances et transmissions. Les clés de calendrier professionnel sont attribuées à des utilisateurs et utilisatrices en fonction du domaine utilisé (domaine d’entreprise, local ou hybride). Voir Configuration des calendriers professionnels. 

Si vous utilisez un domaine d’entreprise, vous pouvez associer le paramètre Calendrier professionnel à un champ du répertoire LDAP. Par exemple, si chaque personne enregistrée dans votre répertoire dispose d’un champ *pays* et que vous souhaitez affecter des calendriers professionnels en fonction du pays dans lequel la personne se trouve, spécifiez le nom du champ *pays* en tant que valeur du paramètre Calendrier professionnel. Vous pouvez ensuite associer les clés de calendrier professionnel (valeurs définies pour le champ *pays* dans le répertoire LDAP) aux calendriers professionnels dans Forms Workflow.

L’espace utilisé pour afficher le nom de la clé de calendrier professionnel dans les pages de Forms Workflow est limité. Limitez le nom de la clé de calendrier professionnel à moins de 53 caractères afin d’éviter qu’il ne soit tronqué sur ces pages.

**Modifier l’horodatage :** pour activer la synchronisation de répertoires delta, définissez cette valeur sur Modifier l’horodatage. Voir Activation de la synchronisation d’annuaires delta.

**Organisation :** attribut de schéma pour le nom de la société à laquelle appartient l’utilisateur.

**Adresse électronique principale :** attribut de schéma pour l’adresse électronique principale de l’utilisateur.

**Adresse électronique secondaire :** attribut de schéma pour l’adresse électronique secondaire de l’utilisateur.

**Téléphone :** attribut de schéma pour le numéro de téléphone de l’utilisateur ou de l’utilisatrice.

**Adresse postale :** attribut de schéma pour l’adresse postale de l’utilisateur ou de l’utilisatrice.

**Paramètres régionaux :** attribut de schéma contenant les paramètres régionaux ISO. La valeur de cet attribut est un code de langue à deux lettres ou un code de langue et de pays.

**Fuseau horaire :** attribut de schéma contenant le fuseau horaire de l’utilisateur. La valeur de cet attribut est une chaîne de type Ville/Pays.

**Activer le contrôle VLV (Virtual List View) :** contrôle LDAP qui permet à AEM Forms de récupérer les données par lots à partir du serveur d’annuaire. Si vous utilisez Sun One en tant qu’annuaire LDAP et si cet annuaire contient de nombreux utilisateurs, l’activation du contrôle VLV crée un index que User Management peut utiliser lors de la recherche d’utilisateurs. Cette option se révèle tout particulièrement utile lors de l’utilisation d’un compte d’utilisateur normal capable de synchroniser un volume limité de données seulement. Vous pouvez également activer le contrôle VLV pour les groupes. Si vous sélectionnez l’option Activer le contrôle VLV (Virtual List View), spécifiez un nom dans la zone Champ de tri.

>[!NOTE]
>
>Pour activer le contrôle VLV, configurez Sun One. Voir [Configurer User Management pour utiliser Virtual List View (VLV)](configuring-directories.md#configure-user-management-to-use-virtual-list-view-vlv).

**Champ de tri :** si vous avez sélectionné Activer le contrôle VLV (Virtual List View), indiquez le nom de l’attribut utilisé pour trier l’index. Il s’agit du nom de l’attribut (UID, par exemple) spécifié lors de la création d’un index pour VLV sur le serveur d’annuaire.

### Paramètres du groupe {#group-settings}

**Identifiant unique :** (obligatoire) attribut unique et constant utilisé pour identifier les groupes. Utilisez un attribut non ND comme identifiant unique. Ce paramètre dépend du serveur d’annuaire. La valeur est objectGUID pour Active Directory 2003, nsuniqueID pour Sun One et guid pour eDirectory.

>[!NOTE]
>
>Vérifiez que vous spécifiez un attribut unique au sein de votre organisation. La saisie d’une valeur incorrecte peut en effet entraîner de graves dysfonctionnements au niveau du système.

**ND de base :** (obligatoire) identifiant de base du répertoire.

Bien que le paramètre ND de base soit obligatoire dans la console d’administration, certains serveurs d’annuaire tels que IBM Domino Enterprise Server requièrent un ND de base vide. Pour spécifier un ND de base vide, exportez le fichier config.xml, modifiez le paramètre dans le fichier config.xml, puis réimportez-le. (Voir [Import et export du fichier du fichier de configuration](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).)

**Filtre de recherche :** (obligatoire) filtre de recherche à utiliser pour trouver l’enregistrement associé au groupe. Vous pouvez effectuer une recherche sur un seul niveau ou sur les niveaux inférieurs.

**Description :** attribut de schéma pour la description du groupe.

**Nom complet :** (obligatoire) attribut de schéma pour le nom complet du groupe.

**ND de membre :** (obligatoire) attribut de schéma pour le nom distinctif des membres d’un groupe.

**Identifiant unique de membre :** identifiant unique d’un utilisateur ou d’un groupe qui est membre du groupe sélectionné. La valeur de ce paramètre dépend du serveur d’annuaire. La valeur est objectSID pour Active Directory 2003, nsuniqueID pour Sun One et guid pour eDirectory.

Si un attribut non ND est spécifié pour l’option ND de membre, User Management utilise l’identifiant unique de membre pour effectuer une requête LDAP en vue de collecter le ND de l’utilisateur ou de l’utilisatrice, car il correspond à une valeur d’identifiant unique.

Si le ND est spécifié comme identifiant unique, il n’est pas nécessaire de configurer l’identifiant unique du membre.

**Organisation :** attribut de schéma pour le nom de la société à laquelle appartient le groupe.

**Adresse électronique principale :** attribut de schéma pour l’adresse électronique principale du groupe.

**Adresse électronique secondaire :** attribut de schéma pour l’adresse électronique secondaire du groupe.

**Modifier l’horodatage :** pour activer la synchronisation de répertoires delta, définissez cette valeur sur Modifier l’horodatage. Voir Activation de la synchronisation d’annuaires delta.

**Activer le contrôle VLV (Virtual List View) :** contrôle LDAP qui permet à AEM Forms de récupérer les données par lots à partir du serveur d’annuaire. Si vous utilisez Sun One en tant qu’annuaire LDAP et si cet annuaire contient de nombreux groupes, l’activation du contrôle VLV crée un index que User Management peut utiliser lors de la recherche de groupes. Cette option se révèle tout particulièrement utile lors de l’utilisation d’un compte d’utilisateur normal capable de synchroniser un volume limité de données seulement. Vous pouvez également activer le contrôle VLV pour les utilisateurs et utilisatrices. Si vous sélectionnez Activer le contrôle VLV (Virtual List View), indiquez un nom de champ de tri.

>[!NOTE]
>
>Pour activer le contrôle VLV, configurez Sun One. Voir [Configurer User Management pour utiliser Virtual List View (VLV)](configuring-directories.md#configure-user-management-to-use-virtual-list-view-vlv).

**Nom de champ de tri :** si vous avez sélectionné Activer le contrôle VLV (Virtual List View), indiquez le nom de l’attribut utilisé pour trier l’index. Il s’agit du nom de l’attribut spécifié lors de la création d’un index pour VLV sur le serveur d’annuaire.

>[!NOTE]
>
>cliquez sur Tester pour vérifier que les paramètres de l’utilisateur et du groupe sont collectés en fonction du ND de base et des critères de recherche.

Si des utilisateurs, des utilisatrices et des groupes sont renvoyés, les résultats affichent les valeurs affectées à chaque champ conformément au jeu d’attributs.

>[!NOTE]
>
>User Management ne prend pas en charge les ID utilisateur en double dans un domaine ; seul un utilisateur ou une utilisatrice portant l’ID utilisateur est synchronisé.

## Configuration de User Management pour utiliser Virtual List View (VLV) {#configure-user-management-to-use-virtual-list-view-vlv}

La synchronisation des annuaires est une exigence importante de User Management. Les utilisateurs, les utilisatrices et les groupes sont synchronisés d’un annuaire d’entreprise vers la base de données d’AEM Forms pour attribuer des rôles et des autorisations. Le nombre d’utilisateurs et d’utilisatrices varie de 100 à plus de 100 000 en fonction des exigences et cela pose un véritable défi technique lorsqu’il s’agit de synchroniser les données efficacement.

Le protocole LDAP fournit un mécanisme destiné à interroger les ensembles de données volumineux. Ce mécanisme utilise une liste paginée et des contrôles de demande. Si vous utilisez Microsoft Active Directory, la synchronisation entre le protocole LDAP et la base de données AEM Forms fait appel à PagedResultsControl pour récupérer les données dans des lots de taille particulière. Le serveur d’annuaire Sun ONE ne prend pas en charge ce contrôle. Pour terminer une requête paginée sur le serveur d’annuaire Sun ONE, veuillez utiliser le contrôle VLV (Virtual List View). Ce contrôle implique à la fois une configuration des annuaires côté serveur et une mise en œuvre côté client.

>[!NOTE]
>
>Cette section décrit l’utilisation du contrôle VLV pour le serveur d’annuaire Sun ONE. Cependant, vous pouvez utiliser ce contrôle pour tout serveur d’annuaire prenant en charge le contrôle VLV.

1. Lors de la configuration de l’annuaire, sélectionnez Activer le contrôle VLV (Virtual List View) sur les pages Paramètres utilisateur et Paramètres du groupe. Lorsque vous cochez cette case, vous devez également spécifier un nom de tri dans la zone Champ de tri. La valeur par défaut est uid. Voir [Ajout d’annuaires ou d’interfaces SPI personnalisées](configuring-directories.md#adding-directories-or-custom-spis) ou [Modification d’un annuaire](configuring-directories.md#edit-a-directory).
1. Utilisez la console d’administration Sun ONE ou un script de ligne de commande pour créer les entrées VLV LDAP pour les utilisateurs, les utilisatrices et les groupes. Si vous utilisez un script de ligne de commande, vous pouvez utiliser les fichiers LDIF utilisateurs et groupes fournis à titre d’exemple. (Voir [Configuration du serveur d’annuaire Sun ONE pour VLV](configuring-directories.md#configuring-the-sun-one-directory-server-for-vlv).)
1. Arrêtez le serveur et créez l’index requis. Voir [Création de l’index du serveur d’annuaire pour VLV](configuring-directories.md#create-the-directory-server-index-for-vlv).

### Configuration du serveur d’annuaire Sun ONE pour VLV {#configuring-the-sun-one-directory-server-for-vlv}

La création d’un contrôle VLV exige une paire d’entrées intégrant les classes d’objet `vlvSearch` et `vlvIndex`. L’entrée vlvSearch inclut une base de recherche et l’attribut `vlvFilter` qui définit la classe d’objet contenant les attributs à trier. La classe d’objet `vlvIndex` inclut l’attribut `vlvSort` qui spécifie un ou plusieurs attributs à trier et l’ordre dans lequel les trier. (Un signe moins (-) indique l’ordre alphabétique inverse). L’utilisation de VLV avec AEM Forms nécessite des entrées distinctes pour les utilisateurs, les utilisatrices et les groupes.

>[!NOTE]
>
>Les entrées d’objet peuvent être créées à l’aide de l’interface utilisateur graphique (GUI) Sun ONE ou à l’aide d’un script de ligne de commande. Pour obtenir des instructions sur la création des entrées d’objet à l’aide de la GUI, consultez la documentation de Sun ONE.

Voici un exemple de script LDIF pour une entrée VLV pour les utilisateurs et utilisatrices :

```text
 dn: cn=lcuser,cn=userRoot,cn=ldbm database,cn=plugins,cn=config
 objectclass: top
 objectclass: vlvSearch
 cn: lcuser
 vlvBase: dc=corp,dc=adobe,dc=com
 vlvScope: 2
 vlvFilter: (&(objectclass=inetOrgPerson))
 aci: (target="ldap:///cn=lcuser,cn=userRoot,cn=ldbm database,cn=plugins,cn=config")(targetattr="*")(version 3.0; acl "Config"
 ;allow(read,search,compare) userdn="ldap:///all"; )
 dn: cn=lcuser,cn=lcuser,cn=userRoot,cn=ldbm database,cn=plugins,cn=config
 cn: lcuser
 vlvSort: cn
 objectclass: top
 objectclass: vlvIndex
```

**Création des entrées d’objet à l’aide d’un script**

1. Le script donné en exemple contient une entrée LDAP appelée `lcuser`. Cette entrée est destinée à la configuration VLV pour la synchronisation des utilisateurs et des utilisatrices dans AEM Forms. Modifiez les propriétés suivantes en conséquence :

   **Nom de l’entrée :** le nom de l’entrée dans cet exemple est `lcuser`. Si `lcuser` est modifié, il doit l’être dans toutes les zones du script fourni à titre d’exemple.

   **vlvBase :** nom distinctif de base spécifié dans la page Paramètres utilisateur.

   **vlvFilter :** filtre de recherche spécifié dans la page Paramètres utilisateur.

   **vlvSort :** champ de tri défini dans la section des paramètres VLV de la page Paramètres utilisateur. Un contrôle VLV nécessite de spécifier un contrôle de tri. Ce champ est utilisé comme paramètre de tri pour l’index vlv créé.

   **aci :** le contrôle d’accès spécifié dans l’exemple de script accorde à toute personne authentifiée le droit d’accéder aux index VLV pour les opérations de lecture, de recherche et de comparaison. L’équipe d’administration peut restreindre l’accès à une personne de liaison qui est configurée dans la page Paramètres du serveur d’annuaire définie dans l’interface utilisateur de User Management. Si aucune autorisation n’est accordée, la recherche d’utilisateur ou d’utilisatrice ne peut pas utiliser le VLV. Le serveur LDAP renvoie en outre une exception d’autorisation.

   >[!NOTE]
   >
   >par convention, le nom de l’entrée vlvIndex est également `lcuser`, mais vous pouvez le nommer différemment. Utilisez le même nom dans l’outil vlvindex. Voir [Création de l’index du serveur d’annuaire pour VLV ](configuring-directories.md#create-the-directory-server-index-for-vlv)*.*

1. En vous aidant de l’outil `ldapmodify` fourni par le serveur Sun ONE, créez une entrée similaire pour les groupes en utilisant respectivement le nom distinctif de base du groupe, le filtre de recherche et le champ de tri :

   `server directory\shared\bin>ldapmodify -v -a -h host -p port -D "admin user" -w "password" -f "LDIF file location"`

   Par exemple, saisissez le texte suivant :

   `D:\tools\ldap\sun\shared\bin> -v -a -h localhost -p 55850 -D "uid=admin,ou=administrators,ou=topologymanagement,o=netscaperoot" -w "admin" -f "D:\tools\ldap\data\vlv feature\users.ldif"`

### Création de l’index de serveur d’annuaire pour VLV {#create-the-directory-server-index-for-vlv}

Lorsque vous avez configuré les paramètres d’annuaire et créé les entrées VLV LDAP pour les utilisateurs, les utilisatrices et les groupes, arrêtez le serveur et créez l’index requis.

1. Après avoir créé les entrées d’objet, arrêtez le serveur Sun ONE.
1. À l’aide de l’outil vlvindex, générez l’index en saisissant le texte suivant :

   *instance de serveur Directory* `\vlvindex.bat -n userRoot -T lcuser`

   La sortie suivante est générée :

   ```shell
    D:\tools\ldap\sun\shared\bin>..\..\slapd-chetanmeh-xp3\vlvindex.bat -n userRoot -T livecycle
    [21/Nov/2007:16:47:26 +051800] - userRoot: Indexing VLV: livecycle
    [21/Nov/2007:16:47:27 +051800] - userRoot: Indexed 1000 entries (5%).
    [21/Nov/2007:16:47:27 +051800] - userRoot: Indexed 2000 entries (9%).
    ...
    [21/Nov/2007:16:47:29 +051800] - userRoot: Indexed 20000 entries (94%).
    [21/Nov/2007:16:47:29 +051800] - userRoot: Indexed 21000 entries (99%).
    [21/Nov/2007:16:47:29 +051800] - userRoot: Finished indexing.
   ```

   L’outil vlvindex se trouve dans le répertoire de l’instance du serveur d’annuaire. Si le serveur Sun ONE comporte deux instances exécutant server1 et server2, l’outil vlvindex se trouve dans *répertoire du serveur Sun ONE*\server1. La valeur du paramètre `-T` correspond à la valeur de l’attribut `cn` dans l’entrée vlvindex créée ci-dessus dans le fichier LDIF fourni à titre d’exemple. En l’occurrence, il s’agit de `lcuser`.

1. Si le VLV est également activé pour les groupes, créez l’index correspondant pour les groupes. Vérifiez si les index sont créés en exécutant la commande suivante :

   *sun one server directory* `\shared\bin>ldapsearch -h`*hostname* `-p`*port no* `-s base -b "" objectclass=*`

   Une sortie du type de celle des données fournies à titre d’exemple est générée :

   ```shell
    D:\tools\ldap\sun\shared\bin>ldapsearch.exe -h localhost -p 55850 -s base -b "" objectclass=*
    ldapsearch.exe: started Tue Nov 27 16:34:20 2007
    version: 1
    dn:
    objectClass: top
    namingContexts: dc=corp,dc=adobe,dc=com
    supportedExtension: 2.16.840.1.113730.3.5.7
    ...
    vlvsearch: cn=MCC ou=testdata dc=corp dc=adobe dc=com, cn=userRoot,cn=ldbm dat
        abase,cn=plugins,cn=config
    vlvsearch: cn=lcuser,cn=userRoot,cn=ldbm database,cn=plugins,cn=config
    vlvsearch: cn=Browsing ou=testdata,cn=userRoot,cn=ldbm database,cn=plugins,cn=
        config
    1 matches
   ```
