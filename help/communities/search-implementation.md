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
source-git-commit: 6ab91667ad668abf80ccf1710966169b3a187928
workflow-type: tm+mt
source-wordcount: '1189'
ht-degree: 6%

---


# Essentials de recherche {#search-essentials}

## Présentation {#overview}

La fonction de recherche est une caractéristique essentielle de l&#39;AEM Communities. Outre les fonctionnalités de recherche [de plateforme](../../help/sites-deploying/queries-and-indexing.md) AEM, AEM Communities fournit l’API [de recherche](#ugc-search-api) UGC pour la recherche de contenu généré par l’utilisateur (UGC). L’UGC possède des propriétés uniques, car elles sont entrées et stockées séparément du contenu AEM et des données utilisateur.

Pour les communautés, les deux éléments généralement recherchés sont les suivants :

* Contenu publié par les membres de la communauté

   * Utilise l’API de recherche UGC des communautés AEM.

* Utilisateurs et groupes d’utilisateurs (données utilisateur)

   * Utilise les fonctionnalités de recherche AEM plate-forme.

Cette section de la documentation présente un intérêt pour les développeurs qui créent des composants personnalisés qui créent ou gèrent des composants UGC.

## Sécurité et noeuds fantômes {#security-and-shadow-nodes}

Pour un composant personnalisé, il est nécessaire d’utiliser les méthodes [SocialResourceUtilities](socialutils.md#socialresourceutilities-package) . Les méthodes de l&#39;utilitaire qui créent et recherchent l&#39;UGC vont établir les noeuds [d&#39;](srp.md#about-shadow-nodes-in-jcr) ombre requis et s&#39;assurer que le membre dispose des autorisations appropriées pour la demande.

Les propriétés qui ne sont pas gérées par les utilitaires SRP sont liées à la modération.

Voir [SRP et UGC Essentials](srp-and-ugc.md) pour en savoir plus sur les méthodes d’utilité utilisées pour accéder aux noeuds fantômes UGC et ACL.

## API de recherche UGC {#ugc-search-api}

Le magasin [commun](working-with-srp.md) UGC est fourni par l&#39;un des divers fournisseurs de ressources d&#39;enregistrement (SRP), chacun pouvant avoir une langue de requête native différente. Par conséquent, quel que soit le SRP choisi, le code personnalisé doit utiliser les méthodes du package [d’API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) UGC (*com.adobe.cq.social.ugc.api*) qui appelleront le langage de requête approprié pour le SRP choisi.

### Recherches ASRP {#asrp-searches}

Pour [ASRP](asrp.md), UGC est stocké dans le cloud d’Adobe. Bien que l’UGC ne soit pas visible dans CRX, la [modération](moderate-ugc.md) est disponible à la fois auprès des environnements d’auteur et de publication. L’utilisation de l’API [de recherche](#ugc-search-api) UGC fonctionne pour ASRP de la même manière que pour les autres applications de recherche de type SRP.

Il n&#39;existe actuellement aucun outil pour gérer les recherches ASRP.

Lors de la création de propriétés personnalisées pouvant faire l’objet de recherches, il est nécessaire de respecter les exigences [de](#naming-of-custom-properties)nommage.

### Recherches MSRP {#msrp-searches}

Pour [MSRP](msrp.md), UGC est stocké dans MongoDB configuré pour utiliser Solr pour la recherche. L’UGC ne sera pas visible dans CRX, mais la [modération](moderate-ugc.md) est disponible à la fois auprès des environnements d’auteur et de publication.

Concernant MSRP et Solr :

* Le Solr incorporé pour la plateforme AEM n&#39;est pas utilisé pour MSRP.
* Si vous utilisez un Solr distant pour la plateforme AEM, il peut être partagé avec MSRP, mais il doit utiliser des collections différentes.
* Solr peut être configuré pour la recherche standard ou pour la recherche multilingue (MLS).
* Pour plus d’informations sur la configuration, voir Configuration [](msrp.md#solr-configuration) Solr pour MSRP.

Les fonctions de recherche personnalisée doivent utiliser l’API [de recherche](#ugc-search-api)UGC.

Lors de la création de propriétés personnalisées pouvant faire l’objet de recherches, il est nécessaire de respecter les exigences [de](#naming-of-custom-properties)nommage.

### Recherches JSRP {#jsrp-searches}

Pour [JSRP](jsrp.md), l’UGC est stocké dans [Oak](../../help/sites-deploying/platform.md) et n’est visible que dans le référentiel de l’instance d’auteur ou de publication AEM sur laquelle il a été saisi.

Comme l’UGC est généralement saisi dans l’environnement de publication, pour les systèmes de production à plusieurs éditeurs, il est nécessaire de configurer une grappe [de](topologies.md)publication, et non une batterie de publication, de sorte que le contenu saisi soit visible de tous les éditeurs.

Pour JSRP, l’UGC saisi dans l’environnement de publication ne sera jamais visible dans l’environnement d’auteur. Ainsi, toutes les tâches de [modération](moderate-ugc.md) ont lieu dans l’environnement de publication.

Les fonctions de recherche personnalisée doivent utiliser l’API [de recherche](#ugc-search-api)UGC.

#### Indexation des chênes {#oak-indexing}

Bien que les indices Oak ne soient pas automatiquement créés pour la recherche AEM plate-forme, à partir de AEM 6.2, ils ont été ajoutés pour AEM Communities afin d&#39;améliorer les performances et de fournir la prise en charge de la pagination lors de la présentation des résultats de recherche UGC.

Si les propriétés personnalisées sont en cours d’utilisation et que les recherches sont lentes, des indices supplémentaires devront être créés pour que les propriétés personnalisées soient plus performantes. Pour préserver la portabilité, respectez les exigences [de](#naming-of-custom-properties) nommage lors de la création de propriétés personnalisées pouvant faire l’objet de recherches.

Pour modifier des indices existants ou créer des indices personnalisés, reportez-vous aux Requêtes [en chêne et à l&#39;indexation](../../help/sites-deploying/queries-and-indexing.md).

Le Gestionnaire [de l&#39;index](https://adobe-consulting-services.github.io/acs-aem-commons/features/oak-index-manager.html) Oak est disponible sur ACS AEM Commons. Il fournit :

* Vue des indices existants.
* Possibilité de lancer la réindexation.

Pour vue des indices Oak en [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md), l&#39;emplacement est le suivant :

* `/oak:index/socialLucene`

![social-lucène](assets/social-lucene.png)

## Propriétés de recherche indexée {#indexed-search-properties}

### Propriétés de recherche par défaut {#default-search-properties}

Vous trouverez ci-dessous quelques-unes des propriétés pouvant faire l’objet de recherches et utilisées pour diverses fonctionnalités de communautés :

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
| modifiedDate | *Date* |
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

Le suffixe est destiné aux langues de requête qui utilisent un schéma :

* Il identifie la propriété comme pouvant faire l’objet de recherches.
* Il identifie le type de données.

Solr est un exemple de langage requête qui utilise un schéma.

| **Suffixe** | **Type de données** |
|---|---|
| _b | *Booléen* |
| _dt | *Calendrier* |
| _d | *Double* |
| _tl | *Long* |
| _s | *Chaîne* |
| _t | *Texte* |

**Notes:**

* *Le texte* est une chaîne à jetons, *Chaîne* non plus. Utilisez *Texte* pour effectuer des recherches floues (un peu comme celle-ci).

* Pour les types à plusieurs valeurs, ajoutez &quot;s&quot; au suffixe, par exemple :

   * `viewDate_dt`: Date unique, propriété
   * `viewDates_dts`: liste de la propriété de dates

## Filtres {#filters}

Les composants qui incluent le système [de](essentials-comments.md) commentaires prennent en charge l’ajout de paramètres de filtre à leurs points de terminaison.

La syntaxe de filtre pour les logiques ET et OU est exprimée comme suit (affichée avant d’être codée en URL) :

* Pour spécifier OU, utilisez un paramètre de filtre avec des valeurs séparées par des virgules :

   * `filter=name eq 'Jennifer',name eq 'Jen'`

* Pour spécifier ET, utilisez plusieurs paramètres de filtre :

   * `filter = name eq 'Jackson'&filter=message eq 'testing'`

L’implémentation par défaut du composant [](search.md) Search utilise cette syntaxe, comme le montre l’URL qui ouvre la page Résultats de la recherche dans le guide [Composants de la](components-guide.md)communauté. Pour tester, accédez à [http://localhost:4503/content/community-components/en/search.html](http://localhost:4503/content/community-components/en/search.html).

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

* Correct : composant forum
   * `/content/community-components/en/forum/jcr:content/content/forum.social.json`
* Incorrect : page du forum
   * `/content/community-components/en/forum.social.json`

## Outils SRP {#srp-tools}

Il existe un projet Adobe Marketing Cloud GitHub qui contient :

[Outils SRP AEM Communities](https://github.com/Adobe-Marketing-Cloud/aem-communities-srp-tools)

Ce référentiel contient des outils de gestion des données dans SRP.

Actuellement, il existe une servlet qui permet de supprimer toutes les UGC de tout SRP.

Par exemple, pour supprimer tous les fichiers UGC dans ASRP :

```shell
curl -X POST http://localhost:4502/services/social/srp/cleanup?path=/content/usergenerated/asi/cloud -uadmin:admin
```

## Résolution des incidents {#troubleshooting}

### Requête solaire {#solr-query}

Pour résoudre les problèmes liés à une requête Solr, activez la journalisation DEBUG pour

`com.adobe.cq.social.srp.impl.SocialSolrConnector`.

La requête Solr réelle s&#39;affichera sous forme d&#39;URL codée dans le journal de débogage :

La requête à résoudre est : `sort=timestamp+desc&bl=en&pl=en&start=0&rows=10 &q=%2Btitle_t:(hello)+%2Bprovider_id:\/content/usergenerated/asi/mongo/content/+%2Bresource_type_s:&df=provider_id&trf=verbatim&fq={!cost%3D100}report_suite:mongo`

La valeur du `q` paramètre est la requête. Une fois le codage d’URL décodé, la requête peut être transmise à l’outil Solr Admin Requête pour un débogage plus poussé.

## Ressources connexes {#related-resources}

* [Enregistrement](working-with-srp.md) de contenu de la communauté - Parle des options SRP disponibles pour un magasin commun UGC.
* [Présentation](srp.md) du fournisseur de ressources d&#39;Enregistrement - Présentation et présentation de l&#39;utilisation du référentiel.
* [Accès à l&#39;UGC avec SRP](accessing-ugc-with-srp.md) - Règles de codage.
* [SocialUtils Refactoring](socialutils.md) - Méthodes d’utilitaire pour SRP qui remplacent SocialUtils.
* [Composants](search.md) Résultats de la recherche et de la recherche - Ajouter la fonction de recherche UGC à un modèle.

