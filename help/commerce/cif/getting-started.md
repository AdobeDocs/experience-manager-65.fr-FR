---
title: Prise en main d’AEM Content and Commerce
description: Découvrez comment déployer un projet Content and Commerce AEM.
topics: Commerce
feature: Commerce Integration Framework
thumbnail: 37843.jpg
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 6%

---

# Prise en main d’AEM Content and Commerce {#start}

Pour commencer à utiliser AEM Content and Commerce, vous devez installer AEM module complémentaire Content and Commerce pour 6.5.

## Configuration logicielle minimale requise

[AEM 6.5 Service Pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) 7 ou version ultérieure est requis.

## Intégration {#onboarding}

L’intégration à AEM Content and Commerce est un processus en deux étapes :

1. Installation du module complémentaire Content and Commerce AEM pour AEM 6.5

2. Connexion d’AEM à votre solution commerciale

### Installez le module complémentaire Content and Commerce AEM pour AEM 6.5 {#install-add-on}

Téléchargez et installez le module complémentaire Commerce AEM pour AEM 6.5 à partir du portail [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).

Démarrez et installez le Service Pack d’AEM 6.5 requis. Nous vous recommandons d’installer le dernier Service Pack disponible.

>[!NOTE]
>
>Cela sera effectué par l’ingénieur du service client pour les clients AEM Managed Service.

### Connexion d’AEM à votre système Commerce {#connect}

AEM peut être connecté à n’importe quel système commercial disposant d’un point d’entrée GraphQL accessible pour AEM. Ces points de terminaison sont généralement disponibles publiquement ou peuvent être connectés via des connexions VPN privées ou locales selon la configuration du projet individuel.

En option, l’en-tête d’authentification peut être fourni pour utiliser des fonctionnalités CIF supplémentaires nécessitant une authentification.

Les projets générés par [AEM Project Archetype](https://github.com/adobe/aem-project-archetype) et le [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia) qui est déjà inclus dans la [configuration par défaut](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json) doivent être ajustés.

Remplacez la valeur de `url` dans `com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json` par le point d’entrée GraphQL de votre système commercial. Cette configuration peut être effectuée via la console OSGI ou en déployant la configuration OSGI via le projet. Les différentes configurations pour les systèmes d’évaluation et de production sont prises en charge à l’aide de différents modes d’exécution AEM.

Le module complémentaire Content and Commerce AEM et les composants principaux CIF utilisent AEM connexions côté serveur et côté client. Les composants principaux CIF côté client et les outils de création de module complémentaire CIF se connectent par défaut à `/api/graphql`. Cela peut être ajusté via la configuration du Cloud Service CIF si nécessaire (voir ci-dessous).

Le module complémentaire CIF fournit une servlet proxy GraphQL à l’adresse `/api/graphql` qui peut éventuellement être utilisée pour le [développement local](develop.md). Pour les déploiements de production, il est vivement recommandé de configurer un proxy inverse vers le point d’entrée GraphQL de commerce via le Dispatcher AEM ou sur d’autres couches réseau (comme CDN).

## Configuration de magasins et de catalogues {#catalog}

Le module complémentaire et les [composants principaux CIF](https://github.com/adobe/aem-core-cif-components) peuvent être utilisés sur plusieurs structures de site AEM connectées à différents magasins de commerce (ou vues de magasin, etc.). Par défaut, le module complémentaire CIF est déployé avec une configuration par défaut se connectant au magasin et au catalogue par défaut d’Adobe Commerce (Magento).

Cette configuration peut être ajustée pour le projet via la configuration du Cloud Service CIF en procédant comme suit :

1. Dans AEM, accédez à Outils -> Cloud Services -> Configuration CIF.

2. Sélectionnez la configuration commerciale à modifier.

3. Ouvrez les propriétés de configuration via la barre d’actions.

![Configuration des Cloud Services CIF](/help/commerce/cif/assets/cif-cloud-service-config.png)

Les propriétés suivantes peuvent être configurées :

- Client GraphQL : sélectionnez le client GraphQL configuré pour la communication du serveur principal Commerce. Cela doit généralement rester par défaut.
- Affichage de magasin : identifiant de vue de magasin (Magento). Si cette valeur est vide, la vue de magasin par défaut est utilisée.
- Chemin du proxy GraphQL : chemin d’URL du proxy GraphQL dans AEM utilisé pour les requêtes proxy vers le point d’entrée GraphQL principal du commerce.
   >[!NOTE]
   >
   > Dans la plupart des configurations, la valeur par défaut `/api/graphql` ne doit pas être modifiée. Seule la configuration avancée n’utilisant pas le proxy GraphQL fourni doit modifier ce paramètre.
- Activer la prise en charge de l’UID du catalogue : activez la prise en charge de l’UID au lieu de l’ID dans les appels GraphQL du serveur principal de commerce.
   >[!NOTE]
   >
   > La prise en charge des UID a été introduite dans Adobe Commerce (Magento) 2.4.2. Activez cette option uniquement si votre serveur principal Commerce prend en charge un schéma GraphQL de la version 2.4.2 ou ultérieure.
- Identifiant de catégorie racine du catalogue : l’identifiant (UID ou ID) de la racine du catalogue du magasin.

La configuration illustrée ci-dessus est à titre de référence. Les projets doivent fournir leurs propres configurations.

Pour des configurations plus complexes à l’aide de plusieurs structures de site AEM combinées à différents catalogues commerciaux, consultez le tutoriel [Configuration multi-magasin de commerce](configuring/multi-store-setup.md) .

## Ressources supplémentaires {#additional-resources}

- [Archétype de projet AEM](https://github.com/adobe/aem-project-archetype)
- [Magasin de référence Venia AEM](https://github.com/adobe/aem-cif-guides-venia)
- [Configuration multi-magasin Commerce](configuring/multi-store-setup.md)
