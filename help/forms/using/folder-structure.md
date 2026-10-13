---
title: Présentation de la structure de dossiers
description: Description de la structure des dossiers du code source de l’espace de travail AEM Forms à personnaliser.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: a4c1d3d8-477e-4edf-9dde-4ef9c766be5a
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 97aafc4b-2598-52d6-9012-295a95969e38
    internal-label: HTML5 Forms
  - id: 59f95943-e802-56ac-990d-21ab923984c1
    internal-label: Mobile Forms
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
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
