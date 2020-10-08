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
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 1%

---


# Clientlibs pour les composants Communities {#clientlibs-for-communities-components}

## Présentation {#introduction}

Cette section de la documentation décrit comment ajouter des bibliothèques côté client (clientlibs) à une page pour les composants Communities.

Pour obtenir des informations de base, visitez :

* [Utilisation des bibliothèques](/help/sites-developing/clientlibs.md) côté client qui fournit des détails d’utilisation ainsi que des outils de débogage
* [Clientlibs pour SCF](/help/communities/client-customize.md#clientlibs) qui fournit des informations utiles lors de la personnalisation des composants SCF
* [Blog : aem bibliothèques clientes expliquées par l’exemple](https://blogs.adobe.com/experiencedelivers/experience-management/clientlibs-explained-example/)

## Raisons pour lesquelles les bibliothèques clientes sont requises {#why-clientlibs-are-required}

Les bibliothèques clientes sont requises pour le bon fonctionnement (JavaScript) et le style (CSS) d’un composant.

Lorsqu&#39;il existe une fonction [](/help/communities/functions.md) communautaire pour une fonction, tous les composants et configurations nécessaires, y compris les clientlibs requis, seront présents sur le site communautaire. Ce n&#39;est que si d&#39;autres composants doivent être disponibles pour les auteurs que des clientlibs supplémentaires doivent être ajoutés.

Lorsque les clientlibs requis sont manquants, [l’ajout d’un composant Communities à une page](/help/communities/author-communities.md) peut entraîner des erreurs javascript ainsi qu’un aspect inattendu.

### Exemple : Révisions placées sans bibliothèques clientes {#example-placed-reviews-without-clientlibs}

![examens placés](assets/placed-reviews.png)

### Exemple : Révisions référencées avec des bibliothèques clientes {#example-placed-reviews-with-clientlibs}

![reviews-clientlibs](assets/reviews-clientlibs.png)

## Identification des bibliothèques clientes requises {#identifying-required-clientlibs}

Les informations essentielles pour les développeurs identifient les clients requis.

De plus, à partir d’une instance AEM, l’accès au Guide [des composants](/help/communities/components-guide.md) de la communauté permet d’accéder à une liste des catégories clientlib requises pour un composant.

Par exemple, en haut de la page [](https://localhost:4502/content/community-components/en/reviews.html) Révisions, les clientlibs requis répertoriés sont

* cq.ckeditor
* cq.social.hbs.reviews

![clientlibs-reviews](assets/clientlibs-reviews.png)

## Ajouter les bibliothèques clientes requises {#adding-required-clientlibs}

Si vous souhaitez ajouter un composant Communautés à une page, vous devez ajouter les clientlibs requis pour le composant si celui-ci n’est pas déjà présent.

Utilisez [CRXDE|Lite](#using-crxde-lite) pour modifier une liste de clients existante pour une page de site communautaire.

Pour ajouter une bibliothèque cliente à un site communautaire à l&#39;aide de [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md):

* Accédez à [https://&lt;serveur>:&lt;port>/crx/de](https://localhost:4502/crx/de).
* Localisez le `clientlibslist` noeud de la page sur laquelle vous souhaitez ajouter le composant :

   * `/content/sites/sample/en/page/jcr:content/clientlibslist`

* Avec le `clientlibslist` noeud sélectionné :

   * Localisez la propriété String[] `scg:requiredClientLibs`.
   * Sélectionnez son `Value` pour accéder à la boîte de dialogue Tableau de chaînes.

      * Faites défiler la page vers le bas si nécessaire.
      * Sélectionnez + pour entrer une nouvelle bibliothèque cliente.

         * Répétez cette opération pour ajouter d’autres bibliothèques clientes.

         * **Cliquez sur OK**.
   * Select **Save All**.


>[!NOTE]
>
>Si le site n&#39;est pas un site communautaire, il faudrait découvrir l&#39;existence ou l&#39;emplacement des bibliothèques clientes utilisées pour le site.

A l’aide de l’exemple [Prise en main d’AEM Communities](/help/communities/getting-started.md) , où `site-name` est *engagé*, voici comment la liste cliente s’affichera si vous ajoutez le composant de révision :

![composant de révision](assets/review-component.png)

