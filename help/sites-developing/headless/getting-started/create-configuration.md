---
title: Guide de prise en main pour la création découplée d’une configuration
description: Créez une configuration comme première étape de prise en main d’AEM 6.5 en mode découplé.
exl-id: f1df97a1-164f-4ed4-bb63-34caf35ae27c
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,GraphQL,Persisted Queries,Developing
role: Admin,Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: bfd4bc52-c397-5127-8f86-8953ba9fc0a3
    internal-label: Headless
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
  - id: a642c50e-80eb-4fc1-a5d2-f3762d1f841d
    internal-label: Administration
  - id: d429a63e-ade4-4117-b04e-9b996d1c94ef
    internal-label: Integrations
  - id: c124fa01-25c5-42ec-adf6-21d1c114058b
    internal-label: Developer tools
subfeature_v2:
  - id: e9db7c79-8f65-4281-a439-c9049296d903
    internal-label: Content Fragments
  - id: a02b73a7-bdfc-4225-bdfd-69f7891ab55e
    internal-label: GraphQL
  - id: d781bc8f-52af-43f6-84d0-b73e59a130d5
    internal-label: Persisted queries
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 91%
---
# Guide de prise en main pour la création découplée d’une configuration {#creating-configuration}

Pour commencer à utiliser le découplage dans AEM 6,5, vous devez créer une configuration.

## Qu’est-ce qu’une configuration ? {#what-is-a-configuration}

L’explorateur de configurations fournit une API de configuration générique, une structure de contenu et un mécanisme de résolution pour les configurations dans AEM.

Dans le contexte d’une gestion de contenu découplée dans AEM, considérez une configuration comme un espace de travail dans AEM où vous pouvez créer vos modèles de contenu, qui définissent la structure de votre futur contenu et des fragments de contenu. Vous pouvez avoir plusieurs configurations pour séparer ces modèles.

>[!NOTE]
>
>Si vous connaissez les modèles de page [dans une implémentation AEM complète,](/help/sites-authoring/templates.md) l’utilisation des configurations pour la gestion des modèles de contenu est similaire.

## Création d’une configuration {#how-to-create-a-configuration}

Un administrateur n’a besoin de créer une configuration qu’une seule fois, ou très rarement lorsqu’un nouvel espace de travail est nécessaire pour organiser vos modèles de contenu. Pour les besoins de ce guide de prise en main, il suffit de créer une configuration.

1. Connectez-vous à AEM as a Cloud Service et dans le menu principal, sélectionnez **Outils -> Général -> Explorateur de configurations**.
1. Indiquez un **Titre** pour votre configuration.
   * Un nom sera automatiquement généré en fonction du titre et adapté selon les [conventions de nommage d’AEM.](/help/sites-developing/naming-conventions.md). Il devient le nom du nœud dans le référentiel.
1. Vérifiez les options suivantes :
   * **Modèles de fragment de contenu**
   * **Requêtes persistantes GraphQL**

   ![Création d’une configuration](assets/create-configuration.png)

1. Cliquez sur **Créer**.

Vous pouvez créer plusieurs configurations si nécessaire. Les configurations peuvent également être imbriquées.

>[!NOTE]
>
>Des options de configuration en plus des **Modèles de fragments de contenu** et des **Requêtes persistantes GraphQL** peuvent être nécessaires en fonction de vos exigences d’implémentation.

## Étapes suivantes {#next-steps}

Cette configuration vous permet maintenant de passer à la deuxième partie du guide de prise en main et de [créer des modèles de fragments de contenu.](create-content-model.md)

<!--
>[!TIP]
>
>For complete details about the Configuration Browser, [see the Configuration Browser documentation.](/help/sites-developing/configurations.md)
-->
