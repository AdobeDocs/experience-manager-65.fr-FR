---
title: Fonction Calendrier
seo-title: Calendar Feature
description: Fournit des informations sur les événements de la communauté au format calendrier
seo-description: Provides community event information in a calendar format
uuid: 262f6afa-d8aa-4815-8440-a8ed5668c76d
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 70fa0b9c-cb98-45c4-9c94-bef4a9f3741e
docset: aem65
exl-id: c9b34b00-525d-4ca3-bd18-11bb7ce66787
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1160'
ht-degree: 42%

---

# Fonction Calendrier {#calendar-feature}

## Présentation  {#introduction}

La fonction Calendrier offre des informations relatives aux événements de la communauté dans un calendrier. Sont concernés tous les visiteurs ou uniquement ceux qui sont inscrits (membres de la communauté). Tous les membres autorisés peuvent ajouter des événements.

Cette section de la documentation décrit :

* Ajout de la fonction Calendrier à un site AEM
* Paramètres de configuration pour `Calendar` components

## Ajout d’un calendrier à une page {#adding-a-calendar-to-a-page}

Pour ajouter une `Calendar` sur une page en mode création, utilisez l’explorateur de composants pour accéder à

* `Communities / Calendar`

et faites glisser le composant sur une page, par exemple à un endroit relatif à la fonction, pour permettre aux utilisateurs de le consulter.

Pour obtenir les informations nécessaires, consultez la section [Principes de base des composants des communautés](/help/communities/basics.md).

Lorsque la variable [bibliothèques côté client requises](/help/communities/calendar-basics-for-developers.md#essentials-for-client-side) sont incluses, c’est ainsi que la variable `Calendar` s’affiche.

![calendar-component](assets/calendar-component.png)

### Configuration du calendrier {#configuring-calendar}

Sélectionnez le `Calendar` pour accéder au composant et le sélectionner. `Configure` qui ouvre la boîte de dialogue de modification.

![configure](assets/configure-new.png)

![configure-calendar](assets/configure-calendar1.png)

#### Onglet Settings {#settings-tab}

Sous , **Paramètres** , indiquez si les balises doivent être appliquées aux entrées de calendrier.

* **Événements par page**

   Définit le nombre d’événements affichés par page. La valeur par défaut est 10.

* **Modéré**

   Si cette case est cochée, la publication des événements et commentaires du calendrier doit être approuvée avant d’apparaître sur un site de publication. Cette option n’est pas cochée par défaut.

* **Fermé**

   Si cette case est cochée, le calendrier est fermé aux nouvelles entrées et commentaires d’événement. Cette option n’est pas cochée par défaut.

* **Éditeur de texte enrichi**

   Si cette case est cochée, les événements et les commentaires du calendrier peuvent être saisis avec une annotation. Cette option est cochée par défaut.

* **Autoriser le balisage**

   Si cette case est cochée, les membres ont le droit d’ajouter des libellés de balise aux événements qu’ils publient (voir **Champ de balise** ). Cette option est cochée par défaut.

* **Autoriser les transferts de fichiers**

   Si cette case est cochée, les fichiers joints peuvent être ajoutés à un événement ou à un commentaire de calendrier. Cette option est cochée par défaut.

* **Autoriser abonnement**

   Si cette case est cochée, les membres ont le droit de suivre les événements publiés dans le calendrier. Cette option est cochée par défaut.

* **Taille maximale du fichier**

   Pertinent uniquement si `Allow File Uploads` est cochée. Ce champ limite la taille (en octets) d’un fichier chargé. La valeur par défaut est 104857600 (10 Mo).

* **Types de fichier autorisés**

   Pertinent uniquement si `Allow File Uploads` est cochée. Liste d’extensions de fichier séparées par des virgules avec le séparateur &quot;point&quot;. Par exemple : .jpg, .jpeg, .png, .doc, .docx, .pdf. Si des types de fichiers sont spécifiés, ceux qui ne sont pas spécifiés ne seront pas autorisés à être chargés. Par défaut, aucun n’est spécifié, de sorte que tous les types de fichiers soient autorisés.

* **Taille max. du fichier image joint**

   À définir uniquement si l’option Autoriser les chargements de fichiers est cochée. Taille maximale en octets pour un fichier image chargé. La valeur par défaut est 2097152** **(2 Mo).

* **Types autorisés d’image de couverture**

   Liste séparée par des virgules d’extensions de fichier image avec le séparateur &quot;point&quot;. La valeur par défaut est `.jpg,.jpeg,.png,.gif,.bmp`.

* **Autoriser les réponses à thème**

   Si cette case est cochée, les réponses aux commentaires sont publiées sur l’événement de calendrier. Cette option est cochée par défaut.

* **Autoriser les utilisateurs à supprimer les commentaires et événements**

   Si cette case est cochée, autorisez les membres à supprimer les commentaires et les événements de calendrier qu’ils ont publiés. La valeur par défaut est****cochée.

* **Autoriser le vote**

   Si cette case est cochée, la fonction de vote est ajoutée à un événement de calendrier. Cette option est cochée par défaut.

* **Afficher le fil d’Ariane**

   Afficher le fil d’Ariane sur la page des événements. Cette option est cochée par défaut.

* **Filtre de plage de dates**

   Définit le nombre de jours ajoutés à la date actuelle afin de calculer la valeur &quot;À&quot; du filtre de la page de liste des événements du calendrier. La valeur par défaut est 30.

* **Autoriser le contenu proposé**

   Si cette case est cochée, l’idée peut être identifiée comme [contenu proposé](/help/communities/featured.md). Cette option n’est pas cochée par défaut.

Sous , **Modération d’utilisateur** , indiquez comment les sujets et réponses publiés (contenu généré par l’utilisateur) sont gérés. Pour plus d’informations, voir [Modération de contenu généré par les utilisateurs](/help/communities/moderate-ugc.md).

#### Onglet Modération d’utilisateur {#user-moderation-tab}

* **Refuser les publications**

   Si cette case est cochée, les modérateurs membres approuvés sont autorisés à refuser des publications et à empêcher que la publication ne s’affiche sur le forum public. Cette option est cochée par défaut.

* **Fermer/rouvrir les événements**

   Si cette case est cochée, les membres modérateurs autorisés peuvent fermer un événement pour ajouter des modifications et des commentaires, et peuvent également rouvrir un événement. Cette option est cochée par défaut.

* **Marquer les publications**

   Si cette case est cochée, les membres ont le droit de signaler les événements ou commentaires d’autres personnes comme étant inappropriés. Cette option est cochée par défaut.

* **Marquer la liste de motifs**

   Si cette case est cochée, les membres ont le droit de choisir dans une liste déroulante la raison pour laquelle ils ont marqué un événement ou un commentaire comme étant inapproprié. Cette option n’est pas cochée par défaut.

* **Motif de la marque personnalisée**

   Si cette case est cochée, autorisez les membres à indiquer leur propre motif de marquage d’un événement ou d’un commentaire comme étant inapproprié. Cette option n’est pas cochée par défaut.

* **Seuil de modération**

   Saisissez le nombre de fois qu’un événement ou un commentaire doit être marqué par les membres avant que les modérateurs ne soient informés. La valeur par défaut est 1 (une fois).

* **Limite de marquage**

   Saisissez le nombre de fois qu’un événement ou un commentaire doit être marqué avant qu’il ne soit plus visible pour le public. Si la valeur est -1, le sujet ou le commentaire marqué est toujours visible pour le public. Dans le cas contraire, cette valeur doit être supérieure ou égale au seuil de modération. La valeur par défaut est 5.

#### Onglet Champ de balise {#tag-field-tab}

Dans l’onglet **Champ de balise**, les balises qui peuvent être appliquées, si l’option est activée dans l’onglet **Paramètres**, sont limitées selon les espaces de noms sélectionnés.

* **Espaces de noms autorisés**

   Pertinent si `Allow Tagging` est coché sous **Paramètres** . Les balises pouvant être appliquées se limitent à celles liées aux catégories d’espace de noms cochées. La liste des espaces de noms inclut &quot;Balises standard&quot; (l’espace de noms par défaut) ainsi que &quot;Inclure toutes les balises&quot;. La valeur par défaut n’est pas cochée, ce qui signifie que tous les espaces de noms sont autorisés.

* **Limite de suggestions**

   Saisissez le nombre de balises à afficher comme suggestion au membre qui publie sur le forum. La valeur par défaut est **-**1 (aucune limite).

>[!NOTE]
>
>Consultez la rubrique [Administration des balises](/help/sites-administering/tags.md) pour savoir comment ajouter un espace de noms de balise (taxonomie).

#### Onglet Traduction {#translation-tab}

Sous l’onglet **Traduction**, si la traduction est activée pour le site de la communauté, elle peut être définie de sorte à traduire le fil d’Ariane entier (événement et commentaires) au lieu de certaines publications.

* **Tout traduire**

   Si cette case est cochée, l’événement et les commentaires sont traduits dans la langue préférée de l’utilisateur. Cette option est cochée par défaut.

## Expérience des visiteurs {#site-visitor-experience}

Dans l’environnement de publication, la fonction Calendrier présente un champ de recherche avec une plage de dates par défaut et tous les événements de calendrier prévus pour cette plage.

Lorsqu’un événement de calendrier est sélectionné, ses détails, sa description et ses commentaires sont affichés.

Les autres choix varient selon que le visiteur est modérateur, administrateur, membre de la communauté, membre privilégié ou anonyme.

### Modérateurs et administrateurs {#moderators-and-administrators}

Lorsque l’utilisateur connecté dispose de privilèges de modérateur ou d’administrateur, il peut se charger d’[activités de modération](/help/communities/moderate-ugc.md) (autorisées par la configuration du composant) pour tous les événements et commentaires de calendrier publiés pour un événement.

![modérateurs-view](assets/moderators-view.png)

#### Membres {#members}

Lorsque l’utilisateur connecté est membre de la communauté ou [membre privilégié](/help/communities/users.md#privileged-members-group) (selon la configuration), ils peuvent sélectionner `New Event` pour créer et publier un événement de calendrier.

Plus précisément, il est autorisé à:

* Créer un événement de calendrier
* Publication d’un commentaire sur un événement de calendrier
* Modifier leur propre événement ou commentaire de calendrier
* Suppression d’un événement ou d’un commentaire de calendrier
* Marquer les événements ou commentaires de calendrier d’autres

![create-event](assets/configure-calendar2.png)

![event-post](assets/configure-calendar3.png)

#### Anonyme {#anonymous}

Les visiteurs non inscrits peuvent lire les événements de calendrier et les traduire lorsque cela est possible. Toutefois, ils ne sont pas autorisés à ajouter un événement ou un commentaire de calendrier, ni à marquer les événements ou les commentaires d’autres membres.

![anonymous-user-view](assets/anonymous-user-view1.png)

## Informations supplémentaires {#additional-information}

Vous trouverez plus d’informations sur la [Principes de base du calendrier](/help/communities/calendar-basics-for-developers.md) pour les développeurs.

Pour des informations sur la modération des événements et des commentaires de calendrier, voir [Modération de contenu généré par les utilisateurs](/help/communities/moderate-ugc.md).

Pour baliser des événements et des commentaires de calendrier, voir [Balisage du contenu généré par l’utilisateur](/help/communities/tag-ugc.md).

Pour consulter la traduction des événements et des commentaires de calendrier, voir [Traduction de contenu généré par l’utilisateur](/help/communities/translate-ugc.md).
