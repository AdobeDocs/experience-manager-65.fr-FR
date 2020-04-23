---
title: Aide-mémoire SCF
seo-title: Aide-mémoire SCF
description: Barres d'outils Méthodes d'aide pour faciliter le travail avec SCF
seo-description: Barres d'outils Méthodes d'aide pour faciliter le travail avec SCF
uuid: 9c514199-871e-4b68-8147-2052d2eeda15
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 8b6c1697-d693-41f4-8337-f41658465107
translation-type: tm+mt
source-git-commit: 0270cee1970b5b092361c2f1ad4a117795465311

---


# Aide-mémoire SCF {#scf-handlebars-helpers}

| **[⇐ Fonctionnalités Essentials](essentials.md)** | **[Personnalisation côté serveur](server-customize.md)** |
|---|---|
|  | **[Personnalisation côté client](client-customize.md)** |

Handlebars Helpers (aides) sont des méthodes appelables à partir des scripts Handlebars pour faciliter l’utilisation des composants SCF.

L’implémentation comprend une définition côté client et côté serveur. Il est également possible pour les développeurs de créer des assistants personnalisés.

Les assistants SCF personnalisés fournis avec les communautés AEM sont définis dans la bibliothèque [client](../../help/sites-developing/clientlibs.md):

* `/etc/clientlibs/social/commons/scf/helpers.js`

>[!NOTE]
>
>Assurez-vous d’installer le [dernier pack de fonctionnalités des communautés](deploy-communities.md#latestfeaturepack).


## Abrévier {#abbreviate}

Aide à renvoyer une chaîne abrégée conforme aux propriétés maxWords et maxLength.

La chaîne à abréger est fournie comme contexte. Si aucun contexte n’est fourni, une chaîne vide est renvoyée.

Tout d’abord, le contexte est réduit à maxLength, puis le contexte est divisé en mots et réduit à maxWords.

Si safeString est défini sur true, la chaîne renvoyée est une SafeString.

### Paramètres {#parameters}

* **contexte**: Chaîne

   (Facultatif) La valeur par défaut est la chaîne vide.

* **maxLength**: Nombre

   (Facultatif) La valeur par défaut est la longueur du contexte.

* **maxWords**: Nombre

   (Facultatif) La valeur par défaut est le nombre de mots de la chaîne rognée.

* **safeString**: Booléen

   (Facultatif) Renvoie une valeur Handlebars.SafeString() si true. La valeur par défaut est false.

### Exemples {#examples}

```
{{abbreviate subject maxWords=2}}

/*
If subject =
    "AEM Communities - Site Creation Wizard"

Then abbreviate would return
    "AEM Communities".
*/
```

```
{{{abbreviate message safeString=true maxLength=30}}}

/*
If message =
    "The goal of AEM Communities is to quickly create a community engagement site."

Then abbreviate would return
    "The goal of AEM Communities is"
*/
```

## Content-loadmore {#content-loadmore}

Une aide pour ajouter deux plages sous une balise div, l’une pour le texte intégral et l’autre pour le texte less, avec la possibilité de basculer entre les deux  de.

### Paramètres {#parameters-1}

* **contexte**: Chaîne

   (Facultatif) La valeur par défaut est la chaîne vide.

* **numChars**: Nombre

   (Facultatif) Nombre de caractères à afficher lorsque le texte intégral n’est pas affiché. La valeur par défaut est 100.

* **moreText**: Chaîne

   (Facultatif) Texte à afficher indiquant qu’il y a plus de texte à afficher. La valeur par défaut est &quot;more&quot;.

* **ellipsesText**: Chaîne

   (Facultatif) Texte à afficher indiquant qu’il existe du texte masqué. La valeur par défaut est &quot;...&quot;.

* **safeString**: Booléen

   (Facultatif) Valeur booléenne indiquant s’il faut appliquer Handlebars.SafeString() avant de renvoyer le résultat. La valeur par défaut est false.

### Exemple {#example}

```
{{content-loadmore  context numChars=32  moreText="go on"  ellipsesText="..." }}

/*
If context =
    "Here is the initial less content and this is more content."

Then content-loadmore would return
    "Here is the initial less content<span class="moreelipses">...</span> <span class="scf-morecontent"><span>and this is more content.</span>  <a href="" class="scf-morelink" evt="click=toggleContent">go on</a></span>"
*/
```

## DateUtil {#dateutil}

Aide à renvoyer une chaîne de date formatée.

### Paramètres {#parameters-2}

* **contexte**: Nombre

   (Facultatif) décalage de la valeur en millisecondes par rapport au 1er janvier 1970 (époque). La date par défaut est la date actuelle.

* **format**: Chaîne

   (Facultatif) Format de date à appliquer. La valeur par défaut est &quot;YYYY-MM-DTHH:mm:ss.sssZ&quot; et le résultat est &quot;2015-03-18T18:17:13-07:00&quot;.

### Exemples {#examples-1}

```
{{dateUtil this.memberSince format="dd MMM yyyy, hh:mm"}}

// returns "18 Mar 2015, 18:17"
```

```
{{dateUtil this.birthday format="MM-DD-YYYY"}}

// returns "03-18-2015"
```

## Equals {#equals}

Une aide pour renvoyer du contenu selon une condition d’égalité.

### Paramètres {#parameters-3}

* **lvalue**: Chaîne

   Valeur de gauche à comparer.

* **rvalue**: Chaîne

   Valeur de droite à comparer.

### Exemple {#example-1}

```
{{#equals  value "some-value"}}
  <div>They are EQUAL!</div>
{{else}}
  <div>They are NOT equal!</div>
{{/equals}}
```

## If-wcm-mode {#if-wcm-mode}

Aide de bloc qui teste la valeur actuelle du mode [](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html) WCM par rapport à un de modes séparé par des chaînes.

### Paramètres {#parameters-4}

* **contexte**: Chaîne

   (Facultatif) Chaîne à traduire. Obligatoire si aucune valeur par défaut n’est fournie.

* **mode**: Chaîne

   (Facultatif) Un de modes [](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html) WCM séparé par des virgules à tester s’il est défini.

### Exemple {#example-2}

```xml
{{#if-wcm-mode mode="DESIGN, EDIT"}}
 ...
{{else}}
 ...
{{/if-wcm-mode}}
```

## i18n {#i-n}

Cette aide remplace l’aide de Handlebars &quot;i18n&quot;.

Voir aussi [Internationalisation des chaînes dans le code](../../help/sites-developing/i18n-dev.md#internationalizing-strings-in-javascript-code)JavaScript.

### Paramètres {#parameters-5}

* **contexte**: Chaîne

   (Facultatif) Chaîne à traduire. Obligatoire si aucune valeur par défaut n’est fournie.

* **default**: Chaîne

   (Facultatif) Chaîne par défaut à traduire. Obligatoire si aucun contexte n’est fourni.

* **commentaire**: Chaîne

   (Facultatif) Indicatif de traduction

### Exemple {#example-3}

```
{{i18n "hello"}}
{{i18n "hello" comment="greeting" default="bonjour"}}
```

## Inclure {#include}

Une aide pour inclure un composant en tant que ressource non existante dans un modèle.

Cela permet à la ressource d’être personnalisée par programmation plus facilement qu’il n’est possible pour une ressource ajoutée en tant que noeud JCR. Voir [Ajouter ou Inclure un composant](scf.md#add-or-include-a-communities-component)Collectivités.

Seuls quelques composants de communautés sont inclus. Pour AEM 6.1, les [commentaires](essentials-comments.md), l’ [évaluation](rating-basics.md), les [révisions](reviews-basics.md)et le [vote sont inclus.](essentials-voting.md)

Cette aide, appropriée uniquement côté serveur, fournit des fonctionnalités similaires à [cq:include](../../help/sites-developing/taglib.md) pour les scripts JSP.

### Paramètres {#parameters-6}

* **contexte**: Chaîne ou objet

   (Facultatif, sauf si vous fournissez un chemin relatif)

   Utilisez `this` pour transmettre le contexte actuel.

   Utilisez `this.id` pour obtenir la ressource à `id` des fins de rendu du type de ressource demandé.

* **resourceType**: Chaîne

   (Facultatif) Le type de ressource est défini par défaut sur le type de ressource à partir du contexte.

* **modèle**: Chaîne

   Chemin d’accès au script de composant.

* **chemin**: Chaîne

   (Obligatoire) Chemin d’accès à la ressource. Si le chemin est relatif, un contexte doit être fourni, sinon la chaîne vide est renvoyée.

* **authoringDisabled**: Booléen

   (Facultatif) La valeur par défaut est false. usage interne uniquement.

### Exemple {#example-4}

```
{{include this.id path="comments" resourceType="social/commons/components/hbs/comments"}}
```

Ceci inclut un nouveau composant de commentaires sous `this.id` + /commentaires.

## IncludeClientLib {#includeclientlib}

Une aide qui comprend une bibliothèque cliente AEM html, qui peut être un fichier js, un fichier CSS ou une bibliothèque de thèmes. Pour plusieurs inclusions de types différents, par exemple js et css, cette balise doit être utilisée plusieurs fois dans le script Handlebars.

Cette aide, appropriée uniquement côté serveur, fournit des fonctionnalités similaires à [ui:includeClientLib](../../help/sites-developing/taglib.md) pour les scripts JSP.

### Paramètres {#parameters-7}

* ****: Chaîne

   (Facultatif) Un  de de bibliothèque cliente séparée par des virgules. Cela inclut toutes les bibliothèques JavaScript et CSS pour les catégories données. Le nom du thème est extrait de la requête.

* **thème**: Chaîne

   (Facultatif) Un  de de bibliothèque cliente séparée par des virgules. Cela inclut toutes les bibliothèques (CSS et JS) relatives au thème pour les catégories données. Le nom du thème est extrait de la requête.

* **js**: Chaîne

   (Facultatif) Un  de de bibliothèque cliente séparée par des virgules. Cela inclut toutes les bibliothèques JavaScript et CSS pour les catégories données.

* **css**: Chaîne

   (Facultatif) Un  de de bibliothèque cliente séparée par des virgules. Cela inclut toutes les bibliothèques CSS pour les catégories données.

### Exemples {#examples-2}

```
// all: js + theme (theme-js + css)
{{includeClientLib categories="cq.social.hbs.comments, cq.social.hbs.voting"}}

// returns
    <link href="/etc/clientlibs/social/hbs/tally/voting.css" rel="stylesheet" type="text/css">
    <link href="/etc/clientlibs/social/hbs/socialgraph.css" rel="stylesheet" type="text/css">
    <link href="/etc/clientlibs/social/hbs/comments.css" rel="stylesheet" type="text/css">
    <script src="/etc/clientlibs/social/hbs/tally/voting.js" type="text/javascript"></script>
    <script src="/etc/clientlibs/social/hbs/socialgraph.js" type="text/javascript"></script>
    <script src="/etc/clientlibs/social/hbs/comments.js" type="text/javascript"></script>

// only js libs
{{includeClientLib js="cq.social.hbs.comments, cq.social.hbs.voting"}}

// returns
    <script src="/etc/clientlibs/social/hbs/tally/voting.js" type="text/javascript"></script>
    <script src="/etc/clientlibs/social/hbs/socialgraph.js" type="text/javascript"></script>
    <script src="/etc/clientlibs/social/hbs/comments.js" type="text/javascript"></script>

// theme only (theme-js + css)
{{includeClientLib theme="cq.social.hbs.comments, cq.social.hbs.voting"}}

// returns
    <link href="/etc/clientlibs/social/hbs/tally/voting.css" rel="stylesheet" type="text/css">
    <link href="/etc/clientlibs/social/hbs/comments.css" rel="stylesheet" type="text/css">
    <script src="/etc/clientlibs/social/hbs/tally/voting.js" type="text/javascript"></script>
    <script src="/etc/clientlibs/social/hbs/comments.js" type="text/javascript"></script>

// css only
{{includeClientLib css="cq.social.hbs.comments, cq.social.hbs.voting"}}

// returns
    <link href="/etc/clientlibs/social/hbs/tally/voting.css" rel="stylesheet" type="text/css">
    <link href="/etc/clientlibs/social/hbs/socialgraph.css" rel="stylesheet" type="text/css">
    <link href="/etc/clientlibs/social/hbs/comments.css" rel="stylesheet" type="text/css">
```

## Plutôt {#pretty-time}

Une aide pour afficher le temps passé jusqu’à un point de coupure, après lequel un format de date normal est affiché.

Par exemple :

* Il y a 12 heures
* 7 jours auparavant

### Paramètres {#parameters-8}

* **contexte**: Nombre

   Une époque dans le passé à comparer à &quot;maintenant&quot;. Le temps est exprimé sous la forme d’un décalage de valeur en millisecondes par rapport au 1er janvier 1970 (époque).

* **daysCutoff**: Nombre

   Nombre de jours avant de passer à une date réelle. La valeur par défaut est 60.

### Exemple {#example-5}

```
{{pretty-time this.published daysCutoff=7}}

/*
Depending on how long in the past, may return

  "3 minutes ago"

  "3 hours ago"

  "3 days ago"
*/
```

## Xss-html {#xss-html}

Une aide qui code une chaîne source pour le contenu d’élément HTML afin de vous protéger contre le format XSS.

REMARQUE : il ne s’agit pas d’un validateur et ne doit pas être utilisé pour écrire des valeurs d’attribut.

### Paramètres {#parameters-9}

* **contexte**: objet

   Code HTML à coder.

### Exemple {#example-6}

```
<p>{{xss-html forum-ugc}}</p>
```

## Xss-htmlAttr {#xss-htmlattr}

Une aide qui code une chaîne source pour l’écriture dans une valeur d’attribut HTML afin de vous protéger contre le format XSS.

REMARQUE : il ne s’agit pas d’un validateur et ne doit pas être utilisé pour écrire des attributs activables (href, src, gestionnaires de  de).

### Paramètres {#parameters-10}

* **contexte**: Objet

   Code HTML à coder.

### Exemple {#example-7}

```
<div id={{xss-htmlAttr id}} />
```

## Xss-jsString {#xss-jsstring}

Aide qui code une chaîne source pour l’écriture dans le contenu de chaîne JavaScript afin de vous protéger contre le format XSS.

REMARQUE : il ne s’agit pas d’un validateur et ne doit pas être utilisé pour écrire sur du code JavaScript arbitraire.

### Paramètres {#parameters-11}

* **contexte**: Objet

   Code HTML à coder.

### Exemple {#example-8}

```
var input = {{xss-jsString topic-title}}
```

## Xss-validHref {#xss-validhref}

Une aide qui analyse une URL pour l’écriture en tant que valeur d’attribut href ou force HTML afin de vous protéger contre le format XSS.

REMARQUE : cela peut renvoyer une chaîne vide

### Paramètres {#parameters-12}

* **contexte**: Objet

   URL à expurger.

### Exemple {#example-9}

```
<a href="{{xss-validHref url}}">my link</a>
```

## Présentation de base de Handlebars.js {#handlebars-js-basic-overview}

Aperçu rapide des fonctions d’aide de la documentation [](https://handlebarsjs.com/expressions.html)Handlebars.js :

* Un appel d’assistance des barres de main est un identifiant simple (le *nom* de l’assistance), suivi de zéro ou de plusieurs paramètres séparés par des espaces.
* Les paramètres peuvent être un simple objet String, number, booléen ou JSON, ainsi qu’une séquence facultative de paires clé-valeur (arguments de hachage) comme dernier(s) paramètre(s).
* Les clés des arguments de hachage doivent être des identifiants simples.
* Les valeurs dans les arguments de hachage sont des barres de contrôle   : identificateurs simples, chemins ou chaînes.
* Le contexte actuel `this`est toujours accessible aux assistants des barres de main.
* Le contexte peut être une chaîne, un nombre, une valeur booléenne ou un objet de données JSON.
* Il est possible de transmettre un objet imbriqué dans le contexte actuel en tant que contexte, par exemple `this.url` ou `this.id` (voir les exemples suivants d’aides simples et de blocs).

* Les assistants de bloc sont des fonctions qui peuvent être appelées n’importe où dans le modèle. Ils peuvent appeler un bloc du modèle zéro ou plusieurs fois avec un contexte différent à chaque fois. Ils contiennent un contexte entre {{#*name*}} et {{/*name*}.

* Les barres de poignées fournissent un paramètre final aux assistants nommés &quot;options&quot;. L’objet spécial &quot;options&quot; inclut

   * Données privées facultatives (options.data)
   * Propriétés clé-valeur facultatives de l’appel (options.hash)
   * Capacité à s’appeler (options.fn())
   * Possibilité d’appeler l’inverse d’elle-même (options.inverse())

* Il est recommandé que le contenu de la chaîne HTML renvoyé par un assistant soit une chaîne SafeString.

### Exemple d’aide simple de la documentation de Handlebars.js : {#an-example-of-a-simple-helper-from-handlebars-js-documentation}

```
Handlebars.registerHelper('link_to', function(title, options) {
    return new Handlebars.SafeString('<a href="/posts' + this.url + '">' + title + "!</a>");
});

var context = {posts: [
    {url: "/hello-world",
      body: "Hello World!"}
  ] };

// when link_to is called, posts is the current context
var source = '<ul>{{#posts}}<li>{{{link_to "Post"}}}</li>{{/posts}}</ul>'

var template = Handlebars.compile(source);

template(context);
```

Rendu :

&lt;ul>&lt;li>&lt;a href=&quot;/posts/hello-world&quot;>Publier!&lt;/a>&lt;/li>&lt;/ul>

### Exemple d’aide de bloc provenant de la documentation de Handlebars.js : {#an-example-of-a-block-helper-from-handlebars-js-documentation}

```
Handlebars.registerHelper('link', function(options) {
    return new Handlebars.SafeString('<a href="/people/' + this.id + '">' + options.fn(this) + '</a>');
});

var data = { "people": [
  { "name": "Alan", "id": 1 },
  { "name": "Yehuda", "id": 2 }
]};

// when link is called, people is the current context
var source = "<ul>{{#people}}<li>{{#link}}{{name}}{{/link}}</li>{{/people}}</ul>";

var template = Handlebars.compile(source);

template(data);
```

Rendu :
&lt;ul>&lt;li>&lt;a href=&quot;/people/1&quot;>Alan&lt;/a>&lt;/li>&lt;li>&lt;a href=&quot;/people/2&quot;>Yehuda&lt;/a>&lt;/li>&lt;/ul>

## Aide SCF personnalisée {#custom-scf-helpers}

Les assistants personnalisés doivent être implémentés côté serveur ainsi que côté client, en particulier lors du transfert de données. Pour SCF, la plupart des modèles sont compilés et rendus côté serveur, car le serveur génère le code HTML pour un composant donné lorsque la page est demandée.

### Aide personnalisée côté serveur {#server-side-custom-helpers}

Pour mettre en oeuvre et enregistrer un assistant SCF personnalisé côté serveur, il vous suffit de mettre en oeuvre l’interface Java [TemplateHelper](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/handlebars/api/TemplateHelper.html), d’en faire un service [](../../help/sites-developing/the-basics.md#osgi) OSGi et de l’installer dans le cadre d’un lot OSGi.

Par exemple :

### FooTextHelper.java {#footexthelper-java}

```java
/** Custom Handlebars Helper */

package com.my.helpers;

import java.io.IOException;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;

import com.adobe.cq.social.handlebars.api.TemplateHelper;
import com.github.jknack.handlebars.Options;

@Service
@Component
public class FooTextHelper implements TemplateHelper<String>{

    @Override
    public CharSequence apply(String context, Options options) throws IOException {
        return "foo-" + context;
    }

    @Override
    public String getHelperName() {
        return "foo-text";
    }

    @Override
    public Class<String> getContextType() {
        return String.class;
    }
}
```

>[!NOTE]
>
>Un assistant créé pour le serveur doit également être créé pour le client.
>
>Le composant est rendu de nouveau côté client pour l’utilisateur connecté. Si l’assistance côté client est introuvable, le composant disparaît.


### Assistance personnalisée côté client {#client-side-custom-helpers}

Les assistants côté client sont des scripts Handlebars enregistrés en appelant `Handlebars.registerHelper()`.
Par exemple :

### custom-helpers.js {#custom-helpers-js}

```
function(Handlebars, SCF, $CQ) {

    Handlebars.registerHelper('foo-text', function(context, options) {
        if (!context) {
            return "";
        }
        return "foo-" + context;
    });

})(Handlebars, SCF, $CQ);
```

Les assistants personnalisés côté client doivent être ajoutés à une bibliothèque cliente personnalisée.
clientlib doit :

* Incluez une dépendance sur `cq.social.scf`.
* Charger après le chargement des barres de contrôle.
* Soyez [inclus](clientlibs.md).

Remarque : les aides SCF sont définies dans `/etc/clientlibs/social/commons/scf/helpers.js`.

| **[⇐ Fonctionnalités Essentials](essentials.md)** | **[Personnalisation côté serveur](server-customize.md)** |
|---|---|
|  | **[Personnalisation côté client](client-customize.md)** |

