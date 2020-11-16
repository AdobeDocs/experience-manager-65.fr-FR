---
title: Structure d’une application
seo-title: Structure d’une application
description: Suivez cette page pour découvrir comment créer la structure d’une application. Cette page décrit comment structurer les modèles et les composants ainsi que les informations sur JavaScript et les bibliothèques clientes CSS.
seo-description: Suivez cette page pour découvrir comment créer la structure d’une application. Cette page décrit comment structurer les modèles et les composants ainsi que les informations sur JavaScript et les bibliothèques clientes CSS.
uuid: bf0e8b0c-a075-4847-b56d-de458715027c
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: c614a7ff-0d13-4407-bda0-c0a402a13dcd
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '973'
ht-degree: 2%

---


# Structure d’une application{#structure-an-app}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

Un projet AEM Mobile implique divers types de contenu, notamment des pages, des bibliothèques clientes JavaScript et CSS, des composants AEM réutilisables, des configurations Content Sync et le contenu du shell d&#39;application PhoneGap. Baser votre nouvelle application AEM Mobile sur le kit [de](https://github.com/Adobe-Marketing-Cloud-Apps/aem-phonegap-starter-kit) démarrage est un bon moyen d&#39;intégrer tous les types de contenu dans notre structure recommandée afin de faciliter à la fois la portabilité et la maintenance à long terme.

## Contenu de la page {#page-content}

Les pages de votre application doivent toutes se trouver sous /content/mobileapps pour être reconnues par la console AEM Mobile.

![chlimage_1-52](assets/chlimage_1-52.png)

Par AEM convention, la première page de votre application doit être une redirection vers l’un de ses enfants qui sert de langue par défaut de l’application (en dans les cas Geometrixx et Starter Kit). La page de paramètres régionaux de niveau supérieur hérite généralement du composant de page de démarrage de la base (/libs/mobileapps/components/splash-page) qui prend en charge l’initialisation nécessaire à l’installation des mises à jour de la synchronisation de contenu en direct (le code contentInit se trouve à l’adresse /etc/clientlibs/mobile/content-sync/js/contentInit.js).

## Modèles et composants {#templates-and-components}

Le modèle et le code de composant de votre application doivent se trouver dans /apps/&lt;nom de la marque>/&lt;nom de l’application>. Conformément à la convention, vous devez placer votre modèle et votre code de composant dans /apps/&lt;nom de la marque>/&lt;nom de l’application>. Ce modèle devrait être familier aux développeurs qui ont déjà travaillé avec Site en AEM. Il est généralement suivi car /apps/ est verrouillé par défaut sur l’accès anonyme sur les instances de publication. Par conséquent, votre code JSP brut est protégé des agresseurs potentiels.

Les modèles spécifiques à l’application peuvent être configurés pour être présentés uniquement en utilisant le noeud `allowedPaths` de propriété sur le modèle lui-même et en définissant sa valeur sur &#39;/content/mobileapps(/.&amp;ast;)?&#39; - ou même quelque chose de plus spécifique si le modèle ne doit être utilisable que pour une seule application. Les propriétés `allowedParents` et `allowedChildren` peuvent également être exploitées pour un contrôle affiné très précis sur les modèles qui seront disponibles pour un auteur en fonction de l&#39;endroit où la nouvelle page est créée.

Lors de la création d’un composant de page d’application à partir de zéro, il est recommandé de définir sa `sling:resourceSuperType` propriété sur &quot;mobileapps/components/angular/ng-page&quot;. Cette opération permet de configurer la page pour la création et le rendu en tant qu’application d’une seule page et d’incruster les fichiers .jsp que votre composant doit modifier. Comme ng-page n’inclut aucune structure d’interface utilisateur, un développeur finit généralement par superposer (au moins) &quot;template.jsp&quot; (superposé depuis /libs/mobileapps/components/angular/ng-page/template.jsp).

Les composants de page autorisés, qui souhaitent exploiter AngularJS, disposent d&#39;un `sling:resourceSuperType` composant équivalent situé dans /libs/mobileapps/components/angular/ng-component qui peut être superposé et personnalisé de la même manière.

## Clientlibs JavaScript et CSS {#javascript-and-css-clientlibs}

En ce qui concerne les bibliothèques clientes, le développeur dispose de quelques options pour les placer dans le référentiel. Le schéma suivant est proposé pour guider, mais n&#39;est pas une exigence difficile.

Si votre code client peut être autonome et ne correspond pas à un composant spécifique de votre application - ce qui signifie qu’il peut être réutilisé dans d’autres applications - nous vous recommandons de le stocker dans /etc/clientlibs/&lt;nom de la marque>/&lt;nom de la bibliothèque>. En revanche, si clientlib est spécifique à une seule application, vous pouvez l’imbriquer en tant qu’enfant du noeud de conception de votre application ; /etc/designs/phonegap/&lt;nom de la marque>/&lt;nom de l’application>/clientlibs. La catégorie de clientlib ne doit pas être utilisée par d&#39;autres libs et doit être utilisée pour incorporer d&#39;autres libs si nécessaire. En suivant ces modèles, le développeur n’a plus à ajouter de nouvelles configurations Content Sync chaque fois qu’une bibliothèque cliente est ajoutée à l’application, mais se contente de mettre à jour la propriété &quot;embeds&quot; de la bibliothèque cliente de l’application. Par exemple, jetez un oeil au noeud de configuration Content Sync Geometrixx clientlibs-all sous /content/phonegap/geometrixx-outdoors/fr/jcr:content/page-app/app-config/clientlibs-all.

Si votre code client est étroitement associé à un composant spécifique, placez ce code dans une bibliothèque cliente imbriquée sous l’emplacement du composant dans /apps/ et incorporez-le dans la catégorie clientlib &quot;design&quot; de votre application.

## PhoneGap Configuration {#phonegap-configuration}

Chaque application AEM Mobile contient un répertoire qui héberge les fichiers de configuration utilisés par l&#39;interface [de ligne de](https://github.com/phonegap/phonegap-cli) commande PhoneGap et la compilation [](https://build.phonegap.com/) PhoneGap pour transformer votre contenu Web en une application exécutable. Dans l’exemple de Geometrixx, par exemple, ce répertoire (/content/phonegap/geometrixx-outdoors/shell/jcr:content/page-app/app-content) fait partie de l’environnement Shell ; une décision de conception prise en raison du fait qu’elle contient uniquement du contenu qui ne peut pas être mis à jour en direct, comme des modules externes qui traitent des API de périphérique et de la configuration de l’application elle-même.

Dans ce répertoire, vous trouverez également un certain nombre de crochets [](https://cordova.apache.org/docs/en/edge/guide_appdev_hooks_index.md.html#Hooks%20Guide) Cordova qui peuvent être utilisés pour installer des modules externes, placer des fichiers de ressources dans leurs emplacements spécifiques à la plate-forme et d&#39;autres actions qui doivent être exécutées dans le cadre de la compilation. Remarque : au lieu de télécharger chaque module externe dans le cadre de la création, vous pouvez suivre le modèle de l’application Kitchen Sink et [inclure le code](https://github.com/blefebvre/aem-phonegap-kitchen-sink/tree/master/content/src/main/content/jcr_root/content/phonegap/kitchen-sink/shell/_jcr_content/pge-app/app-content/phonegap/plugins) source du module externe au reste de votre projet d’application.

## Étapes suivantes {#the-next-steps}

Une fois que vous avez pris connaissance de la structure de l’application, voir [Création et modification des applications à l’aide d’App Console](/help/mobile/phonegap-apps-console.md).
