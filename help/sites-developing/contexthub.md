---
title: ContextHub
description: ContextHub est une structure pour stocker, manipuler et présenter des données contextuelles
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: 3fd50655-7461-4900-a3b8-c01b04c7ba7a
solution: Experience Manager, Experience Manager Sites
feature: Developing,Personalization
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 100%

---

# ContextHub{#contexthub}

ContextHub est une structure pour stocker, manipuler et présenter des données contextuelles. L’API Javascript côté client vous permet d’accéder aux données pour personnaliser le contenu.

>[!NOTE]
>
>L’implémentation [We.Retail de référence](/help/sites-developing/we-retail.md) met en œuvre ContextHub et peut servir de référence lorsque vous intégrez ContextHub dans votre propre projet.

>[!CAUTION]
>
>Le chemin contenant l’exemple de configuration ContextHub utilisé par l’implémentation [We.Retail de référence](/help/sites-developing/we-retail.md) (`/libs/settings/cloudsettings/legacy`) ne doit être utilisé que comme référence pour créer votre propre configuration.
>
>Il ne doit pas être utilisé dans un projet en tant que votre propre configuration ContextHub.

## Persistance {#persistence}

ContextHub stocke les données de contexte de persistance sur le client. L’API JavaScript ContextHub vous permet d’accéder aux magasins pour créer, mettre à jour et supprimer des données si nécessaire. En tant que tel, ContextHub représente une couche de données sur vos pages.

Chaque magasin ContextHub est une instance d’un type de magasin prédéfini :

* ContextHub fournit plusieurs [exemples de types de magasin](/help/sites-developing/ch-samplestores.md).
* Utilisez les consoles AEM pour [créer des magasins](ch-configuring.md#creating-a-contexthub-store).
* Les développeurs peuvent [créer des types de magasin personnalisés](/help/sites-developing/ch-extend.md#creating-custom-store-candidates).
* L’équipe de développement peut [accéder aux données du magasin](/help/sites-developing/ch-adding.md#interacting-with-contexthub-stores) via JavaScript.

## Segmentation {#segmentation}

ContextHub propose un moteur de segmentation qui gère les segments et détermine les segments qui sont résolus pour le contexte actuel. Plusieurs segments sont définis. Vous pouvez utiliser l’API JavaScript pour [déterminer les segments résolus](/help/sites-developing/ch-adding.md#determining-resolved-contexthub-segments).

## Présentation {#presentation}

La barre d’outils [ContextHub](/help/sites-authoring/ch-previewing.md) permet aux spécialistes du marketing et aux auteurs de voir et de manipuler les données du magasin afin de simuler l’expérience utilisateur lors de la création de pages. La barre d’outils est constituée de groupes de modules d’IU qui permettent d’accéder aux magasins ContextHub.

Chaque module d’IU ContextHub est une instance d’un type de module prédéfini :

* ContextHub fournit plusieurs [exemples de types de module](/help/sites-developing/ch-samplemodules.md).
* Utilisez les consoles AEM pour [ajouter des modules d’IU](ch-configuring.md#adding-a-ui-module) et [les regrouper en modes d’IU](ch-configuring.md#adding-a-ui-mode).

* Les développeurs et développeuses peuvent [créer des types de module personnalisés](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types).

Les développeurs et développeuses doivent [ajouter le composant ContextHub à la page](/help/sites-developing/ch-adding.md).
