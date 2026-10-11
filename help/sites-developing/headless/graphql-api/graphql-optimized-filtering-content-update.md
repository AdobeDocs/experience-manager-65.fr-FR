---
title: Mise à jour des fragments de contenu pour un filtrage GraphQL optimisé
description: Découvrez comment mettre à jour vos fragments de contenu pour le filtrage GraphQL optimisé dans Adobe Experience Manager pour une diffusion de contenu découplée.
exl-id: d78ec052-c091-49ca-9f36-a3d24eb9edd5
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
source-wordcount: '249'
ht-degree: 93%
---
# Mise à jour des fragments de contenu pour un filtrage GraphQL optimisé {#updating-content-fragments-for-optimized-graphql-filtering}

Pour optimiser les performances de vos filtres GraphQL, exécutez une procédure pour mettre à jour vos fragments de contenu.

>[!NOTE]
>
>Après avoir mis à jour vos fragments de contenu, vous pouvez suivre les recommandations relatives à l’[Optimisation des requêtes GraphQL](/help/sites-developing/headless/graphql-api/graphql-optimization.md).

## Conditions préalables {#prerequisites}

Assurez-vous de disposer au minimum de la version 6.5.17.0 d’AEM.

## Mise à jour des fragments de contenu {#updating-content-fragments}

Pour exécuter la procédure, procédez comme suit :

1. [Configuration des paramètres OSGi](/help/sites-deploying/configuring-osgi.md) pour la **Configuration de la tâche de migration de fragments de contenu** :

   ![Configuration de la tâche de migration de fragments de contenu OSGi](assets/cfm-graphql-update-01.png "Configuration de la tâche de migration de fragments de contenu OSGi")

1. Dans la boîte de dialogue, définissez les deux paramètres de la manière suivante :

   * **ContentFragmentMigration:Enabled** : `1`
   * **ContentFragmentMigration:Enforce** : `1`

1. **Enregistrer** les spécifications - la procédure de mise à jour démarre.

1. Attendez que la procédure soit terminée. La procédure est terminée lorsque la propriété `cfGlobalVersion` apparaît sur `/content/dam` et est définie sur `1`.

1. Revenez à la configuration OSGi pour désactiver la procédure.

   Dans la boîte de dialogue de la **Configuration de la tâche de migration de fragments de contenu**, définissez ces deux paramètres comme suit :

   * **ContentFragmentMigration:Enabled** : `0`
   * **ContentFragmentMigration:Enforce** : `0`

## Limites {#limitations}

Gardez à l’esprit les limites suivantes :

* L’optimisation des performances des filtres GraphQL ne sera possible qu’après une mise à jour complète de tous vos fragments de contenu (indiquée par la présence de la propriété `cfGlobalVersion` pour le nœud JCR `/content/dam`).

* Si des fragments de contenu sont importés à partir d’un module de contenu (à l’aide de `crx/de`) après l’exécution de la procédure de mise à jour, ces fragments de contenu ne seront pas pris en compte dans les résultats de la requête GraphQL, tant que la procédure de mise à jour n’aura pas été exécutée à nouveau.
