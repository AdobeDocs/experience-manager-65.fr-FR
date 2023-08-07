---
title: Outils de test et de suivi
description: AEM fournit un framework pour le test de l’interface utilisateur des composants et un mécanisme pour le test et le débogage des composants
uuid: 12abedb5-4ee7-4389-9340-e628adbbc053
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 3cf0fd8d-7fc8-468a-bb1e-1debb68a82a5
docset: aem65
exl-id: bb5d1c7c-56ce-4d1e-a3cb-4e74d6922137
source-git-commit: 78c584db8c35ea809048580fe5b440a0b73c8eea
workflow-type: ht
source-wordcount: '292'
ht-degree: 100%

---

# Outils de test et de suivi{#testing-and-tracking-tools}

## Tests {#testing}

AEM fournit :

* [Un framework pour tester l’interface utilisateur des composants](/help/sites-developing/hobbes.md).
* [Un mécanisme de test et de débogage des composants](/help/sites-developing/developer-mode.md).

Voici deux outils de test Open Source :

**Selenium**

Selenium est utilisé pour le test des fonctions dans un navigateur avec un utilisateur ou une utilisatrice par activité. Il enregistre les étapes de test (clics) sous la forme de tables HTML ou de classes Java™.

Pour plus d’informations, consultez [https://www.selenium.dev/](https://www.selenium.dev/).

**JMeter**

JMeter sert à effectuer le suivi des demandes et peut être utilisé pour les tests fonctionnels, de performances et de stress.

Pour plus d’informations, consultez [https://jmeter.apache.org/](https://jmeter.apache.org/).

Il existe également de nombreux outils propriétaires pour automatiser les tests et gérer les plans de test.

### Suivi {#tracking}

Les outils suivants sont facilement accessibles. Cependant, la disponibilité des données pour tous les membres de l’équipe du projet, partenaires et clientèle, constitue toujours une question clé.

**Bugzilla**

Un système de suivi des bogues qui peut être configuré selon vos besoins.

**Feuilles de calcul**

Bien qu’il ne s’agisse pas spécifiquement d’un outil de suivi des bogues, les feuilles de calcul sont souvent *utilisées* à cette fin, car elles sont faciles à comprendre et la plupart des utilisateurs et utilisatrices connaissent leurs fonctionnalités.

Si ces feuilles de calcul sont utilisées pour le suivi :

* Elles doivent être simples.
* Le nombre de feuilles de calcul doit être limité au minimum.
* Elles doivent être mises à jour régulièrement.
* Une seule copie principale doit être conservée et tout le monde doit savoir où elle se trouve.
* Elles doivent être accessibles à tous les membres du projet.
* Si la sécurité constitue un point sensible (dans les grandes entreprises, en général) et qu’un accès commun n’est pas envisageable, les copies peuvent être distribuées tant que tout le monde comprend que ces feuilles de calcul sont des copies et qu’elles ne peuvent pas être mises à jour.

Pour rappel, il existe de nombreux outils propriétaires pour effectuer le suivi des bogues et des fonctionnalités demandées.
