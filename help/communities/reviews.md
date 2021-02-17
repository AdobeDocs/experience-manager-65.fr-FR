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

Le composant `Reviews` est un composite des composants [Comments](comments.md) et [Rating](rating.md) prêts à être utilisés.

Le composant `Reviews Summary (Display)` fournit un résumé d&#39;une instance principale ou fermée d&#39;un composant `Reviews` à afficher ailleurs sur le site.

>[!NOTE]
>
>La publication anonyme d’une révision n’est pas possible. Les visiteurs du site doivent s&#39;inscrire (devenir membre) et se connecter pour participer. Les visiteurs connectés peuvent mettre à jour leurs révisions à tout moment.

## Ajout d’une révision à une page {#adding-a-review-to-a-page}

Pour ajouter un composant `Reviews` à une page en mode création, utilisez l&#39;explorateur de composants pour localiser `Communities / Reviews` et faites-le glisser sur une page, par exemple une position relative à la fonction à réviser pour les utilisateurs.

Pour obtenir les informations nécessaires, consultez [Community Components Basics](basics.md).

Lorsque les [bibliothèques client requises](reviews-basics.md#essentials-for-client-side) sont incluses, c&#39;est ainsi que le composant `Reviews` s&#39;affiche.

![create-review](assets/create-review.png)

## Configuration des révisions {#configuring-reviews}

Sélectionnez le composant `Reviews` placé auquel accéder et sélectionnez l&#39;icône `Configure` qui ouvre la boîte de dialogue de modification.

![configure-new](assets/configure-new.png)

Sous l&#39;onglet **[!UICONTROL Qualifications autorisées]**, indiquez la liste complète des évaluations à afficher aux membres. La première note doit être une note globale/générale, car c&#39;est la note qui fournit la note moyenne pour la composante `Review Summary (Display)`. Les deux évaluations suivantes dans la configuration par défaut doivent recevoir un titre différent, autre que &quot;Subrating 1&quot; ou &quot;Subrating 2&quot;.

![évaluation autorisée](assets/configure-review1.png)

* **[!UICONTROL Evaluations autorisées]**

   Liste de notes à partir de laquelle un membre peut choisir.

   Utilisez les flèches Haut et Bas, ainsi que les boutons de suppression, pour modifier les choix visibles.

   Cliquez sur **[!UICONTROL Ajouter un élément]** pour ajouter un autre choix d’évaluation.

Sous l&#39;onglet **[!UICONTROL Classifications requises]**, entrez à nouveau les éléments de la liste de **[!UICONTROL Classifications autorisées]** qui doivent être évalués. Si un élément est spécifié uniquement dans l’onglet Évaluations autorisées, il peut être laissé non signalé lorsqu’il est soumis par le membre.

Sur le site web, les évaluations requises sont signalées d’un astérisque. Si un élément obligatoire n’est pas marqué, un message s’affiche à l’intention du membre, et sa soumission est refusée jusqu’à ce que toutes les évaluations requises soient marquées.

![qualification requise](assets/configure-review2.png)

* **[!UICONTROL Evaluations requises]**

   Un sous-ensemble d’évaluations autorisées, indiquant les évaluations requises.

   Utilisez les flèches Haut et Bas, ainsi que les boutons de suppression, pour modifier les choix visibles.

   Cliquez sur **[!UICONTROL Ajouter un élément]** pour ajouter un autre choix de réponse.

>[!NOTE]
>
>Si un élément est saisi dans l&#39;onglet **[!UICONTROL Classifications requises]** qui n&#39;est pas spécifié dans l&#39;onglet **[!UICONTROL Classifications autorisées]**, il n&#39;est pas inclus dans les éléments à évaluer.

Sous l&#39;onglet **[!UICONTROL Révisions]**, indiquez comment les révisions sont gérées.

![Révisions](assets/configure-review3.png)

* **[!UICONTROL Permettre des réponses]**

   Si cette option est cochée, autorisez les réponses aux révisions. Cette option n’est pas cochée par défaut.

* **[!UICONTROL Fermé]**

   Si cette option est cochée, la révision est fermée aux nouveaux examens et réponses. Cette option n’est pas cochée par défaut.

* **[!UICONTROL Autoriser les transferts de fichiers]**

   Si cette option est cochée, autorisez le téléchargement des pièces jointes pour la révision. Cette option n’est pas cochée par défaut.

* **Taille maximale du fichier**

   Ne s’applique que si **[!UICONTROL Autoriser les téléchargements de fichiers]** est coché. Ce champ limite la taille (en octets) d’un fichier téléchargé. La valeur par défaut est de 10 Mo.

* **[!UICONTROL Longueur de message max.]**

   Nombre maximal de caractères pouvant être saisis dans la zone de texte. La valeur par défaut est de 4 096 caractères.

* **[!UICONTROL Types de fichier autorisés]**

   Ne s’applique que si **[!UICONTROL Autoriser les téléchargements de fichiers]** est coché. Liste séparée par des virgules d’extensions de fichiers avec le séparateur &quot;point&quot;. Par exemple : .jpg, .jpeg, .png, .doc, .docx, .pdf. Si des types de fichier sont spécifiés, ceux qui ne sont pas spécifiés ne seront pas autorisés. Par défaut, aucun type de fichier n’est spécifié, de sorte que tous les types de fichier soient autorisés.

* **[!UICONTROL Éditeur de texte enrichi]**

   Si cette case est cochée, les publications peuvent être saisies avec une annotation. Cette option n’est pas cochée par défaut.

* **[!UICONTROL Autoriser le vote]**

   Si cette case est cochée, incluez la fonction de vote pour une rubrique. Cette option n’est pas cochée par défaut.

Sous l’onglet **[!UICONTROL Modération utilisateur]**, indiquez comment les révisions publiées sont gérées. Pour plus d’informations, voir [Modération de contenu généré par les utilisateurs](moderate-ugc.md).

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

Pour ajouter un composant `Reviews Summary (Display)` à une page en mode création, recherchez le composant.

* `Communities / Reviews Summary (Display)`

et faites glisser le composant sur la page à l’endroit où le résumé d’une révision active ou fermée doit s’afficher.

Pour obtenir les informations nécessaires, consultez [Community Components Basics](basics.md).

Lorsque les [bibliothèques client requises](reviews-basics.md#essentials-for-client-side) sont incluses, c&#39;est ainsi que le composant `Reviews Summary (Display)`s&#39;affiche.

![review-summary](assets/configure-review5.png)

>[!NOTE]
>
>La « moyenne » reflète les votes pour le premier élément visible dans l’onglet Évaluations autorisées de la révision qui fait l’objet d’un résumé.

### Configuration du résumé des révisions (affichage) {#configuring-reviews-summary-display}

Sélectionnez le composant `Reviews Summary (Display)` placé auquel accéder et sélectionnez l&#39;icône `Configure` qui ouvre la boîte de dialogue de modification.

![configurer](assets/configure-new.png)

Sous l’onglet **[!UICONTROL Résumé des critiques]**

![review-summary](assets/configure-review6.png)

* `Review Path`

   entrez ou recherchez l&#39;instance placée du composant `reviews`pour résumer, par exemple, si elle est ajoutée à la page Web du site [Geometrixx Interagir,](getting-started.md), le chemin serait :

   `/content/sites/engage/en/page/jcr:content/content/primary/reviews`

* `Include histogram`

   Si cette option est cochée, incluez un graphique à barres indiquant le nombre de chaque évaluation d’étoiles dans les révisions résumées. Cette option n’est pas cochée par défaut.

### Passage à un type de commentaire personnalisé {#changing-to-a-custom-review-type}

Le composant Révisions utilise le système de commentaires.

En modifiant le type de ressource de commentaire, le système de commentaires ne génère plus une instance d’un commentaire avec les paramètres par défaut, mais plutôt un commentaire personnalisé (étendu) par les développeurs.

Une fois les types de ressources personnalisées connus, saisissez [Mode de conception](../../help/sites-authoring/default-components-designmode.md) et cliquez sur le doublon sur le composant `Comments` placé pour ouvrir une boîte de dialogue avec un onglet supplémentaire.

Sous l&#39;onglet **[!UICONTROL Types de ressources]**, spécifiez le type de ressource personnalisé pour les nouvelles instances des composants `Comments or Voting` :

![vote de commentaires](assets/configure-review7.png)

* **[!UICONTROL Type de ressource de commentaire]**

   Accédez à resourceType d&#39;un composant `comment`étendu (commentaire unique) dans /apps. Par exemple, `/apps/social/commons/components/hbs/comments/comment`.

   Cette ressource identifie le type de ressource de l&#39;UGC créé lorsqu&#39;un visiteur publie un commentaire.

* **[!UICONTROL Type de ressource de vote]**

   Accédez au resourceType d&#39;un composant `voting`étendu dans /apps. Par exemple, `/apps/social/components/hbs/voting`.

   Cette ressource identifie le type de ressource de l&#39;UGC créé lorsqu&#39;un visiteur publie un vote.

* **[!UICONTROL Type de ressource système de commentaires]**

   Accédez à resourceType d&#39;un composant `comments`étendu (Comment System) dans /apps. Ne renseignez pas ce champ, sauf si le modèle de page [inclut dynamiquement ](scf.md#add-or-include-a-communities-component) le système de commentaires dans le script sous-jacent au lieu d’être ajouté à la page en tant que ressource (noeud de commentaires). Pour en savoir plus, consultez l&#39;aide [{{include}](handlebars-helpers.md#include).

## Expérience des visiteurs {#site-visitor-experience}

### Modérateurs et administrateurs {#moderators-and-administrators}

Lorsque l’utilisateur connecté dispose de privilèges de modérateur ou d’administrateur, il peut se charger d’activités de modération autorisées par la configuration du composant, peu importe qui a créé la révision.

### Membres  {#members}

Lorsque le visiteur est connecté, selon la configuration, il peut:

* Publier une nouvelle révision
* Modifier leur propre révision
* Supprimer leur propre révision
* Signaler les commentaires des autres parties

Une seule évaluation est autorisée par membre.  Le membre peut modifier son évaluation à tout moment.

### Anonyme  {#anonymous}

Les visiteurs non connectés peuvent lire les révisions publiées et les traduire lorsque cela est possible. Toutefois, ils ne sont pas autorisés à ajouter une évaluation ou une révision, ni à marquer celles d’autres membres.

## Informations supplémentaires {#additional-information}

Pour plus d&#39;informations, consultez la page [Review Essentials](reviews-basics.md) destinée aux développeurs.

Pour la modération des commentaires publiés, voir [Modération du contenu généré par l’utilisateur](moderate-ugc.md).

Pour des informations sur la traduction des commentaires publiés, voir [Traduction de contenu généré par les utilisateurs](translate-ugc.md).
