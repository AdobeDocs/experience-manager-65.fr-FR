---
title: Internationaliser des chaînes d’interface utilisateur
description: Les API Java&trade et JavaScript vous permettent d’internationaliser des chaînes.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
exl-id: bc5b1cb7-a011-42fe-8759-3c7ee3068aad
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1091'
ht-degree: 36%

---

# Internationaliser des chaînes d’interface utilisateur {#internationalizing-ui-strings}

Les API Java™ et JavaScript vous permettent d’internationaliser des chaînes dans les types de ressources suivants :

* Fichiers source Java™.
* Scripts JSP.
* JavaScript dans les bibliothèques côté client ou dans la source de la page.
* Valeurs des propriétés de noeud JCR utilisées dans les propriétés de configuration des boîtes de dialogue et des composants.

Pour un aperçu du processus d’internationalisation et de localisation, voir [Internationalisation des composants](/help/sites-developing/i18n.md).

## Internationalisation de chaînes dans le code Java™ et JSP {#internationalizing-strings-in-java-and-jsp-code}

La variable `com.day.cq.i18n` Le package Java™ vous permet d’afficher les chaînes localisées dans votre interface utilisateur. La variable `I18n` fournit la classe `get` qui récupère les chaînes localisées du dictionnaire Adobe Experience Manager (AEM). Le seul paramètre requis de la méthode `get` est le littéral de chaîne en langue anglaise. L’anglais est la langue par défaut de l’interface utilisateur. L’exemple suivant localise le mot `Search` :

`i18n.get("Search");`

L’identification de la chaîne en anglais diffère des structures d’internationalisation standard où un identifiant identifie une chaîne et est utilisé pour référencer la chaîne au moment de l’exécution. L’utilisation du littéral de chaîne anglais offre les avantages suivants :

* Le code est facile à comprendre.
* La chaîne dans la langue par défaut est toujours disponible.

### Définition de la langue de l’utilisateur {#determining-the-user-s-language}

Il existe deux manières de déterminer la langue préférée par l’utilisateur :

* Pour les utilisateurs authentifiés, déterminez la langue à partir des préférences du compte d’utilisateur.
* Paramètre régional de la page demandée.

La propriété language du compte utilisateur est la méthode préférée, car elle est plus fiable. Cependant, l’utilisateur doit être connecté pour utiliser cette méthode.

#### Création de l’objet Java™ I18n {#creating-the-i-n-java-object}

La classe I18n fournit deux constructeurs. La manière dont vous déterminez la langue préférée de l’utilisateur détermine le constructeur à utiliser.

Pour afficher la chaîne dans la langue spécifiée dans le compte d’utilisateur, utilisez le constructeur suivant (après avoir importé `com.day.cq.i18n.I18n)` :

```java
I18n i18n = new I18n(slingRequest);
```

Le constructeur utilise l’objet `SlingHTTPRequest` pour récupérer le paramètre de langue de l’utilisateur.

Pour utiliser les paramètres régionaux de la page afin de déterminer la langue, obtenez d’abord le ResourceBundle pour la langue de la page demandée :

```java
Locale pageLang = currentPage.getLanguage(false);
ResourceBundle resourceBundle = slingRequest.getResourceBundle(pageLang);
I18n i18n = new I18n(resourceBundle);
```

#### Internationalisation d’une chaîne {#internationalizing-a-string}

Utilisez la méthode `get` de l’objet `I18n` pour internationaliser une chaîne. Le seul paramètre requis de la méthode `get` est la chaîne à internationaliser. La chaîne correspond à une chaîne dans un dictionnaire de traducteur. La méthode get recherche la chaîne dans le dictionnaire et renvoie la traduction de la langue actuelle.

Le premier argument de la méthode `get` doit respecter les règles suivantes :

* La valeur doit être un littéral de chaîne. Une variable de type `String` n’est pas acceptable.
* Le littéral de chaîne doit être exprimé sur une seule ligne.
* La chaîne respecte la casse.

```xml
i18n.get("Enter a search keyword");
```

#### Utilisation des conseils de traduction {#using-translation-hints}

Spécifiez l’[indice de traduction](/help/sites-developing/i18n-translator.md#adding-changing-and-removing-strings) de la chaîne internationalisée afin de faire la distinction entre les chaînes en double dans le dictionnaire. Utilisez le deuxième paramètre facultatif de la méthode `get` pour fournir l’indice de traduction. L’indice de traduction doit correspondre exactement à la propriété « Comment » de l’élément dans le dictionnaire.

Par exemple, le dictionnaire contient la chaîne `Request` deux fois : une fois comme verbe et une fois comme nom. Le code suivant inclut l’indice de traduction en tant qu’argument dans la méthode `get` :

```java
i18n.get("Request","A noun, as in a request for a web page");
```

#### Inclusion de variables dans des phrases localisées {#including-variables-in-localized-sentences}

Incluez des variables dans la chaîne localisée pour créer un contexte de signification dans une phrase. Par exemple, après vous être connecté à une application Web, la page d’accueil affiche le message « Bienvenue, Administrateur ou Administratrice. Vous avez deux messages dans votre boîte de réception.&quot; Le contexte de la page détermine le nom de l’utilisateur ou de l’utilisatrice et le nombre de messages.

[Dans le dictionnaire](/help/sites-developing/i18n-translator.md#adding-changing-and-removing-strings), les variables sont représentées dans des chaînes sous la forme d’index entre crochets. Indiquez les valeurs des variables en tant qu’arguments de la méthode `get`. Les arguments sont placés à la suite de l’indice de traduction, et les index correspondent à l’ordre des arguments :

```xml
i18n.get("Welcome back {0}. You have {1} messages.", "user name, number of messages", user.getDisplayName(), numItems);
```

La chaîne internationalisée et l’indice de traduction doivent correspondre exactement à la chaîne et au commentaire du dictionnaire. Vous pouvez omettre l’indice de traduction en fournissant une valeur `null` comme deuxième argument.

#### Utilisation de méthode Get statique {#using-the-static-get-method}

La variable `I18N` définit une classe statique. `get` qui s’avère utile lorsque vous devez localiser quelques chaînes. Outre les paramètres de la méthode `get` d’un objet, la méthode statique nécessite l’objet `SlingHttpRequest` ou le `ResourceBundle` que vous utilisez, suivant la manière dont vous déterminez la langue par défaut de l’utilisateur :

* Utilisation de la préférence de langue de l’utilisateur : indiquez l’objet SlingHttpRequest comme premier paramètre.

  `I18n.get(slingHttpRequest, "Welcome back {}. You have {} messages.", "user name, number of messages", user.getDisplayName(), numItems);`
* Utilisation de la langue de la page : indiquez ResourceBundle comme premier paramètre.

  `I18n.get(resourceBundle,"Welcome back {}. You have {} messages.", "user name, number of messages", user.getDisplayName(), numItems);`

### Internationalisation de chaînes dans un code JavaScript {#internationalizing-strings-in-javascript-code}

L’API JavaScript vous permet de localiser des chaînes sur le client. Comme avec [Java™ et JSP](#internationalizing-strings-in-java-and-jsp-code) , l’API JavaScript vous permet d’identifier les chaînes à localiser, de fournir des conseils de localisation et d’inclure des variables dans les chaînes localisées.

La variable `granite.utils` [dossier de bibliothèque cliente](/help/sites-developing/clientlibs.md) fournit l’API JavaScript. Pour utiliser l’API, vous devez inclure ce dossier sur votre page. Les fonctions de localisation utilisent l’espace de noms `Granite.I18n`.

Avant de présenter des chaînes localisées, définissez les paramètres régionaux à l’aide de la variable `Granite.I18n.setLocale` de la fonction Pour cette fonction, le code de langue du paramètre régional doit être défini comme argument :

```
Granite.I18n.setLocale("fr");
```

Pour présenter une chaîne localisée, utilisez la fonction `Granite.I18n.get` :

```
Granite.I18n.get("string to localize");
```

L’exemple suivant internationalise la chaîne &quot;Welcome back&quot; :

```
Granite.I18n.setLocale("fr");
Granite.I18n.get("string to localize", [variables], "localization hint");
```

Les paramètres de la fonction sont différents de la méthode Java™ I18n.get :

* Le premier paramètre est le littéral de chaîne à localiser.
* Le deuxième paramètre est un tableau de valeurs à injecter dans le littéral de chaîne.
* Le troisième paramètre est l’indice de localisation.

L’exemple suivant utilise JavaScript pour localiser &quot;Welcome back Administrator. Vous avez deux messages dans votre boîte de réception.&quot; phrase :

```
Granite.I18n.setLocale("fr");
Granite.I18n.get("Welcome back {0}. You have {1} new messages in your inbox.", [username, numMsg], "user name, number of messages");
```

### Internationalisation de chaînes à partir de noeuds JCR {#internationalizing-strings-from-jcr-nodes}

Les chaînes d’IU sont souvent basées sur les propriétés de noeud JCR. Par exemple, la propriété `jcr:title` d’une page est généralement utilisée comme contenu de l’élément `h1` dans le code de la page. La classe `I18n` fournit la méthode `getVar` pour localiser ces chaînes.

L’exemple de script JSP suivant récupère la propriété `jcr:title` du référentiel et affiche la chaîne localisée sur la page :

```java
<% title = properties.get("jcr:title", String.class);%>
<h1><%=i18n.getVar(title) %></h1>
```

#### Spécification de conseils de traduction pour les noeuds JCR {#specifying-translation-hints-for-jcr-nodes}

Similaire à [Conseils de traduction dans l’API Java™](#using-translation-hints), vous pouvez fournir des conseils de traduction pour distinguer les chaînes en double dans le dictionnaire. Fournissez l’indice de traduction en tant que propriété du noeud qui contient la propriété internationalisée. Le nom de la propriété hint est composé du nom de la propriété internationalisée avec la propriété `_commentI18n` suffix :

`${prop}_commentI18n`

Par exemple, un nœud `cq:page` comprend la propriété jcr:title en cours de localisation. L’indice est fourni comme valeur de la propriété nommée jcr:title_commentI18n.

### Test de la couverture d’internationalisation {#testing-internationalization-coverage}

Vérifiez si vous avez internationalisé toutes les chaînes de votre interface utilisateur. Pour voir quelles chaînes sont couvertes, définissez la langue de l’utilisateur sur zz_ZZ et ouvrez l’interface utilisateur dans le navigateur web. Les chaînes internationalisées apparaissent avec une traduction en stub au format suivant :

`USR_*Default-String*_尠`

La capture d’écran ci-dessous illustre la traduction souche pour la page d’accueil d’AEM :

![chlimage_1](assets/chlimage_1a.jpeg)

Pour définir la langue de l’utilisateur, configurez la propriété language du noeud preferences du compte utilisateur.

Le noeud preferences d’un utilisateur a un chemin d’accès similaire à celui-ci :

`/home/users/<letter>/<hash>/preferences`

![chlimage_1-1](assets/chlimage_1-1a.jpeg)
