---
title: « Développement de proxy [!DNL Assets] »
description: Un proxy est une instance  [!DNL Experience Manager]  qui utilise des programmes de travail par proxy pour le traitement des tâches. Découvrez comment configurer un proxy  [!DNL Experience Manager] , les opérations prises en charge et les composants de proxy, ainsi que comment développer un programme de travail par proxy personnalisé.
contentOwner: AG
role: Admin, Architect
exl-id: 42fff236-b4e1-4f42-922c-97da32a933cf
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 83%

---

# Développement de proxy [!DNL Assets] {#assets-proxy-development}

[!DNL Adobe Experience Manager Assets] utilise un proxy pour distribuer le traitement de certaines tâches.

Un proxy est une instance Experience Manager spécifique (et parfois distincte) qui utilise des programmes de travail par de proxy comme des processeurs chargés de gérer une tâche et de produire un résultat. Un programme de travail par proxy peut être utilisé pour de nombreuses tâches. Si une variable [!DNL Assets] proxy qui peut être utilisé pour charger des ressources à des fins de rendu dans Assets. Par exemple, le [programme de travail par proxy IDS](indesign.md) utilise un serveur [!DNL Adobe InDesign] pour traiter les fichiers à utiliser dans Assets.

Lorsque le proxy est une instance distincte d’[!DNL Experience Manager], il contribue à réduire la charge sur la ou les instances de création [!DNL Experience Manager]. Par défaut, [!DNL Assets] exécute les tâches de traitement des ressources dans la même JVM (externalisée via proxy) pour réduire la charge sur l’instance de création [!DNL Experience Manager].

## Proxy (Accès HTTP) {#proxy-http-access}

Un proxy est disponible via le servlet HTTP lorsqu’il est configuré de sorte à accepter les tâches de traitement dans le répertoire suivant :  `/libs/dam/cloud/proxy`. Ce servlet crée une tâche sling à partir des paramètres publiés. Il est ensuite ajouté à la file d’attente des tâches de proxy et connecté au worker de proxy approprié.

### Opérations prises en charge {#supported-operations}

* `job`

  **Exigences** : le paramètre `jobevent` doit être défini en tant que correspondance de valeur en série. Il est utilisé pour créer un `Event` pour un processeur de tâches.

  **Résultat** : ajoute une nouvelle tâche. Si l’opération réussit, un identifiant de tâche unique est renvoyé.

```shell
curl -u admin:admin -F":operation=job" -F"someproperty=xxxxxxxxxxxx"
    -F"jobevent=serialized value map" http://localhost:4502/libs/dam/cloud/proxy
```

* `result`

  **Exigences** : le paramètre `jobid` doit être défini.

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

### Programme de travail par proxy {#proxy-worker}

Un programme de travail par proxy est un processeur chargé de gérer une tâche et de produire un résultat. Ils résident sur l’instance de proxy et doivent mettre en œuvre le [JobProcessor sling](https://sling.apache.org/site/eventing-and-jobs.html) pour être reconnus en tant que programmes de travail de proxy.

>[!NOTE]
>
>Le programme de travail doit implémenter [sling JobProcessor](https://sling.apache.org/site/eventing-and-jobs.html) à être reconnu en tant que worker de proxy.

### API client {#client-api}

[`JobService`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html) est disponible en tant que service OSGi qui prévoit des méthodes pour créer des tâches, supprimer des tâches et obtenir des résultats de ces tâches. La mise en œuvre par défaut de ce service (`JobServiceImpl`) utilise le client HTTP pour communiquer avec le servlet de proxy à distance.

Voici un exemple d’utilisation d’API :

```java
@Reference
 JobService proxyJobService;

 // to create a job
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

### Configuration du service cloud {#cloud-service-configurations}

<!-- TBD: Cannot find com.day.cq.dam.api.proxy at https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html which were generated in May 2020. Hiding this broken link for now.
>[!NOTE]
>
>Reference documentation for the proxy API is available under [`com.day.cq.dam.api.proxy`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/proxy/package-summary.html).
-->

Les configurations de proxy et de programme de travail de proxy sont disponibles via des configurations de services cloud et accessibles à partir de la console **Outils** d’[!DNL Assets], ou sous `/etc/cloudservices/proxy`. Chaque programme de travail de proxy doit ajouter un nœud sous `/etc/cloudservices/proxy` pour les détails de configuration spécifiques au programme de travail (par exemple, `/etc/cloudservices/proxy/workername`).

>[!NOTE]
>
>Pour en savoir plus, consultez les sections [Configuration de programme de travail de proxy d’InDesign Server](indesign.md#configuring-the-proxy-worker-for-indesign-server) et [Configuration du service cloud](../sites-developing/extending-cloud-config.md).

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

### Développement d’un programme de travail de proxy personnalisé {#developing-a-customized-proxy-worker}

Le [programme de travail de proxy IDS](indesign.md) est un exemple de programme de travail de proxy [!DNL Assets] déjà prêt à l’emploi pour externaliser le traitement de ressources InDesign.

Vous pouvez également développer et configurer votre propre programme de travail de proxy [!DNL Assets] pour créer un programme spécialisé afin de distribuer et d’externaliser vos tâches de traitement [!DNL Assets].

Pour configurer votre propre programme de travail de proxy personnalisé, vous devez effectuer les opérations suivantes :

* Configurer et mettre en œuvre (à l’aide des événements Sling) :

   * une rubrique de tâche personnalisée ;
   * un gestionnaire d’événement de tâche personnalisé

* Utilisez ensuite l’API JobService pour :

   * distribuer votre tâche personnalisée au proxy ;
   * gérer votre tâche

* Si vous souhaitez utiliser le proxy d’un workflow, vous devez mettre en oeuvre une étape externe personnalisée à l’aide de l’API WorkflowExternalProcess et de l’API JobService.

Le diagramme et les étapes suivants décrivent la marche à suivre :

![chlimage_1-249](assets/chlimage_1-249.png)

>[!NOTE]
>
>Dans les étapes suivantes, des équivalents InDesign sont indiqués en tant qu’exemples de référence.

1. Une [tâche Sling](https://sling.apache.org/site/eventing-and-jobs.html) est utilisée, ce qui signifie que vous devez définir une rubrique de tâche pour votre cas d’emploi.

   Par exemple, consultez `IDSJob.IDS_EXTENDSCRIPT_JOB` pour le programme de travail de proxy IDS.

1. L’étape externe est utilisée pour déclencher l’événement et attendre qu’il soit terminé en interrogeant l’identifiant. Vous devez développer votre propre étape pour mettre en œuvre de nouvelles fonctionnalités.

   Mettez en œuvre une API `WorkflowExternalProcess`, puis utilisez l’API JobService et votre rubrique de tâche pour préparer un événement de tâche et le distribuer à l’API JobService (un service OSGi).

   Par exemple, consultez `INDDMediaExtractProcess`.java pour le programme de travail de proxy IDS.

1. Mettez en œuvre un gestionnaire de tâches pour votre rubrique. Ce gestionnaire nécessite un développement afin d’effectuer votre action spécifique et est considéré comme la mise en œuvre du programme de travail.

   Par exemple, consultez `IDSJobProcessor.java` pour le programme de travail de proxy IDS.

1. Utilisez `ProxyUtil.java` dans dam-commons. Vous pouvez ainsi distribuer des tâches aux programmes de travail à l’aide du proxy dam.

>[!NOTE]
>
>Le mécanisme de pool n’est pas fourni prêt à l’emploi par le framework de proxy [!DNL Assets].
>
>L’intégration d’[!DNL InDesign] autorise l’accès à un pool de serveurs [!DNL InDesign] (IDSPool). Cette mise en pool est spécifique à l’intégration d’[!DNL InDesign] et ne fait pas partie du framework de proxy d’[!DNL Assets].

>[!NOTE]
>
>Synchronisation des résultats :
>
>Avec n instances utilisant le même proxy, le résultat du traitement reste avec le proxy. Il revient au client (auteur Experience Manager) de demander le résultat à l’aide du même identifiant de tâche unique qui lui a été donné lors de la création de la tâche. Le proxy fait son travail et conserve le résultat disponible sur demande.
