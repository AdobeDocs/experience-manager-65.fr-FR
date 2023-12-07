---
title: Propriétés et noeuds de contenu
description: Consultez cette page pour en savoir plus sur les propriétés de contenu et les noeuds.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 05c8c846-69cc-4075-9149-33890b3d1e08
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 21%

---

# Propriétés et noeuds de contenu {#content-properties-and-nodes}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur de SPA pour les projets qui nécessitent un rendu côté client basé sur la structure d’application d’une seule page (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

Les articles, bannières et collections sont représentés sous la forme cq:Pages dans AEM.

Ils partagent les mêmes propriétés communes que dans n’importe quel cq:Page , en plus de plusieurs autres propriétés affichées ci-dessous qui représentent les métadonnées des services Mobile On Demand de Adobe Experience Manager (AEM) et l’intégration qui prennent en charge les propriétés.

Les tableaux suivants décrivent les propriétés et les noeuds du contenu.

## Propriétés d’intégration courantes {#common-integration-properties}

| **Nom de la propriété** | **Type** | **Valeurs par défaut ou attendues** | **Description** |
|---|---|---|---|
| dps-id | Chaîne |  | affectée par AEM Mobile et stockée par AEM une fois chargée dans AEM Mobile ou importée depuis AEM Mobile |
| dps-resourceType | Chaîne | dps:Article | dps:Bannière | dps:Collection | propriété de type d’entité |
| dps-version | Chaîne |  | version de l’entité AEM Mobile (également contenue dans l’aemm-id complet) |
| dps-lastSynced | Date |  | date de la dernière synchronisation/importation d’AEM Mobile dans AEM |
| dps-lastUploaded | Date |  | date du dernier téléchargement d’AEM vers AEM Mobile |
| dps-lastUploadedBy | Chaîne : userid |  | ID de l’utilisateur qui a effectué la dernière requête de chargement d’AEM vers AEM Mobile |

## Propriétés des métadonnées principales {#core-metadata-properties}

| Nom de la propriété | Type | Valeurs par défaut ou attendues |
|--- |--- |--- |
| dps-title | Chaîne |  |
| dps-shortTitle | Chaîne |  |
| dps-abstract | Chaîne |  |
| dps-shortAbstract | Chaîne |  |
| dps-département | Chaîne |  |
| dps-category | Chaîne |  |
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
| dps-tapAction |  | Appuyez surAction depuis {webLink} |
| dps-tapActionUrl |  |  |

### Collections {#collections}

| Nom de la propriété | Type | Valeurs par défaut ou attendues |
|--- |--- |--- |
| dps-productId | Chaîne |  |
| dps-readPosition | Chaîne | de {&quot;reset&quot;,&quot;keep&quot;} |
| dps-horizontalSwipe | Booléen |  |
| dps-allowDownload | Booléen |  |
| dps-openDefault | Chaîne | de {&quot;browsePage&quot;,&quot;contentView&quot;} |
| dps-layout | Chaîne |  |

## Noeuds de contenu {#content-nodes}

### Noeuds communs {#common-nodes}

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
| S/O |  |  |  |

#### Collections {#collections-1}

| Nom du nœud | Type | Valeurs attendues par défaut | Description |
|--- |--- |--- |--- |
| background-image | jcr:primaryType=nt:unstructured <br> sling:resourceType=foundation/components/image |  |  |
