---
title: Consoles de gestion Membres et groupes
seo-title: Consoles de gestion Membres et groupes
description: Accès aux consoles de gestion Membres et groupes
seo-description: Accès aux consoles de gestion Membres et groupes
uuid: 2e93e861-a066-4189-91db-f8b784bc5aea
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ccabf301-b417-48aa-8501-8360fd9f3e36
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '963'
ht-degree: 4%

---


# Consoles de gestion Membres et groupes {#members-groups-management-consoles}

## Présentation {#overview}

Les fonctionnalités AEM Communities exigent souvent que les visiteurs du site soient enregistrés et connectés avant de participer à une communauté dans l’environnement de publication. Leur enregistrement d&#39;utilisateur n&#39;existe que dans l&#39;environnement de publication et ils sont généralement appelés *membres* pour les distinguer de *utilisateurs* enregistrés dans l&#39;environnement d&#39;auteur.

### Membres (utilisateurs) sur Publier {#members-users-on-publish}

À l&#39;aide des consoles Communautés Membres et Groupes, les membres et les groupes de membres enregistrés dans l&#39;environnement *publier* peuvent être créés et gérés à partir de l&#39;environnement *auteur*. Cela n&#39;est possible que lorsque le service de tunnel [a1/> est activé.](deploy-communities.md#tunnel-service-on-author)

### Utilisateurs sur l’auteur {#users-on-author}

Pour gérer les utilisateurs et les groupes enregistrés dans l&#39;environnement *author*, il est nécessaire d&#39;utiliser la console de sécurité de la plate-forme :

* Dans la navigation globale, sélectionnez **[!UICONTROL Outils]** > **[!UICONTROL Sécurité]** > **[!UICONTROL Utilisateurs]**.
* Dans la navigation globale, sélectionnez **[!UICONTROL Outils]** > **[!UICONTROL Sécurité]** > **[!UICONTROL Groupes]**.

>[!NOTE]
>
>Avec un exemple de contenu déployé et activé, de nombreux exemples d’utilisateurs existent dans les environnements d’auteur et de publication. Ces utilisateurs ne seront pas présents lors de l&#39;exécution avec [nosamplecontent runmode](../../help/sites-administering/production-ready.md).

## Console Membres {#members-console}

Dans l’environnement d’auteur, pour accéder à la console Membres de gestion des membres enregistrés dans l’environnement de publication :

* Dans la navigation globale, sélectionnez **[!UICONTROL Navigation]** > **[!UICONTROL Communautés]** > **[!UICONTROL Membres]**

>[!CAUTION]
>
>Il ne sera pas possible d&#39;utiliser la console Membres si le service de tunnel [tunnel](deploy-communities.md#tunnel-service-on-author) n&#39;est pas activé.

![Member-console1](assets/member-console1.png)

### Recherche {#search-features}

Sélectionnez l&#39;icône du panneau latéral sur le côté gauche de l&#39;en-tête `Members` pour ouvrir le panneau latéral de recherche.

![](assets/leftpanel-icon.png)


![Member-console2](assets/member-console2.png)

Sélectionnez l&#39;icône de recherche sur le côté gauche de l&#39;en-tête `Members` pour fermer le panneau latéral de recherche.

### Statistiques des membres {#member-statistics}

Les colonnes qui affichent `Views`, `Posts`, `Follows` et `Likes` sont mises à jour lorsque l&#39;utilisateur est membre d&#39;un ou de plusieurs sites de la communauté avec Adobe Analytics [activé](sites-console.md#analytics).

### Exporter CSV {#export-csv}

Si vous sélectionnez le lien `Export CSV`, tous les membres sont téléchargés en tant que liste de valeurs séparées par des virgules, ce qui permet de les importer dans une feuille de calcul.

Les en-têtes de colonne sont

`| Screen Name |Last Name |First Name |Status |Views |Posts |Follows |Likes |`

## Créer un membre {#create-new-member}

Sélectionnez `Create Member` pour créer un utilisateur dans l’environnement de publication.

![create-Member1](assets/create-member1.png)

### GÉNÉRAL - Détails du membre {#general-member-details}

La plupart des champs sont des champs facultatifs que le membre peut remplir ultérieurement sur son profil.

* **[!UICONTROL ID]**

(*Obligatoire*) L’identifiant autorisé est l’identifiant de connexion du membre.
Par défaut, l’ID est défini sur la valeur de l’adresse électronique requise.
*Une fois créé, l’ID ne peut plus être modifié*.

* **[!UICONTROL Adresse électronique]**

(*Obligatoire*) Adresse électronique du membre.
Le membre peut modifier son adresse électronique lors de la mise à jour de son profil.I
Si l’ID par défaut correspond à l’adresse électronique, l’ID *ne* change pas lorsque l’adresse électronique est modifiée.

* **[!UICONTROL Mot de passe]**

   (*Obligatoire*) Mot de passe de connexion.

* **[!UICONTROL Confirmer le mot de passe]**

   (*Obligatoire*) Saisissez de nouveau le mot de passe pour vérification.

* **[!UICONTROL Ajouter le membre aux sites]**

   (*Facultatif*) Effectuez une sélection parmi les sites communautaires existants afin d’ajouter le membre au groupe de membres du site communautaire.

* **[!UICONTROL Ajouter un membre aux groupes]**

   (*Facultatif*) Effectuez une sélection parmi les groupes de membres existants afin d’ajouter le membre à ce groupe.

* Sélectionnez **[!UICONTROL Enregistrer]**

### GÉNÉRAL - Paramètres du compte {#general-account-settings}

Sous Paramètres du compte, un administrateur de communauté peut :

* **[!UICONTROL État]**
   * Interdit
Un membre ne peut pas se connecter, ce qui l&#39;empêche d&#39;afficher des pages ou de participer à des activités nécessitant une connexion. Ils peuvent encore visiter anonymement un site communautaire ouvert.

   * Non interdit
Un membre a un accès complet au site communautaire.

   La valeur par défaut est `Not Banned`.

* **[!UICONTROL Limites de contribution]**

   Si cette option est cochée, la capacité du membre à publier du contenu est limitée.
Le défaut dépend de la configuration des limites de contribution.
Voir [Limites de contribution des membres](limits.md).

* **[!UICONTROL Modifier le mot de passe]**

   Lien présent lors de la modification d&#39;un membre existant. Permet à un administrateur de la communauté de réinitialiser un mot de passe pour un membre.

### GÉNÉRAL - Photo {#general-photo}

Pour fournir un avatar au membre, sélectionnez **[!UICONTROL Télécharger l’image]** et choisissez une image de type .jpg, .png, .tif ou .gif. La taille préférée pour une image est de 240 x 240 pixels à 72 ppp.

### GÉNÉRAL - Membre Ajouté des sites {#general-add-member-to-sites}

Le membre peut être ajouté à un ou plusieurs groupes de membres de sites communautaires. Commencez par saisir du texte dans la zone de texte.

### GÉNÉRAL - Membre Ajouté des groupes {#general-add-member-to-groups}

Le membre peut être ajouté à un ou plusieurs groupes de membres. Commencez par saisir du texte dans la zone de texte.

### BADGES, onglet {#badges-tab}

Le panneau `BADGES` permet d&#39;attribuer manuellement des badges et de les révoquer. Les insignes peuvent être pour des rôles assignés ainsi que pour des insignes habituellement gagnés.

Voir aussi [Scoring and Badges](implementing-scoring.md).

![create-Member2](assets/create-member2.png)

* **[!UICONTROL badges d&#39;Ajoute]**
   * Commencez la saisie pour sélectionner [badges disponibles](badges.md). Une fois un badge sélectionné, choisissez chaque site ou tous les sites sur lesquels le badge doit être affiché avec l&#39;avatar du membre.
   * Plusieurs badges et sites peuvent être choisis.
* **[!UICONTROL Suppression de badges]**
   * Sélectionnez l’icône de corbeille située en regard d’un badge pour le supprimer.

## Console Groupes {#groups-console}

La console Groupes, disponible à partir de l’environnement d’auteur, permet la création et la gestion des groupes de membres enregistrés dans l’environnement de publication. Il est particulièrement utile pour :
* [Groupes de membres privilégiés](users.md#privilegedmembersgroups)
* Affectation par groupe de [ressources d&#39;activation](resources.md)

Pour accéder à la console Groupes :
* Dans la navigation globale, sélectionnez **[!UICONTROL Navigation]** > **[!UICONTROL Communautés]** > **[!UICONTROL Groupes]**.

>[!CAUTION]
>
>Il ne sera pas possible d&#39;utiliser la console Groupes si le service de tunnel [](deploy-communities.md#tunnel-service-on-author) n&#39;est pas activé.

### Créer un groupe {#create-new-group}

Sélectionnez `Add Group` pour créer un groupe dans l’environnement de publication.

![group-console1](assets/group-console1.png)

Les champs requis pour créer un groupe de membres côté publication sont les suivants :

* **[!UICONTROL ID]**

   (*Obligatoire*) ID unique du groupe.

   *Une fois créé, l’ID ne peut plus être modifié.*

* **[!UICONTROL Name]** (Nom)

   (*Facultatif*) Nom d’affichage du groupe.

   La valeur par défaut est l’identifiant.

* **[!UICONTROL Description]**

   (*Facultatif*) Description de l’objectif et des autorisations du groupe.

* **[!UICONTROL Ajouter des membres au groupe]**

   (*Facultatif*) Sélectionnez les membres côté publication à inclure en tant que membres initiaux du groupe.

* Sélectionnez **[!UICONTROL Enregistrer]**

## Administrateurs autorisés {#authorized-administrators}

Lorsque vous travaillez avec des membres dans la console Membres Communautés, il est nécessaire de se connecter en tant qu&#39;utilisateur disposant des autorisations appropriées et de configurer correctement l&#39;agent de réplication utilisé par le service [tunnel](deploy-communities.md#tunnel-service-on-author).

Si vous n&#39;êtes pas connecté en tant que `admin`, l&#39;utilisateur connecté doit être membre du groupe d&#39;utilisateurs `administrators`.

Voir aussi [Agents de réplication sur l&#39;auteur](deploy-communities.md#replication-agents-on-author).
