---
title: Aide-mémoire SCF
seo-title: Aide-mémoire SCF
description: Handlebars Méthodes d'assistance pour faciliter le travail avec SCF
seo-description: Handlebars Méthodes d'assistance pour faciliter le travail avec SCF
uuid: 9c514199-871e-4b68-8147-2052d2eeda15
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 8b6c1697-d693-41f4-8337-f41658465107
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '1534'
ht-degree: 9%

---


# Aide des barres de poignées SCF {#scf-handlebars-helpers}

| **[⇐ Fonctionnalités Essentials](essentials.md)** | **[Personnalisation côté serveur](server-customize.md)** |
|---|---|
|  | **[Personnalisation côté client](client-customize.md)** |

Handlebars Les aides (aides) sont des méthodes que l&#39;on peut appeler à partir des scripts Handlebars pour faciliter l&#39;utilisation des composants SCF.

L’implémentation comprend une définition côté client et côté serveur. Il est également possible pour les développeurs de créer des assistants personnalisés.

Les assistants SCF personnalisés fournis avec AEM Communities sont définis dans la bibliothèque client [client](../../help/sites-developing/clientlibs.md) :

* `/etc/clientlibs/social/commons/scf/helpers.js`

>[!NOTE]
>
>Veillez à installer le [dernier pack de fonctionnalités Communautés](deploy-communities.md#latestfeaturepack).

## Abrévier {#abbreviate}

Aide à renvoyer une chaîne abrégée conforme aux propriétés maxWords et maxLength.

La chaîne à abréger est fournie comme contexte. Si aucun contexte n’est fourni, une chaîne vide est renvoyée.

Tout d’abord, le contexte est ajusté à maxLength, puis il est divisé en mots et réduit à maxWords.

Si safeString est défini sur true, la chaîne renvoyée est une SafeString.

### Paramètres {#parameters}

* **contexte** : Chaîne

   (Facultatif) La valeur par défaut est la chaîne vide.

* **maxLength** : Nombre

   (Facultatif) La valeur par défaut est la longueur du contexte.

* **maxWords** : Nombre

   (Facultatif) La valeur par défaut est le nombre de mots contenus dans la chaîne rognée.

* **safeString** : Boolean

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

Aide permettant d’ajouter deux plages sous une balise div, l’une pour le texte complet et l’autre pour le texte plus petit, avec la possibilité de basculer entre les deux vues.

### Paramètres {#parameters-1}

* **contexte** : Chaîne

   (Facultatif) La valeur par défaut est la chaîne vide.

* **numChars** : Nombre

   (Facultatif) Nombre de caractères à afficher lorsque le texte intégral n’est pas affiché. La valeur par défaut est 100.

* **moreText** : Chaîne

   (Facultatif) Texte à afficher indiquant qu’il y a plus de texte à afficher. La valeur par défaut est &quot;plus&quot;.

* **ellipsesText** : Chaîne

   (Facultatif) Texte à afficher indiquant qu’il existe du texte masqué. La valeur par défaut est &quot;...&quot;.

* **safeString** : Boolean

   (Facultatif) Valeur booléenne indiquant si Handlebars.SafeString() doit être appliqué avant de renvoyer le résultat. La valeur par défaut est false.

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

* **contexte** : Nombre

   (Facultatif) décalage de la valeur en millisecondes par rapport au 1er janvier 1970 (époque). La date par défaut est la date actuelle.

* **format** : Chaîne

   (Facultatif) Format de date à appliquer. La valeur par défaut est &quot;AAAA-MM-DTHH:mm:ss.sssZ&quot; et le résultat est &quot;2015-03-18T18:17:13-07:00&quot;.

### Exemples {#examples-1}

```
{{dateUtil this.memberSince format="dd MMM yyyy, hh:mm"}}

// returns "18 Mar 2015, 18:17"
```

```
{{dateUtil this.birthday format="MM-DD-YYYY"}}

// returns "03-18-2015"
```

## Est égal à {#equals}

Aide permettant de renvoyer du contenu selon une condition d’égalité.

### Paramètres {#parameters-3}

* **lvalue** : Chaîne

   Valeur de gauche à comparer.

* **rvalue** : Chaîne

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

Aide de bloc qui teste la valeur actuelle de [mode WCM](https://helpx.adobe.com/fr/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html) par rapport à une liste de modes séparée par des chaînes.

### Paramètres {#parameters-4}

* **contexte** : Chaîne

   (Facultatif) Chaîne à traduire. Obligatoire si aucune valeur par défaut n’est fournie.

* **mode** : Chaîne

   (Facultatif) liste séparée par des virgules de [modes WCM](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html) à tester si elle est définie.

### Exemple {#example-2}

```xml
{{#if-wcm-mode mode="DESIGN, EDIT"}}
 ...
{{else}}
 ...
{{/if-wcm-mode}}
```

## i18n {#i-n}

Cette aide remplace l&#39;aide Handlebars &quot;i18n&quot;.

Voir aussi [Internationalizing Strings in JavaScript Code](../../help/sites-developing/i18n-dev.md#internationalizing-strings-in-javascript-code).

### Paramètres {#parameters-5}

* **contexte** : Chaîne

   (Facultatif) Chaîne à traduire. Obligatoire si aucune valeur par défaut n’est fournie.

* **par défaut** : Chaîne

   (Facultatif) Chaîne par défaut à traduire. Obligatoire si aucun contexte n’est fourni.

* **commentaire** : Chaîne

   (Facultatif) Conseils de traduction

### Exemple {#example-3}

```
{{i18n "hello"}}
{{i18n "hello" comment="greeting" default="bonjour"}}
```

## Inclure {#include}

Aide permettant d’inclure un composant en tant que ressource non existante dans un modèle.

Cela permet à la ressource d’être personnalisée par programmation plus facilement qu’il n’est possible pour une ressource ajoutée en tant que noeud JCR. Voir [Ajouter ou inclure un composant Collectivités](scf.md#add-or-include-a-communities-component).

Seuls quelques composants de communautés sélectionnés sont inclus. Pour l&#39;AEM 6.1, ceux qui peuvent être inclus sont [commentaires](essentials-comments.md), [évaluation](rating-basics.md), [révisions](reviews-basics.md) et [vote](essentials-voting.md).

Cette assistance, qui s’applique uniquement côté serveur, fournit des fonctionnalités similaires à [cq:include](../../help/sites-developing/taglib.md) pour les scripts JSP.

### Paramètres {#parameters-6}

* **contexte** : Chaîne ou objet

   (Facultatif, sauf si vous fournissez un chemin relatif)

   Utilisez `this` pour transmettre le contexte actuel.

   Utilisez `this.id` pour obtenir la ressource à `id` pour effectuer le rendu du type de ressource demandé.

* **resourceType** : Chaîne

   (Facultatif) Le type de ressource est défini par défaut sur le type de ressource du contexte.

* **modèle** : Chaîne

   Chemin d’accès au script de composant.

* **chemin** : Chaîne

   (Obligatoire) Chemin d&#39;accès à la ressource. Si le chemin d’accès est relatif, un contexte doit être fourni, sinon la chaîne vide est renvoyée.

* **authoringDisabled** : Boolean

   (Facultatif) La valeur par défaut est false. usage interne uniquement.

### Exemple {#example-4}

```
{{include this.id path="comments" resourceType="social/commons/components/hbs/comments"}}
```

Cela inclura un nouveau composant de commentaires à `this.id` + /commentaires.

## IncludeClientLib {#includeclientlib}

Aide qui comprend une bibliothèque cliente html AEM, qui peut être un js, un CSS ou une bibliothèque de thèmes. Pour plusieurs inclusions de types différents, par exemple js et css, cette balise doit être utilisée plusieurs fois dans le script Handlebars.

Cette assistance, qui s’applique uniquement côté serveur, fournit des fonctionnalités similaires à [ui:includeClientLib](../../help/sites-developing/taglib.md) pour les scripts JSP.

### Paramètres {#parameters-7}

* **catégories** : Chaîne

   (Facultatif) liste de catégories de lib client séparées par des virgules. Cela inclut toutes les bibliothèques JavaScript et CSS pour les catégories données. Le nom du thème est extrait de la requête.

* **thème** : Chaîne

   (Facultatif) liste de catégories de lib client séparées par des virgules. Cela inclut toutes les bibliothèques (CSS et JS) relatives au thème pour les catégories données. Le nom du thème est extrait de la requête.

* **js** : Chaîne

   (Facultatif) liste de catégories de lib client séparées par des virgules. Cela inclut toutes les bibliothèques JavaScript et CSS pour les catégories données.

* **css** : Chaîne

   (Facultatif) liste de catégories de lib client séparées par des virgules. Cela inclut toutes les bibliothèques CSS pour les catégories données.

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

## Relty time {#pretty-time}

Aide permettant d’afficher le temps passé jusqu’à un point de coupure, après lequel un format de date standard est affiché.

Par exemple :

* Il y a 12 heures
* il y a 7 jours

### Paramètres {#parameters-8}

* **contexte** : Nombre

   Une époque dans le passé à comparer à &#39;maintenant&#39;. Le temps est exprimé sous la forme d&#39;un décalage de la valeur en millisecondes par rapport au 1er janvier 1970 (époque).

* **daysCutoff** : Nombre

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

Aide qui code une chaîne source pour le contenu d’élément HTML afin de vous protéger contre le format XSS.

REMARQUE : il ne s’agit pas d’un validateur et ne doit pas être utilisé pour écrire des valeurs d’attribut.

### Paramètres {#parameters-9}

* **contexte** : objet

   Code HTML à coder.

### Exemple {#example-6}

```
<p>{{xss-html forum-ugc}}</p>
```

## Xss-htmlAttr {#xss-htmlattr}

Aide qui code une chaîne source à des fins d’écriture sur une valeur d’attribut HTML afin de vous aider à vous protéger contre le format XSS.

REMARQUE : il ne s&#39;agit pas d&#39;un validateur et ne doit pas être utilisé pour écrire des attributs activables (href, src, gestionnaires de événements).

### Paramètres {#parameters-10}

* **contexte** : Objet

   Code HTML à coder.

### Exemple {#example-7}

```
<div id={{xss-htmlAttr id}} />
```

## Xss-jsString {#xss-jsstring}

Aide qui code une chaîne source pour l’écriture de contenu de chaîne JavaScript afin de vous protéger contre le format XSS.

REMARQUE : ce n&#39;est pas un validateur et ne doit pas être utilisé pour écrire sur JavaScript arbitraire.

### Paramètres {#parameters-11}

* **contexte** : Objet

   Code HTML à coder.

### Exemple {#example-8}

```
var input = {{xss-jsString topic-title}}
```

## Xss-validHref {#xss-validhref}

Aide qui analyse une URL pour l’écriture en tant que valeur d’attribut href ou d’attribut de ressource HTML afin de vous aider à vous protéger contre le format XSS.

REMARQUE : cela peut renvoyer une chaîne vide

### Paramètres {#parameters-12}

* **contexte** : Objet

   URL à expurger.

### Exemple {#example-9}

```
<a href="{{xss-validHref url}}">my link</a>
```

## Handlebars.js Présentation de base {#handlebars-js-basic-overview}

Aperçu rapide des fonctions d’aide de [la documentation de Handlebars.js](https://handlebarsjs.com/expressions.html) :

* Un appel Handlebars helper est un identifiant simple (le *nom* de l&#39;aide), suivi de zéro ou de plusieurs paramètres séparés par des espaces.
* Les paramètres peuvent être un simple objet String, number, booléen ou JSON, ainsi qu’une séquence facultative de paires clé-valeur (arguments de hachage) en tant que dernier paramètre.
* Les clés des arguments de hachage doivent être des identifiants simples.
* Les valeurs des arguments de hachage sont les expressions des barres de contrôle : identificateurs simples, chemins ou chaînes.
* Le contexte actuel, `this`, est toujours disponible pour les assistants Handlebars.
* Le contexte peut être une chaîne, un nombre, une valeur booléenne ou un objet de données JSON.
* Il est possible de transmettre un objet imbriqué dans le contexte actuel en tant que contexte, tel que `this.url` ou `this.id` (voir les exemples suivants d&#39;aides simples et de blocs).

* Les assistants de bloc sont des fonctions qui peuvent être appelées n’importe où dans le modèle. Ils peuvent appeler un bloc du modèle zéro ou plusieurs fois avec un contexte différent à chaque fois. Ils contiennent un contexte entre {{#*name*}} et {{/*name*}.

* Handlebars fournit un paramètre final aux assistants nommés &quot;options&quot;. L&#39;objet spécial &quot;options&quot; inclut

   * Données privées facultatives (options.data)
   * Propriétés de clé-valeur facultatives de l’appel (options.hash)
   * Capacité à s’appeler (options.fn())
   * Possibilité d’appeler l’inverse d’elle-même (options.inverse())

* Il est recommandé que le contenu de la chaîne HTML renvoyé par un assistant soit une chaîne de sécurité.

### Exemple d’aide simple de la documentation Handlebars.js : {#an-example-of-a-simple-helper-from-handlebars-js-documentation}

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

&lt;ul>
&lt;li>&lt;a href=&quot;/posts/hello-world&quot;>Publiez !&lt;/a>&lt;/li>
&lt;/ul>

### Exemple d’aide de bloc provenant de la documentation Handlebars.js : {#an-example-of-a-block-helper-from-handlebars-js-documentation}

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
&lt;ul>
&lt;li>&lt;a href=&quot;/people/1&quot;>Alan&lt;/a>&lt;/li>
&lt;li>&lt;a href=&quot;/people/2&quot;>Yehuda&lt;/a>&lt;/li>
&lt;/ul>

## Aide SCF personnalisée {#custom-scf-helpers}

Les assistants personnalisés doivent être implémentés tant côté serveur que côté client, en particulier lors de la transmission de données. Pour SCF, la plupart des modèles sont compilés et rendus côté serveur, car le serveur génère le code HTML pour un composant donné lorsque la page est demandée.

### Assistance personnalisée côté serveur {#server-side-custom-helpers}

Pour mettre en oeuvre et enregistrer un assistant SCF personnalisé côté serveur, il vous suffit de mettre en oeuvre l&#39;interface Java [TemplateHelper](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/handlebars/api/TemplateHelper.html), de le transformer en service [OSGi](../../help/sites-developing/the-basics.md#osgi) et de l&#39;installer dans le cadre d&#39;un lot OSGi.

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
>Un assistant créé côté serveur doit également être créé côté client.
>
>Le composant est rendu de nouveau côté client pour l’utilisateur connecté et si l’assistance côté client est introuvable, le composant disparaît.

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
* Charger après le chargement des barres de main.
* Soyez [inclus](clientlibs.md).

Remarque : les assistants SCF sont définis dans `/etc/clientlibs/social/commons/scf/helpers.js`.

| **[⇐ Fonctionnalités Essentials](essentials.md)** | **[Personnalisation côté serveur](server-customize.md)** |
|---|---|
|  | **[Personnalisation côté client](client-customize.md)** |

