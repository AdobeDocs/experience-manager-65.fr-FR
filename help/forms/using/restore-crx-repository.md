---
title: Impossible de restaurer le référentiel CRX corrompu applicable au serveur de clusters JEE.
description: Découvrez les étapes de restauration d’un référentiel CRX corrompu.
exl-id: 212f61f1-360f-4abe-b874-055ec65454c7
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms, Troubleshooting
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 100%

---

# Impossible de restaurer le référentiel CRX corrompu. {#unable-to-restore-corrupt-crx-repository}

## Problème {#issue}

Pour AEM Forms on JEE, qui utilise une base de données relationnelle, l’heure de la machine hébergeant AEM Forms et celle de la base de données relationnelle doivent toujours être synchronisées de manière absolue. Si l’heure indiquée sur ces machines n’est pas synchronisée, le référentiel CRX d’AEM Forms sur serveur JEE peut devenir inaccessible. Il peut être apparaître comme corrompu et devenir inaccessible via l’URL. L’erreur `AuthenticationsupportService missing` est consignée.

## Prérequis {#prerequisites}

Effectuez la sauvegarde de votre référentiel CRX avant d’effectuer les étapes mentionnées ci-dessous.

## Solution {#solution}

1. Accédez à `https://[AEM Forms Server]:[port]/system/console/bundles`.

1. Recherchez le lot `oak-core` et vérifiez s’il est en cours d’exécution.

1. Redémarrez le lot `oak-core` s’il n’est pas en cours d’exécution. Si l’icône du ![bouton Pause](/help/forms/using/assets/stop.png) se trouve devant le lot `oak-core`, alors cela signifie que le lot est en cours d’exécution.

1. Si le problème n’est toujours pas résolu, restaurez le référentiel CRX à partir de la sauvegarde ou recréez le référentiel CRX si la sauvegarde n’est pas disponible.


## Application {#applies-to}

Cette solution s’applique au cluster AEM Forms on JEE.
