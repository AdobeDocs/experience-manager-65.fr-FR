---
title: Intégration à Adobe Analytics
description: Découvrez comment intégrer Adobe Experience Manager (AEM) à Adobe Analytics.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: 0a87ece4-57ed-4022-a78a-264c1edf4b4e
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 96%

---

# Intégration à Adobe Analytics{#integrating-with-adobe-analytics}

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Cliquez ici](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/integrations/integrating-adobe-analytics.html?lang=fr) |
| AEM 6.5 | Cet article |


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
* L’article de la base de connaissances, [Intégration Adobe Analytics : résolution des incidents](https://helpx.adobe.com/fr/experience-manager/kb/sitecatalystintegrationtroubleshooting.html) pour plus d’informations concernant le dépannage de votre intégration Adobe Analytics.

>[!NOTE]
>
>Si vous utilisez Adobe Analytics avec une configuration de proxy personnalisée, vous devez [configurer deux lots OSGi](/help/sites-deploying/configuring-osgi.md) (par exemple, avec la console web) requis pour les configurations de proxy **Apache HTTP Client**. Les deux lots sont requis, car certaines fonctionnalités d’AEM utilisent les API 3.x, tandis que d’autres utilisent les API 4.x. Configurer :
>
>* **Day Commons HTTP Client 3.1** pour configurer l’API 3.x ;
>  par exemple, [https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>
>* **Apache HTTP Components Proxy Configuration** pour configurer l’API 4.x ;
>  par exemple, [https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>
