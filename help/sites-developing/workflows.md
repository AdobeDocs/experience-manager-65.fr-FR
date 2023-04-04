---
title: Développement et extension des workflows
seo-title: Developing and Extending Workflows
description: AEM fournit plusieurs outils et ressources pour créer des modèles de workflow, développer des étapes de workflow et interagir par programme avec les workflows.
seo-description: AEM provides several tools and resources for creating workflow models, developing workflow steps, and for programmatically interacting with workflows
uuid: 5a857589-3b13-4519-bda2-b1dab6005550
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 8954e3df-3afa-4d53-a7e1-255f3b8f499f
exl-id: 041b1767-8b6c-4887-a70d-abc96a116976
source-git-commit: 768576e300b655962adc3e1db20fc5ec06a5ba6c
workflow-type: tm+mt
source-wordcount: '1473'
ht-degree: 25%

---


# Développement et extension des workflows{#developing-and-extending-workflows}

AEM fournit plusieurs outils et ressources pour créer des modèles de workflow, développer des étapes de workflow et interagir par programme avec les workflows.

Les workflows permettent d&#39;automatiser les processus de gestion des ressources et de publication de contenu dans votre environnement AEM. Les workflows se composent d’une série d’étapes, chacune d’elles exécutant une tâche discrète. Vous pouvez utiliser la logique et les données d’exécution pour décider quand un processus peut continuer et sélectionner l’étape suivante à partir de l’une des nombreuses étapes possibles.

Par exemple, les processus d’entreprise pour la création et la publication de pages web incluent les tâches de validation et de validation par différents participants. Ces processus peuvent être modélisés à l’aide de workflows AEM et appliqués à un contenu spécifique.

Les principaux aspects sont abordés ci-dessous, tandis que les pages suivantes abordent d’autres détails :

* [Création de modèles de workflow](/help/sites-developing/workflows-models.md)
* [Extension des fonctionnalités de workflows](/help/sites-developing/workflows-customizing-extending.md)
* [Interaction avec les workflows par programmation](/help/sites-developing/workflows-program-interaction.md)
* [Référence sur les étapes de workflow](/help/sites-developing/workflows-step-ref.md)
* [Référence sur les processus de workflow](/help/sites-developing/workflows-process-ref.md)
* [Bonnes pratiques en matière de workflow](/help/sites-developing/workflows-best-practices.md)

>[!NOTE]
>
>Pour obtenir des informations sur :
>
>* la participation aux workflows, consultez [Utilisation des workflows](/help/sites-authoring/workflows.md) ;
>* l’administration des processus et des instances de processus, consultez [Administration des workflows](/help/sites-administering/workflows.md).
>* Pour consulter un article complet de la communauté, reportez-vous à la section [Modification de ressources numériques à l’aide de processus Adobe Experience Manager.](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/assets-workflow.html?lang=fr)
>* Consultez le [Webinaire Demandez aux experts AEM relatif aux workflows](https://communities.adobeconnect.com/p5s33iburd54/).
>* les modifications apportées aux emplacements des informations, consultez [Restructuration de référentiel dans AEM 6.5](/help/sites-deploying/repository-restructuring.md) et [Bonnes pratiques relatives aux workflows – Emplacements](/help/sites-developing/workflows-best-practices.md#locations).
>


## Modèle {#model}

Un `WorkflowModel` représente une définition (un modèle) d’un workflow. Il est composé de `WorkflowNodes` et de `WorkflowTransitions`. Les transitions se connectent aux nœuds et définissent le *flux*. Le modèle comporte toujours un noeud de départ et un noeud de fin.

### Modèle Runtime {#runtime-model}

Les modèles de workflow bénéficient du contrôle de versions. Lorsque vous exécutez une instance de workflow, elle utilise et conserve le modèle d’exécution du workflow, tel qu’il est disponible au moment du démarrage du workflow.

Un modèle d’exécution est [généré lorsque **Synchronisation** est déclenché dans l’éditeur de modèles de workflow](/help/sites-developing/workflows-models.md#sync-your-workflow-generate-a-runtime-model).

Modifications du modèle de workflow qui se produisent ou modèles d’exécution qui sont générés, ou les deux, *after* l’instance spécifique qui a été lancée ne s’applique pas à cette instance.

>[!CAUTION]
>
>Les étapes effectuées sont définies par la fonction [modèle d’exécution](/help/sites-developing/workflows-models.md#sync-your-workflow-generate-a-runtime-model), générée au moment où la variable **Synchronisation** est déclenchée dans l’éditeur de modèles de workflow.
>
>Si le modèle de workflow est modifié après ce moment (sans **Synchronisation** étant déclenché), l’instance d’exécution ne reflète pas ces modifications. Seuls les modèles d’exécution générés après la mise à jour reflètent les modifications. Les exceptions sont les scripts ECMA sous-jacents, qui ne sont conservés qu’une seule fois afin que ces modifications soient prises en compte.

### Étape {#step}

Chaque étape exécute une tâche discrète. Il existe différents types d’étapes de workflow :

* Participant (utilisateur/groupe) : Ces étapes génèrent un élément de travail et l’attribuent à un utilisateur ou à un groupe. Un utilisateur doit terminer l’élément de travail pour progresser dans le workflow.
* Processus (Script, appel de méthode Java™) : Ces étapes sont exécutées automatiquement par le système. Un script ECMA ou une classe Java™ met en oeuvre l’étape. Les services peuvent être développés pour écouter les événements de workflow spéciaux et exécuter des tâches en fonction de la logique métier.
* Conteneur (sous-workflow) : Ce type d’étape lance un autre modèle de workflow.
* Division/jointure OU : Utilisez la logique pour décider quelle étape exécuter ensuite dans le workflow.
* Division/jointure ET : Permet l’exécution simultanée de plusieurs étapes.

Toutes les étapes partagent les propriétés suivantes : alertes `Autoadvance` et `Timeout` (scriptable).

### Transition {#transition}

`WorkflowTransition` représente une transition entre deux `WorkflowNodes` d’un `WorkflowModel`.

* Il définit le lien entre deux étapes consécutives.
* Il est possible d&#39;appliquer des règles.

### Élément de travail {#workitem}

Un `WorkItem` est l’unité qui est transmise par l’intermédiaire d’une instance de `Workflow` d’un `WorkflowModel`. Il contient les `WorkflowData` sur lesquelles agit l’instance, ainsi qu’une référence au `WorkflowNode` qui décrit l’étape de workflow sous-jacente.

* Il est utilisé pour identifier la tâche et placé dans la boîte de réception correspondante.
* Une instance de workflow peut contenir un ou plusieurs `WorkItems` en même temps (selon le modèle de workflow).
* Le `WorkItem` référence l’instance de workflow.
* Dans le référentiel, la variable `WorkItem` est stocké sous l’instance de workflow.

### Payload {#payload}

Fait référence à la ressource qui doit être avancée par le biais d’un workflow.

L’implémentation de la payload référence une ressource dans le référentiel (par chemin, UUID ou URL) ou par un objet Java™ sérialisé. Le référencement d’une ressource dans le référentiel est flexible et, avec sling productif. Par exemple, le noeud référencé peut être rendu sous la forme d’un formulaire.

### Cycle de vie {#lifecycle}

Est créé lors du démarrage d’un nouveau workflow (en choisissant le modèle de workflow correspondant et en définissant la charge utile) et se termine lorsque le noeud de fin est traité.

Les actions suivantes sont possibles sur une instance de workflow :

* Arrêter
* Suspendre
* Reprendre
* Redémarrer

Les instances terminées et terminées sont archivées.

### Boîte de réception {#inbox}

Chaque compte utilisateur possède sa propre boîte de réception de workflow dans laquelle les `WorkItems` attribués sont accessibles.

Le `WorkItems` sont affectés directement au compte utilisateur ou au groupe auquel ils appartiennent.

### Types de workflow {#workflow-types}

Il existe différents types de processus, comme indiqué dans la console Modèles de processus :

![wf-upgraded-03](assets/wf-upgraded-03.png)

* **Par défaut**

   Ces types sont les workflows d&#39;usine inclus dans une instance d&#39;AEM standard.

* Workflows personnalisés (aucun indicateur dans la console)

   Ces workflows ont été créés comme nouveaux ou à partir de workflows d’usine recouverts de personnalisations.

* **Hérité**

   Il s’agit des workflows créés dans une version antérieure d’AEM. Ces workflows peuvent être conservés pendant une mise à niveau ou exportés sous la forme d’un package de workflow à partir de la version précédente, puis importés dans la nouvelle version.

### Workflows transitoires {#transient-workflows}

Les workflows standard enregistrent les informations d’exécution (historique) lors de leur exécution. Vous pouvez également définir un modèle de workflow comme **transitoire** pour éviter la persistance d’un tel historique. Ce workflow est utilisé pour l’optimisation des performances, car il permet de gagner du temps et des ressources lors de la conservation des informations.

Les workflows transitoires peuvent être utilisés pour tout workflow qui :

* sont exécutées fréquemment.
* n’ont pas besoin de l’historique des workflows.

Les workflows transitoires ont été introduits pour charger de nombreuses ressources, où les informations sur les ressources sont importantes, mais pas l’historique d’exécution des workflows.

>[!NOTE]
>
>Voir [Création d’un workflow transitoire](/help/sites-developing/workflows-models.md#creating-a-transient-workflow) pour plus de détails.

>[!CAUTION]
>
>Lorsqu’un modèle de workflow est marqué comme transitoire, il existe quelques scénarios où les informations d’exécution doivent toujours être conservées :
>
>* Le type de charge utile (vidéo, par exemple) nécessite des étapes externes pour le traitement ; dans ce cas, l’historique d’exécution est nécessaire pour la confirmation de l’état.
>* Le workflow entre dans une **Division ET**. Dans ce cas, l’historique d’exécution est nécessaire pour la confirmation de l’état.
>* Lorsque le workflow transitoire entre dans une étape de participant, il passe en mode, au moment de l’exécution, à non transitoire. Lorsque la tâche est transmise à une personne, l&#39;historique doit être conservé.
>


>[!CAUTION]
>
>Dans un workflow transitoire, vous ne devez pas utiliser un **Atteindre l’étape**.
>
>La raison en est que la variable **Atteindre l’étape** crée une tâche sling pour continuer le workflow à l’adresse `goto` point. Cela va à l’encontre de l’objectif consistant à rendre le workflow transitoire et génère une erreur dans le fichier journal.
>
>Utilisation **Division OU** pour effectuer des choix au sein d’un workflow transitoire.

>[!NOTE]
>
>Voir [Bonnes pratiques pour les ressources](/help/assets/performance-tuning-guidelines.md#transient-workflows) pour plus d’informations sur l’impact des workflows transitoires sur les performances des ressources.

### Prise en charge multi-ressource {#multi-resource-support}

Activation **Prise en charge multi-ressource** pour votre modèle de workflow, cela signifie qu’une seule instance de workflow est lancée même lorsque vous sélectionnez plusieurs ressources. Chacun d&#39;eux est joint sous la forme d&#39;un package.

If **Prise en charge multi-ressource** n’est pas activé pour votre modèle de workflow et que plusieurs ressources sont sélectionnées, une instance de workflow individuelle est lancée pour chaque ressource.

>[!NOTE]
>
>Voir [Configuration d’un workflow pour la prise en charge multi-ressource](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support) pour plus de détails.

### Étapes de workflow {#workflow-stages}

Les étapes de workflow permettent de visualiser la progression d’un workflow lors de la gestion des tâches. Ils peuvent être utilisés pour fournir une vue d’ensemble de l’avancement du traitement du workflow. Lorsque le workflow s’exécute, l’utilisateur peut afficher la progression décrite par **Évaluation** (contrairement à une étape individuelle).

Les noms des étapes pouvant être spécifiques et techniques, les noms des phases peuvent être définis pour fournir une vue conceptuelle de la progression du workflow.

Par exemple, pour un workflow comportant six étapes et quatre étapes :

1. Vous pouvez [configurez les étapes de workflow (qui affichent la progression du workflow), puis attribuez l’étape appropriée à chaque étape de votre workflow.](/help/sites-developing/workflows-models.md#configuring-workflow-stages-that-show-workflow-progress):

   * Plusieurs noms d’étape peuvent être créés.
   * Un nom d’étape individuel est ensuite attribué à chaque étape (un nom d’étape peut être attribué à une ou plusieurs étapes).

   | **Nom de l’étape** | **Phase (affectée à l’étape)** |
   |---|---|
   | Étape 1 | Création |
   | Étape 2 | Création |
   | Étape 3 | Révision |
   | Étape 4 | Approuver |
   | Étape 5 | Terminé |
   | Étape 6 | Terminé |

1. Lorsque le workflow est exécuté, l’utilisateur peut afficher la progression en fonction des noms des phases (au lieu des noms des étapes). La progression du workflow s’affiche dans la [Onglet INFORMATIONS DU WORKFLOW de la fenêtre des détails de la tâche de l’élément de workflow](/help/sites-authoring/workflows-participating.md#opening-a-workflow-item-to-view-details-and-take-actions) répertorié dans le [Boîte de réception](/help/sites-authoring/inbox.md).

### Workflows et Forms {#workflows-and-forms}

En règle générale, les processus sont utilisés pour traiter les envois de formulaire dans AEM. Cela peut être avec la fonction [composants principaux de formulaire](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-container.html?lang=en) disponible dans une instance d’AEM standard, ou avec la fonction [Solution AEM Forms](/help/forms/using/aem-forms-workflow.md).

Lors de la création d’un formulaire, l’envoi du formulaire peut facilement être associé à un modèle de processus. Par exemple, pour stocker le contenu à un emplacement particulier du référentiel ou pour informer un utilisateur de l’envoi du formulaire et de son contenu.

### Workflows et traduction {#workflows-and-translation}

Les workflows font également partie des [Traduction](/help/sites-administering/translation.md) processus.
