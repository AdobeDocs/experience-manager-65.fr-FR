---
title: Personnaliser la création de pages
description: Adobe Experience Manager (AEM) fournit divers mécanismes pour vous permettre de personnaliser les fonctionnalités de création de pages.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 90594588-db8e-4d4c-a208-22c1c6ea2a2d
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 3aa55b88f589749fb49d5ff46340b0912d490157
workflow-type: tm+mt
source-wordcount: '1264'
ht-degree: 98%

---

# Personnaliser la création de pages{#customizing-page-authoring}

>[!CAUTION]
>
>Ce document explique comment personnaliser la création de pages dans l’IU tactile moderne et ne s’applique pas à l’IU classique.

Adobe Experience Manager (AEM) fournit divers mécanismes pour vous permettre de personnaliser la fonctionnalité de création de pages (et les [consoles](/help/sites-developing/customizing-consoles-touch.md)) de votre instance de création.

* Clientlibs

  Les bibliothèques clientes (clientlibs) vous permettent d’étendre l’implémentation par défaut afin d’obtenir de nouvelles fonctionnalités, tout en réutilisant les fonctions, objets et méthodes standard. Lors de la personnalisation, vous pouvez créer votre propre bibliothèque cliente sous `/apps.` La nouvelle bibliothèque cliente doit :

   * dépendre de la bibliothèque cliente de création `cq.authoring.editor.sites.page` ;
   * faire partie de la catégorie `cq.authoring.editor.sites.page.hook` appropriée.

* Recouvrements

  Les recouvrements sont basés sur les définitions de nœuds et vous permettent de recouvrir les fonctionnalités standard (dans `/libs`) avec vos propres fonctionnalités personnalisées (dans `/apps`). Lors de la création d’un recouvrement, il n’est pas nécessaire de disposer d’une copie 1:1 de l’original, car [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) autorise l’héritage.

>[!NOTE]
>
>Pour plus d’informations, voir [Jeu de documentation JS](https://developer.adobe.com/experience-manager/reference-materials/6-5/jsdoc/ui-touch/editor-core/index.html?lang=fr).

Il est possible de les utiliser de différentes manières pour étendre la fonctionnalité de création de pages dans votre instance AEM. Une sélection est abordée ci-dessous (à un niveau élevé).

>[!NOTE]
>
>Pour plus d’informations, consultez les sections suivantes :
>
>* Utiliser et créer des [clientlibs](/help/sites-developing/clientlibs.md).
>* Utiliser et créer des [recouvrements](/help/sites-developing/overlays.md).
>* [Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html)
>* [Structure de l’interface utilisateur tactile d’AEM](/help/sites-developing/touch-ui-structure.md) pour plus d’informations sur les zones structurelles utilisées pour la création de pages.
>


>[!CAUTION]
>
>****** Ne modifiez rien dans le chemin d’accès `/libs`.
>
>Cela est dû au fait que le contenu de `/libs` sera écrasé lors de la prochaine mise à niveau de votre instance (et éventuellement lors de l’application d’un correctif ou d’un pack de fonctionnalités).
>
>La méthode recommandée pour la configuration et d’autres modifications est la suivante :
>
>1. Recréez l’élément requis (tel qu’il existe dans `/libs`) sous `/apps`.
>1. Apportez les modifications désirées dans `/apps`.

## Ajouter un nouveau calque (mode) {#add-new-layer-mode}

Lorsque vous modifiez une page, plusieurs [modes](/help/sites-authoring/author-environment-tools.md#page-modes) sont disponibles. Ces modes sont implémentés à l’aide de [calques](/help/sites-developing/touch-ui-structure.md#layer). Ils permettent d’accéder à différents types de fonctionnalités pour le même contenu de page. Les calques standard sont les suivants : modification, prévisualisation, annotation, développeur et ciblage.

### Exemple de calque : statut de Live Copy {#layer-example-live-copy-status}

Une instance AEM standard fournit la couche MSM. Cela permet d’accéder aux données relatives à la [gestion multisite](/help/sites-administering/msm.md) et de les mettre en évidence dans le calque.

Pour obtenir une démonstration, vous pouvez modifier toute page [Copie de langue We.Retail](/help/sites-developing/we-retail-globalized-site-structure.md) (ou n’importe quelle autre page Live Copy) et sélectionner le mode **Statut de Live Copy**.

Vous trouverez la définition du calque MSM (pour référence) à l’emplacement suivant :

`/libs/wcm/msm/content/touch-ui/authoring/editor/js/msm.Layer.js`

### Exemple de code {#code-sample}

Ceci est un exemple de package montrant comment créer un calque (mode), qui est un nouveau calque pour la vue MSM.

CODE SUR GITHUB

Vous pouvez trouver le code de cette page sur GitHub.

* [Ouvrez le projet aem-authoring-new-layer-mode sur GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode).
* Téléchargez le projet sous la forme d’[un fichier ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode/archive/master.zip).

## Ajouter une nouvelle catégorie de sélection à l’explorateur de ressources {#add-new-selection-category-to-asset-browser}

L’explorateur de ressources affiche des ressources de différents types/catégories (par exemple, des images et des documents). Les ressources peuvent également être filtrées par ces catégories.

### Exemple de code {#code-sample-1}

`aem-authoring-extension-assetfinder-flickr` est un exemple de package qui montre comment ajouter un groupe à l’outil de recherche de ressources. Cet exemple se connecte au flux public de [Flickr](https://www.flickr.com) et l’affiche dans le panneau latéral.

CODE SUR GITHUB

Vous pouvez trouver le code de cette page sur GitHub.

* [Ouvrez le projet aem-authoring-extension-assetfinder-flickr sur GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr).
* Téléchargez le projet sous la forme d’[un fichier ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr/archive/master.zip).

## Filtrer les ressources {#filtering-resources}

Lors de la création de pages, l’utilisateur ou l’utilisatrice doit souvent effectuer une sélection parmi des ressources (par exemple, des pages, des composants et des ressources). Cela peut prendre la forme d’une liste, par exemple, à partir de laquelle l’auteur ou l’autrice doit choisir un élément.

Pour maintenir la liste à une taille raisonnable et adaptée au cas d’utilisation, un filtre peut être mis en œuvre sous la forme d’un prédicat personnalisé. Par exemple, si le composant [`pathbrowser`](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html) [Granite](/help/sites-developing/touch-ui-concepts.md#granite-ui) est utilisé pour permettre à l’utilisateur de sélectionner le chemin d’accès à une ressource spécifique, les chemins d’accès présentés peuvent être filtrés comme suit :

* Mettez en œuvre le prédicat personnalisé en implémentant l’interface [`com.day.cq.commons.predicate.AbstractNodePredicate`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/predicate/package-summary.html?lang=fr).
* Spécifiez un nom pour le prédicat et faites-y référence lors de l’utilisation de `pathbrowser`.

Pour plus d’informations sur la création d’un prédicat personnalisé, voir [Implémentation d’un évaluateur de prédicat personnalisé pour Query Builder](/help/sites-developing/implementing-custom-predicate-evaluator.md).

>[!NOTE]
>
>Mettre en œuvre un prédicat personnalisé en implémentant l’interface `com.day.cq.commons.predicate.AbstractNodePredicate` est également possible dans l’IU classique.
>
>Consultez l’[article de la base de connaissances](https://helpx.adobe.com/experience-manager/using/creating-custom-cq-tree.html) pour voir un exemple d’implémentation de prédicat personnalisé dans l’interface utilisateur classique.

## Ajouter une nouvelle action à une barre d’outils de composant {#add-new-action-to-a-component-toolbar}

Chaque composant (en général) dispose d’une barre d’outils qui permet d’accéder à un éventail d’actions pouvant être réalisées sur le composant.

### Exemple de code {#code-sample-2}

`aem-authoring-extension-toolbar-screenshot` est un exemple de package qui montre comment créer une action de barre d’outils personnalisée pour effectuer le rendu de composants.

CODE SUR GITHUB

Vous pouvez trouver le code de cette page sur GitHub.

* [Ouvrez le projet aem-authoring-extension-toolbar-screenshot sur GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot).
* Téléchargez le projet sous la forme d’[un fichier ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot/archive/master.zip).

## Ajouter un nouvel éditeur statique {#add-new-in-place-editor}

### Éditeur statique standard {#standard-in-place-editor}

Dans une installation AEM standard :

1. `/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js`

   Contient les définitions des différents éditeurs disponibles.

1. Il existe une connexion entre l’éditeur et chaque type de ressource (comme dans le composant) qui peut l’utiliser :

   * `cq:inplaceEditing`

     par exemple :

      * `/libs/foundation/components/text/cq:editConfig`
      * `/libs/foundation/components/image/cq:editConfig`

         * property : `editorType`

           Définit le type d’éditeur en ligne utilisé lorsqu’une édition statique est déclenchée pour ce composant ; par exemple, `text`, `textimage`, `image`, `title`.

1. Les informations de configuration supplémentaires de l’éditeur peuvent être définies à l’aide d’un nœud `config` contenant des configurations, ainsi qu’un nœud `plugin` additionnel pour contenir les informations nécessaires à la configuration du plug-in.

   Voici un exemple de définition des proportions pour le plug-in de recadrage d’image du composant d’image. Dans la mesure où la taille d’écran peut être limitée, les proportions de recadrage ont été déplacées vers l’éditeur plein écran et ne sont visibles qu’à cet endroit.

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
   >Dans AEM, les rapports de recadrage, tels qu’ils sont définis par la propriété `ratio`, sont définis sous la forme **hauteur/largeur**.  Cela diffère de la définition conventionnelle de la largeur/hauteur. Cela a été créée pour des raisons de compatibilité héritée. Les utilisateurs chargés de la création ne percevront aucune différence, à condition que vous définissiez clairement la propriété `name`, car c’est cette dernière qui s’affiche dans l’interface utilisateur.

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

`aem-authoring-extension-inplace-editor` est un exemple de package qui montre comment créer un éditeur statique dans AEM.

CODE SUR GITHUB

Vous pouvez trouver le code de cette page sur GitHub.

* [Ouvrez le projet aem-authoring-extension-inplace-editor sur GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor).
* Téléchargez le projet sous la forme d’[un fichier ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor/archive/master.zip).

#### Configurer plusieurs éditeurs statiques {#configuring-multiple-in-place-editors}

Il est possible de configurer un composant de sorte qu’il dispose de plusieurs éditeurs statiques. Après avoir configuré plusieurs éditeurs statiques, vous pouvez sélectionner le contenu approprié et ouvrir l’éditeur adéquat. Pour plus d’informations, consultez [Configuration de plusieurs éditeurs statiques](/help/sites-developing/multiple-inplace-editors.md).

## Ajouter une nouvelle action de page {#add-a-new-page-action}

Pour ajouter une nouvelle action de page à la barre d’outils de la page, par exemple une action **Retour à Sites** (console).

### Exemple de code {#code-sample-3}

`aem-authoring-extension-header-backtosites` est un exemple de package qui montre comment créer une action de barre d’en-tête personnalisée pour revenir à la console Sites.

CODE SUR GITHUB

Vous pouvez trouver le code de cette page sur GitHub.

* [Ouvrez le projet aem-authoring-extension-header-backtosites sur GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites).
* Téléchargez le projet sous la forme d’[un fichier ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites/archive/master.zip).

## Personnalisation du workflow Demander l’activation {#customizing-the-request-for-activation-workflow}

Le workflow d’usine, **Demande d’activation** :

* apparaît automatiquement dans le menu approprié lorsqu’un auteur de contenu **n’a pas** les droits de réplication appropriés, mais **dispose** de l’abonnement des utilisateurs et auteurs de la gestion des ressources numériques ;

* sinon, rien ne s’affiche, car les droits de réplication ont été supprimés.

Pour bénéficier d’un comportement personnalisé lors d’une telle activation, vous pouvez incruster le workflow **Demande d’activation** :

1. Dans `/apps`, recouvrez l’assistant **Sites** :

   `/libs/wcm/core/content/common/managepublicationwizard`

   >[!NOTE]
   >
   >Cela a pour effet de remplacer l’instance commune de :
   >
   >`/libs/cq/gui/content/common/managepublicationwizard`

1. Mettez à jour le [modèle de workflow](/help/sites-developing/workflows-models.md) et les configurations/scripts associés suivant les besoins.
1. Retirez, à toutes les personnes appropriées, le droit dont elles bénéficient sur l’action [`replicate` ](/help/sites-administering/security.md#actions) pour l’ensemble des pages pertinentes ; pour faire en sorte que ce workflow se déclenche comme une action par défaut lorsque l’une des personnes tente de publier (ou de répliquer) une page.
