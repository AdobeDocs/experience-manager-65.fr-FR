---
title: Applications sur une seule page (SPA)
seo-title: Applications sur une seule page (SPA)
description: Suivez cette page pour en savoir plus sur les applications d’une seule page, c’est-à-dire que vous pouvez créer une application qui fonctionne de la même manière qu’une application de bureau ou mobile.
seo-description: Suivez cette page pour en savoir plus sur les applications d’une seule page, c’est-à-dire que vous pouvez créer une application qui fonctionne de la même manière qu’une application de bureau ou mobile.
uuid: d1865e79-6e7c-4149-95c0-556e61478b01
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: a5b5e40e-2457-45fe-9632-baf5008fe8bf
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Applications sur une seule page (SPA){#single-page-applications}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

[Les applications](https://en.wikipedia.org/wiki/Single-page_application) monopages (SPA) ont atteint une masse critique, largement considérée comme le modèle le plus efficace pour créer des expériences homogènes avec la technologie Web. En suivant un modèle d’application d’une seule page, vous pouvez créer une application qui fonctionne de la même manière qu’une application de bureau ou mobile, mais qui atteint une multitude de plates-formes de périphériques et de facteurs de formulaire en raison de sa création dans les normes Web ouvertes.

En règle générale, les applications monopages (SPA) sont plus performantes que les sites Web traditionnels reposant sur des pages, car elles ne chargent généralement une page HTML complète qu’une seule fois **** (y compris CSS, JS et le contenu des polices de prise en charge), puis ne chargent que ce qui est nécessaire chaque fois qu’un changement d’état se produit dans l’application. Les éléments nécessaires à ce changement d’état peuvent varier en fonction de l’ensemble de technologies choisi, mais incluent généralement un fragment HTML unique pour remplacer la vue existante, ainsi que l’exécution d’un bloc de code JS pour câbler la nouvelle vue et effectuer le rendu de modèle côté client qui peut être nécessaire. La vitesse de ce changement d’état peut être encore améliorée en prenant en charge les mécanismes de mise en cache des modèles ou même l’accès hors ligne au contenu des modèles si Adobe PhoneGap est utilisé.

AEM 6.1 prend en charge la création et la gestion des applications monopages via les applications AEM. Cet article présente les concepts qui sous-tendent l’application d’une seule page et explique comment ils utilisent [AngularJS](https://angularjs.org/) pour amener votre marque sur l’App Store et Google Play.

## Application d’une seule page dans les applications AEM {#spa-in-aem-apps}

La structure des applications d’une seule page des applications AEM permet d’obtenir des performances élevées d’une application AngularJS, tout en permettant aux auteurs (ou à d’autres personnes non techniques) de créer et de gérer le contenu de l’application via l’environnement d’éditeur optimisé pour les écrans tactiles, par glisser-déposer, traditionnellement réservé à la gestion des sites Web. Vous avez déjà créé un site avec AEM ? Vous constaterez que la réutilisation de votre contenu, de vos composants, de vos processus, de vos ressources et de vos autorisations est facile avec les applications AEM.

## Module d’application AngularJS {#angularjs-application-module}

Les applications AEM gèrent une grande partie de la configuration AngularJS pour vous, y compris la création du module de niveau supérieur de votre application. Par défaut, ce module est nommé &quot;AEMAngularApp&quot; et le script responsable de sa génération se trouve (et est superposé) dans /libs/mobileapps/components/angular/ng-page/angular-app-module.js.jsp.

Une partie de l’initialisation de votre application implique de spécifier les modules AngularJS dont dépend l’application. La liste des modules utilisés par votre application est spécifiée par un script situé dans /libs/mobileapps/components/angular/ng-page/angular-module-list.js.jsp et peut être superposée par le composant de page de vos propres applications pour extraire tout module AngularJS supplémentaire requis par votre application. Par exemple, comparez le script ci-dessus à l’implémentation de Geometrixx (situé dans /apps/geometrixx-outdoors-app/components/angular/ng-geometrixx-page/angular-module-list.js.jsp).

Pour prendre en charge la navigation entre les différents états de votre application, le script angulaire-app-module effectue une itération sur toutes les pages descendantes de votre page d’application de niveau supérieur afin de générer un ensemble de &quot;routes&quot; et de configurer chaque chemin sur le service $routeProvider d’Angular. Pour un exemple de la manière dont cela se présente dans la pratique, examinez le script angulaire-app-module généré par l’exemple d’application Geometrixx Outdoors : (le lien nécessite une instance locale) [http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js](http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js)

En vous connectant à AEMAngularApp généré, vous trouverez une série d&#39;itinéraires spécifiés comme suit :

```xml
$routeProvider
.when('/content/phonegap/geometrixx-outdoors/en/home/products/:id', {
    templateUrl: 'home/products.template.html',
    controller: 'contentphonegapgeometrixxoutdoorsenhomeproducts'
})
```

L’exemple ci-dessus illustre un exemple de transmission d’un paramètre dans le cadre du chemin d’accès. Dans cet exemple, nous indiquons que lorsqu’un chemin qui correspond au modèle spécifié (/content/phonegap/geometrixx-outdoors/fr/home/products/:id) est demandé, il doit être géré par le modèle home/products.template.html et utiliser le contrôleur &quot;contentphonegapgeometrixx-doorsendevoirs&quot;.

Le modèle à charger lorsque cette route est demandée est spécifié par la propriété templateUrl. Ce modèle contiendra le code HTML des composants AEM inclus dans la page, ainsi que toutes les directives AngularJS nécessaires au câblage du côté client de l’application. Pour un exemple de directive AngularJS dans un composant Geometrixx, examinez la ligne 45 du fichier template.jsp du carrousel de glissement (/apps/geometrixx-outdoors-app/components/swipe-carousel/template.jsp).

## Contrôleurs de page {#page-controllers}

Selon les propres mots d&#39;Angular, &quot;un contrôleur est une fonction constructeur JavaScript utilisée pour augmenter l&#39;étendue angulaire.&quot; ([source](https://docs.angularjs.org/guide/controller)) Chaque page d’une application AEM est automatiquement câblée vers un contrôleur qui peut être augmenté par n’importe quel contrôleur qui spécifie un `frameworkType` nombre de `angular`. Examinez le composant ng-text comme exemple (/libs/mobileapps/components/angular/ng-text), y compris le noeud cq:template qui s&#39;assure que chaque fois que ce composant est ajouté à une page, il inclut cette propriété importante.

Pour un exemple de contrôleur plus complexe, ouvrez le script ng-template-page contrôleur.jsp (situé dans /apps/geometrixx-outdoors-app/components/angular/ng-template-page). Le code javascript généré lors de l’exécution est particulièrement intéressant, ce qui génère le rendu suivant :

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

Dans l’exemple ci-dessus, vous noterez que nous prenons un paramètre du `$routeParams` service, puis nous le massons dans la structure de répertoires dans laquelle sont stockées nos données JSON. En traitant le sku `id` de cette manière, nous sommes en mesure de fournir un modèle de produit unique qui peut générer les données de produit pour des milliers de produits distincts. Il s&#39;agit d&#39;un modèle beaucoup plus évolutif qui nécessite un itinéraire individuel pour chaque élément d&#39;une base de données de produits (potentiellement) massive.

Il y a aussi deux éléments à l&#39;oeuvre ici : ng-product augmente la portée avec les données qu&#39;il extrait de l&#39; `$http` appel ci-dessus. Il y a aussi une ng-image sur cette page qui à son tour augmente la portée avec la valeur qu&#39;elle récupère de la réponse. En vertu du `$http` service d&#39;Angular, chaque composant attendra patiemment jusqu&#39;à ce que la demande soit terminée et que la promesse qu&#39;il a créée soit remplie.

## Étapes suivantes {#the-next-steps}

Une fois que vous avez appris les applications d’une seule page, voir [Développement d’applications avec l’interface de ligne de commande PhoneGap](/help/mobile/phonegap-apps-pg-cli.md).
