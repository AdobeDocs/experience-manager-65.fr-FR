---
title: Créer et gérer les jeux de politiques
description: Les jeux de stratégies sont utilisés pour regrouper des stratégies ayant un objectif commercial commun. Vous pouvez créer, modifier et supprimer des stratégies dans un jeu de stratégies.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
exl-id: 736926af-ae41-4da3-b181-444de72407bd
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1297'
ht-degree: 4%

---

# Créer et gérer les jeux de politiques {#creating-and-managing-policy-sets}

Les jeux de stratégies sont utilisés pour regrouper des stratégies ayant un objectif commercial commun. Les jeux de stratégies peuvent être mis à la disposition d’un sous-ensemble d’utilisateurs du système.

Chaque jeu de stratégies est associé à au moins un coordinateur. La variable *coordinateur de jeux de stratégies* est un administrateur ou un utilisateur disposant d’autorisations supplémentaires. Le coordinateur de jeux de stratégies est généralement un spécialiste de l’organisation qui peut créer au mieux les stratégies d’un jeu donné.

Les coordinateurs et coordinatrices de jeux de politiques peuvent effectuer les tâches suivantes :

* Création de stratégies
* Modifier et supprimer une politique dans le jeu de politiques
* Modifier des paramètres de jeux de politiques
* Ajouter et supprimer des coordinateurs pour le jeu de stratégies
* Afficher des événements de politique et de document pour n’importe quel document ou politique du jeu de politiques
* Révoquer l’accès aux documents
* Changement de stratégies pour le document

Les jeux de stratégies sont créés et supprimés dans l’interface d’administration de Document Security par des super-utilisateurs et des coordinateurs de jeux de stratégies autorisés à le faire.

Lorsque vous supprimez un jeu de stratégies, les stratégies qui faisaient partie du jeu ne peuvent pas être appliquées aux nouveaux documents. Cependant, vous pouvez afficher les informations de stratégie dans Administration Console et dans les pages Web destinées aux utilisateurs finaux pour les stratégies toujours utilisées. Vous pouvez afficher les informations de stratégie à partir de la page des détails du document pour tout document protégé par la stratégie. Les stratégies toujours utilisées peuvent être modifiées.

Le super-utilisateur ou le coordinateur de jeux de stratégies ajoute les domaines créés dans User Management à l’utilisateur et au groupe visible pour chaque jeu de stratégies. Cette liste est visible par le coordinateur de jeux de stratégies et permet de limiter les domaines que le coordinateur de jeux de stratégies peut parcourir lors du choix des utilisateurs à ajouter aux stratégies.

Lorsque vous créez des jeux de stratégies, vous attribuez aux utilisateurs le rôle d’éditeur de document. La variable *éditeur de document* est l’utilisateur qui protège le document avec une stratégie. Par défaut, cet utilisateur est toujours inclus dans une stratégie avec des droits d’accès complets, y compris les fonctionnalités de révocation et de changement de stratégie. Toutefois, les administrateurs peuvent modifier les droits d’accès de l’éditeur pour les stratégies partagées. Par exemple, l’administrateur peut désactiver le droit de l’éditeur de révoquer l’accès au document ou changer de stratégie. Si un administrateur change la stratégie associée au document, le nom de l’éditeur est mis à jour avec le nom du propriétaire de la dernière stratégie appliquée au document.

Lors de l’installation de Document Security, un jeu de stratégies par défaut est créé appelé *Jeu de stratégies global*. Ce jeu de stratégies est géré par l’administrateur qui a installé le logiciel ou par le coordinateur de jeux de stratégies désigné pour ce jeu de stratégies.

## Créer un jeu de politiques {#create-a-policy-set}

Le jeu de stratégies global est le seul jeu de stratégies par défaut créé lors de l’installation. Vous pouvez créer d’autres jeux de stratégies et ajouter des stratégies, des utilisateurs, des coordinateurs de jeux de stratégies et des éditeurs. Après avoir créé un jeu de stratégies, vous pouvez créer des stratégies dans le jeu.

Lors de la création d’un jeu de stratégies, vous pouvez utiliser le bouton Retour pour revenir à l’écran précédent et le bouton Enregistrer pour enregistrer votre jeu de stratégies à tout moment.

1. Dans la page Document Security, cliquez sur Stratégies, sur l’onglet Jeux de stratégies, puis sur Nouveau.
1. Dans la zone Name, saisissez le nom du jeu de stratégies, saisissez éventuellement une Description, puis cliquez sur Next. Le nom ne peut pas contenir de caractère deux-points **:**.

   >[!NOTE]
   >
   >Vous pouvez créer un nom de jeu de stratégies contenant des caractères étendus. Toutefois, lors d’une comparaison entre deux chaînes, les caractères accentués et non accentués tels que &quot;e&quot; et &quot;é&quot; sont considérés comme identiques. Lorsqu’un utilisateur crée un jeu de stratégies, une comparaison est effectuée pour vérifier s’il existe déjà un jeu de stratégies portant le même nom. La comparaison ne peut pas distinguer les noms identiques, à l’exception des caractères accentués. On suppose que le jeu de stratégies est déjà ajouté à la base de données et que le nouveau n’est pas ajouté.

1. (Facultatif) Pour définir les domaines visibles aux éditeurs lorsqu’ils ajoutent des utilisateurs à une stratégie, cliquez sur Ajouter des domaines, sélectionnez les domaines à rechercher, cliquez sur Ajouter, puis sur OK.
1. Sur la page Ajouter les utilisateurs et groupes visibles, cliquez sur Suivant.
1. (Facultatif) Pour ajouter un coordinateur de jeux de stratégies, cliquez sur Ajouter des utilisateurs et des groupes sur la page Ajouter un(s) coordinateur(s) de jeux de stratégies (étape 3 sur 4) et effectuez les tâches suivantes :

   * Dans la zone Rechercher, saisissez le nom ou l’adresse électronique.
   * Dans la liste Utilisation , sélectionnez l’option appropriée.
   * Dans la liste Type, sélectionnez Utilisateur et, dans la liste Dans, sélectionnez un domaine à rechercher.
   * Dans la liste Afficher, sélectionnez le nombre de résultats à afficher par page, puis cliquez sur Rechercher.
   * Cochez la case correspondant à l’utilisateur ou au groupe à ajouter, puis cliquez sur Suivant.
   * Sélectionnez les autorisations du coordinateur de jeux de stratégies, puis cliquez sur Ajouter. Les autorisations suivantes peuvent être définies :

      * Affichage des événements
      * Gérer les documents (révoquer et rétablir l’accès aux documents, et changer de stratégie sur les documents)
      * Gestion des stratégies (création, modification et suppression de stratégies)
      * Gestion des éditeurs (ajout et suppression des éditeurs)
      * Déléguer (ajouter et supprimer des coordinateurs de jeux de stratégies)

1. Répétez l’étape 5 pour ajouter d’autres coordinateurs de jeux de stratégies.
1. Vérifiez les paramètres du coordinateur de jeux de stratégies, puis cliquez sur Suivant.
1. Cliquez sur Ajouter des utilisateurs et des groupes pour ajouter des éditeurs qui peuvent utiliser les stratégies du jeu de stratégies pour protéger les documents.
1. Sur la page Ajouter des éditeurs , effectuez les tâches suivantes :

   * Dans la zone Rechercher, saisissez le nom ou l’adresse électronique.
   * Dans la liste Utilisation , sélectionnez l’option appropriée.
   * Dans la liste Type, sélectionnez Utilisateur et, dans la liste Dans, sélectionnez un domaine à rechercher.
   * Dans la liste Afficher, sélectionnez le nombre de résultats à afficher par page, puis cliquez sur Rechercher.
   * Cochez les cases correspondant aux utilisateurs et aux groupes à ajouter, cliquez sur Ajouter, puis sur OK.

1. Cliquez sur Enregistrer.

Vous pouvez désormais ajouter des stratégies à votre jeu de stratégies. (Voir [Création et modification de stratégies](/help/forms/using/admin-help/creating-policies.md#creating-and-editing-policies).)

## Modification d’un jeu de stratégies {#edit-a-policy-set}

1. Dans la page Document Security, cliquez sur Stratégies, cliquez sur l’onglet Jeux de stratégies, puis sur le jeu de stratégies à modifier.
1. Cliquez sur l’onglet approprié et modifiez les éléments selon les besoins :

   * **Détail :** Modifiez le nom et la description du jeu de stratégies.
   * **Stratégies :** Créez, activez, modifiez et supprimez des stratégies dans le jeu de stratégies.
   * **Utilisateurs et groupes visibles :** Ajouter et supprimer des utilisateurs et des groupes visibles pouvant être inclus dans une stratégie.
   * **Coordinateurs de jeux de stratégies :** Ajouter, supprimer et modifier des autorisations pour les coordinateurs.
   * **Éditeurs de document :** Ajoutez et supprimez des utilisateurs autorisés à publier des documents à l’aide des stratégies du jeu.

1. Pour supprimer un utilisateur ou un groupe visible, un coordinateur de jeux de stratégies ou un éditeur de document, cliquez sur l’onglet approprié, cochez la case correspondant à l’entrée, cliquez sur Supprimer, puis sur OK.
1. Pour ajouter des utilisateurs ou des groupes visibles, un coordinateur de jeux de stratégies ou des éditeurs, cliquez sur l’onglet approprié, sur Ajouter des utilisateurs ou des groupes, recherchez l’utilisateur ou le groupe à ajouter, sélectionnez l’entrée, cliquez sur Ajouter, puis sur OK.
1. Dans l’onglet Stratégies , recherchez des stratégies à ajouter au jeu de stratégies et créez-en de nouvelles :

   * Pour rechercher une stratégie, sélectionnez ID de la stratégie ou Nom de la stratégie, saisissez la valeur correspondante, sélectionnez le nombre d’éléments à afficher, puis cliquez sur Rechercher.
   * Pour plus d’informations sur la création d’une stratégie, voir [Création et modification de stratégies](/help/forms/using/admin-help/creating-policies.md#creating-and-editing-policies).

## Suppression d’un jeu de stratégies {#delete-a-policy-set}

Lorsque vous supprimez un jeu de stratégies, les stratégies qui faisaient partie du jeu ne peuvent pas être appliquées aux nouveaux documents. Cependant, vous pouvez afficher les informations de stratégie dans Administration Console et dans les pages Web destinées aux utilisateurs finaux pour les stratégies toujours utilisées. Vous pouvez afficher les informations de stratégie à partir de la page des détails du document pour tout document protégé par la stratégie. Les stratégies toujours utilisées peuvent être modifiées.

1. Cliquez sur Stratégies , puis sur l’onglet Jeux de stratégies .
1. Cochez la case correspondant au jeu de stratégies à supprimer.
1. Cliquez sur Supprimer, puis sur OK.
