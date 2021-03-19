---
title: Recherche de formulaires et de ressources
seo-title: Recherche de formulaires et de ressources
description: Vous pouvez rechercher des formulaires et des ressources dans votre instance AEM à l’aide de la recherche AEM. Les modes de recherche de base et avancé vous permettent de localiser rapidement vos ressources.
seo-description: Vous pouvez rechercher des formulaires et des ressources dans votre instance AEM à l’aide de la recherche AEM. Les modes de recherche de base et avancé vous permettent de localiser rapidement vos ressources.
uuid: 0928a453-3dc4-448b-9320-dcbf20606dd9
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: e65925ff-1fbf-4da6-bf09-0cf056c86e5a
docset: aem65
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 95%

---


# Recherche de formulaires et de ressources{#searching-for-forms-and-assets}

Vous pouvez rechercher vos formulaires ou ressources de formulaire à l’aide d’une chaîne de texte ou d’une chaîne de texte accompagnée de caractères génériques. Vous pouvez également préciser la recherche à l’aide des critères disponibles dans différentes catégories du panneau Rechercher.

Lorsque vous sélectionnez un ou plusieurs critères et spécifiez également une chaîne de texte, l’intersection du texte et des critères est renvoyée sous la forme de résultats de la recherche. La qualité des résultats est équivalente à celles des métadonnées de formulaires et de ressources fournies.

Cliquez sur ![aem6forms_search](assets/aem6forms_search.png) pour afficher ou masquer le panneau de recherche.

## Recherche de base {#basic-search}

La recherche de base constitue le type de recherche par défaut. Elle s’exécute sans spécifier aucun filtre. Une recherche de texte intégral sur des propriétés de métadonnées est effectuée par AEM Forms.

Pour effectuer une recherche de base, entrez la requête dans le champ de texte et appuyez ensuite sur Entrée. Vous pouvez également saisir le caractère générique (*) pour faire correspondre un nombre indéfini de caractères.

Adobe Experience Manager recherche le texte saisi dans les propriétés de métadonnées et renvoie les résultats correspondants. Si vous entrez plusieurs mots, l’opération de recherche correspond à la totalité du texte.

Tenez compte des points suivants au sujet de la recherche de base :

* La recherche est effectuée à l’aide des propriétés de métadonnées de formulaire et de ressource.
* Si vous entrez plusieurs mots, l’opération de recherche correspond à la totalité du texte.
* La recherche ne respecte pas la casse. Par exemple, lorsque vous tapez `geometrixx`, les ressources dont les titres sont `Geometrixx`, `GEOMETRIXX` et `GeoMetRixx` s’affichent dans les résultats de la recherche.

* Les correspondances partielles d’un mot ne sont pas prises en charge. Pour effectuer une recherche en utilisant des chaînes partielles, utilisez le caractère générique *. Toutefois, si la requête correspond à un mot complet, le formulaire ou la ressource correspondant s’affiche.
* Les espaces supplémentaires sont respectés et ne sont pas coupés lors de la recherche. Par exemple, `My form` n&#39;est pas la même requête de recherche que `My form`.

* Si les données et les valeurs d’affichage des champs dans les propriétés de métadonnées sont différentes, vous ne pouvez pas utiliser ces valeurs comme paramètres de recherche. Par exemple, vous ne pouvez effectuer une recherche sur la base de l’état, tel que Modifié ou Publié, car ces propriétés sont stockées dans un format différent.

## Recherche avancée {#advanced-search}

Dans les critères de recherche, outre la requête, vous pouvez spécifier certains paramètres de recherche pour améliorer l’efficacité et la précision de la recherche.

![Champ de recherche et paramètres ou filtres du formulaire AEM et de recherche de ressources](assets/search_forms_assets.png)

Champ de recherche et paramètres ou filtres du formulaire AEM et de recherche de ressources

### Chemin d’accès à la ressource {#asset-path}

Le filtre de chemin d’accès aux ressources vous permet de limiter les résultats de la recherche au répertoire actuel. Si l’option Rechercher dans le répertoire actuel n’est pas sélectionnée, les résultats de la recherche contiennent des ressources provenant du répertoire de base. Si la page en cours n’est pas un répertoire et que l’option Rechercher dans le répertoire actuel est sélectionnée, la recherche renvoie les éléments figurant dans le répertoire parent.

### Modification des ressources {#asset-modification}

Sélectionnez l’une des options suivantes afin d’effectuer des recherches dans toutes les ressources modifiées au cours d’une période donnée.

| **Option** | **Description** |
|---|---|
| Il y a deux heures | Recherche parmi toutes les ressources qui ont été modifiées au cours des deux dernières heures. |
| Il y a une semaine | Recherche parmi toutes les ressources qui ont été modifiées au cours de la semaine écoulée. |
| Il y a un mois | Recherche parmi toutes les ressources qui ont été modifiées au cours du dernier mois. |
| Il y a un an | Recherche parmi toutes les ressources qui ont été modifiées au cours de l’année écoulée. |

### Etat de la ressource {#asset-status}

Vous pouvez rechercher des ressources en utilisant l’un des états suivants :

* **Publié** : recherche toutes les ressources publiées et non modifiées après la publication.

* **Non publié** : recherche toutes les ressources qui ne sont jamais publiées.

* **Modifié** : recherche toutes les ressources qui sont modifiées ou ne sont pas publiées après la publication.

### Type de ressource {#asset-type}

Vous pouvez choisir un grand nombre de types de ressource. La recherche renvoie tous les types de ressource sélectionnés réunis.

<table>
 <tbody>
  <tr>
   <th>Option</th> 
   <th>Description</th> 
  </tr>
  <tr>
   <td>Modèle de formulaire<br /> </td> 
   <td>Recherche dans tous les modèles de formulaires.<br /> </td> 
  </tr>
  <tr>
   <td>Formulaire PDF</td> 
   <td>Recherche dans tous les documents PDF.</td> 
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
   <td>Recherche dans toutes les ressources.<br /> </td> 
  </tr>
 </tbody>
</table>

### Balises {#tags}

Les balises sont des libellés associés à des ressources pour identification. Lors de la recherche, sélectionnez un nombre de balises dans la liste déroulante ou ajoutez des balises personnalisées, si nécessaire. Un résultat de recherche contient l’intersection des balises sélectionnées.
