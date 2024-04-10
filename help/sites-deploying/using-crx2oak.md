---
title: Utiliser l’outil de migration CRX2Oak
description: Découvrez comment utiliser l’outil de migration CRX2Oak dans Adobe Experience Manager. Cet outil est conçu pour vous aider à migrer des données entre différents référentiels.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
feature: Upgrading
exl-id: ef3895b9-8d35-4881-8188-c864ae3f0b4c
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '1175'
ht-degree: 100%

---

# Utiliser l’outil de migration CRX2Oak{#using-the-crx-oak-migration-tool}

## Présentation {#introduction}

CRX2Oak est un outil conçu pour migrer les données entre différents référentiels.

Il peut être utilisé pour migrer des données des anciennes versions de CQ basées sur Apache Jackrabbit 2 vers Oak, et il peut également être utilisé pour copier des données entre des référentiels Oak.

Vous pouvez télécharger la version la plus récente de crx2oak à partir du référentiel public Adobe via :
[https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/](https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/).

>[!NOTE]
>
>Pour plus d’informations sur Apache Oak et sur les concepts clés de persistance Adobe Experience Manager (AEM), consultez [Présentation de la plateforme AEM](/help/sites-deploying/platform.md).

## Cas d’utilisation de migration {#migration-use-cases}

L’outil peut être utilisé pour :

* migrer d’anciennes versions de CQ 5 vers AEM 6 ;
* copier des données entre plusieurs référentiels Oak ;
* convertir des données entre différentes implémentations Oak Microkernel.

La prise en charge de la migration de référentiels à l’aide de magasins Blob externes (communément appelés magasins de données) est fournie dans différentes combinaisons. Un chemin de migration possible va du référentiel CRX2 utilisant un `FileDataStore` externe vers un référentiel Oak à l’aide d’un `S3DataStore`.

Le diagramme ci-dessous montre toutes les combinaisons de migration possibles prises en charge par CRX2Oak :

![chlimage_1-151](assets/chlimage_1-151.png)

## Fonctions {#features}

CRX2Oak est appelé lors des mises à niveau d’AEM de manière à ce que l’utilisateur ou l’utilisatrice puisse spécifier un profil de migration prédéfini qui automatise la reconfiguration des modes de persistance. Il s’agit du mode de démarrage rapide.

Il peut également être exécuté séparément s’il nécessite davantage de personnalisation. Toutefois, dans ce mode, les modifications sont apportées uniquement au référentiel et toute reconfiguration supplémentaire d’AEM doit être effectuée manuellement. Il s’agit alors du mode autonome.

Notez également qu’avec les paramètres par défaut en mode autonome, seul le magasin de nœuds est migré et le nouveau référentiel réutilise l’ancien stockage binaire.

### Mode de démarrage rapide automatisé {#automated-quickstart-mode}

Depuis AEM 6.3, CRX2Oak est en mesure de gérer les profils de migration définis par les utilisateurs ou utilisatrices qui peuvent être configurés avec toutes les options de migration déjà disponibles. Cela offre une flexibilité supérieure et la possibilité d’automatiser la configuration d’AEM, des fonctionnalités qui ne sont pas disponibles si vous utilisez l’outil en mode autonome.

Pour passer CRX2Oak en mode de démarrage rapide, définissez le chemin d’accès du dossier crx-quickstart dans le répertoire d’installation AEM via cette variable d’environnement du système d’exploitation :

**Pour les systèmes UNIX et macOS :**

```shell
export SLING_HOME="/path/to/crx-quickstart"
```

**Pour Windows :**

```shell
SET "SLING_HOME=/path/to/crx-quickstart"
```

#### Prise en charge de la reprise de la migration {#resume-support}

La migration peut être interrompue à tout moment, avec la possibilité de la reprendre par la suite.

#### Logique de mise à niveau personnalisable {#customizable-upgrade-logic}

La logique Java™ personnalisée peut être mise en œuvre en utilisant `CommitHooks`. Les classes `RepositoryInitializer` personnalisées peuvent être mises en œuvre pour initialiser le référentiel avec des valeurs personnalisées.

#### Prise en charge des opérations de mappage de mémoire {#support-for-memory-mapped-operations}

CRX2Oak prend également en charge les opérations de mappage de mémoire par défaut. Le mappage de mémoire améliore considérablement les performances et doit être utilisé dans la mesure du possible.

>[!CAUTION]
>
>Notez toutefois que les opérations de mappage de la mémoire ne sont pas prises en charge pour les plateformes Windows. Il est donc recommandé d’ajouter le paramètre **--disable-mmap** lors de la migration sous Windows.

#### Migration sélective de contenu {#selective-migration-of-content}

Par défaut, le référentiel est entièrement migré sous le chemin `"/"`. Néanmoins, vous avez un contrôle total du contenu devant être migré.

S’il existe des parties de contenu qui ne sont pas nécessaires sur la nouvelle instance, vous pouvez utiliser le paramètre `--exclude-path` pour supprimer le contenu et optimiser la procédure de mise à niveau.

#### Fusion du chemin {#path-merging}

Si les données doivent être copiées entre deux référentiels différents et que vous disposez d’un chemin de contenu différent sur les deux instances, vous pouvez le définir dans le paramètre `--merge-path`. Grâce à cela, CRX2Oak copie uniquement les nouveaux nœuds dans le référentiel de destination tout en gardant les anciens nœuds en place.

![chlimage_1-152](assets/chlimage_1-152.png)

#### Prise en charge des versions {#version-support}

Par défaut, AEM crée une version de chaque page ou nœud modifiés et les stocke dans le référentiel. Les versions peuvent ensuite être utilisées pour restaurer la page à un état antérieur.

Toutefois, ces versions ne sont jamais purgées, même si la page d’origine est supprimée. Les migrations effectuées avec des référentiels utilisés depuis une longue période peuvent avoir à traiter des données redondantes en raison de versions orphelines.

Il peut être utile pour ce type de problème d’inclure le paramètre `--copy-versions`. Celui-ci peut être utilisé pour ignorer les nœuds de version durant la migration ou la copie d’un référentiel.

Vous pouvez aussi choisir de copier des versions orphelines en ajoutant le paramètre `--copy-orphaned-versions=true`.

Les deux paramètres prennent également en charge le format de date `YYYY-MM-DD` si vous désirez copier des versions jusqu’à une date donnée.

![chlimage_1-153](assets/chlimage_1-153.png)

#### Version open source {#open-source-version}

Une version open source de CRX2Oak est disponible sous la forme oak-upgrade. Elle prend en charge toutes les fonctionnalités, à l’exception des suivantes :

* prise en charge de CRX2 ;
* prise en charge des profils de migration ;
* prise en charge de la reconfiguration automatisée d’AEM.

Consultez la [documentation Apache](https://jackrabbit.apache.org/oak/docs/migration.html) pour en savoir plus.

## Paramètres {#parameters}

### Options de magasin de nœuds {#node-store-options}

* `--cache` : taille du cache en Mo (la valeur par défaut est `256`)

* `--mmap` : active l’accès aux fichiers mappés par la mémoire pour l’entrepôt de segments
* `--src-password:` mot de passe pour la base de données RDB source

* `--src-user:` : utilisateur pour la source RDB

* `--user` : utilisateur ou utilisatrice pour la cible RDB

* `--password` : mot de passe pour la cible RDB.

### Options de migration {#migration-options}

* `--early-shutdown` : arrête le référentiel source JCR2 après la duplication des nœuds et avant l’application des commit hooks.
* `--fail-on-error` : impose l’échec de la migration si les nœuds ne peuvent pas être lus à partir du référentiel source.
* `--ldap` : effectue la migration des utilisateurs LDAP d’une instance CQ 5.x vers une instance basée sur Oak. Pour que cela fonctionne, le fournisseur d’identité dans la configuration Oak doit être nommé ldap. Pour plus d’informations, voir la [documentation LDAP](/help/sites-administering/ldap-config.md).

* `--ldap-config:` Utilisez ce paramètre avec le paramètre `--ldap` pour les référentiels CQ 5.x qui ont utilisé plusieurs serveurs LDAP pour l’authentification. Vous pouvez l’utiliser pour pointer vers les fichiers de configuration CQ 5.x `ldap_login.conf` ou `jaas.conf`. Le format est `--ldapconfig=path/to/ldap_login.conf`.

### Options d’entrepôt de versions {#version-store-options}

* `--copy-orphaned-versions` : permet d’ignorer la copie des versions orphelines. Les paramètres pris en charge sont : `true`, `false` et `yyyy-mm-dd`. La valeur par défaut est `true`.

* `--copy-versions:` : copie le stockage de version. Paramètres : `true`, `false`, `yyyy-mm-dd`. La valeur par défaut est `true`.

#### Options de chemin {#path-options}

* `--include-paths:` : liste séparée par des virgules de chemins à inclure pendant la copie
* `--merge-paths` : liste séparée par des virgules de chemins à fusionner pendant la copie
* `--exclude-paths:` : liste séparée par des virgules de chemins à exclure lors de la copie

### Options d’entrepôt de blob source {#source-blob-store-options}

* `--src-datastore:` : le répertoire du magasin de données à utiliser comme `FileDataStore` source

* `--src-fileblobstore` : le répertoire du magasin de données à utiliser comme `FileBlobStore` source

* `--src-s3datastore` : le répertoire du magasin de données à utiliser comme `S3DataStore` source

* `--src-s3config` : le fichier de configuration pour le `S3DataStore` source

### Options d’entrepôt de blob cible {#destination-blobstore-options}

* `--datastore:` le répertoire du magasin de données à utiliser comme `FileDataStore` cible

* `--fileblobstore:` le répertoire du magasin de données à utiliser comme `FileBlobStore` cible

* `--s3datastore` : le répertoire du magasin de données à utiliser comme `S3DataStore` cible

* `--s3config` : le fichier de configuration pour le `S3DataStore` cible

### Options d’aide {#help-options}

* `-?, -h, --help:` affiche des informations concernant l’aide.

## Débogage {#debugging}

Vous pouvez également activer les informations de débogage pour le processus de migration afin de résoudre les éventuels problèmes pouvant survenir pendant le processus. Vous pouvez effectuer cette opération différemment selon le mode sur lequel vous souhaitez exécuter l’outil :

<table>
 <tbody>
  <tr>
   <td><strong>Mode CRX2Oak</strong></td>
   <td><strong>Action</strong></td>
  </tr>
  <tr>
   <td>Mode démarrage rapide</td>
   <td>Vous pouvez ajouter les options <strong>--log-level TRACE</strong> ou <strong>--log-level DEBUG</strong> à la ligne de commande lors de l’exécution de CRX2Oak. Dans ce mode, les journaux sont redirigés automatiquement vers le <strong>fichier upgrade.log</strong>.</td>
  </tr>
  <tr>
   <td>Mode autonome</td>
   <td><p>Ajoutez les options <strong>--trace</strong> à la ligne de commande CRX2Oak pour afficher les événements TRACE sur la sortie standard (vous devez rediriger les journaux à l’aide du caractère de redirection : ’&gt;’ ou la commande ’tee’ pour une inspection ultérieure).</p> </td>
  </tr>
 </tbody>
</table>

## Autres considérations {#other-considerations}

Lors de la migration vers un ensemble de réplications MongoDB, assurez-vous de configurer le paramètre `WriteConcern` sur `2` pour toutes les connexions aux bases de données Mongo.

Vous pouvez le faire en ajoutant le paramètre `w=2` à la fin de la chaîne de connexion, comme suit :

```xml
java -Xmx4092m -jar crx2oak.jar crx-quickstart/repository/ mongodb://localhost:27017/aem-author?replicaset=replica1&w=2
```

>[!NOTE]
>
>Pour plus d’informations, consultez la documentation de chaîne de connexion MongoDB sur les [problèmes d’écriture](https://docs.mongodb.org/manual/reference/connection-string/#write-concern-options).
