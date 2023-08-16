---
title: Créer un service cloud personnalisé
description: Le jeu de Cloud Services par défaut peut être étendu avec les types de Cloud Service personnalisés.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 9414c77a-b180-4440-8386-e6eb4426e475
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 48%

---

# Créer un service cloud personnalisé{#creating-a-custom-cloud-service}

Le jeu de Cloud Services par défaut peut être étendu avec des types de Cloud Service personnalisés. Vous pouvez ainsi injecter des balises personnalisées dans la page de manière structurée. Il s’agit principalement d’une utilisation pour les fournisseurs d’analyses tiers, par exemple les fournisseurs Google Analytics, Chartbeat, etc. Les pages enfants héritent des Services cloud des pages parents, avec la possibilité d’annuler l’héritage à n’importe quel niveau.

>[!NOTE]
>
>Ce guide détaillé de création d’un Cloud Service est un exemple d’utilisation de Google Analytics. Tout peut ne pas s’appliquer à votre cas d’utilisation.

1. Dans CRXDE Lite, créez un noeud sous `/apps`:

   * **Nom** : `acs`
   * **Type** : `nt:folder`

1. Créez un noeud sous `/apps/acs`:

   * **Nom** : `analytics`
   * **Type** : `sling:Folder`

1. Créez deux noeuds sous `/apps/acs/analytics`:

   * **Nom** : components
   * **Type** : `sling:Folder`

   et

   * **Nom** : templates
   * **Type** : `sling:Folder`

1. Clic droit sur `/apps/acs/analytics/components`. Sélectionner **Créer...** suivie de **Créer un composant...** La boîte de dialogue qui s’ouvre vous permet d’indiquer les informations suivantes :

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

1. Créez un fichier nommé `content.jsp` under `/apps/acs/analytics/components/googleanalyticspage`, avec le contenu suivant :

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

1. Créez un noeud sous `/apps/acs/analytics/components/googleanalyticspage/`:

   * **Nom** : `dialog`
   * **Type** : `cq:Dialog`
   * **Propriétés** :

      * **Nom** : `title`
      * **Type** : `String`
      * **Valeur** : `Google Analytics Config`
      * **Nom** : `xtype`
      * **Type** : `String`
      * **Valeur** : `dialog`

1. Créez un noeud sous `/apps/acs/analytics/components/googleanalyticspage/dialog`:

   * **Nom** : `items`
   * **Type** : `cq:Widget`
   * **Propriétés** :

      * **Nom** : `xtype`
      * **Type** : `String`
      * **Valeur** : `tabpanel`

1. Créez un noeud sous `/apps/acs/analytics/components/googleanalyticspage/dialog/items`:

   * **Nom** : `items`
   * **Type** : `cq:WidgetCollection`

1. Créez un noeud sous `/apps/acs/analytics/components/googleanalyticspage/dialog/items/items`:

   * **Nom** : tab1
   * **Type** : `cq:Panel`
   * **Propriétés** :

      * **Nom** : `title`
      * **Type** : `String`
      * **Valeur** : `Config`

1. Créez un noeud sous `/apps/acs/analytics/components/googleanalyticspage/dialog/items/items/tab1`:

   * **Nom** : items
   * **Type** : `nt:unstructured`
   * **Propriétés** :

      * **Nom** : `fieldLabel`
      * **Type**: chaîne
      * **Valeur**: ID de compte

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
1. Créez un modèle sous `/apps/acs/analytics/templates/`:

   * avec comme **Type de ressource** = `acs/analytics/components/googleanalyticspage` ;
   * avec comme **Libellé** = `googleanalytics` ;
   * avec comme **Titre**= `Google Analytics Configuration` ;
   * avec comme **allowedPath** = `/etc/cloudservices/googleanalytics(/.*)?` ;
   * avec comme **allowedChildren** = `/apps/acs/analytics/templates/googleanalytics` ;
   * avec comme **sling:resourceSuperType** = `cq/cloudserviceconfigs/templates/configpage` (sur le nœud template et non sur le nœud jcr:content) ;
   * avec comme **cq:designPath** = `/etc/designs/cloudservices/googleanalytics` (sur jcr:content).

1. Créez un composant : `/apps/acs/analytics/components/googleanalytics`.

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

1. Accédez à `http://localhost:4502/miscadmin#/etc/cloudservices` et créez une page :

   * **Titre** : `Google Analytics`
   * **Nom** : `googleanalytics`

   Revenez dans CRXDE Lite et, sous `/etc/cloudservices/googleanalytics`, ajoutez la propriété suivante à `jcr:content` :

   * **Nom** : `componentReference`
   * **Type** : `String`
   * **Valeur** : `acs/analytics/components/googleanalytics`

1. Accédez à la page Service nouvellement créée ( `http://localhost:4502/etc/cloudservices/googleanalytics.html`), puis cliquez sur le bouton **+** pour créer une configuration :

   * **Configuration du parent** : `/etc/cloudservices/googleanalytics`
   * **Titre :** `My First GA Config`

   Sélectionnez **Google Analytics Configuration**, puis cliquez sur **Créer**.

1. Saisissez un **Identifiant de compte**, par exemple `AA-11111111-1`. Cliquez sur **OK**.
1. Accédez à une page et ajoutez la configuration nouvellement créée dans les propriétés de page, sous la propriété **Cloud Service** .
1. Les balises personnalisées sont ajoutées à la page.
