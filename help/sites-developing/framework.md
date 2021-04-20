---
title: Cadre de balisage AEM
seo-title: Cadre de balisage AEM
description: Balisage de contenu et utilisation du cadre de balisage AEM
seo-description: Balisage de contenu et utilisation du cadre de balisage AEM
uuid: f80a2cb1-359f-41dd-a70b-626d92cc3d4c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: f69db472-9f5c-4c0d-9292-2920ef69feeb
docset: aem65
feature: Tagging
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1916'
ht-degree: 60%

---


# Cadre de balisage AEM {#aem-tagging-framework}

Pour baliser le contenu et utiliser le cadre de balisage AEM, procédez comme suit :

* La balise doit exister en tant que nœud du type ` [cq:Tag](#tags-cq-tag-node-type)` sous le [nœud racine de taxonomie](#taxonomy-root-node)

* Le type du nœud de contenu balisé doit inclure le mixin [`cq:Taggable`](#taggable-content-cq-taggable-mixin).
* Le [TagID](#tagid) est ajouté à la propriété [ `cq:tags`](#tagged-content-cq-tags-property) du noeud de contenu et est résolu en un noeud de type ` [cq:Tag](#tags-cq-tag-node-type)`.

## Balises : type de nœud cq:Tag  {#tags-cq-tag-node-type}

La déclaration d’une balise est capturée dans le référentiel dans un nœud de type `cq:Tag.`

Une balise peut être constituée d’un simple mot (sky, par exemple) ou représenter une taxonomie hiérarchique (par exemple, fruit/apple, c’est-à-dire la catégorie générique et le fruit).

Les balises sont identifiées par un identifiant unique.

Une balise comprend des méta-informations facultatives, telles qu’un titre, des titres localisés et une description. Le titre doit être affiché dans les interfaces utilisateur au lieu de l’ID de balise, le cas échéant.

Le cadre de balisage offre également la possibilité de contraindre les auteurs et les visiteurs du site à n’utiliser que des balises prédéfinies spécifiques.

### Caractéristiques de la balise {#tag-characteristics}

* type de noeud `cq:Tag`
* nom de noeud est un composant de ` [TagID](#tagid)`
* ` [TagID](#tagid)` inclut toujours un [espace de nommage](#tag-namespace)

* propriété facultative `jcr:title` (titre à afficher dans l’interface utilisateur)

* propriété facultative `jcr:description`

* Lorsqu’elle contient des nœuds enfants, la balise est qualifiée de [balise conteneur](#container-tags).
* Elle est stockée dans le référentiel, sous un chemin de base appelé [nœud racine de taxonomie](#taxonomy-root-node).

### TagID {#tagid}

Un ID de balise identifie un chemin d’accès qui est résolu sur un nœud de balise dans le référentiel.

En règle générale, TagID est un TagID abrégé commençant par l&#39;espace de nommage ou un TagID absolu commençant par le [noeud racine de taxonomie](#taxonomy-root-node).

Lorsque le contenu est balisé, la propriété` [cq:tags](#tagged-content-cq-tags-property)` est ajoutée, le cas échéant, au nœud de contenu et l’ID de balise est ajouté à la valeur de tableau String de la propriété.

L’ID de balise se compose d’un [espace de noms](#tag-namespace), suivi de l’ID de balise local. Les [balises conteneurs](#container-tags) contiennent des sous-balises qui représentent un ordre hiérarchique dans la taxonomie. Les sous-balises peuvent être utilisées pour référencer des balises comme n’importe quel ID de balise local. Par exemple, le balisage du contenu avec &quot;fruit&quot; est autorisé, même s’il s’agit d’une balise conteneur avec des sous-balises, telles que &quot;fruit/pomme&quot; et &quot;fruit/banane&quot;.

### Nœud racine de taxonomie {#taxonomy-root-node}

Le nœud racine de taxonomie est le chemin d’accès de base pour toutes les balises du référentiel. Le nœud racine de taxonomie ne peut *pas* être un nœud de type `  cq   :Tag`.

Dans AEM, le chemin d’accès de base est `/content/  cq   :tags` et le nœud racine est de type `  cq   :Folder`.

### Espace de noms des balises {#tag-namespace}

Les espaces de noms permettent de regrouper des éléments. Le cas d’utilisation le plus courant consiste à disposer d’un espace de nommage par (site Web) site (par exemple public, interne et portail) ou par application plus large (par exemple, WCM, Assets, Communities), mais les espaces de nommage peuvent être utilisés pour divers autres besoins. Les espaces de noms sont utilisés dans l’interface utilisateur pour n’afficher que le sous-ensemble de balises (c’est-à-dire les balises d’un espace de noms donné) applicable au contenu actuel.

L’espace de noms de la balise est le premier niveau de la sous-arborescence de taxonomie, à savoir le nœud situé juste en dessous du [nœud racine de taxonomie](#taxonomy-root-node).  Un espace de noms est un nœud de type `cq:Tag` dont le parent n’est pas de type `cq:Tag`.

Toutes les balises possèdent un espace de noms. Si aucun espace de nommage n’est spécifié, la balise est affectée à l’espace de nommage par défaut, qui est TagID `default` (le titre est `Standard Tags),`qui est `/content/cq:tags/default.`

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
   <td><strong>TagID<br /> </strong></td>
   <td><strong>Espace de noms</strong></td>
   <td><strong>ID local</strong></td>
   <td><strong>Balise(s) de conteneur</strong></td>
   <td><strong>Balise de feuille</strong></td>
   <td><strong>Repository<br /> Chemin d’accès absolu aux balises</strong></td>
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
   <td>(aucune)</td>
   <td>sky</td>
   <td>/content/cq:tags/default/sky</td>
  </tr>
  <tr>
   <td>barrage :</td>
   <td>barrage</td>
   <td>(aucune)</td>
   <td>(aucune)</td>
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

* Accorder au groupe/rôle `tag-administrators` l’accès en écriture à tous les espaces de noms (add/modify sous `/content/cq:tags`). Ce groupe est fourni en standard avec AEM.

* Accorder aux utilisateurs/auteurs l’accès en lecture à tous les espaces de noms qu’ils doivent être autorisés à lire (presque tous).
* Autoriser les utilisateurs/auteurs à écrire l’accès aux espaces de nommage où les balises doivent être définies librement par les utilisateurs/auteurs (add_node sous `/content/cq:tags/some_namespace`)

## Contenu pouvant être balisé : cq:Taggable Mixin {#taggable-content-cq-taggable-mixin}

Pour que les développeurs d’application attachent le balisage à un type de contenu, l’enregistrement du nœud ([CND](https://jackrabbit.apache.org/node-type-notation.html)) doit inclure le mixin `cq:Taggable` ou `cq:OwnerTaggable`.

Le mixin `cq:OwnerTaggable`, qui hérite de `cq:Taggable`, sert à indiquer que le contenu peut être classé par propriétaire/auteur. Dans AEM, il s’agit uniquement d’un attribut du nœud `cq:PageContent`. Le mixin `cq:OwnerTaggable` n’est pas requis par le cadre de balisage.

>[!NOTE]
>
>Il est recommandé de n’activer les balises que sur le nœud de niveau supérieur d’un élément de contenu agrégé (ou sur son nœud jcr:content). Voici quelques exemples :
>
>* pages ( `cq:Page`) où le noeud `jcr:content`est de type `cq:PageContent` qui inclut le mixin `cq:Taggable`.
   >
   >
* actifs ( `cq:Asset`) où le noeud `jcr:content/metadata` a toujours le mixin `cq:Taggable`.

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

* Lorsqu’une balise A est déplacée ou fusionnée dans la balise B sous `/content/cq:tags` :

   * La balise A n’est pas supprimée et obtient une propriété `cq:movedTo`.
   * La balise B est créée (en cas de déplacement) et reçoit une propriété `cq:backlinks`.

* `cq:movedTo` pointe vers la balise B. Cette propriété signifie que la balise A a été déplacée ou fusionnée dans la balise B. Le déplacement de la balise B mettra cette propriété à jour en conséquence. La balise A est donc masquée et elle n’est conservée dans le référentiel que pour résoudre les ID de balise situés dans les nœuds de contenu pointant vers la balise A. Le nettoyeur de mémoire de balise supprime des balises telles que la balise A dès que plus aucun nœud de contenu ne pointe vers elles.
Une valeur spéciale pour la propriété `cq:movedTo` est `nirvana` : elle est appliquée lorsque la balise est supprimée mais ne peut pas être supprimée du référentiel, car il existe des sous-balises avec `cq:movedTo` qui doivent être conservées.

   >[!NOTE]
   >
   >La propriété `cq:movedTo` n’est ajoutée à la balise déplacée ou fusionnée que si l’une de ces conditions est remplie :
   > 1. La balise est utilisée dans le contenu (c&#39;est-à-dire qu&#39;elle contient une référence) OU
   > 1. La balise a des enfants qui ont déjà été déplacés.


* La propriété `cq:backlinks` conserve les références dans l’autre sens ; en d’autres termes, elle conserve la liste de toutes les balises qui ont été déplacées vers la balise B ou fusionnées avec celle-ci. Cela est requis essentiellement pour conserver les propriétés `cq:movedTo` jusqu’à la date de déplacement/fusion/suppression de la balise B ou jusqu’à ce que cette balise soit activée, auquel cas toutes ses balises de lien retour doivent également être activées.

   >[!NOTE]
   >
   >La propriété `cq:backlinks` n’est ajoutée à la balise déplacée ou fusionnée que si l’une de ces conditions est remplie :
   >
   > 1. La balise est utilisée dans le contenu (c&#39;est-à-dire qu&#39;elle contient une référence) OU    >
   > 1. La balise a des enfants qui ont déjà été déplacés.


* La lecture d’une propriété `cq:tags` d’un nœud de contenu implique la résolution suivante :

   1. S’il n’existe aucune correspondance sous `/content/cq:tags`, aucune balise n’est renvoyée.
   1. Si la propriété `cq:movedTo` est définie pour la balise, l’ID de balise référencé est suivi.
 Cette étape est répétée aussi longtemps que la balise suivie contient la propriété `cq:movedTo`.

   1. Si la balise suivie n’est pas associée à une propriété `cq:movedTo`, elle est lue.

* Pour publier la modification lorsqu’une balise a été déplacée ou fusionnée, le nœud `cq:Tag` et tous ses liens retour doivent être répliqués ; cela est exécuté automatiquement lorsque la balise est activée dans la console d’administration des balises.

* Les mises à jour ultérieures apportées à la propriété `cq:tags` de la page nettoient automatiquement les « anciennes » références. Cette opération est déclenchée, car la résolution d’une balise déplacée via l’API renvoie la balise de destination, fournissant ainsi l’ID de balise de destination.

>[!NOTE]
>
>Le déplacement des balises est différent de la migration des balises.

## Migration des balises {#tags-migration}

Les balises Experience Manager 6.4 et ultérieures sont stockées sous `/content/cq:tags`, qui étaient précédemment stockées sous `/etc/tags`. Cependant, dans les scénarios où Adobe Experience Manager a été mis à niveau à partir de la version précédente, les balises sont toujours présentes sous l’ancien emplacement `/etc/tags`. Dans les systèmes mis à niveau, les balises doivent être migrées sous `/content/cq:tags`.

>[!NOTE]
>
>Dans Propriétés de page de la page des balises, il est conseillé d’utiliser l’ID de balise (`geometrixx-outdoors:activity/biking`) au lieu de coder en dur le chemin de base de la balise (par exemple, `/etc/tags/geometrixx-outdoors/activity/biking`).
>
>Pour les balises de liste, `com.day.cq.tagging.servlets.TagListServlet` peut être utilisé.

>[!NOTE]
>
>Il est conseillé d’utiliser l’API du gestionnaire de balises en tant que ressource.

### Si l’instance AEM mise à niveau prend en charge l’API TagManager {#upgraded-instance-support-tagmanager-api}

1. En début de composant, l’API TagManager détecte s’il s’agit d’une instance AEM mise à niveau. Dans le système mis à niveau, les balises sont stockées sous `/etc/tags`.

1. L’API TagManager s’exécute ensuite en mode de compatibilité descendante, ce qui signifie que l’API utilise `/etc/tags` comme chemin de base. Dans le cas contraire, il utilise le nouvel emplacement `/content/cq:tags`.

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

Le script récupère toutes les balises dont la valeur de la propriété `/etc/tags` est `cq:movedTo/cq:backLinks`. Il effectue ensuite une itération dans le jeu de résultats récupéré et résout les valeurs de propriété `cq:movedTo` et `cq:backlinks` en chemins `/content/cq:tags` (dans le cas où `/etc/tags` est détecté dans la valeur).

### Si l’instance AEM mise à niveau s’exécute sur l’interface utilisateur classique {#upgraded-instance-runs-classic-ui}

>[!NOTE]
>
>L’interface utilisateur classique n’est pas compatible avec zéro temps d’arrêt et ne prend pas en charge le nouveau chemin de base des balises. Si vous souhaitez utiliser une interface utilisateur classique, vous devez créer `/etc/tags`, puis redémarrer le composant `cq-tagging`.

Dans le cas d’instances AEM mises à niveau prises en charge par l’API TagManager et s’exécutant dans l’interface utilisateur classique :

1. Une fois que les références à l’ancien chemin de base de balises `/etc/tags` sont remplacées par tagId ou nouvel emplacement de balise `/content/cq:tags`, vous pouvez migrer les balises vers le nouvel emplacement `/content/cq:tags` dans CRX suivi du redémarrage du composant.

1. Après la migration des balises vers le nouvel emplacement, exécutez le script mentionné ci-dessus.
