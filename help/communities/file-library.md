---
title: Fonctionnalité Bibliothèque de fichiers
seo-title: Fonctionnalité Bibliothèque de fichiers
description: La fonction Bibliothèque de fichiers permet aux visiteurs de site connectés de télécharger, gérer et télécharger des fichiers.
seo-description: La fonction Bibliothèque de fichiers permet aux visiteurs de site connectés de télécharger, gérer et télécharger des fichiers.
uuid: e78a90bd-f1d3-44f8-98eb-1498a55e8217
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: ea2b23af-49c3-409b-a041-43c42d846f21
docset: aem65
translation-type: tm+mt
source-git-commit: 9e941ce092f7d3248c11886d6bf1e54f2e726362
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 35%

---


# Fonctionnalité Bibliothèque de fichiers{#file-library-feature}

## Présentation {#introduction}

La fonctionnalité Bibliothèque de fichiers fournit un espace où les visiteurs du site connectés (membres de la communauté) peuvent transférer, gérer et télécharger des fichiers sur le site de la communauté.

Cette section de la documentation décrit : :

* Ajouter la fonction de bibliothèque de fichiers à un site AEM.
* Configuration settings for the `File Library` component.

### Ajout d’une bibliothèque de fichiers à une page {#adding-a-file-library-to-a-page}

To add a `File Library` component to a page in author mode, locate the component:

* `Communities / File Library`

et faites-le glisser sur la page.

For necessary information, visit [Communities Components Basics](/help/communities/basics.md).

When the [required client-side libraries](/help/communities/essentials-file-library.md#essentials-for-client-side) are included, this is how the `File Library` component will appear:

![chlimage_1-430](assets/chlimage_1-430.png)

### Configuration de la bibliothèque de fichiers {#configuring-file-library}

Select the placed `File Library` component to access and select the `Configure` icon which opens the edit dialog.

![chlimage_1-431](assets/chlimage_1-431.png)

![chlimage_1-432](assets/chlimage_1-432.png)

#### Comments tab {#comments-tab}

Dans l’onglet **Commentaires**, indiquez si et comment les commentaires pour les fichiers transférés apparaissent :

* **Autoriser les commentaires sur les fichiers**

   Si cette case est cochée, autorisez des commentaires sur les fichiers téléchargés. Cette option n’est pas cochée par défaut.

* **Commentaires par page**

   Limite le nombre de commentaires affichés par page ainsi que le nombre de réponses affichées. La valeur par défaut est **10**.

* **Taille maximale du fichier**

   Cette valeur limite la taille du fichier chargé. La limite par défaut est 104857600 (10 Mo).

* **Longueur de message max.**

   Nombre maximal de caractères pouvant être saisis dans la zone de texte. La valeur par défaut est de 4 096 caractères.

* **Types de fichier autorisés**

   liste séparée par des virgules d’extensions de fichiers avec le séparateur &quot;point&quot;. Par exemple : .jpg, .jpeg, .png, .doc, .docx, .pdf. Si des types de fichier sont spécifiés, ceux qui ne sont pas spécifiés ne seront pas autorisés. La valeur par défaut n&#39;est pas spécifiée de sorte que tous les types de fichier soient autorisés.

* **Éditeur de texte enrichi**

   Si cette case est cochée, les commentaires peuvent être saisis avec une annotation. Cette option n’est pas cochée par défaut.

* **Supprimer les commentaires**

   Si cette case est cochée, les utilisateurs sont autorisés à supprimer leurs propres commentaires. Cette option est cochée par défaut.

* **Autoriser le balisage**

   Si cette option est cochée, la possibilité d’ajouter une balise au fichier est activée. Cette option n’est pas cochée par défaut.

* **Espaces de noms autorisés**

   Si l’option Autoriser le balisage est cochée, les balises disponibles seront limitées aux espaces de nommage cochés. Si aucun n&#39;est coché, tous sont autorisés. Par défaut, tous les espaces de noms sont autorisés.

* **Limite de suggestions**

   Si l’option Autoriser le balisage est cochée, ce paramètre limite le nombre de balises suggérées à afficher. Si la valeur est -1, il n’existe aucune limite. La valeur par défaut est -1.

* **Autoriser le vote**

   Si cette case est cochée, la possibilité de voter pour un fichier sera activée. Cette option n’est pas cochée par défaut.

* **Autoriser abonnement**

   Si cette option est cochée, incluez la fonctionnalité suivante pour les articles de blog, ce qui permet aux membres d&#39;être [informés](/help/communities/notifications.md) des nouvelles publications. Cette option n’est pas cochée par défaut.

* **Activer la mention**

   S’il est activé, permet aux utilisateurs enregistrés de la communauté d’identifier d’autres membres enregistrés (à l’aide de leur prénom, de leur nom de famille, de leur nom d’utilisateur) et de les baliser à l’aide de la syntaxe courante de @user-name. Les utilisateurs balisés reçoivent des notifications concernant leurs mentions.

* **Nombre max. de mentions**

   Limitez le nombre maximum de mentions autorisées dans une publication. La valeur par défaut est 10.

* **Modèle des mentions de l’IU**

   Spécifiez la chaîne de modèle autorisée à baliser (@mentions) l’utilisateur enregistré dans une publication. Par exemple ~{{familyName}}{{donneesName}}.

* **Autoriser les réponses à thème**

   Si cette option est cochée, autorisez les réponses aux commentaires publiés. Cette option n’est pas cochée par défaut.

#### Onglet Modération utilisateur {#user-moderation-tab}

Dans l’onglet **Modération d’utilisateur**, configurez la modération des commentaires, si les commentaires sont autorisés :

* **Prémodération**

   Si cette option est cochée, les commentaires doivent être approuvés avant d’apparaître sur un site de publication. Cette option n’est pas cochée par défaut.

* **Supprimer les commentaires**

   Si cette case est cochée, le visiteur qui a publié le commentaire peut le supprimer. Cette option est cochée par défaut.

* **Refuser les commentaires**

   Si cette option est cochée, autorisez les modérateurs membres de confiance à refuser les commentaires. Cette option n’est pas cochée par défaut.

* **Fermer/rouvrir les commentaires**

   Si cette option est cochée, autorisez les modérateurs de membres approuvés à fermer et rouvrir les commentaires. Cette option n’est pas cochée par défaut.

* **Marquer les commentaires**

   Si cette option est cochée, autorisez les visiteurs à signaler les commentaires comme inappropriés. Cette option n’est pas cochée par défaut.

* **Marquer la liste de motifs**

   Si cette option est cochée, permettez aux visiteurs de choisir, dans une liste déroulante, la raison pour laquelle ils signalent un commentaire comme inapproprié. Cette option n’est pas cochée par défaut.

* **Motif de la marque personnalisée**

   Si cette option est cochée, autorisez les visiteurs à entrer leur propre raison de signaler un commentaire comme inapproprié. Cette option n’est pas cochée par défaut.

* **Seuil de modération**

   Indiquez le nombre de fois où un commentaire doit être marqué par des visiteurs avant que les modérateurs ne soient avertis. La valeur par défaut est une fois (**1**).

* **Limite de marquage**

   Indiquez le nombre de fois où un commentaire doit être marqué avant d’être masqué dans la vue publique. Dans le cas contraire, cette valeur doit être supérieure ou égale au **seuil de modération**. La valeur par défaut est 5.

### Onglet Paramètres de tri {#sort-settings-tab}

Trier par

Définir par défaut

### Informations supplémentaires {#additional-information}

More information may be found on the [File Library Essentials](/help/communities/essentials-file-library.md) page for developers.

Pour des informations sur la modération des sujets et des commentaires publiés, reportez-vous à la section [Modération du contenu généré par l’utilisateur](/help/communities/moderate-ugc.md).

Pour baliser les sujets et les commentaires publiés, voir [Balisage de contenu généré par l’utilisateur](/help/communities/tag-ugc.md).
