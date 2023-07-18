---
title: Framework de balisage AEM
description: Balisez le contenu et utilisez l’infrastructure de balisage AEM
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
docset: aem65
feature: Tagging
exl-id: 53a37449-ef87-4fa6-82de-88fdc24cf988
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '1645'
ht-degree: 50%

---


# Framework de balisage AEM {#aem-tagging-framework}

Le balisage permet de catégoriser et d’organiser le contenu. Les balises peuvent être classées par un espace de noms et par une taxonomie. Pour obtenir des informations détaillées sur l’utilisation des balises :

* Voir le document [Utilisation des balises](/help/sites-authoring/tags.md) pour plus d’informations sur le balisage du contenu en tant qu’auteur de contenu.
* Voir le document [Administration des balises](/help/sites-administering/tags.md) du point de vue de l’administrateur sur la création et la gestion des balises, ainsi que sur les balises de contenu qui ont été appliquées.

Cet article se concentre sur la structure sous-jacente qui prend en charge le balisage dans AEM et sur la manière de l’utiliser en tant que développeur.

## Présentation {#introduction}

Pour baliser le contenu et utiliser l’infrastructure de balisage AEM :

* La balise doit exister en tant que nœud du type `[cq:Tag](#tags-cq-tag-node-type)` sous le [nœud racine de taxonomie.](#taxonomy-root-node)

* Le `NodeType` du nœud de contenu balisé doit inclure le mixin [`cq:Taggable`](#taggable-content-cq-taggable-mixin).
* Le [`TagID`](#tagid) est ajouté à la propriété [`cq:tags`](#tagged-content-cq-tags-property) du nœud de contenu et est résolu sur un nœud de type ` [cq:Tag](#tags-cq-tag-node-type)`.

## Balises : type de nœud cq:Tag  {#tags-cq-tag-node-type}

La déclaration d’une balise est capturée dans le référentiel dans un nœud de type `cq:Tag`..

Une balise peut être un mot simple (par exemple, `sky`) ou représentent une taxonomie hiérarchique (par exemple, `fruit/apple`, c’est-à-dire que le `fruit` et plus spécifique `apple`).

Les balises sont identifiées par un ID de balise unique.

Une balise contient des métadonnées facultatives telles qu’un titre, des titres localisés et une description. Le titre doit être affiché dans les interfaces utilisateur au lieu de l’ID de balise, le cas échéant.

Le framework de balisage offre également la possibilité de contraindre les auteurs et les visiteurs du site à n’utiliser que des balises prédéfinies spécifiques.

### Caractéristiques de la balise {#tag-characteristics}

* Le type de noeud est `cq:Tag`n
* Le nom de noeud est un composant de la propriété [TagID](#tagid).
* Le [TagID](#tagid) inclut toujours un [espace de noms.](#tag-namespace)
* Le `jcr:title` (titre à afficher dans l’interface utilisateur) est facultatif.
* La propriété `jcr:description` est facultative.
* Lorsque vous contiennent des noeuds enfants, la balise est appelée [balise conteneur.](#container-tags)
* La balise est stockée dans le référentiel, sous un chemin de base appelé [nœud racine de taxonomie.](#taxonomy-root-node)

Puisque les balises sont simplement des noeuds JCR, les noms de noeud doivent bien sûr respecter les [Convention d’affectation de noms JCR.](naming-conventions.md)

### TagID (ID de balise) {#tagid}

Un ID de balise identifie un chemin d’accès qui est résolu sur un nœud de balise dans le référentiel.

En règle générale, l’ID de balise est un identifiant abrégé commençant par l’espace de noms ; il peut également s’agir d’un ID de balise absolu commençant au niveau du [nœud racine de taxonomie.](#taxonomy-root-node)

Lorsque le contenu est balisé, la propriété `[cq:tags](#tagged-content-cq-tags-property)` est ajoutée, si elle n’existe pas déjà, au nœud de contenu et l’ID de balise est ajouté à la valeur de tableau de la propriété.`String`

L’ID de balise se compose d’un [espace de noms](#tag-namespace), suivi de l’ID de balise local. [Balises de conteneur](#container-tags) comportent des sous-balises qui représentent un ordre hiérarchique dans la taxonomie. Les sous-balises peuvent être utilisées pour référencer des balises comme n’importe quel ID de balise local. Par exemple, pour baliser le contenu avec `fruit` est autorisé, même s’il s’agit d’une balise conteneur comportant des sous-balises, telles que `fruit/apple` et `fruit/banana`.

### Nœud racine de taxonomie {#taxonomy-root-node}

Le nœud racine de taxonomie est le chemin d’accès de base pour toutes les balises du référentiel. Le nœud racine de taxonomie ne peut pas être un nœud de type `cq:Tag`.

Dans AEM, le chemin d’accès de base est `/content/cq:tags` et le nœud racine est de type `cq:Folder`.

### Espace de noms des balises {#tag-namespace}

Les espaces de noms vous permettent de regrouper des éléments. Le cas d’utilisation le plus courant est un espace de noms par site (par exemple, public, interne et portail) ou par application plus grande (par exemple, WCM, Assets, Communities). Mais les espaces de noms peuvent être utilisés pour d’autres besoins. Les espaces de noms sont utilisés dans l’interface utilisateur pour afficher uniquement le sous-ensemble de balises (c’est-à-dire les balises d’un certain espace de noms) qui s’applique au contenu actuel.

L’espace de noms de la balise est le premier niveau de la sous-arborescence de taxonomie, à savoir le nœud situé juste en dessous du [nœud racine de taxonomie](#taxonomy-root-node). Un espace de noms est un nœud de type `cq:Tag` dont le parent n’est pas de type `cq:Tag`.

Toutes les balises possèdent un espace de noms. Si aucun espace de noms n’est spécifié, la balise est affectée à l’espace de noms par défaut, qui est TagID. `default` avec le titre `Standard Tags`, c’est-à-dire `/content/cq:tags/default`.

### Balises conteneurs {#container-tags}

Une balise conteneur est un nœud de type `cq:Tag` contenant le nombre et le type des nœuds enfants, ce qui permet d’enrichir le modèle de balise avec des métadonnées personnalisées.

En outre, les balises conteneur (ou super-balises) d’une taxonomie servent de base à toutes les sous-balises. Par exemple, du contenu balisé avec `fruit/apple` est considéré comme balisé avec `fruit` ainsi que . Autrement dit, la recherche de contenu balisé avec `fruit` trouverait également le contenu balisé avec `fruit/apple`.

### Résolution d’identifiant de balise {#resolving-tagids}

Si l’ID de balise contient un deux-points (`:`), le deux-points sépare l’espace de noms de la balise ou de la sous-taxonomie, qui est séparé par des barres obliques (`/`). Si l’ID de balise ne comporte pas de deux-points, l’espace de noms par défaut est implicite.

`/content/cq:tags` constitue l’emplacement standard des balises, mais aussi le seul.

Balisage faisant référence à des chemins ou chemins non existants qui ne pointent pas vers un `cq:Tag` sont considérés comme non valides et sont ignorés.

Le tableau ci-dessous présente quelques exemples d’ID de balise, les éléments associés et la manière dont l’ID de balise est résolu sur un chemin d’accès absolu dans le référentiel :

| TagID (ID de balise) | Espace de noms | ID local | Balises conteneurs | Balise feuille | Chemin d’accès absolu aux balises du référentiel |
|---|---|---|---|---|---|
| `dam:fruit/apple/braeburn` | `dam` | `fruit/apple/braeburn` | `fruit`, `apple` | `braeburn` | `/content/cq:tags/dam/fruit/apple/braeburn` |
| `color/red` | `default` | `color/red` | `color` | `red` | `/content/cq:tags/default/color/red` |
| `sky` | `default` | `sky` | Aucun | `sky` | `/content/cq:tags/default/sky` |
| `dam:` | `dam` | Aucun | Aucun | Aucun, espace de noms | `/content/cq:tags/dam` |
| `/content/cq:tags/category/car` | `category` | `car` | `car` | `car` | `/content/cq:tags/category/car` |

### Localisation du titre de balise {#localization-of-tag-title}

Lorsque la balise comprend la chaîne de titre facultative ( `jcr:title`), il est possible de localiser le titre à afficher en ajoutant la propriété . `jcr:title.<locale>`.

Pour plus d’informations, consultez les documents suivants :

* [Balises dans différentes langues](/help/sites-developing/building.md#tags-in-different-languages), qui décrit l’utilisation des API
* [Gestion des balises dans différentes langues](/help/sites-administering/tags.md#managing-tags-in-different-languages), qui décrit l’utilisation de la console de balisage

### Contrôle d’accès {#access-control}

Les balises existent sous la forme de nœud dans le répertoire sous le [nœud racine de taxonomie](#taxonomy-root-node). Il est possible d’accorder ou de refuser aux auteurs et aux visiteurs du site le droit de créer des balises dans un espace de noms donné en définissant des listes de contrôle d’accès (ACL) appropriées dans le référentiel.

En outre, le refus d’autorisations de lecture pour certaines balises ou espaces de noms contrôle la possibilité d’appliquer des balises à un contenu spécifique.

Une pratique habituelle est la suivante :

* Accorder au groupe/rôle `tag-administrators` l’accès en écriture à tous les espaces de noms (add/modify sous `/content/cq:tags`). Ce groupe est fourni en standard avec AEM.
* Accorder aux utilisateurs/auteurs l’accès en lecture à tous les espaces de noms qu’ils doivent être autorisés à lire (presque tous).
* Autoriser les utilisateurs/auteurs à écrire l’accès aux espaces de noms où les balises doivent être librement définies par les utilisateurs/auteurs (ajouter un noeud sous `/content/cq:tags/some_namespace`)

## Contenu pouvant être balisé : mixin cq:Taggable {#taggable-content-cq-taggable-mixin}

Pour que les développeurs d’applications joignent un balisage à un type de contenu, l’enregistrement du noeud ([CND](https://jackrabbit.apache.org/jcr/node-type-notation.html)) doit inclure la variable `cq:Taggable` mixin ou le `cq:OwnerTaggable` mixin.

Le mixin `cq:OwnerTaggable`, qui hérite de `cq:Taggable`, sert à indiquer que le contenu peut être classé par propriétaire/auteur. Dans AEM, il s’agit uniquement d’un attribut du nœud `cq:PageContent`. Le mixin `cq:OwnerTaggable` n’est pas requis par le cadre de balisage.

>[!NOTE]
>
>Il est recommandé de n’activer les balises que sur le nœud de niveau supérieur d’un élément de contenu agrégé (ou sur son nœud `jcr:content`). Voici quelques exemples :
>
>* Pages (`cq:Page`) où la variable `jcr:content`Le noeud est de type `cq:PageContent` qui inclut la variable `cq:Taggable` mixin
>* Ressources ( `cq:Asset`) où la variable `jcr:content/metadata` Le noeud a toujours la propriété `cq:Taggable` mixin
>

### Notation de type de nœud (CND) {#node-type-notation-cnd}

Des définitions de type de noeud existent dans le référentiel sous la forme de fichiers CND. La notation CND est définie dans le cadre de la documentation JCR [ici](https://jackrabbit.apache.org/jcr/node-type-notation.html).

Les définitions essentielles relatives aux types de nœud inclus dans AEM sont les suivantes :

```xml
[cq:Tag] > mix:title, nt:base
    orderable
    - * (undefined) multiple
    - * (undefined)
    + * (nt:base) = cq:Tag version

[cq:Taggable]
    mixin
    - cq:tags (string) multiple

[cq:OwnerTaggable] > cq:Taggable
    mixin
```

## Contenu balisé : propriété cq:tags {#tagged-content-cq-tags-property}

Le `cq:tags` est une propriété `String` tableau utilisé pour stocker un ou plusieurs ID de balise lorsqu’ils sont appliqués au contenu par les auteurs ou les visiteurs du site. La propriété n’a de sens que lorsqu’elle est ajoutée à un nœud qui est défini avec le mixin `[cq:Taggable](#taggable-content-cq-taggable-mixin)`.

>[!NOTE]
>
>Pour utiliser AEM fonctionnalité de balisage, les applications développées personnalisées ne doivent pas définir de propriétés de balise autres que `cq:tags`.

## Déplacement et fusion de balises {#moving-and-merging-tags}

Voici une description des effets dans le référentiel lors du déplacement ou de la fusion de balises à l’aide de la variable [console de balisage](/help/sites-administering/tags.md):

* Lorsqu’une balise A est déplacée ou fusionnée dans une balise B sous `/content/cq:tags` :

   * La balise A n’est pas supprimée et reçoit une `cq:movedTo` .
   * La balise B est créée (en cas de déplacement) et reçoit un `cq:backlinks` .

* `cq:movedTo` pointe vers la balise B.

   * Cette propriété signifie que la balise A a été déplacée ou fusionnée dans la balise B. Le déplacement de la balise B met à jour cette propriété en conséquence. La balise A est donc masquée et elle n’est conservée dans le référentiel que pour résoudre les ID de balise situés dans les nœuds de contenu pointant vers la balise A. Le nettoyeur de mémoire de balise supprime des balises telles que la balise A dès que plus aucun nœud de contenu ne pointe vers elles.

   * Une valeur spéciale pour la variable `cq:movedTo` est `nirvana`. Elle est appliquée lorsque la balise est supprimée mais ne peut pas être supprimée du référentiel, car il existe des sous-balises avec une balise `cq:movedTo` qui doit être préservée.

  >[!NOTE]
  >
  >La propriété `cq:movedTo` n’est ajoutée à la balise déplacée ou fusionnée que si l’une de ces conditions est remplie :
  >
  >1. La balise est utilisée dans le contenu (ce qui signifie qu’elle comporte une référence) ou
  >1. La balise comporte des enfants qui ont déjà été déplacés.

* `cq:backlinks` conserve les références dans l’autre direction. En d’autres termes, il conserve une liste de toutes les balises qui ont été déplacées ou fusionnées avec la balise B. Cela est principalement nécessaire pour conserver `cq:movedTo` propriétés mises à jour lorsque la balise B est également déplacée/fusionnée/supprimée ou lorsque la balise B est activée, auquel cas toutes ses balises de lien arrière doivent être activées.

  >[!NOTE]
  >
  >La propriété `cq:backlinks` n’est ajoutée à la balise déplacée ou fusionnée que si l’une de ces conditions est remplie :
  >
  >1. La balise est utilisée dans le contenu (ce qui signifie qu’elle comporte une référence) OU
  >1. La balise comporte des enfants qui ont déjà été déplacés.

* La lecture d’une propriété `cq:tags` d’un nœud de contenu implique la résolution suivante :

   1. S’il n’existe aucune correspondance sous `/content/cq:tags`, aucune balise n’est renvoyée.

   1. Si la propriété `cq:movedTo` est définie pour la balise, l’ID de balise référencé est suivi.

      * Cette étape est répétée aussi longtemps que la balise suivie contient la propriété `cq:movedTo`.

   1. Si la balise suivie n’est pas associée à une propriété `cq:movedTo`, elle est lue.

* Pour publier la modification lorsqu’une balise a été déplacée ou fusionnée, le nœud `cq:Tag` et tous ses liens retours doivent être répliqués. Cette opération est réalisée automatiquement lorsque la balise est activée dans la console d’administration des balises.

* Mises à jour ultérieures du rapport `cq:tags` nettoie automatiquement les anciennes références. Cette opération est déclenchée, car la résolution d’une balise déplacée via l’API renvoie la balise de destination, fournissant ainsi l’ID de balise de destination.

>[!NOTE]
>
>Le déplacement des balises diffère de la migration des balises.

## Migration des balises {#tags-migration}

Depuis Adobe Experience Manager 6.4, les balises sont stockées sous `/content/cq:tags` tandis que les versions précédentes stockaient des balises sous `/etc/tags`.

Chaque fois qu’un système AEM est mis à niveau à partir d’une version antérieure à 6.4, les balises doivent être migrées vers `/content/cq:tags`. Consultez le document [Restructuration des référentiels courants dans AEM 6.5](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#tags) pour plus d’informations.
