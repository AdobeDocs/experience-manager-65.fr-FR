---
title: Présentation de la structure de dossiers
seo-title: Présentation de la structure de dossiers
description: Description de la structure des dossiers du code source de l’espace de travail AEM Forms à personnaliser.
seo-description: Description de la structure des dossiers du code source de l’espace de travail AEM Forms à personnaliser.
uuid: ee844f89-887e-4f07-9db3-389859baa374
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 7427858d-8eec-423d-a0a9-444140420620
exl-id: a4c1d3d8-477e-4edf-9dde-4ef9c766be5a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 66%

---

# Présentation de la structure de dossiers {#understanding-the-folder-structure}

Les composants de l’espace de travail AEM Forms reposent sur une architecture MVC (modèle-vue-contrôleur) utilisant le modèle Backbone. Chaque composant possède un fichier pour :

* Un modèle contenant une logique de gestion.
* Un fichier HTML contrôleur contenant des commandes d’interface.
* Une vue agissant comme une classe Controller sur le contrôleur.

Les actifs de tous les composants sont placés dans la structure de dossiers décrite ci-dessous. Pour accéder aux ressources, connectez-vous à CRXDE Lite et accédez à `/libs/ws/js/runtime/`.

**** modelsContient des modèles Backbone.

**** viewsContient des vues Backbone.

**** templatesContient uniquement les modèles HTML pour les composants.

**** routesContient des routes universelles. Le dossier Templates figurant dans routes contient le code HTML et les références aux composants.

**** servicesContient l’interface de service pour appeler les API du serveur Adobe Experience Manager sur le point de terminaison REST.

**** utilContient des utilitaires génériques utilisables par plusieurs composants.
