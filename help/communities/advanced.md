---
title: Notation et badges avancés
seo-title: Notation et badges avancés
description: Configuration d’une notation avancée
seo-description: Configuration d’une notation avancée
uuid: 48caca57-43d3-4f2f-adf3-257428ba54d5
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: eb3d5c37-8097-46de-8c4f-804ea723f1c5
docset: aem65
role: Administrator
exl-id: d3bb6664-6c01-4bcf-840c-072fc491fc99
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 2%

---

# Notation et badges avancés{#advanced-scoring-and-badges}

## Présentation {#overview}

La notation avancée permet l’attribution de badges afin d’identifier les membres en tant qu’experts. La notation avancée attribue des points en fonction de la qualité *et* du contenu créé par un membre, tandis que la notation de base attribue des points simplement en fonction de la quantité de contenu créée.

Cette différence est due au moteur de notation utilisé pour calculer les scores. Le moteur de notation de base applique des maths simples. Le moteur de notation avancé est un algorithme adaptatif qui récompense les membres principaux qui apportent du contenu utile et pertinent, déduit par le traitement du langage naturel (NLP) d’un sujet.

Outre la pertinence du contenu, les algorithmes de notation prennent en compte les activités des membres, telles que le vote et le pourcentage de réponses. Bien que la notation de base les inclut quantitativement, la notation avancée les utilise de manière algorithmique.

Par conséquent, le moteur de notation avancé nécessite suffisamment de données pour que l’analyse ait du sens. Le seuil de réussite pour devenir un expert est constamment réévalué, l’algorithme s’adaptant continuellement au volume et à la qualité du contenu créé. Il existe également un concept de *atténuation* des publications plus anciennes d’un membre. Si un membre expert cesse de participer au sujet sur lequel il a acquis un statut d’expert, il risque de perdre son statut d’expert à un moment prédéterminé (voir [configuration du moteur de notation](#configurable-scoring-engine)).

La configuration d’une notation avancée est pratiquement identique à la notation de base :

* Les règles de notation et de badge de base et avancées sont [appliquées de la même manière au contenu](/help/communities/implementing-scoring.md#apply-rules-to-content).

   * Des règles de notation et de badge de base et avancées peuvent être appliquées au même contenu.

* [L’activation des badges pour les ](/help/communities/implementing-scoring.md#enable-badges-for-component) composants est générique.

Les différences de configuration des règles de notation et de badge sont les suivantes :

* Moteur de notation avancé configurable
* Règles de notation avancées :

   * `scoringType`Définissez  sur `advanced`.
   * Requiert `stopwords`

* Règles de badge avancées :

   * `badgingType`Définissez  sur `advanced`.
   * `badgingLevels` définir sur le  **nombre de niveaux d&#39;experts à attribuer**
   * Nécessite un `badgingPaths` tableau de badges au lieu du mappage de tableau de seuils pointe vers des badges.

>[!NOTE]
>
>Pour utiliser les fonctionnalités avancées de notation et de badge, installez le [package d’identification des experts](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/social/cq-social-expert-identification-pkg).

## Moteur de notation configurable {#configurable-scoring-engine}

Le moteur de notation avancé fournit une configuration OSGi avec des paramètres qui affectent l’algorithme de notation avancé.

![advanced-scoring-engine](assets/advanced-scoring-engine.png)

* **Poids de notation**

   Pour une rubrique, spécifiez le verbe qui doit avoir la priorité la plus élevée lors du calcul du score. Une ou plusieurs rubriques peuvent être saisies, mais limitées à **un verbe par rubrique**. Voir [Rubriques et verbes](/help/communities/implementing-scoring.md#topics-and-verbs).
Saisissez comme `topic,verb` avec la virgule échappée. Par exemple :
   `/social/forum/hbs/social/forum\,ADD`
La valeur par défaut est définie sur le verbe AJOUTER pour les composants Q&amp;R et de forum.

* **Plage de notation**

   La plage des scores avancés est définie par cette valeur (note maximale possible) et 0 (note minimale possible).

   La valeur par défaut est 100, de sorte que la plage de notation est comprise entre 0 et 100.

* **Intervalle de délai de décomposition des entités**

   Ce paramètre représente le nombre d’heures après lesquelles tous les scores de l’entité sont décalés. Cela est nécessaire pour ne plus inclure d’anciens contenus dans les scores d’un site de communauté.

   La valeur par défaut est de 216000 heures (~24 ans).

* ****
Taux de croissance du scoreCeci spécifie le score entre 0 et la plage de notation, au-delà duquel la croissance ralentit pour limiter le nombre d’experts.

   La valeur par défaut est 50.

## Règles de notation avancées {#advanced-scoring-rules}

Dans la notation de base, la quantité nécessaire pour gagner un badge est connue.

Dans le cadre d’une notation avancée, la quantité nécessaire est constamment ajustée en fonction de la quantité de données de qualité au sein du système. La notation est calculée en permanence d’une manière semblable à une courbe en cloche.

Si un membre a obtenu un badge d&#39;expert sur un sujet qui n&#39;est plus principal, il est possible qu&#39;il perde son badge à cause d&#39;une dégradation dans le temps.

### scoringType {#scoringtype}

Une règle de notation est un ensemble de sous-règles de notation, dont chacune déclare la balise `scoringType`.

Pour appeler le moteur de notation avancé, la valeur `scoringType`doit être définie sur `advanced`.

Voir [Sous-règles de notation](/help/communities/implementing-scoring.md#scoring-sub-rules).

![advanced-scoring-type](assets/advanced-scoring-type.png)

### Stopwords {#stopwords}

Le module de notation avancée installe un dossier de configuration contenant un fichier de mots-clés :

* `/libs/settings/community/scoring/configuration/stopwords`

L’algorithme de notation avancée utilise la liste des mots contenus dans le fichier stopwords pour identifier les mots anglais courants qui sont ignorés pendant le traitement du contenu.

Il n’est pas prévu que ce fichier soit modifié.

Si le fichier des mots-clés est manquant, le moteur de notation avancé renvoie une erreur.

## Règles de badge avancé {#advanced-badging-rules}

Les propriétés avancées des règles de badge diffèrent des [propriétés de base des règles de badge](/help/communities/implementing-scoring.md#badging-rules).

Au lieu d&#39;associer des points à une image de badge, il suffit d&#39;identifier le nombre d&#39;experts autorisés et l&#39;image de badge à attribuer.

![advanced-badging-rules](assets/advanced-badging-rules.png)

<table>
 <tbody>
  <tr>
   <th>Propriété</th>
   <th>Type</th>
   <th>Valeur Description</th>
  </tr>
  <tr>
   <td>badgingPath</td>
   <td>Chaîne[]</td>
   <td><em>(Obligatoire)</em> Chaîne à plusieurs valeurs d’images de badge jusqu’au nombre de badgingLelevels. Les chemins des images du badge doivent être triés afin que le premier soit attribué au plus haut expert. S’il existe moins de badges qu’indiqué par badgingLelevels, le dernier badge du tableau remplit le reste du tableau. Exemple d’entrée :<br /> <code>/libs/settings/community/badging/images/expert-badge/jcr:content/expert.png</code></td>
  </tr>
  <tr>
   <td>badgingLelevels</td>
   <td>Long</td>
   <td><em>(Facultatif)</em> Indique les niveaux d’expertise à attribuer. Par exemple, s’il doit y avoir <code>expert </code>et <code>almost expert</code> (deux badges), la valeur doit être définie sur 2. Le badgingLevel doit correspondre au nombre d’images de badge associées à un expert répertoriées pour la propriété badgingPath. La valeur par défaut est 1.</td>
  </tr>
  <tr>
   <td>badgingType</td>
   <td>Chaîne</td>
   <td><em>(Obligatoire)</em> Identifie le moteur de notation comme étant "de base" ou "avancé". Défini sur "advanced" sinon la valeur par défaut est "basic".</td>
  </tr>
  <tr>
   <td>scoringRules</td>
   <td>Chaîne[]</td>
   <td><em>(Facultatif)</em> Chaîne à plusieurs valeurs permettant de limiter la règle de badge aux événements de notation identifiés par la ou les règles de notation répertoriées.<br /> Exemple d’entrée : <br /> <code>/libs/settings/community/scoring/rules/adv-comments-scoring</code><br /> La valeur par défaut est sans restriction.</td>
  </tr>
 </tbody>
</table>

## Règles et badge inclus {#included-rules-and-badge}

### Badge inclus {#included-badge}

Dans cette version bêta, un badge d’expert basé sur les récompenses est inclus :

* `expert`

   `/libs/settings/community/badging/images/expert-badge/jcr:content/expert.png`

![badge d&#39;expert](assets/included-badge.png)

Pour que le badge d&#39;expert apparaisse comme une récompense pour l&#39;activité, veillez à :

* `Badges` sont activés pour la fonctionnalité, comme un forum ou un composant Q&amp;R.

* Les règles de notation et de badge avancées sont appliquées à la page (ou ancêtre) sur laquelle le composant est placé.

Consultez les informations de base pour :

* [Activation de l’attribution d’un badge pour un composant](/help/communities/implementing-scoring.md#enableforcomponent)
* [Appliquer les règles](/help/communities/implementing-scoring.md#applytopage)

### Règles de notation et sous-règles incluses {#included-scoring-rules-and-sub-rules}

La version bêta comprend deux règles de notation avancées pour la [fonction de forum](/help/communities/functions.md#forum-function) (une pour les composants forum et commentaires de la fonctionnalité de forum) :

1. `/libs/settings/community/scoring/rules/adv-comments-scoring`

   * `subRules[] =
/libs/settings/community/scoring/rules/sub-rules/adv-comments-rule
/libs/settings/community/scoring/rules/sub-rules/adv-voting-rule-owner
/libs/settings/community/scoring/rules/sub-rules/adv-voting-rule`

1. `/libs/settings/community/scoring/rules/adv-forums-scoring`

   * `subRules[] =
/libs/settings/community/scoring/rules/sub-rules/adv-forums-rule
/libs/settings/community/scoring/rules/sub-rules/adv-comments-rule
/libs/settings/community/scoring/rules/sub-rules/adv-voting-rule-owner`

**Remarques:**

* Les noeuds `rules` et `sub-rules` sont tous deux de type `cq:Page`.

* `subRules` est un attribut de type [] Chaîne sur le  `jcr:content` noeud de la règle.

* `sub-rules` peut être partagée entre différentes règles de notation.

* `rules` doit être situé dans un emplacement de référentiel avec une autorisation de lecture pour tout le monde.

* Les noms des règles doivent être uniques, quel que soit leur emplacement.

### Règles de badge incluses {#included-badging-rules}

Cette version comprend deux règles de badge avancées qui correspondent aux [forums avancés et aux règles de notation des commentaires](#included-scoring-rules-and-sub-rules).

* `/libs/settings/community/badging/rules/adv-comments-badging`
* `/libs/settings/community/badging/rules/adv-forums-badging`

**Remarques:**

* `rules` Les noeuds sont de type cq:Page.
* `rules` doit être situé dans un emplacement de référentiel avec une autorisation de lecture pour tout le monde.
* Les noms des règles doivent être uniques, quel que soit leur emplacement.
