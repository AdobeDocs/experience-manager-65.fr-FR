---
title: Développement et outil de comparaison des pages
description: Découvrez comment développer et utiliser la fonction de comparaison des pages dans Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: b07134b2-074a-4d52-8d0c-7e7abe51fc3a
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 100%

---

# Développement et outil de comparaison des pages{#developing-and-page-diff}

## Présentation des fonctionnalités {#feature-overview}

La création de contenu est un processus itératif. Pour être efficace lorsque vous créez du contenu, vous devez pouvoir voir ce qui a changé d’une version à l’autre. L’affichage d’une version de page, puis de l’autre, est inefficace et source d’erreurs. Si un auteur ou une autrice veut comparer la page active à une version précédente en même temps que les différences mises en évidence.

L’outil de comparaison des pages permet de comparer la page active aux lancements, versions précédentes, etc. Pour plus d’informations sur cette fonctionnalité utilisateur, voir [Outil de comparaison des pages](/help/sites-authoring/page-diff.md).

## Détails de l’opération {#operation-details}

Lors de la comparaison des versions d’une page, la version précédente à comparer est recréée en arrière-plan par AEM pour faciliter la comparaison. Cette opération est nécessaire pour pouvoir restituer le contenu [pour une comparaison côte à côte](/help/sites-developing/pagediff.md#operation-details).

Cette opération de recréation, réalisée par AEM en interne, est transparente pour l’utilisateur et ne nécessite aucune intervention. Cependant, un administrateur ou une administratrice qui consulte le référentiel, par exemple dans CRXDE Lite, voit ces versions recréées dans la structure de contenu.

Lorsque le contenu est comparé, l’ensemble de l’arborescence jusqu’à la page à comparer est recréé à l’emplacement suivant :

`/tmp/versionhistory/`

Une tâche de nettoyage s’exécute automatiquement pour nettoyer ce contenu temporaire.

## Autorisations {#permissions}

Auparavant, dans l’IU classique, il fallait prêter une attention particulière sur le plan du développement pour permettre la comparaison AEM (par exemple pour l’utilisation de la bibliothèque de balises `cq:text` ou pour l’intégration personnalisée du service OSGi `DiffService` dans des composants). Cela n’est plus nécessaire pour la nouvelle fonction de comparaison, car la comparaison côté client se fait par le biais de la comparaison DOM.

Cependant, certaines limites doivent être prises en compte par le développeur ou la développeuse.

* Cette fonctionnalité utilise des classes CSS qui ne sont pas placées dans un espace de noms sur le produit AEM. Si d’autres classes CSS personnalisées ou des classes CSS tierces portant le même nom sont incluses sur la page, l’affichage de la comparaison peut s’en trouver affecté.

   * `html-added`
   * `html-removed`
   * `cq-component-added`
   * `cq-component-removed`
   * `cq-component-moved`
   * `cq-component-changed`

* Étant donné que la comparaison se trouve côté client et s’exécute au chargement de la page, les ajustements apportés au DOM après l’exécution du service de comparaison côté client ne sont pas pris en compte. Cela peut affecter les éléments suivants :

   * Composants qui utilisent AJAX pour intégrer du contenu
   * Applications sur une seule page
   * Composants JavaScript qui manipulent le DOM lors de l’interaction de l’utilisateur ou l’utilisatrice.

>[!NOTE]
>
>La comparaison des pages ne fonctionne que pour les composants qui possèdent des nœuds cq:editConfig valides.
