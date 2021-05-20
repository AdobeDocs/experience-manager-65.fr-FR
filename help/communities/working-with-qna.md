---
title: Fonction Forum Q&R
seo-title: Fonction Forum Q&R
description: Ajout de la fonction Forum Q&R à une page
seo-description: Ajout de la fonction Forum Q&R à une page
uuid: e0d95009-0d04-4fa7-8d05-5948c4e37f08
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 6e6ffe09-c50b-4238-8b8c-597c133d0a9e
docset: aem65
exl-id: 17081710-35e0-4f5b-9485-1f85c065fd70
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1380'
ht-degree: 19%

---

# Fonction Forum Q&amp;R{#q-a-forum-feature}

## Présentation {#introduction}

La fonction Forum Q&amp;R (questions et réponses) offre aux membres de la communauté un espace où poser leurs questions et y répondre. Il permet aux membres de :

* Créer de nouvelles questions
* Ajout d’images intégrées (avec prise en charge du glisser-déposer)
* Afficher et répondre aux questions
* Recherche d’une question
* Aider à modérer le contenu Q&amp;R
* Identifier les meilleures réponses
* Déplacer des questions Q&amp;R d’une page vers une autre

La documentation décrit :

* Ajout de la fonction Forum Q&amp;R à un site AEM.
* Paramètres de configuration du composant `QnA`.

## Ajout d’un forum Q&amp;R à une page {#adding-a-q-a-forum-to-a-page}

Pour ajouter un composant `QnA` à une page en mode création, utilisez l’explorateur de composants pour localiser `Communities / QnA` et faites-le glisser sur une page où le forum Q&amp;R doit apparaître.

Pour plus d’informations, voir [Principes de base des composants des communautés](/help/communities/basics.md).

Lorsque les [bibliothèques côté client requises](/help/communities/qna-essentials.md#essentials-for-client-side) sont incluses, voici comment le composant `QnA` apparaît :

![qna-component](assets/qna-component.png)

### Configuration de Q&amp;R {#configuring-qna}

Sélectionnez le composant `QnA` inséré pour y accéder et sélectionnez l’icône `Configure` qui ouvre la boîte de dialogue de modification.

![configure](assets/configure-new.png)

![qna-config](assets/qna-config.png)

#### Onglet Settings {#settings-tab}

Sous l’onglet **Paramètres**, spécifiez les paramètres pour les sujets (questions) et les réponses :

* **Autoriser les miniatures de pièces jointes**

   Si cette case est cochée, une miniature de l’image jointe est créée.

* **Taille max. des miniatures de pièces jointes**

   Taille maximale (en pixels) de l’image miniature de la pièce jointe. La valeur par défaut est 800 x 800.

* **Taille d’image minimale pour la miniature**

   Taille minimale (en octets) de l’image pour générer une miniature pour les images intégrées. La valeur par défaut est de 100000 octets (100 Ko).

* **Taille maximale de la miniature**

   Taille maximale (en pixels) de la miniature de l’image intégrée. La valeur par défaut est 800 x 800.

* **Sujets par page**

   Définit le nombre de questions/publications affichées par page. La valeur par défaut est 10.

* **Modéré**

   Si cette case est cochée, la publication des sujets et des commentaires doit être approuvée avant d’apparaître sur un site de publication. La valeur par défaut est désélectionnée.

* **Fermé**

   Si cette case est cochée, le forum est fermé aux nouvelles questions et commentaires. La valeur par défaut est désélectionnée.

* **Éditeur de texte enrichi**

   Si cette case est cochée, les sujets et les commentaires peuvent être saisis avec une annotation. La valeur par défaut est désélectionnée.

* **Autoriser le balisage**

   Si cette case est cochée, les membres ont le droit d’ajouter des libellés de balise à leur publication (voir l’onglet **Champ de balise** ). La valeur par défaut est désélectionnée.

* **Autoriser les transferts de fichiers**

   Si cette option est cochée, des pièces jointes peuvent être ajoutées à la question ou au commentaire. La valeur par défaut est désélectionnée.

* **Autoriser abonnement**

   Si cette case est cochée, incluez la fonction suivante pour les publications de forum, ce qui permet aux membres d’être [informés](/help/communities/notifications.md) des nouvelles publications. La valeur par défaut est désélectionnée.

* **Autoriser l’épinglage**

   Si cette case est cochée, les rubriques des forums peuvent être collées en haut de la liste des rubriques. La valeur par défaut est désélectionnée.

* **Autoriser les abonnements par courrier électronique**

   Si cette case est cochée, autorisez les membres à être informés des nouvelles publications par e-mail ([subscription](/help/communities/subscriptions.md)). Nécessite que l’option Autoriser le suivi soit cochée et que l’adresse [email soit ](/help/communities/email.md) configurée. La valeur par défaut est désélectionnée.

* **Taille maximale du fichier**

   Convient uniquement si `Allow File Uploads` est coché. Ce champ limite la taille (en octets) d’un fichier chargé. La valeur par défaut est 104857600 (10 Mo).

* **Types de fichier autorisés**

   Convient uniquement si `Allow File Uploads` est coché. Liste d’extensions de fichier séparées par des virgules avec le séparateur &quot;point&quot;. Par exemple : .jpg, .jpeg, .png, .doc, .docx, .pdf. Si des types de fichiers sont spécifiés, ceux qui ne sont pas spécifiés ne sont pas autorisés à être chargés. Par défaut, aucun n’est spécifié, de sorte que** ** tous les types de fichiers soient autorisés.

* **Taille max. du fichier image joint**

   À définir uniquement si l’option Autoriser les chargements de fichiers est cochée. Nombre maximal d’octets qu’un fichier image chargé peut contenir. La valeur par défaut est 2097152 (2 Mo).

* **Permettre des réponses**

   Si cette case est cochée, les réponses aux commentaires sont publiées pour la question. La valeur par défaut est désélectionnée.

* **Autoriser le vote**

   Si cette option est cochée, la fonction de vote est ajoutée à une question. La valeur par défaut est désélectionnée.

* **Autoriser les utilisateurs à supprimer les commentaires et sujets**

   Si cette case est cochée, autorisez les membres à supprimer les commentaires et questions qu’ils ont publiés. La valeur par défaut est désélectionnée.

* **Autoriser les membres privilégiés**

   Si cette case est cochée, seuls les membres privilégiés sont autorisés à créer du contenu.

* **Bloquer le contenu généré par l’utilisateur en mode d’édition d’auteur**

   S’il est activé, bloque le contenu généré par l’utilisateur lors de la modification en mode création.

* **Déplacer la réponse sélectionnée vers le haut**

   Si cette case est cochée, la première réponse affichée est une réponse sélectionnée. La valeur par défaut est désélectionnée.
* **Afficher les badges**

   Si cette case est cochée, affichez les [badges](/help/communities/implementing-scoring.md) gagnés et attribués avec l’entrée de blog d’un membre. La valeur par défaut est désélectionnée.

* **Autoriser le contenu proposé**

   si cette case est cochée, l’idée peut être identifiée en tant que [contenu présenté](/help/communities/featured.md). La valeur par défaut est désélectionnée.

* **Activer la mention**

   S’il est activé, permet aux utilisateurs enregistrés de la communauté d’identifier d’autres membres enregistrés (à l’aide du prénom, du nom, du nom d’utilisateur) et de les baliser à l’aide de la syntaxe @user-name courante. Les utilisateurs balisés reçoivent des notifications sur leurs mentions.

* **Nombre max. de mentions**

   Limitez le nombre maximal de mentions autorisées dans une publication. La valeur par défaut est 10.

* **Modèle des mentions de l’IU**

   Spécifiez la chaîne de modèle autorisée à baliser (@mention) l’utilisateur enregistré dans une publication. Par exemple, `~{{familyName}}{{givenName}}`.

#### Onglet Modération d’utilisateur {#user-moderation-tab}

Sous l’onglet **Modération d’utilisateur** , indiquez comment les sujets publiés (questions) et les réponses (contenu généré par l’utilisateur) sont gérés. Pour plus d’informations, voir [Modération de contenu généré par les utilisateurs](/help/communities/moderate-ugc.md).

* **Refuser les réponses**

   Si cette case est cochée, les modérateurs membres approuvés sont autorisés à refuser les réponses publiées et à empêcher l’affichage de la réponse sur le forum Q&amp;R public. La valeur par défaut est désélectionnée.

* **Fermer/rouvrir les sujets**

   Si cette case est cochée, les membres modérateurs autorisés peuvent fermer une question (rubrique) pour apporter d’autres modifications et réponses, puis rouvrir une question. La valeur par défaut est désélectionnée.

* **Déplacer les**
rubriques Si cette option est cochée, les modérateurs côté publication peuvent déplacer les questions. La valeur par défaut est désélectionnée.

* **Marquer les publications**

   Si cette option est cochée, les membres ont le droit de signaler les questions ou réponses des autres comme étant inappropriées. La valeur par défaut est désélectionnée.

* **Marquer la liste de motifs**

   Si cette case est cochée, les membres ont le droit de choisir dans une liste déroulante la raison pour laquelle ils ont marqué une question ou une réponse comme étant inappropriée. La valeur par défaut est désélectionnée.

* **Motif de la marque personnalisée**

   Si cette option est cochée, les membres ont le droit de préciser la raison pour laquelle ils ont marqué une question ou une réponse comme étant inappropriée. La valeur par défaut est désélectionnée.

* **Seuil de modération**

   Saisissez le nombre de fois qu’une question ou une réponse doit être marquée par les membres avant que les modérateurs ne soient informés. La valeur par défaut est 1 (une fois).

* **Limite de marquage**

   Saisissez le nombre de fois qu&#39;une question ou une réponse doit être marquée avant qu&#39;elle ne soit plus visible pour le public. Si la valeur est -1, la question ou la réponse marquée est toujours visible pour le public. Dans le cas contraire, cette valeur doit être supérieure ou égale au seuil de modération. La valeur par défaut est 5.

#### Onglet Champ de balise {#tag-field-tab}

Sous l’onglet **Champ de balise** , les balises qui peuvent être appliquées, si elles sont autorisées sous l’onglet **Paramètres**, sont limitées en fonction des espaces de noms choisis.

* **Espaces de noms autorisés**

   Convient si `Allow Tagging` est coché sous l’onglet **Paramètres**. Les balises qui peuvent être appliquées sont limitées aux catégories d’espace de noms cochées. La liste des espaces de noms inclut &quot;Balises standard&quot; (espace de noms par défaut) et &quot;Inclure toutes les balises&quot;. La valeur par défaut n’est pas cochée, ce qui signifie que tous les espaces de noms sont autorisés.

* **Limite de suggestions**

   Saisissez le nombre de balises à afficher comme suggestion au membre qui publie sur le forum. Une valeur **-**1 signifie qu’aucune limite n’est définie. La valeur par défaut est 0.

#### Onglet Paramètres de tri {#sort-settings-tab}

Sous l’onglet **Paramètres de tri**, indiquez comment les commentaires publiés sont triés lorsqu’ils sont affichés.

* **Trier par**

   Cochez toutes les sélections de tri autorisées : `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. La valeur par défaut est `Newest, Oldest, Last Updated`.

* **Définir par défaut**

   Extrayez pour sélectionner l’une des options de tri cochées à afficher par défaut. La valeur par défaut est `Newest`.

* **Sélectionner les options de temps pour le tri Analytics**

   Déposez pour sélectionner l’une des `All, Last 24 Hours, Last 7 Days, Last 30 Days`. La valeur par défaut est `All`.

## Expérience des visiteurs {#site-visitor-experience}

### Identification des réponses {#identifying-answers}

Une réponse peut être indiquée comme réponse correcte ou utile à l&#39;aide du bouton `Select Answer`. Une fois qu&#39;une question est marquée comme &quot;A répondre&quot;, une autre réponse ne peut pas être sélectionnée tant que la première n&#39;a pas été désélectionnée à l&#39;aide du bouton `Unmark Chosen Answer`.

Une fois sélectionnée comme réponse viable, elle peut être désélectionnée à l’aide du bouton `Unmark Chosen Answer`.

Une fois qu’une réponse est sélectionnée comme réponse viable, une indication que la question a été `Answered` s’affiche en regard du sujet de la question sur la page principale Q&amp;R.

#### Modérateurs et administrateurs {#moderators-and-administrators}

Lorsque l’utilisateur connecté dispose de privilèges de modérateur ou d’administrateur, il peut se charger d’activités de modération autorisées par la configuration du composant, peu importe qui a créé la question ou la réponse.

Ils peuvent également identifier les réponses.

#### Membres {#members}

Lorsque les visiteurs du site sont connectés, en fonction de la configuration, ils peuvent :

* Posez une nouvelle question.
* Modifiez ou supprimez les questions qu’ils ont créées.
* Marquez les questions ou réponses des autres membres.
* Identifiez les réponses aux questions qu’ils ont créées.

#### Anonyme {#anonymous}

Les visiteurs qui ne sont pas connectés peuvent uniquement lire les questions et réponses publiées, les traduire s’ils sont pris en charge, mais ne peuvent ni ajouter de question, ni répondre, ni marquer les publications d’autres personnes.

## Informations supplémentaires {#additional-information}

Vous trouverez plus d’informations sur la page [Notions fondamentales sur la qualité de l’expérience](/help/communities/qna-essentials.md) pour les développeurs.

Pour des informations sur la modération des sujets et des commentaires publiés, reportez-vous à la section [Modération du contenu généré par l’utilisateur](/help/communities/moderate-ugc.md).

Pour baliser les sujets et les commentaires publiés, voir [Balisage de contenu généré par l’utilisateur](/help/communities/tag-ugc.md).
