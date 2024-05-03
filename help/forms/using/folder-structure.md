---
title: Présentation de la structure de dossiers
description: Description de la structure des dossiers du code source de l’espace de travail AEM Forms à personnaliser.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: a4c1d3d8-477e-4edf-9dde-4ef9c766be5a
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 100%

---

# Présentation de la structure de dossiers {#understanding-the-folder-structure}

Les composants de l’espace de travail AEM Forms reposent sur une architecture MVC (modèle-vue-contrôleur) utilisant le modèle Backbone. Chaque composant possède un fichier pour :

* un modèle contenant une logique commerciale ;
* un template, c’est-à-dire un fichier HTML contenant des commandes d’interface ;
* une vue agissant comme une classe Controller sur le template.

Les actifs de tous les composants sont placés dans la structure de dossiers décrite ci-dessous. Pour accéder aux ressources, connectez-vous à CRXDE Lite et accédez à `/libs/ws/js/runtime/`.

**modèles** contient des modèles Backbone.

**vues** contient les vues Backbone.

**modèles** contient uniquement les modèles HTML pour les composants.

**itinéraires** contient les itinéraires universels. Le dossier Templates figurant dans routes contient le code HTML et les références aux composants.

**services** contient l’interface de service permettant d’appeler les API du serveur Adobe Experience Manager au point d’entrée REST.

**util** contient des utilitaires génériques utilisables par plusieurs composants.
