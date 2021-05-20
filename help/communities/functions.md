---
title: Fonctions de la communauté
seo-title: Fonctions de la communauté
description: Découvrez comment accéder à la console Fonctions de la communauté
seo-description: Découvrez comment accéder à la console Fonctions de la communauté
uuid: d3d70134-f318-4709-a673-b01a3467d980
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 91833914-b811-4355-a97d-e1a9cb7441f1
docset: aem65
role: Administrator
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2458'
ht-degree: 9%

---


# Fonctions de la communauté{#community-functions}

Le type de fonctionnalités attendu d’une expérience communautaire est bien connu. Les fonctions de communauté sont disponibles sous la forme de fonctions de communauté. Il s’agit essentiellement d’une ou de plusieurs pages préconfigurées pour mettre en oeuvre une fonctionnalité de communauté qui nécessite plus qu’un simple ajout d’un composant à une page en mode création. Il s’agit des blocs de construction utilisés pour définir la structure d’un [modèle de site communautaire](/help/communities/sites.md) à partir duquel les sites communautaires sont [créés](/help/communities/sites-console.md).

Une fois un site de communauté créé, le contenu peut être ajouté aux pages résultantes à l’aide du [mode de création standard ](/help/sites-authoring/editing-content.md). Diverses fonctions de communauté sont disponibles, comme dans la console des fonctions de communauté.

>[!NOTE]
>
>Les consoles pour la création de [sites de communauté](/help/communities/sites-console.md), [modèles de site de communauté](/help/communities/sites.md), [modèles de groupe de communauté](/help/communities/tools-groups.md) et [fonctions de communauté](/help/communities/functions.md) ne peuvent être utilisées que dans l’environnement de création.

## Console des fonctions de communauté {#community-functions-console}

Pour accéder à la console des fonctions de communauté dans l’environnement de création :

* Accédez à **[!UICONTROL Outils]** > **[!UICONTROL Communautés]** > **[!UICONTROL Fonctions de communauté]**.

![fonctions de communauté](assets/community-functions.png)

## Fonctions préconfigurées {#pre-built-functions}

Vous trouverez ci-dessous une brève description des fonctions fournies avec AEM Communities. Chaque fonction comprend une ou plusieurs pages AEM contenant des composants Communities connectés dans une fonctionnalité facilement intégrée à un [modèle de site communautaire](/help/communities/sites.md).

Un modèle de site de communauté fournit la structure d’un site de communauté, y compris les fonctions de connexion, les profils utilisateur, les notifications, la messagerie, le menu du site, la recherche, le thème et la marque.

### Paramètres de titre et d’URL {#title-and-url-settings}

**** Le titre et  **** l’URL sont des propriétés communes à toutes les fonctions de la communauté.

Lorsqu’une fonction de communauté est ajoutée à un modèle de site de communauté ou ajoutée lors de la [modification](/help/communities/sites-console.md#modifying-site-properties) de la structure d’un site de communauté, la boîte de dialogue de la fonction s’ouvre afin que le titre et l’URL puissent être configurés.

#### Détails de la fonction de configuration {#configuration-function-details}

![title-url-details](assets/title-url-details.png)

* **Titre**

   (*Obligatoire*) Texte qui apparaît dans le menu des fonctionnalités du site.

* **URL**

   (*Obligatoire*) Nom utilisé pour générer l’URI. Le nom doit être conforme aux [conventions de dénomination](/help/sites-developing/naming-conventions.md) imposées par AEM et JCR.

Par exemple, si vous utilisez le site créé à partir du tutoriel [Prise en main](/help/communities/getting-started.md) , si

* Titre = Page web
* URL = page

Ensuite, l’URL de la page est https://localhost:4503/content/sites/engage/en/page.html

et le lien de menu de la page s’affiche comme suit :

![engage-page](assets/engage-page.png)

### Fonction Flux d&#39;activités {#activity-stream-function}

La fonction de flux d’activités est une page avec un [composant Flux d’activités](/help/communities/activities.md) avec toutes les vues sélectionnées (toutes les activités, activités utilisateur et suivantes). Voir aussi [Notions fondamentales sur les flux d’activités](/help/communities/essentials-activities.md) pour les développeurs.

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

### Fonction Affectations {#assignments-function}

La fonction Affectations est la fonction de base qui définit un [site communautaire pour l’activation](/help/communities/overview.md#enablement-community). Il permet d’affecter des ressources d’activation aux membres de la communauté. Voir aussi [Notions fondamentales sur les affectations](/help/communities/essentials-assignments.md) pour les développeurs.

Cette fonction est disponible en tant que fonctionnalité du module complémentaire [d’activation](/help/communities/enablement.md). Le module complémentaire d’activation nécessite des licences supplémentaires pour être utilisé dans un environnement de production.

Lorsqu’elle est ajoutée à un modèle, la seule configuration est pour les [paramètres de titre et d’URL](#title-and-url-settings).

### Fonction Blog {#blog-function}

La fonction de blog est une page dont le [composant Blog](/help/communities/blog-feature.md) est configuré pour le balisage, les chargements de fichiers, le suivi, les membres pour la modification automatique, le vote et la modération. Voir aussi [Notions fondamentales sur les blogs](/help/communities/blog-developer-basics.md) pour les développeurs.

La boîte de dialogue suivante s’ouvre lorsqu’elle est ajoutée à un modèle :

![blog-component](assets/blog-component.png)

* [Paramètres de titre et d’URL](#title-and-url-settings)

* **Autoriser les membres privilégiés**

   Si cette option est sélectionnée, le blog permet uniquement aux membres privilégiés de créer des articles en autorisant la sélection d’un [groupe de membres privilégiés](/help/communities/users.md#privileged-members-group). Si cette option n’est pas sélectionnée, tous les membres de la communauté sont autorisés à créer. La valeur par défaut est désélectionnée.

* **Autoriser les transferts de fichiers**

   Si cette option est sélectionnée, le blog offre aux membres la possibilité de télécharger des fichiers. La valeur par défaut est sélectionnée.

* **Autoriser les réponses à thème**

   S’il n’est pas sélectionné, le blog autorise les réponses (commentaires) à un article, mais les réponses aux commentaires ne sont pas autorisées. La valeur par défaut est sélectionnée.

* **Autoriser le contenu proposé**

   Si cette option est sélectionnée, le blog est identifié comme [contenu présenté](/help/communities/featured.md). La valeur par défaut est sélectionnée.

### Fonction Calendrier {#calendar-function}

La fonction Calendrier est une page avec un [composant Calendrier](/help/communities/calendar.md) configuré pour autoriser le balisage. Voir aussi [Notions fondamentales sur le calendrier](/help/communities/calendar-basics-for-developers.md) pour les développeurs.

La boîte de dialogue suivante s’ouvre lorsqu’elle est ajoutée à un modèle :

![calendar-details](assets/calendar-details.png)

* [Paramètres de titre et d’URL](#title-and-url-settings)

* **Autoriser l’épinglage**

   Si cette option est sélectionnée, le forum permet d’épingler les réponses aux sujets au début de la liste des commentaires. La valeur par défaut est sélectionnée.

* **Autoriser les membres privilégiés**

   Si cette option est sélectionnée, le blog permet uniquement aux membres privilégiés de créer des articles en autorisant la sélection d’un [groupe de membres privilégiés](/help/communities/users.md#privileged-members-group). Si cette option n’est pas sélectionnée, tous les membres de la communauté sont autorisés à créer. La valeur par défaut est désélectionnée.

* **Autoriser les transferts de fichiers**

   Si cette option est sélectionnée, le blog offre aux membres la possibilité de télécharger des fichiers. La valeur par défaut est sélectionnée.

* **Autoriser les réponses à thème**

   S’il n’est pas sélectionné, le blog autorise les réponses (commentaires) à un article, mais les réponses aux commentaires ne sont pas autorisées. La valeur par défaut est sélectionnée.

* **Autoriser le contenu proposé**

   Si cette option est sélectionnée, son contenu est identifié comme [contenu présenté](/help/communities/featured.md). La valeur par défaut est sélectionnée.

### Fonction Catalogue {#catalog-function}

La fonction de catalogue permet aux membres de la [communauté d’activation](/help/communities/overview.md#enablement-community) de parcourir les ressources d’activation qui ne leur sont pas affectées. Voir [Balisage des ressources d’activation](/help/communities/tag-resources.md) et [Catalog Essentials](/help/communities/catalog-developer-essentials.md) pour les développeurs.

Toutes les ressources d’activation et tous les chemins d’apprentissage du site de la communauté s’affichent dans tous les catalogues si leur propriété, ` [Show in Catalog](/help/communities/resources.md)`, est définie sur true. Pour inclure explicitement des ressources et des parcours d’apprentissage, il est nécessaire d’appliquer un [pré-filtre](/help/communities/catalog-developer-essentials.md#pre-filters) au catalogue.

Lorsqu’elle est ajoutée à un modèle, la configuration permet de spécifier le ou les espaces de noms de balise utilisés pour configurer le filtre de balise présenté aux visiteurs du site :

![Fonction Catalog](assets/catalog-function.png)

* [Paramètres de titre et d’URL](#title-and-url-settings)

* **Sélectionner tous les espaces de noms**

   Les espaces de noms de balise sélectionnés définissent les balises pouvant être sélectionnées par les visiteurs pour le filtrage de la liste des ressources d’activation répertoriées dans le catalogue.
Si cette option est sélectionnée, tous les espaces de noms de balise autorisés pour le site de la communauté sont disponibles.
Si cette option est désélectionnée, il est possible de sélectionner un ou plusieurs espaces de noms autorisés pour le site de la communauté.
La valeur par défaut est sélectionnée.

### Fonction de contenu en vedette {#featured-content-function}

La fonction de contenu proposé est une page avec un [composant Contenu proposé](/help/communities/featured.md) configuré pour permettre l’ajout et la suppression de commentaires.

La possibilité d’afficher le contenu peut être autorisée ou non par composant (voir [Fonction Blog](#blog-function), [Fonction Calendrier](#calendar-function), [Fonction Forum](#forum-function), [Fonction Idéation](#ideation-function) et [Fonction QnA](#qna-function)).

Lorsqu’elle est ajoutée à un modèle, la seule configuration est pour les [paramètres de titre et d’URL](#title-and-url-settings).

### Fonction Bibliothèque de fichiers {#file-library-function}

La fonction de bibliothèque de fichiers est une page avec un [composant Bibliothèque de fichiers](/help/communities/file-library.md) configuré pour permettre l’ajout et la suppression de commentaires.

Lorsqu’elle est ajoutée à un modèle, la seule configuration est pour les [paramètres de titre et d’URL](#title-and-url-settings).

### Fonction Forum {#forum-function}

La fonction de forum est une page dont le [composant Forum](/help/communities/forum.md) est configuré pour le balisage, les chargements de fichiers, le suivi, les membres pour la modification automatique, le vote et la modération.

La boîte de dialogue suivante s’ouvre lorsqu’elle est ajoutée à un modèle :

#### Détails de la fonction de configuration {#configuration-function-details-2}

![forum-component1](assets/forum-component1.png)

* [Paramètres de titre et d’URL](#title-and-url-settings)

* **Autoriser l’épinglage**

   Si cette option est sélectionnée, le forum permet d’épingler les réponses aux sujets au début de la liste des commentaires. La valeur par défaut est sélectionnée.

* **Autoriser les membres privilégiés**

   Si cette option est sélectionnée, le forum permet uniquement aux membres privilégiés de publier des rubriques en autorisant la sélection d’un [groupe de membres privilégiés](/help/communities/users.md#privileged-members-group). Si cette option n’est pas sélectionnée, tous les membres de la communauté sont autorisés à publier du contenu. La valeur par défaut est désélectionnée.

* **Autoriser les transferts de fichiers**

   Si cette option est sélectionnée, le forum offre aux membres la possibilité de télécharger des fichiers. La valeur par défaut est sélectionnée.

* **Autoriser les réponses à thème**

   S’il n’est pas sélectionné, le forum autorise les commentaires sur un sujet, mais les réponses à ces commentaires ne sont pas autorisées. La valeur par défaut est sélectionnée.

* **Autoriser le contenu proposé**

   Si cette option est sélectionnée, le contenu du composant est identifié en tant que [contenu présenté](/help/communities/featured.md). La valeur par défaut est sélectionnée.

### Fonction Groupes {#groups-function}

>[!CAUTION]
>
>La fonction groups doit *ne pas* être la *première ou la seule fonction* dans la structure d’un site ou dans un modèle de site communautaire.
>
>Toute autre fonction, telle que la [fonction de page](#page-function), doit être incluse et répertoriée en premier.

La fonction de groupes permet aux membres de la communauté de créer des sous-communautés au sein du site de la communauté dans l’environnement de publication.

Selon les [paramètres](/help/communities/sites-console.md#groupmanagement) lorsque la fonction Groupes est incluse dans un [modèle de site de communauté](/help/communities/sites.md), les groupes peuvent être publics ou privés et un ou plusieurs modèles de groupe de communautés peuvent être configurés pour fournir un choix de modèles lorsque le groupe de communautés est réellement créé (depuis l’environnement de publication, par exemple). Un [modèle de groupe de communautés](/help/communities/tools-groups.md) spécifie les fonctionnalités de communautés qui sont créées pour les pages de groupe, telles que les forums et les calendriers.

Lorsqu’un groupe de communautés est créé, un groupe de membres est créé dynamiquement pour le nouveau groupe, auquel les membres peuvent être affectés ou rejoindre. Pour plus d’informations, voir [Gestion des utilisateurs et des groupes d’utilisateurs](/help/communities/users.md).

À partir de Communities [Feature Pack 1](/help/communities/deploy-communities.md#latestfeaturepack), les groupes de communautés sont créés dans l’environnement de création à l’aide de la [console Groupes de communautés Sites](/help/communities/groups.md) et peuvent être créés dans l’environnement de publication lorsqu’ils sont activés.

La boîte de dialogue suivante s’ouvre lorsqu’elle est ajoutée à un modèle :

![group-template-config](assets/group-template-config.png)

* [Paramètres de titre et d’URL](#title-and-url-settings)

* **Sélectionner les modèles de groupe**

   Une liste déroulante qui permet de sélectionner un ou plusieurs modèles de groupe activés à partir desquels le futur créateur d’un nouveau groupe de communauté (dans l’environnement de publication) peut choisir.

* **Autoriser les membres privilégiés**

   Si cette option est sélectionnée, le forum permet uniquement aux membres privilégiés de publier des rubriques en autorisant la sélection d’un [groupe de sécurité des membres privilégiés](/help/communities/users.md#privileged-members-group). Si cette option n’est pas sélectionnée, tous les membres de la communauté sont autorisés à publier du contenu. La valeur par défaut est désélectionnée.

* **Autoriser la publication de la création**

   Si cette option est sélectionnée, les membres autorisés de la communauté peuvent créer un groupe dans l’environnement de publication. Si cette option est désélectionnée, les nouveaux groupes (sous-communautés) ne peuvent être créés que dans l’environnement de création à partir de la console Groupes de sites de communautés .
La valeur par défaut est sélectionnée.

### Fonction de conceptualisation {#ideation-function}

La fonction d’idéation est une page avec un [composant d’idéation](/help/communities/ideation-feature.md).

Une fois ajouté à un modèle, la boîte de dialogue suivante s’ouvre, qui spécifie le titre et les noms d’URL par défaut, ainsi que les paramètres d’affichage par défaut du modèle :

![ideation-function](assets/ideation-function.png)

* [Paramètres de titre et d’URL](#title-and-url-settings)

* **Autoriser les membres privilégiés**

   Si cette option est sélectionnée, le forum permet uniquement aux membres privilégiés de publier des rubriques en autorisant la sélection d’un [groupe de sécurité des membres privilégiés](/help/communities/users.md#privileged-members-group). Si cette option n’est pas sélectionnée, tous les membres de la communauté sont autorisés à publier du contenu. La valeur par défaut est désélectionnée.

* **Autoriser les transferts de fichiers**

   Si cette option est sélectionnée, l’idée inclut la possibilité pour les membres de charger des fichiers. La valeur par défaut est sélectionnée.

* **Autoriser les réponses à thème**

   Si elle n’est pas sélectionnée, l’idée autorise les réponses (commentaires) à un sujet, mais les réponses aux commentaires ne sont pas autorisées. La valeur par défaut est sélectionnée.

* **Autoriser le contenu proposé**

   Si cette option est sélectionnée, son contenu est identifié comme [contenu présenté](/help/communities/featured.md). La valeur par défaut est sélectionnée.

### Fonction de classement {#leaderboard-function}

La fonction de classement est une page avec un [composant de classement](/help/communities/enabling-leaderboard.md).

**REMARQUE** : Le composant Tableau de classement doit être configuré plus  ** après la création d’un site communautaire à partir d’un modèle communautaire qui inclut la fonction Tableau de classement. Spécifiez les [règles](/help/communities/enabling-leaderboard.md#rules-tab) du composant Tableau de classement, qui dépendent de la configuration de [badges et de notation](/help/communities/implementing-scoring.md) pour le site de la communauté.

Une fois ajouté à un modèle, la boîte de dialogue suivante s’ouvre, qui spécifie le titre et les noms d’URL par défaut, ainsi que les paramètres d’affichage par défaut du modèle :

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

La fonction de page ajoute une page vierge au site de la communauté qu’elle est connectée aux fonctionnalités du site de la communauté : connexion, menu, notifications, messages, thèmes et marques. Le contenu est ajouté à la page à l’aide du [mode de création standard d’AEM](/help/sites-authoring/editing-content.md).

Lorsqu’elle est ajoutée à un modèle, la seule configuration est pour les [paramètres de titre et d’URL](#title-and-url-settings).

### Fonction Q&amp;R {#qna-function}

La fonction Q&amp;R est une page avec un composant [Q&amp;R](/help/communities/working-with-qna.md) configuré pour le balisage, les chargements de fichiers, le suivi, les membres pour la modification automatique, le vote et la modération.

Lorsqu’elle est ajoutée à un modèle, la configuration autorise la restriction aux membres privilégiés :

![qna-dialog](assets/qna-dialog.png)

* [Paramètres de titre et d’URL](#title-and-url-settings)

* **Autoriser l’épinglage**

   Si cette option est sélectionnée, le forum permet d’épingler les réponses aux sujets au début de la liste des commentaires. La valeur par défaut est sélectionnée.

* **Autoriser les membres privilégiés**

   Si cette option est sélectionnée, le forum Q&amp;R permet uniquement aux membres privilégiés de publier des questions en autorisant la sélection d’un [groupe de membres privilégiés](/help/communities/users.md#privileged-members-group). Si cette option n’est pas sélectionnée, tous les membres de la communauté sont autorisés à publier du contenu. La valeur par défaut est désélectionnée.

* **Autoriser les transferts de fichiers**

   Si cette option est sélectionnée, le forum Q&amp;R offre aux membres la possibilité de télécharger des fichiers. La valeur par défaut est sélectionnée.

* **Autoriser les réponses à thème**

   Si cette option n’est pas sélectionnée, le forum Q&amp;R permet d’envoyer des commentaires (réponses) à une question publiée, mais les réponses aux réponses ne sont pas autorisées. La valeur par défaut est sélectionnée.

* **Autoriser le contenu proposé**

   Si cette option est sélectionnée, son contenu est identifié comme [contenu présenté](/help/communities/featured.md). La valeur par défaut est sélectionnée.

## Créer une fonction de communauté {#create-community-function}

Pour créer une fonction de communauté, cliquez sur l’icône `Create Community Function` située en haut de la console Fonctions de communauté. Plusieurs fonctions basées sur le même plan directeur d’AEM peuvent être créées, puis personnalisées de manière unique en s’ouvrant en mode d’édition de création.

![create-community-function](assets/create-community-function.png)

### Nom de fonction de la communauté {#community-function-name}

![function-name](assets/function-name.png)

Dans le panneau Nom de la fonction de la communauté , un nom, une description et si la fonction est activée ou désactivée sont configurés :

* **Nom de fonction de la communauté**

   Nom de fonction utilisé pour l’affichage et le stockage.

* **Description des fonctions de la communauté**

   Description de la fonction pour l’affichage.

* **Désactivé/activé**

   Bouton de basculement contrôlant si la fonction est référencable.

### Plan directeur AEM {#aem-blueprint}

![aem-blueprint](assets/aem-blueprint.png)

Dans le panneau `AEM Blueprint`, il est possible de sélectionner le plan directeur qui est la mise en oeuvre sous-jacente de la fonction de communauté.

La fonction de communauté est un mini-site qui comprend une ou plusieurs pages, préconfigurées pour être incluses dans un site de communauté, y compris les fonctions de connexion, les profils utilisateur, les notifications, la messagerie, le menu du site, la recherche, le thème et la marque. Une fois la fonction créée, il est possible d’[ouvrir la fonction](#open-community-function) en mode d’édition de création et de personnaliser les paramètres de la page ou du composant.

Puisque la fonction de communauté est implémentée en tant que [Live Copy](/help/sites-administering/msm.md#live-copies) d’un [plan directeur](/help/sites-administering/msm-livecopy.md#creatingablueprint), il est possible de déployer les modifications apportées à une fonction qui affecte toutes les pages du site de communauté créées à partir du [modèle de site de communauté](/help/communities/sites.md) ou [modèle de groupe de communauté](/help/communities/tools-groups.md) qui incluait la fonction. Il est également possible de dissocier une page de son plan directeur parent pour effectuer des modifications au niveau de la page.

Voir aussi [Multi Site Manager](/help/sites-administering/msm.md).

### Miniature  {#thumbnail}

![fonction-thumbnail](assets/funtion-thumbnail.png)

Dans le panneau Miniatures, une image peut être chargée pour s’afficher dans la [console Fonctions de communauté](#community-functions-console).

## Ouvrir la fonction de communauté {#open-community-function}

![open-function](assets/open-function.png)

Sélectionnez l’icône `Open Community Function` pour passer en mode d’édition de création pour créer le contenu de la page et modifier la configuration du ou des composants de fonctionnalités.

### Configuration des composants {#configuring-components}

Une fonction de communauté est implémentée en tant que Live Copy d’un plan directeur d’AEM, dont les détails sont documentés sous [Multi Site Manager](/help/sites-administering/msm.md).

Il est possible non seulement de créer du contenu de page, mais aussi de configurer des composants.

Si vous configurez un composant sur une page d’un site de communauté créé, il peut être nécessaire d’annuler l’[héritage](/help/sites-administering/msm-livecopy.md#changing-live-copy-content) pour configurer le composant. L’héritage doit être rétabli une fois la configuration terminée.

Pour plus d’informations sur la configuration, voir [Composants Communities](/help/communities/author-communities.md) pour les auteurs.

## Modifier la fonction de communauté {#edit-community-function}

![edit-function](assets/edit-function.png)

Sélectionnez l’icône `Edit Community Function` pour modifier les propriétés de la fonction à l’aide des mêmes panneaux que [la création d’une fonction de communauté](#create-community-function), y compris l’activation ou la désactivation de la fonction.
