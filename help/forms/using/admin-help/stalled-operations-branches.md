---
title: Travailler avec des opérations et des branches bloquées
description: La page Opérations bloquées et la page Branches bloquées affichent les processus qui sont bloqués.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: c96faae0-2b0f-4334-b61c-f13b2d1ec179
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: ht
source-wordcount: '707'
ht-degree: 100%

---

# Travailler avec des opérations et des branches bloquées {#working-with-stalled-operations-and-branches}

La page Opérations bloquées et la page Branches bloquées affichent les processus qui sont bloqués. Un processus peut bloquer lorsqu’une erreur se produit pendant ou après l’exécution d’une opération ou en raison d’une opération de blocage délibérée dans le processus :

* Les opérations peuvent se bloquer en raison d’une erreur imprévue. Cependant, une opération de blocage de branche dans un processus empêche délibérément un processus de s’exécuter davantage et requiert l’intervention de l’administrateur ou de l’administratrice.
* Les branches peuvent bloquer entre les opérations lors de l’évaluation d’une règle.

Lorsqu’un processus bloque, aucune autre opération n’est exécutée tant que le problème n’a pas été résolu et que l’opération ou la branche n’a pas été redémarrée.

Pour chaque élément bloqué, la liste affiche les informations suivantes :

**Nom de l’opération ou nom de la branche :** le nom de l’opération ou de la branche.

**Statut :** toujours BLOQUÉ pour les éléments bloqués.

**Erreur :** brève description du problème.

**Identifiant du processus :** nombre entier positif affecté par Forms Workflow lorsque le processus est instancié (s’il est démarré par un utilisateur ou une étape automatisée). Vous pouvez utiliser cet identificateur pour assurer le suivi de l’instance du processus sur l’ensemble de son cycle de vie.

**Nom du processus - Version :** nom du processus affecté dans Workbench.

**Date du blocage :** date et heure auxquelles l’opération ou la branche ont été bloquées.

Vous pouvez effectuer les tâches suivantes sur la page Opérations bloquées ou Branches bloquées :

* Sélectionnez une erreur pour en afficher les détails. Lorsque vous sélectionnez une erreur, la page Détails de l’erreur s’affiche.
* Arrêtez ou essayez de relancer des opérations bloquées ou essayez de relancer des branches bloquées.

## Arrêt ou nouvelle tentative d’opérations ou de branches bloquées {#terminating-or-retrying-stalled-operations-or-branches}

Sur la page Opérations bloquées, vous pouvez arrêter les instances de processus affichées.

Lorsque vous arrêtez une instance de processus, l’exécution de cette instance s’arrête et aucune opération supplémentaire n’est exécutée. En règle générale, vous arrêtez un processus uniquement s’il devient bloqué ou inutilisable en raison d’une erreur et qu’il ne peut pas être corrigé et redémarré.

Sur la page Opérations bloquées ou Branches bloquées, vous pouvez relancer l’opération ou la branche.

Lorsque vous essayez de relancer une opération, une requête est envoyée au processus des formulaires pour redémarrer l’opération. Si l’erreur qui a provoqué le blocage du processus a été corrigée et que la requête de nouvelle tentative a réussi, le processus recommence à s’exécuter à partir du point où il a bloqué et son état passe à EN COURS. Si l’opération ne peut pas être redémarrée, elle reste bloquée et vous devrez peut-être l’arrêter.

### Arrêt d’une opération bloquée {#terminate-a-stalled-operation}

1. Dans la console d’administration, cliquez sur Services > Forms Workflow > Erreurs des opérations bloquées.
1. Dans la page Opérations bloquées, sélectionnez l’élément à arrêter, puis cliquez sur Arrêter.

### Tentative de redémarrage d’une opération ou d’une branche bloquée {#retry-a-stalled-operation-or-branch}

1. Dans la console d’administration, cliquez sur Services > Forms Workflow, puis sur Erreurs des opérations bloquées ou Erreurs des branches bloquées.
1. Dans la page Opérations bloquées ou Branches bloquées, sélectionnez l’élément que vous souhaitez relancer, puis cliquez sur Nouvel essai.

## Affichage des détails d’erreur des opérations ou des branches bloquées {#viewing-error-details-about-stalled-operations-or-branches}

Si vous sélectionnez une erreur dans la liste des éléments bloqués de la page Opérations bloquées ou Branches bloquées, la page Détails d’erreur s’affiche, présentant des informations détaillées sur l’erreur, susceptibles de vous aider à corriger le problème.

La zone située en bas de la page contient des informations sur l’erreur.

Depuis la page Détails d’erreur, vous pouvez également arrêter ou essayer de relancer des opérations bloquées et essayer de relancer des branches bloquées.

## Le processus n’est pas bloqué lorsque l’utilisateur ou l’utilisatrice de réaffectation n’existe pas. {#process-does-not-stall-when-escalation-user-does-not-exist}

Les erreurs se produisent lorsque l’opération Attribuer une tâche du service User d’AEM forms est configurée pour transmettre la tâche à un autre utilisateur ou utilisatrice après une période déterminée, et lorsque la personne destinataire de la transmission est supprimé après l’exécution de l’opération Attribuer une tâche, mais avant que la transmission n’ait lieu.

Lorsque cette situation se produit, l’état du processus et de la tâche ne change pas au moment configuré de la réaffectation, et celle-ci ne se produit pas, mais le processus ne se bloque pas. Le message suivant s’affiche dans le journal du serveur :

« Le principal pour la réaffectation n’est pas valide, pour taskID : *nombre*, file d’attente spécifiée : *nombre*. »

Si la personne de réaffectation est supprimée avant que la tâche ne soit générée (avant l’exécution de l’opération Affecter une tâche), le processus se bloque ou l’événement d’exception InvalidPrincipal est généré.

Pour éviter ce problème, lorsque vous supprimez un utilisateur ou une utilisatrice, recherchez les tâches qui lui sont associées et traitez-les en conséquence. (Voir [Utilisation des tâches](/help/forms/using/admin-help/tasks.md#working-with-tasks).)
