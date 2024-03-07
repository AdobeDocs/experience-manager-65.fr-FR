---
title: Éditeur en bloc
description: Découvrez comment utiliser l’éditeur en bloc pour une modification efficace lorsque le contexte visuel de page n’est pas nécessaire.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
exl-id: c63e044c-4d2a-44d3-853b-8e7337e1ee03
source-git-commit: db0e9d6105484b37e2e21e49bf0f95cef9da2a62
workflow-type: tm+mt
source-wordcount: '1160'
ht-degree: 79%

---


# Éditeur en bloc{#the-bulk-editor}

L’éditeur en bloc permet une modification efficace lorsque le contexte visuel de la page n’est pas nécessaire, car il vous permet d’effectuer les opérations suivantes :

* chercher (et afficher) le contenu de plusieurs pages, à l’aide du langage de requête de Google (Google Query Language, GQL) ;
* modifier directement ce contenu dans l’éditeur en bloc :
* d’enregistrer les modifications (dans les pages d’origine) ;
* d’exporter ce contenu vers un fichier de feuille de calcul de données séparées par des tabulations (.tsv).

>[!NOTE]
>
>Vous pouvez également importer du contenu dans le référentiel, mais cette option est désactivée par défaut pour l’éditeur en bloc, tel qu’il est disponible dans la console **Outils**.

Cette section décrit comment utiliser l’éditeur en bloc dans la console **Outils**. En général, les administrateurs et administratrices utilisent l’éditeur en bloc pour chercher et modifier différents éléments. Cette opération est effectuée en renseignant le tableau à l’aide d’une requête GQL, puis en sélectionnant les éléments de contenu sur lesquels travailler. Les créateurs et créatrices utilisent généralement l’éditeur en bloc dans le cadre d’une application d’éditeur en bloc personnalisée par le biais du composant [Liste de produits](/help/sites-authoring/default-components.md#productlist).

>[!CAUTION]
>
>Avec l’[abandon de l’interface utilisateur classique](/help/release-notes/deprecated-removed-features.md) dans AEM 6.4, l’éditeur en bloc a également été abandonné et, par conséquent, Adobe ne prévoit pas d’améliorer davantage l’éditeur en bloc.

## Exemple de cas d’utilisation pour l’éditeur en bloc {#example-use-case-for-the-bulk-editor}

Par exemple, si vous avez besoin de tous les noms et adresses e-mail des utilisateurs et utilisatrices qui ont répondu à une enquête spécifique, l’éditeur en bloc peut fournir ces informations et vous pouvez les exporter dans une feuille de calcul.

Le site web de Geometrixx fournit un exemple illustrant ce cas d’utilisation :

1. Accédez à la page **Assistance**, puis à l’enquête **Satisfaction relative au service clientèle**.
1. **Modifiez** le paragraphe **Début du formulaire**. Dans la boîte de dialogue, cliquez sur le bouton **Avancé** , développez la **Configuration d’action**, puis cliquez sur **Afficher les données...**.

   ![Exemple d’enquête sur la satisfaction de la clientèle](assets/custsatsurvey.png)

1. L’éditeur en bloc est entièrement personnalisable, même si, dans cet exemple, il ne permet pas aux utilisateurs et utilisatrices de modifier le contenu, mais seulement d’exporter les informations vers une feuille de calcul.

   ![Console de l’éditeur en bloc](assets/bulkeditor.png)

## Utilisation de l’éditeur en bloc {#how-to-use-the-bulk-editor}

L’éditeur en bloc vous permet :

* [de rechercher du contenu en fonction de paramètres de requête afin d’afficher les propriétés spécifiées des résultats dans des colonnes, de modifier ce contenu et d’enregistrer les modifications ;](#searching-and-editing-content)
* [d’exporter ce contenu vers une feuille de calcul de données séparées par des tabulations ;](#exporting-content)

* [d’importer le contenu d’une feuille de calcul de données séparées par des tabulations.](#importing-content)

### Recherche et modification de contenu {#searching-and-editing-content}

Pour utiliser l’éditeur en bloc afin de modifier plusieurs éléments simultanément :

1. Dans la console **Outils**, cliquez sur le dossier **Importateurs** pour le développer.
1. Double-cliquez sur le **Éditeur en bloc**.
1. Saisissez vos exigences de sélection :

<table>
 <tbody>
  <tr>
   <td>Champ</td>
   <td>Propriété</td>
  </tr>
  <tr>
   <td>Chemin racine</td>
   <td>Indique le chemin racine que recherche l’éditeur en bloc.<br /> Par exemple, <code>/content/geometrixx/en</code>. L’éditeur en bloc effectue une recherche dans tous les nœuds enfants.</td>
  </tr>
  <tr>
   <td>Paramètres de requête</td>
   <td>À l’aide des paramètres GQL, saisissez la chaîne de recherche que l’éditeur en bloc doit rechercher dans le référentiel. Par exemple : <code>type:Page</code> recherche toutes les pages du chemin racine, <code>text:professional</code> recherche toutes les pages qui contiennent le mot "professionnel", et <code>"jcr:title":English</code> recherche toutes les pages dont le titre est "Anglais". Vous pouvez rechercher uniquement des chaînes.</td>
  </tr>
  <tr>
   <td>Case à cocher Mode Contenu</td>
   <td>Cochez cette case pour pouvoir lire les propriétés dans la variable <code>jcr:content</code> sous-noeud des résultats de la recherche s’il existe. À utiliser uniquement pour des pages. Les noms de propriété comportent le préfixe <code>"jcr:content/"</code></td>
  </tr>
  <tr>
   <td>Propriétés/Colonnes</td>
   <td>Cochez les cases correspondant aux propriétés que l’éditeur en bloc doit renvoyer. Les propriétés que vous sélectionnez sont les titres de colonne dans le volet de résultats. Par défaut, le chemin du nœud s’affiche dans les résultats.</td>
  </tr>
  <tr>
   <td>Propriétés / Colonnes personnalisées</td>
   <td>Saisissez d’autres propriétés qui ne sont pas répertoriées dans le champ <strong>Propriétés/Colonnes</strong>. Ces propriétés personnalisées s’affichent dans le volet de résultats. Vous pouvez ajouter plusieurs propriétés en les séparant par des virgules. <i>Remarque :</i> si vous ajoutez une propriété personnalisée qui n’existe pas encore, la gestion de contenu Web AEM affiche une cellule vide. Lorsque vous modifiez la cellule vide et que vous l’enregistrez, la propriété est ajoutée au nœud. La propriété nouvellement créée doit respecter les contraintes de type de nœud et les espaces de noms de propriété.</td>
  </tr>
 </tbody>
</table>

Par exemple :

![Options de filtre de l’éditeur en bloc](assets/searchfilter.png)

1. Cliquez sur **Rechercher**. L’éditeur en bloc affiche les résultats.
Pour l’exemple ci-dessus, toutes les pages qui correspondent aux critères de recherche sont renvoyées et affichées avec les colonnes demandées.

   ![Résultats de l’éditeur en bloc](assets/chlimage_1-39.png)

1. Double-cliquez sur une cellule pour apporter des modifications.

   ![Modification en bloc](assets/srchresultedit.png)

1. Cliquez sur **Enregistrer** pour enregistrer vos modifications (le **Enregistrer** est activé après avoir modifié une cellule).

   >[!CAUTION]
   >
   >Les modifications que vous apportez sont écrites dans le contenu du référentiel, par exemple la page référencée dans **Chemin d’accès**.

#### Paramètres de requête GQL supplémentaires {#additional-gql-query-parameters}

* **path :** effectue une recherche uniquement sur les nœuds sous ce chemin d’accès. Si vous spécifiez plusieurs termes avec un préfixe de chemin d’accès, seul le dernier terme est pris en compte.
* **type :** renvoie uniquement les noeuds du type de noeud donné. Cela inclut les types principal et mixin. Vous pouvez spécifier plusieurs types de nœuds séparés par des virgules. GQL renvoie les nœuds de l’un des types spécifiés.
* **order :** organise le résultat en fonction des propriétés données. Vous pouvez spécifier plusieurs noms de propriétés séparés par des virgules. Pour contrôler le résultat dans l’ordre descendant, ajoutez simplement le préfixe « - » (moins) au nom de la propriété. Par exemple, order:-name. Si vous utilisez un signe « + » (plus), le résultat est renvoyé dans l’ordre ascendant, qui est également l’ordre par défaut.
* **limit :** limite le nombre de résultats à l’aide d’un intervalle. Par exemple, limit:10.20 L’intervalle est de base zéro, le début est inclusif et la fin est exclusive. Vous pouvez également spécifier une ouverture `interval:limit:10..` ou `limit:..20`
Si les points sont omis et qu’une seule valeur est spécifiée, GQL renvoie au plus ce nombre de résultats. Par exemple : `limit:10` (renvoie les dix premiers résultats).

### Export de contenu {#exporting-content}

Si nécessaire, exportez le contenu dans une feuille de calcul Excel pour apporter des modifications. Par exemple, vous pouvez exporter une liste de diffusion et modifier l’indicatif régional de tous les numéros de téléphone répertoriés directement dans Excel, ou ajouter des lignes supplémentaires.

Pour exporter du contenu :

1. Recherchez du contenu comme décrit dans [Recherche et modification de contenu](#searching-and-editing-content).
1. Cliquez sur **Exporter** vous pouvez ainsi exporter les modifications dans une feuille de calcul Excel séparée par des tabulations. La gestion de contenu web d’AEM vous demande où vous souhaitez télécharger le fichier.

   >[!NOTE]
   >
   >Par défaut, les modifications sont codées en [Windows-1252](https://fr.wikipedia.org/wiki/Windows-1252) (également appelé « CP-1252 »). Vous pouvez cocher UTF-8 pour exporter les modifications au format UTF-8.

   ![Export des résultats](assets/srchrsesultexport.png)

1. Sélectionnez l’emplacement et confirmez que vous souhaitez télécharger le fichier.
1. Une fois que vous avez téléchargé le fichier, vous pouvez l’ouvrir dans votre feuille de calcul, par exemple, Microsoft® Excel. Le programme de feuille de calcul importe le fichier et la convertit au format feuille de calcul.

   ![Résultats exportés dans une feuille de calcul](assets/exportinexcel.png)

### Import du contenu {#importing-content}

Par défaut, la fonctionnalité d’importation est masquée lorsque vous ouvrez l’éditeur en bloc. Il suffit d’ajouter le paramètre `hib=false` à l’adresse URL pour afficher le bouton **Importer** dans la page Éditeur en bloc. Vous pouvez importer du contenu à partir de n’importe quel fichier de données séparées par des tabulations (`.tsv`). Pour que l’import fonctionne correctement, les en-têtes de colonne (première ligne de cellules) doivent correspondre aux en-têtes de colonne du tableau dans lequel vous importez.

>[!NOTE]
>
>Lorsque vous réimportez le contenu, vous effacez le contenu existant de ces nœuds. Veillez à ne pas remplacer des informations importantes.

Pour importer du contenu :

1. Ouvrez l’éditeur en bloc.
1. Ajoutez `?hib=false` à l’URL, par exemple :
   `https://localhost:4502/etc/importers/bulkeditor.html?hib=false`
1. Cliquez sur **Importer**.
1. Sélectionnez le fichier `.tsv`. Les données sont importées dans le référentiel.
