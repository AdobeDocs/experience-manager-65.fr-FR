---
title: Fonctionnalité Bibliothèque de fichiers
seo-title: Fonctionnalité Bibliothèque de fichiers
description: La fonctionnalité Bibliothèque de fichiers permet aux du site connectés de télécharger, de télécharger et de gérer des fichiers.
seo-description: La fonctionnalité Bibliothèque de fichiers permet aux du site connectés de télécharger, de télécharger et de gérer des fichiers.
uuid: e78a90bd-f1d3-44f8-98eb-1498a55e8217
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: ea2b23af-49c3-409b-a041-43c42d846f21
docset: aem65
translation-type: tm+mt
source-git-commit: 58a06c1a16c62bffad2893fbec0b32d2ce7267a7

---


# Fonctionnalité Bibliothèque de fichiers{#file-library-feature}

## Présentation {#introduction}

La fonctionnalité Bibliothèque de fichiers fournit un espace où les visiteurs du site connectés (membres de la communauté) peuvent transférer, gérer et télécharger des fichiers sur le site de la communauté.

Cette section de la documentation décrit : :

* Ajout de la fonctionnalité de bibliothèque de fichiers à un site AEM.
* Configuration settings for the `File Library` component.

### Ajout d’une bibliothèque de fichiers à une page {#adding-a-file-library-to-a-page}

To add a `File Library` component to a page in author mode, locate the component

* `Communities / File Library`

et faites-le glisser sur la page.

For necessary information, visit [Communities Components Basics](/help/communities/basics.md).

When the [required client-side libraries](/help/communities/essentials-file-library.md#essentials-for-client-side) are included, this is how the `File Library` component will appear:

![chlimage_1-145](assets/chlimage_1-145.png)

### Configuration de la bibliothèque de fichiers {#configuring-file-library}

Select the placed `File Library` component to access and select the `Configure` icon which opens the edit dialog.

![chlimage_1-146](assets/chlimage_1-146.png) ![forum-config-1](assets/forum-config-1.png)

#### Comments tab {#comments-tab}

Dans l’onglet **Commentaires**, indiquez si et comment les commentaires pour les fichiers transférés apparaissent :

* **Autoriser les commentaires sur les fichiers**

   Si cette option est cochée, autorisez les commentaires sur les fichiers téléchargés. Cette option n’est pas cochée par défaut.

* **Commentaires par page**

   Limite le nombre de commentaires affichés par page ainsi que le nombre de réponses affichées. La valeur par défaut est **10**.

* **Taille maximale du fichier**

   Cette valeur limite la taille du fichier chargé. La limite par défaut est 104857600 (10 Mo).

* **Longueur de message max.**

   Nombre maximal de caractères pouvant être saisis dans la zone de texte. La valeur par défaut est de 4 096 caractères.

* **Types de fichier autorisés**

   d’extensions de fichier séparé par des virgules avec le séparateur &quot;point&quot;. Par exemple : .jpg, .jpeg, .png, .doc, .docx, .pdf. Si des types de fichier sont spécifiés, ceux qui ne sont pas spécifiés ne seront pas autorisés. Par défaut, tous les types de fichier sont autorisés.

* **Éditeur de texte enrichi**

   Si cette option est cochée, les commentaires peuvent être saisis avec une annotation. Cette option n’est pas cochée par défaut.

* **Supprimer les commentaires**

   Si cette option est cochée, les utilisateurs sont autorisés à supprimer leurs propres commentaires. Cette option est cochée par défaut.

* **Autoriser le balisage**

   Si cette option est cochée, la possibilité d’ajouter une balise au fichier est activée. Cette option n’est pas cochée par défaut.

* **Espaces de noms autorisés**

   Si l’option Autoriser le balisage est cochée, les balises disponibles seront limitées au   coché. Si aucun n&#39;est coché, tous sont autorisés. Par défaut, tous les espaces de noms sont autorisés.

* **Limite de suggestions**

   Si l’option Autoriser le balisage est cochée, ce paramètre limite le nombre de balises suggérées à afficher. Si la valeur est -1, il n’existe aucune limite. La valeur par défaut est -1.

* **Autoriser le vote**

   Si cette option est cochée, la possibilité d&#39;aller voter pour un fichier sera activée. Cette option n’est pas cochée par défaut.

* **Autoriser abonnement**

   Si cette option est cochée, incluez la fonctionnalité suivante pour les articles de blog, ce qui permet aux membres d’être [informés](/help/communities/notifications.md) des nouvelles publications. Cette option n’est pas cochée par défaut.

* **Activer la mention**

   S’il est activé, permet aux utilisateurs enregistrés de la communauté d’identifier d’autres membres enregistrés (à l’aide du prénom, du nom de famille, du nom d’utilisateur) et de les baliser à l’aide de la syntaxe @user-name courante. Les utilisateurs balisés reçoivent des notifications concernant leurs mentions.

* **Nombre max. de mentions**

   Limitez le nombre maximum de mentions autorisées dans une publication. La valeur par défaut est 10.

* **Modèle des mentions de l’IU**

   Spécifiez la chaîne de modèle autorisée à baliser (@mentions) l’utilisateur enregistré dans une publication. Par exemple : ~{{familyName}}{{donnname}}.

* **Autoriser les réponses à thème**

   Si cette option est cochée, autorisez les réponses aux commentaires publiés. Cette option n’est pas cochée par défaut.

#### Onglet Modération utilisateur {#user-moderation-tab}

Dans l’onglet **Modération d’utilisateur**, configurez la modération des commentaires, si les commentaires sont autorisés :

* **Prémodération**

   Si cette option est cochée, les commentaires doivent être approuvés avant de s’afficher sur un site de publication. Cette option n’est pas cochée par défaut.

* **Supprimer les commentaires**

   Si cette option est cochée, le qui a publié le commentaire peut le supprimer. Cette option est cochée par défaut.

* **Refuser les commentaires**

   Si cette option est cochée, autorisez les modérateurs de membres de confiance à refuser les commentaires. Cette option n’est pas cochée par défaut.

* **Fermer/rouvrir les commentaires**

   Si cette option est cochée, autorisez les modérateurs de membres approuvés à fermer et rouvrir les commentaires. Cette option n’est pas cochée par défaut.

* **Marquer les commentaires**

   Si cette option est cochée, autorisez les à signaler les commentaires comme inappropriés. Cette option n’est pas cochée par défaut.

* **Marquer la liste de motifs**

   Si cette option est cochée, permettez aux de choisir, dans un  déroulant, la raison pour laquelle ils signalent un commentaire comme étant inapproprié. Cette option n’est pas cochée par défaut.

* **Motif de la marque personnalisée**

   Si cette option est cochée, autorisez les à saisir leur propre raison pour signaler un commentaire comme inapproprié. Cette option n’est pas cochée par défaut.

* **Seuil de modération**

   Entrez le nombre de fois où un commentaire doit être marqué par les avant que les modérateurs ne soient avertis. La valeur par défaut est une fois (**1**).

* **Limite de marquage**

   Entrez le nombre de fois où un commentaire doit être marqué avant d’être masqué dans le public. Dans le cas contraire, cette valeur doit être supérieure ou égale au **seuil de modération**. La valeur par défaut est 5.

### Onglet Paramètres de tri {#sort-settings-tab}

Trier par

Définir par défaut

### Informations supplémentaires {#additional-information}

More information may be found on the [File Library Essentials](/help/communities/essentials-file-library.md) page for developers.

Pour des informations sur la modération des sujets et des commentaires publiés, reportez-vous à la section [Modération du contenu généré par l’utilisateur](/help/communities/moderate-ugc.md).

Pour baliser les sujets et les commentaires publiés, voir [Balisage de contenu généré par l’utilisateur](/help/communities/tag-ugc.md).
