---
title: Fonction Forum
seo-title: Fonction Forum
description: Comment ajouter et configurer la fonction du forum
seo-description: Comment ajouter et configurer la fonction du forum
uuid: e69be4e1-c9d5-4d51-8e7e-609e5460e378
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: d936cef5-ad76-482d-97bf-c40137185812
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Fonction Forum{#forum-feature}

## Présentation {#introduction}

La fonction Forum offre un espace aux visiteurs connectés (membres de la communauté) dans l’environnement de publication pour leur permettre de :

* créer des sujets ;
* visualiser et répondre à des sujets ;
* suivre un sujet ;
* effectuer une recherche dans un forum ;
* aider à modérer le contenu du forum ;
* déplacer des sujets du forum d’une page à une autre.

Cette section de la documentation décrit :

* l’ajout de la fonction Forum à un site AEM ;
* les paramètres de configuration du composant `Forum`.

### Ajout d’un forum à une page {#adding-a-forum-to-a-page}

To add a `Forum` component to a page in author mode, use the component browser to locate

* `Communities / Forum`

et faites glisser le composant sur la page où le forum doit être visible.

For necessary information, visit [Communities Components Basics](/help/communities/basics.md).

When the [required client-side libraries](/help/communities/essentials-forum.md#essentials-for-client-side) are included, this is how the `Forum`component will appear :

![chlimage_1-104](assets/chlimage_1-104.png)

### Configuration d’un forum {#configuring-a-forum}

Select the placed `Forum` component to access and select the `Configure` icon which opens the edit dialog.

![chlimage_1-105](assets/chlimage_1-105.png) ![forum-config](assets/forum-config.png)

#### Onglet Settings {#settings-tab}

Sous l’onglet **Paramètres **, spécifiez les paramètres des rubriques et des réponses :

* **Autoriser la miniature des pièces jointes**Si cette option est cochée, une miniature de l’image jointe est créée.
* **Taille** maximale des vignettes d’attache Taille maximale (en pixels) de l’image miniature de la pièce jointe. La valeur par défaut est 800 x 800.

* **Taille d’image minimale pour la miniature**
* **Taille** maximale des vignettes Taille maximale (en pixels) de l’image miniature pour l’image intégrée. La valeur par défaut est 800 x 800.

* **Rubriques par page**Définit le nombre de rubriques/publications affichées par page. La valeur par défaut est 10.
* **Modéré** Si cette option est cochée, les sujets et les commentaires doivent être approuvés avant d’être visibles sur un site de publication. Cette option n’est pas cochée par défaut.

* **Fermé** Si cette option est cochée, le forum est fermé et n’accepte aucun nouveau sujet ou commentaire. Cette option n’est pas cochée par défaut.

* **Éditeur de texte enrichi** Si cette option est cochée, les sujets et les commentaires peuvent être saisis avec une mise en forme. Cette option n’est pas cochée par défaut.

* **Autoriser le balisage** Si cette option est cochée, les membres ont le droit d’ajouter des libellés de balise à leur article (voir l’onglet **Champ de balise**). Cette option n’est pas cochée par défaut.

* **Autoriser les chargements de fichiers** Si cette option est cochée, des fichiers joints peuvent être ajoutés à un sujet ou à un commentaire. Cette option n’est pas cochée par défaut.

* **Autoriser le suivi** Si coché, incluez la fonctionnalité suivante pour les publications de forum, ce qui permet aux membres d’être [informés](/help/communities/notifications.md) des nouvelles publications. Cette option n’est pas cochée par défaut.

* **Permettre l’épinglage** Si cette option est cochée, les rubriques du forum peuvent être épinglées en haut de la liste des rubriques. Cette option n’est pas cochée par défaut.

* **Si cette option est cochée, l’idée peut être identifiée comme contenu**[](/help/communities/featured.md)phare. Cette option n’est pas cochée par défaut.

* **Autoriser les abonnements** par courrier électronique Si cette option est cochée, autorisez les membres à être avertis des nouvelles publications par courrier électronique ([abonnement](/help/communities/subscriptions.md)). Requiert `Allow Following` la vérification et la configuration [du](/help/communities/email.md)courrier électronique. Cette option n’est pas cochée par défaut.

* **Taille** de fichier maximale pertinente uniquement si `Allow File Uploads` est cochée. Ce champ limite la taille (en octets) d’un fichier chargé. La valeur par défaut est 1 048 57 600 (10 Mo).

* **Types** de fichiers autorisés pertinents uniquement si `Allow File Uploads` l’option est cochée. Liste d’extensions de fichiers séparées par des virgules avec le séparateur &quot;point&quot;. Par exemple : .jpg, .jpeg, .png, .doc, .docx, .pdf. Si des types de fichier sont spécifiés, ceux qui ne sont pas spécifiés ne seront pas autorisés à être téléchargés. La valeur par défaut n’est pas spécifiée, de sorte que** **tous les types de fichier sont autorisés.

* **Taille** max. du fichier image joint, applicable uniquement si l’option Autoriser les téléchargements de fichiers est cochée. Taille maximale en octets pour un fichier image chargé. La valeur par défaut est 2097152** **(2 Mo).

* **Autoriser les réponses à thème** Si cette option est cochée, les réponses aux commentaires sont publiées pour le sujet. Cette option n’est pas cochée par défaut.

* **Autoriser le vote** Si cette option est cochée, la fonction de vote est ajoutée à un sujet. Cette option n’est pas cochée par défaut.

* **Autoriser les utilisateurs à supprimer les commentaires et sujets** Si cette option est cochée, les membres ont le droit de supprimer les commentaires et les sujets qu’ils ont publiés. Cette option n’est pas cochée par défaut.

* **Afficher le fil d’Ariane** Si cette option est cochée, le fil d’Ariane s’affiche dans les pages de sujet. Cette option est cochée par défaut.

* **Afficher les badges** Si coché, afficher les [badges](/help/communities/implementing-scoring.md) gagnés et attribués avec l&#39;entrée de blog d&#39;un membre. Cette option n’est pas cochée par défaut.

* **Autoriser les membres** privilégiés Si cette case est cochée, seuls les membres privilégiés sont autorisés à créer du contenu.

* **Membres privilégiés autorisés**Ajoutez les membres privilégiés autorisés à créer du contenu.
* **Bloquer le contenu généré par l’utilisateur en mode** d’édition Auteur Si cette option est activée, bloque le contenu généré par l’utilisateur lors de la modification en mode Auteur.

* **Activez la mention** Si elle est activée, permet aux utilisateurs enregistrés de la communauté d’identifier d’autres membres enregistrés (à l’aide du prénom, du nom de famille, du nom d’utilisateur) et de les baliser à l’aide de la syntaxe @user-name courante. Les utilisateurs balisés reçoivent des notifications concernant leurs mentions.

* **Mentions** maximales Limitez le nombre maximum de mentions autorisées dans une publication. La valeur par défaut est 10.

* **Modèle** de mention d’interface utilisateur Spécifiez la chaîne de modèle autorisée à baliser (@mentions) l’utilisateur enregistré dans une publication. Par exemple `~{{familyName}}{{givenName}}`.

>[!NOTE]
>
>Il peut s’avérer nécessaire de vérifier `AllowThreaded Replies` et `Allow users to Delete Comments and Topics` d’activer les commentaires sur un sujet.

#### Onglet Modération utilisateur {#user-moderation-tab}

Sous l’onglet **Modération utilisateur **, spécifiez la manière dont les rubriques et réponses publiées (contenu généré par l’utilisateur) sont gérées. Pour plus d’informations, voir [Modération de contenu généré par les utilisateurs](/help/communities/moderate-ugc.md).

* **Refuser les publications** Si cette option est cochée, les membres modérateurs autorisés ont le droit de refuser des articles et, par conséquent, d’empêcher leur publication sur le forum public. Cette option n’est pas cochée par défaut.

* **Fermer/rouvrir les sujets** Si cette option est cochée, les membres modérateurs autorisés ont le droit de fermer un sujet pour empêcher la publication d’autres modifications et de commentaires, puis de le rouvrir. Cette option n’est pas cochée par défaut.

* **Déplacer des rubriques** Si cette option est cochée, autorisez les modérateurs côté publication à déplacer des rubriques. Cette option est cochée par défaut.

* **Marquer les publications** Si cette option est cochée, les membres ont le droit de marquer les sujets ou commentaires d’autres membres comme étant inappropriés. Cette option n’est pas cochée par défaut.

* **Marquer la liste de motifs** Si cette option est cochée, les membres ont le droit de sélectionner dans une liste déroulante la ou les raisons pour lesquelles ils ont marqué un sujet ou un commentaire comme étant inapproprié. Cette option n’est pas cochée par défaut.

* **Motif de la marque personnalisée** Si cette option est cochée, les membres ont le droit de préciser la raison pour laquelle ils ont marqué un sujet ou un commentaire comme étant inapproprié. Cette option n’est pas cochée par défaut.

* **Seuil de modération** Saisissez le nombre de fois qu’un sujet ou un commentaire doit être marqué par les membres avant que les modérateurs n’en soient informés. La valeur par défaut est 1 (une fois).

* **Limite de marquage** Saisissez le nombre de fois qu’un sujet ou un commentaire doit être marqué avant qu’il ne soit plus visible pour le public. Si la valeur est -1, le sujet ou le commentaire marqué est toujours visible pour le public. Dans le cas contraire, cette valeur doit être supérieure ou égale au seuil de modération. La valeur par défaut est 5.

#### Onglet Champ de balise {#tag-field-tab}

Under the **Tag field** tab, the tags which may be applied, if allowed under the **Settings **tab, are limited according to namespaces chosen.

* **Espaces de noms** autorisés Pertinents si `Allow Tagging` est coché sous l’onglet **Paramètres **Paramètres. Les balises pouvant être appliquées se limitent à celles liées aux catégories d’espace de noms cochées. La liste des espaces de noms inclut &quot;Balises standard&quot; (espace de noms par défaut) ainsi que &quot;Inclure toutes les balises&quot;. La valeur par défaut n’est pas cochée, ce qui signifie que tous les espaces de noms sont autorisés.

* **Limite de suggestions** Entrez le nombre de balises à afficher comme suggestion destinée au membre qui publie sur le forum. La valeur par défaut est **-**1 (aucune limite).

#### Onglet Traduction {#translation-tab}

Sous l’onglet **Traduction **, si la traduction est activée pour le site de la communauté, la traduction peut être définie pour traduire l’intégralité du sujet ou des publications sélectionnées.

* **Tout traduire** Si cette option est cochée, le fil d’Ariane du forum est traduit dans la langue par défaut de l’utilisateur. Cette option n’est pas cochée par défaut.

#### Onglet Paramètres de tri {#sort-settings-tab}

Sous l’onglet **Paramètres de tri **, spécifiez le mode de tri des commentaires publiés lorsqu’ils sont affichés.

* **Trier par** Vérifier toutes les sélections de tri autorisées : `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. La valeur par défaut est `Newest, Oldest, Last Updated`.

* **Définissez cette option comme valeur par défaut** Tirez vers le bas pour sélectionner l’une des options de tri cochées à afficher comme valeur par défaut. La valeur par défaut est `Newest`.

* **Sélectionnez Options de temps pour le tri** Analytics. Décompressez pour sélectionner l’une des options `All, Last 24 Hours, Last 7 Days, Last 30 Days`. La valeur par défaut est `All`.

### Informations supplémentaires {#additional-information}

Pour plus d’informations, reportez-vous à la page [Notions fondamentales sur la fonction Forum](/help/communities/essentials-forum.md) pour les développeurs.

Pour des informations sur la modération des sujets et des commentaires publiés, reportez-vous à la section [Modération du contenu généré par l’utilisateur](/help/communities/moderate-ugc.md).

Pour baliser les sujets et les commentaires publiés, voir [Balisage de contenu généré par l’utilisateur](/help/communities/tag-ugc.md).

Pour des informations sur la traduction des sujets et des commentaires, voir [Traduction de contenu généré par les utilisateurs](/help/communities/translate-ugc.md).
