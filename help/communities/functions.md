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
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '2458'
ht-degree: 10%

---


# Fonctions de la communauté{#community-functions}

Le type de caractéristiques attendues d&#39;une expérience communautaire est bien connu. Les fonctions communautaires sont disponibles en tant que fonctions communautaires. Il s’agit essentiellement d’une ou de plusieurs pages pré-programmées pour mettre en oeuvre une fonctionnalité de communauté qui nécessite plus qu’un simple ajout d’un composant à une page en mode création. Il s’agit des éléments de base utilisés pour définir la structure d’un modèle [de site](/help/communities/sites.md) communautaire à partir duquel des sites communautaires sont [créés](/help/communities/sites-console.md).

Une fois un site communautaire créé, le contenu peut être ajouté aux pages résultantes en utilisant le mode [de création](/help/sites-authoring/editing-content.md)AEM standard. Diverses fonctions communautaires sont disponibles, comme le montre la console des fonctions communautaires.

>[!NOTE]
>
>Les consoles pour la création de sites [](/help/communities/sites-console.md)communautaires, de modèles de sites [](/help/communities/sites.md)communautaires, de modèles de groupes de [communautés et de fonctions de](/help/communities/tools-groups.md)[communauté ne sont utilisées que dans l’environnement d’auteur.](/help/communities/functions.md)

## Console des fonctions de la communauté {#community-functions-console}

Pour accéder à la console des fonctions de la communauté dans l’environnement d’auteur :

* Accédez à **[!UICONTROL Outils]** > **[!UICONTROL Communautés]** > Fonctions **[!UICONTROL de]** communauté.

![chlimage_1-379](assets/chlimage_1-379.png)

## Fonctions préétablies {#pre-built-functions}

Voici une brève description des fonctions fournies avec AEM Communities. Chaque fonction comprend une ou plusieurs pages AEM contenant des composants Communities connectés ensemble dans une fonction qui est facilement intégrée dans un modèle [de site](/help/communities/sites.md)communautaire.

Un modèle de site communautaire fournit la structure d’un site communautaire, y compris les fonctions de connexion, les profils utilisateur, les notifications, les messages, le menu du site, la recherche, le thème et l’identité graphique.

### Paramètres de titre et d’URL {#title-and-url-settings}

**Le titre** et l’ **URL** sont des propriétés communes à toutes les fonctions de la communauté.

Lorsqu’une fonction de communauté est ajoutée à un modèle de site de communauté ou ajoutée lors de la [modification](/help/communities/sites-console.md#modifying-site-properties) de la structure d’un site de communauté, la boîte de dialogue de la fonction s’ouvre afin que le titre et l’URL puissent être configurés.

#### Détails de la fonction de configuration {#configuration-function-details}

![chlimage_1-380](assets/chlimage_1-380.png)

* **Titre**

   (*Obligatoire*) Le texte qui apparaît dans le menu des fonctionnalités du site

* **URL**

   (*Obligatoire*) Nom utilisé pour générer l’URI. Le nom doit être conforme aux conventions [de](/help/sites-developing/naming-conventions.md) dénomination imposées par AEM et JCR.

Par exemple, si vous utilisez le site créé à partir du didacticiel [Prise en main](/help/communities/getting-started.md) , si

* Titre = Page Web
* URL = page

Ensuite, l’URL de la page est https://localhost:4503/content/sites/engage/en/page.html.

et le lien de menu de la page s’affiche comme suit :

![chlimage_1-381](assets/chlimage_1-381.png)

### Fonction Flux d&#39;activités {#activity-stream-function}

La fonction de flux d’activité est une page avec un composant [Flux d’](/help/communities/activities.md) Activité avec toutes les vues sélectionnées (toutes les activités, les activités utilisateur et les suivantes). Voir aussi [Activité Stream Essentials](/help/communities/essentials-activities.md) pour les développeurs.

Lorsqu’elle est ajoutée à un modèle, la boîte de dialogue suivante s’ouvre :

#### Détails de la fonction de configuration {#configuration-function-details-1}

![chlimage_1-382](assets/chlimage_1-382.png)

* [Paramètres de titre et d’URL](#title-and-url-settings)

* **Afficher la vue Mes activités**

   Si cette option est sélectionnée, la page Activités comprend un onglet qui filtres les activités en fonction de celles générées au sein de la communauté par le membre actif. La valeur par défaut est sélectionnée.

* **Afficher la vue Toutes les activités**

   Si cette option est sélectionnée, la page Activités comprend un onglet qui comprend toutes les activités générées au sein de la communauté à laquelle le membre actif a accès. La valeur par défaut est sélectionnée.

* **Afficher la vue Fil d’actualité**

   Si cette option est sélectionnée, les pages Activités comportent un onglet qui filtres les activités en fonction de celles que suit le membre actuel. La valeur par défaut est sélectionnée.

### Fonction Affectations {#assignments-function}

La fonction assignations est la fonction de base qui définit un site [communautaire pour l&#39;activation](/help/communities/overview.md#enablement-community). Il permet d&#39;affecter des ressources d&#39;habilitation aux membres de la communauté. Voir aussi [Affectations Essentials](/help/communities/essentials-assignments.md) pour les développeurs.

Cette fonction est disponible en tant que fonction du module complémentaire [d’](/help/communities/enablement.md)activation. Le module complémentaire d’activation nécessite une licence supplémentaire pour une utilisation dans un environnement de production.

Lorsqu’elle est ajoutée à un modèle, la seule configuration concerne les paramètres [de](#title-and-url-settings)titre et d’URL.

### Fonction Blog {#blog-function}

La fonction de blog est une page dont un composant [de](/help/communities/blog-feature.md) blog est configuré pour le balisage, les téléchargements de fichiers, les éléments suivants, les membres à modifier eux-mêmes, le vote et la modération. Voir aussi [Blog Essentials](/help/communities/blog-developer-basics.md) pour les développeurs.

Lorsqu’elle est ajoutée à un modèle, la boîte de dialogue suivante s’ouvre :

![chlimage_1-383](assets/chlimage_1-383.png)

* [Paramètres de titre et d’URL](#title-and-url-settings)

* **Autoriser les membres privilégiés**

   S&#39;il est sélectionné, le blog permet uniquement aux membres privilégiés de créer des articles en autorisant la sélection d&#39;un groupe [de membres](/help/communities/users.md#privileged-members-group)privilégiés. Si cette option n’est pas sélectionnée, tous les membres de la communauté sont autorisés à créer. La valeur par défaut est désélectionnée.

* **Autoriser les transferts de fichiers**

   Si cette option est sélectionnée, le blog permet aux membres de télécharger des fichiers. La valeur par défaut est sélectionnée.

* **Autoriser les réponses à thème**

   S&#39;il n&#39;est pas sélectionné, le blog autorise les réponses (commentaires) à un article, mais les réponses aux commentaires ne sont pas autorisées. La valeur par défaut est sélectionnée.

* **Autoriser le contenu proposé**

   Si cette option est sélectionnée, le blog est identifié comme contenu [](/help/communities/featured.md)phare. La valeur par défaut est sélectionnée.

### Fonction Calendrier {#calendar-function}

La fonction de calendrier est une page dont le composant [](/help/communities/calendar.md) Calendrier est configuré pour autoriser le balisage. Voir aussi [Calendrier Essentials](/help/communities/calendar-basics-for-developers.md) pour les développeurs.

Lorsqu’elle est ajoutée à un modèle, la boîte de dialogue suivante s’ouvre :

![chlimage_1-384](assets/chlimage_1-384.png)

* [Paramètres de titre et d’URL](#title-and-url-settings)

* **Autoriser l’épinglage**

   Si cette option est sélectionnée, le forum permet d’épingler les réponses aux sujets jusqu’au début de la liste des commentaires. La valeur par défaut est sélectionnée.

* **Autoriser les membres privilégiés**

   S&#39;il est sélectionné, le blog permet uniquement aux membres privilégiés de créer des articles en autorisant la sélection d&#39;un groupe [de membres](/help/communities/users.md#privileged-members-group)privilégiés. Si cette option n’est pas sélectionnée, tous les membres de la communauté sont autorisés à créer. La valeur par défaut est désélectionnée.

* **Autoriser les transferts de fichiers**

   Si cette option est sélectionnée, le blog permet aux membres de télécharger des fichiers. La valeur par défaut est sélectionnée.

* **Autoriser les réponses à thème**

   S&#39;il n&#39;est pas sélectionné, le blog autorise les réponses (commentaires) à un article, mais les réponses aux commentaires ne sont pas autorisées. La valeur par défaut est sélectionnée.

* **Autoriser le contenu proposé**

   Si cette option est sélectionnée, son contenu est identifié comme contenu [](/help/communities/featured.md)phare. La valeur par défaut est sélectionnée.

### Fonction Catalogue {#catalog-function}

La fonction de catalogue permet aux membres de la communauté [d’](/help/communities/overview.md#enablement-community) activation de parcourir les ressources d’activation qui ne leur sont pas affectées. Voir Ressources [d’](/help/communities/tag-resources.md) activation du balisage et [Catalogue essentiel](/help/communities/catalog-developer-essentials.md) pour les développeurs.

Toutes les ressources d’activation et tous les chemins d’apprentissage du site de la communauté s’affichent dans tous les catalogues si leur propriété, ` [Show in Catalog](/help/communities/resources.md)`est définie sur true. Pour inclure explicitement des ressources et des chemins d’apprentissage, il est nécessaire d’appliquer un [pré-filtre](/help/communities/catalog-developer-essentials.md#pre-filters) au catalogue.

Lorsqu’elle est ajoutée à un modèle, la configuration permet de spécifier les espaces de nommage de balise utilisés pour configurer le filtre de balise présenté aux visiteurs du site :

![Fonction de catalogue](assets/catalog-function.png)

* [Paramètres de titre et d’URL](#title-and-url-settings)

* **Sélectionner tous les espaces de noms**

   Les espaces de nommage de balises sélectionnés définissent les balises sélectionnables par les visiteurs pour le filtrage de la liste des ressources d’activation répertoriées dans le catalogue.
Si cette option est sélectionnée, tous les espaces de nommage de balises autorisés pour le site de la communauté sont disponibles.
Si elle est désélectionnée, il est possible de sélectionner un ou plusieurs espaces de nommage autorisés pour le site communautaire.
La valeur par défaut est sélectionnée.

### Fonction de contenu proposé {#featured-content-function}

La fonction de contenu incitatif est une page dont un composant [Contenu proposé](/help/communities/featured.md) est configuré pour permettre l&#39;ajout et la suppression de commentaires.

La fonctionnalité de contenu peut être autorisée ou refusée par composant (voir Fonction [](#blog-function)de blog, Fonction [](#calendar-function)Calendrier, Fonction [](#forum-function)Forum, Fonction [Idéation et Fonction QnA).](#ideation-function)[](#qna-function)

Lorsqu’elle est ajoutée à un modèle, la seule configuration concerne les paramètres [de](#title-and-url-settings)titre et d’URL.

### Fonction Bibliothèque de fichiers {#file-library-function}

La fonction de bibliothèque de fichiers est une page dont le composant [Bibliothèque de](/help/communities/file-library.md) fichiers est configuré pour permettre l’ajout et la suppression de commentaires.

Lorsqu’elle est ajoutée à un modèle, la seule configuration concerne les paramètres [de](#title-and-url-settings)titre et d’URL.

### Fonction Forum {#forum-function}

La fonction de forum est une page avec un composant [](/help/communities/forum.md) Forum configuré pour le balisage, les téléchargements de fichiers, les suivants, les membres à modifier eux-mêmes, le vote et la modération.

Lorsqu’elle est ajoutée à un modèle, la boîte de dialogue suivante s’ouvre :

#### Détails de la fonction de configuration {#configuration-function-details-2}

![chlimage_1-384](assets/chlimage_1-384.png)

* [Paramètres de titre et d’URL](#title-and-url-settings)

* **Autoriser l’épinglage**

   Si cette option est sélectionnée, le forum permet d’épingler les réponses aux sujets jusqu’au début de la liste des commentaires. La valeur par défaut est sélectionnée.

* **Autoriser les membres privilégiés**

   S&#39;il est sélectionné, le forum ne permet aux membres privilégiés que de publier des sujets en autorisant la sélection d&#39;un groupe [de membres](/help/communities/users.md#privileged-members-group)privilégiés. Si cette option n’est pas sélectionnée, tous les membres de la communauté sont autorisés à publier du contenu. La valeur par défaut est désélectionnée.

* **Autoriser les transferts de fichiers**

   Si cette option est sélectionnée, le forum permet aux membres de télécharger des fichiers. La valeur par défaut est sélectionnée.

* **Autoriser les réponses à thème**

   S&#39;il n&#39;est pas sélectionné, le forum permet de commenter un sujet, mais les réponses à ces commentaires ne sont pas autorisées. La valeur par défaut est sélectionnée.

* **Autoriser le contenu proposé**

   Si cette option est sélectionnée, le contenu du composant est identifié comme contenu [](/help/communities/featured.md)phare. La valeur par défaut est sélectionnée.

### Fonction Groupes {#groups-function}

>[!CAUTION]
>
>La fonction de groupes *ne doit pas* être la *première ou la seule* fonction dans la structure d&#39;un site ou dans un modèle de site communautaire.
>
>Toute autre fonction, telle que la fonction [de](#page-function)page, doit être incluse et répertoriée en premier.

La fonction de groupes permet aux membres de la communauté de créer des sous-communautés au sein du site communautaire dans l’environnement de publication.

En fonction des [paramètres](/help/communities/sites-console.md#groupmanagement) lorsque la fonction Groupes est incluse dans un modèle [de site](/help/communities/sites.md)communautaire, les groupes peuvent être publics ou privés et un ou plusieurs modèles de groupes communautaires peuvent être configurés pour fournir un choix de modèles lorsque le groupe de communauté est effectivement créé (à partir de l’environnement de publication, par exemple). Un modèle [de groupe de](/help/communities/tools-groups.md) communautés spécifie les fonctions de communautés qui sont créées pour les pages de groupe, telles que les forums et les calendriers.

Lorsqu’un groupe de communauté est créé, un groupe de membres est créé dynamiquement pour le nouveau groupe, auquel les membres peuvent être affectés ou rejoints. For more information, see [Managing Users and User Groups](/help/communities/users.md).

A compter de la version 1 [de](/help/communities/deploy-communities.md#latestfeaturepack)Feature Pack des communautés, les groupes communautaires sont créés dans l’environnement d’auteur à l’aide de la console [Groupes de sites des](/help/communities/groups.md)communautés et peuvent être créés dans l’environnement de publication lorsqu’ils sont activés.

Lorsqu’elle est ajoutée à un modèle, la boîte de dialogue suivante s’ouvre :

![chlimage_1-386](assets/chlimage_1-386.png)

* [Paramètres de titre et d’URL](#title-and-url-settings)

* **Sélectionner les modèles de groupe**

   Liste déroulante qui permet de sélectionner un ou plusieurs modèles de groupe activés parmi lesquels le futur créateur d’un nouveau groupe de communauté (dans l’environnement de publication) peut choisir.

* **Autoriser les membres privilégiés**

   S&#39;il est sélectionné, le forum ne permet aux membres privilégiés que de publier des sujets en autorisant la sélection d&#39;un groupe [de sécurité de membres](/help/communities/users.md#privileged-members-group)privilégiés. Si cette option n’est pas sélectionnée, tous les membres de la communauté sont autorisés à publier du contenu. La valeur par défaut est désélectionnée.

* **Autoriser la publication de la création**

   Si cette option est sélectionnée, les membres autorisés de la communauté peuvent créer un groupe dans l’environnement de publication. Si elle est désélectionnée, de nouveaux groupes (sous-communautés) ne peuvent être créés que dans l&#39;environnement d&#39;auteur à partir de la console Groupes de sites des communautés.
La valeur par défaut est sélectionnée.

### Fonction de conceptualisation {#ideation-function}

La fonction d’idéation est une page avec un composant [](/help/communities/ideation-feature.md)d’idéation.

Lorsqu’elle est ajoutée à un modèle, la boîte de dialogue suivante s’ouvre, qui spécifie les noms de titre et d’URL par défaut, ainsi que les paramètres d’affichage par défaut du modèle :

![chlimage_1-387](assets/chlimage_1-387.png)

* [Paramètres de titre et d’URL](#title-and-url-settings)

* **Autoriser les membres privilégiés**

   S&#39;il est sélectionné, le forum ne permet aux membres privilégiés que de publier des sujets en autorisant la sélection d&#39;un groupe [de sécurité de membres](/help/communities/users.md#privileged-members-group)privilégiés. Si cette option n’est pas sélectionnée, tous les membres de la communauté sont autorisés à publier du contenu. La valeur par défaut est désélectionnée.

* **Autoriser les transferts de fichiers**

   Si cette option est sélectionnée, les membres peuvent télécharger des fichiers. La valeur par défaut est sélectionnée.

* **Autoriser les réponses à thème**

   Si elle n’est pas sélectionnée, l’idée autorise les réponses (commentaires) à un sujet, mais les réponses aux commentaires ne sont pas autorisées. La valeur par défaut est sélectionnée.

* **Autoriser le contenu proposé**

   Si cette option est sélectionnée, son contenu est identifié comme contenu [](/help/communities/featured.md)phare. La valeur par défaut est sélectionnée.

### Fonction de classement {#leaderboard-function}

La fonction de classement est une page avec un composant [de](/help/communities/enabling-leaderboard.md)classement.

**REMARQUE**: Le composant Leaderboard a besoin d&#39;une configuration plus poussée *après* la création d&#39;un site communautaire à partir d&#39;un modèle communautaire qui inclut la fonction Leaderboard. Spécifiez les [règles](/help/communities/enabling-leaderboard.md#rules-tab)du composant Leaderboard, qui dépendent de la configuration de la [notation et des badges](/help/communities/implementing-scoring.md) pour le site de la communauté.

Lorsqu’elle est ajoutée à un modèle, la boîte de dialogue suivante s’ouvre, qui spécifie les noms de titre et d’URL par défaut, ainsi que les paramètres d’affichage par défaut du modèle :

![chlimage_1-388](assets/chlimage_1-388.png)

* [Paramètres de titre et d’URL](#title-and-url-settings)

* **Afficher le badge**

   Si cette option est sélectionnée, une colonne pour les icônes de badge est incluse dans le tableau de bord.
La valeur par défaut est désélectionnée.

* **Afficher le nom de badge**

   Si cette option est sélectionnée, une colonne correspondant au nom du badge est incluse dans le tableau de bord.
La valeur par défaut est désélectionnée.

* **Afficher l’avatar**

   Si cette option est sélectionnée, l’avatar du membre est inclus dans le tableau de bord, en regard du lien de son nom vers son profil membre.
La valeur par défaut est désélectionnée.

### Fonction Page {#page-function}

La fonction de page ajoute une page vierge au site communautaire qu’elle est intégrée aux fonctionnalités du site communautaire : connexion, menu, notifications, messagerie, thème et marque. Le contenu est ajouté à la page en utilisant le mode [de création AEM](/help/sites-authoring/editing-content.md)standard.

Lorsqu’elle est ajoutée à un modèle, la seule configuration concerne les paramètres [de](#title-and-url-settings)titre et d’URL.

### Fonction Q&amp;R {#qna-function}

La fonction QnA est une page dont le composant [](/help/communities/working-with-qna.md) QnA est configuré pour le balisage, les téléchargements de fichiers, les suivants, les membres à modifier eux-mêmes, le vote et la modération.

Lorsqu’elle est ajoutée à un modèle, la configuration autorise la restriction aux membres privilégiés :

![chlimage_1-384](assets/chlimage_1-384.png)

* [Paramètres de titre et d’URL](#title-and-url-settings)

* **Autoriser l’épinglage**

   Si cette option est sélectionnée, le forum permet d’épingler les réponses aux sujets jusqu’au début de la liste des commentaires. La valeur par défaut est sélectionnée.

* **Autoriser les membres privilégiés**

   S&#39;il est sélectionné, le forum QnA ne permet aux membres privilégiés que de poser des questions en autorisant la sélection d&#39;un groupe [de membres](/help/communities/users.md#privileged-members-group)privilégiés. Si cette option n’est pas sélectionnée, tous les membres de la communauté sont autorisés à publier du contenu. La valeur par défaut est désélectionnée.

* **Autoriser les transferts de fichiers**

   Si cette option est sélectionnée, le forum QnA permet aux membres de télécharger des fichiers. La valeur par défaut est sélectionnée.

* **Autoriser les réponses à thème**

   Si ce n&#39;est pas le cas, le forum QnA permet de faire des commentaires (réponses) à une question publiée, mais les réponses aux réponses ne sont pas autorisées. La valeur par défaut est sélectionnée.

* **Autoriser le contenu proposé**

   Si cette option est sélectionnée, son contenu est identifié comme contenu [](/help/communities/featured.md)phare. La valeur par défaut est sélectionnée.

## Créer une fonction de communauté {#create-community-function}

Pour créer une fonction de communauté, sélectionnez l’ `Create Community Function` icône située en haut de la console Fonctions de la communauté. Il est possible de créer plusieurs fonctions basées sur le même modèle AEM, puis de les personnaliser de manière unique en s’ouvrant en mode d’édition Auteur.

![chlimage_1-390](assets/chlimage_1-390.png)

### Nom de fonction de la communauté {#community-function-name}

![chlimage_1-391](assets/chlimage_1-391.png)

Dans le panneau Nom de la fonction communautaire, un nom, une description et si la fonction est activée ou désactivée sont configurés :

* **Nom de fonction de la communauté**

   Nom de fonction utilisé pour l’affichage et l’enregistrement.

* **Description des fonctions de la communauté**

   Description de la fonction pour l’affichage.

* **Désactivé/Activé**

   Bascule contrôlant si la fonction est référencable.

### Plan directeur AEM {#aem-blueprint}

![chlimage_1-392](assets/chlimage_1-392.png)

Sur le `AEM Blueprint` panel, il est possible de sélectionner le plan directeur qui est la mise en oeuvre sous-jacente de la fonction communautaire.

La fonction de communauté est un mini site qui comprend une ou plusieurs pages, pré-programmées pour l&#39;inclusion dans un site communautaire, y compris les informations de connexion, les profils d&#39;utilisateur, les notifications, les messages, le menu du site, la recherche, le thème et les fonctionnalités de marque. Une fois la fonction créée, il est possible d’ [ouvrir la fonction](#open-community-function) en mode d’édition Auteur et de personnaliser les paramètres de page ou de composant.

Comme la fonction communautaire est mise en oeuvre en tant que copie [](/help/sites-administering/msm.md#live-copies) en direct d&#39;un [plan directeur](/help/sites-administering/msm-livecopy.md#creatingablueprint), il est possible de mettre en oeuvre les modifications apportées à une fonction qui affecte toutes les pages du site de la communauté créées à partir du modèle [de site de la](/help/communities/sites.md) communauté ou du modèle de groupe de [la communauté qui incluait la fonction. ](/help/communities/tools-groups.md) Il est également possible de dissocier une page de son plan parent pour effectuer des modifications au niveau de la page.

Voir aussi Gestionnaire [](/help/sites-administering/msm.md)multisite.

### Miniature  {#thumbnail}

![chlimage_1-393](assets/chlimage_1-393.png)

Dans le panneau Miniature, une image peut être chargée pour s’afficher dans la console [Fonctions de la](#community-functions-console)communauté.

## Ouvrir la fonction de communauté {#open-community-function}

![chlimage_1-394](assets/chlimage_1-394.png)

Sélectionnez l’ `Open Community Function` icône permettant de passer en mode d’édition de l’auteur pour la création du contenu de la page et la modification de la configuration des composants de fonction.

### Configuration des composants {#configuring-components}

Une fonction communautaire est mise en oeuvre sous forme de Live Copy d&#39;un plan directeur AEM, dont les détails sont documentés dans le Gestionnaire [](/help/sites-administering/msm.md)multisite.

Il est possible non seulement de créer du contenu de page, mais aussi de configurer des composants.

Si vous configurez un composant sur une page d’un site communautaire créé, il peut s’avérer nécessaire d’annuler l’ [héritage](/help/sites-administering/msm-livecopy.md#changing-live-copy-content) pour configurer le composant. L&#39;héritage doit être rétabli une fois la configuration terminée.

Pour plus d’informations sur la configuration, consultez Composants [](/help/communities/author-communities.md) Communautés pour les auteurs.

## Modifier la fonction de communauté {#edit-community-function}

![chlimage_1-395](assets/chlimage_1-395.png)

Sélectionnez l&#39; `Edit Community Function` icône pour modifier les propriétés de la fonction à l&#39;aide des mêmes panneaux que ceux qui [créent une fonction](#create-community-function)communautaire, y compris l&#39;activation ou la désactivation de la fonction.
