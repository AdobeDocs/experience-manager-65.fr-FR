---
title: Applications sur une seule page
seo-title: Applications sur une seule page
description: Consultez cette page pour en savoir plus sur les applications d’une seule page, c’est-à-dire que vous pouvez créer une application qui fonctionne de la même manière qu’une application de bureau ou mobile.
seo-description: Consultez cette page pour en savoir plus sur les applications d’une seule page, c’est-à-dire que vous pouvez créer une application qui fonctionne de la même manière qu’une application de bureau ou mobile.
uuid: d1865e79-6e7c-4149-95c0-556e61478b01
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: a5b5e40e-2457-45fe-9632-baf5008fe8bf
exl-id: daf7bf39-a105-46eb-ab7b-1c59484949e2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1015'
ht-degree: 3%

---

# Applications sur une seule page{#single-page-applications}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

[Les applications d’une seule page](https://en.wikipedia.org/wiki/Single-page_application)  (SPA) ont atteint une masse critique, largement considérée comme le modèle le plus efficace pour créer des expériences harmonieuses avec la technologie web. En suivant un modèle de SPA, vous pouvez créer une application qui fonctionne de la même manière qu’une application de bureau ou mobile, mais qui atteint une multitude de plateformes d’appareils et de facteurs de formulaire en raison de sa base dans les normes web ouvertes.

En règle générale, SPA semblent plus performants que les sites web basés sur des pages classiques, car ils chargent généralement une page HTML complète **une seule fois** (y compris CSS, JS et le contenu de police de prise en charge), puis chargent uniquement ce qui est nécessaire chaque fois qu’un changement d’état se produit dans l’application. Ce qui est nécessaire à ce changement d’état peut varier en fonction de l’ensemble de technologies choisi, mais inclut généralement un fragment HTML unique pour remplacer la &quot;vue&quot; existante, et l’exécution d’un bloc de code JS pour câbler la nouvelle vue et effectuer tout rendu de modèle côté client qui peut être nécessaire. La vitesse de ce changement d’état peut être encore améliorée en prenant en charge les mécanismes de mise en cache des modèles, ou même l’accès hors ligne au contenu des modèles si Adobe PhoneGap est utilisé.

AEM 6.1 prend en charge la création et la gestion de SPA par le biais d’Applications d’Adobe. Cet article présente les concepts sous-jacents à la SPA et explique comment ils exploitent [AngularJS](https://angularjs.org/) pour importer votre marque dans l’App Store et Google Play.

## SPA dans AEM applications {#spa-in-aem-apps}

La structure d’applications d’une seule page d’AEM Apps permet d’obtenir des performances élevées d’une application AngularJS, tout en permettant aux auteurs (ou à d’autres personnes non techniques) de créer et de gérer le contenu de l’application via l’environnement d’éditeur par glisser-déposer optimisé pour les écrans tactiles, traditionnellement réservé à la gestion des sites web. Un site a-t-il déjà été créé avec AEM ? Vous constaterez que la réutilisation de votre contenu, de vos composants, de vos workflows, de vos ressources et de vos autorisations est facile avec les applications AEM.

## Module d’application AngularJS {#angularjs-application-module}

AEM Apps gère une grande partie de la configuration AngularJS pour vous, y compris l’assemblage du module de niveau supérieur de votre application. Par défaut, ce module est nommé &quot;AEMAngularApp&quot; et le script responsable de sa génération se trouve (et est superposé) sur /libs/mobileapps/components/angular/ng-page/angular-app-module.js.jsp.

Une partie de l’initialisation de votre application implique de spécifier les modules AngularJS dont dépend l’application. La liste des modules utilisés par votre application est spécifiée par un script situé dans /libs/mobileapps/components/angular/ng-page/angular-module-list.js.jsp et peut être recouverte par le composant de page de vos applications afin d’extraire tout module AngularJS supplémentaire requis par votre application. Par exemple, comparez le script ci-dessus à l’implémentation de Geometrixx (située à l’adresse /apps/geometrixx-outdoors-app/components/angular/ng-geometrixx-page/angular-module-list.js.jsp).

Pour prendre en charge la navigation entre les états distincts de votre application, le script angular-app-module effectue une itération sur toutes les pages descendantes de la page de votre application de niveau supérieur afin de générer un ensemble d’&quot;itinéraires&quot; et de configurer chaque chemin sur le service $routeProvider de l’Angular. Pour un exemple de la manière dont cela se pratique, consultez le script angular-app-module généré par l’exemple d’application Geometrixx Outdoors : (Le lien nécessite une instance locale) [http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js](http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js)

En se connectant à AEMAngularApp généré, vous trouverez une série d’itinéraires spécifiés comme suit :

```xml
$routeProvider
.when('/content/phonegap/geometrixx-outdoors/en/home/products/:id', {
    templateUrl: 'home/products.template.html',
    controller: 'contentphonegapgeometrixxoutdoorsenhomeproducts'
})
```

L’exemple ci-dessus illustre un exemple de transmission d’un paramètre dans le cadre du chemin d’accès. Dans cet exemple, nous indiquons que lorsqu’un chemin qui correspond au modèle spécifié (/content/phonegap/geometrixx-outdoors/en/home/products/:id) est demandé, il doit être géré par le modèle home/products.template.html et utiliser le contrôleur &#39;contentphonegapgeometrixx-doorsendevoirs&#39;.

Le modèle à charger lorsque cet itinéraire est demandé est spécifié par la propriété templateUrl . Ce modèle contiendra le code HTML des composants d’AEM qui ont été inclus sur la page, ainsi que toute directive AngularJS nécessaire pour câbler le côté client de l’application. Pour obtenir un exemple de directive AngularJS dans un composant de Geometrixx, consultez la ligne 45 du template.jsp du carrousel de glissement (/apps/geometrixx-outdoors-app/components/swipe-carousel/template.jsp).

## Contrôleurs de page {#page-controllers}

Selon les propres termes de l’Angular, &quot;un contrôleur est une fonction constructeur JavaScript utilisée pour augmenter la portée de l’Angular.&quot; ([source](https://docs.angularjs.org/guide/controller)) Chaque page d’une application AEM est automatiquement connectée à un contrôleur qui peut être augmenté par n’importe quel contrôleur qui spécifie une `frameworkType` de `angular`. Prenez le composant ng-text comme exemple (/libs/mobileapps/components/angular/ng-text), y compris le noeud cq:template qui s’assure que chaque fois que ce composant est ajouté à une page, il inclut cette propriété importante.

Pour un exemple de contrôleur plus complexe, ouvrez le script ng-template-page controller.jsp (situé dans /apps/geometrixx-outdoors-app/components/angular/ng-template-page). Le code JavaScript généré lors de l’exécution est particulièrement intéressant, car il s’affiche comme suit :

```xml
// Controller for page 'products'
.controller('contentphonegapgeometrixxoutdoorsenhomeproducts', ['$scope', '$http', '$routeParams',
    function($scope, $http, $routeParams) {
        var sku = $routeParams.id;
        var productPath = '/' + sku.substring(0, 2) + '/' + sku.substring(0, 4) + '/' + sku;
        var data = $http.get('home/products' + productPath + '.angular.json' + cacheKiller);

        /* ng-product component controller (path: content-par/ng-product) */
        data.then(function(response) {
            $scope.contentparngproduct = response.data["content-par/ng-product"].items;
        });

        /* ng-image component controller (path: content-par/ng-product/ng-image) */
        data.then(function(response) {
            $scope.contentparngproductngimage = response.data["content-par/ng-product/ng-image"].items;
        });
    }
])
```

Dans l’exemple ci-dessus, vous remarquerez que nous prenons un paramètre du service `$routeParams`, puis nous le massons dans la structure de répertoires dans laquelle nos données JSON sont stockées. En gérant le SKU `id` de cette manière, nous sommes en mesure de fournir un modèle de produit unique qui peut générer les données de produit pour des milliers de produits distincts. Il s’agit d’un modèle beaucoup plus évolutif qui nécessite un itinéraire individuel pour chaque élément d’une base de données de produits (potentiellement) massive.

Deux éléments sont également à l’oeuvre ici : ng-product augmente la portée avec les données qu’il extrait de l’appel `$http` ci-dessus. Il existe également une image ng sur cette page qui, à son tour, augmente également la portée avec la valeur qu’elle récupère de la réponse. En vertu du service `$http` de l’Angular, chaque composant patiente jusqu’à ce que la demande soit terminée et que la promesse qu’il a créée soit remplie.

## Étapes suivantes {#the-next-steps}

Une fois que vous avez appris les applications d’une seule page, voir [Développement d’applications avec l’interface de ligne de commande PhoneGap](/help/mobile/phonegap-apps-pg-cli.md).
