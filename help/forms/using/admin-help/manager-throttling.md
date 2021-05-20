---
title: Work Manager et le ralentissement
seo-title: Work Manager et le ralentissement
description: Ce document fournit des informations sur Work Manager, ainsi que des instructions sur la configuration des options de ralentissement de Work Manager.
seo-description: Ce document fournit des informations sur Work Manager, ainsi que des instructions sur la configuration des options de ralentissement de Work Manager.
uuid: b90998bc-e3d4-493a-9371-55ccb44da20d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9a8b4e3a-f416-4dc6-a90a-9018df5c844e
exl-id: 1f765de2-1362-4318-9302-c5036e6fa7d6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1044'
ht-degree: 95%

---

# Work Manager et le ralentissement{#work-manager-and-throttling}

AEM Forms (et les versions antérieures) utilisaient les files d’attente JMS pour exécuter des opérations de façon asynchrone. Dans AEM Forms, les files d’attente JMS ont été remplacées par Work Manager. Ce document fournit des informations sur Work Manager, ainsi que des instructions sur la configuration des options de ralentissement de Work Manager.

## A propos des opérations de longue durée (asynchrones) {#about-long-lived-asynchronous-operations}

Dans AEM Forms, les opérations effectuées par les services peuvent être de longue (asynchrones) ou de courte durée (synchrones). Les opérations de courte durée sont achevées simultanément sur le même thread que celui qui les a appelées. Ces opérations attendent une réponse avant de continuer.

Les opérations de longue durée peuvent mobiliser plusieurs systèmes ou s’étendre au-delà de l’entreprise, notamment lorsqu’un client doit compléter et soumettre un formulaire de demande de prêt dans le cadre d’une solution regroupant de multiples tâches humaines et automatisées. Ces opérations doivent continuer tout en attendant une réponse. Les opérations de longue durée s’exécutent de manière asynchrone, tout en permettant d’allouer des ressources à une autre tâche entre-temps. Contrairement à une opération de courte durée, Work Manager ne considère pas une opération de longue durée comme terminée lorsqu’elle est appelée. Un déclencheur externe, comme un système demandant une autre opération au même service ou un utilisateur envoyant un formulaire, doit être activé pour achever l’opération.

## A propos de Work Manager  {#about-work-manager}

AEM Forms (et les versions antérieures) utilisaient les files d’attente JMS pour exécuter des opérations de façon asynchrone. AEM Forms utilise Work Manager pour planifier et exécuter des opérations asynchrones via des threads gérés.

Les opérations asynchrones sont gérées comme suit :

1. Work Manager reçoit une tâche prête à être exécutée.
1. Work Manager stocke les travaux dans un tableau de base de données et affecte un identifiant unique à chacun d’eux. L’enregistrement de base de données contient toutes les informations requises pour exécuter la tâche.
1. Les threads Work Manager intègrent les tâches lorsque les threads se libèrent. Avant d’intégrer les tâches, les threads peuvent vérifier si les services requis ont bien été lancés, si la taille du tas est suffisante pour intégrer la tâche suivante et si le nombre de cycles de processeur est suffisant pour traiter la tâche. Work Manager évalue également les attributs de la tâche (tels que sa priorité) lors de la planification de son exécution.

Les administrateurs AEM forms peuvent utiliser Health Monitor pour vérifier les statistiques Work Manager, telles que le nombre de travaux dans la file d’attente et leur statut. Vous pouvez également utiliser Health Monitor pour mettre en pause, reprendre, réessayer ou supprimer des tâches (voir [Affichage des statistiques relatives à Work Manager](/help/forms/using/admin-help/view-statistics-related-manager.md#view-statistics-related-to-work-manager)).

## Configuration des options de ralentissement de Work Manager  {#configuring-work-manager-throttling-options}

Vous pouvez configurer le ralentissement de Work Manager, de façon que les tâches ne soient planifiées qu’une fois les ressources mémoire suffisantes. Pour configurer le ralentissement, définissez les options suivantes pour la JVM dans votre serveur d’applications.

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
   <td><p>Spécifie l’intervalle, en millisecondes, utilisé par Work Manager pour vérifier la présence de nouvelles tâches dans sa file d’attente.</p><p>La valeur de cette option est un entier. La valeur par défaut est <code>1000</code> millisecondes (1 seconde). </p><p>Si le volume d’appels asynchrones est faible, vous pouvez l’augmenter. Vous pouvez par exemple passer à une valeur comprise entre 2 000 et 5 000 (2 à 5 secondes). </p><p>Si le volume d’appels asynchrones est élevé, la valeur par défaut doit suffire, mais vous pouvez, si nécessaire, utiliser une valeur plus faible. Réduire cette valeur de façon trop importante (par exemple en dessous de 50, cette valeur entraînant 20 interrogations par seconde) provoque une surcharge substantielle au niveau du système.</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.debug-mode-enabled</code></td>
   <td><p>Définissez cette option sur <code>true</code> pour activer le mode de débogage ou sur false pour le désactiver. </p><p>En mode de débogage, les messages se rapportant aux violations de stratégies et aux actions de mise en pause/reprise de Work Manager sont enregistrés. Définissez cette option sur true uniquement dans le cadre d’un dépannage.</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.enabled</code></td>
   <td><p>Définissez cette option sur <code>true</code> pour activer le ralentissement en fonction des paramètres de contrôle de la mémoire décrits ci-dessous, ou sur <code>false</code> pour le désactiver.</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.high-limit</code></td>
   <td><p>Spécifie le pourcentage maximum de mémoire pouvant être utilisé avant que Work Manager ralentisse les travaux entrants.</p><p>La valeur par défaut de cette option est <code>95</code>. Elle convient à la plupart des systèmes. Augmentez-la uniquement si votre système a besoin d’utiliser sa capacité maximale. Veuillez toutefois noter qu’une augmentation de cette valeur accroît également le risque de problèmes de mémoire.</p><p>Si vous exécutez AEM Forms dans un environnement en grappe, vous pouvez définir les paramètres de limite de contrôle de la mémoire différemment sur différents nœuds de la grappe. Par exemple, vous pouvez définir une limite haute moins élevée sur les nœuds A et B, qui sont programmés dans votre équilibreur de charge pour le travail interactif. Et vous pouvez définir des limites hautes plus élevées sur les nœuds C et D, qui ne sont pas utilisés par l’équilibreur de charge, mais réservés pour le travail asynchrone.</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.low-limit</code></td>
   <td><p>Spécifie le pourcentage maximum de mémoire pouvant être utilisé avant que Work Manager arrête le ralentissement des travaux entrants.</p><p>La valeur par défaut de cette option est <code>20</code>. Elle convient à la plupart des systèmes.</p></td>
  </tr>
  <tr>
   <td><code>Dadobe.workmanager.allocate.max-batch-size</code></td>
   <td><p>Spécifie la taille de lot maximale pour Work Manager. La taille de lot par défaut est 10.</p><p>Si l’état d’un processus dans le Work Manager n’est pas mis à jour, même une fois la tâche terminée, définissez la taille du lot sur 1.</p></td>
  </tr>
 </tbody>
</table>

**Ajout d’options Java à JBoss**

1. Arrêtez le serveur d’applications JBoss.
1. Ouvrez la *[racine du serveur d’applications]*/bin/run.bat (Windows) ou run.sh (Linux ou UNIX) dans un éditeur et ajoutez l’une des options Java requises, au format `-Dproperty=value`.
1. Redémarrez le serveur.

**Ajout d’options Java à WebLogic**

1. Ouvrez WebLogic Administration Console en saisissant `https://[host name]:[port]/console` dans un navigateur Web.
1. Saisissez le nom d’utilisateur et le mot de passe créés pour le domaine WebLogic Server, puis cliquez sur Log. Sous Change Center, cliquez sur Lock &amp; Edit.
1. Sous Domain Structure, cliquez sur Environment > Servers et, dans le volet de droite, cliquez sur le nom du serveur géré.
1. Dans l’écran suivant, cliquez sur les onglets Configuration > Server Start.
1. Dans la zone Arguments, ajoutez les arguments souhaités à la fin du contenu actuel. Par exemple, pour désactiver Health Monitor, ajoutez :

   `-Dadobe.healthmonitor.enabled=false` désactive Health Monitor.

1. Cliquez sur Enregistrer, puis sur Activer les changements.
1. Redémarrez le serveur géré WebLogic.

**Ajout d’options Java à WebSphere**

1. Dans l’arborescence de navigation de la console d’administration WebSphere, cliquez sur Servers > Server Types > WebSphere Application Servers.
1. Dans le volet de droite, cliquez sur le nom du serveur.
1. Sous Infrastructure du serveur, cliquez sur Processus Java et formulaires > Définition du process.
1. Sous Additional Properties, cliquez sur Java Virtual Machine.
1. Dans la zone Generic JVM arguments, saisissez les arguments souhaités.
1. Cliquez sur OK ou sur Apply, puis sur Save directly to master configuration.
