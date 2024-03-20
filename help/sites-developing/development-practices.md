---
title: Meilleures pratiques de développement
description: Bonnes pratiques pour le développement sur Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 65b2029e-03c9-4df4-8579-2b15dbee1035
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 48%

---

# Meilleures pratiques de développement{#development-practices}

## Travail selon une définition de fin (DoD) {#work-according-to-a-definition-of-done}

Chaque équipe possède une définition différente du concept de « fini ». Cependant, il est essentiel d’en établir une et de s’assurer qu’une story répond aux critères définis avant d’être acceptée.

Voici quelques critères généralement spécifiés par les équipes :

* Code révisé pour la mise en forme
* Comments/Javadoc ajouté
* Respecte les niveaux de couverture de test requis
* Effectue les tests d’unité et d’intégration
* Validé dans l’environnement d’assurance qualité
* Localisation implémentée

Sans un département de la Défense bien défini, il est facile de se retrouver dans une situation où beaucoup de choses sont à mi-chemin et où rien n&#39;est vraiment achevé.

### Définition et conformité aux conventions de codage et de formatage {#define-and-adhere-to-coding-and-formatting-conventions}

Les espaces blancs et les niveaux d’indentation sont des éléments qui peuvent paraître secondaires. Cependant, disposer d’un code bien formaté améliore considérablement la lisibilité et la facilité de maintenance. Les conventions doivent être examinées et adoptées en équipe, puis appliquées dans le code.

### Tendre vers une couverture de test élevée  {#aim-for-high-test-coverage}

À mesure que la taille de la mise en oeuvre d’un projet augmente, le temps nécessaire pour le tester augmente également. Sans une bonne couverture de test, l’équipe de test ne peut pas évoluer et les développeurs finissent par être ensevelis dans les bogues.

Les développeurs doivent pratiquer le développement piloté par les tests (TDD), en écrivant les tests unitaires défaillants avant le code de production qui répond à leurs besoins. Le contrôle qualité doit créer un ensemble automatisé de tests d’acceptation pour s’assurer que le système fonctionne comme prévu à un niveau élevé.

Il existe des frameworks personnalisées, comme Jackalope et Prosper, pour faciliter la simulation d’API JCR afin de garantir la productivité des développeurs lors de la création de tests unitaires.

### Rester prêt pour la démonstration {#stay-demo-ready}

Le système doit être disponible à des fins de démonstration à la fin de chaque itération. En maintenant le système dans cet état, l’équipe se trouvera toujours à une itération de la mise en production. Cela permettra, en outre, de maintenir la dette technique à un niveau gérable.

### Mise en œuvre et utilisation d’un environnement d’intégration continue (CI) {#implement-a-continuous-integration-environment-and-use-it}

La mise en oeuvre d’un environnement d’intégration continue vous permet d’exécuter facilement et de manière répétée des tests unitaires et des tests d’intégration. Il découple également les déploiements de l’équipe de développement, permettant ainsi aux autres membres de l’équipe d’être plus efficaces et de garantir des déploiements plus stables et plus prévisibles.

### Assurer un cycle de développement rapide tout en conservant des temps de génération courts {#keep-the-development-cycle-fast-by-keeping-build-times-low}

Si l’exécution de tests unitaires demande trop de temps, les développeurs éviteront de les exécuter et ils perdront leur intérêt. Si la création et le déploiement de code demandent beaucoup de temps, ses opérations seront exécutées moins souvent. En donnant la priorité aux délais de création courts, vous avez la garantie que le temps que vous avez investi dans la couverture de test et dans l’infrastructure d’intégration continue de rendre l’équipe plus productive.

### Optimiser Sonar et d’autres outils d’analyse de code statique et agir sur leurs rapports {#fine-tune-sonar-and-other-static-code-analysis-tools-and-act-on-their-reports}

Les outils d’analyse de code peuvent se révéler très utiles, mais à la seule condition que leurs rapports débouchent sur une action de la part de l’équipe de développement. Sans affiner l&#39;analyse fournie par ces outils, les recommandations qu&#39;ils génèrent sont devenues inutiles et perdent leur valeur.

### Appliquer la règle du boy-scout {#follow-the-boy-scout-rule}

Les boy-scouts ont une règle : « Laissons (ce monde) dans un meilleur état que nous l’avons trouvé ». Tant que tous les membres de l’équipe de développement respectent cette règle et nettoient quelque chose lorsqu’ils rencontrent un problème, le code s’améliore constamment.

### Éviter la mise en œuvre de fonctionnalités YAGNI {#avoid-implementing-yagni-features}

Les fonctionnalités de YAGNI (Vous n&#39;en aurez pas besoin) sont des choses qui sont mises en oeuvre lorsque nous nous attendons à ce que nous ayons besoin de quelque chose à l&#39;avenir, même si nous n&#39;en avons pas besoin maintenant. Idéalement, il convient d’implémenter l’élément le plus simple qui fonctionnera aujourd’hui et procéder à un réusinage de code (refactoring) continu pour s’assurer que l’architecture du système évolue avec les exigences au fil du temps. Cela nous permet de nous concentrer sur ce qui importe et d’éviter le tassement du code et la perte de fonctionnalités.
