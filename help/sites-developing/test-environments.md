---
title: Quels environnements de test sont nécessaires ?
description: Plusieurs environnements doivent être pris en compte dans le cadre du test.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
exl-id: 05f7a513-5ee7-4870-a691-4a0602e0cbb2
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 100%

---

# Quels environnements de test sont nécessaires ?{#which-test-environments-will-be-needed}

Pour définir les configurations à tester, tenez compte des points suivants :

**Développement** - Pour les tests unitaires, et pour certains tests d’intégration.

**Tests** - Pour la plupart des tests.

**En direct** - Pour les tests finaux de performance et de contrainte. Également pour les tests d’acceptation avec le client.

Déterminez les instances dont vous avez besoin et où (généralement au moins une de chacune pour tous les niveaux de test) :

**Auteur** - Cette instance permet aux auteurs de saisir le contenu et de le publier.

**Publication** - Cette instance affiche le site web sous sa forme publiée pour que les visiteurs puissent y accéder.

Testé avec Dispatcher.

Enfin, le matériel doit être pris en compte : tous les tests de performance doivent être effectués sur un système aussi proche que possible de la configuration de l’environnement actif final. Pour cette raison, il est également recommandé de diviser le lancement du projet en :

**Prélancement** - Disponibilité réduite ; ce qui laisse du temps pour les tests de performance, le réglage et l’optimisation dans des conditions réalistes au sein de l’environnement de production.

**Lancement complet** - Disponibilité complète.
