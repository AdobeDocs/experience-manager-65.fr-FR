---
title: "Correspondence Management\_: dépannage"
description: Gérez les erreurs qui peuvent se produire lors du processus d’enregistrement d’une lettre dans un environnement AEM Forms.
uuid: 25828cdd-110e-4a84-8f31-d82cd610a54f
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: cc473808-e71a-4834-bb30-91e6df783e60
feature: Correspondence Management
exl-id: cf06796b-bb8c-4a65-8f42-02fb0cfa3ebd
source-git-commit: 68a1edf5f62d7a988094fceb3f762504711dc2f1
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 21%

---

# Correspondence Management : dépannage {#correspondence-management-troubleshooting}

## Erreurs lors de l’enregistrement d’une lettre {#errors-when-saving-a-letter}

### Problème {#issue}

L’une des erreurs suivantes s’affichait lors de l’enregistrement d’une lettre :

* Liaison de données non présente pour le module de texte
* Indiquez les informations de propriété nécessaires pour les éléments suivants :

### Raison {#reason}

Ces erreurs peuvent se produire en raison de l’une des raisons suivantes :

* Un dictionnaire de données est lié à la lettre mais n’est pas présent sur le serveur.
* Un dictionnaire de données est lié à la lettre, mais son nom comporte un trait de soulignement (_).

### Solution {#workaround}

Assurez-vous que le dictionnaire de données que vous utilisez dans la lettre est présent sur le serveur et que son nom ne comporte pas de trait de soulignement (_).

## Erreur lors de la prévisualisation d’une lettre {#error-when-previewing-a-letter}

### Problème {#issue-1}

Lors de l’aperçu d’une lettre, l’erreur &quot;Erreur lors du chargement de la lettre : impossible d’importer une ressource à partir d’une entrée XML&quot; s’affiche même lorsqu’une ressource de texte précédemment non publiée dans la lettre est publiée.

### Solution {#workaround-1}

Réinitialisez le cache de lettres sur l’instance de publication en procédant comme suit, puis réessayez d’afficher la lettre :

1. Accédez à **`https://'[server]:[port]'/[contextPath]/system/console/configMgr`** et connectez-vous en tant qu’administrateur.
1. Sélectionnez **Configurations de Correspondence Management**.
1. Dans **Configurations de Correspondence Management**, désactivez l’option **Activer le cache de lettre**, puis cliquez sur **Enregistrer**.
1. Activez l’option **Activer le cache de lettre**, puis cliquez sur **Enregistrer**.
1. Réessayez d’afficher la lettre.
