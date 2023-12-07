---
title: Gestion de processus
description: La page Liste des processus affiche les processus initiés par un utilisateur ou démarrés automatiquement. Découvrez la gestion des processus.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 21a2317d-3542-4ccb-98db-3cedf20c89ea
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1631'
ht-degree: 39%

---

# Gestion de processus {#managing-processes}

La page Liste des processus affiche les processus initiés par un utilisateur ou démarrés automatiquement.

1. Dans Administration Console, cliquez sur Services > Processus Forms > Processus Forms. La liste des processus affiche les informations suivantes :

   **Nom du processus - Version :** nom du processus, tel que défini dans Workbench.

   **Application :** application à laquelle appartient le processus, tel que défini dans Workbench.

   **Statut :** actif signifie que le processus est celui qui est activé pour la version du processus. Inactif signifie que le processus est une ancienne version qui comporte toujours des instances de processus.

   **Date de création :** date et heure auxquelles le processus a été déployé.

1. Cliquez sur le nom d’un processus pour afficher ses instances de processus sur la page Instance du processus .

## Utilisation des instances de processus {#working-with-process-instances}

Si vous accédez à la page Instance du processus à partir de la page Liste des processus, toutes les instances de processus que vous avez sélectionnées sont répertoriées. Si vous accédez à la page Instance du processus après avoir effectué une recherche, seules les instances de processus trouvées sont répertoriées.

Pour chaque instance de processus, la liste affiche les informations suivantes :

**Identifiant de processus :** identifiant attribué par Forms Workflow lorsque le processus est instancié (démarré par un utilisateur ou une étape automatisée). Vous pouvez utiliser cet identificateur pour assurer le suivi de l’instance du processus sur l’ensemble de son cycle de vie.

**Nom du processus - Version :** nom du processus, tel que défini dans Workbench.

**Statut :** indique si l’instance de processus fonctionne normalement, change d’état ou s’est arrêtée. (voir A propos des états d’instances de processus).

**Date de création :** date et heure auxquelles l’instance de processus a été créée.

**Date de mise à jour :** date et heure du dernier changement d’état de l’instance de processus.

Vous pouvez effectuer les tâches suivantes sur la page Instance du processus :

* Sélectionnez une instance de processus pour afficher des détails sur celle-ci, tels que ses opérations et ses sous-processus. Lorsque vous sélectionnez une instance de processus, la page Détails de l’instance du processus s’affiche.
* Suspendre, annuler la suspension ou arrêter des instances de processus.
* Recherchez une instance de processus. Pour lancer une recherche, cliquez sur Rechercher.

### À propos des états d’instances de processus {#about-process-instance-statuses}

Une instance de processus, y compris les sous-processus, peut avoir les états suivants :

**ACHEVÉ :** toutes les branches et opérations de l’instance de processus sont achevées. ACHEVE est l’état final d’une instance de processus.

**EN COURS D’ACHÈVEMENT :** le statut de l’instance de processus est sur le point de devenir ACHEVÉ.

**INITIÉ :** l’instance de processus a été créée, mais n’est pas encore en cours d’exécution. INITIE est le premier état d’une instance de processus.

**EN COURS :** l’instance de processus s’exécute normalement. Il est possible qu’une étape automatique soit en cours, ou que l’instance de processus reçoive des entrées utilisateur ou qu’elle soit en attente d’une interaction utilisateur.

**SUSPENDU :** l’instance de processus a été suspendue par un administrateur ou par une étape du processus. Aucune opération supplémentaire ne sera exécutée jusqu’au changement de l’état.

**SUSPENSION EN COURS :** le statut est sur le point de devenir SUSPENDU. Si une opération a été conçue pour ignorer les requêtes de suspension et n’est pas encore achevée, cette opération doit s’achever avant que l’instance de processus soit suspendue.

**INTERROMPU :** l’instance de processus a été interrompue par un administrateur.

**INTERRUPTION EN COURS :** le statut est sur le point de devenir INTERROMPU. Si une opération a été conçue pour ignorer les requêtes d’arrêt et n’est pas encore achevée, cette opération doit s’achever avant que l’instance de processus soit arrêtée.

**ANNULATION DE SUSPENSION EN COURS :** le statut est sur le point de devenir EN COURS après avoir été SUSPENDU.

>[!NOTE]
>
>Lorsqu’une demande est envoyée pour modifier l’état d’une instance de processus (par exemple, pour suspendre ou arrêter), la demande entre dans la file d’attente des commandes du processus des formulaires. Selon la taille de la file d’attente et la vitesse de traitement globale, l’état affiché peut ne pas changer tant que la page n’est pas rechargée une ou plusieurs fois.

### Suspension ou annulation de la suspension des instances de processus {#suspend-or-unsuspend-process-instances}

Si vous devez résoudre un problème ou si vous savez qu’une instance de processus rencontrera un problème à une étape ultérieure en raison d’une condition externe, vous pouvez suspendre temporairement l’instance de processus.

Vous pouvez suspendre les instances de processus dont l’état est EN COURS.

Après avoir suspendu une instance de processus, son état passe à SUSPENSION, puis SUSPENDU, et le processus s’interrompt au cours de son opération actuelle. L’instance de processus reste dans cet état jusqu’à ce que l’état soit défini sur NON SUSPENDU.

Seules les instances de processus dont l’état est SUSPENDU peuvent être modifiées en NON SUSPENDU.

Lorsque vous annulez la suspension d’une instance de processus, son état devient EN COURS, et l’opération qui l’a suspendue se poursuit.

Lorsque vous suspendez une instance de processus qui a appelé d’autres processus (processus enfants) en utilisant leur opération d’appel, les processus enfants sont également suspendus.

1. Dans Administration Console, cliquez sur Services > Processus Forms > Processus Forms.
1. Sur la page Instance du processus, sélectionnez le processus, puis cliquez sur Suspendre ou Annuler la suspension.

### Arrêt d’une instance de processus {#terminate-a-process-instances}

Si une opération d’une instance de processus a bloqué ou a rencontré une autre condition d’erreur, ou si vous devez forcer l’arrêt de l’exécution d’une instance de processus, vous pouvez arrêter l’instance de processus.

Vous pouvez arrêter les instances de processus ayant un état quelconque.

Lorsque vous arrêtez une instance de processus, son état devient TERMINATING, puis TERMINATED, et le processus s’arrête à son opération actuelle. Aucune autre opération n’est exécutée et toutes les opérations et tâches associées sont arrêtées.

1. Dans Administration Console, cliquez sur Services > Processus Forms > Processus Forms.
1. Sur la page Instance du processus, sélectionnez le processus, puis cliquez sur Arrêter.

## Utilisation des détails d’instance de processus {#working-with-process-instance-details}

La page Détails de l’instance de processus affiche l’historique d’une instance de processus.

La zone Résumé affiche des informations de base sur l’instance de processus.

Dans l’onglet Opérations , chaque opération de l’instance de processus s’affiche dans l’ordre de la fin, du premier au dernier, avec les informations suivantes :

**Nom de l’opération :** nom de l’opération, tel que défini dans Workbench.

**Statut :** indique si l’opération est exécutée normalement ou si elle est arrêtée. (voir A propos des états d’instances de processus).

**Nom de la branche :** nom de la branche, tel que défini dans Workbench.

**Date de début :** date et heure auxquelles l’opération a été lancée.

**Date d’achèvement :** date et heure auxquelles l’opération s’est achevée.

Un sous-processus est une instance de processus démarrée par un autre processus et s’exécute indépendamment de cet autre processus. Les sous-processus ne s’affichent que s’ils ont été conçus dans le cadre du processus dans Workbench. Dans l’onglet Sous-processus , chaque sous-processus est affiché avec les informations suivantes :

**Identifiant du processus :** entier positif attribué par Forms Workflow lorsque le processus est instancié (démarré par un utilisateur ou une étape automatisée). Vous pouvez utiliser cet identificateur pour assurer le suivi de l’instance du processus sur l’ensemble de son cycle de vie.

**Nom du processus - Version :** nom du processus, tel que défini dans Designer.

**Statut :** indique si l’instance de processus fonctionne normalement, change d’état ou s’est arrêtée. (voir A propos des états d’instances de processus).

**Date de création :** date et heure auxquelles le processus secondaire a été créé.

**Date de mise à jour :** date et heure du dernier changement de statut du processus secondaire.

Vous pouvez effectuer les tâches suivantes sur la page Détails de l’instance du processus :

* Sélectionnez une opération pour en afficher les détails. Lorsque vous sélectionnez une opération, la page Détails de l’opération s’affiche.
* Sélectionnez un sous-processus pour afficher les détails le concernant. Lorsque vous sélectionnez un processus secondaire, la page Détails de l’instance du processus s’affiche.
* Arrêtez ou relancez des opérations ou des sous-processus, selon leur état.

### A propos des statuts des opérations {#about-operation-statuses}

Une opération (une étape dans un processus) peut avoir les états suivants :

**ACHEVÉ :** l’opération s’est achevée.

**EN COURS :** l’opération est exécutée normalement. Il est possible qu’elle reçoive des entrées utilisateur ou qu’elle attende une interaction utilisateur, ou encore qu’une étape automatisée soit en cours.

**BLOQUÉ :** un problème est survenu pendant le traitement de l’opération. Recherchez l’erreur ou l’exception dans la page Opérations bloquées.

**INTERROMPU :** l’opération a été arrêtée par un administrateur.

### Arrêt des opérations ou des sous-processus {#terminate-operations-or-subprocesses}

Si une opération ou un sous-processus a bloqué ou a rencontré une autre condition d’erreur, ou si vous devez forcer l’arrêt de l’exécution d’une opération ou d’un sous-processus, vous pouvez l’arrêter.

Vous pouvez arrêter une opération qui est EN COURS.

Lorsque vous arrêtez une opération, son état devient TERMINÉ. L’opération ne se termine pas et l’instance de processus s’arrête.

Vous pouvez arrêter un sous-processus qui a un état quelconque.

Lorsque vous arrêtez un sous-processus, son état devient TERMINATING, puis TERMINATED, et l’instance de processus s’arrête à ses opérations actuelles. Aucune autre opération n’est exécutée dans le sous-processus, bien que l’instance de processus parente continue de s’exécuter.

Vous ne pouvez pas arrêter les processus dont le diagramme de processus contient des éléments de passerelle. Si vous tentez d’arrêter ces types de processus, les opérations dans les éléments de passerelle ne sont pas affectées. Pour arrêter les opérations qui se trouvent dans un élément de passerelle, vous devez arrêter directement les opérations.

1. Sur la page Détails de l’instance du processus, cliquez sur l’onglet Opérations ou Sous-processus .
1. Sélectionnez l’opération ou le sous-processus, puis cliquez sur Arrêter.

### Réessayer une opération {#retry-an-operation}

Vous pouvez effectuer une nouvelle opération dont l’état est BLOQUÉ.

Lorsque vous essayez de relancer une opération, une requête est envoyée au processus des formulaires pour redémarrer l’opération. Si la requête aboutit, l’état devient EN COURS. Si l’opération ne peut pas être redémarrée, elle reste bloquée et vous devrez peut-être l’arrêter.

1. Sur la page Détails de l’instance du processus, cliquez sur l’onglet Opérations .
1. Sélectionnez l’opération et cliquez sur Réessayer.

## Utilisation des opérations {#working-with-operations}

La page Détails de l’opération présente un résumé d’une opération dans un processus et ses affectations d’utilisateurs actuelles.

1. Dans Administration Console, cliquez sur Services > Processus Forms > Processus Forms.
1. Cliquez sur le nom d’un processus pour afficher ses instances de processus. Cliquez sur une instance de processus pour afficher la page Détails de l’instance du processus, puis sélectionnez une opération pour afficher la page Détails de l’opération .

   Pour chaque tâche, la liste affiche les informations suivantes :

   **Nom du processus - Version :** nom du processus, tel que défini dans Workbench.

   **Application :** application à laquelle appartient le processus, tel que défini dans Workbench.

   **Statut :** actif signifie que le processus est celui qui est activé pour la version du processus. Inactif signifie que le processus est une ancienne version qui comporte toujours des instances de processus.

   **Date de création :** date et heure auxquelles le processus a été déployé.
