---
title: Essentials de recherche
seo-title: Essentials de recherche
description: Recherche dans les communautés
seo-description: Recherche dans les communautés
uuid: 5f35a033-2069-499e-9cdb-db25781312f0
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 300aa9f3-596f-42bc-8d46-e535f2bc4379
translation-type: tm+mt
source-git-commit: 6d425dcec4fab19243be9acb41c25b531a84ea74

---


# Essentials de recherche {#search-essentials}

## Présentation {#overview}

La fonction de recherche est une fonctionnalité essentielle des communautés AEM. Outre les fonctionnalités de recherche [de la plateforme](../../help/sites-deploying/queries-and-indexing.md) AEM, les communautés AEM fournissent l’API [de recherche](#ugc-search-api) UGC dans le but de rechercher du contenu généré par l’utilisateur (UGC). L’UGC possède des propriétés uniques puisqu’il est saisi et stocké séparément des autres données utilisateur et du contenu AEM.

Pour les communautés, les deux éléments généralement recherchés sont les suivants :

* Contenu publié par des membres de la communauté

   * Utilise l’API de recherche UGC des communautés AEM.

* Utilisateurs et groupes d’utilisateurs (données utilisateur)

   * Utilise les fonctionnalités de recherche de la plate-forme AEM.

Cette section de la documentation présente un intérêt pour les développeurs qui créent des composants personnalisés qui créent ou gèrent des composants UGC.

## Sécurité et noeuds fantômes {#security-and-shadow-nodes}

Pour un composant personnalisé, il est nécessaire d’utiliser les méthodes [SocialResourceUtilities](socialutils.md#socialresourceutilities-package) . Les méthodes d’utilitaire qui créent et recherchent l’UGC établissent les noeuds [d’](srp.md#about-shadow-nodes-in-jcr) ombre requis et garantissent que le membre dispose des autorisations appropriées pour la requête.

Ce qui n’est pas géré par les utilitaires SRP sont des propriétés liées à la modération.

Voir [SRP et UGC Essentials](srp-and-ugc.md) pour en savoir plus sur les méthodes d’utilitaire utilisées pour accéder aux noeuds fantômes UGC et ACL.

## API de recherche UGC {#ugc-search-api}

Le magasin [commun](working-with-srp.md) UGC est fourni par l&#39;un des nombreux fournisseurs de ressources  (SRP), chacun pouvant avoir une langue de native différente. Par conséquent, quel que soit le SRP choisi, le code personnalisé doit utiliser les méthodes du package [API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) UGC (*com.adobe.cq.social.ugc.api*) qui appellera le langage  approprié pour le SRP choisi.

### Recherches ASRP {#asrp-searches}

Pour [ASRP](asrp.md), l’UGC est stocké dans le cloud Adobe. Bien que l’UGC ne soit pas visible dans CRX, la [modération](moderate-ugc.md) est disponible à la fois auprès de l’auteur et de l’ de publication . L’utilisation de l’API [de recherche](#ugc-search-api) UGC fonctionne pour ASRP comme pour d’autres applications de recherche de type SRP.

Il n’existe actuellement aucun outil pour gérer les recherches ASRP.

Lors de la création de propriétés personnalisées pouvant faire l’objet de recherches, il est nécessaire de respecter les exigences [d’](#naming-of-custom-properties)appellation.

### Recherches MSRP {#msrp-searches}

Pour [MSRP](msrp.md), l’UGC est stocké dans MongoDB configuré pour utiliser Solr pour la recherche. L’UGC ne sera pas visible dans CRX, mais la [modération](moderate-ugc.md) est disponible à la fois auprès de l’auteur et de la publication  .

Concernant MSRP et Solr :

* Le Solr incorporé pour la plate-forme AEM n’est pas utilisé pour MSRP.
* Si vous utilisez un Solr distant pour la plate-forme AEM, il peut être partagé avec MSRP, mais vous devez utiliser des collections différentes.
* Solr peut être configuré pour la recherche standard ou pour la recherche multilingue (MLS).
* Pour plus d’informations sur la configuration, voir Configuration [](msrp.md#solr-configuration) Solr pour MSRP.

Les fonctions de recherche personnalisée doivent utiliser l’API [de recherche](#ugc-search-api)UGC.

Lors de la création de propriétés personnalisées pouvant faire l’objet de recherches, il est nécessaire de respecter les exigences [d’](#naming-of-custom-properties)appellation.

### Recherches JSRP {#jsrp-searches}

Pour [JSRP](jsrp.md), l’UGC est stocké dans [Oak](../../help/sites-deploying/platform.md) et n’est visible que dans le référentiel de l’instance d’auteur ou de publication AEM sur laquelle il a été saisi.

Etant donné que l’UGC est généralement saisi dans le  de publication , pour les systèmes de production à plusieurs éditeurs, il est nécessaire de configurer une grappe [de](topologies.md)publication, et non une batterie de publication, afin que le contenu saisi soit visible par tous les éditeurs.

Pour JSRP, l’UGC saisi dans le  de publication  ne sera jamais visible dans le  de de l’auteur. Ainsi, tous les  de [modération](moderate-ugc.md) ont lieu dans le  de publication.

Les fonctions de recherche personnalisée doivent utiliser l’API [de recherche](#ugc-search-api)UGC.

#### Indexation en chêne {#oak-indexing}

Bien que les indices Oak ne soient pas automatiquement créés pour la recherche de plateformes AEM, depuis AEM 6.2, ils ont été ajoutés pour que les communautés AEM améliorent les performances et prennent en charge la pagination lors de la présentation des résultats de recherche UGC.

Si les propriétés personnalisées sont utilisées et que les recherches sont lentes, des indices supplémentaires doivent être créés pour que les propriétés personnalisées soient plus performantes. Pour préserver la portabilité, respectez les exigences [d’](#naming-of-custom-properties) appellation lors de la création de propriétés personnalisées pouvant faire l’objet de recherches.

Pour modifier des indices existants ou créer des indices personnalisés, reportez-vous à la section  [Oak et indexation](../../help/sites-deploying/queries-and-indexing.md).

Le gestionnaire [d’index](https://adobe-consulting-services.github.io/acs-aem-commons/features/oak-index-manager.html) Oak est disponible à partir d’AEM Commons ACS. Il fournit :

*  d’indices existants.
* Possibilité de lancer la réindexation.

Pour  les indices Oak existants dans [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md), l’emplacement est le suivant :

* `/oak:index/socialLucene`

![chlimage_1-235](assets/chlimage_1-235.png)

## Propriétés de recherche indexée {#indexed-search-properties}

### Propriétés de recherche par défaut {#default-search-properties}

Vous trouverez ci-dessous quelques-unes des propriétés pouvant faire l’objet de recherches et utilisées pour différentes fonctionnalités de communautés :

| **Propriété** | **Type de données** |
|---|---|
| isFlagged | *Booléen* |
| isSpam | *Booléen* |
| lire | *Booléen* |
| influence | *Booléen* |
| attachments | *Booléen* |
| opinion | *Long* |
| marqué | *Booléen* |
| ajoutée | *Date* |
| modifyDate | *Date* |
| state | *Chaîne* |
| userIdentifier | *Chaîne* |
| réponses | *Long* |
| jcr:title | *Chaîne* |
| jcr:description | *Chaîne* |
| sling:resourceType | *Chaîne* |
| allowThreadedReply | *Booléen* |
| isDraft | *Booléen* |
| publishDate | *Date* |
| publishJobId | *Chaîne* |
| répondu | *Booléen* |
| chosena | *Booléen* |
| tag | *Chaîne* |
| cq:Tag | *Chaîne* |
| author_display_name | *Chaîne* |
| location_t | *Chaîne* |
| parentPath | *Chaîne* |
| parentTitle | *Chaîne* |

### Attribution d’un nom aux propriétés personnalisées {#naming-of-custom-properties}

Lors de l’ajout de propriétés personnalisées, pour que ces propriétés soient visibles pour les tris et les recherches créés avec l’API [de recherche](#ugc-search-api)UGC, il est *nécessaire* d’ajouter un suffixe au nom de la propriété.

Le suffixe est destiné aux langues  qui utilisent un  :

* Il identifie la propriété comme pouvant faire l’objet de recherches.
* Il identifie le type de données.

Solr est un exemple de langage  qui utilise un .

| **Suffixe** | **Type de données** |
|---|---|
| _b | *Booléen* |
| _dt | *Calendrier* |
| _d | *Double* |
| _tl | *Long* |
| _s | *Chaîne* |
| _t | *Texte* |

**Notes:**

* *Le texte* est une chaîne à jetons, contrairement à *la chaîne* . Utilisez *Texte* pour les recherches floues (plus comme celle-ci).

* Pour les types à plusieurs valeurs, ajoutez &quot;s&quot; au suffixe, par exemple :

   * `viewDate_dt`: date unique, propriété
   * `viewDates_dts`:  de date, propriété

## Filtres {#filters}

Les composants qui incluent le système [de](essentials-comments.md) commentaires prennent en charge l’ajout du paramètre de filtre à leurs points de fin.

La syntaxe de filtre pour la logique ET et OU est exprimée comme suit (illustré avant le codage URL) :

* Pour spécifier OU, utilisez un paramètre de filtre avec des valeurs séparées par des virgules :

   * `filter=name eq 'Jennifer',name eq 'Jen'`

* Pour spécifier ET, utilisez plusieurs paramètres de filtre :

   * `filter = name eq 'Jackson'&filter=message eq 'testing'`

L’implémentation par défaut du composant [](search.md) Recherche utilise cette syntaxe, comme le montre l’URL qui ouvre la page Résultats de la recherche dans le guide [Composants de la](components-guide.md)communauté. Pour tester, accédez à [http://localhost:4503/content/community-components/en/search.html](http://localhost:4503/content/community-components/en/search.html).

Les opérateurs de filtre sont :

| EQ | égal à |
|---|---|
| NE | n’est pas égal à |
| LT | inférieur à |
| LTE | inférieur ou égal à |
| GE | supérieur à |
| GTE | supérieur ou égal à |
| LIKE | correspondance floue |

Il est important que l’URL fasse référence au composant Communautés (ressource) et non à la page sur laquelle le composant est placé :

* Correct : composant de forum
   * `/content/community-components/en/forum/jcr:content/content/forum.social.json`
* Incorrect : page du forum
   * `/content/community-components/en/forum.social.json`

## Outils SRP {#srp-tools}

Il existe un projet GitHub Adobe Marketing Cloud qui contient :

[Outils SRP des communautés AEM](https://github.com/Adobe-Marketing-Cloud/aem-communities-srp-tools)

Ce référentiel contient des outils de gestion des données dans SRP.

Actuellement, il existe une servlet qui permet de supprimer toutes les UGC de tout SRP.

Par exemple, pour supprimer tous les fichiers UGC dans ASRP :

```shell
curl -X POST http://localhost:4502/services/social/srp/cleanup?path=/content/usergenerated/asi/cloud -uadmin:admin
```

## Résolution des incidents {#troubleshooting}

###  Solr {#solr-query}

Pour résoudre les problèmes liés à un  Solr, activez la journalisation DEBUG pour

`com.adobe.cq.social.srp.impl.SocialSolrConnector`.

Le  Solr réel s’affichera sous forme d’URL codée dans le journal de débogage :

 solr est : `sort=timestamp+desc&bl=en&pl=en&start=0&rows=10 &q=%2Btitle_t:(hello)+%2Bprovider_id:\/content/usergenerated/asi/mongo/content/+%2Bresource_type_s:&df=provider_id&trf=verbatim&fq={!cost%3D100}report_suite:mongo`

La valeur du `q` paramètre est le . Une fois l’encodage de l’URL décodé, le  de peut être transmis à l’outil de d’administration Solr pour un débogage plus poussé.

## Ressources connexes {#related-resources}

* [de contenu de la communauté](working-with-srp.md) - Parle des choix SRP disponibles pour un magasin commun UGC.
* [Aperçu](srp.md) du fournisseur de ressources  - Présentation et aperçu de l’utilisation du référentiel.
* [Accès UGC avec SRP](accessing-ugc-with-srp.md) - Instructions de codage.
* [SocialUtils Refactoring](socialutils.md) - Méthodes d’utilitaire pour SRP qui remplacent SocialUtils.
* [Composants](search.md) de résultats de recherche et de recherche - Ajout d’une fonction de recherche UGC à un modèle.

