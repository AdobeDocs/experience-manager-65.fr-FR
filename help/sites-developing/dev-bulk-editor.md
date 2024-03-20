---
title: Développer l’éditeur en bloc
description: Le balisage permet de catégoriser et d’organiser le contenu.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 8753aaab-959f-459b-bdb6-057cbe05d480
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1833'
ht-degree: 52%

---

# Développer l’éditeur en bloc{#developing-the-bulk-editor}

Cette section décrit le développement de l’outil d’éditeur en bloc et l’extension du composant Liste de produits , basé sur l’éditeur en bloc.

## Paramètres de requête de l’éditeur en bloc {#bulk-editor-query-parameters}

Lorsque vous utilisez l’éditeur en bloc, vous pouvez ajouter plusieurs paramètres de requête à l’URL pour appeler l’éditeur en bloc avec une configuration spécifique. Si vous souhaitez que l’éditeur en bloc soit toujours utilisé avec une certaine configuration, par exemple, comme dans le composant Liste de produits, vous devez modifier . `bulkeditor.jsp` (dans /libs/wcm/core/components/bulkeditor) ou créez un composant avec la configuration spécifique. Les modifications effectuées à l’aide des paramètres de requête ne sont pas permanentes.

Par exemple, si vous entrez les informations suivantes dans l’URL de votre navigateur :

`https://<servername><port_number>/etc/importers/bulkeditor.html?rootPath=/content/geometrixx/en&queryParams=geometrixx&initialSearch=true&hrp=true`

L’éditeur en bloc s’affiche sans le paramètre **Chemin racine** comme hrp=true masque le champ. Avec le paramètre hrp=false, le champ s’affiche (valeur par défaut).

Voici une liste des paramètres de requête de l’éditeur en bloc :

>[!NOTE]
>
>Chaque paramètre peut avoir un nom long et un nom court. Par exemple, le nom long du chemin racine de recherche est `rootPath`, la valeur abrégée est `rp`. Si le nom long n’est pas défini, le nom abrégé est lu dans la requête.

<table>
 <tbody>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p> Paramètre</p> <p>(nom long / nom court)<br /> </p> </td>
   <td> Type <br /> </td>
   <td> Description <br /> </td>
  </tr>
  <tr>
   <td> rootPath / rp<br /> </td>
   <td> Chaîne </td>
   <td> chemin racine de recherche</td>
  </tr>
  <tr>
   <td> queryParams / qp<br /> </td>
   <td> Chaîne</td>
   <td> requête de recherche</td>
  </tr>
  <tr>
   <td> contentMode / cm<br /> </td>
   <td> Booléen</td>
   <td> lorsque la valeur est true, le mode de contenu est activé.<br /> </td>
  </tr>
  <tr>
   <td> colsValue / cv<br /> </td>
   <td> Chaîne[]</td>
   <td> propriétés recherchées (valeurs cochées de colsSelection affichées sous forme de cases à cocher)</td>
  </tr>
  <tr>
   <td> extraCols / ec<br /> </td>
   <td> Chaîne[]</td>
   <td> propriétés recherchées supplémentaires (affichées dans un champ de texte séparé par des virgules)</td>
  </tr>
  <tr>
   <td> initialSearch / is<br /> </td>
   <td> Booléen</td>
   <td> lorsque la valeur est true, la requête est exécutée au chargement de la page.<br /> </td>
  </tr>
  <tr>
   <td> colsSelection / cs<br /> </td>
   <td> Chaîne[]</td>
   <td> sélection des propriétés recherchées (affichée sous forme de cases à cocher)</td>
  </tr>
  <tr>
   <td> showGridOnly / sgo<br /> </td>
   <td> Booléen</td>
   <td> lorsque la valeur est true, affiche uniquement la grille et non le panneau de recherche. <br /> </td>
  </tr>
  <tr>
   <td> searchPanelCollapsed / spc</td>
   <td> Booléen</td>
   <td> lorsque la valeur est true, le panneau de recherche est réduit au chargement.</td>
  </tr>
  <tr>
   <td> hideRootPath / hrp</td>
   <td> Booléen</td>
   <td> lorsque la valeur est true, le champ de chemin d’accès racine est masqué.</td>
  </tr>
  <tr>
   <td> hideQueryParams / hqp</td>
   <td> Booléen</td>
   <td> lorsque la valeur est true, le champ de requête est masqué.</td>
  </tr>
  <tr>
   <td> hideContentMode / hcm</td>
   <td> Booléen</td>
   <td> lorsque la valeur est true, le champ mode de contenu est masqué.</td>
  </tr>
  <tr>
   <td> hideColsSelection / hcs</td>
   <td> Booléen</td>
   <td> lorsque la valeur est true, le champ de sélection des colonnes est masqué.</td>
  </tr>
  <tr>
   <td> hideExtraCols / hec</td>
   <td> Booléen</td>
   <td> lorsque la valeur est true, le champ des colonnes supplémentaires est masqué.</td>
  </tr>
  <tr>
   <td> hideSearchButton</td>
   <td> Booléen</td>
   <td> lorsque la valeur est true, le bouton de recherche est masqué.</td>
  </tr>
  <tr>
   <td> hideSaveButton / hsavep</td>
   <td> Booléen</td>
   <td> lorsque la valeur est true, le bouton d’enregistrement est masqué.</td>
  </tr>
  <tr>
   <td> hideExportButton / hexpb</td>
   <td> Booléen</td>
   <td> lorsque la valeur est true, le bouton d’exportation est masqué.</td>
  </tr>
  <tr>
   <td> hideImportButton / hib</td>
   <td> Booléen</td>
   <td> lorsque la valeur est true, le bouton d’importation est masqué.</td>
  </tr>
  <tr>
   <td> hideResultNumber / hrn</td>
   <td> Booléen</td>
   <td> lorsque la valeur est true, le texte du numéro de résultat de la recherche par grille est masqué.</td>
  </tr>
  <tr>
   <td> hideInsertButton / hinsertb</td>
   <td> Booléen</td>
   <td> lorsque la valeur est true, le bouton d’insertion de grille est masqué.</td>
  </tr>
  <tr>
   <td> hideDeleteButton / hdelb</td>
   <td> Booléen</td>
   <td> lorsque la valeur est true, le bouton de suppression de la grille est masqué.</td>
  </tr>
  <tr>
   <td> hidePathCol / hpc</td>
   <td> Booléen</td>
   <td> lorsque la valeur est true, la colonne « chemin » de la grille est masquée.</td>
  </tr>
 </tbody>
</table>

### Développement d’un composant basé sur l’éditeur en bloc : le composant Liste de produits {#developing-a-bulk-editor-based-component-the-product-list-component}

Cette section présente un aperçu de l’utilisation de l’éditeur en bloc et donne une description du composant de Geometrixx existant en fonction de l’éditeur en bloc : le composant Liste de produits.

Le composant Liste de produits permet aux utilisateurs d’afficher et de modifier une table de données. Par exemple, vous pouvez utiliser le composant Liste de produits pour représenter les produits d’un catalogue. Les informations sont présentées dans un tableau de HTML standard et toute modification est effectuée dans la variable **Modifier** qui contient un widget BulkEditor. (Cet éditeur en bloc est identique à celui accessible à l’adresse /etc/importers/bulkeditor.html ou via le menu Outils). Le composant Liste de produits a été configuré pour des fonctionnalités spécifiques et limitées de l’éditeur en bloc. Chaque partie de l’éditeur en bloc (ou les composants dérivés de l’éditeur en bloc) peut être configurée.

Avec l’éditeur en bloc, vous pouvez ajouter, modifier, supprimer, filtrer et exporter les lignes, enregistrer les modifications et importer un ensemble de lignes. Chaque ligne est stockée en tant que nœud sous l’instance du composant Liste de produits elle-même. Chaque cellule est une propriété de chaque nœud. C’est un choix de conception qui peut être facilement modifié. Par exemple, vous pouvez stocker des nœuds ailleurs dans le référentiel. Le rôle du servlet de requête est de renvoyer la liste des noeuds à afficher ; le chemin de recherche est défini comme une instance Liste de produits.

Le code source du composant Liste de produits est disponible dans le référentiel à l’adresse /apps/geometrixx/components/productlist et est composé de plusieurs parties comme tous les composants Adobe Experience Manager (AEM) :

* Rendu HTML : le rendu est effectué dans un fichier JSP (/apps/geometrixx/components/productlist/productlist.jsp). Le JSP lit les sous-noeuds du composant Liste de produits actuel et les affiche chacun sous la forme d’une ligne d’un tableau de HTML.
* Boîte de dialogue Modifier dans laquelle vous définissez la configuration de l’éditeur en masse. Configurez la boîte de dialogue de sorte à répondre aux besoins du composant : colonnes disponibles et actions possibles effectuées sur la grille ou sur la recherche. Voir [Propriétés de configuration de l’éditeur en bloc](#bulk-editor-configuration-properties) pour plus d’informations sur toutes les propriétés de configuration.

Voici une représentation XML des sous-noeuds de boîte de dialogue :

```xml
        <editor
            jcr:primaryType="cq:Widget"
            colsSelection="[ProductId,ProductName,Color,CatalogCode,SellingSku]"
            colsValue="[ProductId,ProductName,Color,CatalogCode,SellingSku]"
            contentMode="false"
            exportURL="/etc/importers/bulkeditor/export.tsv"
            extraCols="Selection"
            hideColsSelection="false"
            hideContentMode="true"
            hideDeleteButton="false"
            hideExportButton="false"
            hideExtraCols="true"
            hideImportButton="false"
            hideInsertButton="false"
            hideMoveButtons="false"
            hidePathCol="true"
            hideRootPath="true"
            hideSaveButton="false"
            hideSearchButton="false"
            importURL="/etc/importers/bulkeditor/import"
            initialSearch="true"
            insertedResourceType="geometrixx/components/productlist/sku"
            queryParams=""
            queryURL="/etc/importers/bulkeditor/query.json"
            saveURL="/etc/importers/bulkeditor/save"
            xtype="bulkeditor">
            <saveButton
                jcr:primaryType="nt:unstructured"
                text="Save modifications"/>
            <searchButton
                jcr:primaryType="nt:unstructured"
                text="Apply filter"/>
            <queryParamsInput
                jcr:primaryType="nt:unstructured"
                fieldDescription="Enter here your filters"
                fieldLabel="Filters"/>
            <searchPanel
                jcr:primaryType="nt:unstructured"
                height="200">
                <defaults
                    jcr:primaryType="nt:unstructured"
                    labelWidth="150"/>
            </searchPanel>
            <grid
                jcr:primaryType="nt:unstructured"
                height="275"/>
            <store jcr:primaryType="nt:unstructured">
                <sortInfo
                    jcr:primaryType="nt:unstructured"
                    direction="ASC"
                    field="CatalogCode"/>
            </store>
            <colModel
                jcr:primaryType="nt:unstructured"
                width="150"/>
            <colsMetadata jcr:primaryType="nt:unstructured">
                <Selection
                    jcr:primaryType="nt:unstructured"
                    checkbox="true"
                    forcedPosition="0"
                    headerText=""/>
                <ProductId
                    jcr:primaryType="nt:unstructured"
                    cellCls="productlist-cell-productid"
                    headerText="Product Id"/>
                <ProductName
                    jcr:primaryType="nt:unstructured"
                    cellStyle="background-color: #FFCC99;"
                    headerText="Product Name"/>
                <CatalogCode
                    jcr:primaryType="nt:unstructured"
                    cellStyle="background-color: #EDEDED;"
                    headerText="Catalog Code"/>
                <Color jcr:primaryType="nt:unstructured">
                    <editor
                        jcr:primaryType="nt:unstructured"
                        store="[Blue,Red,Yellow]"
                        triggerAction="all"
                        typeAhead="true"
                        xtype="combo"/>
                </Color>
                <SellingSku
                    jcr:primaryType="nt:unstructured"
                    headerText="Sku Id"/>
            </colsMetadata>
        </editor>
```

### Propriétés de configuration de l’éditeur en bloc {#bulk-editor-configuration-properties}

Chaque partie de l’éditeur en bloc peut être configurée. Le tableau suivant répertorie toutes les propriétés de configuration de l’éditeur en bloc.

<table>
 <tbody>
  <tr>
   <td>Nom de la propriété</td>
   <td>Définition</td>
  </tr>
  <tr>
   <td>rootPath</td>
   <td>Chemin racine de la recherche</td>
  </tr>
  <tr>
   <td>queryParams</td>
   <td>Requête de recherche</td>
  </tr>
  <tr>
   <td>contentMode</td>
   <td>True pour activer le mode de contenu : les propriétés sont lues sur le nœud jcr:content et non sur le nœud de résultat de la recherche.</td>
  </tr>
  <tr>
   <td>colsValue</td>
   <td>Propriétés recherchées (valeurs cochées de colsSelection affichées sous forme de cases à cocher)</td>
  </tr>
  <tr>
   <td>extraCols</td>
   <td>Propriétés recherchées supplémentaires (affichées dans un champ séparé par des virgules)</td>
  </tr>
  <tr>
   <td>initialSearch</td>
   <td>True pour effectuer une requête au chargement de la page</td>
  </tr>
  <tr>
   <td>colsSelection</td>
   <td>Sélection des propriétés recherchées (affichée sous forme de cases à cocher)</td>
  </tr>
  <tr>
   <td>showGridOnly</td>
   <td>True pour afficher uniquement la grille et non le panneau de recherche (n’oubliez pas de définir initialSearch sur true)</td>
  </tr>
  <tr>
   <td>searchPanelCollapsed</td>
   <td>True pour réduire le panneau de recherche par défaut</td>
  </tr>
  <tr>
   <td>hideRootPath</td>
   <td>Masquer le champ de chemin racine</td>
  </tr>
  <tr>
   <td>hideQueryParams</td>
   <td>Masquer le champ de requête</td>
  </tr>
  <tr>
   <td>hideContentMode</td>
   <td>Masquer le champ du mode de contenu</td>
  </tr>
  <tr>
   <td>hideColsSelection</td>
   <td>Masquer le champ de sélection des protocoles</td>
  </tr>
  <tr>
   <td>hideExtraCols</td>
   <td>Masquer le champ des protocoles supplémentaires</td>
  </tr>
  <tr>
   <td>hideSearchButton</td>
   <td>Bouton Masquer la recherche</td>
  </tr>
  <tr>
   <td>hideSaveButton</td>
   <td>Bouton Masquer l’enregistrement</td>
  </tr>
  <tr>
   <td>hideExportButton</td>
   <td>Bouton Masquer l’exportation</td>
  </tr>
  <tr>
   <td>hideImportButton</td>
   <td>Bouton Masquer l’importation</td>
  </tr>
  <tr>
   <td>hideResultNumber</td>
   <td>Masquer le texte du numéro de résultat de la recherche par grille</td>
  </tr>
  <tr>
   <td>hideInsertButton</td>
   <td>Masquer le bouton d’insertion de grille</td>
  </tr>
  <tr>
   <td>hideDeleteButton</td>
   <td>Bouton Masquer la suppression de la grille</td>
  </tr>
  <tr>
   <td>hidePathCol</td>
   <td>Masquer la colonne « chemin » de la grille</td>
  </tr>
  <tr>
   <td>queryURL</td>
   <td>Chemin d’accès au servlet de requête</td>
  </tr>
  <tr>
   <td>exportURL</td>
   <td>Chemin d’accès au servlet d’exportation</td>
  </tr>
  <tr>
   <td>importURL</td>
   <td>Chemin d’accès au servlet d’importation</td>
  </tr>
  <tr>
   <td>insertedResourceType</td>
   <td>Type de ressource ajouté au nœud lorsqu’une ligne est insérée</td>
  </tr>
  <tr>
   <td>saveButton</td>
   <td>Enregistrer la configuration du widget de bouton</td>
  </tr>
  <tr>
   <td>searchButton</td>
   <td>Configuration du widget du bouton de recherche</td>
  </tr>
  <tr>
   <td>exportButton</td>
   <td>Configuration du widget du bouton Exporter</td>
  </tr>
  <tr>
   <td>importButton</td>
   <td>Configuration du widget du bouton Importer</td>
  </tr>
  <tr>
   <td>searchPanel</td>
   <td>Configuration du widget du panneau de recherche</td>
  </tr>
  <tr>
   <td>grid</td>
   <td>Configuration du widget Grille</td>
  </tr>
  <tr>
   <td>store</td>
   <td>Configuration du magasin</td>
  </tr>
  <tr>
   <td>colModel</td>
   <td>Configuration du modèle de colonne de grille</td>
  </tr>
  <tr>
   <td>rootPathInput</td>
   <td>Configuration du widget rootPath</td>
  </tr>
  <tr>
   <td>queryParamsInput</td>
   <td>Configuration du widget queryParams</td>
  </tr>
  <tr>
   <td>contentModeInput</td>
   <td>Configuration du widget contentMode</td>
  </tr>
  <tr>
   <td>colsSelectionInput</td>
   <td>colsSelection widget config</td>
  </tr>
  <tr>
   <td>extraColsInput</td>
   <td>Configuration du widget extraCols</td>
  </tr>
  <tr>
   <td>colsMetadata</td>
   <td>Configuration des métadonnées de colonne. Les propriétés possibles sont (appliquées à toutes les cellules de la colonne) : <br />
    <ul>
     <li>cellStyle : style html </li>
     <li>cellCls : classe css </li>
     <li>readOnly : true pour ne pas pouvoir modifier la valeur </li>
     <li>case à cocher : true pour définir toutes les cellules de la colonne comme cases à cocher (valeurs true/false) </li>
     <li>forcedPosition : valeur entière permettant de spécifier où la colonne doit être placée dans la grille (entre 0 et le nombre de colonnes-1)<p><br /> </p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Configuration des métadonnées des colonnes {#columns-metadata-configuration}

Vous pouvez configurer pour chaque colonne :

* les propriétés d’affichage : style html, classe CSS et lecture seule 

* une case à cocher
* une position forcée

Colonnes CSS et lecture seule

L’éditeur en bloc comporte trois configurations de colonne :

* Nom de classe CSS de la cellule (cellCls) : nom de classe CSS ajouté à chaque cellule de la colonne configurée.
* Style de cellule (cellStyle) : style de HTML ajouté à chaque cellule de la colonne configurée.
* Lecture seule (readOnly) : la lecture seule est définie pour chaque cellule de la colonne configurée.

La configuration doit être définie comme suit :

```
"colsMetadata": {
"Column name": {
     "cellStyle": "html style",
     "cellCls": "CSS class",
     "readOnly": true/false
}
}
```

L’exemple suivant se trouve dans le composant de liste de produits (/apps/geometrixx/components/productlist/dialog/items/editor/colsMetadata) :

```xml
            <colsMetadata jcr:primaryType="nt:unstructured">
                <Selection
                    jcr:primaryType="nt:unstructured"
                    checkbox="true"
                    forcedPosition="0"
                    headerText=""/>
                <ProductId
                    jcr:primaryType="nt:unstructured"
                    cellCls="productlist-cell-productid"
                    headerText="Product Id"/>
                <ProductName
                    jcr:primaryType="nt:unstructured"
                    cellStyle="background-color: #FFCC99;"
                    headerText="Product Name"/>
                <CatalogCode
                    jcr:primaryType="nt:unstructured"
                    cellStyle="background-color: #EDEDED;"
                    headerText="Catalog Code"/>
                <Color jcr:primaryType="nt:unstructured">
                    <editor
                        jcr:primaryType="nt:unstructured"
                        store="[Blue,Red,Yellow]"
                        triggerAction="all"
                        typeAhead="true"
                        xtype="combo"/>
                </Color>
                <SellingSku
                    jcr:primaryType="nt:unstructured"
                    headerText="Sku Id"/>
            </colsMetadata>
```

**Case à cocher**

Si la propriété de configuration de case à cocher est définie sur true, toutes les cellules de la colonne sont affichées sous forme de cases à cocher. Une case cochée envoie **true** au servlet Save du serveur, **false** dans le cas contraire. Dans le menu d’en-tête, vous pouvez également **tout sélectionner** ou **ne rien sélectionner**. Ces options sont activées si l’en-tête sélectionné est l’en-tête d’une colonne de case à cocher.

Dans le premier exemple, la colonne de sélection contient uniquement des cases à cocher comme case=&quot;true&quot;.

**Position forcée**

La métadonnée de position forcée forcedPosition vous permet de spécifier l’endroit où la colonne est placée dans la grille : 0 est la première place et &lt;nombre de colonnes>-1 est la dernière position. Toute autre valeur est ignorée.

Dans le premier exemple, la colonne de sélection est la première colonne sous la forme forcedPosition=&quot;0&quot;.

### Query Servlet {#query-servlet}

Par défaut, le servlet Query est disponible dans `/libs/wcm/core/components/bulkeditor/json.java`. Vous pouvez configurer un autre chemin pour récupérer les données.

Le servlet Query fonctionne comme suit : il reçoit une requête GQL et les colonnes à renvoyer, calcule les résultats et renvoie les résultats à l’éditeur en bloc sous la forme d’un flux JSON.

Dans le cas du composant Liste de produits , les deux paramètres envoyés au servlet Query sont les suivants :

* requête : &quot;chemin : /content/geometrixx/en/customers/jcr:content/par/productlist Cube&quot;
* cols : &quot;Selection,ProductId,ProductName,Color,CatalogCode,SellingSku&quot;

Et le flux JSON est renvoyé comme suit :

```
{
  "hits": [{
      "jcr:path": "/content/geometrixx/en/products/jcr:content/par/productlist/1258674828905",
      "ProductId": "21",
      "ProductName": "Cube",
      "Color": "Blue",
      "CatalogCode": "43244",
      "SellingSku": "32131"
    }
  ],
  "results": 1
}
```

Chaque accès correspond à un noeud et à ses propriétés, et s’affiche sous la forme d’une ligne dans la grille.

Vous pouvez étendre le servlet Query de sorte à renvoyer un modèle d’héritage complexe ou à renvoyer des nœuds stockés dans un emplacement logique spécifique. Le servlet Query peut être utilisé pour effectuer n’importe quel type de calcul complexe. La grille peut ensuite afficher les lignes qui sont un agrégat de plusieurs nœuds dans le référentiel. La modification et l’enregistrement de ces lignes doivent dans ce cas être gérés par le servlet Save.

### Save Servlet {#save-servlet}

Dans la configuration par défaut de l’éditeur en bloc, chaque ligne est un noeud et le chemin de ce noeud est stocké dans l’enregistrement de ligne. L’éditeur en bloc conserve le lien entre la ligne et le noeud via le chemin jcr. Lorsqu’un utilisateur modifie la grille, une liste de toutes les modifications est créée. Lorsqu’un utilisateur clique sur **Enregistrer**, une requête POST est envoyée à chaque chemin avec les valeurs de propriétés mises à jour. C’est la base du concept Sling. Ce mécanisme fonctionne bien si chaque cellule est une propriété du nœud. Mais si le servlet Query est implémenté pour effectuer le calcul d’héritage, ce modèle ne peut pas fonctionner en tant que propriété renvoyée par le servlet Query peut être héritée d’un autre noeud.

Le concept du servlet Save est le suivant : les modifications ne sont pas directement publiées sur chaque nœud, mais sont envoyées à un servlet qui effectue la tâche d’enregistrement. Cela permet à ce servlet d’analyser les modifications et d’enregistrer les propriétés sur le noeud droit.

Chaque propriété mise à jour est envoyée au servlet au format suivant :

* Nom du paramètre : &lt;chemin jcr>/&lt;nom de propriété>

  Exemple : /content/geometrixx/fr/products/jcr:content/par/productlist/1258674859000/SellingSku

* Valeur : &lt;valeur>

  Exemple : 12123

Le servlet doit connaître l’emplacement de stockage de la propriété catalogCode.

Une implémentation par défaut du servlet Save est disponible dans /libs/wcm/bulkeditor/save/POST.jsp et est utilisée dans le composant Liste de produits. Il prend tous les paramètres de la requête (au format &lt;chemin jcr>/&lt;nom de propriété>) et écrit des propriétés sur les nœuds à l’aide de l’API JCR. Il crée également un nœud s’il n’existe pas (lignes insérées dans la grille).

N’utilisez pas le code par défaut tel quel, car il réimplémente ce que le serveur fait nativement (un POST sur &lt;jcr path=&quot;&quot;>/&lt;property name=&quot;&quot;>) et n’est donc qu’un bon point de départ pour créer une servlet Save capable de gérer un modèle d’héritage de propriétés.
