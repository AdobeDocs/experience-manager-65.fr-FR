---
title: Outils de test et de suivi
seo-title: Outils de test et de suivi
description: AEM propose une structure pour tester l’interface utilisateur des composants, ainsi qu’un mécanisme destiné au test et au débogage des composants.
seo-description: AEM propose une structure pour tester l’interface utilisateur des composants, ainsi qu’un mécanisme destiné au test et au débogage des composants.
uuid: 12abedb5-4ee7-4389-9340-e628adbbc053
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 3cf0fd8d-7fc8-468a-bb1e-1debb68a82a5
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 94%

---


# Outils de test et de suivi{#testing-and-tracking-tools}

## Tests {#testing}

AEM fournit les éléments suivants :

* [Une structure pour tester l’interface utilisateur des composants](/help/sites-developing/hobbes.md).
* [Un mécanisme pour tester et déboguer les composants](/help/sites-developing/developer-mode.md).

Les deux outils suivants sont des outils de test Open Source :

**Selenium**

Selenium est utilisé pour le test de fonctions dans un navigateur avec un seul utilisateur par activité. Il enregistre les étapes de test (clics) sous la forme de tableaux HTML ou de classes Java.

Pour plus d’informations, voir [https://www.seleniumhq.org/](https://www.seleniumhq.org/).

**JMeter**

JMeter est utilisé pour effectuer le suivi des demandes. Il peut être utilisé dans le cadre de tests fonctionnels, de tests des performances et de tests de contrainte.

Pour plus d’informations, voir [https://jakarta.apache.org/jmeter/](https://jakarta.apache.org/jmeter).

Il existe également une foule d’outils propriétaires conçus pour automatiser les tests et gérer les plans de test.

### Suivi {#tracking}

Les outils suivants sont faciles à obtenir. Il subsiste toutefois un problème fondamental dans tous les cas, à savoir : la disponibilité des données pour l’ensemble des membres de l’équipe du projet, tant le partenaire que le client.

**Bugzilla**

Système de suivi de bogues qui peut être configuré selon vos besoins.

**Tableurs**

Bien qu’il ne s’agisse pas à proprement parler d’un outil de suivi des bogues, le tableur est souvent utilisé *à mauvais escient*, dans la mesure où il est facile à prendre en main et où la plupart des utilisateurs connaissent ses fonctionnalités.

Veuillez tenir compte des points suivants si vous utilisez un tableur à des fins de suivi :

* Les feuilles de calcul doivent rester simples.
* Le nombre de feuilles de calcul doit être limité au minimum.
* Les feuilles de calcul doivent être mises à jour régulièrement.
* Une seule copie principale doit être conservée et son emplacement doit être connu de tous.
* Elles doivent être accessibles à tous les membres du projet.
* Si la sécurité est importante (ce qui est généralement le cas au sein des grandes entreprises) et qu’un accès commun n’est pas possible, les copies peuvent être distribuées pour autant que tout le monde a conscience qu’il s’agit de copies et qu’elles ne peuvent pas être mises à jour.

Pour rappel, il existe de nombreux outils propriétaires pour effectuer le suivi des bogues et des fonctionnalités demandées.
