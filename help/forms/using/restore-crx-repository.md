---
title: Impossible de restaurer le référentiel CRX corrompu applicable au serveur de clusters JEE.
description: Découvrez les étapes de restauration d’un référentiel CRX corrompu.
exl-id: 212f61f1-360f-4abe-b874-055ec65454c7
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 100%
---
# Impossible de restaurer le référentiel CRX corrompu. {#unable-to-restore-corrupt-crx-repository}

## Problème {#issue}

Pour AEM Forms on JEE, qui utilise une base de données relationnelle, l’heure de la machine hébergeant AEM Forms et celle de la base de données relationnelle doivent toujours être synchronisées de manière absolue. Si l’heure indiquée sur ces machines n’est pas synchronisée, le référentiel CRX d’AEM Forms sur serveur JEE peut devenir inaccessible. Il peut apparaître comme corrompu et devenir inaccessible via l’URL. L’erreur `AuthenticationsupportService missing` est consignée.

## Prérequis {#prerequisites}

Effectuez la sauvegarde de votre référentiel CRX avant d’effectuer les étapes mentionnées ci-dessous.

## Solution {#solution}

1. Accédez à `https://[AEM Forms Server]:[port]/system/console/bundles`.

1. Recherchez le bundle `oak-core` et vérifiez s’il est en cours d’exécution.

1. Redémarrez le bundle `oak-core` s’il n’est pas en cours d’exécution. Si l’icône du ![bouton Pause](/help/forms/using/assets/stop.png) se trouve devant le bundle `oak-core`, cela signifie que le bundle est en cours d’exécution.

1. Si le problème n’est toujours pas résolu, restaurez le référentiel CRX à partir de la sauvegarde ou recréez le référentiel CRX si la sauvegarde n’est pas disponible.


## Application {#applies-to}

Cette solution s’applique au cluster AEM Forms on JEE.
