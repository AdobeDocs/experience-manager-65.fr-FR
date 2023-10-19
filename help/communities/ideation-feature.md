---
title: Fonctionnalité d’orientation
description: Découvrez comment ajouter et configurer la fonction d’identification qui permet aux membres de la communauté de créer, d’afficher, de suivre, de voter et de commenter les idées partagées avec la communauté.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: e130bab4-524d-4413-ba8b-53d0ed9e8623
source-git-commit: b8887b4a6f757352e9dbfdf074c10e9ccd6dbd4f
workflow-type: tm+mt
source-wordcount: '1122'
ht-degree: 12%

---

# Fonctionnalité d’orientation {#ideation-feature}

## Présentation {#introduction}

La fonction d’idéation fournit une zone pour les visiteurs connectés du site (membres de la communauté) dans l’environnement de publication afin que :

* Créez des idées à partager avec la communauté.
* Affichez et commentez des idées.
* Suis une idée !
* Votez pour une idée.

Cette section de la documentation décrit :

* Ajout de la fonction d’idéation à un site AEM.
* Paramètres de configuration du composant Idéation.

### Ajout d’une idée à une page {#adding-a-ideation-to-a-page}

Pour ajouter une `Ideation` sur une page en mode création, utilisez l’explorateur de composants pour accéder à

* `Communities / Ideation`

Et faites-le glisser sur une page où l&#39;idée doit apparaître.

Pour obtenir les informations nécessaires, consultez la section [Principes de base des composants des communautés](/help/communities/basics.md).

Lorsque la variable [bibliothèques côté client requises](/help/communities/ideation.md#essentials-for-client-side) sont incluses, c’est ainsi que la variable `Ideation` Le composant apparaît :

![idéation](assets/ideation.png)

### Configuration d’une idée {#configuring-an-ideation}

Sélectionnez le `Ideation` afin que vous puissiez accéder au `Configure` qui ouvre la boîte de dialogue de modification.

![configure-new](assets/configure-new.png)

![ideation-settings](assets/ideation-settings.png)

#### Onglet Paramètres {#settings-tab}

Sous , **[!UICONTROL Paramètres]** , spécifiez les paramètres des idées et des commentaires :

* **Autoriser les miniatures de pièces jointes**
* **Taille max. des miniatures de pièces jointes**
* **Taille d’image minimale pour la miniature**
* **Taille maximale de la miniature**
* **Autoriser les membres privilégiés**
* **Membres privilégiés autorisés**
* **Bloquer le contenu généré par l’utilisateur en mode d’édition d’auteur**
* **Titre de conceptualisation**

* Titre d’affichage de l’idée. La valeur par défaut est `Ideation`.
* **Description de la conceptualisation**

  Description à afficher en tant que sous-titre de l’idée. La valeur par défaut n’est pas une description.

* **Sujets par page**

  Définit le nombre d’idées/de publications affichées par page. La valeur par défaut est 10.

* **Modérée**

  Si cette case est cochée, la publication d’idées et de commentaires doit être approuvée avant de pouvoir apparaître sur un site de publication. La case par défaut est décochée.

* **Fermé**

  Si cette case est cochée, le forum d’idéation est fermé aux idées et commentaires nouveaux. La case par défaut est décochée.

* **Éditeur de texte enrichi**

  Si cette case est cochée, les idées et les commentaires peuvent être saisis avec des balises. La case par défaut est décochée.

* **Autoriser le balisage**

  Si cette case est cochée, les membres ont le droit d’ajouter des libellés de balise à leurs publications (voir **[!UICONTROL Champ de balise]** ). La case par défaut est décochée.

* **Autoriser les chargements de fichiers**

  Si cette case est cochée, vous pouvez ajouter des pièces jointes à l’idée ou au commentaire. La case par défaut est décochée.

* **Taille maximale du fichier**

  Pertinent uniquement si `Allow File Uploads` est cochée. Ce champ limite la taille (en octets) d’un fichier chargé. La valeur par défaut est 104857600 (10 Mo).

* **Types de fichier autorisés**

  Pertinent uniquement si `Allow File Uploads` est cochée. Liste d’extensions de fichier séparées par des virgules avec le séparateur &quot;point&quot;. Par exemple : .jpg, .jpeg, .png, .doc, .docx, .pdf. Si des types de fichiers sont spécifiés, ceux qui ne sont pas spécifiés ne peuvent pas être chargés. Par défaut, aucun n’est spécifié, de sorte que tous les types de fichiers soient autorisés.

* **Taille max. du fichier image joint**

  À définir uniquement si l’option Autoriser les chargements de fichiers est cochée. Nombre maximal d’octets qu’un fichier image chargé peut contenir. La valeur par défaut est 2097152 (2 Mo).

* **Autoriser les réponses**

  Si cette case est cochée, les réponses aux commentaires sont publiées sur l’idée. La case par défaut est décochée.

* **Autoriser le vote**

  Si cette option est cochée, vous pouvez voter sur les commentaires d’une idée. La case par défaut est décochée.

* **Autoriser les utilisateurs à supprimer les commentaires et sujets**

  Si cette case est cochée, autorisez les membres à supprimer les commentaires et idées qu’ils ont publiés. La case par défaut est décochée.

* **Autoriser abonnement**

  Si cette case est cochée, incluez la fonction suivante pour les publications d’idées, ce qui permet aux membres d’être [notifié](/help/communities/notifications.md) de nouvelles publications. La case par défaut est décochée.

* **Autoriser les abonnements par courrier électronique**

  Si cette case est cochée, autorisez les membres à être informés des nouvelles publications par courrier électronique ([abonnement](/help/communities/subscriptions.md)). Nécessite `Allow Following` à vérifier et [email configuré](/help/communities/email.md). La case par défaut est décochée.

* **Autoriser le vote**

  Si cette option est cochée, vous pouvez voter sur les commentaires d’une idée. La case par défaut est décochée.

* **Afficher les badges**

  Si cette case est cochée, affichez les droits gagnés et attribués. [badges](/help/communities/implementing-scoring.md) avec l&#39;idée d&#39;un membre. La case par défaut est décochée.

* **Ne pas obtenir de réponses sur la page de liste**

* **Autoriser le contenu proposé**

  Si cette option est cochée, l’idée est identifiable comme [contenu proposé](/help/communities/featured.md). La case par défaut est décochée.

* **Activer la mention**
* **Nombre max. de mentions**
* **Modèle des mentions de l’IU**

#### Onglet Modération d’utilisateur {#user-moderation-tab}

Sous , **[!UICONTROL Modération d’utilisateur]** , indiquez comment les idées et commentaires publiés (contenu généré par l’utilisateur) sont gérés. Pour plus d’informations, voir [Modération de contenu généré par l’utilisateur](/help/communities/moderate-ugc.md).

* **Refuser les publications**

  Si cette case est cochée, les membres modérateurs autorisés peuvent refuser les publications et empêcher l’affichage de la publication sur le forum public. La case par défaut est décochée.

* **Fermer/rouvrir les sujets**

  Si cette case est cochée, les membres modérateurs autorisés peuvent fermer une rubrique pour ajouter d’autres modifications et commentaires et rouvrir une rubrique. La case par défaut est décochée.

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

Sous , **[!UICONTROL Champ de balise]** , les balises qui peuvent être appliquées, le cas échéant, sous l’onglet **[!UICONTROL Paramètres]** sont limités en fonction des espaces de noms sélectionnés.

* **Espaces de noms autorisés**

  Pertinent si `Allow Tagging` est coché sous **[!UICONTROL Paramètres]** . Les balises qui peuvent être appliquées sont limitées aux catégories d’espace de noms cochées. La liste des espaces de noms inclut &quot;Balises standard&quot; (espace de noms par défaut) et &quot;Inclure toutes les balises&quot;. La valeur par défaut n’est pas cochée, ce qui signifie que tous les espaces de noms sont autorisés.

* **Limite de suggestions**

  Saisissez le nombre de balises à afficher comme suggestion au membre qui publie sur le forum. Une valeur de **-1** signifie pas de limite. La valeur par défaut est 0.

#### Onglet Paramètres de tri {#sort-settings-tab}

Sous , **[!UICONTROL Paramètres de tri]** , indiquez comment les commentaires publiés sont triés lorsqu’ils sont affichés.

* **Trier par**

  Cochez toutes les sélections de tri autorisées : `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. La valeur par défaut est `Newest, Oldest, Last Updated`.

* **Définir par défaut**

  Extrayez pour sélectionner l’une des options de tri cochées à afficher par défaut. La valeur par défaut est `Newest`.

* **Sélectionner les options de temps pour le tri Analytics**

  Menu déroulant pour sélectionner l’un des `All, Last 24 Hours, Last 7 Days, Last 30 Days`. La valeur par défaut est `All`.

## Expérience du visiteur du site {#site-visitor-experience}

### Créer une idée {#creating-idea}

Comme pour toutes les fonctionnalités de Communities, si elle n’est pas connectée, un visiteur du site ne peut lire que des idées et consulter d’autres opinions (par le biais de commentaires et de votes/commentaires).

Une fois connecté, un membre peut créer une idée.

![create-new-idée](assets/create-new-idea.png)

Avant de soumettre l’idée, le membre peut enregistrer un brouillon.

En sélectionnant la variable `Save as Draft` , un brouillon est enregistré.

![save-idée](assets/save-idea.png)

Lors de l’affichage de brouillons enregistrés dans la `My Drafts` onglet, sélectionnez `Read More` pour revenir en mode d’édition :

![edit-idée](assets/edit-idea.png)

#### Fournir des commentaires {#providing-feedback}

Une fois l’idée publiée, d’autres membres peuvent se connecter et ouvrir l’idée ( `Read More`) et aimez l&#39;idée, ajoutant ainsi au nombre de votes, et faites des commentaires.

![feedback](assets/feedback-idea.png)

### Informations supplémentaires {#additional-information}

Vous trouverez plus d’informations sur la [Notions fondamentales relatives aux idées](/help/communities/ideation.md) pour les développeurs.

Pour la modération des sujets et des commentaires publiés, voir [Modération de contenu généré par l’utilisateur](/help/communities/moderate-ugc.md).

Pour baliser des sujets et des commentaires publiés, voir [Balisage du contenu généré par l’utilisateur](/help/communities/tag-ugc.md).
