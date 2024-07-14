---
title: Gérer les comptes d’utilisateurs et d’utilisatrices invités et locaux
description: Grâce à Document Security, vous pouvez rechercher, afficher, modifier, verrouiller, déverrouiller et supprimer des comptes d’utilisateurs invités et locaux.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
exl-id: 23f71b34-a0cb-4664-bb8b-a60f33dc70d8
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1196'
ht-degree: 100%

---

# Gérer les comptes d’utilisateurs et d’utilisatrices invités et locaux {#managing-invited-and-local-user-accounts}

Utilisez la page Utilisateurs invités et locaux pour gérer les utilisateurs et utilisatrices invités et locaux. Cette page s’affiche uniquement si les conditions suivantes sont remplies :

* Vous êtes administrateur ou administratrice et possédez le rôle Gérer les utilisateurs invités et locaux de Document Security ainsi que le rôle Utilisateur de la console d’administration. (Voir [Création et configuration de rôles](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles).)
* L’inscription des utilisateurs et utilisatrices invités est activé. (Voir [Configuration de l’inscription des utilisateurs et utilisatrices invités](/help/forms/using/admin-help/configuring-client-server-options.md#configuring-invited-user-registration).)

La page Utilisateurs et utilisatrices invités et locaux contient deux onglets que vous pouvez utiliser pour rechercher, afficher, modifier, verrouiller, déverrouiller et supprimer des comptes d’utilisateurs et utilisatrices invités et locaux.

Vous pouvez également envoyer manuellement des e-mails d’inscription aux utilisateurs et utilisatrices invités. Cela peut notamment être utile si la période d’inscription autorisée par l’e-mail se termine et que l’utilisateur ou l’utilisatrice ne peut pas utiliser l’URL pour s’inscrire. Dans ce cas, vous pouvez renvoyer un e-mail d’inscription à l’utilisateur ou l’utilisatrice invité. Lorsque l’utilisateur ou l’utilisatrice invité s’inscrit et active le compte, il ou elle devient un utilisateur local ou une utilisatrice locale.

>[!NOTE]
>
>Vous pouvez également ajouter des utilisateurs et utilisatrices invités directement via l’annuaire LDAP que Document Security référence, ou lorsqu’un utilisateur ou une utilisatrice ou un administrateur ou une administratrice invite un nouvel utilisateur ou une nouvelle utilisatrice lors de la création ou de la modification d’une politique, lançant ainsi un e-mail d’invitation à l’inscription. Les utilisateurs et utilisatrices peuvent ajouter de nouveaux utilisateurs et utilisatrices invités aux politiques si vous activez l’option Activer l’inscription des utilisateurs et utilisatrices invités sur la page Inscription des utilisateurs et utilisatrices invités.

## Ajouter un utilisateur ou une utilisatrice invité {#add-an-invited-user}

Vous pouvez ajouter un ou plusieurs comptes d’utilisateurs ou utilisatrices invités à la fois à Document Security. Pour ajouter un compte d’utilisateur ou d’utilisatrice invité, vous avez besoin de l’adresse e-mail de l’utilisateur ou l’utilisatrice. Lorsque vous ajoutez un utilisateur ou une utilisatrice, Document Security envoie un e-mail d’inscription l’invitant à s’inscrire.

1. Dans la console d’administration, cliquez sur Services > Document Security > Utilisateurs invités et locaux, puis cliquez sur Inviter un nouvel utilisateur.
1. Saisissez les adresses e-mail des utilisateurs et utilisatrices que vous souhaitez inviter. Saisissez plusieurs adresses sur une ligne, séparées par une virgule.

   Le message que vous avez créé lors de l’activation de l’inscription des utilisateurs et utilisatrices invités leur est envoyé. (Voir [Configuration de l’inscription des utilisateurs et utilisatrices invités](/help/forms/using/admin-help/configuring-client-server-options.md#configuring-invited-user-registration).)

1. Cliquez sur OK.

## Affichage des informations sur un utilisateur local ou une utilisatrice locale {#view-information-about-a-local-user}

Vous pouvez afficher des informations sur les utilisateurs et utilisatrices locaux, notamment le nom, l’adresse e-mail, l’organisation, le statut de l’inscription et le domaine.

1. Dans la console d’administration, cliquez sur Services > Document Security > Utilisateurs invités et locaux, puis cliquez sur Inviter un nouvel utilisateur.
1. Cliquez sur l’onglet Utilisateurs et utilisatrices locaux et, sur la page Gérer les utilisateurs et utilisatrices locaux, cliquez sur l’adresse e-mail de l’utilisateur ou l’utilisatrice que vous souhaitez afficher.

   Les détails de l’utilisateur ou l’utilisatrice s’affichent et vous pouvez réinitialiser son mot de passe et désactiver le compte.

## Envoyer un e-mail à un utilisateur ou une utilisatrice externe non enregistré {#send-an-email-to-an-unregistered-external-user}

Lorsque vous ajoutez un utilisateur invité ou une utilisatrice invitée, Document Security lui envoie automatiquement une demande d’inscription par e-mail. Vous pouvez également générer manuellement un e-mail d’inscription à envoyer à un utilisateur invité ou une utilisatrice invitée qui n’est pas encore inscrit(e). Cela est notamment utile pour envoyer une nouvelle invitation si l’e-mail d’inscription d’un utilisateur invité ou d’une utilisatrice invitée a expiré.

1. Dans la console d’administration, cliquez sur Services > Document Security > Utilisateurs invités et locaux.
1. Dans la liste des utilisateurs et utilisatrices, cochez la case des utilisateur et utilisatrices auxquels envoyer un e-mail d’inscription, puis cliquez sur Renvoyer l’e-mail d’invitation.
1. Vérifiez la liste des utilisateurs et utilisatrices sélectionnés et cliquez sur OK.

## Réinitialiser le mot de passe d’un utilisateur local ou d’une utilisatrice locale {#reset-a-local-user-password}

Vous pouvez réinitialiser les mots de passe des utilisateurs et utilisatrices invités activés qui se sont inscrits avec Document Security mais qui ont oublié leur mot de passe. Lorsque vous réinitialisez un mot de passe, un e-mail est généré contenant un nouveau mot de passe temporaire pour l’utilisateur ou l’utilisatrice.

Lorsque vous avez activé le processus d’inscription des utilisateurs et utilisatrices invités, vous avez créé un e-mail qui sera envoyé aux utilisateurs et utilisatrices les invitant à réinitialiser leur mot de passe. (Voir [Configuration de l’inscription des utilisateurs et utilisatrices invités](/help/forms/using/admin-help/configuring-client-server-options.md#configuring-invited-user-registration).)

1. Dans la console d’administration, cliquez sur Services > Document Security > Utilisateurs invités et locaux, puis cliquez sur l’onglet Utilisateurs locaux.
1. Dans la liste des utilisateurs et utilisatrices, sélectionnez la personne appropriée.
1. Sur la page Gérer les utilisateurs locaux, cliquez sur Réinitialiser le mot de passe, puis cliquez sur OK. Un e-mail de réinitialisation du mot de passe contenant le nouveau mot de passe est envoyé à l’utilisateur ou l’utilisatrice.

## Activer ou désactiver un compte d’utilisateur {#enable-or-disable-a-user-account}

Vous pouvez désactiver les comptes d’utilisateurs locaux pour empêcher temporairement un utilisateur ou une utilisatrice de se connecter à Document Security. Lorsque vous désactivez le compte, l’utilisateur ou l’utilisatrice ne peut pas utiliser de documents protégés par une politique ni créer ou appliquer des politiques.

Vous pouvez activer un compte d’utilisateur local actuellement désactivé. Vous ne pouvez pas activer un compte d’utilisateur invité répertorié comme enregistré. Le statut enregistré indique que la personne invitée est enregistrée mais qu’elle n’a pas encore activé le compte en utilisant le lien dans l’e-mail d’activation.

**Restreindre un compte d’utilisateur**

1. Dans la console d’administration, cliquez sur Services > Document Security > Utilisateurs invités et locaux, puis cliquez sur l’onglet Utilisateurs locaux.
1. Dans la liste des utilisateurs et utilisatrices, sélectionnez la personne appropriée.
1. Sur la page Détails de l’utilisateur local, cliquez sur Désactiver le compte.

**Rétablir un compte d’utilisateur**

1. Cliquez sur Utilisateurs invités et locaux, puis sur l’onglet Utilisateurs locaux.
1. Dans la liste des utilisateurs et utilisatrices, sélectionnez la personne appropriée.
1. Sur la page Détails de l’utilisateur local, cliquez sur Activer le compte.

## Supprimer un compte d’utilisateur invité {#remove-an-invited-user-account}

Vous pouvez supprimer les comptes d’utilisateurs invités de Document Security. Vous souhaiterez peut-être supprimer un compte, par exemple, lorsqu’une personne modifie les informations de son compte de messagerie personnel.

Si vous supprimez un compte d’utilisateur, son rétablissement à l’aide de l’option Ajouter un utilisateur invité sur la page Utilisateurs invités peut uniquement être effectué par vous-même ou par un administrateur ou une administratrice. Les utilisateurs et utilisatrices ne peuvent pas ajouter le compte d’utilisateur supprimé à une politique et aucun processus d’invitation ne peut être lancé par cette méthode.

>[!NOTE]
>
>Les personnes invitées qui ont été supprimées via l’interface d’User Management d’AEM Forms ne peuvent pas être réinvitées tant qu’elles n’ont pas été à nouveau supprimées à l’aide de la procédure suivante.

1. Dans la console d’administration, cliquez sur Services > Document Security > Utilisateurs invités et locaux, puis cliquez sur l&#39;onglet Utilisateurs invités.
1. Cochez la case située en regard d’une ou de plusieurs personnes, cliquez sur Supprimer, puis sur OK.

## Rechercher un compte d’utilisateur invité {#search-for-an-invited-user-account}

Vous pouvez rechercher des comptes d’utilisateur invités en utilisant une adresse e-mail.

1. Dans la console d’administration, cliquez sur Services > Document Security > Utilisateurs invités et locaux.
1. Dans la zone Rechercher une adresse e-mail, saisissez l’adresse e-mail de la personne, puis cliquez sur Rechercher.

## Rechercher un compte d’utilisateur local {#search-for-a-local-user-account}

Vous pouvez rechercher une personne locale en utilisant son adresse e-mail ou son nom et son domaine.

1. Dans la console d’administration, cliquez sur Services > Document Security > Utilisateurs invités et locaux, puis cliquez sur l’onglet Utilisateurs locaux.
1. Tapez les critères de recherche dans la zone Rechercher, sélectionnez Nom ou Adresse e-mail, puis cliquez sur Rechercher.

## Supprimer un compte d’utilisateur local {#remove-a-local-user-account}

Vous pouvez supprimer des comptes d’utilisateur locaux de Document Security. Vous souhaiterez peut-être supprimer des comptes, par exemple, lorsque les personnes modifient les informations de leur compte de messagerie personnel.

1. Dans la console d’administration, cliquez sur Services > Document Security > Utilisateurs invités et locaux, puis cliquez sur l’onglet Utilisateurs locaux.
1. Cochez la case située en regard d’une ou de plusieurs personnes, cliquez sur Supprimer, puis sur OK.

## Trier la liste des utilisateurs et utilisatrices {#sort-the-user-list}

Vous pouvez trouver des personnes plus facilement en triant la liste des utilisateurs et utilisatrices par en-tête de colonne. Les icônes triangulaires à côté de l’en-tête de colonne indiquent la colonne actuellement utilisée pour le tri :

* Un triangle pointant vers le haut indique un ordre croissant.
* Un triangle pointant vers le bas indique un ordre décroissant.

   1. Dans la console d’administration, cliquez sur Services > Document Security > Utilisateurs invités et locaux.
   1. Pour trier les personnes invitées, cliquez sur l’onglet Utilisateurs invités et cliquez sur l’en-tête de colonne approprié.
   1. Pour trier les personnes locales, cliquez sur l’onglet Utilisateurs locaux et cliquez sur l’en-tête de colonne approprié.
