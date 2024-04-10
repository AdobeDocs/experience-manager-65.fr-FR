---
title: Installer une instance autonome personnalisée
description: Découvrez les options disponibles lors de l’installation d’une instance AEM autonome.
content-type: reference
topic-tags: deploying
exl-id: d6484bb7-8123-4f42-96e8-aa441b1093f3
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '1629'
ht-degree: 100%

---

# Installer une instance autonome personnalisée{#custom-standalone-install}

Cette section décrit les options disponibles lors de l’installation d’une instance AEM autonome. Vous pouvez également lire [Éléments de stockage](/help/sites-deploying/storage-elements-in-aem-6.md) pour plus d’informations sur le choix du type de stockage principal après l’installation d’AEM 6.

## Modification du numéro de port en renommant le fichier {#changing-the-port-number-by-renaming-the-file}

Le port par défaut pour AEM est le 4502. Si ce port n’est pas disponible ou est en cours d’utilisation, le démarrage rapide se configure automatiquement afin d’utiliser le premier numéro de port disponible comme suit : 4502, 8080, 8081, 8082, 8083, 8084, 8085, 8888, 9362, `<*random*>`.

Vous pouvez également définir le numéro de port en renommant le fichier jar de démarrage rapide afin que le nom de fichier inclue le numéro de port ; par exemple, `cq5-publish-p4503.jar` ou `cq5-author-p6754.jar`.

Les différentes règles suivantes s’appliquent lorsque vous renommez le fichier jar de démarrage rapide :

* Lorsque vous renommez le fichier, il doit commencer par `cq;`, par exemple `cq5-publish-p4503.jar`.

* Il est recommandé de *toujours* faire précéder le numéro de port de -p, comme dans cq5-publish-p4503.jar ou cq5-author-p6754.jar.

>[!NOTE]
>
>Cela permet de ne pas avoir à se préoccuper du respect des règles utilisées pour extraire le numéro de port :
>
>* le numéro de port doit comporter 4 ou 5 chiffres
>* ces chiffres doivent figurer après un tiret
>* si le nom du fichier comporte d’autres chiffres, alors le numéro du port doit comporter le préfixe `-p`
>* le préfixe « cq5 » au début du nom du fichier est ignoré
>

>[!NOTE]
>
>Vous pouvez également modifier le numéro de port à l’aide de l’option `-port` dans la commande de démarrage.

### Considérations relatives à Java 11 {#java-considerations}

Si vous exécutez Oracle Java 11 (ou en général les versions de Java ultérieures à la version 8), des modifications supplémentaires doivent être ajoutées à votre ligne de commande lors du démarrage d’AEM.

* Les commutateurs - `-add-opens` suivants doivent être ajoutés pour éviter les messages d’avertissement relatifs à l’accès à la réflexion dans `stdout.log`.

```shell
--add-opens=java.desktop/com.sun.imageio.plugins.jpeg=ALL-UNNAMED --add-opens=java.base/sun.net.www.protocol.jrt=ALL-UNNAMED --add-opens=java.naming/javax.naming.spi=ALL-UNNAMED --add-opens=java.xml/com.sun.org.apache.xerces.internal.dom=ALL-UNNAMED --add-opens=java.base/java.lang=ALL-UNNAMED --add-opens=java.base/jdk.internal.loader=ALL-UNNAMED --add-opens=java.base/java.net=ALL-UNNAMED -Dnashorn.args=--no-deprecation-warning
```

* Vous devez également utiliser le commutateur `-XX:+UseParallelGC` afin de limiter tous les problèmes de performance potentiels.

Voici à quoi doivent ressembler les paramètres supplémentaires JVM au démarrage d’AEM sur Java 11 :

```shell
-XX:+UseParallelGC --add-opens=java.desktop/com.sun.imageio.plugins.jpeg=ALL-UNNAMED --add-opens=java.base/sun.net.www.protocol.jrt=ALL-UNNAMED --add-opens=java.naming/javax.naming.spi=ALL-UNNAMED --add-opens=java.xml/com.sun.org.apache.xerces.internal.dom=ALL-UNNAMED --add-opens=java.base/java.lang=ALL-UNNAMED --add-opens=java.base/jdk.internal.loader=ALL-UNNAMED --add-opens=java.base/java.net=ALL-UNNAMED -Dnashorn.args=--no-deprecation-warning
```

Enfin, si vous exécutez une instance mise à jour d’AEM 6.3, assurez-vous que la propriété suivante est définie sur **true** sous `sling.properties` :

* `felix.bootdelegation.implicit`

## Modes d’exécution {#run-modes}

Les **modes d’exécution** vous permettent d’ajuster votre instance d’AEM à des fins spécifiques. Par exemple, pour la création ou la publication, le test, le développement, l’intranet et plus encore. Ces modes permettent de contrôler l’utilisation d’un exemple de contenu. Cet exemple de contenu est défini avant la création du démarrage rapide et peut inclure des packages, des configurations, etc. Cela peut s’avérer particulièrement utile pour les installations prêtes pour la production lorsque vous souhaitez maintenir votre installation légère et sans exemple de contenu. Pour en savoir plus, voir :

* [Modes d’exécution](/help/sites-deploying/configure-runmodes.md)

## Ajout d’un utilitaire d’installation de fichiers {#adding-a-file-install-provider}

Par défaut, le dossier `crx-quickstart/install` est surveillé pour les fichiers.
Ce dossier n’existe pas, mais peut être simplement créé au moment de l’exécution.

En présence d’un lot, la configuration ou le package de contenu est placé dans ce répertoire. Il est automatiquement sélectionné et installé. S’il est supprimé, il est désinstallé.
Il s’agit d’une autre méthode pour placer des lots, des packages de contenu ou des configurations dans le référentiel.

Cela est particulièrement intéressant pour plusieurs cas d’utilisation :

* Au cours du développement, il peut être plus facile de placer un élément dans le système de fichiers.
* Si un problème se produit, la console web et le référentiel ne sont pas accessibles. Vous pouvez ainsi placer des lots supplémentaires dans ce répertoire et ils doivent être installés.
* Vous pouvez créer le dossier `crx-quickstart/install` avant le lancement du démarrage rapide et vous pouvez y placer des packages supplémentaires.

>[!NOTE]
>
>Pour des exemples, consultez également [Comment installer des packages CRX automatiquement au démarrage du serveur](https://helpx.adobe.com/fr/experience-manager/kb/HowToInstallPackagesUsingRepositoryInstall.html).

## Installation et démarrage d’Adobe Experience Manager en tant que service Windows {#installing-and-starting-adobe-experience-manager-as-a-windows-service}

>[!NOTE]
>
>Veillez à effectuer la procédure suivante lorsque vous êtes connecté en tant qu’administrateur ou administratrice ou démarrez/exécutez ces étapes en sélectionnant **Exécuter en tant qu’administrateur** dans le menu contextuel.
>
>Une connexion en tant qu’utilisateur ou utilisatrice disposant de droits d’administration est **insuffisante**. Si vous n’êtes pas connecté en tant qu’administrateur lors de la réalisation des étapes, vous recevez des erreurs **Accès refusé**.

Pour installer et démarrer AEM en tant que service Windows :

1. Ouvrez le fichier crx-quickstart\opt\helpers\instsrv.bat dans un éditeur de texte.
1. Si vous configurez un serveur Windows 64 bits, remplacez toutes les instances de prunsrv par l’une des commandes suivantes, en fonction du système d’exploitation :

   * prunsrv_amd64
   * prunsrv_ia64

   Cette commande appelle le script approprié qui lance le service de démon Windows en Java 64 bits au lieu de 32 bits.

1. Pour empêcher que le processus ne se transforme en plusieurs processus, augmentez le paramètre JVM PermGen. Localisez la commande `set jvm_options` et définissez la valeur comme suit :

   `set jvm_options=-Xmx1792m`

1. Ouvrez l’invite de commandes, définissez le répertoire courant sur le dossier crx-quickstart/opt/helpers de l’installation AEM et saisissez la commande suivante afin de créer le service :

   `instsrv.bat cq5`

   Pour vérifier que le service est créé, ouvrez Services dans le panneau de commande Outils d’administration ou tapez `start services.msc` dans l’invite de commandes. Le service cq5 apparaît dans la liste.

1. Démarrez le service en effectuant l’une des opérations suivantes :

   * Dans le panneau de configuration Services, cliquez sur cq5, puis sur Démarrer.

   ![chlimage_1-11](assets/chlimage_1-11.png)

   * Sur la ligne de commande, tapez net start cq5.

   ![chlimage_1-12](assets/chlimage_1-12.png)

1. Windows indique que le service est en cours d’exécution. AEM démarre et le fichier exécutable prunsrv apparaît dans le Gestionnaire de tâches. Dans le navigateur Web, accédez à AEM, par exemple `https://localhost:4502` pour commencer à l’utiliser.

   ![chlimage_1-13](assets/chlimage_1-13.png)

>[!NOTE]
>
>Les valeurs de propriété du fichier instsrv.bat sont utilisées lors de la création du service Windows. Si vous modifiez les valeurs de propriété dans instsrv.bat, vous devez désinstaller, puis réinstaller le service.

>[!NOTE]
>
>Lorsque vous installez AEM en tant que service, vous devez indiquer le chemin absolu pour le répertoire des journaux dans `com.adobe.xmp.worker.files.ncomm.XMPFilesNComm` à partir du gestionnaire de la configuration.

Pour désinstaller le service, cliquez sur **Arrêter** dans le panneau de commande **Services** ou dans la ligne de commande, accédez au dossier et saisissez `instsrv.bat -uninstall cq5`. Le service est supprimé de la liste du panneau de commande **Services** ou de la liste de la ligne de commande lorsque vous saisissez `net start`.

## Redéfinition de l’emplacement du répertoire de travail temporaire {#redefining-the-location-of-the-temporary-work-directory}

L’emplacement par défaut du dossier temporaire de la machine java est `/tmp`. AEM utilise également ce dossier, par exemple lors de la création de packages.

Si vous souhaitez modifier l’emplacement du dossier temporaire (par exemple si vous avez besoin d’un répertoire avec plus d’espace libre), définissez un chemin * `<new-tmp-path>` * en ajoutant le paramètre JVM :

`-Djava.io.tmpdir="/<*new-tmp-path*>"`

à :

* la ligne de commande de démarrage du serveur
* le paramètre d’environnement CQ_JVM_OPTS dans le script serverctl ou start

## Autres options disponibles dans le fichier Quickstart {#further-options-available-from-the-quickstart-file}

D’autres options et conventions de renommage sont décrites dans le fichier d’aide du démarrage rapide, disponibles par l’intermédiaire de l’option- help. Pour accéder à l’aide, tapez :

* `java -jar cq-quickstart-6.5.0.jar -help`

>[!CAUTION]
>
>Ces options sont valides à compter de la version d’origine d’AEM 6.5 (6.5.0.0). Des modifications sont susceptibles d’être apportées dans les versions ultérieures de SP.

```shell
Loading quickstart properties: default
Loading quickstart properties: instance
Setting properties from filename '/Users/Desktop/AEM/cq-quickstart-6.5.0.jar'
--------------------------------------------------------------------------------
Adobe Experience Manager Quickstart (build 20190328)                            
--------------------------------------------------------------------------------
Usage:                                                                          
 Use these options on the Quickstart command line.                              
--------------------------------------------------------------------------------

-help (--help,-h)
         Show this help message                                                 
-quickstart.server.port (-p,-port) <port>
         Set server port number                                                 
-contextpath (-c,-org.apache.felix.http.context_path) <contextpath>
         Set context path                                                       
-debug <port>
         Enable Java Debugging on port number; forces forking                   
-gui 
         Show GUI if running on a terminal                                      
-nobrowser (-quickstart.nobrowser)
         Do not open browser at startup                                         
-unpack
         Unpack installation files only, do not start the server (implies       
         -verbose)                                                              
-v (-verbose)
         Do not redirect stdout/stderr to files and do not close stdin          
-nofork
         Do not fork the JVM, even if not running on a console                  
-fork
         Force forking the JVM if running on a console, using recommended       
         default memory settings for the forked JVM.                            
-forkargs <args> [<args> ...]
         Additional arguments for the forked JVM, defaults to '-Xmx1024m        
         -XX:MaxPermSize=256m '.  Use -- to specify values starting with -,     
         example: '-forkargs -- -server'                                        
-a (--interface) <interface>
         Optional IP address (interface) to bind to                             
-pt <string>
         Process type (main/fork) - do not use directly, used when forking a    
         process                                                                
-r <string> [<string> [<string> [<string> [<string> [<string> [<string> [<string> [<string> [<string>]]]]]]]]]
         Runmode(s) - Use this to define the run mode(s)                        
-b <string>
         Base folder - defines the path under which the quickstart work folder  
         is created                                                             
-low-mem-action <string>
         Low memory action - what to do if memory is insufficient at startup    
-use-control-port
         Start a control port                                                   
-nointeractive
         Start with no interactivity                                            
-ll <level>
         Define launchpad log level (1 = error...4 = debug)                     
-n   
         Do not install shutdown hook                                           
-D<property>=<value>
         Additional framework properties.                                       
-listener-port <listener-port>
         Set listener port number                                               
-x <string>
         Run a Quickstart extension.                                            
  Options for executing Quickstart extensions:
                                                                                
    -xargs <arg> [<arg> ...]
         Construct an arguments list for a Quickstart extension (for example, -xargs -- 
         -arg1 val1 -arg2 val2).                                                
--------------------------------------------------------------------------------
Quickstart filename options                                                     
--------------------------------------------------------------------------------
Usage:                                                                          
 Rename the jar file, including one of the patterns shown below, to set the     
corresponding option. Command-line options have priority on these filename      
patterns.                                                                       
--------------------------------------------------------------------------------

-NNNN
         Include -NNNN.jar or -pNNNN in the renamed jar filename to run on port 
         NNNN, for example: quickstart-8085.jar                                 
-nobrowser
         Include -nobrowser in the renamed jar filename to avoid opening the    
         browser at startup, example: quickstart-nobrowser-8085.jar             
-publish
         Include -publish in the renamed jar filename to run in "publish" mode, 
         example: cq-publish-7502.jar                                           
-dynamicmedia
         Include -dynamicmedia in the renamed jar filename to run in            
         "dynamicmedia" mode, example: quickstart-dynamicmedia-4502.jar         
-dynamicmedia_scene7
         Include -dynamicmedia_scene7 in the renamed jar filename to run in     
         "dynamicmedia_scene7" mode, example:                                   
         quickstart-dynamicmedia_scene7-p4502.jar                               
--------------------------------------------------------------------------------
The license.properties file
--------------------------------------------------------------------------------
  The license.properties file stores licensing information, created from the    
  licensing form displayed on first startup and stored in the folder from where 
  Quickstart is run.                                                            
--------------------------------------------------------------------------------
Log files
--------------------------------------------------------------------------------
  Once Quickstart has been unpacked and started, log files can be found under   
  /Users/aemdocs/CQInstallationKits/AEM-65150-L8/crx-quickstart/logs.           
--------------------------------------------------------------------------------
```

## Installation d’AEM dans l’environnement Amazon EC2 {#installing-aem-in-the-amazon-ec-environment}

Lors de l’installation d’AEM sur une instance Amazon Elastic Compute Cloud (EC2), si vous installez à la fois l’instance de création (auteur) et l’instance de publication (publication) sur l’instance EC2, l’instance de création est installée correctement en suivant la procédure [Installation des instances d’AEM Manager](#installinginstancesofaemmanager) ; par contre l’instance de publication devient une instance de création.

Avant d’installer l’instance de publication sur votre environnement EC2, procédez comme suit :

1. Décompressez le fichier jar de l’instance de publication avant de démarrer l’instance pour la première fois. Pour décompresser le fichier, utilisez la commande suivante :

   ```xml
   java -jar quickstart.jar -unpack
   ```

   >[!NOTE]
   >
   >Si vous modifiez le mode **après** le premier démarrage de l’instance, vous ne pouvez pas modifier le mode d’exécution.

1. Démarrez l’instance en exécutant :

   ```xml
   java -jar quickstart.jar -r publish
   ```

   >[!CAUTION]
   >
   >Assurez-vous d’exécuter l’instance après l’avoir décompressée en exécutant la commande ci-dessus. Sinon, le remplissage de quickstart.properties ne sera pas généré. Sans ce fichier, toutes les prochaines mises à niveau d’AEM échoueront.

1. Dans le dossier **bin**, ouvrez le script **start** et vérifiez la section suivante :

   ```xml
   # runmode(s)
   if [ -z "$CQ_RUNMODE" ]; then
    CQ_RUNMODE='author'
   fi
   ```

1. Modifiez le mode d’exécution en **publier** et enregistrez le fichier.

   ```xml
   # runmode(s)
   if [ -z "$CQ_RUNMODE" ]; then
    CQ_RUNMODE='publish'
   fi
   ```

1. Arrêtez l’instance et redémarrez-la en exécutant le script **start**.

## Vérification de l’installation {#verifying-the-installation}

Les liens suivants peuvent être utilisés pour vérifier que votre installation est opérationnelle (tous les exemples reposent sur le fait que l’instance s’exécute sur le port 8080 de l’hôte local, que CRX est installé sous /crx et Launchpad sous /) :

* `https://localhost:8080/crx/de`
Console du CRXDE Lite.

* `https://localhost:8080/system/console`
Console Web.

## Actions après installation {#actions-after-installation}

Bien qu’il existe de nombreuses possibilités de configuration de la gestion du contenu web AEM, certaines actions doivent être entreprises, ou au moins être examinées immédiatement après l’installation :

* Consultez la [Liste de contrôle de sécurité](/help/sites-administering/security-checklist.md) pour obtenir les tâches requises permettant de garantir que votre système reste sécurisé.
* Consultez la liste des utilisateurs, des utilisatrices et des groupes par défaut installés avec la gestion de contenu web AEM. Vérifiez si vous souhaitez effectuer des actions sur d’autres comptes - voir [Sécurité et administration des utilisateurs et utilisatrices](/help/sites-administering/security.md) pour plus de détails.

## Accès à CRXDE Lite et à la console web {#accessing-crxde-lite-and-the-web-console}

Une fois la gestion de contenu AEM démarrée, vous pouvez également accéder aux éléments suivants :

* [CRXDE Lite](#accessing-crxde-lite) - utilisé pour accéder au référentiel et le gérer
* [Console web](#accessing-the-web-console) - utilisée pour gérer ou configurer les lots OSGi (également appelés Console OSGi)

### Accès à CRXDE Lite {#accessing-crxde-lite}

Pour ouvrir CRXDE Lite, vous pouvez sélectionner **CRXDE Lite** dans l’écran de bienvenue ou utiliser le navigateur pour accéder à

```
 https://<<i>host</i>>:<<i>port</i>>/crx/de/index.jsp
```

Par exemple :
`https://localhost:4502/crx/de/index.jsp`

![installcq_crxdelite](assets/installcq_crxdelite.png)

#### Accès à la console Web {#accessing-the-web-console}

Pour accéder à la console Web Adobe CQ, vous pouvez sélectionner **Console OSGi** depuis l’écran de bienvenue ou utiliser le navigateur pour accéder à

```
 https://<host>:<port>/system/console
```

Par exemple :
`https://localhost:4502/system/console`
ou pour la page Lots
`https://localhost:4502/system/console/bundles`

![chlimage_1-14](assets/chlimage_1-14.png)

Voir [Configuration OSGi à l’aide de la console web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) pour plus de détails.

## Résolution des problèmes {#troubleshooting}

Pour plus d’informations sur les problèmes qui peuvent se produire lors de l’installation, voir :

* [Résolution des problèmes](/help/sites-deploying/troubleshooting.md)

## Désinstaller Adobe Experience Manager {#uninstalling-adobe-experience-manager}

AEM s’installant dans un seul répertoire, un utilitaire de désinstallation n’est pas nécessaire. La désinstallation peut être aussi simple que la suppression de l’intégralité du répertoire d’installation, mais elle dépend en réalité de ce que vous souhaitez réaliser et du stockage persistant que vous utilisez.

Si le stockage persistant est incorporé dans le répertoire d’installation, par exemple dans l’installation par défaut de TarPM, la suppression de dossiers supprime également les données.

>[!NOTE]
>
>Adobe vous recommande vivement de sauvegarder votre référentiel avant de supprimer AEM. Si vous supprimez l’intégralité de &lt;cq-installation-directory>, vous supprimez également le référentiel. Pour conserver les données du référentiel avant de supprimer, déplacez ou copiez le dossier &lt;cq-installation-directory>/crx-quickstart/repository ailleurs avant de supprimer les autres dossiers.

Si votre installation d’AEM utilise un stockage externe, par exemple un serveur de base de données, la suppression du dossier ne supprime pas automatiquement les données, mais supprime la configuration de stockage, ce qui rend difficile la restauration du contenu JCR.
