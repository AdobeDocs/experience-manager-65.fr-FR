---
title: Modération du contenu de la communauté
seo-title: Modération du contenu de la communauté
description: Concepts et actions de modération
seo-description: Concepts et actions de modération
uuid: 5c991d3a-0037-4d78-8f91-bb62e44441fa
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 6866d209-5789-4ef9-bc3c-d644d4fb4b1c
docset: aem65
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1524'
ht-degree: 3%

---


# Modération du contenu de la communauté {#moderating-community-content}

## Présentation {#overview}

Le contenu de la communauté, également appelé contenu généré par l’utilisateur (UGC), est créé lorsqu’un membre (connecté au visiteur du site) publie le contenu d’un site communautaire publié par le biais d’une interaction avec l’un des composants de la communauté suivants :

* [Blog](/help/communities/blog-feature.md) : les membres publient un article de blog ou un commentaire.
* [Calendrier](/help/communities/calendar.md) : les membres publient un événement de calendrier ou un commentaire.
* [Commentaires](/help/communities/comments.md) : les membres postent un commentaire ou répondent à un commentaire.

* [Forum](/help/communities/forum.md) : les membres publient une nouvelle rubrique ou répondent à une rubrique.
* [Idée](/help/communities/ideation-feature.md) : les membres publient une idée ou un commentaire.
* [QnA](/help/communities/working-with-qna.md) : les membres créent une question ou répondent à une question.
* [Critiques](/help/communities/reviews.md) : les membres publient un commentaire lorsqu&#39;ils évaluent un article.

La modération de l’UGC est utile pour reconnaître les contributions positives et pour limiter les contributions négatives (comme le spam et le langage abusif). L’UGC peut être modéré à partir de plusieurs environnements :

* [Stockage du contenu de la communauté](working-with-srp.md)

* [Console de modération en bloc](moderation.md)

   La console Modération est accessible aux administrateurs et aux [modérateurs de la communauté](/help/communities/users.md) dans l’environnement public ainsi qu’aux administrateurs de l’environnement d’auteur. Cela est possible lorsque le contenu de la communauté est stocké dans un [magasin commun](/help/communities/working-with-srp.md).

* [Modération en contexte](in-context.md)

   La modération dans l’environnement de publication peut être effectuée par les administrateurs et les modérateurs de la communauté directement sur la page sur laquelle le contenu a été publié.

## Actions de modération {#moderation-actions}

Les actions qui peuvent être exécutées sur du contenu publié (UGC) varient en fonction de l’identité de l’utilisateur et de l’environnement. Le tableau ci-dessous utilise la terminologie suivante pour décrire les différents rôles en fonction de l’identité de l’utilisateur :

* `Admin`

   Utilisateur membre du groupe [community-administrateurs](users.md).

* `Moderator`

   Membre d’un groupe [modérateurs de la communauté](users.md#publishenvironmentusersandgroups) (avec [autorisations de modérateur](in-context.md#moderatorpermissions)).

* `Creator`

   Utilisateur qui a publié le contenu.

* `Member`

   Utilisateur connecté sans autorisations spéciales.

* `Visitor`

   Utilisateur anonyme.

<table>
 <tbody>
  <tr>
   <td> </td>
   <td><strong>Admin</strong></td>
   <td><strong>Modérateur</strong></td>
   <td><strong>Créateur</strong></td>
   <td><strong>Membre</strong></td>
   <td><strong>Visiteur</strong></td>
   <td><strong>Événement<br /> déclenché</strong></td>
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
   <td><strong>Indicateur/<br /> Unflag</strong></td>
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

### Modifier / Supprimer {#edit-delete}

Une fois qu’une publication a été créée, elle peut être modifiée ou supprimée par le créateur, un administrateur ou un modérateur de la communauté.

Lorsque l’UGC est supprimé, il est supprimé du référentiel et ne peut pas être récupéré.

### Couper {#cut}

Il est possible pour un administrateur ou un modérateur de communauté de déplacer un ou plusieurs sujets de forum ou questions QnA d’un emplacement à un autre. Cela inclut d’un site communautaire à un autre site communautaire, à condition que le même membre dispose de privilèges de modération sur les deux sites.

En sélectionnant l’action Couper, le contenu est copié dans le Presse-papiers. Plusieurs publications peuvent être copiées et déplacées en tant que groupe vers le nouvel emplacement.

![cutugc](assets/cutugc.png)

![putbackugc](assets/putbackugc.png)

À l’autre emplacement, lorsque du contenu est présent dans le Presse-papiers, un bouton Coller est visible en regard de Nouvelle publication avec un numéro identifiant le nombre de publications qui seront collées. Le bouton Coller permet d’effacer le Presse-papiers au lieu de le coller.

![pasteugc](assets/pasteugc.png)

![pasteugc1](assets/pasteugc1.png)

### Refuser {#deny}

Un modérateur peut interdire à UGC de rester visible sur le site publié. Pour les administrateurs et les modérateurs de la communauté, la publication est toujours disponible et annotée comme indésirable.

### Fermer / rouvrir {#close-reopen}

L’action Fermer fonctionne sur l’ensemble du fil de conversation (sujet du forum ou commentaire initial) et inclut toutes les publications ou réponses ultérieures.

Une fois fermé, non seulement il n’est plus possible de répondre, mais aucune action de modération n’est autorisée non plus.

Pour effectuer toute opération, la rubrique ou le commentaire doit être rouvert.

L’action Fermer/rouvrir peut être entreprise par des administrateurs ou des modérateurs de la communauté.

### Indicateur / Sans indicateur {#flag-unflag}

Le balisage est un moyen pour tout membre connecté, à l’exception de l’auteur du contenu, d’indiquer qu’il y a un problème avec le contenu d’une publication. Une fois marqué, une icône d’annulation d’indicateur s’affiche, permettant au même membre de démarquer le contenu.

La modération contextuelle peut être configurée pour permettre aux membres de sélectionner un motif lors du marquage d’une publication. La liste des motifs d’indicateur sélectionnables est configurable, y compris la saisie ou non d’un motif personnalisé. La raison de l&#39;indicateur est enregistrée avec l&#39;UGC, mais la raison ne déclenche aucune action particulière. Seul le nombre d’indicateurs déclenche une notification. Le contenu marqué est annoté en tant que tel, de sorte que les modérateurs puissent agir sur celui-ci.

Le système effectue le suivi de tous les indicateurs, qui a marqué et de la raison de l’indicateur et envoie un événement lorsque le seuil a été atteint. Si l’UGC est autorisé par un modérateur de communauté, ces indicateurs sont archivés. Après avoir autorisé et archivé, s&#39;il y a des signalements ultérieurs, ils seraient archivés comme s&#39;il n&#39;y avait pas eu de signalements antérieurs.

### Autoriser {#allow}

L’action Autoriser est une option pour l’UGC qui a été marquée, refusée ou n’a pas été approuvée dans un système prémodéré. L’action Autoriser effacera tout état marqué ou refusé/indésirable présent et archivera toutes les données marquées.

## Concepts de modération courants {#common-moderation-concepts}

### Prémodération {#premoderation}

Lorsque l’UGC est prémodéré, la publication n’apparaît pas sur le site publié tant qu’elle n’a pas été approuvée par une action de modération. Lors de la création d’un [site communautaire](/help/communities/sites-console.md), cochez la case [Contenu prémodéré](sites-console.md#moderation) pour activer la prémodération pour l’ensemble du site. Une fois les composants placés sur une page, les composants qui prennent en charge la modération peuvent être configurés pour la prémodération à l’aide d’un paramètre dans leur boîte de dialogue de modification :

* [](comments.md) Commentaires et  [](reviews.md)
révisions dans Modération **** utilisateur >  **[!UICONTROL Prémodération]**.

* [Forum](/help/communities/forum.md),  [idéation](/help/communities/ideation-feature.md),  [QnA](/help/communities/working-with-qna.md) et  [](/help/communities/calendar.md)
calendriers dans  **[!UICONTROL Paramètres> Modéré.]******

### Détection des messages indésirables {#spam-detection}

La détection des messages indésirables est une fonctionnalité de modération automatique qui filtres les éléments indésirables du contenu généré par l’utilisateur envoyé en les marquant comme des messages indésirables. Une fois activé, il identifie si le contenu généré par l’utilisateur est indésirable ou non en fonction d’une collection préconfigurée de mots indésirables. Les mots de spam par défaut sont fournis dans la section

`/libs/settings/community/sites/moderation/spamdetector-conf/profiles/spam_words.txt`.

Cependant, pour personnaliser ou étendre les mots de spam par défaut, créez un ensemble de mots dans le répertoire /apps suivant la structure des mots de spam par défaut au moyen de [overlay](/help/communities/overlay-comments.md).

Une publication générée par l’utilisateur (dans tous les types de contenu, par exemple les blogs, les forums et les commentaires) contenant des mots indésirables est marquée du texte &quot;Cette publication a été classée comme indésirable&quot; au-dessus de la publication.

Le modérateur peut voir une telle publication et la marquer de la même manière pour autoriser ou refuser l’affichage sur le site. Les actions de modération sur ces publications peuvent être exécutées en contexte ou via l’interface utilisateur de modération en bloc.

![spamdetection](assets/spamdetection.png)

Pour activer le moteur de détection des messages indésirables, procédez comme suit :

1. Ouvrez [Web Console](https://localhost:4502/system/console/configMgr) en accédant à `/system/console/configMgr`.

1. Recherchez la configuration **Modération automatique AEM Communities** et modifiez-la.
1. Ajoutez l&#39;entrée **[!UICONTROL SpamProcess]**.

![spamprocess](assets/spamprocess.png)

>[!NOTE]
>
>La détection des messages indésirables n&#39;est mise en oeuvre que pour les paramètres régionaux anglais.

### Opinion {#sentiment}

L’opinion est calculée en fonction du nombre de mots-clés positifs et négatifs ([watchwords](#configuringwatchwords)) présents dans une publication (UGC).

L’analyse d’opinion utilise un ensemble de règles préconfigurées et calcule l’opinion de l’UGC. Les règles par défaut se trouvent à l’emplacement suivant : `/libs/cq/workflow/components/workflow/social/sentiments/rules.`

La valeur générée par les règles est comprise entre 1 (tous négatifs, aucun mot positif) et 10 (tous positifs, aucun mot négatif). Une valeur d’opinion de 5 est une opinion neutre et est la valeur par défaut.

Les règles définies dans le composant /libs sont les suivantes :

* Règle 1 : définissez la valeur sur 1 s’il n’y a aucun mot positif et au moins un mot négatif.
* Règle 2 : définissez la valeur sur 10 s’il n’y a pas de mots négatifs et au moins un mot positif.
* Règle 3 : définissez la valeur sur 3 s’il y a plus de mots négatifs que de mots positifs.
* Article 4 : définissez la valeur sur 8 s’il y a plus de mots positifs que de mots négatifs.

Pour remplacer ou ajouter des règles, créez un ensemble de règles dans le répertoire /apps suivant la structure des règles par défaut. Modifiez la configuration de l’opinion afin d’identifier l’emplacement des règles.

Une fois analysée, l’opinion est stockée avec l’UGC.

A partir de la [console de modération en bloc](/help/communities/moderation.md), il est possible de filtrer et de vue l’UGC selon que l’opinion est négative, neutre ou positive.

#### Mots-clés {#watchwords}

Les communautés d’AEM fournissent un *analyseur de mots d’attente* en tant qu’étape du processus d’évaluation de [l’opinion](#sentiment). La contribution à la valeur d’opinion fournie par les mots de contrôle est due à la comparaison des mots de contrôle négatifs et positifs utilisés dans le contenu publié, ainsi que des mots interdits.

#### Configuration de l’opinion et des mots de contrôle {#configure-sentiment-and-watchwords}

La liste des mots d’ordre positifs et négatifs peut être personnalisée, de même que les règles d’opinion.

La liste par défaut des mots-clés peut être entrée en tant que propriétés d&#39;un noeud dans le référentiel, comme dans le cas par défaut ou en remplaçant la valeur par défaut par la configuration du service OSGi `sentimentprocess.name` avec la liste de mots.

Il est également possible de modifier **sentimentprocess.name** pour référencer l’emplacement d’un ensemble personnalisé de règles d’opinion.

Pour configurer l’opinion et les mots de contrôle :

* Connectez-vous à votre instance de création  en tant qu’administrateur.
* Ouvrez [Console Web](https://localhost:4502/system/console/configMgr).
* Recherchez `sentimentprocess.name`.
* Sélectionnez la configuration à ouvrir en mode d’édition.

![sentimentprocess](assets/sentimentprocess.png)

* **Mots de contrôle positifs**

   Liste séparée par des virgules de mots qui contribuent à une opinion positive qui remplace les valeurs par défaut. La valeur par défaut est une liste vide.

* **Mots de contrôle négatifs**

   Liste séparée par des virgules de mots qui contribuent à une opinion négative qui remplace les valeurs par défaut. La valeur par défaut est une liste vide.

* **Chemin explicite vers le noeud Watchwords**

   Emplacement du référentiel d’un noeud contenant les propriétés par défaut `positive` et `negative` spécifiant les mots de passe par défaut. La valeur par défaut est `/libs/settings/community/watchwords/default`.

* **Règles d’opinion**

   Emplacement du référentiel des règles de calcul de l’opinion sur la base de mots-clés positifs et négatifs. La valeur par défaut est `/libs/cq/workflow/components/workflow/social/sentiments/rules` (toutefois, aucun flux de travail n’est impliqué).

Voici un exemple d&#39;entrée personnalisée pour les mots-clés par défaut, lorsque `Explicit Path to Watchwords Node` est défini sur `/libs/settings/community/watchwords/default`.

![crxde](assets/crxde.png)

### Autorisations du modérateur {#moderator-permissions}

Les autorisations suivantes, lorsqu&#39;elles sont attribuées à la même ressource, sont collectivement appelées `moderator permissions` :

* `Read`
* `Modify`
* `Create`
* `Delete`
* `Replicate`

