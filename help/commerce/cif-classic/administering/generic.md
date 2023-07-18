---
title: Administration d’eCommerce générique
seo-title: Administering generic eCommerce
description: La solution générique AEM fournit des méthodes de gestion des informations commerciales contenues dans le référentiel.
seo-description: The AEM generic solution provides methods of managing the commerce information held within the repository.
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
docset: aem65
exl-id: c29f6213-1df6-45af-91c8-14b255276d82
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '2979'
ht-degree: 43%

---

# Administration d’eCommerce générique {#administering-generic-ecommerce}

La solution AEM générique fournit des méthodes pour gérer les informations commerciales conservées dans le référentiel (plutôt que d’utiliser un moteur d’e-commerce externe). Cela inclut les éléments suivants :

* [Produits](/help/commerce/cif-classic/administering/concepts.md#products)
* [Variantes de produit](/help/commerce/cif-classic/administering/concepts.md#product-variants)
* [Catalogue(s)](/help/commerce/cif-classic/administering/concepts.md#catalogs)
* [Promotions](/help/commerce/cif-classic/administering/concepts.md#promotions)
* [Bons](/help/commerce/cif-classic/administering/concepts.md#vouchers)
* [Commandes](/help/commerce/cif-classic/administering/concepts.md#shopping-cart-and-orders)
* [Pages de proxy](/help/commerce/cif-classic/administering/concepts.md#proxy-pages)

>[!NOTE]
>
>L’installation d’AEM standard comprend la mise en oeuvre générique d’AEM eCommerce (JCR).
>
>Il est actuellement prévu à des fins de démonstration ou comme base d’une implémentation personnalisée selon vos besoins.

## Produits et variations de produits {#products-and-product-variations}

>[!NOTE]
>
>Les procédures suivantes s’appliquent aux produits et aux variations de produits.

Avant de créer des produits, vous devez définir un [modèle](/help/sites-authoring/scaffolding.md) ou scaffolding. Cela indique les champs dont vous avez besoin pour définir les produits et la manière dont ils sont édités.

Un modèle est nécessaire pour chaque type de produit distinct. L’échafaudage approprié est associé aux produits en effectuant l’une des opérations suivantes :

* le chemin
* ou le produit peut référencer le modèle.

>[!NOTE]
>
>Le magasin Geometrixx-Outdoors dispose d’un type de produit unique (et par conséquent d’un modèle simple) :
>
>`/etc/scaffolding/geometrixx-outdoors`
>
>Le type de produit Geometrixx-Outdoors est actif sur :
>
>`/etc/commerce/products/geometrixx-outdoors`
>
>Vous pouvez créer une définition de produit n’importe où en dessous sans configuration supplémentaire.

### Importation de produits {#importing-products}

#### Importation de produits - IU optimisée pour les écrans tactiles {#importing-products-touch-optimized-ui}

1. Accédez à la console **Produits** via **Commerce**.
1. En utilisant la variable **Produits** accédez à l’emplacement requis dans la console.
1. Utilisez la variable **Importer des produits** pour ouvrir l’assistant.

   ![Icône Importer des produits](/help/sites-administering/do-not-localize/chlimage_1-13.png)

1. Précisez les paramètres suivants :

   * **Importateur**

     L’importateur pour le [fournisseur de commerce](/help/commerce/cif-classic/administering/concepts.md#commerce-providers) spécifique, par défaut `Geometrixx`.

   * **Source**

     Le fichier que vous voulez importer. Vous pouvez utiliser le navigateur pour sélectionner un fichier.

   * **Importation incrémentielle**

     Indiquez s’il s’agit d’une importation incrémentielle (par opposition à une importation complète).

   >[!NOTE]
   >
   >L’importation incrémentielle (par l’importateur geometrixx-outdoor d’exemple) fonctionne au niveau des produits.
   >
   >Un importateur personnalisé peut être défini pour être utilisé selon vos besoins.

1. Sélectionner **Suivant** pour importer les produits, un journal des actions effectuées s’affiche.

   >[!NOTE]
   >
   >Les produits seront importés vers la position actuelle ou par rapport à celle-ci.

   >[!NOTE]
   >
   >L’utilisation répétée de **Suivant** et **Retour** permet d’importer les définitions de produits de manière répétée. Cependant, dans la mesure où ils ont les mêmes SKU, les informations figurant dans le référentiel sont simplement remplacées.

1. Sélectionner **Terminé** pour fermer l’assistant.

#### Importation de produits - IU classique {#importing-products-classic-ui}

1. En utilisant la variable **Outils** ouvrez la console **Commerce** dossier.
1. Double-cliquez pour ouvrir le **Importateur de produits**:

   ![Console de l’importateur de produits](/help/sites-administering/assets/chlimage_1-22.jpeg)

1. Précisez les paramètres suivants :

   * **Nom de la boutique**

     Les produits seront importés dans :

     `/etc/commerce/products/<*store name*>/`

   * **Fournisseur de commerce**

     L’importateur de votre [fournisseur de commerce](/help/commerce/cif-classic/administering/concepts.md#commerce-providers), par défaut Geometrixx.

   * **Fichier source**

     L’emplacement dans le référentiel du fichier que vous voulez importer.

   * **Importation incrémentielle**

     Indiquez s’il s’agit d’une importation incrémentielle (par opposition à une importation complète).

1. Cliquez sur **Importer des produits**.

### Création d’informations sur le produit {#creating-product-information}

>[!NOTE]
>
>La gestion des produits standard est basique, car le jeu de produits Geometrixx-Outdoors a également été défini de manière basique. La complexité dépend du [modèle](/help/sites-authoring/scaffolding.md) ou de la génération de modèles automatique pour les produits. Par conséquent, il est possible d’effectuer des modifications plus sophistiquées avec votre propre modèle de produits.

#### Création d’informations sur le produit - IU optimisée pour les écrans tactiles {#creating-product-information-touch-optimized-ui}

1. En utilisant la variable **Produits** (via **Commerce**) accédez à l’emplacement requis.
1. Utilisez la variable **Créer** pour sélectionner (selon la structure et l&#39;emplacement) :

   * **Créer un produit**
   * **Créer une variante de produit**

   ![Icône de création en forme plus](/help/sites-administering/do-not-localize/chlimage_1-14.png)

1. Un assistant s’ouvre. Utilisez la variable **De base** et **Onglets Produit** pour saisir la variable [attributs de produit](/help/commerce/cif-classic/administering/concepts.md#product-attributes) pour le nouveau produit ou la nouvelle variante de produit.

   >[!NOTE]
   >
   >**Titre** et **SKU** sont le minimum requis pour créer un produit ou une variante.

1. Sélectionner **Créer** pour enregistrer les informations.

>[!NOTE]
>
>De nombreux produits sont proposés dans différentes couleurs et/ou différentes tailles. Vous pouvez gérer les informations sur le produit de base et les variantes de produit associées à partir de la **Produits** console.
>
>Les produits et leurs variantes sont stockés sous la forme d’une arborescence, les informations sur les produits sont dans la partie supérieure, avec les variantes sous (cette structure est appliquée par l’interface utilisateur).

### Modification des informations sur le produit {#editing-product-information}

>[!NOTE]
>
>Les images de produit dans geometrixx-outdoors sont diffusées à partir de :
>
>`/etc/commerce/products/...`
>
>Cela signifie que, par défaut, ils sont bloqués par le [dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=fr), configurez-le selon les besoins.

#### Modification des informations sur les produits - IU optimisée pour les écrans tactiles {#editing-product-information-touch-optimized-ui}

1. En utilisant la variable **Produits** (via **Commerce**) accédez aux informations sur votre produit.
1. En utilisant :

   * [les actions rapides ;](/help/sites-authoring/basic-handling.md#quick-actions)
   * [le mode de sélection.](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   Sélectionnez l’icône **Afficher les données du produit** :

   ![icône afficher les données de produit - icône d’informations](/help/sites-administering/do-not-localize/chlimage_1-15.png)

1. Les [attributs de produit](/help/commerce/cif-classic/administering/concepts.md#product-attributes) sont affichés. Utilisez **Modifier** et **Terminé** pour apporter des modifications.

### Affichage des références de produit {#showing-product-references}

#### Affichage des références de produit - IU optimisée pour les écrans tactiles {#showing-product-references-touch-optimized-ui}

1. En utilisant la variable **Produits** (via **Commerce**) accédez aux informations sur votre produit.
1. Ouvrez le rail secondaire pour Références à l’aide de l’icône :

   ![icône double flèche](/help/sites-administering/do-not-localize/chlimage_1-16.png)

1. Sélectionnez le produit requis ; le rail secondaire est mis à jour pour afficher les types de références disponibles :

   ![console produits avec les références ouvertes](/help/sites-administering/assets/chlimage_1-88.png)

1. Cliquez/appuyez sur le type de référence (par exemple, Pages de produits) pour développer la liste.
1. Sélectionnez une référence spécifique pour afficher les options suivantes :

   * Accéder à la page produits
   * Modifier la page produits

   ![Panneau de référence de la console Produits](/help/sites-administering/assets/chlimage_1-89.png)

### Rechercher des produits {#search-for-products}

1. Accédez à la console **Produits** via **Commerce**.
1. Ouvrez le rail secondaire pour Rechercher à l’aide de l’icône :

   ![icône de loupe](/help/sites-administering/do-not-localize/chlimage_1-17.png)

1. Plusieurs facettes permettent de rechercher des produits. Vous pouvez utiliser une ou plusieurs facettes dans une recherche. Les produits trouvés s’affichent :

   ![Données de produit dans la console de produits](/help/sites-administering/assets/chlimage_1-90.png)

1. Cliquez/appuyez sur un produit pour l’ouvrir. Vous pouvez également le publier ou afficher les données du produit.

#### Extension de la recherche {#extending-search}

Vous pouvez modifier une facette existante ou en ajouter de nouvelles à l’aide de CRXDE Lite :

1. Accédez à :

   `http://localhost:4502/crx/de/index.jsp#/libs/commerce/gui/content/products/aside/items/search/items/searchpanel/facets`

1. Vous pouvez par exemple modifier les tailles qui apparaissent sur la page de recherche de produits. Cliquez sur le nœud `sizegroup`.
1. Cliquez sur le nœud `items`, puis sur le nœud `propertypredicate`.
1. Vous pouvez modifier les `propertyValues`. Par exemple, vous pouvez ajouter XS ou XXL, ou supprimer une taille.
1. Cliquez sur **Enregistrer tout** et accédez à la page de recherche de produits. Vos modifications doivent apparaître.

### Plusieurs ressources {#multiple-assets}

Vous pouvez ajouter plusieurs ressources dans le composant de produit, puis spécifier la ressource qui apparaîtra sur la page de produit.

>[!NOTE]
>
>Tout ce qui est lié à plusieurs ressources est réalisé dans l’interface utilisateur optimisée pour les écrans tactiles.

#### Ajout de plusieurs ressources {#adding-multiple-assets}

1. Accédez à la console **Produits** via **Commerce**.
1. À l’aide de la console **Produits**, accédez au produit souhaité.

   >[!NOTE]
   >
   >Vous devez être au niveau du produit, et non d’une variante.

1. Appuyez ou cliquez sur l’icône **Afficher les données du produit** avec le mode de sélection ou les actions rapides.
1. Appuyez/cliquez sur l’icône Modifier .
1. Faites défiler jusqu’à **Ajouter**.

   ![Ajout d’une capture d’écran de données de produit](/help/sites-administering/assets/chlimage_1-91.png)

1. Appuyez/cliquez sur **Ajouter**. Un nouvel espace réservé de ressource s’affiche.
1. Cliquez ou appuyez sur **Modifier** pour ouvrir une boîte de dialogue qui vous permet de sélectionner une ressource.
1. Sélectionnez la ressource à ajouter.

   >[!NOTE]
   >
   >Les ressources que vous pouvez sélectionner sont les suivantes : [Ressources](/help/assets/assets.md).

1. Appuyez/cliquez sur l’icône Terminé.

Deux ressources sont désormais stockées dans votre composant de produit. Vous pouvez configurer celle qui apparaît sur la page du produit. Cela fonctionne avec un système de catégorie. Vous devez d’abord ajouter une catégorie aux ressources individuelles :

1. Appuyez ou cliquez sur **Afficher les données du produit**.
1. Saisissez une **catégorie de ressources** sous les ressources, par exemple `cat1` et `cat2`.

   >[!NOTE]
   >
   >Vous pouvez également utiliser des balises pour les catégories.

1. Appuyez/cliquez sur l’icône Terminé. Vous devez maintenant [déploiement](#rolling-out-a-catalog) vos modifications.

Désormais, vos ressources dans le composant de produit ont une catégorie. Vous pouvez paramétrer la catégorie qui s&#39;affichera à trois niveaux différents :

* [Page des produits](#product-page)
* [Catalogue](#catalog)
* [Console Produits](#products-console)

>[!NOTE]
>
>Si vous ne définissez pas de catégories, la première ressource s’affiche sur la page du produit.

Le mécanisme de sélection de l&#39;image à afficher est le suivant :

1. Vérifiez si une catégorie est définie pour la page des produits.
1. Dans le cas contraire, vérifiez si une catégorie est définie pour le catalogue.
1. Si ce n’est pas le cas, vérifiez si une catégorie est définie pour la console Produits.

>[!NOTE]
>
>Pour les niveaux Catalogue et Console Produits, vous devez déployer vos modifications pour appliquer les modifications et voir la différence sur la page du produit.

#### Page produit {#product-page}

1. Accédez à la page de votre produit.
1. **Modifier** le composant de produit.
1. Saisissez la **catégorie d’image** choisie (`cat1`, par exemple).
1. Appuyez/cliquez sur **Terminé**. La page s’actualise et la ressource appropriée doit s’afficher.

#### Catalogue  {#catalog}

1. Accédez à votre catalogue.
1. Appuyez/cliquez sur **Afficher les propriétés**.
1. Appuyez ou cliquez sur **Modifier**.
1. Appuyez ou cliquez sur l’onglet **Ressources**.
1. Saisissez les **Catégorie de ressources de produit**.
1. Appuyez/cliquez sur **Terminé**.
1. [Déploiement](#rolling-out-a-catalog) vos modifications.

#### Console Produits {#products-console}

1. À l’aide de la console **Produits**, accédez au produit souhaité.
1. Appuyez ou cliquez sur **Afficher les données du produit**.
1. Appuyez ou cliquez sur **Modifier**.
1. Saisissez un **Catégorie de ressources par défaut**.
1. Appuyez/cliquez sur **Terminé**.
1. [Déploiement](#rolling-out-a-catalog) vos modifications.

### Publication/annulation de la publication des informations sur les produits {#publishing-unpublishing-product-information}

#### Publication/annulation de la publication des informations sur les produits - IU optimisée pour les écrans tactiles {#publishing-unpublishing-product-information-touch-optimized-ui}

>[!NOTE]
>
>Souvent, les informations sur les produits sont publiées par les pages qui y font référence. Par exemple, lors de la publication de la page X qui fait référence au produit Y, AEM vous demandera si vous souhaitez également publier le produit Y.
>
>Pour les cas spéciaux, AEM prend également en charge la publication directe à partir des données de produit.

1. En utilisant la variable **Produits** (via **Commerce**) accédez aux informations sur votre produit.
1. En utilisant :

   * [les actions rapides ;](/help/sites-authoring/basic-handling.md#quick-actions)
   * [le mode de sélection.](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   Sélectionnez l’icône **Publier** ou **Dépublier** selon vos besoins :

   ![icône du monde](/help/sites-administering/do-not-localize/chlimage_1-18.png) ![icône du monde avec une croix - aucun signe](/help/sites-administering/do-not-localize/chlimage_1-19.png)

   Les informations sur les produits sont publiées, ou leur publication est annulée, le cas échéant.

<!-- Search&Promote is end of life as of September 1, 2022 ### Product Feed {#product-feed} -->

<!-- Search&Promote is end of life as of September 1, 2022 The Search&Promote integration allows you to: -->

<!-- Search&Promote is end of life as of September 1, 2022 * use the eCommerce API, independently of the underlying repository structure and commerce platform. -->
<!-- Search&Promote is end of life as of September 1, 2022 * leverage the Index Connector feature of Search&Promote to provide a product feed in XML format. -->
<!-- Search&Promote is end of life as of September 1, 2022 * leverage the Remote Control feature of Search&Promote to perform on-demand or scheduled requests of the product feed -->
<!-- Search&Promote is end of life as of September 1, 2022 * feed generation for different Search&Promote accounts, configured as cloud services configurations. -->

<!-- Search&Promote is end of life as of September 1, 2022 For more information, read [Product Feed](/help/sites-administering/product-feed.md). -->

### Gestionnaire d’événements pour les mises à jour de produit {#event-handler-for-product-updates}

Il existe un gestionnaire d’événements qui consigne un événement lorsqu’un produit est ajouté, modifié ou supprimé, et lorsqu’une page produit est ajoutée, modifiée ou supprimée. Il existe les événements OSGi suivants :

* `com/adobe/cq/commerce/pim/PRODUCT_ADDED`
* `com/adobe/cq/commerce/pim/PRODUCT_MODIFIED`
* `com/adobe/cq/commerce/pim/PRODUCT_DELETED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_ADDED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_MODIFIED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_DELETED`

Pour les événements `PRODUCT_*`, le chemin pointe sur le produit de base dans `/etc/commerce/products`. Pour les événements `PRODUCT_PAGE_*`, le chemin pointe sur le nœud `cq:Page`.

Vous pouvez les afficher au sein de la console Web dans les événements OSGi (`/system/console/events`), par exemple :

![Exemples d’événements OSGI](/help/sites-administering/do-not-localize/chlimage_1-20.png)

>[!NOTE]
>
>Lisez également la section [Gestion des événements dans AEM](https://blogs.adobe.com/experiencedelivers/experience-management/event_handling_incq/).

### Image avec les liens Ajouter au panier {#image-with-add-to-cart-links}

Le composant Image avec liens Ajouter au panier vous permet d’ajouter rapidement un produit au panier en créant une zone réactive liée à un produit sur une image.

Cliquer sur la zone réactive ouvre une boîte de dialogue qui vous permet de choisir la taille et la quantité du produit.

1. Accédez à la page où vous souhaitez ajouter le composant.
1. Faites glisser et déposez le composant dans la page.
1. Faites glisser et déposez une image dans le composant à partir du [navigateur de ressources](/help/sites-authoring/author-environment-tools.md#assets-browser).
1. Vous pouvez effectuer l’une des actions suivantes :

   * cliquer sur le composant, puis cliquer sur l’icône Modifier ;
   * double-clic lent

1. Cliquez sur l’icône en plein écran.

   ![icône plein écran](/help/sites-administering/assets/chlimage_1-92.png)

1. Cliquez sur l’icône Lancer une Map.

   ![icône de plan de lancement](/help/sites-administering/assets/chlimage_1-93.png)

1. Cliquez sur l’une des icônes de forme.

   ![icônes de forme](/help/sites-administering/do-not-localize/chlimage_1-21.png)

1. Modifiez et déplacez la forme selon vos besoins.
1. Cliquez sur la forme.
1. Cliquez sur l’icône Parcourir pour ouvrir la [Sélecteur de ressources](/help/assets/search-assets.md#assetpicker).

   >[!NOTE]
   >
   >Vous pouvez également saisir directement le chemin du produit qui doit se trouver au niveau du produit, et non au niveau de la variante.

   ![chemin du type](/help/sites-administering/assets/chlimage_1-94.png)

1. Cliquez deux fois sur l’icône de confirmation, puis cliquez sur Quitter le mode plein écran.
1. Cliquez quelque part sur la page en regard du composant. La page doit s’actualiser et le symbole suivant doit s’afficher sur votre image :

   ![symbole plus](/help/sites-administering/do-not-localize/chlimage_1-22.png)

1. Basculer vers [aperçu](/help/sites-authoring/editing-content.md#previewingpagestouchoptimizedui) mode .
1. Cliquez sur la zone sensible +. La boîte de dialogue qui s’ouvre vous permet de choisir la taille et la quantité du produit que vous avez saisi dans **Chemin**.

   ![exemple de produit : poncho](/help/sites-administering/assets/chlimage_1-95.png)

1. Saisissez une taille et une quantité.
1. Cliquez sur le bouton Ajouter au panier. La boîte de dialogue se ferme.
1. Accédez à votre panier. Le produit devrait être là.

#### Options de configuration {#configuration-options}

Vous pouvez configurer l’aspect de la boîte de dialogue lorsque vous cliquez sur la zone réactive :

1. Cliquez sur le composant, puis sur l’icône de configuration.

   ![icône de configuration](/help/sites-administering/assets/chlimage_1-96.png)

1. Faites défiler l’écran vers le bas. Il existe une **AJOUTER AU PANIER** .

   ![onglet ajouter au panier](/help/sites-administering/assets/chlimage_1-97.png)

1. Cliquez sur **AJOUTER AU PANIER**. Vous pouvez utiliser 3 options de configuration.

   ![options de configuration](/help/sites-administering/assets/chlimage_1-98.png)

1. Cliquez sur l’icône Terminé .

## Catalogues {#catalogs}

### Génération d’un catalogue {#generating-a-catalog}

#### Génération d’un catalogue - IU optimisée pour les écrans tactiles {#generating-a-catalog-touch-optimized-ui}

>[!NOTE]
>
>Le catalogue référence vos données de produits.

Pour générer un catalogue :

1. Ouvrez la console Sites (par exemple, [http://localhost:4502/sites.html/content](http://localhost:4502/sites.html/content)).
1. Accédez à l’emplacement où créer la page.
1. Pour ouvrir la liste des options, utilisez l’icône **Créer** :

   ![create-icon](/help/sites-administering/do-not-localize/chlimage_1-23.png)

1. Dans la liste, sélectionnez **Créer un catalogue** pour ouvrir l’assistant de création de catalogue.

   ![assistant de création de catalogue](/help/sites-administering/assets/chlimage_1-99.png)

1. Accédez au plan directeur de catalogue requis.
1. Appuyez/cliquez sur **Sélectionner** et appuyez/cliquez sur le plan directeur de catalogue requis.
1. Appuyez/cliquez sur **Suivant**.

   ![assistant de propriétés de catalogue](/help/sites-administering/assets/chlimage_1-100.png)

1. Saisissez un **titre** et un **nom**.
1. Appuyez/cliquez sur le bouton **Créer**. Le catalogue est créé et une boîte de dialogue s’ouvre.

   ![boîte de dialogue créée par le catalogue](/help/sites-administering/assets/chlimage_1-101.png)

1. Appuyez/cliquez sur le bouton **Terminé** pour revenir à la console Sites où vous pouvez voir votre catalogue.

   Appuyez/cliquez sur le bouton **Ouvrir le catalogue** pour ouvrir votre catalogue (par exemple, `http://localhost:4502/editor.html/content/test-catalog.html`).

#### Génération d’un catalogue - IU classique {#generating-a-catalog-classic-ui}

>[!NOTE]
>
>Le catalogue fera référence à votre [Données de produit](#products-and-product-variants).

1. En utilisant la variable **Sites web** , accédez à la **Plan directeur du catalogue**, puis le catalogue de base.

   Par exemple :

   `http://localhost:4502/siteadmin#/content/catalogs/geometrixx-outdoors/base-catalog`

1. Créez une page à l’aide du modèle **Plan directeur de section**.

   Par exemple, `Swimwear`.

1. Ouvrez la nouvelle page `Swimwear`, puis cliquez sur **Modifier le plan directeur** pour ouvrir la boîte de dialogue **Propriétés** dans laquelle vous pouvez configurer la sélection des **Produits**.

   Par exemple, ouvrez le **Balises/Mots-clés** pour sélectionner Activité, puis Nager dans la section Geometrixx extérieure.

1. Cliquez sur **OK** pour enregistrer vos propriétés ; Les exemples de produits s’affichent sous **Critères de sélection de produits** sur la page de plan directeur.
1. Cliquez sur **Déployer les modifications...**, sélectionnez **Déployer la page et toutes les sous-pages**, puis cliquez sur **Suivant** then **Déploiement**. Une fois le déploiement terminé, l’indicateur **Statut** devient vert.
1. Vous pouvez maintenant cliquer sur **Fermer** et vérifier la nouvelle section de catalogue, par exemple, à cette adresse et sous celle-ci :

   `http://localhost:4502/cf#/content/geometrixx-outdoors/en/swimwear.html`

1. À nouveau à partir de la page des plans directeurs, cliquez sur **Modifier le plan directeur** et, dans la boîte de dialogue **Propriétés**, ouvrez l’onglet **Page générée**. Dans le champ de liste Bannière, sélectionnez l’image que vous souhaitez afficher, par exemple, `summer.jpg`.
1. Cliquez sur **OK** pour enregistrer vos propriétés ; les informations sur la bannière s’affichent sous **Critères de sélection de produits** sur la page de plan directeur.
1. Déployez ces nouvelles modifications.

### Déploiement d’un catalogue {#rolling-out-a-catalog}

#### Déploiement d’un catalogue - IU optimisée pour les écrans tactiles {#rolling-out-a-catalog-touch-optimized-ui}

Pour déployer un catalogue :

1. Accédez à la console **Catalogues**, via **Commerce**.
1. Accédez au catalogue que vous souhaitez déployer.
1. En utilisant :

   * [les actions rapides ;](/help/sites-authoring/basic-handling.md#quick-actions)
   * [le mode de sélection.](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   Sélectionnez l’icône **Déployer les modifications** :

   ![déploiement](/help/sites-administering/do-not-localize/chlimage_1-24.png)

1. Dans l’assistant, définissez le déploiement selon les besoins, puis appuyez/cliquez sur **Déployer les modifications**.
1. Une boîte de dialogue s’ouvre. Appuyez/cliquez sur **Terminé** lorsque le processus est terminé.

#### Déploiement d’un catalogue - IU classique {#rolling-out-a-catalog-classic-ui}

Pour déployer un catalogue :

1. Accédez au catalogue à déployer. Par exemple :

   `http://localhost:4502/cf#/content/catalogs/geometrixx-outdoors/base-catalog.html`

1. Cliquez sur **Déployer les modifications...**
1. Définissez le déploiement selon vos besoins.
1. Cliquez sur **Déploiement**.

### Importateur de plan directeur {#blueprint-importer}

#### Importateur de plans directeurs - IU optimisée pour les écrans tactiles {#blueprint-importer-touch-optimized-ui}

1. Accédez à la console **Catalogues**, via **Commerce**.
1. Accédez à l’emplacement où vous souhaitez importer le plan directeur du catalogue.
1. Appuyez/cliquez sur le bouton **Importer les plans directeurs** icône .

   ![Icône Importer les plans directeurs](/help/sites-administering/do-not-localize/chlimage_1-13.png)

1. Dans l’assistant, sélectionnez la source selon les besoins, puis appuyez/cliquez sur **Suivant**.

   ![assistant de plan directeur](/help/sites-administering/assets/chlimage_1-102.png)

1. Appuyez/cliquez sur **Terminé** une fois l’importation terminée.

#### Importateur de plans directeurs - IU classique {#blueprint-importer-classic-ui}

1. À l’aide de la console **Outils**, accédez à **Commerce**.

   Par exemple :

   `http://localhost:4502/miscadmin#/etc/commerce`

1. Ouvrez le **Importateur Blueprint de catalogue**.
1. Définissez l’importation selon vos besoins.
1. Cliquez sur **Importer les plans directeurs du catalogue**.

## Promotions {#promotions}

### Création d’une promotion {#creating-a-promotion}

#### Création d’une promotion - IU classique {#creating-a-promotion-classic-ui}

>[!NOTE]
>
>L’exemple suivant traite d’une promotion contenue directement dans une [campaign](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md), il est utilisé pour les bons.
>
>Une promotion peut également se trouver dans une [expérience](/help/sites-authoring/personalization.md) dans une campagne.
>
>Pour plus d’informations, voir [Promotions et bons](#promotions-and-vouchers).

1. Ouvrez le **Sites web** de votre instance d’auteur.
1. Dans le volet de gauche, sélectionnez les **Campagne**.
1. Cliquez sur **Nouveau**, sélectionnez la variable **Promotion** modèle, puis spécifiez une **Titre** (et **Nom** si nécessaire) pour votre nouveau bon.
1. Cliquez sur **Créer**. La nouvelle page de promotion s’affiche dans le volet droit.

1. Modifiez les **propriétés** en effectuant l’une des opérations suivantes :

   * Ouvrez la page, puis cliquez sur le bouton Modifier pour ouvrir la boîte de dialogue Propriétés.
   * en sélectionnant la page dans la console Sites Web, puis en utilisant le menu contextuel (généralement le bouton droit de la souris) pour sélectionner **Propriétés...** et ouvrez la boîte de dialogue des propriétés.

   Spécifiez la variable **Type de promotion**, **Type de remise**, **Valeur de remise** et tous les autres champs, au besoin.

1. Cliquez sur **OK** pour enregistrer.

1. Vous pouvez maintenant activer votre promotion afin que les acheteurs puissent la voir sur l’instance de publication.

## Bons {#vouchers}

### Création d’un bon {#creating-a-voucher}

#### Création d’un bon - IU classique {#creating-a-voucher-classic-ui}

1. Ouvrez le **Sites web** de votre instance d’auteur.
1. Dans le volet de gauche, sélectionnez les **Campagne**.
1. Cliquez sur **Nouveau**, sélectionnez la variable **Bon** modèle, puis spécifiez une **Titre** (et **Nom** si nécessaire) pour votre nouveau bon.
1. Cliquez sur **Créer**. La nouvelle page de bon s’affiche dans le volet droit.

1. Ouvrez votre nouvelle page de bon avec un double-clic, puis cliquez sur **Modifier** pour configurer les informations suivant vos besoins.
1. Cliquez sur **OK** pour enregistrer.

1. Vous pouvez désormais activer votre bon, de sorte que les acheteurs puissent l’utiliser dans leur panier sur l’instance de publication.

### Suppression des bons {#removing-vouchers}

#### Suppression des bons - IU classique {#removing-vouchers-classic-ui}

Pour rendre un bon indisponible pour les clients, vous pouvez :

* Désactivez le bon : il restera disponible dans l’environnement de création afin que vous puissiez le réactiver ultérieurement.
* Supprimez-le complètement.

Les deux actions peuvent être effectuées à partir de la variable **Sites web** console.

### Modification des bons {#modifying-vouchers}

#### Modification des bons - IU classique {#modifying-vouchers-classic-ui}

Pour modifier les propriétés d’un bon ou d’une promotion, vous pouvez double-cliquer dessus sur la console **Sites web** et cliquer sur **Modifier**. Après l’avoir enregistré, vous devez l’activer afin que les modifications soient transmises aux instances de publication.

### Ajout de bons à un panier {#adding-vouchers-to-a-cart}

Pour permettre aux utilisateurs d’ajouter des bons à leurs paniers, vous pouvez utiliser le composant **Bons** intégré (catégorie Commerce). Vous devez l’ajouter sur la page où le panier est affiché (mais cela n’est pas obligatoire). Le composant Bons est simplement un formulaire dans lequel l’utilisateur peut saisir un code de bon. C’est le composant Panier qui affiche en fait la liste des bons appliqués et leur remise.

Sur le site de démonstration (Geometrixx Outdoors - anglais), vous pouvez voir le formulaire du bon sur la page du panier, sous le panier réel.

## Commandes {#orders}

>[!NOTE]
>
>Souvenez-vous que, par défaut, AEM ne dispose pas des actions requises pour les fonctionnalités standard associées aux commandes, telles que le retour de marchandises, la mise à jour de le statut des commandes, la réalisation et la génération de bons de livraison. Il s’agit principalement d’un aperçu technologique.
>
>La gestion générique des commandes dans AEM est basique ; les champs disponibles dans l’assistant dépendent du modèle ;
>`/etc/scaffolding/geometrixx-outdoors/order/jcr:content/cq:dialog`
>
>Si vous créez un modèle automatique personnalisé, vous pouvez stocker plus d’informations sur la commande.

>[!NOTE]
>
>La console Commandes expose les informations de commande du fournisseur, qui ne sont jamais publiées.
>
>Les informations sur les commandes des clients sont conservées dans les répertoires home et sont exposées par l’historique de commandes pour leur compte. Ces informations sont publiées avec le reste de leur répertoire personnel.

### Création des informations de commande {#creating-order-information}

#### Création d’informations sur la commande - IU optimisée pour les écrans tactiles {#creating-order-information-touch-optimized-ui}

1. En utilisant la variable **Commandes** accédez à l’emplacement requis dans la console.
1. Utilisez la variable **Créer** icône à sélectionner **Créer une commande**.

   ![Icône de création en forme plus](/help/sites-administering/do-not-localize/chlimage_1-14.png)

1. Un assistant s’ouvre. Utilisez les onglets **De base**, **Contenu**, **Paiement** et **Réalisation** pour saisir les [informations concernant la nouvelle commande](/help/commerce/cif-classic/administering/concepts.md#order-information).

1. Sélectionner **Créer** pour enregistrer les informations.

### Modification des informations de commande {#editing-order-information}

#### Modification des informations de commande - IU optimisée pour les écrans tactiles {#editing-order-information-touch-optimized-ui}

1. En utilisant la variable **Commandes** accédez à la commande dans la console.
1. En utilisant :

   * [les actions rapides ;](/help/sites-authoring/basic-handling.md#quick-actions)
   * [le mode de sélection.](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   Sélectionnez la **Afficher les données de commande** icon :

   ![icône d&#39;informations](/help/sites-administering/do-not-localize/chlimage_1-15.png)

1. Le [informations sur la commande](/help/commerce/cif-classic/administering/concepts.md#order-information) s’affiche. Utilisez **Modifier** et **Terminé** pour apporter des modifications.

