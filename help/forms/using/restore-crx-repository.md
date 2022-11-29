---
title: Impossible de restaurer le référentiel CRX corrompu applicable au serveur de grappe JEE
description: Procédure de restauration du référentiel CRX corrompu
exl-id: 212f61f1-360f-4abe-b874-055ec65454c7
source-git-commit: c4f776b08cb8cc8c6eea78a3757735e063bec20c
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 7%

---

# Impossible de restaurer le référentiel CRX corrompu {#unable-to-restore-corrupt-crx-repository}

## Problème {#issue}

Pour AEM Forms on JEE qui utilise une base de données relationnelle, le temps passé sur l’ordinateur hébergeant AEM Forms et la base de données relationnelle doit toujours être synchronisé de manière absolue. Si le temps passé sur ces ordinateurs n’est pas synchronisé, le référentiel CRX du serveur AEM Forms on JEE peut devenir inaccessible. Il peut sembler corrompu et devenir inaccessible via l’URL. Le `AuthenticationsupportService missing` est consignée.

## Prérequis {#prerequisites}

Effectuez la sauvegarde de votre référentiel CRX avant d’effectuer les étapes mentionnées ci-dessous.

## Solution {#solution}

Exécutez les étapes suivantes afin de résoudre ce problème :
1. Accédez à  `https://[AEM Forms Server]:[port]/system/console/bundles`.

1. Recherchez la variable `oak-core` et vérifiez s’il est en cours d’exécution.

1. Redémarrez le `oak-core` s’il n’est pas en cours d’exécution. If  ![Bouton Pause](/help/forms/using/assets/stop.png) se trouve devant l’icône `oak-core` du lot, puis il indique que le lot est à l’état en cours d’exécution.

1. Si le problème n’est toujours pas résolu, restaurez à partir du référentiel CRX à partir de la sauvegarde ou recréez le référentiel CRX si la sauvegarde n’est pas disponible.


## S’applique à {#applies-to}

Cette solution s’applique à :

* Grappe AEM Forms on JEE