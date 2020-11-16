---
title: Ajouter un commentaire sur un exemple de page
seo-title: Ajouter un commentaire sur un exemple de page
description: Ajouter des commentaires personnalisés sur une page
seo-description: Ajouter des commentaires personnalisés sur une page
uuid: ab258960-6de2-4943-80a7-e72904c0fd8e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a5040371-3bc2-43bc-a103-7175c4c6252d
docset: aem65
translation-type: tm+mt
source-git-commit: 230c700d87d82d248b7d0bbc45c69c5c2b0e3ff8
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 1%

---


# Ajouter un commentaire sur un exemple de page  {#add-comment-to-sample-page}

Maintenant que les composants du système de commentaires personnalisés sont en place dans le répertoire de l’application (/apps), il est possible d’utiliser le composant étendu. L’instance du système de commentaires d’un site Web à affecter doit définir resourceType comme système de commentaires personnalisé et inclure toutes les bibliothèques clientes nécessaires.

## Identification des bibliothèques clientes requises {#identify-required-clientlibs}

Les bibliothèques clientes nécessaires au style et au fonctionnement des commentaires par défaut sont également nécessaires pour les commentaires étendus.

Le Guide [des composants](/help/communities/components-guide.md) de la communauté identifie les bibliothèques client requises. Accédez au Guide des composants et vue du composant Commentaires, par exemple :

[https://localhost:4502/content/community-components/en/comments.html](https://localhost:4502/content/community-components/en/comments.html)

Notez les trois bibliothèques clientes requises pour que les commentaires s’affichent et fonctionnent correctement. Ils devront être inclus là où les commentaires étendus sont référencés et la bibliothèque [cliente des commentaires](/help/communities/extend-create-components.md#create-a-client-library-folder) étendus ( `apps.custom.comments`).

![chlimage_1-47](assets/chlimage_1-47.png)

### Ajouter des commentaires personnalisés sur une page {#add-custom-comments-to-a-page}

Comme il ne peut y avoir qu&#39;un seul système de commentaires par page, il est plus simple de créer un exemple de page, comme décrit dans le didacticiel [Créer un exemple de page](/help/communities/create-sample-page.md) .

Une fois le composant créé, entrez en mode Création et rendez disponible le groupe de composants personnalisés pour autoriser son ajout à la page. `Alt Comments`

Pour que le commentaire s’affiche et fonctionne correctement, les bibliothèques clientes pour les commentaires doivent être ajoutées à la liste cliente pour la page (voir [Clientlibs for Communities Components](/help/communities/clientlibs.md)).

#### Commentaires Clientlibs sur l&#39;exemple de page {#comments-clientlibs-on-sample-page}

![chlimage_1-48](assets/chlimage_1-48.png)

#### Auteur : Alt Commenter sur l&#39;exemple de page {#author-alt-comment-on-sample-page}

![chlimage_1-49](assets/chlimage_1-49.png)

#### Auteur : Exemple de noeud de commentaires de page {#author-sample-page-comments-node}

Vous pouvez vérifier le resourceType dans CRXDE en affichant les propriétés du noeud de commentaires pour l’exemple de page à `/content/sites/sample/en/jcr:content/content/primary/comments`l’adresse.

![chlimage_1-50](assets/chlimage_1-50.png)

#### Publier l’exemple de page {#publish-sample-page}

Une fois le composant personnalisé ajouté à la page, il est également nécessaire de (re) [publier la page](/help/communities/sites-console.md#publishing-the-site).

#### Publier : Alt Commenter sur l&#39;exemple de page {#publish-alt-comment-on-sample-page}

Après avoir publié à la fois l’application personnalisée et l’exemple de page, il est possible de saisir un commentaire. Une fois connecté, avec un utilisateur [ou un administrateur de](/help/communities/tutorials.md#demo-users) démonstration, il est possible de publier un commentaire.

aaron.mcdonald@mailinator.com a posté un commentaire :

![chlimage_1-51](assets/chlimage_1-51.png)

![chlimage_1-52](assets/chlimage_1-52.png)

Maintenant qu&#39;il apparaît que le composant étendu fonctionne correctement avec l&#39;apparence par défaut, il est temps de modifier l&#39;apparence.