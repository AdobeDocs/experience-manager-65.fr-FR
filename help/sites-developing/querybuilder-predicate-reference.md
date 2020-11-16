---
title: Référence des prédicats de Query Builder
seo-title: Référence des prédicats de Query Builder
description: Référence complète des prédicats pour l’API Query Builder.
seo-description: Référence complète des prédicats pour l’API Query Builder.
uuid: af0e269e-7d52-4032-b22e-801c7b5dccfa
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
discoiquuid: 94a05894-743a-4ace-a292-bfee90ba9068
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379
workflow-type: tm+mt
source-wordcount: '2323'
ht-degree: 59%

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

Correspond aux propriétés JCR BOOLEAN. Only accepts the values &quot; `true`&quot; and &quot; `false`&quot;. En cas de valeur « `false` », il correspond si la valeur de la propriété est « `false` » ou si la propriété n’existe pas. Cela peut s’avérer utile pour rechercher des indicateurs booléens qui sont définis uniquement lorsqu’ils sont activés.

Le paramètre « `operation` » hérité n’a aucune signification.

Prend en charge l’extraction de facettes. Fournit des buckets pour chaque valeur `true` ou `false`, mais uniquement pour les propriétés existantes.

#### Propriétés {#properties}

* **boolproperty** relatif path to property, par exemple 
`myFeatureEnabled` ou `jcr:content/myFeatureEnabled`

* **valeur** pour laquelle vérifier la propriété, &quot; 
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

   chemin d’accès à la propriété first date

* **property2**

   chemin d’accès à la deuxième propriété de date

* **operation**

   &quot; `=`&quot; for exact match, &quot; `!=`&quot; for unequality comparison, &quot; `>`&quot; for property1 greater than property2, &quot; `>=`&quot; for property1 greater than or equal to property2. La valeur par défaut est &quot; `=`&quot;.

### daterange {#daterange}

Fait correspondre les propriétés JCR DATE par rapport à un intervalle de date/heure. This uses the ISO8601
format for dates and times ( `YYYY-MM-DDTHH:mm:ss.SSSZ`) and allows also partial representations, like `YYYY-MM-DD`. L’horodatage peut également être fourni sous la forme d’un nombre de millisecondes écoulées depuis 1970 dans le fuseau horaire UTC (format d’heure UNIX).

Vous pouvez rechercher tout ce qui se trouve entre deux horodatages, un élément plus récent ou plus ancien qu’une date donnée, et également choisir entre des intervalles inclusifs et ouverts.

Prend en charge l’extraction de facettes. Fournit les buckets « aujourd’hui », « cette semaine » ou « ce mois-ci », « les 3 derniers mois », « cette année », « l’année dernière » et « avant l’année dernière ».

Ne prend pas en charge le filtrage.

#### Propriétés {#properties-3}

* **property**

   relative path to a `DATE` property, for example `jcr:lastModified`

* **lowerBound**

   lower date bound to check property for, for example `2014-10-01`

* **lowerOperation**

   &quot; `>`&quot; (newer) or &quot; `>=`&quot; (at or newer), applies to the `lowerBound`. La valeur par défaut est de &quot; `>`&quot;.

* **upperBound**

   upper bound to check property for, for example `2014-10-01T12:15:00`

* **upperOperation**

   &quot; `<`&quot; (older) or &quot; `<=`&quot; (at or older), applies to the `upperBound`. La valeur par défaut est de &quot; `<`&quot;.

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

   le ou les termes de recherche de texte intégral

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

This is conceptually `(1_property` OR `2_property)`.

Exemple pour les groupes imbriqués :

```
fulltext=Management
group.p.or=true
group.1_group.path=/content/geometrixx/en
group.1_group.type=cq:Page
group.2_group.path=/content/dam/geometrixx
group.2_group.type=dam:Asset
```

This searches for the term &quot;**Management**&quot; within pages in `/content/geometrixx/en` or in assets in `/content/dam/geometrixx`.

C&#39;est conceptuellement `fulltext AND ( (path AND type) OR (path AND type) )`. Pour des jointures OR de ce type, de bons index sont requis pour garantir les performances.

#### Propriétés {#properties-6}

* **p.or**

   if set to &quot; `true`&quot;, only one predicate in the group must match. La valeur par défaut est « `false` », ce qui signifie que tout doit correspondre.

* **p.not**

   if set to &quot; `true`&quot;, it negates the group (defaults to &quot; `false`&quot;)

* **&lt;prédicat>**

   ajoute des prédicats imbriqués

* **N_&lt;prédicat>**

   ajoute plusieurs prédicats imbriqués simultanément, comme `1_property, 2_property, ...`

### hasPermission {#haspermission}

Limite les résultats aux éléments dont la session en cours possède les [privilèges JCR](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges) spécifiés.

Il s’agit d’un prédicat de type filtrage seul qui ne peut pas exploiter d’index de recherche. Il ne prend pas en charge l’extraction de facettes.

#### Propriétés {#properties-7}

* **hasPermission**

   comma-separated JCR privileges that the current user session must ALL have for the node in question; for example `jcr:write`, `jcr:modifyAccessControl`

### language {#language}

Recherche des pages CQ dans une langue spécifique. Ce prédicat examine la propriété language de la page et le chemin d’accès de la page qui inclut souvent la langue ou le paramètre régional dans une structure de site de niveau supérieur.

Il s’agit d’un prédicat de type filtrage seul qui ne peut pas exploiter d’index de recherche.

Prend en charge l’extraction de facettes. Des buckets sont fournis pour chaque code de langue.

#### Propriétés {#properties-8}

* **language**

   ISO language code, for example &quot; `de`&quot;

### mainasset {#mainasset}

Vérifie si un nœud est une ressource DAM principale et non une sous-ressource. Il s’agit, en fait, de tout nœud qui ne se trouve pas à l’intérieur d’un nœud « subassets ». Notez que ce prédicat ne recherche pas le type de nœud `dam:Asset`. To use this predicate, simply set &quot; `mainasset=true`&quot; or &quot; `mainasset=false`&quot;, there are no further properties.

Il s’agit d’un prédicat de type filtrage seul qui ne peut pas exploiter d’index de recherche.

Prend en charge l’extraction de facettes. Fournit 2 buckets pour les ressources principales et les sous-ressources.

#### Propriétés {#properties-9}

* **mainasset**

   boolean, &quot; `true`&quot; for main assets, &quot; `false`&quot; for sub assets

### memberOf {#memberof}

Recherche les éléments qui sont membres d’une [collection de ressources Sling](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/resource/collection/ResourceCollection.html) spécifique.

Il s’agit d’un prédicat de type filtrage seul qui ne peut pas exploiter d’index de recherche. Ne prend pas en charge l’extraction de facettes.

#### Propriétés {#properties-10}

* **memberOf**

   chemin de collecte des ressources Sling

### nodename {#nodename}

Correspond aux noms de nœuds JCR.

Prend en charge l’extraction de facettes. Fournit des buckets pour chaque nom de nœud (nom de fichier).

#### Propriétés {#properties-11}

* **nodename**

   modèle de nom de noeud qui autorise les caractères génériques : `*` = n’importe quel ou aucun caractère, `?` = n’importe quel caractère, `[abc]` = uniquement les caractères entre crochets

### notexpired {#notexpired}

Fait correspondre des éléments en vérifiant si une propriété JCR DATE est supérieure ou égale à l’heure actuelle du serveur. Ce prédicat peut être utilisé pour effectuer une vérification sur une propriété date de type « `expiresAt` » et se limiter uniquement à celles qui n’ont pas encore expiré (`notexpired=true`) ou qui ont déjà expiré ( `notexpired=false`).

Ne prend pas en charge le filtrage.

Prend en charge l’extraction de facettes de la même manière que le prédicat daterange.

#### Propriétés {#properties-12}

* **notexpired**

   Booléen, « `true` » pour les propriétés qui n’ont pas encore expiré (date future ou égale à celle indiquée), « `false` » pour les propriétés qui ont expiré (date dans le passé) (obligatoire)

* **property**

   relative path to the `DATE` property to check (required)

### orderby {#orderby}

Permet de trier les résultats. If ordering by multiple properties is required, this predicate needs to be added multiple times using the number prefix, such as `1_orderby=first`, `2_oderby=second`.

#### Propriétés {#properties-13}

* **orderby**

   either JCR property name indicated by a leading @, for example `@jcr:lastModified` or `@jcr:content/jcr:title`, or another predicate in the query, for example `2_property`, on which to sort

* **trier**

   sort direction, either &quot; `desc`&quot; for descending or &quot; `asc`&quot; for ascending (default)

* **case**

    Si cette valeur est définie sur « `ignore` », le tri n’est pas sensible à la casse, ce qui signifie que « a » vient avant « B » ; si cette valeur est vide ou ignorée, le tri est sensible à la casse, ce qui signifie que « B » vient avant « a ».

### path {#path}

Effectue une recherche à un emplacement donné.

Ne prend pas en charge l’extraction de facettes.

#### Propriétés {#properties-14}

* **path**

   path pattern; depending on exact, either the entire subtree will match (like appending `//*` in xpath, but note that this does not include the base path) (exact=false, default) or only an exact path matches, which can include wildcards ( `*`); if self is set, the entire subtree including the base node will be searched

* **exact**

   if `exact` is true/on, the exact path must match, but it can contain simple wildcards ( `*`), that match names, but not &quot; `/`&quot;; if it is false (default) all descendents are included (optional)

* **plat**

   searches only the direct children (like appending &quot; `/*`&quot; in xpath) (only used if &#39; `exact`&#39; is not true, optional)

* **self**

    Effectue des recherches dans la sous-arborescence, mais inclut le nœud de base indiqué comme chemin d’accès (pas de caractères génériques).

### property {#property}

Correspond aux propriétés JCR et à leur valeurs.

Prend en charge l’extraction de facettes. Fournit des buckets pour chaque valeur de propriété dans les résultats.

#### Propriétés {#properties-15}

* **property**

   relative path to property, for example `jcr:title`

* **value**

    Valeur dont la propriété doit être vérifiée ; suit le type de propriété JCR pour les conversions de chaînes

* **N_value**

   use `1_value`, `2_value`, ... to check for multiple values (combined with `OR` by default, with `AND` if and=true) (since 5.3)

* **et**

   set to true for combining multiple values ( `N_value`) with AND (since 5.3)

* **operation**

   &quot; `equals`&quot; for exact match (default), &quot; `unequals`&quot; for unequality comparison, &quot; `like`&quot; for using the `jcr:like` xpath function (optional), &quot; `not`&quot; for no match (eg. &quot; `not(@prop)`&quot; in xpath, value param will be ignored) or &quot; `exists`&quot; for existence check (value can be true - property must exist, the default - or false - same as &quot; `not`&quot;)

* **profondeur**

   nombre de niveaux de caractères génériques sous lesquels la propriété/le chemin relatif peut exister (par exemple, `property=size depth=2` vérifiera le noeud/taille, noeud/&amp;amp ; ast ;/size et node/&amp;amp ; ast ;/&amp;amp ; ast ;/size)

### rangeproperty {#rangeproperty}

Fait correspondre une propriété JCR par rapport à un intervalle de temps. This applies to properties with linear types such as `LONG`, `DOUBLE` and `DECIMAL`. Pour `DATE`, reportez-vous au prédicat daterange qui présente une entrée de format de date optimisée.

Vous pouvez définir une limite inférieure et une limite supérieure ou seulement l’une des deux. L’opération (par exemple, « inférieur à » ou « inférieur ou égal à ») peut également être spécifiée séparément pour la limite inférieure et la limite supérieure.

Ne prend pas en charge l’extraction de facettes.

#### Propriétés {#properties-16}

* **property**

   chemin relatif à la propriété

* **lowerBound**

   limite inférieure pour vérifier la propriété

* **lowerOperation**

   &quot; `>`&quot; (default) or &quot; `>=`&quot;, applies to the `lowerValue`

* **upperBound**

   limite supérieure pour vérifier la propriété

* **upperOperation**

   &quot; `<`&quot; (default) or &quot; `<=`&quot;, applies to the `lowerValue`

* **decimal**

   &quot; `true`&quot; if the checked property is of type Decimal

### relativedaterange {#relativedaterange}

Fait correspondre les propriétés `JCR DATE` par rapport à un intervalle de date/heure à l’aide de décalages temporels relatifs à l’heure actuelle du serveur. You can specify `lowerBound` and `upperBound` using either a millisecond value or the bugzilla syntax `1s 2m 3h 4d 5w 6M 7y` (one second, two minutes, three hours, four days, five weeks, six months, seven years). Prefix with &quot; `-`&quot; to indicate a negative offset before the current time. Si vous spécifiez uniquement `lowerBound` ou `upperBound`, l’autre propriété est définie par défaut sur 0, ce qui signifie l’heure actuelle.

Par exemple :

* `upperBound=1h` (et aucun `lowerBound`) ne sélectionnerait quoi que ce soit dans l’heure suivante
* `lowerBound=-1d` (et aucun `upperBound`) ne sélectionnerait quoi que ce soit au cours des dernières 24 heures.
* `lowerBound=-6M` et `upperBound=-3M` choisirait n&#39;importe quelle période de 6 mois à 3 mois.
* `lowerBound=-1500` et `upperBound=5500` sélectionner n’importe quoi entre 1 500 millisecondes dans le passé et 5 500 millisecondes dans le futur
* `lowerBound=1d` et `upperBound=2d` sélectionnerait n&#39;importe quoi après-demain

Notez que ce prédicat ne tient pas compte des années bissextiles et que tous les mois comptent 30 jours.

Ne prend pas en charge le filtrage.

Prend en charge l’extraction de facettes de la même manière que le prédicat daterange.

#### Propriétés {#properties-17}

* **upperBound**

   upper date bound in milliseconds or `1s 2m 3h 4d 5w 6M 7y` (one second, two minutes, three hours, four days, five weeks, six months, seven years) relative to current server time, use &quot;-&quot; for negative offset

* **lowerBound**

   lower date bound in milliseconds or `1s 2m 3h 4d 5w 6M 7y` (one second, two minutes, three hours, four days, five weeks, six months, seven years) relative to current server time, use &quot;-&quot; for negative offset

### root {#root}

Groupe de prédicats racine. Prend en charge toutes les fonctionnalités d’un groupe et permet de définir des paramètres de requête globaux.

Le nom « root » n’est jamais utilisé dans une requête ; il est implicite.

#### Propriétés {#properties-18}

* **p.offset**

   Nombre indiquant le début de la page de résultats, c’est-à-dire le nombre d’éléments à ignorer

* **p.limit**

   nombre indiquant le format de page

* **p.devinezTotal**

   Recommandé : évite de calculer le total des résultats, une opération qui peut s’avérer fastidieuse ; il s’agit soit d’un nombre qui indique la limite de comptage maximale (par exemple 1000, un nombre qui offre aux utilisateurs suffisamment d’informations sur la taille approximative et des valeurs exactes pour des résultats plus petits), soit de « `true` » pour compter seulement jusqu’au minimum requis `p.offset` + `p.limit`

* **p.excerpt**

   if set to &quot; `true`&quot;, include full text excerpt in the result

* **p.hits**

    (uniquement pour le servlet JSON) Sélectionne la manière dont les accès sont écrits au format JSON, avec ces éléments standard (extensibles via le service ResultHitWriter) :

   * **simple**:

      éléments minimaux tels que `path`, `title`, `lastmodified`, `excerpt` (s’ils sont définis)

   * **full**:

      sling JSON rendering of the node, with `jcr:path` indicating the path of the hit: by default just lists the direct properties of the node, include a deeper tree with `p.nodedepth=N`, with 0 meaning the entire, infinite subtree; add `p.acls=true` to include the JCR permissions of the current session on the given result item (mappings: `create` = `add_node`, `modify` = `set_property`, `delete` = `remove`)

   * **sélective**:

      only properties specified in `p.properties`, which is a space separated (use &quot;+&quot; in URLs) list of relative paths; if the relative path has a depth > 1 these will be represented as child objects; the special jcr:path property includes the path of the hit

### savedquery {#savedquery}

Inclut tous les prédicats d’une requête Query Builder persistante dans la requête actuelle sous la forme d’un prédicat de sous-groupe.

Notez que ce prédicat n’exécute pas une requête supplémentaire, mais étend la requête en cours.

Queries can be persisted programmatically using `QueryBuilder#storeQuery()`. Ce format peut être soit une propriété String multiligne, soit un nœud `nt:file` contenant la requête en tant que fichier texte au format des propriétés Java.

Ne prend pas en charge l’extraction de facettes pour les prédicats de la requête enregistrée.

#### Propriétés {#properties-19}

* **savedquery**

   path to the saved query (String property or `nt:file` node)

### similar {#similar}

Similarity search using JCR XPath&#39;s `rep:similar()`.

Ne prend pas en charge le filtrage. Ne prend pas en charge l’extraction de facettes.

#### Propriétés {#properties-20}

* **similar** Chemin d’accès absolu au nœud pour lequel des nœuds similaires sont recherchés

* **local** Chemin d’accès relatif à un nœud descendant ou 
`.` pour le noeud actif (facultatif, la valeur par défaut est &quot; `.`&quot;)

### tag {#tag}

Recherche du contenu identifié avec une ou plusieurs balises, en spécifiant les chemins d’accès aux titres de balise.

Prend en charge l’extraction de facettes. Fournit des buckets pour chaque balise, en utilisant le chemin d’accès au titre de balise actif.

#### Propriétés {#properties-21}

* **tag**

    Chemin d’accès au titre de la balise à rechercher ; par exemple, « Propriétés de ressource : Orientation / Paysage »

* **N_value**

   use `1_value`, `2_value`, ... to check for multiple tags (combined with `OR` by default, with `AND` if and=true) (since 5.6)

* **property**

   property (or relative path to property) to look at (default &quot; `cq:tags`&quot;)

### tagid {#tagid}

Recherche du contenu identifié avec une ou plusieurs balises, en spécifiant des ID de balise.

Prend en charge l’extraction de facettes. Fournit des buckets pour chaque balise, en utilisant l’ID de balise en cours.

#### Propriétés {#properties-22}

* **tagid**

   tag id to look for, for example &quot; `properties:orientation/landscape`&quot;

* **N_value**

   use `1_value`, `2_value`, ... to check for multiple tagids (combined with `OR` by default, with `AND` if and=true) (since 5.6)

* **property**

   property (or relative path to property) to look at (default &quot; `cq:tags`&quot;)

### tagsearch {#tagsearch}

Recherche du contenu identifié avec une ou plusieurs balises, en spécifiant des mots-clés. Ce prédicat recherche d’abord les balises dont les titres contiennent ces mots-clés, puis limite les résultats aux seuls éléments balisés de la sorte.

Ne prend pas en charge l’extraction de facettes.

#### Propriétés {#Properties-1}

* **tagsearch**

   Mot-clé à rechercher dans les titres de nœud

* **property**

   property (or relative path to property) to look at (default &quot; `cq:tags`&quot;)

* **lang**

   to search in a certain localized tag title only (e.g. &quot; `de`&quot;)

* **all**

   (booléen) Effectue la recherche dans le texte intégral de la balise, c’est-à-dire tous les titres, la description, etc. (takes precedence over &quot;l `ang`&quot;)

### type {#type}

Limite les résultats à un type de nœud JCR spécifique, aussi bien un type de nœud primaire qu’un type de mixin. Cela permet également de rechercher des sous-types de ce type de nœud. Pour une exécution efficace, notez que les index de recherche de référentiel doivent couvrir les types de nœud.

Prend en charge l’extraction de facettes. Fournit des buckets pour chaque type de valeur dans les résultats.

#### Propriétés {#Properties-2}

* **type**

   node type or mixin name to search for, for example `cq:Page`