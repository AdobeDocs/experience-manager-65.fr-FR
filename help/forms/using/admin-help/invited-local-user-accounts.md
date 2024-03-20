---
title: Gérer les comptes d’utilisateurs et d’utilisatrices invités et locaux
description: Document Security vous permet de rechercher, d’afficher, de modifier, de verrouiller, de déverrouiller et de supprimer des comptes d’utilisateurs invités et locaux.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
exl-id: 23f71b34-a0cb-4664-bb8b-a60f33dc70d8
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1196'
ht-degree: 1%

---

# Gérer les comptes d’utilisateurs et d’utilisatrices invités et locaux {#managing-invited-and-local-user-accounts}

Utilisez la page Utilisateurs invités et locaux pour gérer vos utilisateurs invités et locaux. Cette page s’affiche uniquement si les conditions suivantes sont remplies :

* Vous êtes un administrateur auquel sont attribués les rôles Gestion des utilisateurs invités et locaux de Document Security et Utilisateur d’Administration Console. (Voir [Création et configuration de rôles](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles).)
* L’enregistrement d’utilisateur invité est activé. (Voir [Configuration de l’enregistrement d’utilisateur invité](/help/forms/using/admin-help/configuring-client-server-options.md#configuring-invited-user-registration).)

La page Utilisateurs invités et locaux contient deux onglets que vous pouvez utiliser pour rechercher, afficher, modifier, verrouiller, déverrouiller et supprimer des comptes d’utilisateurs invités et locaux.

Vous pouvez également envoyer manuellement des courriers électroniques d’enregistrement à vos utilisateurs invités. Vous pouvez le faire, par exemple, si la période d’enregistrement autorisée par le courrier électronique se termine et que l’utilisateur ne peut pas utiliser l’URL pour s’enregistrer. Dans ce cas, vous pouvez renvoyer un courrier électronique d’enregistrement à l’utilisateur invité. Lorsque l’utilisateur invité s’enregistre et active le compte, il devient un utilisateur local.

>[!NOTE]
>
>Les utilisateurs invités peuvent également être ajoutés directement par l’intermédiaire de l’annuaire LDAP référencé par Document Security, ou lorsqu’un utilisateur ou un administrateur invite un nouvel utilisateur lors de la création ou de la modification d’une stratégie, déclenchant ainsi l’envoi d’un courrier électronique d’invitation à l’enregistrement. Les utilisateurs peuvent ajouter de nouveaux utilisateurs invités aux stratégies si vous activez l’option Activer l’enregistrement d’utilisateur invité sur la page Enregistrement d’utilisateur invité .

## Ajout d’un utilisateur invité {#add-an-invited-user}

Vous pouvez ajouter à la fois un ou plusieurs comptes d’utilisateurs invités à Document Security. Pour ajouter un compte d’utilisateur invité, vous devez connaître l’adresse électronique de l’utilisateur. Lorsque vous ajoutez un utilisateur, Document Security envoie un courrier électronique invitant l’utilisateur à s’enregistrer.

1. Dans Administration Console, cliquez sur Services > Document Security > Utilisateurs invités et locaux, puis cliquez sur Inviter un nouvel utilisateur.
1. Saisissez les adresses électroniques des utilisateurs que vous souhaitez inviter. Saisissez plusieurs adresses sur une ligne, séparées par une virgule.

   Le message que vous avez créé lors de l’activation de l’enregistrement d’utilisateur invité est envoyé aux utilisateurs. (Voir [Configuration de l’enregistrement d’utilisateur invité](/help/forms/using/admin-help/configuring-client-server-options.md#configuring-invited-user-registration).)

1. Cliquez sur OK.

## Affichage des informations sur un utilisateur local {#view-information-about-a-local-user}

Vous pouvez afficher des informations sur les utilisateurs locaux, notamment le nom, l’adresse électronique, l’organisation, l’état d’enregistrement et le domaine.

1. Dans Administration Console, cliquez sur Services > Document Security > Utilisateurs invités et locaux, puis cliquez sur Inviter un nouvel utilisateur.
1. Cliquez sur l’onglet Utilisateurs locaux et, sur la page Gérer les utilisateurs locaux, cliquez sur l’adresse électronique de l’utilisateur que vous souhaitez afficher.

   Les détails de l’utilisateur s’affichent. Vous pouvez réinitialiser le mot de passe de l’utilisateur et désactiver le compte.

## Envoi d’un courrier électronique à un utilisateur externe non enregistré {#send-an-email-to-an-unregistered-external-user}

Lorsque vous ajoutez un utilisateur invité, Document Security lui envoie automatiquement une demande d’enregistrement par courrier électronique. Vous pouvez également générer manuellement un courrier électronique d’enregistrement à envoyer à un utilisateur invité qui ne s’est pas encore enregistré. Vous pouvez le faire, par exemple, pour envoyer une nouvelle invitation si le courrier électronique d’enregistrement d’un utilisateur invité expire.

1. Dans Administration Console, cliquez sur Services > Document Security > Utilisateurs invités et locaux.
1. Dans la liste des utilisateurs, cochez la case correspondant à chaque utilisateur auquel envoyer un courrier électronique d’enregistrement, puis cliquez sur Envoyer un courrier électronique d’invitation.
1. Vérifiez la liste des utilisateurs sélectionnés et cliquez sur OK.

## Réinitialisation d’un mot de passe utilisateur local {#reset-a-local-user-password}

Vous pouvez réinitialiser les mots de passe des utilisateurs invités activés qui se sont enregistrés avec Document Security mais qui ont oublié leur mot de passe. Lorsque vous réinitialisez un mot de passe, un courrier électronique contenant un nouveau mot de passe temporaire est généré pour l’utilisateur.

Lorsque vous avez activé le processus d’enregistrement des utilisateurs invités, vous avez créé un message électronique qui sera envoyé aux utilisateurs pour leur demander de réinitialiser leurs mots de passe. (Voir [Configuration de l’enregistrement d’utilisateur invité](/help/forms/using/admin-help/configuring-client-server-options.md#configuring-invited-user-registration).)

1. Dans Administration Console, cliquez sur Services > Document Security > Utilisateurs invités et locaux, puis cliquez sur l’onglet Utilisateurs locaux.
1. Dans la liste des utilisateurs, sélectionnez l’utilisateur approprié.
1. Sur la page Gérer les utilisateurs locaux, cliquez sur Réinitialiser le mot de passe, puis sur OK. Un courrier électronique de réinitialisation du mot de passe contenant le nouveau mot de passe est envoyé à l’utilisateur.

## Activation ou désactivation d’un compte utilisateur {#enable-or-disable-a-user-account}

Vous pouvez désactiver les comptes d’utilisateurs locaux pour empêcher temporairement un utilisateur de se connecter à Document Security. Lorsque vous désactivez le compte, l’utilisateur ne peut pas utiliser de documents protégés par une stratégie ni créer ni appliquer de stratégies.

Vous pouvez activer un compte d’utilisateur local actuellement désactivé. Vous ne pouvez pas activer un compte d’utilisateur invité répertorié comme enregistré. Le statut enregistré indique que l’utilisateur invité est enregistré mais n’a pas encore activé le compte à l’aide du lien figurant dans l’e-mail d’activation.

**Limitation d’un compte d’utilisateur**

1. Dans Administration Console, cliquez sur Services > Document Security > Utilisateurs invités et locaux, puis cliquez sur l’onglet Utilisateurs locaux.
1. Dans la liste des utilisateurs, sélectionnez l’utilisateur approprié.
1. Sur la page Détails de l’utilisateur local, cliquez sur Désactiver le compte.

**Rétablissement d’un compte utilisateur**

1. Cliquez sur Utilisateurs invités et locaux, puis sur l’onglet Utilisateurs locaux .
1. Dans la liste des utilisateurs, sélectionnez l’utilisateur approprié.
1. Sur la page Détails de l’utilisateur local, cliquez sur Compte activé.

## Suppression d’un compte d’utilisateur invité {#remove-an-invited-user-account}

Vous pouvez supprimer des comptes d’utilisateurs invités de Document Security. Vous pouvez par exemple souhaiter supprimer un compte lorsqu’un utilisateur modifie ses informations de compte de messagerie personnelles.

Si vous supprimez un compte d’utilisateur, seul vous ou un autre administrateur pouvez rétablir le compte en sélectionnant l’option Ajouter un utilisateur invité sur la page Utilisateurs invités . Les utilisateurs ne peuvent pas ajouter le compte d’utilisateur supprimé à une stratégie et aucun processus d’invitation ne peut être lancé par cette méthode.

>[!NOTE]
>
>Les utilisateurs invités qui ont été supprimés via l’interface de gestion des utilisateurs d’AEM forms ne peuvent pas être réinvités tant qu’ils n’ont pas été à nouveau supprimés à l’aide de la procédure suivante.

1. Dans Administration Console, cliquez sur Services > Document Security > Utilisateurs invités et locaux, puis cliquez sur l’onglet Utilisateurs invités .
1. Cochez la case en regard d’un ou de plusieurs utilisateurs, cliquez sur Supprimer, puis sur OK.

## Recherche d’un compte d’utilisateur invité {#search-for-an-invited-user-account}

Vous pouvez rechercher des comptes d’utilisateurs invités à l’aide d’une adresse électronique.

1. Dans Administration Console, cliquez sur Services > Document Security > Utilisateurs invités et locaux.
1. Dans la zone Rechercher un courrier électronique, saisissez l’adresse électronique de l’utilisateur, puis cliquez sur Rechercher.

## Recherche d’un compte utilisateur local {#search-for-a-local-user-account}

Vous pouvez rechercher un utilisateur local à l’aide de l’adresse électronique ou du nom et du domaine de l’utilisateur.

1. Dans Administration Console, cliquez sur Services > Document Security > Utilisateurs invités et locaux, puis cliquez sur l’onglet Utilisateurs locaux.
1. Saisissez les critères de recherche dans la zone Rechercher, sélectionnez Nom ou Adresse électronique, puis cliquez sur Rechercher.

## Suppression d’un compte utilisateur local {#remove-a-local-user-account}

Vous pouvez supprimer des comptes d’utilisateurs locaux de Document Security. Vous pouvez, par exemple, supprimer des comptes lorsque des utilisateurs modifient leurs informations de compte de messagerie.

1. Dans Administration Console, cliquez sur Services > Document Security > Utilisateurs invités et locaux, puis cliquez sur l’onglet Utilisateurs locaux.
1. Cochez la case en regard d’un ou de plusieurs utilisateurs, cliquez sur Supprimer, puis sur OK.

## Tri de la liste des utilisateurs {#sort-the-user-list}

Vous pouvez trouver plus facilement des utilisateurs en triant la liste des utilisateurs par en-tête de colonne. Les icônes en forme de triangle situées à côté de l’en-tête de colonne indiquent la colonne à trier :

* Un triangle pointant vers le haut indique l’ordre croissant.
* Un triangle pointant vers le bas indique l’ordre décroissant.

   1. Dans Administration Console, cliquez sur Services > Document Security > Utilisateurs invités et locaux.
   1. Pour trier les utilisateurs invités, cliquez sur l’onglet Utilisateurs invités et cliquez sur l’en-tête de colonne approprié.
   1. Pour trier les utilisateurs locaux, cliquez sur l’onglet Utilisateurs locaux, puis sur l’en-tête de colonne approprié.
