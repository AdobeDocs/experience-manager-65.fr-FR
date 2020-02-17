---
title: Score et badges des communautés
seo-title: Score et badges des communautés
description: Les scores et les badges des communautés AEM vous permettent d’identifier et de récompenser les membres de la communauté
seo-description: Les scores et les badges des communautés AEM vous permettent d’identifier et de récompenser les membres de la communauté
uuid: d73683df-a413-4b3c-869c-67568bfdfcf6
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ea033bb9-cb92-4c93-855f-8c902999378c
docset: aem65
tagskeywords: scoring, badging, badges, gamification
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Score et badges des communautés{#communities-scoring-and-badges}

## Présentation {#overview}

La fonction de notation et de badges des communautés AEM permet d’identifier et de récompenser les membres de la communauté.

Les principaux aspects de la notation et des badges sont les suivants :

* [attribuer des badges](#assign-and-revoke-badges) pour déterminer le rôle d&#39;un membre dans la collectivité

* [attribution de base de badges](#enable-scoring) aux membres pour encourager leur participation (quantité de contenu créé)
* [attribution avancée de badges](/help/communities/advanced.md) pour identifier les membres comme experts (qualité du contenu créé)

**Notez** que l’attribution de badges [n’est pas activée par défaut](/help/communities/implementing-scoring.md#main-pars-text-237875536).

>[!CAUTION]
>
>La structure d’implémentation visible dans CRXDE Lite peut être modifiée une fois que l’interface utilisateur est disponible.

## Badges {#badges}

Les insignes sont placés sous le nom d&#39;un membre pour indiquer soit son rôle, soit son statut dans la communauté. Les badges peuvent être affichés sous forme d’image ou de nom. Lorsqu’il est affiché sous forme d’image, le nom est inclus comme texte de remplacement pour l’accessibilité.

Par défaut, les badges se trouvent dans le référentiel à l’adresse

* /etc/community/badging/images

S’ils sont stockés à un autre emplacement, ils doivent être lus accessibles à tous.

Les insignes sont différenciés en UGC quant à savoir s&#39;ils ont été attribués ou s&#39;ils ont été acquis conformément aux règles. Actuellement, les badges attribués apparaissent sous forme de texte et les badges gagnés sous forme d’image.

### Interface utilisateur de gestion des badges {#badge-management-ui}

La console [Badges communautaires](/help/communities/badges.md) permet d&#39;ajouter des badges personnalisés qui peuvent être affichés pour un membre lorsqu&#39;il est gagné (attribué) ou lorsqu&#39;il assume un rôle spécifique dans la communauté (attribué).

### Badges attribués {#assigned-badges}

Un administrateur attribue aux membres de la collectivité des badges fondés sur le rôle en fonction de leur rôle dans la collectivité.

Les badges attribués (et attribués) sont stockés dans le [SRP](/help/communities/srp.md) sélectionné et ne sont pas directement accessibles. Jusqu’à ce qu’une interface utilisateur graphique soit disponible, le seul moyen d’attribuer des badges basés sur les rôles consiste à utiliser du code ou cURL. Pour obtenir des instructions sur l’URL, voir la section intitulée [Attribuer et révoquer des badges](#assign-and-revoke-badges).

Cette version comprend trois badges basés sur les rôles :

* modérateur
   `/etc/community/badging/images/moderator/jcr:content/moderator.png`

* gestionnaire de groupe
   `/etc/community/badging/images/group-manager/jcr:content/group-manager.png`

* membre privilégié
   `/etc/community/badging/images/privileged-member/jcr:content/privileged-member.png`

![chlimage_1-98](assets/chlimage_1-98.png)

### Badges décernés {#awarded-badges}

Le service de notation décerne aux membres de la collectivité des badges de récompense en fonction des règles appliquées à leur activité dans la collectivité.

Pour que les badges apparaissent comme une récompense pour l&#39;activité, deux choses doivent se produire :

* le badge doit être [activé](#enableforcomponent) pour le composant de fonction
* les règles de notation et de mise en badge doivent être [appliquées](#applytopage) à la page (ou ancêtre) sur laquelle le composant est placé.

La version comprend trois badges basés sur la récompense :

* or
   `/etc/community/badging/images/gold-badge/jcr:content/gold.png`

* argent
   `/etc/community/badging/images/silver-badge/jcr:content/silver.png`

* bronze
   `/etc/community/badging/images/bronze-badge/jcr:content/bronze.png`

![chlimage_1-99](assets/chlimage_1-99.png)

>[!NOTE]
>
>Les règles de score peuvent être configurées pour affecter des points négatifs aux publications marquées comme inappropriées et affecter ainsi la valeur de score. Cependant, une fois qu’un badge est gagné, il n’est pas automatiquement supprimé en raison de la réduction du point de notation ou des modifications apportées aux règles de notation.
>
>Les badges attribués peuvent être révoqués de la même manière que les badges attribués. Voir la section [Attribuer et révoquer des badges](#assign-and-revoke-badges) . Les améliorations futures comprendront une interface utilisateur pour gérer les badges des membres.

### Badges personnalisés {#custom-badges}

Les badges personnalisés peuvent être installés à l’aide de la console [](/help/communities/badges.md) Badges et être affectés ou spécifiés dans les règles de badge.

Une fois installés à partir de la console Badges, les badges personnalisés sont automatiquement répliqués dans l’environnement de publication.

## Activer le score {#enable-scoring}

Le score n’est pas activé par défaut. Les étapes de base de la configuration et de l’activation de la notation et de l’attribution des badges sont les suivantes :

* identifier les règles pour les points de rémunération (règles[de](#scoring-rules)notation) ;
* pour les points cumulés par règle de notation, attribuez des [badges](#badges) (règles[de](#badging-rules)badge)

* [appliquer les règles de notation et de badge à un site communautaire](#apply-rules-to-content)
* [activer les badges pour les fonctionnalités de la communauté](#enable-badges-for-component)

Consultez la section Test [rapide](#quick-test) pour activer la notation pour un site communautaire à l’aide des règles de notation et de badge par défaut pour les forums et les commentaires.

### Appliquer des règles au contenu {#apply-rules-to-content}

Pour activer les scores et les badges, ajoutez les propriétés `scoringRules` et `badgingRules`à n’importe quel noeud de l’arborescence de contenu du site.

Si le site est déjà publié, après avoir appliqué toutes les règles et activé les composants, republiez le site.

Les règles qui s’appliquent à un composant activé par badge sont celles du noeud actif ou de son ancêtre.

Si le noeud est de type `cq:Page` (recommandé), ajoutez les propriétés à son `jcr:content`noeud à l’aide de CRXDE|Lite.

| **Propriété** | **Type** | **Description** |
|---|---|---|
| badgingRules | Chaîne[] | une liste de règles de [mise en badge](#badging-rules) |
| scoringRules | Chaîne[] | une liste de tableaux de règles de [notation](#scoring-rules) |

>[!NOTE]
>
>Si une règle d’évaluation ne semble pas avoir d’effet sur l’attribution des badges, assurez-vous que la règle d’évaluation n’a pas été bloquée par la propriété scoringRules de la règle d’évaluation. Voir la section intitulée Règles [de](#badging-rules)badge.

### Activer les badges pour le composant {#enable-badges-for-component}

Les règles de notation et de bourrage sont en vigueur uniquement pour les instances de composants qui ont activé le badge en modifiant la configuration du composant en mode [de](/help/communities/author-communities.md)création.

Propriété booléenne `allowBadges`, active/désactive l’affichage des badges pour une instance de composant. Il est configurable dans la boîte de dialogue [d’édition des](/help/communities/author-communities.md) composants pour les composants forum, QnA et de commentaire via une case à cocher intitulée **Afficher les badges**.

#### Exemple : allowBadges pour l’instance de composant Forum {#example-allowbadges-for-forum-component-instance}

![chlimage_1-100](assets/chlimage_1-100.png)

>[!NOTE]
>
>N’importe quel composant peut être superposé pour afficher les badges à l’aide du code HBS trouvé dans les forums, QnA et les commentaires comme exemple.

## Règles de score {#scoring-rules}

Les règles de notation sont la base de la notation pour l’attribution des badges.

Très simplement, chaque règle de score est une liste d’une ou de plusieurs sous-règles. Des règles de score sont appliquées au contenu du site de la communauté pour identifier les règles à appliquer lorsque les badges sont activés.

Les règles de score sont héritées mais pas additifs. Par exemple :

* si la page2 contient la règle de score2 et sa page1 ancêtre contient la règle de score1
* une action sur un composant page2 appelle à la fois règle1 et règle2.
* si les deux règles contiennent des sous-règles applicables pour la même `topic/verb` :

   * seule la sous-règle de la règle2 affectera le score
   * les scores des deux sous-règles ne sont pas additionnés

S’il existe plusieurs règles de notation, les scores sont conservés séparément pour chaque règle.

Les règles de score sont des noeuds de type `cq:Page` avec des propriétés sur son `jcr:content`noeud qui spécifient la liste des sous-règles qui le définissent.

Les scores sont stockés dans SRP.

>[!NOTE]
>
>Meilleure pratique : attribuez un nom unique à chaque règle de score.
>
>Les noms des règles de score doivent être uniques au niveau mondial ; ils ne doivent pas se terminer par le même nom.
>
>Un exemple de ce que *ne pas *faire :
>/etc/community/score/rule/site1/forums-score
>/etc/community/score/rule/site2/forums-score

### Sous-règles de score {#scoring-sub-rules}

Les sous-règles de notation contiennent les propriétés qui détaillent les valeurs de participation à la communauté.

Chaque sous-règle de notation identifie

* quelles activités sont suivies ?
* quelle fonction communautaire spécifique implique
* nombre de points attribués

Par défaut, les points sont attribués au membre qui agit, sauf si la sous-règle spécifie le propriétaire du contenu comme recevant les points ( `forOwner`).

Chaque sous-règle peut être incluse dans une ou plusieurs règles de notation.

Le nom de la sous-règle suit généralement le modèle d’utilisation d’un objet *objet, d’un objet *et d’un *verbe.* Par exemple :

* members-comment-create
* membre-bénéficiaire-vote

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
     <li>requis; le verbe correspond à une action d’événement.</li>
     <li>il doit y avoir au moins une propriété verb</li>
     <li>le verbe doit être saisi en MAJUSCULE</li>
     <li>il peut exister plusieurs propriétés de verbe, mais pas de doublons</li>
     <li>la valeur est le score à appliquer pour cet événement</li>
     <li>la valeur peut être positive ou négative</li>
     <li>la liste des verbes pris en charge dans cette version figure dans la section <a href="#topics-and-verbs">Rubriques et verbes</a> .</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>topics</code></td>
   <td>Chaîne[]</td>
   <td>
    <ul>
     <li>facultatif; limite la sous-règle aux composants de la communauté identifiés par les rubriques d’événement.</li>
     <li>if specified : est une chaîne de plusieurs valeurs des rubriques d’événement</li>
     <li>la liste des rubriques de la version se trouve dans la section <a href="#topics-and-verbs">Rubriques et versions</a> .</li>
     <li>s’applique par défaut à toutes les rubriques associées aux verbes.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>forOwner</code></td>
   <td>Booléen  </td>
   <td>
    <ul>
     <li>facultatif; n'est pas pertinent lorsque le membre agit sur le contenu qu'il possède</li>
     <li>si la valeur est true, appliquez un score au propriétaire du contenu concerné</li>
     <li>si la valeur est false, appliquez un score à l’action du membre</li>
     <li>default est false</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>scoringType</code></td>
   <td>Chaîne</td>
   <td>
    <ul>
     <li>facultatif; identifie le moteur de notation</li>
     <li>si "de base", indique le moteur de notation en fonction de la quantité
      <ul>
       <li>inclus dans la version</li>
      </ul> </li>
     <li>si "advanced", indique le moteur de notation en fonction de la qualité et de la quantité
      <ul>
       <li>nécessite un package <a href="/help/communities/advanced.md">supplémentaire</a></li>
      </ul> </li>
     <li>default is "basic"</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Règles et sous-règles de score incluses {#included-scoring-rules-and-sub-rules}

Cette version comprend deux règles de notation pour la fonction [du](/help/communities/functions.md#forum-function) forum (une pour chacune des composantes du forum et des commentaires) :

1. /etc/community/score/rule/commentaires-score

   * sous-règles[] =/etc/communauté/score/règles/sous-règles/membre-commentaire-créer/etc/communauté/score/règles/sous-règles/membre-reçu-vote/etc/communauté/notation/règles/sous-règles/membre-donné-vote/etc/communauté/notation/règles/sous-règles/membre-est-modéré

1. /etc/community/score/rule/forums-score

   * sous-règles[] =/etc/communauté/notation/règles/sous-règles/forum-membre-créer/etc/communauté/notation/règles/sous-règles/membre-reçu-vote/etc/communauté/notation/règles/sous-règles/membre-donné-vote/etc/communauté/notation/règles/sous-règles/membre-est-modéré

**Remarque:**

* les deux `rules`et `sub-rules` noeuds sont de type cq:Page

* `subRules`est un attribut de type String[] sur le `jcr:content` noeud de la règle

* `sub-rules` peut être partagée entre différentes règles de notation
* `rules`doit être situé dans un emplacement de référentiel avec une autorisation de lecture pour tout le monde

   * les noms de règle doivent être uniques, quel que soit l’emplacement

### Activation de règles de score personnalisées {#activating-custom-scoring-rules}

Toute modification ou tout ajout apporté aux règles de notation ou aux sous-règles apportées dans l’environnement de création doit être installé lors de la publication.

## Règles de badge {#badging-rules}

Les règles de badge lient les règles de notation aux badges en spécifiant :

* règle de notation
* le score nécessaire pour obtenir un badge spécifique

Les règles de badge sont des noeuds de type `cq:Page` avec des propriétés sur son `jcr:content`noeud qui corrélent les règles de notation aux scores et aux badges.

Les règles de badge se composent d’une `thresholds`propriété obligatoire qui est une liste ordonnée de scores mappés sur des badges. Les scores doivent être classés en valeur croissante. Par exemple :

* `1|/etc/community/badging/images/bronze-badge/jcr:content/bronze.png`

   * un badge en bronze est décerné pour avoir obtenu 1 point

* `60|/etc/community/badging/images/silver-badge/jcr:content/silver.png`

   * un badge d&#39;argent est attribué lorsque 60 points ont été accumulés

* `80|/etc/community/badging/images/gold-badge/jcr:content/gold.png`

   * un badge d&#39;or est décerné lorsque 80 points ont été accumulés

Les règles de badge sont associées aux règles de notation, qui déterminent le mode d’accumulation des points. Voir la section intitulée [Appliquer des règles au contenu](#apply-rules-to-content).

La `scoringRules`propriété d’une règle de badge limite simplement les règles de notation qui peuvent être associées à cette règle de badge particulière.

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
   <td><em>(obligatoire)</em> Chaîne à plusieurs valeurs du formulaire "number|path"
    <ul>
     <li>nombre = score</li>
     <li>| = le caractère de ligne verticale (U+007C)</li>
     <li>chemin = chemin complet vers la ressource image de badge</li>
    </ul> Les chaînes doivent être triées afin que les nombres augmentent en valeur et qu’aucun espace blanc ne s’affiche entre le nombre et le chemin.<br /><br /> Exemple d’entrée : <code>80|/etc/community/badging/images/gold-badge/jcr:content/gold.png</code></td>
  </tr>
  <tr>
   <td>badgingType</td>
   <td>Chaîne</td>
   <td><em>(Facultatif)</em> Identifie le moteur de notation comme étant "de base" ou "avancé". Si vous souhaitez utiliser le moteur de notation avancé, voir <a href="/help/communities/advanced.md">Scores et badges</a>avancés. La valeur par défaut est "basic".</td>
  </tr>
  <tr>
   <td>scoringRules</td>
   <td>Chaîne[]</td>
   <td>(<em>facultatif</em>) Chaîne à plusieurs valeurs qui limite la règle de badge aux événements de notation identifiés par les règles de notation</td>
  </tr>
 </tbody>
</table>

### Règles de badge incluses {#included-badging-rules}

Cette version comprend deux règles de mise en badge qui correspondent aux règles [de notation des commentaires et des](#includedscoringrules)forums.

* /etc/community/badging/Rules/Comments-badging
* /etc/community/badging/Rules/forums-badging

**Remarque:**

* `rules` les noeuds sont de type cq:Page
* `rules`doit être situé dans un emplacement de référentiel avec une autorisation de lecture pour tout le monde

   * les noms de règle doivent être uniques, quel que soit l’emplacement

### Activation de règles de badge personnalisées {#activating-custom-badging-rules}

Toute modification ou tout ajout apporté aux règles de mise en badge ou aux images effectuées dans l’environnement de création doit être installé lors de la publication.

## Affectation et révocation de badges {#assign-and-revoke-badges}

Des badges peuvent être attribués aux membres à l’aide de la console [](/help/communities/members.md#badges-tab) membres ou par programmation à l’aide des commandes cURL.

Les commandes cURL suivantes indiquent ce qui est nécessaire pour une demande HTTP d’attribution et de révocation de badges. Le format de base est :

cURL -i -X POST -H *header* -u *signature * -F *opération * -F *badge * *membre-profil-url*

*header* = &quot;Accepter:application/json&quot;en-tête personnalisé à transmettre au serveur (obligatoire)

*signature* = administrator-id:mot de passe, par exemple : admin:admin

*operation* = &quot;:operation=social:assignBadge&quot; OR &quot;:operation=social:deleteBadge&quot;

*badge* = &quot;badgeContentPath=*badge-image-file*&quot;

*badge-image-file* = emplacement du fichier image de badge dans le référentiel, par exemple : content/moderator.png

*members-profile-url* = point de terminaison du profil du membre sur la publication, par exemple : https://&lt;serveur>:&lt;port>/home/users/community/riley/profile.social.json

>[!NOTE]
>
>Le *membre-profil-url*
>
>* peut faire référence à une instance d’auteur si le service [](/help/communities/users.md#tunnel-service) tunnel est activé
>* peut être un nom aléatoire et obscur - voir Liste de contrôle [de](/help/sites-administering/security-checklist.md#verify-that-you-are-not-disclosing-personally-identifiable-information-in-the-users-home-path) sécurité concernant l&#39;ID autorisé
>



### Exemples: {#examples}

#### Attribuer un badge de modérateur {#assign-a-moderator-badge}

```shell
curl -i -X POST -H "Accept:application/json" -u admin:admin -F ":operation=social:assignBadge" -F "badgeContentPath=/etc/community/badging/images/moderator/jcr:content/moderator.png" /home/users/community/updcs9DndLEI74DB9zsB/profile.social.json
```

#### Révocation d’un badge d’argent attribué {#revoke-an-assigned-silver-badge}

```shell
curl -i -X POST -H "Accept:application/json" -u admin:admin -F ":operation=social:deleteBadge" -F "badgeContentPath=/etc/community/badging/images/silver/jcr:content/silver.png" /home/users/community/updcs9DndLEI74DB9zsB/profile.social.json
```

>[!NOTE]
>
>L’utilisation de cURL pour attribuer et révoquer des badges fonctionne pour n’importe quelle image de badge, mais lorsqu’elle est attribuée à la place d’un badge gagné, elle est marquée comme un badge attribué et gérée en conséquence.

## Scores et badges pour les composants personnalisés {#scoring-and-badges-for-custom-components}

Il est possible de créer des règles de score et de badge pour les composants personnalisés en associant les rubriques d’événement créées pour le composant aux verbes.

## Rubriques et verbes {#topics-and-verbs}

Lorsque les membres interagissent avec les fonctionnalités des communautés, des événements sont envoyés, qui peuvent déclencher des écouteurs asynchrones, tels que des notifications et des scores.

L’instance SocialEvent d’un composant enregistre les événements comme `actions`cela se produit pour un `topic`composant. SocialEvent inclut une méthode pour renvoyer une `verb`associée à l’action. Il existe une relation *n-1* entre `actions`et `verbs`.

Pour les composants de communautés livrés, les tableaux suivants décrivent les `verbs`paramètres définis pour chaque `topic`disponible à utiliser dans les sous-règles [de](#scoring-sub-rules)notation.

>[!NOTE]
>
>Une nouvelle propriété booléenne `allowBadges`, active/désactive l’affichage des badges pour une instance de composant. Il sera configurable dans les boîtes de dialogue [de modification des](/help/communities/author-communities.md) composants mises à jour par le biais d’une case à cocher intitulée **Badges** d’affichage.

**[Composant](/help/communities/calendar.md)**Calendrier SocialEvent`topic`= com/adobe/cq/social/calendar

| **Verbe** | **Description** |
|---|---|
| POST | crée un événement de calendrier |
| AJOUTER | commentaires de membre sur un événement de calendrier |
| UPDATE | l’événement de calendrier ou le commentaire du membre est modifié. |
| DELETE | l’événement de calendrier ou le commentaire du membre est supprimé |

**[Composant](/help/communities/comments.md)**de commentaires SocialEvent`topic`= com/adobe/cq/social/comment

| **Verbe** | **Description** |
|---|---|
| POST | crée un commentaire |
| AJOUTER | les réponses du membre au commentaire |
| UPDATE | le commentaire du membre est modifié. |
| DELETE | commentaire du membre supprimé |

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
| UPDATE | Le sujet ou la réponse du membre du forum est modifié |
| DELETE | Le sujet ou la réponse du membre du forum est supprimé |

**[Composant](/help/communities/blog-feature.md)**du journal SocialEvent`topic`= com/adobe/cq/social/journal

| **Verbe** | **Description** |
|---|---|
| POST | crée un article de blog |
| AJOUTER | commentaires d&#39;un membre sur un article de blog |
| UPDATE | l’article ou le commentaire du blog du membre est modifié. |
| DELETE | article ou commentaire de blog du membre supprimé |

**[Composant](/help/communities/working-with-qna.md)**QA SocialEvent`topic`= com/adobe/cq/social/qna

| **Verbe** | **Description** |
|---|---|
| POST | crée une question QnA |
| AJOUTER | crée une réponse QnA |
| UPDATE | QnUne question ou une réponse du membre est modifiée |
| SELECT | la réponse du membre est sélectionnée |
| DÉSÉLECTIONNER | la réponse du membre est désélectionnée |
| DELETE | qualité du membre Une question ou une réponse est supprimée |

**[Composant](/help/communities/reviews.md)**Révisions SocialEvent`topic`= com/adobe/cq/social/review

| **Verbe** | **Description** |
|---|---|
| POST | membre crée une révision |
| UPDATE | révision du membre est modifiée |
| DELETE | la révision du membre est supprimée |

**[Composant](/help/communities/rating.md)**de notation SocialEvent`topic`= com/adobe/cq/social/tally/rating

| **Verbe** | **Description** |
|---|---|
| AJOUTER UNE COTATION | le contenu du membre a été amélioré |
| SUPPRIMER LA COTE | le contenu du membre a été mal évalué |

**[Composant](/help/communities/voting.md)**de vote SocialEvent`topic`= com/adobe/cq/social/tally/vote

| **Verbe** | **Description** |
|---|---|
| AJOUTER UN VOTE | le contenu du membre a été voté |
| SUPPRIMER LE VOTE | le contenu du membre a été rejeté |

**Composants** SocialEvent prenant en charge la modération `topic`= com/adobe/cq/social/modération

| **Verbe** | **Description** |
|---|---|
| DENY | contenu du membre refusé |
| INDICATEUR COMME INAPPROPRIÉ | le contenu du membre est marqué |
| INAPPROPRIÉ | le contenu du membre n’est pas marqué |
| ACCEPTER | le contenu du membre est approuvé par le modérateur |
| CLOSE | le membre ferme les commentaires aux modifications et aux réponses |
| OUVRIR | membre réouvre le commentaire |

### Evénements de composant personnalisés {#custom-component-events}

Dans le cas d’un composant personnalisé, un événement SocialEvent est appelé pour enregistrer les événements du composant comme `actions`cela se produit pour un `topic`composant.

Pour prendre en charge la notation, SocialEvent doit remplacer la méthode `getVerb()` afin qu’un paramètre approprié `verb`soit renvoyé pour chaque `action`événement. Le `verb` retour d’une action peut être un élément couramment utilisé ( `POST`) ou spécialisé pour le composant ( `ADD RATING`). Il existe une relation *n-1* entre `actions`et `verbs`.

## Résolution des incidents {#troubleshooting}

### Les badges ne s’affichent pas {#badges-are-not-appearing}

Si des règles de notation et de badge ont été appliquées au contenu du site Web, mais que les badges ne sont attribués à aucune activité, assurez-vous que les badges ont été activés pour l’instance de ce composant.

Voir [Activation des badges pour le composant](#enable-badges-for-component).

### Règle de score sans effet {#scoring-rule-has-no-effect}

Si des règles de notation et de badge ont été appliquées au contenu du site Web et que des badges sont attribués pour certaines actions, mais pas pour d’autres, vérifiez que la règle de badge n’a pas limité les règles de notation auxquelles elle s’applique.

Voir la `scoringRules`propriété des règles [de](#badging-rules)badge.

### Type sensible à la casse {#case-sensitive-typo}

La plupart des propriétés et des valeurs, en particulier les verbes, sont sensibles à la casse. Les verbes doivent être tous en MAJUSCULE lorsqu’ils sont utilisés dans une sous-règle de score.

Si la fonction ne fonctionne pas comme prévu, assurez-vous que les données ont été saisies correctement.

## Test rapide {#quick-test}

Il est possible de tester rapidement le score et le badge à l’aide du site [Getting Started Tutorial](/help/communities/getting-started.md) (engager) :

* accès à CRXDE Lite sur l’auteur
* accédez à la page de base :

   * /content/sites/interaction/fr/jcr:content

* ajoutez la propriété badgingRules :

   * **Nom**: `badgingRules`
   * **Type**: `String`
   * sélectionner **Multi**
   * sélectionner **Ajouter**
   * enter `/etc/community/badging/rules/forums-badging`
   * select **+**
   * enter `/etc/community/badging/rules/comments-badging`
   * sélectionnez **OK**

* ajoutez la propriété scoringRules :

   * **Nom**: `scoringRules`
   * **Type**: `String`
   * sélectionner **Multi**
   * sélectionner **Ajouter**
   * enter `/etc/community/scoring/rules/forums-scoring`
   * select **+**
   * enter `/etc/community/scoring/rules/comments-scoring`
   * sélectionnez **OK**

* sélectionnez **Enregistrer tout**

![chlimage_1-102](assets/chlimage_1-102.png)

Ensuite, assurez-vous que les composants du forum et des commentaires permettent l’affichage des badges :

* utilisation de CRXDE Lite
* accéder au composant de forum

   * `/content/sites/engage/en/forum/jcr:content/content/primary/forum`

* ajoutez la propriété booléenne allowBadges, si nécessaire, et assurez-vous qu’elle est définie sur true.

   * **Nom**: `allowBadges`
   * **Type**: `Boolean`
   * **Valeur**: `true`

![chlimage_1-103](assets/chlimage_1-103.png)

Ensuite, [republiez](/help/communities/sites-console.md#publishing-the-site) le site de la communauté.

Enfin,

* accéder au composant sur l’instance de publication
* se connecter en tant que membre de la communauté (par exemple : weston.mccall@dodgit.com / password)
* publier un nouveau sujet de forum
* la page doit être actualisée pour que le badge affiche

   * déconnexion et connexion en tant que membre de la communauté différent (par exemple : aaron.mcdonald@mailinator.com/password)

* sélectionner le Forum

Cela devrait permettre au membre de la communauté de recevoir un badge en bronze visible avec son billet sur le forum, car le premier seuil de la règle de badge sur les forums est un score de 1.

![bronzebadge](assets/bronzebadge.png)

## Informations supplémentaires {#additional-information}

More information may be found on the [Scoring and Badges Essentials](/help/communities/configure-scoring.md) page for developers.

Pour plus d’informations sur le moteur de notation avancé, voir [Advanced Scoring and Badges](/help/communities/advanced.md)(Note et badges avancés).

Le [composant](/help/communities/enabling-leaderboard.md) et la [fonction](/help/communities/functions.md#leaderboard-function) configurable du Tableau de bord simplifie l’affichage des membres et de leurs scores sur un site communautaire.
