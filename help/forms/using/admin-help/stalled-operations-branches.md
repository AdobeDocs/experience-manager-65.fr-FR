---
title: Travailler avec des opérations et des branches bloquées
description: La page Opérations bloquées et la page Branches bloquées affichent les processus qui ont bloqué.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: c96faae0-2b0f-4334-b61c-f13b2d1ec179
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '707'
ht-degree: 16%

---

# Travailler avec des opérations et des branches bloquées {#working-with-stalled-operations-and-branches}

La page Opérations bloquées et la page Branches bloquées affichent les processus qui ont bloqué. Un processus peut bloquer lorsqu’une erreur se produit pendant ou après l’exécution d’une opération ou en raison d’une opération de blocage délibérée dans le processus :

* Les opérations peuvent se bloquer en raison d’une erreur imprévue. Cependant, une opération de blocage de branche dans un processus empêche délibérément un processus de s’exécuter davantage et requiert l’intervention de l’administrateur.
* Les branches peuvent bloquer entre les opérations lors de l’évaluation d’une règle.

Lorsqu’un processus bloque, aucune autre opération n’est exécutée tant que le problème n’a pas été résolu et que l’opération ou la branche n’a pas été redémarrée.

Pour chaque élément bloqué, la liste affiche les informations suivantes :

**Nom de l’opération ou nom de la branche :** le nom de l’opération ou de la branche.

**Statut :** toujours BLOQUÉ pour les éléments bloqués.

**Erreur :** brève description du problème.

**Identifiant du processus :** nombre entier positif affecté par Forms Workflow lorsque le processus est instancié (s’il est démarré par un utilisateur ou une étape automatisée). Vous pouvez utiliser cet identificateur pour assurer le suivi de l’instance du processus sur l’ensemble de son cycle de vie.

**Nom du processus - Version :** nom du processus affecté dans Workbench.

**Date du blocage :** date et heure auxquelles l’opération ou la branche ont été bloquées.

Vous pouvez effectuer les tâches suivantes sur la page Opérations bloquées ou Branches bloquées :

* Sélectionnez une erreur pour en afficher les détails. Lorsque vous sélectionnez une erreur, la page Détails de l’erreur s’affiche.
* Arrêtez ou essayez de relancer des opérations bloquées ou essayez de relancer des branches bloquées.

## Arrêt ou nouvelle tentative d’opérations ou de branches bloquées {#terminating-or-retrying-stalled-operations-or-branches}

Sur la page Opérations bloquées, vous pouvez arrêter les instances de processus affichées.

Lorsque vous arrêtez une instance de processus, celle-ci s’arrête et aucune opération supplémentaire n’a lieu. En règle générale, vous arrêtez un processus uniquement s’il devient bloqué ou inutilisable en raison d’une erreur et qu’il ne peut pas être corrigé et redémarré.

Sur la page Opérations bloquées ou Branches bloquées, vous pouvez relancer l’opération ou la branche.

Lorsque vous essayez de relancer une opération, une requête est envoyée au processus des formulaires pour redémarrer l’opération. Si l’erreur qui a provoqué le blocage du processus a été corrigée et que la requête de nouvelle tentative a réussi, le processus recommence à s’exécuter à partir du point où il a bloqué et son état passe à EN COURS. Si l’opération ne peut pas être redémarrée, elle reste bloquée et vous devrez peut-être l’arrêter.

### Arrêt d’une opération bloquée {#terminate-a-stalled-operation}

1. Dans Administration Console, cliquez sur Services > Processus des formulaires > Erreurs des opérations bloquées.
1. Sur la page Opérations bloquées , sélectionnez l’élément que vous souhaitez arrêter, puis cliquez sur Arrêter.

### Réessayer une opération ou une branche bloquée {#retry-a-stalled-operation-or-branch}

1. Dans Administration Console, cliquez sur Services > Processus des formulaires, puis sur Erreurs des opérations bloquées ou Erreurs de branche bloquée.
1. Sur la page Opérations bloquées ou Branches bloquées , sélectionnez l’élément que vous souhaitez réessayer, puis cliquez sur Réessayer.

## Affichage des détails d’erreur sur les opérations ou les branches bloquées {#viewing-error-details-about-stalled-operations-or-branches}

Si vous sélectionnez une erreur dans la liste des éléments bloqués de la page Opérations bloquées ou Branches bloquées, la page Détails de l’erreur s’affiche, qui affiche des détails sur l’erreur qui peut vous aider à résoudre le problème.

La zone située au bas de la page contient les informations d’erreur.

Vous pouvez également arrêter ou essayer de relancer des opérations bloquées et essayer de relancer des branches bloquées à partir de la page Détails de l’erreur .

## Le processus n’est pas bloqué lorsque l’utilisateur de réaffectation n’existe pas {#process-does-not-stall-when-escalation-user-does-not-exist}

Des erreurs se produisent lorsque l’opération Assign Task du service Utilisateur d’AEM forms est configurée pour réaffecter la tâche à un autre utilisateur après une période spécifique, et que l’utilisateur de réaffectation est supprimé après l’exécution de l’opération Assign Task mais avant la transmission.

Lorsque cette situation se produit, l’état du processus et de la tâche ne change pas au moment configuré de la réaffectation, et celle-ci ne se produit pas, mais le processus ne se bloque pas. Le message suivant apparaît dans le journal du serveur :

&quot;L’entité spécifiée pour la transmission n’est pas valide, pour taskID : *nombre*, queue spécifiée : *nombre*.&quot;

Si l’utilisateur de réaffectation est supprimé avant que la tâche ne soit générée (avant l’exécution de l’opération Assign Task), le processus se bloque ou l’événement d’exception InvalidPrincipal est généré.

Pour éviter ce problème, lorsque vous supprimez un utilisateur, recherchez les tâches qui lui sont associées et traitez-les en conséquence. (Voir [Utilisation des tâches](/help/forms/using/admin-help/tasks.md#working-with-tasks).)
