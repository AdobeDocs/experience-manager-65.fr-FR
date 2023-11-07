---
title: Fonctionnalité du forum
description: Découvrez comment ajouter et configurer la fonction de forum qui fournit une zone dans laquelle les membres de la communauté connectés peuvent créer, afficher, suivre, rechercher ou répondre aux rubriques.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 2b1a4917-9db6-436a-a5fd-c102fe41fb9d
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1219'
ht-degree: 10%

---

# Fonctionnalité du forum{#forum-feature}

## Présentation {#introduction}

La fonction de forum fournit une zone pour les visiteurs connectés du site (membres de la communauté) dans l’environnement de publication afin que :

* Création de rubriques
* Affichage des rubriques et réponse
* Suivre une rubrique
* Recherche d’un forum
* Aider à modérer le contenu du forum
* Déplacement des sujets de forum d’une page vers une autre

Cette section de la documentation décrit :

* Ajout de la fonction Forum à un site AEM.
* Paramètres de configuration de la variable `Forum` composant.

### Ajout d’un forum à une page {#adding-a-forum-to-a-page}

Pour ajouter une `Forum` sur une page en mode création, utilisez l’explorateur de composants pour accéder à

* `Communities / Forum`

Et faites-le glisser sur la page où le forum doit apparaître.

Pour obtenir les informations nécessaires, consultez la section [Principes de base des composants des communautés](/help/communities/basics.md).

Lorsque la variable [bibliothèques côté client requises](/help/communities/essentials-forum.md#essentials-for-client-side) sont incluses, c’est ainsi que la variable `Forum` Le composant apparaît :

![forum-component](assets/forum-component.png)

### Configuration d’un forum {#configuring-a-forum}

Sélectionnez le `Forum` afin que vous puissiez accéder au `Configure` qui ouvre la boîte de dialogue de modification.

![configure-new](assets/configure-new.png)

![forum-config](assets/forum-config.png)

#### Onglet Paramètres {#settings-tab}

Sous , **Paramètres** , spécifiez les paramètres des sujets et réponses :

* **Autoriser les miniatures de pièces jointes**

  Si cette case est cochée, une miniature de l’image jointe est créée.

* **Taille max. des miniatures de pièces jointes**

  Taille maximale (en pixels) de la miniature de la pièce jointe. La valeur par défaut est 800 x 800.

* **Taille d’image min. pour la miniature**
* **Taille maximale de la miniature**

  Taille maximale (en pixels) de la miniature de l’image intégrée. La valeur par défaut est 800 x 800.

* **Sujets par page**

  Définit le nombre de sujets/publications par page. La valeur par défaut est 10.

* **Modérée**

  Si cette case est cochée, la publication des sujets et des commentaires doit être approuvée avant de pouvoir apparaître sur un site de publication. La case par défaut est décochée.

* **Fermé**

  Si cette case est cochée, le forum est fermé pour de nouveaux sujets et commentaires. La case par défaut est décochée.

* **Éditeur de texte enrichi**

  Si cette case est cochée, les sujets et les commentaires peuvent être saisis avec une annotation. La case par défaut est décochée.

* **Autoriser le balisage**

  Si cette case est cochée, les membres ont le droit d’ajouter des libellés de balise à leurs publications (voir **Champ de balise** ). La case par défaut est décochée.

* **Autoriser les chargements de fichiers**

  Si cette case est cochée, vous pouvez ajouter des pièces jointes à la rubrique ou au commentaire. La case par défaut est décochée.

* **Autoriser abonnement**

  Si cette case est cochée, incluez la fonction suivante pour les publications de forum, ce qui permet aux membres d’être [notifié](/help/communities/notifications.md) de nouvelles publications. La case par défaut est décochée.

* **Autoriser l’épinglage**

  Si cette case est cochée, les sujets de forum peuvent être placés en haut de la liste des sujets. La case par défaut est décochée.

* **Autoriser le contenu proposé**

  Si cette option est cochée, l’idée est identifiable comme [contenu proposé](/help/communities/featured.md). La case par défaut est décochée.

* **Autoriser les abonnements par courrier électronique**

  Si cette case est cochée, autorisez les membres à être informés des nouvelles publications par courrier électronique ([abonnement](/help/communities/subscriptions.md)). Nécessite `Allow Following` à vérifier et [email configuré](/help/communities/email.md). La case par défaut est décochée.

* **Taille maximale du fichier**

  Pertinent uniquement si `Allow File Uploads` est cochée. Ce champ limite la taille (en octets) d’un fichier chargé. La valeur par défaut est 104857600 (10 Mo).

* **Types de fichier autorisés**

  Pertinent uniquement si `Allow File Uploads` est cochée. Liste d’extensions de fichier séparées par des virgules avec le séparateur &quot;point&quot;. Par exemple, .jpg, .jpeg, .png, .doc, .docx, .pdf. Si des types de fichiers sont spécifiés, ceux qui ne sont pas spécifiés ne peuvent pas être chargés. Par défaut, aucun n’est spécifié, de sorte que tous les types de fichiers soient autorisés.

* **Taille max. du fichier image joint**
À définir uniquement si l’option Autoriser les chargements de fichiers est cochée. Nombre maximal d’octets qu’un fichier image chargé peut contenir. La valeur par défaut est 2097152 (2 Mo).

* **Autoriser les réponses à thème**

  Si cette case est cochée, les réponses aux commentaires sont publiées sur le sujet. La case par défaut est décochée.

* **Autoriser le vote**

  Si cette case est cochée, la fonction de vote est ajoutée à un sujet. La case par défaut est décochée.

* **Autoriser les utilisateurs à supprimer les commentaires et sujets**

  Si cette case est cochée, autorisez les membres à supprimer les commentaires et les sujets qu’ils ont publiés. La case par défaut est décochée.

* **Afficher le fil d’Ariane**

  Si cette case est cochée, les chemins de navigation s’affichent sur les pages de rubrique. La valeur par défaut est cochée.

* **Afficher les badges**

  Si cette case est cochée, affichez les droits gagnés et attribués. [badges](/help/communities/implementing-scoring.md) avec l&#39;entrée de blog d&#39;un membre. La case par défaut est décochée.

* **Autoriser les membres privilégiés**

  Si cette case est cochée, seuls les membres privilégiés sont autorisés à créer du contenu.

* **Membres privilégiés autorisés**

  Ajoutez les membres privilégiés autorisés à créer du contenu.

* **Bloquer le contenu généré par l’utilisateur en mode d’édition de l’auteur**

  S’il est activé, bloque le contenu généré par l’utilisateur lors de la modification en mode création.

* **Activer la mention**

  S’il est activé, permet aux utilisateurs enregistrés de la communauté d’identifier d’autres membres enregistrés (à l’aide du prénom, du nom, du nom d’utilisateur) et de les baliser à l’aide de la syntaxe @user-name courante. Les utilisateurs balisés reçoivent des notifications sur leurs mentions.

* **Nombre max. de mentions**

  Limitez le nombre maximal de mentions autorisées dans une publication. La valeur par défaut est 10.

* **Modèle des mentions de l’IU**

  Spécifiez la chaîne de modèle autorisée à baliser (@mention) l’utilisateur enregistré dans une publication. Par exemple, `~{{familyName}}{{givenName}}`.

>[!NOTE]
>
>Il peut être nécessaire de vérifier les deux `AllowThreaded Replies` et `Allow users to Delete Comments and Topics` pour activer les commentaires sur un sujet.

#### Onglet Modération d’utilisateur {#user-moderation-tab}

Sous , **Modération d’utilisateur** , indiquez comment les sujets et réponses publiés (contenu généré par l’utilisateur) sont gérés. Pour plus d’informations, voir [Modération de contenu généré par l’utilisateur](/help/communities/moderate-ugc.md).

* **Refuser les publications**

  Si cette case est cochée, les modérateurs membres approuvés sont autorisés à refuser des publications et à empêcher que la publication ne s’affiche sur le forum public. La case par défaut est décochée.

* **Fermer/rouvrir les sujets**

  Si cette case est cochée, les membres modérateurs autorisés peuvent fermer une rubrique pour ajouter d’autres modifications et commentaires et rouvrir une rubrique. La case par défaut est décochée.

* **Déplacer les rubriques**

  Si cette case est cochée, les modérateurs du côté publication peuvent déplacer les rubriques. La valeur par défaut est cochée.

* **Marquer les publications**

  Si cette case est cochée, les membres ont le droit de marquer les sujets ou commentaires d’autres personnes comme étant inappropriés. La case par défaut est décochée.

* **Marquer la liste de motifs**

  Si cette case est cochée, les membres ont le droit de choisir dans une liste déroulante la raison pour laquelle ils ont marqué un sujet ou un commentaire comme étant inapproprié. La case par défaut est décochée.

* **Motif de la marque personnalisée**

  Si cette case est cochée, autorisez les membres à indiquer leur propre raison de signaler un sujet ou un commentaire comme étant inapproprié. La case par défaut est décochée.

* **Seuil de modération**

  Saisissez le nombre de fois qu’un sujet ou un commentaire doit être marqué par les membres avant que les modérateurs ne soient informés. La valeur par défaut est 1 (une fois).

* **Limite de marquage**

  Saisissez le nombre de fois qu’un sujet ou un commentaire doit être marqué avant qu’il ne soit plus visible pour le public. S’il est défini sur -1, le sujet ou le commentaire marqué n’est jamais masqué à la vue du public. Sinon, ce nombre doit être supérieur ou égal au seuil de modération. La valeur par défaut est 5.

#### Onglet Champ de balise {#tag-field-tab}

Sous , **Champ de balise** , les balises qui peuvent être appliquées, le cas échéant, sous l’onglet **Paramètres** sont limités en fonction des espaces de noms sélectionnés.

* **Espaces de noms autorisés**

  Pertinent si `Allow Tagging` est coché sous **Paramètres** . Les balises qui peuvent être appliquées sont limitées aux catégories d’espace de noms cochées. La liste des espaces de noms inclut &quot;Balises standard&quot; (espace de noms par défaut) et &quot;Inclure toutes les balises&quot;. La valeur par défaut n’est pas cochée, ce qui signifie que tous les espaces de noms sont autorisés.

* **Limite de suggestions**

  Saisissez le nombre de balises à afficher comme suggestion au membre qui publie sur le forum. La valeur par défaut est **-**1 (aucune limite).

#### Onglet Traduction {#translation-tab}

Sous , **Traduction** , si la traduction est activée pour le site de la communauté, elle peut être définie pour traduire l’intégralité de la rubrique ou les publications sélectionnées.

* **Tout traduire**

  Si cette case est cochée, le fil du forum est traduit dans la langue préférée de l’utilisateur. La case par défaut est décochée.

#### Onglet Paramètres de tri {#sort-settings-tab}

Sous , **Paramètres de tri** , indiquez comment les commentaires publiés sont triés lorsqu’ils sont affichés.

* **Trier par**

  Cochez toutes les sélections de tri autorisées : `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. La valeur par défaut est `Newest, Oldest, Last Updated`.

* **Définir par défaut**

  Extrayez pour sélectionner l’une des options de tri cochées à afficher par défaut. La valeur par défaut est `Newest`.

* **Sélectionner les options de temps pour le tri Analytics**

  Faites glisser le curseur pour sélectionner l’une des options suivantes : `All, Last 24 Hours, Last 7 Days, Last 30 Days`.

  La valeur par défaut est `All`.

### Informations supplémentaires {#additional-information}

Vous trouverez plus d’informations sur la [Notions fondamentales sur le forum](/help/communities/essentials-forum.md) pour les développeurs.

Pour la modération des sujets et des commentaires publiés, voir [Modération de contenu généré par l’utilisateur](/help/communities/moderate-ugc.md).

Pour baliser des sujets et des commentaires publiés, voir [Balisage de contenu généré par l’utilisateur](/help/communities/tag-ugc.md).

Pour la traduction des sujets et des commentaires publiés, voir [Traduction de contenu généré par l’utilisateur](/help/communities/translate-ugc.md).
