---
title: Configuration de l’utilisation de cookies
seo-title: Configuration de l’utilisation de cookies
description: AEM propose un service qui vous permet de configurer et contrôler le mode d’utilisation des cookies avec vos pages web.
seo-description: AEM propose un service qui vous permet de configurer et contrôler le mode d’utilisation des cookies avec vos pages web.
uuid: 10d95176-0a56-41f1-9d36-01dbdac757d4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 5773ec1a-f15b-462d-8f9f-54ee1d7ead44
translation-type: tm+mt
source-git-commit: f64eb57a69f2124523bd6eaed3e2f58a54c1ea8e
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 81%

---


# Configuration de l’utilisation de cookies{#configuring-cookie-usage}

AEM fournit un service qui vous permet de configurer et de contrôler l’utilisation des cookies dans vos pages Web :

* Un service configurable côté serveur conserve la liste des cookies qui peuvent être utilisés.
* Une API JavaScript permet à votre code JavaScript de vérifier qu’un cookie peut être utilisé.

Utilisez cette fonctionnalité pour vous assurer que vos pages respectent l’autorisation des utilisateurs concernant l’utilisation des cookies.

## Configuration des cookies autorisés {#configuring-allowed-cookies}

Configuration du service d’exclusion d’Adobe Granite pour indiquer la façon dont les cookies sont utilisés sur vos pages web. Le tableau suivant décrit les propriétés que vous pouvez configurer.

Pour configurer le service, vous pouvez utiliser la [console Web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) ou [ajouter une configuration OSGi au référentiel](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository). Le tableau suivant décrit les propriétés dont vous avez besoin pour l’une ou l’autre de ces méthodes. Pour une configuration OSGi, le PID du service est `com.adobe.granite.optout`.

| Nom de propriété (console Web) | Nom de propriété OSGi | Description |
|---|---|---|
| Cookies d’exclusion | optout.cookies | Nom des cookies qui indiquent, lorsqu’ils sont présents sur le périphérique de l’utilisateur, que celui-ci n’a pas consenti à utiliser les cookies. |
| En-têtes HTTP d’exclusion | optout.headers | Noms des en-têtes HTTP qui indiquent, lorsqu’ils sont présents, que l’utilisateur n’a pas consenti à utiliser des cookies. |
| Cookies de Liste blanche | optout.whitelist.cookies | Liste de cookies essentiels au fonctionnement du site Web et pouvant être utilisés sans le consentement de l’utilisateur. |

## Validation de l’utilisation de cookies {#validating-cookie-usage}

Code JavaScript côté client permettant d’appeler le service d’exclusion d’Adobe Granite pour vérifier que vous pouvez utiliser un cookie. Utilisez l’objet JavaScript Granite.OptOutUtil pour effectuer l’une des tâches suivantes :

* Obtenir une liste de noms de cookie indiquant que cet utilisateur n’autorise pas l’utilisation des cookies à des fins de suivi.
* Obtenir la liste des cookies qui peuvent être utilisés.
* Déterminer si le navigateur web contient un cookie indiquant que l’utilisateur n’autorise pas l’utilisation de cookies à des fins de suivi.
* Déterminer si un cookie spécifique peut être utilisé.

Le [dossier de bibliothèque cliente](/help/sites-developing/clientlibs.md#referencing-client-side-libraries) fournit l’objet Granite.OptOutUtil. Ajoutez le code suivant au JSP d’en-tête de votre page pour inclure un lien vers la bibliothèque JavaScript :

`<ui:includeClientLib categories="granite.utils" />`

Par exemple, la fonction JavaScript suivante détermine si le cookie COOKIE_NAME peut être utilisé avant de faire l’objet d’opérations d’écriture :

```
function writeCookie(value){
   if (!Granite.OptOutUtil.maySetCookie("COOKIE_NAME"))
      return;
   if (value) {
      value = encodeURIComponent(value);
      document.cookie = "COOKIE_NAME=" + value;
   }
}
```

## Objet JavaScript Granite.OptOutUtil  {#the-granite-optoututil-javascript-object}

L’objet Granite.OptOutUtil vous permet de déterminer si l’utilisation des cookies est autorisée.

### Fonction getCookieNames()  {#getcookienames-function}

Renvoie les noms des cookies qui indiquent, lorsqu’ils sont présents, que l’utilisateur n’a pas consenti à ce que les cookies soient utilisés.

**Paramètres**

Aucune.

**Renvoie**

Tableau de noms de cookies.

#### Fonction getWhitelistCookieNames()  {#getwhitelistcookienames-function}

Renvoie les noms des cookies qui peuvent être utilisés indépendamment de l’autorisation de l’utilisateur.

**Paramètres**

Aucune.

**Renvoie**

Tableau de noms de cookies.

#### Fonction isOptedOut()  {#isoptedout-function}

Détermine si le navigateur de l’utilisateur contient des cookies qui indiquent que l’autorisation d’utilisation des cookies n’a pas été accordée.

**Paramètres**

Aucune.

**Renvoie**

Valeur booléenne `true` si un cookie indique que l’autorisation n’a pas été accordée et valeur `false` si aucun cookie n’indique une absence d’autorisation.

### Fonction maySetCookie(cookieName){#maysetcookie-cookiename-function}

Détermine si un cookie spécifique peut être utilisé dans le navigateur de l’utilisateur. Cette fonction revient à utiliser `isOptedOut` parallèlement à la fonction permettant de déterminer si le cookie en question est inclus dans la liste renvoyée par la fonction `getWhitelistCookieNames`.

**Paramètres**

* cookieName : String. Nom du cookie.

**Renvoie**

Valeur booléenne `true` si `cookieName` peut être utilisée, ou valeur `false` si `cookieName` ne peut pas être utilisée.
