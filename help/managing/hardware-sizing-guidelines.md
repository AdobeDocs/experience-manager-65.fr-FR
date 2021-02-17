---
title: Consignes de dimensionnement du matériel
seo-title: Consignes de dimensionnement du matériel
description: Ces consignes de dimensionnement procurent une estimation des ressources matérielles requises pour déployer un projet AEM.
seo-description: Ces consignes de dimensionnement procurent une estimation des ressources matérielles requises pour déployer un projet AEM.
uuid: 395f9869-17c4-4b9b-99f8-d35a44dd6256
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: managing
content-type: reference
discoiquuid: 8893306f-4bc0-48eb-8448-36d0214caddf
docset: aem65
translation-type: tm+mt
source-git-commit: f24142064b15606a5706fe78bf56866f7f9a40ae
workflow-type: tm+mt
source-wordcount: '2835'
ht-degree: 80%

---


# Consignes de dimensionnement du matériel{#hardware-sizing-guidelines}

Ces consignes de dimensionnement procurent une estimation des ressources matérielles requises pour déployer un projet AEM. Les estimations de dimensionnement dépendent de l&#39;architecture du projet, de la complexité de la solution, du trafic attendu et des exigences du projet. Ce guide vous aide à déterminer les besoins matériels pour une solution spécifique ou à trouver une estimation supérieure et inférieure pour les exigences matérielles.

Les facteurs fondamentaux à prendre en compte sont (dans cet ordre) :

* **Vitesse du réseau**

   * Latence du réseau
   * Bande passante disponible

* **Vitesse de calcul**

   * Efficacité de la mise en cache
   * Trafic attendu
   * Complexité des modèles, des applications et des composants
   * Auteurs simultanés
   * Complexité de l’opération de création (modification de contenu simple, déploiement MSM, etc.)

* **Performance d’E/S**

   * Performance et efficacité du stockage des fichiers ou de la base de données

* **Disque dur**

   * Au moins deux ou trois fois plus grand que la taille du référentiel

* **Mémoire**

   * Taille du site web (nombre d’objets de contenu, de pages et d’utilisateurs)
   * Nombre d’utilisateurs/de sessions qui sont actifs en même temps

## Architecture {#architecture}

Une configuration AEM type se compose d’un environnement de création et de publication. Ces environnements ont différentes exigences en ce qui concerne la taille du matériel sous-jacent et la configuration système. Les considérations détaillées relatives aux deux environnements sont décrites dans les sections [environnement d’auteur](/help/managing/hardware-sizing-guidelines.md#author-environment-specific-calculations) et [environnement de publication](/help/managing/hardware-sizing-guidelines.md#publish-environment-specific-calculations).

Dans une configuration de projet type, vous disposez de plusieurs environnements sur lesquels définir les phases du projet :

* L’**environnement de développement** pour le développement de nouvelles fonctions ou pour apporter des modifications importantes. La meilleure pratique consiste à utiliser un environnement de développement par développeur (généralement des installations locales sur leurs systèmes personnels).

* ****
Environnement de test de l’auteurPour vérifier les modifications. Le nombre d’environnements de test peut varier en fonction des exigences du projet (par exemple, séparément pour l’assurance qualité, les tests d’intégration ou les tests d’acceptation par l’utilisateur).

* L’**environnement de test de publication** principalement pour tester les cas d’utilisation de collaboration sociale et/ou l’interaction entre l’instance de création et plusieurs instances de publication.

* L’**environnement de production de création** pour que les auteurs modifient le contenu.

* L’**environnement de production de publication** pour servir du contenu publié.

En outre, les environnements peuvent varier, d’un système à un serveur exécutant AEM et un serveur d’application, à un ensemble d’instances organisées en grappes multiserveur et multiprocesseur hautement évoluées. Nous vous recommandons d’utiliser un ordinateur distinct pour chaque système de production et de ne pas exécuter d’autres applications sur ces ordinateurs.

## Remarques génériques concernant le dimensionnement du matériel {#generic-hardware-sizing-considerations}

Les sections suivantes fournissent des instructions pour calculer les configurations matérielles requises, en prenant en compte plusieurs points. Pour les systèmes de grande taille, nous suggérons que vous réalisiez un simple jeu de tests d’évaluation des performances en interne sur une configuration de référence.

L’optimisation des performances est une tâche fondamentale qui doit être effectuée avant que toute évaluation des performances ne puisse être réalisée pour un projet spécifique. Veillez à suivre les conseils fournis dans la [documentation d’optimisation des performances](/help/sites-deploying/configuring-performance.md) avant de procéder aux tests d’évaluation des performances et d’utiliser leurs résultats pour les calculs de dimensionnement du matériel.

Les exigences de dimensionnement du matériel pour les cas d’utilisation plus complexes doivent reposer sur une estimation détaillée des performances du projet. Les cas d’utilisation plus complexes qui nécessitent des ressources matérielles exceptionnelles présentent une combinaison des caractéristiques suivantes :

* charge utile/débit de contenu élevé ;
* usage intensif de code personnalisé, de workflows personnalisés ou de bibliothèques de logiciels tiers ;
* intégration à des systèmes externes non pris en charge.

### Disque dur/espace disque  {#disk-space-hard-drive}

L’espace disque requis dépend largement du volume et du type de votre application web. Les calculs doivent prendre en compte les éléments suivants :

* le nombre et la taille des pages, des ressources et des autres entités stockées dans un référentiel, telles que les workflows, les profils, etc. ;
* la fréquence attendue de modifications du contenu et donc de la création de versions de contenu ;
* le volume de rendus de ressources de gestion des actifs numériques qui seront générés ;
* la croissance générale du contenu au fil du temps.

L’espace disque est continuellement surveillé en ligne, hors ligne et lors du nettoyage des révisions. Si l’espace disque passe en dessous d’une certaine valeur, le processus est annulé. La valeur critique correspond à 25 % de l’encombrement sur le disque du référentiel ; elle n’est pas configurable. Il est recommandé de dimensionner le disque de sorte qu’il soit au moins deux ou trois fois plus large que la taille du référentiel, y compris sa croissance estimée.

Envisagez une configuration de baies redondantes composée de disques indépendants (RAID, par exemple RAID10) pour la redondance des données.

>[!NOTE]
>
>Le répertoire temporaire d’une instance de production doit disposer d’au moins 6 Go d’espace disponible.

#### Virtualisation  {#virtualization}

AEM s’exécute correctement dans les environnements virtualisés, mais certains facteurs tels que l’unité centrale ou les E/S peuvent ne pas correspondre directement au matériel physique. Nous vous recommandons de sélectionner une vitesse d’E/S accrue (en général), car il s’agit d’un facteur déterminant dans la plupart des cas. L’évaluation des performances de votre environnement est nécessaire pour obtenir une idée précise des ressources requises.

#### Mise en parallèle d’instances AEM  {#parallelization-of-aem-instances}

**Absence de sécurité**

Un site web doté de la prévention de défaillance est déployé sur au moins deux systèmes distincts. Si un système tombe en panne, un autre système peut prendre la relève de façon à compenser la défaillance du système.

**Évolutivité des ressources système**

Lorsque tous les systèmes sont en cours d’exécution, une performance de calcul accrue est disponible. Ces performances supplémentaires ne sont pas nécessairement linéaires avec le nombre de noeuds de grappe, car la relation est fortement dépendante de l&#39;environnement technique ; pour plus d&#39;informations, consultez la [documentation sur les grappes](/help/sites-deploying/recommended-deploys.md).

L’estimation du nombre de nœuds de grappes nécessaires dépend des exigences de base, ainsi que des cas d’utilisation spécifiques du projet web en question :

* Du point de vue de la prévention de défaillance, il est nécessaire de déterminer, pour tous les environnements, l’importance de la défaillance et le temps de compensation de la défaillance en fonction du temps nécessaire pour qu’un nœud de grappes se rétablisse.
* En ce qui concerne l’évolutivité, le nombre d’opérations d’écriture est fondamentalement le facteur le plus important. Voir [Auteurs travaillant en parallèle](/help/managing/hardware-sizing-guidelines.md#authors-working-in-parallel) pour l’environnement de création et [Collaboration sociale](/help/managing/hardware-sizing-guidelines.md#socialcollaborationspecificconsiderations) pour l’environnement de publication. L&#39;équilibrage de charge peut être établi pour les opérations qui n&#39;ont accès au système que pour traiter les opérations de lecture ; pour plus de détails, voir [Répartiteur](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html).

## Calculs spécifiques à l’environnement de création {#author-environment-specific-calculations}

Adobe a développé plusieurs tests d’évaluation des performances pour des instances de création autonomes.

* **Test d’évaluation des performances 1** Calcule le débit d’un profil de charge lorsque les utilisateurs exécutent un simple exercice de création de pages sur une charge de base de 300 pages existantes, toutes de nature similaire. Les étapes impliquées étaient la connexion au site, la création d’une page contenant un SWF et une image/du texte, l’ajout d’un nuage de balises, puis l’activation de la page.

   * **Résultat** Le débit maximal d’un simple exercice de création de pages comme plus haut (considéré comme une transaction) est de 1 730 transactions/heure.

* **Test d’évaluation des performances 2** Calcule le débit maximal lorsque le profil de charge comprend la création d’une page (10 %), la modification d’une page existante (80 %), ainsi que la création, puis la modification d’une page successivement (10 %). La complexité des pages reste la même que dans le profil du test d’évaluation des performances 1. La modification de base de la page est effectuée en ajoutant une image et en modifiant le contenu textuel. Là encore, l’exercice a été effectué sur une charge de base de 300 pages de même complexité, tel que défini dans le test d’évaluation des performances 1.

   * **Résultat** Le débit maximal d’un tel scénario mélangeant des opérations est de 3 252 transactions par heure.

>[!NOTE]
>
>Le débit ne fait pas la distinction entre les types de transactions au sein d’un profil de charge. La méthode utilisée pour mesurer le débit s’assure qu’une proportion fixe de chaque type de transaction est incluse dans la charge de travail.

Les deux tests ci-dessus indiquent que le débit varie en fonction du type d’opération. Utilisez les activités dans votre environnement comme base pour dimensionner votre système. Vous obtenez un meilleur débit avec des actions moins intensives, telles que la modification (qui est également plus courante).

### Mise en cache {#caching}

Dans l’environnement de création, l’efficacité de la mise en cache est en général bien plus faible, car les modifications du site web sont plus fréquentes et en raison du caractère hautement interactif et personnalisé du contenu. Grâce au répartiteur, vous pouvez mettre en cache AEM bibliothèques, JavaScript, fichiers CSS et images de mise en page. Cela permet d’accélérer certains aspects du processus de création. La configuration du serveur web afin de définir des en-têtes supplémentaires pour la mise en cache de ces ressources dans le navigateur, réduit le nombre de requêtes HTTP et améliore ainsi la réactivité du système pour les auteurs.

### Auteurs travaillant en parallèle {#authors-working-in-parallel}

Dans l’environnement de création, le nombre d’auteurs qui travaillent en parallèle et la charge que leurs interactions ajoutent au système constituent les principaux facteurs de limitation. Par conséquent, nous vous recommandons de dimensionner votre système en fonction du débit partagé des données.

Pour de tels scénarios, Adobe a effectué des tests d’évaluation des performances sur une grappe à deux nœuds sans partage d’instances de création.

* **Test d’évaluation des performances 1a** Avec une grappe sans partage active-active de deux instances de création, calcule le débit maximal avec un profil de charge où les utilisateurs exécutent un exercice simple de création de page sur une charge de base de 300 pages existantes, toutes de nature similaire.

   * **Résultat** Le débit maximal d’un simple exercice de création de page comme plus haut (considéré comme une transaction) est de 2 016 transactions/heure. Il s’agit d’une augmentation d’environ 16 % par rapport à une instance de création autonome pour la même évaluation des performances.

* **Test Benchmark 2**
bAvec une grappe principale de 2 instances d’auteur sans partage, calculez le débit maximal lorsque le profil de chargement comporte un mélange de création de page nouvelle (10 %), de modification d’une page existante (80 %) et de création et de modification d’une page en succession (10 %). La complexité de la page reste la même que dans le profil du test d’évaluation des performances 1. La modification de base de la page est effectuée en ajoutant une image et en modifiant le contenu textuel. Là encore, l’exercice a été effectué sur une charge de base de 300 pages de même complexité, tel que défini dans le test d’évaluation des performances 1.

   * **Résultat** Le débit maximal d’un tel scénario mélangeant des opérations est de 6 288 transactions par heure. Il s’agit d’une augmentation d’environ 93 % par rapport à une instance de création autonome pour la même évaluation des performances.

>[!NOTE]
>
>Le débit ne fait pas la distinction entre les types de transactions au sein d’un profil de charge. La méthode utilisée pour mesurer le débit s’assure qu’une proportion fixe de chaque type de transaction est incluse dans la charge de travail.

Les deux tests ci-dessus indiquent clairement qu’AEM se dimensionne correctement pour les auteurs qui exécutent des opérations de modification de base avec AEM. En général, AEM est plus efficace pour dimensionner les opérations de lecture.

Sur un site web type, la plus grande partie de la création se produit pendant la phase de projet. Une fois le site web activé, le nombre d’auteurs travaillant en parallèle baisse généralement vers une moyenne inférieure (en mode opérationnel).

Vous pouvez calculer le nombre d’ordinateurs (ou d’unités centrales) requis pour l’environnement d’auteur comme suit :

`n = numberOfParallelAuthors / 30`

Cette formule peut servir d’orientation générale pour dimensionner les unités centrales lorsque les auteurs effectuent des opérations de base avec AEM. Elle part du principe que le système et l’application sont optimisés. Toutefois, la formule ne convient pas pour les fonctions avancées telles que MSM ou Assets (voir les sections ci-dessous).

Consultez également les commentaires supplémentaires sur [Parallélisation](/help/managing/hardware-sizing-guidelines.md#parallelization-of-aem-instances) et [Optimisation des performances](/help/sites-deploying/configuring-performance.md).

### Recommandations matérielles {#hardware-recommendations}

En règle générale, vous pouvez utiliser pour votre environnement de création le même matériel que celui recommandé pour votre environnement de publication. Le trafic de votre site web est normalement nettement inférieur sur les systèmes de création, mais l’efficacité du cache est également inférieure. Toutefois, le facteur fondamental est ici le nombre d’auteurs travaillant en parallèle, ainsi que le type des actions réalisées sur le système. En général, la mise en grappe AEM (de l’environnement de création) est plus efficace pour dimensionner les opérations de lecture ; en d’autres termes, une grappe AEM se dimensionne correctement avec les auteurs qui effectuent des opérations de modification de base.

Les tests de référence à l&#39;Adobe ont été effectués à l&#39;aide du système d&#39;exploitation RedHat 5.5, exécuté sur une plate-forme matérielle Hewlett-Packard ProLiant DL380 G5 avec la configuration suivante :

* Deux unités centrales Intel Xeon Quad Core X5450 à 3 GHz
* 8 Go de RAM
* Gigabit Ethernet Broadcom NetXtreme II BCM5708
* Contrôleur RAID HP Smart Array, avec une mémoire cache de 256 Mo
* Deux disques SAS à 10 000 tr/min de 146 Go configurés en tant que jeu d’agrégats par bandes RAID0
* Le score d’évaluation des performances de la spécification CINT2006 est de 110.

Les instances AEM fonctionnaient avec une taille de tas minimale de 256 Mo et une taille maximale de 1 024 Mo.

## Calculs spécifiques à l’environnement de publication  {#publish-environment-specific-calculations}

### Efficacité de la mise en mémoire cache et trafic {#caching-efficiency-and-traffic}

L’efficacité de la mise en mémoire cache est cruciale pour la vitesse du site web. Le tableau suivant indique le nombre de pages pouvant être gérées par seconde par un système AEM optimisé à l’aide d’un proxy inverse, tel que le Dispatcher :

| Ratio de cache | Pages/s (pic) | Millions de pages par jour (moyenne) |
|---|---|---|
| 100% | 1000-2000 | 35-70 |
| 99% | 910 | 32 |
| 95% | 690 | 25 |
| 90 % | 520 | 18 |
| 60% | 220 | 8 |
| 0% | 100 | 3.5 |

>[!CAUTION]
>
>Clause de non-responsabilité : les chiffres sont basés sur une configuration matérielle par défaut et peuvent varier en fonction du matériel utilisé.

Le rapport de cache est le pourcentage de pages que le Dispatcher peut renvoyer sans devoir accéder à AEM. 100 % indique que le Dispatcher répond à toutes les requêtes, 0 % signifie qu’AEM calcule chaque page.

### Complexité des modèles et des applications  {#complexity-of-templates-and-applications}

Si vous utilisez des modèles complexes, AEM aura besoin de plus de temps pour effectuer le rendu d’une page. Les pages extraites du cache ne sont pas affectées, mais la taille de la page est toujours pertinente en ce qui concerne le délai de réponse global. Le rendu d’une page complexe peut aisément prendre dix fois plus longtemps que le rendu d’une seule page.

### Formule  {#formula}

La formule suivante vous permet de calculer une estimation de la complexité globale de votre solution AEM :

`complexity = applicationComplexity + ((1-cacheRatio) * templateComplexity)`

En fonction de la complexité, vous pouvez déterminer le nombre de serveurs (ou de coeurs CPU) nécessaires pour l’environnement de publication comme suit :

`n = (traffic * complexity / 1000 ) * activations`

Les variables de l’équation sont les suivantes :

<table>
 <tbody>
  <tr>
   <td>trafic</td>
   <td>Trafic de pointe attendu par seconde. Vous pouvez l’estimer comme le nombre de visites de pages par jour, divisé par 35 000.</td>
  </tr>
  <tr>
   <td>applicationComplexity</td>
   <td><p>Utilisez 1 pour une application simple, 2 pour une application complexe ou une valeur intermédiaire :</p>
    <ul>
     <li>1 - un site entièrement anonyme, orienté contenu</li>
     <li>1.1 - un site entièrement anonyme orienté contenu avec personnalisation côté client/Cible</li>
     <li>1.5 - site orienté contenu avec des sections anonymes et connectées, personnalisation côté client/Cible</li>
     <li>1.7 - pour un site orienté contenu avec des sections anonymes et connectées, personnalisation côté client/Cible et certains contenus générés par les utilisateurs</li>
     <li>2 - où l'ensemble du site nécessite la connexion, avec une utilisation intensive du contenu généré par les utilisateurs et une variété de techniques de personnalisation</li>
    </ul> </td>
  </tr>
  <tr>
   <td>cacheRatio</td>
   <td>Pourcentage de pages qui sortent du cache du répartiteur. Utilisez 1 si toutes les pages proviennent du cache ou 0 si chaque page est calculée par AEM.</td>
  </tr>
  <tr>
   <td>templateComplexity</td>
   <td>Utilisez une valeur comprise entre 1 et 10 pour indiquer la complexité de vos modèles. Des valeurs plus élevées indiquent des modèles plus complexes ; utilisez une valeur de 1 pour les sites avec une moyenne de 10 composants par page, une valeur de 5 pour une moyenne de 40 composants par page et 10 pour une moyenne de plus de 100 composants.</td>
  </tr>
  <tr>
   <td>activations</td>
   <td>Nombre d’activations moyennes (réplication de pages et de ressources de taille moyenne de l’auteur au niveau de publication) par heure divisé par x, où x est le nombre d’activations effectuées sur un système sans effets secondaires sur les performances pour d’autres tâches traitées par le système. Vous pouvez également prédéfinir une valeur initiale pessimiste comme x = 100.<br /> </td>
  </tr>
 </tbody>
</table>

Si vous possédez un site web plus complexe, vous avez également besoin de serveurs web plus puissants afin qu’AEM réponde à une requête dans un délai acceptable.

* Complexité inférieure à 4 :
・ 1 024 Mo de RAM JVM*
・ Processeur basse à moyenne performance

* Complexité entre 4 et 8 :
・ 2 048 Mo de RAM JVM*
・ Processeur milieu à hautes performances

* Complexité supérieure à 8 :
・ 4 096 Mo de RAM JVM*
・ Processeur haute-performance

>[!NOTE]
>
>* Réservez suffisamment de RAM pour votre système d’exploitation en plus de la mémoire requise pour votre JVM.

## Autres calculs spécifiques aux cas d’utilisation {#additional-use-case-specific-calculations}

En plus du calcul pour une application web par défaut, il est possible que vous deviez tenir compte de facteurs spécifiques pour les cas d’utilisation suivants. Les valeurs calculées doivent être ajoutées au calcul par défaut.

### Considérations spécifiques aux ressources  {#assets-specific-considerations}

Le traitement étendu des ressources numériques nécessite des ressources matérielles optimisées. Les facteurs les plus pertinents sont la taille des images et le débit maximal des images traitées.

Attribuez au moins 16 Go de tas et configurez le flux de travaux [!UICONTROL DAM Update Asset] pour utiliser le [package Camera Raw](/help/assets/camera-raw.md) pour l&#39;assimilation d&#39;images brutes.

>[!NOTE]
Un débit d’images plus élevé signifie que les ressources de calcul doivent pouvoir suivre la cadence des E/S du système et vice versa. Par exemple, si des workflows sont lancés en important des images, le téléchargement de nombreuses images via WebDAV peut entraîner un journal des workflows en souffrance.
L’utilisation de disques distincts pour TarPM, le magasin de données et l’index de recherche peut aider à optimiser le comportement d’E/S du système (il est toutefois généralement préférable de conserver l’index de recherche localement).

>[!NOTE]
Voir aussi le [guide de performance des ressources](/help/sites-deploying/assets-performance-sizing.md).

### Gestionnaire multisite  {#multi-site-manager}

La consommation de ressources lors de l’utilisation du gestionnaire multisite AEM dans un environnement de création dépend en grande partie des cas d’utilisation spécifiques. Les facteurs de base sont les suivants :

* Le nombre de Live Copies
* La fréquence des déploiements
* La taille de l’arborescence de contenu à déployer
* La fonctionnalité de connexion des actions de déploiement

Le test du cas d’utilisation prévu avec un extrait de contenu représentatif peut vous aider à améliorer votre compréhension de la consommation des ressources. Si vous extrapolez les résultats avec la fréquence prévue, vous pouvez évaluer les ressources supplémentaires requises pour AEM MSM.

Tenez compte également du fait que les auteurs travaillant en parallèle subiront des effets secondaires au niveau des performances si les cas d’utilisation AEM MSM consomment davantage de ressources que prévu.

### Considérations de dimensionnement pour AEM Communities  {#aem-communities-sizing-considerations}

Les sites AEM qui incluent des fonctions AEM Communities (des sites de communauté) connaissent un haut niveau d’interaction des visiteurs du site (membres) dans l’environnement de publication.

Les considérations de dimensionnement pour un site de communauté dépendent de l’interaction anticipée des membres de la communauté et de l’importance de disposer de performances optimales pour le contenu des pages.

Le contenu généré par les utilisateurs et soumis par les membres est stocké séparément du contenu des pages. Alors que la plateforme AEM utilise une banque de noeuds qui répliquera le contenu du site de l’auteur à la publication, AEM Communities utilise une banque de données unique et commune pour l’UGC qui n’est jamais répliquée.

Pour le magasin du contenu généré par les utilisateurs, il est nécessaire de sélectionner un fournisseur de ressources de stockage qui influence le déploiement sélectionné.
Voir

* [Stockage de contenu de la communauté](/help/communities/working-with-srp.md)
* [Topologies recommandées pour Communities](/help/communities/topologies.md)

