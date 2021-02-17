---
title: Correspondence Management | Gestion des données utilisateur
seo-title: Correspondence Management | Gestion des données utilisateur
description: Correspondence Management | Gestion des données utilisateur
uuid: d5bb190b-d668-4da3-95da-b7705ad302d9
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 764d8e0d-604d-4c7b-89cd-7686ce5f03ff
translation-type: tm+mt
source-git-commit: a873cf3e7efd3bc9cd4744bf09078d9040efcdda
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 87%

---


# Correspondence Management | Gestion des données utilisateur {#correspondence-management-handling-user-data}

AEM Forms Correspondence Management vous permet de créer, gérer et rationaliser des correspondances client sécurisées et personnalisées. Il fournit une interface utilisateur intuitive pour que les utilisateurs professionnels puissent créer des correspondances à l’aide de blocs de contenu pré-approuvés et d’éléments multimédias. Pour plus d’informations sur la création de correspondances, voir [Création de correspondance](/help/forms/using/create-correspondence.md).

Lorsqu’un utilisateur professionnel ou un agent enregistre une correspondance en tant que brouillon ou l’envoie, une instance de lettre est enregistrée dans le référentiel AEM. L’instance de lettre comprend des données de correspondance et des métadonnées.

>[!NOTE]
>
>Dans AEM 6.5 Forms, la gestion des correspondances n’est pas disponible hors champ. Si vous effectuez une mise à niveau à partir d’une version précédente d’AEM Forms, installez le package de compatibilité et migrez vos actifs Correspondence Management pour continuer à les utiliser dans AEM 6.5 Forms. Pour plus d’informations, reportez-vous à la section [Package de compatibilité](/help/forms/using/compatibility-package.md).

## Données utilisateur et stockage de données {#data}

Correspondence Management stocke les données de brouillon et les lettres envoyées dans le référentiel AEM uniquement si l’instance de publication est configurée pour gérer les instances de lettre. Pour en savoir plus sur les propriétés de configuration, reportez-vous à la section [Propriétés de configuration de Correspondence Management](/help/forms/using/cm-configuration-properties.md).

Selon la persistance du stockage de données configuré pour votre déploiement AEM, les données de correspondances sous forme de brouillons et envoyées sont stockées aux emplacements suivants.

<table>
 <tbody>
  <tr>
   <td><p><strong>Type de persistance</strong></p> </td>
   <td><p><strong>Stockage de données</strong></p> </td>
   <td><p><strong>Emplacement</strong></p> </td>
  </tr>
  <tr>
   <td><p>Valeur par défaut</p> </td>
   <td><p>Référentiel AEM d’une instance de publication et des instances d’auteur spécifiées dans la configuration d’une réplication inverse</p> </td>
   <td><p><code>/content/apps/cm/letterInstances/[yyyy]/[mm]/[dd]/[node-id]/[letter-instance-name]/</code> </p> </td>
  </tr>
  <tr>
   <td><p>Distant</p> </td>
   <td><p>Référentiel AEM de l’instance d’auteur de traitement distante</p> </td>
   <td><p><code>/content/apps/cm/letterInstances/[yyyy]/[mm]/[dd]/[node-id]/[letter-instance-name]/</code></p> </td>
  </tr>
 </tbody>
</table>

À l’emplacement du référentiel AEM spécifié ci-dessus :

* `[yyyy]/[mm]/[dd]` correspond à la structure du nœud en fonction de la date à laquelle l’instance de lettre a été créée
* `[node-id]` correspond à l’ID attribué au dossier contenant la lettre
* `[letter-instance-name]` correspond au nom spécifié lors de l’enregistrement ou de l’envoi d’une lettre

Sous le noeud [letter-instance-name], la structure de noeud suivante est créée et les données de chaque instance de lettre sont stockées dans le référentiel AEM :

| Node | Description |
|---|---|
| `extendedProperties` | Stocke les propriétés de métadonnées de l’instance de lettre. |
| `dataXML` | Stocke un fichier dataXML téléchargeable contenant les données de correspondance au format binaire. |
| `processedXDP` | Comprend les détails du modèle XDP utilisé pour créer la lettre envoyée. Ce nœud est créé uniquement pour les correspondances envoyées. |
| `submittedLetter` | Stocke les données de lettres envoyées dans un format binaire téléchargeable. Ce nœud est créé uniquement pour les correspondances envoyées. |

## Accès et suppression des données utilisateur {#access-and-delete-user-data}

Vous pouvez accéder aux données de correspondances sous forme de brouillons et envoyées dans les stockages de données configurés et, si nécessaire, les supprimer.

### Accès aux données utilisateur  {#access-user-data}

Correspondence Management fournit des API que vous pouvez utiliser pour rechercher et accéder à des instances de lettres envoyées et sous forme de brouillons. Grâce aux API vous pouvez rechercher et ouvrir des instances de lettre à l’aide de l’ID de l’instance de lettre ou de l’utilisateur qui a enregistré ou envoyé la correspondance. Pour plus d’informations, voir [API pour accéder aux instances de lettre](/help/forms/using/cm-apis-to-access-letter-instances.md).

Vous pouvez également accéder à une instance de lettre dans un référentiel AEM à l’aide de CRX DELite. Reportez-vous à la section [Données utilisateur et stockage de données](/help/forms/using/correspondence-management-handling-user-data.md#data) pour en savoir plus sur les données stockées et l’emplacement du référentiel.

### Suppression de données utilisateur  {#delete-user-data}

Pour rechercher une instance de lettre qui contient les données d’un utilisateur spécifique, vous pouvez :

* utiliser les API de Correspondence Management si le nom de l’instance de lettre ou l’utilisateur qui a enregistré le brouillon ou envoyé la correspondance est connu ;
* Utilisez AEM recherche de référentiel à l’aide d’informations d’identification personnelle telles que l’ID ou le nom de l’adresse électronique pour rechercher le noeud sur lequel les informations sont stockées.

Pour supprimer définitivement des données utilisateur de correspondances sous forme de brouillon et envoyées dans les systèmes AEM, vous devez supprimer manuellement le nœud d’instance de lettre de toutes les instances AEM applicables.
