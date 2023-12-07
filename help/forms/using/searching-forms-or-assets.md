---
title: Rechercher des formulaires et des ressources
description: Vous pouvez rechercher des formulaires et des ressources dans votre instance AEM à l’aide de la recherche AEM. Les recherches de base et avancées vous permettent de localiser rapidement vos ressources.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
docset: aem65
role: Admin
exl-id: 1f4f49b7-5f32-47dd-9dc7-a6974faf2bdf
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 30%

---

# Rechercher des formulaires et des ressources{#searching-for-forms-and-assets}

Vous pouvez rechercher vos formulaires ou actifs de formulaire à l’aide d’une chaîne de texte ou d’une chaîne de texte accompagnée de caractères génériques. Vous pouvez également affiner votre recherche à l’aide des critères disponibles dans différentes catégories du panneau Rechercher.

Lorsque vous sélectionnez un ou plusieurs critères et spécifiez également une chaîne de texte, l’intersection du texte et des critères est renvoyée sous forme de résultats de recherche. La qualité des résultats est équivalente à celles des métadonnées de formulaires et de ressources fournies.

Cliquez sur ![aem6forms_search](assets/aem6forms_search.png) pour afficher ou masquer le panneau de recherche.

## Recherche de base {#basic-search}

Une recherche de base est la recherche par défaut, exécutée sans spécifier de filtres. Une recherche de texte intégral sur les propriétés de métadonnées est effectuée par AEM Forms.

Pour lancer une recherche de base, saisissez la requête dans le champ de texte et appuyez sur Retour. Vous pouvez également saisir le caractère générique (&#42;) pour faire correspondre un nombre indéfini de caractères.

Adobe Experience Manager recherche le texte saisi dans les propriétés de métadonnées et renvoie les résultats correspondants. Si vous saisissez plusieurs mots, l’opération de recherche correspond au texte complet à rechercher.

Notez les points suivants concernant la recherche de base :

* La recherche est effectuée à l’aide des propriétés de métadonnées de formulaire et de ressource.
* Si vous saisissez plusieurs mots, l’opération de recherche correspond au texte complet à rechercher.
* La recherche n’est pas sensible à la casse. Par exemple, lorsque vous saisissez `geometrixx`, des ressources intitulées `Geometrixx`, `GEOMETRIXX` et `GeoMetRixx` sont reprises dans les résultats de la recherche.

* Les correspondances partielles d’un mot ne sont pas prises en charge. Pour effectuer une recherche en utilisant des chaînes partielles, utilisez le caractère générique &#42;. Cependant, si la requête de recherche correspond à un mot complet, le formulaire ou la ressource correspondant s’affiche.
* Les espaces supplémentaires sont respectés et ne sont pas supprimés lors de la recherche. Par exemple : `My form` n’est pas la même requête que `My form`.

* Si les données et les valeurs d’affichage des champs dans les propriétés de métadonnées sont différentes, vous ne pouvez pas utiliser les valeurs d’affichage comme paramètres de recherche. Par exemple, vous ne pouvez pas effectuer de recherche en fonction de l’état, tel que Modifié ou Publié, car ces propriétés sont stockées dans un autre format.

## Recherche avancée {#advanced-search}

Dans les critères de recherche, outre la requête, vous pouvez spécifier certains paramètres de recherche afin de rendre la recherche de base plus efficace et plus précise.

![Champ de recherche et paramètres ou filtres du formulaire AEM et de recherche de ressources](assets/search_forms_assets.png)

Champ de recherche et paramètres ou filtres du formulaire AEM et de recherche de ressources

### Chemin d&#39;accès à la ressource {#asset-path}

En utilisant le filtre de chemin d’accès aux ressources, vous pouvez limiter les résultats de recherche au répertoire actuel. Si l’option Rechercher dans le répertoire actuel n’est pas sélectionnée, les résultats de la recherche contiennent des ressources provenant du répertoire de base. Si la page en cours n’est pas un répertoire et que l’option Rechercher dans le répertoire actuel est sélectionnée, la recherche renvoie les éléments figurant dans le répertoire parent.

### Modification des ressources {#asset-modification}

Sélectionnez l’une des options suivantes pour effectuer une recherche sur toutes les ressources modifiées au cours d’une période donnée.

| **Option** | **Description** |
|---|---|
| Il y a deux heures | Recherche parmi toutes les ressources qui ont été modifiées au cours des deux dernières heures. |
| Il y a une semaine | Recherche parmi toutes les ressources qui ont été modifiées au cours de la dernière semaine. |
| Il y a un mois | Recherche parmi toutes les ressources qui ont été modifiées au cours du dernier mois. |
| Il y a un an | Recherche parmi toutes les ressources qui ont été modifiées au cours de l’année écoulée. |

### Statut de la ressource {#asset-status}

Vous pouvez rechercher des ressources à l’aide de l’un des états suivants :

* **Publié** : recherche toutes les ressources publiées et non modifiées après la publication.

* **Dépublié** : recherche toutes les ressources qui ne sont jamais publiées.

* **Modifié**: recherche toutes les ressources qui sont modifiées ou dont la publication a été annulée après la publication.

### Type de ressource {#asset-type}

Vous pouvez sélectionner un nombre indéfini de types de ressources. La recherche renvoie l’union de tous les types de ressources sélectionnés.

<table>
 <tbody>
  <tr>
   <th>Option</th> 
   <th>Description</th> 
  </tr>
  <tr>
   <td>Modèle de formulaire<br /> </td> 
   <td>Recherche dans tous les modèles de formulaire.<br /> </td> 
  </tr>
  <tr>
   <td>Formulaire de PDF</td> 
   <td>Recherche dans tous les documents du PDF.</td> 
  </tr>
  <tr>
   <td>Document</td> 
   <td>Recherche dans tous les documents.</td> 
  </tr>
  <tr>
   <td>Formulaire adaptatif<br /> </td> 
   <td>Recherche dans tous les formulaires adaptatifs.</td> 
  </tr>
  <tr>
   <td>Ressource</td> 
   <td>Recherche parmi toutes les ressources.<br /> </td> 
  </tr>
 </tbody>
</table>

### Balises {#tags}

Les balises sont des libellés associés aux ressources à des fins d’identification. Lors de la recherche, sélectionnez un nombre de balises dans la liste déroulante ou ajoutez des balises personnalisées, si nécessaire. Un résultat de recherche contient l’intersection des balises sélectionnées.
