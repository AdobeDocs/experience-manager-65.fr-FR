---
title: Effectuer des vérifications transversales et des contrôles de cohérence
seo-title: Consistency and Traversal Checks
description: Découvrez comment effectuer des vérifications transversales et des contrôles de cohérence.
seo-description: Learn how to perform consistency and traversal checks.
uuid: 0304e378-7c60-4bf5-9052-d01149d2a6df
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: af9a3e9d-194a-42e5-be28-b238e0c1e55e
feature: Configuring
exl-id: 10dde29b-5dc7-4d4e-80ae-3d4fd0397f7e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '156'
ht-degree: 100%

---

# Effectuer des vérifications transversales et des contrôles de cohérence{#consistency-and-traversal-checks}

Lors de la mise à niveau, vous pouvez rencontrer des problèmes dus à des incohérences de l’espace de travail. Vous pouvez exécuter une mise à niveau de test pour voir si ce type d’incohérence pose problème ou exécuter des vérifications de cohérence comme action préventive.

Si vous exécutez une mise à niveau de test qui échoue en raison d’incohérences de l’espace de travail, vous rencontrez, dans le journal crx-quickstart/logs/crx/error.log, des entrées similaires à celles présentées ci-dessous :

```xml
*ERROR* TarPersistenceManager: No bundle found for uuid 'deadbeef-cafe-babe-cafe-babecafebabe'
 ...
*ERROR* RepositoryImpl: Failed to initialize workspace 'crx.default'
javax.jcr.RepositoryException: Error indexing workspace: Error indexing workspace: Error indexing workspace
...
```

## Réalisation d’une vérification de cohérence {#perform-a-consistency-check}

Pour réaliser une vérification de cohérence, accédez à la page d’administration de JMX MBean **com.adobe.granite (Repository)**. Depuis l’écran principal d’AEM, accédez à :

**Outils > Console Web > Principal (dans la barre de menus) > JMX > com.adobe.granite (Repository)**

Dans une installation par défaut, il se trouve ici :**[|Afficher](http://localhost:4502/system/console/jmx/com.adobe.granite%3Atype%3DRepository)**

Dans la section **Opérations** de la page, vous trouverez deux méthodes : **`traversalCheck`** et **`consistencyCheck`**. Pour exécuter une vérification, cliquez sur l’opération et saisissez les paramètres souhaités.

![chlimage_1-117](assets/chlimage_1-117.png)
