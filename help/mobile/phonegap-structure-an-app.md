---
title: Structure d’une application
description: Consultez cette page pour en savoir plus sur la création de la structure d’une application. Cette page décrit comment structurer les modèles et les composants, ainsi que des informations sur les bibliothèques clientes JavaScript et CSS.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: f37f239f-065b-44f8-acb1-93485b713b49
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '850'
ht-degree: 0%

---

# Structure d’une application{#structure-an-app}

{{ue-over-mobile}}

Un projet AEM Mobile implique un ensemble diversifié de types de contenu, notamment des pages, des bibliothèques clientes JavaScript et CSS, des composants AEM réutilisables, des configurations de synchronisation de contenu et du contenu de shell d’application PhoneGap. Baser votre nouvelle application AEM Mobile sur le [Starter Kit](https://github.com/Adobe-Marketing-Cloud-Apps/aem-phonegap-starter-kit) est un bon moyen d’intégrer tous les différents types de contenu dans la structure recommandée afin de faciliter la portabilité et la maintenabilité à long terme.

## Contenu de la page {#page-content}

Les pages de votre application doivent toutes se trouver sous /content/mobileapps pour être reconnues par la console AEM Mobile.

![chlimage_1-52](assets/chlimage_1-52.png)

Par convention AEM, la première page de votre application doit être une redirection vers l’un de ses enfants, qui correspond à la langue par défaut de l’application (en dans les cas de Geometrixx et de Starter Kit). La page de paramètres régionaux de niveau supérieur hérite généralement du composant « splash-page » de base (/libs/mobileapps/components/splash-page) qui s’occupe de l’initialisation nécessaire pour prendre en charge l’installation de mises à jour de synchronisation de contenu par voie hertzienne (le code contentInit se trouve à l’adresse /etc/clientlibs/mobile/content-sync/js/contentInit.js).

## Modèles et composants {#templates-and-components}

Le modèle et le code de composant de votre application doivent se trouver dans /apps/&lt;nom de marque>/&lt;nom de l’application>. Conformément à la convention, vous devez placer votre modèle et le code du composant dans /apps/&lt;nom de marque>/&lt;nom de l’application>. Ce modèle doit être familier aux développeurs qui ont déjà travaillé avec Site dans AEM. Elle est généralement suivie car /apps/ est verrouillé sur l’accès anonyme par défaut sur les instances de publication. Ainsi, votre code JSP brut est caché à des attaquant(e)s potentiel(le)s.

Les modèles spécifiques à une application peuvent être configurés pour n’être présentés qu’à l’aide du nœud de propriété `allowedPaths` sur le modèle lui-même et en définissant sa valeur sur « /content/mobileapps(/.&ast;)? - ou même quelque chose de plus spécifique si le modèle ne doit être utilisable que pour une seule application. Les propriétés `allowedParents` et `allowedChildren` peuvent également être utilisées pour un contrôle précis des modèles disponibles pour un auteur en fonction de l’emplacement de création de la page.

Lors de la création entièrement nouvelle d’un composant de page d’application, il est recommandé de définir sa propriété `sling:resourceSuperType` sur « mobileapps/components/angular/ng-page ». Cela configure votre page pour la création et le rendu en tant qu’application monopage et vous permet de superposer tous les fichiers .jsp que votre composant doit modifier. Comme ng-page n’inclut aucun framework d’interface utilisateur, un développeur finit généralement par recouvrir (au moins) « template.jsp » (recouvert à partir de /libs/mobileapps/components/angular/ng-page/template.jsp).

Les composants de page modifiables qui souhaitent utiliser AngularJS disposent d’un composant `sling:resourceSuperType` équivalent sous /libs/mobileapps/components/angular/ng-component, qui peut être superposé et personnalisé de la même manière.

## Bibliothèques clientes JavaScript et CSS {#javascript-and-css-clientlibs}

Dans les bibliothèques clientes, le développeur dispose de quelques options pour savoir où les placer dans le référentiel. Le modèle suivant est proposé à titre indicatif, mais n’est pas une exigence stricte.

Si votre code côté client peut être autonome et ne se rapporte pas à un composant spécifique de votre application (ce qui signifie qu’il peut être réutilisé dans d’autres applications), Adobe recommande de le stocker dans /etc/clientlibs/&lt;nom de marque>/&lt;nom de bibliothèque>. D’un autre côté, si la bibliothèque cliente est spécifique à une seule application, vous pouvez l’imbriquer en tant qu’enfant du nœud de conception de votre application : /etc/designs/phonegap/&lt;nom de marque>/&lt;nom de l’application>/clientlibs. N’utilisez pas la catégorie de cette bibliothèque cliente avec d’autres bibliothèques. Au lieu de cela, incorporez d’autres bibliothèques si nécessaire. Le fait de suivre ce modèle évite au développeur d’avoir à ajouter de nouvelles configurations de synchronisation de contenu chaque fois qu’une bibliothèque cliente est ajoutée à l’application, au lieu de simplement mettre à jour la propriété « embeds » de la bibliothèque cliente de conception de l’application. Geometrixx Par exemple, examinez le nœud de configuration de la synchronisation de contenu de clientlibs-all dans /content/phonegap/geometrixx-outdoors/en/jcr:content/page-app/app-config/clientlibs-all.

Si votre code côté client est étroitement associé à un composant spécifique, placez-le dans une bibliothèque cliente imbriquée sous l’emplacement du composant dans /apps/ et incorporez sa catégorie dans la bibliothèque cliente « conception » de votre application.

## Configuration de PhoneGap {#phonegap-configuration}

Chaque application AEM Mobile contient un répertoire qui héberge les fichiers de configuration utilisés par PhoneGap [interface de ligne de commande](https://github.com/phonegap/phonegap-cli) et PhoneGap build à `https://build.phonegap.com/` pour transformer votre contenu web en application exécutable. Dans l’exemple de Geometrixx, ce répertoire (/content/phonegap/geometrixx-outdoors/shell/jcr:content/pge-app/app-content) fait partie intégrante du shell. C’est une décision de conception, car il contient uniquement du contenu qui ne peut pas être mis à jour en direct, comme les plug-ins qui traitent des API d’appareil et de la configuration de l’application elle-même.

Dans ce répertoire, vous trouverez également quelques [hooks Cordova](https://cordova.apache.org/docs/en/dev/guide/appdev/hooks/index.html#Hooks%20Guide) qui peuvent être utilisés pour installer des modules externes, placer des fichiers de ressources à leur emplacement spécifique à la plateforme et effectuer d’autres actions qui doivent être exécutées dans le cadre de la version. Remarque : au lieu de télécharger chaque module externe dans le cadre de la création, vous pouvez suivre le modèle de l’application Kitchen Sink et inclure le code source du module externe<!-- THIS URL IS 404 (https://github.com/blefebvre/aem-phonegap-kitchen-sink/tree/master/content/src/main/content/jcr_root/content/phonegap/kitchen-sink/shell/_jcr_content/pge-app/app-content/phonegap/plugins) --> avec le reste de votre projet d’application.

## Les étapes suivantes {#the-next-steps}

Après avoir découvert la structure de l’application, reportez-vous à la section [Création et modification des applications à l’aide de la console d’applications](/help/mobile/phonegap-apps-console.md).
