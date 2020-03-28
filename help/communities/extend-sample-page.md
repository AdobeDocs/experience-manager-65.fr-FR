---
title: Ajouter Commenter à un exemple de page
seo-title: Ajouter Commenter à un exemple de page
description: Ajouter des commentaires personnalisés à une page
seo-description: Ajouter des commentaires personnalisés à une page
uuid: ab258960-6de2-4943-80a7-e72904c0fd8e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a5040371-3bc2-43bc-a103-7175c4c6252d
docset: aem65
translation-type: tm+mt
source-git-commit: 0b25d956c19c5fc5d79f87b292a0c61a23e5d66a

---


# Ajouter Commenter à un exemple de page {#add-comment-to-sample-page}

Maintenant que les composants du système de commentaires personnalisé sont en place dans le répertoire de l’application (/apps), il est possible d’utiliser le composant étendu. L’instance du système de commentaires d’un site Web à affecter doit définir resourceType comme système de commentaires personnalisé et inclure toutes les bibliothèques clientes nécessaires.

## Identification des bibliothèques clientes requises {#identify-required-clientlibs}

Les bibliothèques clientes nécessaires au style et au fonctionnement des commentaires par défaut sont également nécessaires pour les commentaires étendus.

Le Guide des composants [de la communauté](/help/communities/components-guide.md) identifie les bibliothèques client requises. Accédez au Guide des composants et  le composant Commentaires, par exemple :

[https://localhost:4502/content/community-components/en/comments.html](https://localhost:4502/content/community-components/en/comments.html)

Notez les trois bibliothèques clientes requises pour que les commentaires s’affichent et fonctionnent correctement. Elles devront être incluses lorsque les commentaires étendus sont référencés et la bibliothèque [cliente des commentaires](/help/communities/extend-create-components.md#create-a-client-library-folder) étendus ( `apps.custom.comments`).

![chlimage_1-79](assets/chlimage_1-79.png)

### Ajouter des commentaires personnalisés à une page {#add-custom-comments-to-a-page}

Comme il ne peut exister qu’un seul système de commentaires par page, il est plus simple de créer un exemple de page, comme décrit dans le didacticiel [Créer un exemple de page](/help/communities/create-sample-page.md) .

Une fois le composant créé, entrez en mode Conception et rendez disponible le groupe de composants personnalisés pour permettre l’ajout du `Alt Comments` composant à la page.

Pour que le Commentaire s’affiche et fonctionne correctement, les bibliothèques clientes pour les commentaires doivent être ajoutées à la liste des clients pour la page (voir [Clientlibs for Communities Components](/help/communities/clientlibs.md)).

#### Commentaires Clientlibs sur l&#39;exemple de page {#comments-clientlibs-on-sample-page}

![Commentaires Clientlibs sur l&#39;exemple de page](assets/chlimage_1-80.png)

#### Auteur : Commentaire Alt sur l’exemple de page {#author-alt-comment-on-sample-page}

![Commentaire Alt sur l’exemple de page](assets/chlimage_1-81.png)

#### Auteur : Exemple de noeud de commentaires de page {#author-sample-page-comments-node}

Vous pouvez vérifier le resourceType dans CRXDE en affichant les propriétés du noeud de commentaires pour l’exemple de page à l’adresse `/content/sites/sample/en/jcr:content/content/primary/comments`.

![chlimage_1-82](assets/chlimage_1-82.png)

#### Publier l’exemple de page {#publish-sample-page}

Une fois le composant personnalisé ajouté à la page, il est également nécessaire de (re) [publier la page](/help/communities/sites-console.md#publishing-the-site).

#### Publier : Commentaire Alt sur l’exemple de page {#publish-alt-comment-on-sample-page}

Après avoir publié l’application personnalisée et l’exemple de page, il est possible d’entrer un commentaire. Une fois connecté, avec un utilisateur [de](/help/communities/tutorials.md#demo-users) démonstration ou un administrateur, il est possible de publier un commentaire.

Voici aaron.mcdonald@mailinator.com qui a publié un commentaire :

![chlimage_1-83](assets/chlimage_1-83.png) ![chlimage_1-84](assets/chlimage_1-84.png)

Maintenant que le composant étendu fonctionne correctement avec l’apparence par défaut, il est temps de modifier l’apparence.