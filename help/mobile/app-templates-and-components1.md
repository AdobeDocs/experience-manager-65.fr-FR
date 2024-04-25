---
title: Modèles et composants d’application
description: Consultez cette page pour en savoir plus sur les modèles d’application et les composants. Il fournit des informations détaillées sur la structure des modèles.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 58d95325-7cb1-4204-842d-17add70e1fbf
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 28%

---

# Modèles et composants d’application{#app-templates-and-components}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur SPA pour les projets nécessitant un rendu côté client, basé sur un framework, pour une application à une seule page (comme React). [En savoir plus](/help/sites-developing/spa-overview.md).

Un modèle sert à créer une page. Il définit les composants pouvant être utilisés dans l’étendue sélectionnée. Un modèle est une hiérarchie de nœuds ayant la même structure que la page à créer, mais sans contenu réel.

Chaque modèle vous présente une sélection de composants disponibles.

* Les modèles sont constitués de [Composants](/help/sites-developing/components.md);
* Les composants utilisent et permettent d’accéder aux widgets, qui sont utilisés pour le rendu du contenu.

>[!NOTE]
>
>Pour savoir comment développer votre application Adobe Experience Manager (AEM) à l’aide de CRXDE Lite, voir [Développement avec le CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

Un modèle sert de fondement pour une page.

Pour créer une page, le modèle doit être copié (arborescence de noeuds) **/apps/&lt;myapp>/templates/&lt;mytemplate>**) à la position correspondante dans l’arborescence du site : c’est ce qui se passe si une page est créée à l’aide de la fonction **Sites web** .

Cette action de copie confère également à la page son contenu initial (généralement le contenu de niveau supérieur uniquement) et la propriété sling:resourceType, le chemin d’accès au composant de page utilisé pour rendre la page (tout ce qui est présent dans le nœud enfant jcr:content).

## Structure d’un modèle {#structure-of-a-template}

Deux aspects doivent être pris en compte :

* la structure du modèle lui-même ;
* la structure du contenu produit lors de l&#39;utilisation d&#39;un modèle ;

Un modèle est créé sous un noeud de type **cq:Template**.

Différentes propriétés peuvent être définies, notamment :

* **jcr:title** - titre du modèle ; s’affiche dans la boîte de dialogue lors de la création d’une page.
* **jcr:description** - description du modèle ; s’affiche dans la boîte de dialogue lors de la création d’une page.

Ce noeud contient *un jcr:content (cq:PageContent)* qui sert de base au noeud de contenu des pages créées. Cette référence, à l’aide de *sling:resourceType*, composant à utiliser pour le rendu du contenu réel d’une nouvelle page.

>[!NOTE]
>
>Pour en savoir plus sur les principes de base des modèles et des composants dans AEM, consultez les ressources ci-dessous :
>
>* [Modèles](/help/sites-developing/templates.md)
>* [Composants](/help/sites-developing/components.md)
>

Une fois que vous avez une compréhension de base des modèles et des composants, consultez les ressources suivantes :

* [Création et ajout de modèles et de composants](/help/mobile/mobile-ondemand-app-templates.md)
* [Utilisation des propriétés de contenu pour exporter du contenu](/help/mobile/on-demand-content-properties-exporting.md)
* [Bonnes pratiques](/help/mobile/best-practices-aem-mobile.md)
* [Développement d’AEM Mobile Content Services](/help/mobile/developing-content-services.md)

### Ressources supplémentaires {#additional-resources}

Pour en savoir plus sur les rubriques supplémentaires sur les applications mobiles, voir les liens ci-dessous :

* [Mobile avec synchronisation de contenu](/help/mobile/mobile-ondemand-contentsync.md)
* [Test des applications mobiles](/help/mobile/develop-mobile-apps-testing.md)
