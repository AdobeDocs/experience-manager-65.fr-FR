---
title: Référence des prédicats de Query Builder
description: Référence des prédicats pour l’API Query Builder.
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
exl-id: 54b942f9-5dd9-4826-9a0a-028f2d7b8e41
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2313'
ht-degree: 92%

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

Correspond aux propriétés BOOLEAN JCR. Accepte uniquement les valeurs « `true` » et « `false` ». Si la valeur est `false`, elle correspond si la propriété a la valeur `false`, ou si elle n’existe pas du tout. Cela peut s’avérer utile pour rechercher des indicateurs booléens qui sont définis uniquement lorsqu’ils sont activés.

Le paramètre « `operation` » hérité n’a aucune signification.

Prend en charge l’extraction de facettes. Fournit des compartiments pour chaque valeur `true` ou `false`, mais uniquement pour les propriétés existantes.

#### Propriétés {#properties}

* **boolproperty**
Chemin d’accès relatif à la propriété, par exemple : `myFeatureEnabled` ou `jcr:content/myFeatureEnabled`.

* **value**
Valeur pour laquelle vérifier la propriété, « `true` » ou « `false` ».

### contentfragment {#contentfragment}

Limite le résultat aux fragments de contenu.

Ne prend pas en charge le filtrage.

Ne prend pas en charge l’extraction de facettes.

#### Propriétés {#properties-1}

* **contentfragment**
Peut être utilisé avec n’importe quelle valeur pour rechercher des fragments de contenu.

### dateComparison {#datecomparison}

Compare entre elles deux propriétés DATE JCR. Vous pouvez tester si elles sont égales, inégales, supérieures ou supérieures ou égales.

Il s’agit d’un prédicat de type filtrage seul qui ne peut pas utiliser d’index de recherche.

#### Propriétés {#properties-2}

* **property1**

  Chemin d’accès à la première propriété date.

* **property2**

  Chemin d’accès à la deuxième propriété date.

* **operation**

  « `equals` » pour une correspondance exacte, « `!=` » pour une comparaison inégale, « `greater` » lorsque la property1 est plus grande que la property2, « `>=` » lorsque la property1 est plus grande ou égale à la property2. La valeur par défaut est « `equals` ».

### daterange {#daterange}

Met en correspondance les propriétés DATE JCR par rapport à un intervalle de date/heure. Il utilise le format ISO8601
pour les dates et heures (`YYYY-MM-DDTHH:mm:ss.SSSZ`) et autorise les représentations partielles, comme `YYYY-MM-DD`. Vous pouvez également fournir la date et l’heure sous la forme du nombre de millisecondes écoulées depuis 1970 dans le fuseau horaire UTC, le format d’heure UNIX®.

Vous pouvez rechercher tout ce qui se trouve entre deux horodatages, un élément plus récent ou plus ancien qu’une date donnée, et également choisir entre des intervalles inclusifs et ouverts.

Prend en charge l’extraction de facettes. Fournit des compartiments « aujourd’hui », « cette semaine », « ce mois-ci », « les 3 derniers mois », « cette année », « l’année dernière » et « avant l’année dernière ».

Ne prend pas en charge le filtrage.

#### Propriétés {#properties-3}

* **property**

  Chemin d’accès relatif à un `DATE` par exemple, `jcr:lastModified`.

* **lowerBound**

  Limite de date inférieure pour laquelle vérifier la propriété, par exemple : `2014-10-01`.

* **lowerOperation**

  « `>` » (plus récent) ou « `>=` » (à cette date ou plus récent) ; applicable à `lowerBound`. La valeur par défaut est de « `>` ».

* **upperBound**

  Limite supérieure pour laquelle vérifier la propriété, par exemple `2014-10-01T12:15:00`.

* **upperOperation**

  « `<` » (antérieur) ou « `<=` » (à cette date ou antérieur) ; applicable à `upperBound`. La valeur par défaut est de « `<` ».

* **timeZone**

  ID du fuseau horaire à utiliser lorsqu’il n’est pas indiqué sous la forme d’une chaîne de date ISO-8601. La valeur par défaut est le fuseau horaire par défaut du système.

### excludepaths {#excludepaths}

Exclut des nœuds du résultat lorsque leur chemin d’accès correspond à une expression régulière.

Il s’agit d’un prédicat de type filtrage seul qui ne peut pas utiliser d’index de recherche.

Ne prend pas en charge l’extraction de facettes.

#### Propriétés {#properties-4}

* **excludepaths**

  Expression régulière comparée à des chemins de résultat, en excluant les correspondances du résultat.

### fulltext {#fulltext}

Recherche des termes dans l’index en texte intégral.

Ne prend pas en charge le filtrage.

Ne prend pas en charge l’extraction de facettes.

#### Propriétés {#properties-5}

* **fulltext**

  Termes de recherche en texte intégral.

* **relPath**

  Chemin d’accès relatif devant faire l’objet d’une recherche dans la propriété ou le sous-nœud. Cette propriété est facultative.

### group {#group}

Permet la création de conditions imbriquées. Les groupes peuvent contenir des groupes imbriqués. Tout le contenu d’une requête Query Builder se trouve implicitement dans un groupe racine qui peut également posséder des paramètres `p.or` et `p.not`.

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

Il s’agit conceptuellement de `fulltext AND ( (path AND type) OR (path AND type) )`. De telles jointures OR nécessitent de bons index pour des raisons de performances.

#### Propriétés {#properties-6}

* **p.or**

  Si défini sur « `true` », un seul prédicat du groupe doit correspondre. La valeur par défaut est « `false` », ce qui signifie que tout doit correspondre.

* **p.not**

  Si défini sur « `true` », le groupe est annulé (la valeur par défaut est « `false` »).

* **&lt;predicate>**

  Ajoute des prédicats imbriqués.

* **N_&lt;predicate>**

  Ajoute plusieurs prédicats imbriqués simultanément, comme `1_property, 2_property, ...`.

### hasPermission {#haspermission}

Limite les résultats aux éléments dont la session en cours possède les [privilèges JCR](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges) spécifiés.

Il s’agit d’un prédicat de type filtrage seul qui ne peut pas utiliser d’index de recherche. Il ne prend pas en charge l’extraction de facettes.

#### Propriétés {#properties-7}

* **hasPermission**

  Privilèges JCR séparés par des virgules qui doivent TOUS être associés à la session utilisateur en cours pour le nœud en question. Par exemple, `jcr:write`, `jcr:modifyAccessControl`.

### language {#language}

Recherche les pages CQ dans une langue spécifique. Cela permet d’examiner à la fois la propriété de langue de la page et le chemin d’accès à la page qui inclut souvent la langue ou les paramètres régionaux dans une structure de site de niveau supérieur.

Il s’agit d’un prédicat de type filtrage seul qui ne peut pas utiliser d’index de recherche.

Prend en charge l’extraction de facettes. Fournit des compartiments pour chaque code de langue unique.

#### Propriétés {#properties-8}

* **language**

  Code de langue ISO, par exemple, &quot;`de`&quot;

### mainasset {#mainasset}

Vérifie si un nœud est une ressource principale DAM et non une sous-ressource. Il s’agit, en fait, de tout nœud qui ne se trouve pas à l’intérieur d’un nœud « sub-assets ». Ce prédicat ne recherche pas le type de nœud `dam:Asset`. Pour utiliser ce prédicat, définissez « `mainasset=true` » ou « `mainasset=false` » ; il n’y a pas d’autres propriétés.

Il s’agit d’un prédicat de type filtrage seul qui ne peut pas utiliser d’index de recherche.

Prend en charge l’extraction des facettes et fournit deux compartiments pour les ressources principales et secondaires.

#### Propriétés {#properties-9}

* **mainasset**

  Booléen, « `true` » pour les ressources principales, « `false` » pour les sous-ressources.

### memberOf {#memberof}

Recherche les éléments membres d’une [collection de ressources Sling](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/resource/collection/ResourceCollection.html) spécifique.

Il s’agit d’un prédicat de type filtrage seul qui ne peut pas utiliser d’index de recherche. Ne prend pas en charge l’extraction de facettes.

#### Propriétés {#properties-10}

* **memberOf**

  Chemin d’accès à la collection de ressources Sling.

### nodename {#nodename}

Correspond aux noms des noeuds JCR.

Prend en charge l’extraction de facettes. Fournit des compartiments pour chaque nom de nœud unique (nom de fichier).

#### Propriétés {#properties-11}

* **nodename**

  Modèle de nom de nœud qui autorise les caractères génériques : `*` = n’importe quel caractère, ou aucun, `?` = n’importe quel caractère, `[abc]` = uniquement les caractères entre crochets.

### notexpired {#notexpired}

Met en correspondance des éléments en vérifiant si une propriété DATE JCR est supérieure ou égale à l’heure actuelle du serveur. Ce prédicat peut être utilisé pour effectuer une vérification sur une propriété date de type « `expiresAt` » et se limiter uniquement à celles qui n’ont pas encore expiré (`notexpired=true`) ou qui ont déjà expiré (`notexpired=false`).

Ne prend pas en charge le filtrage.

Prend en charge l’extraction de facettes de la même manière que le prédicat.

#### Propriétés {#properties-12}

* **notexpired**

  Booléen, « `true` » pour les propriétés qui n’ont pas encore expiré (date future ou égale à celle indiquée), « `false` » pour les propriétés qui ont expiré (date dans le passé) (obligatoire).

* **property**

  Chemin d’accès relatif à la propriété `DATE` à vérifier (obligatoire).

### orderby {#orderby}

Permet de trier les résultats. Si un classement basé sur plusieurs propriétés est requis, ce prédicat doit être ajouté plusieurs fois à l’aide du préfixe numérique, tel que `1_orderby=first`, `2_oderby=second`.

#### Propriétés {#properties-13}

* **orderby**

  Nom de propriété JCR indiqué par un caractère @ en début, par exemple : `@jcr:lastModified` ou `@jcr:content/jcr:title`ou un autre prédicat dans la requête, par exemple : `2_property`, sur laquelle trier.

* **sort**

  Sens du tri, soit « `desc` » pour décroissant, soit « `asc` » pour croissant (valeur par défaut).

* **case**

  Si cette valeur est définie sur « `ignore` », le tri ne respecte pas la casse, ce qui signifie que « a » vient avant « B »; si cette valeur est vide ou ignorée, le tri respecte la casse, ce qui signifie que « B » vient avant « a ».

### path {#path}

Recherche dans un chemin donné.

Ne prend pas en charge l’extraction de facettes.

#### Propriétés {#properties-14}

* **path**

  Modèle de chemin. Selon la propriété exacte, soit l’ensemble de la sous-arborescence correspond (revient à ajouter `//*` dans xpath, mais notez que cela n’inclut pas le chemin de base), ou seulement un chemin d’accès exact correspond, lequel peut inclure des caractères génériques (`*`) ; si la valeur self est définie, la recherche portera sur l’ensemble de la sous-arborescence, y compris le nœud de base.

* **exact**

  Si la propriété `exact` est définie sur true/on, le chemin d’accès exact doit correspondre, mais il peut contenir des caractères génériques simples (`*`), qui correspondent aux noms, mais pas « `/` » ; si elle est définie sur false (par défaut) tous les descendants sont inclus (facultatif).

* **flat**

  Effectue uniquement des recherches dans les enfants directs (revient à ajouter « `/*` » dans xpath) (utilisé uniquement si « `exact` » n’est pas défini sur true, facultatif).

* **self**

  Effectue des recherches dans la sous-arborescence, mais inclut le nœud de base indiqué comme chemin d’accès (pas de caractères génériques).

### property {#property}

Met en correspondance des propriétés JCR et leurs valeurs.

Prend en charge l’extraction de facettes. Fournit des compartiments pour chaque valeur de propriété dans les résultats.

#### Propriétés {#properties-15}

* **property**

  Chemin d’accès relatif à la propriété, par exemple : `jcr:title`.

* **value**

  Valeur dont la propriété doit être vérifiée ; suit le type de propriété JCR pour les conversions de chaînes.

* **N_value**

  Utilisez `1_value`, `2_value`, ... pour rechercher plusieurs valeurs (combinées avec `OR` par défaut, avec `AND` si et=true) (à partir de la version 5.3).

* **and**

  Définissez cette valeur sur true pour combiner plusieurs valeurs (`N_value`) avec AND (à partir de la version 5.3).

* **operation**

  « `equals` » pour une correspondance exacte (par défaut), « `unequals` » pour la comparaison des inégalités,« `like` » pour utiliser la fonction xpath `jcr:like` (facultatif), « `not` » pour aucune correspondance (par exemple, « `not(@prop)` » dans xpath, le paramètre value est ignoré) ou « `exists` » pour la vérification de l’existence (la valeur peut être true – la propriété doit exister, par défaut – ou false – comme « `not` »).

* **depth**

  Nombre de niveaux de caractères génériques sous lesquels le chemin de propriété/relatif peut exister (par exemple, `property=size depth=2` vérifie le nœud/la taille, le nœud/&amp;ast;/taille et le nœud/&amp;ast;/&amp;ast;/taille).

### rangeproperty {#rangeproperty}

Met en correspondance une propriété JCR par rapport à un intervalle. Ce prédicat s’applique à des propriétés de type linéaire telles que `LONG`, `DOUBLE` et `DECIMAL`. Pour `DATE`, reportez-vous au prédicat daterange qui présente une entrée de format de date optimisée.

Vous pouvez définir une limite inférieure et une limite supérieure ou seulement l’une d’elles. L’opération (par exemple, « inférieure à », ou « inférieure ou égale à ») peut également être spécifiée individuellement pour les limites inférieure et supérieure.

Ne prend pas en charge l’extraction de facettes.

#### Propriétés {#properties-16}

* **property**

  Chemin d’accès relatif à la propriété.

* **lowerBound**

  Limite inférieure pour laquelle la propriété doit être vérifiée.

* **lowerOperation**

  « `>` » (par défaut) ou « `>=` », s’applique à `lowerValue`.

* **upperBound**

  Limite supérieure pour laquelle la propriété doit être vérifiée.

* **upperOperation**

  « `<` » (par défaut) ou « `<=` », s’applique à `lowerValue`.

* **decimal**

  « `true` » si la propriété vérifiée est de type Décimal

### relativedaterange {#relativedaterange}

Fait correspondre les propriétés `JCR DATE` par rapport à un intervalle de date/heure à l’aide de décalages temporels relatifs à l’heure actuelle du serveur. Vous pouvez spécifier `lowerBound` et `upperBound` en utilisant une valeur en millisecondes ou la syntaxe bugzilla `1s 2m 3h 4d 5w 6M 7y` (une seconde, deux minutes, trois heures, quatre jours, cinq semaines, six mois, sept ans). Préfixe avec « `-` » pour indiquer un décalage négatif avant l’heure actuelle. Si vous spécifiez uniquement `lowerBound` ou `upperBound`, l’autre propriété est définie par défaut sur 0, ce qui signifie l’heure actuelle.

Par exemple :

* `upperBound=1h` (et pas de `lowerBound`) sélectionnerait tous les éléments dans l’heure suivante.
* `lowerBound=-1d` (et pas de `upperBound`) sélectionnerait tous les éléments dans les dernières 24 heures.
* `lowerBound=-6M` et `upperBound=-3M` sélectionneraient tous les éléments entre 6 mois et 3 mois.
* `lowerBound=-1500` et `upperBound=5500` sélectionneraient tous les éléments entre 1 500 millisecondes dans le passé et 5 500 millisecondes dans le futur.
* `lowerBound=1d` et `upperBound=2d` sélectionneraient tous les éléments du jour d’après-demain ;

Il ne tient pas compte des années bissextiles et tous les mois comptent 30 jours.

Ne prend pas en charge le filtrage.

Prend en charge l’extraction de facettes de la même manière que le prédicat.

#### Propriétés {#properties-17}

* **upperBound**

  Limite de date supérieure en millisecondes ou `1s 2m 3h 4d 5w 6M 7y` (une seconde, deux minutes, trois heures, quatre jours, cinq semaines, six mois, sept ans) par rapport à l’heure actuelle du serveur ; utilisez « - » pour un décalage négatif.

* **lowerBound**

  Limite de date inférieure en millisecondes ou `1s 2m 3h 4d 5w 6M 7y` (une seconde, deux minutes, trois heures, quatre jours, cinq semaines, six mois, sept ans) par rapport à l’heure actuelle du serveur ; utilisez « - » pour un décalage négatif.

### root {#root}

Groupe de prédicats racine. Prend en charge toutes les fonctionnalités d’un groupe et vous permet de définir des paramètres de requête globaux.

Le nom &quot;root&quot; n’est jamais utilisé dans une requête, il est implicite.

#### Propriétés {#properties-18}

* **p.offset**

  Nombre indiquant le début de la page de résultats, c’est-à-dire le nombre d’éléments à ignorer.

* **p.limit**

  Nombre indiquant la taille de la page.

* **p.guessTotal**

  Recommandé : évitez de calculer le total des résultats qui peut s’avérer coûteux ; soit un nombre indiquant le total maximum à comptabiliser (par exemple, 1 000, un nombre qui donne aux utilisateurs suffisamment de commentaires sur la taille brute et les nombres exacts pour des résultats plus modestes), soit &quot; `true`&quot; pour ne compter que le minimum nécessaire `p.offset` + `p.limit`.

* **p.excerpt**

  Si la valeur est définie sur « `true` », l’extrait de texte complet est inclus dans les résultats.

* **p.hits**

   (uniquement pour le servlet JSON) Sélectionne la manière dont les accès sont écrits au format JSON, avec ces éléments standard (extensibles via le service ResultHitWriter) :

   * **simple** :

     Éléments minimaux tels que `path`, `title`, `lastmodified`, `excerpt` (s’ils sont définis).

   * **full** :

     Rendu JSON Sling du nœud, avec `jcr:path` qui indique le chemin de l’accès : par défaut, seules les propriétés directes du nœud sont répertoriées, inclure une arborescence plus profonde avec `p.nodedepth=N`, 0 signifiant l’ensemble de la sous-arborescence infinie ; ajouter `p.acls=true` pour inclure les autorisations JCR de la session en cours sur l’élément de résultat donné (mappages : `create` = `add_node`, `modify` = `set_property`, `delete` = `remove`).

   * **selective** :

     Uniquement les propriétés spécifiées dans `p.properties`, à savoir une liste de chemins d’accès relatifs séparés par des espaces (utiliser « + » dans les URL) ; si le chemin d’accès relatif a une profondeur > 1, ils seront représentés sous la forme d’objets enfants ; la propriété jcr:path spéciale inclut le chemin de l’accès.

### savedquery {#savedquery}

Inclut tous les prédicats d’une requête Query Builder persistante dans la requête actuelle sous la forme d’un prédicat de sous-groupe.

Il n’exécute pas de requête supplémentaire, mais étend la requête actuelle.

Les requêtes peuvent être conservées par programmation à l’aide de `QueryBuilder#storeQuery()`. Ce format peut être soit une propriété String multiligne, soit un nœud `nt:file` contenant la requête en tant que fichier texte au format des propriétés Java™.

Ne prend pas en charge l’extraction de facettes pour les prédicats de la requête enregistrée.

#### Propriétés {#properties-19}

* **savedquery**

  Chemin d’accès à la requête enregistrée (propriété String ou nœud `nt:file`).

### similar {#similar}

Recherche par analogie à l’aide du `rep:similar()` du Xpath JCR.

Ne prend pas en charge le filtrage. Ne prend pas en charge l’extraction de facettes.

#### Propriétés {#properties-20}

* **similar**
Chemin d’accès absolu au nœud pour lequel des nœuds similaires sont recherchés.

* **local**
Un chemin relatif vers un nœud descendant ou `.` pour le nœud actif (facultatif, la valeur par défaut est« `.` »).

### tag {#tag}

Recherche du contenu identifié avec une ou plusieurs balises, en spécifiant les chemins d’accès aux titres des balises.

Prend en charge l’extraction de facettes. Fournit des compartiments pour chaque balise, en utilisant le chemin d’accès vers le titre de balise active.

#### Propriétés {#properties-21}

* **tag**

  Chemin d’accès au titre de la balise à rechercher, par exemple, &quot;Propriétés de la ressource : orientation/paysage&quot;.

* **N_value**

  Utilisez `1_value`, `2_value`, ... pour rechercher plusieurs balises (combinées avec `OR` par défaut, avec `AND` si et=true) (depuis la version 5.6).

* **property**

  Propriété (ou chemin d’accès relatif à la propriété) à examiner (par défaut : « `cq:tags` »)

### tagid {#tagid}

Recherche du contenu identifié avec une ou plusieurs balises, en spécifiant les chemins d’accès aux ID des balise.

Prend en charge l’extraction de facettes. Fournit des compartiments pour chaque balise, en utilisant le chemin d’accès à l’ID de la balise active.

#### Propriétés {#properties-22}

* **tagid**

  Identifiant de balise afin que vous puissiez rechercher, par exemple, &quot; `properties:orientation/landscape`&quot;.

* **N_value**

  Utilisez `1_value`, `2_value`, ... pour rechercher plusieurs ID de balise (combinés avec `OR` par défaut, avec `AND` si et=true) (à partir de la version 5.6).

* **property**

  Propriété (ou chemin d’accès relatif à la propriété) à examiner (par défaut : « `cq:tags` »).

### tagsearch {#tagsearch}

Recherche du contenu identifié avec une ou plusieurs balises, en spécifiant des mots-clés. Cette action recherche d’abord les balises dont les titres contiennent ces mots clés, puis limite les résultats aux seuls éléments balisés de la sorte.

Ne prend pas en charge l’extraction de facettes.

#### Propriétés {#Properties-1}

* **tagsearch**

  Mot-clé à rechercher dans les titres de nœud.

* **property**

  Propriété (ou chemin d’accès relatif à la propriété) à examiner (par défaut `cq:tags`).

* **lang**

  Pour rechercher uniquement dans un titre de balise localisé donné (par exemple, `de`).

* **all**

  (bool) Recherchez le texte intégral d’une balise, c’est-à-dire tous les titres, la description, etc. Prévaut sur &quot;l&quot; `ang`&quot;.

### type {#type}

Limite les résultats à un type de nœud JCR spécifique, aussi bien pour les types de nœuds primaires que de mixin. Cette action trouve également des sous-types de ce type de nœud. Les index de recherche de référentiel doivent couvrir les types de nœuds pour une exécution efficace.

Prend en charge l’extraction de facettes. Fournit des compartiments pour chaque type unique dans les résultats.

#### Propriétés {#Properties-2}

* **type**

  Type de noeud ou nom de mixin à rechercher, par exemple : `cq:Page`.
