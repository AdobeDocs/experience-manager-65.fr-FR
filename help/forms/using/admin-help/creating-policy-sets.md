---
title: Créer et gérer les jeux de politiques
description: Les jeux de politiques regroupent plusieurs politiques ayant une finalité commune. Vous pouvez créer, modifier et supprimer des politiques dans un jeu de politiques.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
exl-id: 736926af-ae41-4da3-b181-444de72407bd
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '1297'
ht-degree: 100%

---

# Créer et gérer les jeux de politiques {#creating-and-managing-policy-sets}

Les jeux de politiques regroupent plusieurs politiques ayant une finalité commune. Ces jeux de politiques sont ensuite rendus accessibles à un sous-ensemble d’utilisateurs et d’utilisatrices du système.

Chaque jeu de politiques est associé à au moins un coordinateur ou une coordinatrice. Le *coordinateur ou la coordinatrice de jeux de politiques* est un administrateur, une administratrice, un utilisateur ou une utilisatrice possédant des autorisations supplémentaires. Au sein de l’organisation, le coordinateur ou la coordinatrice de jeux de politiques est généralement la personne la plus à même de créer des politiques dans un jeu donné.

Les coordinateurs et coordinatrices de jeux de politiques peuvent effectuer les tâches suivantes :

* Créer des politiques
* Modifier et supprimer une politique dans le jeu de politiques
* Modifier des paramètres de jeux de politiques
* Ajouter et supprimer des coordinateurs et coordinatrices pour le jeu de politiques
* Afficher des événements de politique et de document pour n’importe quel document ou politique du jeu de politiques
* Révoquer l’accès aux documents
* Changer de politiques pour le document

Les jeux de politiques sont créés et supprimés dans l’interface d’administration de Document Security par les super-utilisateurs et super-utilisatrices et les coordinateurs et coordinatrices de jeux de politiques bénéficiant des autorisations requises.

Lorsque vous supprimez un jeu de politiques, les politiques qui faisaient partie du jeu ne peuvent pas être appliquées aux nouveaux documents. Cependant, vous pouvez afficher les informations de politique dans la console d’administration et dans les pages web destinées aux utilisateurs finaux et utilisatrices finales pour les politiques toujours utilisées. Vous pouvez afficher les informations de politique à partir de la page des détails du document pour tout document protégé par la politique. Les politiques toujours utilisées peuvent être modifiées.

Le super-utilisateur ou la super-utilisatrice (ou le coordinateur ou la coordinatrice) de jeux de politiques ajoute les domaines créés dans User Management à l’utilisateur ou l’utilisatrice et au groupe visible pour chaque jeu de politiques. Cette liste est visible par le coordinateur ou la coordinatrice de l’ensemble de politiques et est utilisée pour limiter les domaines que le coordinateur ou la coordinatrice de l’ensemble de politiques peut parcourir lors du choix des personnes à ajouter aux politiques.

Lorsque vous créez des jeux de politiques, vous attribuez aux utilisateurs et aux utilisatrices le rôle d’éditeurs et d’éditrices de document. L’*éditeur ou l’éditrice de documents* est l’utilisateur ou l’utilisatrice qui protège le document avec une politique. Par défaut, cette personne est toujours incluse dans une politique avec des droits d’accès complets, y compris les fonctionnalités de révocation et de changement de politique. Toutefois, l’équipe d’administration peut modifier les droits d’accès de l’éditeur ou de l’éditrice pour les politiques partagées. Par exemple, l’équipe d’administration peut désactiver le droit de l’éditeur ou de l’éditrice à révoquer l’accès au document ou à changer de politique. Si l’équipe d’administration change la politique associée au document, le nom de l’éditeur ou de l’éditrice est mis à jour avec le nom de la personne propriétaire de la dernière politique appliquée au document.

L’installation de Document Security crée un jeu de politiques par défaut appelé *Jeu de politiques global*. Ce jeu de politiques est géré par l’administrateur ou l’administratrice qui a installé le logiciel ou par le coordinateur ou la coordinatrice de jeux de politiques désignés pour ce jeu en particulier.

## Créer un jeu de politiques {#create-a-policy-set}

Le jeu de politiques global est le seul jeu de politiques par défaut créé lors de l’installation. Vous pouvez créer d’autres jeux de politiques et ajouter des politiques, des utilisateurs ou des utilisatrices, des coordinateurs ou des coordinatrices de jeux de politiques et des éditeurs ou des éditrices. Lorsque vous avez créé un jeu de politiques, vous pouvez créer des politiques dans le jeu.

Lorsque vous créez un jeu de politiques, vous pouvez utiliser le bouton Précédent pour revenir à l’écran précédent et le bouton Enregistrer pour enregistrer votre jeu de politiques à tout moment.

1. Dans la page Document Security, cliquez sur Politiques, sur l’onglet Jeux de politiques, puis sur Nouveau.
1. Dans la zone Nom, saisissez le nom du jeu de politiques, indiquez éventuellement une description dans la zone prévue à cet effet, puis cliquez sur Suivant. Le nom ne peut pas contenir de caractère deux-points **:**.

   >[!NOTE]
   >
   >Vous pouvez créer un nom de jeu de politiques contenant des caractères étendus. Toutefois, lors d’une comparaison entre deux chaînes, les caractères accentués et non accentués tels que « e » et « é » sont considérés comme identiques. Lorsqu’un utilisateur ou une utilisatrice crée un jeu de politiques, une comparaison est effectuée pour vérifier s’il en existe déjà un portant ce nom. La comparaison ne fait pas de distinction entre les noms identiques, à l’exception des caractères accentués. Le jeu de politiques étant considéré comme existant dans la base de données, aucun ajout n’est possible.

1. (Facultatif) Pour définir les domaines visibles aux éditeurs et éditrices lorsqu’ils ajoutent des utilisateurs et utilisatrices à une politique, cliquez sur Ajouter des domaines, sélectionnez les domaines dans lesquels vous souhaitez autoriser la recherche, cliquez sur Ajouter, puis sur OK.
1. Dans la page Ajouter des utilisateurs, des utilisatrices ou des groupes visibles, cliquez sur Suivant.
1. (Facultatif) Pour ajouter un coordinateur ou une coordinatrice de jeux de politiques, cliquez sur Ajouter des utilisateurs, des utilisatrices ou des groupes dans la page Ajouter un ou plusieurs coordinateurs et coordinatrices de jeux de politiques (étape 3 sur 4) et effectuez les tâches suivantes :

   * Dans la zone Rechercher, saisissez le nom ou l’adresse e-mail.
   * Dans la liste Utilisation, sélectionnez l’option appropriée.
   * Dans la liste Type, sélectionnez Utilisateur ou utilisatrice et, dans la liste Dans, sélectionnez un domaine à rechercher.
   * Dans la liste Afficher, indiquez le nombre de résultats de recherche à afficher par page et cliquez sur Rechercher.
   * Cochez la case correspondant à l’utilisateur, à l’utilisatrice ou au groupe à ajouter, puis cliquez sur Suivant.
   * Sélectionnez les autorisations du coordinateur ou de la coordinatrice de jeux de politiques, puis cliquez sur Ajouter. Les autorisations suivantes peuvent être définies :

      * Affichage des événements
      * Gérer les documents (révoquer et rétablir l’accès aux documents et changer de politiques sur les documents)
      * Gérer les politiques (création, modification et suppression de politiques)
      * Gérer les éditeurs et éditrices (ajout et suppression d’éditeurs ou d’éditrices)
      * Déléguer (ajout et suppression de coordinateurs ou de coordinatrices de jeux de politiques)

1. Répétez l’étape 5 pour ajouter d’autres coordinateurs ou coordinatrices de jeux de politiques.
1. Vérifiez les paramètres du coordinateur ou de la coordinatrice de jeux de politiques, puis cliquez sur Suivant.
1. Cliquez sur Ajouter des utilisateurs, des utilisatrices et des groupes pour ajouter des éditeurs et éditrices qui peuvent utiliser les politiques du jeu de politiques pour protéger les documents.
1. Dans la page Ajouter des éditeurs et éditrices, effectuez les tâches suivantes :

   * Dans la zone Rechercher, saisissez le nom ou l’adresse e-mail.
   * Dans la liste Utilisation, sélectionnez l’option appropriée.
   * Dans la liste Type, sélectionnez Utilisateur ou utilisatrice et, dans la liste Dans, sélectionnez un domaine à rechercher.
   * Dans la liste Afficher, indiquez le nombre de résultats de recherche à afficher par page et cliquez sur Rechercher.
   * Cochez les cases des utilisateurs, des utilisatrices et des groupes à ajouter, cliquez sur Ajouter, puis cliquez sur OK.

1. Cliquez sur Enregistrer.

Vous pouvez maintenant ajouter des politiques à votre jeu de politiques. (Voir [Création et modification de politiques](/help/forms/using/admin-help/creating-policies.md#creating-and-editing-policies).)

## Modification d’un jeu de politiques {#edit-a-policy-set}

1. Dans la page Document Security, cliquez sur Politiques, sur l’onglet Jeux de politiques, puis sur le jeu de politiques à modifier.
1. Cliquez sur l’onglet approprié, puis effectuez les modifications souhaitées :

   * **Détails :** modifiez le nom et la description du jeu de politiques.
   * **Politiques :** créez, activez, modifiez et supprimez des politiques dans le jeu de politiques.
   * **Utilisateurs, utilisatrices et groupes visibles :** ajoutez et supprimez des utilisateurs, des utilisatrices et des groupes visibles pouvant être inclus dans une politique.
   * **Coordinateurs ou coordinatrices de jeux de politiques :** ajoutez, supprimez et modifiez des autorisations pour les coordinateurs et coordinatrices.
   * **Éditeurs ou éditrices :** ajoutez et supprimez des utilisateurs et des utilisatrices autorisés à publier des documents à l’aide des politiques du jeu.

1. Pour supprimer un utilisateur, une utilisatrice ou un groupe visible, un coordinateur ou une coordinatrice de jeux de politiques ou un éditeur ou une éditrice, cliquez sur l’onglet approprié, cochez la case correspondant à l’entrée, cliquez sur Supprimer, puis sur OK.
1. Pour ajouter des utilisateurs, des utilisatrices ou des groupes visibles, un coordinateur ou une coordinatrice de jeux de politiques ou des éditeurs et éditrices, cliquez sur l’onglet approprié, sur Ajouter des utilisateurs, des utilisatrices ou des groupes, recherchez l’utilisateur, l’utilisatrice ou le groupe à ajouter, sélectionnez l’entrée, cliquez sur Ajouter, puis sur OK.
1. Dans l’onglet Politiques, recherchez les politiques à ajouter au jeu de politiques et créez d’autres politiques :

   * Pour rechercher une politique, sélectionnez ID de la politique ou Nom de la politique, saisissez la valeur correspondante, sélectionnez le nombre d’éléments à afficher, puis cliquez sur Rechercher.
   * Pour plus d’informations sur la création d’une politique, voir [Création et modification de politiques](/help/forms/using/admin-help/creating-policies.md#creating-and-editing-policies).

## Suppression d’un jeu de politiques {#delete-a-policy-set}

Lorsque vous supprimez un jeu de politiques, les politiques qui faisaient partie du jeu ne peuvent pas être appliquées aux nouveaux documents. Cependant, vous pouvez afficher les informations de politique dans la console d’administration et dans les pages web destinées aux utilisateurs et utilisatrices finaux pour les politiques toujours utilisées. Vous pouvez afficher les informations de politique à partir de la page des détails du document pour tout document protégé par la politique. Les politiques toujours utilisées peuvent être modifiées.

1. Cliquez sur Politiques, puis sur l’onglet Jeux de politiques.
1. Cochez la case correspondant au jeu de politiques à supprimer.
1. Cliquez sur Supprimer, puis sur OK.
