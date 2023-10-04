---
title: 'Gestion des projets : liste de contrôle des meilleures pratiques'
description: La gestion d’un projet de mise en œuvre d’Adobe Experience Manager (AEM) nécessite planification et compréhension. Les listes de contrôle de projet sont conçues comme un ensemble de bonnes pratiques pour la diffusion du projet. Elles vous guident tout au long du cycle de vie du projet et vous permettent de surveiller de haut niveau votre état.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: managing-checklist, introduction
content-type: reference
docset: aem65
exl-id: 94b91996-d2b2-4d4a-b770-334cfa2dc0b7
source-git-commit: 5bdf42d1ce7b2126bfb2670049deec4b6eaedba2
workflow-type: tm+mt
source-wordcount: '3240'
ht-degree: 12%

---

# Gestion des projets : liste de contrôle des meilleures pratiques{#managing-projects-best-practices-checklist}

La gestion d’un projet pour mettre en oeuvre Adobe Experience Manager (AEM) nécessite une planification et une compréhension afin que vous soyez conscient des problèmes et des décisions (associées) que vous devez prendre, avant et pendant la mise en oeuvre de votre projet.

Pour vous aider, les bonnes pratiques sont les suivantes :

* Un [liste de contrôle interactive](/help/managing/best-practices-checklist.md) qui vous permet de suivre et de surveiller vos progrès grâce à ces bonnes pratiques.

   * Définit les entrées et les livrables en fonction de la phase, du jalon et du personnage.
   * Fournit des aperçus automatisés (qualité, intégrité et exhaustivité) pour indiquer la progression et l’intégrité du projet.

* Documentation basée sur la variable [liste de contrôle](/help/managing/best-practices-checklist.md) qui détaille :

   * l’analyse de [pulsation du projet](#projectheartbeat) ;
   * l’aperçu du [Statut par rôle](#status-by-role) ;
   * [Phases et jalons](#phases-and-milestones).
   * [Persona clé](#persona) et leur participation à chaque étape (pertinente).
   * un [glossaire](/help/managing/best-practices-glossary.md) des [documents et éléments livrables requis](#required-documents-and-deliverables).

* [Référence supplémentaire](/help/managing/best-practices-further-reference.md) matériel pour fournir plus de détails sur des domaines spécifiques.

## Tableau de bord de pulsation du projet {#project-heartbeat-dashboard}

La variable **Pulsation du projet** La feuille de calcul offre un aperçu graphique des mesures critiques pour votre projet :

* **Qualité de la phase**

   * Indique la qualité de la variable [Documents requis et éléments livrables](#required-documents-and-deliverables) dans l’ensemble du projet.

* **État de la phase**

   * Indicateur d’état de haut niveau pour votre projet ; utile pour mettre en évidence les zones qui peuvent être à risque.

* **Complétude de la phase**

   * À tout moment pendant le projet, cela indique combien de temps a déjà été terminé pour chaque phase de votre projet.

## État par rôle {#status-by-role}

La variable **État par rôle** La feuille de calcul affiche une ventilation détaillée de [**Santé**, **Qualité et **Complétude**](#projectheartbeat) par **[Phase](#phases-and-milestones)** et **[Persona](#persona)**.

## Phases et jalons {#phases-and-milestones}

Le plan de projet est divisé en phases distinctes (de haut niveau).

Chaque phase contient ses propres jalons. Pour chaque [personnage](#persona) (ou rôle), les jalons pertinents sont répertoriés, ainsi que les documents qui sont requis pour générer les éléments livrables définis.

>[!NOTE]
>
>Il n’existe pas de relation directe 1:1 entre les documents requis et les éléments livrables.

### Préparation {#preparation}

La préparation de votre projet constitue la base de l’ensemble du projet. Définissez des exigences clés ainsi que des objectifs et des attentes clairs pour les éléments suivants :

* **Fonction commerciale**

   * Les raisons fondamentales et la justification de la réalisation du projet.

* **Portée et planification**

   * Une portée de base et un calendrier approximatif doivent être mis à disposition pour définir ce qui est nécessaire et dans quel délai ; si cela permet de clarifier la situation, vous pouvez également définir ce qui se trouve en dehors du champ d’application.

La façon dont vous préparez, planifiez et exécutez votre projet et mettez en oeuvre votre solution est affectée par les restrictions que vous opérez. Par exemple, budget fixe, calendrier fixe, quantité de contenu, qualité requise.

Comme toujours, l’ajustement de l’un des facteurs a un impact sur les autres. Par exemple, réduire le temps, mais exiger le même niveau de qualité augmentera probablement le prix tout en réduisant la quantité de contenu que vous pouvez traiter. Le budget est souvent un facteur clé, de sorte que de telles relations ne peuvent être oubliées.

Les quatre facteurs :

![projectphases_fourphases](assets/projectphases_fourphases.png)

#### Jalons {#milestones}

* **Validation**

  Au cours de cette phase, vous devez valider et confirmer les objectifs du projet, par exemple :

   * Que voulez-vous réaliser/fournir ?
   * Qui en bénéficie ?
   * Quelle est la portée ?

      * S’il aide à clarifier la situation, vous pouvez également définir ce qui se trouve en dehors du champ d’application.

   * Comment définissez-vous le succès ?
   * Comment mesurez-vous le succès ?
   * Quelles sont les exigences, commerciales et techniques ?
   * Existe-t-il des systèmes hérités à remplacer et, dans l’affirmative, existe-t-il des données à migrer ?
   * Qui est impliqué ?
   * Comment mesurez-vous le progrès ?
   * À quelle fréquence passez-vous en revue les progrès au cours de la vie du projet ?

* **Budget**

  Avant de démarrer un projet, vous avez besoin d’une estimation fiable et réaliste de ce qu’il coûte de mettre en oeuvre :

   * Utilisez les informations du jalon de validation comme base des estimations.
   * Soyez réaliste dans vos estimations.
   * Tenez compte des directives, processus ou restrictions du client et respectez-les.
   * Tenez compte des éventualités et des processus d&#39;examen si un examen ou une amélioration du budget est nécessaire ultérieurement.
   * N&#39;oubliez pas que les coûts peuvent revêtir de nombreuses formes telles que les achats, l&#39;utilisation des ressources et les frais, entre autres.

### Planification {#planning}

La planification du projet consolide la préparation. Vous devriez commencer à transformer les objectifs et les attentes en une feuille de route bien définie, composée de tâches concrètes, liées par une communication claire, avec des révisions rigoureuses pour mesurer les progrès.

#### Jalons {#milestones-1}

* **Transfert**

  Une remise nette permet de s’assurer que les personnes ou les groupes appropriés sont conscients de leurs responsabilités au sein du projet.

  Des détails complets doivent être fournis/générés pour s’assurer qu’ils comprennent pleinement tous les aspects pertinents, y compris la feuille de route, la portée, les objectifs, les exigences et les indicateurs clés de performance.

* **Évaluation des risques**

  Pour éviter des surprises déplaisantes, utilisez l’évaluation des risques pour identifier et quantifier les risques potentiels, ainsi que leur impact et leur probabilité.

  Cela doit être fait au début du cycle de vie du projet pour s’assurer que toutes les vulnérabilités sont identifiées et évaluées. En fonction des résultats, vous pouvez signaler à vos parties prenantes si toutes les exigences peuvent être mises en oeuvre et, au besoin, s’il est possible de planifier les actions appropriées à entreprendre et à suivre.

* **Communication**

  La communication est toujours essentielle au succès d’un projet. Communiquez clairement et efficacement pour vous assurer que chacun :

   * Utiliser les mêmes objectifs de base
   * À partir de la même base d’informations
   * Avec les mêmes canaux

* **Démarrage désactivé**

  La réunion de coup d’envoi permet de signifier le début du projet. C’est une bonne occasion pour :

   * Invitez toutes les parties intéressées (ou au moins les représentants de groupes).
   * Présenter des faits clés sur le projet.
   * Répondez aux questions.
   * Assurez-vous que chacun dispose de la même base de connaissances.
   * Obtenez l&#39;engagement de tous ceux qui seront impliqués - cela devra être gagné.

      * En impliquant les principaux acteurs (y compris les auteurs potentiels) dès le début du projet, vous augmentez vos chances d&#39;obtenir leur engagement dans le projet.

### Préparation du développement {#development-preparation}

La planification du développement est essentielle pour vous assurer que votre projet est construit sur une conception solide par une équipe qui possède les connaissances requises.

#### Jalons {#milestones-2}

* **Équipe de développement en état de préparation et formée**

  Avant de commencer un projet, vous devez vous assurer que votre équipe de développement dispose d’un personnel adéquat et que tous les membres de l’équipe sont formés pour la tâche en cours.

* **Architecture de contenu**

  L’architecture de contenu définit et décrit l’architecture future du contenu, notamment :

   * Arborescence de contenu, y compris les ressources
   * Les structures de base, y compris les campagnes, etc.
   * Structures multisites et multilingues (MSM, Traduction, etc.)
   * Contenu pris en charge (y compris les balises et les concepts de balisage)
   * Stratégies de mise en cache et de réutilisation du contenu

* **Architecture du système**

  L’architecture du système définit la vision conceptuelle de votre système, notamment (entre autres informations) :

   * [Structure du système](/help/sites-deploying/recommended-deploys.md#deployment-scenarios) pour tous les environnements requis
   * Sous-systèmes
   * Systèmes tiers
   * Interfaces ; matériel, logiciel et interaction humaine
   * les serveurs pour chaque environnement, consultez les [Exigences techniques](/help/sites-deploying/technical-requirements.md) et les [Consignes de dimensionnement du matériel](/help/managing/hardware-sizing-guidelines.md) ;

   * Processus pour chaque environnement ; par exemple, exigences de déploiement et de maintenance
   * Activités de maintenance (GC de banque de données, optimisation TarPM, etc.)
   * Mise en cache du [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=fr)
   * [Mise en grappe de la publication/création partagée](/help/sites-deploying/recommended-deploys.md#deployment-scenarios)
   * Performances côté client (minification JS, concat, sprites CSS, nombre total de requêtes http, etc.)

* **Architecture d’application**

  L’architecture de l’application définit et décrit le comportement des applications proposées.

  Il se concentre sur :

   * Comment ils interagissent entre eux et avec les utilisateurs.
   * Données à consommer et à produire par les applications, plutôt que leur structure interne.

  Les définitions doivent couvrir :

   * Structure de code de base du projet
   * Artefacts de code (lots, packages, etc.)
   * Ventilations des modèles/composants et de leurs relations
   * Détails de haut niveau sur les personnalisations requises (des superpositions spécifiques suivent ultérieurement)
   * Conception des workflows requis par la solution (par exemple, création de contenu, approbation, publication, transformations, importations et exportations)
   * Prise en compte spéciale pour tout module complexe, tel que MSM, Commerce, intégration tierce

* **Intégration système**

  L’intégration du système requiert que vous planifiiez (puis mettiez en oeuvre) :

   * Comment tous les sous-systèmes et [intégrations de solutions](/help/sites-administering/integration.md) sont regroupées pour fonctionner comme un système unique et cohérent.
   * Comment les systèmes tiers sont-ils intégrés, ainsi que toute considération spéciale, telle que hors ligne/en ligne, côté client/côté navigateur ou la gestion des basculements lorsqu’un système tiers est hors service ?

* **Concept de test**

  Avant de commencer le développement, vous devez élaborer un concept détaillé et complet de tous les [test](/help/sites-developing/planning.md) conditions requises pour votre projet.

  Cela devrait inclure (entre autres) :

   * Détails de tous les tests à effectuer
   * Préparation de tout contenu requis pour ces tests
   * Informations sur les outils de test à utiliser
   * Une indication de haut niveau de qui sera impliqué dans les tests, en particulier les groupes en dehors de l’équipe d’assurance qualité
   * Détails de l’automatisation des tests ; par exemple, avec Selenium ou le mode AEM Développeur

* **Conception d’expérience**

  La conception de l’expérience (XD) implique la conception de l’expérience utilisateur pour votre solution.

  L’expérience utilisateur doit être analysée et développée pour les auteurs et les utilisateurs finaux de votre site web.

* **Configuration de l’assistance**

  Avant le développement, tous les processus de prise en charge nécessaires au déploiement, à la publication, au test et aux problèmes de rapports doivent être mis en place.

  Voir aussi [Portail d’assistance à l’Adobe](https://experienceleague.adobe.com/?support-solution=General&amp;lang=fr&amp;support-tab=home#support).

### Planification des opérations et opérations {#operations-planning-and-operations}

De la même manière, les opérations doivent être correctement planifiées pour vous assurer que vous disposez des environnements dont vous avez besoin, pour toutes les étapes du cycle de vie du projet. Vous avez également besoin des processus appropriés pour les gérer.

#### Jalons {#milestones-3}

* **Autorisations**

  Vous devez planifier et mettre en oeuvre un concept de rôles et de droits pour tous les utilisateurs/groupes qui utiliseront la solution.

  Par exemple :

   * Une liste de rôles (c’est-à-dire, de groupes) avec `read`/ `write` Définitions d’accès pour chaque

   * la définition des privilèges qui affectent l’environnement de publication, par exemple, `replicate`.
   * Pour les utilisateurs qui disposent des privilèges minimaux, des workflow doivent être définis.
   * Les utilisateurs du groupe `editor` ne doivent pas disposer de droits `admin` ni faire partie du groupe `administrators`.

  Pour plus d’informations, consultez [Administration et sécurité des utilisateurs](/help/sites-administering/security.md).

* **Surveillance et maintenance**

  La surveillance et la maintenance sont des aspects essentiels pour assurer le bon fonctionnement de votre solution une fois qu’elle est activée. Pour cela, vous devez définir :

   * Éléments à surveiller
   * Tâches de maintenance, régulières et pour des cas particuliers

  Voir aussi [Surveillance et maintenance](/help/sites-deploying/monitoring-and-maintaining.md) pour plus d’informations.

* **Migration**

  Tout contenu du système hérité doit être révisé et validé pour la migration.

* **Plan de récupération**

  Assurez-vous que vous disposez d’un plan de récupération. En cas d’urgence, cette option doit être disponible pour garantir l’utilisation de l’AEM en production. Cela devrait couvrir des situations telles que la sauvegarde, la restauration, le basculement, etc.

### Développement {#development}

Le développement est une phase cruciale qui nécessite plus que du simple codage.

#### Jalons {#milestones-4}

* **Environnement de développement**

  Planifiez et documentez votre environnement de développement, notamment :

   * Architecture
   * [les outils de développement.](/help/sites-developing/dev-tools.md)

      * Un environnement type se compose des éléments suivants :

         * un système de suivi des problèmes, tel que Jira ;
         * un IDE, tel qu’Eclipse ;
         * un outil de gestion des versions, tel que Maven ;
         * un outil pour l’intégration continue, comme Jenkins ;
         * un outil de contrôle de version, tel que GIT/SVN ;
         * un gestionnaire de référentiel d’artefacts de build, par exemple Archiva/Nexus ;

   * Intégration/dépendances de logiciels tiers
   * [l’intégration/les dépendances des solutions ;](/help/sites-administering/integration.md)
   * La cadence de déploiement

* **Système de test**

  Planifiez et documentez votre environnement de test, notamment :

   * Architecture
   * Dépendances des versions de développement, y compris les versions nocturnes
   * Les possibilités ou limites du test de l’intégration/des dépendances de logiciels tiers
   * Outils de test
   * Stratégie de test automatisé

* **Système de production**

  Planifiez et documentez votre environnement de production, notamment :

   * Architecture
   * La cadence de déploiement
   * Intégration/dépendances de logiciels tiers
   * Configuration de la sécurité
   * les performances de base vérifiées par l’exécution de [tests ToughDay](/help/sites-developing/tough-day.md) sur la configuration d’exploitation ;
   * Conditions requises pour les tests de performance ; voir [Bonnes pratiques pour l’assurance qualité](/help/sites-deploying/configuring-performance.md#best-practices-for-quality-assurance)

* **Intégration**

  Planification, documenter et tester tous les aspects du système et [intégration de solution](/help/sites-administering/integration.md), notamment :

   * Une stratégie de test automatisée
   * Processus automatisés vers [déplacer les applications du développement au test, puis à la production ;](/help/managing/enterprise-devops.md#code-movement)
   * Processus automatisés vers [déplacer le contenu de la production vers le test et le développement ;](/help/managing/enterprise-devops.md#content-movement)

* **Migration**

  Planifiez, documentez et testez tous les aspects de la migration de contenu, notamment :

   * Architecture du contenu
   * Stratégie de migration

* **Communication**

  Assurez-vous que tous les membres de l’équipe et le personnel du projet sont tenus à jour, si nécessaire.

* **Documentation**

  Documentez entièrement la solution, notamment :

   * Manuel des opérations
   * Toutes les personnalisations pouvant affecter les mises à niveau
   * Notes de mise à jour

### Performances et tests {#performance-and-testing}

Une fois la nouvelle application disponible, elle doit subir des tests stricts, tant pour sa fonctionnalité que pour [performance](/help/sites-deploying/configuring-performance.md).

>[!NOTE]
>
>Toute équipe de test doit être autorisée à rester neutre et à fournir les résultats de test.
>
>Il incombe au chef de projet d’évaluer les implications des résultats et de décider des mesures à prendre.

#### Jalons {#milestones-5}

* **Test d’acceptation utilisateur final**

  [Test d’acceptation des utilisateurs](/help/sites-developing/acceptance-signoff.md) (UAT) est essentiel pour s’assurer que :

   * La solution répond aux exigences de l’utilisateur/du client.
   * Le client/les utilisateurs acceptent la solution (fonction, conception et performances)

  Il doit y avoir une liste de contrôle formalisée pour la remise aux clients ; idéalement automatisée et exécutée de nuit sur un instantané. Les résultats doivent être envoyés au chef de projet et à l’équipe de développement.

* **Tests de performance et de chargement**

  Les tests de performance et de charge permettent de s’assurer que la solution respecte les niveaux de performance requis, à des charges moyennes et de pointe.

  Pour plus d’informations sur les tests de performance, voir :

   * [Test de performance](/help/sites-deploying/configuring-performance.md)
   * [Planification et exécution des tests](/help/sites-developing/planning.md)

   * [Consignes de performances de base](/help/sites-deploying/configuring-performance.md#basic-performance-guidelines)

  >[!NOTE]
  >
  >Ce processus doit se poursuivre pendant l&#39;utilisation normale des AEM, mais ces étapes initiales sont les plus cruciales.

### Déploiement {#rollout}

Le déploiement de votre nouvelle application nécessite une planification attentive pour garantir une activation fluide. Cela inclut la confirmation d’un niveau élevé de sécurité, la formation de tous les utilisateurs potentiels et la réalisation de plusieurs exécutions préliminaires pour confirmer que tous les problèmes ont été traités.

#### Jalons {#milestones-6}

* **Préparation**

  La préparation et la planification aideront à assurer un déploiement en douceur.

* **Formation**

  Assurez-vous que tous les membres du personnel impliqués ont été formés.

  Voir [Adobe Experience Manager](https://training.adobe.com/training/courses.html#solution=adobeExperienceManager) dans le catalogue de cours.

* **Administrateurs formés**

  Assurez-vous que vos administrateurs de solution disposent des éléments suivants :

   * Formé
   * Reçu le matériel de formation approprié
   * Reçu la documentation appropriée

* **Utilisateurs formés**

  Assurez-vous que vos auteurs disposent des éléments suivants :

   * Formé
   * Reçu le matériel de formation approprié
   * Reçu la documentation appropriée ; par exemple, le Guide de l’utilisateur

* **Tests de pénétration**

  Les tests de pénétration simulent une attaque sur un système informatique afin d’identifier les éventuelles failles de sécurité.

* **Tests de pénétration/sécurité**

  Pour garantir la sécurité de votre solution, effectuez des tests de pénétration spécifiques, ainsi qu’un plus large éventail de tests de sécurité.

  Consultez la [Liste de contrôle de sécurité](/help/sites-administering/security-checklist.md) pour plus de détails.

### Activation {#go-live}

Vous voulez que votre Go Live soit aussi fluide que possible. Encore une fois, les dernières étapes doivent être planifiées pour une exécution propre.

#### Jalons {#milestones-7}

* **Préparation**

  La préparation et la planification aideront à assurer une activation fluide.

* **Sécurité**

  Confirmez la sécurité de votre solution pour les utilisateurs internes et externes et leur contenu.

* **Secours**

  Assurez-vous que tous les systèmes, procédures et mécanismes requis pour la secours sont en place avant de passer en ligne.

* **Assistance**

  Assurez-vous que les services d’assistance sont en place et prêts.

* **Transition**

  Planifiez et exécutez la transition vers votre environnement de production et vos utilisateurs.

* **Déployer**

  Préparez et exécutez vos tests de détection de fumée.

## Personne {#persona}

Les listes de contrôle sont conçues par persona. Il s’agit des rôles qui jouent un rôle important dans le cycle de vie du projet.

Il y en a aussi quelques [autre personnage](#other-persona) qui sont impliqués dans des tâches spécifiques.

### Sponsor de projet {#project-sponsor}

Le sponsor du projet est :

* Responsable de l’exécution/de la présentation de l’analyse de cas pour le projet.
* Clé pour définir et définir la portée du projet, notamment :

   * la définition et les critères de réussite
   * les principaux indicateurs de performance clés ;

* Indiquez les jalons principaux en fonction de la feuille de route du client.

### Chef de projet {#project-manager}

Le chef de projet est :

* Responsable de la diffusion globale du projet en fonction des exigences (par exemple, portée, indicateurs de performance clés, critères de réussite et définition) fournies par le sponsor du projet.
* Responsable de la définition du budget et de la dotation en ressources du projet sur la base de ce budget.
* Point de communication principal pour toutes les personnes impliquées dans le projet.

### Architecte {#architect}

L’architecte de la solution :

* est responsable de la conception de haut niveau de la solution et du système ;
* aide à définir la stratégie de mise en œuvre d’AEM Par exemple, la mise en oeuvre d’une installation en grappe ou d’une reprise à froid ou la nécessité d’un réseau de diffusion de contenu.
* Définissez également l’architecture de la solution AEM en fonction des exigences du client. Cela peut inclure le concept des rôles utilisateur (avec les droits associés), la relation entre les modèles et les composants, ou le moment où utiliser la gestion multisite.

### Analyste métier {#business-analyst}

L’analyste d’entreprise :

* est principalement chargé de rassembler et d’analyser les exigences de haut niveau, puis de les transformer en spécifications :

   * pour que le chef de projet l’utilise lors de la planification du développement.
   * pour que l’équipe de développement puisse travailler pendant la conception et le développement.

* Travaille en étroite collaboration avec le client pour analyser les exigences. Ils les comparent à :

   * La définition de la réussite.
   * Les critères de réussite.
   * IPC (basés à la fois sur les activités et les performances).

### Responsable du développement {#development-lead}

Le responsable du développement :

* est responsable de la diffusion technique du projet ;
* est chargé de sélectionner une méthodologie de développement conforme aux exigences du client ;
* élabore la stratégie de développement :

   * s’assurer qu’il est aligné sur les indicateurs clés de performance métier et de performance ;
   * prise en compte des critères et de la définition de réussite

* Travaille en étroite collaboration avec l’architecte (notamment lors de l’élaboration de la stratégie de développement pour AEM) afin de définir des aspects tels que la relation entre les modèles et les composants, la stratégie d’intégration pour les applications tierces et toute fonctionnalité spécialisée.

### Responsable de la qualité {#quality-lead}

Le prospect de qualité :

* est responsable de la qualité de la diffusion ; s’assurer qu’elle répond aux critères de réussite et aux indicateurs de performance clés définis par le client ;
* Définit les mesures de qualité, s’aligne sur toutes les parties prenantes, élabore les plans de test et s’assure qu’ils sont exécutés.
* Crée et diffuse des rapports aux parties prenantes du projet.

### Ingénieur système {#system-engineer}

L’ingénieur système :

* est responsable de la supervision de l’infrastructure du projet ;
* est responsable de :

   * la configuration des environnements de développement et de test internes ;
   * pour faire correspondre ces systèmes aux systèmes client.

* Fournit des recommandations matérielles, surveille les différentes mises en oeuvre et assure la prise en charge des opérations avant et après la mise en service.

### Responsable de la sécurité {#security-lead}

Le responsable de la sécurité :

* est responsable du concept de sécurité global de la solution, en s’assurant qu’elle est alignée sur les exigences et stratégies du client ;
* Fournit un concept de sécurité, des opérations de sécurité et des recommandations pour tout concept de sécurité matériel, tel que les zones et les pare-feu.

### Autre personnage {#other-persona}

* Parties prenantes

   * Personnes (souvent issues de l’entreprise) qui ont un intérêt (intérêt) dans le succès du projet. Ils contribuent souvent au budget.

* Légal

   * Des conseils juridiques sont nécessaires lors de la négociation de contrats.

* Formateurs

   * Selon l&#39;ampleur et la nature du projet, des formateurs spécialisés peuvent être utilisés pour développer et présenter des sessions de formation pour les groupes concernés.

* Écrivains techniques

   * Selon l’ampleur et la nature du projet, des rédacteurs techniques spécialisés peuvent être utilisés pour écrire des directives et des manuels pour des groupes spécifiques. Par exemple, un manuel de maintenance pour les administrateurs système ou un guide de l’utilisateur pour les auteurs.

* Administrateurs système

   * Responsable du fonctionnement continu du système.

* Auteurs et utilisateurs finaux

   * Les personnes qui utilisent le système pour créer et gérer le contenu de votre site web.

## Documents requis et éléments livrables {#required-documents-and-deliverables}

Les listes de contrôle couvrent les **documents requis** et les **éléments livrables** pour chaque jalon.

* Il n’existe aucune relation 1:1 entre ces deux éléments ; par exemple, un groupe de documents requis peut générer un seul livrable.
* Un livrable d’une personne peut être un document requis pour une autre personne au cours du même jalon.

### Documents requis {#required-documents}

La variable **Documents requis** sont nécessaires pour le personnage approprié lors de la production de ses éléments livrables.

Pour chaque **Document requis**, le persona doit indiquer :

* **O/N**: s’il a été reçu.
* **1-3**: une indication de la qualité du document reçu.

### Deliverables {#deliverables}

Pour chaque jalon, le personnage approprié est chargé de fournir des documents spécifiques et, par conséquent, de remplir ses responsabilités pour un jalon spécifique.

Pour chaque **Délivrés**, le persona doit indiquer :

* **O/N** : s’il est terminé.

Les éléments livrables sont souvent utilisés comme des **documents requis** pour le jalon en cours ou un jalon ultérieur.

## Bonnes pratiques connexes {#related-best-practices}

Pour connaître les bonnes pratiques en matière de déploiement, d’administration, de développement ou de création, voir :

* Autres bonnes pratiques et consignes liées à la gestion d’un projet AEM :
   * [Consignes de dimensionnement du matériel](/help/managing/hardware-sizing-guidelines.md)
   * [Opérations de développement d’entreprise (DevOps)](/help/managing/enterprise-devops.md)
   * [Bonnes pratiques de SEO et de gestion des URL](/help/managing/seo-and-url-management.md)
   * [Instructions relatives à AEM et à l’accessibilité Web](/help/managing/web-accessibility.md)
   * [Règlement général sur la protection des données](/help/managing/data-protection-and-privacy.md)* [Bonnes pratiques de déploiement et de maintenance](/help/sites-deploying/best-practices.md)
* [Bonnes pratiques d’administration](/help/sites-administering/administer-best-practices.md)
* [Bonnes pratiques de développement](/help/sites-developing/best-practices.md)
* [Bonnes pratiques de création](/help/sites-authoring/best-practices.md)

## Principale documentation {#key-documentation-areas}

* Documentation AEM
Les sections suivantes de la documentation AEM présentent un intérêt particulier (toutefois, cette liste n’est pas exhaustive) :

   * [Sécurité](/help/sites-developing/security.md)
   * [Déploiements recommandés](/help/sites-deploying/recommended-deploys.md)
   * [Opérations de développement d’entreprise (DevOps)](/help/managing/enterprise-devops.md)
   * [Dimensionnement matériel](/help/managing/hardware-sizing-guidelines.md)
   * Concepts AEM :

      * [Développement – Les principes de base](/help/sites-developing/the-basics.md)
      * [Concepts relatifs au MSM](/help/sites-administering/msm.md)
      * [Langage de modèle HTML (HTL)](https://experienceleague.adobe.com/docs/experience-manager-htl/using/overview.html?lang=fr)

* Documentation connexe

   * Adobe Experience Cloud – [Planification pour Adobe Experience Cloud](https://experienceleague.adobe.com/docs/core-services/interface/services/core-services.html)
