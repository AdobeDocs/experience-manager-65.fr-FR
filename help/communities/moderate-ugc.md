---
title: Modération de contenu de la communauté
description: Découvrez comment modérer le contenu généré par l’utilisateur afin que vous puissiez reconnaître les contributions positives et limiter les contributions négatives, telles que les spams et le langage abusif.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: 22276580-e6bc-41c5-9ac3-e8f291f676b7
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1516'
ht-degree: 3%

---

# Modération de contenu de la communauté {#moderating-community-content}

## Vue d’ensemble {#overview}

Le contenu de la communauté, également appelé contenu généré par l’utilisateur, est créé lorsqu’un membre (connecté au visiteur du site) publie du contenu d’un site de la communauté publié en interagissant avec l’un des composants de la communauté suivants :

* [Blog](/help/communities/blog-feature.md): les membres publient un article de blog ou un commentaire.
* [Calendrier](/help/communities/calendar.md): les membres publient un événement ou un commentaire de calendrier.
* [Commentaires](/help/communities/comments.md): les membres publient un commentaire ou une réponse à un commentaire.

* [Forum](/help/communities/forum.md): les membres publient un nouveau sujet ou répondent à un sujet.
* [Idéation](/help/communities/ideation-feature.md): les membres publient une idée ou un commentaire.
* [Q&amp;R](/help/communities/working-with-qna.md): les membres créent une question ou répondent à une question.
* [Révisions](/help/communities/reviews.md): les membres publient un commentaire lors de l’évaluation d’un élément.

La modération du contenu créé par l’utilisateur est utile pour reconnaître les contributions positives et limiter celles qui sont négatives (comme les spams et le langage abusif). Le contenu généré par l’utilisateur peut être modéré à partir de plusieurs environnements :

* [Stockage de contenu communautaire](working-with-srp.md)

* [Console de modération en bloc](moderation.md)

  La console Modération est accessible aux administrateurs et aux [modérateurs de communauté](/help/communities/users.md) dans l’environnement public et par les administrateurs dans l’environnement de création. Cela est possible lorsque le contenu de la communauté est stocké dans une [magasin commun](/help/communities/working-with-srp.md).

* [Modération dans le contexte](in-context.md)

  La modération dans l’environnement de publication peut être effectuée par les administrateurs et les modérateurs de la communauté directement sur la page où le contenu a été publié.

## Actions de modération {#moderation-actions}

Les actions pouvant être effectuées sur du contenu publié (UGC) varient en fonction de l’identité de l’utilisateur et de l’environnement. Le tableau ci-dessous utilise la terminologie suivante pour décrire les différents rôles en fonction de l’identité de l’utilisateur :

* `Admin`

  Un utilisateur qui est membre de [community-administrators](users.md) groupe.

* `Moderator`

  Un membre d’une [modérateurs de communauté](users.md#publishenvironmentusersandgroups) groupe (has [autorisations du modérateur](in-context.md#moderatorpermissions)).

* `Creator`

  Utilisateur qui a publié le contenu.

* `Member`

  Utilisateur connecté sans autorisations spéciales.

* `Visitor`

  Un utilisateur anonyme.

<table>
 <tbody>
  <tr>
   <td> </td>
   <td><strong>Admin</strong></td>
   <td><strong>Modérateur</strong></td>
   <td><strong>Créateur</strong></td>
   <td><strong>Membre</strong></td>
   <td><strong>Visiteur</strong></td>
   <td><strong>Événement<br /> Déclenché</strong></td>
   <td><strong>Prémodéré</strong></td>
  </tr>
  <tr>
   <td><strong>Modifier/<br /> Supprimer</strong></td>
   <td>X</td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Couper</strong></td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Refuser</strong></td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td>X</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Fermer/<br /> Réouvrir</strong></td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td>X</td>
   <td>X<br /> </td>
  </tr>
  <tr>
   <td><strong>Flag/<br /> Unflag</strong></td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td>X</td>
   <td> </td>
   <td>X</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Autoriser</strong></td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td>X</td>
   <td>X</td>
  </tr>
 </tbody>
</table>

### Modifier/Supprimer {#edit-delete}

Une fois une publication créée, elle peut être modifiée ou supprimée par le créateur, un administrateur ou un modérateur de la communauté.

Lorsque le contenu créé par l’utilisateur est supprimé, il est supprimé du référentiel et ne peut pas être récupéré.

### Couper {#cut}

Il est possible pour un administrateur ou un modérateur de communauté de déplacer un ou plusieurs sujets de forum ou questions Q&amp;R d’un emplacement à un autre. Cela inclut d’un site de communauté à un autre site de communauté, à condition que le même membre dispose de privilèges de modération sur les deux sites.

Lorsque vous sélectionnez l’action Couper , le contenu est copié dans le Presse-papiers. Plusieurs publications peuvent être copiées et déplacées sous la forme d’un groupe vers le nouvel emplacement.

![cutugc](assets/cutugc.png)

![putbackugc](assets/putbackugc.png)

À l’autre emplacement, lorsque du contenu est présent dans le Presse-papiers, un bouton Coller est visible en regard de Nouvelle publication, avec un nombre identifiant le nombre de publications qui seront collées. Le bouton Coller comprend une option permettant d’effacer le Presse-papiers au lieu de coller.

![pasteugc](assets/pasteugc.png)

![pasteugc1](assets/pasteugc1.png)

### Refuser {#deny}

Un modérateur peut interdire au contenu créé par l’utilisateur de rester visible sur le site publié. Pour les administrateurs et les modérateurs de la communauté, la publication est toujours disponible et annotée comme spam.

### Fermer/rouvrir {#close-reopen}

L&#39;action Fermer fonctionne sur l&#39;ensemble du fil de conversation (un sujet de forum ou le commentaire initial) et inclut toutes les publications ou réponses suivantes.

Une fois fermées, non seulement les réponses ne sont plus possibles, mais aucune action de modération n’est autorisée.

Pour effectuer toute opération, la rubrique ou le commentaire doit être rouvert.

L’action Fermer/rouvrir peut être entreprise par des administrateurs ou des modérateurs de la communauté.

### Indicateur/désindicateur {#flag-unflag}

Le marquage est un moyen pour tout membre connecté, à l’exception du créateur du contenu, d’indiquer qu’il existe un problème avec le contenu d’une publication. Une fois le contenu marqué, une icône de non-indicateur s’affiche, ce qui permet au même membre de démarquer le contenu.

La modération contextuelle peut être configurée pour permettre aux membres de sélectionner un motif lors du marquage d’une publication. La liste des motifs d’indicateur sélectionnables est configurable, y compris si un motif personnalisé peut être saisi. La raison de l’indicateur est enregistrée avec le contenu généré par l’utilisateur, mais la raison ne déclenche aucune action particulière. Seul le nombre d’indicateurs déclenche une notification. Le contenu marqué est annoté en tant que tel, de sorte que les modérateurs puissent agir dessus.

Le système effectue le suivi de tous les indicateurs, qui ont été marqués et de la raison de l’indicateur et envoie un événement lorsque le seuil a été atteint. Si le contenu généré par l’utilisateur est autorisé par un modérateur de communauté, ces indicateurs sont archivés. Après autorisation et archivage, s’il existe des indicateurs suivants, ils seraient archivés comme s’il n’y avait eu aucun indicateur précédent.

### Autoriser {#allow}

L’action Autoriser est une option pour le contenu généré par l’utilisateur qui a été marqué, refusé ou qui n’a pas été approuvé dans un système prémodéré. L’action Autoriser efface tout état marqué ou refusé/indésirable présent et archive toutes les données marquées.

## Concepts de modération courants {#common-moderation-concepts}

### Prémodération {#premoderation}

Lorsque le contenu généré par l’utilisateur est prémodéré, la publication n’apparaît pas sur le site publié tant qu’elle n’a pas été approuvée par une action de modération. Lors de la création d’un [site communautaire](/help/communities/sites-console.md), en cochant la case [Contenu prémodéré](sites-console.md#moderation) active la prémodération pour l’ensemble du site. Lorsque des composants sont placés sur une page, les composants qui prennent en charge la modération peuvent être configurés pour la prémodération à l’aide d’un paramètre de leur boîte de dialogue de modification :

* [Commentaires](comments.md) et [critiques](reviews.md)
in **[!UICONTROL Modération d’utilisateur]** > **[!UICONTROL Prémodération]**.

* [Forum](/help/communities/forum.md), [idéation](/help/communities/ideation-feature.md), [Q&amp;R](/help/communities/working-with-qna.md), et [calendar](/help/communities/calendar.md)
in **[!UICONTROL Paramètres]** > **[!UICONTROL Modéré]**.

### Détection des messages indésirables {#spam-detection}

La détection des messages indésirables est une fonctionnalité de modération automatique qui filtre les éléments indésirables du contenu généré par l’utilisateur envoyé en les marquant comme des messages indésirables. Une fois activé, il identifie si un contenu généré par l’utilisateur est du spam ou non en fonction d’un ensemble préconfiguré de mots-clés indésirables. Les mots de spam par défaut sont fournis à l’adresse

`/libs/settings/community/sites/moderation/spamdetector-conf/profiles/spam_words.txt`.

Cependant, pour personnaliser ou étendre les mots indésirables par défaut, créez un ensemble de mots dans le répertoire /apps en suivant la structure des mots indésirables par défaut avec [superposition](/help/communities/overlay-comments.md).

Une publication générée par l’utilisateur (dans tous les types de contenu, les blogs, les forums et les commentaires, par exemple) contenant des mots &quot;spam&quot; est marquée avec le texte &quot;Cette publication a été classée comme spam&quot; au-dessus de la publication.

Le modérateur peut voir une telle publication et la marquer de la même manière pour autoriser ou refuser l’affichage sur le site. Les actions de modération sur ces publications peuvent être effectuées dans le contexte ou via l’interface utilisateur de modération en bloc.

![spamdétection](assets/spamdetection.png)

Pour activer le moteur de détection de spam, procédez comme suit :

1. Ouvrir [Console web](https://localhost:4502/system/console/configMgr), en accédant à `/system/console/configMgr`.

1. Localiser **Modération automatique d’AEM Communities** et modifiez-la.
1. Ajoutez la variable **[!UICONTROL SpamProcess]** entrée .

![spamprocess](assets/spamprocess.png)

>[!NOTE]
>
>La détection des messages indésirables n’est mise en oeuvre que pour les paramètres régionaux anglais.

### Opinion {#sentiment}

L’opinion est calculée en fonction du nombre de mots-clés positifs et négatifs ([watchwords](#configuringwatchwords)) présente dans une publication (contenu généré par l’utilisateur).

L’analyse de l’opinion utilise un ensemble de règles préconfigurées et calcule l’opinion du contenu généré par l’utilisateur. Les règles par défaut sont les suivantes : `/libs/cq/workflow/components/workflow/social/sentiments/rules`.

La valeur générée par les règles est comprise entre 1 (tous les mots négatifs, aucun mot positif) et 10 (tous les mots positifs, aucun mot négatif). Une valeur d’opinion de 5 est une opinion neutre et est la valeur par défaut.

Les règles définies dans le composant /libs sont les suivantes :

* Règle 1 : définissez la valeur sur 1 s’il n’existe aucun mot positif et au moins un mot négatif.
* Règle 2 : définissez la valeur sur 10 s’il n’y a pas de mots négatifs et au moins un mot positif.
* Règle 3 : définissez la valeur sur 3 s’il y a plus de mots négatifs que de mots positifs.
* Règle 4 : définissez la valeur sur 8 s’il y a plus de mots positifs que négatifs.

Pour remplacer ou ajouter des règles, créez un ensemble de règles dans le répertoire /apps suivant la structure des règles par défaut. Modifiez la configuration de l’opinion afin d’identifier l’emplacement des règles.

Une fois analysée, l’opinion est stockée avec le contenu généré par l’utilisateur.

Dans la [console de modération en bloc](/help/communities/moderation.md), il est possible de filtrer et d’afficher le contenu généré par l’utilisateur selon que l’opinion est négative, neutre ou positive.

#### Watchwords {#watchwords}

AEM Communities fournit une *analyseur de mots-clés* comme étape du processus d’évaluation [sentiment](#sentiment). La contribution à la valeur d’opinion fournie par les mots-clés est due à la comparaison des mots-clés négatifs et positifs utilisés dans le contenu publié et des mots interdits.

#### Configuration de l’opinion et des mots de contrôle {#configure-sentiment-and-watchwords}

Il est possible de personnaliser la liste des mots-clés positifs et négatifs, de même que les règles d’opinion.

La liste par défaut des mots-clés peut être saisie en tant que propriétés d’un noeud dans le référentiel, comme par défaut ou en remplaçant la valeur par défaut par la configuration du service OSGi. `sentimentprocess.name` avec la liste des mots.

La variable **sentimentprocess.name** peut également être modifié pour référencer l’emplacement d’un ensemble personnalisé de règles d’opinion.

Pour configurer l’opinion et les mots-clés :

* Connectez-vous à votre instance d’auteur en tant qu’administrateur 
* Ouvrir [Console web](https://localhost:4502/system/console/configMgr).
* Localiser `sentimentprocess.name`.
* Sélectionnez la configuration afin de pouvoir l’ouvrir en mode d’édition.

![sentimentprocess](assets/sentimentprocess.png)

* **Mots-clés positifs**

  Liste de mots séparés par des virgules, qui contribuent à une opinion positive qui remplace les valeurs par défaut. La valeur par défaut est une liste vide.

* **Mots-clés négatifs**

  Liste de mots séparés par des virgules, qui contribuent à une opinion négative qui remplace les valeurs par défaut. La valeur par défaut est une liste vide.

* **Chemin explicite vers le noeud Watchwords**

  Emplacement du référentiel d’un noeud contenant la valeur par défaut `positive` et `negative` propriétés spécifiant les mots-clés par défaut. La valeur par défaut est `/libs/settings/community/watchwords/default`.

* **Règles d’opinion**

  Emplacement du référentiel des règles pour calculer l’opinion selon des mots-clés positifs et négatifs. Par défaut : `/libs/cq/workflow/components/workflow/social/sentiments/rules` (cependant, il n’y a plus de workflow impliqué).

Voici un exemple d’entrée personnalisée pour les mots-clés par défaut, lorsque `Explicit Path to Watchwords Node` est défini sur `/libs/settings/community/watchwords/default`.

![crxde](assets/crxde.png)

### Autorisations du modérateur {#moderator-permissions}

Les autorisations suivantes, lorsqu’elles sont affectées à la même ressource, sont collectivement appelées `moderator permissions`:

* `Read`
* `Modify`
* `Create`
* `Delete`
* `Replicate`
