---
title: Consignes de dimensionnement du matériel
description: Ces consignes de dimensionnement procurent une estimation des ressources matérielles requises pour déployer un projet AEM.
exl-id: 5837ef4f-d4e0-49d7-a671-87d5547e0d98
solution: Experience Manager, Experience Manager 6.5
feature: Compliance
role: Developer,Leader
source-git-commit: 9eeba0532a9eddb668b8488218c0570ca2241439
workflow-type: tm+mt
source-wordcount: '1367'
ht-degree: 98%

---

# Consignes de dimensionnement du matériel{#hardware-sizing-guidelines}

Ces consignes de dimensionnement procurent une estimation des ressources matérielles requises pour déployer un projet AEM. Les estimations de dimensionnement dépendent de l’architecture du projet, de la complexité de la solution, du trafic estimé et des exigences du projet. Ce guide vous aide à déterminer les besoins matériels pour une solution spécifique ou à trouver une estimation supérieure et inférieure pour les exigences matérielles.

Les facteurs de base à prendre en compte sont (dans cet ordre) :

* **Vitesse réseau**

   * Latence réseau
   * Bande passante disponible

* **Vitesse de calcul**

   * Efficacité du cache
   * Trafic attendu
   * Complexité des modèles, applications et composants
   * Auteurs et autrices simultanés
   * Complexité de l’opération de création (édition de contenu simple, déploiement MSM, etc.)

* **Performances d’E/S**

   * Performances et efficacité du stockage du fichier ou de la base de données

* **Disque dur**

   * Au moins deux ou trois fois plus grand que la taille du référentiel

* **Mémoire**

   * Taille du site Web (nombre d’objets de contenu, de pages et d’utilisateurs et d’utilisatrices)
   * Nombre d’utilisateurs et d’utilisatrices/sessions actifs en même temps

## Architecture {#architecture}

Une configuration d’AEM standard consiste en un environnement de création et de publication. Ces environnements ont des exigences différentes en ce qui concerne la taille matérielle et la configuration système sous-jacentes. Vous trouverez des considérations sur ces deux environnements dans les sections [Environnement de création](/help/managing/hardware-sizing-guidelines.md#author-environment-specific-calculations) et [Environnement de publication](/help/managing/hardware-sizing-guidelines.md#publish-environment-specific-calculations).

Dans une configuration de projet type, vous disposez de plusieurs environnements sur lesquels définir les phases du projet :

* **Environnement de développement**
Pour le développement de nouvelles fonctions ou pour apporter des modifications importantes. Les bonnes pratiques recommandent de travailler dans un environnement de développement par développeur ou développeuse (généralement des installations locales sur leurs systèmes personnels).

* **Environnement de test de création**
Pour vérifier les modifications. Le nombre d’environnements de test varie selon les exigences du projet (qui nécessite, par exemple, un environnement distinct pour l’assurance qualité, le test de l’intégration ou le test d’acceptation utilisateur).

* **Environnement de test de publication**
Principalement pour tester les cas d’utilisation de collaboration sociale ou l’interaction entre l’instance de création et plusieurs instances de publication.

* **Environnement d’exploitation de création**
Pour que les auteurs modifient le contenu.

* **Environnement d’exploitation de publication**
Pour servir du contenu publié.

En outre, les environnements peuvent varier, allant d’un système à serveur unique exécutant AEM et un serveur d’applications, à un ensemble d’instances en cluster à plusieurs serveurs et processeurs à très grande échelle. Adobe recommande d’utiliser un ordinateur distinct pour chaque système de production et de ne pas exécuter d’autres applications sur ces ordinateurs.

## Considérations génériques sur le dimensionnement du matériel {#generic-hardware-sizing-considerations}

Les sections ci-dessous fournissent des conseils sur la manière de calculer les exigences matérielles, en tenant compte de diverses considérations. Pour les systèmes de grande taille, nous suggérons que vous réalisiez un simple jeu de tests d’évaluation des performances en interne sur une configuration de référence.

L’optimisation des performances est une tâche fondamentale qui doit être effectuée avant que toute évaluation des performances ne puisse être réalisée pour un projet spécifique. Veillez à suivre les conseils fournis dans la [documentation d’optimisation des performances](/help/sites-deploying/configuring-performance.md) avant de procéder aux tests d’évaluation des performances et d’utiliser leurs résultats pour les calculs de dimensionnement du matériel.

Les exigences de dimensionnement du matériel pour les cas d’utilisation avancés doivent être basées sur une évaluation détaillée des performances du projet. Les caractéristiques des cas d’utilisation avancés nécessitant des ressources matérielles exceptionnelles incluent les combinaisons suivantes :

* Un payload ou un débit de contenu élevé
* Une utilisation étendue de code personnalisé, de workflows personnalisés ou de bibliothèques logicielles tierces
* Une intégration à des systèmes externes non pris en charge

## Espace disque/disque dur {#disk-space-hard-drive}

L’espace disque requis dépend largement du volume et du type de votre application web. Les calculs doivent tenir compte des éléments suivants :

* la quantité et la taille des pages, des ressources et d’autres entités stockées dans le référentiel telles que les workflows, les profils, etc. ;
* la fréquence estimée des changements de contenu et, par conséquent, la création de versions de contenu ;
* le volume de rendus de ressources DAM qui seront générés ;
* la croissance globale du contenu au fil du temps.

L’espace disque est surveillé en permanence lors du nettoyage des révisions en ligne et hors ligne. Si l’espace disque disponible descend en dessous d’une valeur critique, le processus est annulé. La valeur critique est de 25 % de l’empreinte disque actuelle du référentiel et elle n’est pas configurable. Adobe recommande de dimensionner le disque de sorte qu’il soit au moins deux ou trois fois plus large que la taille du référentiel, y compris sa croissance estimée.

Envisagez une configuration de tableaux redondants de disques indépendants (RAID, par exemple, RAID10) pour la redondance des données.

### Virtualisation {#virtualization}

AEM fonctionne bien dans les environnements virtualisés, mais certains facteurs tels que le processeur ou les E/S ne peuvent pas être directement liés au matériel physique. Il est recommandé de choisir une vitesse d’E/S plus élevée (en général), car il s’agit généralement d’un facteur essentiel. L’évaluation comparative de votre environnement est nécessaire pour obtenir une compréhension précise des ressources requises.

### Parallélisation des instances AEM {#parallelization-of-aem-instances}

**Prévention de défaillance**

Un site web doté de la prévention de défaillance est déployé sur au moins deux systèmes distincts. Si un système tombe en panne, un autre système peut prendre la relève de façon à compenser la défaillance du système.

**Évolutivité des ressources système**

Pendant que tous les systèmes sont en cours d’exécution, les performances de calcul sont accrues. Ces performances supplémentaires ne sont pas nécessairement linéaires par rapport au nombre de nœuds de cluster, car les relations dépendent lourdement de l’environnement technique. Consultez la [documentation relative aux clusters](/help/sites-deploying/recommended-deploys.md) pour plus d’informations.

L’estimation du nombre de nœuds de cluster nécessaires repose sur les exigences de base et les cas d’utilisation particuliers du projet web spécifique :

* Du point de vue de la sécurité des défaillances, il est nécessaire de déterminer, pour tous les environnements, l’importance de l’échec et le temps de compensation de l’échec en fonction du temps nécessaire à la récupération d’un nœud de cluster.
* Pour ce qui est de l’évolutivité, le nombre d’opérations d’écriture est essentiellement le facteur le plus important. L’équilibrage de charge peut être établi pour les opérations qui accèdent au système uniquement afin de traiter les opérations de lecture. Consultez la section [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=fr) pour plus d’informations.

### Recommandations matérielles {#hardware-recommendations}

En règle générale, vous pouvez utiliser le même matériel pour votre environnement de création que celui recommandé pour votre environnement de publication. En règle générale, le trafic sur le site web est plus faible sur les systèmes de création, mais l’efficacité du cache l’est également. Cependant, le facteur fondamental ici est le nombre d’auteurs et autrices travaillant en parallèle, ainsi que le type d’actions effectuées sur le système. En général, la mise en cluster d’AEM (de l’environnement de création) est plus efficace pour dimensionner les opérations de lecture ; en d’autres termes, un cluster AEM se dimensionne correctement quand les auteurs et autrices effectuent des opérations de modification de base.

## Autres calculs spécifiques à un cas d’utilisation {#additional-use-case-specific-calculations}

Outre le calcul d’une application web par défaut, vous devrez peut-être prendre en compte des facteurs spécifiques pour les cas d’utilisation suivants. Les valeurs calculées doivent être ajoutées au calcul par défaut.

### Considérations spécifiques à Assets {#assets-specific-considerations}

Le traitement approfondi des ressources numériques nécessite des ressources matérielles optimisées, les facteurs les plus pertinents étant la taille de l’image et le débit maximal des images traitées.

Allouez au moins 16 Go de segment de mémoire et configurez le workflow [!UICONTROL Ressource de mise à jour de gestion des ressources numériques] pour qu’il utilise le [package Camera Raw](/help/assets/camera-raw.md) pour l’ingestion des images au format RAW.

>[!NOTE]
>
>Un débit d’images plus élevé signifie que les ressources informatiques doivent pouvoir suivre le rythme des E/S du système et inversement. Par exemple, si les workflows sont lancés par l’import d’images, le chargement de nombreuses images via WebDAV pourrait entraîner un retard dans les workflows.
>
>L’utilisation de disques distincts pour TarPM, le magasin de données et l’index de recherche peut aider à optimiser le comportement d’E/S du système (il est toutefois généralement préférable de conserver l’index de recherche localement).

>[!NOTE]
>
>Voir aussi le[ Guide de performance des ressources](/help/sites-deploying/assets-performance-sizing.md).

### Gestionnaire multi-sites {#multi-site-manager}

La consommation de ressources lors de l’utilisation d’AEM MSM sur un environnement de création dépend fortement des cas d’utilisation spécifiques. Les facteurs de base sont :

* le nombre de requêtes ;
* la périodicité des déploiements ;
* la taille de l’arborescence de contenu à déployer ;
* la fonctionnalité connectée des actions de déploiement.

Tester le cas d’utilisation prévu avec un extrait de contenu représentatif peut vous aider à améliorer votre compréhension de la consommation des ressources. Si vous extrapolez les résultats avec la fréquence prévue, vous pouvez évaluer les ressources supplémentaires requises pour AEM MSM.

Tenez également compte des auteurs et des autrices travaillant en parallèle. Ils percevront des effets secondaires sur les performances si les cas d’utilisation d’AEM MSM consomment plus de ressources que prévu.

### Considérations relatives au dimensionnement d’AEM Communities {#aem-communities-sizing-considerations}

Les sites AEM qui incluent des fonctions AEM Communities connaissent un haut niveau d’interaction des visiteurs du site (membres) dans l’environnement de publication.

Les considérations de dimensionnement d’un site communautaire dépendent de l’interaction anticipée des membres de la communauté et de la question de savoir si les performances optimales du contenu de la page sont d’une plus grande importance.

Le contenu créé par l’utilisateur ou l’utilisatrice (UGC) soumis par les membres est stocké séparément du contenu de la page. Alors que la plateforme AEM utilise un magasin de nœuds qui réplique le contenu du site de l’instance de création vers l’instance de publication, AEM Communities utilise un magasin simple et commun pour le contenu généré par les utilisateurs qui n’est jamais répliqué.

Pour le magasin du contenu généré par les utilisateurs, il est nécessaire de sélectionner un fournisseur de ressources de stockage qui influence le déploiement sélectionné.
Voir

* [Stockage de contenu de la communauté](/help/communities/working-with-srp.md)
* [Topologies recommandées pour Communities](/help/communities/topologies.md)
