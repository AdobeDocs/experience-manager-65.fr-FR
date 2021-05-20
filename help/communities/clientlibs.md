---
title: Clientlibs des composants Communities
seo-title: Clientlibs des composants Communities
description: Bibliothèques côté client pour les communautés
seo-description: Bibliothèques côté client pour les communautés
uuid: d2a9f986-96cf-4ee8-81e6-36a96f45ddcb
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 68ce47c8-a03f-40d6-a7f3-2cc64aee0594
docset: aem65
exl-id: 94415926-a273-4f03-b7b6-57fdac12c741
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 1%

---

# Clientlibs pour les composants Communities {#clientlibs-for-communities-components}

## Présentation {#introduction}

Cette section de la documentation décrit comment ajouter des bibliothèques côté client (clientlibs) à une page pour les composants Communities.

Pour obtenir des informations de base, rendez-vous sur :

* [Utilisation de ](/help/sites-developing/clientlibs.md) bibliothèques côté client qui fournit des détails d’utilisation ainsi que des outils de débogage
* [Clientlibs pour ](/help/communities/client-customize.md#clientlibs) SCF qui fournit des informations utiles lors de la personnalisation des composants SCF
* [Blog : AEM bibliothèques clientes expliquées par l’exemple](https://blogs.adobe.com/experiencedelivers/experience-management/clientlibs-explained-example/)

## Pourquoi les bibliothèques côté client sont requises {#why-clientlibs-are-required}

Les bibliothèques côté client sont nécessaires au bon fonctionnement (JavaScript) et au style (CSS) d’un composant.

Lorsqu’il existe une [fonction de communauté](/help/communities/functions.md) pour une fonction, tous les composants et configurations nécessaires, y compris les clientlibs requises, sont présents sur le site de la communauté. Il est nécessaire d’ajouter des clientlibs supplémentaires uniquement si des composants supplémentaires doivent être disponibles pour les auteurs.

Si les clientlibs requises sont manquantes, [l’ajout d’un composant Communities à une page](/help/communities/author-communities.md) peut entraîner des erreurs JavaScript et un aspect inattendu.

### Exemple : Révisions placées sans Clientlibs {#example-placed-reviews-without-clientlibs}

![places-review](assets/placed-reviews.png)

### Exemple : Révisions avec Clientlibs {#example-placed-reviews-with-clientlibs}

![review-clientlibs](assets/reviews-clientlibs.png)

## Identification des bibliothèques clientes requises {#identifying-required-clientlibs}

Les informations de fonction essentielles pour les développeurs identifient les clientlibs requises.

En outre, à partir d’une instance AEM, l’accès au [Guide des composants de la communauté](/help/communities/components-guide.md) permet d’accéder à la liste des catégories clientlib requises pour un composant.

Par exemple, en haut de la [page Révisions](https://localhost:4502/content/community-components/en/reviews.html), les clientlibs requises sont répertoriées.

* cq.ckeditor
* cq.social.hbs.reviews

![clientlibs-review](assets/clientlibs-reviews.png)

## Ajout de bibliothèques clientes requises {#adding-required-clientlibs}

Si vous souhaitez ajouter un composant Communities à une page, vous devez ajouter les bibliothèques clientes requises pour le composant s’il n’est pas déjà présent.

Utilisez [CRXDE|Lite](#using-crxde-lite) pour modifier une liste de bibliothèques clientes existante pour une page de site de communauté.

Pour ajouter une bibliothèque cliente pour un site communautaire à l’aide de [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) :

* Accédez à [https://&lt;serveur>:&lt;port>/crx/de](https://localhost:4502/crx/de).
* Recherchez le noeud `clientlibslist` de la page sur laquelle vous souhaitez ajouter le composant :

   * `/content/sites/sample/en/page/jcr:content/clientlibslist`

* Avec le noeud `clientlibslist` sélectionné :

   * Recherchez la propriété String[] `scg:requiredClientLibs`.
   * Sélectionnez sa `Value` pour accéder à la boîte de dialogue Tableau de chaînes .

      * Faites défiler l’écran vers le bas si nécessaire.
      * Sélectionnez + pour entrer une nouvelle bibliothèque cliente.

         * Répétez l’opération pour ajouter d’autres bibliothèques clientes.

         * **Cliquez sur OK**.
   * Sélectionnez **Enregistrer tout**.


>[!NOTE]
>
>Si le site n’est pas un site communautaire, l’existence ou l’emplacement des bibliothèques clientes utilisées pour le site doivent être découverts.

À l’aide de l’exemple [Prise en main d’AEM Communities](/help/communities/getting-started.md), où `site-name` est *engage*, voici comment la liste client s’afficherait lors de l’ajout du composant de révisions :

![review-component](assets/review-component.png)
