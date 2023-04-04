---
title: Bonnes pratiques pour les tests de performance
description: Découvrez les stratégies globales et les méthodologies utilisées pour les tests de performance, ainsi que certains des outils disponibles pour faciliter le processus.
uuid: ab8720d6-b864-4d00-9e07-2e1699cfe7db
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 669018a0-f6ef-42b2-9c6f-83d7dd5a7095
exl-id: fcac75e1-15c1-4a37-8d43-93c95267b903
source-git-commit: 9defa6d1843007e9375d839f72f6993c691a37c0
workflow-type: tm+mt
source-wordcount: '1831'
ht-degree: 19%

---

# Bonnes pratiques pour les tests de performance{#best-practices-for-performance-testing}

## Présentation {#introduction}

Les tests de performance constituent une partie importante de tout déploiement d’AEM. Selon les besoins du client, les tests de performance peuvent être effectués sur les instances de publication, d’auteur ou les deux.

Cette documentation décrit les stratégies et les méthodologies globales d’exécution des tests de performance ainsi que certains des outils mis à disposition par Adobe pour faciliter le processus. Enfin, lisez une analyse des outils disponibles dans AEM 6 pour faciliter l’optimisation des performances, tant du point de vue de l’analyse du code que de la configuration du système.

### Simulation de la réalité {#simulating-reality}

Lors des tests de performance, veillez à imiter un environnement de production aussi près que possible. Bien qu’une telle tâche puisse souvent être difficile, il est impératif d’assurer l’exactitude de ces tests. Lorsque vous concevez des tests de performance, il est important de prendre en compte les points suivants :

* Contenu de type production

De nombreuses mesures de performances dans AEM, telles que le temps de réponse des requêtes, peuvent être affectées par la taille du contenu sur le système. Il est important de s’assurer que l’environnement de test dispose d’une copie aussi proche que possible des données de production.

* Code de production

La version AEM et les correctifs déployés en production doivent être identiques dans l’environnement de test. Il est également important de tester la version du code déployé en production.

* Configuration matérielle et réseau de type production

Les tests n’ont aucun sens sans environnement qui ressemble le plus possible à celui de la production. Idéalement, les spécifications matérielles, les interfaces réseau, les équilibreurs de charge et le réseau de diffusion de contenu doivent être identiques à la production dans l’environnement de test.

* Charge de production

De nombreux problèmes de performances ne sont pas visibles tant que le système n’est pas soumis à une charge importante. De bons tests de performance doivent simuler la charge que les systèmes de production subissent à leur maximum.

### Définition des objectifs {#setting-goals}

Avant de commencer les tests de performance, il est nécessaire de définir des exigences non fonctionnelles pour spécifier les temps de chargement et de réponse. Si vous effectuez une migration à partir d’un système existant, assurez-vous que les temps de réponse sont similaires aux valeurs de production actuelles. Pour la charge, il est préférable d’utiliser la charge de pointe actuelle et de la doubler. Cela permet de s’assurer que le site web peut continuer à fonctionner correctement au fur et à mesure de son développement.

### Outils {#tools}

De nombreux outils de test de performance sont proposés sur le marché. Lors de l’exécution d’un outil de génération de charge, il est important de s’assurer que les ordinateurs qui effectuent les tests disposent d’une bande passante réseau suffisante. Dans le cas contraire, une fois que la machine test a atteint les limites de sa connexion, aucune charge supplémentaire n’est générée sur l’environnement en cours de test.

#### Outils de test {#testing-tools}

* Adobe **Tough Day** peut être utilisé pour générer la charge sur les instances AEM et collecter des données de performances. L’équipe AEM d’ingénierie d’Adobe utilise en fait l’outil pour effectuer des tests de charge du produit AEM lui-même. Les scripts exécutés dans Tough Day sont configurés via des fichiers de propriétés et des fichiers XML JMX. Pour plus d’informations, voir [Documentation de Tough Day](/help/sites-developing/tough-day.md).

* AEM fournit des outils prêts à l’emploi pour afficher rapidement les requêtes, les requêtes et les messages d’erreur problématiques. Pour plus d’informations, voir [Outils de diagnostic](/help/sites-administering/operations-dashboard.md#diagnosis-tools) de la documentation du tableau de bord des opérations.
* Apache fournit un produit appelé **JMeter** qui peut être utilisé pour les tests de performance et de chargement, ainsi que pour le comportement fonctionnel. Il s’agit d’un logiciel open source et gratuit, mais il dispose d’un plus petit ensemble de fonctionnalités que les produits d’entreprise et d’une courbe d’apprentissage plus rapide. JMeter est disponible sur le site web d’Apache à l’adresse [https://jmeter.apache.org/](https://jmeter.apache.org/)

* **Load Runner** est un produit de test de charge de qualité professionnelle. Une version d’évaluation gratuite est disponible. Vous trouverez plus d’informations à l’adresse [https://www.microfocus.com/en-us/portfolio/performance-engineering/overview](https://www.microfocus.com/en-us/portfolio/performance-engineering/overview)

* Outils de test de chargement de site web, tels que [Neustar](https://neustarsecurityservices.com/web-performance-management) peut également être utilisé.
* Lors du test de sites web mobiles ou réactifs, un ensemble distinct d’outils doit être utilisé. Ils fonctionnent en limitant la bande passante du réseau, en simulant des connexions mobiles plus lentes comme 3G ou EDGE. Parmi les outils les plus utilisés, on trouve :

   * **[Network Link Conditioner](https://nshipster.com/network-link-conditioner/)** : fournit une interface utilisateur facile à utiliser et fonctionne à un niveau relativement bas sur la pile de mise en réseau. Prend en charge OS X et iOS.
   * [**Charles**](https://www.charlesproxy.com/) : application proxy de débogage Web qui, outre plusieurs autres utilisations, offre une fonction de limitation du réseau. Les versions sont fournies pour Windows, OS X et Linux®.

#### Outils d’optimisation {#optimization-tools}

**Surveillance**

Le [Surveillance des performances](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance) la documentation est une bonne ressource pour les outils et les méthodes qui peuvent être utilisés pour diagnostiquer les problèmes et identifier les zones à optimiser.

**Mode Développeur de l’IU tactile**

L’une des nouvelles fonctionnalités de l’interface utilisateur tactile d’AEM 6 est le mode Développeur. De la même manière que les auteurs peuvent basculer entre les modes de modification et d’aperçu, les développeurs peuvent passer en mode développeur dans l’interface utilisateur de création. Cela vous permet d’afficher le temps de rendu de chacun des composants sur la page et d’afficher les traces de pile des erreurs. Pour plus d’informations sur le mode Développeur, voir cette section [Présentation de CQ Gems](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2014/aem-developer-mode.html?lang=en).

**Utilisation de rlog.jar pour lire les journaux de requêtes**

Pour une analyse plus complète des journaux de demandes d’un système AEM, vous pouvez utiliser `rlog.jar` pour rechercher et trier les fichiers `request.log` générés par AEM. Ce fichier jar est inclus avec une installation AEM dans le dossier `/crx-quickstart/opt/helpers`. Pour plus d’informations sur l’outil de journalisation et le journal des requêtes en général, reportez-vous à la section [Surveillance et maintenance](/help/sites-deploying/monitoring-and-maintaining.md) documentation.

**Outil Expliquer la requête**

Le [Explication de l’outil de requête](/help/sites-administering/operations-dashboard.md#explain-query) dans ACS AEM les outils peuvent être utilisés pour afficher les index utilisés lors de l’exécution d’une requête. Cet outil est utile pour optimiser les requêtes à exécution lente.

**Outils PageSpeed** 

Les outils PageSpeed de Google offrent une analyse du site en vue de respecter les bonnes pratiques en matière de performances de page et un module externe qui peut être installé avec Dispatcher sur une instance Apache pour des optimisations supplémentaires.
Voir [Site Web des outils PageSpeed](https://developers.google.com/speed).

## Environnement de création {#author-environment}

### Exécution de tests {#performing-tests}

Pour effectuer des tests de performance dans l’environnement de création, il est nécessaire de simuler l’expérience des auteurs de production. En d’autres termes, les installations de création doivent contenir tous les composants, les lots OSGi, la personnalisation de l’interface utilisateur, les index personnalisés et tout autre ajout mis en place pour les instances d’auteur de production.

De nombreuses structures d’automatisation disponibles sont conçues pour les tests de performance et de charge. Des scripts personnalisés peuvent être enregistrés dans ces outils, puis exécutés pour simuler un nombre maximal d’auteurs effectuant simultanément des activités similaires de création et d’activation de contenu. Il est recommandé d’utiliser l’outil Tough Day pour simuler des activités telles que le chargement de milliers de ressources ou l’activation d’un grand nombre de pages.

Pour les types d’environnements qui nécessitent un chargement de ressources important ou la création de pages, il est impératif d’utiliser des outils tels que Tough Day. Cela permet de s’assurer que l’environnement fonctionne efficacement sous une charge maximale. [WebDAV](/help/sites-administering/webdav-access.md) est un outil qui ne nécessite aucun script et qui peut également servir à charger de grandes quantités de ressources.

#### Étapes spécifiques à MongoDB {#mongodb-specific-steps}

Sur les systèmes avec des serveurs principaux MongoDB, AEM fournit plusieurs [JMX](/help/sites-administering/jmx-console.md) MBeans qui doivent être surveillés lors des tests de charge ou de performance :

* Le **Statistiques de cache consolidées** MBean. Il est accessible directement depuis :

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D6%2Cname%3D%22Consolidated+Cache+statistics%22%2Ctype%3D%22ConsolidatedCacheStats%22`

Pour le cache nommé **Document-Diff**, le taux d’accès doit être supérieur à `.90`. Si le taux d’accès est inférieur à 90 %, il est probable que vous deviez modifier votre `DocumentNodeStoreService` configuration. La prise en charge du produit Adobe peut recommander des paramètres optimaux pour votre environnement.

* MBean **Oak Repository Statistics**. Il est accessible directement depuis :

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D16%2Cname%3D%22Oak+Repository+Statistics%22%2Ctype%3D%22RepositoryStats%22`

Le **ObservationQueueMaxLength** La section indique le nombre d’événements dans la file d’attente d’observation d’Oak au cours des dernières heures, minutes, secondes et semaines. Recherchez le plus grand nombre d’événements dans la section &quot;Par heure&quot;. Comparez ce nombre à la valeur `oak.observation.queue-length` . Si le nombre le plus élevé affiché pour la file d’attente d’observation dépasse la valeur du paramètre `queue-length` :

1. Créez un fichier nommé `com.adobe.granite.repository.impl.SlingRepositoryManager.cfg` contenant le paramètre `oak.observation.queue‐length=50000`.
1. Placez-le sous le dossier /crx-­‐quickstart/install.

>[!NOTE]
>Voir [AEM 6.x | Conseils sur l’optimisation des performances](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-performance.html?lang=en)

Le paramètre par défaut est de 10 000, mais la plupart des déploiements doivent l’augmenter à 20 000 ou 50 000.

## Environnement de publication {#publish-environment}

### Exécution de tests {#performing-tests-1}

La partie la plus importante d’un déploiement qui doit être soumise à des tests de chargement est l’environnement de publication ou de dispatcher de l’utilisateur final.

Des outils de test automatisés tiers peuvent être utilisés pour tester les performances du site web. Ces outils vous permettent d’enregistrer les étapes que les utilisateurs parcourent sur le site et d’exécuter plusieurs de ces sessions en même temps pour simuler la charge typique d’un site web de production.

La plupart des sites web de production disposent d’optimisations telles que la mise en cache de Dispatcher et la mise en place d’un réseau de diffusion de contenu. Lors du test, assurez-vous que ces optimisations sont également disponibles pour l’environnement de test. Outre la surveillance des temps de réponse pour les utilisateurs finaux, surveillez les mesures système sur les serveurs de publication et les dispatchers pour vous assurer que le système n’est pas limité par les ressources matérielles.

Sur un système qui ne nécessite pas un niveau élevé de personnalisation, Dispatcher doit mettre en cache la plupart des requêtes. Par conséquent, la charge sur l’instance de publication doit rester relativement nulle. Si un niveau élevé de personnalisation est requis, il est recommandé d’utiliser des technologies telles que les iFrames ou d’AJAX de requêtes pour le contenu personnalisé afin de permettre une mise en cache maximale du Dispatcher.

Pour les tests de base, Apache Bench peut être utilisé pour mesurer les temps de réponse du serveur web et aider à créer la charge pour mesurer des éléments comme les fuites de mémoire. Voir l’exemple de la section [Documentation de supervision](/help/sites-deploying/monitoring-and-maintaining.md#apache-bench).

## Résolution des problèmes de performances {#troubleshooting-performance-issues}

Après l’exécution des tests de performance sur l’instance d’auteur, tous les problèmes doivent être étudiés, diagnostiqués et résolus. Vous pouvez utiliser plusieurs outils et techniques pour effectuer des analyses et résoudre des problèmes :

* Vous pouvez examiner la variable [Journal des performances des requêtes](/help/sites-administering/operations-dashboard.md#request-performance) dans le tableau de bord des opérations. Cet outil peut être utilisé pour identifier les demandes de page lente.
* Analysez les requêtes à exécution lente avec l’outil [Performances des requêtes](/help/sites-administering/operations-dashboard.md#query-performance).

* Recherchez des erreurs ou des avertissements dans le journal des erreurs. Pour plus d’informations, consultez la section [Journalisation](/help/sites-deploying/configure-logging.md).
* Surveillez les ressources matérielles du système telles que l’utilisation de la mémoire et du processeur, les E/S de disque ou les E/S réseau. Ces ressources sont souvent à l’origine de goulets d’étranglement au niveau des performances.
* Optimisez l’architecture des pages et la manière dont elles sont traitées afin de minimiser l’utilisation des paramètres d’URL pour permettre une mise en cache maximale possible.
* Suivez la [Optimisation des performances](/help/sites-deploying/configuring-performance.md) et [Conseils sur l’optimisation des performances](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-performance.html?lang=en) documentation.

* Si des problèmes surviennent lors de la modification de certaines pages ou composants sur les instances de création, utilisez le mode Développeur de l’interface utilisateur tactile pour inspecter la page en question. Vous obtenez ainsi une ventilation de chaque zone de contenu de la page et de son temps de chargement.
* Minimiser tous les JS et CSS sur le site. Voir [article de blog](https://blogs.adobe.com/foxes/enable-js-and-css-minification/).
* Éliminez les éléments CSS et JS incorporés des composants. Ils doivent être inclus et minimisés avec les bibliothèques côté client afin de minimiser le nombre de demandes requises pour effectuer le rendu de la page.
* Pour examiner les requêtes du serveur et déterminer celles qui prennent le plus de temps, utilisez les outils de navigateur tels que l’onglet Réseau de Chrome.

Une fois les zones problématiques identifiées, le code de l’application peut être inspecté pour optimiser les performances. Toutes les fonctionnalités AEM prêtes à l’emploi qui ne fonctionnent pas correctement peuvent être traitées par l’assistance d’Adobe.
