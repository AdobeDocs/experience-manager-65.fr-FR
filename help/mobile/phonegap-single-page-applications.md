---
title: Applications sur une seule page
description: Consultez cette page pour en savoir plus sur les applications monopages. En d’autres termes, vous pouvez créer une application offrant des performances identiques à celles d’une application de bureau ou mobile.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: daf7bf39-a105-46eb-ab7b-1c59484949e2
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 0%

---

# Applications sur une seule page{#single-page-applications}

{{ue-over-mobile}}

[Applications d’une seule page](https://en.wikipedia.org/wiki/Single-page_application) (SPA) ont atteint leur masse critique, largement considérée comme le modèle le plus efficace pour créer des expériences transparentes avec la technologie web. En suivant un modèle SPA, vous pouvez créer une application dont les performances sont identiques à celles d’une application de bureau ou mobile, mais qui atteint une multitude de plateformes d’appareils et de formats en raison de sa base dans les normes web ouvertes.

En règle générale, les SPA semblent plus performants que les sites web traditionnels basés sur des pages, car ils chargent généralement une page d’HTML complète **une seule fois** (y compris des contenus CSS, JS et de polices de support), puis ne chargent que ce qui est nécessaire chaque fois qu’un changement d’état se produit dans l’application. Ce qui est nécessaire pour ce changement d’état peut varier en fonction de l’ensemble de technologies choisies, mais inclut généralement un fragment d’HTML unique pour remplacer la « vue » existante, et l’exécution d’un bloc de code JS pour câbler la nouvelle vue et effectuer tout rendu de modèle côté client qui pourrait être nécessaire. La vitesse de ce changement d’état peut être encore améliorée en prenant en charge les mécanismes de mise en cache des modèles, ou même l’accès hors ligne au contenu du modèle si Adobe PhoneGap est utilisé.

AEM 6.1 prend en charge la création et la gestion de SPA via les applications AEM. Cet article présente les concepts sous-jacents au SPA et la manière dont il utilise [AngularJS](https://angularjs.org/) pour importer votre marque dans App Store et Google Play.

## SPA dans les applications AEM {#spa-in-aem-apps}

La structure d’application d’une seule page dans les applications AEM permet d’obtenir des performances élevées de l’application AngularJS, tout en permettant aux auteurs (ou à tout autre personnel non technique) de créer et de gérer le contenu de l’application via l’environnement d’éditeur par glisser-déposer optimisé pour les écrans tactiles, qui était traditionnellement réservé à la gestion des sites web. Un site a-t-il déjà été créé avec AEM ? La réutilisation de votre contenu, de vos composants, de vos workflows, de vos ressources et de vos autorisations est simple grâce aux applications AEM.

## Module d’application AngularJS {#angularjs-application-module}

AEM Apps gère une grande partie de la configuration AngularJS pour vous, y compris l’assemblage du module de niveau supérieur de votre application. Par défaut, ce module est nommé « AEMAngularApp » et le script responsable de sa génération figure (et est recouvert) à l’adresse /libs/mobileapps/components/angular/ng-page/angular-app-module.js.jsp.

Une partie de l’initialisation de votre application consiste à spécifier les modules AngularJS dont dépend l’application. La liste des modules utilisés par votre application est spécifiée par un script situé à l’adresse /libs/mobileapps/components/angular/ng-page/angular-module-list.js.jsp et peut être recouverte par le composant de page de vos propres applications pour extraire tous les modules AngularJS supplémentaires dont votre application a besoin. À titre d’exemple, comparez le script ci-dessus à l’implémentation de Geometrixx (située à l’adresse /apps/geometrixx-outdoors-app/components/angular/ng-geometrixx-page/angular-module-list.js.jsp).

Pour prendre en charge la navigation entre les différents états de votre application, le script angular-app-module effectue une itération sur toutes les pages descendantes de votre page d’application de niveau supérieur afin de générer un ensemble d’« itinéraires » et configure chaque chemin d’accès sur le service $routeProvider d’Angular. Pour un exemple concret, consultez le script angular-app-module généré par l’exemple d’application Geometrixx Outdoors : (le lien nécessite une instance locale) [http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js](http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js)

En creusant dans l’AEMAngularApp générée, vous trouverez une série d’itinéraires spécifiés comme suit :

```xml
$routeProvider
.when('/content/phonegap/geometrixx-outdoors/en/home/products/:id', {
    templateUrl: 'home/products.template.html',
    controller: 'contentphonegapgeometrixxoutdoorsenhomeproducts'
})
```

L’exemple ci-dessus illustre en particulier un exemple de transmission d’un paramètre comme partie du chemin. Dans cet exemple, cela indique que lorsqu’un chemin d’accès qui répond au modèle spécifié (/content/phonegap/geometrixx-outdoors/en/home/products/:id) est demandé, il doit être géré par le modèle home/products.template.html et utiliser le contrôleur « contentphonegapgeometrixxoutdoorsenhomeproducts ».

Le modèle à charger lorsque cet itinéraire est demandé est spécifié par la propriété templateUrl . Ce modèle contient l’HTML des composants AEM qui ont été inclus dans la page, ainsi que toutes les directives AngularJS nécessaires pour câbler le côté client de l’application. Pour obtenir un exemple de directive AngularJS dans un composant de Geometrixx, consultez la ligne 45 du fichier template.jsp du carrousel de balayage (/apps/geometrixx-outdoors-app/components/swipe-carousel/template.jsp).

## Contrôleurs de page {#page-controllers}

Selon les propres termes d’Angular, « un contrôleur est une fonction constructeur JavaScript utilisée pour augmenter la portée de l’Angular ». ([source](https://docs.angularjs.org/guide/controller)) Chaque page d&#39;une application AEM est automatiquement connectée à un contrôleur qui peut être augmenté par n&#39;importe quel contrôleur qui spécifie un `frameworkType` de `angular`. Examinez le composant ng-text à titre d’exemple (/libs/mobileapps/components/angular/ng-text), en incluant le nœud cq:template qui s’assure que chaque fois que ce composant est ajouté à une page, il inclut cette propriété importante.

Pour obtenir un exemple de contrôleur plus complexe, ouvrez le script controler.jsp ng-template-page (dans /apps/geometrixx-outdoors-app/components/angular/ng-template-page). Le code JavaScript généré lors de l’exécution est particulièrement intéressant. Il se présente comme suit :

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

Dans l’exemple ci-dessus, le paramètre du service `$routeParams` est récupéré, puis transféré dans la structure de répertoires dans laquelle les données JSON sont stockées. En traitant le `id` de SKU de cette manière, vous êtes en mesure de fournir un modèle de produit unique qui peut effectuer le rendu des données de produit pour potentiellement des milliers de produits distincts. Il s’agit d’un modèle beaucoup plus évolutif qui nécessite un itinéraire individuel pour chaque article dans une base de données de produits (potentiellement) volumineuse.

Deux composants sont également à l’œuvre ici : ng-product augmente la portée avec les données qu’il extrait de l’appel de `$http` ci-dessus. Il existe également une image « ng » sur cette page qui, à son tour, augmente également la portée avec la valeur qu’elle récupère de la réponse. Grâce au service `$http` d&#39;Angular, chaque composant attend patiemment que la demande soit terminée et que la promesse qu&#39;il a créée soit remplie.

## Les étapes suivantes {#the-next-steps}

Une fois que vous en savez plus sur les applications sur une seule page, consultez [Développement d’applications avec l’interface de ligne de commande PhoneGap](/help/mobile/phonegap-apps-pg-cli.md).
