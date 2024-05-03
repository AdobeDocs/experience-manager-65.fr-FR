---
title: Créer et configurer des groupes
description: Découvrez comment créer des groupes manuellement ou dynamiquement, modifier un groupe, afficher des détails sur un groupe ou supprimer un groupe.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 72edd8d1-8573-4942-8ced-1a100af58d78
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1576'
ht-degree: 100%

---

# Créer et configurer des groupes{#creating-and-configuring-groups}

La création de groupes d’utilisateurs et utilisatrices vous permet d’affecter des rôles au groupe plutôt qu’à des personnes individuelles.

Deux types de groupes sont disponibles. Vous pouvez créer manuellement un groupe et y ajouter des personnes et d’autres groupes. Vous pouvez également créer des groupes dynamiques qui incluent automatiquement toutes les personnes qui répondent à un ensemble de règles spécifié.

Le temps de réponse peut être plus lent pour les personnes qui appartiennent à de nombreux groupes (par exemple, 500 ou plus) ou si les groupes sont profondément imbriqués (par exemple, 30 niveaux). Si vous rencontrez ce problème, vous pouvez configurer AEM Forms pour prérécupérer les informations de certains domaines. (Voir [Configurer AEM Forms pour prérécupérer les informations de domaine](/help/forms/using/admin-help/configure-aem-forms-prefetch-domain.md#configure-aem-forms-to-prefetch-domain-information)).

## Créer manuellement un groupe {#create-a-group-manually}

Lorsque vous créez manuellement un groupe, vous pouvez y ajouter des personnes et d’autres groupes, puis lui affecter des rôles. Vous pouvez également associer le groupe à un groupe parent.

Si vous utilisez Content Services (obsolète), vous pouvez sélectionner l’option « Sélectionner cette option pour forcer les utilisateurs, les utilisatrices et les groupes à devenir des fournisseurs de stockage d’entités de sécurité externes enregistrés sur la page Gestion des domaines » pour envoyer les informations relatives aux nouveaux utilisateurs, nouvelles utilisatrices ou nouveaux groupes que vous créez dans Content Services (obsolète).

1. Dans la console d’administration, cliquez sur Paramètres > Gestion des utilisateurs > Utilisateurs et groupes, puis cliquez sur Nouveau groupe.
1. Renseignez la section Paramètres généraux et cliquez sur Suivant. Le Nom canonique et le Nom du groupe sont des attributs obligatoires.

   Le Nom canonique est l’identificateur unique du groupe. Toutes les personnes et groupes d’un domaine doivent disposer d’un nom canonique unique. Cochez la case Généré par le système pour laisser User Management affecter une valeur unique au paramètre Nom canonique ou désélectionnez la case et saisissez une valeur personnalisée.

   Évitez d’utiliser les caractères de soulignement (_) dans les noms canoniques, par exemple `sample_group`. Lorsque vous recherchez des groupes à l’aide de leur nom canonique, les noms contenant des caractères de soulignement n’apparaissent pas dans les résultats.

1. Pour ajouter des personnes et des groupes à ce nouveau groupe, cliquez sur Rechercher des utilisateurs/groupes et procédez comme suit :

   * Dans la zone Rechercher, saisissez vos critères de recherche.
   * Dans la liste Dans, sélectionnez Utilisateurs, Groupes ou Utilisateurs et groupes.
   * Dans la liste Utilisation, sélectionnez Nom, Adresse électronique ou ID utilisateur.
   * Sélectionnez le domaine, le nombre d’éléments à afficher, puis cliquez sur Rechercher.
   * Dans les résultats de la recherche, cochez les cases en regard des personnes et des groupes à ajouter à ce nouveau groupe, puis cliquez sur OK.

1. Cliquez sur Suivant.
1. Pour ajouter ce nouveau groupe à d’autres groupes existants, cliquez sur Rechercher des groupes et procédez comme suit :

   * Dans la zone Rechercher, saisissez vos critères de recherche.
   * Sélectionnez le domaine, le nombre d’éléments à afficher, puis cliquez sur Rechercher.
   * Dans les résultats de la recherche, cochez les cases correspondant aux groupes auxquels ajouter le nouveau groupe, puis cliquez sur OK.

1. Cliquez sur Suivant.
1. Pour affecter des rôles au groupe, cliquez sur Rechercher des rôles, cochez les cases correspondant à chaque rôle à affecter au groupe, puis cliquez sur OK. Les personnes du groupe héritent des rôles affectés au niveau du groupe.
1. Cliquez sur Finish (Terminer). 

## Créer un groupe dynamique {#create-a-dynamic-group}

Dans un groupe dynamique, vous ne devez pas sélectionner les personnes une à une. Il s’agit en fait de définir un ensemble de règles pour que toutes les personnes correspondant à ces règles soient automatiquement ajoutées au groupe dynamique.

Pour créer des groupes dynamiques, utilisez l’une de ces deux méthodes :

* Activez la création automatique de groupes dynamiques à partir de domaines de messagerie, tels que @adobe.com. Lorsque vous activez cette fonction, User Management crée un groupe dynamique pour chaque domaine de messagerie unique dans la base de données AEM Forms. Utilisez une expression cron pour définir la fréquence à laquelle User Management recherche de nouveaux domaines de messagerie dans la base de données AEM Forms. Ces groupes dynamiques sont ajoutés au domaine local DefaultDom et sont appelés « Tous les utilisateurs avec un ID d’e-mail *`[email domain]`* ».
* Créez un groupe dynamique à partir de critères spécifiques, notamment le domaine de messagerie de la personne, la description, le nom canonique et le nom de domaine. Pour faire partie du groupe dynamique, une personne doit répondre à l’ensemble des critères spécifiés. Pour définir une condition « ou », créez deux groupes dynamiques distincts et ajoutez-les tous les deux à un groupe local. Par exemple, adoptez cette démarche pour créer un groupe de personnes appartenant au domaine de messagerie @adobe.com ou dont le nom canonique contient ou=adobe.com. Notez que les personnes ne sont pas tenues de respecter ces deux conditions.

Un groupe dynamique contient uniquement des utilisateurs et des utilisatrices. Il ne peut pas contenir d’autres groupes. Cependant, un groupe dynamique peut appartenir à un groupe parent.

### Créer automatiquement des groupes dynamiques à partir de domaines de messagerie {#automatically-create-dynamic-groups-based-on-email-domains}

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Configuration > Configurer les attributs système avancés.
1. Sous Création automatique de groupe dynamique, cochez la case.
1. Indiquez à quel moment User Manager recherche de nouveaux domaines de messagerie. Ce moment doit être postérieur à la synchronisation des domaines, car la création de groupes dynamiques n’est logique que si la synchronisation des domaines est terminée.

   * Pour activer une synchronisation automatique quotidienne, saisissez l’heure au format 24 heures dans la zone Se produit quotidiennement à. Lorsque vous enregistrez vos paramètres, cette valeur est convertie en expression cron, qui s’affiche dans la zone ci-dessous.
   * Pour planifier la synchronisation un jour particulier de la semaine ou du mois, ou pendant un mois spécifique, sélectionnez l’expression cron appropriée dans la case. La valeur par défaut est `0 00 4 ? * *` (ce qui se traduit par un contrôle à 4 heures du matin tous les jours).

     L’utilisation de l’expression cron est basée sur le système de planification des tâches open source Quartz, version 1.4.0.

1. Cliquez sur Enregistrer.

### Créer un groupe dynamique à partir de critères spécifiés {#create-a-dynamic-group-based-on-specified-criteria}

1. Dans la console d’administration, cliquez sur Paramètres > User Management > Utilisateurs et groupes.
1. Cliquez sur Nouveau groupe dynamique.
1. Renseignez la section Paramètres généraux. Le Nom du groupe est un attribut obligatoire. Vous pouvez affecter le groupe à n’importe quel domaine configuré.
1. Sous Critères de groupe dynamique, spécifiez un ou plusieurs attributs utilisés pour remplir le groupe dynamique.

   >[!NOTE]
   >
   >Les attributs E-mail, Description et Nom canonique sont sensibles à la casse lors de l’utilisation de l’opérateur Est égal à. Ils ne sont pas sensibles à la casse avec les opérateurs Commence par, Se termine par ou Contient.

   **Adresse électronique :** domaine de l’adresse électronique de l’utilisateur, par exemple `@adobe.com`.

   **Description :** description de l’utilisateur, tel que « Informaticien ».

   **Nom canonique :** nom canonique de l’utilisateur, tel que `ou=adobe.com`.

   **Nom de domaine :** nom du domaine auquel l’utilisateur appartient, par exemple `DefaultDom`. L’attribut Nom de domaine est sensible à la casse lors de l’utilisation de l’opérateur Contient. Il n’est pas sensible à la casse avec les opérateurs Commence par, Se termine par ou Est égal à.

1. Cliquez sur Tester. Une page Test affiche les 200 premiers utilisateurs ou utilisatrices qui répondent aux critères définis. Cliquez sur Fermer.
1. Si le test a renvoyé les résultats attendus, cliquez sur Suivant. Dans le cas contraire, modifiez les critères du groupe dynamique et effectuez à nouveau le test.
1. Pour ajouter le groupe dynamique à un groupe parent, cliquez sur Rechercher des groupes et procédez comme suit :

   * Dans la zone Rechercher, saisissez vos critères de recherche.
   * Sélectionnez le domaine, le nombre d’éléments à afficher, puis cliquez sur Rechercher.
   * Dans les résultats de recherche, cochez les cases correspondant aux groupes auxquels appartient le groupe dynamique et cliquez sur OK.

1. Cliquez sur Suivant.
1. Pour affecter des rôles au groupe dynamique, cliquez sur Rechercher des rôles, cochez les cases correspondant à chaque rôle à affecter au groupe, puis cliquez sur OK. Les personnes du groupe héritent des rôles affectés au niveau du groupe.
1. Cliquez sur Finish (Terminer). 

## Afficher les détails concernant un groupe {#view-details-about-a-group}

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Utilisateurs et groupes.
1. Dans la liste Dans, sélectionnez Groupe, puis cliquez sur Rechercher. Les résultats de la recherche apparaissent au bas de la page. Vous pouvez trier la liste en cliquant sur l’un des en-têtes de colonne.
1. Cliquez sur le nom du groupe dont vous souhaitez afficher les détails. La page Détails du groupe s’affiche.
1. Pour afficher les membres directs du groupe, cliquez sur Entités enfants.

## Modifier un groupe {#edit-a-group}

1. Dans la console d’administration, cliquez sur Paramètres > User Management > Utilisateurs et groupes.
1. Pour rechercher le groupe à modifier, procédez comme suit :

   * Dans la zone Rechercher, saisissez vos critères de recherche.
   * Dans la liste Utilisation, sélectionnez Nom ou E-mail.
   * Dans la liste Dans, sélectionnez Groupes.
   * Sélectionnez le domaine, le nombre d’éléments à afficher, puis cliquez sur Rechercher.
   * Dans les résultats de la recherche, cliquez sur le nom du groupe à modifier.

1. Dans l’onglet Détails, modifiez les options générales et cliquez sur Enregistrer.
1. Pour modifier les groupes associés, cliquez sur l’onglet Groupes parents et procédez comme suit :

   * Pour rechercher des groupes à ajouter à l’association, cliquez sur Rechercher des groupes et entrez les informations de recherche.
   * Pour ajouter des groupes, cochez les cases correspondantes aux groupes à ajouter, cliquez sur OK, puis sur Enregistrer.
   * Pour supprimer un groupe associé, cochez la case en regard du groupe à supprimer, cliquez sur Supprimer, sur OK, puis sur Enregistrer.

1. Pour modifier les utilisateurs, les utilisatrices et les groupes, cliquez sur l’onglet Entités enfants et procédez comme suit :

   * Pour rechercher des utilisateurs, des utilisatrices et des groupes à ajouter, cliquez sur Rechercher des utilisateurs/groupes et entrez les informations de recherche.
   * Pour ajouter un utilisateur, une utilisatrice ou un groupe, cochez la case correspondante, cliquez sur OK, puis sur Enregistrer.
   * Pour supprimer un utilisateur, une utilisatrice ou un groupe, cochez la case correspondante, cliquez sur Supprimer, sur OK, puis sur Enregistrer.

1. Pour modifier des affectations de rôles, cliquez sur l’onglet Affectations de rôles et procédez comme suit :

   * Pour rechercher des rôles à affecter au groupe, cliquez sur Rechercher des rôles.
   * Pour ajouter un nouveau rôle, activez la case à cocher qui lui correspond, cliquez sur OK, puis sur Enregistrer.
   * Pour retirer l’affectation d’un rôle, cochez la case correspondante, cliquez sur Retirer, puis sur Enregistrer.

## Supprimer un groupe {#delete-a-group}

1. Dans la console d’administration, cliquez sur Paramètres > User Management > Utilisateurs et groupes.
1. Dans la liste Rechercher, sélectionnez Groupes, puis cliquez sur Rechercher.
1. Cochez la case située en regard du groupe à supprimer, cliquez sur Supprimer, puis sur OK.
