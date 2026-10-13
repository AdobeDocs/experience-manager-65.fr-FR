---
title: Ajouter un commentaire à l’exemple de page
description: Découvrez comment une instance du système de commentaires d’un site web doit définir resourceType sur le système de commentaires personnalisé et inclure toutes les bibliothèques clientes nécessaires.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: d4295a77-b931-4bc8-b3b4-eec42fdcfc56
solution: Experience Manager
feature: Communities
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%
---
# Ajouter un commentaire à l’exemple de page  {#add-comment-to-sample-page}

Maintenant que les composants du système de commentaires personnalisés sont en place dans le répertoire de l’application (/apps), il est possible d’utiliser le composant étendu. L’instance du système de commentaire dans un site web à affecter doit définir son resourceType sur le système de commentaire personnalisé et inclure toutes les bibliothèques clientes nécessaires.

## Identification des bibliothèques clientes requises {#identify-required-clientlibs}

Les bibliothèques clientes nécessaires pour le style et le fonctionnement des commentaires par défaut sont également nécessaires pour les commentaires étendus.

Le [&#x200B; Guide des composants de communauté &#x200B;](/help/communities/components-guide.md) identifie les bibliothèques clientes requises. Accédez au Guide du composant et affichez le composant Commentaires, par exemple :

[&#128279;](https://localhost:4502/content/community-components/en/comments.html)

Notez les trois bibliothèques clientes requises pour que Comments s’affiche et fonctionne correctement. Ils doivent être inclus là où les commentaires étendus sont référencés, ainsi que la [bibliothèque cliente des commentaires étendus](/help/communities/extend-create-components.md#create-a-client-library-folder) ( `apps.custom.comments`).

![comments-component1](assets/comments-component1.png)

### Ajout de commentaires personnalisés à une page {#add-custom-comments-to-a-page}

Comme il ne peut y avoir qu’un seul système de commentaires par page, il est plus simple de créer un exemple de page comme décrit dans le court tutoriel [créer un exemple de page](/help/communities/create-sample-page.md).

Une fois créé, passez en mode Conception et rendez disponible le groupe de composants Personnalisé pour permettre l’ajout du composant `Alt Comments` à la page.

Pour que le Commentaire s’affiche et fonctionne correctement, les bibliothèques clientes de Comments doivent être ajoutées à la liste clientlibs de la page (voir [Clientlibs pour les composants Communities](/help/communities/clientlibs.md)).

#### Bibliothèques clientes de commentaires dans l’exemple de page {#comments-clientlibs-on-sample-page}

![comments-clientlibs-crxde](assets/comments-clientlibs-crxde.png)

#### Auteur : commentaire alternatif sur la page échantillon {#author-alt-comment-on-sample-page}

![commentaire alternatif](assets/alt-comment.png)

#### Auteur : Exemple de nœud de commentaires de page {#author-sample-page-comments-node}

Vous pouvez vérifier resourceType dans CRXDE en affichant les propriétés du nœud comments pour l’exemple de page à l’adresse `/content/sites/sample/en/jcr:content/content/primary/comments`.

![verify-comment-crxde](assets/verify-comment-crxde.png)

#### Publier l’exemple de page {#publish-sample-page}

Une fois le composant personnalisé ajouté à la page, il est également nécessaire de (re) [publier la page](/help/communities/sites-console.md#publishing-the-site).

#### Publier : commentaire alternatif sur l’exemple de page {#publish-alt-comment-on-sample-page}

Après avoir publié l’application personnalisée et l’exemple de page, il est possible de saisir un commentaire. Une fois connecté, avec un [utilisateur de démonstration](/help/communities/tutorials.md#demo-users) ou un administrateur, il est possible de publier un commentaire.

Voici aaron.mcdonald@mailinator.com postant un commentaire :

![publish-alt-comment](assets/publish-alt-comment.png)

![publish-alt-comment1](assets/publish-alt-comment1.png)

Maintenant qu’il semble que le composant étendu fonctionne correctement avec l’aspect par défaut, il est temps de modifier l’aspect.
