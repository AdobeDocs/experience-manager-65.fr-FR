---
title: Intégration à Adobe Analytics
seo-title: Intégration à Adobe Analytics
description: Découvrez comment intégrer AEM à Adobe Analytics.
seo-description: Découvrez comment intégrer AEM à Adobe Analytics.
uuid: d8548263-6ac5-45fb-8c70-52ecd4161bbb
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 444c522e-2f33-4f41-846c-8d317e799659
docset: aem65
translation-type: tm+mt
source-git-commit: ca25e66b280db479f69c487753a557b0240233da
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 100%

---


# Intégration à Adobe Analytics{#integrating-with-adobe-analytics}

L’intégration d’Adobe Analytics et d’AEM vous permet de suivre votre activité de pages web :

* Une configuration Adobe Analytics permet à AEM de s’authentifier avec Adobe Analytics.
* Une structure identifie les données envoyées à votre suite de rapports Adobe Analytics.

Les données incluent la page et les données sur l’utilisateur, par exemple :

* Données collectées par les composants AEM
* Clics sur les liens
* Informations sur l’utilisation des vidéos
* Nombre de visites de pages provenant d’Adobe Analytics

Les pages suivantes vous aident à configurer l’intégration :

* [Connexion à Adobe Analytics et création de structures](/help/sites-administering/adobeanalytics-connect.md)
* [Configuration du suivi des liens pour Adobe Analytics](/help/sites-administering/adobeanalytics-link.md)
* [Mise en correspondance des données de composant avec les propriétés Adobe Analytics](/help/sites-administering/adobeanalytics-mapping.md)
* [Configuration du suivi vidéo pour Adobe Analytics](/help/sites-administering/adobeanalytics-video.md)
* [Classifications Adobe](/help/sites-administering/adobeanalytics-classifications.md)

Vous pouvez également utiliser l’[assistant de souscription](/help/sites-administering/opt-in.md) pour exécuter facilement l’intégration.

>[!NOTE]
>
>Voir également l’article de procédures : [Intégration d’AEM avec Adobe Target et Analytics à l’aide de la gestion dynamique des balises](https://helpx.adobe.com/fr/experience-manager/using/integrate-digital-marketing-solutions.html).

## Informations supplémentaires {#further-information}

Voir :

* [Extension de l’intégration à Adobe Analytics](/help/sites-developing/extending-analytics.md) pour plus d’informations sur le développement de composants qui collectent des données utilisateur et la personnalisation de la structure d’Adobe Analytics.
* L’article de la base de connaissances, [Intégration Adobe Analytics : résolution des incidents ](https://helpx.adobe.com/experience-manager/kb/sitecatalystintegrationtroubleshooting.html) pour plus d’informations concernant le dépannage de votre intégration Adobe Analytics.

>[!NOTE]
>
>Si vous utilisez Adobe Analytics avec une configuration de proxy personnalisée, vous devez [configurer deux lots OSGi](/help/sites-deploying/configuring-osgi.md) (par exemple, avec la console web) requis pour les configurations de proxy **Apache HTTP Client**. Les deux lots sont requis, car certaines fonctionnalités d’AEM utilisent les API 3.x, tandis que d’autres utilisent les API 4.x. Configurer:
>
>* **Day Commons HTTP Client 3.1** pour configurer l’API 3.x ;
   >  par exemple, [https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
   >
   >
* **Apache HTTP Components Proxy Configuration** pour configurer l’API 4.x ;
   >  par exemple, [https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)

>



