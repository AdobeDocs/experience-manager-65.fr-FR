---
title: La Liste de contrôle – Référence supplémentaire
description: Découvrez d’autres informations qui développent et/ou complètent les documents et principes couverts par la section Gestion des projets - Liste des bonnes pratiques.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: managing-checklist
content-type: reference
exl-id: 36620e3e-ecdf-4062-bbef-65513362d691
solution: Experience Manager, Experience Manager 6.5
feature: Compliance
role: Admin,Architect,Data Architect,Developer,Leader
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '3699'
ht-degree: 100%

---

# La Liste de contrôle – Référence supplémentaire{#the-checklist-further-reference}

Cette page fournit des détails supplémentaires qui développent et/ou complètent les documents et principes couverts par la section [Gestion des projets - Liste des bonnes pratiques](/help/managing/best-practices.md).

## AEM - Qu’allez-vous utiliser ? {#aem-what-will-you-be-using}

>[!CAUTION]
>
>Les listes de cette sous-section ne sont pas exhaustives, mais elles ont pour but de servir d’introduction.

### Fonctionnalités d’AEM {#features-within-aem}

Lors de l’implémentation d’AEM (notamment pour la première fois), vous devez passer en revue les [fonctionnalités et les workflows d’AEM](https://business.adobe.com/fr/products/experience-manager/adobe-experience-manager.html) afin de connaître avec certitude les domaines souhaités/requis.

Tenez compte des fonctions d’AEM que vous utiliserez et de l’impact sur votre travail de conception, notamment pour les éléments suivants :

* [Commerce](/help/commerce/cif-classic/administering/ecommerce.md)
* [Screens](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/aem-screens-introduction.html?lang=fr)
* [Assets](/help/assets/assets.md)
* [Balises](/help/sites-administering/tags.md)
* [Gestion de sites multiples et traduction](/help/sites-administering/msm-and-translation.md)
* [Forms](/help/forms/using/introduction-aem-forms.md)
* [Communities](/help/communities/deploy-communities.md)

Vérifiez également les [Notes de mise à jour](/help/release-notes/release-notes.md) des différentes versions d’AEM, pour savoir quand de nouvelles fonctionnalités ont été ajoutées.

### Intégrations {#integrations}

AEM peut être intégré à d’autres produits Adobe, à des services tiers, ou aux deux. Ces workflows peuvent augmenter la puissance et les fonctionnalités à votre disposition.

Voir [Intégration de solutions](/help/sites-administering/integration.md) pour plus d’informations.

## Migrer ou mettre à niveau ? {#migrate-or-upgrade}

Il est important de déterminer si vous souhaitez :

* Mettre à niveau l’installation existante.
* Migrer le contenu du système actuel vers une nouvelle installation.

Lorsque vous passez d’une version précédente à la version actuelle, deux options sont disponibles :

* Utiliser le [gestionnaire de modules](/help/sites-administering/package-manager.md) pour exporter tout le contenu et le code de l’application de l’ancien système vers le nouveau.
* [Mettre à niveau](/help/sites-deploying/upgrade.md) l’ancien système. Cette méthode est généralement recommandée.

## Règles de base {#basic-ground-rules}

Comme pour tout projet, il est essentiel d’établir des règles de base dès que possible. Ces règles incluent :

>[!NOTE]
>
>Ces points sont génériques, la [liste de contrôle des bonnes pratiques](/help/managing/best-practices.md) aborde les détails spécifiques à AEM.

* **Rôles**

  Les rôles doivent être clairement définis et connus de toutes les personnes qui participent au projet. En outre, il est conseillé de mettre en évidence les rôles suivants :

   * les décideurs et décideuses ;
   * les points de contact ;

* **les responsabilités**.

   * Pour chaque rôle, une définition claire des responsabilités liées à votre projet permet d’éviter toute confusion.

* **Implication**

  En impliquant dès que possible les parties intéressées, vous pouvez les encourager à devenir *parties prenantes* du projet. Vous augmentez ainsi leur engagement en vue du succès du projet.

   * Côté clientèle, ce rôle inclut les personnes qui travaillent au quotidien avec le système.
   * Au sein de votre propre équipe de projet, cette implication inclut également les personnes responsables de l’assurance qualité. Mieux elles comprennent les exigences de la clientèle, mieux elles peuvent planifier les tests.

* **Voies de communication**

   * Les voies de communications ne doivent pas être trop formalisées, mais des définitions spécifiques doivent toutefois veiller à ce que les personnes principales soient toujours informées. Une attention particulière doit être portée à la communication avec les parties externes.

* **Processus**

  Les processus définis dépendent de votre projet individuel. Là encore, essayez de garder ces processus simples, en tenant compte des éléments suivants :

   * Vous devez définir des processus (et voies de communication) pour interagir avec des tiers, comme les agences de conception et les fournisseurs de logiciels tiers.
   * Souvent, le client ou la cliente dispose de ses propres procédures et outils de gestion de projet et de création de rapports.

* **Outils de tracking**

  De nombreux outils sont disponibles pour effectuer le tracking d’informations sur les bugs, les tâches et d’autres aspects de votre projet. Voir [Vue d’ensemble des outils potentiels](#overview-of-potential-tools) pour plus d’informations.

   * Le point essentiel à noter ici est de ne conserver qu’une seule copie de l’information et de la partager (et donc d’accéder à l’outil utilisé). Ce workflow facilite la maintenance et permet d’éviter les incohérences.

* **Portée**

  Définissez clairement ce qui doit être couvert par le projet à différents niveaux :

   * les versions individuelles (si un processus de publication itératif est utilisé, et qu’elles soient diffusées ou non aux clientes et clients ou à votre équipe de test interne) ;
   * le projet AEM ;
   * l’ensemble du projet, y compris les logiciels tiers, leur impact sur les tests, les problèmes d’organisation, etc.
   * Pour certains aspects, il peut également être utile d’indiquer ce qui *n’entre pas* dans le cadre du projet. Cette méthode peut aider à éviter la confusion et les hypothèses incorrectes, bien qu’elle doive se limiter à des questions essentielles.

* **Création de rapports**

  Définissez clairement les informations que vous souhaitez rapporter, sous quelle forme, à quelle fréquence et à qui.

* **Terminologie**

   * Définissez les abréviations et/ou la terminologie à utiliser spécifiques à la clientèle.

* **Hypothèses**

   * Définissez les hypothèses faites.

Ces informations peuvent être définies dans un manuel de projet ; l’utilisation d’un wiki peut également vous assurer que les modifications en cours sont gérées efficacement. Lorsqu’elles sont définies, les principaux facteurs sont les suivants :

* les informations sont définies et conservées ;
* les informations sont clairement communiquées à toutes les personnes impliquées. Bien que cette pratique soit courante en matière de gestion de projet, on ne répètera jamais assez qu’une définition claire des rôles et une bonne communication peuvent faire ou défaire un projet.
* Une seule version des informations suivies est conservée, par exemple, le tracking des bugs et le tracking des problèmes.

## Indicateurs de performance clés et mesures cibles {#key-performance-indicators-and-target-metrics}

Les organisations utilisent des indicateurs de performances clés (IPC) pour évaluer leur capacité à atteindre des cibles. Ces indicateurs sont des valeurs mesurables qui peuvent être utilisées pour démontrer l’efficacité avec laquelle des objectifs spécifiques sont atteints.

Ces tests peuvent être les éléments suivants :

* Entreprise :

   * permet de mesurer les objectifs d’entreprise clés.
   * Il est important de choisir les indicateurs de performance clés appropriés à votre entreprise/scénario et de définir clairement ce qu’ils sont, comment ils sont mesurés, comment ils sont utilisés et par qui.

* Performances :

   * permet de définir comment mesurer les performances du système.
   * Voici quelques exemples : temps de chargement des pages, temps de réponse du serveur et performances des requêtes de base de données.

Certains indicateurs peuvent être basés sur les mesures cibles que vous identifiez et définissez.

### Mesures cibles : {#target-metrics}

ces mesures permettent de définir quantitativement la qualité de votre site web. Il s’agit essentiellement d’une définition des objectifs de performances à atteindre et qui peuvent être utilisés pour définir vos [indicateurs de performance clés](#key-performance-indicators-and-target-metrics).

De nombreuses mesures peuvent être définies. Souvent, celles que vous définissez couvrent vos objectifs en termes de performances et de simultanéité. En particulier, il s’agit des facteurs qui peuvent être difficiles à quantifier et qui sont souvent sujets à une évaluation *émotionnelle* :

* « Le site web est *beaucoup trop lent* aujourd’hui » - Que signifie *lent* et à quel moment doit-on en tenir compte ?

* « Tout *se fige* lorsque mon collègue se connecte » - Combien d’utilisateurs simultanés le système peut-il prendre en charge ?
* « Lorsque j’effectue une recherche, le système *se fige* » - Quelles sont les requêtes de recherche qui affectent le système ?
* « Le fichier *prend des lustres* à se télécharger » - Quel est le délai de téléchargement acceptable (dans des conditions réseau normales) ?

Les mesures cibles sont définies au début d’un projet pour :

* indiquer les dimensions attendues du site web que vous pouvez proposer ;
* indiquer la qualité minimale à atteindre ;
* définir la manière dont ces facteurs sont mesurés ;
* être utilisées comme base pour les [indicateurs de performance clés](#key-performance-indicators-and-target-metrics).

Comme toujours, vous devez faire attention lors de la définition des mesures cibles :

* si elles sont trop élevées, elles risquent d’être inaccessibles ;
* si elles sont trop faibles, les fluctuations peuvent ne pas être mises en évidence ;
* pour s’assurer qu’elles peuvent être mesurées de manière répétée et cohérente ;
* afin de fournir un équilibre entre les différents facteurs mesurés ;
* certaines mesures concernent un environnement de test mais d’autres devraient refléter des scénarios de la vie réelle, car elles doivent être mesurables et reproductibles sur votre site web de production ;
* classez les mesures par priorité en fonction de leur importance pour le site web ;
* limitez les mesures à un ensemble pouvant être surveillé.

Au cours du développement du projet, elles peuvent être mises à jour et ajustées selon les besoins. Une fois le projet implémenté avec succès, vous pouvez les utiliser pour contrôler votre installation et surveiller/gérer les niveaux de service requis pour le fonctionnement en cours.

Si elles sont correctement utilisées, ces mesures peuvent fournir un outil utile. En revanche, si elles sont utilisées de manière irresponsable, elles peuvent constituer une distraction et une perte de temps. Comme toujours, comprenez ce que vous mesurez, comment vous le mesurez et pourquoi.

>[!NOTE]
>
>Cette section présente les principes de base et les problèmes à résoudre. Chaque installation étant différente, les valeurs réelles à mesurer ont tendance à varier.

### Tout repose sur la conception de votre projet. {#everything-rests-on-your-project-design}

Toutes les mesures mesurées sont affectées par la conception de votre projet. À l’inverse, de nombreux problèmes sont mieux résolus par des modifications de conception.

Par conséquent, définissez vos mesures cibles *avant* de décider de votre conception. Cela vous permet d’optimiser votre conception en fonction de ces facteurs. Une fois votre projet développé, il sera difficile d’appliquer les principes de conception de base.

Lorsque vous créez la structure du site web, suivez la structure recommandée pour les sites web d’AEM. Assurez-vous de bien comprendre les questions et/ou principes suivants :

* comment structurer le contenu d’un site web ;
* comment fonctionnent les modèles et les composants ;
* comment fonctionne la mise en cache ;
* les impacts du contenu personnalisé ;
* comment fonctionne la fonction de recherche ;
* comment utiliser le CSS et les technologies associées pour créer un code HTML compact et non redondant.

Si vous estimez que votre conception ne suit pas les directives ou si vous vous posez des questions sur certaines implications, penchez-vous sur ces problèmes. Faites-le avant de lancer la phase de programmation ou de remplir le contenu.

### Infrastructure {#infrastructure}

Pour définir ou évaluer l’infrastructure, il convient de définir des valeurs cibles telles que :

* visiteurs et visiteuses/jour ; moyenne et pic
* accès/jour ; moyenne et pic
* nombre de pages web mises à disposition
* volume de contenu web

Selon votre situation et l’importance stratégique du site web, la définition de l’infrastructure peut vous aider à évaluer et à choisir votre infrastructure :

* nombre de serveurs ;
* nombre d’instances AEM (création et publication).

### Performances {#performance}

Plusieurs facteurs de performances peuvent être évalués :

* le temps de réponse pour des pages individuelles, en tenant compte des éléments suivants :

   * le temps de réponse dans un environnement de création ;
   * le temps de réponse dans l’environnement de publication ;

* le temps de réponse des requêtes de recherche.

Cette section peut être lue en parallèle de la section [Optimisation des performances](/help/sites-deploying/configuring-performance.md) qui répertorie les détails techniques relatifs à la mesure réelle des performances.

#### Temps de réponse pour des pages individuelles {#response-times-for-individual-pages}

L’un des problèmes majeurs est le temps que met votre site web pour répondre aux requêtes des visiteurs et visiteuses.

Bien que cette valeur varie pour chaque requête, une valeur cible moyenne peut être définie. Une fois que cette valeur s’est avérée à la fois réalisable et gérable, elle peut être utilisée pour surveiller les performances du site web et indiquer le développement de problèmes potentiels.

Cibles différentes sur les environnements de création et de publication

Les temps de réponse que vous visez sont différents dans les environnements de création et de publication, reflétant l’audience cible :

* **Environnement de création**

  Cet environnement est utilisé par les auteurs et autrices qui saisissent et mettent à jour du contenu. Il doit donc :

   * répondre aux besoins de quelques utilisateurs et utilisatrices qui génèrent un grand nombre de requêtes lors de la mise à jour de pages de contenu et les éléments individuels de ces pages ;
   * être aussi rapide que possible afin d’optimiser leur productivité pour intégrer du contenu à votre site web.

* **Environnement de publication**

  Cet environnement intègre le contenu que vous mettez à la disposition de vos utilisateurs et utilisatrices :

   * la vitesse reste essentielle, mais elle est souvent plus faible qu’un environnement de création ;
   * d’autres mécanismes d’amélioration des performances sont souvent appliqués :

      * le contenu est mis en cache ;
      * l’équilibrage de charge est appliqué.

#### Définir des temps de réponse cibles {#setting-target-response-times}

Comment déterminer les temps de réponse (moyens) atteignables ? La question et la réponse sont souvent une question d’expérience :

* l’expérience sur votre site web ;
* l’expérience avec AEM ;
* l’identification des pages complexes dont les temps de réponse sont supérieurs à la moyenne (ces pages doivent être optimisées individuellement, si possible).

Toutefois, dans des circonstances contrôlées, les directives suivantes peuvent être appliquées :

* 70 % des demandes de pages doivent répondre en moins de 100 ms.
* 25 % des demandes de pages doivent répondre en moins de 100 à 300 ms.
* 4 % des demandes de pages doivent répondre en moins de 300 à 500 ms.
* 1 % des demandes de pages doivent répondre en moins de 500 à 1 000 ms.
* Aucune page ne doit avoir de temps de réponse de plus d’une seconde.

Les chiffres ci-dessus supposent les conditions suivantes :

* mesures prises lors de la publication (aucun environnement de création et/ou surcharge CFC) ;
* mesures prises sur le serveur (pas de surcharge réseau)
* pas de mise en cache (pas de cache de sortie AEM, pas de cache du Dispatcher)
* uniquement pour les éléments complexes présentant de nombreuses dépendances (HTML, JS, PDF...)
* pas d’autre charge sur le système

Il existe plusieurs mécanismes permettant de surveiller les temps de réponse :

* **Surveillance des temps de réponse avec le request.log AEM**

  Le journal des requêtes est un point de départ intéressant pour l’analyse de performances. Entre autres informations, vous pouvez consulter les temps de réponse des requêtes individuelles. Voir [Optimisation des performances](/help/sites-deploying/configuring-performance.md) pour plus d’informations.

* **Surveillance des temps de réponse avec des commentaires HTML**

  Les commentaires HTML peuvent être utilisés pour inclure des informations sur le temps de réponse dans la source de chaque page :

  `</body> </html>v <-- Page took 58 milliseconds to be rendered by the server --> Response times for search requests`

#### Requêtes de recherche {#search-requests}

Les requêtes de recherche peuvent avoir un impact significatif sur votre site web à différents niveaux :

* Temps de réponse de la recherche réelle

   * Une fonction de recherche rapide est un objectif de qualité pour votre site web.

* Impact sur les performances générales

   * Lorsqu’une fonction de recherche doit analyser des sections du contenu (potentiellement importantes), ou analyser un index spécifiquement extrait, cette fonctionnalité peut avoir un impact sur les performances de l’ensemble du système si elle n’est pas optimisée.

La définition de cibles pour les requêtes de recherche est, encore une fois, une question d’expérience dépendant des éléments suivants :

* expérience d’AEM
* une évaluation de la fréquence d’utilisation de la recherche par rapport à d’autres objectifs ;
* votre gestionnaire de persistance ;
* votre index de recherche ;
* la complexité de votre fonction de recherche ; une fonction de recherche de base qui permet d’entrer un terme de recherche est plus rapide qu’une recherche avancée qui permet à l’utilisateur ou à l’utilisatrice de créer des instructions de recherche complexes à l’aide de AND/OR/NOT.

Ces requêtes de recherche doivent être prévues et intégrées dès le début de votre projet. Les mécanismes de surveillance disponibles sont les suivants :

* **Surveillance des temps de réponse de la recherche avec le fichier request.log d’AEM**

  Là encore, le fichier request.log peut être utilisé pour surveiller les temps de réponse des requêtes de recherche. Voir [Optimisation des performances](/help/sites-deploying/configuring-performance.md) pour plus d’informations.

* **Mécanismes programmés pour mesurer les temps de réponse des recherches**

  Pour personnaliser les informations que vous collectez sur les requêtes de recherche et leurs performances, il est recommandé d’inclure la collecte d’informations dans le code source de votre projet. Voir [Optimisation des performances](/help/sites-deploying/configuring-performance.md) pour plus d’informations.

### Simultanéité {#concurrency}

Mettez votre site web à la disposition de certains utilisateurs ou utilisatrices, et visiteurs ou visiteuses, dans les environnements de création et de publication. Les nombres sont souvent plus élevés que ceux que vous utilisiez lors des tests, mais aussi fluctuants et difficiles à prédire. Concevez votre site web pour un nombre moyen d’utilisateurs ou utilisatrices, et de visiteurs ou visiteuses, simultané(e)s sans remarquer d’impact négatif sur les performances. Une fois de plus, utilisez le fichier `request.log` pour effectuer des tests de simultanéité. Voir [Optimisation des performances](/help/sites-deploying/configuring-performance.md) pour plus d’informations.

Les cibles pour le nombre d’utilisateurs ou utilisatrices simultané(e)s dépendent du type d’environnement :

* **Environnement de création**

   * Généralement, le nombre d’utilisateurs simultanés peut être estimé avec précision. Vous pouvez savoir combien d’auteurs et autrices vous avez au total, bien que tous et toutes ne soient (probablement) pas actifs ou actives en même temps.

* **Environnement de publication**

   * L’environnement de publication est plus difficile à prédire. Vous devez donc sélectionner une valeur cible. Là encore, elle doit être basée sur l’expérience de votre site web actuel et sur des attentes réalistes de votre nouveau site web.
   * Les événements spéciaux (par exemple, lorsque vous publiez du nouveau contenu populaire) peuvent dépasser les attentes, voire même les capacités (comme cela est parfois rapporté dans la presse lorsque des billets pour certains événements sont mis en vente).

### Capacité et volume {#capacity-and-volume}

Avant de discuter des mesures connexes, une définition rapide des termes :

* **Volume**

   * La quantité en sortie qui est traitée et diffusée par le système.

* **Capacité**

   * Capacité du système à fournir le volume.
   * À chaque étape, la capacité et le volume sont mesurés différemment, comme le montre le tableau ci-dessous. Pour de meilleures performances, assurez-vous que la capacité correspond au volume à chaque étape et que la capacité et le volume sont partagés à l’échelle de toutes les étapes. Par exemple, vous pouvez calculer la navigation sur l’ordinateur client ou la mettre dans le cache, au lieu de la calculer sur le serveur pour chaque requête.

* **Capacité et volume**

  | Quoi / Où | Capacité | Volume |
  |---|---|---|
  | Client | Puissance de calcul de l’ordinateur de l’utilisateur ou utilisatrice. | Complexité de la mise en page. |
  | Réseau | Bande passante réseau. | Taille de la page (code, images, etc.). |
  | Cache du Dispatcher | Mémoire serveur du serveur Web (mémoire principale et disque dur). | Serveur web (mémoire principale et disque dur). Nombre et taille des pages mises en cache. |
  | Cache de sortie | Mémoire serveur du serveur AEM (mémoire principale et disque dur). | Nombre et taille des pages dans le cache de sortie, et nombre de dépendances par page. Le cache du Dispatcher réduit ce volume. |
  | Serveur web | Puissance de calcul du serveur Web. | Nombre de requêtes. La mise en cache réduit ce volume. |
  | Modèle | Puissance de calcul du serveur web. | Complexité des modèles. |
  | Référentiel | Performances du référentiel. | Nombre de pages chargées à partir du référentiel. |

### Autres mesures {#other-metrics}

Les sections précédentes détaillent les principales mesures à définir.

En fonction de vos besoins spécifiques, il peut s’avérer utile de définir des mesures supplémentaires, soit isolément, soit en tenant compte des classifications ci-dessus.

Cependant, il est préférable de disposer d’un petit ensemble de mesures principales précises qui fonctionnent facilement et de manière fiable, plutôt que d’essayer de mesurer et de définir chaque aspect de votre site web. Par sa nature même, votre site web commence à changer et à évoluer lorsqu’il est transmis à vos utilisateurs et utilisatrices.

## Sécurité {#security}

La sécurité est cruciale et présente un défi toujours plus grand. Il ***doit*** être considéré et prévu dès les premières étapes de votre projet.

La [liste de contrôle de sécurité](/help/sites-administering/security-checklist.md) décrit les mesures à prendre pour s’assurer que votre installation d’AEM est sécurisée lors de son déploiement. D’autres aspects liés à la sécurité sont traités dans les sections [Sécurité (lors du développement)](/help/sites-developing/security.md) et [Administration des utilisateurs et sécurité](/help/sites-administering/security.md).

## Tâches parallèles et itératives {#parallel-and-iterative-tasks}

>[!NOTE]
>
>Les éléments suivants :
>
>* offrent un aperçu de la *première* implémentation d’un projet AEM ;
>* sont conçus comme un aperçu abstrait ; voir la [Liste de contrôle du projet](/help/managing/best-practices.md) pour des phases/jalons/tâches spécifiques.
>* Toutes les échelles de temps sont théoriques.
>

Pour une nouvelle implémentation d’un projet AEM standard, tenez compte des tâches suivantes :

* Transfert à partir du processus de vente.
* Implémentation de l’application cliente (**Développement**).
* Installation et configuration de l’infrastructure (et des processus associés) sur le site client (**Infrastructure**).
* Création (ou migration) du contenu (**Contenu**).
* Transfert aux opérations (**Maintenance/assistance**).
* Versions de suivi.

![chlimage_1-2](assets/chlimage_1-2.png)

Pour tous les aspects, il est recommandé d’utiliser une approche itérative :

![chlimage_1-3](assets/chlimage_1-3.png)

>[!NOTE]
>
>Pour permettre l’optimisation et la formation des utilisateurs et utilisatrices dans des conditions réalistes dans l’environnement de production, divisez le lancement du projet en **Essai-pilote** (disponibilité réduite, itérations multiples) et **Lancement officiel** (disponibilité complète - En direct).

>[!NOTE]
>
>Voir la [Liste de contrôle du projet](/help/managing/best-practices.md) pour obtenir des exemples de tâches que vous devez effectuer (ou évaluer) pendant le cycle de vie de votre projet.

Voici quelques points à noter pour chaque catégorie :

* **Développement**

   * Définissez d’abord l’architecture de base.
   * Utilisez plusieurs itérations (sprints) pour le développement :

      * Le premier sprint correspond au premier cycle de développement complet.
      * Le premier sprint entraîne le premier déploiement dans votre environnement de test.
      * Chaque sprint a un résultat exécutable.
      * Chaque sprint reçoit une approbation client (minimum de test structuré avec commentaires).

   * Planifiez l’éventualité d’une mise à jour de la version d’AEM disponible au cours du projet.
   * Planifiez les tests et l’optimisation lors des sprints.
   * Planifiez les phases de stabilisation et d’optimisation.
   * Créez un journal des éléments à planifier pour les prochaines versions.
   * Planifiez la prise en charge et la participation des partenaires.

* **Infrastructure**

   * Définissez d’abord l’architecture de base :

      * Définissez les exigences de performances.
      * Définissez les objectifs de performances (cela signifie que vous devez définir clairement les attentes).
      * Définissez l’architecture du matériel et de l’infrastructure, y compris le dimensionnement.
      * Définissez le déploiement.

   * Utilisez plusieurs itérations. Pour la préparation du premier sprint et de la configuration initiale, préparez les éléments suivants :

      * Environnement de développement.
      * Processus de développement.
      * Environnement de test.
      * Processus de déploiement (y compris la gestion de la configuration).

   * Planifiez plusieurs tests de chargement.
   * Planifiez les tests et l’optimisation lors des sprints.
   * Planifiez une phase de stabilisation et d’optimisation.
   * Effectuez le déploiement dans l’environnement de production le plus tôt possible (laissez l’équipe d’exploitation configurer le système pour acquérir de l’expérience).
   * Utilisez aussi tôt que possible les utilisateurs et utilisatrices nommés et les rôles définis.
   * Planifiez les formations (formation des administrateurs et administratrices, par exemple).
   * Planifiez le transfert vers les opérations.

* **Contenu**

   * L’architecture de base :
      * Permet d’orienter la hiérarchie du contenu.
      * Permet de définir le concept du contenu.
      * Définit l’utilisation et la mise en page MSM.
      * Définit les rôles, les groupes, les workflows et les autorisations.
   * Déterminez si la création de pages hors ligne est utile.
   * Planifiez la création précoce des premières pages et du contenu (à utiliser dans les tests et dans les commentaires).
   * Planifiez la migration du contenu existant.
   * Planifiez la « migration interne au sprint » après la refactorisation.
   * Planifiez le « burndown de contenu » (plan du site pour le contenu de mise en ligne).

## Estimation du temps et de l’effort {#estimating-time-and-effort}

En fonction de la liste des tâches qui en résulte, vous pouvez ensuite effectuer des estimations initiales du temps et de l’effort nécessaires pour les définitions de tâches (de haut niveau). Ces estimations doivent inclure une indication de qui (client ou partenaire) fait quoi et quand.

La liste suivante présente les approximations standard et les corrélations d’effort impliquées et, par conséquent, les coûts :

>[!CAUTION]
>
>Ces chiffres ne peuvent être utilisés que pour les estimations initiales. Un développeur ou une développeuse AEM expérimenté(e) doit effectuer l’analyse détaillée.

| Phase | Effort |
|---|---|
| Développement | On estime qu’approximativement 2 à 4 heures de travail pour chaque nœud de composant sont nécessaires pour couvrir toutes les exigences de développement. |
| Test du développeur | 15 % du développement |
| Suivi | 10 % du développement |
| Documentation | 15 % du développement |
| Documentation JavaDoc | 10 % du développement |
| Correction de bogues | 15 % du développement |
| Gestion de projets | 20 % des coûts du projet alloués à la gestion et à la gouvernance continues du projet |

Une planification détaillée peut ensuite établir un lien entre les ressources disponibles ou nécessaires, les échéances et les coûts.

## Architecture de référence {#reference-architecture}

L’architecture de référence est proposée pour fournir une solution de modèle pour l’architecture AEM. L’architecture de référence résout les problèmes courants rencontrés dans les systèmes d’entreprise, notamment l’évolutivité, la fiabilité et la sécurité.

Les mesures de site suivantes doivent être définies :

| Classification | Définition |
|---|---|
| Nombre de sites Internet |  |
| Nombre de sites intranet |  |
| Nombre de bases de code (par exemple, si elles sont différentes pour Internet et l’intranet) |  |
| Nombre de pages individuelles |  |
| Nombre de visites du site par jour |  |
| Nombre de pages vues par jour |  |
| Volume (en Go) de transfert de données par jour |  |
| Nombre d’utilisateurs simultanés (groupe d’utilisateurs fermé) |  |
| Nombre de visiteurs simultanés (publication) |  |
| Nombre d’auteurs simultanés |  |
| Nombre d’auteurs enregistrés |  |
| Nombre d’activations de page par jour de travail |  |
| Nombre d’activations de page lors du déploiement |  |

## Présentation des outils potentiels {#overview-of-potential-tools}

La liste suivante est fournie pour vous informer des outils qui peuvent être utilisés. Il s’agit d’une simple introduction et non d’une liste de recommandations exhaustive, elle ne doit pas vous dissuader d’utiliser d’autres outils.

<table>
 <tbody>
  <tr>
   <td><strong>Produit</strong></td>
   <td><strong>Description</strong></td>
  </tr>
  <tr>
   <td>AEM</td>
   <td><p>AEM fournit tout un éventail d’outils pour vous aider à surveiller, tester, étudier et déboguer votre application, notamment :</p>
    <ul>
     <li><a href="/help/sites-developing/developer-mode.md">Mode Développeur</a></li>
     <li>La <a href="/help/sites-developing/hobbes.md">Console de test</a></li>
     <li><a href="/help/sites-administering/operations-dashboard.md">Tableau de bord des opérations</a></li>
     <li><a href="/help/sites-authoring/content-insights.md">Content Insight</a></li>
     <li>L’<a href="/help/sites-authoring/author-environment-tools.md#content-tree">Arborescence de contenu</a></li>
    </ul> </td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Selenium</td>
   <td><a href="https://www.selenium.dev/">Selenium</a> est un outil de test en open-source. Les tests s’exécutent directement dans le navigateur en émulant la façon dont les utilisateurs travaillent.</td>
  </tr>
  <tr>
   <td>Microsoft® Project </td>
   <td>Outil de gestion de projet couramment utilisé.</td>
  </tr>
  <tr>
   <td>Jira</td>
   <td><a href="https://www.atlassian.com/software/jira">Jira</a> est un outil en open-source destiné au suivi et à la gestion des détails de vos bogues logiciels. Vous pouvez appliquer des workflows aux détails des bogues, selon vos besoins.</td>
  </tr>
  <tr>
   <td>Git</td>
   <td><a href="https://git-scm.com/">Git</a> est un logiciel de contrôle des révisions.</td>
  </tr>
  <tr>
   <td>Eclipse</td>
   <td><p>Eclipse est un environnement de développement intégré en open-source, composé de différents projets. Il se concentre sur la création d’une plateforme de développement ouverte composée de frameworks, d’outils et d’environnements d’exécution extensibles pour la création, le déploiement et la gestion de logiciels tout au long de leur cycle de vie.</p> <p>Consultez <a href="/help/sites-developing/howto-projects-eclipse.md">Développement de projets AEM à l’aide d’Eclipse</a> pour plus d’informations.</p> </td>
  </tr>
  <tr>
   <td>IntelliJ</td>
   <td><p>Un environnement de développement intégré professionnel (et pouvant donc engendrer des coûts de licence) offrant une gamme complète de fonctions. </p> <p>Consultez <a href="/help/sites-developing/ht-intellij.md">Développement de projets AEM à l’aide d’IntelliJ IDEA</a> pour plus d’informations.</p> </td>
  </tr>
  <tr>
   <td>Maven</td>
   <td><a href="https://maven.apache.org/">Maven</a> est un outil pour vous aider à comprendre et à gérer vos projets logiciels et à gérer le processus de conception d’un projet (qu’il s’agisse de la partie logicielle ou de la documentation).</td>
  </tr>
 </tbody>
</table>

## Informations complémentaires {#further-reading}

En outre, les sections suivantes présentent un intérêt particulier :

* [Prise en main](/help/sites-deploying/deploy.md#getting-started)
* [Exigences techniques](/help/sites-deploying/technical-requirements.md)
* [Surveillance et maintenance de votre instance](/help/sites-deploying/monitoring-and-maintaining.md)

### Bonnes pratiques {#best-practices}

Adobe fournit d’autres bonnes pratiques pour toutes les phases et audiences :

* [Déploiement](/help/sites-deploying/best-practices.md)
* [Création](/help/sites-authoring/best-practices.md)
* [Administration](/help/sites-administering/administer-best-practices.md)
* [Développement](/help/sites-developing/best-practices.md)
* [Gestion de projets](/help/managing/best-practices.md)
