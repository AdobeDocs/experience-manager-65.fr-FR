---
title: Quels environnements de test sont nécessaires ?
seo-title: Which Test Environments are needed?
description: Plusieurs environnements doivent être pris en compte dans le cadre du test.
seo-description: Several environments should be considered as part of testing
uuid: bb725e50-edae-4c20-8107-d1c8df2e60e2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: db528b9b-3407-462d-8254-20b3cc2c3ccf
exl-id: 05f7a513-5ee7-4870-a691-4a0602e0cbb2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '180'
ht-degree: 100%

---

# Quels environnements de test sont nécessaires ?{#which-test-environments-will-be-needed}

Pour définir les configurations à tester, tenez compte des points suivants :

**Développement** - Pour les tests unitaires, et pour certains tests d’intégration.

**Test** - Pour la majorité des tests.

**En direct** - Pour les tests finaux de performance et de contrainte. Également pour les tests d’acceptation avec le client.

Vous devez également déterminer les instances dont vous aurez besoin et leur emplacement (généralement au moins un de chaque pour tous les niveaux de test) :

**Auteur** - Cette instance permet aux auteurs de saisir le contenu et de le publier.

**Publication** - Cette instance affiche le site web sous sa forme publiée pour que les visiteurs puissent y accéder.

Elle devrait être testée conjointement au Dispatcher.

Enfin, le matériel doit être pris en compte : tous les tests de performance doivent être effectués sur un système aussi proche que possible de la configuration de l’environnement actif final. Pour cette raison, nous vous recommandons également de diviser le lancement du projet de la façon suivante :

**Prélancement** - Disponibilité réduite ; ce qui laisse du temps pour les tests de performance, le réglage et l’optimisation dans des conditions réalistes au sein de l’environnement d’exploitation.

**Lancement complet** - Disponibilité complète.
