---
title: Modèles de page - Statiques
seo-title: Modèles de page - Statiques
description: Un modèle sert à créer une page. Il définit les composants pouvant être utilisés dans l’étendue sélectionnée
seo-description: Un modèle sert à créer une page. Il définit les composants pouvant être utilisés dans l’étendue sélectionnée
uuid: 7a473c19-9565-476e-9e54-ab179da04d71
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: cfd90e8f-9b9b-4d0b-be31-828469b961de
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5
workflow-type: tm+mt
source-wordcount: '1648'
ht-degree: 65%

---


# Modèles de page - Statiques{#page-templates-static}

Un modèle sert à créer une page. Il définit les composants pouvant être utilisés dans l’étendue sélectionnée. Un modèle est une hiérarchie de nœuds qui a la même structure que la page à créer, mais sans contenu réel.

Chaque modèle présente une sélection de composants disponibles.

* Les modèles sont constitués de [Composants](/help/sites-developing/components.md) ;
* Les composants utilisent et autorisent l’accès aux Widgets et ceux-ci sont utilisés pour rendre le contenu.

>[!NOTE]
>
>[Les modèles](/help/sites-developing/page-templates-editable.md) modifiables sont également disponibles et sont le type recommandé pour la plus grande flexibilité et les fonctionnalités les plus récentes.

## Propriétés et nœuds enfants d’un modèle {#properties-and-child-nodes-of-a-template}

Un modèle est un nœud de type cq:Template et possède les propriétés et les nœuds enfants suivants :

<table>
 <tbody>
  <tr>
   <td><strong>Nom <br /> </strong></td>
   <td><strong>Type <br /> </strong></td>
   <td><strong>Description <br /> </strong></td>
  </tr>
  <tr>
   <td>. <br /> </td>
   <td> cq:Template</td>
   <td>Modèle actuel. Un modèle possède le type de noeud cq:Template.<br /> </td>
  </tr>
  <tr>
   <td> allowChildren </td>
   <td> Chaîne[]</td>
   <td>Path of a template that is allowed to be a child of this template.<br /> </td>
  </tr>
  <tr>
   <td> allowParents</td>
   <td> Chaîne[]</td>
   <td>Path of a template that is allowed to be a parent of this template.<br /> </td>
  </tr>
  <tr>
   <td> allowPaths</td>
   <td> Chaîne[]</td>
   <td>Chemin d’accès d’une page autorisée à être basée sur ce modèle.<br /> </td>
  </tr>
  <tr>
   <td> jcr:created</td>
   <td> Date</td>
   <td>Date of creation of the template.<br /> </td>
  </tr>
  <tr>
   <td> jcr:description</td>
   <td> Chaîne</td>
   <td>Description of the template.<br /> </td>
  </tr>
  <tr>
   <td> jcr:title</td>
   <td> Chaîne</td>
   <td>Title of the template.<br /> </td>
  </tr>
  <tr>
   <td> classement</td>
   <td> Long</td>
   <td>Classement du modèle. Utilisé pour afficher le modèle dans l’interface utilisateur.<br /> </td>
  </tr>
  <tr>
   <td> jcr:content</td>
   <td> cq:PageContent</td>
   <td>Noeud contenant le contenu du modèle.<br /> </td>
  </tr>
  <tr>
   <td> thumbnail.png</td>
   <td> nt:file</td>
   <td>Miniature du modèle.<br /> </td>
  </tr>
  <tr>
   <td> icon.png</td>
   <td> nt:file</td>
   <td>Icône du modèle.<br /> </td>
  </tr>
 </tbody>
</table>

Un modèle sert de fondement pour une page.

To create a page, the template must be copied (node-tree `/apps/<myapp>/template/<mytemplate>`) to the corresponding position in the site-tree: this is what happens if a page is created using the **Websites** tab.

Cette action de copie confère également à la page son contenu initial (généralement le contenu de niveau supérieur uniquement) et la propriété sling: resourceType, le chemin d’accès au composant de page utilisé pour rendre la page (tout ce qui est présent dans le nœud enfant jcr:content).

## Structuration des modèles {#how-templates-are-structured}

Il y a deux aspects à considérer :

* la structure du modèle lui-même
* la structure du contenu produit lorsqu’un modèle est utilisé

### Structure d’un modèle {#the-structure-of-a-template}

Un modèle est créé sous un nœud de type **cq:Template**.

![screen_shot_2012-02-13at63646pm](assets/screen_shot_2012-02-13at63646pm.png)

Différentes propriétés peuvent être définies, en particulier :

* **jcr:title**- titre du modèle. Apparaît dans la boîte de dialogue lors de la création d’une page.
* **jcr:description**- description du modèle. Apparaît dans la boîte de dialogue lors de la création d’une page.

Ce nœud contient un nœud jcr:content (cq:PageContent) qui sert de base au nœud de contenu des pages résultantes. Cela référence, au moyen de sling:resourceType, le composant à utiliser pour rendre le contenu réel d’une nouvelle page.

![screen_shot_2012-02-13at64010pm](assets/screen_shot_2012-02-13at64010pm.png)

Ce composant est utilisé pour définir la structure et la conception du contenu lors de la création d’une page.

![screen_shot_2012-02-13at64137pm](assets/screen_shot_2012-02-13at64137pm.png)

### Contenu produit par un modèle {#the-content-produced-by-a-template}

Les modèles servent à créer des pages de type `cq:Page`(comme mentionné précédemment, une page est un type spécial de composant). Each AEM Page has a structured node `jcr:content`. Cela :

* est de type cq:PageContent
* est un type de nœud structuré contenant une définition de contenu définie
* possède une propriété `sling:resourceType` pour référencer le composant contenant les scripts sling utilisés pour le rendu du contenu

### Modèles par défaut {#default-templates}

AEM offre un certain nombre de modèles par défaut prêts à l’emploi. Dans certaines situations, vous pouvez utiliser les modèles tels quels. Dans ce cas, vous devez vous assurer que le modèle est disponible pour votre site Web.

Par exemple, AEM s’accompagne de plusieurs modèles, dont contentpage et homepage.

| **Titre** | **Composant** | **Emplacement** | **Objectif** |
|---|---|---|---|
| Page d’accueil | homepage | geometrixx | Modèle de page d’accueil de Geometrixx. |
| Page de contenu | contentpage | geometrixx | Modèle de page de contenu de Geometrixx. |

#### Affichage des modèles par défaut {#displaying-default-templates}

Pour voir la liste de tous les modèles disponibles dans le référentiel, procédez comme suit :

1. Dans CRXDE Lite, ouvrez le menu **Outils**, puis cliquez sur **Requête**.

1. Dans l’onglet Requête :
1. Indiquez le **Type** **XPath**.

1. Dans la zone de saisie **Requête**, entrez la chaîne suivante :
//element(*, cq:Template)

1. Cliquez sur **Exécuter**. La liste s’affiche dans la zone des résultats.

Dans la plupart des cas, c’est à partir d’un modèle existant que vous élaborerez un nouveau modèle pour votre usage personnel. Pour plus d’informations, voir [Développement de modèles de page](#developing-page-templates).

To enable an existing template for your website and you want it to be displayed in the **Create Page** dialog when creating a page right under **Websites** from the **Websites** console, set the allowedPaths property of the template node to: **/content(/.*)?**

## Application des conceptions de modèle {#how-template-designs-are-applied}

Lorsque des styles sont définis dans l’interface utilisateur à l’aide du mode [de](/help/sites-authoring/default-components-designmode.md)conception, la conception est conservée à l’emplacement exact du noeud de contenu pour lequel le style est défini.

>[!CAUTION]
>
>Adobe recommande uniquement d’appliquer des conceptions en mode [](/help/sites-authoring/default-components-designmode.md)Design.
>
>La modification de conceptions dans CRX DE, par exemple, n’est pas recommandée et l’application de ces conceptions risque de provoquer un comportement imprévu.

Si les conceptions sont appliquées uniquement en mode Création, les sections suivantes, Résolution [du chemin de](/help/sites-developing/page-templates-static.md#design-path-resolution)conception, Arborescence [de](/help/sites-developing/page-templates-static.md#decision-tree)décision et [Exemple](/help/sites-developing/page-templates-static.md#example) ne sont pas applicables.

### Résolution du chemin de conception {#design-path-resolution}

Lors du rendu du contenu à partir d’un modèle statique, AEM tentera d’appliquer la conception et les styles les plus pertinents au contenu en fonction d’une traversée de la hiérarchie du contenu.

aem détermine le style le plus pertinent pour un noeud de contenu dans l’ordre suivant :

* S’il existe une conception pour le chemin d’accès complet et exact du noeud de contenu (comme lorsque la conception est définie en mode Création), utilisez cette conception.
* S’il existe une conception pour le noeud de contenu du parent, utilisez-la.
* S’il existe une conception pour un noeud sur le chemin du noeud de contenu, utilisez cette conception.

Dans les deux derniers cas, s’il existe plusieurs conceptions applicables, utilisez celle qui est la plus proche du noeud de contenu.

### Arborescence de décision {#decision-tree}

Il s’agit d’une représentation graphique de la logique de résolution [des chemins de](/help/sites-developing/page-templates-static.md#design-path-resolution) conception.

![design_path_resolution](assets/design_path_resolution.png)

### Exemple {#example}

Considérez une structure de contenu simple comme suit, où une conception peut s’appliquer à l’un des noeuds :

`/root/branch/leaf`

Le tableau suivant décrit comment AEM choisira une conception.

<table>
 <tbody>
  <tr>
   <td><strong>Recherche de conception pour<br /> </strong></td>
   <td><strong>Il existe des conceptions pour<br /> </strong></td>
   <td><strong>Conception choisie<br /> </strong></td>
   <td><strong>Commentaire</strong></td>
  </tr>
  <tr>
   <td><code class="code">leaf
      </code></td>
   <td><p><code>root</code></p> <p><code>branch</code></p> <p><code>leaf</code></p> </td>
   <td><code>leaf</code></td>
   <td>La correspondance la plus exacte est toujours prise.<br /> </td>
  </tr>
  <tr>
   <td><code>leaf</code></td>
   <td><p><code>root</code></p> <p><code>branch</code></p> </td>
   <td><code>branch</code></td>
   <td>Revenez à la correspondance la plus proche plus bas dans l'arbre.</td>
  </tr>
  <tr>
   <td><code>leaf</code></td>
   <td><code>root</code></td>
   <td><code>root</code></td>
   <td>Si tout le reste échoue, prenez ce qui reste.<br /> </td>
  </tr>
  <tr>
   <td><code>branch</code></td>
   <td><code>branch</code></td>
   <td><code>branch</code></td>
   <td> </td>
  </tr>
  <tr>
   <td><code>branch</code></td>
   <td><p><code>branch</code></p> <p><code class="code">leaf
       </code></p> </td>
   <td><code>branch</code></td>
   <td> </td>
  </tr>
  <tr>
   <td><code>branch</code></td>
   <td><p><code>root</code></p> <p><code class="code">branch
       </code></p> </td>
   <td><code>branch</code></td>
   <td> </td>
  </tr>
  <tr>
   <td><code>branch</code></td>
   <td><p><code>root</code></p> <p><code class="code">leaf
       </code></p> </td>
   <td><code>root</code></td>
   <td><p>S'il n'y a pas de correspondance exacte, prenez celle plus bas dans l'arbre.</p> <p>L'hypothèse est que cela sera toujours applicable, mais plus haut l'arbre peut être trop spécifique.<br /> </p> </td>
  </tr>
 </tbody>
</table>

## Développement de modèles de page {#developing-page-templates}

Les modèles de pages AEM sont simplement des modèles utilisés pour créer des pages. Ils peuvent contenir autant de contenu initial que nécessaire, leur rôle étant de créer des structures de nœuds correctes avec les propriétés requises (principalement sling:resourceType) définies pour permettre la modification et le rendu.

### Création d’un modèle (basé sur un modèle existant) {#creating-a-new-template-based-on-an-existing-template}

Inutile de dire qu’un nouveau modèle peut être entièrement créé de toutes pièces, mais en pratique un modèle existant est copié et modifié pour faire gagner du temps. Par exemple, les modèles Geometrixx peuvent servir de point de départ.

Pour créer un modèle d’après un modèle existant :

1. Copiez un modèle existant (de préférence avec une définition aussi proche que possible de ce que vous souhaitez réaliser) sur un nouveau nœud.

   Les modèles sont généralement stockés dans **/apps/&lt;nom-siteweb>/templates/&lt;nom-modèle>**.

   >[!NOTE]
   >
   >La liste des modèles disponibles dépend de l’emplacement de la nouvelle page et des restrictions de positionnement spécifiées dans chaque modèle. Voir [Disponibilité des modèles](#templateavailibility).

1. Changez le **jcr:title** du nouveau nœud de modèle de manière à refléter son nouveau rôle. Vous pouvez également mettre à jour **jcr:description** si nécessaire. Veillez à modifier la disponibilité du modèle de la page, le cas échéant.

   >[!NOTE]
   >
   >If you want your template to be displayed in the **Create Page** dialog when creating a page right under **Websites** from the **Websites** console, set the `allowedPaths` property of the template node to: `/content(/.*)?`

   ![chlimage_1-88](assets/chlimage_1-88.png)

1. Copiez le composant sur lequel le modèle est basé (ceci est indiqué par la propriété **sling:resourceType** du nœud **jcr:content** dans le modèle) pour créer une nouvelle instance.

   Les composants sont généralement stockés dans **/apps/&lt;nom-siteweb>/components/&lt;nom-composant>**.

1. Mettez à jour les propriétés **jcr:title** et **jcr:description** du nouveau composant.
1. Remplacez thumbnail.png si vous souhaitez afficher une nouvelle vignette dans la liste de sélection de modèles (taille 128 x 98 px).
1. Mettez à jour le **sling:resourceType** du nœud **jcr:content** du modèle pour référencer le nouveau composant.
1. Apportez d’autres modifications aux fonctionnalités ou à la conception du modèle et/ou de son composant sous-jacent.

   >[!NOTE]
   >
   >Les modifications apportées au nœud **/apps/&lt;site Web>/templates/&lt;nom-modèle>** sont répercutées sur l’instance du modèle (comme dans la liste de sélection).
   Les modifications apportées au nœud **/apps/&lt;site Web>/components/&lt;nom-composant>** sont répercutées sur la page de contenu créée lorsque le modèle est utilisé.

   Vous pouvez à présent créer une page sur votre site Web en vous servant du nouveau modèle.

>[!NOTE]
The editor client library assumes the presence of the `cq.shared` namespace in content pages, and if it is absent the JavaScript error `Uncaught TypeError: Cannot read property 'shared' of undefined` will result.
`cq.shared` est inclus dans tous les exemples de pages de contenu. Par conséquent, tout contenu basé sur ces pages inclut automatiquement `cq.shared`. Toutefois, si vous décidez de créer vos propres pages de contenu à partir de zéro, sans vous servir de l’exemple de contenu, vous devez veiller à inclure l’espace de noms `cq.shared`.
Pour plus d’informations, voir [Utilisation des bibliothèques côté client](/help/sites-developing/clientlibs.md).

## Mise à disposition d’un modèle existant {#making-an-existing-template-available}

Cet exemple illustre comment autoriser l’utilisation d’un modèle pour certains chemins de contenu. The templates that are available to the page author when creating new pages are determined by the logic defined in [Template Availability](/help/sites-developing/templates.md#template-availability).

1. Dans CRXDE Lite, accédez au modèle que vous souhaitez utiliser pour votre page, par exemple, le modèle Newsletter.
1. Modifiez la propriété `allowedPaths` et les autres propriétés utilisées pour la [disponibilité du modèle](/help/sites-developing/templates.md#template-availability). For example, `allowedPaths`: `/content/geometrixx-outdoors/[^/]+(/.*)?` means that this template is allowed in any path under `/content/geometrixx-outdoors`.

   ![chlimage_1-89](assets/chlimage_1-89.png)
