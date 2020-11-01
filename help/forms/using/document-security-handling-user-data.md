---
title: Document Security | Gestion des données utilisateur
seo-title: Document Security | Gestion des données utilisateur
description: Sécurité du document | Gestion des données utilisateur
uuid: 1624a465-8b0c-4347-a53f-1118bfa6e18f
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 898268cb-4426-421f-8f63-d75bd85cb57f
translation-type: tm+mt
source-git-commit: a873cf3e7efd3bc9cd4744bf09078d9040efcdda
workflow-type: tm+mt
source-wordcount: '953'
ht-degree: 59%

---


# Document Security | Gestion des données utilisateur {#document-security-handling-user-data}

La sécurité des documents AEM Forms vous permet de créer, stocker et appliquer des paramètres de sécurité prédéfinis à vos documents. Cela garantit que seuls les utilisateurs autorisés peuvent utiliser les documents. Vous pouvez protéger les documents à l’aide de stratégies. Une stratégie est un groupe d’informations comprenant des paramètres de sécurité et une liste d’utilisateurs autorisés. Vous pouvez appliquer une stratégie à un ou plusieurs documents et autoriser des utilisateurs ajoutés dans le composant User Management d’AEM Forms JEE.

<!-- Fix broken link For more information about how document security works, see AEM Forms JEE administration help. -->

## Données utilisateur et stockage de données {#user-data-and-data-stores}

Document Security stocke des stratégies et des données associées à des documents protégés, notamment des données utilisateur stockées dans une base de données telle que MySQL, Oracle, MS SQL Server et IBM DB2. Par ailleurs, les données des utilisateurs autorisés sont stockées dans une stratégie dans User Management. For information about data stored in user management, see [Forms User Management: Handling user data](/help/forms/using/user-management-handling-user-data.md).

Le tableau suivant montre comment Document Security organise les données dans les tables de base de données.

<table>
 <tbody>
  <tr>
   <td>Table de base de données</td>
   <td>Description</td>
  </tr>
  <tr>
   <td><code>EdcPrincipalKeyEntity</code></td>
   <td>Stocke des informations sur les clés principales des utilisateurs. Les clés sont utilisées dans les flux de travail de Document Security hors ligne.</td>
  </tr>
  <tr>
   <td><code>EdcAuditEntity</code></td>
   <td>Stocke des informations sur les événements de contrôle tels que les événements utilisateur, les événements de document et les événements de stratégie.</td>
  </tr>
  <tr>
   <td><p><code>EdcLicenseEntity</code></p> </td>
   <td>Stocke l’enregistrement d’un document protégé. Il stocke des informations de licence pour chaque document protégé.</td>
  </tr>
  <tr>
   <td><p><code>EdcDocumentEntity</code></p> </td>
   <td>Stocke le nom du document pour chaque licence créée dans le système.</td>
  </tr>
  <tr>
   <td><p><code>EdcRevokationEntity</code></p> </td>
   <td>Stocke des informations sur la révocation et la réintégration des documents protégés.</td>
  </tr>
  <tr>
   <td><code>EdcMyPolicyListEntity</code></td>
   <td>Stocke des informations sur les utilisateurs qui peuvent créer des stratégies personnelles qui apparaissent sous l’onglet Mes stratégies sur la page Stratégies. </td>
  </tr>
  <tr>
   <td><code>EdcPolicyEntity</code></td>
   <td>Stocke des informations sur les stratégies. Chaque stratégie correspond à une ligne dans le tableau ci-dessous.</td>
  </tr>
  <tr>
   <td><code>EdcPolicyXmlEntity</code></td>
   <td>Stocke des fichiers XML pour les stratégies actives. A policy XML<sup> </sup>contains references to principal IDs of users associated with the policy. La stratégie XML est stockée en tant qu’objet Blob.</td>
  </tr>
  <tr>
   <td><code>EdcPolicyArchiveEntity</code></td>
   <td>Stocke des informations sur les stratégies archivées. Une stratégie archivée contient son code XML de stratégie stocké en tant qu’objet Blob.</td>
  </tr>
  <tr>
   <td><p><code>EdcPolicySetPrincipalEntity</code></p> <p><code>EdcPolicySetPrincipalEnt</code> (bases de données Oracle et MS SQL)</p> </td>
   <td>Stocke le mappage entre le jeu de stratégies et les utilisateurs.</td>
  </tr>
  <tr>
   <td><code>EdcInvitedUserEntity</code></td>
   <td>Stocke des informations sur l’utilisateur invité.</td>
  </tr>
 </tbody>
</table>

## Accès et suppression des données utilisateur {#access-and-delete-user-data}

Vous pouvez accéder et exporter les données de Document Security pour les utilisateurs dans les bases de données et, si nécessaire, les supprimer définitivement.

Pour exporter ou supprimer des données utilisateur d’une base de données, vous devez vous connecter à la base de données à l’aide d’un client de base de données et rechercher l’ID principal en fonction des informations d’identification personnelle de l’utilisateur. Par exemple, pour récupérer l’ID principal d’un utilisateur à l’aide d’un ID de connexion, exécutez la commande `select` suivante sur la base de données.

In the `select` command, replace the `<user_login_id>` with the login ID of the user whose principal ID you want to retrieve from the `EdcPrincipalUserEntity` database table.

```sql
select refprincipalid from EdcPrincipalUserEntity where uidstring = <user_login_id>
```

Une fois que vous connaissez l’ID principal, vous pouvez exporter ou supprimer les données de l’utilisateur.

### Exportation des données utilisateur {#export-user-data}

Exécutez les commandes de base de données suivantes pour exporter les données utilisateur d’un ID principal à partir des tables de base de données. In the `select` command, replace `<principal_id>` with the principal ID of the user whose data you want to export.

>[!NOTE]
>
>Les commandes suivantes utilisent des noms de tables de base de données dans les bases de données MySQL et IBM DB2. When running these commands on Oracle and MS SQL databases, replace `EdcPolicySetPrincipalEntity` with `EdcPolicySetPrincipalEnt` in the commands.

```sql
Select * from EdcPrincipalKeyEntity where principalid = '<principal_id>';

Select * from EdcLicenseEntity where publisherId = '<principal_id>';

Select * from EdcDocumentEntity where id in (Select documentid from EdcLicenseEntity where publisherId = '<principal_id>');

Select * from EdcRevokationEntity where licenseid in (Select id from EdcLicenseEntity where publisherId = '<principal_id>');

Select * from EdcMyPolicyListEntity where principalId = '<principal_id>';

Select * from edcpolicyentity where policyownerId = '<principal_id>';

Select * from edcpolicyxmlentity where policyidref in (Select id from edcpolicyentity where policyownerId = '<principal_id>');

Select * from edcpolicyarchiveentity where policyownerId = '<principal_id>';

Select * from edcpolicysetprincipalentity where principalId = '<principal_id>';

Select * from edcinviteduserentity where principalId = '<principal_id>';
```

>[!NOTE]
>
>To export data from the `EdcAuditEntity` table, use the [EventManager.exportEvents](https://helpx.adobe.com/experience-manager/6-5/forms/programlc/javadoc/index.html?com/adobe/livecycle/rightsmanagement/client/EventManager.html) API that takes [EventSearchFilter](https://helpx.adobe.com/experience-manager/6-5/forms/programlc/javadoc/com/adobe/livecycle/rightsmanagement/client/infomodel/EventSearchFilter.html) as a parameter to export audit data based on `principalId`, `policyId`, or `licenseId`.

Pour obtenir des informations complètes sur un utilisateur du système, vous devez accéder et exporter les données de la base de données User Management. For more information, see [Forms user management: Handling user data](/help/forms/using/user-management-handling-user-data.md).

### Suppression de données utilisateur {#delete-user-data}

Procédez comme suit pour supprimer les données de Document Security pour un ID principal des tables de la base de données.

1. Arrêtez le serveur AEM Forms.
1. Exécutez les commandes de base de données suivantes pour supprimer les données de l’ID principal des tables de base de données pour Document Security. In the `Delete` command, replace `<principal_id>` with the principal ID of the user whose data you want to delete.

   ```sql
   Delete from EdcPrincipalKeyEntity where principalid = '<principal_id>';
   
   Delete from EdcMyPolicyListEntity where principalId = '<principal_id>';
   
   Delete from edcpolicyarchiveentity where policyownerId = '<principal_id>';
   
   Delete from edcpolicysetprincipalentity where principalId = '<principal_id>';
   
   Delete from edcinviteduserentity where principalId = '<principal_id>';
   ```

   >[!NOTE]
   >
   >To delete data from the `EdcAuditEntity` table, use the [EventManager.deleteEvents](https://helpx.adobe.com/experience-manager/6-5/forms/programlc/javadoc/index.html?com/adobe/livecycle/rightsmanagement/client/EventManager.html) API that takes [EventSearchFilter](https://helpx.adobe.com/experience-manager/6-5/forms/programlc/javadoc/com/adobe/livecycle/rightsmanagement/client/infomodel/EventSearchFilter.html) as a parameter to delete audit data based on `principalId`, `policyId`, or `licenseId`.

1. Active and archived policy XML files are stored in the `EdcPolicyXmlEntity` and `EdcPolicyArchiveEntity` database tables, respectively. Pour supprimer les données d’un utilisateur de ces tables, procédez comme suit :

   1. Open the XML blob of each row in the `EdcPolicyXMLEntity` or `EdcPolicyArchiveEntity` table and extract the XML file. Le fichier XML ressemble à l’un des fichiers ci-dessous.
   1. Modifiez le fichier XML pour supprimer l’objet Blog de l’ID principal.
   1. Répétez les étapes 1 et 2 pour l’autre fichier.

   >[!NOTE]
   >
   >You must remove the complete blob within the `Principal` tag for a principal ID or the policy XML may get corrupt or unusable.

   ```xml
   <ns2:Principal PrincipalNameType="USER">
       <ns2:PrincipalDomain>OID</ns2:PrincipalDomain>
       <ns2:PrincipalName>56F33FEB-098A-1036-A651-00000A2A2656</ns2:PrincipalName>
   </ns2:Principal>
   </ns2:PolicyEntry>
       <ns2:Property PropertyName="isCertified">
           <ns2:PropertyValue xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xmlns:xs="https://www.w3.org/2001/XMLSchema" xsi:type="xs:string">false</ns2:PropertyValue>
       </ns2:Property>
       <ns2:Property PropertyName="encryptionAlgorithm">
           <ns2:PropertyValue xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xmlns:xs="https://www.w3.org/2001/XMLSchema" xsi:type="xs:string">AES128</ns2:PropertyValue>
       </ns2:Property>
       <ns2:Property PropertyName="AccessDeniedErrorMessage">
           <ns2:PropertyValue xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xmlns:xs="https://www.w3.org/2001/XMLSchema" xsi:type="xs:string"></ns2:PropertyValue>
       </ns2:Property>
   <ns2:PolicyEntry>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.onlineOpen" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.copy" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.offlineOpen" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.accessible" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.editNotes" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.edit" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.fillAndSign" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.printHigh" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.printLow" Access="ALLOW"/>
   ```

   Outre la suppression des données directement à partir de la table `EdcPolicyXmlEntity`, vous pouvez également utiliser les deux méthodes suivantes :

   **Utilisation de la console d’administration**

   1. As an administrator, log into the Forms JEE administration console at https://[*server*]:[*port*]/adminui.
   1. Navigate to **[!UICONTROL Services > Document Security > Policy Sets]**.
   1. Ouvrez un jeu de stratégies et supprimez l’utilisateur de la stratégie.

   **Utilisation d’une page Web Document Security**

   Les utilisateurs de Document Security détenant les autorisations nécessaires pour créer des stratégies personnelles peuvent supprimer des données utilisateur de leurs stratégies. Pour ce faire :

   1. Users who have personal policies log into their document security web page at https://[*server*]:[*port*]/edc.
   1. Navigate to **[!UICONTROL Services > Document Security > My Policies]**.
   1. Ouvrez une stratégie et supprimez l’utilisateur de la stratégie.

   >[!NOTE]
   >
   >Administrators can search, access, and delete user data from personal policies of other users in **[!UICONTROL Services > Document Security > My Policies]** using administration console.

1. Supprimez les données de l’ID principal de la base de données User Management. For detailed steps, see [Forms User Management | Handling user data](/help/forms/using/user-management-handling-user-data.md).
1. Démarrez le serveur AEM Forms.

