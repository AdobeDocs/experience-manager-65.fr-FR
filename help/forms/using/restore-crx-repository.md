---
title: Impossible de restaurer le référentiel CRX corrompu applicable au serveur de grappe JEE
description: Procédure de restauration du référentiel CRX corrompu
source-git-commit: a7d125503b0bd3c52cb3a959e2f0dde1a69cbe2b
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 8%

---

# Impossible de restaurer le référentiel CRX corrompu {#unable-to-restore-corrupt-crx-repository}

## Problème {#issue}

Pour AEM Forms déployé sur JEE avec une persistance RDB, il est nécessaire que les machines hôtes AEM Forms et les machines de base de données soient synchronisées en temps absolu. Cependant, si, pour une raison quelconque, les horloges ne sont pas synchronisées, le référentiel CRX est corrompu et ses URL deviennent inaccessibles. L’erreur en tant que `AuthenticationsupportService missing` survient dans les fichiers journaux.

## Solution {#solution}

Exécutez les étapes suivantes afin de résoudre ce problème :
1. Accédez à  [https://localhost:4502/system/console/bundles](http://localhost:4502/system/console/bundles).

1. Recherchez la variable `oak-core` et vérifiez qu’il est en cours d’exécution.

1. Redémarrez le `oak-core` s’il n’est pas en cours d’exécution. Si le bouton de pause se trouve devant la fonction `oak-core` du lot, puis il indique que le lot est à l’état en cours d’exécution.

1. Si le problème n’est toujours pas résolu, restaurez à partir du référentiel CRX à partir de la sauvegarde ou recréez le référentiel CRX si la sauvegarde n’est pas disponible.

   >[!NOTE]
   >
   >Effectuez la sauvegarde de votre référentiel CRX avant d’effectuer les étapes ci-dessus.

## S’applique à {#applies-to}

Cette solution s’applique à :

* Serveur de la grappe AEM Forms on JEE


