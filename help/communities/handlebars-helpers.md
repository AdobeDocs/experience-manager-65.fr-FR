---
title: Assistants Handlebars SCF
description: Méthodes d’assistance Handlebars pour faciliter le travail avec SCF
topic-tags: developing
content-type: reference
exl-id: bfb95cae-4b0f-4521-a113-042dc4005a63
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1531'
ht-degree: 5%

---

# Assistants Handlebars SCF {#scf-handlebars-helpers}

| ⇐ Feature Essentials [&#128279;](essentials.md)**&#x200B;**|[&#x200B;  ⇒ de personnalisation côté serveur &#x200B;](server-customize.md)**&#x200B;** |
|---|---|
|   | ⇒ de personnalisation côté client [&#128279;](client-customize.md)**&#x200B;** |

Les assistants Handlebars (helpers) sont des méthodes appelables à partir des scripts Handlebars pour faciliter l’utilisation des composants SCF.

L’implémentation comprend une définition côté client et côté serveur. Il est également possible pour les développeurs de créer des assistants personnalisés.

Les assistants SCF personnalisés fournis avec AEM Communities sont définis dans la [bibliothèque cliente](../../help/sites-developing/clientlibs.md) :

* `/etc/clientlibs/social/commons/scf/helpers.js`

>[!NOTE]
>
>Veillez à installer le [dernier pack de fonctionnalités Communities](deploy-communities.md#latestfeaturepack).

## Abréger {#abbreviate}

Helper permettant de renvoyer une chaîne abrégée conforme aux propriétés maxWords et maxLength.

La chaîne à abréger est fournie en tant que contexte. Si aucun contexte n’est fourni, une chaîne vide est renvoyée.

Tout d’abord, le contexte est réduit à maxLength, puis il est découpé en mots et réduit à maxWords.

Si safeString est défini sur true, la chaîne renvoyée est une chaîne SafeString.

### Paramètres {#parameters}

* **context** : chaîne

  (Facultatif) La valeur par défaut est la chaîne vide

* **maxLength** : nombre

  (Facultatif) La valeur par défaut est la longueur du contexte.

* **maxWords** : Nombre

  (Facultatif) La valeur par défaut est le nombre de mots dans la chaîne tronquée.

* **safeString** : booléen

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

Un helper permettant d’ajouter deux plages sous une balise &lt;div>, l’une pour le texte complet et l’autre pour le texte inférieur, avec la possibilité de basculer entre les deux vues.

### Paramètres {#parameters-1}

* **context** : chaîne

  (Facultatif) La valeur par défaut est la chaîne vide.

* **numChars** : nombre

  (Facultatif) Nombre de caractères à afficher en cas d’affichage de texte intégral. La valeur par défaut est 100.

* **moreText** : chaîne

  (Facultatif) Texte à afficher pour indiquer qu’il reste du texte à afficher. La valeur par défaut est « plus ».

* **ellipsesText** : chaîne

  (Facultatif) Texte à afficher pour signaler la présence de texte masqué. La valeur par défaut est « ... ».

* **safeString** : booléen

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

Helper permettant de renvoyer une chaîne de date formatée.

### Paramètres {#parameters-2}

* **context** : nombre

  (Facultatif) Valeur en millisecondes décalée par rapport au 1er janvier 1970 (époque). La valeur par défaut est la date actuelle.

* **format** : chaîne

  (Facultatif) Format de date à appliquer. La valeur par défaut est « `YYYY-MM-DDTHH:mm:ss.sssZ` » et le résultat apparaît comme « `2015-03-18T18:17:13-07:00` »

### Exemples {#examples-1}

```
{{dateUtil this.memberSince format="dd MMM yyyy, hh:mm"}}

// returns "18 Mar 2015, 18:17"
```

```
{{dateUtil this.birthday format="MM-DD-YYYY"}}

// returns "03-18-2015"
```

## Égal {#equals}

Helper permettant de renvoyer du contenu en fonction d’une condition d’égalité.

### Paramètres {#parameters-3}

* **lvalue** : chaîne

  Valeur de gauche à comparer.

* **rvalue** : chaîne

  Valeur de droite à comparer.

### Exemple {#example-1}

```
{{#equals  value "some-value"}}
  <div>They are EQUAL!</div>
`{{else}}`
  <div>They are NOT equal!</div>
{{/equals}}
```

## If-wcm-mode {#if-wcm-mode}

Assistant de bloc qui teste la valeur actuelle du [mode de gestion de contenu web](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/WCMMode.html) par rapport à une liste de modes séparés par une chaîne.

### Paramètres {#parameters-4}

* **context** : chaîne

  (Facultatif) Chaîne à traduire. Obligatoire si aucune valeur par défaut n’est fournie.

* **mode** : chaîne

  (Facultatif) Liste séparée par des virgules de [modes de gestion de contenu web](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/WCMMode.html) à tester si elle est définie.

### Exemple {#example-2}

```xml
{{#if-wcm-mode mode="DESIGN, EDIT"}}
 ...
{else}}
 ...
`{{/if-wcm-mode}}`
```

## i18n {#i-n}

Cet helper remplace l&#39;helper Handlebars &#39;i18n&#39;.

Voir aussi [Internationalisation de chaînes dans le code JavaScript](../../help/sites-developing/i18n-dev.md#internationalizing-strings-in-javascript-code).

### Paramètres {#parameters-5}

* **context** : chaîne

  (Facultatif) Chaîne à traduire. Obligatoire si aucune valeur par défaut n’est fournie.

* **default** : chaîne

  (Facultatif) Chaîne par défaut à traduire. Obligatoire si aucun contexte n’est fourni.

* **comment** : chaîne

  (Facultatif) Astuce de traduction

### Exemple {#example-3}

```
{{i18n "hello"}}
{{i18n "hello" comment="greeting" default="bonjour"}}
```

## Inclure {#include}

Helper permettant d’inclure un composant en tant que ressource non existante dans un modèle.

Cette méthode permet de personnaliser plus facilement la ressource par programmation que pour une ressource ajoutée en tant que nœud JCR. Voir [Ajouter ou inclure un composant de communautés](scf.md#add-or-include-a-communities-component).

Seuls quelques composants sélectionnés de Communities sont disponibles. <!-- OBSOLETE/OLD  NEED TO UPDATE FOR 6.5  For AEM 6.1, those that are includable are [comments](essentials-comments.md), [rating](rating-basics.md), [reviews](reviews-basics.md), and [voting](essentials-voting.md). -->

Cet helper, approprié uniquement du côté serveur, fournit des fonctionnalités similaires à [cq:include](../../help/sites-developing/taglib.md) pour les scripts JSP.

### Paramètres {#parameters-6}

* **context** : chaîne ou objet

  (Facultatif, sauf si vous fournissez un chemin relatif)

  Utilisez `this` pour transmettre le contexte actif.

  Utilisez `this.id` pour obtenir la ressource à l’`id` afin d’effectuer le rendu de resourceType demandé.

* **resourceType** : chaîne

  (Facultatif) Le type de ressource est défini par défaut sur Type de ressource provenant du contexte.

* **template** : chaîne

  Chemin d’accès au script du composant.

* **path** : chaîne

  (Obligatoire) Chemin d’accès à la ressource. Si le chemin est relatif, un contexte doit être fourni, sinon la chaîne vide est renvoyée.

* **authoringDisabled** : booléen

  (Facultatif) La valeur par défaut est false. Pour usage interne uniquement.

### Exemple {#example-4}

```
{{include this.id path="comments" resourceType="social/commons/components/hbs/comments"}}
```

Inclut un nouveau composant de commentaires sous `this.id` + /comments.

## IncludeClientLib {#includeclientlib}

Un helper qui inclut une bibliothèque cliente HTML AEM, qui peut être de type js, css ou theme. Pour plusieurs inclusions de types différents (js et css, par exemple), cette balise doit être utilisée plusieurs fois dans le script Handlebars.

Cet helper, approprié uniquement du côté serveur, fournit des fonctionnalités similaires à [ui:includeClientLib](../../help/sites-developing/taglib.md) pour les scripts JSP.

### Paramètres {#parameters-7}

* **categories** : chaîne

  (Facultatif) Liste de catégories de bibliothèques clientes séparées par des virgules. Incluez toutes les bibliothèques JavaScript et CSS pour les catégories données. Le nom du thème est extrait de la requête.

* **theme** : String

  (Facultatif) Liste de catégories de bibliothèques clientes séparées par des virgules. Incluez toutes les bibliothèques liées au thème (à la fois CSS et JS) pour les catégories données. Le nom du thème est extrait de la requête.

* **js** : chaîne

  (Facultatif) Liste de catégories de bibliothèques clientes séparées par des virgules. Inclut toutes les bibliothèques JavaScript pour les catégories données.

* **css** : chaîne

  (Facultatif) Liste de catégories de bibliothèques clientes séparées par des virgules. Inclut toutes les bibliothèques CSS pour les catégories données.

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

## Joli {#pretty-time}

Un helper permettant d’afficher le temps écoulé jusqu’à un point limite, après quoi un format de date normal est affiché.

Par exemple :

* Il y a 12 heures
* il y a 7 jours

### Paramètres {#parameters-8}

* **context** : nombre

  Une époque révolue pour comparer avec &#39;maintenant&#39;. Le temps est exprimé en décalage de valeur en millisecondes par rapport au 1er janvier 1970 (époque).

* **daysCutoff** : nombre

  Nombre de jours écoulés avant le passage à une date réelle. La valeur par défaut est 60.

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

Helper qui code une chaîne source pour le contenu de l’élément HTML afin de vous protéger contre XSS.

REMARQUE : cet helper n’est pas un programme de validation et ne doit pas être utilisé pour écrire des valeurs d’attribut.

### Paramètres {#parameters-9}

* **context**: objet

  HTML à coder.

### Exemple {#example-6}

```
<p>{{xss-html forum-ugc}}</p>
```

## Xss-htmlAttr {#xss-htmlattr}

Helper qui code une chaîne source pour l’écriture d’une valeur d’attribut HTML afin de se protéger contre XSS.

REMARQUE : cet helper n’est pas un programme de validation et ne doit pas être utilisé pour écrire des attributs exploitables (href, src, gestionnaires d’événements).

### Paramètres {#parameters-10}

* **context** : objet

  HTML à coder.

### Exemple {#example-7}

```
<div id={{xss-htmlAttr id}} />
```

## Xss-jsString {#xss-jsstring}

Helper qui code une chaîne source pour écrire du contenu de chaîne JavaScript afin de se protéger contre XSS.

REMARQUE : cet helper n’est pas un programme de validation et ne doit pas être utilisé pour écrire dans un JavaScript arbitraire.

### Paramètres {#parameters-11}

* **context** : objet

  HTML à coder.

### Exemple {#example-8}

```
var input = {{xss-jsString topic-title}}
```

## Xss-validHref {#xss-validhref}

Helper qui assainit une URL pour l’écriture en tant que valeur d’attribut href ou source HTML afin de se protéger contre XSS.

REMARQUE : cet helper peut renvoyer une chaîne vide.

### Paramètres {#parameters-12}

* **context** : objet

  URL à assainir.

### Exemple {#example-9}

```
<a href="{{xss-validHref url}}">my link</a>
```

## Présentation de base de Handlebars.js {#handlebars-js-basic-overview}

* Un appel d’assistance Handlebars est un identifiant simple (le *nom* de l’assistant), suivi de zéro ou de plusieurs paramètres séparés par des espaces.
* Les paramètres peuvent être une simple chaîne, un nombre, une valeur booléenne ou un objet JSON, et une séquence facultative de paires clé-valeur (arguments de hachage) comme derniers paramètres.
* Les clés des arguments de hachage doivent être de simples identifiants.
* Les valeurs des arguments de hachage sont des expressions Handlebars : identifiants simples, chemins ou chaînes.
* Le contexte actuel, `this`, est toujours disponible pour les assistants Handlebars.
* Le contexte peut être une chaîne, un nombre, une valeur booléenne ou un objet de données JSON.
* Il est possible de transmettre un objet imbriqué dans le contexte actif comme contexte, par exemple `this.url` ou `this.id` (voir les exemples suivants d’assistants simples et de blocs).

* Les assistants de bloc sont des fonctions qui peuvent être appelées depuis n’importe où dans le modèle. Ils peuvent appeler un bloc du modèle zéro ou plusieurs fois avec un contexte différent à chaque fois. Ils contiennent un contexte entre `{{#*name*}}` et `{{/*name*}}`.

* Les barres de contrôle fournissent un paramètre final aux assistants nommés « options ». L&#39;objet spécial &#39;options&#39; comprend

   * Données privées facultatives (options.data)
   * Propriétés clé-valeur facultatives de l’appel (options.hash)
   * Possibilité d’appeler elle-même (options.fn())
   * Possibilité d’appeler l’inverse de lui-même (options.inverse())

* Il est recommandé que le contenu de chaîne HTML renvoyé par un helper soit une chaîne SafeString.

### Exemple d’assistant simple de la documentation Handlebars.js : {#an-example-of-a-simple-helper-from-handlebars-js-documentation}

```
Handlebars.registerHelper('link_to', function(title, options) {
    return new Handlebars.SafeString('<a href="/posts' + this.url + '">' + title + "!</a>");
});

var context = {posts: [
    {url: "/hello-world",
      body: "Hello World!"}
  ] };

// when link_to is called, posts is the current context
var source = '<ul>`{{#posts}}`<li>{{{link_to "Post"}}}</li>`{{/posts}}`</ul>'

var template = Handlebars.compile(source);

template(context);
```

Effectuerait le rendu :

&lt;ul>
&lt;li>&lt;a href=« /posts/hello-world »>Publication !&lt;/a>&lt;/li>
&lt;/ul>

### Exemple d’assistant de bloc de la documentation Handlebars.js : {#an-example-of-a-block-helper-from-handlebars-js-documentation}

```
Handlebars.registerHelper('link', function(options) {
    return new Handlebars.SafeString('<a href="/people/' + this.id + '">' + options.fn(this) + '</a>');
});

var data = { "people": [
  { "name": "Alan", "id": 1 },
  { "name": "Yehuda", "id": 2 }
]};

// when link is called, people is the current context
var source = "<ul>`{{#people}}`<li>`{{#link}}``{{name}}``{{/link}}`</li>`{{/people}}`</ul>";

var template = Handlebars.compile(source);

template(data);
```

Effectuerait le rendu :
&lt;ul>
&lt;li>&lt;a href=« /people/1 »>Alan&lt;/a>&lt;/li>
&lt;li>&lt;a href=« /people/2 »>Yehuda&lt;/a>&lt;/li>
&lt;/ul>

## Assistants SCF personnalisés {#custom-scf-helpers}

Les assistants personnalisés doivent être implémentés côté serveur et côté client, en particulier lors de la transmission de données. Pour SCF, la plupart des modèles sont compilés et rendus côté serveur, car le serveur génère l’HTML pour un composant donné lorsque la page est demandée.

### Assistants personnalisés côté serveur {#server-side-custom-helpers}

Pour implémenter et enregistrer un assistant SCF personnalisé côté serveur, il vous suffit d’implémenter l’interface Java™ [TemplateHelper](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/handlebars/api/TemplateHelper.html), d’en faire un [service OSGi](../../help/sites-developing/the-basics.md#osgi) et de l’installer dans le cadre d’un lot OSGi.

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
>Un helper créé pour le côté serveur doit également être créé pour le côté client.
>
>Le composant est rendu de nouveau côté client pour l’utilisateur ou l’utilisatrice connecté(e), et si l’assistant côté client est introuvable, le composant disparaît.

### Assistants personnalisés côté client {#client-side-custom-helpers}

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

Les assistants côté client personnalisés doivent être ajoutés à une bibliothèque cliente personnalisée.
La bibliothèque cliente doit :

* Incluez une dépendance sur `cq.social.scf`.
* Charger après le chargement de Handlebars.
* Soyez [&#x200B; inclus &#x200B;](clientlibs.md).

Remarque : les assistants SCF sont définis dans `/etc/clientlibs/social/commons/scf/helpers.js`.

| ⇐ Feature Essentials [&#128279;](essentials.md)**&#x200B;**|[&#x200B;  ⇒ de personnalisation côté serveur &#x200B;](server-customize.md)**&#x200B;** |
|---|---|
|   | ⇒ de personnalisation côté client [&#128279;](client-customize.md)**&#x200B;** |
