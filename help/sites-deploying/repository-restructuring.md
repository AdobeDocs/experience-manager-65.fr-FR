---
title: Restructuration des référentiels dans AEM 6.5
seo-title: Restructuration des référentiels dans AEM 6.5
description: Découvrez les principes de base et la logique sur laquelle repose le reformatage des référentiels dans AEM 6.5
seo-description: Découvrez les principes de base et la logique sur laquelle repose le reformatage des référentiels dans AEM 6.5
uuid: e9cd3e88-e352-44a8-9b97-69488d3267cb
contentOwner: chaikels
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: fc879b0b-823b-4bdc-aaa6-36f53a33fb22
feature: Mise à niveau
exl-id: 2572aa8d-2a3a-4e5b-ae5f-07e1017ea0f4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 61%

---

# Restructuration des référentiels dans AEM 6.5{#repository-restructuring-in-aem}

## Présentation {#introduction}

Avant la version 6.4 d’AEM, le code client était déployé dans des zones imprévisibles du JCR qui pouvaient faire l’objet de modifications lors des mises à niveau. C’est pourquoi il était courant que les versions d’AEM officielles écrasent le code, la configuration ou le contenu personnalisé. En outre, les modifications apportées aux clients remplaçaient parfois le code ou le contenu du produit AEM, annulant les fonctionnalités du produit.

Il est possible d’éviter ces conflits en définissant clairement les hiérarchies applicables au code du produit AEM et au code client.

À cette fin, à partir de la version 6.4 d’AEM et qui sera poursuivie dans les prochaines versions, le contenu est restructuré depuis /etc vers d’autres dossiers du référentiel, ainsi que des directives sur le contenu à destination, en respectant les règles de haut niveau suivantes :

* Le code de produit AEM sera toujours placé dans /libs, qui ne peut pas être écrasé par du code personnalisé.
* Le code personnalisé doit être placé dans /apps, /content et /conf.

## Impact sur les mises à niveau vers le version 6.5 {#impact-on-upgrades}

Lors de la mise à niveau vers AEM 6.5, un sous-ensemble important du contenu sous /etc sera dupliqué dans d’autres dossiers du référentiel. Ces nouveaux emplacements sont les emplacements favoris dans lesquels le contenu est référencé. Cependant, tout a été mis en œuvre pour que la mise à niveau d’AEM 6.5 soit rétrocompatible avec les emplacements précédents du dossier /etc. Ainsi, dans la plupart des cas, les anciens emplacements continueront à être référencés par le code AEM jusqu’à ce que les modifications soient activement - et dans de nombreux cas manuellement - créées dans l’application d’un client. Du point de vue de la chronologie, il existe deux catégories de modifications :

* Avec la mise à niveau vers la version 6.5 : quelques modifications de restructuration /etc ne sont pas compatibles avec les versions antérieures. Par conséquent, les modifications doivent être planifiées et implémentées dans le cadre de la mise à niveau d’AEM 6.5.
* Avant la mise à niveau ultérieure : la grande majorité des modifications de restructuration /etc peuvent être différées jusqu’à un certain temps après la mise à niveau. Comme mentionné précédemment, le code AEM 6.5 continuera à faire référence aux anciens emplacements jusqu’à ce que les modifications soient implémentées dans le cadre d’une version client. Bien qu’il n’existe pas de calendrier forcé pour lequel les modifications doivent être apportées, il est recommandé de les effectuer avant la mise à niveau ultérieure, car les fonctionnalités futures pourront dépendre des nouveaux emplacements référencés. De plus, par convention, la documentation relative à une fonctionnalité donnée référencera les nouveaux emplacements. Cela pourrait donc prêter à confusion si les anciens emplacements sont toujours utilisés.

### Guide de restructuration {#restructuring-guidance}

Lors de la planification d’une mise à niveau vers AEM 6.5, les pages suivantes par solution doivent être référencées afin d’évaluer le travail :

* [Restructuration du référentiel commun à toutes les solutions AEM](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md)
* [Restructuration du référentiel d’AEM Sites](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md)
* [Restructuration du référentiel AEM Assets](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md)
* [Restructuration du référentiel d’AEM Assets Dynamic Media](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md)
* [Restructuration du référentiel AEM Forms](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md)
* [Restructuration du référentiel AEM Communities](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md)
* [Restructuration du référentiel d’AEM Commerce](/help/sites-deploying/ecommerce-repository-restructuring-in-aem-6-5.md)

Chaque page contient deux sections correspondant à l’urgence des modifications nécessaires. Tout élément de la section « Avec la mise à niveau vers la version 6.5 » doit être traité dans le cadre du projet de mise à niveau d’AEM 6.5. Tout ce qui se trouve sous &quot;Avant la mise à niveau vers l’avenir&quot; peut éventuellement être différé jusqu’à après la mise à niveau.

Chaque entrée de la page comprend un champ &quot;Conseil de restructuration&quot;, qui détaille la stratégie technique recommandée pour l’alignement avec le nouveau modèle de référentiel 6.5 afin que les nouveaux emplacements soient référencés pour le contenu situé précédemment sous le dossier /etc. Un champ supplémentaire « Remarques » fournit un contexte utile.
