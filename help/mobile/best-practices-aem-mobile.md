---
title: Bonnes pratiques relatives à AEM Mobile On-demand Services
description: Découvrez les bonnes pratiques et les directives qui aident les développeurs Adobe Experience Manager (AEM) compétents pour les sites qui souhaitent créer des modèles et des composants d’applications mobiles.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 63ceaba6-b796-4c13-a86d-f0609ec679c9
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 0%

---

# Bonnes pratiques {#best-practices}

{{ue-over-mobile}}

La création d’une application AEM Mobile On-demand Services est différente de la création d’une application qui s’exécute directement dans le shell Cordova (ou PhoneGap). Les développeurs doivent connaître les éléments suivants :

* Modules externes prêts à l’emploi et modules externes spécifiques à Adobe Experience Manager (AEM) Mobile.

>[!NOTE]
>
>Pour en savoir plus sur les modules externes, consultez les ressources suivantes :
>
>* [Utilisation des plug-ins Cordova dans AEM Mobile](https://helpx.adobe.com/digital-publishing-solution/help/cordova-api.html)
>* [Utilisation de plug-ins Cordova spécifiques à AEM Mobile](https://helpx.adobe.com/digital-publishing-solution/help/app-runtime-api.html)
>

* Les modèles qui utilisent la fonctionnalité de module externe doivent être écrits de manière à pouvoir être créés dans le navigateur, sans que le pont de module externe soit présent.

   * Par exemple, veillez à attendre la fonction *deviceready* avant de tenter d’accéder à l’API d’un plug-in.

## Consignes destinées aux développeurs d’AEM {#guidelines-for-aem-developers}

Les instructions suivantes aident les développeurs AEM compétents pour les sites qui souhaitent créer des modèles et des composants d’applications mobiles :

**Structurer les modèles de sites AEM pour encourager la réutilisation et l’extensibilité**

* Préférez plusieurs fichiers de script de composant à un fichier monolithique unique

   * Plusieurs points d’extension vides sont fournis, tels que *customheaderlibs.html* et *customfooterlibs.html*, qui permettent au développeur ou à la développeuse de modifier le modèle de page tout en dupliquant le moins de code principal possible
   * Les modèles peuvent ensuite être étendus et personnalisés via le mécanisme *sling:resourceSuperType* de Sling

* Préférez Sightly/HTL au JSP en tant que langage de modèle

   * L’utilisation de cette syntaxe favorise la séparation du code des balises, offre une protection XSS intégrée et a une syntaxe plus familière

**Optimiser les performances sur l’appareil**

* Le script et les feuilles de style spécifiques à l’article doivent être inclus dans la payload d’article à l’aide du modèle de synchronisation de contenu dps-article
* Les feuilles de script et de style partagées par plusieurs articles doivent être incluses dans les ressources partagées, au moyen du modèle de synchronisation de contenu dps-HTMLResources
* Ne référencez aucun script externe bloquant le rendu

>[!NOTE]
>
>Pour en savoir plus sur les scripts externes bloquant le rendu, cliquez [ici](https://developers.google.com/speed/docs/insights/BlockingJS).

**Préférez les bibliothèques JS et CSS côté client spécifiques à l’application à celles spécifiques au web**

* Pour éviter de surcharger les bibliothèques telles que jQuery Mobile afin de gérer une énorme variété d’appareils et de navigateurs
* Lorsqu’un modèle est exécuté dans l’affichage Web d’une application, vous avez le contrôle sur les plateformes et versions que l’application va prendre en charge et la connaissance de la prise en charge de JavaScript. Par exemple, préférez Ionic (uniquement le CSS) à jQuery Mobile et l’interface utilisateur Onsen à Bootstrap.

>[!NOTE]
>
>Pour en savoir plus sur jQuery Mobile, cliquez [ici](https://jquerymobile.com/browser-support/1.4/).

**Préférez les microbibliothèques à la pile complète**

* Le temps nécessaire pour placer votre contenu sur le verre de l’appareil est ralenti par chaque bibliothèque dont dépendent vos articles. Ce ralentissement est aggravé lorsqu’une nouvelle vue web est utilisée pour effectuer le rendu de chaque article, de sorte que chaque bibliothèque doit être initialisée à nouveau à partir de zéro
* Si vos articles ne sont pas créés en tant que SPA (applications d’une seule page), vous n’avez probablement pas besoin d’inclure une bibliothèque full stack comme Angular
* Privilégiez les bibliothèques plus petites et à usage unique qui permettent d’ajouter l’interactivité dont votre page a besoin, par exemple [Fastclick](https://github.com/ftlabs/fastclick) ou [Velocity.js](https://velocityjs.org)

**Réduire la taille de la payload de l’article**

* Utilisez les ressources les plus petites possible afin de couvrir efficacement la fenêtre d’affichage la plus grande que vous prenez en charge, avec une résolution raisonnable
* Utilisez un outil tel que *ImageOptim* sur vos images afin de supprimer tout excès de métadonnées

## Progresser {#getting-ahead}

Pour en savoir plus sur les deux autres rôles et responsabilités, consultez les ressources ci-dessous :

* [Administrateur](/help/mobile/aem-mobile.md)
* [Création](/help/mobile/aem-mobile-on-demand.md)
