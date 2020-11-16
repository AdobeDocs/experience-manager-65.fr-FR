---
title: Bonnes pratiques
seo-title: Bonnes pratiques
description: Suivez cette page pour découvrir les meilleures pratiques et les directives qui aideront les développeurs AEM expérimentés pour les sites qui souhaitent créer des modèles et des composants d’applications mobiles.
seo-description: Suivez cette page pour découvrir les meilleures pratiques et les directives qui aideront les développeurs AEM expérimentés pour les sites qui souhaitent créer des modèles et des composants d’applications mobiles.
uuid: 7733c8b1-a88c-455c-8080-f7add4205b92
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: a0647696-72c3-409b-85ba-9275d8f99cff
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 4%

---


# Bonnes pratiques {#best-practices}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

La création d&#39;une application AEM Mobile On-demand Services diffère de la création d&#39;une application qui s&#39;exécute directement dans le shell Cordova (ou PhoneGap). Les développeurs doivent connaître les points suivants :

* Plug-ins pris en charge en standard, ainsi que les plug-ins spécifiques à AEM Mobile.

>[!NOTE]
>
>Pour en savoir plus sur les modules externes, consultez les ressources suivantes :
>
>* [Utilisation des plug-ins Cordova en AEM Mobile](https://helpx.adobe.com/digital-publishing-solution/help/cordova-api.html)
>* [Utilisation de plug-ins activés pour Cordova spécifiques à AEM Mobile](https://helpx.adobe.com/digital-publishing-solution/help/app-runtime-api.html)

>



* Les modèles qui utilisent la fonctionnalité de module externe doivent être écrits de manière à ce qu’ils soient toujours autorisés dans le navigateur, sans que le pont de module externe soit présent.

   * Par exemple, veillez à attendre la fonction *deviceready* avant de tenter d’accéder à l’API d’un module externe.

## Conseils à l’intention des développeurs AEM {#guidelines-for-aem-developers}

Les recommandations suivantes s’adressent aux développeurs chevronnés AEM sites qui souhaitent créer des modèles et des composants d’applications mobiles :

**Structurer les modèles de sites AEM pour encourager la réutilisation et l&#39;extensibilité**

* Préférer plusieurs fichiers de script de composant sur un seul fichier monolithique

   * Un certain nombre de points d’extension vides sont fournis, tels que *customheaderlibs.html* et *customfooterlibs.html*, qui permettent au développeur de modifier le modèle de page tout en dupliquant le moins de code de base possible.
   * Les modèles peuvent ensuite être étendus et personnalisés via le mécanisme *sling:resourceSuperType* de Sling

* Préférer Sightly/HTL sur JSP en tant que langage de modèle

   * Cette méthode permet de séparer le code des balises, d’obtenir des offres intégrées à la protection XSS et d’utiliser une syntaxe plus familière.

**Optimiser les performances sur périphérique**

* Le script spécifique à l’article et les feuilles de style doivent être inclus dans la charge utile de l’article, à l’aide du modèle dps-article contentsync.
* Les feuilles de script et de style partagées par plusieurs articles doivent être incluses dans les ressources partagées, via le modèle contentsync dps-HTMLResources
* Ne référencez aucun script externe qui bloque le rendu.

>[!NOTE]
>
>Vous pouvez en savoir plus sur les scripts externes de blocage du rendu [ici](https://developers.google.com/speed/docs/insights/BlockingJS).

**Préférer les bibliothèques JS et CSS côté client spécifiques à l’application plutôt que celles spécifiques au Web**

* Pour éviter les frais généraux dans les bibliothèques telles que jQuery Mobile afin de gérer une vaste gamme de périphériques et de navigateurs
* Lorsqu’un modèle s’exécute dans la vue Web d’une application, vous avez le contrôle sur les plateformes et versions que l’application va prendre en charge, ainsi que sur la connaissance de la présence de la prise en charge de JavaScript. Par exemple, préférez Ionic (peut-être simplement CSS) à jQuery Mobile et l’interface utilisateur d’Onsen à Bootstrap.

>[!NOTE]
>
>Pour en savoir plus sur jQuery Mobile, cliquez [ici](https://jquerymobile.com/browser-support/1.4/).

**Préférer les micro-bibliothèques à la pile complète**

* Le temps nécessaire pour que votre contenu soit visible sur le périphérique sera ralenti par chaque bibliothèque dont dépendent vos articles. Ce ralentissement est aggravé lorsqu’une nouvelle vue Web est utilisée pour générer chaque article. Par conséquent, chaque bibliothèque doit être à nouveau initialisée à partir de zéro.
* Si vos articles ne sont pas créés en tant qu’SPA (applications d’une seule page), il n’est probablement pas nécessaire d’inclure une bibliothèque de piles complète, telle que Angular.
* Préférez des bibliothèques à fonction unique plus petites pour vous aider à ajouter l’interactivité dont votre page a besoin, telle que [Fastclick](https://github.com/ftlabs/fastclick) ou [Velocity.js.](https://velocityjs.org)

**Réduire la taille de la charge utile d’article**

* Utilisez les ressources les plus réduites possible qui peuvent efficacement couvrir la plus grande fenêtre d’affichage que vous allez prendre en charge, à une résolution raisonnable
* Utilisez un outil tel que *ImageOptim* sur vos images pour supprimer les métadonnées en excès.

## Pour avancer {#getting-ahead}

Pour en savoir plus sur les deux autres rôles et responsabilités, voir les ressources ci-dessous :

* [Administrateur](/help/mobile/aem-mobile.md)
* [Auteur](/help/mobile/aem-mobile-on-demand.md)
