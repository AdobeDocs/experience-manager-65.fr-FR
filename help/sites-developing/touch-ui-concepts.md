---
title: Concepts de l’interface utilisateur tactile d’Adobe Experience Manager
description: Avec Adobe Experience Manager 5.6, Adobe a introduit une nouvelle interface utilisateur optimisée pour les écrans tactiles en responsive design pour l’environnement de création.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: f13ac6c2-16ab-422d-9005-ab0b49172271
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '2147'
ht-degree: 100%

---

# Concepts de l’interface utilisateur tactile d’Adobe Experience Manager{#concepts-of-the-aem-touch-enabled-ui}

Adobe Experience Manager (AEM) dispose d’une interface d’utilisation tactile en [responsive design](/help/sites-authoring/responsive-layout.md) pour l’environnement de création conçue pour fonctionner sur les appareils tactiles et de bureau.

>[!NOTE]
>
>L’IU tactile est l’IU standard d’AEM. L’IU classique est devenue obsolète avec AEM 6.4.

L’interface utilisateur tactile se compose des éléments suivants :

* L’en-tête de la suite qui :
   * affiche le logo,
   * fournit un lien vers la navigation globale,
   * fournit le lien vers d’autres actions génériques, comme Rechercher, Aide, Solutions Experience Cloud, Notifications et Paramètres utilisateur.
* Le rail de gauche (affiché lorsque cela s’avère nécessaire et pouvant être masqué) qui peut afficher les options suivantes :
   * Chronologie
   * Références
   * Filtres
* En-tête de navigation, qui est à nouveau contextuel et peut afficher les éléments suivants :
   * La console en cours d’utilisation et/ou la position au sein de cette console
   * Sélection pour le rail gauche.
   * Chemin de navigation
   * Accès aux actions **Créer** appropriées
   * Afficher les sélections
* La zone de contenu qui :
   * répertorie les éléments de contenu (qu’il s’agisse de pages, de ressources, de messages de forum, etc.) ;
   * peut être formatée comme demandé, par exemple, colonne, carte ou liste ;
   * utilise la technologie responsive design (l’affichage est redimensionné automatiquement en fonction de la taille de l’appareil et/ou de la fenêtre) ;
   * utilise le défilement infini (plus de pagination, tous les éléments sont répertoriés sur une seule fenêtre).

![chlimage_1-79](assets/chlimage_1-79.png)

>[!NOTE]
>
>Presque toutes les fonctionnalités d’AEM ont été portées sur l’interface utilisateur tactile. Cependant, dans certains cas limités, les fonctionnalités reviennent à l’interface utilisateur classique. Voir [Statut des fonctionnalités de l’interface utilisateur tactile](/help/release-notes/touch-ui-features-status.md) pour plus d’informations.

L’interface utilisateur tactile a été conçue par Adobe pour assurer la cohérence de l’expérience client entre plusieurs produits. Elle repose sur les éléments suivants :

* **Interface utilisateur Coral** (CUI), une implémentation du style visuel d’Adobe pour l’interface utilisateur tactile. L’interface utilisateur Coral fournit tout ce dont votre produit/projet/application web a besoin pour adopter le style visuel de l’interface utilisateur.
* Les composants d’**interface utilisateur Granite** sont construits avec l’IU Coral.

Les principes de base de l’interface utilisateur tactile sont les suivants :

* Mobile en priorité (en pensant toutefois à la version de bureau)
* Responsive Design
* Affichage contextuel
* Réutilisable
* Inclusion de la documentation de référence intégrée
* Inclusion des tests intégrés
* Approche ascendante pour garantir l’application de ces principes à tous les éléments et composants

Pour une vue d’ensemble plus détaillée de la structure de l’interface utilisateur tactile, consultez [Structure de l’interface utilisateur tactile d’AEM](/help/sites-developing/touch-ui-structure.md).

## Pile technologique AEM {#aem-technology-stack}

AEM utilise la plateforme Granite comme base et la plateforme Granite comprend, entre autres, le référentiel de contenu Java™.

![chlimage_1-80](assets/chlimage_1-80.png)

## Granite {#granite}

Granite est la pile web ouverte d’Adobe, fournissant divers composants, notamment :

* Un lanceur d’application
* Un framework OSGi dans lequel tout est déployé
* Plusieurs services de compendium OSGi pour prendre en charge la création d’applications
* Un framework de journalisation complet fournissant diverses API de journalisation
* L’implémentation du référentiel CRX de la spécification de l’API JCR
* Le framework web Apache Sling
* Les éléments supplémentaires du produit CRX actuel

>[!NOTE]
>
>Granite est géré comme un projet de développement ouvert au sein d’Adobe : les contributions au code, les discussions et les problèmes proviennent de toute l’entreprise.
>
>Cependant, Granite **n’est pas** un projet open source. Il dépend très largement de plusieurs projets open source (Apache Sling, Felix, Jackrabbit et Lucene, en particulier), mais Adobe distingue clairement l’aspect public du contenu interne.

## IU Granite {#granite-ui}

La plateforme d’ingénierie Granite fournit également un framework d’interface utilisateur de base. Les principaux objectifs de celui-ci sont les suivants :

* Fournir des widgets d’interface utilisateur granulaires
* Implémenter les concepts de l’IU et illustrer les bonnes pratiques (rendu de listes longues, filtrage de listes, CRUD objet, assistants CUD...)
* Fournir une interface utilisateur d’administration extensible et basée sur des plug-ins

Ceux-ci répondent aux exigences suivantes :

* Respecter la notion de « mobile en priorité »
* Être extensible
* Être facile à remplacer

![chlimage_1-81](assets/chlimage_1-81.png)
GraniteUI.pdf

[Obtenir le fichier](assets/graniteui.pdf)
L’IU Granite :

* Utilise l’architecture RESTful de Sling.
* Implémente des bibliothèques de composants destinées à la création d’applications web centrées sur le contenu.
* Fournit des widgets d’interface utilisateur granulaires.
* Fournit une interface utilisateur standardisée par défaut.
* Est extensible.
* Est conçue pour les appareils mobiles et de bureau (respecte la notion de mobile en priorité).
* Peut être utilisée dans une plateforme/un produit/un projet basés sur Granite ; par exemple, AEM.

![chlimage_1-82](assets/chlimage_1-82.png)

* [Composants de base de l’IU Granite](#granite-ui-foundation-components)
Cette bibliothèque de composants de base peut être utilisée ou étendue par d’autres bibliothèques.
* [Composants d’administration de l’IU Granite](#granite-ui-administration-components)

### Côté client et côté serveur {#client-side-vs-server-side}

La communication client-serveur dans l’interface utilisateur Granite se compose d’hypertexte et non d’objets, le client n’a donc pas besoin de comprendre la logique commerciale.

* Le serveur enrichit le code HTML avec des données sémantiques.
* Le client enrichit l’hypertexte avec l’hypermédia (interaction).

![chlimage_1-83](assets/chlimage_1-83.png)

#### Côté client {#client-side}

Celui-ci utilise une extension du vocabulaire HTML, fournie pour que la personne chargée de la création puisse exprimer son intention de créer une application web interactive. Il s’agit d’une approche similaire à [WAI-ARIA](https://www.w3.org/TR/wai-aria/) et aux [microformats](https://microformats.org/).

Il s’agit principalement d’un ensemble de modèles d’interaction (par exemple, la soumission asynchrone d’un formulaire) qui sont interprétés par des codes JS et CSS, exécutés côté client. Le rôle du côté client est d’améliorer le balisage (donné comme capacité hypermédia par le serveur) pour l’interactivité.

Le côté client est indépendant de toute technologie de serveur. Tant que le serveur donne le balisage approprié, le côté client peut remplir son rôle.

Actuellement, les codes JS et CSS sont fournis sous forme de [bibliothèques clientes](/help/sites-developing/clientlibs.md) Granite dans la catégorie :

`granite.ui.foundation and granite.ui.foundation.admin`

Elles sont distribuées dans le cadre du package de contenu :

`granite.ui.content`

#### Côté serveur {#server-side}

Cela est formé par un ensemble de composants Sling qui permettent à la personne chargée de la création de *composer* rapidement une application web. Le développement consiste à développer des composants, la création à assembler les composants pour constituer une application web. Le rôle du côté serveur est de donner la capacité hypermédia (balisage) au client.

Actuellement, les composants se trouvent dans le référentiel Granite à l’adresse :

`/libs/granite/ui/components/foundation`

Il est distribué dans le cadre du package de contenu :

`granite.ui.content`

### Différences avec l’IU classique {#differences-with-the-classic-ui}

Il est aussi intéressant d’examiner les différences entre l’IU Granite et ExtJS (utilisé pour l’IU classique) :

<table>
 <tbody>
  <tr>
   <td><strong>ExtJS</strong></td>
   <td><strong>IU Granite</strong></td>
  </tr>
  <tr>
   <td>Appel de procédure à distance<br /> </td>
   <td>Transitions d’état</td>
  </tr>
  <tr>
   <td>Objets de transfert de données</td>
   <td>Hypermédia</td>
  </tr>
  <tr>
   <td>Le client connaît les paramètres internes du serveur.</td>
   <td>Le client ne connaît pas les informations internes.</td>
  </tr>
  <tr>
   <td>« Client lourd »</td>
   <td>« Client léger »</td>
  </tr>
  <tr>
   <td>Bibliothèques clientes spécialisées</td>
   <td>Bibliothèques client universelles</td>
  </tr>
 </tbody>
</table>

### Composants de base de l’IU Granite {#granite-ui-foundation-components}

Les [composants de base de l’interface utilisateur Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html) fournissent les éléments de base nécessaires à la création de n’importe quelle interface utilisateur. Ils comprennent entre autres les éléments suivants :

* Bouton
* Lien hypertexte
* Avatar de l’utilisateur ou de l’utilisatrice

Les composants principaux se trouvent dans :

`/libs/granite/ui/components/foundation`

Cette bibliothèque contient un composant d’IU Granite pour chaque élément Coral. Un composant est piloté par le contenu, sa configuration résidant dans le référentiel. Cela permet de composer une application IU Granite sans écrire manuellement de balises HTML.

Objectif :

* Modèle de composant des éléments HTML
* Composition des composants
* Tests unitaires et de fonctionnalités automatiques

Mise en œuvre :

* Composition et configuration basées sur un référentiel
* Utiliser les installations de test fournies par la plateforme Granite
* Modèles JSP

Cette bibliothèque de composants de base peut être utilisée ou étendue par d’autres bibliothèques.

### ExtJS et composants d’interface utilisateur Granite correspondants {#extjs-and-corresponding-granite-ui-components}

Lors de la mise à niveau du code ExtJS pour utiliser l’IU Granite, la liste suivante fournit une vue d’ensemble pratique des xtypes ExtJS et des types de nœuds avec les types de ressources équivalents dans l’IU Granite.

| **ExtJS xtype** | **Type de ressource de l’IU Granite** |
|---|---|
| `button` | `granite/ui/components/foundation/form/button` |
| `checkbox` | `granite/ui/components/foundation/form/checkbox` |
| `componentstyles` | `cq/gui/components/authoring/dialog/componentstyles` |
| `cqinclude` | `granite/ui/components/foundation/include` |
| `datetime` | `granite/ui/components/foundation/form/datepicker` |
| `dialogfieldset` | `granite/ui/components/foundation/form/fieldset` |
| `hidden` | `granite/ui/components/foundation/form/hidden` |
| `html5smartfile, html5smartimage` | `granite/ui/components/foundation/form/fileupload` |
| `multifield` | `granite/ui/components/foundation/form/multifield` |
| `numberfield` | `granite/ui/components/foundation/form/numberfield` |
| `pathfield, paragraphreference` | `granite/ui/components/foundation/form/pathbrowser` |
| `selection` | `granite/ui/components/foundation/form/select` |
| `sizefield` | `cq/gui/components/authoring/dialog/sizefield` |
| `tags` | `granite/ui/components/foundation/form/autocomplete``cq/gui/components/common/datasources/tags` |
| `textarea` | `granite/ui/components/foundation/form/textarea` |
| `textfield` | `granite/ui/components/foundation/form/textfield` |

| **Type de nœud** | **Type de ressource de l’IU Granite** |
|---|---|
| `cq:WidgetCollection` | `granite/ui/components/foundation/container` |
| `cq:TabPanel` | `granite/ui/components/foundation/container``granite/ui/components/foundation/layouts/tabs` |
| `cq:panel` | `granite/ui/components/foundation/container` |

### Composants d’administration de l’IU Granite {#granite-ui-administration-components}

Les [composants d’administration de l’IU Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html) dépendent des composants de base pour fournir les éléments génériques que toute application d’administration peut implémenter. Il peut s’agir, entre autres :

* Barre de navigation globale
* Rail (squelette)
* Panneau de recherche

Objectif :

* Apparence unifiée pour les applications d’administration
* RAD pour les applications d’administration

Mise en œuvre :

* Composants prédéfinis utilisant les composants de base
* Composants personnalisables

## IU Coral {#coral-ui}

CoralUI.pdf

[Obtenir le fichier](assets/coralui.pdf)
L’interface utilisateur Coral (CUI) est une implémentation du style visuel d’Adobe pour l’interface utilisateur tactile. Elle a été conçue par Adobe pour garantir une expérience client homogène entre plusieurs produits. L’IU Coral fournit tout ce dont vous avez besoin pour adopter le style visuel utilisé dans l’environnement de création.

>[!CAUTION]
>
>L’IU Coral est une bibliothèque d’interface utilisateur mise à la disposition des clientes et clients AEM pour créer des applications et des interfaces web dans les limites de leur utilisation sous licence du produit.
>
>L’utilisation de l’IU Coral est autorisée uniquement dans les cas suivants :
>
>
>* Lorsqu’elle a été fournie avec AEM.
>* À utiliser lors de l’extension de l’interface utilisateur existante de l’environnement de création.
>* Documents marketing, publicités et présentations Adobe.
>* Interface utilisateur des applications de marque Adobe (la police ne doit pas être facilement disponible pour d’autres utilisations).
>* Avec des personnalisations mineures.
>
>L’utilisation de l’IU Coral doit être évitée pour les éléments suivants :
>
>* Documents et autres éléments non liés à Adobe.
>* Environnements de création de contenu (dans lesquels les éléments précédents peuvent être générés par d’autres).
>* Applications/composants/pages web qui ne sont pas clairement connectés à Adobe.
>

L’IU Coral est un ensemble de composantes de base destinées au développement d’applications web.

![chlimage_1-84](assets/chlimage_1-84.png)

Conçu pour être modulaire dès le départ, chaque module forme une couche distincte en fonction de son rôle principal. Bien que les couches aient été conçues pour se soutenir mutuellement, elles peuvent également être utilisées indépendamment si nécessaire. Cela permet d’implémenter l’expérience client de Coral dans n’importe quel environnement compatible HTML.

Avec l’interface utilisateur Coral, il n’est pas obligatoire d’utiliser un modèle et/ou une plateforme de développement en particulier. L’objectif principal de Coral est de fournir un balisage HTML5 unifié et propre, indépendant de la méthode réelle utilisée pour émettre ce balisage. Cela peut être utilisé pour le rendu côté client ou serveur, les modèles, les applications JSP, PHP ou même Adobe Flash RIA, pour ne nommer que ces éléments.

### Éléments HTML - Couche de balisage {#html-elements-the-markup-layer}

Les éléments HTML offrent une apparence commune pour tous les éléments d’interface utilisateur de base (y compris la barre de navigation, les boutons, les menus, le rail, etc.).

Au niveau le plus bas, un élément HTML est une balise HTML avec un nom de classe dédié. Les éléments plus complexes peuvent être composés de plusieurs balises, imbriquées les unes dans les autres (d’une manière spécifique).

Le code CSS est utilisé pour définir l’apparence réelle. Pour qu’il soit possible de personnaliser facilement l’apparence (dans le cas d’une valorisation de marque, par exemple), les valeurs de style proprement dites sont déclarées en tant que variables qui sont étendues par le préprocesseur [LESS](https://lesscss.org/) lors de la phase d’exécution.

Objectif :

* Fournir des éléments d’interface utilisateur de base avec une apparence commune
* Fournir le système de grille par défaut

Mise en œuvre :

* Balises HTML avec des styles inspirés de [Bootstrap](https://twitter.github.com/bootstrap/)
* Les classes sont définies dans des fichiers LESS.
* Les icônes sont définies comme des sprites de police.

Par exemple, le balisage suivant :

```xml
<button class="btn btn-large btn-primary" type="button">Large button</button>
<button class="btn btn-large" type="button">Large button</button>
```

s’affiche sous la forme :

![chlimage_1-85](assets/chlimage_1-85.png)

L’apparence est définie dans un fichier LESS et liée à un élément par un nom de classe dédié (l’extrait suivant a été raccourci dans un souci de concision) :

```xml
.btn {
    font-size: @baseFontSize;
    line-height: @baseLineHeight;
    .buttonBackground(@btnBackground,
                                @btnBackgroundHighlight,
                                @grayDark, 0 1px 1px rgba(255,255,255,.75));
```

Les valeurs réelles sont définies dans un fichier de variables LESS (l’extrait suivant a été raccourci dans un souci de concision) :

```xml
@btnBackgroundHighlight: darken(@white, 10%);
@btnPrimaryBackgroundHighlight: spin(@btnPrimaryBackground, 20%);
@baseFontSize: 17px;
@baseFontFamily: @sansFontFamily;
```

### Plug-ins d’éléments {#element-plugins}

De nombreux éléments HTML doivent présenter une sorte de comportement dynamique, tel que l’ouverture et la fermeture de menus contextuels. C’est le rôle des plug-ins d’éléments, qui accomplissent de telles tâches en manipulant le DOM à l’aide de JavaScript.

Un plug-in est soit :

* Conçu pour fonctionner sur un élément DOM spécifique. Par exemple, un module externe de boîte de dialogue s’attend à trouver `DIV class=dialog`.
* Générique par nature. Par exemple, un gestionnaire de mises en page fournit la disposition pour toute liste d’éléments `DIV` ou `LI`.

Le comportement du plug-in peut être personnalisé avec des paramètres, de l’une des manières suivantes :

* En transmettant les paramètres avec un appel JavaScript
* Utilisation d’attributs `data-*` dédiés liés au balisage HTML

Bien que le développeur puisse choisir la méthode la mieux adaptée à chaque module externe, le principe de base consiste à utiliser les éléments suivants :

* Des attributs `data-*` pour les options relatives à la mise en page HTML. Par exemple, pour spécifier le nombre de colonnes
* Options/classes API pour les fonctionnalités liées aux données. Par exemple, pour construire la liste des éléments à afficher

Le même concept est utilisé pour implémenter la validation de formulaire. Pour un élément qui doit être validé, vous devez spécifier le formulaire de saisie requis sous la forme d’un attribut `data-*` personnalisé. Cet attribut est ensuite utilisé comme option pour un module externe de validation.

>[!NOTE]
>
>La validation de formulaire native au format HTML5 doit être utilisée lorsque cela s’avère possible et/ou s’il y a une volonté de l’enrichir.

Objectif :

* Fournir un comportement dynamique pour les éléments HTML
* Fournir des dispositions personnalisées n’est pas possible avec une feuille de style CSS pure.
* Effectuer la validation de formulaires
* Effectuer une manipulation avancée du DOM

Mise en œuvre :

* Plug-in jQuery, lié à des éléments DOM spécifiques
* Utilisation d’attributs `data-*` pour personnaliser le comportement

Extrait de l’exemple de balisage (notez les options spécifiées sous la forme d’attributs data-&#42;) :

```xml
<ul data-column-width="220" data-layout="card" class="cards">
  <li class="item">
    <div class="thumbnail">
      <img href="/a.html" src="/a.thumb.319.319..png">
      <div class="caption">
        <h4>Toolbar</h4>
          <p><small>toolbar</small><br></p>
      </div>
    </div>
  </li>
  <li class="item">
    <div class="thumbnail">
      <img href="/a.html" src="/a.thumb.319.319..png">
      <div class="caption">
        <h4>Toolbar</h4>
        <p><small>toolbar</small><br></p>
      </div>
    </div>
  </li>
```

Appel au module externe jQuery :

```
$('.cards').cardlayout ();
```

Cela se présente comme suit :

![chlimage_1-86](assets/chlimage_1-86.png)

Le plug-in `cardLayout` dispose les éléments `UL` entre crochets sur leurs hauteurs respectives, en tenant également compte de la largeur du parent.

### Widgets d’éléments HTML {#html-elements-widgets}

Un widget combine un ou plusieurs éléments de base avec un plug-in JavaScript pour former des éléments d’interface utilisateur de « niveau supérieur ». Ceux-ci peuvent implémenter un comportement plus complexe ainsi qu’une apparence plus complexe qu’un seul élément ne pourrait offrir. Le sélecteur de balises et les widgets de rail constituent deux bons exemples.

Un widget peut se déclencher et écouter des événements personnalisés pour coopérer avec d’autres widgets sur la page. Certains widgets sont des widgets jQuery natifs qui utilisent les éléments HTML Coral.

Objectif :

* Implémenter des éléments d’IU de niveau supérieur présentant un comportement complexe
* Déclencher et gérer des événements

Mise en œuvre :

* Balisage HTML du plug-in jQuery
* Peut utiliser des modèles côté client/serveur.

Voici un exemple de balisage :

```
<input type="text" name="tags" placeholder="Tags" class="tagManager"/>
```

Appel au plug-in jQuery (avec options) :

```
$(".tagManager").tagsManager({
        prefilled: ["Pisa", "Rome"] })
```

Le plug-in émet un balisage HTML (ce balisage utilise des éléments de base, qui peuvent utiliser d’autres plug-ins en interne) :

```
<span>Pisa</code>
<a title="Removing tag" tagidtoremove="0"
   id="myRemover_0" class="myTagRemover" href="#">x</a></code>

<span id="myTag_1" class="myTag"><span>Rome</code>
<a title="Removing tag" tagidtoremove="1"
   id="myRemover_1" class="myTagRemover" href="#">x</a></code>

<input type="text" data-original-title="" class="input-medium tagManager"
       placeholder="Tags" name="tags" data-provide="typeahead" data-items="6"
       autocomplete="off">
```

Cela se présente comme suit :

![chlimage_1-87](assets/chlimage_1-87.png)

### Bibliothèque d’utilitaires {#utility-library}

Cette bibliothèque est un ensemble de fonctions et/ou de plug-ins d’assistants JavaScript qui ont les caractéristiques suivantes :

* Indépendance vis-à-vis de l’interface utilisateur
* Importance pourtant cruciale pour créer des applications web complètes

Ceux-ci incluent la gestion XSS et l’eventBus.

Bien que les plug-ins et widgets d’éléments HTML puissent s’appuyer sur des fonctionnalités fournies par la bibliothèque d’utilitaires, la bibliothèque d’utilitaires ne peut pas dépendre fortement des éléments ni des widgets eux-mêmes.

Objectif :

* Fourniture de fonctionnalités communes
* Implémentation de l’eventBus
* Modèles côté client
* XSS

Mise en œuvre :

* Plug-ins jQuery ou modules JavaScript compatibles AMD
