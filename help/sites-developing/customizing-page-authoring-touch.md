---
title: Personnaliser la création de pages
description: Adobe Experience Manager (AEM) fournit divers mécanismes pour vous permettre de personnaliser les fonctionnalités de création de pages.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 90594588-db8e-4d4c-a208-22c1c6ea2a2d
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1339'
ht-degree: 46%

---

# Personnaliser la création de pages{#customizing-page-authoring}

>[!CAUTION]
>
>Ce document décrit comment personnaliser la création de pages dans l’IU tactile moderne et ne s’applique pas à l’IU classique.

Adobe Experience Manager (AEM) fournit divers mécanismes pour vous permettre de personnaliser la fonctionnalité de création de pages (et la fonction [consoles](/help/sites-developing/customizing-consoles-touch.md)) de votre instance de création.

* Clientlibs

  Les bibliothèques côté client vous permettent d’étendre l’implémentation par défaut pour créer de nouvelles fonctionnalités, tout en réutilisant les fonctions, objets et méthodes standard. Lors de la personnalisation, vous pouvez créer votre propre bibliothèque cliente sous `/apps.` La nouvelle bibliothèque cliente doit :

   * dépendre de la bibliothèque cliente de création `cq.authoring.editor.sites.page` ;
   * faire partie de la catégorie `cq.authoring.editor.sites.page.hook` appropriée.

* Recouvrements

  Les superpositions reposent sur des définitions de noeud et vous permettent de superposer la fonctionnalité standard (dans `/libs`) avec vos propres fonctionnalités personnalisées (dans `/apps`). Lors de la création d’une superposition, une copie 1:1 de l’original n’est pas requise, car la variable [fusion de ressources sling](/help/sites-developing/sling-resource-merger.md) autorise l’héritage.

>[!NOTE]
>
>Pour plus d’informations, voir [Jeu de documentation JS](https://developer.adobe.com/experience-manager/reference-materials/6-5/jsdoc/ui-touch/editor-core/index.html).

Elles peuvent être utilisées de différentes manières pour étendre la fonctionnalité de création de pages dans votre instance AEM. Une sélection est présentée ci-dessous (à un niveau élevé).

>[!NOTE]
>
>Pour plus d’informations, voir :
>
>* Utilisation et création [clientlibs](/help/sites-developing/clientlibs.md).
>* Utilisation et création [superpositions](/help/sites-developing/overlays.md).
>* [Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html)
>* [Structure de l’interface utilisateur tactile d’AEM](/help/sites-developing/touch-ui-structure.md) pour plus d’informations sur les zones structurelles utilisées pour la création de pages.
>


>[!CAUTION]
>
>****** Ne modifiez rien dans le chemin d’accès `/libs`. 
>
>La raison en est que le contenu de `/libs` est remplacé, la prochaine fois que vous mettez à niveau votre instance (et peut être remplacée lorsque vous appliquez un correctif ou un Feature Pack).
>
>La méthode recommandée pour la configuration et d’autres modifications est la suivante :
>
>1. Recréez l’élément requis (c’est-à-dire, tel qu’il existe dans `/libs`) sous `/apps`
>1. Apportez les modifications désirées dans `/apps`.

## Ajouter un nouveau calque (mode) {#add-new-layer-mode}

Lorsque vous modifiez une page, il existe plusieurs [modes](/help/sites-authoring/author-environment-tools.md#page-modes) disponible. Ces modes sont implémentés à l’aide de [calques](/help/sites-developing/touch-ui-structure.md#layer). Ils permettent d’accéder à différents types de fonctionnalités pour le même contenu de page. Les calques standard sont les suivants : édition, prévisualisation, annotation, développeur et ciblage.

### Exemple de calque : État de Live Copy {#layer-example-live-copy-status}

Une instance AEM standard fournit la couche MSM. Il accède aux données relatives à [gestion multisite](/help/sites-administering/msm.md) et le met en surbrillance dans le calque.

Pour l’afficher en action, vous pouvez modifier n’importe quel [Copie de langue We.Retail](/help/sites-developing/we-retail-globalized-site-structure.md) (ou toute autre page Live Copy) et sélectionnez **État de Live Copy** mode .

Vous trouverez la définition du calque MSM (pour référence) à l’emplacement suivant :

`/libs/wcm/msm/content/touch-ui/authoring/editor/js/msm.Layer.js`

### Exemple de code {#code-sample}

Il s’agit d’un exemple de package montrant comment créer un calque (mode), qui est un nouveau calque pour la vue MSM.

CODE SUR GITHUB

Vous pouvez trouver le code de cette page sur GitHub.

* [Ouvrez le projet aem-authoring-new-layer-mode sur GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode).
* Téléchargez le projet sous la forme d’[un fichier ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode/archive/master.zip).

## Ajout d’une nouvelle catégorie de sélection à l’explorateur de ressources {#add-new-selection-category-to-asset-browser}

L’explorateur de ressources affiche des ressources de différents types/catégories (par exemple, des images et des documents). Les ressources peuvent également être filtrées par ces catégories.

### Exemple de code {#code-sample-1}

`aem-authoring-extension-assetfinder-flickr` est un exemple de module montrant comment ajouter un groupe à l’outil de recherche de ressources. Cet exemple se connecte à [Flickr](https://www.flickr.com)est un flux public et les affiche dans le panneau latéral.

CODE SUR GITHUB

Vous pouvez trouver le code de cette page sur GitHub.

* [Ouvrez le projet aem-authoring-extension-assetfinder-flickr sur GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr).
* Téléchargez le projet sous la forme d’[un fichier ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr/archive/master.zip).

## Filtrage des ressources {#filtering-resources}

Lors de la création de pages, l’utilisateur doit souvent effectuer une sélection parmi des ressources (par exemple, des pages, des composants et des ressources). Cela peut prendre la forme d’une liste, par exemple, à partir de laquelle l’auteur doit choisir un élément.

Pour maintenir la liste à une taille raisonnable et adaptée au cas d’utilisation, un filtre peut être mis en oeuvre sous la forme d’un prédicat personnalisé. Par exemple, si le composant [`pathbrowser`](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html) [Granite](/help/sites-developing/touch-ui-concepts.md#granite-ui) est utilisé pour permettre à l’utilisateur de sélectionner le chemin d’accès à une ressource spécifique, les chemins d’accès présentés peuvent être filtrés comme suit :

* Mettez en œuvre le prédicat personnalisé en implémentant l’interface [`com.day.cq.commons.predicate.AbstractNodePredicate`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/predicate/package-summary.html).
* Spécifiez un nom pour le prédicat et faites-y référence lors de l’utilisation de `pathbrowser`.

Pour plus d’informations sur la création d’un prédicat personnalisé, consultez [cet article](/help/sites-developing/implementing-custom-predicate-evaluator.md).

>[!NOTE]
>
>Mettre en œuvre un prédicat personnalisé en implémentant l’interface `com.day.cq.commons.predicate.AbstractNodePredicate` est également possible dans l’IU classique.
>
>Voir [article de la base de connaissances](https://helpx.adobe.com/experience-manager/using/creating-custom-cq-tree.html) exemple d’implémentation d’un prédicat personnalisé dans l’IU classique.

## Ajouter une nouvelle action à une barre d’outils de composant {#add-new-action-to-a-component-toolbar}

Chaque composant (en général) dispose d’une barre d’outils qui permet d’accéder à un éventail d’actions pouvant être entreprises sur ce composant.

### Exemple de code {#code-sample-2}

`aem-authoring-extension-toolbar-screenshot` est un exemple de package qui montre comment créer une action de barre d’outils personnalisée pour effectuer le rendu de composants.

CODE SUR GITHUB

Vous pouvez trouver le code de cette page sur GitHub.

* [Ouvrez le projet aem-authoring-extension-toolbar-screenshot sur GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot).
* Téléchargez le projet sous la forme d’[un fichier ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot/archive/master.zip).

## Ajout d’un nouvel éditeur statique {#add-new-in-place-editor}

### Éditeur statique standard {#standard-in-place-editor}

Dans une installation AEM standard :

1. `/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js`

   Contient les définitions des différents éditeurs disponibles.

1. Il existe une connexion entre l’éditeur et chaque type de ressource (comme dans le composant) qui peut l’utiliser :

   * `cq:inplaceEditing`

     par exemple :

      * `/libs/foundation/components/text/cq:editConfig`
      * `/libs/foundation/components/image/cq:editConfig`

         * property : `editorType`

           Définit le type d’éditeur intégré utilisé lorsque la modification statique est déclenchée pour ce composant ; par exemple, `text`, `textimage`, `image`, `title`.

1. Vous pouvez configurer d’autres détails de configuration de l’éditeur à l’aide d’un `config` noeud contenant des configurations et un `plugin` pour contenir les détails de configuration du module.

   Voici un exemple de définition des proportions pour le module externe de recadrage d’image du composant d’image. En raison de la taille d’écran limitée, les proportions de recadrage ont été déplacées vers l’éditeur plein écran et ne peuvent être vues qu’à cet endroit.

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
   >AEM les rapports de recadrage, tels que définis par `ratio` sont définies comme **hauteur/largeur**. Cela diffère de la définition conventionnelle de la largeur/hauteur. Cela a été créée pour des raisons de compatibilité héritée. Les utilisateurs chargés de la création ne percevront aucune différence, à condition que vous définissiez clairement la propriété `name`, car c’est cette dernière qui s’affiche dans l’interface utilisateur.

#### Création d’un éditeur statique {#creating-a-new-in-place-editor}

Pour mettre en œuvre un nouvel éditeur statique (au sein de votre bibliothèque cliente) :

>[!NOTE]
>
>Pour obtenir un exemple, reportez-vous à :
>`/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js`

1. Implémentez les éléments suivants :

   * `setUp`
   * `tearDown`

1. Enregistrez l’éditeur (comprend le constructeur) :

   * `editor.register`

1. Fournissez la connexion entre l’éditeur et chaque type de ressource (comme dans le composant) qui peut l’utiliser.

#### Exemple de code pour la création d’un éditeur statique {#code-sample-for-creating-a-new-in-place-editor}

`aem-authoring-extension-inplace-editor` est un exemple de package montrant comment créer un éditeur statique dans AEM.

CODE SUR GITHUB

Vous pouvez trouver le code de cette page sur GitHub.

* [Ouvrez le projet aem-authoring-extension-inplace-editor sur GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor).
* Téléchargez le projet sous la forme d’[un fichier ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor/archive/master.zip).

#### Configurer plusieurs éditeurs statiques {#configuring-multiple-in-place-editors}

Il est possible de configurer un composant de sorte qu’il dispose de plusieurs éditeurs statiques. Lorsque plusieurs éditeurs statiques sont configurés, vous pouvez sélectionner le contenu approprié et ouvrir l’éditeur approprié. Pour plus d’informations, consultez [Configuration de plusieurs éditeurs statiques](/help/sites-developing/multiple-inplace-editors.md).

## Ajout d’une action Nouvelle page {#add-a-new-page-action}

Pour ajouter une nouvelle action de page à la barre d’outils de la page, par exemple une **Retour à Sites** (console).

### Exemple de code {#code-sample-3}

`aem-authoring-extension-header-backtosites` est un exemple de package qui montre comment créer une action de barre d’en-tête personnalisée pour revenir à la console Sites.

CODE SUR GITHUB

Vous pouvez trouver le code de cette page sur GitHub.

* [Ouvrez le projet aem-authoring-extension-header-backtosites sur GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites).
* Téléchargez le projet sous la forme d’[un fichier ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites/archive/master.zip).

## Personnalisation du workflow Demander l’activation {#customizing-the-request-for-activation-workflow}

Le workflow d’usine, **Demande d’activation** :

* apparaît automatiquement dans le menu approprié lorsqu’un auteur de contenu **n’a pas** les droits de réplication appropriés, mais **dispose** de l’abonnement des utilisateurs et auteurs de la gestion des ressources numériques ;

* Sinon, rien ne s’affiche, car les droits de réplication ont été supprimés.

Pour appliquer un comportement personnalisé à une telle activation, vous pouvez superposer la variable **Demande d’activation** workflow :

1. Dans `/apps`, recouvrez l’assistant **Sites** :

   `/libs/wcm/core/content/common/managepublicationwizard`

   >[!NOTE]
   >
   >Cela a pour effet de remplacer l’instance commune de :
   >
   >`/libs/cq/gui/content/common/managepublicationwizard`

1. Mettez à jour le [modèle de workflow](/help/sites-developing/workflows-models.md) et les configurations/scripts associés suivant les besoins.
1. Retirez, à tous les utilisateurs appropriés, le droit dont ils bénéficient sur l’[`replicate`action ](/help/sites-administering/security.md#actions) pour l’ensemble des pages pertinentes ; pour faire en sorte que ce workflow se déclenche comme une action par défaut lorsque l’un des utilisateurs tente de publier (ou de répliquer) une page.
