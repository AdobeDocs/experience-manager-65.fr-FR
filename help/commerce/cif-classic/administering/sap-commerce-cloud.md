---
title: SAP Commerce Cloud
seo-title: SAP Commerce Cloud
description: Découvrez comment utiliser AEM avec SAP Commerce Cloud.
seo-description: Découvrez comment utiliser AEM avec SAP Commerce Cloud.
uuid: cee1a781-fcba-461e-a0a4-c561a1dbcbf3
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
translation-type: tm+mt
source-git-commit: 1cef6f87fa66fd78d439c23e6ac907f9531b8fd6
workflow-type: tm+mt
source-wordcount: '1726'
ht-degree: 91%

---

# SAP Commerce Cloud{#sap-commerce-cloud}

Après l’installation, vous pouvez configurer votre instance :

1. [Configuration de la recherche à facette pour Geometrixx Outdoors](#configure-the-facetted-search-for-geometrixx-outdoors)
1. [Configuration de la version du catalogue](#configure-the-catalog-version)
1. [Configuration de la structure d’importation](#configure-the-import-structure)
1. [Configuration des attributs du produit à charger](#configure-the-product-attributes-to-load)
1. [Importation des données du produit](#importing-the-product-data)
1. [Configuration de l’importateur de catalogues](#configure-the-catalog-importer)
1. Utilisation de l’[importateur pour importer le catalogue](#catalog-import) dans un emplacement spécifique dans AEM

## Configuration de la recherche à facette de Geometrixx Outdoors {#configure-the-facetted-search-for-geometrixx-outdoors}

>[!NOTE]
>
>Ceci n’est pas nécessaire pour Hybris 5.3.0.1 et version ultérieure.

1. Dans le navigateur, accédez à la **console de gestion Hybris**, à l’adresse :

   [http://localhost:9001/hmc/hybris](http://localhost:9001/hmc/hybris)

1. Dans la barre latérale, sélectionnez **System**, puis **Facet search** et **Facet Search Config**.
1. **Ouvrez l’éditeur** sur **Sample Solr Configuration for clothescatalog**.

1. Sous **Catalog versions**, utilisez **Add Catalog version** pour ajouter `outdoors-Staged` et `outdoors-Online` à la liste.
1. **Enregistrez la configuration.**
1. Ouvrez **SOLR Item types** pour ajouter **SOLR Sorts** à `ClothesVariantProduct` :

   * relevance (« Pertinence », score)
   * name-asc (« Nom (ascendant) », nom)
   * name-desc (« Nom (descendant) », nom)
   * price-asc (« Prix (ascendant) », priceValue)
   * price-desc (« Prix (descendant) », priceValue)

   >[!NOTE]
   >
   >Utilisez le menu contextuel (généralement clic droit) pour sélectionner `Create Solr sort`.
   >
   >Pour Hybris 5.0.0, ouvrez l&#39;onglet `Indexed Types`, cliquez en doublon sur `ClothesVariantProduct`, puis l&#39;onglet `SOLR Sort`.

   ![chlimage_1-36](/help/sites-administering/assets/chlimage_1-36a.png)

1. Dans l’onglet **Indexed Types**, définissez **Composed Type** sur :

   `Product - Product`

1. Dans l’onglet **Indexed Types**, définissez les requêtes **Indexer queries** sur `full` :

   ```shell
   SELECT {pk} FROM {Product} WHERE {pk} NOT IN ({{SELECT {baseProductpk} FROM {variantproduct}}})
   ```

1. Dans l’onglet **Indexed Types**, définissez les requêtes **Indexer queries** sur `incremental` :

   ```shell
   SELECT {pk} FROM {Product} WHERE {pk} NOT IN ({{SELECT {baseProductpk} FROM {variantproduct}}}) AND {modifiedtime} <= ?lastIndexTime
   ```

1. Dans l’onglet **Indexed Types**, définissez la facette `category`. Double-cliquez sur la dernière entrée de la liste « category » pour afficher l’onglet **Indexed property** :

   >[!NOTE]
   >
   >Sous Hybris 5.2, assurez-vous que l’attribut `Facet` du tableau Properties est sélectionné en vous reportant à la capture d’écran ci-dessous :

   ![chlimage_1-37](/help/sites-administering/assets/chlimage_1-37a.png) ![chlimage_1-38](/help/sites-administering/assets/chlimage_1-38a.png)

1. Ouvrez l’onglet **Facet Settings** et définissez les valeurs de champs suivantes :

   ![chlimage_1-39](/help/sites-administering/assets/chlimage_1-39a.png)

1. **Enregistrez** les modifications.
1. Sous **SOLR Item types**, définissez la facette `price` en vous reportant aux captures d’écran suivantes. Comme pour `category`, double-cliquez sur `price` pour ouvrir l’onglet **Indexed property** :

   ![chlimage_1-40](/help/sites-administering/assets/chlimage_1-40a.png)

1. Ouvrez l’onglet **Facet Settings** et définissez les valeurs de champs suivantes :

   ![chlimage_1-41](/help/sites-administering/assets/chlimage_1-41a.png)

1. **Enregistrez** les modifications.
1. Ouvrez **System**, **Facet search**, puis **Indexer operation wizard**. Commencez une tâche cronjob :

   * **Opération** d&#39;indexation :  `full`
   * **Configuration** Solr :  `Sample Solr Config for Clothes`

## Configuration de la version du catalogue {#configure-the-catalog-version}

La **version du catalogue** (`hybris.catalog.version`) importée peut être configurée pour le service OSGi :

**Configuration Day CQ Commerce Hybris**
( `com.adobe.cq.commerce.hybris.common.DefaultHybrisConfigurationService`)

La **version du catalogue** est généralement définie sur `Online` (en ligne) ou `Staged` (intermédiaire ; valeur par défaut).

>[!NOTE]
>
>Dans AEM, il existe plusieurs méthodes pour gérer les paramètres de configuration pour ces services. Pour plus d’informations, voir [Configuration d’OSGi](/help/sites-deploying/configuring-osgi.md). Pour obtenir une liste exhaustive des paramètres configurables et de leurs valeurs par défaut, reportez-vous également à la console.

La sortie du journal fournit un retour sur les pages et les composants créés et signale les erreurs potentielles.

## Configuration de la structure d’importation  {#configure-the-import-structure}

La liste ci-dessous présente un exemple de la structure (des ressources, des pages et des composants) créée par défaut :

```shell
+ /content/dam/path/to/images
  + 12345.jpg (dam:Asset)
    + ...
  + ...
+ /content/site/en
  - cq:commerceProvider = "hybris"
  - cq:hybrisBaseStore = "basestore"
  - cq:hybrisCatalogId = "catalog"
  + category1 (cq:Page)
    + jcr:content (cq:PageContent)
      - jcr:title = "Category 1"
    + category11 (cq:Page)
      + jcr:content (cq:PageContent)
        - jcr:title = "Category 1.1"
      + 12345 (cq:Page)
        + jcr:content (cq:PageContent)
          + par
            + product (nt:unstructured)
              - cq:hybrisProductId = "12345"
              - sling:resourceType = "commerce/components/product"
              + image (nt:unstructured)
                - sling:resourceType = "commerce/components/product/image"
                - fileReference = "/content/dam/path/to/images/12345.jpg"
              + 12345.1-S (nt:unstructured)
                - cq:hybrisProductId = "12345.1-S"
                - sling:resourceType = "commerce/components/product"
                + image (nt:unstructured)
                  - sling:resourceType = "commerce/components/product/image"
                  - fileReference = "/content/dam/path/to/images/12345.1-S.jpg"
              + ...
```

Ce type de structure est créé par le service OSGi `DefaultImportHandler`, qui met en œuvre l’interface `ImportHandler`. L’importateur réel appelle un gestionnaire d’importation pour créer des produits, des variantes de produit, des catégories, des ressources, etc.

>[!NOTE]
>
>Vous pouvez [personnaliser ce processus en mettant en œuvre votre propre gestionnaire d’importation](#configure-the-import-structure).

La structure à générer lors de l’importation peut être configurée pour :

``**Day CQ Commerce Hybris Default Import Handler**
`(com.adobe.cq.commerce.hybris.importer.DefaultImportHandler`)

Dans AEM, il existe plusieurs méthodes pour gérer les paramètres de configuration pour ces services. Pour plus d’informations, voir [Configuration d’OSGi](/help/sites-deploying/configuring-osgi.md). Pour obtenir une liste exhaustive des paramètres configurables et de leurs valeurs par défaut, reportez-vous également à la console.

## Configuration des attributs du produit à charger  {#configure-the-product-attributes-to-load}

L’analyseur de réponse peut être configuré pour définir des propriétés et des attributs à charger pour des produits (variantes) :

1. Configurez le lot OSGi :

   **Day CQ Commerce Hybris Default Response Parser**
(`com.adobe.cq.commerce.hybris.impl.importer.DefaultResponseParser`)

   Vous pouvez définir différents attributs et options nécessaires au chargement et au mappage.

   >[!NOTE]
   >
   >Dans AEM, il existe plusieurs méthodes pour gérer les paramètres de configuration pour ces services. Pour plus d’informations, voir [Configuration d’OSGi](/help/sites-deploying/configuring-osgi.md). Pour obtenir une liste exhaustive des paramètres configurables et de leurs valeurs par défaut, reportez-vous également à la console.

## Importation des données de produit {#importing-the-product-data}

Vous pouvez importer les données d’un produit de différentes façons. Les données d’un produit peuvent être importées lors de la configuration initiale de l’environnement ou après que des modifications ont été apportées aux données Hybris :

* [Importation complète](#full-import)
* [Importation incrémentielle](#incremental-import)
* [Mise à jour express](#express-update)

Les informations sur les produits importées d’Hybris se trouvent dans le référentiel sous :

`/etc/commerce/products`

Les propriétés ci-dessous indiquent le lien avec Hybris :

* `commerceProvider`
* `cq:hybrisCatalogId`
* `cq:hybrisProductID`

>[!NOTE]
>
>La mise en oeuvre de l&#39;hybris (c.-à-d. `geometrixx-outdoors/en_US`) ne stocke que les ID de produit et d&#39;autres informations de base sous `/etc/commerce`.
>
>Le serveur Hybris est référencé chaque fois que des informations sur un produit sont demandées.

### Importation complète  {#full-import}

1. Si nécessaire, supprimez toutes les données existantes d’un produit à l’aide de CRXDE Lite.

   1. Accédez à la sous-arborescence contenant les données du produit :

      `/etc/commerce/products`

      Par exemple :

      [`http://localhost:4502/crx/de/index.jsp#/etc/commerce/products`](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

   1. Supprimez le nœud qui contient les données d’un produit, par exemple, `outdoors`.
   1. **Enregistrez tout** pour conserver la modification.

1. Ouvrez l’importateur Hybris dans AEM :

   `/etc/importers/hybris.html`

   Par exemple :

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. Configurez les paramètres nécessaires, par exemple :

   ![chlimage_1-42](/help/sites-administering/assets/chlimage_1-42a.png)

1. Cliquez sur **Import Catalog** pour commencer l’importation.

   Vous pouvez ensuite vérifier les données importées à l’adresse :

   ```
       /etc/commerce/products/outdoors
   ```

   Vous pouvez l’ouvrir en CRXDE Lite ; par exemple :

   `[http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)`

### Importation incrémentielle {#incremental-import}

1. Consultez les informations que contient AEM pour les produits correspondants, dans la sous-arborescence appropriée sous :

   `/etc/commerce/products`

   Vous pouvez l’ouvrir en CRXDE Lite ; par exemple :

   [http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

1. Dans Hybris, mettez à jour les informations conservées sur les produits correspondants.

1. Ouvrez l’importateur Hybris dans AEM :

   `/etc/importers/hybris.html`

   Par exemple :

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. Activez la case à cocher **Incremental Import**.
1. Cliquez sur **Import Catalog** pour commencer l’importation.

   Une fois l’opération terminée, vous pouvez vérifier les données mises à jour dans AEM sous :

   ```
       /etc/commerce/products
   ```


### Mise à jour express {#express-update}

Le processus d’importation peut être long. Ainsi, en prolongement de la synchronisation des produits, vous pouvez sélectionner des sections spécifiques du catalogue pour les mettre rapidement à jour (déclenchement manuel). Pour ce faire, le flux d’exportation est utilisé conjointement avec la configuration d’attributs standard.

1. Consultez les informations que contient AEM pour les produits correspondants, dans la sous-arborescence appropriée sous :

   `/etc/commerce/products`

   Vous pouvez l’ouvrir en CRXDE Lite ; par exemple :

   [http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

1. Dans Hybris, mettez à jour les informations conservées sur les produits correspondants.

1. Dans Hybris, ajoutez les produits à la file d’attente Rapide, par exemple :

   ![chlimage_1-43](/help/sites-administering/assets/chlimage_1-43a.png)

1. Ouvrez l’importateur Hybris dans AEM :

   `/etc/importers/hybris.html`

   Par exemple :

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. Activez la case à cocher **Mise à jour express**.
1. Cliquez sur **Import Catalog** pour commencer l’importation.

   Une fois l’opération terminée, vous pouvez vérifier les données mises à jour dans AEM sous :

   ```
       /etc/commerce/products
   ```

   ` [](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)`

## Configuration de l’importateur de catalogues {#configure-the-catalog-importer}

Il est possible d’importer le catalogue Hybris dans AEM à l’aide de l’importateur par lots pour des catalogues, des catégories et des produits Hybris.

Les paramètres utilisés par l’importateur peuvent être configurés pour :

**Day CQ Commerce Hybris Catalog Importer**
( `com.adobe.cq.commerce.hybris.impl.importer.DefaultHybrisImporter`)

Dans AEM, il existe plusieurs méthodes pour gérer les paramètres de configuration pour ces services. Pour plus d’informations, voir [Configuration d’OSGi](/help/sites-deploying/configuring-osgi.md). Pour obtenir une liste exhaustive des paramètres configurables et de leurs valeurs par défaut, reportez-vous également à la console.

## Importation d’un catalogue {#catalog-import}

Le module Hybris est fourni avec un importateur de catalogues pour configurer la structure de page initiale.

Il est disponible à l’adresse suivante :

`http://localhost:4502/etc/importers/hybris.html`

![ecommerceimportconsole](/help/sites-administering/assets/ecommerceimportconsole.png)

Les informations ci-dessous doivent être fournies :

* **Base store**  Identificateur de la boutique de base configurée dans Hybris.

* **Catalog**  Identificateur du catalogue à importer.

* **Root path**  Chemin d’accès racine où doit être importé le catalogue.

## Suppression d’un produit du catalogue {#removing-a-product-from-the-catalog}

Pour supprimer un ou plusieurs produits du catalogue, procédez comme suit :

1. [Configurez le service OSGi](/help/sites-deploying/configuring-osgi.md) **Day CQ Commerce Hybris Catalog Importer**. Voir aussi [Configuration de l’importateur de catalogues](#configure-the-catalog-importer).

   Activez les propriétés suivantes :

   * **Enable product removal**
   * **Enable product asset removal**

   >[!NOTE]
   >
   >Dans AEM, il existe plusieurs méthodes pour gérer les paramètres de configuration pour ces services. Pour plus d’informations, voir [Configuration d’OSGi](/help/sites-deploying/configuring-osgi.md). Pour obtenir une liste exhaustive des paramètres configurables et de leurs valeurs par défaut, reportez-vous également à la console.

1. Initialisez l’importateur en exécutant deux mises à jour incrémentielle (voir [Importation d’un catalogue](#catalog-import)) :

   * Le premier cycle de mise à jour génère un ensemble de produits modifiés, mentionnés dans la liste de journaux.
   * Pour la seconde mise à jour, aucun produit ne doit être mis à jour.

   >[!NOTE]
   >
   >La première importation permet d’initialiser les informations du produit. La deuxième importation vérifie que tout a fonctionné et que l’ensemble de produits est prêt.

1. Consultez la page de catégories qui contient le produit à supprimer. Les détails du produit sont normalement visibles.

   Par exemple, la catégorie ci-dessous présente les détails sur le produit Cajamara :

   [http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html](http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html)

1. Supprimez le produit dans la console Hybris. À l’aide de l’option **Change approval status**, définissez l’état sur `unapproved`. Le produit sera supprimé du flux en direct.

   Par exemple :

   * Ouvrez la page [http://localhost:9001/productcockpit](http://localhost:9001/productcockpit).
   * Sélectionnez le catalogue `Outdoors Staged`
   * Recherchez `Cajamara`
   * Sélectionnez ce produit et définissez l’état d’approbation sur `unapproved`.

1. Procédez à une autre mise à jour incrémentielle (voir [Importation d’un catalogue](#catalog-import)). Le produit supprimé apparaît dans le journal.
1. [Déployez](/help/commerce/cif-classic/administering/generic.md#rolling-out-a-catalog) le catalogue approprié. Le produit et la page des produits sont supprimés d’AEM.

   Par exemple :

   * Ouvrez :

      [http://localhost:4502/aem/catalogs.html/content/catalogs/geometrixx-outdoors-hybris](http://localhost:4502/aem/catalogs.html/content/catalogs/geometrixx-outdoors-hybris)

   * Déploiement du catalogue `Hybris Base`
   * Ouvrez :

      [http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html](http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html)

   * Le produit `Cajamara` a été supprimé de la catégorie `Bike`

1. Pour réinstaller le produit :

   1. Dans Hybris, redéfinissez l’état d’approbation sur **approved**.
   1. Dans AEM :

      1. Procédez à une mise à jour incrémentielle.
      1. Redéployez le catalogue approprié.
      1. Actualisez la page de catégories appropriée.

## Ajout de la caractéristique Historique de commandes à ClientContext  {#add-order-history-trait-to-the-client-context}

Pour ajouter un historique de commandes à [ClientContext](/help/sites-developing/client-context.md), procédez comme suit :

1. Ouvrez la [page de conception de ClientContext](/help/sites-administering/client-context.md) selon l’une des méthodes suivantes :

   * Ouvrez une page pour modification, puis ouvrez le contexte client à l’aide de **Ctrl-Alt-c** (windows) ou **control-option-c** (Mac). À l’aide de l’icône de crayon dans le coin supérieur gauche de ClientContext, **ouvrez la page de conception de ClientContext**.
   * Accédez directement à [http://localhost:4502/etc/clientcontext/default/content.html](http://localhost:4502/etc/clientcontext/default/content.html).

1. [Ajoutez le composant **Historique de commandes**](/help/sites-administering/client-context.md#adding-a-property-component) au composant **Panier** de ClientContext.
1. Vous pouvez confirmer que ClientContext affiche les détails de votre historique de commandes. Par exemple :

   1. Ouvrez [ClientContext](/help/sites-administering/client-context.md).
   1. Ajoutez un article au panier.
   1. Passez en caisse.
   1. Vérifiez ClientContext.
   1. Ajoutez un autre article au panier.
   1. Accédez à la page Passage en caisse :

      * ClientContext affiche un récapitulatif de l’historique des commandes.
      * Un message stipulant que vous êtes un client régulier s’affiche.

   >[!NOTE]
   >
   >Le message est obtenu de la façon suivante :
   >
   >* Accédez à [http://localhost:4502/content/campaigns/geometrixx-outdoors/hybris-returning-customer.html](http://localhost:4502/content/campaigns/geometrixx-outdoors/hybris-returning-customer.html)
   >
   >  La campagne se compose d’une expérience.
   >
   >* Cliquez sur le segment ([http://localhost:4502/etc/segmentation/geometrixx-outdoors/returning-customer.html](http://localhost:4502/etc/segmentation/geometrixx-outdoors/returning-customer.html)).
      >
      >
   * Le segment est créé à l’aide de la caractéristique **Propriété de l’historique de commandes**.

