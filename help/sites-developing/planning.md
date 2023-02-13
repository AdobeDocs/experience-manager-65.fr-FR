---
title: Planification
seo-title: Planning
description: Éléments à connaître pour planifier votre test
seo-description: What you need to know to plan for your test
uuid: 29b1127a-da85-46ed-98e7-1c983eb40cfe
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 12268c43-93f9-42c1-8dd7-f17f9ae2219b
exl-id: ed662279-0679-4ba3-b744-6649fb8dda17
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: ht
source-wordcount: '974'
ht-degree: 100%

---

# Planification{#planning}

Ce document décrit les éléments que vous devez connaître pour planifier votre test. Vous devez, en outre, répondre à ces questions avant d’effectuer vos tests :

* [Quels environnements de test sont nécessaires ?](/help/sites-developing/test-environments.md)
* [Définition de cas de test](/help/sites-developing/test-cases.md)
* [Les tests - Quand et avec qui ?](/help/sites-developing/when-who.md)

## Avant de commencer {#before-you-start}

Avant de procéder à l’analyse proprement dite et de passer à la définition des tests, consultez les informations suivantes :

**Architecte AEM** - Consultez la section Concepts de base pour vous familiariser avec l’architecture et les principes de bases d’AEM.

**Documentation** - Pour de plus amples informations, consultez n’importe quelle section de la documentation ou les articles de procédure.

**Principes de base du test** - Vous devez connaître les principes de base relatifs aux test de logiciels et à l’assurance qualité. Vous devez idéalement avoir de l’expérience en matière de test de projets.

Il existe de nombreux sites web, livres et cours traitant de ces principes. C’est pourquoi nous ne les traiterons pas en détail dans ce document.

**Idées préconçues à éviter** - On part généralement du principe que votre site web devra satisfaire, chaque jour, des millions de requêtes. Dans certains cas, cela se vérifie, mais on ne peut rien affirmer.

Bien qu’il soit impossible de faire des prévisions avec une précision absolue, vous pouvez obtenir de bonnes indications en observant votre site actuel et le trafic échangé. Vous pourrez alors faire des estimations sur la base du facteur d’augmentation attendue/escomptée du trafic.

**La qualité comme maître-mot** - Il est essentiel que la personne qui réalise les tests fasse preuve d’une totale neutralité et se contente de rapporter les résultats des tests effectués.

Il est de la responsabilité du chef de projet de déterminer les mesures à prendre en fonction des résultats et d’agir en conséquence.

**L’engagement au cœur** - Bien qu’il appartienne au chef de projet de s’assurer que toutes les parties s’impliquent pleinement dans toutes les réunions (de statut, ateliers, etc.), vous devez tâcher de vous impliquer le plus tôt possible dans le cycle de projet, y compris pour les processus de collecte d’informations et d’analyse des exigences.

**Impliquer le client** Dans le même esprit, tâchez d’impliquer le client (dans la mesure du possible) lors de la définition de votre protocole et de vos scénarios de test.

## Types de tests {#types-of-tests}

Plusieurs catégories de tests standard sont adaptées au test d’un projet AEM. Vous devez bien connaître ces différentes catégories pour déterminer celle à utiliser :

>[!NOTE]
>
>Elles sont répertoriées dans l’ordre chronologique d’application.

**Tests unitaires** - Tests (généralement) effectués par l’équipe de développement pour s’assurer que les différents éléments se comportent correctement, bien que de manière isolée.

**Tests d’intégration** - Teste les modules lorsqu’ils sont combinés. Ces tests sont effectués après les tests unitaires, mais avant les tests du système.

**Tests de détection de fumée** - Il s’agit de tests « quick-and-dirty » destinés à prouver que le logiciel est en cours d’exécution et qu’une fonctionnalité de haut niveau est disponible. Ces tests ne portent pas sur les détails.

**Tests fonctionnels** - Utilisés pour tester les fonctionnalités du logiciel. Une série de tests sera élaborée pour couvrir tous les détails fonctionnels, avec les entrées attendues et inattendues et/ou incorrectes.

Les tests de boîte noire sont des tests fonctionnels portant sur une unité, un composant ou un module complet. Ils sont effectués sans aucune connaissance du fonctionnement interne de l’élément en question.

**Tests du système** - Ces tests sont réalisés sur l’ensemble du système une fois qu’il a été totalement intégré et installé sur une plateforme appropriée.

Ils testent les fonctionnalités sur la base d’une boîte noire.

**Tests de performance** - Les tests de performance sont essentiels dans le cadre du test d’AEM.

Ils sont utilisés pour illustrer les performances dans différentes conditions :

* Normales

   Conditions de fonctionnement du site pendant 90 % du temps (environ). Par exemple, lorsque seulement une petite partie des auteurs utilisent le système.

* Crête

   Conditions qui prévaudront pendant une période (proportionnellement) courte en raison de circonstances particulières ; par exemple, si tous les auteurs utilisent le système simultanément ou si du nouveau contenu est publié et qu’un nombre accru de visiteurs consulte votre site.

* Extrême

   Ces tests peuvent être utilisés pour émuler les prévisions de performance lors de la publication d’un nouveau contenu extrêmement intéressant sur votre site web. Un pic extrême peut alors être observé, bien que cela ne soit pas nécessairement toujours totalement prévisible.

   On peut se trouver dans ce type de situation lors de la mise en vente de billets pour des événements spéciaux ou lors de la publication initiale d’un site web très attendu.

Les résultats sont ensuite utilisés pour optimiser l’application.

**Tests de contrainte** - Les tests de contrainte sont effectués pour vérifier le comportement d’un composant ou d’une application dans des conditions extrêmes. On a notamment recours à ces tests pour illustrer la manière dont le comportement se détériorera lors de l’échec de l’élément, ainsi que la façon dont cela se produira.

**Tests de régression** - Les tests de régression sont utilisés pour confirmer qu’une fonctionnalité déjà éprouvée dans une version précédente du logiciel fonctionne toujours correctement.

L’automatisation est particulièrement adaptée dans ce cas (dans la mesure du possible) afin de s’assurer qu’ils peuvent être reproduits rapidement et de manière cohérente.

**Tests d’acceptation** - Les tests d’acceptation constituent une catégorie spéciale, dans la mesure où ils sont utilisés pour indiquer que le client a accepté le projet.

Ces tests d’acceptation peuvent être constitués de tests issus des différentes catégories mentionnées ci-dessus et être sélectionnés dans le but de s’assurer que le projet répond aux exigences du client.

Pour plus d’informations, voir [Acceptation et approbation](/help/sites-developing/acceptance-signoff.md).

## Prise en main {#getting-started}

Avant de commencer votre plan et vos scénarios de test détaillés, vous pouvez :

**Définir les objectifs** - Définir vos objectifs de haut niveau pour servir de référence aux processus d’optimisation à mesure que les tests sont réalisés. Vous pouvez effectuer les opérations suivantes :

* Tester les fonctionnalités conformément à la spécification détaillée des exigences.
* Tester les performances conformément aux [mesures cibles](/help/managing/best-practices-further-reference.md#key-performance-indicators-and-target-metrics).

Entre autres.

**Collecter des statistiques de trafic à partir du site web existant** - Ces informations peuvent être extraites des fichiers journaux - Consultez la section Surveillance des performances pour plus d’informations.

Ces valeurs vous donnent une indication quant au trafic actuel (volume et étendue) sur le site web existant et peuvent être utilisées comme référence pour le nouveau site web.

**Collecter des statistiques de trafic à partir de sites web externes** - Si possible, vous pouvez essayer de collecter des statistiques de trafic auprès d’autres sites web à des fins de comparaison. Notez toutefois que ces chiffres ne sont pas toujours publiés.

**Confirmer les mesures cibles** - Les mesures sont utilisées pour définir des mesures quantitatives pour la qualité du site web, étant donné qu’elles représentent les objectifs de performance à atteindre.

Elles doivent être définies au début du projet, avec le client. Pour plus d’informations, voir [Mesures cibles](/help/sites-developing/planning.md).
