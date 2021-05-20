---
title: Fonctionnalité d’orientation
seo-title: Fonctionnalité d’orientation
description: Ajout et configuration de la fonction Idéation
seo-description: Ajout et configuration de la fonction Idéation
uuid: 38468290-6d00-4ee4-91d8-7c2e8ae32712
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: a3f5a21d-2df6-4663-a1ea-3a067c46f860
docset: aem65
exl-id: e130bab4-524d-4413-ba8b-53d0ed9e8623
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1124'
ht-degree: 28%

---

# Fonction d’information {#ideation-feature}

## Présentation {#introduction}

La fonction d’idéation fournit une zone pour les visiteurs connectés du site (membres de la communauté) dans l’environnement de publication afin que :

* Créez des idées à partager avec la communauté.
* Affichez et commentez des idées.
* Suis une idée !
* Votez pour une idée.

Cette section de la documentation décrit:

* Ajout de la fonction d’idéation à un site AEM.
* Paramètres de configuration du composant Idéation.

### Ajout d’une idée à une page {#adding-a-ideation-to-a-page}

Pour ajouter un composant `Ideation` à une page en mode création, utilisez l’explorateur de composants pour accéder à :

* `Communities / Ideation`

et faites-le glisser sur la page où l’idée doit apparaître.

Pour plus d’informations, voir [Principes de base des composants des communautés](/help/communities/basics.md).

Lorsque les [bibliothèques côté client requises](/help/communities/ideation.md#essentials-for-client-side) sont incluses, voici comment le composant `Ideation` apparaîtra :

![idéation](assets/ideation.png)

### Configuration d’une idée {#configuring-an-ideation}

Sélectionnez le composant `Ideation` inséré pour y accéder et sélectionnez l’icône `Configure` qui ouvre la boîte de dialogue de modification.

![configure-new](assets/configure-new.png)

![ideation-settings](assets/ideation-settings.png)

#### Onglet Settings {#settings-tab}

Sous l’onglet **[!UICONTROL Paramètres]**, spécifiez les paramètres des idées et des commentaires :

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

   Si cette case est cochée, la publication d’idées et de commentaires doit être approuvée avant d’apparaître sur un site de publication. Cette option n’est pas cochée par défaut.

* **Fermé**

   Si cette case est cochée, le forum d’idéation est fermé aux idées et commentaires nouveaux. Cette option n’est pas cochée par défaut.

* **Éditeur de texte enrichi**

   Si cette case est cochée, les idées et les commentaires peuvent être saisis avec des balises. Cette option n’est pas cochée par défaut.

* **Autoriser le balisage**

   Si cette case est cochée, les membres ont le droit d’ajouter des libellés de balise à leur publication (voir l’onglet **[!UICONTROL Champ de balise]** ). Cette option n’est pas cochée par défaut.

* **Autoriser les transferts de fichiers**

   Si cette case est cochée, vous pouvez ajouter des pièces jointes à l’idée ou au commentaire. Cette option n’est pas cochée par défaut.

* **Taille maximale du fichier**

   Convient uniquement si `Allow File Uploads` est coché. Ce champ limite la taille (en octets) d’un fichier chargé. La valeur par défaut est 104857600 (10 Mo).

* **Types de fichier autorisés**

   Convient uniquement si `Allow File Uploads` est coché. Liste d’extensions de fichier séparées par des virgules avec le séparateur &quot;point&quot;. Par exemple : .jpg, .jpeg, .png, .doc, .docx, .pdf. Si des types de fichiers sont spécifiés, ceux qui ne sont pas spécifiés ne seront pas autorisés à être chargés. Par défaut, aucun n’est spécifié, de sorte que tous les types de fichiers soient autorisés.

* **Taille max. du fichier image joint**

   À définir uniquement si l’option Autoriser les chargements de fichiers est cochée. Taille maximale en octets pour un fichier image chargé. La valeur par défaut est 2097152 (2 Mo).

* **Permettre des réponses**

   Si cette case est cochée, les réponses aux commentaires sont publiées sur l’idée. Cette option n’est pas cochée par défaut.

* **Autoriser le vote**

   Si cette option est cochée, vous pouvez voter sur les commentaires d’une idée. Cette option n’est pas cochée par défaut.

* **Autoriser les utilisateurs à supprimer les commentaires et sujets**

   Si cette case est cochée, autorisez les membres à supprimer les commentaires et idées qu’ils ont publiés. Cette option n’est pas cochée par défaut.

* **Autoriser abonnement**

   Si cette case est cochée, incluez la fonction suivante pour les publications d’idées, ce qui permet aux membres d’être [informés](/help/communities/notifications.md) des nouvelles publications. Cette option n’est pas cochée par défaut.

* **Autoriser les abonnements par courrier électronique**

   Si cette case est cochée, autorisez les membres à être informés des nouvelles publications par e-mail ([subscription](/help/communities/subscriptions.md)). `Allow Following` doit être vérifié et [email configuré](/help/communities/email.md). Cette option n’est pas cochée par défaut.

* **Autoriser le vote**

   Si cette option est cochée, vous pouvez voter sur les commentaires d’une idée. Cette option n’est pas cochée par défaut.

* **Afficher les badges**

   Si cette case est cochée, affichez les [badges](/help/communities/implementing-scoring.md) gagnés et attribués avec l’idée d’un membre. Cette option n’est pas cochée par défaut.

* **Ne pas obtenir de réponses sur la page de liste**

* **Autoriser le contenu proposé**

   Si cette option est cochée, l’idée peut être identifiée en tant que [contenu présenté](/help/communities/featured.md). Cette option n’est pas cochée par défaut.

* **Activer la mention**
* **Nombre max. de mentions**
* **Modèle des mentions de l’IU**

#### Onglet Modération d’utilisateur {#user-moderation-tab}

Sous l’onglet **[!UICONTROL Modération d’utilisateur]** , indiquez comment les idées et commentaires publiés (contenu généré par l’utilisateur) sont gérés. Pour plus d’informations, voir [Modération de contenu généré par les utilisateurs](/help/communities/moderate-ugc.md).

* **Refuser les publications**

   Si cette case est cochée, les modérateurs membres approuvés sont autorisés à refuser des publications et à empêcher que la publication ne s’affiche sur le forum public. Cette option n’est pas cochée par défaut.

* **Fermer/rouvrir les sujets**

   Si cette case est cochée, les membres modérateurs autorisés peuvent fermer une rubrique pour ajouter d’autres modifications et commentaires et rouvrir une rubrique. Cette option n’est pas cochée par défaut.

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

Dans l’onglet **[!UICONTROL Champ de balise]**, les balises qui peuvent être appliquées, si l’option est activée dans l’onglet **[!UICONTROL Paramètres]**, sont limitées selon les espaces de noms sélectionnés.

* **Espaces de noms autorisés**

   Convient si `Allow Tagging` est coché sous l’onglet **[!UICONTROL Paramètres]**. Les balises pouvant être appliquées se limitent à celles liées aux catégories d’espace de noms cochées. La liste des espaces de noms inclut &quot;Balises standard&quot; (l’espace de noms par défaut) ainsi que &quot;Inclure toutes les balises&quot;. La valeur par défaut n’est pas cochée, ce qui signifie que tous les espaces de noms sont autorisés.

* **Limite de suggestions**

   Saisissez le nombre de balises à afficher comme suggestion au membre qui publie sur le forum. Une valeur **-1** ne signifie aucune limite. La valeur par défaut est 0.

#### Onglet Paramètres de tri {#sort-settings-tab}

Sous l’onglet **[!UICONTROL Paramètres de tri]**, indiquez comment les commentaires publiés sont triés lorsqu’ils sont affichés.

* **Trier par**

   Cochez toutes les sélections de tri autorisées : `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. La valeur par défaut est `Newest, Oldest, Last Updated`.

* **Définir par défaut**

   Extrayez pour sélectionner l’une des options de tri cochées à afficher par défaut. La valeur par défaut est `Newest`.

* **Sélectionner les options de temps pour le tri Analytics**

   Appuyez sur la touche pour sélectionner l’une des valeurs `All, Last 24 Hours, Last 7 Days, Last 30 Days`. La valeur par défaut est `All`.

## Expérience des visiteurs {#site-visitor-experience}

### Création d’une idée {#creating-idea}

Comme pour toutes les fonctionnalités de Communities, si elle n’est pas connectée, un visiteur du site ne peut lire que des idées et consulter d’autres opinions (par le biais de commentaires et de votes/commentaires).

Une fois connecté, un membre peut créer une nouvelle idée.

![create-new-idée](assets/create-new-idea.png)

Avant de soumettre l’idée, le membre peut enregistrer un brouillon.

En sélectionnant le bouton `Save as Draft`, un brouillon est enregistré.

![save-idée](assets/save-idea.png)

Lors de l’affichage de brouillons enregistrés dans l’onglet `My Drafts` , sélectionnez `Read More` pour revenir en mode d’édition :

![edit-idée](assets/edit-idea.png)

#### Fournir des commentaires {#providing-feedback}

Une fois l&#39;idée publiée, d&#39;autres membres peuvent se connecter, ouvrir l&#39;idée ( `Read More`) et aimer l&#39;idée, ajoutant ainsi au nombre de votes, et faire des commentaires.

![feedback](assets/feedback-idea.png)

### Informations supplémentaires {#additional-information}

Pour plus d’informations, reportez-vous à la page [Notions fondamentales sur les idées](/help/communities/ideation.md) pour les développeurs.

Pour des informations sur la modération des sujets et des commentaires publiés, reportez-vous à la section [Modération du contenu généré par l’utilisateur](/help/communities/moderate-ugc.md).

Pour baliser les sujets et les commentaires publiés, voir [Balisage de contenu généré par l’utilisateur](/help/communities/tag-ugc.md).
