---
title: Développement (générique)
seo-title: Développement (générique)
description: Le framework d’intégration inclut une couche d’intégration avec une API permettant de créer des composants AEM pour les fonctionnalités de commerce électronique
seo-description: Le framework d’intégration inclut une couche d’intégration avec une API permettant de créer des composants AEM pour les fonctionnalités de commerce électronique
uuid: 393bb28a-9744-44f4-9796-09228fcd466f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
discoiquuid: d8ee3b57-633a-425e-bf36-646f0e0bad52
translation-type: tm+mt
source-git-commit: ebf3f34af7da6b1a659ac8d8843152b97f30b652
workflow-type: tm+mt
source-wordcount: '1886'
ht-degree: 83%

---


# Développement (générique){#developing-generic}

>[!NOTE]
>
>[La documentation relative à l’API](/help/sites-developing/ecommerce.md#api-documentation) est également disponible.

La structure d’intégration comprend une couche d’intégration avec une API. Vous pouvez ainsi construire des composants AEM pour les fonctionnalités de commerce électronique (indépendant de votre moteur d’eCommerce). Il vous permet également d’utiliser la base de données interne CRX ou de connecter un système de commerce électronique et d’extraire les données de produit dans AEM.

Un certain nombre de composants AEM prêts à l’emploi sont fournis pour utiliser la couche d’intégration. Actuellement, il s’agit des composants suivants :

* Composant d’affichage de produit
* Panier
* Promotions et bons
* Catalogue et des plans directeurs
* Passage en caisse
* Rechercher

Pour la recherche, un hook d’intégration permet d’utiliser la recherche AEM, une recherche tierce (comme Search &amp; Promote) ou une combinaison de ceux-ci.

## Sélection du moteur eCommerce {#ecommerce-engine-selection}

Le framework eCommerce est compatible avec n’importe quelle solution eCommerce. Le moteur utilisé doit être identifié par AEM, même avec le moteur générique AEM :

* Les moteurs eCommerce sont des services OSGi prenant en charge l’interface `CommerceService`.

   * Les moteurs peuvent être distingués par une propriété de service `commerceProvider`.

* AEM prend en charge `Resource.adaptTo()` `CommerceService` les `Product`

   * The `adaptTo` implementation looks for a `cq:commerceProvider` property in the resource&#39;s hierarchy:

      * Si elle est trouvée, la valeur est utilisée pour filtrer la recherche de service de commerce.
      * Dans le cas contraire, le service de commerce le mieux classé est utilisé.
   * A `cq:Commerce` mixin is used so the `cq:commerceProvider` can be added to strongly-typed resources.


* La propriété `cq:commerceProvider` est également utilisée pour référencer la définition de fabrique de commerce appropriée.

   * Par exemple, une propriété `cq:commerceProvider` avec la valeur correspond à la configuration OSGi de **Day CQ Commerce Factory pour Geometrixx-Outdoors**(`com.adobe.cq.commerce.hybris.impl.GeoCommerceServiceFactory`), où le paramètre `commerceProvider` a aussi la valeur `geometrixx`geometrixx.
   * Ici d’autres propriétés peuvent être configurées (le cas échéant et selon leur disponibilité).

Dans une installation AEM standard, une implémentation spécifique est requise, par exemple :

|  |  |
|---|---|
| `cq:commerceProvider = geometrixx` | exemple geometrixx ; cela inclut des extensions minimales de l&#39;API générique |

### Exemple {#example}

```shell
/etc/commerce/products/geometrixx-outdoors
+ cq:commerceProvider = geometrixx
  + adobe-logo-shirt
    + cq:commerceType = product
    + price = 12.50
  + adobe-logo-shirt_S
    + cq:commerceType = variant
    + size = S
  + adobe-logo-shirt_XL
    + cq:commerceType = variant
    + size = XL
    + price = 14.50
```

>[!NOTE]
>
>En utilisant CRXDE Lite, vous pouvez voir comment cela est géré dans le composant de produit pour l’implémentation générique d’AEM :
>
>`/apps/geometrixx-outdoors/components/product`

### Gestion de session {#session-handling}

Session permettant de stocker des informations relatives au panier du client.

L’API **CommerceSession** :

* Possède le **panier**

   * exécute les ajouts/suppressions/etc. ;
   * effectue les divers calculs sur le panier ;

      `commerceSession.getProductPriceInfo(Product product, Predicate filter)`

* Owns persistance of the **order** data:

   `CommerceSession.getUserContext()`

* Can retrieve/update delivery details by using `updateOrder(Map<String, Object> delta)`
* Possède également la connexion du traitement des **paiements**
* Possède également la connexion d’**exécution**

### Architecture {#architecture}

#### Architecture d’un produit et de ses variantes {#architecture-of-product-and-variants}

Un produit unique peut posséder plusieurs variantes ; par exemple, il peut présenter différentes couleurs et/ou tailles. Un produit doit définir les propriétés pouvant varier que nous appelons *axes des variantes*.

Cependant, toutes les propriétés ne sont pas des axes de variante. Les variantes peuvent également avoir un impact sur d’autres propriétés. Par exemple, le prix peut dépendre de la taille. Ces propriétés ne peuvent pas être sélectionnées par l’acheteur et ne sont donc pas considérées comme des axes de variante.

Chaque produit et/ou variante est représenté par une ressource, et se voit donc mapper selon une relation 1:1 à un nœud du référentiel. Le corollaire est qu’un produit et/ou une variante spécifique peut être identifié par son chemin.

Any product resource can be represented by a `Product API`. Most calls in the product API are variation specific (although variations might inherit shared values from an ancestor), but there are also calls which list the set of variations ( `getVariantAxes()`, `getVariants()`, etc.).

>[!NOTE]
>
>In effect a variant axes is determined by whatever `Product.getVariantAxes()` returns:
>
>* pour l’implémentation générique, AEM le lit à partir d’une propriété dans les données du produit (`cq:productVariantAxes` )
>
>
Bien que les produits (en général) peuvent présenter plusieurs axes de variante, le composant de produit prêt à l’emploi n’en prend en charge que deux :
>
>1. `size`
>1. plus un

>
>   
This additional variant is selected via the `variationAxis` property of the product reference (usually `color` for Geometrixx Outdoors).

#### Références de produits et données PIM {#product-references-and-pim-data}

En général :

* Les données PIM sont situées sous `/etc`

* Product references under `/content`.

Il doit y avoir un mappage 1:1 entre les variations de produit et les nœuds de données de produit.

Les références de produit doivent également disposer d’un nœud pour chaque variation présentée, mais il n’est pas nécessaire de présenter toutes les variations. Par exemple, si un produit présente des variations S, M et L, les données du produit peuvent être les suivantes :

```shell
etc
  commerce
    products
      shirt
        shirt-s
        shirt-m
        shirt-l
```

Alors qu’un catalogue « grandes tailles » aurait uniquement :

```shell
content
  big-and-tall
    shirt
      shirt-l
```

Enfin, il n’est pas nécessaire d’utiliser les données de produits. Vous pouvez placer toutes les données de produits sous les références dans le catalogue, mais vous ne pouvez pas vraiment avoir plusieurs catalogues sans dupliquer toutes les données de produits.

**API**

#### Interface com.adobe.cq.commerce.api.Product {#com-adobe-cq-commerce-api-product-interface}

```java
public interface Product extends Adaptable {

    public String getPath();            // path to specific variation
    public String getPagePath();        // path to presentation page for all variations
    public String getSKU();             // unique ID of specific variation

    public String getTitle();           // shortcut to getProperty(TITLE)
    public String getDescription();     // shortcut to getProperty(DESCRIPTION)
    public String getImageUrl();        // shortcut to getProperty(IMAGE_URL)
    public String getThumbnailUrl();    // shortcut to getProperty(THUMBNAIL_URL)

    public <T> T getProperty(String name, Class<T> type);

    public Iterator<String> getVariantAxes();
    public boolean axisIsVariant(String axis);
    public Iterator<Product> getVariants(VariantFilter filter) throws CommerceException;
}
```

#### com.adobe.cq.commerce.api.VariantFilter  {#com-adobe-cq-commerce-api-variantfilter}

```java
/**
 * Interface for filtering variants and AxisFilter provided as common implementation
 *
 * The <code>VariantFilter</code> is used to filter variants,
 * e.g. when using {@link Product#getVariants(VariantFilter filter)}.
 */
public interface VariantFilter {
    public boolean includes(Product product);
}

/**
 * A {@link VariantFilter} for filtering variants by the given
 * axis and value. The following example returns a list of
 * variant products that have a value of <i>blue</i> on the
 * <i>color</i> axis.
 *
 * <p>
 * <code>product.getVariants(new AxisFilter("color", "blue"));</code>
 */
public class AxisFilter implements VariantFilter {

    private String axis;
    private String value;

    public AxisFilter(String axis, String value) {
        this.axis = axis;
        this.value = value;
    }

    /**
     * {@inheritDoc}
     */
    public boolean includes(Product product) {
        ValueMap values = product.adaptTo(ValueMap.class);

        if(values != null) {
            String v = values.get(axis, String.class);

            return v != null && v == value;
        }

        return false;
    }
}
```

* **Mécanisme de stockage général**

   * Les nœuds de produit sont nt:unstructured.
   * Un nœud de produit peut être soit :

      * une référence, avec les données de produits stockées ailleurs :

         * Product references contain a `productData` property, which points to the product data (typically under `/etc/commerce/products`).
         * Les données de produit sont hiérarchiques. Les attributs de produit sont hérités des ancêtres d’un nœud de données de produit.
         * Les références de produit peuvent également contenir des propriétés locales qui remplacent celles spécifiées dans leurs données de produit.
      * un produit lui-même :

         * Without a `productData` property.
         * Un nœud de produit qui contient toutes les propriétés localement (et ne contient pas de propriété productData) hérite des attributs de produit directement de ses propres ancêtres.


* **Structure de produit générique AEM**

   * Chaque variante doit avoir son propre nœud feuille.
   * L’interface du produit représente à la fois les produits et les variantes, mais le nœud du référentiel associé est spécifique.
   * Le nœud de produit décrit les attributs de produit et les axes de variante.

#### Exemple {#example-1}

```shell
+ banyan_shirt
    - cq:commerceType = product
    - cq:productAttributes = [jcr:title, jcr:description, size, price, color]
    - cq:productVariantAxes = [color, size]
    - jcr:title = Banyan Shirt
    - jcr:description = Flowery, all-cotton shirt.
    - price = 14.00
    + banyan_shirt_s
        - cq:commerceType = variant
        - size = S
        + banyan_shirt_s_red
            - cq:commerceType = variant
            - color = red
        + banyan_shirt_s_blue
            - cq:commerceType = variant
            - color = blue
    + banyan_shirt_m
        - cq:commerceType = variant
        - size = M
        + banyan_shirt_m_red
            - cq:commerceType = variant
            - color = red
        + banyan_shirt_m_blue
            - cq:commerceType = variant
            - color = blue
    + banyan_shirt_l
        - cq:commerceType = variant
        - size = L
        + banyan_shirt_l_red
            - cq:commerceType = variant
            - color = red
        + banyan_shirt_l_blue
            - cq:commerceType = variant
            - color = blue
    + banyan_shirt_xl
        - cq:commerceType = variant
        - size = XL
        - price = 18.00
```

#### Architecture du panier {#architecture-of-the-shopping-cart}

**Composants**

* Le panier est détenu par `CommerceSession:` :

   * L’API `CommerceSession` effectue l’ajout, la suppression, etc.
   * `CommerceSession` effectue également les différents calculs sur le panier.
   * `CommerceSession` applique aussi les bons et les promotions qui ont été validés avec le panier.

* Bien que n’étant pas directement associé au panier, `CommerceSession` doit également fournir des informations de prix de catalogue (puisqu’il gère les prix).

   * Les prix peuvent avoir plusieurs modificateurs :

      * Remises en fonction de la quantité.
      * Différentes devises.
      * Sujets ou non à la TVA.
   * Les modificateurs sont totalement ouverts avec l’interface suivante :

      * `int CommerceSession.getQuantityBreakpoints(Product product)`
      * `String CommerceSession.getProductPrice(Product product)`


**Stockage**

* Stockage

   * Dans le cas de l’interface AEM générique, les paniers sont stockés dans [ClientContext](/help/sites-administering/client-context.md)

**Personnalisation**

* La personnalisation doit toujours être pilotée via [ClientContext](/help/sites-administering/client-context.md).
* A ClientContext `/version/` of the cart is created in all cases:

   * Products should be added by using the `CommerceSession.addCartEntry()` method.

* Voici un exemple d’informations de panier dans le panier ClientContext :

![chlimage_1-33](assets/chlimage_1-33a.png)

#### Architecture du passage en caisse {#architecture-of-checkout}

**Données de panier et de commande**

`CommerceSession` possède trois éléments :

1. **Contenu du panier**

   Le schéma du contenu du panier est défini par l’API :

   ```java
       public void addCartEntry(Product product, int quantity);
       public void modifyCartEntry(int entryNumber, int quantity);
       public void deleteCartEntry(int entryNumber);
   ```

1. **Prix**

   Le schéma de prix est également fixé par le biais de l’API :

   ```java
       public String getCartPreTaxPrice();
       public String getCartTax();
       public String getCartTotalPrice();
       public String getOrderShipping();
       public String getOrderTotalTax();
       public String getOrderTotalPrice();
   ```

1. **Détails de la commande**

   Toutefois, les détails de la commande *ne sont pas fixés* par le biais de l’API :

   ```java
       public void updateOrderDetails(Map<String, String> orderDetails);
       public Map<String, String> getOrderDetails();
       public void submitOrder();
   ```

**Calculs des frais d’expédition**

* Les formulaires de commande doivent souvent afficher plusieurs options d’expédition (et leurs prix).
* Ils peuvent être basés sur des éléments et des détails de la commande, tels que le poids et/ou l’adresse d’expédition.
* `CommerceSession` a accès à toutes les dépendances, afin qu’il puisse être traité de manière similaire au prix du produit :

   * The `CommerceSession` owns shipping pricing.
   * Use `updateOrder(Map<String, Object> delta)` to retrieve/update delivery details.

### Définition de la recherche {#search-definition}

Suivant le modèle d’API de service standard, le projet eCommerce fournit un ensemble d’API associées à la recherche qui peut être mis en œuvre dans des moteurs de commerce individuels.

>[!NOTE]
>
>Actuellement, seul le moteur hybris implémente l’API de recherche prête à l’emploi.
>
>Cependant, l’API de recherche est générique et peut être implémentée par chaque CommerceService individuellement.
>
>Ainsi, bien que l’implémentation générique prête à l’emploi ne mette pas en œuvre cette API, vous pouvez l’étendre et ajouter la fonctionnalité de recherche.

Le projet eCommerce contient un composant de recherche par défaut, situé sous :

`/libs/commerce/components/search`

![chlimage_1-34](assets/chlimage_1-34a.png)

Il utilise l’API de recherche pour interroger le moteur de commerce sélectionné (voir [Sélection d’un moteur eCommerce](#ecommerce-engine-selection)) :

#### API de recherche {#search-api}

Plusieurs classes génériques/helper sont fournies par le projet principal :

1. `CommerceQuery`

   Sert à décrire une requête de recherche (il contient des informations sur le texte de requête, la page actuelle, le format de page, le tri et les facettes sélectionnées). Tous les services eCommerce qui mettent en œuvre l’API de recherche recevront des instances de cette classe pour effectuer la recherche. A `CommerceQuery` can be instantiated from a request object ( `HttpServletRequest`).

1. `FacetParamHelper`

    Est une classe utilitaire qui fournit une méthode statique, `toParams`, utilisée pour générer les chaînes de paramètre `GET` à partir d’une liste de facettes et d’une valeur basculée. Cela est utile du côté de l’IU, où vous devez afficher un lien hypertexte pour chaque valeur de chaque facette, de façon à ce que, lorsque l’utilisateur clique sur le lien hypertexte, la valeur correspondante soit activée (c’est-à-dire, si elle a été sélectionnée, elle est supprimée de la requête, ou ajoutée dans le cas contraire). Cela prend en charge toute la logique de gestion des facettes multiples/à valeur unique, du remplacement des valeurs, etc.

Le point d’entrée de l’API de recherche est la méthode `CommerceService#search` qui renvoie un objet `CommerceResult`. Consultez la documentation relative à l’API pour plus d’informations à ce sujet.

### Développement de promotions et de bons {#developing-promotions-and-vouchers}

* Bons :

   * Un bon est un composant basé sur une page qui est créé/modifié avec la console Sites Web et stocké sous :

      `/content/campaigns`

   * Diffusion de bons :

      * Un code de réduction (à saisir dans le panier par l’acheteur).
      * Un libellé de bon (à afficher après que le client l’a entré dans le panier).
      * Un chemin d’accès à une promotion (qui définit l’action que le bon applique).
   * Les bons n’ont pas leur propre date et heure de début et de fin, mais utilisent ceux de leurs campagnes parentes.
   * Les moteurs de commerce externes peuvent également fournir des bons. Ceux-ci nécessitent au minimum :

      * Un code promotionnel
      * An `isValid()` method
   * The **Voucher** component ( `/libs/commerce/components/voucher`) provides:

      * Un moteur de rendu pour l’administration des bons qui affiche tous les bons actuellement dans le panier.
      * Les boîtes de dialogue de modification (formulaire) pour administrer (ajouter/supprimer) les bons.
      * Les actions requises pour l’ajout/la suppression de bons dans le panier.



* Promotions :

   * Une promotion est un composant basé sur une page qui est créé/modifié avec la console Sites Web et stocké sous :

      `/content/campaigns`

   * Diffusion de promotions :

      * Une priorité
      * Un chemin de gestionnaire de promotion
   * Vous pouvez associer des promotions à une campagne pour définir leur date/heure d’activation/de désactivation.
   * Vous pouvez associer des promotions à une expérience pour définir leurs segments.
   * Les promotions qui ne sont pas liées à une expérience ne se déclenchent pas d’elles-mêmes, mais peuvent toujours être déclenchées par un bon.
   * The Promotion component ( `/libs/commerce/components/promotion`) contains:

      * des rendus et des boîtes de dialogue pour l’administration des promotions
      * des sous-composants pour le rendu et la modification de paramètres de configuration spécifiques aux gestionnaires de promotion
   * Deux gestionnaires de promotion prêts à l’emploi sont proposés :

      * `DiscountPromotionHandler` qui applique une réduction absolue ou en pourcentage à l’ensemble du panier
      * `PerfectPartnerPromotionHandler` qui applique une réduction absolue ou en pourcentage à un produit si un produit partenaire est également présent dans le panier
   * The ClientContext `SegmentMgr` resolves segments and the ClientContext `CartMgr` resolves promotions. Chaque promotion soumise à au moins un segment résolu est déclenchée.

      * Les promotions déclenchées sont renvoyées au serveur via un appel AJAX pour recalculer le montant du panier.
      * Les promotions déclenchées (et les bons ajoutés) sont également affichées dans le panneau ClientContext.




L’ajout/la suppression d’un bon d’un panier est réalisé via l’API `CommerceSession` :

```java
/**
 * Apply a voucher to this session's cart.
 *
 * @param code the voucher's code
 * @throws CommerceException
 */
public void addVoucher(String code) throws CommerceException;

/**
 * Remove a voucher that was previously added with {@link #addVoucher(String)}.
 *
 * @param code the voucher's code
 * @throws CommerceException
 */
public void removeVoucher(String code) throws CommerceException;

/**
 * Get a list of vouchers that were added to this cart via {@link #addVoucher(String)}.
 *
 * @throws CommerceException
 */
public List<Voucher> getVouchers() throws CommerceException;
```

De cette façon, `CommerceSession` est chargée de vérifier si un bon existe et s’il peut être appliqué ou non. Cela vaut pour les bons qui ne peuvent être appliqués que si une certaine condition est remplie, par exemple, lorsque le montant total du panier est supérieur à 100 euros. Si un bon ne peut être appliqué pour une raison ou une autre, la méthode `addVoucher` génère une exception. En outre, l’API `CommerceSession` est responsable de la mise à jour du(des) prix des articles dans le panier après l’ajout/la suppression d’un bon.

`Voucher` est une classe semblable à un bean qui contient des champs pour :

* Code promotionnel
* Une courte description
* Le référencement de la promotion associée indiquant le type et la valeur de la réduction

`AbstractJcrCommerceSession` (fourni) peut appliquer des bons. The vouchers returned by the class `getVouchers()` are instances of `cq:Page` containing a jcr:content node with the following properties (amongst others):

* `sling:resourceType` (Chaîne) - ceci doit être `commerce/components/voucher`

* `jcr:title` (Chaîne) - pour la description du voucher
* `code`( (Chaîne) - code promotionnel que l’utilisateur doit entrer pour appliquer ce bon
* `promotion` (chaîne) - promotion à appliquer ; par ex. `/content/campaigns/geometrixx-outdoors/article/10-bucks-off`

Les gestionnaires de promotions sont des services OSGi qui modifient le panier. Le panier prend en charge plusieurs hooks définis dans l’interface `PromotionHandler`.

```java
/**
 * Apply promotion to a cart line item. The method returns a discount
 * <code>PriceInfo</code> instance or <code>null</code> if no discount
 * was applied.
 * @param commerceSession The commerce session
 * @param promotion The configured promotion
 * @param cartEntry The cart line item
 * @return A discounted <code>PriceInfo</code> or <code>null</code>
 */
public PriceInfo applyCartEntryPromotion(CommerceSession commerceSession,
                                         Promotion promotion, CartEntry cartEntry)
    throws CommerceException;

/**
 * Apply promotion to an order. The method returns a discount
 * <code>PriceInfo</code> instance or <code>null</code> if no discount
 * was applied.
 * @param commerceSession The commerce session
 * @param promotion The configured promotion
 * @return A discounted <code>PriceInfo</code> or <code>null</code>
 */
public PriceInfo applyOrderPromotion(CommerceSession commerceSession, Promotion promotion)
    throws CommerceException;

public PriceInfo applyShippingPromotion(CommerceSession commerceSession, Promotion promotion)
    throws CommerceException;

/**
 * Allows a promotion handler to define a custom, author-oriented message for a promotion.
 * The {@link com.adobe.cq.commerce.common.promotion.PerfectPartnerPromotionHandler}, for instance,
 * uses this to list the qualifying pairs of products in the current cart.
 * @param commerceSession
 * @param promotion
 * @return A message to display
 * @throws CommerceException
 */
public String getMessage(SlingHttpServletRequest request, CommerceSession commerceSession, Promotion promotion) throws CommerceException;

/**
 * Informs the promotion handler that something under the promotions root has been edited, and the handler
 * should invalidate any caches it might be keeping.
 */
public void invalidateCaches();
```

Trois gestionnaires de promotion prêts à l’emploi sont proposés :

* `DiscountPromotionHandler` applique une réduction absolue ou en pourcentage à l’ensemble du panier
* `PerfectPartnerPromotionHandler` applique une réduction absolue ou en pourcentage à un produit si un produit partenaire est également présent dans le panier
* `FreeShippingPromotionHandler` applique la livraison gratuite

