---
title: Composants pour les fragments de contenu
description: Les fragments de contenu Adobe Experience Manager (AEM) sont créés et gérés en tant que ressources indépendantes de la page
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
docset: aem65
pagetitle: Components for Content Fragments
exl-id: f2edd9b2-f231-42f3-a25e-428cd1d96c2a
source-git-commit: b66ec42c35b5b60804015d340b8194bbd6ef3e28
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 45%

---

# Composants pour les fragments de contenu{#components-for-content-fragments}

## Composants pour la création de fragments {#components-for-fragment-authoring}

>[!CAUTION]
>
>Il n’est pas recommandé d’étendre ou de modifier les composants réellement utilisés dans l’éditeur de fragment car ils sont susceptibles d’être modifiés.

Consultez [API de gestion des fragments de contenu - Côté client](/help/sites-developing/customizing-content-fragments.md#the-content-fragment-management-api-client-side).

## Composants pour la création de pages {#components-for-page-authoring}

>[!CAUTION]
>
>Le [composant de base Fragment de contenu](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=fr) est désormais recommandé. Voir [Développement des composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html?lang=fr) pour plus d’informations.
>
>Cette section décrit le composant d’origine diffusé pour une utilisation avec des fragments de contenu (**Fragment de contenu** dans le **Général** ).

>[!NOTE]
>
>Consultez également la section [Composants de configuration de fragments de contenu pour les rendus](/help/sites-developing/content-fragments-config-components-rendering.md) pour plus d’informations.

Les fragments de contenu Adobe Experience Manager (AEM) sont [créés et gérés en tant que ressources indépendantes de la page](/help/assets/content-fragments/content-fragments.md). Ils vous permettent de créer du contenu neutre pour les canaux, ainsi que des variantes (éventuellement spécifiques aux canaux). [Vous pouvez ensuite utiliser ces fragments et leurs variantes lors de la création de vos pages de contenu](/help/sites-authoring/content-fragments.md). Vous pouvez également utiliser une ressource de fragment de contenu existante en [le faisant glisser de l’explorateur de ressources vers la page ;](/help/sites-authoring/content-fragments.md#adding-a-content-fragment-to-your-page) (comme pour d’autres composants basés sur des ressources, tels que le composant de base Image). Le composant de fragment de contenu prêt à l’emploi affiche un seul [élément](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) du fragment de contenu référencé. Dans la boîte de dialogue des composants, vous pouvez définir l’[élément, la variation et la plage des paragraphes de fragment](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) que vous souhaitez afficher sur la page.

>[!NOTE]
>
>Ce composant de fragment de contenu a été introduit dans AEM 6.2 en tant que version améliorée du composant Article, qui a été obsolète.

>[!NOTE]
>
>Les fragments de contenu ne sont pas pris en charge dans l’IU classique.

### Définition {#definition}

Le composant **Fragment de contenu** est utilisé pour contenir une référence à un élément de fragment de contenu (éléments textuels améliorés). Le type de ressource pour le fragment de contenu est :

`dam/cfm/components/contentfragment/contentfragment`

La référence est définie dans la propriété :

`fileReference`

Seul l’éditeur de l’interface utilisateur tactile prend entièrement en charge les composants de fragment de contenu, qui incluent la bibliothèque cliente :

`cq.authoring.editor.plugin.cfm`

Cette bibliothèque ajoute à l’éditeur des fonctionnalités spécifiques aux fragments de contenu. Par exemple, la prise en charge de la possibilité d’ajouter et de configurer des fragments de contenu sur la page, de rechercher des ressources de fragments de contenu dans l’explorateur de ressources et du contenu associé dans le panneau latéral est disponible.

### Contenu intermédiaire {#in-between-content}

La variable **Fragment de contenu** Le composant t permet de déposer des composants supplémentaires entre les différents paragraphes de l’objet affiché. [element](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment). À la base, l’élément affiché est composé de différents paragraphes (chaque paragraphe est marqué par un retour chariot). Entre chacun de ces paragraphes, vous pouvez insérer du contenu à l’aide d’autres composants.

D’un point de vue technique, chaque paragraphe de l’élément affiché réside dans son propre parsys, et chaque composant que vous ajoutez entre les paragraphes est (sous le capot) inséré dans le parsys.

En d’autres termes, si l’instance du composant de fragment de contenu est composée de trois paragraphes, le composant dispose de trois parsys différents dans le référentiel. Tout le contenu intermédiaire qui est ajouté au fragment de contenu est en fait situé à l’intérieur de ces parsys.

Dans le référentiel, le contenu intermédiaire est stocké par rapport à sa position dans la structure globale du paragraphe, c’est-à-dire qu’il n’est pas joint au contenu réel du paragraphe.

Pour illustrer cela, tenez compte des points suivants :

* Une instance d’un fragment de contenu composé de trois paragraphes
* Et qu’un certain contenu a déjà été inséré après le deuxième paragraphe ;

   * Cela signifie que le contenu est stocké dans le second parsys.

Fondamentalement, si la structure de paragraphe de cette instance change (en modifiant la variation, l’élément ou la plage de paragraphes affichés), cela peut affecter le contenu intermédiaire affiché lorsque le contenu du fragment de contenu :

* est modifié et qu’un autre paragraphe est ajouté avant le deuxième paragraphe :

   * Le contenu intermédiaire s’affiche après le paragraphe nouvellement créé (le deuxième parsys contient désormais le paragraphe nouvellement créé).

* est modifié et que le deuxième paragraphe est supprimé :

   * Le contenu intermédiaire s’affiche après le paragraphe qui était précédemment le troisième (le deuxième parsys contient désormais le troisième paragraphe précédent).

* est configuré de sorte que seul le premier paragraphe soit affiché :

   * Le contenu intermédiaire n’est pas affiché (le deuxième parsys n’est plus rendu en raison de la nouvelle configuration).

### Personnalisation du composant de fragment de contenu {#customizing-the-content-fragment-component}

Pour utiliser le composant de fragment de contenu d’usine comme plan directeur pour l’extension, vous devez respecter le contrat suivant :

* Réutilisez le script de rendu HTL et son POJO associé afin de voir comment la fonctionnalité de contenu intermédiaire est implémentée.
* Réutiliser le nœud du fragment de contenu : `cq:editConfig`

   * Les listeners `afterinsert`/ `afteredit`/ `afterdelete` servent à déclencher des événements JS. Ces événements sont gérés dans la variable `cq.authoring.editor.plugin.cfm` bibliothèque cliente pour afficher le contenu associé dans le panneau latéral.
   * Les `cq:dropTargets` sont configurés de manière à prendre en charge la gestion des fragments de contenu.
   * `cq:inplaceEditing` est configuré de sorte à prendre en charge la création d’un fragment de contenu dans l’éditeur de pages. L’éditeur de fragment local est défini dans la bibliothèque cliente `cq.authoring.editor.plugin.cfm` et permet à un lien rapide d’ouvrir [l’élément/la variation](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) dans l’[éditeur de fragment](/help/assets/content-fragments/content-fragments-variations.md).

### Réécriture des ressources avant le rendu {#asset-rewriting-before-rendering}

La gestion de fragments de contenu utilise un processus de rendu interne pour générer la sortie HTML finale pour une page. Il est utilisé en interne par le composant Fragment de contenu, mais également par le processus d’arrière-plan qui met à jour les fragments référencés sur les pages de référencement.

En interne, Sling Rewriter est utilisé pour ce rendu. La configuration correspondante se trouve à l’adresse `/libs/dam/config/rewriter/cfm` et peuvent être ajustés, si nécessaire. Consultez [Apache Sling Rewriter](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html) pour en savoir plus.

>[!CAUTION]
>
>Si vous ajustez/superposez la configuration du module de réécriture :
>
>* `/libs/dam/config/rewriter/cfm`
>
>Ensuite, la variable `serializerType` **must** être mis à jour vers :
>
>* `serializerType="html5-serializer"`

La configuration prête à l’emploi utilise les transformateurs suivants :

* `transformer-cfm-payloadfilter` : pour récupérer la partie `body` (`<body>...</body>`) du fragment HTML seulement

* `transformer-cfm-parfilter` : filtre les paragraphes indésirables si une plage de paragraphes est spécifiée (comme cela peut être fait avec le composant Fragment de contenu)
* `transformer-cfm-assetprocessor` : est utilisé en interne pour récupérer une liste des ressources incorporées au fragment

Le processus de rendu est exposé via [`com.adobe.cq.dam.cfm.content.FragmentRenderService`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html) et peut être utilisé (par exemple) par des composants personnalisés, si nécessaire.
