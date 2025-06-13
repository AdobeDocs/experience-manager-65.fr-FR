---
title: Bonnes pratiques pour les tests de performance
description: Découvrez les stratégies globales et les méthodes utilisées pour les tests de performance, ainsi que certains des outils disponibles pour faciliter le processus.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: fcac75e1-15c1-4a37-8d43-93c95267b903
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 8f638eb384bdca59fb6f4f8990643e64f34622ce
workflow-type: tm+mt
source-wordcount: '1767'
ht-degree: 100%

---

# Bonnes pratiques pour les tests de performance{#best-practices-for-performance-testing}

## Présentation {#introduction}

Les tests de performance constituent une partie importante de tout déploiement d’AEM. Selon les besoins de la clientèle, les tests de performance peuvent être effectués sur les instances de publication, de création ou les deux.

Cette documentation présente les stratégies et méthodes globales d’exécution des tests de performance ainsi que certains des outils mis à disposition par Adobe pour faciliter le processus. Enfin, lisez une analyse des outils disponibles dans AEM 6 pour faciliter l’optimisation des performances, tant du point de vue de l’analyse du code que de la configuration du système.

### Simuler la réalité {#simulating-reality}

Lors des tests de performance, veillez à imiter un environnement de production du mieux possible. Bien qu’une telle tâche puisse souvent être difficile, il est impératif d’assurer l’exactitude de ces tests. Lorsque vous concevez des tests de performance, il est important de prendre en compte les points suivants :

* Contenu de type production

De nombreuses mesures de performances dans AEM, telles que le temps de réponse des requêtes, peuvent être affectées par la taille du contenu sur le système. Il est important de s’assurer que l’environnement de test dispose d’une copie aussi proche que possible des données de production.

* Code de production

La version d’AEM et les correctifs déployés en production doivent être identiques dans l’environnement de test. Il est également important de tester la version du code déployé en production.

* Configuration matérielle et réseau de type production

Les tests n’ont aucun sens sans environnement qui ressemble le plus possible à celui de la production. Idéalement, les spécifications matérielles, les interfaces réseau, les équilibreurs de charge et le réseau CDN doivent être identiques à la production dans l’environnement de test.

* Charge de production

De nombreux problèmes de performances ne sont pas visibles tant que le système n’est pas soumis à une charge importante. De bons tests de performance doivent simuler la charge que les systèmes de production subissent à leur maximum.

### Définir des objectifs {#setting-goals}

Avant de commencer les tests de performance, il est nécessaire de définir des exigences non fonctionnelles pour spécifier les temps de chargement et de réponse. Si vous migrez à partir d’un système existant, assurez-vous que le temps de réponse est similaire à vos valeurs de production actuelles. Pour la charge, il est préférable d’utiliser la charge de pointe actuelle et de la doubler. Cela permet de s’assurer que le site web peut continuer à fonctionner correctement au fur et à mesure de son développement.

### Outils {#tools}

De nombreux outils de test de performance sont proposés sur le marché. Lors de l’exécution d’un outil de génération de charge, il est important de s’assurer que les ordinateurs qui effectuent les tests disposent d’une bande passante réseau suffisante. Dans le cas contraire, une fois que la machine de test a atteint les limites de sa connexion, aucune charge supplémentaire n’est générée sur l’environnement en cours de test.

#### Outils de test {#testing-tools}

* L’outil **Tough Day** d’Adobe peut être utilisé pour générer une charge sur des instances d’AEM et collecter des données de performance. L’équipe d’ingénierie d’AEM d’Adobe utilise actuellement l’outil pour effectuer des tests de charge sur le produit AEM lui-même. Les scripts exécutés dans Tough Day sont configurés via des fichiers de propriétés et des fichiers XML JMX. Pour plus d’informations, voir la [documentation de Tough Day](/help/sites-developing/tough-day.md).

* AEM fournit des outils prêts à l’emploi pour identifier rapidement les requêtes, demandes et messages d’erreur problématiques. Pour plus d’informations, voir la section [Outils de diagnostic](/help/sites-administering/operations-dashboard.md#diagnosis-tools) de la documentation du tableau de bord des opérations.
* Apache fournit un produit appelé **JMeter** qui peut être utilisé pour les tests de performance et de chargement, ainsi que pour le comportement fonctionnel. Il s’agit d’un logiciel open source et gratuit, mais il dispose d’un plus petit ensemble de fonctionnalités que les produits d’entreprise et d’une courbe d’apprentissage plus difficile. JMeter est disponible sur le site web d’Apache à l’adresse [https://jmeter.apache.org/](https://jmeter.apache.org/).

* Des outils de test de chargement de site web tels que [Vercara](https://vercara.com/website-performance-management) peuvent également être utilisés.
* Lors du test de sites web mobiles ou réactifs, un ensemble distinct d’outils doit être utilisé. Ils fonctionnent en limitant la bande passante du réseau, en simulant des connexions mobiles plus lentes comme la 3G ou EDGE. Parmi les outils les plus utilisés, on peut citer :

   * **[Network Link Conditioner](https://nshipster.com/network-link-conditioner/)** : fournit une interface utilisateur facile à utiliser et fonctionne à un niveau relativement bas sur la pile de mise en réseau. Prend en charge OS X et iOS.
   * [**Charles**](https://www.charlesproxy.com/) : application proxy de débogage Web qui, outre plusieurs autres utilisations, offre une fonction de limitation du réseau. Les versions fournies prennent en charge Windows, OS X et Linux®.

#### Outils d’optimisation {#optimization-tools}

**Surveillance**

La documentation sur la [surveillance des performances](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance) est une bonne ressource pour les outils et les méthodes qui peuvent être utilisés pour diagnostiquer les problèmes et identifier les zones à optimiser.

**Mode Développeur de l’IU tactile**

L’une des nouvelles fonctionnalités de l’interface utilisateur tactile d’AEM 6 est le mode Développeur. De la même manière que les auteurs et autrices peuvent passer du mode de modification au mode d’aperçu, les développeurs et développeuses peuvent passer en mode Développeur dans l’interface utilisateur de création. Cela vous permet d’afficher le temps de rendu de chacun des composants sur la page et d’afficher les traces de pile des erreurs. Pour plus d’informations sur le mode Développeur, reportez-vous à cette [présentation Gems de CQ](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2014/aem-developer-mode.html?lang=fr).

**Utilisation de rlog.jar pour lire les journaux de requêtes**

Pour une analyse plus complète des journaux de demandes d’un système AEM, vous pouvez utiliser `rlog.jar` pour rechercher et trier les fichiers `request.log` générés par AEM. Ce fichier jar est inclus avec une installation AEM dans le dossier `/crx-quickstart/opt/helpers`. Pour plus d’informations sur l’outil rlog et le journal des requêtes en général, reportez-vous à la documentation sur la [surveillance et maintenance](/help/sites-deploying/monitoring-and-maintaining.md).

**Outil Expliquer la requête**

L’[outil Expliquer la requête](/help/sites-administering/operations-dashboard.md#explain-query) dans les Outils AEM d’ACS peut être utilisé pour afficher les index utilisés lors de l’exécution d’une requête. Cet outil est utile pour optimiser les requêtes à exécution lente.

**Outils PageSpeed**

Les outils PageSpeed de Google proposent une analyse de site pour garantir le respect des bonnes pratiques en matière de performances de page, ainsi qu’un plug-in pouvant être installé avec le Dispatcher sur une instance Apache pour des optimisations supplémentaires.
Reportez-vous au [site web des outils PageSpeed](https://developers.google.com/speed).

## Environnement de création {#author-environment}

### Exécution de tests {#performing-tests}

Pour réaliser des tests de performance dans l’environnement de création, il est nécessaire de simuler l’expérience des auteurs et autrices de production. En d’autres termes, les installations de création doivent contenir tous les composants, les lots OSGi, la personnalisation de l’interface utilisateur, les index personnalisés et tous les autres ajouts que vous avez mis en place pour les instances de création de production.

De nombreuses structures d’automatisation disponibles sont conçues pour les tests de performance et de charge. Des scripts personnalisés peuvent être enregistrés dans ces outils, puis exécutés pour simuler un nombre maximal d’auteurs effectuant simultanément des activités similaires de création et d’activation de contenu. Il est recommandé d’utiliser l’outil Tough Day pour simuler des activités telles que le chargement de milliers de ressources ou l’activation d’un grand nombre de pages.

Pour les types d’environnements qui nécessitent un chargement de ressources important ou la création d’un grand nombre de pages, il est impératif d’utiliser des outils tels que Tough Day. Cela permet de s’assurer que l’environnement fonctionne efficacement sous une charge maximale. [WebDAV](/help/sites-administering/webdav-access.md) est un outil qui ne nécessite aucun script et qui peut également servir à charger de grandes quantités de ressources.

#### Étapes spécifiques à MongoDB {#mongodb-specific-steps}

Sur les systèmes disposant de serveurs principaux MongoDB, AEM fournit plusieurs MBeans [JMX](/help/sites-administering/jmx-console.md) qui doivent être surveillés lors des tests de chargement ou de performances :

* Le MBean **Statistiques de cache consolidées**. Il est accessible directement depuis :

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D6%2Cname%3D%22Consolidated+Cache+statistics%22%2Ctype%3D%22ConsolidatedCacheStats%22`

Pour le cache nommé **Document-Diff**, le taux d’accès doit être supérieur à `.90`. Si le taux d’accès se retrouve en dessous de 90 %, il est probable que vous deviez modifier la configuration `DocumentNodeStoreService`. La prise en charge du produit Adobe peut recommander des paramètres optimaux pour votre environnement.

* MBean **Oak Repository Statistics**. Il est accessible directement depuis :

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D16%2Cname%3D%22Oak+Repository+Statistics%22%2Ctype%3D%22RepositoryStats%22`

La section **ObservationQueueMaxLength** indique le nombre d’événements dans la file d’attente d’observation d’Oak au cours des dernières heures, minutes, secondes et semaines. Recherchez le plus grand nombre d’événements dans la section « Par heure ». Comparez ce nombre au paramètre `oak.observation.queue-length`. Si le nombre le plus élevé affiché pour la file d’attente d’observation dépasse la valeur du paramètre `queue-length` :

1. Créez un fichier nommé `com.adobe.granite.repository.impl.SlingRepositoryManager.cfg` contenant le paramètre `oak.observation.queue‐length=50000`.
1. Placez-le sous le dossier /crx-­‐quickstart/install.

>[!NOTE]
>Voir [AEM 6.x | Conseils d’optimisation de la performance](https://experienceleague.adobe.com/docs/experience-manager-65/content/implementing/deploying/configuring/configuring-performance.html?lang=fr)

Le paramètre par défaut est 10 000, mais la plupart des déploiements doivent l’augmenter jusqu’à 20 000 ou 50 000.

## Environnement de publication {#publish-environment}

### Exécuter des tests {#performing-tests-1}

La partie la plus importante d’un déploiement qui doit être soumise à des tests de chargement est l’environnement de publication ou du Dispatcher de l’utilisateur final.

Il est possible d’utiliser des outils de test automatisés tiers pour tester les performances du site web. Ces outils vous permettent d’enregistrer les étapes que les utilisateurs et utilisatrices suivent sur le site et d’exécuter plusieurs de ces sessions en même temps pour simuler la charge type d’un site web de production.

La plupart des sites web de production disposent d’optimisations telles que la mise en cache du Dispatcher et la mise en place d’un réseau de diffusion de contenu. Lors du test, assurez-vous que ces optimisations sont également disponibles pour l’environnement de test. Outre la surveillance des temps de réponse pour les utilisateurs et utilisatrices finaux, surveillez les mesures du système sur les serveurs de publication et les dispatchers pour vous assurer que le système n’est pas limité par les ressources matérielles.

Sur un système qui ne nécessite pas un niveau élevé de personnalisation, le Dispatcher doit mettre en cache la plupart des requêtes. Par conséquent, la charge sur l’instance de publication doit rester relativement nulle. Si un niveau élevé de personnalisation est requis, il est recommandé d’utiliser des technologies telles que les requêtes iFrames ou AJAX pour le contenu personnalisé afin de permettre une mise en cache maximale du Dispatcher.

Pour les tests de base, il est possible d’utiliser Apache Bench pour mesurer les temps de réponse du serveur web et créer la charge pour mesurer des éléments comme les fuites de mémoire. Voir l’exemple dans la [documentation sur la surveillance](/help/sites-deploying/monitoring-and-maintaining.md#apache-bench).

## Résoudre les problèmes de performances {#troubleshooting-performance-issues}

Après l’exécution des tests de performance sur l’instance de création, tous les problèmes doivent être étudiés, diagnostiqués et résolus. Vous pouvez utiliser plusieurs outils et techniques pour effectuer des analyses et résoudre des problèmes :

* Vous pouvez examiner le [Journal des performances des requêtes](/help/sites-administering/operations-dashboard.md#request-performance) dans le tableau de bord des opérations. Il est possible d’utiliser cet outil pour identifier les requêtes de page lente.
* Analysez les requêtes à exécution lente avec l’outil [Performances des requêtes](/help/sites-administering/operations-dashboard.md#query-performance).

* Recherchez des erreurs ou des avertissements dans le journal des erreurs. Pour plus d’informations, consultez la section [Journalisation](/help/sites-deploying/configure-logging.md).
* Surveillez les ressources matérielles du système telles que l’utilisation de la mémoire et de l’UC, les E/S de disque ou les E/S réseau. Ces ressources sont souvent à l’origine de goulots d’étranglement au niveau des performances.
* Optimisez l’architecture des pages et la manière dont elles sont traitées afin de minimiser l’utilisation des paramètres d’URL pour permettre une mise en cache aussi complète que possible.
* Consultez la documentation sur l’[Optimisation des performances](/help/sites-deploying/configuring-performance.md) et les [Conseils sur l’optimisation des performances](https://experienceleague.adobe.com/docs/experience-manager-65/content/implementing/deploying/configuring/configuring-performance.html?lang=fr).

* Si des problèmes surviennent lors de la modification de certaines pages ou certains composants sur les instances de création, utilisez le mode Développeur de l’IU tactile pour inspecter la page en question. Vous obtenez ainsi une répartition de chaque zone de contenu de la page et leur temps de chargement.
* Minimisez tous les JS et CSS sur le site. Voir cet [article de blog](https://blogs.adobe.com/foxes/enable-js-and-css-minification/).
* Éliminez les CSS et JS intégrés des composants. Ils doivent être inclus et minimisés avec les bibliothèques côté client afin de minimiser le nombre de requêtes requises pour effectuer le rendu de la page.
* Pour examiner les requêtes du serveur et identifier celles qui prennent le plus de temps, utilisez les outils du navigateur tels que l’onglet Réseau de Chrome.

Une fois les zones problématiques identifiées, le code de l’application peut être inspecté pour optimiser les performances. Toutes les fonctionnalités AEM prêtes à l’emploi qui ne fonctionnent pas correctement peuvent être traitées par l’assistance d’Adobe.
