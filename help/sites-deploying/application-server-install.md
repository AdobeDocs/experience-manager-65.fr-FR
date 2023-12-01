---
title: Installer un serveur d’applications
description: Découvrez comment installer Adobe Experience Manager avec un serveur d’applications.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
exl-id: 3a90f1d2-e53f-4cc4-8122-024ad6500de0
source-git-commit: 5e56441d2dc9b280547c91def8d971e7b1dfcfe3
workflow-type: tm+mt
source-wordcount: '1164'
ht-degree: 41%

---

# Installer un serveur d’applications{#application-server-install}

>[!NOTE]
>
>`JAR` et `WAR` sont les types de fichiers dans lesquels Adobe Experience Manager (AEM) est publié. Ces formats font l’objet d’une assurance qualité pour s’adapter aux niveaux de prise en charge auxquels l’Adobe s’est engagé.
>

Cette section vous explique comment installer Adobe Experience Manager (AEM) avec un serveur d’applications. Consultez la [Plateformes prises en charge](/help/sites-deploying/technical-requirements.md#servlet-engines-application-servers) pour en savoir plus sur les niveaux de prise en charge spécifiques fournis pour chaque serveur d’applications.

La procédure d’installation est décrite pour les serveurs d’applications suivants :

* [WebSphere](#websphere)
* [JBoss](#jboss-eap)
* [Oracle WebLogic 12.1.3/12.2](#oracle-weblogic)
* [Tomcat 8/8.5](#tomcat)

Pour plus d’informations sur l’installation d’applications Web, sur les configurations serveur et sur le démarrage et l’arrêt du serveur, consultez la documentation du serveur d’applications approprié.

>[!NOTE]
>
>Si vous utilisez Dynamic Media dans un déploiement WAR, voir [Documentation Dynamic Media](/help/assets/config-dynamic.md#enabling-dynamic-media).

## Description générale {#general-description}

### Comportement par défaut lors de l’installation d’AEM sur un serveur d’applications {#default-behaviour-when-installing-aem-in-an-application-server}

AEM est fourni sous la forme d’un fichier war unique à déployer.

En cas de déploiement, les événements suivants se produisent par défaut :

* Le mode d’exécution est `author`.
* l’instance (référentiel, environnement Felix OSGI, bundles, etc.) est installée dans `${user.dir}/crx-quickstart`where `${user.dir}` est le répertoire de travail actuel, ce chemin d’accès à crx-quickstart est appelé `sling.home`

* la racine du contexte est le nom du fichier war, par exemple :  `aem-6`

#### Configuration {#configuration}

Vous pouvez modifier le comportement par défaut de la manière suivante :

* Mode d’exécution : configurez le paramètre `sling.run.modes` dans le fichier `WEB-INF/web.xml` du fichier war AEM avant le déploiement.

* sling.home : configurez le paramètre `sling.home` dans le fichier `WEB-INF/web.xml` du fichier war AEM avant le déploiement.

* Racine de contexte : renommez le fichier war AEM.

#### Installation de l’instance de publication {#publish-installation}

Pour qu’une instance de publication soit déployée, vous devez définir le mode d’exécution sur publish :

* Décompressez le fichier WEB-INF/web.xml du fichier war AEM.
* Modification du paramètre sling.run.modes pour publier
* Recompressez le fichier web.xml dans AEM fichier war.
* Déployez le fichier war AEM.

#### Vérification de l’installation {#installation-check}

Pour vérifier si tout est installé, vous pouvez :

* parcourir le fichier `error.log` jusqu’à la fin pour vous assurer que tout le contenu est installé ;
* vérifier que tous les ensembles sont installés sous `/system/console`.

#### Deux instances sur le même serveur d’applications {#two-instances-on-the-same-application-server}

À des fins de démonstration, il peut être approprié d’installer les instances de création et de publication sur un serveur d’applications. Pour cela, procédez comme suit :

1. Modifiez les variables sling.home et sling.run.modes de l’instance de publication.
1. Décompressez le fichier WEB-INF/Web.xml à partir du fichier war AEM.
1. Remplacez le paramètre sling.home par un autre chemin d’accès (les chemins absolus et relatifs sont possibles).
1. Définissez la variable sling.run.modes sur « publication » pour l’instance de publication.
1. Recompressez le fichier Web.xml.
1. Renommez les fichiers war afin qu’ils portent des noms différents. Par exemple, l’un renomme aemauthor.war, l’autre aempublish.war.
1. Utilisez des paramètres de mémoire plus élevés. Par exemple, les instances AEM par défaut utilisent `-Xmx3072m`
1. Déployez les deux applications web.
1. Après le déploiement, arrêtez les deux applications web.
1. Dans les instances de création et de publication, vérifiez dans les fichiers sling.properties que la propriété felix.service.urlhandlers=false est définie sur « false » (par défaut, elle est définie sur « true »).
1. Redémarrez les deux applications web.

## Procédures d’installation des serveurs d’applications {#application-servers-installation-procedures}

### WebSphere® 8.5 {#websphere}

Avant de procéder à un déploiement, lisez la [Description générale](#general-description) ci-dessus.

**Préparation du serveur**

* Laissez passer les en-têtes d’authentification de base :

   * Pour permettre à AEM d’authentifier un utilisateur, désactivez la sécurité administrative globale du serveur WebSphere®. Pour cela, accédez à Sécurité -> Sécurité globale et décochez la case Activer la sécurité administrative, enregistrez et redémarrez le serveur.

* Définissez `"JAVA_OPTS= -Xmx2048m"`.
* Si vous souhaitez installer AEM à l’aide de la racine du contexte = /, modifiez la racine du contexte de l’application web par défaut existante.

**Déploiement de l’application Web AEM**

* Téléchargez le fichier war AEM.
* Effectuez vos configurations dans web.xml si nécessaire (voir ci-dessus dans la Description générale).

   * Décompressez le fichier WEB-INF/Web.xml.
   * Définissez le paramètre sling.run.modes sur « publication ».
   * Supprimez les marques de commentaire du paramètre sling.home initial et définissez ce chemin d’accès en fonction de vos besoins.
   * Recompressez le fichier Web.xml.

* Déployez le fichier war AEM.

   * Choisissez une racine de contexte (si vous souhaitez définir les modes d’exécution sling, vous devez sélectionner les étapes détaillées de l’assistant de déploiement, puis la spécifier à l’étape 6 de l’assistant).

* Démarrer AEM application web

#### JBoss® EAP 6.3.0/6.4.0 {#jboss-eap}

Avant de procéder à un déploiement, lisez la [Description générale](#general-description) ci-dessus.

**Préparation du serveur JBoss®**

Définir des arguments de mémoire dans votre fichier conf (par exemple, `standalone.conf`)

* JAVA_OPTS=&quot;-Xms64m -Xmx2048m&quot;

Si vous utilisez le scanner de déploiement pour installer l’application web AEM, il peut être judicieux d’augmenter la `deployment-timeout,` pour ce jeu de `deployment-timeout` dans le fichier xml de votre instance (par exemple, `configuration/standalone.xml)`:

```xml
<subsystem xmlns="urn:jboss:domain:deployment-scanner:1.1">
            <deployment-scanner path="deployments" relative-to="jboss.server.base.dir" scan-interval="5000" deployment-timeout="1000"/>
</subsystem>
```

**Déploiement de l’application Web AEM**

* Téléchargez l’application web AEM dans la console d’administration JBoss®.

* Activez l’application Web AEM.

#### Oracle WebLogic 12.1.3/12.2 {#oracle-weblogic}

Avant de procéder à un déploiement, lisez la [Description générale](#general-description) ci-dessus.

Cette opération utilise une simple disposition de serveur avec uniquement un serveur d’administration.

**Préparation de WebLogic Server**

* Dans le fichier `${myDomain}/config/config.xml`, ajoutez ce qui suit à la section security-configuration :

   * `<enforce-valid-basic-auth-credentials>false</enforce-valid-basic-auth-credentials>`Pour en connaître la position exacte (vous pouvez, par défaut, le positionner à la fin de la section), rendez-vous à l’adresse [https://xmlns.oracle.com/Weblogic/domain/1.0/domain.xsd](https://xmlns.oracle.com/Weblogic/domain/1.0/domain.xsd).

* Augmentez les paramètres mémoire de la machine virtuelle :

   * open `${myDomain}/bin/setDomainEnv.cmd` (resp.sh) recherchez WLS_MEM_ARGS, définissez, par exemple, set. `WLS_MEM_ARGS_64BIT=-Xms256m -Xmx2048m`
   * Redémarrez WebLogic Server.

* Créez un dossier de packages dans `${myDomain}`. Placez-y un dossier cq et, à l’intérieur de celui-ci, un dossier Plan.

**Déploiement de l’application Web AEM**

* Téléchargez le fichier war AEM.
* Placez le fichier war AEM dans le dossier ${myDomain}/packages/cq.
* Au besoin, effectuez vos configurations dans le fichier `WEB-INF/web.xml` (voir ci-dessus, sous Description générale).

   * Décompresser le fichier `WEB-INF/web.xml`.
   * Définissez le paramètre sling.run.modes sur « publication ».
   * Supprimez les marques de commentaire du paramètre sling.home initial et définissez ce chemin d’accès en fonction de vos besoins (voir la Description générale).
   * Recompressez le fichier Web.xml.

* Déployez le fichier war AEM. en tant qu’application (pour les autres paramètres, utilisez les paramètres par défaut)
* L&#39;installation peut prendre du temps...
* Vérifiez que l’installation est terminée comme indiqué ci-dessus dans la Description générale (par exemple, en contournant le fichier error.log).
* Vous pouvez modifier la racine du contexte dans l’onglet Configuration de l’application Web dans la `/console` WebLogic.

#### Tomcat 8/8.5 {#tomcat}

Avant de procéder à un déploiement, lisez la [Description générale](#general-description) ci-dessus.

* **Préparation du serveur Tomcat**

   * Augmentez les paramètres mémoire de la machine virtuelle :

      * Dans `bin/catalina.bat` (resp `catalina.sh` sur UNIX®) ajoutez le paramètre suivant :
      * `set "JAVA_OPTS= -Xmx2048m`

   * Tomcat n’active pas l’accès administrateur ou manager lors de l’installation. Par conséquent, vous devez modifier manuellement `tomcat-users.xml` pour autoriser l’accès à ces comptes :

      * Modifiez le fichier `tomcat-users.xml` afin d’inclure l’accès pour l’administrateur et le gestionnaire. La configuration doit être semblable à l’exemple suivant :

        ```xml
        <?xml version='1.0' encoding='utf-8'?>
        <tomcat-users>
        role rolename="manager"/>
        role rolename="tomcat"/>
        <role rolename="admin"/>
        <role rolename="role1"/>
        <role rolename="manager-gui"/>
        <user username="both" password="tomcat" roles="tomcat,role1"/>
        <user username="tomcat" password="tomcat" roles="tomcat"/>
        <user username="admin" password="admin" roles="admin,manager-gui"/>
        <user username="role1" password="tomcat" roles="role1"/>
        </tomcat-users>
        ```

   * Si vous souhaitez déployer AEM avec la racine de contexte &quot;/&quot;, vous devez modifier la racine de contexte de l’application Web ROOT existante :

      * Arrêt et annulation du déploiement de l’application web ROOT
      * Renommez le dossier ROOT.war dans le dossier webapps de tomcat.
      * Redémarrer l’application web

   * Si vous installez l’application web AEM à l’aide de l’interface de ligne de commande manager-gui, vous devez augmenter la taille maximale d’un fichier téléchargé, car la valeur par défaut autorise uniquement une taille de chargement de 50 Mo. Pour ce faire, ouvrez le fichier Web.xml de l’application de gestion Web,

     `webapps/manager/WEB-INF/web.xml`

     et augmentez la taille de fichier maximale et la taille de requête maximale à au moins 500 Mo. Voir à ce propos la section `multipart-config` un exemple de ce type `web.xml` fichier .

     ```xml
     <multipart-config>
     <!-- 500MB max -->
     <max-file-size>524288000</max-file-size>
     <max-request-size>524288000</max-request-size>
     <file-size-threshold>0</file-size-threshold>
     </multipart-config>
     ```

* **Déploiement de l’application Web AEM**

   * Téléchargez le fichier war AEM.
   * Effectuez vos configurations dans web.xml si nécessaire (voir ci-dessus dans la Description générale).

      * Décompressez le fichier WEB-INF/Web.xml.
      * Définissez le paramètre sling.run.modes sur « publication ».
      * Supprimez les marques de commentaire du paramètre sling.home initial et définissez ce chemin d’accès en fonction de vos besoins.
      * Recompressez le fichier Web.xml.

   * Renommez AEM fichier war en ROOT.war si vous souhaitez le déployer en tant qu’application web racine, renommez-le par exemple aemauthor.war si vous souhaitez que aemauthor soit la racine du contexte.
   * copiez-le dans le dossier webapps de tomcat
   * patienter jusqu’à ce que AEM soit installé

## Résolution des problèmes {#troubleshooting}

Pour plus d’informations sur les problèmes qui peuvent survenir lors de l’installation, voir :

* [Résolution des problèmes](/help/sites-deploying/troubleshooting.md)
