---
title: Développement et outil de comparaison des pages
description: Développement et outil de comparaison des pages
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: b07134b2-074a-4d52-8d0c-7e7abe51fc3a
source-git-commit: 1ef5593495b4bf22d2635492a360168bccc1725d
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 35%

---

# Développement et outil de comparaison des pages{#developing-and-page-diff}

## Présentation des fonctionnalités {#feature-overview}

La création de contenu est un processus itératif. Pour être efficace lorsque vous créez du contenu, vous devez pouvoir voir ce qui a changé d’une version à l’autre. L’affichage d’une version de page, puis de l’autre, est inefficace et susceptible d’erreur. Un auteur souhaite pouvoir comparer la page active à une version précédente, côte à côte, avec les différences mises en évidence.

L’outil de comparaison des pages permet à l’utilisateur de comparer la page active aux lancements, aux versions précédentes, etc. Pour plus d’informations sur cette fonction utilisateur, voir [Outil de comparaison des pages](/help/sites-authoring/page-diff.md).

## Détails de l’opération {#operation-details}

Lors de la comparaison des versions d’une page, la version précédente que l’utilisateur souhaite comparer est recréée par AEM en arrière-plan afin de faciliter la comparaison. Cette opération est nécessaire pour pouvoir restituer le contenu [pour une comparaison côte à côte](/help/sites-developing/pagediff.md#operation-details).

Cette opération de recréation, réalisée par AEM en interne, est transparente pour l’utilisateur et ne nécessite aucune intervention. Cependant, un administrateur qui consulte le référentiel, par exemple en CRXDE Lite, voit ces versions recréées dans la structure de contenu.

Lorsque le contenu est comparé, l’ensemble de l’arborescence jusqu’à la page à comparer est recréé à l’emplacement suivant :

`/tmp/versionhistory/`

Une tâche de nettoyage s’exécute automatiquement pour nettoyer ce contenu temporaire.

## Autorisations {#permissions}

Auparavant, dans l’IU classique, il fallait prêter une attention particulière sur le plan du développement pour permettre la comparaison AEM (par exemple pour l’utilisation de la bibliothèque de balises `cq:text` ou pour l’intégration personnalisée du service OSGi `DiffService` dans des composants). Cela n’est plus nécessaire pour la nouvelle fonction de comparaison, car la comparaison côté client se fait par le biais de la comparaison DOM.

Cependant, certaines limites doivent être prises en compte par le développeur.

* Cette fonctionnalité utilise des classes CSS qui ne sont pas des espaces de noms du produit AEM. Si d’autres classes CSS personnalisées ou des classes CSS tierces portant le même nom sont incluses sur la page, l’affichage de la comparaison peut être affecté.

   * `html-added`
   * `html-removed`
   * `cq-component-added`
   * `cq-component-removed`
   * `cq-component-moved`
   * `cq-component-changed`

* Étant donné que la comparaison est côté client et s’exécute au chargement de la page, les ajustements apportés au DOM après l’exécution du service de comparaison côté client ne seront pas pris en compte. Cela peut affecter

   * Composants qui utilisent AJAX pour intégrer du contenu
   * Applications sur une seule page
   * Composants JavaScript qui manipulent le DOM lors de l’interaction de l’utilisateur.

>[!NOTE]
>
>La comparaison des différences de page fonctionne uniquement pour les composants qui possèdent des noeuds cq:editConfig valides.
