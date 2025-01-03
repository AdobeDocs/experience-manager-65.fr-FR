---
title: Work Manager et le ralentissement
description: Ce document fournit des informations d’arrière-plan sur Work Manager et fournit des instructions sur la configuration des options de ralentissement de Work Manager.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 1f765de2-1362-4318-9302-c5036e6fa7d6
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '1042'
ht-degree: 100%

---

# Work Manager et le ralentissement{#work-manager-and-throttling}

>[!NOTE]
> 
> Vérifiez que l’utilisateur ou l’utilisatrice dispose de droits d’administration pour accéder à la console d’administration.

AEM Forms (et les versions antérieures) utilisaient les files d’attente JMS pour exécuter des opérations de manière asynchrone. Dans AEM Forms, les files d’attente JMS ont été remplacées par Work Manager. Ce document fournit des informations d’arrière-plan sur Work Manager et fournit des instructions sur la configuration des options de ralentissement de Work Manager.

## À propos des opérations de longue durée (asynchrones) {#about-long-lived-asynchronous-operations}

Dans AEM Forms, les opérations effectuées par les services peuvent être de courte durée (synchrones) ou de longue durée (asynchrones). Les opérations de courte durée se terminent de manière synchrone sur le même thread à partir duquel elles ont été appelées. Ces opérations attendent une réponse avant de continuer.

Les opérations de longue durée peuvent mobiliser plusieurs systèmes ou s’étendre au-delà de l’entreprise, notamment lorsqu’un client ou une cliente doit compléter et soumettre un formulaire de demande de prêt dans le cadre d’une solution regroupant de multiples tâches humaines et automatisées. Ces opérations doivent se poursuivre en attendant une réponse. Les opérations de longue durée exécutent leur travail sous-jacent de manière asynchrone, ce qui permet d’allouer des ressources à une autre tâche en attendant qu’elles se terminent. Contrairement à une opération de courte durée, Work Manager ne considère pas une opération de longue durée comme terminée lorsqu’elle est appelée. Un déclencheur externe, tel qu’un système demandant une autre opération au même service ou un utilisateur ou une utilisatrice envoyant un formulaire, doit se produire pour terminer l’opération.

## À propos de Work Manager {#about-work-manager}

AEM Forms (et les versions antérieures) utilisaient les files d’attente JMS pour exécuter des opérations de manière asynchrone. AEM Forms utilise Work Manager pour planifier et exécuter des opérations asynchrones via des threads gérés.

Les opérations asynchrones sont gérées comme suit :

1. Work Manager reçoit une tâche à exécuter.
1. Work Manager stocke la tâche dans un tableau de base de données et lui affecte un identifiant unique. L’enregistrement de base de données contient toutes les informations requises pour exécuter la tâche.
1. Les threads Work Manager intègrent les tâches lorsque les threads sont libres. Avant d’intégrer les tâches, les threads peuvent vérifier si les services requis ont bien été lancés, si la taille du tas est suffisante pour intégrer la tâche suivante et si le nombre de cycles de processeur est suffisant pour traiter la tâche. Work Manager évalue également les attributs de la tâche (tels que sa priorité) lors de la planification de son exécution.

Les administrateurs et administratrices d’AEM Forms peuvent utiliser Health Monitor pour vérifier les statistiques de Work Manager, telles que le nombre de tâches dans la file d’attente et leur statut. Vous pouvez également utiliser Health Monitor pour suspendre, reprendre, réessayer ou supprimer des tâches. (Voir [Affichage des statistiques relatives à Work Manager](/help/forms/using/admin-help/view-statistics-related-manager.md#view-statistics-related-to-work-manager)).

## Configuration des options de ralentissement de Work Manager {#configuring-work-manager-throttling-options}

Vous pouvez configurer le ralentissement pour Work Manager, afin que les tâches soient planifiées uniquement lorsque les ressources mémoire disponibles sont suffisantes. Vous configurez le ralentissement en définissant les options JVM suivantes dans votre serveur d’applications.

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
   <td><p>Spécifie l’intervalle de temps, en millisecondes, que Work Manager utilise lors de la recherche de nouveaux éléments dans sa file d’attente.</p><p>La valeur de cette option est un nombre entier. La valeur par défaut est de <code>1000</code> millisecondes (1 seconde). </p><p>Si le volume d’appels asynchrones est faible, vous pouvez augmenter cette valeur. Par exemple, vous pouvez l’augmenter jusqu’à un nombre compris entre 2 000 et 5 000 (de 2 à 5 secondes). </p><p>Si le volume d’appels asynchrones est élevé, la valeur par défaut devrait être suffisante, mais vous pouvez aussi utiliser une valeur inférieure en cas de besoin. Une diminution trop importante de cette valeur (par exemple, en dessous de 50, ce qui entraîne une fréquence d’interrogation de 20 fois par seconde) provoque une surcharge importante du système.</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.debug-mode-enabled</code></td>
   <td><p>Définissez cette option sur <code>true</code> pour activer le mode de débogage ou sur false pour le désactiver. </p><p>En mode débogage, les messages concernant les violations de politique de Work Manager et les actions de pause/reprise de Work Manager sont consignés. Définissez cette option sur True pendant le dépannage uniquement.</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.enabled</code></td>
   <td><p>Définissez cette option sur <code>true</code> pour activer le ralentissement en fonction des paramètres de contrôle de la mémoire décrits ci-dessous, ou sur <code>false</code> pour le désactiver.</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.high-limit</code></td>
   <td><p>Spécifie le pourcentage maximum de mémoire pouvant être utilisé avant que Work Manager ralentisse les travaux entrants.</p><p>La valeur par défaut de cette option est <code>95</code>. Elle convient à la plupart des systèmes. Augmentez-la seulement lorsque votre système doit atteindre sa capacité maximale. Mais notez que plus vous augmentez cette valeur, plus le risque de problèmes de mémoire insuffisante augmente également.</p><p>Si vous exécutez AEM Forms dans un environnement en cluster, vous souhaiterez peut-être définir les paramètres de limite de contrôle de la mémoire différemment sur différents nœuds de ce cluster. Par exemple, vous pouvez avoir une limite supérieure plus basse sur les nœuds A et B, qui sont programmés dans votre équilibreur de charge pour le travail interactif. Et vous pouvez avoir des limites supérieures plus élevées sur les nœuds C et D, qui ne sont pas utilisés par l’équilibreur de charge, mais réservés au travail asynchrone.</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.low-limit</code></td>
   <td><p>Spécifie le pourcentage maximal de mémoire qui peut être utilisé avant que Work Manager n’arrête de ralentir les tâches entrantes.</p><p>La valeur par défaut de cette option est <code>20</code>. Elle convient à la plupart des systèmes.</p></td>
  </tr>
  <tr>
   <td><code>Dadobe.workmanager.allocate.max-batch-size</code></td>
   <td><p>Spécifie la taille maximale du lot pour Work Manager. La taille du lot par défaut est 0.</p><p>Si le statut d’un processus dans Work Manager n’est pas mis à jour même une fois la tâche terminée, définissez la taille du lot sur 1.</p></td>
  </tr>
 </tbody>
</table>

**Ajouter des options Java à JBoss**

1. Arrêtez le serveur d’applications JBoss.
1. Ouvrez *[appserver root]*/bin/run.bat (Windows) ou run.sh (Linux ou UNIX) dans un éditeur et ajoutez toutes les options Java requises, au format `-Dproperty=value`.
1. Redémarrez le serveur.

**Ajouter des options Java à WebLogic**

1. Démarrez la console d’administration WebLogic en saisissant `https://[host name]:[port]/console` dans un navigateur web.
1. Tapez le nom d’utilisateur et le mot de passe que vous avez créés pour le domaine du serveur WebLogic, sélectionnez Se connecter sous Centre des modifications, puis Verrouiller et modifier.
1. Sous Structure du domaine, cliquez sur Environment > Serveurs et, dans le volet de droite, cliquez sur le nom du serveur géré.
1. Dans l’écran suivant, cliquez sur les onglets Configuration > Server Start.
1. Dans la zone Arguments, ajoutez les arguments dont vous avez besoin à la fin du contenu actuel. Par exemple, pour désactiver Health Monitor, ajoutez :

   `-Dadobe.healthmonitor.enabled=false` permet de désactiver Health Monitor.

1. Cliquez sur Save, puis sur Activate Changes.
1. Redémarrez le serveur géré WebLogic.

**Ajouter des options Java à WebSphere**

1. Dans l’arborescence de navigation de la console d’administration WebSphere, cliquez sur Serveurs > Types de serveurs > Serveurs d’applications WebSphere.
1. Dans le volet de droite, cliquez sur le nom du serveur.
1. Sous Infrastructure du serveur, cliquez sur Java et Forms Workflow > Définition du processus.
1. Sous Propriétés supplémentaires, cliquez sur Machine virtuelle Java (JVM).
1. Dans la zone Arguments JVM génériques, saisissez les arguments dont vous avez besoin.
1. Cliquez sur OK ou Appliquer, puis sur Enregistrer directement dans la configuration principale.
