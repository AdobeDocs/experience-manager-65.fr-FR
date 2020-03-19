---
title: Fonctionnalité Flux d’activités
seo-title: Fonctionnalité Flux d’activités
description: '  d’un membre de la communauté connecté'
seo-description: '  d’un membre de la communauté connecté'
uuid: decd2d6c-4d4b-4698-a92c-2b5b441458cf
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 89f3630f-c01a-4dc0-9ff5-169785f22c01
docset: aem65
translation-type: tm+mt
source-git-commit: 974d58efa560b90234d5121a11bdb445c7bf94cf

---


# Fonctionnalité Flux d’activités {#activity-streams-feature}

## Présentation {#introduction}

The activities of a signed in community member, such as posting to a forum or blog, are collected into a stream which may be filtered and displayed in various ways through configuration of the `Activity Streams` component.

La possibilité de suivi ajoute une autre vue des activités lorsque des membres de la communauté suivent des publications d’intérêt ou suivent les activités d’autres membres de la communauté.

Le  décrit :

* Ajout du composant   flux à un site AEM
* Paramètres de configuration du composant   flux

### Ajout de flux d’activités à une page {#adding-activity-streams-to-a-page}

If it is desired to add an `Activity Streams` component to a page in author mode, use the component browser to locate

* `Communities / Activity Streams`

et faites-le glisser sur la page où des flux d’activités doivent apparaître.

For necessary information, visit [Communities Components Basics](/help/communities/basics.md).

When the [required client-side libraries](/help/communities/essentials-activities.md#essentials-for-client-side) are included, this is how the `Activity Streams` component will appear :

![chlimage_1-24](assets/chlimage_1-24.png)

### Configuration du composant Flux d’activités {#configuring-activity-streams}

Select the placed `Activity Streams` component to access and select the `Configure` icon which opens the edit dialog.

![chlimage_1-25](assets/chlimage_1-25.png)

Dans l’onglet **Activités de l’utilisateur**, spécifiez les activités à afficher :

![chlimage_1-26](assets/chlimage_1-26.png)

* **Nombre max. d&#39;activités**

   Nombre de   à afficher

* **Chemin d&#39;accès aux ressources de flux**

   Laissez vide pour que le site de la communauté ou le groupe de la communauté soit défini par défaut. Le chemin d’accès aux ressources de flux identifie la source des activités. Par défaut, ce champ est vide.

* **Afficher la vue Activités de l’utilisateur**

   Si cette option est cochée, la page  du  inclura un onglet qui desen fonction de ceux générés au sein de la communauté par le membre actuel. Cette option est cochée par défaut.

* **Afficher la vue Toutes les activités**

   Si cette option est cochée, la page  du  comprend un onglet qui comprend tous les  de générés au sein de la communauté à laquelle le membre actuel a accès. Cette option est cochée par défaut.

* **Afficher la vue suivante**

   Si cette option est cochée, la page  du  inclura un onglet qui lesen fonction de ceux que suit le membre actuel. Cette option est cochée par défaut.

### suivant {#following-view}

Les composants doivent être configurés pour activer les éléments suivants. Les fonctionnalités qui permettent ce qui suit sont [blog](/help/communities/blog-feature.md), [forum](/help/communities/forum.md), [QnA](/help/communities/working-with-qna.md), [calendar, filelibrary etcommentaires.](/help/communities/calendar.md)[](/help/communities/file-library.md)[](/help/communities/comments.md)

![chlimage_1-27](assets/chlimage_1-27.png)

Le bouton **Suivre** permet de suivre les entrées sous la forme  , [notifications](/help/communities/notifications.md)ou [](/help/communities/subscriptions.md). Chaque fois que le bouton **Suivre** est sélectionné, il est possible d’activer ou de désactiver une sélection. La `Email Subscriptions` sélection n’est présente que lorsqu’elle est configurée.

Si l’une des méthodes suivantes est sélectionnée, le texte du bouton devient **Suivant**. Pour des raisons pratiques, il est possible de choisir `Unfollow All` de désactiver toutes les méthodes.

Le bouton **Suivre** s’affiche.

* lors de l’affichage de la  d’un autre membre
* sur une page de présentation principale, telle que les forums, la qualité de vie et les blogs

   * suit tous les   pour cette fonctionnalité générale

* pour une entrée spécifique, telle qu’un sujet de forum, une question QnA ou un article de blog

   * suit tous les   pour cette entrée spécifique

### Informations supplémentaires {#additional-information}

Pour plus d’informations, reportez-vous à la page [Notions fondamentales sur les flux d’activités](/help/communities/essentials-activities.md) du développeur.
