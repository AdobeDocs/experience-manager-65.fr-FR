---
title: Conception réactive pour les pages web
seo-title: Responsive design for web pages
description: Le Responsive Design permet d’afficher les mêmes pages sur plusieurs appareils selon différentes orientations.
seo-description: With responsive design, the same pages can be effectively displayed on multiple devices in multiple orientations
uuid: 3d324557-e7ff-4c82-920f-9b5a906925e8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
discoiquuid: 532544b0-1932-419a-b6bd-ecf57a926fef
legacypath: /content/docs/en/aem/6-0/develop/mobile/responsive
exl-id: c705710b-a94a-4f4f-affa-ddd4fc6cb0ec
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '5317'
ht-degree: 70%

---

# Responsive Design pour les pages web{#responsive-design-for-web-pages}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur de SPA pour les projets qui nécessitent un rendu côté client basé sur la structure d’application d’une seule page (tel que _React_). [En savoir plus](/help/sites-developing/spa-overview.md).

Concevez vos pages web afin qu’elles s’adaptent à la fenêtre dans laquelle elles sont affichées. Le Responsive Design permet d’afficher les mêmes pages sur plusieurs appareils dans les deux orientations. L’image suivante présente différentes méthodes par lesquelles une page peut s’adapter aux changements de taille de la fenêtre d’affichage :

* Mise en page : utilisez des mises en page à une seule colonne pour les fenêtres d’affichage plus petites et des mises en page à plusieurs colonnes pour les fenêtres d’affichage plus grandes.
* Taille du texte : utilisez un texte plus grand (pour les titres, par exemple) dans les fenêtres d’affichage de plus grande taille.
* Contenu : n’insérez que le contenu le plus important en cas de visualisation sur des appareils de petite taille.
* Navigation : des outils spécifiques à l’appareil sont fournis pour accéder à d’autres pages.
* Images : Diffusion de rendus d’image adaptés à la fenêtre d’affichage client. selon les dimensions de la fenêtre.

![chlimage_1-4](assets/chlimage_1-4a.png)

Développez des applications Adobe Experience Manager (AEM) qui génèrent des pages HTML5 qui s’adaptent à plusieurs tailles de fenêtre et orientations. À titre d’exemple, les plages de largeurs de fenêtre d’affichage suivantes correspondent à divers types d’appareil et à diverses orientations :

* Largeur maximale de 480 pixels (téléphone, portrait)
* Largeur maximale de 767 pixels (téléphone, paysage)
* Largeur entre 768 pixels et 979 pixels (tablette, portrait)
* Largeur entre 980 pixels et 1 199 pixels (tablette, paysage)
* Largeur de 1 200 px ou plus (ordinateur de bureau)

Consultez les rubriques suivantes pour en savoir plus sur la mise en œuvre du comportement Responsive Design :

* [Requête de média](/help/sites-developing/responsive.md#using-media-queries)
* [Grilles fluides](/help/sites-developing/responsive.md#developing-a-fluid-grid)
* [Images adaptatives](/help/sites-developing/responsive.md#using-adaptive-images)

Lors de la conception, utilisez **[!UICONTROL Sidekick]** pour prévisualiser vos pages pour différents formats d’écran.

## Avant le développement {#before-you-develop}

Avant de développer l’application AEM prenant en charge vos pages web, il convient de prendre plusieurs décisions en matière de conception. Vous devez, par exemple, disposer des informations suivantes :

* Appareils ciblés.
* Tailles de fenêtre d’affichage ciblées.
* Mises en page de chacune des tailles de fenêtre d’affichage ciblées.

### Structure de l&#39;application {#application-structure}

La structure d’application AEM type prend en charge toutes les implémentations de Responsive Design :

* Les composants de page sont stockés sous /apps/*nom_application*/components.
* Les composants sont stockés sous /apps/*nom_application*/templates.
* Les conceptions sont stockées sous /etc/designs.

## Utilisation des requêtes multimédias {#using-media-queries}

Les requêtes de média permettent une utilisation sélective des styles CSS pour le rendu des pages. Les fonctionnalités et outils de développement AEM vous permettent d’implémenter efficacement des requêtes de média dans vos applications.

Le groupe W3C fournit la recommandation [Media Queries](https://www.w3.org/TR/css3-mediaqueries/) (Requêtes de média) qui décrit cette fonctionnalité CSS3, ainsi que la syntaxe.

### Création du fichier CSS {#creating-the-css-file}

Dans votre fichier CSS, définissez les requêtes de média en fonction des propriétés des appareils que vous ciblez. La stratégie d’implémentation suivante se révèle particulièrement utile pour gérer des styles pour chaque requête de média :

* Utilisez un ClientLibraryFolder pour définir le CSS qui est assemblé lors du rendu de la page.
* Définissez chaque requête de média et les styles associés dans des fichiers CSS distincts. Il s’avère utile d’utiliser des noms de fichier qui représentent les fonctions de périphérique de la requête de média.
* Définissez des styles communs à tous les périphériques dans un fichier CSS distinct.
* Dans le fichier css.txt du ClientLibraryFolder, classez les fichiers CSS comme l’exige le fichier CSS assemblé.

L’exemple de média We.Retail utilise cette stratégie pour définir des styles dans la conception du site. Le fichier CSS utilisé par We.Retail se trouve à l’adresse `*/apps/weretail/clientlibs/clientlib-site/less/grid.less`.

Le tableau suivant répertorie les fichiers situés dans le dossier enfant CSS.

<table>
 <tbody>
  <tr>
   <th>Nom du fichier</th>
   <th>Description</th>
   <th>Requête multimédia</th>
  </tr>
  <tr>
   <td>style.css</td>
   <td>Styles communs.</td>
   <td>S/O</td>
  </tr>
  <tr>
   <td>bootstrap.css</td>
   <td>Styles communs, définis par le Bootstrap Twitter.</td>
   <td>S/O</td>
  </tr>
  <tr>
   <td>responsive-1200px.css</td>
   <td>Styles pour tous les médias d’une largeur ou d’une largeur de 1 200 pixels.</td>
   <td><p>@media (min-width: 1200px) {<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-980px-1199px.css</td>
   <td>Styles pour les médias dont la largeur est comprise entre 980 et 1 199 pixels.</td>
   <td><p>@media (min-width: 980 px) et (largeur max. : 1199px) {<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-768px-979px.css</td>
   <td>Styles pour les médias dont la largeur est comprise entre 768 et 979 pixels. </td>
   <td><p>@media (min-width: 768px) et (max-width: 979px) {<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-767px-max.css</td>
   <td>Styles pour tous les médias dont la largeur est inférieure à 768 pixels.</td>
   <td><p>@media (max-width: 767px) {<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-480px.css</td>
   <td>Styles pour tous les médias dont la largeur est inférieure à 481 pixels.</td>
   <td>@media (max-width: 480) {<br /> ...<br /> }</td>
  </tr>
 </tbody>
</table>

Le fichier css.txt dans la variable `/etc/designs/weretail/clientlibs` répertorie les fichiers CSS que le dossier de bibliothèque cliente inclut. L’ordre des fichiers applique la priorité de style. Plus la taille du périphérique diminue, plus les styles sont précis.

`#base=css`

```
style.css
 bootstrap.css
```

```
responsive-1200px.css
 responsive-980px-1199px.css
 responsive-768px-979px.css
 responsive-767px-max.css
 responsive-480px.css
```

**Conseil**: Les noms de fichiers descriptifs vous permettent d’identifier facilement la taille de fenêtre d’affichage ciblée.

### Utilisation de requêtes de média avec des pages AEM {#using-media-queries-with-aem-pages}

Ajoutez le dossier de bibliothèque cliente dans le script JSP de votre composant de page afin de générer le fichier CSS qui contient les requêtes de média et de référencer le fichier.

```xml
<ui:includeClientLib categories="apps.weretail.all"/>
```

>[!NOTE]
>
>Le `apps.weretail.all` le dossier de bibliothèques clientes intègre la bibliothèque clientlibs .

Le script JSP génère le code HTML suivant qui référence les feuilles de style :

```xml
<link rel="stylesheet" href="/etc/designs/weretail/clientlibs-all.css" type="text/css">
<link href="/etc/designs/weretail.css" rel="stylesheet" type="text/css">
```

## Aperçu pour des appareils spécifiques {#previewing-for-specific-devices}

Vous pouvez afficher des aperçus de vos pages dans différents formats de fenêtre afin de tester le comportement de votre conception Responsive Design. Dans **[!UICONTROL Aperçu]** mode, **[!UICONTROL Sidekick]** inclut une **[!UICONTROL Périphériques]** menu déroulant que vous utilisez pour sélectionner un appareil. Lorsque vous sélectionnez un périphérique, la page change afin de s’adapter à la taille de la fenêtre d’affichage.

![chlimage_1-5](assets/chlimage_1-5a.png)

Pour activer l’aperçu du périphérique dans **[!UICONTROL Sidekick]**, vous devez configurer la page et la variable **[!UICONTROL MobileEmulatorProvider]** service. Une autre configuration de page contrôle la liste des périphériques qui s’affichent dans la variable **[!UICONTROL Périphériques]** liste.

### Ajout de la liste des périphériques {#adding-the-devices-list}

Le **[!UICONTROL Périphériques]** apparaît dans la liste **[!UICONTROL Sidekick]** lorsque votre page inclut le script JSP qui effectue le rendu de la variable **[!UICONTROL Périphériques]** liste. Pour ajouter la variable **[!UICONTROL Périphériques]** à **[!UICONTROL Sidekick]**, incluez la variable `/libs/wcm/mobile/components/simulator/simulator.jsp` dans le `head` de votre page.

Insérez le code suivant dans le JSP qui définit la section `head` :

`<cq:include script="/libs/wcm/mobile/components/simulator/simulator.jsp"/>`

Pour afficher un exemple, ouvrez le `/apps/weretail/components/page/head.jsp` dans CRXDE Lite.

### Enregistrement des composants Page pour la simulation {#registering-page-components-for-simulation}

Pour permettre au simulateur de périphérique de prendre en charge vos pages, enregistrez vos composants de page auprès du service de fabrique MobileEmulatorProvider et définissez la propriété `mobile.resourceTypes`.

Dans AEM, il existe plusieurs méthodes pour gérer les paramètres de configuration pour ces services. Pour plus d’informations, voir [Configuration d’OSGi](/help/sites-deploying/configuring-osgi.md). 

Par exemple, pour créer un nœud ` [sling:OsgiConfig](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository)` dans votre application, procédez comme suit :

* Dossier parent : `/apps/application_name/config`
* Nom : `com.day.cq.wcm.mobile.core.impl.MobileEmulatorProvider-*alias*`

   Le - `*alias*` Le suffixe est requis, car le service MobileEmulatorProvider est un service d’usine. Utilisez un alias unique pour cette fabrique.

* jcr:primaryType: `sling:OsgiConfig`

Ajoutez la propriété de nœud suivante :

* Nom : `mobile.resourceTypes`
* Type : `String[]`
* Valeur : chemins d’accès aux composants de page qui effectuent le rendu de vos pages web. Par exemple, l’application geometrixx-media utilise les valeurs suivantes :

   ```
   geometrixx-media/components/page
    geometrixx-unlimited/components/pages/page
    geometrixx-unlimited/components/pages/coverpage
    geometrixx-unlimited/components/pages/issue
   ```

### Spécification des groupes d’appareils {#specifying-the-device-groups}

Pour spécifier les groupes de périphériques qui figurent dans la liste Périphériques, ajoutez une propriété `cq:deviceGroups` au nœud `jcr:content` de la page racine de votre site. La valeur de la propriété est un tableau de chemins d’accès pointant vers les nœuds du groupe de périphériques.

Les noeuds du groupe d’appareils se trouvent dans la variable `/etc/mobile/groups` dossier.

Par exemple, la page racine du site Geometrixx Media est `/content/geometrixx-media`. Le `/content/geometrixx-media/jcr:content` comprend la propriété suivante :

* Nom : `cq:deviceGroups`
* Type : `String[]`
* Valeur : `/etc/mobile/groups/responsive`

Utilisez la console Outils pour [créer et modifier des groupes de périphériques](/help/sites-developing/groupfilters.md).

>[!NOTE]
>
>S’agissant des groupes de périphériques que vous utilisez dans le cadre du Responsive Design, modifiez le groupe, puis sélectionnez Désactiver l’émulateur sur l’onglet Général. Cette option empêche l’affichage du carrousel de l’émulateur, qui n’est pas pertinent dans le cadre du Responsive Design.

## Utilisation d’images adaptatives {#using-adaptive-images}

Vous pouvez utiliser des requêtes de média pour sélectionner une ressource d’image à afficher sur la page. Sachez toutefois que chaque ressource qui utilise une requête de média pour appliquer des conditions à son utilisation est téléchargée sur le client. La requête de média détermine simplement si la ressource téléchargée est affichée.

Dans le cas des ressources de grande taille, comme les images, télécharger l’ensemble des éléments ne constitue pas une utilisation efficace du pipeline des données du client. Pour télécharger les ressources de manière sélective, utilisez du code JavaScript afin de lancer une requête de ressource après que les requêtes de média ont effectué la sélection.

La stratégie suivante charge une ressource unique qui est sélectionnée à l’aide des requêtes de média :

1. Ajoutez un élément DIV pour chaque version de la ressource. Insérez l’URI de la ressource en tant que valeur d’un attribut. Le navigateur n’interprète pas l’attribut comme une ressource.
1. Ajoutez une requête de média à chaque élément DIV adapté à la ressource.
1. Lors du chargement du document ou du redimensionnement de la fenêtre, le code JavaScript teste la requête de média de chaque élément DIV.
1. En vous basant sur les résultats des requêtes, déterminez la ressource à inclure.
1. Insérez un élément HTML dans le DOM qui référence la ressource.

### Évaluation des requêtes de média à l’aide de JavaScript {#evaluating-media-queries-using-javascript}

Les mises en oeuvre de [Interface de MediaQueryList](https://dev.w3.org/csswg/cssom-view/#the-mediaquerylist-interface) que le W3C définit vous permet d’évaluer les requêtes multimédias à l’aide de javascript. Vous pouvez appliquer la logique à des résultats de requête de média et exécuter les scripts qui sont destinés à la fenêtre active :

* Les navigateurs qui implémentent l’interface MediaQueryList prennent en charge la variable `window.matchMedia()` fonction . Cette fonction teste les requêtes de média par rapport à une chaîne donnée. La fonction renvoie un objet `MediaQueryList` qui permet d’accéder aux résultats de la requête.

* Pour les navigateurs qui n’implémentent pas l’interface, vous pouvez utiliser une `matchMedia()` polyfill, par exemple [matchMedia.js](https://github.com/paulirish/matchMedia.js), une bibliothèque JavaScript disponible gratuitement.

#### Sélection de ressources spécifiques au média {#selecting-media-specific-resources}

L’[élément picture](https://picture.responsiveimages.org/) proposé par le W3C utilise des requêtes de média afin de déterminer la source à utiliser pour les éléments images. L’élément picture utilise des attributs d’élément pour associer des requêtes de média à des chemins d’accès aux images.

Le libre accès [bibliothèque picturefill.js](https://github.com/scottjehl/picturefill) offre des fonctionnalités similaires à celles proposées. `picture` et utilise une stratégie similaire. La bibliothèque picturefill.js appelle `window.matchMedia` pour évaluer les requêtes de média définies pour un ensemble d’éléments `div`. Chaque élément `div`spécifie également une source d’images. Cette source est utilisée lorsque la requête de média de l’élément `div` renvoie la valeur `true`.

Le `picturefill.js` La bibliothèque requiert un code HTML similaire à l’exemple suivant :

```xml
<div data-picture>
    <div data-src='path to default image'></div>
    <div data-src='path to small image'    data-media="(media query for phone)"></div>
    <div data-src='path to medium image'   data-media="(media query for tablet)"></div>
    <div data-src='path to large image'     data-media="(media query for monitor)"></div>
</div>
```

Lorsque la page est rendue, picturefull.js insère une `img` comme dernier enfant de l’élément `<div data-picture>` element:

```xml
<div data-picture>
    <div data-src='path to default image'></div>
    <div data-src='path to small image'    data-media="(media query for phone)"></div>
    <div data-src='path to medium image'   data-media="(media query for tablet)"></div>
    <div data-src='path to large image'     data-media="(media query for monitor)"></div>
    <img src="path to medium image">
</div>
```

Dans une page AEM, la valeur de l’attribut `data-src` est le chemin d’accès à une ressource dans le référentiel.

### Mise en oeuvre d’images adaptatives dans AEM {#implementing-adaptive-images-in-aem}

Pour implémenter des images adaptatives dans votre application AEM, vous devez ajouter les bibliothèques JavaScript requises et inclure le balisage HTML dans vos pages.

**Bibliothèques**

Procurez-vous les bibliothèques JavaScript suivantes et insérez-les dans un dossier de bibliothèque cliente :

* [matchMedia.js](https://github.com/paulirish/matchMedia.js) (pour les navigateurs qui n’implémentent pas l’interface MediaQueryList)
* [picturefill.js](https://github.com/scottjehl/picturefill)
* jquery.js (disponible au moyen de la fonction `/etc/clientlibs/granite/jquery` dossier de bibliothèque cliente (catégorie = jquery)
* [jquery.debouncedresize.js](https://github.com/louisremi/jquery-smartresize) (événement jquery qui se produit une seule fois après le redimensionnement de la fenêtre)

**Conseil :** Vous pouvez concaténer automatiquement plusieurs dossiers de bibliothèques clientes en [incorporation](/help/sites-developing/clientlibs.md#embedding-code-from-other-libraries).

**HTML**

Créez un composant qui génère les éléments div requis attendus par le code picturefill.js. Dans une page AEM, la valeur de l’attribut data-src est le chemin d’accès à une ressource dans le référentiel. Par exemple, un composant de page peut coder en dur les requêtes de média et les chemins associés pour les rendus d’image dans la gestion des ressources numériques. Vous pouvez également créer un composant Image personnalisé permettant aux auteurs de sélectionner des rendus d’image ou de définir des options de rendu lors de l’exécution.

L’exemple de code HTML ci-dessous effectue une sélection parmi 2 rendus DAM de la même image.

```xml
<div data-picture>
    <div data-src='/content/dam/geometrixx-media/articles/meridien.png'></div>
    <div data-src='/content/dam/geometrixx-media/articles/meridien.png/jcr:content/renditions/cq5dam.thumbnail.319.319.png'    data-media="(min-width: 769px)"></div>
    <div data-src='/content/dam/geometrixx-media/articles/meridien.png/jcr:content/renditions/cq5dam.thumbnail.140.100.png'   data-media="(min-width: 481px)"></div>
</div>
```

>[!NOTE]
>
>Le composant de base Image adaptative implémente des images adaptatives :
>
>* Dossier de la bibliothèque cliente: `/libs/foundation/components/adaptiveimage/clientlibs`
>* Script qui génère le HTML : `/libs/foundation/components/adaptiveimage/adaptiveimage.jsp`
>
>Vous trouverez plus d’informations sur ce composant à la section suivante.

### Comprendre le rendu des images dans AEM {#understanding-image-rendering-in-aem}

Pour personnaliser le rendu d’images, vous devez comprendre l’implémentation du rendu d’images statiques par défaut dans AEM. AEM fournit le composant Image et un servlet de rendu d’images qui fonctionnent de concert pour effectuer le rendu d’images pour la page web. La séquence d’événements suivante se produit lorsque le composant Image est inclus dans le système de paragraphes de la page :

1. Création : les auteurs modifient le composant Image afin de spécifier le fichier image à inclure dans une page HTML. Le chemin d’accès au fichier est stocké en tant que valeur de propriété du nœud de composant Image.
1. Demande de page : le JSP du composant de page génère le code HTML. Le JSP du composant Image génère un élément img et l’ajoute à la page.
1. Demande d’image : le navigateur web charge la page et demande l’image en fonction de l’attribut src de l’élément img.
1. Rendu de l’image : le servlet de rendu d’images renvoie l’image au navigateur web.

![chlimage_1-6](assets/chlimage_1-6a.png)

Par exemple, le JSP du composant Image génère l’élément HTML suivant :

`<img title="My Image" alt="My Image" class="cq-dd-image" src="/content/mywebsite/en/_jcr_content/par/image_0.img.jpg/1358372073597.jpg">`

Lorsque la navigateur charge la page, il demande l’image en utilisant la valeur de l’attribut src en tant qu’URL. Sling décompose l’URL :

* Ressource: `/content/mywebsite/en/_jcr_content/par/image_0`
* Extension de nom de fichier : `.jpg`
* Sélecteur: `img`
* Suffixe: `1358372073597.jpg`

Le `image_0` possède un noeud `jcr:resourceType` valeur de `foundation/components/image`, qui a une `sling:resourceSuperType` valeur de `foundation/components/parbase`. Le composant parbase contient le script img.GET.java qui correspond au sélecteur et à l’extension de nom de fichier de l’URL de demande. CQ utilise ce script (servlet) pour effectuer le rendu de l’image.

Pour afficher le code source du script, utilisez CRXDE Lite pour ouvrir la `/libs/foundation/components/parbase/img.GET.java`
fichier .

## Mise à l’échelle des images pour la taille actuelle de la fenêtre d’affichage {#scaling-images-for-the-current-viewport-size}

Dimensionnez les images au moment de l’exécution en fonction des caractéristiques de la fenêtre d’affichage du client pour fournir des images conformes aux principes du Responsive Design. Utilisez le même schéma de conception que le rendu d’images statiques, à l’aide d’un servlet et d’un composant de création.

Le composant doit effectuer les tâches suivantes :

* Stocker le chemin d’accès et les dimensions souhaitées de la ressource d’image sous la forme de valeurs de propriété.
* Générer des éléments `div` contenant des sélecteurs de médias et des appels de service pour le rendu de l’image.

>[!NOTE]
>
>Le client web utilise les bibliothèques JavaScript matchMedia et Picturefill (ou des bibliothèques similaires) pour évaluer les sélecteurs de médias.

Le servlet qui traite la demande d’image doit effectuer les tâches suivantes :

* Récupérer le chemin d’accès et les dimensions de l’image dans les propriétés du composant.
* Redimensionner l’image conformément aux propriétés et la renvoyer.

**Solutions disponibles**

AEM installe les implémentations suivantes que vous pouvez utiliser ou étendre.

* Le composant de base Image adaptative qui génère des requêtes de média, ainsi que des requêtes HTTP adressées au servlet Adaptive Image Component Servlet qui redimensionne les images.
* Le module Geometrixx Commons installe l’exemple de servlet Image Reference Modification Servlet qui modifie la résolution de l’image.

### Présentation du composant Image adaptative {#understanding-the-adaptive-image-component}

Le composant Image adaptative génère des appels vers le servlet Adaptive Image Component Servlet pour effectuer le rendu d’une image dimensionnée en fonction de l’écran de l’appareil. Le composant contient les ressources suivantes :

* JSP : ajoute des éléments div qui associent des requêtes de média à des appels vers le servlet Adaptive Image Component Servlet.
* Bibliothèques clientes : Le dossier clientlibs est un `cq:ClientLibraryFolder` qui assemble la bibliothèque JavaScript matchMedia polyfill et une bibliothèque JavaScript Picturefill modifiée.
* Boîte de dialogue de modification : Le `cq:editConfig` remplace le composant d’image de base CQ de sorte que la cible de dépôt crée un composant d’image adaptative plutôt qu’un composant d’image de base.

#### Ajouter les éléments DIV {#adding-the-div-elements}

Le script adaptive-image.jsp contient le code suivant qui génère des éléments div et des requêtes de média :

```
<div data-picture data-alt='<%= alt %>'>
    <div data-src='<%= path + ".img.320.low." + extension + suffix %>'       data-media="(min-width: 1px)"></div>                                        <%-- Small mobile --%>
    <div data-src='<%= path + ".img.320.medium." + extension + suffix %>'    data-media="(min-width: 320px)"></div>  <%-- Portrait mobile --%>
    <div data-src='<%= path + ".img.480.medium." + extension + suffix %>'    data-media="(min-width: 321px)"></div>  <%-- Landscape mobile --%>
    <div data-src='<%= path + ".img.476.high." + extension + suffix %>'      data-media="(min-width: 481px)"></div>   <%-- Portrait iPad --%>
    <div data-src='<%= path + ".img.620.high." + extension + suffix %>'      data-media="(min-width: 769px)"></div>  <%-- Landscape iPad --%>
    <div data-src='<%= path + ".img.full.high." + extension + suffix %>'     data-media="(min-width: 1025px)"></div> <%-- Desktop --%>

    <%-- Fallback content for non-JS browsers. Same img src as the initial, unqualified source element. --%>
    <noscript>
        <img src='<%= path + ".img.320.low." + extension + suffix %>' alt='<%= alt %>'>
    </noscript>
</div>
```

La variable `path` contient le chemin d’accès de la ressource actuelle (le nœud du composant Image adaptative). Le code génère une série d’éléments `div` avec la structure suivante :

`<div data-scr = "*path-to-parent-node*.adaptive-image.adapt.*width*.*quality*.jpg" data-media="*media query*"></div>`

La valeur de l’attribut `data-scr` est une URL que Sling résout sur le servlet Adaptive Image Component Servlet qui effectue le rendu de l’image. L’attribut data-media contient la requête de média qui est évaluée par rapport aux propriétés du client.

Le code de HTML suivant est un exemple de la variable `div` éléments générés par le JSP :

```xml
<div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.320.low.jpg'></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.320.medium.jpg'    data-media="(min-width: 320px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.480.medium.jpg'    data-media="(min-width: 321px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.476.high.jpg'     data-media="(min-width: 481px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.620.high.jpg'     data-media="(min-width: 769px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.full.high.jpg'     data-media="(min-width: 1025px)"></div>
```

#### Modification des sélecteurs de taille d’image {#changing-the-image-size-selectors}

Si vous personnalisez le composant Image adaptative et modifiez les sélecteurs de largeur, vous devez également configurer le servlet Adaptive Image Component Servlet pour qu’il prenne en charge ces largeurs.

### Présentation du servlet Adaptive Image Component Servlet {#understanding-the-adaptive-image-component-servlet}

Le servlet Adaptive Component Servlet redimensionne une image JPEG selon une largeur spécifiée et définit la qualité JPEG.

#### Interface du servlet Adaptive Image Component Servlet {#the-interface-of-the-adaptive-image-component-servlet}

Le servlet Adaptive Image Component Servlet est lié au servlet Sling par défaut. Il prend en charge les extensions de fichier .jpg, .jpeg, .gif et .png. Le sélecteur de servlet est img.

>[!CAUTION]
>
>Les fichiers .gif animés ne sont pas pris en charge dans AEM pour les rendus adaptatifs.

Par conséquent, Sling résout les URL de requête HTTP au format suivant sur ce servlet :

`*path-to-node*.img.*extension*`

Par exemple, Sling transfère des requêtes HTTP avec l’URL `http://localhost:4502/content/geometrixx/adaptiveImage.img.jpg` vers le servlet Adaptive Image Component Servlet.

Deux sélecteurs supplémentaires définissent la largeur d’image demandée et la qualité JPEG. L’exemple suivant demande une image d’une largeur de 480 pixels et de qualité moyenne :

`http://localhost:4502/content/geometrixx/adaptiveImage.adapt.480.MEDIUM.jpg`

**Propriétés d’image prises en charge**

Le servlet accepte un nombre fini de largeurs et de qualités d’image. Les largeurs suivantes sont prises en charge par défaut (en pixels) :

* full
* 320
* 480
* 476
* 620

La valeur full (complet) indique qu’il n’y a pas de mise à l’échelle.

Les valeurs de qualité JPEG ci-dessous sont prises en charge :

* LOW (FAIBLE)
* MEDIUM (MOYENNE)
* HIGH (ÉLEVÉE)

Les valeurs numériques sont, respectivement, 0,4, 0,82 et 1,0.

**Modification des largeurs par défaut prises en charge**

Utilisez la console web ([http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)) ou un nœud sling:OsgiConfig pour configurer les largeurs prises en charge du servlet Adaptive Image Component Servlet Adobe CQ.

Pour plus d’informations sur la configuration des services AEM, voir [Configuration d’OSGi](/help/sites-deploying/configuring-osgi.md).

<table>
 <tbody>
  <tr>
   <th> </th>
   <th>Console web</th>
   <th>sling:OsgiConfig</th>
  </tr>
  <tr>
   <th>Nom du service ou du noeud</th>
   <td>Le nom du service sur l’onglet Configuration est Adobe CQ Adaptive Image Component Servlet</td>
   <td>com.day.cq.wcm.foundation.impl. AdaptiveImageComponentServlet</td>
  </tr>
  <tr>
   <th>Propriété</th>
   <td><p>Largeurs prises en charge</p>
    <ul>
     <li>Pour ajouter une largeur prise en charge, cliquez sur un bouton + et saisissez un entier positif.</li>
     <li>Pour supprimer une largeur prise en charge, cliquez sur le bouton - associé.</li>
     <li>Pour modifier une largeur prise en charge, modifiez la valeur du champ.</li>
    </ul> </td>
   <td><p>adapt.supported.widths</p>
    <ul>
     <li>La propriété est une valeur String à plusieurs valeurs.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

#### Détails de mise en œuvre {#implementation-details}

Le `com.day.cq.wcm.foundation.impl.AdaptiveImageComponentServlet` étend la classe [AbstractImageServlet](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.html) classe . Le code source AdaptiveImageComponentServlet se trouve dans la variable `/libs/foundation/src/impl/src/com/day/cq/wcm/foundation/impl` dossier.

La classe utilise les annotations SCR Felix pour configurer le type de ressource et l’extension de fichier auxquels le servlet est associé, ainsi que le nom du premier sélecteur.

```java
@Component(metatype = true, label = "Adobe CQ Adaptive Image Component Servlet",
        description = "Render adaptive images in a variety of qualities")
@Service
@Properties(value = {
    @Property(name = "sling.servlet.resourceTypes", value = "foundation/components/adaptiveimage", propertyPrivate = true),
    @Property(name = "sling.servlet.selectors", value = "img", propertyPrivate = true),
    @Property(name = "sling.servlet.extensions", value ={
            "jpg",
            "jpeg",
            "png",
            "gif"
    }, propertyPrivate = true)
})
```

Le servlet utilise l’annotation SCR Property pour définir les dimensions et la qualité d’image prises en charge par défaut.

```java
@Property(value = {
            "320", // iPhone portrait
            "480", // iPhone landscape
            "476", // iPad portrait
            "620" // iPad landscape
    },
            label = "Supported Widths",
            description = "List of widths this component is permitted to generate.")
```

Le `AbstractImageServlet` fournit la classe `doGet` qui traite la requête HTTP. Cette méthode détermine la ressource associée à la requête, récupère les propriétés de ressource du référentiel et les renvoie dans un [ImageContext](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.ImageContext.html) .

>[!NOTE]
>
>Le [com.day.cq.commons.DownloadResource](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/DownloadResource.html) fournit la classe `getFileReference method`, qui récupère la valeur de la variable `fileReference` .

Le `AdaptiveImageComponentServlet` remplace la classe `createLayer` . La méthode récupère le chemin d’accès de la ressource d’image et la largeur d’image demandée auprès de l’objet `ImageContext`. Elle appelle ensuite les méthodes de la classe `info.geometrixx.commons.impl.AdaptiveImageHelper` , , qui effectue la mise à l’échelle proprement dite de l’image.

La classe AdaptiveImageComponentServlet remplace également la méthode writeLayer . Cette méthode applique la qualité JPEG à l’image.

### Image Reference Modification Servlet (Geometrixx Commons) {#image-reference-modification-servlet-geometrixx-common}

L’exemple·de·servlet·Image Reference Modification Servlet génère des attributs de taille pour l’élément img afin de dimensionner une image sur la page web.

#### Appel du servlet {#calling-the-servlet}

Le servlet est lié aux ressources `cq:page` et prend en charge l’extension de fichier .jpg. Le sélecteur de servlet est `image`. Par conséquent, Sling résout les URL de requête HTTP au format suivant sur ce servlet :

`path-to-page-node.image.jpg`

Par exemple, Sling transfère des requêtes HTTP avec l’URL `http://localhost:4502/content/geometrixx/en.image.jpg` vers le servlet Image Reference Modification.

Trois sélecteurs supplémentaires définissent la largeur, la hauteur et (éventuellement) la qualité d’image demandées. L’exemple suivant demande une image d’une largeur de 770 pixels, d’une hauteur de 360 pixels et de qualité moyenne :

`http://localhost:4502/content/geometrixx/en.image.770.360.MEDIUM.jpg`

**Propriétés d’image prises en charge**

Le servlet accepte un nombre fini de dimensions d’image et de valeurs de qualité.

Les valeurs suivantes sont prises en charge par défaut (largeur x hauteur) :

* 256x192
* 370x150
* 480x200
* 127x127
* 770x360
* 620x290
* 480x225
* 320x150
* 375x175
* 303x142
* 1170x400
* 940x340
* 770x300
* 480x190

Les valeurs de qualité d’image ci-dessous sont prises en charge :

* faible
* moyenne
* élevée

Lorsque vous utilisez AEM, plusieurs méthodes de gestion des paramètres de configuration sont disponibles pour ces services ; pour en savoir plus, voir [Configuration d’OSGi](/help/sites-deploying/configuring-osgi.md).

#### Indication de la ressource d’image {#specifying-the-image-resource}

Le chemin d’accès de l’image, les dimensions et les valeurs de qualité doivent être stockés sous la forme de propriétés d’un nœud dans le référentiel :

* Le nom du noeud est `image`.
* Le noeud parent est le noeud `jcr:content` noeud d’un `cq:page` ressource.

* Le chemin d’accès de l’image est stocké en tant que valeur d’une propriété nommée `fileReference`.

Lors de la création d’une page, utilisez **Sidekick** pour spécifier l’image et ajouter le `image` noeud aux propriétés de la page :

1. Dans **Sidekick**, cliquez sur le bouton **Page** puis cliquez sur **Propriétés de la page**.
1. Cliquez sur le bouton **Image** et indiquez l’image.
1. Cliquez sur **OK**.

#### Détails de mise en œuvre {#implementation-details-1}

La classe info.geometrixx.commons.impl.servlets.ImageReferenceModificationServlet étend la propriété [AbstractImageServlet](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.html) classe . Si le package cq-geometrixx-commons-pkg est installé, le code source ImageReferenceModificationServlet se trouve dans la variable `/apps/geometrixx-commons/src/core/src/main/java/info/geometrixx/commons/impl/servlets` dossier.

La classe utilise les annotations SCR Felix pour configurer le type de ressource et l’extension de fichier auxquels le servlet est associé, ainsi que le nom du premier sélecteur.

```java
@Component(metatype = true, label = "Adobe CQ Image Reference Modification Servlet",
        description = "Render the image associated with a page in a variety of dimensions and qualities")
@Service
@Properties(value = {
    @Property(name = "sling.servlet.resourceTypes", value = NameConstants.NT_PAGE, propertyPrivate = true),
    @Property(name = "sling.servlet.selectors", value = "image", propertyPrivate = true),
    @Property(name = "sling.servlet.extensions", value = "jpg", propertyPrivate = true)
})
```

Le servlet utilise l’annotation SCR Property pour définir les dimensions et la qualité d’image prises en charge par défaut.

```java
@Property(label = "Image Quality",
            description = "Quality must be a double between 0.0 and 1.0", value = "0.82")
@Property(value = {
                "256x192", // Category page article list images
                "370x150", // "Most popular" desktop & iPad & carousel min-width: 1px
                "480x200", // "Most popular" phone
                "127x127", // article summary phone square images
                "770x360", // article summary, desktop
                "620x290", // article summary, tablet
                "480x225", // article summary, phone (landscape)
                "320x150", // article summary, phone (portrait) and fallback
                "375x175", // 2-column article summary, desktop
                "303x142", // 2-column article summary, tablet
                "1170x400", // carousel, full
                "940x340",  // carousel min-width: 980px
                "770x300",  // carousel min-width: 768px
                "480x190"   // carousel min-width: 480px
            },
            label = "Supported Resolutions",
            description = "List of resolutions this component is permitted to generate.")
```

Le `AbstractImageServlet` fournit la classe `doGet` qui traite la requête HTTP. Cette méthode détermine la ressource associée à l’appel , récupère les propriétés de ressource du référentiel et les enregistre dans un [ImageContext](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.ImageContext.html) .

Le `ImageReferenceModificationServlet` remplace la classe `createLayer` et met en oeuvre la logique qui détermine la ressource image à afficher. La méthode récupère un noeud enfant de la page `jcr:content` noeud nommé `image`. Un [Image](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/foundation/Image.html) est créé à partir de cet objet `image` et le noeud `getFileReference` renvoie le chemin d’accès au fichier image à partir de la propriété `fileReference` du noeud image.

>[!NOTE]
>Le [com.day.cq.commons.DownloadResource](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/DownloadResource.html) fournit la méthode getFileReferencemod.

## Développement d’une grille fluide {#developing-a-fluid-grid}

AEM permet une implémentation efficace de grilles fluides. Cette page explique comment intégrer votre grille fluide ou une mise en oeuvre de grille existante (telle que [Bootstrap](https://twitter.github.com/bootstrap/)) dans votre application AEM.

Si le concept des grilles fluides ne vous est pas familier, reportez-vous à la section [Présentation des grilles fluides](/help/sites-developing/responsive.md#developing-a-fluid-grid) au bas de cette page. Vous y trouverez une présentation des grilles fluides, ainsi que des conseils de conception.

### Définition de la grille à l’aide d’un composant Page {#defining-the-grid-using-a-page-component}

Utilisez les composants de page pour générer les éléments HTML qui définissent les blocs de contenu de la page. Le dossier de bibliothèque cliente (ClientLibraryFolder) auquel la page fait référence fournit le CSS qui contrôle la mise en page des blocs de contenu :

* Composant de page : ajoute des éléments div qui représentent des lignes de blocs de contenu. Les éléments div qui représentent des blocs de contenu comportent un composant parsys dans lequel les auteurs ajoutent du contenu.
* Dossier de bibliothèque cliente : fournit le fichier CSS contenant les requêtes de média et les styles pour les éléments div.

Par exemple, l’exemple d’application geometrixx-media contient le composant media-home. Ce composant insère deux scripts, lesquels génèrent deux éléments `div` de la classe `row-fluid` :

* La première ligne contient un élément `div` de la classe `span12` (le contenu s’étend sur 12 colonnes). L’élément `div` contient le composant parsys.

* La deuxième ligne contient deux `div` éléments, un de la classe `span8` et l’autre de la classe `span4`. Chaque élément `div` inclut le composant parsys.

```xml
<div class="page-content">
    <div class="row-fluid">
        <div class="span12">
            <cq:include path="grid-12-par" resourceType="foundation/components/parsys" />
        </div>
    </div>
    <div class="row-fluid">
        <div class="span8">
            <cq:include path="grid-8-par" resourceType="foundation/components/parsys" />
        </div>
        <div class="span4">
            <cq:include path="grid-4-par" resourceType="foundation/components/parsys" />
        </div>
    </div>
</div>
```

>[!NOTE]
>
>Lorsqu’un composant comprend plusieurs `cq:include` éléments qui font référence au composant parsys, chaque `path` doit avoir une valeur différente.

#### Mise à l’échelle de la grille du composant Page {#scaling-the-page-component-grid}

La conception associée au composant de page geometrixx-media (`/etc/designs/geometrixx-media`) contient la variable `clientlibs` ClientLibraryFolder. Ce dossier définit les styles CSS pour `row-fluid` classes, `span*` classes et `span*` classes qui sont des enfants de `row-fluid` classes. Les requêtes de média permettent de redéfinir les styles pour différentes tailles de fenêtre d’affichage.

L’exemple de CSS suivant est un sous-ensemble de ces styles. Ce sous-ensemble est axé sur `span12`, `span8`, et `span4` et requêtes de média pour deux tailles de fenêtre d’affichage. Notez les caractéristiques suivantes du CSS :

* Le `.span` Les styles définissent les largeurs d’élément à l’aide de nombres absolus.
* Le `.row-fluid .span*` Les styles définissent les largeurs d’élément en tant que pourcentage du parent. Les pourcentages sont calculés à partir des largeurs absolues.
* Les requêtes de média relatives à des fenêtres d’affichage plus grandes attribuent des largeurs absolues plus élevées.

>[!NOTE]
>
>L’exemple d’application Geometrixx Media intègre la structure JavaScript [Bootstrap](https://twitter.github.com/bootstrap/javascript.html) dans son implémentation de grille fluide. La structure Bootstrap fournit le fichier bootstrap.css.

```xml
/* default styles (no media queries) */
 .span12 { width: 940px }
 .span8 { width: 620px }
 .span4 { width: 300px }
 .row-fluid .span12 { width: 100% }
 .row-fluid .span8 { width: 65.95744680851064% }
 .row-fluid .span4 { width: 31.914893617021278% }

@media (min-width: 768px) and (max-width: 979px) {
 .span12 { width: 724px; }
 .span8 {     width: 476px; }
 .span4 {     width: 228px; }
 .row-fluid .span12 {     width: 100%;}
 .row-fluid .span8 {     width: 65.74585635359117%; }
 .row-fluid .span4 {     width: 31.491712707182323%; }
}

@media (min-width: 1200px) {
 .span12 { width: 1170px }
 .span8 { width: 770px }
 .span4 { width: 370px }
 .row-fluid .span12 { width: 100% }
 .row-fluid .span8 { width: 65.81196581196582% }
 .row-fluid .span4 { width: 31.623931623931625% }
}
```

#### Repositionnement du contenu dans la grille du composant Page {#repositioning-content-in-the-page-component-grid}

Dans l’exemple d’application Geometrixx Media, les lignes de blocs de contenu sont distribuées horizontalement dans les fenêtres larges. Dans les fenêtres plus petites, ces mêmes blocs sont distribués verticalement. L’exemple CSS suivant illustre les styles qui implémentent ce comportement pour le code HTML généré par le composant de page media-home :

* La page CSS par défaut de la page de bienvenue multimédia affecte la variable `float:left` style pour `span*` classes qui se trouvent à l’intérieur `row-fluid` classes.

* Les requêtes de média relatives aux fenêtres d’affichage plus petites affectent le style `float:none` pour ces mêmes classes.

```xml
/* default styles (no media queries) */
    .row-fluid [class*="span"] {
        width: 100%;
        float: left;
}

@media (max-width: 767px) {
    [class*="span"], .row-fluid [class*="span"] {
        float: none;
        width: 100%;
    }
}
```

#### Modularisation des composants de page {#tip-modularize-your-page-components}

Il est conseillé de modulariser les composants de page pour utiliser efficacement le code. Il est probable que votre site utilise différents types de pages, comme une page de bienvenue, une page d’article ou encore une page de produit. Le contenu affiché et la mise en page varient généralement en fonction du type de page. Cependant, lorsque des éléments d’une mise en page se retrouvent sur plusieurs pages, vous pouvez réutiliser le code qui implémente cette partie de la mise en page.

**Utilisation d’incrustations de composants de page**

Créez un composant de page principal qui fournit des scripts pour générer les différentes parties d’une page, telles que `head` et `body` sections et `header`, `content`, et `footer` dans le corps.

Créez d’autres composants de page qui utilisent le composant de page principal en tant que `cq:resourceSuperType`. Ces composants comprennent des scripts qui remplacent les scripts de la page principale suivant les besoins.

Par exemple, l’application geometrixx-media comprend le composant de page (`sling:resourceSuperType` est le composant de page de base). Plusieurs composants enfants (tels que article, category et media-home) utilisent ce composant de page en tant `sling:resourceSuperType`. Chaque composant enfant contient un fichier content.jsp qui remplace le fichier content.jsp du composant de page.

**Réutilisation de scripts**

Créez des scripts JSP qui génèrent des combinaisons de lignes et de colonnes communes à plusieurs composants de page. Par exemple, la variable `content.jsp` le script de l’article et les composants media-home font tous deux référence à la fonction `8x4col.jsp` script.

**Organisation des styles CSS par taille de fenêtre d’affichage ciblée**

Insérez les styles CSS et les requêtes de média relatifs à différentes tailles de fenêtre dans des fichiers distincts. Utilisez des dossiers de bibliothèques clientes pour les concaténer.

### Insérer des composants dans la grille de page {#inserting-components-into-the-page-grid}

Lorsque les composants génèrent un seul bloc de contenu, la grille définie par le composant de page contrôle généralement le positionnement du contenu.

Les auteurs doivent comprendre que le bloc de contenu peut être rendu selon différentes tailles et positions relatives. Le texte de contenu ne doit pas utiliser de directions relatives pour faire référence à d’autres blocs de contenu.

Si nécessaire, le composant doit fournir toutes les bibliothèques CSS ou JavaScript requises pour le code HTML qu’il génère. Utilisez un dossier de bibliothèque cliente au sein du composant pour générer les fichiers CSS et JS. Pour exposer les fichiers, [créez une dépendance ou incorporez la bibliothèque](/help/sites-developing/clientlibs.md#creating-client-library-folders) dans un autre dossier de bibliothèque cliente sous /etc. 

**Sous-grilles**

Si le composant comporte plusieurs blocs de contenu, ajoutez-les à l’intérieur d’une ligne pour créer une sous-grille sur la page :

* Utilisez les mêmes noms de classe que le composant de page conteneur pour exprimer des éléments div sous la forme de lignes et de blocs de contenu.
* Pour remplacer le comportement appliqué par le CSS de la conception de page, utilisez un deuxième nom de classe pour l’élément div de la ligne et fournissez le CSS associé dans un dossier de bibliothèque cliente.

Par exemple, la variable `/apps/geometrixx-media/components/2-col-article-summary` génère deux colonnes de contenu. Le code HTML généré présente la structure suivante :

```xml
<div class="row-fluid mutli-col-article-summary">
    <div class="span6">
        <article>
            <div class="article-summary-image">...</div>
            <div class="social-header">...</div>
            <div class="article-summary-description">...</div>
            <div class="social">...</div>
        </article>
    </div>
</div>
```

Le `.row-fluid .span6` les sélecteurs du CSS de la page s’appliquent à la variable `div` éléments de la même classe et structure dans ce HTML. Cependant, le composant comprend également le dossier de bibliothèque cliente /apps/geometrixx-media/components/2-col-article-summary/clientlibs :

* Le CSS utilise les mêmes requêtes de média que le composant de page pour procéder à des changements de mise en page au niveau des mêmes largeurs discrètes.
* Les sélecteurs utilisent la classe `multi-col-article-summary` de l’élément `div` de la ligne pour remplacer le comportement de la classe `row-fluid` de la page.

Par exemple, les styles suivants sont inclus dans la variable `/apps/geometrixx-media/components/2-col-article-summary/clientlibs/css/responsive-480px.css` fichier :

```xml
@media (max-width: 480px) {
    .mutli-col-article-summary .article-summary-image {
        float: left;
        width: 127px;
    }
    .mutli-col-article-summary .article-summary-description {
        width: auto;
        margin-left: 127px;
    }
    .mutli-col-article-summary .article-summary-description h4 {
        padding-left: 10px;
    }
    .mutli-col-article-summary .article-summary-text {
        margin-left: 127px;
        min-height: 122px;
        top: 0;
    }
}
```

## Présentation des grilles fluides {#introduction-to-fluid-grids}

Les grilles fluides permettent aux mises en page de s’adapter aux dimensions de la fenêtre d’affichage du client. Les grilles sont constituées de lignes et de colonnes logiques qui positionnent les blocs de contenu sur la page.

* Les colonnes déterminent les largeurs et les positions horizontales des blocs de contenu.
* Les lignes déterminent les positions verticales relatives des blocs de contenu.

La technologie HTML5 vous permet d’implémenter la grille et de la manipuler afin d’adapter les mises en page à différentes tailles de fenêtre :

* HTML `div` Les éléments contiennent des blocs de contenu qui s’étendent sur un certain nombre de colonnes.
* Un ou plusieurs de ces éléments div se composent d’une ligne lorsqu’ils partagent un développement parent commun.

### Utiliser des largeurs discrètes {#using-discrete-widths}

Pour chaque plage de largeurs de fenêtre que vous ciblez, utilisez une largeur de page statique et des blocs de contenu de largeur constante. Lors du redimensionnement manuel d’une fenêtre de navigateur, les modifications apportées à la taille du contenu s’opèrent au niveau des largeurs de fenêtre discrètes (connues également sous le nom de points d’arrêt). En conséquence, les conceptions de page sont respectées de façon plus rigoureuse, optimisant ainsi l’expérience utilisateur.

#### Mise à l’échelle de la grille {#scaling-the-grid}

Utilisez des grilles pour redimensionner les blocs de contenu à adapter à différentes tailles de fenêtre. Les blocs de contenu s’étendent sur un nombre spécifique de colonnes. La largeur des blocs de contenu augmente ou diminue à mesure que la largeur des colonnes s’adapte à la taille des fenêtres d’affichage. La mise à l’échelle peut prendre en charge les fenêtres de grande taille et de taille moyenne qui sont suffisamment larges pour permettre l’affichage des blocs de contenu côte à côte.

![](do-not-localize/chlimage_1-1a.png)

#### Repositionnement du contenu dans la grille {#repositioning-content-in-the-grid}

La taille des blocs de contenu peut être limitée par une largeur minimale au-delà de laquelle la mise à l’échelle n’est plus efficace. Dans le cas des fenêtres plus petites, la grille peut être utilisée pour répartir des blocs de contenu verticalement plutôt qu’horizontalement.

![](do-not-localize/chlimage_1-2a.png)

### Concevoir la grille {#designing-the-grid}

Déterminez les colonnes et les lignes dont vous avez besoin pour positionner les blocs de contenu sur vos pages. Les mises en page déterminent le nombre de colonnes et de lignes qui s’étendent sur votre grille.

**Nombre de colonnes**

Insérez suffisamment de colonnes pour positionner horizontalement les blocs de contenu dans toutes vos mises en page et pour toutes les tailles de fenêtre. Il est conseillé d’utiliser plus de colonnes que ce qui est actuellement nécessaire pour prendre en charge les futures conceptions de page.

**Contenu de ligne**

Utilisez des lignes pour contrôler le positionnement vertical des blocs de contenu. Déterminez les blocs de contenu qui partagent la même ligne :

* Les blocs de contenu situés les uns à côté des autres horizontalement dans n’importe quelle mise en page se trouvent dans la même ligne.
* Les blocs de contenu situés les uns à côté des autres horizontalement (fenêtres plus larges) et verticalement (fenêtres plus petites) se trouvent dans la même ligne.

### Mises en oeuvre de grille {#grid-implementations}

Créez des styles et des classes CSS pour contrôler la disposition des blocs de contenu sur une page. Les conceptions de page dépendent souvent de la position et de la taille relatives des blocs de contenu dans la fenêtre d’affichage. La fenêtre détermine la taille réelle des blocs de contenu. Votre CSS doit prendre en compte les tailles relatives et absolues. Vous pouvez implémenter une grille fluide à l’aide de trois types de classes CSS :

* Une classe pour une `div` élément qui est un conteneur pour toutes les lignes. Cette classe définit la largeur absolue de la grille.
* Une classe pour `div` qui représentent une ligne. Cette classe contrôle le positionnement horizontal ou vertical des blocs de contenu qui y sont inclus.
* Classes pour des éléments `div` qui représentent des blocs de contenu de largeurs différentes. Les largeurs sont exprimées en tant que pourcentage du parent (la ligne).

Les largeurs de fenêtre ciblées (et les requêtes de média qui y sont associées) définissent les largeurs discrètes utilisées pour une mise en page.

#### Largeurs des blocs de contenu {#widths-of-content-blocks}

En règle générale, le style `width` des classes de blocs de contenu repose sur les caractéristiques suivantes de votre page et de votre grille :

* Largeur de page absolue que vous utilisez pour chaque taille de fenêtre ciblée. Il s’agit de valeurs connues.
* Largeur absolue des colonnes de la grille pour chaque largeur de page. Il vous appartient de déterminer ces valeurs.
* Largeur relative de chaque colonne en tant que pourcentage de la largeur totale de la page. Il vous appartient de calculer ces valeurs.

Le CSS comprend une série de requêtes de média qui utilisent la structure suivante :

```xml
@media(query_for_targeted_viewport){

  .class_for_container{ width:absolute_page_width }
  .class_for_row { width:100%}

  /* several selectors for content blocks   */
  .class_for_content_block1 { width:absolute_block_width1 }
  .class_for_content_block2 { width:absolute_block_width2 }
  ...

  /* several selectors for content blocks inside rows */
  .class_for_row .class_for_content_block1 { width:relative_block_width1 }
  .class_for_row .class_for_content_block2 { width:relative_block_width2 }
  ...
}
```

Utilisez l’algorithme suivant comme point de départ pour développer les classes d’éléments et les styles CSS de vos pages.

1. Définissez un nom de classe pour l’élément div contenant toutes les lignes ; `content.`, par exemple.
1. Définissez une classe CSS pour les éléments div qui représentent des lignes, comme `row-fluid`.
1. Définissez des noms de classe pour les éléments de bloc de contenu. Une classe est requise pour toutes les largeurs possibles, en termes d’étendues de colonnes. Utilisez, par exemple, la classe `span3` pour les éléments `div` qui s’étendent sur 3 colonnes et `span4` pour les étendues de 4 colonnes. Définissez autant de classes qu’il y a de colonnes dans votre grille.

1. Pour chaque taille de fenêtre que vous ciblez, ajoutez la requête de média correspondante à votre fichier CSS. Ajoutez les éléments suivants dans chaque requête de média :

   * Un sélecteur pour la `content` par exemple, `.content{}`.
   * Sélecteurs pour chaque classe d’étendue, par exemple `.span3{ }`.
   * Un sélecteur pour la `row-fluid` par exemple, `.row-fluid{ }`
   * Sélecteurs pour les classes span qui se trouvent à l’intérieur des classes row-fluid, par exemple `.row-fluid span3 { }`.

1. Ajout des styles width pour chaque sélecteur :

   1. Définissez la largeur des sélecteurs `content` sur la taille absolue de la page ; `width:480px`, par exemple.
   1. Définissez la largeur de tous les sélecteurs row-fluid sur 100 %.
   1. Définissez la largeur de tous les sélecteurs d’étendue sur la largeur absolue du bloc de contenu. Une grille triviale utilise des colonnes uniformément réparties de la même largeur : `(absolute width of page)/(number of columns)`.
   1. Définissez la largeur de la variable `.row-fluid .span` sélecteurs en pourcentage de la largeur totale. Calculez cette largeur à l’aide du `(absolute span width)/(absolute page width)*100` formule

#### Positionnement des blocs de contenu dans des lignes {#positioning-content-blocks-in-rows}

Utilisez le style flottant du `.row-fluid` pour contrôler si les blocs de contenu d’une ligne sont disposés horizontalement ou verticalement.

* Le `float:left` ou `float:right` style provoque la distribution horizontale des éléments enfants (blocs de contenu).

* Le `float:none` style provoque la distribution verticale des éléments enfants.

Ajoutez le style au `.row-fluid` sélecteur à l’intérieur de chaque requête de média. Définissez la valeur en fonction de la mise en page que vous utilisez pour cette requête de média. Par exemple, le schéma ci-dessous illustre une ligne qui répartit le contenu horizontalement pour les fenêtres larges et verticalement pour les fenêtres étroites.

![](do-not-localize/chlimage_1-3a.png)

Le code CSS suivant peut implémenter ce comportement :

```xml
@media (min-width: 768px) and (max-width: 979px) {
   .row-fluid {
       width:100%;
       float:left
   }
}

@media (max-width:480px){
    .row-fluid {
       width:100%;
       float:none
   }
}
```

#### Attribution de classes aux blocs de contenu {#assigning-classes-to-content-blocks}

Pour la mise en page de chaque taille de fenêtre que vous ciblez, déterminez le nombre de colonnes couvertes par chaque bloc de contenu. Déterminez ensuite la classe à utiliser pour les éléments div de ces blocs de contenu.

Après avoir créé les classes div, vous pouvez implémenter la grille à l’aide de votre application AEM.
