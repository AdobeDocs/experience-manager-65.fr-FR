---
title: Réglage des performances du serveur AEM Forms
seo-title: Réglage des performances du serveur AEM Forms
description: Pour qu’AEM Forms s’exécute de manière optimale, vous pouvez affiner les paramètres du cache et les paramètres JVM. En outre, l’utilisation d’un serveur Web peut améliorer les performances du déploiement d’AEM Forms.
seo-description: Pour qu’AEM Forms s’exécute de manière optimale, vous pouvez affiner les paramètres du cache et les paramètres JVM. En outre, l’utilisation d’un serveur Web peut améliorer les performances du déploiement d’AEM Forms.
uuid: bf23b62c-7559-4726-8f4e-cc8b1457e501
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 38c0ec46-5686-4656-bfb4-7125ec194673
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 76%

---


# Réglage des performances du serveur AEM Forms{#performance-tuning-of-aem-forms-server}

Cet article explique les stratégies et les recommandations que vous pouvez implémenter pour réduire les ralentissements et optimiser les performances du déploiement d’AEM Forms.

## Paramètres du cache {#cache-settings}

Vous pouvez configurer et contrôler la stratégie de mise en cache d’AEM Forms à l’aide du composant **Mobile Forms Configurations** de la console d’administration Web d’AEM à l’adresse :

* (AEM Forms on OSGi) `https://'[server]:[port]'/system/console/configMgr`
* (AEM Forms on JEE) `https://'[server]:[port]'/lc/system/console/configMgr`

Les options disponibles pour la mise en cache sont les suivantes :

* **Aucune** : Impose de ne mettre en cache aucun artefact. En pratique, ceci ralentit les performances et nécessite une disponibilité importante de la mémoire en raison de l’absence de cache.
* **Conservatrice** : Indique de ne mettre en cache que les artefacts intermédiaires générés avant le rendu du formulaire, tels qu’un modèle contenant des fragments et des images en ligne.
* **Agressive** : Impose de mettre en cache presque tout ce qui peut être mis en cache, y compris le contenu HTML rendu, outre tous les artefacts du niveau de mise en cache Conservatrice. Ceci permet d’obtenir de meilleures performances mais utilise davantage de mémoire pour le stockage des artefacts mis en cache. La stratégie de mise en cache Agressive permet d’obtenir des performances constantes dans la rapidité du rendu d’un formulaire car le contenu rendu est mis en cache.

Les paramètres de cache par défaut d’AEM Forms peuvent ne pas suffire pour obtenir des performances optimales. Par conséquent, il est recommandé d’utiliser les paramètres suivants :

* **Stratégie de cache** : Agressive
* **Taille du cache** (nombre de formulaires) : Selon les besoins
* **Taille d’objet maximale** : Selon les besoins

![Configuration de Mobile Forms](assets/snap.png)

>[!NOTE]
>
>Si vous utilisez le répartiteur AEM pour mettre en cache des formulaires adaptatifs, il met également en cache les formulaires adaptatifs contenant des formulaires avec des données préremplies. Si ces formulaires sont diffusés à partir du cache du répartiteur AEM, il se peut que des données préremplies ou obsolètes soient diffusées aux utilisateurs. Par conséquent, utilisez le répartiteur AEM pour mettre en cache des formulaires adaptatifs qui n’utilisent pas de données pré-renseignées. De plus, un cache de répartiteur n’invalide pas automatiquement les fragments mis en cache. Par conséquent, ne l’utilisez pas pour mettre en cache des fragments de formulaire. Pour de tels formulaires et fragments, utilisez le [Cache de formulaires adaptatifs](../../forms/using/configure-adaptive-forms-cache.md).

## Paramètres JVM    {#jvm-parameters}

For optimal performance, it is recomended to use the following JVM `init` arguments to configure the `Java heap` and `PermGen`.

```shell
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -Xms8192m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -Xmx8192m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -XX:PermSize=256m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -XX:MaxPermSize=1024m
```

>[!NOTE]
>
>Les paramètres recommandés sont pour le JDK Windows 2008 R2 8 Core et Oracle HotSpot 1.7 (64 bits) et doivent être augmentés ou réduits en fonction de votre configuration système.

## Utilisation d’un serveur Web {#using-a-web-server}

Les formulaires adaptatifs et les formulaires HTML5 sont rendus au format HTML5. Le résultat peut être volumineux en fonction de facteurs comme la taille du formulaire et les images qu’il contient. Pour optimiser le transfert des données, l’approche recommandée consiste à compresser la réponse HTML à l’aide du serveur Web à partir duquel la demande est traitée. Cette approche réduit la taille de la réponse, le trafic réseau et le temps nécessaire pour diffuser les données entre les machines client et serveur.

Par exemple, suivez les étapes ci-dessous pour activer la compression sur Apache Web Server 2.0 32 bits avec JBoss :

>[!NOTE]
>
>Les instructions suivantes ne s&#39;appliquent à aucun autre serveur que le serveur Web Apache 2.0 32 bits. Pour obtenir des instructions spécifiques à un autre serveur, reportez-vous à la documentation correspondante.

Les étapes suivantes présentent les modifications à effectuer pour activer la compression avec le serveur Web Apache.

**Procurez-vous le logiciel du serveur Web Apache correspondant à votre système d’exploitation**

* Windows : Téléchargez le serveur Web Apache à partir du site Apache HTTP Server Project.
* Solaris 64 bits : Téléchargez le serveur Web Apache à partir du site Web Sunfreeware for Solaris.
* Linux : Le serveur Web Apache est préinstallé sur un système Linux.

Apache peut communiquer avec CRX via le protocole HTTP. Les configurations concernent l’optimisation via HTTP.

1. Uncomment the following module configurations in `APACHE_HOME/conf/httpd.conf` file.

   ```shell
   LoadModule proxy_balancer_module modules/mod_proxy.so
   LoadModule proxy_balancer_module modules/mod_proxy_http.so
   LoadModule deflate_module modules/mod_deflate.so
   ```

   >[!NOTE]
   >
   >For Linux, the default `APACHE_HOME` is `/etc/httpd/`.

1. Configurez le proxy sur le port 4502 de crx.
Ajoutez la configuration suivante dans le fichier de `APACHE_HOME/conf/httpd.conf` configuration.

   ```shell
   ProxyPass / https://<server>:4502/
   ProxyPassReverse / https://<server>:4502/
   ```

1. Activez la compression. Ajoutez la configuration suivante dans le fichier de `APACHE_HOME/conf/httpd.conf` configuration.

   **Pour les formulaires HTML5**

   ```xml
   <Location /content/xfaforms>
       <IfModule mod_deflate.c>
           SetOutputFilter DEFLATE
           #Don’t compress
           SetEnvIfNoCase Request_URI \.(?:gif|jpe?g|png)$ no-gzip dont-vary
           SetEnvIfNoCase Request_URI \.(?:exe|t?gz|zip|bz2|sit|rar)$ no-gzip dont-vary
           #Dealing with proxy servers
               <IfModule mod_headers.c>
                   Header append Vary User-Agent
               </IfModule>
       </IfModule>
   </Location>
   ```

   **Pour les formulaires adaptatifs**

   ```xml
   <Location /content/forms/af>
       <IfModule mod_deflate.c>
           SetOutputFilter DEFLATE
           #Don’t compress
           SetEnvIfNoCase Request_URI \.(?:gif|jpe?g|png)$ no-gzip dont-vary
           SetEnvIfNoCase Request_URI \.(?:exe|t?gz|zip|bz2|sit|rar)$ no-gzip dont-vary
           #Dealing with proxy servers
               <IfModule mod_headers.c>
                   Header append Vary User-Agent
               </IfModule>
       </IfModule>
   </Location>
   ```

   To access the crx server, use `https://'server':80`, where `server` is the name of the server on which the Apache server is running.

## À l’aide d’un antivirus sur un serveur exécutant AEM Forms {#using-an-antivirus-on-server-running-aem-forms}

Les performances peuvent être lentes sur les serveurs exécutant un logiciel antivirus. Un logiciel antivirus (analyse à l’accès) toujours actif analyse tous les fichiers d’un système. Il peut ralentir le serveur et les performances d’AEM Forms sont affectées.

Pour améliorer les performances, vous pouvez configurer le logiciel antivirus pour exclure les fichiers et dossiers AEM Forms suivants de l’analyse permanente (à l’accès) :

* Répertoire d’installation d’AEM. S’il n’est pas possible d’exclure le répertoire complet, excluez les fichiers suivants :

   * [Répertoire]d’installation d’AEM \crx-repository\temp
   * [Répertoire]d’installation d’AEM \crx-repository\repository
   * [Répertoire]d’installation d’AEM \crx-repository\launchpad

* Répertoire temporaire du serveur d’applications. L’emplacement par défaut est :

   * (Jboss) [AEM installation directory]\jboss\standalone\tmp
   * (Weblogic) \Oracle\Middleware\user_projects\domains\LCDomain\servers\LCServer1\tmp
   * (Websphere) \Program Files\IBM\WebSphere\AppServer\profiles\AppSrv01\temp

* **(AEM Forms on JEE uniquement)** Répertoire de stockage global de documents (GDS). L’emplacement par défaut est :

   * (JBoss) [appserver root]/server/&#39;server&#39;/svcnative/DocumentStorage
   * (WebLogic) [appserverdomain]/&#39;server&#39;/adobe/LiveCycleServer/DocumentStorage
   * (WebSphere) [appserver root]/installedApps/adobe/&#39;server&#39;/DocumentStorage

* **(AEM Forms on JEE uniquement)** Journaux du serveur et répertoire temporaire AEM Forms. L’emplacement par défaut est :

   * Server logs - [AEM Forms installation directory]\Adobe\AEM forms\[app-server]\server\all\logs
   * Temp directory - [AEM Forms installation directory]\temp

>[!NOTE]
>
>* If you are using a different location for GDS and temporary directory, open AdminUI at `https://'[server]:[port]'/adminui`, navigate to **Home > Settings > Core System Settings > Core Configurations** to confirm the location in use.

* Si le serveur AEM Forms se comporte lentement même après avoir exclu les répertoires suggérés, excluez également le fichier exécutable Java (java.exe).



