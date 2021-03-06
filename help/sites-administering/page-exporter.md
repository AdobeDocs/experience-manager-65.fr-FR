---
title: Exportateur de page
description: Découvrez comment utiliser l’exportateur de page d’AEM.
exl-id: 15d08758-cf75-43c0-9818-98a579d64183
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1065'
ht-degree: 30%

---

# Exportateur de page{#the-page-exporter}

AEM vous permet d’exporter une page sous la forme d’une page web complète comprenant des images, des fichiers `.js` et `.css`.

Une fois la configuration effectuée, vous demandez l’exportation d’une page à partir de votre navigateur en remplaçant `html` par `export.zip` dans l’URL. Cette opération génère un fichier d’archive (zip) contenant la page rendue au format html, ainsi que les ressources référencées. Tous les chemins d’accès de la page (par exemple, les chemins d’accès aux images) sont réécrits afin de pointer vers les fichiers inclus dans l’archive ou vers les ressources du serveur. Le fichier d’archive (zip) peut ensuite être téléchargé à partir de votre navigateur.

>[!NOTE]
>
>Selon votre navigateur et les paramètres, le téléchargement sera :
>* un fichier d’archive (`<page-name>.export.zip`) ;
>* un dossier (`<page-name>`); en fait, le fichier d’archive a déjà été développé.


## Exportation d’une page {#exporting-a-page}

La procédure ci-dessous décrit comment exporter une page et considère qu’il existe un modèle de de l’exportation pour votre site. Un modèle d’exportation définit la manière dont une page est exportée et est spécifique à votre site. Pour créer un modèle d’exportation, reportez-vous à la section [Création d’une configuration d’exportateur de page pour votre site](#creating-a-page-exporter-configuration-for-your-site) .

Pour exporter une page, procédez comme suit :

1. Accédez à la page requise dans la console **Sites**.

1. Sélectionnez la page, puis ouvrez la boîte de dialogue **Propriétés**.

1. Sélectionnez l’onglet **Avancé**.

1. Développez le champ **Export** pour sélectionner un modèle d&#39;export.
Sélectionnez le modèle requis pour votre site, puis confirmez avec **OK**.

1. Sélectionnez **Enregistrer et fermer** pour fermer la boîte de dialogue des propriétés de la page.

1. Demandez la page à exporter, en remplaçant le suffixe `html` par `export.zip` dans l’URL.

   Par exemple :
   * localhost:4502/content/we-retail/language-masters/en.html

   Est accessible via :
   * localhost:4502/content/we-retail/language-masters/en.export.zip


1. Téléchargez le fichier d’archive sur votre système de fichiers.

1. Dans votre système de fichiers, décompressez le fichier si nécessaire. Une fois développé, un dossier portant le même nom que la page sélectionnée s’affiche. Ce dossier contient :

   * le sous-dossier `content`, qui est la racine d’une série de sous-dossiers qui reflètent le chemin d’accès à la page dans le référentiel.

      * dans cette structure, il existe le fichier html pour la page sélectionnée (`<page-name>.html`).
   * autres ressources (`.js` fichiers, `.css` fichiers, images, etc.) se situent en fonction des paramètres du modèle d’exportation.


1. Ouvrez le fichier HTML de la page (`<unzip-dir>/<path>/<to>/<page>/<page-path>.html`) dans votre navigateur pour vérifier le rendu.

## Création d’une configuration de l’exportateur de page pour votre site {#creating-a-page-exporter-configuration-for-your-site}

L’exportateur de page est basé sur la [structure de synchronisation de contenu](https://helpx.adobe.com/fr/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/package-summary.html). Les configurations disponibles dans la boîte de dialogue **Propriétés de page** sont des modèles d’exportation qui définissent les dépendances requises pour une page.

Lorsqu’une exportation de page est déclenchée, le modèle d’exportation est référencé et le chemin de page et le chemin de conception sont appliqués dynamiquement. Le fichier compressé est alors créé à l’aide de la fonctionnalité de synchronisation de contenu standard.

Une installation AEM prête à l’emploi comprend un modèle par défaut sous `/etc/contentsync/templates/default`.

* Ce modèle est le modèle de secours lorsqu’aucun modèle d’exportation n’est trouvé dans le référentiel.

* Le modèle `default` indique comment une exportation de page peut être configurée, afin de servir de base à un nouveau modèle d’exportation.

* Pour afficher la structure de noeud du modèle dans votre navigateur au format JSON, demandez l’URL suivante :
   `http://localhost:4502/etc/contentsync/templates/default.json`

La méthode la plus simple pour créer un modèle d’exportateur de page consiste à :

* copier le modèle `default`,

* attribuer un nouveau nom, approprié à votre site,

* effectuez ensuite les mises à jour requises.

Pour créer un modèle totalement nouveau :

1. Dans **CRXDE Lite**, créez un noeud sous `/etc/contentsync/templates` :

   * `Name`: un nom approprié à votre site ; par exemple,  `<mysite>`. Le nom apparaît dans la boîte de dialogue Propriétés de la page lors du choix du modèle d’exportateur de page.

   * `Type`: `nt:unstructured`

2. Sous le noeud de modèle, appelé ici `mysite`, créez une structure de noeud à l’aide des noeuds de configuration décrits ci-dessous.

## Activation d’un modèle d’exportateur de page pour vos pages {#activating-a-page-exporter-configuration-for-your-pages}

Une fois votre modèle paramétré, vous devez le rendre disponible :

1. Dans CRXDE, accédez à la page requise dans la branche `/content`. Il peut s’agir d’une page individuelle ou de la page racine d’une sous-arborescence.

1. Sur le noeud `jcr:content` de la page, créez la propriété :
   * `Name`:  `cq:exportTemplate`
   * `Type`:  `String`
   * `Value`: chemin d’accès au modèle ; par exemple :  `/etc/contentsync/templates/mysite`

### Nœuds de configuration de l’exportateur de page {#page-exporter-configuration-nodes}

Le modèle se compose d’une structure de noeud, car il utilise la [structure de synchronisation de contenu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/package-summary.html).  Chaque nœud possède une propriété `type` qui définit une action spécifique dans le processus de création du fichier compressé.

<!-- For more details about the type property, refer to the Overview of configuration types section in the Content Sync framework page.
-->

Les nœuds ci-dessous peuvent être utilisés pour créer un modèle de d’exportation :

* `page`Le nœud page est utilisé pour copier le code HTML de la page dans le fichier compressé. Il possède les caractéristiques suivantes :

   * C’est un nœud obligatoire.
   * Se trouve sous `/etc/contentsync/templates/<mysite>`.
   * Est défini avec la propriété `Name`définie sur `page`.
   * Le type de noeud est `nt:unstructured`

   Le nœud `page` possède les propriétés suivantes :

   * Une propriété `type` définie avec la valeur `pages`.

   * Il ne comporte pas de propriété `path`, car le chemin d’accès actuel à la page est copié dynamiquement dans la configuration.

   <!--
  * The other properties are described in the Overview of configuration types section of the Content Sync framework.
  -->

* `rewrite`Le nœud rewrite définit la façon dont les liens sont réécrits dans la page exportée. Les liens réécrits peuvent pointer vers les fichiers inclus dans le fichier compressé ou vers les ressources sur le serveur.
   <!-- Please refer to the Content Sync page for a complete description of the `rewrite` node. -->

* `design`Le nœud design est utilisé pour copier la conception utilisée pour la page exportée. Il possède les caractéristiques suivantes :

   * Il est facultatif.
   * Se trouve sous `/etc/contentsync/templates/<mysite>`.
   * Est défini avec la propriété `Name` définie sur `design`.
   * Le type de noeud est `nt:unstructured`.

   Le nœud `design` possède les propriétés suivantes :

   * Une propriété `type` définie sur la valeur `copy`.

   * Il ne possède pas de propriété `path`, car le chemin de page actuel est copié dynamiquement dans la configuration.


* `generic`
Un noeud générique est utilisé pour copier des ressources telles que clientlibs. 
`.js` ou  `.css` au fichier zip. Il possède les caractéristiques suivantes :

   * Il est facultatif.
   * Se trouve sous `/etc/contentsync/templates/<mysite>`.
   * Il ne possède pas de domaine spécifique.
   * Le type de noeud est `nt:unstructured`.
   * Possède une propriété `type` et des propriétés `type` associées. <!--Has a `type` property and any `type` related properties as defined in the Overview of configuration types section of the Content Sync framework.-->

   Par exemple, le noeud de configuration suivant copie les fichiers `mysite.clientlibs.js` dans le fichier zip :

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

Pour répondre à certaines exigences spécifiques, vous devrez peut-être implémenter un [gestionnaire de mise à jour personnalisé](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/handler/package-summary.html).

<!-- To meet some specific requirements, you may need to implement a custom `type` property: to do so, refer to the Implementing a custom update handler section in the Content Sync page.
-->

## Exportation d’une page par programmation {#programmatically-exporting-a-page}

Pour exporter une page par programmation, vous pouvez utiliser le service OSGi [PageExporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/wcm/contentsync/PageExporter.html). Ce service permet ce qui suit :

* exporter une page et écrire la réponse du servlet HTTP ;
* exporter une page et enregistrer le fichier compressé à un emplacement spécifique.

Le servlet lié au sélecteur `export` et à l’extension `zip` utilise le service PageExporter.

## Résolution des problèmes {#troubleshooting}

Si vous rencontrez un problème lors du téléchargement du fichier zip, vous pouvez supprimer le noeud `/var/contentsync` dans le référentiel et envoyer à nouveau la demande d’exportation.
