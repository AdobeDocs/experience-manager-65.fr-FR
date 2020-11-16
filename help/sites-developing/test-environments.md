---
title: Quels Environnements de test sont nécessaires ?
seo-title: Quels Environnements de test sont nécessaires ?
description: Plusieurs environnements doivent être considérés comme faisant partie des tests.
seo-description: Plusieurs environnements doivent être considérés comme faisant partie des tests.
uuid: bb725e50-edae-4c20-8107-d1c8df2e60e2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: db528b9b-3407-462d-8254-20b3cc2c3ccf
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 44%

---


# Quels environnements de test sont nécessaires ?{#which-test-environments-will-be-needed}

Pour définir les configurations à tester, tenez compte des points suivants :

**Développement** - Pour l’unité et certains tests d’intégration.

**Tests** - Pour la majorité des tests.

**En direct** - Pour les tests de performances et de stress finaux. Également pour les tests d’acceptation avec le client.

Vous devez également déterminer les instances dont vous aurez besoin et leur emplacement (généralement au moins un de chaque pour tous les niveaux de test) :

**Auteur** : cette instance permet aux auteurs d’entrer et de publier du contenu.

**Publier** : cette instance présente le site Web dans son formulaire publié pour y accéder en visiteur.

Elle devrait être testée conjointement au dispatcher.

Enfin, le matériel doit être pris en compte : tous les tests de performance doivent être effectués sur un système aussi proche que possible de la configuration de l’environnement actif final. Pour cette raison, nous vous recommandons également de diviser le lancement du projet de la façon suivante :

**Lancement** léger - Disponibilité réduite ; qui permet de gagner du temps pour les tests de performances, le réglage et l&#39;optimisation dans des conditions réalistes sur l&#39;environnement de production.

**Lancement** en dur - Disponibilité complète.
