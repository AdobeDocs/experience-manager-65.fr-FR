---
title: Configuration des annuaires
seo-title: Configuration des annuaires
description: Découvrez comment ajouter, modifier et supprimer des répertoires et comment configurer la gestion des utilisateurs afin d’utiliser VLV (Virtual List View).
seo-description: Découvrez comment ajouter, modifier et supprimer des répertoires et comment configurer la gestion des utilisateurs afin d’utiliser VLV (Virtual List View).
uuid: 0bf1a8a7-c917-4248-9937-d24e31c5ba17
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 1f15f028-aa81-478e-97eb-f83a4dc0418c
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '3246'
ht-degree: 78%

---


# Configuration des annuaires {#configuring-directories}

Pour chaque domaine d’entreprise que vous configurez, indiquez les annuaires que le fournisseur d’authentification interroge pour obtenir les informations utilisateur. Il est possible de configurer plusieurs annuaires par domaine.

## Ajout d’annuaires ou d’interfaces SPI personnalisées {#adding-directories-or-custom-spis}

Pour chaque domaine d’entreprise que vous configurez, indiquez les annuaires que le fournisseur d’authentification interroge pour obtenir les informations utilisateur. Vous pouvez ajouter un annuaire à un domaine d’entreprise existant ou à un nouveau domaine d’entreprise que vous ajoutez. Il est possible de configurer plusieurs annuaires par domaine. Vous pouvez également configurer un domaine afin qu’il utilise une interface SPI personnalisée pour la synchronisation.

### Ajout d’un annuaire  {#add-a-directory}

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des domaines.
1. Cliquez sur Nouveau domaine d’entreprise ou sélectionnez un domaine d’entreprise existant.
1. Cliquez sur Ajouter un annuaire.
1. Dans la zone Nom du profil, saisissez un nom permettant de distinguer cet annuaire, puis cliquez sur Suivant.
1. Configurez les paramètres du serveur d’annuaire. Voir [Paramètres d’annuaire](configuring-directories.md#directory-settings).
1. Cliquez sur Tester pour vérifier qu’il est possible d’établir une connexion avec le serveur LDAP. Si le test échoue, consultez l’exception dans le fichier journal du serveur d’applications pour déterminer la cause initiale de l’échec. Cliquez sur Fermer, puis sur Suivant.
1. Sélectionnez Paramètres utilisateur et procédez à la configuration requise. Voir [Paramètres d’annuaire](configuring-directories.md#directory-settings).
1. Cliquez sur Tester pour vérifier que le DN de base et les autres attributs configurés collectent le lot d’utilisateurs correct. LDAP tente de récupérer les 200 premiers enregistrements à l’aide des paramètres fournis (ND de base, filtre de recherche et tous les attributs).

   Si des utilisateurs sont renvoyés, les résultats affichent les valeurs affectées à chaque champ conformément à l’ensemble d’attributs. Si le test échoue en raison d’un nom de serveur non existant, d’informations d’identification erronées ou d’attributs incorrects, le message d’erreur suivant apparaît : « Les critères de recherche spécifiés ne renvoient aucun résultat ». Pour déterminer la cause initiale de l’échec, consultez l’exception dans le fichier journal du serveur d’applications. Cliquez sur Fermer, puis sur Suivant.

1. Sélectionnez Paramètres du groupe et procédez à la configuration requise. Voir [Paramètres d’annuaire](configuring-directories.md#directory-settings).
1. Cliquez sur Tester pour vérifier que le DN de base et les autres attributs configurés collectent le lot de groupes correct. Si des groupes sont renvoyés, les résultats affichent les valeurs affectées à chaque champ conformément à l’ensemble d’attributs. Cliquez sur Fermer.

### Ajout d’une interface SPI personnalisée  {#add-a-custom-spi}

Pour plus d’informations sur la création d’une interface SPI personnalisée, consultez la section « Développement d’interfaces SPI pour AEM Forms » dans [Programmation avec AEM Forms](https://www.adobe.com/go/learn_aemforms_programming_63). Afin de rendre disponible une interface SPI personnalisée déployée récemment pour une association au domaine, redémarrez le serveur.

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des domaines.
1. Cliquez sur Nouveau domaine d’entreprise ou sélectionnez un domaine d’entreprise existant.
1. Cliquez sur Ajouter un annuaire.
1. Saisissez un nom dans la zone Nom du profil, sélectionnez Fournisseur SPI personnalisé, puis cliquez sur Suivant.
1. Sélectionnez un fournisseur d’utilisateurs personnalisé dans la liste et cliquez sur Suivant.
1. Sélectionnez un fournisseur de groupes personnalisé dans la liste et cliquez sur Terminer.

## Modification d’un annuaire  {#edit-a-directory}

Vous pouvez modifier les détails d’un annuaire déjà configuré.

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des domaines.
1. Cliquez sur le domaine voulu dans la liste, puis, dans la page qui apparaît, sélectionnez l’annuaire approprié dans la liste.
1. Configurez les paramètres relatifs à l’annuaire, à l’utilisateur et au groupe. Voir [Paramètres d’annuaire](configuring-directories.md#directory-settings).
1. Cliquez sur OK.

## Suppression d’un annuaire  {#delete-a-directory}

Lorsque vous synchronisez vos domaines après la suppression d’un annuaire, tous les utilisateurs et groupes de cet annuaire sont marqués comme obsolètes dans la base de données. Ils ne sont renvoyés dans aucune recherche effectuée à partir de Administration Console.

>[!NOTE]
>
>les domaines d’entreprise requièrent au moins un fournisseur d’authentification et un fournisseur d’annuaires.

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des domaines.
1. Sélectionnez le domaine approprié dans la liste.
1. Cochez la case correspondant à l’annuaire approprié, puis cliquez sur Supprimer.
1. Cliquez sur OK dans la page de confirmation qui s’affiche, puis de nouveau sur OK.

## Paramètres d’annuaire  {#directory-settings}

Lorsque vous ajoutez un nouvel annuaire à un domaine, définissez les paramètres d’annuaire suivants.

**Serveur :** (obligatoire) nom de domaine complet (FQDN) du serveur d’annuaire. Par exemple, le nom de domaine complet d’un ordinateur appelé x sur le réseau corp.adobe.com est x.corp.adobe.com. Il est possible d’utiliser une adresse IP à la place du nom de domaine complet du serveur.

**Port :** (obligatoire) port utilisé par le serveur d’annuaire. Il s’agit du port 389 ou 636 si les informations d’authentification sont envoyées via le protocole SSL sur le réseau.

**SSL:** (obligatoire) indique si le serveur d’annuaire utilise SSL lors de l’envoi de données sur le réseau. La valeur par défaut est Non. Avec la valeur Oui, le certificat du serveur LDAP correspondant doit être approuvé par l’environnement d’exécution Java™ (JRE) du serveur d’applications.

**Liaison**  (obligatoire) indique comment accéder à l’annuaire.

**Anonyme :** aucun nom d’utilisateur ou mot de passe n’est requis. Un utilisateur anonyme peut récupérer uniquement un volume limité de données. Cette option se révèle utile pour les premiers tests.

**User:** Authentication est requis. Dans le champ Nom, indiquez le nom de l’enregistrement utilisateur qui peut accéder à l’annuaire. Il est généralement conseillé d’entrer le nom distinctif complet (ND) du compte utilisateur, par exemple : cn=Jane Doe, ou=user, dc=can, dc=com. Dans le champ Mot de passe, indiquez le mot de passe associé. Ces paramètres sont obligatoires lorsque vous sélectionnez Utilisateur pour l’option Liaison.

**Nom :** nom qui peut être utilisé pour la connexion à la base de données LDAP lorsque l’accès anonyme n’est pas activé. Pour Principale Directory 2003, indiquez `[domain name]\[userid]`. Pour Sun™ One, eDirectory ou IBM Tivoli Directory Server, spécifiez le nom qualifié complet de l’utilisateur, comme uid=lcuser,ou=it,o=company.com.

**Mot de passe :** mot de passe correspondant au nom que vous avez spécifié pour la connexion à la base de données LDAP lorsque l’accès anonyme n’est pas activé.

**Remplir la page avec :** lorsque cette option est sélectionnée, les attributs des pages de paramètres Utilisateur et Groupe sont renseignés avec les valeurs LDAP par défaut correspondantes.

**Récupérer les DN de base :** Récupère les DN de base et les affiche dans la liste déroulante. Ce paramètre est utile lorsque vous avez plusieurs DN de base et que vous devez sélectionner une valeur.

**Activer le référent :** ce paramètre est applicable lorsque votre organisation utilise plusieurs domaines Principale Directory organisés dans une structure hiérarchique et que vous avez spécifié des paramètres d&#39;annuaire pour le domaine parent uniquement. Dans ce cas, lorsque vous sélectionnez cette option, User Management peut accéder aux détails des utilisateurs et des groupes à partir des domaines enfants.

>[!NOTE]
>
>cliquez sur Tester pour vérifier qu’il est possible d’établir une connexion au serveur LDAP. Pour déterminer la cause d’un échec, consultez l’exception dans le fichier journal du serveur d’applications.

### Paramètres utilisateur {#user-settings}

**Identificateur unique :** (obligatoire) attribut unique et constant utilisé pour identifier les utilisateurs. Utilisez un attribut non ND comme identificateur unique, car le ND d’un utilisateur peut changer si l’utilisateur évolue au sein de l’entreprise. Ce paramètre dépend du serveur d’annuaire. La valeur est objectGUID pour Active Directory 2003, nsuniqueID pour Sun™ One et guid pour eDirectory.

>[!NOTE]
>
>vérifiez que vous spécifiez un attribut unique au sein de votre entreprise. La saisie d’une valeur incorrecte peut en effet entraîner de graves dysfonctionnements au niveau du système.

**ND de base :** défini comme point de départ pour la synchronisation des utilisateurs et des groupes à partir de la hiérarchie LDAP. Il est préférable de spécifier un DN de base au niveau inférieur de la hiérarchie, de manière à englober tous les utilisateurs et les groupes à synchroniser pour les services.

Si vous avez sélectionné l’option Activer le référentiel dans les paramètres d’annuaire, sélectionnez la partie *dc* du ND comme ND de base. Pour que le référentiel fonctionne, la recherche doit porter sur les domaines parents et enfants.

>[!NOTE]
>
>n’incluez pas le ND de l’utilisateur dans ce paramètre. Pour synchroniser un utilisateur particulier, utilisez le paramètre Filtre de recherche.

Bien que le paramètre ND de base soit obligatoire dans Administration Console, certains serveurs d’annuaire tels que IBM Domino Enterprise Server peuvent requérir un ND de base vide. Pour en définir un, exportez le fichier config.xml, modifiez le paramètre correspondant dans ce fichier, puis réimportez-le. Voir [Importation et exportation du fichier de configuration](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).

**Filtre de recherche :** (obligatoire) filtre de recherche à utiliser pour trouver l’enregistrement associé à l’utilisateur. Vous pouvez effectuer une recherche sur un seul niveau ou sur les niveaux inférieurs. (Voir Syntaxe des filtres de recherche, en anglais ou la RFC 2254.) Pour obtenir des informations supplémentaires sur le schéma Microsoft AD, voir Active Directory Schema (en anglais).

**Description:attribut de** Schéma pour la description de l’utilisateur

**Nom complet :**  attribut de Schéma (obligatoire) pour le nom complet de l’utilisateur.

**ID de connexion :**  attribut de Schéma (obligatoire) pour l’ID de connexion de l’utilisateur.

**Nom : attribut de Schéma** (obligatoire) pour le nom de famille de l’utilisateur.

**Attribut de Schéma Prénom:** (obligatoire) pour le prénom de l’utilisateur

**Initiales:attribut de** Schéma pour les initiales de l’utilisateur

**Calendrier professionnel : vous** permet de mapper un calendrier professionnel à un utilisateur, en fonction de la valeur de ce paramètre (clé de calendrier professionnel). Les calendriers professionnels définissent les jours ouvrés et non ouvrés. AEM forms peut faire appel à des calendriers professionnels lors du calcul des dates et heures futures associées à des événements, tels que rappels, échéances et transmissions. Les clés de calendrier professionnel sont attribuées à des utilisateurs en fonction du domaine utilisé (domaine d’entreprise, local ou hybride). Voir Configuration des calendriers professionnels. 

Si vous utilisez un domaine d’entreprise, vous pouvez associer le paramètre Calendrier professionnel à un champ de l’annuaire LDAP. Par exemple, si chaque utilisateur enregistré dans votre annuaire dispose d’un champ *pays* et que vous souhaitez affecter des calendriers professionnels en fonction du pays dans lequel l’utilisateur se trouve, spécifiez le nom du champ *pays* en tant que valeur du paramètre Calendrier professionnel. Vous pouvez ensuite associer les clés de calendrier professionnel (valeurs définies pour le champ *pays* dans l’annuaire LDAP) aux calendriers professionnels dans le processus des formulaires.

L’espace utilisé pour l’affichage du nom de clé du calendrier professionnel dans les pages du processus des formulaires est limité. Limitez le nom de la clé de calendrier professionnel à 53 caractères afin d’éviter qu’il ne soit tronqué sur ces pages.

**Modifier l’horodatage :** Pour activer la synchronisation d’annuaires delta, définissez cette valeur sur modify TimeStamp. Voir Activation de la synchronisation d’annuaires delta.

**Organisation : attribut** Schéma pour le nom de l’organisation à laquelle appartient l’utilisateur.

**Adresse électronique Principal : attribut** Schéma pour l’adresse électronique Principale de l’utilisateur.

**Adresse électronique Secondaire : attribut** Schéma pour l’adresse électronique secondaire de l’utilisateur.

**Téléphone : attribut de** Schéma pour le numéro de téléphone de l’utilisateur.

**Adresse postale : attribut de** Schéma pour l’adresse postale de l’utilisateur.

**Attribut Locale:** Schéma contenant les informations de paramètres régionaux ISO. La valeur de cet attribut est un code de langue à deux lettres ou un code de langue et de pays.

**Fuseau horaire : attribut de** Schéma qui contient le fuseau horaire où se trouve l’utilisateur. La valeur de cet attribut est une chaîne de type Ville/Pays.

**Activer le contrôle VLV (Virtual Liste Vue) :** contrôle LDAP qui permet à AEM forms de récupérer des données par lots à partir du serveur d’annuaire. Si vous utilisez Sun One en tant qu’annuaire LDAP et si cet annuaire contient de nombreux utilisateurs, l’activation du contrôle VLV crée un index que User Management peut utiliser lors de la recherche d’utilisateurs. Cette option se révèle tout particulièrement utile lors de l’utilisation d’un compte utilisateur normal capable de synchroniser un volume limité de données seulement. Vous pouvez également activer le contrôle VLV pour les groupes. Si vous sélectionnez l’option Activer le contrôle VLV (Virtual List View), spécifiez un nom dans la zone Champ de tri.

>[!NOTE]
>
>pour activer le contrôle VLV, configurez Sun One. Voir [Configurer User Management pour utiliser la Vue de Liste virtuelle (VLV)](configuring-directories.md#configure-user-management-to-use-virtual-list-view-vlv).

**Champ de tri :** si vous avez sélectionné Activer le contrôle VLV (Virtual Liste Vue), indiquez le nom d’attribut utilisé pour trier l’index. Il s’agit du nom de l’attribut (uid, par exemple) spécifié lors de la création d’un index pour VLV sur le serveur d’annuaire.

### Paramètres du groupe {#group-settings}

**Identificateur unique :** (obligatoire) attribut unique et constant utilisé pour identifier les groupes. Utilisez un attribut non DN comme identificateur unique. Ce paramètre dépend du serveur d’annuaire. La valeur est objectGUID pour Active Directory 2003, nsuniqueID pour Sun One et guid pour eDirectory.

>[!NOTE]
>
>vérifiez que vous spécifiez un attribut unique au sein de votre entreprise. La saisie d’une valeur incorrecte peut en effet entraîner de graves dysfonctionnements au niveau du système.

**ND de base :** (obligatoire) nom unique de base du répertoire.

Bien que le paramètre ND de base soit obligatoire dans Administration Console, certains serveurs d’annuaire tels que IBM Domino Enterprise Server requièrent un ND de base vide. Pour en définir un, exportez le fichier config.xml, modifiez le paramètre correspondant dans ce fichier, puis réimportez-le. Voir [Importation et exportation du fichier de configuration](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).

**Filtre de recherche :** (obligatoire) filtre de recherche à utiliser pour trouver l&#39;enregistrement associé au groupe. Vous pouvez effectuer une recherche sur un seul niveau ou sur les niveaux inférieurs.

**Description:attribut de** Schéma pour la description du groupe

**Nom complet :**  attribut de Schéma (obligatoire) pour le nom complet du groupe

**ND de membre : attribut de Schéma** (obligatoire) pour le nom unique des membres d’un groupe

**Identificateur unique de membre : identifiant** unique d&#39;un utilisateur ou d&#39;un groupe membre du groupe sélectionné. La valeur de ce paramètre dépend du serveur d’annuaire. La valeur est objectSID pour Active Directory 2003, nsuniqueID pour Sun One et guid pour eDirectory.

Si un attribut non ND est spécifié pour l’option ND de membre, User Management utilise l’identificateur unique de membre pour interroger LDAP en vue de collecter le ND de l’utilisateur, car il correspond à une valeur d’identificateur unique.

Si ND est spécifié comme identificateur unique, il n’est pas nécessaire de configurer l’identificateur unique de membre.

**Organisation : attribut de** Schéma pour le nom de l’organisation à laquelle appartient le groupe.

**Adresse électronique Principal : attribut** Schéma pour l’adresse électronique Principale du groupe.

**Courriel Secondaire : attribut** Schéma pour l’adresse électronique secondaire du groupe

**Modifier l’horodatage :** Pour activer la synchronisation d’annuaires delta, définissez cette valeur sur modify TimeStamp. Voir Activation de la synchronisation d’annuaires delta.

**Activer le contrôle VLV (Virtual Liste Vue) :** contrôle LDAP qui permet à AEM forms de récupérer des données par lots à partir du serveur d’annuaire. Si vous utilisez Sun One en tant qu’annuaire LDAP et si cet annuaire contient de nombreux groupes, l’activation du contrôle VLV crée un index que User Management peut utiliser lors de la recherche de groupes. Cette option se révèle tout particulièrement utile lors de l’utilisation d’un compte utilisateur normal capable de synchroniser un volume limité de données seulement. Vous pouvez également activer le contrôle VLV pour les utilisateurs. Si vous sélectionnez l’option Activer le contrôle VLV (Virtual List View), spécifiez un nom de champ de tri.

>[!NOTE]
>
>pour activer le contrôle VLV, configurez Sun One. Voir [Configurer User Management pour utiliser la Vue de Liste virtuelle (VLV)](configuring-directories.md#configure-user-management-to-use-virtual-list-view-vlv).

**Nom du champ de tri :** si vous avez sélectionné Activer le contrôle VLV (Virtual Liste Vue), indiquez le nom d’attribut utilisé pour trier l’index. Il s’agit du nom de l’attribut spécifié lors de la création d’un index pour VLV sur le serveur d’annuaire.

>[!NOTE]
>
>cliquez sur Tester pour vérifier que les paramètres de l’utilisateur et du groupe sont collectés en fonction du ND de base et des critères de recherche.

Si des utilisateurs et des groupes sont renvoyés, les résultats affichent les valeurs qui sont affectées à chaque champ conformément à l’ensemble d’attributs.

>[!NOTE]
>
>User Management ne prend pas en charge les ID utilisateur en double dans un même domaine, et seul un utilisateur portant cet ID utilisateur est synchronisé.

## Configuration de User Management pour utiliser Virtual List View (VLV)  {#configure-user-management-to-use-virtual-list-view-vlv}

Il est très important de synchroniser les annuaires de User Management. Les utilisateurs et les groupes sont synchronisés depuis un annuaire d’entreprise vers la base de données AEM forms afin d’attribuer les rôles et les autorisations. Le nombre d’utilisateurs varie de 100 à plus de 100 000 en fonction des exigences et cela pose un véritable défi technique lorsqu’il s’agit de synchroniser les données efficacement.

Le protocole LDAP fournit un mécanisme destiné à interroger les ensembles de données volumineux. Ce mécanisme utilise une liste paginée et des contrôles de demande. Si vous utilisez Microsoft Active Directory, la synchronisation entre le protocole LDAP et la base de données AEM forms fait appel à PagedResultsControl pour récupérer les données dans des lots de taille particulière. Le serveur d’annuaire Sun ONE ne prend pas en charge ce contrôle. Pour terminer une requête paginée sur le serveur d’annuaire Sun ONE, utilisez le contrôle VLV (Virtual List View). Ce contrôle implique une configuration des annuaires côté serveur et une mise en œuvre côté client.

>[!NOTE]
>
>cette section décrit l’utilisation du contrôle VLV pour le serveur d’annuaire Sun ONE. Cependant, vous pouvez utiliser ce type de contrôle pour tout serveur d’annuaire prenant en charge le contrôle VLV.

1. Lors de la configuration de l’annuaire, sélectionnez Activer le contrôle VLV (Virtual List View) sur les pages Paramètres utilisateur et Paramètres du groupe. Lorsque vous cochez cette case, vous devez également spécifier un nom de tri dans la zone Nom de champ de tri. La valeur par défaut est uid. Voir [Ajout d’annuaires ou d’interfaces SPI personnalisées ](configuring-directories.md#adding-directories-or-custom-spis) ou [Modification d’un annuaire](configuring-directories.md#edit-a-directory).
1. Utilisez Sun ONE Administration Console ou un script de ligne de commande pour créer les entrées VLV LDAP des utilisateurs et des groupes. Si vous utilisez un script de ligne de commande, aidez-vous des fichiers LDIF utilisateurs et groupes fournis à titre d’exemple. Voir [Configuration du serveur d’annuaire Sun ONE pour VLV](configuring-directories.md#configuring-the-sun-one-directory-server-for-vlv).
1. Arrêtez le serveur et redémarrez l’index requis. Voir [Création de l’index du serveur d’annuaire pour VLV](configuring-directories.md#create-the-directory-server-index-for-vlv).

### Configuration du serveur d’annuaire Sun ONE pour VLV  {#configuring-the-sun-one-directory-server-for-vlv}

La création d’un contrôle VLV exige une paire d’entrées intégrant les classes d’objet `vlvSearch` et `vlvIndex`. L’entrée vlvSearch inclut une base de recherche et l’attribut `vlvFilter` qui définit la classe d’objet contenant les attributs à trier. La classe d&#39;objet `vlvIndex` comprend l&#39;attribut `vlvSort`, qui spécifie un ou plusieurs attributs à trier et l&#39;ordre de tri. (Un signe moins (-) indique l’ordre alphabétique inverse). L’utilisation du contrôle VLV avec AEM forms exige des entrées séparées pour les utilisateurs et les groupes.

>[!NOTE]
>
>il est possible de créer les entrées d’objet au moyen de l’interface utilisateur graphique Sun ONE ou au moyen d’un script de ligne de commande. Pour plus d’instructions sur la création d’entrées d’objet à l’aide de l’interface utilisateur graphique, consultez la documentation de Sun ONE.

Vous trouverez ci-dessous un exemple de script LDIF pour une entrée VLV relative aux utilisateurs :

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

1. Le script donné en exemple contient une entrée LDAP appelée `lcuser`. Cette entrée sert à la configuration du contrôle VLV pour la synchronisation des utilisateurs dans AEM forms. Modifiez les propriétés suivantes en conséquence :

   **Nom de l’entrée :** le nom de l’entrée dans cet exemple est `lcuser`. Si `lcuser` est modifié, il doit l’être dans toutes les zones du script fourni à titre d’exemple.

   **vlvBase :** ND de base défini dans la page Paramètres utilisateur.

   **vlvFilter :** filtre de recherche défini dans la page Paramètres utilisateur.

   **vlvSort :** champ de tri indiqué dans la section des paramètres VLV de la page Paramètres utilisateur. Un contrôle VLV exige la définition d’un contrôle du tri. Ce champ est utilisé comme paramètre de tri pour l’index vlv créé.

   **aci :** le contrôle d’accès défini dans l’exemple de script accorde à tous les utilisateurs authentifiés l’accès aux index VLV pour des opérations de lecture, de recherche et de comparaison. L’administrateur peut restreindre l’accès à l’utilisateur configuré sur la page des paramètres du serveur d’annuaire défini dans l’interface utilisateur de User Management. Si aucune autorisation n’est accordée, les recherches utilisateur ne peuvent pas utiliser le contrôle VLV et le serveur LDAP envoie une exception d’autorisation.

   >[!NOTE]
   >
   >par convention, le nom de l’entrée vlvIndex est également `lcuser`, mais vous pouvez le nommer différemment. Utilisez le même nom dans l’outil vlvindex. Voir [Création de l’index du serveur d’annuaire pour VLV ](configuring-directories.md#create-the-directory-server-index-for-vlv)*.*

1. En vous aidant de l’outil `ldapmodify` fourni par le serveur Sun ONE, créez une entrée similaire pour les groupes en utilisant respectivement le nom distinctif de base du groupe, le filtre de recherche et le champ de tri :

   `server directory\shared\bin>ldapmodify -v -a -h host -p port -D "admin user" -w "password" -f "LDIF file location"`

   Par exemple, saisissez le texte suivant :

   `D:\tools\ldap\sun\shared\bin> -v -a -h localhost -p 55850 -D "uid=admin,ou=administrators,ou=topologymanagement,o=netscaperoot" -w "admin" -f "D:\tools\ldap\data\vlv feature\users.ldif"`

### Création de l’index du serveur d’annuaire pour VLV {#create-the-directory-server-index-for-vlv}

Après avoir configuré les paramètres d’annuaire et créé les entrées VLV LDAP des utilisateurs et des groupes, arrêtez le serveur et créez l’index requis.

1. Après avoir créé les entrées d’objet, arrêtez le serveur Sun ONE.
1. A l’aide de l’outil vlvindex, générez l’index en saisissant :

   *instance du serveur de répertoires* `\vlvindex.bat -n userRoot -T lcuser`

   La sortie suivante est alors générée :

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

   L’outil vlvindex figure dans le répertoire de l’instance du serveur d’annuaire. Si le serveur Sun ONE possède deux instances exécutant server1 et server2, alors l’outil vlvindex se situe dans le *répertoire annuaire serveur Sun ONE*\server1. La valeur du paramètre `-T` correspond à la valeur de l’attribut `cn` de l’entrée vlvindex créée précédemment dans l’exemple LDIF. En l’occurrence, il s’agit de `lcuser`.

1. Si le contrôle VLV est activé pour les groupes, créez l’index correspondant pour les groupes. Vérifiez que les index ont été créés en exécutant la commande suivante :

   *sun one server* `\shared\bin>ldapsearch -h`** `-p`*directoryhostnameport no* `-s base -b "" objectclass=*`

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

