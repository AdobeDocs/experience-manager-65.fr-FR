---
title: Clientlibs pour les composants Communities
seo-title: Clientlibs pour les composants Communities
description: Bibliothèques côté client pour les communautés
seo-description: Bibliothèques côté client pour les communautés
uuid: d2a9f986-96cf-4ee8-81e6-36a96f45ddcb
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 68ce47c8-a03f-40d6-a7f3-2cc64aee0594
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Clientlibs pour les composants Communities{#clientlibs-for-communities-components}

## Présentation {#introduction}

Cette section de la documentation décrit comment ajouter des bibliothèques côté client (clientlibs) à une page pour les composants Communities.

Pour obtenir des informations de base, visitez :

* [Utilisation des bibliothèques](/help/sites-developing/clientlibs.md) côté client qui fournit des informations d’utilisation ainsi que des outils de débogage
* [Clientlibs for SCF](/help/communities/client-customize.md#clientlibs) qui fournit des informations utiles lors de la personnalisation des composants SCF
* [Blog : Bibliothèques clientes AEM expliquées par exemple](https://blogs.adobe.com/experiencedelivers/experience-management/clientlibs-explained-example/)

## Raisons pour lesquelles les bibliothèques clientes sont requises {#why-clientlibs-are-required}

Les bibliothèques clientes sont requises pour le bon fonctionnement (JavaScript) et le style (CSS) d’un composant.

Lorsqu’il existe une fonction [de](/help/communities/functions.md) communauté pour une fonction, tous les composants et configurations nécessaires, y compris les clients requis, seront présents sur le site de la communauté. Ce n&#39;est que si des composants supplémentaires doivent être disponibles pour les auteurs que des clients supplémentaires doivent être ajoutés.

Lorsque les clientlibs requis sont manquants, l’ [ajout d’un composant Communities à une page](/help/communities/author-communities.md) peut entraîner des erreurs JavaScript et un aspect inattendu.

### Exemple : Révisions importées sans bibliothèques clientes {#example-placed-reviews-without-clientlibs}

![chlimage_1-132](assets/chlimage_1-132.png)

### Exemple : Révisions importées avec des bibliothèques clientes {#example-placed-reviews-with-clientlibs}

![chlimage_1-133](assets/chlimage_1-133.png)

## Identification des bibliothèques clientes requises {#identifying-required-clientlibs}

Les informations essentielles pour les développeurs identifient les clients requis.

En outre, à partir d’une instance AEM, l’accès au Guide [des composants de la](/help/communities/components-guide.md) communauté permet d’accéder à une liste des catégories clientlib requises pour un composant.

Par exemple, en haut de la page [](https://localhost:4502/content/community-components/en/reviews.html) Révisions, les clients requis répertoriés sont

* cq.ckeditor
* cq.social.hbs.reviews

![chlimage_1-134](assets/chlimage_1-134.png)

## Ajout de bibliothèques clientes requises {#adding-required-clientlibs}

Lorsqu’il est nécessaire d’ajouter un composant Communautés à une page, il est nécessaire d’ajouter les clients requis pour le composant s’il n’est pas déjà présent.

Utilisez [CRXDE|Lite](#using-crxde-lite) pour modifier une liste de clients existante pour une page de site communautaire.

Pour ajouter une bibliothèque cliente pour un site communautaire à l’aide de [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) :

* accédez à [https://&lt;serveur>:&lt;port>/crx/de](https://localhost:4502/crx/de)
* recherchez le `clientlibslist` noeud de la page sur laquelle vous souhaitez ajouter le composant.

   * `/content/sites/sample/en/page/jcr:content/clientlibslist`

* avec le `clientlibslist` noeud sélectionné

   * localiser la propriété String[]`scg:requiredClientLibs`
   * sélectionnez son `Value` pour accéder à la boîte de dialogue Tableau de chaînes

      * faire défiler vers le bas si nécessaire
      * sélectionner + pour entrer une nouvelle bibliothèque cliente

         * répéter pour ajouter d’autres bibliothèques clientes
      * select** OK***
   * sélectionnez **Enregistrer tout**



>[!NOTE]
>
>Si le site n&#39;est pas un site communautaire, l&#39;existence ou l&#39;emplacement des bibliothèques clientes utilisées pour le site devront être découverts.

A l’aide de l’exemple [Prise en main des communautés](/help/communities/getting-started.md) AEM, où `site-name` s’engage **, voici comment la liste cliente s’affichera si vous ajoutez le composant de révisions :

![chlimage_1-135](assets/chlimage_1-135.png)

