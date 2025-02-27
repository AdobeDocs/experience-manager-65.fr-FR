---
title: Utiliser AEM avec le Commerce Cloud SAP
description: Découvrez comment utiliser Adobe Experience Manager avec SAP Commerce Cloud.
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
exl-id: c342f789-2ff7-4802-99c7-c3699218fe47
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '1574'
ht-degree: 100%

---

# SAP Commerce Cloud{#sap-commerce-cloud}

Après l’installation, vous pouvez configurer votre instance :

1. [Configurer la recherche à facettes pour Geometrixx Outdoors](#configure-the-facetted-search-for-geometrixx-outdoors).
1. [Configuration de la version du catalogue](#configure-the-catalog-version).
1. [Configuration de la structure d’importation](#configure-the-import-structure).
1. [Configuration des attributs de produit à charger](#configure-the-product-attributes-to-load).
1. [Importation des données de produit](#importing-the-product-data).
1. [Configuration de l’importateur de catalogues](#configure-the-catalog-importer).
1. Utilisez l’[importateur pour importer le catalogue](#catalog-import) dans un emplacement spécifique d’AEM.

## Configurer la recherche à facettes pour Geometrixx Outdoors {#configure-the-facetted-search-for-geometrixx-outdoors}

>[!NOTE]
>
>Cette étape n’est pas nécessaire pour Hybris 5.3.0.1 et les versions ultérieures.

1. Dans votre navigateur, accédez à la **console de gestion Hybris** à l’emplacement :

   [http://localhost:9001/hmc/hybris](http://localhost:9001/hmc/hybris)

1. Dans la barre latérale, sélectionnez **Système**, puis **Recherche à facettes**, puis **Configuration de la recherche à facettes**.
1. **Ouvrez l’éditeur** sur **Configuration for clothescatalog Sample Solr**.

1. Sous **Versions des catalogues**, utilisez **Ajouter une version de catalogue** pour ajouter `outdoors-Staged` et `outdoors-Online` à la liste.
1. **Enregistrez** la configuration.
1. Ouvrez les **Types d’éléments SOLR** pour ajouter les **Tris SOLR** à `ClothesVariantProduct` :

   * relevance (« Pertinence », score)
   * name-asc (« Nom (ascendant) », name)
   * name-desc (« Nom (descendant) », name)
   * price-asc (« Prix (ascendant) », priceValue)
   * price-desc (« Prix (descendant) », priceValue)

   >[!NOTE]
   >
   >Dans le menu contextuel (généralement accessible par un clic droit), sélectionnez `Create Solr sort`.
   >
   >Sous Hybris 5.0.0, ouvrez l’onglet `Indexed Types`, double-cliquez sur `ClothesVariantProduct`, puis sur l’onglet `SOLR Sort`.

   ![chlimage_1-36](/help/sites-administering/assets/chlimage_1-36a.png)

1. Dans l’onglet **Types indexés**, définissez le **Type composé** sur :

   `Product - Product`

1. Dans l’onglet **Types indexés**, définissez les **Requêtes de l’indexeur** pour `full` :

   ```shell
   SELECT {pk} FROM {Product} WHERE {pk} NOT IN ({{SELECT {baseProductpk} FROM {variantproduct}}})
   ```

1. Dans l’onglet **Types indexés**, définissez les **Requêtes de l’indexeur** pour `incremental` :

   ```shell
   SELECT {pk} FROM {Product} WHERE {pk} NOT IN ({{SELECT {baseProductpk} FROM {variantproduct}}}) AND {modifiedtime} <= ?lastIndexTime
   ```

1. Dans l’onglet **Types indexés**, définissez la facette `category`. Double-cliquez sur la dernière entrée de la liste de catégorie pour afficher l’onglet **Propriété indexée** :

   >[!NOTE]
   >
   >Sous Hybris 5.2, assurez-vous que l’attribut `Facet` du tableau Propriétés est sélectionné en vous reportant à la capture d’écran ci-dessous :

   ![chlimage_1-37](/help/sites-administering/assets/chlimage_1-37a.png) ![chlimage_1-38](/help/sites-administering/assets/chlimage_1-38a.png)

1. Ouvrez l’onglet **Paramètres de facettes** et définissez les valeurs de champs suivantes :

   ![chlimage_1-39](/help/sites-administering/assets/chlimage_1-39a.png)

1. **Enregistrez** les modifications.
1. Sous **Types d’éléments SOLR**, définissez la facette `price` en vous reportant aux captures d’écran suivantes. Comme pour `category`, double-cliquez sur `price` pour ouvrir l’onglet **Propriété indexée** :

   ![chlimage_1-40](/help/sites-administering/assets/chlimage_1-40a.png)

1. Ouvrez l’onglet **Paramètres de facettes** et définissez les valeurs de champs suivantes :

   ![chlimage_1-41](/help/sites-administering/assets/chlimage_1-41a.png)

1. **Enregistrez** les modifications.
1. Ouvrez **Système**, **Recherche à facettes**, puis **Assistant d’opération de l’indexeur**. Démarrez une tâche cron :

   * **Opération de l’indexeur** : `full`
   * **Configuration de Solr** : `Sample Solr Config for Clothes`

## Configuration de la version du catalogue {#configure-the-catalog-version}

La **version du catalogue** (`hybris.catalog.version`) importée peut être configurée pour le service OSGi :

**Configuration Day CQ Commerce Hybris**
( `com.adobe.cq.commerce.hybris.common.DefaultHybrisConfigurationService`)

La **version du catalogue** est généralement définie sur `Online` ou `Staged` (valeur par défaut).

>[!NOTE]
>
>Dans AEM, il existe plusieurs méthodes pour gérer les paramètres de configuration pour ces services. Pour plus d’informations, voir [Configuration d’OSGi](/help/sites-deploying/configuring-osgi.md). Pour obtenir une liste exhaustive des paramètres configurables et de leurs valeurs par défaut, reportez-vous également à la console.

La sortie du journal fournit des commentaires sur les pages et composants créés et signale les erreurs potentielles.

## Configurer la structure d’importation {#configure-the-import-structure}

La liste suivante présente un exemple de structure (de ressources, de pages et de composants) créée par défaut :

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

Ce type de structure est créé par le service OSGi `DefaultImportHandler`, qui met en œuvre l’interface `ImportHandler`. L’importateur appelle un gestionnaire d’import pour créer des produits, des variations de produits, des catégories, des ressources, etc.

>[!NOTE]
>
>Vous pouvez [personnaliser ce processus en implémentant votre propre gestionnaire d’importation](#configure-the-import-structure).

La structure à générer lors de l’importation peut être configurée pour :

``**Gestionnaire d’importation par défaut Day CQ Commerce Hybris**
`(com.adobe.cq.commerce.hybris.importer.DefaultImportHandler`)

Dans AEM, il existe plusieurs méthodes pour gérer les paramètres de configuration pour ces services. Pour plus d’informations, voir [Configuration d’OSGi](/help/sites-deploying/configuring-osgi.md). Pour obtenir une liste exhaustive des paramètres configurables et de leurs valeurs par défaut, reportez-vous également à la console.

## Configurer les attributs de produit à charger {#configure-the-product-attributes-to-load}

L’analyseur de réponse peut être configuré pour définir les propriétés et les attributs à charger pour les produits (variantes) :

1. Configurez le lot OSGi :

   **Analyseur de réponse par défaut Day CQ Commerce Hybris**
(`com.adobe.cq.commerce.hybris.impl.importer.DefaultResponseParser`)

   Vous pouvez définir différents attributs et options nécessaires au chargement et au mappage.

   >[!NOTE]
   >
   >Dans AEM, il existe plusieurs méthodes pour gérer les paramètres de configuration pour ces services. Pour plus d’informations, voir [Configuration d’OSGi](/help/sites-deploying/configuring-osgi.md). Pour obtenir une liste exhaustive des paramètres configurables et de leurs valeurs par défaut, reportez-vous également à la console.

## Importer les données de produit {#importing-the-product-data}

Il existe différentes manières d’importer les données de produit. Les données de produit peuvent être importées lors de la configuration initiale de l’environnement ou après la modification de données Hybris :

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
>La mise en œuvre d’Hybris (c’est-à-dire `geometrixx-outdoors/en_US`) stocke uniquement les identifiants de produit et d’autres informations de base sous `/etc/commerce`.
>
>Le serveur Hybris est référencé lors de chaque demande d’informations sur un produit.

### Importation complète {#full-import}

1. Si nécessaire, supprimez toutes les données de produit existantes à l’aide de CRXDE Lite.

   1. Accédez à la sous-arborescence contenant les données de produit :

      `/etc/commerce/products`

      Par exemple :

      [`http://localhost:4502/crx/de/index.jsp#/etc/commerce/products`](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

   1. Supprimez le nœud qui contient les données d’un produit, par exemple, `outdoors`.
   1. **Enregistrez tout** pour conserver la modification.

1. Ouvrez l’importateur Hybris dans AEM :

   `/etc/importers/hybris.html`

   Par exemple :

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. Configurez les paramètres requis, par exemple :

   ![chlimage_1-42](/help/sites-administering/assets/chlimage_1-42a.png)

1. Cliquez sur **Importer le catalogue** pour commencer l’importation.

   Vous pouvez ensuite vérifier les données importées à l’adresse :

   ```
       /etc/commerce/products/outdoors
   ```

   Vous pouvez l’ouvrir dans CRXDE Lite, par exemple :

   `[http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)`

### Importation incrémentielle {#incremental-import}

1. Vérifiez les informations contenues dans AEM pour le ou les produits concernés, dans la sous-arborescence appropriée sous :

   `/etc/commerce/products`

   Vous pouvez l’ouvrir dans CRXDE Lite, par exemple :

   [http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

1. Dans Hybris, mettez à jour les informations conservées sur les produits concernés.

1. Ouvrez l’importateur Hybris dans AEM :

   `/etc/importers/hybris.html`

   Par exemple :

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. Sélectionnez la case **Importation incrémentielle**.
1. Cliquez sur **Importer le catalogue** pour commencer l’importation.

   Une fois l’opération terminée, vous pouvez vérifier les données mises à jour dans AEM sous :

   ```
       /etc/commerce/products
   ```


### Mise à jour express {#express-update}

Le processus d’importation peut être long. Ainsi, en prolongement de la synchronisation des produits, vous pouvez sélectionner des sections spécifiques du catalogue pour les mettre rapidement à jour (déclenchement manuel). Cette méthode utilise le flux d’exportation avec la configuration des attributs standard.

1. Vérifiez les informations contenues dans AEM pour le ou les produits concernés, dans la sous-arborescence appropriée sous :

   `/etc/commerce/products`

   Vous pouvez l’ouvrir dans CRXDE Lite, par exemple :

   [http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

1. Dans Hybris, mettez à jour les informations conservées sur les produits concernés.

1. Dans Hybris, ajoutez un ou plusieurs produits à la file d’attente express, par exemple :

   ![chlimage_1-43](/help/sites-administering/assets/chlimage_1-43a.png)

1. Ouvrez l’importateur Hybris dans AEM :

   `/etc/importers/hybris.html`

   Par exemple :

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. Sélectionnez la case **Mise à jour express**.
1. Cliquez sur **Importer le catalogue** pour commencer l’importation.

   Une fois l’opération terminée, vous pouvez vérifier les données mises à jour dans AEM sous :

   ```
       /etc/commerce/products
   ```

## Configuration de l’importateur de catalogues {#configure-the-catalog-importer}

Il est possible d’importer le catalogue Hybris dans AEM à l’aide de l’importateur par lots pour des catalogues, des catégories et des produits Hybris.

Les paramètres utilisés par l’importateur peuvent être configurés pour :

**Importateur de catalogue Day CQ Commerce Hybris**
(`com.adobe.cq.commerce.hybris.impl.importer.DefaultHybrisImporter`)

Dans AEM, il existe plusieurs méthodes pour gérer les paramètres de configuration pour ces services. Pour plus d’informations, voir [Configuration d’OSGi](/help/sites-deploying/configuring-osgi.md). Pour obtenir une liste exhaustive des paramètres configurables et de leurs valeurs par défaut, reportez-vous également à la console.

## Importer des catalogues {#catalog-import}

Le package Hybris est fourni avec un importateur de catalogues pour configurer la structure de page initiale.

Cette option est disponible à partir de :

`http://localhost:4502/etc/importers/hybris.html`

![ecommerceimportconsole](/help/sites-administering/assets/ecommerceimportconsole.png)

Les informations suivantes sont fournies :

* **Boutique de base**
Identificateur de la boutique de base configurée dans Hybris.

* **Catalogue**
Identificateur du catalogue à importer.

* **Chemin racine**
Chemin d’accès racine où doit être importé le catalogue.

## Supprimer un produit du catalogue {#removing-a-product-from-the-catalog}

Pour supprimer un ou plusieurs produits du catalogue :

1. [Configurez les paramètres du service OSGi](/help/sites-deploying/configuring-osgi.md) **Importateur de catalogues Hybris Day CQ Commerce**. Voir aussi [Configuration de l’importateur de catalogues](#configure-the-catalog-importer).

   Activez les propriétés suivantes :

   * **Activer la suppression de produit**
   * **Activer la suppression de ressources de produit**

   >[!NOTE]
   >
   >Dans AEM, il existe plusieurs méthodes pour gérer les paramètres de configuration pour ces services. Pour plus d’informations, voir [Configuration d’OSGi](/help/sites-deploying/configuring-osgi.md). Pour obtenir une liste exhaustive des paramètres configurables et de leurs valeurs par défaut, reportez-vous également à la console.

1. Initialisez l’importateur en exécutant deux mises à jour incrémentielle (voir [Importation d’un catalogue](#catalog-import)) :

   * Le premier cycle de mise à jour génère un ensemble de produits modifiés, mentionnés dans la liste de journaux.
   * Pour la deuxième fois, aucun produit ne doit être mis à jour.

   >[!NOTE]
   >
   >La première importation permet d’initialiser les informations du produit. La deuxième importation vérifie que tout a fonctionné et que l’ensemble des produits est prêt.

1. Consultez la page de catégories qui contient le produit à supprimer. Les détails du produit doivent être visibles.

   Par exemple, la catégorie suivante affiche les détails du produit Cajamara :

   [http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html](http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html)

1. Supprimez le produit dans la console Hybris. À l’aide de l’option **Modifier le statut d’approbation**, définissez le statut sur `unapproved`. Le produit est supprimé du flux en direct.

   Par exemple :

   * Ouvrez la page [http://localhost:9001/productcockpit](http://localhost:9001/productcockpit).
   * Sélectionnez le catalogue `Outdoors Staged`.
   * Recherchez `Cajamara`.
   * Sélectionnez ce produit et définissez le statut d’approbation sur `unapproved`.

1. Procédez à une autre mise à jour incrémentielle (voir [Importation d’un catalogue](#catalog-import)). Le journal répertorie le produit supprimé.
1. [Déployez](/help/commerce/cif-classic/administering/generic.md#rolling-out-a-catalog) le catalogue approprié. Le produit et la page produit ont été supprimés d’AEM.

   Par exemple :

   * Ouvrez :

     [http://localhost:4502/aem/catalogs.html/content/catalogs/geometrixx-outdoors-hybris](http://localhost:4502/aem/catalogs.html/content/catalogs/geometrixx-outdoors-hybris)

   * Déployez le catalogue `Hybris Base`.
   * Ouvrez :

     [http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html](http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html)

   * Le produit `Cajamara` est supprimé de la catégorie `Bike`.

1. Pour rétablir le produit, procédez comme suit :

   1. Dans Hybris, redéfinissez le statut d’approbation sur **approuvé**.
   1. Dans AEM :

      1. Effectuez une mise à jour incrémentielle.
      1. Redéployez le catalogue approprié.
      1. Actualisez la page de catégorie appropriée.

## Ajouter un historique de commandes à ClientContext {#add-order-history-trait-to-the-client-context}

Pour ajouter un historique de commandes à [ClientContext](/help/sites-developing/client-context.md), procédez comme suit :

1. Ouvrez la [page de conception de ClientContext](/help/sites-administering/client-context.md) selon l’une des méthodes suivantes :

   * Ouvrez une page à modifier, puis ouvrez ClientContext à l’aide des raccourcis clavier **Ctrl+Alt+C** (Windows) ou **Ctrl+Option+C** (Mac). À l’aide de l’icône de crayon dans le coin supérieur gauche de ClientContext, **ouvrez la page de conception de ClientContext**.
   * Accédez directement à [http://localhost:4502/etc/clientcontext/default/content.html](http://localhost:4502/etc/clientcontext/default/content.html).

1. [Ajoutez le composant **Historique de commandes**](/help/sites-administering/client-context.md#adding-a-property-component) au composant **Panier** de ClientContext.
1. Vous pouvez confirmer que ClientContext affiche les détails de votre historique de commandes. Par exemple :

   1. Ouvrez [ClientContext](/help/sites-administering/client-context.md).
   1. Ajoutez un article au panier.
   1. Effectuez le passage en caisse.
   1. Vérifiez ClientContext.
   1. Ajoutez un autre article au panier.
   1. Accédez à la page de passage en caisse :

      * ClientContext affiche un récapitulatif de l’historique des commandes.
      * Un message stipulant que vous êtes un client régulier s’affiche.

   >[!NOTE]
   >
   >Le message est obtenu de la façon suivante :
   >
   >* Accédez à [http://localhost:4502/content/campaigns/geometrixx-outdoors/hybris-returning-customer.html](http://localhost:4502/content/campaigns/geometrixx-outdoors/hybris-returning-customer.html).
   >
   >  La campagne se compose d’une expérience.
   >
   >* Cliquez sur le segment ([http://localhost:4502/etc/segmentation/geometrixx-outdoors/returning-customer.html](http://localhost:4502/etc/segmentation/geometrixx-outdoors/returning-customer.html)).
   >
   >* Le segment est créé à l’aide de la caractéristique **Propriété de l’historique de commandes**.
