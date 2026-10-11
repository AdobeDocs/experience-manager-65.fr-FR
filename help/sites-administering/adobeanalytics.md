---
title: Intégration à Adobe Analytics
description: Découvrez comment intégrer Adobe Experience Manager (AEM) à Adobe Analytics.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: 0a87ece4-57ed-4022-a78a-264c1edf4b4e
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: 243139ec-8e41-5296-a287-31343ab1bc0f
    internal-label: Integration
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 93%
---
# Intégration à Adobe Analytics{#integrating-with-adobe-analytics}

L’intégration d’Adobe Analytics et d’AEM vous permet de suivre votre activité de pages Web :

* Une configuration Adobe Analytics permet à AEM de s’authentifier avec Adobe Analytics.
* Une structure identifie les données envoyées à votre suite de rapports Adobe Analytics.

Les données incluent la page et les données sur l’utilisateur, par exemple :

* Données collectées par les composants AEM
* Clics sur les liens
* Informations sur l’utilisation des vidéos
* Nombre de visites de pages provenant d’Adobe Analytics

Les pages suivantes vous aident à configurer l’intégration :

* [Connexion à Adobe Analytics et création de frameworks](/help/sites-administering/adobeanalytics-connect.md)
* [Configuration du suivi des liens Adobe Analytics](/help/sites-administering/adobeanalytics-link.md)
* [Mappage des données de composant aux propriétés Adobe Analytics](/help/sites-administering/adobeanalytics-mapping.md)
* [Configuration du suivi vidéo pour Adobe Analytics](/help/sites-administering/adobeanalytics-video.md)
* [Adobe Classifications](/help/sites-administering/adobeanalytics-classifications.md)

Vous pouvez également utiliser l’[assistant de souscription](/help/sites-administering/opt-in.md) pour exécuter facilement l’intégration.

>[!NOTE]
>
>Consultez également la procédure : [Intégration d’AEM à Adobe Target et Adobe Analytics à l’aide de DTM](https://helpx.adobe.com/fr/experience-manager/using/integrate-digital-marketing-solutions.html).

## Informations supplémentaires {#further-information}

Voir :

* [Extension de l’intégration à Adobe Analytics](/help/sites-developing/extending-analytics.md) pour plus d’informations sur le développement de composants qui collectent des données utilisateur et la personnalisation de la structure d’Adobe Analytics.

>[!NOTE]
>
>Si vous utilisez Adobe Analytics avec une configuration de proxy personnalisée, vous devez [configurer deux bundles OSGi](/help/sites-deploying/configuring-osgi.md) (par exemple, avec la console web) requis pour les configurations de proxy **Apache HTTP Client**. Les deux lots sont requis, car certaines fonctionnalités d’AEM utilisent les API 3.x, tandis que d’autres utilisent les API 4.x. Configurer :
>
>* **Day Commons HTTP Client 3.1** pour configurer l’API 3.x ;
>  par exemple, [&#128279;](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>
>* **Apache HTTP Components Proxy Configuration** pour configurer l’API 4.x ;
>  par exemple, [&#128279;](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>
