---
title: Ajout d’un commentaire à un exemple de page
seo-title: Ajout d’un commentaire à un exemple de page
description: Ajout de commentaires personnalisés à une page
seo-description: Ajout de commentaires personnalisés à une page
uuid: ab258960-6de2-4943-80a7-e72904c0fd8e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a5040371-3bc2-43bc-a103-7175c4c6252d
docset: aem65
exl-id: d4295a77-b931-4bc8-b3b4-eec42fdcfc56
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---

# Ajouter un commentaire à l’exemple de page {#add-comment-to-sample-page}

Maintenant que les composants du système de commentaires personnalisé sont en place dans le répertoire de l’application (/apps), il est possible d’utiliser le composant étendu. L’instance du système de commentaires d’un site web à affecter doit définir resourceType comme système de commentaires personnalisé et inclure toutes les bibliothèques clientes nécessaires.

## Identification des bibliothèques clientes requises {#identify-required-clientlibs}

Les bibliothèques clientes nécessaires au style et au fonctionnement des commentaires par défaut sont également nécessaires pour les commentaires étendus.

Le [Guide des composants de la communauté](/help/communities/components-guide.md) identifie les bibliothèques clientes requises. Accédez au Guide du composant et affichez le composant Commentaires , par exemple :

[https://localhost:4502/content/community-components/en/comments.html](https://localhost:4502/content/community-components/en/comments.html)

Notez les trois bibliothèques clientes requises pour que les commentaires s’affichent et fonctionnent correctement. Ils doivent être inclus là où les commentaires étendus sont référencés et la [bibliothèque cliente des commentaires étendus](/help/communities/extend-create-components.md#create-a-client-library-folder) ( `apps.custom.comments`).

![comments-component1](assets/comments-component1.png)

### Ajout de commentaires personnalisés à une page {#add-custom-comments-to-a-page}

Comme il ne peut y avoir qu’un seul système de commentaires par page, il est plus simple de créer un exemple de page, comme décrit dans le tutoriel court [Créer une page d’exemple](/help/communities/create-sample-page.md) .

Une fois créé, passez en mode de conception et rendez disponible le groupe de composants personnalisés pour permettre l’ajout du composant `Alt Comments` à la page.

Pour que le commentaire s’affiche et fonctionne correctement, les bibliothèques clientes pour les commentaires doivent être ajoutées à la liste clientlibslist pour la page (voir [Clientlibs for Communities Components](/help/communities/clientlibs.md)).

#### Comments Clientlibs sur l’exemple de page {#comments-clientlibs-on-sample-page}

![comments-clientlibs-crxde](assets/comments-clientlibs-crxde.png)

#### Auteur : Commentaire Alt sur l’exemple de page {#author-alt-comment-on-sample-page}

![alt-comment](assets/alt-comment.png)

#### Auteur : Exemple de noeud de commentaires de page {#author-sample-page-comments-node}

Vous pouvez vérifier le type de ressource dans CRXDE en affichant les propriétés du noeud de commentaires pour l’exemple de page à l’adresse `/content/sites/sample/en/jcr:content/content/primary/comments`.

![verify-comment-crxde](assets/verify-comment-crxde.png)

#### Publier l’exemple de page {#publish-sample-page}

Une fois le composant personnalisé ajouté à la page, il est également nécessaire de (re) [publier la page](/help/communities/sites-console.md#publishing-the-site).

#### Publier : Commentaire Alt sur l’exemple de page {#publish-alt-comment-on-sample-page}

Après la publication de l’application personnalisée et de l’exemple de page, il est possible de saisir un commentaire. Une fois connecté, avec un [utilisateur de démonstration](/help/communities/tutorials.md#demo-users) ou un administrateur, il est possible de publier un commentaire.

Voici aaron.mcdonald@mailinator.com en publiant un commentaire :

![publish-alt-comment](assets/publish-alt-comment.png)

![publish-alt-comment1](assets/publish-alt-comment1.png)

Maintenant qu’il apparaît que le composant étendu fonctionne correctement avec l’apparence par défaut, il est temps de modifier l’apparence.
