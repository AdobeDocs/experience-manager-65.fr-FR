---
title: Fonctions de la communauté
seo-title: Community Functions
description: Découvrez comment accéder à la console Fonctions de la communauté
seo-description: Learn how to access the Community Functions console
uuid: d3d70134-f318-4709-a673-b01a3467d980
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 91833914-b811-4355-a97d-e1a9cb7441f1
docset: aem65
role: Admin
exl-id: 2395c895-c611-43ac-abb6-c2bc4b4a41f4
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '2220'
ht-degree: 6%

---

# Fonctions de la communauté{#community-functions}

Le type de fonctionnalités attendu d’une expérience communautaire est bien connu. Les fonctions de communauté sont disponibles sous la forme de fonctions de communauté. Il s’agit essentiellement d’une ou de plusieurs pages préconfigurées pour mettre en oeuvre une fonctionnalité de communauté qui nécessite plus qu’un simple ajout d’un composant à une page en mode création. Il s’agit des blocs de construction utilisés pour définir la structure d’une [modèle de site communautaire](/help/communities/sites.md) à partir de quels sites communautaires [created](/help/communities/sites-console.md).

Une fois qu’un site communautaire est créé, le contenu peut être ajouté aux pages résultantes à l’aide de la norme [AEM mode création](/help/sites-authoring/editing-content.md). Diverses fonctions de communauté sont disponibles, comme dans la console des fonctions de communauté.

>[!NOTE]
>
>Les consoles pour la création de [sites communautaires](/help/communities/sites-console.md), [modèles de site de communauté](/help/communities/sites.md), [modèles de groupe de communautés](/help/communities/tools-groups.md), et [fonctions de communauté](/help/communities/functions.md) sont utilisables uniquement dans l’environnement de création.

## Console des fonctions de communauté {#community-functions-console}

Pour accéder à la console des fonctions de communauté dans l’environnement de création :

* Accédez à **[!UICONTROL Outils]** > **[!UICONTROL Communautés]** > **[!UICONTROL Fonctions de communauté]**.

![fonctions de communauté](assets/community-functions.png)

## Fonctions préconfigurées {#pre-built-functions}

Vous trouverez ci-dessous une brève description des fonctions fournies avec AEM Communities. Chaque fonction comprend une ou plusieurs pages AEM contenant des composants Communities connectés ensemble dans une fonction qui est facilement intégrée à un [modèle de site communautaire](/help/communities/sites.md).

Un modèle de site de communauté fournit la structure d’un site de communauté, y compris les fonctions de connexion, les profils utilisateur, les notifications, la messagerie, le menu du site, la recherche, le thème et la marque.

### Paramètres de titre et d’URL {#title-and-url-settings}

**Titre** et **URL** sont des propriétés communes à toutes les fonctions de la communauté.

Lorsqu’une fonction de communauté est ajoutée à un modèle de site de communauté ou ajoutée lors d’une [modification](/help/communities/sites-console.md#modifying-site-properties) structure d’un site de communauté, la boîte de dialogue de la fonction s’ouvre afin que le titre et l’URL puissent être configurés.

#### Détails de la fonction de configuration {#configuration-function-details}

![title-url-details](assets/title-url-details.png)

* **Titre**

  (*Obligatoire*) Texte qui apparaît dans le menu des fonctionnalités du site.

* **URL**

  (*Obligatoire*) Nom utilisé pour générer l’URI. Le nom doit être conforme à la variable [conventions de dénomination](/help/sites-developing/naming-conventions.md) imposé par AEM et JCR.

Par exemple, en utilisant le site créé à partir de la fonction [Prise en main](/help/communities/getting-started.md) tutoriel, si

* Titre = Page web
* URL = page

Ensuite, l’URL de la page est https://localhost:4503/content/sites/engage/en/page.html

et le lien de menu de la page s’affiche comme suit :

![engage-page](assets/engage-page.png)

### Fonction Flux d&#39;activités {#activity-stream-function}

La fonction de flux d’activités est une page avec une [Composant Flux d’activités](/help/communities/activities.md) avec toutes les vues sélectionnées (toutes les activités, activités utilisateur et suivantes). Voir aussi [Notions fondamentales sur les flux d’activités](/help/communities/essentials-activities.md) pour les développeurs.

La boîte de dialogue suivante s’ouvre lorsqu’elle est ajoutée à un modèle :

#### Détails de la fonction de configuration {#configuration-function-details-1}

![function-details](assets/function-details.png)

* [Paramètres de titre et d’URL](#title-and-url-settings)

* **Afficher la vue Mes activités**

  Si cette option est sélectionnée, la page Activités comprend un onglet qui filtre les activités en fonction de celles générées dans la communauté par le membre actuel. La valeur par défaut est sélectionnée.

* **Afficher la vue Toutes les activités**

  Si cette option est sélectionnée, la page Activités comprend un onglet qui inclut toutes les activités générées au sein de la communauté auxquelles le membre actuel a accès. La valeur par défaut est sélectionnée.

* **Afficher la vue Fil d’actualité**

  Si cette option est sélectionnée, les pages Activités comprennent un onglet qui filtre les activités en fonction de celles que le membre actuel suit. La valeur par défaut est sélectionnée.

### Fonction Blog {#blog-function}

La fonction de blog est une page avec une [Composant Blog](/help/communities/blog-feature.md) configuré pour le balisage, les chargements de fichiers, les suivants, les membres à modifier, le vote et la modération. Voir aussi [Notions fondamentales sur les blogs](/help/communities/blog-developer-basics.md) pour les développeurs.

La boîte de dialogue suivante s’ouvre lorsqu’elle est ajoutée à un modèle :

![blog-component](assets/blog-component.png)

* [Paramètres de titre et d’URL](#title-and-url-settings)

* **Autoriser les membres privilégiés**

  Si cette option est sélectionnée, le blog permet uniquement aux membres privilégiés de créer des articles en autorisant la sélection d’une [groupe de membres privilégiés](/help/communities/users.md#privileged-members-group). Si cette option n’est pas sélectionnée, tous les membres de la communauté sont autorisés à créer. La valeur par défaut est désélectionnée.

* **Autoriser les chargements de fichiers**

  Si cette option est sélectionnée, le blog offre aux membres la possibilité de télécharger des fichiers. La valeur par défaut est sélectionnée.

* **Autoriser les réponses à thème**

  S’il n’est pas sélectionné, le blog autorise les réponses (commentaires) à un article, mais les réponses aux commentaires ne sont pas autorisées. La valeur par défaut est sélectionnée.

* **Autoriser le contenu proposé**

  Si cette option est sélectionnée, le blog est identifié comme [contenu proposé](/help/communities/featured.md). La valeur par défaut est sélectionnée.

### Fonction Calendrier {#calendar-function}

La fonction Calendrier est une page avec une [Composant Calendrier](/help/communities/calendar.md) configuré pour autoriser le balisage. Voir aussi [Principes de base du calendrier](/help/communities/calendar-basics-for-developers.md) pour les développeurs.

La boîte de dialogue suivante s’ouvre lorsqu’elle est ajoutée à un modèle :

![calendar-details](assets/calendar-details.png)

* [Paramètres de titre et d’URL](#title-and-url-settings)

* **Autoriser l’épinglage**

  Si cette option est sélectionnée, le forum permet d’épingler les réponses aux sujets au début de la liste des commentaires. La valeur par défaut est sélectionnée.

* **Autoriser les membres privilégiés**

  Si cette option est sélectionnée, le blog permet uniquement aux membres privilégiés de créer des articles en autorisant la sélection d’une [groupe de membres privilégiés](/help/communities/users.md#privileged-members-group). Si cette option n’est pas sélectionnée, tous les membres de la communauté sont autorisés à créer. La valeur par défaut est désélectionnée.

* **Autoriser les chargements de fichiers**

  Si cette option est sélectionnée, le blog offre aux membres la possibilité de télécharger des fichiers. La valeur par défaut est sélectionnée.

* **Autoriser les réponses à thème**

  S’il n’est pas sélectionné, le blog autorise les réponses (commentaires) à un article, mais les réponses aux commentaires ne sont pas autorisées. La valeur par défaut est sélectionnée.

* **Autoriser le contenu proposé**

  Si cette option est sélectionnée, son contenu est identifié comme [contenu proposé](/help/communities/featured.md). La valeur par défaut est sélectionnée.

### Fonction de contenu en vedette {#featured-content-function}

La fonction de contenu présenté est une page avec une [Composant Contenu proposé](/help/communities/featured.md) configuré pour autoriser l’ajout et la suppression de commentaires.

La possibilité d’afficher du contenu peut être autorisée ou non par composant (voir [Fonction de blog](#blog-function), [Fonction Calendrier](#calendar-function), [Fonction Forum](#forum-function), [Idéation, fonction](#ideation-function), et [Fonction Q&amp;R](#qna-function)).

Lors de l’ajout à un modèle, la seule configuration est celle de la variable [Paramètres de titre et d’URL](#title-and-url-settings).

### Fonction Bibliothèque de fichiers {#file-library-function}

La fonction de bibliothèque de fichiers est une page avec une [Composant Bibliothèque de fichiers](/help/communities/file-library.md) configuré pour autoriser l’ajout et la suppression de commentaires.

Lors de l’ajout à un modèle, la seule configuration est celle de la variable [Paramètres de titre et d’URL](#title-and-url-settings).

### Fonction Forum {#forum-function}

La fonction de forum est une page avec une [Composant Forum](/help/communities/forum.md) configuré pour le balisage, les chargements de fichiers, les suivants, les membres à modifier, le vote et la modération.

La boîte de dialogue suivante s’ouvre lorsqu’elle est ajoutée à un modèle :

#### Détails de la fonction de configuration {#configuration-function-details-2}

![forum-component1](assets/forum-component1.png)

* [Paramètres de titre et d’URL](#title-and-url-settings)

* **Autoriser l’épinglage**

  Si cette option est sélectionnée, le forum permet d’épingler les réponses aux sujets au début de la liste des commentaires. La valeur par défaut est sélectionnée.

* **Autoriser les membres privilégiés**

  Si cette option est sélectionnée, le forum permet uniquement aux membres privilégiés de publier des sujets en autorisant la sélection d’une [groupe de membres privilégiés](/help/communities/users.md#privileged-members-group). Si cette option n’est pas sélectionnée, tous les membres de la communauté sont autorisés à publier du contenu. La valeur par défaut est désélectionnée.

* **Autoriser les chargements de fichiers**

  Si cette option est sélectionnée, le forum offre aux membres la possibilité de télécharger des fichiers. La valeur par défaut est sélectionnée.

* **Autoriser les réponses à thème**

  S’il n’est pas sélectionné, le forum autorise les commentaires sur un sujet, mais les réponses à ces commentaires ne sont pas autorisées. La valeur par défaut est sélectionnée.

* **Autoriser le contenu proposé**

  Si cette option est sélectionnée, le contenu du composant est identifié comme [contenu proposé](/help/communities/featured.md). La valeur par défaut est sélectionnée.

### Fonction Groupes {#groups-function}

>[!CAUTION]
>
>La fonction groups doit *not* be *first ni unique* dans la structure d’un site ou dans un modèle de site communautaire.
>
>Toute autre fonction, telle que [fonction de page](#page-function), doit être inclus et répertorié en premier.

La fonction de groupes permet aux membres de la communauté de créer des sous-communautés au sein du site de la communauté dans l’environnement de publication.

Selon [paramètres](/help/communities/sites-console.md#groupmanagement) lorsque la fonction Groupes est incluse dans une [modèle de site communautaire](/help/communities/sites.md), les groupes peuvent être publics ou privés et un ou plusieurs modèles de groupes de communautés peuvent être configurés pour offrir un choix de modèles lorsque le groupe de communautés est réellement créé (à partir de l’environnement de publication, par exemple). A [modèle de groupe de communautés](/help/communities/tools-groups.md) permet d’indiquer les fonctionnalités de communauté qui sont créées pour les pages de groupe, telles que les forums et les calendriers.

Lorsqu’un groupe de communautés est créé, un groupe de membres est créé dynamiquement pour le nouveau groupe, auquel les membres peuvent être affectés ou rejoindre. Pour plus d’informations, voir [Gestion des utilisateurs et des groupes d’utilisateurs](/help/communities/users.md).

À partir des communautés [feature pack 1](/help/communities/deploy-communities.md#latestfeaturepack), les groupes de communautés sont créés dans l’environnement de création à l’aide de la variable [Console Groupes de sites Communities](/help/communities/groups.md)et peuvent être créés dans l’environnement de publication lorsqu’ils sont activés.

La boîte de dialogue suivante s’ouvre lorsqu’elle est ajoutée à un modèle :

![group-template-config](assets/group-template-config.png)

* [Paramètres de titre et d’URL](#title-and-url-settings)

* **Sélectionner les modèles de groupe**

  Une liste déroulante qui permet de sélectionner un ou plusieurs modèles de groupe activés à partir desquels le futur créateur d’un nouveau groupe de communauté (dans l’environnement de publication) peut choisir.

* **Autoriser les membres privilégiés**

  Si cette option est sélectionnée, le forum permet uniquement aux membres privilégiés de publier des sujets en autorisant la sélection d’une [groupe de sécurité des membres privilégiés](/help/communities/users.md#privileged-members-group). Si cette option n’est pas sélectionnée, tous les membres de la communauté sont autorisés à publier du contenu. La valeur par défaut est désélectionnée.

* **Autoriser la publication de la création**

  Si cette option est sélectionnée, les membres autorisés de la communauté peuvent créer un groupe dans l’environnement de publication. Si cette option est désélectionnée, les nouveaux groupes (sous-communautés) ne peuvent être créés que dans l’environnement de création à partir de la console Groupes de sites de communautés .
La valeur par défaut est sélectionnée.

### Fonction de conceptualisation {#ideation-function}

La fonction d’idéation est une page avec une [Composant Ideation](/help/communities/ideation-feature.md).

Lorsqu’elle est ajoutée à un modèle, la boîte de dialogue suivante s’ouvre, qui spécifie le titre et les noms d’URL par défaut, ainsi que les paramètres d’affichage par défaut du modèle :

![ideation-function](assets/ideation-function.png)

* [Paramètres de titre et d’URL](#title-and-url-settings)

* **Autoriser les membres privilégiés**

  Si cette option est sélectionnée, le forum permet uniquement aux membres privilégiés de publier des sujets en autorisant la sélection d’une [groupe de sécurité des membres privilégiés](/help/communities/users.md#privileged-members-group). Si cette option n’est pas sélectionnée, tous les membres de la communauté sont autorisés à publier du contenu. La valeur par défaut est désélectionnée.

* **Autoriser les chargements de fichiers**

  Si cette option est sélectionnée, l’idée inclut la possibilité pour les membres de charger des fichiers. La valeur par défaut est sélectionnée.

* **Autoriser les réponses à thème**

  Si elle n’est pas sélectionnée, l’idée autorise les réponses (commentaires) à un sujet, mais les réponses aux commentaires ne sont pas autorisées. La valeur par défaut est sélectionnée.

* **Autoriser le contenu proposé**

  Si cette option est sélectionnée, son contenu est identifié comme [contenu proposé](/help/communities/featured.md). La valeur par défaut est sélectionnée.

### Fonction de classement {#leaderboard-function}

La fonction de classement est une page comportant une seule [Composant de classement](/help/communities/enabling-leaderboard.md).

**REMARQUE**: le composant du classement nécessite une configuration supplémentaire. *after* un site communautaire est créé à partir d’un modèle communautaire qui inclut la fonction Leaderboard . Spécification de la variable [rules](/help/communities/enabling-leaderboard.md#rules-tab), qui dépendent de la configuration de [notation et badges](/help/communities/implementing-scoring.md) pour le site de la communauté.

Lorsqu’elle est ajoutée à un modèle, la boîte de dialogue suivante s’ouvre, qui spécifie le titre et les noms d’URL par défaut, ainsi que les paramètres d’affichage par défaut du modèle :

![lead-board-dialog](assets/leaderboard-dialog.png)

* [Paramètres de titre et d’URL](#title-and-url-settings)

* **Afficher le badge**

  Si cette option est sélectionnée, une colonne pour les icônes de badge est incluse dans le tableau de classement.
La valeur par défaut est désélectionnée.

* **Afficher le nom de badge**

  Si cette option est sélectionnée, une colonne pour le nom du badge est incluse dans le tableau de classement.
La valeur par défaut est désélectionnée.

* **Afficher l’avatar**

  Si cette option est sélectionnée, l’avatar du membre est inclus dans le tableau de classement, en regard du lien de son nom vers son profil de membre.
La valeur par défaut est désélectionnée.

### Fonction Page {#page-function}

La fonction de page ajoute une page vierge au site de la communauté qu’elle est connectée aux fonctionnalités du site de la communauté : connexion, menu, notifications, messages, thèmes et marques. Le contenu est ajouté à la page à l’aide de la fonction [mode de création AEM standard](/help/sites-authoring/editing-content.md).

Lors de l’ajout à un modèle, la seule configuration est celle de la variable [Paramètres de titre et d’URL](#title-and-url-settings).

### Fonction Q&amp;R {#qna-function}

La fonction Q&amp;R est une page avec une [Composant Q&amp;R](/help/communities/working-with-qna.md) configuré pour le balisage, les chargements de fichiers, les suivants, les membres à modifier, le vote et la modération.

Lorsqu’elle est ajoutée à un modèle, la configuration autorise la restriction aux membres privilégiés :

![qna-dialog](assets/qna-dialog.png)

* [Paramètres de titre et d’URL](#title-and-url-settings)

* **Autoriser l’épinglage**

  Si cette option est sélectionnée, le forum permet d’épingler les réponses aux sujets au début de la liste des commentaires. La valeur par défaut est sélectionnée.

* **Autoriser les membres privilégiés**

  Si cette option est sélectionnée, le forum Q&amp;R permet uniquement aux membres privilégiés de publier des questions en autorisant la sélection d’une [groupe de membres privilégiés](/help/communities/users.md#privileged-members-group). Si cette option n’est pas sélectionnée, tous les membres de la communauté sont autorisés à publier du contenu. La valeur par défaut est désélectionnée.

* **Autoriser les chargements de fichiers**

  Si cette option est sélectionnée, le forum Q&amp;R offre aux membres la possibilité de télécharger des fichiers. La valeur par défaut est sélectionnée.

* **Autoriser les réponses à thème**

  Si cette option n’est pas sélectionnée, le forum Q&amp;R permet d’envoyer des commentaires (réponses) à une question publiée, mais les réponses aux réponses ne sont pas autorisées. La valeur par défaut est sélectionnée.

* **Autoriser le contenu proposé**

  Si cette option est sélectionnée, son contenu est identifié comme [contenu proposé](/help/communities/featured.md). La valeur par défaut est sélectionnée.

## Créer une fonction de communauté {#create-community-function}

Pour créer une fonction de communauté, sélectionnez la fonction `Create Community Function` dans la partie supérieure de la console Fonctions de communauté. Plusieurs fonctions basées sur le même plan directeur d’AEM peuvent être créées, puis personnalisées de manière unique en s’ouvrant en mode d’édition de création.

![create-community-function](assets/create-community-function.png)

### Nom de fonction de la communauté {#community-function-name}

![function-name](assets/function-name.png)

Dans le panneau Nom de la fonction de la communauté , un nom, une description et si la fonction est activée ou désactivée sont configurés :

* **Nom de fonction de la communauté**

  Nom de fonction utilisé pour l’affichage et le stockage.

* **Description des fonctions de la communauté**

  Description de la fonction à afficher.

* **Désactivé/activé**

  Bouton de basculement contrôlant si la fonction est référencable.

### Plan directeur AEM {#aem-blueprint}

![aem-blueprint](assets/aem-blueprint.png)

Sur le `AEM Blueprint` , il est possible de sélectionner le plan directeur qui est la mise en oeuvre sous-jacente de la fonction de communauté.

La fonction de communauté est un mini-site qui comprend une ou plusieurs pages, préconfigurées pour être incluses dans un site de communauté, y compris les fonctions de connexion, les profils utilisateur, les notifications, la messagerie, le menu du site, la recherche, le thème et la marque. Une fois la fonction créée, il est possible de [ouvrir la fonction](#open-community-function) en mode d’édition de création et personnalisez la page ou les paramètres du composant.

Puisque la fonction de communauté est implémentée sous la forme d’une [Live Copy](/help/sites-administering/msm.md#live-copies) de [plan directeur](/help/sites-administering/msm-livecopy.md#creatingablueprint), il est possible de déployer les modifications apportées à une fonction qui affectent toutes les pages de site de communauté créées à partir de la fonction [modèle de site communautaire](/help/communities/sites.md) ou [modèle de groupe de communautés](/help/communities/tools-groups.md) qui incluait la fonction . Il est également possible de dissocier une page de son plan directeur parent pour effectuer des modifications au niveau de la page.

Voir aussi [Multi Site Manager](/help/sites-administering/msm.md).

### Miniature {#thumbnail}

![fonction-thumbnail](assets/funtion-thumbnail.png)

Dans le panneau Miniatures, une image peut être téléchargée pour s’afficher dans le [Console Fonctions de communauté](#community-functions-console).

## Ouvrir la fonction de communauté {#open-community-function}

![open-function](assets/open-function.png)

Sélectionnez la variable `Open Community Function` pour passer en mode d’édition de création pour créer le contenu de la page et modifier la configuration du ou des composants de fonction.

### Configuration des composants {#configuring-components}

Une fonction de communauté est implémentée en tant que Live Copy d’un plan directeur d’AEM, dont les détails sont documentés sous [Multi Site Manager](/help/sites-administering/msm.md).

Il est possible non seulement de créer du contenu de page, mais aussi de configurer des composants.

Si vous configurez un composant sur une page d’un site de communauté créé, il peut être nécessaire d’annuler [héritage](/help/sites-administering/msm-livecopy.md#changing-live-copy-content) pour configurer le composant. L’héritage doit être rétabli une fois la configuration terminée.

Pour plus d’informations sur la configuration, voir [Composants Communities](/help/communities/author-communities.md) pour les auteurs.

## Modifier la fonction de communauté {#edit-community-function}

![edit-function](assets/edit-function.png)

Sélectionnez la variable `Edit Community Function` pour modifier les propriétés de la fonction à l’aide des mêmes panneaux que [création d’une fonction communautaire](#create-community-function), notamment l’activation ou la désactivation de la fonction .
