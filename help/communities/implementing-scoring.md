---
title: Notation et badges des communautés
description: Les badges et scores AEM Communities vous permettent d’identifier et de récompenser les membres de la communauté.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
tagskeywords: scoring, badging, badges, gamification
role: Admin
exl-id: 4aa857f7-d111-4548-8f03-f6d6c27acf51
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '2856'
ht-degree: 3%

---

# Notation et badges des communautés {#communities-scoring-and-badges}

## Vue d’ensemble {#overview}

La fonction Scores et badges d’AEM Communities permet d’identifier et de récompenser les membres de la communauté.

Les principaux aspects de la notation et des badges sont les suivants :

* [Attribution de badges](#assign-and-revoke-badges) pour identifier le rôle d’un membre dans la communauté.

* [Délivrabilité de base des badges](#enable-scoring) aux membres pour encourager leur participation (quantité de contenu créé).

* [Attribution avancée de badges](/help/communities/advanced.md) identifier les membres comme experts (qualité du contenu créé).

**Remarque** que l&#39;attribution des badges est [non activé par défaut](/help/communities/implementing-scoring.md#main-pars-text-237875536).

>[!CAUTION]
>
>La structure d’implémentation visible dans CRXDE Lite peut être modifiée une fois l’interface utilisateur disponible.

## Badges {#badges}

Les badges sont placés sous le nom d’un membre pour indiquer son rôle ou sa position dans la communauté. Les badges peuvent être affichés sous la forme d’une image ou d’un nom. Lorsqu’il est affiché sous forme d’image, le nom est inclus en tant que texte de remplacement pour l’accessibilité.

Par défaut, les badges se trouvent dans le référentiel à l’emplacement suivant :

* `/libs/settings/community/badging/images`

S’ils sont stockés à un autre emplacement, ils doivent être lus et accessibles à tous.

Les badges sont différenciés par contenu généré par l’utilisateur, qu’ils aient été attribués ou qu’ils aient été gagnés selon les règles. Actuellement, les badges attribués apparaissent sous forme de texte et les badges gagnés apparaissent sous forme d’image.

### Interface utilisateur de gestion des badges {#badge-management-ui}

Les communautés [Console Badges](/help/communities/badges.md) vous permet d’ajouter des badges personnalisés qui peuvent être affichés pour un membre lorsqu’il est gagné (attribué) ou lorsqu’il occupe un rôle spécifique dans la communauté (affecté).

### Badges attribués {#assigned-badges}

Les badges en fonction du rôle sont attribués par un administrateur aux membres de la communauté en fonction de leur rôle dans la communauté.

Les badges attribués (et attribués) sont stockés dans le [SRP](/help/communities/srp.md) et ne sont pas directement accessibles. Tant qu’une interface utilisateur graphique n’est pas disponible, le seul moyen d’affecter des badges basés sur un rôle consiste à utiliser du code ou cURL. Pour obtenir des instructions sur cURL, consultez la section intitulée [Attribution et révocation des badges](#assign-and-revoke-badges).

Cette version comprend trois badges basés sur les rôles :

* **modérateur**
  `/libs/settings/community/badging/images/moderator/jcr:content/moderator.png`

* **gestionnaire de groupe**
  `/libs/settings/community/badging/images/group-manager/jcr:content/group-manager.png`

* **membre privilégié**
  `/libs/settings/community/badging/images/privileged-member/jcr:content/privileged-member.png`

  ![assigned-badges](assets/assigned-badges.png)

### Badges décernés {#awarded-badges}

Les badges récompensés sont attribués par le service de notation aux membres de la communauté selon les règles appliquées à leur activité dans la communauté.

Pour que les badges apparaissent comme une récompense pour l’activité, deux choses doivent se produire :

* Le badge doit être [enabled](#enableforcomponent) pour le composant de fonctionnalité.
* Les règles de notation et de badge doivent être [appliqué](#applytopage) sur la page (ou l’ancêtre) sur laquelle le composant est placé.

Trois badges basés sur les récompenses sont inclus dans la version :

* **or**
  `/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png`

* **argent**
  `/libs/settings/community/badging/images/silver-badge/jcr:content/silver.png`

* **bronze**
  `/libs/settings/community/badging/images/bronze-badge/jcr:content/bronze.png`

  ![badges primés](assets/awarded-badges.png)

>[!NOTE]
>
>Les règles de notation peuvent être configurées pour affecter des points négatifs aux publications marquées comme inappropriées et affecter ainsi la valeur du score. Cependant, une fois qu’un badge est gagné, il n’est pas automatiquement supprimé en raison de la réduction du point de notation ou des modifications des règles de notation.
>
>Les badges primés peuvent être révoqués de la même manière que les badges attribués. Voir [Attribution et révocation des badges](#assign-and-revoke-badges) . À l’avenir, une interface utilisateur sera ajoutée pour gérer les badges des membres.

### Badges personnalisés {#custom-badges}

Les badges personnalisés peuvent être installés à l’aide de la fonction [Console Badges](/help/communities/badges.md) et affectés ou spécifiés dans les règles de badge.

Une fois installés à partir de la console Badges, les badges personnalisés sont automatiquement répliqués vers l’environnement de publication.

## Activation de la notation {#enable-scoring}

La notation n’est pas activée par défaut. Les étapes de base pour configurer et activer la notation et l’attribution de badges sont les suivantes :

* Identifier les règles pour les points d’entrée ([règles de notation](#scoring-rules)).
* Pour les points cumulés par règle de notation, affectez [badges](#badges) ([règles de badge](#badging-rules)).

* [Application des règles de notation et de badge à un site communautaire](#apply-rules-to-content).
* [Activation des badges pour les fonctionnalités de la communauté](#enable-badges-for-component).

Voir [Test rapide](#quick-test) pour activer la notation d’un site de la communauté à l’aide des règles de notation et de badge par défaut pour les forums et les commentaires.

### Application de règles au contenu {#apply-rules-to-content}

Pour activer la notation et les badges, ajoutez les propriétés `scoringRules` et `badgingRules` à n’importe quel noeud de l’arborescence de contenu du site.

Si le site est déjà publié, après avoir appliqué toutes les règles et activé les composants, republiez le site.

Les règles qui s’appliquent à un composant activé par badge sont celles du noeud actif ou de son ancêtre.

Si le noeud est de type `cq:Page` (recommandé), puis à l’aide de CRXDE|Lite, ajoutez les propriétés à son `jcr:content` noeud .

| **Propriété** | **Type** | **Description** |
|---|---|---|
| badgingRules | Chaîne | une liste de tableaux de [règles de badge](#badging-rules) |
| scoringRules | Chaîne | une liste de tableaux de [règles de notation](#scoring-rules) |

>[!NOTE]
>
>Si une règle de notation ne semble avoir aucun effet sur l’attribution des badges, assurez-vous que la règle de notation n’a pas été bloquée par la propriété scoringRules de la règle de badge. Voir la section intitulée [Règles de badge](#badging-rules).

### Activation des badges pour le composant {#enable-badges-for-component}

Les règles de notation et de mise en page ne sont appliquées que pour les instances de composants qui ont activé la mise en badge en modifiant la configuration du composant dans [mode création](/help/communities/author-communities.md).

Une propriété booléenne, `allowBadges`, active/désactive l’affichage des badges pour une instance de composant. Il peut être configuré dans la variable [boîte de dialogue de modification du composant](/help/communities/author-communities.md) pour les composants forum, Q&amp;R et commentaire via une case à cocher intitulée **Badges d’affichage**.

#### Exemple : allowBadges pour l’instance de composant Forum {#example-allowbadges-for-forum-component-instance}

![enable-badges-component](assets/enable-badges-component.png)

>[!NOTE]
>
>N’importe quel composant peut être superposé pour afficher les badges à l’aide du code HBS trouvé dans les forums, la qualité de service et les commentaires comme exemple.

## Règles de notation {#scoring-rules}

Les règles de notation sont la base de la notation pour l’attribution de badges.

Chaque règle de notation est une liste d’une ou de plusieurs sous-règles. Les règles de notation sont appliquées au contenu du site de la communauté afin d’identifier les règles à appliquer lorsque les badges sont activés.

Les règles de notation sont héritées, mais pas additifs. Par exemple :

* Si la page 2 contient la règle de notation 2 et que sa page 1 ancêtre contient la règle de notation 1.
* Une action sur un composant page2 appelle à la fois règle1 et règle2.
* Si les deux règles contiennent des sous-règles applicables pour la même `topic/verb`:

   * Seule la sous-règle de la règle 2 affecte le score.
   * Les scores des deux sous-règles ne sont pas ajoutés.

S’il existe plusieurs règles de notation, les scores sont conservés séparément pour chaque règle.

Les règles de notation sont des noeuds de type `cq:Page` avec les propriétés à sa disposition `jcr:content` qui spécifient la liste des sous-règles qui la définissent.

Les scores sont stockés dans SRP.

>[!NOTE]
>
>Bonne pratique : attribuez un nom unique à chaque règle de notation.
>
>Les noms des règles de notation doivent être uniques au niveau global. Ils ne doivent pas se terminer par le même nom.
>
>Exemple d’objet *not* pour effectuer les opérations suivantes :
>
>/libs/settings/community/scoring/rules/site1/forums-scoring
>/libs/settings/community/scoring/rules/site2/forums-scoring

### Sous-règles de notation {#scoring-sub-rules}

Les sous-règles de notation contiennent les propriétés qui détaillent les valeurs de participation à la communauté.

Chaque sous-règle de notation identifie :

* Quelles activités sont suivies ?
* Quelle fonction communautaire spécifique est impliquée ?
* Combien de points sont attribués ?

Par défaut, les points sont attribués au membre qui agit, sauf si la sous-règle spécifie au propriétaire du contenu qu’il reçoit les points ( `forOwner`).

Chaque sous-règle peut être incluse dans une ou plusieurs règles de notation.

Le nom de la sous-règle suit généralement le modèle d’utilisation d’une *subject*, *objet*, et *verbe*. Par exemple :

* member-comment-create
* member-receive-vote

Les sous-règles sont des noeuds de type `cq:Page` avec les propriétés à sa disposition `jcr:content`qui spécifient le noeud [verbes et rubriques](#topics-and-verbs) .

<table>
 <tbody>
  <tr>
   <th>Propriété</th>
   <th>Type</th>
   <th> Valeur Description</th>
  </tr>
  <tr>
   <td><i><code>VERB</code></i></td>
   <td>Long</td>
   <td>
    <ul>
     <li>obligatoire ; le verbe correspond à une action d’événement.</li>
     <li>il doit y avoir au moins une propriété verb</li>
     <li>le verbe doit être saisi en MAJUSCULES</li>
     <li>il peut y avoir plusieurs propriétés de verbe, mais pas de doublons.</li>
     <li>la valeur est le score à appliquer pour cet événement.</li>
     <li>la valeur peut être positive ou négative.</li>
     <li>la liste des verbes pris en charge dans la version figure dans la section <a href="#topics-and-verbs">Rubriques et verbes</a> section</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>topics</code></td>
   <td>Chaîne</td>
   <td>
    <ul>
     <li>facultatif ; limite la sous-règle aux composants de communauté identifiés par les rubriques d’événement</li>
     <li>si spécifié : la valeur est une chaîne à plusieurs valeurs de rubriques d’événement</li>
     <li>une liste des rubriques de cette version figure dans la section <a href="#topics-and-verbs">Rubriques et verbes</a> section</li>
     <li>La valeur par défaut est d’appliquer à toutes les rubriques associées aux verbes.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>forOwner</code></td>
   <td>Booléen</td>
   <td>
    <ul>
     <li>facultatif ; non pertinent lorsque le membre agit sur le contenu lui-même</li>
     <li>si la valeur est true, appliquez un score au propriétaire du contenu sur lequel l’action a été effectuée.</li>
     <li>si la valeur est false, appliquez un score à l’action du membre.</li>
     <li>false par défaut</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>scoringType</code></td>
   <td>Chaîne</td>
   <td>
    <ul>
     <li>facultatif ; identifie le moteur de notation</li>
     <li>si "basic", spécifie le moteur de notation en fonction de la quantité
      <ul>
       <li>inclus dans la version</li>
      </ul> </li>
     <li>si "advanced", indique le moteur de notation en fonction de la qualité et de la quantité
      <ul>
       <li>nécessite une <a href="/help/communities/advanced.md">package supplémentaire</a></li>
      </ul> </li>
     <li>La valeur par défaut est "basic"</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Règles de notation et sous-règles incluses {#included-scoring-rules-and-sub-rules}

Cette version comprend deux règles de notation pour la variable [Fonction Forum](/help/communities/functions.md#forum-function) (un pour les composants Forum et Commentaires de la fonction Forum ) :

1. /libs/settings/community/scoring/rules/comments-scoring

   * subRules[] = /libs/settings/community/scoring/rules/sub-rules/member-comment-create /libs/settings/community/scoring/rules/sub-rules/member-receive-vote /libs/settings/community/scoring/rules/sub-rules/member-don-voter /libs/settings/community/scoring/rules/sub-rules/member-is-modérated

1. /libs/settings/community/scoring/rules/forums-scoring

   * subRules[] = /libs/settings/community/scoring/rules/sub-rules/member-forum-create /libs/settings/community/scoring/rules/sub-rules/member-receive-vote /libs/settings/community/scoring/rules/sub-rules/member-don-voter /libs/settings/community/scoring/rules/sub-rules/member-is-modérated

**Remarques:**

* Les deux `rules` et `sub-rules` Les noeuds sont de type cq:Page.

* `subRules` est un attribut de type String[] sur la règle `jcr:content` noeud .

* `sub-rules` peut être partagée entre différentes règles de notation.
* `rules` doit se trouver dans un emplacement de référentiel avec une autorisation de lecture pour tout le monde.

   * Les noms des règles doivent être uniques, quel que soit l’emplacement.

### Activation de règles de notation personnalisées {#activating-custom-scoring-rules}

Toute modification ou tout ajout apporté aux règles de notation ou aux sous-règles effectuées dans l’environnement de création doit être installé lors de la publication.

## Règles de badge {#badging-rules}

Les règles de badge lient les règles de notation aux badges en spécifiant :

* Règle de notation
* Score nécessaire pour obtenir un badge spécifique

Les règles de badge sont des noeuds de type `cq:Page` avec les propriétés à sa disposition `jcr:content` noeud qui met en relation les règles de notation avec les scores et les badges.

Les règles de badge se composent d’un `thresholds` qui est une liste ordonnée de scores mappés à des badges. Les scores doivent être triés en valeur croissante. Par exemple :

* `1|/libs/settings/community/badging/images/bronze-badge/jcr:content/bronze.png`

   * Un badge en bronze est décerné pour avoir gagné un point.

* `60|/libs/settings/community/badging/images/silver-badge/jcr:content/silver.png`

   * Un badge d&#39;argent est attribué lorsque 60 points ont été accumulés.

* `80|/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png`

   * Un badge d&#39;or est attribué lorsque 80 points ont été accumulés.

Les règles de badge sont associées à des règles de notation qui déterminent la manière dont les points s’accumulent. Voir la section intitulée [Application de règles au contenu](#apply-rules-to-content).

La variable `scoringRules` sur une règle de badge limite simplement les règles de notation qui peuvent être associées à cette règle de badge spécifique.

>[!NOTE]
>
>Bonne pratique : créez des images de badge uniques à chaque site AEM.

![badging-rule-configuration](assets/badging-rule-configuration.png)

<table>
 <tbody>
  <tr>
   <th>Propriété</th>
   <th>Type</th>
   <th>Valeur Description</th>
  </tr>
  <tr>
   <td>seuils</td>
   <td>Chaîne</td>
   <td><em>(obligatoire)</em> Chaîne à plusieurs valeurs de la forme 'number|path'
    <ul>
     <li>nombre = score</li>
     <li>| = la ligne verticale char (U+007C)</li>
     <li>path = chemin complet de la ressource image de badge</li>
    </ul> Les chaînes doivent être triées de sorte que les nombres augmentent en valeur et qu’aucun espace vide ne s’affiche entre le nombre et le chemin.<br /> Exemple d’entrée :<br /> <code>80|/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png</code></td>
  </tr>
  <tr>
   <td>badgingType</td>
   <td>Chaîne</td>
   <td><em>(facultatif)</em> Identifie le moteur de notation comme "de base" ou "avancé". Si vous souhaitez utiliser le moteur de notation avancé, reportez-vous à la section <a href="/help/communities/advanced.md">Notation et badges avancés</a>. La valeur par défaut est "basic".</td>
  </tr>
  <tr>
   <td>scoringRules</td>
   <td>Chaîne</td>
   <td>(<em>facultatif</em>) Chaîne à plusieurs valeurs permettant de limiter la règle de badge aux événements de notation identifiés par les règles de notation.</td>
  </tr>
 </tbody>
</table>

### Règles de badge incluses {#included-badging-rules}

Cette version comprend deux règles de badge qui correspondent à la variable [Forums et règles de notation des commentaires](#includedscoringrules).

* `/libs/settings/community/badging/rules/comments-badging`

* `/libs/settings/community/badging/rules/forums-badging`

**Remarques:**

* `rules` Les noeuds sont de type cq:Page.
* `rules` doit se trouver dans un emplacement de référentiel avec une autorisation de lecture pour tout le monde.

   * Les noms des règles doivent être uniques, quel que soit leur emplacement.

### Activation de règles de badge personnalisées {#activating-custom-badging-rules}

Toute modification ou tout ajout apporté aux règles de badge ou aux images effectuées dans l’environnement de création doit être installé lors de la publication.

## Affecter et révoquer des badges {#assign-and-revoke-badges}

Les badges peuvent être attribués aux membres à l’aide de la fonction [console membres](/help/communities/members.md#badges-tab) ou par programmation à l’aide des commandes cURL.

Les commandes cURL suivantes indiquent les éléments nécessaires à une requête HTTP d’attribution et de révocation des badges. Le format de base est le suivant :

cURL -i -X POST -H *header* -u *signature* -F *operation* -F *badge* *member-profile-url*

*header* = En-tête personnalisé &quot;Accept:application/json&quot; à transmettre au serveur (obligatoire)

*signature* = administrator-id:password par exemple, admin:admin

*operation* = &quot;:operation=social:assignBadge&quot; OU &quot;:operation=social:deleteBadge&quot;

*badge* = &quot;badgeContentPath=*badge-image-file*&quot;

*badge-image-file* = emplacement du fichier image de badge dans le référentiel, par exemple, /libs/settings/community/badging/images/modérator/jcr:content/moderator.png

*member-profile-url* = point de terminaison du profil du membre lors de la publication, par exemple, https://&lt;server>:&lt;port>/home/users/community/riley/profile.social.json

>[!NOTE]
>
>La variable *member-profile-url*:
>
>* Peut faire référence à une instance d’auteur si la variable [Service Tunnel](/help/communities/users.md#tunnel-service) est activée.
>* Peut être un nom obscur et aléatoire - voir [Liste de contrôle de sécurité](/help/sites-administering/security-checklist.md#verify-that-you-are-not-disclosing-personally-identifiable-information-in-the-users-home-path) concernant l’ID autorisable.

### Exemples : {#examples}

#### Attribution d’un badge de modérateur {#assign-a-moderator-badge}

```shell
curl -i -X POST -H "Accept:application/json" -u admin:admin -F ":operation=social:assignBadge" -F "badgeContentPath=/libs/settings/community/badging/images/moderator/jcr:content/moderator.png" /home/users/community/updcs9DndLEI74DB9zsB/profile.social.json
```

#### Révoquer un badge d’argent attribué {#revoke-an-assigned-silver-badge}

```shell
curl -i -X POST -H "Accept:application/json" -u admin:admin -F ":operation=social:deleteBadge" -F "badgeContentPath=/libs/settings/community/badging/images/silver/jcr:content/silver.png" /home/users/community/updcs9DndLEI74DB9zsB/profile.social.json
```

>[!NOTE]
>
>L’utilisation de cURL pour attribuer et révoquer des badges fonctionne pour n’importe quelle image de badge, mais lorsqu’elle est affectée au lieu d’être acquise, elles sont marquées comme des badges attribués et gérées en conséquence.

## Notation et badges pour les composants personnalisés {#scoring-and-badges-for-custom-components}

Il est possible de créer des règles de notation et de badge pour les composants personnalisés en associant les rubriques d’événement créées pour le composant aux verbes.

## Rubriques et verbes {#topics-and-verbs}

Lorsque les membres interagissent avec les fonctionnalités des communautés, des événements sont envoyés, qui peuvent déclencher des écouteurs asynchrones, tels que des notifications et des scores.

L’instance SocialEvent d’un composant enregistre les événements en tant que `actions` qui se produit pour un `topic`. SocialEvent comprend une méthode pour renvoyer une `verb` associée à l’action. Il existe une *n-1* relation entre `actions` et `verbs`.

Pour les composants des communautés distribués, les tableaux suivants décrivent la variable `verbs` définie pour chaque `topic` disponible dans [règles de notation](#scoring-sub-rules).

>[!NOTE]
>
>Une nouvelle propriété booléenne, `allowBadges`, active/désactive l’affichage des badges pour une instance de composant. Il peut être configuré dans la mise à jour [modification de composant, boîtes de dialogue](/help/communities/author-communities.md) à travers une case à cocher étiquetée **Badges d’affichage**.

**[Composant Calendrier](/help/communities/calendar.md)**
SocialEvent `topic`= com/adobe/cq/social/calendar

| **Verbe** | **Description** |
|---|---|
| POST | crée un événement de calendrier. |
| AJOUTER | commentaires d’un membre sur un événement de calendrier |
| MISE À JOUR | l’événement ou le commentaire de calendrier du membre est modifié. |
| SUPPRIMER | l’événement ou le commentaire de calendrier du membre est supprimé. |

**[Composant Commentaires](/help/communities/comments.md)**
SocialEvent `topic`= com/adobe/cq/social/comment

| **Verbe** | **Description** |
|---|---|
| POST | crée un commentaire. |
| AJOUTER | réponses du membre au commentaire |
| MISE À JOUR | le commentaire du membre est modifié. |
| SUPPRIMER | le commentaire du membre est supprimé. |

**[Composant Bibliothèque de fichiers](/help/communities/file-library.md)**
SocialEvent `topic`= com/adobe/cq/social/fileLibrary

| **Verbe** | **Description** |
|---|---|
| POST | crée un dossier |
| ATTACH | Le membre charge un fichier |
| MISE À JOUR | met à jour un dossier ou un fichier |
| SUPPRIMER | supprime un dossier ou un fichier |

**[Composant du forum](/help/communities/forum.md)**
SocialEvent `topic`= com/adobe/cq/social/forum

| **Verbe** | **Description** |
|---|---|
| POST | thème de forum de création de membre |
| AJOUTER | réponses des membres au sujet du forum |
| MISE À JOUR | Le sujet ou la réponse du forum du membre est modifié |
| SUPPRIMER | La rubrique ou la réponse du forum du membre est supprimée |

**[Composant Journal](/help/communities/blog-feature.md)**
SocialEvent `topic`= com/adobe/cq/social/journal

| **Verbe** | **Description** |
|---|---|
| POST | Un membre crée un article de blog |
| AJOUTER | commentaires d&#39;un membre sur un article de blog |
| MISE À JOUR | article ou commentaire de blog du membre modifié |
| SUPPRIMER | article ou commentaire de blog du membre supprimé |

**[Composant Q&amp;R](/help/communities/working-with-qna.md)**
SocialEvent `topic` = com/adobe/cq/social/qna

| **Verbe** | **Description** |
|---|---|
| POST | crée une question Q&amp;R |
| AJOUTER | crée une réponse Q&amp;R |
| MISE À JOUR | Question ou réponse Q&amp;R du membre modifié |
| SELECT | la réponse du membre est sélectionnée. |
| UNSELECT | la réponse du membre est désélectionnée. |
| SUPPRIMER | Question ou réponse Q&amp;R du membre supprimée |

**[Composant Révisions](/help/communities/reviews.md)**
SocialEvent `topic`= com/adobe/cq/social/review

| **Verbe** | **Description** |
|---|---|
| POST | création d’une révision par le membre |
| MISE À JOUR | révision du membre est modifiée |
| SUPPRIMER | la révision du membre est supprimée. |

**[Composant d’évaluation](/help/communities/rating.md)**
SocialEvent `topic`= com/adobe/cq/social/tally/rating

| **Verbe** | **Description** |
|---|---|
| AJOUTER UNE NOTE | le contenu du membre a été mis au point |
| SUPPRESSION DE LA NOTE | le contenu du membre a été abaissé. |

**[Composant Vote](/help/communities/voting.md)**
SocialEvent `topic`= com/adobe/cq/social/tally/vote

| **Verbe** | **Description** |
|---|---|
| AJOUTER UN VOTE | le contenu du membre a été voté |
| SUPPRIMER LE VOTE | le contenu du membre a été rejeté |

**Composants activés pour la modération**
SocialEvent `topic`= com/adobe/cq/social/modération

| **Verbe** | **Description** |
|---|---|
| DENY | le contenu du membre est refusé ; |
| INDICATEUR : INAPPROPRIÉ | le contenu du membre est marqué |
| INAPPROPRIÉ | le contenu du membre n’est pas marqué |
| ACCEPTER | le contenu du membre est approuvé par le modérateur ; |
| CLOSE | le membre ferme le commentaire aux modifications et aux réponses |
| OUVRIR | commentaire de réouverture du membre |

### Événements de composant personnalisés {#custom-component-events}

Pour un composant personnalisé, un événement SocialEvent est appelé pour enregistrer les événements du composant comme `actions` qui se produit pour un `topic`.

Pour prendre en charge la notation, SocialEvent doit remplacer la méthode . `getVerb()` afin qu’une `verb` est renvoyé pour chaque `action`. La variable `verb` renvoyé pour une action peut être une méthode couramment utilisée (telle que `POST`) ou spécialisé pour le composant (par exemple `ADD RATING`). Il existe une *n-1* relation entre `actions` et `verbs`.

## Résolution des problèmes {#troubleshooting}

### Les badges ne s’affichent pas {#badges-are-not-appearing}

Si des règles de notation et de badge ont été appliquées au contenu du site web, mais que des badges n’ont été attribués pour aucune activité, assurez-vous que les badges ont été activés pour l’instance de ce composant.

Voir [Activation des badges pour le composant](#enable-badges-for-component).

### La règle de notation n’a aucun effet {#scoring-rule-has-no-effect}

Si des règles de notation et de badge ont été appliquées au contenu du site web et que des badges sont attribués pour certaines actions, mais pas pour d’autres, vérifiez que la règle de badge n’a pas restreint les règles de notation auxquelles elle s’applique.

Voir `scoringRules` de [Règles de badge](#badging-rules).

### Type sensible à la casse {#case-sensitive-typo}

La plupart des propriétés et valeurs, en particulier les verbes, sont sensibles à la casse. Les verbes doivent être en MAJUSCULES lorsqu’ils sont utilisés dans une sous-règle de notation.

Si la fonction ne fonctionne pas comme prévu, vérifiez que les données ont été correctement saisies.

## Test rapide {#quick-test}

Il est possible d’essayer rapidement la notation et la notation à l’aide de la variable [Tutoriel de prise en main](/help/communities/getting-started.md) site (engage) :

* Accédez au CRXDE Lite sur l’auteur.
* Accédez à la page de base :

   * /content/sites/engage/en/jcr:content

* Ajoutez la propriété badgingRules :

   * **Nom** : `badgingRules`
   * **Type** : `String`
   * Sélectionner **Multi**
   * Sélectionner **Ajouter**
   * Enter `/libs/settings/community/badging/rules/forums-badging`
   * Sélectionner **+**
   * Enter `/libs/settings/community/badging/rules/comments-badging`
   * Sélectionnez **OK**.

* Ajoutez la propriété scoringRules :

   * **Nom** : `scoringRules`
   * **Type** : `String`
   * Sélectionner **Multi**
   * Sélectionner **Ajouter**
   * Enter `/libs/settings/community/scoring/rules/forums-scoring`
   * Sélectionner **+**
   * Enter `/libs/settings/community/scoring/rules/comments-scoring`
   * Sélectionnez **OK**.

* Sélectionnez **Enregistrer tout**.

![test-scoring-badging](assets/test-scoring-badging.png)

Ensuite, assurez-vous que les composants de forum et de commentaires permettent l’affichage des badges :

* Encore une fois en utilisant CRXDE Lite.
* Accédez au composant Forum

   * `/content/sites/engage/en/forum/jcr:content/content/primary/forum`

* Ajoutez la propriété booléenne allowBadges, si nécessaire, et assurez-vous qu’elle est définie sur true.

   * **Nom** : `allowBadges`
   * **Type** : `Boolean`
   * **Valeur** : `true`

![test-forum-component](assets/test-forum-component.png)

Ensuite, [republier](/help/communities/sites-console.md#publishing-the-site) le site de la communauté.

Enfin,

* Accédez au composant sur l’instance de publication.
* Connectez-vous en tant que membre de la communauté (par exemple, weston.mccall@dodgit.com / password).
* Publiez un nouveau sujet de forum.
* La page doit être actualisée pour que le badge s’affiche.

   * Déconnectez-vous et connectez-vous en tant que membre différent de la communauté (par exemple : aaron.mcdonald@mailinator.com/password).

* Sélectionnez le Forum.

Cela devrait permettre au membre de la communauté d’obtenir un badge en bronze visible avec sa publication sur le forum car le premier seuil de la règle de badge des forums est de 1.

![bronzebadge](assets/bronzebadge.png)

## Informations supplémentaires {#additional-information}

Vous trouverez plus d’informations sur la [Notions fondamentales sur la notation et les badges](/help/communities/configure-scoring.md) pour les développeurs.

Pour plus d’informations sur le moteur de notation avancé, voir [Notation et badges avancés](/help/communities/advanced.md).

Tableau de classement configurable [component](/help/communities/enabling-leaderboard.md) et [function](/help/communities/functions.md#leaderboard-function) simplifie l’affichage des membres et de leurs scores sur un site communautaire.
