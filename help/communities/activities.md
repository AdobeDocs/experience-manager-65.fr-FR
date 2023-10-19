---
title: Fonctionnalité Flux d’activités
description: Découvrez comment les activités d’un membre de la communauté connecté sont collectées dans un flux que vous pouvez filtrer et afficher via le composant Flux d’activités .
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 2b2a5de0-e7c7-4417-a217-4b929bc7dcfb
source-git-commit: b8887b4a6f757352e9dbfdf074c10e9ccd6dbd4f
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 4%

---

# Fonctionnalité Flux d’activités {#activity-streams-feature}

## Présentation {#introduction}

Les activités d’un membre de la communauté connecté, comme la publication sur un forum ou un blog, sont regroupées dans un flux qui peut être filtré et affiché de différentes manières via la configuration de la fonction `Activity Streams` composant.

La possibilité de suivre ajoute une autre vue des activités lorsque les membres de la communauté suivent des messages d’intérêt ou suivent les activités d’autres membres de la communauté.

Le document décrit :

* Ajout du composant Flux d’activités à un site AEM
* Paramètres de configuration du composant Flux d’activités

### Ajout de flux d’activités à une page {#adding-activity-streams-to-a-page}

Si vous souhaitez ajouter une `Activity Streams` sur une page en mode création, utilisez l’explorateur de composants pour accéder à

* `Communities / Activity Streams`

Faites-le glisser sur la page où les flux d’activités doivent apparaître.

Pour obtenir les informations nécessaires, consultez la section [Principes de base des composants des communautés](/help/communities/basics.md).

Lorsque la variable [bibliothèques côté client requises](/help/communities/essentials-activities.md#essentials-for-client-side) sont incluses, c’est ainsi que la variable `Activity Streams` Le composant apparaît :

![activity-streams](assets/activity-component.png)

### Configuration des flux d’activités {#configuring-activity-streams}

Sélectionnez le `Activity Streams` afin que vous puissiez accéder au `Configure` qui ouvre la boîte de dialogue de modification.

![configure](assets/configure-new.png)

Sous , **Activités utilisateurs** , définissez les activités à afficher :

![user-activities](assets/user-activities.png)

* **Nombre max. d&#39;activités**

  Le nombre d’activités à afficher

* **Chemin d&#39;accès aux ressources de flux**

  Laissez ce champ vide par défaut pour le site de la communauté ou le groupe de la communauté. Le chemin d’accès à la ressource de flux identifie la source des activités. La valeur par défaut est vide.

* **Afficher la vue Activités de l’utilisateur**

  Si cette case est cochée, la page des activités comprend un onglet qui filtre les activités en fonction de celles générées au sein de la communauté par le membre actuel. La valeur par défaut est cochée.

* **Afficher la vue Toutes les activités**

  Si cette case est cochée, la page des activités comprend un onglet qui inclut toutes les activités générées au sein de la communauté auxquelles le membre actuel a accès. La valeur par défaut est cochée.

* **Afficher la vue suivante**

  Si cette case est cochée, la page Activités comprend un onglet qui filtre les activités en fonction de celles que le membre actuel suit. La valeur par défaut est cochée.

### Vue suivante {#following-view}

Les composants doivent être configurés pour activer les éléments suivants. Les fonctionnalités qui permettent les suivantes sont [blog](/help/communities/blog-feature.md), [forum](/help/communities/forum.md), [Q&amp;R](/help/communities/working-with-qna.md), [calendar](/help/communities/calendar.md), [bibliothèque de fichiers](/help/communities/file-library.md), et [commentaires](/help/communities/comments.md).

![after-view](assets/following-activities.png)

La variable **Suivez** fournit un moyen de suivre les entrées en tant qu’activités, [notifications](/help/communities/notifications.md), ou [subscriptions](/help/communities/subscriptions.md). Chaque fois que la fonction **Suivez** est sélectionné, il est possible d’activer ou de désactiver une sélection. La variable `Email Subscriptions` n’est présente que lorsqu’elle est configurée.

Si l’une des méthodes suivantes est sélectionnée, le texte du bouton devient **Suivre**. Pour des raisons pratiques, il est possible de sélectionner `Unfollow All` pour désactiver toutes les méthodes.

La variable **Suivez** s’affiche :

* Lors de l’affichage du profil d’un autre membre.
* Sur une page principale, comme les forums, les Q&amp;R et les blogs.

   * Suit toutes les activités pour cette fonction générale.

* Pour une entrée spécifique, comme un sujet de forum, une question Q&amp;R ou un article de blog.

   * Suit toutes les activités pour cette entrée spécifique.

### Informations supplémentaires {#additional-information}

Vous trouverez plus d’informations sur la [Notions fondamentales sur les flux d’activités](/help/communities/essentials-activities.md) pour les développeurs.
