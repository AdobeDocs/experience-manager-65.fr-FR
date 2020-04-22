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
source-git-commit: 58a06c1a16c62bffad2893fbec0b32d2ce7267a7

---


# Fonction Forum{#forum-feature}

## Présentation {#introduction}

La fonction Forum offre un espace aux visiteurs connectés (membres de la communauté) dans l’environnement de publication pour leur permettre de :

* Création de nouvelles rubriques
*  et répondre à des sujets
* Suivre une rubrique
* Rechercher un forum
* Aider à modérer le contenu du forum
* Déplacement des rubriques de forum d’une page vers une autre

Cette section de la documentation décrit:

* Ajout de la fonctionnalité de forum à un site AEM.
* Configuration settings for the `Forum`component.

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

Sous l’onglet **Paramètres**, spécifiez les paramètres des sujets et des réponses :

* **Autoriser les miniatures de pièces jointes**

   Si cette option est cochée, une miniature de l’image jointe est créée.

* **Taille max. des miniatures de pièces jointes**

   Taille maximale (en pixels) de l’image miniature de la pièce jointe. La valeur par défaut est 800 x 800.

* **Taille d’image min. pour la miniature**
* **Taille maximale de la miniature**

   Taille maximale (en pixels) de l’image miniature pour l’image intégrée. La valeur par défaut est 800 x 800.

* **Sujets par page**

   Définit le nombre de sujets/publications par page. La valeur par défaut est 10.

* **Modéré**

   Si cette option est cochée, la publication des sujets et des commentaires doit être approuvée avant qu’ils ne s’affichent sur un site de publication. Cette option n’est pas cochée par défaut.

* **Fermé**

   Si cette option est cochée, le forum est fermé aux nouveaux sujets et commentaires. Cette option n’est pas cochée par défaut.

* **Éditeur de texte enrichi**

   Si cette option est cochée, les rubriques et les commentaires peuvent être saisis avec une annotation. Cette option n’est pas cochée par défaut.

* **Autoriser le balisage**

   If checked, allow members to add tag labels to their post (see **Tag field** tab). Cette option n’est pas cochée par défaut.

* **Autoriser les transferts de fichiers**

   Si cette option est cochée, autorisez l’ajout de pièces jointes à la rubrique ou au commentaire. Cette option n’est pas cochée par défaut.

* **Autoriser abonnement**

   Si cette option est cochée, incluez la fonctionnalité suivante pour les publications de forum, ce qui permet aux membres d’être [informés](/help/communities/notifications.md) des nouvelles publications. Cette option n’est pas cochée par défaut.

* **Autoriser l’épinglage**

   Si cette option est cochée, les sujets du forum peuvent être épinglés en haut du  des sujets. Cette option n’est pas cochée par défaut.

* **Autoriser le contenu proposé**

   Si cette option est cochée, l’idée peut être identifiée comme contenu [](/help/communities/featured.md)incitatif. Cette option n’est pas cochée par défaut.

* **Autoriser les abonnements par courrier électronique**

   Si cette option est cochée, autorisez les membres à être informés des nouvelles publications par courrier électronique ([](/help/communities/subscriptions.md)). Requiert `Allow Following` la vérification et la configuration [du](/help/communities/email.md)courrier électronique. Cette option n’est pas cochée par défaut.

* **Taille maximale du fichier**

   N’est pertinent que si `Allow File Uploads` est coché. Ce champ limite la taille (en octets) d’un fichier chargé. La valeur par défaut est 1 048 57 600 (10 Mo).

* **Types de fichier autorisés**

   N’est pertinent que si `Allow File Uploads` est coché. d’extensions de fichier séparé par des virgules avec le séparateur &quot;point&quot;. Par exemple : .jpg, .jpeg, .png, .doc, .docx, .pdf. Si des types de fichier sont spécifiés, ceux qui ne sont pas spécifiés ne seront pas autorisés à être téléchargés. Par défaut, aucun type de fichier n’est spécifié, de sorte que tous les types de fichier soient autorisés.

* **Taille** max. du fichier image joint pertinent uniquement si l’option Autoriser les téléchargements de fichiers est cochée. Taille maximale en octets pour un fichier image chargé. La valeur par défaut est 2097152 (2 Mo).

* **Autoriser les réponses à thème**

   Si cette option est cochée, autorisez les réponses aux commentaires publiés sur la rubrique. Cette option n’est pas cochée par défaut.

* **Autoriser le vote**

   Si cette option est cochée, incluez la fonction de vote dans une rubrique. Cette option n’est pas cochée par défaut.

* **Autoriser les utilisateurs à supprimer les commentaires et sujets**

   Si cette option est cochée, autorisez les membres à supprimer les commentaires et les sujets qu’ils ont publiés. Cette option n’est pas cochée par défaut.

* **Afficher le fil d’Ariane**

   Si cette option est cochée, affichez les chemins de navigation dans les pages de rubrique. Cette option est cochée par défaut.

* **Afficher les badges**

   Si cette option est cochée, affichez les [badges](/help/communities/implementing-scoring.md) gagnés et attribués avec l&#39;entrée de blog d&#39;un membre. Cette option n’est pas cochée par défaut.

* **Autoriser les membres privilégiés**

   Si cette option est cochée, seuls les membres privilégiés sont autorisés à créer du contenu.

* **Membres privilégiés autorisés**

   Ajouter les membres privilégiés sont autorisés à créer du contenu.

* **Bloquer le contenu généré par l’utilisateur en mode d’édition d’auteur**

   S’il est activé, bloque le contenu généré par l’utilisateur lors de la modification en mode Auteur.

* **Activer la mention**

   S’il est activé, permet aux utilisateurs enregistrés de la communauté d’identifier d’autres membres enregistrés (à l’aide du prénom, du nom de famille, du nom d’utilisateur) et de les baliser à l’aide de la syntaxe @user-name courante. Les utilisateurs balisés reçoivent des notifications concernant leurs mentions.

* **Nombre max. de mentions**

   Limitez le nombre maximum de mentions autorisées dans une publication. La valeur par défaut est 10.

* **Modèle des mentions de l’IU**

   Spécifiez la chaîne de modèle autorisée à baliser (@mentions) l’utilisateur enregistré dans une publication. Par exemple, `~{{familyName}}{{givenName}}`.

>[!NOTE]
>
>Il peut s’avérer nécessaire de vérifier `AllowThreaded Replies` et `Allow users to Delete Comments and Topics` d’activer les commentaires sur un sujet.


#### Onglet Modération utilisateur {#user-moderation-tab}

Under the **User Moderation** tab, specify how the posted topics and replies (user generated content) are managed. Pour plus d’informations, voir [Modération de contenu généré par les utilisateurs](/help/communities/moderate-ugc.md).

* **Refuser les publications**

   Si cette option est cochée, les modérateurs membres de confiance seront autorisés à refuser les publications et à empêcher leur publication de s’afficher sur le forum public. Cette option n’est pas cochée par défaut.

* **Fermer/rouvrir les sujets**

   Si cette option est cochée, les modérateurs de membres de confiance peuvent fermer une rubrique pour apporter d’autres modifications et commentaires et rouvrir une rubrique. Cette option n’est pas cochée par défaut.

* **Déplacer les rubriques**

   Si cette option est cochée, autorisez les modérateurs côté publication à déplacer les rubriques. Cette option est cochée par défaut.

* **Marquer les publications**

   Si cette option est cochée, autorisez les membres à signaler les sujets ou commentaires d’autres personnes comme inappropriés. Cette option n’est pas cochée par défaut.

* **Marquer la liste de motifs**

   Si cette option est cochée, permettez aux membres de choisir, dans un  déroulant, la raison pour laquelle ils signalent une rubrique ou un commentaire comme inapproprié. Cette option n’est pas cochée par défaut.

* **Motif de la marque personnalisée**

   Si cette option est cochée, autorisez les membres à entrer leur propre raison de signaler une rubrique ou un commentaire comme étant inapproprié. Cette option n’est pas cochée par défaut.

* **Seuil de modération**

   Entrez le nombre de fois où une rubrique ou un commentaire doit être marqué par les membres avant que les modérateurs ne soient avertis. La valeur par défaut est 1 (une fois).

* **Limite de marquage**

   Entrez le nombre de fois où une rubrique ou un commentaire doit être marqué avant d’être masqué dans les  publics. Si la valeur est -1, le sujet ou le commentaire marqué est toujours visible pour le public. Dans le cas contraire, cette valeur doit être supérieure ou égale au seuil de modération. La valeur par défaut est 5.

#### Onglet Champ de balise {#tag-field-tab}

Dans l’onglet **Champ de balise**, les balises qui peuvent être appliquées, si l’option est activée dans l’onglet **Paramètres**, sont limitées selon les espaces de noms sélectionnés.

* **Espaces de noms autorisés**

   Pertinente si `Allow Tagging` est cochée sous l’onglet **Paramètres** . Les balises pouvant être appliquées se limitent à celles liées aux catégories d’espace de noms cochées. Le de  inclut les balises standard (le par défaut) ainsi que l’option Inclure toutes les balises. La valeur par défaut n’est pas cochée, ce qui signifie que tous les  de  sont autorisés.

* **Limite de suggestions**

   Entrez le nombre de balises à afficher comme suggestion au membre qui publie sur le forum. La valeur par défaut est **-**1 (aucune limite).

#### Onglet Traduction {#translation-tab}

Sous l’onglet **Traduction**, si la traduction est activée pour le site de la communauté, elle peut être définie de sorte à traduire le sujet entier ou certaines publications en particulier.

* **Tout traduire**

   Si cette option est cochée, le fil du forum est traduit dans la langue préférée de l’utilisateur. Cette option n’est pas cochée par défaut.

#### Onglet Paramètres de tri {#sort-settings-tab}

Sous l’onglet Paramètres **de** tri, spécifiez le mode de tri des commentaires publiés lorsqu’ils sont affichés.

* **Trier par**

   Vérifiez toutes les sélections de tri autorisées : `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. La valeur par défaut est `Newest, Oldest, Last Updated`.

* **Définir par défaut**

   Appuyez sur la touche Bas pour sélectionner l’une des options de tri cochées et l’afficher comme valeur par défaut. La valeur par défaut est `Newest`.

* **Sélectionner les options de temps pour le tri Analytics**

   Tirez vers le bas pour sélectionner l’un des `All, Last 24 Hours, Last 7 Days, Last 30 Days`. La valeur par défaut est `All`.

### Informations supplémentaires {#additional-information}

Pour plus d’informations, reportez-vous à la page [Notions fondamentales sur la fonction Forum](/help/communities/essentials-forum.md) pour les développeurs.

Pour des informations sur la modération des sujets et des commentaires publiés, reportez-vous à la section [Modération du contenu généré par l’utilisateur](/help/communities/moderate-ugc.md).

Pour baliser les sujets et les commentaires publiés, voir [Balisage de contenu généré par l’utilisateur](/help/communities/tag-ugc.md).

Pour des informations sur la traduction des sujets et des commentaires, voir [Traduction de contenu généré par les utilisateurs](/help/communities/translate-ugc.md).
