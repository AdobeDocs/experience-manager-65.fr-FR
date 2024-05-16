---
title: Stratégie de sauvegarde et de récupération d’AEM forms
description: Découvrez comment implémenter une stratégie de sauvegarde des données et veiller à ce qu’elles soient synchronisées avec les données AEM Forms.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 01ec6ebc-6d80-4417-9604-c8571aebb57e
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '1518'
ht-degree: 100%

---

# Stratégie de sauvegarde et de récupération d’AEM forms{#backup-and-recovery-strategy-for-aem-forms}

Si votre implémentation AEM Forms stocke les données personnalisées supplémentaires dans une base de données différente, vous devez mettre en place une stratégie de sauvegarde pour ces données et veiller à ce qu’elles soient synchronisées avec les données AEM Forms. En outre, l’application doit être conçue de manière à pouvoir faire face à un scénario où les bases de données supplémentaires se désynchronisent. Il est vivement recommandé d’effectuer toute opération de base de données dans le contexte d’une transaction afin de maintenir un état cohérent.

Une fois que vous avez compris le fonctionnement d’AEM Forms, déterminez les fichiers à sauvegarder, la fréquence de sauvegarde et la fenêtre de sauvegarde à mettre à disposition.

>[!NOTE]
>
>Comme pour tous les autres aspects relatifs à l’implémentation AEM Forms, vous devez développer et tester une stratégie de sauvegarde et de récupération dans un environnement de développement ou d’évaluation avant de passer à la phase de production. Il s’agit de veiller à ce que l’intégralité de la solution fonctionne comme prévu, sans perte de données.

Adobe Experience Manager (AEM) fait partie intégrante d’AEM Forms. Par conséquent, vous devez sauvegarder AEM en synchronisation avec la sauvegarde d’AEM Forms car Correspondence Management Solution et les services, tels que Forms Manager, sont basés sur des données stockées dans la partie AEM d’AEM Forms. Pour éviter toute perte de données, les données spécifiques à AEM Forms doivent être sauvegardées de manière à garantir la corrélation entre GDS et AEM (référentiel) et les références de base de données. La base de données, GDS, AEM et les répertoires racines de stockage de contenu doivent être restaurés sur un ordinateur portant le même nom DNS que l’original.

## Types de sauvegardes {#types-of-backups}

La stratégie de sauvegarde d’AEM Forms implique deux types de sauvegardes :

**Image système :** vous pouvez utiliser cette sauvegarde complète du système pour récupérer le contenu de votre ordinateur si le disque dur ou l’ordinateur lui-même cesse de fonctionner. Une sauvegarde de l’image système n’est nécessaire qu’avant le déploiement en production d’AEM Forms. Les politiques d’entreprise internes déterminent ensuite la fréquence requise des sauvegardes d’image système.

**Données spécifiques d’AEM Forms :** les données d’application existent dans la base de données, le stockage global de documents (GDS) ainsi que le référentiel AEM et doivent être sauvegardées en temps réel. GDS est un répertoire qui sert à stocker les fichiers de longue durée utilisés dans un processus. Ces fichiers peuvent inclure des PDF, des politiques ou des modèles de formulaire.

>[!NOTE]
>
>Si Content Services (obsolète) est installé, sauvegardez également le répertoire racine de stockage de contenu. Consultez la section [Répertoire racine de stockage de contenu (Content Services uniquement)](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-directory-content-services-only).

La base de données sert à stocker les artefacts de formulaire, les configurations de service, l’état de traitement et les références de base de données dans les fichiers du GDS. Si vous avez activé le stockage de documents dans la base de données, les données et les documents persistants dans le GDS sont également stockés dans la base de données. La sauvegarde et la récupération de la base de données peuvent être réalisées à l’aide des méthodes suivantes :

* Le mode **Sauvegarde instantanée** indique que le système AEM Forms est en mode de sauvegarde indéfini ou pendant un nombre défini de minutes, après quoi le mode de sauvegarde est désactivé. Pour entrer ou quitter le mode de sauvegarde instantanée, vous pouvez utiliser l’une des options suivantes. Après un scénario de récupération, le mode de sauvegarde instantanée ne doit pas être activé.

   * Utilisez la page Paramètres de sauvegarde dans la console d’administration. Pour passer en mode instantané, cochez la case Fonctionner en mode de sauvegarde sécurisé. Décochez la case pour quitter le mode instantané.
   * Utilisez le script LCBackupMode (voir [Sauvegarde de la base de données, du GDS et des répertoires racines de stockage de contenu](/help/forms/using/admin-help/backing-aem-forms-data.md#back-up-the-database-gds-aem-repository-and-content-storage-root-directories)). Pour quitter le mode de sauvegarde instantané, définissez le paramètre `continuousCoverage` sur `false` ou utilisez l’option `leaveContinuousCoverage` dans l’argument du script.
   * Utilisez l’API de sauvegarde/récupération fournie. <!-- Fix broken link(see AEM forms API Reference section on AEM Forms Help and Tutorials page).-->

* Le mode **Sauvegarde en continu** indique que le système est toujours en mode de sauvegarde et qu’une nouvelle session en mode de sauvegarde est initiée à la fin de la session précédente. Aucun délai d’expiration n’est associé au mode de sauvegarde en continu. Lorsque le script LCBackupMode ou les API sont appelés pour quitter le mode de sauvegarde en continu, une nouvelle session du mode de sauvegarde en continu démarre. Ce mode est utile pour la prise en charge des sauvegardes en continu tout en permettant le nettoyage des documents anciens et inutiles du répertoire GDS. Le mode de sauvegarde en continu n’est pas pris en charge via la page Sauvegarde et récupération. Après un scénario de récupération, le mode de sauvegarde en continu reste activé. Vous pouvez quitter le mode de sauvegarde en continu (mode de sauvegarde restauration) en utilisant le script LCBackupMode avec l’option `leaveContinuousCoverage`.

>[!NOTE]
>
>si vous quittez le mode de sauvegarde restauration, une nouvelle session du mode de sauvegarde commence immédiatement. Pour désactiver entièrement le mode de sauvegarde restauration, utilisez l’option `leaveContinuousCoverage` dans le script, ce qui remplace la session de sauvegarde restauration existante. En mode de sauvegarde instantanée, vous pouvez quitter le mode de sauvegarde comme vous le faites habituellement.

Pour éviter les pertes de données, les données spécifiques d’AEM forms doivent être sauvegardées de façon que les documents du répertoire de stockage global de documents et du répertoire racine de stockage de contenu soient en corrélation avec les références de la base de données.

>[!NOTE]
>
>Lorsque le GDS est stocké sur le système de fichiers et non dans la base de données, effectuez la sauvegarde de la base de données avant la sauvegarde du GDS.

## Remarques spécifiques à la sauvegarde et la récupération {#special-considerations-for-backup-and-recovery}

Suivez les instructions ci-dessous si vous devez récupérer AEM Forms dans un environnement différent en raison des modifications suivantes :

* Modification de l’adresse IP, du nom d’hôte ou du port du serveur AEM Forms ;
* Modification des lettres de lecteur ou du chemin d’accès au répertoire
* Modification de l’hôte de base de données, du port ou du nom

En règle générale, de tels scénarios de récupération sont provoqués par une défaillance matérielle du serveur hébergeant le serveur d’applications, le serveur de base de données ou le serveur Forms. En plus des configurations spécifiques d&#39;AEM Forms décrites dans cette section, vous devez également effectuer les modifications nécessaires au niveau des autres composants du déploiement d&#39;AEM Forms, tels que les services d’équilibrage de charge et les pare-feu, en cas de modification du nom d’hôte ou de l’adresse IP d’un serveur AEM Forms.

### Ce qui ne peut pas être modifié {#what-cannot-be-changed}

Il est possible de modifier le serveur de base de données et de nombreux autres paramètres ; toutefois, la modification du type de serveur d’applications ou de base de données est impossible lors de la récupération d&#39;AEM Forms à partir d’une sauvegarde. Par exemple, lorsque vous récupérez une sauvegarde AEM Forms, vous ne pouvez pas modifier le serveur d’applications et le faire passer de JBoss à WebLogic, ni faire passer une base de données d’Oracle à DB2. De plus, la version d’AEM Forms récupérée doit utiliser les mêmes chemins d’accès au système de fichiers, par exemple le répertoire des polices.

### Redémarrage post-récupération {#restarting-after-a-recovery}

Avant de redémarrer le serveur Forms après une récupération, procédez comme suit :

1. Démarrez le système en mode de maintenance.
1. Effectuez les opérations suivantes pour vous assurer que Form Manager est synchronisé avec AEM Forms en mode de maintenance :

   1. Accédez à https://&lt;*serveur*>:&lt;*port*>/lc/fm et connectez-vous en utilisant les informations d’identification administrateur/mot de passe.
   1. Cliquez sur le nom de l’utilisateur ou de l’utilisatrice (Super administrateur ou Super administratrice dans ce cas) dans l’angle supérieur droit.
   1. Cliquez sur **Options d’administration**.
   1. Cliquez sur **Début** pour synchroniser les ressources du référentiel.

1. Dans un environnement organisé en grappes, le nœud principal (par rapport à AEM) doit être au-dessus des nœuds secondaires.
1. Assurez-vous qu’aucun processus n’est initialisé à partir de sources internes ou externes telles que les initiateurs de processus Web, SOAP ou EJB jusqu’à ce que le fonctionnement normal du système soit validé.

Si la base de données principale d&#39;AEM Forms est déplacée ou modifiée, consultez les guides d’installation correspondant à votre serveur d’applications pour connaître les détails de mise à jour des informations de connexion des sources de données IDP_DS et EDC_DS pour AEM Forms.

>[!NOTE]
> 
> Il est recommandé d’utiliser la commande « Ctrl + C » pour redémarrer le SDK. Le redémarrage du SDK AEM à l’aide de méthodes alternatives, par exemple l’arrêt des processus Java, peut entraîner des incohérences dans l’environnement de développement AEM.

### Modification du nom d’hôte ou de l’adresse IP d&#39;AEM Forms {#changing-the-aem-forms-hostname-or-ip-address}

Dans un cluster, lorsque vous utilisez une mise en cache TCP plutôt qu’UDP, vous devez mettre à jour la configuration du localisateur de mise en cache. Reportez-vous à « Configuration des localisateurs de mise en cache (mise en cache via TCP uniquement) », dans le guide de configuration correspondant à votre serveur d’applications.

### Modification des chemins d’accès au système de fichiers des nœuds AEM Forms {#changing-the-aem-forms-node-file-system-paths}

Si vous modifiez les chemins d’accès au système de fichiers d’un nœud autonome, vous devez mettre à jour les références appropriées dans les préférences, dans les autres configurations système, dans les applications personnalisées et dans les applications AEM Forms déployées. Lorsqu’il s’agit d’un cluster, tous les nœuds doivent utiliser la même configuration de chemin d’accès au système de fichiers. Définissez le répertoire racine de stockage global de documents (GDS) et assurez-vous qu’il pointe vers une copie du répertoire de stockage global de documents récupéré, lui-même synchronisé avec la base de données récupérée. La définition d’un chemin d’accès au répertoire de stockage global de documents est primordiale, car ce dernier peut contenir des données conçues pour persister au fil des redémarrages du serveur d’applications.

Dans un environnement organisé en clusters, la configuration de chemin d’accès au système de fichiers du référentiel doit être la même pour tous les nœuds de cluster avant la sauvegarde et après la récupération.

Utilisez le script `LCSetGDS` dans le dossier `[*aem-forms root]*\sdk\misc\Foundation\SetGDSCommandline` pour définir le chemin d’accès au répertoire de stockage global de documents après avoir modifié les chemins d’accès au système de fichiers. Voir le fichier `ReadMe.txt` dans le même dossier pour plus d’informations. S’il est impossible d’utiliser l’ancien chemin du répertoire de stockage global de documents, le script `LCSetGDS` doit être utilisé pour définir le nouveau chemin d’accès à ce répertoire avant le démarrage d’AEM forms.

>[!NOTE]
>
>Il s’agit de la seule situation dans laquelle vous devez utiliser ce script pour modifier l’emplacement du répertoire de stockage global de documents. Pour modifier l’emplacement du répertoire de stockage global de documents pendant l’exécution d’AEM Forms, utilisez la console d’administration. (Consultez la section [Configurer les paramètres généraux d’AEM Forms](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)*).*

Après avoir défini le chemin d’accès au répertoire de stockage global de documents, démarrez le serveur Forms en mode de maintenance puis utilisez la console d’administration pour mettre à jour les chemins d’accès au système de fichiers restants pour le nouveau nœud. Après avoir vérifié que toutes les configurations nécessaires ont été mises à jour, redémarrez et testez AEM Forms.
