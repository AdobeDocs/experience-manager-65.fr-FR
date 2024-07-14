---
title: Bonnes pratiques pour AEM Mobile On-demand Services
description: Découvrez les bonnes pratiques et les directives qui aident les développeurs Adobe Experience Manager (AEM) compétents pour les sites qui souhaitent créer des modèles d’applications mobiles et des composants.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 63ceaba6-b796-4c13-a86d-f0609ec679c9
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 4%

---

# Bonnes pratiques {#best-practices}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur SPA pour les projets nécessitant un rendu côté client, basé sur un framework, pour une application à une seule page (comme React). [En savoir plus](/help/sites-developing/spa-overview.md).

La création d’une application AEM Mobile On-demand Services diffère de la création d’une application qui s’exécute directement dans le shell Cordova (ou PhoneGap). Les développeurs doivent connaître :

* Modules externes pris en charge prêts à l’emploi et modules externes spécifiques à Adobe Experience Manager (AEM) Mobile .

>[!NOTE]
>
>Pour en savoir plus sur les modules externes, consultez les ressources suivantes :
>
>* [Utilisation des plug-ins Cordova dans AEM Mobile](https://helpx.adobe.com/digital-publishing-solution/help/cordova-api.html)
>* [Utilisation de plug-ins activés pour Cordova spécifiques à AEM Mobile](https://helpx.adobe.com/digital-publishing-solution/help/app-runtime-api.html)
>

* Les modèles qui utilisent la fonctionnalité de module externe doivent être écrits de telle sorte qu’ils puissent toujours être créés dans le navigateur, sans que le pont de module externe soit présent.

   * Par exemple, veillez à attendre la fonction *deviceready* avant de tenter d’accéder à l’API d’un module externe.

## Conseils à l’intention des développeurs AEM {#guidelines-for-aem-developers}

Les instructions suivantes aident les développeurs AEM compétents pour les sites qui souhaitent créer des modèles et des composants d’applications mobiles :

**Modèles de sites d&#39;AEM de structure pour encourager la réutilisation et l&#39;extensibilité**

* Préférer plusieurs fichiers de script de composant sur un seul fichier monolithique

   * Plusieurs points d’extension vides sont fournis, tels que *customheaderlibs.html* et *customfooterlibs.html*, qui permettent au développeur de modifier le modèle de page tout en dupliquant le moins de code principal possible.
   * Les modèles peuvent ensuite être étendus et personnalisés via le mécanisme *sling:resourceSuperType* de Sling

* Préférez Sightly/HTL par rapport à JSP comme langage de modèle.

   * L’utilisation de cette méthode encourage la séparation du code du balisage, offre une protection XSS intégrée et une syntaxe plus familière.

**Optimiser pour les performances sur appareil**

* Le script spécifique à l’article et les feuilles de style doivent être inclus dans la payload de l’article, à l’aide du modèle dps-article contentsync .
* Les feuilles de script et de style partagées par plusieurs articles doivent être incluses dans les ressources partagées au moyen du modèle contentsync dps-HTMLResources
* Ne référencez aucun script externe qui bloque le rendu

>[!NOTE]
>
>Vous pouvez en savoir plus sur les scripts externes de blocage de rendu [ici](https://developers.google.com/speed/docs/insights/BlockingJS).

**Préférez les bibliothèques JS et CSS côté client spécifiques à l’application par rapport aux bibliothèques spécifiques au web**

* Pour éviter les frais généraux liés à des bibliothèques telles que jQuery Mobile afin de gérer un large éventail de périphériques et de navigateurs
* Lorsqu’un modèle s’exécute dans l’affichage Web d’une application, vous avez le contrôle des plateformes et versions que l’application va prendre en charge, et vous savez que la prise en charge de JavaScript sera présente. Par exemple, préférez Ionic (seulement le CSS) à jQuery Mobile et l’interface utilisateur d’Onsen à Bootstrap.

>[!NOTE]
>
>Pour en savoir plus sur jQuery mobile, cliquez [ici](https://jquerymobile.com/browser-support/1.4/).

**Préférer les micro-bibliothèques par rapport à la pile complète**

* Chaque bibliothèque dont dépendent vos articles ralentit le temps nécessaire pour que votre contenu s’affiche sur la vitre de l’appareil. Ce ralentissement est aggravé lorsqu’une nouvelle vue web est utilisée pour effectuer le rendu de chaque article. Chaque bibliothèque doit donc être réinitialisée de zéro.
* Si vos articles ne sont pas créés en tant que SPA (applications d’une seule page), il est probable que vous n’ayez pas besoin d’inclure une bibliothèque de pile complète comme Angular.
* Préférez des bibliothèques plus petites et à usage unique pour ajouter l’interactivité dont votre page a besoin, comme [Fastclick](https://github.com/ftlabs/fastclick) ou [Velocity.js](https://velocityjs.org)

**Minimiser la taille de la charge utile de l’article**

* Utilisez les plus petites ressources possibles pouvant couvrir efficacement la plus grande fenêtre d’affichage que vous prenez en charge, à une résolution raisonnable.
* Utilisez un outil tel que *ImageOptim* sur vos images pour supprimer les métadonnées en trop

## Prise en main {#getting-ahead}

Pour en savoir plus sur les deux autres rôles et responsabilités, consultez les ressources ci-dessous :

* [Administrateur](/help/mobile/aem-mobile.md)
* [Création](/help/mobile/aem-mobile-on-demand.md)
