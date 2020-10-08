---
title: Fonction Forum
seo-title: Fonction Forum
description: Comment ajouter et configurer la fonction de forum
seo-description: Comment ajouter et configurer la fonction de forum
uuid: e69be4e1-c9d5-4d51-8e7e-609e5460e378
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: d936cef5-ad76-482d-97bf-c40137185812
docset: aem65
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '1226'
ht-degree: 35%

---


# Fonction Forum{#forum-feature}

## Présentation {#introduction}

La fonction Forum offre un espace aux visiteurs connectés (membres de la communauté) dans l’environnement de publication pour leur permettre de :

* Créer de nouvelles rubriques
* Vue et réponse aux rubriques
* Suivre une rubrique
* Rechercher un forum
* Aider à modérer le contenu du forum
* Déplacement des rubriques de forum d’une page vers une autre

Cette section de la documentation décrit:

* Ajouter la fonction du forum à un site AEM.
* Configuration settings for the `Forum` component.

### Ajout d’un forum à une page {#adding-a-forum-to-a-page}

To add a `Forum` component to a page in author mode, use the component browser to locate

* `Communities / Forum`

et faites glisser le composant sur la page où le forum doit être visible.

For necessary information, visit [Communities Components Basics](/help/communities/basics.md).

When the [required client-side libraries](/help/communities/essentials-forum.md#essentials-for-client-side) are included, this is how the `Forum` component will appear:

![chlimage_1-60](assets/chlimage_1-60.png)

### Configuration d’un forum {#configuring-a-forum}

Select the placed `Forum` component to access and select the `Configure` icon which opens the edit dialog.

![chlimage_1-61](assets/chlimage_1-61.png)

![forum-config](assets/forum-config.png)

#### Onglet Settings {#settings-tab}

Sous l’onglet **Paramètres**, spécifiez les paramètres des sujets et des réponses :

* **Autoriser les miniatures de pièces jointes**

   Si cette option est cochée, une miniature de l’image jointe est créée.

* **Taille max. des miniatures de pièces jointes**

   Taille maximale (en pixels) de l’image miniature de la pièce jointe. La valeur par défaut est 800 x 800.

* **Taille d’image minimale pour la miniature**
* **Taille maximale de la miniature**

   Taille maximale (en pixels) de la vignette de l’image intégrée. La valeur par défaut est 800 x 800.

* **Sujets par page**

   Définit le nombre de sujets/publications par page. La valeur par défaut est 10.

* **Modéré**

   Si cette option est cochée, la publication des sujets et commentaires doit être approuvée avant qu’ils n’apparaissent sur un site de publication. Cette option n’est pas cochée par défaut.

* **Fermé**

   Si cette option est cochée, le forum est fermé aux nouveaux sujets et commentaires. Cette option n’est pas cochée par défaut.

* **Éditeur de texte enrichi**

   Si cette option est cochée, les rubriques et commentaires peuvent être saisis avec une annotation. Cette option n’est pas cochée par défaut.

* **Autoriser le balisage**

   If checked, allow members to add tag labels to their post (see **Tag field** tab). Cette option n’est pas cochée par défaut.

* **Autoriser les transferts de fichiers**

   Si cette option est cochée, autorisez l’ajout de pièces jointes à la rubrique ou au commentaire. Cette option n’est pas cochée par défaut.

* **Autoriser abonnement**

   Si cette option est cochée, incluez la fonction suivante pour les publications de forum, ce qui permet aux membres d’être [informés](/help/communities/notifications.md) des nouvelles publications. Cette option n’est pas cochée par défaut.

* **Autoriser l’épinglage**

   Si cette option est cochée, les sujets du forum peuvent être épinglés en haut de la liste des sujets. Cette option n’est pas cochée par défaut.

* **Autoriser le contenu proposé**

   Si cette option est cochée, l’idée peut être identifiée comme contenu [](/help/communities/featured.md)phare. Cette option n’est pas cochée par défaut.

* **Autoriser les abonnements par courrier électronique**

   Si cette case est cochée, autorisez les membres à être informés des nouvelles publications par courriel ([abonnement](/help/communities/subscriptions.md)). Nécessite `Allow Following` la vérification et la configuration [du](/help/communities/email.md)courrier électronique. Cette option n’est pas cochée par défaut.

* **Taille maximale du fichier**

   Ne s’applique que si `Allow File Uploads` la vérification est effectuée. Ce champ limite la taille (en octets) d’un fichier chargé. La valeur par défaut est 104857600 (10 Mo).

* **Types de fichier autorisés**

   Ne s’applique que si `Allow File Uploads` la vérification est effectuée. Liste séparée par des virgules d’extensions de fichiers avec le séparateur &quot;point&quot;. Par exemple : .jpg, .jpeg, .png, .doc, .docx, .pdf. Si des types de fichier sont spécifiés, ceux qui ne sont pas spécifiés ne seront pas autorisés à être téléchargés. Par défaut, aucun type de fichier n’est spécifié, de sorte que tous les types de fichier soient autorisés.

* **Taille** de fichier d’image de pièce jointe maximale adaptée uniquement si l’option Autoriser les téléchargements de fichiers est cochée. Taille maximale en octets pour un fichier image chargé. La valeur par défaut est 2097152 (2 Mo).

* **Autoriser les réponses à thème**

   Si cette option est cochée, autorisez les réponses aux commentaires publiés sur la rubrique. Cette option n’est pas cochée par défaut.

* **Autoriser le vote**

   Si cette case est cochée, incluez la fonction de vote avec une rubrique. Cette option n’est pas cochée par défaut.

* **Autoriser les utilisateurs à supprimer les commentaires et sujets**

   Si cette option est cochée, autorisez les membres à supprimer les commentaires et les rubriques qu’ils ont publiés. Cette option n’est pas cochée par défaut.

* **Afficher le fil d’Ariane**

   Si cette case est cochée, affichez les chemins de navigation dans les pages de rubrique. Cette option est cochée par défaut.

* **Afficher les badges**

   Si cette option est cochée, affichez les [badges](/help/communities/implementing-scoring.md) gagnés et attribués avec l&#39;entrée de blog d&#39;un membre. Cette option n’est pas cochée par défaut.

* **Autoriser les membres privilégiés**

   Si cette case est cochée, seuls les membres privilégiés sont autorisés à créer du contenu.

* **Membres privilégiés autorisés**

   Ajoutez les membres privilégiés autorisés à créer du contenu.

* **Bloquer le contenu généré par l’utilisateur en mode d’édition d’auteur**

   Si cette option est activée, bloque le contenu généré par l’utilisateur lors de la modification en mode Auteur.

* **Activer la mention**

   S’il est activé, permet aux utilisateurs enregistrés de la communauté d’identifier d’autres membres enregistrés (à l’aide de leur prénom, de leur nom de famille, de leur nom d’utilisateur) et de les baliser à l’aide de la syntaxe courante de @user-name. Les utilisateurs balisés reçoivent des notifications concernant leurs mentions.

* **Nombre max. de mentions**

   Limitez le nombre maximum de mentions autorisées dans une publication. La valeur par défaut est 10.

* **Modèle des mentions de l’IU**

   Spécifiez la chaîne de modèle autorisée à baliser (@mentions) l’utilisateur enregistré dans une publication. Par exemple, `~{{familyName}}{{givenName}}`.

>[!NOTE]
>
>Il peut être nécessaire de vérifier à la fois `AllowThreaded Replies` et `Allow users to Delete Comments and Topics` d&#39;activer les commentaires sur un sujet.

#### Onglet Modération utilisateur {#user-moderation-tab}

Under the **User Moderation** tab, specify how the posted topics and replies (user generated content) are managed. Pour plus d’informations, voir [Modération de contenu généré par les utilisateurs](/help/communities/moderate-ugc.md).

* **Refuser les publications**

   Si cette option est cochée, les modérateurs membres de confiance seront autorisés à refuser les publications et à empêcher que la publication ne s&#39;affiche sur le forum public. Cette option n’est pas cochée par défaut.

* **Fermer/rouvrir les sujets**

   Si cette option est cochée, les modérateurs membres approuvés peuvent fermer une rubrique pour apporter d’autres modifications et commentaires et peuvent également rouvrir une rubrique. Cette option n’est pas cochée par défaut.

* **Déplacer les rubriques**

   Si cette option est cochée, autorisez les modérateurs côté publication à déplacer les rubriques. Cette option est cochée par défaut.

* **Marquer les publications**

   Si cette option est cochée, autorisez les membres à signaler les sujets ou commentaires d&#39;autres personnes comme inappropriés. Cette option n’est pas cochée par défaut.

* **Marquer la liste de motifs**

   Si cette option est cochée, permettez aux membres de choisir, dans une liste déroulante, la raison pour laquelle ils signalent une rubrique ou un commentaire comme inapproprié. Cette option n’est pas cochée par défaut.

* **Motif de la marque personnalisée**

   Si cette option est cochée, autorisez les membres à entrer leur propre raison de signaler une rubrique ou un commentaire comme inapproprié. Cette option n’est pas cochée par défaut.

* **Seuil de modération**

   Indiquez le nombre de fois où une rubrique ou un commentaire doit être marqué par les membres avant que les modérateurs ne soient avertis. La valeur par défaut est 1 (une fois).

* **Limite de marquage**

   Saisissez le nombre de fois où une rubrique ou un commentaire doit être marqué avant d’être masqué dans la vue publique. Si la valeur est -1, le sujet ou le commentaire marqué est toujours visible pour le public. Dans le cas contraire, cette valeur doit être supérieure ou égale au seuil de modération. La valeur par défaut est 5.

#### Onglet Champ de balise {#tag-field-tab}

Dans l’onglet **Champ de balise**, les balises qui peuvent être appliquées, si l’option est activée dans l’onglet **Paramètres**, sont limitées selon les espaces de noms sélectionnés.

* **Espaces de noms autorisés**

   Pertinent si `Allow Tagging` est coché sous l’onglet **Paramètres** . Les balises pouvant être appliquées se limitent à celles liées aux catégories d’espace de noms cochées. La liste des espaces de nommage inclut &quot;Balises standard&quot; (l’espace de nommage par défaut) ainsi que &quot;Inclure toutes les balises&quot;. La valeur par défaut n’est pas cochée, ce qui signifie que tous les espaces de nommage sont autorisés.

* **Limite de suggestions**

   Entrez le nombre de balises à afficher comme suggestion au membre qui publie sur le forum. La valeur par défaut est **-**1 (aucune limite).

#### Onglet Traduction {#translation-tab}

Sous l’onglet **Traduction**, si la traduction est activée pour le site de la communauté, elle peut être définie de sorte à traduire le sujet entier ou certaines publications en particulier.

* **Tout traduire**

   Si cette option est cochée, le fil du forum est traduit dans la langue préférée de l’utilisateur. Cette option n’est pas cochée par défaut.

#### Onglet Paramètres de tri {#sort-settings-tab}

Sous l’onglet Paramètres **de** tri, indiquez comment les commentaires publiés sont triés lorsqu’ils s’affichent.

* **Trier par**

   Cochez toutes les sélections de tri autorisées : `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. La valeur par défaut est `Newest, Oldest, Last Updated`.

* **Définir par défaut**

   Appuyez sur la touche Ctrl pour sélectionner l’une des options de tri cochées pour qu’elle s’affiche par défaut. La valeur par défaut est `Newest`.

* **Sélectionner les options de temps pour le tri Analytics**

   Maintenez la touche enfoncée pour sélectionner l’une des options suivantes : `All, Last 24 Hours, Last 7 Days, Last 30 Days`.

   La valeur par défaut est `All`.

### Informations supplémentaires {#additional-information}

Pour plus d’informations, reportez-vous à la page [Notions fondamentales sur la fonction Forum](/help/communities/essentials-forum.md) pour les développeurs.

Pour des informations sur la modération des sujets et des commentaires publiés, reportez-vous à la section [Modération du contenu généré par l’utilisateur](/help/communities/moderate-ugc.md).

Pour baliser les sujets et les commentaires publiés, voir [Balisage de contenu généré par l’utilisateur](/help/communities/tag-ugc.md).

Pour des informations sur la traduction des sujets et des commentaires, voir [Traduction de contenu généré par les utilisateurs](/help/communities/translate-ugc.md).
