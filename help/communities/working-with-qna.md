---
title: Fonction Forum Q&R
seo-title: Fonction Forum Q&R
description: Ajout de la fonctionnalité de forum QnA à une page
seo-description: Ajout de la fonctionnalité de forum QnA à une page
uuid: e0d95009-0d04-4fa7-8d05-5948c4e37f08
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 6e6ffe09-c50b-4238-8b8c-597c133d0a9e
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Fonction Forum Q&amp;R{#q-a-forum-feature}

## Présentation {#introduction}

La fonction de forum de la QnA (questions et réponses) offre aux membres de la communauté un espace où poser des questions et y répondre. Il permet aux membres de :

* Créer de nouvelles questions
* Ajout d’images intégrées (avec prise en charge du glisser-déposer)
* Afficher et répondre aux questions
* Rechercher une question
* Aidez à modérer le contenu de la QnA
* Identifier les meilleures réponses
* Déplacement des questions QnA d’une page vers une autre

La documentation décrit :

* l’ajout de la fonction Forum Q&amp;R aux paramètres de configuration.
* configuration settings for the `QnA`component.

## Ajout d’un forum Q&amp;R à une page {#adding-a-q-a-forum-to-a-page}

Pour ajouter un `QnA` composant à une page en mode création, utilisez l’explorateur de composants pour le localiser `Communities / QnA`et le faire glisser vers sa place sur une page où le forum QnA doit apparaître.

For necessary information, visit [Communities Components Basics](/help/communities/basics.md).

When the [required client-side libraries](/help/communities/qna-essentials.md#essentials-for-client-side) are included, this is how the `QnA`component appears:

![chlimage_1](assets/chlimage_1.png)

### Configuration de Q&amp;R {#configuring-qna}

Select the placed `QnA` component to access and select the `Configure` icon which opens the edit dialog.

![chlimage_1-1](assets/chlimage_1-1.png) - ![qna-config](assets/qna-config.png)

#### Onglet Settings {#settings-tab}

Sous l’onglet **Paramètres**, spécifiez les paramètres pour les sujets (questions) et les réponses :

* **Autoriser les miniatures de pièces jointes**

   Si cette option est cochée, une miniature de l’image jointe est créée.

* **Taille max. des miniatures de pièces jointes**

   Taille maximale (en pixels) de l’image miniature de la pièce jointe. La valeur par défaut est 800 x 800.

* **Taille d’image minimale pour la miniature**

   Taille minimale (en octets) de l’image pour la génération de vignettes pour les images en ligne. La valeur par défaut est 100 000 octets (100 Ko).

* **Taille maximale de la miniature**

   Taille maximale (en pixels) de l’image miniature pour l’image intégrée. La valeur par défaut est 800 x 800.

* **Sujets par page**

   Définit le nombre de questions/publications affichées par page. La valeur par défaut est 10.

* **Modéré**

   Si cette option est cochée, la publication des rubriques et des commentaires doit être approuvée avant qu’ils ne s’affichent sur un site de publication. La valeur par défaut est désélectionnée.

* **Fermé**

   Si cette option est cochée, le forum est fermé aux nouvelles questions et commentaires. La valeur par défaut est désélectionnée.

* **Éditeur de texte enrichi**

   Si cette option est cochée, les rubriques et les commentaires peuvent être saisis avec une annotation. La valeur par défaut est désélectionnée.

* **Autoriser le balisage**

   If checked, allow members to add tag labels to their post (see **Tag field** tab). La valeur par défaut est désélectionnée.

* **Autoriser les transferts de fichiers**

   Si cette option est cochée, autorisez l’ajout de pièces jointes à la question ou au commentaire. La valeur par défaut est désélectionnée.

* **Autoriser abonnement**

   Si cette option est cochée, incluez la fonctionnalité suivante pour les publications de forum, ce qui permet aux membres d’être [informés](/help/communities/notifications.md) des nouvelles publications. La valeur par défaut est désélectionnée.

* **Autoriser l’épinglage**

   Si cette option est cochée, les rubriques du forum peuvent être épinglées en haut de la liste des rubriques. La valeur par défaut est désélectionnée.

* **Autoriser les abonnements par courrier électronique**

   Si cette option est cochée, autorisez les membres à être informés des nouvelles publications par courrier électronique ([abonnement](/help/communities/subscriptions.md)). Requiert que l’option Autoriser le suivi soit cochée et que le [courrier électronique soit configuré](/help/communities/email.md). La valeur par défaut est désélectionnée.

* **Taille maximale du fichier**

   N’est pertinent que si `Allow File Uploads` est coché. Ce champ limite la taille (en octets) d’un fichier téléchargé. La valeur par défaut est 1 048 57 600 (10 Mo).

* **Types de fichier autorisés**

   N’est pertinent que si `Allow File Uploads` est coché. Liste d’extensions de fichiers séparées par des virgules avec le séparateur &quot;point&quot;. Par exemple : .jpg, .jpeg, .png, .doc, .docx, .pdf. Si des types de fichier sont spécifiés, ceux qui ne sont pas spécifiés ne sont pas autorisés à être téléchargés. La valeur par défaut n’est pas spécifiée, de sorte que** **tous les types de fichier sont autorisés.

* **Taille max. du fichier image joint**

   Applicable uniquement si l’option Autoriser les téléchargements de fichiers est cochée. nombre maximal d’octets qu’un fichier image téléchargé peut contenir. La valeur par défaut est 2097152** **(2 Mo).

* **Permettre des réponses**

   Si cette option est cochée, autorisez les réponses aux commentaires publiés sur la question. La valeur par défaut est désélectionnée.
* **Autoriser le vote**

   Si cette option est cochée, incluez la fonction de vote avec une question. La valeur par défaut est désélectionnée.

* **Autoriser les utilisateurs à supprimer les commentaires et sujets**

   Si cette option est cochée, autorisez les membres à supprimer les commentaires et questions qu’ils ont publiés. La valeur par défaut est** **désélectionnée.

* **Autoriser les membres privilégiés**

   Si cette option est cochée, seuls les membres privilégiés sont autorisés à créer du contenu.

* **Bloquer le contenu généré par l’utilisateur en mode d’édition d’auteur**

   S’il est activé, bloque le contenu généré par l’utilisateur lors de la modification en mode Auteur.

* **Déplacer la réponse sélectionnée vers le haut**Si cochée, la première réponse affichée est une réponse sélectionnée. La valeur par défaut est désélectionnée.
* **Afficher les badges**

   Si cette option est cochée, affichez les [badges](/help/communities/implementing-scoring.md) gagnés et attribués avec l&#39;entrée de blog d&#39;un membre. La valeur par défaut est désélectionnée.

* **Autoriser le contenu proposé**

   si cette option est cochée, l’idée peut être identifiée comme contenu [](/help/communities/featured.md)incitatif. La valeur par défaut est désélectionnée.

* **Activer la mention**

   S’il est activé, permet aux utilisateurs enregistrés de la communauté d’identifier d’autres membres enregistrés (à l’aide du prénom, du nom de famille, du nom d’utilisateur) et de les baliser à l’aide de la syntaxe @user-name courante. Les utilisateurs balisés reçoivent des notifications concernant leurs mentions.

* **Nombre max. de mentions**

   Limitez le nombre maximum de mentions autorisées dans une publication. La valeur par défaut est 10.

* **Modèle des mentions de l’IU**

   Spécifiez la chaîne de modèle autorisée à baliser (@mentions) l’utilisateur enregistré dans une publication. Par exemple : ~{{familyName}}{{donnname}}.

#### Onglet Modération utilisateur {#user-moderation-tab}

Under the **User Moderation** tab, specify how the posted topics (questions) and answers (user generated content) are managed. Pour plus d’informations, voir [Modération de contenu généré par les utilisateurs](/help/communities/moderate-ugc.md).

* **Refuser les réponses**

   Si cette option est cochée, les modérateurs membres de confiance sont autorisés à refuser les réponses affichées et à empêcher la réponse de s’afficher sur le forum public de questions-réponses. La valeur par défaut est désélectionnée.

* **Fermer/rouvrir les sujets**

   Si cette option est cochée, les modérateurs de membres de confiance peuvent fermer une question (rubrique) pour apporter d’autres modifications et réponses, ainsi que rouvrir une question. La valeur par défaut est désélectionnée.

* **Déplacer des rubriques** Si cette option est cochée, autorisez les modérateurs côté publication à déplacer des questions. La valeur par défaut est désélectionnée.

* **Marquer les publications**

   Si cette option est cochée, permettez aux membres de signaler que les questions ou réponses des autres personnes sont inappropriées. La valeur par défaut est désélectionnée.

* **Marquer la liste de motifs**

   Si cette option est cochée, permettez aux membres de choisir, dans une liste déroulante, la raison pour laquelle ils signalent une question ou une réponse comme étant inappropriée. La valeur par défaut est désélectionnée.

* **Motif de la marque personnalisée**

   Si cette option est cochée, autorisez les membres à indiquer leur propre raison de signaler une question ou une réponse comme étant inappropriée. La valeur par défaut est désélectionnée.

* **Seuil de modération**

   Entrez le nombre de fois où une question ou une réponse doit être signalée par les membres avant que les modérateurs ne soient avertis. La valeur par défaut est 1 (une fois).

* **Limite de marquage**

   Entrez le nombre de fois où une question ou une réponse doit être marquée avant d’être masquée de la vue publique. Si la valeur est -1, la question ou la réponse marquée est toujours visible pour le public. Dans le cas contraire, cette valeur doit être supérieure ou égale au seuil de modération. La valeur par défaut est 5.

#### Onglet Champ de balise {#tag-field-tab}

Under the **Tag field** tab, the tags that can be applied, if allowed under the **Settings **tab, are limited according to namespaces chosen.

* **Espaces de noms** autorisés Pertinents si `Allow Tagging` est coché sous l’onglet **Paramètres **Paramètres. Les balises qui peuvent être appliquées sont limitées à celles des catégories d’espace de noms cochées. La liste des espaces de noms comprend &quot;Balises standard&quot; (espace de noms par défaut) et &quot;Inclure toutes les balises&quot;. La valeur par défaut n’est pas cochée, ce qui signifie que tous les espaces de noms sont autorisés.

* **Limite de suggestions** Entrez le nombre de balises à afficher comme suggestion destinée au membre qui publie sur le forum. Une valeur **-**1 signifie aucune limite. La valeur par défaut est 0.

#### Onglet Paramètres de tri {#sort-settings-tab}

Sous l’onglet Paramètres **de** tri, spécifiez le mode de tri des commentaires publiés lorsqu’ils sont affichés.

* **Trier par**

   Vérifier toutes les sélections de tri autorisées : `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. La valeur par défaut est `Newest, Oldest, Last Updated`.

* **Définir par défaut**

   Appuyez sur la touche Bas pour sélectionner l’une des options de tri cochées et l’afficher comme valeur par défaut. La valeur par défaut est `Newest`.

* **Sélectionner les options de temps pour le tri Analytics**

   Déposez pour sélectionner l’un des `All, Last 24 Hours, Last 7 Days, Last 30 Days`. La valeur par défaut est `All`.

## Expérience des visiteurs {#site-visitor-experience}

### Identification des réponses {#identifying-answers}

Une réponse peut être marquée comme une réponse correcte ou utile à l&#39;aide du `Select Answer` bouton. Une fois qu&#39;une question est marquée comme Réponse, une autre réponse ne peut pas être sélectionnée tant que la première n&#39;a pas été désélectionnée à l&#39;aide du `Unmark Chosen Answer`bouton.

Une fois sélectionnée comme réponse viable, elle peut être désélectionnée à l’aide du `Unmark Chosen Answer` bouton.

Une fois qu’une réponse est sélectionnée comme réponse viable, une indication que la question a été `Answered`affichée en regard de la rubrique de la question sur la page QnA principale.

#### Modérateurs et administrateurs {#moderators-and-administrators}

Lorsque l’utilisateur connecté dispose de privilèges de modérateur ou d’administrateur, il peut se charger d’activités de modération autorisées par la configuration du composant, peu importe qui a créé la question ou la réponse.

Ils peuvent aussi identifier des réponses.

#### Membres {#members}

Lorsque les visiteurs du site sont connectés, selon la configuration, ils peuvent :

* poser une nouvelle question.
* modifier ou supprimer les questions qu’il a publiées.
* signaler les questions ou réponses des autres membres.
* identifier les réponses aux questions qu’ils ont posées.

#### Anonyme {#anonymous}

Les visiteurs du site qui ne sont pas connectés peuvent uniquement lire les questions et réponses publiées, les traduire s’ils sont pris en charge, mais ils ne peuvent ni ajouter de question ni répondre, ni marquer les publications des autres.

## Informations supplémentaires {#additional-information}

More information can be found on the [QnA Essentials](/help/communities/qna-essentials.md) page for developers.

Pour des informations sur la modération des sujets et des commentaires publiés, reportez-vous à la section [Modération du contenu généré par l’utilisateur](/help/communities/moderate-ugc.md).

Pour baliser les sujets et les commentaires publiés, voir [Balisage de contenu généré par l’utilisateur](/help/communities/tag-ugc.md).
