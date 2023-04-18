---
title: Flux de travail basé sur l’utilisation de Forms sur OSGi | Gestion des données utilisateur
seo-title: Forms-centric workflows on OSGi | Handling user data
description: Flux de travail basé sur l’utilisation de Forms sur OSGi | Gestion des données utilisateur
uuid: 6eefbe84-6496-4bf8-b065-212aa50cd074
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9f400560-8152-4d07-a946-e514e9b9cedf
role: Admin
exl-id: fd0e17d7-c3e9-4dec-ad26-ed96a1881f42
source-git-commit: fb9363a39ffc9d3929a31a3a19a124b806607ef4
workflow-type: tm+mt
source-wordcount: '1005'
ht-degree: 36%

---

# Flux de travail basé sur l’utilisation de Forms sur OSGi | Gestion des données utilisateur {#forms-centric-workflows-on-osgi-handling-user-data}

Les workflows d’AEM centrés sur Forms vous permettent d’automatiser des processus d’entreprise basés sur l’utilisation de Forms. Les workflows se composent d’une série d’étapes qui s’exécutent dans un ordre spécifié dans le modèle de workflow associé. Chaque étape exécute une action spécifique, comme affecter une tâche à un utilisateur ou envoyer un message électronique. Les workflows peuvent interagir avec des ressources dans le référentiel, les comptes d’utilisateurs et les services. Par conséquent, les workflows peuvent coordonner des activités complexes qui impliquent tous les aspects du Experience Manager.

Un processus basé sur l’utilisation de formulaires peut être déclenché ou lancé par l’une des méthodes suivantes :

* Envoi d’une demande depuis la boîte de réception AEM
* Envoi d’une demande depuis l’application AEM [!DNL Forms]
* Envoi d’un formulaire adaptatif
* Utilisation d’un dossier de contrôle
* Envoi d’une communication interactive ou d’une lettre

Pour plus d’informations sur les workflows et les fonctionnalités Forms AEM, voir [Processus centré sur Forms sur OSGi](/help/forms/using/aem-forms-workflow.md).

## Données utilisateur et stockage de données {#user-data-and-data-stores}

Lorsqu’un workflow est déclenché, une payload est automatiquement générée pour l’instance de workflow. Chaque instance de workflow se voit attribuer un ID d’instance unique et un ID de charge utile associé. La payload contient les emplacements de référentiel pour les données utilisateur et de formulaire associées à une instance de workflow. En outre, les brouillons et les données historiques d’une instance de workflow sont également stockés dans le référentiel AEM.

Les emplacements de référentiel par défaut où résident la charge utile, les brouillons et l’historique d’une instance de workflow sont les suivants :

>[!NOTE]
>
>Vous pouvez configurer différents emplacements pour stocker les données de charge utile, de brouillon et d’historique lors de la création d’un workflow ou d’une application. Pour identifier les emplacements où un workflow ou une application a stocké des données, passez en revue le workflow.

<table>
 <tbody>
  <tr>
   <td> </td>
   <td><b>AEM 6.4 [!DNL Forms]</b></td>
   <td><b>AEM 6.3 [!DNL Forms]</b></td>
  </tr>
  <tr>
   <td><strong>Instance <br /> de flux de travail</strong></td>
   <td>/var/workflow/instances/[server_id]/&lt;date&gt;/[workflow-instance]/</td>
   <td>/etc/workflow/instances/[server_id]/[date]/[workflow-instance]/</td>
  </tr>
  <tr>
   <td><strong>Charge utile</strong></td>
   <td>/var/fd/dashboard/payload/[server_id]/[date]/<br /> [payload-id]/</td>
   <td>/etc/fd/dashboard/payload/[server_id]/[date]/<br /> [payload-id]/</td>
  </tr>
  <tr>
   <td><strong>Brouillons</strong></td>
   <td>/var/fd/dashboard/instances/[server_id]/<br /> [date]/[instance-workflow]/draft/[élément-travail]/</td>
   <td>/etc/fd/dashboard/instances/[server_id]/<br /> [date]/[instance-workflow]/draft/[élément-travail]/</td>
  </tr>
  <tr>
   <td><strong>Historique</strong></td>
   <td>/var/fd/dashboard/instances/[server_id]/<br /> [date]/[instance_de_workflow]/history/</td>
   <td>/etc/fd/dashboard/instances/[server_id]/<br /> [date]/[instance_de_workflow]/history/</td>
  </tr>
 </tbody>
</table>

## Accès et suppression des données utilisateur {#access-and-delete-user-data}

Vous pouvez accéder aux données utilisateur et les supprimer d’une instance de workflow dans le référentiel. Pour ce faire, vous devez connaître l’ID d’instance de workflow associé à l’utilisateur. Vous pouvez rechercher l’ID d’instance d’une instance de workflow à l’aide du nom d’utilisateur de l’instance de workflow qui a initié l’instance ou qui est la personne désignée actuelle de l’instance de workflow.

Cependant, vous ne pouvez pas identifier ou les résultats peuvent être ambigus lors de l’identification des workflows associés à un initiateur dans les scénarios suivants :

* **Workflow déclenché par un dossier de contrôle**: Une instance de workflow ne peut pas être identifiée à l’aide de son initiateur si le workflow est déclenché par un dossier de contrôle. Dans ce cas, les informations utilisateur sont codées dans les données stockées.
* **Workflow lancé à partir de l’instance de publication AEM**: Toutes les instances de workflow sont créées à l’aide d’un utilisateur de service lorsque des formulaires adaptatifs, des communications interactives ou des lettres sont envoyés à partir de l’instance de publication AEM. Dans ce cas, le nom d’utilisateur de l’utilisateur connecté n’est pas capturé dans les données de l’instance de workflow.

### Accès aux données utilisateur {#access}

Pour identifier et accéder aux données utilisateur stockées pour une instance de flux de travail, procédez comme suit :

1. Sur l’instance d’auteur AEM, accédez à `https://'[server]:[port]'/crx/de` puis à **[!UICONTROL Outils > Requête]**.

   Sélectionner **[!UICONTROL SQL2]** de la **[!UICONTROL Type]** menu déroulant.

1. Selon les informations disponibles, exécutez l’une des requêtes suivantes :

   * Exécutez les opérations suivantes si l’initiateur du workflow est connu :

   `SELECT &ast; FROM [cq:Workflow] AS s WHERE ISDESCENDANTNODE([path-to-workflow-instances]) and s.[initiator]='*initiator-ID*'`

   * Exécutez la commande suivante si l’utilisateur des données que vous recherchez est actuellement la personne à laquelle le flux de travail est assigné :

   `SELECT &ast; FROM [cq:WorkItem] AS s WHERE ISDESCENDANTNODE([path-to-workflow-instances]) and s.[assignee]='*assignee-id*'`

   La requête renvoie l’emplacement de toutes les instances de flux de travail de l’initiateur de flux de travail spécifié ou de la personne à laquelle le flux de travail est actuellement assigné.

   Par exemple, la requête suivante renvoie le chemin d’accès de deux instances de flux de travail du nœud `/var/workflow/instances` pour lequel l’initiateur du flux de travail est `srose`.

   ![instance de flux de travail](assets/workflow-instance.png)

1. Accédez au chemin d’une instance de workflow renvoyée par la requête. La propriété status affiche l’état actuel de l’instance de workflow.

   ![status](assets/status.png)

1. Dans le nœud de l’instance de flux de travail, accédez à `data/payload/`. La propriété `path` enregistre le chemin de la charge utile de l’instance de flux de travail. Vous pouvez accéder au chemin d’accès des données stockées dans la charge utile.

   ![chemin_d’accès-charge_utile](assets/payload-path.png)

1. Accédez aux emplacements des brouillons et de l’historique de l’instance de workflow.

   Par exemple :

   `/var/fd/dashboard/instances/server0/2018-04-09/_var_workflow_instances_server0_2018-04-09_basicmodel_54/draft/`

   `/var/fd/dashboard/instances/server0/2018-04-09/_var_workflow_instances_server0_2018-04-09_basicmodel_54/history/`

1. Répétez les étapes 3 à 5 pour toutes les instances de flux de travail renvoyées par la requête à l’étape 2.

   >[!NOTE]
   >
   >L’application AEM [!DNL Forms] stocke également les données en mode hors ligne. Les données d’une instance de flux de travail peuvent être enregistrées localement sur des appareils individuels et envoyées au serveur lorsque l’application se synchronise avec le serveur.[!DNL Forms]

### Suppression de données utilisateur {#delete-user-data}

Vous devez être un administrateur AEM pour supprimer les données utilisateur des instances de workflow en procédant comme suit :

1. Suivez les instructions de la section [Accès aux données utilisateur](/help/forms/using/forms-workflow-osgi-handling-user-data.md#access) et notez ce qui suit :

   * Chemins d’accès aux instances de workflow associées à l’utilisateur
   * État des instances de workflow
   * Chemins d’accès aux payloads pour les instances de workflow
   * Chemins vers les brouillons et l’historique pour les instances de workflow

1. Effectuez cette étape pour des instances de flux de travail à l’état **EN COURS**,**SUSPENDU** ou **** OBSOLÈTE :

   1. Accédez à `https://'[server]:[port]'/aem/start.html` et connectez-vous avec les informations d’identification de l’administrateur.
   1. Accédez à **[!UICONTROL Outils > Workflow > Instances]**.
   1. Sélectionnez les instances de workflow appropriées pour l’utilisateur et appuyez sur **[!UICONTROL Arrêter]** pour arrêter les instances en cours d’exécution.

      Pour plus d’informations sur l’utilisation des instances de flux de travail, voir [Gestion des instances de flux de travail](/help/sites-administering/workflows-administering.md).

1. Accédez à la console [!DNL CRXDE Lite], puis au chemin d’accès de la charge utile d’une instance de flux de travail et supprimez le nœud `payload`.
1. Accédez au chemin d’accès des brouillons d’une instance de flux de travail et supprimez le nœud `draft`.
1. Accédez au chemin d’accès de l’historique d’une instance de flux de travail et supprimez le nœud `history`.
1. Accédez au chemin d’accès d’une instance de flux de travail et supprimez le nœud `[workflow-instance-ID]` du flux de travail.

   >[!NOTE]
   >
   >La suppression du noeud d’instance de workflow supprime l’instance de workflow pour tous les participants au workflow.

1. Répétez les étapes 2 à 6 pour toutes les instances de workflow identifiées pour un utilisateur.
1. Identifiez et supprimez les données de brouillon et d’envoi hors ligne dans la boîte d’envoi de l’application AEM [!DNL Forms] des participants au flux de travail afin d’éviter tout envoi au serveur.

Vous pouvez également utiliser des API pour accéder aux noeuds et propriétés et les supprimer. Pour plus d’informations, consultez la documentation suivante.

* [Comment accéder au JCR AEM par programmation](/help/sites-developing/access-jcr.md)
* [Suppression des nœuds et propriétés](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/10_Writing.html#10.9%20Removing%20Nodes%20and%20Properties)
* [Guide de référence des API](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=fr)
