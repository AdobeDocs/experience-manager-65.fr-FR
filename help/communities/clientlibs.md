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
source-git-commit: efa6c7be93908b2f264da4689caa9c02912c0f0a
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 2%

---


# Clientlibs pour les composants Communities {#clientlibs-for-communities-components}

## Présentation {#introduction}

Cette section de la documentation décrit comment ajouter des bibliothèques côté client (clientlibs) à une page pour les composants Communities.

Pour obtenir des informations de base, visitez :

* [Utilisation des bibliothèques](/help/sites-developing/clientlibs.md) côté client qui fournit des détails d’utilisation ainsi que des outils de débogage
* [Clientlibs pour SCF](/help/communities/client-customize.md#clientlibs) qui fournit des informations utiles lors de la personnalisation des composants SCF
* [Blog : Bibliothèques clientes AEM expliquées par exemple](https://blogs.adobe.com/experiencedelivers/experience-management/clientlibs-explained-example/)

## Raisons pour lesquelles les bibliothèques clientes sont requises {#why-clientlibs-are-required}

Les bibliothèques clientes sont requises pour le bon fonctionnement (JavaScript) et le style (CSS) d’un composant.

Lorsqu&#39;il existe une fonction [](/help/communities/functions.md) communautaire pour une fonction, tous les composants et configurations nécessaires, y compris les clientlibs requis, seront présents sur le site communautaire. Ce n&#39;est que si d&#39;autres composants doivent être disponibles pour les auteurs que des clientlibs supplémentaires doivent être ajoutés.

Lorsque les clientlibs requis sont manquants, [l’ajout d’un composant Communities à une page](/help/communities/author-communities.md) peut entraîner des erreurs javascript ainsi qu’un aspect inattendu.

### Exemple : Révisions placées sans bibliothèques clientes {#example-placed-reviews-without-clientlibs}

![chlimage_1-426](assets/chlimage_1-426.png)

### Exemple : Révisions référencées avec des bibliothèques clientes {#example-placed-reviews-with-clientlibs}

![chlimage_1-427](assets/chlimage_1-427.png)

## Identification des bibliothèques clientes requises {#identifying-required-clientlibs}

Les informations essentielles pour les développeurs identifient les clients requis.

En outre, à partir d’une instance AEM, l’accès au Guide [des composants de la](/help/communities/components-guide.md) communauté permet d’accéder à une liste des catégories clientlib requises pour un composant.

Par exemple, en haut de la page [](https://localhost:4502/content/community-components/en/reviews.html) Révisions, les clientlibs requis répertoriés sont

* cq.ckeditor
* cq.social.hbs.reviews

![chlimage_1-246](assets/chlimage_1-246.png)

## Ajouter les bibliothèques clientes requises {#adding-required-clientlibs}

Si vous souhaitez ajouter un composant Communautés à une page, vous devez ajouter les clientlibs requis pour le composant si celui-ci n’est pas déjà présent.

Utilisez [CRXDE|Lite](#using-crxde-lite) pour modifier une liste de clients existante pour une page de site communautaire.

Pour ajouter une bibliothèque cliente pour un site communautaire à l’aide de [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md):

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


L’exemple [Prise en main des AEM Communities](/help/communities/getting-started.md) , où `site-name` est *engagé*, illustre l’affichage de la liste cliente si vous ajoutez le composant de révision :

![chlimage_1-247](assets/chlimage_1-247.png)

