---
title: Développement et extension des workflows
seo-title: Développement et extension des workflows
description: AEM fournit plusieurs outils et ressources pour créer des modèles de workflow, développer des étapes de workflow et interagir par programme avec les workflows.
seo-description: AEM fournit plusieurs outils et ressources pour créer des modèles de workflow, développer des étapes de workflow et interagir par programme avec les workflows.
uuid: 5a857589-3b13-4519-bda2-b1dab6005550
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 8954e3df-3afa-4d53-a7e1-255f3b8f499f
exl-id: 041b1767-8b6c-4887-a70d-abc96a116976
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1535'
ht-degree: 75%

---

# Développement et extension des workflows{#developing-and-extending-workflows}

AEM fournit plusieurs outils et ressources pour créer des modèles de workflow, développer des étapes de workflow et interagir par programme avec les workflows.

Les workflows vous permettent d’automatiser les processus pour gérer les ressources et publier le contenu dans votre environnement AEM. Les workflows sont constitués d’une série d’étapes accomplissant chacune une tâche discrète. Vous pouvez utiliser la logique et les données d’exécution pour prendre des décisions quant au moment où un processus peut se poursuivre et choisir l’étape suivante parmi plusieurs possibles.

Par exemple, les processus métier pour la création et la publication de pages web incluent des tâches d’approbation et de validation par différents participants. Ces processus peuvent être modélisés à l’aide de workflows AEM et appliqués au contenu spécifié.

Les aspects clés sont présentés ci-dessous, tandis que les pages suivantes abordent d’autres détails :

* [Création de modèles de workflow](/help/sites-developing/workflows-models.md)
* [Extension des fonctionnalités de processus](/help/sites-developing/workflows-customizing-extending.md)
* [Interaction avec les workflows par programmation](/help/sites-developing/workflows-program-interaction.md)
* [Référence sur les étapes de workflow](/help/sites-developing/workflows-step-ref.md)
* [Référence sur les processus de workflow](/help/sites-developing/workflows-process-ref.md)
* [Meilleures pratiques en matière de workflow](/help/sites-developing/workflows-best-practices.md)

>[!NOTE]
>
>Pour obtenir des informations sur :
>
>* Pour participer aux workflows, voir [Utilisation des workflows](/help/sites-authoring/workflows.md).
>* l’administration des processus et des instances de processus, voir [Administration des workflows](/help/sites-administering/workflows.md).
>* Pour un article complet de la communauté, voir [Modification de ressources numériques à l’aide de processus Adobe Experience Manager.](https://helpx.adobe.com/fr/experience-manager/using/modify_asset_workflow.html)
>* Voir le [webinaire Ask the AEM Experts relatif aux workflows](https://bit.ly/ATACE218).
>* Pour un article complet de la communauté, reportez-vous à la section [Création d’une étape de participant dynamique Adobe Experience Manager 6.3 personnalisée](https://helpx.adobe.com/fr/experience-manager/using/dynamic-steps-aem63.html).
>* les modifications apportées aux emplacements des informations, voir [Restructuration de référentiel dans AEM 6.5](/help/sites-deploying/repository-restructuring.md) et [Meilleures pratiques relatives aux workflows – emplacements](/help/sites-developing/workflows-best-practices.md#locations).

>



## Modèle {#model}

Un `WorkflowModel` représente une définition (un modèle) d’un workflow. Il est composé de `WorkflowNodes` et `WorkflowTransitions`. Les transitions relient les noeuds et définissent le *flux*. Le modèle dispose toujours d’un nœud de début et d’un nœud de fin.

### Modèle d’exécution {#runtime-model}

Les modèles de workflow bénéficient du contrôle de versions. Lorsque vous exécutez une instance de workflow, celle-ci utilise (et conserve) le modèle d’exécution du workflow (si disponible lors du démarrage du workflow).

Un modèle d’exécution est [généré lorsque la **synchronisation** est déclenchée dans l’editeur de modèles de workflow](/help/sites-developing/workflows-models.md#sync-your-workflow-generate-a-runtime-model).

Les modifications apportées au modèle de workflow et/ou aux modèles d’exécution générés, *après* le démarrage de l’instance spécifique ne sont pas appliqués à cette instance.

>[!CAUTION]
>
>Les étapes exécutées sont celles définies par le [modèle d’exécution](/help/sites-developing/workflows-models.md#sync-your-workflow-generate-a-runtime-model) qui est généré lorsque l’action de **synchronisation** est déclenchée dans l’éditeur de modèles de workflow.
>
>Si le modèle de workflow est modifié après ce stade (sans déclenchement de **synchronisation**), son instance d’exécution ne reflète pas ces modifications. Seuls les modèles de mise en œuvre générés après la mise à jour reflètent les modifications. Les exceptions sont les scripts ECMA sous-jacents, qui ne sont conservés qu’une seule fois, de sorte que les modifications apportées à ces derniers sont sélectionnées.

### Étape {#step}

Chaque étape accomplit une tâche discrète. Il existe différents types d’étapes de workflow :

* Participant (utilisateur/groupe) : ces étapes génèrent un élément de travail et l’attribuent à un utilisateur ou à un groupe. Un utilisateur doit terminer l’élément de travail pour faire avancer le processus.
* Processus (script ou appel de méthode Java) : ces étapes sont exécutées automatiquement par le système. Un script ECMA ou une classe Java met l’étape en œuvre. Les services peuvent être développés pour écouter les événements de workflow spéciaux et effectuer des tâches en fonction de la logique métier.
* Conteneur (sous-processus) : ce type d’étape démarre un autre modèle de workflow.
* Division/jonction OU : utilisez la logique pour décider de l’étape suivante à exécuter dans le workflow.
* Division/jonction ET : autorisez l’exécution simultanée de plusieurs étapes.

Toutes les étapes partagent les propriétés communes suivantes : Alertes `Autoadvance` et `Timeout` (scriptable).

### Transition {#transition}

Une `WorkflowTransition` représente une transition entre deux `WorkflowNodes` d&#39;une `WorkflowModel`.

* Il définit le lien entre deux étapes consécutives.
* Il est possible d’appliquer des règles.

### Élément de travail {#workitem}

Une `WorkItem` est l’unité transmise par l’intermédiaire d’une instance `Workflow` d’une `WorkflowModel`. Elle contient la balise `WorkflowData` sur laquelle l’instance agit et une référence à la balise `WorkflowNode` qui décrit l’étape du workflow sous-jacent.

* Il est utilisé pour identifier la tâche et placé dans la boîte de réception correspondante.
* Une instance de workflow peut comporter une ou plusieurs `WorkItems` en même temps (selon le modèle de workflow).
* `WorkItem` référence l’instance de workflow.
* Dans le référentiel, `WorkItem` est stocké sous l’instance de workflow.

### Charge utile {#payload}

Elle référence la ressource qui doit être avancée par un workflow.

La mise en œuvre de charge utile référence une ressource dans le référentiel (par chemin, UUID ou URL) ou par un objet Java sérialisé. Le référencement d’une ressource dans le référentiel est très flexible et productif en conjonction avec Sling ; par exemple, le rendu du nœud référencé peut être effectué sous forme de formulaire.

### Cycle de vie {#lifecycle}

Il est créé lorsque vous démarrez un nouveau workflow (en choisissant le modèle de workflow respectif et en définissant la charge utile) et se termine lorsque le nœud de fin est traité.

Les actions suivantes sont possibles sur une instance de workflow :

* Arrêter
* Suspendre
* Reprendre
* Redémarrer

Les instances terminées et arrêtées sont archivées.

### Boîte de réception {#inbox}

Chaque compte utilisateur possède sa propre boîte de réception de workflow dans laquelle les `WorkItems` attribués sont accessibles.

Les `WorkItems` sont affectés directement au compte utilisateur ou au groupe auquel ils appartiennent.

### Types de workflow {#workflow-types}

Il existe différents types de workflow comme indiqué dans la console Modèles de workflow :

![wf-upgrade-03](assets/wf-upgraded-03.png)

* **Valeur par défaut**

   Il s’agit des workflows d’usine inclus dans une instance d’AEM standard.

* Workflows personnalisés (aucun indicateur dans la console)

   Il s’agit de workflows qui ont été créés comme nouveaux ou à partir de workflows d’usine qui ont été recouverts de personnalisations.

* **Legacy**

   Workflows créés dans une version antérieure d’AEM. Ils peuvent être conservés lors d’une mise à niveau, ou exportés en tant que module de workflow à partir de la version antérieure, puis importés dans la nouvelle version.

### Workflows transitoires {#transient-workflows}

Les workflows standard enregistrent les informations (d’historique) d’exécution lors de leur exécution. Vous pouvez également définir un modèle de workflow en tant que **Transitoire** pour éviter que cet historique ne soit conservé. Il est utilisé pour ajuster les performances, car il économise le temps/les ressources utilisés pour rendre les informations persistantes.

Les workflows transitoires peuvent être utilisés pour tout workflow qui :

* est exécuté fréquemment ;
* ne nécessite pas l’historique de workflows.

Les workflows transitoires ont été introduits pour charger un grand nombre de ressources, où les informations des ressources sont importantes, mais pas l’historique d’exécution des workflows.

>[!NOTE]
>
>Voir [Création d’un workflow transitoire](/help/sites-developing/workflows-models.md#creating-a-transient-workflow) pour plus de détails.

>[!CAUTION]
>
>Lorsqu’un modèle de workflow a été marqué comme transitoire, il y a quelques situations dans lesquelles les informations d’exécution persisteront toujours :
>
>* Le type de charge utile (par exemple, vidéo) nécessite des étapes externes pour le traitement. Dans ce cas, l’historique d’exécution est nécessaire pour la confirmation de l’état.
>* Le workflow entre en **Division ET**. Dans ce cas, l’historique d’exécution est nécessaire pour la confirmation de l’état.
>* Lorsque le workflow transitoire entre dans une étape de participant, il modifie le mode (à l’exécution) en non transitoire, car la tâche est transmise à une personne, l’historique doit persister.

>



>[!CAUTION]
>
>Dans un workflow transitoire, vous ne devriez pas utiliser **Atteindre l’étape**.
>
>La raison en est que **Atteindre l’étape** crée un travail Sling pour continuer le workflow au point `goto`. Cela va à l’encontre du but recherché en rendant le workflow transitoire et génère une erreur dans le fichier journal.
>
>Pour prendre des décisions dans un workflow transitoire, vous pouvez utiliser la **division OU**.

>[!NOTE]
>
>Voir [Meilleures pratiques pour les ressources](/help/assets/performance-tuning-guidelines.md#transient-workflows) pour plus d’informations sur la façon dont les workflows transitoires affectent les performances des ressources.

### Prise en charge multi-ressource {#multi-resource-support}

L’activation de la **prise en charge multi-ressource** pour votre modèle de workflow signifie qu’une seule instance de workflow sera lancée même lorsque vous sélectionnez plusieurs ressources. ils seront joints sous forme de paquet.

Si la **prise en charge multi-ressource** n’est pas activée pour votre modèle de workflow, et si plusieurs ressources sont sélectionnées, une instance de workflow individuelle sera démarrée pour chaque ressource.

>[!NOTE]
>
>Voir [Configuration d’un workflow pour la prise en charge multi-ressource](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support) pour plus de détails.

### Phases de processus {#workflow-stages}

Les phases de processus permettent de visualiser la progression d’un workflow lors de la gestion des tâches. Elles peuvent être utilisées pour fournir un aperçu de la progression du workflow dans le traitement. Lors de l’exécution du workflow, l’utilisateur peut ainsi afficher la progression décrite par la **phase** (par opposition à l’étape individuelle).

Comme les noms des étapes peuvent être spécifiques et techniques, les noms des étapes peuvent être définis pour fournir une vue conceptuelle de la progression du workflow.

Par exemple, pour un workflow avec six étapes et quatre phases :

1. Vous pouvez [configurer les phases de processus (qui indiquent la progression du workflow), puis attribuer la phase appropriée à chaque étape du workflow](/help/sites-developing/workflows-models.md#configuring-workflow-stages-that-show-workflow-progress) :

   * Plusieurs noms de phases peuvent être créés.
   * Un nom de phase individuel est ensuite attribué à chaque étape (un nom de phase peut être attribué à une ou plusieurs étapes).

   | **Nom de l’étape** | **Phase (affectée à l’étape)** |
   |---|---|
   | Étape 1 | Créer |
   | Étape 2 | Créer |
   | Étape 3 | Révision |
   | Étape 4 | Approuver |
   | Étape 5 | Terminé |
   | Étape 6 | Terminé |

1. Lorsque le workflow est exécuté, l’utilisateur peut afficher la progression en fonction des noms des phases (au lieu des noms des étapes). La progression du workflow est affichée dans l’onglet [Informations du processus de la fenêtre Détails de la tâche de l’élément de travail](/help/sites-authoring/workflows-participating.md#opening-a-workflow-item-to-view-details-and-take-actions) répertorié dans la [boîte de réception](/help/sites-authoring/inbox.md).

### workflows et Forms {#workflows-and-forms}

En règle générale, les workflows sont utilisés pour traiter les envois de formulaires dans AEM. Cela peut être avec les [composants principaux des composants de formulaire](https://helpx.adobe.com/experience-manager/core-components/using/form-container.html) disponibles dans une instance d’AEM standard ou avec la [solution AEM Forms](/help/forms/using/aem-forms-workflow.md).

Lors de la création d’un formulaire, l’envoi de ce formulaire peut facilement être associé à un modèle de workflow ; par exemple pour stocker le contenu dans un emplacement précis du référentiel ou pour notifier un utilisateur de l’envoi du formulaire et de son contenu.

### workflows et traduction  {#workflows-and-translation}

Les workflows font également partie intégrante du processus [Traduction](/help/sites-administering/translation.md).
