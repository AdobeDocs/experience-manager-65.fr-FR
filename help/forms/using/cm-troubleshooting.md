---
title: '« Correspondence Management : dépannage »'
description: Découvrez comment gérer les erreurs qui apparaissent pendant le processus d’enregistrement d’une lettre dans un environnement AEM Forms.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
feature: Correspondence Management
exl-id: cf06796b-bb8c-4a65-8f42-02fb0cfa3ebd
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 100%

---

# Correspondence Management : dépannage {#correspondence-management-troubleshooting}

## Erreurs lors de l’enregistrement d’une lettre {#errors-when-saving-a-letter}

### Problème {#issue}

L’une des erreurs suivantes s’est affichée lors de l’enregistrement d’une lettre :

* La liaison de données n’est pas définie pour le module de texte.
* Fournissez les informations de propriété nécessaires pour les éléments suivants.

### Raison {#reason}

Ces erreurs peuvent se produire à cause de l’une des raisons suivantes :

* Un dictionnaire de données est associé à la lettre, mais n’est pas présent sur le serveur.
* Un dictionnaire de données est associé à la lettre, mais son nom comporte un caractère de soulignement (_).

### Solution {#workaround}

Assurez-vous que le dictionnaire de données utilisé dans la lettre est présent sur le serveur et que son nom ne comporte aucun trait de soulignement (_).

## Erreur lors de la prévisualisation d’une lettre {#error-when-previewing-a-letter}

### Problème {#issue-1}

Lors de la prévisualisation d’une lettre, l’erreur « Erreur lors du chargement de la lettre : import de la ressource impossible depuis l’entrée XML » apparaît même lorsqu’une ressource de texte précédemment non publiée dans la lettre est publiée.

### Solution {#workaround-1}

Réinitialisez le cache de lettre sur l’instance de publication en suivant les étapes ci-après, puis réessayez d’afficher la lettre :

1. Accédez à **`https://'[server]:[port]'/[contextPath]/system/console/configMgr`** et connectez-vous en tant qu’administrateur.
1. Sélectionnez **Configurations de Correspondence Management**.
1. Dans **Configurations de Correspondence Management**, désactivez l’option **Activer le cache de lettre**, puis cliquez sur **Enregistrer**.
1. Cochez l’option **Activer le cache de lettre**, puis cliquez sur **Enregistrer**.
1. Réessayez d’afficher la lettre.
