---
title: Exportateur de page
description: Découvrez comment utiliser l’exporteur de page Adobe Experience Manager (AEM).
exl-id: 15d08758-cf75-43c0-9818-98a579d64183
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '997'
ht-degree: 100%

---

# Exportateur de page{#the-page-exporter}

Adobe Experience Manager (AEM) vous permet d’exporter une page sous la forme d’une page web complète comprenant des images et des fichiers `.js` et `.css`.

Une fois la configuration effectuée, il vous suffit de demander un export de page à partir de votre navigateur en remplaçant `html` par `export.zip` dans l’URL. Cette opération génère un fichier d’archive (zip) contenant la page rendue au format html, ainsi que les ressources référencées. Tous les chemins d’accès dans la page (par exemple, d’accès aux images) sont réécrits de manière à pointer vers les fichiers inclus dans le fichier compressé ou vers les ressources disponibles sur le serveur. Le fichier d’archive (zip) peut ensuite être téléchargé à partir de votre navigateur.

>[!NOTE]
>
>Selon votre navigateur et les paramètres, le téléchargement est :
>
>* un fichier d’archive (`<page-name>.export.zip`) ;
>* un dossier (`<page-name>`) ; en fait, le fichier d’archive a déjà été développé.

## Exportation d’une page {#exporting-a-page}

La procédure ci-dessous décrit comment exporter une page et considère qu’il existe un modèle d’exportation pour votre site. Un modèle d’export définit la manière dont votre page est exportée. Il est spécifique à votre site. Pour créer un modèle d’export, consultez [Création de la configuration d’un exporteur de page pour votre site](#creating-a-page-exporter-configuration-for-your-site).

Pour exporter une page, procédez comme suit :

1. Accédez à la page requise dans la console **Sites**.

1. Sélectionnez la page, puis ouvrez la boîte de dialogue **Propriétés**.

1. Sélectionnez l’onglet **Avancé**.

1. Développez le champ **Exporter** pour sélectionner un modèle d’exportation.
Sélectionnez le modèle requis pour votre site, puis confirmez avec **OK**.

1. Sélectionnez **Enregistrer et fermer** pour fermer la boîte de dialogue des propriétés de la page.

1. Faites une demande d’export de la page, en remplaçant le suffixe `html` avec `export.zip` dans l’URL.

   Par exemple :
   * localhost:4502/content/we-retail/language-masters/en.html

   Accessible via :
   * localhost:4502/content/we-retail/language-masters/en.export.zip

1. Téléchargez l’archive dans votre système de fichiers. 

1. Dans votre système de fichiers, décompressez le fichier si nécessaire. Une fois développé, un dossier portant le même nom que la page sélectionnée s’affiche. Ce dossier contient les éléments suivants :

   * Le sous-dossier `content`, qui est la racine d’une série de sous-dossiers reflétant le chemin d’accès à la page dans le référentiel.

      * Cette structure comprend le fichier html pour la page sélectionnée (`<page-name>.html`).

   * D’autres ressources (fichiers `.js`, fichiers `.css`, images, etc.) sont localisées en fonction des paramètres du modèle d’export.

1. Ouvrez le fichier HTML de la page (`<unzip-dir>/<path>/<to>/<page>/<page-path>.html`) dans votre navigateur pour contrôler le rendu.

## Création d’une configuration de l’exportateur de page pour votre site {#creating-a-page-exporter-configuration-for-your-site}

L’exportateur de page repose sur le [framework de synchronisation du contenu. ](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/contentsync/package-summary.html) Les configurations disponibles dans la boîte de dialogue **Propriétés de la page** sont des modèles d’exportation qui définissent les dépendances requises pour une page.

Au déclenchement d’un export de page, le modèle de configuration est utilisé. Les chemins d’accès à la page et à la conception s’appliquent dynamiquement à la configuration. Le fichier compressé est alors créé à l’aide de la fonctionnalité de synchronisation de contenu standard.

Une installation AEM prête à l’emploi comprend un modèle par défaut sous `/etc/contentsync/templates/default`.

* Ce modèle est le modèle de secours à utiliser lorsqu’aucun modèle d’exportation n’est trouvé dans le référentiel.

* Le modèle `default` vous indique comment une exportation de page peut être configurée, afin de servir de base à un nouveau modèle d’exportation.

* Pour afficher la structure du nœud du modèle dans le navigateur au format JSON, demandez l’adresse URL suivante :
  `http://localhost:4502/etc/contentsync/templates/default.json`

La méthode la plus simple pour créer un modèle d’exporteur de page consiste à :

* copier le modèle `default` ;

* lui attribuer un nouveau nom, approprié à votre site ;

* effectuer ensuite les mises à jour requises.

Pour créer un modèle totalement nouveau :

1. Dans **CRXDE Lite**, créez un nœud sous `/etc/contentsync/templates` :

   * `Name` : un nom approprié à votre site ; par exemple, `<mysite>`. Le nom s’affiche dans la boîte de dialogue Propriétés de la page lorsque vous sélectionnez le modèle de l’exportateur de page.

   * `Type`: `nt:unstructured`

2. Sous le nœud de modèle, appelé ici `mysite`, créez une structure de nœud à l’aide des nœuds de configuration décrits ci-dessous.

## Activation d’un modèle d’exportateur de page pour vos pages {#activating-a-page-exporter-configuration-for-your-pages}

Une fois votre modèle configuré, rendez-le disponible :

1. Dans CRXDE, accédez à la page requise dans la branche `/content`. Il peut s’agir d’une page individuelle ou de la page racine d’une sous-arborescence.

1. Sur le nœud `jcr:content` de la page, créez la propriété :
   * `Name`: `cq:exportTemplate`
   * `Type`: `String`
   * `Value` : chemin d’accès au modèle ; par exemple : `/etc/contentsync/templates/mysite`

### Nœuds de configuration de l’exportateur de page {#page-exporter-configuration-nodes}

Le modèle se compose d’une structure de nœud, dans la mesure où il utilise le [Framework de synchronisation de contenu](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/contentsync/package-summary.html). Chaque nœud possède une propriété `type` qui définit une action spécifique dans le processus de création du fichier compressé.

<!-- For more details about the type property, see the Overview of configuration types section in the Content Sync framework page.
-->

Les nœuds ci-dessous peuvent être utilisés pour créer un modèle de d’exportation :

* `page`
Le nœud page est utilisé pour copier le code HTML de la page dans le fichier compressé. Il possède les caractéristiques suivantes :

   * Nœud obligatoire.
   * Situé sous `/etc/contentsync/templates/<mysite>`.
   * Est défini avec la propriété `Name` définie sur `page`.
   * Le type de nœud est `nt:unstructured`.

  Le nœud `page` possède les propriétés suivantes :

   * Une propriété `type` définie avec la valeur `pages`.

   * Il ne comporte pas de propriété `path`, car le chemin d’accès actuel à la page est copié dynamiquement dans la configuration.
  <!--
  * The other properties are described in the Overview of configuration types section of the Content Sync framework.
  -->

* `rewrite`
Le nœud rewrite définit la façon dont les liens sont réécrits dans la page exportée. Les liens réécrits peuvent pointer vers les fichiers inclus dans le fichier compressé ou vers les ressources sur le serveur.
  <!-- See the Content Sync page for a complete description of the `rewrite` node. -->

* `design`
Le nœud design est utilisé pour copier la conception utilisée pour la page exportée. Il possède les caractéristiques suivantes :

   * Facultatif.
   * Situé sous `/etc/contentsync/templates/<mysite>`.
   * Est défini avec la propriété `Name` définie sur `design`.
   * Le type de nœud est `nt:unstructured`.

  Le nœud `design` possède les propriétés suivantes :

   * Une propriété `type` définie avec la valeur `copy`.

   * Il ne comporte pas de propriété `path`, car le chemin d’accès actuel à la page est copié dynamiquement dans la configuration.

* `generic`
Un nœud générique sert à copier des ressources telles que des fichiers `.js` ou `.css` de bibliothèques clientes dans le fichier zip. Il possède les caractéristiques suivantes :

   * Facultatif.
   * Situé sous `/etc/contentsync/templates/<mysite>`.
   * Aucun nom spécifique.
   * Le type de nœud est `nt:unstructured`.
   * Comporte une propriété `type` et des propriétés `type` connexes. <!--Has a `type` property and any `type` related properties as defined in the Overview of configuration types section of the Content Sync framework.-->

  Par exemple, le nœud de configuration ci-dessous copie les fichiers `mysite.clientlibs.js` dans le fichier zip :

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

Pour répondre à certaines exigences spécifiques, implémentez un [gestionnaire de mise à jour personnalisé](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/contentsync/handler/package-summary.html).

<!-- To meet some specific requirements, you may need to implement a custom `type` property. To do so, see the Implementing a custom update handler section in the Content Sync page.
-->

## Exporter une page par programmation {#programmatically-exporting-a-page}

Pour exporter une page par programmation, vous pouvez utiliser le service OSGi [PageExporter](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/index.html?com/day/cq/wcm/contentsync/PageExporter.html). Ce service permet d’effectuer les opérations suivantes :

* Exportez une page et écrivez dans la réponse du servlet HTTP.
* Exportez une page et enregistrez le fichier zip à un emplacement spécifique.

Le servlet lié au sélecteur `export` et à l’extension `zip` utilise le service PageExporter.

## Résolution des problèmes {#troubleshooting}

Si vous rencontrez un problème lors du téléchargement du fichier compressé, supprimez le nœud `/var/contentsync` du référentiel et renvoyez la demande d’exportation.
