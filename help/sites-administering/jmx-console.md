---
title: Contrôle des ressources de serveur à l’aide de la console JMX
seo-title: Monitoring Server Resources Using the JMX Console
description: Découvrez comment surveiller les ressources du serveur par le biais de la console JMX.
seo-description: Learn how to monitor server resources using the JMX console.
uuid: 0a28aafe-61b2-472b-8f8f-2cd6540cbfee
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 873ce073-0055-4e1b-b3c6-ae7967700894
docset: aem65
exl-id: eabd8335-6140-4c15-8cff-21608719aa5f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '4957'
ht-degree: 100%

---

# Contrôle des ressources de serveur à l’aide de la console JMX{#monitoring-server-resources-using-the-jmx-console}

La console JMX permet de surveiller et de gérer des services sur le serveur CRX. Les sections suivantes récapitulent les attributs et les opérations exposés par le biais de la structure JMX.

Pour plus d’informations sur l’utilisation des commandes de la console, consultez la section [Utilisation de la console JMX](#using-the-jmx-console). Pour obtenir des informations d’ordre général sur JMX, consultez la page [Technologie Java Management Extensions (JMX)](https://www.oracle.com/technetwork/java/javase/tech/javamanagement-140525.html) (en anglais) sur le site web d’Oracle.

Pour plus d’informations sur la création de beans gérés (MBeans) pour gérer ces services à l’aide de la console JMX, voir [Intégration des services à la console JMX](/help/sites-developing/jmx-integration.md) (en anglais).

## Maintenance des workflow {#workflow-maintenance}

Opérations d’administration des instances de workflow en cours d’exécution, terminées, obsolètes et ayant échoué.

* Domaine : com.adobe.granite.workflow
* Type : maintenance

>[!NOTE]
>
>Pour plus d’informations sur les outils d’administration des workflows et une description des statuts possibles des instances de workflows, voir [Console Workflow](/help/sites-administering/workflows-administering.md).

### Opérations {#operations}

**listRunningWorkflowsPerModel** Indique le nombre d’instances de workflows exécutées pour chaque modèle de workflow.

* Arguments : aucun
* Valeur renvoyée : données présentées sous forme de tableau, qui contient les colonnes Nombre et ID de modèle.

**listCompletedWorkflowsPerModel** Indique le nombre d’instances de workflows terminées pour chaque modèle de workflow.

* Arguments : aucun
* Valeur renvoyée : données présentées sous forme de tableau, qui contient les colonnes Nombre et ID de modèle.

**returnWorkflowQueueInfo** Répertorie les informations sur les éléments de workflows traités et mis en file d’attente pour le traitement.

* Arguments : aucun
* Valeur renvoyée : données présentées sous forme de tableau, qui contient les colonnes suivantes :

   * Tâches
   * Nom de la file d’attente
   * Tâches actives
   * Temps de traitement moyen
   * Temps d’attente moyen
   * Tâches annulées
   * Tâches en échec
   * Tâches terminées
   * Tâches traitées
   * Tâches en file d’attente

**returnWorkflowJobTopicInfo** Répertorie les informations de traitement des tâches de workflow, organisées par rubrique.

* Arguments : aucun
* Valeur renvoyée : données présentées sous forme de tableau, qui contient les colonnes suivantes :

   * Nom de la rubrique
   * Temps de traitement moyen
   * Temps d’attente moyen
   * Tâches annulées
   * Tâches en échec
   * Tâches terminées
   * Tâches traitées

**returnFailedWorkflowCount** Affiche le nombre d’instances de workflow ayant échoué. Vous pouvez spécifier un modèle de workflow pour interroger ou extraire les informations pour tous les modèles de workflow.

* Arguments :

   * Modèle : ID du modèle à interroger. Pour afficher le nombre d’instances de workflows ayant échoué pour tous les modèles de workflows, ne spécifiez aucune valeur. L’ID est le chemin d’accès au nœud de modèle, par exemple :

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* Valeur renvoyée : nombre d’instances de workflow ayant échoué.

**returnFailedWorkflowCountPerModel** Affiche le nombre d’instances de workflow ayant échoué pour chaque modèle de workflow.

* Arguments : aucun.
* Valeur renvoyée : données présentées sous forme de tableau, qui contient les colonnes Nombre et ID de modèle.

**terminateFailedInstances** Interrompt les instances de workflow ayant échoué. Vous pouvez interrompre toutes les instances ayant échoué ou uniquement les instances ayant échoué pour un modèle spécifique. Vous avez la possibilité de redémarrer les instances après les avoir interrompues. Vous pouvez également tester l’opération pour afficher les résultats sans effectuer réellement l’opération.

* Arguments :

   * Redémarrez l’instance : (facultatif) spécifiez la valeur `true` pour redémarrer les instances après les avoir interrompues. La valeur par défaut `false` n’entraîne pas le redémarrage des instances de workflow interrompues.
   * Exécution d’essai : (facultatif) spécifiez la valeur `true` pour afficher les résultats de l’opération sans effectuer réellement l’opération. La valeur par défaut `false` entraîne l’exécution de l’opération.
   * Modèle : (facultatif) ID du modèle auquel l’opération est appliquée. Ne spécifiez aucun modèle pour appliquer l’opération aux instances ayant échoué de tous les modèles de workflows. L’ID est le chemin d’accès au nœud de modèle, par exemple :

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* Valeur renvoyée : données sur les instances interrompues présentées sous forme de tableau, qui contient les colonnes suivantes :

   * Initiateur
   * ID d’instance
   * ID de modèle
   * Payload
   * Commentaire de début
   * Titre du workflow

**retryFailedWorkItems** Tente d’exécuter les étapes d’une tâche ayant échoué. Vous pouvez tenter de réexécuter toutes les tâches ayant échoué ou seulement les tâches ayant échoué pour un modèle de workflow spécifique. Vous avez la possibilité de tester l’opération pour afficher les résultats sans effectuer réellement l’opération.

* Arguments :

   * Exécution d’essai : (facultatif) spécifiez la valeur `true` pour afficher les résultats de l’opération sans effectuer réellement l’opération. La valeur par défaut `false` entraîne l’exécution de l’opération.
   * Modèle : (facultatif) ID du modèle auquel l’opération est appliquée. Ne spécifiez aucun modèle pour appliquer l’opération aux tâches ayant échoué pour tous les modèles de workflows. L’ID est le chemin d’accès au nœud de modèle, par exemple :

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* Valeur renvoyée : données sur les tâches ayant échoué qui ont été retentées, présentées sous forme de tableau, qui contient les colonnes suivantes :

   * Initiateur
   * ID d’instance
   * ID de modèle
   * Payload
   * Commentaire de début
   * Titre du workflow

**PurgeActive** Supprime les instances de workflows actives d’une ancienneté déterminée. Vous pouvez purger des instances actives pour tous les modèles ou pour un modèle spécifique seulement. Vous avez la possibilité de tester l’opération pour afficher les résultats sans effectuer réellement l’opération.

* Arguments :

   * Modèle : (facultatif) ID du modèle auquel l’opération est appliquée. Ne spécifiez aucun modèle pour appliquer l’opération aux instances de workflows de tous les modèles de workflows. L’ID est le chemin d’accès au nœud de modèle, par exemple :

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`
   * Nombre de jours écoulés depuis le début du workflow : ancienneté des instances de workflows à purger, exprimée en jours.
   * Exécution d’essai : (facultatif) spécifiez la valeur `true` pour afficher les résultats de l’opération sans effectuer réellement l’opération. La valeur par défaut `false` entraîne l’exécution de l’opération.

* Valeur renvoyée : données sur les instances de workflows actives purgées, présentées sous forme de tableau, qui contient les colonnes suivantes :

   * Initiateur
   * ID d’instance
   * ID de modèle
   * Payload
   * Commentaire de début
   * Titre du workflow

**countStaleWorkflows** Renvoie le nombre d’instances de workflows obsolètes. Vous pouvez extraire le nombre d’instances obsolètes pour tous les modèles de workflows ou pour un modèle spécifique.

* Arguments :

   * Modèle : (facultatif) ID du modèle auquel l’opération est appliquée. Ne spécifiez aucun modèle pour appliquer l’opération aux instances de workflows de tous les modèles de workflows. L’ID est le chemin d’accès au nœud de modèle, par exemple :

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* Valeur renvoyée : nombre d’instances de workflows obsolètes.

**restartStaleWorkflows** Redémarrez les instances de workflows obsolètes. Vous pouvez redémarrer toutes les instances obsolètes ou seulement les instances obsolètes pour un modèle spécifique. Vous pouvez également tester l’opération pour afficher les résultats sans effectuer réellement l’opération.

* Arguments :

   * Modèle : (facultatif) ID du modèle auquel l’opération est appliquée. Ne spécifiez aucun modèle pour appliquer l’opération aux instances obsolètes de tous les modèles de workflows. L’ID est le chemin d’accès au nœud de modèle, par exemple :

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`
   * Exécution d’essai : (facultatif) spécifiez la valeur `true` pour afficher les résultats de l’opération sans effectuer réellement l’opération. La valeur par défaut `false` entraîne l’exécution de l’opération.

* Valeur renvoyée : une liste d’instances de workflows redémarrées.

**fetchModelList** Répertorie tous les modèles de workflows.

* Arguments : aucun
* Valeur renvoyée : données identifiant les modèles de workflows, présentées sous forme de tableau, qui contient les colonnes ID de modèle et Nom du modèle.

**countRunningWorkflows** Renvoie le nombre d’instances de workflows en cours d’exécution. Vous pouvez extraire le nombre d’instances en cours d’exécution pour tous les modèles de workflows ou pour un modèle spécifique.

* Arguments :

   * Modèle : (facultatif) ID du modèle pour lequel le nombre d’instances exécutées est renvoyé. Ne spécifiez aucun modèle pour renvoyer le nombre d’instances exécutées pour tous les modèles de workflows. L’ID est le chemin d’accès au nœud de modèle, par exemple :

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* Valeur renvoyée : nombre d’instances de workflows en cours d’exécution.

**countCompletedWorkflows** Renvoie le nombre d’instances de workflows terminées. Vous pouvez extraire le nombre d’instances terminées pour tous les modèles de workflows ou pour un modèle spécifique.

* Arguments :

   * Modèle : (facultatif) ID du modèle pour lequel le nombre d’instances terminées est renvoyé. Ne spécifiez aucun modèle pour renvoyer le nombre d’instances terminées pour tous les modèles de workflows. L’ID est le chemin d’accès au nœud de modèle, par exemple :

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* Valeur renvoyée : nombre d’instances de workflows terminées.

**purgeCompleted** Supprime du référentiel les enregistrements des workflows terminés disposant d’une ancienneté spécifique. Utilisez régulièrement cette opération pour réduire la taille du référentiel lorsque vous utilisez intensivement des workflows. Vous pouvez purger les instances terminées pour tous les modèles ou pour un modèle spécifique seulement. Vous avez la possibilité de tester l’opération pour afficher les résultats sans effectuer réellement l’opération.

* Arguments :

   * Modèle : (facultatif) ID du modèle auquel l’opération est appliquée. Ne spécifiez aucun modèle pour appliquer l’opération aux instances de workflows de tous les modèles de workflows. L’ID est le chemin d’accès au nœud de modèle, par exemple :

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`
   * Nombre de jours écoulés depuis la fin du workflow : nombre de jours pendant lesquels les instances de workflows ont eu le statut Terminé.
   * Exécution d’essai : (facultatif) spécifiez la valeur `true` pour afficher les résultats de l’opération sans effectuer réellement l’opération. La valeur par défaut `false` entraîne l’exécution de l’opération.

* Valeur renvoyée : données sur les instances de workflows terminées purgées, présentées sous forme de tableau, qui contient les colonnes suivantes :

   * Initiateur
   * ID d’instance
   * ID de modèle
   * Payload
   * Commentaire de début
   * Titre du workflow

## Référentiel {#repository}

Informations sur le référentiel CRX

* Domaine : com.adobe.granite
* Type : référentiel

### Attributs {#attributes}

**Name** Nom de la mise en œuvre du référentiel JCR. Lecture seule.

**Version** Version de la mise en œuvre du référentiel. Lecture seule.

**HomeDir** Répertoire dans lequel se trouve le référentiel. L’emplacement par défaut est &lt;QuickStart_Jar_Location>/crx-quickstart/repository. Lecture seule.

**CustomerName** Nom du client pour lequel la licence du logiciel est émise. Lecture seule.

**LicenseKey** Clé de licence unique pour cette installation du référentiel. Lecture seule.

**AvailableDiskSpace** Espace disque disponible pour cette instance du référentiel, en mégaoctets (Mo). Lecture seule.

**MaximumNumberOfOpenFiles** Nombre de fichiers pouvant être ouverts simultanément. Lecture seule.

**SessionTracker** Valeur de la variable système crx.debug.sessions. La valeur true indique une session de débogage. La valeur false indique une session normale. Lecture/écriture.

**Descriptors** Ensemble de paires clé-valeur, qui représentent les propriétés du référentiel. Toutes les propriétés sont en lecture seule.

<table>
 <tbody>
  <tr>
   <th>Clé</th>
   <th>Valeur</th>
  </tr>
  <tr>
   <td>option.node.and.property.with.same.name.supported</td>
   <td>Indique si un nœud et une propriété du nœud peuvent porter le même nom. La valeur true indique qu’il est possible de leur attribuer le même nom, la valeur false, que cela ne l’est pas. </td>
  </tr>
  <tr>
   <td>identifier.stability</td>
   <td>Indique la stabilité des identifiants de nœud non référençables. Les valeurs possibles sont les suivantes :
    <ul>
     <li>identifier.stability.indefinite.duration : les identifiants ne changent pas.</li>
     <li>identifier.stability.method.duration : les identifiants peuvent changer entre les appels de la méthode.</li>
     <li>identifier.stability.save.duration : les identifiants ne changent pas au cours d’un cycle d’enregistrement/actualisation.</li>
     <li>identifier.stability.session.duration : les identifiants ne changent pas au cours d’une session.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>query.xpath.pos.index</td>
   <td>Indique si le langage de requête XPath JCR 1.0 est pris en charge. La valeur true indique que ce langage est pris en charge, la valeur false indique qu’il ne l’est pas.</td>
  </tr>
  <tr>
   <td>crx.repository.systemid</td>
   <td>Identifiant système figurant dans le fichier system.id.</td>
  </tr>
  <tr>
   <td>option.query.sql.supported</td>
   <td>Indique si le langage de requête XPath JCR 1.0 est pris en charge. La valeur true indique que ce langage est pris en charge, la valeur false indique qu’il ne l’est pas.</td>
  </tr>
  <tr>
   <td>jcr.repository.version</td>
   <td>Version de la mise en œuvre du référentiel.</td>
  </tr>
  <tr>
   <td>option.update.primary.node.type.supported</td>
   <td>Indique si le type de nœud principal d’un nœud peut être modifié. La valeur true indique que vous pouvez modifier le type de nœud principal, la valeur false indique que cela n’est pas possible.</td>
  </tr>
  <tr>
   <td>option.node.type.management.supported</td>
   <td>Indique si la gestion du type de nœud est prise en charge. La valeur true indique que la gestion est prise en charge, la valeur false, qu’elle ne l’est pas.</td>
  </tr>
  <tr>
   <td>node.type.management.overrides.supported</td>
   <td>Indique si vous pouvez remplacer la propriété héritée ou la définition de nœud enfant d’un type de nœud. La valeur true indique que les remplacements sont pris en charge, la valeur false qu’ils ne le sont pas.</td>
  </tr>
  <tr>
   <td>option.observation.supported</td>
   <td>La valeur true indique que l’observation asynchrone des modifications apportées au référentiel est prise en charge. La prise en charge de l’observation asynchrone permet aux applications de recevoir et de répondre aux notifications concernant chaque modification au fur et à mesure de leur apparition.</td>
  </tr>
  <tr>
   <td>query.jcrscore</td>
   <td><p>La valeur true indique que la pseudo-propriété jcr:score est disponible dans les requêtes XPath et SQL, qui comportent une fonction jcrfn:contains (dans XPath) ou CONTAINS (dans SQL) pour effectuer une recherche en texte intégral.</p> </td>
  </tr>
  <tr>
   <td>option.simple.versioning.supported</td>
   <td>La valeur true indique que le référentiel prend en charge le contrôle de version simple. Avec le contrôle de version simple, le référentiel conserve une série séquentielle des versions d’un nœud.</td>
  </tr>
  <tr>
   <td>option.workspace.management.supported</td>
   <td>La valeur true indique que le référentiel prend en charge la création et la suppression des espaces de travail à l’aide d’API.</td>
  </tr>
  <tr>
   <td>option.update.mixin.node.types.supported</td>
   <td>La valeur true indique que le référentiel prend en charge l’ajout et la suppression des types de nœuds Mixin d’un nœud existant.</td>
  </tr>
  <tr>
   <td>node.type.management.primary.item.name.supported</td>
   <td>La valeur true indique que le référentiel permet aux définitions de nœud de contenir un élément principal en tant qu’enfant. Un élément principal est accessible à l’aide de l’API sans connaître le nom de l’élément.</td>
  </tr>
  <tr>
   <td>level.2.supported</td>
   <td>La valeur true indique que LEVEL_1_SUPPORTED et OPTION_XML_IMPORT_SUPPORTED sont définis sur true.</td>
  </tr>
  <tr>
   <td>write.supported</td>
   <td>La valeur true indique que le référentiel fournit un accès en écriture à l’aide de l’API. La valeur false indique un accès en lecture seule.</td>
  </tr>
  <tr>
   <td>node.type.management.update.in.us e.supported</td>
   <td>La valeur true indique que vous pouvez modifier les définitions de nœud utilisées par les nœuds existants.</td>
  </tr>
  <tr>
   <td>jcr.specification.version</td>
   <td>Version de la spécification JCR mise en œuvre par le référentiel.</td>
  </tr>
  <tr>
   <td>option.journaled.observation.supported</td>
   <td>La valeur true indique que les applications peuvent effectuer une observation journalisée du référentiel. Avec l’observation journalisée, un ensemble de notifications de modification peut être obtenu pour une période spécifiée. </td>
  </tr>
  <tr>
   <td>query.languages</td>
   <td>Langages de requête pris en charge par le référentiel. Si aucune valeur n’est définie, les requêtes ne sont pas prises en charge.</td>
  </tr>
  <tr>
   <td>option.xml.export.supported</td>
   <td>La valeur true indique que le référentiel prend en charge l’exportation des nœuds sous forme de code XML.</td>
  </tr>
  <tr>
   <td>node.type.management.multiple.binary.properties.supported</td>
   <td>La valeur true indique que le référentiel prend en charge l’enregistrement des types de nœuds comportant plusieurs propriétés de fichier binaire. La valeur false indique qu’une seule propriété binaire est prise en charge pour un type de nœud.</td>
  </tr>
  <tr>
   <td>option.access.control.supported</td>
   <td>La valeur true indique que le référentiel prend en charge le contrôle d’accès pour définir et déterminer les droits d’utilisateur pour l’accès au nœud.</td>
  </tr>
  <tr>
   <td>option.baselines.supported</td>
   <td>La valeur true indique que le référentiel prend en charge les configurations et les lignes de base.</td>
  </tr>
  <tr>
   <td>option.shareable.nodes.supported</td>
   <td>La valeur true indique que le référentiel prend en charge la création de nœuds partageables.</td>
  </tr>
  <tr>
   <td>crx.cluster.id</td>
   <td>Identifiant du cluster du référentiel.</td>
  </tr>
  <tr>
   <td>query.stored.queries.supported</td>
   <td>La valeur true indique que le référentiel prend en charge les requêtes enregistrées.</td>
  </tr>
  <tr>
   <td>query.full.text.search.supported</td>
   <td>La valeur true indique que le référentiel prend en charge la recherche de texte intégral.</td>
  </tr>
  <tr>
   <td>node.type.management.inheritance</td>
   <td><p>Indique le niveau de prise en charge du référentiel pour l’héritage du type de nœud. Les valeurs possibles sont les suivantes :</p> <p>node.type.management.inheritance.minimal : l’enregistrement des types de nœuds principaux se limite aux types qui contiennent uniquement le supertype nt:base. L’enregistrement des types de nœuds Mixin se limite aux types ne comportant pas de supertype.</p> <p>node.type.management.inheritance.single : l’enregistrement des types de nœuds principaux se limite aux types comportant un seul supertype. L’enregistrement des types de nœuds Mixin se limite aux types comportant un supertype au maximum.</p> <p><br /> node.type.management.inheritance.multiple : les types de nœuds principaux peuvent être enregistrés avec un ou plusieurs supertypes. Les types de nœuds Mixin peuvent être enregistrés sans supertype ou avec un ou plusieurs supertypes.</p> </td>
  </tr>
  <tr>
   <td>crx.cluster.preferredMaster</td>
   <td>La valeur true indique que ce nœud de cluster est le maître préféré du cluster.</td>
  </tr>
  <tr>
   <td>option.transactions.supported</td>
   <td>La valeur true indique que le référentiel prend en charge les transactions.</td>
  </tr>
  <tr>
   <td>jcr.repository.vendor.url</td>
   <td>Adresse URL du fournisseur de référentiel.</td>
  </tr>
  <tr>
   <td>node.type.management.value.constraints.supported</td>
   <td>La valeur true indique que le référentiel prend en charge les contraintes de valeur des propriétés de nœud.</td>
  </tr>
  <tr>
   <td>node.type.management.property.types</td>
   <td>Tableau de constantes javax.jcr.PropertyType, qui représentent les types de propriétés qu’un type de nœud enregistré peut spécifier. Un tableau dont la longueur est égale à zéro indique que les types de nœuds enregistrés ne peuvent pas spécifier de définitions de propriétés. Les types de propriétés sont STRING, URI, BOOLEAN, LONG, DOUBLE, DECIMAL, BINARY, DATE, NAME, PATH, WEAKREFERENCE, REFERENCE et UNDEFINED (s’ils sont pris en charge).</td>
  </tr>
  <tr>
   <td>node.type.management.orderable.child.nodes.supported</td>
   <td>La valeur true indique que le référentiel prend en charge la conservation de l’ordre des nœuds enfants.</td>
  </tr>
  <tr>
   <td>jcr.repository.vendor</td>
   <td>Nom du fournisseur de référentiel.</td>
  </tr>
  <tr>
   <td>query.joins</td>
   <td><p>Niveau de prise en charge des jointures dans les requêtes. Les valeurs possibles sont les suivantes :</p>
    <ul>
     <li>query.joins.none : jointures non prises en charge. Les requêtes peuvent utiliser un sélecteur.</li>
     <li>query.joins.inner : prise en charge des jointures internes.</li>
     <li>query.joins.inner.outer : prise en charge des jointures internes et externes.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>org.apache.jackrabbit.spi.commons.AdditionalEventInfo</td>
   <td> </td>
  </tr>
  <tr>
   <td>query.xpath.doc.order</td>
   <td>La valeur true indique que le référentiel prend en charge le langage de requête XPath 1.0.</td>
  </tr>
  <tr>
   <td>query.jcrpath</td>
   <td> </td>
  </tr>
  <tr>
   <td>option.xml.import.supported</td>
   <td>La valeur true indique que le référentiel prend en charge l’importation de code XML sous forme de contenu.</td>
  </tr>
  <tr>
   <td>node.type.management.same.name.siblings.supported</td>
   <td>La valeur true indique que le référentiel prend en charge des nœuds apparentés (nœuds possédant le même parent) portant le même nom.</td>
  </tr>
  <tr>
   <td>node.type.management.residual.definitions.supported</td>
   <td>La valeur true indique que le référentiel prend en charge les propriétés de nom avec des définitions résiduelles. Si cette version est prise en charge, l’attribut de nom d’une définition d’élément peut être un astérisque (« * »).</td>
  </tr>
  <tr>
   <td>node.type.management.autocreated.definitions.supported</td>
   <td>La valeur true indique que le référentiel prend en charge la création automatique des éléments (nœuds ou propriétés) enfants d’un nœud lorsque le nœud est créé.</td>
  </tr>
  <tr>
   <td>crx.cluster.master</td>
   <td>La valeur true indique que ce référentiel est le nœud maître du cluster.</td>
  </tr>
  <tr>
   <td>level.1.supported</td>
   <td>La valeur true indique que option.xml.export.support est vrai et que query.languages possède une longueur non nulle.</td>
  </tr>
  <tr>
   <td>option.unfiled.content.supported</td>
   <td>La valeur true indique que le référentiel prend en charge le contenu non classé. Les nœuds non classés ne font pas partie de la hiérarchie du référentiel.</td>
  </tr>
  <tr>
   <td>jcr.specification.name</td>
   <td>Nom de la spécification JCR mise en œuvre par le référentiel.</td>
  </tr>
  <tr>
   <td>option.versioning.supported</td>
   <td>La valeur true indique que le référentiel prend en charge le contrôle de version complet.</td>
  </tr>
  <tr>
   <td>jcr.repository.name</td>
   <td>Nom du référentiel.</td>
  </tr>
  <tr>
   <td>option.locking.supported</td>
   <td>La valeur true indique que le référentiel prend en charge le verrouillage des nœuds. Grâce au verrouillage, un utilisateur peut empêcher temporairement les autres utilisateurs d’apporter des modifications.</td>
  </tr>
  <tr>
   <td>jcr.repository.version.display</td>
   <td> </td>
  </tr>
  <tr>
   <td>option.activities.supported</td>
   <td>La valeur true indique que le référentiel prend en charge des activités. Les activités sont un ensemble de modifications apportées à un espace de travail, qui sont fusionnées dans un autre espace de travail.</td>
  </tr>
  <tr>
   <td>node.type.management.multivalued.properties.supported</td>
   <td>La valeur true indique que le référentiel prend en charge les propriétés de nœud qui peuvent ne comporter aucune valeur ou comporter une ou plusieurs valeurs.</td>
  </tr>
  <tr>
   <td>option.retention.supported</td>
   <td>La valeur true indique que le référentiel prend en charge l’utilisation d’applications externes de gestion de la conservation pour appliquer des stratégies de conservation à du contenu et prend en charge la rétention et la diffusion.</td>
  </tr>
  <tr>
   <td>option.lifecycle.supported</td>
   <td>La valeur true indique que le référentiel prend en charge la gestion du cycle de vie.</td>
  </tr>
 </tbody>
</table>

**WorkspaceNames** Nom des espaces de travail dans le référentiel. Lecture seule.

**DataStoreGarbageCollectionDelay** Délai, en millisecondes, pendant lequel le nettoyage est mis en veille après l’analyse de chaque dixième nœud. Lecture/écriture.

**BackupDelay** Délai, en millisecondes, pendant lequel le processus de sauvegarde est mis en veille entre chaque étape de la sauvegarde. Lecture/écriture.

**BackupInProgress** Une valeur true indique qu’un processus de sauvegarde est en cours d’exécution. Lecture seule.

**BackupProgress** Pour la sauvegarde actuelle, pourcentage de tous les fichiers sauvegardés. Lecture seule.

**CurrentBackupTarget** Pour la sauvegarde actuelle, fichier ZIP dans lequel les fichiers de sauvegarde sont enregistrés. Lorsqu’il n’y a pas de sauvegarde en cours, aucune valeur ne s’affiche. Lecture seule.

**BackupWasSuccessful** La valeur true indique qu’aucune erreur ne s’est produite lors de la sauvegarde actuelle ou qu’aucune sauvegarde n’est en cours. La valeur false indique qu’une erreur s’est produite lors de la sauvegarde actuelle. Lecture seule.

**BackupResult** Statut de la sauvegarde actuelle. Les valeurs possibles sont les suivantes :

* Sauvegarde en cours : une sauvegarde est en cours d’exécution.
* Sauvegarde annulée : la sauvegarde a été annulée.
* Sauvegarde terminée avec une erreur : une erreur s’est produite lors de la sauvegarde. Le message d’erreur contient des informations sur la cause.
* Sauvegarde terminée : la sauvegarde a réussi.
* Aucune sauvegarde exécutée jusque-là : il n’y a pas de sauvegarde en cours.

Lecture seule.

**TarOptimizationRunningSince** Heure à laquelle le processus d’optimisation actuel du fichier TAR a commencé. Lecture seule.

**TarOptimizationDelay** Délai, en millisecondes, pendant lequel le processus d’optimisation du fichier TAR est mis en veille entre chaque étape du processus. Lecture/écriture.

**ClusterProperties** Ensemble de paires clé-valeur, qui représente les propriétés et les valeurs du cluster. Chaque ligne du tableau représente une propriété du cluster. Lecture seule.

**ClusterNodes** Membres du cluster de référentiel.

**ClusterId** Identifiant de ce cluster de référentiel. Lecture seule.

**ClusterMasterId** Identifiant du nœud maître de ce cluster de référentiel. Lecture seule.

**ClusterNodeId** Identifiant de ce nœud du cluster de référentiel. Lecture seule.

### Opérations {#operations-1}

**createWorkspace** Crée un espace de travail dans ce référentiel.

* Arguments :

   * name : valeur de chaîne, qui représente le nom du nouvel espace de travail.

* Valeur renvoyée : aucune

**runDataStoreGarbageCollection** Exécute le nettoyage sur les nœuds du référentiel.

* Arguments :

   * delete : valeur booléenne, qui indique si les éléments inutilisés du référentiel doivent être supprimés. La valeur true entraîne la suppression des nœuds et des propriétés inutilisés. La valeur false entraîne l’analyse de tous les nœuds, mais aucun nœud n’est supprimé.

* Valeur renvoyée : aucune

**stopDataStoreGarbageCollection** Arrête le nettoyage en cours d’un entrepôt de données.

* Arguments : aucun
* Valeur renvoyée : représentation de l’état actuel, sous forme de chaîne

**startBackup** Sauvegarde les données du référentiel dans un fichier ZIP.

* Arguments :

   * `target` : (facultatif) valeur de `String`, qui représente le nom du fichier ZIP ou d’un répertoire dans lequel archiver les données du référentiel. Pour utiliser un fichier ZIP, incluez l’extension du nom de fichier ZIP. Pour utiliser un répertoire, n’incluez pas d’extension de nom de fichier.

      Pour effectuer une sauvegarde incrémentielle, spécifiez le répertoire qui a déjà été utilisé pour la sauvegarde.

        Vous pouvez spécifier un chemin d’accès absolu ou relatif. Les chemins d’accès relatifs le sont par rapport au parent du répertoire crx-quickstart.

      Lorsque vous ne spécifiez aucune valeur, la valeur par défaut `backup-currentdate.zip` est utilisée, où `currentdate` est au format `yyyyMMdd-HHmm`.

* Valeur renvoyée : aucune

**cancelBackup** Arrête le processus de sauvegarde en cours et supprime l’archive temporaire créée par le processus pour archiver les données.

* Arguments : aucun
* Valeur renvoyée : aucune

**blockRepositoryWrites** Empêche d’apporter des modifications aux données du référentiel. Tous les programmes d’écoute de la sauvegarde du référentiel sont informés du blocage.

* Arguments : aucun
* Valeur renvoyée : aucune

**unblockRepositoryWrites** Supprime le blocage du référentiel. Tous les programmes d’écoute de la sauvegarde du référentiel sont informés de la levée du blocage.

* Arguments : aucun
* Valeur renvoyée : aucune

**startTarOptimization** Commence le processus d’optimisation du fichier TAR à l’aide de la valeur par défaut pour tarOptimizationDelay.

* Arguments : aucun
* Valeur renvoyée : aucune

**stopTarOptimization** Interrompt l’optimisation du fichier TAR.

* Arguments : aucun
* Valeur renvoyée : aucune

**tarIndexMerge** Fusionne les fichiers d’index de niveau supérieur de tous les ensembles TAR. Les fichiers d’index de niveau supérieur sont des fichiers comportant des versions principales différentes. Par exemple, les fichiers ci-dessous sont fusionnés dans le fichier file index_3_1.tar: index_1_1.tar, index_2_0.tar, index_3_0.tar. Les fichiers fusionnés sont supprimés (dans l’exemple précédent, index_1_1.tar, index_2_0.taret index_3_0.tar sont supprimés).

* Arguments :

   * `background` : valeur booléenne, qui indique si l’opération doit être exécutée en arrière-plan afin que la console web soit utilisable lors de l’exécution. La valeur true exécute l’opération en arrière-plan.

* Valeur renvoyée : aucune

**becomeClusterMaster** Définit ce nœud de référentiel comme nœud maître du cluster. S’il n’est pas déjà le nœud principal, cette commande arrête le programme d’écoute de l’instance principale actuelle et démarre un programme d’écoute sur le nœud actuel. Ce nœud est ensuite défini comme nœud principal et redémarre, ce qui fait que tous les autres nœuds du cluster (c’est-à-dire ceux qui sont contrôlés par le nœud principal) se connectent à cette instance.

* Arguments : aucun
* Valeur renvoyée : aucune

**joinCluster** Ajoute ce référentiel à un cluster en tant que nœud contrôlé par le nœud principal du cluster. Vous devez fournir un nom d’utilisateur et un mot de passe pour l’authentification. La connexion utilise l’authentification de base. Les informations de connexion de sécurité sont codées en base 64 avant d’être envoyées au serveur.

* Arguments :

   * `master` : valeur de chaîne, qui représente l’adresse IP ou le nom de l’ordinateur qui exécute le nœud de référentiel principal.
   * `username` : nom à utiliser pour l’authentification au niveau du cluster.
   * `password` : mot de passe à utiliser pour l’authentification.

* Valeur renvoyée : aucune

**traversalCheck** Parcourt et corrige, éventuellement, les incohérences d’une sous-arborescence, en commençant par un nœud spécifique. Cet aspect est abordé en détail dans la documentation sur les gestionnaires de persistance.

**consistencyCheck** Vérifie et corrige, éventuellement, les incohérences dans l’entrepôt de données. Cet aspect est abordé en détail dans la documentation sur l’entrepôt de données.

## Statistiques du référentiel (TimeSeries) {#repository-statistics-timeseries}

Valeur du champ TimeSeries pour chaque type de statistiques défini par `org.apache.jackrabbit.api.stats.RepositoryStatistics`.

* Domaine : `com.adobe.granite`
* Type : `TimeSeries`
* Nom : l’une des valeurs ci-dessous de la classe d’énumération `org.apache.jackrabbit.api.stats.RepositoryStatistics.Type` :

   * BUNDLE_CACHE_ACCESS_COUNTER
   * BUNDLE_CACHE_MISS_AVERAGE
   * BUNDLE_CACHE_MISS_COUNTER
   * BUNDLE_CACHE_MISS_DURATION
   * BUNDLE_CACHE_SIZE_COUNTER
   * BUNDLE_COUNTER
   * BUNDLE_READ_COUNTER
   * BUNDLE_WRITE_AVERAGE
   * BUNDLE_WRITE_COUNTER
   * BUNDLE_WRITE_DURATION
   * BUNDLE_WS_SIZE_COUNTER
   * QUERY_AVERAGE
   * QUERY_COUNT
   * QUERY_DURATION
   * SESSION_COUNT
   * SESSION_LOGIN_COUNTER
   * SESSION_READ_AVERAGE
   * SESSION_READ_COUNTER
   * SESSION_READ_DURATION
   * SESSION_WRITE_AVERAGE
   * SESSION_WRITE_COUNTER
   * SESSION_WRITE_DURATION

### Attributs {#attributes-1}

Les attributs ci-dessous sont fournis pour chaque type de statistique faisant l’objet d’un compte-rendu :

* ValuePerSecond : valeur mesurée par seconde au cours de la dernière minute. Lecture seule.
* ValuePerMinute : valeur mesurée par minute au cours de la dernière heure. Lecture seule.
* ValuePerHour : valeur mesurée par heure au cours de la dernière semaine. Lecture seule.
* ValuePerWeek : valeur mesurée par semaine au cours des trois dernières années. Lecture seule.

## Statistiques des requêtes dans le référentiel {#repository-query-stats}

Informations statistiques sur les requêtes dans le référentiel.

* Domaine : com.adobe.granite
* Type : QueryStat

### Attributs {#attributes-2}

**SlowQueries** Informations sur les requêtes dans le référentiel qui ont pris le plus de temps. Lecture seule.

**SlowQueriesQueueSize** Nombre maximal de requêtes à inclure dans la liste de SlowQueries. Lecture-écriture.

**PopularQueries** Informations sur les requêtes dans le référentiel exécutées le plus souvent. Lecture seule.

**PopularQueriesQueueSize** Nombre maximal de requêtes dans la liste de PopularQueries. Lecture-écriture.

### Opérations {#operations-2}

**clearSlowQueriesQueue** Supprime toutes les requêtes de la liste SlowQueries.

* Arguments : aucun
* Valeur renvoyée : aucune

**clearPopularQueriesQueue** Supprime toutes les requêtes de la liste PopularQueries.

* Arguments : aucun
* Valeur renvoyée : aucune

## Agents de réplication {#replication-agents}

Surveillez les services pour chaque agent de réplication. Lorsque vous créez un agent de réplication, le service s’affiche automatiquement dans la console JMX.

* **Domaine** : com.adobe.granite.replication
* **Type** : agent
* **Nom** : aucune valeur
* **Propriétés** : {id=&quot;*Name*&quot;}, où *Name* est la valeur de la propriété Name de l’agent.

### Attributs {#attributes-3}

**Id** Valeur de chaîne qui représente l’identifiant de la configuration de l’agent de réplication. Plusieurs agents peuvent utiliser la même configuration. Lecture seule.

**Valid** Valeur booléenne qui indique si l’agent est configuré correctement :

* `true` : configuration valide.
* `false` : la configuration contient des erreurs.

Lecture seule.

**Enabled** Valeur booléenne qui indique si l’agent est activé :

* `true` : activé.
* `false` : désactivé.

**QueueBlocked** Valeur booléenne qui indique si la file d’attente existe et si elle est bloquée :

* `true` : bloquée. Une nouvelle tentative automatique est en attente.
* `false` : non bloquée ou inexistante.

Lecture seule.

**QueuePaused** Valeur booléenne qui indique si la file d’attente de tâches est suspendue :

* `true` : suspendue.
* `false` : non suspendue ou inexistante.

Lecture-écriture.

**QueueNumEntries** Valeur d’entier (int) représentant le nombre de tâches dans la file d’attente de l’agent. Lecture seule.

**QueueStatusTime** Valeur Date indiquant le temps passé sur le serveur une fois que les valeurs de statut affichées ont été obtenues. La valeur correspond au délai de chargement de la page. Lecture seule.

**QueueNextRetryTime** Pour les files d’attente bloquées, valeur Date indiquant le moment auquel la tentative automatique suivante aura lieu. Lorsque aucun délai ne s’affiche, la file d’attente n’est pas bloquée. Lecture seule.

**QueueProcessingSince** Valeur Date indiquant le moment auquel le traitement a commencé pour la tâche actuelle. Lorsque aucun délai ne s’affiche, la file d’attente est bloquée ou inactive. Lecture seule.

**QueueLastProcessTime** Valeur Date indiquant le moment auquel la tâche précédente s’est terminée. Lecture seule.

### Opérations {#operations-3}

**queueForceRetry** Pour les files d’attente bloquées, exécute la commande retry dans la file d’attente.

* Arguments : aucun
* Valeur renvoyée : aucune

**queueClear** Supprime toutes les tâches de la file d’attente.

* Arguments : aucun
* Valeur renvoyée : aucune

## Moteur Sling {#sling-engine}

Fournit des statistiques sur les demandes HTTP afin de pouvoir surveiller les performances du service SlingRequestProcessor.

* Domaine : org.apache.sling
* Type : moteur
* Propriétés : {service=RequestProcessor}

### Attributs {#attributes-4}

**RequestsCount** Nombre de demandes exécutées depuis que les statistiques ont été réinitialisées pour la dernière fois.

**MinRequestDurationMsec** Délai le plus court (en millisecondes) nécessaire pour traiter une demande depuis que les statistiques ont été réinitialisées pour la dernière fois.

**MaxRequestDuratioMsec** Durée la plus longue (en millisecondes) nécessaire pour traiter une demande depuis que les statistiques ont été réinitialisées pour la dernière fois.

**StandardDeviationDurationMsec** Écart-type du délai nécessaire pour traiter des demandes. L’écart-type est calculé à l’aide de toutes les demandes depuis que les statistiques ont été réinitialisées pour la dernière fois.

**MeanRequestDurationMsec** Délai moyen nécessaire pour traiter une demande. La moyenne est calculée à l’aide de toutes les demandes depuis que les statistiques ont été réinitialisées pour la dernière fois.

### Opérations {#operations-4}

**resetStatistics** Définit toutes les statistiques sur zéro. Réinitialisez les statistiques lorsque vous devez analyser les performances de traitement des demandes pendant une période spécifique.

* Arguments : aucun
* Valeur renvoyée : aucune

**id** Représentation sous forme de chaîne de l’ID du module.

**installed** Valeur booléenne indiquant si le module est installé :

* `true` : installé.
* `false` : non installé.

**installedBy** ID du dernier utilisateur ayant installé le module.

**installedDate** Date à laquelle le module a été installé pour la dernière fois.

**size** Valeur longue contenant la taille du module en octets.


## Lanceur de Quickstart {#quickstart-launcher}

Informations sur le processus de démarrage et le lanceur de Quickstart.

* Domaine : com.adobe.granite.quickstart
* Type : lanceur

### Opérations {#operations-5}

**Journal**

Affiche un message dans la fenêtre QuickStart.

Arguments :

* p1 : valeur de `String` représentant le message à afficher.
* Valeur renvoyée : aucune

**startupFinished**

Appelle la méthode startupFinished du lanceur du serveur. La méthode tente d’ouvrir la page d’accueil dans un navigateur web.

* Arguments : aucun
* Valeur renvoyée : aucune

**startupProgress**

Définit la valeur de fin du processus de démarrage du serveur. La barre de progression dans la fenêtre QuickStart représente la valeur de fin.

* Arguments :
   * p1 : valeur flottante représentant la quantité du processus de démarrage terminée, sous forme de fraction. La valeur doit être comprise entre zéro et un. Par exemple, 0,3 indique que le processus est terminé à 30 %.
* Valeur renvoyée : aucune.

## Services tiers {#third-party-services}

Plusieurs ressources de serveur tiers installent des beans gérés (MBeans), qui exposent des attributs et des opérations dans la console JMX. Le tableau ci-dessous répertorie les ressources tierces et contient des liens vers des informations supplémentaires.

<table>
 <tbody>
  <tr>
   <th>Domaine</th>
   <th>Type</th>
   <th>Classe MBean</th>
  </tr>
  <tr>
   <td>JMImplementation</td>
   <td>MBeanServerDelegate</td>
   <td><a href="https://docs.oracle.com/javase/8/docs/api/javax/management/MBeanServerDelegate.html">javax.management.MBeanServerDelegate</a></td>
  </tr>
  <tr>
   <td>com.sun.management</td>
   <td>HotSpotDiagnostic</td>
   <td><a href="https://docs.oracle.com/javase/8/docs/jre/api/management/extension/com/sun/management/HotSpotDiagnosticMXBean.html">com.sun.management.HotSpotDiagnosticMXBean</a></td>
  </tr>
  <tr>
   <td>java.lang</td>
   <td>
    <ul>
     <li>ClassLoading</li>
     <li>Compilation</li>
     <li>GarbageCollector</li>
     <li>Mémoire</li>
     <li>MemoryManager</li>
     <li>MemoryPool</li>
     <li>OperatingSystem</li>
     <li>Runtime</li>
     <li>Threading</li>
    </ul> </td>
   <td>module <a href="https://docs.oracle.com/javase/8/docs/api/javax/management/package-summary.html">javax.management</a></td>
  </tr>
  <tr>
   <td>java.util.logging</td>
   <td> </td>
   <td><a href="https://docs.oracle.com/javase/8/docs/api/java/util/logging/LoggingMXBean.html">java.util.logging.LoggingMXBean</a></td>
  </tr>
  <tr>
   <td>osgi.core</td>
   <td>
    <ul>
     <li>bundleState</li>
     <li>framework</li>
     <li>packageState</li>
     <li>serviceState</li>
    </ul> </td>
   <td>module <a href="https://osgi.org/specification/osgi.enterprise/7.0.0/service.jmx.html#d0e42567">org.osgi.jmx.framework</a></td>
  </tr>
 </tbody>
</table>

## Utilisation de la console JMX {#using-the-jmx-console}

La console JMX affiche des informations sur différents services exécutés sur le serveur :

* Attributs : propriétés de service, comme des configurations ou des données d’exécution. Les attributs peuvent être en lecture seule ou en lecture/écriture.
* Opérations : commandes que vous pouvez appeler dans le service.

Les MBeans déployés avec un service OSGi exposent les attributs et les opérations du service dans la console. Le MBean détermine les attributs et les opérations exposés et si les attributs sont en lecture seule ou en lecture/écriture.

La page principale de la console JMX comporte un tableau des services. Chaque ligne du tableau représente un service exposé par un MBean.

1. Ouvrez la console web et cliquez sur l’onglet JMX. ([http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))
2. Cliquez sur une valeur de cellule pour un service afin d’afficher les attributs et les opérations du service.
3. Pour modifier une valeur d’attribut, cliquez sur la valeur, spécifiez la valeur dans la boîte de dialogue qui s’affiche, puis cliquez sur Enregistrer.
4. Pour appeler une opération de service, cliquez sur le nom de l’opération, spécifiez les valeurs des arguments dans la boîte de dialogue qui s’affiche, puis cliquez sur Appeler.

## Utilisation des applications JMX externes pour la surveillance {#using-external-jmx-applications-for-monitoring}

CRX permet aux applications externes d’interagir avec les beans gérés (MBeans) par le biais de [Java Management Extensions (JMX)](https://docs.oracle.com/javase/6/docs/technotes/guides/management/overview.html). L’utilisation de consoles génériques comme [JConsole](https://java.sun.com/developer/technicalArticles/J2SE/jconsole.html) ou d’applications de surveillance spécifiques au domaine permet d’extraire et de définir les configurations et les propriétés de CRX, ainsi que de surveiller les performances et l’utilisation des ressources.

### Utilisation de JConsole pour la connexion à CRX {#using-jconsole-to-connect-to-crx}

Pour se connecter à CRX à l’aide de JConsole, procédez comme suit :

1. Ouvrez une fenêtre de terminal.
1. Saisissez la commande suivante :

   `jconsole`

JConsole démarre et la fenêtre JConsole s’affiche.

### Connexion à un processus CRX local {#connecting-to-a-local-crx-process}

JConsole affiche une liste des processus locaux de machine virtuelle Java. La liste contient deux processus QuickStart. Sélectionnez le processus « ENFANT » QuickStart dans la liste des processus locaux (il s’agit généralement du processus qui possède le PID le plus élevé).

![screen_shot_2012-03-26at114557am](assets/screen_shot_2012-03-26at114557am.png)

### Connexion à un processus CRX distant {#connecting-to-a-remote-crx-process}

Pour se connecter à un processus CRX distant, la machine virtuelle Java qui héberge le processus CRX distant doit être activée pour accepter les connexions JMX à distance.

  Pour activer les connexions JMX à distance, la propriété système ci-dessous doit être définie au démarrage de la machine virtuelle Java :

`com.sun.management.jmxremote.port=portNum`

Dans la propriété ci-dessus, `portNum` correspond au numéro de port sur lequel vous souhaitez activer les connexions RMI JMX. Veillez à spécifier un numéro de port inutilisé. Outre la publication d’un connecteur RMI pour l’accès local, la définition de cette propriété publie un autre connecteur RMI dans un registre privé en lecture seule sur le port spécifié à l’aide d’un nom bien connu, « jmxrmi ».

Par défaut, lorsque vous activez l’agent JMX pour la surveillance à distance, il utilise l’authentification par mot de passe à partir d’un fichier de mot de passe qui doit être spécifié à l’aide de la propriété système ci-dessous au démarrage de la machine virtuelle Java :

`com.sun.management.jmxremote.password.file=pwFilePath`

Pour obtenir des instructions détaillées sur la configuration d’un fichier de mot de passe, consultez la [documentation JMX correspondante](https://docs.oracle.com/javase/6/docs/technotes/guides/management/agent.html).

Exemple :

```shell
$ java
  -Dcom.sun.management.jmxremote.password.file=pwFilePath
  -Dcom.sun.management.jmxremote.port=8463
  -jar ./cq-quickstart.jar
```

### Utilisation des MBeans fournis par CRX {#using-the-mbeans-provided-by-crx}

Après la connexion au processus QuickStart, JConsole fournit différents outils de surveillance d’ordre général pour la machine virtuelle Java sur laquelle CRX est exécuté.

![screen_shot_2012-03-26at115056am](assets/screen_shot_2012-03-26at115056am.png)

Pour accéder aux options de surveillance et de configuration internes de CRX, cliquez sur l’onglet MBeans et, dans l’arborescence à gauche, sélectionnez la section Attributs ou Opérations qui vous intéresse. Par exemple, la section com.adobe.granite/Repository/Operations.

Dans cette section, sélectionnez l’attribut ou l’opération de votre choix dans le volet de gauche.

![screen_shot_2012-03-26at115728am](assets/screen_shot_2012-03-26at115728am.png)
