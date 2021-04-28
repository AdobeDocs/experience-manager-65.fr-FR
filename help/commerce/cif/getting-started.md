---
title: Prise en main du contenu et du commerce AEM
description: Découvrez comment déployer un projet AEM Content and Commerce.
topics: Commerce
feature: Commerce Integration Framework
thumbnail: 37843.jpg
translation-type: tm+mt
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 6%

---

# Prise en main de AEM Contenu et commerce {#start}

Pour commencer à utiliser AEM Content and Commerce, vous devez installer AEM Content and Commerce Ajoute-On pour AEM 6.5.

## Configuration logicielle minimale requise

[AEM 6.5 Service Pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) 7 ou version ultérieure est requis.

## Intégration {#onboarding}

L’intégration pour AEM Content and Commerce est un processus en deux étapes :

1. Installation de l’Ajoute de contenu et de commerce AEM pour AEM 6.5

2. Connectez AEM à votre solution commerciale

### Installer l&#39;Ajoute de contenu et de commerce AEM pour AEM 6.5 {#install-add-on}

Téléchargez et installez l&#39;Ajoute commerciale AEM pour AEM 6.5 à partir du portail [Distribution de logiciels](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).

Début et installation du Service Pack AEM 6.5 requis. Nous vous recommandons d&#39;installer le dernier Service Pack disponible.

>[!NOTE]
>
>Ce sera fait par le CST pour les clients AEM Service Géré.

### Connectez AEM à votre système commercial {#connect}

AEM peut être connecté à tout système commercial qui dispose d&#39;un point de terminaison GraphQL accessible pour AEM. Ces points de terminaison sont généralement accessibles au public ou peuvent être connectés via un VPN privé ou des connexions locales selon la configuration du projet individuel.

Vous pouvez éventuellement fournir un en-tête d’authentification pour utiliser des fonctions CIF supplémentaires nécessitant une authentification.

Les projets générés par l&#39;archétype de projet [AEM ](https://github.com/adobe/aem-project-archetype) et le magasin de référence [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia) qui est déjà inclus dans la configuration [par défaut](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json) doivent être ajustés.

Remplacez la valeur de `url` dans `com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json` par le point de terminaison GraphQL de votre système commercial. Cette configuration peut être effectuée via la console OSGI ou en déployant la configuration OSGI via le projet. Différentes configurations pour les systèmes d’évaluation et de production sont prises en charge à l’aide de différents modes d’exécution AEM.

L’Ajoute de contenu et de commerce AEM et les composants principaux CIF utilisent à la fois AEM connexions côté serveur et côté client. Les composants principaux CIF côté client et les outils de création CIF Ajoute-On se connectent par défaut à `/api/graphql`. Si nécessaire, cette option peut être ajustée via la configuration du Cloud Service CIF (voir ci-dessous).

L&#39;Ajoute CIF-On fournit une servlet proxy GraphQL à l&#39;adresse `/api/graphql` qui peut éventuellement être utilisée pour le [développement local](develop.md). Pour les déploiements de production, il est fortement recommandé de configurer un proxy inverse vers le point de terminaison GraphQL de commerce via le répartiteur d&#39;AEM ou à d&#39;autres couches du réseau (comme CDN).

## Configuration de magasins et de catalogues {#catalog}

L&#39;Ajoute-On et les [Composants principaux du FIC](https://github.com/adobe/aem-core-cif-components) peuvent être utilisés sur plusieurs structures de site AEM reliées à différents magasins commerciaux (ou vues de stockage, etc.). Par défaut, l&#39;Ajoute CIF est déployée avec une configuration par défaut se connectant au magasin et au catalogue par défaut d&#39;Adobe Commerce (Magento).

Cette configuration peut être ajustée pour le projet via la configuration du Cloud Service CIF en procédant comme suit :

1. Dans AEM accédez à Outils -> Cloud Services -> Configuration CIF

2. Sélectionnez la configuration commerciale à modifier.

3. Ouvrez les propriétés de configuration via la barre d’actions.

![Configuration des Cloud Services CIF](/help/commerce/cif/assets/cif-cloud-service-config.png)

Les propriétés suivantes peuvent être configurées :

- Client GraphQL : sélectionnez le client GraphQL configuré pour la communication d&#39;arrière-plan de commerce. En règle générale, cette option doit rester par défaut.
- Vue de stockage : identifiant (Magento) de vue de stockage. Si elle est vide, la vue de stockage par défaut est utilisée.
- Chemin d&#39;accès du proxy GraphQL : chemin d&#39;accès de l&#39;URL Proxy GraphQL dans AEM utilisé pour les demandes de proxy au point de terminaison GraphQL principal du commerce.
   >[!NOTE]
   >
   > Dans la plupart des configurations, la valeur par défaut `/api/graphql` ne doit pas être modifiée. Seule une configuration avancée n&#39;utilisant pas le proxy GraphQL fourni doit modifier ce paramètre.
- Activer la prise en charge de l&#39;UID du catalogue : activez la prise en charge de l&#39;UID plutôt que de l&#39;ID dans les appels GraphQL d&#39;arrière-plan du commerce.
   >[!NOTE]
   >
   > La prise en charge des UID a été introduite dans Adobe Commerce (Magento) 2.4.2. Activez cette option uniquement si votre serveur principal de commerce prend en charge un schéma GraphQL de la version 2.4.2 ou ultérieure.
- Identifiant de Catégorie racine du catalogue - identifiant (UID ou ID) de la racine du catalogue de stockage

La configuration illustrée ci-dessus est à titre de référence. Les projets doivent fournir leurs propres configurations.

Pour des configurations plus complexes à l’aide de plusieurs structures de site AEM associées à différents catalogues commerciaux, consultez le [didacticiel Configuration de plusieurs magasins de commerce](configuring/multi-store-setup.md).

## Ressources supplémentaires {#additional-resources}

- [Archétype de projet AEM](https://github.com/adobe/aem-project-archetype)
- [Magasin de référence Venia AEM](https://github.com/adobe/aem-cif-guides-venia)
- [Configuration de plusieurs magasins commerciaux](configuring/multi-store-setup.md)
