---
title: Modèles et composants d’application
seo-title: Modèles et composants d’application
description: Consultez cette page pour en savoir plus sur les modèles d’application et les composants. Il fournit des informations détaillées sur la structure des modèles.
seo-description: Consultez cette page pour en savoir plus sur les modèles d’application et les composants. Il fournit des informations détaillées sur la structure des modèles.
uuid: ba2fd91b-de5a-4f39-a976-5455f9983669
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: 7f31c6a7-92d5-4a87-a9f0-68a82b834d5a
exl-id: 58d95325-7cb1-4204-842d-17add70e1fbf
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 51%

---

# Modèles d’application et composants{#app-templates-and-components}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

Un modèle sert à créer une page. Il définit les composants pouvant être utilisés dans l’étendue sélectionnée. Un modèle est une hiérarchie de nœuds qui a la même structure que la page à créer, mais sans contenu réel.

Chaque modèle présente une sélection de composants disponibles.

* Les modèles sont constitués de [Composants](/help/sites-developing/components.md) ;
* Les composants utilisent et autorisent l’accès aux Widgets et ceux-ci sont utilisés pour rendre le contenu.

>[!NOTE]
>
>Pour savoir comment développer votre application AEM à l’aide de CRXDE Lite, voir [Développement avec CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

Un modèle sert de fondement pour une page.

Pour créer une page, le modèle doit être copié (node-tree **/apps/&lt;myapp>/templates/&lt;mytemplate>**) à la position correspondante dans l’arborescence du site : c’est ce qui se passe si une page est créée à l’aide de l’onglet **Sites web** .

Cette action de copie confère également à la page son contenu initial (généralement le contenu de niveau supérieur uniquement) et la propriété sling: resourceType, le chemin d’accès au composant de page utilisé pour rendre la page (tout ce qui est présent dans le nœud enfant jcr:content).

## Structure d’un modèle {#structure-of-a-template}

Il y a deux aspects à considérer :

* la structure du modèle lui-même
* la structure du contenu produit lorsqu’un modèle est utilisé

Un modèle est créé sous un nœud de type **cq:Template**.

Différentes propriétés peuvent être définies, en particulier :

* **jcr:title**- titre du modèle. Apparaît dans la boîte de dialogue lors de la création d’une page.
* **jcr:description**- description du modèle. Apparaît dans la boîte de dialogue lors de la création d’une page.

Ce noeud contient *un noeud jcr:content (cq:PageContent)* qui doit être utilisé comme base du noeud de contenu des pages résultantes ; cette référence, à l’aide de *sling:resourceType*, le composant à utiliser pour le rendu du contenu réel d’une nouvelle page.

>[!NOTE]
>
>Pour en savoir plus sur les principes de base des modèles et des composants dans AEM, consultez les ressources ci-dessous :
>
>* [Modèles](/help/sites-developing/templates.md)
* [Composants](/help/sites-developing/components.md)



Une fois que vous avez une compréhension de base des modèles et des composants, consultez les ressources suivantes :

* [Création et ajout de modèles et de composants](/help/mobile/mobile-ondemand-app-templates.md)
* [Utilisation des propriétés de contenu pour exporter du contenu](/help/mobile/on-demand-content-properties-exporting.md)
* [Bonnes pratiques](/help/mobile/best-practices-aem-mobile.md)
* [Développement d’AEM Mobile Content Services](/help/mobile/developing-content-services.md)

### Ressources supplémentaires {#additional-resources}

Pour en savoir plus sur les rubriques supplémentaires sur les applications mobiles, voir les liens ci-dessous :

* [Mobile avec synchronisation de contenu](/help/mobile/mobile-ondemand-contentsync.md)
* [Test des applications mobiles](/help/mobile/develop-mobile-apps-testing.md)
