---
title: Gestion par programmation des nœuds de préférences
description: Utilisez l’API de service du Gestionnaire de Préférences (Java) pour gérer par programmation les nœuds de préférences.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 108eb249-879b-4e4f-b431-8118b8656e62
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,APIs & Integrations
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 516393bc-fa69-5e74-a04e-f7ec9ffe2c5e
    internal-label: APIs & Integrations
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 100%
---
# Gestion par programmation des nœuds de préférences {#programmatically-managing-the-preferencesnodes}

**Les exemples et les échantillons de ce document sont réservés à l’environnement AEM Forms sur JEE.**

Cette rubrique décrit comment utiliser l’API de service du Gestionnaire de préférences (Java) pour gérer par programmation les nœuds de préférences.

Vous pouvez modifier manuellement les paramètres de configuration à partir de l’interface utilisateur de l’administrateur. Pour modifier les options, accédez à `Home>Settings>User Management> Configuration>Manual Configuration`. Importez `config.xml` après avoir apporté les modifications. Vous remarquerez que toutes les modifications, à l’exception des modifications apportées au nœud `/Adobe/Adobe Experience Manager Forms/Config/UM persist` sont perdues. L’aperçu de l’importation et de l’exportation de User Management ne prend pas en charge la modification des paramètres de configuration d’autres composants. Désormais, ces modifications peuvent être effectuées à l’aide des API `PreferencesManagerServiceClient`.

**Résumé des étapes** Pour gérer par programmation les nœuds de préférences, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créer un client PreferencesManagerService
1. Appeler les opérations de rôle ou d’autorisation appropriées

**Inclure des fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, veillez à inclure les fichiers proxy.

**Créer un client PreferencesManagerService**

Avant d’effectuer par programmation une opération de User Management PreferencesManagerService, vous devez créer un client PreferencesManagerService. Avec l’API Java, cela se fait en créant un objet PreferencesManagerServiceClient.

**Appeler les opérations de rôle ou d’autorisation appropriées**

Une fois le client de service créé, vous pouvez alors appeler les opérations du Gestionnaire de préférences. Le client de service vous permet de lire et de définir des autorisations.
