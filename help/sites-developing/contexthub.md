---
title: ContextHub
seo-title: ContextHub
description: ContextHub est une structure pour stocker, manipuler et présenter des données contextuelles
seo-description: ContextHub is a framework for storing, manipulating, and presenting context data
uuid: 14e6ff4f-ffbe-454a-b2ec-a35333526e27
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: acf5c17a-95b7-43ba-9734-241e20f4f374
exl-id: 3fd50655-7461-4900-a3b8-c01b04c7ba7a
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 53%

---

# ContextHub{#contexthub}

ContextHub est une structure pour stocker, manipuler et présenter des données contextuelles. L&#39;API JavaScript côté client permet d&#39;accéder aux données pour personnaliser le contenu.

>[!NOTE]
>
>L’implémentation [We.Retail de référence](/help/sites-developing/we-retail.md) met en œuvre ContextHub et peut servir de référence lorsque vous intégrez ContextHub dans votre propre projet.

>[!CAUTION]
>
>Le chemin contenant l’exemple de configuration ContextHub utilisé par l’implémentation [We.Retail de référence](/help/sites-developing/we-retail.md) (`/libs/settings/cloudsettings/legacy`) ne doit être utilisé que comme référence pour créer votre propre configuration.
>
>Il ne doit pas être utilisé dans un projet en tant que configuration ContextHub proprement dite.

## Persistance {#persistence}

ContextHub stocke les données de contexte de persistance sur le client. L’API JavaScript ContextHub vous permet d’accéder aux magasins pour créer, mettre à jour et supprimer des données si nécessaire. En tant que tel, ContextHub représente une couche de données sur vos pages.

Chaque magasin ContextHub est une instance d’un type de magasin prédéfini :

* ContextHub fournit plusieurs [exemples de types de magasin](/help/sites-developing/ch-samplestores.md).
* Utilisez AEM consoles pour [créer des magasins](ch-configuring.md#creating-a-contexthub-store).
* Les développeurs peuvent [créer des types de magasin personnalisés](/help/sites-developing/ch-extend.md#creating-custom-store-candidates).
* Les développeurs peuvent [accès aux données du magasin](/help/sites-developing/ch-adding.md#interacting-with-contexthub-stores) via JavaScript.

## Segmentation {#segmentation}

ContextHub propose un moteur de segmentation qui gère les segments et détermine les segments qui sont résolus pour le contexte actuel. Plusieurs segments sont définis. Vous pouvez utiliser l’API JavaScript pour [déterminer les segments résolus ;](/help/sites-developing/ch-adding.md#determining-resolved-contexthub-segments).

## Présentation {#presentation}

La barre d’outils [ContextHub](/help/sites-authoring/ch-previewing.md) permet aux spécialistes du marketing et aux auteurs de voir et de manipuler les données du magasin afin de simuler l’expérience utilisateur lors de la création de pages. La barre d’outils est constituée de groupes de modules d’IU qui permettent d’accéder aux magasins ContextHub.

Chaque module d’IU ContextHub est une instance d’un type de module prédéfini :

* ContextHub fournit plusieurs [exemples de types de module](/help/sites-developing/ch-samplemodules.md).
* Utilisez AEM consoles pour [ajout de modules d’IU](ch-configuring.md#adding-a-ui-module)et à [les regrouper en modes d’interface utilisateur](ch-configuring.md#adding-a-ui-mode).

* Les développeurs peuvent [créer des types de module personnalisés ;](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types).

Les développeurs doivent [ajouter le composant ContextHub à la page ;](/help/sites-developing/ch-adding.md).
