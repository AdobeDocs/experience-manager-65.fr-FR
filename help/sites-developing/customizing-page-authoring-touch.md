---
title: Personnalisation de la création de pages
seo-title: Personnalisation de la création de pages
description: AEM s’accompagne de divers mécanismes pour vous permettre de personnaliser la fonctionnalité de création de pages.
seo-description: AEM s’accompagne de divers mécanismes pour vous permettre de personnaliser la fonctionnalité de création de pages.
uuid: 9dc72d98-c5ff-4a00-b367-688ccf896526
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 6825dcd6-fa75-4410-b6b2-e7bd4a391224
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Personnalisation de la création de pages{#customizing-page-authoring}

>[!CAUTION]
>
>Ce document explique comment personnaliser la création de pages dans l’IU tactile moderne. Il ne s’applique pas à l’interface classique.

AEM s’accompagne de divers mécanismes pour vous permettre de personnaliser la fonctionnalité de création de pages (et les [consoles](/help/sites-developing/customizing-consoles-touch.md)) de votre instance de création.

* Clientlibs

    Les bibliothèques clientes (clientlibs) vous permettent d’étendre l’implémentation par défaut afin d’obtenir la nouvelle fonctionnalité, tout en réutilisant les fonctions, objets et méthodes standard. Lors de la personnalisation, vous pouvez créer votre propre bibliothèque cliente sous `/apps.` La nouvelle bibliothèque cliente doit :

   * Dépendre de la bibliothèque cliente de création `cq.authoring.editor.sites.page`
   * Faire partie de la catégorie `cq.authoring.editor.sites.page.hook`appropriée

* Recouvrements

   Overlays are based on node definitions and allow you to overlay the standard functionality (in `/libs`) with your own customized functionality (in `/apps`). Lors de la création d’une incrustation, aucune copie de l’original au format 1:1 n’est nécessaire, car [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) prend en charge l’héritage.

>[!NOTE]
>
>Pour plus d’informations, voir la [documentation JS](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/jsdoc/ui-touch/editor-core/index.html).

Ils peuvent être utilisés de différentes manières pour étendre la fonctionnalité de création de pages dans votre instance AEM. Plusieurs sont traités ci-après (à un niveau élevé).

>[!NOTE]
>
>Pour plus d’informations, voir :
>
>* Utilisation et création de [bibliothèques clientes](/help/sites-developing/clientlibs.md).
>* Utilisation et création d’[incrustations](/help/sites-developing/overlays.md).
>* [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html)
>* [Structure de l’interface utilisateur tactile d’AEM](/help/sites-developing/touch-ui-structure.md) pour plus d’informations sur les zones structurelles utilisées pour la création de pages.
>
>
Ce thème est également abordé dans la session [AEM Gems](https://docs.adobe.com/content/ddc/en/gems.html) – [Personnalisation de l’interface utilisateur pour AEM 6.0](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-user-interface-customization-for-aem6.html).

>[!CAUTION]
>
>You ***must*** not change anything in the `/libs` path.
>
>This is because the content of `/libs` is overwritten the next time you upgrade your instance (and may well be overwritten when you apply either a hotfix or feature pack).
>
>La méthode recommandée pour la configuration et d’autres modifications est la suivante :
>
>1. Recreate the required item (i.e. as it exists in `/libs`) under `/apps`
>1. Make any changes within `/apps`


## Ajout d’un nouveau calque (mode) {#add-new-layer-mode}

Lorsque vous modifiez une page, plusieurs [modes](/help/sites-authoring/author-environment-tools.md#page-modes) sont disponibles. Ces modes sont implémentés à l’aide de [calques](/help/sites-developing/touch-ui-structure.md#layer). Ils permettent d’accéder à différents types de fonctionnalités pour le même contenu de page. Les calques standard sont les suivants : édition, aperçu, annotation, développeur et ciblage.

### Exemple de calque : État de Live Copy {#layer-example-live-copy-status}

Une instance AEM standard fournit le calque MSM. Elle accède aux données associées à la [gestion multisite](/help/sites-administering/msm.md) et les met en évidence dans le calque.

To see it in action you may edit any [We.Retail language copy](/help/sites-developing/we-retail-globalized-site-structure.md) page (or any other live copy page) and select the **Live Copy Status** mode.

Vous trouverez la définition du calque MSM (pour référence) à l’emplacement suivant :

`/libs/wcm/msm/content/touch-ui/authoring/editor/js/msm.Layer.js`

### Exemple de code {#code-sample}

Il s’agit d’un exemple de module qui montre comment créer un calque (mode), qui est un nouveau calque pour la vue MSM.

CODE SUR GITHUB

Vous pouvez trouver le code de cette page sur GitHub.

* [Ouvrez le projet aem-authoring-new-layer-mode sur GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode)
* Téléchargez le projet sous la forme d’[un fichier ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode/archive/master.zip).

## Ajout d’une nouvelle catégorie de sélection à l’explorateur de ressources {#add-new-selection-category-to-asset-browser}

L’explorateur de ressources affiche les ressources de différents types/catégories (images, documents, etc.). Les ressources peuvent également être filtrées par ces catégories.

### Exemple de code {#code-sample-1}

`aem-authoring-extension-assetfinder-flickr` est un exemple de package qui montre comment ajouter un nouveau groupe à l’outil de recherche de ressources. Cet exemple se connecte au flux public de [Flickr](https://www.flickr.com) et l’affiche dans le panneau latéral.

CODE SUR GITHUB

Vous pouvez trouver le code de cette page sur GitHub.

* [Ouvrez le projet aem-authoring-extension-assetfinder-flickr sur GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr)
* Téléchargez le projet sous la forme d’[un fichier ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr/archive/master.zip).

## Filtrage des ressources {#filtering-resources}

Lors de la création de pages, vous êtes souvent amené à faire une sélection dans des ressources (pages, composants, ressources, etc.). Il peut s’agir, par exemple, d’une liste dans laquelle l’auteur doit choisir un élément.

Pour maintenir la liste à une taille raisonnable et faire en sorte qu’elle soit appropriée au scénario d’utilisation, un filtre peut être implémenté sous la forme d’un prédicat personnalisé. Par exemple, si le composant Granite[`pathbrowser`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) [](/help/sites-developing/touch-ui-concepts.md#granite-ui) est utilisé pour permettre à l’utilisateur de sélectionner le chemin d’accès à une ressource spécifique, les chemins d’accès présentés peuvent être filtrés comme suit :

* Mettez en œuvre le prédicat personnalisé en implémentant l’interface [`com.day.cq.commons.predicate.AbstractNodePredicate`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/predicate/package-summary.html).
* Spécifiez un nom pour le prédicat et faites-y référence lors de l’utilisation de `pathbrowser`.

Pour plus d’informations sur la création d’un prédicat personnalisé, consultez [cet article](/help/sites-developing/implementing-custom-predicate-evaluator.md).

>[!NOTE]
>
>Mettre en œuvre un prédicat personnalisé en implémentant l’interface `com.day.cq.commons.predicate.AbstractNodePredicate` est également possible dans l’IU classique.
>
>Consultez cet [article de la base de connaissances](https://helpx.adobe.com/experience-manager/using/creating-custom-cq-tree.html) pour obtenir un exemple d’implémentation d’un prédicat personnalisé dans l’interface utilisateur classique.

## Ajout d’une nouvelle action à une barre d’outils de composants {#add-new-action-to-a-component-toolbar}

Chaque composant (en règle générale) s’accompagne d’une barre d’outils qui permet d’accéder à un éventail d’actions auxquelles il peut être soumis.

### Exemple de code {#code-sample-2}

`aem-authoring-extension-toolbar-screenshot` est un exemple de package qui montre comment créer une action de barre d’outils personnalisée pour effectuer le rendu de composants.

CODE SUR GITHUB

Vous pouvez trouver le code de cette page sur GitHub.

* [Ouvrez le projet aem-authoring-extension-toolbar-screenshot sur GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot)
* Téléchargez le projet sous la forme d’[un fichier ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot/archive/master.zip).

## Ajout d’un nouvel éditeur statique {#add-new-in-place-editor}

### Éditeur statique standard {#standard-in-place-editor}

Dans une installation AEM standard :

1. `/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js`

   Conserve les définitions des différents éditeurs disponibles.

1. Il existe un lien entre l’éditeur et chaque type de ressource (comme dans le composant) qui peut l’utiliser :

   * `cq:inplaceEditing`

      par exemple:

      * `/libs/foundation/components/text/cq:editConfig`
      * `/libs/foundation/components/image/cq:editConfig`

         * property: `editorType`

            Defines the type of inline editor that will be used when the in-place editing is triggered for that component; e.g. `text`, `textimage`, `image`, `title`.

1. Les informations de configuration supplémentaires de l’éditeur peuvent être définies à l’aide d’un nœud `config` contenant des configurations, ainsi qu’un nœud `plugin` additionnel pour contenir les informations nécessaires à la configuration du module externe.

   Voici un exemple de définition des proportions pour le module externe de recadrage d’image du composant d’image. Notez que, dans la mesure où la taille d’écran peut être très limitée, les proportions de recadrage ont été déplacées vers l’éditeur plein écran et ne sont visibles qu’à cet endroit.

   ```xml
   <cq:inplaceEditing
           jcr:primaryType="cq:InplaceEditingConfig"
           active="{Boolean}true"
           editorType="image">
           <config jcr:primaryType="nt:unstructured">
               <plugins jcr:primaryType="nt:unstructured">
                   <crop jcr:primaryType="nt:unstructured">
                       <aspectRatios jcr:primaryType="nt:unstructured">
                           <_x0031_6-10
                               jcr:primaryType="nt:unstructured"
                               name="16 : 10"
                               ratio="0.625"/>
                       </aspectRatios>
                   </crop>
               </plugins>
           </config>
   </cq:inplaceEditing>
   ```

   >[!CAUTION]
   >
   >Nous attirons également votre attention sur le fait que, dans AEM, les rapports de recadrage, tels qu’ils sont définis par la propriété `ratio`, sont définis sous la forme **hauteur/largeur**. Cela diffère de la définition conventionnelle de la largeur/hauteur. Cette différence a été créée pour des raisons de compatibilité héritée. Les utilisateurs chargés de la création ne percevront aucune différence, à condition que vous définissiez clairement la propriété `name`, car c’est cette dernière qui s’affiche dans l’interface utilisateur.

#### Création d’un éditeur statique {#creating-a-new-in-place-editor}

Pour mettre en œuvre un nouvel éditeur statique (au sein de votre bibliothèque cliente) :

>[!NOTE]
>
>Pour obtenir un exemple, reportez-vous à la section :
>`/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js`

1. Implémentez les éléments suivants :

   * `setUp`
   * `tearDown`

1. Enregistrez l’éditeur (comprend le constructeur) :

   * `editor.register`

1. Fournissez la connexion entre l’éditeur et chaque type de ressource (comme dans le composant) qui peut l’utiliser.

#### Exemple de code pour créer un éditeur statique {#code-sample-for-creating-a-new-in-place-editor}

`aem-authoring-extension-inplace-editor` est un exemple de package montrant comment créer un éditeur statique dans AEM.

CODE SUR GITHUB

Vous pouvez trouver le code de cette page sur GitHub.

* [Ouvrez le projet aem-authoring-extension-inplace-editor sur GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor)
* Téléchargez le projet sous la forme d’[un fichier ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor/archive/master.zip).

#### Configuration de plusieurs éditeurs statiques {#configuring-multiple-in-place-editors}

Il est possible de configurer un composant afin qu’il comporte plusieurs éditeurs statiques. Lorsque plusieurs éditeurs statiques sont configurés, vous pouvez sélectionner le contenu approprié et ouvrir l’éditeur adéquat. See the [Configuring Multiple In-Place Editors](/help/sites-developing/multiple-inplace-editors.md) documentation for more information.

## Ajout d’une nouvelle action de page {#add-a-new-page-action}

Vous pouvez ajouter une action de page à la barre d’outils de la page ; **Retour aux sites** (console), par exemple.

### Exemple de code {#code-sample-3}

`aem-authoring-extension-header-backtosites` est un exemple de package qui montre comment créer une action de barre d’en-tête personnalisée pour revenir à la console Sites.

CODE SUR GITHUB

Vous pouvez trouver le code de cette page sur GitHub.

* [Ouvrez le projet aem-authoring-extension-header-backtosites sur GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites)
* Téléchargez le projet sous la forme d’[un fichier ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites/archive/master.zip).

## Personnalisation du workflow Demander l’activation {#customizing-the-request-for-activation-workflow}

Le workflow prêt à l’emploi **Demander l’activation** se déclenche automatiquement lorsqu’un auteur de contenu ne dispose pas des droits de réplication appropriés.

To have customized behavior upon such activation you can overlay the **Request for Activation** workflow:

1. Dans `/apps` l’assistant **Sites** :

   `/libs/wcm/core/content/common/managepublicationwizard`

   >[!NOTE]
   >
   >Cela a pour effet de remplacer l’instance commune de :
   >
   >`/libs/cq/gui/content/common/managepublicationwizard`

1. Update the [workflow model](/help/sites-developing/workflows-models.md) and related configurations/scripts as required.
1. Remove the right to the [ `replicate` action](/help/sites-administering/security.md#actions) from all appropriate users for all relevant pages; to have this workflow triggered as a default action when any of the users try to publish (or replicate) a page.

