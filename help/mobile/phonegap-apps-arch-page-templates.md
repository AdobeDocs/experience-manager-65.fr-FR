---
title: Modèles de page de contenu pour les applications mobiles
description: Consultez cette page pour en savoir plus sur les modèles de page pour les applications mobiles.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: 7f00d426-4d28-41ee-8c54-636349e48669
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '2548'
ht-degree: 0%

---

# Modèles de page pour les applications mobiles {#page-templates-for-mobile-apps}

{{ue-over-mobile}}

## Modèles de page pour les applications mobiles {#page-templates-for-mobile-apps-1}

Les composants de page que vous créez pour votre application sont basés sur le composant /libs/mobileapps/components/angular/ng-page ([ouverture dans le CRXDE Lite sur un serveur local](http://localhost:4502/crx/de/index.jsp#/libs/mobileapps/components/angular/ng-page)). Ce composant contient les scripts JSP suivants, que votre composant hérite ou remplace :

* ng-page.jsp
* head.jsp
* body.jsp
* angular-app-module.js.jsp
* angular-route-fragment.js.jsp
* angular-app-controllers.js.jsp
* controller.js.jsp
* template.jsp
* angular-module-list.js.jsp
* header.jsp
* footer.jsp
* js_clientlibs.jsp
* css_clientlibs.jsp

### ng-page.jsp {#ng-page-jsp}

Détermine le nom de l’application à l’aide de la propriété `applicationName` et l’expose via pageContext.

Inclut head.jsp et body.jsp.

### head.jsp {#head-jsp}

Écrit l’élément `<head>` de la page de l’application.

Si vous souhaitez remplacer la propriété meta de la fenêtre d’affichage de l’application, il s’agit du fichier que vous remplacez.

Conformément aux bonnes pratiques, l’application inclut la partie css des bibliothèques clientes dans la tête, tandis que le JS est inclus dans l’élément de fermeture &lt; `body>`.

### body.jsp {#body-jsp}

Le corps d’une page d’Angular est rendu différemment selon que wcmMode est détecté (!)= WCMMode.DISABLED) pour déterminer si la page est ouverte pour la création ou en tant que page publiée.

**Mode création**

En mode de création, chaque page est rendue séparément. Angular ne gère pas le routage entre les pages et n’est pas non plus utilisé pour charger un modèle partiel contenant les composants de la page. Au lieu de cela, le contenu du modèle de page (template.jsp) est inclus côté serveur via la balise `cq:include`.

Cette stratégie permet aux fonctions de création (par exemple, l’ajout et la modification de composants dans le système de paragraphes, le Sidekick, le mode de conception, etc.) de fonctionner sans modification. Les pages qui reposent sur un rendu côté client, comme celles des applications, ne fonctionnent pas correctement en mode de création AEM.

L’inclusion template.jsp est encapsulée dans un élément `div` contenant la directive `ng-controller`. Cette structure permet de lier les contenus DOM au contrôleur. Par conséquent, bien que les pages qui s’affichent du côté client échouent, les composants individuels qui le font fonctionnent correctement (voir la section sur les composants ci-dessous).

```xml
<div ng-controller="<c:out value="${controllerNameStripped}"/>">
      <cq:include script="template.jsp"/>
</div>
```

**Mode Publish**

En mode de publication (par exemple, lorsque l’application est exportée à l’aide de la synchronisation du contenu), toutes les pages deviennent une application d’une seule page (SPA). (Pour en savoir plus sur SPA, suivez le tutoriel sur l’Angular, en particulier [https://docs.angularjs.org/tutorial/step_07](https://docs.angularjs.org/tutorial/step_07).)

Il n’existe qu’une seule page d’HTML dans un SPA (une page qui contient l’élément `<html>`). Cette page est appelée « modèle de mise en page ». Dans la terminologie de l’Angular, il s’agit de « ...un modèle commun à toutes les vues de notre application ». Considérez cette page comme la « page d’application de niveau supérieur ». Par convention, la page d’application de niveau supérieur est le nœud de `cq:Page` de votre application le plus proche de la racine (et n’est pas une redirection).

Comme l’URI réel de votre application ne change pas en mode de publication, les références aux ressources externes de cette page doivent utiliser des chemins d’accès relatifs. Par conséquent, un composant d’image spécial est fourni, qui prend en compte cette page de niveau supérieur lors du rendu d’images pour l’exportation.

En tant que SPA, cette page de modèle de mise en page génère simplement un élément div avec une directive ng-view.

```xml
 <div ng-view ng-class="transition"></div>
```

Le service d’itinéraire d’Angular utilise cet élément pour afficher le contenu de chaque page de l’application, y compris le contenu modifiable de la page active (contenu dans template.jsp).

Le fichier body.jsp contient les fichiers header.jsp et footer.jsp vides. Si vous souhaitez fournir du contenu statique sur chaque page, vous pouvez remplacer ces scripts dans votre application.

Enfin, les bibliothèques clientes JavaScript sont incluses au bas de l’élément &lt;body>, y compris deux fichiers JS spéciaux générés sur le serveur : *&lt;nom de page>*.angular-app-module.js et *&lt;nom de page>*.angular-app-controllers.js.

### angular-app-module.js.jsp {#angular-app-module-js-jsp}

Ce script définit le module d’Angular de l’application. La sortie de ce script est liée au balisage que le reste du composant du modèle génère via l’élément `html` dans ng-page.jsp qui contient l’attribut suivant :

```xml
ng-app="<c:out value='${applicationName}'/>"
```

Cet attribut indique à l’Angular que le contenu de cet élément DOM doit être lié au module suivant. Ce module relie les vues (dans AEM, il s’agirait de ressources cq:Page) aux contrôleurs correspondants.

Ce module définit également un contrôleur de niveau supérieur nommé `AppController` qui expose la variable `wcmMode` à la portée et configure l’URI à partir duquel récupérer les payloads de la mise à jour de synchronisation de contenu.

Enfin, ce module effectue une itération sur chaque page descendante (y compris lui-même) et effectue le rendu du contenu du fragment d’itinéraire de chaque page (via le sélecteur et l’extension angular-route-fragment.js ), y compris celui-ci en tant qu’entrée de configuration pour $routeProvider d’Angular. En d’autres termes, $routeProvider indique à l’application le contenu à rendre lorsqu’un chemin d’accès donné est demandé.

### angular-route-fragment.js.jsp {#angular-route-fragment-js-jsp}

Ce script génère un fragment de JavaScript qui doit se présenter comme suit :

```
.when('/<path>', {
    templateUrl: '<path to template>',
    controller: '<controller name>'
})
```

Ce code indique à $routeProvider (défini dans angular-app-module.js.jsp) que &#39;/&lt;path>&#39; doit être géré par la ressource à l’adresse `templateUrl`, et câblé par `controller` (ce que nous allons voir ensuite).

Si nécessaire, vous pouvez remplacer ce script pour gérer des chemins plus complexes, y compris ceux contenant des variables. Vous pouvez en voir un exemple dans le script /apps/weretail-app/components/angular/ng-template-page/angular-route-fragment.js.jsp installé avec AEM :

```xml
// note the :id suffix on the path
.when('<c:out value="${resource.path}"/>/:id', {
    templateUrl: '<c:out value="${relativeResourcePath}"/>.template.html',
    controller: '<c:out value="${controllerNameStripped}"/>'
})
```

### angular-app-controllers.js.jsp {#angular-app-controllers-js-jsp}

En Angular, les contrôleurs connectent des variables dans la $scope, les exposant à la vue. Le script angular-app-controllers.js.jsp suit le modèle illustré par angular-app-module.js.jsp dans la mesure où il itère à travers chaque page descendante (y compris lui-même) et génère le fragment de contrôleur que chaque page définit (via controller.js.jsp). Le module qu’il définit est appelé `cqAppControllers` et doit être répertorié comme une dépendance du module d’application de niveau supérieur afin que les contrôleurs de page soient disponibles.

### controller.js.jsp {#controller-js-jsp}

Le script controller.js.jsp génère le fragment de contrôleur pour chaque page. Ce fragment de contrôleur se présente comme suit :

```
.controller('<c:out value="${controllerNameStripped}"/>', ['$scope', '$http',
    function($scope, $http) {
        var data = $http.get('<c:out value="${relativeResourcePath}"/>.angular.json' + cacheKiller);

        // component fragments which consume the contents of `data` go here
    }
])
```

La variable `data` se voit attribuer la promesse renvoyée par la méthode de `$http.get` d’Angular. Chaque composant inclus dans cette page peut, si vous le souhaitez, rendre du contenu .json disponible (via son script angular.json.jsp) et agir sur le contenu de cette requête lorsqu’elle est résolue. La requête est très rapide sur les appareils mobiles, car elle accède simplement au système de fichiers.

Pour qu’un composant fasse partie du contrôleur de cette manière, il doit étendre le composant /libs/mobileapps/components/angular/ng-component et inclure la propriété `frameworkType: angular`.

### template.jsp {#template-jsp}

Présenté pour la première fois dans la section body.jsp, template.jsp contient simplement le système de paragraphes (parsys) de la page. En mode de publication, ce contenu est référencé directement (à l’adresse &lt;page-path>.template.html) et chargé dans le SPA via le templateUrl configuré sur le $routeProvider.

Le système de paragraphes (parsys) de ce script peut être configuré pour accepter n’importe quel type de composant. Cependant, vous devez faire attention lorsque vous traitez des composants créés pour un site web traditionnel (par opposition à un SPA). Par exemple, le composant d’image de base ne fonctionne correctement que sur la page d’application de niveau supérieur, car il n’est pas conçu pour référencer les ressources qui se trouvent dans une application.

### angular-module-list.js.jsp {#angular-module-list-js-jsp}

Ce script génère simplement les dépendances d’Angular du module d’application d’Angular de niveau supérieur. Il est référencé par angular-app-module.js.jsp.

### header.jsp {#header-jsp}

Un script pour placer le contenu statique en haut de l’application. Ce contenu est inclus par la page de niveau supérieur, en dehors de la portée de ng-view.

### footer.jsp {#footer-jsp}

Un script pour placer le contenu statique en bas de l’application. Ce contenu est inclus par la page de niveau supérieur, en dehors de la portée de ng-view.

### js_clientlibs.jsp {#js-clientlibs-jsp}

Remplacez ce script pour inclure vos bibliothèques clientes JavaScript.

### css_clientlibs.jsp {#css-clientlibs-jsp}

Remplacez ce script pour inclure vos bibliothèques clientes CSS.

## Composants d’application {#app-components}

Les composants d’application doivent non seulement fonctionner sur une instance AEM (publication ou création), mais également lorsque le contenu de l’application est exporté vers le système de fichiers via la synchronisation de contenu. Le composant doit donc présenter les caractéristiques suivantes :

* Toutes les ressources, tous les modèles et tous les scripts d’une application PhoneGap doivent être référencés de manière relative.
* La gestion des liens diffère si l’instance AEM fonctionne en mode de création ou de publication.

### Assets relative {#relative-assets}

L’URI d’une ressource donnée dans une application PhoneGap diffère non seulement par plateforme, mais est unique pour chaque installation de l’application. Par exemple, notez l’URI suivant d’une application s’exécutant dans le simulateur iOS :

`file:///Users/userId/Library/Application%20Support/iPhone%20Simulator/7.0.3/Applications/24BA22ED-7D06-4330-B7EB-F6FC73251CA3/Library/files/www/content/phonegap/weretail/apps/ng-we-retail/en/home.html`

Notez le GUID « 24BA22ED-7D06-4330-B7EB-F6FC73251CA3 » dans le chemin .

En tant que développeur PhoneGap, le contenu qui vous intéresse se trouve sous le répertoire www. Pour accéder aux ressources de l’application, utilisez des chemins d’accès relatifs.

Pour aggraver le problème, votre application PhoneGap utilise le modèle d’application sur une seule page (SPA) afin que l’URI de base (à l’exclusion du hachage) ne change jamais. Par conséquent, chaque ressource, modèle ou script que vous référencez **doit être relatif à votre page de niveau supérieur. &#x200B;** La page de niveau supérieur initialise le routage et les contrôleurs d’Angular grâce à `<name>.angular-app-module.js` et `<name>.angular-app-controllers.js`. Cette page doit être la page la plus proche de la racine du référentiel qui *n’étend pas* un sling:redirect.

Plusieurs méthodes d’assistance sont disponibles pour gérer les chemins relatifs :

* FrameworkContentExporterUtils.getTopLevelAppResource
* FrameworkContentExporterUtils.getRelativePathToRootLevel
* FrameworkContentExporterUtils.getPathToAsset

Pour consulter des exemples d’utilisation, ouvrez la source mobileapps située sous /libs/mobileapps/components/angular.

### Liens {#links}

Les liens doivent utiliser la fonction `ng-click="go('/path')"` pour prendre en charge tous les modes de gestion de contenu web. Cette fonction dépend de la valeur d’une variable de portée pour déterminer correctement l’action du lien :

```xml
<c:choose><c:when test="${wcmMode}">
    <%-- WCMMode is enabled - page is being rendered in AEM --%>
    $scope.wcmMode = true;
</c:when><c:otherwise>
    <%-- WCMMode is disabled --%>
    $scope.wcmMode = false;
</c:otherwise></c:choose>
```

Lorsque nous `$scope.wcmMode == true`, nous gérons chaque événement de navigation de manière habituelle, de sorte que le résultat est une modification du chemin d’accès et/ou de la partie page de l’URL.

Si `$scope.wcmMode == false`, chaque événement de navigation entraîne une modification de la partie hachage de l’URL qui est résolue en interne par le module ngRoute d’Angular.

### Détails du script de composant {#component-script-details}

![chlimage_1-51](assets/chlimage_1-51.png)

### ng-component.jsp {#ng-component-jsp}

Ce script affiche le contenu du composant ou un espace réservé approprié lorsque le mode d’édition est détecté.

### template.jsp {#template-jsp-1}

Le script template.jsp effectue le rendu des balises du composant. Si le composant en question est piloté par des données JSON extraites d’AEM (par exemple « ng-text » : /libs/mobileapps/components/angular/ng-text/template.jsp), ce script est alors chargé de câbler le balisage avec les données exposées par la portée du contrôleur de la page.

Cependant, les exigences de performances imposent parfois d’ne pas effectuer de création de modèles côté client (ou liaison de données). Dans ce cas, il vous suffit d’effectuer le rendu du balisage du composant côté serveur, et il est inclus dans le contenu du modèle de page.

### overhead.jsp {#overhead-jsp}

Dans les composants pilotés par des données JSON (tels que &#39;ng-text&#39; : /libs/mobileapps/components/angular/ng-text), overhead.jsp peut être utilisé pour supprimer tout le code Java de template.jsp. Il est ensuite référencé à partir de template.jsp et toutes les variables qu’il expose sur la requête peuvent être utilisées. Cette stratégie encourage la séparation de la logique de la présentation et limite la quantité de code qui doit être copié et collé lorsqu’un nouveau composant est dérivé d’un composant existant.

### controller.js.jsp {#controller-js-jsp-1}

Comme décrit dans [Modèles de page AEM](/help/mobile/apps-architecture.md), chaque composant peut générer un fragment JavaScript pour utiliser le contenu JSON exposé par la promesse `data`. Conformément aux conventions d&#39;Angular, un contrôleur ne doit être utilisé que pour affecter des variables à la portée.

### angular.json.jsp {#angular-json-jsp}

Ce script est inclus sous forme de fragment dans le fichier « &lt;page-name>.angular.json » à l’échelle de la page qui est exporté pour chaque page qui étend ng-page. Dans ce fichier, le développeur de composants peut exposer toute structure JSON dont le composant a besoin. Dans l’exemple « ng-text », cette structure inclut simplement le contenu textuel du composant, et un indicateur indiquant si le composant inclut ou non du texte enrichi.

Le composant de produit d’application We.Retail est un exemple plus complexe (/apps/weretail-app/components/angular/ng-product) :

```xml
{
    "content-par/ng-product": {
        "items": [{
            "name": "Cajamara",
            "description": "Bike",
            "summaryHTML": "",
            "price": "$610.00",
            "SKU": "eqsmcj",
            "numberOfLikes": "0",
            "numberOfComments": "0"
        }]
    },
    "content-par/ng-product/ng-image": {
        "items": [{
            "hasContent": true,
            "imgSrc": "home/products/eq/eqsm/eqsmcj/jcr_content/content-par/ng-product/ng-image.img.jpg/1377771306985.jpg",
            "description": "",
            "alt": "Cajamara",
            "title": "Cajamara",
            "hasLink": false,
            "linkPath": "",
            "attributes": [{
                "attributeName": "class",
                "attributeValue": "cq-dd-image"
            }]
        }]
    }
}
```

## Contenu de l’interface de ligne de commande Téléchargement Assets {#contents-of-the-cli-assets-download}

Téléchargez les ressources de l’interface de ligne de commande à partir de la console Applications afin de les optimiser pour une plateforme spécifique, puis créez l’application à l’aide de l’API d’intégration de ligne de commande PhoneGap. Le contenu du fichier ZIP que vous enregistrez sur le système de fichiers local présente la structure suivante :

```xml
.cordova/
  |- hooks/
     |- after_prepare/
     |- before_platform_add/
     |- Other Hooks
plugins/
www/
  |- config.xml
  |- index.html
  |- res/
  |- etc/
  |- apps/
  |- content/
  |- package.json
  |- package-update.json
```

### .cordova {#cordova}

Il s’agit d’un répertoire masqué que vous ne verrez peut-être pas en fonction des paramètres actuels du système d’exploitation. Vous devez configurer votre système d’exploitation de sorte que ce répertoire soit visible si vous envisagez de modifier les hooks d’application qu’il contient.

### .cordova/hooks/ {#cordova-hooks}

Ce répertoire contient les points d’extension [CLI](https://gist.github.com/jlcarvalho/22402d013bc72f795d45a01836ce735c). Les dossiers du répertoire hooks contiennent des scripts node.js exécutés à des moments précis de la génération.

### .cordova/hooks/after-platform_add/ {#cordova-hooks-after-platform-add}

Le répertoire after-platform_add contient le fichier `copy_AMS_Conifg.js`. Ce script copie un fichier de configuration pour prendre en charge la collecte d’analyses Mobile Services d’Adobe.

### .cordova/hooks/after-preparation/ {#cordova-hooks-after-prepare}

Le répertoire de post-préparation contient le fichier `copy_resource_files.js`. Ce script copie plusieurs images d’icône et d’écran de démarrage à des emplacements spécifiques à la plateforme.

### .cordova/hooks/before_platform_add/ {#cordova-hooks-before-platform-add}

Le répertoire before_platform_add contient le fichier `install_plugins.js`. Ce script effectue une itération sur une liste d’identifiants de plug-in Cordova, en installant ceux qui, selon lui, ne sont pas déjà disponibles.

Cette stratégie ne nécessite pas de regrouper et d’installer les modules externes sur AEM chaque fois que la commande Maven `content-package:install` est exécutée. La stratégie alternative de vérification des fichiers dans votre système SCM nécessite des activités de regroupement et d’installation répétitives.

### .cordova/hooks/Other Hooks {#cordova-hooks-other-hooks}

Ajoutez d’autres points d’extension, au besoin. Les hooks suivants sont disponibles (tels que fournis par l’exemple d’application Hello World de Phonegap) :

* after_build
* before_build
* after_compile
* before_compile
* after_docs
* before_docs
* after_emulate
* before_emulate
* after_platform_add
* before_platform_add
* after_platform_ls
* before_platform_ls
* after_platform_rm
* before_platform_rm
* after_plugin_add
* before_plugin_add
* after_plugin_ls
* before_plugin_ls
* after_plugin_rm
* before_plugin_rm
* after_preparation
* before_preparation
* after_run
* before_run

### plateformes/ {#platforms}

Ce répertoire est vide jusqu&#39;à ce que vous exécutiez la commande `phonegap run *<platform>*` sur le projet. Actuellement, `*<platform>*` peut être `ios` ou `android`.

Après avoir créé l’application pour une plateforme spécifique, le répertoire correspondant est créé et il contient le code de l’application spécifique à la plateforme.

### plugins/ {#plugins}

Le répertoire des modules externes est renseigné par chaque module externe répertorié dans le fichier `.cordova/hooks/before_platform_add/install_plugins.js` après l’exécution de la commande `phonegap run *<platform>*`. Le répertoire est initialement vide.

### www/ {#www}

Le répertoire www contient tout le contenu web (fichiers HTML, JS et CSS) qui met en œuvre l’apparence et le comportement de l’application. À l’exception des exceptions décrites ci-dessous, ce contenu provient d’AEM et est exporté sous sa forme statique via la synchronisation de contenu.

### www/config.xml {#www-config-xml}

La documentation PhoneGap (`https://docs.phonegap.com`) fait référence à ce fichier en tant que « fichier de configuration global ». Le fichier config.xml contient de nombreuses propriétés d’application, telles que le nom de l’application, les « préférences » de l’application (par exemple, si une vue web iOS autorise le survol) et les dépendances de plug-in qui sont *uniquement* utilisées par la génération PhoneGap.

Le fichier config.xml est un fichier statique dans AEM et est exporté en l’état via la synchronisation de contenu.

### www/index.html {#www-index-html}

Le fichier index.html redirige vers la page de démarrage de l’application.

Le fichier config.xml contient l’élément `content` :

`<content src="content/phonegap/weretail/apps/ng-we-retail/en.html" />`

Dans la documentation PhoneGap (`https://docs.phonegap.com`), cet élément est décrit comme « L’élément facultatif &lt;content> définit la page de départ de l’application dans le répertoire des ressources web de niveau supérieur. La valeur par défaut est index.html, qui apparaît généralement dans le répertoire www de niveau supérieur d’un projet. »

Le build PhoneGap échoue si aucun fichier index.html n’est présent. Par conséquent, ce fichier est inclus.

### www/res {#www-res}

Le répertoire res contient des images et des icônes d’écran de démarrage. Le script `copy_resource_files.js` copie les fichiers à leurs emplacements spécifiques à la plateforme pendant la phase de création de `after_prepare`.

### www/etc {#www-etc}

Par convention, dans AEM, le nœud /etc contient du contenu clientlib statique. Le répertoire etc contient les bibliothèques Topcoat, AngularJS et We.Retail ng-clientlibsall.

### www/apps {#www-apps}

Le répertoire d’applications contient le code associé à la page d’accueil. La caractéristique unique de la page d’accueil d’une application AEM est qu’elle initialise l’application sans interaction de l’utilisateur. Le contenu de la bibliothèque cliente (à la fois CSS et JS) de l’application est donc minimal pour maximiser les performances.

### www/content {#www-content}

Le répertoire de contenu contient le reste du contenu web de l’application. Le contenu peut inclure, sans s’y limiter, les fichiers suivants :

* HTML du contenu de la page, directement créé dans AEM ;
* Ressources d’image associées aux composants AEM
* Contenu JavaScript généré par les scripts côté serveur
* Fichiers JSON décrivant le contenu de la page ou du composant.

### www/package.json {#www-package-json}

Le fichier package.json est un fichier manifeste qui répertorie les fichiers inclus dans un téléchargement de synchronisation de contenu **full**. Ce fichier contient également la date et l’heure auxquelles la payload de synchronisation du contenu a été générée ( `lastModified`). Cette propriété est utilisée lors de la demande de mises à jour partielles de l’application à AEM.

### www/package-update.json {#www-package-update-json}

Si cette payload correspond à un téléchargement de l’application entière, ce manifeste contient la liste exacte des fichiers comme `package.json`.

Cependant, si cette payload est une mise à jour partielle, `package-update.json` ne contient que les fichiers inclus dans cette payload particulière.
