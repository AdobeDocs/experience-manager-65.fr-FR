---
title: Interagir avec les workflows par programmation
seo-title: Interacting with Workflows Programmatically
description: Découvrez comment interagir avec les workflows par programmation dans Adobe Experience Manager.
seo-description: null
uuid: a0f19fc6-b9bd-4b98-9c0e-fbf4f7383026
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: cb621332-a149-4f8d-9425-fd815b033c38
exl-id: 2b396850-e9fb-46d9-9daa-ebd410a9e1a5
source-git-commit: b703f356f9475eeeafb1d5408c650d9c6971a804
workflow-type: tm+mt
source-wordcount: '2011'
ht-degree: 72%

---

# Interagir avec les workflows par programmation{#interacting-with-workflows-programmatically}

When [personnalisation et extension de vos workflows](/help/sites-developing/workflows-customizing-extending.md) vous pouvez accéder aux objets de workflow :

* [Utilisation de l’API Java Workflow](#using-the-workflow-java-api)
* [Obtention d’objets de workflow dans des scripts ECMA](#obtaining-workflow-objects-in-ecma-scripts)
* [Utilisation de l’API REST Workflow](#using-the-workflow-rest-api)

## Utilisation de l’API Java Workflow {#using-the-workflow-java-api}

L’API Java Workflow se compose du package [`com.adobe.granite.workflow`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/package-summary.html) et de plusieurs sous-packages. L’élément le plus important de l’API est la classe `com.adobe.granite.workflow.WorkflowSession`. La classe `WorkflowSession` permet d’accéder aux objets de workflow au moment de la conception et de l’exécution :

* modèles de workflow
* éléments de travail
* instances de workflow
* données de workflow
* éléments de boîte de réception

La classe fournit également plusieurs méthodes pour intervenir dans les cycles de vie des workflows.

Le tableau suivant fournit des liens vers la documentation de référence de plusieurs objets Java clés à utiliser lors de l’interaction par programmation avec des workflows. Les exemples suivants montrent comment obtenir et utiliser les objets de classe dans le code.

| Fonctions | Objets |
|---|---|
| Accès à un workflow | [`WorkflowSession`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/WorkflowSession.html) |
| Exécution et interrogation d’une instance de workflow | [`Workflow`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/Workflow.html)</br>[`WorkItem`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/WorkItem.html)</br>[`WorkflowData`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/WorkflowData.html) |
| Gestion d’un modèle de workflow | [`WorkflowModel`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/model/WorkflowModel.html)</br>[`WorkflowNode`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/model/WorkflowNode.html)</br>[`WorkflowTransition`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/model/WorkflowTransition.html) |
| Informations relatives à un nœud qui se trouve (ou non) dans le workflow | [`WorkflowStatus`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/status/WorkflowStatus.html) |

## Obtention d’objets de workflow dans des scripts ECMA {#obtaining-workflow-objects-in-ecma-scripts}

Comme indiqué dans la section [Recherche du script](/help/sites-developing/the-basics.md#locating-the-script), AEM (via Apache Sling) fournit un moteur de script ECMA qui exécute des scripts ECMA côté serveur. La classe [`org.apache.sling.scripting.core.ScriptHelper`](https://sling.apache.org/apidocs/sling5/org/apache/sling/scripting/core/ScriptHelper.html) est mise immédiatement à la disposition de vos scripts en tant que variable `sling`.

La classe `ScriptHelper` permet d’accéder à l’objet `SlingHttpServletRequest` que vous pouvez utiliser pour obtenir finalement l’objet `WorkflowSession` ; par exemple :

```
var wfsession = sling.getRequest().getResource().getResourceResolver().adaptTo(Packages.com.adobe.granite.workflow.WorkflowSession);
```

## Utilisation de l’API REST Workflow {#using-the-workflow-rest-api}

La console Workflow fait un usage intensif de l’API REST ; cette page décrit donc l’API REST pour les workflows.

>[!NOTE]
>
>L’outil de ligne de commande curl vous permet d’utiliser l’API REST Workflow pour accéder à des objets de workflow et gérer les cycles de vie d’une instance. Les exemples présentés dans cette page illustrent l&#39;utilisation de l&#39;API REST via l&#39;outil de ligne de commande curl.

Les actions suivantes sont prises en charge avec l’API REST :

* démarrage ou arrêt d’un service de workflow
* créer, mettre à jour ou supprimer des modèles de workflow
* [Démarrer, interrompre, reprendre ou mettre fin à des instances de workflow](/help/sites-administering/workflows.md#workflow-status-and-actions)
* terminer ou déléguer des éléments de travail

>[!NOTE]
>
>En utilisant Firebug, une extension Firefox pour le développement web, il est possible de suivre le trafic HTTP lorsque la console est utilisée. Vous pouvez, par exemple, vérifier les paramètres et les valeurs envoyés au serveur AEM avec une requête `POST`.

Dans cette page, on part du principe qu’AEM s’exécute sur localhost sur le port `4502` et que le contexte d’installation est « `/` » (racine). Si ce n’est pas le cas de votre installation, les URI auxquelles les requêtes HTTP s’appliquent doivent être adaptées en conséquence.

Le rendu pris en charge pour les requêtes `GET` est de type JSON. Les URL relatives à `GET` doivent avoir l’extension `.json` ; par exemple :

`http://localhost:4502/etc/workflow.json`

### Gestion des instances de workflow {#managing-workflow-instances}

Les méthodes de requête HTTP suivantes s’appliquent à :

`http://localhost:4502/etc/workflow/instances`

<table>
 <tbody>
  <tr>
   <td>Méthode de requête HTTP</td>
   <td>Actions</td>
  </tr>
  <tr>
   <td><code>GET</code></td>
   <td>Répertorie les instances de workflow disponibles.</td>
  </tr>
  <tr>
   <td><code>POST</code></td>
   <td><p>Crée une instance de workflow. Les paramètres sont les suivants :<br /> - <code>model</code> : l’ID (URI) du modèle de workflow correspondant<br /> - <code>payloadType</code> : contenant le type de payload (par exemple, <code>JCR_PATH</code> ou URL).<br /> Le payload est envoyé en tant que paramètre <code>payload</code>. Une réponse <code>201</code> (<code>CREATED</code>) est renvoyée avec un en-tête d’emplacement contenant l’URL de la nouvelle instance de workflow.</p> </td>
  </tr>
 </tbody>
</table>

#### Gestion d’une instance de workflow par son état {#managing-a-workflow-instance-by-its-state}

Les méthodes de requête HTTP suivantes s’appliquent à :

`http://localhost:4502/etc/workflow/instances.{state}`

| Méthode de requête HTTP | Actions |
|---|---|
| `GET` | Répertorie les instances de workflow disponibles et leur statut (`RUNNING`, `SUSPENDED`, `ABORTED` ou `COMPLETED`). |

#### Gestion d’une instance de workflow par son identifiant {#managing-a-workflow-instance-by-its-id}

Les méthodes de requête HTTP suivantes s’appliquent à :

`http://localhost:4502/etc/workflow/instances/{id}`

<table>
 <tbody>
  <tr>
   <td>Méthode de requête HTTP</td>
   <td>Actions</td>
  </tr>
  <tr>
   <td><code>GET</code></td>
   <td>Récupère les données des instances (définition et métadonnées), y compris le lien vers le modèle de workflow correspondant.</td>
  </tr>
  <tr>
   <td><code>POST</code></td>
   <td>Modifie le statut de l’instance. Le nouveau statut est envoyé en tant que paramètre <code>state</code> et doit avoir l’une des valeurs suivantes : <code>RUNNING</code>, <code>SUSPENDED</code> ou <code>ABORTED</code>.<br /> Si le nouveau statut est inaccessible (par exemple, lors de l’interruption d’une instance terminée), une réponse <code>409</code> (<code>CONFLICT</code>) est renvoyée au client.</td>
  </tr>
 </tbody>
</table>

### Gestion de modèles de workflow {#managing-workflow-models}

Les méthodes de requête HTTP suivantes s’appliquent à :

`http://localhost:4502/etc/workflow/models`

<table>
 <tbody>
  <tr>
   <td>Méthode de requête HTTP</td>
   <td>Actions</td>
  </tr>
  <tr>
   <td><code>GET</code></td>
   <td>Liste des modèles de workflow disponibles.</td>
  </tr>
  <tr>
   <td><code>POST</code></td>
   <td>Crée un modèle de workflow. Si le paramètre <code>title</code> est envoyé, un nouveau modèle est créé avec le titre spécifié. L’association d’un modèle JSON en tant que paramètre <code>model</code> crée un modèle de workflow en fonction de la définition fournie.<br /> Une réponse <code>201</code> (<code>CREATED</code>) est renvoyée avec un en-tête d’emplacement contenant l’URL de la nouvelle ressource de modèle de workflow.<br /> Cela se produit également lorsqu’une définition de modèle est associée en tant que paramètre de fichier appelé <code>modelfile</code>.<br /> Pour les deux paramètres <code>model</code> et <code>modelfile</code>, un paramètre supplémentaire appelé <code>type</code> est nécessaire pour définir le format de sérialisation. De nouveaux formats de sérialisation peuvent être intégrés à l’aide de l’API OSGI. Un sérialiseur JSON standard est fourni avec le moteur de workflow. Son type est JSON. Voir ci-dessous un exemple du format.</td>
  </tr>
 </tbody>
</table>

Exemple : dans le navigateur, une requête adressée à `http://localhost:4502/etc/workflow/models.json` génère une réponse json semblable à ce qui suit :

```
[
    {"uri":"/var/workflow/models/activationmodel"}
    ,{"uri":"/var/workflow/models/dam/adddamsize"}
    ,{"uri":"/var/workflow/models/cloudconfigs/dtm-reactor/library-download"}
    ,{"uri":"/var/workflow/models/ac-newsletter-workflow-simple"}
    ,{"uri":"/var/workflow/models/dam/dam-create-language-copy"}
    ,{"uri":"/var/workflow/models/dam/dam-create-and-translate-language-copy"}
    ,{"uri":"/var/workflow/models/dam-indesign-proxy"}
    ,{"uri":"/var/workflow/models/dam-xmp-writeback"}
    ,{"uri":"/var/workflow/models/dam-parse-word-documents"}
    ,{"uri":"/var/workflow/models/dam/process_subasset"}
    ,{"uri":"/var/workflow/models/dam/dam_set_last_modified"}
    ,{"uri":"/var/workflow/models/dam/dam-autotag-assets"}
    ,{"uri":"/var/workflow/models/dam/update_asset"}
    ,{"uri":"/var/workflow/models/dam/update_asset_offloading"}
    ,{"uri":"/var/workflow/models/dam/dam-update-language-copy"}
    ,{"uri":"/var/workflow/models/dam/update_from_lightbox"}
    ,{"uri":"/var/workflow/models/cloudservices/DTM_bundle_download"}
    ,{"uri":"/var/workflow/models/dam/dam_download_asset"}
    ,{"uri":"/var/workflow/models/dam/dynamic-media-encode-video"}
    ,{"uri":"/var/workflow/models/dam/dynamic-media-video-thumbnail-replacement"}
    ,{"uri":"/var/workflow/models/dam/dynamic-media-video-user-uploaded-thumbnail"}
    ,{"uri":"/var/workflow/models/newsletter_bounce_check"}
    ,{"uri":"/var/workflow/models/projects/photo_shoot_submission"}
    ,{"uri":"/var/workflow/models/projects/product_photo_shoot"}
    ,{"uri":"/var/workflow/models/projects/approval_workflow"}
    ,{"uri":"/var/workflow/models/prototype-01"}
    ,{"uri":"/var/workflow/models/publish_example"}
    ,{"uri":"/var/workflow/models/publish_to_campaign"}
    ,{"uri":"/var/workflow/models/screens/publish_to_author_bin"}
    ,{"uri":"/var/workflow/models/s7dam/request_to_publish_to_youtube"}
    ,{"uri":"/var/workflow/models/projects/request_copy"}
    ,{"uri":"/var/workflow/models/projects/request_email"}
    ,{"uri":"/var/workflow/models/projects/request_landing_page"}
    ,{"uri":"/var/workflow/models/projects/request_launch"}
    ,{"uri":"/var/workflow/models/request_for_activation"}
    ,{"uri":"/var/workflow/models/request_for_deactivation"}
    ,{"uri":"/var/workflow/models/request_for_deletion"}
    ,{"uri":"/var/workflow/models/request_for_deletion_without_deactivation"}
    ,{"uri":"/var/workflow/models/request_to_complete_move_operation"}
    ,{"uri":"/var/workflow/models/reverse_replication"}
    ,{"uri":"/var/workflow/models/salesforce-com-export"}
    ,{"uri":"/var/workflow/models/scene7"}
    ,{"uri":"/var/workflow/models/scheduled_activation"}
    ,{"uri":"/var/workflow/models/scheduled_deactivation"}
    ,{"uri":"/var/workflow/models/screens/screens-update-asset"}
    ,{"uri":"/var/workflow/models/translation"}
    ,{"uri":"/var/workflow/models/s7dam/request_to_remove_from_youtube"}
    ,{"uri":"/var/workflow/models/wcm-translation/create_language_copy"}
    ,{"uri":"/var/workflow/models/wcm-translation/prepare_translation_project"}
    ,{"uri":"/var/workflow/models/wcm-translation/translate-i18n-dictionary"}
    ,{"uri":"/var/workflow/models/wcm-translation/sync_translation_job"}
    ,{"uri":"/var/workflow/models/wcm-translation/translate-language-copy"}
    ,{"uri":"/var/workflow/models/wcm-translation/update_language_copy"}
]
```

#### Gestion d’un modèle de workflow spécifique {#managing-a-specific-workflow-model}

Les méthodes de requête HTTP suivantes s’appliquent à :

`http://localhost:4502*{uri}*`

Où `*{uri}*` est le chemin d’accès au nœud de modèle dans le référentiel.

<table>
 <tbody>
  <tr>
   <td>Méthode de requête HTTP</td>
   <td>Actions</td>
  </tr>
  <tr>
   <td><code>GET</code></td>
   <td>Obtient la version <code>HEAD</code> du modèle (définition et métadonnées).</td>
  </tr>
  <tr>
   <td><code>PUT</code></td>
   <td>Met à jour la version <code>HEAD</code> du modèle (crée une version).<br /> La définition complète de modèle de la nouvelle version du modèle doit être ajoutée sous la forme d’un paramètre appelé <code>model</code>. En outre, un paramètre <code>type</code> est nécessaire, comme lors de la création de modèles, et doit être associé à la valeur <code>JSON</code>.<br /> </td>
  </tr>
  <tr>
   <td><code>POST</code></td>
   <td>Même comportement qu’avec PUT. Cette méthode est nécessaire car les widgets AEM ne prennent pas en charge les opérations <code>PUT</code>.</td>
  </tr>
  <tr>
   <td><code>DELETE</code></td>
   <td>Supprime le modèle. Pour résoudre les problèmes de pare-feu/proxy, un <code>POST</code> qui contient une entrée d’en-tête <code>X-HTTP-Method-Override</code> avec la valeur <code>DELETE</code> sera également accepté en tant que requête <code>DELETE</code>.</td>
  </tr>
 </tbody>
</table>

Exemple : dans le navigateur, une requête adressée à `http://localhost:4502/var/workflow/models/publish_example.json` renvoie une réponse `json` semblable au code suivant :

```shell
{
  "id":"/var/workflow/models/publish_example",
  "title":"Publish Example",
  "version":"1.0",
  "description":"This example shows a simple review and publish process.",
  "metaData":
  {
    "multiResourceSupport":"true",
    "tags":"wcm,publish"
  },
  "nodes":
  [{
    "id":"node0",
    "type":"START",
    "title":"Start",
    "description":"The start node of the workflow.",
    "metaData":
    {
    }
  },
  {
    "id":"node1",
    "type":"PARTICIPANT",
    "title":"Validate Content",
    "description":"Validate the modified content.",
    "metaData":
    {
      "PARTICIPANT":"admin"
    }
  },
  {
    "id":"node2",
    "type":"PROCESS",
    "title":"Publish Content",
    "description":"Publish the modified content.",
    "metaData":
    {
      "PROCESS_AUTO_ADVANCE":"true",
      "PROCESS":"com.day.cq.wcm.workflow.process.ActivatePageProcess"
    }
  },
  {
    "id":"node3",
    "type":"END",
    "title":"End",
    "description":"The end node of the workflow.",
    "metaData":
    {
    }
  }],
  "transitions":
  [{
    "from":"node0",
    "to":"node1",
    "metaData":
    {
    }
  },
  {
    "from":"node1",
    "to":"node2",
    "metaData":
    {
    }
  },
  {
    "from":"node2",
    "to":"node3",
    "metaData":
    {
    }
  }
]}
```

#### Gestion d’un modèle de workflow en fonction de sa version {#managing-a-workflow-model-by-its-version}

Les méthodes de requête HTTP suivantes s’appliquent à :

`http://localhost:4502/etc/workflow/models/{id}.{version}`

| Méthode de requête HTTP | Actions |
|---|---|
| `GET` | Obtient les données du modèle dans la version donnée (le cas échéant). |

### Gestion de boîtes de réception (utilisateur) {#managing-user-inboxes}

Les méthodes de requête HTTP suivantes s’appliquent à :

`http://localhost:4502/bin/workflow/inbox`

<table>
 <tbody>
  <tr>
   <td>Méthode de requête HTTP</td>
   <td>Actions</td>
  </tr>
  <tr>
   <td><code>GET</code></td>
   <td>Répertorie les tâches qui se trouvent dans la boîte de réception de l’utilisateur, qui est identifié par les en-têtes d’authentification HTTP.</td>
  </tr>
  <tr>
   <td><code>POST</code></td>
   <td>Termine l’élément de travail dont l’URI est envoyé en tant que paramètre <code>item</code> et transmet l’instance de workflow correspondante aux nœuds suivants, en fonction de ce qui est défini par le paramètre <code>route</code> ou <code>backroute</code>, en cas de rétroaction.<br /> Si le paramètre <code>delegatee</code> est envoyé, l’élément de travail identifié par le paramètre <code>item</code> est délégué au participant spécifié.</td>
  </tr>
 </tbody>
</table>

#### Gestion d’une boîte de réception (utilisateur) par l’identifiant de l’élément de travail {#managing-a-user-inbox-by-the-workitem-id}

Les méthodes de requête HTTP suivantes s’appliquent à :

`http://localhost:4502/bin/workflow/inbox/{id}`

| Méthode de requête HTTP | Actions |
|---|---|
| `GET` | Obtient les données (définition et métadonnées) du `WorkItem` de la boîte de réception identifié par son ID. |

## Exemples {#examples}

### Comment obtenir une liste de tous les workflows en cours d’exécution avec leurs ID {#how-to-get-a-list-of-all-running-workflows-with-their-ids}

Pour obtenir la liste de tous les workflows en cours d’exécution, effectuez une GET pour :

`http://localhost:4502/etc/workflow/instances.RUNNING.json`

#### Comment obtenir une liste de tous les workflows en cours d’exécution avec leurs identifiants - REST à l’aide de curl {#how-to-get-a-list-of-all-running-workflows-with-their-ids-rest-using-curl}

Exemple avec curl :

```shell
curl -u admin:admin http://localhost:4502/etc/workflow/instances.RUNNING.json
```

L’`uri` affichée dans les résultats peut être utilisée comme `id` d’instance dans d’autres commandes. Par exemple :

```shell
[
    {"uri":"/etc/workflow/instances/server0/2017-03-08/request_for_activation_1"}
]
```

>[!NOTE]
>
>Cette commande `curl` peut être utilisée avec n’importe quel [statut de workflow](/help/sites-administering/workflows.md#workflow-status-and-actions) à la place de `RUNNING`.

### Comment modifier le titre du workflow {#how-to-change-the-workflow-title}

Pour modifier le **Titre du workflow** affiché dans l’onglet **Instances** de la console Workflow, envoyez une commande `POST` :

* vers : `http://localhost:4502/etc/workflow/instances/{id}`

* avec les paramètres suivants :

   * `action` : sa valeur doit être `UPDATE`.
   * `workflowTitle` : titre du workflow

#### Comment modifier le titre du workflow - REST à l’aide de curl {#how-to-change-the-workflow-title-rest-using-curl}

Exemple avec curl :

```shell
curl -u admin:admin -d "action=UPDATE&workflowTitle=myWorkflowTitle" http://localhost:4502/etc/workflow/instances/{id}

# for example
curl -u admin:admin -d "action=UPDATE&workflowTitle=myWorkflowTitle" http://localhost:4502/etc/workflow/instances/server0/2017-03-08/request_for_activation_1
```

### Comment répertorier tous les modèles de processus {#how-to-list-all-workflow-models}

Pour obtenir la liste de tous les modèles de workflow disponibles, effectuez une GET pour :

`http://localhost:4502/etc/workflow/models.json`

#### Comment répertorier tous les modèles de processus - REST à l’aide de curl {#how-to-list-all-workflow-models-rest-using-curl}

Exemple avec curl :

```shell
curl -u admin:admin http://localhost:4502/etc/workflow/models.json
```

>[!NOTE]
>
>Consultez également la section [Gestion de modèles de workflow](#managing-workflow-models).

### Obtention d’un objet WorkflowSession {#obtaining-a-workflowsession-object}

La classe `com.adobe.granite.workflow.WorkflowSession` peut être adaptée à partir d’un objet `javax.jcr.Session` ou `org.apache.sling.api.resource.ResourceResolver`.

#### Obtention d’un objet WorkflowSession – Java {#obtaining-a-workflowsession-object-java}

Dans un script JSP (ou un code Java pour une classe servlet), utilisez l’objet de requête HTTP pour obtenir un objet `SlingHttpServletRequest` qui permet d’accéder à un objet `ResourceResolver`. Adaptez l’objet `ResourceResolver` en `WorkflowSession`.

```java
<%
%><%@include file="/libs/foundation/global.jsp"%><%
%><%@page session="false"
    import="com.adobe.granite.workflow.WorkflowSession,
  org.apache.sling.api.SlingHttpServletRequest"%><%

SlingHttpServletRequest slingReq = (SlingHttpServletRequest)request;
WorkflowSession wfSession = slingReq.getResourceResolver().adaptTo(WorkflowSession.class);
%>
```

#### Obtention d’un objet WorkflowSession – Script ECMA {#obtaining-a-workflowsession-object-ecma-script}

Utilisez la variable `sling` pour récupérer l’objet `SlingHttpServletRequest` que vous utilisez pour obtenir un objet `ResourceResolver`. Adaptez l’objet `ResourceResolver` en objet `WorkflowSession`.

```
var wfsession = sling.getRequest().getResource().getResourceResolver().adaptTo(Packages.com.adobe.granite.workflow.WorkflowSession);
```

### Création, lecture ou suppression de modèles de processus {#creating-reading-or-deleting-workflow-models}

Les exemples suivants montrent comment accéder aux modèles de workflow :

* Le code pour les scripts Java et ECMA utilise la méthode `WorkflowSession.createNewModel`.
* La commande curl accède directement au modèle à l’aide de son URL.

Exemples utilisés :

1. créent un modèle (avec l’ID `/var/workflow/models/mymodel/jcr:content/model`) ;
1. suppriment le modèle.

>[!NOTE]
>
>La suppression du modèle définit la propriété `deleted` du nœud enfant `metaData` du modèle sur `true`.
>
>La suppression ne supprime pas le noeud de modèle.

Lors de la création d’un modèle :

* L’éditeur de modèle de workflow exige que les modèles utilisent une structure de nœud spécifique sous `/var/workflow/models`. Le nœud parent du modèle doit être de type `cq:Page` avec un nœud `jcr:content` présentant les valeurs de propriété suivantes :

   * `sling:resourceType`: `cq/workflow/components/pages/model`
   * `cq:template`: `/libs/cq/workflow/templates/model`

  Lorsque vous créez un modèle, vous devez d’abord créer ce nœud `cq:Page` et utiliser son nœud `jcr:content` comme parent du nœud de modèle.

* L’argument `id` requis par certaines méthodes pour identifier le modèle est le chemin d’accès absolu du modèle de nœud dans le référentiel :

  `/var/workflow/models/<*model_name>*/jcr:content/model`

  >[!NOTE]
  >
  >Consultez la section [Comment répertorier tous les modèles de workflow](#how-to-list-all-workflow-models).

#### Création, lecture ou suppression de modèles de workflow - Java {#creating-reading-or-deleting-workflow-models-java}

```java
<%@include file="/libs/foundation/global.jsp"%><%
%><%@page session="false" import="com.adobe.granite.workflow.WorkflowSession,
                 com.adobe.granite.workflow.model.WorkflowModel,
             org.apache.sling.api.SlingHttpServletRequest"%><%

SlingHttpServletRequest slingReq = (SlingHttpServletRequest)request;
WorkflowSession wfSession = slingReq.getResourceResolver().adaptTo(WorkflowSession.class);
/* Create the parent page */
String modelRepo = new String("/var/workflow/models");
String modelTemplate = new String ("/libs/cq/workflow/templates/model");
String modelName = new String("mymodel");
Page modelParent = pageManager.create(modelRepo, modelName, modelTemplate, "My workflow model");

/* create the model */
String modelId = new String(modelParent.getPath()+"/jcr:content/model")
WorkflowModel model = wfSession.createNewModel("Made using Java",modelId);

/* delete the model */
wfSession.deleteModel(modelId);
%>
```

#### Création, lecture ou suppression de modèles de processus - Script ECMA {#creating-reading-or-deleting-workflow-models-ecma-script}

```
var resolver = sling.getRequest().getResource().getResourceResolver();
var wfSession = resolver.adaptTo(Packages.com.adobe.granite.workflow.WorkflowSession);
var pageManager = resolver.adaptTo(Packages.com.day.cq.wcm.api.PageManager);

//create the parent page node
var workflowPage = pageManager.create("/var/workflow/models", "mymodel", "/libs/cq/workflow/templates/model", "Created via ECMA Script");
var modelId = workflowPage.getPath()+ "/jcr:content/model";
//create the model
var model = wfSession.createNewModel("My Model", modelId);
//delete the model
var model = wfSession.deleteModel(modelId);
```

#### Suppression d’un modèle de workflow - REST à l’aide de curl {#deleting-a-workflow-model-rest-using-curl}

```shell
# deleting the model by its id
curl -u admin:admin -X DELETE http://localhost:4502/etc/workflow/models/{id}
```

>[!NOTE]
>
>En raison du niveau de détail requis, curl n’est pas considéré comme pratique pour créer et/ou lire un modèle.

### Filtrage des workflows système lors de la vérification de l’état du workflow {#filtering-out-system-workflows-when-checking-workflow-status}

Vous pouvez utiliser l’[API WorkflowStatus](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/status/WorkflowStatus.html) pour récupérer des informations sur le statut des workflows d’un nœud.

Plusieurs méthodes sont associées au paramètre :

`excludeSystemWorkflows`

Ce paramètre peut être défini sur `true` pour indiquer que les workflows système doivent être exclus des résultats.

Vous [pouvez mettre à jour la configuration OSGi](/help/sites-deploying/configuring-osgi.md) **Adobe Granite Workflow PayloadMapCache** qui spécifie les `Models`modèles de workflow à prendre en compte en tant que workflows système. Les modèles de workflow (d’exécution) par défaut sont les suivants :

* `/var/workflow/models/scheduled_activation/jcr:content/model`
* `/var/workflow/models/scheduled_deactivation/jcr:content/model`

### Avance automatique de l’étape de participant après un dépassement de délai {#auto-advance-participant-step-after-a-timeout}

Si vous devez avancer automatiquement une **Participant** étape qui n’a pas été effectuée dans un délai prédéfini, vous pouvez :

1. Implémentez un écouteur d’événement OSGI pour écouter la création et la modification de tâches.
1. Spécifiez un délai d’expiration (échéance), puis créez une tâche sling planifiée à déclencher à ce moment-là.
1. Créez un gestionnaire de tâches qui est averti lors du dépassement du délai et qui déclenche la tâche.

    Ce gestionnaire exécutera l’action requise sur la tâche si cette dernière n’est pas encore terminée.

>[!NOTE]
>
>Les mesures à prendre doivent être clairement définies pour pouvoir utiliser cette approche.

### Interaction avec des instances de workflow {#interacting-with-workflow-instances}

Vous trouverez ci-dessous des exemples de base sur la façon d’interagir (par programmation) avec des instances de workflow.

#### Interaction avec des instances de workflow – Java {#interacting-with-workflow-instances-java}

```java
// starting a workflow
WorkflowModel model = wfSession.getModel(workflowId);
WorkflowData wfData = wfSession.newWorkflowData("JCR_PATH", repoPath);
wfSession.startWorkflow(model, wfData);

// querying and managing a workflow
Workflow[] workflows workflows = wfSession.getAllWorkflows();
Workflow workflow= wfSession.getWorkflow(id);
wfSession.suspendWorkflow(workflow);
wfSession.resumeWorkflow(workflow);
wfSession.terminateWorkflow(workflow);
```

#### Interaction avec des instances de workflow – Script ECMA {#interacting-with-workflow-instances-ecma-script}

```
// starting a workflow
var model = wfSession.getModel(workflowId);
var wfData = wfSession.newWorkflowData("JCR_PATH", repoPath);
wfSession.startWorkflow(model, wfData);

// querying and managing a workflow
var workflows = wfSession.getWorkflows("RUNNING");
var workflow= wfSession.getWorkflow(id);
wfSession.suspendWorkflow(workflow);
wfSession.resumeWorkflow(workflow);
wfSession.terminateWorkflow(workflow);
```

#### Interaction avec des instances de workflow – REST avec curl {#interacting-with-workflow-instances-rest-using-curl}

* **Démarrage d’un workflow**

  ```shell
  # starting a workflow
  curl -d "model={id}&payloadType={type}&payload={payload}" http://localhost:4502/etc/workflow/instances
  
  # for example:
  curl -u admin:admin -d "model=/var/workflow/models/request_for_activation&payloadType=JCR_PATH&payload=/content/we-retail/us/en/products" http://localhost:4502/etc/workflow/instances
  ```

* **Liste des instances**

  ```shell
  # listing the instances
  curl -u admin:admin http://localhost:4502/etc/workflow/instances.json
  ```

  Toutes les instances seront répertoriées, par exemple :

  ```shell
  [
      {"uri":"/var/workflow/instances/server0/2018-02-26/prototype-01_1"}
      ,{"uri":"/var/workflow/instances/server0/2018-02-26/prototype-01_2"}
  ]
  ```

  >[!NOTE]
  >
  >Consultez la section [Comment obtenir la liste de tous les workflow actifs](#how-to-get-a-list-of-all-running-workflows-with-their-ids) avec leurs ID pour répertorier les instances qui présentent un statut spécifique.

* **Suspension d&#39;un workflow**

  ```shell
  # suspending a workflow
  curl -d "state=SUSPENDED" http://localhost:4502/etc/workflow/instances/{id}
  
  # for example:
  curl -u admin:admin -d "state=SUSPENDED" http://localhost:4502/etc/workflow/instances/server0/2017-03-08/request_for_activation_1
  ```

* **Reprise d’un workflow**

  ```shell
  # resuming a workflow
  curl -d "state=RUNNING" http://localhost:4502/etc/workflow/instances/{id}
  
  # for example:
  curl -u admin:admin -d "state=RUNNING" http://localhost:4502/etc/workflow/instances/server0/2017-03-08/request_for_activation_1
  ```

* **Arrêt d’une instance de workflow**

  ```shell
  # terminating a workflow
  curl -d "state=ABORTED" http://localhost:4502/etc/workflow/instances/{id}
  
  # for example:
  curl -u admin:admin -d "state=ABORTED" http://localhost:4502/etc/workflow/instances/server0/2017-03-08/request_for_activation_1
  ```

### Interaction avec des éléments de travail {#interacting-with-work-items}

Vous trouverez ci-dessous des exemples de base sur la manière d’interagir (par programmation) avec des tâches.

#### Interaction avec les éléments de travail - Java {#interacting-with-work-items-java}

```java
// querying work items
WorkItem[] workItems = wfSession.getActiveWorkItems();
WorkItem workItem = wfSession.getWorkItem(id);

// getting routes
List<Route> routes = wfSession.getRoutes(workItem);

// delegating
Iterator<Participant> delegatees = wfSession.getDelegatees(workItem);
wfSession.delegateWorkItem(workItem, delegatees.get(0));

// completing or advancing to the next step
wfSession.complete(workItem, routes.get(0));
```

#### Interaction avec des éléments de travail - Script ECMA {#interacting-with-work-items-ecma-script}

```
// querying work items
var workItems = wfSession.getActiveWorkItems();
var workItem = wfSession.getWorkItem(id);

// getting routes
var routes = wfSession.getRoutes(workItem);

// delegating
var delegatees = wfSession.getDelegatees(workItem);
wfSession.delegateWorkItem(workItem, delegatees.get(0));

// completing or advancing to the next step
wfSession.complete(workItem, routes.get(0));
```

#### Interaction avec des éléments de travail - REST à l’aide de curl {#interacting-with-work-items-rest-using-curl}

* **Liste des éléments de travail de la boîte de réception**

  ```shell
  # listing the work items
  curl -u admin:admin http://localhost:4502/bin/workflow/inbox
  ```

  Les détails des tâches actuellement présentes dans la boîte de réception sont répertoriés, par exemple :

  ```shell
  [{
      "uri_xss": "/var/workflow/instances/server0/2018-02-26/prototype-01_2/workItems/node2_var_workflow_instances_server0_2018-02-26_prototype-01_2",
      "uri": "/var/workflow/instances/server0/2018-02-26/prototype-01_2/workItems/node2_var_workflow_instances_server0_2018-02-26_prototype-01_2",
      "currentAssignee_xss": "workflow-administrators",
      "currentAssignee": "workflow-administrators",
      "startTime": 1519656289274,
      "payloadType_xss": "JCR_PATH",
      "payloadType": "JCR_PATH",
      "payload_xss": "/content/we-retail/es/es",
      "payload": "/content/we-retail/es/es",
      "comment_xss": "Process resource is null",
      "comment": "Process resource is null",
      "type_xss": "WorkItem",
      "type": "WorkItem"
    },{
      "uri_xss": "configuration/configure_analyticstargeting",
      "uri": "configuration/configure_analyticstargeting",
      "currentAssignee_xss": "administrators",
      "currentAssignee": "administrators",
      "type_xss": "Task",
      "type": "Task"
    },{
      "uri_xss": "configuration/securitychecklist",
      "uri": "configuration/securitychecklist",
      "currentAssignee_xss": "administrators",
      "currentAssignee": "administrators",
      "type_xss": "Task",
      "type": "Task"
    },{
      "uri_xss": "configuration/enable_collectionofanonymoususagedata",
      "uri": "configuration/enable_collectionofanonymoususagedata",
      "currentAssignee_xss": "administrators",
      "currentAssignee": "administrators",
      "type_xss": "Task",
      "type": "Task"
    },{
      "uri_xss": "configuration/configuressl",
      "uri": "configuration/configuressl",
      "currentAssignee_xss": "administrators",
      "currentAssignee": "administrators",
      "type_xss": "Task",
      "type": "Task"
    }
  ```

* **Délégation d’éléments de travail**

  ```xml
  # delegating
  curl -d "item={item}&delegatee={delegatee}" http://localhost:4502/bin/workflow/inbox
  
  # for example:
  curl -u admin:admin -d "item=/etc/workflow/instances/server0/2017-03-08/request_for_activation_1/workItems/node1_etc_workflow_instances_server0_2017-03-08_request_for_act_1&delegatee=administrators" http://localhost:4502/bin/workflow/inbox
  ```

  >[!NOTE]
  >
  >Le `delegatee` doit être une option valide pour l’étape de workflow.

* **Réalisation ou progression d’éléments de travail à l’étape suivante**

  ```xml
  # retrieve the list of routes; the results will be similar to {"results":1,"routes":[{"rid":"233123169","label":"End","label_xss":"End"}]}
  http://localhost:4502/etc/workflow/instances/<path-to-the-workitem>.routes.json
  
  # completing or advancing to the next step; use the appropriate route ID (rid value) from the above list
  curl -d "item={item}&route={route}" http://localhost:4502/bin/workflow/inbox
  
  # for example:
  curl -u admin:admin -d "item=/etc/workflow/instances/server0/2017-03-08/request_for_activation_1/workItems/node1_etc_workflow_instances_server0_2017-03-08_request_for_activation_1&route=233123169" http://localhost:4502/bin/workflow/inbox
  ```

### Écoute des événements de workflow {#listening-for-workflow-events}

Utilisez le framework d’événement OSGi pour écouter les événements définis par la classe [`com.adobe.granite.workflow.event.WorkflowEvent`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/event/WorkflowEvent.html). Cette classe propose également plusieurs méthodes utiles pour obtenir des informations sur le sujet de l’événement. La méthode `getWorkItem`, par exemple, renvoie l’objet `WorkItem` de l’élément de travail qui est impliqué dans l’événement.

L’exemple de code suivant définit un service qui écoute les événements de workflow et exécute les tâches selon le type d’événement.

```java
package com.adobe.example.workflow.listeners;

import org.apache.sling.event.jobs.JobProcessor;
import org.apache.sling.event.jobs.JobUtil;

import org.osgi.service.event.Event;
import org.osgi.service.event.EventHandler;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Service;

import com.adobe.granite.workflow.event.WorkflowEvent;
import com.adobe.granite.workflow.exec.WorkItem;

/**
 * The <code>WorkflowEventCatcher</code> class listens to workflow events.
 */
@Component(metatype=false, immediate=true)
@Service(value=org.osgi.service.event.EventHandler.class)
public class WorkflowEventCatcher implements EventHandler, JobProcessor {

 @Property(value=com.adobe.granite.workflow.event.WorkflowEvent.EVENT_TOPIC)
 static final String EVENT_TOPICS = "event.topics";

 private static final Logger logger = LoggerFactory.getLogger(WorkflowEventCatcher.class);

 public void handleEvent(Event event) {
  JobUtil.processJob(event, this);
 }

 public boolean process(Event event) {
  logger.info("Received event of topic: " + event.getTopic());
  String topic = event.getTopic();

  try {
   if (topic.equals(WorkflowEvent.EVENT_TOPIC)) {
    WorkflowEvent wfevent = (WorkflowEvent)event;
    String eventType = wfevent.getEventType();
    String instanceId = wfevent.getWorkflowInstanceId();

    if (instanceId != null) {
     //workflow instance events
     if (eventType.equals(WorkflowEvent.WORKFLOW_STARTED_EVENT) ||
       eventType.equals(WorkflowEvent.WORKFLOW_RESUMED_EVENT) ||
       eventType.equals(WorkflowEvent.WORKFLOW_SUSPENDED_EVENT)) {
      // your code comes here...
     } else if (
       eventType.equals(WorkflowEvent.WORKFLOW_ABORTED_EVENT) ||
       eventType.equals(WorkflowEvent.WORKFLOW_COMPLETED_EVENT)) {
      // your code comes here...
     }
     // workflow node event
     if (eventType.equals(WorkflowEvent.NODE_TRANSITION_EVENT)) {
      WorkItem currentItem = (WorkItem) event.getProperty(WorkflowEvent.WORK_ITEM);
      // your code comes here...
     }
    }
   }
  } catch(Exception e){
   logger.debug(e.getMessage());
   e.printStackTrace();
  }
  return true;
 }
}
```
