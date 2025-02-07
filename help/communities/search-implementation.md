---
title: Principes de recherche
description: Découvrez la fonctionnalité de recherche essentielle d’AEM Communities. Les communautés fournissent également l’API de recherche pour le contenu généré par l’utilisateur.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 8af5ee58-19d7-47b6-b45d-e88006703a5d
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1158'
ht-degree: 4%

---

# Principes de recherche {#search-essentials}

## Vue d’ensemble {#overview}

La fonction de recherche est une fonctionnalité essentielle de Adobe Experience Manager (AEM) Communities. Outre les fonctionnalités [AEM recherche de plateforme](../../help/sites-deploying/queries-and-indexing.md), AEM Communities fournit l’ [ API de recherche UGC](#ugc-search-api) pour la recherche de contenu généré par l’utilisateur. Le contenu généré par l’utilisateur possède des propriétés uniques, car il est saisi et stocké séparément du contenu AEM et des données utilisateur.

Pour Communities, les deux éléments généralement recherchés sont les suivants :

* Contenu publié par les membres de la communauté

   * Il utilise l’API de recherche UGC d’AEM Communities.

* Utilisateurs et groupes d’utilisateurs (données utilisateur)

   * Elle utilise les fonctionnalités de recherche de la plateforme AEM.

Cette section de la documentation intéresse les développeurs qui créent des composants personnalisés qui créent ou gèrent du contenu généré par l’utilisateur.

## Noeuds de sécurité et ombre {#security-and-shadow-nodes}

Pour un composant personnalisé, il est nécessaire d’utiliser les méthodes [SocialResourceUtilities](socialutils.md#socialresourceutilities-package). Les méthodes d’utilitaire qui créent et recherchent le contenu généré par l’utilisateur établissent les [noeuds fantômes](srp.md#about-shadow-nodes-in-jcr) requis et s’assurent que le membre dispose des autorisations appropriées pour la requête.

Les propriétés qui ne sont pas gérées par les utilitaires SRP sont liées à la modération.

Voir [SRP et UGC Essentials](srp-and-ugc.md) pour plus d’informations sur les méthodes d’utilitaire utilisées pour accéder aux noeuds fantômes UGC et ACL.

## API de recherche UGC {#ugc-search-api}

Le [magasin commun UGC](working-with-srp.md) est fourni par l’un des différents fournisseurs de ressources de stockage (SRP), chacun pouvant avoir un langage de requête natif différent. Par conséquent, quel que soit la SRP choisie, le code personnalisé doit utiliser des méthodes du [package de l’API UGC](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) (*com.adobe.cq.social.ugc.api*) qui appelle le langage de requête approprié pour la SRP choisie.

### Recherches ASRP {#asrp-searches}

Pour [ASRP](asrp.md), le contenu créé par l’utilisateur est stocké dans le cloud d’Adobe. Bien que le contenu généré par l’utilisateur ne soit pas visible dans CRX, la [modération](moderate-ugc.md) est disponible dans les environnements de création et de Publish. L’utilisation de l’ [API de recherche UGC](#ugc-search-api) fonctionne pour ASRP de la même manière que pour les autres SRP.

Il n’existe actuellement aucun outil pour gérer les recherches ASRP.

Lors de la création de propriétés personnalisées pouvant faire l’objet de recherches, il est nécessaire de respecter les [exigences d’attribution de noms](#naming-of-custom-properties).

### Recherches MSRP {#msrp-searches}

Pour [MSRP](msrp.md), le contenu créé par l’utilisateur est stocké dans MongoDB configuré pour utiliser Solr pour la recherche. Le contenu généré par l’utilisateur n’est pas visible dans CRX, mais la [modération](moderate-ugc.md) est disponible dans les environnements de création et de Publish.

Concernant MSRP et Solr :

* Le Solr incorporé pour la plateforme AEM n’est pas utilisé pour MSRP.
* Si vous utilisez un Solr distant pour la plateforme AEM, il peut être partagé avec MSRP, mais il doit utiliser des collections différentes.
* Solr peut être configuré pour la recherche standard ou pour la recherche multilingue (MLS).
* Pour plus d’informations sur la configuration, voir [Configuration Solr](msrp.md#solr-configuration) pour MSRP.

Les fonctions de recherche personnalisées doivent utiliser l’[ API de recherche UGC](#ugc-search-api).

Lors de la création de propriétés personnalisées pouvant faire l’objet de recherches, il est nécessaire de respecter les [exigences d’attribution de noms](#naming-of-custom-properties).

### Recherches JSRP {#jsrp-searches}

Pour [JSRP](jsrp.md), le contenu créé par l’utilisateur est stocké dans [Oak](../../help/sites-deploying/platform.md) et n’est visible que dans le référentiel de l’instance d’auteur ou de Publish AEM sur laquelle il a été saisi.

Comme le contenu généré par l’utilisateur est généralement saisi dans l’environnement Publish, pour les systèmes de production multi-éditeurs, il est nécessaire de configurer une [grappe de publication](topologies.md), et non une ferme de publication, de sorte que le contenu saisi soit visible par tous les éditeurs.

Pour JSRP, le contenu généré par l’utilisateur entré dans l’environnement Publish n’est jamais visible dans l’environnement de création. Par conséquent, toutes les tâches de [modération](moderate-ugc.md) ont lieu dans l’environnement Publish.

Les fonctions de recherche personnalisées doivent utiliser l’[ API de recherche UGC](#ugc-search-api).

#### Indexation Oak {#oak-indexing}

Bien que les index Oak ne soient pas automatiquement créés pour la recherche de plateforme AEM, à partir d’AEM 6.2, ils ont été ajoutés pour qu’AEM Communities améliore les performances et prenne en charge la pagination lors de la présentation des résultats de recherche UGC.

Si des propriétés personnalisées sont utilisées et que les recherches sont lentes, des index supplémentaires doivent être créés pour les propriétés personnalisées afin de les rendre plus performantes. Pour maintenir la portabilité, respectez les [exigences d’attribution de noms](#naming-of-custom-properties) lors de la création de propriétés personnalisées pouvant faire l’objet de recherches.

Pour modifier des index existants ou créer des index personnalisés, reportez-vous à la section [Requêtes et indexation Oak](../../help/sites-deploying/queries-and-indexing.md).

[Oak Index Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/oak-index-manager.html) est disponible sous ACS AEM Commons. Elle fournit les éléments suivants :

* Une vue des index existants.
* La possibilité d’initier la réindexation.

Pour afficher les index Oak existants dans [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md), l’emplacement est le suivant :

* `/oak:index/socialLucene`

![social-lucene](assets/social-lucene.png)

## Propriétés de recherche indexées {#indexed-search-properties}

### Propriétés de recherche par défaut {#default-search-properties}

Vous trouverez ci-dessous quelques-unes des propriétés pouvant faire l’objet de recherches utilisées pour différentes fonctionnalités de Communities :

| **Propriété** | **Type de données** |
|---|---|
| isFlagged | *Booléen* |
| isSpam | *Booléen* |
| lecture | *Booléen* |
| influence | *Booléen* |
| attachments | *Booléen* |
| sentiment | *Long* |
| marqué | *Booléen* |
| ajoutée | *Date* |
| modifiedDate | *Date* |
| state | *Chaîne* |
| userIdentifier | *Chaîne* |
| responses | *Long* |
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

### Dénomination des propriétés personnalisées {#naming-of-custom-properties}

Lors de l’ajout de propriétés personnalisées, pour que ces propriétés soient visibles pour les recherches et le tri créés avec l’ [API de recherche UGC](#ugc-search-api), il est *obligatoire* d’ajouter un suffixe au nom de la propriété.

Le suffixe est destiné aux langages de requête qui utilisent un schéma :

* Il identifie la propriété comme pouvant faire l’objet d’une recherche.
* Il identifie le type de données.

Solr est un exemple de langage de requête qui utilise un schéma.

| **Suffix** | **Type de données** |
|---|---|
| _b | *Booléen* |
| _dt | *Calendrier* |
| _d | *Double* |
| _tl | *Long* |
| _s | *Chaîne* |
| _t | *Texte* |

**Remarques:**

* *Text* est une chaîne en unités lexicales, *String* ne l&#39;est pas. Utilisez *Texte* pour effectuer des recherches approximatives (comme celle-ci).

* Pour les types à plusieurs valeurs, ajoutez &quot;s&quot; au suffixe, par exemple :

   * `viewDate_dt` : propriété de date unique
   * `viewDates_dts` : propriété de liste de dates

## Filtres {#filters}

Les composants, qui incluent le [système de commentaires](essentials-comments.md), prennent en charge le paramètre de filtre en plus de leurs points de terminaison.

La syntaxe du filtre pour la logique ET et OU est exprimée comme suit (affichée avant d’être codée au format URL) :

* Pour spécifier OU, utilisez un paramètre de filtre avec des valeurs séparées par des virgules :

   * `filter=name eq 'Jennifer',name eq 'Jen'`

* Pour spécifier ET, utilisez plusieurs paramètres de filtre :

   * `filter = name eq 'Jackson'&filter=message eq 'testing'`

L’implémentation par défaut du [composant Recherche](search.md) utilise cette syntaxe, comme on peut le voir dans l’URL qui ouvre la page Résultats de la recherche dans le [guide des composants de la communauté](components-guide.md). Pour tester, accédez à [http://localhost:4503/content/community-components/en/search.html](http://localhost:4503/content/community-components/en/search.html).

Les opérateurs de filtre sont les suivants :

| EQ | est égal à |
|---|---|
| NE | not equals |
| LT | inférieur à |
| LTE | inférieur ou égal à |
| GE | supérieur à |
| GTE | supérieur ou égal à |
| LIKE | correspondance approximative |

Il est important que l’URL référence le composant Communities (ressource) et non la page sur laquelle le composant est placé :

* Correct : composant de forum
   * `/content/community-components/en/forum/jcr:content/content/forum.social.json`
* Incorrect : page du forum
   * `/content/community-components/en/forum.social.json`

## Outils SRP {#srp-tools}

Il existe un projet Adobe Experience Cloud GitHub qui contient :

[Outils AEM Communities SRP](https://github.com/Adobe-Marketing-Cloud/aem-communities-srp-tools)

Ce référentiel contient des outils pour gérer les données dans la SRP.

Actuellement, il existe un servlet qui peut supprimer tout le contenu généré par l’utilisateur de n’importe quelle SRP.

Par exemple, pour supprimer tout le contenu généré par l’utilisateur dans ASRP :

```shell
curl -X POST http://localhost:4502/services/social/srp/cleanup?path=/content/usergenerated/asi/cloud -uadmin:admin
```

## Résolution des problèmes {#troubleshooting}

### Requête Solr {#solr-query}

Pour résoudre les problèmes liés à une requête Solr, activez la journalisation DEBUG pour

`com.adobe.cq.social.srp.impl.SocialSolrConnector`.

La requête Solr réelle s’affiche sous forme d’URL encodée dans le journal de débogage :

La requête à résoudre est : `sort=timestamp+desc&bl=en&pl=en&start=0&rows=10 &q=%2Btitle_t:(hello)+%2Bprovider_id:\/content/usergenerated/asi/mongo/content/+%2Bresource_type_s:&df=provider_id&trf=verbatim&fq={!cost%3D100}report_suite:mongo`

La valeur du paramètre `q` est la requête. Une fois le codage de l’URL décodé, la requête peut être transmise à l’outil Solr Admin Query pour un débogage plus poussé.

## Ressources connexes {#related-resources}

* [Stockage de contenu de la communauté](working-with-srp.md) - Discute des choix de SRP disponibles pour un magasin commun UGC.
* [Présentation du fournisseur de ressources de stockage](srp.md) - Présentation et utilisation du référentiel.
* [Accès au contenu créé par l’utilisateur avec SRP](accessing-ugc-with-srp.md) - Instructions de codage.
* [Refactorisation de SocialUtils](socialutils.md) - Méthodes utilitaires pour SRP qui remplacent SocialUtils.
* [Composants Résultats de la recherche et de la recherche](search.md) - Ajout d’une fonctionnalité de recherche UGC à un modèle.
