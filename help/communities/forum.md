---
title: Fonction Forum
seo-title: Fonction Forum
description: Ajout et configuration de la fonction de forum
seo-description: Ajout et configuration de la fonction de forum
uuid: e69be4e1-c9d5-4d51-8e7e-609e5460e378
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: d936cef5-ad76-482d-97bf-c40137185812
docset: aem65
exl-id: 2b1a4917-9db6-436a-a5fd-c102fe41fb9d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1226'
ht-degree: 35%

---

# Fonction Forum{#forum-feature}

## Présentation {#introduction}

La fonction Forum offre un espace aux visiteurs connectés (membres de la communauté) dans l’environnement de publication pour leur permettre de :

* Création de rubriques
* Affichage des rubriques et réponse
* Suivre une rubrique
* Recherche d’un forum
* Aider à modérer le contenu du forum
* Déplacement des sujets de forum d’une page vers une autre

Cette section de la documentation décrit:

* Ajout de la fonction Forum à un site AEM.
* Paramètres de configuration du composant `Forum`.

### Ajout d’un forum à une page {#adding-a-forum-to-a-page}

Pour ajouter un composant `Forum` à une page en mode création, utilisez l’explorateur de composants pour accéder à :

* `Communities / Forum`

et faites glisser le composant sur la page où le forum doit être visible.

Pour plus d’informations, voir [Principes de base des composants des communautés](/help/communities/basics.md).

Lorsque les [bibliothèques côté client requises](/help/communities/essentials-forum.md#essentials-for-client-side) sont incluses, voici comment le composant `Forum` apparaîtra :

![forum-component](assets/forum-component.png)

### Configuration d’un forum {#configuring-a-forum}

Sélectionnez le composant `Forum` inséré pour y accéder et sélectionnez l’icône `Configure` qui ouvre la boîte de dialogue de modification.

![configure-new](assets/configure-new.png)

![forum-config](assets/forum-config.png)

#### Onglet Settings {#settings-tab}

Sous l’onglet **Paramètres**, spécifiez les paramètres des sujets et des réponses :

* **Autoriser les miniatures de pièces jointes**

   Si cette case est cochée, une miniature de l’image jointe est créée.

* **Taille max. des miniatures de pièces jointes**

   Taille maximale (en pixels) de l’image miniature de la pièce jointe. La valeur par défaut est 800 x 800.

* **Taille d’image min. pour la miniature**
* **Taille maximale de la miniature**

   Taille maximale (en pixels) de la miniature de l’image intégrée. La valeur par défaut est 800 x 800.

* **Sujets par page**

   Définit le nombre de sujets/publications par page. La valeur par défaut est 10.

* **Modéré**

   Si cette case est cochée, la publication des sujets et des commentaires doit être approuvée avant d’apparaître sur un site de publication. Cette option n’est pas cochée par défaut.

* **Fermé**

   Si cette case est cochée, le forum est fermé pour de nouveaux sujets et commentaires. Cette option n’est pas cochée par défaut.

* **Éditeur de texte enrichi**

   Si cette case est cochée, les sujets et les commentaires peuvent être saisis avec une annotation. Cette option n’est pas cochée par défaut.

* **Autoriser le balisage**

   Si cette case est cochée, les membres ont le droit d’ajouter des libellés de balise à leur publication (voir l’onglet **Champ de balise** ). Cette option n’est pas cochée par défaut.

* **Autoriser les transferts de fichiers**

   Si cette case est cochée, vous pouvez ajouter des pièces jointes à la rubrique ou au commentaire. Cette option n’est pas cochée par défaut.

* **Autoriser abonnement**

   Si cette case est cochée, incluez la fonction suivante pour les publications de forum, ce qui permet aux membres d’être [informés](/help/communities/notifications.md) des nouvelles publications. Cette option n’est pas cochée par défaut.

* **Autoriser l’épinglage**

   Si cette case est cochée, les sujets de forum peuvent être placés en haut de la liste des sujets. Cette option n’est pas cochée par défaut.

* **Autoriser le contenu proposé**

   Si cette option est cochée, l’idée peut être identifiée en tant que [contenu présenté](/help/communities/featured.md). Cette option n’est pas cochée par défaut.

* **Autoriser les abonnements par courrier électronique**

   Si cette case est cochée, autorisez les membres à être informés des nouvelles publications par e-mail ([subscription](/help/communities/subscriptions.md)). `Allow Following` doit être vérifié et [email configuré](/help/communities/email.md). Cette option n’est pas cochée par défaut.

* **Taille maximale du fichier**

   Convient uniquement si `Allow File Uploads` est coché. Ce champ limite la taille (en octets) d’un fichier chargé. La valeur par défaut est 104857600 (10 Mo).

* **Types de fichier autorisés**

   Convient uniquement si `Allow File Uploads` est coché. Liste d’extensions de fichier séparées par des virgules avec le séparateur &quot;point&quot;. Par exemple : .jpg, .jpeg, .png, .doc, .docx, .pdf. Si des types de fichiers sont spécifiés, ceux qui ne sont pas spécifiés ne seront pas autorisés à être chargés. Par défaut, aucun n’est spécifié, de sorte que tous les types de fichiers soient autorisés.

* **Max Attach Image File**
SizeRelevant uniquement si l’option Autoriser les chargements de fichiers est cochée. Taille maximale en octets pour un fichier image chargé. La valeur par défaut est 2097152 (2 Mo).

* **Autoriser les réponses à thème**

   Si cette case est cochée, les réponses aux commentaires sont publiées sur le sujet. Cette option n’est pas cochée par défaut.

* **Autoriser le vote**

   Si cette case est cochée, la fonction de vote est ajoutée à un sujet. Cette option n’est pas cochée par défaut.

* **Autoriser les utilisateurs à supprimer les commentaires et sujets**

   Si cette case est cochée, autorisez les membres à supprimer les commentaires et les sujets qu’ils ont publiés. Cette option n’est pas cochée par défaut.

* **Afficher le fil d’Ariane**

   Si cette case est cochée, les chemins de navigation s’affichent sur les pages de rubrique. Cette option est cochée par défaut.

* **Afficher les badges**

   Si cette case est cochée, affichez les [badges](/help/communities/implementing-scoring.md) gagnés et attribués avec l’entrée de blog d’un membre. Cette option n’est pas cochée par défaut.

* **Autoriser les membres privilégiés**

   Si cette case est cochée, seuls les membres privilégiés sont autorisés à créer du contenu.

* **Membres privilégiés autorisés**

   Ajoutez les membres privilégiés autorisés à créer du contenu.

* **Bloquer le contenu généré par l’utilisateur en mode d’édition d’auteur**

   S’il est activé, bloque le contenu généré par l’utilisateur lors de la modification en mode création.

* **Activer la mention**

   S’il est activé, permet aux utilisateurs enregistrés de la communauté d’identifier d’autres membres enregistrés (à l’aide du prénom, du nom, du nom d’utilisateur) et de les baliser à l’aide de la syntaxe @user-name courante. Les utilisateurs balisés reçoivent des notifications concernant leurs mentions.

* **Nombre max. de mentions**

   Limitez le nombre maximal de mentions autorisées dans une publication. La valeur par défaut est 10.

* **Modèle des mentions de l’IU**

   Spécifiez la chaîne de modèle autorisée à baliser (@mention) l’utilisateur enregistré dans une publication. Par exemple, `~{{familyName}}{{givenName}}`.

>[!NOTE]
>
>Il peut être nécessaire de vérifier `AllowThreaded Replies` et `Allow users to Delete Comments and Topics` pour activer les commentaires sur un sujet.

#### Onglet Modération d’utilisateur {#user-moderation-tab}

Sous l’onglet **Modération d’utilisateur** , indiquez comment les sujets et réponses publiés (contenu généré par l’utilisateur) sont gérés. Pour plus d’informations, voir [Modération de contenu généré par les utilisateurs](/help/communities/moderate-ugc.md).

* **Refuser les publications**

   Si cette case est cochée, les modérateurs membres approuvés sont autorisés à refuser des publications et à empêcher que la publication ne s’affiche sur le forum public. Cette option n’est pas cochée par défaut.

* **Fermer/rouvrir les sujets**

   Si cette case est cochée, les membres modérateurs autorisés peuvent fermer une rubrique pour ajouter d’autres modifications et commentaires et rouvrir une rubrique. Cette option n’est pas cochée par défaut.

* **Déplacer les rubriques**

   Si cette case est cochée, les modérateurs côté publication peuvent déplacer des rubriques. Cette option est cochée par défaut.

* **Marquer les publications**

   Si cette case est cochée, les membres ont le droit de marquer les sujets ou commentaires d’autres personnes comme étant inappropriés. Cette option n’est pas cochée par défaut.

* **Marquer la liste de motifs**

   Si cette case est cochée, les membres ont le droit de choisir dans une liste déroulante la raison pour laquelle ils ont marqué un sujet ou un commentaire comme étant inapproprié. Cette option n’est pas cochée par défaut.

* **Motif de la marque personnalisée**

   Si cette case est cochée, autorisez les membres à indiquer leur propre motif de signalement d’un sujet ou d’un commentaire comme étant inapproprié. Cette option n’est pas cochée par défaut.

* **Seuil de modération**

   Saisissez le nombre de fois qu’un sujet ou un commentaire doit être marqué par les membres avant que les modérateurs ne soient informés. La valeur par défaut est 1 (une fois).

* **Limite de marquage**

   Saisissez le nombre de fois qu’un sujet ou un commentaire doit être marqué avant qu’il ne soit plus visible pour le public. Si la valeur est -1, le sujet ou le commentaire marqué est toujours visible pour le public. Dans le cas contraire, cette valeur doit être supérieure ou égale au seuil de modération. La valeur par défaut est 5.

#### Onglet Champ de balise {#tag-field-tab}

Dans l’onglet **Champ de balise**, les balises qui peuvent être appliquées, si l’option est activée dans l’onglet **Paramètres**, sont limitées selon les espaces de noms sélectionnés.

* **Espaces de noms autorisés**

   Convient si `Allow Tagging` est coché sous l’onglet **Paramètres**. Les balises pouvant être appliquées se limitent à celles liées aux catégories d’espace de noms cochées. La liste des espaces de noms inclut &quot;Balises standard&quot; (l’espace de noms par défaut) ainsi que &quot;Inclure toutes les balises&quot;. La valeur par défaut n’est pas cochée, ce qui signifie que tous les espaces de noms sont autorisés.

* **Limite de suggestions**

   Saisissez le nombre de balises à afficher comme suggestion au membre qui publie sur le forum. La valeur par défaut est **-**1 (aucune limite).

#### Onglet Traduction {#translation-tab}

Sous l’onglet **Traduction**, si la traduction est activée pour le site de la communauté, elle peut être définie de sorte à traduire le sujet entier ou certaines publications en particulier.

* **Tout traduire**

   Si cette case est cochée, le fil du forum est traduit dans la langue préférée de l’utilisateur. Cette option n’est pas cochée par défaut.

#### Onglet Paramètres de tri {#sort-settings-tab}

Sous l’onglet **Paramètres de tri**, indiquez comment les commentaires publiés sont triés lorsqu’ils sont affichés.

* **Trier par**

   Cochez toutes les sélections de tri autorisées : `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. La valeur par défaut est `Newest, Oldest, Last Updated`.

* **Définir par défaut**

   Extrayez pour sélectionner l’une des options de tri cochées à afficher par défaut. La valeur par défaut est `Newest`.

* **Sélectionner les options de temps pour le tri Analytics**

   Faites glisser le curseur pour sélectionner l’une des options suivantes : `All, Last 24 Hours, Last 7 Days, Last 30 Days`.

   La valeur par défaut est `All`.

### Informations supplémentaires {#additional-information}

Pour plus d’informations, reportez-vous à la page [Notions fondamentales sur la fonction Forum](/help/communities/essentials-forum.md) pour les développeurs.

Pour des informations sur la modération des sujets et des commentaires publiés, reportez-vous à la section [Modération du contenu généré par l’utilisateur](/help/communities/moderate-ugc.md).

Pour baliser les sujets et les commentaires publiés, voir [Balisage de contenu généré par l’utilisateur](/help/communities/tag-ugc.md).

Pour des informations sur la traduction des sujets et des commentaires, voir [Traduction de contenu généré par les utilisateurs](/help/communities/translate-ugc.md).
