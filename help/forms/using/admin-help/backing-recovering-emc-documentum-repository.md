---
title: Sauvegarde et récupération du référentiel EMC Documentum
seo-title: Sauvegarde et récupération du référentiel EMC Documentum
description: Ce document décrit les tâches nécessaires à la sauvegarde et à la récupération du référentiel EMC Documentum configuré pour votre environnement AEM Forms.
seo-description: Ce document décrit les tâches nécessaires à la sauvegarde et à la récupération du référentiel EMC Documentum configuré pour votre environnement AEM Forms.
uuid: ab3b1fb1-25b3-4c95-801f-82d4b58f05ff
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f146202f-25f1-46a0-9943-c483f5f09f9f
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 88%

---


# Sauvegarde et récupération du référentiel EMC Documentum {#backing-up-and-recovering-the-emc-documentum-repository}

Cette section décrit les tâches nécessaires à la sauvegarde et à la récupération du référentiel EMC Documentum configuré pour votre environnement AEM Forms.

>[!NOTE]
>
>Ces instructions partent du principe qu’AEM Forms, Connecteurs pour ECM et le serveur de contenu EMC Documentum sont installés et configurés de manière appropriée.

Il est nécessaire d’exécuter les deux tâches suivantes pour les processus de sauvegarde et de restauration :

* Sauvegarde (ou restauration) de l’environnement AEM Forms.
* Sauvegarde (ou restauration) d’EMC Documentum Content Server.

>[!NOTE]
>
>Sauvegardez vos données AEM Forms avant de sauvegarder le système EMC Documentum et par la suite, restaurez le système EMC Documentum avant de restaurer l’environnement AEM Forms.

## Configuration logicielle requise {#software-requirements}

Pour pouvoir réaliser les tâches de sauvegarde nécessaires sur EMC Documentum Content Server, achetez un utilitaire tiers approprié du type EMC NetWorker auprès d’EMC ou CYA SmartRecovery pour EMC Documentum auprès de CYA. Les instructions suivantes décrivent les étapes de l’utilisation du module EMC NetWorker version 7.2.2.

Les modules EMC NetWorker suivants sont nécessaires :

* Module NetWorker
* Assistant de configuration NetWorker
* Assistant de configuration de dispositifs NetWorker
* Module NetWorker pour le type de base de données utilisé par votre serveur de contenu
* Module NetWorker pour Documentum

## Préparation d’EMC Document Content Server pour la sauvegarde et la récupération {#preparing-the-emc-document-content-server-for-backup-and-recovery}

Cette section décrit l’installation et la configuration du logiciel EMC NetWorker sur le serveur de contenu.

**Préparation du serveur EMC Documentum pour la sauvegarde**

1. Installez les modules EMC NetWorker sur EMC Documentum Content Server, en acceptant tous les paramètres par défaut.

   Durant les procédures d’installation, vous devez saisir le nom du serveur de l’ordinateur sur lequel Content Server est installé, et ce, sous la forme *Nom de serveur NetWorker*. Au moment d’installer le module EMC NetWorker concernant votre base de données, choisissez une installation « complète ».

1. En vous appuyant sur l’exemple ci-dessous, créez un fichier de configuration appelé *nsrnmd_win.cfg* et enregistrez-le sur un emplacement accessible de Content Server. Ce fichier sera appelé par les commandes de sauvegarde et de restauration.

   le texte suivant contient des caractères de formatage pour les sauts de ligne. Si vous copiez ce texte en dehors de ce document, copiez-en une partie après l’autre, puis supprimez les caractères de formatage sur le nouvel emplacement.

   ```shell
    ################################################
    # NetWorker Module for Documentum v1.2 nsrnmd_win.cfg D5.3+ example with
    # typical set of working parameters.  THIS FILE MUST BE SITE-CUSTOMISED.
    #
    # Parameters not shown can be set in this file (as per site customisation) #or from the command-line.
    #
    # Please refer to the user Guides for details on all parameters, including
    # those not listed below.
    # Note: DCTM environment for D6 is slightly different from D5, refer to D6
    # Installation Guide to update the values.
    ################################################
    #Can get values for most of below from doing as the dctm inst owner: cmd> set DOCUMENTUM=C:\Documentum
    DM_HOME=C:\Documentum\product\6.0
    JAVA_HOME=C:\Progra~1\Documentum\java\1.5.0_12
    JAVA_PATH=C:\Progra~1\Documentum\java\1.5.0_12\bin
    PATH=C:\WINNT\system32;C:\WINNT;C:\WINNT\system32\WBEM;C:\Documentum\product\6.0\bin;C:\Documentum\fulltext\fast;C:\Documentum\product\6.0\fusion;C:\Program Files\Documentum\Shared;C:\Program Files\Legato\nsr\bin;C:\Program Files\Microsoft SQL Server\80\Tools\Binn;C:\Program Files\Microsoft SQL Server\90\DTS\Binn\;C:\Program Files\Microsoft SQL Server\90\Tools\binn;C:\Program Files\Microsoft SQL Server\90\Tools\Binn\VSShell\Common7\IDE;C:\Program Files\Documentum\java\1.5.0_12\bin;C:\Documentum\config;C:\Documentum
    #See also manifest dctm.jar file for class path locations
    CLASSPATH=.;C:\Program Files\Legato\nsr\bin;C:\Program Files\Legato\nsr\bin\nsrnmdde.jar;C:\Program Files\Documentum\java\1.5.0_12\lib\tools.jar;C:\Program Files\Documentum\Shared\dfc.jar;C:\Program Files\Documentum\Shared\aspectjrt.jar;C:\Program Files\Documentum\dctm.jar;C:\Program Files\Documentum\Shared\workflow.jar;C:\Program Files\Documentum\Shared\log4j.jar;C:\Program Files\Documentum\java\1.5.0_12\lib\dt.jar;C:\Documentum\config
   
    ################################################
    #If not using nsrnmdsv -m ALL|DB|DB_LOG|FTI|FTI_ALL|ICF|SA|SA_ALL, set #for backup
    NMD_SCOPE=ALL
    #Mandatory when scope (backup or restore) is FTI/SA without -a option
    #NMD_OBJECT_NAME=filestore_01
    ################################################
    NMDDE_DM_DOCBASE=Docbase
    NMDDE_DM_USER=Administrator
    #NMDDE_DM_PASSWD must be set via running: nsrnmdsv -f <nmdcfg> -P <pwd>.
    ################################################
    #DB related hooks to invoke arbitrary scripts:
    #Set if DB is on a remote host
    #NMD_DB_HOST=dbhost
    #Pure basename implies remote host execution; absolute path ... local
    #execution as in NMD v1.0.
    #
    #Remote execution requires script be put in remote nsrexecd bin directory
    #and D5.3+ host be added to remote nsr\res\servers file w/ nsrexecd recycled
    #
    #Refer to user Guides for sample script code.
    NMD_DB_FULL_BACKUP_CMD=C:\DocumentumBackup\Scripts\nsrnmddbf.bat
    NMD_DB_LOG_BACKUP_CMD=C:\DocumentumBackup\Scripts\nsrnmddbl.bat
    NMD_DB_INCR_BACKUP_CMD=C:\DocumentumBackup\Scripts\nsrnmddbi.bat
    ################################################
    #For D5.3+ only: NMD_FTI_INCLUDED, NMD_FTI_HOST, NMD_FTI_USER,
    #NMD_FTI_PASSWD & NMD_FTI_SUBDIRS.
    #Optional for remote D5.3+ FTI server
    NMD_FTI_INCLUDED=no
    #NMD_FTI_HOST=ftihost
    #Recommended for D5.3+ FTI server quiesce/unquiesce
    #NMD_FTI_USER=ftiadmin
    #The index name: optional for D5.3+ FTI server, used with -M FTI_ALL or
    #-M ALL
    #NMD_FTI_NAME=rep_name_ftindex_01
    #Recommended for D5.3+ FTI server quiesce/unquiesce
    #NMDDE_FTI_PASSWD must be set via running: nsrnmdsv -f <nmdcfg> -P <pwd>
    #-M FTI.
    #Pure basename implies remote host execution; absolute path ... local execution
    #as in NMD v1.0.
    #
    #Remote execution requires script be put in remote nsrexecd bin directory
    #and D5.3+ host be added to remote nsr\res\servers file w/ nsrexecd
    #recycled.
    #
    #See example nsrnmdfti*.bat examples.
    #
    #Mandatory for D5.3+
    #NMD_BACKUP_FTI_QUIESCE=nsrnmdftiq.bat
    #NMD_BACKUP_FTI_UNQUIESCE=nsrnmdftiu.bat
    #Used for D5.3+ to get InstallProfile.xml FTI file in multinode
    #discovery.
    #Optional, if not specified, will treat as single-node FTI.
    #NMD_FTI_GET_INSTPROF=nsrnmdfti_instprof.bat
    #Mandatory for D5.3+. No spaces in paths or around comma separators.
    #For remote FTI, paths must be valid at the FTI host.
    #NMD_FTI_SUBDIRS=F:\Documentum_idx\data\fulltext\fixml,F:\Documentum_idx
    #\data\fulltext\index
    ################################################
    #Mandatory. No spaces in paths or before comma
    #separators in NMD_ICF_SUBDIRS_xxx:
    #NMD_ICF_INCLUDED=yes
    #NMD_ICF_SUBDIRS=C:\Documentum\dba,C:\Documentum\product\5.3
    ################################################
    NMD_FILEREPORT_INCLUDED=yes
    NMDDE_METADATA_OUTPUT_DEST=C:\docbase_freports\
    ################################################
    #Other misc recommended NMD_xxx parameters
    #Recommended to get more meaningful saveset names
    NMD_USE_DEFAULT_SAVESET_NAMES=yes
    #Use following to skip unwanted ICF, FTI and non-SnapImage SA dirs/files.
    #For example, "<</>> +skip: dm_ftwork_dir" line will skip non-data
    #files.
    #
    #The path will be the same and must exist on D5.3+, remote FTI host, and
    #RCS hosts correspondingly if used.
    #NMD_DIRECTIVES_FILE=E:\Program Files\Legato\nsr\res\nsrnmddirectives.txt
    #For non-SnapImage SA backup
    #NMD_SA_FULL_NUM_SAVESET=16
    #NMD_SA_INCR_NUM_SAVESET=4
    #NMD_USE_SNAPIMAGE=yes
    ################################################
    # DSA setup
    ################################################
    # Name of the config file at the remote sites;
    # Mandatory, listed in the config file at the primary host.
    # (if skipped, backup is treated as local)
    # NMD_RCS_CFG_FILE=rep_name_rcs.cfg
   
    # SA-host mapping add, optional, will override far-store list info.
    # No space around comma.
    # NMD_HOST_SAS_MAP=host01,sa_01,sa_02
    # NMD_HOST_SAS_MAP=host02,sa_03
    ################################################
    NSR_SERVER=con-dctm
    #NSR_CLIENT=d5svrhost
    NSR_GROUP=Default
    NSR_DATA_VOLUME_POOL=Default
    #NSR_SNAPIMAGE_DATA_VOLUME_POOL=Default
    #Relocation dir will be the same on D5+ and remote FTI/SA hosts.
    NSR_RELOCATION=C:\reloc
    #NSR_PARALLELISM=16
    NSR_DEBUG_FILE=C:\Program Files\Legato\nsr\applogs\nmd.log
    NSR_DEBUG_LEVEL=9
    ################################################
    NMDDE_DM_PASSWD=XAtup9pl
   ```

   Ne renseignez pas le champ de mot de passe du fichier de configuration `NMDDE_DM_PASSWD`. Vous définirez ce mot de passe à l’étape suivante.

1. Définissez le mot de passe du fichier de configuration comme suit :

   * Ouvrez une invite de commande et remplacez-la par `[NetWorker_root]\Legato\nsr\bin`.
   * Exécutez la commande suivante : `-nsrnmdsv.exe -f`*&lt;chemin_vers_fichier_cfg> -P &lt;mot de passe>*

1. Créez les fichiers de commande (.bat) exécutables utilisés pour sauvegarder la base de données (reportez-vous à la documentation de NetWorker). Définissez les fichiers de commandes en fonction de votre installation.

   * Sauvegarde complète de la base de données (nsrnmddbf.bat) :

      `NetWorker_database_module_root` `-s`*&lt;networker_server_name>* `-U``[username]` `-P`*[password ]*`-l full`*&lt;database_name>*

   * Sauvegarde incrémentielle de la base de données (nsrnmddbi.bat) :

      `[NetWorker_database_module_root]` `-s`*&lt;networker_server_name>* `-U``[username]` `-P``[password]` `-l 1 -R`*&lt;database_name>*

   * Sauvegarde du journal de la base de données (nsrnmddbl.bat) :

      `[NetWorker_database_module_root]` `-s``<NetWorker_Server_Name>` `-U``[username]` `-P``[password]` `-l incr -R`*&lt;database_name>*

      Où :

      `[NetWorker_database_module_root]` est le répertoire d&#39;installation du module NetWorker. Par exemple, le répertoire d’installation par défaut du module NetWorker pour SQL Server est C:\Program Files\Legato\nsr\bin\nsrsqlsv.

      `NetWorker_Server_Name` est le serveur sur lequel NetWorker est installé.

      `username` &amp;  `password` sont le nom d&#39;utilisateur et le mot de passe de l&#39;utilisateur administrateur de la base de données.

      `database_name` est le nom de la base de données à sauvegarder.

**Création d’un périphérique de sauvegarde**

1. Créez un répertoire sur le serveur EMC Documentum, puis partagez le dossier en accordant tous les droits à l’ensemble des utilisateurs.
1. Démarrez EMC NetWorker Administrator, puis cliquez sur Media Management > Devices.
1. Cliquez avec le bouton droit de la souris sur Devices et sélectionnez Create.
1. Saisissez les valeurs suivantes et cliquez sur OK :

   **Nom :** chemin d’accès complet au répertoire partagé

   **Type de support :** `File`

1. Cliquez avec le bouton droit de la souris sur le nouveau périphérique, puis sélectionnez Operations.
1. Cliquez sur Label, saisissez un nom, puis cliquez sur Mount.

Un périphérique est ajouté sur lequel les fichiers sauvegardés seront enregistrés. Vous pouvez ajouter plusieurs périphériques de formats différents.

## Sauvegarde d’EMC Documentum Content Server  {#back-up-the-emc-documentum-content-server}

Après avoir réalisé une sauvegarde complète des données AEM forms, procédez comme suit (voir [Sauvegarde des données AEM forms](/help/forms/using/admin-help/backing-aem-forms-data.md#backing-up-the-aem-forms-data)).

>[!NOTE]
>
>les scripts de commande exigent que le chemin d’accès complet soit configuré sur le fichier nsrnmd_win.cfg créé dans la section [Préparation d’EMC Document Content Server pour la sauvegarde et la récupération](backing-recovering-emc-documentum-repository.md#preparing-the-emc-document-content-server-for-backup-and-recovery).

1. Ouvrez une invite de commande et remplacez-la par `[NetWorker_root]\Legato\nsr\bin`.
1. Exécutez la commande suivante :

   ```shell
    - nsrnmdsv.exe -f <path_to_cfg_file>
   ```

## Restauration d’EMC Documentum Content Server  {#restore-the-emc-documentum-content-server}

Avant de restaurer les données de votre environnement AEM forms, procédez comme suit (voir [Récupération des données AEM forms](/help/forms/using/admin-help/recovering-aem-forms-data.md#recovering-the-aem-forms-data)).

>[!NOTE]
>
>les scripts de commande exigent que le chemin d’accès complet soit configuré sur le fichier nsrnmd_win.cfg créé dans la section [Préparation d’EMC Document Content Server pour la sauvegarde et la récupération](backing-recovering-emc-documentum-repository.md#preparing-the-emc-document-content-server-for-backup-and-recovery).

1. Arrêtez le service Docbase en cours de restauration.
1. Démarrez l’utilitaire NetWorker User pour votre module de base de données (par exemple, *NetWorker User pour SQL Server*).
1. Cliquez sur l’outil Restore, puis sélectionnez Normal.
1. A gauche de l’écran, sélectionnez la base de données correspondant à votre Docbase, puis cliquez sur le bouton Start de la barre d’outils.
1. Lorsque la base de données est restaurée, redémarrez le service Docbase.
1. Ouvrez une invite de commande et passez à *[racine_NetWorker]*\Legato\nsr\bin
1. Exécutez la commande suivante :

   ```shell
    - nsrnmdrs.exe -B <docbase_name> -f <path_to_cfg_file> -C SA
   ```
