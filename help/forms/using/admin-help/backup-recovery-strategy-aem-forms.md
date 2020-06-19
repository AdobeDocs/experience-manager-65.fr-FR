---
title: Stratégie de sauvegarde et de récupération d’AEM forms
seo-title: Stratégie de sauvegarde et de récupération d’AEM forms
description: Découvrez comment mettre en place une stratégie de sauvegarde des données et veiller à ce qu’elles restent synchronisées avec les données de formulaires AEM.
seo-description: Découvrez comment mettre en place une stratégie de sauvegarde des données et veiller à ce qu’elles restent synchronisées avec les données de formulaires AEM.
uuid: 98fc3115-76e5-4e58-aa30-3601866a441f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f192a8a3-1116-4d32-9b57-b53d532c0dbf
translation-type: tm+mt
source-git-commit: b703c59d7d913fc890c713c6e49e7d89211fd998
workflow-type: tm+mt
source-wordcount: '1520'
ht-degree: 92%

---


# Stratégie de sauvegarde et de récupération d’AEM forms{#backup-and-recovery-strategy-for-aem-forms}

Si votre déploiement d’AEM forms stocke les données personnalisées supplémentaires dans une base de données différente, il vous incombe de mettre en place une stratégie de sauvegarde pour ces données et de veiller à ce qu’elles soient synchronisées avec les données d’AEM forms. De plus, vous devez concevoir l’application de sorte à ce qu’elle puisse gérer un scénario dans lequel les bases de données supplémentaires se désynchronisent. Il est fortement recommandé d’effectuer toutes les opérations de base de données dans le contexte d’une transaction pour veiller à sa cohérence.

Après avoir identifié le mode d’utilisation d’AEM Forms, déterminez les fichiers à sauvegarder, la fréquence de sauvegarde, ainsi que la fenêtre de sauvegarde à mettre en place.

>[!NOTE]
>
>Comme pour tous les autres aspects relatifs à l’implémentation d’AEM forms, vous devez développer et tester une stratégie de sauvegarde et de récupération dans un environnement de développement ou intermédiaire avant de passer à la phase de production. Il s’agit de veiller à ce que l’intégralité de la solution fonctionne comme prévu, sans perte de données.

Adobe Experience Manager (AEM) fait partie intégrante d’AEM forms. Par conséquent, vous devez également sauvegarder AEM en synchronisation avec la sauvegarde AEM Forms, car les services et la solution Correspondence Management, tels que Forms Manager, sont basés sur les données stockées dans la partie AEM d’AEM Forms. Pour éviter toute perte de données, les données propres à AEM Forms doivent être sauvegardées de sorte que le stockage global de documents et AEM (référentiel) soient en corrélation avec les références de la base de données. La base de données, le répertoire de stockage global de documents, le répertoire AEM et le répertoire racine de stockage de contenu doivent être restaurés sur un ordinateur avec le même nom DNS que le nom d’origine.

## Types de sauvegardes {#types-of-backups}

La stratégie de sauvegarde d’AEM forms implique deux types de sauvegardes :

**Image système :** Sauvegarde complète du système que vous pouvez utiliser pour restaurer le contenu de votre ordinateur si le disque dur ou l&#39;ordinateur entier cesse de fonctionner. Une sauvegarde de l’image système doit être exécutée avant tout déploiement de production d’AEM Forms. Les stratégies internes à l’entreprise définissent ensuite la fréquence d’exécution des sauvegardes de l’image système.

**Données spécifiques à AEM forms :** Les données d’application existent dans la base de données, l’Enregistrement de Document global (GDS) et le référentiel AEM et doivent être sauvegardées en temps réel. Le répertoire de stockage global de documents est un répertoire utilisé pour stocker les fichiers de longue durée utilisés dans le cadre d’un processus. Ces fichiers comprennent des PDF, des stratégies ou des modèles de formulaires.

>[!NOTE]
>
>si Content Services (obsolète) est installé, sauvegardez également le répertoire racine de stockage de contenu See [Content Storage Root directory (Content Services only)](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-directory-content-services-only).

La base de données est utilisée pour stocker des artefacts de formulaires, des configurations de services, un état de traitement et des références de base de données dans les fichiers du répertoire de stockage global de documents. Si le stockage de documents dans la base de données est activé, les données et documents persistants du répertoire de stockage global de documents sont également stockés dans la base de données. Les méthodes suivantes permettent de sauvegarder et de récupérer la base de données :

* Le mode de **sauvegarde d’instantané** indique que le système AEM forms est en mode indéfini de sauvegarde, ou pour un nombre de minutes spécifié après lequel le mode de sauvegarde n’est plus activé. Pour passer en mode de sauvegarde instantané ou pour le quitter, vous pouvez utiliser l’une des options suivantes. Après un scénario de récupération, le mode de sauvegarde instantané ne devrait pas être activé.

   * Utilisez la page Paramètres de sauvegarde Administration Console. Pour entrer en mode instantané, cochez la case Fonctionner en mode de sauvegarde sécurisé. Désélectionnez la case pour quitter ce mode.
   * Utilisez le script LCBackupMode (voir [Sauvegarde de la base de données, du répertoire de stockage global de documents et du répertoire racine de stockage de contenu](/help/forms/using/admin-help/backing-aem-forms-data.md#back-up-the-database-gds-aem-repository-and-content-storage-root-directories)). Pour quitter le mode de sauvegarde instantané, définissez le paramètre `continuousCoverage` sur `false` ou utilisez l’option `leaveContinuousCoverage` dans l’argument du script.
   * Utilisez l’API de sauvegarde/récupération fournie. <!-- Fix broken link(see AEM forms API Reference section on AEM Forms Help and Tutorials page).-->

* Le mode de **sauvegarde restauration** indique que le système sera toujours en mode de sauvegarde et qu’une nouvelle session du mode de sauvegarde sera initiée à la libération de la session précédente. Aucun délai d’expiration n’est associé au mode de sauvegarde restauration. Lorsque le script LCBackupMode ou les API sont appelés pour quitter le mode de sauvegarde restauration, une nouvelle session du mode de sauvegarde restauration commence. Cela s’avère utile pour prendre en charge des sauvegardes en continu, tout en permettant la suppression des documents anciens et inutiles du répertoire de stockage global de documents. Le mode de sauvegarde restauration n’est pas pris en charge via la page relative à la sauvegarde et à la récupération. Après un scénario de récupération, le mode de sauvegarde restauration reste activé. Vous pouvez quitter le mode de sauvegarde en continu (mode de sauvegarde restauration) en utilisant le script LCBackupMode avec l’option `leaveContinuousCoverage`.

>[!NOTE]
>
>si vous quittez le mode de sauvegarde restauration, une nouvelle session du mode de sauvegarde commence immédiatement. Pour désactiver entièrement le mode de sauvegarde restauration, utilisez l’option `leaveContinuousCoverage` dans le script, ce qui remplace la session de sauvegarde restauration existante. Lorsque vous êtes en mode de sauvegarde instantané, vous pouvez quitter le mode de sauvegarde comme vous le faites habituellement.

Pour éviter les pertes de données, les données spécifiques d&#39;AEM forms doivent être sauvegardées de façon que les documents du répertoire de stockage global de documents et du répertoire racine de stockage de contenu soient en corrélation avec les références de la base de données.

>[!NOTE]
>
>lorsque le répertoire de stockal global de documents est stocké sur le système de fichiers et non dans la base de données, effectuez la sauvegarde de la base de données avant la sauvegarde du répertoire de stockal global de documents.

## Remarques spécifiques à la sauvegarde et la récupération {#special-considerations-for-backup-and-recovery}

Utilisez les recommandations ci-dessous si vous souhaitez récupérer AEM forms dans un environnement différent suite aux modifications suivantes :

* modification de l’adresse IP, du nom d’hôte ou du port du serveur AEM Forms ;
* modification de la lettre des lecteurs ou du chemin d’accès au répertoire ;
* passage à un hôte, un port ou un nom de base de données différents.

En règle générale, de tels scénarios de récupération se produisent suite à une défaillance matérielle du serveur hébergeant le serveur d’applications, le serveur de base de données ou le serveur Forms. En plus des configurations spécifiques d’AEM forms décrites dans cette section, vous devez également effectuer les modifications nécessaires au niveau des autres composants du déploiement d’AEM forms, tels que les services d’équilibrage de charge et les pare-feu, en cas de modification du nom d’hôte ou de l’adresse IP d’un serveur AEM forms.

### Eléments non modifiables {#what-cannot-be-changed}

Il est possible de modifier le serveur de base de données et de nombreux autres paramètres ; toutefois, la modification du type de serveur d’applications ou de base de données est impossible lors de la récupération d’AEM Forms à partir d’une sauvegarde. Par exemple, lorsque vous récupérez une sauvegarde AEM forms, vous ne pouvez pas modifier le serveur d’applications et le faire passer de JBoss à WebLogic, ni faire passer une base de données d’Oracle à DB2. De plus, la version d’AEM forms récupérée doit utiliser les mêmes chemins d’accès au système de fichiers, par exemple le répertoire des polices.

### Redémarrage post-récupération {#restarting-after-a-recovery}

Avant de redémarrer le serveur Forms après une récupération, procédez comme suit :

1. Démarrez le système en mode de maintenance.
1. Effectuez les opérations suivantes pour vous assurer que Form Manager est synchronisé avec AEM Forms en mode de maintenance :

   1. Go to https://&lt;*server*>:&lt;*port*>/lc/fm and log in using adminstrator/password credentials.
   1. Cliquez sur le nom de l’utilisateur (Super administrateur dans ce cas) dans l’angle supérieur droit.
   1. Cliquez sur **Admin Options** (Options d’administration).
   1. Cliquez sur **Start** (Démarrer) pour synchroniser les actifs du référentiel.

1. Dans un environnement organisé en grappes, le noeud principal (par rapport à AEM) doit être supérieur aux noeuds secondaires.
1. Assurez-vous qu’aucun processus n’est initialisé à partir de sources internes ou externes telles que les initiateurs de processus Web, SOAP ou EJB jusqu’à ce que le fonctionnement normal du système soit validé.

Si la base de données principale d’AEM forms est déplacée ou modifiée, consultez les guides d’installation correspondant à votre serveur d’applications pour connaître les détails de mise à jour des informations de connexion des sources de données IDP_DS et EDC_DS pour AEM Forms.

### Modification du nom d’hôte ou de l’adresse IP d’AEM Forms {#changing-the-aem-forms-hostname-or-ip-address}

Dans une grappe, lorsque vous utilisez une mise en cache TCP plutôt qu’UDP, vous devez mettre à jour la configuration du localisateur de mise en cache. Voir Configuration des localisateurs de mise en cache (mise en cache via TCP uniquement), dans le guide de configuration correspondant au serveur d’applications.

### Modification des chemins d’accès au système de fichiers des nœuds AEM forms {#changing-the-aem-forms-node-file-system-paths}

Si vous modifiez les chemins d’accès au système de fichiers d’un nœud autonome, vous devez mettre à jour les références appropriées dans les préférences, dans les autres configurations système, dans les applications personnalisées et dans les applications AEM forms déployées. Lorsqu’il s’agit d’une grappe, tous les nœuds doivent utiliser la même configuration de chemin d’accès au système de fichiers. Vous devez définir le répertoire racine de stockage global de documents et vous assurer qu’il pointe vers une copie du répertoire de stockage global de documents récupéré, lui-même synchronisé avec la base de données récupérée. La définition d’un chemin d’accès au répertoire de stockage global de documents est primordiale car ce dernier peut contenir des données conçues pour persister au fil des redémarrages du serveur d’applications.

Dans un environnement organisé en grappes, la configuration de chemin d’accès au système de fichiers du référentiel doit être la même pour tous les nœuds de grappe avant la sauvegarde et après la récupération.

Use the `LCSetGDS`script in the `[*aem-forms root]*\sdk\misc\Foundation\SetGDSCommandline` folder to set the GDS path after you change the file system paths. Voir le fichier `ReadMe.txt` dans le même dossier pour plus d’informations. S’il est impossible d’utiliser l’ancien chemin du répertoire de stockage global de documents, le script `LCSetGDS` doit être utilisé pour définir le nouveau chemin d’accès à ce répertoire avant le démarrage d&#39;AEM forms.

>[!NOTE]
>
>Il s’agit là de la seule circonstance vous permettant d’utiliser ce script pour modifier l’emplacement du répertoire de stockage global de documents. Pour modifier l’emplacement du répertoire de stockage global de documents pendant l’exécution d’AEM forms, utilisez Administration Console (See [Configure general AEM forms settings](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)*.) *

Après avoir défini le chemin d’accès au répertoire de stockage global de documents, démarrez le serveur Forms en mode de maintenance puis utilisez Administration Console pour mettre à jour les chemins d’accès au système de fichiers restants pour le nouveau nœud. Après avoir vérifié que toutes les configurations nécessaires ont été mises à jour, redémarrez et testez AEM Forms.
