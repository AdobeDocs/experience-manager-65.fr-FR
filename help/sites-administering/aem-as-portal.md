---
title: Portails et portlets AEM
seo-title: AEM Portals and Portlets
description: Découvrez comment configurer et administrer AEM en tant que portail et comment configurer et afficher AEM contenu dans un portlet.
seo-description: Learn how to configure and administer AEM as a portal and how to configure and display AEM content in a portlet.
uuid: 7f9e316d-277e-4a1e-b6f3-cd89addc897b
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 99528fda-5c8c-4034-bcbe-a4cea42f694b
docset: aem65
exl-id: b5f3d3a6-39c0-4aa5-8562-3cc6fa2b9e46
source-git-commit: c7c32130a3257c14c98b52f9db31d80587d7993a
workflow-type: tm+mt
source-wordcount: '6100'
ht-degree: 58%

---

# Portails et portlets AEM{#aem-portals-and-portlets}

Ce document répond aux questions suivantes :

* Architecture d’AEM Portal
* Administration et configuration d’AEM en tant que portail
* Utilisation d’AEM comme portail
* Installation, configuration et affichage du contenu d’AEM dans un portlet (serveur Web, par exemple)

## Architecture d’AEM Portal {#aem-portal-architecture}

L’architecture d’AEM portail comprend des définitions de portails et de portlets.

### Qu’est-ce qu’un portail ? {#what-is-a-portal}

Un portail est une application web qui fournit la personnalisation, l’authentification unique, l’intégration de contenu provenant de différentes sources et héberge la couche de présentation des systèmes d’information.

Dans AEM, vous pouvez exécuter des portlets compatibles avec la spécification JSR-286. Le composant Portlet permet également d’incorporer un portlet dans la page. Consultez [Administration du portlet de contenu AEM](#administeringthecqcontentportlet).

### Qu’est-ce qu’un portlet ? {#what-is-a-portlet}

Les portlets sont des composants web déployés dans un conteneur, qui proposent du contenu dynamique. L’interface du portlet est regroupée et déployée sous forme de fichier WAR dans un conteneur de portlet. Si vous exécutez AEM en tant que portail, vous avez besoin du fichier .war du portlet pour exécuter le portlet.

Pour configurer AEM contenu à afficher dans un portail, voir [Installation, configuration et utilisation d’AEM dans un portlet](#installingconfiguringandusingcqinaportlet).

### Director du portail AEM {#aem-portal-director}

>[!CAUTION]
>
>AEM Portal Director est obsolète depuis AEM 6.4. Voir [Fonctionnalités obsolètes et supprimées](https://helpx.adobe.com/fr/experience-manager/6-4/release-notes/deprecated-removed-features.html).

## Administration du portlet de contenu AEM {#administering-the-aem-content-portlet}

Le portlet de contenu AEM permet d’afficher du contenu AEM sur un portail. Le portlet est disponible à l’adresse `/crx-quickstart/opt/portal` et peut être personnalisé de différentes façons. Par exemple, vous pouvez personnaliser la gestion SSO/de l’authentification en déployant votre propre service d’authentification générant les informations d’authentification nécessaires pour qu’AEM remplace le comportement par défaut. Les modules externes utilisent une API définie, qui permet d’ajouter votre propre fonctionnalité en créant le module externe contre les API. Le module externe peut être déployé dans le portlet exécuté. Pour fonctionner correctement, il nécessite une configuration de l’instance d’auteur et de publication d’AEM ainsi que le chemin d’accès au contenu à afficher au démarrage.

Certaines des configurations sont modifiables par le biais des préférences de portlet et d’autres par le biais des configurations de service OSGI. Vous pouvez modifier ces configurations à l’aide des fichiers **config** ou de la console Web OSGi.

### Préférences de portlet {#portlet-preferences}

Les préférences de porlet peuvent être configurées lors du déploiement sur le serveur du portail ou en modifiant le fichier **WEB-INF/portlet.xml** avant de déployer l’application web du portlet. Le fichier portlet.xml se présente, par défaut, comme suit :

```xml
<?xml version="1.0" encoding="UTF-8"?>
<portlet-app xmlns="https://java.sun.com/xml/ns/portlet/portlet-app_1_0.xsd"
             xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
             xsi:schemaLocation="https://java.sun.com/xml/ns/portlet/portlet-app_1_0.xsd /opt/SUNWps/dtd/portlet.xsd"
             version="1.0">
   <portlet>
      <portlet-name>RSSWeatherPortlet</portlet-name>
      <portlet-class>org.jboss.portlet.weather.WeatherPortlet</portlet-class>
      <init-param>
         <name>default_zipcode</name>
         <value>05673</value>
      </init-param>
      <init-param>
         <name>RSS_XSL</name>
         <value>/WEB-INF/Rss.xsl</value>
      </init-param>
      <init-param>
         <name>base_url</name>
         <value>https://xml.weather.yahoo.com/forecastrss?p=</value>
      </init-param>
      <expiration-cache>180</expiration-cache>
      <supports>
         <mime-type>text/html</mime-type>
         <portlet-mode>VIEW</portlet-mode>
         <portlet-mode>EDIT</portlet-mode>
      </supports>
      <portlet-info>
         <title>Weather Portlet</title>
      </portlet-info>
      <portlet-preferences>
         <preference>
            <name>expires</name>
            <value>180</value>
         </preference>
         <preference>
            <name>RssXml</name>
            <value>https://xml.weather.yahoo.com/forecastrss?p=33145</value>
            <read-only>false</read-only>
         </preference>
      </portlet-preferences>
   </portlet>
</portlet-app>
```

Le portlet peut être configuré avec les préférences suivantes :

<table>
 <tbody>
  <tr>
   <td>startPath</td>
   <td><p>Il s’agit du chemin de début du portlet : il définit le contenu affiché initialement.</p> <p><strong>Important</strong>: si le portlet est configuré pour se connecter à AEM instances de création et de publication qui s’exécutent sur un chemin de contexte différent de<strong> /</strong>, vous devez activer la force. <strong>CQUrlInfo</strong> dans la configuration du Gestionnaire de bibliothèques Html de ces instances AEM (par exemple, via la console web Felix) ou la modification ne fonctionnera pas et la boîte de dialogue Préférences ne s’affichera pas.</p> </td>
  </tr>
  <tr>
   <td>htmlSelector</td>
   <td>Sélecteur ajouté à chaque adresse URL. Par défaut, il s’agit d’un <strong>portlet</strong> afin que toutes les demandes de pages HTML qui utilisent des adresses URL qui se terminent par <strong>.portlet.html.</strong> Cela permet d’utiliser des scripts personnalisés dans AEM pour le rendu du portlet.</td>
  </tr>
  <tr>
   <td>addCssToPortalHeader</td>
   <td><p>Par défaut, les fichiers CSS d’AEM que contient la page HTML sont inclus dans le portlet. La désactivation de cette option exclut les fichiers CSS par défaut.</p> <p>Si cette option est activée, les fichiers CSS sont ajoutés à l’en-tête de la page html ou incorporés dans la page html en fonction du comportement du portail.</p> </td>
  </tr>
  <tr>
   <td>includeToolbar</td>
   <td>Par défaut, une barre d’outils est rendue dans le portlet de contenu pour la fonctionnalité de gestion. Si vous désactivez cette option, aucune barre d’outils n’est affichée.</td>
  </tr>
  <tr>
   <td>urlParameterNames</td>
   <td><p>Liste des autres noms de paramètre URL susceptibles de contenir la nouvelle adresse URL du contenu à afficher pour le portlet. La liste est traitée de haut en bas. Le premier paramètre contenant une valeur est utilisé. Si le système ne trouve aucune adresse URL, le paramètre d’URL par défaut est utilisé. L’URL fournie est utilisée, en l’état, sans modification supplémentaire.</p> <p>Ce paramètre est défini par portlet déployé. Il permet également de configurer globalement certains paramètres d’URL dans la configuration OSGi pour le "Day Portal Director Portlet Bridge".</p> </td>
  </tr>
  <tr>
   <td>preferredDialog</td>
   <td>Chemin d’accès à la boîte de dialogue Préférences dans AEM. Si cette préférence n’est pas renseignée, la boîte de dialogue Préférences intégrée est utilisée. Par défaut, cette valeur est définie sur /libs/portal/content/prefs.html.</td>
  </tr>
  <tr>
   <td>initialRedirect</td>
   <td>Par défaut, le portlet exécute une redirection JavaScript de toute la page du portail lors du premier appel. Cela permet de prendre en charge le scénario de glisser-déposer des serveurs de portail modernes. En production, cette redirection est rarement nécessaire et peut donc être désactivée lorsque cette préférence est définie sur <em>false</em>.</td>
  </tr>
 </tbody>
</table>

#### Console web OSGi {#osgi-web-console}

Si le serveur est exécuté sur localhost, port, et que l’application Web du portlet AEM est montée dans le contexte de l’application Web *cqportlet*, l’adresse URL de la console Web est `https://localhost:8080/cqportlet/cqbridge/system/console`:8080/. L’utilisateur et le mot de passe par défaut sont : **admin**.

Ouvrez l’onglet **Configurations** et sélectionnez **Configuration du serveur CQ de Portal Directory**. Vous spécifiez l’adresse URL de base de l’instance de création et de publication. Cette procédure est décrite dans la section [Configuration du portlet](#configuring-the-portlet).

>[!NOTE]
>
>La console web OSGi n’est destinée qu’à la modification des configurations en phase de développement (ou de test). Veillez à bloquer les demandes à la console pour les systèmes de production.

### Fournir des configurations {#providing-configurations}

Pour prendre en charge les déploiements automatisés et la configuration, le portlet de contenu d’AEM dispose d’une prise en charge de la configuration intégrée qui tente de lire les configurations du chemin d’accès aux classes fourni à l’application du portlet.

Au démarrage, la propriété système **com.day.cq.po rtet.config** est lue pour détecter l’environnement actif. En règle générale, la valeur de cette propriété est du type **dev**, **prod**, **test** et ainsi de suite. Si aucun environnement n’est défini, aucune configuration n’est lue.

Si un environnement est défini, le système cherche un fichier config dans le chemin d’accès aux classes sous** **com/day/cq/portlet/{env}.config**, où **env** est remplacé par la valeur actuelle pour l’environnement. Ce fichier doit répertorier tous les fichiers de configuration pour cet environnement. Ces fichiers sont recherchés par rapport à l’emplacement du fichier .config. Par exemple, si le fichier contient une ligne `my.service.xml,`, ce fichier est lu à partir du chemin d’accès aux classes sous `com/day/cq/portlet/my.service.config.`. Le nom du fichier est composé de l’identifiant de persistance du service, suivi de **.config**. Dans l’exemple précédent, l’ID de persistance est **my.service**. Le format du fichier de configuration est le format utilisé par le programme d’installation OSGi Apache Sling.

Cela signifie qu’un fichier .config correspondant doit être ajouté pour chaque environnement. Une configuration qui doit être appliquée à tous les environnements doit être indiquée dans tous ces fichiers. Si un seul environnement est concerné, elle est simplement indiquée dans ce fichier. Ce mécanisme garantit un contrôle total sur la configuration lue dans quel environnement.

Il est possible d’utiliser une autre propriété système pour détecter l’environnement. Spécification de la propriété système **com.day.cq.portet.configproperty** contenant le nom de la propriété système à utiliser au lieu de **com.day.cq.portet.config**.

#### Mise en cache et invalidation de la mise en cache {#caching-and-caching-invalidation}

Le portlet, dans sa configuration par défaut, met en cache les réponses qu’il reçoit d’AEM WCM dans un cache spécifique à l’utilisateur. Les caches doivent être annulés si des modifications sont apportées au contenu de l’instance de publication. À cet effet, un agent de réplication doit être configuré dans l’instance de création AEM WCM. Le cache peut également être vidé manuellement. Cette section décrit ces deux procédures.

Le portlet peut être configuré avec son propre cache, de sorte que le contenu dans le portlet s’affiche sans avoir à accéder à AEM. Le portail est disponible sous forme de contenu dans le répertoire /libs/portal/director. Pour accéder au contenu, démarrez une instance AEM et téléchargez le fichier de cet emplacement à l’aide de CRXDE Lite ou Webdav.

Vous pouvez déployer ce lot lors de l’exécution ou l’ajouter à l’application Web du portlet sous `WEB-INF/lib/resources/bundles` avant le déploiement.

Une fois le cache déployé, le portlet met en cache le contenu de l’instance de publication. Le cache du portlet peut être annulé en vidant le Dispatcher d’AEM. Pour configurer le portlet afin qu’il utilise son propre cache, procédez comme suit :

1. Configurez un agent de réplication dans l’auteur qui cible le serveur de portail.
1. Si le serveur du portail est exécuté sur **localhost**, **port 8080**, et que l’application Web du portlet AEM est montée dans le contexte **cqportlet**, l’adresse URL pour vider le cache de la console Web est `https://localhost:8080/cqportlet/cqbridge/cqpcache?Path=$(path)`. Utilisez la méthode GET.
   **Remarque :** au lieu d’utiliser un paramètre de demande, vous pouvez envoyer un en-tête HTTP appelé **Path**.

#### Purge du cache via l’agent de réplication {#flushing-the-cache-via-replication-agent}

Comme l’annulation normale de Dispatcher, un agent de réplication peut être configuré de manière à cibler le cache du portlet AEM du portail. Une fois que vous avez configuré l’agent de réplication, chaque activation de page régulière vide la mémoire cache du portail.

Si vous utilisez plusieurs noeuds de portail exécutant le portlet AEM, vous devez créer un agent pour chaque noeud, comme décrit dans cette procédure.

Pour configurer un agent de réplication pour le portail :

1. Connectez-vous à l’instance d’auteur.
1. Sur l’onglet Sites web, cliquez sur l’onglet *Outils*.
1. Cliquez sur **Nouvelle page...** dans le menu **Nouveau...** de l’agent de réplication.

   ![screen_shot_2012-02-15at40647pm](assets/screen_shot_2012-02-15at40647pm.png)

1. Dans *Modèle*, sélectionnez *Agent de réplication* et entrez un nom pour l’agent. Cliquez sur *Créer*.

   ![screen_shot_2012-02-15at40817pm](assets/screen_shot_2012-02-15at40817pm.png)

1. Double-cliquez sur l’agent de réplication que vous venez de créer. Il s’affiche comme non valide, car il n’a pas encore été configuré.

   ![screen_shot_2012-02-15at41001pm](assets/screen_shot_2012-02-15at41001pm.png)

1. Cliquez sur **Modifier**.
1. Sur l’onglet **Paramètres**, cochez la case **Activé**, sélectionnez le type de sérialisation **Vider Dispatcher**, puis saisissez un délai avant une nouvelle tentative (60 000, par exemple).

   ![screen_shot_2012-02-15at42101pm](assets/screen_shot_2012-02-15at42101pm.png)

1. Cliquez sur l’onglet **Transfert**.
1. Dans le champ **URI**, saisissez l’URI (URL) de vidage du portlet. L’URI est au format suivant :

   ```xml
   https://<wps-host>:<port>/<wps-context>/<cq5-portlet-context>/cqbridge/cqpcache
   ```

   ![screen_shot_2012-02-15at42322pm](assets/screen_shot_2012-02-15at42322pm.png)

1. Cliquez sur l’onglet **Étendu**.

   ![screen_shot_2012-02-15at42515pm](assets/screen_shot_2012-02-15at42515pm.png)

1. Dans la boîte de dialogue **Méthode HTTP**, saisissez **GET**.
1. Dans le champ **En-têtes HTTP**, cliquez sur **+** pour ajouter une nouvelle entrée, puis saisissez **Chemin d’accès : {path}**.
1. Si nécessaire, cliquez sur l’onglet **Proxy** et saisissez les informations du serveur proxy dans l’agent.
1. Pour enregistrer les modifications, cliquez sur **OK**.
1. Pour tester la connexion, cliquez sur le lien **Tester la connexion**. Un message du journal s’affiche et indique si le test de réplication a réussi. Par exemple :

   ![screen_shot_2012-02-15at42639pm](assets/screen_shot_2012-02-15at42639pm.png)

#### Purge manuelle du cache du portlet {#manually-flushing-the-portlet-cache}

Vous pouvez vider manuellement le cache du portlet en accédant à l’adresse URL configurée pour l’agent de réplication. Pour le format de l’adresse URL, voir [Vidage du cache](#flushing-the-cache-via-replication-agent). En outre, l’URL doit être étendue avec un paramètre d’URL Path=&lt;path> pour indiquer les éléments à vider.

Par exemple :

`https://10.0.20.99:10040/wps/PA_CQ5_Portlet/cqbridge/cqpcache?Path=*` vide le cache complet. `https://10.0.20.99:10040/wps/PA_CQ5_Portlet/cqbridge/cqpcache?Path=/content/mypage/xyz` vide `/content/mypage/xyz` du cache.

### Sécurité du portail {#portal-security}

Le portail est le mécanisme d’authentification principal. Vous pouvez vous connecter à AEM avec un utilisateur technique, un utilisateur du portail, un groupe et ainsi de suite. Le portlet n’a pas accès au mot de passe de l’utilisateur du portail. Par conséquent, si le portlet ne connaît pas toutes les informations d’identification pour connecter correctement un utilisateur, une solution de connexion unique doit être utilisée. Dans ce cas, le portlet AEM transfère toutes les informations nécessaires à AEM, qui les transfère à son tour au référentiel AEM sous-jacent. Ce comportement est enfichable et peut être personnalisé.

### Authentification lors de la publication {#authentication-on-publish}

Cette section décrit les modes d’authentification disponibles que le portlet peut utiliser pour communiquer avec les instances WCM d’AEM sous-jacentes.

Par défaut, aucune information de l’utilisateur n’est envoyée à l’instance de publication d’AEM. Le contenu s’affiche toujours en tant qu’utilisateur anonyme. Si des informations spécifiques à l’utilisateur doivent être diffusées à partir d’AEM ou si l’authentification de l’utilisateur pour la publication est requise, cette option doit être activée.

#### Accès à la configuration de l’authentification du portlet {#accessing-the-portlet-s-authentication-configuration}

Les options de configuration d’authentification que le portlet utilise dans AEM instances WCM sont disponibles dans la console web (configuration OSGi).

>[!NOTE]
>
>Lorsque vous utilisez AEM, plusieurs méthodes permettent de gérer les paramètres de configuration des services OSGi (noeuds de console ou de référentiel).
>
>Voir [Configuration d’OSGi](/help/sites-deploying/configuring-osgi.md) pour plus d’informations.

Pour accéder à la configuration d’authentification du portlet :

1. Accédez à la console Web à l’adresse suivante :

   `https://localhost:8080/cqportlet/cqbridge/system/console`

   Par exemple, dans sa configuration par défaut :

   `https://wps-host:10040/wps/PA_CQ5_Portlet/cqbridge/system/console`

1. Connectez-vous à la console Web. Les informations d’identification par défaut sont `admin/admin`.
1. Dans la console, sélectionnez **Configuration**.
1. Dans le menu **Configuration**, sélectionnez un service particulier à configurer. Les services sont fournis par le portlet dans la structure OSGi.

   | Nom du service | Description |
   |---|---|
   | Authentificateur Director Day Portal | Configurer le mode d’authentification utilisé pour les instances AEM WCM. En fonction du mode sélectionné, vous pouvez spécifier un utilisateur technique ou le nom du cookie de connexion unique. En outre, l’authentification pour AEM instances de publication WCM peut être activée. |
   | Cache du fichier Director du portail Day | Configurez les paramètres de la façon dont le portlet met en cache les réponses qu’il reçoit des instances de gestion de contenu web AEM. |
   | Service client HTTP Day Portal Director | Configurer la façon dont le portlet se connecte aux instances AEM WCM sous-jacentes via HTTP. Vous pouvez, par exemple, spécifier un serveur proxy. |
   | Gestionnaire de paramètres régionaux de Director Day Portal | Configurer les paramètres régionaux pris en charge par le portlet. Les demandes au niveau des instances de gestion de contenu Web AEM dépendent des paramètres régionaux de l’utilisateur. Par exemple, si la langue de l’utilisateur est *Allemand*, la demande sera `/content/geometrixx/de/`... |
   | Day Portal Director Privileger Manager | Indiquez si le portlet doit tester l’onglet Sites web en fonction de l’utilisateur actuellement connecté. |
   | Rendu de la barre d’outils Day Portal Director | Personnalisez le rendu de la barre d’outils du portlet. |

1. Vous pouvez également configurer la console web et le service de journalisation. Par exemple, vous pouvez modifier les informations d’identification de l’administrateur de la console web en cliquant sur le lien Console de gestion Apache Felix OSGi .

#### Mode Utilisateur technique {#technical-user-mode}

Dans le mode par défaut, toutes les demandes émises par le portlet pour l’instance de création AEM WCM sont authentifiées à l’aide du même utilisateur technique, indépendamment de l’utilisateur actuel du portail. Le mode Utilisateur technique est activé par défaut. Vous activez/désactivez ce mode dans l’écran de configuration correspondant de la console de gestion OSGi :

L’utilisateur technique spécifié doit exister sur l’instance de création de gestion de contenu Web AEM et sur l’instance de publication si l’option **S’authentifier lors de la publication** est activée. Veillez à accorder aux utilisateurs des privilèges d’accès suffisants pour leur travail de création.

#### SSO {#sso}

Le portlet prend en charge la connexion unique avec la version commerciale d’AEM. Le service d’authentification peut être configuré de manière à utiliser la connexion unique et transmettre à AEM l’utilisateur actuel du portail au format **De base** sous forme de cookie appelé « `cqpsso` ». AEM doit être configuré de manière à utiliser le gestionnaire d’authentification SSO pour le chemin d’accès /. Le nom du cookie doit lui aussi être configuré ici.

Le fichier `crx-quickstart/repository/repository.xml` du référentiel d’AEM doit être configuré en conséquence :

```xml
<LoginModule class="com.day.crx.security.authentication.CRXLoginModule">
  ...
  <param name="trust_credentials_attribute" value="TrustedInfo"/>
  <param name="anonymous_principal" value="anonymous"/>
</LoginModule>
```

#### Mode d’authentification SSO {#sso-authentication-mode}

Le portlet peut s’authentifier pour AEM WCM à l’aide du schéma de connexion unique (SSO). Dans ce mode, l’utilisateur actuellement connecté au portail est transféré à AEM WCM sous forme de cookie de connexion unique. Si le mode SSO est utilisé, tous les utilisateurs du portail ayant accès au portlet AEM doivent être connus au niveau des instances AEM WCM sous-jacentes, le plus souvent sous forme d’AEM WCM connecté au LDAP ou en ayant créé manuellement les utilisateurs à l’avance. De plus, avant d’activer la connexion unique dans le portlet, l’instance de création de gestion de contenu Web AEM sous-jacente (et l’instance de publication si l’option **S’authentifier lors de la publication** est activée) doit être configurée pour accepter les demandes basées sur l’authentification unique.

Pour configurer le portlet afin d’utiliser le mode d’authentification SSO, procédez comme suit (décrit en détail dans les sections suivantes) :

* Activez le référentiel d’AEM WCM pour accepter les informations d’identification approuvées.
* Activez l’authentification SSO dans la gestion de contenu web AEM.
* Activez l’authentification SSO dans le portlet AEM.

#### Activation du référentiel d’AEM WCM pour accepter les informations d’identification approuvées {#enabling-aem-wcm-s-repository-to-accept-trusted-credentials}

Avant de pouvoir activer la connexion unique pour AEM WCM, le référentiel sous-jacent doit être configuré de manière à accepter les informations d’identification approuvées fournies par AEM WCM. Pour ce faire, configurez AEM repository.xml.

1. Dans le système de fichiers où AEM WCM est installé, ouvrez le fichier suivant :

   `//crx-quickstart/repository/repository.xml`

1. Dans le fichier XML, recherchez l’entrée correspondant au **LoginModule** et ajoutez trust_credentials_attribute à sa configuration :

   ```xml
   <LoginModule class="com.day.crx.security.authentication.CRXLoginModule">
     ...
     <param name="trust_credentials_attribute" value="TrustedInfo"/>
     <param name="anonymous_principal" value="anonymous"/>
   </LoginModule>
   ```

1. Redémarrez AEM WCM pour que les modifications prennent effet.

#### Activation de l’authentification SSO dans AEM WCM {#enabling-sso-authentication-in-the-aem-wcm}

Pour activer l’authentification unique dans AEM WCM, accédez à l’entrée de configuration appropriée dans la console de gestion web Apache Felix (OSGi) d’AEM WCM :

1. Accédez à la console par le biais de son URI à l’adresse https://&lt;hôte-AEM>:&lt;port>/system/console.
1. Dans le menu Configuration, sélectionnez Gestionnaire d’authentification SSO. Dans cet exemple, le gestionnaire de connexion unique accepte des demandes de connexion unique de tous les chemins d’accès en fonction du cookie fourni par le portlet AEM. Votre configuration peut varier.

   | Chemin | / | Active le gestionnaire d’authentification unique pour toutes les requêtes |
   |---|---|---|
   | Noms de cookie | cqpsso | Nom du cookie fourni par le portlet tel que configuré dans la console OSGi du portlet. |

1. Cliquez sur **Enregistrer** pour activer la connexion unique. SSO est désormais le schéma d’authentification principal.

Pour chaque demande que reçoit AEM WCM, l’authentification SSO est tentée en premier. En cas d’échec, un système de secours du schéma d’authentification de base habituel est exécuté. Par conséquent, des connexions normales à AEM WCM sans SSO restent possibles.

#### Activation de l’authentification SSO dans un portlet AEM {#enabling-sso-authentication-in-a-aem-portlet}

Pour que cette instance de gestion de contenu Web AEM sous-jacente accepte des requêtes de connexion unique, le mode d’autorisation du portlet doit être défini non plus sur **Technique**, mais sur **Connexion unique**.

Pour activer l’authentification SSO dans un portlet AEM :

1. Accédez à la console par le biais de son URI à l’adresse https://&lt;hôte-AEM>:&lt;port>/system/console.
1. Dans le menu Configuration, sélectionnez Authentificateur Director Day Portal dans la liste des configurations disponibles.
1. Dans ce mode, sélectionnez Connexion unique. Conservez les valeurs par défaut des autres paramètres.

   ![chlimage_1-135](assets/chlimage_1-135.png)

1. Cliquez sur Enregistrer pour activer l’authentification unique pour le portlet.

   À des fins de test, accédez au portlet avec l’utilisateur administrateur de votre portail, après avoir créé le même utilisateur dans AEM WCM avec les privilèges d’administrateur.

Après avoir exécuté cette procédure, les demandes sont authentifiées à l’aide d’une connexion unique. Un fragment de code type provenant de la communication HTTP révèle la présence des en-têtes spécifiques SSO et Portlet suivants :

```xml
C-12-#001898 -> [GET /mynet/en/_jcr_content/par/textimage/image.img.png HTTP/1.1 ]
C-12-#001963 -> [cq5:locale: en ]
C-12-#001979 -> [cq5:used-locale: en ]
C-12-#002000 -> [cq5:locales: en,en_US ]
C-12-#002023 -> [cqp:user: wpadmin ]
C-12-#002042 -> [cqp:portal: IBM WebSphere Portal/6.1 ]
C-12-#002080 -> [cqp:windowid: 7_CGAH47L000CE302V2KFNOG0084 ]
C-12-#002124 -> [cqp:windowstate: normal ]
C-12-#002149 -> [cqp:portletmode: view ]
C-12-#002172 -> [User-Agent: Jakarta Commons-HttpClient/3.1 ]
C-12-#002216 -> [Host: 10.0.0.68:4502 ]
C-12-#002238 -> [Cookie: $Version=0; cqpsso=Basic+d3BhZG1pbg%3D%3D ]
C-12-#002289 -> [ ]
```

### Activation de l’authentification par code PIN {#enabling-pin-authentication}

Si vous n’utilisez pas les fonctionnalités de modification en ligne par défaut du portlet de contenu AEM, mais que vous souhaitez que la création et l’administration fassent partie du portlet en dehors du portail directement dans l’instance de création AEM, vous devez activer l’authentification par code personnel. Vous devez également modifier le paramétrage des boutons de gestion.

Pour afficher la page d’administration du site web ou modifier une page du portlet, le portlet de contenu AEM utilise la nouvelle authentification par code personnel. Par défaut, l’authentification par code PIN est désactivée. Par conséquent, les modifications de configuration suivantes doivent être apportées dans AEM :

1. Activez l’authentification approuvée dans AEM en ajoutant les informations de confiance dans le fichier repository.xml :

   ```xml
   <LoginModule class="com.day.crx.security.authentication.CRXLoginModule">
     ...
     <param name="trust_credentials_attribute" value="TrustedInfo"/>
   </LoginModule>
   ```

1. Dans la console de configuration OSGi, située par défaut à l’adresse https://localhost:4502/system/console/configMgr, sélectionnez **Gestionnaire d’authentification par code personnel CQ** dans le menu déroulant.
1. Modifiez la variable **Chemin racine de l’URL** pour contenir uniquement la valeur unique **/**.

### Autorisations {#privileges}

Certaines fonctions du portlet sont protégées par des autorisations. L’utilisateur actuel doit disposer de cette autorisation pour pouvoir accéder à cette fonction. Les autorisations ci-dessous sont prédéfinies :

* &quot;toolbar&quot; : il s’agit du privilège général d’afficher/utiliser la barre d’outils dans le portlet.
* &quot;prefs&quot; : si l’utilisateur dispose de ce privilège, il est autorisé à voir/modifier les préférences du portlet.
* &quot;cq-author:edit&quot; : avec ce privilège, l’utilisateur est autorisé à appeler la vue d’édition du contenu.
* &quot;cq-author:preview&quot; : avec ce privilège, l’utilisateur est autorisé à voir l’aperçu.
* &quot;cq-author:siteadmin&quot; : avec cette confidentialité, l’utilisateur est autorisé à ouvrir le siteadmin dans AEM.

La meilleure approche pour gérer les autorisations consiste à utiliser les rôles du portail et d’affecter des rôles à ces droits. Cette opération peut être effectuée par le biais d’une configuration OSGi. La configuration « Day Portal Director Privilege Manager » peut être configurée avec un ensemble de rôles pour chaque autorisation. Si l’utilisateur possède l’un des rôles, il dispose du privilège correspondant.

De plus, il est possible de définir cet accès en fonction des rôles pour chaque instance de portlet. La boîte de dialogue Préférences du portlet contient un champ de saisie pour chacune des autorisations ci-dessus. Pour chaque autorisation, il est possible de configurer une liste des rôles de portlet, séparés par des virgules. Si une valeur est configurée, elle remplace la configuration globale du service « Day Portal Director Privilege Manager », et il peut être nécessaire d’ajouter les mêmes rôles que dans ce paramètre global, car les rôles ne sont pas fusionnés. Si aucune valeur n’est spécifiée, la configuration globale est utilisée.

### Personnalisation de l’application AEM portlet {#customizing-the-aem-portlet-application}

L’application du portlet AEM indiquée lance un conteneur OSGi dans l’application web comme le fait AEM. Cette architecture vous permet d’utiliser tous les avantages d’OSGi :

* Facile à mettre à jour et à étendre
* Fourniture de mises à jour dynamiques dans le portlet sans intervention du serveur du portail
* Facile à personnaliser le portlet

### Boutons de la barre d’outils {#toolbar-buttons}

La barre d’outils et ses boutons peuvent être configurés et personnalisés. Vous pouvez ajouter vos propres boutons à la barre d’outils ou définir les boutons affichés dans les différents modes. Chaque bouton est un service OSGi configurable via une configuration OSGi.

La console web OSGi répertorie toutes les configurations de bouton sur l’onglet **Configuration**. Pour chaque bouton, vous pouvez choisir le mode dans lequel ce bouton s’affiche. Vous pouvez ainsi désactiver un bouton en supprimant tous les modes, par exemple.

Par défaut, le portlet de contenu AEM utilise la fonctionnalité de modification en ligne. Cependant, si vous préférez passer à l’instance de création AEM pour la modification, activez **Bouton SiteAdmin** et **Bouton ContentFinder**, mais désactivez **Bouton Modifier**. Dans ce cas, veillez à configurer correctement l’authentification par code personnel dans AEM.

La mise en page de la barre d’outils du portlet peut être personnalisée en installant un bundle via la console web Felix du portlet, qui contient un CSS/HTML personnalisé à un emplacement prédéfini.

#### Structure du lot {#bundle-structure}

Voici un exemple de structure de regroupement :

```xml
$ jar tvf target/toolbarlayout-0.0.1-SNAPSHOT.jar | awk '{print $8}'
META-INF/
META-INF/MANIFEST.MF
/com/day/cq/portlet/toolbar/layout/
/com/day/cq/portlet/toolbar/layout/author.gif
/com/day/cq/portlet/toolbar/layout/back.gif
/com/day/cq/portlet/toolbar/layout/button.html
/com/day/cq/portlet/toolbar/layout/edit.gif
/com/day/cq/portlet/toolbar/layout/manage.html
/com/day/cq/portlet/toolbar/layout/publish.html
/com/day/cq/portlet/toolbar/layout/refresh.gif
/com/day/cq/portlet/toolbar/layout/siteadmin.gif
/com/day/cq/portlet/toolbar/layout/toolbar.css
```

Le dossier META-INF contient le fichier MANIFEST.MF nécessaire à OSGi afin de l’identifier comme lot. Il se présente comme suit :

```xml
Manifest-Version: 1.0
Built-By: djaeggi
Created-By: Apache Maven Bundle Plugin
Import-Package: com.day.cq.portlet.toolbar.layout
Bnd-LastModified: 1234178347159
Export-Package: com.day.cq.portlet.toolbar.layout
Bundle-Version: 0.0.1.SNAPSHOT
Bundle-Name: Company CQ5 Portal Director Portlet Toolbar Layout
Bundle-Description: This bundle provides a custom layout for the CQ5 P
 ortal Director Portlet Toolbar.
Build-Jdk: 1.5.0_16
Bundle-ManifestVersion: 2
Bundle-SymbolicName: com.day.cq.portlet.company.toolbarlayout
Tool: Bnd-0.0.255
```

La présence du répertoire HTML/CSS/images dans le dossier /com/day/cq/portlet/toolbar/layout est déterminée par le portlet et ne peut pas être modifiée. De même, les en-têtes Import-Package et Export-Package du fichier MANIFEST.MF doivent être appelés eux aussi dans le dossier /com/day/cq/portlet/toolbar/layout. Bundle-SymbolicName doit être un nom de package complet unique.

Vous pouvez le créer à l’aide d’un outil tel que maven ou créer manuellement un fichier jar avec l’en-tête correspondant défini, comme illustré dans cette section.

#### Vues de la barre d’outils du portlet {#portlet-toolbar-views}

La barre d’outils du portlet comporte deux états d’affichage. Chaque vue et les boutons associés peuvent être personnalisés avec un fichier de HTML correspondant.

#### Mode Publication {#publish-view}

L’affichage Publication ne comporte qu’un seul bouton, qui permet d’afficher/de masquer la barre d’outils dans l’affichage Gestion. L’affichage Publication est représenté par le fichier publish.html dans le [lot précédent](/help/sites-deploying/configuring-osgi.md#bundles). Dans le HTML, vous pouvez utiliser les espaces réservés suivants, qui sont remplacés par le portlet par le contenu correspondant lors du rendu :

#### Espaces réservés de la vue Publication {#publish-view-placeholders}

| Chaîne de l’espace réservé | Description |
|---|---|
| {buttonManage} | L’espace réservé est remplacé par le bouton **Gérer** qui change le statut du portlet et le fait passer en statut de gestion. |

#### Gérer l’affichage {#manage-view}

L’affichage Gestion comporte quatre boutons : Modifier, onglet Sites web, Actualiser et Précédent. L’affichage Gestion est représenté par le fichier manage.html dans le [lot précédent](/help/sites-deploying/configuring-osgi.md#bundles). Dans le HTML, vous pouvez utiliser les espaces réservés suivants, qui sont remplacés par le portlet par le contenu correspondant lors du rendu :

#### Gérer les espaces réservés d’affichage {#manage-view-placeholders}

| Chaîne de l’espace réservé | Description |
|---|---|
| {buttonEdit} | L’espace réservé est remplacé par le bouton **Modifier**, qui affiche une nouvelle fenêtre contenant la page active en mode d’édition dans AEM. |
| {buttonWebsites tab} | Espace réservé, remplacé par un bouton qui ouvre l’onglet Sites web d’AEM WCM. |
| {buttonRefresh} | Actualise la vue actuelle. |
| {buttonBack} | Replace le portlet dans la vue de publication. |

#### Boutons {#buttons}

Les boutons, quelle que soit la vue qu’ils affichent, utilisent le même HTML commun, défini dans button.html.

Dans le HTML, vous pouvez utiliser les espaces réservés suivants, qui sont remplacés par le portlet par le contenu correspondant lors du rendu :

#### Boutons Gestion et publication {#manage-and-publish-view-buttons}

| Chaîne de l’espace réservé | Description |
|---|---|
| {name} | Nom du bouton, par exemple **auteur, précédent, actualiser**, etc. |
| {id} | Identifiant CSS du bouton. |
| {url} | URL de la cible du bouton. |
| {text} | Libellé du bouton. |
| {onclick} | JavaScript **onclick** fonction (contains {url}). |

Exemple de fichier button.html :

```xml
<div class="cqp_button">

 <a href="#" onclick="{onclick}">

 <img src="/wps/PA_CQ5_Portlet/cqbridge/static/{id}.gif" alt="{text}"
title="{text}"/>

 </a>
</div>
```

#### Installation d’une disposition personnalisée {#installing-a-custom-layout}

Pour installer une mise en page personnalisée, accédez à la section **Lots** de la console Web OSGI du portlet et chargez le lot.

#### Packages {#packages}

Si vous devez charger ou créer des packages pour votre installation, consultez Gestionnaire de packages dans la documentation d’AEM pour obtenir des instructions détaillées.

### Gestion des liens {#link-handling}

Tous les liens sont réécrits afin de fonctionner dans le contexte du portail. Par défaut, ce sont les liens avec des paramètres de rendu qui sont utilisés. Il est possible de configurer le module de réécriture de HTMLS de Portal Director pour qu’il utilise des liens d’action à la place.

Vous pouvez également définir d’autres paramètres de demande qui peuvent faire l’objet d’une requête pour le chemin d’accès au contenu à afficher. Cette fonction est utile, par exemple, s’il y a un lien de l’extérieur vers du contenu spécifique.

De plus, le service Portal Director HTML Rewriter peut être configuré avec une liste d’exclusions définies par des expressions régulières pour la réécriture des liens. Par exemple, s’il y a des liens relatifs vers des systèmes externes, vous devez les ajouter à cette liste d’exclusions.

### Localisation {#localization}

Le portlet de contenu d’AEM dispose d’une fonction de localisation intégrée, qui garantit que le contenu d’AEM est dans la langue correcte.

Pour ce faire, deux étapes sont nécessaires :

1. Le service Portal Directory Locale Detector détecte les paramètres régionaux du portail en extrayant le paramètre des paramètres régionaux du portail. Ce service doit être configuré avec la liste des langues disponibles dans AEM.
1. Le service Portal Director Locale Handler gère la localisation de la demande actuelle. Il utilise le chemin d’accès au contenu demandé, par exemple, `/content/geometrixx/en/company.html`, et conformément à la configuration, il remplace les paramètres régionaux **en** par les paramètres régionaux de l’utilisateur.

Le service Portal Director Locale Handler peut être configuré avec les chemins d’accès pour vérifier les informations des paramètres régionaux, qui incluent généralement tout ce qui se trouve sous `/content` et avec la position des informations des paramètres régionaux dans le chemin d’accès. Par défaut, le gestionnaire des paramètres régionaux suit la recommandation de structure des sites multilingues dans AEM.

Si votre site ne comporte pas de règle absolue pour gérer les informations des paramètres régionaux avec le chemin d’accès, il est possible de remplacer le gestionnaire des paramètres régionaux par votre propre mise en œuvre.

### Services OSGi facultatifs {#optional-osgi-services}

Des services OSGi facultatifs peuvent être mis en œuvre pour personnaliser différentes parties du portlet. Chaque service correspond à une interface Java. Cette interface peut être mise en œuvre et déployée par le biais d’un lot dans le portlet.

<table>
 <tbody>
  <tr>
   <td>RequestTracker</td>
   <td>Le suivi des demandes reçoit une notification chaque fois que le contenu s’affiche dans le portlet. Vous pouvez ainsi effectuer le suivi des appels du portlet.</td>
  </tr>
  <tr>
   <td>InvocationContextListener</td>
   <td>Programme d’écoute appelé au début et à la fin de chaque demande adressée au portlet. L’écouteur peut être utilisé pour modifier ou ajouter des informations pour la requête actuelle.<br /> </td>
  </tr>
  <tr>
   <td>ErrorHandler</td>
   <td>Gestionnaire d’erreurs personnalisé pour les erreurs pendant la phase de rendu.</td>
  </tr>
  <tr>
   <td>HttpProcessor</td>
   <td>Ce service peut être utilisé pour ajouter des informations à chaque appel http à AEM.</td>
  </tr>
  <tr>
   <td>PortletAction</td>
   <td>Ajoutez une action propre au portlet. Cette action peut être appelée à l’aide d’un lien d’action de portlet.</td>
  </tr>
  <tr>
   <td>PortletDecoratorService</td>
   <td>Ce service peut être utilisé pour décorer le contenu du portlet.</td>
  </tr>
  <tr>
   <td>ResourceProvider</td>
   <td>Ajoutez votre propre fournisseur de ressources pour fournir une ressource via un lien vers le client via une ressource de portlet.</td>
  </tr>
  <tr>
   <td>TextMapper</td>
   <td>Permet de post-traiter des fichiers de HTML, CSS et JavaScript.</td>
  </tr>
  <tr>
   <td>ToolbarButton</td>
   <td>Ajoutez votre propre bouton à la barre d’outils.</td>
  </tr>
  <tr>
   <td>UrlMapper</td>
   <td>Ajoutez un service pour appliquer un mapping ou une réécriture d’URL personnalisée.</td>
  </tr>
  <tr>
   <td>UserInfoProvider</td>
   <td>Ajoutez vos propres informations sur l’utilisateur. Ce service peut être utilisé pour obtenir des informations du portail vers le portlet.</td>
  </tr>
 </tbody>
</table>

#### Remplacement des services par défaut {#replacing-default-services}

Les services ci-dessous possèdent une mise en œuvre par défaut dans le portlet de contenu (grâce à une interface Java correspondante). Pour personnaliser, un lot contenant la nouvelle mise en oeuvre du service doit être déployé dans l’application du portlet.

En mettant en œuvre ce service, veillez à définir la propriété **service.ranking** du service sur une valeur positive. La mise en œuvre par défaut utilise le classement **0**, et le portlet utilise le service avec le classement le plus élevé.

| **Nom** | **Description** | **Comportement par défaut** |
|---|---|---|
| Authentificateur | Fournit les informations d’authentification à AEM | Utilise un utilisateur technique configurable pour la création et la publication. Ou SSO peut être utilisé. |
| HTMLRewriter | Réécrit les liens, les images, etc. | Réécrit AEM liens vers des liens de portail, peut être étendu par un UrlMapper et un TextMapper. |
| HttpClientService | Gère toutes les connexions http | Mise en oeuvre standard |
| LocaleHandler | Gestion des informations sur les paramètres régionaux | Réécrit un lien vers le contenu par rapport aux paramètres régionaux. |
| LocaleDetector | Détecte les paramètres régionaux de l’utilisateur. | Utilise les paramètres régionaux fournis par le portail. |
| PrivilegeManager | Vérifie les droits des utilisateurs | Vérifie l’accès à l’instance d’auteur si l’utilisateur est autorisé à modifier le contenu |
| ToolbarRenderer | Rendu de la barre d’outils | Ajoute une fonctionnalité de barre d’outils. |

### Événements de portlet {#portlet-events}

L’API de portlet (JSR-286) spécifie les événements de portlet. Le portlet de contenu d’AEM dispose d’un pont intégré, qui distribue les événements de portlet pour le portlet AEM en tant qu’événements OSGi. Cela rend la gestion des événements de portlet enfichable.

Si vous souhaitez gérer des événements spécifiques, déclarez-les comme événements de réception dans le descripteur de déploiement (ou configurez-le via votre serveur de portail) et mettez en oeuvre un service OSGi déclarant l’interface EventHandler (voir la spécification OSGi EventAdmin).

Chaque fois qu’un événement de portlet se produit, un événement OSGi spécifique est envoyé pour appeler le gestionnaire. Le gestionnaire extrait toutes les informations contextuelles et peut mettre à jour le statut du portlet en conséquence ou envoyer de nouveaux événements. Essentiellement, dans la méthode handle, toutes les fonctionnalités de la phase d’événement de portlet peuvent être utilisées.

## Utilisation d’AEM comme portail {#using-aem-as-a-portal}

Utilisez le composant Portlet pour ajouter des fenêtres de portlet à des pages AEM. Les bibliothèques partagées que vous installez sur le serveur d’applications permettent au composant Portlet de détecter les applications de portlet déployées.

Pour utiliser AEM comme portail, effectuez les tâches suivantes :

1. Installez le composant Portlet et les bibliothèques partagées.
1. Ajoutez le composant Portlet à Sidekick.
1. Configurez et déployez l’application web qui contient les portlets que vous souhaitez afficher dans le composant Portal.
1. Ajoutez le composant Portlet à une page et sélectionnez le portlet à afficher.

>[!NOTE]
>
>Vous ne pouvez utiliser le composant Portlet que lorsque AEM est déployé comme application web. ([Voir Installation d’AEM avec un serveur d’applications](/help/sites-deploying/application-server-install.md).)

### Installation du composant Portlet {#installing-the-portlet-component}

Le fichier JAR d’AEM Quickstart contient les fichiers du composant Portlet. Pour obtenir les fichiers (cq-portlet-components.zip), vous pouvez exécuter Quickstart ou extraire le contenu.

1. Exécutez ou extrayez le contenu du fichier JAR de Quickstart et recherchez le fichier cq-portlet-components.zip en conséquence :

   * Exécutez Quickstart : crx-quickstart/opt/portal
   * Extraire le contenu Quickstart : static/opt/portal

1. Ouvrez le Gestionnaire de packages de l’instance de création CQ5 déployée sur le serveur d’applications. (https://*appserverhost*:*port*/cq5author/crx/packmgr)

1. Utilisez le Gestionnaire de packages pour [charger et installer](/help/sites-administering/package-manager.md#uploading-packages-from-your-file-system) le package cq-portlets-components.zip.

   Le package installe cq-portlet-director-sharedlibs-x.x.x.jar dans le dossier /libs/portal/director dans le référentiel.

1. Copiez cq-portlet-director-sharedlibs-x.x.x.jar sur votre disque dur. Utilisez tous les moyens pour obtenir le fichier, par exemple FileVault ou un client WebDAV.
1. Déplacez le fichier cq-portlet-director-sharedlibs.x.x.x.jar vers le dossier de bibliothèque partagée de votre serveur d’applications afin que les classes soient disponibles pour les applications de portlet déployées.

### Ajout du composant Portlet au Sidekick {#adding-the-portlet-component-to-sidekick}

Ajoutez le composant Portlet au système de paragraphes afin qu’il soit disponible pour les auteurs.

1. Dans le Sidekick, cliquez sur l’icône en forme de règle pour accéder au mode Conception.
1. À côté du titre `Design of par`, au-dessus du premier paragraphe, cliquez sur **Modifier**.

1. Dans la catégorie de composants **Général**, cochez la case en regard du composant Portlet et cliquez sur OK.

![chlimage_1-25](assets/chlimage_1-25.jpeg)

### Configuration et déploiement des applications de portlet {#configuring-and-deploying-your-portlet-applications}

Déployez les portlets dans le conteneur web du serveur d’applications afin qu’ils soient disponibles dans le composant Portail. Avant de déployer l’application de portlet, vous devez configurer l’application afin qu’elle charge le servlet du conteneur de portail d’AEM. Cette configuration permet au composant Portlet d’accéder aux portlets.

1. Extrayez le contenu du fichier WAR de l’application du portlet.

   **Conseil :** la commande jar xf *nomapp*.war extrait les fichiers.

1. Ouvrez le fichier Web.xml dans un éditeur de texte.
1. Ajoutez la configuration de servlet ci-dessous dans l’élément Web-app :

   ```xml
   <servlet>
           <servlet-name>slingportal</servlet-name>
           <servlet-class>org.apache.sling.portal.container.api.ContainerServlet</servlet-class>
           <load-on-startup>1</load-on-startup>
   </servlet>
   <servlet-mapping>
           <servlet-name>slingportal</servlet-name>
           <url-pattern>/SlingPortletInvoker</url-pattern>
   </servlet-mapping>
   ```

1. Enregistrez le fichier Web.xml et recompressez le fichier WAR.

   **Conseil :** la commande `jar cvf nameofapp.war *` ajoute le contenu du répertoire actif au fichier nomapp.war.

1. Déployez l’application de portlet sur le serveur d’applications. Pour plus d’informations, consultez la documentation de votre serveur d’applications.

### Ajout de portlets à votre page AEM {#adding-portlets-to-your-aem-page}

Utilisez le composant Portail pour ajouter une fenêtre du portlet à votre page web. Utilisez les propriétés du composant pour spécifier le portlet à afficher.

1. Sur la page web, faites glisser le **Portlet** du groupe Général en Sidekick vers la page.

   >[!NOTE]
   >
   >Après avoir fait glisser le composant sur la page, rechargez la page pour vous assurer qu’elle fonctionne correctement.

1. Double-cliquez sur le composant pour ouvrir les propriétés Portlet.
1. Dans le **Entité de portlet** , sélectionnez le portlet dans la liste.
1. Cochez ou désélectionnez la case **Masquer la barre de titre** selon si vous souhaitez afficher la barre de titre du portlet ou non.
1. Dans le **Fenêtre de portlet** , saisissez un ID de fenêtre de portlet unique, le cas échéant.

   >[!NOTE]
   >
   >Si vous prévoyez d’utiliser plusieurs fois le même portlet sur la même page, attribuez à chaque portlet un identifiant de fenêtre différent.

1. Cliquez sur **OK**. Le portlet s’affiche sur votre page AEM.

   ![chlimage_1-136](assets/chlimage_1-136.png)

## Installation, configuration et utilisation d’AEM dans un portlet {#installing-configuring-and-using-aem-in-a-portlet}

Pour accéder au contenu fourni par AEM WCM, le serveur du portail peut disposer d’AEM Portal Director Portlet. Pour ce faire, installez, configurez et ajoutez le portlet à la page du portail à l’aide des étapes fournies dans cette section.

Par défaut, le portlet se connecte à l’instance de publication sur localhost 4503 et l’instance de création sur locahost 4502. Ces valeurs peuvent être modifiées lors du déploiement du portlet. Portal Director est disponible sous forme de contenu dans le référentiel, sous /libs/portal/directory. Avant de l’utiliser, vous devez télécharger le fichier WAR de l’application.

### Téléchargement du fichier WAR {#downloading-the-war-file}

1. À l’aide de WebDAV ou CRXDE Lite, accédez à /libs/portal/director.

1. Téléchargez *cq-portlet-Webapp.war*.

>[!NOTE]
>
>Ces procédures utilisent le portail WebSphere à titre d’exemple même si elles sont aussi génériques que possible. N’oubliez pas que les procédures varient pour les autres portails web. Bien que les étapes soient essentiellement identiques pour tous les portails web, vous devez redéfinir les étapes de votre portail web spécifique.

#### Installation du portlet {#installing-the-portlet}

Pour installer le portlet :

1. Connectez-vous au portail avec les privilèges d’administrateur.
1. Accédez à la partie Gestion de portlet de votre portail web.
1. Cliquez sur Installer et accédez à l’application AEM portlet (cq-portlet-webapp.war) que vous avez téléchargée, puis saisissez d’autres informations importantes sur le portlet.

   Pour obtenir des informations essentielles sur le portlet, vous pouvez accepter les valeurs par défaut ou modifier les valeurs. Si vous acceptez les valeurs par défaut, le portlet est disponible à l’adresse suivante : https://&lt;wps-host>:&lt;port>/wps/PA_CQ5_Portlet. La console d’administration OSGi fournie par le portlet est disponible à l’emplacement https://&lt;wps-host>:&lt;port>/wps/ PA_CQ5_Portlet/cqbridge/system/console (la paire nom d’utilisateur/mot de passe est admin/admin).

1. Assurez-vous que l’application de portlet démarre automatiquement en sélectionnant cette option ou en cochant la case, puis enregistrez vos modifications. Un message s’affiche indiquant que l’installation a réussi.

#### Configuration du portlet {#configuring-the-portlet}

Une fois que vous avez installé le portlet, vous devez le configurer afin qu’il connaisse les adresses URL des instances AEM sous-jacentes (création et publication). Vous pouvez également configurer d’autres options.

Pour configurer le portlet :

1. Dans la fenêtre d’administration du portail du serveur d’applications, accédez à la gestion des portlets, où tous les portlets sont répertoriés et sélectionnez le portlet Director d’AEM Portal.
1. Configurez le portlet, au besoin. Par exemple, vous pouvez avoir besoin de modifier l’adresse URL pour les instances de création et de publication et l’adresse URL du chemin d’accès de début. Les configurations par défaut sont décrites dans la section [Préférences de portlet](/help/sites-administering/aem-as-portal.md#portlet-preferences).

   >[!NOTE]
   >
   >Si le portlet est configuré pour se connecter à AEM instances de création et de publication qui s’exécutent sur un chemin de contexte différent de** /**, vous devez activer la force **CQUrlInfo** dans la configuration du Gestionnaire de bibliothèques Html de ces instances AEM (par exemple, via la console web Felix) ou la modification ne fonctionnera pas et la boîte de dialogue Préférences ne s’affichera pas.

1. Enregistrez les modifications apportées à la configuration sur le serveur d’applications.

1. Accédez à la console d’administration OSGi pour le portlet. L’emplacement par défaut est `https://<wps-host>:<port>/wps/PA_CQ5_Portlet/cqbridge/system/console/configMgr`. La paire nom d’utilisateur/mot de passe est par défaut **admin/admin**.

1. Sélectionnez la variable **Configuration du serveur Day Portal Director CQ** et modifiez les valeurs suivantes :

   * **URL de base de création**: URL de base de l’instance d’auteur AEM.
   * **Publier l’URL de base**: URL de base de l’instance de publication AEM.
   * **Création utilisée comme publication** : l’instance de création est-elle utilisée comme instance de publication (pour le développement) ?

   ![chlimage_1-137](assets/chlimage_1-137.png)

1. Cliquez sur **Enregistrer**. Vous pouvez maintenant ajouter le portlet aux pages du portail et utiliser le portail.

### URL de contenu {#content-urls}

Lorsque le contenu est demandé à partir d’AEM, le portlet utilise le mode d’affichage actuel (publication ou création) et le chemin d’accès actuel pour assembler une adresse URL complète. Avec les valeurs par défaut, la première adresse URL est `https://localhost:4503/content/geometrixx/en.portlet.html`. La valeur de la propriété `htmlSelector` est ajoutée automatiquement à l’adresse URL avant l’extension.

Si le portlet passe en mode Aide et que `appendHelpViewModeAsSelector` est sélectionné, le sélecteur `help` est lui aussi ajouté, par exemple, `https://localhost:4503/content/geometrixx/en.portlet.html.help`. Si la fenêtre du portlet est agrandie et que `appendMaxWindowStateAsSelector` est sélectionné, le sélecteur est lui aussi ajouté, par exemple, `https://localhost:4503/content/geometrixx/en.portlet.max.help`.

Les sélecteurs peuvent être évalués dans AEM et un modèle différent peut être utilisé pour différents sélecteurs.

### Utilisation d’une carte d’URL de contenu dans AEM {#using-a-content-url-map-in-aem}

Généralement, le chemin d’accès de début pointe directement vers le contenu dans AEM. Cependant, si vous voulez conserver les chemins d’accès de début dans AEM plutôt que dans les préférences de portlet, vous pouvez faire pointer le chemin d’accès de début vers une correspondance de contenu dans AEM, comme `/var/portlets`. Dans ce cas, un script exécuté dans AEM peut utiliser les informations envoyées à partir du portlet pour déterminer l’adresse URL qui est l’adresse URL de début. Il doit émettre une redirection vers la bonne URL.

#### Ajout du portlet à la page du portail {#adding-the-portlet-to-the-portal-page}

Pour ajouter le portlet à la page de portail :

1. Assurez-vous que vous êtes dans la fenêtre administration du serveur d’applications et accédez à l’emplacement de gestion des pages. (par exemple, dans WebSphere 6.1, cliquez sur **Gestion des pages**).
1. Sélectionnez le nom dans le portlet, puis sélectionnez une page existante ou créez-en une.
1. Modifiez la mise en page.
1. Sélectionnez le portlet et ajoutez-le à un conteneur.
1. Enregistrez vos modifications.

#### Utilisation du portlet {#using-the-portlet}

Pour accéder à la page que vous avez ajoutée au portlet :

1. Dans le menu de personnalisation du portlet, configurez le portlet tel que vous l’avez configuré dans le portail.
1. Ouvrez la configuration (le portlet affiche l’URL de début de publication configurée dans la configuration du portlet), apportez les modifications nécessaires, puis enregistrez-les.
