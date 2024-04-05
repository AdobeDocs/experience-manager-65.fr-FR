---
title: Créer et utiliser des tâches pour le déchargement
description: La fonctionnalité Apache Sling Discovery fournit une API Java qui vous permet de créer des tâches JobManager et des services JobConsumer qui les utilisent.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: 4e6f452d-0251-46f3-ba29-1bd85cda73a6
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 100%

---

# Créer et utiliser des tâches pour le déchargement{#creating-and-consuming-jobs-for-offloading}

La fonctionnalité Apache Sling Discovery fournit une API Java qui vous permet de créer des tâches JobManager et des services JobConsumer qui les utilisent.

Pour plus d’informations sur la création de topologies de déchargement et la configuration de la consommation de rubrique, voir [Tâches de déchargement](/help/sites-deploying/offloading.md).

## Gérer les payloads de la tâche {#handling-job-payloads}

Le cadre de déchargement définit deux propriétés de tâche que vous utilisez pour identifier la payload de la tâche. Les agents de réplication de déchargement utilisent ces propriétés pour identifier les ressources à répliquer sur les instances dans la topologie :

* `offloading.job.input.payload` : liste de chemins d’accès au contenu séparés par des virgules. Le contenu est répliqué sur l’instance qui exécute la tâche.
* `offloading.job.output.payload` : liste de chemins d’accès au contenu séparés par des virgules. Une fois l’exécution de la tâche terminée, le payload est répliqué sur ces chemins d’accès sur l’instance qui a créé la tâche.

Utilisez l’énumération `OffloadingJobProperties` pour faire référence aux noms de propriété :

* `OffloadingJobProperties.INPUT_PAYLOAD.propertyName()`
* `OffloadingJobProperties.OUTPUT_PAYLOAD.propetyName()`

Les tâches ne nécessitent pas de payloads. Toutefois, la payload est nécessaire si la tâche nécessite la manipulation d’une ressource et si elle est déchargée sur un ordinateur qui ne l’a pas créée.

## Créer des tâches pour le déchargement {#creating-jobs-for-offloading}

Créez un client qui appelle la méthode JobManager.addJob pour créer une tâche qu’un JobConsumer sélectionné automatiquement exécute. Indiquez les informations suivantes pour créer la tâche :

* Rubrique : rubrique de tâche.
* Nom : (Facultatif)
* Carte des propriétés : objet `Map<String, Object>` contenant un nombre indéfini de propriétés, telles que les chemins de payload en entrée et en sortie. Cet objet de mappage est disponible pour l’objet JobConsumer qui exécute la tâche.

L’exemple de service suivant crée une tâche pour une rubrique et un chemin de payload d’entrée donnés.

```java
package com.adobe.example.offloading;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;
import org.apache.felix.scr.annotations.Reference;

import java.util.HashMap;

import org.apache.sling.event.jobs.Job;
import org.apache.sling.event.jobs.JobManager;

import org.apache.sling.api.resource.ResourceResolverFactory;
import org.apache.sling.api.resource.ResourceResolver;

import com.adobe.granite.offloading.api.OffloadingJobProperties;

@Component
@Service
public class JobGeneratorImpl implements JobGenerator  {

 @Reference
 private JobManager jobManager;
 @Reference ResourceResolverFactory resolverFactory;

 public String createJob(String topic, String payload) throws Exception {
  Job offloadingJob;

  ResourceResolver resolver = resolverFactory.getResourceResolver(null);
  if(resolver.getResource(payload)!=null){

   HashMap<String, Object> jobprops = new HashMap<String, Object>();
   jobprops.put(OffloadingJobProperties.INPUT_PAYLOAD.propertyName(), payload);

   offloadingJob = jobManager.addJob(topic, null, jobprops);
  } else {
   throw new Exception("Payload for job cannot be found");
  }
  if (offloadingJob == null){
   throw new Exception ("Offloading job could not be created");
  }
  return offloadingJob.getId();
 }
}
```

Le journal contient le message suivant lorsque JobGeneratorImpl.createJob est appelé pour la rubrique `com/adobe/example/offloading` et le payload `/content/geometrixx/de/services` :

```shell
10.06.2013 15:43:33.868 *INFO* [JobHandler: /etc/workflow/instances/2013-06-10/model_1554418768647484:/content/geometrixx/en/company] com.adobe.example.offloading.JobGeneratorImpl Received request to make job for topic com/adobe/example/offloading and payload /content/geometrixx/de/services
```

## Développement d’un consommateur de tâche {#developing-a-job-consumer}

Pour exécuter des tâches, développez un service OSGi qui met en œuvre l’interface `org.apache.sling.event.jobs.consumer.JobConsumer`. Effectuez l’identification avec la rubrique à consommer à l’aide de la propriété `JobConsumer.PROPERTY_TOPICS`.

L’exemple d’implémentation JobConsumer suivant s’enregistre auprès de la rubrique `com/adobe/example/offloading`. Le consommateur définit simplement la propriété Consumed du nœud de contenu de payload sur True.

```java
package com.adobe.example.offloading;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.api.resource.ResourceResolverFactory;
import org.apache.sling.event.jobs.Job;
import org.apache.sling.event.jobs.JobManager;
import org.apache.sling.event.jobs.consumer.JobConsumer;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import javax.jcr.Session;
import javax.jcr.Node;

import com.adobe.granite.offloading.api.OffloadingJobProperties;

@Component
@Service
public class MyJobConsumer implements JobConsumer {

 public static final String TOPIC = "com/adobe/example/offloading";

 @Property(value = TOPIC)
 static final String myTopic = JobConsumer.PROPERTY_TOPICS;

 @Reference
 private ResourceResolverFactory resolverFactory;

 @Reference
 private JobManager jobManager;

 private final Logger log = LoggerFactory.getLogger(getClass());

 public JobResult process(Job job) {
  JobResult result = JobResult.FAILED;
  String topic = job.getTopic();
  log.info("Consuming job of topic: {}", topic);
  String payloadIn =  (String) job.getProperty(OffloadingJobProperties.INPUT_PAYLOAD.propertyName());
  String payloadOut =  (String) job.getProperty(OffloadingJobProperties.OUTPUT_PAYLOAD.propertyName());

  log.info("Job has Input Payload {} and Output Payload {}",payloadIn, payloadOut);

  ResourceResolver resolver = null;
  try {
   resolver = resolverFactory.getAdministrativeResourceResolver(null);
   Session session = resolver.adaptTo(Session.class);
   Node inNode = session.getNode(payloadIn);
   inNode.getNode(Node.JCR_CONTENT).setProperty("consumed",true);
   result = JobResult.OK;
  }catch (Exception e){
   log.info("ERROR -- JOB RESULT IS FAILURE " + e.getMessage());
   result = JobResult.FAILED;
  }
  log.info("Job OK for payload {}",payloadIn);
  return result;
 }
}
```

La classe MyJobConsumer génère les messages de journal suivants pour une payload d’entrée /content/geometrixx/de/services :

```shell
10.06.2013 16:02:40.803 *INFO* [pool-7-thread-17-<main queue>(com/adobe/example/offloading)] com.adobe.example.offloading.MyJobConsumer Consuming job of topic: com/adobe/example/offloading
10.06.2013 16:02:40.803 *INFO* [pool-7-thread-17-<main queue>(com/adobe/example/offloading)] com.adobe.example.offloading.MyJobConsumer Job has Input Payload /content/geometrixx/de/services and Output Payload /content/geometrixx/de/services
10.06.2013 16:02:40.884 *INFO* [pool-7-thread-17-<main queue>(com/adobe/example/offloading)] com.adobe.example.offloading.MyJobConsumer Job OK for payload /content/geometrixx/de/services
```

La propriété Consumed peut être observée à l’aide de CRXDE Lite :

![chlimage_1-25](assets/chlimage_1-25a.png)

## Dépendances Maven {#maven-dependencies}

Ajoutez les définitions de dépendance suivantes à votre fichier pom.xml afin que Maven puisse résoudre les classes liées au déchargement.

```xml
<dependency>
   <groupId>org.apache.sling</groupId>
   <artifactId>org.apache.sling.event</artifactId>
   <version>3.1.5-R1485539</version>
   <scope>provided</scope>
</dependency>
<dependency>
   <groupId>com.adobe.granite</groupId>
   <artifactId>com.adobe.granite.offloading.core</artifactId>
   <version>1.0.4</version>
   <scope>provided</scope>
</dependency>
```

Les exemples précédents nécessitaient également les définitions de dépendance suivantes :

```xml
<dependency>
   <groupId>org.apache.sling</groupId>
   <artifactId>org.apache.sling.api</artifactId>
   <version>2.4.3-R1488084</version>
   <scope>provided</scope>
</dependency>

<dependency>
   <groupId>org.apache.sling</groupId>
   <artifactId>org.apache.sling.jcr.jcr-wrapper</artifactId>
   <version>2.0.0</version>
   <scope>provided</scope>
</dependency>
```
