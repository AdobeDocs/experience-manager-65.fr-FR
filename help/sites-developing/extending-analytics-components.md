---
title: Ajout d’un suivi Adobe Analytics aux composants
description: Ajout d’un suivi Adobe Analytics aux composants
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: e6c1258c-81d5-48e4-bdf1-90d7cc13a22d
source-git-commit: 260f71acd330167572d817fdf145a018b09cbc65
workflow-type: tm+mt
source-wordcount: '1266'
ht-degree: 91%

---

# Ajout d’un suivi Adobe Analytics aux composants{#adding-adobe-analytics-tracking-to-components}

## Inclusion du module Adobe Analytics dans un composant de page {#including-the-adobe-analytics-module-in-a-page-component}

Les composants de modèle de page (par exemple, `head.jsp, body.jsp`) ont besoin d’inclusions JSP pour charger l’intégration de ContextHub et d’Adobe Analytics (dans le cadre des services cloud). Ils incluent tous le chargement de fichiers JavaScript.

L’entrée ContextHub doit être incluse immédiatement sous la balise `<head>`, tandis que les Services cloud doivent être inclus dans le `<head>` et avant la section `</body>` ; par exemple :

```xml
<head>
   <sling:include path="contexthub" resourceType="granite/contexthub/components/contexthub" />
...
   <cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
...
</head>
<body>
...
    <cq:include path="cloudservices" resourceType="cq/cloudserviceconfigs/components/servicecomponents"/>
</body>
```

Le script `contexthub` que vous insérez après l’élément `<head>` ajoute les fonctions de ContextHub à la page.

Les scripts `cloudservices` que vous ajoutez dans les sections `<head>` et `<body>` s’appliquent aux configurations de Cloud Services ajoutées à la page. (Si la page utilise plusieurs configurations de Cloud Services, vous ne devez inclure le jsp ContextHub et le jsp Cloud Services qu’une seule fois.)

Lorsqu’un framework Adobe Analytics est ajouté à la page, les scripts `cloudservices` génèrent du code JavaScript lié à Adobe Analytics et des références à des bibliothèques côté client, comme dans l’exemple suivant :

```xml
<div class="sitecatalyst cloudservice">
<script type="text/javascript" src="/etc/clientlibs/foundation/sitecatalyst/sitecatalyst.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/sitecatalyst/util.js"></script>
<script type="text/javascript" src="/content/geometrixx-outdoors/_jcr_content/analytics.sitecatalyst.js"></script>
<script type="text/javascript" src="/etc/clientlibs/mac/mac-sc.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/sitecatalyst/plugins.js"></script>
<script type="text/javascript">
<!--
CQ_Analytics.Sitecatalyst.frameworkComponents = ['foundation/components/page'];
/**
 * Sets Adobe Analytics variables accordingly to mapped components. If <code>options</code>
 * object is provided only variables matching the options.componentPath are set.
 *
 * @param {Object} options Parameter object from CQ_Analytics.record() call. Optional.
 */
CQ_Analytics.Sitecatalyst.updateEvars = function(options) {
    this.frameworkMappings = [];
 this.frameworkMappings.push({scVar:"pageName",cqVar:"pagedata.title",resourceType:"foundation/components/page"});
    for (var i=0; i<this.frameworkMappings.length; i++){
  var m = this.frameworkMappings[i];
  if (!options || options.compatibility || (options.componentPath == m.resourceType)) {
   CQ_Analytics.Sitecatalyst.setEvar(m);
  }
    }
}

CQ_Analytics.CCM.addListener("storesinitialize", function(e) {
 var collect = true;
    var lte = s.linkTrackEvents;
    s.pageName="content:geometrixx-outdoors:en";
    CQ_Analytics.Sitecatalyst.collect(collect);
    if (collect) {
  CQ_Analytics.Sitecatalyst.updateEvars();
     /************* DO NOT ALTER ANYTHING BELOW THIS LINE ! **************/
     var s_code=s.t();if(s_code)document.write(s_code);
     s.linkTrackEvents = lte;
     if(s.linkTrackVars.indexOf('events')==-1){delete s.events};
     $CQ(document).trigger("sitecatalystAfterCollect");
    }
});
//-->
</script>
<script type="text/javascript">
<!--
if(navigator.appVersion.indexOf('MSIE')>=0)document.write(unescape('%3C')+'\!-'+'-')
//-->
</script>
<noscript><img src="https://daydocumentation.112.2o7.net/b/ss/daydocumentation/1/H.25--NS/1380120772954?cdp=3&gn=content%3Ageometrixx-outdoors%3Aen" height="1" width="1" border="0" alt=""/></noscript>
<span data-tracking="{event:'pageView', values:{}, componentPath:'foundation/components/page'}"></span>
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
```

Ce code est inclus pour tous les exemples de sites AEM tels que les Geometrixx Outdoors.

### Événement sitecatalystAfterCollect {#the-sitecatalystaftercollect-event}

Le script `cloudservices` déclenche l’événement `sitecatalystAfterCollect` :

```
$CQ(document).trigger("sitecatalystAfterCollect");
```

Cet événement est déclenché pour indiquer que le tracking des pages est terminé. Si vous effectuez d’autres opérations de tracking sur cette page, vous devez considérer cet événement au lieu de l’événement document chargé ou document prêt. L’utilisation de l’événement `sitecatalystAfterCollect` permet d’éviter les collisions ou tout autre comportement imprévisible.

>[!NOTE]
>
>La bibliothèque `/libs/cq/analytics/clientlibs/sitecatalyst/sitecatalyst.js` comprend le code provenant du fichier `s_code.js` d’Adobe Analytics.

## Mise en œuvre du suivi Adobe Analytics pour les composants personnalisés {#implementing-adobe-analytics-tracking-for-custom-components}

Activez vos composants AEM pour interagir avec le framework Adobe Analytics. Ensuite, configurez votre framework de sorte que Adobe Analytics suive les données de composant.

Les composants qui interagissent avec le framework Adobe Analytics apparaissent dans le sidekick latéral lorsque vous modifiez un framework. Faites glisser le composant vers le framework pour faire apparaître les propriétés du composant. Vous pouvez ensuite les mapper avec des propriétés Adobe Analytics. (Voir [Configuration d’un framework pour le suivi de base](/help/sites-administering/adobeanalytics-connect.md#creating-a-adobe-analytics-framework).)

Les composants peuvent interagir avec le framework Adobe Analytics lorsqu’ils sont dotés d’un nœud enfant appelé `analytics`. Le nœud `analytics` possède les propriétés suivantes :

* `cq:trackevents` : identifie les événements CQ exposés par le composant. (Voir Événements personnalisés.)
* `cq:trackvars` : nomme les variables CQ qui sont mappées avec les propriétés Adobe Analytics.
* `cq:componentName` : nom du composant qui s’affiche dans le sidekick.
* `cq:componentGroup` : groupe dans le sidekick qui comprend le composant.

Le code dans le composant JSP ajoute le code JavaScript à la page pour déclencher le tracking et définir les données qui font l’objet d’un suivi. Le nom de l’événement et les noms des données utilisés dans le code JavaScript doivent être identiques aux valeurs correspondantes des propriétés de nœud `analytics`.

* Utilisez l’attribut data-tracking pour suivre les données d’événement lors du chargement d’une page. (Voir [Tracking des événements personnalisés lors du chargement d’une page](/help/sites-developing/extending-analytics.md#tracking-custom-events-on-page-load).)
* Utilisez la fonction CQ_Analytics.record pour suivre les données d’événement lorsque les utilisateurs interagissent avec les fonctions de page. (Voir [Tracking des événements personnalisés après le chargement d’une page](/help/sites-developing/extending-analytics.md#tracking-custom-events-after-page-load).)

Lorsque vous utilisez ces méthodes de suivi des données, le module d’intégration de Adobe Analytics effectue automatiquement les appels auprès de Adobe Analytics pour enregistrer les événements et les données.

### Exemple : suivi des clics de topnav {#example-tracking-topnav-clicks}

Étendez le composant topnav de base afin que Adobe Analytics suive les clics sur les liens de navigation en haut de la page. Lorsqu’un lien de navigation fait l’objet d’un clic, Adobe Analytics enregistre le lien sur lequel l’utilisateur a cliqué, ainsi que la page sur laquelle il a cliqué.

Pour ces procédures, il est nécessaire d’avoir déjà effectué les tâches suivantes :

* Création d’une application CQ.
* Création d’une configuration Adobe Analytics et d’un framework Adobe Analytics

#### Copie du composant topnav {#copy-the-topnav-component}

Copiez le composant topnav dans votre application CQ. Il est nécessaire que votre application soit configurée dans CRXDE Lite pour la procédure.

1. Cliquez avec le bouton droit sur le nœud `/libs/foundation/components/topnav` et cliquez sur Copier.
1. Cliquez avec le bouton droit sur le dossier Composants sous votre dossier d’application, puis sélectionnez Coller.
1. Cliquez sur Enregistrer tout.

#### Intégration de topnav au framework Adobe Analytics {#integrating-topnav-with-the-adobe-analytics-framework}

Configurez le composant topnav et modifiez le fichier JSP pour définir les événements et les données de suivi.

1. Cliquez avec le bouton droit sur le nœud topnav et cliquez sur Créer > Créer un nœud. Indiquez les valeurs de propriété suivantes, puis cliquez sur OK :

   * Nom : `analytics`
   * Type : `nt:unstructured`

1. Ajoutez la propriété suivante au noeud analytics afin de pouvoir nommer l’événement de suivi :

   * Nom : cq:trackevents
   * Type : chaîne
   * Valeur : topnavClick

1. Ajoutez la propriété suivante au noeud analytics afin de pouvoir nommer les variables de données :

   * Nom : cq:trackvars
   * Type : chaîne
   * Valeur : topnavTarget,topnavLocation

1. Ajoutez la propriété suivante au nœud Analytics pour nommer le composant pour Sidekick :

   * Nom : cq:componentName
   * Type : chaîne
   * Valeur : topnav (suivi)

1. Ajoutez la propriété suivante au nœud Analytics pour nommer le groupe de composants pour Sidekick :

   * Nom : cq:componentGroup
   * Type : chaîne
   * Valeur : Général

1. Cliquez sur Enregistrer tout.
1. Ouvrez le fichier `topnav.jsp`
1. Dans l’élément , ajoutez l’attribut suivant :

   ```xml
   onclick = "tracknav('<%= child.getPath() %>.html')"
   ```

1. Au bas de la page, ajoutez le code JavaScript suivant :

   ```xml
   <script type="text/javascript">
       function tracknav(target) {
               if (CQ_Analytics.Sitecatalyst) {
                   CQ_Analytics.record({
                       event: 'topnavClick',
                       values: {
                           topnavTarget: target,
                           topnavLocation:'<%=currentPage.getPath() %>.html'
                       },
                       componentPath: '<%=resource.getResourceType()%>'
                   });
               }
       }
   </script>
   ```

1. Cliquez sur Enregistrer tout.

Le contenu du fichier `topnav.jsp` devrait se présenter comme suit :

```xml
<%@page session="false"%><%--
  Copyright 1997-2008 Day Management AG
  Barfuesserplatz 6, 4001 Basel, Switzerland
  All Rights Reserved.

  This software is the confidential and proprietary information of
  Day Management AG, ("Confidential Information"). You shall not
  disclose such Confidential Information and shall use it only in
  accordance with the terms of the license agreement you entered into
  with Day.

  ==============================================================================

  Top Navigation component

  Draws the top navigation

--%><%@include file="/libs/foundation/global.jsp"%><%
%><%@ page import="java.util.Iterator,
        com.day.text.Text,
        com.day.cq.wcm.api.PageFilter,
        com.day.cq.wcm.api.Page,
        com.day.cq.commons.Doctype,
        org.apache.commons.lang3.StringEscapeUtils" %><%

    // get starting point of navigation
    long absParent = currentStyle.get("absParent", 2L);
    String navstart = Text.getAbsoluteParent(currentPage.getPath(), (int) absParent);

    //if not deep enough take current node
    if (navstart.equals("")) navstart=currentPage.getPath();

    Resource rootRes = slingRequest.getResourceResolver().getResource(navstart);
    Page rootPage = rootRes == null ? null : rootRes.adaptTo(Page.class);
    String xs = Doctype.isXHTML(request) ? "/" : "";
    if (rootPage != null) {
        Iterator<Page> children = rootPage.listChildren(new PageFilter(request));
        while (children.hasNext()) {
            Page child = children.next();
            %><a onclick = "tracknav('<%= child.getPath() %>.html')"  href="<%= child.getPath() %>.html"><%
            %><img alt="<%= StringEscapeUtils.escapeXml(child.getTitle()) %>" src="<%= child.getPath() %>.navimage.png"<%= xs %>></a><%
        }
    }
%><script type="text/javascript">
    function tracknav(target) {
            if (CQ_Analytics.Sitecatalyst) {
                CQ_Analytics.record({
                    event: 'topnavClick',
                    values: {
                        topnavTarget:target,
                        topnavLocation:'<%=currentPage.getPath() %>.html'
                    },
                    componentPath: '<%=resource.getResourceType()%>'
                });
            }
    }
</script>
```

>[!NOTE]
>
>Il est souvent préférable de suivre les données à partir du ContextHub. Pour plus d’informations sur l’utilisation de JavaScript afin d’obtenir ces informations, voir [Accès aux valeurs dans le ContextHub](/help/sites-developing/extending-analytics.md#accessing-values-in-the-contexthub).

#### Ajout du composant de suivi au sidekick {#adding-the-tracking-component-to-sidekick}

Ajoutez au sidekick des composants permettant le suivi en utilisant Adobe Analytics afin de pouvoir les inclure dans votre framework.

1. Ouvrez votre framework Adobe Analytics à partir de votre configuration Adobe Analytics. ([http://localhost:4502/etc/cloudservices/sitecatalyst.html](http://localhost:4502/etc/cloudservices/sitecatalyst.html))
1. Sur Sidekick, cliquez sur le bouton Conception.

   ![Bouton Conception avec un carré en angle droit.](assets/chlimage_1a.png)

1. Dans la zone Configuration du suivi des liens, cliquez sur Configurer l’héritage.

   ![chlimage_1](assets/chlimage_1aa.png)

1. Dans la liste Composants autorisés, sélectionnez topnav (suivi) dans la section Général, puis cliquez sur OK.
1. Développez Sidekick pour passer en mode d’édition. Le composant est désormais disponible dans le groupe Général.

#### Ajout du composant topnav à votre framework {#adding-the-topnav-component-to-your-framework}

Faites glisser le composant topnav vers votre framework de Adobe Analytics, et mappez les événements et les variables de composants aux événements et variables d’Adobe Analytics. (Voir [Configuration d’un framework pour le suivi de base](/help/sites-administering/adobeanalytics-connect.md).)

![chlimage_1-1](assets/chlimage_1-1a.png)

Le composant topnav est désormais intégré au framework Adobe Analytics. Lorsque vous ajoutez le composant à une page, le fait de cliquer sur les éléments dans la barre de navigation supérieure entraîne l’envoi de données de suivi à Adobe Analytics.

### Envoi de données s.products à Adobe Analytics {#sending-s-products-data-to-adobe-analytics}

Les composants peuvent générer des données pour la variable s.products qui sont envoyées à Adobe Analytics. Concevez vos composants de manière à ce qu’ils contribuent à la variable s.products :

* Enregistrez une valeur nommée `product` avec une structure spécifique.
* Affichez les membres de données de la valeur `product` de façon à ce qu’ils puissent être mappés aux variables Adobe Analytics dans le framework Adobe Analytics.

La variable s.products de Adobe Analytics utilise la syntaxe suivante :

```
s.products="category;product;quantity;price;eventY={value}|eventZ={value};evarA={value}|evarB={value}"
```

Le module d’intégration Adobe Analytics construit la variable `s.products` à l’aide des valeurs `product` que les composants AEM génèrent. La valeur `product` dans le code JavaScript que génèrent les composants AEM est un tableau de valeurs avec la structure suivante :

```
"product": [{
    "category": "",
    "sku"     : "path to product node",
    "quantity": quantity,
    "price"   : price,
    "events   : {
      "eventName1": "eventValue1",
      "eventName_n": "eventValue_n"
    }
    "evars"   : {
      "eVarName1": "eVarValue1",
      "eVarName_n": "eVarValue_n"
    }
}]
```

Lorsqu’un élément de données est omis dans la valeur `product`, il est envoyé en tant que chaîne vide dans s.products.

>[!NOTE]
>
>Lorsqu’aucun événement n’est associé à une valeur de produit, Adobe Analytics utilise l’événement `prodView` par défaut.

Le nœud `analytics` du composant doit exposer les noms des variables à l’aide de la propriété `cq:trackvars` :

* product.category
* product.sku
* product.quantity
* product.price
* product.events.eventName1
* product.events.eventName_n
* product.evars.eVarName1
* product.evars.eVarName_n

Le module eCommerce fournit plusieurs composants qui génèrent des données de variable s.products. Par exemple, la variable `submitorder` component ([http://localhost:4502/crx/de/index.jsp#/libs/commerce/components/submitorder/submitorder.jsp](http://localhost:4502/crx/de/index.jsp#/libs/commerce/components/submitorder/submitorder.jsp)) génère du code JavaScript semblable à l’exemple suivant :

```
<script type="text/javascript">
    function trackCartPurchase() {
        if (CQ_Analytics.Sitecatalyst) {
            CQ_Analytics.record({
                "event": ["productsCartPurchase"],
                "values": {
                    "product": [
                        {
                            "category": "",
                            "sku"     : "/path/to/prod/1",
                            "quantity": 3,
                            "price"   : 179.7,
                            "evars"   : {
                                "childSku": "/path/to/prod/1/green/xs",
                                "size"    : "XS"
                            }
                        },
                        {
                            "category": "",
                            "sku"     : "/path/to/prod/2",
                            "quantity": 10,
                            "price"   : 150,
                            "evars"   : {
                                "childSku": "/path/to/prod/2",
                                "size"    : ""
                            }
                        },
                        {
                            "category": "",
                            "sku"     : "/path/to/prod/3",
                            "quantity": 2,
                            "price"   : 102,
                            "evars"   : {
                                "childSku": "/path/to/prod/3/m",
                                "size"    : "M"
                            }
                        }
                    ]
                },
                "componentPath": "commerce/components/submitorder"
            });
            CQ_Analytics.record({
                "event": ["discountRedemption"],
                "values": {
                    "discount": "/path/to/discount/1 - /path/to/discount/2",
                    "product" : [{
                        "category": "",
                        "sku"     : "Promotional Discount",
                        "events"  : {"discountRedemption": 20.00}
                    }]
                },
                "componentPath": "commerce/components/submitorder"
            });
            CQ_Analytics.record({
                "event": ["cartPurchase"],
                "values": {
                    "orderId"       : "00e40e2d-13a2-4a00-a8ee-01a9ebb0bf68",
                    "shippingMethod": "overnight",
                    "paymentMethod" : "Amex",
                    "billingState"  : "NY",
                    "billingZip"    : "10458",
                    "product"       : [{"category": "", "sku": "", "quantity": "", "price": ""}]
                },
                "componentPath": "commerce/components/submitorder"
            });
        }
        return true;
    }
</script>
```

#### Limitation de la taille des appels de suivi {#limiting-the-size-of-tracking-calls}

En règle générale, les navigateurs Web limitent la taille des demandes GET. Étant donné que les valeurs de SKU et de produit CQ sont des chemins de référentiel, les tableaux de produits qui incluent plusieurs valeurs peuvent dépasser la limite de taille de la requête. Par conséquent, vos composants doivent limiter le nombre d’éléments dans le tableau `product` de chaque `CQ_Analytics.record function`. Créez plusieurs fonctions si le nombre d’éléments dont vous devez effectuer le suivi peut dépasser la limite.

Par exemple, l’eCommerce `submitorder` limite le nombre de `product` éléments d’un appel à quatre. Lorsque le panier contient plus de quatre produits, il génère plusieurs fonctions `CQ_Analytics.record`.
