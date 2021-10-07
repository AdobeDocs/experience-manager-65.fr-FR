---
title: Référence des prédicats de Query Builder
seo-title: Query Builder Predicate Reference
description: Référence complète des prédicats pour l’API Query Builder.
seo-description: Complete predicate reference for the Query Builder API.
uuid: af0e269e-7d52-4032-b22e-801c7b5dccfa
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
discoiquuid: 94a05894-743a-4ace-a292-bfee90ba9068
exl-id: 54b942f9-5dd9-4826-9a0a-028f2d7b8e41
source-git-commit: 2bae11eafb875f01602c39c0dba00a888e11391a
workflow-type: tm+mt
source-wordcount: '2310'
ht-degree: 61%

---

# Référence des prédicats de Query Builder{#query-builder-predicate-reference}

## Général {#general}

* [root](#root)
* [groupe](#group)
* [orderby](#orderby)

## Prédicats {#predicates}

* [boolproperty](/help/sites-developing/querybuilder-predicate-reference.md#boolproperty)
* [contentfragment](/help/sites-developing/querybuilder-predicate-reference.md#contentfragment)
* [dateComparison](/help/sites-developing/querybuilder-predicate-reference.md#datecomparison)
* [daterange](/help/sites-developing/querybuilder-predicate-reference.md#daterange)
* [excludepaths](/help/sites-developing/querybuilder-predicate-reference.md#excludepaths)
* [fulltext](/help/sites-developing/querybuilder-predicate-reference.md#fulltext)
* [hasPermission](/help/sites-developing/querybuilder-predicate-reference.md#haspermission)
* [language](/help/sites-developing/querybuilder-predicate-reference.md#language)
* [mainasset](/help/sites-developing/querybuilder-predicate-reference.md#mainasset)
* [memberOf](/help/sites-developing/querybuilder-predicate-reference.md#memberof)
* [nodename](/help/sites-developing/querybuilder-predicate-reference.md#nodename)
* [notexpired](/help/sites-developing/querybuilder-predicate-reference.md#notexpired)
* [path](/help/sites-developing/querybuilder-predicate-reference.md#path)
* [property](/help/sites-developing/querybuilder-predicate-reference.md#property)
* [rangeproperty](/help/sites-developing/querybuilder-predicate-reference.md#rangeproperty)
* [relativedaterange](/help/sites-developing/querybuilder-predicate-reference.md#relativedaterange)
* [savedquery](/help/sites-developing/querybuilder-predicate-reference.md#savedquery)
* [similar](/help/sites-developing/querybuilder-predicate-reference.md#similar)
* [tag](/help/sites-developing/querybuilder-predicate-reference.md#tag)
* [tagid](/help/sites-developing/querybuilder-predicate-reference.md#tagid)
* [tagsearch](/help/sites-developing/querybuilder-predicate-reference.md#tagsearch)
* [type](/help/sites-developing/querybuilder-predicate-reference.md#type)

### boolproperty {#boolproperty}

Correspond aux propriétés JCR BOOLEAN. Accepte uniquement les valeurs &quot;`true`&quot; et &quot;`false`&quot;. En cas de valeur « `false` », il correspond si la valeur de la propriété est « `false` » ou si la propriété n’existe pas. Cela peut s’avérer utile pour rechercher des indicateurs booléens qui sont définis uniquement lorsqu’ils sont activés.

Le paramètre « `operation` » hérité n’a aucune signification.

Prend en charge l’extraction de facettes. Fournit des buckets pour chaque valeur `true` ou `false`, mais uniquement pour les propriétés existantes.

#### Propriétés {#properties}

* ****
boolproperty Chemin d’accès relatif à la propriété, par exemple 
`myFeatureEnabled` ou `jcr:content/myFeatureEnabled`

* ****
valeur à vérifier pour la propriété, &quot; 
`true`&quot; ou &quot; `false`&quot;

### contentfragment {#contentfragment}

Limite le résultat aux fragments de contenu.

Ne prend pas en charge le filtrage.

Ne prend pas en charge l’extraction de facettes.

#### Propriétés {#properties-1}

* **contentfragment** Peut être utilisé avec n’importe quelle valeur pour rechercher des fragments de contenu.

### dateComparison {#datecomparison}

Compare deux propriétés JCR DATE entre elles. Permet d’établir des comparaisons de type « est égale à », « est différente de », « est supérieure à » ou encore « est supérieure ou égale à ».

Il s’agit d’un prédicat de type filtrage seul qui ne peut pas exploiter d’index de recherche.

#### Propriétés {#properties-2}

* **property1**

   chemin d’accès à la première propriété date

* **property2**

   chemin d’accès à la propriété second date

* **operation**

   &quot; `equals`&quot; pour la correspondance exacte, &quot; `!=`&quot; pour la comparaison des inégalités, &quot; `greater`&quot; pour property1 supérieure à property2, &quot; `>=`&quot; pour property1 supérieure ou égale à property2. La valeur par défaut est &quot; `equals`&quot;.

### daterange {#daterange}

Fait correspondre les propriétés JCR DATE par rapport à un intervalle de date/heure. Il utilise le format ISO8601
pour les dates et heures (`YYYY-MM-DDTHH:mm:ss.SSSZ`) et autorise les représentations partielles, comme `YYYY-MM-DD`. L’horodatage peut également être fourni sous la forme d’un nombre de millisecondes écoulées depuis 1970 dans le fuseau horaire UTC (format d’heure UNIX).

Vous pouvez rechercher tout ce qui se trouve entre deux horodatages, un élément plus récent ou plus ancien qu’une date donnée, et également choisir entre des intervalles inclusifs et ouverts.

Prend en charge l’extraction de facettes. Fournit les buckets « aujourd’hui », « cette semaine » ou « ce mois-ci », « les 3 derniers mois », « cette année », « l’année dernière » et « avant l’année dernière ».

Ne prend pas en charge le filtrage.

#### Propriétés {#properties-3}

* **property**

   chemin relatif à une propriété `DATE`, par exemple `jcr:lastModified`

* **lowerBound**

    Limite de date inférieure pour laquelle la propriété doit être vérifiée ; par exemple, `2014-10-01`

* **lowerOperation**

   &quot; `>`&quot; (plus récent) ou &quot;`>=`&quot; (plus récent ou plus récent), s’applique à `lowerBound`. La valeur par défaut est de &quot; `>`&quot;.

* **upperBound**

   limite supérieure pour laquelle vérifier la propriété, par exemple `2014-10-01T12:15:00`

* **upperOperation**

   &quot; `<`&quot; (plus ancien) ou &quot; `<=`&quot; (plus ancien ou plus ancien), s’applique à la balise `upperBound`. La valeur par défaut est de &quot; `<`&quot;.

* **timeZone**

   ID du fuseau horaire à utiliser lorsqu’il n’est pas indiqué sous la forme d’une chaîne de date ISO-8601. La valeur par défaut est le fuseau horaire par défaut du système.

### excludepaths {#excludepaths}

Exclut des nœuds du résultat lorsque leur chemin d’accès correspond à une expression régulière.

Il s’agit d’un prédicat de type filtrage seul qui ne peut pas exploiter d’index de recherche.

Ne prend pas en charge l’extraction de facettes.

#### Propriétés {#properties-4}

* **excludepaths**

   Expression régulière comparée à des chemins de résultat, en excluant les correspondances du résultat.

### fulltext {#fulltext}

Recherches de termes dans l’index en texte intégral.

Ne prend pas en charge le filtrage.

Ne prend pas en charge l’extraction de facettes.

#### Propriétés {#properties-5}

* **fulltext**

   le ou les termes de recherche en texte intégral

* **relPath**

   Chemin d’accès relatif devant faire l’objet d’une recherche dans la propriété ou le sous-nœud. Cette propriété est facultative.

### groupe {#group}

Permet de créer des conditions imbriquées. Les groupes peuvent contenir des groupes imbriqués. Tout le contenu d’une requête Query Builder se trouve implicitement dans un groupe racine qui peut également posséder des paramètres `p.or` et `p.not`.

Exemple pour la correspondance de l’une des deux propriétés par rapport à une valeur :

```
group.p.or=true
group.1_property=jcr:title
group.1_property.value=My Page
group.2_property=navTitle
group.2_property.value=My Page
```

D’un point de vue conceptuel, il s’agit de `(1_property`OR `2_property)`.

Exemple pour les groupes imbriqués :

```
fulltext=Management
group.p.or=true
group.1_group.path=/content/geometrixx/en
group.1_group.type=cq:Page
group.2_group.path=/content/dam/geometrixx
group.2_group.type=dam:Asset
```

Cela permet de rechercher le terme &quot;**Gestion**&quot; dans les pages de `/content/geometrixx/en` ou dans les ressources de `/content/dam/geometrixx`.

Il s’agit conceptuellement de `fulltext AND ( (path AND type) OR (path AND type) )`. Pour des jointures OR de ce type, de bons index sont requis pour garantir les performances.

#### Propriétés {#properties-6}

* **p.or**

   si elle est définie sur &quot;`true`&quot;, un seul prédicat du groupe doit correspondre. La valeur par défaut est « `false` », ce qui signifie que tout doit correspondre.

* **p.not**

   s’il est défini sur &quot;`true`&quot;, il annule le groupe (par défaut, &quot; `false`&quot;).

* **&lt;predicate>**

   ajoute des prédicats imbriqués ;

* **N_&lt;predicate>**

   ajoute plusieurs prédicats imbriqués en même temps, comme `1_property, 2_property, ...` ;

### hasPermission {#haspermission}

Limite les résultats aux éléments dont la session en cours possède les [privilèges JCR](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges) spécifiés.

Il s’agit d’un prédicat de type filtrage seul qui ne peut pas exploiter d’index de recherche. Il ne prend pas en charge l’extraction de facettes.

#### Propriétés {#properties-7}

* **hasPermission**

   des privilèges JCR séparés par des virgules que la session utilisateur actuelle doit TOUS posséder pour le noeud en question ; par exemple `jcr:write`, `jcr:modifyAccessControl`

### language {#language}

Recherche des pages CQ dans une langue spécifique. Ce prédicat examine la propriété language de la page et le chemin d’accès de la page qui inclut souvent la langue ou le paramètre régional dans une structure de site de niveau supérieur.

Il s’agit d’un prédicat de type filtrage seul qui ne peut pas exploiter d’index de recherche.

Prend en charge l’extraction de facettes. Des buckets sont fournis pour chaque code de langue.

#### Propriétés {#properties-8}

* **language**

   Code de langue ISO, par exemple &quot;`de`&quot;

### mainasset {#mainasset}

Vérifie si un nœud est une ressource DAM principale et non une sous-ressource. Il s’agit, en fait, de tout nœud qui ne se trouve pas à l’intérieur d’un nœud « subassets ». Notez que ce prédicat ne recherche pas le type de nœud `dam:Asset`. Pour utiliser ce prédicat, définissez simplement &quot;`mainasset=true`&quot; ou &quot;`mainasset=false`&quot;, il n’y a aucune autre propriété.

Il s’agit d’un prédicat de type filtrage seul qui ne peut pas exploiter d’index de recherche.

Prend en charge l’extraction de facettes. Fournit 2 buckets pour les ressources principales et les sous-ressources.

#### Propriétés {#properties-9}

* **mainasset**

   booléen, &quot; `true`&quot; pour les ressources principales, &quot; `false`&quot; pour les sous-ressources

### memberOf {#memberof}

Recherche les éléments qui sont membres d’une [collection de ressources Sling](https://helpx.adobe.com/fr/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/resource/collection/ResourceCollection.html) spécifique.

Il s’agit d’un prédicat de type filtrage seul qui ne peut pas exploiter d’index de recherche. Ne prend pas en charge l’extraction de facettes.

#### Propriétés {#properties-10}

* **memberOf**

   chemin d’accès à la collecte des ressources Sling

### nodename {#nodename}

Correspond aux noms de nœuds JCR.

Prend en charge l’extraction de facettes. Fournit des buckets pour chaque nom de nœud (nom de fichier).

#### Propriétés {#properties-11}

* **nodename**

   modèle de nom de noeud qui autorise les caractères génériques : `*` = n’importe quel caractère, `?` = n’importe quel caractère, `[abc]` = uniquement les caractères entre crochets

### notexpired {#notexpired}

Fait correspondre des éléments en vérifiant si une propriété JCR DATE est supérieure ou égale à l’heure actuelle du serveur. Ce prédicat peut être utilisé pour effectuer une vérification sur une propriété date de type « `expiresAt` » et se limiter uniquement à celles qui n’ont pas encore expiré (`notexpired=true`) ou qui ont déjà expiré ( `notexpired=false`).

Ne prend pas en charge le filtrage.

Prend en charge l’extraction de facettes de la même manière que le prédicat daterange.

#### Propriétés {#properties-12}

* **notexpired**

   Booléen, « `true` » pour les propriétés qui n’ont pas encore expiré (date future ou égale à celle indiquée), « `false` » pour les propriétés qui ont expiré (date dans le passé) (obligatoire)

* **property**

   chemin d’accès relatif à la propriété `DATE` à vérifier (obligatoire).

### orderby {#orderby}

Permet de trier les résultats. Si un classement basé sur plusieurs propriétés est requis, ce prédicat doit être ajouté plusieurs fois à l’aide du préfixe numérique, tel que `1_orderby=first`, `2_oderby=second`.

#### Propriétés {#properties-13}

* **orderby**

   soit le nom de propriété JCR indiqué par un @ de début, par exemple `@jcr:lastModified` ou `@jcr:content/jcr:title`, soit un autre prédicat dans la requête, par exemple `2_property`, sur lequel trier

* **trier**

   direction du tri, soit &quot;`desc`&quot; pour les valeurs descendantes, soit &quot; `asc`&quot; pour les valeurs ascendantes (par défaut)

* **cas**

    Si cette valeur est définie sur « `ignore` », le tri n’est pas sensible à la casse, ce qui signifie que « a » vient avant « B » ; si cette valeur est vide ou ignorée, le tri est sensible à la casse, ce qui signifie que « B » vient avant « a ».

### path {#path}

Effectue une recherche à un emplacement donné.

Ne prend pas en charge l’extraction de facettes.

#### Propriétés {#properties-14}

* **path**

   modèle de chemin; selon l’exact, soit la sous-arborescence entière correspond (comme ajouter `//*` dans xpath, mais notez que cela n’inclut pas le chemin de base) (exact=false, valeur par défaut) ou qu’un chemin exact correspond, ce qui peut inclure des caractères génériques ( `*`) ; si self est défini, la recherche porte sur la sous-arborescence entière, y compris le noeud de base.

* **exact**

   si `exact` est vrai/actif, le chemin exact doit correspondre, mais il peut contenir de simples caractères génériques ( `*`), qui correspondent aux noms, mais pas &quot;`/`&quot;; s’il est faux (par défaut), tous les descendants sont inclus (facultatif)

* **plat**

   recherche uniquement les enfants directs (comme ajouter &quot;`/*`&quot; dans xpath) (utilisé uniquement si &quot;`exact`&quot; n’est pas vrai, facultatif) ;

* **self**

    Effectue des recherches dans la sous-arborescence, mais inclut le nœud de base indiqué comme chemin d’accès (pas de caractères génériques).

### property {#property}

Correspond aux propriétés JCR et à leur valeurs.

Prend en charge l’extraction de facettes. Fournit des buckets pour chaque valeur de propriété dans les résultats.

#### Propriétés {#properties-15}

* **property**

   chemin d’accès relatif à la propriété, par exemple `jcr:title`

* **value**

    Valeur dont la propriété doit être vérifiée ; suit le type de propriété JCR pour les conversions de chaînes

* **N_value**

   utilisez `1_value`, `2_value`, ... pour rechercher plusieurs valeurs (combinées avec `OR` par défaut, avec `AND` si et=true) (depuis la version 5.3).

* **et**

   défini sur true pour la combinaison de plusieurs valeurs ( `N_value`) avec AND (depuis la version 5.3)

* **operation**

   &quot;`equals`&quot; pour la correspondance exacte (par défaut), &quot;`unequals`&quot; pour la comparaison des inégalités, &quot; `like`&quot; pour l’utilisation de la fonction `jcr:like` xpath (facultative), &quot;`not`&quot; pour aucune correspondance (par exemple &quot;`not(@prop)`&quot; dans xpath, la valeur param sera ignorée) ou &quot;`exists`&quot; pour la vérification de l’existence (la valeur peut être true - la propriété doit exister, la valeur par défaut - ou false - identique à &quot; `not`&quot;)

* **profondeur**

   nombre de niveaux de caractères génériques sous lesquels le chemin d’accès relatif/de propriété peut exister (par exemple, `property=size depth=2` vérifie le noeud/la taille, node/amp;ast;/size et node/&amp;ast;/&amp;ast;/size)

### rangeproperty {#rangeproperty}

Fait correspondre une propriété JCR par rapport à un intervalle de temps. Ce prédicat s’applique à des propriétés de type linéaire telles que `LONG`, `DOUBLE` et `DECIMAL`. Pour `DATE`, reportez-vous au prédicat daterange qui présente une entrée de format de date optimisée.

Vous pouvez définir une limite inférieure et une limite supérieure ou seulement l’une des deux. L’opération (par exemple, « inférieur à » ou « inférieur ou égal à ») peut également être spécifiée séparément pour la limite inférieure et la limite supérieure.

Ne prend pas en charge l’extraction de facettes.

#### Propriétés {#properties-16}

* **property**

   chemin d’accès relatif à la propriété

* **lowerBound**

   limite inférieure pour laquelle la propriété

* **lowerOperation**

   &quot; `>`&quot; (par défaut) ou &quot;`>=`&quot;, s’applique à la balise `lowerValue`

* **upperBound**

   limite supérieure pour laquelle la propriété doit être vérifiée

* **upperOperation**

   &quot; `<`&quot; (par défaut) ou &quot;`<=`&quot;, s’applique à la balise `lowerValue`

* **decimal**

   &quot; `true`&quot; si la propriété vérifiée est de type Décimal

### relativedaterange {#relativedaterange}

Fait correspondre les propriétés `JCR DATE` par rapport à un intervalle de date/heure à l’aide de décalages temporels relatifs à l’heure actuelle du serveur. Vous pouvez spécifier `lowerBound` et `upperBound` à l’aide d’une valeur en millisecondes ou de la syntaxe de bugzilla `1s 2m 3h 4d 5w 6M 7y` (une seconde, deux minutes, trois heures, quatre jours, cinq semaines, six mois, sept ans). Préfixe avec &quot;`-`&quot; pour indiquer un décalage négatif avant l’heure actuelle. Si vous spécifiez uniquement `lowerBound` ou `upperBound`, l’autre propriété est définie par défaut sur 0, ce qui signifie l’heure actuelle.

Par exemple :

* `upperBound=1h` (et aucun  `lowerBound`) sélectionne n’importe quoi au cours de l’heure suivante.
* `lowerBound=-1d` (et aucun  `upperBound`) sélectionne n’importe quoi au cours des dernières 24 heures.
* `lowerBound=-6M` et  `upperBound=-3M` sélectionnerait tout ce qui a entre 6 mois et 3 mois.
* `lowerBound=-1500` et  `upperBound=5500` sélectionnerait tout ce qui se situe entre 1 500 millisecondes dans le passé et 5 500 millisecondes dans le futur.
* `lowerBound=1d` et  `upperBound=2d` sélectionnerait n’importe quel élément après-demain

Notez que ce prédicat ne tient pas compte des années bissextiles et que tous les mois comptent 30 jours.

Ne prend pas en charge le filtrage.

Prend en charge l’extraction de facettes de la même manière que le prédicat daterange.

#### Propriétés {#properties-17}

* **upperBound**

   date supérieure limite en millisecondes ou `1s 2m 3h 4d 5w 6M 7y` (une seconde, deux minutes, trois heures, quatre jours, cinq semaines, six mois, sept ans) par rapport à l’heure actuelle du serveur, utilisez &quot;-&quot; pour un décalage négatif.

* **lowerBound**

   date inférieure limite en millisecondes ou `1s 2m 3h 4d 5w 6M 7y` (une seconde, deux minutes, trois heures, quatre jours, cinq semaines, six mois, sept ans) par rapport à l’heure actuelle du serveur, utilisez &quot;-&quot; pour un décalage négatif.

### root {#root}

Groupe de prédicats racine. Prend en charge toutes les fonctionnalités d’un groupe et permet de définir des paramètres de requête globaux.

Le nom « root » n’est jamais utilisé dans une requête ; il est implicite.

#### Propriétés {#properties-18}

* **p.offset**

   Nombre indiquant le début de la page de résultats, c’est-à-dire le nombre d’éléments à ignorer

* **p.limit**

   nombre indiquant la taille de la page

* **p.guessTotal**

   Recommandé : évite de calculer le total des résultats, une opération qui peut s’avérer fastidieuse ; il s’agit soit d’un nombre qui indique la limite de comptage maximale (par exemple 1000, un nombre qui offre aux utilisateurs suffisamment d’informations sur la taille approximative et des valeurs exactes pour des résultats plus petits), soit de « `true` » pour compter seulement jusqu’au minimum requis `p.offset` + `p.limit`

* **p.excerpt**

   si elle est définie sur &quot;`true`&quot;, incluez un extrait de texte intégral dans le résultat.

* **p.hits**

    (uniquement pour le servlet JSON) Sélectionne la manière dont les accès sont écrits au format JSON, avec ces éléments standard (extensibles via le service ResultHitWriter) :

   * **simple**:

      éléments minimaux tels que `path`, `title`, `lastmodified`, `excerpt` (s’il est défini)

   * **full**:

      rendu Sling JSON du noeud, avec `jcr:path` indiquant le chemin de l’accès : par défaut, répertorie uniquement les propriétés directes du noeud, incluez une arborescence plus profonde avec `p.nodedepth=N`, 0 signifiant la sous-arborescence entière et infinie ; ajoutez `p.acls=true` pour inclure les autorisations JCR de la session en cours sur l’élément de résultat donné (mappages : `create` = `add_node`, `modify` = `set_property`, `delete` = `remove`

   * **sélective**:

      seules les propriétés spécifiées dans `p.properties`, qui est une liste de chemins relatifs séparés par des espaces (utilisez &quot;+&quot; dans les URL) ; si le chemin relatif a une profondeur supérieure à 1, ils seront représentés en tant qu’objets enfants ; la propriété spéciale jcr:path inclut le chemin de l’accès.

### savedquery {#savedquery}

Inclut tous les prédicats d’une requête Query Builder persistante dans la requête actuelle sous la forme d’un prédicat de sous-groupe.

Notez que ce prédicat n’exécute pas une requête supplémentaire, mais étend la requête en cours.

Les requêtes peuvent être conservées par programmation à l’aide de `QueryBuilder#storeQuery()`. Ce format peut être soit une propriété String multiligne, soit un nœud `nt:file` contenant la requête en tant que fichier texte au format des propriétés Java.

Ne prend pas en charge l’extraction de facettes pour les prédicats de la requête enregistrée.

#### Propriétés {#properties-19}

* **savedquery**

   chemin d’accès à la requête enregistrée (propriété String ou noeud `nt:file`)

### similaire {#similar}

Recherche par analogie à l’aide de Xpath JCR `rep:similar()`.

Ne prend pas en charge le filtrage. Ne prend pas en charge l’extraction de facettes.

#### Propriétés {#properties-20}

* **similar** Chemin d’accès absolu au nœud pour lequel des nœuds similaires sont recherchés

* **local** Chemin d’accès relatif à un nœud descendant ou 
`.` pour le noeud actif (facultatif, la valeur par défaut est &quot;  `.`&quot;)

### tag {#tag}

Recherche du contenu identifié avec une ou plusieurs balises, en spécifiant les chemins d’accès aux titres de balise.

Prend en charge l’extraction de facettes. Fournit des buckets pour chaque balise, en utilisant le chemin d’accès au titre de balise actif.

#### Propriétés {#properties-21}

* **tag**

    Chemin d’accès au titre de la balise à rechercher ; par exemple, « Propriétés de ressource : Orientation / Paysage »

* **N_value**

   utilisez `1_value`, `2_value`, ... pour rechercher plusieurs balises (combinées avec `OR` par défaut, avec `AND` si et=true) (depuis la version 5.6).

* **property**

   (ou chemin relatif à la propriété) à examiner (par défaut &quot;`cq:tags`&quot;)

### tagid {#tagid}

Recherche du contenu identifié avec une ou plusieurs balises, en spécifiant des ID de balise.

Prend en charge l’extraction de facettes. Fournit des buckets pour chaque balise, en utilisant l’ID de balise en cours.

#### Propriétés {#properties-22}

* **tagid**

   ID de balise à rechercher, par exemple &quot;`properties:orientation/landscape`&quot;

* **N_value**

   utilisez `1_value`, `2_value`, ... pour rechercher plusieurs identifiants (combinés avec `OR` par défaut, avec `AND` si et=true) (depuis la version 5.6).

* **property**

   (ou chemin relatif à la propriété) à examiner (par défaut &quot;`cq:tags`&quot;)

### tagsearch {#tagsearch}

Recherche du contenu identifié avec une ou plusieurs balises, en spécifiant des mots-clés. Ce prédicat recherche d’abord les balises dont les titres contiennent ces mots-clés, puis limite les résultats aux seuls éléments balisés de la sorte.

Ne prend pas en charge l’extraction de facettes.

#### Propriétés {#Properties-1}

* **tagsearch**

   Mot-clé à rechercher dans les titres de nœud

* **property**

   (ou chemin relatif à la propriété) à examiner (par défaut &quot;`cq:tags`&quot;)

* **lang**

   pour effectuer uniquement une recherche dans un certain titre de balise localisé (par exemple, &quot; `de`&quot;)

* **all**

   (booléen) Effectue la recherche dans le texte intégral de la balise, c’est-à-dire tous les titres, la description, etc. (a la priorité sur &quot;l `ang`&quot;)

### type {#type}

Limite les résultats à un type de nœud JCR spécifique, aussi bien un type de nœud primaire qu’un type de mixin. Cela permet également de rechercher des sous-types de ce type de nœud. Pour une exécution efficace, notez que les index de recherche de référentiel doivent couvrir les types de nœud.

Prend en charge l’extraction de facettes. Fournit des buckets pour chaque type de valeur dans les résultats.

#### Propriétés {#Properties-2}

* **type**

   type de noeud ou nom de mixin à rechercher, par exemple `cq:Page`
