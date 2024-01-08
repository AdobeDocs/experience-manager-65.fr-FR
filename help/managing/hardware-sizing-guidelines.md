---
title: Consignes de dimensionnement du matériel
description: Ces consignes de dimensionnement procurent une estimation des ressources matérielles requises pour déployer un projet AEM.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: managing
content-type: reference
docset: aem65
exl-id: 5837ef4f-d4e0-49d7-a671-87d5547e0d98
source-git-commit: 3bcdbfc17efe1f4c6069fd97fd6a16ec41d0579e
workflow-type: tm+mt
source-wordcount: '2846'
ht-degree: 38%

---

# Consignes de dimensionnement du matériel{#hardware-sizing-guidelines}

Ces consignes de dimensionnement procurent une estimation des ressources matérielles requises pour déployer un projet AEM. Les estimations de dimensionnement dépendent de l’architecture du projet, de la complexité de la solution, du trafic attendu et des exigences du projet. Ce guide vous aide à déterminer les besoins matériels pour une solution spécifique ou à trouver une estimation supérieure et inférieure pour les exigences matérielles.

Les facteurs de base à prendre en compte sont (dans cet ordre) :

* **Vitesse réseau**

   * Latence réseau
   * Bande passante disponible

* **Vitesse de calcul**

   * Efficacité du cache
   * Trafic attendu
   * Complexité des modèles, applications et composants
   * Auteurs simultanés
   * Complexité de l’opération de création (édition de contenu simple, déploiement MSM, etc.)

* **Performances des E/S**

   * Performances et efficacité du stockage du fichier ou de la base de données

* **Disque dur**

   * Au moins deux ou trois fois plus grand que la taille du référentiel

* **Mémoire**

   * Taille du site web (nombre d’objets de contenu, de pages et d’utilisateurs)
   * Nombre d’utilisateurs/sessions actifs en même temps

## Architecture {#architecture}

Une configuration d’AEM standard consiste en un environnement de création et de publication. Ces environnements ont des exigences différentes en ce qui concerne la taille matérielle et la configuration système sous-jacentes. Vous trouverez des considérations sur ces deux environnements dans les sections [Environnement de création](/help/managing/hardware-sizing-guidelines.md#author-environment-specific-calculations) et [Environnement de publication](/help/managing/hardware-sizing-guidelines.md#publish-environment-specific-calculations).

Dans une configuration de projet type, vous disposez de plusieurs environnements sur lesquels définir les phases du projet :

* **Environnement de développement**
Pour le développement de nouvelles fonctions ou pour apporter des modifications importantes. La bonne pratique consiste à utiliser un environnement de développement par développeur (installations locales sur leurs systèmes personnels).

* **Environnement de test de création**
Pour vérifier les modifications. Le nombre d’environnements de test varie selon les exigences du projet (qui nécessite, par exemple, un environnement distinct pour l’assurance qualité, le test de l’intégration ou le test d’acceptation utilisateur).

* **Environnement de test de publication**
Principalement pour tester les cas d’utilisation de collaboration sociale ou l’interaction entre l’instance de création et plusieurs instances de publication.

* **Environnement d’exploitation de création**
Pour que les auteurs modifient le contenu.

* **Environnement d’exploitation de publication**
Pour servir du contenu publié.

En outre, les environnements peuvent varier, allant d’un système à serveur unique exécutant AEM et un serveur d’applications, à un ensemble d’instances en grappe multi-serveur et multi-processeur à très grande échelle. Adobe recommande d’utiliser un ordinateur distinct pour chaque système de production et de ne pas exécuter d’autres applications sur ces ordinateurs.

## Considérations génériques sur le dimensionnement du matériel {#generic-hardware-sizing-considerations}

Les sections ci-dessous fournissent des conseils sur la manière de calculer les exigences matérielles, en tenant compte de diverses considérations. Pour les systèmes volumineux, Adobe vous suggère d’effectuer un simple ensemble de tests de référence internes sur une configuration de référence.

L’optimisation des performances est une tâche fondamentale qui doit être effectuée avant que toute évaluation des performances ne puisse être réalisée pour un projet spécifique. Veillez à appliquer les conseils fournis dans la section [Documentation sur l’optimisation des performances](/help/sites-deploying/configuring-performance.md) avant d’effectuer des tests d’évaluation des performances et d’utiliser leurs résultats pour tout calcul de dimensionnement matériel.

Les exigences de dimensionnement du matériel pour les cas d’utilisation avancés doivent être basées sur une évaluation détaillée des performances du projet. Les caractéristiques des cas d’utilisation avancés nécessitant des ressources matérielles exceptionnelles incluent les combinaisons suivantes :

* Un payload ou un débit de contenu élevé
* utilisation étendue de code personnalisé, de workflows personnalisés ou de bibliothèques logicielles tierces
* intégration à des systèmes externes non pris en charge

### Espace disque/disque dur {#disk-space-hard-drive}

L’espace disque requis dépend largement du volume et du type de votre application web. Les calculs doivent tenir compte des éléments suivants :

* la quantité et la taille des pages, des ressources et d’autres entités stockées dans le référentiel telles que les workflows, les profils, etc.
* la fréquence estimée des changements de contenu et, par conséquent, la création de versions de contenu ;
* le volume de rendus de ressources DAM qui seront générés ;
* la croissance globale du contenu au fil du temps ;

L’espace disque est surveillé en permanence pendant le nettoyage des révisions en ligne et hors ligne. Si l’espace disque disponible tombe en dessous d’une valeur critique, le processus est annulé. La valeur critique est de 25 % de l’empreinte disque actuelle du référentiel et elle n’est pas configurable. Adobe recommande de dimensionner le disque au moins deux ou trois fois plus grand que la taille du référentiel, y compris la croissance estimée.

Envisagez une configuration de tableaux redondants de disques indépendants (RAID, par exemple, RAID10) pour la redondance des données.

>[!NOTE]
>
>Le répertoire temporaire d’une instance de production doit contenir au moins 6 Go d’espace disponible.

#### Virtualisation {#virtualization}

AEM fonctionne bien dans les environnements virtualisés, mais certains facteurs tels que le processeur ou les E/S ne peuvent pas être directement liés au matériel physique. Il est recommandé de choisir une vitesse d’E/S plus élevée (en général), car il s’agit généralement d’un facteur essentiel. L’évaluation comparative de votre environnement est nécessaire pour obtenir une compréhension précise des ressources requises.

#### Mise en parallèle des instances AEM {#parallelization-of-aem-instances}

**Prévention de défaillance**

Un site web doté de la prévention de défaillance est déployé sur au moins deux systèmes distincts. Si un système tombe en panne, un autre système peut prendre le relais et ainsi compenser la défaillance du système.

**Évolutivité des ressources système**

Pendant que tous les systèmes sont en cours d’exécution, une performance de calcul accrue est disponible. Ces performances supplémentaires ne sont pas nécessairement linéaires avec le nombre de noeuds de grappe, car la relation dépend fortement de l’environnement technique. Voir [Documentation du cluster](/help/sites-deploying/recommended-deploys.md) pour plus d’informations.

L’estimation du nombre de noeuds de grappe nécessaires repose sur les exigences de base et les cas d’utilisation spécifiques du projet web spécifique :

* Du point de vue de la sécurité des défaillances, il est nécessaire de déterminer, pour tous les environnements, l’importance de l’échec et le temps de compensation de l’échec en fonction du temps nécessaire à la récupération d’un noeud de grappe.
* En ce qui concerne l’évolutivité, le nombre d’opérations d’écriture est fondamentalement le facteur le plus important. Consultez la section [Auteurs travaillant en parallèle](/help/managing/hardware-sizing-guidelines.md#authors-working-in-parallel) pour l’environnement de création et [Collaboration sociale](/help/managing/hardware-sizing-guidelines.md#socialcollaborationspecificconsiderations) pour l’environnement de publication. L’équilibrage de charge peut être établi pour les opérations qui accèdent au système uniquement afin de traiter les opérations de lecture. Consultez la section [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=fr) pour plus d’informations.

## Calculs spécifiques à l’environnement de création {#author-environment-specific-calculations}

À des fins d’évaluation des performances, Adobe a développé des tests d’évaluation des performances pour les instances d’auteur autonomes.

* **Test d’évaluation des performances 1**
Calcule le débit d’un profil de charge lorsque les utilisateurs exécutent un simple exercice de création de pages sur une charge de base de 300 pages existantes, toutes de nature similaire. Les étapes impliquées étaient la connexion au site, la création d’une page contenant un SWF et une image ou du texte, l’ajout d’un nuage de balises, puis l’activation de la page.

   * **Résultat**
Le débit maximal d’un simple exercice de création de pages comme décrit plus haut (considéré comme une transaction) est de 1 730 transactions/heure.

* **Test d’évaluation des performances 2**
Calcule le débit maximal lorsque le profil de charge comprend la création d’une page (10 %), la modification d’une page existante (80 %), ainsi que la création, puis la modification d’une page successivement (10 %). La complexité des pages reste la même que dans le profil du test de référence 1. La modification de base de la page s’effectue en ajoutant une image et en modifiant le contenu texte. Là encore, l’exercice a été effectué sur une charge de base de 300 pages de la même complexité que celle définie dans le test de référence 1.

   * **Résultat**
Le débit maximal d’un tel scénario mélangeant des opérations est de 3 252 transactions par heure.

>[!NOTE]
>
>Le débit ne fait pas la distinction entre les types de transaction dans un profil de charge. L’approche utilisée pour mesurer le débit permet de s’assurer qu’une proportion fixe de chaque type de transaction est incluse dans la charge de travail.

Les deux tests ci-dessus montrent clairement que le débit varie en fonction du type d&#39;opération. Utilisez les activités de votre environnement comme base pour dimensionner votre système. Vous obtiendrez un meilleur débit avec des actions moins intensives telles que la modification (qui est également plus courante).

### Mise en cache {#caching}

Dans l’environnement de création, l’efficacité de la mise en cache est en général bien plus faible, car les modifications du site web sont plus fréquentes et en raison du caractère hautement interactif et personnalisé du contenu. Dispatcher vous permet de mettre en cache AEM bibliothèques, JavaScript, fichiers CSS et images de mise en page. Cela permet d’accélérer certains aspects du processus de création. La configuration du serveur web pour définir également des en-têtes pour la mise en cache du navigateur sur ces ressources réduit le nombre de requêtes HTTP et améliore ainsi la réactivité du système telle qu’elle est vécue par les auteurs.

### Auteurs travaillant en parallèle {#authors-working-in-parallel}

Dans l’environnement de création, le nombre d’auteurs qui travaillent en parallèle et la charge que leurs interactions ajoutent au système constituent les principaux facteurs de limitation. Par conséquent, Adobe vous recommande de mettre votre système à l’échelle en fonction du débit partagé des données.

Pour de tels scénarios, Adobe exécute des tests de référence sur un cluster à deux noeuds sans partage d’instances d’auteur.

* **Test d’évaluation des performances 1a**
Avec un cluster sans partage actif-actif de deux instances de création, calcule le débit maximal avec un profil de charge où les utilisateurs exécutent un exercice simple de création de page sur une charge de base de 300 pages existantes, toutes de nature similaire.

   * **Résultat**
Le débit maximal d’un simple exercice de création de page comme plus haut (considéré comme une transaction) est de 2 016 transactions/heure. Il s’agit d’une augmentation d’environ 16 % par rapport à une instance de création autonome pour la même évaluation des performances.

* **Test d’évaluation des performances 2b**
Avec un cluster sans partage actif-actif de deux instances de création, calcule le débit maximal lorsque le profil de charge comprend la création d’une page (10 %), la modification de pages existantes (80 %), ainsi que la création et la modification d’une page successivement (10 %). La complexité de la page reste la même que dans le profil du test de référence 1. La modification de base de la page s’effectue en ajoutant une image et en modifiant le contenu texte. Encore une fois, l’exercice a été effectué sur une charge de base de 300 pages de complexité identique à celle définie dans le test de référence 1.

   * **Résultat**
Le débit maximal d’un tel scénario mélangeant des opérations est de 6 288 transactions par heure. Il s’agit d’une augmentation d’environ 93 % par rapport à une instance de création autonome pour la même évaluation des performances.

>[!NOTE]
>
>Le débit ne fait pas la distinction entre les types de transaction dans un profil de charge. L’approche utilisée pour mesurer le débit permet de s’assurer qu’une proportion fixe de chaque type de transaction est incluse dans la charge de travail.

Les deux tests ci-dessus montrent clairement que AEM s’adapte bien aux auteurs qui effectuent des opérations de modification de base avec AEM. En général, AEM est plus efficace pour dimensionner les opérations de lecture.

Sur un site web type, la plupart des opérations de création se produisent pendant la phase du projet. Une fois le site web lancé, le nombre d’auteurs travaillant en parallèle atteint généralement une moyenne inférieure (mode opérationnel).

Vous pouvez calculer le nombre d’ordinateurs (ou unités centrales) requis pour l’environnement de création comme suit :

`n = numberOfParallelAuthors / 30`

Cette formule peut servir de ligne directrice générale pour la mise à l’échelle des processeurs lorsque les auteurs effectuent des opérations de base avec AEM. Cela suppose que le système et l’application soient optimisés. Toutefois, la formule ne contiendra pas la valeur true pour les fonctionnalités avancées telles que MSM ou Assets (voir les sections ci-dessous).

Voir aussi [Mise en parallèle](/help/managing/hardware-sizing-guidelines.md#parallelization-of-aem-instances) et [Optimisation des performances](/help/sites-deploying/configuring-performance.md).

### Recommendations matériel {#hardware-recommendations}

En règle générale, vous pouvez utiliser le même matériel pour votre environnement de création que celui recommandé pour votre environnement de publication. En règle générale, le trafic sur le site web est beaucoup plus faible sur les systèmes de création, mais l’efficacité du cache est également plus faible. Cependant, le facteur fondamental ici est le nombre d’auteurs travaillant en parallèle, ainsi que le type d’actions effectuées sur le système. En règle générale, la mise en grappe AEM (de l’environnement de création) est plus efficace pour dimensionner les opérations de lecture ; en d’autres termes, une grappe AEM se met à l’échelle avec les auteurs qui effectuent des opérations de modification de base.

Les tests comparatifs à Adobe ont été réalisés à l’aide du système d’exploitation Red Hat® 5.5, exécuté sur une plateforme matérielle Hewlett-Packard ProLiant DL380 G5 avec la configuration suivante :

* Deux processeurs Intel Xeon® X5450 quadri-coeur à 3,00 GHz
* 8 Go de mémoire vive
* Broadcom NetXtreme II BCM5708 gigabit Ethernet
* Contrôleur RAID HP Smart Array, cache de 256 Mo
* Deux disques SAS à 10 000 tr/min de 146 Go configurés en tant qu’ensemble à bandes RAID0
* Le score de référence de taux SPEC CINT2006 est de 110

AEM instances s’exécutaient avec une taille de tas minimale de 256 M, une taille de tas maximale de 1 024 M.

## Publication de calculs spécifiques à l’environnement {#publish-environment-specific-calculations}

### Efficacité de la mise en cache et trafic {#caching-efficiency-and-traffic}

L’efficacité du cache est essentielle à la vitesse du site web. Le tableau suivant indique le nombre de pages qu’un système AEM optimisé peut gérer par seconde à l’aide d’un proxy inverse, tel que Dispatcher :

| Ratio de cache | Pages/s (pic) | Millions de pages/jour (moyenne) |
|---|---|---|
| 100% | 1000-2000 | 35-70 |
| 99% | 910 | 32 |
| 95% | 690 | 25 |
| 90% | 520 | 18 |
| 60% | 220 | 8 |
| 0% | 100 | 3,5 |

>[!CAUTION]
>
>Clause de non-responsabilité : les numéros dépendent d’une configuration matérielle par défaut et peuvent varier en fonction du matériel utilisé.

Le ratio de cache est le pourcentage de pages que Dispatcher peut renvoyer sans avoir à accéder à AEM. 100 % indique que Dispatcher répond à toutes les requêtes, 0 % signifie que AEM calcule chaque page.

### Complexité des modèles et des applications {#complexity-of-templates-and-applications}

Si vous utilisez des modèles complexes, AEM plus de temps sera nécessaire pour effectuer le rendu d’une page. Les pages extraites du cache ne sont pas affectées par cette situation, mais la taille de la page reste pertinente en ce qui concerne le temps de réponse global. Le rendu d’une page complexe peut facilement prendre dix fois plus de temps que le rendu d’une page simple.

### Formule {#formula}

À l’aide de la formule suivante, vous pouvez faire une estimation de la complexité globale de votre solution AEM :

`complexity = applicationComplexity + ((1-cacheRatio) * templateComplexity)`

Selon la complexité, vous pouvez déterminer le nombre de serveurs (ou de cœurs d’unité centrale) dont vous avez besoin pour l’environnement de publication comme suit :

`n = (traffic * complexity / 1000 ) * activations`

Les variables de l’équation sont les suivantes :

<table>
 <tbody>
  <tr>
   <td>traffic</td>
   <td>Le trafic en pic attendu par seconde. Vous pouvez l’estimer comme le nombre d’accès aux pages par jour, divisé par 35 000.</td>
  </tr>
  <tr>
   <td>applicationComplexity</td>
   <td><p>Utilisez 1 pour une application simple, 2 pour une application complexe, ou une valeur intermédiaire :</p>
    <ul>
     <li>1 - Un site entièrement anonyme, orienté contenu</li>
     <li>1.1 - Un site entièrement anonyme, orienté contenu, avec personnalisation côté client/Target</li>
     <li>1.5 - Un site orienté contenu avec des sections anonymes et connectées, personnalisation côté client/Target</li>
     <li>1.7 - Pour un site orienté contenu avec des sections anonymes et connectées, une personnalisation côté client/Target et un contenu généré par l’utilisateur</li>
     <li>2 - où l’ensemble du site nécessite une connexion, avec une utilisation intensive du contenu généré par l’utilisateur et diverses techniques de personnalisation</li>
    </ul> </td>
  </tr>
  <tr>
   <td>cacheRatio</td>
   <td>Pourcentage de pages qui sortent du cache de Dispatcher. Utilisez 1 si toutes les pages proviennent du cache ou 0 si chaque page est calculée par AEM.</td>
  </tr>
  <tr>
   <td>templateComplexity</td>
   <td>Utilisez une valeur comprise entre 1 et 10 pour indiquer la complexité de vos modèles. Des valeurs plus élevées indiquent des modèles plus complexes ; utilisez une valeur de 1 pour les sites avec une moyenne de 10 composants par page, une valeur de 5 pour une moyenne de 40 composants par page et 10 pour une moyenne de plus de 100 composants.</td>
  </tr>
  <tr>
   <td>activations</td>
   <td>Nombre d’activations moyennes (réplication de pages et de ressources de taille moyenne de l’auteur vers le niveau de publication) par heure divisé par x, où x est le nombre d’activations effectuées sur un système sans effets secondaires sur la performance des autres tâches traitées par le système. Vous pouvez également prédéfinir une valeur initiale pessimiste comme x = 100.<br /> </td>
  </tr>
 </tbody>
</table>

Si vous possédez un site web plus complexe, vous avez également besoin de serveurs web plus puissants afin qu’AEM réponde à une requête dans un délai acceptable.

* Complexité inférieure à 4 :
   * RAM JVM 1 024 Mo&#42;
   * Processeur basse à moyenne performance

* Complexité de 4 à 8 :
   * JVM 2 048 Mo&#42;
   * Processeur milieu à hautes performances

* Complexité supérieure à 8 :
   * 4 096 Mo de RAM JVM&#42;
   * Processeur hautes performances de bout en bout

>[!NOTE]
>
>&#42; Réservez suffisamment de RAM pour votre système d’exploitation en plus de la mémoire requise pour votre JVM.

## Autres calculs spécifiques à un cas d’utilisation {#additional-use-case-specific-calculations}

Outre le calcul d’une application web par défaut, vous devrez peut-être prendre en compte des facteurs spécifiques pour les cas d’utilisation suivants. Les valeurs calculées doivent être ajoutées au calcul par défaut.

### Considérations spécifiques aux ressources {#assets-specific-considerations}

Le traitement étendu des ressources numériques nécessite des ressources matérielles optimisées, les facteurs les plus pertinents sont la taille de l’image et le débit maximal des images traitées.

Allouez au moins 16 Go de segment de mémoire et configurez le workflow [!UICONTROL Ressource de mise à jour de gestion des ressources numériques] pour qu’il utilise le [package Camera Raw](/help/assets/camera-raw.md) pour l’ingestion des images au format RAW.

>[!NOTE]
>
>Un débit d’images plus élevé signifie que les ressources informatiques doivent pouvoir suivre le rythme des E/S système et inversement. Par exemple, si les workflows sont lancés par l&#39;import d&#39;images, le téléchargement de nombreuses images via WebDAV peut entraîner un retard de workflows.
>
>L’utilisation de disques distincts pour TarPM, le magasin de données et l’index de recherche peut aider à optimiser le comportement d’E/S du système (cependant, il est généralement logique de conserver l’index de recherche localement).

>[!NOTE]
>
>Voir aussi [Guide des performances des ressources](/help/sites-deploying/assets-performance-sizing.md).

### Multi-site Manager {#multi-site-manager}

La consommation des ressources lors de l’utilisation d’AEM MSM dans un environnement de création dépend fortement des cas d’utilisation spécifiques. Les facteurs de base sont les suivants :

* Nombre de Live Copies
* Périodicité des déploiements
* Taille de l’arborescence de contenu à déployer
* Fonctionnalité connectée des actions de déploiement

Le test du cas d’utilisation prévu avec un extrait de contenu représentatif peut vous aider à mieux comprendre la consommation de ressources. Si vous extrapolez les résultats avec la fréquence prévue, vous pouvez évaluer les ressources supplémentaires requises pour AEM MSM.

Tenez également compte des auteurs travaillant en parallèle. Ils percevront les effets secondaires sur les performances si AEM cas d’utilisation MSM consomment plus de ressources que prévu.

### Considérations relatives au dimensionnement d’AEM Communities {#aem-communities-sizing-considerations}

Les sites AEM qui incluent des fonctions AEM Communities connaissent un haut niveau d’interaction des visiteurs du site (membres) dans l’environnement de publication.

Les considérations de dimensionnement d’un site de communauté dépendent de l’interaction anticipée des membres de la communauté et de l’importance accrue des performances optimales du contenu de la page.

Les membres envoyés du contenu généré par l’utilisateur sont stockés séparément du contenu de la page. Alors que la plateforme AEM utilise un magasin de nœuds qui réplique le contenu du site de l’instance de création vers l’instance de publication, AEM Communities utilise un magasin simple et commun pour le contenu généré par les utilisateurs qui n’est jamais répliqué.

Pour le magasin du contenu généré par les utilisateurs, il est nécessaire de sélectionner un fournisseur de ressources de stockage qui influence le déploiement sélectionné.
Voir

* [Stockage de contenu de la communauté](/help/communities/working-with-srp.md)
* [Topologies recommandées pour Communities](/help/communities/topologies.md)
