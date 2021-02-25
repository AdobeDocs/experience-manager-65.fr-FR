---
title: Gestion par programmation des préférencesNodes
seo-title: Gestion par programmation des préférencesNodes
description: Utilisez l’API de service Preferences Manager (Java) pour gérer par programmation les noeuds Preferences.
seo-description: Utilisez l’API de service Preferences Manager (Java) pour gérer par programmation les noeuds Preferences.
uuid: f0cb117a-a6cc-4ca5-8511-b3bc9f6738e9
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9d4dba7f-49d8-4112-bc8a-04dafc99a936
translation-type: tm+mt
source-git-commit: 9cf46a26d2aa2e41b924a4de89cf8ab5fdeeefc6
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 0%

---


# Gestion par programmation des noeuds de préférences {#programmatically-managing-the-preferencesnodes}

**Les exemples et exemples de ce document ne concernent que l’environnement AEM Forms on JEE.**

Cette rubrique décrit comment vous pouvez utiliser l’API de service Preferences Manager (Java) pour gérer par programmation les noeuds Preferences.

Vous pouvez modifier manuellement les paramètres de configuration à partir de l’interface utilisateur de l’administrateur. Pour modifier les options, accédez à `Home>Settings>User Management> Configuration>Manual Configuration`. Importez `config.xml` après avoir apporté les modifications, vous remarquerez que toutes les modifications, à l&#39;exception des modifications apportées au noeud `/Adobe/Adobe Experience Manager Forms/Config/UM persist`, sont perdues. La prévisualisation de l’importation et de l’exportation User Management ne prend pas en charge la modification des paramètres de configuration pour les autres composants. Désormais, ces modifications peuvent être effectuées à l’aide des API `PreferencesManagerServiceClient`.

**Résumé des**&#x200B;étapes Pour gérer par programmation les noeuds de préférences, effectuez les étapes suivantes :

1. Incluez des fichiers de projet.
1. Création d’un client PreferencesManagerService
1. Appeler le rôle approprié ou les opérations d’autorisation

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un client PreferencesManagerService**

Avant de pouvoir exécuter par programmation une opération User Management PreferencesManagerService, vous devez créer un client PreferencesManagerService. Avec l’API Java, cela se fait en créant un objet PreferencesManagerServiceClient.

**Appeler le rôle approprié ou les opérations d’autorisation**

Une fois le client de service créé, vous pouvez appeler les opérations du Gestionnaire de préférences. Le client de service vous permet de lire et de définir des autorisations.
