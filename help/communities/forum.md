---
title: Fonctionnalité du forum
description: Découvrez comment ajouter et configurer la fonction de forum qui fournit une zone dans laquelle les membres de la communauté connectés peuvent créer, afficher, suivre, rechercher ou répondre aux rubriques.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 2b1a4917-9db6-436a-a5fd-c102fe41fb9d
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1233'
ht-degree: 2%

---

# Fonctionnalité du forum{#forum-feature}

## Présentation {#introduction}

La fonction de forum fournit une zone pour les visiteurs connectés du site (membres de la communauté) dans l’environnement Publish afin que :

* Création de rubriques
* Affichage des rubriques et réponse
* Suivre une rubrique
* Recherche d’un forum
* Aider à modérer le contenu du forum
* Déplacement des sujets de forum d’une page vers une autre

Cette section de la documentation décrit :

* Ajout de la fonction Forum à un site AEM.
* Paramètres de configuration du composant `Forum`.

### Ajout d’un forum à une page {#adding-a-forum-to-a-page}

Pour ajouter un composant `Forum` à une page en mode création, utilisez l’explorateur de composants pour accéder à :

* `Communities / Forum`

Et faites-le glisser sur la page où le forum doit apparaître.

Pour plus d’informations, consultez la page [Principes de base des composants Communities](/help/communities/basics.md).

Lorsque les [bibliothèques côté client demandées](/help/communities/essentials-forum.md#essentials-for-client-side) sont incluses, voici comment le composant `Forum` apparaît :

![forum-component](assets/forum-component.png)

### Configuration d’un forum {#configuring-a-forum}

Sélectionnez le composant `Forum` inséré afin que vous puissiez accéder à l’icône `Configure` qui ouvre la boîte de dialogue de modification.

![configure-new](assets/configure-new.png)

![forum-config](assets/forum-config.png)

#### Onglet Paramètres {#settings-tab}

Sous l’onglet **Paramètres** , spécifiez les paramètres des sujets et des réponses :

* **Autoriser la miniature des pièces jointes**

  Si cette case est cochée, une miniature de l’image jointe est créée.

* **Taille max. de la miniature de la pièce jointe**

  Taille maximale (en pixels) de la miniature de la pièce jointe. La valeur par défaut est 800 x 800.

* **Taille d’image min. pour la miniature**
* **Taille max. de miniature**

  Taille maximale (en pixels) de la miniature de l’image intégrée. La valeur par défaut est 800 x 800.

* **Sujets par page**

  Définit le nombre de sujets/publications par page. La valeur par défaut est 10.

* **Modéré**

  Si cette case est cochée, la publication des sujets et des commentaires doit être approuvée avant de pouvoir apparaître sur un site de publication. La case par défaut est décochée.

* **Fermé**

  Si cette case est cochée, le forum est fermé pour de nouveaux sujets et commentaires. La case par défaut est décochée.

* **Éditeur de texte enrichi**

  Si cette case est cochée, les sujets et les commentaires peuvent être saisis avec une annotation. La case par défaut est décochée.

* **Autoriser le balisage**

  Si cette case est cochée, les membres ont le droit d’ajouter des libellés de balise à leurs publications (voir l’onglet **Champ de balise** ). La case par défaut est décochée.

* **Autoriser les chargements de fichiers**

  Si cette case est cochée, vous pouvez ajouter des pièces jointes à la rubrique ou au commentaire. La case par défaut est décochée.

* **Autoriser l’abonnement**

  Si cette case est cochée, incluez la fonction suivante pour les publications de forum, ce qui permet aux membres d’être [informés](/help/communities/notifications.md) des nouvelles publications. La case par défaut est décochée.

* **Autoriser la mise en classe**

  Si cette case est cochée, les sujets de forum peuvent être placés en haut de la liste des sujets. La case par défaut est décochée.

* **Autoriser le contenu en vedette**

  Si cette case est cochée, l’idée est identifiable en tant que [contenu présenté](/help/communities/featured.md). La case par défaut est décochée.

* **Autoriser les abonnements aux emails**

  Si cette case est cochée, autorisez les membres à être informés des nouvelles publications par e-mail ([subscription](/help/communities/subscriptions.md)). Nécessite `Allow Following` à vérifier et [email configuré](/help/communities/email.md). La case par défaut est décochée.

* **Taille de fichier max.**

  Pertinent uniquement si `Allow File Uploads` est coché. Ce champ limite la taille (en octets) d’un fichier chargé. La valeur par défaut est 104857600 (10 Mo).

* **Types de fichiers autorisés**

  Pertinent uniquement si `Allow File Uploads` est coché. Liste d’extensions de fichier séparées par des virgules avec le séparateur &quot;point&quot;. Par exemple, .jpg, .jpeg, .png, .doc, .docx, .pdf. Si des types de fichiers sont spécifiés, ceux qui ne sont pas spécifiés ne peuvent pas être chargés. Par défaut, aucun n’est spécifié, de sorte que tous les types de fichiers soient autorisés.

* **Taille max. du fichier image joint**
À définir uniquement si l’option Autoriser les chargements de fichiers est cochée. Nombre maximal d’octets qu’un fichier image chargé peut contenir. La valeur par défaut est 2097152 (2 Mo).

* **Autoriser les réponses à threads**

  Si cette case est cochée, les réponses aux commentaires sont publiées sur le sujet. La case par défaut est décochée.

* **Autoriser le vote**

  Si cette case est cochée, la fonction de vote est ajoutée à un sujet. La case par défaut est décochée.

* **Autoriser les utilisateurs à supprimer des commentaires et des sujets**

  Si cette case est cochée, autorisez les membres à supprimer les commentaires et les sujets qu’ils ont publiés. La case par défaut est décochée.

* **Afficher le chemin de navigation**

  Si cette case est cochée, les chemins de navigation s’affichent sur les pages de rubrique. La valeur par défaut est cochée.

* **Badges d’affichage**

  Si cette case est cochée, affichez les [badges](/help/communities/implementing-scoring.md) gagnés et attribués avec l’entrée de blog d’un membre. La case par défaut est décochée.

* **Autoriser les membres privilégiés**

  Si cette case est cochée, seuls les membres privilégiés sont autorisés à créer du contenu.

* **Membres autorisés**

  Ajoutez les membres privilégiés autorisés à créer du contenu.

* **Bloquer le contenu généré par l’utilisateur en mode d’édition de l’auteur**

  S’il est activé, bloque le contenu généré par l’utilisateur lors de la modification en mode création.

* **Activer la mention**

  S’il est activé, permet aux utilisateurs enregistrés de la communauté d’identifier d’autres membres enregistrés (à l’aide du prénom, du nom, du nom d’utilisateur) et de les baliser à l’aide de la syntaxe @user-name courante. Les utilisateurs balisés reçoivent des notifications sur leurs mentions.

* **Nombre maximal de mentions**

  Limitez le nombre maximal de mentions autorisées dans une publication. La valeur par défaut est 10.

* **Modèle de mention d’interface utilisateur**

  Spécifiez la chaîne de modèle autorisée à baliser (@mention) l’utilisateur enregistré dans une publication. Par exemple, `~{{familyName}}{{givenName}}`.

>[!NOTE]
>
>Il peut être nécessaire de vérifier `AllowThreaded Replies` et `Allow users to Delete Comments and Topics` pour activer les commentaires sur un sujet.

#### Onglet Modération d’utilisateur {#user-moderation-tab}

Sous l’onglet **Modération d’utilisateur** , spécifiez la manière dont les sujets et réponses publiés (contenu généré par l’utilisateur) sont gérés. Pour plus d’informations, voir [Modération de contenu généré par l’utilisateur](/help/communities/moderate-ugc.md).

* **Refuser des publications**

  Si cette case est cochée, les modérateurs membres approuvés sont autorisés à refuser des publications et à empêcher que la publication ne s’affiche sur le forum public. La case par défaut est décochée.

* **Fermer/rouvrir les rubriques**

  Si cette case est cochée, les membres modérateurs autorisés peuvent fermer une rubrique pour ajouter d’autres modifications et commentaires et rouvrir une rubrique. La case par défaut est décochée.

* **Déplacer des rubriques**

  Si cette case est cochée, les modérateurs du côté publication peuvent déplacer les rubriques. La valeur par défaut est cochée.

* **Marquer les publications**

  Si cette case est cochée, les membres ont le droit de marquer les sujets ou commentaires d’autres personnes comme étant inappropriés. La case par défaut est décochée.

* **Liste des motifs de l’indicateur**

  Si cette case est cochée, les membres ont le droit de choisir dans une liste déroulante la raison pour laquelle ils ont marqué un sujet ou un commentaire comme étant inapproprié. La case par défaut est décochée.

* **Motif d’indicateur personnalisé**

  Si cette case est cochée, autorisez les membres à indiquer leur propre raison de signaler un sujet ou un commentaire comme étant inapproprié. La case par défaut est décochée.

* **Seuil de modération**

  Saisissez le nombre de fois qu’un sujet ou un commentaire doit être marqué par les membres avant que les modérateurs ne soient informés. La valeur par défaut est 1 (une fois).

* **Limite de marquage**

  Saisissez le nombre de fois qu’un sujet ou un commentaire doit être marqué avant qu’il ne soit plus visible pour le public. S’il est défini sur -1, le sujet ou le commentaire marqué n’est jamais masqué à la vue du public. Sinon, ce nombre doit être supérieur ou égal au seuil de modération. La valeur par défaut est 5.

#### Onglet Champ de balise {#tag-field-tab}

Sous l’onglet **Champ de balise** , les balises qui peuvent être appliquées, si elles sont autorisées sous l’onglet **Paramètres**, sont limitées en fonction des espaces de noms sélectionnés.

* **Espaces de noms autorisés**

  Pertinent si `Allow Tagging` est coché sous l’onglet **Paramètres**. Les balises qui peuvent être appliquées sont limitées aux catégories d’espace de noms cochées. La liste des espaces de noms inclut &quot;Balises standard&quot; (espace de noms par défaut) et &quot;Inclure toutes les balises&quot;. La valeur par défaut n’est pas cochée, ce qui signifie que tous les espaces de noms sont autorisés.

* **Limite de suggestion**

  Saisissez le nombre de balises à afficher comme suggestion au membre qui publie sur le forum. La valeur par défaut est **-**1 (aucune limite).

#### Onglet Traduction {#translation-tab}

Sous l’onglet **Traduction**, si la traduction est activée pour le site de la communauté, la traduction peut être définie pour traduire l’intégralité du sujet ou les publications sélectionnées.

* **Traduire tout**

  Si cette case est cochée, le fil du forum est traduit dans la langue préférée de l’utilisateur. La case par défaut est décochée.

#### Onglet Paramètres de tri {#sort-settings-tab}

Sous l’onglet **Paramètres de tri**, indiquez comment les commentaires publiés sont triés lorsqu’ils sont affichés.

* **Trier Par**

  Cochez toutes les sélections de tri autorisées : `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. La valeur par défaut est `Newest, Oldest, Last Updated`.

* **Défini comme valeur par défaut**

  Extrayez pour sélectionner l’une des options de tri cochées à afficher par défaut. La valeur par défaut est `Newest`.

* **Sélectionner les options d’heure pour le tri Analytics**

  Effectuez un zoom vers le bas pour sélectionner l’une des options suivantes : `All, Last 24 Hours, Last 7 Days, Last 30 Days`.

  La valeur par défaut est `All`.

### Informations supplémentaires {#additional-information}

Vous trouverez plus d’informations sur la page [Notions fondamentales sur le forum](/help/communities/essentials-forum.md) pour les développeurs.

Pour la modération des sujets et des commentaires publiés, voir [Modération de contenu généré par l’utilisateur](/help/communities/moderate-ugc.md).

Pour baliser les rubriques et commentaires publiés, voir [Balisage de contenu généré par l’utilisateur](/help/communities/tag-ugc.md).

Pour la traduction des sujets et des commentaires publiés, voir [Traduction de contenu généré par l’utilisateur](/help/communities/translate-ugc.md).
