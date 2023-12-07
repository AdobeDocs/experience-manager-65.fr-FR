---
title: Extension des fonctionnalités de workflows
description: Découvrez comment étendre la fonctionnalité du workflow de Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 9e205912-50a6-414a-b8d4-a0865269d0e0
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '3499'
ht-degree: 67%

---

# Extension des fonctionnalités de workflows{#extending-workflow-functionality}

Cette rubrique décrit le développement de composants d’étape personnalisés pour vos workflows, puis comment interagir par programmation avec les workflows.

La création d’une étape de workflow personnalisée implique les activités suivantes :

* Développez le composant d’étape de workflow.
* Mettez en oeuvre la fonctionnalité d’étape en tant que service OSGi ou script ECMA.

Vous pouvez également [interagir avec les workflows de vos programmes et scripts](/help/sites-developing/workflows-program-interaction.md).

## Composants d’étape de workflow - Principes de base {#workflow-step-components-the-basics}

Un composant d’étape de workflow définit l’aspect et le comportement de l’étape lors de la création de modèles de workflow :

* Nom de catégorie et d’étape dans le sidekick du processus.
* Apparence de l’étape dans les modèles de workflow.
* Boîte de dialogue de modification pour la configuration des propriétés du composant.
* Service ou script exécuté au moment de l’exécution.

Comme avec [tous les composants](/help/sites-developing/components.md), les composants de l’étape de processus héritent du composant spécifié pour la variable `sling:resourceSuperType` . Le diagramme suivant présente la hiérarchie des nœuds `cq:component` qui constituent la base de tous les composants des étapes de workflow. Le diagramme inclut également les composants **Étape du processus**, **Étape du participant** et **Étape du participant dynamique**, car il s’agit des points de départ les plus courants (et les plus simples) pour développer des composants d’étape personnalisée.

![aem_wf_componentinherit](assets/aem_wf_componentinherit.png)

>[!CAUTION]
>
>Vous ne devez ***rien*** modifier dans le chemin `/libs`.
>
>En effet, le contenu de `/libs` est remplacé dès que vous mettez à niveau votre instance (et risque de l’être si vous appliquez un correctif ou un Feature Pack).
>
>La méthode recommandée pour la configuration et d’autres modifications est la suivante :
>
>1. Recréez l’élément requis (c’est-à-dire, tel qu’il existe dans `/libs` under `/apps`
>2. Apportez les modifications désirées dans `/apps`.

Le composant `/libs/cq/workflow/components/model/step` est l’ancêtre commun le plus proche de l’**Étape du processus**, l’**Étape du participant** et l’**Étape du participant dynamique**, qui héritent tous des éléments suivants :

* `step.jsp`

  Le script `step.jsp` affiche le titre du composant d’étape lorsqu’il est ajouté à un modèle.

  ![wf-22-1](assets/wf-22-1.png)

* [cq:dialog](/help/sites-developing/developing-components.md#creating-and-configuring-a-dialog)

  Une boîte de dialogue avec les onglets suivants :

   * **Courant**: pour modifier le titre et la description.
   * **Avancé**: pour modifier les propriétés des notifications électroniques.

  ![wf-44](assets/wf-44.png) ![wf-45](assets/wf-45.png)

  >[!NOTE]
  >
  >Lorsque les onglets de la boîte de dialogue de modification d’un composant d’étape ne correspondent pas à cette apparence par défaut, le composant d’étape a défini des scripts, des propriétés de noeud ou des onglets de boîte de dialogue qui remplacent ces onglets hérités.

### Scripts ECMA {#ecma-scripts}

Les objets suivants sont disponibles (en fonction du type d’étape) dans les scripts ECMA :

* [WorkItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/exec/WorkItem.html) workItem
* [WorkflowSession](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/WorkflowSession.html) workflowSession
* [WorkflowData](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/exec/WorkflowData.html) workflowData
* `args` : tableau contenant les arguments du processus.

* `sling` : pour accéder à d’autres services osgi.
* `jcrSession`

### MetaDataMaps {#metadatamaps}

Vous pouvez utiliser les métadonnées de processus pour conserver les informations requises pendant la durée de vie du processus. Les étapes d’un workflow sont généralement nécessaires pour conserver les données en vue d’une utilisation ultérieure dans le workflow ou pour récupérer les données persistantes.

Il existe trois types d’objets MetaDataMap pour les objets `Workflow`, `WorkflowData` et `WorkItem`. Ils ont tous la même fonction : stocker les métadonnées.

Un élément de travail possède sa propre carte MetaData qui ne peut être utilisée que pendant l’exécution de cet élément de travail (par exemple, l’étape).

Les objets MetaDataMap `Workflow` et `WorkflowData` sont partagés sur l’ensemble du workflow. Pour ces cas, il est recommandé d’utiliser uniquement l’objet MetaDataMap `WorkflowData`.

## Création de composants d’étape de processus personnalisés {#creating-custom-workflow-step-components}

Les composants d’étape de workflow peuvent être [créé de la même manière que tout autre composant](/help/sites-developing/components.md).

Pour hériter de l’un des composants de l’étape de base (existante), ajoutez la propriété suivante au nœud `cq:Component` :

* Nom : `sling:resourceSuperType`
* Type : `String`
* Valeur : l’un des chemins suivants qui se résout en un composant de base :

   * `cq/workflow/components/model/process`
   * `cq/workflow/components/model/participant`
   * `cq/workflow/components/model/dynamic_participant`

### Spécification du titre et de la description par défaut pour les instances d’étape {#specifying-the-default-title-and-description-for-step-instances}

Procédez comme suit pour spécifier les valeurs par défaut de la variable **Titre** et **Description** dans le champ **Courant** .

>[!NOTE]
>
>Les valeurs de champ s’affichent sur l’instance d’étape lorsque les deux exigences suivantes sont satisfaites :
>
>* La boîte de dialogue de modification de l’étape stocke le titre et la description aux emplacements suivants : >
>* `./jcr:title`
>* Emplacements `./jcr:description`
>
>  Cette exigence est satisfaite lorsque la boîte de dialogue de modification utilise l’onglet Commun que le composant `/libs/cq/flow/components/step/step` implémente.
>
>* Le composant d’étape ou un ancêtre du composant ne remplace pas le script `step.jsp` que le composant `/libs/cq/flow/components/step/step` implémente.

1. Sous le nœud `cq:Component`, ajoutez le nœud suivant :

   * Nom : `cq:editConfig`
   * Type : `cq:EditConfig`

   >[!NOTE]
   >
   >Pour plus d’informations sur le nœud cq:editConfig, consultez [Configuration du comportement de modification d’un composant](/help/sites-developing/developing-components.md#configuring-the-edit-behavior).

1. Sous le nœud `cq:EditConfig`, ajoutez le nœud suivant :

   * Nom : `cq:formParameters`
   * Type : `nt:unstructured`

1. Ajoutez les propriétés `String` des noms suivants au nœud `cq:formParameters` :

   * `jcr:title` : la valeur remplit le champ **Titre** de l’onglet **Commun**.
   * `jcr:description` : la valeur remplit le champ **Description** de l’onglet **Commun**.

### Enregistrement des valeurs de propriété dans les métadonnées de workflow {#saving-property-values-in-workflow-metadata}

>[!NOTE]
>
>Voir [Persistance et accès aux données](#persisting-and-accessing-data). En particulier, pour plus d’informations sur l’accès à la valeur de propriété au moment de l’exécution, voir [Accès aux valeurs des propriétés de boîte de dialogue au moment de l’exécution](#accessing-dialog-property-values-at-runtime).

La propriété de nom des éléments `cq:Widget` spécifie le nœud JCR qui stocke la valeur du widget. Lorsque des widgets dans la boîte de dialogue de composant de l’étape du workflow stockent des valeurs sous la balise `./metaData`, la valeur est ajoutée au workflow `MetaDataMap`.

Par exemple, un champ de texte dans une boîte de dialogue est un nœud `cq:Widget` qui possède les propriétés suivantes :

| Nom | Type | Valeur |
|---|---|---|
| `xtype` | `String` | `textarea` |
| `name` | `String` | `./metaData/subject` |
| `fieldLabel` | `String` | `Email Subject` |

La valeur spécifiée dans ce champ de texte est ajoutée à l’objet ` [MetaDataMap](#metadatamaps)` de l’instance de workflow et est associée à la clé `subject`.

>[!NOTE]
>
>Lorsque la clé est `PROCESS_ARGS`, la valeur est immédiatement disponible dans les implémentations de script ECMA via la variable `args`. Dans ce cas, la valeur de la propriété name est `./metaData/PROCESS_ARGS.`

### Remplacement de la mise en œuvre de l’étape {#overriding-the-step-implementation}

Chaque composant d’étape de base permet à l’équipe de développement des modèles de workflow de configurer les fonctionnalités clés suivantes lors de la conception :

* Étape du processus : service ou script ECMA à exécuter au moment de l’exécution.
* Participant : ID de l’utilisateur auquel est affecté l’élément de travail généré.
* Étape choix dynamique de participant : le service ou le script ECMA qui sélectionne l’identifiant de l’utilisateur auquel est affecté l’élément de travail.

Pour cibler le composant en vue de l’utiliser dans un scénario de workflow spécifique, configurez la fonction clé dans la conception et supprimez la possibilité pour les développeurs de modèles de la modifier.

1. Sous le noeud cq:component , ajoutez le noeud suivant :

   * Nom : `cq:editConfig`
   * Type : `cq:EditConfig`

   Pour plus d’informations sur le noeud cq:editConfig , voir [Configuration du comportement de modification d’un composant](/help/sites-developing/developing-components.md#configuring-the-edit-behavior).

1. Sous le nœud cq:EditConfig, ajoutez le nœud suivant :

   * Nom : `cq:formParameters`
   * Type : `nt:unstructured`

1. Ajoutez une propriété `String` au nœud `cq:formParameters`. Le supertype de composant détermine le nom de la propriété :

   * Étape du processus : `PROCESS`
   * Étape du participant : `PARTICIPANT`
   * Étape de participant dynamique : `DYNAMIC_PARTICIPANT`

1. Définissez la valeur de la propriété :

   * `PROCESS` : chemin d’accès au script ECMA ou au PID du service qui implémente le comportement de l’étape.
   * `PARTICIPANT` : ID de l’utilisateur à qui l’élément de travail a été affecté.
   * `DYNAMIC_PARTICIPANT` : chemin d’accès au script ECMA ou au PID du service qui sélectionne l’utilisateur auquel affecter l’élément de travail.

1. Pour empêcher l’équipe de développement des modèles de modifier vos valeurs de propriété, remplacez la boîte de dialogue du supertype de composant.

### Ajout de formulaires et de boîtes de dialogue aux étapes du participant {#adding-forms-and-dialogs-to-participant-steps}

Personnalisez votre composant d’étape de participant pour proposer des fonctionnalités disponibles avec les composants [Étape de participant du formulaire](/help/sites-developing/workflows-step-ref.md#form-participant-step) et [Étape de participant de la boîte de dialogue](/help/sites-developing/workflows-step-ref.md#dialog-participant-step) :

* Présentez un formulaire à l’utilisateur lorsqu’il ouvre l’élément de travail généré.
* Présentez une boîte de dialogue personnalisée à l’utilisateur lorsqu’il effectue l’élément de travail généré.

Effectuez la procédure suivante sur votre nouveau composant (voir [Création de composants d’étape de workflow personnalisée](#creating-custom-workflow-step-components)) :

1. Sous le nœud `cq:Component`, ajoutez le nœud suivant :

   * Nom : `cq:editConfig`
   * Type : `cq:EditConfig`

   Pour plus d’informations sur le nœud cq:editConfig, consultez [Configuration du comportement de modification d’un composant](/help/sites-developing/components-basics.md#edit-behavior).

1. Sous le nœud cq:EditConfig, ajoutez le nœud suivant :

   * Nom : `cq:formParameters`
   * Type : `nt:unstructured`

1. Pour présenter un formulaire lorsque l’utilisateur ouvre l’élément de travail, ajoutez la propriété suivante au nœud `cq:formParameters` :

   * Nom : `FORM_PATH`
   * Type : `String`
   * Valeur : chemin d’accès qui résout le formulaire

1. Pour présenter une boîte de dialogue personnalisée lorsque l’utilisateur effectue l’élément de travail, ajoutez la propriété suivante au nœud `cq:formParameters`.

   * Nom : `DIALOG_PATH`
   * Type : `String`
   * Valeur : chemin d’accès qui résout la boîte de dialogue.

### Configuration du comportement d’exécution de l’étape de workflow {#configuring-the-workflow-step-runtime-behavior}

Sous le nœud `cq:Component`, ajoutez un nœud `cq:EditConfig`. En dessous, ajoutez un nœud `nt:unstructured` (doit être nommé `cq:formParameters`) et ajoutez à ce nœud les propriétés suivantes :

* Nom : `PROCESS_AUTO_ADVANCE`

   * Type : `Boolean`
   * Valeur :

      * Lorsque la propriété est définie sur `true`, le workflow exécute cette étape et se poursuit (c’est le paramètre par défaut qui est également recommandé).
      * Si sa valeur est `false`, le processus s’exécute et s’arrête. Ceci nécessite une manipulation supplémentaire, donc la valeur `true` est recommandée.

* Nom : `DO_NOTIFY`

   * Type : `Boolean`
   * Valeur : indique si des notifications électroniques doivent être envoyées pour les étapes de participation de l’utilisateur (et suppose que le serveur de messagerie est correctement configuré).

## Persistance et accès aux données {#persisting-and-accessing-data}

### Données persistantes pour les étapes de workflow suivantes {#persisting-data-for-subsequent-workflow-steps}

Vous pouvez utiliser les métadonnées de processus pour conserver les informations requises pendant la durée de vie du processus et entre les étapes. Les étapes d’un workflow sont généralement nécessaires pour conserver les données en vue d’une utilisation ultérieure ou pour récupérer les données persistantes des étapes précédentes.

Les métadonnées de processus sont stockées dans un objet [`MetaDataMap`](#metadatamaps). L’API Java fournit la méthode [`Workflow.getWorkflowData`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/Workflow.html) pour renvoyer un objet [`WorkflowData`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/WorkflowData.html) qui fournit l’objet `MetaDataMap` approprié. Cet objet `WorkflowData` `MetaDataMap` est disponible pour le service OSGi ou le script ECMA d’un composant d’étape.

#### Java {#java}

La méthode d’exécution de l’implémentation `WorkflowProcess` est transmise à l’objet `WorkItem`. Utilisez cet objet afin d’obtenir l’objet `WorkflowData` pour l’instance de workflow active. L’exemple suivant ajoute un élément à l’objet workflow `MetaDataMap`, puis enregistre chaque élément. L’élément (&quot;mykey&quot;, &quot;My Step Value&quot;) est disponible pour les étapes suivantes du workflow.

```java
public void execute(WorkItem item, WorkflowSession session, MetaDataMap args) throws WorkflowException {

    MetaDataMap wfd = item.getWorkflow().getWorkflowData().getMetaDataMap();

    wfd.put("mykey", "My Step Value");

    Set<String> keyset = wfd.keySet();
    Iterator<String> i = keyset.iterator();
    while (i.hasNext()){
     Object key = i.next();
     log.info("The workflow medata includes key {} and value {}",key.toString(),wfd.get(key).toString());
    }
}
```

#### Script ECMA {#ecma-script}

La variable `graniteWorkItem` est la représentation de script ECMA de l’objet Java `WorkItem` actif. Par conséquent, vous pouvez utiliser la variable `graniteWorkItem` pour obtenir les métadonnées de workflow. Le script ECMA suivant peut être utilisé pour implémenter un composant **Étape du processus** afin d’ajouter un élément à l’objet de workflow `MetaDataMap`, puis consigner chaque élément. Ces éléments sont ensuite disponibles pour les étapes suivantes du workflow.

>[!NOTE]
>
>La variable `metaData` immédiatement disponible pour le script de l’étape est la métadonnée de l’étape. Les métadonnées d’étape sont différentes des métadonnées de workflow.

```
var currentDateInMillis = new Date().getTime();

graniteWorkItem.getWorkflowData().getMetaDataMap().put("hardcodedKey","theKey");

graniteWorkItem.getWorkflowData().getMetaDataMap().put("currentDateInMillisKey",currentDateInMillis);

var iterator = graniteWorkItem.getWorkflowData().getMetaDataMap().keySet().iterator();
while (iterator.hasNext()){
    var key = iterator.next();
    log.info("Workflow metadata key, value = " + key.toString() + ", " + graniteWorkItem.getWorkflowData().getMetaDataMap().get(key));
}
```

### Accès aux valeurs des propriétés de boîte de dialogue au moment de l’exécution {#accessing-dialog-property-values-at-runtime}

L’objet `MetaDataMap` des instances de workflow est utile pour stocker et récupérer des données tout au long de la durée de vie du workflow. Dans le cas d’implémentations de composants d’étape de workflow, l’objet `MetaDataMap` est particulièrement utile pour récupérer les valeurs de propriété de composant au moment de l’exécution.

>[!NOTE]
>
>Pour plus d’informations sur la configuration de la boîte de dialogue de composant dans le but de stocker les propriétés en tant que métadonnées de workflow, consultez la section [Enregistrement des valeurs de propriété dans les métadonnées de workflow](#saving-property-values-in-workflow-metadata).

Le workflow `MetaDataMap` est disponible pour les implémentations de processus de script Java et ECMA :

* Dans les implémentations Java de l’interface WorkflowProcess, le paramètre `args` est l’objet `MetaDataMap` du workflow.

* Dans les implémentations de script ECMA, la valeur est disponible en utilisant les variables `args` et `metadata`.

### Exemple : récupération des arguments du composant de l’étape de processus {#example-retrieving-the-arguments-of-the-process-step-component}

La boîte de dialogue de modification du composant **Étape du processus** inclut la propriété **Arguments**. La valeur de la propriété **Arguments** est stockée dans les métadonnées du workflow et est associée à la clé `PROCESS_ARGS`.

Dans le diagramme suivant, la valeur de la propriété **Arguments** est `argument1, argument2` :

![wf-24](assets/wf-24.png)

#### Java {#java-1}

Le code Java suivant est la méthode `execute` pour une implémentation `WorkflowProcess`. La méthode enregistre la valeur dans l’objet `args` `MetaDataMap` associé à la clé `PROCESS_ARGS`.

```java
public void execute(WorkItem item, WorkflowSession session, MetaDataMap args) throws WorkflowException {
     if (args.containsKey("PROCESS_ARGS")){
      log.info("workflow metadata for key PROCESS_ARGS and value {}",args.get("PROCESS_ARGS","string").toString());
     }
    }
```

Lorsqu’une étape de processus qui utilise cette implémentation Java s’exécute, le journal contient l’entrée suivante :

```xml
16.02.2018 12:07:39.566 *INFO* [JobHandler: /var/workflow/instances/server0/2018-02-16/model_855140139900189:/content/we-retail/de] com.adobe.example.workflow.impl.process.LogArguments workflow metadata for key PROCESS_ARGS and value argument1, argument2
```

#### Script ECMA {#ecma-script-1}

Le script ECMA suivant est utilisé comme processus pour **Étape du processus**. Il consigne le nombre d’arguments et les valeurs d’argument :

```
var iterator = graniteWorkItem.getWorkflowData().getMetaDataMap().keySet().iterator();
while (iterator.hasNext()){
    var key = iterator.next();
    log.info("Workflow metadata key, value = " + key.toString() + ", " + graniteWorkItem.getWorkflowData().getMetaDataMap().get(key));
}
log.info("hardcodedKey "+ graniteWorkItem.getWorkflowData().getMetaDataMap().get("hardcodedKey"));
log.info("currentDateInMillisKey "+ graniteWorkItem.getWorkflowData().getMetaDataMap().get("currentDateInMillisKey"));
```

>[!NOTE]
>
>Cette section explique comment utiliser les arguments pour les étapes de processus. Les informations s’appliquent également aux programmes de sélection des participants dynamiques.

>[!NOTE]
>Pour un autre exemple de stockage des propriétés de composant dans les métadonnées de workflow, consultez l’Exemple : Créer une étape de workflow de logger. Cet exemple comporte un journal qui associe la valeur des métadonnées à une clé autre que PROCESS_ARGS.

### Scripts et arguments de processus {#scripts-and-process-arguments}

Dans un script pour un composant **Étape du processus**, les arguments sont disponibles via l’objet `args`.

Lors de la création d’un composant d’étape personnalisée, l’objet `metaData` est disponible dans un script. Cet objet est limité à un seul argument de chaîne.

## Développement de mises en oeuvre d’étapes de processus {#developing-process-step-implementations}

Lorsque les étapes de processus sont lancées au cours du traitement d’un processus, les étapes envoient une requête à un service OSGi ou exécutent un script ECMA. Développez le service ou le script ECMA qui effectue les actions requises par votre workflow.

>[!NOTE]
>
>Pour plus d’informations sur l’association de votre composant Étape du processus au service ou au script, voir [Étape du processus](/help/sites-developing/workflows-step-ref.md#process-step) ou [Remplacement de la mise en oeuvre de l’étape](#overriding-the-step-implementation).

### Mise en oeuvre d’une étape de processus avec une classe Java {#implementing-a-process-step-with-a-java-class}

Pour définir une étape de processus en tant que composant de service OSGI (lot Java) :

1. Créez le bundle et déployez-le dans le conteneur OSGI. Reportez-vous à la documentation sur la création d’un bundle avec [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) ou [Eclipse](/help/sites-developing/howto-projects-eclipse.md).

   >[!NOTE]
   >
   >Le composant OSGI doit implémenter l’interface `WorkflowProcess` avec sa méthode `execute()`. Voir l’exemple de code ci-dessous.

   >[!NOTE]
   >
   >Le nom du package doit être ajouté à la section `<*Private-Package*>` de la configuration `maven-bundle-plugin`.

1. Ajoutez la propriété SCR `process.label` et définissez sa valeur selon vos besoins. Il s’agit du nom sous lequel votre étape de processus est listée lorsque vous utilisez le composant générique **Étape du processus**. Voir l’exemple ci-dessous.
1. Dans l’éditeur de **Modèles**, ajoutez l’étape de traitement au workflow à l’aide du composant générique **Étape du processus**.
1. Dans la boîte de dialogue de modification (de l’**étape du processus**), accédez à l’onglet **Processus** et sélectionnez votre implémentation de processus.
1. Si vous utilisez des arguments dans votre code, définissez les **Arguments du processus**. Par exemple : false.
1. Enregistrez les modifications, tant pour l’étape que pour le modèle de workflow (coin supérieur gauche de l’éditeur de modèles).

Les méthodes java, respectivement les classes qui implémentent la méthode Java exécutable, sont enregistrées en tant que services OSGI, ce qui vous permet d’ajouter des méthodes à tout moment pendant l’exécution.

Le composant OSGI suivant ajoute la propriété `approved` au nœud de contenu de page lorsque la charge est une page :

```java
package com.adobe.example.workflow.impl.process;

import com.adobe.granite.workflow.WorkflowException;
import com.adobe.granite.workflow.WorkflowSession;
import com.adobe.granite.workflow.exec.WorkItem;
import com.adobe.granite.workflow.exec.WorkflowData;
import com.adobe.granite.workflow.exec.WorkflowProcess;
import com.adobe.granite.workflow.metadata.MetaDataMap;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Service;

import org.osgi.framework.Constants;

import javax.jcr.Node;
import javax.jcr.RepositoryException;
import javax.jcr.Session;

/**
 * Sample workflow process that sets an <code>approve</code> property to the payload based on the process argument value.
 */
@Component
@Service
public class MyProcess implements WorkflowProcess {

 @Property(value = "An example workflow process implementation.")
 static final String DESCRIPTION = Constants.SERVICE_DESCRIPTION;
 @Property(value = "Adobe")
 static final String VENDOR = Constants.SERVICE_VENDOR;
 @Property(value = "My Sample Workflow Process")
 static final String LABEL="process.label";

 private static final String TYPE_JCR_PATH = "JCR_PATH";

 public void execute(WorkItem item, WorkflowSession session, MetaDataMap args) throws WorkflowException {
  WorkflowData workflowData = item.getWorkflowData();
  if (workflowData.getPayloadType().equals(TYPE_JCR_PATH)) {
   String path = workflowData.getPayload().toString() + "/jcr:content";
   try {
    Session jcrSession = session.adaptTo(Session.class);
    Node node = (Node) jcrSession.getItem(path);
    if (node != null) {
     node.setProperty("approved", readArgument(args));
     jcrSession.save();
    }
   } catch (RepositoryException e) {
    throw new WorkflowException(e.getMessage(), e);
   }
  }
 }

 private boolean readArgument(MetaDataMap args) {
  String argument = args.get("PROCESS_ARGS", "false");
  return argument.equalsIgnoreCase("true");
 }
}
```

>[!NOTE]
>
>Si le processus échoue trois fois de suite, un élément est placé dans la boîte de réception de l’administrateur de workflow.

### Utilisation d’ECMAScript {#using-ecmascript}

Les scripts ECMA permettent aux développeurs de scripts d’implémenter des étapes de processus. Les scripts se trouvent dans le référentiel JCR et sont exécutés à partir de cet emplacement.

Le tableau suivant répertorie les variables immédiatement disponibles pour traiter les scripts, ce qui permet d’accéder aux objets de l’API Java du workflow.

| Classe Java | Nom de variable de script | Description |
|---|---|---|
| `com.adobe.granite.workflow.exec.WorkItem` | `graniteWorkItem` | Instance de l’étape en cours. |
| `com.adobe.granite.workflow.WorkflowSession` | `graniteWorkflowSession` | Session de workflow de l’instance d’étape actuelle. |
| `String[]` (contient des arguments de processus) | `args` | Arguments de l’étape. |
| `com.adobe.granite.workflow.metadata.MetaDataMap` | `metaData` | Métadonnées de l’instance d’étape actuelle. |
| `org.apache.sling.scripting.core.impl.InternalScriptHelper` | `sling` | Permet d’accéder à l’environnement d’exécution Sling. |

L’exemple de script suivant montre comment accéder au nœud JCR qui représente le payload du workflow. La variable `graniteWorkflowSession` est adaptée à une variable de session JCR, utilisée pour obtenir le nœud à partir du chemin d’accès du payload.

```
var workflowData = graniteWorkItem.getWorkflowData();
if (workflowData.getPayloadType() == "JCR_PATH") {
    var path = workflowData.getPayload().toString();
    var jcrsession = graniteWorkflowSession.adaptTo(Packages.javax.jcr.Session);
    var node = jcrsession.getNode(path);
    if (node.hasProperty("approved")){
     node.setProperty("approved", args[0] == "true" ? true : false);
     node.save();
 }
}
```

Le script suivant vérifie si le payload est un fichier image (`.png`), crée une image en noir et blanc et l’enregistre en tant que nœud frère.

```
var workflowData = graniteWorkItem.getWorkflowData();
if (workflowData.getPayloadType() == "JCR_PATH") {
    var path = workflowData.getPayload().toString();
    var jcrsession = graniteWorkflowSession.adaptTo(Packages.javax.jcr.Session);
    var node = jcrsession.getRootNode().getNode(path.substring(1));
     if (node.isNodeType("nt:file") && node.getProperty("jcr:content/jcr:mimeType").getString().indexOf("image/") == 0) {
        var is = node.getProperty("jcr:content/jcr:data").getStream();
        var layer = new Packages.com.day.image.Layer(is);
        layer.grayscale();
                var parent = node.getParent();
                var gn = parent.addNode("grey" + node.getName(), "nt:file");
        var content = gn.addNode("jcr:content", "nt:resource");
                content.setProperty("jcr:mimeType","image/png");
                var cal = Packages.java.util.Calendar.getInstance();
                content.setProperty("jcr:lastModified",cal);
                var f = Packages.java.io.File.createTempFile("test",".png");
        var tout = new Packages.java.io.FileOutputStream(f);
        layer.write("image/png", 1.0, tout);
        var fis = new Packages.java.io.FileInputStream(f);
                content.setProperty("jcr:data", fis);
                parent.save();
        tout.close();
        fis.close();
        is.close();
        f.deleteOnExit();
    }
}
```

Pour utiliser le script, procédez comme suit :

1. Créez le script (par exemple, avec CRXDE Lite) et enregistrez-le dans le référentiel ci-dessous. `//apps/workflow/scripts/`
1. Pour spécifier un titre qui identifie le script dans la boîte de dialogue de modification d’**Étape du processus**, ajoutez les propriétés suivantes au nœud `jcr:content` de votre script :

   | Nom | Type | Valeur |
   |---|---|---|
   | `jcr:mixinTypes` | `Name[]` | `mix:title` |
   | `jcr:title` | `String` | Nom à afficher dans la boîte de dialogue de modification. |

1. Modifiez la variable **Étape du processus** et indiquez le script à utiliser.

## Développement de sélecteurs de participant {#developing-participant-choosers}

Vous pouvez développer des programmes de sélection des participants pour **Étape choix dynamique de participant** composants.

Lorsqu’un composant **Étape de participant dynamique** est démarré pendant un workflow, l’étape doit déterminer le participant auquel l’élément de travail généré peut être attribué. Pour ce faire, l’étape :

* envoie une requête à un service OSGi ou
* exécute un script ECMA pour sélectionner le participant.

Vous pouvez développer un service ou un script ECMA qui sélectionne le participant en fonction des exigences de votre workflow.

>[!NOTE]
>
>Pour plus d’informations sur l’association de votre **Étape choix dynamique de participant** avec le service ou le script, voir [Étape choix dynamique de participant](/help/sites-developing/workflows-step-ref.md#dynamic-participant-step) ou [Remplacement de la mise en oeuvre de l’étape](#persisting-and-accessing-data).

### Développement d’un sélecteur de participant à l’aide d’une classe Java {#developing-a-participant-chooser-using-a-java-class}

Pour définir une étape de participant en tant que composant de service OSGI (classe Java) :

1. Le composant OSGI doit implémenter l’interface `ParticipantStepChooser` avec sa méthode `getParticipant()`. Voir l’exemple de code ci-dessous.

   Créez le bundle et déployez-le dans le conteneur OSGI.

1. Ajoutez la propriété SCR `chooser.label` et définissez sa valeur selon vos besoins. Il s’agit du nom sous lequel votre programme de sélection de participants est listé si vous utilisez le composant **Étape de participant dynamique**. Voir l’exemple :

   ```java
   package com.adobe.example.workflow.impl.process;
   
   import com.adobe.granite.workflow.WorkflowException;
   import com.adobe.granite.workflow.WorkflowSession;
   import com.adobe.granite.workflow.exec.ParticipantStepChooser;
   import com.adobe.granite.workflow.exec.WorkItem;
   import com.adobe.granite.workflow.exec.WorkflowData;
   import com.adobe.granite.workflow.metadata.MetaDataMap;
   
   import org.apache.felix.scr.annotations.Component;
   import org.apache.felix.scr.annotations.Property;
   import org.apache.felix.scr.annotations.Service;
   
   import org.osgi.framework.Constants;
   
   /**
    * Sample dynamic participant step that determines the participant based on a path given as argument.
    */
   @Component
   @Service
   
   public class MyDynamicParticipant implements ParticipantStepChooser {
   
    @Property(value = "An example implementation of a dynamic participant chooser.")
    static final String DESCRIPTION = Constants.SERVICE_DESCRIPTION;
       @Property(value = "Adobe")
       static final String VENDOR = Constants.SERVICE_VENDOR;
       @Property(value = "Dynamic Participant Chooser Process")
       static final String LABEL=ParticipantStepChooser.SERVICE_PROPERTY_LABEL;
   
       private static final String TYPE_JCR_PATH = "JCR_PATH";
   
       public String getParticipant(WorkItem workItem, WorkflowSession workflowSession, MetaDataMap args) throws WorkflowException {
           WorkflowData workflowData = workItem.getWorkflowData();
           if (workflowData.getPayloadType().equals(TYPE_JCR_PATH)) {
               String path = workflowData.getPayload().toString();
               String pathFromArgument = args.get("PROCESS_ARGS", String.class);
               if (pathFromArgument != null && path.startsWith(pathFromArgument)) {
                   return "admin";
               }
           }
           return "administrators";
       }
   }
   ```

1. Dans l’éditeur de **Modèles**, ajoutez l’étape de participant dynamique au workflow à l’aide du composant **Étape de participant dynamique** générique.
1. Dans la boîte de dialogue de modification, sélectionnez l’onglet **Programme de sélection des participants** et choisissez votre implémentation de programme de sélection.
1. Si vous utilisez des arguments dans votre code, définissez les **Arguments du processus**. Pour cet exemple : `/content/we-retail/de`.
1. Enregistrez les modifications, tant pour l’étape que pour le modèle de workflow.

### Développement d’un sélecteur de participant à l’aide d’un script ECMA {#developing-a-participant-chooser-using-an-ecma-script}

Vous pouvez créer un script ECMA qui sélectionne l’utilisateur auquel est affecté l’élément de travail généré par **Étape du participant**. Le script doit inclure une fonction nommée `getParticipant` qui ne nécessite aucun argument et renvoie une `String` contenant l’ID d’un utilisateur ou d’un groupe.

Les scripts se trouvent dans le référentiel JCR et y sont exécutés.

Le tableau suivant répertorie les variables qui permettent un accès immédiat aux objets Java de workflow dans vos scripts.

| Classe Java | Nom de variable de script |
|---|---|
| `com.adobe.granite.workflow.exec.WorkItem` | `graniteWorkItem` |
| `com.adobe.granite.workflow.WorkflowSession` | `graniteWorkflowSession` |
| `String[]` (contient des arguments de processus) | `args` |
| `com.adobe.granite.workflow.metadata.MetaDataMap` | `metaData` |
| `org.apache.sling.scripting.core.impl.InternalScriptHelper` | `sling` |

```
function getParticipant() {
    var workflowData = graniteWorkItem.getWorkflowData();
    if (workflowData.getPayloadType() == "JCR_PATH") {
        var path = workflowData.getPayload().toString();
        if (path.indexOf("/content/we-retail/de") == 0) {
            return "admin";
        } else {
            return "administrators";
        }
    }
}
```

1. Créez le script (par exemple, avec CRXDE Lite) et enregistrez-le dans le référentiel ci-dessous. `//apps/workflow/scripts`
1. Pour spécifier un titre qui identifie le script dans la boîte de dialogue de modification d’**Étape du processus**, ajoutez les propriétés suivantes au nœud `jcr:content` de votre script :

   | Nom | Type | Valeur |
   |---|---|---|
   | `jcr:mixinTypes` | `Name[]` | `mix:title` |
   | `jcr:title` | `String` | Nom à afficher dans la boîte de dialogue de modification. |

1. Modifiez l’instance [Étape de participant dynamique](/help/sites-developing/workflows-step-ref.md#dynamic-participant-step) et spécifiez le script à utiliser.

## Gestion des packages de workflow {#handling-workflow-packages}

[Les packages de workflow](/help/sites-authoring/workflows-applying.md#specifying-workflow-details-in-the-create-workflow-wizard) peuvent être transmis à un workflow pour traitement. Les modules de workflow contiennent des références à des ressources telles que des pages et des ressources.

>[!NOTE]
>
>Les étapes de processus de workflow suivantes acceptent les modules de processus pour l’activation de pages en bloc :
>
>* [`com.day.cq.wcm.workflow.process.ActivatePageProcess`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/workflow/process/ActivatePageProcess.html)
>* [`com.day.cq.wcm.workflow.process.DeactivatePageProcess`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/workflow/process/DeactivatePageProcess.html)
>

Vous pouvez développer des étapes de workflow qui obtiennent et traitent les ressources de package. Les membres suivants du package `com.day.cq.workflow.collection` donnent accès aux packages de workflow :

* `ResourceCollection` : classe de package de workflow.
* `ResourceCollectionUtil` : permet de récupérer des objets ResourceCollection.
* `ResourceCollectionManager` : crée et récupère des collections. Une implémentation est déployée en tant que service OSGi.

L’exemple de classe Java suivant montre comment obtenir des ressources de package :

```java
package com.adobe.example;

import java.util.ArrayList;
import java.util.List;

import com.day.cq.workflow.WorkflowException;
import com.day.cq.workflow.WorkflowSession;
import com.day.cq.workflow.collection.ResourceCollection;
import com.day.cq.workflow.collection.ResourceCollectionManager;
import com.day.cq.workflow.collection.ResourceCollectionUtil;
import com.day.cq.workflow.exec.WorkItem;
import com.day.cq.workflow.exec.WorkflowData;
import com.day.cq.workflow.exec.WorkflowProcess;
import com.day.cq.workflow.metadata.MetaDataMap;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Service;
import org.apache.felix.scr.annotations.Reference;
import org.osgi.framework.Constants;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import javax.jcr.Node;
import javax.jcr.PathNotFoundException;
import javax.jcr.RepositoryException;
import javax.jcr.Session;

@Component
@Service
public class LaunchBulkActivate implements WorkflowProcess {

 private static final Logger log = LoggerFactory.getLogger(LaunchBulkActivate.class);

 @Property(value="Bulk Activate for Launches")
  static final String PROCESS_NAME ="process.label";
 @Property(value="A sample workflow process step to support Launches bulk activation of pages")
 static final String SERVICE_DESCRIPTION = Constants.SERVICE_DESCRIPTION;

 @Reference
 private ResourceCollectionManager rcManager;
public void execute(WorkItem workItem, WorkflowSession workflowSession) throws Exception {
    Session session = workflowSession.getSession();
    WorkflowData data = workItem.getWorkflowData();
    String path = null;
    String type = data.getPayloadType();
    if (type.equals(TYPE_JCR_PATH) && data.getPayload() != null) {
        String payloadData = (String) data.getPayload();
        if (session.itemExists(payloadData)) {
            path = payloadData;
        }
    } else if (data.getPayload() != null && type.equals(TYPE_JCR_UUID)) {
        Node node = session.getNodeByUUID((String) data.getPayload());
        path = node.getPath();
    }

    // CUSTOMIZED CODE IF REQUIRED....

    if (path != null) {
        // check for resource collection
        ResourceCollection rcCollection = ResourceCollectionUtil.getResourceCollection((Node)session.getItem(path), rcManager);
        // get list of paths to replicate (no resource collection: size == 1
        // otherwise size >= 1
        List<String> paths = getPaths(path, rcCollection);
        for (String aPath: paths) {

            // CUSTOMIZED CODE....

        }
    } else {
        log.warn("Cannot process because path is null for this " + "workitem: " + workItem.toString());
    }
}

/**
 * helper
 */
private List<String> getPaths(String path, ResourceCollection rcCollection) {
    List<String> paths = new ArrayList<String>();
    if (rcCollection == null) {
        paths.add(path);
    } else {
        log.debug("ResourceCollection detected " + rcCollection.getPath());
        // this is a resource collection. the collection itself is not
        // replicated. only its members
        try {
            List<Node> members = rcCollection.list(new String[]{"cq:Page", "dam:Asset"});
            for (Node member: members) {
                String mPath = member.getPath();
                paths.add(mPath);
            }
        } catch(RepositoryException re) {
            log.error("Cannot build path list out of the resource collection " + rcCollection.getPath());
        }
    }
    return paths;
}
}
```

## Exemple : création d’une étape personnalisée {#example-creating-a-custom-step}

Pour commencer facilement à créer votre propre étape personnalisée, copiez une étape existante depuis :

`/libs/cq/workflow/components/model`

### Création de l’étape de base {#creating-the-basic-step}

1. Recréez le chemin sous /apps, par exemple :

   `/apps/cq/workflow/components/model`

   Les nouveaux dossiers sont de type `nt:folder` :

   ```xml
   - apps
     - cq
       - workflow (nt:folder)
         - components (nt:folder)
           - model (nt:folder)
   ```

   >[!NOTE]
   >
   >Cette étape ne s’applique pas à l’éditeur de modèle d’IU classique.

1. Placez ensuite l’étape copiée dans votre dossier /apps ; par exemple, comme suit :

   `/apps/cq/workflow/components/model/myCustomStep`

   Voici le résultat de notre exemple d’étape personnalisée :

   ![wf-34](assets/wf-34.png)

   >[!CAUTION]
   >
   >Puisque dans l’IU standard, seul le titre, et non les détails, est affiché sur la carte, `details.jsp` n’est pas nécessaire (comme c’était le cas avec l’éditeur de l’IU classique).

1. Appliquez les propriétés suivantes au nœud :

   `/apps/cq/workflow/components/model/myCustomStep`

   **Propriétés d’intérêt :**

   * `sling:resourceSuperType`

     Doit hériter d’une étape existante.

     Dans cet exemple, nous héritons de l’étape de base à l’adresse `cq/workflow/components/model/step`, mais vous pouvez utiliser d’autres super types comme `participant`, `process`, etc.

   * `jcr:title`

     Le titre est-il affiché lorsque le composant est répertorié dans le navigateur d’étapes (panneau de gauche de l’éditeur de modèle de workflow).

   * `cq:icon`

     Permet de spécifier une [icône Coral](https://helpx.adobe.com/fr/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html) pour l’étape.

   * `componentGroup`

     Doit être l’un des éléments suivants :

      * Processus de collaboration
      * Processus de gestion des actifs numériques
      * Workflows de formulaires
      * Projets
      * Processus WCM
      * Workflow

   ![wf-35](assets/wf-35.png)

1. Vous pouvez désormais ouvrir un modèle de workflow pour le modifier. Dans le navigateur d’étapes, vous pouvez filtrer pour voir **Mon étape personnalisée** :

   ![wf-36](assets/wf-36.png)

   Si vous faites glisser **Mon étape personnalisée** sur le modèle, la carte s’affiche :

   ![wf-37](assets/wf-37.png)

   Si la propriété `cq:icon` n’a pas été définie pour l’étape, une icône par défaut est rendue d’après les deux premières lettres du titre. Par exemple :

   ![wf-38](assets/wf-38.png)

#### Définition de la boîte de dialogue Configuration de l’étape {#defining-the-step-configure-dialog}

Après [Création de l’étape de base](#creating-the-basic-step), définir l’étape **Configurer** de la boîte de dialogue comme suit :

1. Configurez les propriétés sur le nœud `cq:editConfig` comme suit :

   **Propriétés d’intérêt :**

   * `cq:inherit`

     Si sa valeur est `true`, votre composant d’étape hérite des propriétés de l’étape spécifiée dans `sling:resourceSuperType`.

   * `cq:disableTargeting`

     Définissez-la selon vos besoins.

   ![wf-39](assets/wf-39.png)

1. Configurez les propriétés sur le nœud `cq:formsParameter` comme suit :

   **Propriétés d’intérêt :**

   * `jcr:title`

     Définit le titre par défaut sur la carte étape dans la carte modèle et dans le champ **Titre** de la boîte de dialogue de configuration **Mes propriétés d’étape personnalisées**.

   * Vous pouvez également définir vos propres propriétés personnalisées.

   ![wf-40](assets/wf-40.png)

1. Configurez les propriétés sur le nœud `cq:listeners`.

   La variable `cq:listener` et ses propriétés vous permettent de définir des gestionnaires d’événements qui réagissent aux événements dans l’éditeur de modèles de l’interface utilisateur tactile, comme faire glisser une étape sur une page de modèle ou modifier les propriétés d’une étape.

   **Propriétés d’intérêt :**

   * `afterMove: REFRESH_PAGE`
   * `afterdelete: CQ.workflow.flow.Step.afterDelete`
   * `afteredit: CQ.workflow.flow.Step.afterEdit`
   * `afterinsert: CQ.workflow.flow.Step.afterInsert`

   Cette configuration est essentielle au bon fonctionnement de l’éditeur. Dans la plupart des cas, cette configuration ne doit pas être modifiée.

   Toutefois, la définition de `cq:inherit` sur true (sur la `cq:editConfig` , voir ci-dessus) vous permet d’hériter de cette configuration, sans avoir à l’inclure explicitement dans votre définition d’étape. Si aucun héritage n’est en place, vous devez ajouter ce nœud avec les propriétés et valeurs suivantes.

   Dans cet exemple, l’héritage a été activé pour pouvoir supprimer le nœud `cq:listeners` et permettre à l’étape de fonctionner correctement.

   ![wf-41](assets/wf-41.png)

1. Vous pouvez désormais ajouter une instance de votre étape à un modèle de workflow. Lorsque vous **configurez** l’étape vous voyez s’afficher la boîte de dialogue :

   ![wf-42](assets/wf-42.png) ![wf-43](assets/wf-43.png)

#### Exemple de balisage utilisé dans ce cas de figure {#sample-markup-used-in-this-example}

Le balisage d’une étape personnalisée doit être représenté dans le fichier `.content.xml` du composant nœud racine. Exemple de `.content.xml` utilisé pour ce cas de figure :

`/apps/cq/workflow/components/model/myCustomStep/.content.xml`

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
    cq:icon="bell"
    jcr:primaryType="cq:Component"
    jcr:title="My Custom Step"
    sling:resourceSuperType="cq/workflow/components/model/process"
    allowedParents="[*/parsys]"
    componentGroup="Workflow"/>
```

Exemple de `_cq_editConfig.xml` utilisé dans ce cas de figure :

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:nt="https://www.jcp.org/jcr/nt/1.0"
    cq:disableTargeting="{Boolean}true"
    cq:inherit="{Boolean}true"
    jcr:primaryType="cq:EditConfig">
    <cq:formParameters
        jcr:primaryType="nt:unstructured"
        jcr:title="My Custom Step Card"
        SAMPLE_PROPERY="sample value"/>
    <cq:listeners
        jcr:primaryType="cq:EditListenersConfig"
        afterdelete="CQ.workflow.flow.Step.afterDelete"
        afteredit="CQ.workflow.flow.Step.afterEdit"
        afterinsert="CQ.workflow.flow.Step.afterInsert"
        afterMove="REFRESH_PAGE"/>
</jcr:root>
```

Exemple de `_cq_dialog/.content.xml` utilisé dans ce cas de figure :

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:nt="https://www.jcp.org/jcr/nt/1.0"
    jcr:primaryType="nt:unstructured"
    jcr:title="My Custom - Step Properties"
    sling:resourceType="cq/gui/components/authoring/dialog">
    <content
        jcr:primaryType="nt:unstructured"
        sling:resourceType="granite/ui/components/coral/foundation/tabs">
        <items jcr:primaryType="nt:unstructured">
            <common
                cq:hideOnEdit="true"
                jcr:primaryType="nt:unstructured"
                jcr:title="Common"
                sling:resourceType="granite/ui/components/coral/foundation/fixedcolumns"/>
            <process
                cq:hideOnEdit="true"
                jcr:primaryType="nt:unstructured"
                jcr:title="Process"
                sling:resourceType="granite/ui/components/coral/foundation/fixedcolumns"/>
            <mycommon
                jcr:primaryType="nt:unstructured"
                jcr:title="Common"
                sling:resourceType="granite/ui/components/coral/foundation/fixedcolumns">
                <items jcr:primaryType="nt:unstructured">
                    <columns
                        jcr:primaryType="nt:unstructured"
                        sling:resourceType="granite/ui/components/coral/foundation/container">
                        <items jcr:primaryType="nt:unstructured">
                            <title
                                jcr:primaryType="nt:unstructured"
                                sling:resourceType="granite/ui/components/coral/foundation/form/textfield"
                                fieldLabel="Title"
                                name="./jcr:title"/>
                            <description
                                jcr:primaryType="nt:unstructured"
                                sling:resourceType="granite/ui/components/coral/foundation/form/textarea"
                                fieldLabel="Description"
                                name="./jcr:description"/>
                        </items>
                    </columns>
                </items>
            </mycommon>
            <advanced
                jcr:primaryType="nt:unstructured"
                jcr:title="Advanced"
                sling:resourceType="granite/ui/components/coral/foundation/fixedcolumns">
                <items jcr:primaryType="nt:unstructured">
                    <columns
                        jcr:primaryType="nt:unstructured"
                        sling:resourceType="granite/ui/components/coral/foundation/container">
                        <items jcr:primaryType="nt:unstructured">
                            <email
                                jcr:primaryType="nt:unstructured"
                                sling:resourceType="granite/ui/components/coral/foundation/form/checkbox"
                                fieldDescription="Notify user via email."
                                fieldLabel="Email"
                                name="./metaData/PROCESS_AUTO_ADVANCE"
                                text="Notify user via email."
                                value="true"/>
                        </items>
                    </columns>
                </items>
            </advanced>
        </items>
    </content>
</jcr:root>
```

>[!NOTE]
>
>Notez les nœuds communs et de processus dans la définition de la boîte de dialogue. Ils sont hérités de l’étape de processus que nous avons utilisée comme supertype pour notre étape personnalisée :
>
>`sling:resourceSuperType : cq/workflow/components/model/process`

>[!NOTE]
>
>Les boîtes de dialogue classiques de l’éditeur de modèle de l’IU classique continuent de fonctionner avec celui de l’IU standard tactile.
>
>AEM possède un [outil de modernisation](/help/sites-developing/modernization-tools.md) pour mettre à niveau vos boîtes de dialogue de l’IU classique vers des boîtes de dialogue de l’IU tactile. Une fois la conversion terminée, vous devez apporter quelques améliorations manuelles à la boîte de dialogue pour certains cas.
>
>* Dans les cas où une boîte de dialogue mise à niveau est vide, vous pouvez consulter des boîtes de dialogue `/libs` avec des fonctionnalités similaires à titre d’exemple. Par exemple :
>
>* `/libs/cq/workflow/components/model`
>* `/libs/cq/workflow/components/workflow`
>* `/libs/dam/components`
>* `/libs/wcm/workflow/components/autoassign`
>* `/libs/cq/projects`
>
>  Ne modifiez rien dans `/libs`, utilisez-les simplement comme exemples. Si vous souhaitez utiliser l’une des étapes existantes, copiez-les dans `/apps` et éditez-les ici.
