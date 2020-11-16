---
title: Votre application hybride est-elle prête pour l'AEM Mobile ?
seo-title: Votre application hybride est-elle prête pour l'AEM Mobile ?
description: Suivez cette page pour en savoir plus sur les applications hrybrid. Une application dans AEM est généralement divisée en deux parties. Le "shell" et le "contenu" et cette page fournissent plus d'informations sur ces sujets.
seo-description: Suivez cette page pour en savoir plus sur les applications hrybrid. Une application dans AEM est généralement divisée en deux parties. Le "shell" et le "contenu" et cette page fournissent plus d'informations sur ces sujets.
uuid: cbcce3fa-9100-46ea-9f24-931b42666709
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: b7fd7954-f2a5-402d-b259-e18b5a618be9
pagetitle: Is your hybrid app ready for AEM Mobile?
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '780'
ht-degree: 3%

---


# Votre application hybride est-elle prête pour l&#39;AEM Mobile ?{#is-your-hybrid-app-ready-for-aem-mobile}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

Vous avez donc importé votre application Hybrid PhoneGap ou Cordova en AEM, et maintenant ? Il est probable que vous souhaitiez ajouter du contenu autorisé à votre application. Pour accomplir cette tâche, vous aurez besoin d’une connaissance générale de la structure d’une application AEM. Une application dans AEM est généralement divisée en deux parties. &quot;shell&quot; et &quot;content&quot;. Le &quot;shell&quot; comprend les parties statiques de votre application ; tels que les fichiers de configuration PhoneGap, la structure de l’application et les commandes de navigation. Le contenu de l&#39;archive que vous avez importée est stocké dans le shell. Dans le contexte de ce document, le shell correspond à l’ensemble du contenu non-AEM créé par le développeur de l’application pour votre application PhoneGap hybride.

Le contenu fait référence aux composants, modèles et pages créés dans AEM créé par AEM Developer. Le contenu est classé comme contenu de développement ou comme contenu créé. Les composants, conceptions et modèles de page sont considérés comme du contenu de développement puisqu’ils sont créés par un développeur. author-content sont des pages qui ont été créées à l’aide des composants et des modèles. Elles sont généralement effectuées par un concepteur ou un spécialiste du marketing.

Pour Ajouter les pages d’AEM créées à votre application hybride, il faut une coordination entre le développeur de l’application et le développeur AEM. Partout dans l’application où vous souhaitez ajouter du contenu créé, le développeur de l’application doit organiser ces pages dans une structure qui peut être superposée dans AEM. Le développeur de l’application doit être en mesure de fournir au développeur AEM les chemins d’accès vers l’emplacement où le contenu créé AEM doit être ajouté, puis fournir une page d’espace réservé dans l’application hybride qui sera remplacée une fois que le développeur a créé le contenu de la page.

Pour faciliter le suivi de l&#39;explication, nous utiliserons l&#39;Marketing Cloud AEM : Référence hybride AEM Mobile pour expliquer les concepts. L’application de référence hybride est composée d’une page de bienvenue avec un menu latéral.

![chlimage_1-76](assets/chlimage_1-76.png)

Dans cet exemple, nous allons créer la page de bienvenue de l&#39;application. Jetez un oeil à la source [https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/hybrid-app/www/js/app.js#L75](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/hybrid-app/www/js/app.js#L75). Nous constatons que le développeur d’applications a défini une page d’accueil et fourni un modèle pour la page rendue par l’application. C’est là que le développeur d’applications et le développeur d’AEM doivent se coordonner. Le chemin d’accès au modèle de page d’accueil dans l’application de référence hybride est défini comme étant &quot;&quot;content/mobileapps/hybrid-reference-app/en/welcome.template.html&quot;. Ce chemin d’accès est extrêmement important car le développeur AEM va créer sa page d’accueil dans le référentiel AEM en utilisant le même chemin d’accès.

![chlimage_1-77](assets/chlimage_1-77.png)

Il est important que l’application hybride et le contenu créé AEM utilisent le même chemin d’accès car nous nous appuyons sur la possibilité d’incruster du contenu à l’aide de Content Sync pour ajouter de nouvelles pages à l’application hybride. Lorsque l’application hybride est importée dans AEM dans le cadre du processus d’importation, les configurations Content Sync sont configurées.

![chlimage_1-78](assets/chlimage_1-78.png)

Lorsque vous téléchargez la source à partir du tableau de bord de l’application, ces scripts ContentSync sont exécutés pour assembler une archive de votre application hybride.

![chlimage_1-79](assets/chlimage_1-79.png)

ContentSync extrait d&#39;abord &quot;shell&quot; de l&#39;application, où est stocké tout le contenu développé de l&#39;application hybride, puis extrait le &quot;contenu&quot; de l&#39;application. Désormais, s&#39;il y a des pages dans le shell qui ont le même chemin que dans le contenu, les pages sous le shell seront (remplacées) par les pages sous le contenu. En d&#39;autres termes, dans l&#39;exemple d&#39;application de référence hybride si nous créons une page dans AEM qui a le même chemin que &quot;content/mobileapps/hybrid-reference-app/en/welcome.template.html&quot; lorsque ContentSync s&#39;exécute, elle superpose la page qui faisait partie de l&#39;application de référence hybride avec tout ce qui se trouve en AEM à cet emplacement. L’incrustation est prise en charge par ContentSync. Ainsi, pour les utilisateurs de l’application, les mises à jour apportées à l’application avec le contenu créé AEM apparaîtront sans heurts et ne nécessiteront pas de recréation de l’application. Par conséquent, lorsque vous exécutez l’application, la page d’accueil s’affiche comme suit :

![chlimage_1-80](assets/chlimage_1-80.png)
