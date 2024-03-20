---
title: Utilisation de l’outil VLT
description: L’outil Jackrabbit FileVault (VLT) est un outil développé par The Apache Foundation. Il mappe le contenu d’une instance Jackrabbit/AEM à votre système de fichiers.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
exl-id: efbba312-9fc8-4670-b8f1-d2a86162d075
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2687'
ht-degree: 93%

---

# Utilisation de l’outil VLT {#how-to-use-the-vlt-tool}

L’outil Jackrabbit FileVault (VLT) est un outil développé par [The Apache Foundation](https://www.apache.org/) qui mappe le contenu d’une instance Jackrabbit/AEM à un système de fichiers. L’outil VLT dispose de fonctions similaires comme client du système de contrôle de code source (tel qu’un client Subversion (SVN)), offrant des opérations d’archivage, d’extraction et de gestion normales, ainsi que des options de configuration pour une représentation flexible du contenu du projet.

L’outil VLT s’exécute à partir de la ligne de commande. Ce document décrit l’utilisation de l’outil, notamment la prise en main et l’obtention d’une aide, ainsi qu’une liste de tous les éléments [Commandes](#vlt-commands) et disponibles [options](#vlt-global-options).

## Concepts et architecture {#concepts-and-architecture}

Consultez la page [Présentation de Filevault](https://jackrabbit.apache.org/filevault/overview.html) et [Vault FS](https://jackrabbit.apache.org/filevault/vaultfs.html) de la [Documentation Apache Jackrabbit Filevault](https://jackrabbit.apache.org/filevault/index.html) officielle pour une présentation approfondie des concepts et de la structure de l’outil Filevault.

## Prise en main de VLT {#getting-started-with-vlt}

Pour commencer à utiliser VLT, procédez comme suit :

1. Installez VLT, mettez à jour les variables d’environnement et mettez à jour les fichiers de subversion globaux ignorés.
1. Configurez le référentiel AEM (si ce n’est pas déjà fait).
1. Extrayez le référentiel AEM.
1. Effectuez une synchronisation avec le référentiel.
1. Vérifiez si la synchronisation a fonctionné.

### Installation de l’outil VLT {#installing-the-vlt-tool}

Pour utiliser l’outil VLT, vous devez d’abord l’installer. Il n’est pas installé par défaut car il s’agit d’un outil supplémentaire. En outre, vous devez définir la variable d’environnement de votre système.

1. Téléchargez l’archive FileVault à partir du [Référentiel d’artefacts Maven.](https://repo1.maven.org/maven2/org/apache/jackrabbit/vault/vault-cli/)
   >[!NOTE]
   >
   >La source de l’outil VLT est [disponible sur GitHub.](https://github.com/apache/jackrabbit-filevault)
1. Extrayez l’archive.
1. Ajoutez `<archive-dir>/vault-cli-<version>/bin` à votre environnement `PATH` afin que les fichiers de commande `vlt` ou `vlt.bat` soient accessibles selon les besoins. Par exemple :

   `<aem-installation-dir>/crx-quickstart/opt/helpers/vault-cli-3.1.16/bin>`

1. Ouvrez un shell de ligne de commande et exécutez `vlt --help`. Assurez-vous que la sortie est similaire à l’écran d’aide suivant :

   ```shell
   vlt --help
   -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
   Jackrabbit FileVault [version 3.1.16] Copyright 2013 by Apache Software Foundation. See LICENSE.txt for more information.
   -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
   Usage:
     vlt [options] <command> [arg1 [arg2 [arg3] ..]]
   -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
   
   Global options:
   
     -Xjcrlog <arg>           Extended JcrLog options (omit argument for help)
     -Xdavex <arg>            Extended JCR remoting options (omit argument for help)
     --credentials <arg>      The default credentials to use
     --update-credentials     if present the credentials-to-host list is updated in the ~/.vault/auth.xml
     --config <arg>           The JcrFs config to use
     -v (--verbose)           verbose output
     -q (--quiet)             print as little as possible
     --version                print the version information and exit
     --log-level <level>      the log4j log level
     -h (--help) <command>    print this help
   ```

Après l’avoir installé, vous devez mettre à jour les fichiers Subversion globaux ignorés. Modifiez vos paramètres svn et ajoutez les éléments suivants :

```xml
[miscellany]
### Set global-ignores to a set of whitespace-delimited globs
### which Subversion will ignore in its 'status' output, and
### while importing or adding files and directories.
global-ignores = .vlt
```

### Configurer le caractère de fin de ligne {#configuring-the-end-of-line-character}

VLT gère automatiquement la fin de ligne (EOL) selon les règles suivantes : 

* Les lignes des fichiers extraits sous Windows se terminent par `CRLF`.
* Les lignes des fichiers extraits sur Linux/Unix se terminent par `LF`.
* Les lignes des fichiers validés dans le référentiel se terminent par `LF`.

Pour garantir la comptabilité entre la configuration de VLT et de SVN, vous devez configurer la propriété `svn:eol-style` sur `native` pour l’extension des fichiers stockés dans le référentiel. Modifiez vos paramètres svn et ajoutez les éléments suivants :

```xml
[auto-props]
*.css = svn:eol-style=native
*.cnd = svn:eol-style=native
*.java = svn:eol-style=native
*.js = svn:eol-style=native
*.json = svn:eol-style=native
*.xjson = svn:eol-style=native
*.jsp = svn:eol-style=native
*.txt = svn:eol-style=native
*.html = svn:eol-style=native
*.xml = svn:eol-style=native
*.properties = svn:eol-style=native
```

### Extraction du référentiel {#checking-out-the-repository}

Extrayez le référentiel à l’aide du système de gestion des versions du code source. Dans svn, par exemple, saisissez ce qui suit (en remplaçant l’URI et le chemin par votre référentiel) : 

```shell
svn co https://svn.server.com/repos/myproject
```

### Synchronisation avec le référentiel {#synchronizing-with-the-repository}

Vous devez synchroniser filevault avec le référentiel. Pour ce faire :

1. Dans la ligne de commande, accédez à `content/jcr_root`.
1. Extrayez le référentiel en saisissant ce qui suit (en remplaçant **4502** par votre numéro de port et vos mots de passe d’administration) :

   ```shell
   vlt --credentials admin:admin co --force http://localhost:4502/crx
   ```

   >[!NOTE]
   >
   >Les informations d’identification doivent être spécifiées une seule fois lors de la première extraction. Elles sont ensuite stockées dans votre répertoire d’accueil dans le fichier `.vault/auth.xml`.

### Vérification de la synchronisation {#testing-whether-the-synchronization-worked}

Après avoir extrait le référentiel et l’avoir synchronisé, vous devez vous assurer que tout fonctionne correctement. Un moyen simple de le faire consiste à modifier un fichier **.jsp** pour voir si les changements sont répercutés une fois validés.

Pour tester la synchronisation :

1. Accédez à `.../jcr_content/libs/foundation/components/text`.
1. Modifiez le texte dans `text.jsp`.
1. Vérifiez les fichiers modifiés en tapant `vlt st`.
1. Vérifiez les changements en tapant `vlt diff text.jsp`.
1. Validez les modifications : `vlt ci test.jsp`.
1. Rechargez une page contenant un composant Texte et déterminez si vos modifications ont bien été appliquées.

## Obtenir de l’aide avec l’outil VLT {#getting-help-with-the-vlt-tool}

Après avoir installé l’outil VLT, vous pouvez accéder à son fichier d’aide à partir de la ligne de commande :

```shell
vlt --help
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Jackrabbit FileVault [version 3.1.16] Copyright 2013 by Apache Software Foundation. See LICENSE.txt for more information.
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Usage:
  vlt [options] <command> [arg1 [arg2 [arg3] ..]]
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Global options:
  -Xjcrlog <arg>           Extended JcrLog options (omit argument for help)
  -Xdavex <arg>            Extended JCR remoting options (omit argument for help)
  --credentials <arg>      The default credentials to use
  --update-credentials     if present the credentials-to-host list is updated in the ~/.vault/auth.xml
  --config <arg>           The JcrFs config to use
  -v (--verbose)           verbose output
  -q (--quiet)             print as little as possible
  --version                print the version information and exit
  --log-level <level>      the log4j log level
  -h (--help) <command>    print this help
Commands:
  export                   Export the Vault filesystem
  import                   Import a Vault filesystem
  checkout (co)            Checkout a Vault file system
  status (st)              Print the status of working copy files and directories.
  update (up)              Bring changes from the repository into the working copy.
  info                     Displays information about a local file.
  commit (ci)              Send changes from your working copy to the repository.
  revert (rev)             Restore pristine working copy file (undo most local edits).
  resolved (res)           Remove 'conflicted' state on working copy files or directories.
  propget (pg)             Print the value of a property on files or directories.
  proplist (pl)            Print the properties on files or directories.
  propset (ps)             Set the value of a property on files or directories.
  add                      Put files and directories under version control.
  delete (del,rm)          Remove files and directories from version control.
  diff (di)                Display the differences between two paths.
  rcp                      Remote copy of repository content.
  sync                     Control vault sync service
  console                  Run an interactive console
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
```

Pour obtenir de l’aide sur une commande particulière, saisissez la commande d’aide suivie du nom de la commande. Par exemple :

```shell
vlt --help export
Usage:
 export -v|-t <arg>|-p <uri> <jcr-path> <local-path>

Description:
  Export the Vault filesystem mounted at <uri> to the local filesystem at <local-path>. An optional <jcr-path> can be specified to export just a sub tree.
  Example:
    vlt export http://localhost:4502/crx /apps/geometrixx myproject

Options:
  -v (--verbose)          verbose output
  -t (--type) <arg>       specifies the export type. either 'platform' or 'jar'.
  -p (--prune-missing)    specifies if missing local files should be deleted.
  <uri>                   mountpoint uri
  <jcr-path>              the jcr path
  <local-path>            the local path
```

## Tâches courantes exécutées dans VLT {#common-tasks-performed-in-vlt}

Voici quelques tâches courantes effectuées dans VLT. Pour des informations détaillées sur chaque commande, reportez-vous à la description individuelle des [commandes](#vlt-commands).

### Extraction d’une sous-arborescence {#checking-out-a-subtree}

Si vous voulez uniquement extraire une sous-arborescence du référentiel, par exemple, `/apps/geometrixx`, vous pouvez le faire en tapant ce qui suit :

```shell
vlt co http://localhost:4502/crx/-/jcr:root/apps/geometrixx geo
```

Ceci crée une nouvelle racine d’exportation `geo` avec un répertoire `META-INF` et `jcr_root` et place tous les fichiers `/apps/geometrixx` dans `geo/jcr_root`.

### Réalisation d’une extraction filtrée {#performing-a-filtered-checkout}

Si vous avez configuré un filtre d’espace de travail et que vous voulez l’utiliser pour l’extraction, il faut soit d’abord créer le répertoire `META-INF/vault` et y placer le filtre, soit le spécifier sur la ligne de commande comme suit :

```shell
$ vlt co --filter filter.xml http://localhost:4502/crx/-/jcr:root geo
```

Un exemple de filtre : 

```xml
<?xml version="1.0" encoding="UTF-8"?>
<workspaceFilter version="1.0">
    <filter root="/etc/designs/geometrixx" />
    <filter root="/apps/geometrixx"/>
</workspaceFilter>
```

### Utilisation de l’import/export au lieu du contrôle .vlt {#using-import-export-instead-of-vlt-control}

Vous pouvez importer et exporter du contenu entre un référentiel JCR et le système de fichiers local sans utiliser de fichiers de contrôle.

Pour importer et exporter du contenu sans utiliser le contrôle `.vlt` :

1. configurez d’abord le référentiel :

   ```shell
   $ cd /projects
   $ svn mkdir https://svn.server.com/repos/myproject
   $ svn co https://svn.server.com/repos/myproject
   $ vlt export -v http://localhost:4502/crx /apps/geometrixx geometrixx
   $ cd geometrixx/
   $ svn add META-INF/ jcr_root/
   $ svn ci
   ```

1. modifiez la copie distante et mettez à jour JCR :

   ```shell
   $ cd /projects/geometrixx
   $ vlt -v import http://localhost:4502/crx . /
   ```

1. modifiez la copie distante et mettez à jour le serveur de fichiers : 

   ```shell
   $ cd /projects/geometrixx
   $ vlt export -v http://localhost:4502/crx /apps/geometrixx .
   $ svn st
   M      META-INF/vault/properties.xml
   M      jcr_root/apps/geometrixx/components/contentpage/.content.xml
   $ svn ci
   ```

## Utilisation de VLT {#using-vlt}

Pour exécuter des commandes dans VLT, saisissez ce qui suit sur la ligne de commande : 

```shell
vlt [options] <command> [arg1 [arg2 [arg3] ..]]  
```

Les options et commandes sont décrites en détail dans les sections suivantes.

## Options globales VLT {#vlt-global-options}

Voici une liste des options VLT disponibles pour toutes les commandes. Reportez-vous à la description individuelle de chaque commande pour plus d’informations sur les autres options disponibles.

|  |  |
|--- |--- |
| Option | Description |
| `-Xjcrlog <arg>` | Options JcrLog étendues |
| `-Xdavex <arg>` | Options de suppression JCR étendues |
| `--credentials <arg>` | Informations d’identification par défaut à utiliser |
| `--config <arg>` | Configuration JcrFs à utiliser |
| `-v (--verbose)` | Sortie verbose |
| `-q (--quiet)` | Imprimer aussi petit que possible |
| `--version` | Imprime les informations de version et quitte VLT. |
| `--log-level <level>` | Indique le niveau de journal, par exemple, le niveau de journal log4j. |
| `-h (--help) <command>` | Imprime l’aide pour cette commande spécifique. |

## Commandes VLT {#vlt-commands}

Le tableau suivant décrit toutes les commandes VLT disponibles. Reportez-vous à la description individuelle de chaque commande pour plus d’informations sur la syntaxe, les options disponibles et des exemples.

|  |  |  |
|--- |--- |--- |
| Commande | Commande abrégée | Description |
| `export` |  | Exporte à partir d’un référentiel JCR (système de fichiers Vault) vers le système de fichiers local, sans fichiers de contrôle. |
| `import` |  | Importe un système de fichiers local dans un référentiel JCR (système de fichiers Vault). |
| `checkout` | `co` | Extrait un système de fichiers Vault. Utilisez cette option pour un référentiel JCR initial dans le système de fichiers local. (Remarque : commencez par extraire le référentiel dans subversion.) |
| `analyze` |  | Analyse les packages. |
| `status` | `st` | Imprime le statut des fichiers et des répertoires de travail. |
| `update` | `up` | Importe les modifications du référentiel dans la copie de travail. |
| `info` |  | Affiche des informations relatives à un fichier local. |
| `commit` | `ci` | Valide et envoie les modifications de votre copie de travail au référentiel. |
| `revert` | `rev` | Rétablit le fichier de copie de travail à son état d’origine et annule la plupart des modifications locales. |
| `resolved` | `res` | Annule le statut conflictuel des fichiers ou répertoires de travail. |
| `propget` | `pg` | Imprime la valeur d’une propriété dans des fichiers ou répertoires. |
| `proplist` | `pl` | Imprime les propriétés dans des fichiers ou répertoires. |
| `propset` | `ps` | Définit la valeur d’une propriété sur des fichiers ou répertoires. |
| `add` |  | Place les fichiers et répertoires en contrôle de version. |
| `delete` | `del` ou `rm` | Supprime les fichiers et les répertoires de la gestion des versions. |
| `diff` | `di` | Affiche les différences entre deux chemins. |
| `console` |  | Exécute une console interactive. |
| `rcp` |  | Copie une arborescence de nœuds entre deux référentiels distants. |
| `sync` |  | Permet de contrôler le service de synchronisation Vault. |

### Exportation {#export}

Exporte le système de fichiers Vault monté sur &lt;uri> vers le système de fichiers local sur &lt;local-path>. Une &lt;jcr-path> peut être spécifié pour exporter uniquement une sous-arborescence.

#### Syntaxe {#syntax}

```shell
export -v|-t <arg>|-p <uri> <jcr-path> <local-path>
```

#### Options {#options}

|  |  |
|--- |--- |
| `-v (--verbose)` | Sortie verbose |
| `-t (--type) <arg>` | Spécifie le type d’export, qu’il s’agisse de la plateforme ou du fichier jar. |
| `-p (--prune-missing)` | Indique si les fichiers locaux manquants doivent être supprimés. |
| `<uri>` | uri de point de montage |
| `<jcrPath>` | Chemin JCR |
| `<localPath>` | chemin local |

#### Exemples {#examples}

```shell
vlt export http://localhost:4502/crx /apps/geometrixx myproject
```

### Import {#import}

Importe le système de fichiers local (en commençant par `<local-path>` dans le système de fichiers Vault sur `<uri>`. Vous pouvez définir un `<jcr-path>` en tant que racine d’importation. Si `--sync` est défini, les fichiers importés sont automatiquement soumis à un contrôle Vault.

#### Syntaxe {#syntax-1}

```shell
import -v|-s <uri> <local-path> <jcr-path>
```

#### Options {#options-1}

|  |  |
|--- |--- |
| `-v (--verbose)` | Sortie verbose |
| `-s (-- sync)` | place les fichiers locaux sous contrôle Vault |
| `<uri>` | uri de point de montage |
| `<jcrPath>` | Chemin JCR |
| `<localPath>` | chemin local |

#### Exemples {#examples-1}

```shell
vlt import http://localhost:4502/crx . /
```

### Checkout (co) {#checkout-co}

Effectue une extraction initiale à partir d’un référentiel JCR en commençant par &lt;uri> dans le système de fichiers local sur &lt;local-path>. Vous pouvez également ajouter un argument &lt;jcrPath> pour extraire un sous-répertoire de l’arborescence distante. Les filtres de l’espace de travail peuvent être spécifiés et copiés dans le répertoire META-INF.

#### Syntaxe {#syntax-2}

```shell
checkout --force|-v|-q|-f <file> <uri> <jcrPath> <localPath>  
```

#### Options {#options-2}

|  |  |
|--- |--- |
| `--force` | Force l’extraction à remplacer les fichiers locaux s’ils existent déjà. |
| `-v (--verbose)` | Sortie verbose |
| `-q (--quiet)` | Imprime aussi petit que possible. |
| `-f (--filter) <file>` | Spécifie les filtres automatiques si aucun filtre n’est défini. |
| `<uri>` | uri de point de montage |
| `<jcrPath>` | (facultatif) chemin d’accès distant |
| `<localPath>` | (facultatif) chemin d’accès local |

#### Exemples {#examples-2}

Utilisation de JCR Remoting : 

```shell
vlt --credentials admin:admin co http://localhost:8080/crx/server/crx.default/jcr_root/
```

Avec l’espace de travail par défaut : 

```shell
vlt --credentials admin:admin co http://localhost:8080/crx/server/-/jcr_root/
```

Si l’URI est incomplet, il est développé : 

```shell
vlt --credentials admin:admin co http://localhost:8080/crx
```

### Analyse {#analyze}

Analyse les packages.

#### Syntaxe {#syntax-3}

```shell
analyze -l <format>|-v|-q <localPaths1> [<localPaths2> ...]
```

#### Options {#options-3}

|  |  |
|--- |--- |
| `-l (--linkFormat) <format>` | format printf pour les liens de correctif (nom,id), par exemple, `[CQ520_HF_%s|%s]` |
| `-v (--verbose)` | Sortie verbose |
| `-q (--quiet)` | Imprime aussi petit que possible. |
| `<localPaths> [<localPaths> ...]` | chemin local |

### Statut {#status}

Imprime le statut des fichiers et des répertoires de travail.

Si `--show-update` est spécifié, chaque fichier est vérifié par rapport à la version distante. La deuxième lettre spécifie ensuite l’action qui sera effectuée par une opération de mise à jour.

#### Syntaxe {#syntax-4}

```shell
status -v|-q|-u|-N <file1> [<file2> ...]
```

#### Options {#options-4}

|  |  |
|--- |--- |
| `-v (--verbose)` | Sortie verbose |
| `-q (--quiet)` | Imprime aussi petit que possible. |
| `-u (--show-update)` | Affiche les informations de mise à jour. |
| `-N (--non-recursive)` | Fonctionne sur un seul répertoire. |
| `<file> [<file> ...]` | fichier ou répertoire dans lequel afficher le statut |

### Mettre à jour {#update}

Copie les modifications du référentiel dans la copie de travail.

#### Syntaxe {#syntax-5}

```shell
update -v|-q|--force|-N <file1> [<file2> ...]
```

#### Options {#options-5}

|  |  |
|--- |--- |
| `-v (--verbose)` | Sortie verbose |
| `-q (--quiet)` | Imprime aussi petit que possible. |
| `--force` | Force le remplacement des fichiers locaux. |
| `-N (--non-recursive)` | Fonctionne sur un seul répertoire. |
| `<file> [<file> ...]` | fichier ou répertoire à mettre à jour |

### Infos {#info}

Affiche des informations relatives à un fichier local.

#### Syntaxe {#syntax-6}

```shell
info -v|-q|-R <file1> [<file2> ...]
```

#### Options {#options-6}

|  |  |
|--- |--- |
| `-v (--verbose)` | Sortie verbose |
| `-q (--quiet)` | Imprime aussi petit que possible. |
| `-R (--recursive)` | Fonctionne de manière récursive. |
| `<file> [<file> ...]` | fichier ou répertoire d’affichage des informations |

### Commit {#commit}

Valide et envoie les modifications de votre copie de travail au référentiel.

#### Syntaxe {#syntax-7}

```shell
commit -v|-q|--force|-N <file1> [<file2> ...]
```

#### Options {#options-7}

|  |  |
|--- |--- |
| `-v (--verbose)` | Sortie verbose |
| `-q (--quiet)` | Imprime aussi petit que possible. |
| `--force` | Force la validation même si la copie distante est modifiée. |
| `-N (--non-recursive)` | Fonctionne sur un seul répertoire. |
| `<file> [<file> ...]` | fichier ou répertoire à valider |

### Rétablir {#revert}

Rétablit le fichier de la copie de travail à son état d’origine et annule la plupart des modifications locales.

#### Syntaxe {#syntax-8}

```shell
revert -q|-R <file1> [<file2> ...]
```

#### Options {#options-8}

|  |  |
|--- |--- |
| `-q (--quiet)` | Imprime aussi petit que possible. |
| `-R (--recursive)` | Descend récursivement. |
| `<file> [<file> ...]` | fichier ou répertoire à valider |

### Résolu {#resolved}

Annule le statut **conflictuel** des fichiers ou répertoires de travail.

>[!NOTE]
>
>Cette commande ne résout pas sémantiquement les conflits ni ne supprime les marqueurs de conflit ; elle supprime simplement les fichiers d’artefacts liés au conflit et permet à PATH d’être à nouveau validé.

#### Syntaxe {#syntax-9}

```shell
resolved -q|-R|--force <file1> [<file2> ...]  
```

#### Options {#options-9}

|  |  |
|--- |--- |
| `-q (--quiet)` | Imprime aussi petit que possible. |
| `-R (--recursive)` | Descend récursivement. |
| `--force` | Résout l’élément, même s’il existe des marqueurs de conflit. |
| `<file> [<file> ...]` | fichier ou répertoire à résoudre |

### Propget {#propget}

Imprime la valeur d’une propriété dans des fichiers ou répertoires.

#### Syntaxe {#syntax-10}

```shell
propget -q|-R <propname> <file1> [<file2> ...]
```

#### Options {#options-10}

|  |  |
|--- |--- |
| `-q (--quiet)` | Imprime aussi petit que possible. |
| `-R (--recursive)` | Descend récursivement. |
| `<propname>` | nom de la propriété |
| `<file> [<file> ...]` | fichier ou répertoire à partir duquel obtenir la propriété |

### Proplist {#proplist}

Imprime les propriétés dans des fichiers ou répertoires.

#### Syntaxe {#syntax-11}

```shell
proplist -q|-R <file1> [<file2> ...]
```

#### Options {#options-11}

|  |  |
|--- |--- |
| `-q (--quiet)` | Imprime aussi petit que possible. |
| `-R (--recursive)` | Descend récursivement. |
| `<file> [<file> ...]` | fichier ou répertoire à partir duquel répertorier les propriétés |

### Propset {#propset}

Définit la valeur d’une propriété sur des fichiers ou répertoires.

>[!NOTE]
>
>VLT reconnaît les propriétés versionnées spéciales suivantes :
>
>`vlt:mime-type`
>
>Le type MIME du fichier. Utilisé pour déterminer s’il faut fusionner le fichier. Un type MIME commençant par &#39;text/&#39; (ou un type MIME absent) est traité comme du texte. Tout le reste est traité comme binaire.

#### Syntaxe {#syntax-12}

```shell
propset -q|-R <propname> <propval> <file1> [<file2> ...]
```

#### Options {#options-12}

|  |  |
|--- |--- |
| `-q (--quiet)` | Imprime aussi petit que possible. |
| `-R (--recursive)` | Descend récursivement. |
| `<propname>` | nom de la propriété |
| `<propval>` | valeur de la propriété |
| `<file> [<file> ...]` | fichier ou répertoire dans lequel définir la propriété |

### Ajouter {#add}

Ajoute des fichiers et répertoires à la gestion de versions et programme leur ajout au référentiel. Ils seront ajoutés à la prochaine validation (commit).

#### Syntaxe {#syntax-13}

```shell
add -v|-q|-N|--force <file1> [<file2> ...]
```

#### Options {#options-13}

|  |  |
|--- |--- |
| `-v (--verbose)` | Sortie verbose |
| `-q (--quiet)` | Imprime aussi petit que possible. |
| `-N (--non-recursive)` | Fonctionne sur un seul répertoire. |
| `--force` | Force l’exécution de l’opération. |
| `<file> [<file> ...]` | fichier ou répertoire local à ajouter |

### Supprimer {#delete}

Supprime les fichiers et les répertoires du contrôle de version.

#### Syntaxe {#syntax-14}

```shell
delete -v|-q|--force <file1> [<file2> ...]
```

#### Options {#options-14}

|  |  |
|--- |--- |
| `-v (--verbose)` | Sortie verbose |
| `-q (--quiet)` | Imprime aussi petit que possible. |
| `--force` | Force l’exécution de l’opération. |
| `<file> [<file> ...]` | fichier ou répertoire local à supprimer |

### Diff {#diff}

Affiche les différences entre deux chemins.

#### Syntaxe {#syntax-15}

```shell
diff -N <file1> [<file2> ...]
```

#### Options {#options-15}

|  |  |
|--- |--- |
| `-N (--non-recursive)` | Fonctionne sur un seul répertoire. |
| `<file> [<file> ...]` | fichier ou répertoire dans lequel afficher les différences |

### Console {#console}

Exécute une console interactive.

#### Syntaxe {#syntax-16}

```shell
console -F <file>
```

#### Options {#options-16}

|  |  |
|--- |--- |
| `-F (--console-settings) <file>` | Spécifie le fichier de paramètres de la console. Le fichier par défaut est console.properties. |

### Rcp {#rcp}

Copie une arborescence de nœuds entre deux référentiels distants. `<src>` pointe vers le nœud source et `<dst>` indique le chemin de destination où le nœud parent doit être présent. Rcp traite les nœuds en diffusant les données en continu.

#### Syntaxe {#syntax-17}

```shell
rcp -q|-r|-b <size>|-t <seconds>|-u|-n|-e <arg1> [<arg2> ...] <src> <dst>
```

#### Options {#options-17}

|  |  |
|--- |--- |
| `-q (--quiet)` | Imprime aussi petit que possible. |
| `-r (--recursive)` | Descend de manière récursive. |
| `-b (--batchSize) <size>` | Nombre de nœuds à traiter avant un enregistrement intermédiaire. |
| `-t (--throttle) <seconds>` | Nombre de secondes à attendre après un enregistrement intermédiaire. |
| `-u (--update)` | Remplacer/supprimer des nœuds existants. |
| `-n (--newer)` | Respecter les propriétés lastModified pour la mise à jour. |
| `-e (--exclude) <arg> [<arg> ...]` | Regexp des chemins source exclus. |
| `<src>` | Adresse du référentiel de l’arborescence source. |
| `<dst>` | Adresse du référentiel du nœud de destination. |

#### Exemples {#examples-3}

```shell
vlt rcp http://localhost:4502/crx/-/jcr:root/content  https://admin:admin@localhost:4503/crx/-/jcr:root/content_copy  
```

>[!NOTE]
>
>Les options `--exclude` doivent être suivies d’une autre option avant les arguments `<src>` et `<dst>`. Par exemple :
>
>`vlt rcp -e ".*\.txt" -r`

### Sync {#sync}

Permet de contrôler le service de synchronisation Vault. Sans aucun argument, cette commande tente de soumettre le répertoire de travail en cours au contrôle de synchronisation. S’il est exécuté dans un passage en caisse vlt, il utilise le filtre et l’hôte respectifs pour configurer la synchronisation. S’il est exécuté en dehors d’un passage en caisse vlt, il enregistre le dossier actif pour synchronisation uniquement si le répertoire est vide.

#### Syntaxe {#syntax-18}

```shell
sync -v|--force|-u <uri> <command> <localPath>
```

#### Options {#options-18}

|  |  |
|--- |--- |
| `-v (--verbose)` | Sortie verbose |
| `--force` | Force l’exécution de certaines commandes. |
| `-u (--uri) <uri>` | Spécifie l’URI de l’hôte de synchronisation. |
| `<command>` | Commande sync à exécuter |
| `<localPath>` | Dossier local à synchroniser |

### Codes d’état {#status-codes}

Les codes d’état utilisés par VLT sont les suivants :

* &#39; &#39; pas de modifications
* &#39;A&#39; ajouté
* &#39;C&#39; en conflit
* &#39;D&#39; supprimé
* &#39;I&#39; ignoré
* &#39;M&#39; modifié
* &#39;R&#39; remplacé
* &#39;?’ élément non soumis à la gestion des versions
* &#39;!’ élément manquant (supprimé par une commande non-svn) ou incomplet
* &#39;~&#39; élément versionné bloqué par un objet d’un genre différent

## Configuration de la synchronisation FileVault {#setting-up-filevault-sync}

Le service de synchronisation Vault sert à synchroniser le contenu du référentiel avec une représentation locale du système de fichiers et vice versa. Pour cela, il faut installer un service OSGi qui écoutera les modifications du référentiel et analysera le contenu du système de fichiers périodiquement. Il utilise le même format de sérialisation que Vault pour mapper le contenu du référentiel avec le disque.

>[!NOTE]
>
>Le service de synchronisation Vault étant un outil de développement, il est fortement déconseillé de l’utiliser sur un système en production. En outre, le service ne peut être synchronisé qu’avec le système de fichiers local et ne peut pas être utilisé pour le développement à distance.

### Installation du service à l’aide de VLT {#installing-the-service-using-vlt}

La commande `vlt sync install` peut être utilisée pour installer automatiquement le lot de services de synchronisation Vault et sa configuration.

Le lot est installé sous `/libs/crx/vault/install` et le nœud de configuration est créé sous `/libs/crx/vault/com.day.jcr.sync.impl.VaultSyncServiceImpl`. Au départ, le service est activé, mais aucune racine de synchronisation n’est configurée.

L’exemple suivant installe le service de synchronisation sur l’instance CRX accessible par l’URI donné.

```shell
$ vlt --credentials admin:admin sync --uri http://localhost:4502/crx install
```

### Affichage de l’état du service {#displaying-the-service-status}

La commande `status` permet d’afficher des informations relatives au service de synchronisation actif. ``

```shell
$ vlt sync status --uri http://localhost:4502/crx
Connecting via JCR remoting to http://localhost:4502/crx/server
Listing sync status for http://localhost:4502/crx/server/-/jcr:root
- Sync service is enabled.
- No sync directories configured.
```

>[!NOTE]
>
>La commande `status` ne récupère aucune live data du service mais lit la configuration sous `/libs/crx/vault/com.day.jcr.sync.impl.VaultSyncServiceImpl`.

### Ajout d’un dossier de synchronisation {#adding-a-sync-folder}

La commande `register` permet d’ajouter un dossier à synchroniser à la configuration.

```shell
$ vlt sync register
Connecting via JCR remoting to http://localhost:4502/crx/server
Added new sync directory: /tmp/workspace/vltsync/jcr_root
```

>[!NOTE]
>
>La commande `register` ne déclenche pas de synchronisation tant que vous n’avez pas configuré la configuration `sync-once`.

### Suppression d’un dossier de synchronisation {#removing-a-sync-folder}

La commande `unregister` permet de supprimer un dossier à synchroniser de la configuration.

```shell
$  vlt sync unregister
Connecting via JCR remoting to http://localhost:4502/crx/server
Removed sync directory: /tmp/workspace/vltsync/jcr_root
```

>[!NOTE]
>
>Vous devez annuler l’enregistrement d’un dossier de synchronisation avant de supprimer le dossier lui-même. 

### Configuration de la synchronisation {#configuring-synchronization}

#### Configuration du service {#service-configuration}

Une fois le service en cours d’exécution, il peut être configuré avec les paramètres suivants :

* `vault.sync.syncroots` : un ou plusieurs chemins de système de fichiers locaux qui définissent les racines de synchronisation.

* `vault.sync.fscheckinterval` : fréquence (en secondes) à laquelle le système de fichiers doit être analysé pour déterminer s’il y a eu des modifications. La valeur par défaut est de 5 secondes.
* `vault.sync.enabled` : indicateur général qui active ou désactive le service.

>[!NOTE]
>
>Le service peut être configuré avec la console web ou un nœud `sling:OsgiConfig` (portant le nom `com.day.jcr.sync.impl.VaultSyncServiceImpl`) dans le référentiel.
>
>Lorsque vous utilisez AEM, il existe plusieurs méthodes de gestion des paramètres de configuration pour de tels services ; voir [Configuration d’OSGi](/help/sites-deploying/configuring-osgi.md) pour plus de détails.

#### Configuration du dossier de synchronisation {#sync-folder-configuration}

Chaque dossier de synchronisation stocke la configuration et le statut dans trois fichiers : 

* `.vlt-sync-config.properties` : fichier de configuration

* `.vlt-sync.log` : fichier journal contenant des informations sur les opérations effectuées lors de la synchronisation
* `.vlt-sync-filter.xml` : filtres qui définissent les parties du référentiel qui sont synchronisées Le format de ce fichier est décrit dans la section [Extraction filtrée](#performing-a-filtered-checkout).

Le fichier `.vlt-sync-config.properties` permet de configurer les propriétés suivantes :

**désactivé** Active ou désactive la synchronisation. Par défaut, ce paramètre est défini sur false pour permettre la synchronisation.

**sync-once** Si le paramètre n’est pas vide, l’analyse suivante synchronise le dossier dans le sens spécifié, puis le paramètre est effacé. Deux valeurs sont possibles :

* `JCR2FS` : exporte tout le contenu du référentiel JCR et écrit sur le disque local.
* `FS2JCR` : importe tout le contenu du disque dans le référentiel JCR.

**sync-log** Définit le nom du fichier journal. Par défaut, la valeur est .vlt-sync.log.

### Utilisation de la synchronisation VLT pour le développement {#using-vlt-sync-for-development}

Pour configurer un environnement de développement selon un dossier de synchronisation, procédez comme suit :

1. Extrayez le référentiel avec la ligne de commande vlt : 

   ```shell
   $ vlt --credentials admin:admin co --force http://localhost:4502/crx dev
   ```

   >[!NOTE]
   >
   >Vous pouvez utiliser des filtres pour extraire uniquement les chemins concernés. Consultez la section [Extraction filtrée](#performing-a-filtered-checkout) pour plus d’informations. 

1. Accédez au dossier racine de votre copie de travail :

   ```shell
   $ cd dev/jcr_root/
   ```

1. Installez le service de synchronisation sur votre référentiel :

   ```xml
   $ vlt sync install
   Connecting via JCR remoting to http://localhost:4502/crx/server
   Preparing to install vault-sync-2.4.24.jar...
   Updated bundle: vault-sync-2.4.24.jar
   Created new config at /libs/crx/vault/config/com.day.jcr.sync.impl.VaultSyncServiceImpl
   ```

1. Initialisez le service de synchronisation :

   ```shell
   $ vlt sync
   Connecting via JCR remoting to http://localhost:4502/crx/server
   Starting initialization of sync service in existing vlt checkout /Users/colligno/Applications/cq5/vltsync/sandbox/dev/jcr_root for http://localhost:4502/crx/server/-/jcr:root
   Added new sync directory: /Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root
   
   The directory /Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root is now enabled for syncing.
   You might perform a 'sync-once' by setting the
   appropriate flag in the /Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/.vlt-sync-config.properties file.
   ```

1. Modifiez le fichier masqué `.vlt-sync-config.properties` et configurez la synchronisation pour synchroniser le contenu de votre référentiel :

   ```xml
   sync-once=JCR2FS
   ```

   >[!NOTE]
   >
   >Cette étape télécharge l’ensemble du référentiel en fonction de la configuration des filtres.

1. Consultez le fichier journal `.vlt-sync.log` pour voir la progression :

   ```xml
   ***
   30.04.2017 14:39:10 A file:///Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/apps/geometrixx-outdoors/src/core/src/main/java/info/geometrixx/outdoors/
   30.04.2017 14:39:10 A file:///Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/apps/geometrixx-outdoors/src/core/src/main/java/info/geometrixx/outdoors/core/
   30.04.2017 14:39:10 A file:///Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/apps/geometrixx-outdoors/src/core/src/main/java/info/geometrixx/outdoors/core/product/
   30.04.2017 14:39:10 A file:///Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/apps/geometrixx-outdoors/src/core/src/main/java/info/geometrixx/outdoors/core/product/GeoProduct.java
   ***
   ```

Votre dossier local est désormais synchronisé avec le référentiel. La synchronisation est bidirectionnelle, de sorte que toute modification du référentiel est appliquée au dossier de synchronisation local, et vice versa. 

>[!NOTE]
>
>La fonction de synchronisation VLT ne prend en charge que les fichiers et dossiers simples, mais détecte les fichiers sérialisés Vault spéciaux (.content.xml, dialog.xml, etc.) et les ignore silencieusement. Il est donc possible d’utiliser la synchronisation Vault sur une extraction VLT par défaut.
