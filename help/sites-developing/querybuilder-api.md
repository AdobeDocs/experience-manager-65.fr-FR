---
title: API Query Builder
description: La fonctionnalité du générateur de requêtes de partage de ressources est exposée par le biais d’une API Java™ et d’une API REST.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
pagetitle: Query Builder API
tagskeywords: querybuilder
exl-id: b2288442-d055-4966-8057-8b7b7b6bff28
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2033'
ht-degree: 67%

---

# API Query Builder{#query-builder-api}

La fonctionnalité de la variable [Générateur de requêtes de partage de ressources](/help/assets/assets-finder-editor.md) est exposé par le biais d’une API Java™ et d’une API REST. Cette section décrit ces API.

Créateur de requêtes côté serveur ( [`QueryBuilder`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html)) accepte une description de requête, crée et exécute une requête XPath, filtre éventuellement le jeu de résultats et extrait également les facettes, le cas échéant.

La description de requête correspond simplement à un ensemble de prédicats ([`Predicate`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/Predicate.html)). Par exemple, un prédicat de texte intégral correspond à la fonction `jcr:contains()` dans XPath.

Pour chaque type de prédicat, il existe un composant Évaluateur ([`PredicateEvaluator`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/PredicateEvaluator.html)) qui sait comment en effectuer la gestion pour XPath, pour le filtrage et pour l’extraction de facettes. Il est facile de créer des évaluateurs personnalisés, qui sont connectés via l’exécution du composant OSGi.

L’API REST permet d’accéder aux mêmes fonctionnalités via HTTP avec les réponses envoyées dans JSON.

>[!NOTE]
>
>L’API QueryBuilder est créée à l’aide de l’API JCR. Vous pouvez également interroger le JCR Adobe Experience Manager à l’aide de l’API JCR depuis un lot OSGi. Pour plus d’informations, voir [Adobe Experience Manager à l’aide de l’API JCR](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/access-jcr.html).

## Session Gem {#gem-session}

[Astuces pour Adobe Experience Manager (AEM)](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/overview.html?lang=fr) est une série de séances approfondies sur Adobe Experience Manager réalisées par des experts en Adobe. Cette session dédiée au Query Builder est utile pour une vue d’ensemble et l’utilisation de l’outil.

>[!NOTE]
>
>AEM session Gem [Formulaires de recherche simplifiés avec AEM querybuilder](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2017/aem-search-forms-using-querybuilder.html?lang=fr) pour une présentation détaillée de query builder.

## Exemples de requêtes {#sample-queries}

Ces exemples sont fournis dans la notation de style des propriétés Java™. Pour les utiliser avec l’API Java™, utilisez une `HashMap` Java™ comme dans l’exemple d’API suivant.

Pour le servlet JSON `QueryBuilder`, chaque exemple comprend un lien vers votre installation CQ locale (à l’emplacement par défaut, `http://localhost:4502`). Connectez-vous à votre instance CQ avant d’utiliser ces liens.

>[!CAUTION]
>
>Par défaut, le servlet json du Query Builder affiche un maximum de dix accès.
>
>L’ajout du paramètre suivant permet au servlet d’afficher tous les résultats de la requête :
>
>**`p.limit=-1`**

>[!NOTE]
>
>Pour afficher les données JSON renvoyées dans votre navigateur, vous pouvez utiliser un plug-in tel que JSONView pour Firefox.

### Renvoi de tous les résultats {#returning-all-results}

La requête suivante **renvoyer dix résultats** (ou, pour être précis, un maximum de dix), mais informez-vous de la variable **Nombre d’accès :** qui sont disponibles :

`http://localhost:4502/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=foundation/components/text&1_property.operation=like&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=foundation/components/text
1_property.operation=like
orderby=path
```

La même requête (avec le paramètre `p.limit=-1`) **renvoie tous les résultats** (il peut s’agir d’un nombre élevé en fonction de votre instance) :

`http://localhost:4502/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=foundation/components/text&1_property.operation=like&p.limit=-1&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=foundation/components/text
1_property.operation=like
p.limit=-1
orderby=path
```

### Utilisation de p.guessTotal pour renvoyer les résultats {#using-p-guesstotal-to-return-the-results}

L’objet de la variable `p.guessTotal` est de renvoyer le nombre approprié de résultats pouvant être affichés en combinant les valeurs minimum p.offset et p.limit viables. Utilisé avec des jeux de résultats de grande taille, ce paramètre offre des performances encore meilleures. Cela permet d’éviter de calculer le total (par exemple, en appelant result.getSize()) et de lire l’ensemble de résultats, optimisé jusqu’au moteur et à l’index Oak. Il peut s’agir d’une différence significative lorsqu’il y a 100 000 résultats, à la fois en termes de temps d’exécution et d’utilisation de la mémoire.

L’inconvénient de ce paramètre est que les utilisateurs ne voient pas le total exact. Cependant, vous pouvez définir un nombre minimum comme p.guessTotal=1000 afin qu’il soit toujours lu jusqu’à 1 000, de sorte que vous obtenez des totaux exacts pour les jeux de résultats plus petits, mais s’il est plus grand, vous pouvez uniquement afficher &quot;et plus&quot;.

Ajoutez `p.guessTotal=true` à la requête ci-dessous pour voir comment cela fonctionne :

`http://localhost:4502/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=foundation/components/text&1_property.operation=like&p.guessTotal=true&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=foundation/components/text
1_property.operation=like
p.guessTotal=true
orderby=path
```

La requête renvoie la valeur `p.limit` par défaut de `10` résultats avec un décalage de `0` :

```xml
"success": true,
"results": 10,
"total": 10,
"more": true,
"offset": 0,
```

Depuis AEM 6.0 SP2, vous pouvez également utiliser une valeur numérique pour compter jusqu’à un nombre personnalisé de résultats maximums. Utilisez la même requête que ci-dessus, mais définissez la valeur de `p.guessTotal` sur `50` :

`http://localhost:4502/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=foundation/components/text&1_property.operation=like&p.guessTotal=50&orderby=path`

Elle renvoie un nombre correspondant à la même limite par défaut de dix résultats avec un décalage de 0, mais affiche uniquement un maximum de 50 résultats :

```xml
"success": true,
"results": 10,
"total": 50,
"more": true,
"offset": 0,
```

### Implémentation de la pagination {#implementing-pagination}

Par défaut, Query Builder fournit également le nombre d’accès. Selon la taille du résultat, cette opération peut prendre un certain temps, car déterminer le nombre exact implique de vérifier chaque résultat pour le contrôle d’accès. Le total est principalement utilisé pour implémenter la pagination pour l’interface utilisateur de l’utilisateur final. Étant donné que la détermination du nombre exact peut être lente, il est recommandé d’utiliser la fonction guessTotal pour mettre en oeuvre la pagination.

Par exemple, l’interface utilisateur peut adapter l’approche suivante :

* Obtenez et affichez le nombre exact d’accès totaux ([SearchResult.getTotalMatches()](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/result/SearchResult.html#gettotalmatches) ou le total dans la réponse querybuilder.json) qui est inférieur ou égal à 100 ;
* Définissez `guessTotal` sur 100 tout en effectuant l’appel vers Query Builder.

* La réponse peut générer le résultat suivant :

   * `total=43`, `more=false` – Indique que le nombre total d’accès est de 43. L’interface utilisateur peut afficher jusqu’à dix résultats dans le cadre de la première page et fournir la pagination pour les trois pages suivantes. Vous pouvez également utiliser cette implémentation pour afficher un texte descriptif tel que **« 43 résultats trouvés »**.
   * `total=100`, `more=true` – Indique que le nombre total d’accès est supérieur à 100 et que le nombre exact est inconnu. L’interface utilisateur peut afficher jusqu’à dix résultats dans le cadre de la première page et fournir la pagination pour les dix pages suivantes. Vous pouvez également l’utiliser pour afficher du texte comme **&quot;plus de 100 résultats trouvés&quot;**. Lorsque l’utilisateur accède aux pages suivantes, les appels effectués vers Query Builder augmentent la limite de `guessTotal`, ainsi que celle des paramètres `offset` et `limit`.

`guessTotal` doit être utilisé lorsque l’interface utilisateur doit utiliser le défilement infini pour éviter que Query Builder ne détermine le nombre exact d’accès.

### Recherche et classement des fichiers JAR, en commençant par le plus récent {#find-jar-files-and-order-them-newest-first}

`http://localhost:4502/bin/querybuilder.json?type=nt:file&nodename=*.jar&orderby=@jcr:content/jcr:lastModified&orderby.sort=desc`

```xml
type=nt:file
nodename=*.jar
orderby=@jcr:content/jcr:lastModified
orderby.sort=desc
```

### Recherche de toutes les pages et classement par date de la dernière modification {#find-all-pages-and-order-them-by-last-modified}

`http://localhost:4502/bin/querybuilder.json?type=cq:Page&orderby=@jcr:content/cq:lastModified`

```xml
type=cq:Page
orderby=@jcr:content/cq:lastModified
```

### Recherche de toutes les pages et classement par date de la dernière modification, mais par ordre décroissant {#find-all-pages-and-order-them-by-last-modified-but-descending}

`http://localhost:4502/bin/querybuilder.json?type=cq:Page&orderby=@jcr:content/cq:lastModified&orderby.sort=desc]`

```xml
type=cq:Page
orderby=@jcr:content/cq:lastModified
orderby.sort=desc
```

### Recherche en texte intégral, avec classement par score {#fulltext-search-ordered-by-score}

`http://localhost:4502/bin/querybuilder.json?fulltext=Management&orderby=@jcr:score&orderby.sort=desc`

```xml
fulltext=Management
orderby=@jcr:score
orderby.sort=desc
```

### Recherche des pages présentant une balise donnée {#search-for-pages-tagged-with-a-certain-tag}

`http://localhost:4502/bin/querybuilder.json?type=cq:Page&tagid=marketing:interest/product&tagid.property=jcr:content/cq:tags`

```xml
type=cq:Page
tagid=marketing:interest/product
tagid.property=jcr:content/cq:tags
```

Utilisez le prédicat `tagid`, comme dans l’exemple, si vous connaissez l’ID de balise explicite.

Utilisez le prédicat `tag` pour le chemin d’accès au titre de la balise (sans espaces).

Dans l’exemple précédent, car vous recherchez des pages ( `cq:Page` ), utilisez le chemin d’accès relatif à partir de ce noeud pour la variable `tagid.property` prédicat, qui est `jcr:content/cq:tags`. Par défaut, le prédicat `tagid.property` est simplement `cq:tags`.

### Recherche dans plusieurs chemins d’accès (à l’aide de groupes) {#search-under-multiple-paths-using-groups}

`http://localhost:4502/bin/querybuilder.json?fulltext=Management&group.1_path=/content/geometrixx/en/company/management&group.2_path=/content/geometrixx/en/company/bod&group.p.or=true`

```xml
fulltext=Management
group.p.or=true
group.1_path=/content/geometrixx/en/company/management
group.2_path=/content/geometrixx/en/company/bod
```

Cette requête utilise un *groupe* (appelé « `group` »), qui sert à délimiter les sous-expressions dans une requête, à l’instar des parenthèses dans des notations plus standard. Par exemple, la requête précédente peut être exprimée dans un style plus familier comme suit :

`"Management" and ("/content/geometrixx/en/company/management" or "/content/geometrixx/en/company/bod")`

Le prédicat `path` est utilisé à plusieurs reprises dans le groupe de l’exemple précédent. Pour différencier et classer les deux instances du prédicat (un classement est requis pour certains prédicats), vous devez faire précéder les prédicats de *N* où `_ where`*N* est l’index de classement. Dans l’exemple précédent, les prédicats obtenus sont `1_path` et `2_path`.

Le `p` dans `p.or` est un délimiteur spécial qui indique que ce qui suit (dans ce cas, `or`) est un *paramètre* du groupe, par opposition à un sous-prédicat du groupe, tel que `1_path`.

Si aucun `p.or` n’est indiqué, tous les prédicats sont associés avec AND ; en d’autres termes, chaque résultat doit répondre à l’ensemble des prédicats.

>[!NOTE]
>
>Vous ne pouvez pas utiliser le même préfixe numérique dans une seule requête, même pour des prédicats différents.

### Recherche de propriétés {#search-for-properties}

Dans ce cas, vous recherchez toutes les pages d’un modèle donné, à l’aide de la propriété `cq:template` :

`http://localhost:4502/bin/querybuilder.json?property=cq%3atemplate&property.value=%2fapps%2fgeometrixx%2ftemplates%2fhomepage&type=cq%3aPageContent`

```xml
type=cq:PageContent
property=cq:template
property.value=/apps/geometrixx/templates/homepage
```

L’inconvénient est que les nœuds `jcr:content` des pages sont renvoyés, et non les pages proprement dites. Pour remédier à ce problème, vous pouvez effectuer une recherche par chemin d’accès relatif :

`http://localhost:4502/bin/querybuilder.json?property=jcr%3acontent%2fcq%3atemplate&property.value=%2fapps%2fgeometrixx%2ftemplates%2fhomepage&type=cq%3aPage`

```xml
type=cq:Page
property=jcr:content/cq:template
property.value=/apps/geometrixx/templates/homepage
```

### Recherche de plusieurs propriétés {#search-for-multiple-properties}

Lorsque vous utilisez plusieurs fois le prédicat property, vous devez ajouter à nouveau les préfixes numériques :

`http://localhost:4502/bin/querybuilder.json?1_property=jcr%3acontent%2fcq%3atemplate&1_property.value=%2fapps%2fgeometrixx%2ftemplates%2fhomepage&2_property=jcr%3acontent%2fjcr%3atitle&2_property.value=English&type=cq%3aPage`

```xml
type=cq:Page
1_property=jcr:content/cq:template
1_property.value=/apps/geometrixx/templates/homepage
2_property=jcr:content/jcr:title
2_property.value=English
```

### Recherche de plusieurs valeurs de propriété {#search-for-multiple-property-values}

Pour éviter les groupes de grande taille lorsque vous souhaitez rechercher plusieurs valeurs d’une propriété ( `"A" or "B" or "C"`), vous pouvez fournir plusieurs valeurs à la variable `property` prédicat :

`http://localhost:4502/bin/querybuilder.json?property=jcr%3atitle&property.1_value=Products&property.2_value=Square&property.3_value=Events`

```xml
property=jcr:title
property.1_value=Products
property.2_value=Square
property.3_value=Events
```

Pour les propriétés à plusieurs valeurs, vous pouvez également exiger que plusieurs valeurs correspondent (`"A" and "B" and "C"`) :

`http://localhost:4502/bin/querybuilder.json?property=jcr%3atitle&property.and=true&property.1_value=test&property.2_value=foo&property.3_value=bar`

```xml
property=jcr:title
property.and=true
property.1_value=test
property.2_value=foo
property.3_value=bar
```

## Amélioration des propriétés renvoyées {#refining-what-is-returned}

Par défaut, le servlet JSON QueryBuilder renvoie un jeu de propriétés par défaut pour chaque nœud dans les résultats de recherche (par exemple, chemin d’accès, nom et titre). Pour contrôler les propriétés renvoyées, vous pouvez effectuer l’une des opérations suivantes :

Spécifiez

```
p.hits=full
```

Dans ce cas, toutes les propriétés sont incluses pour chaque nœud :

`http://localhost:4502/bin/querybuilder.json?p.hits=full&property=jcr%3atitle&property.value=Triangle`

```xml
property=jcr:title
property.value=Triangle
p.hits=full
```

Utilisez

```
p.hits=selective
```

Et spécifiez les propriétés à intégrer

```
p.properties
```

Séparées par un espace :

`http://localhost:4502/bin/querybuilder.json?p.hits=selective&property=jcr%3atitle&property.value=Triangle`

[`http://localhost:4502/bin/querybuilder.json?`](http://localhost:4502/bin/querybuilder.json?p.hits=selective&amp;p.properties=sling%3aresourceType%20jcr%3aprimaryType&amp;property=jcr%3atitle&amp;property.value=Triangle) [p.hits=sélective&amp;](http://localhost:4502/bin/querybuilder.json?p.hits=selective&amp;p.nodedepth=5&amp;p.properties=sling%3aresourceType%20jcr%3apath&amp;property=jcr%3atitle&amp;property.value=Triangle)p.properties=sling%3aresourceType%20jcr%3aprimaryType&amp;property=jcr%3atitle&amp;property.value=Triangle

```xml
property=jcr:title
property.value=Triangle
p.hits=selective
p.properties=sling:resourceType jcr:primaryType
```

Vous pouvez également inclure des nœuds enfants dans la réponse de QueryBuilder. Pour cela, vous devez indiquer

```
p.nodedepth=n
```

Où `n` correspond au nombre de niveaux que la requête doit renvoyer. Pour qu’un nœud enfant soit renvoyé, il doit être spécifié par le sélecteur de propriétés

```
p.hits=full
```

Exemple :

`http://localhost:4502/bin/querybuilder.json?p.hits=full&p.nodedepth=5&property=jcr%3atitle&property.value=Triangle`

```xml
property=jcr:title
property.value=Triangle
p.hits=full
p.nodedepth=5
```

## Plus de prédicats {#morepredicates}

Pour plus de prédicats, consultez la [page de référence des prédicats de Query Builder](/help/sites-developing/querybuilder-predicate-reference.md).

Vous pouvez également consulter le [JavaDoc relatif aux `PredicateEvaluator`classes](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/PredicateEvaluator.html). Ce JavaDoc contient la liste des propriétés que vous pouvez utiliser.

Le préfixe du nom de classe (par exemple, « `similar` » dans [`SimilarityPredicateEvaluator`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/SimilarityPredicateEvaluator.html)), est la *propriété principale* de la classe. Cette propriété est également le nom du prédicat à utiliser dans la requête (en minuscules).

Pour ces propriétés principales, vous pouvez raccourcir la requête et utiliser `similar=/content/en` au lieu de la variante complète « `similar.similar=/content/en` ». La forme complète doit être utilisée pour toutes les propriétés non principales d’une classe.

## Exemple d’utilisation de l’API Query Builder {#example-query-builder-api-usage}

```java
   String fulltextSearchTerm = "Geometrixx";

    // create query description as hash map (simplest way, same as form post)
    Map<String, String> map = new HashMap<String, String>();

// create query description as hash map (simplest way, same as form post)
    map.put("path", "/content");
    map.put("type", "cq:Page");
    map.put("group.p.or", "true"); // combine this group with OR
    map.put("group.1_fulltext", fulltextSearchTerm);
    map.put("group.1_fulltext.relPath", "jcr:content");
    map.put("group.2_fulltext", fulltextSearchTerm);
    map.put("group.2_fulltext.relPath", "jcr:content/@cq:tags");

    // can be done in map or with Query methods
    map.put("p.offset", "0"); // same as query.setStart(0) below
    map.put("p.limit", "20"); // same as query.setHitsPerPage(20) below

    Query query = builder.createQuery(PredicateGroup.create(map), session);
    query.setStart(0);
    query.setHitsPerPage(20);

    SearchResult result = query.getResult();

    // paging metadata
    int hitsPerPage = result.getHits().size(); // 20 (set above) or lower
    long totalMatches = result.getTotalMatches();
    long offset = result.getStartIndex();
    long numberOfPages = totalMatches / 20;

    //Place the results in XML to return to client
    DocumentBuilderFactory factory =     DocumentBuilderFactory.newInstance();
    DocumentBuilder builder = factory.newDocumentBuilder();
    Document doc = builder.newDocument();

    //Start building the XML to pass back to the AEM client
    Element root = doc.createElement( "results" );
    doc.appendChild( root );

    // iterating over the results
    for (Hit hit : result.getHits()) {
       String path = hit.getPath();

      //Create a result element
      Element resultel = doc.createElement( "result" );
      root.appendChild( resultel );

      Element pathel = doc.createElement( "path" );
      pathel.appendChild( doc.createTextNode(path ) );
      resultel.appendChild( pathel );
    }
```

>[!NOTE]
>
>Pour savoir comment créer un lot OSGi qui utilise l’API QueryBuilder et utiliser ce lot OSGi dans une application Adobe Experience Manager, voir [Création de lots OSGi Adobe CQ qui utilisent l’API Query Builder](https://helpx.adobe.com/experience-manager/using/using-query-builder-api.html)I.

La même requête exécutée sur HTTP à l’aide du servlet Query Builder (JSON) :

`http://localhost:4502/bin/querybuilder.json?path=/content&type=cq:Page&group.p.or=true&group.1_fulltext=Geometrixx&group.1_fulltext.relPath=jcr:content&group.2_fulltext=Geometrixx&group.2_fulltext.relPath=jcr:content/@cq:tags&p.offset=0&p.limit=20`

## Stocker et charger des requêtes {#storing-and-loading-queries}

Les requêtes peuvent être stockées dans le référentiel de manière à pouvoir les utiliser ultérieurement. `QueryBuilder` fournit la méthode `storeQuery` avec la signature suivante :

```java
void storeQuery(Query query, String path, boolean createFile, Session session) throws RepositoryException, IOException;
```

Si vous utilisez la méthode [`QueryBuilder#storeQuery`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html#storequerycomdaycqsearchqueryjavalangstringbooleanjavaxjcrsession), la `Query` donnée est stockée dans le référentiel sous la forme d’un fichier ou d’une propriété suivant la valeur de l’argument `createFile`. L’exemple suivant illustre l’enregistrement d’une `Query` sous `/mypath/getfiles` en tant que fichier :

```java
builder.storeQuery(query, "/mypath/getfiles", true, session);
```

Toutes les requêtes stockées précédemment peuvent être chargées à partir du référentiel en utilisant la méthode [`QueryBuilder#loadQuery`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html#loadqueryjavalangstringjavaxjcrsession) :

```java
Query loadQuery(String path, Session session) throws RepositoryException, IOException
```

Par exemple, une `Query` stockée sous `/mypath/getfiles` peut être chargée par l’extrait de code suivant :

```java
Query loadedQuery = builder.loadQuery("/mypath/getfiles", session);
```

## Tests et débogage {#testing-and-debugging}

Pour lire et déboguer des requêtes QueryBuilder, vous pouvez utiliser la console du débogueur QueryBuilder à l’adresse

`http://localhost:4502/libs/cq/search/content/querydebug.html`

Ou bien le servlet json de Query Builder à l’adresse

`http://localhost:4502/bin/querybuilder.json?path=/tmp`

(`path=/tmp` est donné uniquement à titre d’exemple).

### Recommandations générales en matière de débogage {#general-debugging-recommendations}

### Obtention d’un XPath explicable via la journalisation {#obtain-explain-able-xpath-via-logging}

Expliquez **toutes** les requêtes au cours du cycle de développement par rapport à l’ensemble d’index cible.

* Activez les journaux de débogage pour QueryBuilder afin d’obtenir une requête XPath explicable sous-jacente

   * Accédez à https://&lt;serveraddress>:&lt;serverport>/system/console/slinglog. Créez un enregistreur pour `com.day.cq.search.impl.builder.QueryImpl` lors du **débogage**.

* Une fois que le débogage a été activé pour la classe ci-dessus, les journaux affichent la requête XPath générée par le générateur de requêtes.
* Copiez la requête XPath à partir de l’entrée de journal pour la requête QueryBuilder associée. Par exemple :

   * `com.day.cq.search.impl.builder.QueryImpl XPath query: /jcr:root/content//element(*, cq:Page)[(jcr:contains(jcr:content, "Geometrixx") or jcr:contains(jcr:content/@cq:tags, "Geometrixx"))]`

* Collez la requête XPath dans [Expliquer la requête](/help/sites-administering/operations-dashboard.md#explain-query) en tant que XPath afin d’obtenir le plan de requête.

### Obtention de XPath explicable via le débogueur Query Builder {#obtain-explain-able-xpath-via-the-query-builder-debugger}

* Utilisez le débogueur QueryBuilder AEM pour générer une requête XPath explicable :

Expliquez **toutes** les requêtes au cours du cycle de développement par rapport à l’ensemble d’index cible.

**Obtention d’un XPath explicable via la journalisation**

* Activez les journaux de débogage pour QueryBuilder afin d’obtenir une requête XPath explicable sous-jacente

   * Accédez à https://&lt;serveraddress>:&lt;serverport>/system/console/slinglog. Créez un enregistreur pour `com.day.cq.search.impl.builder.QueryImpl` lors du **débogage**.

* Une fois que le débogage a été activé pour la classe ci-dessus, les journaux affichent la requête XPath générée par le générateur de requêtes.
* Copiez la requête XPath à partir de l’entrée de journal pour la requête QueryBuilder associée. Par exemple :

   * `com.day.cq.search.impl.builder.QueryImpl XPath query: /jcr:root/content//element(*, cq:Page)[(jcr:contains(jcr:content, "Geometrixx") or jcr:contains(jcr:content/@cq:tags, "Geometrixx"))]`

* Collez la requête XPath dans [Expliquer la requête](/help/sites-administering/operations-dashboard.md#explain-query) en tant que XPath afin d’obtenir le plan de requête.

**Obtention de XPath explicable via le débogueur Query Builder**

* Utilisez le débogueur QueryBuilder AEM pour générer une requête XPath explicable :

![chlimage_1-66](assets/chlimage_1-66a.png)

1. Indiquez la requête Query Builder dans le débogueur Query Builder.
1. Exécutez la recherche
1. Obtenez le XPath généré
1. Collez la requête XPath dans Explain Query en tant que XPath afin d’obtenir le plan de requête

>[!NOTE]
>
>Les requêtes non Query Builder (XPath, JCR-SQL2) peuvent être fournies directement pour expliquer la requête.

Pour un aperçu de la procédure de débogage des requêtes avec QueryBuilder, reportez-vous à la vidéo ci-dessous.

>[!NOTE]
>
>[https://www.youtube.com/watch?v=BnyXjhRKYKc](https://www.youtube.com/watch?v=BnyXjhRKYKc)

## Débogage de requêtes à l’aide de la journalisation {#debugging-queries-with-logging}

>[!NOTE]
>
>La configuration des enregistreurs est décrite à la section [Création de vos propres enregistreurs et rédacteurs](/help/sites-deploying/configure-logging.md#creating-your-own-loggers-and-writers).

La sortie du journal (niveau INFO) de l’implémentation du Query Builder lors de l’exécution de la requête décrite dans Test et débogage :

```xml
com.day.cq.search.impl.builder.QueryImpl executing query (predicate tree):
null=group: limit=20, offset=0[
    {group=group: or=true[
        {1_fulltext=fulltext: fulltext=Geometrixx, relPath=jcr:content}
        {2_fulltext=fulltext: fulltext=Geometrixx, relPath=jcr:content/@cq:tags}
    ]}
    {path=path: path=/content}
    {type=type: type=cq:Page}
]
com.day.cq.search.impl.builder.QueryImpl XPath query: /jcr:root/content//element(*, cq:Page)[(jcr:contains(jcr:content, "Geometrixx") or jcr:contains(jcr:content/@cq:tags, "Geometrixx"))]
com.day.cq.search.impl.builder.QueryImpl no filtering predicates
com.day.cq.search.impl.builder.QueryImpl query execution took 69 ms
```

Dans le cas d’une requête qui utilise des évaluateurs de prédicats qui filtrent ou appliquent un ordre personnalisé par comparateur, cela est également indiqué dans la requête :

```xml
com.day.cq.search.impl.builder.QueryImpl executing query (predicate tree):
null=group: [
    {nodename=nodename: nodename=*.jar}
    {orderby=orderby: orderby=@jcr:content/jcr:lastModified}
    {type=type: type=nt:file}
]
com.day.cq.search.impl.builder.QueryImpl custom order by comparator: jcr:content/jcr:lastModified
com.day.cq.search.impl.builder.QueryImpl XPath query: //element(*, nt:file)
com.day.cq.search.impl.builder.QueryImpl filtering predicates: {nodename=nodename: nodename=*.jar}
com.day.cq.search.impl.builder.QueryImpl query execution took 272 ms
```

## Liens JavaDoc {#javadoc-links}

| **Javadoc** | **Description** |
|---|---|
| [com.day.cq.search](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/package-summary.html) | QueryBuilder de base et l’API Query |
| [com.day.cq.search.result](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/result/package-summary.html) | API Result |
| [com.day.cq.search.facets](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/facets/package-summary.html) | Facettes |
| [com.day.cq.search.facets.buckets](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/facets/buckets/package-summary.html) | Intervalles (contenus dans les facettes) |
| [com.day.cq.search.eval](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/package-summary.html) | Évaluateurs de prédicats |
| [com.day.cq.search.facets.extractors](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/facets/extractors/package-summary.html) | Extracteurs de facettes (pour les évaluateurs) |
| [com.day.cq.search.writer](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/writer/package-summary.html) | Auteur d’accès JSON Result pour le servlet Query Builder (/bin/querybuilder.json) |
