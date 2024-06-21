---
title: User Management Forms | Gestion des données utilisateur
description: Découvrez comment le composant User Management d’AEM Forms JEE vous permet de créer, d’autoriser et de gérer les utilisateurs et utilisatrices qui doivent accéder à AEM Forms.
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
role: Admin,User
exl-id: eeeab5d1-073a-4e13-a781-391dfe70bb37
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 100%

---

# User Management Forms | Gestion des données utilisateur {#forms-user-management-handling-user-data}

User Management est un composant d’AEM Forms JEE qui permet de créer, de gérer et d’autoriser les utilisateurs et utilisatrices d’AEM Forms à accéder à AEM Forms. User Management utilise des domaines en tant qu’annuaires pour obtenir des informations sur les utilisateurs et utilisatrices. Les types de domaine suivants sont pris en charge :

**Domaines locaux** : ce type de domaine n’est pas connecté à un système de stockage tiers. En effet, les utilisateurs, les utilisatrices et les groupes sont créés localement et résident dans la base de données User Management. Les mots de passe sont stockés localement et l’authentification est effectuée à l’aide d’une base de données locale.

**Domaines hybrides** : ce type de domaine n’est pas connecté à un système de stockage tiers. En effet, les utilisateurs, les utilisatrices et les groupes sont créés localement et résident dans la base de données User Management. Contrairement aux domaines locaux, les domaines hybrides utilisent un fournisseur d’authentification externe, qui peut être LDAP, Kerberos, SAML ou un fournisseur d’authentification personnalisé.

**Domaines d’entreprise** : ils sont constitués d’utilisateurs, d’utilisatrices et de groupes résidant dans un système de stockage tiers, tel qu’un annuaire LDAP. User Management n’a pas la possibilité d’écrire dans le système de stockage tiers, mais assure la synchronisation des informations relatives aux utilisateurs, aux utilisatrices et aux groupes avec sa propre base de données. Les domaines d’entreprise utilisent également un fournisseur d’authentification externe pouvant être LDAP, Kerberos, SAML ou un fournisseur d’authentification personnalisé.

<!-- Fix broken links For more information about how user management works and configured, see AEM Forms JEE administration help. -->

## Données utilisateur et stockage de données {#user-data-and-data-stores}

User Management stocke des données utilisateur dans une base de données telle que MySQL, Oracle, MS® SQL Server et IBM® DB2®. De plus, tout utilisateur qui s’est connecté au moins une fois dans les applications Forms sur l’instance d’auteur AEM à l’adresse `https://'[server]:[port]'lc`, est créé dans le référentiel AEM. User Management est donc enregistré dans les magasins de données suivants :

* Base de données
* Référentiel AEM
* Stockage tiers tel qu’un annuaire LDAP

>[!NOTE]
>
>Les données stockées dans des stockages tiers ne sont pas couvertes par ce document. Contactez directement le fournisseur tiers pour gérer les données utilisateur dans ces stockages.

### Base de données {#database}

User Management stocke les données utilisateur dans les tables de base de données suivantes :

<table>
 <tbody>
  <tr>
   <td>Tableau de base de données</td>
   <td>Description</td>
  </tr>
  <tr>
   <td><code>EdcPrincipalEntity</code></td>
   <td><p>Stocke des informations sur les entités principales. L’entité Principal peut correspondre à un utilisateur, une utilisatrice, un groupe ou un rôle.</p> <p> </p> </td>
  </tr>
  <tr>
   <td><code>EdcPrincipalUserEntity</code></td>
   <td>Stocke des informations d’identification personnelle des utilisateurs et des utilisatrices. Elle contient une entrée pour chaque utilisateur et utilisatrice provenant de domaines locaux, d’entreprise et hybrides.</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalLocalAccountEntity</code></p> <p><code class="code">EdcPrincipalLocalAccount
       </code>(bases de données Oracle et MS® SQL)</p> </td>
   <td>Stocke les données uniquement pour les utilisatrices ou utilisateurs locaux.</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalEmailAliasEntity</code></p> <p><code class="code">EdcPrincipalEmailAliasEn
       </code>(bases de données Oracle et MS® SQL)</p> </td>
   <td>Contient les entrées de l’ensemble des utilisateurs et utilisatrices provenant de domaines locaux, d’entreprise et hybrides. Contient des ID d’e-mail d’utilisateurs ou d’utilisatrices.</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalGrpCtmntEntity</code></p> <p><code>EdcPrincipalGrpCtmntEnti</code><br /> (bases de données Oracle et MS® SQL)</p> </td>
   <td>Stocke le mappage entre les utilisateurs, les utilisatrices et les groupes.</td>
  </tr>
  <tr>
   <td><code>EdcPrincipalRoleEntity</code></td>
   <td>Stocke le mappage entre les rôles et l’entité Principal pour les utilisateurs, les utilisatrices et les groupes.</td>
  </tr>
  <tr>
   <td><code>EdcPriResPrmEntity</code></td>
   <td>Stocke le mappage entre l’entité Principal et les autorisations pour les utilisateurs, les utilisatrices et les groupes.</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalMappingEntity</code></p> <p><code>EdcPrincipalMappingEntit</code><br /> (bases de données Oracle et MS® SQL)</p> </td>
   <td>Stocke les anciennes et nouvelles valeurs d’attribut associées à une entité Principal.<br /> </td>
  </tr>
 </tbody>
</table>

### Référentiel AEM {#aem-repository}

Les données User Management qui ont accédé au moins une fois aux applications Forms à l’adresse `https://'[server]:[port]'lc` sont également stockées dans le référentiel AEM.

## Accès et suppression des données utilisateur {#access-and-delete-user-data}

Vous pouvez accéder aux données User Management et les exporter pour les utilisateurs et utilisatrices dans les bases de données User Management et dans le référentiel AEM, puis les supprimer définitivement si nécessaire.

### Base de données {#database-1}

Pour exporter ou supprimer des données utilisateur d’une base de données User Management, vous devez vous connecter à la base de données à l’aide d’un client de base de données et rechercher l’identifiant principal en fonction de certaines informations d’identification personnelle de l’utilisateur ou de l’utilisatrice. Par exemple, pour récupérer l’ID principal d’un utilisateur à l’aide d’un ID de connexion, exécutez la commande `select` suivante sur la base de données.

Dans la commande `select`, remplacez l’ID de connexion `<user_login_id>` par l’ID de connexion de l’utilisateur dont vous souhaitez récupérer l’ID principal.

```sql
select refprincipalid from EdcPrincipalUserEntity where uidstring = <user_login_id>
```

Une fois que vous connaissez l’identifiant principal, vous pouvez exporter ou supprimer les données utilisateur.

#### Exporter les données utilisateur {#export-user-data}

Exécutez les commandes de base de données suivantes pour exporter les données User Management d’un ID principal à partir des tables de base de données. Dans la commande `select`, remplacez `<principal_id>` par l’ID principal de l’utilisateur ou de l’utilisatrice dont vous souhaitez exporter les données.

>[!NOTE]
>
>Les commandes suivantes utilisent des noms de tables de base de données dans les bases de données MySQL et IBM® DB2®. Lors de l’exécution de ces commandes sur les bases de données Oracle et MS® SQL, remplacez les noms de table suivants dans les commandes :
>
>* Remplacez `EdcPrincipalLocalAccountEntity` par `EdcPrincipalLocalAccount`
>
>* Remplacez `EdcPrincipalEmailAliasEntity` par `EdcPrincipalEmailAliasEn`
>
>* Remplacez `EdcPrincipalMappingEntity` par `EdcPrincipalMappingEntit`
>
>* Remplacez `EdcPrincipalGrpCtmntEntity` par `EdcPrincipalGrpCtmntEnti`
>

```sql
Select * from EdcPrincipalLocalAccountEntity where refuserprincipalid in (Select id from EdcPrincipalUserEntity where refprincipalid in (Select id from EDCPRINCIPALENTITY where id='<principal_id>'));

Select * from EdcPrincipalEmailAliasEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalRoleEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPriResPrmEntity where refprinid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalUserEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalMappingEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalGrpCtmntEntity where refchildprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalEntity where id='<principal_id>';
```

#### Suppression de données utilisateur {#delete-user-data}

Procédez comme suit pour supprimer les données User Management d’un ID principal des tables de base de données.

1. Supprimez les données utilisateur du référentiel AEM, le cas échéant, comme décrit dans [Suppression de données utilisateur](/help/forms/using/user-management-handling-user-data.md#delete-aem).
1. Arrêtez AEM Forms Server.
1. Exécutez les commandes de base de données suivantes afin de pouvoir supprimer les données User Management pour un ID principal des tables de base de données. Dans la commande `Delete`, remplacez `<principal_id>` par l’ID principal de l’utilisateur ou de l’utilisatrice dont vous souhaitez supprimer les données.

   ```sql
   Delete from EdcPrincipalLocalAccountEntity where refuserprincipalid in (Select id from EdcPrincipalUserEntity where refprincipalid in (select id from EdcPrincipalEntity where id='<principal_id>'));
   
   Delete from EdcPrincipalEmailAliasEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalRoleEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPriResPrmEntity where refprinid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalUserEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalMappingEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalGrpCtmntEntity where refchildprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalEntity where id='<principal_id>';
   ```

1. Démarrez AEM Forms Server.

### Référentiel AEM {#aem-repository-1}

Les utilisateurs et les utilisatrices de Forms JEE disposent de leurs données dans le référentiel AEM s’ils ont accédé au moins une fois à l’instance de création AEM Forms. Vous pouvez accéder à leurs données utilisateur et les supprimer du référentiel AEM.

#### Accès aux données utilisateur {#access-user-data}

Pour afficher un utilisateur créé dans le référentiel AEM, connectez-vous à `https://'[server]:[port]'/lc/useradmin` à l’aide des informations d’identification de l’administrateur AEM. Notez que les valeurs `server` et `port` indiquées dans l’URL sont celles de l’instance d’auteur AEM. Ici, vous pouvez rechercher des utilisateurs et des utilisatrices avec leur nom d’utilisateur ou d’utilisatrice. Double-cliquez sur un utilisateur ou une utilisatrice pour afficher des informations telles que les propriétés, les autorisations et les groupes de l’utilisateur ou de l’utilisatrice. La propriété `Path` d’un utilisateur indique le chemin d’accès au nœud d’utilisateur créé dans le référentiel AEM.

#### Suppression de données utilisateur {#delete-aem}

Pour supprimer un utilisateur ou une utilisatrice :

1. Accédez à `https://'[server]:[port]'/lc/useradmin` à lʼaide des informations d’identification de lʼadministrateur AEM.
1. Recherchez un utilisateur et cliquez deux fois sur le nom d’utilisateur pour ouvrir ses propriétés. Copiez la propriété `Path`.
1. Accédez à AEM CRXDE Lite à l’adresse `https://'[server]:[port]'/lc/crx/de/index.jsp`, puis accédez ou recherchez le chemin d’accès de l’utilisateur ou de l’utilisatrice.
1. Supprimez le chemin d’accès et cliquez sur **[!UICONTROL Enregistrer tout]** pour supprimer définitivement l’utilisateur ou l’utilisatrice du référentiel AEM.
