---
title: Développer des composants pour du contenu ciblé
seo-title: Developing for Targeted Content
description: Sujets relatifs au développement de composants à utiliser avec le ciblage de contenu
seo-description: Topics about developing components for use with content targeting
uuid: 2449347e-7e1c-427b-a5b0-561055186934
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: bff078cd-c390-4870-ad1d-192807c67ca4
docset: aem65
exl-id: 92b62532-4f79-410d-903e-d2bca6d0fd1c
source-git-commit: fb9363a39ffc9d3929a31a3a19a124b806607ef4
workflow-type: tm+mt
source-wordcount: '1275'
ht-degree: 45%

---

# Développer des composants pour du contenu ciblé{#developing-for-targeted-content}

Cette section décrit les rubriques relatives au développement de composants à utiliser avec le ciblage de contenu.

* Pour plus d’informations sur la connexion à Adobe Target, voir [Intégration à Adobe Target](/help/sites-administering/target.md).
* Pour plus d’informations sur la création de contenu ciblé, voir [Création de contenu ciblé en mode Ciblage](/help/sites-authoring/content-targeting-touch.md).

>[!NOTE]
>
>Lorsque vous ciblez un composant dans AEM auteur, le composant effectue une série d’appels côté serveur vers Adobe Target pour enregistrer la campagne, configurer des offres et récupérer des segments Adobe Target (s’ils sont configurés). Aucun appel côté serveur n’est effectué depuis la publication AEM vers Adobe Target.

## Activation du ciblage avec Adobe Target sur vos pages {#enabling-targeting-with-adobe-target-on-your-pages}

Pour utiliser, sur vos pages, des composants ciblés qui interagissent avec Adobe Target, vous devez inclure du code côté client spécifique dans l’élément &lt;head>.

### Section head {#the-head-section}

Ajoutez les deux blocs de code suivants au &lt;head> de votre page :

```xml
<!--/* Include Context Hub */-->
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

```xml
<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
```

Ce code ajoute les objets JavaScript d’analyse requis et charge les bibliothèques de services cloud associées au site web. Pour le service Target, les bibliothèques sont chargées via `/libs/cq/analytics/components/testandtarget/headlibs.jsp`.

Le jeu de bibliothèques chargé dépend du type de bibliothèque cliente cible (mbox.js ou at.js) utilisé dans la configuration de Target :

**Pour le fichier mbox.js par défaut**

```
<script type="text/javascript" src="/libs/cq/foundation/testandtarget/parameters.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/mbox.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/personalization/integrations/commons.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/util.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/init.js"></script>
```

**Pour le fichier mbox.js personnalisé**

```
<script type="text/javascript" src="/etc/cloudservices/testandtarget/<CLIENT-CODE>/_jcr_content/public/mbox.js"></script>
        <script type="text/javascript" src="/libs/cq/foundation/testandtarget/parameters.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/personalization/integrations/commons.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/util.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/init.js"></script>
```

**Pour at.js**

```
<script type="text/javascript" src="/libs/cq/foundation/testandtarget/parameters.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/atjs-integration.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/atjs.js"></script>
```

>[!NOTE]
>
>Seule la version de `at.js` fournie avec le produit est prise en charge. La version de `at.js` fournie avec le produit peut être obtenue dans le fichier `at.js` à l’emplacement :
>
>**/libs/cq/testandtarget/clientlibs/testandtarget/atjs/source/at.js**.

**Pour le type at.js personnalisé**

```
<script type="text/javascript" src="/etc/cloudservices/testandtarget/<CLIENT-CODE>/_jcr_content/public/at.js"></script>
    <script type="text/javascript" src="/libs/cq/foundation/testandtarget/parameters.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/atjs-integration.js"></script>
```

La fonctionnalité Target côté client est gérée par l’objet `CQ_Analytics.TestTarget`. Par conséquent, la page contient du code init comme dans l’exemple suivant :

```
<script type="text/javascript">
            if ( !window.CQ_Analytics ) {
                window.CQ_Analytics = {};
            }
            if ( !CQ_Analytics.TestTarget ) {
                CQ_Analytics.TestTarget = {};
            }
            CQ_Analytics.TestTarget.clientCode = 'my_client_code';
        </script>
      ...

    <div class="cloudservice testandtarget">
  <script type="text/javascript">
  CQ_Analytics.TestTarget.maxProfileParams = 11;

  if (CQ_Analytics.CCM) {
   if (CQ_Analytics.CCM.areStoresInitialized) {
    CQ_Analytics.TestTarget.registerMboxUpdateCalls();
   } else {
    CQ_Analytics.CCM.addListener("storesinitialize", function (e) {
     CQ_Analytics.TestTarget.registerMboxUpdateCalls();
    });
   }
  } else {
   // client context not there, still register calls
   CQ_Analytics.TestTarget.registerMboxUpdateCalls();
  }
  </script>
 </div>
```

Le JSP ajoute les objets JavaScript d’analyse requis et les références aux bibliothèques JavaScript côté client. Le fichier testandtarget.js contient les fonctions mbox.js. Le HTML généré par le script est similaire à l’exemple suivant :

```xml
<script type="text/javascript">
        if ( !window.CQ_Analytics ) {
            window.CQ_Analytics = {};
        }
        if ( !CQ_Analytics.TestTarget ) {
            CQ_Analytics.TestTarget = {};
        }
        CQ_Analytics.TestTarget.clientCode = 'MyClientCode';
</script>
<link rel="stylesheet" href="/etc/clientlibs/foundation/testandtarget/testandtarget.css" type="text/css">
<script type="text/javascript" src="/etc/clientlibs/foundation/testandtarget/testandtarget.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/testandtarget/init.js"></script>
```

#### Section de corps (début) {#the-body-section-start}

Ajoutez le code suivant immédiatement après la balise &lt;body> pour ajouter les fonctions ClientContext à la page :

```xml
<cq:include path="clientcontext" resourceType="cq/personalization/components/clientcontext"/>
```

#### Section de corps (fin) {#the-body-section-end}

Ajoutez le code suivant juste avant la balise &lt;/body> de fin :

```xml
<cq:include path="cloudservices" resourceType="cq/cloudserviceconfigs/components/servicecomponents"/>
```

Le script JSP de ce composant génère des appels vers l’API JavaScript Target et met en œuvre d’autres configurations requises. Le HTML généré par le script est similaire à l’exemple suivant :

```xml
<div class="servicecomponents cloudservices">
  <div class="cloudservice testandtarget">
    <script type="text/javascript">
      CQ_Analytics.TestTarget.maxProfileParams = 11;
      CQ_Analytics.CCM.addListener("storesinitialize", function(e) {
        CQ_Analytics.TestTarget.registerMboxUpdateCalls();
      });
    </script>
    <div id="cq-analytics-texthint" style="background:white; padding:0 10px; display:none;">
      <h3 class="cq-texthint-placeholder">Component clientcontext is missing or misplaced.</h3>
    </div>
    <script type="text/javascript">
      $CQ(function(){
      if( CQ_Analytics &&
          CQ_Analytics.ClientContextMgr &&
          !CQ_Analytics.ClientContextMgr.isConfigLoaded )
        {
          $CQ("#cq-analytics-texthint").show();
        }
      });
    </script>
  </div>
</div>
```

### Utilisation d’un fichier de bibliothèque Target personnalisé {#using-a-custom-target-library-file}

>[!NOTE]
>
>Si vous n’utilisez pas DTM ni un autre système marketing cible, vous pouvez utiliser des fichiers de bibliothèque cible personnalisés.

>[!NOTE]
>
>Par défaut, les mbox sont masquées. La classe mboxDefault détermine ce comportement. Le masquage des mbox permet de s’assurer que les visiteurs ne voient pas le contenu par défaut avant qu’il ne soit permuté. toutefois, le masquage des mbox a un impact sur les performances perçues.

Le fichier mbox.js par défaut qui est utilisé pour la création de mbox se trouve à l’emplacement suivant : /etc/clientlibs/foundation/testandtarget/mbox/source/mbox.js. Pour utiliser un fichier mbox.js client, ajoutez-le à la configuration cloud Target. Pour ajouter le fichier , le fichier mbox.js doit être disponible sur le système de fichiers.

Par exemple, si vous souhaitez utiliser le [service Marketing Cloud ID](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=fr), vous devez télécharger le fichier mbox.js afin qu’il contienne la valeur appropriée pour la variable `imsOrgID` qui est basée sur votre client. Cette variable est requise pour l’intégration au service Marketing Cloud ID. Pour plus d’informations, consultez les sections [Adobe Analytics comme source de création de rapports pour Adobe Target](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=fr) et [Avant l’implémentation](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/before-implement.html?lang=fr).

>[!NOTE]
>
>Si une mbox personnalisée est définie dans une configuration Target, vous devez posséder un accès en lecture à **/etc/cloudservices** sur les serveurs de publication. Sans cet accès, le chargement de fichiers mbox.js sur un site web de publication générera une erreur 404.

1. Accédez à la page **Outils** de CQ et sélectionnez ensuite **Services cloud**. ([https://localhost:4502/libs/cq/core/content/tools/cloudservices.html](https://localhost:4502/libs/cq/core/content/tools/cloudservices.html))
1. Dans l’arborescence, sélectionnez Adobe Target, puis, dans la liste des configurations, double-cliquez sur votre configuration Target.
1. Sur la page de configuration, cliquez sur Modifier.
1. Pour la propriété mbox.js personnalisée, cliquez sur Parcourir et sélectionnez le fichier.
1. Pour appliquer les modifications, saisissez le mot de passe de votre compte Adobe Target, cliquez sur Reconnecter à Target, puis cliquez sur OK lorsque la connexion est établie. Cliquez ensuite sur OK dans la boîte de dialogue Modifier le composant .

Votre configuration Target comprend un fichier mbox.js personnalisé, [le code requis dans la section head](/help/sites-developing/target.md#p-the-head-section-p) de votre page ajoute le fichier à la structure de bibliothèque cliente au lieu d’une référence à la bibliothèque testandtarget.js.

## Désactivation de la commande Target pour les composants {#disabling-the-target-command-for-components}

La plupart des composants peuvent être convertis en composants ciblés à l’aide de la commande Cible du menu contextuel.

![chlimage_1-21](assets/chlimage_1-21.png)

Pour supprimer la commande Target du menu contextuel, ajoutez la propriété suivante au noeud cq:editConfig du composant :

* Nom : cq:disableTargeting
* Type : booléen
* Valeur : True

Par exemple, pour désactiver le ciblage pour les composants de titre des pages Site de démonstration de Geometrixx, ajoutez la propriété au nœud /apps/geometrixx/components/title/cq:editConfig.

![chlimage_1-22](assets/chlimage_1-22.png)

## Envoi des informations de confirmation de commande à Adobe Target {#sending-order-confirmation-information-to-adobe-target}

>[!NOTE]
>
>Si vous n’utilisez pas la gestion dynamique des balises, vous envoyez une confirmation de commande à Adobe Target.

Pour effectuer le suivi des performances de votre site web, envoyez les informations d’achat de votre page de confirmation de commande à Adobe Target. (Voir [Création d’une mbox orderConfirmPage](https://developer.adobe.com/target/implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager/?lang=en) et [Mbox de confirmation de commande : ajoutez des paramètres personnalisés.](https://experienceleaguecommunities.adobe.com/t5/adobe-target-questions/order-confirmation-mbox-add-custom-parameters/m-p/275779)) Adobe Target reconnaît les données de mbox comme données de confirmation de commande lorsque le nom de votre mbox est `orderConfirmPage` et utilise les noms de paramètres spécifiques suivants :

* productPurchasedId : Liste des identifiants qui identifient les produits achetés.
* orderId : L’identifiant de la commande.
* orderTotal : Montant total de l’achat.

Le code de la page de HTML rendu qui crée la mbox est similaire à l’exemple suivant :

```xml
<script type="text/javascript">
     mboxCreate('orderConfirmPage',
     'productPurchasedId=product1 product2 product3',
     'orderId=order1234',
     'orderTotal=24.54');
</script>
```

Les valeurs de chaque paramètre sont différentes pour chaque commande. Par conséquent, vous avez besoin d’un composant qui génère le code en fonction des propriétés de l’achat. Le [framework d’intégration eCommerce](/help/commerce/cif-classic/administering/ecommerce.md) de CQ vous permet de réaliser une intégration dans votre catalogue de produits, et d’implémenter un panier d’achat et une page de passage en caisse.

L’exemple Geometrixx Outdoors affiche la page de confirmation suivante lorsqu’un visiteur achète des produits :

![chlimage_1-23](assets/chlimage_1-23.png)

Le code suivant du script JSP d’un composant accède aux propriétés du panier, puis imprime le code de création de la mbox.

```java
<%--

  confirmationmbox component.

--%><%
%><%@include file="/libs/foundation/global.jsp"%><%
%><%@page session="false"
          import="com.adobe.cq.commerce.api.CommerceService,
                  com.adobe.cq.commerce.api.CommerceSession,
                  com.adobe.cq.commerce.common.PriceFilter,
                  com.adobe.cq.commerce.api.Product,
                  java.util.List, java.util.Iterator"%><%

/* obtain the CommerceSession object */
CommerceService commerceservice = resource.adaptTo(CommerceService.class);
CommerceSession session = commerceservice.login(slingRequest, slingResponse);

/* obtain the cart items */
List<CommerceSession.CartEntry> entries = session.getCartEntries();
Iterator<CommerceSession.CartEntry> cartiterator = entries.iterator();

/* iterate the items and get the product IDs */
String productIDs = new String();
while(cartiterator.hasNext()){
 CommerceSession.CartEntry entry = cartiterator.next();
 productIDs = productIDs + entry.getProduct().getSKU();
    if (cartiterator.hasNext()) productIDs = productIDs + ", ";
}

/* get the cart price and orderID */
String total = session.getCartPrice(new PriceFilter("CART", "PRE_TAX"));
String orderID = session.getOrderId();

%><div class="mboxDefault"></div>
<script type="text/javascript">
     mboxCreate('orderConfirmPage',
     'productPurchasedId=<%= productIDs %>',
     'orderId=<%= orderID %>',
     'orderTotal=<%= total %>');
</script>
```

Lorsque le composant est inclus dans la page de passage en caisse de l’exemple précédent, la source de la page inclut le script suivant qui crée la mbox :

```
<div class="mboxDefault"></div>
<script type="text/javascript">

     mboxCreate('orderConfirmPage',
     'productPurchasedId=47638-S, 46587',
     'orderId=d03cb015-c30f-4bae-ab12-1d62b4d105ca',
     'orderTotal=US$677.00');

</script>
```

## Présentation du composant cible {#understanding-the-target-component}

Le composant cible permet aux auteurs de créer des mbox dynamiques à partir des composants de contenu CQ. (voir [Ciblage de contenu](/help/sites-authoring/content-targeting-touch.md)). Le composant Target se trouve à l’emplacement suivant : /libs/cq/personalization/components/target.

Le script target.jsp accède aux propriétés de la page pour déterminer le moteur de ciblage à utiliser pour le composant, puis exécute le script approprié :

* Adobe Target : /libs/cq/personalization/components/target/engine_tnt.jsp
* [Adobe Target avec AT.JS](/help/sites-administering/target.md) : /libs/cq/personalization/components/target/engine_atjs.jsp
* [Adobe Campaign](/help/sites-authoring/target-adobe-campaign.md) : /libs/cq/personalization/components/target/engine_cq_campaign.jsp
* Règles côté client/ContextHub : /libs/cq/personalization/components/target/engine_cq.jsp

### Création de mbox {#the-creation-of-mboxes}

>[!NOTE]
>
>Par défaut, les mbox sont masquées. La classe mboxDefault détermine ce comportement. Le masquage des mbox permet de s’assurer que les visiteurs ne voient pas le contenu par défaut avant qu’il ne soit permuté. toutefois, le masquage des mbox a un impact sur les performances perçues.

Lorsque Adobe Target effectue le ciblage du contenu, le script engine_tnt.jsp crée des mbox qui contiennent le contenu de l’expérience ciblée :

* Ajout d’un élément `div` avec la classe `mboxDefault`, comme l’exige l’API Adobe Target

* Ajout du contenu de la mbox (le contenu de l’expérience ciblée) dans l’élément `div`

Le JavaScript qui crée la mbox est inséré après l’élément div `mboxDefault` :

* Le nom, l’identifiant et l’emplacement de la mbox sont basés sur le chemin du référentiel du composant.
* Le script obtient les noms et les valeurs des paramètres ClientContext.
* Des appels sont effectués vers les fonctions définies par mbox.js et d’autres bibliothèques clientes pour créer des mbox.

#### Bibliothèques clientes pour le ciblage de contenu {#client-libraries-for-content-targeting}

Voici les catégories de bibliothèques clientes disponibles :

* testandtarget.mbox
* testandtarget.init
* testandtarget.util
* testandtarget.atjs
* testandtarget.atjs-integration
