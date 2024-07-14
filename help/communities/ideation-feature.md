---
title: Fonctionnalité d’orientation
description: Découvrez comment ajouter et configurer la fonction d’identification qui permet aux membres de la communauté de créer, d’afficher, de suivre, de voter et de commenter les idées partagées avec la communauté.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: e130bab4-524d-4413-ba8b-53d0ed9e8623
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1132'
ht-degree: 1%

---

# Fonctionnalité d’orientation {#ideation-feature}

## Présentation {#introduction}

La fonction d’idéation fournit une zone pour les visiteurs connectés du site (membres de la communauté) dans l’environnement Publish afin que :

* Créez des idées à partager avec la communauté.
* Affichez et commentez des idées.
* Suis une idée !
* Votez pour une idée.

Cette section de la documentation décrit :

* Ajout de la fonction d’idéation à un site AEM.
* Paramètres de configuration du composant Idéation.

### Ajout d’une idée à une page {#adding-a-ideation-to-a-page}

Pour ajouter un composant `Ideation` à une page en mode création, utilisez l’explorateur de composants pour accéder à :

* `Communities / Ideation`

Et faites-le glisser sur une page où l&#39;idée doit apparaître.

Pour plus d’informations, consultez la page [Principes de base des composants Communities](/help/communities/basics.md).

Lorsque les [bibliothèques côté client demandées](/help/communities/ideation.md#essentials-for-client-side) sont incluses, voici comment le composant `Ideation` apparaît :

![idéation](assets/ideation.png)

### Configuration d’une idée {#configuring-an-ideation}

Sélectionnez le composant `Ideation` inséré afin que vous puissiez accéder à l’icône `Configure` qui ouvre la boîte de dialogue de modification.

![configure-new](assets/configure-new.png)

![ideation-settings](assets/ideation-settings.png)

#### Onglet Paramètres {#settings-tab}

Sous l’onglet **[!UICONTROL Paramètres]** , spécifiez les paramètres des idées et des commentaires :

* **Autoriser la miniature des pièces jointes**
* **Taille max. de la miniature de la pièce jointe**
* **Taille d’image min. pour la miniature**
* **Taille max. de miniature**
* **Autoriser les membres privilégiés**
* **Membres autorisés**
* **Bloquer le contenu généré par l’utilisateur en mode d’édition de l’auteur**
* **Titre de l’idéation**

* Titre d’affichage de l’idée. La valeur par défaut est `Ideation`.
* **Description de l’idée**

  Description à afficher en tant que sous-titre de l’idée. La valeur par défaut n’est pas une description.

* **Sujets par page**

  Définit le nombre d’idées/de publications affichées par page. La valeur par défaut est 10.

* **Modéré**

  Si cette case est cochée, la publication d’idées et de commentaires doit être approuvée avant de pouvoir apparaître sur un site de publication. La case par défaut est décochée.

* **Fermé**

  Si cette case est cochée, le forum d’idéation est fermé aux idées et commentaires nouveaux. La case par défaut est décochée.

* **Éditeur de texte enrichi**

  Si cette case est cochée, les idées et les commentaires peuvent être saisis avec des balises. La case par défaut est décochée.

* **Autoriser le balisage**

  Si cette case est cochée, les membres ont le droit d’ajouter des libellés de balise à leurs publications (voir l’onglet **[!UICONTROL Champ de balise]** ). La case par défaut est décochée.

* **Autoriser les chargements de fichiers**

  Si cette case est cochée, vous pouvez ajouter des pièces jointes à l’idée ou au commentaire. La case par défaut est décochée.

* **Taille de fichier max.**

  Pertinent uniquement si `Allow File Uploads` est coché. Ce champ limite la taille (en octets) d’un fichier chargé. La valeur par défaut est 104857600 (10 Mo).

* **Types de fichiers autorisés**

  Pertinent uniquement si `Allow File Uploads` est coché. Liste d’extensions de fichier séparées par des virgules avec le séparateur &quot;point&quot;. Par exemple, .jpg, .jpeg, .png, .doc, .docx, .pdf. Si des types de fichiers sont spécifiés, ceux qui ne sont pas spécifiés ne peuvent pas être chargés. Par défaut, aucun n’est spécifié, de sorte que tous les types de fichiers soient autorisés.

* **Taille max. du fichier image joint**

  À définir uniquement si l’option Autoriser les chargements de fichiers est cochée. Nombre maximal d’octets qu’un fichier image chargé peut contenir. La valeur par défaut est 2097152 (2 Mo).

* **Autoriser les réponses**

  Si cette case est cochée, les réponses aux commentaires sont publiées sur l’idée. La case par défaut est décochée.

* **Autoriser le vote**

  Si cette option est cochée, vous pouvez voter sur les commentaires d’une idée. La case par défaut est décochée.

* **Autoriser les utilisateurs à supprimer des commentaires et des sujets**

  Si cette case est cochée, autorisez les membres à supprimer les commentaires et idées qu’ils ont publiés. La case par défaut est décochée.

* **Autoriser l’abonnement**

  Si cette case est cochée, incluez la fonction suivante pour les publications d’idées, ce qui permet aux membres d’être [informés](/help/communities/notifications.md) des nouvelles publications. La case par défaut est décochée.

* **Autoriser les abonnements aux emails**

  Si cette case est cochée, autorisez les membres à être informés des nouvelles publications par e-mail ([subscription](/help/communities/subscriptions.md)). Nécessite `Allow Following` à vérifier et [email configuré](/help/communities/email.md). La case par défaut est décochée.

* **Autoriser le vote**

  Si cette option est cochée, vous pouvez voter sur les commentaires d’une idée. La case par défaut est décochée.

* **Badges d’affichage**

  Si cette case est cochée, affichez les [badges](/help/communities/implementing-scoring.md) gagnés et attribués avec l’idée d’un membre. La case par défaut est décochée.

* **Ne pas obtenir de réponses sur la page de liste**

* **Autoriser le contenu en vedette**

  Si cette case est cochée, l’idée est identifiable en tant que [contenu présenté](/help/communities/featured.md). La case par défaut est décochée.

* **Activer la mention**
* **Nombre maximal de mentions**
* **Modèle de mention d’interface utilisateur**

#### Onglet Modération d’utilisateur {#user-moderation-tab}

Sous l’onglet **[!UICONTROL Modération d’utilisateur]** , indiquez comment les idées et les commentaires publiés (contenu généré par l’utilisateur) sont gérés. Pour plus d’informations, voir [Modération de contenu généré par l’utilisateur](/help/communities/moderate-ugc.md).

* **Refuser des publications**

  Si cette case est cochée, les membres modérateurs autorisés peuvent refuser les publications et empêcher l’affichage de la publication sur le forum public. La case par défaut est décochée.

* **Fermer/rouvrir les rubriques**

  Si cette case est cochée, les membres modérateurs autorisés peuvent fermer une rubrique pour ajouter d’autres modifications et commentaires et rouvrir une rubrique. La case par défaut est décochée.

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

Sous l’onglet **[!UICONTROL Champ de balise]** , les balises qui peuvent être appliquées, si elles sont autorisées sous l’onglet **[!UICONTROL Paramètres]**, sont limitées en fonction des espaces de noms sélectionnés.

* **Espaces de noms autorisés**

  Pertinent si `Allow Tagging` est coché sous l’onglet **[!UICONTROL Paramètres]**. Les balises qui peuvent être appliquées sont limitées aux catégories d’espace de noms cochées. La liste des espaces de noms inclut &quot;Balises standard&quot; (espace de noms par défaut) et &quot;Inclure toutes les balises&quot;. La valeur par défaut n’est pas cochée, ce qui signifie que tous les espaces de noms sont autorisés.

* **Limite de suggestion**

  Saisissez le nombre de balises à afficher comme suggestion au membre qui publie sur le forum. Une valeur **-1** signifie qu’aucune limite n’est définie. La valeur par défaut est 0.

#### Onglet Paramètres de tri {#sort-settings-tab}

Sous l’onglet **[!UICONTROL Paramètres de tri]**, indiquez comment les commentaires publiés sont triés lorsqu’ils sont affichés.

* **Trier Par**

  Cochez toutes les sélections de tri autorisées : `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. La valeur par défaut est `Newest, Oldest, Last Updated`.

* **Défini comme valeur par défaut**

  Extrayez pour sélectionner l’une des options de tri cochées à afficher par défaut. La valeur par défaut est `Newest`.

* **Sélectionner les options d’heure pour le tri Analytics**

  Descends pour sélectionner l’un des `All, Last 24 Hours, Last 7 Days, Last 30 Days`. La valeur par défaut est `All`.

## Expérience du visiteur du site {#site-visitor-experience}

### Créer une idée {#creating-idea}

Comme pour toutes les fonctionnalités de Communities, si elle n’est pas connectée, un visiteur du site ne peut lire que des idées et consulter d’autres opinions (par le biais de commentaires et de votes/commentaires).

Une fois connecté, un membre peut créer une idée.

![create-new-idée](assets/create-new-idea.png)

Avant de soumettre l’idée, le membre peut enregistrer un brouillon.

En sélectionnant le bouton `Save as Draft`, un brouillon est enregistré.

![save-idée](assets/save-idea.png)

Lors de l’affichage des brouillons enregistrés dans l’onglet `My Drafts`, sélectionnez `Read More` pour revenir en mode d’édition :

![edit-idée](assets/edit-idea.png)

#### Fournir des commentaires {#providing-feedback}

Une fois l&#39;idée publiée, d&#39;autres membres peuvent se connecter, ouvrir l&#39;idée ( `Read More`) et aimer l&#39;idée, ajoutant ainsi au nombre de votes, et faire des commentaires.

![feedback](assets/feedback-idea.png)

### Informations supplémentaires {#additional-information}

Vous trouverez plus d’informations sur la page [Ideation Essentials](/help/communities/ideation.md) pour les développeurs.

Pour la modération des sujets et des commentaires publiés, voir [Modération de contenu généré par l’utilisateur](/help/communities/moderate-ugc.md).

Pour baliser les rubriques et commentaires publiés, voir [Balisage de contenu généré par l’utilisateur](/help/communities/tag-ugc.md).
