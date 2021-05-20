---
title: Modèles de page pour les applications mobiles
seo-title: Modèles de page pour les applications mobiles
description: Consultez cette page pour en savoir plus sur les modèles de page pour les applications mobiles.
seo-description: Consultez cette page pour en savoir plus sur les modèles de page pour les applications mobiles.
uuid: ef469796-10f5-44f4-a5c7-25025ca192b0
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: f45d8a9b-14d6-468f-a44c-3933e962922c
exl-id: 7f00d426-4d28-41ee-8c54-636349e48669
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2665'
ht-degree: 0%

---

# Modèles de page pour les applications mobiles {#page-templates-for-mobile-apps}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

## Modèles de page pour les applications mobiles {#page-templates-for-mobile-apps-1}

Les composants de page que vous créez pour votre application sont basés sur le composant /libs/mobileapps/components/angular/ng-page ([ouvert dans CRXDE Lite sur un serveur local](http://localhost:4502/crx/de/index.jsp#/libs/mobileapps/components/angular/ng-page)). Ce composant contient les scripts JSP suivants que votre composant hérite ou remplace :

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

Selon les bonnes pratiques, l’application inclut la partie CSS des bibliothèques clientes dans l’en-tête, tandis que le JS est inclus à l’élément &lt; `body>` de fermeture.

### body.jsp {#body-jsp}

Le corps d’une page d’Angular est rendu différemment selon que wcmMode est détecté ou non (!= WCMMode.DISABLED) pour déterminer si la page est ouverte à des fins de création ou comme page publiée.

**Mode Auteur**

En mode création, chaque page individuelle est rendue séparément. Angular ne gère pas le routage entre les pages, pas plus qu’un mode ng n’est utilisé pour charger un modèle partiel contenant les composants de la page. Au lieu de cela, le contenu du modèle de page (template.jsp) est inclus côté serveur via la balise `cq:include` .

Cette stratégie active les fonctionnalités de création (telles que l’ajout et la modification de composants dans le système de paragraphes, le sidekick, le mode de conception, etc.) pour fonctionner sans modification. Les pages qui reposent sur le rendu côté client, comme celles des applications, ne fonctionnent pas correctement en mode de création AEM.

Notez que l’inclusion template.jsp est encapsulée dans un élément `div` contenant la directive `ng-controller`. Cette structure permet de lier le contenu DOM au contrôleur. Par conséquent, bien que les pages qui s’affichent du côté client échouent, les composants individuels qui le font fonctionnent correctement (voir la section sur les composants ci-dessous).

```xml
<div ng-controller="<c:out value="${controllerNameStripped}"/>">
      <cq:include script="template.jsp"/>
</div>
```

**Mode de publication**

En mode de publication (par exemple, lorsque l’application est exportée à l’aide de la synchronisation de contenu), toutes les pages deviennent une application d’une seule page (SPA). (Pour en savoir plus sur SPA, utilisez le tutoriel sur l’Angular, en particulier [https://docs.angularjs.org/tutorial/step_07](https://docs.angularjs.org/tutorial/step_07).)

Il n’y a qu’une seule page HTML dans un SPA (une page qui contient l’élément `<html>` ). Cette page est appelée &quot;modèle de mise en page&quot;. Dans la terminologie Angular, il s&#39;agit &quot; d&#39;un groupe d&#39;individus dont la mission est de se doter d&#39;un système de gestion et de gestion de l&#39;information13 &quot;.un modèle commun à toutes les vues de notre application.&quot; Considérez cette page comme la &quot;page de l’application de niveau supérieur&quot;. Par convention, la page de niveau supérieur de l’application est le noeud `cq:Page` de votre application qui est le plus proche de la racine (et n’est pas une redirection).

Comme l’URI réel de votre application ne change pas en mode de publication, les références aux ressources externes de cette page doivent utiliser des chemins d’accès relatifs. Par conséquent, un composant d’image spécial est fourni, qui prend en compte cette page de niveau supérieur lors du rendu des images pour l’exportation.

SPA, cette page de modèle de mise en page génère simplement un élément div avec une directive ng-view.

```xml
 <div ng-view ng-class="transition"></div>
```

Le service d’itinéraire Angular utilise cet élément pour afficher le contenu de chaque page de l’application, y compris le contenu modifiable de la page active (contenu dans template.jsp).

Le fichier body.jsp comprend les fichiers header.jsp et footer.jsp qui sont vides. Si vous souhaitez fournir du contenu statique sur chaque page, vous pouvez remplacer ces scripts dans votre application.

Enfin, les bibliothèques clientes JavaScript sont incluses au bas de l’élément &lt;body> , y compris deux fichiers JS spéciaux générés sur le serveur : *&lt;nom de page>*.angular-app-module.js et *&lt;nom de page>*.angular-app-contrôleurs.js.

### angular-app-module.js.jsp {#angular-app-module-js-jsp}

Ce script définit le module d’Angular de l’application. La sortie de ce script est liée au balisage généré par le reste du composant du modèle via l’élément `html` dans ng-page.jsp, qui contient l’attribut suivant :

```xml
ng-app="<c:out value='${applicationName}'/>"
```

Cet attribut indique que pour Angular, le contenu de cet élément DOM doit être lié au module suivant. Ce module relie les vues (dans AEM, il s’agit de ressources cq:Page ) aux contrôleurs correspondants.

Ce module définit également un contrôleur de niveau supérieur nommé `AppController` qui expose la variable `wcmMode` à la portée et configure l’URI à partir duquel récupérer les payloads de mise à jour de synchronisation de contenu.

Enfin, ce module effectue une itération sur chaque page descendante (y compris lui-même) et effectue le rendu du contenu de la fractionnement d’itinéraire de chaque page (via le sélecteur et l’extension angular-route-fragment.js ), y compris en tant qu’entrée de configuration du $routeProvider d’Angular. En d’autres termes, le $routeProvider indique à l’application quel contenu afficher lorsqu’un chemin donné est demandé.

### angular-route-fragment.js.jsp {#angular-route-fragment-js-jsp}

Ce script génère un fragment JavaScript qui doit se présenter comme suit :

```
.when('/<path>', {
    templateUrl: '<path to template>',
    controller: '<controller name>'
})
```

Ce code indique à $routeProvider (défini dans angular-app-module.js.jsp) que &#39;/&lt;chemin>&#39; doit être géré par la ressource à l’adresse `templateUrl` et câblé par `controller` (ce que nous allons passer à la suivante).

Si nécessaire, vous pouvez remplacer ce script pour gérer des chemins plus complexes, y compris ceux avec des variables. Vous trouverez un exemple de cela dans le script /apps/weretail-app/components/angular/ng-template-page/angular-route-fragment.js.jsp installé avec AEM :

```xml
// note the :id suffix on the path
.when('<c:out value="${resource.path}"/>/:id', {
    templateUrl: '<c:out value="${relativeResourcePath}"/>.template.html',
    controller: '<c:out value="${controllerNameStripped}"/>'
})
```

### angular-app-controllers.js.jsp {#angular-app-controllers-js-jsp}

En Angular, les contrôleurs relient les variables à la portée $scope, les exposant à la vue. Le script angular-app-controllers.js.jsp suit le modèle illustré par angular-app-module.js.jsp dans la mesure où il effectue une itération à travers chaque page descendante (y compris lui-même) et génère le fragment de contrôleur défini par chaque page (via controller.js.jsp). Le module qu’il définit est appelé `cqAppControllers` et doit être répertorié comme une dépendance du module d’application de niveau supérieur afin que les contrôleurs de page soient disponibles.

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

Notez que la variable `data` se voit attribuer la promesse renvoyée par la méthode `$http.get` Angular. Chaque composant inclus dans cette page peut, si vous le souhaitez, rendre un certain contenu .json disponible (via son script angular.json.jsp) et agir sur le contenu de cette requête lorsqu’elle est résolue. La requête est très rapide sur les appareils mobiles, car elle accède simplement au système de fichiers.

Pour qu’un composant fasse partie du contrôleur de cette manière, il doit étendre le composant /libs/mobileapps/components/angular/ng-component et inclure la propriété `frameworkType: angular` .

### template.jsp {#template-jsp}

Introduit pour la première fois dans la section body.jsp , template.jsp contient simplement le parsys de la page. En mode de publication, ce contenu est référencé directement (à l’adresse &lt;page-path>.template.html) et chargé dans le SPA via le templateUrl configuré sur le $routeProvider.

Le parsys de ce script peut être configuré pour accepter n’importe quel type de composant. Cependant, il faut être prudent lorsque vous traitez des composants créés pour un site web traditionnel (par opposition à un SPA). Par exemple, le composant d’image de base fonctionne correctement uniquement sur la page de l’application de niveau supérieur, car il n’est pas conçu pour référencer des ressources qui se trouvent dans une application.

### angular-module-list.js.jsp {#angular-module-list-js-jsp}

Ce script génère simplement les dépendances d’Angular du module d’application d’Angular de niveau supérieur. Il est référencé par angular-app-module.js.jsp.

### header.jsp {#header-jsp}

Script permettant de placer du contenu statique en haut de l’application. Ce contenu est inclus par la page de niveau supérieur, en dehors de la portée de la vue ng.

### footer.jsp {#footer-jsp}

Script permettant de placer du contenu statique au bas de l’application. Ce contenu est inclus par la page de niveau supérieur, en dehors de la portée de la vue ng.

### js_clientlibs.jsp {#js-clientlibs-jsp}

Remplacez ce script pour inclure vos bibliothèques clientes JavaScript.

### css_clientlibs.jsp {#css-clientlibs-jsp}

Remplacez ce script pour inclure vos bibliothèques clientes CSS.

## Composants de l’application {#app-components}

Les composants de l’application ne doivent pas seulement fonctionner sur une instance AEM (publication ou création), mais également lorsque le contenu de l’application est exporté vers le système de fichiers via la synchronisation de contenu. Le composant doit donc inclure les caractéristiques suivantes :

* Tous les actifs, modèles et scripts d’une application PhoneGap doivent être référencés de manière relativement précise.
* La gestion des liens diffère si l’instance AEM fonctionne en mode création ou publication.

### Ressources relatives {#relative-assets}

L’URI d’une ressource donnée dans une application PhoneGap diffère non seulement d’une plateforme à l’autre, mais est unique à chaque installation de l’application. Par exemple, notez l’URI suivant d’une application s’exécutant dans le simulateur iOS :

`file:///Users/userId/Library/Application%20Support/iPhone%20Simulator/7.0.3/Applications/24BA22ED-7D06-4330-B7EB-F6FC73251CA3/Library/files/www/content/phonegap/weretail/apps/ng-we-retail/en/home.html`

Notez le GUID &quot;24BA22ED-7D06-4330-B7EB-F6FC73251CA3&quot; dans le chemin.

En tant que développeur PhoneGap, le contenu qui vous intéresse se trouve sous le répertoire www . Pour accéder aux ressources de l’application, utilisez des chemins d’accès relatifs.

Pour aggraver le problème, votre application PhoneGap utilise le modèle de l’application monopage (SPA) afin que l’URI de base (à l’exception du hachage) ne change jamais. Par conséquent, chaque ressource, modèle ou script que vous référencez **doit être relatif à votre page de niveau supérieur. **La page de niveau supérieur initialise le routage et les contrôleurs de l’Angular en vertu de `<name>.angular-app-module.js` et `<name>.angular-app-controllers.js`. Cette page doit être la page la plus proche de la racine du référentiel qui *n’étend pas* un sling:redirect.

Plusieurs méthodes d’assistance sont disponibles pour traiter les chemins relatifs :

* FrameworkContentExporterUtils.getTopLevelAppResource
* FrameworkContentExporterUtils.getRelativePathToRootLevel
* FrameworkContentExporterUtils.getPathToAsset

Pour voir des exemples d’utilisation, ouvrez la source mobileapps située sous /libs/mobileapps/components/angular.

### Liens {#links}

Les liens doivent utiliser la fonction `ng-click="go('/path')"` pour prendre en charge tous les modes de gestion de contenu web. Cette fonction dépend de la valeur d’une variable scope pour déterminer correctement l’action de lien :

```xml
<c:choose><c:when test="${wcmMode}">
    <%-- WCMMode is enabled - page is being rendered in AEM --%>
    $scope.wcmMode = true;
</c:when><c:otherwise>
    <%-- WCMMode is disabled --%>
    $scope.wcmMode = false;
</c:otherwise></c:choose>
```

Lorsque `$scope.wcmMode == true` nous gérons chaque événement de navigation de la manière habituelle, de sorte que le résultat soit un changement du chemin et/ou de la partie page de l’URL.

Sinon, si `$scope.wcmMode == false`, chaque événement de navigation entraîne une modification de la partie de hachage de l’URL, qui est résolue en interne par le module ngRoute de l’Angular.

### Détails du script de composant {#component-script-details}

![chlimage_1-51](assets/chlimage_1-51.png)

### ng-component.jsp {#ng-component-jsp}

Ce script affiche le contenu du composant ou un espace réservé approprié lors de la détection du mode d’édition.

### template.jsp {#template-jsp-1}

Le script template.jsp effectue le rendu du balisage du composant. Si le composant en question est piloté par les données JSON extraites d’AEM (telles que &#39;ng-text&#39;) : /libs/mobileapps/components/angular/ng-text/template.jsp), ce script sera chargé de câbler le balisage avec les données exposées par la portée du contrôleur de la page.

Toutefois, les exigences de performances exigent parfois qu’aucun modèle côté client (ou liaison de données) ne soit effectué. Dans ce cas, il vous suffit d’effectuer le rendu du balisage du composant côté serveur et il est inclus dans le contenu du modèle de page.

### surcharge.jsp {#overhead-jsp}

Dans les composants pilotés par les données JSON (par exemple &quot;ng-text&quot;) : /libs/mobileapps/components/angular/ng-text), surcharge.jsp peut être utilisé pour supprimer tout le code Java de template.jsp. Il est ensuite référencé à partir de template.jsp et toutes les variables qu’il expose dans la requête peuvent être utilisées. Cette stratégie encourage la séparation logique et présentation et limite la quantité de code qui doit être copiée et collée lorsqu’un nouveau composant est dérivé d’un composant existant.

### controller.js.jsp {#controller-js-jsp-1}

Comme décrit dans [AEM Modèles de page](/help/mobile/apps-architecture.md), chaque composant peut générer un fragment JavaScript pour consommer le contenu JSON exposé par la promesse `data`. Conformément aux conventions d’Angular, un contrôleur ne doit être utilisé que pour affecter des variables à la portée.

### angular.json.jsp {#angular-json-jsp}

Ce script est inclus en tant que fragment dans le fichier &quot;&lt;page-name>.angular.json&quot; à l’échelle de la page qui est exporté pour chaque page qui étend la page ng. Dans ce fichier, le développeur de composants peut exposer toute structure JSON requise par le composant. Dans l’exemple &quot;ng-text&quot;, cette structure inclut simplement le contenu textuel du composant et un indicateur indiquant si le composant comprend du texte enrichi.

Le composant produit de l’application We.Retail est un exemple plus complexe (/apps/weretail-app/components/angular/ng-product) :

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

## Contenu du téléchargement des ressources de l’interface en ligne de commande {#contents-of-the-cli-assets-download}

Téléchargez des ressources d’interface de ligne de commande à partir de la console Applications afin de les optimiser pour une plateforme spécifique, puis créez l’application à l’aide de l’API d’intégration de ligne de commande PhoneGap (CLI). Le contenu du fichier ZIP que vous enregistrez dans le système de fichiers local présente la structure suivante :

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

Il s’agit d’un répertoire masqué que vous ne verrez peut-être pas en fonction des paramètres actuels du système d’exploitation. Vous devez configurer votre système d’exploitation afin que ce répertoire soit visible si vous envisagez de modifier les hooks d’applications qu’il contient.

### .cordova/hooks/ {#cordova-hooks}

Ce répertoire contient les [hooks CLI](https://devgirl.org/2013/11/12/three-hooks-your-cordovaphonegap-project-needs/). Les dossiers du répertoire hooks contiennent des scripts node.js exécutés exactement à des moments précis pendant la génération.

### .cordova/hooks/after-platform_add/ {#cordova-hooks-after-platform-add}

Le répertoire after-platform_add contient le fichier `copy_AMS_Conifg.js` . Ce script copie un fichier de configuration pour prendre en charge la collecte des analyses Adobe Mobile Services.

### .cordova/hooks/after-prepare/ {#cordova-hooks-after-prepare}

Le répertoire after-prepare contient le fichier `copy_resource_files.js` . Ce script copie un certain nombre d’images d’icône et d’écran de démarrage dans des emplacements spécifiques à la plateforme.

### .cordova/hooks/before_platform_add/ {#cordova-hooks-before-platform-add}

Le répertoire before_platform_add contient le fichier `install_plugins.js` . Ce script effectue une itération sur une liste d’identifiants du plug-in Cordova, en installant ceux qu’il détecte qui ne sont pas déjà disponibles.

Cette stratégie ne nécessite pas que vous groupiez et installez les modules externes à AEM chaque exécution de la commande Maven `content-package:install`. La stratégie alternative consistant à archiver les fichiers dans votre système SCM nécessite un regroupement et une installation répétitifs des activités.

### .cordova/hooks/Autres points {#cordova-hooks-other-hooks}

Incluez d’autres hooks selon les besoins. Les hooks suivants sont disponibles (comme fourni par l’exemple d’application Phonegap hello world) :

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
* after_prepare
* before_prepare
* after_run
* before_run

### platforms/ {#platforms}

Ce répertoire est vide jusqu’à ce que vous exécutiez la commande `phonegap run *<platform>*` sur le projet. Actuellement, `*<platform>*` peut être `ios` ou `android`.

Une fois l’application créée pour une plateforme spécifique, le répertoire correspondant est créé et contient le code de l’application spécifique à la plateforme.

### plugins/ {#plugins}

Le répertoire des modules externes est renseigné par chaque module externe répertorié dans le fichier `.cordova/hooks/before_platform_add/install_plugins.js` après avoir exécuté la commande `phonegap run *<platform>*`. Le répertoire est initialement vide.

### www/ {#www}

Le répertoire www contient tout le contenu web (HTML, JS et fichiers CSS) qui met en oeuvre l’apparence et le comportement de l’application. À l’exception des exceptions décrites ci-dessous, ce contenu provient d’AEM et est exporté dans sa forme statique via la synchronisation de contenu.

### www/config.xml {#www-config-xml}

La [documentation PhoneGap](https://docs.phonegap.com) fait référence à ce fichier en tant que &quot;fichier de configuration global&quot;. Le fichier config.xml contient de nombreuses propriétés d’application, telles que le nom de l’application, les &quot;préférences&quot; de l’application (par exemple, si un affichage Web iOS permet le survol) et les dépendances de module externe qui sont *uniquement* consommées par la version de PhoneGap.

Le fichier config.xml est un fichier statique dans AEM et est exporté en l’état par synchronisation de contenu.

### www/index.html {#www-index-html}

Le fichier index.html redirige vers la page de début de l’application.

Le fichier config.xml contient l’élément `content` :

`<content src="content/phonegap/weretail/apps/ng-we-retail/en.html" />`

Dans [la documentation PhoneGap](https://docs.phonegap.com), cet élément est décrit comme &quot;L’élément &lt;content> facultatif définit la page de début de l’application dans le répertoire des ressources web de niveau supérieur. La valeur par défaut est index.html, qui s’affiche généralement dans le répertoire www de niveau supérieur d’un projet.&quot;

La version de PhoneGap échoue si un fichier index.html n’est pas présent. Par conséquent, ce fichier est inclus.

### www/res {#www-res}

Le répertoire res contient des images et des icônes d’écran de démarrage. Le script `copy_resource_files.js` copie les fichiers à leurs emplacements spécifiques à la plateforme au cours de la phase de génération `after_prepare`.

### www/etc {#www-etc}

Par convention, dans AEM noeud /etc , le contenu clientlib statique est contenu. Le répertoire etc contient les bibliothèques Topcoat, AngularJS et We.Retail ng-clientlibsall.

### www/apps {#www-apps}

Le répertoire des applications contient du code associé à la page de démarrage. La caractéristique unique de la page de démarrage d’une application AEM est qu’elle initialise l’application sans interaction de l’utilisateur. Le contenu clientlib (CSS et JS) de l’application est donc minimal pour optimiser les performances.

### www/content {#www-content}

Le répertoire de contenu contient le reste du contenu web de l’application. Le contenu peut inclure, sans s’y limiter, les fichiers suivants :

* Contenu de la page HTML directement créé dans AEM
* Ressources d’image associées aux composants AEM
* Contenu JavaScript généré par les scripts côté serveur
* Fichiers JSON décrivant le contenu d’une page ou d’un composant

### www/package.json {#www-package-json}

Le fichier package.json est un fichier manifeste qui répertorie les fichiers qu’un téléchargement de synchronisation de contenu **full** comprend. Ce fichier contient également l’horodatage auquel la charge utile de synchronisation de contenu a été générée ( `lastModified`). Cette propriété est utilisée lorsque vous demandez des mises à jour partielles de l’application à partir d’AEM.

### www/package-update.json {#www-package-update-json}

Si cette payload est un téléchargement de l’application entière, ce manifeste contient la liste exacte des fichiers sous la forme `package.json`.

Cependant, si cette payload est une mise à jour partielle, `package-update.json` contient uniquement les fichiers inclus dans cette payload particulière.
