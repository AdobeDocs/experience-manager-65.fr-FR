---
title: Outils de test et de suivi
description: AEM fournit une structure pour le test de l’interface utilisateur des composants et un mécanisme pour le test et le débogage des composants.
uuid: 12abedb5-4ee7-4389-9340-e628adbbc053
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 3cf0fd8d-7fc8-468a-bb1e-1debb68a82a5
docset: aem65
exl-id: bb5d1c7c-56ce-4d1e-a3cb-4e74d6922137
source-git-commit: 78c584db8c35ea809048580fe5b440a0b73c8eea
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 11%

---

# Outils de test et de suivi{#testing-and-tracking-tools}

## Tests {#testing}

AEM fournit :

* [Un framework pour tester l’interface utilisateur des composants](/help/sites-developing/hobbes.md).
* [un mécanisme de test et de débogage des composants ;](/help/sites-developing/developer-mode.md).

Voici deux outils de test Open Source :

**Selenium**

Selenium est utilisé pour le test des fonctions dans un navigateur avec un utilisateur par activité. Il enregistre les étapes de test (clics) sous la forme de tables de HTML ou de classes Java™.

Pour plus d’informations, voir [https://www.selenium.dev/](https://www.selenium.dev/).

**JMeter**

JMeter est utilisé pour effectuer le suivi des demandes et peut être utilisé pour les tests fonctionnels, de performance et de stress.

Pour plus d’informations, voir [https://jmeter.apache.org/](https://jmeter.apache.org/).

Il existe également de nombreux outils propriétaires pour automatiser les tests et gérer les plans de test.

### Tracking {#tracking}

Les outils suivants sont facilement disponibles. Cependant, un problème clé dans tous les cas est la disponibilité des données pour tous les membres de l’équipe du projet - partenaire et client.

**Bugzilla**

Un système de suivi des bogues qui peut être configuré selon vos besoins.

**Feuilles de calcul**

Bien qu’il ne s’agisse pas spécifiquement d’un outil de suivi des bogues, les feuilles de calcul sont souvent *mis* utilisés à cette fin, car ils sont faciles à comprendre et la plupart des utilisateurs connaissent leurs fonctionnalités.

Si ces feuilles de calcul sont utilisées pour le suivi, alors :

* ils devraient être simples.
* le nombre de feuilles de calcul individuelles doit être limité au minimum.
* ils doivent être mis à jour régulièrement.
* une seule Principale copie doit être conservée et tout le monde doit savoir où se trouve la Principale copie.
* ils doivent être accessibles à tous les membres du projet.
* si la sécurité est un problème (qui se produit souvent dans les grandes entreprises) et qu’un accès commun n’est pas possible, les copies peuvent être distribuées tant que tout le monde comprend que ces feuilles de calcul sont des copies et ne peuvent pas être mises à jour.

Pour rappel, il existe de nombreux outils propriétaires pour effectuer le suivi des bogues et des fonctionnalités demandées.
