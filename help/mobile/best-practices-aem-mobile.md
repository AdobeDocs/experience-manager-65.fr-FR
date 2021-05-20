---
title: Bonnes pratiques
seo-title: Bonnes pratiques
description: Consultez cette page pour découvrir les bonnes pratiques et les directives qui aideront les développeurs AEM expérimentés pour les sites qui souhaitent créer des modèles d’applications mobiles et des composants.
seo-description: Consultez cette page pour découvrir les bonnes pratiques et les directives qui aideront les développeurs AEM expérimentés pour les sites qui souhaitent créer des modèles d’applications mobiles et des composants.
uuid: 7733c8b1-a88c-455c-8080-f7add4205b92
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: a0647696-72c3-409b-85ba-9275d8f99cff
exl-id: 63ceaba6-b796-4c13-a86d-f0609ec679c9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 4%

---

# Bonnes pratiques {#best-practices}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

La création d’une application AEM Mobile On-demand Services est différente de la création d’une application qui s’exécute directement dans le shell Cordova (ou PhoneGap). Les développeurs doivent connaître :

* Modules externes pris en charge prêts à l’emploi, ainsi que les modules externes spécifiques à AEM Mobile.

>[!NOTE]
>
>Pour en savoir plus sur les modules externes, consultez les ressources suivantes :
>
>* [Utilisation des plug-ins Cordova dans AEM Mobile](https://helpx.adobe.com/digital-publishing-solution/help/cordova-api.html)
>* [Utilisation de modules externes activés pour Cordova spécifiques à AEM Mobile](https://helpx.adobe.com/digital-publishing-solution/help/app-runtime-api.html)

>



* Les modèles qui utilisent la fonctionnalité de module externe doivent être écrits de telle sorte qu’ils puissent toujours être créés dans le navigateur, sans que le pont de module externe soit présent.

   * Par exemple, veillez à attendre la fonction *deviceready* avant de tenter d’accéder à l’API d’un module externe.

## Instructions destinées aux développeurs AEM {#guidelines-for-aem-developers}

Les conseils suivants aideront les développeurs AEM expérimentés pour les sites qui souhaitent créer des modèles d’applications mobiles et des composants :

**Structuration AEM modèles de sites pour encourager la réutilisation et l’extensibilité**

* Préférer plusieurs fichiers de script de composant sur un seul fichier monolithique

   * Un certain nombre de points d’extension vides sont fournis, tels que *customheaderlibs.html* et *customfooterlibs.html*, qui permettent au développeur de modifier le modèle de page tout en dupliquant le moins de code de base possible.
   * Les modèles peuvent ensuite être étendus et personnalisés via le mécanisme *sling:resourceSuperType* de Sling

* Préférez Sightly/HTL par rapport à JSP comme langage de modèle.

   * Cette utilisation encourage une séparation du code avec les balises, offre une protection XSS intégrée et une syntaxe plus familière.

**Optimisation des performances sur l’appareil**

* Le script spécifique à l’article et les feuilles de style doivent être inclus dans la payload de l’article, à l’aide du modèle dps-article contentsync .
* Les feuilles de style et les scripts partagés par plusieurs articles doivent être inclus dans les ressources partagées, via le modèle contentsync dps-HTMLResources
* Ne référencez aucun script externe qui bloque le rendu

>[!NOTE]
>
>Vous pouvez en savoir plus sur les scripts externes de blocage de rendu [ici](https://developers.google.com/speed/docs/insights/BlockingJS).

**Préférez les bibliothèques JS et CSS côté client spécifiques à l’application par rapport aux bibliothèques spécifiques au web.**

* Pour éviter les frais généraux liés à des bibliothèques telles que jQuery Mobile afin de gérer un large éventail de périphériques et de navigateurs
* Lorsqu’un modèle s’exécute dans l’affichage Web d’une application, vous contrôlez les plateformes et versions que l’application va prendre en charge, ainsi que la connaissance de la prise en charge de JavaScript. Par exemple, préférez Ionic (peut-être uniquement CSS) à jQuery Mobile et l’interface utilisateur d’Onsen plutôt qu’à Bootstrap.

>[!NOTE]
>
>Pour en savoir plus sur jQuery mobile, cliquez [ici](https://jquerymobile.com/browser-support/1.4/).

**Préférez les microbibliothèques par rapport à la pile complète**

* Le temps nécessaire pour que votre contenu soit intégré à la vitrine de l’appareil sera ralenti par chaque bibliothèque dont dépendent vos articles. Ce ralentissement est aggravé lorsqu’une nouvelle vue web est utilisée pour effectuer le rendu de chaque article. Chaque bibliothèque doit donc être réinitialisée de zéro.
* Si vos articles ne sont pas créés comme SPA (applications d’une seule page), vous n’avez probablement pas besoin d’inclure une bibliothèque de pile complète comme Angular.
* Préférez des bibliothèques à fonction unique plus petites pour ajouter l’interactivité dont votre page a besoin, telle que [Fastclick](https://github.com/ftlabs/fastclick) ou [Velocity.js](https://velocityjs.org)

**Réduction de la taille de la charge utile d’article**

* Utilisez les plus petites ressources possibles pouvant couvrir efficacement la plus grande fenêtre d’affichage que vous prendrez en charge, à une résolution raisonnable.
* Utilisez un outil tel que *ImageOptim* sur vos images pour supprimer tout excès de métadonnées.

## Prise en main {#getting-ahead}

Pour en savoir plus sur les deux autres rôles et responsabilités, consultez les ressources ci-dessous :

* [Administrateur](/help/mobile/aem-mobile.md)
* [Création](/help/mobile/aem-mobile-on-demand.md)
