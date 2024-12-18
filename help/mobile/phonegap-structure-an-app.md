---
title: Structure d’une application
description: Consultez cette page pour en savoir plus sur la création de la structure d’une application. Cette page décrit la structure des modèles et des composants, ainsi que des informations sur les bibliothèques clientes JavaScript et CSS.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: f37f239f-065b-44f8-acb1-93485b713b49
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '871'
ht-degree: 2%

---

# Structure d’une application{#structure-an-app}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur SPA pour les projets nécessitant un rendu côté client, basé sur un framework, pour une application à une seule page (comme React). [En savoir plus](/help/sites-developing/spa-overview.md).

Un projet AEM Mobile implique divers types de contenu, notamment des pages, des bibliothèques clientes JavaScript et CSS, des composants d’AEM réutilisables, des configurations de synchronisation de contenu et du contenu shell d’application PhoneGap. Baser votre nouvelle application AEM Mobile sur le [Starter Kit](https://github.com/Adobe-Marketing-Cloud-Apps/aem-phonegap-starter-kit) est un bon moyen d’intégrer tous les types de contenu différents dans notre structure recommandée afin de faciliter à la fois la portabilité et la maintenabilité à long terme.

## Contenu de la page {#page-content}

Les pages de votre application doivent toutes se trouver sous /content/mobileapps pour qu’elles soient reconnues par la console AEM Mobile.

![chlimage_1-52](assets/chlimage_1-52.png)

Par convention AEM, la première page de votre application doit être une redirection vers l’un de ses enfants qui sert de langue par défaut de l’application (&quot;en&quot; dans les cas de Geometrixx et de kit de démarrage). La page locale de niveau supérieur hérite généralement du composant &quot;splash-page&quot; de base (/libs/mobileapps/components/splash-page) qui prend en charge l’initialisation nécessaire pour prendre en charge l’installation des mises à jour de synchronisation de contenu en direct (le code contentInit se trouve à l’adresse /etc/clientlibs/mobile/content-sync/js/contentInit.js).

## Modèles et composants {#templates-and-components}

Le modèle et le code de composant de votre application doivent se trouver dans /apps/&lt;nom de la marque>/&lt;nom de l’application>. En conformité avec la convention, vous devez placer le modèle et le code du composant dans /apps/&lt;nom de la marque>/&lt;nom de l’application>. Ce modèle devrait être familier aux développeurs qui ont déjà travaillé avec Site dans AEM. Il est généralement suivi car /apps/ est verrouillé par défaut sur l’accès anonyme sur les instances de publication. Donc, votre code JSP brut est caché des attaquants potentiels.

Les modèles spécifiques à l’application peuvent être configurés pour être présentés uniquement en utilisant le noeud de propriété `allowedPaths` sur le modèle lui-même et en définissant sa valeur sur &#39;/content/mobileapps(/.&amp;ast;)?&#39; - ou même quelque chose de plus spécifique si le modèle ne doit être utilisable que pour une seule application. Les propriétés `allowedParents` et `allowedChildren` peuvent également être utilisées pour un contrôle affiné des modèles disponibles pour un auteur en fonction de l’emplacement de création de la page.

Lors de la création d’un composant de page d’application à partir de zéro, il est recommandé de définir sa propriété `sling:resourceSuperType` sur &quot;mobileapps/components/angular/ng-page&quot;. Cela permet de configurer votre page pour la création et le rendu sous la forme d’une application d’une seule page et de superposer les fichiers .jsp que votre composant peut avoir à modifier. Étant donné que ng-page n’inclut aucune structure d’interface utilisateur, un développeur finit généralement par superposer (au moins) &quot;template.jsp&quot; (superposé à partir de /libs/mobileapps/components/angular/ng-page/template.jsp).

Les composants de page autorisés, qui souhaitent utiliser AngularJS, disposent d’un composant `sling:resourceSuperType` équivalent dans /libs/mobileapps/components/angular/ng-component, qui peut être superposé et personnalisé de la même manière.

## Clientlibs JavaScript et CSS {#javascript-and-css-clientlibs}

Dans les bibliothèques clientes, le développeur dispose de quelques options permettant de les placer dans le référentiel. Le modèle suivant est proposé à titre indicatif, mais ce n&#39;est pas une exigence difficile.

Si votre code côté client peut être autonome et ne correspond pas à un composant spécifique de votre application (ce qui signifie qu’il peut être réutilisé dans d’autres applications), Adobe recommande de le stocker dans /etc/clientlibs/&lt;nom de la marque>/&lt;nom de la bibliothèque>. D’un autre côté, si la bibliothèque cliente est spécifique à une seule application, vous pouvez l’imbriquer en tant qu’enfant du noeud de conception de votre application : /etc/designs/phonegap/&lt;nom de marque>/&lt;nom de l’application>/clientlibs. N’utilisez pas la catégorie de cette bibliothèque cliente avec d’autres bibliothèques, mais incorporez d’autres bibliothèques si nécessaire. En suivant ce modèle, le développeur n’a plus à ajouter de nouvelles configurations de synchronisation de contenu chaque fois qu’une bibliothèque cliente est ajoutée à l’application, mais se contente de mettre à jour la propriété &quot;embeds&quot; de la bibliothèque cliente de conception de l’application. Par exemple, observez le noeud de configuration de synchronisation de contenu clientlibs-all à l’adresse /content/phonegap/geometrixx-outdoors/en/jcr:content/page-app/app-config/clientlibs-all.

Si votre code côté client est étroitement lié à un composant spécifique, placez ce code dans une bibliothèque cliente imbriquée sous l’emplacement du composant dans /apps/ et incorporez sa catégorie dans la bibliothèque cliente &quot;design&quot; de votre application.

## Configuration PhoneGap {#phonegap-configuration}

Chaque application AEM Mobile contient un répertoire qui héberge les fichiers de configuration utilisés par l’ [ interface de ligne de commande ](https://github.com/phonegap/phonegap-cli) PhoneGap et la version PhoneGap `https://build.phonegap.com/` pour transformer votre contenu web en application exécutable. Dans l’exemple de Geometrixx, par exemple, ce répertoire (/content/phonegap/geometrixx-outdoors/shell/jcr:content/page-app/app-content) fait partie du Shell. Une décision de conception est prise car elle contient uniquement du contenu qui ne peut pas être mis à jour en direct, comme des modules externes qui traitent des API de périphérique et de la configuration de l’application elle-même.

Dans ce répertoire, vous trouverez également quelques [hooks Cordova](https://cordova.apache.org/docs/en/dev/guide/appdev/hooks/index.html#Hooks%20Guide) qui peuvent être utilisés pour installer des modules externes, placer des fichiers de ressources dans leurs emplacements spécifiques à la plateforme et d’autres actions qui doivent être exécutées dans le cadre de la génération. Remarque : au lieu de télécharger chaque module externe dans le cadre de la version, vous pouvez suivre le modèle de l’application Kitchen Sink et inclure le code source du module externe <!-- THIS URL IS 404 (https://github.com/blefebvre/aem-phonegap-kitchen-sink/tree/master/content/src/main/content/jcr_root/content/phonegap/kitchen-sink/shell/_jcr_content/pge-app/app-content/phonegap/plugins) --> au reste de votre projet d’application.

## Les étapes suivantes {#the-next-steps}

Après avoir découvert la structure de l’application, voir [Création et modification des applications à l’aide de la console d’applications](/help/mobile/phonegap-apps-console.md).
