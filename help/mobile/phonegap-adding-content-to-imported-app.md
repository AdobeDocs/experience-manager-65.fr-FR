---
title: Votre application hybride est-elle prête pour AEM Mobile ?
description: Découvrez les applications hybrides. Dans Experience Manager, une application est généralement divisée en deux parties. Les sections « shell » et « content », ainsi que cette page, fournissent plus d’informations sur insight dans ces rubriques.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
pagetitle: Is your hybrid app ready for AEM Mobile?
exl-id: 4625890c-2b76-4c78-88e8-23741bc09f5b
solution: Experience Manager
feature: Mobile
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '738'
ht-degree: 1%
---
# Votre application hybride est-elle prête pour Adobe Experience Manager Mobile ?{#is-your-hybrid-app-ready-for-aem-mobile}

{{ue-over-mobile}}

Vous avez donc importé votre application Hybrid PhoneGap ou Cordova dans AEM, et maintenant ? Vous souhaitez probablement ajouter du contenu modifiable à votre application. Pour accomplir cette tâche, vous avez besoin d’une compréhension générale de la structure d’une application AEM. Dans AEM, une application est généralement divisée en deux parties. Le « shell » et le « content ». Le shell comprend les parties statiques de votre application, telles que les fichiers de configuration PhoneGap, le framework de l’application et les commandes de navigation. Le contenu de l’archive importée est stocké dans le shell. Dans le cadre de ce document, le shell est tout le contenu non créé par AEM de votre application Hybrid PhoneGap créée par le développeur d’applications.

Le contenu fait référence aux composants, modèles et pages créés dans AEM créés par le développeur d’AEM. Le contenu est classé en tant que contenu développeur ou contenu créé. Les composants, les conceptions et les modèles de page sont considérés comme des contenus de développement, car ils sont créés par un développeur ou une développeuse. Les contenus de création sont des pages qui ont été créées à l’aide des composants et des modèles. Ces pages sont généralement créées par un Designer ou un marketeur.

L’ajout de pages AEM créées à votre application hybride nécessite une coordination entre le développeur d’applications et le développeur d’AEM. À tout endroit de l’application où vous souhaitez ajouter du contenu créé, le développeur ou la développeuse de l’application doit organiser ces pages dans une structure qui peut être superposée dans Experience Manager. Le développeur d’application doit être en mesure de lui fournir les chemins d’accès vers lesquels le contenu créé par Experience Manager est ajouté. Ensuite, fournissez une page d’espace réservé dans l’application hybride qui est remplacée une fois que le développeur Experience Manager a créé le contenu de la page.

Pour faciliter la compréhension de l’explication, AEM Experience Cloud est utilisé : Référence hybride AEM Mobile pour expliquer les concepts. L’application Référence hybride se compose d’une page d’accueil avec un menu latéral.

![chlimage_1-76](assets/chlimage_1-76.png)

Dans cet exemple, la page d’accueil de l’application va être créée. En examinant la source [&#128279;](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/hybrid-app/www/js/app.js#L75). Notez que le développeur ou la développeuse d’applications a défini une page d’accueil et fourni un modèle pour la page générée par l’application. Sur cette page, le développeur d’application et le développeur AEM doivent se coordonner. Le chemin d’accès au modèle de page d’accueil dans l’application de référence hybride est défini sur « content/mobileapps/hybrid-reference-app/en/welcome.template.html ». Ce chemin est important, car le développeur AEM créera sa page d’accueil dans le référentiel AEM à l’aide du même chemin.

![chlimage_1-77](assets/chlimage_1-77.png)

Il est important que l’application hybride et le contenu créé par AEM utilisent le même chemin d’accès, car cela repose sur la possibilité de superposer du contenu à l’aide de la synchronisation de contenu pour ajouter de nouvelles pages à l’application hybride. Lors de l’importation de l’application hybride dans AEM, dans le cadre du processus d’importation, les configurations de synchronisation de contenu sont configurées.

![chlimage_1-78](assets/chlimage_1-78.png)

Lorsque vous « Téléchargez Source » à partir du tableau de bord de l’application, ces scripts ContentSync sont exécutés pour assembler une archive de votre application hybride.

![chlimage_1-79](assets/chlimage_1-79.png)

ContentSync extrait d’abord le shell de l’application, où est stocké tout le contenu développé par l’application dans l’application hybride. Ensuite, il extrait le « contenu » de l’application. Désormais, si des pages dans le « shell » ont le même chemin d’accès que dans « content », les pages sous « shell » sont (remplacées) par les pages sous « content ». Ainsi, dans l’exemple d’application de référence hybride, si une page créée dans AEM a le même chemin d’accès que « content/mobileapps/hybrid-reference-app/en/welcome.template.html », lorsque ContentSync s’exécute, elle recouvre la page qui faisait partie de l’application de référence hybride. Il le recouvre avec tout ce qui se trouve dans AEM à cet emplacement. La superposition est gérée par ContentSync. Ainsi, pour une personne qui utilise l’application, les mises à jour de l’application avec le contenu créé par AEM sont transparentes et ne nécessitent pas de reconstruire l’application. Par conséquent, lorsque vous exécutez l’application, la page d’accueil s’affiche comme suit :

![chlimage_1-80](assets/chlimage_1-80.png)
