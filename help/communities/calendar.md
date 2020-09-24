---
title: Fonction Calendrier
seo-title: Fonction Calendrier
description: Fournit des informations sur les événements de la communauté dans un format de calendrier
seo-description: Fournit des informations sur les événements de la communauté dans un format de calendrier
uuid: 262f6afa-d8aa-4815-8440-a8ed5668c76d
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 70fa0b9c-cb98-45c4-9c94-bef4a9f3741e
docset: aem65
translation-type: tm+mt
source-git-commit: 41de9fff615b5b2f77d835740dfb1d33aa81e59b
workflow-type: tm+mt
source-wordcount: '1170'
ht-degree: 42%

---


# Fonction Calendrier {#calendar-feature}

## Présentation {#introduction}

La fonction Calendrier offre des informations relatives aux événements de la communauté dans un calendrier. Sont concernés tous les visiteurs ou uniquement ceux qui sont inscrits (membres de la communauté). Tous les membres autorisés peuvent ajouter des événements.

Cette section de la documentation décrit :

* ajouter la fonction Calendrier à un site AEM
* Configuration settings for `Calendar` components

## Ajout d’un calendrier à une page {#adding-a-calendar-to-a-page}

To add a `Calendar` component to a page in author mode, use the component browser to locate

* `Communities / Calendar`

et faites glisser le composant sur une page, par exemple à un endroit relatif à la fonction, pour permettre aux utilisateurs de le consulter.

For necessary information, visit [Communities Components Basics](/help/communities/basics.md).

When the [required client-side libraries](/help/communities/calendar-basics-for-developers.md#essentials-for-client-side) are included, this is how the `Calendar` component will appear.

![calendar-component](assets/calendar-component.png)

### Configuration du calendrier {#configuring-calendar}

Select the placed `Calendar` component to access and select the `Configure` icon which opens the edit dialog.

![configurer](assets/configure-new.png)

![configure-calendar](assets/configure-calendar1.png)

#### Onglet Settings {#settings-tab}

Under the **Settings** tab, specify whether or not to allow tags to be applied to calendar entries.

* **Événements par page**

   Définit le nombre d’événements affichés par page. La valeur par défaut est 10.

* **Modéré**

   Si cette case est cochée, la publication des événements calendaires et des commentaires doit être approuvée avant d&#39;apparaître sur un site de publication. Cette option n’est pas cochée par défaut.

* **Fermé**

   Si cette option est cochée, le calendrier est fermé aux nouvelles entrées et aux nouveaux commentaires de événement. Cette option n’est pas cochée par défaut.

* **Éditeur de texte enrichi**

   Si cette case est cochée, les événements calendaires et les commentaires peuvent être saisis avec une annotation. Cette option est cochée par défaut.

* **Autoriser le balisage**

   If checked, allow members to add tag labels to the events they post (see **Tag field** tab). Cette option est cochée par défaut.

* **Autoriser les transferts de fichiers**

   Si cette option est cochée, autorisez l’ajout de pièces jointes à un événement de calendrier ou à un commentaire. Cette option est cochée par défaut.

* **Autoriser abonnement**

   Si cette option est cochée, autorisez les membres à suivre les événements publiés dans le calendrier. Cette option est cochée par défaut.

* **Taille maximale du fichier**

   Ne s’applique que si `Allow File Uploads` la vérification est effectuée. Ce champ limite la taille (en octets) d’un fichier chargé. La valeur par défaut est 104857600 (10 Mo).

* **Types de fichier autorisés**

   Ne s’applique que si `Allow File Uploads` la vérification est effectuée. Liste séparée par des virgules d’extensions de fichiers avec le séparateur &quot;point&quot;. Par exemple : .jpg, .jpeg, .png, .doc, .docx, .pdf. Si des types de fichier sont spécifiés, ceux qui ne sont pas spécifiés ne seront pas autorisés à être téléchargés. Par défaut, aucun type de fichier n’est spécifié, de sorte que tous les types de fichier soient autorisés.

* **Taille max. du fichier image joint**

   N’est pertinent que si l’option Autoriser les téléchargements de fichiers est cochée. Taille maximale en octets pour un fichier image chargé. La valeur par défaut est 2097152** **(2 Mo).

* **Types autorisés d’image de couverture**

   Liste séparée par des virgules des extensions de fichiers d’image avec le séparateur &quot;point&quot;. La valeur par défaut est `.jpg,.jpeg,.png,.gif,.bmp`.

* **Autoriser les réponses à thème**

   Si cette option est cochée, autorisez les réponses aux commentaires publiés sur le événement du calendrier. Cette option est cochée par défaut.

* **Autoriser les utilisateurs à supprimer les commentaires et événements**

   Si cette option est cochée, autorisez les membres à supprimer les commentaires et les événements de calendrier qu’ils ont publiés. La valeur par défaut est** **cochée.

* **Autoriser le vote**

   Si cette case est cochée, incluez la fonction Vote avec un événement de calendrier. Cette option est cochée par défaut.

* **Afficher le fil d’Ariane**

   Afficher le fil d’Ariane sur la page des événements. Cette option est cochée par défaut.

* **Filtre de plage de dates**

   Définit le nombre de jours ajoutés à la date actuelle afin de calculer la valeur &quot;À&quot; du filtre de page de liste des événements du calendrier. Le nombre par défaut est 30.

* **Autoriser le contenu proposé**

   Si cette option est cochée, l’idée peut être identifiée comme contenu [](/help/communities/featured.md)phare. Cette option n’est pas cochée par défaut.

Under the **User Moderation** tab, specify how the posted topics and replies (user generated content) are managed. Pour plus d’informations, voir [Modération de contenu généré par les utilisateurs](/help/communities/moderate-ugc.md).

#### Onglet Modération utilisateur {#user-moderation-tab}

* **Refuser les publications**

   Si cette option est cochée, les modérateurs membres de confiance seront autorisés à refuser les publications et à empêcher que la publication ne s&#39;affiche sur le forum public. Cette option est cochée par défaut.

* **Fermer/rouvrir les événements**

   Si cette option est cochée, les modérateurs membres approuvés peuvent fermer un événement pour apporter d&#39;autres modifications et commentaires, et peuvent également rouvrir un événement. Cette option est cochée par défaut.

* **Marquer les publications**

   Si cette option est cochée, autorisez les membres à signaler que les événements ou commentaires d&#39;autrui sont inappropriés. Cette option est cochée par défaut.

* **Marquer la liste de motifs**

   Si cette option est cochée, permettez aux membres de choisir, dans une liste déroulante, la raison pour laquelle ils signalent un événement ou un commentaire comme inapproprié. Cette option n’est pas cochée par défaut.

* **Motif de la marque personnalisée**

   Si cette option est cochée, autorisez les membres à indiquer leur propre raison de signaler un événement ou un commentaire comme inapproprié. Cette option n’est pas cochée par défaut.

* **Seuil de modération**

   Indiquez le nombre de fois où un événement ou un commentaire doit être marqué par les membres avant que les modérateurs ne soient avertis. La valeur par défaut est 1 (une fois).

* **Limite de marquage**

   Indiquez le nombre de fois où un événement ou un commentaire doit être marqué avant d’être masqué dans la vue publique. Si la valeur est -1, le sujet ou le commentaire marqué est toujours visible pour le public. Dans le cas contraire, cette valeur doit être supérieure ou égale au seuil de modération. La valeur par défaut est 5.

#### Onglet Champ de balise {#tag-field-tab}

Dans l’onglet **Champ de balise**, les balises qui peuvent être appliquées, si l’option est activée dans l’onglet **Paramètres**, sont limitées selon les espaces de noms sélectionnés.

* **Espaces de noms autorisés**

   Pertinent si `Allow Tagging` est coché sous l’onglet **Paramètres** . Les balises pouvant être appliquées se limitent à celles liées aux catégories d’espace de noms cochées. La liste des espaces de nommage inclut &quot;Balises standard&quot; (l’espace de nommage par défaut) ainsi que &quot;Inclure toutes les balises&quot;. La valeur par défaut n’est pas cochée, ce qui signifie que tous les espaces de nommage sont autorisés.

* **Limite de suggestions**

   Entrez le nombre de balises à afficher comme suggestion au membre qui publie sur le forum. La valeur par défaut est **-**1 (aucune limite).

>[!NOTE]
>
>Consultez la rubrique [Administration des balises](/help/sites-administering/tags.md) pour savoir comment ajouter un espace de noms de balise (taxonomie).


#### Onglet Traduction {#translation-tab}

Sous l’onglet **Traduction**, si la traduction est activée pour le site de la communauté, elle peut être définie de sorte à traduire le fil d’Ariane entier (événement et commentaires) au lieu de certaines publications.

* **Tout traduire**

   Si cette case est cochée, le événement et les commentaires sont traduits dans la langue préférée de l’utilisateur. Cette option est cochée par défaut.

## Expérience des visiteurs {#site-visitor-experience}

Dans l’environnement de publication, la fonction Calendrier présente un champ de recherche avec une plage de dates par défaut et tous les événements de calendrier prévus pour cette plage.

Lorsqu’un événement de calendrier est sélectionné, ses détails, sa description et ses commentaires sont affichés.

Les autres choix varient selon que le visiteur est modérateur, administrateur, membre de la communauté, membre privilégié ou anonyme.

### Modérateurs et administrateurs {#moderators-and-administrators}

Lorsque l’utilisateur connecté dispose de privilèges de modérateur ou d’administrateur, il peut se charger d’[activités de modération](/help/communities/moderate-ugc.md) (autorisées par la configuration du composant) pour tous les événements et commentaires de calendrier publiés pour un événement.

![modérateurs-vue](assets/moderators-view.png)

#### Membres {#members}

When the signed in user is a community member or [privileged member](/help/communities/users.md#privileged-members-group) (depending on configuration), they are able to select `New Event` to create and post a new calendar event.

Plus précisément, il est autorisé à:

* Créer un événement de calendrier
* Publier un commentaire sur un événement de calendrier
* Modifier leur propre événement de calendrier ou commentaire
* Supprimer leur propre événement de calendrier ou commentaire
* Marquer les événements ou commentaires du calendrier d’autres utilisateurs

![create-événement](assets/configure-calendar2.png)

![événement-post](assets/configure-calendar3.png)

#### Anonyme {#anonymous}

Les visiteurs non inscrits peuvent lire les événements de calendrier et les traduire lorsque cela est possible. Toutefois, ils ne sont pas autorisés à ajouter un événement ou un commentaire de calendrier, ni à marquer les événements ou les commentaires d’autres membres.

![anonyme-user-vue](assets/anonymous-user-view1.png)

## Informations supplémentaires {#additional-information}

More information may be found on the [Calendar Essentials](/help/communities/calendar-basics-for-developers.md) page for developers.

Pour des informations sur la modération des événements et des commentaires de calendrier, voir [Modération de contenu généré par les utilisateurs](/help/communities/moderate-ugc.md).

For tagging calendar events and comments, see [Tagging User Generated Content](/help/communities/tag-ugc.md).

For translation of calendar events and comments, see [Translating User Generated Content](/help/communities/translate-ugc.md).
