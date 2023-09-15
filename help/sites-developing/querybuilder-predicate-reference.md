---
title: Référence des prédicats de Query Builder
description: Référence complète des prédicats pour l’API Query Builder.
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
exl-id: 54b942f9-5dd9-4826-9a0a-028f2d7b8e41
source-git-commit: 4e2ee7da5424ac6677eaa2392de7803e7543d13c
workflow-type: tm+mt
source-wordcount: '2347'
ht-degree: 28%

---

# Référence des prédicats de Query Builder{#query-builder-predicate-reference}

>[!CAUTION]
>
>Les informations contenues dans cette page ne sont pas exhaustives.
>
>Pour plus d’informations, reportez-vous à la liste figurant dans **Prédicats disponibles** dans la console de débogage Query Builder, par exemple, à l’adresse :
>* [http://localhost:4502/libs/cq/search/content/querydebug.html](http://localhost:4502/libs/cq/search/content/querydebug.html)
>
>Pour obtenir un exemple, reportez-vous à :
>
>* [http://localhost:4502/system/console/services?filter=%28component.factory%3Dcom.day.cq.search.eval.PredicateEvaluator%2F*%29](http://localhost:4502/system/console/services?filter=%28component.factory%3Dcom.day.cq.search.eval.PredicateEvaluator%2F*%29)

## Général {#general}

* [root](#root)
* [group](#group)
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

Correspond aux propriétés JCR BOOLEAN. Accepte uniquement les valeurs « `true` » et « `false` ». Si &quot; `false`&quot;, il correspond si la propriété a la valeur &quot; `false`&quot; ou s’il n’existe pas du tout. Cela peut s’avérer utile pour rechercher des indicateurs booléens qui sont définis uniquement lorsqu’ils sont activés.

Le paramètre « `operation` » hérité n’a aucune signification.

Prend en charge l’extraction de facettes. Fournit des compartiments pour chaque `true` ou `false` , mais uniquement pour les propriétés existantes.

#### Propriétés {#properties}

* **boolproperty**
Chemin d’accès relatif à la propriété, par exemple `myFeatureEnabled` ou `jcr:content/myFeatureEnabled`.

* **value**
Valeur pour laquelle la propriété doit être vérifiée, &quot; `true`&quot; ou &quot; `false`&quot;.

### contentfragment {#contentfragment}

Limite le résultat aux fragments de contenu.

Ne prend pas en charge le filtrage.

Ne prend pas en charge l’extraction de facettes.

#### Propriétés {#properties-1}

* **contentfragment**
Peut être utilisé avec n’importe quelle valeur pour rechercher des fragments de contenu.

### dateComparison {#datecomparison}

Compare deux propriétés JCR DATE l’une à l’autre. Vous pouvez tester s’ils sont égaux, inégaux, supérieurs ou supérieurs ou égaux.

Il s’agit d’un prédicat de filtrage uniquement qui ne peut pas utiliser d’index de recherche.

#### Propriétés {#properties-2}

* **property1**

  Chemin d’accès à la première propriété de date.

* **property2**

  Chemin d’accès à la propriété second date.

* **operation**

  « `equals` » pour une correspondance exacte, « `!=` » pour une comparaison inégale, « `greater` » lorsque la property1 est plus grande que la property2, « `>=` » lorsque la property1 est plus grande ou égale à la property2. La valeur par défaut est « `equals` ».

### daterange {#daterange}

Correspond aux propriétés JCR DATE par rapport à un intervalle de date/heure. Il utilise le format ISO8601
pour les dates et heures (`YYYY-MM-DDTHH:mm:ss.SSSZ`) et autorise les représentations partielles, comme `YYYY-MM-DD`. Vous pouvez également fournir l’horodatage sous la forme du nombre de millisecondes écoulées depuis 1970 dans le fuseau horaire UTC, le format d’heure UNIX®.

Vous pouvez rechercher tout ce qui se trouve entre deux horodatages, un élément plus récent ou plus ancien qu’une date donnée, et également choisir entre des intervalles inclusifs et ouverts.

Prend en charge l’extraction de facettes. Fournit des intervalles &quot;aujourd’hui&quot;, &quot;cette semaine&quot;, &quot;ce mois-ci&quot;, &quot;les 3 derniers mois&quot;, &quot;cette année&quot;, &quot;l’année dernière&quot; et &quot;avant l’année dernière&quot;.

Ne prend pas en charge le filtrage.

#### Propriétés {#properties-3}

* **property**

  Chemin d’accès relatif à un `DATE` par exemple, `jcr:lastModified`.

* **lowerBound**

  Limite de date inférieure pour laquelle vérifier la propriété, par exemple `2014-10-01`.

* **lowerOperation**

  « `>` » (plus récent) ou « `>=` » (à cette date ou plus récent) ; applicable à `lowerBound`. La valeur par défaut est de « `>` ».

* **upperBound**

  Limite supérieure pour laquelle vérifier la propriété, par exemple `2014-10-01T12:15:00`.

* **upperOperation**

  « `<` » (antérieur) ou « `<=` » (à cette date ou antérieur) ; applicable à `upperBound`. La valeur par défaut est de « `<` ».

* **timeZone**

  ID du fuseau horaire à utiliser lorsqu’il n’est pas indiqué sous la forme d’une chaîne de date ISO-8601. La valeur par défaut est le fuseau horaire par défaut du système.

### excludepaths {#excludepaths}

Exclut les noeuds du résultat où leur chemin correspond à une expression régulière.

Il s’agit d’un prédicat de filtrage uniquement qui ne peut pas utiliser d’index de recherche.

Ne prend pas en charge l’extraction de facettes.

#### Propriétés {#properties-4}

* **excludepaths**

  Expression régulière comparée aux chemins de résultat, à l’exception des chemins correspondants du résultat.

### fulltext {#fulltext}

Recherche des termes dans l’index de texte intégral.

Ne prend pas en charge le filtrage.

Ne prend pas en charge l’extraction de facettes.

#### Propriétés {#properties-5}

* **fulltext**

  Termes de recherche en texte intégral.

* **relPath**

  Chemin d’accès relatif à rechercher dans la propriété ou le sous-noeud. Cette propriété est facultative.

### group {#group}

Permet la création de conditions imbriquées. Les groupes peuvent contenir des groupes imbriqués. Tout ce qui se trouve dans une requête Query Builder se trouve implicitement dans un groupe racine, qui peut avoir `p.or` et `p.not` également.

Exemple pour la correspondance de l’une des deux propriétés par rapport à une valeur :

```
group.p.or=true
group.1_property=jcr:title
group.1_property.value=My Page
group.2_property=navTitle
group.2_property.value=My Page
```

D’un point de vue conceptuel, il s’agit de `(1_property` OU `2_property)`.

Exemple pour les groupes imbriqués :

```
fulltext=Management
group.p.or=true
group.1_group.path=/content/geometrixx/en
group.1_group.type=cq:Page
group.2_group.path=/content/dam/geometrixx
group.2_group.type=dam:Asset
```

Dans ce cas, le terme « **Management** » est recherché dans des pages sous `/content/geometrixx/en` ou dans des ressources sous `/content/dam/geometrixx`.

Il s’agit conceptuellement de `fulltext AND ( (path AND type) OR (path AND type) )`. De telles jointures OR nécessitent de bons index de performance.

#### Propriétés {#properties-6}

* **p.or**

  Si la variable est définie sur &quot; `true`&quot;, un seul prédicat du groupe doit correspondre. La valeur par défaut est « `false` », ce qui signifie que tout doit correspondre.

* **p.not**

  Si la variable est définie sur &quot; `true`&quot;, il annule le groupe (par défaut, &quot; `false`&quot;).

* **&lt;predicate>**

  Ajoute des prédicats imbriqués.

* **N_&lt;predicate>**

  Ajoute plusieurs prédicats imbriqués en même temps, comme `1_property, 2_property, ...`.

### hasPermission {#haspermission}

Limite les résultats aux éléments dont la session en cours possède les [privilèges JCR](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges) spécifiés.

Il s’agit d’un prédicat de filtrage uniquement qui ne peut pas utiliser d’index de recherche. Il ne prend pas en charge l’extraction de facettes.

#### Propriétés {#properties-7}

* **hasPermission**

  Privilèges JCR séparés par des virgules, qui doivent TOUS comporter le noeud en question pour la session utilisateur actuelle. Par exemple, `jcr:write`, `jcr:modifyAccessControl`.

### language {#language}

Recherche les pages CQ dans une langue spécifique. Cela permet d’examiner à la fois la propriété de langue de la page et le chemin d’accès à la page qui inclut souvent la langue ou les paramètres régionaux dans une structure de site de niveau supérieur.

Il s’agit d’un prédicat de filtrage uniquement qui ne peut pas utiliser d’index de recherche.

Prend en charge l’extraction de facettes. Fournit des buckets pour chaque code de langue unique.

#### Propriétés {#properties-8}

* **language**

  Code langue ISO ; par exemple, « `de` »

### mainasset {#mainasset}

Vérifie si un noeud est une ressource principale DAM et non une sous-ressource. Il s’agit essentiellement de chaque noeud qui ne se trouve pas à l’intérieur d’un noeud &quot;subassets&quot;. Cela ne vérifie pas que la variable `dam:Asset` type de noeud. Pour utiliser ce prédicat, définissez &quot; `mainasset=true`&quot; ou &quot; `mainasset=false`&quot;, il n’y a pas d’autres propriétés.

Il s’agit d’un prédicat de filtrage uniquement qui ne peut pas utiliser d’index de recherche.

Prend en charge l’extraction de facettes et fournit deux compartiments pour les sous-ressources principales et secondaires.

#### Propriétés {#properties-9}

* **mainasset**

  Booléen, &quot; `true`&quot; pour les ressources principales, &quot; `false`&quot; pour les sous-ressources.

### memberOf {#memberof}

Recherche les éléments qui sont membres d’un [collecte de ressources sling](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/resource/collection/ResourceCollection.html).

Il s’agit d’un prédicat de filtrage uniquement qui ne peut pas utiliser d’index de recherche. Ne prend pas en charge l’extraction de facettes.

#### Propriétés {#properties-10}

* **memberOf**

  Chemin d’accès de la collecte des ressources Sling.

### nodename {#nodename}

Correspond aux noms de noeud JCR.

Prend en charge l’extraction de facettes. Fournit des compartiments pour chaque nom de noeud unique (nom de fichier).

#### Propriétés {#properties-11}

* **nodename**

  Modèle de nom de noeud qui permet les caractères génériques : `*` = n’importe quel caractère ou aucun caractère, `?` = tout caractère, `[abc]` = uniquement les caractères entre crochets.

### notexpired {#notexpired}

Correspond aux éléments en vérifiant si une propriété JCR DATE est supérieure ou égale à l’heure actuelle du serveur. Ce prédicat peut être utilisé pour effectuer une vérification sur une propriété date de type « `expiresAt` » et se limiter uniquement à celles qui n’ont pas encore expiré (`notexpired=true`) ou qui ont déjà expiré (`notexpired=false`).

Ne prend pas en charge le filtrage.

Prend en charge l’extraction de facettes de la même manière que le prédicat daterange.

#### Propriétés {#properties-12}

* **notexpired**

  Booléen, &quot; `true`&quot; pour pas encore expiré (date ultérieure ou égale), &quot; `false`&quot; pour expiré (date antérieure) (obligatoire).

* **property**

  Chemin d’accès relatif à `DATE` à vérifier (obligatoire).

### orderby {#orderby}

Permet de trier les résultats. Si un classement par plusieurs propriétés est requis, ce prédicat doit être ajouté plusieurs fois à l’aide du préfixe numérique, tel que `1_orderby=first`, `2_oderby=second`.

#### Propriétés {#properties-13}

* **orderby**

  Nom de propriété JCR indiqué par un caractère @ de début, par exemple `@jcr:lastModified` ou `@jcr:content/jcr:title`, ou un autre prédicat dans la requête, par exemple `2_property`, sur laquelle trier.

* **trier**

  Tri de la direction : `desc`&quot; pour décroissant ou &quot; `asc`&quot; pour croissant (par défaut).

* **case**

  Si la variable est définie sur `ignore`, le tri n’est pas sensible à la casse, ce qui signifie que &quot;a&quot; précède &quot;B&quot;. Si ce paramètre est vide ou omis, le tri est sensible à la casse, ce qui signifie que &quot;B&quot; précède &quot;a&quot;.

### path {#path}

Recherche dans un chemin donné.

Ne prend pas en charge l’extraction de facettes.

#### Propriétés {#properties-14}

* **path**

  Modèle de chemin. Selon les valeurs exactes, l’une ou l’autre des sous-arborescences correspond (comme l’ajout de `//*` dans xpath, mais notez que cela n’inclut pas le chemin de base (exact=false, par défaut), ou qu’il ne s’agit que d’une correspondance de chemin exacte, qui peut inclure des caractères génériques ( `*`) ; si self est défini, la sous-arborescence entière, y compris le noeud de base, est recherchée.

* **exact**

  If `exact` est défini sur true/on, le chemin exact doit correspondre, mais il peut contenir des caractères génériques simples ( `*`), qui correspondent aux noms, mais pas à &quot; `/`&quot;; s’il est faux (par défaut), tous les descendants sont inclus (facultatif).

* **flat**

  Recherche uniquement les enfants directs (comme l’ajout de &quot; `/*`&quot; dans xpath (utilisé uniquement si &quot;) `exact`&quot; n’est pas vrai, facultatif).

* **self**

  Recherche la sous-arborescence, mais inclut le noeud de base indiqué comme chemin d’accès (aucun caractère générique).

### property {#property}

Correspond aux propriétés JCR et à leurs valeurs.

Prend en charge l’extraction de facettes. Fournit des intervalles pour chaque valeur de propriété unique dans les résultats.

#### Propriétés {#properties-15}

* **property**

  Chemin d’accès relatif à la propriété, par exemple `jcr:title`.

* **value**

  Valeur pour laquelle vérifier la propriété ; suit le type de propriété JCR en conversions de chaîne.

* **N_value**

  Utilisation `1_value`, `2_value`, etc. pour vérifier plusieurs valeurs (combinées avec `OR` par défaut, avec `AND` si et=true) (depuis la version 5.3).

* **and**

  Définissez cette variable sur true pour combiner plusieurs valeurs ( `N_value`) avec ET (depuis la version 5.3).

* **operation**

  &quot;`equals`&quot; pour une correspondance exacte (par défaut), &quot; `unequals`&quot; pour la comparaison des inégalités, &quot; `like`&quot; pour utiliser la variable `jcr:like` fonction xpath (facultatif), &quot; `not`&quot; pour aucune correspondance (par exemple, &quot;`not(@prop)`&quot; dans xpath, le paramètre value est ignoré) ou &quot; `exists`&quot; pour la vérification de l’existence (la valeur peut être true - la propriété doit exister, par défaut - ou false - comme &quot; `not`&quot;).

* **depth**

  Nombre de niveaux de caractères génériques sous lesquels le chemin de propriété/relatif peut exister (par exemple, `property=size depth=2` vérifie le noeud/la taille, le noeud/&amp;ast;/size et le noeud/&amp;ast;/&amp;ast;/size).

### rangeproperty {#rangeproperty}

Correspond à une propriété JCR par rapport à un intervalle. Cela s’applique aux propriétés avec des types linéaires tels que `LONG`, `DOUBLE`, et `DECIMAL`. Pour `DATE`, voir le prédicat daterange qui contient une entrée de format de date optimisée.

Vous pouvez définir une limite inférieure et une limite supérieure ou seulement l’une d’elles. L’opération (par exemple, &quot;inférieur à&quot; ou &quot;inférieur ou égal à&quot;) peut également être spécifiée pour les limites inférieure et supérieure, individuellement.

Ne prend pas en charge l’extraction de facettes.

#### Propriétés {#properties-16}

* **property**

  Chemin d’accès relatif à la propriété.

* **lowerBound**

  Limite inférieure pour laquelle vérifier la propriété.

* **lowerOperation**

  « `>` » (par défaut) ou « `>=` », s’applique à `lowerValue`.

* **upperBound**

  Limite supérieure pour laquelle vérifier la propriété.

* **upperOperation**

  « `<` » (par défaut) ou « `<=` », s’applique à `lowerValue`.

* **decimal**

  « `true` » si la propriété vérifiée est de type Décimal

### relativedaterange {#relativedaterange}

Fait correspondre les propriétés `JCR DATE` par rapport à un intervalle de date/heure à l’aide de décalages temporels relatifs à l’heure actuelle du serveur. Vous pouvez spécifier `lowerBound` et `upperBound` en utilisant une valeur en millisecondes ou la syntaxe bugzilla `1s 2m 3h 4d 5w 6M 7y` (une seconde, deux minutes, trois heures, quatre jours, cinq semaines, six mois, sept ans). Préfixe avec « `-` » pour indiquer un décalage négatif avant l’heure actuelle. Si vous indiquez uniquement `lowerBound` ou `upperBound`, l’autre valeur par défaut est 0, ce qui signifie l’heure actuelle.

Par exemple :

* `upperBound=1h` (et pas de `lowerBound`) sélectionnerait tous les éléments dans l’heure suivante.
* `lowerBound=-1d` (et pas de `upperBound`) sélectionnerait tous les éléments dans les dernières 24 heures.
* `lowerBound=-6M` et `upperBound=-3M` sélectionneraient tous les éléments entre 6 mois et 3 mois.
* `lowerBound=-1500` et `upperBound=5500` sélectionneraient tous les éléments entre 1 500 millisecondes dans le passé et 5 500 millisecondes dans le futur.
* `lowerBound=1d` et `upperBound=2d` sélectionneraient tous les éléments du jour d’après-demain ;

Il ne faut pas tenir compte des années bissextiles et tous les mois sont 30 jours.

Ne prend pas en charge le filtrage.

Prend en charge l’extraction de facettes de la même manière que le prédicat daterange.

#### Propriétés {#properties-17}

* **upperBound**

  Limite de date supérieure en millisecondes ou `1s 2m 3h 4d 5w 6M 7y` (une seconde, deux minutes, trois heures, quatre jours, cinq semaines, six mois, sept ans) par rapport à l’heure actuelle du serveur, utilisez &quot;-&quot; pour un décalage négatif.

* **lowerBound**

  Limite de date inférieure en millisecondes ou `1s 2m 3h 4d 5w 6M 7y` (une seconde, deux minutes, trois heures, quatre jours, cinq semaines, six mois, sept ans) par rapport à l’heure actuelle du serveur, utilisez &quot;-&quot; pour un décalage négatif.

### root {#root}

Groupe de prédicats racine. Prend en charge toutes les fonctionnalités d’un groupe et vous permet de définir des paramètres de requête globaux.

Le nom « root » n’est jamais utilisé dans une requête ; il est implicite.

#### Propriétés {#properties-18}

* **p.offset**

  Nombre indiquant le début de la page de résultat, c’est-à-dire le nombre d’éléments à ignorer.

* **p.limit**

  Nombre indiquant la taille de la page.

* **p.guessTotal**

  Recommandé : évitez de calculer le total des résultats, qui peut s’avérer coûteux ; soit un nombre indiquant le total maximum à comptabiliser (par exemple 1 000, un nombre qui donne aux utilisateurs suffisamment de commentaires sur la taille brute et les nombres exacts pour des résultats plus modestes), soit &quot; `true`&quot; pour ne compter que le minimum nécessaire `p.offset` + `p.limit`.

* **p.excerpt**

  Si la variable est définie sur &quot; `true`&quot;, incluez un extrait de texte intégral dans le résultat.

* **p.hits**

   (uniquement pour le servlet JSON) Sélectionne la manière dont les accès sont écrits au format JSON, avec ces éléments standard (extensibles via le service ResultHitWriter) :

   * **simple** :

     Éléments minimaux tels que `path`, `title`, `lastmodified`, `excerpt` (si défini).

   * **full** :

     Rendu Sling JSON du noeud, avec `jcr:path` indiquant le chemin de l’accès : par défaut, répertorie uniquement les propriétés directes du noeud, incluez une arborescence plus profonde avec `p.nodedepth=N`, avec 0 signifiant la sous-arborescence entière et infinie ; ajoutez `p.acls=true` pour inclure les autorisations JCR de la session en cours sur l’élément de résultat donné (mappages : `create` = `add_node`, `modify` = `set_property`, `delete` = `remove`).

   * **selective** :

     Uniquement les propriétés spécifiées dans `p.properties`, qui est une liste de chemins relatifs séparés par des espaces (utilisez &quot;+&quot; dans les URL) ; si le chemin relatif a une profondeur > 1, ils sont représentés comme objets enfants ; la propriété spéciale jcr:path inclut le chemin de l’accès.

### savedquery {#savedquery}

Inclut tous les prédicats d’une requête du créateur de requêtes persistante dans la requête actuelle sous la forme d’un prédicat de sous-groupe.

Cela n’exécute pas de requête supplémentaire, mais étend la requête actuelle.

Les requêtes peuvent être conservées par programmation à l’aide de `QueryBuilder#storeQuery()`. Le format peut être soit une propriété String multiligne, soit une propriété `nt:file` qui contient la requête sous la forme d’un fichier texte au format des propriétés Java™.

Ne prend pas en charge l’extraction de facettes pour les prédicats de la requête enregistrée.

#### Propriétés {#properties-19}

* **savedquery**

  Chemin d’accès à la requête enregistrée (propriété String ou `nt:file` ).

### similar {#similar}

Recherche par analogie à l’aide du `rep:similar()` du Xpath JCR.

Ne prend pas en charge le filtrage. Ne prend pas en charge l’extraction de facettes.

#### Propriétés {#properties-20}

* **similaire**
Chemin d’accès absolu au noeud pour lequel trouver des noeuds similaires.

* **local**
Un chemin relatif à un noeud descendant ou `.` pour le noeud actif (facultatif, la valeur par défaut est &quot; `.`&quot;).

### tag {#tag}

Recherche du contenu balisé avec une ou plusieurs balises, en spécifiant les chemins d’accès au titre de la balise.

Prend en charge l’extraction de facettes. Fournit des buckets pour chaque balise, à l’aide de son chemin d’accès actuel au titre de la balise.

#### Propriétés {#properties-21}

* **tag**

  Chemin d’accès au titre de la balise à rechercher, par exemple &quot;Propriétés de la ressource : orientation/paysage&quot;.

* **N_value**

  Utilisation `1_value`, `2_value`, ... pour rechercher plusieurs balises (combinées avec `OR` par défaut, avec `AND` si et=true) (depuis la version 5.6).

* **property**

  Propriété (ou chemin d’accès relatif à la propriété) à examiner (par défaut &quot; `cq:tags`&quot;)

### tagid {#tagid}

Recherche du contenu balisé avec une ou plusieurs balises, en spécifiant des ID de balise.

Prend en charge l’extraction de facettes. Fournit des compartiments pour chaque balise unique, à l’aide de leur ID de balise actuel.

#### Propriétés {#properties-22}

* **tagid**

  Identifiant de balise pour pouvoir rechercher, par exemple &quot; `properties:orientation/landscape`&quot;.

* **N_value**

  Utilisation `1_value`, `2_value`, etc. pour rechercher plusieurs identifiants (combinés avec `OR` par défaut, avec `AND` si et=true) (depuis la version 5.6).

* **property**

  Propriété (ou chemin d’accès relatif à la propriété) à examiner (par défaut &quot; `cq:tags`&quot;).

### tagsearch {#tagsearch}

Recherche du contenu balisé avec une ou plusieurs balises, en spécifiant des mots-clés. Cette recherche commence par les balises qui contiennent ces mots-clés dans leur titre, puis limite le résultat aux seuls éléments balisés avec ces mots-clés.

Ne prend pas en charge l’extraction de facettes.

#### Propriétés {#Properties-1}

* **tagsearch**

  Mot-clé à rechercher dans les titres de balise.

* **property**

  Propriété (ou chemin d’accès relatif à la propriété) à examiner (par défaut) `cq:tags`).

* **lang**

  Pour effectuer une recherche dans un certain titre de balise localisé uniquement (par exemple : `de`).

* **all**

  (booléen) Recherchez le texte intégral d’une balise, c’est-à-dire tous les titres, la description, etc. (la priorité est accordée à &quot;l&quot; `ang`&quot;).

### type {#type}

Limite les résultats à un type de noeud JCR spécifique, qu’il s’agisse d’un type de noeud principal ou d’un type de mixin. Il trouve également des sous-types de ce type de noeud. Les index de recherche de référentiel doivent couvrir les types de noeuds pour une exécution efficace.

Prend en charge l’extraction de facettes. Fournit des intervalles pour chaque type unique dans les résultats.

#### Propriétés {#Properties-2}

* **type**

  Type de noeud ou nom de mixin à rechercher, par exemple `cq:Page`.
