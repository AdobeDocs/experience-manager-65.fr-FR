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
exl-id: 0125021a-1c00-4ea3-b7fb-1533b7b9f4f2
source-git-commit: a5f3e33a6abe7ac1bbd610a8528fd599d1ffd2aa
workflow-type: ht
source-wordcount: '0'
ht-degree: 100%

---

# Configurations d’URL avancées {#url}

>[!NOTE]
>
>L’optimisation pour les moteurs de recherche est devenue une préoccupation essentielle pour de nombreux spécialistes du marketing. En conséquence, les questions d’optimisation pour les moteurs de recherche doivent être traitées pour de nombreux projets AEM. Consultez les [Bonnes pratiques de gestion des URL et de l’optimisation pour les moteurs de recherche](https://experienceleague.adobe.com/docs/experience-manager-65/managing/managing-further-reference/seo-and-url-management.html?lang=fr) pour plus d’informations.

Les [composants principaux AEM CIF](https://github.com/adobe/aem-core-cif-components) offrent des configurations avancées pour personnaliser les URL des pages de produits et de catégories. De nombreuses mises en œuvre personnalisent ces URL à des fins d’optimisation pour les moteurs de recherche (SEO). La vidéo suivante explique comment configurer le `UrlProvider` service et les fonctionnalités du [mappage Sling](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) pour personnaliser les URL des pages de produits et de catégories.

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## Configuration {#configuration}

Pour configurer le service `UrlProvider` en fonction des exigences SEO et des besoins, un projet doit fournir une configuration OSGI pour la « configuration du fournisseur d’URL CIF ».

>[!NOTE]
>
>Depuis la version 2.0.0 des composants principaux CIF d’AEM, la configuration du fournisseur d’URL fournit uniquement des formats d’URL prédéfinis, au lieu des formats configurables en texte libre connus des versions 1.x. De plus, l’utilisation de sélecteurs pour transmettre des données dans des URL a été remplacée par des suffixes.

### Format d’URL de page de produits {#product}

Celui-ci configure les URL des pages de produits et prend en charge les options suivantes :

* `{{page}}.html/{{sku}}.html#{{variant_sku}}` (par défaut)
* `{{page}}.html/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{url_path}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_path}}.html#{{variant_sku}}`

Dans le cas du [magasin de référence Venia](https://github.com/adobe/aem-cif-guides-venia) :

* `{{page}}` sera remplacé par `/content/venia/us/en/products/product-page`
* `{{sku}}` sera remplacé par le SKU du produit, par exemple `VP09`
* `{{url_key}}` sera remplacé par la propriété `url_key` du produit, par exemple `lenora-crochet-shorts`
* `{{url_path}}` sera remplacé par le `url_path` du produit, par exemple `venia-bottoms/venia-pants/lenora-crochet-shorts`
* `{{variant_sku}}` sera remplacé par la variante actuellement sélectionnée, par exemple `VP09-KH-S`

Depuis que `url_path` a été déprécié, les formats d’URL de produit prédéfinis utilisent les `url_rewrites` d’un produit et choisissent celui qui contient le plus de segments de chemin comme alternative si `url_path` n’est pas disponible.

Avec les données d’exemple ci-dessus, une URL de variante de produit formatée à l’aide du format d’URL par défaut ressemblera à `/content/venia/us/en/products/product-page.html/VP09.html#VP09-KH-S`.

### Format d’URL de page de catégorie {#product-list}

Celui-ci configure les URL des pages de listes de catégories ou de produits et prend en charge les options suivantes :

* `{{page}}.html/{{url_path}}.html` (par défaut)
* `{{page}}.html/{{url_key}}.html`

Dans le cas du [magasin de référence Venia](https://github.com/adobe/aem-cif-guides-venia) :

* `{{page}}` sera remplacé par `/content/venia/us/en/products/category-page`
* `{{url_key}}` sera remplacé par la propriété `url_key` de la catégorie.
* `{{url_path}}` sera remplacé par le `url_path` de la catégorie

Avec les données d’exemple ci-dessus, une URL de page de catégorie formatée à l’aide du format d’URL par défaut ressemblera à `/content/venia/us/en/products/category-page.html/venia-bottoms/venia-pants.html`.

>[!NOTE]
> 
>`url_path` est une concaténation de `url_keys` des ancêtres d’un produit ou d’une catégorie et de `url_key` du produit ou de la catégorie séparés par une barre oblique `/`.

### Pages de catégorie/produit spécifiques {#specific-pages}

Il est possible de créer [plusieurs pages de catégories et de produits](multi-template-usage.md) pour un sous-ensemble spécifique de catégories ou de produits d’un catalogue.

L’`UrlProvider` est préconfiguré pour générer des liens profonds vers ces pages sur les instances dʼauteur. Cette fonctionnalité est utile aux rédacteurs qui parcourent un site en mode Prévisualisation, se rendent sur une page produit ou de catégorie spécifique, puis repassent en mode Édition pour modifier la page.

Dans les instances de publication, en revanche, les adresses URL des pages de catalogue doivent rester stables pour ne pas perdre les gains de classement dans les moteurs de recherche, par exemple. Pour cette raison, les instances de publication ne généreront pas de liens profonds vers des pages de catalogue spécifiques par défaut. Pour modifier ce comportement, une _Stratégie de page spécifique du fournisseur d’URL CIF_ peut être configurée pour toujours générer des adresses URL de page spécifiques.

## Formats d’URL personnalisés {#custom-url-format}

Pour fournir un format dʼURL personnalisé, un projet peut implémenter soit lʼinterface de service [`ProductUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/ProductUrlFormat.html) ou [`CategoryUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/CategoryUrlFormat.html) et enregistrer lʼimplémentation en tant que service OSGI. Ces implémentations, si elles sont disponibles, remplaceront le format configuré et prédéfini. S’il existe plusieurs implémentations enregistrées, celle qui a le rang de service supérieur remplace celle ou ceux qui ont le rang de service inférieur.

Les implémentations de format dʼURL personnalisé doivent implémenter une paire de méthodes pour créer une adresse URL à partir de paramètres donnés, et pour analyser une URL afin de renvoyer les mêmes paramètres, respectivement.

## Combinaison avec des mappages Sling {#sling-mapping}

En plus du `UrlProvider`, il est également possible de configurer des [mappages Sling](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) afin de réécrire et de traiter les URL. Le projet AEM Archetype fournit également [un exemple de configuration](https://github.com/adobe/aem-cif-project-archetype/tree/master/src/main/archetype/samplecontent/src/main/content/jcr_root/etc/map.publish) afin de configurer des mappages Sling pour le port 4503 (publication) et 80 (Dispatcher).

## Combinaison avec AEM Dispatcher {#dispatcher}

Les réécritures d’URL peuvent également être archivées en utilisant le serveur HTTP AEM Dispatcher avec le module `mod_rewrite`. L’[archétype de projet AEM](https://github.com/adobe/aem-project-archetype) fournit une configuration de Dispatcher AEM de référence qui inclut déjà des [règles de réécriture](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/dispatcher.cloud) de base pour la taille générée.

## Exemple

Le projet de [magasin de référence Venia](https://github.com/adobe/aem-cif-guides-venia) comprend des exemples de configuration afin de démontrer l’utilisation d’URL personnalisées pour les pages de produits et de catégories. Cela permet à chaque projet de configurer des modèles d’URL individuels pour les pages de produits et de catégories en fonction de leurs besoins d’optimisation de moteur de recherche. Une combinaison de mappages `UrlProvider` et Sling CIF telle que décrite ci-dessus est utilisée.

>[!NOTE]
>
>Cette configuration doit être ajustée avec le domaine externe utilisé par le projet. Les mappages Sling fonctionnent en fonction du nom d’hôte et du domaine. Par conséquent, cette configuration est désactivée par défaut et doit être activée avant le déploiement. Pour ce faire, renommez le dossier `hostname.adobeaemcloud.com` de mappage Sling dans `ui.content/src/main/content/jcr_root/etc/map.publish/https` en fonction du nom de domaine utilisé et activez cette configuration en ajoutant `resource.resolver.map.location="/etc/map.publish"` à la configuration `JcrResourceResolver` du projet.

## Ressources supplémentaires

* [Magasin de référence Venia](https://github.com/adobe/aem-cif-guides-venia)
* [Mappage des ressources AEM](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/resource-mapping.html?lang=fr)
* [Mappages Sling](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
