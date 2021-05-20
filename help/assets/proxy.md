---
title: '[!DNL Assets] développement de proxy'
description: Un proxy est un  [!DNL Experience Manager] instance that uses proxy workers to process jobs. Learn how to configure an [!DNL Experience Manager] proxy, des opérations prises en charge, des composants de proxy et la manière de développer un programme de travail de proxy personnalisé.
contentOwner: AG
role: Administrator, Architect
exl-id: 42fff236-b4e1-4f42-922c-97da32a933cf
source-git-commit: 15f83387629687994bc2ffee4156d7d42dc1c537
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 58%

---

# [!DNL Assets] développement de proxy  {#assets-proxy-development}

[!DNL Adobe Experience Manager Assets] utilise un proxy pour distribuer le traitement de certaines tâches.

Un proxy est une instance de Experience Manager spécifique (et parfois distincte) qui utilise des programmes de traitement du proxy comme processeurs chargés de gérer une tâche et de créer un résultat. Un worker de proxy peut être utilisé pour de nombreuses tâches. Dans le cas d’un proxy [!DNL Assets], il peut être utilisé pour charger des ressources pour le rendu dans Assets. Par exemple, le [worker de proxy IDS](indesign.md) utilise un serveur pour traiter les fichiers à utiliser dans  Assets.[!DNL Adobe InDesign]

Lorsque le proxy est une instance [!DNL Experience Manager] distincte, cela permet de réduire la charge sur la ou les instances de création [!DNL Experience Manager]. Par défaut, [!DNL Assets] exécute les tâches de traitement des ressources dans la même JVM (externalisée via proxy) pour réduire la charge sur l’instance de création [!DNL Experience Manager].

## Proxy (Accès HTTP) {#proxy-http-access}

Un proxy est disponible via le servlet HTTP lorsqu’il est configuré pour accepter des tâches de traitement à l’adresse : `/libs/dam/cloud/proxy`. Ce servlet crée une tâche sling à partir des paramètres publiés. Elle est ensuite ajoutée à la file d’attente des tâches du proxy et connectée au worker de proxy approprié.

### Opérations prises en charge {#supported-operations}

* `job`

   **Exigences** : le paramètre `jobevent` doit être défini en tant que correspondance de valeur en série. Il est utilisé pour créer une `Event` pour un traitement de tâche.

   **Résultat** : ajoute une nouvelle tâche. Si l’opération réussit, un identifiant de tâche unique est renvoyé.

```shell
curl -u admin:admin -F":operation=job" -F"someproperty=xxxxxxxxxxxx"
    -F"jobevent=serialized value map" http://localhost:4502/libs/dam/cloud/proxy
```

* `result`

   **Conditions requises** : le paramètre  `jobid` doit être défini.

   **Résultat** : renvoie une représentation JSON du nœud de résultats tel que créé par le processeur de tâches.

```shell
curl -u admin:admin -F":operation=result" -F"jobid=xxxxxxxxxxxx"
    http://localhost:4502   /libs/dam/cloud/proxy
```

* `resource`

   **Exigences** : le paramètre jobid doit être défini.

   **Résultat** : renvoie une ressource associée à la tâche concernée.

```shell
curl -u admin:admin -F":operation=resource" -F"jobid=xxxxxxxxxxxx"
    -F"resourcePath=something.pdf" http://localhost:4502/libs/dam/cloud/proxy
```

* `remove`

   **Exigences** : le paramètre jobid doit être défini.

   **Résultats** : supprime une tâche si elle est trouvée.

```shell
curl -u admin:admin -F":operation=remove" -F"jobid=xxxxxxxxxxxx"
    http://localhost:4502/libs/dam/cloud/proxy
```

### Worker de proxy {#proxy-worker}

Un worker de proxy est un processeur chargé de gérer une tâche et de produire un résultat. Les workers résident sur l’instance de proxy et doivent mettre en œuvre [sling JobProcessor](https://sling.apache.org/site/eventing-and-jobs.html) pour être reconnus en tant que workers de proxy.

>[!NOTE]
>
>Le worker doit mettre en œuvre [sling JobProcessor](https://sling.apache.org/site/eventing-and-jobs.html) pour être reconnu en tant que worker de proxy.

### API client {#client-api}

[`JobService`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html) est disponible en tant que service OSGi qui prévoit des méthodes pour créer des tâches, supprimer des tâches et obtenir des résultats de ces tâches. La mise en œuvre par défaut de ce service (`JobServiceImpl`) utilise le client HTTP pour communiquer avec le servlet de proxy à distance.

Voici un exemple d’utilisation d’API :

```java
@Reference
 JobService proxyJobService;

 // to create a new job
 final Hashtable props = new Hashtable();
 props.put("someproperty", "some value");
 props.put(JobUtil.PROPERTY_JOB_TOPIC, "myworker/job"); // this is an identifier of the worker
 final String jobId = proxyJobService.addJob(props, new Asset[]{asset});

 // to check status (returns JobService.STATUS_FINISHED or JobService.STATUS_INPROGRESS)
 int status = proxyJobService.getStatus(jobId)

 // to get the result
 final String jsonString = proxyJobService.getResult(jobId);

 // to remove job and cleanup
 proxyJobService.removeJob(jobId);
```

### Configurations de Cloud Service {#cloud-service-configurations}

>[!NOTE]
>
>La documentation de référence pour l’API de proxy est disponible sous [`com.day.cq.dam.api.proxy`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/proxy/package-summary.html).

Les configurations de worker de proxy et de proxy sont disponibles via les configurations de services cloud comme accessibles à partir de la console [!DNL Assets] **Outils** ou sous `/etc/cloudservices/proxy`. Chaque worker de proxy doit ajouter un noeud sous `/etc/cloudservices/proxy` pour les détails de configuration spécifiques au worker (par exemple, `/etc/cloudservices/proxy/workername`).

>[!NOTE]
>
>Voir [Configuration du traitement du proxy d’InDesign Server](indesign.md#configuring-the-proxy-worker-for-indesign-server) et [Configuration des Cloud Services](../sites-developing/extending-cloud-config.md) pour plus d’informations.

Voici un exemple d’utilisation d’API :

```java
@Reference(policy = ReferencePolicy.STATIC)
 ProxyConfig proxyConfig;

 // to get proxy config
 Configuration cloudConfig = proxyConfig.getConfiguration();
 final String value = cloudConfig.get("someProperty", "defaultValue");

 // to get worker config
 Configuration cloudConfig = proxyConfig.getConfiguration("workername");
 final String value = cloudConfig.get("someProperty", "defaultValue");
```

### Développement d’un worker de proxy personnalisé {#developing-a-customized-proxy-worker}

[Le worker de proxy IDS](indesign.md) est un exemple de worker de proxy [!DNL Assets] qui est déjà fourni prêt à l’emploi pour externaliser le traitement des ressources d’InDesign.

Vous pouvez également développer et configurer votre propre worker de proxy [!DNL Assets] afin de créer un worker spécialisé pour distribuer et externaliser vos tâches de traitement [!DNL Assets].

Pour configurer votre propre worker de proxy personnalisé, vous devez effectuer les opérations suivantes :

* Configurer et mettre en œuvre (à l’aide des événements Sling) :

   * une rubrique de tâche personnalisée ;
   * un gestionnaire d’événements de tâche personnalisé.

* Puis utiliser l’API JobService pour :

   * distribuer votre tâche personnalisée au proxy ;
   * gérer votre tâche.

* Si vous souhaitez utiliser le proxy à partir d’un processus, vous devez mettre en œuvre une étape externe personnalisée à l’aide de l’API WorkflowExternalProcess et de l’API JobService.

Le schéma et les étapes ci-dessous détaillent la procédure à suivre :

![chlimage_1-249](assets/chlimage_1-249.png)

>[!NOTE]
>
>Dans les étapes suivantes, les équivalents InDesigns sont indiqués comme exemples de référence.

1. Une [tâche Sling](https://sling.apache.org/site/eventing-and-jobs.html) est utilisée, ce qui signifie que vous devez définir une rubrique de tâche pour votre cas d’emploi.

   Par exemple, consultez `IDSJob.IDS_EXTENDSCRIPT_JOB` pour le worker de proxy IDS.

1. L’étape externe est utilisée pour déclencher l’événement et attendre qu’il soit terminé en interrogeant l’identifiant. Vous devez développer votre propre étape pour mettre en œuvre de nouvelles fonctionnalités.

   Mettez en œuvre une API `WorkflowExternalProcess`, puis utilisez l’API JobService et votre rubrique de tâche pour préparer un événement de tâche et le distribuer à l’API JobService (un service OSGi).

   Par exemple, consultez `INDDMediaExtractProcess`.java pour le worker de proxy IDS.

1. Mettez en œuvre un gestionnaire de tâches pour votre rubrique. Ce gestionnaire nécessite un développement afin d’effectuer votre action spécifique et est considéré comme la mise en œuvre du worker.

   Par exemple, consultez `IDSJobProcessor.java` pour le worker de proxy IDS.

1. Utilisez `ProxyUtil.java` dans dam-commons. Cela vous permet de distribuer des tâches à des workers à l’aide du proxy de gestion des actifs numériques.

>[!NOTE]
>
>Ce que la structure de proxy [!DNL Assets] ne fournit pas d’usine est le mécanisme de pool.
>
>L&#39;intégration [!DNL InDesign] permet d&#39;accéder à un pool de serveurs [!DNL InDesign] (IDSPool). Ce pool est spécifique à l’intégration [!DNL InDesign] et ne fait pas partie de la structure de proxy [!DNL Assets].

>[!NOTE]
>
>Synchronisation des résultats :
>
>Avec n instances utilisant le même proxy, le résultat de traitement reste avec le proxy. Il incombe au client (auteur Experience Manager) de demander le résultat en utilisant le même identifiant de tâche unique que celui donné au client lors de la création de la tâche. Le proxy fait son travail et conserve le résultat disponible sur demande.
