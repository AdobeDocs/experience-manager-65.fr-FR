---
title: Scores et badges avancés
seo-title: Scores et badges avancés
description: Configuration d’un score avancé
seo-description: Configuration d’un score avancé
uuid: 48caca57-43d3-4f2f-adf3-257428ba54d5
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: eb3d5c37-8097-46de-8c4f-804ea723f1c5
docset: aem65
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 1%

---


# Scores et badges avancés{#advanced-scoring-and-badges}

## Présentation {#overview}

La notation avancée permet l&#39;attribution de badges pour identifier les membres comme experts. Le score avancé attribue des points en fonction de la qualité *et* du contenu créé par un membre, tandis que le score de base attribue des points simplement en fonction de la quantité de contenu créée.

Cette différence est due au moteur de notation utilisé pour calculer les scores. Le moteur de score de base applique des maths simples. Le moteur de score avancé est un algorithme adaptatif qui récompense les membres principaux qui contribuent à un contenu pertinent et précieux, déduit par le traitement du langage naturel (NLP) d’une rubrique.

Outre la pertinence du contenu, les algorithmes de notation prennent en compte les activités membres, telles que le vote et le pourcentage de réponses. Bien que le score de base les inclut quantitativement, le score avancé les utilise de manière algorithmique.

Par conséquent, le moteur d’évaluation avancé nécessite suffisamment de données pour que l’analyse ait du sens. Le seuil de réussite pour devenir un expert est constamment réévalué à mesure que l’algorithme s’ajuste continuellement au volume et à la qualité du contenu créé. Il existe également un concept de &lt; a0/>désintégration *des postes plus anciens d&#39;un membre.* Si un membre expert cesse de participer à la matière sur laquelle il a acquis le statut d&#39;expert, à un moment déterminé (voir [configuration du moteur de notation](#configurable-scoring-engine)), il pourrait perdre son statut d&#39;expert.

La configuration d’un score avancé est pratiquement identique à celle d’un score de base :

* Les règles de notation et de badge de base et avancées sont [appliquées de la même manière au contenu](/help/communities/implementing-scoring.md#apply-rules-to-content).

   * Des règles de notation et de badge de base et avancées peuvent être appliquées au même contenu.

* [L&#39;activation des badges pour les ](/help/communities/implementing-scoring.md#enable-badges-for-component) composants est générique.

Les différences dans la configuration des règles de notation et de badge sont les suivantes :

* Moteur de notation avancé configurable
* Règles de notation avancées :

   * `scoringType`Définissez  sur `advanced`.
   * Requiert `stopwords`

* Règles de mise en badge avancées :

   * `badgingType`Définissez  sur `advanced`.
   * `badgingLevels` fixé au  **nombre de niveaux d&#39;experts à attribuer**
   * Nécessite un `badgingPaths` tableau de badges au lieu des points de mappage de la baie de seuils aux badges.

>[!NOTE]
>
>Pour utiliser des capacités avancées de notation et de badge, installez le [module d&#39;identification d&#39;expert](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/social/cq-social-expert-identification-pkg).

## Moteur de score configurable {#configurable-scoring-engine}

Le moteur d’évaluation avancé fournit une configuration OSGi avec des paramètres qui affectent l’algorithme d’évaluation avancé.

![moteur de score avancé](assets/advanced-scoring-engine.png)

* **Poids de score**

   Pour une rubrique, spécifiez le verbe qui doit recevoir la priorité la plus élevée lors du calcul du score. Une ou plusieurs rubriques peuvent être entrées, mais limitées à **un verbe par rubrique**. Voir [Rubriques et verbes](/help/communities/implementing-scoring.md#topics-and-verbs).
Saisissez `topic,verb` avec la virgule échappée. Par exemple :
   `/social/forum/hbs/social/forum\,ADD`
La valeur par défaut est définie sur le verbe AJOUTER pour les composants QnA et de forum.

* **Plage de score**

   La plage des scores avancés est définie par cette valeur (score maximum possible) et par 0 (score minimum possible).

   La valeur par défaut est 100, de sorte que la plage de score soit comprise entre 0 et 100.

* **Intervalle de décomposition d&#39;entité**

   Ce paramètre représente le nombre d’heures après lesquelles tous les scores d’entité sont décalés. Ceci est nécessaire pour ne plus inclure de contenu ancien dans les scores d’un site communautaire.

   La valeur par défaut est de 2 16 000 heures (~24 ans).

* **Score de croissance**
Taux de croissanceIndique le score compris entre 0 et la plage de score, au-delà de laquelle la croissance ralentit pour limiter le nombre d&#39;experts.

   La valeur par défaut est 50.

## Règles de score avancées {#advanced-scoring-rules}

Dans le score de base, la quantité nécessaire pour gagner un badge est connue.

Dans le cadre d’un score avancé, la quantité nécessaire est constamment ajustée en fonction de la quantité de données de qualité au sein du système. Le score est calculé en permanence de la même manière qu&#39;une courbe en cloche.

Si un membre a gagné un badge d&#39;expert sur un sujet qui n&#39;est plus principal, il est possible qu&#39;il perde son badge à cause de la dégradation au fil du temps.

### scoreType {#scoringtype}

Une règle d’évaluation est un ensemble de sous-règles d’évaluation, chacune d’elles déclarant le `scoringType`.

Pour appeler le moteur de score avancé, `scoringType`doit être défini sur `advanced`.

Voir [Sous-règles de score](/help/communities/implementing-scoring.md#scoring-sub-rules).

![type de score avancé](assets/advanced-scoring-type.png)

### Mots-clés {#stopwords}

Le package d’évaluation avancé installe un dossier de configuration contenant un fichier de mots de passe :

* `/libs/settings/community/scoring/configuration/stopwords`

L’algorithme d’évaluation avancé utilise la liste des mots contenus dans le fichier de mots-clés pour identifier les mots anglais courants qui sont ignorés pendant le traitement du contenu.

On ne s&#39;attend pas à ce que ce fichier soit modifié.

Si le fichier de mots-clés est manquant, le moteur d’évaluation avancé génère une erreur.

## Règles de badge avancées {#advanced-badging-rules}

Les propriétés avancées de la règle de badge diffèrent des [propriétés de la règle de badge de base](/help/communities/implementing-scoring.md#badging-rules).

Au lieu d&#39;associer des points à une image de badge, il suffit d&#39;identifier le nombre d&#39;experts autorisés et l&#39;image de badge à attribuer.

![règles avancées de badge](assets/advanced-badging-rules.png)

<table>
 <tbody>
  <tr>
   <th>Propriété</th>
   <th>Type</th>
   <th>Description de la valeur</th>
  </tr>
  <tr>
   <td>badgingPath</td>
   <td>Chaîne[]</td>
   <td><em>(Obligatoire)</em> Chaîne multi-valeurs d’images de badge jusqu’au nombre de badgingLevels. Les chemins d'image du badge doivent être commandés pour que le premier soit attribué au plus haut expert. S'il y a moins de badges qu'indiqué par badgingLevels, le dernier badge de la baie remplit le reste de la baie. Exemple d'entrée :<br /> <code>/libs/settings/community/badging/images/expert-badge/jcr:content/expert.png</code></td>
  </tr>
  <tr>
   <td>badgingLevels</td>
   <td>Long</td>
   <td><em>(Facultatif)</em> Indique les niveaux d’expertise à attribuer. Par exemple, s’il doit y avoir <code>expert </code>et <code>almost expert</code> (deux badges), la valeur doit être définie sur 2. Le badgingLevel doit correspondre au nombre d’images de badge d’expert répertoriées pour la propriété badgingPath. La valeur par défaut est 1.</td>
  </tr>
  <tr>
   <td>badgingType</td>
   <td>Chaîne</td>
   <td><em>(Obligatoire)</em> Identifie le moteur d’évaluation comme étant "de base" ou "avancé". Défini sur "avancé", sinon la valeur par défaut est "de base".</td>
  </tr>
  <tr>
   <td>scoringRules</td>
   <td>Chaîne[]</td>
   <td><em>(Facultatif)</em> Chaîne à plusieurs valeurs pour limiter la règle de badge aux événements de notation identifiés par la ou les règles de notation répertoriées.<br /> Exemple d’entrée : <br /> <code>/libs/settings/community/scoring/rules/adv-comments-scoring</code><br /> La valeur par défaut n’est pas une restriction.</td>
  </tr>
 </tbody>
</table>

## Règles et badge inclus {#included-rules-and-badge}

### Badge inclus {#included-badge}

Cette version bêta comprend un badge d&#39;expert basé sur la récompense :

* `expert`

   `/libs/settings/community/badging/images/expert-badge/jcr:content/expert.png`

![badge d&#39;expert](assets/included-badge.png)

Pour que le badge d&#39;expert s&#39;affiche comme une récompense pour l&#39;activité, assurez-vous que :

* `Badges` sont activées pour la fonction, par exemple un forum ou un composant QnA.

* Les règles avancées de notation et de badge sont appliquées à la page (ou à l’ancêtre) sur laquelle le composant est placé.

Consultez les informations de base pour :

* [Activation de la mise en badge pour un composant](/help/communities/implementing-scoring.md#enableforcomponent)
* [Application de règles](/help/communities/implementing-scoring.md#applytopage)

### Règles et sous-règles de score incluses {#included-scoring-rules-and-sub-rules}

La version bêta comprend deux règles de notation avancées pour la fonction de forum [](/help/communities/functions.md#forum-function) (une pour chacune des composantes du forum et des commentaires de la fonction de forum) :

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

* Les noeuds `rules` et `sub-rules` sont de type `cq:Page`.

* `subRules` est un attribut de type [] String sur le  `jcr:content` noeud de la règle.

* `sub-rules` peut être partagée entre différentes règles de notation.

* `rules` doit être situé dans un emplacement de référentiel avec une autorisation de lecture pour tout le monde.

* Les noms de règle doivent être uniques, quel que soit l’emplacement.

### Règles de mise en badge incluses {#included-badging-rules}

Cette version comprend deux règles de mise en badge avancées qui correspondent aux [forums avancés et aux règles de notation des commentaires](#included-scoring-rules-and-sub-rules).

* `/libs/settings/community/badging/rules/adv-comments-badging`
* `/libs/settings/community/badging/rules/adv-forums-badging`

**Remarques:**

* `rules` sont de type cq:Page.
* `rules` doit être situé dans un emplacement de référentiel avec une autorisation de lecture pour tout le monde.
* Les noms de règle doivent être uniques, quel que soit l’emplacement.

