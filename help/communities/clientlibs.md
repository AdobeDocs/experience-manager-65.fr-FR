---
title: Clientlibs des composants Communities
description: Bibliothèques côté client pour les communautés
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 94415926-a273-4f03-b7b6-57fdac12c741
source-git-commit: b9c164321baa3ed82ae87a97a325fcf0ad2f6ca0
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 2%

---

# Clientlibs des composants Communities {#clientlibs-for-communities-components}

## Présentation {#introduction}

Cette section de la documentation décrit comment ajouter des bibliothèques côté client (clientlibs) à une page pour les composants Communities.

Pour obtenir des informations de base, rendez-vous sur :

* [Utilisation de bibliothèques côté client](/help/sites-developing/clientlibs.md) qui fournit des détails d’utilisation et des outils de débogage
* [Clientlibs pour SCF](/help/communities/client-customize.md#clientlibs) qui fournit des informations utiles lors de la personnalisation des composants SCF


## Pourquoi les bibliothèques côté client sont nécessaires {#why-clientlibs-are-required}

Les bibliothèques côté client sont nécessaires au bon fonctionnement (JavaScript) et au style (CSS) d’un composant.

Lorsqu’il existe une [fonction communautaire](/help/communities/functions.md) pour une fonctionnalité, tous les composants et configurations nécessaires, y compris les bibliothèques clientes requises, sont présents sur le site de la communauté. Il est nécessaire d’ajouter des clientlibs supplémentaires uniquement si des composants supplémentaires doivent être disponibles pour les auteurs.

Lorsque les clientlibs requises sont manquantes, [ajout d’un composant Communautés à une page](/help/communities/author-communities.md) peut entraîner des erreurs JavaScript et un aspect inattendu.

### Exemple : Révisions placées sans clientlibs {#example-placed-reviews-without-clientlibs}

![places-review](assets/placed-reviews.png)

### Exemple : Révisions placées avec Clientlibs {#example-placed-reviews-with-clientlibs}

![review-clientlibs](assets/reviews-clientlibs.png)

## Identification des bibliothèques clientes requises {#identifying-required-clientlibs}

Les informations de fonction essentielles pour les développeurs identifient les clientlibs requises.

En outre, à partir d’une instance AEM, accédez au [Guide des composants de communauté](/help/communities/components-guide.md) permet d’accéder à la liste des catégories clientlib requises pour un composant.

Par exemple, en haut de la page [Page des révisions](https://localhost:4502/content/community-components/en/reviews.html) les clientlibs requises répertoriées sont

* cq.ckeditor
* cq.social.hbs.reviews

![clientlibs-review](assets/clientlibs-reviews.png)

## Ajout de bibliothèques clientes requises {#adding-required-clientlibs}

Si vous souhaitez ajouter un composant Communities à une page, il est nécessaire d’ajouter les clientlibs requises pour le composant s’il n’est pas déjà présent.

Utilisation [CRXDE|Lite](#using-crxde-lite) pour modifier une liste de bibliothèques clientes existante pour une page de site communautaire.

Pour ajouter une bibliothèque cliente à un site de la communauté à l’aide d’ [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md):

* Accédez à [https://&lt;server>:&lt;port>/crx/de](https://localhost:4502/crx/de).
* Recherchez la variable `clientlibslist` pour la page sur laquelle vous souhaitez ajouter le composant :

   * `/content/sites/sample/en/page/jcr:content/clientlibslist`

* Avec `clientlibslist` noeud sélectionné :

   * Localisation de la chaîne[] property `scg:requiredClientLibs`.
   * Sélectionnez `Value` pour accéder à la boîte de dialogue Tableau de chaînes .

      * Faites défiler l’écran vers le bas si nécessaire.
      * Sélectionnez + pour entrer une nouvelle bibliothèque cliente.

         * Répétez l’opération pour ajouter d’autres bibliothèques clientes.

         * Sélectionnez **OK**.

   * Sélectionnez **Enregistrer tout**.

>[!NOTE]
>
>Si le site n’est pas un site communautaire, l’existence ou l’emplacement des bibliothèques clientes utilisées pour le site doivent être découverts.

En utilisant la variable [Prise en main d’AEM Communities](/help/communities/getting-started.md) exemple, où `site-name` is *engager*, voici comment clientliblist s’affiche lors de l’ajout du composant de révisions :

![review-component](assets/review-component.png)
