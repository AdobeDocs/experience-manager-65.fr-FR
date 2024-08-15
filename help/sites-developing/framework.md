---
title: Framework de balisage AEM
description: Baliser du contenu et utiliser l’infrastructure de balisage AEM
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
docset: aem65
feature: Developing,Tagging
exl-id: 53a37449-ef87-4fa6-82de-88fdc24cf988
solution: Experience Manager, Experience Manager Sites
role: Developer
source-git-commit: f30decf0e32a520dcda04b89c5c1f5b67ab6e028
workflow-type: tm+mt
source-wordcount: '1637'
ht-degree: 99%

---


# Framework de balisage AEM {#aem-tagging-framework}

Le balisage permet de catégoriser et d’organiser le contenu. Les balises peuvent être classées par un espace de noms et par une taxonomie. Pour obtenir des informations détaillées sur l’utilisation des balises :

* Voir le document [Utilisation des balises](/help/sites-authoring/tags.md) pour plus d’informations sur le balisage du contenu en tant qu’auteur ou autrice de contenu.
* Consultez le document [Administration des balises](/help/sites-administering/tags.md) pour savoir comment un administrateur ou une administratrice peut créer et gérer des balises et déterminer à quel contenu elles ont été appliquées.

Cet article se concentre sur le cadre sous-jacent qui prend en charge le balisage dans AEM et explique comment l’utiliser en tant que développeur ou développeuse.

## Présentation {#introduction}

Pour baliser le contenu et utiliser l’infrastructure de balisage AEM, procédez comme suit :

* La balise doit exister en tant que nœud du type `[cq:Tag](#tags-cq-tag-node-type)` sous le [nœud racine de taxonomie.](#taxonomy-root-node)

* Le `NodeType` du nœud de contenu balisé doit inclure le mixin [`cq:Taggable`](#taggable-content-cq-taggable-mixin).
* Le [`TagID`](#tagid) est ajouté à la propriété [`cq:tags`](#tagged-content-cq-tags-property) du nœud de contenu et est résolu sur un nœud de type ` [cq:Tag](#tags-cq-tag-node-type)`.

## Balises : type de nœud cq:Tag  {#tags-cq-tag-node-type}

La déclaration d’une balise est capturée dans le référentiel dans un nœud de type `cq:Tag`.

Une balise peut être constituée d’un simple mot (`sky`, par exemple) ou représenter une taxonomie hiérarchique (`fruit/apple`, par exemple, c’est-à-dire le `fruit` en tant que catégorie générique et la `apple` en étant plus spécifique).

Les balises sont identifiées par un TagID unique.

Une balise comprend des méta-informations facultatives, telles qu’un titre, des titres localisés et une description. Le titre doit être affiché dans les interfaces utilisateur au lieu de l’ID de balise, le cas échéant.

Le framework de balisage offre également la possibilité de contraindre les auteurs et les visiteurs du site à n’utiliser que des balises prédéfinies spécifiques.

### Caractéristiques de la balise {#tag-characteristics}

* Le type de nœud est `cq:Tag`.
* Le nom du nœud est un composant du [TagID](#tagid).
* Le [TagID](#tagid) contient toujours un [espace de noms.](#tag-namespace)
* La propriété `jcr:title` (le titre à afficher dans l’interface utilisateur) est facultative.
* La propriété `jcr:description` est facultative.
* Lorsqu’elle contient des nœuds enfants, la balise est qualifiée de [balise conteneur.](#container-tags)
* La balise est stockée dans le référentiel, sous un chemin de base appelé [nœud racine de taxonomie.](#taxonomy-root-node)

Les balises étant simplement des nœuds JCR, les noms de nœud doivent respecter la [Convention de nommage JCR.](naming-conventions.md)

### TagID (ID de balise) {#tagid}

Un ID de balise identifie un chemin d’accès qui est résolu sur un nœud de balise dans le référentiel.

En règle générale, le TagID est un identifiant abrégé commençant par l’espace de noms ; il peut également s’agir d’un TagID absolu commençant au niveau du [nœud racine de taxonomie](#taxonomy-root-node).

Lorsque le contenu est balisé, la propriété `[cq:tags](#tagged-content-cq-tags-property)` est ajoutée, si elle n’existe pas déjà, au nœud de contenu et le TagID est ajouté à la valeur de tableau `String` de la propriété.

L’ID de balise se compose d’un [espace de noms](#tag-namespace), suivi du TagID local. Les [balises conteneurs](#container-tags) contiennent des sous-balises qui représentent un ordre hiérarchique dans la taxonomie. Des sous-balises peuvent être utilisées pour référencer des balises identiques à tout TagID local. Par exemple, baliser du contenu avec `fruit` est autorisé, même s’il s’agit d’une balise conteneur avec des sous-balises, comme `fruit/apple` et `fruit/banana`.

### Nœud racine de taxonomie {#taxonomy-root-node}

Le nœud racine de taxonomie est le chemin d’accès de base pour toutes les balises du référentiel. Le nœud racine de taxonomie ne peut pas être un nœud de type `cq:Tag`.

Dans AEM, le chemin d’accès de base est `/content/cq:tags` et le nœud racine est de type `cq:Folder`.

### Espace de noms des balises {#tag-namespace}

Les espaces de noms vous permettent de regrouper des éléments. Le cas d’utilisation le plus courant est un espace de noms par site (par exemple, public, interne et portail) ou par application plus grande (par exemple, WCM, Assets, Communities). Mais les espaces de noms peuvent être utilisés pour d’autres besoins. Les espaces de noms sont utilisés dans l’interface utilisateur pour n’afficher que le sous-ensemble de balises (c’est-à-dire les balises d’un espace de noms donné) applicable au contenu actuel.

L’espace de noms de la balise est le premier niveau de la sous-arborescence de taxonomie, à savoir le nœud situé juste en dessous du [nœud racine de taxonomie](#taxonomy-root-node). Un espace de noms est un nœud de type `cq:Tag` dont le parent n’est pas de type `cq:Tag`.

Toutes les balises possèdent un espace de noms. Si aucun espace de noms n’est spécifié, la balise est affectée à l’espace de noms par défaut, qui est l’ID de balise (TagID) par `default` (le titre est `Standard Tags` ce qui donnera `/content/cq:tags/default`).

### Balises conteneurs {#container-tags}

Une balise conteneur est un nœud de type `cq:Tag` contenant le nombre et le type des nœuds enfants, ce qui permet d’enrichir le modèle de balise avec des métadonnées personnalisées.

En outre, les balises conteneurs (ou super-balises) d’une taxonomie servent de sous-combinaison de toutes les sous-balises. Par exemple, du contenu balisé avec `fruit/apple` est considéré comme balisé avec `fruit`, également. Autrement dit, la recherche de contenu balisé avec `fruit` trouve également le contenu balisé avec `fruit/apple`.

### Résolution d’identifiants de balise {#resolving-tagids}

Si l’ID de balise contient le signe deux-points (`:`), celui-ci sépare l’espace de noms de la balise ou de la sous-taxonomie, qui sont alors séparées par des barres obliques (`/`). En l’absence de signe deux-points dans le TagID, l’espace de noms par défaut est sous-entendu.

`/content/cq:tags` constitue l’emplacement standard des balises, mais aussi le seul.

Les balises qui référencent des chemins d’accès inexistants ou qui ne pointent pas vers un nœud `cq:Tag` sont considérées comme non valides et sont ignorées.

Le tableau ci-dessous présente quelques exemples d’ID de balise, les éléments associés et la manière dont l’ID de balise est résolu sur un chemin d’accès absolu dans le référentiel :

| TagID (ID de balise) | Espace de noms | ID local | Balises conteneurs | Balise feuille | Chemin d’accès absolu aux balises du référentiel |
|---|---|---|---|---|---|
| `dam:fruit/apple/braeburn` | `dam` | `fruit/apple/braeburn` | `fruit`, `apple` | `braeburn` | `/content/cq:tags/dam/fruit/apple/braeburn` |
| `color/red` | `default` | `color/red` | `color` | `red` | `/content/cq:tags/default/color/red` |
| `sky` | `default` | `sky` | Aucun | `sky` | `/content/cq:tags/default/sky` |
| `dam:` | `dam` | Aucun | Aucun | Aucun, l’espace de noms | `/content/cq:tags/dam` |
| `/content/cq:tags/category/car` | `category` | `car` | `car` | `car` | `/content/cq:tags/category/car` |

### Localisation du titre de balise {#localization-of-tag-title}

Lorsque la balise comprend une chaîne de titre facultative (`jcr:title`), il est possible de localiser le titre à afficher en ajoutant la propriété `jcr:title.<locale>`.

Pour plus d’informations, voir les documents suivants :

* [Balises dans différentes langues](/help/sites-developing/building.md#tags-in-different-languages), qui décrit l’utilisation des API.
* [Gestion des balises dans différentes langues](/help/sites-administering/tags.md#managing-tags-in-different-languages), qui décrit l’utilisation de la console de balisage.

### Contrôle d’accès {#access-control}

Les balises existent sous la forme de nœud dans le répertoire sous le [nœud racine de taxonomie](#taxonomy-root-node). Il est possible d’accorder ou de refuser aux auteurs et autrices et aux visiteurs et visiteuses du site le droit de créer des balises dans un espace de noms donné en définissant des listes de contrôle d’accès (ACL) appropriées dans le référentiel.

Refuser les autorisations de lecture sur certains espaces de noms et balises détermine la possibilité d’appliquer des balises à du contenu spécifique.

Une pratique habituelle est la suivante :

* Accorder au groupe/rôle `tag-administrators` l’accès en écriture à tous les espaces de noms (add/modify sous `/content/cq:tags`). Ce groupe est fourni en standard avec AEM.
* Accorder aux utilisateurs/auteurs l’accès en lecture à tous les espaces de noms qu’ils doivent être autorisés à lire (presque tous).
* Accorder aux utilisateurs et utilisatrices/auteurs et autrices l’accès en écriture aux espaces de noms dont ils doivent être en mesure de définir librement les balises (add_node sous `/content/cq:tags/some_namespace`).

## Contenu pouvant être balisé : mixin cq:Taggable {#taggable-content-cq-taggable-mixin}

Pour que les développeurs et développeuses d’application associent le balisage à un type de contenu, l’enregistrement du nœud ([CND](https://jackrabbit.apache.org/jcr/node-type-notation.html)) doit inclure le mixin `cq:Taggable` ou `cq:OwnerTaggable`.

Le mixin `cq:OwnerTaggable`, qui hérite de `cq:Taggable`, sert à indiquer que le contenu peut être classé par propriétaire/auteur. Dans AEM, il s’agit uniquement d’un attribut du nœud `cq:PageContent`. Le mixin `cq:OwnerTaggable` n’est pas requis par le cadre de balisage.

>[!NOTE]
>
>Il est recommandé de n’activer les balises que sur le nœud de niveau supérieur d’un élément de contenu agrégé (ou sur son nœud `jcr:content`). Voici quelques exemples :
>
>* Pages (`cq:Page`) sur lesquelles le nœud `jcr:content` est de type `cq:PageContent`, ce qui inclut le mixin `cq:Taggable`.
>* Ressources (`cq:Asset`) dans lesquelles le nœud `jcr:content/metadata` possède toujours le mixin `cq:Taggable`.
>

### Notation de type de nœud (CND) {#node-type-notation-cnd}

Les définitions de type de nœud existent dans le référentiel sous la forme de fichiers CND. La notation CND est définie dans le cadre de la [documentation Jackrabbit](https://jackrabbit.apache.org/jcr/node-type-notation.html).

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

La propriété `cq:tags` est un tableau de `String` utilisé pour stocker un ou plusieurs ID de balise lorsque les auteurs et autrices ou les visiteurs et visiteuses du site les appliquent au contenu. La propriété n’a de sens que lorsqu’elle est ajoutée à un nœud qui est défini avec le mixin `[cq:Taggable](#taggable-content-cq-taggable-mixin)`.

>[!NOTE]
>
>Pour utiliser la fonctionnalité de balisage d’AEM, les applications personnalisées ne doivent pas définir de propriétés de balise autres que `cq:tags`.

## Déplacer et fusionner des balises {#moving-and-merging-tags}

Vous trouverez, ci-après, la description des effets dans le référentiel lors du déplacement ou de la fusion de balises à l’aide de la [console de balisage](/help/sites-administering/tags.md) :

* Lorsqu’une balise A est déplacée ou fusionnée dans une balise B sous `/content/cq:tags` :

   * La balise A n’est pas supprimée et reçoit une propriété `cq:movedTo`.
   * La balise B est créée (dans le cas d’un déplacement) et reçoit une propriété `cq:backlinks`.

* `cq:movedTo` pointe vers la balise B.

   * Cette propriété signifie que la balise A a été déplacée ou fusionnée dans la balise B. Le déplacement de la balise B va mettre à jour cette propriété en conséquence. La balise A est donc masquée et elle n’est conservée dans le référentiel que pour résoudre les ID de balise situés dans les nœuds de contenu pointant vers la balise A. Tag Garbage Collector supprime des balises telles que la balise A dès que plus aucun nœud de contenu ne pointe vers elles.

   * Une valeur spéciale pour la propriété `cq:movedTo` est `nirvana`. Elle est appliquée lorsque la balise est supprimée. Cependant, elle ne peut pas être supprimée du référentiel, car des sous-balises avec une propriété `cq:movedTo` doivent être conservées.

  >[!NOTE]
  >
  >La propriété `cq:movedTo` n’est ajoutée à la balise déplacée ou fusionnée que si l’une de ces conditions est remplie :
  >
  >1. La balise est utilisée dans le contenu (ce qui signifie qu’elle comporte une référence), ou
  >1. La balise comporte des enfants qui ont déjà été déplacés.

* `cq:backlinks` conserve les références dans l’autre direction. En d’autres termes, elle conserve la liste de toutes les balises qui ont été déplacées vers la balise B ou fusionnées avec celle-ci. Cela est requis essentiellement pour conserver les propriétés `cq:movedTo` jusqu’à la date du déplacement, de la fusion ou de la suppression de la balise B ou jusqu’à ce que cette balise soit activée, auquel cas toutes ses balises de lien retour doivent également être activées.

  >[!NOTE]
  >
  >La propriété `cq:backlinks` n’est ajoutée à la balise déplacée ou fusionnée que si l’une de ces conditions est remplie :
  >
  >1. La balise est utilisée dans le contenu (ce qui signifie qu’elle comporte une référence), OU
  >1. La balise comporte des enfants qui ont déjà été déplacés.

* La lecture d’une propriété `cq:tags` d’un nœud de contenu implique la résolution suivante :

   1. S’il n’existe aucune correspondance sous `/content/cq:tags`, aucune balise n’est renvoyée.

   1. Si la propriété `cq:movedTo` est définie pour la balise, l’ID de balise référencé est suivi.

      * Cette étape est répétée aussi longtemps que la balise suivie contient la propriété `cq:movedTo`.

   1. Si la balise suivie n’est pas associée à une propriété `cq:movedTo`, elle est lue.

* Pour publier la modification lorsqu’une balise a été déplacée ou fusionnée, le nœud `cq:Tag` et tous ses liens retours doivent être répliqués. Cette opération est réalisée automatiquement lorsque la balise est activée dans la console d’administration des balises.

* Les mises à jour ultérieures apportées à la propriété `cq:tags` de la page nettoient automatiquement les anciennes références. Cette opération est déclenchée, car la résolution d’une balise déplacée via l’API renvoie la balise de destination, fournissant ainsi l’ID de balise de destination.

>[!NOTE]
>
>Le déplacement des balises diffère de la migration des balises.

## Migration de balises {#tags-migration}

Depuis Adobe Experience Manager 6.4, les balises sont stockées sous `/content/cq:tags` tandis que les versions précédentes stockaient des balises sous `/etc/tags`.

Lorsque vous mettez à niveau un système AEM à partir d’une version antérieure à 6.4, les balises doivent être migrées vers `/content/cq:tags`. Pour plus d’informations, consultez [Restructuration du référentiel commun dans AEM 6.5](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#tags).
