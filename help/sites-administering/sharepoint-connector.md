---
title: SharePoint Connector
description: Day JCR Connector for Microsoft SharePoint 2010 et Microsoft SharePoint 2013, version 4.0.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: 10ea7d2e-6e44-4d5c-a2b2-63c73b18f172
feature: Integration
role: Admin
source-git-commit: c4133584e9c2328b3a55042902c67770d78afcf7
workflow-type: ht
source-wordcount: '1482'
ht-degree: 100%

---

# SharePoint Connector{#sharepoint-connector}

Cet article comprend des détails relatifs au connecteur JCR Adobe pour Microsoft SharePoint 2010 et Microsoft SharePoint 2013, version 4.0.

SharePoint Connector prend en charge les fonctionnalités de base suivantes :

* la lecture de contenu et de métadonnées dans SharePoint ;
* la reconnaissance des paramètres de sécurité SharePoint pour le contenu consulté en appliquant l’authentification et l’autorisation SharePoint natives ;
* l’intégration de contenu à l’aide de Content Finder ;
* l’utilisation de composants AEM, tels que Ressource externe pour afficher des images et des vidéos SharePoint ;
* la synchronisation de SharePoint avec AEM Assets ;

Toutes les fonctionnalités sont implémentées à l’aide des services web SharePoint natifs comme interface de contenu et de services SharePoint.

>[!NOTE]
>
>SharePoint Connector est également pris en charge avec le pack de services 2 d’AEM 6.1. Le connecteur ne prend plus en charge le montage de référentiel virtuel et, par conséquent, il ne peut pas être monté. Si vous souhaitez accéder au référentiel SharePoint à l’aide des API Java, utilisez une mise en œuvre de référentiel JCR de SharePoint Connector dans votre projet.
>
>L’installation, la configuration, la gestion et les opérations informatiques du serveur SharePoint et de l’infrastructure informatique associée ne rentrent pas dans le cadre de ce document. Consultez la documentation du fournisseur relative à [SharePoint](https://www.microsoft.com/sharepoint) pour plus d’informations sur ces sujets. Le connecteur nécessite que ces parties de l’infrastructure soient correctement installées, configurées et utilisées.
>

## Prise en main {#getting-started}

Pour commencer à utiliser le connecteur, procédez comme suit :

* Assurez-vous de disposer au moins de Java 7.
* Téléchargez le fichier de distribution du package de connecteur depuis la Distribution logicielle.
* Copiez un fichier valide *license.properties* dans le répertoire contenant le fichier *cq-quickstart-6.4.0.jar*.

* Double-cliquez sur le fichier .jar pour démarrer AEM, ou démarrez-le à partir de la ligne de commande.
* Installez le package du connecteur depuis le Gestionnaire de modules.
* Configurez les options du connecteur.

## Installation de SharePoint Connector {#installing-sharepoint-connector}

Le connecteur est un package de contenu qui facilite la configuration. Installez le package à l’aide du gestionnaire de packages, puis définissez l’URL du serveur SharePoint, ainsi que les autres options de configuration. Le contenu SharePoint est disponible dans le référentiel AEM.

### Configuration requise {#installation-requirements}

Le connecteur requiert les éléments suivants :

* Java Runtime Environment 1.7 ou version ultérieure
* Services web SharePoint disponibles via le réseau
* URL du serveur SharePoint
* Informations d’identification et autorisations de l’utilisateur pour les référentiels CRX et SharePoint
* [Plateformes prises en charge](#supported-platforms)

SharePoint Connector est disponible en téléchargement à partir de la [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/featurepack/cq-6.3.0-featurepack-17673).

### Plateformes prises en charge {#supported-platforms}

Le connecteur prend en charge les éléments suivants :

* Versions d’AEM :

   * AEM 6.4, 6.3

* Versions de Microsoft SharePoint :

   * Microsoft Office SharePoint Server (MOSS) 2010
   * Microsoft Office SharePoint Server (MOSS) 2013

* Si vous avez besoin d’assistance pour les déploiements personnalisés du connecteur (OEM, exigences spéciales, méthodes d’authentification personnalisées), contactez le bureau d’Adobe de votre région.

>[!NOTE]
>
>Le connecteur ne prend en charge que les configurations officiellement prises en charge par Microsoft. Consultez les configurations système requises pour [MOSS 2010](https://technet.microsoft.com/en-us/library/cc262485(office.14).aspx) et [MOSS 2013](https://technet.microsoft.com/en-us/library/cc262485.aspx).

### Installation standard {#standard-installation}

La Distribution logicielle est utilisé pour la distribution des fonctionnalités produit, des exemples et des correctifs logiciels. Pour plus d’informations, consultez la [Documentation sur la Distribution logicielle](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html?lang=fr#software-distribution).


#### Intégration à AEM {#integrating-with-aem}

Pour installer le package de contenu connecteur.

1. Ouvrez un ticket d’assistance Adobe pour demander le package de fonctionnalités du connecteur.
1. Téléchargez le package lorsqu’il est disponible, puis ouvrez le gestionnaire de modules de votre instance AEM.
1. Cliquez sur **Installer** sur la page de description du package.
1. Dans la boîte de dialogue **Installer le package**, cliquez sur **Installer**.

   **Remarque** : assurez-vous d’être connecté en tant qu’administrateur ou administratrice.

1. Lorsque le package est installé, cliquez sur **Fermer**.

## Configuration de SharePoint Connector {#configuring-sharepoint-connector}

Une fois que vous avez installé SharePoint Connector, configurez l’application et les couches SharePoint pour le connecteur.

Définissez l’URL du serveur SharePoint pour rendre votre référentiel SharePoint conforme à JCR. Vous pouvez définir des paramètres supplémentaires pour configurer la connexion au serveur SharePoint. Configurez également l’authentification avec le connecteur SharePoint.

### Configuration de la connexion au serveur SharePoint {#configuring-the-connection-with-the-sharepoint-server}

Pour définir l’URL du serveur SharePoint et les options avancées, procédez comme suit :

1. Accédez à la console de gestion OSGi : [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr).
1. Recherchez le lot **Connecteur JCR Day pour Microsoft SharePoint**.
1. Modifiez les valeurs de configuration.
1. Définissez l’URL de SharePoint Server comme valeur des **Espaces de travail**.
1. Cliquez sur **Enregistrer**.

![chlimage_1-62](assets/chlimage_1-62.png)

Paramètres « Espaces de travail » et « Nom de l’espace de travail par défaut » :

Par défaut, le connecteur expose un espace de travail JCR unique. Le SharePoint Server exposé par cet espace de travail est défini via le paramètre de configuration « URL de SharePoint Server ».

Le connecteur peut également être configuré pour plusieurs espaces de travail. Dans ce cas, chaque espace de travail est associé à l’URL du serveur SharePoint correspondant qui est exposé par l’espace de travail. Pour ajouter un espace de travail, ajoutez une définition d’espace de travail au paramètre Espaces de travail. La définition d’espace de travail présente le format suivant :
`<name>`= `<url>` où
`<name>` est le nom de l’espace de travail JCR, et
`<url>` est l’URL du serveur SharePoint pour cet espace de travail.

Dans AEM, effectuez une étape en plus des étapes de configuration ci-dessus. Ajoutez dans la liste autorisée le lot ’**com.day.cq.dam.cq-dam-jcr-connectors**’.

Pour placer les lots en liste autorisée dans AEM, effectuez les étapes suivantes :

1. Accédez à la console de gestion OSGi : http://localhost:4502/system/console/configMgr.
1. Recherchez le service Liste autorisée d’administration des connexions Apache Sling.
1. Sélectionnez **Contourner la liste autorisée**.
1. Ajoutez `com.day.cq.dam.cq-dam-jcr-connectors` dans la liste autorisée des lots par défaut.
1. Cliquez sur Enregistrer.

![chlimage_1-82](assets/chlimage_1-82a.png)

>[!NOTE]
>
>Si vous configurez plusieurs espaces de travail, indiquez le nom de l’espace de travail par défaut dans le paramètre du nom d’espace de travail par défaut.

Pour plus d’informations sur les paramètres associés à l’authentification, consultez la section [Authentification](/help/sites-administering/sharepoint-connector.md#configuring-authentication).

### Vérifier la configuration de SharePoint {#verifying-the-sharepoint-setup}

Après avoir configuré le connecteur, vérifiez les éléments suivants :

* Le serveur SharePoint s’exécute et les services web sont accessibles à l’instance de connecteur.
* Les informations d’identification de l’utilisateur ou de l’utilisatrice SharePoint sont valides et la personne dispose des autorisations SharePoint nécessaires.
* Le connecteur est installé et configuré correctement.

### Configurer la synchronisation DAM avec le serveur SharePoint {#configuring-dam-sync-with-the-sharepoint-server}

Pour synchroniser les ressources SharePoint avec AEM, procédez comme suit :

1. Accédez à la console de gestion OSGi : [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr).
1. Recherchez le service « Default DAMAssetSynchronization ».
1. Modifiez les valeurs de configuration.
1. Définissez le nom d’utilisateur ou d’utilisatrice et le mot de passe correspondant de la personne ayant accès au site SharePoint.
1. Cliquez sur Enregistrer.

Activez le service de synchronisation DAM, qui est désactivé par défaut :

1. Accédez aux composants de la console web OSGi : [http://localhost:4502/system/console/components](http://localhost:4502/system/console/components).
1. Recherchez « com.day.cq.dam.jcrconnectors.impl.AssetSynchronizationService. »
1. Cliquez sur Activer.

Vous pouvez éventuellement configurer le délai de synchronisation entre différents cycles de synchronisation :

1. Accédez à la console de gestion OSGi : [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr).
1. Recherchez « DAY CQ DAM JCR Connector Asset Synchronization Service ».
1. Modifiez les valeurs de configuration.
1. Définissez la valeur de la période de synchronisation (en secondes).
1. Cliquez sur Enregistrer.

### Configuration de l’authentification {#configuring-authentication}

SharePoint comprend les méthodes d’authentification classique et basée sur les revendications qui prennent en charge les types d’authentification suivants :

* Réglages de base
* Basée sur les formulaires

En particulier, les types d’authentification suivants sont disponibles :

* De base - classique
* Basée sur les formulaires - classique
* Basée sur les revendications - classique
* Basée sur les formulaires - revendications

Le connecteur JCR d’AEM pour Microsoft SharePoint 2010 et Microsoft SharePoint 2013, version 4.0., prend en charge l’authentification basée sur les revendications (suggérée par Microsoft), qui fonctionne dans les modes suivants :

* **Authentification de base/NTLM** : le connecteur tente d’abord de se connecter à l’aide de l’authentification de base. Si cela n’est pas possible, l’authentification s’appuie alors sur NTLM.
* **Authentification reposant sur les formulaires** : SharePoint valide les utilisateurs en fonction des informations d’identification qu’ils saisissent dans un formulaire de connexion (généralement une page web). Le système émet un jeton pour les requêtes authentifiées contenant une clé pour rétablir l’identité des requêtes ultérieures.

**Configuration de l’authentification basée sur les formulaires**

Allez à : [http://localhost:4502/system/console/bundles](http://localhost:4502/system/console/bundles).

1. Cliquez sur OSGI > Configuration.
1. Recherchez « Day JCR Connector for Microsoft SharePoint ».
1. Cliquez sur « Modifier les valeurs de configuration ».
1. Définissez la valeur de « Fabrique de connexions SharePoint » sur « com.day.crx.spi.sharepoint.security.FormsBasedAuthenticationConnectionFactory ».
1. Cliquez sur **Enregistrer**.

**Configuration de l’authentification de base (Windows)**

1. [Désactivez l’authentification par jeton](#disable-token-authentication).
1. Allez à : [http://localhost:4502/system/console/bundles](http://localhost:4502/system/console/bundles).
1. Cliquez sur OSGI > Configuration.
1. Recherchez **Day JCR Connector pour Microsoft Sharepoint**.
1. Cliquez sur `Edit the configuration values`.
1. Définissez la valeur de la Fabrique de connexions SharePoint sur `com.day.crx.spi.sharepoint.security.WindowsAuthenticationConnectionFactory`.
1. Cliquez sur **Enregistrer**.

Seul un utilisateur authentifié à la fois sur AEM et SharePoint peut accéder au contenu SharePoint par le biais du connecteur.

Vous pouvez également utiliser l’extension de connecteur pour l’authentification afin de créer un module d’authentification personnalisé, qui, par exemple, met en correspondance l’accès par des utilisateurs et utilisatrices AEM à des utilisateurs et utilisatrices SharePoint spécifiques. Créez des utilisateurs et utilisatrices AEM correspondant aux utilisateurs et utilisatrices SharePoint (le nom d’utilisateur et le mot de passe doivent correspondre) pour pouvoir voir le contenu SharePoint mappé à l’instance de connecteur.

Pour créer un utilisateur dans AEM, procédez comme suit :

1. Connectez-vous à http://localhost:9502/ avec l’utilisateur administrateur.
1. Cliquez sur Outils.
1. Cliquez sur Sécurité.
1. Cliquez sur Utilisateurs.
1. Cliquez sur **Créer un utilisateur**.
1. Fournissez l’ID utilisateur (un nom d’utilisateur ayant accès à SharePoint).
1. Fournissez le mot de passe correspondant.
1. Cliquez sur la coche verte pour créer l’utilisateur.

Pour ajouter l’utilisateur ou l’utilisatrice au groupe d’administration :

1. Accédez à l’administration du groupe.
1. Cliquez sur le nœud « a ».
1. Cliquez sur « Administrateurs ».
1. Saisissez l’ID utilisateur créé plus haut dans la zone de texte en face du bouton **Parcourir**. 
1. Cliquez sur la coche verte pour ajouter l’utilisateur au groupe administrateur.

### Désactivation de l’authentification par jeton {#disable-token-authentication}

1. Téléchargez et installez le package `basic auth`. `zip` à partir de la Distribution logicielle.

1. Fermez Quickstart.
1. Ouvrez le fichier *\crx-quickstart\repository\repository.xml*.
1. Recherchez la balise `<LoginModule class="com.day.crx.core.CRXLoginModule"> ... </LoginModule>.`.
1. Insérez la balise `<param name="disableTokenAuth" value="true"/>` dans la balise mentionnée à l’étape 4.
1. Enregistrez et fermez le fichier XML.
1. Redémarrez le QuickStart et connectez-vous avec vos informations d’identification.

#### Prise en charge de différentes méthodes d’authentification du serveur SharePoint {#supporting-different-authentication-methods-of-the-sharepoint-server}

Dans sa version standard, le connecteur prend en charge l’authentification **Windows** IIS standard (de base) et l’authentification basée sur les formulaires (reposant sur les jetons). Les [autres méthodes d’authentification](https://technet.microsoft.com/fr-fr/library/cc262350.aspx#section2) peuvent être prises en charge grâce au mécanisme d’extensibilité.

Les étapes suivantes fournissent des instructions permettant d’étendre l’authentification standard afin de prendre en charge différentes méthodes d’authentification du serveur SharePoint :

1. Mettez en œuvre `com.day.crx.spi.sharepoint.security.SharepointConnectionFactory` pour gérer le côté client de votre processus d’authentification spécifique.
1. Installez la mise en œuvre `SharepointConnectionFactory` comme un lot de fragment avec l’hôte de fragment `com.day.crx.spi.crx2sharepoint-bundle`.

   Si vous utilisez Maven, adaptez la configuration suivante de `maven-bundle-plugin` aux exigences de votre projet :

   ```xml
              <plugin>
                  <groupId>org.apache.felix</groupId>
                  <artifactId>maven-bundle-plugin</artifactId>
                  <extensions>true</extensions>
                  <configuration>
                      <instructions>
                          <Export-Package />
                          <Private-Package>
                              <!-- your private package here -->
                          </Private-Package>
                          <Fragment-Host>
                              com.day.crx.spi.crx2sharepoint-bundle
                          </Fragment-Host>
                       </instructions>
                  </configuration>
              </plugin>
   ```

1. Enregistrez la mise en œuvre `SharepointConnectionFactory` dans la configuration de connecteur. Dans la fenêtre de configuration du connecteur, cliquez sur **Options avancées**. Dans le champ **Fabrique de connexions SharePoint**, spécifiez le nom de la mise en œuvre `com.day.crx.spi.sharepoint.auth.CustomConnectionFactory`.

1. Redémarrez le connecteur.
