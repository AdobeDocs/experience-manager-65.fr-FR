---
title: Consoles de gestion des membres et des groupes
seo-title: Consoles de gestion des membres et des groupes
description: Accès aux consoles de gestion des membres et des groupes
seo-description: Accès aux consoles de gestion des membres et des groupes
uuid: 2e93e861-a066-4189-91db-f8b784bc5aea
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ccabf301-b417-48aa-8501-8360fd9f3e36
translation-type: tm+mt
source-git-commit: f7e5afe46100db7837647ac89aaf58cf101143b0

---


# Consoles de gestion des membres et des groupes {#members-groups-management-consoles}

## Présentation {#overview}

Les fonctionnalités des communautés AEM exigent souvent que les du site soient enregistrés et connectés avant de participer à une communauté dans le  de publication . Leur enregistrement d’utilisateur n’existe que dans le  de publication   et ils sont généralement appelés *membres* pour les distinguer des *utilisateurs* enregistrés dans le de l’auteur.

### Membres (utilisateurs) sur Publication {#members-users-on-publish}

À l&#39;aide des consoles Communautés Membres et Groupes, les membres et les groupes de membres enregistrés dans le  de *publication*   peuvent être créés et gérés à partir du de l&#39; *auteur* . Cela n’est possible que lorsque le service [de](deploy-communities.md#tunnel-service-on-author) tunnel est activé.

### Utilisateurs sur l’auteur {#users-on-author}

Pour gérer les utilisateurs et les groupes enregistrés dans le  de l’ *auteur* , il est nécessaire d’utiliser la console de sécurité de la plateforme :

* Dans la navigation globale, sélectionnez **[!UICONTROL Outils]** > **[!UICONTROL Sécurité]** > **[!UICONTROL Utilisateurs]**.
* Dans la navigation globale, sélectionnez **[!UICONTROL Outils]** > **[!UICONTROL Sécurité]** > **[!UICONTROL Groupes]**.

>[!NOTE]
>
>Avec le déploiement et l’activation d’exemples de contenu, de nombreux exemples d’utilisateurs existent à la fois dans le d’auteur et de publication  . Ces utilisateurs ne seront pas présents lors de l’exécution en mode [d’exécution](../../help/sites-administering/production-ready.md)nosamplecontent.


## Console Membres {#members-console}

Dans le de l&#39;auteur  , pour accéder à la console Membres pour la gestion des membres enregistrés dans le de publication  :

* Dans la navigation globale, sélectionnez **[!UICONTROL Navigation]** > **[!UICONTROL Communautés]** > **[!UICONTROL Membres.]**

>[!CAUTION]
>
>Il ne sera pas possible d&#39;utiliser la console Membres si le service [de](deploy-communities.md#tunnel-service-on-author) tunnel n&#39;est pas activé.


![chlimage_1-119](assets/chlimage_1-119.png)

### Recherche {#search-features}

Sélectionnez l’icône du panneau latéral sur le côté gauche de l’ `Members` en-tête pour ouvrir le panneau latéral de recherche.

![chlimage_1-120](assets/chlimage_1-120.png) ![chlimage_1-121](assets/chlimage_1-121.png)

Sélectionnez l’icône de recherche sur le côté gauche de l’ `Members` en-tête pour fermer le panneau latéral de recherche.

### Statistiques des membres {#member-statistics}

Les colonnes qui s’affichent `Views`, `Posts`et `Follows` sont mises à jour lorsque l’utilisateur est membre d’un ou de plusieurs sites de la communauté pour lesquels Adobe Analytics est `Likes` activé [](sites-console.md#analytics).

### Exporter CSV {#export-csv}

La sélection du `Export CSV` lien entraîne le téléchargement de tous les membres sous la forme d’un de valeurs séparées par des virgules, approprié pour l’importation dans une feuille de calcul.

Les en-têtes de colonne sont

`| Screen Name |Last Name |First Name |Status |Views |Posts |Follows |Likes |`

## Créer un membre {#create-new-member}

Sélectionnez `Create Member` pour créer un utilisateur dans le  de publication .

![chlimage_1-122](assets/chlimage_1-122.png)

### GÉNÉRAL - Détails du membre {#general-member-details}

La plupart des champs sont des champs facultatifs que le membre peut remplir par la suite sur son .

* **[!UICONTROL ID]**

(*Obligatoire*) L’ID autorisé est l’ID de connexion du membre.
Par défaut, l’ID est défini sur la valeur de l’adresse électronique requise.
*Une fois créé, l’ID ne peut plus être modifié*.

* **[!UICONTROL Adresse électronique]**

(*Obligatoire*) Adresse électronique du membre.
Le membre peut modifier son adresse électronique lors de la mise à jour de son.Si l&#39;ID par défaut est l&#39;adresse électronique, l&#39;ID *ne changera pas* lorsque l&#39;adresse électronique sera modifiée.

* **[!UICONTROL Mot de passe]**

   (*Obligatoire*) Mot de passe de connexion.

* **[!UICONTROL Confirmer le mot de passe]**

   (*Obligatoire*) Entrez de nouveau le mot de passe à des fins de vérification.

* **[!UICONTROL Ajouter le membre aux sites]**

   (*Facultatif*) Sélectionnez parmi les sites communautaires existants pour ajouter le membre au groupe de membres du site.

* **[!UICONTROL Ajouter un membre aux groupes]**

   (*Facultatif*) Sélectionnez un membre parmi les groupes de membres existants pour l’ajouter à ce groupe.

* Sélectionnez **[!UICONTROL Enregistrer]**

### GENERAL - Account settings {#general-account-settings}

Sous Paramètres du compte, un administrateur de communauté peut :

* **[!UICONTROL État]**
   * InterditUn membre ne peut pas se connecter, ce qui l&#39;empêche d&#39;afficher des pages ou de participer à   qui nécessitent une connexion. Ils peuvent encore visiter anonymement un site communautaire ouvert.

   * Non interditUn membre a un accès complet au site communautaire.
   La valeur par défaut est `Not Banned`.

* **[!UICONTROL Limites de contribution]**

   Si cette option est cochée, la capacité du membre à publier du contenu est limitée.
La valeur par défaut dépend de la configuration des limites de contribution.
Voir Limites [des contributions des](limits.md)membres.

* **[!UICONTROL Modifier le mot de passe]**

   Lien présent lors de la modification d’un membre existant. Permet à un administrateur de la communauté de réinitialiser le mot de passe d’un membre.

### GÉNÉRAL - Photo {#general-photo}

Pour fournir un avatar au membre, sélectionnez **[!UICONTROL Télécharger l’image]** et choisissez une image de type .jpg, .png, .tif ou .gif. La taille préférée d’une image est de 240 x 240 pixels à 72 ppp.

### GENERAL - Add Member to Sites {#general-add-member-to-sites}

Le membre peut être ajouté à un ou plusieurs groupes de membres de sites communautaires. Commencez par saisir du texte dans la zone de texte.

### GENERAL - Add Member to Groups {#general-add-member-to-groups}

Le membre peut être ajouté à un ou plusieurs groupes de membres. Commencez par saisir du texte dans la zone de texte.

### BADGES, panneau {#badges-tab}

Le `BADGES` panneau permet d’attribuer manuellement des badges et de les révoquer. Les badges peuvent être attribués à des rôles ainsi qu’à des badges généralement gagnés.

Voir aussi [Scoring and Badges](implementing-scoring.md).

![chlimage_1-123](assets/chlimage_1-123.png)

* **[!UICONTROL Ajouter badges]**
   * Commencez la saisie pour sélectionner parmi les badges [](badges.md)disponibles. Une fois un badge sélectionné, choisissez chaque site ou tous les sites sur lesquels le badge doit être affiché avec l&#39;avatar du membre.
   * Plusieurs badges et sites peuvent être choisis.
* **[!UICONTROL Suppression de badges]**
   * Sélectionnez l’icône de corbeille en regard d’un badge pour le supprimer.

## Console Groupes {#groups-console}

La console Groupes, disponible à partir de l’auteur  , permet la création et la gestion des groupes de membres enregistrés dans le de publication . Elle est particulièrement utile pour :
* [Groupes de membres privilégiés](users.md#privilegedmembersgroups)
* Affectation par groupe de ressources d&#39; [activation](resources.md)

Pour accéder à la console Groupes :
* Dans la navigation globale, sélectionnez **[!UICONTROL Navigation]** > **[!UICONTROL Communautés]** > **[!UICONTROL Groupes]**.

>[!CAUTION]
>
>Il ne sera pas possible d&#39;utiliser la console Groupes si le service [de](deploy-communities.md#tunnel-service-on-author) tunnel n&#39;est pas activé.


### Créer un groupe {#create-new-group}

Sélectionnez `Add Group` pour créer un groupe dans le  de publication .

![chlimage_1-124](assets/chlimage_1-124.png)

Les champs obligatoires pour créer un groupe de membres côté publication sont les suivants :

* **[!UICONTROL ID]**

   (*Obligatoire*) Identifiant unique du groupe.

   *Une fois créé, l’ID ne peut plus être modifié.*

* **[!UICONTROL Nom]**

   (*Facultatif*) Nom d’affichage du groupe.

   La valeur par défaut est l’ID.

* **[!UICONTROL Description]**

   (*Facultatif*) Description de l’objectif et des autorisations du groupe.

* **[!UICONTROL Ajouter des membres au groupe]**

   (*Facultatif*) Sélectionnez les membres côté publication à inclure comme membres initiaux du groupe.

* Sélectionnez **[!UICONTROL Enregistrer]**

## Administrateurs autorisés {#authorized-administrators}

Lorsque vous travaillez avec des membres dans la console Membres Communautés, il est nécessaire de se connecter en tant qu&#39;utilisateur disposant des autorisations appropriées et de configurer correctement l&#39;agent de réplication utilisé par le service [](deploy-communities.md#tunnel-service-on-author) tunnel.

S’il n’est pas connecté en tant que `admin`tel, l’utilisateur connecté doit être membre du groupe `administrators` d’utilisateurs.

Voir aussi Agents [de réplication sur l’auteur](deploy-communities.md#replication-agents-on-author).
