---
title: Concepts de configuration de base
description: Découvrez comment configurer Adobe Experience Manager en fonction de vos besoins.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
feature: Configuring
exl-id: 3777a1ba-cc4e-41b9-9098-236f8141925f
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 8f638eb384bdca59fb6f4f8990643e64f34622ce
workflow-type: tm+mt
source-wordcount: '2085'
ht-degree: 98%

---

# Concepts de configuration de base{#basic-configuration-concepts}

Adobe Experience Manager (AEM) est installé avec les paramètres par défaut, ce qui le rend prêt à l’emploi. Cependant, vous pouvez configurer AEM selon vos besoins.

De nombreux aspects d’AEM peuvent être configurés :

* Certains sont [couramment configurés pour chaque installation de projet](#primary-configuration-considerations) et doivent être examinés pour confirmer s’ils s’appliquent à votre projet.
* D’[autres configurations](#further-configuration-considerations) peuvent être courantes, mais pas impératives. Elles sont associées aux fonctionnalités ou aux performances et à la stabilité du système.
* D’autres encore sont uniquement nécessaires pour certaines fonctionnalités facultatives d’AEM (elles sont documentées avec la fonctionnalité appropriée).

Selon la configuration spécifique, ces modifications peuvent être effectuées à l’aide de l’un des éléments suivants :

* **Console Web Adobe CQ**

  Il s’agit d’un emplacement standard pour la configuration des lots et services OSGi.

  Consultez [Configuration d’OSGi](/help/sites-deploying/configuring-osgi.md) pour avoir plus de détails et connaître les pratiques recommandées.

* **Référentiel**

  Un sous-ensemble de configurations OSGi est disponible dans le référentiel. Cela garantit que la copie ou la réplication du contenu du référentiel recrée des configurations identiques. Vous pouvez également ajouter vos propres configurations au référentiel, en fonction du mode d’exécution.

  Consultez [Configuration d’OSGi dans le référentiel](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) et en particulier [Ajout d’une configuration au référentiel](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository) pour plus de détails.

* **Système de fichiers**

  Certains fichiers de configuration résident dans le système de fichiers.

* **Gestion de contenu Web AEM**

  Différents aspects peuvent être configurés directement dans la gestion de contenu Web AEM, à l’aide de la console [Outils](/help/sites-administering/tools-consoles.md) ; par exemple, les agents de réplication.

>[!NOTE]
>
>Lorsque vous utilisez Adobe Experience Manager, plusieurs méthodes permettent de gérer les paramètres de configuration pour les services OSGi (console ou nœuds de référentiel).
>
>Pour plus d’informations, voir [Configurer OSGi](/help/sites-deploying/configuring-osgi.md).

>[!NOTE]
>
>La configuration d’AEM est simple. Certaines modifications peuvent toutefois avoir un impact majeur sur les applications. Pour cette raison, assurez-vous de disposer de l’expérience et des connaissances nécessaires avant de commencer à configurer AEM et n’apportez que les modifications que vous savez requises. Toutes les modifications effectuées via la console OSGi sont **immédiatement** appliquées au système en cours d’exécution (aucun redémarrage n’est requis).

## Considérations relatives à la configuration principale {#primary-configuration-considerations}

Cette liste décrit les principales zones généralement configurées pour chaque nouveau projet. Toutes ces informations ne sont pas nécessaires, mais la liste doit être lue et révisée pour établir ce qui s’applique à votre projet.

La liste donne un bref aperçu de chaque aspect de la configuration, ainsi que des liens vers les pages qui fournissent des détails complets.

### Liste de contrôle de sécurité {#security-checklist}

Plusieurs problèmes de configuration clés sont répertoriés dans la [Liste de contrôle de sécurité](/help/sites-administering/security-checklist.md). Assurez-vous de la lire et de prendre toutes les mesures requises pour votre installation.

### Configuration de l’IU par défaut - optimisée pour les écrans tactiles ou classique {#configuring-the-default-ui-touch-optimized-or-classic}

Il existe deux interfaces utilisateur disponibles dans AEM :

* L’interface utilisateur optimisée pour les écrans tactiles
* L’interface utilisateur classique

Vous pouvez configurer l’interface utilisateur dont vous avez besoin à l’aide du [Mappage racine](/help/sites-deploying/osgi-configuration-settings.md).

>[!NOTE]
>
>Pour plus d’informations sur la sélection de l’interface utilisateur, consultez [Sélection de votre interface utilisateur](/help/sites-authoring/select-ui.md).

### IPv4 et IPv6 {#ipv-and-ipv}

Vous pouvez installer tous les éléments d’AEM (comme le référentiel et le Dispatcher) sur des réseaux IPv4 et IPv6.

Le fonctionnement est fluide, car aucune configuration spéciale n’est requise. Vous pouvez simplement spécifier une adresse IP au format approprié à votre type de réseau, le cas échéant.

Cela signifie que, lorsqu’une adresse IP doit être indiquée, vous avez le choix entre les éléments suivants (suivant les besoins) :

* une adresse IPv6 ;

  par exemple, `https://[ab12::34c5:6d7:8e90:1234]:4502`

* une adresse IPv4 ;

  par exemple, `https://123.1.1.4:4502`

* un nom de serveur ;

  par exemple, `https://www.yourserver.com:4502`

* Le scénario par défaut de `localhost` sera interprété à la fois pour les installations réseau IPv4 et IPv6.

  par exemple, `http://localhost:4502`

### Purge de version {#version-purging}

Dans une installation standard, AEM crée une version d’une page ou d’un nœud chaque fois que vous activez une page (après la mise à jour du contenu). Vous pouvez également créer des versions supplémentaires sur demande à l’aide de l’onglet **Contrôle de version** du sidekick. Toutes ces versions sont stockées dans le référentiel et peuvent être restaurées, si nécessaire.

Ces versions ne sont jamais purgées. La taille du référentiel augmente au fil du temps et doit donc être gérée.

Consultez [Purge de version](/help/sites-deploying/version-purging.md) pour des informations complètes, en particulier [Gestionnaire de versions](/help/sites-deploying/version-purging.md#version-manager) pour plus de détails sur la configuration d’AEM pour purger les anciennes versions si une version est créée.

### Journalisation {#logging}

AEM vous offre la possibilité de configurer :

* les paramètres globaux pour le service de journalisation centrale
* la journalisation des données de requête ; une configuration de journalisation spécialisée pour les informations de requête
* des paramètres spécifiques pour les services individuels ; par exemple, un fichier journal individuel et le format des messages du journal.

Consultez [Journalisation](/help/sites-deploying/configure-logging.md) pour des détails complets.

### Modes d’exécution {#run-modes}

Les modes d’exécution vous permettent d’ajuster votre instance AEM à des fins spécifiques. Par exemple, la création, la publication, les tests, le développement, l’intranet, etc.

Pour ce faire, définissez des ensembles de paramètres de configuration pour chaque mode d’exécution. Un ensemble de paramètres de configuration de base est appliqué à tous les modes d’exécution, puis vous pouvez ajuster les ensembles ajoutés en fonction de l’objectif de votre environnement spécifique. Ils sont appliqués selon les besoins.

Tous les paramètres de configuration sont stockés dans le référentiel et activés en définissant le **mode d’exécution**.

Pour plus d’informations, consultez [Modes d’exécution](/help/sites-deploying/configure-runmodes.md).

### Authentification unique {#single-sign-on}

L’authentification unique (SSO) permet à une personne d’accéder à plusieurs systèmes après avoir fourni une seule fois des informations d’identification d’authentification (telles qu’un nom d’utilisateur ou d’utilisatrice et un mot de passe). Un système distinct (appelé authentificateur approuvé) effectue l’authentification et fournit à Experience Manager les informations d’identification de l’utilisateur ou utilisatrice. Experience Manager vérifie les autorisations d’accès et les applique pour l’utilisateur ou l’utilisatrice (c’est-à-dire, détermine les ressources auxquelles l’utilisateur ou l’utilisatrice est autorisé à accéder).

Pour plus d’informations, consultez [Authentification unique](/help/sites-deploying/single-sign-on.md).

### Mappage de ressource {#resource-mapping}

Le mappage de ressources permet de définir des redirections, des URL de redirection et des hôtes virtuels pour AEM.

Par exemple, vous pouvez utiliser ces mappages pour :

* faire précéder toutes les demandes de `/content` afin que la structure interne soit masquée pour les visiteurs de votre site web ;
* définir une redirection afin que toutes les requêtes en direction de la page `/content/en/gateway` de votre site Web soient redirigées vers `https://gbiv.com/`.

Pour plus d’informations, consultez [Mappage de ressources](/help/sites-deploying/resource-mapping.md).

### Réplication, réplication inverse et agents de réplication {#replication-reverse-replication-and-replication-agents}

Les agents de réplication sont essentiels pour AEM en tant que mécanisme utilisé pour :

* [publier (activer)](/help/sites-authoring/publishing-pages.md) le contenu d’un environnement de création vers un de publication ;
* purger explicitement du contenu du cache de Dispatcher ;
* renvoyer les entrées utilisateur (par exemple, les entrées de formulaire) de l’environnement de publication vers celui de création (sous le contrôle de l’environnement de création).

Pour plus d’informations, consultez [Réplication](/help/sites-deploying/replication.md).

### Paramètres de configuration OSGi {#osgi-configuration-settings}

L’[OSGi](https://www.osgi.org/) est un élément fondamental de la pile technologique d’AEM. Il est utilisé pour contrôler les lots composites d’AEM et leur configuration.

Pour obtenir la liste des différents lots pertinents pour la mise en œuvre du projet (répertoriés en fonction du lot), consultez [Paramètres de configuration OSGi](/help/sites-deploying/osgi-configuration-settings.md). Les paramètres répertoriés ne doivent pas tous être ajustés, certains sont mentionnés pour vous aider à comprendre comment fonctionne AEM.

Lorsque vous utilisez AEM, plusieurs méthodes permettent de gérer les paramètres de configuration pour ces services. Consultez la section [Configuration d’OSGi](/help/sites-deploying/configuring-osgi.md) pour plus de détails et connaître les pratiques recommandées.

### Configuration de LDAP {#configuring-ldap}

L’authentification LDAP est requise pour authentifier les utilisateurs et utilisatrices stockés dans un annuaire LDAP (central) tel qu’Active Directory. Cela permet de réduire les efforts requis pour gérer les comptes utilisateurs.

L’authentification LDAP se produit au niveau du référentiel ; elle est donc traitée directement par le référentiel. Pour plus de détails, consultez [Configuration de LDAP avec AEM](/help/sites-administering/ldap-config.md).

Pour la gestion des utilisateurs et utilisatrices dans AEM (y compris l’attribution des droits d’accès), consultez [Administration et sécurité des utilisateurs et utilisatrices](/help/sites-administering/security.md).

### Configurer le Dispatcher {#configuring-the-dispatcher}

Dispatcher est un outil d’Adobe Experience Manager pour la mise en cache ou l’équilibrage de charge, ou les deux. Il peut être utilisé avec un serveur web de niveau entreprise.

Consultez [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=fr) pour plus de détails, notamment la [Configuration de Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=fr) pour plus informations sur la configuration.

### Configuration d’AEM LiveCycle Connector {#configuring-aem-livecycle-connector}

Grâce à AEM Doc Services et AEM Doc Security, AEM peut désormais appeler les services de document de LiveCycle pour effectuer le rendu d’un formulaire XFA, convertir un document au format PDF et protéger un document à l’aide d’une politique.

### Déchargement des tâches et administration de la topologie {#job-offloading-and-topology-administration}

Le [déchargement](/help/sites-deploying/offloading.md) permet de répartir les tâches de traitement entre les instances d’Experience Manager dans une topologie. Avec le déchargement, vous pouvez utiliser des instances particulières d’Experience Manager pour exécuter des types de traitement spécifiques. Un traitement spécialisé vous permet d’optimiser l’utilisation des ressources serveur disponibles.

Les topologies sont des clusters Experience Manager légèrement interconnectées qui participent au déchargement. Un cluster se compose d’une ou de plusieurs instances de serveur Experience Manager (une seule instance est considérée comme un cluster).

Pour plus d’informations sur l’affichage ou la modification de l’appartenance à une topologie, consultez la section [Administrer des topologies](/help/sites-deploying/offloading.md#administering-topologies).

### Configurer la console de bienvenue {#configuring-the-welcome-console}

La console de bienvenue de l’IU classique fournit une liste de liens vers les différentes consoles et fonctionnalités d’AEM.

Il est possible de configurer les liens visibles. Pour plus de détails, voir [Configurer la console de bienvenue](/help/sites-developing/customizing-the-welcome-console.md).

### Configurer pour optimiser la performance {#configuring-for-performance}

Les [performances](/help/sites-deploying/configuring-performance.md) sont la clé de votre projet. Certains aspects d’AEM (et/ou du référentiel sous-jacent) peuvent être configurés pour optimiser la performance.

Pour plus de détails, voir [Configurer les performances](/help/sites-deploying/configuring-performance.md#configuring-for-performance).

<!--delete ### Scaling {#scaling}

Scaling a CQ installation correctly depends greatly on the details of your particular use case. A detailed discussion of solution patterns for various situations can be found in [Scaling CQ](/help/sites-deploying/scaling.md).-->

### Magasin de données partagé {#shared-data-store}

Le magasin de données de référentiel est utilisé pour décharger le stockage des binaires de grande taille du référentiel vers une zone distincte, de sorte que les instances multiples du même binaire (une image, par exemple) de l’arborescence du référentiel soient stockées une seule fois.

Cette fonctionnalité « stocker une fois, référencer plusieurs fois » peut être étendue pour desservir non seulement une arborescence de référentiel unique, mais aussi des référentiels entièrement distincts, en configurant le magasin de données de chacun pour faire référence au même emplacement du système de fichiers partagé.

Un tel magasin de données peut être partagé entre différents nœuds dans le même cluster, entre différentes instances de publication et/ou d’auteur dans la même installation, ou même entre des instances entièrement distinctes dans différentes installations.

Pour plus d’informations, voir [Configurer des magasins de données et des magasins de nœuds](/help/sites-deploying/data-store-config.md).

## Autres considérations relatives à la configuration {#further-configuration-considerations}

### Activer HTTP sur SSL {#enabling-http-over-ssl}

Vous pouvez activer HTTP sur SSL pour utiliser des connexions plus sécurisées à vos serveurs.

Voir [Activer HTTP sur SSL](/help/sites-administering/ssl-by-default.md) pour plus de détails.

### Portails et portlets AEM {#aem-portals-and-portlets}

Un portail est une application web qui offre la personnalisation, l’authentification unique et l’intégration de contenu provenant de différentes sources et héberge la couche de présentation des systèmes d’information. Le composant portlet permet également d’incorporer un portlet dans la page. Pour accéder au contenu fourni par la Gestion de contenu web CQ5, le serveur du portail peut disposer de CQ5 Portal Director Portlet. Pour ce faire, installez, configurez et ajoutez le portlet à la page du portail.

Consultez [Portail et portlets](/help/sites-administering/aem-as-portal.md) pour plus de détails.

### Expiration des objets statiques {#expiration-of-static-objects}

Les objets statiques (par exemple, les icônes) ne changent pas. Par conséquent, le système doit être configuré de manière à ce qu’ils n’expirent pas (pendant une période raisonnable) et ainsi réduire le trafic inutile.

Voir [Expiration des objets statiques](/help/sites-deploying/expiration-static-objects.md) pour plus de détails.

### Ouvrir les fichiers dans le processus Java™ {#open-files-in-the-java-process}

Chaque processus Java™ peut accéder aux fichiers, ce qui nécessite des ressources système. Pour cette raison, une limite supérieure est définie quant au nombre de fichiers auxquels chaque processus est autorisé à accéder simultanément. En cas de dépassement, une erreur d’exception peut se produire.

Si le processus AEM dépasse ce seuil, le message « `too many open files` » est affiché dans `error.log`.

Pour éviter de telles exceptions, procédez comme suit :

1. Vérifiez le nombre de fichiers ouverts utilisés par votre processus AEM.

   Ce contrôle dépend de la plateforme sur laquelle votre instance est en cours d’exécution. Des utilitaires tels qu’lsof (UNIX®) ou Process Explorer (Windows) peuvent être utilisés.

    Cette valeur doit être contrôlée au cours du développement et du test de façon à :

   * confirmer que les fichiers sont fermés selon les besoins ;
   * pour déterminer la valeur maximale nécessaire (selon diverses circonstances)

1. Définissez le nombre maximal autorisé.

   La nouvelle valeur doit recouvrir les exigences en cours et tous les pics futurs, c’est pourquoi il est recommandé de doubler vos besoins actuels.

   Par défaut, `serverctl` configure `CQ_MAX_OPEN_FILES` sur `8192` ; cela devrait être suffisant pour la plupart des scénarios.

### Configuration de l’éditeur de texte enrichi {#configuring-the-rich-text-editor}

L’**éditeur de texte enrichi** (**RTE**) offre aux auteurs et auteures un large éventail de [fonctionnalités](/help/sites-authoring/rich-text-editor.md) pour modifier leur contenu textuel, en leur fournissant des icônes, des boîtes de sélection et des menus pour une expérience WYSIWYG.

Pour plus d’informations, consultez [Configuration de l’éditeur de texte enrichi](/help/sites-administering/rich-text-editor.md).

### Configurer la commande Annuler pour modifier des pages {#configuring-undo-for-page-editing}

Plusieurs propriétés contrôlent le comportement des commandes Annuler et Rétablir pour la modification des pages. Celles-ci peuvent être configurées. Pour plus d’informations, consultez [Configuration de l’annulation pour la modification de page](/help/sites-administering/config-undo.md).

### Configuration du composant vidéo {#configuring-the-video-component}

Le [composant vidéo](/help/sites-authoring/default-components-foundation.md#video) vous permet de placer un élément vidéo prédéfini et prêt à l’emploi sur une page.

Pour réaliser un bon transcodage, votre administrateur ou administratrice doit [installer FFmpeg](/help/sites-administering/config-video.md#install-ffmpeg) séparément. Il ou elle peut également [configurer vos profils vidéo](/help/sites-administering/config-video.md#configure-video-profiles) pour l’utilisation d’éléments HTML5.

### Configuration et personnalisation des rapports {#configuring-and-customizing-reports}

Pour vous aider à analyser et surveiller l’état de votre instance, CQ propose une sélection de rapports par défaut, qui peuvent être configurés en fonction de vos besoins :

Pour plus d’informations, consultez [Principes de base de la personnalisation des rapports](/help/sites-administering/reporting.md#the-basics-of-report-customization).

### Configurer les notifications par e-mail {#configuring-email-notification}

CQ envoie des notifications par e-mail aux utilisateurs et utilisatrices qui :

* Ont souscrit à des événements de page, par exemple une modification ou une réplication.
* Ont souscrit aux événements de forum.
* doivent effectuer une opération dans un workflow.

Pour plus d’informations, consultez [Configuration des notifications par e-mail](/help/sites-administering/notification.md).

### Activation des impressions de page {#enabling-page-impressions}

Les impressions de page s’affichent dans la colonne **Impressions** de la console siteadmin de l’IU classique. Pour activer la capture des impressions de page, configurez les éléments suivants :

* Sur l’instance de publication :

   * [Statistiques de page de gestionnaire de contenu Web Day CQ](/help/sites-deploying/osgi-configuration-settings.md)

* Sur l’instance de création :

   * [Adobe Page Impressions Tracker](/help/sites-deploying/osgi-configuration-settings.md)

>[!CAUTION]
>
>La configuration d’Adobe Page Impressions Tracker sur l’environnement de création permet d’envoyer des requêtes anonymes vers le service de suivi.
