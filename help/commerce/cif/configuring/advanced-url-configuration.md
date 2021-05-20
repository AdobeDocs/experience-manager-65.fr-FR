---
title: Configurations d’URL avancées
description: Découvrez comment personnaliser les URL des pages de produits et de catégories. Cela permet aux implémentations d’optimiser les URL pour les moteurs de recherche et de promouvoir la découverte.
sub-product: Commerce
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
kt: 4933
thumbnail: 34350.jpg
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 91%

---

# Configurations d’URL avancées {#url}

Les [composants principaux AEM CIF](https://github.com/adobe/aem-core-cif-components) fournissent des configurations avancées pour personnaliser les URL des pages de produits et de catégories. De nombreuses mises en œuvre personnalisent ces URL à des fins d’optimisation du moteur de recherche (SEO). La vidéo suivante explique comment configurer les services et les fonctionnalités `UrlProvider` du [mappage Sling](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) pour personnaliser les URL des pages de produits et de catégories.

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## Configuration {#configuration}

Pour configurer le service `UrlProvider` en fonction des exigences SEO et des besoins, un projet doit fournir une configuration OSGI pour la configuration &quot;configuration du fournisseur d’URL CIF&quot;, puis configurer le service comme décrit ci-dessous.

>[!NOTE]
>
> Le projet de [magasin de référence Venia](https://github.com/adobe/aem-cif-guides-venia) (voir ci-dessous) comprend des exemples de configuration afin de démontrer l’utilisation d’URL personnalisées pour les pages de produits et de catégories.

### Modèle d’URL de page de produit {#product}

Ce modèle configure les URL des pages de produits avec les propriétés suivantes :

* **Modèle d’URL de produit** : définit le format des URL avec un ensemble d’espaces réservés. La valeur par défaut est `{{page}}.{{url_key}}.html#{{variant_sku}}`, qui a pour effet de générer des URL ; par exemple, `/content/venia/us/en/products/product-page.chaz-kangeroo-hoodie.html#MH01-M-Orange`, où
   * `{{page}}` a été remplacé par `/content/venia/us/en/products/product-page`
   * `{{url_key}}` a été remplacé par la propriété `url_key` de Magento du produit, ici `chaz-kangeroo-hoodie`.
   * `{{variant_sku}}` a été remplacé par la variante actuellement sélectionnée, ici `MH01-M-Orange`.
* **Emplacement de l’identifiant de produit** : définit l’emplacement de l’identifiant qui sera utilisé pour récupérer les données du produit. La valeur par défaut est `SELECTOR`, l’autre valeur possible étant `SUFFIX`. Dans l’exemple d’URL précédent, cela signifie que l’identifiant `chaz-kangeroo-hoodie` sera utilisé pour récupérer les données du produit.
* **Type d’identifiant de produit** : définit le type de l’identifiant à utiliser lors de la récupération des données de produit. La valeur par défaut est `URL_KEY`, l’autre valeur possible étant `SKU`. Avec l’exemple d’URL précédent, cela signifie que les données de produit seront récupérées avec un filtre GraphQL Magento tel que `filter:{url_key:{eq:"chaz-kangeroo-hoodie"}}`.

### Modèle d’URL de page de liste de produits {#product-list}

Ce modèle configure les URL des pages de listes de catégories ou de produits avec les propriétés suivantes :

* **Modèle d’URL de catégorie** : définit le format des URL avec un ensemble d’espaces réservés. La valeur par défaut est `{{page}}.{{id}}.html`, qui a pour effet de générer des URL ; par exemple, `/content/venia/us/en/products/category-page.3.html`, où
   * `{{page}}` a été remplacé par `/content/venia/us/en/products/category-page`
   * `{{id}}` a été remplacé par la propriété `id` de Magento de la catégorie, ici `3`.
* **Emplacement de l’identifiant de catégorie** : définit l’emplacement de l’identifiant qui sera utilisé pour récupérer les données du produit. La valeur par défaut est `SELECTOR`, l’autre valeur possible étant `SUFFIX`. Dans l’exemple d’URL précédent, cela signifie que l’identifiant `3` sera utilisé pour récupérer les données du produit.
* **Type d’identifiant de catégorie** : définit le type de l’identifiant à utiliser lors de la récupération des données de produit. La valeur par défaut et actuellement la seule valeur prise en charge est `ID`. Avec l’exemple d’URL précédent, cela signifie que les données de catégorie seront récupérées avec un filtre GraphQL Magento tel que `category(id:3)`.

Il est possible d’ajouter des propriétés personnalisées pour chaque modèle, à condition que les données correspondantes soient définies par les composants qui utilisent le `UrlProvider`. Vérifiez par exemple le code de la classe `ProductListItemImpl` pour savoir comment cela est mis en œuvre.

Il est également possible de remplacer le service `UrlProvider` par un service OSGi entièrement personnalisé. Dans ce cas, vous devez mettre en œuvre l’interface `UrlProvider` et l’enregistrer avec un rang de service supérieur afin de remplacer la mise en œuvre par défaut.

## Combinaison avec des mappages Sling {#sling-mapping}

En plus du `UrlProvider`, il est également possible de configurer des [mappages Sling](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) afin de réécrire et de traiter les URL. Le projet AEM Archetype fournit également [un exemple de configuration](https://github.com/adobe/aem-cif-project-archetype/tree/master/src/main/archetype/samplecontent/src/main/content/jcr_root/etc/map.publish) afin de configurer des mappages Sling pour le port 4503 (publication) et 80 (Dispatcher).

## Combinaison avec AEM Dispatcher {#dispatcher}

Les réécritures d’URL peuvent également être archivées en utilisant le serveur HTTP AEM Dispatcher avec le module `mod_rewrite`. L’[archétype de projet AEM](https://github.com/adobe/aem-project-archetype) fournit une configuration de Dispatcher AEM de référence qui inclut déjà des [règles de réécriture](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/dispatcher.cloud) de base pour la taille générée.

## Exemple

Le projet de [magasin de référence Venia](https://github.com/adobe/aem-cif-guides-venia) comprend des exemples de configuration afin de démontrer l’utilisation d’URL personnalisées pour les pages de produits et de catégories. Cela permet à chaque projet de configurer des modèles d’URL individuels pour les pages de produits et de catégories en fonction de leurs besoins SEO. Une combinaison de mappages `UrlProvider` et Sling CIF telle que décrite ci-dessus est utilisée.

>[!NOTE]
>
>Cette configuration doit être ajustée avec le domaine externe utilisé par le projet. Les mappages Sling fonctionnent en fonction du nom d’hôte et du domaine. Par conséquent, cette configuration est désactivée par défaut et doit être activée avant le déploiement. Pour ce faire, renommez le dossier `hostname.adobeaemcloud.com` de mappage Sling dans `ui.content/src/main/content/jcr_root/etc/map.publish/https` en fonction du nom de domaine utilisé et activez cette configuration en ajoutant `resource.resolver.map.location="/etc/map.publish"` à la configuration `JcrResourceResolver` du projet.

## Ressources supplémentaires

* [Magasin de référence Venia](https://github.com/adobe/aem-cif-guides-venia)
* [Mappage des ressources AEM](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/resource-mapping.html)
* [Mappages Sling](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
