---
title: Configuration des files d’attente partagées
seo-title: Configuration des files d’attente partagées
description: Découvrez comment utiliser les files d’attente partagées pour les flux de travaux Forms sur AEM Forms sur OSGi.
seo-description: Découvrez comment utiliser les files d’attente partagées pour les flux de travaux Forms sur AEM Forms sur OSGi.
uuid: null
topic-tags: process
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: null
docset: aem65
translation-type: tm+mt
source-git-commit: 9a250e739adcf094856f1eafa75de2649d6d3d5f

---


# Partage et demande l’accès aux éléments de boîte de réception d’un utilisateur {#share-and-request-access}

Une file d’attente est une liste d’éléments dans la boîte de réception AEM d’un utilisateur. Il peut s’agir d’éléments affectés à un utilisateur ou d’éléments partagés dans le groupe auquel appartient un utilisateur. Vous pouvez accéder à votre boîte de réception pour afficher et agir sur l’élément de boîte de réception. Par exemple, partagez un élément avec un autre utilisateur.

Vous pouvez également partager vos éléments de boîte de réception avec un autre utilisateur. Une fois qu’un autre utilisateur a accès à vos éléments de boîte de réception, il peut demander et prendre les mesures appropriées sur les éléments partagés. De même, vous pouvez demander à d’autres utilisateurs l’accès aux éléments de la boîte de réception.

## Conditions préalables {#pre-requisites}

L’utilisateur connecté doit être membre du `workflow-users` groupe. L’utilisateur peut partager des éléments ou demander l’accès aux éléments uniquement aux utilisateurs sur lesquels l’utilisateur connecté dispose d’autorisations de lecture ou uniquement aux utilisateurs qui ont activé le profil public.

## Partage d’un ou de tous les éléments de votre boîte de réception avec un autre utilisateur

La boîte de réception AEM vous permet de partager un ou tous les éléments de votre boîte de réception avec un autre utilisateur.

### Partage de tous les éléments de la boîte de réception

Pour partager tous les éléments d’une boîte de réception avec un autre utilisateur, procédez comme suit :

1. Connectez-vous à votre instance AEM. Appuyez sur l’icône ![Boîte de réception](assets/bell.svg) et appuyez sur **[!UICONTROL Afficher tout]**. Une liste de vos éléments de boîte de réception s’affiche.
1. Appuyez sur l’icône ![Afficher le sélecteur](assets/viewlist.svg) ou ![Afficher le sélecteur](assets/calendar.svg) en regard du bouton **[!UICONTROL Créer]** et appuyez sur **[!UICONTROL Paramètres.]** La boîte de dialogue des paramètres s’affiche.
1. Ouvrez l’onglet **[!UICONTROL Partager]** dans la boîte de dialogue des paramètres.
1. Entrez le nom d’un utilisateur dans la zone de texte **[!UICONTROL Octroi de l’accès aux éléments]** de la boîte de réception et appuyez sur **[!UICONTROL Octroi]**. Répétez l’étape pour ajouter d’autres utilisateurs. Tous les utilisateurs ayant accès à vos éléments apparaissent sous la section **Nom d’utilisateur** .
1. Appuyez sur **[!UICONTROL Enregistrer]**.

>[!NOTE]
>
> (Pour les éléments de flux de travail centrés sur les formulaires uniquement) Activez l’option **[Autoriser les personnes désignées à partager via la boîte de réception de l’étape](aem-forms-workflow-step-reference.md)**Attribuer la tâche ****dans le flux de travail. Seuls les éléments pour lesquels l’option mentionnée ci-dessus est activée s’affichent pour les autres utilisateurs.

### Partage d’éléments individuels

Pour partager un élément de boîte de réception avec un autre utilisateur, procédez comme suit :

1. Connectez-vous à votre instance AEM. Appuyez sur l’icône ![Boîte de réception](assets/bell.svg) et appuyez sur **[!UICONTROL Afficher tout]**. Une liste de vos éléments de boîte de réception s’affiche.
1. Sélectionnez un élément et appuyez sur **[!UICONTROL Partager]**. Une boîte de dialogue s’affiche.
1. Entrez le nom d’un utilisateur dans la zone de texte Ajouter des utilisateurs pour partager cet élément et appuyez sur **[!UICONTROL Ajouter]**. Répétez l’étape pour ajouter d’autres utilisateurs. Tous les utilisateurs ayant accès à vos éléments apparaissent sous la section **[!UICONTROL Nom d’utilisateur]** .
1. Appuyez sur **[!UICONTROL Enregistrer]**.


>[!NOTE]
>
> (Pour les éléments de flux de travail centrés sur Forms uniquement) Activez l’option **[Autoriser les personnes désignées à partager explicitement dans la boîte de réception](aem-forms-workflow-step-reference.md)**de l’étape **Attribuer la tâche**dans le flux de travail. Seuls les éléments pour lesquels l’option mentionnée ci-dessus est activée s’affichent pour les autres utilisateurs.

## Request access to Inbox items {#request-access}

Vous pouvez demander l’accès aux éléments de la boîte de réception d’un autre utilisateur. Une fois l’accès accordé, vous pouvez afficher, demander et prendre les actions appropriées sur les éléments partagés. Effectuez les étapes suivantes pour demander l’accès aux éléments de boîte de réception d’un autre utilisateur :

1. Connectez-vous à votre instance AEM. Appuyez sur l’icône ![Afficher le sélecteur](assets/bell.svg) et appuyez sur **[!UICONTROL Afficher tout]**.
1. Appuyez sur l’icône ![Afficher le sélecteur](assets/viewlist.svg) ou ![Afficher le sélecteur](assets/calendar.svg) en regard du bouton **[!UICONTROL Créer]** et appuyez sur **[!UICONTROL Paramètres.]** La boîte de dialogue des paramètres s’affiche.
1. Entrez le nom d’un utilisateur dans la zone de texte **[!UICONTROL Demander l’accès aux éléments de la boîte de réception de l’utilisateur]** et appuyez sur **[!UICONTROL Demander]**. Une requête est envoyée à l’utilisateur et son état est affiché par rapport au nom de l’utilisateur. Répétez l’étape pour ajouter d’autres utilisateurs.
1. Appuyez sur **[!UICONTROL Enregistrer]**. La requête est envoyée en tant qu’élément de boîte de réception aux utilisateurs. L’utilisateur peut sélectionner l’élément et appuyer sur Approuver ou Rejeter pour accorder ou rejeter l’accès.


## Demander des éléments partagés par d’autres utilisateurs {#claim-items}

Vous ne pouvez commencer à travailler sur un élément partagé qu’après l’avoir revendiqué. Cela empêche plusieurs utilisateurs de travailler sur un seul élément. Effectuez les étapes suivantes pour demander un article :

1. Connectez-vous à votre instance AEM. Appuyez sur l’icône ![Boîte de réception](assets/bell.svg) et appuyez sur **[!UICONTROL Afficher tout]**.
1. Appuyez sur l’icône ![Contenu uniquement](assets/railleft.svg) pour ouvrir le sélecteur de filtre.
1. Appuyez sur la liste déroulante **[!UICONTROLSSélectionner le destinataire]** pour afficher et sélectionner les utilisateurs qui ont partagé leurs éléments de boîte de réception avec vous.
1. Sélectionnez un élément et appuyez sur **[!UICONTROL Demander]**. L’élément est ajouté à votre boîte de réception.

## Libérer les éléments réclamés {#release-items}

Vous ne pouvez travailler sur un élément partagé qu’après l’avoir revendiqué. Les autres utilisateurs ne peuvent pas afficher ni travailler sur un élément que vous avez demandé. Si vous ne pouvez pas continuer à travailler sur un élément, vous pouvez le libérer dans le pool.   Une fois l’élément publié, d’autres utilisateurs peuvent le demander et le traiter :

Pour libérer un élément, procédez comme suit :

1. Connectez-vous à votre instance AEM. Appuyez sur l’icône ![Boîte de réception](assets/bell.svg) et appuyez sur **[!UICONTROL Afficher tout]**. Une liste de vos éléments de boîte de réception s’affiche.
1. Sélectionnez l’élément à libérer et appuyez sur **[!UICONTROL AnnulerDemande]**. L’élément est de nouveau ajouté au pool. D’autres peuvent désormais Demander l’élément.

## Restrictions {#limitations}

* Le partage d’éléments avec un groupe n’est pas pris en charge.
* Le partage de tâches de projet n’est pas pris en charge.
