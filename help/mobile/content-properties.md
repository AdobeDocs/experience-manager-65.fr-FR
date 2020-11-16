---
title: Propriétés de contenu et noeuds
seo-title: Propriétés de contenu et noeuds
description: Suivez cette page pour en savoir plus sur les propriétés de contenu et les noeuds.
seo-description: Suivez cette page pour en savoir plus sur les propriétés de contenu et les noeuds.
uuid: 2dad52c8-5b6c-4b90-8498-62217a9a27fc
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: f5721ddc-df5c-496c-be61-38d1cab63ad4
translation-type: tm+mt
source-git-commit: 50c0bdfc3203410d392e53536bc7cd00245406e5
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 25%

---


# Propriétés de contenu et noeuds {#content-properties-and-nodes}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

Les articles, bannières et collections sont représentés sous la forme cq:Pages dans AEM.

Ils partagent les mêmes propriétés communes que celles qui se trouvent dans cq:Page, en plus de plusieurs autres qui représentent les métadonnées de services à la demande Adobe Experience Manager (AEM) Mobile On-Demand et les propriétés de prise en charge de l&#39;intégration.

Les tableaux suivants décrivent les propriétés et les noeuds de contenu.

## Propriétés d’intégration courantes {#common-integration-properties}

| **Nom de la propriété** | **Type** | **Valeurs par défaut ou attendues** | **Description** |
|---|---|---|---|
| dps-id | Chaîne |  | affecté par AEM Mobile et stocké par AEM une fois téléchargé vers AEM Mobile ou importé de AEM Mobile |
| dps-resourceType | Chaîne | dps:Article | dps:Bannière | dps:Collection | propriété de type d&#39;entité |
| dps-version | Chaîne |  | version de l’entité AEM Mobile (également incluse dans l’aemm-id complet) |
| dps-lastSynced | Date |  | date de la dernière synchronisation/importation d&#39;AEM Mobile vers AEM |
| dps-lastUploaded | Date |  | date du dernier transfert de l’AEM vers AEM Mobile |
| dps-lastUploadedBy | String:userid |  | ID de l’utilisateur qui a effectué la dernière demande de transfert d’AEM à AEM Mobile |

## Propriétés de métadonnées de base {#core-metadata-properties}

| Nom de la propriété | Type | Valeurs par défaut ou attendues |
|--- |--- |--- |
| dps-title | Chaîne |  |
| dps-shortTitle | Chaîne |  |
| dps-abstract | Chaîne |  |
| dps-shortAbstract | Chaîne |  |
| dps-département | Chaîne |  |
| dps-catégorie | Chaîne |  |
| dps-keywords | Chaîne[] |  |
| dps-internalKeywords | Chaîne[] |  |
| importance dps | Chaîne[] | Importance de {&quot;low&quot;, &quot;normal&quot;, &quot;high&quot;} |

### Articles {#articles}

| **Nom de la propriété** | **Type** | **Valeurs par défaut ou attendues** |
|---|---|---|
| dps-author | Chaîne |  |
| dps-authorURL | Chaîne |  |
| dps-hideFromBrowsePage | Booléen |  |
| dps-access | Chaîne | ProtectedAccess de {&quot;protected&quot;, &quot;metered&quot;, &quot;free&quot;} |
| **Social** |  |  |
| dps-socialShareURL | Chaîne |  |
| dps-articleText | Chaîne |  |
| dps-url | Chaîne |  |

### Bannières {#banners}

| **Nom de la propriété** | **Type** | **Valeurs par défaut ou attendues** |
|---|---|---|
| dps-tapAction |  | Appuyez sur Action à partir de {webLink} |
| dps-tapActionUrl |  |  |

### Collections {#collections}

| Nom de la propriété | Type | Valeurs par défaut ou attendues |
|--- |--- |--- |
| dps-productId | Chaîne |  |
| dps-readingPosition | Chaîne | de {&quot;reset&quot;,&quot;keep&quot;} |
| dps-horizontalSwipe | Booléen |  |
| dps-allowDownload | Booléen |  |
| dps-openDefault | Chaîne | de {&quot;browsePage&quot;,&quot;contentView&quot;} |
| dps-layout | Chaîne |  |

## Noeuds de contenu {#content-nodes}

### Noeuds courants {#common-nodes}

| Nom du nœud | Type | Valeurs par défaut ou attendues | Description |
|--- |--- |--- |--- |
| image | jcr:primaryType=nt:unstructured <br> sling:resourceType=foundation/components/image |  |  |

### Entités {#entities}

#### Articles {#articles-1}

| Nom du nœud | Type | Valeurs attendues par défaut | Description |
|--- |--- |--- |--- |
| social-share-image |  | jcr:primaryType=nt:unstructured <br> sling:resourceType=foundation/components/image |  |

#### Bannières {#banners-1}

| Nom du nœud | Type | Valeurs attendues par défaut | Description |
|---|---|---|---|
| N/A |  |  |  |

#### Collections {#collections-1}

| Nom du nœud | Type | Valeurs attendues par défaut | Description |
|--- |--- |--- |--- |
| image d’arrière-plan | jcr:primaryType=nt:unstructured <br> sling:resourceType=foundation/components/image |  |  |
