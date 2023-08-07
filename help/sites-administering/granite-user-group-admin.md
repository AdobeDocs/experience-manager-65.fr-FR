---
title: Opérations Granite - Administration des utilisateurs et des groupes
seo-title: Granite Operations - User and Group Administration
description: Découvrez l’administration des utilisateurs et utilisatrices et des groupes Granite.
seo-description: Learn about Granite user and group administration.
uuid: 7b6b7767-712c-4cc8-8d90-36f26280d6e3
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 95ab2e54-0f8d-49e0-ad20-774875f6f80a
exl-id: f3477d21-7e9a-4588-94e8-496bc42434a8
feature: Security
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 94%

---


# Opérations Granite - Administration des utilisateurs et des groupes{#granite-operations-user-and-group-administration}

Granite intègre l’implémentation du référentiel CRX de la spécification API JCR. Elle dispose de sa propre administration d’utilisateurs et utilisatrices et de groupes.

Ces comptes constituent la base sous-jacente de la [Comptes AEM](/help/sites-administering/security.md) et toutes les modifications apportées au compte avec l’administration Granite sont répercutées si/quand les comptes sont accessibles depuis la variable [AEM console Utilisateurs](/help/sites-administering/security.md#accessing-user-administration-with-the-security-console) (par exemple, `http://localhost:4502/useradmin`). Dans la console Utilisateurs d’AEM, vous pouvez également gérer les privilèges et d’autres spécificités d’AEM.

Les consoles d’administration des utilisateurs et utilisatrices et des groupes Granite sont toutes deux disponibles dans la console **[Outils](/help/sites-administering/tools-consoles.md)** de l’UI optimisée pour les écrans tactiles :

![Console Outils](assets/chlimage_1-72a.png)

Choisir entre **Utilisateurs** ou **Groupes** dans la console Outils ouvre la console adéquate. Dans les deux, vous pouvez agir soit en utilisant la case à cocher, puis les actions de la barre d’outils, soit en ouvrant les détails du compte via le lien situé sous **Nom**.

* [Administration des utilisateurs](#user-administration)

  ![chlimage_1-73](assets/chlimage_1-73a.png)

  Les listes de la console **Utilisateurs** :

   * le nom d’utilisateur ou d’utilisatrice
   * l’identifiant de connexion de l’utilisateur (nom de compte)
   * tout titre attribué au compte

* [Administration des groupes](#group-administration)

  ![Console de gestion des utilisateurs](assets/chlimage_1-74a.png)

  Les listes de la console **Groupes** :

   * le nom du groupe
   * la description du groupe
   * le nombre d’utilisateurs et utilisatrices/de groupes dans le groupe

## Administration des utilisateurs {#user-administration}

### Ajout d’un nouvel utilisateur ou d’une nouvelle utilisatrice {#adding-a-new-user}

1. Utilisez l’icône **Ajouter un utilisateur ou une utilisatrice** :

   ![Icône Ajouter un utilisateur](do-not-localize/chlimage_1-1.png)

1. Le formulaire **Créer un utilisateur ou une utilisatrice** s’ouvre :

   ![Formulaire de détails utilisateur](assets/chlimage_1-75a.png)

   Vous pouvez y saisir les détails de l’utilisateur pour le compte (la plupart sont des détails standard et explicites) :

   * **ID**

      Il s’agit de l’identifiant unique du compte utilisateur. Il est obligatoire et ne peut pas contenir d’espaces.

   * **Adresse électronique**
   * **Mot de passe**

     Le mot de passe est obligatoire.

   * **Confirmer le mot de passe**

     Ce champ est obligatoire car nécessaire à la confirmation du mot de passe.

   * **Prénom**
   * **Nom**
   * **Numéro de téléphone**
   * **Fonction**
   * **Rue**
   * **Mobile**
   * **Ville**
   * **Code postal**
   * **Pays**
   * **État**
   * **Titre**
   * **Genre**
   * **À propos**
   * **Paramètres du compte**

      * **Statut**
Vous pouvez marquer le compte comme **actif** ou **inactif**.

   * **Photo**

     Vous pouvez ici charger une photo à utiliser comme avatar.

     Types de fichiers acceptés : `.jpg .png .tif .gif`

     Taille préférée : `240x240px`

   * **Ajouter un utilisateur aux groupes**

     Utilisez le menu déroulant de sélection pour sélectionner les groupes dont l’utilisateur doit être membre. Pour les groupes déjà sélectionnés, utilisez le **X** à côté du nom pour les désélectionner avant d’enregistrer.

   * **Groupes**

     Liste des groupes dont l’utilisateur est actuellement membre. Utilisez le **X** à côté du nom pour les désélectionner avant d’enregistrer.

1. Lorsque vous avez défini le compte d’utilisateur, utilisez :

   * **Annuler** pour abandonner l’enregistrement ;
   * **Enregistrer** pour terminer l’enregistrement. La création du compte d’utilisateur est confirmée par un message.

### Modification d’un utilisateur existant {#editing-an-existing-user}

1. Accédez aux détails de l’utilisateur à partir du lien situé sous le nom d’utilisateur dans la console Utilisateurs.

1. Vous pouvez à présent modifier les détails comme indiqué dans la rubrique [Ajout d’un nouvel utilisateur](#adding-a-new-user).

1. Accédez aux détails de l’utilisateur à partir du lien situé sous le nom d’utilisateur dans la console Utilisateurs.

1. Vous pouvez à présent modifier les détails comme indiqué dans la rubrique [Ajout d’un nouvel utilisateur](#adding-a-new-user).

### Modification du mot de passe d’un utilisateur {#changing-the-password-for-an-existing-user}

1. Accédez aux détails de l’utilisateur à partir du lien situé sous le nom d’utilisateur dans la console Utilisateurs.

1. Vous pouvez à présent modifier les détails comme indiqué dans la rubrique [Ajout d’un nouvel utilisateur](#adding-a-new-user). Sous **Paramètres du compte** se trouve un lien permettant de **Modifier le mot de passe**.

   ![Boîte de dialogue Paramètres du compte](assets/chlimage_1-76a.png)

1. La boîte de dialogue **Modifier le mot de passe** s’ouvre. Saisissez et confirmez le nouveau mot de passe, ainsi que votre mot de passe. Cliquez sur **OK** pour confirmer les modifications.

   ![Boîte de dialogue Modifier le mot de passe](assets/chlimage_1-77a.png)

   Un message confirme que le mot de passe a été modifié.

### Attribution rapide de groupes {#quick-group-assignment}

1. Utilisez la case à cocher pour marquer plusieurs utilisateurs ou utilisatrices.
1. Utilisez l’icône **Groupes** :

   ![Utilisation de l’icône Groupes](do-not-localize/chlimage_1-2.png)

   Pour ouvrir le menu déroulant de sélection de groupe :

   ![Sélecteur de groupes](assets/chlimage_1-78a.png)

1. Dans la boîte de dialogue de sélection, vous pouvez sélectionner ou désélectionner les groupes auxquels le compte utilisateur doit appartenir.

1. Lorsque vous avez affecté les groupes ou avez annulé leur affectation selon les besoins, utilisez :

   * **Annuler** pour abandonner les modifications ;
   * **Enregistrer** pour confirmer les modifications.

### Suppression de détails d’utilisateur ou d’utilisatrice existants {#deleting-existing-user-details}

1. Utilisez la case à cocher pour marquer plusieurs utilisateurs ou utilisatrices.
1. Utilisez l’icône **Supprimer** pour supprimer les détails de l’utilisateur :

   ![Suppression de détails d’utilisateur ou d’utilisatrice existants](do-not-localize/chlimage_1-3.png)

1. Vous êtes invité(e) à confirmer la suppression, puis un message confirme que la suppression a eu lieu.

## Administration des groupes {#group-administration}

### Ajout d’un nouveau groupe {#adding-a-new-group}

1. Utilisez l’icône Ajouter un groupe :

   ![Ajouter un nouveau groupe](do-not-localize/chlimage_1-4.png)

1. Le formulaire **Créer un groupe** s’ouvre :

   ![Formulaire Détails du groupe](assets/chlimage_1-79a.png)

   Vous pouvez y saisir les détails du groupe :

   * **ID**

     Il s’agit d’un identifiant unique pour le groupe. Il est obligatoire et ne peut pas contenir d’espaces.

   * **Nom**

     Nom du groupe. Il est affiché dans la console Groupes.

   * **Description**

     Description du groupe.

   * **Ajouter des membres au groupe**

     Utilisez le menu déroulant de sélection pour sélectionner un ou des utilisateurs à ajouter au groupe. Pour les groupes déjà sélectionnés, utilisez le **X** à côté du nom pour les désélectionner avant d’enregistrer.

   * **Membres du groupe**

     Liste des utilisateurs figurant dans le groupe. Utilisez le **X** à côté du nom pour les désélectionner avant d’enregistrer.

1. Lorsque vous avez défini le groupe, utilisez :

   * **Annuler** pour abandonner l’enregistrement ;
   * **Enregistrer** pour terminer l’enregistrement. La création du groupe est confirmée par un message.

### Modification d’un groupe existant {#editing-an-existing-group}

1. Accédez aux détails du groupe à partir du lien situé sous le nom de groupe dans la console Groupes.

1. Vous pouvez à présent modifier les détails comme indiqué dans la rubrique [Ajout d’un nouveau groupe](#adding-a-new-group).

### Copie d’un groupe existant {#copying-an-existing-group}

1. Utilisez la case à cocher pour marquer un groupe.
1. Utilisez l’icône **Copier** pour copier les détails du groupe :

   ![Copier un groupe existant](do-not-localize/chlimage_1-5.png)

1. Le formulaire **Modifier les paramètres de groupe** s’ouvre.

   L’identifiant de groupe est identique à l’identifiant d’origine, mais comporte le préfixe `Copy of`. Vous devez le modifier, car l’identifiant ne peut pas contenir d’espaces. Tous les autres détails sont identiques aux détails d’origine.

   Vous pouvez à présent modifier les détails comme indiqué dans la rubrique [Ajout d’un nouveau groupe](#adding-a-new-group).

### Suppression d’un groupe existant {#deleting-an-existing-group}

1. Utilisez la case à cocher pour marquer un ou plusieurs groupes.
1. Utilisez l’icône **Supprimer** pour supprimer les détails du groupe :

   ![Suppression d’un groupe existant](do-not-localize/chlimage_1-6.png)

1. Vous êtes invité à confirmer la suppression, puis un message confirme que la suppression a eu lieu.
