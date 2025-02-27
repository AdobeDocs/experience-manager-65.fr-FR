---
title: Utilisation des commentaires
description: La fonction Commentaires permet aux visiteurs connectés du site de partager leurs opinions et leurs connaissances.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 30baebd9-13c5-4fde-a494-85601abc32a5
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 2%

---

# Utilisation des commentaires {#using-comments}

## Présentation {#introduction}

La fonction de commentaires permet aux visiteurs (membres) connectés de partager leurs opinions et leurs connaissances sur le contenu du site. Cette fonctionnalité est souvent déjà présente dans d’autres fonctionnalités, mais peut être ajoutée à n’importe quel site web.

Le document décrit :

* Ajout de `Comments` à une page.
* Paramètres de configuration du composant `Comments`.

>[!NOTE]
>
>La publication anonyme d’un commentaire n’est pas prise en charge. Les visiteurs du site doivent s’inscrire (devenir membres) et se connecter pour participer.

### Ajout de commentaires à une page {#adding-comments-to-a-page}

Pour ajouter un composant `Comments` à une page en mode création, utilisez l’explorateur de composants pour accéder à :

* `Communities / Comments`

et faites-le glisser sur la page, par exemple à une position relative à la fonction pour que les utilisateurs puissent commenter, ou simplement au bas de la page.

Pour plus d’informations, consultez la page [Principes de base des composants Communities](/help/communities/basics.md).

Lorsque les [bibliothèques côté client demandées](/help/communities/essentials-comments.md#essentials-for-client-side) sont incluses, voici comment le composant `Comments` apparaît.

![comments-component](assets/comments-component.png)

>[!NOTE]
>
>Un seul composant `Comments` peut exister sur une page. Notez que plusieurs fonctionnalités de Communities incluent déjà des commentaires, tels qu’un blog, un calendrier, un forum, une note de service et des commentaires.

### Configuration des commentaires {#configuring-comments}

Sélectionnez le composant `Comments` inséré pour y accéder et sélectionnez l’icône `Configure` qui ouvre la boîte de dialogue de modification.

![icône de configuration](assets/configure.png)

![commentsettings](assets/commentssettings.png)

#### Onglet Commentaires {#comments-tab}

Sous l’onglet **Commentaires** , indiquez la manière dont les commentaires sont saisis par les visiteurs.

* **Autoriser les réponses**

  Si cette case est cochée, les membres ont la possibilité de répondre aux commentaires existants. La valeur par défaut est désélectionnée.

* **Commentaires par page**

  Limite le nombre de commentaires affichés par page et le nombre de réponses affichées. La valeur par défaut est 10.

* **Autoriser les chargements de fichiers**

  Si cette case est cochée, l’option permettant de télécharger un fichier est présentée avec la zone de saisie de texte. La valeur par défaut est désélectionnée.

* **Taille de fichier max.**

  À définir uniquement si l’option Autoriser les chargements de fichiers est cochée. Cette valeur limite la taille du fichier téléchargé. La limite par défaut est de 10 Mo.

* **Longueur de message max.**

  Nombre maximal de caractères pouvant être saisis dans la zone de texte. La valeur par défaut est de 4 096 caractères.

* **Types de fichiers autorisés**

  À définir uniquement si l’option Autoriser les chargements de fichiers est cochée. Liste d’extensions de nom de fichier séparées par des virgules avec le séparateur &quot;point&quot;. Par exemple : .jpg, .jpeg, .png, .doc, .docx, .pdf. Si des types de fichiers sont spécifiés, ceux qui ne sont pas spécifiés ne sont pas autorisés. Par défaut, aucun n’est spécifié, de sorte que tous les types de fichiers soient autorisés.

* **Éditeur de texte enrichi**

  Si cette case est cochée, les commentaires sont saisis avec un balisage. La valeur par défaut est désélectionnée.

* **Autoriser le vote**

  Si cette case est cochée, l’option permettant de voter vers le haut ou vers le bas est présentée avec la zone de saisie de texte. La valeur par défaut est désélectionnée.

* **Autoriser l’abonnement**

  Si cette option est cochée, les membres ont le droit de suivre les commentaires. La valeur par défaut est désélectionnée.

* **Badges d’affichage**

  Si cette case est cochée, les badges mérités et attribués doivent s’afficher. La valeur par défaut est désélectionnée.

#### Onglet Modération d’utilisateur {#user-moderation-tab}

Sous l’onglet **Modération d’utilisateur**, indiquez comment les commentaires publiés sont gérés. Pour plus d’informations, voir [Modération de contenu généré par l’utilisateur](/help/communities/moderate-ugc.md).

* **Pré-modération**

  Si cette case est cochée, les commentaires doivent être approuvés avant d’apparaître sur un site de publication. La valeur par défaut est désélectionnée.

* **Supprimer les commentaires**

  Si cette case est cochée, le membre qui a publié le commentaire peut le supprimer. La valeur par défaut est désélectionnée.

* **Refuser les commentaires**

  Si cette case est cochée, autorisez les modérateurs à refuser les commentaires. La valeur par défaut est désélectionnée.

* **Fermer/rouvrir les commentaires**

  Si cette case est cochée, les modérateurs peuvent fermer et rouvrir les commentaires. La valeur par défaut est désélectionnée.

* **Flag Comments**

  Si cette case est cochée, les membres ont le droit de signaler les commentaires comme inappropriés. La valeur par défaut est désélectionnée.

* **Liste des motifs de l’indicateur**

  Si cette case est cochée, les membres ont le droit de choisir dans une liste déroulante la raison pour laquelle ils ont marqué un commentaire comme étant inapproprié. La valeur par défaut est désélectionnée.

* **Motif d’indicateur personnalisé**

  Si cette case est cochée, autorisez les membres à indiquer leur propre raison de signaler un commentaire comme inapproprié. La valeur par défaut est désélectionnée.

* **Seuil de modération**

  Saisissez le nombre de fois qu’un commentaire doit être marqué par les membres avant que les modérateurs ne soient informés. La valeur par défaut est une fois (1).

* **Limite de marquage**

  Saisissez le nombre de fois qu’un commentaire doit être marqué avant qu’il ne soit plus visible pour le public. Ce nombre doit être supérieur ou égal au **seuil de modération**. La valeur par défaut est 5.

#### Onglet Paramètres de tri {#sort-settings-tab}

Sous l’onglet **Paramètres de tri**, indiquez comment les commentaires publiés sont triés lorsqu’ils sont affichés.

* **Champ de tri**

  Descendez pour sélectionner l’un des `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed` ou `Most Liked`.

* **Ordre de tri**

  Descendez pour sélectionner l’un des `Ascending` ou `Descending`.

### Modification d’un type de commentaire personnalisé {#changing-to-a-custom-comment-type}

En modifiant le type de ressource de commentaire, le système de commentaires ne génère plus une instance d’un commentaire à l’aide de la valeur par défaut, mais une instance qui a été personnalisée (étendue) par les développeurs.

Une fois les types de ressources personnalisés connus, saisissez [Mode de conception](/help/sites-authoring/default-components-designmode.md) et double-cliquez sur le composant `Comments` inséré pour ouvrir une boîte de dialogue avec un onglet supplémentaire.

Sous l’onglet **Resource Types** , spécifiez le type de ressource personnalisé pour les nouvelles instances des composants `Comments or Voting` :

![resource-type](assets/resource-type.png)

* **Type de ressource de commentaire**

  Accédez au resourceType d’un composant `comment` étendu (commentaire unique) dans /apps. Par exemple, `/apps/social/commons/components/hbs/comments/comment`.

  Cette ressource identifie le type de ressource du contenu créé par un visiteur lorsqu’il publie un commentaire.

* **Type de ressource de vote**

  Accédez au resourceType d’un composant `voting` étendu dans /apps. Par exemple, `/apps/social/components/hbs/voting`.

  Cette ressource identifie le type de ressource du contenu créé par un visiteur lorsqu’il publie un vote.

* **Type de ressource système de commentaire**

  Accédez au resourceType d’un composant `comments`étendu (système de commentaires) dans /apps. Laissez ce champ vide, sauf si le modèle de page [inclut dynamiquement](/help/communities/scf.md#add-or-include-a-communities-component) le système de commentaires dans le script sous-jacent au lieu d’être ajouté à la page en tant que ressource (noeud de commentaires). Pour en savoir plus, consultez la section [`{{include}}` Helper](/help/communities/handlebars-helpers.md#include).

### Expérience du visiteur du site {#site-visitor-experience}

#### Modérateurs et administrateurs {#moderators-and-administrators}

Lorsque l’utilisateur connecté dispose de privilèges de modérateur ou d’administrateur, il peut exécuter les tâches de modération autorisées par la configuration du composant, indépendamment de la personne ayant créé le commentaire.

#### Membres {#members}

Lorsque le visiteur du site est connecté, selon la configuration, il peut :

* Post d’un nouveau commentaire
* Modifier son propre commentaire
* Supprimer son propre commentaire
* Marquer les commentaires des autres

#### Anonyme {#anonymous}

Les visiteurs qui ne sont pas connectés ne peuvent lire que les commentaires publiés, les traduire s’ils sont pris en charge, mais ne peuvent pas ajouter de commentaire ni marquer les commentaires d’autres personnes.

### Informations supplémentaires {#additional-information}

Pour plus d’informations, reportez-vous à la page [Comments Essentials](/help/communities/essentials-comments.md) pour les développeurs.

Pour la modération des commentaires publiés, voir [Modération de contenu généré par les utilisateurs](/help/communities/moderate-ugc.md).

Pour la traduction des commentaires publiés, voir [Traduction de contenu généré par l’utilisateur](/help/communities/translate-ugc.md).
