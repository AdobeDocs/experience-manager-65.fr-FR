---
title: Migration des actifs en bloc
description: Décrit comment importer des fichiers dans  [!DNL Adobe Experience Manager], appliquer des métadonnées, générer des rendus et les activer pour publier des instances.
contentOwner: AG
role: Architecte, Administrateur
feature: Migration, Rendus, Gestion des ressources
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '1805'
ht-degree: 66%

---


# Comment migrer des ressources en vrac {#assets-migration-guide}

Lorsque vous migrez des ressources dans [!DNL Adobe Experience Manager], plusieurs étapes doivent être prises en compte. L’extraction de fichiers et de métadonnées hors de leur page d’accueil actuelle n’est pas du ressort de ce document car elle varie considérablement d’une implémentation à l’autre. Toutefois, ce document décrit comment importer ces ressources dans [!DNL Experience Manager], appliquer leurs métadonnées, générer des rendus et les activer pour publier des instances.

## Conditions préalables {#prerequisites}

Avant d&#39;effectuer l&#39;une des étapes de cette méthodologie, passez en revue et implémentez les instructions dans [Conseils d&#39;optimisation des performances des ressources](performance-tuning-guidelines.md). La plupart des étapes, telles que la configuration des tâches simultanées maximales, améliorent considérablement la stabilité et les performances du serveur en charge. D’autres étapes, telles que la configuration d’un entrepôt de données basé sur les fichiers, sont beaucoup plus difficiles à effectuer une fois le système chargé avec des ressources.

>[!NOTE]
>
>Les outils de migration d’actifs suivants ne font pas partie de [!DNL Experience Manager] et ne sont pas pris en charge par l’Adobe :
>
>* Tools Tag Maker d’ACS AEM
>* Tools CSV Asset Importer d’ACS AEM
>* Bulk Workflow Manager d’ACS Commons
>* Fast Action Manager d’ACS Commons
>* Synthetic Workflow

>
>
Ces logiciels sont Open Source et couverts par la [Licence Apache v2](https://adobe-consulting-services.github.io/pages/license.html). Pour poser une question ou signaler un problème, consultez les sections respectives [Problèmes GitHub pour les outils ACS AEM](https://github.com/Adobe-Consulting-Services/acs-aem-commons/issues) et [ACS AEM Commons](https://github.com/Adobe-Consulting-Services/acs-aem-tools/issues).

## Migrer vers [!DNL Experience Manager] {#migrating-to-aem}

La migration des ressources vers [!DNL Experience Manager] nécessite plusieurs étapes et doit être considérée comme un processus échelonné. Les phases de la migration sont les suivantes :

1. Désactivation des workflows.
1. Chargement des balises.
1. Assimilation des ressources.
1. Traitement des rendus.
1. Activation des ressources.
1. Activation des workflows.

![chlimage_1-223](assets/chlimage_1-223.png)

### Désactivez les workflows {#disabling-workflows}

Avant de commencer la migration, désactivez vos lanceurs pour le flux de travaux [!UICONTROL DAM Update Asset]. Il est préférable d’intégrer toutes les ressources dans le système, puis d’exécuter les workflows par lots. Si vous êtes déjà en ligne pendant la migration, vous pouvez planifier ces activités en dehors des heures de bureau.

### Chargement des balises {#loading-tags}

Vous avez peut-être déjà mis en place une taxonomie de balises que vous appliquez à vos images. Bien que des outils tels que CSV Asset Importer et [!DNL Experience Manager] la prise en charge des profils de métadonnées puissent automatiser le processus d’application de balises aux ressources, les balises doivent être chargées dans le système. La fonctionnalité [Tools Tag Maker d’ACS AEM](https://adobe-consulting-services.github.io/acs-aem-tools/features/tag-maker/index.html) permet de renseigner les balises à l’aide d’une feuille de calcul Microsoft Excel chargée dans le système.

### Ingestion des ressources {#ingesting-assets}

Les performances et la stabilité sont des préoccupations importantes lors de l’intégration des ressources dans le système. Comme vous chargez une grande quantité de données dans le système, vous devez vous assurer que le système fonctionne le mieux possible, afin de minimiser le temps nécessaire et d’éviter de surcharger le système, ce qui peut entraîner un blocage de ce dernier, en particulier des systèmes déjà en production.

Il existe deux approches pour charger les ressources dans le système : une approche basée sur le push utilisant le protocole HTTP ou une approche basée sur l’extraction utilisant les API JCR.

#### Envoyer via HTTP {#pushing-through-http}

L’équipe Managed Services d’Adobe utilise un outil appelé Glutton pour charger les données dans les environnements clients. Glutton est une petite application Java qui charge toutes les ressources d&#39;un répertoire dans un autre répertoire d&#39;un déploiement [!DNL Experience Manager]. À la place de Glutton, vous pouvez également utiliser des outils tels que les scripts Perl pour publier les ressources dans le référentiel.

L’utilisation de l’approche Push à l’aide du protocole HTTPS présente deux inconvénients :

1. Les ressources doivent être transmises au serveur via HTTP. Cette transmission nécessite beaucoup de temps et crée une surcharge, ce qui rallonge le temps nécessaire pour effectuer la migration.
1. Si vous disposez de balises et de métadonnées personnalisées devant être appliquées aux ressources, cette approche nécessite un deuxième processus personnalisé que vous devez exécuter pour appliquer ces métadonnées aux ressources une fois qu’elles ont été importées.

L’autre approche de l’intégration des ressources consiste à extraire les ressources du système de fichiers local. Toutefois, si vous ne parvenez pas à obtenir un lecteur externe ou un partage réseau monté sur le serveur pour effectuer une approche par extraction, la publication des ressources en utilisant HTTP est la meilleure option.

#### Récupérer à partir du système de fichiers local {#pulling-from-the-local-filesystem}

L’utilitaire [Tools CSV Asset Importer d’ACS AEM](https://adobe-consulting-services.github.io/acs-aem-tools/features/csv-asset-importer/index.html) extrait les ressources du système de fichiers et des métadonnées des ressources à partir d’un fichier CSV pour l’importation des ressources. L’API Asset Manager du Experience Manager est utilisée pour importer les ressources dans le système et appliquer les propriétés de métadonnées configurées. Idéalement, les ressources sont montées sur le serveur via un montage de fichiers réseau ou via un lecteur externe.

Comme il n’est pas nécessaire que les ressources soient transmises sur un réseau, les performances globales s’améliorent considérablement et cette méthode est généralement considérée comme le moyen le plus efficace de charger des ressources dans le référentiel. En outre, comme l’outil prend en charge l’assimilation des métadonnées, vous pouvez importer toutes les ressources et métadonnées en une seule étape plutôt que de créer une deuxième étape pour appliquer les métadonnées via un outil distinct.

### Traitement des rendus {#processing-renditions}

Après avoir chargé les ressources dans le système, vous devez les traiter via le processus [!UICONTROL DAM Update Asset] pour extraire les métadonnées et générer des rendus. Avant d&#39;exécuter cette étape, vous devez duplicata et modifier le flux de travaux [!UICONTROL DAM Update Asset] en fonction de vos besoins. Le processus prêt à l’emploi contient de nombreuses étapes qui peuvent ne pas être nécessaires pour vous, telles que la génération Dynamic Media PTIFF ou l’intégration [!DNL InDesign Server].

Après avoir configuré le workflow en fonction de vos besoins, vous disposez de deux options pour l’exécuter :

1. L’approche la plus simple consiste à utiliser l’outil [Bulk Workflow Manager d’ACS Commons](https://adobe-consulting-services.github.io/acs-aem-commons/features/bulk-workflow-manager.html). Cet outil permet d’exécuter une requête et de traiter les résultats de la requête via un workflow. Il existe également des options permettant de définir la taille des lots.
1. Vous pouvez utiliser l’outil [Fast Action Manager d’ACS Commons](https://adobe-consulting-services.github.io/acs-aem-commons/features/fast-action-manager.html) en association avec [Synthetic Workflows](https://adobe-consulting-services.github.io/acs-aem-commons/features/synthetic-workflow.html). Bien que cette approche soit beaucoup plus impliquée, elle vous permet de supprimer les frais généraux du moteur de workflow [!DNL Experience Manager] tout en optimisant l&#39;utilisation des ressources serveur. De plus, Fast Action Manager améliore les performances en surveillant de manière dynamique les ressources du serveur et en réduisant la charge placée sur le système. Des exemples de scripts ont été fournis sur la page de fonctionnalités d’ACS Commons.

### Activation des ressources {#activating-assets}

Pour les déploiements disposant d’un niveau de publication, vous devez activer les ressources dans la ferme de serveurs de publication. Bien qu’Adobe recommande d’exécuter plusieurs instances de publication, il est plus efficace de répliquer toutes les ressources sur une seule instance de publication, puis de cloner cette instance. Lorsque vous activez un grand nombre de ressources, après le déclenchement d’une activation d’arborescence, vous devrez peut-être intervenir. Voici pourquoi : Lors du déclenchement d’activations, des éléments sont ajoutés aux tâches/files d&#39;événements Sling. Une fois que la taille de cette file d’attente commence à dépasser environ 40 000 éléments, le traitement ralentit considérablement. Lorsque la taille de cette file d’attente dépasse 100 000 éléments, la stabilité du système commence à souffrir.

Pour contourner ce problème, vous pouvez utiliser l’outil [Fast Action Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/fast-action-manager.html) pour gérer la réplication des ressources. Il fonctionne sans utiliser les files d’attente Sling, réduisant les surcharges, tout en régulant la charge de travail pour éviter que le serveur ne soit surchargé. Un exemple d’utilisation de cet outil pour gérer la réplication est présenté sur la page de documentation de FAM.

D’autres options permettant de transférer des ressources vers la batterie de serveurs de publication incluent l’utilisation de [vlt-rcp](https://jackrabbit.apache.org/filevault/rcp.html) ou [oak-run](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run), qui sont fournis en tant qu’outils dans le cadre de Jackrabbit. Une autre option consiste à utiliser un outil open-source pour votre infrastructure [!DNL Experience Manager] appelée [Grabbit](https://github.com/TWCable/grabbit), qui prétend avoir des performances plus rapides que vlt.

Pour toutes ces approches, notez que les ressources de l’instance de création ne s’affichent pas comme ayant été activées. Pour marquer ces ressources avec l’état d’activation correct, vous devez également exécuter un script les marquant comme activées.

>[!NOTE]
>
>Adobe ne prend pas en charge Grabbit.

### Cloner la publication {#cloning-publish}

Une fois les ressources activées, vous pouvez cloner votre instance de publication afin de créer autant de copies que nécessaire pour le déploiement. Le clonage d’un serveur est relativement simple, mais il existe quelques étapes importantes à retenir. Pour cloner la publication :

1. Sauvegardez l’instance source et la banque de données.
1. Restaurez la sauvegarde de l’instance et de la banque de données à l’emplacement cible. Les étapes suivantes se rapportent toutes à cette nouvelle instance.
1. Recherchez `crx-quickstart/launchpad/felix` sous `sling.id` dans le système de fichiers. Supprimez ce fichier.
1. Sous le chemin d’accès racine du magasin de données, recherchez et supprimez les fichiers `repository-XXX`.
1. Modifiez `crx-quickstart/install/org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config` et `crx-quickstart/launchpad/config/org/apache/jackrabbit/oak/plugins/blob/datastore/FileDataStore.config` pour qu’ils pointent sur l’emplacement du magasin de données sur le nouvel environnement.
1. Démarrez l’environnement.
1. Mettez à jour la configuration de tous les agents de réplication sur le ou les auteurs afin de pointer vers les instances de publication ou les agents de vidage du Dispatcher corrects sur la nouvelle instance. Cela permet de pointer vers les Dispatchers appropriés du nouvel environnement.

### Activation des workflows {#enabling-workflows}

Une fois la migration terminée, les lanceurs des workflows [!UICONTROL DAM Update Asset] doivent être réactivés afin de prendre en charge la génération de rendus et l’extraction des métadonnées pour une utilisation courante du système.

## Migration entre les déploiements [!DNL Experience Manager] {#migrating-between-aem-instances}

Bien que ce ne soit pas aussi courant, vous devez parfois migrer de grandes quantités de données d&#39;un déploiement [!DNL Experience Manager] vers un autre ; par exemple, lorsque vous effectuez une mise à niveau de [!DNL Experience Manager], mettez à niveau votre matériel ou migrez vers un nouveau centre de données, par exemple avec une migration AMS.

Dans ce cas, les ressources sont déjà renseignées avec les métadonnées et les rendus déjà générés. Il ne vous reste plus qu’à vous concentrer sur le déplacement des ressources d’une instance à une autre. Lors de la migration entre le déploiement [!DNL Experience Manager], vous effectuez les étapes suivantes :

1. Désactiver les workflows : Puisque vous migrez des rendus avec nos ressources, vous souhaitez désactiver les lanceurs de processus pour le flux de travaux [!UICONTROL DAM Update Asset].

1. Migrer les balises : Les balises étant déjà chargées dans le déploiement source [!DNL Experience Manager], vous pouvez les créer dans un package de contenu et installer le package sur l’instance de cible.

1. Migration des ressources : Deux outils sont recommandés pour transférer des ressources d&#39;un déploiement [!DNL Experience Manager] à un autre :

   * **Vault Remote** Copyor vlt rcp vous permet d&#39;utiliser vlt sur un réseau. Vous pouvez indiquer des répertoires source et de destination pour que vlt télécharge toutes les données du référentiel d’une instance et les charge dans l’autre. Vlt rcp est documenté à l’adresse [https://jackrabbit.apache.org/filevault/rcp.html](https://jackrabbit.apache.org/filevault/rcp.html)
   * **** Grabbitis est un outil de synchronisation de contenu open-source développé par Time Warner Cable pour leur  [!DNL Experience Manager] mise en oeuvre. Comme il utilise des flux de données continus, en comparaison avec vlt rcp, sa latence est inférieure et il annonce une vitesse de deux à dix fois plus rapide que vlt rcp. Grabbit prend également en charge la synchronisation du contenu delta uniquement, ce qui lui permet de synchroniser les modifications après l’achèvement d’une passe de migration initiale.

1. Activer les ressources : Suivez les instructions pour [activer les ressources](#activating-assets) documentées pour la migration initiale vers [!DNL Experience Manager].

1. Cloner la publication : Comme pour une nouvelle migration, le chargement d’une instance de publication unique et le clonage sont plus efficaces que l’activation du contenu sur les deux noeuds. Voir [Clonage de la publication](#cloning-publish).

1. Activer les workflows : Une fois la migration terminée, réactivez les lanceurs pour le processus [!UICONTROL DAM Update Asset] afin de prendre en charge la génération de rendus et l’extraction des métadonnées pour une utilisation courante du système.
