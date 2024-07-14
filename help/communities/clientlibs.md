---
title: Clientlibs des composants Communities
description: Découvrez comment ajouter des bibliothèques côté client (clientlibs) à une page afin que vous puissiez rassembler les détails d’utilisation et utiliser les outils de débogage pour les composants Communities.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 94415926-a273-4f03-b7b6-57fdac12c741
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 1%

---

# Clientlibs des composants Communities {#clientlibs-for-communities-components}

## Présentation {#introduction}

Cette section de la documentation décrit comment ajouter des bibliothèques côté client (clientlibs) à une page pour les composants Communities.

Pour plus d’informations, voir :

* [Utilisation des bibliothèques côté client](/help/sites-developing/clientlibs.md) qui fournit des détails d’utilisation et des outils de débogage
* [Clientlibs for SCF](/help/communities/client-customize.md#clientlibs) qui fournit des informations utiles lors de la personnalisation des composants SCF


## Pourquoi les bibliothèques côté client sont nécessaires {#why-clientlibs-are-required}

Les bibliothèques côté client sont nécessaires au bon fonctionnement (JavaScript) et à la mise en forme (CSS) d’un composant.

Lorsqu’il existe une [fonction de communauté](/help/communities/functions.md) pour une fonction, tous les composants et configurations nécessaires, y compris les bibliothèques clientes requises, sont présents dans le site de la communauté. Les auteurs ne doivent ajouter des clientlibs supplémentaires que si d’autres composants doivent être disponibles.

Lorsque les clientlibs requises sont manquantes, [l’ajout d’un composant Communities à une page](/help/communities/author-communities.md) peut entraîner des erreurs JavaScript et un aspect inattendu.

### Exemple : révisions placées sans clientlibs {#example-placed-reviews-without-clientlibs}

![placés-review](assets/placed-reviews.png)

### Exemple : révisions placées avec Clientlibs {#example-placed-reviews-with-clientlibs}

![review-clientlibs](assets/reviews-clientlibs.png)

## Identification des bibliothèques clientes requises {#identifying-required-clientlibs}

Les informations de fonction essentielles pour les développeurs identifient les clientlibs requises.

En outre, à partir d’une instance AEM, l’accès au [Guide des composants de la communauté](/help/communities/components-guide.md) permet d’accéder à la liste des catégories clientlib requises pour un composant.

Par exemple, en haut de la [page de révisions](https://localhost:4502/content/community-components/en/reviews.html), les clientlibs requises répertoriées sont

* cq.ckeditor
* cq.social.hbs.reviews

![clientlibs-review](assets/clientlibs-reviews.png)

## Ajout de bibliothèques clientes requises {#adding-required-clientlibs}

Si vous souhaitez ajouter un composant Communities à une page, il est nécessaire d’ajouter les clientlibs requises pour le composant s’il n’est pas déjà présent.

Utilisez [CRXDE|Lite](#using-crxde-lite) pour modifier une liste de bibliothèques clientes existante pour une page de site communautaire.

Pour ajouter une bibliothèque cliente pour un site communautaire à l’aide de [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) :

* Accédez à [https://&lt;server>:&lt;port>/crx/de](https://localhost:4502/crx/de).
* Recherchez le noeud `clientlibslist` de la page sur laquelle vous souhaitez ajouter le composant :

   * `/content/sites/sample/en/page/jcr:content/clientlibslist`

* Avec le noeud `clientlibslist` sélectionné :

   * Localisez la propriété String[] `scg:requiredClientLibs`.
   * Sélectionnez son `Value` pour accéder à la boîte de dialogue Tableau de chaînes .

      * Faites défiler l’écran vers le bas si nécessaire.
      * Sélectionnez + pour entrer une nouvelle bibliothèque cliente.

         * Répétez l’opération pour ajouter d’autres bibliothèques clientes.

         * Sélectionnez **OK**.

   * Sélectionnez **Enregistrer tout**.

>[!NOTE]
>
>Si le site n’est pas un site communautaire, l’existence ou l’emplacement des bibliothèques clientes utilisées pour le site doivent être découverts.

En reprenant l’exemple [Prise en main d’AEM Communities](/help/communities/getting-started.md), où `site-name` est *engage*, voici comment la clientliblist s’affiche en cas d’ajout du composant de révisions :

![review-component](assets/review-component.png)
