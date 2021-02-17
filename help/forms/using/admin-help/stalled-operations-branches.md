---
title: Utilisation d’opérations et de branches bloquées
seo-title: Utilisation d’opérations et de branches bloquées
description: La page Opérations bloquées et la page Branches bloquées répertorient les processus bloqués.
seo-description: La page Opérations bloquées et la page Branches bloquées répertorient les processus bloqués.
uuid: 5f6202b0-79c2-4c3c-847a-236c0366e60b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8c2567f3-7220-436a-b9f2-2824a98c1ccc
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 89%

---


# Utilisation d’opérations et de branches bloquées {#working-with-stalled-operations-and-branches}

La page Opérations bloquées et la page Branches bloquées répertorient les processus bloqués. Un processus peut bloquer lorsqu’une erreur survient pendant ou après l’exécution d’une opération ou en raison d’une opération de blocage délibérée dans le processus :

* Les opérations peuvent bloquer suite à une erreur imprévue. Toutefois, une opération de blocage de branche dans un processus arrête délibérément l’exécution d’un processus et implique l’intervention de l’administrateur.
* Les branches peuvent bloquer entre des opérations pendant l’évaluation d’une règle.

Quand un processus bloque, l’exécution de toutes les opérations suivantes est interrompue jusqu’à ce que le problème soit corrigé et que l’opération ou la branche soit redémarrée.

Pour chaque élément bloqué, la liste présente les informations suivantes :

**Nom de l&#39;opération ou Nom de la branche : nom** de l&#39;opération ou de la branche.

**Statut :** Toujours BLOQUE pour les éléments bloqués.

**Erreur :** brève description du problème.

**ID de processus : entier positif attribué par** le processus des formulaires lorsque le processus est instancié (c’est-à-dire lorsqu’un utilisateur ou une étape automatisée lance un processus). Vous pouvez utiliser cet identificateur pour assurer le suivi de l’instance du processus sur l’ensemble de son cycle de vie.

**Nom du processus - Version : nom** du processus affecté dans Workbench.

**Date bloquée :** date et heure auxquelles l’opération ou la branche est bloquée.

Vous pouvez exécuter les tâches suivantes dans la page Opérations bloquées ou Branches bloquées :

* Sélectionner une erreur pour afficher des informations détaillées sur cette erreur. Si vous sélectionnez une erreur, la page Détails d’erreur s’affiche.
* Arrêter ou essayer de relancer les opérations bloquées ou essayer de relancer les branches bloquées.

## Arrêt ou nouvelle tentative d’opérations ou de branches bloquées {#terminating-or-retrying-stalled-operations-or-branches}

Dans la page Opérations bloquées, vous pouvez arrêter les instances de processus affichées.

Lorsque vous arrêtez une instance de processus, l’exécution de cette instance s’arrête et aucune opération supplémentaire n’est exécutée. En règle générale, vous n’arrêtez un processus que s’il a bloqué, ou que s’il est inutilisable suite à une erreur et ne peut pas être corrigé ou redémarré.

Dans la page Opérations bloquées ou Branches bloquées, vous pouvez essayer de relancer l’opération ou la branche.

Lorsque vous essayez de relancer une opération, une requête est envoyée au processus des formulaires pour redémarrer l’opération. Si l’erreur qui a généré le blocage du processus a été corrigée et que la requête de nouvelle tentative réussit, l’exécution du processus recommence à partir du point où le processus a bloqué. Son état devient alors EN COURS. Si l’opération ne peut pas être redémarrée, son état reste BLOQUE ; il est possible que vous deviez alors l’arrêter.

### Arrêt d’une opération bloquée  {#terminate-a-stalled-operation}

1. Dans Administration Console, cliquez sur Services > Processus des formulaires > Erreurs des opérations bloquées.
1. Dans la page Opérations bloquées, sélectionnez l’élément à arrêter, puis cliquez sur Arrêter.

### Tentative de redémarrage d’une opération ou d’une branche bloquée  {#retry-a-stalled-operation-or-branch}

1. Dans Administration Console, cliquez sur Services > Processus des formulaires, puis sélectionnez Erreurs des opérations bloquées ou Erreurs de branche bloquée.
1. Dans la page Opérations bloquées ou Branches bloquées, sélectionnez l’élément que vous souhaitez relancer, puis cliquez sur Nouvel essai.

## Affichage des détails d’erreur des opérations ou des branches bloquées  {#viewing-error-details-about-stalled-operations-or-branches}

Si vous sélectionnez une erreur dans la liste des éléments bloqués de la page Opérations bloquées ou Branches bloquées, la page Détails d’erreur s’affiche, présentant des informations détaillées sur l’erreur, susceptibles de vous aider à corriger le problème.

La zone située en bas de la page contient des informations sur l’erreur.

Depuis la page Détails d’erreur, vous pouvez également arrêter ou essayer de relancer des opérations bloquées et essayer de relancer des branches bloquées.

## Le processus n’est pas gelé si aucun utilisateur de transmission n’existe  {#process-does-not-stall-when-escalation-user-does-not-exist}

Les erreurs se produisent lorsque l’opération Attribuer une tâche du service User d’AEM forms est configurée pour transmettre la tâche à un autre utilisateur après une période déterminée, et lorsque l’utilisateur destinataire de la transmission est supprimé après l’exécution de l’opération Attribuer une tâche, mais avant que la transmission n’ait lieu.

Dans ces cas-là, l’état du processus et de la tâche ne change pas au moment configuré pour la transmission. La transmission n’a pas lieu, mais le processus ne se bloque pas. Le message suivant s’affiche dans le fichier journal du serveur :

« L’entité de sécurité spécifiée pour la transmission n’est pas valide pour l’ID de la tâche :*numéro*, file d’attente spécifiée :*numéro* ».

Si l’utilisateur de transmission est supprimé avant que la tâche ne soit générée (avant l’exécution de l’opération Attribuer une tâche), le processus est gelé ou l’événement d’exception InvalidPrincipal est généré.

Pour éviter ce problème, lorsque vous supprimez un utilisateur, recherchez les tâches lui appartenant et traitez-les de manière appropriée (voir [Utilisation de tâches](/help/forms/using/admin-help/tasks.md#working-with-tasks)).
