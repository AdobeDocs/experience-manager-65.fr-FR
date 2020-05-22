---
title: Infrastructure de balisage AEM
seo-title: Infrastructure de balisage AEM
description: Balisage de contenu et utilisation de l’infrastructure de balisage AEM
seo-description: Balisage de contenu et utilisation de l’infrastructure de balisage AEM
uuid: f80a2cb1-359f-41dd-a70b-626d92cc3d4c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: f69db472-9f5c-4c0d-9292-2920ef69feeb
docset: aem65
translation-type: tm+mt
source-git-commit: cef5251d6bd72a6fd352f18e31d3f9d787e4320e
workflow-type: tm+mt
source-wordcount: '1906'
ht-degree: 52%

---


# Infrastructure de balisage AEM {#aem-tagging-framework}

Pour baliser le contenu et utiliser l’infrastructure de balisage AEM, procédez comme suit :

* La balise doit exister en tant que nœud du type ` [cq:Tag](#tags-cq-tag-node-type)` sous le [nœud racine de taxonomie](#taxonomy-root-node).

* Le type du nœud de contenu balisé doit inclure le mixin [`cq:Taggable`](#taggable-content-cq-taggable-mixin).
* The [TagID](#tagid) is added to the content node&#39;s [ `cq:tags`](#tagged-content-cq-tags-property) property and resolves to a node of type ` [cq:Tag](#tags-cq-tag-node-type)`

## Balises : type de nœud cq:Tag  {#tags-cq-tag-node-type}

The declaration of a tag is captured in the repository in a node of type `cq:Tag.`

Une balise peut être constituée d’un simple mot (sky, par exemple) ou représenter une taxonomie hiérarchique (par exemple, fruit/apple, c’est-à-dire la catégorie générique et le fruit).

Les balises sont identifiées par un identifiant unique.

Une balise comprend des méta-informations facultatives, telles qu’un titre, des titres localisés et une description. Le titre doit être affiché dans les interfaces utilisateur au lieu de l’ID de balise, le cas échéant.

La structure de balisage offre également la possibilité de contraindre les auteurs et les visiteurs du site à n’utiliser que des balises prédéfinies spécifiques.

### Caractéristiques de la balise {#tag-characteristics}

* node type is `cq:Tag`
* node name is a component of the ` [TagID](#tagid)`
* the ` [TagID](#tagid)` always includes a [namespace](#tag-namespace)

* optional `jcr:title` property (the Title to display in the UI)

* propriété facultative `jcr:description`

* Lorsqu’elle contient des nœuds enfants, la balise est qualifiée de [balise conteneur](#container-tags).
* Elle est stockée dans le référentiel, sous un chemin de base appelé [nœud racine de taxonomie](#taxonomy-root-node).

### ID de balise {#tagid}

Un ID de balise identifie un chemin d’accès qui est résolu sur un nœud de balise dans le référentiel.

Typically, the TagID is a shorthand TagID starting with the namespace or it can be an absolute TagID starting from the [taxonomy root node](#taxonomy-root-node).

Lorsque le contenu est balisé, la propriété` [cq:tags](#tagged-content-cq-tags-property)` est ajoutée, le cas échéant, au nœud de contenu et l’ID de balise est ajouté à la valeur de tableau String de la propriété.

L’ID de balise se compose d’un [espace de noms](#tag-namespace), suivi de l’ID de balise local. Les [balises conteneurs](#container-tags) contiennent des sous-balises qui représentent un ordre hiérarchique dans la taxonomie. Les sous-balises peuvent être utilisées pour référencer des balises comme n’importe quel ID de balise local. Par exemple, le balisage du contenu avec &quot;fruit&quot; est autorisé, même s’il s’agit d’une balise conteneur avec des sous-balises, telles que &quot;fruit/pomme&quot; et &quot;fruit/banane&quot;.

### Nœud racine de taxonomie {#taxonomy-root-node}

Le nœud racine de taxonomie est le chemin d’accès de base pour toutes les balises du référentiel. Le nœud racine de taxonomie ne peut *pas* être un nœud de type `  cq   :Tag`.

In AEM, the base path is `/content/  cq   :tags` and the root node is of type `  cq   :Folder`.

### Espace de noms des balises {#tag-namespace}

Les espaces de noms permettent de regrouper des éléments. Le cas d’utilisation le plus courant consiste à disposer d’un espace de nommage par (site Web) site (par exemple public, interne et portail) ou par application plus large (par exemple, WCM, Assets, Communities), mais les espaces de nommage peuvent être utilisés pour divers autres besoins. Les espaces de noms sont utilisés dans l’interface utilisateur pour n’afficher que le sous-ensemble de balises (c’est-à-dire les balises d’un espace de noms donné) applicable au contenu actuel.

L’espace de noms de la balise est le premier niveau de la sous-arborescence de taxonomie, à savoir le nœud situé juste en dessous du [nœud racine de taxonomie](#taxonomy-root-node). A namespace is a node of type `cq:Tag` whose parent is not a `cq:Tag`node type.

Toutes les balises possèdent un espace de noms. Si aucun espace de nommage n’est spécifié, la balise est affectée à l’espace de nommage par défaut, qui est TagID `default` (le titre est `Standard Tags),`celui-ci). `/content/cq:tags/default.`

### Balises conteneurs {#container-tags}

Une balise conteneur est un nœud de type `cq:Tag` contenant le nombre et le type des nœuds enfants, ce qui permet d’enrichir le modèle de balise avec des métadonnées personnalisées.

En outre, les balises conteneurs (ou super-balises) d’une taxonomie font office de sous-cumul de toutes les sous-balises. Par exemple, le contenu balisé avec « fruit/apple » est considéré comme étant également balisé avec « fruit ». Dès lors, une recherche de contenu balisé simplement avec « fruit » renverra également le contenu balisé avec « fruit/apple ».

### Résolution d’ID de balise {#resolving-tagids}

Si l’ID de balise contient le signe deux-points (« : »), celui-ci sépare l’espace de noms de la balise ou de la sous-taxonomie, qui sont alors séparés par des barres obliques (« / »). En l’absence de signe deux-points dans l’ID de balise, l’espace de noms par défaut est impliqué.

L’emplacement standard et unique des balises est inférieur à /content/cq:tags.

Les balises référençant des chemins ou chemins non existants qui ne pointent pas vers un noeud cq:Tag sont considérées comme non valides et sont ignorées.

Le tableau ci-dessous présente quelques exemples d’ID de balise, les éléments associés et la manière dont l’ID de balise est résolu sur un chemin d’accès absolu dans le référentiel :

Le tableau suivant présente quelques exemples d’ID de balise, leurs éléments et la manière dont l’ID de balise se résout en chemin absolu dans le référentiel :
Le tableau suivant présente quelques exemples d’ID de balise, leurs éléments et la manière dont l’ID de balise se résout en chemin absolu dans le référentiel :

<table>
 <tbody>
  <tr>
   <td><strong>ID de balise<br /> </strong></td>
   <td><strong>Espace de noms</strong></td>
   <td><strong>ID local</strong></td>
   <td><strong>Balise(s) de Conteneur</strong></td>
   <td><strong>Balise de feuille</strong></td>
   <td><strong>Chemin d’accès absolu à la balise Repository<br /></strong></td>
  </tr>
  <tr>
   <td>barrage:fruit/pomme/feu</td>
   <td>barrage</td>
   <td>fruit/pomme/brasé</td>
   <td>fruit, pomme</td>
   <td>brassard</td>
   <td>/content/cq:tags/dam/fruit/apple/braeburn</td>
  </tr>
  <tr>
   <td>couleur/rouge</td>
   <td>default</td>
   <td>couleur/rouge</td>
   <td>couleur</td>
   <td>rouge</td>
   <td>/content/cq:tags/default/color/red</td>
  </tr>
  <tr>
   <td>sky</td>
   <td>default</td>
   <td>sky</td>
   <td>(none)</td>
   <td>sky</td>
   <td>/content/cq:tags/default/sky</td>
  </tr>
  <tr>
   <td>barrage :</td>
   <td>barrage</td>
   <td>(none)</td>
   <td>(none)</td>
   <td>(aucun, l'espace de nommage)</td>
   <td>/content/cq:tags/dam</td>
  </tr>
  <tr>
   <td>/content/cq:tags/catégorie/car</td>
   <td>catégorie</td>
   <td>voiture</td>
   <td>voiture</td>
   <td>voiture</td>
   <td>/content/cq:tags/catégorie/car</td>
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

* Allowing the `tag-administrators` group/role write access to all namespaces (add/modify under `/content/cq:tags`). Ce groupe est fourni en standard avec AEM.

* Accorder aux utilisateurs/auteurs l’accès en lecture à tous les espaces de noms qu’ils doivent être autorisés à lire (presque tous).
* Allowing users/authors write access to those namespaces where tags should be freely definable by users/authors (add_node under `/content/cq:tags/some_namespace`)

## Contenu pouvant être balisé : cq:Taggable Mixin {#taggable-content-cq-taggable-mixin}

In order for application developers to attach tagging to a content type, the node&#39;s registration ([CND](https://jackrabbit.apache.org/node-type-notation.html)) must include the `cq:Taggable` mixin or the `cq:OwnerTaggable` mixin.

Le mixin `cq:OwnerTaggable`, qui hérite de `cq:Taggable`, sert à indiquer que le contenu peut être classé par propriétaire/auteur. In AEM, it is only an attribute of the `cq:PageContent` node. The `cq:OwnerTaggable` mixin is not required by the tagging framework.

>[!NOTE]
>
>Il est recommandé de n’activer les balises que sur le nœud de niveau supérieur d’un élément de contenu agrégé (ou sur son nœud jcr:content). Voici quelques exemples :
>
>* pages ( `cq:Page`) where the `jcr:content`node is of type `cq:PageContent` which includes the `cq:Taggable` mixin.
   >
   >
* assets ( `cq:Asset`) where the `jcr:content/metadata` node always has the `cq:Taggable` mixin.
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

La propriété `cq:tags` est une table de chaînes utilisée pour stocker un ou plusieurs ID de balise lorsque les auteurs ou les visiteurs du site les appliquent au contenu. The property only has meaning when added to a node which is defined with the `[cq:Taggable](#taggable-content-cq-taggable-mixin)` mixin.

>[!NOTE]
>
>Pour tirer parti de la fonctionnalité de balisage d’AEM, les applications personnalisées ne doivent pas définir de propriétés de balise autres que `cq:tags`.

## Déplacement et fusion de balises {#moving-and-merging-tags}

Vous trouverez, ci-après, la description des effets dans le référentiel lors du déplacement ou de la fusion de balises à l’aide de la [console de balisage](/help/sites-administering/tags.md) :

* When a tag A is moved or merged into tag B under `/content/cq:tags`:

   * tag A is not deleted and gets a `cq:movedTo` property.
   * La balise B est créée (en cas de déplacement) et reçoit une propriété `cq:backlinks`.

* `cq:movedTo` pointe vers la balise B. Cette propriété signifie que la balise A a été déplacée ou fusionnée dans la balise B. Le déplacement de la balise B mettra cette propriété à jour en conséquence. La balise A est donc masquée et elle n’est conservée dans le référentiel que pour résoudre les ID de balise situés dans les nœuds de contenu pointant vers la balise A. Le nettoyeur de mémoire de balise supprime des balises telles que la balise A dès que plus aucun nœud de contenu ne pointe vers elles.
A special value for the `cq:movedTo` property is `nirvana`: it is applied when the tag is deleted but cannot be removed from the repository because there are subtags with a `cq:movedTo` that must be kept.

   >[!NOTE]
   >
   >La `cq:movedTo` propriété n’est ajoutée à la balise déplacée ou fusionnée que si l’une de ces conditions est remplie :
   > 1. La balise est utilisée dans le contenu (c&#39;est-à-dire qu&#39;elle contient une référence) OU
   > 1. La balise a des enfants qui ont déjà été déplacés.


* La propriété `cq:backlinks` conserve les références dans l’autre sens ; en d’autres termes, elle conserve la liste de toutes les balises qui ont été déplacées vers la balise B ou fusionnées avec celle-ci. Cela est requis essentiellement pour conserver les propriétés `cq:movedTo` jusqu’à la date de déplacement/fusion/suppression de la balise B ou jusqu’à ce que cette balise soit activée, auquel cas toutes ses balises de lien retour doivent également être activées.

   >[!NOTE]
   >
   >La `cq:backlinks` propriété n’est ajoutée à la balise déplacée ou fusionnée que si l’une de ces conditions est remplie :
   >
   > 1. La balise est utilisée dans le contenu (c’est-à-dire qu’elle contient une référence) OU >
   > 1. La balise a des enfants qui ont déjà été déplacés.


* La lecture d’une propriété `cq:tags` d’un nœud de contenu implique la résolution suivante :

   1. If there is no match under `/content/cq:tags`, no tag is returned.
   1. Si la propriété `cq:movedTo` est définie pour la balise, l’ID de balise référencé est suivi.
 Cette étape est répétée aussi longtemps que la balise suivie contient la propriété `cq:movedTo`.

   1. Si la balise suivie n’est pas associée à une propriété `cq:movedTo`, elle est lue.

* Pour publier la modification lorsqu’une balise a été déplacée ou fusionnée, le nœud `cq:Tag` et tous ses liens retour doivent être répliqués ; cela est exécuté automatiquement lorsque la balise est activée dans la console d’administration des balises.

* Les mises à jour ultérieures apportées à la propriété `cq:tags` de la page nettoient automatiquement les « anciennes » références. Cette opération est déclenchée, car la résolution d’une balise déplacée via l’API renvoie la balise de destination, fournissant ainsi l’ID de balise de destination.

## Migration des balises {#tags-migration}

Les balises Experience Manager 6.4 et ultérieures sont stockées sous `/content/cq:tags`, qui étaient précédemment stockées sous `/etc/tags`. Cependant, dans les scénarios où Adobe Experience Manager a été mis à niveau à partir de la version précédente, les balises sont toujours présentes sous l’ancien emplacement `/etc/tags`. Dans les systèmes mis à niveau, les balises doivent être migrées sous `/content/cq:tags`.

> [!NOTE]
> Dans Propriétés de page de la page des balises, il est conseillé d’utiliser l’ID de balise (`geometrixx-outdoors:activity/biking`) plutôt que de coder en dur le chemin de base de la balise (par exemple, `/etc/tags/geometrixx-outdoors/activity/biking`).
> Pour les balises de liste, `com.day.cq.tagging.servlets.TagListServlet` vous pouvez les utiliser.

> [!NOTE]
> Il est conseillé d’utiliser l’API du gestionnaire de balises en tant que ressource.

### Si l’instance AEM mise à niveau prend en charge l’API TagManager {#upgraded-instance-support-tagmanager-api}

1. En début de composant, l’API TagManager détecte s’il s’agit d’une instance AEM mise à niveau. Dans le système mis à niveau, les balises sont stockées sous `/etc/tags`.

1. L’API TagManager s’exécute ensuite en mode de compatibilité descendante, ce qui signifie que l’API utilise `/etc/tags` le chemin de base. Dans le cas contraire, il utilise un nouvel emplacement `/content/cq:tags`.

1. Mettez à jour l’emplacement des balises.

1. Après la migration des balises vers le nouvel emplacement, exécutez le script suivant :

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

Le script récupère toutes les balises qui ont `/etc/tags` la valeur de `cq:movedTo/cq:backLinks` la propriété. Il effectue ensuite une itération dans l’ensemble de résultats récupéré et résout les valeurs `cq:movedTo` et les `cq:backlinks` propriétés en `/content/cq:tags` chemins d’accès (dans le cas où `/etc/tags` la valeur est détectée).

### Si l’instance AEM mise à niveau s’exécute sur l’interface utilisateur classique {#upgraded-instance-runs-classic-ui}

> [!NOTE]
> L’interface utilisateur classique n’est pas compatible avec zéro temps d’arrêt et ne prend pas en charge le nouveau chemin de base des balises. Si vous souhaitez utiliser une interface utilisateur classique qui ne doit pas `/etc/tags` être créée, suivie du redémarrage du `cq-tagging` composant.


Dans le cas d’instances AEM mises à niveau prises en charge par l’API TagManager et s’exécutant dans l’interface utilisateur classique :

1. Une fois que les références à l’ancien chemin de base de balises `/etc/tags` sont remplacées par tagId ou un nouvel emplacement de balise `/content/cq:tags`, vous pouvez migrer les balises vers le nouvel emplacement `/content/cq:tags` dans CRX, suivi du redémarrage du composant.

1. Après la migration des balises vers le nouvel emplacement, exécutez le script mentionné ci-dessus.
