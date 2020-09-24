---
title: Connexion unique
seo-title: Connexion unique
description: 'Découvrez comment configurer la connexion unique (SSO) pour une instance AEM. '
seo-description: 'Découvrez comment configurer la connexion unique (SSO) pour une instance AEM. '
uuid: b8dcb28e-4604-4da5-b8dd-4e1e2cbdda18
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring, Security
content-type: reference
discoiquuid: 86e8dc12-608d-4aff-ba7a-5524f6b4eb0d
translation-type: tm+mt
source-git-commit: 46f2ae565fe4a8cfea49572eb87a489cb5d9ebd7
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 81%

---


# Connexion unique {#single-sign-on}

La connexion unique permet à l’utilisateur d’accéder à plusieurs systèmes après avoir fourni une seule fois ses informations d’identification (telles qu’un nom d’utilisateur et un mot de passe). Un système distinct (appelé l’authentificateur de confiance) effectue une authentification et fournit à Experience Manager les informations d’identification de l’utilisateur. Experience Manager vérifie les autorisations d’accès de l’utilisateur et les applique (c’est-à-dire qu’il détermine les ressources auxquelles l’utilisateur a accès).

Le service de gestion de l’authentification SSO (`com.adobe.granite.auth.sso.impl.SsoAuthenticationHandler`) traite les résulats de l’authentification que l’authentificateur de confiance fournit. Le gestionnaire d’authentification unique recherche un identifiant d’authentification unique (identifiant d’authentification unique) comme valeur d’un attribut spécial aux emplacements suivants dans cet ordre :

1. En-têtes de la demande
1. Cookies
1. Paramètres de la demande

Lorsqu’une valeur est trouvée, la recherche est terminée et cette valeur est utilisée. 

Configurez les deux services suivants pour identifier le nom de l’attribut qui stocke le ssid :

* Le module de connexion.
* Le service d’authentification SSO.

Vous devez spécifier le même nom d’attribut pour les deux services. The attribute is included in the `SimpleCredentials` that is provided to `Repository.login`. La valeur de l’attribut est inutile et ignorée. Sa simple présence est importante et vérifiée.

## CONFIGURATION SSO {#configuring-sso}

Pour configurer le SSO pour une instance AEM, vous devez configurer le [gestionnaire d’authentification SSO](/help/sites-deploying/osgi-configuration-settings.md#adobegranitessoauthenticationhandler) :

1. Lorsque vous utilisez AEM, plusieurs méthodes de gestion des paramètres de configuration sont disponibles pour ces services ; voir [Configuration OSGi](/help/sites-deploying/configuring-osgi.md) pour plus de détails et les pratiques recommandées.

   Par exemple, pour l’ensemble NTLM :

   * **Chemin d’accès :** en fonction des besoins, par exemple, `/`
   * **Noms des** en-têtes : `LOGON_USER`
   * **Format** d’ID : `^<DOMAIN>\\(.+)$`

      Where `<*DOMAIN*>` is replaced by your own domain name.
   Pour CoSign :

   * **Chemin d’accès :** en fonction des besoins, par exemple, `/`
   * **Noms des en-têtes** : remote_user
   * **Format d’ID :** AsIs

   Pour SiteMinder :

   * **Chemin d’accès :** en fonction des besoins, par exemple, `/`
   * **Noms des en-têtes :** SM_USER
   * **Format d’ID** : AsIs



1. Vérifiez que la connexion unique fonctionne selon vos besoins, y compris les autorisations.

>[!CAUTION]
>
>Assurez-vous que les utilisateurs ne peuvent pas accéder à AEM directement si le SSO est configuré. 
>
>En demandant aux utilisateurs de passer par un serveur web exécutant l’agent de votre système, cela assure qu’aucun utilisateur ne peut directement envoyer un en-tête, un cookie ou un paramètre qui entraînerait son approbation par AEM, puisque l’agent va filtrer de telles informations si elles sont envoyées depuis l’extérieur.
>
>Tout utilisateur pouvant accéder directement à votre instance AEM sans passer par le serveur web peut agir comme n’importe quel autre utilisateur en envoyant l’en -tête, le cookie ou le paramètre si les noms sont connus.
>
>Assurez-vous également vous configurez uniquement les en-têtes, cookies et noms de paramètres de demandes requis pour votre configuration SSO.


>[!NOTE]
>
>La connexion unique est souvent utilisée avec [LDAP](/help/sites-administering/ldap-config.md).

>[!NOTE]
>
>Si vous utilisez également le [dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html) avec le serveur Microsoft Internet Information (IIS) une configuration supplémentaire sera nécessaire dans :
>
>* `disp_iis.ini`
>* IIS

>
>
Dans le `disp_iis.ini` jeu :
>(see [installing the Dispatcher with the Microsoft Internet Information Server](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-install.html#microsoft-internet-information-server) for full details)
>
>* `servervariables=1` (transmet des variables de serveur IIS comme en-têtes de requête à une instance distante)
>* `replaceauthorization=1` (remplace n’importe quel en-tête appelé « Authorization » autre que l’en-tête « Basic » par son « Basic » équivalent)

>
>
Dans IIS :
>
>* désactiver **l’accès anonyme**
   >
   >
* autoriser **l’authentification intégrée de Windows**

>



Vous pouvez voir quel gestionnaire d’authentification est appliqué à n’importe quelle section de l’arborescence de contenu à l’aide de l’option **Authentificateur** de la console Felix ; par exemple :

`http://localhost:4502/system/console/slingauth`

Le gestionnaire qui correspond le mieux au chemin est le premier à être appelé. For example, if you configure handler-A for the path `/` and handler-B for the path `/content`, then a request to `/content/mypage.html` will query handler-B first.

![screen_shot_2012-02-15at21006pm](assets/screen_shot_2012-02-15at21006pm.png)

### Exemple {#example}

For a cookie request (using the URL `http://localhost:4502/libs/wcm/content/siteadmin.html`):

```xml
GET /libs/cq/core/content/welcome.html HTTP/1.1
Host: localhost:4502
Cookie: TestCookie=admin
```

Utilisation de la configuration suivante :

* **Chemin**: `/`

* **Noms des** en-têtes : `TestHeader`

* **Noms** des cookies : `TestCookie`

* **Noms des** paramètres : `TestParameter`

* **Format** d’ID : `AsIs`

La réponse est :

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

Cela fonctionne également si vous demandez :
`http://localhost:4502/libs/cq/core/content/welcome.html?TestParameter=admin`

Vous pouvez également utiliser la commande curl suivante pour envoyer l’ `TestHeader` en-tête à `admin:`
`curl -D - -H "TestHeader: admin" http://localhost:4502/libs/cq/core/content/welcome.html`

>[!NOTE]
>
>Lorsque vous utilisez le paramètre de demande dans un navigateur, vous ne verrez qu’une partie du HTML, sans le CSS. C’est parce que toutes les demandes HTML sont effectuées sans paramètre de requête.

## Suppression des liens de déconnexion AEM {#removing-aem-sign-out-links}

Lorsque vous utilisez le SSO, la connexion et la déconnexion sont traités en externe, de sorte que les liens de déconnexion d’AEM ne s’appliquent plus et doivent être supprimés.

Le lien de déconnexion sur l’écran de bienvenue peut être supprimé en suivant les étapes suivantes.

1. Recouvrement `/libs/cq/core/components/welcome/welcome.jsp` vers `/apps/cq/core/components/welcome/welcome.jsp`
1. Supprimez la partie suivante de JSP.

   `<a href="#" onclick="signout('<%= request.getContextPath() %>');" class="signout"><%= i18n.get("sign out", "welcome screen") %>`

Pour supprimer le lien de déconnexion disponible dans le menu personnel de l’utilisateur dans le coin supérieur droit, procédez comme suit :

1. Recouvrement `/libs/cq/ui/widgets/source/widgets/UserInfo.js` vers `/apps/cq/ui/widgets/source/widgets/UserInfo.js`

1. Supprimez la partie suivante du fichier :

   ```
   menu.addMenuItem({
       "text":CQ.I18n.getMessage("Sign out"),
       "cls": "cq-userinfo-logout",
       "handler": this.logout
   });
   menu.addSeparator();
   ```

