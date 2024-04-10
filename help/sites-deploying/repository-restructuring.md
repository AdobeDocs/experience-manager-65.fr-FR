---
title: Restructuration des référentiels dans AEM 6.5
description: Découvrez les principes de base et la logique sur laquelle repose le reformatage des référentiels dans AEM 6.5.
contentOwner: chaikels
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: 2572aa8d-2a3a-4e5b-ae5f-07e1017ea0f4
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 100%

---

# Restructuration des référentiels dans AEM 6.5{#repository-restructuring-in-aem}

## Présentation {#introduction}

Dans les versions antérieures à AEM 6.4, le code client était déployé dans des zones imprévisibles du référentiel JCR, lesquelles pouvaient donc varier lors des mises à niveau. Pour cette raison, il était courant que les versions AEM officielles écrasent le code, la configuration ou le contenu personnalisé. En outre, les modifications des clientes et clients remplacent parfois le code ou le contenu du produit AEM, rompant ainsi la fonctionnalité du produit.

Il est possible d’éviter ces conflits en définissant clairement les hiérarchies applicables au code du produit AEM et au code client.

À cette fin, à compter de la version AEM 6.4 et pour les versions à venir, le contenu est restructuré à partir de /etc vers d’autres dossiers du référentiel, avec des instructions sur le contenu du répertoire, en respectant les règles de haut niveau suivantes :

* Le code de produit AEM sera toujours placé dans /libs, qui ne peut pas être écrasé par du code personnalisé.
* Le code personnalisé doit être placé dans /apps, /content et /conf.

## Impact sur les mises à niveau vers la version 6.5 {#impact-on-upgrades}

Lors de la mise à niveau vers AEM 6.5, un sous-ensemble important du contenu sous /etc sera dupliqué dans d’autres dossiers du référentiel. Ces nouveaux emplacements sont les emplacements favoris dans lesquels le contenu est référencé. Cependant, tout a été mis en œuvre pour que la mise à niveau d’AEM 6.5 soit rétrocompatible avec les emplacements précédents du dossier /etc. Ainsi, dans la plupart des cas, les anciens emplacements continueront à être référencés par le code AEM jusqu’à ce que les modifications soient activement - et dans de nombreux cas manuellement - créées dans l’application d’un client. Du point de vue de la chronologie, il existe deux catégories de modifications :

* Avec la mise à niveau vers la version 6.5 : quelques modifications de restructuration /etc ne sont pas compatibles avec les versions antérieures. Par conséquent, les modifications doivent être planifiées et implémentées dans le cadre de la mise à niveau d’AEM 6.5.
* Avant la mise à niveau vers la future version : la grande majorité des modifications de restructuration /etc peuvent être différées à une période ultérieure à la mise à niveau. Comme mentionné précédemment, le code AEM 6.5 continuera à faire référence aux anciens emplacements jusqu’à ce que les modifications soient implémentées dans le cadre d’une version client. Bien qu’il n’y ait pas de calendrier forcé pour apporter les modifications, il est recommandé de les effectuer avant la mise à niveau vers la version car les fonctionnalités futures peuvent s’appuyer sur les nouveaux emplacements référencés. De plus, par convention, la documentation relative à une fonctionnalité donnée référencera les nouveaux emplacements. Cela pourrait donc prêter à confusion si les anciens emplacements sont toujours utilisés.

### Conseils de restructuration {#restructuring-guidance}

Lors de la planification d’une mise à niveau vers AEM 6.5, les pages suivantes par solution doivent être référencées afin d’évaluer l’effort de travail :

* [Restructuration du référentiel commun à toutes les solutions AEM](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md)
* [Restructuration du référentiel d’AEM Sites](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md)
* [Restructuration du référentiel d’AEM Assets](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md)
* [Restructuration du référentiel d’AEM Assets Dynamic Media](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md)
* [Restructuration du référentiel d’AEM Forms](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md)
* [Restructuration du référentiel d’AEM Communities](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md)
* [Restructuration du référentiel d’AEM Commerce](/help/sites-deploying/ecommerce-repository-restructuring-in-aem-6-5.md)

Chaque page contient deux sections correspondant à l’urgence des modifications nécessaires. Tout élément de la section « Avec la mise à niveau vers la version 6.5 » doit être traité dans le cadre du projet de mise à niveau d’AEM 6.5. Tout ce qui se trouve sous « Avant la mise à niveau vers la version » peut éventuellement être différé jusqu’à une période ultérieure à la mise à niveau.

Chaque entrée de la page comprend un champ « Conseil de restructuration » qui détaille la stratégie technique recommandée pour l’alignement avec le nouveau modèle de référentiel 6.5 afin que les nouveaux emplacements soient référencés pour le contenu situé précédemment sous le dossier /etc. Un champ supplémentaire « Remarques » fournit un contexte utile.
