---
title: Fonctionnalité d’orientation
seo-title: Fonctionnalité d’orientation
description: Ajout et configuration de la fonction d’orientation
seo-description: Ajout et configuration de la fonction d’orientation
uuid: 38468290-6d00-4ee4-91d8-7c2e8ae32712
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: a3f5a21d-2df6-4663-a1ea-3a067c46f860
docset: aem65
translation-type: tm+mt
source-git-commit: 85f3b8f2a5f079954f4907037c1c722a6b25fd91

---


# Fonctionnalité d’orientation {#ideation-feature}

## Présentation {#introduction}

La fonctionnalité d’idéation fournit une zone pour les du site connectés (membres de la communauté) dans le  de publication  à :

* Créez des idées à partager avec la communauté.
*  et commenter les idées.
* Suis une idée.
* Votez pour une idée.

Cette section de la documentation décrit:

* Ajout de la fonctionnalité d’idéation à un site AEM.
* Paramètres de configuration du composant Ideation.

### Adding a Ideation to a Page {#adding-a-ideation-to-a-page}

To add a `Ideation` component to a page in author mode, use the component browser to locate

* `Communities / Ideation`

et faites-le glisser sur une page où l&#39;idée doit apparaître.

For necessary information, visit [Communities Components Basics](/help/communities/basics.md).

When the [required client-side libraries](/help/communities/ideation.md#essentials-for-client-side) are included, this is how the `Ideation` component will appear:

![chlimage_1-71](assets/chlimage_1-71.png)

### Configuration d’une idée {#configuring-an-ideation}

Select the placed `Ideation` component to access and select the `Configure` icon which opens the edit dialog.

![chlimage_1-72](assets/chlimage_1-72.png) ![ideation-settings](assets/ideation-settings.png)

#### Onglet Settings {#settings-tab}

Under the **[!UICONTROL Settings]** tab, specify settings for ideas and comments:

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

* **Modéré**

   Si cette option est cochée, la publication d’idées et de commentaires doit être approuvée avant qu’ils ne s’affichent sur un site de publication. Cette option n’est pas cochée par défaut.

* **Fermé**

   Si cette option est cochée, le forum d&#39;idéation est fermé aux nouvelles idées et aux nouveaux commentaires. Cette option n’est pas cochée par défaut.

* **Éditeur de texte enrichi**

   Si cette option est cochée, les idées et les commentaires peuvent être saisis avec annotation. Cette option n’est pas cochée par défaut.

* **Autoriser le balisage**

   If checked, allow members to add tag labels to their post (see **[!UICONTROL Tag field]** tab). Cette option n’est pas cochée par défaut.

* **Autoriser les transferts de fichiers**

   Si cette option est cochée, autorisez l’ajout de pièces jointes à l’idée ou au commentaire. Cette option n’est pas cochée par défaut.

* **Taille maximale du fichier**

   N’est pertinent que si `Allow File Uploads` est coché. Ce champ limite la taille (en octets) d’un fichier chargé. La valeur par défaut est 1 048 57 600 (10 Mo).

* **Types de fichier autorisés**

   N’est pertinent que si `Allow File Uploads` est coché. d’extensions de fichier séparé par des virgules avec le séparateur &quot;point&quot;. Par exemple : .jpg, .jpeg, .png, .doc, .docx, .pdf. Si des types de fichier sont spécifiés, ceux qui ne sont pas spécifiés ne seront pas autorisés à être téléchargés. Par défaut, aucun type de fichier n’est spécifié, de sorte que tous les types de fichier soient autorisés.

* **Taille max. du fichier image joint**

   N’est pertinent que si l’option Autoriser les téléchargements de fichiers est cochée. Taille maximale en octets pour un fichier image chargé. La valeur par défaut est 2097152 (2 Mo).

* **Permettre des réponses**

   Si cette option est cochée, autorisez les réponses aux commentaires publiés sur l’idée. Cette option n’est pas cochée par défaut.

* **Autoriser le vote**

   Si cette option est cochée, autorisez le vote sur les commentaires d&#39;une idée. Cette option n’est pas cochée par défaut.

* **Autoriser les utilisateurs à supprimer les commentaires et sujets**

   Si cette option est cochée, permettez aux membres de supprimer les commentaires et idées qu’ils ont publiés. Cette option n’est pas cochée par défaut.

* **Autoriser abonnement**

   Si cette option est cochée, incluez la fonctionnalité suivante pour les publications d’idées, ce qui permet aux membres d’être [informés](/help/communities/notifications.md) des nouvelles publications. Cette option n’est pas cochée par défaut.

* **Autoriser les abonnements par courrier électronique**

   Si cette option est cochée, autorisez les membres à être informés des nouvelles publications par courrier électronique ([](/help/communities/subscriptions.md)). Requiert `Allow Following` la vérification et la configuration [du](/help/communities/email.md)courrier électronique. Cette option n’est pas cochée par défaut.

* **Autoriser le vote**

   Si cette option est cochée, autorisez le vote sur les commentaires d&#39;une idée. Cette option n’est pas cochée par défaut.

* **Afficher les badges**

   Si cette option est cochée, affichez les [badges](/help/communities/implementing-scoring.md) gagnés et attribués avec l’idée d’un membre. Cette option n’est pas cochée par défaut.

* **Ne pas obtenir de réponses sur la page de liste**

* **Autoriser le contenu proposé**

   Si cette option est cochée, l’idée peut être identifiée comme contenu [](/help/communities/featured.md)incitatif. Cette option n’est pas cochée par défaut.

* **Activer la mention**
* **Nombre max. de mentions**
* **Modèle des mentions de l’IU**

#### Onglet Modération utilisateur {#user-moderation-tab}

Under the **[!UICONTROL User Moderation]** tab, specify how the posted ideas and comments (user generated content) are managed. Pour plus d’informations, voir [Modération de contenu généré par les utilisateurs](/help/communities/moderate-ugc.md).

* **Refuser les publications**

   Si cette option est cochée, les modérateurs membres de confiance seront autorisés à refuser les publications et à empêcher leur publication de s’afficher sur le forum public. Cette option n’est pas cochée par défaut.

* **Fermer/rouvrir les sujets**

   Si cette option est cochée, les modérateurs de membres de confiance peuvent fermer une rubrique pour apporter d’autres modifications et commentaires et rouvrir une rubrique. Cette option n’est pas cochée par défaut.

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

Dans l’onglet **[!UICONTROL Champ de balise]**, les balises qui peuvent être appliquées, si l’option est activée dans l’onglet **[!UICONTROL Paramètres]**, sont limitées selon les espaces de noms sélectionnés.

* **Espaces de noms autorisés**

   Pertinente si `Allow Tagging` est cochée sous l’onglet **[!UICONTROL Paramètres]** . Les balises pouvant être appliquées se limitent à celles liées aux catégories d’espace de noms cochées. Le de  inclut les balises standard (le par défaut) ainsi que l’option Inclure toutes les balises. La valeur par défaut n’est pas cochée, ce qui signifie que tous les  de  sont autorisés.

* **Limite de suggestions**

   Entrez le nombre de balises à afficher comme suggestion au membre qui publie sur le forum. Une valeur de **-1** signifie aucune limite. La valeur par défaut est 0.

#### Onglet Paramètres de tri {#sort-settings-tab}

Sous l’onglet Paramètres **[!UICONTROL de]** tri, spécifiez le mode de tri des commentaires publiés lorsqu’ils sont affichés.

* **Trier par**

   Vérifier toutes les sélections de tri autorisées : `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. La valeur par défaut est `Newest, Oldest, Last Updated`.

* **Définir par défaut**

   Appuyez sur la touche Bas pour sélectionner l’une des options de tri cochées et l’afficher comme valeur par défaut. La valeur par défaut est `Newest`.

* **Sélectionner les options de temps pour le tri Analytics**

   Tirez vers le bas pour sélectionner l’un des `All, Last 24 Hours, Last 7 Days, Last 30 Days`. La valeur par défaut est `All`.

## Expérience des visiteurs {#site-visitor-experience}

### Création d’une idée {#creating-idea}

Comme pour toutes les fonctionnalités des Communautés, si elles ne sont pas connectées, un de site ne peut lire que des idées et des opinions (par le biais de commentaires et de votes/appréciations).

Une fois connecté, un membre peut créer une nouvelle idée.

![chlimage_1-73](assets/chlimage_1-73.png)

Avant de soumettre l&#39;idée, il est possible que le membre enregistre un brouillon.

En sélectionnant le `Save as Draft` bouton, un brouillon est enregistré.

![chlimage_1-74](assets/chlimage_1-74.png)

Lors de l’affichage des brouillons enregistrés dans le `My Drafts` panneau, sélectionnez `Read More` pour passer de nouveau en mode d’édition :

![chlimage_1-75](assets/chlimage_1-75.png)

#### Fournir des commentaires {#providing-feedback}

Une fois l&#39;idée publiée, d&#39;autres membres peuvent se connecter, ouvrir l&#39;idée ( `Read More`) et aimer l&#39;idée, ce qui ajoute au nombre de votes, et faire des commentaires.

![chlimage_1-76](assets/chlimage_1-76.png)

### Informations supplémentaires {#additional-information}

More information may be found on the [Ideation Essentials](/help/communities/ideation.md) page for developers.

Pour des informations sur la modération des sujets et des commentaires publiés, reportez-vous à la section [Modération du contenu généré par l’utilisateur](/help/communities/moderate-ugc.md).

Pour baliser les sujets et les commentaires publiés, voir [Balisage de contenu généré par l’utilisateur](/help/communities/tag-ugc.md).
