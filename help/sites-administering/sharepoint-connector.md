---
title: SharePoint Connector
seo-title: SharePoint Connector
description: Day JCR Connector for Microsoft SharePoint 2010 and Microsoft SharePoint 2013, version 4.0.
seo-description: En savoir plus sur SharePoint Connector dans AEM.
uuid: df650476-4e2a-486f-a007-b5ac437ff99f
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 907316d1-3d23-4c46-bccb-bad6fe1bd1bb
docset: aem65
exl-id: 10ea7d2e-6e44-4d5c-a2b2-63c73b18f172
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1571'
ht-degree: 70%

---

# SharePoint Connector{#sharepoint-connector}

Cet article contient des informations détaillées sur Adobe JCR Connector for Microsoft SharePoint 2010 et Microsoft SharePoint 2013, version 4.0.

SharePoint Connector prend en charge les fonctionnalités de base suivantes :

* Lecture de contenu et de métadonnées SharePoint
* Reconnaissance des paramètres de sécurité SharePoint pour le contenu auquel vous accédez en appliquant l’authentification et l’autorisation SharePoint natives
* Intégration de contenu à l’aide de l’outil de recherche de contenu
* Utilisation des composants AEM, tels qu’une ressource externe pour afficher des images et des vidéos SharePoint
* Synchronisation de SharePoint avec AEM Assets

Toutes les fonctionnalités sont mises en œuvre en utilisant les services web SharePoint natifs comme interface du contenu et des services SharePoint.

>[!NOTE]
>
>SharePoint Connector est également pris en charge avec AEM 6.1 Service Pack 2. Le connecteur ne prend plus en charge le montage de référentiel virtuel et, par conséquent, il ne peut pas être monté. Si vous souhaitez accéder au référentiel SharePoint à l’aide d’API Java, utilisez l’implémentation du référentiel JCR du connecteur SharePoint dans votre projet.
>
>L’installation, la configuration, la gestion et les opérations informatiques du serveur SharePoint et de l’infrastructure informatique associée ne rentrent pas dans le cadre de ce document. Voir la documentation du fournisseur sur [SharePoint](https://www.microsoft.com/sharepoint) pour plus d’informations sur ces rubriques. Le connecteur nécessite que ces parties de l’infrastructure soient correctement installées, configurées et utilisées.


## Prise en main {#getting-started}

Pour débuter avec le connecteur, effectuez les opérations suivantes :

* Assurez-vous de disposer au moins de Java 7.
* Téléchargez le fichier de distribution du package connecteur depuis Distribution logicielle.
* Copiez un fichier *license.properties* valide vers le répertoire contenant le fichier *cq-quickstart-6.4.0.jar*.

* Double-cliquez/appuyez sur le fichier .jar pour démarrer AEM ou démarrez-le à partir de la ligne de commande.
* Installez le module du connecteur depuis le gestionnaire de modules.
* Configurez les options du connecteur.

## Installation de SharePoint Connector {#installing-sharepoint-connector}

Le connecteur est un module de contenu qui facilite la configuration. Installez le module à l’aide de Package Manager, puis définissez l’URL du serveur SharePoint.
et d’autres options de configuration. Le contenu SharePoint est disponible dans le référentiel AEM.

### Configuration requise pour l’installation {#installation-requirements}

Le connecteur nécessite ce qui suit :

* Java Runtime Environment 1.7 ou version ultérieure
* Services web SharePoint disponibles via le réseau
* URL du serveur SharePoint
* Informations d’identification et autorisations de l’utilisateur pour les référentiels CRX et SharePoint
* [Plateformes prises en charge](#supported-platforms)

Le connecteur SharePoint peut être téléchargé à partir de [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/featurepack/cq-6.3.0-featurepack-17673).

### Plateformes prises en charge {#supported-platforms}

Le connecteur prend en charge les applications suivantes :

* Versions d’AEM :

   * AEM 6.4, 6.3

* Versions de Microsoft SharePoint

   * Microsoft Office SharePoint Server (MOSS) 2010
   * Microsoft Office SharePoint Server (MOSS) 2013

* Si vous avez besoin d’une assistance pour des déploiements personnalisés du connecteur (OEM, besoins particuliers, méthodes d’authentification personnalisées), contactez le bureau Adobe de votre région.

>[!NOTE]
>
>Le connecteur ne prend en charge que les configurations officiellement prises en charge par Microsoft. Voir les configurations système requises par [MOSS 2010](https://technet.microsoft.com/en-us/library/cc262485(office.14).aspx) et [MOSS 2013](https://technet.microsoft.com/en-us/library/cc262485.aspx).

### Installation standard {#standard-installation}

Distribution logicielle est utilisée pour distribuer des fonctionnalités de produit, des exemples et des correctifs logiciels. Pour plus d’informations, voir la [documentation Distribution logicielle](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html#software-distribution).


#### Intégration à AEM {#integrating-with-aem}

Pour installer le module de contenu du connecteur.

1. Ouvrez un ticket d’assistance Adobe pour demander le Feature Pack de connecteur.
1. Téléchargez le module lorsqu’il est disponible et ouvrez ensuite le gestionnaire de modules pour votre instance AEM.
1. Appuyez/cliquez sur **Installer** dans la page de description du package.
1. Dans la boîte de dialogue **Installer le package**, appuyez/cliquez sur **Installer**.

   **Remarque** : Assurez-vous d’être connecté en tant qu’administrateur.

1. Une fois le package installé, appuyez/cliquez sur **Fermer**.

## Configuration de SharePoint Connector {#configuring-sharepoint-connector}

Une fois que vous avez installé SharePoint Connector, configurez l’application et les couches SharePoint pour le connecteur.

Définissez l’URL du serveur SharePoint pour rendre votre référentiel SharePoint conforme à JCR. Vous pouvez définir des paramètres supplémentaires pour configurer la connexion au serveur SharePoint. En outre, configurez l’authentification à l’aide de SharePoint Connector.

### Configuration de la connexion au serveur SharePoint  {#configuring-the-connection-with-the-sharepoint-server}

Pour définir l’URL du serveur SharePoint et les options avancées, procédez comme suit :

1. Accédez à la console de gestion OSGi : [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr).
1. Recherchez le lot **Day JCR Connector for Microsoft SharePoint** .
1. Modifiez les valeurs de configuration.
1. Définissez l’URL du serveur SharePoint comme valeur dans **Espaces de travail**.
1. Appuyez/cliquez sur **Enregistrer**.

![chlimage_1-62](assets/chlimage_1-62.png)

Paramètres Espaces de travail et Nom d’espace de travail par défaut :

Par défaut, le connecteur expose un espace de travail JCR unique. Le serveur SharePoint exposé par cet espace de travail est défini via le paramètre de configuration URL du serveur SharePoint.

  Le connecteur peut également être configuré pour plusieurs espaces de travail. Dans ce cas, chaque espace de travail est associé à l’URL du serveur SharePoint correspondant qui est exposé par l’espace de travail. Pour ajouter un espace de travail, ajoutez une définition d’espace de travail au paramètre Espaces de travail. Une définition d’espace de travail a le format suivant :
`<name>`= `<url>` où
`<name>` est le nom de l’espace de travail JCR et
`<url>` est l’URL du serveur SharePoint pour cet espace de travail.

Dans AEM, effectuez une étape en plus des étapes de configuration ci-dessus. Liste autorisée du lot &#39;**com.day.cq.dam.cq-dam-jcr-connectors**&#39;.

Pour liste autorisée des lots dans AEM, procédez comme suit :

1. Accédez à la console de gestion OSGi : http://localhost:4502/system/console/configMgr.
1. Recherchez le service Apache Sling Login Admin Whitelist.
1. Sélectionnez **Contourner la liste autorisée**.
1. Ajouter `com.day.cq.dam.cq-dam-jcr-connectors` dans la valeur par défaut des lots de liste autorisée
1. Cliquez sur Enregistrer.

![chlimage_1-82](assets/chlimage_1-82a.png)

>[!NOTE]
>
>Si vous configurez plusieurs espaces de travail, indiquez le nom de l’espace de travail par défaut dans le paramètre du nom d’espace de travail par défaut.

Pour plus d’informations sur les paramètres liés à l’authentification, voir [Authentification](/help/sites-administering/sharepoint-connector.md#configuring-authentication).

### Vérification de la configuration de SharePoint {#verifying-the-sharepoint-setup}

Une fois que vous avez configuré le connecteur, vérifiez les points suivants :

* Le serveur SharePoint s’exécute et les services web sont accessibles à l’instance de connecteur.
* Les informations d’identification d’utilisateur SharePoint sont valides, et l’utilisateur dispose des permissions nécessaires pour SharePoint.
* Le connecteur est installé et configuré correctement.

### Configuration de la synchronisation de la gestion des actifs numériques avec le serveur SharePoint  {#configuring-dam-sync-with-the-sharepoint-server}

Pour synchroniser les ressources SharePoint avec AEM, effectuez les étapes suivantes :

1. Accédez à la console de gestion OSGi : [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr).
1. Recherchez le service Default DAMAssetSynchronization.
1. Modifiez les valeurs de configuration.
1. Définissez le nom et le mot de passe correspondants de l’utilisateur ayant accès au site SharePoint.
1. Cliquez sur Enregistrer.

Activez le service de synchronisation de la gestion des actifs numériques, qui est désactivé par défaut :

1. Accédez aux composants de la console web OSGi : [http://localhost:4502/system/console/components](http://localhost:4502/system/console/components)
1. Recherchez com.day.cq.dam.jcrconnectors.impl.AssetSynchronizationService.
1. Cliquez sur Activer.

Vous pouvez éventuellement configurer le délai de synchronisation entre les cycles de synchronisation :

1. Accédez à la console de gestion OSGi : [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)
1. Recherchez DAY CQ DAM JCR Connector Asset Synchronization Service.
1. Modifiez les valeurs de configuration.
1. Définissez la valeur de la période de synchronisation (en secondes).
1. Cliquez sur Enregistrer.

### Configuration de l’authentification  {#configuring-authentication}

SharePoint comprend les méthodes d’authentification classique et basée sur les revendications qui prennent toutes les deux en charge les types d’authentification suivants :

* De base
* Basée sur les formulaires

En particulier, les types d’authentification suivants sont disponibles :

* Classique – de base
* Classique – reposant sur les formulaires
* Revendications – de base
* Revendications – reposant sur les formulaires

Le connecteur JCR AEM pour Microsoft SharePoint 2010 et Microsoft SharePoint 2013, version 4.0. prend en charge l’authentification basée sur les revendications (suggérée par Microsoft), qui fonctionne dans les modes suivants :

* **Authentification de base/NTLM** : le connecteur tente d’abord de se connecter à l’aide de l’authentification de base. Si elle n’est pas disponible, il passe à l’authentification basée sur NTLM.
* **Authentification** basée sur Forms : SharePoint valide les utilisateurs en fonction des informations d’identification saisies par les utilisateurs dans un formulaire de connexion (généralement une page web). Le système génère un jeton pour les requêtes authentifiées contenant une clé pour rétablir l’identité des requêtes ultérieures.

**Configuration de l’authentification reposant sur les formulaires**

Accédez à : [http://localhost:4502/system/console/bundles](http://localhost:4502/system/console/bundles)

1. Cliquez sur OSGi > Configuration.
1. Recherchez Day JCR Connector for Microsoft SharePoint.
1. Cliquez sur Modifier les valeurs de configuration.
1. Définissez la valeur de Fabrique de connexions SharePoint sur com.day.crx.spi.sharepoint.security.FormsBasedAuthenticationConnectionFactory/.
1. Cliquez sur **Enregistrer**.

**Configuration de l’authentification de base (Windows)**

1. [Désactivez l’authentification par jeton](#disable-token-authentication).
1. Accédez à [http://localhost:4502/system/console/bundles](http://localhost:4502/system/console/bundles).
1. Cliquez sur OSGi > Configuration.
1. Recherchez **Day JCR Connector for Microsoft SharePoint**.
1. Cliquez sur `Edit the configuration values`.
1. Définissez la valeur de Fabrique de connexions SharePoint sur `com.day.crx.spi.sharepoint.security.WindowsAuthenticationConnectionFactory`.
1. Cliquez sur **Enregistrer**.

Seul un utilisateur authentifié à la fois sur AEM et SharePoint peut accéder au contenu SharePoint par le biais du connecteur.

Vous pouvez également utiliser l’extension de connecteur pour l’authentification afin de créer un module d’authentification personnalisé, qui, par exemple, met en correspondance l’accès par des utilisateurs AEM à des utilisateurs SharePoint spécifiques. Créez des utilisateurs AEM correspondant aux utilisateurs SharePoint (le nom d’utilisateur et le mot de passe doivent correspondre) afin de pouvoir afficher le contenu SharePoint mis en correspondance avec une instance de connecteur.

Pour créer un utilisateur dans AEM :

1. Connectez-vous à http://localhost:9502/ avec l’utilisateur administrateur.
1. Cliquez sur Outils.
1. Cliquez sur Sécurité.
1. Cliquez sur Utilisateurs.
1. Cliquez sur **Créer un utilisateur**.
1. Indiquez l’ID utilisateur (nom d’utilisateur ayant accès à SharePoint).
1. Indiquez le mot de passe correspondant.
1. Cliquez sur le symbole de coche verte pour créer l’utilisateur.

Pour ajouter l’utilisateur au groupe administrateur :

1. Accédez à l’administration des groupes..
1. Cliquez sur le noeud &quot;a&quot;.
1. Cliquez sur &quot;administrateurs&quot;.
1. Saisissez l’ID utilisateur créé ci-dessus dans la zone de texte devant le bouton **Parcourir** .
1. Cliquez sur le symbole représentant une coche verte pour ajouter l’utilisateur au groupe d’administrateurs.

### Désactivation de l’authentification par jeton {#disable-token-authentication}

1. Téléchargez et installez le package `basic auth`. `zip` de Distribution logicielle.

1. Fermez QuickStart.
1. Ouvrez le fichier *\crx-quickstart\repository\repository.xml*.
1. Recherchez la balise `<LoginModule class="com.day.crx.core.CRXLoginModule"> ... </LoginModule>.`
1. Insérez la balise `<param name="disableTokenAuth" value="true"/>` à l’intérieur de la balise mentionnée à l’étape 4.
1. Enregistrez et fermez le fichier XML.
1. Redémarrez QuickStart et connectez-vous avec vos informations d’identification.

#### Prise en charge de différentes méthodes d’authentification du serveur SharePoint {#supporting-different-authentication-methods-of-the-sharepoint-server}

Dans sa version standard, le connecteur prend en charge l’authentification **Windows** IIS standard (de base) et l’authentification basée sur les formulaires (reposant sur les jetons). Les [autres méthodes d’authentification](https://technet.microsoft.com/en-us/library/cc262350.aspx#section2) peuvent être prises en charge grâce au mécanisme d’extensibilité.

Les étapes suivantes fournissent des instructions permettant d’étendre l’authentification standard afin de prendre en charge différentes méthodes d’authentification du serveur SharePoint :

1. Mettez en œuvre `com.day.crx.spi.sharepoint.security.SharepointConnectionFactory` pour gérer le côté client de votre processus d’authentification spécifique.
1. Installez l’implémentation `SharepointConnectionFactory` en tant que lot de fragments avec l’hôte de fragment `com.day.crx.spi.crx2sharepoint-bundle`.

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

1. Enregistrez la mise en œuvre `SharepointConnectionFactory` dans la configuration de connecteur. Dans la fenêtre de configuration du connecteur, cliquez sur **Options avancées**. Dans le champ pour **Usine de connexion SharePoint** , indiquez le nom de l’implémentation `com.day.crx.spi.sharepoint.auth.CustomConnectionFactory`.

1. Redémarrez le connecteur.
