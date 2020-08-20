---
title: Portail Forms| Gestion des données utilisateur
seo-title: Portail Forms| Gestion des données utilisateur
description: 'null'
seo-description: 'null'
uuid: 2ac2b2a9-b603-489a-86b8-a78b697f130d
contentOwner: vishgupt
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 48f841b7-0e7f-4216-9ee8-fb6e843acaf0
translation-type: tm+mt
source-git-commit: 4e0709031aca030e50840811a9b3717f3cb20340
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 64%

---


# Portail Forms| Gestion des données utilisateur {#forms-portal-handling-user-data}

[!DNL AEM Forms] Portal fournit des composants que vous pouvez utiliser pour liste des formulaires adaptatifs, des formulaires HTML5 et d’autres ressources Forms sur [!DNL AEM Sites] la page. Vous pouvez également le configurer pour qu’il affiche les formulaires adaptatifs sous forme de brouillons et envoyés ainsi que les formulaires HTML5 d’un utilisateur connecté. For more information about forms portal, see [Introduction to publishing forms on a portal](/help/forms/using/introduction-publishing-forms.md).

Lorsqu’un utilisateur connecté enregistre un formulaire adaptatif en tant que brouillon ou l’envoie, il s’affiche dans les onglets Brouillons et Envois sur le portail Forms. Les données des formulaires sous forme de brouillons ou envoyés sont stockées dans le stockage de données configuré pour le déploiement AEM. Les brouillons et les envois des utilisateurs anonymes ne sont pas affichés sur la page du portail Forms, cependant les données sont stockées dans le stockage de données configuré. Pour plus d’informations, voir [Configuration des services de stockage pour les brouillons et les envois](/help/forms/using/configuring-draft-submission-storage.md).

## Données utilisateur et stockage de données {#user-data-and-data-stores}

Le portail Forms stocke les données des formulaires sous forme de brouillons et envoyés dans les cas suivants :

* L’action d’envoi configurée dans le formulaire adaptatif est **Action d’envoi du portail Forms**.
* For submit actions other than **Forms Portal Submit Action**, the **[!UICONTROL Store data in forms portal]** option is enabled in the **[!UICONTROL Submission]** properties of the adaptive form container.

Pour chaque formulaire sous forme de brouillon et envoyé pour des utilisateurs connectés et anonymes, le portail Forms stocke les données suivantes :

* Métadonnées de formulaire telles que le nom du formulaire, le chemin d’accès au formulaire, l’ID de brouillon ou d’envoi, le chemin d’accès aux pièces jointes et l’ID des données utilisateur
* Pièce jointe au formulaire en tant qu’octets de données
* Données de formulaire en tant qu’octets de données

Selon la persistance du stockage de données configuré, les données de formulaires sous forme de brouillons et envoyés sont stockées aux emplacements suivants.

<table>
 <tbody>
  <tr>
   <td><p><strong>Type de persistance</strong></p> </td>
   <td><p><strong>Stockage de données</strong></p> </td>
   <td><p><strong>Emplacement</strong></p> </td>
  </tr>
  <tr>
   <td><p>Valeur par défaut</p> </td>
   <td><p>Référentiel AEM d’instances d’auteur et de publication</p> </td>
   <td><p><code>/content/forms/fp/</code></p> </td>
  </tr>
  <tr>
   <td><p>Distant</p> </td>
   <td><p>Référentiel AEM d’instances d’auteur et distantes</p> </td>
   <td><p><code>/content/forms/fp/</code></p> </td>
  </tr>
  <tr>
   <td><p>Base de données</p> </td>
   <td><p>Référentiel AEM d’instances d’auteur et de tables de base de données</p> </td>
   <td>Tables de base de données <code>data</code>, <code>metadata</code>et <code>additionalmetadata</code></td>
  </tr>
 </tbody>
</table>

## Accès et suppression des données utilisateur {#access-and-delete-user-data}

Vous pouvez accéder aux données de formulaires envoyés et sous forme de brouillons pour des utilisateurs connectés et anonymes dans les stockages de données configurés et, si nécessaire, les supprimer.

### Instances AEM {#aem-instances}

All drafts and submitted forms data in AEM instances (author, publish, or remote) for logged-in and anonymous users are stored in the `/content/forms/fp/` node of the applicable AEM repository. Chaque fois qu’un utilisateur connecté ou anonyme enregistre un formulaire en tant que brouillon ou l’envoie, un `draft ID` ou un `submission ID`, un `user data ID`, et un `ID` aléatoire pour chaque pièce jointe (le cas échéant) sont générés et associés au brouillon ou à l’envoi correspondant.

#### Accès aux données utilisateur {#access-user-data}

Lorsqu’un utilisateur connecté enregistre un formulaire en tant que brouillon ou l’envoie, un nœud enfant est créé avec son ID utilisateur. For example, drafts and submissions data for Sarah Rose whose user ID is `srose` are stored in `/content/forms/fp/srose/` node in AEM repository. Dans le nœud de l’ID utilisateur, les données sont organisées dans une structure hiérarchique.

The following table explains how the data for all drafts by `srose` is stored in AEM repository.

>[!NOTE]
>
>An exact structure like `drafts` is replicated for submitted forms for `srose` under the `/content/forms/fp/srose/submit/` node.
>
>All drafts and submissions by `anonymous` users are stored under the `/content/forms/fp/anonymous/` node, which organizes drafts and submissions for all anonymous users under the `draft` and `submit` nodes.

| Node | Description |
|---|---|
| `/content/forms/fp/srose/drafts` | Données de nœud de conteneur pour tous les brouillons de l’utilisateur |
| `/content/forms/fp/srose/drafts/attachments/` | Range toutes les pièces jointes de l’utilisateur en fonction de l’ID du brouillon |
| `/content/forms/fp/srose/drafts/attachments/<ID>` | Contient la pièce jointe de l’ID sélectionné au format binaire |
| `/content/forms/fp/srose/drafts/metadata/` | Organise les métadonnées de formulaire pour l’utilisateur en fonction de l’ID de brouillon. |
| `/content/forms/fp/srose/drafts/metadata/<draft ID>` | Contient les métadonnées de formulaire de l’ID de brouillon sélectionné |
| `/content/forms/fp/srose/drafts/data/` | Range les données de formulaire de l’utilisateur en fonction de l’ID de données utilisateur |
| `/content/forms/fp/srose/drafts/data/<user data ID>` | Contient les données de formulaire pour l’ID de données utilisateur sélectionné au format binaire |

#### Suppression de données utilisateur {#delete-user-data}

Pour supprimer définitivement des données utilisateur des brouillons et des envois dans les systèmes AEM pour un utilisateur connecté, vous devez supprimer le nœud `user ID` pour un utilisateur spécifique à partir du nœud d’auteur. Vous devez supprimer manuellement les données de toutes les instances AEM applicables.

Drafts and submission data for all anonymous users is stored within the common `drafts` and `submit` nodes under `/content/forms/fp/anonymous`. Il n&#39;existe aucune méthode pour rechercher des données pour un utilisateur anonyme particulier à moins que certaines informations identifiables ne soient connues. Dans ce cas, vous pouvez rechercher les informations qui identifient l’utilisateur anonyme dans AEM référentiel et supprimer manuellement le noeud qui le contient de toutes les instances AEM applicables afin de supprimer les données du système AEM. However, to delete data for all anonymous users, you can delete the `anonymous` node to remove drafts and submissions data for all anonymous users.

### Base de données {#database}

Lorsqu’AEM est configuré pour stocker des données dans une base de données, les données de brouillon et d’envoi du portail Forms sont stockées dans les tables de base de données suivantes pour les utilisateurs connectés et anonymes :

* data
* metadata
* additionalmetadata

#### Accès aux données utilisateur {#access-user-data-1}

Pour accéder aux données de brouillons et d’envois pour un utilisateur connecté et anonyme dans les tables de base de données, exécutez la commande de base de données suivante. In the query, replace `logged-in user` with the user ID whose data you want to access or with `anonymous` for anonymous users.

```sql
select * from metadata, data, additionalmetadatatable where metadata.owner = 'logged-in user' and metadata.id = additionalmetadatatable.id and metadata.userdataID = data.id
```

#### Suppression de données utilisateur {#delete-user-data-1}

Pour supprimer les données de brouillons et d’envois d’un utilisateur connecté dans les tables de base de données, exécutez la commande de base de données suivante : In the query, replace `logged-in user` with the user ID whose data you want to delete or with `anonymous` for anonymous users. Notez que pour supprimer les données d’un utilisateur anonyme particulier dans la base de données, vous devez le trouver à l’aide d’informations d’identification et le supprimer des tables de base de données contenant ces informations.

```sql
DELETE FROM metadata, data, additionalmetadatatable USING metadata INNER JOIN data ON metadata.userdataID = data.id INNER JOIN additionalmetadatatable ON metadata.id = additionalmetadatatable.id WHERE metadata.owner = 'logged-in user'
```

