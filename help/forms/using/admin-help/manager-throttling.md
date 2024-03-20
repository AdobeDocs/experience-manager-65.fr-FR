---
title: Work Manager et le ralentissement
description: Ce document fournit des informations d’arrière-plan sur Work Manager et fournit des instructions sur la configuration des options de ralentissement de Work Manager.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 1f765de2-1362-4318-9302-c5036e6fa7d6
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1030'
ht-degree: 15%

---

# Work Manager et le ralentissement{#work-manager-and-throttling}

AEM forms (et les versions antérieures) utilisaient les files d’attente JMS pour exécuter des opérations de manière asynchrone. Dans AEM forms, les files d’attente JMS ont été remplacées par Work Manager. Ce document fournit des informations d’arrière-plan sur Work Manager et fournit des instructions sur la configuration des options de ralentissement de Work Manager.

## À propos des opérations de longue durée (asynchrones) {#about-long-lived-asynchronous-operations}

Dans AEM forms, les opérations effectuées par les services peuvent être de courte durée (synchrone) ou de longue durée (asynchrone). Les opérations de courte durée se terminent de manière synchrone sur le même thread à partir duquel elles ont été invoquées. Ces opérations attendent une réponse avant de continuer.

Les opérations de longue durée peuvent s’étendre à plusieurs systèmes ou même s’étendre au-delà de l’organisation, par exemple lorsqu’un client doit remplir et envoyer un formulaire de demande de prêt dans le cadre d’une solution plus vaste qui intègre plusieurs tâches automatisées et humaines. Ces opérations doivent se poursuivre en attendant une réponse. Les opérations de longue durée exécutent leur travail sous-jacent de manière asynchrone, ce qui permet d’allouer des ressources autrement en attendant leur achèvement. Contrairement à une opération de courte durée, Work Manager ne considère pas une opération de longue durée comme terminée une fois appelée. Un déclencheur externe, tel qu’un système demandant une autre opération sur le même service ou un utilisateur envoyant un formulaire, doit se produire pour terminer l’opération.

## À propos de Work Manager {#about-work-manager}

AEM forms (et les versions antérieures) utilisaient les files d’attente JMS pour exécuter des opérations de manière asynchrone. AEM forms utilise Work Manager pour planifier et exécuter des opérations asynchrones via des threads gérés.

Les opérations asynchrones sont gérées de la manière suivante :

1. Work Manager reçoit une tâche à exécuter.
1. Work Manager stocke l’élément de travail dans un tableau de base de données et lui affecte un identifiant unique. L’enregistrement de base de données contient toutes les informations requises pour exécuter l’élément de travail.
1. Les threads Work Manager extraient des tâches lorsque les threads deviennent libres. Avant d’extraire les tâches, les threads peuvent vérifier si les services requis sont démarrés, s’il existe suffisamment de taille de tas pour extraire l’élément de travail suivant et s’il existe suffisamment de cycles de processeur pour traiter l’élément de travail. Work Manager évalue également les attributs de l’élément de travail (comme sa priorité) lors de la planification de son exécution.

Les administrateurs d’AEM forms peuvent utiliser Health Monitor pour vérifier les statistiques Work Manager, telles que le nombre de tâches dans la file d’attente et leur état. Vous pouvez également utiliser Health Monitor pour suspendre, reprendre, réessayer ou supprimer des tâches. (Voir [Affichage des statistiques relatives à Work Manager](/help/forms/using/admin-help/view-statistics-related-manager.md#view-statistics-related-to-work-manager).)

## Configuration des options de ralentissement de Work Manager {#configuring-work-manager-throttling-options}

Vous pouvez configurer le ralentissement pour Work Manager, de sorte que les tâches ne soient planifiées que lorsque les ressources mémoire sont suffisantes. Configurez le ralentissement en définissant les options JVM suivantes dans votre serveur d’applications.

<table>
 <thead>
  <tr>
   <th><p>Propriété</p></th>
   <th><p>Description</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><code> adobe.work-manager.queue-refill-interval</code></td>
   <td><p>Indique l’intervalle, en millisecondes, utilisé par Work Manager lors de la vérification de nouveaux éléments dans sa file d’attente.</p><p>La valeur de cette option est un entier. La valeur par défaut est de <code>1000</code> millisecondes (1 seconde). </p><p>Si le volume des appels asynchrones est faible, vous pouvez augmenter cette valeur. Par exemple, vous pouvez l’augmenter à un niveau compris entre 2 000 et 5 000 (2 à 5 secondes). </p><p>Si le volume des appels asynchrones est élevé, la valeur par défaut doit être suffisante, mais vous pouvez utiliser une valeur inférieure si nécessaire. Si vous réduisez trop cette valeur (par exemple, en dessous de 50, ce qui entraîne une fréquence d’interrogation de 20 fois par seconde), le système est considérablement pris en charge.</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.debug-mode-enabled</code></td>
   <td><p>Définissez cette option sur <code>true</code> pour activer le mode de débogage ou sur false pour le désactiver. </p><p>En mode de débogage, les messages concernant les violations de stratégie de Work Manager et les actions de mise en pause/reprise de Work Manager sont consignés. Définissez cette option sur true uniquement lors de la résolution des problèmes.</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.enabled</code></td>
   <td><p>Définissez cette option sur <code>true</code> pour activer le ralentissement en fonction des paramètres de contrôle de la mémoire décrits ci-dessous, ou sur <code>false</code> pour le désactiver.</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.high-limit</code></td>
   <td><p>Spécifie le pourcentage maximum de mémoire pouvant être utilisé avant que Work Manager ralentisse les travaux entrants.</p><p>La valeur par défaut de cette option est <code>95</code>. Elle convient à la plupart des systèmes. Augmentez-la uniquement si votre système doit atteindre sa capacité maximale. Mais notez que lorsque vous augmentez cette valeur, le risque de problèmes de mémoire insuffisante augmente également.</p><p>Si vous exécutez AEM forms dans un environnement organisé en grappe, vous pouvez définir les paramètres de limite de contrôle de la mémoire différemment sur différents noeuds de la grappe. Par exemple, vous pouvez avoir une limite élevée plus faible sur les noeuds A et B, qui sont programmés dans votre équilibreur de charge pour un travail interactif. Et vous pouvez définir des limites hautes plus élevées sur les noeuds C et D, qui ne sont pas utilisés par l’équilibreur de charge, mais réservés au travail asynchrone.</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.low-limit</code></td>
   <td><p>Spécifie le pourcentage maximal de mémoire pouvant être utilisé avant que Work Manager cesse de limiter les tâches entrantes.</p><p>La valeur par défaut de cette option est <code>20</code>. Elle convient à la plupart des systèmes.</p></td>
  </tr>
  <tr>
   <td><code>Dadobe.workmanager.allocate.max-batch-size</code></td>
   <td><p>Indique la taille maximale du lot pour workmanager. La taille de lot par défaut est 10.</p><p>Si l’état d’un processus dans le gestionnaire de travail n’est pas mis à jour même une fois la tâche terminée, définissez la taille du lot sur 1.</p></td>
  </tr>
 </tbody>
</table>

**Ajout d’options Java à JBoss**

1. Arrêtez le serveur d’applications JBoss.
1. Ouvrez *[appserver root]*/bin/run.bat (Windows) ou run.sh (Linux ou UNIX) dans un éditeur et ajoutez toutes les options Java requises, au format `-Dproperty=value`.
1. Redémarrez le serveur.

**Ajout d’options Java à WebLogic**

1. Démarrez la console d’administration WebLogic en saisissant `https://[host name]:[port]/console` dans un navigateur web.
1. Saisissez le nom d’utilisateur et le mot de passe que vous avez créés pour le domaine WebLogic Server, puis cliquez sur Journal sous Change Center, puis sur Lock &amp; Edit.
1. Sous Domain Structure, cliquez sur Environment > Servers et, dans le volet de droite, cliquez sur le nom du serveur géré.
1. Dans l’écran suivant, cliquez sur les onglets Configuration > Server Start.
1. Dans la zone Arguments , ajoutez les arguments dont vous avez besoin à la fin du contenu actuel. Par exemple, pour désactiver Health Monitor, ajoutez :

   `-Dadobe.healthmonitor.enabled=false` permet de désactiver Health Monitor.

1. Cliquez sur Save, puis sur Activate Changes.
1. Redémarrez le serveur géré WebLogic.

**Ajout d’options Java à WebSphere**

1. Dans l’arborescence de navigation de la console d’administration WebSphere, cliquez sur Servers > Server Types > WebSphere application servers.
1. Dans le volet de droite, cliquez sur le nom du serveur.
1. Sous Server Infrastructure, cliquez sur Java and forms workflow > Process Definition.
1. Sous Additional Properties, cliquez sur Java Virtual Machine.
1. Dans la zone Generic JVM arguments , saisissez les arguments dont vous avez besoin.
1. Cliquez sur OK ou sur Apply, puis sur Save directly to master configuration.
