---
title: Création et gestion des jeux de stratégies
seo-title: Création et gestion des jeux de stratégies
description: Les jeux de stratégies regroupent plusieurs stratégies ayant une finalité commune. Vous pouvez également créer, modifier et supprimer des stratégies dans un jeu de stratégies.
seo-description: Les jeux de stratégies regroupent plusieurs stratégies ayant une finalité commune. Vous pouvez également créer, modifier et supprimer des stratégies dans un jeu de stratégies.
uuid: 11faf67c-b9b7-4394-8672-d43cace131ad
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a4fb1a11-8fe3-4092-a036-1c079aea1250
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1324'
ht-degree: 100%

---


# Création et gestion des jeux de stratégies {#creating-and-managing-policy-sets}

Les jeux de stratégies regroupent plusieurs stratégies ayant une finalité commune. Ces jeux de stratégies sont ensuite rendus accessibles à un sous-groupe d’utilisateurs du système.

Chaque jeu de stratégies est associé à un coordinateur au moins. Le *coordinateur de jeux de stratégies* est un administrateur ou un utilisateur possédant des autorisations supplémentaires. Au sein de l’organisation, c’est généralement la personne la plus à même de créer des stratégies dans un jeu donné.

Les coordinateurs de jeux de stratégie peuvent exécuter les tâches suivantes :

* créer des stratégies ;
* modifier et supprimer des stratégies dans un jeu de stratégies ;
* modifier des paramètres de jeux de stratégies ;
* ajouter et supprimer des coordinateurs pour le jeu de stratégies ;
* afficher des événements de stratégie et de document pour n’importe quel document ou stratégie du jeu de stratégies ;
* révoquer l’accès aux documents ;
* changer de stratégies pour le document.

Les jeux de stratégies sont créés et supprimés dans l’interface d’administration de Document Security par des super-utilisateurs et des coordinateurs de jeux de stratégies qui possèdent les autorisations requises.

Lorsque vous supprimez un jeu de stratégies, les stratégies qui faisaient partie de ce jeu ne peuvent pas être appliquées aux nouveaux documents. Cependant, vous pouvez afficher les informations de stratégie dans Administration Console et dans les pages Web destinées aux utilisateurs finaux, correspondant aux stratégies toujours utilisées. Vous pouvez afficher les informations de stratégie dans la page Détails du document pour tout document protégé par la stratégie. Les stratégies encore utilisées peuvent être modifiées.

Le super-utilisateur ou le coordinateur de jeux de stratégies ajoute les domaines créés dans User Management pour l’utilisateur et pour le groupe visible pour chaque jeu de stratégies. Cette liste est accessible au coordinateur de jeux de stratégies et permet de restreindre les domaines que ce dernier peut consulter lorsqu’il choisit les utilisateurs à ajouter aux stratégies.

Lorsque vous créez des jeux de stratégies, vous affectez à des utilisateurs le rôle d’éditeur de document. L’*éditeur* est l’utilisateur qui protège le document avec une stratégie. Cet utilisateur est toujours inclus par défaut dans une stratégie, avec des droits d’accès complets, notamment la capacité de révoquer et de changer de stratégie. Toutefois, les administrateurs peuvent modifier les droits d’accès de l’éditeur relatifs aux stratégies partagées. Ils peuvent par exemple désactiver la capacité de l’éditeur à révoquer l’accès à un document ou à changer de stratégie. Si un administrateur change la stratégie associée au document, le nom de l’éditeur sera mis à jour avec le nom du propriétaire de la dernière politique appliquée au document.

L’installation de Document Security crée un jeu de stratégies par défaut, appelé *Jeu de stratégies global*. Ce jeu de stratégies est géré par l’administrateur ayant installé le logiciel ou par le coordinateur de jeux de stratégies désigné pour ce jeu de stratégies.

## Création d’un jeu de stratégies {#create-a-policy-set}

Le Jeu de stratégies global est le seul jeu de stratégies par défaut créé lors de l’installation. Vous pouvez créer d’autres jeux de stratégies et ajouter des stratégies, des utilisateurs, des coordinateurs de jeux de stratégies et des éditeurs. Après avoir créé un jeu de stratégies, vous pouvez créer des stratégies à l’intérieur du jeu.

Lors de la création d’un jeu de stratégies, cliquez sur le bouton Précédent pour revenir à l’écran précédent, et sur le bouton Enregistrer pour enregistrer votre jeu de stratégies à tout moment.

1. Dans la page Document Security, cliquez sur Stratégies, sur l’onglet Jeux de stratégies, puis sur Nouveau.
1. Dans la zone Nom, saisissez le nom du jeu de stratégies, indiquez éventuellement une description dans la zone Description, puis cliquez sur Suivant. Le nom ne peut pas contenir de caractère deux-points **:**.

   >[!NOTE]
   >
   >vous pouvez créer un nom de jeu de stratégies qui contient des caractères étendus. Cependant, en cas de comparaison entre deux chaînes, aucune différence n’est faite entre les caractères accentués et non accentués (« e » et « é », par exemple). Si quelqu’un crée un jeu de stratégies, une comparaison est lancée pour vérifier s’il en existe déjà un portant le même nom. La comparaison ne fait pas de distinction entre les noms identiques, à l’exception des caractères accentués. Le jeu de stratégies étant considéré comme existant dans la base de données, aucun ajout n’est possible.

1. (Facultatif) Pour définir les domaines visibles aux éditeurs lorsqu’ils ajoutent des utilisateurs à une stratégie, cliquez sur Ajouter un domaine, sélectionnez les domaines dans lesquels vous souhaitez autoriser la recherche, cliquez sur Ajouter, puis sur OK.
1. Dans la page Ajouter des utilisateurs ou des groupes visibles, cliquez sur Suivant.
1. (Facultatif) Pour ajouter un coordinateur de jeux de stratégies, cliquez sur « Ajouter des utilisateurs ou des groupes » dans la page « Ajouter un/des coordinateur(s) de jeux de stratégies » (étape 3 sur 4) et exécutez les tâches suivantes :

   * Dans la zone Rechercher, saisissez le nom ou l’adresse électronique.
   * Dans la liste Utilisation, sélectionnez l’option appropriée.
   * Dans la liste Type, sélectionnez Utilisateur, puis, dans la liste Dans, sélectionnez un domaine de recherche.
   * Dans la liste Afficher, indiquez le nombre de résultats de recherche à afficher par page et cliquez sur Rechercher.
   * Cochez la case en regard de l’utilisateur ou du groupe à ajouter et cliquez sur Suivant.
   * Sélectionnez les droits à affecter au coordinateur de jeux de stratégies et cliquez sur Ajouter. Vous pouvez choisir les autorisations suivantes :

      * Affichage des événements
      * Gérer des documents (révoquer et rétablir l’accès aux documents, et changer de stratégie sur des documents)
      * Gérer les stratégies (créer, modifier et supprimer des stratégies)
      * Gérer les éditeurs (ajouter et supprimer des éditeurs)
      * Déléguer (ajouter et supprimer des coordinateurs de jeux de stratégies)

1. Répétez l’étape 5 pour ajouter d’autres coordinateurs de jeux de stratégies.
1. Vérifiez les droits attribués au coordinateur de jeux de stratégies et cliquez sur Suivant.
1. Cliquez sur Ajouter des utilisateurs ou des groupes pour ajouter des éditeurs autorisés à utiliser les stratégies du jeu pour protéger des documents.
1. Dans la page Ajouter un/des éditeur(s), effectuez les opérations suivantes :

   * Dans la zone Rechercher, saisissez le nom ou l’adresse électronique.
   * Dans la liste Utilisation, sélectionnez l’option appropriée.
   * Dans la liste Type, sélectionnez Utilisateur, puis, dans la liste Dans, sélectionnez un domaine de recherche.
   * Dans la liste Afficher, indiquez le nombre de résultats de recherche à afficher par page et cliquez sur Rechercher.
   * Cochez les cases en regard des utilisateurs et des groupes à ajouter, cliquez sur Ajouter, puis sur OK.

1. Cliquez sur Enregistrer.

Vous pouvez maintenant ajouter des stratégies à votre jeu de stratégies (voir [Création et modification de stratégies](/help/forms/using/admin-help/creating-policies.md#creating-and-editing-policies)).

## Modification d’un jeu de stratégies {#edit-a-policy-set}

1. Dans la page Document Security, cliquez sur Stratégies, sur l’onglet Jeux de stratégies, puis sur le jeu de stratégies à modifier.
1. Cliquez sur l’onglet approprié, puis effectuez les modifications souhaitées :

   * **Détails :** modifiez le nom et la description du jeu de stratégies.
   * **Stratégies :** créez, activez, modifiez et supprimez des stratégies dans le jeu de stratégies.
   * **Utilisateurs et groupes visibles :** ajoutez et supprimez des utilisateurs et groupes visibles susceptibles d’être inclus dans une stratégie.
   * **Coordinateurs de jeux de stratégies :** ajoutez, supprimez et modifiez des autorisations pour les coordinateurs.
   * **Editeurs :** ajoutez et supprimez des utilisateurs habilités à publier des documents à l’aide des stratégies du jeu.

1. Pour supprimer un utilisateur ou un groupe visible, un coordinateur de jeux de stratégies ou un éditeur, cliquez sur l’onglet approprié, sélectionnez la case à cocher correspondant à l’entrée, puis cliquez sur Supprimer et sur OK.
1. Pour ajouter des utilisateurs ou groupes visibles, un coordinateur de jeux de stratégies ou des éditeurs, cliquez sur l’onglet approprié, sur Ajouter des utilisateurs ou des groupes, recherchez l’utilisateur ou le groupe à ajouter, sélectionnez l’entrée, cliquez sur Ajouter, puis sur OK.
1. Dans l’onglet Stratégies, recherchez les stratégies à ajouter au jeu et créez d’autres stratégies :

   * Pour rechercher une stratégie, sélectionnez ID de la stratégie ou Nom de la stratégie, saisissez la valeur correspondante, sélectionnez le nombre d’éléments à afficher et cliquez sur Rechercher.
   * Pour plus d’informations sur la création d’une nouvelle stratégie, voir [Création et modification de stratégies](/help/forms/using/admin-help/creating-policies.md#creating-and-editing-policies).

## Suppression d’un jeu de stratégies {#delete-a-policy-set}

Lorsque vous supprimez un jeu de stratégies, les stratégies qui faisaient partie de ce jeu ne peuvent pas être appliquées aux nouveaux documents. Cependant, vous pouvez afficher les informations de stratégie dans Administration Console et dans les pages Web destinées aux utilisateurs finaux, correspondant aux stratégies toujours utilisées. Vous pouvez afficher les informations de stratégie dans la page Détails du document pour tout document protégé par la stratégie. Les stratégies encore utilisées peuvent être modifiées.

1. Cliquez sur Stratégies, puis sur l’onglet Jeux de stratégies.
1. Cochez la case correspondant au jeu de stratégies à supprimer.
1. Cliquez sur Supprimer, puis sur OK.

