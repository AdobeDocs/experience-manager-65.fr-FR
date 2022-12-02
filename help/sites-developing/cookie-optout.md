---
title: Configuration de l’utilisation de cookies
seo-title: Configuring Cookie Usage
description: AEM propose un service qui vous permet de configurer et contrôler le mode d’utilisation des cookies avec vos pages web.
seo-description: AEM provides a service that enables you to configure and control how cookies are used with your web pages
uuid: 10d95176-0a56-41f1-9d36-01dbdac757d4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 5773ec1a-f15b-462d-8f9f-54ee1d7ead44
exl-id: 42e8d804-6b6a-432e-a651-940b9f45db4e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 100%

---

# Configuration de l’utilisation de cookies{#configuring-cookie-usage}

AEM propose un service qui vous permet de configurer et contrôler le mode d’utilisation des cookies avec vos pages web. :

* Un service configurable côté serveur conserve la liste des cookies qui peuvent être utilisés.
* Une API JavaScript permet à votre code JavaScript de vérifier qu’un cookie peut être utilisé.

Utilisez cette fonctionnalité pour vous assurer que vos pages respectent l’autorisation des utilisateurs concernant l’utilisation des cookies.

## Configuration des cookies autorisés {#configuring-allowed-cookies}

Configuration du service d’exclusion d’Adobe Granite pour indiquer la façon dont les cookies sont utilisés sur vos pages web. Le tableau suivant décrit les propriétés que vous pouvez configurer.

Pour configurer le service, vous pouvez utiliser la [console Web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) ou [ajouter une configuration OSGi au référentiel](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository). Le tableau suivant décrit les propriétés dont vous avez besoin pour l’une ou l’autre de ces méthodes. Pour une configuration OSGi, le PID du service est `com.adobe.granite.optout`.

| Nom de propriété (console Web) | Nom de propriété OSGi | Description |
|---|---|---|
| Cookies de droit d’opposition | optout.cookies | Les noms des cookies qui indiquent, lorsqu’ils sont présents sur l’appareil de l’utilisateur, que celui-ci n’a pas consenti à utiliser les cookies. |
| En-têtes HTTP de droit d’opposition | optout.headers | Les noms des en-têtes HTTP qui indiquent, lorsqu’ils sont présents, que l’utilisateur n’a pas consenti à l’utilisation de cookies. |
| Cookies de liste autorisée | optout.whitelist.cookies | Liste des cookies qui sont essentiels au fonctionnement du site Web et qui peuvent être utilisés sans le consentement de l’utilisateur. |

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

## Objet JavaScript Granite.OptOutUtil {#the-granite-optoututil-javascript-object}

L’objet Granite.OptOutUtil vous permet de déterminer si l’utilisation des cookies est autorisée.

### Fonction getCookieNames() {#getcookienames-function}

Renvoie les noms des cookies qui indiquent, lorsqu’ils sont présents, que l’utilisateur n’a pas consenti à ce que les cookies soient utilisés.

**Paramètres**

Aucun.

**Renvoie**

Tableau de noms de cookies.

#### Fonction getWhitelistCookieNames() {#getwhitelistcookienames-function}

Renvoie les noms des cookies qui peuvent être utilisés indépendamment de l’autorisation de l’utilisateur.

**Paramètres**

Aucun.

**Renvoie**

Tableau de noms de cookies.

#### Fonction isOptedOut() {#isoptedout-function}

Détermine si le navigateur de l’utilisateur contient des cookies qui indiquent que l’autorisation d’utilisation des cookies n’a pas été accordée.

**Paramètres**

Aucun.

**Renvoie**

Valeur booléenne `true` si un cookie indique que l’autorisation n’a pas été accordée et valeur `false` si aucun cookie n’indique une absence d’autorisation.

### Fonction maySetCookie(cookieName) {#maysetcookie-cookiename-function}

Détermine si un cookie spécifique peut être utilisé dans le navigateur de l’utilisateur. Cette fonction revient à utiliser `isOptedOut` parallèlement à la fonction permettant de déterminer si le cookie en question est inclus dans la liste renvoyée par la fonction `getWhitelistCookieNames`.

**Paramètres**

* cookieName : String. Nom du cookie.

**Renvoie**

Valeur booléenne `true` si `cookieName` peut être utilisé et valeur `false` si `cookieName` ne peut pas l’être.
