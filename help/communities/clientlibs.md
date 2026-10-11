---
title: Bibliothèques clientes pour les composants de Communities
description: Découvrez comment ajouter des bibliothèques côté client (clientlibs) à une page afin de rassembler des détails d’utilisation et d’utiliser des outils de débogage pour les composants de Communities.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 94415926-a273-4f03-b7b6-57fdac12c741
solution: Experience Manager
feature: Communities
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 2%
---
# Bibliothèques clientes pour les composants de Communities {#clientlibs-for-communities-components}

## Présentation {#introduction}

Cette section de la documentation décrit comment ajouter des bibliothèques côté client (clientlibs) à une page pour les composants de Communities.

Pour obtenir des informations de base, voir :

* [Utilisation des bibliothèques côté client](/help/sites-developing/clientlibs.md) qui fournit des détails d’utilisation et des outils de débogage
* [Clientlibs pour SCF](/help/communities/client-customize.md#clientlibs) qui fournit des informations utiles pour la personnalisation des composants SCF


## Pourquoi les bibliothèques clientes sont-elles requises ? {#why-clientlibs-are-required}

Les bibliothèques clientes sont requises pour le bon fonctionnement (JavaScript) et le style (CSS) d’un composant.

Lorsqu’il existe une [fonction de communauté](/help/communities/functions.md) pour une fonctionnalité, tous les composants et configurations nécessaires, y compris les bibliothèques clientes requises, sont présents dans le site de la communauté. D’autres bibliothèques clientes doivent être ajoutées uniquement si des composants supplémentaires doivent être disponibles pour les auteurs.

Lorsque les bibliothèques clientes requises sont manquantes, [ l’ajout d’un composant Communities à une page](/help/communities/author-communities.md) peut entraîner des erreurs JavaScript et une apparence inattendue.

### Exemple : révisions effectuées sans Clientlibs {#example-placed-reviews-without-clientlibs}

![places-review](assets/placed-reviews.png)

### Exemple : commentaires placés avec Clientlibs {#example-placed-reviews-with-clientlibs}

![review-clientlibs](assets/reviews-clientlibs.png)

## Identification des bibliothèques clientes requises {#identifying-required-clientlibs}

Les informations essentielles sur les fonctionnalités destinées aux développeurs identifient les bibliothèques clientes requises.

En outre, à partir d’une instance AEM, en accédant au [guide des composants de la communauté](/help/communities/components-guide.md) vous pouvez accéder à une liste des catégories de bibliothèques clientes requises pour un composant.

Par exemple, en haut de la page [Examens](https://localhost:4502/content/community-components/en/reviews.html) les bibliothèques clientes requises répertoriées sont les suivantes :

* cq.ckeditor
* cq.social.hbs.views

![clientlibs-views](assets/clientlibs-reviews.png)

## Ajout des bibliothèques clientes requises {#adding-required-clientlibs}

Lorsque vous souhaitez ajouter un composant Communities à une page, il est nécessaire d’ajouter les bibliothèques clientes requises pour le composant, si elles ne sont pas déjà présentes.

Utilisez [CRXDE|Lite](#using-crxde-lite) pour modifier une liste de bibliothèques clientes existante pour une page de site communautaire.

Pour ajouter une bibliothèque cliente pour un site communautaire à l’aide de [](/help/sites-developing/developing-with-crxde-lite.md) :

* Accédez à [https://&lt;server>:&lt;port>/crx/de](https://localhost:4502/crx/de).
* Recherchez le nœud `clientlibslist` de la page sur laquelle vous souhaitez ajouter le composant :

  * `/content/sites/sample/en/page/jcr:content/clientlibslist`

* Avec `clientlibslist` nœud sélectionné :

  * Recherchez le `scg:requiredClientLibs` de propriété String[] .
  * Sélectionnez son `Value` pour accéder à la boîte de dialogue Tableau de chaînes.

    * Faites défiler l’écran vers le bas si nécessaire.
    * Sélectionnez + pour saisir une nouvelle bibliothèque cliente.

      * Répétez l’opération pour ajouter d’autres bibliothèques clientes.

      * Sélectionnez **OK**.

  * Sélectionnez **Enregistrer tout**.

>[!NOTE]
>
>Si le site n’est pas un site communautaire, l’existence ou l’emplacement des bibliothèques clientes utilisées pour le site doit être découvert.

En reprenant l’exemple [Prise en main d’AEM Communities](/help/communities/getting-started.md), où `site-name` est *engage*, voici à quoi la liste de bibliothèques clientes s’afficherait si vous ajoutiez le composant révisions :

![review-component](assets/review-component.png)
