---
title: Extension et configuration de l’importateur de conception pour les pages d’entrée
seo-title: Extension et configuration de l’importateur de conception pour les pages d’entrée
description: Découvrez comment configurer l’importateur de conception pour les pages d’entrée.
seo-description: Découvrez comment configurer l’importateur de conception pour les pages d’entrée.
uuid: a2dd0c30-03e4-4e52-ba01-6b0b306c90fc
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: e02f5484-fbc2-40dc-8d06-ddb53fd9afc2
docset: aem65
translation-type: tm+mt
source-git-commit: 0a94bf49a7136c5831c42eb274d07517c12014ec
workflow-type: tm+mt
source-wordcount: '3522'
ht-degree: 76%

---


# Extension et configuration de l’importateur de conception pour les pages d’entrée{#extending-and-configuring-the-design-importer-for-landing-pages}

Cette section décrit la configuration et, si vous le souhaitez, l’extension de l’importateur de conception pour les pages d’entrée. L’utilisation de pages d’entrée après l’importation est décrite dans la section [Pages d’entrée](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md).

**Faire en sorte que l’importateur de conception extraie votre composant personnalisé**

Voici les étapes logiques à suivre pour faire en sorte que l’importateur reconnaisse votre composant personnalisé.

1. Création d’un gestionnaire de balises

   * Un gestionnaire de balises est un POJO (Plain Old Java Object) qui traite les balises HTML d’un type spécifique. Le « type » des balises HTML que votre TagHandler peut traiter est défini au moyen de la propriété OSGi « tagpattern.name » de TagHandlerFactory. Cette propriété OSGi est en réalité une expression régulière (regex) qui doit correspondre à la balise HTML en entrée que vous souhaitez traiter. Toutes les balises imbriquées sont envoyées pour traitement à votre gestionnaire de balises. Par exemple, si vous enregistrez une balise &lt;div> contenant une balise &lt;p> imbriquée, la balise &lt;p> est également envoyée vers le gestionnaire de balises. Il vous appartiendra alors d’en déterminer le mode de traitement.
   * L’interface du gestionnaire de balises est semblable à une interface de gestion de contenu SAX. Elle reçoit des événements SAX pour chaque balise HTML. En votre qualité de fournisseur de gestionnaire de balises, vous devez mettre en œuvre certaines méthodes de cycle de vie qui sont appelées automatiquement par le cadre de l’importateur de conception.

1. Créez le composant TagHandlerFactory correspondant.

   * TagHandlerFactory est un composant OSGi (singleton) responsable du déclenchement d’instances sur votre gestionnaire de balises.
   * Votre TagHandlerFactory doit exposer une propriété OSGi appelée « tagpattern.name » dont la valeur est comparée à la balise HTML d’entrée.
   * Si plusieurs gestionnaires de tags correspondent au tag HTML en entrée, celui dont le classement est le plus élevé est choisi. The ranking itself is exposed as an OSGi property **service.ranking**.
   * TagHandlerFactory est un composant OSGi. Toute référence que vous souhaitez attribuer à votre TagHandler doit l’être par ce biais.

1. Assurez-vous que votre composant TagHandlerFactory présente un meilleur classement si vous souhaitez ignorer la valeur par défaut.

>[!CAUTION]
>
>L’importateur de conception, utilisé pour importer des pages d’entrée, [est obsolète avec AEM 6.5](/help/release-notes/deprecated-removed-features.md#deprecated-features).

## Préparation du fichier HTML pour l’importation {#preparing-the-html-for-import}

Après avoir créé une page d’importation, vous pouvez importer votre page d’entrée HTML dans son intégralité. Pour importer votre page d’entrée HTML, vous devez d’abord compresser son contenu dans un module de conception. Le module de conception contient votre page d’entrée HTML, ainsi que les ressources référencées (images, css, icônes, scripts, etc.).

L’aide-mémoire ci-dessous décrit la préparation de votre fichier HTML en vue de l’importation :

Aide-mémoire de page d’entrée

[Obtenir le fichier](assets/cheatsheet.zip)

### Disposition du fichier ZIP et exigences {#zip-file-layout-and-requirements}

>[!NOTE]
>
>Pour l’heure, les fichiers zip ne peuvent contenir qu’une seule page HTML ou une partie de page.

Voici un exemple de disposition de fichier ZIP :

* /index.html -> fichier HTML de page d’entrée
* /css -> à ajouter dans la bibliothèque client CSS
* /img -> ensemble des images et des actifs
* /js -> à ajouter à la bibliothèque client JS

La mise en page s’appuie sur les meilleures pratiques HTML5 Boilerplate. Read more at [https://html5boilerplate.com/](https://html5boilerplate.com/)

>[!NOTE]
>
>Le module de conception **doit** contenir, au minimum, un fichier **index.html** au niveau racine. Au cas où la page d’entrée à importer comporterait également une version pour mobiles, le fichier ZIP doit contenir un fichier **mobile.index.html** en complément du fichier **index.html** au niveau racine.

### Préparation du fichier HTML de la page d’entrée {#preparing-the-landing-page-html}

Pour qu’il soit possible d’importer le fichier HTML, vous devez ajouter une balise &lt;div> de canevas au fichier HTML de la page d’entrée.

The canvas div is an html **div** with `id="cqcanvas"` that must be inserted within the HTML `<body>` tag and must wrap the content intended for conversion.

Vous trouverez, ci-dessous, un exemple de fragment de code du fichier HTML de la page d’entrée de la balise &lt;div> du canevas :

```xml
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title></title>
  <meta name="description" content="">
</head>
<body>
 <div id="cqcanvas">
  <!-- HTML content intended for conversion -->
 </div>
</body>
</html>
```

### Préparation du fichier HTML en vue d’inclure des composants AEM modifiables {#preparing-the-html-to-include-editable-aem-components}

Lorsque vous importez une page d’entrée, vous pouvez choisir de l’importer telle quelle. Cela signifie qu’une fois la page importée, vous ne pourrez modifier aucun des éléments importés dans AEM (vous pourrez toutefois ajouter des composants AEM sur la page).

Avant d’importer la page d’entrée, vous pouvez en convertir certaines parties pour en faire des composants AEM modifiables. Cela vous permettra de modifier rapidement des parties de la page d’entrée, même après en avoir importé la conception.

Pour ce faire, ajoutez `data-cq-component` au composant approprié dans le fichier HTML importé.

La section suivante décrit la modification de votre fichier HTML de manière à convertir certaines parties de vos pages d’entrée en différents composants AEM modifiables. Les composants sont décrits en détail dans la section [Composants Pages d’entrée](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md).

>[!NOTE]
>
>Les balises HTML destinées à la conversion de parties de la page d’entrée en composants AEM comportent une déclaration de balises de forme longue et de forme courte. Toutes deux sont décrites pour chaque composant.

### Restrictions {#limitations}

Avant de procéder à l’importation, veuillez tenir compte des restrictions suivantes :

### Les attributs, tels que class ou id, appliqués à  la balise &amp;lt;body> ne sont pas conservés. {#any-attribute-like-class-or-id-applied-on-the-amp-lt-body-tag-is-not-preserved}

If any attribute like id or class is applied on the body tag for example `<body id="container">` then it is not preserved after the import. So the design being imported should not have any dependencies on the attributes applied on the `<body>` tag.

### Transfert de fichiers ZIP par glisser-déposer {#drag-and-drop-zip}

Le transfert par glisser-déposer de fichiers zip n’est pas pris en charge pour Internet Explorer et Firefox versions 3.6 et antérieures. Pour télécharger une conception à l’aide de ces navigateurs, cliquez sur la zone de déplacement de fichiers afin d’ouvrir une boîte de dialogue de téléchargement et de l’utiliser pour réaliser le transfert.

Les navigateurs qui prennent en charge le « glisser-déposer » du fichier ZIP de conception sont Chrome, Safari 5.x, Firefox 4 et versions ultérieures.

### Modernizr n’est pas pris en charge {#modernizr-is-not-supported}

`Modernizr.js` est un outil JavaScript qui détecte les fonctionnalités natives des navigateurs et détermine si elles sont adaptées ou non aux éléments HTML5. Les conceptions qui utilisent Modernizr pour améliorer la prise en charge dans les versions plus anciennes des différents navigateurs peuvent entraîner des problèmes d’importation dans la solution de page d’entrée. Les scripts `Modernizr.js` ne sont pas pris en charge avec l’importateur de conception.

### Les propriétés de page ne sont pas conservées lors de l’importation du module de conception {#page-properties-are-not-preserved-at-the-time-of-importing-design-package}

Toute propriété de page (par exemple, Custom Domain, Enforcing HTTPS, etc.) définie pour une page (qui utilise le modèle Page d’entrée vierge) avant d’importer le module de conception est perdue une fois l’importation réalisée. Il est donc conseillé de définir les propriétés de la page après l’importation du module de conception.

### Balises HTML {#html-only-markup-assumed}

Lors de lʼimportation, le balisage est nettoyé pour des raisons de sécurité et afin dʼéviter lʼimportation et la publication de balisage non valide. Cela suppose que les balises HTML et que toutes les autres formes dʼéléments, tels que les SVG ou les composants web intégrés, seront filtrés.

### Texte {#text}

Balise HTML permettant d’insérer un composant texte (`foundation/components/text`) dans le fichier HTML à l’intérieur du module de conception :

```xml
<div data-cq-component="text"> <p>This is some editable text</p> </div>
```

L’insertion des balises ci-dessus dans le fichier HTML produit les effets suivants :

* Creates an editable AEM text component ( `sling:resourceType=foundation/components/text`) in the landing page created after importing the design package.
* Définition de la propriété `text` du composant texte créé sur le code HTML placé entre les balises `div`.

**Forme courte de la déclaration de balise du composant** :

```xml
<p data-cq-component="text">Text component shorthand</p>
```

**Texte avec liste**

Pour ajouter du texte avec une liste, procédez comme suit :

* 1er
* 2e

pouvant être modifié dans l’éditeur RTE :

```xml
<div data-cq-component="text"><p>This is text with a list:</p><ul><li>1st</li><li>2nd</li></ul><p>It can be edited with the RTE editor</p></div>
```

**Texte avec couleur**

Pour ajouter du texte de couleur rose pouvant être modifié dans l’éditeur RTE

```xml
<div class="pink" data-cq-component="text"><p>This is pink text.</p><p>It can be edited with the RTE editor</p></div>
```

### Titre {#title}

HTML markup to insert a title component ( `wcm/landingpage/components/title`) in the HTML within design package:

```xml
<div data-cq-component="title"> <h1>This is some editable title text</h1> </div>
```

L’insertion des balises ci-dessus dans le fichier HTML produit les effets suivants :

* Creates an editable AEM title component ( `sling:resourceType=wcm/landingpage/components/title`) in the landing page created after importing the design package.
* Définition de la propriété `jcr:title` du composant de titre créé sur le texte dans la balise d’en-tête (heading) placé entre balises div.
* Définition de la propriété `type` sur la balise d’en-tête (heading) ; dans ce cas `h1`.

Le composant de titre prend en charge 7 types - `h1, h2, h3, h4, h5, h6` et `default`.

**Forme courte de la déclaration de balise du composant** :

```xml
<h1 data-cq-component="title">Title component shorthand</h1>
```

### Image {#image}

Balise HTML permettant d’insérer un composant image (foundation/components/image) dans le fichier HTML à l’intérieur du module de conception :

```xml
<div data-cq-component="image">
<img src="img/video1.png" alt="Video about Polar Brake Goggles in action" title="Polar Brake Goggles" width="300" height="200" />
</div>
```

L’insertion des balises ci-dessus dans le fichier HTML produit les effets suivants :

* Creates an editable AEM image component ( `sling:resourceType=foundation/components/image`) in the landing page created after importing the design package.
* Définition de la propriété `fileReference` du composant image créé sur le chemin d’importation de l’image spécifiée dans l’attribut src.
* Sets the `alt` property to the value of alt attribute in the img tag.
* Sets the `title` property to the value of title attribute in the img tag.
* Sets the `width` property to the value of width attribute in the img tag.
* Sets the `height` property to the value of height attribute in the img tag.

**Forme courte de la déclaration de balise du composant** :

```xml
<img data-cq-component="image" src="test.png" alt="Image component shorthand"/>
```

#### Source d’image d’URL absolue non prise en charge dans la balise &lt;div> du composant image {#absolute-url-img-src-not-supported-within-image-component-div}

If an `<img>` tag with an absolute url src is attempted for component conversion, an appropriate **UnsupportedTagContentException** is raised. Par exemple, le code suivant n’est pas pris en charge :

`<div data-cq-component="image">`

`<img src="https://cdn.printfriendly.com/pf-button.gif" alt="Print Friendly and PDF"/>`

`</div>`

Sinon, les images URL absolues sont prises en charge pour les balises img qui ne font pas partie d’une balise &lt;div> de composant image.

### Composants CTA (Appel à l’action) {#call-to-action-components}

Vous pouvez marquer une partie de la page d’entrée pour l’importation sous forme de « composant CTA modifiable ». Les composants de ce type peuvent être modifiés après l’importation de la page d’entrée. AEM inclut les composants CTA suivants :

* Lien des clics publicitaires - Permet d’ajouter un lien texte cliquable qui dirige l’utilisateur vers une URL cible.
* Lien graphique : permet d’ajouter une image cliquable qui redirige l’utilisateur vers une URL cible.

#### Lien des clics publicitaires {#click-through-link}

Vous pouvez utiliser ce composant CTA pour ajouter le lien texte sur la page d’entrée.

Propriétés prises en charge

* Libellé, avec les options « gras », « italique » et « souligné »
* URL cible, prise en charge d’URL tierces et AEM
* Options de rendu de page (même fenêtre, nouvelle fenêtre, etc.)

Balise HTML permettant d’inclure le composant « clics publicitaires » dans le fichier ZIP importé. Dans ce cas, &lt;href> est mis en correspondance avec l’adresse URL cible. « Afficher les détails du produit » est mis en correspondance avec le libellé, etc.

```xml
<div id="cqcanvas">
.
.
                <div data-cq-component="clickThroughLink">
        <a href="/content/we-retail/us/en/products/equipment/snow-sports/flying-snowboard.html">View Product Details  ></a>
  </div>
.
.
</div>
```

Ce composant peut être utilisé dans n’importe quelle application autonome ou importé à partir du fichier ZIP.

**Forme courte de la déclaration de balise du composant** :

```xml
<a href="/somelink.html" data-cq-component="clickThroughLink">Click Through Link shorthand</a>
```

#### Lien graphique {#graphical-link}

Vous pouvez utiliser ce composant CTA pour ajouter une image graphique avec un lien sur la page d’entrée. Il peut s’agir d’un simple bouton ou d’une image en arrière-plan. Lorsque l’utilisateur clique sur l’image, il accède à l’URL cible spécifiée dans les propriétés du composant. Elle fait partie du groupe « Appel à l’action ».

Propriétés prises en charge

* Recadrage et rotation d’images
* Test de pointage, description, taille en pixels
* URL cible, prise en charge d’URL tierces et AEM
* Options de rendu de page (même fenêtre, nouvelle fenêtre, etc.)

Balise HTML permettant d’inclure le composant « lien graphique » dans le fichier ZIP importé. Dans le cas présent, &lt;href> est mis en correspondance avec l’adresse URL cible, &lt;img src> est l’image de rendu, « titre » est utilisé comme texte affiché au survol, etc.

```xml
<div id="cqcanvas">
  <div data-cq-component="clickThroughGraphicalLink"><a href="https://www.adobe.com/go/wem"><img src="img/call-to-action-button.png" title="Click Here to Learn More" /></a></div>
</div>
```

**Forme courte de la déclaration de balise du composant** :

```xml
<a href="/somelink.html" data-cq-component="clickThroughGraphicalLink"><img src="linkimage.png" alt="Click Through Graphical Link shorthand"/></a>
```

>[!NOTE]
>
>To create a clickthroughgraphical link, you need to wrap an anchor tag and the image tag inside a div with `data-cq-component="clickthroughgraphicallink"` attribute.
>
>Par exemple`<div data-cq-component="clickthroughlink"> <a href="https://myURLhere/"><img src="image source here"></a> </div>`
>
>Les autres méthodes d’association d’une image avec une balise anchor à l’aide de CSS ne sont pas prises en charge. Ainsi, les balises suivantes ne fonctionnent pas :
>
>`<div data-cq-component="clickthroughgraphicallink">`
>
>`<a class="hasBackground" href="https://myURLhere/"></a>`
>
>`</div>`
>
>associé à `css .hasbackground { background-image: pathtoimage }`


### Formulaire de piste {#lead-form}

Le formulaire de piste est utilisé pour collecter des informations sur le profil d’un visiteur/prospect. Ces informations pourront être stockées et exploitées ultérieurement pour mener une campagne marketing efficace. Il s’agit généralement du titre, du nom, de l’adresse électronique, de la date de naissance, de l’adresse, du centre d’intérêt, etc. Il fait partie du groupe &quot;Formulaire de piste CTA&quot;.

**Fonctionnalités prises en charge**

* Les champs de piste prédéfinis - prénom, nom, adresse, dob, genre, about, userId, emailId, submit button sont disponibles dans le sidekick. Il vous suffit de faire glisser le composant requis dans votre formulaire de piste.
* Grâce à ces composants, l’auteur peut concevoir un formulaire de piste autonome. Ces champs correspondent à ceux du formulaire de piste. Dans une application ZIP importée ou autonome, l’utilisateur peut ajouter des champs à l’aide des champs de formulaire de prospect cq:form ou cta, les nommer et les concevoir en fonction des besoins.
* Faites correspondre les champs de formulaire de piste à l&#39;aide de noms prédéfinis spécifiques du formulaire de piste CTA, par exemple, firstName pour le prénom dans le formulaire de piste, etc.
* Les champs qui ne sont pas mis en correspondance avec un formulaire de piste le sont avec des composants cq:form : texte, case d’option, case à cocher, liste déroulante, masqué, mot de passe.
* L’utilisateur peut fournir le titre à l’aide de la balise « label » et indiquer le style en utilisant l’attribut de style « class » (disponible uniquement pour les composants du formulaire de prospect CTA).
* La page de remerciement et la liste d&#39;abonnement peuvent être fournies en tant que paramètre masqué du formulaire (présent dans index.htm) ou peuvent être ajoutées/modifiées à partir de la barre d&#39;édition de &quot;Début du formulaire de piste&quot;

   &lt;input type=&quot;hidden&quot; name=&quot;redirectUrl&quot; value=&quot;/content/we-commerce/fr/user/register/Thank_you&quot;/>

   &lt;input type=&quot;hidden&quot; name=&quot;groupName&quot; value=&quot;leadForm&quot;/>

* Des contraintes telles que - requises peuvent être fournies à partir de la configuration de modification de chaque composant.

Balise HTML permettant d’inclure le composant « lien graphique » dans le fichier ZIP importé. En l’occurrence, « firstName » est mis en correspondance avec le formulaire de piste firstName etc., à l’exception des cases à cocher. Ces deux cases à cocher sont mises en correspondance avec le composant Liste déroulante cq:form.

```xml
<div id="cqcanvas">
   <div id="form_wrapper">
    <h2>NEWSLETTER SIGN UP</h2>
       <div data-cq-component="leadFormGeneration">
       <form method="post" action="#" onsubmit="return popupBox()">
       <label for="firstName" class="checkText">
        FIRST NAME
       </label><br />
       <input name="firstName" class="text pink" type="text" /><br />
       <label for="lastName" class="checkText">
        LAST NAME
       </label><br />
       <input name="lastName" class="text pink" type="text" /><br />
       <label for="emailId" class="checkText">
        EMAIL ADDRESS
       </label><br />
       <input name="emailId" class="text pink" type="text" /><br />

       <div class="checkboxes">
       <input type="checkbox" class="check" name="send_news" /> <label for="send_news" class="checkText">Send me the latest We.Retail news and announcements.</label><br />
       <input type="checkbox" class="check" name="send_offers" /> <label for="send_offers" class="checkText">Send me We.Retail deals and special offers.</label><br />
       </div>
       <input type="submit" name="submit" class="submit pink" value="Sign Up >" />
       </form>
     </div>
   </div>
```

### Parsys {#parsys}

Le composant parsys d’AEM est un composant conteneur qui peut contenir d’autres composants AEM. Il est possible d’ajouter un composant parsys dans le fichier HTML importé. Cela permet à l’utilisateur d’ajouter des composants AEM modifiables à la page d’entrée, ou de les supprimer, après l’importation.

Le système de paragraphes offre aux utilisateurs la possibilité d’ajouter des composants à l’aide du Sidekick.

Balise HTML permettant d’insérer un composant parsys (`foundation/components/parsys`) dans le fichier HTML à l’intérieur du module de conception :

```xml
<div data-cq-component="parsys">
   <div data-cq-component="title"><h2>ULTIMATE PROTECTION</h2></div>
        <div data-cq-component="title"><h3>ON SALE</h3></div>
</div>
```

L’insertion des balises ci-dessus dans le fichier HTML produit les effets suivants :

* Insertion d’un composant parsys AEM (foundation/components/parsys) dans la page d’entrée créée après l’importation du module de conception.
* Initialisation du Sidekick avec des composants par défaut. Il est possible d’ajouter de nouveaux composants à la page d’entrée en les faisant glisser depuis le Sidekick vers le composant parsys.
* Deux composants titre font également partie du système de paragraphes (parsys).

### Cible {#target}

Le composant cible affiche le contenu d’une expérience sur la page : Il se peut que de nombreuses expériences aient été créées dans une campagne et que le composant cible affiche, de manière dynamique, le contenu issu de diverses expériences aux différents internautes qui consultent la page.

Balise HTML permettant d’insérer un composant cible et aussi de créer différentes expériences dans une campagne :

```xml
<div data-cq-component="target">
 <section data-cq-component="experience" data-cq-experience="default">
  <p data-cq-component="text">Default content. Select this campaign in client context to view other experiences</p>
 </section>

 <section data-cq-component="experience" data-cq-segment="over-30">
  <p data-cq-component="text">Content for Over 30</p>
 </section>

 <section data-cq-component="experience" data-cq-segment="under-30">
  <p data-cq-component="text">Content for Under 30</p>
 </section>
</div>
```

## Options d’importation supplémentaires {#additional-importing-options}

Outre l’identification des composants importés comme étant des composants AEM modifiables ou non, vous pouvez configurer les éléments suivants avant d’importer le module de conception :

* Définition des propriétés de page en extrayant les métadonnées définies dans le fichier HTML importé.
* Indication du codage du jeu de caractères dans le fichier HTML.
* Recouvrement du modèle de page d’importation.

### Définition des propriétés de page en extrayant les métadonnées définies dans le fichier HTML importé {#setting-page-properties-by-extracting-metadata-defined-in-imported-html}

Les métadonnées ci-dessous déclarées dans l’en-tête du fichier HTML importé doivent être extraites et conservées par l’importateur de conception sous forme de propriété « jcr:description » :

* &lt;meta name=&quot;description&quot; content=&quot;&quot;>

L’attribut Lang défini dans la balise HTML doit être extrait et conservé par l’importateur de conception sous forme de propriété « jcr:language » :

* &lt;html lang=&quot;en&quot;>

### Indication du codage du jeu de caractères dans le fichier HTML {#specifying-the-charset-encoding-in-the-html}

L’importateur de conception lit le codage spécifié dans le fichier HTML importé. Le codage peut être spécifié comme suit :

`<meta charset="UTF-8">`

*OU*

`<meta http-equiv="content-type" content="text/html;charset=utf-8">`

Si aucun codage n’est spécifié dans le fichier HTML importé, le codage par défaut défini par l’importateur de conception est UTF-8.

### Recouvrement du modèle {#overlaying-template}

The Blank Landing Page template can be overlayed by creating a new one at: `/apps/<appName>/designimporter/templates/<templateName>`

Steps for creating a new template in AEM are explained [here](/help/sites-developing/templates.md).

### Référencement d’un composant à partir de la page d’entrée {#referring-a-component-from-landing-page}

Supposons que vous souhaitiez référencer un composant dans votre fichier HTML à l’aide de l’attribut data-cq-component, de telle sorte que l’importateur de conception effectue le rendu d’un composant include à cet emplacement. e.g., you want to reference the table component ( `resourceType = /libs/foundation/components/table`). Vous devez ajouter ce qui suit dans le fichier HTML :

`<div data-cq-component="/libs/foundation/components/table">foundation table</div>`

Le chemin d’accès dans l’attribut data-cq-component doit être le resourceType du composant.

### Bonnes pratiques {#best-practices}

L’utilisation de sélecteurs CSS semblables à ceux présentés ci-dessous est déconseillée avec des éléments marqués pour la conversion de composants lors de l’importation.

| E > F | un élément F immédiatement précédé par un élément E | [Combinateur enfant](https://www.w3.org/TR/css3-selectors/#child-combinators) |
|---|---|---|
| E + F | un élément F qui est le fils d’un élément E | [Combinateur frère adjacent](https://www.w3.org/TR/css3-selectors/#adjacent-sibling-combinators) |
| E ~ F | un élément F précédé par un élément E | [Combinateur frère général](https://www.w3.org/TR/css3-selectors/#general-sibling-combinators) |
| E:root | un élément E, racine du document | [pseudo-classes structurelles](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-child(n) | un élément E qui est le n-ième enfant de son parent | [pseudo-classes structurelles](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-last-child(n) | un élément E qui est le n-ième enfant de son parent en comptant depuis le dernier enfant | [pseudo-classes structurelles](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-of-type(n) | un élément E qui est le n-ième enfant de son parent et de ce type | [pseudo-classes structurelles](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-last-of-type(n) | un élément E qui est le n-ième enfant de son parent et de ce type en comptant depuis le dernier enfant | [pseudo-classes structurelles](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |

Cela est dû au fait que d’autres éléments HTML, comme la balise &lt;div>, sont ajoutés au fichier HTML généré après l’importation.

* L’utilisation de scripts organisés selon une structure semblable à celle décrite ci-dessus est déconseillée avec des éléments marqués en vue d’une conversion en composants AEM.
* Il n’est pas recommandé d’utiliser des styles sur les balises pour la conversion de composants tels que &lt;div data-cq-component=&quot;&amp;ast;&quot;>.
* La mise en page de conception doit suivre les meilleures pratiques relatives au modèle HTML5 Boilerplate. Read more on: [https://html5boilerplate.com/](https://html5boilerplate.com/).

## Configuration de modules OSGI {#configuring-osgi-modules}

Les composants qui exposent les propriétés configurables via la console OSGI sont les suivants :

* Importateur de conception de page d’entrée
* Générateur de pages d’entrée
* Générateur de pages d’entrée pour mobiles
* Préprocesseur de saisie de pages d’entrée

Vous trouverez dans le tableau ci-dessous une brève description des propriétés :

<table>
 <tbody>
  <tr>
   <td><strong>Composant</strong></td>
   <td><strong>Nom de la propriété</strong></td>
   <td><strong>Description de la propriété  </strong></td>
  </tr>
  <tr>
   <td>Importateur de conception de page d’entrée</td>
   <td>Filtre exact</td>
   <td>Liste des expressions régulières à utiliser pour le filtrage des fichiers de l’extraction. <br />Les entrées zip correspondant à l’un des modèles spécifiés sont exclues de l’extraction.</td>
  </tr>
  <tr>
   <td>Générateur de pages d’entrée</td>
   <td>Modèle de fichier</td>
   <td>Le créateur de Landings page peut être configuré pour gérer les fichiers HTML correspondant à une expression normale, comme défini par le modèle de fichier.</td>
  </tr>
  <tr>
   <td>Générateur de pages d’entrée pour mobiles</td>
   <td>Modèle de fichier</td>
   <td>Le créateur de Landings page peut être configuré pour gérer les fichiers HTML correspondant à une expression normale, comme défini par le modèle de fichier.</td>
  </tr>
  <tr>
   <td> </td>
   <td>Groupes de périphériques</td>
   <td>Liste des groupes de périphériques à prendre en charge.</td>
  </tr>
  <tr>
   <td>Préprocesseur de saisie de pages d’entrée</td>
   <td>Modèle de recherche </td>
   <td>Modèle à rechercher, dans le contenu d’entrée de l’archive. Cette expression régulière est mise en correspondance ligne par ligne avec le contenu d’entrée. Lors de la correspondance, le texte correspondant est remplacé par le modèle de remplacement spécifié.<br /> <br /> Reportez-vous à la remarque ci-dessous concernant les limitations actuelles du préprocesseur de saisie de pages d’entrée.</td>
  </tr>
  <tr>
   <td> </td>
   <td>Modèle de remplacement</td>
   <td>Modèle qui remplace les correspondances trouvées. Vous pouvez utiliser des références de groupe regex telles que $1, $2. De plus, ce modèle prend en charge les mots-clés tels que {designPath} qui sont résolus avec la valeur réelle au cours de l’importation.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>**Limitations actuelles du préprocesseur de saisie de pages d’entrée :**
>S’il s’avère nécessaire d’apporter des modifications au modèle de recherche, lors de l’ouverture de l’éditeur de propriétés felix, vous devez ajouter manuellement des barres obliques inversées (\) pour appliquer un échappement aux métacaractères regex. Si vous n’ajoutez pas manuellement ces barres obliques inversées, l’expression régulière (regex) est considérée comme non valide et ne remplace pas la plus ancienne.
>
>Par exemple, si la configuration par défaut est :
>`/\* *CQ_DESIGN_PATH *\*/ *(['"])`
>
>Et vous devez remplacer >`CQ_DESIGN_PATH` dans `VIPURL` le modèle de recherche, votre modèle de recherche doit se présenter comme suit :
`/\* *VIPURL *\*/ *(['"])`

## Résolution des incidents {#troubleshooting}

Plusieurs erreurs peuvent être générées lors de l’importation du module de conception. Elles sont décrites dans cette section.

### Initialisation du Sidekick avec des composants relatifs à la page d’entrée {#initialization-of-sidekick-with-landing-page-relevant-components}

Si le module de conception contient des balises de composant parsys, le Sidekick commence à afficher les composants relatifs à la page d’entrée après l’importation. Vous pouvez faire glisser de nouveaux composants sur le composant parsys à l’intérieur de votre page d’entrée. Vous pouvez également passer en mode de conception et ajouter de nouveaux composants au Sidekick.

### Messages d’erreur affichés au cours de l’importation {#error-messages-displayed-during-import}

En cas d’erreur (par exemple, le package importé n’est pas un zip valide), l’importation de conception n’importe pas le package et affiche à la place un message d’erreur au-dessus de la page juste au-dessus de la zone de glisser-déposer. Des exemples de scénarios d’erreur sont présentés ici. Une fois l’erreur corrigée, vous pouvez réimporter le fichier ZIP mis à jour sur la même page d’entrée vierge. Vous trouverez, ci-dessous, différents scénarios entraînant la génération d’erreurs :

* Le module de conception importé n’est pas une archive ZIP valide.
* Le package de conception importé ne contient pas index.html au niveau supérieur.

### Avertissements affichés après l’importation {#warnings-displayed-after-import}

En cas d’avertissements (par exemple, HTML fait référence à des images qui n’existent pas dans le package), l’importateur de conception importe le fichier zip mais affiche en même temps une liste de problèmes/avertissements dans le volet des résultats, en cliquant sur le lien Problèmes, affiche une liste d’avertissements qui signalent tout problème dans le package de conception. Les différents scénarios selon lesquels les avertissements sont interceptés et affichés par l’importateur de conceptions sont les suivants :

* HTML fait référence aux images qui n’existent pas dans le package.
* HTML fait référence aux scripts qui n’existent pas dans le package.
* HTML fait référence aux styles qui n’existent pas dans le package.

### Where are the files of the ZIP file being stored in AEM? {#where-are-the-files-of-the-zip-file-being-stored-in-aem}

Une fois la page d’entrée importée, les fichiers (images, css, js, etc.) qui se trouvent dans le module de conception sont stockés à l’emplacement AEM suivant :

`/etc/designs/default/canvas/content/campaigns/<name of brand>/<name of campaign>/<name of landing page>`

Supposons que la page d’entrée soit créée sous la campagne We.Retail et que son nom soit **myBlankLandingPage**, l’emplacement de stockage des fichiers ZIP est le suivant :

`/etc/designs/default/canvas/content/campaigns/geometrixx/myBlankLandingPage`

### La mise en forme n’est pas conservée {#formatting-not-preserved}

Lorsque vous créez votre CSS, veuillez tenir compte des limitations suivantes :

Si un texte et une image (modifiable) se présentent comme suit :

```xml
<div class="box">
<p><div data-cq-component="image"><img src="assets/image.jpg" width="115"
height="116" /></div>Some Text </p>
</div>
```

avec une feuille de style CSS appliquée à la classe `box`, comme suit :

```xml
.box

{ width: 450px; padding:10px; border: 1px #C5DBE7 solid; margin: 0px auto 0 auto; background-image:url(assets/box.gif); background-repeat:repeat-x,y; font-family:Verdana, Arial, Helvetica, sans-serif; font-size:12px; color:#6D6D6D; }
```

`box img` est utilisé dans l’importateur de conception, la page d’entrée qui en résulte semble ne pas avoir conservé la mise en forme. Pour contourner ce problème, sachez qu’AEM ajoute des balises &lt;div> dans le CSS et réécrit le code en conséquence. Dans le cas contraire, certaines règles CSS ne seront pas valides.

```xml
.box img

{ float:right; margin: 0 0 5px 5px; border: 1px #343434 solid; }
```

>[!NOTE]
Also, designers should be aware that only code inside the **id=cqcanvas** tag is recognized by the importer, otherwise design is not preserved.

