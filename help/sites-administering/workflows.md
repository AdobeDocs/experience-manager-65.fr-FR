---
title: Administration des workflows
seo-title: Administration des workflows
description: Découvrez comment administrer les workflows dans AEM.
seo-description: Découvrez comment administrer les workflows dans AEM.
uuid: d000a13c-97cb-4b1b-809e-6c3eb0d675e8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 4b09cd44-434e-4834-bc0d-c9c082a4ba5a
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 90%

---


# Administration des workflows{#administering-workflows}

Les workflows vous permettent d’automatiser les activités d’Adobe Experience Manager (AEM). Workflows :

* série d’étapes exécutées dans un ordre donné.

   * Chaque étape effectue une activité distincte (par exemple, attendre la saisie de l’utilisateur, activer une page ou envoyer un message électronique).

* Peuvent interagir avec les ressources dans le référentiel, les comptes d’utilisateur et les services AEM.
* Peuvent coordonner des activités complexes impliquant n’importe quel aspect d’AEM.

Les workflows d’entreprise que votre organisation a établis peuvent être représentés sous forme de workflows. Par exemple, le workflow de publication de contenu de site web implique généralement des étapes telles que l’approbation et la validation par différents intervenants. Ces processus peuvent être mis en œuvre sous la forme de workflows AEM et être appliqués aux pages de contenu et aux ressources.

* [Démarrage de workflows](/help/sites-administering/workflows-starting.md)
* [Administration d’instances de workflow](/help/sites-administering/workflows-administering.md)
* [Gestion de l’accès aux workflows](/help/sites-administering/workflows-managing.md)

>[!NOTE]
>
>Pour plus d’informations, voir :
>
>* Applying and participating in workflows: [Working with Workflows](/help/sites-authoring/workflows.md).
>* Création de modèles de workflows et extension de la fonctionnalité de workflow : [Développement et extension des workflows](/help/sites-developing/workflows.md).
>* Amélioration des performances des workflows qui utilisent des ressources de serveur significatives : [Traitement de workflows simultanés](/help/sites-deploying/configuring-performance.md#concurrent-workflow-processing).

>



## Modèles et instances de workflow {#workflow-models-and-instances}

Les [modèles de workflows](/help/sites-developing/workflows.md#model) dans AEM sont la représentation et la mise en œuvre de processus d’entreprise :

* ils agissent généralement sur les pages ou les ressources pour obtenir un résultat spécifique.
* Ces pages et/ou ressources sont appelées charge utile de workflow.
* Les modèles de workflows se composent d’une série d’étapes exécutant une tâche spécifique.
* La charge utile est transmise d’une étape à l’autre à mesure que le workflow progresse.

Lorsqu’un modèle de workflow est démarré (exécuté), une instance de workflow est créée. Les modèles de workflow peuvent être démarrés plusieurs fois, générant à chaque fois une instance de workflow distincte. Pour chaque instance, les étapes que le modèle de workflow définit sont exécutées.

>[!CAUTION]
>
>Les étapes exécutées sont celles définies par le modèle de workflow *au moment où l’instance est générée*. See [Developing Workflows](/help/sites-developing/workflows.md#model) for further details.

Les instances de flux de travail progressent tout au long du cycle de vie suivant :

1. Le modèle de workflow est lancé et une instance de workflow est créée et exécutée.

   1. La charge utile de l’instance de workflow est identifiée lorsque le modèle est démarré.
   1. Concrètement, l’instance est une copie du modèle (au moment de la création).
   1. Les auteurs, les administrateurs ou les services AEM peuvent démarrer des modèles de workflows.

1. La première étape du modèle de workflow est exécutée.
1. L’étape est terminée et le moteur de workflow utilise le modèle pour déterminer la prochaine étape à exécuter.
1. Les étapes suivantes dans le modèle de workflow sont exécutées et terminées.
1. Lorsque la dernière étape est terminée, l’instance de workflow est terminée et donc archivée.

De nombreux modèles de workflow utiles sont fournis avec AEM. En outre, les développeurs de votre entreprise peuvent créer des modèles de workflows personnalisés, adaptés aux besoins de vos processus d’entreprise.

## Étapes de workflow {#workflow-steps}

Lorsque les étapes de workflow sont exécutées, elles sont associées à une instance de workflow. L’historique d’une instance de workflow comprend des informations sur chaque étape exécutée pour l’instance. Ces informations sont utiles pour examiner les problèmes qui se produisent lors de l’exécution.

Un utilisateur ou un service exécute les étapes de workflow, selon le type d’étape :

* Lorsqu’un utilisateur effectue une étape, il est affecté à un élément de travail qui est placé dans sa boîte de réception. L’utilisateur a la responsabilité d’exécuter manuellement l’étape de sorte que l’instance de workflow progresse.
* Lorsqu’un service effectue une étape, à la fin de cette étape, l’instance de workflow passe automatiquement à l’étape suivante.

>[!NOTE]
>
>Si une erreur se produit, la mise en œuvre du service/de l’étape doit gérer le comportement pour un scénario d’erreur. Le moteur de workflow lui-même relance la tâche, puis consigne une erreur et arrête l’’instance.

## Statut et actions de workflow {#workflow-status-and-actions}

Les workflows peuvent présenter l’un des statuts suivants :

* **EN COURS** : l’instance de workflow est en cours d’exécution.
* **TERMINÉ** : l’instance de workflow s’est terminée correctement.

* **SUSPENDU** : l’instance de workflow a été suspendue.
* **ABANDON** : l’instance de workflow a été arrêtée.
* **PÉRIMÉ** : la progression de l’instance de workflow nécessite l’exécution d’une tâche en arrière-plan, mais la tâche est introuvable dans le système. Cette situation peut se produire lorsqu’une erreur survient pendant l’exécution du workflow.

>[!NOTE]
>
>When the execution of a Process Step results in errors, the step appears in the administrator&#39;s Inbox and the workflow status is **RUNNING**.

En fonction du statut actuel, vous pouvez effectuer des actions sur les instances de workflows en cours d’exécution lorsque vous devez intervenir dans la progression normale d’une instance de workflow :

* **Suspendre** : arrête provisoirement l’exécution du workflow. Cette suspension est utile dans les cas exceptionnels où vous ne souhaitez pas que le workflow se poursuive (par exemple, pour des raisons de maintenance). Suspendre un workflow redéfinit son statut sur SUSPENDU.
* **Reprendre**: Redémarre un flux de travaux suspendu au même point d’exécution où il a été suspendu, en utilisant la même configuration.
* **Arrêter**: Met fin à l’exécution du flux de travail et définit l’état sur **ABORTED**. Une instance de workflow abandonnée ne peut pas être redémarrée.

