---
title: Créer un service cloud personnalisé
seo-title: Creating a Custom Cloud Service
description: L’ensemble de services cloud par défaut peut être étendu à l’aide de types de service cloud personnalisés.
seo-description: The default set of Cloud Services can be extended with custom Cloud Service types
uuid: b105a0c1-b68c-4f57-8e3b-561c8051a08e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: e48e87c6-43ca-45ba-bd6b-d74c969757cd
exl-id: 9414c77a-b180-4440-8386-e6eb4426e475
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '418'
ht-degree: 100%

---

# Créer un service cloud personnalisé{#creating-a-custom-cloud-service}

L’ensemble de services cloud par défaut peut être étendu à l’aide de types de service cloud personnalisés. Cela vous permet d’injecter un balisage personnalisé dans la page de manière structurée. Cela s’avérera particulièrement utile pour les fournisseurs de données analytiques tiers, tels que Google Analytics, Chartbeat, etc. Les pages enfants héritent des Services cloud des pages parents, avec la possibilité d’annuler l’héritage à n’importe quel niveau.

>[!NOTE]
>
>Google Analytics est utilisé comme exemple dans ce guide détaillé de création d’un service cloud. Il se peut que certains éléments ne soient pas applicables à votre scénario d’utilisation.

1. Dans CRXDE Lite, créez un nœud sous `/apps` :

   * **Nom** : `acs`
   * **Type** : `nt:folder`

1. Créez un nœud sous `/apps/acs` :

   * **Nom** : `analytics`
   * **Type** : `sling:Folder`

1. Créez 2 nœuds sous `/apps/acs/analytics` :

   * **Nom** : components
   * **Type** : `sling:Folder`

   et

   * **Nom** : templates
   * **Type** : `sling:Folder`


1. Clic droit sur `/apps/acs/analytics/components`. Sélectionnez **Créer...**, suivi de **Créer un composant...**. La boîte de dialogue qui s’ouvre alors vous permet de spécifier ce qui suit :

   * **Libellé** : `googleanalyticspage`
   * **Titre** : `Google Analytics Page`
   * **Super Type** : `cq/cloudserviceconfigs/components/configpage`
   * **Groupe** : `.hidden`

1. Cliquez deux fois sur **Suivant** et indiquez :

   * **Parents autorisés :** `acs/analytics/templates/googleanalytics`

   Cliquez deux fois sur **Suivant**, puis cliquez sur **OK**.

1. Ajoutez une propriété à `googleanalyticspage` :

   * **Nom :** `cq:defaultView`
   * **Valeur :** `html`

1. Créez un fichier nommé `content.jsp` sous `/apps/acs/analytics/components/googleanalyticspage`, avec le contenu suivant :

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

1. Créez un nœud sous `/apps/acs/analytics/components/googleanalyticspage/` :

   * **Nom** : `dialog`
   * **Type** : `cq:Dialog`
   * **Propriétés** :

      * **Nom** : `title`
      * **Type** : `String`
      * **Valeur** : `Google Analytics Config`
      * **Nom** : `xtype`
      * **Type** : `String`
      * **Valeur** : `dialog`

1. Créez un nœud sous `/apps/acs/analytics/components/googleanalyticspage/dialog` :

   * **Nom** : `items`
   * **Type** : `cq:Widget`
   * **Propriétés** :

      * **Nom** : `xtype`
      * **Type** : `String`
      * **Valeur** : `tabpanel`

1. Créez un nœud sous `/apps/acs/analytics/components/googleanalyticspage/dialog/items` :

   * **Nom** : `items`
   * **Type** : `cq:WidgetCollection`

1. Créez un nœud sous `/apps/acs/analytics/components/googleanalyticspage/dialog/items/items` :

   * **Nom** : tab1
   * **Type** : `cq:Panel`
   * **Propriétés** :

      * **Nom** : `title`
      * **Type** : `String`
      * **Valeur** : `Config`

1. Créez un nœud sous `/apps/acs/analytics/components/googleanalyticspage/dialog/items/items/tab1` :

   * **Nom** : items
   * **Type** : `nt:unstructured`
   * **Propriétés** :

      * **Nom** : `fieldLabel`
      * **Type** : String
      * **Valeur** : ID de compte

      * **Nom** : `fieldDescription`
      * **Type** : `String`
      * **Valeur** : `The account ID assigned by Google. Usually in the form UA-NNNNNN-N`

      * **Nom** : `name`
      * **Type** : `String`
      * **Valeur** : `./accountID`
      * **Nom** : `validateOnBlur`
      * **Type** : `String`
      * **Valeur** : `true`
      * **Nom** : `xtype`
      * **Type** : `String`
      * **Valeur** : `textfield`

1. Copiez `/libs/cq/cloudserviceconfigs/components/configpage/body.jsp` sur `/apps/acs/analytics/components/googleanalyticspage/body.jsp`, remplacez `libs` par `apps` à la ligne 34 et faites de la référence de script à la ligne 79 un chemin d’accès entièrement qualifié.
1. Créez un modèle sous `/apps/acs/analytics/templates/` :

   * avec comme **Type de ressource** = `acs/analytics/components/googleanalyticspage` ;
   * avec comme **Libellé** = `googleanalytics` ;
   * avec comme **Titre**= `Google Analytics Configuration` ;
   * avec comme **allowedPath** = `/etc/cloudservices/googleanalytics(/.*)?` ;
   * avec comme **allowedChildren** = `/apps/acs/analytics/templates/googleanalytics` ;
   * avec comme **sling:resourceSuperType** = `cq/cloudserviceconfigs/templates/configpage` (sur le nœud template et non sur le nœud jcr:content) ;
   * avec comme **cq:designPath** = `/etc/designs/cloudservices/googleanalytics` (sur jcr:content).

1. Créez un composant : `/apps/acs/analytics/components/googleanalytics`.

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

1. Accédez à `http://localhost:4502/miscadmin#/etc/cloudservices` et créez une page :

   * **Titre** : `Google Analytics`
   * **Nom** : `googleanalytics`

   Revenez dans CRXDE Lite et, sous `/etc/cloudservices/googleanalytics`, ajoutez la propriété suivante à `jcr:content` :

   * **Nom** : `componentReference`
   * **Type** : `String`
   * **Valeur** : `acs/analytics/components/googleanalytics`


1. Accédez à la page Service qui vient d’être créée (`http://localhost:4502/etc/cloudservices/googleanalytics.html`) et cliquez ensuite sur le signe **+** pour créer une configuration :

   * **Configuration du parent** : `/etc/cloudservices/googleanalytics`
   * **Titre :** `My First GA Config`

   Sélectionnez **Google Analytics Configuration**, puis cliquez sur **Créer**.

1. Saisissez un **ID de compte** ; par exemple, `AA-11111111-1`. Cliquez sur **OK**.
1. Accédez à une page et ajoutez la nouvelle configuration dans les propriétés de la page, sous l’onglet **Services cloud.**
1. Le balisage personnalisé est ajouté à la page.
