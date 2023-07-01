---
title: Consoles de gestion des membres et des groupes
description: Accès aux consoles de gestion des membres et des groupes
uuid: 2e93e861-a066-4189-91db-f8b784bc5aea
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ccabf301-b417-48aa-8501-8360fd9f3e36
role: Admin
exl-id: b64e24d2-8407-484c-8216-8d328ef5fa4f
source-git-commit: 4fd5e9a1bc603202ee52e85a1c09125b13cec315
workflow-type: tm+mt
source-wordcount: '942'
ht-degree: 4%

---

# Consoles de gestion des membres et des groupes {#members-groups-management-consoles}

## Présentation {#overview}

Les fonctionnalités AEM Communities nécessitent souvent que les visiteurs du site soient enregistrés et connectés avant de participer à une communauté dans l’environnement de publication. Leur enregistrement d’utilisateur n’a besoin d’exister que dans l’environnement de publication ; il est généralement appelé *members* pour les distinguer de *utilisateurs* enregistré dans l’environnement de création.

### Membres (utilisateurs) sur la publication {#members-users-on-publish}

À l’aide des consoles Membres et groupes des communautés , des membres et des groupes de membres enregistrés dans la variable *publier* peut être créé et géré à partir de l’ *author* environnement. Cela n’est possible que lorsque la variable [service tunnel](deploy-communities.md#tunnel-service-on-author) est activée.

### Utilisateurs sur l’auteur {#users-on-author}

Pour gérer les utilisateurs et les groupes enregistrés dans la variable *author* , est nécessaire pour utiliser la console de sécurité de la plateforme :

* Dans la navigation globale, sélectionnez **[!UICONTROL Outils]** > **[!UICONTROL Sécurité]** > **[!UICONTROL Utilisateurs]**.
* Dans la navigation globale, sélectionnez **[!UICONTROL Outils]** > **[!UICONTROL Sécurité]** > **[!UICONTROL Groupes]**.

>[!NOTE]
>
>Avec les exemples de contenu déployés et activés, de nombreux exemples d’utilisateurs existent dans les environnements de création et de publication. Ces utilisateurs ne seront pas présents lors de l’exécution de avec [nosamplecontent runmode](../../help/sites-administering/production-ready.md).

## Console Membres {#members-console}

Dans l’environnement de création, pour accéder à la console Membres afin de gérer les membres enregistrés dans l’environnement de publication :

* Dans la navigation globale, sélectionnez **[!UICONTROL Navigation]** > **[!UICONTROL Communautés]** > **[!UICONTROL Membres]**

>[!CAUTION]
>
>Il ne sera pas possible d’utiliser la console Membres si la variable [service tunnel](deploy-communities.md#tunnel-service-on-author) n’est pas activé.

![member-console1](assets/member-console1.png)

### Recherche {#search-features}

Sélectionnez l’icône du panneau latéral sur le côté gauche de la `Members` pour ouvrir le panneau latéral de recherche.

![Icône du panneau latéral de recherche.](assets/leftpanel-icon.png)


![member-console2](assets/member-console2.png)

Sélectionnez l’icône de recherche sur le côté gauche de la `Members` pour fermer le panneau latéral de recherche.

### Statistiques des membres {#member-statistics}

Les colonnes qui s&#39;affichent `Views`, `Posts`, `Follows` et `Likes` sont mis à jour lorsque l’utilisateur est membre d’un ou de plusieurs sites de la communauté avec Adobe Analytics ; [enabled](sites-console.md#analytics).

### Exporter CSV {#export-csv}

En sélectionnant le `Export CSV` entraîne le téléchargement de tous les membres sous la forme d’une liste de valeurs séparées par des virgules, adaptées à l’importation dans une feuille de calcul.

Les en-têtes de colonne sont :

`| Screen Name |Last Name |First Name |Status |Views |Posts |Follows |Likes |`

## Créer un membre {#create-new-member}

Sélectionner `Create Member` pour créer un utilisateur dans l’environnement de publication.

![create-member1](assets/create-member1.png)

### GÉNÉRAL - Détails du membre {#general-member-details}

La plupart des champs sont des champs facultatifs que le membre peut remplir ultérieurement sur son profil.

* **[!UICONTROL ID]**

(*Obligatoire*) L’ID autorisable est l’ID de connexion du membre.
Par défaut, l’ID est défini sur la valeur de l’adresse électronique requise.
*Une fois créé, l&#39;identifiant ne peut pas être modifié.*.

* **[!UICONTROL Adresse électronique]**

(*Obligatoire*) Adresse électronique du membre.
Le membre peut modifier son adresse email lors de la mise à jour de son profil. Si l&#39;identifiant est l&#39;adresse email par défaut, l&#39;identifiant sera *not* change lorsque l’adresse électronique est modifiée.

* **[!UICONTROL Password]**

  (*Obligatoire*) Mot de passe de connexion.

* **[!UICONTROL Confirmer le mot de passe]**

  (*Obligatoire*) Saisissez à nouveau le mot de passe à vérifier.

* **[!UICONTROL Ajouter le membre aux sites]**

  (*Facultatif*) Sélectionnez sur les sites de la communauté existants pour ajouter le membre au groupe de membres du site de la communauté.

* **[!UICONTROL Ajouter un membre aux groupes]**

  (*Facultatif*) Effectuez une sélection parmi les groupes de membres existants pour ajouter le membre à ce groupe.

* Sélectionnez **[!UICONTROL Enregistrer]**.

### GÉNÉRAL - Paramètres du compte {#general-account-settings}

Sous Paramètres du compte , un administrateur de communauté peut :

* **[!UICONTROL Statut]**
   * Interdit Un membre ne parvient pas à se connecter, ce qui l’empêche d’afficher des pages ou de participer à des activités nécessitant une connexion. Ils peuvent encore visiter anonymement un site communautaire ouvert.

   * Non interdit Un membre a un accès complet au site de la communauté.

  La valeur par défaut est `Not Banned`.

* **[!UICONTROL Limites de contribution]**

  Si cette case est cochée, la capacité du membre à publier du contenu est limitée.
La valeur par défaut dépend de la configuration des limites de contribution.
Voir [Limites des contributions des membres](limits.md).

* **[!UICONTROL Modifier le mot de passe]**

  Lien présent lors de la modification d’un membre existant. Permet à un administrateur de la communauté de réinitialiser un mot de passe pour un membre.

### GÉNÉRAL - Photo {#general-photo}

Pour fournir un avatar au membre, commencez par sélectionner **[!UICONTROL Télécharger l’image]** et choisissez une image de type .jpg, .png, .tif ou .gif. La taille préférée d’une image est de 240 x 240 pixels à 72 ppp.

### GÉNÉRAL - Ajouter un membre à Sites {#general-add-member-to-sites}

Le membre peut être ajouté à un ou plusieurs groupes de membres de sites de communauté. Saisissez tout d’abord du texte dans la zone de texte.

### GÉNÉRAL - Ajouter un membre aux groupes {#general-add-member-to-groups}

Le membre peut être ajouté à un ou plusieurs groupes de membres. Saisissez tout d’abord du texte dans la zone de texte.

### Onglet BADGES {#badges-tab}

Le `BADGES` panneau permet d’attribuer manuellement des badges et de les révoquer. Les badges peuvent être pour les rôles attribués ainsi que pour les badges généralement gagnés.

Voir aussi [Notation et badges](implementing-scoring.md).

![create-member2](assets/create-member2.png)

* **[!UICONTROL Ajouter des badges]**
   * Commencer à saisir pour effectuer une sélection dans [badges disponibles](badges.md). Une fois qu’un badge est sélectionné, sélectionnez chaque site, ou tous les sites, sur lesquels le badge doit s’afficher avec l’avatar du membre.
   * Plusieurs badges et sites peuvent être choisis.
* **[!UICONTROL Suppression des badges]**
   * Sélectionnez l’icône de corbeille en regard d’un badge pour le supprimer.

## Console Groupes {#groups-console}

La console Groupes , disponible dans l’environnement de création, permet la création et la gestion des groupes de membres enregistrés dans l’environnement de publication. Elle est particulièrement utile pour [Groupes de membres privilégiés](users.md#privilegedmembersgroups).

Pour accéder à la console Groupes , procédez comme suit :
* Dans la navigation globale, sélectionnez **[!UICONTROL Navigation]** > **[!UICONTROL Communautés]** > **[!UICONTROL Groupes]**.

>[!CAUTION]
>
>Il ne sera pas possible d’utiliser la console Groupes si la variable [service tunnel](deploy-communities.md#tunnel-service-on-author) n’est pas activé.

### Créer un groupe {#create-new-group}

Sélectionner `Add Group` pour créer un groupe dans l’environnement de publication.

![group-console1](assets/group-console1.png)

Les champs requis pour créer un groupe de membres côté publication sont les suivants :

* **[!UICONTROL ID]**

  (*Obligatoire*) Identifiant unique du groupe.

  *Une fois créé, l&#39;identifiant ne peut plus être modifié.*

* **[!UICONTROL Nom]**

  (*Facultatif*) Nom d’affichage du groupe.

  La valeur par défaut est l’ID.

* **[!UICONTROL Description]**

  (*Facultatif*) Description de l’objectif et des autorisations du groupe.

* **[!UICONTROL Ajouter des membres au groupe]**

  (*Facultatif*) Sélectionnez les membres côté publication à inclure en tant que membres initiaux du groupe.

* Sélectionnez **[!UICONTROL Enregistrer]**.

## Administrateurs autorisés {#authorized-administrators}

Lorsque vous travaillez avec des membres dans la console des membres de Communities, il est nécessaire de se connecter en tant qu’utilisateur avec les autorisations appropriées, ainsi que pour l’agent de réplication utilisé par la fonction [service tunnel](deploy-communities.md#tunnel-service-on-author) pour être correctement configurés.

Si vous n’êtes pas connecté en tant que `admin`, l’utilisateur connecté doit être membre du `administrators` groupe d’utilisateurs.

Voir aussi [Agents de réplication sur l’auteur](deploy-communities.md#replication-agents-on-author).
