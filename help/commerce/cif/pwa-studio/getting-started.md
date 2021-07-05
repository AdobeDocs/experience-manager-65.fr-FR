---
title: Prise en main d’AEM Extension for PWA Studio
description: Découvrez comment déployer un projet Content and Commerce sans interface AEM avec PWA Studio.
topics: Commerce
feature: Commerce Integration Framework
thumbnail: 37843.jpg
source-git-commit: 247c521e93990df2c8026da5edd84d163d5d424b
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 1%

---


# Prise en main d’AEM Extension for PWA Studio {#getting-started-pwa}

PWA Studio s’intègre de manière transparente à Adobe Commerce par le biais de GraphQL. Il offre des options illimitées pour créer des storefronts innovants et attrayants et d’autres expériences numériques.

Les fragments de contenu sont des éléments de contenu dotés d’une structure prédéfinie qui leur permettent d’être utilisés sans interface à l’aide de GraphQL en tant qu’API dans différents formats (par exemple, JSON, Markdown) et rendus indépendamment. Les fragments de contenu incluent tous les types de données et champs requis par GraphQL pour s’assurer que votre application ne demande que les éléments disponibles et reçoit les éléments attendus. La flexibilité qu’ils offrent en termes de structure les rend parfaitement utilisables à plusieurs emplacements et sur plusieurs canaux.

La conception de la structure dont vous avez besoin est simple avec l’éditeur de modèle de fragment de contenu d’Adobe Experience Manager. Le principal défi de l’intégration des fragments de contenu Adobe Experience Manager (ou de toute autre donnée) à votre application de PWA Studio consiste à récupérer des données à partir de plusieurs points d’entrée GraphQL. En effet, PWA Studio fonctionne avec un seul point d’entrée GraphQL de Commerce Adobe prêt à l’emploi.

## Architecture {#architecture}

![Architecture sans tête PWA](/help/commerce/cif/assets/pwa-studio/PWA-Studio_Architecture.png)

## Configuration du PWA Studio {#setup-pwa}

Suivez la [documentation du PWA Studio Adobe](https://magento.github.io/pwa-studio/tutorials/) pour configurer votre application de PWA Studio.

Pour connecter PWA Studio au point d’entrée GraphQL d’AEM, vous pouvez utiliser l’extension [AEM pour PWA Studio](https://github.com/adobe/aem-pwa-studio-extensions).

1. Extraction du référentiel

1. Dans votre application de PWA Studio, ajoutez l’extension en tant que dépendance de développement.

   ```javascript
   yarn add --dev file:{path-to-extension}/extension
   ```

1. Ajoutez le wrapper Apollo Link à votre application de PWA Studio. Dans pwa-root/src/index.js, apportez les modifications suivantes :

   ```javascript
     import { linkWrapper } from '@adobe/pwa-studio-aem-cfm-blog-extension';
   
   // ...
   
   <Adapter apiBase={apiBase} apollo={{ link: linkWrapper(apolloLink) }} store={store}>
   ```

   Vous trouverez plus d’informations sur la personnalisation du client Apollo dans [linkWrapper.js](https://github.com/adobe/aem-pwa-studio-extensions/blob/master/aem-cfm-blog-extension/extension/src/linkWrapper.js).

1. Pour étendre le composant de navigation avec une entrée Blog, ajoutez les adaptions suivantes à pwa-root/local-intercept.js :

   ```javascript
   const addBlogToNavigation = require('@adobe/pwa-studio-aem-cfm-blog-extension/src/addBlogToNavigation');
   
   function localIntercept(targets) {
       addBlogToNavigation(targets);
   }    
   ```

   Vous trouverez plus d’informations sur la personnalisation du composant Navigation dans [addBlogToNavigation.js](https://github.com/adobe/aem-pwa-studio-extensions/blob/master/aem-cfm-blog-extension/extension/src/addBlogToNavigation.js) et dans la documentation [Extensibility Framework](https://magento.github.io/pwa-studio/pwa-buildpack/extensibility-framework/) de PWA Studio.

1. Le client Apollo s’attend à ce que le point d’entrée GraphQL AEM soit à <https://pwa-studio/endpoint.js>. Pour mapper le point de terminaison à cet emplacement, vous devez personnaliser la configuration UPWARD de votre application de PWA Studio :
a. Ajoutez la variable AEM_CFM_GRAPHQL à pwa-root/.env et adaptez-la pour qu’elle pointe vers votre point d’entrée GraphQL de fragments de contenu AEM.

   Exemple : AEM_CFM_GRAPHQL=<http://localhost:4503/content/graphql/global>

   b. Ajoutez un résolveur de proxy à votre configuration UPWARD. Voici un exemple de configuration UPWARD :

```json
   response:
     resolver: conditional
     when:
       - matches: request.url.pathname
         pattern: ^/endpoint.json(/|$)
         use: aemProxy
     default: veniaResponse

   aemProxy:
     resolver: proxy
     target: env.AEM_CFM_GRAPHQL
     ignoreSSLErrors: true

   status: response.status
   headers: response.headers
   body: response.body
```

## Configuration des AEM {#setup-aem}

Consultez la documentation des fragments de contenu AEM pour configurer un point d’entrée GraphQL pour votre projet AEM. De plus, dans votre projet AEM, ajoutez les configurations suivantes pour permettre à votre application PWA Studio d’accéder au point d’entrée GraphQL :

* Adobe de la stratégie de partage des ressources cross-origin Granite (com.adobe.granite.cors.impl.CORSPolicyImpl)

   Définissez la propriété allowedorigin sur le nom d’hôte complet de votre application de PWA.

   Exemple:  <https://pwa-studio-test-vflyn.local.pwadev:9366>

* Filtre de référent Apache Sling (org.apache.sling.security.impl.ReferrerFilter.cfg.json)

   Définissez la propriété allow.hosts sur le nom d’hôte de votre application de PWA.

   Exemple : pwa-studio-test-vflyn.local.pwadev

Vous trouverez des exemples complets des deux configurations ici : <https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cfm-blog-extension/aem/config/src/main/content/jcr_root/apps/blog-demo/config>.

Pour présenter le point d’entrée GraphQL, nous avons préparé quelques exemples de données et de modèles de fragments de contenu via un module de contenu. Ces composants fonctionnent bien avec les composants React fournis avec l’extension de PWA Studio.

## Utilisation {#how-to-use}

Cette extension est considérée comme un exemple d’implémentation de la connexion d’une application de PWA Studio avec AEM pour récupérer et effectuer le rendu du contenu via GraphQL.

En fonction de votre cas d’utilisation, vous souhaitez créer vos propres modèles de fragment de contenu personnalisés, qui génèrent un schéma GraphQL personnalisé qui peut ensuite être utilisé par vos propres composants React.

Les configurations de production peuvent varier sous plusieurs aspects.

* Vous pouvez disposer d’un point d’entrée GraphQL fédéré unique qui combine des données GraphQL AEM et Magento au lieu de personnaliser le client Apollo.
* Votre application de PWA Studio peut utiliser directement l’URL AEM point d’entrée GraphQL, sans proxy avec UPWARD. Le proxy peut également être déplacé vers une autre couche (par exemple, CDN).
* L’approche qui vous convient le mieux dépend également de la manière dont vous diffusez l’application de PWA Studio à l’utilisateur final.

Cette extension est fournie avec deux exemples.

### Blog {#blog}

Affichez les publications de blog en fonction de certains modèles de fragments de contenu. Il contient en outre des exemples de configuration du client Apollo pour qu’il fonctionne avec le point d’entrée GraphQL AEM et d’extension du composant de navigation dans PWA Studio. Voir [GitHub](https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cfm-blog-extension) pour plus d’informations.

### Enrichissement PDP {#pdp-enrichment}

Permet aux marketeurs d’enrichir facilement les PDP avec du contenu supplémentaire qui est géré en tant que fragments de contenu.  Voir [GitHub](https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cif-product-page-extension) pour plus d’informations.
