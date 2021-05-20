---
title: Document Security | Gestion des données utilisateur
seo-title: Document Security | Gestion des données utilisateur
description: Document Security | Gestion des données utilisateur
uuid: 1624a465-8b0c-4347-a53f-1118bfa6e18f
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 898268cb-4426-421f-8f63-d75bd85cb57f
role: Administrator
exl-id: 00c01a12-1180-4f35-9179-461bf177c787
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '953'
ht-degree: 59%

---

# Document Security | Gestion des données utilisateur {#document-security-handling-user-data}

AEM Forms Document Security vous permet de créer, de stocker et d’appliquer des paramètres de sécurité prédéfinis à vos documents. Cela garantit que seuls les utilisateurs autorisés peuvent utiliser les documents. Vous pouvez protéger les documents à l’aide de stratégies. Une stratégie est un groupe d’informations comprenant des paramètres de sécurité et une liste d’utilisateurs autorisés. Vous pouvez appliquer une stratégie à un ou plusieurs documents et autoriser des utilisateurs ajoutés dans le composant User Management d’AEM Forms JEE.

<!-- Fix broken link For more information about how document security works, see AEM Forms JEE administration help. -->

## Données utilisateur et stockage de données {#user-data-and-data-stores}

Document Security stocke des stratégies et des données associées à des documents protégés, notamment des données utilisateur stockées dans une base de données telle que MySQL, Oracle, MS SQL Server et IBM DB2. Par ailleurs, les données des utilisateurs autorisés sont stockées dans une stratégie dans User Management. Pour plus d’informations sur les données stockées dans la gestion des utilisateurs, voir [Gestion utilisateur de Forms : Gestion des données utilisateur](/help/forms/using/user-management-handling-user-data.md).

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
   <td>Stocke des informations sur la révocation et la restauration de documents protégés.</td>
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
   <td>Stocke des fichiers XML pour les stratégies actives. Une stratégie XML<sup> </sup>contient des références aux ID principaux des utilisateurs associés à la stratégie. La stratégie XML est stockée en tant qu’objet Blob.</td>
  </tr>
  <tr>
   <td><code>EdcPolicyArchiveEntity</code></td>
   <td>Stocke des informations sur les stratégies archivées. Une stratégie archivée contient sa stratégie XML stockée en tant qu’objet Blob.</td>
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

## Accès et suppression des données utilisateur  {#access-and-delete-user-data}

Vous pouvez accéder et exporter les données de Document Security pour les utilisateurs dans les bases de données et, si nécessaire, les supprimer définitivement.

Pour exporter ou supprimer des données utilisateur d’une base de données, vous devez vous connecter à la base de données à l’aide d’un client de base de données et rechercher l’ID principal en fonction des informations d’identification personnelle de l’utilisateur. Par exemple, pour récupérer l’ID principal d’un utilisateur à l’aide d’un ID de connexion, exécutez la commande `select` suivante sur la base de données.

Dans la commande `select`, remplacez `<user_login_id>` par l&#39;identifiant de connexion de l&#39;utilisateur dont vous souhaitez récupérer l&#39;identifiant principal à partir de la table de base de données `EdcPrincipalUserEntity`.

```sql
select refprincipalid from EdcPrincipalUserEntity where uidstring = <user_login_id>
```

Une fois que vous connaissez l’ID principal, vous pouvez exporter ou supprimer les données de l’utilisateur.

### Exportation des données utilisateur  {#export-user-data}

Exécutez les commandes de base de données suivantes pour exporter les données utilisateur d’un ID principal à partir des tables de base de données. Dans la commande `select`, remplacez `<principal_id>` par l’ID principal de l’utilisateur dont vous souhaitez exporter les données.

>[!NOTE]
>
>Les commandes suivantes utilisent des noms de tables de base de données dans les bases de données MySQL et IBM DB2. Lors de l’exécution de ces commandes sur les bases de données Oracle et MS SQL, remplacez `EdcPolicySetPrincipalEntity` par `EdcPolicySetPrincipalEnt` dans les commandes.

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
>Pour exporter des données de la table `EdcAuditEntity`, utilisez l’API [EventManager.exportEvents](https://helpx.adobe.com/experience-manager/6-5/forms/programlc/javadoc/index.html?com/adobe/livecycle/rightsmanagement/client/EventManager.html) qui utilise [EventSearchFilter](https://helpx.adobe.com/experience-manager/6-5/forms/programlc/javadoc/com/adobe/livecycle/rightsmanagement/client/infomodel/EventSearchFilter.html) comme paramètre pour exporter les données d’audit en fonction de `principalId`, `policyId` ou `licenseId`.

Pour obtenir des informations complètes sur un utilisateur du système, vous devez accéder et exporter les données de la base de données User Management. Pour plus d’informations, voir [Gestion des utilisateurs de Forms : Gestion des données utilisateur](/help/forms/using/user-management-handling-user-data.md).

### Suppression de données utilisateur {#delete-user-data}

Procédez comme suit pour supprimer les données de Document Security pour un ID principal des tables de la base de données.

1. Arrêtez le serveur AEM Forms.
1. Exécutez les commandes de base de données suivantes pour supprimer les données de l’ID principal des tables de base de données pour Document Security. Dans la commande `Delete`, remplacez `<principal_id>` par l’ID principal de l’utilisateur dont vous souhaitez supprimer les données.

   ```sql
   Delete from EdcPrincipalKeyEntity where principalid = '<principal_id>';
   
   Delete from EdcMyPolicyListEntity where principalId = '<principal_id>';
   
   Delete from edcpolicyarchiveentity where policyownerId = '<principal_id>';
   
   Delete from edcpolicysetprincipalentity where principalId = '<principal_id>';
   
   Delete from edcinviteduserentity where principalId = '<principal_id>';
   ```

   >[!NOTE]
   >
   >Pour supprimer des données de la table `EdcAuditEntity`, utilisez l’API [EventManager.deleteEvents](https://helpx.adobe.com/experience-manager/6-5/forms/programlc/javadoc/index.html?com/adobe/livecycle/rightsmanagement/client/EventManager.html) qui utilise [EventSearchFilter](https://helpx.adobe.com/experience-manager/6-5/forms/programlc/javadoc/com/adobe/livecycle/rightsmanagement/client/infomodel/EventSearchFilter.html) comme paramètre pour supprimer les données d’audit en fonction de `principalId`, `policyId` ou `licenseId`.

1. Les fichiers XML de stratégie principal et archivés sont stockés dans les tables de base de données `EdcPolicyXmlEntity` et `EdcPolicyArchiveEntity`, respectivement. Pour supprimer les données d’un utilisateur de ces tables, procédez comme suit :

   1. Ouvrez l’objet Blob XML de chaque ligne dans le tableau `EdcPolicyXMLEntity` ou `EdcPolicyArchiveEntity` et extrayez le fichier XML. Le fichier XML ressemble à l’un des fichiers ci-dessous.
   1. Modifiez le fichier XML pour supprimer l’objet Blog de l’ID principal.
   1. Répétez les étapes 1 et 2 pour l’autre fichier.

   >[!NOTE]
   >
   >Vous devez supprimer l’objet blob complet dans la balise `Principal` d’un ID principal ou le code XML de la stratégie peut être corrompu ou inutilisable.

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

   1. En tant qu’administrateur, connectez-vous à la console d’administration de Forms JEE à l’adresse https://[*server*]:[*port*]/adminui.
   1. Accédez à **[!UICONTROL Services > Document Security > Jeux de stratégies]**.
   1. Ouvrez un jeu de stratégies et supprimez l’utilisateur de la stratégie.

   **Utilisation d’une page Web Document Security**

   Les utilisateurs de Document Security détenant les autorisations nécessaires pour créer des stratégies personnelles peuvent supprimer des données utilisateur de leurs stratégies. Pour ce faire :

   1. Les utilisateurs qui disposent de stratégies personnelles se connectent à leur page Web Document Security à l’adresse https://[*server*]:[*port*]/edc.
   1. Accédez à **[!UICONTROL Services > Document Security > Mes stratégies]**.
   1. Ouvrez une stratégie et supprimez l’utilisateur de la stratégie.

   >[!NOTE]
   >
   >Les administrateurs peuvent rechercher, accéder et supprimer des données utilisateur des stratégies personnelles d’autres utilisateurs dans **[!UICONTROL Services > Document Security > Mes stratégies]** à l’aide de la console d’administration.

1. Supprimez les données de l’ID principal de la base de données User Management. Pour obtenir des instructions détaillées, voir [Gestion utilisateur de Forms | Gestion des données utilisateur](/help/forms/using/user-management-handling-user-data.md).
1. Démarrez le serveur AEM Forms.
