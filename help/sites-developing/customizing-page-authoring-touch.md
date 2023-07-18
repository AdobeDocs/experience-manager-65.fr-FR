---
title: Personnaliser la création de pages
seo-title: Customizing Page Authoring
description: AEM fournit divers mécanismes pour vous permettre de personnaliser les fonctionnalités de création de pages.
seo-description: AEM provides various mechanisms to enable you to customize page authoring functionality
uuid: 9dc72d98-c5ff-4a00-b367-688ccf896526
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 6825dcd6-fa75-4410-b6b2-e7bd4a391224
exl-id: 90594588-db8e-4d4c-a208-22c1c6ea2a2d
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '1357'
ht-degree: 65%

---

# Personnaliser la création de pages{#customizing-page-authoring}

>[!CAUTION]
>
>Ce document décrit comment personnaliser la création de pages dans l’IU tactile moderne et ne s’applique pas à l’IU classique.

AEM fournit divers mécanismes pour vous permettre de personnaliser la fonctionnalité de création de pages (et la fonction [consoles](/help/sites-developing/customizing-consoles-touch.md)) de votre instance de création.

* Clientlibs

   Les bibliothèques clientes (clientlibs) vous permettent d’étendre l’implémentation par défaut afin d’obtenir la nouvelle fonctionnalité, tout en réutilisant les fonctions, objets et méthodes standard. Lors de la personnalisation, vous pouvez créer votre propre bibliothèque cliente sous `/apps.` La nouvelle bibliothèque cliente doit :

   * dépendre de la bibliothèque cliente de création `cq.authoring.editor.sites.page` ;
   * faire partie de la catégorie `cq.authoring.editor.sites.page.hook` appropriée.

* Recouvrements

  Les recouvrements sont basés sur les définitions de nœuds et vous permettent de recouvrir la fonctionnalité standard (dans `/libs`) avec votre propre fonctionnalité personnalisée (dans `/apps`). Lors de la création d’une superposition, une copie 1:1 de l’original n’est pas nécessaire, car la fonction [fusion de ressources sling](/help/sites-developing/sling-resource-merger.md) autorise l’héritage.

>[!NOTE]
>
>Pour plus d’informations, voir [Jeu de documentation JS](https://helpx.adobe.com/fr/experience-manager/6-5/sites/developing/using/reference-materials/jsdoc/ui-touch/editor-core/index.html).

Elles peuvent être utilisées de différentes manières pour étendre la fonctionnalité de création de pages dans votre instance AEM. Une sélection est présentée ci-dessous (à un niveau élevé).

>[!NOTE]
>
>Pour plus d’informations, voir :
>
>* Utilisation et création [clientlibs](/help/sites-developing/clientlibs.md).
>* Utilisation et création [superpositions](/help/sites-developing/overlays.md).
>* [Granite](https://helpx.adobe.com/fr/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html)
>* [Structure de l’interface utilisateur tactile d’AEM](/help/sites-developing/touch-ui-structure.md) pour plus d’informations sur les zones structurelles utilisées pour la création de pages.
>


>[!CAUTION]
>
>Vous ne devez ***rien*** modifier dans le chemin `/libs`.
>
>En effet, le contenu de `/libs` est remplacé dès que vous mettez à niveau votre instance (et risque de l’être si vous appliquez un correctif ou un Feature Pack).
>
>La méthode recommandée pour la configuration et d’autres modifications est la suivante :
>
>1. Recréez l’élément requis (tel qu’il existe dans `/libs`) sous `/apps`.
>1. Apportez les modifications désirées dans `/apps`.

## Ajouter un nouveau calque (mode) {#add-new-layer-mode}

Lorsque vous modifiez une page, il existe plusieurs [modes](/help/sites-authoring/author-environment-tools.md#page-modes) disponible. Ces modes sont implémentés à l’aide de [calques](/help/sites-developing/touch-ui-structure.md#layer). Ils permettent d’accéder à différents types de fonctionnalités pour le même contenu de page. Les couches standard sont les suivantes : modifier, prévisualiser, annoter, développer et cibler.

### Exemple de calque : État de Live Copy {#layer-example-live-copy-status}

Une instance d’AEM standard fournit la couche MSM. Il accède aux données relatives à [gestion multi-site](/help/sites-administering/msm.md) et le surligne dans le calque.

Pour obtenir une démonstration, vous pouvez modifier toute page [Copie de langue We.Retail](/help/sites-developing/we-retail-globalized-site-structure.md) (ou n’importe quelle autre page Live Copy) et sélectionner le mode **Statut de Live Copy**.

Vous trouverez la définition du calque MSM (pour référence) à l’emplacement suivant :

`/libs/wcm/msm/content/touch-ui/authoring/editor/js/msm.Layer.js`

### Exemple de code {#code-sample}

Il s’agit d’un exemple de package montrant comment créer un nouveau calque (mode), qui est un nouveau calque pour la vue MSM.

CODE SUR GITHUB

Vous pouvez trouver le code de cette page sur GitHub.

* [Ouvrez le projet aem-authoring-new-layer-mode sur GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode).
* Téléchargez le projet sous la forme d’[un fichier ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode/archive/master.zip).

## Ajout d’une nouvelle catégorie de sélection à l’explorateur de ressources {#add-new-selection-category-to-asset-browser}

L’explorateur de ressources affiche des ressources de différents types/catégories (par exemple, image, documents, etc.). Les ressources peuvent également être filtrées par ces catégories.

### Exemple de code {#code-sample-1}

`aem-authoring-extension-assetfinder-flickr` est un exemple de package qui montre comment ajouter un nouveau groupe à l’outil de recherche de ressources. Cet exemple se connecte au flux public de [Flickr](https://www.flickr.com) et l’affiche dans le panneau latéral.

CODE SUR GITHUB

Vous pouvez trouver le code de cette page sur GitHub.

* [Ouvrez le projet aem-authoring-extension-assetfinder-flickr sur GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr).
* Téléchargez le projet sous la forme d’[un fichier ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr/archive/master.zip).

## Filtrage des ressources {#filtering-resources}

Lors de la création de pages, l’utilisateur doit souvent sélectionner parmi des ressources (par exemple, des pages, des composants, des ressources, etc.). Cela peut prendre la forme d’une liste, par exemple à partir de laquelle l’auteur doit choisir un élément.

Pour maintenir la liste à une taille raisonnable et adaptée au cas d’utilisation, un filtre peut être mis en oeuvre sous la forme d’un prédicat personnalisé. Par exemple, si le composant [`pathbrowser`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) [Granite](/help/sites-developing/touch-ui-concepts.md#granite-ui) est utilisé pour permettre à l’utilisateur de sélectionner le chemin d’accès à une ressource spécifique, les chemins d’accès présentés peuvent être filtrés comme suit :

* Mettez en œuvre le prédicat personnalisé en implémentant l’interface [`com.day.cq.commons.predicate.AbstractNodePredicate`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/predicate/package-summary.html).
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

           Définit le type d’éditeur intégré qui sera utilisé lorsque la modification statique est déclenchée pour ce composant ; par exemple, `text`, `textimage`, `image`, `title`.

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
>Pour obtenir un exemple, reportez-vous à :
>`/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js`

1. Implémentez les éléments suivants :

   * `setUp`
   * `tearDown`

1. Enregistrez l’éditeur (comprend le constructeur) :

   * `editor.register`

1. Indiquez la connexion entre l’éditeur et chaque type de ressource (comme dans le composant) qui peut l’utiliser.

#### Exemple de code pour la création d’un éditeur statique {#code-sample-for-creating-a-new-in-place-editor}

`aem-authoring-extension-inplace-editor` est un exemple de package qui montre comment créer un éditeur statique dans AEM.

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

* sinon, rien ne s’affichera, car les droits de réplication ont été supprimés.

Pour bénéficier d’un comportement personnalisé lors d’une telle activation, vous pouvez incruster le workflow **Demander l’activation** :

1. Dans `/apps`, recouvrez l’assistant **Sites** :

   `/libs/wcm/core/content/common/managepublicationwizard`

   >[!NOTE]
   >
   >Cela a pour effet de remplacer l’instance commune de :
   >
   >`/libs/cq/gui/content/common/managepublicationwizard`

1. Mettez à jour le [modèle de workflow](/help/sites-developing/workflows-models.md) et les configurations/scripts associés suivant les besoins.
1. Retirez, à tous les utilisateurs appropriés, le droit dont ils bénéficient sur l’[`replicate`action ](/help/sites-administering/security.md#actions) pour l’ensemble des pages pertinentes ; pour faire en sorte que ce workflow se déclenche comme une action par défaut lorsque l’un des utilisateurs tente de publier (ou de répliquer) une page.
