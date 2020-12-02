---
title: Fonction Forum Q&R
seo-title: Fonction Forum Q&R
description: Ajouter la fonction de forum QnA à une page
seo-description: Ajouter la fonction de forum QnA à une page
uuid: e0d95009-0d04-4fa7-8d05-5948c4e37f08
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 6e6ffe09-c50b-4238-8b8c-597c133d0a9e
docset: aem65
translation-type: tm+mt
source-git-commit: c190d5f223c85f6c49fea1391d8a3d2baff20192
workflow-type: tm+mt
source-wordcount: '1380'
ht-degree: 19%

---


# Fonction Forum Q&amp;R{#q-a-forum-feature}

## Présentation {#introduction}

La fonction de forum QnA (questions et réponses) offre aux membres de la communauté un espace où poser des questions et y répondre. Il permet aux membres :

* Créer de nouvelles questions
* Ajouter des images en ligne (avec prise en charge du glisser-déposer)
* Vue et réponses aux questions
* Rechercher une question
* Aider à modérer le contenu de QnA
* Identifier les meilleures réponses
* Déplacer les questions QnA d&#39;une page à une autre

La documentation décrit :

* Ajouter la fonction de forum QnA à un site AEM.
* Paramètres de configuration du composant `QnA`.

## Ajout d’un forum Q&amp;R à une page {#adding-a-q-a-forum-to-a-page}

Pour ajouter un composant `QnA` à une page en mode création, utilisez l&#39;explorateur de composants pour localiser `Communities / QnA` et faites-le glisser sur une page sur laquelle le forum QnA doit apparaître.

Pour obtenir les informations nécessaires, consultez [Community Components Basics](/help/communities/basics.md).

Lorsque les [bibliothèques client requises](/help/communities/qna-essentials.md#essentials-for-client-side) sont incluses, c&#39;est ainsi que le composant `QnA` apparaît :

![qna-component](assets/qna-component.png)

### Configuration de Q&amp;R {#configuring-qna}

Sélectionnez le composant `QnA` placé auquel accéder et sélectionnez l&#39;icône `Configure` qui ouvre la boîte de dialogue de modification.

![configurer](assets/configure-new.png)

![qna-config](assets/qna-config.png)

#### Onglet Settings {#settings-tab}

Sous l’onglet **Paramètres**, spécifiez les paramètres pour les sujets (questions) et les réponses :

* **Autoriser les miniatures de pièces jointes**

   Si cette option est cochée, une miniature de l’image jointe est créée.

* **Taille max. des miniatures de pièces jointes**

   Taille maximale (en pixels) de l’image miniature de la pièce jointe. La valeur par défaut est 800 x 800.

* **Taille d’image minimale pour la miniature**

   Taille minimale (en octets) de l’image pour la création de miniatures pour les images insérées. La valeur par défaut est de 100 000 octets (100 Ko).

* **Taille maximale de la miniature**

   Taille maximale (en pixels) de l’image miniature de l’image intégrée. La valeur par défaut est 800 x 800.

* **Sujets par page**

   Définit le nombre de questions/publications affichées par page. La valeur par défaut est 10.

* **Modéré**

   Si cette option est cochée, la publication des rubriques et commentaires doit être approuvée avant qu’ils n’apparaissent sur un site de publication. La valeur par défaut est désélectionnée.

* **Fermé**

   Si cette option est cochée, le forum est fermé aux nouvelles questions et observations. La valeur par défaut est désélectionnée.

* **Éditeur de texte enrichi**

   Si cette option est cochée, les rubriques et les commentaires peuvent être saisis avec une annotation. La valeur par défaut est désélectionnée.

* **Autoriser le balisage**

   Si cette option est cochée, autorisez les membres à ajouter des étiquettes de balise à leur publication (voir **onglet Champ de balise**). La valeur par défaut est désélectionnée.

* **Autoriser les transferts de fichiers**

   Si cette option est cochée, autorisez l&#39;ajout de pièces jointes à la question ou au commentaire. La valeur par défaut est désélectionnée.

* **Autoriser abonnement**

   Si cette option est cochée, incluez la fonction suivante pour les publications de forum, ce qui permet aux membres d’être [avertis](/help/communities/notifications.md) des nouvelles publications. La valeur par défaut est désélectionnée.

* **Autoriser l’épinglage**

   Si cette option est cochée, les sujets du forum peuvent être épinglés en haut de la liste des sujets. La valeur par défaut est désélectionnée.

* **Autoriser les abonnements par courrier électronique**

   Si cette option est cochée, autorisez les membres à être informés des nouvelles publications par courriel ([abonnement](/help/communities/subscriptions.md)). Nécessite que l’option Autoriser le suivi soit cochée et [que le courrier électronique soit configuré](/help/communities/email.md). La valeur par défaut est désélectionnée.

* **Taille maximale du fichier**

   Ne s&#39;applique que si `Allow File Uploads` est coché. Ce champ limite la taille (en octets) d’un fichier téléchargé. La valeur par défaut est 104857600 (10 Mo).

* **Types de fichier autorisés**

   Ne s&#39;applique que si `Allow File Uploads` est coché. Liste d’extensions de fichiers séparées par des virgules avec le séparateur &quot;point&quot;. Par exemple : .jpg, .jpeg, .png, .doc, .docx, .pdf. Si des types de fichier sont spécifiés, ceux qui ne sont pas spécifiés ne sont pas autorisés à être téléchargés. Aucune valeur par défaut n&#39;est spécifiée, de sorte que ** **tous les types de fichier soient autorisés.

* **Taille max. du fichier image joint**

   N’est pertinent que si l’option Autoriser les téléchargements de fichiers est cochée. Nombre maximal d’octets qu’un fichier image téléchargé peut contenir. La valeur par défaut est 2097152 (2 Mo).

* **Permettre des réponses**

   Si cette option est cochée, autorisez les réponses aux commentaires publiés sur la question. La valeur par défaut est désélectionnée.

* **Autoriser le vote**

   Si cette option est cochée, incluez la fonction de vote avec une question. La valeur par défaut est désélectionnée.

* **Autoriser les utilisateurs à supprimer les commentaires et sujets**

   Si cette option est cochée, autorisez les membres à supprimer les commentaires et questions qu’ils ont publiés. La valeur par défaut est désélectionnée.

* **Autoriser les membres privilégiés**

   Si cette case est cochée, seuls les membres privilégiés sont autorisés à créer du contenu.

* **Bloquer le contenu généré par l’utilisateur en mode d’édition d’auteur**

   Si cette option est activée, bloque le contenu généré par l’utilisateur lors de la modification en mode Auteur.

* **Déplacer la réponse sélectionnée vers le haut**

   Si cochée, la première réponse affichée est une réponse sélectionnée. La valeur par défaut est désélectionnée.
* **Afficher les badges**

   Si cette case est cochée, afficher les [badges](/help/communities/implementing-scoring.md) gagnés et attribués avec l&#39;entrée de blog d&#39;un membre. La valeur par défaut est désélectionnée.

* **Autoriser le contenu proposé**

   si cette option est cochée, l&#39;idée peut être identifiée comme [contenu incitatif](/help/communities/featured.md). La valeur par défaut est désélectionnée.

* **Activer la mention**

   S’il est activé, permet aux utilisateurs enregistrés de la communauté d’identifier d’autres membres enregistrés (à l’aide de leur prénom, de leur nom de famille, de leur nom d’utilisateur) et de les baliser à l’aide de la syntaxe courante de @user-name. Les utilisateurs balisés reçoivent des notifications concernant leurs mentions.

* **Nombre max. de mentions**

   Limitez le nombre maximum de mentions autorisées dans une publication. La valeur par défaut est 10.

* **Modèle des mentions de l’IU**

   Spécifiez la chaîne de modèle autorisée à baliser (@mentions) l’utilisateur enregistré dans une publication. Par exemple, `~{{familyName}}{{givenName}}`.

#### Onglet Modération utilisateur {#user-moderation-tab}

Sous l’onglet **Modération utilisateur**, spécifiez comment les rubriques publiées (questions) et les réponses (contenu généré par l’utilisateur) sont gérées. Pour plus d’informations, voir [Modération de contenu généré par les utilisateurs](/help/communities/moderate-ugc.md).

* **Refuser les réponses**

   Si cette option est cochée, les modérateurs membres de confiance sont autorisés à refuser les réponses affichées et à empêcher la réponse de s&#39;afficher sur le forum public de questions-réponses. La valeur par défaut est désélectionnée.

* **Fermer/rouvrir les sujets**

   Si cette option est cochée, les modérateurs membres approuvés peuvent fermer une question (rubrique) pour apporter d&#39;autres modifications et réponses, et également rouvrir une question. La valeur par défaut est désélectionnée.

* **Déplacer des**
rubriquesSi cette option est cochée, autorisez les modérateurs côté publication à déplacer les questions. La valeur par défaut est désélectionnée.

* **Marquer les publications**

   Si cette option est cochée, permettez aux membres de signaler que les questions ou réponses des autres personnes sont inappropriées. La valeur par défaut est désélectionnée.

* **Marquer la liste de motifs**

   Si cette option est cochée, permettez aux membres de choisir, dans une liste déroulante, la raison pour laquelle ils signalent une question ou une réponse comme inappropriée. La valeur par défaut est désélectionnée.

* **Motif de la marque personnalisée**

   Si cette option est cochée, autorisez les membres à indiquer leur propre raison de signaler une question ou une réponse comme inappropriée. La valeur par défaut est désélectionnée.

* **Seuil de modération**

   Entrez le nombre de fois où une question ou une réponse doit être signalée par les membres avant que les modérateurs ne soient avertis. La valeur par défaut est 1 (une fois).

* **Limite de marquage**

   Entrez le nombre de fois où une question ou une réponse doit être marquée avant d&#39;être masquée de la vue publique. Si la valeur est -1, la question ou la réponse marquée est toujours visible pour le public. Dans le cas contraire, cette valeur doit être supérieure ou égale au seuil de modération. La valeur par défaut est 5.

#### Onglet Champ de balise {#tag-field-tab}

Sous l&#39;onglet **Tag field**, les balises qui peuvent être appliquées, si elles sont autorisées sous l&#39;onglet **Settings**, sont limitées en fonction des espaces de nommage choisis.

* **Espaces de noms autorisés**

   Pertinent si `Allow Tagging` est coché sous l&#39;onglet **Paramètres**. Les balises qui peuvent être appliquées sont limitées à celles qui se trouvent dans les catégories d’espace de nommage vérifiées. La liste des espaces de nommage inclut &quot;Balises standard&quot; (l’espace de nommage par défaut) et &quot;Inclure toutes les balises&quot;. La valeur par défaut n’est pas cochée, ce qui signifie que tous les espaces de nommage sont autorisés.

* **Limite de suggestions**

   Entrez le nombre de balises à afficher comme suggestion au membre qui publie sur le forum. Une valeur **-**1 signifie qu’aucune limite n’est définie. La valeur par défaut est 0.

#### Onglet Paramètres de tri {#sort-settings-tab}

Sous l’onglet **Paramètres de tri**, spécifiez le mode de tri des commentaires publiés lorsqu’ils s’affichent.

* **Trier par**

   Cochez toutes les sélections de tri autorisées : `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. La valeur par défaut est `Newest, Oldest, Last Updated`.

* **Définir par défaut**

   Appuyez sur la touche Ctrl pour sélectionner l’une des options de tri cochées pour qu’elle s’affiche par défaut. La valeur par défaut est `Newest`.

* **Sélectionner les options de temps pour le tri Analytics**

   Déposez pour sélectionner l&#39;un des `All, Last 24 Hours, Last 7 Days, Last 30 Days`. La valeur par défaut est `All`.

## Expérience des visiteurs {#site-visitor-experience}

### Identification des réponses {#identifying-answers}

Une réponse peut être marquée comme une réponse correcte ou utile à l&#39;aide du bouton `Select Answer`. Une fois qu&#39;une question est marquée comme Réponse, une autre réponse ne peut pas être sélectionnée tant que la première n&#39;a pas été désélectionnée à l&#39;aide du bouton `Unmark Chosen Answer`.

Une fois sélectionnée comme réponse viable, elle peut être désélectionnée à l’aide du bouton `Unmark Chosen Answer`.

Une fois qu&#39;une réponse est sélectionnée comme réponse viable, une indication que la question a été `Answered` s&#39;affiche en regard de la rubrique de la question sur la page principale QnA.

#### Modérateurs et administrateurs {#moderators-and-administrators}

Lorsque l’utilisateur connecté dispose de privilèges de modérateur ou d’administrateur, il peut se charger d’activités de modération autorisées par la configuration du composant, peu importe qui a créé la question ou la réponse.

Ils peuvent aussi identifier les réponses.

#### Membres {#members}

Lorsque les visiteurs du site sont connectés, en fonction de la configuration, ils peuvent :

* Posez une nouvelle question.
* Modifiez ou supprimez les questions qu’ils ont créées.
* Signaler les questions ou réponses des autres membres.
* Identifiez les réponses aux questions qu’ils ont rédigées.

#### Anonyme {#anonymous}

Les visiteurs du site qui ne sont pas connectés peuvent seulement lire les questions et réponses publiées, les traduire s&#39;ils sont pris en charge, mais ne peuvent ni ajouter de question, ni répondre, ni marquer les messages des autres.

## Informations supplémentaires {#additional-information}

Pour plus d&#39;informations, consultez la page [QnA Essentials](/help/communities/qna-essentials.md) destinée aux développeurs.

Pour des informations sur la modération des sujets et des commentaires publiés, reportez-vous à la section [Modération du contenu généré par l’utilisateur](/help/communities/moderate-ugc.md).

Pour baliser les sujets et les commentaires publiés, voir [Balisage de contenu généré par l’utilisateur](/help/communities/tag-ugc.md).
