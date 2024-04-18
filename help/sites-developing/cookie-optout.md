---
title: Configuration de l’utilisation de cookies
description: AEM fournit un service qui vous permet de configurer et de contrôler la manière dont les cookies sont utilisés avec vos pages web.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: 42e8d804-6b6a-432e-a651-940b9f45db4e
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 100%

---

# Configuration de l’utilisation de cookies{#configuring-cookie-usage}

AEM fournit un service qui vous permet de configurer et de contrôler la manière dont les cookies sont utilisés avec vos pages web :

* Un service côté serveur configurable conserve une liste de cookies pouvant être utilisés.
* Une API JavaScript permet à votre code JavaScript de vérifier qu’un cookie peut être utilisé.

Utilisez cette fonction pour vous assurer que vos pages respectent le consentement de vos utilisateurs et utilisatrices concernant l’utilisation des cookies.

## Configuration des cookies autorisés {#configuring-allowed-cookies}

Configurez le service d’opt-out d’Adobe Granite pour spécifier la manière dont les cookies sont utilisés sur vos pages web. Le tableau ci-dessous décrit les propriétés que vous pouvez configurer.

Pour configurer le service, vous pouvez utiliser la [console Web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) ou [ajouter une configuration OSGi au référentiel](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository). Le tableau suivant décrit les propriétés dont vous avez besoin pour l’une ou l’autre de ces méthodes. Pour une configuration OSGi, le PID du service est `com.adobe.granite.optout`.

| Nom de propriété (console web) | Nom de propriété OSGi | Description |
|---|---|---|
| Cookies de droit d’opposition | optout.cookies | Les noms des cookies qui indiquent, lorsqu’ils sont présents sur l’appareil de l’utilisateur ou de l’utilisatrice, que celui-ci ou celle-ci n’a pas consenti à utiliser les cookies. |
| En-têtes HTTP de droit d’opposition | optout.headers | Les noms des en-têtes HTTP qui indiquent, lorsqu’ils sont présents, que l’utilisateur ou l’utilisatrice n’a pas consenti à l’utilisation de cookies. |
| Cookies de liste autorisée | optout.whitelist.cookies | Liste des cookies qui sont essentiels au fonctionnement du site Web et qui peuvent être utilisés sans le consentement de l’utilisateur. |

## Validation de l’utilisation des cookies {#validating-cookie-usage}

Utilisez JavaScript côté client pour appeler le service d’opt-out d’Adobe Granite afin de vérifier que vous pouvez utiliser un cookie. Utilisez l’objet JavaScript Granite.OptOutUtil pour effectuer l’une des tâches suivantes :

* Obtenez une liste de noms de cookie indiquant que cet utilisateur ou cette utilisatrice n’autorise pas l’utilisation de cookies à des fins de suivi.
* Obtenez la liste des cookies qui peuvent être utilisés.
* Déterminez si le navigateur Web contient un cookie qui indique que l’utilisateur ou l’utilisatrice ne consent pas à l’utilisation des cookies pour le suivi.
* Déterminez si un cookie spécifique peut être utilisé.

Le [dossier de bibliothèque cliente](/help/sites-developing/clientlibs.md#referencing-client-side-libraries) granite.utils fournit l’objet Granite.OptOutUtil. Ajoutez le code suivant au JSP d’en-tête de votre page pour inclure un lien vers la bibliothèque JavaScript :

`<ui:includeClientLib categories="granite.utils" />`

Par exemple, la fonction JavaScript suivante détermine si le cookie COOKIE_NAME peut être utilisé avant d’y écrire :

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

Granite.OptOutUtil vous permet de déterminer si l’utilisation des cookies est autorisée.

### Fonction getCookieNames() {#getcookienames-function}

Les noms des cookies qui, lorsqu’ils sont présents, indiquent que l’utilisateur ou l’utilisatrice n’a pas donné son consentement à l’utilisation des cookies.

**Paramètres**

Aucun.

**Renvoie**

Tableau de noms de cookies.

#### Fonction getWhitelistCookieNames() {#getwhitelistcookienames-function}

Les noms des cookies qui peuvent être utilisés, quel que soit le consentement de l’utilisateur ou de l’utilisatrice.

**Paramètres**

Aucun.

**Renvoie**

Tableau de noms de cookies.

#### Fonction isOptedOut() {#isoptedout-function}

Détermine si le navigateur de l’utilisateur ou de l’utilisatrice contient des cookies qui indiquent que le consentement pour l’utilisation des cookies n’a pas été donné.

**Paramètres**

Aucun.

**Renvoie**

Valeur booléenne `true` si un cookie indique que l’autorisation n’a pas été accordée et valeur `false` si aucun cookie n’indique une absence d’autorisation.

### Fonction maySetCookie(cookieName) {#maysetcookie-cookiename-function}

Détermine si un cookie spécifique peut être utilisé sur le navigateur de l’utilisateur ou l’utilisatrice. Cette fonction revient à utiliser la fonction `isOptedOut` permettant de déterminer si le cookie en question est inclus dans la liste renvoyée par la fonction `getWhitelistCookieNames`.

**Paramètres**

* cookieName : chaîne. Le nom du cookie.

**Renvoie**

Valeur booléenne `true` si `cookieName` peut être utilisé et valeur `false` si `cookieName` ne peut pas l’être.
