---
title: Propriétés et nœuds de contenu
description: Consultez cette page pour en savoir plus sur les propriétés et les nœuds de contenu.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 05c8c846-69cc-4075-9149-33890b3d1e08
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 22%

---

# Propriétés et nœuds de contenu {#content-properties-and-nodes}

{{ue-over-mobile}}

Les articles, bannières et collections sont représentés sous la forme cq:Pages dans AEM.

Ils partagent les mêmes propriétés communes que celles trouvées dans n’importe quel cq:Page en plus de plusieurs autres présentées ci-dessous qui représentent les métadonnées des services mobiles On-Demand Adobe Experience Manager (AEM) et les propriétés de prise en charge de l’intégration.

Les tableaux suivants décrivent les propriétés et les nœuds de contenu.

## Propriétés d’intégration communes {#common-integration-properties}

| **Nom de la propriété** | **Type** | **Valeurs par défaut ou valeurs attendues** | **Description** |
|---|---|---|---|
| dps-id | Chaîne |  | affecté par AEM Mobile et stocké par AEM une fois chargé dans AEM Mobile ou importé depuis AEM Mobile |
| dps-resourceType | Chaîne | dps:Article | dps:Bannière | dps:Collection | propriété de type d’entité |
| dps-version | Chaîne |  | version de l’entité AEM Mobile (également contenue dans l’aem-id complet) |
| dps-lastSynced | Date |  | date de la dernière synchronisation/importation d’AEM Mobile dans AEM |
| dps-lastUploaded | Date |  | date du dernier chargement d’AEM vers AEM Mobile |
| dps-lastUploadedBy | String:userid |  | id de l’utilisateur qui a effectué la dernière demande de chargement d’AEM vers AEM Mobile |

## Propriétés des métadonnées de base {#core-metadata-properties}

| Nom de la propriété | Type | Valeurs par défaut ou valeurs attendues |
|--- |--- |--- |
| dps-title | Chaîne |  |
| dps-shortTitle | Chaîne |  |
| dps-abstract | Chaîne |  |
| dps-shortAbstract | Chaîne |  |
| dps-department | Chaîne |  |
| dps-category | Chaîne |  |
| dps-keywords | String[] |  |
| dps-internalKeywords | String[] |  |
| dps-importance | String[] | Importance à partir de {« low », « normal », « high »} |

### Articles {#articles}

| **Nom de la propriété** | **Type** | **Valeurs par défaut ou valeurs attendues** |
|---|---|---|
| dps-author | Chaîne |  |
| dps-authorURL | Chaîne |  |
| dps-hideFromBrowsePage | Booléen |  |
| dps-access | Chaîne | ProtectedAccess depuis {« protected », « metered », « free »} |
| **Social** |  |  |
| dps-socialShareURL | Chaîne |  |
| dps-articleText | Chaîne |  |
| dps-url | Chaîne |  |

### Bannières {#banners}

| **Nom de la propriété** | **Type** | **Valeurs par défaut ou valeurs attendues** |
|---|---|---|
| dps-tapAction |  | TapAction depuis l’{webLink} |
| dps-tapActionUrl |  |  |

### Collections {#collections}

| Nom de la propriété | Type | Valeurs par défaut ou valeurs attendues |
|--- |--- |--- |
| dps-productId | Chaîne |  |
| dps-readingPosition | Chaîne | depuis {« reset »,« retain »} |
| dps-horizontalSwipe | Booléen |  |
| dps-allowDownload | Booléen |  |
| dps-openDefault | Chaîne | de {« browsePage »,« contentView »} |
| dps-layout | Chaîne |  |

## Nœuds de contenu {#content-nodes}

### Nœuds communs {#common-nodes}

| Nom du nœud | Type | Valeurs par défaut ou valeurs attendues | Description |
|--- |--- |--- |--- |
| image | jcr:primaryType=nt:unstructured <br> sling:resourceType=foundation/components/image |  |  |

### Entités {#entities}

#### Articles {#articles-1}

| Nom du nœud | Type | Valeurs par défaut attendues | Description |
|--- |--- |--- |--- |
| social-share-image |  | jcr:primaryType=nt:unstructured <br> sling:resourceType=foundation/components/image |  |

#### Bannières {#banners-1}

| Nom du nœud | Type | Valeurs par défaut attendues | Description |
|---|---|---|---|
| S/O |  |  |  |

#### Collections {#collections-1}

| Nom du nœud | Type | Valeurs par défaut attendues | Description |
|--- |--- |--- |--- |
| background-image | jcr:primaryType=nt:unstructured <br> sling:resourceType=foundation/components/image |  |  |
