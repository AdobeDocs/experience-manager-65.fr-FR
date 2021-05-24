---
title: Planification
seo-title: Planification
description: Éléments à connaître pour planifier votre test
seo-description: Éléments à connaître pour planifier votre test
uuid: 29b1127a-da85-46ed-98e7-1c983eb40cfe
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 12268c43-93f9-42c1-8dd7-f17f9ae2219b
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '985'
ht-degree: 59%

---


# Planification{#planning}

Ce document décrit les éléments que vous devez connaître pour planifier votre test. Vous devez, en outre, répondre à ces questions avant d’effectuer vos tests :

* [Quels environnements de test sont nécessaires ?](/help/sites-developing/test-environments.md)
* [Définition de cas de test](/help/sites-developing/test-cases.md)
* [Test - quand et avec qui ?](/help/sites-developing/when-who.md)

## Avant de commencer {#before-you-start}

Avant de procéder à l’analyse proprement dite et de passer à la définition des tests, consultez les informations suivantes :

**Architecture d’AEM**  : consultez les Concepts de base pour vous familiariser avec l’architecture et les principes de base d’AEM.

**Documentation**  - Pour plus d’informations, reportez-vous à l’une des sections de la documentation ou aux articles Comment .

**Principes de base des tests**  : vous devez connaître les principes de base des tests logiciels et de l’assurance qualité. Vous devez idéalement avoir de l’expérience en matière de test de projets.

Il existe de nombreux sites web, livres et cours traitant de ces principes. C’est pourquoi nous ne les traiterons pas en détail dans ce document.

**Hypothèses à éviter**  : la plus grande hypothèse (faite régulièrement) est que votre site web devra traiter des millions de demandes chaque jour. Dans certains cas, cela se vérifie, mais on ne peut rien affirmer.

Bien qu’il soit impossible de faire des prévisions avec une précision absolue, vous pouvez obtenir de bonnes indications en observant votre site actuel et le trafic échangé. Vous pourrez alors faire des estimations sur la base du facteur d’augmentation attendue/escomptée du trafic.

**Engagement envers la qualité**  : il est d’une importance capitale que quiconque teste reste neutre et rapporte simplement les résultats des tests effectués.

Il est de la responsabilité du chef de projet de déterminer les mesures à prendre en fonction des résultats et d’agir en conséquence.

**Devenir impliqué**  - Bien qu’il soit de la responsabilité du chef de projet de s’assurer que toutes les parties sont pleinement impliquées dans n’importe quelle réunion (état, ateliers, etc.), vous devez également essayer de vous impliquer le plus tôt possible dans le cycle du projet, y compris dans les processus de collecte d’informations et d’analyse des exigences.

**Impliquer le client**  : sur un thème similaire, essayez d’impliquer le client (si possible) lors de la définition de vos cas de test et de votre plan.

## Types de tests {#types-of-tests}

Plusieurs catégories de tests standard sont adaptées au test d’un projet AEM. Vous devez bien connaître ces différentes catégories pour déterminer celle à utiliser :

>[!NOTE]
>
>Elles sont répertoriées dans l’ordre chronologique d’application.

**Tests d’unité**  : tests (généralement) effectués par l’équipe de développement pour s’assurer que les éléments individuels se comportent correctement, bien qu’isolément.

**Tests d’intégration**  : teste les modules lorsqu’ils sont combinés. Ces tests sont effectués après les tests unitaires, mais avant les tests du système.

**Tests de détection de fumée**  : il s’agit de tests rapides et sales utilisés pour prouver que le logiciel est en cours d’exécution et que des fonctionnalités de haut niveau sont disponibles. Ces tests ne portent pas sur les détails.

**Tests fonctionnels**  : ils sont utilisés pour tester les fonctionnalités du logiciel. Une série de tests sera élaborée pour couvrir tous les détails fonctionnels, avec les entrées attendues et inattendues et/ou incorrectes.

Les tests de boîte noire sont des tests fonctionnels portant sur une unité, un composant ou un module complet. Ils sont effectués sans aucune connaissance du fonctionnement interne de l’élément en question.

**Tests du système**  : ils testent l’ensemble du système une fois qu’il a été entièrement intégré et installé sur une plateforme appropriée.

Ils testent les fonctionnalités sur la base d’une boîte noire.

**Tests**  de performance : les tests de performance sont essentiels lors des AEM de test.

Ils sont utilisés pour illustrer les performances dans différentes conditions :

* Normal

   Conditions de fonctionnement du site pendant 90 % du temps (environ). Par exemple, lorsque seulement une petite partie des auteurs utilisent le système.

* Crête

   Conditions qui prévaudront pendant une période (proportionnellement) courte en raison de circonstances particulières ; par exemple, si tous les auteurs utilisent le système simultanément ou si du nouveau contenu est publié et qu’un nombre accru de visiteurs consulte votre site.

* Extrême

   Ces tests peuvent être utilisés pour émuler les prévisions de performance lors de la publication d’un nouveau contenu extrêmement intéressant sur votre site web. Un pic extrême peut alors être observé, bien que cela ne soit pas nécessairement toujours totalement prévisible.

   On peut se trouver dans ce type de situation lors de la mise en vente de billets pour des événements spéciaux ou lors de la publication initiale d’un site web très attendu.

Les résultats sont ensuite utilisés pour optimiser l’application.

**Tests de contrainte**  : des tests de contrainte sont effectués pour confirmer le comportement d’un composant ou d’une application dans des conditions extrêmes. On a notamment recours à ces tests pour illustrer la manière dont le comportement se détériorera lors de l’échec de l’élément, ainsi que la façon dont cela se produira.

**Tests de régression**  : les tests de régression permettent de confirmer que les fonctionnalités déjà connues dans une version précédente du logiciel fonctionnent toujours correctement.

Il s’agit de bons candidats pour l’automatisation (dans la mesure du possible) afin de s’assurer qu’ils peuvent être reproduits rapidement et de manière cohérente.

**Tests d’acceptation**  : les tests d’acceptation sont une catégorie spéciale, car ils sont utilisés pour indiquer que le client a accepté le projet.

Ces tests d’acceptation peuvent être constitués de tests issus des différentes catégories mentionnées ci-dessus et être sélectionnés dans le but de s’assurer que le projet répond aux exigences du client.

Pour plus d’informations, voir [Acceptation et approbation](/help/sites-developing/acceptance-signoff.md).

## Prise en main {#getting-started}

Avant de commencer votre plan et vos scénarios de test détaillés, vous pouvez :

**Définition des objectifs**  : définissez vos objectifs de haut niveau afin qu’ils servent de point de départ à l’optimisation au fil du test. Vous pouvez effectuer les opérations suivantes :

* Tester les fonctionnalités conformément à la spécification détaillée des exigences.
* Tester les performances conformément aux [mesures cibles](/help/managing/best-practices-further-reference.md#key-performance-indicators-and-target-metrics).

Entre autres.

**Collecter les statistiques de trafic à partir du site web**  existant - Ces informations peuvent être extraites des fichiers journaux - voir Surveillance des performances pour plus de détails.

Ces valeurs vous donnent une indication quant au trafic actuel (volume et étendue) sur le site web existant et peuvent être utilisées comme référence pour le nouveau site web.

**Collecter des statistiques de trafic à partir de sites Web**  externes : si possible, vous pouvez essayer de collecter des statistiques de trafic à partir d’autres sites Web à des fins de comparaison, mais ces chiffres ne sont pas toujours publiés.

**Confirmer les mesures**  cibles : les mesures servent à définir des mesures quantitatives de la qualité du site web, car elles représentent les objectifs de performances à atteindre.

Elles doivent être définies au début du projet, avec le client. Pour plus d’informations, voir [Mesures cibles](/help/sites-developing/planning.md).
