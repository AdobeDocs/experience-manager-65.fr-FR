---
title: Modèles de page pour les applications mobiles
seo-title: Modèles de page pour les applications mobiles
description: Suivez cette page pour en savoir plus sur les modèles de page pour les applications mobiles.
seo-description: Suivez cette page pour en savoir plus sur les modèles de page pour les applications mobiles.
uuid: ef469796-10f5-44f4-a5c7-25025ca192b0
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: f45d8a9b-14d6-468f-a44c-3933e962922c
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '2665'
ht-degree: 0%

---


# Modèles de page pour les applications mobiles {#page-templates-for-mobile-apps}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

## Modèles de page pour les applications mobiles {#page-templates-for-mobile-apps-1}

Les composants de page que vous créez pour votre application sont basés sur le composant /libs/mobileapps/components/angular/ng-page ([ouvert en CRXDE Lite sur un serveur](http://localhost:4502/crx/de/index.jsp#/libs/mobileapps/components/angular/ng-page)local). Ce composant contient les scripts JSP suivants que votre composant hérite ou remplace :

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

Détermine le nom de l’application à l’aide de la `applicationName` propriété et l’expose au moyen de pageContext.

Inclut head.jsp et body.jsp.

### head.jsp {#head-jsp}

Écrit l’ `<head>` élément de la page de l’application.

Si vous souhaitez remplacer la propriété meta de viewport de l’application, il s’agit du fichier que vous remplacez.

Selon les meilleures pratiques, l’application inclut la partie CSS des bibliothèques clientes dans l’en-tête, tandis que la partie JS est incluse dans l’élément &lt; `body>` de fermeture.

### body.jsp {#body-jsp}

Le corps d’une page angulaire est rendu différemment selon que wcmMode est détecté (!= WCMMode.DISABLED) pour déterminer si la page est ouverte pour la création ou en tant que page publiée.

**Mode Auteur**

En mode création, chaque page individuelle est générée séparément. Angular ne gère pas le routage entre les pages, pas plus qu&#39;une vue ng n&#39;est utilisée pour charger un modèle partiel qui contient les composants de la page. En revanche, le contenu du modèle de page (template.jsp) est inclus côté serveur via la `cq:include` balise .

Cette stratégie active les fonctions d’auteur (telles que l’ajout et la modification de composants dans le système de paragraphe, le Sidekick, le mode de conception, etc.) pour fonctionner sans modification. Les pages reposant sur le rendu côté client, telles que celles des applications, ne fonctionnent pas correctement en mode AEM création.

Notez que l’inclusion template.jsp est encapsulée dans un `div` élément qui contient la `ng-controller` directive. Cette structure permet de lier le contenu DOM au contrôleur. Par conséquent, bien que les pages qui se rendent elles-mêmes côté client échouent, les composants individuels qui le font fonctionnent correctement (voir la section sur Composants ci-dessous).

```xml
<div ng-controller="<c:out value="${controllerNameStripped}"/>">
      <cq:include script="template.jsp"/>
</div>
```

**Mode de publication**

En mode de publication (par exemple, lorsque l’application est exportée à l’aide de la synchronisation de contenu), toutes les pages deviennent une application d’une seule page (SPA). (Pour en savoir plus sur SPA, utilisez le didacticiel Angular, en particulier [https://docs.angularjs.org/tutorial/step_07](https://docs.angularjs.org/tutorial/step_07).)

Il n&#39;y a qu&#39;une seule page HTML dans un SPA (une page qui contient l&#39; `<html>` élément). Cette page est connue sous le nom de &quot;modèle de mise en page&quot;. En termes angulaires, il s&#39;agit &quot; d&#39;un groupe d&#39;individus qui ne sont pas membres de l&#39;Armée de terre ou de l&#39;Armée de terre.un modèle commun à toutes les vues de notre application.&quot; Considérez cette page comme la &quot;page d’application de niveau supérieur&quot;. Par convention, la page de l’application de niveau supérieur est le `cq:Page` noeud de l’application le plus proche de la racine (et n’est pas une redirection).

Puisque l’URI réel de votre application ne change pas en mode de publication, les références aux ressources externes de cette page doivent utiliser des chemins d’accès relatifs. Par conséquent, un composant d’image spécial est fourni qui prend en compte cette page de niveau supérieur lors du rendu des images pour l’exportation.

En tant que SPA, cette page de modèle de mise en page génère simplement un élément div avec une directive ng-vue.

```xml
 <div ng-view ng-class="transition"></div>
```

Le service d’itinéraire angulaire utilise cet élément pour afficher le contenu de chaque page de l’application, y compris le contenu autorisé de la page active (contenu dans template.jsp).

Le fichier body.jsp comprend header.jsp et footer.jsp qui sont vides. Si vous souhaitez fournir du contenu statique sur chaque page, vous pouvez remplacer ces scripts dans votre application.

Enfin, les clientlibs javascript sont inclus au bas de l’élément &lt;body>, y compris deux fichiers JS spéciaux qui sont générés sur le serveur : *&lt;page name>*.angular-app-module.js et *&lt;page name>*.angular-app-contrôleurs.js.

### angular-app-module.js.jsp {#angular-app-module-js-jsp}

Ce script définit le module angulaire de l’application. La sortie de ce script est liée au balisage généré par le reste du composant du modèle via l’ `html` élément de ng-page.jsp, qui contient l’attribut suivant :

```xml
ng-app="<c:out value='${applicationName}'/>"
```

Cet attribut indique à Angular que le contenu de cet élément DOM doit être lié au module suivant. Ce module relie les vues (en AEM il s&#39;agit des ressources cq:Page) aux contrôleurs correspondants.

Ce module définit également un contrôleur de niveau supérieur nommé `AppController` qui expose la `wcmMode` variable à la portée et configure l&#39;URI à partir duquel récupérer les charges de mise à jour de Content Sync.

Enfin, ce module effectue une itération sur chaque page descendante (y compris elle-même) et effectue le rendu du contenu de la frange de route de chaque page (via le sélecteur et l&#39;extension angulaire-route-fragment.js), y compris en tant qu&#39;entrée de configuration de $routeProvider d&#39;Angular. En d’autres termes, $routeProvider indique à l’application le contenu à rendre lorsqu’un chemin d’accès donné est demandé.

### angular-route-fragment.js.jsp {#angular-route-fragment-js-jsp}

Ce script génère un fragment JavaScript qui doit se présenter comme suit :

```
.when('/<path>', {
    templateUrl: '<path to template>',
    controller: '<controller name>'
})
```

Ce code indique à $routeProvider (défini dans angular-app-module.js.jsp) que &#39;/&lt;chemin>&#39; doit être géré par la ressource à l&#39; `templateUrl`adresse et câblé par `controller` (nous allons passer à la suivante).

Si nécessaire, vous pouvez remplacer ce script pour gérer des chemins plus complexes, y compris ceux contenant des variables. Vous trouverez un exemple dans le script /apps/weretail-app/components/angular/ng-template-page/angular-route-fragment.js.jsp installé avec AEM :

```xml
// note the :id suffix on the path
.when('<c:out value="${resource.path}"/>/:id', {
    templateUrl: '<c:out value="${relativeResourcePath}"/>.template.html',
    controller: '<c:out value="${controllerNameStripped}"/>'
})
```

### angular-app-controllers.js.jsp {#angular-app-controllers-js-jsp}

Dans Angular, les contrôleurs placent les variables dans la plage $scope, les exposant à la vue. Le script angular-app-controllers.js.jsp suit le schéma illustré par angular-app-module.js.jsp en ce sens qu’il effectue une itération sur chaque page descendante (y compris sur elle-même) et génère le fragment de contrôleur défini par chaque page (via controller.js.jsp). Le module qu’il définit est appelé `cqAppControllers` et doit être répertorié comme une dépendance du module d’application de niveau supérieur afin que les contrôleurs de page soient disponibles.

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

Notez que la `data` variable se voit attribuer la promesse renvoyée par la `$http.get` méthode Angular. Chaque composant inclus dans cette page peut, si nécessaire, rendre un certain contenu .json disponible (via son script angular.json.jsp) et agir sur le contenu de cette requête lorsqu’elle est résolue. La demande est très rapide sur les périphériques mobiles, car elle accède simplement au système de fichiers.

Pour qu&#39;un composant fasse partie du contrôleur de cette manière, il doit étendre le composant /libs/mobileapps/components/angular/ng-component et inclure la `frameworkType: angular` propriété.

### template.jsp {#template-jsp}

Introduit pour la première fois dans la section body.jsp, template.jsp contient simplement les paramètres de la page. En mode de publication, ce contenu est référencé directement (à l’adresse &lt;page-path>.template.html) et chargé dans le SPA par le biais de templateUrl configuré sur $routeProvider.

Les paramètres de ce script peuvent être configurés pour accepter n’importe quel type de composant. Cependant, il faut faire attention lorsque l&#39;on traite de composants conçus pour un site Web traditionnel (par opposition à un SPA). Par exemple, le composant d’image de base fonctionne correctement uniquement sur la page de l’application de niveau supérieur, car il n’est pas conçu pour référencer les ressources qui se trouvent dans une application.

### angular-module-list.js.jsp {#angular-module-list-js-jsp}

Ce script fournit simplement les dépendances angulaires du module d’application Angular de niveau supérieur. Il est référencé par angular-app-module.js.jsp.

### header.jsp {#header-jsp}

Script destiné à placer le contenu statique en haut de l’application. Ce contenu est inclus par la page de niveau supérieur, en dehors de la portée de la vue ng.

### footer.jsp {#footer-jsp}

Script destiné à placer du contenu statique au bas de l’application. Ce contenu est inclus par la page de niveau supérieur, en dehors de la portée de la vue ng.

### js_clientlibs.jsp {#js-clientlibs-jsp}

Remplacez ce script pour inclure vos clientlibs JavaScript.

### css_clientlibs.jsp {#css-clientlibs-jsp}

Remplacez ce script pour inclure vos clientlibs CSS.

## Composants de l’application {#app-components}

Les composants de l’application ne doivent pas seulement fonctionner sur une instance AEM (publication ou auteur), mais également lorsque le contenu de l’application est exporté vers le système de fichiers via Content Sync. Le composant doit donc comporter les caractéristiques suivantes :

* Tous les actifs, modèles et scripts d’une application PhoneGap doivent être référencés de manière relativement précise.
* La gestion des liens diffère si l’instance AEM fonctionne en mode création ou publication.

### Ressources relatives {#relative-assets}

L’URI d’une ressource donnée dans une application PhoneGap diffère non seulement d’une plate-forme à l’autre, mais est unique à chaque installation de l’application. Par exemple, notez l’URI suivant d’une application s’exécutant dans le simulateur iOS :

`file:///Users/userId/Library/Application%20Support/iPhone%20Simulator/7.0.3/Applications/24BA22ED-7D06-4330-B7EB-F6FC73251CA3/Library/files/www/content/phonegap/weretail/apps/ng-we-retail/en/home.html`

Notez le GUID &#39;24BA22ED-7D06-4330-B7EB-F6FC73251CA3&#39; dans le chemin.

En tant que développeur PhoneGap, le contenu qui vous préoccupe se trouve sous le répertoire www. Pour accéder aux ressources de l’application, utilisez des chemins d’accès relatifs.

Pour aggraver le problème, votre application PhoneGap utilise le modèle d’application d’une seule page (SPA) de sorte que l’URI de base (à l’exception du hachage) ne change jamais. Par conséquent, chaque fichier, modèle ou script référencé par **doit être relatif à votre page de niveau supérieur. **La page de niveau supérieur initialise le routage angulaire et les contrôleurs en vertu de `<name>.angular-app-module.js` et `<name>.angular-app-controllers.js`. Cette page doit être la page la plus proche de la racine du référentiel qui *n’étend pas une redirection sling:redirect.

Plusieurs méthodes d’assistance sont disponibles pour traiter les chemins relatifs :

* FrameworkContentExporterUtils.getTopLevelAppResource
* FrameworkContentExporterUtils.getRelativePathToRootLevel
* FrameworkContentExporterUtils.getPathToAsset

Pour afficher des exemples de leur utilisation, ouvrez la source mobileapps située dans /libs/mobileapps/components/angular.

### Liens {#links}

Les liens doivent utiliser la `ng-click="go('/path')"` fonction pour prendre en charge tous les modes WCM. Cette fonction dépend de la valeur d’une variable d’étendue pour déterminer correctement l’action de lien :

```xml
<c:choose><c:when test="${wcmMode}">
    <%-- WCMMode is enabled - page is being rendered in AEM --%>
    $scope.wcmMode = true;
</c:when><c:otherwise>
    <%-- WCMMode is disabled --%>
    $scope.wcmMode = false;
</c:otherwise></c:choose>
```

Lorsque `$scope.wcmMode == true` nous traitons chaque événement de navigation de la manière habituelle, de telle sorte que le résultat soit une modification du chemin et/ou de la partie de page de l’URL.

Sinon, si `$scope.wcmMode == false`chaque événement de navigation entraîne un changement de la partie hachée de l&#39;URL qui est résolue en interne par le module ngRoute d&#39;Angular.

### Détails du script de composant {#component-script-details}

![chlimage_1-51](assets/chlimage_1-51.png)

### ng-component.jsp {#ng-component-jsp}

Ce script affiche le contenu du composant ou un espace réservé approprié lorsque le mode d’édition est détecté.

### template.jsp {#template-jsp-1}

Le script template.jsp effectue le rendu du balisage du composant. Si le composant en question est piloté par des données JSON extraites d’AEM (telles que &quot;ng-text&quot;) : /libs/mobileapps/components/angular/ng-text/template.jsp), ce script sera alors responsable du câblage de l&#39;annotation avec les données exposées par l&#39;étendue du contrôleur de la page.

Cependant, les exigences de performances exigent parfois qu’aucun modèle côté client (c’est-à-dire la liaison de données) ne soit effectué. Dans ce cas, il vous suffit de rendre l’annotation du composant côté serveur et de l’inclure dans le contenu du modèle de page.

### surcharge.jsp {#overhead-jsp}

Dans les composants pilotés par des données JSON (telles que &#39;ng-text&#39;) : /libs/mobileapps/components/angular/ng-text), over.jsp peut être utilisé pour supprimer tout le code Java de template.jsp. Il est ensuite référencé à partir de template.jsp et toutes les variables qu’il expose sur la requête sont disponibles pour utilisation. Cette stratégie encourage la séparation de la logique et de la présentation et limite la quantité de code à copier et coller lorsqu&#39;un nouveau composant est dérivé d&#39;un composant existant.

### controller.js.jsp {#controller-js-jsp-1}

Comme décrit dans [AEM Modèles](/help/mobile/apps-architecture.md)de page, chaque composant peut générer un fragment JavaScript afin de consommer le contenu JSON exposé par la `data` promesse. Conformément aux conventions angulaire, un contrôleur ne doit être utilisé que pour affecter des variables à l&#39;étendue.

### angular.json.jsp {#angular-json-jsp}

Ce script est inclus en tant que fragment dans le fichier &#39;&lt;page-name>.angular.json&#39; à l’échelle de la page qui est exporté pour chaque page qui étend ng-page. Dans ce fichier, le développeur de composants peut exposer toute structure JSON requise par le composant. Dans l&#39;exemple &#39;ng-text&#39;, cette structure inclut simplement le contenu du texte du composant et un indicateur indiquant si le composant inclut ou non du texte enrichi.

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

## Contenu du téléchargement des ressources de l’interface de ligne de commande {#contents-of-the-cli-assets-download}

Téléchargez les ressources de l’interface de ligne de commande à partir de la console Apps pour les optimiser pour une plateforme spécifique, puis créez l’application à l’aide de l’API d’intégration de ligne de commande PhoneGap (CLI). Le contenu du fichier ZIP que vous enregistrez sur le système de fichiers local possède la structure suivante :

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

Il s’agit d’un répertoire masqué que vous ne verrez peut-être pas en fonction de vos paramètres actuels du système d’exploitation. Configurez votre système d’exploitation de sorte que ce répertoire soit visible si vous envisagez de modifier les hooks d’application qu’il contient.

### .cordova/hooks/ {#cordova-hooks}

Ce répertoire contient les crochets [de l’](https://devgirl.org/2013/11/12/three-hooks-your-cordovaphonegap-project-needs/)interface de ligne de commande. Les dossiers du répertoire des crochets contiennent des scripts node.js exécutés exactement à des moments précis au cours de la génération.

### .cordova/hooks/after-platform_add/ {#cordova-hooks-after-platform-add}

Le répertoire after-platform_add contient le `copy_AMS_Conifg.js` fichier. Ce script copie un fichier de configuration pour prendre en charge la collecte des analyses Adobe Mobile Services.

### .cordova/hooks/after-prepare/ {#cordova-hooks-after-prepare}

Le répertoire after-prepare contient le `copy_resource_files.js` fichier. Ce script copie un certain nombre d’images d’icône et d’écran de démarrage dans des emplacements spécifiques à la plate-forme.

### .cordova/hooks/before_platform_add/ {#cordova-hooks-before-platform-add}

Le répertoire before_platform_add contient le `install_plugins.js` fichier. Ce script effectue une itération à travers une liste d&#39;identificateurs de plug-ins Cordova, en installant ceux qu&#39;il détecte ne sont pas déjà disponibles.

Cette stratégie ne nécessite pas que vous assembliez et installiez les modules externes pour AEM chaque exécution de la commande Maven `content-package:install` . L&#39;autre stratégie de vérification des fichiers dans votre système SCM nécessite l&#39;assemblage et l&#39;installation répétitifs d&#39;activités.

### .cordova/Hooks/Autres Hooks {#cordova-hooks-other-hooks}

Insérez d’autres crochets selon les besoins. Les crochets suivants sont disponibles (comme fourni par l&#39;exemple d&#39;application Phonegap hello world) :

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

Ce répertoire est vide jusqu&#39;à ce que vous exécutiez la `phonegap run *<platform>*` commande sur le projet. Actuellement, `*<platform>*` peut être soit `ios` soit `android`.

Après avoir créé l’application pour une plateforme spécifique, le répertoire correspondant est créé et contient le code de l’application spécifique à la plate-forme.

### plugins/ {#plugins}

Le répertoire des modules externes est renseigné par chaque module externe répertorié dans le `.cordova/hooks/before_platform_add/install_plugins.js` fichier après l’exécution de la `phonegap run *<platform>*` commande. Le répertoire est initialement vide.

### www/ {#www}

Le répertoire www contient l’ensemble du contenu Web (fichiers HTML, JS et CSS) qui met en oeuvre l’apparence et le comportement de l’application. A l’exception des exceptions décrites ci-dessous, ce contenu provient d’AEM et est exporté dans son formulaire statique via Content Sync.

### www/config.xml {#www-config-xml}

La documentation [de](https://docs.phonegap.com) PhoneGap fait référence à ce fichier en tant que &quot;fichier de configuration global&quot;. Le fichier config.xml contient de nombreuses propriétés d’application, telles que le nom de l’application, les &quot;préférences&quot; de l’application (par exemple, si une vue Web iOS autorise le surdéfilement) et les dépendances de plug-ins qui sont *uniquement* utilisées par PhoneGap build.

Le fichier config.xml est un fichier statique dans AEM et il est exporté en l’état au moyen de Content Sync.

### www/index.html {#www-index-html}

Le fichier index.html redirige vers la page de démarrage de l’application.

Le fichier config.xml contient l’ `content` élément :

`<content src="content/phonegap/weretail/apps/ng-we-retail/en.html" />`

Dans [la documentation](https://docs.phonegap.com)PhoneGap, cet élément est décrit comme &quot;L’élément facultatif &lt;content> définit la page de démarrage de l’application dans le répertoire des ressources Web de niveau supérieur. La valeur par défaut est index.html, qui s’affiche habituellement dans le répertoire www supérieur d’un projet.&quot;

La création de PhoneGap échoue si un fichier index.html n’est pas présent. Par conséquent, ce fichier est inclus.

### www/res {#www-res}

Le répertoire res contient des images et des icônes d’écran de démarrage. Le `copy_resource_files.js` script copie les fichiers vers leurs emplacements spécifiques à la plate-forme pendant la phase de `after_prepare` création.

### www/etc {#www-etc}

Par convention, dans AEM noeud /etc, le contenu statique clientlib est contenu. Le répertoire etc contient les bibliothèques Topcoat, AngularJS et We.Retail ng-clientlibsall.

### www/apps {#www-apps}

Le répertoire des applications contient le code associé à la page de démarrage. La caractéristique unique de la page de démarrage d’une application AEM est qu’elle initialise l’application sans interaction de l’utilisateur. Le contenu clientlib (CSS et JS) de l’application est donc minime pour optimiser les performances.

### www/content {#www-content}

Le répertoire de contenu contient le reste du contenu Web de l’application. Le contenu peut inclure, sans s’y limiter, les fichiers suivants :

* Contenu de la page HTML, directement créé dans AEM
* Fichiers d’image associés aux composants AEM
* Contenu JavaScript généré par les scripts côté serveur
* Fichiers JSON décrivant le contenu d’une page ou d’un composant

### www/package.json {#www-package-json}

Le fichier package.json est un fichier manifeste qui liste les fichiers qu’un téléchargement **complet** de synchronisation de contenu inclut. Ce fichier contient également l’horodatage auquel la charge utile de synchronisation de contenu a été générée ( `lastModified`). Cette propriété est utilisée lors de la demande de mises à jour partielles de l’application auprès d’AEM.

### www/package-update.json {#www-package-update-json}

Si cette charge utile est un téléchargement de l’application entière, ce manifeste contient la liste exacte des fichiers sous `package.json`forme de.

Cependant, si cette charge utile est une mise à jour partielle, `package-update.json` ne contient que les fichiers inclus dans cette charge utile particulière.
