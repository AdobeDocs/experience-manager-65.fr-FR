---
title: Créer un index personnalisé pour les références de formulaire adaptatif
description: Découvrez comment créer un index Lucene balisé pour les requêtes de référence de formulaire adaptatif dans AEM Forms afin d’éviter les requêtes de traversée lors de la publication de fragments d’expérience.
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, Developer
source-git-commit: 9240de61985dc32f17593f416e5d054cadb8a392
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 1%
---

# Créer un index personnalisé pour les références de formulaire adaptatif {#create-custom-index-for-adaptive-forms-references}

Créez un index Lucene balisé pour éviter les requêtes de traversée lorsque Adobe Experience Manager (AEM) Forms résout les références de formulaires adaptatifs. Sans index approprié, la publication d’un fragment d’expérience contenant une référence de formulaire adaptatif peut générer un avertissement `Traversal query (query without index)` dans les journaux.

Dans AEM Forms 6.5.24.0 et versions ultérieures, la requête de référence utilise la balise d’index `aemformsAFReferences`. Ces versions incluent la modification de la requête, mais vous devez créer un index personnalisé avec cette balise. Cet article explique comment définir et déployer l’index.

Pour AEM Forms 6.5 LTS, voir [Création d’un index personnalisé pour les références de formulaires adaptatifs dans AEM Forms 6.5 LTS](https://experienceleague.adobe.com/en/docs/experience-manager-65-lts/content/forms/install-aem-forms/configure-aem-forms/create-custom-index-for-adaptive-forms-references).

## Prérequis {#prerequisites}

Avant de commencer, vérifiez que vous disposez des éléments suivants :

* AEM Forms version 6.5.24.0 ou ultérieure, avec le module complémentaire Forms correspondant installé.
* Accès à la création d’un index sous `/oak:index` sur l’instance de création.
* Un projet AEM avec un module `ui.apps` si vous déployez l’index par le biais d’un package de contenu ou d’un accès à CRXDE Lite pour l’alternative de développement.

Testez l’index dans un environnement de développement ou d’évaluation avant de le déployer en production. [La création d’un index peut prendre du temps sur un référentiel volumineux](/help/sites-deploying/queries-and-indexing.md#configuring-the-indexes).

## Définition de l’index personnalisé {#define-the-custom-index}

Créez l’index à l’adresse `/oak:index/customAFReferenceLuceneIndex-1`. Vous pouvez choisir un autre nom de nœud d’index, mais ne modifiez pas la balise `aemformsAFReferences` afin que la requête de référence Forms puisse sélectionner l’index.

Utilisez la définition suivante. Il indexe les `sling:resourceType` sur `nt:unstructured` nœuds sous `/content`.

```json
{
  "jcr:primaryType": "oak:QueryIndexDefinition",
  "selectionPolicy": "tag",
  "compatVersion": 2,
  "includedPaths": ["/content"],
  "queryPaths": ["/content"],
  "tags": ["aemformsAFReferences"],
  "type": "lucene",
  "async": ["async"],
  "evaluatePathRestrictions": true,
  "reindex": false,
  "indexRules": {
    "jcr:primaryType": "nt:unstructured",
    "nt:unstructured": {
      "jcr:primaryType": "nt:unstructured",
      "properties": {
        "jcr:primaryType": "nt:unstructured",
        "resourceType": {
          "jcr:primaryType": "nt:unstructured",
          "propertyIndex": true,
          "name": "sling:resourceType"
        }
      }
    }
  }
}
```

N’ajoutez pas de `analyzed=true`. La requête de référence utilise des restrictions de propriété plutôt qu’une condition de `contains` en texte intégral, ce qui rend ce paramètre inutile.

## Déployer l’index avec un package de contenu {#deploy-the-index-with-a-content-package}

Utilisez un package de contenu pour les déploiements en production.

1. Dans le module `ui.apps` de votre projet AEM, créez des `ui.apps/src/main/content/jcr_root/_oak_index/customAFReferenceLuceneIndex-1/`.
1. Créez des `.content.xml` dans ce répertoire avec la définition suivante :

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:oak="http://jackrabbit.apache.org/oak/ns/1.0"
             xmlns:jcr="http://www.jcp.org/jcr/1.0"
             xmlns:nt="http://www.jcp.org/jcr/nt/1.0"
             jcr:primaryType="oak:QueryIndexDefinition"
             async="[async]"
             compatVersion="{Long}2"
             evaluatePathRestrictions="{Boolean}true"
             includedPaths="[/content]"
             queryPaths="[/content]"
             reindex="{Boolean}false"
             selectionPolicy="tag"
             tags="[aemformsAFReferences]"
             type="lucene">
       <indexRules jcr:primaryType="nt:unstructured">
           <nt:unstructured jcr:primaryType="nt:unstructured">
               <properties jcr:primaryType="nt:unstructured">
                   <resourceType jcr:primaryType="nt:unstructured"
                                 name="sling:resourceType"
                                 propertyIndex="{Boolean}true"/>
               </properties>
           </nt:unstructured>
       </indexRules>
   </jcr:root>
   ```

1. Ajoutez le filtre suivant à l’intérieur de l’élément `workspaceFilter` existant dans `ui.apps/src/main/content/META-INF/vault/filter.xml`. Gardez les autres filtres du projet inchangés.

   ```xml
   <filter root="/oak:index/customAFReferenceLuceneIndex-1"/>
   ```

1. Générez le projet à l’aide de sa configuration de génération existante et installez le package de contenu obtenu sur l’instance de création. Pour les instructions de chargement et d’installation de package, voir [Gestionnaire de packages](/help/sites-administering/package-manager.md#uploading-packages-from-your-file-system).
1. Vérifiez que `/oak:index/customAFReferenceLuceneIndex-1` existe. Autorisez l’indexation asynchrone à se terminer avant de vérifier le plan de requête.

Si vous choisissez un autre nom d’index, utilisez-le de manière cohérente dans le répertoire, le filtre et le chemin d’accès au référentiel.

## Création de l’index avec CRXDE Lite {#create-the-index-with-crxde-lite}

Utilisez cette alternative dans un environnement de développement au lieu de la méthode du package de contenu.

Utilisez les propriétés suivantes lors de la création du nœud d’index :

| Propriété | Type | Valeur |
| --- | --- | --- |
| `selectionPolicy` | Chaîne | `tag` |
| `compatVersion` | Long | `2` |
| `includedPaths` | `String[]` | `/content` |
| `queryPaths` | `String[]` | `/content` |
| `tags` | `String[]` | `aemformsAFReferences` |
| `type` | Chaîne | `lucene` |
| `async` | `String[]` | `async` |
| `evaluatePathRestrictions` | Booléen | `true` |
| `reindex` | Booléen | `false` |

`String[]` signifie une propriété String à plusieurs valeurs, même si elle ne contient qu’une seule valeur.

1. Ouvrez `http://localhost:4502/crx/de/index.jsp`. Remplacez l’hôte et le port par ceux de votre instance de création.
1. Accédez à `/oak:index`. Cliquez avec le bouton droit sur le nœud et sélectionnez [!UICONTROL Créer] > [!UICONTROL Créer un nœud].
1. Créez des `customAFReferenceLuceneIndex-1` avec le type `oak:QueryIndexDefinition`.
1. Ajoutez les propriétés du tableau ci-dessus au nœud d’index.
1. Sous le nœud d’index, créez la hiérarchie de nœud enfant suivante. Définissez le type de chaque nœud enfant sur `nt:unstructured` :

   ```text
   indexRules
       nt:unstructured
           properties
               resourceType
   ```

1. Sur `resourceType`, ajoutez `name` (chaîne) avec la valeur `sling:resourceType` et `propertyIndex` (booléen) avec la valeur `true`.
1. Sélectionnez [!UICONTROL Enregistrer tout] et attendez la fin de l’indexation asynchrone.

## Vérifiez que la requête utilise l’index . {#verify-that-the-query-uses-the-index}

Vérifiez le plan de requête pour vous assurer que la requête de référence sélectionne votre index personnalisé.

1. Vérifiez que l’indexation asynchrone est terminée. Utilisez [Gestionnaire d’index](/help/sites-administering/operations-dashboard.md#the-index-manager) pour examiner le statut de l’index.
1. Ouvrez [!UICONTROL Outils] > [!UICONTROL Opérations] > [!UICONTROL Diagnostic] > [!UICONTROL Performances des requêtes] et sélectionnez [!UICONTROL Expliquer la requête]. Sélectionnez le langage de requête XPath et saisissez :

   ```text
   /jcr:root/content//element(*, nt:unstructured)[
     (@sling:resourceType = 'fd/af/components/aemform'
     or jcr:like(@sling:resourceType, '%components/aemformscontainer%')
     or jcr:like(@sling:resourceType, '%components/adaptiveForm/fragment%'))]
   option (index tag aemformsAFReferences)
   ```

1. Sélectionnez [!UICONTROL  Expliquer ]. Vérifiez que le plan utilise `lucene:customAFReferenceLuceneIndex-1` et `/oak:index/customAFReferenceLuceneIndex-1`, ou le nom d&#39;index de votre choix, pour les branches de la requête plutôt qu&#39;un plan de traversée. Pour plus d’informations, voir [Expliquer la requête](/help/sites-administering/operations-dashboard.md#explain-query).
1. Répétez l’opération de publication de fragment d’expérience qui a généré l’avertissement. Recherchez `error.log` nouveaux avertissements de traversée de `com.adobe.aem.formsndocuments.publish.AssetReferenceProvider.resolvePathsToFindReferences`.

Si le plan ne sélectionne pas l’index personnalisé, vérifiez la balise , la hiérarchie des `indexRules` et la définition de propriété `sling:resourceType` par rapport aux exemples ci-dessus. Pour un diagnostic plus approfondi, voir [Dépannage des index Oak](/help/sites-deploying/troubleshooting-oak-indexes.md).

## Tâches connexes {#related-tasks}

Pour plus d’informations sur les performances des requêtes et la configuration de l’index, voir :

* [Requêtes et indexation Oak](/help/sites-deploying/queries-and-indexing.md)
* [Bonnes pratiques relatives aux requêtes et à l’indexation](/help/sites-deploying/best-practices-for-queries-and-indexing.md)
* [Résolution des problèmes de lenteur des requêtes](/help/sites-developing/troubleshooting-slow-queries.md)
