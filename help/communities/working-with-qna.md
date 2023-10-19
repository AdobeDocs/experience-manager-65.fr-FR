---
title: Fonction Forum Q&R
description: Découvrez comment ajouter la fonction de forum Q&R à une page qui permet aux membres de la communauté connectés de poser des questions et de répondre à des questions.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 17081710-35e0-4f5b-9485-1f85c065fd70
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '1376'
ht-degree: 10%

---

# Fonction Forum Q&amp;R{#q-a-forum-feature}

## Présentation {#introduction}

La fonction Forum Q&amp;R (questions et réponses) offre aux membres de la communauté un espace où poser leurs questions et y répondre. Il permet aux membres de :

* Création de questions
* Ajout d’images intégrées (avec prise en charge du glisser-déposer)
* Afficher et répondre aux questions
* Recherche d’une question
* Aider à modérer le contenu Q&amp;R
* Identifier les meilleures réponses
* Déplacer des questions Q&amp;R d’une page vers une autre

La documentation décrit :

* Ajout de la fonction Forum Q&amp;R à un site AEM.
* Paramètres de configuration de la variable `QnA`composant.

## Ajout d’un forum de questions-réponses à une page {#adding-a-q-a-forum-to-a-page}

Pour ajouter une `QnA` sur une page en mode création, utilisez l’explorateur de composants pour accéder à `Communities / QnA` et faites-le glisser sur une page où le forum Q&amp;R doit apparaître.

Pour obtenir les informations nécessaires, consultez la section [Principes de base des composants des communautés](/help/communities/basics.md).

Lorsque la variable [bibliothèques côté client requises](/help/communities/qna-essentials.md#essentials-for-client-side) sont incluses, c’est ainsi que la variable `QnA` Le composant apparaît :

![qna-component](assets/qna-component.png)

### Configuration de Q&amp;R {#configuring-qna}

Sélectionnez le `QnA` afin que vous puissiez accéder au `Configure` qui ouvre la boîte de dialogue de modification.

![configure](assets/configure-new.png)

![qna-config](assets/qna-config.png)

#### Onglet Paramètres {#settings-tab}

Sous , **Paramètres** , définissez les paramètres des sujets (questions) et réponses (réponses) :

* **Autoriser les miniatures de pièces jointes**

  Si cette case est cochée, une miniature de l’image jointe est créée.

* **Taille max. des miniatures de pièces jointes**

  Taille maximale (en pixels) de la miniature de la pièce jointe. La valeur par défaut est 800 x 800.

* **Taille d’image minimale pour la miniature**

  Taille minimale (en octets) de l’image pour générer une miniature pour les images intégrées. La valeur par défaut est de 100000 octets (100 Ko).

* **Taille maximale de la miniature**

  Taille maximale (en pixels) de la miniature de l’image intégrée. La valeur par défaut est 800 x 800.

* **Sujets par page**

  Définit le nombre de questions/publications affichées par page. La valeur par défaut est 10.

* **Modérée**

  Si cette case est cochée, la publication des sujets et des commentaires doit être approuvée avant d’apparaître sur un site de publication. La valeur par défaut est désélectionnée.

* **Fermé**

  Si cette case est cochée, le forum est fermé aux nouvelles questions et commentaires. La valeur par défaut est désélectionnée.

* **Éditeur de texte enrichi**

  Si cette case est cochée, les sujets et les commentaires peuvent être saisis avec une annotation. La valeur par défaut est désélectionnée.

* **Autoriser le balisage**

  Si cette case est cochée, les membres ont le droit d’ajouter des libellés de balise à leurs publications (voir **Champ de balise** ). La valeur par défaut est désélectionnée.

* **Autoriser les chargements de fichiers**

  Si cette option est cochée, des pièces jointes peuvent être ajoutées à la question ou au commentaire. La valeur par défaut est désélectionnée.

* **Autoriser abonnement**

  Si cette case est cochée, incluez la fonction suivante pour les publications de forum, ce qui permet aux membres d’être [notifié](/help/communities/notifications.md) de nouvelles publications. La valeur par défaut est désélectionnée.

* **Autoriser l’épinglage**

  Si cette case est cochée, les rubriques des forums peuvent être collées en haut de la liste des rubriques. La valeur par défaut est désélectionnée.

* **Autoriser les abonnements par courrier électronique**

  Si cette case est cochée, autorisez les membres à être informés des nouvelles publications par courrier électronique ([abonnement](/help/communities/subscriptions.md)). Requiert que l’option Autoriser le suivi soit cochée et [email configuré](/help/communities/email.md). La valeur par défaut est désélectionnée.

* **Taille maximale du fichier**

  Pertinent uniquement si `Allow File Uploads` est cochée. Ce champ limite la taille (en octets) d’un fichier chargé. La valeur par défaut est 104857600 (10 Mo).

* **Types de fichier autorisés**

  Pertinent uniquement si `Allow File Uploads` est cochée. Liste d’extensions de fichier séparées par des virgules avec le séparateur &quot;point&quot;. Par exemple : .jpg, .jpeg, .png, .doc, .docx, .pdf. Si des types de fichiers sont spécifiés, ceux qui ne sont pas spécifiés ne peuvent pas être chargés. La valeur par défaut n’est pas spécifiée. **all** les types de fichiers sont autorisés.

* **Taille max. du fichier image joint**

  À définir uniquement si l’option Autoriser les chargements de fichiers est cochée. Nombre maximal d’octets qu’un fichier image chargé peut contenir. La valeur par défaut est 2097152 (2 Mo).

* **Autoriser les réponses**

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

  Si cette case est cochée, affichez les droits gagnés et attribués. [badges](/help/communities/implementing-scoring.md) avec l&#39;entrée de blog d&#39;un membre. La valeur par défaut est désélectionnée.

* **Autoriser le contenu proposé**

  Si cette option est cochée, l’idée est identifiable comme [contenu proposé](/help/communities/featured.md). La valeur par défaut est désélectionnée.

* **Activer la mention**

  S’il est activé, permet aux utilisateurs enregistrés de la communauté d’identifier d’autres membres enregistrés (à l’aide du prénom, du nom, du nom d’utilisateur) et de les baliser à l’aide de la syntaxe @user-name courante. Les utilisateurs balisés reçoivent des notifications sur leurs mentions.

* **Nombre max. de mentions**

  Limitez le nombre maximal de mentions autorisées dans une publication. La valeur par défaut est 10.

* **Modèle des mentions de l’IU**

  Spécifiez la chaîne de modèle autorisée à baliser (@mention) l’utilisateur enregistré dans une publication. Par exemple, `~{{familyName}}{{givenName}}`.

#### Onglet Modération d’utilisateur {#user-moderation-tab}

Sous , **Modération d’utilisateur** , indiquez comment gérer les sujets publiés (questions) et les réponses (contenu généré par l’utilisateur). Pour plus d’informations, voir [Modération de contenu généré par l’utilisateur](/help/communities/moderate-ugc.md).

* **Refuser les réponses**

  Si cette case est cochée, les modérateurs membres approuvés sont autorisés à refuser les réponses publiées et à empêcher les réponses de s’afficher sur le forum Q&amp;R public. La valeur par défaut est désélectionnée.

* **Fermer/rouvrir les sujets**

  Si cette case est cochée, les membres modérateurs autorisés peuvent fermer une question (rubrique) pour apporter d’autres modifications et réponses, puis rouvrir une question. La valeur par défaut est désélectionnée.

* **Déplacer les rubriques**
Si cette case est cochée, les modérateurs côté publication peuvent déplacer les questions. La valeur par défaut est désélectionnée.

* **Marquer les publications**

  Si cette option est cochée, les membres ont le droit de signaler les questions ou réponses des autres comme étant inappropriées. La valeur par défaut est désélectionnée.

* **Marquer la liste de motifs**

  Si cette case est cochée, les membres ont le droit de choisir dans une liste déroulante la raison pour laquelle ils ont marqué une question ou une réponse comme étant inappropriée. La valeur par défaut est désélectionnée.

* **Motif de la marque personnalisée**

  Si cette case est cochée, autorisez les membres à indiquer leur propre raison de signaler une question ou une réponse comme inappropriée. La valeur par défaut est désélectionnée.

* **Seuil de modération**

  Saisissez le nombre de fois qu’une question ou une réponse doit être marquée par les membres avant que les modérateurs ne soient informés. La valeur par défaut est 1 (une fois).

* **Limite de marquage**

  Saisissez le nombre de fois qu&#39;une question ou une réponse doit être marquée avant qu&#39;elle ne soit plus visible pour le public. S’il est défini sur -1, la question ou la réponse marquée n’est jamais masquée de la vue du public. Sinon, ce nombre doit être supérieur ou égal au seuil de modération. La valeur par défaut est 5.

#### Onglet Champ de balise {#tag-field-tab}

Sous , **Champ de balise** , les balises qui peuvent être appliquées, si elles sont autorisées sous l’onglet **Paramètres** sont limités en fonction des espaces de noms sélectionnés.

* **Espaces de noms autorisés**

  Pertinent si `Allow Tagging` est coché sous **Paramètres** . Les balises qui peuvent être appliquées sont limitées aux catégories d’espace de noms cochées. La liste des espaces de noms inclut &quot;Balises standard&quot; (espace de noms par défaut) et &quot;Inclure toutes les balises&quot;. La valeur par défaut n’est pas cochée, ce qui signifie que tous les espaces de noms sont autorisés.

* **Limite de suggestions**

  Saisissez le nombre de balises à afficher comme suggestion au membre qui publie sur le forum. Une valeur **-**1 signifie qu’aucune limite n’est définie. La valeur par défaut est 0.

#### Onglet Paramètres de tri {#sort-settings-tab}

Sous , **Paramètres de tri** , indiquez comment les commentaires publiés sont triés lorsqu’ils sont affichés.

* **Trier par**

  Cochez toutes les sélections de tri autorisées : `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. La valeur par défaut est `Newest, Oldest, Last Updated`.

* **Définir par défaut**

  Extrayez pour sélectionner l’une des options de tri cochées à afficher par défaut. La valeur par défaut est `Newest`.

* **Sélectionner les options de temps pour le tri Analytics**

  Menu déroulant pour sélectionner l’un des `All, Last 24 Hours, Last 7 Days, Last 30 Days`. La valeur par défaut est `All`.

## Expérience du visiteur du site {#site-visitor-experience}

### Identification des réponses {#identifying-answers}

Une réponse peut être indiquée comme réponse correcte ou utile à l’aide de la variable `Select Answer` bouton . Une fois qu&#39;une question est marquée comme ayant reçu une réponse, une autre réponse ne peut pas être sélectionnée tant que la première question n&#39;a pas été désélectionnée à l&#39;aide de la variable `Unmark Chosen Answer` bouton .

Une fois sélectionnée comme réponse viable, elle peut être désélectionnée à l’aide de la variable `Unmark Chosen Answer` bouton .

Une fois qu&#39;une réponse est sélectionnée comme réponse viable, une indication que la question a été `Answered` s’affiche en regard de la rubrique de question sur la page Q&amp;R principale.

#### Modérateurs et administrateurs {#moderators-and-administrators}

Lorsque l’utilisateur connecté dispose de privilèges de modérateur ou d’administrateur, il peut effectuer les tâches de modération autorisées par la configuration du composant, indépendamment de la personne qui a créé la question ou la réponse.

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

Vous trouverez plus d’informations sur la [Notions fondamentales sur la qualité de vie](/help/communities/qna-essentials.md) pour les développeurs.

Pour la modération des sujets et des commentaires publiés, voir [Modération de contenu généré par l’utilisateur](/help/communities/moderate-ugc.md).

Pour baliser des sujets et des commentaires publiés, voir [Balisage du contenu généré par l’utilisateur](/help/communities/tag-ugc.md).
