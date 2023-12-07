---
title: Synchroniser des annuaires
description: Découvrez comment synchroniser la base de données User Management avec les modifications apportées aux serveurs d’annuaire sources à l’aide d’une synchronisation manuelle ou planifiée.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: cb642289-4137-4ba7-8bde-0e458c8c94fe
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1003'
ht-degree: 11%

---

# Synchroniser des annuaires {#synchronizing-directories}

Pour synchroniser des domaines, vous pouvez choisir d’effectuer une synchronisation manuelle ou planifiée. A *synchronisation manuelle* synchronise les domaines sélectionnés. A *synchronisation planifiée* synchronise tous les domaines.

La synchronisation des annuaires permet d’extraire, dans la base de données User Management, les détails des serveurs d’annuaire que vous avez spécifiés dans les paramètres d’annuaire. Par la suite, vous pouvez également effectuer une synchronisation manuelle si des modifications ou des mises à jour se produisent sur les serveurs d’annuaire. Par exemple, vous pouvez effectuer une synchronisation manuelle si des utilisateurs et des groupes sont ajoutés ou si des modifications sont apportées au compte d’un utilisateur.

Vous pouvez également définir une synchronisation quotidienne pour synchroniser automatiquement la base de données User Management avec les modifications ou mises à jour apportées aux serveurs d’annuaire sources. Toutefois, ce processus utilise des ressources réseau et serveur. Choisissez des périodes de faible utilisation et évitez de planifier des synchronisations inutiles qui bloquent les ressources système et réseau. Pour minimiser les synchronisations inutiles, utilisez plutôt l’option de synchronisation immédiate.

Vous pouvez également indiquer s’il faut transmettre des informations sur les utilisateurs et les groupes dans Adobe LiveCycle Content Services 9 (obsolète) lors de la synchronisation des domaines.

>[!NOTE]
>
>Ne créez pas plusieurs utilisateurs et groupes locaux pendant la synchronisation d&#39;un annuaire LDAP. Toute tentative est susceptible d’entraîner des erreurs.

>[!NOTE]
>
>Si le processus de synchronisation des domaines est interrompu (par exemple, le serveur d’applications est arrêté pendant le processus), patientez avant de tenter de synchroniser le domaine. Pour évaluer l’état de la synchronisation, observez l’état. Si User Management a acquis un verrou avant l’arrêt, attendez 10 minutes que le verrou soit libéré après le redémarrage du serveur. Si l’état de synchronisation est &quot;En cours&quot; mais que la synchronisation est interrompue ou bloquée, User Management effectue une nouvelle synchronisation après 3 minutes. Après trois tentatives infructueuses, User Management déclare l’échec de la synchronisation et relâche le verrou.

>[!NOTE]
>
>Adobe® LiveCycle® Content Services ES (obsolète) est un système de gestion de contenu installé avec LiveCycle. Il permet aux utilisateurs de concevoir, gérer, surveiller et optimiser des processus pour des intervenants humains. La prise en charge de Content Services (obsolète) prend fin le 12/31/2014. Consultez le[ Document sur le cycle de vie des produits Adobe](https://www.adobe.com/fr/support/products/enterprise/eol/eol_matrix.html).

## Activation de la synchronisation des annuaires delta {#enable-delta-directory-synchronization}

La synchronisation différentielle des annuaires améliore l’efficacité de la synchronisation des annuaires. Lorsque la synchronisation différentielle des annuaires est activée, User Management synchronise uniquement les utilisateurs et les groupes qui ont été ajoutés ou mis à jour depuis la dernière synchronisation.

User Management effectue les étapes suivantes lorsque la synchronisation d’annuaires delta est activée :

* Récupérez tous les utilisateurs des serveurs d’annuaire, mais mettez à jour la base de données User Management uniquement avec les utilisateurs dont l’horodatage a été modifié.
* Récupérez tous les groupes, mais mettez à jour la base de données User Management uniquement avec les groupes dont l’horodatage a été modifié.
* Récupérez les membres du groupe uniquement pour les groupes dont les horodatages ont été modifiés et mettez à jour la base de données User Management avec ces informations.

>[!NOTE]
>
>Les utilisateurs et les groupes supprimés de l’annuaire ne sont pas supprimés de la base de données User Management tant que vous n’effectuez pas une synchronisation complète des annuaires.

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des domaines.
1. Sous Synchronisation delta, cochez la case et cliquez sur Enregistrer.
1. Modifiez les paramètres d’annuaire de chacun des domaines d’entreprise qui utiliseront la fonction de synchronisation d’annuaires delta. Dans les pages Paramètres utilisateur et Paramètres du groupe, recherchez le paramètre Modifier l’horodatage et affectez-lui la valeur `modify TimeStamp`. Pour plus d’informations sur la modification des domaines d’entreprise, voir [Modification et conversion de domaines](/help/forms/using/admin-help/editing-converting-existing-domains.md#editing-and-converting-existing-domains).

## Activation ou désactivation de la journalisation détaillée lors de la synchronisation {#enable-or-disable-detailed-logging-during-synchronization}

Par défaut, User Management consigne les statistiques détaillées pendant le processus de synchronisation.

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Configuration > Configurer les attributs système avancés.
1. Sous Journalisation des statistiques de synchronisation, décochez la case pour désactiver la journalisation détaillée ou sélectionnez-la pour activer la journalisation, puis cliquez sur Enregistrer.

## Configuration de l’option de nouvelle synchronisation des annuaires {#configure-the-directory-synchronization-retry-option}

Vous pouvez configurer User Management de manière à ce qu’il vérifie périodiquement si des tentatives de synchronisation d’annuaires ont échoué. User Management tente ensuite d’effectuer les synchronisations ayant échoué.

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Configuration > Configurer les attributs système avancés.
1. Sous Expression cron d’achèvement de synchronisation, saisissez une expression cron qui représente l’intervalle auquel User Management tente de relancer les synchronisations ayant échoué. L’utilisation de l’expression cron est basée sur le système de planification des tâches Open Source Quartz, version 1.4.0.

   La valeur par défaut est 0 0/13 &amp;ast; ? &amp;ast; , ce qui signifie que la vérification survient toutes les 13 minutes.

## Synchronisation manuelle des répertoires {#manually-synchronize-directories}

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des domaines.
1. (Facultatif) Pour transmettre des informations sur les utilisateurs et les groupes à Content Services (obsolète), sélectionnez l’option Sélectionner cette option pour pousser les utilisateurs et les groupes vers des fournisseurs de stockage d’entités de sécurité externes enregistrés . Cette option s’applique également lors de l’ajout de nouveaux utilisateurs et groupes via la page Utilisateurs et groupes .
1. Cochez la case correspondant à chaque domaine d’entreprise à synchroniser, puis cliquez sur Synchroniser maintenant.

   Si vous sélectionnez plusieurs domaines, la synchronisation des domaines pour tous les domaines peut être exécutée en même temps. Toutefois, si vous sélectionnez les domaines séparément, une seule synchronisation de domaine peut s’exécuter à la fois.

## Synchronisation des annuaires {#schedule-directory-synchronization}

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des domaines.
1. Planification de la synchronisation :

   * Pour activer une synchronisation automatique quotidienne, sélectionnez Se produit sous Planificateur. Sélectionnez Quotidienne dans la liste et saisissez l’heure au format 24 heures dans la zone correspondante. Lorsque vous enregistrez vos paramètres, cette valeur est convertie en expression cron, qui s’affiche dans la zone Expression cron .
   * Pour planifier la synchronisation un jour particulier de la semaine ou du mois, ou pendant un mois spécifique, sélectionnez Expression cron et saisissez l’expression appropriée dans la zone. Par exemple, synchronisez à 13 h 30 le dernier vendredi du mois.

L’utilisation de l’expression cron est basée sur le système de planification des tâches Open Source Quartz, version 1.4.0.

* Pour désactiver la synchronisation automatique, sélectionnez Se produit, puis Jamais dans la liste.
* (Facultatif) Pour transmettre des informations sur les utilisateurs et les groupes à Content Services (obsolète), sélectionnez l’option Sélectionner cette option pour pousser les utilisateurs et les groupes vers des fournisseurs de stockage d’entités de sécurité externes enregistrés . Cette option s’applique également lors de l’ajout de nouveaux utilisateurs et groupes via la page Utilisateurs et groupes .
* Cliquez sur Enregistrer.

## Arrêter toutes les synchronisations de répertoires en cours {#stop-all-directory-synchronizations-currently-in-progress}

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des domaines.
1. Cliquez sur Abandonner. Ce bouton s’affiche uniquement lorsqu’une synchronisation d’annuaires est en cours.
