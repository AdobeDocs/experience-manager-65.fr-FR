---
title: Workflows basés sur l’utilisation de Forms sur OSGi | Gestion des données utilisateur
description: Workflows basés sur l’utilisation de Forms sur OSGi | Gestion des données utilisateur
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
role: Admin,User
exl-id: fd0e17d7-c3e9-4dec-ad26-ed96a1881f42
solution: Experience Manager, Experience Manager Forms
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '986'
ht-degree: 100%

---

# Workflows basés sur l’utilisation de Forms sur OSGi | Gestion des données utilisateur {#forms-centric-workflows-on-osgi-handling-user-data}

Les workflows d’AEM basés sur Forms vous permettent d’automatiser des processus d’entreprise réels basés sur Forms. Les workflows se composent d’une série d’étapes qui s’exécutent dans un ordre spécifié dans le modèle de workflow associé. Chaque étape exécute une action spécifique, comme affecter une tâche à un utilisateur ou une utilisatrice ou envoyer un e-mail. Les workflows peuvent interagir avec des ressources du référentiel, les comptes d’utilisateurs et d’utilisatrices et les services. Par conséquent, les workflows peuvent coordonner des activités complexes qui impliquent tous les aspects d’Experience Manager.

Les méthodes suivantes permettent de délencher ou de lancer un workflow basé sur Forms :

* Envoi d’une demande depuis la boîte de réception AEM
* Envoi d’une demande depuis l’application AEM [!DNL Forms]
* Envoi d’un formulaire adaptatif
* Utiliser un dossier de contrôle
* Envoi d’une communication interactive ou d’une lettre

Pour plus d’informations sur les workflows et les fonctionnalités d’AEM basés sur Forms, voir [Workflow basé sur Forms sur OSGi](/help/forms/using/aem-forms-workflow.md).

## Données utilisateur et stockage de données {#user-data-and-data-stores}

Le déclenchement d’un workflow entraîne la génération automatique d’une payload pour l’instance de workflow. Chaque instance de workflow se voit attribuer un ID d’instance unique et un ID de payload associé. La payload contient les emplacements de référentiel pour les données utilisateur et de formulaire associées à une instance de workflow. Les brouillons et les données historiques d’une instance de workflow sont également stockés dans le référentiel AEM.

Les emplacements de référentiel par défaut où se trouvent la payload, les brouillons et l’historique d’une instance de workflow sont les suivants :

>[!NOTE]
>
>Vous pouvez configurer différents emplacements pour stocker la payload, les brouillons et les données historiques lors de la création d’un workflow ou d’une application. Examinez le workflow ou l’application pour identifier les emplacements où les données ont été stockées.

<table>
 <tbody>
  <tr>
   <td> </td>
   <td><b>AEM 6.4 [!DNL Forms]</b></td>
   <td><b>AEM 6.3 [!DNL Forms]</b></td>
  </tr>
  <tr>
   <td><strong>Instance <br /> de workflow</strong></td>
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
   <td>/var/fd/dashboard/instances/[server_id]/<br /> [date]/[workflow-instance]/draft/[workitem]/</td>
   <td>/etc/fd/dashboard/instances/[server_id]/<br /> [date]/[workflow-instance]/draft/[workitem]/</td>
  </tr>
  <tr>
   <td><strong>Historique</strong></td>
   <td>/var/fd/dashboard/instances/[server_id]/<br /> [date]/[instance_de_workflow]/history/</td>
   <td>/etc/fd/dashboard/instances/[server_id]/<br /> [date]/[workflow_instance]/history/</td>
  </tr>
 </tbody>
</table>

## Accès et suppression des données utilisateur {#access-and-delete-user-data}

Vous pouvez accéder aux données utilisateur et les supprimer d’une instance de workflow dans le référentiel. Pour cela, vous devez connaître l’ID de l’instance de workflow associé à l’utilisateur ou l’utilisatrice. Vous pouvez rechercher l’ID d’instance d’une instance de workflow à l’aide du nom de l’utilisateur ou de l’utilisatrice qui a initié l’instance de workflow ou qui est la personne désignée actuelle de l’instance de workflow.

Toutefois, dans les scénarios suivants d’identification des workflows associés à un initiateur ou une initiatrice, l’identification peut échouer ou les résultats peuvent être ambigus :

* **Workflow déclenché par un dossier de contrôle** : il est impossible d’identifier une instance de workflow à l’aide de son initiateur ou initiatrice si le workflow est déclenché par un dossier de contrôle. Dans ce cas, les informations utilisateur sont codées dans les données stockées.
* **Workflow initié à partir de l’instance de publication AEM** : toutes les instances de workflow sont créées à l’aide d’un utilisateur de service lorsque les formulaires adaptatifs, les communications interactives ou les lettres sont envoyés depuis l’instance de publication AEM. Dans ce cas, le nom d’utilisateur de la personne connectée n’est pas capturé dans les données de l’instance de workflow.

### Accès aux données utilisateur {#access}

Pour identifier et accéder aux données utilisateur stockées pour une instance de workflow, procédez comme suit :

1. Sur l’instance d’auteur AEM, accédez à `https://'[server]:[port]'/crx/de` puis à **[!UICONTROL Outils > Requête]**.

   Sélectionnez **[!UICONTROL SQL2]** dans le menu déroulant **[!UICONTROL Type]**.

1. Selon les informations disponibles, exécutez l’une des requêtes suivantes :

   * Exécutez les opérations suivantes si vous connaissez l’initiateur ou l’initiatrice du workflow :

   `SELECT &ast; FROM [cq:Workflow] AS s WHERE ISDESCENDANTNODE([path-to-workflow-instances]) and s.[initiator]='*initiator-ID*'`

   * Exécutez la commande suivante si l’utilisateur des données que vous recherchez est actuellement la personne à laquelle le workflow est assigné :

   `SELECT &ast; FROM [cq:WorkItem] AS s WHERE ISDESCENDANTNODE([path-to-workflow-instances]) and s.[assignee]='*assignee-id*'`

   La requête renvoie l’emplacement de toutes les instances de workflow de l’initiateur de workflow spécifié ou de la personne à laquelle le workflow est actuellement assigné.

   Par exemple, la requête suivante renvoie le chemin d’accès de deux instances de workflow du nœud `/var/workflow/instances` pour lequel l’initiateur du workflow est `srose`.

   ![instance de workflow](assets/workflow-instance.png)

1. Accédez au chemin d’une instance de workflow renvoyé par la requête. La propriété Statut affiche le statut actuel de l’instance de workflow.

   ![status](assets/status.png)

1. Dans le nœud de l’instance de workflow, accédez à `data/payload/`. La propriété `path` enregistre le chemin de la charge utile de l’instance de workflow. Vous pouvez accéder au chemin d’accès des données stockées dans la charge utile.

   ![chemin_d’accès-charge_utile](assets/payload-path.png)

1. Accédez aux emplacements des brouillons et de l’historique de l’instance de workflow.

   Par exemple :

   `/var/fd/dashboard/instances/server0/2018-04-09/_var_workflow_instances_server0_2018-04-09_basicmodel_54/draft/`

   `/var/fd/dashboard/instances/server0/2018-04-09/_var_workflow_instances_server0_2018-04-09_basicmodel_54/history/`

1. Répétez les étapes 3 à 5 pour toutes les instances de workflow renvoyées par la requête à l’étape 2.

   >[!NOTE]
   >
   >L’application AEM [!DNL Forms] stocke également les données en mode hors ligne. Les données d’une instance de workflow peuvent être enregistrées localement sur des appareils individuels et envoyées au serveur lorsque l’application se synchronise avec le serveur.[!DNL Forms]

### Suppression de données utilisateur {#delete-user-data}

Vous devez être administrateur ou administratrice AEM pour supprimer les données utilisateur des instances de workflow de la manière suivante :

1. Suivez les instructions de la section [Accès aux données utilisateur](/help/forms/using/forms-workflow-osgi-handling-user-data.md#access) et notez ce qui suit :

   * Chemins d’accès aux instances de workflow associées à l’utilisateur ou à l’utilisatrice
   * Statut des instances de workflow
   * Chemins d’accès aux payloads des instances de workflow
   * Chemins d’accès aux brouillons et à l’historique des instances de workflow

1. Effectuez cette étape pour des instances de workflow à l’état **EN COURS**,**SUSPENDU** ou **** OBSOLÈTE :

   1. Accédez à `https://'[server]:[port]'/aem/start.html` et connectez-vous avec les informations d’identification de l’administrateur.
   1. Accédez à **[!UICONTROL Outils > Workflow > Instances]**.
   1. Sélectionnez les instances de workflow appropriées pour l’utilisateur ou l’utilisatrice et sélectionnez **[!UICONTROL Arrêter]** pour arrêter les instances en cours d’exécution.

      Pour plus d’informations sur l’utilisation des instances de workflow, voir [Gestion des instances de workflow](/help/sites-administering/workflows-administering.md).

1. Accédez à la console [!DNL CRXDE Lite], puis au chemin d’accès de la charge utile d’une instance de workflow et supprimez le nœud `payload`.
1. Accédez au chemin d’accès des brouillons d’une instance de workflow et supprimez le nœud `draft`.
1. Accédez au chemin d’accès de l’historique d’une instance de workflow et supprimez le nœud `history`.
1. Accédez au chemin d’accès d’une instance de workflow et supprimez le nœud `[workflow-instance-ID]` du workflow.

   >[!NOTE]
   >
   >La suppression de l’instancier de workflow supprime l’instance de workflow pour tous les participantes et participants au workflow.

1. Répétez les étapes 2 à 6 pour toutes les instances de workflow identifiées pour un utilisateur ou une utilisatrice.
1. Identifiez et supprimez les données de brouillon et d’envoi hors ligne dans la boîte d’envoi de l’application AEM [!DNL Forms] des participants au workflow afin d’éviter tout envoi au serveur.

Vous pouvez également utiliser des API pour accéder aux nœuds et propriétés et les supprimer. Consultez la documentation suivante pour en savoir plus.

* [Comment accéder au JCR AEM par programmation](/help/sites-developing/access-jcr.md)
* [Suppression des nœuds et propriétés](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/10_Writing.html#10.9%20Removing%20Nodes%20and%20Properties)
* [Guide de référence des API](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=fr)
