---
title: Fonctionnalité Bibliothèque de fichiers
description: La fonctionnalité Bibliothèque de fichiers permet aux visiteurs connectés du site de télécharger, gérer et télécharger des fichiers.
uuid: e78a90bd-f1d3-44f8-98eb-1498a55e8217
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: ea2b23af-49c3-409b-a041-43c42d846f21
docset: aem65
exl-id: 05cfaab5-a12d-475f-9095-a9fb13571d0a
source-git-commit: d673a447e9ce2377c8645c87f12be81cbad06238
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 10%

---

# Fonctionnalité Bibliothèque de fichiers{#file-library-feature}

## Présentation {#introduction}

La fonctionnalité Bibliothèque de fichiers fournit un emplacement où les visiteurs connectés du site (membres de la communauté) peuvent charger, gérer et télécharger des fichiers dans le site de la communauté.

Cette section de la documentation décrit :

* Ajout de la fonction Bibliothèque de fichiers à un site AEM.
* Paramètres de configuration de la variable `File Library` composant.

### Ajout d’une bibliothèque de fichiers à une page {#adding-a-file-library-to-a-page}

Pour ajouter une `File Library` pour accéder à une page en mode création, recherchez le composant :

* `Communities / File Library`

Et faites-le glisser sur la page.

Pour obtenir les informations nécessaires, consultez la section [Principes de base des composants des communautés](/help/communities/basics.md).

Lorsque la variable [bibliothèques côté client requises](/help/communities/essentials-file-library.md#essentials-for-client-side) sont incluses, c’est ainsi que la variable `File Library` Le composant apparaît :

![file-library1](assets/file-library1.png)

### Configuration de la bibliothèque de fichiers {#configuring-file-library}

Sélectionnez le `File Library` afin que vous puissiez accéder au `Configure` qui ouvre la boîte de dialogue de modification.

![configure-new](assets/configure-new.png)

![file-library2](assets/file-library2.png)

#### Onglet Commentaires {#comments-tab}

Sous , **Commentaires** , indiquez si et comment les commentaires des fichiers chargés apparaissent :

* **Autoriser les commentaires sur les fichiers**

  Si cette option est cochée, les commentaires sur les fichiers chargés sont autorisés. La case par défaut est décochée.

* **Commentaires par page**

  Limite le nombre de commentaires affichés par page et le nombre de réponses affichées. La valeur par défaut est **10**.

* **Taille maximale du fichier**

  Cette valeur limite la taille du fichier téléchargé. La limite par défaut est 104857600 (10 Mo).

* **Longueur de message max.**

  Nombre maximal de caractères pouvant être saisis dans la zone de texte. La valeur par défaut est de 4 096 caractères.

* **Types de fichier autorisés**

  Liste d’extensions de fichier séparées par des virgules avec le séparateur &quot;point&quot;. Par exemple, .jpg, .jpeg, .png, .doc, .docx, .pdf. Si des types de fichiers sont spécifiés, les types qui ne sont pas spécifiés ne sont pas autorisés. La valeur par défaut n’est pas spécifiée de sorte que tous les types de fichiers soient autorisés.

* **Éditeur de texte enrichi**

  Si cette case est cochée, les commentaires peuvent être saisis avec une annotation. La case par défaut est décochée.

* **Supprimer les commentaires**

  Si cette case est cochée, les utilisateurs sont autorisés à supprimer leurs propres commentaires. La valeur par défaut est cochée.

* **Autoriser le balisage**

  Si cette case est cochée, la possibilité d’ajouter une balise au fichier est activée. La case par défaut est décochée.

* **Espaces de noms autorisés**

  Si l’option Autoriser le balisage est cochée, les balises disponibles sont limitées aux espaces de noms cochés. Si aucun espace de noms n’est coché, tous sont autorisés. La valeur par défaut est tous les espaces de noms.

* **Limite de suggestions**

  Si l’option Autoriser le balisage est cochée, ce paramètre limite le nombre de balises suggérées à afficher. S’il est défini sur -1, il n’y a aucune limite. La valeur par défaut est -1.

* **Autoriser le vote**

  Si cette case est cochée, la possibilité de voter pour un fichier est activée. La case par défaut est décochée.

* **Autoriser abonnement**

  Si cette case est cochée, incluez la fonction suivante pour les articles de blog, ce qui permet aux membres d’être [notify](/help/communities/notifications.md) de nouvelles publications. La case par défaut est décochée.

* **Activer la mention**

  S’il est activé, permet aux utilisateurs enregistrés de la communauté d’identifier d’autres membres enregistrés (à l’aide du prénom, du nom, du nom d’utilisateur) et de les baliser à l’aide de la syntaxe @user-name courante. Les utilisateurs balisés reçoivent des notifications sur leurs mentions.

* **Nombre max. de mentions**

  Limitez le nombre maximal de mentions autorisées dans une publication. La valeur par défaut est 10.

* **Modèle des mentions de l’IU**

  Spécifiez la chaîne de modèle autorisée afin de marquer (@mention) l’utilisateur enregistré dans une publication. Par exemple, `~{{familyName}}{{givenName}}`.

* **Autoriser les réponses à thème**

  Si cette case est cochée, les réponses aux commentaires publiés sont autorisées. La case par défaut est décochée.

#### Onglet Modération d’utilisateur {#user-moderation-tab}

Sous , **Modération d’utilisateur** , configurez la modération des commentaires, si les commentaires sont autorisés :

* **Prémodération**

  Si cette case est cochée, les commentaires doivent être approuvés avant d’apparaître sur un site de publication. La case par défaut est décochée.

* **Supprimer les commentaires**

  Si cette case est cochée, le visiteur qui a publié le commentaire peut le supprimer, si nécessaire. La valeur par défaut est cochée.

* **Refuser les commentaires**

  Si cette case est cochée, autorisez les modérateurs de membres approuvés à refuser des commentaires. La case par défaut est décochée.

* **Fermer/rouvrir les commentaires**

  Si cette case est cochée, autorisez les modérateurs de membres approuvés à fermer et rouvrir les commentaires. La case par défaut est décochée.

* **Marquer les commentaires**

  Si cette case est cochée, autorisez les visiteurs à signaler les commentaires comme inappropriés. La case par défaut est décochée.

* **Marquer la liste de motifs**

  Si cette case est cochée, les visiteurs ont le droit de sélectionner dans une liste déroulante la ou les raisons pour lesquelles ils ont marqué un commentaire comme étant inapproprié. La case par défaut est décochée.

* **Motif de la marque personnalisée**

  Si cette case est cochée, autorisez les visiteurs à indiquer leur propre raison de signaler un commentaire comme inapproprié. La case par défaut est décochée.

* **Seuil de modération**

  Saisissez le nombre de fois qu’un commentaire doit être marqué par les visiteurs avant que les modérateurs ne soient informés. La valeur par défaut est une fois (**1**).

* **Limite de marquage**

  Saisissez le nombre de fois qu’un commentaire doit être marqué avant qu’il ne soit plus visible pour le public. Ce nombre doit être supérieur ou égal à **Seuil de modération**. La valeur par défaut est 5.

### Onglet Paramètres de tri {#sort-settings-tab}

Trier par

Définir par défaut

### Informations supplémentaires {#additional-information}

Vous trouverez plus d’informations sur la [Notions fondamentales sur la bibliothèque de fichiers](/help/communities/essentials-file-library.md) pour les développeurs.

Pour la modération des sujets et des commentaires publiés, voir [Modération de contenu généré par l’utilisateur](/help/communities/moderate-ugc.md).

Pour baliser des sujets et des commentaires publiés, voir [Balisage de contenu généré par l’utilisateur](/help/communities/tag-ugc.md).
