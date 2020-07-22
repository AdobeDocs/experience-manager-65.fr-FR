---
title: Exportateur de page
description: Découvrez comment utiliser l’exportateur de page d’AEM.
translation-type: tm+mt
source-git-commit: b0126894dec33648a24c0308972aa5b47d7e4b84
workflow-type: tm+mt
source-wordcount: '1052'
ht-degree: 26%

---


# Exportateur de page{#the-page-exporter}

AEM allows you to export a page as a complete web page including images, `.js` and `.css` files.

Une fois configurée, vous demandez une exportation de page à partir de votre navigateur en la remplaçant `html` par `export.zip` dans l’URL. Ceci génère un fichier d’archive (zip) contenant la page rendue au format html, ainsi que les ressources référencées. Tous les chemins de la page (par exemple, les chemins d’accès aux images) sont réécrits pour pointer vers les fichiers inclus dans l’archive ou vers les ressources du serveur. Le fichier d’archive (zip) peut ensuite être téléchargé à partir de votre navigateur.

>!![NOTE]
Selon votre navigateur et les paramètres, le téléchargement sera soit :
* un fichier d&#39;archive (`<page-name>.export.zip`)
* un dossier (`<page-name>`); en fait, le fichier d&#39;archive a déjà été développé


## Exportation d’une page {#exporting-a-page}

La procédure ci-dessous décrit comment exporter une page et considère qu’il existe un modèle de de l’exportation pour votre site. Un modèle d’exportation définit la manière dont une page est exportée et est spécifique à votre site. To create an export template refer to the [Creating a Page Exporter Configuration for your Site](#creating-a-page-exporter-configuration-for-your-site) section.

Pour exporter une page, procédez comme suit :

1. Accédez à la page requise dans la console **Sites** .

1. Sélectionnez la page, puis ouvrez la boîte de dialogue **Propriétés** .

1. Sélectionnez l’onglet **Avancé**.

1. Développez le champ **Exporter** pour sélectionner un modèle d’exportation.
Sélectionnez le modèle requis pour votre site, puis confirmez avec **OK**.

1. Sélectionnez **Enregistrer et fermer** pour fermer la boîte de dialogue des propriétés de page.

1. Demandez la page à exporter en remplaçant le suffixe `html` par `export.zip` dans l’URL.

   Par exemple :
   * localhost:4502/content/we-retail/language-masters/en.html

   Est accessible via :
   * localhost:4502/content/we-retail/language-masters/en.export.zip


1. Téléchargez le fichier d’archive sur votre système de fichiers.

1. Dans votre système de fichiers, décompressez le fichier si nécessaire. Une fois développé, il y aura un dossier portant le même nom que la page sélectionnée. Ce dossier contient :

   * le sous-dossier `content`, qui est la racine d’une série de sous-dossiers qui reflètent le chemin d’accès à la page dans le référentiel.

      * dans cette structure, il y a le fichier html pour la page sélectionnée (`<page-name>.html`)
   * autres ressources (`.js` fichiers, `.css` fichiers, images, etc.) sont situés en fonction des paramètres définis dans le modèle d’exportation.


1. Open the page html file (`<unzip-dir>/<path>/<to>/<page>/<page-path>.html`) in your browser to check the rendering.

## Création d’une configuration de l’exportateur de page pour votre site {#creating-a-page-exporter-configuration-for-your-site}

The page exporter is based on the [Content Sync framework](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/package-summary.html). Les configurations disponibles dans la boîte de dialogue Propriétés **de la** page sont des modèles d’exportation qui définissent les dépendances requises pour une page.

Lorsqu’une exportation de page est déclenchée, le modèle d’exportation est référencé et le chemin de page et le chemin de conception sont appliqués dynamiquement. Le fichier compressé est alors créé à l’aide de la fonctionnalité de synchronisation de contenu standard.

Une installation prête à l’emploi d’AEM comprend un modèle par défaut sous `/etc/contentsync/templates/default`.

* Il s’agit du modèle de secours lorsqu’aucun modèle d’exportation n’est trouvé dans le référentiel.

* Le `default` modèle montre comment une exportation de page peut être configurée, de sorte qu&#39;il puisse servir de base pour un nouveau modèle d&#39;exportation.

* Pour vue de la structure des noeuds du modèle dans votre navigateur au format JSON, demandez l’URL suivante :
   `http://localhost:4502/etc/contentsync/templates/default.json`

La méthode la plus simple pour créer un nouveau modèle d&#39;exportateur de pages consiste à :

* copier le `default` modèle,

* attribuez un nouveau nom, approprié à votre site,

* puis effectuez les mises à jour requises.

Pour créer un modèle entièrement nouveau :

1. In **CRXDE Lite**, create a node below `/etc/contentsync/templates`:

   * `Name`: un nom approprié à votre site ; par exemple, `<mysite>`. Le nom s’affiche dans la boîte de dialogue des propriétés de la page lors du choix du modèle d’exportateur de page.

   * `Type`: `nt:unstructured`

2. Below the template node, called here `mysite`, create a node structure using the configuration nodes described below.

## Activation d&#39;un modèle d&#39;exportateur de pages pour vos pages {#activating-a-page-exporter-configuration-for-your-pages}

Une fois votre modèle configuré, vous devez le rendre disponible :

1. Dans CRXDE, accédez à la page requise de la `/content` branche.

1. Sur le `jcr:content` noeud de la page, créez la propriété :
   * `Name`: `cq:exportTemplate`
   * `Type`: `String`
   * `Value`: chemin d’accès au modèle ; par exemple : `/etc/contentsync/templates/mysite`

### Nœuds de configuration de l’exportateur de page {#page-exporter-configuration-nodes}

Le modèle est constitué d’une structure de noeuds, dans la mesure où il utilise la structure [de synchronisation de](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/package-summary.html)contenu.  Chaque nœud possède une propriété `type` qui définit une action spécifique dans le processus de création du fichier compressé.

<!-- For more details about the type property, refer to the Overview of configuration types section in the Content Sync framework page.
-->

Les nœuds ci-dessous peuvent être utilisés pour créer un modèle de d’exportation :

* `page`Le nœud page est utilisé pour copier le code HTML de la page dans le fichier compressé. Il possède les caractéristiques suivantes :

   * C’est un nœud obligatoire.
   * Se trouve en dessous `/etc/contentsync/templates/<mysite>`.
   * Est défini avec la propriété `Name`définie sur `page`.
   * Le type de noeud est `nt:unstructured`

   Le nœud `page` possède les propriétés suivantes :

   * A `type` property set with the value `pages`.

   * Il ne comporte pas de propriété `path`, car le chemin d’accès actuel à la page est copié dynamiquement dans la configuration.

   <!--
  * The other properties are described in the Overview of configuration types section of the Content Sync framework.
  -->

* `rewrite`Le nœud rewrite définit la façon dont les liens sont réécrits dans la page exportée. Les liens réécrits peuvent pointer vers les fichiers inclus dans le fichier compressé ou vers les ressources sur le serveur.
   <!-- Please refer to the Content Sync page for a complete description of the `rewrite` node. -->

* `design`Le nœud design est utilisé pour copier la conception utilisée pour la page exportée. Il possède les caractéristiques suivantes :

   * Il est facultatif.
   * Se trouve en dessous `/etc/contentsync/templates/<mysite>`.
   * Est défini avec la propriété `Name` définie sur `design`.
   * Le type de noeud est `nt:unstructured`.

   Le nœud `design` possède les propriétés suivantes :

   * A `type` property set to the value `copy`.

   * It does not have a `path` property, as the current page path is dynamically copied to the configuration.


* `generic`
Un noeud générique est utilisé pour copier des ressources telles que clientlibs 
`.js` ou `.css` des fichiers au fichier zip. Il possède les caractéristiques suivantes :

   * Il est facultatif.
   * Se trouve en dessous `/etc/contentsync/templates/<mysite>`.
   * Il ne possède pas de domaine spécifique.
   * Le type de noeud est `nt:unstructured`.
   * Comporte une `type` propriété et des propriétés `type` connexes. <!--Has a `type` property and any `type` related properties as defined in the Overview of configuration types section of the Content Sync framework.-->

   For example the following configuration node copies the `mysite.clientlibs.js` files to the zip file:

   ```xml
   "mysite.clientlibs.js": {
       "extension": "js",
       "type": "clientlib",
       "path": "/etc/designs/mysite/clientlibs",
       "jcr:primaryType": "nt:unstructured"
   }
   ```

**Mise en œuvre d’une configuration personnalisée**

Des configurations personnalisées sont également possibles.

<!--
As you may have noticed in the node structure, the **Geometrixx** page export template has a `logo` node with a `type` property set to `image`. This is a special configuration type that has been created to copy the image logo to the zip file. 
-->

Pour répondre à certaines exigences spécifiques, vous devrez peut-être implémenter un gestionnaire [de mise à jour](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/handler/package-summary.html)personnalisé.

<!-- To meet some specific requirements, you may need to implement a custom `type` property: to do so, refer to the Implementing a custom update handler section in the Content Sync page.
-->

## Exportation d’une page par programmation {#programmatically-exporting-a-page}

Pour exporter une page par programmation, vous pouvez utiliser le service OSGi [PageExporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/wcm/contentsync/PageExporter.html). Ce service permet ce qui suit :

* exporter une page et écrire la réponse du servlet HTTP ;
* exporter une page et enregistrer le fichier compressé à un emplacement spécifique.

Le servlet lié au sélecteur `export` et à l’extension `zip` utilise le service PageExporter.

## Résolution des incidents {#troubleshooting}

If you experience a problem with the download of the zip file, you may delete the `/var/contentsync` node in the repository and send the export request again.
