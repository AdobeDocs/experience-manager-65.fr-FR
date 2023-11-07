---
title: Extension et configuration de l’importateur de conception pour les pages de destination
description: Découvrez comment configurer l’importateur de conception pour les landing pages.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
docset: aem65
exl-id: 1b8c6075-13c6-4277-b726-8dea7991efec
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '3498'
ht-degree: 43%

---

# Extension et configuration de l’importateur de conception pour les pages de destination{#extending-and-configuring-the-design-importer-for-landing-pages}

Cette section décrit la configuration et, si vous le souhaitez, l’extension de l’importateur de conception pour les pages de destination. L’utilisation de pages d’entrée après l’importation est traitée dans [Pages d’entrée.](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md)

**Pour que l’importateur de conception extraie votre composant personnalisé**

Voici les étapes logiques pour que l’importateur de conception reconnaisse votre composant personnalisé.

1. Création d’un gestionnaire de balises

   * Un gestionnaire de balises est un POJO (Plain Old Java Object) qui traite les balises HTML d’un type spécifique. Le &quot;type&quot; des balises de HTML que votre TagHandler peut gérer est défini via la propriété OSGi de TagHandlerFactory &quot;tagpattern.name&quot;. Cette propriété OSGi est en réalité une expression régulière (regex) qui doit correspondre à la balise HTML en entrée que vous souhaitez traiter. Toutes les balises imbriquées sont envoyées pour traitement à votre gestionnaire de balises. Par exemple, si vous vous enregistrez pour une balise div contenant une balise imbriquée &lt;p> , &lt;p> est également envoyée à votre gestionnaire de balises. C’est à vous de décider comment vous souhaitez vous en charger.
   * L’interface du gestionnaire de balises est semblable à une interface de gestion de contenu SAX. Elle reçoit des événements SAX pour chaque balise HTML. En tant que fournisseur de gestionnaire de balises, vous devez mettre en oeuvre certaines méthodes de cycle de vie qui sont automatiquement appelées par la structure de l’importateur de conception.

1. Créez le composant TagHandlerFactory correspondant.

   * La fabrique de gestionnaires de balises est un composant OSGi (singleton) responsable de la génération d’instances de votre gestionnaire de balises.
   * Votre TagHandlerFactory doit exposer une propriété OSGi appelée « tagpattern.name » dont la valeur est comparée à la balise HTML d’entrée.
   * Si plusieurs gestionnaires de balises correspondent à la balise HTML en entrée, celui dont le classement est le plus élevé est celui choisi. Le classement proprement dit est exposé sous forme de propriété OSGi **service.ranking**.
   * TagHandlerFactory est un composant OSGi. Toutes les références que vous souhaitez fournir à votre TagHandler doivent être fournies via cette fabrique.

1. Assurez-vous que votre composant TagHandlerFactory présente un meilleur classement si vous souhaitez ignorer la valeur par défaut.

>[!CAUTION]
>
>l’importateur de conception, utilisé pour importer des landing pages, [a été abandonné avec AEM 6.5.](/help/release-notes/deprecated-removed-features.md#deprecated-features).

## Préparation du HTML pour l’importation {#preparing-the-html-for-import}

Après avoir créé une page d’importation, vous pouvez importer votre page de destination HTML dans son intégralité. Pour importer votre page de destination HTML, vous devez d’abord compresser son contenu dans un module de conception. Le module de conception contient votre landing page de HTML avec les ressources référencées (images, css, icônes, scripts, etc.).

La feuille de calcul suivante fournit un exemple de préparation de votre HTML pour l’importation :

Aide-mémoire pour la page d’entrée

[Obtenir le fichier](assets/cheatsheet.zip)

### Mise en page et exigences du fichier Zip {#zip-file-layout-and-requirements}

>[!NOTE]
>
>À ce stade, les fichiers ZIP ne peuvent contenir qu’une page de HTML ou une partie d’une page.

Voici un exemple de mise en page du fichier zip :

* /index.html -> fichier de HTML de landing page
* /css -> à ajouter à la bibliothèque cliente CSS
* /img -> toutes les images et tous les actifs
* /js -> à ajouter à la bibliothèque cliente JS

La disposition s’appuie sur les bonnes pratiques HTML5 Boilerplate. Pour en savoir plus, consultez [https://html5boilerplate.com/](https://html5boilerplate.com/).

>[!NOTE]
>
>Le package de conception **doit** contenir, au minimum, un fichier **index.html** au niveau racine. Si la landing page à importer comporte également une version mobile, le fichier zip doit contenir une balise **mobile.index.html** avec **index.html** au niveau racine.

### Préparation du HTML de page d’entrée {#preparing-the-landing-page-html}

Pour pouvoir importer le HTML, vous devez ajouter une balise div de canevas au HTML de page d’entrée.

La balise &lt;div> du canevas est une balise **div** html avec `id="cqcanvas"`, qui doit être insérée dans la balise `<body>` HTML et doit encapsuler le contenu destiné à la conversion.

Voici un exemple de fragment de HTML de page d’entrée après l’ajout de la balise div de canevas :

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

### Préparation du HTML pour l’inclusion de composants AEM modifiables {#preparing-the-html-to-include-editable-aem-components}

Lorsque vous importez une page d’entrée, vous avez la possibilité d’importer la page telle quelle, ce qui signifie qu’une fois la page d’entrée importée, vous ne pouvez plus modifier aucun des éléments importés dans AEM (vous pouvez toujours ajouter des composants AEM supplémentaires sur la page).

Avant d’importer la page de destination, vous pouvez en convertir certaines parties pour en faire des composants AEM modifiables. Vous pouvez ainsi modifier rapidement des parties de la landing page, même après l&#39;import de la conception de la landing page.

Pour ce faire, ajoutez `data-cq-component` au composant approprié dans le fichier HTML importé.

La section suivante décrit la modification de votre fichier HTML de manière à convertir certaines parties de vos pages de destination en différents composants AEM modifiables. Les composants sont décrits en détail à la section [Composants de pages d’entrée](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md).

>[!NOTE]
>
>Les balises HTML destinées à la conversion de parties de la page de destination en composants AEM comportent une déclaration de balises de forme longue et de forme courte. Les deux sont décrits pour chaque composant.

### Limites {#limitations}

Avant l’importation, notez les restrictions suivantes :

### Les attributs, tels que class ou id, appliqués à la balise &amp;lt;body> ne sont pas conservés. {#any-attribute-like-class-or-id-applied-on-the-amp-lt-body-tag-is-not-preserved}

Si un attribut tel que id ou class est appliqué à la balise body, par exemple : `<body id="container">` il n’est pas conservé après l’importation. La conception importée ne doit donc avoir aucune dépendance sur les attributs appliqués à la balise `<body>`.

### Transfert de fichiers ZIP par glisser-déposer {#drag-and-drop-zip}

Le chargement de fichiers ZIP par glisser-déposer n’est pas pris en charge par les versions 3.6 et inférieures d’Internet Explorer et Firefox. Pour charger une conception lorsque vous utilisez ces navigateurs, cliquez sur la zone de dépôt pour ouvrir une boîte de dialogue de téléchargement de fichier et chargez votre conception à l’aide de cette boîte de dialogue.

Les navigateurs qui prennent en charge le &quot;glisser-déposer&quot; du fichier compressé de conception sont Chrome, Safari 5.x, Firefox 4 et versions ultérieures.

### Modernizr n’est pas pris en charge {#modernizr-is-not-supported}

`Modernizr.js` est un outil JavaScript qui détecte les fonctionnalités natives des navigateurs et détecte s’ils sont adaptés ou non aux éléments html5. Les conceptions qui utilisent Modernizr pour améliorer la prise en charge dans les versions plus anciennes des différents navigateurs peuvent entraîner des problèmes d’importation dans la solution de page de destination. Les scripts `Modernizr.js` ne sont pas pris en charge avec l’importateur de conception.

### Les propriétés de page ne sont pas conservées au moment de l’importation du module de conception. {#page-properties-are-not-preserved-at-the-time-of-importing-design-package}

Toute propriété de page (par exemple, Domaine personnalisé, Application HTTPS, etc.) définie pour une page (qui utilise le modèle Page d’entrée vierge) avant d’importer le module de conception est perdue une fois la conception importée. Par conséquent, la pratique recommandée consiste à définir les propriétés de page après l’importation du module de conception.

### Balisage en HTML seul supposé {#html-only-markup-assumed}

Lors de l’importation, les balises sont assainies pour des raisons de sécurité et pour éviter d’importer et de publier des balises non valides. Cela suppose que les balises HTML uniquement et que toutes les autres formes d’éléments tels que les SVG en ligne ou les composants web soient filtrées.

### Texte {#text}

Balise HTML permettant d’insérer un composant texte (`foundation/components/text`) dans le fichier HTML à l’intérieur du package de conception :

```xml
<div data-cq-component="text"> <p>This is some editable text</p> </div>
```

L’insertion des balises ci-dessus dans le fichier HTML produit les effets suivants :

* Crée un composant texte AEM modifiable (`sling:resourceType=foundation/components/text`) dans la page de destination créée après l’importation du module de conception.
* Définit la propriété `text` du composant texte créé sur le code HTML placé entre les balises `div`.

**Déclaration courte des balises de composant**:

```xml
<p data-cq-component="text">Text component shorthand</p>
```

**Texte avec liste**

Pour ajouter un texte avec une liste :

* 1st
* 2nd

qui peuvent être modifiés dans l’éditeur d’éditeur de texte enrichi :

```xml
<div data-cq-component="text"><p>This is text with a list:</p><ul><li>1st</li><li>2nd</li></ul><p>It can be edited with the RTE editor</p></div>
```

**Texte avec couleur**

Pour ajouter un texte de couleur (rose) qui peut être modifié dans l’éditeur de texte enrichi :

```xml
<div class="pink" data-cq-component="text"><p>This is pink text.</p><p>It can be edited with the RTE editor</p></div>
```

### Titre {#title}

Balise HTML permettant d’insérer un composant de titre (`wcm/landingpage/components/title`) dans le fichier HTML à l’intérieur du package de conception :

```xml
<div data-cq-component="title"> <h1>This is some editable title text</h1> </div>
```

L’insertion des balises ci-dessus dans le fichier HTML produit les effets suivants :

* Crée un composant de titre AEM modifiable (`sling:resourceType=wcm/landingpage/components/title`) dans la page de destination créée après l’importation du module de conception.
* Définition de la propriété `jcr:title` du composant de titre créé sur le texte dans la balise d’en-tête placée entre les balises div.
* Définit la propriété `type` sur la balise d’en-tête, dans ce cas `h1`.

Le composant Titre prend en charge sept types : `h1, h2, h3, h4, h5, h6` et `default`.

**Déclaration courte des balises de composant**:

```xml
<h1 data-cq-component="title">Title component shorthand</h1>
```

### Image {#image}

Balisage de HTML pour insérer un composant d’image (foundation/components/image) dans le HTML dans le module de conception :

```xml
<div data-cq-component="image">
<img src="img/video1.png" alt="Video about Polar Brake Goggles in action" title="Polar Brake Goggles" width="300" height="200" />
</div>
```

L’insertion des balises ci-dessus dans le fichier HTML produit les effets suivants :

* Crée un composant image AEM modifiable (`sling:resourceType=foundation/components/image`) dans la page de destination créée après l’importation du module de conception.
* Définit la propriété `fileReference` du composant image créé sur le chemin d’importation de l’image spécifiée dans l’attribut src.
* Définit la propriété `alt` sur la valeur de l’attribut alt dans la balise &lt;img>.
* Définit la propriété `title` sur la valeur de l’attribut title dans la balise &lt;img>.
* Définit la propriété `width` sur la valeur de l’attribut width dans la balise &lt;img>.
* Définit la propriété `height` sur la valeur de l’attribut height dans la balise &lt;img>.

**Déclaration courte des balises du composant :**

```xml
<img data-cq-component="image" src="test.png" alt="Image component shorthand"/>
```

#### Image d’URL absolue non prise en charge dans la balise Div du composant Image {#absolute-url-img-src-not-supported-within-image-component-div}

Si une balise `<img>` avec une adresse URL &lt;src> absolue est utilisée pour la conversion d’un composant, une exception **UnsupportedTagContentException** appropriée est générée. Par exemple, le code suivant n’est pas pris en charge :

`<div data-cq-component="image">`

`<img src="https://cdn.printfriendly.com/pf-button.gif" alt="Print Friendly and PDF"/>`

`</div>`

Dans le cas contraire, les images URL absolues sont prises en charge pour les balises img qui ne font pas partie de la balise div du composant d’image.

### Composants d’appel à l’action {#call-to-action-components}

Vous pouvez marquer une partie de la page de destination pour l’importation sous forme de « composant CTA modifiable ». Les composants de ce type peuvent être modifiés après l’importation de la page de destination. AEM comprend les composants CTA suivants :

* Lien des clics publicitaires : permet d’ajouter un lien texte qui, lorsqu’un utilisateur clique dessus, dirige le visiteur vers une URL cible.
* Lien graphique : permet d’ajouter une image qui, lorsqu’un utilisateur clique dessus, dirige le visiteur vers une URL cible.

#### Lien des clics publicitaires {#click-through-link}

Ce composant CTA peut être utilisé pour ajouter un lien texte sur la page d’entrée.

Propriétés prises en charge

* Libellé, avec options de gras, d’italique et de soulignement
* URL Target, prend en charge l’URL tierce et AEM
* Options de rendu de page (même fenêtre, nouvelle fenêtre, etc.)

Balise HTML permettant d’inclure le composant « clics publicitaires » dans le fichier ZIP importé. Dans le cas présent, href mappe sur l’URL cible, &quot;Afficher les détails du produit&quot; mappe sur l’étiquette, etc.

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

Ce composant peut être utilisé dans n’importe quelle application autonome ou importé à partir de ZIP.

**Déclaration courte des balises de composant**:

```xml
<a href="/somelink.html" data-cq-component="clickThroughLink">Click Through Link shorthand</a>
```

#### Lien graphique {#graphical-link}

Vous pouvez utiliser ce composant CTA pour ajouter une image graphique avec un lien sur la page de destination. Il peut s’agir d’un simple bouton ou d’une image en arrière-plan. Lorsque l’utilisateur clique sur l’image, il est amené à l’URL cible spécifiée dans les propriétés du composant. Il fait partie du groupe &quot;Appel à l’action&quot;.

Propriétés prises en charge

* Recadrage d’image, rotation
* Texte de survol, description, taille en px
* URL Target, prend en charge l’URL tierce et AEM
* Options de rendu de page (même fenêtre, nouvelle fenêtre, etc.)

Balise HTML permettant d’inclure le composant « lien graphique » dans le fichier ZIP importé. Ici href mappe sur l’URL cible, img src est l’image de rendu, &quot;titre&quot; est utilisé comme texte de survol, etc.

```xml
<div id="cqcanvas">
  <div data-cq-component="clickThroughGraphicalLink"><a href="https://www.adobe.com/go/wem"><img src="img/call-to-action-button.png" title="Click Here to Learn More" /></a></div>
</div>
```

**Déclaration courte des balises de composant**:

```xml
<a href="/somelink.html" data-cq-component="clickThroughGraphicalLink"><img src="linkimage.png" alt="Click Through Graphical Link shorthand"/></a>
```

>[!NOTE]
>
>Pour créer un lien graphique à cliquer, vous devez encapsuler une balise &lt;anchor> et la balise d’image dans une balise &lt;div> avec l’attribut `data-cq-component="clickthroughgraphicallink"`.
>
>Par exemple, `<div data-cq-component="clickthroughlink"> <a href="https://myURLhere/"><img src="image source here"></a> </div>`
>
>Les autres méthodes d’association d’une image à une balise d’ancrage à l’aide de CSS ne sont pas prises en charge. Par exemple, les balises suivantes ne fonctionnent pas :
>
>`<div data-cq-component="clickthroughgraphicallink">`
>
>`<a class="hasBackground" href="https://myURLhere/"></a>`
>
>`</div>`
>
>par un `css .hasbackground { background-image: pathtoimage }` lié
>

### Formulaire de prospect {#lead-form}

Le formulaire de piste est utilisé pour collecter des informations sur le profil d’un visiteur/prospect. Ces informations pourront être stockées et exploitées ultérieurement pour mener une campagne marketing efficace. Ces informations comprennent généralement le titre, le nom, l’adresse électronique, la date de naissance, l’adresse, l’intérêt, etc. Il fait partie du groupe « Formulaire de prospect CTA ».

**Fonctionnalités prises en charge**

* Champs de prospect prédéfinis : les boutons Prénom, Nom, Adresse, Fonction, À propos de, ID utilisateur, ID d’e-mail et Envoyer sont disponibles dans le Sidekick. Il vous suffit de faire glisser le composant requis dans votre formulaire de prospect.
* Grâce à ces composants, l’auteur peut concevoir un formulaire de prospect autonome. Ces champs correspondent à ceux du formulaire de prospect. Dans une application ZIP importée ou autonome, l’utilisateur peut ajouter des champs supplémentaires à l’aide des champs de formulaire de piste cq:form ou cta, les nommer et les concevoir selon les besoins.
* Mappez les champs de formulaire de piste à l’aide de noms prédéfinis spécifiques du formulaire de piste CTA, par exemple : firstName pour first-name dans le formulaire de piste, etc.
* Les champs qui ne sont pas mappés à des composants de formulaire de piste sont mappés à cq:form - texte, radio, case à cocher, liste déroulante, masqué, mot de passe.
* L’utilisateur ou l’utilisatrice peut fournir le titre à l’aide de la balise « label » et indiquer le style en utilisant l’attribut de style « class » (disponible uniquement pour les composants du formulaire de prospect CTA).
* La page de remerciements et la liste d’abonnements peuvent être fournies sous forme de paramètre masqué du formulaire (présent dans le fichier index.htm) ou être ajoutées ou modifiées dans la barre de modification de « Début du formulaire de prospect ».

  &lt;input type=&quot;hidden&quot; name=&quot;redirectUrl&quot; value=&quot;/content/we-retail/en/user/register/thank_you&quot;/>

  &lt;input type=&quot;hidden&quot; name=&quot;groupName&quot; value=&quot;leadForm&quot;/>

* Des contraintes (telles qu’« Obligatoire ») peuvent être fournies à partir de la configuration de modification de chaque composant.

Balise HTML permettant d’inclure le composant « lien graphique » dans le fichier ZIP importé. Ici, &quot;firstName&quot; est mappé sur firstName du formulaire de piste, etc., à l’exception des cases à cocher : ces deux cases à cocher sont mappées sur le composant déroulant cq:form .

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

Le composant parsys d’AEM est un composant conteneur qui peut contenir d’autres composants AEM. Il est possible d’ajouter un composant parsys dans le fichier HTML importé. Cela permet à l’utilisateur d’ajouter/supprimer des composants d’AEM modifiables à la page d’entrée, même après son importation.

Le système de paragraphes permet aux utilisateurs d’ajouter des composants à l’aide du sidekick.

Balise HTML permettant d’insérer un composant parsys (`foundation/components/parsys`) dans le fichier HTML à l’intérieur du package de conception :

```xml
<div data-cq-component="parsys">
   <div data-cq-component="title"><h2>ULTIMATE PROTECTION</h2></div>
        <div data-cq-component="title"><h3>ON SALE</h3></div>
</div>
```

L’inclusion des balises ci-dessus dans le HTML effectue les opérations suivantes :

* Insère un composant parsys d’AEM (foundation/components/parsys) dans la page d’entrée créée après l’importation du module de conception.
* Initialisation du Sidekick avec des composants par défaut. De nouveaux composants peuvent être ajoutés à la page d’entrée en faisant glisser les composants du sidekick vers le composant parsys.
* Deux composants de titre font également partie du système de paragraphes (parsys).

### Cible {#target}

Le composant cible affiche le contenu d’une expérience sur la page : Il peut y avoir de nombreuses expériences créées dans une campagne et le composant cible peut afficher dynamiquement le contenu de différentes expériences aux différents utilisateurs qui visitent la page.

Balise HTML permettant d’insérer un composant cible et de créer différentes expériences dans une campagne :

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

Outre la spécification de l’AEM des composants importés modifiables, vous pouvez également configurer les éléments suivants avant d’importer le module de conception :

* Définition des propriétés de page en extrayant les métadonnées définies dans le HTML importé.
* Spécification du codage du jeu de caractères dans le HTML.
* Recouvrement du modèle de page de l’importateur.

### Définition des propriétés de page en extrayant les métadonnées définies dans le HTML importé {#setting-page-properties-by-extracting-metadata-defined-in-imported-html}

Les métadonnées suivantes déclarées dans l’en-tête du HTML importé doivent être extraites et conservées par l’importateur de conception en tant que propriété &quot;jcr:description&quot; :

* &lt;meta name=&quot;description&quot; content=&quot;&quot;>

L’attribut Lang défini dans la balise de HTML doit être extrait et conservé par l’importateur de conception en tant que propriété &quot;jcr:language&quot;.

* &lt;html lang=&quot;en&quot;>

### Spécification du codage du jeu de caractères dans le fichier HTML {#specifying-the-charset-encoding-in-the-html}

L’importateur de conception lit le codage spécifié dans le fichier HTML importé. Le codage peut être spécifié comme suit :

`<meta charset="UTF-8">`

*OU*

`<meta http-equiv="content-type" content="text/html;charset=utf-8">`

Si aucun codage n’est spécifié dans le HTML importé, le codage par défaut défini par l’importateur de conception est UTF-8.

### Recouvrement d’un modèle {#overlaying-template}

Le modèle Page d’entrée vierge peut être recouvert en en créant une sur : `/apps/<appName>/designimporter/templates/<templateName>`

Les étapes de création d’un modèle dans AEM sont expliquées. [here](/help/sites-developing/templates.md).

### Référencement d’un composant à partir de la page d’entrée {#referring-a-component-from-landing-page}

Supposons que vous souhaitiez référencer un composant dans votre fichier HTML à l’aide de l’attribut data-cq-component, de telle sorte que l’importateur de conception effectue le rendu d’un composant include à cet emplacement. Par exemple, vous souhaitez référencer le composant de tableau ( `resourceType = /libs/foundation/components/table`). Vous devez ajouter ce qui suit dans le fichier HTML :

`<div data-cq-component="/libs/foundation/components/table">foundation table</div>`

Le chemin d’accès dans le composant data-cq-component doit être resourceType du composant.

### Bonnes pratiques {#best-practices}

L’utilisation de sélecteurs CSS similaires aux suivants n’est pas recommandée avec les éléments marqués pour la conversion de composants lors de l’importation.

| E > F | un élément F immédiatement précédé par un élément E | [Combinateur enfant](https://www.w3.org/TR/css3-selectors/#child-combinators) |
|---|---|---|
| E + F | un élément F qui est le fils d’un élément E | [Combinateur frère adjacent](https://www.w3.org/TR/css3-selectors/#adjacent-sibling-combinators) |
| E ~ F | un élément F précédé d’un élément E ; | [Combinateur frère général](https://www.w3.org/TR/css3-selectors/#general-sibling-combinators) |
| E:root | un élément E, racine du document | [Pseudo-classes structurelles](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-child(n) | un élément E, le n-ième enfant de son parent ; | [Pseudo-classes structurelles](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-last-child(n) | un élément E, le n-ième enfant de son parent, en comptant à partir du dernier | [Pseudo-classes structurelles](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-of-type(n) | un élément E, le n-ième frère de son type | [Pseudo-classes structurelles](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-last-of-type(n) | un élément E, le n-ième frère de son type, en comptant à partir du dernier | [Pseudo-classes structurelles](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |

En effet, des éléments HTML supplémentaires tels que &lt;div> Les balises sont ajoutées au fichier Html généré après l’importation.

* Les scripts reposant sur la structure similaire à ci-dessus ne sont pas non plus recommandés pour une utilisation avec des éléments marqués pour conversion en composants AEM.
* Il est déconseillé d’utiliser des styles sur les balises de mise en forme pour la conversion d’un composant, comme &lt;div data-cq-component=&quot;&amp;ast;&quot;>.
* La disposition de conception doit suivre les bonnes pratiques relatives au modèle HTML5 Boilerplate. Pour en savoir plus, consultez [https://html5boilerplate.com/](https://html5boilerplate.com/).

## Configuration de modules OSGI {#configuring-osgi-modules}

Les composants qui exposent des propriétés configurables par le biais de la console OSGI sont les suivants :

* Importateur de conception de page d’entrée
* Générateur de page d’entrée
* Générateur de page d’entrée pour mobile
* Préprocesseur de saisie de page d’entrée

Le tableau ci-dessous décrit brièvement les propriétés :

<table>
 <tbody>
  <tr>
   <td><strong>Composant</strong></td>
   <td><strong>Nom de la propriété</strong></td>
   <td><strong>Description de la propriété </strong></td>
  </tr>
  <tr>
   <td>Importateur de conception de page d’entrée</td>
   <td>Extraire le filtre</td>
   <td>Liste des expressions régulières à utiliser pour le filtrage des fichiers de l’extraction. <br />Les entrées zip correspondant à l’un des modèles spécifiés sont exclues de l’extraction.</td>
  </tr>
  <tr>
   <td>Générateur de page d’entrée</td>
   <td>Modèle de fichier</td>
   <td>Le générateur de pages de destination peut être configuré pour traiter les fichiers HTML correspondant à une expression régulière, tel que défini par le modèle de fichier.</td>
  </tr>
  <tr>
   <td>Générateur de page d’entrée pour mobile</td>
   <td>Modèle de fichier</td>
   <td>Le générateur de pages de destination peut être configuré pour traiter les fichiers HTML correspondant à une expression régulière, tel que défini par le modèle de fichier.</td>
  </tr>
  <tr>
   <td> </td>
   <td>Groupes de périphériques</td>
   <td>Liste des groupes d’appareils à prendre en charge.</td>
  </tr>
  <tr>
   <td>Préprocesseur de saisie de page d’entrée</td>
   <td>Motif de recherche </td>
   <td>Motif à rechercher, dans le contenu d’entrée de l’archive. Dans le cas de cette expression régulière, une correspondance est effectuée, ligne par ligne, avec le contenu de l’entrée. En cas de correspondance, le texte concerné est remplacé par le modèle de remplacement spécifié.<br /> <br /> Reportez-vous à la remarque ci-dessous concernant les limitations actuelles du préprocesseur de saisie de pages d’entrée.</td>
  </tr>
  <tr>
   <td> </td>
   <td>Modèle de remplacement</td>
   <td>Modèle qui remplace les correspondances trouvées. Vous pouvez utiliser des références de groupe regex, telles que $1, $2. Ce modèle prend également en charge des mots-clés tels que {designPath} qui sont résolus avec la valeur réelle pendant l’importation.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>**Limites actuelles du préprocesseur de saisie de page d’entrée :**
>Si vous devez apporter des modifications au modèle de recherche, lorsque vous ouvrez l’éditeur de propriétés felix, vous devez ajouter manuellement des barres obliques inversées pour échapper les métacaractères regex. Si vous n’ajoutez pas manuellement de barre oblique inverse, l’expression régulière est considérée comme non valide et ne remplacera pas l’ancienne.
>
>Par exemple, si la configuration par défaut est
>
>>`/\* *CQ_DESIGN_PATH *\*/ *(['"])`
>
>Et vous devez remplacer `CQ_DESIGN_PATH`par `VIPURL` dans le motif de recherche, celui-ci doit se présenter comme suit :
>
>`/\* *VIPURL *\*/ *(['"])`

## Résolution des problèmes {#troubleshooting}

Lors de l’import du module de conception, plusieurs erreurs peuvent se produire, décrites dans cette section.

### Initialisation du sidekick avec les composants pertinents de la page d’entrée {#initialization-of-sidekick-with-landing-page-relevant-components}

Si le package de conception contient des balises de composant parsys, le Sidekick commence à afficher les composants relatifs à la page d’entrée après l’importation. Vous pouvez faire glisser de nouveaux composants sur le composant parsys à l’intérieur de votre page de destination. Vous pouvez également accéder au mode de conception et ajouter de nouveaux composants au sidekick.

### Messages d’erreur affichés au cours de l’importation {#error-messages-displayed-during-import}

En cas d’erreur (par exemple, le package importé n’est pas un fichier zip valide), l’importation de conception n’importe pas le package. Un message d’erreur s’affiche en haut de la page, juste au-dessus de la zone de glisser-déposer. Des exemples de scénarios d’erreur sont présentés ici. Après avoir corrigé l’erreur, vous pouvez réimporter le fichier compressé mis à jour sur la même page d’entrée vierge. Les différents scénarios où des erreurs sont générées sont les suivants :

* Le package de conception importé n’est pas une archive ZIP valide.
* Le package de conception importé ne comporte pas de fichier index.html au niveau supérieur.

### Avertissements affichés après l’importation {#warnings-displayed-after-import}

S’il existe des avertissements (par exemple, HTML fait référence à des images qui n’existent pas dans le module), l’importateur de conception importe le fichier zip, mais affiche en même temps une liste de problèmes/avertissements dans le volet Résultat. Cliquez sur le lien Problèmes pour afficher une liste d’avertissements qui indiquent les problèmes éventuels dans le module de conception. Voici différents scénarios dans lesquels l’importateur de conception a intercepté et affiché des avertissements :

* Le fichier HTML fait référence à des images qui n’existent pas dans le package.
* Le fichier HTML fait référence à des scripts qui n’existent pas dans le package.
* Le fichier HTML fait référence à des styles qui n’existent pas dans le package.

### Où les fichiers du fichier ZIP sont-ils stockés dans AEM ? {#where-are-the-files-of-the-zip-file-being-stored-in-aem}

Une fois la page d’entrée importée, les fichiers (images, css, js, etc.) du module de conception sont stockés à l’emplacement suivant dans AEM :

`/etc/designs/default/canvas/content/campaigns/<name of brand>/<name of campaign>/<name of landing page>`

Supposons que la landing page soit créée sous la campagne We.Retail et que le nom de la landing page soit **myBlankLandingPage** alors l’emplacement où les fichiers zip sont stockés est le suivant :

`/etc/designs/default/canvas/content/campaigns/geometrixx/myBlankLandingPage`

### Mise en forme non conservée {#formatting-not-preserved}

Lors de la création de votre CSS, tenez compte des limites suivantes :

Si un texte et une image (modifiable) se présentent comme suit :

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

Alors `box img` est utilisé dans l’importateur de conception, la page d’entrée qui en résulte ne semble pas avoir conservé la mise en forme. Pour contourner ce problème, AEM ajoute des balises div dans le CSS et réécrivez le code en conséquence. Dans le cas contraire, certaines règles CSS ne seront pas valides.

```xml
.box img

{ float:right; margin: 0 0 5px 5px; border: 1px #343434 solid; }
```

>[!NOTE]
>
>Les concepteurs doivent également tenir compte du fait que l’importateur ne reconnaît que le code placé à l’intérieur de la balise **id=cqcanvas**, autrement la conception n’est pas conservée.
