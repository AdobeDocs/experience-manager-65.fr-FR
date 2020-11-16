---
title: Bonnes pratiques pour les tests de performance
seo-title: Bonnes pratiques pour les tests de performance
description: Cet article présente les stratégies et méthodologies globales utilisées pour les tests de performance ainsi que certains des outils disponibles pour faciliter le processus.
seo-description: Cet article présente les stratégies et méthodologies globales utilisées pour les tests de performance ainsi que certains des outils disponibles pour faciliter le processus.
uuid: ab8720d6-b864-4d00-9e07-2e1699cfe7db
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 669018a0-f6ef-42b2-9c6f-83d7dd5a7095
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1925'
ht-degree: 92%

---


# Bonnes pratiques pour les tests de performance{#best-practices-for-performance-testing}

## Présentation {#introduction}

Les tests de performance constituent une partie importante de tout déploiement d’AEM. Selon les exigences du client, les tests de performance peuvent être effectués sur les instances de publication, les instances d’auteur, ou les deux.

Cette documentation présente les stratégies et méthodologies globales d’exécution des tests de performance ainsi que certains des outils mis à disposition par Adobe pour faciliter le processus. Enfin, nous analyserons certains des outils disponibles dans AEM 6 pour faciliter le réglage des performances, à la fois du point de vue de l’analyse du code et de la configuration du système.

### Simulation de la réalité {#simulating-reality}

Le plus important lorsque vous effectuez des tests de performance, c’est de vous assurer que vous simulez un environnement de production le plus fidèlement possible. Même si c’est souvent difficile de le faire, il est impératif de garantir la précision de ces tests. Lorsque vous concevez des tests de performance, il est important de prendre en compte les points suivants :

* Contenu semblable à la production

Dans AEM, de nombreuses mesures de performance, par exemple le temps de réponse d’une requête, peuvent être affectées par la taille du contenu du système. Il est important de s’assurer que l’environnement de test est le plus fidèle possible aux données de production.

* Code de production

La version d’AEM et les correctifs déployés en production doivent être les mêmes dans l’environnement de test. Il est également important de tester la version du code qui est déployé en production.

* Matériel et configuration réseau semblables à la production

Les tests n’auront aucun sens sans un environnement qui ressemble le plus possible à celui de la production. Idéalement, les spécifications matérielles, les interfaces réseau, les équilibreurs de charge et le réseau de diffusion de contenu doivent être identiques à la production dans l’environnement de test.

* Charge de production

De nombreux problèmes de performances ne sont pas visibles tant que le système n’est pas soumis à une charge importante. De bons tests de performance devraient simuler la charge à laquelle les systèmes de production seront soumis à leur maximum.

### Établissement des objectifs {#setting-goals}

Avant de commencer les tests de performance, il est nécessaire de définir des exigences non fonctionnelles afin de spécifier la charge et les temps de réponse. Si vous migrez à partir d’un système existant, assurez-vous que le temps de réponse est similaire à vos valeurs de production actuelles. Pour la charge, il est préférable d’utiliser la charge de pointe actuelle et de la doubler. Cela permet au site web de continuer à être performant à mesure qu’il se développe.

### Outils {#tools}

De nombreux outils de test de performance sont proposés sur le marché. Lors de l’exécution d’un outil de génération de charge, il est important de s’assurer que les ordinateurs qui effectuent les tests disposent d’une bande passante réseau suffisante. À défaut, une fois que la machine de test atteint les limites de sa connexion, aucune charge supplémentaire n’est générée sur l’environnement testé.

#### Outils de test {#testing-tools}

* L’outil **Tough Day** d’Adobe peut être utilisé pour générer une charge sur des instances AEM et collecter des données de performance. L’équipe AEM d’ingénieurs d’Adobe utilise en fait l’outil pour tester la charge du produit AEM lui-même. Les scripts exécutés dans Tough Day sont configurés via des fichiers de propriétés et des fichiers XML JMX. Pour plus d’informations, voir la [documentation Tough Day](/help/sites-developing/tough-day.md).

* AEM fournit des outils prêts à l’emploi pour identifier rapidement les requêtes, demandes et messages d’erreur problématiques. Pour plus d’informations, voir la section [Outils de diagnostic](/help/sites-administering/operations-dashboard.md#diagnosis-tools) de la documentation Tableau de bord des opérations.
* Apache propose un produit appelé **JMeter** pouvant être utilisé pour les tests de performance et de charge ainsi que pour le comportement fonctionnel. Il s’agit d’un logiciel open source et gratuit, mais dont le jeu de fonctionnalités est plus restreint que les produits destinées aux entreprises et dont la courbe d’apprentissage est plus rapide. JMeter can be found on Apache’s website at [https://jmeter.apache.org/](https://jmeter.apache.org/)

* **Load Runner** est un produit de test de charge de niveau entreprise. Une version d&#39;évaluation gratuite est disponible. Pour plus d&#39;informations, voir [https://www.microfocus.com/en-us/products/loadrunner-load-testing/overview](https://www.microfocus.com/en-us/products/loadrunner-load-testing/overview)

* Des outils de test de charge dans le cloud comme [Neustar](https://www.neustar.biz/services/web-performance/load-testing) peuvent également être utilisés.
* Pour tester des sites web mobiles ou réactifs, un jeu d’outils distinct doit être utilisé. Ils fonctionnent en limitant la bande passante réseau et en simulant des connexions mobiles plus lentes telles que 3G ou EDGE. Les outils les plus utilisés sont les suivants : 

   * **[Network Link Conditioner](https://nshipster.com/network-link-conditioner/)** : fournit une interface utilisateur facile à utiliser et fonctionne à un niveau relativement bas sur la pile de mise en réseau. Prend en charge OS X et iOS.[](https://nshipster.com/network-link-conditioner/)
   * [**Charles**](https://www.charlesproxy.com/) : application proxy de débogage web qui, outre plusieurs autres utilisations, offre une fonction de limitation du réseau. Prend en charge Windows, OS X et Linux. [](https://www.charlesproxy.com/)

#### Outils d’optimisation {#optimization-tools}

**Surveillance**

La documentation [Surveillance des performances](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance) est une excellente ressource sur les outils et les méthodes à employer pour diagnostiquer les problèmes et identifier les zones à optimiser.

**Mode Développeur de l’IU tactile**

L’une des nouvelles fonctionnalités de l’interface utilisateur tactile d’AEM 6 est le mode Développeur. Tout comme les auteurs peuvent basculer entre les modes de modification et de prévisualisation, les développeurs peuvent passer en mode Développeur dans l’interface utilisateur de création pour voir le temps de rendu de chacun des composants sur la page et identifier les traces de pile de toutes les erreurs. Pour plus d’informations sur le mode Développeur, voir cette [présentation de CQ Gems](https://docs.adobe.com/content/ddc/en/gems/aem-6-0-developer-mode.html).

**Utilisation de rlog.jar pour lire les journaux de demandes**

Pour une analyse plus complète des journaux de demandes d’un système AEM, vous pouvez utiliser `rlog.jar` pour rechercher et trier les fichiers `request.log` générés par AEM. This jar file is included with an AEM installation in the `/crx-quickstart/opt/helpers` folder. Pour plus d’informations sur l’outil rlog et le journal des demandes en général, voir la documentation [Surveillance et gestion](/help/sites-deploying/monitoring-and-maintaining.md).

**Outil Explain Query**

L’[outil Explain Query](/help/sites-administering/operations-dashboard.md#explain-query) des outils ACS AEM peut servir à afficher les index utilisés lors de l’exécution d’une requête. Cela peut être très utile lors de l’optimisation de requêtes à exécution lente.

**Outils PageSpeed&#x200B;&#x200B;** 

Les outils PageSpeed &#x200B;&#x200B;de Google proposent une analyse de site pour garantir le respect des bonnes pratiques en matière de performances de page, ainsi qu’un plug-in pouvant être installé avec le dispatcher sur une instance Apache pour des optimisations supplémentaires. Pour plus d’informations, voir le [site web des outils PageSpeed](https://developers.google.com/speed/pagespeed/).

## Environnement de création {#author-environment}

### Exécution de tests {#performing-tests}

Pour réaliser des tests de performance dans l’environnement de création, il est nécessaire de simuler l’expérience des auteurs de production. Cela signifie que les installations d’auteur doivent contenir tous les composants, les lots OSGi, la personnalisation de l’interface utilisateur, les index personnalisés et tous les autres ajouts que vous avez mis en place pour les instances d’auteur de production.

De nombreuses structures d’automatisation disponibles sont conçues pour les tests de performance et de charge. Des scripts personnalisés peuvent être enregistrés dans ces outils, puis exécutés pour simuler un nombre maximal d’auteurs effectuant simultanément des activités similaires de création et d’activation de contenu. Il est recommandé d’utiliser l’outil Tough Day pour simuler des activités telles que le téléchargement de milliers de ressources ou l’activation d’un grand nombre de pages.

Pour les types d’environnements dont les exigences de chargement de ressources ou de création de pages sont élevées, il est impératif d’utiliser des outils tels que Tough Day afin de garantir le fonctionnement efficace de l’environnement à une charge maximale. [WebDAV](/help/sites-administering/webdav-access.md) est un outil qui ne nécessite aucun script et qui peut également servir à charger de grandes quantités de ressources.

#### Étapes spécifiques à MongoDB {#mongodb-specific-steps}

Sur les systèmes dotés de serveurs principaux MongoDB, AEM fournit plusieurs MBeans [JMX](/help/sites-administering/jmx-console.md) qu’il faut surveiller lors des tests de charge ou de performance :

* MBean **Consolidated Cache Statistics**. Vous pouvez y accéder directement en vous rendant à :

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D6%2Cname%3D%22Consolidated+Cache+statistics%22%2Ctype%3D%22ConsolidatedCacheStats%22`

For the cache named **Document-Diff**, the hit rate should be over `.90`. Si le taux d’accès chute en dessous de 90 %, il est probable que vous deviez modifier la configuration `DocumentNodeStoreService`. L’assistance pour les produits Adobe peut vous recommander des paramètres optimaux pour votre environnement.

* Mbean **Oak Repository Statistics**. Vous pouvez y accéder directement en vous rendant à :

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D16%2Cname%3D%22Oak+Repository+Statistics%22%2Ctype%3D%22RepositoryStats%22`

La section **ObservationQueueMaxLength** affiche le nombre d’événements de la file d’attente d’observation d’Oak au cours des dernières heures, minutes, secondes et semaines. Identifiez le plus grand nombre d’événements dans la section « per hour ». Ce nombre doit être comparé au paramètre `oak.observation.queue-length` disponible dans le composant **SlingRepositoryManager** de la [console OSGi](/help/sites-deploying/web-console.md). Si le nombre le plus élevé affiché pour la file d’attente d’observation dépasse le paramètre `queue-length`, contactez l’assistance d’Adobe pour obtenir de l’aide sur l’augmentation de la valeur du paramètre. Le paramètre par défaut est 1 000, mais la plupart des déploiements doivent généralement l’augmenter jusqu’à 20 000 ou 50 000.

## Environnement de publication {#publish-environment}

### Exécution de tests {#performing-tests-1}

La partie la plus importante d’un déploiement qui doit être soumise à des tests de charge est l’environnement de publication ou de dispatcher de l’utilisateur final.

Il est possible d’utiliser des outils tiers de test automatisés pour tester les performances du site web. Ces outils vous permettent d’enregistrer le parcours de navigation que les utilisateurs suivent sur le site et d’exécuter plusieurs de ces sessions en même temps pour simuler la charge type d’un site web de production.

La plupart des sites web de production intègrent des optimisations telles que la mise en cache des dispatchers et la mise en place d’un réseau de diffusion de contenu. Lors du test, vous devez vous assurer que ces optimisations sont également disponibles pour l’environnement de test. Outre la surveillance des temps de réponse pour les utilisateurs finaux, vous devez également surveiller les mesures du système sur les serveurs de publication et les dispatchers pour vous assurer que le système n’est pas limité par des ressources matérielles.

Sur un système qui ne nécessite pas un niveau élevé de personnalisation, le dispatcher doit mettre en cache la plupart des demandes. Par conséquent, la charge sur l’instance de publication doit rester relativement stable. Si un niveau élevé de personnalisation est requis, il est recommandé d’utiliser des technologies telles que les iFrames ou les demandes AJAX pour le contenu personnalisé afin de permettre une mise en cache maximale par le dispatcher.

Dans le cas de tests simples, Apache Bench peut servir à mesurer les temps de réponse du serveur web et à créer une charge pour mesurer des événements comme des fuites de mémoire. Pour plus d’informations, voir l’exemple de la [documentation Surveillance](/help/sites-deploying/monitoring-and-maintaining.md#apache-bench).

## Résolution des problèmes liés aux performances {#troubleshooting-performance-issues}

Après avoir exécuté des tests de performance sur l’instance de création, tous les problèmes doivent être analysés, diagnostiqués et résolus. Vous pouvez avoir recours à plusieurs outils et techniques pour effectuer des analyses et résoudre des problèmes :

* Vous pouvez consulter le [journal Performances des demandes](/help/sites-administering/operations-dashboard.md#request-performance) dans le tableau de bord des opérations. Vous pouvez utiliser cet outil pour identifier les demandes de page lentes.
* Analysez les requêtes à exécution lente avec l’outil [Performances des requêtes](/help/sites-administering/operations-dashboard.md#query-performance).

* Recherchez, dans le journal des erreurs, les erreurs ou les avertissements. Pour plus d’informations, voir [Journalisation](/help/sites-deploying/configure-logging.md).
* Surveillez les ressources matérielles du système telles que l’utilisation de la mémoire et du processeur, les E/S de disque ou les E/S réseau. Ces ressources sont souvent la cause de la détérioration des performances.
* Optimisez l’architecture des pages et la façon dont elles sont adressées afin de minimiser l’utilisation des paramètres d’URL pour permettre un niveau maximal de mise en cache.
* Lisez la documentation [Optimisation des performances](/help/sites-deploying/configuring-performance.md) et [Conseils pour le réglage des performances](https://helpx.adobe.com/fr/experience-manager/kb/performance-tuning-tips.html).

* Si des problèmes surviennent lors de la modification de certaines pages ou composants sur des instances de création, utilisez le mode Développeur de l’UI tactile pour inspecter la page en question. Cela permet de décomposer chaque zone de contenu sur la page ainsi que son temps de chargement.
* Réduisez tous les JS et CSS sur le site. Pour plus d’informations sur la procédure à suivre, voir cet [article de blog](https://blogs.adobe.com/foxes/enable-js-and-css-minification/).
* Supprimez les CSS et JS incorporés des composants. Ils doivent être inclus et minimisés avec les bibliothèques côté client afin de minimiser le nombre de demandes requises pour le rendu de la page.
* Utilisez les outils du navigateur comme l’onglet Réseau de Chrome pour inspecter les demandes du serveur et déterminer les plus lentes.

Une fois les zones problématiques identifiées, le code de l’application peut être inspecté pour optimiser les performances. Toutes les fonctionnalités AEM prêtes à l’emploi qui ne fonctionnent pas correctement peuvent être traitées par l’assistance d’Adobe.
