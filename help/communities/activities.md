---
title: Fonctionnalité Flux d’activités
seo-title: Fonctionnalité Flux d’activités
description: Activités d’un membre de la communauté connecté
seo-description: Activités d’un membre de la communauté connecté
uuid: decd2d6c-4d4b-4698-a92c-2b5b441458cf
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 89f3630f-c01a-4dc0-9ff5-169785f22c01
docset: aem65
exl-id: 2b2a5de0-e7c7-4417-a217-4b929bc7dcfb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 25%

---

# Fonctionnalité Flux d’activités {#activity-streams-feature}

## Présentation {#introduction}

Les activités d’un membre de la communauté connecté, comme la publication sur un forum ou un blog, sont collectées dans un flux qui peut être filtré et affiché de différentes manières via la configuration du composant `Activity Streams`.

La possibilité de suivi ajoute une autre vue des activités lorsque des membres de la communauté suivent des publications d’intérêt ou suivent les activités d’autres membres de la communauté.

Le document décrit :

* Ajout du composant Flux d’activités à un site AEM
* Paramètres de configuration du composant Flux d’activités

### Ajout de flux d’activités à une page {#adding-activity-streams-to-a-page}

Si vous souhaitez ajouter un composant `Activity Streams` à une page en mode création, utilisez l’explorateur de composants pour accéder à :

* `Communities / Activity Streams`

et faites-le glisser sur la page où des flux d’activités doivent apparaître.

Pour plus d’informations, voir [Principes de base des composants des communautés](/help/communities/basics.md).

Lorsque les [bibliothèques côté client requises](/help/communities/essentials-activities.md#essentials-for-client-side) sont incluses, voici comment le composant `Activity Streams` apparaîtra :

![activity-streams](assets/activity-component.png)

### Configuration du composant Flux d’activités {#configuring-activity-streams}

Sélectionnez le composant `Activity Streams` inséré pour y accéder et sélectionnez l’icône `Configure` qui ouvre la boîte de dialogue de modification.

![configure](assets/configure-new.png)

Dans l’onglet **Activités de l’utilisateur**, spécifiez les activités à afficher :

![user-activities](assets/user-activities.png)

* **Nombre max. d&#39;activités**

   Le nombre d’activités à afficher

* **Chemin d&#39;accès aux ressources de flux**

   Laissez ce champ vide par défaut pour le site de la communauté ou le groupe de la communauté. Le chemin d’accès aux ressources de flux identifie la source des activités. Par défaut, ce champ est vide.

* **Afficher la vue Activités de l’utilisateur**

   Si cette case est cochée, la page des activités comprend un onglet qui filtre les activités en fonction de celles générées au sein de la communauté par le membre actuel. Cette option est cochée par défaut.

* **Afficher la vue Toutes les activités**

   Si cette case est cochée, la page des activités comporte un onglet qui inclut toutes les activités générées au sein de la communauté auxquelles le membre actuel a accès. Cette option est cochée par défaut.

* **Afficher la vue suivante**

   Si cette case est cochée, la page Activités comprend un onglet qui filtre les activités en fonction de celles que le membre actuel suit. Cette option est cochée par défaut.

### Vue suivante {#following-view}

Les composants doivent être configurés pour activer les éléments suivants. Les fonctions qui permettent ce qui suit sont [blog](/help/communities/blog-feature.md), [forum](/help/communities/forum.md), [Qa](/help/communities/working-with-qna.md), [calendar](/help/communities/calendar.md), [filelibrary](/help/communities/file-library.md) et [commentaires](/help/communities/comments.md).

![after-view](assets/following-activities.png)

Le bouton **Suivre** permet de suivre les entrées en tant qu’activités, [notifications](/help/communities/notifications.md) ou [abonnements](/help/communities/subscriptions.md). Chaque fois que le bouton **Suivre** est sélectionné, il est possible d’activer ou de désactiver une sélection. La sélection `Email Subscriptions` n’est présente que lorsqu’elle est configurée.

Si l’une des méthodes suivantes est sélectionnée, le texte du bouton passe à **Suivant**. Pour des raisons pratiques, il est possible de sélectionner `Unfollow All` pour désactiver toutes les méthodes.

Le bouton **Suivre** s’affiche :

* Lors de l’affichage du profil d’un autre membre.
* Sur une page principale, comme les forums, les Q&amp;R et les blogs.

   * Suit toutes les activités pour cette fonction générale.

* Pour une entrée spécifique, telle qu’un sujet de forum, une question Q&amp;R ou un article de blog.

   * Suit toutes les activités pour cette entrée spécifique.

### Informations supplémentaires {#additional-information}

Pour plus d’informations, reportez-vous à la page [Notions fondamentales sur les flux d’activités](/help/communities/essentials-activities.md) du développeur.
