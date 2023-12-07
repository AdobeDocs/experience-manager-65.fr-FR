---
title: Créer et configurer des groupes
description: Découvrez comment créer des groupes manuellement ou dynamiquement, modifier un groupe, afficher des détails sur un groupe ou supprimer un groupe.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 72edd8d1-8573-4942-8ced-1a100af58d78
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1576'
ht-degree: 14%

---

# Créer et configurer des groupes{#creating-and-configuring-groups}

La création de groupes d’utilisateurs vous permet d’affecter des rôles au groupe plutôt qu’à des utilisateurs individuels.

Deux types de groupes différents sont disponibles. Vous pouvez créer manuellement un groupe et y ajouter des utilisateurs et d’autres groupes. Vous pouvez également créer des groupes dynamiques qui incluent automatiquement tous les utilisateurs qui répondent à un ensemble de règles spécifié.

Les utilisateurs peuvent avoir un temps de réponse plus lent s’ils appartiennent à de nombreux groupes (par exemple, 500 ou plus) ou si les groupes sont profondément imbriqués (par exemple, 30 niveaux). Si vous rencontrez ce problème, vous pouvez configurer AEM forms pour prérécupérer les informations de certains domaines. (Voir [Configuration de AEM forms pour la prérécupération des informations de domaine](/help/forms/using/admin-help/configure-aem-forms-prefetch-domain.md#configure-aem-forms-to-prefetch-domain-information).)

## Création manuelle d’un groupe {#create-a-group-manually}

Lorsque vous créez manuellement un groupe, vous pouvez y ajouter des utilisateurs et d’autres groupes et lui affecter des rôles. Vous pouvez également associer le groupe à un groupe parent.

Si vous utilisez Content Services (obsolète), vous pouvez sélectionner l’option Sélectionner cette option pour forcer les utilisateurs et les groupes à devenir des fournisseurs de stockage d’entités de sécurité externes enregistrés sur la page Gestion des domaines pour envoyer les informations relatives aux nouveaux utilisateurs ou groupes que vous créez dans Content Services (obsolète).

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Utilisateurs et groupes, puis sur Nouveau groupe.
1. Renseignez la section Paramètres généraux et cliquez sur Suivant. Le nom canonique et le nom du groupe sont des attributs obligatoires.

   Le Nom canonique est un identifiant unique du groupe. Chaque groupe et utilisateur d’un domaine doit disposer d’un nom canonique unique. Cochez la case Généré par le système pour laisser User Management affecter une valeur unique au paramètre Nom canonique ou désélectionnez la case et saisissez une valeur personnalisée.

   Évitez d’utiliser les caractères de soulignement (_) dans les noms canoniques, par exemple `sample_group`. Lorsque vous recherchez des groupes en fonction de leur nom canonique, ceux contenant des caractères de soulignement ne sont pas renvoyés.

1. Pour ajouter des utilisateurs et des groupes à ce nouveau groupe, cliquez sur Rechercher des utilisateurs/groupes et procédez comme suit :

   * Dans la zone Rechercher, saisissez vos critères de recherche.
   * Dans la liste Dans, sélectionnez Utilisateurs, Groupes ou Utilisateurs et groupes.
   * Dans la liste Utilisation, sélectionnez Nom, Adresse électronique ou ID utilisateur.
   * Sélectionnez le domaine, le nombre d’éléments à afficher, puis cliquez sur Rechercher.
   * Dans les résultats de recherche, cochez les cases correspondant aux utilisateurs et aux groupes à ajouter à ce nouveau groupe, puis cliquez sur OK.

1. Cliquez sur Suivant.
1. Pour ajouter ce nouveau groupe à d’autres groupes existants, cliquez sur Rechercher des groupes et procédez comme suit :

   * Dans la zone Rechercher, saisissez vos critères de recherche.
   * Sélectionnez le domaine, le nombre d’éléments à afficher, puis cliquez sur Rechercher.
   * Dans les résultats de recherche, cochez les cases correspondant aux groupes auxquels le nouveau groupe appartient, puis cliquez sur OK.

1. Cliquez sur Suivant.
1. Pour affecter des rôles au groupe, cliquez sur Rechercher des rôles, cochez les cases correspondant à chaque rôle à affecter au groupe, puis cliquez sur OK. Les utilisateurs du groupe héritent des rôles affectés au niveau du groupe.
1. Cliquez sur Finish (Terminer). 

## Création d’un groupe dynamique {#create-a-dynamic-group}

Dans un groupe dynamique, vous ne sélectionnez pas individuellement les utilisateurs qui appartiennent au groupe. Vous spécifiez plutôt un ensemble de règles et tous les utilisateurs qui répondent à ces règles sont automatiquement ajoutés au groupe dynamique.

Utilisez l’une des deux méthodes suivantes pour créer des groupes dynamiques :

* Activez la création automatique de groupes dynamiques à partir de domaines d&#39;email, tels que @adobe.com. Lorsque vous activez cette fonction, User Management crée un groupe dynamique pour chaque domaine d’adresse électronique unique dans la base de données d’AEM forms. Utilisez une expression cron pour spécifier la fréquence à laquelle User Management recherche de nouveaux domaines de messagerie dans la base de données d’AEM forms. Ces groupes dynamiques sont ajoutés au domaine local DefaultDom et sont appelés « Tous les utilisateurs avec un ID d’e-mail *`[email domain]`* ».
* Créez un groupe dynamique basé sur des critères spécifiés, notamment le domaine d’adresse électronique, la description, le nom canonique et le nom de domaine de l’utilisateur. Pour appartenir au groupe dynamique, un utilisateur doit satisfaire à tous les critères spécifiés. Pour configurer une condition &quot;ou&quot;, créez deux groupes dynamiques distincts et ajoutez-les à un groupe local. Par exemple, utilisez cette approche pour créer un groupe d’utilisateurs appartenant au domaine d’adresse électronique @adobe.com ou dont le nom canonique contient ou=adobe.com. Toutefois, les utilisateurs ne doivent pas nécessairement respecter les deux conditions.

Un groupe dynamique contient uniquement des utilisateurs. Il ne peut pas contenir d’autres groupes. Cependant, un groupe dynamique peut appartenir à un groupe parent.

### Créer automatiquement des groupes dynamiques à partir de domaines d’email {#automatically-create-dynamic-groups-based-on-email-domains}

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Configuration > Configurer les attributs système avancés.
1. Sous Création automatique de groupe dynamique, cochez la case .
1. Indiquez à quel moment User Manager recherche de nouveaux domaines de messagerie. Cette fois doit être postérieure à la synchronisation des domaines, car la création de groupes dynamiques n’est logique que si la synchronisation des domaines est terminée.

   * Pour activer une synchronisation automatique quotidienne, saisissez l’heure au format 24 heures dans la zone Se produit quotidiennement à . Lorsque vous enregistrez vos paramètres, cette valeur est convertie en expression cron, qui s’affiche dans la zone ci-dessous.
   * Pour planifier la synchronisation un jour particulier de la semaine ou du mois, ou pendant un mois spécifique, sélectionnez l’expression cron appropriée dans la zone. La valeur par défaut est `0 00 4 ? * *` (ce qui se traduit par un contrôle à 4 heures du matin tous les jours).

     L’utilisation de l’expression cron est basée sur le système de planification des tâches Open Source Quartz, version 1.4.0.

1. Cliquez sur Enregistrer.

### Création d’un groupe dynamique à partir de critères spécifiés {#create-a-dynamic-group-based-on-specified-criteria}

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Utilisateurs et groupes.
1. Cliquez sur Nouveau groupe dynamique.
1. Renseignez la section Paramètres généraux . Le nom de groupe est un attribut obligatoire. Vous pouvez affecter le groupe à n’importe quel domaine configuré.
1. Sous Critères de groupe dynamique, spécifiez un ou plusieurs attributs utilisés pour remplir le groupe dynamique.

   >[!NOTE]
   >
   >Les attributs Email, Description et Nom canonique sont sensibles à la casse lors de l’utilisation de l’opérateur Egal. Ils ne sont pas sensibles à la casse avec les opérateurs Commence par, Se termine par ou Contient .

   **Adresse électronique :** domaine de l’adresse électronique de l’utilisateur, par exemple `@adobe.com`.

   **Description :** description de l’utilisateur, tel que « Informaticien ».

   **Nom canonique :** nom canonique de l’utilisateur, tel que `ou=adobe.com`.

   **Nom de domaine :** nom du domaine auquel l’utilisateur appartient, par exemple `DefaultDom`. L’attribut Nom de domaine est sensible à la casse lors de l’utilisation de l’opérateur Contient . Elle n’est pas sensible à la casse avec les opérateurs Commence par, Se termine par ou Est égal à .

1. Cliquez sur Tester. Une page Test affiche les 200 premiers utilisateurs qui répondent aux critères définis. Cliquez sur Fermer.
1. Si le test a renvoyé les résultats attendus, cliquez sur Suivant. Dans le cas contraire, modifiez les critères du groupe dynamique et effectuez à nouveau le test.
1. Pour ajouter le groupe dynamique à un groupe parent, cliquez sur Rechercher des groupes et procédez comme suit :

   * Dans la zone Rechercher, saisissez vos critères de recherche.
   * Sélectionnez le domaine, le nombre d’éléments à afficher, puis cliquez sur Rechercher.
   * Dans les résultats de recherche, cochez les cases correspondant aux groupes auxquels appartient le groupe dynamique et cliquez sur OK.

1. Cliquez sur Suivant.
1. Pour affecter des rôles au groupe dynamique, cliquez sur Rechercher des rôles, cochez les cases correspondant à chaque rôle à affecter au groupe, puis cliquez sur OK. Les utilisateurs du groupe héritent des rôles affectés au niveau du groupe.
1. Cliquez sur Finish (Terminer). 

## Affichage des détails d’un groupe {#view-details-about-a-group}

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Utilisateurs et groupes.
1. Dans la liste Dans, sélectionnez Groupe, puis cliquez sur Rechercher. Les résultats de la recherche apparaissent au bas de la page. Vous pouvez trier la liste en cliquant sur l’un des en-têtes de colonne.
1. Cliquez sur le nom du groupe dont vous souhaitez afficher les détails. La page Détails du groupe s’affiche.
1. Pour afficher les membres directs du groupe, cliquez sur Entités de sécurité enfants.

## Modification d’un groupe {#edit-a-group}

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Utilisateurs et groupes.
1. Pour trouver le groupe à modifier, procédez comme suit :

   * Dans la zone Rechercher, saisissez vos critères de recherche.
   * Dans la liste Utilisation, sélectionnez Nom ou Adresse électronique.
   * Dans la liste Dans, sélectionnez Groupes.
   * Sélectionnez le domaine, le nombre d’éléments à afficher, puis cliquez sur Rechercher.
   * Dans les résultats de la recherche, cliquez sur le nom du groupe à modifier.

1. Dans l’onglet Détails , modifiez les paramètres généraux et cliquez sur Enregistrer.
1. Pour modifier les groupes associés, cliquez sur l’onglet Groupes parents et procédez comme suit :

   * Pour rechercher des groupes à ajouter à l’association, cliquez sur Rechercher des groupes et renseignez les informations de recherche.
   * Pour ajouter des groupes, cochez la case correspondant aux groupes à ajouter, cliquez sur OK, puis sur Enregistrer.
   * Pour supprimer un groupe associé, cochez la case correspondant au groupe à supprimer, cliquez sur Supprimer, sur OK, puis sur Enregistrer.

1. Pour modifier les utilisateurs et les groupes du groupe, cliquez sur l’onglet Entités de sécurité enfants et procédez comme suit :

   * Pour rechercher des utilisateurs et des groupes à ajouter, cliquez sur Rechercher des utilisateurs/groupes et renseignez les informations de recherche.
   * Pour ajouter un utilisateur ou un groupe, cochez la case correspondant à l’utilisateur ou au groupe, cliquez sur OK, puis sur Enregistrer.
   * Pour supprimer un utilisateur ou un groupe, cochez la case correspondant à l’utilisateur ou au groupe, cliquez sur Supprimer, sur OK, puis sur Enregistrer.

1. Pour modifier les affectations de rôle, cliquez sur l’onglet Affectations de rôle et procédez comme suit :

   * Pour rechercher des rôles à affecter au groupe, cliquez sur Rechercher des rôles.
   * Pour ajouter un nouveau rôle, activez la case à cocher qui lui correspond, cliquez sur OK, puis sur Enregistrer.
   * Pour annuler l’affectation d’un rôle, cochez la case correspondante, cliquez sur Annuler l’affectation, puis sur Enregistrer.

## Suppression d’un groupe {#delete-a-group}

1. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Utilisateurs et groupes.
1. Dans la liste Rechercher, sélectionnez Groupes, puis cliquez sur Rechercher.
1. Cochez la case correspondant au groupe à supprimer, cliquez sur Supprimer, puis sur OK.
