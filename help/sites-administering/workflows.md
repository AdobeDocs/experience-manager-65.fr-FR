---
title: Administration des workflows
description: Découvrez comment automatiser les activités Adobe Experience Manager à l’aide de workflows.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: 10eecfb8-d43d-4f01-9778-87c752dee64c
solution: Experience Manager, Experience Manager Sites
feature: Operations
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 100%

---

# Administration des workflows{#administering-workflows}

Les workflows vous permettent d’automatiser les activités d’Adobe Experience Manager (AEM). Workflows :

* ils se composent d’une série d’étapes effectuées dans un ordre spécifique.

   * Chaque étape effectue une activité distincte, telle que l’attente de l’entrée d’un utilisateur ou d’une utilisatrice, l’activation d’une page ou l’envoi d’un e-mail.

* Ils peuvent interagir avec des ressources dans le référentiel, les comptes d’utilisateur ou d’utilisatrice et dans les services AEM.
* Peuvent coordonner des activités complexes impliquant n’importe quel aspect d’AEM.

Les workflows d’entreprise que votre organisation a établis peuvent être représentés sous forme de workflows. Par exemple, le workflow de publication de contenu de site web implique généralement des étapes telles que l’approbation et la validation par différents intervenants. Ces processus peuvent être implémentés sous la forme de workflows AEM et appliqués aux pages de contenu et aux ressources.

* [Démarrage d’un workflow](/help/sites-administering/workflows-starting.md)
* [Administration d’instances de workflow](/help/sites-administering/workflows-administering.md)
* [Gestion de l’accès aux workflows](/help/sites-administering/workflows-managing.md)

>[!NOTE]
>
>Pour plus d’informations, consultez :
>
>* Demande de workflow et participation à des workflows : [Utilisation des workflows](/help/sites-authoring/workflows.md).
>* Création de modèles de workflows et extension de la fonctionnalité de workflow : [Développement et extension des workflows](/help/sites-developing/workflows.md).
>* Amélioration des performances des workflows qui utilisent des ressources de serveur importantes : [Traitement de workflows simultanés](/help/sites-deploying/configuring-performance.md#concurrent-workflow-processing).
>

## Modèles de workflow et instances {#workflow-models-and-instances}

Les [modèles de workflow](/help/sites-developing/workflows.md#model) dans AEM sont la représentation et l’implémentation des processus d’entreprise :

* En règle générale, ils agissent sur les pages ou les ressources pour obtenir un résultat spécifique.
* Ces pages et ressources sont appelées payload de workflow.
* Les modèles de workflows se composent d’une série d’étapes exécutant une tâche spécifique.
* La payload est transmise d’une étape à l’autre au fur et à mesure que le workflow progresse.

Lorsqu’un modèle de workflow est démarré (exécuté), une instance de workflow est créée. Les modèles de workflow peuvent être démarrés plusieurs fois, générant à chaque fois une instance de workflow distincte. Pour chaque instance, les étapes définies par le modèle de workflow sont exécutées.

>[!CAUTION]
>
>Les étapes exécutées sont celles définies par le modèle de workflow *au moment où l’instance est générée*. Consultez la section [Développement de workflows](/help/sites-developing/workflows.md#model) pour plus de détails.

Les instances de workflows progressent selon le cycle de vie suivant :

1. Le modèle de workflow est lancé et une instance de workflow est créée et exécutée.

   1. Le payload de l’instance de workflow est identifié lorsque le modèle est démarré.
   1. L’instance est en fait une copie du modèle (au moment de la création).
   1. Les auteurs et autrices et les administrateurs et administratrices AEM ou les services peuvent démarrer des modèles de workflow.

1. La première étape du modèle de workflow est exécutée.
1. L’étape est terminée et le moteur de workflow utilise le modèle pour déterminer la prochaine étape à exécuter.
1. Les étapes suivantes du modèle de workflow sont exécutées et terminées.
1. Une fois la dernière étape terminée, l’instance de workflow est terminée et donc archivée.

De nombreux modèles de workflow utiles sont fournis avec AEM. En outre, les développeurs et développeuses de votre entreprise peuvent créer des modèles de workflow personnalisés, adaptés aux besoins spécifiques de vos processus d’entreprise.

## Étapes du workflow {#workflow-steps}

Lorsque les étapes de workflow sont exécutées, elles sont associées à une instance de workflow. L’historique d’une instance de workflow comprend des informations sur chaque étape exécutée pour l’instance. Ces informations sont utiles pour étudier les problèmes qui se produisent pendant l’exécution.

Un utilisateur ou une utilisatrice ou un service effectue des étapes de workflow, selon le type d’étape :

* Lorsqu’un utilisateur effectue une étape, il est affecté à un élément de travail qui est placé dans sa boîte de réception. La personne est chargée d’exécuter manuellement l’étape afin que l’instance de workflow progresse.
* Lorsqu’un service effectue une étape, une fois l’instance de workflow terminée, elle passe automatiquement à l’étape suivante.

>[!NOTE]
>
>Si une erreur se produit, la mise en œuvre du service/de l’étape doit gérer le comportement pour un scénario d’erreur. Le moteur de workflow lui-même relance la tâche, puis consigne une erreur et arrête l’instance.

## Statut et actions du workflow {#workflow-status-and-actions}

Les workflows peuvent présenter l’un des statuts suivants :

* **EN COURS** : l’instance de workflow est en cours d’exécution.
* **TERMINÉ** : l’instance de workflow s’est terminée correctement.

* **SUSPENDU** : marque le workflow comme suspendu. Toutefois, reportez-vous à la remarque « Attention » ci-dessous portant sur un problème connu avec cet état.
* **ABANDONNÉ** : l’instance de workflow a été arrêtée.
* **PÉRIMÉ** : la progression de l’instance de workflow nécessite l’exécution d’une tâche en arrière-plan, mais la tâche est introuvable dans le système. Cette situation peut se produire lorsqu’une erreur se produit lors de l’exécution du workflow.

>[!NOTE]
>
>Lorsque l’exécution d’une étape de processus se traduit par des erreurs, l’étape apparaît dans la boîte de réception de l’administrateur et le statut du workflow est **EN COURS**.

En fonction du statut actuel, vous pouvez effectuer des actions sur les instances de workflows en cours d’exécution lorsque vous devez intervenir dans la progression normale d’une instance de workflow :

* **Suspendre** ; suspendre un workflow redéfinit son statut sur SUSPENDU. Voir « Attention » ci-dessous :

>[!CAUTION]
>
>Le marquage d’un workflow sur « Suspendu » présente un problème connu. Dans ce statut, il est possible d’agir sur les éléments de workflow suspendus dans une boîte de réception.

* **Reprendre** : redémarre un workflow suspendu à partir du point d’exécution auquel il a été suspendu, en utilisant la même configuration.
* **Arrêter** : arrête l’exécution du workflow et redéfinit son statut sur **ABANDON**. Une instance de workflow abandonnée ne peut pas être redémarrée.
