---
title: User Management Forms | Gestion des données utilisateur
seo-title: User Management Forms | Gestion des données utilisateur
description: User Management Forms | Gestion des données utilisateur
uuid: 2b76b69f-6f3a-4f1a-a2a4-d39f5e529f75
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a88fc933-f1af-4798-b72f-10e7b0d2fd11
role: Administrator
exl-id: eeeab5d1-073a-4e13-a781-391dfe70bb37
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 81%

---

# User Management Forms | Gestion des données utilisateur {#forms-user-management-handling-user-data}

User Management est un composant d’AEM Forms JEE qui permet de créer, de gérer et d’autoriser les utilisateurs AEM Forms à accéder à AEM Forms. User Management utilise des domaines en tant que répertoire pour obtenir des informations sur les utilisateurs. Les types de domaine suivants sont pris en charge :

**Domaines locaux** : ce type de domaine n’est pas connecté à un système de stockage tiers. En effet, les utilisateurs et les groupes sont créés localement et résident dans la base de données User Management. Les mots de passe sont stockés localement et l’authentification est effectuée par le biais d’une base de données locale.

**Domaines hybrides** : ce type de domaine n’est pas connecté à un système de stockage tiers. En effet, les utilisateurs et les groupes sont créés localement et résident dans la base de données User Management. A la différence des domaines locaux, les domaines hybrides utilisent un fournisseur d’authentification externe, pouvant être LDAP, Kerberos, SAML ou un fournisseur d’authentification personnalisé.

**Domaines d’entreprise** : ils sont constitués d’utilisateurs et de groupes résidant dans un système de stockage tiers, tel qu’un annuaire LDAP. User Management n’a pas la possibilité d’écrire dans le système de stockage tiers, mais assure la synchronisation des informations relatives aux utilisateurs et aux groupes avec sa propre base de données. Les domaines d’entreprise utilisent également un fournisseur d’authentification externe pouvant être LDAP, Kerberos, SAML ou un fournisseur d’authentification personnalisé.

<!-- Fix broken links For more information about how user management works and configured, see AEM Forms JEE administration help. -->

## Données utilisateur et stockage de données {#user-data-and-data-stores}

User Management stocke des données utilisateur dans une base de données telle que MySQL, Oracle, MS SQL Server et IBM DB2. En outre, tout utilisateur qui s’est connecté au moins une fois dans des applications Forms sur AEM auteur à l’adresse `https://'[server]:[port]'lc`, l’utilisateur est créé dans AEM référentiel. User Management est donc enregistré dans les stockages de données suivants :

* Base de données
* Référentiel AEM
* Stockage tiers tel qu’un annuaire LDAP

>[!NOTE]
>
>Les données stockées dans des stockages tiers ne sont pas prises en charge pour ce document. Contactez directement le fournisseur tiers pour gérer les données utilisateur dans ces stockages.

### Base de données {#database}

User Management stocke les données utilisateur dans les tables de base de données suivantes :

<table>
 <tbody>
  <tr>
   <td>Table de base de données</td>
   <td>Description</td>
  </tr>
  <tr>
   <td><code>EdcPrincipalEntity</code></td>
   <td><p>Stocke des informations sur les entités principales. L’entité Principal peut correspondre à un utilisateur, un groupe ou un rôle.</p> <p> </p> </td>
  </tr>
  <tr>
   <td><code>EdcPrincipalUserEntity</code></td>
   <td>Stocke des informations d’identification personnelle des utilisateurs. Il contient une entrée pour chaque utilisateur de domaines locaux, d’entreprise et hybrides.</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalLocalAccountEntity</code></p> <p><code class="code">EdcPrincipalLocalAccount
       </code>(bases de données Oracle et MS SQL)</p> </td>
   <td>Stocke les données uniquement pour les utilisateurs locaux.</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalEmailAliasEntity</code></p> <p><code class="code">EdcPrincipalEmailAliasEn
       </code>(bases de données Oracle et MS SQL)</p> </td>
   <td>Il contient des entrées pour tous les utilisateurs de domaines locaux, d’entreprise et hybrides. Il contient des ID de courrier électronique d’utilisateur.</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalGrpCtmntEntity</code></p> <p><code>EdcPrincipalGrpCtmntEnti</code> (bases de données Oracle et MS SQL)</p> </td>
   <td>Stocke le mappage entre les utilisateurs et les groupes.</td>
  </tr>
  <tr>
   <td><code>EdcPrincipalRoleEntity</code></td>
   <td>Stocke le mappage entre les rôles et l’entité Principal pour les utilisateurs et les groupes.</td>
  </tr>
  <tr>
   <td><code>EdcPriResPrmEntity</code></td>
   <td>Stocke le mappage entre l’entité Principal et les autorisations pour les utilisateurs et les groupes.</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalMappingEntity</code></p> <p><code>EdcPrincipalMappingEntit</code> (bases de données Oracle et MS SQL)</p> </td>
   <td>Stocke les anciennes et nouvelles valeurs d’attribut associées à une entité Principal.<br /> </td>
  </tr>
 </tbody>
</table>

### Référentiel AEM  {#aem-repository}

Les données de gestion des utilisateurs pour les utilisateurs qui ont accédé au moins une fois aux applications Forms sous `https://'[server]:[port]'lc` sont également stockées dans le référentiel AEM.

## Accès et suppression des données utilisateur  {#access-and-delete-user-data}

Vous pouvez accéder et exporter les données User Management pour les utilisateurs dans les bases de données User Management et, si nécessaire, les supprimer définitivement.

### Base de données  {#database-1}

Pour exporter ou supprimer des données utilisateur d’une base de données User Management, vous devez vous connecter à la base de données à l’aide d’un client de base de données et rechercher l’ID principal en fonction des informations d’identification personnelle de l’utilisateur. Par exemple, pour récupérer l’ID principal d’un utilisateur à l’aide d’un ID de connexion, exécutez la commande `select` suivante sur la base de données.

Dans la commande `select`, remplacez `<user_login_id>` par l’ID de connexion de l’utilisateur dont vous souhaitez récupérer l’ID principal.

```sql
select refprincipalid from EdcPrincipalUserEntity where uidstring = <user_login_id>
```

Une fois que vous connaissez l’ID principal, vous pouvez exporter ou supprimer les données de l’utilisateur.

#### Exportation des données utilisateur  {#export-user-data}

Exécutez les commandes de base de données suivantes pour exporter les données User Management d’un ID principal à partir des tables de base de données. Dans la commande `select`, remplacez `<principal_id>` par l’ID principal de l’utilisateur dont vous souhaitez exporter les données.

>[!NOTE]
>
>Les commandes suivantes utilisent des noms de tables de base de données dans les bases de données MySQL et IBM DB2. Lors de l’exécution de ces commandes sur les bases de données Oracle et MS SQL, remplacez les noms de table suivantes dans les commandes :
>
>* Remplacer `EdcPrincipalLocalAccountEntity` par `EdcPrincipalLocalAccount`
   >
   >
* Remplacer `EdcPrincipalEmailAliasEntity` par `EdcPrincipalEmailAliasEn`
   >
   >
* Remplacer `EdcPrincipalMappingEntity` par `EdcPrincipalMappingEntit`
   >
   >
* Remplacer `EdcPrincipalGrpCtmntEntity` par `EdcPrincipalGrpCtmntEnti`

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

Procédez comme suit pour supprimer les données User Management pour un ID principal des tables de base de données.

1. Supprimez les données utilisateur du référentiel AEM, le cas échéant, comme indiqué dans la section [Suppression de données utilisateur](/help/forms/using/user-management-handling-user-data.md#delete-aem).
1. Arrêtez le serveur AEM Forms.
1. Exécutez les commandes de base de données suivantes pour supprimer les données User Management d’un ID principal à partir des tables de base de données. Dans la commande `Delete`, remplacez `<principal_id>` par l’ID principal de l’utilisateur dont vous souhaitez supprimer les données.

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

1. Démarrez le serveur AEM Forms.

### Référentiel AEM  {#aem-repository-1}

Les données des utilisateurs Forms JEE se trouvent dans le référentiel AEM s’ils ont accédé à l’instance d’auteur AEM Forms au moins une fois. Vous pouvez accéder et supprimer des données utilisateur d’un référentiel AEM.

#### Accès aux données utilisateur  {#access-user-data}

Pour afficher l’utilisateur créé dans AEM référentiel, connectez-vous à `https://'[server]:[port]'/lc/useradmin` avec les informations d’identification d’administrateur AEM. Notez que les valeurs `server` et `port` indiquées dans l’URL sont celles de l’instance d’auteur AEM. Ici, vous pouvez rechercher des utilisateurs avec leur nom d’utilisateur. Cliquez deux fois sur un utilisateur pour afficher des informations telles que les propriétés, les autorisations et les groupes de l’utilisateur. La propriété `Path` d’un utilisateur indique le chemin d’accès au nœud d’utilisateur créé dans le référentiel AEM.

#### Suppression de données utilisateur {#delete-aem}

Pour supprimer un utilisateur :

1. Accédez à `https://'[server]:[port]'/lc/useradmin` avec les informations d’identification AEM administrateur.
1. Recherchez un utilisateur et cliquez deux fois sur le nom d’utilisateur pour ouvrir ses propriétés. Copiez la propriété `Path` .
1. Accédez à AEM CRX DELite à l’adresse `https://'[server]:[port]'/lc/crx/de/index.jsp` et recherchez ou recherchez le chemin d’accès de l’utilisateur.
1. Supprimer le chemin d’accès et cliquez sur **[!UICONTROL Enregistrer tout]** pour supprimer définitivement l’utilisateur du référentiel AEM.
