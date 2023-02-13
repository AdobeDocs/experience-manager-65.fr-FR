---
title: Démarrage d’un workflow
seo-title: Starting Workflows
description: Découvrez comment démarrer des workflows dans AEM.
seo-description: Learn how to start Workflows in AEM.
uuid: 0648d335-ecce-459d-95fd-3d4d76181b32
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: e9ab4796-a050-40de-b073-af7d33cff009
exl-id: 84a1964c-4121-4763-b946-9eee6093747d
source-git-commit: 2bae11eafb875f01602c39c0dba00a888e11391a
workflow-type: ht
source-wordcount: '794'
ht-degree: 100%

---

# Démarrage d’un workflow{#starting-workflows}

Lors de l’administration des workflows, vous pouvez les démarrer selon différentes méthodes :

* Manuellement :

   * À partir d’un [modèle de workflow](#workflow-models)
   * À l’aide d’un module de workflow pour le [le traitement par lots](#workflow-packages-for-batch-processing)

* Automatiquement :

   * En réponse à des modifications de nœud, [à l’aide d’un lanceur](#workflows-launchers)

>[!NOTE]
>
>D’autres méthodes sont également disponibles pour les créateurs. Pour plus d’informations, voir :
>
>* [Application de workflows aux pages](/help/sites-authoring/workflows-applying.md)
>* [Application de workflows à des ressources de gestion des ressources numériques](/help/assets/assets-workflow.md)
>* [AEM Forms](https://helpx.adobe.com/fr/aem-forms/6-2/aem-workflows-submit-process-form.html)
>* [Projets de traduction](/help/sites-administering/tc-manage.md)
>


## Modèles de workflow {#workflow-models}

Vous pouvez démarrer un workflow [reposant sur l’un des modèles](/help/sites-administering/workflows.md#workflow-models-and-instances) répertoriés dans la console Modèles de workflows. La charge utile constitue les seules informations obligatoires, même s’il est possible d’ajouter également un titre et/ou un commentaire.

## Lanceurs de workflows {#workflows-launchers}

Le lanceur de workflows surveille les modifications du référentiel de contenu pour lancer des workflows en fonction du type d’emplacement et de ressource du nœud modifié.

À l’aide du **Lanceur**, vous pouvez :

* afficher les workflows déjà lancés pour des nœuds spécifiques ;
* sélectionner un workflow à lancer lorsqu’un certain nœud/type de nœud a été créé/modifié/supprimé ;
* supprimer des relations workflow -nœud existantes.

Vous pouvez créer un lanceur sur n’importe quel nœud. Cependant, les modifications apportées à certains nœuds ne lancent pas de workflows. Les modifications apportées à des nœuds sous les chemins d’accès ci-dessous n’entraînent pas le lancement des workflows :

* `/var/workflow/instances`
* Tout nœud workflow-inbox situé n’importe où dans la branche `/home/users`
* `/tmp`
* `/var/audit`
* `/var/classes`
* `/var/eventing`
* `/var/linkchecker`
* `/var/mobile`
* `/var/statistics`

   * Exception : les modifications apportées aux nœuds sous `/var/statistics/tracking` *provoquent* le lancement de workflows.

Différentes définitions sont incluses avec l’installation standard. Elles sont utilisées pour les tâches de gestion des actifs numériques et de collaboration sociale :

![wf-100](assets/wf-100.png)

## Modules de workflow pour le traitement par lots {#workflow-packages-for-batch-processing}

Les modules de workflow sont des modules qui peuvent être transmis à un workflow sous forme de charge utile pour traitement, ce qui permet de traiter plusieurs ressources.

Un module de workflow :

* contient des liens vers un ensemble de ressources (comme des pages ou des ressources) ;
* contient des informations sur les modules, comme la date de création, l’utilisateur qui a créé le module et une brève description ;
* est défini à l’aide d’un modèle de page spécialisé. Ce type de page permet de spécifier les ressources dans le module ;
* peut être utilisé plusieurs fois ;
* peut être modifié par l’utilisateur (ajout ou suppression de ressources) alors que l’instance de workflow est en cours d’exécution.

## Démarrage d’un workflow à partir de la console Modèles {#starting-a-workflow-from-the-models-console}

1. Accédez à la console **Modèles** en sélectionnant **Outils**, **Workflow**, puis **Modèles**.
1. Sélectionnez le workflow (selon la vue de la console). Vous pouvez également utiliser la fonction Rechercher (dans la partie supérieure gauche), si nécessaire :

   ![wf-103](assets/wf-103.png)

   >[!NOTE]
   >
   >L’indicateur **[Transitoire](/help/sites-developing/workflows.md#transient-workflows)** affiche les workflows pour lesquels l’historique des workflows n’est pas conservé.

1. Sélectionnez **Démarrer le workflow** dans la barre d’outils.
1. La boîte de dialogue Exécuter le workflow s’ouvre, d’où vous pouvez spécifier les éléments suivants :

   * **Payload**

      Il peut s’agir d’une page, d’un nœud, d’une ressource, d’un module, entre autres ressources.

   * **Titre**

      Titre facultatif permettant d’identifier cette instance.

   * **Commentaire**

      Commentaire facultatif permettant d’indiquer des détails sur cette instance.
   ![wf-104](assets/wf-104.png)

## Création d’une configuration de lanceur {#creating-a-launcher-configuration}

1. Accédez à la console **Lanceurs de workflow** en sélectionnant **Outils**, **Workflow**, puis **Lanceurs**.
1. Sélectionnez **Créer**, puis **Ajouter un lanceur** pour ouvrir la boîte de dialogue :

   ![wf-105](assets/wf-105.png)

   * **Type d’événement**

      Type d’événement qui lance le workflow :

      * Créé
      * Modifié
      * Supprimé
   * **Type de nœud**

      Type de nœud auquel s’applique le lanceur de workflow.

   * **Chemin**

      Chemin d’accès auquel s’applique le lanceur de workflow.

   * **Mode(s) d’exécution**

      Type de serveur auquel s’applique le lanceur de workflow. Sélectionnez **Auteur**, **Publier** ou **Créer et publier**.

   * **Conditions**

      Liste de conditions pour les valeurs de nœuds qui, lorsqu’elles sont évaluées, déterminent si le workflow est lancé. Par exemple, la condition ci-dessous provoque le lancement du workflow lorsque le nœud possède un nom de propriété avec la valeur Utilisateur :

      name==User

   * **Fonctionnalités**

      Liste des fonctionnalités à activer. Sélectionnez les fonctionnalités nécessaires à l’aide du sélecteur de liste déroulante.

   * **Fonctionnalités désactivées**

   Liste des fonctionnalités à désactiver. Sélectionnez les fonctionnalités nécessaires à l’aide du sélecteur de liste déroulante.

   * **Modèle de workflow**

      Workflow à lancer lorsque le type d’événement se produit sur le type de nœud et/ou au chemin d’accès dans la condition définie.

   * **Description**

      Votre propre texte pour décrire et identifier la configuration du lanceur.

   * **Activer**

      Contrôle si le lanceur de workflow est activé :

      * Sélectionnez **Activer** pour lancer des workflows lorsque des propriétés de configuration sont remplies.
      * Sélectionnez **Désactiver** lorsque le workflow ne doit pas être exécuté (pas même lorsque les propriétés de configuration sont satisfaites).
   * **Exclure la liste**

      Cette option spécifie des événements JCR à exclure (c’est-à-dire à ignorer) lorsque vous déterminez si un workflow doit être déclenché.

      Cette propriété de lanceur est une liste d’éléments séparés par des virgules : ``

      * `property-name` ignore les événements `jcr` déclenchés avec le nom de propriété spécifié. ``
      * `event-user-data:<*someValue*>` ignore tout événement contenant la variable `*<someValue*`> `user-data` défini par le biais de l’API `ObservationManager` [ ](https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/observation/ObservationManager.html#setUserData(java.lang.String.

      Par exemple :

      `jcr:lastModified,dc:modified,dc:format,jcr:lastModifiedBy,imageMap,event-user-data:changedByWorkflowProcess`

      Cette fonctionnalité peut être utilisée pour ignorer les modifications déclenchées par un autre processus de workflow en ajoutant l’élément d’exclusion :

      `event-user-data:changedByWorkflowProcess`





1. Sélectionnez **Créer** pour créer le lanceur et revenir à la console.

   Une fois que l’événement approprié se produit, le lanceur est déclenché et le workflow est démarré.

## Gestion d’une configuration de lanceur {#managing-a-launcher-configuration}

Une fois que vous avez créé la configuration de lanceur, vous pouvez utiliser la même console pour sélectionner l’instance, puis sélectionner **Afficher les propriétés** (et les modifier) ou **Supprimer**.
