---
title: 'Gestion des projets : liste de contrôle des bonnes pratiques'
description: La gestion d’un projet de mise en œuvre d’Adobe Experience Manager (AEM) nécessite planification et compréhension. Les listes de contrôle de projet sont conçues comme un ensemble de bonnes pratiques pour la diffusion du projet. Elles vous guident tout au long du cycle de vie du projet et vous offrent une surveillance détaillée de votre statut.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: managing-checklist, introduction
content-type: reference
docset: aem65
exl-id: 94b91996-d2b2-4d4a-b770-334cfa2dc0b7
solution: Experience Manager, Experience Manager 6.5
feature: Compliance
role: Admin,Architect,Data Architect,Developer,Leader
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '3214'
ht-degree: 100%

---

# Gestion des projets : liste de contrôle des bonnes pratiques{#managing-projects-best-practices-checklist}

La gestion d’un projet pour mettre en œuvre Adobe Experience Manager (AEM) nécessite planification et compréhension afin que vous ayez conscience des problèmes et des décisions (associées) que vous devez prendre, avant et pendant la mise en œuvre de votre projet.

Pour vous aider, les bonnes pratiques sont les suivantes :

* Une [liste de contrôle interactive](/help/managing/best-practices-checklist.md) qui vous permet de suivre et de surveiller vos progrès grâce à ces bonnes pratiques.

   * Définit les entrées et les livrables en fonction de la phase, du jalon et du persona.
   * Fournit des aperçus automatisés (qualité, intégrité et exhaustivité) pour indiquer la progression et l’intégrité du projet.

* Documentation basée sur la [liste de contrôle](/help/managing/best-practices-checklist.md) qui détaille :

   * l’analyse de [pulsation du projet](#projectheartbeat) ;
   * l’aperçu du [Statut par rôle](#status-by-role) ;
   * les [phases et jalons](#phases-and-milestones) ;
   * le [persona clé](#persona) et sa participation à chaque étape (pertinente) ;
   * un [glossaire](/help/managing/best-practices-glossary.md) des [documents et éléments livrables requis](#required-documents-and-deliverables).

* du matériel de [référence supplémentaire](/help/managing/best-practices-further-reference.md) pour fournir plus de détails sur des domaines spécifiques.

## Tableau de bord de pulsation du projet {#project-heartbeat-dashboard}

La feuille de calcul **Pulsation du projet** offre une vue d’ensemble graphique des mesures critiques pour votre projet :

* **Qualité de la phase**

   * Indique la qualité des [Documents requis et éléments livrables](#required-documents-and-deliverables) dans l’ensemble du projet.

* **Intégrité de la phase**

   * Indicateur de statut de haut niveau pour votre projet ; utile pour mettre en évidence les zones qui peuvent être à risque.

* **Achèvement de la phase**

   * À tout moment pendant le projet, indique le niveau d’achèvement pour chaque phase de votre projet.

## Statut par rôle {#status-by-role}

La feuille de calcul **Statut par rôle** indique le détail de l’[**intégrité**, la **qualité et le **niveau d’achèvement**](#projectheartbeat) par **[phase](#phases-and-milestones)** et **[persona](#persona)**.

## Phases et jalons {#phases-and-milestones}

Le plan de projet est divisé en plusieurs phases distinctes (de haut niveau).

Chaque phase contient ses propres jalons. Pour chaque [personnage](#persona) (ou rôle), les jalons pertinents sont répertoriés, ainsi que les documents qui sont requis pour générer les éléments livrables définis.

>[!NOTE]
>
>Il n’existe pas de relation directe 1:1 entre les documents requis et les éléments livrables.

### Préparation {#preparation}

La préparation de votre projet constitue la base de l’ensemble du projet. Définissez des exigences clés ainsi que des objectifs et des attentes clairs pour les éléments suivants :

* **Arguments commerciaux**

   * Les raisons fondamentales et la justification de la réalisation du projet.

* **Portée et planning**

   * Une portée de base et un planning approximatif doivent être mis à disposition pour définir ce qui est nécessaire et dans quel délai ; si cela permet de clarifier la situation, vous pouvez également définir ce qui se trouve en dehors du champ d’application.

La façon dont vous préparez, planifiez et exécutez votre projet et mettez en œuvre votre solution est affectée par les restrictions que vous opérez. Par exemple, budget fixe, journal fixe, quantité de contenu, qualité requise.

Comme toujours, l’ajustement de l’un des facteurs a un impact sur les autres. Par exemple, réduire le délai, mais exiger le même niveau de qualité augmentera probablement le prix tout en réduisant la quantité de contenu que vous pouvez traiter. Le budget est souvent un facteur clé, de sorte que de telles relations ne peuvent être oubliées.

Les quatre facteurs :

![projectphases_fourphases](assets/projectphases_fourphases.png)

#### Jalons {#milestones}

* **Validation**

  Au cours de cette phase, vous devez valider et confirmer les objectifs du projet, par exemple :

   * Que voulez-vous réaliser/fournir ?
   * Qui en bénéficie ?
   * Quelle est la portée ?

      * Si cela aide à clarifier la situation, vous pouvez également définir ce qui se trouve en dehors de la portée.

   * Comment définissez-vous le succès ?
   * Comment mesurez-vous le succès ?
   * Quelles sont les exigences, commerciales et techniques ?
   * Existe-t-il des systèmes hérités à remplacer et, existe-t-il des données à migrer ?
   * Qui est impliqué ?
   * Comment mesurez-vous la progression ?
   * À quelle fréquence suivez-vous la progression au cours du projet ?

* **Budget**

  Avant de lancer un projet, vous avez besoin d’une estimation fiable et réaliste de ce que sa mise en œuvre coûte :

   * Utilisez les informations du jalon de validation comme base des estimations.
   * Soyez réaliste dans vos estimations.
   * Tenez compte des directives, processus ou restrictions du client ou de la cliente et respectez-les.
   * Tenez compte des éventualités et des processus d’examen si un examen ou une amélioration du budget est nécessaire ultérieurement.
   * N’oubliez pas que les coûts peuvent revêtir de nombreuses formes telles que les achats, l’utilisation des ressources et les frais, entre autres.

### Planification {#planning}

La planification du projet consolide la préparation. Vous devez ici commencer à transformer les objectifs et les attentes en une feuille de route bien définie, composée de tâches concrètes, liées par une communication claire, avec des révisions rigoureuses pour mesurer la progression du projet.

#### Jalons {#milestones-1}

* **Transfert**

  Un transfert net permet de s’assurer que les personnes ou les groupes appropriés sont conscients de leurs responsabilités au sein du projet.

  Des détails complets doivent être fournis/générés pour s’assurer qu’ils comprennent pleinement tous les aspects pertinents, y compris la feuille de route, la portée, les objectifs, les exigences et les indicateurs clés de performance.

* **Évaluation des risques**

  Pour éviter des surprises déplaisantes, utilisez l’évaluation des risques pour identifier et quantifier les risques potentiels, ainsi que leur impact et leur probabilité.

  Cela doit être fait au début du cycle de vie du projet pour s’assurer que toutes les vulnérabilités sont identifiées et évaluées. En fonction des résultats, vous pouvez signaler à vos parties prenantes si toutes les exigences peuvent être mises en œuvre et, au besoin, s’il est possible de planifier les actions appropriées à entreprendre et à suivre.

* **Communication**

  La communication est toujours essentielle au succès d’un projet. Communiquez de manière claire et efficace pour vous assurer que tout le monde :

   * Utilise les mêmes objectifs de base
   * à partir de la même base d’informations
   * avec les mêmes canaux.

* **Coup d’envoi**

  La réunion de coup d’envoi permet de signifier le début du projet. C’est une bonne occasion pour :

   * inviter toutes les parties intéressées (ou au moins les représentants et représentantes de groupes) ;
   * présenter des éléments clés sur le projet ;
   * répondre aux questions ;
   * s’assurer que chacun dispose de la même base de connaissances ;
   * obtenir l’engagement de tous ceux qui seront impliqués et le tour est joué.

      * En impliquant les principaux acteurs et actrices (y compris les auteurs et autrices potentiels) dès le début du projet, vous augmentez vos chances d’obtenir leur engagement dans le projet.

### Préparation du développement {#development-preparation}

La planification du développement est essentielle pour vous assurer que votre projet est construit sur une conception solide par une équipe qui possède les connaissances requises.

#### Jalons {#milestones-2}

* **Équipe de développement constituée et formée**

  Avant de commencer un projet, vous devez vous assurer que votre équipe de développement dispose d’un personnel adéquat et que tous les membres de l’équipe sont formés pour la tâche en cours.

* **Architecture de contenu**

  L’architecture de contenu définit et décrit l’architecture future du contenu, notamment :

   * l’arborescence de contenu, y compris les ressources ;
   * les structures de base, y compris les campagnes, etc. ;
   * les structures multisites et multilingues (MSM, traduction, etc.) ;
   * le contenu pris en charge (y compris les balises et les concepts de balisage) ;
   * les stratégies de cache et de réutilisation du contenu.

* **Architecture du système**

  L’architecture du système définit la vision conceptuelle de votre système, notamment (entre autres informations) :

   * [Structure du système](/help/sites-deploying/recommended-deploys.md#deployment-scenarios) pour tous les environnements requis
   * Sous-systèmes
   * Systèmes tiers
   * Interfaces ; interaction matérielle, logicielle et humaine
   * les serveurs pour chaque environnement, consultez les [Exigences techniques](/help/sites-deploying/technical-requirements.md) et les [Consignes de dimensionnement du matériel](/help/managing/hardware-sizing-guidelines.md) ;

   * Processus pour chaque environnement ; par exemple, exigences de déploiement et de maintenance
   * Activités de maintenance (GC de magasin de données, optimisation TarPM, etc.)
   * Mise en cache du [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=fr)
   * [Mise en grappe de la publication/création partagée](/help/sites-deploying/recommended-deploys.md#deployment-scenarios)
   * Performances côté client (minification JS, concat, sprites CSS, nombre total de requêtes http, etc.)

* **Architecture d’application**

  L’architecture de l’application définit et décrit le comportement des applications proposées.

  Elle est axée sur :

   * la manière dont elles interagissent entre elles et avec les utilisateurs et utilisatrices ;
   * les données à consommer et à produire par les applications, plutôt que leur structure interne.

  Les définitions doivent couvrir :

   * la structure de code de base du projet ;
   * les artefacts de code (bundles, packages, etc.) ;
   * les pannes des modèles/composants et de leurs relations ;
   * les détails de haut niveau sur les personnalisations requises (des superpositions spécifiques suivront ultérieurement) ;
   * la conception des workflows requis par la solution (par exemple, création de contenu, approbation, publication, transformations, imports et exports) ;
   * la considération spéciale pour tout module complexe, tel que MSM, Commerce, intégration tierce.

* **Intégration système**

  L’intégration système requiert que vous planifiiez (puis que vous mettiez en œuvre) :

   * la façon dont tous les sous-systèmes et [intégrations de solutions](/help/sites-administering/integration.md) seront rassemblés pour fonctionner comme un système cohérent ;
   * la façon dont les éventuels systèmes tiers sont intégrés, ainsi que toute considération spéciale, telle que hors ligne ou en ligne, côté client ou côté navigateur, ou encore la gestion des basculements lorsqu’un système tiers est hors service.

* **Concept test**

  Avant de commencer le développement, vous devez élaborer un concept détaillé et complet de toutes les conditions de [test](/help/sites-developing/planning.md) requises pour votre projet.

  Cela devrait inclure (entre autres) :

   * des détails de tous les tests à effectuer ;
   * une préparation de tout contenu requis pour ces tests ;
   * des informations sur les outils de test à utiliser ;
   * une indication de haut niveau sur ce qui sera impliqué dans les tests, en particulier les groupes en dehors de l’équipe d’assurance qualité ;
   * des détails sur l’automatisation des tests ; par exemple, avec Selenium ou le mode AEM Developer.

* **Conception d’expérience**

  La conception d’expérience (XD) implique la conception de l’expérience utilisateur pour votre solution.

  L’expérience utilisateur doit être analysée et développée pour les auteurs et les autrices, les utilisateurs et les utilisatrices finaux de votre site web.

* **Configuration de l’assistance**

  Avant le développement, tous les processus de prise en charge nécessaires au déploiement, à la publication, au test et aux problèmes de rapports doivent être mis en place.

  Voir aussi le [portail d’assistance Adobe](https://experienceleague.adobe.com/?support-solution=General&amp;lang=fr&amp;support-tab=home#support).

### Planification et mise en œuvre des opérations {#operations-planning-and-operations}

De la même manière, les opérations doivent être correctement planifiées pour vous assurer que vous disposez des environnements nécessaires pour toutes les étapes du cycle de vie du projet. Vous avez également besoin des processus appropriés pour les gérer.

#### Jalons {#milestones-3}

* **Autorisations**

  Vous devez planifier et mettre en œuvre un concept de rôles et de droits pour tous les utilisateurs/utilisatrices/groupes qui utiliseront la solution.

  Par exemple :

   * la liste des rôles (c’est-à-dire, des groupes) avec les définitions d’accès en `read`/`write` pour chacun d’eux ;

   * la définition des privilèges qui affectent l’environnement de publication, par exemple, `replicate`.
   * Pour les utilisateurs qui disposent des privilèges minimaux, des workflow doivent être définis.
   * Les utilisateurs du groupe `editor` ne doivent pas disposer de droits `admin` ni faire partie du groupe `administrators`.

  Pour plus d’informations, consultez [Administration et sécurité des utilisateurs](/help/sites-administering/security.md).

* **Surveillance et maintenance**

  La surveillance et la maintenance sont des aspects essentiels pour assurer le bon fonctionnement de votre solution une fois lancée. Pour cela, vous devez définir :

   * Les éléments à surveiller
   * Les tâches de maintenance : les tâches régulières et les tâches particulières

  Voir aussi [Surveillance et maintenance](/help/sites-deploying/monitoring-and-maintaining.md) pour plus d’informations.

* **Migration**

  Tout contenu du système hérité doit être revu et validé pour la migration.

* **Plan de récupération**

  Assurez-vous que vous disposez d’un plan de récupération. En cas d’urgence, cette option doit être disponible pour garantir l’utilisation d’AEM en production. Cela devrait couvrir des situations telles que la sauvegarde, la restauration, le basculement, etc.

### Développement {#development}

Le développement est une phase cruciale qui nécessite plus que du simple codage.

#### Jalons {#milestones-4}

* **Environnement de développement**

  Planifiez et documentez votre environnement de développement, notamment :

   * Architecture
   * [les outils de développement.](/help/sites-developing/dev-tools.md)

      * Un environnement type se compose des éléments suivants :

         * un système de suivi des problèmes, tel que Jira ;
         * un IDE, tel qu’Eclipse ;
         * un outil de gestion de projets, tel que Maven ;
         * un outil pour l’intégration continue, comme Jenkins ;
         * un outil de gestion de versions, tel que GIT/SVN ;
         * un gestionnaire de référentiel d’artefacts de projets, tel qu’Archiva/Nexus ;

   * l’intégration/les dépendances de logiciels tiers ;
   * [l’intégration/les dépendances des solutions ;](/help/sites-administering/integration.md)
   * la cadence de déploiement.

* **Système de test**

  Planifiez et documentez votre environnement de test, notamment :

   * Architecture
   * les dépendances des versions de développement, y compris les versions nocturnes ;
   * les possibilités ou limites du test de l’intégration/des dépendances de logiciels tiers ;
   * les outils de test ;
   * la stratégie de test automatisé.

* **Système de production**

  Planifiez et documentez votre environnement de production, notamment :

   * Architecture
   * la cadence de déploiement.
   * l’intégration/les dépendances de logiciels tiers ;
   * la configuration de la sécurité ;
   * les performances de base vérifiées par l’exécution de [tests ToughDay](/help/sites-developing/tough-day.md) sur la configuration d’exploitation ;
   * les conditions requises pour les tests de performance ; voir [Bonnes pratiques pour l’assurance qualité](/help/sites-deploying/configuring-performance.md#best-practices-for-quality-assurance).

* **Intégration**

  Planifiez, documentez et testez tous les aspects du système et de l’[intégration de solution](/help/sites-administering/integration.md), notamment :

   * une stratégie de test automatisée ;
   * des processus automatisés pour [déplacer les applications de l’environnement de développement à l’environnement de test, puis à celui de production ;](/help/managing/enterprise-devops.md#code-movement)
   * des processus automatisés pour [déplacer le contenu de l’environnement de production vers l’environnement de test et celui de développement ;](/help/managing/enterprise-devops.md#content-movement)

* **Migration**

  Planifiez, documentez et testez tous les aspects de la migration de contenu, notamment :

   * l’architecture de contenu ;
   * la stratégie de migration ;

* **Communication**

  Assurez-vous que tous les membres de l’équipe et le personnel du projet sont tenus à jour.

* **Documentation**

  Documentez entièrement la solution, notamment :

   * Manuel des opérations
   * toutes les personnalisations pouvant affecter les mises à niveau ;
   * Notes de mise à jour

### les performances et les tests ; {#performance-and-testing}

Une fois la nouvelle application disponible, elle doit subir des tests stricts, tant pour son fonctionnement que pour ses [performances](/help/sites-deploying/configuring-performance.md).

>[!NOTE]
>
>Toute équipe de test doit être autorisée à rester neutre et à fournir les résultats de test.
>
>Il incombe au chef de projet d’évaluer les implications des résultats et de décider des mesures à prendre.

#### Jalons {#milestones-5}

* **Test d’acceptation utilisateur ou utilisatrice final**

  Le [Test d’acceptation des utilisateurs et utilisatrices](/help/sites-developing/acceptance-signoff.md) (UAT) est essentiel pour s’assurer que :

   * La solution répond aux exigences de l’utilisateur, de l’utilisatrice ou de la clientèle.
   * La clientèle, les utilisateurs ou les utilisatrices acceptent la solution (fonction, conception et performances).

  Il doit y avoir une liste de contrôle formalisée pour la remise aux clientes et clients ; idéalement automatisée et exécutée de nuit sur un instantané. Les résultats doivent être envoyés au chef ou à la cheffe de projet et à l’équipe de développement.

* **Tests de performance et de charge**

  Les tests de performance et de charge permettent de s’assurer que la solution respecte les niveaux de performance requis, à des charges moyennes et de pointe.

  Pour plus d’informations sur les tests de performance, voir :

   * [Test de performance](/help/sites-deploying/configuring-performance.md)
   * [Planification et exécution des tests](/help/sites-developing/planning.md)

   * [Consignes de performances de base](/help/sites-deploying/configuring-performance.md#basic-performance-guidelines)

  >[!NOTE]
  >
  >Ce processus doit être poursuivi pendant l’utilisation normale d’AEM, mais ces étapes initiales sont les plus cruciales.

### Déploiement {#rollout}

Le déploiement de votre nouvelle application nécessite une planification attentive pour garantir une mise en production fluide. Cela inclut la confirmation d’un niveau élevé de sécurité, la formation de tous les utilisateurs et utilisatrices potentiels et la réalisation de plusieurs exécutions préliminaires pour confirmer que tous les problèmes ont été traités.

#### Jalons {#milestones-6}

* **Préparation**

  La préparation et la planification aideront à assurer un déploiement en douceur.

* **Formation**

  Assurez-vous que tous les membres du personnel impliqués ont été formés.

  Consultez [Adobe Experience Manager](https://training.adobe.com/training/courses.html#solution=adobeExperienceManager) dans le catalogue de cours.

* **Administrateurs et administratrices formés**

  Assurez-vous que vos administrateurs et administratrices de solution ont :

   * été formés ;
   * reçu les ressources de formation appropriées ;
   * reçu la documentation appropriée.

* **Utilisateurs et utilisatrices formés**

  Assurez-vous que vos auteurs et autrices ont :

   * été formés ;
   * reçu les ressources de formation appropriées ;
   * reçu la documentation appropriée ; par exemple, le Guide d’utilisation.

* **Tests de pénétration**

  Les tests de pénétration simulent une attaque sur un système informatique afin d’identifier les éventuelles failles de sécurité.

* **Tests de pénétration/sécurité**

  Pour garantir la sécurité de votre solution, effectuez des tests de pénétration spécifiques, ainsi qu’un plus large éventail de tests de sécurité.

  Consultez la [Liste de contrôle de sécurité](/help/sites-administering/security-checklist.md) pour plus de détails.

### Activation {#go-live}

Vous voulez que votre activation soit aussi fluide que possible. Encore une fois, les dernières étapes doivent être planifiées pour une exécution propre.

#### Jalons {#milestones-7}

* **Préparation**

  La préparation et la planification aideront à assurer une mise en production fluide.

* **Sécurité**

  Confirmez la sécurité de votre solution pour les utilisateurs et utilisatrices internes et externes et leur contenu.

* **Secours**

  Assurez-vous que l’ensemble des systèmes, procédures et mécanismes requis pour le secours sont en place avant la mise en production.

* **Assistance**

  Assurez-vous que les services d’assistance sont en place et prêts.

* **Transition**

  Planifiez et exécutez la transition vers votre environnement de production et vos utilisateurs et utilisatrices.

* **Déploiement**

  Préparez et exécutez vos tests de fumée.

## Personne {#persona}

Les listes de contrôle sont conçues par persona. Il s’agit des rôles importants dans le cycle de vie du projet.

Il y a aussi quelques [autres personas](#other-persona) qui sont impliqués dans des tâches spécifiques.

### Sponsor du projet {#project-sponsor}

Le sponsor du projet est :

* responsable de l’exécution/de la présentation de l’analyse de rentabilité du projet ;
* essentiel pour définir la portée du projet, notamment :

   * la définition et les critères de réussite ;
   * les principaux KPI ;

* indiquer les jalons principaux en fonction de la feuille de route du client ou de la cliente.

### Chef de projet {#project-manager}

Le chef ou la cheffe de projet est :

* responsable de la diffusion globale du projet en fonction des exigences (par exemple, la portée, les KPI, la définition et les critères de réussite) fournies par le sponsor du projet ;
* responsable de la définition du budget et de la dotation en ressources du projet sur la base de ce budget.
* la principale ou le principal responsable à contacter pour toutes les personnes impliquées dans le projet.

### Architecte {#architect}

L’architecte de la solution :

* est responsable de la conception de haut niveau de la solution et du système ;
* aide à définir la stratégie de mise en œuvre d’AEM Par exemple, déterminer si implémenter une installation mise en cluster ou une reprise à froid ou lorsqu’un réseau de diffusion de contenu (CDN) est nécessaire ;
* définit également l’architecture de la solution AEM en fonction des exigences du client ou de la cliente. Cela peut inclure le concept des rôles utilisateur (avec les droits associés), la relation entre les modèles et les composants ou quand utiliser la gestion multisite.

### Analyste métier {#business-analyst}

L’analyste métier :

* est principalement responsable de rassembler et d’analyser les exigences de haut niveau, puis de les transformer en spécifications :

   * pour que le chef ou la cheffe de projet l’utilise lors de la planification du développement ;
   * pour que l’équipe de développement puisse travailler pendant la conception et le développement.

* travaille en étroite collaboration avec le client ou la cliente pour analyser les exigences. Il ou elle les compare :

   * à la définition de la réussite ;
   * aux critères de réussite ;
   * aux KPI (basés à la fois sur les activités et les performances).

### Responsable du développement {#development-lead}

La ou le responsable du développement :

* est en charge de la diffusion technique du projet ;
* est en charge de choisir une méthodologie de développement conforme aux exigences du client ou de la cliente ;
* élabore la stratégie de développement :

   * en s’assurant qu’elle est alignée sur les KPI métier et de performances ;
   * en prenant en compte les critères et la définition de réussite.

* travaille en étroite collaboration avec l’architecte (notamment lors de l’élaboration de la stratégie de développement pour AEM) afin de définir des aspects tels que la relation entre les modèles et les composants, la stratégie d’intégration pour les applications tierces et toute fonctionnalité spécialisée.

### Responsable qualité {#quality-lead}

Le ou la responsable qualité :

* est en charge de la qualité de la diffusion, en s’assurant qu’elle répond aux critères de réussite et aux KPI définis par le client ou la cliente ;
* définit les mesures de qualité, s’aligne sur toutes les parties prenantes, élabore les plans de test et s’assure qu’ils sont exécutés ;
* crée et diffuse des rapports aux parties prenantes du projet.

### Ingénieur ou ingénieure système {#system-engineer}

L’ingénieur ou l’ingénieure système :

* est responsable de la supervision de l’infrastructure du projet ;
* est responsable de :

   * la configuration des environnements de développement et de test internes ;
   * faire correspondre ces systèmes aux systèmes client.

* fournit des recommandations matérielles, surveille les différentes mises en œuvre et assure la prise en charge des opérations avant et après la mise en service.

### Responsable de la sécurité {#security-lead}

Le ou la responsable de la sécurité :

* est en charge du concept de sécurité global de la solution, en s’assurant qu’elle est alignée sur les exigences et stratégies du client ou de la cliente ;
* fournit un concept de sécurité, des opérations de sécurité et des recommandations pour tout concept de sécurité matériel, tel que les zones et les pare-feu.

### Autres rôles {#other-persona}

* Parties prenantes

   * Personnes (souvent issues de l’entreprise) qui ont un intérêt dans le succès du projet. Elles contribuent souvent au budget.

* Juristes

   * Des conseils juridiques sont nécessaires lors de la négociation de contrats.

* Formateurs et formatrices

   * Selon l’ampleur et la nature du projet, des formateurs et formatrices spécialisés peuvent participer pour développer et présenter des sessions de formation pour les groupes concernés.

* Rédacteurs et rédactrices techniques

   * Selon l’ampleur et la nature du projet, des rédacteurs et rédactrices techniques spécialisés peuvent participer pour écrire des directives et des manuels pour des groupes spécifiques. Par exemple, un manuel de maintenance pour les administrateurs et administratrices système ou un guide d’utilisation pour les auteurs et autrices.

* Administrateurs et administratrices système

   * Responsable du fonctionnement continu du système.

* Auteurs, autrices, utilisateurs et utilisatrices finaux

   * Les personnes qui utilisent le système pour créer et gérer le contenu de votre site web.

## Documents et livrables requis {#required-documents-and-deliverables}

Les listes de contrôle couvrent les **documents requis** et les **éléments livrables** pour chaque jalon.

* Il n’existe aucune relation individuelle entre ces deux éléments ; par exemple, un groupe de documents requis peut générer un seul livrable.
* Le livrable d’un rôle peut être un document requis par un autre rôle au cours du même jalon.

### Documents requis {#required-documents}

Les **documents requis** sont nécessaires au rôle adéquat lors de la production de ses livrables.

Pour chaque **document requis**, le rôle doit indiquer :

* **O/N** : s’il est reçu.
* **1-3** : une indication de la qualité du document reçu.

### objectifs ; {#deliverables}

Pour chaque jalon, le rôle adéquat est chargé de fournir des documents spécifiques et, par conséquent, de remplir ses responsabilités pour un jalon spécifique.

Pour chaque **livrable**, le rôle doit indiquer :

* **O/N** : s’il est terminé.

Les éléments livrables sont souvent utilisés comme des **documents requis** pour le jalon en cours ou un jalon ultérieur.

## Bonnes pratiques connexes {#related-best-practices}

Pour les bonnes pratiques de déploiement, d’administration, de développement ou de création, consultez l’un des liens suivants :

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

   * Adobe Experience Cloud – [Planification pour Adobe Experience Cloud](https://experienceleague.adobe.com/fr/docs/core-services/interface/services/core-services)
