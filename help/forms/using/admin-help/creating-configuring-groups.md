---
title: Création et configuration de groupes
seo-title: Création et configuration de groupes
description: Découvrez comment créer des groupes de manière manuelle ou dynamique, modifier un groupe, afficher des détails sur un groupe ou supprimer un groupe.
seo-description: Découvrez comment créer des groupes de manière manuelle ou dynamique, modifier un groupe, afficher des détails sur un groupe ou supprimer un groupe.
uuid: 8532d72b-270a-4fcf-b7a5-56fca979a5fe
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 2058b501-65ce-4ad3-8e1b-b2eab896f70f
exl-id: 72edd8d1-8573-4942-8ced-1a100af58d78
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1593'
ht-degree: 97%

---

# Création et configuration de groupes{#creating-and-configuring-groups}

La création de groupes d’utilisateurs permet d’affecter des rôles au groupe et non à des utilisateurs isolés.

Deux types de groupes différents sont disponibles. Vous pouvez créer manuellement un groupe et y ajouter des utilisateurs, ainsi que d’autres groupes. Vous pouvez également créer des groupes dynamiques qui incluent automatiquement tous les utilisateurs répondant à un ensemble de règles spécifié.

Les utilisateurs appartenant à de nombreux groupes (500 ou plus par exemple) ou dont les groupes sont imbriqués profondément (30 niveaux) peuvent connaître un ralentissement du temps de réponse. Si vous rencontrez ce problème, vous pouvez configurer AEM forms pour la prélecture des informations provenant de certains domaines (voir [Configuration d’AEM forms pour la prélecture des informations de domaine](/help/forms/using/admin-help/configure-aem-forms-prefetch-domain.md#configure-aem-forms-to-prefetch-domain-information)).

## Création manuelle d’un groupe {#create-a-group-manually}

Lors de la création manuelle d’un groupe, vous pouvez ajouter des utilisateurs et d’autres groupes à ce dernier et lui affecter des rôles. Vous pouvez également associer le groupe à un groupe parent.

Si vous utilisez Content Services (obsolète), vous pouvez sélectionner l’option Sélectionnez cette option pour forcer les utilisateurs et les groupes à devenir des fournisseurs de stockage d’entités de sécurité externes enregistrés dans la page Gestion des domaines pour envoyer les informations relatives aux utilisateurs ou groupes que vous créez dans Content Services (obsolète).

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Utilisateurs et groupes, puis sur Nouveau groupe.
1. Renseignez la section Paramètres généraux et cliquez sur Suivant. Le Nom canonique et le Nom du groupe sont des attributs obligatoires.

   Le Nom canonique est l’identificateur unique du groupe. Tous les utilisateurs et groupes d’un domaine doivent disposer d’un nom canonique unique. Cochez la case Généré par le système pour laisser User Management affecter une valeur unique au paramètre Nom canonique ou désélectionnez la case et saisissez une valeur personnalisée.

   Évitez d’utiliser des caractères de soulignement (_) dans les noms canoniques, par exemple `sample_group`. Lorsque vous recherchez des groupes à l’aide de leur nom canonique, les noms contenant des caractères de soulignement n’apparaissent pas dans les résultats.

1. Pour ajouter des utilisateurs et des groupes à ce nouveau groupe, cliquez sur Rechercher des utilisateurs/groupes et procédez comme suit :

   * Dans la zone Rechercher, saisissez vos critères de recherche.
   * Dans la liste Dans, sélectionnez Utilisateurs, Groupes ou Utilisateurs et groupes.
   * Dans la liste Utilisation, sélectionnez Nom, Adresse électronique ou ID utilisateur.
   * Sélectionnez le domaine, le nombre d’éléments à afficher, puis cliquez sur Rechercher.
   * Dans les résultats de la recherche, cochez les cases en regard des utilisateurs et des groupes à ajouter à ce nouveau groupe, puis cliquez sur OK.

1. Cliquez sur Suivant.
1. Pour ajouter ce nouveau groupe à d’autres groupes existants, cliquez sur Rechercher des groupes et procédez comme suit :

   * Dans la zone Rechercher, saisissez vos critères de recherche.
   * Sélectionnez le domaine, le nombre d’éléments à afficher, puis cliquez sur Rechercher.
   * Dans les résultats de la recherche, activez les cases à cocher correspondant aux groupes auxquels ajouter le nouveau groupe, puis cliquez sur OK.

1. Cliquez sur Suivant.
1. Pour affecter des rôles au groupe, cliquez sur Rechercher des rôles, activez les cases à cocher correspondant aux rôles à affecter, puis cliquez sur OK. Les utilisateurs d’un groupe héritent des rôles affectés au niveau du groupe.
1. Cliquez sur Terminer.

## Création d’un groupe dynamique  {#create-a-dynamic-group}

Dans un groupe dynamique, vous ne devez pas sélectionner les utilisateurs un à un. Il s’agit en fait de définir un ensemble de règles et tous les utilisateurs correspondant à ces règles sont automatiquement ajoutés au groupe dynamique.

Pour créer des groupes dynamiques, utilisez l’une de ces deux méthodes :

* Activation de la création automatique de groupes dynamiques à partir du domaine de messagerie, tels que @adobe.com. Lorsque vous activez cette fonction, le gestionnaire des utilisateurs crée un groupe dynamique pour chaque domaine d’adresse électronique unique dans la base de données AEM forms. Utilisez une expression cron pour définir la fréquence à laquelle Gestion des utilisateurs recherche de nouveaux domaines d’adresses électroniques dans la base de données AEM forms. Ces groupes dynamiques sont ajoutés au domaine local DefaultDom et sont nommés &quot;Tous les utilisateurs avec un *`[email domain]`* ID de courrier&quot;.
* Créer un groupe dynamique à partir de critères spécifiques, notamment le domaine de l’adresse électronique de l’utilisateur, la description, le nom canonique et le nom de domaine. Pour faire partie du groupe dynamique, un utilisateur doit répondre à l’ensemble des critères spécifiés. Pour définir une condition « ou », créez deux groupes dynamiques distincts et ajoutez-les tous les deux à un groupe local. Par exemple, adoptez cette démarche pour créer un groupe d’utilisateurs appartenant au domaine d’adresse électronique @adobe.com ou dont le nom canonique contient ou=adobe.com. Notez que les utilisateurs ne sont pas tenus de respecter ces deux conditions.

Un groupe dynamique contient uniquement des utilisateurs. Il ne peut pas contenir d’autres groupes. Cependant, un groupe dynamique peut appartenir à un groupe parent.

### Création automatique des groupes dynamiques à partir des domaines d’adresses électroniques  {#automatically-create-dynamic-groups-based-on-email-domains}

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Configuration > Configurer les attributs système avancés.
1. Activez la case à cocher située sous Création automatique de groupe dynamique.
1. Indiquez à quel moment User Manager recherchera de nouveaux domaines d’adresses électroniques. Cette recherche doit être postérieure à la synchronisation des domaines, car la création de groupes dynamiques n’est pertinente que lorsque la synchronisation des domaines est terminée.

   * Pour activer une synchronisation automatique quotidienne, saisissez l’heure au format 24 heures dans la zone Se produit Quotidiennement à. Lorsque vous enregistrez vos paramètres, cette valeur est convertie en expression cron, qui s’affiche dans la zone située au-dessous.
   * Pour programmer la synchronisation un jour donné de la semaine ou du mois, ou un mois donné, sélectionnez Expression cron et saisissez l’expression appropriée dans la zone. La valeur par défaut est `0 00 4 ? * *` (c’est-à-dire qu’elle est vérifiée à 4 heures du matin tous les jours).

      L’utilisation de l’expression cron est basée sur le système de planification des tâches Open Source de Quartz, version 1.4.0 

1. Cliquez sur Enregistrer.

### Création d’un groupe dynamique à partir de critères spécifiques  {#create-a-dynamic-group-based-on-specified-criteria}

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Utilisateurs et groupes.
1. Cliquez sur Nouveau groupe dynamique.
1. Renseignez la section Options générales. Nom du groupe est un attribut obligatoire. Vous pouvez assigner le groupe à n’importe quel domaine configuré.
1. Sous Critères de groupe dynamique, définissez un ou plusieurs attributs utilisés pour constituer le groupe dynamique.

   >[!NOTE]
   >
   >les attributs Adresse électronique, Description et Nom canonique sont sensibles à la casse lorsque vous utilisez l’opérateur Egal. Ces attributs ne sont pas sensibles à la casse lorsque vous utilisez les opérateurs Commence par, Se termine par ou Contient.

   **Adresse électronique :** domaine de l’adresse électronique de l’utilisateur, par exemple `@adobe.com`.

   **Description :** description de l’utilisateur, tel que « Informaticien ».

   **Nom canonique : nom canonique de l’utilisateur** , tel que  `ou=adobe.com`

   **Nom de domaine :** nom du domaine auquel l’utilisateur appartient, par exemple `DefaultDom`. L’attribut Nom de domaine est sensible à la casse lorsque vous utilisez l’opérateur Contient. Cet attribut n’est pas sensible à la casse lorsque vous utilisez les opérateurs Commence par, Se termine par ou Egal.

1. Cliquez sur Tester. Une page Test affiche les 200 premiers utilisateurs qui correspondent aux critères définis. Cliquez sur Fermer.
1. Si les résultats du test sont ceux attendus, cliquez sur Suivant. Dans le cas contraire, modifiez les critères du groupe dynamique et relancez le test.
1. Pour ajouter ce groupe dynamique à un groupe parent, cliquez sur Rechercher des groupes et procédez comme suit :

   * Dans la zone Rechercher, saisissez vos critères de recherche.
   * Sélectionnez le domaine, le nombre d’éléments à afficher, puis cliquez sur Rechercher.
   * Dans les résultats de la recherche, activez les cases à cocher correspondant aux groupes auxquels ajouter le groupe dynamique, puis cliquez sur OK.

1. Cliquez sur Suivant.
1. Pour affecter des rôles au groupe dynamique, cliquez sur Rechercher des rôles, activez les cases à cocher correspondant aux rôles à affecter, puis cliquez sur OK. Les utilisateurs d’un groupe héritent des rôles affectés au niveau du groupe.
1. Cliquez sur Terminer.

## Affichage des détails d’un groupe  {#view-details-about-a-group}

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Utilisateurs et groupes.
1. Dans la liste Dans, sélectionnez Groupe, puis cliquez sur Rechercher. Les résultats de recherche apparaissent au bas de la page. Vous pouvez trier la liste en cliquant sur les en-têtes de colonne.
1. Cliquez sur le nom du groupe dont vous souhaitez afficher les détails. La page Détails du groupe apparaît.
1. Pour afficher les membres directs du groupe, cliquez sur Entités de sécurité enfants.

## Modification d’un groupe  {#edit-a-group}

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Utilisateurs et groupes.
1. Pour rechercher le groupe à modifier, procédez comme suit :

   * Dans la zone Rechercher, saisissez vos critères de recherche.
   * Dans la liste Utilisation, sélectionnez Nom ou Adresse électronique.
   * Dans la liste Dans, sélectionnez Groupes.
   * Sélectionnez le domaine, le nombre d’éléments à afficher, puis cliquez sur Rechercher.
   * Dans les résultats de la recherche, cliquez sur le nom du groupe à modifier.

1. Dans l’onglet Détails, modifiez les options générales et cliquez sur Enregistrer.
1. Pour modifier les groupes associés, cliquez sur l’onglet Groupes parents et procédez comme suit :

   * Pour rechercher des groupes à ajouter à l’association, cliquez sur Rechercher des groupes et entrez les informations de recherche.
   * Pour ajouter des groupes, activez les cases à cocher correspondant aux groupes à ajouter, cliquez sur OK, puis sur Enregistrer.
   * Pour supprimer un groupe associé, cochez la case en regard du groupe à a supprimer, cliquez sur Supprimer, sur OK, puis sur Enregistrer.

1. Pour modifier les utilisateurs et les groupes contenus dans le groupe, cliquez sur l’onglet Entités de sécurité enfants et procédez comme suit :

   * Pour rechercher des utilisateurs et des groupes à ajouter, cliquez sur Rechercher des utilisateurs/groupes et entrez les informations de recherche.
   * Pour ajouter un utilisateur ou un groupe, cochez la case correspondante, cliquez sur OK, puis sur Enregistrer.
   * Pour supprimer un utilisateur ou un groupe, cochez la case correspondante, cliquez sur Supprimer, sur OK, puis sur Enregistrer.

1. Pour modifier des affectations de rôles, cliquez sur l’onglet Affectations de rôles et procédez comme suit :

   * Pour rechercher des rôles à affecter au groupe, cliquez sur Rechercher des rôles.
   * Pour ajouter un nouveau rôle, activez la case à cocher qui lui correspond, cliquez sur OK, puis sur Enregistrer.
   * Pour retirer l’affectation d’un rôle, activez la case à cocher qui lui correspond, cliquez sur Retirer, puis sur Enregistrer.

## Suppression d’un groupe  {#delete-a-group}

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Utilisateurs et groupes.
1. Dans la liste Rechercher, sélectionnez Groupes, puis cliquez sur Rechercher.
1. Activez la case à cocher située en regard du groupe à supprimer, cliquez sur Supprimer, puis sur OK.
