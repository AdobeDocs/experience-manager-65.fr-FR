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
source-git-commit: 9a4ae73c08657195da2741cccdb196bd7f7142c9
workflow-type: tm+mt
source-wordcount: '1189'
ht-degree: 6%

---


# Essentials de recherche {#search-essentials}

## Présentation {#overview}

La fonction de recherche est une caractéristique essentielle de l&#39;AEM Communities. Outre les fonctionnalités de [AEM recherche de plate-forme](../../help/sites-deploying/queries-and-indexing.md), AEM Communities fournit l&#39;[API de recherche UGC](#ugc-search-api) dans le but de rechercher le contenu généré par l&#39;utilisateur. L’UGC possède des propriétés uniques, car elles sont entrées et stockées séparément du contenu AEM et des données utilisateur.

Pour les communautés, les deux éléments généralement recherchés sont les suivants :

* Contenu publié par les membres de la communauté

   * Utilise l’API de recherche UGC des communautés AEM.

* Utilisateurs et groupes d’utilisateurs (données utilisateur)

   * Utilise les fonctionnalités de recherche AEM plate-forme.

Cette section de la documentation présente un intérêt pour les développeurs qui créent des composants personnalisés qui créent ou gèrent des composants UGC.

## Noeuds de sécurité et ombres {#security-and-shadow-nodes}

Pour un composant personnalisé, il est nécessaire d’utiliser les méthodes [SocialResourceUtilities](socialutils.md#socialresourceutilities-package). Les méthodes d&#39;utilitaire qui créent et recherchent l&#39;UGC vont établir les [noeuds fantômes](srp.md#about-shadow-nodes-in-jcr) requis et s&#39;assurer que le membre dispose des autorisations appropriées pour la demande.

Les propriétés qui ne sont pas gérées par les utilitaires SRP sont liées à la modération.

Voir [SRP et UGC Essentials](srp-and-ugc.md) pour plus d&#39;informations sur les méthodes d&#39;utilité utilisées pour accéder aux noeuds fantômes UGC et ACL.

## API de recherche UGC {#ugc-search-api}

Le [magasin commun UGC](working-with-srp.md) est fourni par l&#39;un des divers fournisseurs de ressources d&#39;enregistrement (SRP), chacun pouvant avoir une langue de requête native différente. Par conséquent, quel que soit le SRP choisi, le code personnalisé doit utiliser les méthodes du [package d&#39;API UGC](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) (*com.adobe.cq.social.ugc.api*) qui appelleront le langage de requête approprié pour le SRP choisi.

### Recherches ASRP {#asrp-searches}

Pour [ASRP](asrp.md), l’UGC est stocké dans le cloud d’Adobe. Bien que l’UGC ne soit pas visible dans CRX, [la modération](moderate-ugc.md) est disponible dans les environnements d’auteur et de publication. L’utilisation de l’[API de recherche UGC](#ugc-search-api) fonctionne pour ASRP de la même manière que pour les autres PRS.

Il n&#39;existe actuellement aucun outil pour gérer les recherches ASRP.

Lors de la création de propriétés personnalisées pouvant faire l’objet de recherches, il est nécessaire de respecter les [exigences d’attribution de noms](#naming-of-custom-properties).

### Recherches MSRP {#msrp-searches}

Pour [MSRP](msrp.md), UGC est stocké dans MongoDB configuré pour utiliser Solr pour la recherche. L’UGC ne sera pas visible dans CRX, mais [la modération](moderate-ugc.md) est disponible dans les environnements d’auteur et de publication.

Concernant MSRP et Solr :

* Le Solr incorporé pour la plateforme AEM n&#39;est pas utilisé pour MSRP.
* Si vous utilisez un Solr distant pour la plateforme AEM, il peut être partagé avec MSRP, mais il doit utiliser des collections différentes.
* Solr peut être configuré pour la recherche standard ou pour la recherche multilingue (MLS).
* Pour plus d&#39;informations sur la configuration, voir [Configuration du serveur](msrp.md#solr-configuration) pour MSRP.

Les fonctions de recherche personnalisée doivent utiliser l&#39;[API de recherche UGC](#ugc-search-api).

Lors de la création de propriétés personnalisées pouvant faire l’objet de recherches, il est nécessaire de respecter les [exigences d’attribution de noms](#naming-of-custom-properties).

### Recherches JSRP {#jsrp-searches}

Pour [JSRP](jsrp.md), l’UGC est stocké dans [Oak](../../help/sites-deploying/platform.md) et n’est visible que dans le référentiel de l’instance d’auteur ou de publication AEM sur laquelle il a été saisi.

Etant donné que l’UGC est généralement saisi dans l’environnement de publication, pour les systèmes de production à plusieurs éditeurs, il est nécessaire de configurer une [grappe de publication](topologies.md), et non une batterie de publication, afin que le contenu saisi soit visible de tous les éditeurs.

Pour JSRP, l’UGC saisi dans l’environnement de publication ne sera jamais visible dans l’environnement d’auteur. Toutes les tâches de [modération](moderate-ugc.md) ont donc lieu dans l’environnement de publication.

Les fonctions de recherche personnalisée doivent utiliser l&#39;[API de recherche UGC](#ugc-search-api).

#### Indexation de chêne {#oak-indexing}

Bien que les index Oak ne soient pas automatiquement créés pour la recherche AEM plate-forme, à partir de AEM 6.2, ils ont été ajoutés pour AEM Communities afin d&#39;améliorer les performances et de fournir la prise en charge de la pagination lors de la présentation des résultats de recherche UGC.

Si les propriétés personnalisées sont en cours d’utilisation et que les recherches sont lentes, des index supplémentaires doivent être créés pour que les propriétés personnalisées soient plus performantes. Pour préserver la portabilité, respectez les [exigences de nommage](#naming-of-custom-properties) lors de la création de propriétés personnalisées pouvant faire l&#39;objet de recherches.

Pour modifier des index existants ou créer des index personnalisés, reportez-vous à la section [Requêtes en chêne et indexation](../../help/sites-deploying/queries-and-indexing.md).

[Oak Index Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/oak-index-manager.html) est disponible sur ACS AEM Commons. Il fournit :

* Vue des index existants.
* Possibilité de lancer la réindexation.

Pour vue des index Oak existants dans [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md), l&#39;emplacement est :

* `/oak:index/socialLucene`

![social-lucène](assets/social-lucene.png)

## Propriétés de recherche indexée {#indexed-search-properties}

### Propriétés de recherche par défaut {#default-search-properties}

Vous trouverez ci-dessous quelques-unes des propriétés pouvant faire l’objet de recherches et utilisées pour diverses fonctionnalités de communautés :

| **Propriété** | **Type de données** |
|---|---|
| isFlagged | *Booléen* |
| isSpam | *Booléen* |
| lecture | *Booléen* |
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

Lors de l’ajout de propriétés personnalisées, afin que ces propriétés soient visibles pour les tris et les recherches créés avec l’[API de recherche UGC](#ugc-search-api), il est *nécessaire* d’ajouter un suffixe au nom de la propriété.

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

**Remarques:**

* ** Textis est une chaîne jetée,  ** Stringis non. Utilisez *Texte* pour les recherches floues (plus semblables à celles-ci).

* Pour les types à plusieurs valeurs, ajoutez &quot;s&quot; au suffixe, par exemple :

   * `viewDate_dt`: Date unique, propriété
   * `viewDates_dts`: liste de la propriété de dates

## Filtres {#filters}

Les composants qui incluent le [système de commentaires](essentials-comments.md) prennent en charge l&#39;ajout du paramètre de filtre à leurs points de terminaison.

La syntaxe de filtre pour les logiques ET et OU est exprimée comme suit (affichée avant d’être codée en URL) :

* Pour spécifier OU, utilisez un paramètre de filtre avec des valeurs séparées par des virgules :

   * `filter=name eq 'Jennifer',name eq 'Jen'`

* Pour spécifier ET, utilisez plusieurs paramètres de filtre :

   * `filter = name eq 'Jackson'&filter=message eq 'testing'`

L&#39;implémentation par défaut du [composant de recherche](search.md) utilise cette syntaxe, comme le montre l&#39;URL qui ouvre la page Résultats de la recherche dans le [guide des composants de la communauté](components-guide.md). Pour tester, accédez à [http://localhost:4503/content/community-components/en/search.html](http://localhost:4503/content/community-components/en/search.html).

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

La valeur du paramètre `q` est la requête. Une fois le codage d’URL décodé, la requête peut être transmise à l’outil Solr Admin Requête pour un débogage plus poussé.

## Ressources connexes {#related-resources}

* [Enregistrement](working-with-srp.md)  de contenu communautaire - Discute des options SRP disponibles pour un magasin commun UGC.
* [Présentation](srp.md)  du fournisseur de ressources d&#39;Enregistrement - Présentation et présentation de l&#39;utilisation du référentiel.
* [Accès à l&#39;UGC avec des directives de codage SRP](accessing-ugc-with-srp.md) .
* [SocialUtils Refactoring](socialutils.md)  - Méthodes d’utilitaire pour SRP qui remplacent SocialUtils.
* [Composants](search.md)  Résultats de la recherche et de la recherche - Ajouter la fonction de recherche UGC à un modèle.

