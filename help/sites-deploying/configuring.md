---
title: Concepts de configuration de base
seo-title: Concepts de configuration de base
description: Apprenez à configurer AEM.
seo-description: Apprenez à configurer AEM.
uuid: edcdd4bd-5917-417e-8913-40d488383ea9
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 2673ea92-1651-4b1b-9aac-f4ba8b36782e
translation-type: tm+mt
source-git-commit: 8f35717324cd2c1524fb2cf931b3ce21be05729a
workflow-type: tm+mt
source-wordcount: '2132'
ht-degree: 88%

---


# Concepts de configuration de base{#basic-configuration-concepts}

Adobe Experience Manager (AEM) est installé avec les paramètres par défaut, ce qui le rend prêt à l’emploi. Vous pouvez toutefois configurer AEM en fonction de vos besoins spécifiques.

De nombreux aspects d’AEM peuvent être configurés :

* Certains sont [configurés généralement pour chaque installation de projet](#primary-configuration-considerations) et doivent être examinés afin de confirmer s’ils s’appliquent à votre projet.
* [D’autres configurations](#further-configuration-considerations) peuvent être courantes, bien que non impératives, et liées aux fonctionnalités, ou aux performances et à la stabilité du système.
* D’autres encore sont uniquement requises pour certaines fonctionnalités optionnelles d’AEM (elles sont documentées avec la fonctionnalité correspondante).

Selon la configuration spécifique, ces modifications peuvent être effectuées en utilisant au choix :

* **Console Web Adobe CQ**

   Il s’agit d’un emplacement standard pour la configuration des lots et services OSGi.

   Voir [Configuration d’OSGi](/help/sites-deploying/configuring-osgi.md) pour avoir plus de détails et connaître les pratiques recommandées.

* **Référentiel**

   Un sous-ensemble de configurations OSGi est disponible dans le référentiel. Cela assure que la copie ou la réplication du contenu du référentiel recrée des configurations identiques. Vous pouvez également ajouter vos propres configurations au référentiel, en fonction du mode d’exécution.

   Voir [Configuration d’OSGi dans le référentiel](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) et en particulier [Ajout d’une configuration au référentiel](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository) pour plus de détails.

* **Système de fichiers**

   Quelques fichiers de configuration se trouvent dans le système de fichiers.

* **Gestion de contenu Web AEM**

   Différents aspects peuvent être configurés directement dans AEM WCM (gestion de contenu web), à l’aide de la console [Outils](/help/sites-administering/tools-consoles.md) ; par exemple, les agents de réplication.

>[!NOTE]
>
>Lorsque vous utilisez Adobe Experience Manager, plusieurs méthodes permettent de gérer les paramètres de configuration pour les services OSGi (des nœuds de la console ou de référentiel).
>
>Voir [Configuration d’OSGi](/help/sites-deploying/configuring-osgi.md) pour des détails complets.

>[!NOTE]
>
>AEM est simple à configurer, mais vous devez savoir les choses suivantes :
>
>Certaines modifications peuvent avoir un impact majeur sur la ou les applications. C’est pourquoi vous devez vous assurer de disposer de l’expérience et des connaissances requises avant de commencer à configurer AEM, et apporter uniquement les changements dont vous savez la nécessité. Tout changement effectué via la console OSGi est **immédiatement** appliqué au système en exécution (aucun redémarrage n’est requis).

## Principales considérations en matière de configuration {#primary-configuration-considerations}

Cette liste présente les principaux aspects qui sont généralement configurés pour chaque nouveau projet. Ils ne sont pas tous nécessaires, mais la liste doit être lue et examinée afin de voir ce qui s’applique à votre projet.

La liste offre une présentation succincte de chaque aspect de configuration, ainsi que des liens vers les pages qui fournissent des détails complets.

### Liste de contrôle de sécurité {#security-checklist}

Plusieurs problèmes de configuration importants sont répertoriés dans la [Liste de contrôle de sécurité](/help/sites-administering/security-checklist.md). Assurez-vous de la lire et de prendre toute mesure requise pour votre installation.

### Configuration de l’interface utilisateur par défaut – optimisée pour les écrans tactiles ou classique {#configuring-the-default-ui-touch-optimized-or-classic}

Deux interfaces utilisateur sont disponibles dans AEM :

* l’interface utilisateur optimisée pour les écrans tactiles ;
* Interface utilisateur classique

Vous pouvez configurer l’interface utilisateur dont vous avez besoin à l’aide du [Mappage racine](/help/sites-deploying/osgi-configuration-settings.md).

>[!NOTE]
>
>Pour plus d’informations sur la sélection de l’interface utilisateur, voir [Sélection de votre interface utilisateur](/help/sites-authoring/select-ui.md).

### IPv4 et IPv6 {#ipv-and-ipv}

Tous les éléments d’AEM (par exemple, le référentiel, Dispatcher, etc.) peuvent être installés sur des réseaux IPv4 et IPv6.

Tout fonctionne sans problème et aucune configuration particulière n’est requise. Si nécessaire, vous pouvez simplement indiquer une adresse IP suivant le format approprié au type de réseau.

Cela signifie que lorsqu’une adresse IP doit être indiquée, vous avez le choix entre (suivant les besoins) :

* une adresse IPv6

   par exemple `https://[ab12::34c5:6d7:8e90:1234]:4502`

* une adresse IPv4

   par exemple `https://123.1.1.4:4502`

* un nom de serveur ;

   par exemple, `https://www.yourserver.com:4502`

* la casse par défaut de `localhost` sera interprétée pour les installations réseau IPv4 et IPv6.

   par exemple, `http://localhost:4502`

### Purge de version {#version-purging}

Dans une installation standard, AEM crée une version d’une page ou d’un nœud à chaque fois que vous activez une page (après avoir mis à jour le contenu). Vous pouvez également créé d’autres versions à la demande grâce à l’onglet **Contrôle de version** du sidekick. Toutes ces versions sont stockées dans le référentiel et peuvent être restaurées si nécessaire.

Ces versions n’étant jamais purgées, la taille du référentiel va continuer d’augmenter et devra être gérée.

Voir [Purge de version](/help/sites-deploying/version-purging.md) pour des détails complets, en particulier [Gestionnaire de versions](/help/sites-deploying/version-purging.md#version-manager) pour plus de détails sur la configuration d’AEM pour purger les anciennes versions si une version est créée.

### Journalisation {#logging}

AEM vous offre la possibilité de configurer :

* les paramètres généraux du service de journalisation central ;
* la journalisation des données de requête (une configuration de journalisation spécialisée pour les informations de requête) :
* les paramètres spécifiques des services individuels; par exemple, un fichier journal individuel et un format pour les messages du journal

Voir [Journalisation](/help/sites-deploying/configure-logging.md) pour des détails complets.

### Modes d’exécution {#run-modes}

Les modes d’exécution vous permettent d’accéder à votre instance AEM à une fin spécifique ; par exemple, la création ou la publication, le test, le développement ou l’intranet, etc.

Cela s’effectue en définissant des collections de paramètres de configuration pour chaque mode d’exécution. Un ensemble de paramètres de configuration de base est appliqué à tous les modes d’exécution, puis vous pouvez ajuster les ensembles ajoutés en fonction de l’objectif de votre environnement spécifique. Ils sont ensuite appliqués au besoin.

Tous les paramètres de configuration sont stockés dans un référentiel et activés en définissant le **Mode d’exécution**.

Voir [Modes d’exécution](/help/sites-deploying/configure-runmodes.md) pour des détails complets.

### Connexion unique  {#single-sign-on}

La connexion unique permet à l’utilisateur d’accéder à plusieurs systèmes après avoir fourni une seule fois ses informations d’identification (telles qu’un nom d’utilisateur et un mot de passe). Un système distinct (appelé l’authentificateur de confiance) effectue une authentification et fournit à Experience Manager les informations d’identification de l’utilisateur. Experience Manager vérifie les autorisations d’accès de l’utilisateur et les applique (c’est-à-dire qu’il détermine les ressources auxquelles l’utilisateur a accès).

Voir [Connexion unique](/help/sites-deploying/single-sign-on.md) pour des détails complets.

### Mappage de ressource  {#resource-mapping}

Le mappage de ressource permet de définir des redirections, des URL Vanity et des hôtes virtuels pour AEM.

Par exemple, vous pouvez utiliser ces mappages pour :

* Ajoutez un préfixe `/content` à toutes les requêtes afin que la structure interne soit masquée des visiteurs vers votre site Web.
* Définissez une redirection de sorte que toutes les requêtes envoyées à la page `/content/en/gateway` de votre site Web soient redirigées vers `https://gbiv.com/`.

Voir [Mappage de ressource](/help/sites-deploying/resource-mapping.md) pour plus de détails.

### Réplication, réplication inverse et agents de réplication  {#replication-reverse-replication-and-replication-agents}

Les agents de réplication sont essentiels à AEM comme mécanismes utilisés pour :

* [publier (activer)](/help/sites-authoring/publishing-pages.md) le contenu d’un environnement de création vers un environnement de publication ;
* vider explicitement le contenu de la mémoire cache de Dispatcher ;
* déplacer l’entrée de l’utilisateur (par exemple, entrée de formulaire) de l’environnement de publication à l’environnement de création (sous le contrôle de l’environnement de création).

Pour plus de détails, voir [Réplication](/help/sites-deploying/replication.md).

### Paramètres de configuration OSGi {#osgi-configuration-settings}

[](https://www.osgi.org/) OSGiest un élément fondamental de la pile technologique de l&#39;AEM. Il est utilisé pour contrôler les lots composites d’AEM et leur configuration.

Voir [Paramètres de configuration d’OSGi](/help/sites-deploying/osgi-configuration-settings.md) afin d’obtenir la liste des différents lots pertinents pour la mise en œuvre d’un projet (répertoriés par lot). Les paramètres répertoriés ne doivent pas tous être ajustés, certains sont mentionnés pour vous aider à comprendre comment fonctionne AEM.

Lorsque vous utilisez AEM, plusieurs méthodes permettent de gérer les paramètres de configuration pour ces services. Voir [Configuration d’OSGi](/help/sites-deploying/configuring-osgi.md) pour avoir plus de détails et connaître les pratiques recommandées.

### Configuration de LDAP  {#configuring-ldap}

L’authentification LDAP est requise pour authentifier les utilisateurs stockés dans un répertoire LDAP (central), tels qu’Active Directory. Cela permet de réduire l’effort nécessaire pour gérer les comptes utilisateur.

L’authentification LDAP se produit au niveau du référentiel ; elle est donc traitée directement par le référentiel. Pour plus d’informations, voir [Configuration de LDAP avec AEM](/help/sites-administering/ldap-config.md).

Pour la gestion des utilisateurs au sein d’AEM (y compris l’affectation des droits d’accès), voir [Administration des utilisateurs et sécurité](/help/sites-administering/security.md).

### Configuration de Dispatcher  {#configuring-the-dispatcher}

Le répartiteur est un outil de mise en cache et/ou d’équilibrage de charge Adobe Experience Manager qui peut être utilisé conjointement avec un serveur Web d’entreprise.

Voir [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html) pour plus de détails, notamment [Configuration de Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html) pour plus informations sur la configuration.

### Configuration d’AEM LiveCycle Connector {#configuring-aem-livecycle-connector}

Grâce à AEM Doc Services et AEM Doc Security, nous pouvons désormais appeler les services de document de LiveCycle pour effectuer le rendu d’un formulaire XFA, convertir un document au format PDF et protéger un document à l’aide d’une stratégie. Pour plus d&#39;informations, consultez [AEM LiveCycle Connector](https://helpx.adobe.com/livecycle/help/aem/aem-livecycle-connector.html).

### Déchargement des tâches et administration de la topologie {#job-offloading-and-topology-administration}

Le [déchargement](/help/sites-deploying/offloading.md) répartit les tâches de traitement entre les instances d’Experience Manager dans une topologie. Avec le déchargement, vous pouvez utiliser des instances spécifiques d’Experience Manager pour exécuter des types de traitements spécifiques. Le traitement spécialisé permet d’optimiser l’utilisation des ressources disponibles sur le serveur.

Les topologies sont des clusters Experience Manager légèrement interconnectées qui participent au déchargement. Un cluster est composé d’une ou de plusieurs instances de serveur Experience Manager (une instance unique est considérée comme un cluster).

Pour plus d’informations sur la procédure à suivre pour afficher ou modifier l’appartenance à une topologie, consultez la section [Administration des topologies](/help/sites-deploying/offloading.md#administering-topologies).

### Configuration de la console de bienvenue  {#configuring-the-welcome-console}

La console de bienvenue de l’interface utilisateur classique propose une liste de liens vers les différentes consoles et fonctionnalités au sein d’AEM.

Il est possible de configurer les liens qui sont visibles, voir [Configuration de la console de bienvenue](/help/sites-developing/customizing-the-welcome-console.md) pour plus de détails.

### Configuration des performances  {#configuring-for-performance}

La [performance](/help/sites-deploying/configuring-performance.md) est essentielle pour votre projet. Certains aspects d’AEM (et/ou du référentiel sous-jacent) peuvent être configurés pour optimiser la performance.

Voir [Configuration de la performance](/help/sites-deploying/configuring-performance.md#configuring-for-performance) pour plus de détails.

<!--delete ### Scaling {#scaling}

Scaling a CQ installation correctly depends greatly on the details of your particular use case. A detailed discussion of solution patterns for various situations can be found in [Scaling CQ](/help/sites-deploying/scaling.md).-->

### Entrepôt de données partagé {#shared-data-store}

Le magasin de données du référentiel est utilisé pour décharger l&#39;enregistrement de binaires volumineux du référentiel proprement dit dans une zone distincte, de sorte que plusieurs instances du même binaire (une image, par exemple) dans l&#39;arborescence du référentiel ne soient stockées qu&#39;une seule fois.

Cette fonction de stockage unique et référencement multiple peut être étendue pour servir non seulement une arborescence de référentiel, mais des référentiels entiers, en configurant l’entrepôt de données de chacun d’entre eux de façon à ce qu’il fasse référence au même emplacement de système de fichiers partagé.

Un tel entrepôt de données peut être partagé entre les différents nœuds du même cluster, entre différentes instances de publication et/ou de création de la même installation, voire même entre des instances complètement distinctes au sein de différentes installations.

Pour plus d’informations, voir [Configuration des entrepôts de données et des entrepôts de nœuds](/help/sites-deploying/data-store-config.md).

## Autres considérations concernant la configuration  {#further-configuration-considerations}

### Activation de HTTP via SSL {#enabling-http-over-ssl}

Vous pouvez activer HTTP via SSL afin d’utiliser des connexions plus sécurisées sur vos serveurs.

Voir [Activation de HTTP via SSL](/help/sites-administering/ssl-by-default.md) pour plus de détails.

### Portails et portlets AEM  {#aem-portals-and-portlets}

Un portail est une application Web qui fournit la personnalisation, la connexion unique et l’intégration du contenu provenant de sources différentes, et qui héberge la couche de présentation des systèmes d’information. Le composant portlet permet également d’incorporer un portlet sur la page. Pour accéder au contenu fourni par CQ5 WCM, le serveur du portail peut être équipé d’un portlet CQ5 Portal Director. Pour ce faire, vous devez installer, configurer et ajouter le portlet sur la page de portail.

Voir [Portail et portlets](/help/sites-administering/aem-as-portal.md) pour plus de détails.

### Expiration des objets statiques {#expiration-of-static-objects}

Les objets statiques (par exemple, les icônes) ne changent pas. Par conséquent, le système devrait être configuré de façon à ce qu’elles n’expirent pas (pendant une période raisonnable) de façon à réduire le trafic inutile.

Voir [Expiration des objets statiques](/help/sites-deploying/expiration-static-objects.md) pour plus de détails.

### Fichiers ouverts dans le processus Java  {#open-files-in-the-java-process}

Chaque processus Java peut accéder à des fichiers, ce qui nécessite des ressources système. Pour cette raison, une limite supérieure est définie en ce qui concerne le nombre de fichiers auxquels chaque processus est autorisé à accéder simultanément. Si elle est dépassée, une erreur d’exception peut se produire.

Si le processus AEM dépasse ce maximum, le message &quot; `too many open files`&quot; apparaît dans `error.log`.

Pour éviter ce type d’exception, vous devez procéder comme suit :

1. Vérifiez le nombre de fichiers ouverts par votre processus AEM.

   La marche à suivre pour effectuer cette vérification dépend de la plateforme sur laquelle votre instance s’exécute. Les utilitaires tels que lsof (Unix) ou l’Explorateur de processus (Windows) peuvent être utilisés.

    Cette valeur doit être contrôlée au cours du développement et du test de façon à :

   * confirmer que les fichiers sont fermés selon les besoins ;
   * déterminer la valeur maximale requise (selon différents cas).

1. Définissez le maximum autorisé.

   La nouvelle valeur doit recouvrir les exigences en cours et tous les pics futurs, c’est pourquoi il est recommandé de doubler vos besoins actuels.

   Par défaut, `serverctl` configure `CQ_MAX_OPEN_FILES` en `8192`; cela devrait suffire à la plupart des scénarios.

### Configuration de l’éditeur de texte enrichi {#configuring-the-rich-text-editor}

**L’éditeur de texte enrichi** (**RTE**) offre aux auteurs un large éventail de [fonctionnalités](/help/sites-authoring/rich-text-editor.md) pour modifier leur contenu textuel en leur fournissant des icônes, des boîtes de dialogue de sélection et des menus pour une expérience WYSIWYG intuitive.

Voir [Configuration de l’éditeur de texte enrichi](/help/sites-administering/rich-text-editor.md) pour plus de détails.

### Configuration de la commande Annuler pour la modification des pages  {#configuring-undo-for-page-editing}

Il existe plusieurs propriétés qui contrôlent le comportement des commandes Annuler et Rétablir pour modifier des pages. Celles-ci peuvent être configurées, voir [Configuration de la commande Annuler pour la modification des pages](/help/sites-administering/config-undo.md) pour plus de détails.

### Configuration du composant vidéo  {#configuring-the-video-component}

Le [composant vidéo](/help/sites-authoring/default-components-foundation.md#video) vous permet de placer sur votre page un élément vidéo prédéfini et prêt à l’emploi.

Pour qu’un transcodage correct ait lieu, l’administrateur doit [installer FFmpeg](/help/sites-administering/config-video.md#install-ffmpeg) séparément. Il peut également [configurer vos profils vidéo](/help/sites-administering/config-video.md#configure-video-profiles) pour permettre leur utilisation avec des éléments HTML5.

### Configuration et personnalisation des rapports  {#configuring-and-customizing-reports}

Pour vous aider à analyser et surveiller l’état de votre instance, CQ propose une sélection de rapports par défaut, qui peuvent être configurés pour vos différentes exigences :

Voir [Principes de base de la personnalisation des rapports](/help/sites-administering/reporting.md#the-basics-of-report-customization) pour plus de détails.

### Configuration des notifications par e-mail  {#configuring-email-notification}

CQ envoie des notifications par e-mail aux utilisateurs qui :

* Ont souscrit aux événements de pages, par exemple la modification ou la réplication.
* ont souscrit aux événements de forums ;
* doivent effectuer une opération dans un workflow.

Voir [Configuration des notifications par e-mail](/help/sites-administering/notification.md) pour plus de détails.

### Activation des impressions de page  {#enabling-page-impressions}

Les impressions de page sont affichées dans la colonne **Impressions** de la console siteadmin de l’interface utilisateur classique. Pour activer l’acquisition des impressions de page, vous devez configurer :

* Sur l’instance de publication :

   * [Day CQ WCM Page Statistics](/help/sites-deploying/osgi-configuration-settings.md)

* Sur l’instance de création :

   * [Adobe Page Impressions Tracke](/help/sites-deploying/osgi-configuration-settings.md)

>[!CAUTION]
>
>La configuration d’Adobe Page Impressions Tracker sur l’environnement de création permettra l’envoi de requêtes anonymes vers le service de suivi.

