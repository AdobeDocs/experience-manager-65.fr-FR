---
title: Gestion de processus
seo-title: Gestion de processus
description: La page Liste de processus répertorie les processus initiés par un utilisateur ou démarrés automatiquement. Découvrez la gestion des processus.
seo-description: La page Liste de processus répertorie les processus initiés par un utilisateur ou démarrés automatiquement. Découvrez la gestion des processus.
uuid: 4cd17400-681a-4e40-996c-7dda57ce449a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 37e702c2-8716-4360-a3eb-d9877b28cc86
exl-id: 21a2317d-3542-4ccb-98db-3cedf20c89ea
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1656'
ht-degree: 74%

---

# Gestion de processus {#managing-processes}

La page Liste de processus répertorie les processus initiés par un utilisateur ou démarrés automatiquement.

1. Dans Administration Console, cliquez sur Services > Processus des formulaires > Processus des formulaires. La Liste de processus présente les informations suivantes :

   **Nom du processus - Version :**  nom du processus, tel que défini dans Workbench.

   **Application :** application à laquelle appartient le processus, telle que définie dans Workbench.

   **État :** Principal signifie que le processus est celui qui est activé pour la version de processus. Inactif signifie que le processus est une ancienne version qui comporte toujours des instances de processus.

   **Date de création :** date et heure de déploiement du processus.

1. Cliquez sur le nom d’un processus pour afficher les instances de ce processus dans la page Instance du processus.

## Utilisation d’instances de processus {#working-with-process-instances}

Si vous accédez à la page Instance du processus à partir de la page Liste de processus, toutes les instances de processus que vous avez sélectionnées sont répertoriées. Si vous accédez à la page Instance du processus après avoir exécuté une recherche, seules les instances de processus trouvées sont répertoriées.

Pour chaque instance de processus, la liste présente les informations suivantes :

**ID de processus :** identifiant attribué par le processus des formulaires lorsque le processus est instancié (c’est-à-dire lorsqu’un utilisateur ou une étape automatisée lance un processus). Vous pouvez utiliser cet identificateur pour assurer le suivi de l’instance du processus sur l’ensemble de son cycle de vie.

**Nom du processus - Version :**  nom du processus, tel que défini dans Workbench.

**État :** indique si l’instance de processus s’exécute normalement, change d’état ou s’est arrêtée. (voir A propos des états d’instances de processus).

**Date de création :** date et heure de création de l’instance de processus.

**Date de mise à jour :** date et heure de la dernière modification de l’état de l’instance de processus.

Dans la page Instance du processus, vous pouvez exécuter les tâches suivantes :

* Sélectionner une instance de processus pour afficher des informations détaillées sur cette instance comme, par exemple, ses opérations et ses processus secondaires. Lorsque vous sélectionnez une instance de processus, la page Détails de l’instance du processus s’affiche.
* Suspendre ou arrêter des instances de processus, ou encore en annuler la suspension.
* Rechercher une instance de processus. Pour lancer une recherche, cliquez sur Rechercher.

### A propos des états d’instances de processus  {#about-process-instance-statuses}

Une instance de processus, y compris ses processus secondaires, peut présenter les états suivants :

**TERMINÉ :** toutes les branches et opérations de l’instance de processus sont terminées. ACHEVE est l’état final d’une instance de processus.

**TERMINÉ :** l’état de l’instance de processus est sur le point de devenir TERMINÉ.

**INITIÉ :** l’instance de processus a été créée, mais n’est pas encore en cours d’exécution. INITIE est le premier état d’une instance de processus.

**EN COURS :**  l’instance de processus s’exécute normalement. Il est possible qu’une étape automatique soit en cours, ou que l’instance de processus reçoive des entrées utilisateur ou qu’elle soit en attente d’une interaction utilisateur.

**SUSPENDU :** l’instance de processus a été suspendue par un administrateur ou par une étape du processus. Aucune opération supplémentaire ne sera exécutée jusqu’au changement de l’état.

**SUSPENSION :** l’état est sur le point de devenir SUSPENDU. Si une opération a été conçue pour ignorer les requêtes de suspension et n’est pas encore achevée, cette opération doit s’achever avant que l’instance de processus soit suspendue.

**TERMINÉ :** l’instance de processus a été arrêtée par un administrateur.

**TERMINAISON :** l’état est sur le point de devenir TERMINÉ. Si une opération a été conçue pour ignorer les requêtes d’arrêt et n’est pas encore achevée, cette opération doit s’achever avant que l’instance de processus soit arrêtée.

**UNSUSPENDING :**  l’état est sur le point de passer à EN COURS après avoir été SUSPENDU.

>[!NOTE]
>
>Si une demande est envoyée pour changer l’état d’une instance de processus (par exemple, pour suspendre ou arrêter l’instance), la demande entre dans la file d’attente des commandes du processus des formulaires. Selon la taille de la file d’attente et la vitesse de traitement globale, il est possible que l’état affiché ne change pas avant que la page ait été rechargée une ou plusieurs fois.

### Suspension ou annulation de la suspension des instances de processus  {#suspend-or-unsuspend-process-instances}

Si vous devez dépanner un problème ou si vous savez qu’une instance de processus rencontrera un problème lors d’une étape ultérieure en raison d’une condition externe, vous pouvez suspendre temporairement l’instance de processus.

Vous pouvez suspendre les instances de processus dont l’état est EN COURS.

Lorsque vous suspendez une instance de processus, son état devient SUSPENSION EN COURS, puis SUSPENDU, et le processus s’interrompt momentanément au niveau de l’opération en cours. L’instance de processus conserve cet état jusqu’à ce que l’état soit défini sur NON SUSPENDU.

L’état d’une instance de processus ne peut être défini sur NON SUSPENDU que si l’état de cette instance est SUSPENDU.

Quand vous annulez la suspension d’une instance de processus, son état devient EN COURS et l’instance de processus continue à exécuter l’opération depuis l’endroit où elle avait été suspendue.

Lorsque vous suspendez une instance de processus qui a appelé d’autres processus (processus enfants) en utilisant leur opération d’appel, les processus enfants sont également suspendus.

1. Dans Administration Console, cliquez sur Services > Processus des formulaires > Processus des formulaires. 
1. Dans la page Instance du processus, sélectionnez le processus, puis cliquez sur Suspendre ou Non suspendu.

### Arrêt d’une instance de processus  {#terminate-a-process-instances}

Si une opération d’une instance de processus a bloqué ou a rencontré une autre condition d’erreur, ou si vous avez besoin de forcer l’arrêt de l’exécution d’une instance de processus, vous pouvez arrêter l’instance de processus.

Vous pouvez arrêter toutes les instances de processus, quel que soit leur état.

Une fois que vous avez terminé une instance de processus, son état devient PRESQUE TERMINE, puis TERMINE, et le processus s’arrête au niveau de l’opération en cours. Aucune opération supplémentaire n’est exécutée et toutes les opérations et les tâches associées sont arrêtées.

1. Dans Administration Console, cliquez sur Services > Processus des formulaires > Processus des formulaires. 
1. Dans la page Instance du processus, sélectionnez le processus, puis cliquez sur Arrêter.

## Utilisation de détails d’instances de processus  {#working-with-process-instance-details}

La page Détails de l’instance du processus affiche l’historique d’une instance de processus.

La zone Résumé présente des informations de base sur l’instance de processus.

Sur l’onglet Opérations, les opérations de l’instance de processus sont affichées dans l’ordre dans lequel elles se sont achevées, avec les informations suivantes :

**Nom de l’opération :** nom de l’opération, tel que défini dans Workbench.

**État :** indique si l’opération s’exécute normalement ou s’est arrêtée. (voir A propos des états d’instances de processus).

**Nom de branche :** nom de la branche, tel que défini dans Workbench.

**Date de début :** date et heure auxquelles l’opération a commencé.

**Date d’achèvement :** date et heure auxquelles l’opération s’est terminée.

Un processus secondaire est une instance de processus qui a été démarrée par un autre processus et qui s’exécute indépendamment de cet autre processus. Des processus secondaires ne sont affichés que s’ils ont été conçus comme faisant partie du processus dans Workbench. Sur l’onglet Processus secondaires, chaque processus secondaire est affiché avec les informations suivantes :

**ID de processus :** entier positif attribué par le processus des formulaires lorsque le processus est instancié (c’est-à-dire lorsqu’un utilisateur ou une étape automatisée lance le processus). Vous pouvez utiliser cet identificateur pour assurer le suivi de l’instance du processus sur l’ensemble de son cycle de vie.

**Nom du processus - Version :**  nom du processus, tel que défini dans Designer.

**État :** indique si l’instance de processus s’exécute normalement, change d’état ou s’est arrêtée. (voir A propos des états d’instances de processus).

**Date de création :** date et heure de création du sous-processus.

**Date de mise à jour :** date et heure de la dernière modification de l’état du sous-processus.

Dans la page Détails de l’instance du processus, vous pouvez exécuter les tâches suivantes :

* Sélectionner une opération pour afficher des informations détaillées sur cette opération. Si vous sélectionnez une opération, la page Détails de l’opération s’affiche.
* Sélectionner un processus secondaire pour afficher des informations détaillées sur ce processus secondaire. Lorsque vous sélectionnez un processus secondaire, la page Détails de l’instance du processus s’affiche.
* Arrêter ou essayer de relancer des opérations ou des processus secondaires, selon leur état.

### A propos des états d’opérations  {#about-operation-statuses}

Une opération (une étape dans un processus) peut présenter les états suivants :

**COMPLETE :** l’opération s’est terminée.

**EN COURS :** l’opération s’exécute normalement. Il est possible qu’elle reçoive des entrées utilisateur ou qu’elle attende une interaction utilisateur, ou encore qu’une étape automatisée soit en cours.

**BLOQUE :** un problème s’est produit pendant le traitement de l’opération. Recherchez l’erreur ou l’exception dans la page Opérations bloquées.

**TERMINÉ :** l’opération a été arrêtée par un administrateur.

### Arrêt d’opérations ou de processus secondaires {#terminate-operations-or-subprocesses}

Si une opération ou un processus secondaire a bloqué ou a rencontré une autre condition d’erreur, ou si vous avez besoin de forcer l’arrêt d’une opération ou d’un processus secondaire, vous pouvez arrêter cette opération ou ce processus secondaire.

Vous pouvez arrêter une opération dont l’état est EN COURS.

Lorsque vous arrêtez une opération, son état devient TERMINE. L’opération ne s’achève pas et l’exécution de l’instance de processus est interrompue.

Vous pouvez arrêter un processus secondaire, quel que soit son état.

Une fois que vous avez arrêté un processus secondaire, son état devient PRESQUE TERMINE, puis TERMINE, et l’instance de processus s’interrompt au niveau de l’opération en cours. Aucune opération supplémentaire n’est exécutée dans le processus secondaire, bien que l’instance de processus parente continue à être exécutée.

Vous ne pouvez pas arrêter des processus dont le schéma de processus contient des éléments de la passerelle. Si vous arrêtez ce type de processus, les opérations se trouvant dans les éléments de la passerelle ne sont pas concernées. Pour arrêter ces opérations, vous devez les arrêter directement.

1. Dans la page Détails de l’instance du processus, cliquez sur l’onglet Opérations ou Processus secondaires.
1. Sélectionnez l’opération ou le processus secondaire, puis cliquez sur Arrêter.

### Tentative de redémarrage d’une opération  {#retry-an-operation}

Vous pouvez essayer de relancer une opération dont l’état est BLOQUE.

Lorsque vous essayez de relancer une opération, une requête est envoyée au processus des formulaires pour redémarrer l’opération. Si la requête aboutit, l’état devient EN COURS. Si l’opération ne peut pas être redémarrée, son état reste BLOQUE ; il est possible que vous deviez alors l’arrêter.

1. Dans la page Détails de l’instance du processus, cliquez sur l’onglet Opérations.
1. Sélectionnez l’opération, puis cliquez sur Nouvel essai.

## Utilisation d’opérations  {#working-with-operations}

La page Détails de l’opération affiche le résumé d’une opération dans un processus et ses affectations d’utilisateurs actuelles.

1. Dans Administration Console, cliquez sur Services > Processus des formulaires > Processus des formulaires. 
1. Cliquez sur le nom d’un processus pour afficher ses instances. Cliquez sur une instance de processus pour afficher la page Détails de l’instance du processus, puis sélectionnez une opération pour afficher la page Détails de l’opération.

   Pour chaque tâche, la liste présente les informations suivantes :

   **Nom du processus - Version :**  nom du processus, tel que défini dans Workbench.

   **Application :** application à laquelle appartient le processus, telle que définie dans Workbench.

   **État :** Principal signifie que le processus est celui qui est activé pour la version de processus. Inactif signifie que le processus est une ancienne version qui comporte toujours des instances de processus.

   **Date de création :** date et heure de déploiement du processus.
