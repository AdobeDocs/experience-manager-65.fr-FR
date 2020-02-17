---
title: Fonctionnalité Bibliothèque de fichiers
seo-title: Fonctionnalité Bibliothèque de fichiers
description: La fonctionnalité Bibliothèque de fichiers permet aux visiteurs du site connectés de télécharger, de télécharger et de gérer des fichiers.
seo-description: La fonctionnalité Bibliothèque de fichiers permet aux visiteurs du site connectés de télécharger, de télécharger et de gérer des fichiers.
uuid: e78a90bd-f1d3-44f8-98eb-1498a55e8217
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: ea2b23af-49c3-409b-a041-43c42d846f21
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Fonctionnalité Bibliothèque de fichiers{#file-library-feature}

## Présentation {#introduction}

La fonctionnalité Bibliothèque de fichiers fournit un espace où les visiteurs du site connectés (membres de la communauté) peuvent transférer, gérer et télécharger des fichiers sur le site de la communauté.

Cette section de la documentation décrit :

* l’ajout de la fonctionnalité Bibliothèque de fichiers à un site AEM ;
* les paramètres de configuration du composant `File Library`.

### Ajout d’une bibliothèque de fichiers à une page {#adding-a-file-library-to-a-page}

To add a `File Library` component to a page in author mode, locate the component

* `Communities / File Library`

et faites-le glisser sur la page.

For necessary information, visit [Communities Components Basics](/help/communities/basics.md).

When the [required client-side libraries](/help/communities/essentials-file-library.md#essentials-for-client-side) are included, this is how the `File Library` component will appear :

![chlimage_1-145](assets/chlimage_1-145.png)

### Configuration de la bibliothèque de fichiers {#configuring-file-library}

Select the placed `File Library` component to access and select the `Configure` icon which opens the edit dialog.

![chlimage_1-146](assets/chlimage_1-146.png) ![forum-config-1](assets/forum-config-1.png)

#### Onglet Commentaires {#comments-tab}

Sous l’onglet **Commentaires **, indiquez si et comment les commentaires des fichiers téléchargés apparaissent :

* **Autoriser les commentaires sur les fichiers** Si cette option est cochée, les commentaires sur les fichiers transférés sont autorisés. Cette option n’est pas cochée par défaut.

* **Commentaires par page** Limite le nombre de commentaires par page, ainsi que le nombre de réponses affichées. La valeur par défaut est **10**.

* **Taille maximale du fichier** Cette valeur limite la taille du fichier transféré. La limite par défaut est 104857600 (10 Mo).

* **Longueur de message max.** Nombre maximal de caractères qui peuvent être saisis dans la zone de texte. La valeur par défaut est de 4 096 caractères.

* **Types de fichier autorisés** Une liste d’extensions de fichier séparées par des virgules avec le séparateur « point ». Par exemple : .jpg, .jpeg, .png, .doc, .docx, .pdf. Si des types de fichier sont spécifiés, ceux qui ne sont pas spécifiés ne seront pas autorisés. La valeur par défaut n’est pas spécifiée, de sorte que** **tous les types de fichier sont autorisés.

* **Éditeur de texte enrichi** Si cette option est activée, les commentaires peuvent être saisis avec une mise en forme. Cette option n’est pas cochée par défaut.

* **Supprimer les commentaires** Si cette option est cochée, les utilisateurs sont autorisés à supprimer leurs propres commentaires. Cette option est cochée par défaut.

* **Autoriser le balisage** Si cette option est cochée, une balise peut être ajoutée au fichier. Cette option n’est pas cochée par défaut.

* **Espaces de noms** autorisés Si l’option Autoriser le balisage est cochée, les balises disponibles seront limitées aux espaces de noms cochés. Si aucun n&#39;est coché, tous sont autorisés. Par défaut, tous les espaces de noms sont autorisés.

* **Limite de suggestions** Si l’option Autoriser le balisage est sélectionnée, ce paramètre limite le nombre de balises suggérées à afficher. Si la valeur est -1, il n’existe aucune limite. La valeur par défaut est -1.

* **Autoriser le vote** Si cette option est cochée, la possibilité d’élire un fichier sera activée. Cette option n’est pas cochée par défaut.

* **Autoriser le suivi** Si cette option est cochée, incluez la fonctionnalité suivante pour les articles de blog, ce qui permet aux membres d’être [informés](/help/communities/notifications.md) des nouvelles publications. Cette option n’est pas cochée par défaut.

* **Activez la mention** Si elle est activée, permet aux utilisateurs enregistrés de la communauté d’identifier d’autres membres enregistrés (à l’aide du prénom, du nom de famille, du nom d’utilisateur) et de les baliser à l’aide de la syntaxe @user-name courante. Les utilisateurs balisés reçoivent des notifications concernant leurs mentions.

* **Mentions** maximales Limitez le nombre maximum de mentions autorisées dans une publication. La valeur par défaut est 10.

* **Modèle** de mention d’interface utilisateur Spécifiez la chaîne de modèle autorisée à baliser (@mentions) l’utilisateur enregistré dans une publication. Par exemple ~{{familyName}}{{donnname}}.

* **Autoriser les réponses** liées Si cette option est cochée, autoriser les réponses aux commentaires publiés. Cette option n’est pas cochée par défaut.

#### Onglet Modération utilisateur {#user-moderation-tab}

Dans l’onglet **Modération d’utilisateur**, configurez la modération des commentaires, si les commentaires sont autorisés :

* **Prémodération** Si cette option est activée, les commentaires doivent être approuvés pour être visibles sur un site de publication. Cette option n’est pas cochée par défaut.

* **Supprimer les commentaires** Si cette option est activée, le visiteur qui a publié le commentaire a le droit de le supprimer. Cette option est cochée par défaut.

* **Refuser les commentaires** Si cette option est activée, les modérateurs de membre approuvés ont le droit de refuser des commentaires. Cette option n’est pas cochée par défaut.

* **Fermer/rouvrir les commentaires** Si cette option est activée, les modérateurs de membre approuvés sont autorisés à fermer et à rouvrir les commentaires. Cette option n’est pas cochée par défaut.

* **Marquer les commentaires** Si cette option est activée, les visiteurs ont le droit de marquer des commentaires comme étant inappropriés. Cette option n’est pas cochée par défaut.

* **Marquer la liste de motifs** Si cette option est activée, les visiteurs ont le droit de sélectionner dans une liste déroulante la ou les raisons pour lesquelles ils ont marqué un commentaire comme étant inapproprié. Cette option n’est pas cochée par défaut.

* **Motif de la marque personnalisée** Si cette option est activée, les visiteurs ont le droit de préciser la raison pour laquelle ils ont marqué un commentaire comme étant inapproprié. Cette option n’est pas cochée par défaut.

* **Seuil de modération** Saisissez le nombre de fois qu’un commentaire doit être marqué par les visiteurs avant que les modérateurs n’en soient informés. La valeur par défaut est une fois (**1**).

* **Limite de marquage** Saisissez le nombre de fois qu’un commentaire doit être marqué avant qu’il ne soit plus visible pour le public. Dans le cas contraire, cette valeur doit être supérieure ou égale au **seuil de modération**. La valeur par défaut est 5.

### Onglet Paramètres de tri {#sort-settings-tab}

Trier par

Définir par défaut

### Informations supplémentaires {#additional-information}

More information may be found on the [File Library Essentials](/help/communities/essentials-file-library.md) page for developers.

Pour des informations sur la modération des sujets et des commentaires publiés, reportez-vous à la section [Modération du contenu généré par l’utilisateur](/help/communities/moderate-ugc.md).

Pour baliser les sujets et les commentaires publiés, voir [Balisage de contenu généré par l’utilisateur](/help/communities/tag-ugc.md).
