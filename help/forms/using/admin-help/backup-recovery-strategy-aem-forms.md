---
title: Stratégie de sauvegarde et de récupération d’AEM forms
description: Découvrez comment mettre en oeuvre une stratégie de sauvegarde des données et de synchronisation avec les données d’AEM forms.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 01ec6ebc-6d80-4417-9604-c8571aebb57e
source-git-commit: fc2f26a69c208947c14e8c6036825bb217901481
workflow-type: tm+mt
source-wordcount: '1486'
ht-degree: 25%

---

# Stratégie de sauvegarde et de récupération d’AEM forms{#backup-and-recovery-strategy-for-aem-forms}

Si votre implémentation d’AEM forms stocke des données personnalisées supplémentaires dans une autre base de données, vous devez mettre en oeuvre une stratégie de sauvegarde de ces données et vous assurer qu’elles restent synchronisées avec les données d’AEM forms. En outre, l’application doit être conçue de manière à pouvoir faire face à un scénario où les bases de données supplémentaires se désynchronisent. Il est vivement recommandé d’effectuer toute opération de base de données dans le contexte d’une transaction afin de maintenir un état cohérent.

Une fois que vous avez identifié l’utilisation d’AEM forms, déterminez les fichiers à sauvegarder, la fréquence de sauvegarde et la fenêtre de sauvegarde à mettre à disposition.

>[!NOTE]
>
>Comme pour tout autre aspect de votre mise en oeuvre d’AEM forms, votre stratégie de sauvegarde et de récupération doit être développée et testée dans un environnement de développement ou d’évaluation avant d’être utilisée en production pour vous assurer que l’ensemble de la solution fonctionne comme prévu sans perte de données.

Adobe Experience Manager (AEM) fait partie intégrante d’AEM forms. Par conséquent, vous devez sauvegarder AEM et synchroniser la sauvegarde d’AEM forms en tant que solution et services Correspondence Management, tels que Forms Manager, basés sur des données stockées dans une partie d’AEM forms. Pour éviter toute perte de données, les données spécifiques aux formulaires d’ doivent être sauvegardées de manière à garantir la corrélation entre le répertoire de stockage global de documents et les  (référentiel) et les références de base de données. Les répertoires de base, de stockage de contenu, d’ et de stockage de données doivent être restaurés sur un ordinateur portant le même nom DNS que l’original.

## Types de sauvegardes {#types-of-backups}

La stratégie de sauvegarde d’AEM forms implique deux types de sauvegardes :

**Image système :** vous pouvez utiliser cette sauvegarde complète du système pour récupérer le contenu de votre ordinateur si le disque dur ou l’ordinateur lui-même cesse de fonctionner. Une sauvegarde de l’image système n’est nécessaire qu’avant le déploiement en production d’AEM forms. Les stratégies d’entreprise internes déterminent ensuite la fréquence des sauvegardes d’image système requises.

**Données spécifiques d’AEM Forms :** les données d’application existent dans la base de données, le stockage global de documents (GDS) ainsi que le référentiel AEM et doivent être sauvegardées en temps réel. Le répertoire de stockage global de documents est utilisé pour stocker les fichiers de longue durée utilisés dans un processus. Ces fichiers peuvent inclure des PDF, des stratégies ou des modèles de formulaire.

>[!NOTE]
>
>Si Content Services (obsolète) est installé, sauvegardez également le répertoire racine de stockage de contenu. Consultez la section [Répertoire racine de stockage de contenu (Content Services uniquement)](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-directory-content-services-only).

La base de données est utilisée pour stocker les artefacts de formulaire, les configurations de service, l’état de traitement et les références de base de données dans les fichiers du répertoire de stockage global de documents. Si vous avez activé le stockage de documents dans la base de données, les données et les documents persistants dans le répertoire de stockage global de documents sont également stockés dans la base de données. La sauvegarde et la récupération de la base peuvent être réalisées à l&#39;aide des méthodes suivantes :

* **Sauvegarde instantanée** Le mode indique que le système d’AEM forms est en mode de sauvegarde indéfini ou pendant un nombre spécifié de minutes, après quoi le mode de sauvegarde n’est plus activé. Pour entrer ou quitter le mode de sauvegarde instantané, vous pouvez utiliser l’une des options suivantes. Après un scénario de récupération, le mode de sauvegarde instantané ne doit pas être activé.

   * Utilisez la page Paramètres de sauvegarde dans Administration Console. Pour passer en mode instantané, cochez la case Fonctionner en mode de sauvegarde sécurisé . Décochez la case pour quitter le mode instantané.
   * Utilisez le script LCBackupMode (voir [Sauvegarde de la base de données, du répertoire de stockage global de documents et du répertoire racine de stockage de contenu](/help/forms/using/admin-help/backing-aem-forms-data.md#back-up-the-database-gds-aem-repository-and-content-storage-root-directories)). Pour quitter le mode de sauvegarde instantané, définissez le paramètre `continuousCoverage` sur `false` ou utilisez l’option `leaveContinuousCoverage` dans l’argument du script.
   * Utilisez l’API de sauvegarde/récupération fournie. <!-- Fix broken link(see AEM forms API Reference section on AEM Forms Help and Tutorials page).-->

* **Sauvegarde restauration** Le mode indique que le système est toujours en mode de sauvegarde, avec une nouvelle session du mode de sauvegarde lancée dès que la session précédente est libérée. Aucun délai d’expiration n’est associé au mode de sauvegarde restauration. Lorsque le script LCBackupMode ou les API sont appelés pour quitter le mode de sauvegarde restauration, une nouvelle session du mode de sauvegarde restauration commence. Ce mode est utile pour la prise en charge des sauvegardes en continu tout en permettant le nettoyage des documents anciens et inutiles du répertoire de stockage global de documents. Le mode de sauvegarde restauration n’est pas pris en charge via la page Sauvegarde et récupération . Après un scénario de récupération, le mode de sauvegarde restauration est toujours activé. Vous pouvez quitter le mode de sauvegarde en continu (mode de sauvegarde restauration) en utilisant le script LCBackupMode avec l’option `leaveContinuousCoverage`.

>[!NOTE]
>
>si vous quittez le mode de sauvegarde restauration, une nouvelle session du mode de sauvegarde commence immédiatement. Pour désactiver entièrement le mode de sauvegarde restauration, utilisez l’option `leaveContinuousCoverage` dans le script, ce qui remplace la session de sauvegarde restauration existante. En mode de sauvegarde instantané, vous pouvez quitter le mode de sauvegarde comme vous le faites habituellement.

Pour éviter les pertes de données, les données spécifiques d’AEM forms doivent être sauvegardées de façon que les documents du répertoire de stockage global de documents et du répertoire racine de stockage de contenu soient en corrélation avec les références de la base de données.

>[!NOTE]
>
>Lorsque le répertoire de stockage global de documents est stocké sur le système de fichiers et non dans la base de données, effectuez la sauvegarde de la base de données avant la sauvegarde du répertoire de stockage global de documents.

## Remarques spéciales sur la sauvegarde et la récupération {#special-considerations-for-backup-and-recovery}

Suivez les instructions ci-dessous si vous devez récupérer AEM formulaires dans un environnement différent en raison des modifications suivantes :

* modification de l’adresse IP, du nom d’hôte ou du port du serveur AEM Forms ;
* Modification des lettres de lecteur ou du chemin d’accès au répertoire
* Modification d’un hôte de base de données, d’un port ou d’un nom différent

En règle générale, de tels scénarios de récupération sont provoqués par une défaillance matérielle du serveur hébergeant le serveur d’applications, le serveur de base de données ou le serveur Forms. Outre les configurations spécifiques à AEM forms décrites dans cette section, vous devez également apporter les modifications nécessaires à d’autres parties du déploiement d’AEM forms, telles que les équilibreurs de charge et les pare-feu, en cas de modification du nom d’hôte ou de l’adresse IP d’un serveur de formulaires d’AEM.

### Ce qui ne peut pas être modifié {#what-cannot-be-changed}

Même si vous pouvez modifier le serveur de base de données et de nombreux autres paramètres, vous ne pouvez pas modifier le type de serveur d’applications ou de base de données lors de la récupération d’AEM forms à partir d’une sauvegarde. Par exemple, si vous récupérez une sauvegarde d’AEM forms, vous ne pouvez pas modifier le serveur d’applications de JBoss en WebLogic ou la base de données d’Oracle en DB2. En outre, les formulaires AEM récupérés doivent utiliser les mêmes chemins d’accès au système de fichiers que le répertoire des polices.

### Redémarrage après une récupération {#restarting-after-a-recovery}

Avant de redémarrer le serveur Forms après une récupération, procédez comme suit :

1. Démarrez le système en mode de maintenance.
1. Procédez comme suit pour vous assurer que Form Manager est synchronisé avec AEM forms en mode de maintenance :

   1. Accédez à https://&lt;*serveur*>:&lt;*port*>/lc/fm et connectez-vous en utilisant les informations d’identification administrateur/mot de passe.
   1. Cliquez sur le nom de l’utilisateur (Super administrateur dans ce cas) dans le coin supérieur droit.
   1. Cliquez sur **Options d’administration**.
   1. Cliquez sur **Début** pour synchroniser les ressources du référentiel.

1. Dans un environnement organisé en grappes, le nœud principal (par rapport à AEM) doit être au-dessus des nœuds secondaires.
1. Assurez-vous qu’aucun processus n’est lancé à partir de sources internes ou externes, telles que les initiateurs de processus Web, SOAP ou EJB, jusqu’à ce que le fonctionnement normal du système soit validé.

Si la base de données d’AEM principale est déplacée ou modifiée, consultez les guides d’installation correspondant à votre serveur d’applications pour plus d’informations sur la mise à jour des informations de connexion à la base de données pour AEM sources de données IDP_DS et EDC_DS.

### Modification du nom d’hôte ou de l’adresse IP d’AEM forms {#changing-the-aem-forms-hostname-or-ip-address}

Dans une grappe, si vous utilisez la mise en cache TCP au lieu du protocole UDP, vous devez mettre à jour la configuration du localisateur de cache. Reportez-vous à « Configuration des localisateurs de mise en cache (mise en cache via TCP uniquement) », dans le guide de configuration correspondant à votre serveur d’applications.

### Modification des chemins d’accès au système de fichiers de noeud d’AEM forms {#changing-the-aem-forms-node-file-system-paths}

Si vous modifiez les chemins d’accès au système de fichiers d’un noeud autonome, vous devez mettre à jour les références appropriées dans les préférences, les autres configurations système, les applications personnalisées et les applications d’AEM déployées. D’un autre côté, pour une grappe, tous les noeuds doivent utiliser la même configuration de chemin d’accès au système de fichiers. Définissez le répertoire racine de stockage global de documents et assurez-vous qu’il pointe vers une copie du stockage global de documents récupéré, qui est synchronisé avec la base de données récupérée. Il est important de définir le chemin du répertoire de stockage global de documents, car celui-ci peut contenir des données destinées à persister au fil des redémarrages du serveur d’applications.

Dans un environnement organisé en grappe, la configuration du chemin d’accès au système de fichiers du référentiel doit être la même pour tous les noeuds de la grappe avant la sauvegarde et après la récupération.

Utilisez le script `LCSetGDS` dans le dossier `[*aem-forms root]*\sdk\misc\Foundation\SetGDSCommandline` pour définir le chemin d’accès au répertoire de stockage global de documents après avoir modifié les chemins d’accès au système de fichiers. Voir le fichier `ReadMe.txt` dans le même dossier pour plus d’informations. S’il est impossible d’utiliser l’ancien chemin du répertoire de stockage global de documents, le script `LCSetGDS` doit être utilisé pour définir le nouveau chemin d’accès à ce répertoire avant le démarrage d’AEM forms.

>[!NOTE]
>
>Il s’agit de la seule situation dans laquelle vous devez utiliser ce script pour modifier l’emplacement du répertoire de stockage global de documents. Pour modifier l’emplacement du répertoire de stockage global de documents pendant l’exécution d’AEM Forms, utilisez la console d’administration. (Consultez la section [Configurer les paramètres généraux d’AEM Forms](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)*).*

Après avoir défini le chemin d’accès au répertoire de stockage global de documents, démarrez le serveur Forms en mode de maintenance, puis utilisez Administration Console pour mettre à jour les chemins d’accès au système de fichiers restants pour le nouveau noeud. Une fois que vous avez vérifié que toutes les configurations nécessaires ont été mises à jour, redémarrez et testez AEM formulaires.
