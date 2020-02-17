---
title: Gestion des packages à l’aide de Maven
seo-title: Gestion des packages à l’aide de Maven
description: Le module externe Content Package Maven permet d’intégrer des tâches de gestion de packages dans vos projets Maven
seo-description: Le module externe Content Package Maven permet d’intégrer des tâches de gestion de packages dans vos projets Maven
uuid: fa73f0d6-8848-4911-9b96-311c875b45be
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 943de371-0149-4307-be3a-b11c590b3451
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d

---


# Gestion des packages à l’aide de Maven{#managing-packages-using-maven}

Le module externe Content Package Maven permet d’intégrer des tâches de gestion de packages dans vos projets Maven. Les paramètres et les goals du module externe permettent d’automatiser de nombreuses tâches qui sont normalement effectuées sur la page Package Manager ou la ligne de commande FileVault :

* Création de packages à partir des fichiers du système de fichiers
* Installation et désinstallation de packages sur le serveur CRX ou CQ
* Création de packages déjà définis sur le serveur
* Obtention de la liste des packages installés sur le serveur
* Suppression d’un package du serveur

## Ajout du module externe Content Package Maven au fichier POM {#adding-the-content-package-maven-plugin-to-the-pom-file}

Pour utiliser le module externe Content Package Maven, ajoutez l’élément plugin suivant dans l’élément build du fichier POM :

```xml
<plugin>
 <groupId>com.day.jcr.vault</groupId>
 <artifactId>content-package-maven-plugin</artifactId>
 <version>0.0.24</version>
 <configuration>
       <!-- parameters and values common to all goals, as required -->
 </configuration>
</plugin>
```

Pour que Maven puisse télécharger le module externe, utilisez le profil fourni dans la section [Obtention du module externe Content Package Maven](#obtaining-the-content-package-maven-plugin) de cette page.

## Version du module externe Content Package Maven : {#goals-of-the-content-package-maven-plugin}

Les goals et les paramètres de goal fournis par le module externe Content Package sont décrits dans les sections qui suivent. Les paramètres qui sont décrits dans la section Paramètres communs peuvent être utilisés pour la plupart des goals. Les paramètres qui s’appliquent à un goal sont décrits dans la section consacrée au goal en question.

**Préfixe du module externe**

Le préfixe du module externe est content-package. Utilisez ce préfixe pour exécuter un goal à partir de la ligne de commande, comme illustré ci-après.

```shell
mvn content-package:build
```

**Préfixe des paramètres**

Sauf indication contraire, les goals et les paramètres du module externe utilisent le préfixe vault, comme illustré ci-après.

```shell
mvn content-package:install -Dvault.targetURL="https://192.168.1.100:4502/crx/packmgr/service.jsp"
```

**Proxys**

Les goals qui utilisent des proxys pour le serveur CRX ou CQ ont recours à la première configuration de proxy valide dans les paramètres Maven. Si aucune configuration de proxy n’est trouvée, aucun proxy n’est utilisé. Reportez-vous au paramètre useProxy dans la section Paramètres communs.

### Paramètres communs {#common-parameters}

Les paramètres contenus dans le tableau ci-après sont communs à tous les goals, sauf si une note indique le contraire dans la colonne Goals.

<table>
 <tbody>
  <tr>
   <th>Nom</th>
   <th>Type</th>
   <th>Requis</th>
   <th>Valeur par défaut</th>
   <th>Description</th>
   <th>Goals</th>
  </tr>
  <tr>
   <td>failOnError</td>
   <td>booléen</td>
   <td>Non</td>
   <td>false</td>
   <td>La valeur <code>true</code> entraîne l’échec de la création lorsqu’une erreur se produit. La valeur <code>false</code> entraîne la création à ignorer l’erreur.</td>
   <td>Tous les goals, à l’exception de package.</td>
  </tr>
  <tr>
   <td>nom est</td>
   <td>Chaîne</td>
   <td>build : Oui<br /> installation : Non<br /> rm : Oui</td>
   <td>Créer : Aucune valeur par défaut.<br /> install : Valeur de la propriété artifactId du projet expert.</td>
   <td>Nom du package sur lequel exécuter une action.</td>
   <td>Tous les goals, à l’exception de Is.</td>
  </tr>
  <tr>
   <td>password</td>
   <td>Chaîne</td>
   <td>Oui</td>
   <td>admin</td>
   <td>Mot de passe utilisé pour l’authentification auprès du serveur CRX.</td>
   <td>Tous les goals, à l’exception de package.</td>
  </tr>
  <tr>
   <td>serverId</td>
   <td>Chaîne</td>
   <td>Non</td>
   <td></td>
   <td>ID du serveur à partir duquel récupérer le nom d’utilisateur et le mot de passe pour l’authentification.</td>
   <td>Tous les goals, à l’exception de package.</td>
  </tr>
  <tr>
   <td>targetURL</td>
   <td>Chaîne</td>
   <td>Oui</td>
   <td>http://localhost:4502/<br /> crx/packmgr/<br /> service.jsp</td>
   <td>URL de l’API du service HTTP du gestionnaire de packages CRX.</td>
   <td>Tous les goals, à l’exception de package.</td>
  </tr>
  <tr>
   <td>timeout</td>
   <td>int</td>
   <td>Non</td>
   <td>5</td>
   <td>Délai de connexion, exprimé en secondes, pour communiquer avec le service du gestionnaire de packages.</td>
   <td>Tous les goals, à l’exception de package.</td>
  </tr>
  <tr>
   <td>useProxy</td>
   <td>booléen</td>
   <td>Non</td>
   <td>true</td>
   <td>Détermine si les configurations de proxy du fichier des paramètres Maven doivent être utilisées ou non. A value of <code>true</code> causes the use of the first active proxy configuration found to proxy requests to the package manager. La valeur false entraîne la non-utilisation d’un proxy.</td>
   <td>Tous les goals, à l’exception de package.</td>
  </tr>
  <tr>
   <td>userId</td>
   <td>Chaîne</td>
   <td>Oui</td>
   <td>admin</td>
   <td>Nom d’utilisateur pour l’authentification auprès du serveur CRX.</td>
   <td>Tous les goals, à l’exception de package.</td>
  </tr>
  <tr>
   <td>verbose</td>
   <td>booléen</td>
   <td>Non</td>
   <td>false</td>
   <td>Active ou désactive la journalisation documentée. La valeur <code>true</code> l’active.</td>
   <td>Tous les goals, à l’exception de package.</td>
  </tr>
 </tbody>
</table>

### build {#build}

Crée un package de contenu déjà défini sur une instance AEM.

>[!NOTE]
>
>Il n’est pas nécessaire que le goal soit exécuté dans un projet Maven.

#### Paramètres {#parameters}

Tous les paramètres du goal build sont décrits dans la section [Paramètres communs](#common-parameters).

#### Exemple {#example}

L’exemple suivant crée le package workflow-mbean installé sur l’instance AEM avec l’adresse IP 10.36.79.223. L’objectif est exécuté à l’aide de la commande suivante :

```shell
mvn content-package:build
```

Le fichier POM ci-dessous est situé dans le répertoire actuel de l’outil de ligne de commande. Il spécifie le nom du package et l’URL du service du package.

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
  xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example</groupId>
  <artifactId>example-package</artifactId>
  <version>0.0.1-SNAPSHOT</version>
    <build>
        <plugins>
     <plugin>
  <groupId>com.day.jcr.vault</groupId>
  <artifactId>content-package-maven-plugin</artifactId>
  <version>0.0.24</version>
  <configuration>
   <name>workflow-mbean</name>
   <failOnError>true</failOnError>
   <targetURL>https://10.36.79.223:4502/crx/packmgr/service.jsp</targetURL>
  </configuration>
     </plugin>
 </plugins>
    </build>
</project>
```

### install {#install}

Installe un package dans le référentiel L’exécution de ce goal ne nécessite pas de projet Maven. Le goal est lié à la phase d’installation du cycle de vie de création Maven.

#### Paramètres {#parameters-1}

In addition to the following parameters, see the descriptions in the [Common Parameters](#common-parameters) section.

<table>
 <tbody>
  <tr>
   <th>Nom</th>
   <th>Type</th>
   <th>Requis</th>
   <th>Valeur par défaut</th>
   <th>Description</th>
  </tr>
  <tr>
   <td>artifact</td>
   <td>Chaîne</td>
   <td>Non</td>
   <td>Valeur de la propriété artifactId du projet Maven.</td>
   <td>Chaîne au format groupId:artifactId:version[:packaging].</td>
  </tr>
  <tr>
   <td>artifactId</td>
   <td>Chaîne</td>
   <td>Non</td>
   <td></td>
   <td>ID de l’artifact à installer.</td>
  </tr>
  <tr>
   <td>groupId</td>
   <td>Chaîne</td>
   <td>Non</td>
   <td></td>
   <td>groupId de l’artifact à installer.</td>
  </tr>
  <tr>
   <td>install</td>
   <td>booléen</td>
   <td>Non</td>
   <td>true</td>
   <td>Détermine si le package doit être décompressé automatiquement lorsqu’il est téléchargé. La valeur true décompresse le package. La valeur false ne décompresse pas le package.</td>
  </tr>
  <tr>
   <td>localRepository</td>
   <td>org.apache.maven.<br /> artifact. repository.<br /> ArtifactRepository</td>
   <td>Non</td>
   <td>Valeur de la variable système localRepository.</td>
   <td>Référentiel Maven local. Vous ne pouvez pas configurer ce paramètre à l’aide de la configuration du module externe. La propriété système est toujours utilisée.</td>
  </tr>
  <tr>
   <td>packageFile</td>
   <td>java.io.File</td>
   <td>Non</td>
   <td>artifact principal défini pour le projet Maven.</td>
   <td>Nom du fichier de package à installer.</td>
  </tr>
  <tr>
   <td>packaging</td>
   <td>Chaîne</td>
   <td>Non</td>
   <td>zip</td>
   <td>Type de package de l’artifact à installer.</td>
  </tr>
  <tr>
   <td>pomRemoteRepositories</td>
   <td>java.util.List</td>
   <td>Oui</td>
   <td>Valeur de la propriété remoteAtifactRepositories définie pour le projet Maven.</td>
   <td>Cette valeur ne peut pas être configurée à l’aide de la configuration du plugin. La valeur doit être spécifiée dans le projet. </td>
  </tr>
  <tr>
   <td>project</td>
   <td>org.apache.maven.<br /> project.MavenProject</td>
   <td>Oui</td>
   <td>Projet pour lequel le plugin est configuré.</td>
   <td>Projet Maven. Le projet est implicite, car il contient la configuration du module externe.</td>
  </tr>
  <tr>
   <td>repositoryId <i>(POM)</i><br /> repoID <i>(ligne de commande)</i></td>
   <td>Chaîne</td>
   <td>Non</td>
   <td>temp</td>
   <td>ID du référentiel duquel est récupéré l’artifact. Dans le code POM, utilisez repositoryID. Dans une ligne de commande, utilisez repoID.</td>
  </tr>
  <tr>
   <td>repositoryUrl <i>(POM)</i><br /> repoURL <i>(ligne de commande)</i></td>
   <td>Chaîne</td>
   <td>Non</td>
   <td></td>
   <td>URL du référentiel duquel est récupéré l’artifact. Dans le code POM, utilisez repositoryURL. Dans une ligne de commande, utilisez repoURL.</td>
  </tr>
  <tr>
   <td>version</td>
   <td>Chaîne</td>
   <td>Non</td>
   <td></td>
   <td>Version de l’artifact à installer.</td>
  </tr>
 </tbody>
</table>

#### Exemple {#example-1}

L’exemple suivant illustre la création d’un package contenant le lot OSGi workflow-mbean (voir l’exemple du goal [build](#build)), puis l’installation du package. Comme le goal install est lié à la phase d’installation du package, la commande suivante exécute le goal install :

```shell
mvn install
```

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
    xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="https://maven.apache.org/POM/4.0.0
    https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example.myapp</groupId>
  <artifactId>workflow-mbean</artifactId>
  <version>0.0.3-SNAPSHOT</version>

  <build>
    <plugins>
      <plugin>
        <groupId>com.day.jcr.vault</groupId>
        <artifactId>content-package-maven-plugin</artifactId>
        <version>0.0.24</version>
        <configuration>
          <builtContentDirectory>jcr_root</builtContentDirectory>
          <targetURL>https://10.36.79.223:4502/crx/packmgr/service.jsp</targetURL>
        </configuration>
        <executions>
          <execution>
            <goals>
              <goal>package</goal>
            </goals>
          </execution>
        </executions>
      </plugin>
    </plugins>
  </build>
</project>
```

### ls {#ls}

Répertorie les packages qui sont déployés dans Package Manager.

#### Paramètres {#parameters-2}

All parameters of the ls goal are described in the [Common Parameters](#common-parameters) section.

#### Exemple {#example-2}

L’exemple suivant répertorie les packages installés sur l’instance AEM avec l’adresse IP 10.36.79.223. L’objectif est exécuté à l’aide de la commande suivante :

```shell
mvn content-package:ls
```

Le fichier POM ci-dessous est situé dans le répertoire actuel de l’outil de ligne de commande. Il spécifie l’URL du service du package.

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
  xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example</groupId>
  <artifactId>example-package</artifactId>
  <version>0.0.1-SNAPSHOT</version>
    <build>
        <plugins>
     <plugin>
  <groupId>com.day.jcr.vault</groupId>
  <artifactId>content-package-maven-plugin</artifactId>
  <version>0.0.24</version>
  <configuration>
      <targetURL>https://10.36.79.223:4502/crx/packmgr/service.jsp</targetURL>
  </configuration>
      </plugin>
   </plugins>
     </build>
</project>
```

### rm {#rm}

Supprime un package de Package Manager.

#### Paramètres {#parameters-3}

All parameters of the rm goal are described in the [Common Parameters](#common-parameters) section.

#### Exemple {#example-3}

L’exemple suivant supprime le package workfow-mbean installé sur l’instance AEM avec l’adresse IP 10.36.79.223. L’objectif est exécuté à l’aide de la commande suivante :

```shell
mvn content-package:rm
```

Le fichier POM ci-dessous est situé dans le répertoire actuel de l’outil de ligne de commande. Il spécifie l’URL du service du package et le nom du package.

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
  xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example</groupId>
  <artifactId>example-package</artifactId>
  <version>0.0.1-SNAPSHOT</version>
    <build>
        <plugins>
     <plugin>
  <groupId>com.day.jcr.vault</groupId>
  <artifactId>content-package-maven-plugin</artifactId>
  <version>0.0.24</version>
  <configuration>
                    <name>workflow-mbean</name>
      <targetURL>https://10.36.79.223:4502/crx/packmgr/service.jsp</targetURL>
  </configuration>
      </plugin>
   </plugins>
     </build>
</project>
```

### uninstall {#uninstall}

Désinstalle un package. Le package reste sur le serveur avec l’état désinstallé.

#### Paramètres {#parameters-4}

All parameters of the uninstall goal are described in the [Common Parameters](#common-parameters) section.

#### Exemple {#example-4}

L’exemple suivant désinstalle le package workflow-mbean installé sur l’instance AEM avec l’adresse IP 10.36.79.223. L’objectif est exécuté à l’aide de la commande suivante :

```shell
mvn content-package:uninstall
```

Le fichier POM ci-dessous est situé dans le répertoire actuel de l’outil de ligne de commande. Il spécifie le nom du package et l’URL du service du package.

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
  xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example</groupId>
  <artifactId>workflow-mbean</artifactId>
  <version>0.0.3-SNAPSHOT</version>
    <build>
        <plugins>
     <plugin>
  <groupId>com.day.jcr.vault</groupId>
  <artifactId>content-package-maven-plugin</artifactId>
  <version>0.0.24</version>
  <configuration>
   <name>workflow-mbean</name>
   <failOnError>true</failOnError>
   <targetURL>https://10.36.79.223:4502/crx/packmgr/service.jsp</targetURL>
  </configuration>
     </plugin>
 </plugins>
    </build>
</project>
```

### package {#package}

Crée un package de contenu. La configuration par défaut du goal du package comprend le contenu du répertoire dans lequel les fichiers compilés sont enregistrés. L’exécution du goal du package requiert que la phase de création de la compilation soit terminée. Le goal est lié à la phase de package du cycle de vie de création Maven.

#### Paramètres {#parameters-5}

In addition to the following parameters, see the description of the `name` parameter in the [Common Parameters](#common-parameters) section.

<table>
 <tbody>
  <tr>
   <th>Nom</th>
   <th>Type</th>
   <th>Requis</th>
   <th>Valeur par défaut</th>
   <th>Description</th>
  </tr>
  <tr>
   <td>archive</td>
   <td>org.apache.maven.<br /> archiver.<br /> MavenArchiveConfiguration</td>
   <td>Non</td>
   <td></td>
   <td>Configuration d’archive à utiliser. Voir <a href="https://maven.apache.org/shared/maven-archiver/index.html">la documentation de Maven Archiver</a>.</td>
  </tr>
  <tr>
   <td>builtContentDirectory</td>
   <td>java.io.File</td>
   <td>Oui</td>
   <td>Valeur du répertoire de sortie de la build Maven.</td>
   <td>Répertoire qui comporte le contenu à inclure dans le package.</td>
  </tr>
  <tr>
   <td>dependencies</td>
   <td>java.util.List</td>
   <td>Non</td>
   <td></td>
   <td></td>
  </tr>
  <tr>
   <td>embeddedTarget</td>
   <td>java.lang.String</td>
   <td>Non</td>
   <td></td>
   <td></td>
  </tr>
  <tr>
   <td>embeddeds</td>
   <td>java.util.List</td>
   <td>Non</td>
   <td></td>
   <td></td>
  </tr>
  <tr>
   <td>failOnMissingEmbed</td>
   <td>booléen</td>
   <td>Oui</td>
   <td>false</td>
   <td>La valeur true provoque l’échec de la génération lorsqu’un artefact incorporé est introuvable dans les dépendances du projet. Une valeur incorrecte entraîne l’ignorance de l’erreur par la génération.</td>
  </tr>
  <tr>
   <td>filterSource</td>
   <td>java.io.File</td>
   <td>Non</td>
   <td></td>
   <td>Fichiers qui spécifie la source du filter de l’espace de travail. Les filtres spécifiés dans le fichier de configuration et injectés via les incorporations ou les sous-packages sont fusionnés avec le contenu du fichier.</td>
  </tr>
  <tr>
   <td>filters</td>
   <td>com.day.jcr.<br /> vault.maven.pack.impl.<br /> DefaultWorkspaceFilter</td>
   <td>Non</td>
   <td></td>
   <td>Contient les éléments filter qui définissent le contenu du package. Lorsqu’ils sont exécutés, les filtres sont inclus dans le fichier filter.xml. Voir la section Utilisation de l’élément filters ci-dessous.</td>
  </tr>
  <tr>
   <td>finalName</td>
   <td>java.lang.String</td>
   <td>Oui</td>
   <td>Paramètre finalName défini dans le projet Maven (phase build).</td>
   <td>Nom du fichier ZIP du package généré sans l’extension de fichier .zip.</td>
  </tr>
  <tr>
   <td>group</td>
   <td>java.lang.String</td>
   <td>Oui</td>
   <td>Paramètre groupID défini dans le projet Maven.</td>
   <td>groupId du package de contenu généré. Cette valeur fait partie du chemin d’installation cible du package de contenu.</td>
  </tr>
  <tr>
   <td>outputDirectory</td>
   <td>java.io.File</td>
   <td>Oui</td>
   <td>Répertoire build défini dans le projet Maven.</td>
   <td>Répertoire local dans lequel est enregistré le package de contenu.</td>
  </tr>
  <tr>
   <td>prefix</td>
   <td>java.lang.String</td>
   <td>Non</td>
   <td></td>
   <td></td>
  </tr>
  <tr>
   <td>project</td>
   <td>org.apache.maven.<br /> project.MavenProject</td>
   <td>Oui</td>
   <td></td>
   <td>Projet Maven.</td>
  </tr>
  <tr>
   <td>properties</td>
   <td>java.util.Map</td>
   <td>Non</td>
   <td></td>
   <td>Autres propriétés que vous pouvez définir dans le fichier properties.xml. Ces propriétés ne peuvent pas remplacer les propriétés prédéfinies suivantes :
    <ul>
     <li>group : Utilisez le paramètre de groupe à définir</li>
     <li>name : Utilisez le paramètre name pour définir</li>
     <li>version : Utiliser le paramètre de version à définir</li>
     <li>description : Défini à partir de la description du projet</li>
     <li>groupId : groupid du descripteur de projet Maven.</li>
     <li>artifactId : artifactId du descripteur de projet Maven.</li>
     <li>dépendances : Utiliser le paramètre de dépendances pour définir</li>
     <li>createdBy : Valeur de la propriété système user.name</li>
     <li>créé : Heure système actuelle</li>
     <li>requireRoot : Utiliser le paramètre requireRoot pour définir</li>
     <li>packagePath : Généré automatiquement à partir du nom du groupe et du package</li>
    </ul> </td>
  </tr>
  <tr>
   <td>requiresRoot</td>
   <td>booléen</td>
   <td>Oui</td>
   <td>false</td>
   <td>Définit si le package requiert ou non root. Cela deviendra la propriété &lt;code&gt;requiresRoot&lt;/code&gt; du fichier properties.xml.</td>
  </tr>
  <tr>
   <td>subPackages</td>
   <td>java.util.List</td>
   <td>Non</td>
   <td></td>
   <td></td>
  </tr>
  <tr>
   <td>version</td>
   <td>java.lang.String</td>
   <td>Oui</td>
   <td>Version définie dans le projet Maven.</td>
   <td>version du package de contenu.</td>
  </tr>
  <tr>
   <td>workDirectory</td>
   <td>java.io.File</td>
   <td>Oui</td>
   <td>Répertoire défini dans le projet Maven (phase build).</td>
   <td>Répertoire qui comporte le contenu à inclure dans le package.</td>
  </tr>
 </tbody>
</table>

#### Utilisation de l’élément filters {#using-filters}

Utilisez l’élément filters pour définir le contenu du package. Les filtres sont ajoutés à l’élément workspaceFilter du fichier `META-INF/vault/filter.xml` du package.

L’exemple de filtre suivant montre la structure XML à utiliser :

```xml
<filter>
   <root>/apps/myapp</root>
   <mode>merge</mode>
       <includes>
              <include>/apps/myapp/install/</include>
              <include>/apps/myapp/components</include>
       </includes>
       <excludes>
              <exclude>/apps/myapp/config/*</exclude>
       </excludes>
</filter>
```

**Mode d’importation**

L’élément `mode` définit l’impact de l’importation du package sur le contenu du référentiel. Les valeurs suivantes peuvent être utilisées :

* **Fusionner** : le contenu du package ne se trouvant pas encore dans le référentiel est ajouté. Le contenu se trouvant dans le package et le référentiel reste inchangé. Aucun contenu n’est supprimé du référentiel.
* **** Remplacer : Le contenu du package qui ne se trouve pas dans le référentiel est ajouté au référentiel. Le contenu du référentiel est remplacé par le contenu correspondant du package. Le contenu est supprimé du référentiel lorsqu’il n’existe pas dans le package.
* **Mettre à jour** : le contenu du package ne se trouvant pas dans le référentiel y est ajouté. Le contenu du référentiel est remplacé par le contenu correspondant du package. Le contenu existant est supprimé du référentiel.

Lorsque le filtre ne contient pas d’élément `mode`, la valeur `replace` par défaut est utilisée.

#### Exemple {#example-5}

L’exemple suivant illustre la création d’un package qui contient le lot OSGi workflow-mbean. Le fichier POM identifie le répertoire jcr_root en tant que valeur de la propriété builtContentDirectory. Le répertoire jcr_root contient le fichier JAR du lot dans la structure des dossiers qui reflète le référentiel :

`jcr_root/apps/myapp/install/workflow-mbean-0.03-SNAPSHOT.jar`

Comme le goal est lié à la phase de création du package, la commande suivante exécute le goal install :

`mvn package`

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
    xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="https://maven.apache.org/POM/4.0.0
    https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example.myapp</groupId>
  <artifactId>workflow-mbean</artifactId>
  <version>0.0.3-SNAPSHOT</version>

  <build>
    <plugins>
      <plugin>
        <groupId>com.day.jcr.vault</groupId>
        <artifactId>content-package-maven-plugin</artifactId>
        <version>0.0.24</version>
        <configuration>
          <builtContentDirectory>jcr_root</builtContentDirectory>
          <targetURL>https://10.36.79.223:4502/crx/packmgr/service.jsp</targetURL>
        </configuration>
        <executions>
          <execution>
            <goals>
              <goal>package</goal>
            </goals>
          </execution>
        </executions>
      </plugin>
    </plugins>
  </build>
</project>
```

Instead of expressing the `package` goal in the plugin `executions` section, you can use `content-package` as the value of the project `packaging` element:

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
    xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="https://maven.apache.org/POM/4.0.0
    https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example.myapp</groupId>
  <artifactId>workflow-mbean</artifactId>
  <version>0.0.3-SNAPSHOT</version>
  <packaging>content-package</packaging>
  <build>
    <plugins>
      <plugin>
        <groupId>com.day.jcr.vault</groupId>
        <artifactId>content-package-maven-plugin</artifactId>
        <version>0.0.24</version>
        <configuration>
          <builtContentDirectory>jcr_root</builtContentDirectory>
          <targetURL>https://10.36.79.223:4502/crx/packmgr/service.jsp</targetURL>
        </configuration>
      </plugin>
    </plugins>
  </build>
</project>
```

### help {#help}

#### Paramètres {#parameters-6}

| Nom | Type | Requis | Valeur par défaut | Description |
|---|---|---|---|---|
| detail | booléen | Non | false | Détermine si toutes les propriétés définissables doivent être affichées ou non pour chaque goal. La valeur true affiche toutes les propriétés définissables. |
| goal | Chaîne | Non |  | Nom du goal pour lequel afficher l’aide. Si aucune valeur n’est spécifiée, l’aide est affichée pour tous les goals. |
| indentSize | int | Non | 2 | Nombre d’espaces à utiliser pour la mise en retrait de chaque niveau. Si vous spécifiez une valeur, celle-ci doit être positive. |
| lineLength | int | Non | 80 | Longueur maximale d’une ligne d’affichage. Si vous spécifiez une valeur, celle-ci doit être positive. |

## Obtention du module externe Content Package Maven {#obtaining-the-content-package-maven-plugin}

Le module externe est disponible dans le référentiel Adobe public. Pour le télécharger, ajoutez le profil Maven suivant à votre fichier de paramètres Maven et activez-le. Lorsque vous utilisez une commande Maven, le module externe est téléchargé dans votre référentiel local, si nécessaire.

>[!NOTE]
>
>Le référentiel Adobe Public Releases ne peut pas être parcouru. L’accès à l’URL du référentiel à l’aide de votre navigateur web entraîne donc une erreur de page introuvable. Maven peut toutefois accéder aux répertoires du référentiel.

```xml
<profile>
    <id>adobe-public</id>
    <activation>
         <activeByDefault>false</activeByDefault>
    </activation>
    <properties>
         <releaseRepository-Id>adobe-public-releases</releaseRepository-Id>
         <releaseRepository-Name>Adobe Public Releases</releaseRepository-Name>
         <releaseRepository-URL>https://repo.adobe.com/nexus/content/groups/public</releaseRepository-URL>
    </properties>
    <repositories>
         <repository>
             <id>adobe-public-releases</id>
             <name>Adobe Basel Public Repository</name>
             <url>https://repo.adobe.com/nexus/content/groups/public</url>
             <releases>
                 <enabled>true</enabled>
                 <updatePolicy>never</updatePolicy>
             </releases>
             <snapshots>
                 <enabled>false</enabled>
             </snapshots>
         </repository>
     </repositories>
     <pluginRepositories>
         <pluginRepository>
             <id>adobe-public-releases</id>
             <name>Adobe Basel Public Repository</name>
             <url>https://repo.adobe.com/nexus/content/groups/public</url>
             <releases>
                 <enabled>true</enabled>
                 <updatePolicy>never</updatePolicy>
             </releases>
             <snapshots>
                 <enabled>false</enabled>
             </snapshots>
         </pluginRepository>
     </pluginRepositories>
</profile>
```

## Incorporation des lots OSGi dans un package de contenu {#embedding-osgi-bundles-in-a-content-package}

Utilisez le module externe Content Package Maven pour incorporer des lots OSGi dans le package de contenu. Pour incorporer le lot, implémentez les configurations suivantes :

* Le lot doit être déclaré en tant que dépendance du projet Maven.
* La configuration du module externe référence le lot à l’aide du chemin d’accès souhaité au lot dans le package.

L’exemple POM suivant illustre la création d’un package qui contient le lot UserManager Apache Sling JCR. In the package, the bundle JAR is located in the `jcr_root/apps/myapp/install` folder:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="https://maven.apache.org/POM/4.0.0"
             xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
             xsi:schemaLocation="https://maven.apache.org/POM/4.0.0
             https://maven.apache.org/maven-v4_0_0.xsd">
 <modelVersion>4.0.0</modelVersion>
   <groupId>com.adobe.example.myapp</groupId>
 <artifactId>embedded-example</artifactId>
 <packaging>content-package</packaging>
 <version>1.0.0-SNAPSHOT</version>

   <build>
 <plugins>
     <plugin>
        <groupId>com.day.jcr.vault</groupId>
      <artifactId>content-package-maven-plugin</artifactId>
      <version>0.0.24</version>
      <extensions>true</extensions>
      <configuration>
   <filters>
       <filter>
    <root>/apps/myapp</root>
       </filter>
    </filters>
    <embeddeds>
       <embedded>
    <groupId>org.apache.sling</groupId>
    <artifactId>org.apache.sling.jcr.jackrabbit.usermanager</artifactId>
    <target>/apps/myproject/install</target>
        </embedded>
    </embeddeds>
       </configuration>
  </plugin>
    </plugins>
    </build>
    <dependencies>
 <dependency>
      <groupId>org.apache.sling</groupId>
      <artifactId>org.apache.sling.jcr.jackrabbit.usermanager</artifactId>
      <version>2.2.0</version>
 </dependency>
    </dependencies>
</project>
```

## Inclusion d’une image de miniature ou d’un fichier de propriétés dans le package {#including-a-thumbnail-image-or-properties-file-in-the-package}

Remplacez les fichiers de configuration du package par défaut afin de personnaliser les propriétés du package. Incluez, par exemple, une image miniature pour différencier le package dans Package Manager et Package Share.

Dans le package, les fichiers propres à FileVault sont situés dans le dossier /META-INF/vault. Les fichiers sources peuvent se trouver n’importe où dans le système de fichiers. Dans le fichier POM, définissez les ressources de création pour copier les fichiers sources dans target/vault-work/META-INF à des fins d’inclusion dans le package.

Le code POM suivant ajoute les fichiers du dossier META-INF de la source du projet au package :

```xml
<build>
    <resources>
        <!-- vault META-INF resources (thumbnail etc.) -->
        <resource>
            <directory>${basedir}/src/main/content/META-INF</directory>
            <targetPath>../vault-work/META-INF</targetPath>
        </resource>
    </resources>
</build>
```

Le code POM ci-après ajoute uniquement une image miniature au package. L’image miniature doit être appelée thumbnail.png et figurer dans le dossier META-INF/vault/definition du package. Dans cet exemple, le fichier source se trouve dans le dossier /src/main/content/META-INF/vault/definition du projet :

```xml
<build>
    <resources>
        <!-- thumbnail only -->
        <resource>
            <directory>${basedir}/src/main/content/META-INF/vault/definition</directory>
            <targetPath>../vault-work/META-INF/vault/definition</targetPath>
        </resource>
    </resources>
</build>
```

## Using Archetypes To Generate AEM Projects {#using-archetypes-to-generate-aem-projects}

Plusieurs archétypes Maven sont disponibles pour la génération de projets AEM. Utilisez l’archetype qui correspond à vos objectifs de développement :

* A content package that installs resources for a AEM application: [simple-content-package-archetype](#simple-content-package-archetype)
* Un module de contenu qui comporte des artifacts tiers : [simple-content-package-with-embedded-archetype](#simple-content-package-with-embedded-archetype).
* Une application à plusieurs modules qui convient au développement de classes Java et de tests unitaires : [multimodule-content-package-archetype](#multimodule-content-package-archetype).

>[!NOTE]
>
>Le projet Apache Sling offre également des archétypes utiles dans le développement d’AEM. These are documented at [https://sling.apache.org/site/maven-archetypes.html](https://sling.apache.org/documentation/development/maven-archetypes.html).

Chaque archetype génère les éléments suivants :

* structure des dossiers du projet ;
* fichiers POM ;
* fichiers de configuration FileVault.

Les artifacts d’archetype sont disponibles dans le référentiel Maven public Adobe. Pour télécharger et exécuter un archetype, identifiez-le ainsi que le référentiel Adobe à l’aide des paramètres de la commande Maven archetype:generate :

```shell
mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault \
-DarchetypeArtifactId={id_of_archetype} -DarchetypeVersion=1.0.2 \
-DarchetypeRepository=adobe-public-releases
```

Le module externe d’archetype Maven utilise le mode interactif du shell ou de l’invite de commandes pour collecter des informations sur votre projet. Les informations que vous fournissez sont utilisées pour configurer diverses propriétés de projet telles que les noms des dossiers et les ID d’artifact.

**Fichiers POM**

Les fichiers POM générés comprennent des commandes de compilation de code, de création de lots et de déploiement vers AEM dans des packages. The `groupID`, `artifactId`, `version`, and `name` properties of the Maven project are automatically populated using the values that you provide to the Maven `archetype:generate` interactive prompt.

Vous pouvez modifier les valeurs par défaut suivantes dans le fichier pom.xml généré :

* The CQ server name or IP address: The default value is `localhost`. The `crx.host` element below `project/properties` contains this value.

* Numéro de port du serveur CQ : la valeur par défaut est `4502`. The `crx.port` element below `project/properties` contains this value.

*  du module externe Content Package Maven : utilisez la version la plus récente comme contenu de l’élément `version`version pour le module externe avec `artifactId` défini sur `content-package-maven-plugin`. La valeur par défaut est `0.0.24`.

**Utilisation des archetypes**

1. Dans une fenêtre shell ou une invite de commandes, saisissez la commande `archetype:generate` Maven. Lorsque vous y êtes invité, fournissez les valeurs des paramètres restants.

   Pour plus d&#39;informations sur chaque paramètre, reportez-vous à la section correspondant au type d&#39;archétype utilisé.

1. Utilisez un éditeur de texte pour ouvrir le fichier pom.xml et modifier les valeurs par défaut selon vos besoins.
1. Remplissez les dossiers générés avec des ressources.
1. Saisissez la `mvn clean install` commande.

### simple-content-package-archetype {#simple-content-package-archetype}

Crée un projet expert qui permet d’installer des ressources pour une application AEM simple. The folder structure is that used below the `/apps` folder of the AEM repository. Le POM définit les commandes permettant de compresser les ressources que vous importez dans les dossiers et d’installer les packages sur l’instance AEM.

**Propriétés de lot archetype :**

* Group ID: `com.day.jcr.vault`
* Artifact ID: `simple-content-package-archetype`
* Version: `1.0.2`
* Référentiel: `adobe-public-releases`

**Commande Maven :**

```shell
mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault \
-DarchetypeArtifactId=simple-content-package-archetype \
-DarchetypeVersion=1.0.2 \
-DarchetypeRepository=adobe-public-releases
```

**Paramètres d’archetype :**

* groupId : ID de groupe du module de contenu généré par Maven. Cette valeur est automatiquement utilisée dans le fichier POM.
* artifactId : nom du module de contenu. Cette valeur est également utilisée en tant que nom du dossier de projet.
* version : version du module de contenu. 
* package : cette valeur n’est pas utilisée pour simple-content-package-archetype.
* appsFolderName : nom du dossier sous /apps.
* artifactName : description du module de contenu.
* packageGroup : nom du groupe du module de contenu. Cette valeur configure le paramètre group du goal package du module externe Content Package.

**Structure des dossiers :**

```xml
${artifactId}
   |- pom.xml
   |- README.txt
   |- src
      |- main
         |- content
             |- jcr_root
                 |- apps
                     |- ${appsFolderName}
                            |- components
                               |- .content.xml
                            |- config
                            |- install
             |- META-INF
                 |- vault
                     |- config.xml
                     |- filter.xml
                     |- nodetypes.cnd
                     |- properties.xml
                     |- definition
                        |- .content.xml
```

### simple-content-package-with-embedded-archetype {#simple-content-package-with-embedded-archetype}

Effectue les mêmes tâches que simple-content-package-archetype, télécharge également un artifact d’un référentiel Maven public et l’inclut.

**Propriétés de lot archetype :**

* Group ID: `com.day.jcr.vault`
* Artifact ID: `simple-content-package-with-embedded-archetype`
* Version: `1.0.2`
* Référentiel: `adobe-public-releases`

**Commande Maven :**

```shell
mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault \
-DarchetypeArtifactId=simple-content-package-with-embedded-archetype \
-DarchetypeVersion=1.0.2 \
-DarchetypeRepository=adobe-public-releases
```

**Paramètres d’archetype :**

* groupId : ID de groupe du module de contenu généré par Maven. Cette valeur est automatiquement utilisée dans le fichier POM.
* artifactId : nom du module de contenu. Cette valeur est également utilisée en tant que nom du dossier de projet.
* version : version du module de contenu. 
* package : ce paramètre n’est pas utilisé.
* appsFolderName : nom du dossier sous /apps.
* artifactName : description du module de contenu.
* embeddedArtifactId : ID de l’artifact à incorporer dans le module de contenu.
* embeddedGroupId : ID de groupe de l’artifact à incorporer.
* embeddedVersion : version de l’artifact à incorporer.
* packageGroup : nom du groupe du module de contenu. Cette valeur configure le paramètre group du goal package du module externe Content Package.

**Structure des dossiers :**

```xml
${artifactId}
   |- pom.xml
   |- README.txt
   |- src
      |- main
         |- content
             |- jcr_root
                 |- apps
                     |- ${appsFolderName}
                            |- components
                            |- config
                            |- install
             |- META-INF
                 |- vault
                     |- config.xml
                     |- filter.xml
                     |- nodetypes.cnd
                     |- properties.xml
                     |- definition
```

### multimodule-content-package-archetype {#multimodule-content-package-archetype}

Crée un projet expert qui inclut la structure de dossiers pour le développement d’une application AEM et l’installation de ressources sur le serveur.

Le dossier `bundle` contient la structure des dossiers qui stocke les fichiers sources Java et JUnit que vous développez. Le fichier pom.xml contenu dans ce dossier crée le lot OSGi. Les valeurs suivantes du fichier POM identifient l’artifact et le lot :

* artifactID: `${artifactID}-bundle`.
* Bundle-SymbolicName: `${groupId}.${artifactId}-bundle`.

`${artifactID}` et `${groupId}` sont les valeurs que vous fournissez pour ces paramètres lors de l’exécution des archétypes.

The `content` folder contains the resources that are installed to the AEM instance. The value of artifactID is `${artifactID}multimodule-bundle`.

Le dossier parent contient le fichier POM parent qui gère les modules externes et les dépendances Maven.

**Propriétés de lot archetype :**

* Group ID: `com.day.jcr.vault`
* Artifact ID: `multimodule-content-package-archetype`
* Version: `1.0.2`
* Référentiel: `adobe-public-releases`

**Commande Maven :**

```shell
mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault \
-DarchetypeArtifactId=multimodule-content-package-archetype \
-DarchetypeVersion=1.0.2 \
-DarchetypeRepository=adobe-public-releases
```

**Paramètres d’archetype :**

* groupId : ID de groupe du module de contenu généré par Maven. Cette valeur est automatiquement utilisée dans le fichier POM.
* artifactId : nom du module de contenu. Cette valeur est également utilisée en tant que nom du dossier de projet.
* version : version du module de contenu. 
* package : cette valeur n’est pas utilisée pour multimodule-content-package-archetype.
* appsFolderName : nom du dossier sous /apps.
* artifactName : description du module de contenu.
* packageGroup : nom du groupe du module de contenu. Cette valeur configure le paramètre group du goal package du module externe Content Package.

**Structure des dossiers :**

```xml
${artifactId}
   |- pom.xml
   |- bundle
      |- pom.xml
      |- src
         |- main
            |- java
               |- ${groupId}
                  |- SimpleDSComponent.java
         |- test
            |- java
               |- ${groupId}
                  |- SimpleUnitTest.java
   |- content
      |- pom.xml
      |- src
         |- main
            |- content
               |- jcr_root
                  |- apps
                     |- ${appsFolderName}
                            |- config
                            |- install
                  |- META-INF
                      |- vault
                         |- config.xml
                         |- filter.xml
                         |- nodetypes.cnd
                         |- properties.xml
                         |- definition
                            |- .content.xml
```

