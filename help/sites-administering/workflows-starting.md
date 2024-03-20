---
title: Démarrage d’un workflow
description: Découvrez comment administrer des workflows dans Adobe Experience Manager afin de pouvoir les démarrer à l’aide de différentes méthodes, manuellement ou automatiquement.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: 84a1964c-4121-4763-b946-9eee6093747d
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 47%

---

# Démarrage d’un workflow{#starting-workflows}

Lors de l’administration des workflows, vous pouvez les démarrer à l’aide de différentes méthodes :

* Manuellement :

   * Depuis un [Modèle de workflow](#workflow-models).
   * Utilisation d’un module de workflow pour [traitement par lots](#workflow-packages-for-batch-processing).

* Automatiquement :

   * En réponse aux modifications de noeud, [utilisation d’un lanceur](#workflows-launchers).

>[!NOTE]
>
>D’autres méthodes sont également disponibles pour les auteurs. Pour plus d’informations, voir :
>
>* [Application de workflows aux pages](/help/sites-authoring/workflows-applying.md)
>* [Application de workflows à des ressources de gestion des ressources numériques](/help/assets/assets-workflow.md)
>* [AEM Forms](https://helpx.adobe.com/fr/aem-forms/6-2/aem-workflows-submit-process-form.html)
>* [Projets de traduction](/help/sites-administering/tc-manage.md)
>

## Modèles de workflow {#workflow-models}

Vous pouvez démarrer un workflow [reposant sur l’un des modèles](/help/sites-administering/workflows.md#workflow-models-and-instances) répertoriés dans la console Modèles de workflows. La seule information obligatoire est la payload, bien qu’un titre et/ou un commentaire puisse également être ajouté.

## Lanceurs de workflows {#workflows-launchers}

Le lanceur de processus surveille les modifications apportées au référentiel de contenu pour lancer les processus en fonction de l’emplacement et du type de ressource du noeud modifié.

À l’aide du **Lanceur**, vous pouvez :

* Voir les workflows déjà lancés pour des noeuds spécifiques.
* Sélectionnez un workflow à lancer lorsqu’un certain noeud/type de noeud a été créé/modifié/supprimé.
* Supprimez une relation workflow-noeud existante.

Vous pouvez créer un lanceur sur n’importe quel nœud. Cependant, les modifications apportées à certains nœuds ne lancent pas de workflows. Les modifications apportées aux noeuds situés sous les chemins suivants ne provoquent pas le lancement des workflows :

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

Différentes définitions sont incluses avec l’installation standard. Ils sont utilisés pour les tâches de gestion des ressources numériques et de collaboration sociale :

![wf-100](assets/wf-100.png)

## Modules de processus pour le traitement par lots {#workflow-packages-for-batch-processing}

Les modules de workflow sont des modules qui peuvent être transmis à un workflow en tant que charge utile pour le traitement, ce qui permet de traiter plusieurs ressources.

Un module de workflow :

* contient des liens vers un ensemble de ressources (telles que des pages, des ressources).
* contient des informations sur le package, telles que la date de création, l’utilisateur qui a créé le package et une brève description.
* est défini à l’aide d’un modèle de page spécialisé. Ce type de page permet de spécifier les ressources dans le package ;
* peut être utilisé plusieurs fois.
* peut être modifié par l’utilisateur (ajouter ou supprimer des ressources) pendant que l’instance de workflow est en cours d’exécution.

## Démarrage d’un workflow à partir de la console Modèles {#starting-a-workflow-from-the-models-console}

1. Accédez à la console **Modèles** en sélectionnant **Outils**, **Workflow**, puis **Modèles**.
1. Sélectionnez le workflow (en fonction de la vue de la console) ; vous pouvez également utiliser la fonction Rechercher (en haut à gauche) si nécessaire :

   ![wf-103](assets/wf-103.png)

   >[!NOTE]
   >
   >La variable **[Transitoire](/help/sites-developing/workflows.md#transient-workflows)** affiche les workflows pour lesquels l’historique des workflows n’est pas conservé.

1. Sélectionnez **Démarrer le workflow** dans la barre d’outils.
1. La boîte de dialogue Exécuter le processus s’ouvre, vous permettant de spécifier les éléments suivants :

   * **Payload**

     Il peut s’agir d’une page, d’un noeud, d’une ressource, d’un module, etc.

   * **Titre**

     Titre facultatif permettant d’identifier cette instance.

   * **Commentaire**

     Commentaire facultatif permettant d’indiquer des détails sur cette instance.

   ![wf-104](assets/wf-104.png)

## Création d’une configuration de lanceur {#creating-a-launcher-configuration}

1. Accédez à la console **Lanceurs de workflow** en sélectionnant **Outils**, **Workflow**, puis **Lanceurs**.
1. Sélectionner **Créer**, puis **Ajouter un lanceur** pour ouvrir la boîte de dialogue :

   ![wf-105](assets/wf-105.png)

   * **Type d’événement**

     Type d’événement qui lance le workflow :

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

     Liste des fonctionnalités à activer. Sélectionnez les fonctionnalités requises à l’aide du sélecteur de liste déroulante.

   * **Fonctionnalités désactivées**

   Liste des fonctionnalités à désactiver. Sélectionnez les fonctionnalités requises à l’aide du sélecteur de liste déroulante.

   * **Modèle de workflow**

     Workflow à lancer lorsque le type d’événement se produit sur le type de nœud et/ou au chemin d’accès dans la condition définie.

   * **Description**

     Votre propre texte pour décrire et identifier la configuration du lanceur.

   * **Activer**

     Contrôle si le lanceur de workflow est activé :

      * Sélectionner **Activer** pour lancer des workflows lorsque les propriétés de configuration sont satisfaites.
      * Sélectionner **Désactiver** lorsque le workflow ne doit pas s’exécuter (pas même lorsque les propriétés de configuration sont satisfaites).

   * **Exclure la liste**

     Cela spécifie tous les événements JCR à exclure (c’est-à-dire à ignorer) lorsque vous déterminez si un workflow doit être déclenché.

     Cette propriété de lanceur est une liste d’éléments séparés par des virgules : &quot;

      * `property-name` ignore les événements `jcr` déclenchés avec le nom de propriété spécifié. ``
      * `event-user-data:<*someValue*>` ignore tout événement contenant la variable `*<someValue*`> `user-data` défini par le biais de la variable [`ObservationManager` API](https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/observation/ObservationManager.html#setUserData(java.lang.String)).

     Par exemple :

     `jcr:lastModified,dc:modified,dc:format,jcr:lastModifiedBy,imageMap,event-user-data:changedByWorkflowProcess`

     Cette fonctionnalité peut être utilisée pour ignorer les modifications déclenchées par un autre processus de workflow en ajoutant l’élément d’exclusion :

     `event-user-data:changedByWorkflowProcess`

1. Sélectionnez **Créer** pour créer le lanceur et revenir à la console.

   Lorsque l’événement approprié se produit, le lanceur est déclenché et le workflow a démarré.

## Gestion d’une configuration de lanceur {#managing-a-launcher-configuration}

Une fois que vous avez créé la configuration de lanceur, vous pouvez utiliser la même console pour sélectionner l’instance, puis sélectionner **Afficher les propriétés** (et les modifier) ou **Supprimer**.
