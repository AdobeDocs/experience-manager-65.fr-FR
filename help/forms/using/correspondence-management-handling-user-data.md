---
title: Correspondence Management | Gestion des données utilisateur
description: Découvrez Correspondence Management et la gestion des données utilisateur dans un environnement Adobe Experience Manager Forms.
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
role: Admin,User
exl-id: a0c6a02c-47a3-4e70-a14c-953ee016b8e4
solution: Experience Manager, Experience Manager Forms
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 100%

---

# Correspondence Management | Gestion des données utilisateur {#correspondence-management-handling-user-data}

AEM Forms Correspondence Management vous permet de créer, gérer et rationaliser les correspondances clientes sécurisées et personnalisées. Il fournit une interface utilisateur intuitive permettant aux utilisateurs et utilisatrices professionnels de créer des correspondances à l’aide de blocs de contenu et d’éléments multimédias pré-approuvés. Pour obtenir plus d’informations sur la création de correspondances, reportez-vous à la section [Créer une correspondance](/help/forms/using/create-correspondence.md).

Lorsque des utilisateurs ou utilisatrices professionnels ou des agentes ou agents enregistrent une correspondance en tant que brouillon ou la soumettent, une instance de lettre est enregistrée dans le référentiel AEM. L’instance de lettre comprend des données de correspondance et des métadonnées.

>[!NOTE]
>
>Dans AEM 6.5 Forms, la gestion des correspondances n’est pas disponible hors champ. Si vous effectuez une mise à niveau à partir d’une version précédente d’AEM Forms, installez le package de compatibilité et migrez vos actifs Correspondence Management pour continuer à les utiliser dans AEM 6.5 Forms. Pour plus d’informations, reportez-vous à la section [Package de compatibilité](/help/forms/using/compatibility-package.md).

## Données utilisateur et stockage de données {#data}

Correspondence Management stocke les données des brouillons et des lettres soumises dans le référentiel AEM uniquement si l’instance de publication est configurée pour gérer les instances de lettre. Pour plus d’informations sur la configuration, voir [Propriétés de configuration de Correspondence Management](/help/forms/using/cm-configuration-properties.md).

En fonction de la persistance du magasin de données configuré pour votre déploiement AEM, les brouillons et les données de correspondance soumises sont stockés aux emplacements suivants.

<table>
 <tbody>
  <tr>
   <td><p><strong>Type de persistance</strong></p> </td>
   <td><p><strong>Stockage de données</strong></p> </td>
   <td><p><strong>Emplacement</strong></p> </td>
  </tr>
  <tr>
   <td><p>Valeur par défaut</p> </td>
   <td><p>Référentiel AEM des instances de publication et des instances de création spécifiées dans la configuration de réplication inverse</p> </td>
   <td><p><code>/content/apps/cm/letterInstances/[yyyy]/[mm]/[dd]/[node-id]/[letter-instance-name]/</code><br /> </p> </td>
  </tr>
  <tr>
   <td><p>Distant</p> </td>
   <td><p>Référentiel AEM de l’instance de création de traitement à distance</p> </td>
   <td><p><code>/content/apps/cm/letterInstances/[yyyy]/[mm]/[dd]/[node-id]/[letter-instance-name]/</code></p> </td>
  </tr>
 </tbody>
</table>

À l’emplacement du référentiel AEM spécifié ci-dessus :

* `[yyyy]/[mm]/[dd]` correspond à la structure du nœud en fonction de la date à laquelle l’instance de lettre a été créée
* `[node-id]` correspond à l’ID attribué au dossier contenant la lettre
* `[letter-instance-name]` correspond au nom spécifié lors de l’enregistrement ou de l’envoi d’une lettre

Sous le nœud [letter-instance-name], la structure de nœud suivante est créée et les données de chaque instance de lettre sont stockées dans le référentiel AEM :

| Nœud | Description |
|---|---|
| `extendedProperties` | Stocke les propriétés de métadonnées de l’instance de lettre. |
| `dataXML` | Stocke un fichier dataXML téléchargeable contenant les données de correspondance au format binaire. |
| `processedXDP` | Inclut les détails du modèle XDP utilisé pour créer la lettre soumise. Ce nœud est créé uniquement pour les correspondances envoyées. |
| `submittedLetter` | Stocke les données de lettres envoyées dans un format binaire téléchargeable. Ce nœud est créé uniquement pour les correspondances envoyées. |

## Accès et suppression des données utilisateur {#access-and-delete-user-data}

Vous pouvez accéder aux données de correspondance envoyées et sous forme de brouillons dans les magasins de données configurés et, si nécessaire, les supprimer.

### Accès aux données utilisateur {#access-user-data}

Correspondence Management fournit des API que vous pouvez utiliser pour rechercher et accéder aux instances de brouillons et de lettres envoyées. À l’aide des API, vous pouvez rechercher et ouvrir des instances de lettre à l’aide de l’ID de l’instance de lettre ou de la personne qui a enregistré ou envoyé la correspondance. Pour plus d’informations, reportez-vous à la section [Utiliser les API pour accéder aux instances de lettre](/help/forms/using/cm-apis-to-access-letter-instances.md).

Vous pouvez également accéder à l’instance de lettre dans le référentiel AEM à l’aide de CRXDE Lite. Voir [Données d’utilisateur ou d’utilisatrice et magasins de données](/help/forms/using/correspondence-management-handling-user-data.md#data) pour plus d’informations sur les données stockées et l’emplacement du référentiel.

### Suppression de données utilisateur {#delete-user-data}

Pour rechercher une instance de lettre contenant les données d’une personne spécifique, vous pouvez procéder des manières suivantes :

* Utilisez les API Correspondence Management si le nom de l’instance de lettre ou la personne qui a enregistré le brouillon ou envoyé la correspondance est connue.
* Utilisez l’option de recherche du référentiel AEM et saisissez des informations d’identification personnelles telles que l’identifiant ou le nom de l’adresse électronique pour trouver le nœud dans lequel l’information est stockée. 

Pour supprimer définitivement des données utilisateur de correspondances sous forme de brouillon et envoyées dans les systèmes AEM, vous devez supprimer manuellement le nœud d’instance de lettre de toutes les instances AEM applicables.
