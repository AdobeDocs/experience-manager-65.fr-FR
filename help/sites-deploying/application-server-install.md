---
title: Installation du serveur d’applications
seo-title: Installation du serveur d’applications
description: 'Découvrez comment installer AEM avec un serveur d’applications. '
seo-description: 'Découvrez comment installer AEM avec un serveur d’applications. '
uuid: c9571f80-6ed1-46fe-b7c3-946658dfc3f4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 6fdce35d-2709-41cc-87fb-27a4b867e960
translation-type: tm+mt
source-git-commit: 0a082d3cff66b82ef6de551a735a16a001446a1e
workflow-type: tm+mt
source-wordcount: '1175'
ht-degree: 65%

---


# Installation du serveur d’applications{#application-server-install}

>[!NOTE]
>
>`JAR` et `WAR` sont les types de fichiers dans lesquels AEM est publié. Ces formats font l’objet d’une assurance qualité afin d’offrir les niveaux d’assistance qu’Adobe s’est engagé à fournir.


Cette section vous explique comment installer Adobe Experience Manager (AEM) avec un serveur d’applications. Consultez la section [Plates-formes prises en charge](/help/sites-deploying/technical-requirements.md#servlet-engines-application-servers) pour afficher les niveaux de prise en charge relatifs aux différents serveurs d’applications.

La procédure d’installation est décrite pour les serveurs d’applications suivants :

* [WebSphere 8.5](#websphere)
* [JBoss EAP 6.3.0/6.4.0](#jboss-eap)
* [Oracle WebLogic 12.1.3/12.2](#oracle-weblogic)
* [Tomcat 8/8.5](#tomcat)

Pour plus d’informations sur l’installation d’applications web, sur les configurations serveur et sur le démarrage et l’arrêt du serveur, consultez la documentation du serveur d’applications approprié.

>[!NOTE]
>
>Si vous utilisez Dynamic Media dans un déploiement WAR, consultez la [documentation de Dynamic Media](/help/assets/config-dynamic.md#enabling-dynamic-media).

## Description générale {#general-description}

### Default behavior when installing AEM in an Application Server {#default-behaviour-when-installing-aem-in-an-application-server}

AEM se présente sous la forme d’un seul fichier war à déployer.

En cas de déploiement, le comportement par défaut est le suivant :

* the run mode is `author`
* l’instance (référentiel, environnement Felix OSGI, lots, etc.) est installé dans `${user.dir}/crx-quickstart`où `${user.dir}` se trouve le répertoire de travail actuel, ce chemin vers crx-quickstart est appelé `sling.home`

* the context root is the war file name e.g : `aem-6`

#### Configuration {#configuration}

Vous pouvez changer le comportement par défaut comme suit :

* mode d’exécution : configurez le paramètre `sling.run.modes` dans le fichier `WEB-INF/web.xml` du fichier war AEM avant le déploiement.

*  : configurez le paramètre `sling.home`sling.home dans le fichier `WEB-INF/web.xml` du fichier war AEM avant le déploiement.

* racine du contexte : renommez le fichier war AEM.

#### Installation de l’instance de publication {#publish-installation}

Pour qu’une instance de publication soit déployée, vous devez définir le mode d’exécution sur publish :

* Décompressez le fichier WEB-INF/web.xml à partir du fichier war AEM.
* Définissez le paramètre sling.run.modes sur publish.
* Recompressez le fichier web.xml dans le fichier war AEM.
* Déployez le fichier war AEM.

#### Vérification de l’installation {#installation-check}

Pour vérifier que tous les éléments ont été installés, vous pouvez :

* parcourir le fichier `error.log` jusqu’à la fin pour vous assurer que tout le contenu est installé ;
* look in `/system/console` that all bundles are installed

#### Deux instances sur le même serveur d’applications {#two-instances-on-the-same-application-server}

À des fins de démonstration, il peut s’avérer utile d’installer les instances de création et de publication sur un seul serveur d’applications. Pour ce faire, procédez comme suit :

1. Modifiez les variables sling.home et sling.run.modes de l’instance de publication.
1. Décompressez le fichier WEB-INF/web.xml du fichier AEM war.
1. Définissez le paramètre sling.home sur un autre chemin d’accès (les chemins d’accès absolus et relatifs sont possibles).
1. Modifiez sling.run.modes pour publier pour l’instance de publication.
1. Recompressez le fichier web.xml.
1. Renommez les fichiers de guerre afin qu’ils portent des noms différents : Par exemple, l’un renomme aemauthor.war et l’autre, aempublish.war.
1. Utilisez des paramètres de mémoire plus élevés, par exemple pour les instances AEM par défaut, utilisez par exemple : -Xmx3072m
1. Déployez les deux applications web.
1. Une fois le déploiement effectué, arrêtez les deux applications web.
1. Dans les instances d’auteur et de publication, assurez-vous que dans les fichiers sling.properties, la propriété felix.service.urlhandlers=false est définie sur false (par défaut, elle est définie sur true).
1. Redémarrez les deux applications web.

## Procédures d’installation des serveurs d’applications {#application-servers-installation-procedures}

### /WebSphere 8.5{#websphere}

Avant de procéder à un déploiement, lisez la [Description générale](#general-description) ci-dessus.

**Préparation du serveur**

* Laissez passer les en-têtes d’authentification de base :

   * Pour laisser à AEM le soin d’authentifier un utilisateur, une méthode consiste à désactiver la sécurité d’administration globale du serveur WebSphere. Pour ce faire, accédez à Sécurity > Global Security et désactivez la case à cocher « Enable administrative security », enregistrez et redémarrez le serveur.

* set `"JAVA_OPTS= -Xmx2048m"`
* Si vous souhaitez installer AEM à l’aide de la racine du contexte = /, vous devez tout d’abord modifier la racine de contexte de l’application web par défaut existante.

**Déploiement de l’application web AEM**

* Téléchargez le fichier war AEM.
* Au besoin, effectuez vos configurations dans le fichier web.xml (voir ci-dessus, sous Description générale).

   * Décompresser le fichier WEB-INF/web.xml
   * modifier le paramètre sling.run.modes pour publier
   * annuler la mise en commentaire du paramètre initial sling.home et définir ce chemin selon vos besoins
   * Réparer le fichier web.xml

* Déployez le fichier war AEM.

   * Choisissez une racine de context (si vous souhaitez définir les modes d’exécution sling, vous devez sélectionner les étapes détaillées de l’assistant de déploiement, puis le spécifier à l’étape 6 de l’assistant).

* Démarrez l’application web AEM.

#### JBoss EAP 6.3.0/6.4.0 {#jboss-eap}

Avant de procéder à un déploiement, lisez la [Description générale](#general-description) ci-dessus.

**Préparation du serveur JBoss**

Set Memory arguments in your conf file(e.g. `standalone.conf`)

* JAVA_OPTS=&quot;-Xms64m -Xmx2048m&quot;

if you use the deployment-scanner for to install the AEM web application it might be good to increase the `deployment-timeout,` for that set a `deployment-timeout` attribute in the xml file of your instance (e.g `configuration/standalone.xml)`:

```xml
<subsystem xmlns="urn:jboss:domain:deployment-scanner:1.1">
            <deployment-scanner path="deployments" relative-to="jboss.server.base.dir" scan-interval="5000" deployment-timeout="1000"/>
</subsystem>
```

**Déploiement de l’application web AEM**

* Téléchargez l’application Web AEM dans JBoss Administration Console.

* Activez l’application Web AEM.

#### Oracle WebLogic 12.1.3/12.2 {#oracle-weblogic}

Avant de procéder à un déploiement, lisez la [Description générale](#general-description) ci-dessus.

Dans ce cas, une simple disposition serveur est utilisée avec uniquement un serveur d’administration.

**Préparation de WebLogic Server**

* In `${myDomain}/config/config.xml`add to the security-configuration section:

   * `<enforce-valid-basic-auth-credentials>false</enforce-valid-basic-auth-credentials>` voir sur [https://xmlns.oracle.com/weblogic/domain/1.0/domain.xsd](https://xmlns.oracle.com/weblogic/domain/1.0/domain.xsd) pour connaître la position correcte (par défaut, la position à la fin de la section est ok).

* Augmentez les paramètres mémoire de la machine virtuelle :

   * open `${myDomain}/bin/setDomainEnv.cmd` (resp.sh) search for WLS_MEM_ARGS, set e.g set `WLS_MEM_ARGS_64BIT=-Xms256m -Xmx2048m`
   * redémarrage de WebLogic Server

* Create in `${myDomain}` a packages folder and inside a cq folder and in it a Plan folder

**Déploiement de l’application web AEM**

* Téléchargez le fichier war AEM.
* Placez le fichier d&#39;AEM guerre dans le dossier ${myDomain}/packages/cq.
* Make your configurations In `WEB-INF/web.xml` if needed (see above in the General Description)

   * Décompresser le `WEB-INF/web.xml`fichier
   * modifier le paramètre sling.run.modes pour publier
   * annuler la mise en commentaire du paramètre initial sling.home et définir ce chemin selon vos besoins (voir Description générale)
   * Réparer le fichier web.xml

* Déployez le fichier war AEM en tant qu’application (pour les autres paramètres, utilisez les valeurs par défaut).
* L’installation peut prendre un certain temps.
* Vérifiez que l’installation est bien terminée, comme indiqué ci-dessus dans la section Description générale (par exemple, en parcourant le fichier error.log jusqu’à la fin).
* You can change the context root in the Configuration tab of the web application in the WebLogic `/console`

#### Tomcat 8/8.5 {#tomcat}

Avant de procéder à un déploiement, lisez la [Description générale](#general-description) ci-dessus.

* **Préparation du serveur Tomcat**

   * Augmentez les paramètres mémoire de la machine virtuelle :

      * In `bin/catalina.bat` (resp `catalina.sh` on unix) add the following setting:
      * `set "JAVA_OPTS= -Xmx2048m`
   * Tomcat n’active aucun accès de type administrateur ou gestionnaire au niveau de l’installation. Vous devez donc modifier manuellement le fichier `tomcat-users.xml` si vous souhaitez autoriser l’accès pour ces comptes :

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
   * Si vous souhaitez déployer AEM à l’aide de la racine du contexte « / », vous devez tout d’abord modifier la racine de contexte de l’application web ROOT existante :

      * Arrêtez et annulez le déploiement de l’application web ROOT.
      * Renommez le dossier ROOT.war dans le dossier webapps de Tomcat.
      * Redémarrez l’application web.
   * Si vous installez l’application web AEM à l’aide de l’interface utilisateur graphique du gestionnaire, vous devez augmenter la taille maximale d’un fichier chargé, étant donné que le paramètre par défaut autorise uniquement une taille de chargement de 50 Mo. Pour cela, ouvrez le fichier web.xml de l’application web manager,

      `webapps/manager/WEB-INF/web.xml`

      and increase the max-file-size and max-request-size to at least 500MB, see the following `multipart-config` example of such a a `web.xml` file.

      ```xml
      <multipart-config>
      <!-- 500MB max -->
      <max-file-size>524288000</max-file-size>
      <max-request-size>524288000</max-request-size>
      <file-size-threshold>0</file-size-threshold>
      </multipart-config>
      ```




* **Déploiement de l’application web AEM**

   * Téléchargez le fichier war AEM.
   * Au besoin, effectuez vos configurations dans le fichier web.xml (voir ci-dessus, sous Description générale).

      * Décompresser le fichier WEB-INF/web.xml
      * modifier le paramètre sling.run.modes pour publier
      * annuler la mise en commentaire du paramètre initial sling.home et définir ce chemin selon vos besoins
      * Réparer le fichier web.xml
   * Renommez le fichier war AEM en ROOT.war si vous souhaitez effectuer un déploiement en tant qu’application web racine ; renommez-le en aemauthor.war, par exemple, si aemauthor doit être une racine de contexte.
   * Copiez-le dans le dossier webapps de Tomcat.
   * Attendez que l’application AEM soit installée.


## Résolution des incidents {#troubleshooting}

Pour plus d’informations sur la résolution des problèmes qui peuvent survenir en cours d’installation, voir :

* [Résolution des incidents](/help/sites-deploying/troubleshooting.md)
