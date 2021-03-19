---
title: Gestion des comptes d’utilisateurs invités et locaux
seo-title: Gestion des comptes d’utilisateurs invités et locaux
description: La sécurité des documents permet de rechercher, afficher, modifier, verrouiller, déverrouiller et supprimer des comptes d’utilisateurs invités et locaux.
seo-description: La sécurité des documents permet de rechercher, afficher, modifier, verrouiller, déverrouiller et supprimer des comptes d’utilisateurs invités et locaux.
uuid: 0d0c717a-6e6e-4e42-96eb-3a7166e215ab
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 65720eed-ab06-463f-9567-2fdc468b6219
feature: Document Security
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1222'
ht-degree: 100%

---


# Gestion des comptes d’utilisateurs invités et locaux {#managing-invited-and-local-user-accounts}

Utilisez la page Utilisateurs invités et locaux pour gérer vos utilisateurs invités et locaux. Cette page n’apparaît que si les exigences suivantes sont respectées :

* Vous êtes administrateur et les rôles Gestion des utilisateurs invités et locaux de Document Security et Utilisateur d’Administration Console vous ont été attribués (voir [Création et configuration de rôles](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles)).
* L’enregistrement des utilisateurs invités est activé (voir [Configuration de l’enregistrement d’utilisateur invité](/help/forms/using/admin-help/configuring-client-server-options.md#configuring-invited-user-registration)).

La page Utilisateurs invités et locaux contient deux onglets qui vous permettent de rechercher, afficher, modifier, verrouiller, déverrouiller et supprimer des comptes d’utilisateur invité et local.

Vous pouvez également envoyer manuellement des courriers électroniques d’enregistrement à vos utilisateurs invités. Cette opération se révèle notamment appropriée si la période d’enregistrement autorisée par le courrier électronique arrive à terme et que l’utilisateur ne peut pas utiliser l’URL pour s’enregistrer. Dans ce cas, vous pouvez renvoyer un courrier électronique d’enregistrement à l’utilisateur invité. Dès que l’utilisateur invité s’enregistre et active son compte, il devient un utilisateur local.

>[!NOTE]
>
>Il est également possible d’ajouter des utilisateurs invités directement par l’intermédiaire de l’annuaire LDAP (Lightweight Directory Access Protocol) référencé par Document Security ou lorsqu’un utilisateur ou un administrateur invite un nouvel utilisateur lors de la création ou de la modification d’une stratégie, déclenchant ainsi l’envoi d’un courrier électronique l’invitant à s’enregistrer. Les utilisateurs peuvent ajouter des utilisateurs invités à des stratégies si vous activez l’option correspondante dans la page Enregistrement d’utilisateur invité.

## Ajout d’un utilisateur invité {#add-an-invited-user}

Vous pouvez ajouter un ou plusieurs comptes d’utilisateurs invités simultanément dans Document Security. Pour ajouter un compte d’utilisateur invité, vous devez connaître l’adresse électronique de l’utilisateur. Lorsque vous ajoutez un utilisateur, Document Security envoie un courrier électronique invitant l’utilisateur à s’enregistrer.

1. Dans Administration Console, cliquez sur Services > Document Security > Utilisateurs invités et locaux, puis cliquez sur Inviter un nouvel utilisateur.
1. Saisissez les adresses électroniques des utilisateurs à inviter. Si vous entrez plusieurs adresses sur la même ligne, séparez-les par une virgule.

   Le message que vous avez créé lors de l’activation de l’enregistrement d’utilisateur invité sera envoyé aux utilisateurs (voir [Configuration de l’enregistrement d’utilisateur invité](/help/forms/using/admin-help/configuring-client-server-options.md#configuring-invited-user-registration)).

1. Cliquez sur OK.

## Affichage des informations d’un utilisateur local  {#view-information-about-a-local-user}

Vous pouvez afficher des informations sur les utilisateurs locaux, notamment le nom, l’adresse électronique, l’entreprise, l’état d’enregistrement et le domaine.

1. Dans Administration Console, cliquez sur Services > Document Security > Utilisateurs invités et locaux, puis cliquez sur Inviter un nouvel utilisateur.
1. Cliquez sur l’onglet Utilisateurs locaux puis, dans la page Gérer des utilisateurs locaux, cliquez sur l’adresse électronique de l’utilisateur à afficher.

   Les détails de l’utilisateur s’affichent et vous pouvez alors réinitialiser le mot de passe de l’utilisateur et désactiver son compte.

## Envoi d’un courrier électronique à un utilisateur externe non enregistré  {#send-an-email-to-an-unregistered-external-user}

Lorsque vous ajoutez un utilisateur invité, Document Security lui envoie automatiquement un courrier électronique l’invitant à s’enregistrer. Vous pouvez également générer manuellement un courrier électronique d’enregistrement à envoyer à l’utilisateur invité non encore enregistré. Vous pouvez par exemple effectuer cette opération pour envoyer une nouvelle invitation si le courrier électronique d’enregistrement de l’utilisateur invité arrive à expiration.

1. Dans Administration Console, cliquez sur Services > Document Security > Utilisateurs invités et locaux.
1. Dans la liste des utilisateurs, cochez la case correspondant à chacun des utilisateurs auxquels envoyer un courrier électronique d’enregistrement, puis cliquez sur Renvoyer le courrier électronique d’invitation.
1. Vérifiez la liste des utilisateurs sélectionnés, puis cliquez sur OK.

## Réinitialisation d’un mot de passe d’utilisateur local  {#reset-a-local-user-password}

Vous pouvez réinitialiser les mots de passe des utilisateurs invités activés qui sont enregistrés dans Document Security mais qui ont oublié leur mot de passe. Lorsque vous réinitialisez un mot de passe, un courrier électronique est envoyé à l’utilisateur avec un nouveau mot de passe temporaire.

Lorsque vous avez activé le processus d’enregistrement des utilisateurs invités, vous avez créé un courrier électronique qui est envoyé aux utilisateurs pour les inviter à réinitialiser leur mot de passe (voir [Configuration de l’enregistrement d’utilisateur invité](/help/forms/using/admin-help/configuring-client-server-options.md#configuring-invited-user-registration)).

1. Dans Administration Console, cliquez sur Services > Document Security > Utilisateurs invités et locaux, puis cliquez sur l’onglet Utilisateurs locaux.
1. Dans la liste des utilisateurs, sélectionnez l’utilisateur approprié.
1. Dans la page Gérer des utilisateurs locaux, cliquez sur Réinitialiser le mot de passe, puis sur OK, Un courrier électronique est envoyé à l’utilisateur avec le nouveau mot de passe.

## Activation ou désactivation d’un compte utilisateur  {#enable-or-disable-a-user-account}

Vous pouvez désactiver un compte d’utilisateur local si vous souhaitez empêcher temporairement un utilisateur d’ouvrir une session Document Security. Lorsque vous désactivez le compte, l’utilisateur ne peut pas utiliser les documents protégés par une stratégie, ni créer ou appliquer des stratégies.

Vous pouvez activer un compte d’utilisateur local désactivé. En revanche, il est impossible d’activer un compte d’utilisateur invité répertorié comme enregistré. L’état enregistré indique que l’utilisateur invité s’est enregistré mais n’a pas encore activé son compte en cliquant sur le lien fourni dans le courrier électronique d’activation.

**Restriction d’un compte utilisateur**

1. Dans Administration Console, cliquez sur Services > Document Security > Utilisateurs invités et locaux, puis cliquez sur l’onglet Utilisateurs locaux.
1. Dans la liste des utilisateurs, sélectionnez l’utilisateur approprié.
1. Dans la page Détails de l’utilisateur local, cliquez sur Compte désactivé.

**Rétablissement d’un compte utilisateur**

1. Cliquez sur Utilisateurs invités et locaux, puis sur l’onglet Utilisateurs locaux.
1. Dans la liste des utilisateurs, sélectionnez l’utilisateur approprié.
1. Dans la page Détails de l’utilisateur local, cliquez sur Compte activé.

## Suppression d’un compte utilisateur invité  {#remove-an-invited-user-account}

Vous pouvez supprimer des comptes d’utilisateurs invités de Document Security. Vous pouvez notamment être amené à supprimer un compte lorsqu’un utilisateur change de compte de messagerie.

Si vous supprimez un compte d’utilisateur, vous ou un autre administrateur êtes les seules personnes habilitées à rétablir le compte à l’aide de l’option Ajouter un utilisateur invité dans la page Utilisateurs invités. Les utilisateurs ne peuvent pas ajouter le compte d’utilisateur supprimé à une stratégie, et aucune invitation ne peut être envoyée par cette méthode.

>[!NOTE]
>
>Les utilisateurs invités supprimés via l’interface Gestion des utilisateurs d’ AEM forms ne peuvent être invités de nouveau qu’après une nouvelle suppression effectuée à l’aide de la procédure suivante.

1. Dans Administration Console, cliquez sur Services > Document Security > Utilisateurs invités et locaux, puis cliquez sur l’onglet Utilisateurs invités.
1. Sélectionnez la case à cocher située en regard d’un ou de plusieurs utilisateurs, cliquez sur Supprimer, puis sur OK.

## Recherche d’un compte utilisateur invité  {#search-for-an-invited-user-account}

Vous pouvez rechercher des comptes d’utilisateurs invités par adresse électronique.

1. Dans Administration Console, cliquez sur Services > Document Security > Utilisateurs invités et locaux.
1. Dans la zone Rechercher un courrier électronique, saisissez l’adresse électronique de l’utilisateur, puis cliquez sur Rechercher.

## Recherche d’un compte utilisateur local  {#search-for-a-local-user-account}

Vous pouvez rechercher un utilisateur local en spécifiant son adresse électronique ou son nom ainsi que son domaine.

1. Dans Administration Console, cliquez sur Services > Document Security > Utilisateurs invités et locaux, puis cliquez sur l’onglet Utilisateurs locaux.
1. Saisissez les critères de recherche dans la zone Rechercher, sélectionnez Nom ou Adresse électronique, puis cliquez sur Rechercher.

## Suppression d’un compte utilisateur local  {#remove-a-local-user-account}

Vous pouvez supprimer des comptes d’utilisateurs locaux de Document Security. Vous pouvez notamment être amené à supprimer des comptes lorsque des utilisateurs changent de compte de messagerie.

1. Dans Administration Console, cliquez sur Services > Document Security > Utilisateurs invités et locaux, puis cliquez sur l’onglet Utilisateurs locaux.
1. Sélectionnez la case à cocher située en regard d’un ou de plusieurs utilisateurs, cliquez sur Supprimer, puis sur OK.

## Tri de la liste des utilisateurs  {#sort-the-user-list}

Pour trouver des utilisateurs plus rapidement, vous pouvez trier la liste par en-tête de colonne. Le triangle situé à côté de l’en-tête de colonne indique la colonne triée :

* Lorsque la pointe du triangle est dirigée vers le haut, l’ordre de tri est croissant.
* Lorsque la pointe du triangle est dirigée vers le bas, l’ordre de tri est décroissant.

   1. Dans Administration Console, cliquez sur Services > Document Security > Utilisateurs invités et locaux.
   1. Pour trier les utilisateurs invités, cliquez sur l’onglet Utilisateurs invités, puis sur l’en-tête de colonne approprié.
   1. Pour trier les utilisateurs locaux, cliquez sur l’onglet Utilisateurs locaux, puis sur l’en-tête de colonne approprié.

