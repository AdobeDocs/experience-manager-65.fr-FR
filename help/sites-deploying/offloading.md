---
title: Tâches de déchargement
description: Découvrez comment configurer et utiliser des instances d’AEM dans une topologie pour exécuter des types de traitement spécifiques.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
feature: Configuring
exl-id: 429c96ff-4185-4215-97e8-9bd2c130a9b1
solution: Experience Manager, Experience Manager Sites
source-git-commit: a28883778c5e8fb90cbbd0291ded17059ab2ba7e
workflow-type: tm+mt
source-wordcount: '2318'
ht-degree: 98%

---

# Tâches de déchargement{#offloading-jobs}

## Présentation {#introduction}

Le déchargement permet de répartir le traitement des tâches entre les instances d’Experience Manager dans une topologie. Avec le déchargement, vous pouvez utiliser des instances particulières d’Experience Manager pour exécuter des types de traitement spécifiques. Un traitement spécialisé vous permet d’optimiser l’utilisation des ressources serveur disponibles.

Le déchargement est basé sur les fonctionnalités [Apache Sling Discovery](https://sling.apache.org/documentation/bundles/discovery-api-and-impl.html) et Sling JobManager. Pour utiliser le déchargement, ajoutez des clusters Experience Manager à une topologie, puis identifiez les rubriques de tâche devant être traitées par le cluster. Les clusters sont composés d’une ou de plusieurs instances Experience Manager, de sorte qu’une seule instance est considérée comme un cluster.

Pour plus d’informations sur l’ajout d’instances à une topologie, voir [Administrer des topologies](/help/sites-deploying/offloading.md#administering-topologies).

### Distribution des traitements {#job-distribution}

Sling JobManager et JobConsumer permettent de créer des traitements qui sont traités dans une topologie :

* JobManager : un service qui crée des traitements pour des rubriques spécifiques.
* JobConsumer : un service qui exécute les traitements d’une ou de plusieurs rubriques. Plusieurs services JobConsumer peuvent être enregistrés pour la même rubrique.

Lorsque JobManager crée un traitement, le framework de déchargement sélectionne un cluster Experience Manager dans la topologie pour l’exécuter :

* Le cluster doit inclure une ou plusieurs instances qui exécutent un JobConsumer enregistré pour la rubrique de traitement.
* La rubrique doit être activée pour au moins une instance du cluster.

Pour en savoir plus sur l’amélioration de la distribution des traitements, voir [Configurer la consommation de rubriques](/help/sites-deploying/offloading.md#configuring-topic-consumption).

![chlimage_1-109](assets/chlimage_1-109.png)

Lorsque la structure de déchargement sélectionne un cluster pour effectuer une tâche et que ce cluster est composé de plusieurs instances, Sling Distribution détermine quelle instance du cluster exécute la tâche.

### Payloads de traitements {#job-payloads}

Le framework de déchargement prend en charge les payloads de traitements qui associent des traitements à des ressources dans le référentiel. Les payloads de traitements sont utiles lorsque des traitements sont créés pour des ressources de travail et que la tâche est déchargée sur un autre ordinateur.

Lors de la création d’un traitement, la position de la payload n’est garantie que sur l’instance qui crée le traitement. Lors du déchargement du traitement, les agents de réplication s’assurent que la payload est créée sur l’instance qui finit par consommer le traitement. Lorsque l’exécution du traitement est terminée, la réplication inverse entraîne la copie de la payload vers l’instance qui a créé le traitement.

## Administrer les topologies {#administering-topologies}

Les topologies sont des grappes de Experience Manager à couplage faible qui participent au déchargement. Un cluster se compose d’une ou de plusieurs instances de serveur Experience Manager (une seule instance est considérée comme un cluster).

Chaque instance d’Experience Manager exécute les services suivants liés au déchargement :

* Discovery Service : envoie des demandes à un connecteur de topologie afin de faire adhérer la topologie.
* Topology Connector : reçoit les demandes d’adhésion et accepte ou refuse chaque demande.

Le Discovery Service de tous les membres de la topologie pointe vers le Topology Connector sur l’un des membres. Dans les sections qui suivent, ce membre est appelé membre racine.

![chlimage_1-110](assets/chlimage_1-110.png)

Chaque cluster de la topologie contient une instance reconnue comme leader. Le leader du cluster interagit avec la topologie au nom des autres membres du cluster. Lorsque le leader quitte le cluster, un nouveau leader est automatiquement sélectionné.

### Afficher la topologie {#viewing-the-topology}

Utilisez le navigateur de topologies pour explorer l’état de la topologie à laquelle participe l’instance Experience Manager. Le navigateur de topologies affiche les clusters et les instances de la topologie.

Pour chaque cluster, vous voyez une liste des membres du cluster qui indique l’ordre dans lequel chaque membre a rejoint le cluster et quel membre est le leader. La propriété actuelle indique l’instance que vous êtes en train de gérer.

Pour chaque instance de cluster, vous pouvez voir plusieurs propriétés liées à la topologie :

* Une liste autorisée de rubriques pour le client des travaux de l’instance.
* Points d’entrée exposés pour la connexion à la topologie.
* Rubriques de traitement pour lesquelles l’instance est enregistrée pour le déchargement.
* Rubriques de traitement que l’instance traite.

1. À l’aide de l’interface utilisateur tactile, appuyez sur l’onglet Outils. ([http://localhost:4502/tools.html](http://localhost:4502/tools.html))
1. Dans la zone Opérations Granite, cliquez sur Navigateur de déchargement.
1. Dans le panneau de navigation, cliquez sur Navigateur de topologies.

   Les clusters qui participent à la topologie s’affichent.

   ![chlimage_1-111](assets/chlimage_1-111.png)

1. Cliquez sur un cluster pour afficher la liste des instances du cluster, ainsi que leur ID, Statut actuel et Statut de leader.
1. Cliquez sur un ID d’instance pour afficher des propriétés plus détaillées.

Vous pouvez également utiliser la console web pour afficher les informations sur la topologie. La console fournit des informations supplémentaires sur les clusters de la topologie :

* L’instance qui correspond à l’instance locale.
* Les services Topology Connector que cette instance utilise pour se connecter à la topologie (sortants) et les services qui se connectent à cette instance (entrants).
* L’historique des modifications des propriétés de la topologie et de l’instance.

Utilisez la procédure suivante pour ouvrir la page de gestion des topologies de la console web :

1. Ouvrez la console web dans votre navigateur. ([http://localhost:4502/system/console](http://localhost:4502/system/console))
1. Cliquez sur Principal > Gestion de la topologie.

   ![chlimage_1-112](assets/chlimage_1-112.png)

### Configuration de l’appartenance à une topologie {#configuring-topology-membership}

Le service de découverte basé sur les ressources Apache Sling s’exécute sur chaque instance pour contrôler la manière dont les instances Experience Manager interagissent avec une topologie.

Le service de découverte envoie des requêtes POST périodiques (pulsations) aux services Topology Connector pour établir et maintenir des connexions avec la topologie. Le service Topology Connector maintient une liste d’adresses IP ou de noms d’hôte autorisés à rejoindre la topologie :

* Pour joindre une instance à une topologie, précisez l’URL du service Topology Connector du membre racine.
* Pour permettre à une instance de rejoindre une topologie, ajoutez l’instance à la liste autorisée du service Topology Connector du membre racine.

Utilisez la console web ou un nœud sling:OsgiConfig pour configurer les propriétés suivantes du service org.apache.sling.discovery.impt.Config :

<table>
 <tbody>
  <tr>
   <th>Nom de la propriété</th>
   <th>Nom OSGi</th>
   <th>Description</th>
   <th>Valeur par défaut</th>
  </tr>
  <tr>
   <td>Délai d’expiration de la pulsation (secondes)</td>
   <td>heartbeatTimeout</td>
   <td>Durée, en secondes, d’attente d’une réponse de pulsation avant que l’instance ciblée ne soit considérée comme non disponible. </td>
   <td>20</td>
  </tr>
  <tr>
   <td>Fréquence des pulsations (en secondes)</td>
   <td>heartbeatInterval</td>
   <td>La durée en secondes entre les pulsations.</td>
   <td>15</td>
  </tr>
  <tr>
   <td>Délai d’événement minimal (secondes)</td>
   <td>minEventDelay</td>
   <td><p>Lorsqu’une modification est apportée à la topologie, délai nécessaire pour retarder le changement de statut de TOPOLOGY_CHANGING à TOPOLOGY_CHANGED. Chaque changement qui se produit lorsque l’état est TOPOLOGY_CHANGING augmente le délai de cette durée.</p> <p>Ce délai évite aux listeners d’être inondés d’événements. </p> <p>Si vous ne souhaitez pas utiliser de délai, spécifiez 0 ou un nombre négatif.</p> </td>
   <td>3</td>
  </tr>
  <tr>
   <td>URL de Topology Connector</td>
   <td>topologyConnectorUrls</td>
   <td>URL des services Topology Connector pour envoyer des messages de pulsation.</td>
   <td>http://localhost:4502/libs/sling/topology/connector</td>
  </tr>
  <tr>
   <td>Liste autorisée de Topology Connector</td>
   <td>topologyConnectorWhitelist</td>
   <td>Liste des adresses IP ou noms d’hôte autorisés par le service Topology Connector local dans la topologie. </td>
   <td><p>localhost</p> <p>127.0.0.1</p> </td>
  </tr>
  <tr>
   <td>Nom du descripteur de référentiel</td>
   <td>leaderElectionRepositoryDescriptor</td>
   <td> </td>
   <td>&lt;no value&gt;</td>
  </tr>
 </tbody>
</table>

Utilisez la procédure suivante pour connecter une instance CQ au membre racine d’une topologie. La procédure pointe l’instance vers l’URL du Topology Connector du membre de topologie racine. Effectuez cette procédure sur tous les membres de la topologie.

1. Ouvrez la console web dans votre navigateur. ([http://localhost:4502/system/console](http://localhost:4502/system/console))
1. Cliquez sur Principal > Gestion de la topologie.
1. Cliquez sur Configurer le service de détection.
1. Ajoutez un élément à la propriété URL de Topology Connector et spécifiez l’URL du service Topology Connector du membre de topologie racine. L’URL se présente sous la forme https://rootservername:4502/libs/sling/topology/connector.

Effectuez la procédure suivante sur le membre racine de la topologie. La procédure ajoute les noms des autres membres de la topologie à sa liste d’autorisation du service de détection.

1. Ouvrez la console web dans votre navigateur. ([http://localhost:4502/system/console](http://localhost:4502/system/console))
1. Cliquez sur Principal > Gestion de la topologie.
1. Cliquez sur Configurer le service de détection.
1. Pour chaque membre de la topologie, ajoutez un élément à la propriété de liste autorisée de Topology Connector, puis indiquez le nom d’hôte ou l’adresse IP du membre de la topologie.

## Configuration de la consommation des rubriques {#configuring-topic-consumption}

Utilisez le navigateur de déchargement pour configurer la consommation de rubriques pour les instances Experience Manager dans la topologie. Pour chaque instance, vous pouvez spécifier les rubriques qu&#39;elle consomme. Par exemple, pour configurer votre topologie afin qu’une seule instance consomme des rubriques d’un type spécifique, désactivez la rubrique sur toutes les instances sauf une.

Les tâches sont réparties entre les instances ayant la rubrique associée activée à l’aide d’une logique circulaire.

1. À l’aide de l’interface utilisateur tactile, appuyez sur l’onglet Outils. ([http://localhost:4502/tools.html](http://localhost:4502/tools.html))
1. Dans la zone Opérations Granite, cliquez sur Navigateur de déchargement.
1. Dans le panneau de navigation, cliquez sur Navigateur de déchargement.

   Les rubriques de déchargement et les instances de serveur pouvant consommer les rubriques apparaissent.

   ![chlimage_1-113](assets/chlimage_1-113.png)

1. Pour désactiver la consommation d’une rubrique pour une instance, au-dessous du nom de la rubrique, cliquez sur Désactiver en regard de l’instance.
1. Pour configurer toutes les consommations de rubrique pour une instance, cliquez sur l’identificateur de l’instance au-dessous d’une rubrique.

   ![chlimage_1-114](assets/chlimage_1-114.png)

1. Cliquez sur l’un des boutons suivants en regard d&#39;une rubrique pour configurer le comportement de consommation de l’instance, puis cliquez sur Enregistrer :

   * Activé : cette instance consomme uniquement les traitements de cette rubrique.
   * Désactivé : cette instance ne consomme pas les tâches de cette rubrique.
   * Exclusif : cette instance consomme uniquement les tâches de cette rubrique.

   **Note :** lorsque vous sélectionnez Exclusif pour une rubrique, toutes les autres rubriques sont automatiquement définies sur Désactivé.

### Consommateurs et consommatrices de traitement installés {#installed-job-consumers}

Plusieurs implémentations de JobConsumer sont installées avec Experience Manager. Les rubriques pour lesquelles ces JobConsumers sont enregistrés apparaissent dans le navigateur de déchargement. Les rubriques supplémentaires qui apparaissent sont ceux que les JobConsumers personnalisés ont enregistrées. Le tableau suivant décrit les JobConsumers par défaut.

| Rubrique de tâche | PID de service | Description |
|---|---|---|
| / | org.apache.sling.event.impl.jobs.deprecated.EventAdminBridge | Installé avec Apache Sling. Tâches de traitement générées par l’administrateur d’événements OSGi, à des fins de rétrocompatibilité. |
| com/day/cq/replication/job/&amp;ast; | com.day.cq.replication.impl.AgentManagerImpl | Un agent de réplication qui réplique les payloads de la tâche. |

<!--
| com/adobe/granite/workflow/offloading |com.adobe.granite.workflow.core.offloading.WorkflowOffloadingJobConsumer |Processes jobs that the DAM Update Asset Offloader workflow generates. |
-->

### Désactivation et activation des rubriques pour une instance {#disabling-and-enabling-topics-for-an-instance}

Le service Apache Sling Job Consumer Manager fournit des propriétés de liste autorisée et de liste bloquée de rubriques. Configurez ces propriétés pour activer ou désactiver le traitement de rubriques spécifiques sur une instance Experience Manager.

**Remarque :** Si l’instance appartient à une topologie, vous pouvez également utiliser le navigateur de déchargement sur tout ordinateur de la topologie pour activer ou désactiver les rubriques.

La logique qui crée la liste des rubriques activées autorise d’abord toutes les rubriques qui se trouvent dans la liste autorisée, puis supprime les rubriques qui se trouvent dans la liste bloquée. Par défaut, toutes les rubriques sont activées (la valeur de la liste autorisée est `*`) et aucune rubrique n’est désactivée (la liste bloquée n’a aucune valeur).

Utilisez le console web ou un nœud `sling:OsgiConfig` pour configurer les propriétés suivantes. Pour les nœuds `sling:OsgiConfig`, le paramètre PID du service Gestionnaire de consommation de tâche est org.apache.sling.event.impl.jobs.JobConsumerManager.

| Nom de propriété dans la console web | ID OSGi | Description |
|---|---|---|
| Liste de rubriques autorisées | job.consumermanager.whitelist | Liste de rubriques traitées par le service JobManager local. La valeur par défaut &amp;ast; envoie toutes les rubriques au service TopicConsumer enregistré. |
| Liste bloquée de rubriques | job.consumermanager.blacklist | Liste de rubriques que le service JobManager local ne traite pas. |

## Création d’agents de réplication pour le déchargement {#creating-replication-agents-for-offloading}

Le framework de déchargement utilise la réplication pour transporter les ressources entre l’auteur ou l’autrice et le secondaire. Le framework de déchargement crée automatiquement des agents de réplication lorsque les instances rejoignent la topologie. Les agents sont créés avec des valeurs par défaut. Modifiez manuellement le mot de passe que les agents utilisent pour l’authentification.

>[!CAUTION]
>
>Un problème connu avec les agents de réplication générés automatiquement nécessite la création manuelle de nouveaux agents de réplication.

Créez les agents de réplication qui transportent les charges utiles de traitement entre les instances pour le déchargement. L’illustration suivante montre les agents qui doivent être déchargés de l’instance de création vers une instance secondaire. L’auteur a un identifiant Sling de 1, alors que l’identifiant Sling de l’instance de travail est 2 :

![chlimage_1-115](assets/chlimage_1-115.png)

Cette configuration nécessite les trois agents suivants :

1. Un agent sortant sur l’instance de création qui se réplique sur l’instance secondaire.
1. Un agent inverse sur l’instance de création qui extrait de la boîte d’envoi sur l’instance secondaire.
1. Un agent de boîte d’envoi sur l’instance secondaire.

Ce schéma de réplication est similaire à celui utilisé entre les instances de création et de publication. Cependant, pour la situation de déchargement, toutes les instances impliquées sont des instances de création.

>[!NOTE]
>
>Le framework de déchargement utilise la topologie pour obtenir les adresses IP des instances de déchargement. Le framework crée ensuite automatiquement les agents de réplication en fonction de ces adresses IP. Si les adresses IP des instances de déchargement changent ultérieurement, la modification se propage automatiquement sur la topologie après le redémarrage de l’instance. Toutefois, la structure de déchargement ne met pas automatiquement à jour les agents de réplication pour refléter les nouvelles adresses IP. Pour éviter cette situation, utilisez des adresses IP fixes pour toutes les instances de la topologie.

### Nommage des agents de réplication pour le déchargement {#naming-the-replication-agents-for-offloading}

Utilisez un format spécifique pour la propriété ***Nom*** des agents de réplication, afin que la structure de déchargement puisse utiliser automatiquement l’agent correct pour les instances de travail spécifiques.

**Nommer un agent sortant sur l’instance d’auteur :** 

`offloading_<slingid>`, où `<slingid>` est l’identifiant Sling de l’instance de travail.

Exemple : `offloading_f5c8494a-4220-49b8-b079-360a72f71559`

**Nommer l’agent inverse sur l’instance d’auteur :** 

`offloading_reverse_<slingid>`, où `<slingid>` est l’identifiant Sling de l’instance de travail.

Exemple : `offloading_reverse_f5c8494a-4220-49b8-b079-360a72f71559`

**Nommer le dossier d’envoi sur l’instance de travail :**

`offloading_outbox`

### Création de l’agent sortant {#creating-the-outgoing-agent}

1. Créez un **agent de réplication** sur l’auteur. (Voir la [documentation sur les agents de réplication](/help/sites-deploying/replication.md)). Indiquez un **titre**. Le **nom** doit suivre la convention de dénomination.
1. Créez un agent en utilisant les propriétés suivantes :

   | Propriété | Valeur |
   |---|---|
   | Paramètres > Type de sérialisation | Valeur par défaut |
   | Transfert >URI de transfert | https://*`<ip of target instance>`*:*`<port>`*`/bin/receive?sling:authRequestLogin=1` |
   | Transfert > Utilisateur de transfert | Utilisateur de réplication sur l’instance cible |
   | Transfert > Mot de passe de transfert | Mot de passe de l’utilisateur de réplication sur l’instance cible |
   | Extension > Méthode HTTP | POST |
   | Déclencheurs > Ignorer la valeur par défaut | True |

### Création de l’agent inverse {#creating-the-reverse-agent}

1. Créez un **agent de réplication inverse** sur l’auteur. (Voir la [documentation sur les agents de réplication](/help/sites-deploying/replication.md).) Indiquez un **titre**. Le **nom** doit suivre la convention de dénomination.
1. Créez un agent en utilisant les propriétés suivantes :

   | Propriété | Valeur |
   |---|---|
   | Paramètres > Type de sérialisation | Valeur par défaut |
   | Transfert >URI de transfert | https://*`<ip of target instance>`*:*`<port>`*`/bin/receive?sling:authRequestLogin=1` |
   | Transfert > Utilisateur de transfert | Utilisateur de réplication sur l’instance cible |
   | Transfert > Mot de passe de transfert | Mot de passe de l’utilisateur de réplication sur l’instance cible |
   | Extension > Méthode HTTP | GET |

### Création de l’agent de dossier d’envoi {#creating-the-outbox-agent}

1. Créez un **agent de réplication** sur l’instance de travail. (Voir la [documentation sur les agents de réplication](/help/sites-deploying/replication.md).) Indiquez un **titre**. Le **nom** doit être `offloading_outbox`.
1. Créez l’agent en utilisant les propriétés suivantes.

   | Propriété | Valeur |
   |---|---|
   | Paramètres > Type de sérialisation | Valeur par défaut |
   | Transfert >URI de transfert | repo://var/replication/outbox |
   | Déclencheur > Ignorer la valeur par défaut | True |

### Trouver l’identifiant Sling {#finding-the-sling-id}

Obtenez l’identifiant Sling d’une instance Experience Manager à l’aide de l’une des méthodes suivantes :

* Ouvrez la console web et, dans les paramètres Sling, recherchez la valeur de la propriété d’identifiant Sling ([http://localhost:4502/system/console/status-slingsettings](http://localhost:4502/system/console/status-slingsettings)). Cette méthode est utile si l’instance ne fait pas encore partie de la topologie.
* Utilisez le navigateur de topologies si l’instance fait déjà partie de la topologie.

<!--
## Offloading the Processing of DAM Assets {#offloading-the-processing-of-dam-assets}

Configure the instances of a topology so that specific instances perform the background processing of assets that are added or updated in DAM.

By default, Experience Manager executes the [!UICONTROL DAM Update Asset] workflow when a DAM asset changes or one is added to DAM. Change the default behavior so that Experience Manager instead executes the [!UICONTROL DAM Update Asset Offloader] workflow. This workflow generates a JobManager job that has a topic of `com/adobe/granite/workflow/offloading`. Then, configure the topology so that the job is offloaded to a dedicated worker.

>[!CAUTION]
>
>No workflow should be transient when used with workflow offloading. For example, the [!UICONTROL DAM Update Asset] workflow must not be transient when used for asset offloading. To set/unset the transient flag on a workflow, see [Transient Workflows](/help/assets/performance-tuning-guidelines.md#workflows).

The following procedure assumes the following characteristics for the offloading topology:

* One or more Experience Manager instance are authoring instances that users interact with for adding or updating DAM assets.
* Users to do not directly interact with one or more Experience Manager instances that process the DAM assets. These instances are dedicated to the background processing of DAM assets.

1. On each Experience Manager instance, configure the Discovery Service so that it points to the root Topography Connector. (See [Configuring Topology Membership](#title4).)
1. Configure the root Topography Connector so that the connecting instances are on the allow list.
1. Open Offloading Browser and disable the `com/adobe/granite/workflow/offloading` topic on the instances with which users interact to upload or change DAM assets.

   ![chlimage_1-116](assets/chlimage_1-116.png)

1. On each instance that users interact with to upload or change DAM assets, configure workflow launchers to use the [!UICONTROL DAM Update Asset Offloading] workflow:

    1. Open the Workflow console.
    1. Click the Launcher tab.
    1. Locate the two Launcher configurations that execute the [!UICONTROL DAM Update Asset] workflow. One launcher configuration event type is Node Created, and the other type is Node Modified.
    1. Change both event types so that they execute the [!UICONTROL DAM Update Asset Offloading] workflow. (For information about launcher configurations, see [Starting Workflows When Nodes Change](/help/sites-administering/workflows-starting.md).)

1. On the instances that perform the background processing of DAM assets, disable the workflow launchers that execute the [!UICONTROL DAM Update Asset] workflow.
-->

## Informations complémentaires {#further-reading}

En plus des informations présentées sur cette page, vous pouvez également lire ce qui suit :

* Pour plus d’informations sur l’utilisation des API Java pour créer des tâches et des consommateurs de tâche, consultez la section [Création et consommation des tâches pour le déchargement](/help/sites-developing/dev-offloading.md).
