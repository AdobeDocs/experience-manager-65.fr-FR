---
title: Connexion unique
description: Découvrez comment configurer l’authentification unique (SSO) pour une instance de Adobe Experience Manager (AEM).
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring, Security
content-type: reference
feature: Configuring
exl-id: 7d2e4620-c3a5-4f5a-9eb6-42a706479d41
source-git-commit: 3bcdbfc17efe1f4c6069fd97fd6a16ec41d0579e
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 40%

---

# Connexion unique {#single-sign-on}

L’authentification unique (SSO) permet à une personne d’accéder à plusieurs systèmes après avoir fourni une seule fois des informations d’identification d’authentification (telles qu’un nom d’utilisateur ou d’utilisatrice et un mot de passe). Un système distinct (appelé authentificateur approuvé) effectue l’authentification et fournit à Experience Manager les informations d’identification de l’utilisateur ou utilisatrice. Experience Manager vérifie les autorisations d’accès et les applique pour l’utilisateur ou l’utilisatrice (c’est-à-dire, détermine les ressources auxquelles l’utilisateur ou l’utilisatrice est autorisé à accéder).

Le service de gestion de l’authentification SSO (`com.adobe.granite.auth.sso.impl.SsoAuthenticationHandler`) traite les résultats de l’authentification fournis par l’authentificateur de confiance. Le gestionnaire d’authentification SSO recherche un identificateur SSO (SSID) comme valeur d’un attribut spécial aux emplacements suivants dans cet ordre :

1. En-têtes de requête
1. Cookies
1. Paramètres de requête

Lorsqu’une valeur est trouvée, la recherche est terminée et cette valeur est utilisée.

Configurez les deux services suivants pour reconnaître le nom de l’attribut qui stocke le SSID :

* Module de connexion.
* Service d’authentification SSO.

Indiquez le même nom d’attribut pour les deux services. L’attribut est inclus dans les `SimpleCredentials` fournies dans `Repository.login`. La valeur de l’attribut n’est pas pertinente et ignorée, la simple présence de l’attribut est importante et vérifiée.

## Configuration d’authentification unique {#configuring-sso}

Pour configurer l’authentification unique pour une instance AEM, vous devez configurer la variable [Gestionnaire d’authentification SSO](/help/sites-deploying/osgi-configuration-settings.md#adobegranitessoauthenticationhandler):

1. Lorsque vous utilisez AEM, plusieurs méthodes permettent de gérer les paramètres de configuration pour ces services. Consultez la section [Configuration d’OSGi](/help/sites-deploying/configuring-osgi.md) pour plus de détails et connaître les pratiques recommandées.

   Par exemple, pour l’ensemble NTLM :

   * **Chemin d’accès :** en fonction des besoins, par exemple, `/`
   * **Noms d’en -tête** : `LOGON_USER`
   * **Format d’ID** : `^<DOMAIN>\\(.+)$`

     Où `<*DOMAIN*>` est remplacé par le nom de votre propre domaine.

   Pour CoSign :

   * **Chemin d’accès :** en fonction des besoins, par exemple, `/`
   * **Noms des en-têtes** : remote_user
   * **Format d’ID :** AsIs

   Pour SiteMinder :

   * **Chemin d’accès :** en fonction des besoins, par exemple, `/`
   * **Noms des en-têtes :** SM_USER
   * **Format d’ID** : AsIs

1. Vérifiez que la connexion unique fonctionne selon vos besoins, y compris les autorisations.

>[!CAUTION]
>
>Assurez-vous que les utilisateurs ne peuvent pas accéder directement à AEM si SSO est configuré.
>
>En obligeant les utilisateurs à passer par un serveur web qui exécute l’agent de votre système SSO, il est garanti qu’aucun utilisateur ne peut envoyer directement un en-tête, un cookie ou un paramètre qui amènera l’utilisateur à être approuvé par AEM, car l’agent filtrera ces informations si elles sont envoyées de l’extérieur.
>
>Tout utilisateur qui peut accéder directement à votre instance AEM sans passer par le serveur web pourra agir comme n’importe quel utilisateur en envoyant l’en-tête, le cookie ou le paramètre si les noms sont connus.
>
>Assurez-vous également que, parmi les en-têtes, les cookies et les noms de paramètres de requête, vous ne configurez que celui qui est requis pour votre configuration SSO.
>

>[!NOTE]
>
>L’authentification unique est souvent utilisée avec [LDAP](/help/sites-administering/ldap-config.md).

>[!NOTE]
>
>Si vous utilisez également la variable [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=fr) avec Microsoft® Internet Information Server (IIS), une configuration supplémentaire est requise dans :
>
* `disp_iis.ini`
* IIS
>
Dans `disp_iis.ini` set : (voir [installation de Dispatcher avec Microsoft® Internet Information Server](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/dispatcher-install.html#microsoft-internet-information-server) pour plus de détails)
>
* `servervariables=1` (transmet des variables de serveur IIS comme en-têtes de requête à une instance distante)
* `replaceauthorization=1` (remplace n’importe quel en-tête appelé « Authorization » autre que l’en-tête « De base » par son « De base » équivalent)
>
Dans IIS :
>
* Désactivez **l’accès anonyme**.
>
* enable **Authentification Windows intégrée**
>

Vous pouvez voir quel gestionnaire d’authentification est appliqué à n’importe quelle section de l’arborescence de contenu à l’aide de la variable **Authentificateur** de la console Felix, par exemple :

`http://localhost:4502/system/console/slingauth`

Le gestionnaire qui correspond le mieux au chemin est le premier à être appelé. Par exemple, si vous configurez le gestionnaire A pour le chemin `/`/ et le gestionnaire B pour le chemin `/content`, alors une demande à `/content/mypage.html` appellera le gestionnaire B en premier.

![screen_shot_2012-02-15at21006pm](assets/screen_shot_2012-02-15at21006pm.png)

### Exemple {#example}

Pour une demande de cookie (à l’aide de l’URL `http://localhost:4502/libs/wcm/content/siteadmin.html`) :

```xml
GET /libs/cq/core/content/welcome.html HTTP/1.1
Host: localhost:4502
Cookie: TestCookie=admin
```

Utilisation de la configuration suivante :

* **Chemin** : `/`

* **Noms d’en-têtes** : `TestHeader`

* **Noms de cookies** : `TestCookie`

* **Noms des paramètres** : `TestParameter`

* **Format d’ID** : `AsIs`

La réponse serait :

```xml
HTTP/1.1 200 OK
Connection: Keep-Alive
Server: Day-Servlet-Engine/4.1.24
Content-Type: text/html;charset=utf-8
Date: Thu, 23 Aug 2012 09:58:39 GMT
Transfer-Encoding: chunked

<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "https://www.w3.org/TR/html4/strict.dtd">
<html>
<head>
    <meta http-equiv="content-type" content="text/html; charset=UTF-8">
    <title>Welcome to Adobe&reg; CQ5</title>
....
```

Cela fonctionne également si vous demandez :
`http://localhost:4502/libs/cq/core/content/welcome.html?TestParameter=admin`

Vous pouvez également utiliser la commande curl suivante pour envoyer l’en-tête `TestHeader` à `admin:`
`curl -D - -H "TestHeader: admin" http://localhost:4502/libs/cq/core/content/welcome.html`

>[!NOTE]
>
Lors de l’utilisation du paramètre de requête dans un navigateur, vous ne voyez qu’une partie du HTML, sans CSS. Cela est dû au fait que toutes les requêtes du HTML sont effectuées sans le paramètre de requête .

## Suppression de liens AEM de déconnexion {#removing-aem-sign-out-links}

Lors de l’utilisation de l’authentification unique, la connexion et la déconnexion sont gérées en externe, de sorte que AEM liens de déconnexion ne sont plus applicables et doivent être supprimés.

Le lien de déconnexion sur l’écran de bienvenue peut être supprimé en procédant comme suit.

1. Recouvrez `/libs/cq/core/components/welcome/welcome.jsp` sur `/apps/cq/core/components/welcome/welcome.jsp`.
1. Supprimez la partie suivante du JSP.

   `<a href="#" onclick="signout('<%= request.getContextPath() %>');" class="signout"><%= i18n.get("sign out", "welcome screen") %>`

Pour supprimer le lien de déconnexion disponible dans le menu personnel de l’utilisateur dans le coin supérieur droit, procédez comme suit :

1. Recouvrez `/libs/cq/ui/widgets/source/widgets/UserInfo.js` sur `/apps/cq/ui/widgets/source/widgets/UserInfo.js`.

1. Supprimez la partie suivante du fichier :

   ```
   menu.addMenuItem({
       "text":CQ.I18n.getMessage("Sign out"),
       "cls": "cq-userinfo-logout",
       "handler": this.logout
   });
   menu.addSeparator();
   ```
