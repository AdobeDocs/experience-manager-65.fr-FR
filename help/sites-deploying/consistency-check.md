---
title: Effectuer des vérifications transversales et des contrôles de cohérence
description: Découvrez comment effectuer des vérifications de cohérence et de traversée.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
feature: Configuring
exl-id: 10dde29b-5dc7-4d4e-80ae-3d4fd0397f7e
source-git-commit: b66ec42c35b5b60804015d340b8194bbd6ef3e28
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 31%

---

# Effectuer des vérifications transversales et des contrôles de cohérence{#consistency-and-traversal-checks}

Lors de la mise à niveau, des problèmes peuvent se produire en raison d’incohérences de l’espace de travail. Vous pouvez exécuter une mise à niveau de test pour voir s’il s’agit d’un problème ou exécuter les contrôles de cohérence comme action préventive.

Si vous exécutez une mise à niveau de test qui échoue en raison d’incohérences de l’espace de travail, des entrées similaires à celles présentées dans crx-quickstart/logs/crx/error.log :

```xml
*ERROR* TarPersistenceManager: No bundle found for uuid 'deadbeef-cafe-babe-cafe-babecafebabe'
 ...
*ERROR* RepositoryImpl: Failed to initialize workspace 'crx.default'
javax.jcr.RepositoryException: Error indexing workspace: Error indexing workspace: Error indexing workspace
...
```

## Réalisation d’une vérification de cohérence {#perform-a-consistency-check}

Pour vérifier la cohérence, accédez à la page d’administration du MBean JMX. **com.adobe.granite (référentiel)**. Depuis l’écran principal d’AEM, accédez à :

**Outils > Console Web > Principal (dans la barre de menus) > JMX > com.adobe.granite (Repository)**

Dans une installation par défaut, il se trouve ici :**[|Afficher](http://localhost:4502/system/console/jmx/com.adobe.granite%3Atype%3DRepository)**

Dans le **Opérations** de la page, vous trouverez deux méthodes : **`traversalCheck`** et **`consistencyCheck`**. Pour effectuer une vérification, cliquez sur l’opération et saisissez les paramètres souhaités.

![chlimage_1-117](assets/chlimage_1-117.png)
