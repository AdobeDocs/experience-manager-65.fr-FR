---
title: Création d’un service cloud personnalisé
seo-title: Création d’un service cloud personnalisé
description: L’ensemble de services cloud par défaut peut être étendu à l’aide de types de service cloud personnalisés.
seo-description: L’ensemble de services cloud par défaut peut être étendu à l’aide de types de service cloud personnalisés.
uuid: b105a0c1-b68c-4f57-8e3b-561c8051a08e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: e48e87c6-43ca-45ba-bd6b-d74c969757cd
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 62%

---


# Création d’un service cloud personnalisé{#creating-a-custom-cloud-service}

L’ensemble de services cloud par défaut peut être étendu à l’aide de types de service cloud personnalisés. Cela vous permet d’injecter un balisage personnalisé dans la page de manière structurée. Cela s’avérera particulièrement utile pour les fournisseurs de données analytiques tiers, tels que Google Analytics, Chartbeat, etc. Les pages enfants héritent des services cloud des pages parents, avec la possibilité d’annuler l’héritage à n’importe quel niveau.

>[!NOTE]
>
>Google Analytics est utilisé comme exemple dans ce guide détaillé de création d’un service cloud. Il se peut que certains éléments ne soient pas applicables à votre scénario d’utilisation.

1. In CRXDE Lite, ceate a new node under `/apps`:

   * **Nom** : `acs`
   * **Type** : `nt:folder`

1. Create a new node under `/apps/acs`:

   * **Nom** : `analytics`
   * **Type** : `sling:Folder`

1. Create 2 new nodes under `/apps/acs/analytics`:

   * **Nom**: composants
   * **Type** : `sling:Folder`

   et

   * **Nom**: templates
   * **Type** : `sling:Folder`


1. Cliquez avec le bouton droit sur `/apps/acs/analytics/components`. Sélectionnez **Créer**, suivi de **Créer un composant**. La boîte de dialogue qui s’ouvre alors vous permet de spécifier ce qui suit :

   * **Libellé**: `googleanalyticspage`
   * **Titre**: `Google Analytics Page`
   * **Super Type**: `cq/cloudserviceconfigs/components/configpage`
   * **Groupe**: `.hidden`

1. Click **Next** twice and specify:

   * **Parents autorisés:** `acs/analytics/templates/googleanalytics`

   Click **Next** twice and click **OK**.

1. Add a property to `googleanalyticspage`:

   * **Nom:** `cq:defaultView`
   * **Valeur:** `html`

1. Create a new file named `content.jsp` under `/apps/acs/analytics/components/googleanalyticspage`, with the following content:

   ```xml
   <%@page contentType="text/html"
               pageEncoding="utf-8"%><%
   %><%@include file="/libs/foundation/global.jsp"%><div>
   
   <div>
       <h3>Google Analytics Settings</h3>
       <ul>
           <li><div class="li-bullet"><strong>accountID: </strong><br><%= xssAPI.encodeForHTML(properties.get("accountID", "")) %></div></li>
       </ul>
   </div>
   ```

1. Create a new node under `/apps/acs/analytics/components/googleanalyticspage/`:

   * **Nom** : `dialog`
   * **Type** : `cq:Dialog`
   * **Propriétés** :

      * **Nom** : `title`
      * **Type** : `String`
      * **Valeur**: `Google Analytics Config`
      * **Nom** : `xtype`
      * **Type** : `String`
      * **Valeur**: `dialog`

1. Create a new node under `/apps/acs/analytics/components/googleanalyticspage/dialog`:

   * **Nom** : `items`
   * **Type** : `cq:Widget`
   * **Propriétés** :

      * **Nom** : `xtype`
      * **Type** : `String`
      * **Valeur**: `tabpanel`

1. Create a new node under `/apps/acs/analytics/components/googleanalyticspage/dialog/items`:

   * **Nom** : `items`
   * **Type** : `cq:WidgetCollection`

1. Create a new node under `/apps/acs/analytics/components/googleanalyticspage/dialog/items/items`:

   * **Nom** : tab1
   * **Type** : `cq:Panel`
   * **Propriétés** :

      * **Nom** : `title`
      * **Type** : `String`
      * **Valeur**: `Config`

1. Create a new node under `/apps/acs/analytics/components/googleanalyticspage/dialog/items/items/tab1`:

   * **Nom** : items
   * **Type** : `nt:unstructured`
   * **Propriétés** :

      * **Nom** : `fieldLabel`
      * **Type** : String
      * **Valeur** : ID de compte

      * **Nom** : `fieldDescription`
      * **Type** : `String`
      * **Valeur**: `The account ID assigned by Google. Usually in the form UA-NNNNNN-N`

      * **Nom** : `name`
      * **Type** : `String`
      * **Valeur**: `./accountID`
      * **Nom** : `validateOnBlur`
      * **Type** : `String`
      * **Valeur**: `true`
      * **Nom** : `xtype`
      * **Type** : `String`
      * **Valeur**: `textfield`

1. Copy `/libs/cq/cloudserviceconfigs/components/configpage/body.jsp` to `/apps/acs/analytics/components/googleanalyticspage/body.jsp` and change `libs` to `apps` on line 34 and make the script reference on line 79 a fully qualified path.
1. Create a new template under `/apps/acs/analytics/templates/`:

   * avec le type **de** ressource = `acs/analytics/components/googleanalyticspage`
   * avec **Étiquette** = `googleanalytics`
   * avec **Title**= `Google Analytics Configuration`
   * avec **allowedPath** = `/etc/cloudservices/googleanalytics(/.*)?`
   * avec **allowedChildren** = `/apps/acs/analytics/templates/googleanalytics`
   * with **sling:resourceSuperType** = `cq/cloudserviceconfigs/templates/configpage` (on template node, not the jcr:content node)
   * with **cq:designPath** = `/etc/designs/cloudservices/googleanalytics` (on jcr:content)

1. Créer un nouveau composant : `/apps/acs/analytics/components/googleanalytics`.

   Ajoutez le contenu suivant à `googleanalytics.jsp` :

   ```xml
   <%@page import="org.apache.sling.api.resource.Resource,
                   org.apache.sling.api.resource.ValueMap,
                   org.apache.sling.api.resource.ResourceUtil,
                   com.day.cq.wcm.webservicesupport.Configuration,
                   com.day.cq.wcm.webservicesupport.ConfigurationManager" %>
   <%@include file="/libs/foundation/global.jsp" %><%
   
   String[] services = pageProperties.getInherited("cq:cloudserviceconfigs", new String[]{});
   ConfigurationManager cfgMgr = resource.getResourceResolver().adaptTo(ConfigurationManager.class);
   if(cfgMgr != null) {
       String accountID = null;
       Configuration cfg = cfgMgr.getConfiguration("googleanalytics", services);
       if(cfg != null) {
           accountID = cfg.get("accountID", null);
       }
   
       if(accountID != null) {
       %>
   <script type="text/javascript">
   
     var _gaq = _gaq || [];
     _gaq.push(['_setAccount', '<%= accountID %>']);
     _gaq.push(['_trackPageview']);
   
     (function() {
       var ga = document.createElement('script'); ga.type = 'text/javascript'; ga.async = true;
       ga.src = ('https:' == document.location.protocol ? 'https://ssl' : 'https://www') + '.google-analytics.com/ga.js';
       var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(ga, s);
     })();
   
   </script><%
       }
   }
   %>
   ```

   Cela devrait générer le balisage personnalisé sur la base des propriétés de configuration.

1. Navigate to `http://localhost:4502/miscadmin#/etc/cloudservices` and create a new page:

   * **Titre**: `Google Analytics`
   * **Nom** : `googleanalytics`

   Go back in CRXDE Lite, and under `/etc/cloudservices/googleanalytics`, add the following property to `jcr:content`:

   * **Nom** : `componentReference`
   * **Type** : `String`
   * **Valeur**: `acs/analytics/components/googleanalytics`


1. Navigate to the newly created Service page ( `http://localhost:4502/etc/cloudservices/googleanalytics.html`) and click the **+** to create a new config:

   * **Configuration du parent**: `/etc/cloudservices/googleanalytics`
   * **Titre:**  `My First GA Config`

   Sélectionnez **Google Analytics Configuration**, puis cliquez sur **Créer**.

1. Saisissez un **ID de compte** ; par exemple, `AA-11111111-1`. Cliquez sur **OK**.
1. Accédez à une page et ajoutez la nouvelle configuration dans les propriétés de la page, sous l’onglet **Services cloud.**
1. Le balisage personnalisé est ajouté à la page.

