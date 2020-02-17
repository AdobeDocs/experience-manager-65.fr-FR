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
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Scores et badges avancés{#advanced-scoring-and-badges}

## Présentation {#overview}

La notation avancée permet l&#39;attribution de badges pour identifier les membres comme des experts. La notation avancée affecte des points en fonction de la quantité *et *qualité du contenu créé par un membre, tandis que la notation de base affecte des points simplement en fonction de la quantité de contenu créé.

Cette différence est due au moteur de notation utilisé pour calculer les scores. Le moteur de notation de base applique des maths simples. Le moteur de notation avancé est un algorithme adaptatif qui récompense les membres actifs qui contribuent à un contenu pertinent et précieux, déduit par le traitement du langage naturel (NLP) d’une rubrique.

Outre la pertinence du contenu, les algorithmes de notation prennent en compte les activités des membres, telles que le vote et le pourcentage de réponses. Bien que le score de base les inclut quantitativement, le score avancé les utilise algorithmiquement.

Par conséquent, le moteur de notation avancé nécessite suffisamment de données pour que l’analyse soit significative. Le seuil de réussite pour devenir un expert est constamment réévalué à mesure que l’algorithme s’ajuste continuellement au volume et à la qualité du contenu créé. Il y a aussi un concept de *désintégration *des postes plus anciens d&#39;un membre. Si un membre expert cesse de participer à l&#39;objet sur lequel il a acquis le statut d&#39;expert, à un moment déterminé (voir configuration [du moteur de](#configurable-scoring-engine)notation), il pourrait perdre son statut d&#39;expert.

La configuration d’un score avancé est pratiquement identique à celle d’un score de base :

* les règles de notation et de badge de base et avancées sont [appliquées au contenu](/help/communities/implementing-scoring.md#apply-rules-to-content) de la même manière.

   * des règles de notation et de badge de base et avancées peuvent être appliquées au même contenu

* [l’activation de badges pour les composants](/help/communities/implementing-scoring.md#enable-badges-for-component) est générique

Les différences dans la configuration des règles de notation et de badge sont les suivantes :

* moteur de notation avancé configurable
* règles de notation avancées :

   * scoreType défini sur &quot;advanced&quot;
   * nécessite des mots-clés

* règles de badge avancées :

   * badgingType défini sur &quot;advanced&quot;
   * badgingLevels défini sur le nombre de niveaux d&#39;experts à attribuer
   * nécessite un tableau badgingPaths de badges au lieu des points de mappage des tableaux de seuils aux badges

>[!NOTE]
>
>Pour utiliser des fonctionnalités avancées de notation et de badge, installez le package [d’identification des](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/social/cq-social-expert-identification-pkg)experts.

## Moteur de score configurable {#configurable-scoring-engine}

Le moteur de notation avancé fournit une configuration OSGi avec des paramètres qui affectent l’algorithme de notation avancé.

![chlimage_1-139](assets/chlimage_1-139.png)

* **pondérations** Pour une rubrique, spécifiez le verbe qui doit avoir la priorité la plus élevée lors du calcul du score. Une ou plusieurs rubriques peuvent être entrées, mais limitées à **un verbe par rubrique**. Voir [Rubriques et verbes](/help/communities/implementing-scoring.md#topics-and-verbs).
Saisi comme `topic,verb` avec la virgule d’échappement. Par exemple :
   `/social/forum/hbs/social/forum\,ADD`
La valeur par défaut est le verbe ADD pour les composants QnA et de forum.

* **plage**de notation La plage des scores avancés est définie par cette valeur (note maximale possible) et par 0 (note minimale possible).
La valeur par défaut est 100, de sorte que la plage de notation soit comprise entre 0 et 100.

* **intervalle**de désintégration d&#39;entité Ce paramètre représente le nombre d&#39;heures après lesquelles tous les scores d&#39;entité sont décalés. Ceci est nécessaire pour ne plus inclure de contenu ancien dans les scores d’un site communautaire.
La valeur par défaut est de 2 16 000 heures (~24 ans).

* **score de croissance**Cette valeur indique le score entre 0 et la plage de score, au-delà de laquelle la croissance ralentit pour limiter le nombre d&#39;experts.
La valeur par défaut est 50.

## Règles de score avancées {#advanced-scoring-rules}

Dans le score de base, la quantité nécessaire pour gagner un badge est connue.

Dans le cadre d’un score avancé, la quantité nécessaire est constamment ajustée en fonction de la quantité de données de qualité au sein du système. Le score est calculé en permanence de la même manière qu’une courbe en cloche.

Si un membre a obtenu un badge d&#39;expert sur un sujet qui n&#39;est plus actif, il est possible qu&#39;il perde son badge à cause de la carie au fil du temps.

### scoringType {#scoringtype}

Une règle d’évaluation est un ensemble de sous-règles d’évaluation, chacune d’elles déclarant la règle `scoringType`.

Pour appeler le moteur de notation avancé, `scoringType`vous devez définir `advanced`.

Voir Sous-règles [de score](/help/communities/implementing-scoring.md#scoring-sub-rules).

![chlimage_1-140](assets/chlimage_1-140.png)

### Stopwords {#stopwords}

Le package d’évaluation avancé installe un dossier de configuration contenant un fichier de mots-clés :

* /etc/community/score/configuration/stopwords

L’algorithme de notation avancé utilise la liste des mots contenus dans le fichier de mots-clés pour identifier les mots anglais courants qui sont ignorés pendant le traitement du contenu.

On ne s&#39;attend pas à ce que ce fichier soit modifié.

Si le fichier de mots-clés est manquant, le moteur de notation avancé renvoie une erreur.

## Règles de badge avancées {#advanced-badging-rules}

Les propriétés avancées des règles de mise en badge diffèrent des propriétés [de](/help/communities/implementing-scoring.md#badging-rules)base des règles de mise en badge.

Au lieu d’associer des points à une image d’insigne, il suffit d’identifier le nombre d’experts autorisés et l’image d’insigne à attribuer.

![chlimage_1-141](assets/chlimage_1-141.png)

<table>
 <tbody>
  <tr>
   <th>Propriétés</th>
   <th>Type</th>
   <th>Description de la valeur</th>
  </tr>
  <tr>
   <td>badgingPath</td>
   <td>Chaîne[]</td>
   <td><em>(obligatoire)</em> Chaîne multi-valeurs d’images de badge jusqu’au nombre de niveaux de badge. Les chemins d'image du badge doivent être triés afin que le premier soit attribué au plus haut expert. S'il y a moins de badges que ceux indiqués par badgingLevels, le dernier badge de la baie remplit le reste de la baie.  Exemple d’entrée :<br /> <code>/etc/community/badging/images/expert-badge/jcr:content/expert.png</code></td>
  </tr>
  <tr>
   <td>badgingLevels</td>
   <td>Long</td>
   <td><em>(facultatif)</em> Indique les niveaux d’expertise à attribuer. Par exemple, s’il doit y avoir un <code>expert </code>et un <code>almost expert</code> (deux badges), la valeur doit être définie sur 2. Le badgingLevel doit correspondre au nombre d’images de badge liées à un expert répertoriées pour la propriété badgingPath. La valeur par défaut est 1.</td>
  </tr>
  <tr>
   <td>badgingType</td>
   <td>Chaîne</td>
   <td><em>(obligatoire)</em> Identifie le moteur de notation comme étant "de base" ou "avancé". Défini sur "advanced", sinon la valeur par défaut est "basic".</td>
  </tr>
  <tr>
   <td>scoringRules</td>
   <td>Chaîne[]</td>
   <td><em>(Facultatif)</em> Chaîne à plusieurs valeurs qui limite la règle de badge aux événements de notation identifiés par les règles de notation répertoriées.<br /><br /> Exemple d’entrée : La valeur <code>/etc/community/scoring/rules/adv-comments-scoring</code><br /> par défaut n’est pas une restriction.</td>
  </tr>
 </tbody>
</table>

## Règles et badge inclus {#included-rules-and-badge}

### Badge inclus {#included-badge}

Cette version bêta comprend un badge d’expert basé sur la récompense :

* expert/etc/community/badging/images/expert-badge/jcr:content/expert.png

![chlimage_1-142](assets/chlimage_1-142.png)

Pour que le badge d’expert s’affiche comme une récompense pour l’activité, assurez-vous que :

* `badges` sont activées pour la fonctionnalité, comme un forum ou un composant QnA
* les règles avancées de notation et de badge sont appliquées à la page (ou ancêtre) sur laquelle le composant est placé.

Consultez les informations de base pour :

* [activation du badge pour un composant](/help/communities/implementing-scoring.md#enableforcomponent)
* [application de règles](/help/communities/implementing-scoring.md#applytopage)

### Règles et sous-règles de score incluses {#included-scoring-rules-and-sub-rules}

La version bêta comprend deux règles de notation avancées pour la fonction [de](/help/communities/functions.md#forum-function) forum (une pour le forum et les composants de commentaires de la fonctionnalité de forum) :

1. /etc/community/score/Rules/relief-commentaires-score

   * sous-règles[] =/etc/communauté/score/règles/sous-règles/sous-règles/avancé-commentaires-règle/etc/communauté/score/règles/sous-règles/avancé-droit-de-vote-règle-propriétaire/etc/communauté/notation/règles/sous-règles/avancé-règle-de-vote

1. /etc/community/score/Rules/relief-forums-score

   * sous-règles[] =/etc/community/scoring/Rules/sub-rule/puisque-forums-rule/etc/community/scoring/rule/sub-rule/ISF-Commentaire-rule/etc/community/scoring/rule/sub-rule/suite-règles/suite-avancée-vote-règle-propriétaire

**Remarque:**

* les deux `rules`et `sub-rules` noeuds sont de type cq:Page

* `subRules`est un attribut de type String[] sur le `jcr:content` noeud de la règle

* `sub-rules` peut être partagée entre différentes règles de notation
* `rules`doit être situé dans un emplacement de référentiel avec une autorisation de lecture pour tout le monde

   * les noms de règle doivent être uniques, quel que soit l’emplacement

### Règles de badge incluses {#included-badging-rules}

Cette version comprend deux règles de mise en badge avancées qui correspondent aux règles [de notation des commentaires et des forums](#included-scoring-rules-and-sub-rules)avancés.

* /etc/community/badging/Rules/relief-comments-badging
* /etc/community/badging/Rules/relief-forums-badging

**Remarque:**

* `rules` les noeuds sont de type cq:Page
* `rules`doit être situé dans un emplacement de référentiel avec une autorisation de lecture pour tout le monde

   * les noms de règle doivent être uniques, quel que soit l’emplacement

