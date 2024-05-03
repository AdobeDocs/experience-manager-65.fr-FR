---
title: Synchroniser des annuaires
description: Découvrez comment synchroniser la base de données User Management avec les modifications apportées aux serveurs de répertoire sources à l’aide d’une synchronisation manuelle ou planifiée.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: cb642289-4137-4ba7-8bde-0e458c8c94fe
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1003'
ht-degree: 100%

---

# Synchroniser des annuaires {#synchronizing-directories}

Pour synchroniser des domaines, vous pouvez choisir d’effectuer une synchronisation manuelle ou planifiée. Une *synchronisation manuelle* synchronise les domaines sélectionnés. Une *synchronisation planifiée* synchronise tous les domaines.

La synchronisation des annuaires permet d’extraire, dans la base de données User Management, les détails des serveurs d’annuaire que vous avez spécifiés dans les paramètres d’annuaire. Vous pouvez effectuer par la suite une synchronisation manuelle en cas de modification ou de mise à jour des serveurs d’annuaire. Par exemple, vous pouvez effectuer une synchronisation manuelle si des utilisateurs, des utilisatrices et des groupes sont ajoutés ou si des modifications sont apportées au compte d’un utilisateur ou d’une utilisatrice.

Vous pouvez également définir une synchronisation quotidienne pour harmoniser automatiquement la base de données User Management avec les modifications ou les mises à jour effectuées sur les serveurs d’annuaire sources. Toutefois, ce processus utilise des ressources réseau et serveur. Choisissez des périodes de faible utilisation et évitez de planifier des synchronisations inutiles qui bloquent les ressources système et réseau. Pour minimiser les synchronisations inutiles, utilisez plutôt l’option de synchronisation immédiate.

Vous pouvez également indiquer s’il convient d’envoyer des informations relatives aux utilisateurs, aux utilisatrices et aux groupes dans LiveCycle Content Services 9 (obsolète) lors de la synchronisation de domaines.

>[!NOTE]
>
>Ne créez pas plusieurs utilisateurs, utilisatrices et groupes locaux lorsqu’une synchronisation d’annuaire LDAP est en cours. Toute tentative est susceptible d’entraîner des erreurs.

>[!NOTE]
>
>Si le processus de synchronisation des domaines est interrompu (par exemple, le serveur d’applications est arrêté pendant le processus), patientez avant de tenter de synchroniser le domaine. Pour évaluer la synchronisation, observez son état. Si User Management a appliqué un verrou avant l’arrêt, patientez dix minutes pour son déverrouillage après le redémarrage du serveur. Si le statut de synchronisation est « En cours » mais que la synchronisation a été interrompue ou bloquée, User Management tente une nouvelle synchronisation après 3 minutes. Après trois tentatives infructueuses, User Management déclare l’échec de la synchronisation et procède au déverrouillage.

>[!NOTE]
>
>Remarque : Adobe® LiveCycle® Content Services ES (obsolète) est un système de gestion de contenu installé avec LiveCycle. Il permet aux utilisateurs et utilisatrices de concevoir, de gérer, de surveiller et d’optimiser des processus pour des intervenants humains. La prise en charge de Content Services (obsolète) s’est terminée le 31/12/2014. Consultez le[ Document sur le cycle de vie des produits Adobe](https://www.adobe.com/fr/support/products/enterprise/eol/eol_matrix.html).

## Activation de la synchronisation différentielle d’annuaires {#enable-delta-directory-synchronization}

La synchronisation différentielle des annuaires améliore l’efficacité de la synchronisation des annuaires. Lorsque la synchronisation différentielle des annuaires est activée, User Management synchronise uniquement les utilisateurs, les utilisatrices et les groupes qui ont été ajoutés ou mis à jour depuis la dernière synchronisation.

Lorsque la synchronisation différentielle des annuaires est activée, User Management effectue les étapes suivantes :

* récupération de l’ensemble des utilisateurs et utilisatrices des serveurs d’annuaire, mais mise à jour de la base de données User Management uniquement avec les utilisateurs et utilisatrices dont l’horodatage a été modifié ;
* récupération de tous les groupes, mais mise à jour de la base de données User Management uniquement avec les groupes dont l’horodatage a été modifié ;
* récupération des membres de groupes uniquement pour les groupes dont l’horodatage a été modifié et mise à jour de la base de données User Management avec ces informations.

>[!NOTE]
>
>Les utilisateurs, les utilisatrices et les groupes supprimés de l’annuaire ne sont pas supprimés de la base de données User Management tant que vous n’effectuez pas une synchronisation complète de l’annuaire.

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des domaines.
1. Sous Synchronisation différentielle, cochez la case et cliquez sur Enregistrer.
1. Modifiez les paramètres d’annuaire de chacun des domaines d’entreprise qui utiliseront la fonction de synchronisation différentielle d’annuaires. Dans les pages Paramètres utilisateur et Paramètres du groupe, recherchez le paramètre Modifier l’horodatage et affectez-lui la valeur `modify TimeStamp`. Pour plus d’informations sur la modification des domaines d’entreprise, voir [Modification et conversion de domaines existants](/help/forms/using/admin-help/editing-converting-existing-domains.md#editing-and-converting-existing-domains).

## Activation ou désactivation de la journalisation détaillée lors de la synchronisation {#enable-or-disable-detailed-logging-during-synchronization}

Par défaut, User Management consigne les statistiques détaillées pendant le processus de synchronisation.

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Configuration > Configurer les attributs système avancés.
1. Sous Journalisation des statistiques de synchronisation, décochez la case pour désactiver la journalisation détaillée ou sélectionnez-la pour activer la journalisation, puis cliquez sur Enregistrer.

## Configuration de l’option de nouvelle synchronisation des annuaires {#configure-the-directory-synchronization-retry-option}

Vous pouvez configurer User Management de manière à ce qu’il vérifie périodiquement si des tentatives de synchronisation d’annuaires ont échoué. User Management tente ensuite de terminer les synchronisations ayant échoué.

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Configuration > Configurer les attributs système avancés.
1. Sous Expression cron d’achèvement de synchronisation, saisissez une expression cron qui représente l’intervalle auquel User Management tente de relancer les synchronisations ayant échoué. L’utilisation de l’expression cron est basée sur le système de planification des tâches open source Quartz, version 1.4.0.

   La valeur par défaut est 0 0/13 &amp;ast; ? &amp;ast; , ce qui signifie que la vérification survient toutes les 13 minutes.

## Synchronisation manuelle des annuaires {#manually-synchronize-directories}

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des domaines.
1. (Facultatif) Pour envoyer des informations sur les utilisateurs, les utilisatrices et les groupes à Content Services (obsolète), activez Sélectionnez cette option pour forcer les utilisateurs, les utilisatrices et les groupes à devenir des fournisseurs de stockage de principaux de sécurité externes enregistrés. Cette option s’applique également lors de l’ajout d’utilisateurs, d’utilisatrices et de groupes via la page Utilisateurs et groupes.
1. Cochez la case correspondant à chaque domaine d’entreprise à synchroniser, puis cliquez sur Synchroniser maintenant.

   Si vous sélectionnez plusieurs domaines, il est possible de les synchroniser simultanément. Cependant, si vous sélectionnez les domaines séparément, un seul domaine est synchronisé à la fois.

## Planification de la synchronisation des annuaires {#schedule-directory-synchronization}

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des domaines.
1. Planifiez la synchronisation :

   * Pour activer une synchronisation automatique quotidienne, sélectionnez Se produit sous Planificateur. Sélectionnez Quotidiennement dans la liste, puis saisissez l’heure au format 24 heures dans la zone correspondante. Lorsque vous enregistrez vos paramètres, cette valeur est convertie en une expression cron qui s’affiche dans la zone Expression Cron.
   * Pour planifier la synchronisation un jour donné de la semaine ou du mois, ou au cours d’un mois donné, sélectionnez Expression Cron et saisissez l’expression appropriée dans la zone. Par exemple, synchronisez à 13 h 30 le dernier vendredi du mois.

L’utilisation de l’expression cron est basée sur le système de planification des tâches open source Quartz, version 1.4.0.

* Pour désactiver la synchronisation automatique, sélectionnez Se produit, puis Jamais dans la liste.
* (Facultatif) Pour envoyer des informations sur les utilisateurs, les utilisatrices et les groupes à Content Services (obsolète), activez Sélectionnez cette option pour forcer les utilisateurs, les utilisatrices et les groupes à devenir des fournisseurs de stockage de principaux de sécurité externes enregistrés. Cette option s’applique également lors de l’ajout d’utilisateurs, d’utilisatrices et de groupes via la page Utilisateurs et groupes.
* Cliquez sur Enregistrer.

## Arrêter toutes les synchronisations de répertoire en cours {#stop-all-directory-synchronizations-currently-in-progress}

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des domaines.
1. Cliquez sur Abandonner. Ce bouton s’affiche uniquement lorsqu’une synchronisation de répertoire est en cours.
