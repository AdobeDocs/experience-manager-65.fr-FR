---
title: Gestion programmatique des noeuds Preferences
seo-title: Gestion programmatique des noeuds Preferences
description: 'null'
seo-description: 'null'
uuid: f0cb117a-a6cc-4ca5-8511-b3bc9f6738e9
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9d4dba7f-49d8-4112-bc8a-04dafc99a936
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Gestion programmatique des noeuds de préférences {#programmatically-managing-the-preferencesnodes}

Cette rubrique explique comment utiliser l’API du service Preferences Manager (Java) pour gérer par programmation les noeuds Preferences.

Vous pouvez modifier manuellement les paramètres de configuration à partir de l’interface utilisateur de l’administrateur. Pour modifier les options, accédez à `Home>Settings>User Management> Configuration>Manual Configuration`. Importer `config.xml` après avoir apporté les modifications, vous remarquerez que toutes les modifications, à l’exception des modifications apportées au noeud `/Adobe/Adobe Experience Manager Forms/Config/UM persist` , sont perdues. L’aperçu de l’importation et de l’exportation User Management ne prend pas en charge la modification des paramètres de configuration pour les autres composants. Ces modifications peuvent être effectuées à l&#39;aide `PreferencesManagerServiceClient` d&#39;API.

**Résumé des**&#x200B;étapes Pour gérer par programmation les noeuds de préférences, procédez comme suit :

1. Incluez des fichiers de projet.
1. Création d’un client PreferencesManagerService
1. Appeler les opérations de rôle ou d’autorisation appropriées

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un client PreferencesManagerService**

Avant de pouvoir exécuter par programmation une opération User Management PreferencesManagerService, vous devez créer un client PreferencesManagerService. Avec l’API Java, cela se fait en créant un objet PreferencesManagerServiceClient.

**Appeler les opérations de rôle ou d’autorisation appropriées**

Après avoir créé le client de service, vous pouvez appeler les opérations du Gestionnaire de préférences. Le client de service vous permet de lire et de définir des autorisations.
