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
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Présentation de la structure de dossiers {#understanding-the-folder-structure}

Les composants de l’espace de travail AEM Forms reposent sur une architecture MVC (modèle-vue-contrôleur) utilisant le modèle Backbone. Chaque composant possède un fichier pour :

* Un modèle contenant une logique de gestion.
* Un fichier HTML contrôleur contenant des commandes d’interface.
* Une vue agissant comme une classe Controller sur le contrôleur.

Les actifs de tous les composants sont placés dans la structure de dossiers décrite ci-dessous. To access the assets, log in to CRXDE Lite and browse to `/libs/ws/js/runtime/`.

**models** contient des modèles Backbone.

**views** Contient des vues Backbone.

**templates** Contient uniquement les modèles HTML pour les composants.

**routes** Contient des routes universelles. Le dossier Templates figurant dans routes contient le code HTML et les références aux composants.

**services** contient l’interface de service permettant d’appeler les API du serveur Adobe Experience Manager sur le point de fin REST.

**util** contient des utilitaires génériques utilisables par plusieurs composants.

**[Contacter le support technique](https://www.adobe.com/account/sign-in.supportportal.html)**
