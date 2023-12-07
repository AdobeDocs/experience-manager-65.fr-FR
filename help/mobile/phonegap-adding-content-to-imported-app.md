---
title: Votre application hybride est-elle prête pour AEM Mobile ?
description: Découvrez les applications hybrides. Une application en Experience Manager est généralement divisée en deux parties. Le "shell" et le "contenu" et cette page fournissent des informations supplémentaires sur ces sujets.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
pagetitle: Is your hybrid app ready for AEM Mobile?
exl-id: 4625890c-2b76-4c78-88e8-23741bc09f5b
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 1%

---

# Votre application hybride est-elle prête pour Adobe Experience Manager Mobile ?{#is-your-hybrid-app-ready-for-aem-mobile}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur de SPA pour les projets qui nécessitent un rendu côté client basé sur la structure d’application d’une seule page (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

Vous avez importé votre application PhoneGap hybride ou Cordova dans AEM, et maintenant ? Il est probable que vous souhaitiez ajouter du contenu modifiable à votre application. Pour accomplir cette tâche, vous avez besoin d’une compréhension générale de la structure d’une application AEM. Une application dans AEM est généralement divisée en deux parties. &quot;shell&quot; et &quot;contenu&quot;. Le &quot;shell&quot; comprend les parties statiques de votre application, telles que les fichiers de configuration PhoneGap, la structure de l’application et les commandes de navigation. Le contenu de l’archive que vous avez importée est stocké dans le shell. Dans le contexte de ce document, le shell est tout le contenu créé non AEM de votre application PhoneGap hybride créée par le développeur de l’application.

Le contenu fait référence aux composants, modèles et pages créées dans AEM générés par le développeur AEM. Le contenu est classé comme contenu de développement ou comme contenu créé. Les composants, conceptions et modèles de page sont considérés comme du contenu de développement puisqu’ils sont créés par un développeur. Les contenus d’auteur sont des pages qui ont été créées à l’aide des composants et des modèles. Ces pages sont généralement effectuées par un concepteur ou un spécialiste du marketing.

L’ajout de pages d’AEM créées à votre application hybride nécessite une coordination entre le développeur de l’application et le développeur AEM. Partout dans l’application où vous souhaitez ajouter du contenu créé, le développeur de l’application doit organiser ces pages dans une structure qui peut être superposée en Experience Manager. Le développeur de l’application doit être en mesure de fournir au développeur du Experience Manager les chemins vers lesquels le contenu créé du Experience Manager est ajouté. Ensuite, fournissez une page d’espace réservé dans l’application hybride qui est remplacée une fois que le développeur du Experience Manager a créé le contenu de la page.

Pour faciliter l’explication, l’Experience Cloud d’AEM est utilisé : Référence hybride AEM Mobile pour expliquer les concepts. L’application de référence hybride se compose d’une page de bienvenue avec un menu latéral.

![chlimage_1-76](assets/chlimage_1-76.png)

Dans cet exemple, la page d’accueil de l’application va être créée. Recherche de la source [https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/hybrid-app/www/js/app.js#L75](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/hybrid-app/www/js/app.js#L75). Notez que le développeur de l’application a défini une page de bienvenue et fourni un modèle pour la page rendue par l’application. C’est sur cette page que le développeur de l’application et le développeur AEM doivent se coordonner. Le chemin d’accès au modèle de page de bienvenue dans l’application de référence hybride est défini sur &quot;content/mobileapps/hybrid-reference-app/en/welcome.template.html&quot;. Ce chemin d’accès est important, car le développeur AEM va créer sa page de bienvenue dans le référentiel AEM en utilisant le même chemin d’accès.

![chlimage_1-77](assets/chlimage_1-77.png)

Il est important que l’application hybride et le contenu créé AEM utilisent le même chemin d’accès, car il repose sur la possibilité de superposer du contenu à l’aide de la synchronisation de contenu pour ajouter de nouvelles pages à l’application hybride. Lorsque l’application hybride est importée dans AEM, les configurations de synchronisation de contenu sont configurées dans le cadre du processus d’importation.

![chlimage_1-78](assets/chlimage_1-78.png)

Lorsque vous &quot;Téléchargez la source&quot; depuis le tableau de bord de l’application, ces scripts ContentSync sont exécutés pour assembler une archive de votre application hybride.

![chlimage_1-79](assets/chlimage_1-79.png)

ContentSync extrait d’abord &quot;shell&quot; de l’application, où est stocké tout le contenu développé par l’application Hybrid. Ensuite, il extrait le &quot;contenu&quot; de l’application. Désormais, s’il existe des pages dans &quot;shell&quot; qui ont le même chemin que dans &quot;contenu&quot;, les pages sous &quot;shell&quot; sont (remplacées) par les pages sous &quot;contenu&quot;. Ainsi, dans l’exemple d’application de référence hybride, si une page est créée dans AEM avec le même chemin que &quot;content/mobileapps/hybrid-reference-app/en/welcome.template.html&quot;, lorsque ContentSync s’exécute, elle incruste la page qui faisait partie de l’application de référence hybride. Il le superpose avec tout ce qui se trouve dans AEM à cet emplacement. La superposition est gérée par ContentSync. Pour les utilisateurs de l’application, les mises à jour apportées à l’application avec AEM contenu créé apparaissent de manière transparente et ne nécessitent pas de reconstruction de l’application. Par conséquent, lorsque vous exécutez l’application, la page de bienvenue s’affiche comme suit :

![chlimage_1-80](assets/chlimage_1-80.png)
