---
title: Cadre de balisage AEM
seo-title: AEM Tagging Framework
description: Balisage de contenu et utilisation du cadre de balisage AEM
seo-description: Tag content and leverage the AEM Tagging infrastructure
uuid: f80a2cb1-359f-41dd-a70b-626d92cc3d4c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: f69db472-9f5c-4c0d-9292-2920ef69feeb
docset: aem65
feature: Tagging
exl-id: 53a37449-ef87-4fa6-82de-88fdc24cf988
source-git-commit: efb4f9f8a97baf8d3d02160226e4f4d3f8f64c89
workflow-type: ht
source-wordcount: '1883'
ht-degree: 100%

---

# Framework de balisage AEM {#aem-tagging-framework}

Pour baliser le contenu et utiliser le framework de balisage AEM, procédez comme suit :

* La balise doit exister en tant que nœud du type ` [cq:Tag](#tags-cq-tag-node-type)` sous le [nœud racine de taxonomie](#taxonomy-root-node).

* Le type du nœud de contenu balisé doit inclure le mixin [`cq:Taggable`](#taggable-content-cq-taggable-mixin).
* L’[ID de balise](#tagid) est ajouté à la propriété [`cq:tags`](#tagged-content-cq-tags-property) du nœud de contenu et est résolu sur un nœud de type ` [cq:Tag](#tags-cq-tag-node-type)`.

## Balises : type de nœud cq:Tag  {#tags-cq-tag-node-type}

La déclaration d’une balise est capturée dans le référentiel dans un nœud de type `cq:Tag.`.

Une balise peut être constituée d’un simple mot (sky, par exemple) ou représenter une taxonomie hiérarchique (par exemple, fruit/apple, c’est-à-dire la catégorie générique et le fruit).

Les balises sont identifiées par un identifiant unique.

Une balise comprend des méta-informations facultatives, telles qu’un titre, des titres localisés et une description. Le titre doit être affiché dans les interfaces utilisateur au lieu de l’ID de balise, le cas échéant.

Le framework de balisage offre également la possibilité de contraindre les auteurs et les visiteurs du site à n’utiliser que des balises prédéfinies spécifiques.

### Caractéristiques de la balise {#tag-characteristics}

* Le type de nœud est `cq:Tag`.
* Le nom du nœud est un composant de ` [TagID](#tagid)`.
* Le ` [TagID](#tagid)` contient toujours un [espace de noms](#tag-namespace).

* Propriété `jcr:title` facultative (Titre à afficher dans l’interface utilisateur).

* propriété `jcr:description` facultative

* Lorsqu’elle contient des nœuds enfants, la balise est qualifiée de [balise conteneur](#container-tags).
* Elle est stockée dans le référentiel, sous un chemin de base appelé [nœud racine de taxonomie](#taxonomy-root-node).

### TagID (ID de balise) {#tagid}

Un ID de balise identifie un chemin d’accès qui est résolu sur un nœud de balise dans le référentiel.

En règle générale, l’ID de balise est un identifiant abrégé commençant par l’espace de noms ; il peut également s’agir d’un ID de balise absolu commençant au niveau du [nœud racine de taxonomie](#taxonomy-root-node).

Lorsque le contenu est balisé, la propriété ` [cq:tags](#tagged-content-cq-tags-property)` est ajoutée, si elle n’existe pas déjà, au nœud de contenu et l’ID de balise est ajouté à la valeur de tableau String de la propriété.

L’ID de balise se compose d’un [espace de noms](#tag-namespace), suivi de l’ID de balise local. Les [balises conteneurs](#container-tags) contiennent des sous-balises qui représentent un ordre hiérarchique dans la taxonomie. Des sous-balises peuvent être utilisées pour référencer des balises identiques à tout ID de balise local. Par exemple, baliser du contenu avec « fruit » est autorisé, même s’il s’agit d’une balise conteneur avec des sous-balises, comme « fruit/apple » et « fruit/banana ».

### Nœud racine de taxonomie {#taxonomy-root-node}

Le nœud racine de taxonomie est le chemin d’accès de base pour toutes les balises du référentiel. Le nœud racine de taxonomie ne peut *pas* être un nœud de type `  cq   :Tag`.

Dans AEM, le chemin d’accès de base est `/content/  cq   :tags` et le nœud racine est de type `  cq   :Folder`.

### Espace de noms des balises {#tag-namespace}

Les espaces de noms permettent de regrouper des éléments. Le cas d’utilisation le plus courant consiste à disposer d’un espace de noms par site (Web) (par exemple, public, interne ou sur portail) ou par grande application (par exemple la gestion de contenu Web, ou Assets, Communities), mais les espaces de noms peuvent être utilisés pour d’autres besoins. Les espaces de noms sont utilisés dans l’interface utilisateur pour n’afficher que le sous-ensemble de balises (c’est-à-dire les balises d’un espace de noms donné) applicable au contenu actuel.

L’espace de noms de la balise est le premier niveau de la sous-arborescence de taxonomie, à savoir le nœud situé juste en dessous du [nœud racine de taxonomie](#taxonomy-root-node). Un espace de noms est un nœud de type `cq:Tag` dont le parent n’est pas de type `cq:Tag`.

Toutes les balises possèdent un espace de noms. Si aucun espace de noms n’est spécifié, la balise est affectée à l’espace de noms par défaut, qui est l’ID de balise (TagID) par `default` (le titre est `Standard Tags),` ce qui donnera `/content/cq:tags/default.`.

### Balises conteneurs {#container-tags}

Une balise conteneur est un nœud de type `cq:Tag` contenant le nombre et le type des nœuds enfants, ce qui permet d’enrichir le modèle de balise avec des métadonnées personnalisées.

En outre, les balises conteneurs (ou super-balises) d’une taxonomie font office de sous-cumul de toutes les sous-balises. Par exemple, le contenu balisé avec « fruit/apple » est considéré comme étant également balisé avec « fruit ». Dès lors, une recherche de contenu balisé simplement avec « fruit » renverra également le contenu balisé avec « fruit/apple ».

### Résolution d’ID de balise {#resolving-tagids}

Si l’ID de balise contient le signe deux-points (« : »), celui-ci sépare l’espace de noms de la balise ou de la sous-taxonomie, qui sont alors séparés par des barres obliques (« / »). En l’absence de signe deux-points dans l’ID de balise, l’espace de noms par défaut sera utilisé.

L’emplacement standard et unique pour les balises est sous /content/cq:tags.

Les balises qui référencent des chemins d’accès inexistants ou des chemins d’accès qui ne pointent pas vers un nœud cq:Tag sont considérées comme non valides et sont ignorées.

Le tableau ci-dessous présente quelques exemples d’ID de balise, les éléments associés et la manière dont l’ID de balise est résolu sur un chemin d’accès absolu dans le référentiel :

Le tableau ci-dessous présente quelques exemples d’ID de balise, les éléments associés et la manière dont l’ID de balise est résolu sur un chemin d’accès absolu dans le référentiel :

<table>
 <tbody>
  <tr>
   <td><strong>TagID (ID de balise)<br /> </strong></td>
   <td><strong>Espace de noms</strong></td>
   <td><strong>ID local</strong></td>
   <td><strong>Balise(s) conteneur(s)</strong></td>
   <td><strong>Balise feuille</strong></td>
   <td><strong>Chemin d’accès absolu<br /> aux balises du référentiel</strong></td>
  </tr>
  <tr>
   <td>dam:fruit/apple/braeburn</td>
   <td>dam</td>
   <td>fruit/apple/braeburn</td>
   <td>fruit, apple</td>
   <td>braeburn</td>
   <td>/content/cq:tags/dam/fruit/apple/braeburn</td>
  </tr>
  <tr>
   <td>color/red</td>
   <td>par défaut</td>
   <td>color/red</td>
   <td>couleur</td>
   <td>red</td>
   <td>/content/cq:tags/default/color/red</td>
  </tr>
  <tr>
   <td>sky</td>
   <td>par défaut</td>
   <td>sky</td>
   <td>(aucune)</td>
   <td>sky</td>
   <td>/content/cq:tags/default/sky</td>
  </tr>
  <tr>
   <td>dam:</td>
   <td>dam</td>
   <td>(aucune)</td>
   <td>(aucune)</td>
   <td>(aucun, l’espace de noms)</td>
   <td>/content/cq:tags/dam</td>
  </tr>
  <tr>
   <td>/content/cq:tags/category/car</td>
   <td>category</td>
   <td>car</td>
   <td>car</td>
   <td>car</td>
   <td>/content/cq:tags/category/car</td>
  </tr>
 </tbody>
</table>

### Localisation du titre de balise {#localization-of-tag-title}

Lorsque la balise comprend une chaîne de titre facultative (`jcr:title`), il est possible de localiser le titre à afficher en ajoutant la propriété `jcr:title.<locale>`.

Pour plus d’informations, voir

* [Balises dans différentes langues](/help/sites-developing/building.md#tags-in-different-languages). Cette section décrit l’utilisation des API.
* [Gestion des balises dans différentes langues](/help/sites-administering/tags.md#managing-tags-in-different-languages). Cette section décrit l’utilisation de la console de balisage.

### Contrôle d’accès {#access-control}

Les balises existent sous la forme de nœud dans le répertoire sous le [nœud racine de taxonomie](#taxonomy-root-node). Il est possible d’accorder ou de refuser aux auteurs et aux visiteurs du site le droit de créer des balises dans un espace de noms donné en définissant des listes de contrôle d’accès (ACL) appropriées dans le référentiel.

En outre, refuser les autorisations de lecture sur certains espaces de noms et balises détermine la possibilité d’appliquer des balises à du contenu spécifique.

Une pratique habituelle est la suivante :

* Accorder au groupe/rôle `tag-administrators` l’accès en écriture à tous les espaces de noms (add/modify sous `/content/cq:tags`). Ce groupe est fourni en standard avec AEM.

* Accorder aux utilisateurs/auteurs l’accès en lecture à tous les espaces de noms qu’ils doivent être autorisés à lire (presque tous).
* Accorder aux utilisateurs/auteurs l’accès en écriture aux espaces de noms dont ils doivent être en mesure de définir librement les balises (add_node sous `/content/cq:tags/some_namespace`).

## Contenu pouvant être balisé : mixin cq:Taggable {#taggable-content-cq-taggable-mixin}

Pour que les développeurs d’application attachent le balisage à un type de contenu, l’enregistrement du nœud ([CND](https://jackrabbit.apache.org/node-type-notation.html)) doit inclure le mixin `cq:Taggable` ou `cq:OwnerTaggable`.

Le mixin `cq:OwnerTaggable`, qui hérite de `cq:Taggable`, sert à indiquer que le contenu peut être classé par propriétaire/auteur. Dans AEM, il s’agit uniquement d’un attribut du nœud `cq:PageContent`. Le mixin `cq:OwnerTaggable` n’est pas requis par le cadre de balisage.

>[!NOTE]
>
>Il est recommandé de n’activer les balises que sur le nœud de niveau supérieur d’un élément de contenu agrégé (ou sur son nœud jcr:content). Voici quelques exemples :
>
>* Pages (`cq:Page`) sur lesquelles le nœud `jcr:content` est de type `cq:PageContent` ce qui inclut le mixin `cq:Taggable`
>
>* Ressources (`cq:Asset`) dans lesquelles le nœud `jcr:content/metadata` possède toujours le mixin `cq:Taggable`
>


### Notation de type de nœud (CND) {#node-type-notation-cnd}

Les définitions de type de nœud existent dans le référentiel sous la forme de fichiers CND. La notation CND est définie dans le cadre de la documentation JCR [ici](https://jackrabbit.apache.org/node-type-notation.html).

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

La propriété `cq:tags` est une table de chaînes utilisée pour stocker un ou plusieurs ID de balise lorsque les auteurs ou les visiteurs du site les appliquent au contenu. La propriété n’a de sens que lorsqu’elle est ajoutée à un nœud qui est défini avec le mixin `[cq:Taggable](#taggable-content-cq-taggable-mixin)`.

>[!NOTE]
>
>Pour tirer parti de la fonctionnalité de balisage d’AEM, les applications personnalisées ne doivent pas définir de propriétés de balise autres que `cq:tags`.

## Déplacement et fusion de balises {#moving-and-merging-tags}

Vous trouverez, ci-après, la description des effets dans le référentiel lors du déplacement ou de la fusion de balises à l’aide de la [console de balisage](/help/sites-administering/tags.md) :

* Lorsqu’une balise A est déplacée ou fusionnée dans une balise B sous `/content/cq:tags` :

   * La balise A n’est pas supprimée et reçoit une propriété `cq:movedTo`.
   * La balise B est créée (en cas de déplacement) et reçoit une propriété `cq:backlinks`.

* `cq:movedTo` pointe vers la balise B.
Cette propriété signifie que la balise A a été déplacée ou fusionnée dans la balise B. Le déplacement de la balise B va mettre à jour cette propriété en conséquence. La balise A est donc masquée et elle n’est conservée dans le référentiel que pour résoudre les ID de balise situés dans les nœuds de contenu pointant vers la balise A. Le nettoyeur de mémoire de balise supprime des balises telles que la balise A dès que plus aucun nœud de contenu ne pointe vers elles.
Une valeur spéciale pour la propriété `cq:movedTo` est `nirvana` : elle est appliquée lorsque la balise est supprimée. Cependant, elle ne peut pas être supprimée du référentiel, car des sous-balises avec une propriété `cq:movedTo` doivent être conservées.

   >[!NOTE]
   >
   >La propriété `cq:movedTo` n’est ajoutée à la balise déplacée ou fusionnée que si l’une de ces conditions est remplie :
   >
   >1. La balise est utilisée dans le contenu (ce qui signifie qu’elle comporte une référence) OU
   >1. La balise comporte des enfants qui ont déjà été déplacés.


* La propriété `cq:backlinks` conserve les références dans l’autre sens ; en d’autres termes, elle conserve la liste de toutes les balises qui ont été déplacées vers la balise B ou fusionnées avec celle-ci. Cela est requis essentiellement pour conserver les propriétés `cq:movedTo` jusqu’à la date du déplacement, de la fusion ou de la suppression de la balise B ou jusqu’à ce que cette balise soit activée, auquel cas toutes ses balises de lien retour doivent également être activées.

   >[!NOTE]
   >
   >La propriété `cq:backlinks` n’est ajoutée à la balise déplacée ou fusionnée que si l’une de ces conditions est remplie :
   >
   >1. La balise est utilisée dans le contenu (ce qui signifie qu’elle comporte une référence) OU
   >1. La balise comporte des enfants qui ont déjà été déplacés.


* La lecture d’une propriété `cq:tags` d’un nœud de contenu implique la résolution suivante :

   1. S’il n’existe aucune correspondance sous `/content/cq:tags`, aucune balise n’est renvoyée.
   1. Si la propriété `cq:movedTo` est définie pour la balise, l’ID de balise référencé est suivi.
Cette étape est répétée aussi longtemps que la balise suivie contient la propriété `cq:movedTo`.

   1. Si la balise suivie n’est pas associée à une propriété `cq:movedTo`, elle est lue.

* Pour publier la modification lorsqu’une balise a été déplacée ou fusionnée, le nœud `cq:Tag` et tous ses liens retour doivent être répliqués ; cela est exécuté automatiquement lorsque la balise est activée dans la console d’administration des balises.

* Les mises à jour ultérieures apportées à la propriété `cq:tags` de la page nettoient automatiquement les « anciennes » références. Cette opération est déclenchée, car la résolution d’une balise déplacée via l’API renvoie la balise de destination, fournissant ainsi l’ID de balise de destination.

>[!NOTE]
>
>Le déplacement des balises diffère de la migration des balises.

## Migration des balises {#tags-migration}

Les balises Experience Manager 6.4 et ultérieures sont stockées sous `/content/cq:tags`, qui étaient auparavant stockées sous `/etc/tags`. Cependant, dans les cas où Adobe Experience Manager a été mis à niveau à partir de la version précédente, les balises sont toujours présentes sous l’ancien emplacement `/etc/tags`. Dans les systèmes mis à niveau, les balises doivent être migrées sous `/content/cq:tags`.

>[!NOTE]
>
>Dans la page Propriétés de page des balises, il est conseillé d’utiliser l’ID de balise (`geometrixx-outdoors:activity/biking`) au lieu de coder en dur le chemin d’accès de base de la balise (par exemple, `/etc/tags/geometrixx-outdoors/activity/biking`).
>
>Pour répertorier des balises, vous pouvez utiliser `com.day.cq.tagging.servlets.TagListServlet`.

>[!NOTE]
>
>Il est conseillé d’utiliser l’API du gestionnaire de balises comme ressource.

### Si l’instance d’AEM mise à niveau prend en charge l’API TagManager {#upgraded-instance-support-tagmanager-api}

1. Au lancement du composant, l’API TagManager détecte s’il s’agit d’une instance AEM mise à niveau. Dans le système mis à niveau, les balises sont stockées sous `/etc/tags`.

1. L’API TagManager s’exécute ensuite en mode de compatibilité descendante, ce qui signifie que l’API utilise `/etc/tags` comme chemin de base. Si ce n’est pas le cas, il utilise le nouvel emplacement `/content/cq:tags`.

1. Mettez à jour l’emplacement des balises.

1. Après la migration des balises vers le nouvel emplacement, exécutez le script suivant :

```java
import org.apache.sling.api.resource.*
import javax.jcr.*

ResourceResolverFactory resourceResolverFactory = osgi.getService(ResourceResolverFactory.class);
ResourceResolver resolver = resourceResolverFactory.getAdministrativeResourceResolver(null);
Session session = resolver.adaptTo(Session.class);

def queryManager = session.workspace.queryManager;
def statement = "/jcr:root/content/cq:tags//element(*, cq:Tag)[jcr:contains(@cq:movedTo,\'/etc/tags\') or jcr:contains(@cq:backlinks,\'/etc/tags\')]";
def query = queryManager.createQuery(statement, "xpath");

println "query = ${query.statement}\n";

def tags = query.execute().getNodes();


tags.each { node ->
  def tagPath = node.path;
  println "tag = ${tagPath}";

  if(node.hasProperty("cq:movedTo") && node.getProperty("cq:movedTo").getValue().toString().startsWith("/etc/tags"))
    {
     def movedTo = node.getProperty("cq:movedTo").getValue().toString();

     println "cq:movedTo = ${movedTo} \n";

     movedTo = movedTo.replace("/etc/tags","/content/cq:tags");
     node.setProperty("cq:movedTo",movedTo);
     } else if(node.hasProperty("cq:backlinks")){

     String[] backLinks = node.getProperty("cq:backlinks").getValues();
     int count = 0;

     backLinks.each { value ->
             if(value.startsWith("/etc/tags")){
                     println "cq:backlinks = ${value}\n";
                     backLinks[count] = value.replace("/etc/tags","/content/cq:tags");
    }
             count++;
     }

    node.setProperty("cq:backlinks",backLinks);
  }
}
session.save();

println "---------------------------------Success-------------------------------------"
```

Le script récupère toutes les balises qui ont `/etc/tags` comme valeur de `cq:movedTo/cq:backLinks`. Il effectue ensuite une itération sur l’ensemble des résultats récupérés et résout les valeurs des propriétés `cq:movedTo` et `cq:backlinks` vers les chemins `/content/cq:tags` (dans le cas où `/etc/tags` est détecté dans la valeur).

### Si l’instance d’AEM mise à niveau s’exécute sur l’interface utilisateur classique {#upgraded-instance-runs-classic-ui}

>[!NOTE]
>
>L’interface utilisateur classique n’est pas compatible avec zéro temps d’arrêt et ne prend pas en charge le nouveau chemin d’accès à la base de balises. Si vous souhaitez utiliser l’IU classique, vous devez créer `/etc/tags` puis redémarrer le composant `cq-tagging`.

Dans le cas d’instances d’AEM mises à niveau prises en charge par l’API TagManager et s’exécutant dans l’interface utilisateur classique :

1. Une fois que les références à l’ancien chemin d’accès de base des balises `/etc/tags` sont remplacées à l’aide de l’ID de balise ou d’un nouvel emplacement de balise `/content/cq:tags`, vous pouvez migrer les balises vers le nouvel emplacement `/content/cq:tags` dans CRX, puis redémarrer le composant.

1. Après la migration des balises vers le nouvel emplacement, exécutez le script mentionné ci-dessus.
