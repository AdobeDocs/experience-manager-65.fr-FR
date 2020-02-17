---
title: Exportateur de page
seo-title: Exportateur de page
description: Découvrez comment utiliser l’exportateur de page d’AEM.
seo-description: Découvrez comment utiliser l’exportateur de page d’AEM.
uuid: 2ca2b8f1-c723-4e6b-8c3d-f5886cd0d3f1
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: 6ab07b5b-ee37-4029-95da-be2031779107
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Exportateur de page{#the-page-exporter}

Dans AEM, vous pouvez exporter une page sous la forme d’une page web complète, comprenant des images, des fichiers .js et des fichiers .css.

Une fois l’exportation configurée, il vous suffit de demander une page dans le navigateur en remplaçant `html` par `export.zip` dans l’URL ; vous obtenez alors un fichier compressé à télécharger contenant la page rendue au format HTML avec les ressources référencées. Tous les chemins d’accès dans la page, par exemple les chemins d’accès aux images, sont réécrits de manière à pointer vers les fichiers inclus dans le fichier compressé ou vers les ressources disponibles sur le serveur.

## Exportation d’une page {#exporting-a-page}

La procédure ci-dessous décrit comment exporter une page et considère qu’il existe un modèle de configuration de l’exportation pour votre site. Un modèle de configuration définit la méthode d’exportation d’une page. Il est spécifique à votre site. To create a configuration template refer to the [Creating a Page Exporter Configuration for your Site](#creating-a-page-exporter-configuration-for-your-site) section.

Pour exporter une page, procédez comme suit :

1. Ouvrez la page dans un navigateur. Par exemple :
1. `http://localhost:4502/content/geometrixx/en/products/triangle.html`
1. Ouvrez la boîte de dialogue Propriétés de la page, sélectionnez l’onglet **Avancé**, puis développez l’ensemble de champs **Exporter**.

1. Cliquez sur l’icône de loupe et sélectionnez un modèle de configuration. Sélectionnez le modèle **geometrixx**, car il s’agit du modèle par défaut pour le site Geometrixx. Cliquez sur **OK**.

1. Cliquez sur **OK** pour fermer la boîte de dialogue Propriétés de la page.
1. Request the page by replacing `html` with `export.zip` in the URL.

1. Download the `<page-name>.export.zip` file to your file system.

1. Dans votre système de fichiers, décompressez le fichier :

   * le fichier html de la page ( `<page-name>.html`) est disponible ci-dessous `<unzip-dir>/<page-path>`
   * Les autres ressources (fichiers .js, fichiers .css, images, etc.) se trouvent à un emplacement dépendant des paramètres du modèle d’exportation. Dans cet exemple, certaines ressources sont ci-dessous `<unzip-dir>/etc`, d’autres `<unzip-dir>/<page-path>`.

1. Open the page html file ( `<unzip-dir>/<page-path>.html`) in your browser to check the rendering.

## Création d’une configuration de l’exportateur de page pour votre site {#creating-a-page-exporter-configuration-for-your-site}

L’exportateur de page repose sur la structure de synchronisation du contenu. Les configurations disponibles dans la boîte de dialogue Propriétés de la page sont des modèles de configuration. Elles définissent toutes les dépendances nécessaires pour une page. Lorsqu’une exportation de page est déclenchée, le modèle de configuration est utilisé et le chemin de page et le chemin de conception sont appliqués dynamiquement à la configuration. Le fichier compressé est alors créé à l’aide de la fonctionnalité de synchronisation de contenu standard.

AEM comporte quelques modèles, notamment :

* A default one at `/etc/contentsync/templates/default`. Ce modèle :

   * est le modèle de secours lorsque aucun modèle de configuration ne se trouve dans le référentiel ;
   * Peut servir de base pour un nouveau modèle de configuration.

* One that is dedicated to the **Geometrixx** site, at `/etc/contentsync/templates/geometrixx`. Ce modèle peut être utilisé comme exemple pour en créer un autre.

Pour créer un modèle de configuration de l’exportateur de page, procédez comme suit :

1. In **CRXDE Lite**, create a node below `/etc/contentsync/templates`:

   * Nom :p. ex. `mysite`. Le nom s’affiche dans la boîte de dialogue Propriétés de la page lors du choix du modèle d’exportation de page.
   * Type: `nt:unstructured`

1. Below the template node, called here `mysite`, create a node structure using the configuration nodes described below.

### Nœuds de configuration de l’exportateur de page {#page-exporter-configuration-nodes}

Le modèle de configuration est constitué d’une structure de nœud. Chaque nœud possède une propriété `type` qui définit une action spécifique dans le processus de création du fichier compressé. Pour plus d’informations sur la propriété type, voir la section Présentation des types de configuration dans la page de structure de synchronisation de contenu.

Les nœuds ci-dessous peuvent être utilisés pour créer un modèle de configuration d’exportation :

**noeud** de page Le noeud de page est utilisé pour copier le code html de la page dans le fichier zip. Il possède les caractéristiques suivantes :

* C’est un nœud obligatoire.
* Se trouve en dessous `/etc/contentsync/templates/<sitename>`.
* Its name is `page`.
* Its node type is `nt:unstructured`

Le nœud `page` possède les propriétés suivantes :

* A `type` property set with the value `pages`.

* Il ne comporte pas de propriété `path`, car le chemin d’accès actuel à la page est copié dynamiquement dans la configuration.

* Les autres propriétés sont décrites dans la section Présentation des types de configuration de la structure Content Sync.

**noeud** de réécriture Le noeud de réécriture définit la manière dont les liens sont réécrits dans la page exportée. Les liens réécrits peuvent pointer vers les fichiers inclus dans le fichier compressé ou vers les ressources sur le serveur.

Consultez la page Synchronisation du contenu pour obtenir une description exhaustive du nœud `rewrite`.

**noeud** de conception Le noeud de conception est utilisé pour copier la conception utilisée pour la page exportée. Il possède les caractéristiques suivantes :

* Il est facultatif.
* Se trouve en dessous `/etc/contentsync/templates/<sitename>`.
* Its name is `design`.
* Its node type is `nt:unstructured`.

Le nœud `design` possède les propriétés suivantes :

* A `type` property set to the value `copy`.

* Il ne comporte pas de propriété `path`, car le chemin d’accès actuel à la page est copié dynamiquement dans la configuration.

**noeud** générique Un noeud générique est utilisé pour copier des ressources telles que des fichiers clientlibs.js ou .css dans le fichier zip. Il possède les caractéristiques suivantes :

* Il est facultatif.
* Se trouve en dessous `/etc/contentsync/templates/<sitename>`.
* Il ne possède pas de domaine spécifique.
* Its node type is `nt:unstructured`.
* Has a `type` property and any `type` related properties as defined in the Overview of configuration types section of the Content Sync framework.

Par exemple, le nœud de configuration ci-dessous copie les fichiers .js des bibliothèques clientes geometrixx dans le fichier compressé :

```xml
"geometrixx.clientlibs.js": {
    "extension": "js",
    "type": "clientlib",
    "path": "/etc/designs/geometrixx/clientlibs",
    "jcr:primaryType": "nt:unstructured"
}
```

Le modèle de configuration de l’exportation de page **Geometrixx** explique comment vous pouvez configurer une exportation de page. Pour afficher la structure du nœud du modèle dans le navigateur au format JSON, demandez l’adresse URL suivante :

`http://localhost:4502/etc/contentsync/templates/geometrixx.-1.json`

**Mise en œuvre d’une configuration personnalisée**

Comme vous l’avez peut-être constaté dans la structure du nœud, le modèle de configuration de l’exportation de page **Geometrixx** comporte un nœud `logo` avec une propriété `type` définie sur `image`. Il s’agit d’un type de configuration spécial, créé pour copier le logo de l’image dans le fichier compressé. Pour respecter certaines exigences spécifiques, il vous faudra peut-être mettre en œuvre une propriété `type` personnalisée : à cet effet, consultez la section Mise en œuvre d’un gestionnaire de mise à jour personnalisé dans la page Synchronisation du contenu.

## Exportation d’une page par programmation {#programmatically-exporting-a-page}

Pour exporter une page par programmation, vous pouvez utiliser le service OSGi [PageExporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/wcm/contentsync/PageExporter.html). Ce service permet ce qui suit :

* exporter une page et écrire la réponse du servlet HTTP ;
* exporter une page et enregistrer le fichier compressé à un emplacement spécifique.

Le servlet lié au sélecteur `export` et à l’extension `zip` utilise le service PageExporter.

## Résolution des incidents {#troubleshooting}

If you experience a problem with the download of the zip file, you may delete the `/var/contentsync` node in the repository and send the export request again.

