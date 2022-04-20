---
title: Projets
seo-title: Projects
description: Les projets vous permettent de regrouper des ressources dans une seule entité dont l’environnement commun et partagé facilite la gestion de vos projets.
seo-description: Projects let you group resources into one entity whose common, shared environment makes it easy to manage your projects
uuid: 4b5b9d78-d515-46af-abe2-882da0a1c8ae
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: projects
content-type: reference
discoiquuid: dee7ac7c-ca86-48e9-8d95-7826fa926c68
docset: aem65
exl-id: 632c0608-2ab8-4a5b-8251-cd747535449b
source-git-commit: 85e993000c016240c0fbf398ec8192990e60eee6
workflow-type: tm+mt
source-wordcount: '1366'
ht-degree: 36%

---


# Projets {#projects}

Les projets permettent de regrouper des ressources dans une seule entité. Un environnement commun et partagé permet de gérer facilement vos projets. Dans AEM, les types de ressources que vous pouvez associer à un projet s’appellent des mosaïques. Les mosaïques peuvent inclure des informations de projet et d’équipe, des ressources numériques, des workflows et d’autres types d’informations, comme le précise en détail la section [Mosaïques de projet](#project-tiles).

En tant qu’utilisateur, vous pouvez :

* Création et suppression de projets
* Associer du contenu et des dossiers de ressources à un projet
* Supprimer les liens de contenu d’un projet

## Conditions d’accès {#access-requirements}

Envoie une fonction d’AEM standard sans nécessiter de configuration supplémentaire.

Toutefois, pour que les utilisateurs participant à des projets voient d’autres utilisateurs/groupes lorsqu’ils utilisent des projets, comme lors de la création de projets, de la création de tâches/workflows ou de l’affichage et de la gestion de l’équipe, ces utilisateurs doivent disposer d’un accès en lecture à `/home/users` et `/home/groups`.

Le moyen le plus simple de le faire est de donner au **projects-users** accès en lecture au groupe `/home/users` et `/home/groups`.

## Console Projets {#projects-console}

Dans AEM, la console Projets permet d’accéder à vos projets et de les gérer.

![Console Projets](assets/screen-shot_2019-03-05at125110.png)

La console Projets est similaire aux autres consoles d’AEM. Elle permet d’agir sur des projets individuels et d’ajuster l’affichage des projets.

### Activation/désactivation du mode {#modes}

Vous pouvez utiliser le sélecteur de rail pour passer d’un mode console à un autre.

![Sélecteur de rail](assets/projects-rail.png)

#### Contenu uniquement {#content-only}

Contenu uniquement est le mode par défaut lors de l’ouverture de la console. Tous vos projets s’affichent.

#### Chronologie {#timeline}

La vue chronologique vous permet de sélectionner un projet individuel et d’afficher l’activité sur celui-ci. Utilisation du sélecteur de rail ou de la touche rapide `alt+1` pour accéder à cette vue.

![Mode Chronologie](assets/project-timeline.png)

### Activation/désactivation de la vue {#views}

Vous pouvez utiliser le sélecteur d’affichage pour passer de l’affichage des projets sous forme de mosaïques de grande taille (valeur par défaut) à leur affichage sous forme de liste ou sur un calendrier.

![Vues](assets/projects-views.png)

### Filtrer votre vue {#filter}

Vous pouvez utiliser le filtre pour basculer entre tous les projets et uniquement ceux qui sont principaux.

![Filtrer](assets/projects-filter.png)

### Sélection et affichage de projets {#selecting}

Sélectionnez un projet en pointant la souris sur la mosaïque du projet et en cliquant sur la coche.

Affichez les détails d’un projet en cliquant dessus pour en parcourir les détails.

### Création de projets {#creating}

Cliquez sur **Créer** pour ajouter un nouveau projet.

## Mosaïques de projet {#project-tiles}

Les projets sont constitués de différents types d’informations que vous souhaitez gérer ensemble. Ces informations sont représentées par différentes **Mosaïques**.

Vous pouvez associer les mosaïques suivantes à votre projet.

* [Assets](#assets)
* [Collections de ressources](#asset-collections)
* [Expériences](#experiences)
* [Liens](#links)
* [Informations sur le projet](#project-info)
* [Équipe](#team)
* [Pages d’entrée](#landing-pages)
* [Courriels](#emails)
* [Workflows](#workflows)
* [Lancements](#launches)
* [Tâches](#tasks)

Cliquez sur le menu déroulant dans le coin supérieur droit d’une mosaïque pour ajouter d’autres données à la mosaïque.

Cliquez sur le bouton représentant des points de suspension en bas à droite d’une mosaïque pour ouvrir les données de la mosaïque dans la console qui lui est associée.

### Ressources {#assets}

Dans la mosaïque **Ressources**, vous pouvez regrouper tous les éléments dont vous avez besoin pour un projet particulier.

![Mosaïque Ressources](assets/project-tile-assets.png)

Vous chargez des ressources directement dans la mosaïque.

### Collections de ressources {#asset-collections}

Comme avec les ressources, vous pouvez ajouter des [collections de ressources](/help/assets/manage-collections.md) directement à votre projet. Vous définissez les collections dans Assets.

![Mosaïque Collection de ressources](assets/project-tile-asset-collection.png)

Ajoutez une collection en cliquant sur **Ajouter une collection** et en sélectionnant la collection appropriée dans la liste.

### Expériences {#experiences}

Le **Expériences** vous permet d’ajouter au projet une application mobile, un site web ou une publication.

![Mosaïque Expériences](assets/project-tile-experiences.png)

Les icônes indiquent le type d’expérience représenté.

* site web
* Application mobile

### Liens {#links}

Le **Liens** vous permet d’associer des liens externes à votre projet.

![Mosaïque Liens](assets/project-tile-links.png)

Vous pouvez donner au lien un nom facile à reconnaître et changer de miniature.

### Informations sur le projet {#project-info}

Le **Informations sur le projet** La mosaïque fournit des informations générales sur le projet, notamment une description, l’état du projet (inactif ou principal), une date d’échéance et les membres. En outre, vous pouvez ajouter une miniature de projet qui sera visible dans la page principale Projets.

![Mosaïque Informations du projet](assets/project-tile-info.png)

### Tâche de traduction {#translation-job}

Le **Tâche de traduction** est l’emplacement où vous commencez une traduction et où vous voyez l’état de vos traductions.

![Mosaïque de tâche de traduction](assets/project-tile-translation.png)

Pour configurer votre traduction, consultez le document . [Création de projets de traduction.](/help/assets/translation-projects.md)

### Équipe {#team}

Dans cette mosaïque, vous pouvez définir les membres de l’équipe de projet. En mode d’édition, vous pouvez saisir le nom des membres d’équipe et attribuer des rôles utilisateur.

![Mosaïque Équipe](assets/project-tile-team.png)

Vous pouvez ajouter et supprimer des membres de l’équipe. De plus, vous pouvez modifier le [rôle utilisateur](#userroles) attribué à chaque membre de l’équipe.

### Pages d’entrée {#landing-pages}

La mosaïque **** Pages d’entrée vous permet de demander une nouvelle page d’entrée.

![Mosaïque Landing page](assets/project-tile-landing.png)

Ce workflow est décrit dans le document .[Créez un workflow Landing Page.](/help/sites-authoring/projects-with-workflows.md#request-landing-page-workflow)

### Courriels {#emails}

La mosaïque **Courriels** permet de gérer les demandes de courrier électronique. Elle commence par la fonction **Demande de courrier électronique** workflow.

![Mosaïque Email](assets/project-tile-email.png)

Pour plus d’informations, se reporter à [Worfklow de demande de courrier électronique.](/help/sites-authoring/projects-with-workflows.md#request-email-workflow) 

### Workflows {#workflows}

Vous pouvez démarrer des workflows pour votre projet. Si des workflows sont en cours d’exécution, leur état s’affiche dans la variable **Workflows** mosaïque.

![Mosaïque Workflows](assets/project-tile-workflows.png)

Selon le projet que vous créez, différents workflows sont disponibles.

Ils sont décrits à la section [Utilisation des workflows de projet](/help/sites-authoring/projects-with-workflows.md).

### Lancements {#launches}

Le **Lancements** affiche tous les lancements qui ont été demandés avec une [Worfklow Demander le lancement .](/help/sites-authoring/projects-with-workflows.md)

![Mosaïque Lancements](assets/project-tile-launches.png)

### Tâches {#tasks}

Les tâches vous permettent de surveiller le statut de toutes les activités associées à un projet, y compris des workflows. Les tâches sont décrites en détail à la section [Utilisation des tâches](/help/sites-authoring/task-content.md).

![Mosaïque Tâches](assets/project-tile-tasks.png)

## Modèles de projet {#project-templates}

Les modèles servent de base pour démarrer votre projet. AEM fournit ces modèles de projet standard.

* **Projet de média** - Il s’agit d’un exemple de projet de référence pour les activités liées aux médias. Il comprend plusieurs rôles de projet liés aux médias et inclut également des workflows liés au contenu multimédia.
* **[Projet de séance photo du produit](/help/sites-authoring/managing-product-information.md)** - Il s’agit d’un exemple de référence pour la gestion de la photographie de produit liée au commerce électronique.
* **[Projet de traduction](/help/sites-administering/translation.md)** - Il s’agit d’un exemple de référence pour la gestion des activités liées à la traduction. Il comprend des rôles de base et des workflows pour gérer la traduction.
* **Projet simple** - Il s’agit d’un exemple de référence pour les projets qui ne correspondent pas à d’autres catégories. Il comprend trois rôles de base et quatre workflows AEM généraux.

En fonction du modèle que vous sélectionnez, vous disposez de différentes options disponibles dans le projet, telles que les rôles utilisateur et les workflows fournis.

## Rôles utilisateur dans un projet {#user-roles-in-a-project}

Les différents rôles utilisateur sont définis dans le modèle de projet et sont utilisés pour deux Principales raisons :

1. Autorisations : Les rôles utilisateur appartiennent à l’une des trois catégories répertoriées : observateur, éditeur, propriétaire. Par exemple, un photographe ou un rédacteur aura les mêmes privilèges qu’un éditeur. Les autorisations déterminent ce que les utilisateurs peuvent faire avec le contenu d’un projet.
1. Workflows : Les workflows déterminent les tâches affectées à un projet. Les tâches peuvent être associées à un rôle de projet. Par exemple, une tâche peut être affectée aux photographes afin que tous les membres de l’équipe qui ont le rôle de photographe puissent l’obtenir.

Tous les projets prennent en charge les rôles par défaut suivants pour vous permettre d’administrer les autorisations de sécurité et de contrôle.

| Rôle | Description | Autorisations | Appartenance à un groupe |
|---|---|---|---|
| Observateur | Un utilisateur disposant de ce rôle peut afficher les détails du projet, y compris son statut. | Droits en lecture seule sur un projet | Groupe `workflow-users` |
| Éditeur | Un utilisateur disposant de ce rôle peut charger et modifier le contenu d’un projet. | Accès en lecture et en écriture sur un projet, les métadonnées associées et les ressources associées<br>Privilèges pour télécharger une liste de plans, une séance photo et revoir et approuver des ressources<br>Droits en écriture sur `/etc/commerce`<br>Modifier l’autorisation d’un projet spécifique | Groupe `workflow-users` |
| Propriétaire | Un utilisateur disposant de ce rôle peut créer un projet, lancer le travail dans un projet et déplacer les ressources approuvées dans le dossier de production. Toutes les autres tâches du projet peuvent également être visualisées et exécutées par le propriétaire. | Droits en écriture sur `/etc/commerce` | `dam-users` pour pouvoir créer un projet.<br>`project-administrators` groupe pour pouvoir créer un projet et déplacer des ressources. |

Pour les projets créatifs, des rôles supplémentaires tels que des photographes sont également fournis. Vous pouvez utiliser ces rôles pour créer des rôles personnalisés liés à un projet spécifique.

### Création automatique de groupe {#auto-group-creation}

Lorsque vous créez le projet et ajoutez des utilisateurs aux différents rôles, les groupes associés au projet sont automatiquement créés pour gérer les autorisations associées.

Par exemple, un projet appelé Myproject aurait trois groupes **Myproject Owners**, **Myproject Editors**, **Myproject Observators**.

Si le projet est supprimé, ces groupes ne sont supprimés que si vous sélectionnez l’option appropriée. [lors de la suppression du projet.](/help/sites-authoring/touch-ui-managing-projects.md#deleting-a-project) Un administrateur peut également supprimer manuellement les groupes dans **Outils** > **Sécurité** > **Groupes**.

## Ressources supplémentaires {#additional-resources}

Pour plus d’informations sur l’utilisation des projets, consultez les documents supplémentaires suivants :

* [Gestion de projets](/help/sites-authoring/touch-ui-managing-projects.md)
* [Utilisation de tâches](/help/sites-authoring/task-content.md)
* [Utilisation des workflows de projet](/help/sites-authoring/projects-with-workflows.md)
* [Projet de création et intégration à PIM](/help/sites-authoring/managing-product-information.md)
