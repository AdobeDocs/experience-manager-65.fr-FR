---
title: Développement et outil de comparaison des pages
seo-title: Développement et outil de comparaison des pages
description: Développement et outil de comparaison des pages
seo-description: 'null'
uuid: 06f27bc2-f42a-4176-ab94-255e721c6933
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 6612f89d-c518-4e5a-8df1-6487cc330a9a
docset: aem65
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 92%

---


# Développement et outil de comparaison des pages{#developing-and-page-diff}

## Présentation des fonctionnalités {#feature-overview}

La création de contenu est un processus itératif. Pour être efficace lorsque vous créez du contenu, vous devez pouvoir voir ce qui a changé d’une version à l’autre. Afficher les versions en alternance est une méthode inefficace avec un fort risque d’erreur. Un auteur souhaite afficher, côte à côte, deux versions d’une page afin de les comparer en mettant les différences en évidence.

L’outil de comparaison des pages permet à un utilisateur de comparer la page active aux lancements, aux versions précédentes, etc. Pour plus d’informations sur cette fonctionnalité utilisateur, voir [Outil de comparaison des pages](/help/sites-authoring/page-diff.md).

## Détails de l’opération {#operation-details}

Lors de la comparaison des versions d’une page, la version précédente que l’utilisateur souhaite comparer est recréée en arrière-plan par AEM pour faciliter la comparaison. Cette opération est nécessaire pour pouvoir restituer le contenu [pour une comparaison côte à côte](/help/sites-developing/pagediff.md#operation-details).

Cette opération de recréation, réalisée par AEM en interne, est transparente pour l’utilisateur et ne nécessite aucune intervention. Cependant, un administrateur qui consulte le référentiel, par exemple dans CRX DE Lite, voit ces versions recréées dans la structure de contenu.

Lorsque le contenu est comparé, l’ensemble de l’arborescence jusqu’à la page à comparer est recréé à l’emplacement suivant :

`/tmp/versionhistory/`

Une tâche de nettoyage s’exécute automatiquement pour nettoyer ce contenu temporaire.

## Autorisations {#permissions}

Auparavant, dans l’interface utilisateur classique, une attention particulière devait être accordée au développement afin de faciliter la modification AEM (par exemple en utilisant `cq:text` tag lib ou en intégrant le service `DiffService` OSGi dans les composants). Cela n’est plus nécessaire pour la nouvelle fonction de comparaison (diff), puisque cela s’effectue du côté client via la comparaison DOM.

Cependant, il subsiste un certain nombre de restrictions qui doivent être prises en compte par le développeur.

* Cette fonctionnalité utilise des classes CSS qui ne sont pas placées dans un espace de noms sur le produit AEM. Si d’autres classes CSS personnalisées ou des classes CSS tierces portant le même nom sont incluses sur la page, l’affichage de la comparaison peut s’en trouver affecté.

   * `html-added`
   * `html-removed`
   * `cq-component-added`
   * `cq-component-removed`
   * `cq-component-moved`
   * `cq-component-changed`

* Étant donné que la comparaison s’effectue du côté client et s’exécute au chargement de la page, les réglages apportés au DOM après l’exécution de ce service de comparaison ne sont pas pris en compte. Cela peut avoir une incidence sur éléments suivants :

   * Composants qui utilisent AJAX pour intégrer du contenu
   * Applications sur une seule page
   * Composants basés sur JavaScript qui manipulent le DOM lors d’une interaction de l’utilisateur
