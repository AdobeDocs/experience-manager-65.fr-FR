---
title: Extension et configuration de l’importateur de conception pour les pages de destination
description: Découvrez comment configurer l’importateur de conception pour les pages de destination.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
docset: aem65
exl-id: 1b8c6075-13c6-4277-b726-8dea7991efec
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '3442'
ht-degree: 99%

---

# Extension et configuration de l’importateur de conception pour les pages de destination{#extending-and-configuring-the-design-importer-for-landing-pages}

Cette section décrit la configuration et, si vous le souhaitez, l’extension de l’importateur de conception pour les pages de destination. L’utilisation de pages de destination après l’import est traitée dans [Pages de destination.](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md)

**Pour que l’importateur de conception extraie votre composant personnalisé**

Voici les étapes logiques pour que l’importateur de conception reconnaisse votre composant personnalisé.

1. Création d’un gestionnaire de balises

   * Un gestionnaire de balises est un POJO (Plain Old Java Object) qui traite les balises HTML d’un type spécifique. Le « type » des balises HTML que votre TagHandler peut traiter est défini au moyen de la propriété OSGi « tagpattern.name » de TagHandlerFactory. Cette propriété OSGi est en réalité une expression régulière (regex) qui doit correspondre à la balise HTML en entrée que vous souhaitez traiter. Toutes les balises imbriquées sont envoyées pour traitement à votre gestionnaire de balises. Par exemple, si vous enregistrez une balise div contenant une balise &lt;p> imbriquée, &lt;p> est également envoyée à votre gestionnaire de balises. C’est à vous de décider comment vous souhaitez vous en charger.
   * L’interface du gestionnaire de balises est semblable à une interface de gestion de contenu SAX. Elle reçoit des événements SAX pour chaque balise HTML. En tant que fournisseur de gestionnaire de balises, vous devez mettre en œuvre certaines méthodes de cycle de vie qui sont automatiquement appelées par le framework de l’importateur de conception.

1. Créez le composant TagHandlerFactory correspondant.

   * La fabrique de gestionnaires de balises est un composant OSGi (singleton) responsable du déclenchement d’instances sur votre gestionnaire de balises.
   * Votre TagHandlerFactory doit exposer une propriété OSGi appelée « tagpattern.name » dont la valeur est comparée à la balise HTML d’entrée.
   * Si plusieurs gestionnaires de balises correspondent à la balise HTML en entrée, celui dont le classement est le plus élevé est celui choisi. Le classement proprement dit est exposé sous forme de propriété OSGi **service.ranking**.
   * TagHandlerFactory est un composant OSGi. Toutes les références que vous souhaitez fournir à votre gestionnaire de balises doivent être fournies via cette fabrique.

1. Assurez-vous que votre composant TagHandlerFactory présente un meilleur classement si vous souhaitez ignorer la valeur par défaut.

>[!CAUTION]
>
>L’importateur de conception utilisé pour importer les pages de destination [a été abandonné avec AEM 6.5.](/help/release-notes/deprecated-removed-features.md#deprecated-features).

## Préparer le code HTML pour l’import {#preparing-the-html-for-import}

Après avoir créé une page d’importation, vous pouvez importer votre page de destination HTML dans son intégralité. Pour importer votre page de destination HTML, vous devez d’abord compresser son contenu dans un module de conception. Le package de conception contient votre page de destination HTML avec les ressources référencées (images, css, icônes, scripts, etc.).

L’aide-mémoire suivante fournit un exemple de préparation de votre HTML pour l’import :

Aide-mémoire pour la page de destination

[Obtenir le fichier](assets/cheatsheet.zip)

### Disposition et exigences du fichier Zip {#zip-file-layout-and-requirements}

>[!NOTE]
>
>À ce stade, les fichiers ZIP ne peuvent contenir qu’une page HTML ou une partie d’une page.

Voici un exemple de disposition du fichier zip :

* /index.html -> fichier HTML de page de destination
* /css -> à ajouter à la bibliothèque cliente CSS
* /img -> toutes les images et ressources
* /js -> à ajouter à la bibliothèque cliente JS

La disposition s’appuie sur les bonnes pratiques HTML5 Boilerplate. Pour en savoir plus, consultez [https://html5boilerplate.com/](https://html5boilerplate.com/).

>[!NOTE]
>
>Le package de conception **doit** contenir, au minimum, un fichier **index.html** au niveau racine. Si la page de destination à importer comporte également une version mobile, le fichier zip doit contenir une balise **mobile.index.html** avec **index.html** au niveau racine.

### Préparation du HTML de la page de destination {#preparing-the-landing-page-html}

Pour pouvoir importer le HTML, vous devez ajouter une balise div de canevas au HTML de la page de destination.

La balise &lt;div> du canevas est une balise **div** html avec `id="cqcanvas"`, qui doit être insérée dans la balise `<body>` HTML et doit encapsuler le contenu destiné à la conversion.

Voici un exemple de fragment de HTML de page de destination après l’ajout de la balise div de canevas :

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

Lorsque vous importez une page de destination, vous avez la possibilité d’importer la page telle quelle, ce qui signifie qu’une fois la page de destination importée, vous ne pouvez plus modifier aucun des éléments importés dans AEM (vous pouvez toujours ajouter des composants AEM supplémentaires sur la page).

Avant d’importer la page de destination, vous pouvez en convertir certaines parties pour en faire des composants AEM modifiables. Cela vous permet de modifier rapidement des parties de la page de destination, même après en avoir importé la conception.

Pour ce faire, ajoutez `data-cq-component` au composant approprié dans le fichier HTML importé.

La section suivante décrit la modification de votre fichier HTML de manière à convertir certaines parties de vos pages de destination en différents composants AEM modifiables. Les composants sont décrits en détail dans la section [Composants des pages de destination](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md).

>[!NOTE]
>
>Les balises HTML destinées à la conversion de parties de la page de destination en composants AEM comportent une déclaration de balises de forme longue et de forme courte. Les deux sont décrits pour chaque composant.

### Limites {#limitations}

Avant l’importation, veuillez noter les restrictions suivantes :

### Tout attribut de classe ou d’id appliqué à la balise &lt;body> n’est pas conservé.  {#any-attribute-like-class-or-id-applied-on-the-amp-lt-body-tag-is-not-preserved}

Si un attribut d’id ou de classe est appliqué à la balise body, par exemple `<body id="container">`, il n’est pas conservé après l’importation. La conception importée ne doit donc avoir aucune dépendance sur les attributs appliqués à la balise `<body>`.

### Transfert de fichiers ZIP par glisser-déposer {#drag-and-drop-zip}

Le chargement de fichiers ZIP par glisser-déposer n’est pas pris en charge par les versions 3.6 et inférieures d’Internet Explorer et Firefox. Pour charger une conception lorsque vous utilisez ces navigateurs, cliquez sur la zone de dépôt de fichier pour ouvrir une boîte de dialogue de chargement de fichier, puis chargez votre conception à l’aide de cette boîte de dialogue.

Les navigateurs qui prennent en charge le « glisser-déposer » du fichier zip de conception sont Chrome, Safari 5.x, Firefox 4 et versions ultérieures.

### Modernizr n’est pas pris en charge {#modernizr-is-not-supported}

`Modernizr.js` est un outil JavaScript qui détecte les fonctionnalités natives des navigateurs et détermine si elles sont adaptées ou non aux éléments HTML5. Les conceptions qui utilisent Modernizr pour améliorer la prise en charge dans les versions plus anciennes des différents navigateurs peuvent entraîner des problèmes d’importation dans la solution de page de destination. Les scripts `Modernizr.js` ne sont pas pris en charge avec l’importateur de conception.

### Les propriétés de page ne sont pas conservées au moment de l’import du package de conception. {#page-properties-are-not-preserved-at-the-time-of-importing-design-package}

Toute propriété de page (par exemple, Domaine personnalisé, Application HTTPS, etc.) définie pour une page (qui utilise le modèle Page de destination vierge) avant d’importer le package de conception est perdue une fois la conception importée. Par conséquent, la pratique recommandée consiste à définir les propriétés de page après l’import du package de conception.

### Balisage uniquement HTML supposé {#html-only-markup-assumed}

Lors de lʼimport, le balisage est nettoyé pour des raisons de sécurité et afin dʼéviter lʼimport et la publication de balisage non valide. Cela suppose que les balises HTML et que toutes les autres formes d’éléments tels que les SVG en ligne ou les composants web soient filtrées.

### Texte {#text}

Balise HTML permettant d’insérer un composant texte (`foundation/components/text`) dans le fichier HTML à l’intérieur du package de conception :

```xml
<div data-cq-component="text"> <p>This is some editable text</p> </div>
```

L’insertion des balises ci-dessus dans le fichier HTML produit les effets suivants :

* Crée un composant texte AEM modifiable (`sling:resourceType=foundation/components/text`) dans la page de destination créée après l’importation du module de conception.
* Définit la propriété `text` du composant texte créé sur le code HTML placé entre les balises `div`.

**Déclaration courte des balises de composant** :

```xml
<p data-cq-component="text">Text component shorthand</p>
```

**Texte avec liste**

Pour ajouter un texte avec une liste :

* 1st
* 2nd

qui peut être modifié dans l’éditeur de texte enrichi :

```xml
<div data-cq-component="text"><p>This is text with a list:</p><ul><li>1st</li><li>2nd</li></ul><p>It can be edited with the RTE editor</p></div>
```

**Texte avec couleur**

Pour ajouter un texte de couleur (rose) qui peut être modifié dans l’éditeur de texte enrichi :

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

Le composant Titre prend en charge sept types : `h1, h2, h3, h4, h5, h6` et `default`.

**Déclaration courte des balises de composant** :

```xml
<h1 data-cq-component="title">Title component shorthand</h1>
```

### Image {#image}

Balisage HTML pour insérer un composant d’image (foundation/components/image) dans le HTML dans le package de conception :

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

**Déclaration courte des balises du composant :**

```xml
<img data-cq-component="image" src="test.png" alt="Image component shorthand"/>
```

#### L’élément img src d’URL absolue n’est pas pris en charge dans la balise Div du composant Image. {#absolute-url-img-src-not-supported-within-image-component-div}

Si une balise `<img>` avec une adresse URL &lt;src> absolue est utilisée pour la conversion d’un composant, une exception **UnsupportedTagContentException** appropriée est générée. Par exemple, le code suivant n’est pas pris en charge :

`<div data-cq-component="image">`

`<img src="https://cdn.printfriendly.com/pf-button.gif" alt="Print Friendly and PDF"/>`

`</div>`

Dans le cas contraire, les images d’URL absolues sont prises en charge pour les balises img qui ne font pas partie de la balise div du composant d’image.

### Composants d’appel à l’action {#call-to-action-components}

Vous pouvez marquer une partie de la page de destination pour l’importation sous forme de « composant CTA modifiable ». Les composants de ce type peuvent être modifiés après l’importation de la page de destination. AEM comprend les composants CTA suivants :

* Lien de clics publicitaires : permet d’ajouter un lien texte qui, lorsqu’il est fait l’objet d’un clic, dirige le visiteur ou la visiteuse vers une URL cible.
* Lien graphique : permet d’ajouter une image qui, lorsqu’elle fait l’objet d’un clic, dirige le visiteur ou la visiteuse vers une URL cible.

#### Lien de clics publicitaires {#click-through-link}

Vous pouvez utiliser ce composant CTA pour ajouter un lien textuel sur la page de destination.

Propriétés prises en charge

* Libellé, avec options de gras, d’italique et de soulignement
* URL cible, prend en charge l’URL tierce et AEM
* Options de rendu de page (même fenêtre, nouvelle fenêtre, etc.)

Balise HTML permettant d’inclure le composant « clics publicitaires » dans le fichier ZIP importé. Ici href mappe sur l’URL cible, « Afficher les détails du produit » mappe sur le libellé, etc.

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

Ce composant peut être utilisé dans n’importe quelle application autonome ou importé à partir d’un fichier zip.

**Déclaration courte des balises de composant** :

```xml
<a href="/somelink.html" data-cq-component="clickThroughLink">Click Through Link shorthand</a>
```

#### Lien graphique {#graphical-link}

Vous pouvez utiliser ce composant CTA pour ajouter une image graphique avec un lien sur la page de destination. Il peut s’agir d’un simple bouton ou d’une image en arrière-plan. Lorsqu’une personne clique sur l’image, elle accède à l’URL cible spécifiée dans les propriétés du composant. Il fait partie du groupe « Appel à l’action ».

Propriétés prises en charge

* Recadrage d’image, rotation
* Texte de survol, description, taille en px
* URL cible, prend en charge l’URL tierce et AEM
* Options de rendu de page (même fenêtre, nouvelle fenêtre, etc.)

Balise HTML permettant d’inclure le composant « lien graphique » dans le fichier ZIP importé. Ici href mappe sur l’URL cible, img src est l’image de rendu, « title » est utilisé comme texte de survol, etc.

```xml
<div id="cqcanvas">
  <div data-cq-component="clickThroughGraphicalLink"><a href="https://www.adobe.com/go/wem"><img src="img/call-to-action-button.png" title="Click Here to Learn More" /></a></div>
</div>
```

**Déclaration courte des balises de composant** :

```xml
<a href="/somelink.html" data-cq-component="clickThroughGraphicalLink"><img src="linkimage.png" alt="Click Through Graphical Link shorthand"/></a>
```

>[!NOTE]
>
>Pour créer un lien graphique à cliquer, vous devez encapsuler une balise &lt;anchor> et la balise d’image dans une balise &lt;div> avec l’attribut `data-cq-component="clickthroughgraphicallink"`.
>
>Par exemple, `<div data-cq-component="clickthroughlink"> <a href="https://myURLhere/"><img src="image source here"></a> </div>`.
>
>Les autres façons d’associer une image à une balise d’ancrage à l’aide des CSS ne sont pas prises en charge. Par exemple, le balisage suivant ne fonctionne pas :
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

Le formulaire de piste est utilisé pour collecter des informations sur le profil d’un visiteur/prospect. Ces informations pourront être stockées et exploitées ultérieurement pour mener une campagne marketing efficace. Il s’agit généralement du titre, du nom, de l’adresse e-mail, de la date de naissance, de l’adresse, du centre d’intérêt, etc. Il fait partie du groupe « Formulaire de prospect CTA ».

**Fonctionnalités prises en charge**

* Champs de prospect prédéfinis : les boutons Prénom, Nom, Adresse, Fonction, À propos de, ID utilisateur, ID d’e-mail et Envoyer sont disponibles dans le Sidekick. Il vous suffit de faire glisser le composant requis dans votre formulaire de prospect.
* Grâce à ces composants, l’auteur peut concevoir un formulaire de prospect autonome. Ces champs correspondent à ceux du formulaire de prospect. Dans une application ZIP importée ou autonome, l’utilisateur ou utilisatrice peut ajouter des champs à l’aide des champs de formulaire de prospect cq:form ou cta, les nommer et les concevoir en fonction des besoins.
* Mappez les champs de formulaire de prospect à l’aide de noms prédéfinis spécifiques du formulaire de prospect CTA ; par exemple, firstName pour first-name dans le formulaire de prospect, etc.
* Les champs qui ne sont pas mappés sur un formulaire de prospect le sont sur des composants cq:form : texte, case d’option, case à cocher, liste déroulante, masqué, mot de passe.
* L’utilisateur ou l’utilisatrice peut fournir le titre à l’aide de la balise « label » et indiquer le style en utilisant l’attribut de style « class » (disponible uniquement pour les composants du formulaire de prospect CTA).
* La page de remerciements et la liste d’abonnements peuvent être fournies sous forme de paramètre masqué du formulaire (présent dans le fichier index.htm) ou être ajoutées ou modifiées dans la barre de modification de « Début du formulaire de prospect ».

  &lt;input type=&quot;hidden&quot; name=&quot;redirectUrl&quot; value=&quot;/content/we-retail/en/user/register/thank_you&quot;/>

  &lt;input type=&quot;hidden&quot; name=&quot;groupName&quot; value=&quot;leadForm&quot;/>

* Des contraintes (telles qu’« Obligatoire ») peuvent être fournies à partir de la configuration de modification de chaque composant.

Balise HTML permettant d’inclure le composant « lien graphique » dans le fichier ZIP importé. Ici, « firstName » est mappé sur le firstName du formulaire de prospect, etc., à l’exception des cases à cocher : ces deux cases à cocher sont mappées sur le composant déroulant cq:form.

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

### Parsys (système de paragraphes) {#parsys}

Le composant parsys d’AEM est un composant conteneur qui peut contenir d’autres composants AEM. Vous pouvez ajouter un composant parsys dans le fichier HTML importé. Cela permet à l’utilisateur ou utilisatrice d’ajouter/supprimer des composants AEM modifiables à la page de destination même après son import.

Le système de paragraphes permet aux utilisateurs et utilisatrices d’ajouter des composants à l’aide du sidekick.

Balise HTML permettant d’insérer un composant parsys (`foundation/components/parsys`) dans le fichier HTML à l’intérieur du package de conception :

```xml
<div data-cq-component="parsys">
   <div data-cq-component="title"><h2>ULTIMATE PROTECTION</h2></div>
        <div data-cq-component="title"><h3>ON SALE</h3></div>
</div>
```

L’insertion des balises ci-dessus dans le fichier HTML produit les effets suivants :

* Insère un composant parsys d’AEM (foundation/components/parsys) dans la page de destination créée après l’import du package de conception.
* Initialisation du Sidekick avec des composants par défaut. De nouveaux composants peuvent être ajoutés à la page de destination en faisant glisser les composants du sidekick vers le composant parsys.
* Deux composants de titre font également partie du système de paragraphes.

### Cible {#target}

Le composant cible affiche le contenu d’une expérience sur la page : Il peut y avoir de nombreuses expériences créées dans une campagne et le composant cible peut afficher dynamiquement le contenu de différentes expériences aux différents utilisateurs et utilisatrices qui visitent la page.

Balisage HTML permettant d’insérer un composant cible et de créer différentes expériences dans une campagne :

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

## Options d’import supplémentaires {#additional-importing-options}

En plus de spécifier si les composants importés sont des composants AEM modifiables, vous pouvez également configurer les éléments suivants avant d’importer le package de conception :

* Définition des propriétés de page en extrayant les métadonnées définies dans le HTML importé.
* Spécification du codage du jeu de caractères dans le HTML.
* Recouvrement du modèle de page de l’importateur.

### Définition des propriétés de page en extrayant les métadonnées définies dans le HTML importé {#setting-page-properties-by-extracting-metadata-defined-in-imported-html}

Les métadonnées suivantes déclarées dans l’en-tête du HTML importé doivent être extraites et conservées par l’importateur de conception en tant que propriété « jcr:description » :

* &lt;meta name=&quot;description&quot; content=&quot;&quot;>

L’attribut Lang défini dans la balise HTML doit être extrait et conservé par l’importateur de conception en tant que propriété « jcr:language ».

* &lt;html lang=&quot;en&quot;>

### Spécification du codage du jeu de caractères dans le fichier HTML {#specifying-the-charset-encoding-in-the-html}

L’importateur de conception lit le codage spécifié dans le fichier HTML importé. Le codage peut être spécifié comme suit :

`<meta charset="UTF-8">`

*OU*

`<meta http-equiv="content-type" content="text/html;charset=utf-8">`

Si aucun codage n’est spécifié dans le HTML importé, le codage par défaut défini par l’importateur de conception est UTF-8.

### Superposition d’un modèle {#overlaying-template}

Vous pouvez recouvrir le modèle Page de destination vierge en créant un autre modèle dans `/apps/<appName>/designimporter/templates/<templateName>`.

Vous trouverez [ici](/help/sites-developing/templates.md) la procédure de création d’un modèle dans AEM.

### Référencement d’un composant à partir de la page de destination {#referring-a-component-from-landing-page}

Supposons que vous souhaitiez référencer un composant dans votre fichier HTML à l’aide de l’attribut data-cq-component, de telle sorte que l’importateur de conception effectue le rendu d’un composant include à cet emplacement. Vous souhaitez, par exemple, référencer le composant Table (`resourceType = /libs/foundation/components/table`). Vous devez ajouter ce qui suit dans le fichier HTML :

`<div data-cq-component="/libs/foundation/components/table">foundation table</div>`

Le chemin d’accès dans le composant data-cq-component doit être le resourceType du composant.

### Bonnes pratiques {#best-practices}

L’utilisation de sélecteurs CSS similaires aux suivants n’est pas recommandée avec les éléments marqués pour la conversion de composants lors de l’import.

| E > F | un élément F immédiatement précédé par un élément E | [Combinateur enfant](https://www.w3.org/TR/css3-selectors/#child-combinators) |
|---|---|---|
| E + F | un élément F qui est le fils d’un élément E | [Combinateur frère adjacent](https://www.w3.org/TR/css3-selectors/#adjacent-sibling-combinators) |
| E ~ F | un élément F précédé d’un élément E | [Combinateur frère général](https://www.w3.org/TR/css3-selectors/#general-sibling-combinators) |
| E:root | un élément E, racine du document | [Pseudo-classes structurelles](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-child(n) | un élément E, le n-ième enfant de son parent | [Pseudo-classes structurelles](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-last-child(n) | un élément E, le n-ième enfant de son parent, en comptant à partir du dernier | [Pseudo-classes structurelles](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-of-type(n) | un élément E, le n-ième frère de son type | [Pseudo-classes structurelles](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-last-of-type(n) | un élément E, le n-ième frère de son type, en comptant à partir du dernier | [Pseudo-classes structurelles](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |

En effet, des éléments HTML supplémentaires tels que les balises &lt;div> sont ajoutés au fichier Html généré après l’import.

* Les scripts reposant sur une structure similaire à ci-dessus ne sont pas non plus recommandés pour une utilisation avec des éléments marqués pour conversion en composants AEM.
* Il est déconseillé d’utiliser des styles sur les balises de mise en forme pour la conversion d’un composant, comme &lt;div data-cq-component=&quot;&amp;ast;&quot;>.
* La disposition de conception doit suivre les bonnes pratiques relatives au modèle HTML5 Boilerplate. Pour en savoir plus, consultez [https://html5boilerplate.com/](https://html5boilerplate.com/).

## Configuration de modules OSGI {#configuring-osgi-modules}

Les composants qui exposent des propriétés configurables par le biais de la console OSGI sont les suivants :

* Importateur de conception de page de destination
* Générateur de page de destination
* Générateur de page de destination pour appareils mobiles
* Préprocesseur de saisie de page de destination

Le tableau ci-dessous décrit brièvement les propriétés :

<table>
 <tbody>
  <tr>
   <td><strong>Composant</strong></td>
   <td><strong>Nom de la propriété</strong></td>
   <td><strong>Description de la propriété </strong></td>
  </tr>
  <tr>
   <td>Importateur de conception de page de destination</td>
   <td>Extraire le filtre</td>
   <td>Liste des expressions régulières à utiliser pour le filtrage des fichiers de l’extraction. <br />Les entrées zip correspondant à l’un des modèles spécifiés sont exclues de l’extraction.</td>
  </tr>
  <tr>
   <td>Générateur de page de destination</td>
   <td>Modèle de fichier</td>
   <td>Le générateur de pages de destination peut être configuré pour traiter les fichiers HTML correspondant à une expression régulière, tel que défini par le modèle de fichier.</td>
  </tr>
  <tr>
   <td>Générateur de page de destination pour appareils mobiles</td>
   <td>Modèle de fichier</td>
   <td>Le générateur de pages de destination peut être configuré pour traiter les fichiers HTML correspondant à une expression régulière, tel que défini par le modèle de fichier.</td>
  </tr>
  <tr>
   <td> </td>
   <td>Groupes de périphériques</td>
   <td>Liste des groupes d’appareils à prendre en charge.</td>
  </tr>
  <tr>
   <td>Préprocesseur de saisie de page de destination</td>
   <td>Motif de recherche </td>
   <td>Motif à rechercher, dans le contenu d’entrée de l’archive. Dans le cas de cette expression régulière, une correspondance est effectuée, ligne par ligne, avec le contenu de l’entrée. En cas de correspondance, le texte concerné est remplacé par le modèle de remplacement spécifié.<br /> <br /> Reportez-vous à la remarque ci-dessous concernant les limitations actuelles du préprocesseur de saisie de pages d’entrée.</td>
  </tr>
  <tr>
   <td> </td>
   <td>Modèle de remplacement</td>
   <td>Modèle qui remplace les correspondances trouvées. Vous pouvez utiliser des références de groupe regex, telles que $1, $2. Ce modèle prend également en charge des mots-clés tels que {designPath}, qui sont résolus avec leur valeur réelle au cours de l’import.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>**Limites actuelles du préprocesseur de saisie de page de destination :**
>Si vous devez apporter des modifications au modèle de recherche, lorsque vous ouvrez l’éditeur de propriétés Felix, vous devez ajouter manuellement des barres obliques inversées pour utiliser les métacaractères regex. Si vous n’ajoutez pas manuellement de barre oblique inverse, la regex est considérée comme non valide et ne remplacera pas l’ancienne.
>
>Par exemple, si la configuration par défaut est
>
>>`/\* *CQ_DESIGN_PATH *\*/ *(['"])`
>
>Et vous devez remplacer `CQ_DESIGN_PATH` par `VIPURL` dans le modèle de recherche, qui doit se présenter comme suit :
>
>`/\* *VIPURL *\*/ *(['"])`

## Résolution des problèmes {#troubleshooting}

Lors de l’import du package de conception, plusieurs erreurs peuvent se produire. Découvrez-les dans cette section.

### Initialisation du sidekick avec les composants pertinents de la page de destination {#initialization-of-sidekick-with-landing-page-relevant-components}

Si le package de conception contient des balises de composant parsys, le Sidekick commence à afficher les composants relatifs à la page d’entrée après l’importation. Vous pouvez faire glisser de nouveaux composants sur le composant parsys à l’intérieur de votre page de destination. Vous pouvez également accéder au mode de conception et ajouter de nouveaux composants au sidekick.

### Messages d’erreur affichés au cours de l’importation {#error-messages-displayed-during-import}

En cas d’erreur (par exemple, le package importé n’est pas un fichier zip valide), l’import de conception n’importe pas le package. Un message d’erreur s’affiche en haut de la page, juste au-dessus de la zone de dépôt. Des exemples de scénarios d’erreur sont présentés ici. Une fois l’erreur corrigée, vous pouvez réimporter le fichier zip mis à jour sur la même page de destination vierge. Les différents scénarios où des erreurs sont générées sont les suivants :

* Le package de conception importé n’est pas une archive ZIP valide.
* Le package de conception importé ne comporte pas de fichier index.html au niveau supérieur.

### Avertissements affichés après l’importation {#warnings-displayed-after-import}

Si des avertissements sont générés (par exemple, le fichier HTML fait référence à des images qui n’existent pas dans le package), l’importateur de conception importe le fichier ZIP, mais affiche, en même temps, une liste d’erreurs/avertissements dans le volet Résultat. Si vous cliquez sur le lien Problèmes, une liste d’avertissements, qui indique les problèmes éventuels survenus dans le package de conception, s’affiche. Voici différents scénarios dans lesquels l’importateur de conception a intercepté et affiché des avertissements :

* Le fichier HTML fait référence à des images qui n’existent pas dans le package.
* Le fichier HTML fait référence à des scripts qui n’existent pas dans le package.
* Le fichier HTML fait référence à des styles qui n’existent pas dans le package.

### Où les fichiers du fichier ZIP sont-ils stockés dans AEM ? {#where-are-the-files-of-the-zip-file-being-stored-in-aem}

Une fois la page de destination importée, les fichiers (images, css, js, etc.) du package de conception sont stockés à l’emplacement suivant dans AEM :

`/etc/designs/default/canvas/content/campaigns/<name of brand>/<name of campaign>/<name of landing page>`

Supposons que la landing page soit créée sous la campagne `We.Retail` et le nom de la landing page est **myBlankLandingPage** alors l’emplacement où les fichiers zip sont stockés est le suivant :

`/etc/designs/default/canvas/content/campaigns/geometrixx/myBlankLandingPage`

### Mise en forme non conservée {#formatting-not-preserved}

Lors de la création de votre CSS, tenez compte des limites suivantes :

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

`box img` est utilisé dans l’importateur de conception, la page de destination qui en résulte semble ne pas avoir conservé la mise en forme. Pour contourner ce problème, sachez qu’AEM ajoute des balises div dans le CSS et réécrit le code en conséquence. Dans le cas contraire, certaines règles CSS ne seront pas valides.

```xml
.box img

{ float:right; margin: 0 0 5px 5px; border: 1px #343434 solid; }
```

>[!NOTE]
>
>Les concepteurs et conceptrices ne doivent coder qu’à l’intérieur de la balise **id=cqcanvas** reconnue par l’importateur, sinon la conception n’est pas conservée.
