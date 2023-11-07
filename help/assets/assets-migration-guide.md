---
title: Migration des ressources en bloc
description: Décrit comment importer des ressources dans  [!DNL Adobe Experience Manager], comment appliquer des métadonnées, générer des rendus et les activer en tant qu’instances de publication.
contentOwner: AG
role: Architect, Admin
feature: Migration,Renditions,Asset Management
exl-id: 184f1645-894a-43c1-85f5-8e0d2d77aa73
source-git-commit: fc2f26a69c208947c14e8c6036825bb217901481
workflow-type: tm+mt
source-wordcount: '1791'
ht-degree: 56%

---

# Comment migrer des ressources en bloc {#assets-migration-guide}

Lors de la migration des ressources dans [!DNL Adobe Experience Manager], il existe plusieurs étapes à prendre en compte. L’extraction des ressources et des métadonnées hors de la page en cours n’est pas traitée dans ce document, car elle varie considérablement selon la mise en œuvre. Ce document explique toutefois comment récupérer ces ressources dans [!DNL Experience Manager], comment appliquer leurs métadonnées, générer des rendus et les activer pour publier des instances.

## Prérequis {#prerequisites}

Avant de suivre toute étape de cette méthode, consultez et mettez en œuvre les instructions du document [Conseils relatifs à l’optimisation des performances des ressources](performance-tuning-guidelines.md). La plupart des étapes, telles que la configuration de tâches simultanées maximales, améliorent considérablement la stabilité et les performances du serveur en charge. D’autres étapes, telles que la configuration d’un entrepôt de données basé sur les fichiers, sont beaucoup plus difficiles à exécuter une fois le système chargé avec des ressources.

>[!NOTE]
>
>Les outils de migration des ressources suivants ne font pas partie d’[!DNL Experience Manager] et ne sont pas pris en charge par Adobe :
>
>* Tools Tag Maker d’ACS AEM
>* Importateur de ressources CSV pour les outils ACS AEM
>* Gestionnaire de processus en bloc ACS Commons
>* ACS Commons Fast Action Manager
>* Processus syntaxique
>
>Ces logiciels sont Open Source et couverts par la [Licence Apache v2](https://adobe-consulting-services.github.io/pages/license.html). Pour poser une question ou signaler un problème, consultez les sections respectives [Problèmes GitHub pour les outils ACS AEM](https://github.com/Adobe-Consulting-Services/acs-aem-commons/issues) et [ACS AEM Commons](https://github.com/Adobe-Consulting-Services/acs-aem-tools/issues).

## Migrer vers [!DNL Experience Manager] {#migrating-to-aem}

La migration des ressources vers [!DNL Experience Manager] se déroule en plusieurs étapes et doit être considérée comme un processus échelonné. Les phases de migration sont les suivantes :

1. Désactivation des workflows.
1. Chargement des balises.
1. Assimilation des ressources.
1. Traitement des rendus.
1. Activation des ressources.
1. Activation des workflows.

![chlimage_1-223](assets/chlimage_1-223.png)

### Désactivation des workflows {#disabling-workflows}

Avant de commencer la migration, désactivez les lanceurs du workflow [!UICONTROL Ressource de mise à jour de la gestion des ressources numériques]. Il est préférable d’ingérer toutes les ressources dans le système, puis d’exécuter les workflows par lots. Si vous êtes déjà en ligne pendant la migration, vous pouvez planifier l’exécution de ces activités en dehors des heures de bureau.

### Chargement des balises {#loading-tags}

Vous avez peut-être déjà mis en place une taxonomie de balises que vous appliquez à vos images. Bien que la prise en charge des profils de métadonnées par des outils tels que CSV Asset Importer et l’assistance [!DNL Experience Manager] puisse automatiser le processus d’application des balises aux ressources, les balises doivent être chargées dans le système. La fonctionnalité [Tag Maker des outils d’ACS AEM](https://adobe-consulting-services.github.io/acs-aem-tools/features/tag-maker/index.html) permet de renseigner les balises à l’aide d’une feuille de calcul Microsoft Excel chargée dans le système.

### Assimilation des ressources {#ingesting-assets}

Les performances et la stabilité sont des préoccupations importantes lors de l’ingestion de ressources dans le système. Étant donné que vous chargez une grande quantité de données dans le système, vous souhaitez vous assurer que le système fonctionne correctement pour réduire le temps nécessaire et éviter de surcharger le système, ce qui peut entraîner un blocage du système, en particulier dans les systèmes déjà en production.

Il existe deux approches pour charger les ressources dans le système : une approche basée sur les notifications push utilisant HTTP ou une approche basée sur les extractions utilisant les API JCR.

#### Envoyer via HTTP {#pushing-through-http}

L’équipe Managed Services d’Adobe utilise un outil appelé Glutton pour charger des données dans les environnements clients. Glutton est une petite application Java qui charge toutes les ressources d’un répertoire dans un autre répertoire d’un déploiement [!DNL Experience Manager]. À la place de Glutton, vous pouvez également utiliser des outils tels que les scripts Perl pour publier les ressources dans le référentiel.

L’utilisation de l’approche Push à l’aide du protocole HTTPS présente deux inconvénients :

1. Les ressources doivent être transmises au serveur via HTTP. Cela nécessite pas mal de temps et est chronophage, ce qui rallonge le temps nécessaire à la migration.
1. Si des balises et des métadonnées personnalisées doivent être appliquées aux ressources, cette approche nécessite un deuxième processus personnalisé que vous devez exécuter pour appliquer ces métadonnées aux ressources après leur importation.

L’autre méthode d’ingestion de ressources consiste à extraire des ressources du système de fichiers local. Cependant, si vous ne pouvez pas obtenir un lecteur externe ou un partage réseau monté sur le serveur pour effectuer une approche basée sur l’extraction, la publication des ressources sur HTTP est la meilleure option.

#### Récupération à partir du système de fichiers local {#pulling-from-the-local-filesystem}

L’utilitaire [Tools CSV Asset Importer d’ACS AEM](https://adobe-consulting-services.github.io/acs-aem-tools/features/csv-asset-importer/index.html) extrait les ressources du système de fichiers et des métadonnées des ressources à partir d’un fichier CSV pour l’importation des ressources. L’API Experience Manager Asset Manager est utilisée pour importer les ressources dans le système et appliquer les propriétés des métadonnées configurées. Idéalement, les ressources sont montées sur le serveur via un montage de fichiers réseau ou via un lecteur externe.

Comme les ressources n’ont pas besoin d’être transmises sur un réseau, les performances globales s’améliorent considérablement et cette méthode est généralement considérée comme la méthode la plus efficace pour charger des ressources dans le référentiel. En outre, comme l’outil prend en charge l’ingestion de métadonnées, vous pouvez importer toutes les ressources et métadonnées en une seule étape plutôt que de créer une deuxième étape pour appliquer les métadonnées via un outil distinct.

### Traitement des rendus {#processing-renditions}

Après avoir chargé les ressources dans le système, vous devez les traiter via le workflow [!UICONTROL Ressource de mise à jour de la gestion des ressources numériques], afin d’extraire les métadonnées et de générer les rendus. Avant d’effectuer cette étape, vous devez dupliquer et modifier le workflow [!UICONTROL Ressource de mise à jour de la gestion des ressources numériques] pour l’adapter à vos besoins. Le workflow prêt à l’emploi contient de nombreuses étapes qui peuvent ne pas vous être nécessaires, telles que la génération de PTIFF Dynamic Media ou l’intégration du [!DNL InDesign Server].

Après avoir configuré le workflow en fonction de vos besoins, vous disposez de deux options pour l’exécuter :

1. L’approche la plus simple est la suivante : [Gestionnaire de processus en bloc d’ACS Commons](https://adobe-consulting-services.github.io/acs-aem-commons/features/bulk-workflow-manager.html). Cet outil permet d&#39;exécuter une requête et de traiter les résultats de la requête via un workflow. Il existe également des options pour définir les tailles de lots.
1. Vous pouvez utiliser l’outil [Fast Action Manager d’ACS Commons](https://adobe-consulting-services.github.io/acs-aem-commons/features/fast-action-manager.html) en association avec [Synthetic Workflows](https://adobe-consulting-services.github.io/acs-aem-commons/features/synthetic-workflow.html). Bien que cette approche soit beaucoup plus impliquée, elle vous permet de supprimer la surcharge du moteur de processus [!DNL Experience Manager], tout en optimisant l’utilisation des ressources du serveur. De plus, Fast Action Manager améliore les performances en surveillant de manière dynamique les ressources du serveur et en réduisant la charge placée sur le système. Des exemples de scripts ont été fournis sur la page de fonctionnalités d’ACS Commons.

### Activation des ressources {#activating-assets}

Pour les déploiements comportant un niveau de publication, vous devez activer les ressources vers la ferme de publication. Bien qu’Adobe recommande d’exécuter plusieurs instances de publication, il est plus efficace de répliquer toutes les ressources sur une seule instance de publication, puis de cloner cette instance. Lorsque vous activez un grand nombre de ressources, après avoir déclenché une activation d’arborescence, vous devrez peut-être intervenir. En effet, lors du déclenchement des activations, les éléments sont ajoutés à la file d’attente des tâches et des événements Sling. Une fois que la taille de cette file d’attente commence à dépasser environ 40 000 éléments, le traitement ralentit considérablement. Une fois que la taille de cette file d’attente dépasse 100 000 éléments, la stabilité du système commence à en pâtir.

Pour contourner ce problème, vous pouvez utiliser la variable [Fast Action Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/fast-action-manager.html) pour gérer la réplication des ressources. Cela fonctionne sans utiliser les files d’attente Sling, réduisant la surcharge, tout en réduisant la charge de travail pour empêcher le serveur d’être surchargé. Un exemple d’utilisation de FAM pour gérer la réplication est présenté sur la page de documentation de la fonctionnalité.

D’autres options permettant de transférer des ressources vers la batterie de serveurs de publication incluent l’utilisation de [vlt-rcp](https://jackrabbit.apache.org/filevault/rcp.html) ou [oak-run](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run), qui sont fournis en tant qu’outils dans le cadre de Jackrabbit. Une autre option consiste à utiliser un outil open-source pour votre infrastructure [!DNL Experience Manager], à savoir [Grabbit](https://github.com/TWCable/grabbit), qui se targue d’être plus rapide que vlt.

Pour toutes ces approches, notez que les ressources de l’instance de création ne s’affichent pas comme ayant été activées. Pour gérer le marquage de ces ressources avec l’état d’activation correct, vous devez également exécuter un script pour les marquer comme activées.

>[!NOTE]
>
>Adobe ne prend pas en charge Grabbit.

### Clonage de la publication {#cloning-publish}

Une fois les ressources activées, vous pouvez cloner votre instance de publication pour créer autant de copies que nécessaire pour le déploiement. Le clonage d’un serveur est relativement simple, mais il y a quelques étapes importantes à retenir. Pour cloner la publication :

1. Sauvegardez l’instance source et la banque de données.
1. Restaurez la sauvegarde de l’instance et de la banque de données à l’emplacement cible. Les étapes suivantes font toutes référence à cette nouvelle instance.
1. Recherchez `crx-quickstart/launchpad/felix` sous `sling.id` dans le système de fichiers. Supprimez ce fichier.
1. Sous le chemin d’accès racine du magasin de données, recherchez et supprimez les fichiers `repository-XXX`.
1. Modifiez `crx-quickstart/install/org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config` et `crx-quickstart/launchpad/config/org/apache/jackrabbit/oak/plugins/blob/datastore/FileDataStore.config` pour qu’ils pointent sur l’emplacement du magasin de données sur le nouvel environnement.
1. Démarrez l’environnement.
1. Mettez à jour la configuration de tous les agents de réplication sur le ou les auteurs pour qu’ils pointent vers les instances de publication ou les agents de vidage du dispatcher corrects sur la nouvelle instance afin qu’ils pointent vers les dispatchers appropriés pour le nouvel environnement.

### Activation des workflows {#enabling-workflows}

Une fois la migration terminée, les lanceurs des workflows [!UICONTROL Ressource de mise à jour de la gestion des ressources numériques] doivent être réactivés pour prendre en charge la génération des rendus et l’extraction des métadonnées pour une utilisation quotidienne continue du système.

## Migration entre les déploiements [!DNL Experience Manager] {#migrating-between-aem-instances}

Bien que ce ne soit pas aussi courant, vous devez parfois migrer de grandes quantités de données d’une instance [!DNL Experience Manager] à une autre, par exemple, lorsque vous effectuez une mise à niveau de [!DNL Experience Manager], que vous mettez à niveau votre matériel ou que vous migrez vers un nouveau centre de données, comme avec une migration AMS.

Dans ce cas, vos ressources sont déjà renseignées avec des métadonnées et des rendus sont déjà générés. Vous pouvez simplement vous concentrer sur le déplacement de ressources d’une instance à une autre. Lors de la migration entre les déploiements d’[!DNL Experience Manager], procédez comme suit :

1. Désactivation des workflows : comme vous migrez des rendus avec les ressources, vous souhaitez désactiver les lanceurs pour le workflow [!UICONTROL Ressource de mise à jour de la gestion des ressources numériques].

1. Migration des balises : comme des balises sont déjà chargées dans le déploiement source d’[!DNL Experience Manager], vous pouvez les créer dans un package de contenu et installer le package sur l’instance cible.

1. Migration des ressources : nous recommandons deux outils pour déplacer des ressources d’un déploiement d’[!DNL Experience Manager] à un autre :

   * **Vault Remote Copy** ou vlt rcp, vous permet d’utiliser vlt sur un réseau. Vous pouvez indiquer des répertoires source et de destination pour que vlt télécharge toutes les données du référentiel d’une instance et les charge dans l’autre. Vlt rcp est documenté à l’adresse [https://jackrabbit.apache.org/filevault/rcp.html](https://jackrabbit.apache.org/filevault/rcp.html)
   * **Grabbit** est un outil de synchronisation de contenu open-source développé par Time Warner Cable dans le cadre de la mise en œuvre d’[!DNL Experience Manager]. Comme il utilise des flux de données continus, en comparaison avec vlt rcp, sa latence est inférieure et il annonce une vitesse de deux à dix fois plus rapide que vlt rcp. Grabbit prend également en charge la synchronisation du contenu delta uniquement, ce qui lui permet de synchroniser les modifications une fois la migration initiale terminée.

1. Activation des ressources : suivez les instructions d’[activation des ressources](#activating-assets) documentées pour la migration initiale vers [!DNL Experience Manager].

1. Clonage de la publication : comme pour une nouvelle migration, il est plus efficace de charger une seule instance de publication et de la cloner que d’activer le contenu sur les deux nœuds. Consultez [Clonage de la publication](#cloning-publish).

1. Activation des processus : une fois la migration terminée, réactivez les lanceurs de workflow [!UICONTROL Ressource de mise à jour de la gestion des ressources numériques] afin de prendre en charge la génération des rendus et l’extraction des métadonnées pour une utilisation quotidienne continue du système.
