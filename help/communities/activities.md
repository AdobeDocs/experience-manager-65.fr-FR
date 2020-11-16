---
title: Fonctionnalité Flux d’activités
seo-title: Fonctionnalité Flux d’activités
description: Activités d'un membre de la communauté inscrit
seo-description: Activités d'un membre de la communauté inscrit
uuid: decd2d6c-4d4b-4698-a92c-2b5b441458cf
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 89f3630f-c01a-4dc0-9ff5-169785f22c01
docset: aem65
translation-type: tm+mt
source-git-commit: fcdae5363e7a0070b5d6b76227e5c65efb71bc03
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 25%

---


# Fonctionnalité Flux d’activités {#activity-streams-feature}

## Présentation {#introduction}

The activities of a signed in community member, such as posting to a forum or blog, are collected into a stream which may be filtered and displayed in various ways through configuration of the `Activity Streams` component.

La possibilité de suivi ajoute une autre vue des activités lorsque des membres de la communauté suivent des publications d’intérêt ou suivent les activités d’autres membres de la communauté.

Le document décrit :

* Ajouter le composant Flux d&#39;Activité à un site AEM
* Paramètres de configuration du composant Flux d’Activité

### Ajout de flux d’activités à une page {#adding-activity-streams-to-a-page}

If it is desired to add an `Activity Streams` component to a page in author mode, use the component browser to locate

* `Communities / Activity Streams`

et faites-le glisser sur la page où des flux d’activités doivent apparaître.

For necessary information, visit [Communities Components Basics](/help/communities/basics.md).

When the [required client-side libraries](/help/communities/essentials-activities.md#essentials-for-client-side) are included, this is how the `Activity Streams` component will appear :

![activité-flux](assets/activity-component.png)

### Configuration du composant Flux d’activités {#configuring-activity-streams}

Select the placed `Activity Streams` component to access and select the `Configure` icon which opens the edit dialog.

![configurer](assets/configure-new.png)

Dans l’onglet **Activités de l’utilisateur**, spécifiez les activités à afficher :

![activités utilisateur](assets/user-activities.png)

* **Nombre max. d&#39;activités**

   Nombre d’activités à afficher

* **Chemin d&#39;accès aux ressources de flux**

   Ne renseignez pas ce champ pour que le site de la communauté ou le groupe de la communauté soit défini par défaut. Le chemin d’accès aux ressources de flux identifie la source des activités. Par défaut, ce champ est vide.

* **Afficher la vue Activités de l’utilisateur**

   Si cette case est cochée, la page activités comprend un onglet qui filtres les activités en fonction de celles générées au sein de la communauté par le membre actuel. Cette option est cochée par défaut.

* **Afficher la vue Toutes les activités**

   Si cette case est cochée, la page activités comprend un onglet qui comprend toutes les activités générées au sein de la communauté à laquelle le membre actif a accès. Cette option est cochée par défaut.

* **Afficher la vue suivante**

   Si cette case est cochée, la page activités comprend un onglet qui filtres les activités en fonction de celles que suit le membre actuel. Cette option est cochée par défaut.

### Vue suivante {#following-view}

Les composants doivent être configurés pour activer les éléments suivants. Les fonctionnalités qui permettent ce qui suit sont [blog](/help/communities/blog-feature.md), [forum](/help/communities/forum.md), [QnA](/help/communities/working-with-qna.md), [calendar, filelibrary et les commentaires.](/help/communities/calendar.md)[](/help/communities/file-library.md)[](/help/communities/comments.md)

![vue suivante](assets/following-activities.png)

Le bouton **Suivre** permet de suivre les entrées en tant qu’activités, [notifications](/help/communities/notifications.md)ou [abonnements](/help/communities/subscriptions.md). Chaque fois que le bouton **Suivre** est sélectionné, il est possible d’activer ou de désactiver une sélection. La `Email Subscriptions` sélection n’est présente que lorsqu’elle est configurée.

Si une méthode de suivi est sélectionnée, le texte du bouton devient **Suivant**. Pour plus de commodité, il est possible de choisir `Unfollow All` de désactiver toutes les méthodes.

Le bouton **Suivre** s’affiche :

* Lors de l’affichage du profil d’un autre membre.
* Sur une page de présentation principale, telle que les forums, la qualité de vie et les blogs.

   * Suit toutes les activités de cette fonction générale.

* Pour une entrée spécifique, telle qu’un sujet de forum, une question QnA ou un article de blog.

   * Suit toutes les activités de cette entrée spécifique.

### Informations supplémentaires {#additional-information}

Pour plus d’informations, reportez-vous à la page [Notions fondamentales sur les flux d’activités](/help/communities/essentials-activities.md) du développeur.
