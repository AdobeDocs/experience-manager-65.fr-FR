---
title: Synchronisation d’annuaires
seo-title: Synchronisation d’annuaires
description: Découvrez comment synchroniser la base de données User Management avec des modifications apportées aux serveurs d’annuaire sources à l’aide de la synchronisation manuelle ou planifiée.
seo-description: Découvrez comment synchroniser la base de données User Management avec des modifications apportées aux serveurs d’annuaire sources à l’aide de la synchronisation manuelle ou planifiée.
uuid: 71cbc04d-6172-49b7-a490-ff3233c1b2bb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7ec0698a-9e6e-48d4-bba2-5a6eee313900
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1040'
ht-degree: 97%

---


# Synchronisation d’annuaires {#synchronizing-directories}

Vous pouvez synchroniser les domaines manuellement ou de manière programmée. Une *synchronisation manuelle* synchronise les domaines sélectionnés. Une *synchronisation programmée* synchronise tous les domaines.

La synchronisation des annuaires permet d’extraire les détails des serveurs d’annuaire que vous avez indiqués dans les paramètres d’annuaire et de les placer dans la base de données User Management. Vous pouvez effectuer par la suite une synchronisation manuelle en cas de modification ou de mise à jour des serveurs d’annuaire. Par exemple, vous pouvez effectuer une synchronisation manuelle en cas d’ajout d’utilisateurs et de groupes ou de modifications apportées au compte d’un utilisateur.

Vous pouvez également définir une synchronisation quotidienne pour harmoniser automatiquement la base de données User Management avec les modifications ou les mises à jour effectuées sur les serveurs d’annuaire sources, mais notez que ce processus utilise des ressources réseau et serveur. Choisissez des périodes de faible utilisation et évitez de programmer des synchronisations inutiles susceptibles d’immobiliser les ressources système et réseau. Pour éviter ce type de synchronisation, il est préférable d’utiliser l’option de synchronisation immédiate.

Vous pouvez également indiquer s’il convient d’envoyer des informations relatives aux utilisateurs et aux groupes dans LiveCycle Content Services 9 (obsolète) lors de la synchronisation de domaines.

>[!NOTE]
>
>ne créez pas plusieurs utilisateurs et groupes locaux lorsque l’annuaire LDAP est en cours de synchronisation. Toute tentative est susceptible d’entraîner des erreurs.

>[!NOTE]
>
>si la synchronisation des domaines s’interrompt, quelle qu’en soit la raison (par exemple, si le serveur d’applications s’arrête pendant le processus), patientez avant toute nouvelle tentative de synchronisation du domaine. Pour évaluer la synchronisation, consultez son état. Si User Management a appliqué un verrou avant l’arrêt, patientez dix minutes pour son déverrouillage après le redémarrage du serveur. Si l’état indique « En cours » mais que la synchronisation a été interrompue ou bloquée, User Management tente une nouvelle synchronisation après trois minutes. Après trois tentatives infructueuses, User Management déclare l’échec de la synchronisation et procède au déverrouillage.

>[!NOTE]
>
>Adobe® LiveCycle® Content Services ES (obsolète) est un système de gestion de contenu installé avec LiveCycle. Il permet aux utilisateurs de concevoir, gérer, surveiller et optimiser des processus pour des intervenants humains. La prise en charge de Content Services (obsolète) s’est terminée le 31/12/2014. Consultez le[ Document sur le cycle de vie des produits Adobe](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html). Pour savoir comment configurer Content Services (obsolète), consultez [Administration de Content Services](https://help.adobe.com/en_US/livecycle/9.0/admin_contentservices.pdf).

## Activation de la synchronisation d’annuaires Delta {#enable-delta-directory-synchronization}

La synchronisation différentielle des annuaires améliore l’efficacité de la synchronisation des annuaires. Lorsque la synchronisation différentielle des annuaires est activée, User Management synchronise uniquement les utilisateurs et les groupes qui ont été ajoutés et mis à jour depuis la dernière synchronisation.

Lorsque la synchronisation d’annuaires Delta est activée, User Management effectue les étapes suivantes :

* récupération de tous les utilisateurs des serveurs d’annuaire, mais mise à jour de la base de données User Management uniquement avec les utilisateurs dont l’horodatage a été modifié ;
* récupération de tous les groupes, mais mise à jour de la base de données User Management uniquement avec les groupes dont l’horodatage a été modifié ;
* récupération des membres de groupes uniquement pour les groupes dont l’horodatage a été modifié et mise à jour de la base de données User Management avec ces informations.

>[!NOTE]
>
>les utilisateurs et les groupes supprimés de l’annuaire ne sont pas supprimés de la base de données User Management avant la synchronisation complète de l’annuaire.

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des domaines.
1. Sous Synchronisation des modifications Delta, cochez la case et cliquez sur Enregistrer.
1. Modifiez les paramètres de chacun des domaines d’entreprise destinés à utiliser la fonctionnalité de synchronisation d’annuaires delta. Dans les pages Paramètres utilisateur et Paramètres du groupe, recherchez le paramètre Modifier l’horodatage et affectez-lui la valeur `modify TimeStamp`. Pour plus d’informations sur la modification des domaines d’entreprise, voir [Modification et conversion de domaines existants](/help/forms/using/admin-help/editing-converting-existing-domains.md#editing-and-converting-existing-domains).

## Activation ou désactivation de la journalisation détaillée lors de la synchronisation  {#enable-or-disable-detailed-logging-during-synchronization}

Par défaut, User Management crée un journal des statistiques détaillées pendant le processus de synchronisation.

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Configuration > Configurer les attributs système avancés.
1. Sous Consignation de statistiques de synchronisation, désélectionnez la case afin de désactiver la journalisation détaillée ou cochez-la pour l’activer, puis cliquez sur Enregistrer.

## Configuration de l’option de nouvelle synchronisation des annuaires  {#configure-the-directory-synchronization-retry-option}

Vous pouvez configurer User Management de manière à ce qu’il vérifie périodiquement si des tentatives de synchronisation d’annuaires ont échoué. User Management tente ensuite de terminer ces tentatives de synchronisation échouées.

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Configuration > Configurer les attributs système avancés.
1. Sous Expression cron d’achèvement de synchronisation, saisissez une expression cron représentant l’intervalle auquel User Management tente d’effectuer à nouveau les synchronisations ayant échoué. L’utilisation de l’expression cron est basée sur le système de planification des tâches Open Source de Quartz, version 1.4.0 

   La valeur par défaut est 0 0/13 &amp;ast; ? &amp;ast; , ce qui signifie que la vérification a lieu toutes les 13 minutes.

## Synchronisation manuelle des annuaires {#manually-synchronize-directories}

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des domaines.
1. (Facultatif) Pour envoyer des informations sur les utilisateurs et les groupes à Content Services (obsolète), activez Sélectionnez cette option pour forcer les utilisateurs et les groupes à devenir des fournisseurs de stockage d’entités de sécurité externes enregistrés. Cette option s’applique également lors de l’ajout de nouveaux utilisateurs et groupes via la page Utilisateurs et groupes.
1. Cochez la case correspondant à chaque domaine d’entreprise à synchroniser et cliquez sur Synchroniser maintenant.

   Si vous sélectionnez plusieurs domaines, il est possible de les synchroniser simultanément. Cependant, si vous sélectionnez les domaines séparément, un seul domaine est synchronisé à la fois.

## Programmation de la synchronisation des annuaires  {#schedule-directory-synchronization}

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des domaines.
1. Programmez la synchronisation :

   * Pour activer une synchronisation automatique quotidienne, sélectionnez Se produit sous Planificateur. Sélectionnez Quotidiennement dans la liste, et saisissez l’heure au format 24 heures dans la zone correspondante. Lorsque vous enregistrez vos paramètres, cette valeur est convertie en une expression cron qui s’affiche dans la zone Expression Cron.
   * Pour programmer la synchronisation pour un jour donné de la semaine ou du mois, ou au cours d’un mois donné, sélectionnez Expression cron et saisissez l’expression appropriée dans le champ. Vous pouvez, par exemple, programmer une synchronisation à 13:30 le dernier vendredi du mois.

L’utilisation de l’expression cron est basée sur le système de planification des tâches Open Source de Quartz, version 1.4.0 

* Pour désactiver la synchronisation automatique, sélectionnez Se produit, puis Jamais dans la liste.
* (Facultatif) Pour envoyer des informations sur les utilisateurs et les groupes à Content Services (obsolète), activez Sélectionnez cette option pour forcer les utilisateurs et les groupes à devenir des fournisseurs de stockage d’entités de sécurité externes enregistrés. Cette option s’applique également lors de l’ajout de nouveaux utilisateurs et groupes via la page Utilisateurs et groupes.
* Cliquez sur Enregistrer.

## Arrêt de toutes les synchronisations d’annuaires en cours  {#stop-all-directory-synchronizations-currently-in-progress}

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Gestion des domaines.
1. Cliquez sur Abandonner. Ce bouton apparaît uniquement lorsqu’une synchronisation d’annuaires est en cours.

