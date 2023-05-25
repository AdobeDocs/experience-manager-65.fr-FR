---
title: Mise à jour des fragments de contenu pour un filtrage GraphQL optimisé.
description: Découvrez comment mettre à jour vos fragments de contenu pour le filtrage GraphQL optimisé dans Adobe Experience Manager pour une diffusion de contenu découplée.
source-git-commit: 1481d613783089046b44d4652d38f7b4b16acc4d
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 42%

---


# Mise à jour des fragments de contenu pour un filtrage GraphQL optimisé. {#updating-content-fragments-for-optimized-graphql-filtering}

Pour optimiser les performances de vos filtres GraphQL, exécutez une procédure pour mettre à jour vos fragments de contenu.

>[!NOTE]
>
>Après avoir mis à jour vos fragments de contenu, vous pouvez suivre les recommandations relatives à la [Optimisation des requêtes GraphQL](/help/sites-developing/headless/graphql-api/graphql-optimization.md).

## Prérequis {#prerequisites}

Assurez-vous que vous disposez au minimum de la version 6.5.17.0 d’AEM.

## Mise à jour des fragments de contenu. {#updating-content-fragments}

Pour exécuter la procédure, procédez comme suit :

1. [Configuration des paramètres OSGi](/help/sites-deploying/configuring-osgi.md) pour le **Configuration de la tâche de migration de fragments de contenu**:

   ![Configuration de la tâche de migration de fragments de contenu OSGi](assets/cfm-graphql-update-01.png "Configuration de la tâche de migration de fragments de contenu OSGi")

1. Dans la boîte de dialogue, définissez les deux paramètres suivants :

   * **ContentFragmentMigration:Enabled** : `1`
   * **ContentFragmentMigration:Enforce** : `1`

1. **Enregistrer** les spécifications - la procédure de mise à jour démarre.

1. Attendez que la procédure soit terminée. La procédure est terminée lorsque la propriété `cfGlobalVersion` apparaît sur `/content/dam` et est défini sur `1`.

1. Revenez à la configuration OSGi pour désactiver la procédure.

   Dans la boîte de dialogue du **Configuration de la tâche de migration de fragments de contenu** définissez ces deux paramètres comme suit :

   * **ContentFragmentMigration:Enabled** : `0`
   * **ContentFragmentMigration:Enforce** : `0`

## Limites {#limitations}

Tenez compte des limites suivantes :

* L’optimisation des performances des filtres GraphQL ne sera possible qu’après une mise à jour complète de tous vos fragments de contenu (indiquée par la présence de la propriété `cfGlobalVersion` pour le nœud JCR `/content/dam`).

* Si des fragments de contenu sont importés à partir d’un package de contenu (à l’aide de `crx/de`) après l’exécution de la procédure de mise à jour, ces fragments de contenu ne seront pas pris en compte dans les résultats de la requête GraphQL, tant que la procédure de mise à jour n’aura pas été exécutée à nouveau.