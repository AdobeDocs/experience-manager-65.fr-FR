---
title: Effectuer des vérifications transversales et des contrôles de cohérence
description: Découvrez comment effectuer des vérifications de cohérence et de parcours.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
feature: Configuring
exl-id: 10dde29b-5dc7-4d4e-80ae-3d4fd0397f7e
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 100%

---

# Effectuer des vérifications transversales et des contrôles de cohérence{#consistency-and-traversal-checks}

Lors de la mise à niveau, des problèmes peuvent survenir en raison d’incohérences dans l’espace de travail. Vous pouvez exécuter une mise à niveau de test pour voir si ce type d’incohérence pose problème ou exécuter des vérifications de cohérence comme action préventive.

Si vous exécutez une mise à niveau de test qui échoue en raison d’incohérences de l’espace de travail, vous rencontrez, dans le journal crx-quickstart/logs/crx/error.log, des entrées similaires à celles présentées ci-dessous :

```xml
*ERROR* TarPersistenceManager: No bundle found for uuid 'deadbeef-cafe-babe-cafe-babecafebabe'
 ...
*ERROR* RepositoryImpl: Failed to initialize workspace 'crx.default'
javax.jcr.RepositoryException: Error indexing workspace: Error indexing workspace: Error indexing workspace
...
```

## Réalisation d’une vérification de cohérence {#perform-a-consistency-check}

Pour réaliser une vérification de cohérence, accédez à la page d’administration de JMX MBean **com.adobe.granite (référentiel)**. Depuis l’écran principal d’AEM, accédez à :

**Outils > Console Web > Principal (dans la barre de menus) > JMX > com.adobe.granite (Repository)**

Dans une installation par défaut, il se trouve ici :**[|Afficher](http://localhost:4502/system/console/jmx/com.adobe.granite%3Atype%3DRepository)**

Dans la section **Opérations** de la page, vous trouverez deux méthodes : **`traversalCheck`** et **`consistencyCheck`**. Pour exécuter une vérification, cliquez sur l’opération et saisissez les paramètres souhaités.

![chlimage_1-117](assets/chlimage_1-117.png)
