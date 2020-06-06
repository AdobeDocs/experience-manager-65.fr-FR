---
title: Score et badges des communautés
seo-title: Score et badges des communautés
description: Les scores et les badges des communautés AEM vous permettent d’identifier et de récompenser les membres de la communauté.
seo-description: Les scores et les badges des communautés AEM vous permettent d’identifier et de récompenser les membres de la communauté.
uuid: d73683df-a413-4b3c-869c-67568bfdfcf6
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ea033bb9-cb92-4c93-855f-8c902999378c
docset: aem65
tagskeywords: scoring, badging, badges, gamification
translation-type: tm+mt
source-git-commit: fb7d2a3cebda86fa4d91d2ea89ae459fa4b86fa0
workflow-type: tm+mt
source-wordcount: '2896'
ht-degree: 3%

---


# Score et badges des communautés {#communities-scoring-and-badges}

## Présentation {#overview}

La fonction de notation et de badges des communautés AEM permet d’identifier et de récompenser les membres de la communauté.

Les principaux aspects de la notation et des badges sont les suivants :

* [Attribuer des badges](#assign-and-revoke-badges) pour identifier le rôle d&#39;un membre dans la communauté.

* [Attribution de base de badges](#enable-scoring) aux membres pour encourager leur participation (quantité de contenu créé).
* [Attribution avancée de badges](/help/communities/advanced.md) pour identifier les membres comme experts (qualité du contenu créé).

**Notez** que l’attribution de badges [n’est pas activée par défaut](/help/communities/implementing-scoring.md#main-pars-text-237875536).

>[!CAUTION]
>
>La structure d’implémentation visible dans CRXDE Lite peut être modifiée une fois que l’interface utilisateur est disponible.


## Badges {#badges}

Les insignes sont placés sous le nom d&#39;un membre pour indiquer soit son rôle, soit son statut dans la communauté. Les badges peuvent être affichés sous forme d&#39;image ou de nom. Lorsqu’il est affiché sous forme d’image, le nom est inclus en tant que texte de remplacement pour l’accessibilité.

Par défaut, les badges se trouvent dans le référentiel à l’adresse

* `/libs/settings/community/badging/images`

S&#39;ils sont stockés à un autre emplacement, ils doivent être lus accessibles à tous.

Les insignes sont différenciés en UGC selon qu&#39;ils ont été attribués ou acquis selon les règles. Actuellement, les badges attribués apparaissent sous forme de texte et les badges gagnés apparaissent sous forme d’image.

### Interface utilisateur de gestion des badges {#badge-management-ui}

La console [](/help/communities/badges.md) Badges communautaires permet d&#39;ajouter des badges personnalisés qui peuvent être affichés pour un membre lorsqu&#39;ils sont gagnés (attribués) ou lorsqu&#39;ils assument un rôle spécifique dans la communauté (attribués).

### Badges attribués {#assigned-badges}

Un administrateur attribue aux membres de la communauté des badges fondés sur le rôle en fonction de leur rôle dans la communauté.

Les badges attribués (et attribués) sont stockés dans le [SRP](/help/communities/srp.md) sélectionné et ne sont pas directement accessibles. Tant qu’une interface graphique n’est pas disponible, le seul moyen d’attribuer des badges basés sur les rôles consiste à le faire avec du code ou de l’URL. Pour obtenir des instructions sur les URL, voir la section intitulée [Attribuer et révoquer des badges](#assign-and-revoke-badges).

Cette version comprend trois badges basés sur les rôles :

* **modérateur**

   `/libs/settings/community/badging/images/moderator/jcr:content/moderator.png`

* **gestionnaire de groupes**

   `/libs/settings/community/badging/images/group-manager/jcr:content/group-manager.png`

* **membre privilégié**

   `/libs/settings/community/badging/images/privileged-member/jcr:content/privileged-member.png`

![chlimage_1-98](assets/chlimage_1-98.png)

### Insignes attribués {#awarded-badges}

Le service de notation accorde aux membres de la communauté des badges récompensés en fonction des règles appliquées à leur activité dans la communauté.

Pour que les badges apparaissent comme une récompense pour l&#39;activité, deux choses doivent se produire :

* Le badge doit être [activé](#enableforcomponent) pour le composant de fonction.
* Les règles de score et de badge doivent être [appliquées](#applytopage) à la page (ou à l’ancêtre) sur laquelle le composant est placé.

La version comprend trois badges basés sur la récompense :

* **or**

   `/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png`

* **argent**

   `/libs/settings/community/badging/images/silver-badge/jcr:content/silver.png`

* **bronze**

   `/libs/settings/community/badging/images/bronze-badge/jcr:content/bronze.png`

![chlimage_1-99](assets/chlimage_1-99.png)

>[!NOTE]
>
>Les règles de score peuvent être configurées pour affecter des points négatifs aux publications marquées comme inappropriées et affecter ainsi la valeur de score. Cependant, une fois qu’un badge est gagné, il ne sera pas automatiquement supprimé en raison de la réduction du point de notation ou des modifications de la règle de notation.
>
>Les badges attribués peuvent être révoqués de la même manière que les badges attribués. Voir la section [Attribuer et révoquer des insignes](#assign-and-revoke-badges) . Les améliorations futures comprendront une interface utilisateur pour gérer les badges des membres.


### Badges personnalisés {#custom-badges}

Les badges personnalisés peuvent être installés à l&#39;aide de la console [](/help/communities/badges.md) Badges et être affectés ou spécifiés dans les règles de badge.

Une fois installés à partir de la console Badges, les badges personnalisés sont automatiquement répliqués dans l’environnement de publication.

## Activer le score {#enable-scoring}

Le score n’est pas activé par défaut. Les étapes de base pour la configuration et l&#39;activation de la notation et de l&#39;attribution des badges sont les suivantes :

* Identifiez les règles relatives aux points de rendement (règles[de](#scoring-rules)notation).
* Pour les points cumulés par règle de score, attribuez des [badges](#badges) (règles[de](#badging-rules)badge).

* [Appliquez les règles de score et de badge à un site](#apply-rules-to-content)communautaire.
* [Activez le badge pour les fonctionnalités](#enable-badges-for-component)de la communauté.

Consultez la section Test [](#quick-test) rapide pour activer la notation pour un site communautaire à l’aide des règles de notation et de badge par défaut pour les forums et les commentaires.

### Appliquer des règles au contenu {#apply-rules-to-content}

Pour activer la notation et les badges, ajoutez les propriétés `scoringRules` et `badgingRules` à n’importe quel noeud de l’arborescence de contenu du site.

Si le site est déjà publié, après avoir appliqué toutes les règles et activé les composants, republiez le site.

Les règles qui s’appliquent à un composant activé par badge sont celles du noeud actif ou de son ancêtre.

Si le noeud est de type `cq:Page` (recommandé), ajoutez les propriétés à son `jcr:content` noeud à l&#39;aide de CRXDE|Lite.

| **Propriété** | **Type** | **Description** |
|---|---|---|
| badgingRules | Chaîne[] | une liste de tableau des règles de [mise en badge](#badging-rules) |
| scoringRules | Chaîne[] | liste de tableau des règles de [notation](#scoring-rules) |

>[!NOTE]
>
>Si une règle d’évaluation ne semble pas avoir d’effet sur l’attribution des badges, assurez-vous que la règle d’évaluation n’a pas été bloquée par la propriété scoringRules de la règle d’évaluation. Consultez la section intitulée Règles [de](#badging-rules)mise en badge.


### Activer les badges pour le composant {#enable-badges-for-component}

Les règles d’évaluation et d’évaluation ne sont en vigueur que pour les instances de composants qui ont activé l’attribution de balises en modifiant la configuration du composant en mode [de](/help/communities/author-communities.md)création.

Propriété booléenne, `allowBadges`active/désactive l’affichage des badges pour une instance de composant. Il est configurable dans la boîte de dialogue [de modification des](/help/communities/author-communities.md) composants pour les composants forum, QnA et de commentaire par le biais d’une case à cocher intitulée **Afficher les badges**.

#### Exemple : allowBadges pour l’instance de composant Forum {#example-allowbadges-for-forum-component-instance}

![chlimage_1-100](assets/chlimage_1-100.png)

>[!NOTE]
>
>N’importe quel composant peut être superposé pour afficher les badges à l’aide du code HBS trouvé dans les forums, QnA et les commentaires comme exemple.


## Règles de score {#scoring-rules}

Les règles de score sont la base de la notation pour l’attribution de badges.

Très simplement, chaque règle de score est une liste d’une ou de plusieurs sous-règles. Des règles de score sont appliquées au contenu du site de la communauté afin d’identifier les règles à appliquer lorsque les badges sont activés.

Les règles de score sont héritées, mais pas additifs. Par exemple :

* Si la page2 contient la règle de score2 et son ancêtre page1 contient la règle de score1.
* Une action sur un composant page2 appelle à la fois règle1 et règle2.
* Si les deux règles contiennent des sous-règles applicables pour la même `topic/verb`:

   * Seule la sous-règle de la règle2 affectera le score.
   * Les scores des deux sous-règles ne sont pas additionnés.

Lorsqu’il existe plusieurs règles de score, les scores sont conservés séparément pour chaque règle.

Les règles de score sont des noeuds de type `cq:Page` avec des propriétés sur son `jcr:content` noeud qui spécifient la liste des sous-règles qui la définissent.

Les scores sont stockés dans SRP.

>[!NOTE]
>
>Bonne pratique : nommez de manière unique chaque règle de score.
>
>Les noms des règles de score doivent être globalement uniques ; ils ne devraient pas se terminer par le même nom.
>
>Voici un exemple de ce que *ne pas* faire :
>/libs/settings/community/scoring/rules/site1/forums-score
>/libs/settings/community/scoring/rules/site2/forums-score


### Sous-règles de score {#scoring-sub-rules}

Les sous-règles de notation contiennent les propriétés qui détaillent les valeurs de participation à la communauté.

Chaque sous-règle de notation identifie :

* Quelles activités sont suivies ?
* Quelle fonction communautaire particulière est impliquée ?
* Combien de points sont attribués ?

Par défaut, les points sont attribués au membre qui agit, sauf si la sous-règle spécifie le propriétaire du contenu comme recevant les points ( `forOwner`).

Chaque sous-règle peut être incluse dans une ou plusieurs règles de notation.

Le nom de la sous-règle suit généralement le modèle d’utilisation d’un *sujet* , d’un *objet* et d’un *verbe*. Par exemple :

* membre-commentaire-créer
* membre-réception-vote

Les sous-règles sont des noeuds de type `cq:Page` avec des propriétés sur son `jcr:content`noeud qui spécifient les [verbes et les rubriques](#topics-and-verbs) .

<table>
 <tbody>
  <tr>
   <th>Propriétés</th>
   <th>Type</th>
   <th> Description de la valeur</th>
  </tr>
  <tr>
   <td><i><code>VERB</code></i></td>
   <td>Long</td>
   <td>
    <ul>
     <li>requis ; le verbe correspond à une action de événement</li>
     <li>il doit y avoir au moins une propriété verbe</li>
     <li>le verbe doit être saisi en UPPERCASE</li>
     <li>il peut y avoir plusieurs propriétés de verbes, mais aucun duplicata</li>
     <li>la valeur est le score à appliquer pour ce événement</li>
     <li>la valeur peut être positive ou négative</li>
     <li>une liste de verbes prise en charge dans la version se trouve dans la section <a href="#topics-and-verbs">Rubriques et verbes</a> .</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>topics</code></td>
   <td>Chaîne[]</td>
   <td>
    <ul>
     <li>facultatif ; restreint la sous-règle aux composants de la communauté identifiés par des sujets de événement</li>
     <li>si spécifié : est une chaîne de plusieurs valeurs de rubriques de événement</li>
     <li>une liste de rubriques de la version se trouve dans la section <a href="#topics-and-verbs">Rubriques et verbes</a> .</li>
     <li>par défaut est appliquée à toutes les rubriques associées aux verbes.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>forOwner</code></td>
   <td>Booléen</td>
   <td>
    <ul>
     <li>facultatif ; n'est pas pertinent lorsque le membre agit sur le contenu qu'il possède</li>
     <li>si la valeur est true, appliquez un score au propriétaire du contenu concerné</li>
     <li>si la valeur est false, appliquer un score à l'action du membre</li>
     <li>false par défaut</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>scoringType</code></td>
   <td>Chaîne</td>
   <td>
    <ul>
     <li>facultatif ; identifie le moteur de notation</li>
     <li>si "de base", spécifie le moteur de notation en fonction de la quantité
      <ul>
       <li>inclus dans la version</li>
      </ul> </li>
     <li>si "avancé", indique le moteur de notation en fonction de la qualité et de la quantité
      <ul>
       <li>nécessite un package <a href="/help/communities/advanced.md">supplémentaire</a></li>
      </ul> </li>
     <li>default is "basic"</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Règles et sous-règles de score incluses {#included-scoring-rules-and-sub-rules}

Cette version comprend deux règles de notation pour la fonction [du](/help/communities/functions.md#forum-function) Forum (une pour le Forum et les composants Commentaires de la fonctiondu Forum) :

1. /libs/settings/community/score/rules/commentaires-score

   * sous-règles[] =/libs/settings/community/scoring/rules/sub-rules/membre-comment-create/libs/settings/community/scoring/rules/sub-rules/membre-receive-vote/libs/settings/community/scoring/rules/subrules/sub-rules/members-rule/members-don-vote/libs/settings/community/scoring/rules/sub-rules/members-est modéré

1. /libs/settings/community/score/rules/forums-score

   * sous-règles[] =/libs/settings/community/scoring/rules/sub-rules/membre-forum-create/libs/settings/community/scoring/rules/sub-rules/membre-receive-vote/libs/settings/community/scoring/rules/subrules/sub-rules/members-rule/members-don-vote/libs/settings/community/scoring/rules/sub-rules/members-est modéré

**Notes:**

* Les deux `rules` noeuds et `sub-rules` les noeuds sont de type cq:Page.

* `subRules` est un attribut de type String[] sur le `jcr:content` noeud de la règle.

* `sub-rules` peut être partagée entre différentes règles de notation.
* `rules` doit être situé dans un emplacement de référentiel avec une autorisation de lecture pour tout le monde.

   * Les noms de règle doivent être uniques, quel que soit l’emplacement.

### Activation de règles de score personnalisées {#activating-custom-scoring-rules}

Toute modification ou tout ajout apporté aux règles de notation ou aux sous-règles apportées dans l’environnement d’auteur doit être installé lors de la publication.

## Règles de badge {#badging-rules}

Les règles de mise en badge lient les règles de notation aux badges en spécifiant :

* Règle de score.
* Le score nécessaire pour recevoir un badge spécifique.

Les règles de mise en badge sont des noeuds de type `cq:Page` avec des propriétés sur son `jcr:content` noeud qui mettent en corrélation les règles de notation avec des scores et des badges.

Les règles de badge consistent en une `thresholds` propriété obligatoire qui est une liste ordonnée de scores mappés à des badges. Les scores doivent être triés en valeur croissante. Par exemple :

* `1|/libs/settings/community/badging/images/bronze-badge/jcr:content/bronze.png`

   * Un badge en bronze est décerné pour avoir gagné 1 point.

* `60|/libs/settings/community/badging/images/silver-badge/jcr:content/silver.png`

   * Un badge d&#39;argent est attribué lorsque 60 points ont été accumulés.

* `80|/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png`

   * Un badge d&#39;or est décerné lorsque 80 points ont été accumulés.

Les règles de badge sont associées à des règles de score, qui déterminent comment les points s’accumulent. Reportez-vous à la section intitulée [Appliquer des règles au contenu](#apply-rules-to-content).

La `scoringRules` propriété d’une règle de badge limite simplement les règles de score qui peuvent être associées à cette règle de badge particulière.

>[!NOTE]
>
>Meilleure pratique : créez des images de badge propres à chaque site AEM.


![chlimage_1-101](assets/chlimage_1-101.png)

<table>
 <tbody>
  <tr>
   <th>Propriétés</th>
   <th>Type</th>
   <th>Description de la valeur</th>
  </tr>
  <tr>
   <td>seuils</td>
   <td>Chaîne[]</td>
   <td><em>(obligatoire)</em> Chaîne à plusieurs valeurs du formulaire "numéro|chemin"
    <ul>
     <li>nombre = score</li>
     <li>| = la ligne verticale char (U+007C)</li>
     <li>chemin = chemin complet vers la ressource image de badge</li>
    </ul> Les chaînes doivent être triées afin que les nombres augmentent en valeur et qu’aucun espace blanc ne s’affiche entre le nombre et le chemin.<br /> Exemple d’entrée :<br /> <code>80|/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png</code></td>
  </tr>
  <tr>
   <td>badgingType</td>
   <td>Chaîne</td>
   <td><em>(Facultatif)</em> Identifie le moteur d’évaluation comme étant "de base" ou "avancé". Si vous souhaitez utiliser le moteur de score avancé, voir <a href="/help/communities/advanced.md">Advanced Scoring and Badges (Scores et badges</a>avancés). La valeur par défaut est "basic".</td>
  </tr>
  <tr>
   <td>scoringRules</td>
   <td>Chaîne[]</td>
   <td>(<em>facultatif</em>) Chaîne à plusieurs valeurs pour limiter la règle de badge aux événements de notation identifiés par les règles de notation</td>
  </tr>
 </tbody>
</table>

### Règles de mise en badge incluses {#included-badging-rules}

Cette version comprend deux règles de mise en badge qui correspondent aux [forums et aux règles](#includedscoringrules)de score des commentaires.

* /libs/settings/community/badging/rules/comments-badging

* /libs/settings/community/badging/rules/forums-badging

**Notes:**

* `rules` sont de type cq:Page.
* `rules` doit être situé dans un emplacement de référentiel avec une autorisation de lecture pour tout le monde.

   * Les noms de règle doivent être uniques, quel que soit l’emplacement.

### Activation de règles de badge personnalisées {#activating-custom-badging-rules}

Toute modification ou tout ajout apporté aux règles de mise en badge ou aux images effectuées dans l’environnement d’auteur doit être installé lors de la publication.

## Affectation et révocation de badges {#assign-and-revoke-badges}

Des badges peuvent être attribués à des membres à l&#39;aide de la console [](/help/communities/members.md#badges-tab) membres ou par programmation à l&#39;aide de commandes cURL.

Les commandes cURL suivantes indiquent ce qui est nécessaire pour une demande HTTP d’attribution et de révocation de badges. Le format de base est le suivant :

cURL -i -X POST -H *header* -u *signature* -F *opération* -F *badge membre-profil-url***

*header* = &quot;Accepter:application/json&quot;en-tête personnalisé à transmettre au serveur (obligatoire)

*signature* = administrator-id:password, par exemple : admin:admin

*opération* = &quot;:operation=social:assignBadge&quot; OU &quot;:operation=social:deleteBadge&quot;

*badge* = &quot;badgeContentPath=*badge-image-file*&quot;

*badge-image-file* = emplacement du fichier image de badge dans le référentiel, par exemple : /libs/settings/community/badging/images/modérator/jcr:content/moderator.png

*Member-profil-url* = point de terminaison du profil du membre sur la publication, par exemple : https://&lt;serveur>:&lt;port>/home/users/community/riley/profile.social.json

>[!NOTE]
>
>Le *membre-profil-url*:
>
>* Peut faire référence à une instance d’auteur si le service [](/help/communities/users.md#tunnel-service) tunnel est activé.
>* Il peut s’agir d’un nom obscur et aléatoire - voir Liste de contrôle [de](/help/sites-administering/security-checklist.md#verify-that-you-are-not-disclosing-personally-identifiable-information-in-the-users-home-path) sécurité concernant l’ID autorisé.

>



### Exemples: {#examples}

#### Attribuer un badge de modérateur {#assign-a-moderator-badge}

```shell
curl -i -X POST -H "Accept:application/json" -u admin:admin -F ":operation=social:assignBadge" -F "badgeContentPath=/libs/settings/community/badging/images/moderator/jcr:content/moderator.png" /home/users/community/updcs9DndLEI74DB9zsB/profile.social.json
```

#### Révoquer un badge argenté assigné {#revoke-an-assigned-silver-badge}

```shell
curl -i -X POST -H "Accept:application/json" -u admin:admin -F ":operation=social:deleteBadge" -F "badgeContentPath=/libs/settings/community/badging/images/silver/jcr:content/silver.png" /home/users/community/updcs9DndLEI74DB9zsB/profile.social.json
```

>[!NOTE]
>
>L’utilisation de cURL pour attribuer et révoquer des badges fonctionne pour n’importe quelle image de badge, mais lorsqu’elle est affectée à la place de celle acquise, elle est marquée comme des badges attribués et gérée en conséquence.

## Scores et badges pour les composants personnalisés {#scoring-and-badges-for-custom-components}

Il est possible de créer des règles de score et de badge pour les composants personnalisés en associant les rubriques de événement créées pour le composant aux verbes.

## Rubriques et verbes {#topics-and-verbs}

Lorsque les membres interagissent avec les fonctionnalités des communautés, des événements sont envoyés qui peuvent déclencher des écouteurs asynchrones, tels que des notifications et des scores.

L’instance SocialEvent d’un composant enregistre les événements comme `actions` ceux qui se produisent pour un `topic`composant. SocialEvent comprend une méthode permettant de renvoyer une `verb` variable associée à l’action. Il y a une relation *n-1* entre `actions` et `verbs`.

Pour les composants de communautés livrés, les tableaux suivants décrivent la `verbs` définition de chaque `topic` variable disponible pour l’utilisation dans les sous-règles [de](#scoring-sub-rules)notation.

>[!NOTE]
>
>Une nouvelle propriété booléenne `allowBadges`, active/désactive l’affichage des badges pour une instance de composant. Il sera configurable dans les boîtes de dialogue [de modification des](/help/communities/author-communities.md) composants mises à jour par le biais d’une case à cocher intitulée **Badges** d’affichage.


**[Composant](/help/communities/calendar.md)**Calendrier SocialEvent`topic`= com/adobe/cq/social/calendar

| **Verbe** | **Description** |
|---|---|
| POST | crée un événement de calendrier |
| AJOUTER | commentaires d&#39;un membre sur un événement de calendrier |
| UPDATE | le événement de calendrier ou le commentaire du membre est modifié |
| DELETE | le événement de calendrier ou le commentaire du membre est supprimé |

**[Composant](/help/communities/comments.md)**Commentaires SocialEvent`topic`= com/adobe/cq/social/comment

| **Verbe** | **Description** |
|---|---|
| POST | crée un commentaire |
| AJOUTER | réponse du membre au commentaire |
| UPDATE | le commentaire du membre est modifié |
| DELETE | le commentaire du membre est supprimé |

**[Composant](/help/communities/file-library.md)**de bibliothèque de fichiers SocialEvent`topic`= com/adobe/cq/social/fileLibrary

| **Verbe** | **Description** |
|---|---|
| POST | crée un dossier |
| ATTAQUE | le membre télécharge un fichier |
| UPDATE | met à jour un dossier ou un fichier |
| DELETE | supprime un dossier ou un fichier |

**[Composant](/help/communities/forum.md)**du forum SocialEvent`topic`= com/adobe/cq/social/forum

| **Verbe** | **Description** |
|---|---|
| POST | membre crée une rubrique de forum |
| AJOUTER | réponses des membres au sujet du forum |
| UPDATE | le sujet ou la réponse du forum du membre est modifié |
| DELETE | le sujet ou la réponse du membre du forum est supprimé |

**[Composant](/help/communities/blog-feature.md)**Journal SocialEvent`topic`= com/adobe/cq/social/journal

| **Verbe** | **Description** |
|---|---|
| POST | crée un article de blog |
| AJOUTER | commentaires d&#39;un membre sur un article de blog |
| UPDATE | article ou commentaire du blog du membre modifié |
| DELETE | article ou commentaire du blog du membre supprimé |

**[Composant](/help/communities/working-with-qna.md)**QnA SocialEvent`topic`= com/adobe/cq/social/qna

| **Verbe** | **Description** |
|---|---|
| POST | crée une question QnA |
| AJOUTER | crée une réponse QnA |
| UPDATE | Question ou réponse QnA du membre modifiée |
| SELECT | la réponse du membre est sélectionnée |
| DÉSÉLECTIONNER | la réponse du membre est désélectionnée |
| DELETE | QnUne question ou réponse du membre est supprimée |

**[Composant](/help/communities/reviews.md)**de révision SocialEvent`topic`= com/adobe/cq/social/review

| **Verbe** | **Description** |
|---|---|
| POST | membre crée une révision |
| UPDATE | révision du membre est modifiée |
| DELETE | la révision du membre est supprimée |

**[Composant](/help/communities/rating.md)**de notation SocialEvent`topic`= com/adobe/cq/social/tally/rating/rating

| **Verbe** | **Description** |
|---|---|
| AJOUTER LA COTATION | le contenu du membre a été amélioré |
| SUPPRESSION DE LA COTE | le contenu du membre a été réduit |

**[Composant](/help/communities/voting.md)**de vote SocialEvent`topic`= com/adobe/cq/social/tally/vote

| **Verbe** | **Description** |
|---|---|
| AJOUTER le vote | le contenu du député a été voté |
| SUPPRIMER LE VOTE | le contenu du député a été rejeté, voté |

**Composants** SocialEvent prenant en charge la modération `topic`= com/adobe/cq/social/modération

| **Verbe** | **Description** |
|---|---|
| DENY | le contenu du membre est refusé |
| INDICATEUR INAPPROPRIÉ | le contenu du membre est marqué |
| INAPPROPRIÉ | le contenu du membre n&#39;est pas marqué |
| ACCEPTER | le contenu du membre est approuvé par le modérateur |
| CLOSE | le membre ferme les commentaires aux modifications et aux réponses |
| OUVRIR | membre réouvre le commentaire |

### Événements de composants personnalisés {#custom-component-events}

Dans le cas d’un composant personnalisé, un événement SocialEvent est appelé pour enregistrer les événements du composant comme `actions` ceux qui se produisent pour un `topic`composant.

Pour prendre en charge le score, SocialEvent doit remplacer la méthode `getVerb()` afin qu’une valeur appropriée `verb` soit renvoyée pour chaque `action`événement. L&#39; `verb` action renvoyée peut être couramment utilisée (par exemple `POST`) ou spécialisée pour le composant (par exemple `ADD RATING`). Il y a une relation *n-1* entre `actions` et `verbs`.

## Résolution des incidents {#troubleshooting}

### Les badges ne s&#39;affichent pas {#badges-are-not-appearing}

Si des règles de notation et de badge ont été appliquées au contenu du site Web, mais que les badges ne sont attribués à aucune activité, assurez-vous que les badges ont été activés pour l’instance de ce composant.

Voir [Activer les badges pour le composant](#enable-badges-for-component).

### La règle de score n’a aucun effet {#scoring-rule-has-no-effect}

Si des règles de notation et de badge ont été appliquées au contenu du site Web et que des badges sont attribués pour certaines actions, mais pas pour d’autres, vérifiez que la règle de badge n’a pas limité les règles de notation auxquelles elle s’applique.

Voir la `scoringRules` propriété des règles [de](#badging-rules)badge.

### Type sensible à la casse {#case-sensitive-typo}

La plupart des propriétés et valeurs, en particulier les verbes, sont sensibles à la casse. Les verbes doivent être en MAJUSCULES lorsqu’ils sont utilisés dans une sous-règle de score.

Si la fonction ne fonctionne pas comme prévu, assurez-vous que les données ont été saisies correctement.

## Test rapide {#quick-test}

Il est possible d’essayer rapidement de marquer et de marquer des points à l’aide du site [Getting Started Tutorial](/help/communities/getting-started.md) (engager) :

* Accédez à CRXDE Lite sur author.
* Accédez à la page de base :

   * /content/sites/learn/fr/jcr:content

* Ajoutez la propriété badgingRules :

   * **Nom**: `badgingRules`
   * **Type**: `String`
   * Sélectionner **plusieurs**
   * Sélectionner le **Ajoute**
   * Enter `/libs/settings/community/badging/rules/forums-badging`
   * Sélectionner **+**
   * Enter `/libs/settings/community/badging/rules/comments-badging`
   * **Cliquez sur OK**

* Ajoutez la propriété scoringRules :

   * **Nom**: `scoringRules`
   * **Type**: `String`
   * Sélectionner **plusieurs**
   * Sélectionner le **Ajoute**
   * Enter `/libs/settings/community/scoring/rules/forums-scoring`
   * Sélectionner **+**
   * Enter `/libs/settings/community/scoring/rules/comments-scoring`
   * **Cliquez sur OK**

* Select **Save All**.

![chlimage_1-102](assets/chlimage_1-102.png)

Ensuite, assurez-vous que les composants du forum et des commentaires permettent l&#39;affichage des badges :

* Encore une fois en utilisant CRXDE Lite.
* Accédez au composant de forum

   * `/content/sites/engage/en/forum/jcr:content/content/primary/forum`

* Ajoutez la propriété booléenne allowBadges, si nécessaire, et assurez-vous qu’elle est vraie.

   * **Nom**: `allowBadges`
   * **Type**: `Boolean`
   * **Valeur**: `true`

![chlimage_1-103](assets/chlimage_1-103.png)

Ensuite, [republiez](/help/communities/sites-console.md#publishing-the-site) le site de la communauté.

Enfin,

* Accédez au composant sur l’instance de publication.
* Connectez-vous en tant que membre de la communauté (par exemple : weston.mccall@dodgit.com / mot de passe).
* Publiez un nouveau sujet de forum.
* La page doit être actualisée pour que le badge s’affiche.

   * Déconnexion et connexion en tant que membre de la communauté différent (par exemple : aaron.mcdonald@mailinator.com/mot de passe).

* Sélectionnez le forum.

Cela devrait permettre au membre de la communauté d&#39;obtenir un badge en bronze visible avec son billet sur le forum car le premier seuil de la règle de badge de forums est un score de 1.

![bronzebadge](assets/bronzebadge.png)

## Informations supplémentaires {#additional-information}

More information may be found on the [Scoring and Badges Essentials](/help/communities/configure-scoring.md) page for developers.

Pour plus d’informations sur le moteur de score avancé, voir [Advanced Scoring and Badges](/help/communities/advanced.md).

Le [composant](/help/communities/enabling-leaderboard.md) et la [fonction](/help/communities/functions.md#leaderboard-function) configurable du Tableau de bord simplifie l&#39;affichage des membres et leurs scores sur un site communautaire.
