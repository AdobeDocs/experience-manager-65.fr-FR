---
title: Concepts de configuration de base
description: Découvrez comment configurer Adobe Experience Manager.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
feature: Configuring
exl-id: 3777a1ba-cc4e-41b9-9098-236f8141925f
source-git-commit: ae08247c7be0824151637d744f17665c3bd82f2d
workflow-type: tm+mt
source-wordcount: '2112'
ht-degree: 26%

---

# Concepts de configuration de base{#basic-configuration-concepts}

Adobe Experience Manager (AEM) est installé avec les paramètres par défaut de tous les paramètres qui lui permettent d’exécuter &quot;prêt à l’emploi&quot;. Cependant, vous pouvez configurer AEM selon vos besoins.

Il existe de nombreux aspects de l’AEM qui peuvent être configurés :

* Certains sont [couramment configuré pour chaque installation de projet](#primary-configuration-considerations) et doivent être examinés pour confirmer s’ils s’appliquent à votre projet.
* [Autres configurations](#further-configuration-considerations) peut être courant, mais pas impératif; en rapport avec les fonctionnalités ou les performances et la stabilité du système.
* D’autres sont uniquement nécessaires pour certaines fonctionnalités facultatives d’AEM (elles sont documentées avec la fonctionnalité appropriée).

Selon la configuration spécifique, ces modifications peuvent être effectuées à l’aide de :

* **Console Web Adobe CQ**

  Il s’agit d’un emplacement standard pour la configuration des lots et services OSGi.

  Consultez [Configuration d’OSGi](/help/sites-deploying/configuring-osgi.md) pour avoir plus de détails et connaître les pratiques recommandées.

* **Référentiel**

  Un sous-ensemble de configurations OSGi est disponible dans le référentiel. Cela garantit que la copie ou la réplication du contenu du référentiel recrée des configurations identiques. Vous pouvez également ajouter vos propres configurations, selon le mode d’exécution, au référentiel.

  Consultez [Configuration d’OSGi dans le référentiel](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) et en particulier [Ajout d’une configuration au référentiel](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository) pour plus de détails.

* **Système de fichiers**

  Certains fichiers de configuration résident dans le système de fichiers.

* **Gestion de contenu Web AEM**

  Différents aspects peuvent être configurés directement dans la gestion de contenu Web AEM, à l’aide de la console [Outils](/help/sites-administering/tools-consoles.md) ; par exemple, les agents de réplication.

>[!NOTE]
>
>Lorsque vous utilisez Adobe Experience Manager, plusieurs méthodes permettent de gérer les paramètres de configuration pour les services OSGi (noeuds de console ou de référentiel).
>
>Voir [Configuration d’OSGi](/help/sites-deploying/configuring-osgi.md) pour plus d’informations.

>[!NOTE]
>
>La configuration des AEM est simple. Sachez toutefois que certaines modifications peuvent avoir un impact majeur sur les applications. Pour cette raison, assurez-vous de disposer de l’expérience et des connaissances nécessaires avant de commencer à configurer AEM et d’apporter uniquement les modifications dont vous savez qu’elles sont requises. Toutes les modifications effectuées via la console OSGi sont **immédiatement** appliquée au système en cours d’exécution (aucun redémarrage n’est requis).

## Considérations Principal sur la configuration {#primary-configuration-considerations}

Cette liste décrit les Principales zones généralement configurées pour chaque nouveau projet. Toutes ces informations ne sont pas nécessaires, mais la liste doit être lue et révisée pour voir ce qui s’applique à votre projet.

La liste donne un bref aperçu de chaque aspect de configuration, ainsi que des liens vers les pages qui fournissent des détails complets.

### Liste de contrôle de sécurité {#security-checklist}

Plusieurs problèmes de configuration clés sont répertoriés dans la section [Liste de contrôle de sécurité](/help/sites-administering/security-checklist.md). Assurez-vous de lire ce document et d’effectuer toute action nécessaire à votre installation.

### Configuration de l’IU par défaut - optimisée pour les écrans tactiles ou classique {#configuring-the-default-ui-touch-optimized-or-classic}

Deux interfaces utilisateur sont disponibles dans AEM :

* L’interface utilisateur optimisée pour les écrans tactiles
* L’interface utilisateur classique

Vous pouvez configurer l’interface utilisateur dont vous avez besoin à l’aide du [Mappage racine](/help/sites-deploying/osgi-configuration-settings.md).

>[!NOTE]
>
>Pour plus d’informations sur la sélection de l’interface utilisateur, consultez [Sélection de votre interface utilisateur](/help/sites-authoring/select-ui.md).

### IPv4 et IPv6 {#ipv-and-ipv}

Tous les éléments d’AEM (par exemple, le référentiel et Dispatcher) peuvent être installés sur les réseaux IPv4 et IPv6.

Le fonctionnement est fluide, car aucune configuration spéciale n’est requise. Vous pouvez simplement spécifier une adresse IP selon le format approprié à votre type de réseau, le cas échéant.

Cela signifie que lorsqu’une adresse IP doit être spécifiée, vous pouvez sélectionner (au besoin) parmi :

* une adresse IPv6 ;

  par exemple `https://[ab12::34c5:6d7:8e90:1234]:4502`

* une adresse IPv4 ;

  par exemple `https://123.1.1.4:4502`

* un nom de serveur ;

  par exemple, `https://www.yourserver.com:4502`

* Le scénario par défaut de `localhost` sera interprété à la fois pour les installations réseau IPv4 et IPv6.

  par exemple, `http://localhost:4502`

### Purge de version {#version-purging}

Dans une installation standard, AEM crée une version d’une page ou d’un noeud chaque fois que vous activez une page (après la mise à jour du contenu). Vous pouvez également créer des versions supplémentaires sur demande à l’aide de la variable **Contrôle de version** de l’onglet du sidekick. Toutes ces versions sont stockées dans le référentiel et peuvent être restaurées, si nécessaire.

Ces versions ne sont jamais purgées. La taille du référentiel augmente au fil du temps et doit donc être gérée.

Consultez [Purge de version](/help/sites-deploying/version-purging.md) pour des informations complètes, en particulier [Gestionnaire de versions](/help/sites-deploying/version-purging.md#version-manager) pour plus de détails sur la configuration d’AEM pour purger les anciennes versions si une version est créée.

### Journalisation {#logging}

AEM vous offre la possibilité de configurer :

* paramètres globaux pour le service de journalisation central
* la journalisation des données de demande ; une configuration de journalisation spécialisée pour les informations de requête ;
* les paramètres spécifiques des services individuels ; par exemple, un fichier journal individuel et le format des messages du journal.

Consultez [Journalisation](/help/sites-deploying/configure-logging.md) pour des détails complets.

### Modes d’exécution {#run-modes}

Les modes d’exécution vous permettent d’ajuster votre instance AEM à des fins spécifiques. Par exemple, créez ou publiez, testez, développez ou intranet, etc.

Pour ce faire, définissez des collections de paramètres de configuration pour chaque mode d’exécution. Un ensemble de paramètres de configuration de base est appliqué à tous les modes d’exécution, puis vous pouvez ajuster les ensembles ajoutés en fonction de l’objectif de votre environnement spécifique. Ils sont ensuite appliqués selon les besoins.

Tous les paramètres de configuration sont stockés dans le référentiel unique et activés en définissant la variable **Mode d’exécution**.

Voir [Modes d’exécution](/help/sites-deploying/configure-runmodes.md) pour plus d’informations.

### Connexion unique {#single-sign-on}

L’authentification unique (SSO) permet à un utilisateur d’accéder à plusieurs systèmes après avoir fourni une seule fois des informations d’identification d’authentification (telles qu’un nom d’utilisateur et un mot de passe). Un système distinct (appelé authentificateur approuvé) effectue l’authentification et fournit au Experience Manager les informations d’identification de l’utilisateur. Experience Manager vérifie et applique les autorisations d’accès pour l’utilisateur (c’est-à-dire, détermine les ressources auxquelles l’utilisateur est autorisé à accéder).

Voir [Authentification unique](/help/sites-deploying/single-sign-on.md) pour plus de détails.

### Mappage de ressource {#resource-mapping}

Le mappage de ressources permet de définir des redirections, des URL de redirection vers un microsite et des hôtes virtuels pour AEM.

Par exemple, vous pouvez utiliser ces mappages pour :

* faire précéder toutes les requêtes de `/content` afin que la structure interne soit masquée pour les visiteurs de votre site web ;
* définir une redirection afin que toutes les requêtes en direction de la page `/content/en/gateway` de votre site Web soient redirigées vers `https://gbiv.com/`.

Voir [Mappage des ressources](/help/sites-deploying/resource-mapping.md) pour plus de détails.

### Agents de réplication, de réplication inverse et de réplication {#replication-reverse-replication-and-replication-agents}

Les agents de réplication sont essentiels pour AEM en tant que mécanisme utilisé pour :

* [Publier (activer)](/help/sites-authoring/publishing-pages.md) contenu d’un auteur vers un environnement de publication.
* Purge explicite du contenu du cache de Dispatcher.
* Renvoyer les entrées utilisateur (par exemple, les entrées de formulaire) de l’environnement de publication vers l’environnement de création (sous le contrôle de l’environnement de création).

Pour plus d’informations, voir [Réplication](/help/sites-deploying/replication.md).

### Paramètres de configuration OSGi {#osgi-configuration-settings}

L’[OSGi](https://www.osgi.org/) est un élément fondamental de la pile technologique d’AEM. Il est utilisé pour contrôler les lots composites d’AEM et leur configuration.

Voir [Paramètres de configuration OSGi](/help/sites-deploying/osgi-configuration-settings.md) pour obtenir la liste des différents lots pertinents pour la mise en oeuvre du projet (répertoriés en fonction du lot). Les paramètres répertoriés ne doivent pas tous être ajustés, certains sont mentionnés pour vous aider à comprendre comment fonctionne AEM.

Lorsque vous utilisez AEM, plusieurs méthodes permettent de gérer les paramètres de configuration pour ces services. Consultez la section [Configuration d’OSGi](/help/sites-deploying/configuring-osgi.md) pour plus de détails et connaître les pratiques recommandées.

### Configuration de LDAP {#configuring-ldap}

L’authentification LDAP est requise pour authentifier les utilisateurs stockés dans un annuaire LDAP (central), tel que Principal Directory. Cela permet de réduire les efforts requis pour gérer les comptes d’utilisateurs.

L’authentification LDAP se produit au niveau du référentiel ; elle est donc traitée directement par le référentiel. Pour plus de détails, consultez [Configuration de LDAP avec AEM](/help/sites-administering/ldap-config.md).

Pour la gestion des utilisateurs dans AEM (y compris l’attribution des droits d’accès), voir [Administration et sécurité des utilisateurs](/help/sites-administering/security.md).

### Configurer le Dispatcher {#configuring-the-dispatcher}

Dispatcher est un outil de Adobe Experience Manager pour la mise en cache ou l’équilibrage de charge, ou les deux. Il peut être utilisé avec un serveur web de niveau élevé.

Consultez [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=fr) pour plus de détails, notamment la [Configuration de Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=fr) pour plus informations sur la configuration.

### Configuration d’AEM LiveCycle Connector {#configuring-aem-livecycle-connector}

Avec la mise à jour des services Doc AEM et AEM sécurité Doc, l’utilisateur peut désormais appeler les services Doc LiveCycle pour générer un formulaire XFA, convertir un document en PDF et protéger un document par une stratégie. Voir [Connecteur LiveCycle AEM](https://helpx.adobe.com/fr/livecycle/help/aem/aem-livecycle-connector.html) pour plus d’informations.

### Déchargement des tâches et administration de la topologie {#job-offloading-and-topology-administration}

[Le déchargement permet de répartir le traitement des tâches entre les instances d’Experience Manager dans une topologie. ](/help/sites-deploying/offloading.md) Avec le déchargement, vous pouvez utiliser des instances de Experience Manager spécifiques pour exécuter des types de traitement spécifiques. Un traitement spécialisé vous permet de maximiser l’utilisation des ressources de serveur disponibles.

Les topologies sont des clusters Experience Manager légèrement interconnectées qui participent au déchargement. Une grappe se compose d’une ou de plusieurs instances de serveur Experience Manager (une seule instance est considérée comme une grappe).

Pour plus d’informations sur l’affichage ou la modification de l’appartenance à une topologie, consultez la section [Administration des topologies](/help/sites-deploying/offloading.md#administering-topologies) .

### Configuration de la console de bienvenue {#configuring-the-welcome-console}

La console de bienvenue de l’IU classique fournit une liste de liens vers les différentes consoles et fonctionnalités d’AEM.

Il est possible de configurer les liens visibles, voir [Configuration de la console de bienvenue](/help/sites-developing/customizing-the-welcome-console.md) pour plus de détails.

### Configurer pour optimiser la performance {#configuring-for-performance}

[Performances](/help/sites-deploying/configuring-performance.md) est la clé de votre projet. Certains aspects d’AEM (et/ou du référentiel sous-jacent) peuvent être configurés pour optimiser la performance.

Voir [Configuration des performances](/help/sites-deploying/configuring-performance.md#configuring-for-performance) pour plus de détails.

<!--delete ### Scaling {#scaling}

Scaling a CQ installation correctly depends greatly on the details of your particular use case. A detailed discussion of solution patterns for various situations can be found in [Scaling CQ](/help/sites-deploying/scaling.md).-->

### Magasin de données partagé {#shared-data-store}

Le magasin de données de référentiel est utilisé pour décharger le stockage des binaires de grande taille du référentiel vers une zone distincte, de sorte que les instances multiples du même binaire (une image, par exemple) de l’arborescence du référentiel soient stockées une seule fois.

Cette fonctionnalité &quot;store-once, reference-many-times&quot; peut être étendue pour servir non seulement une arborescence de référentiel unique, mais des référentiels entièrement distincts, en configurant l’entrepôt de données de chacun pour faire référence au même emplacement du système de fichiers partagé.

Un tel entrepôt de données peut être partagé entre différents noeuds dans la même grappe, entre différentes instances de publication et/ou d’auteur dans la même installation, ou même entre des instances entièrement distinctes dans différentes installations.

Pour plus d’informations, voir [Configuration des entrepôts de données et des entrepôts de noeuds](/help/sites-deploying/data-store-config.md).

## Autres considérations relatives à la configuration {#further-configuration-considerations}

### Activation de HTTP via SSL {#enabling-http-over-ssl}

Vous pouvez activer HTTP via SSL pour utiliser des connexions plus sécurisées à vos serveurs.

Voir [Activation de HTTP via SSL](/help/sites-administering/ssl-by-default.md) pour plus de détails.

### Portails et portlets AEM {#aem-portals-and-portlets}

Un portail est une application web qui fournit la personnalisation, l’authentification unique, l’intégration de contenu provenant de différentes sources et héberge la couche de présentation des systèmes d’information. Le composant Portlet vous permet également d’incorporer un portlet dans la page. Pour accéder au contenu fourni par la gestion de contenu web CQ5, le serveur de portail peut être équipé du portlet Director du portail CQ5. Pour ce faire, installez, configurez et ajoutez le portlet à la page du portail.

Consultez [Portail et portlets](/help/sites-administering/aem-as-portal.md) pour plus de détails.

### Expiration des objets statiques {#expiration-of-static-objects}

Les objets statiques (par exemple, les icônes) ne changent pas. Par conséquent, le système doit être configuré de sorte qu’il n’expire pas (pendant une période raisonnable) et ainsi réduire le trafic inutile.

Voir [Expiration des objets statiques](/help/sites-deploying/expiration-static-objects.md) pour plus de détails.

### Ouvrir des fichiers dans le processus Java™ {#open-files-in-the-java-process}

Chaque processus Java™ peut accéder aux fichiers, ce qui nécessite des ressources système. Pour cette raison, une limite supérieure est définie quant au nombre de fichiers auxquels chaque processus est autorisé à accéder simultanément. En cas de dépassement, une erreur d’exception peut se produire.

Si le processus AEM dépasse ce maximum, alors le message &quot; `too many open files`&quot; apparaît dans `error.log`.

Pour éviter de telles exceptions, procédez comme suit :

1. Vérifiez le nombre de fichiers ouverts utilisés par votre processus AEM.

   Ce contrôle dépend de la plateforme sur laquelle votre instance est en cours d’exécution. Des utilitaires tels que lsof (UNIX®) ou Process Explorer (Windows) peuvent être utilisés.

    Cette valeur doit être contrôlée au cours du développement et du test de façon à :

   * confirmer que les fichiers sont fermés selon les besoins ;
   * pour déterminer la valeur maximale nécessaire (selon diverses circonstances)

1. Définissez le nombre maximal autorisé.

   La nouvelle valeur doit prendre en compte à la fois les besoins actuels et les pics futurs. Il est donc conseillé de doubler les besoins actuels.

   Par défaut, `serverctl` configure `CQ_MAX_OPEN_FILES` sur `8192` ; cela devrait être suffisant pour la plupart des scénarios.

### Configuration de l’éditeur de texte enrichi {#configuring-the-rich-text-editor}

Le **Éditeur de texte enrichi** (**RTE**) fournit aux auteurs un large éventail de [fonctionnalité](/help/sites-authoring/rich-text-editor.md) pour modifier leur contenu textuel ; leur fournissant des icônes, des boîtes de sélection et des menus pour une expérience WYSIWYG.

Voir [Configuration de l’éditeur de texte enrichi](/help/sites-administering/rich-text-editor.md) pour plus de détails.

### Configurer la commande Annuler pour modifier des pages {#configuring-undo-for-page-editing}

Plusieurs propriétés contrôlent le comportement des commandes Annuler et Rétablir pour la modification des pages. Ils peuvent être configurés, voir [Configuration de l’annulation pour la modification de page](/help/sites-administering/config-undo.md) pour plus de détails.

### Configuration du composant vidéo {#configuring-the-video-component}

Le [Composant vidéo](/help/sites-authoring/default-components-foundation.md#video) vous permet de placer un élément vidéo prédéfini prêt à l’emploi sur votre page.

Pour qu’un transcodage correct se produise, votre administrateur doit [Installation de FFmpeg](/help/sites-administering/config-video.md#install-ffmpeg) séparément. Ils peuvent également [Configuration des profils vidéo](/help/sites-administering/config-video.md#configure-video-profiles) à utiliser avec les éléments html5.

### Configuration et personnalisation des rapports {#configuring-and-customizing-reports}

Pour vous aider à surveiller et analyser l’état de votre instance, CQ fournit une sélection de rapports par défaut, qui peuvent être configurés en fonction de vos besoins :

Voir [Principes de base de la personnalisation des rapports](/help/sites-administering/reporting.md#the-basics-of-report-customization) pour plus de détails.

### Configurer les notifications par e-mail {#configuring-email-notification}

CQ envoie des notifications par courrier électronique aux utilisateurs qui :

* ont souscrit aux événements de pages, par exemple la modification ou la réplication ;
* Ont souscrit aux événements de forum.
* doivent effectuer une opération dans un workflow.

Voir [Configuration des notifications par e-mail](/help/sites-administering/notification.md) pour plus de détails.

### Activation des impressions de page {#enabling-page-impressions}

Les impressions de page s’affichent dans la variable **Impressions** de la console siteadmin de l’IU classique. Pour activer la capture des impressions de page, configurez les éléments suivants :

* Sur l’instance de publication :

   * [Statistiques de page de gestionnaire de contenu Web Day CQ](/help/sites-deploying/osgi-configuration-settings.md)

* Sur l’instance de création :

   * [Adobe Page Impressions Tracker](/help/sites-deploying/osgi-configuration-settings.md)

>[!CAUTION]
>
>La configuration du dispositif de suivi des impressions de page d’Adobe dans l’environnement de création permet d’envoyer des requêtes anonymes au service de suivi.
