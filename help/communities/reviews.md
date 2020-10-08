---
title: Utilisation des révisions et du résumé des révisions (affichage)
seo-title: Utilisation des révisions et du résumé des révisions (affichage)
description: Ajouter les composants Résumé des révisions et révisions à une page
seo-description: Ajouter les composants Résumé des révisions et révisions à une page
uuid: bd1ccee7-b26b-4a27-b1ea-89609f5080af
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: bf4e7809-8def-4647-aaa6-3ac36865511f
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '1311'
ht-degree: 36%

---


# Utilisation des révisions et du résumé des révisions (affichage) {#using-reviews-and-reviews-summary-display}

The `Reviews` component is a composite of [Comments](comments.md) and [Rating](rating.md) components ready for use.

The `Reviews Summary (Display)` component provides a summary of an active or closed instance of a `Reviews` component for display elsewhere on the site.

>[!NOTE]
>
>La publication anonyme d’une révision n’est pas possible. Les visiteurs du site doivent s&#39;inscrire (devenir membre) et se connecter pour participer. Les visiteurs connectés peuvent mettre à jour leurs révisions à tout moment.

## Ajout d’une révision à une page {#adding-a-review-to-a-page}

Pour ajouter un `Reviews` composant à une page en mode création, utilisez l’explorateur de composants pour le localiser `Communities / Reviews` et le faire glisser sur une page, par exemple une position relative à la fonction à réviser pour les utilisateurs.

For necessary information, visit [Communities Components Basics](basics.md).

When the [required client-side libraries](reviews-basics.md#essentials-for-client-side) are included, this is how the `Reviews` component will appear.

![create-review](assets/create-review.png)

## Configuration des révisions {#configuring-reviews}

Select the placed `Reviews` component to access and select the `Configure` icon which opens the edit dialog.

![configure-new](assets/configure-new.png)

Under the **[!UICONTROL Allowed Ratings]** tab, specify the complete list of ratings to be shown to members. The first rating should be an overall/general rating, as it is the rating which provides the average rating for the `Review Summary (Display)` component. Les deux évaluations suivantes dans la configuration par défaut doivent recevoir un titre différent, autre que &quot;Subrating 1&quot; ou &quot;Subrating 2&quot;.

![évaluation autorisée](assets/configure-review1.png)

* **[!UICONTROL Evaluations autorisées]**

   Liste de notes à partir de laquelle un membre peut choisir.

   Utilisez les flèches Haut et Bas, ainsi que les boutons de suppression, pour modifier les choix visibles.

   Cliquez sur **[!UICONTROL Ajouter un élément]** pour ajouter un autre choix d’évaluation.

Under the **[!UICONTROL Required Ratings]** tab, re-enter items from the list of **[!UICONTROL Allowed Ratings]** that are required to be rated. Si un élément est spécifié uniquement dans l’onglet Évaluations autorisées, il peut être laissé non signalé lorsqu’il est soumis par le membre.

Sur le site web, les évaluations requises sont signalées d’un astérisque. Si un élément obligatoire n’est pas marqué, un message s’affiche à l’intention du membre, et sa soumission est refusée jusqu’à ce que toutes les évaluations requises soient marquées.

![qualification requise](assets/configure-review2.png)

* **[!UICONTROL Evaluations requises]**

   Un sous-ensemble d’évaluations autorisées, indiquant les évaluations requises.

   Utilisez les flèches Haut et Bas, ainsi que les boutons de suppression, pour modifier les choix visibles.

   Cliquez sur **[!UICONTROL Ajouter un élément]** pour ajouter un autre choix de réponse.

>[!NOTE]
>
>If an item is entered on the **[!UICONTROL Required Ratings]** tab that is not specified on the **[!UICONTROL Allowed Ratings]** tab, then it is not included in the items to rate.

Under the **[!UICONTROL Reviews]** tab, specify how reviews are handled.

![Révisions](assets/configure-review3.png)

* **[!UICONTROL Permettre des réponses]**

   Si cette option est cochée, autorisez les réponses aux révisions. Cette option n’est pas cochée par défaut.

* **[!UICONTROL Fermé]**

   Si cette option est cochée, la révision est fermée aux nouveaux examens et réponses. Cette option n’est pas cochée par défaut.

* **[!UICONTROL Autoriser les transferts de fichiers]**

   Si cette option est cochée, autorisez le téléchargement des pièces jointes pour la révision. Cette option n’est pas cochée par défaut.

* **Taille maximale du fichier**

   N’est pertinent que si l’option **[!UICONTROL Autoriser les téléchargements]** de fichiers est cochée. Ce champ limite la taille (en octets) d’un fichier téléchargé. La valeur par défaut est de 10 Mo.

* **[!UICONTROL Longueur de message max.]**

   Nombre maximal de caractères pouvant être saisis dans la zone de texte. La valeur par défaut est de 4 096 caractères.

* **[!UICONTROL Types de fichier autorisés]**

   N’est pertinent que si l’option **[!UICONTROL Autoriser les téléchargements]** de fichiers est cochée. Liste séparée par des virgules d’extensions de fichiers avec le séparateur &quot;point&quot;. Par exemple : .jpg, .jpeg, .png, .doc, .docx, .pdf. Si des types de fichier sont spécifiés, ceux qui ne sont pas spécifiés ne seront pas autorisés. Par défaut, aucun type de fichier n’est spécifié, de sorte que tous les types de fichier soient autorisés.

* **[!UICONTROL Éditeur de texte enrichi]**

   Si cette case est cochée, les publications peuvent être saisies avec une annotation. Cette option n’est pas cochée par défaut.

* **[!UICONTROL Autoriser le vote]**

   Si cette case est cochée, incluez la fonction de vote pour une rubrique. Cette option n’est pas cochée par défaut.

Under the **[!UICONTROL User Moderation]** tab, specify how the posted reviews are managed. Pour plus d’informations, voir [Modération de contenu généré par les utilisateurs](moderate-ugc.md).

![modération utilisateur](assets/configure-review4.png)

* **[!UICONTROL Prémodération]**

   Si cette option est cochée, les révisions doivent être approuvées avant d’apparaître sur un site de publication. Cette option n’est pas cochée par défaut.

* **[!UICONTROL Supprimer les révisions]**

   Si cette case est cochée, le membre qui a publié la révision peut la supprimer. Cette option n’est pas cochée par défaut.

* **[!UICONTROL Refuser les révisions]**

   Si cette option est cochée, autorisez les modérateurs à refuser les révisions. Cette option n’est pas cochée par défaut.

* **[!UICONTROL Fermer/rouvrir les révisions]**

   Si cette option est cochée, autorisez les modérateurs à fermer et rouvrir les révisions. Cette option n’est pas cochée par défaut.

* **[!UICONTROL Marquer les révisions]**

   Si cette option est cochée, autorisez les membres à signaler les révisions comme inappropriées. Cette option n’est pas cochée par défaut.

* **[!UICONTROL Marquer la liste de motifs]**

   Si cette option est cochée, permettez aux membres de choisir, dans une liste déroulante, la raison pour laquelle ils signalent une révision comme inappropriée. Cette option n’est pas cochée par défaut.

* **[!UICONTROL Motif de la marque personnalisée]**

   Si cette option est cochée, autorisez les membres à indiquer leur propre raison de signaler une révision comme inappropriée. Cette option n’est pas cochée par défaut.

* **[!UICONTROL Seuil de modération]**

   Indiquez le nombre de fois où une révision doit être signalée par les membres avant que les modérateurs ne soient avertis. La valeur par défaut est une fois (1).

* **[!UICONTROL Limite de marquage]**

   Indiquez le nombre de fois où une révision doit être marquée avant d’être masquée de la vue publique. Dans le cas contraire, cette valeur doit être supérieure ou égale au **[!UICONTROL seuil de modération]**. La valeur par défaut est 5.

### Ajout d’un résumé des révisions (affichage) à une page {#adding-a-review-summary-display-to-a-page}

To add a `Reviews Summary (Display)` component to a page in author mode, locate the component

* `Communities / Reviews Summary (Display)`

et faites glisser le composant sur la page à l’endroit où le résumé d’une révision active ou fermée doit s’afficher.

For necessary information, visit [Communities Components Basics](basics.md).

When the [required client-side libraries](reviews-basics.md#essentials-for-client-side) are included, this is how the `Reviews Summary (Display)`component will appear.

![review-summary](assets/configure-review5.png)

>[!NOTE]
>
>La « moyenne » reflète les votes pour le premier élément visible dans l’onglet Évaluations autorisées de la révision qui fait l’objet d’un résumé.

### Configuration du résumé des révisions (affichage) {#configuring-reviews-summary-display}

Select the placed `Reviews Summary (Display)` component to access and select the `Configure` icon which opens the edit dialog.

![configurer](assets/configure-new.png)

Sous l’onglet **[!UICONTROL Résumé des critiques]**

![review-summary](assets/configure-review6.png)

* `Review Path`

   entrez ou accédez à l&#39;instance placée du `reviews`composant pour résumer, par exemple, si elle est ajoutée à la page Web du site [Interagir,](getting-started.md) le chemin serait le suivant :

   `/content/sites/engage/en/page/jcr:content/content/primary/reviews`

* `Include histogram`

   Si cette option est cochée, incluez un graphique à barres indiquant le nombre de chaque évaluation d’étoiles dans les révisions résumées. Cette option n’est pas cochée par défaut.

### Passage à un type de commentaire personnalisé {#changing-to-a-custom-review-type}

Le composant Révisions utilise le système de commentaires.

En modifiant le type de ressource de commentaire, le système de commentaires ne génère plus une instance d’un commentaire avec les paramètres par défaut, mais plutôt un commentaire personnalisé (étendu) par les développeurs.

Once the custom resource types is known, enter [Design Mode](../../help/sites-authoring/default-components-designmode.md) and double click on the placed `Comments` component to open a dialog with an additional tab.

Under the **[!UICONTROL Resource Types]** tab, specify the custom resourceType for new instances of the `Comments or Voting` components:

![vote de commentaires](assets/configure-review7.png)

* **[!UICONTROL Type de ressource de commentaire]**

   Accédez à resourceType d&#39;un `comment`composant étendu (commentaire unique) dans /apps. Par exemple, `/apps/social/commons/components/hbs/comments/comment`.

   Cette ressource identifie le type de ressource de l&#39;UGC créé lorsqu&#39;un visiteur publie un commentaire.

* **[!UICONTROL Type de ressource de vote]**

   Accédez à resourceType d&#39;un `voting`composant étendu dans /apps. Par exemple, `/apps/social/components/hbs/voting`.

   Cette ressource identifie le type de ressource de l&#39;UGC créé lorsqu&#39;un visiteur publie un vote.

* **[!UICONTROL Type de ressource système de commentaires]**

   Accédez à resourceType d&#39;un `comments`composant étendu (système de commentaires) dans /apps. Leave blank unless the page template [dynamically includes](scf.md#add-or-include-a-communities-component) the Comment System in the underlying script instead of being added to the page as a resource (comments node). Learn more by reading about the [{{include}} helper](handlebars-helpers.md#include).

## Expérience des visiteurs {#site-visitor-experience}

### Modérateurs et administrateurs {#moderators-and-administrators}

Lorsque l’utilisateur connecté dispose de privilèges de modérateur ou d’administrateur, il peut se charger d’activités de modération autorisées par la configuration du composant, peu importe qui a créé la révision.

### Membres {#members}

Lorsque le visiteur est connecté, selon la configuration, il peut:

* Publier une nouvelle révision
* Modifier leur propre révision
* Supprimer leur propre révision
* Signaler les commentaires des autres parties

Une seule évaluation est autorisée par membre.  Le membre peut modifier son évaluation à tout moment.

### Anonyme {#anonymous}

Les visiteurs non connectés peuvent lire les révisions publiées et les traduire lorsque cela est possible. Toutefois, ils ne sont pas autorisés à ajouter une évaluation ou une révision, ni à marquer celles d’autres membres.

## Informations supplémentaires {#additional-information}

More information may be found on the [Review Essentials](reviews-basics.md) page for developers.

For moderation of posted comments, see [Moderating User Generated Content](moderate-ugc.md).

Pour des informations sur la traduction des commentaires publiés, voir [Traduction de contenu généré par les utilisateurs](translate-ugc.md).
