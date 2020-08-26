---
title: Configuration des files d’attente partagées
seo-title: Configuration des files d’attente partagées
description: Découvrez comment utiliser les files d’attente partagées pour les workflows centrés sur Forms sur AEM Forms sur OSGi.
seo-description: Découvrez comment utiliser les files d’attente partagées pour les workflows centrés sur Forms sur AEM Forms sur OSGi.
uuid: null
topic-tags: process
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: null
docset: aem65
translation-type: tm+mt
source-git-commit: 2c8220aab9215efba2e4568961a2a6a544803920
workflow-type: tm+mt
source-wordcount: '858'
ht-degree: 4%

---


# Partage et demande l’accès aux éléments de boîte de réception d’un utilisateur {#share-and-request-access}

Une file d&#39;attente est une liste d&#39;éléments dans AEM boîte de réception d&#39;un utilisateur. Il peut s’agir d’éléments affectés à un utilisateur ou d’éléments partagés au groupe auquel un utilisateur appartient. Vous pouvez accéder à votre boîte de réception pour la vue et agir sur l&#39;élément de boîte de réception. Par exemple, partagez un élément avec un autre utilisateur.

Vous pouvez également partager vos éléments de boîte de réception avec un autre utilisateur. Une fois qu&#39;un autre utilisateur a accès à vos éléments de boîte de réception, il peut demander et prendre les mesures appropriées sur les éléments partagés. De même, vous pouvez demander l’accès aux éléments de boîte de réception à d’autres utilisateurs.

## Conditions préalables {#pre-requisites}

L&#39;utilisateur connecté doit être membre du `workflow-users` groupe. L’utilisateur peut partager des éléments ou demander l’accès aux éléments uniquement aux utilisateurs sur lesquels il dispose d’autorisations de lecture ou uniquement aux utilisateurs qui ont activé le profil public.

## Partager un ou tous les éléments de votre boîte de réception avec un autre utilisateur

aem Boîte de réception vous permet de partager un ou tous les éléments de votre boîte de réception avec un autre utilisateur.

### Partage de tous les éléments de la boîte de réception

Effectuez les étapes suivantes pour partager tous les éléments d’une boîte de réception avec un autre utilisateur :

1. Connectez-vous à l’instance AEM  Appuyez sur l’icône ![Boîte de réception](assets/bell.svg) et appuyez sur **[!UICONTROL Vue tout]**. Une liste de vos éléments de boîte de réception s’affiche.
1. Appuyez sur l’icône Sélecteur ![de](assets/viewlist.svg) Vue ou Sélecteur ![de](assets/calendar.svg) Vue située en regard du bouton **[!UICONTROL Créer]** et appuyez sur **[!UICONTROL Paramètres.]** La boîte de dialogue des paramètres s’affiche.
1. Ouvrez l’onglet **[!UICONTROL Partager]** dans la boîte de dialogue des paramètres.
1. Saisissez le nom d’un utilisateur dans la zone de texte **[!UICONTROL Octroi de l’accès à vos éléments]** de boîte de réception et appuyez sur **[!UICONTROL Octroi]**. Répétez l’étape pour ajouter d’autres utilisateurs. Tous les utilisateurs ayant accès à vos éléments apparaissent sous la section Nom d’ **utilisateur** .
1. Appuyez sur **[!UICONTROL Save]** (Enregistrer).

>[!NOTE]
>
>(Pour les éléments de flux de travaux centrés sur Forms uniquement) Activez l’option **[Autoriser les personnes désignées à partager par l’intermédiaire de l’option de partage](aem-forms-workflow-step-reference.md)** de boîte de réception de l’étape **Attribuer une tâche** dans le flux de travaux. Seuls les éléments pour lesquels cette option est activée s’affichent pour les autres utilisateurs.

### Partage d’éléments individuels

Effectuez les étapes suivantes pour partager un élément de boîte de réception avec un autre utilisateur :

1. Connectez-vous à l’instance AEM  Appuyez sur l’icône ![Boîte de réception](assets/bell.svg) et appuyez sur **[!UICONTROL Vue tout]**. Une liste de vos éléments de boîte de réception s’affiche.
1. Sélectionnez un élément et appuyez sur **[!UICONTROL Partager]**. Une boîte de dialogue s’affiche.
1. Entrez le nom d&#39;un utilisateur dans la zone de texte Ajouter les utilisateurs à partager cet élément et appuyez sur **[!UICONTROL Ajouter]**. Répétez l’étape pour ajouter d’autres utilisateurs. Tous les utilisateurs ayant accès à vos éléments apparaissent sous la section Nom d’ **[!UICONTROL utilisateur]** .
1. Appuyez sur **[!UICONTROL Save]** (Enregistrer).


>[!NOTE]
>
>(Pour les éléments de flux de travaux centrés sur Forms uniquement) Activez l’option **[Autoriser les personnes désignées à partager explicitement dans la boîte de réception](aem-forms-workflow-step-reference.md)** de l’étape **Attribuer une tâche** dans le processus. Seuls les éléments pour lesquels cette option est activée s’affichent pour les autres utilisateurs.

## Request access to Inbox items {#request-access}

Vous pouvez demander l&#39;accès aux éléments de boîte de réception d&#39;un autre utilisateur. Une fois l’accès accordé, vous pouvez vue, demander et prendre les mesures appropriées sur les éléments partagés. Effectuez les étapes suivantes pour demander l&#39;accès aux éléments de boîte de réception d&#39;un autre utilisateur :

1. Connectez-vous à l’instance AEM  Appuyez sur l’icône ![Sélecteur](assets/bell.svg) de Vue et sur **[!UICONTROL Vue Tout]**.
1. Appuyez sur l’icône Sélecteur ![de](assets/viewlist.svg) Vue ou Sélecteur ![de](assets/calendar.svg) Vue située en regard du bouton **[!UICONTROL Créer]** et appuyez sur **[!UICONTROL Paramètres.]** La boîte de dialogue des paramètres s’affiche.
1. Saisissez le nom d’un utilisateur dans les éléments **[!UICONTROL Demander l’accès aux boîtes de réception de la zone de texte utilisateur]** et appuyez sur **[!UICONTROL Demander]**. Une requête est envoyée à l’utilisateur et l’état de la requête est affiché par rapport au nom de l’utilisateur. Répétez l’étape pour ajouter d’autres utilisateurs.
1. Appuyez sur **[!UICONTROL Save]** (Enregistrer). La demande est envoyée en tant qu’élément de boîte de réception aux utilisateurs. L’utilisateur peut sélectionner l’élément et appuyer sur Approuver ou Rejeter pour accorder ou refuser l’accès.


## Demander des éléments partagés par d&#39;autres utilisateurs {#claim-items}

Vous ne pouvez début travailler sur un élément partagé qu&#39;après l&#39;avoir réclamé. Elle empêche plusieurs utilisateurs de travailler sur un seul élément. Effectuez les étapes suivantes pour demander un article :

1. Connectez-vous à l’instance AEM  Appuyez sur l’icône ![Boîte de réception](assets/bell.svg) de la boîte de réception et appuyez sur **[!UICONTROL Vue tout]**.
1. Appuyez sur l’icône ![Contenu uniquement](assets/railleft.svg) pour ouvrir le sélecteur de filtre.
1. Appuyez sur la liste **[!UICONTROL déroulante Sélectionner un destinataire]** pour accéder à la vue et sélectionnez les utilisateurs qui ont partagé leurs éléments de boîte de réception avec vous.
1. Sélectionnez un élément et appuyez sur **[!UICONTROL Demander]**. L&#39;élément est ajouté à votre boîte de réception.

## Libérer les éléments réclamés {#release-items}

Vous ne pouvez travailler sur un élément partagé qu&#39;après l&#39;avoir réclamé. Les autres utilisateurs ne peuvent pas afficher ou travailler sur un élément revendiqué. Si vous ne pouvez pas continuer à travailler sur un élément, vous pouvez le remettre dans le pool.   Une fois l’élément publié, d’autres utilisateurs peuvent demander à l’élément et le traiter :

Effectuez les étapes suivantes pour libérer un élément :

1. Connectez-vous à l’instance AEM  Appuyez sur l’icône ![Boîte de réception](assets/bell.svg) de la boîte de réception et appuyez sur **[!UICONTROL Vue tout]**. Une liste de vos éléments de boîte de réception s’affiche.
1. Sélectionnez l’élément à libérer et appuyez sur **[!UICONTROL Annuler]** la réclamation. L&#39;élément est de nouveau ajouté au pool. D’autres peuvent désormais Demander l’élément.

## Restrictions {#limitations}

* Le partage d’éléments avec un groupe n’est pas pris en charge.
* Le partage de tâches de projet n&#39;est pas pris en charge.
