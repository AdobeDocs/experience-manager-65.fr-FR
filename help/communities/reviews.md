---
title: Utilisation des révisions et du résumé des révisions (affichage)
description: Découvrez comment ajouter les composants Résumé des révisions et révisions à une page.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 170414a6-c40b-4ad2-9294-7c2266850c3d
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1290'
ht-degree: 0%

---

# Utilisation des révisions et du résumé des révisions (affichage) {#using-reviews-and-reviews-summary-display}

Le composant `Reviews` est un composite des composants [Comments](comments.md) et [Rating](rating.md) prêts à l’emploi.

Le composant `Reviews Summary (Display)` fournit un résumé d’une instance active ou fermée d’un composant `Reviews` à afficher ailleurs sur le site.

>[!NOTE]
>
>La publication anonyme d’une révision n’est pas prise en charge. Les visiteurs du site doivent s’inscrire (devenir membres) et se connecter pour participer. Le visiteur connecté peut mettre à jour sa révision à tout moment.

## Ajout d’une révision à une page {#adding-a-review-to-a-page}

Pour ajouter un composant `Reviews` à une page en mode création, utilisez l’explorateur de composants pour localiser `Communities / Reviews` et le faire glisser sur une page, par exemple une position relative à la fonction à réviser pour les utilisateurs.

Pour plus d’informations, consultez la page [Principes de base des composants Communities](basics.md).

Lorsque les [bibliothèques côté client demandées](reviews-basics.md#essentials-for-client-side) sont incluses, voici comment le composant `Reviews` apparaît.

![create-review](assets/create-review.png)

## Configuration des révisions {#configuring-reviews}

Sélectionnez le composant `Reviews` inséré afin que vous puissiez accéder à l’icône `Configure` qui ouvre la boîte de dialogue de modification.

![configure-new](assets/configure-new.png)

Sous l’onglet **[!UICONTROL Évaluations autorisées]** , spécifiez la liste complète des évaluations à présenter aux membres. La première évaluation doit être une évaluation globale/générale, car c’est la notation qui fournit la notation moyenne pour le composant `Review Summary (Display)`. Les deux évaluations suivantes dans la configuration par défaut doivent recevoir un titre différent, autre que &quot;Sous-évaluation 1&quot; ou &quot;Sous-évaluation 2&quot;.

![allowed-rating](assets/configure-review1.png)

* **[!UICONTROL Classement autorisé]**

  Liste d’évaluations à partir desquelles un membre peut choisir.

  Pour modifier les sélections visibles, utilisez les boutons fléchés Haut, Bas et Supprimer.

  Cliquez sur **[!UICONTROL Ajouter un élément]** pour ajouter un autre choix d’évaluation.

Sous l’onglet **[!UICONTROL Évaluations requises]**, saisissez à nouveau les éléments de la liste **[!UICONTROL Évaluations autorisées]** qui sont requis pour l’évaluation. Si un élément n’est spécifié que dans l’onglet Évaluations autorisées , il peut ne pas être marqué lorsqu’il est envoyé par le membre.

Sur le site web, les évaluations requises sont marquées d’un astérisque. Si un élément est requis et laissé sans marque, un message s’affiche pour le membre et l’envoi est refusé jusqu’à ce que toutes les évaluations requises soient marquées.

![required-rating](assets/configure-review2.png)

* **[!UICONTROL Évaluations requises]**

  Un sous-ensemble d’évaluations autorisées, indiquant les évaluations requises.

  Pour modifier les sélections visibles, utilisez les boutons fléchés Haut, Bas et Supprimer.

  Cliquez sur **[!UICONTROL Ajouter un élément]** pour ajouter un autre choix de réponse.

>[!NOTE]
>
>Si un élément est saisi dans l’onglet **[!UICONTROL Évaluations requises]** qui n’est pas spécifié dans l’onglet **[!UICONTROL Évaluations autorisées]**, il n’est pas inclus dans les éléments à évaluer.

Sous l’onglet **[!UICONTROL Révisions]**, indiquez comment les révisions sont traitées.

![révisions](assets/configure-review3.png)

* **[!UICONTROL Autoriser les réponses]**

  Si cette case est cochée, les réponses aux révisions sont autorisées. La case par défaut est décochée.

* **[!UICONTROL Fermé]**

  Si cette case est cochée, la révision est fermée aux nouvelles révisions et réponses. La case par défaut est décochée.

* **[!UICONTROL Autoriser les chargements de fichiers]**

  Si cette case est cochée, les pièces jointes peuvent être chargées pour la révision. La case par défaut est décochée.

* **Taille de fichier max.**

  Paramètre à définir uniquement si l’option **[!UICONTROL Autoriser les chargements de fichiers]** est cochée. Ce champ limite la taille (en octets) d’un fichier chargé. La valeur par défaut est de 10 Mo.

* **[!UICONTROL Longueur de message max.]**

  Nombre maximal de caractères pouvant être saisis dans la zone de texte. La valeur par défaut est de 4 096 caractères.

* **[!UICONTROL Types de fichiers autorisés]**

  Paramètre à définir uniquement si l’option **[!UICONTROL Autoriser les chargements de fichiers]** est cochée. Liste d’extensions de fichier séparées par des virgules avec le séparateur &quot;point&quot;. Par exemple, .jpg, .jpeg, .png, .doc, .docx, .pdf. Si des types de fichiers sont spécifiés, ceux qui ne sont pas spécifiés ne sont pas autorisés. Par défaut, aucun n’est spécifié, de sorte que tous les types de fichiers soient autorisés.

* **[!UICONTROL Éditeur de texte enrichi]**

  Si cette case est cochée, les publications peuvent être entrées avec des balises. La case par défaut est décochée.

* **[!UICONTROL Autoriser le vote]**

  Si cette case est cochée, la fonction de vote d’une rubrique est ajoutée. La case par défaut est décochée.

Sous l’onglet **[!UICONTROL Modération d’utilisateur]**, indiquez comment les révisions publiées sont gérées. Pour plus d’informations, voir [Modération de contenu généré par l’utilisateur](moderate-ugc.md).

![user-modération](assets/configure-review4.png)

* **[!UICONTROL Pré-modération]**

  Si cette case est cochée, les révisions doivent être approuvées avant d’apparaître sur un site de publication. La case par défaut est décochée.

* **[!UICONTROL Supprimer les révisions]**

  Si cette case est cochée, le membre qui a publié la révision peut la supprimer. La case par défaut est décochée.

* **[!UICONTROL Refuser les révisions]**

  Si cette case est cochée, autorisez les modérateurs à refuser les révisions. La case par défaut est décochée.

* **[!UICONTROL Fermer/rouvrir les révisions]**

  Si cette case est cochée, les modérateurs peuvent fermer et rouvrir les révisions. La case par défaut est décochée.

* **[!UICONTROL Flag Reviews]**

  Si cette case est cochée, autorisez les membres à signaler les révisions comme inappropriées. La case par défaut est décochée.

* **[!UICONTROL Liste des motifs de l’indicateur]**

  Si cette case est cochée, les membres ont le droit de sélectionner dans une liste déroulante la ou les raisons pour lesquelles ils ont marqué une révision comme étant inappropriée. La case par défaut est décochée.

* **[!UICONTROL Motif d’indicateur personnalisé]**

  Si cette case est cochée, autorisez les membres à indiquer leur propre raison de signaler une révision comme inappropriée. La case par défaut est décochée.

* **[!UICONTROL Seuil de modération]**

  Saisissez le nombre de fois qu’une révision doit être marquée par les membres avant que les modérateurs ne soient informés. La valeur par défaut est une fois (1).

* **[!UICONTROL Limite de marquage]**

  Saisissez le nombre de fois qu’une révision doit être marquée avant qu’elle ne soit masquée dans la vue publique. Ce nombre doit être supérieur ou égal au **[!UICONTROL seuil de modération]**. La valeur par défaut est 5.

### Ajout d’un résumé des révisions (affichage) à une page {#adding-a-review-summary-display-to-a-page}

Pour ajouter un composant `Reviews Summary (Display)` à une page en mode création, localisez le composant

* `Communities / Reviews Summary (Display)`

Faites-le glisser sur la page où s’affiche un résumé d’une révision active ou fermée.

Pour plus d’informations, consultez la page [Principes de base des composants Communities](basics.md).

Lorsque les [bibliothèques côté client demandées](reviews-basics.md#essentials-for-client-side) sont incluses, voici comment le composant `Reviews Summary (Display)` apparaît.

![review-summary](assets/configure-review5.png)

>[!NOTE]
>
>La &quot;moyenne&quot; reflète les votes pour le premier élément répertorié dans les onglets Évaluations autorisées de la révision résumée.

### Configuration du résumé des révisions (affichage) {#configuring-reviews-summary-display}

Sélectionnez le composant `Reviews Summary (Display)` inséré afin que vous puissiez accéder à l’icône `Configure` qui ouvre la boîte de dialogue de modification.

![configure](assets/configure-new.png)

Sous l’onglet **[!UICONTROL Résumé de la révision]**

![review-summary](assets/configure-review6.png)

* `Review Path`

  Saisissez ou accédez à l’instance placée du composant `reviews` afin de pouvoir résumer, par exemple, si vous l’ajoutez à la page web du [site Engage de Geometrixx,](getting-started.md), le chemin d’accès serait :

  `/content/sites/engage/en/page/jcr:content/content/primary/reviews`

* `Include histogram`

  Si cette case est cochée, incluez l’affichage d’un graphique à barres indiquant le nombre d’évaluations résumées dans les révisions. La case par défaut est décochée.

### Passage à un type de révision personnalisé {#changing-to-a-custom-review-type}

Le composant Révisions utilise le système de commentaires.

En modifiant le type de ressource de commentaire, le système de commentaires ne génère plus une instance d’un commentaire à l’aide de la valeur par défaut, mais une instance qui a été personnalisée (étendue) par les développeurs.

Lorsque les types de ressources personnalisés sont connus, saisissez [Mode de conception](../../help/sites-authoring/default-components-designmode.md) et double-cliquez sur le composant `Comments` placé pour ouvrir une boîte de dialogue avec un onglet supplémentaire.

Sous l’onglet **[!UICONTROL Resource Types]** , spécifiez le type de ressource personnalisé pour les nouvelles instances des composants `Comments or Voting` :

![comments-voter](assets/configure-review7.png)

* **[!UICONTROL Type de ressource de commentaire]**

  Accédez au resourceType d&#39;un composant `comment`étendu (commentaire unique) dans /apps. Par exemple, `/apps/social/commons/components/hbs/comments/comment`.

  Cette ressource identifie le type de ressource du contenu créé par un visiteur lorsqu’il publie un commentaire.

* **[!UICONTROL Type de ressource de vote]**

  Accédez au resourceType d&#39;un composant `voting` étendu dans /apps. Par exemple, `/apps/social/components/hbs/voting`.

  Cette ressource identifie le type de ressource du contenu créé par un visiteur lorsqu’il publie un vote.

* **[!UICONTROL Type de ressource système de commentaire]**

  Accédez au resourceType d’un composant `comments`étendu (système de commentaires) dans /apps. Laissez ce champ vide, sauf si le modèle de page [inclut dynamiquement](scf.md#add-or-include-a-communities-component) le système de commentaires dans le script sous-jacent au lieu d’être ajouté à la page en tant que ressource (noeud de commentaires). Pour en savoir plus, consultez la section [`{{include}}` Helper](handlebars-helpers.md#include).

## Expérience du visiteur du site {#site-visitor-experience}

### Modérateurs et administrateurs {#moderators-and-administrators}

Lorsque l’utilisateur connecté dispose de privilèges de modérateur ou d’administrateur, il peut exécuter les tâches de modération autorisées par la configuration du composant, indépendamment de la personne ayant créé la révision.

### Membres {#members}

Lorsque le visiteur du site est connecté, selon la configuration, il peut :

* Post : nouvelle révision
* Modifier sa propre révision
* Supprimer sa propre révision
* Marquer les commentaires de révision des autres

Une seule évaluation par membre est autorisée. Le membre peut modifier sa note à tout moment.

### Anonyme {#anonymous}

Les visiteurs qui ne sont pas connectés ne peuvent lire que les révisions publiées, les traduire si elles sont prises en charge, mais peuvent ne pas ajouter d’évaluation ou de révision, ni marquer les commentaires de révision d’autres personnes.

## Informations supplémentaires {#additional-information}

Pour plus d’informations, reportez-vous à la page [Notions fondamentales sur la révision](reviews-basics.md) pour les développeurs.

Pour la modération des commentaires publiés, voir [Modération de contenu généré par les utilisateurs](moderate-ugc.md).

Pour la traduction des commentaires publiés, voir [Traduction de contenu généré par l’utilisateur](translate-ugc.md).
