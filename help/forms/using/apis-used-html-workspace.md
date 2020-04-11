---
title: API utilisées dans l’espace de travail AEM Forms
seo-title: API utilisées dans l’espace de travail AEM Forms
description: API Public Java et JavaScript et méthodes de l’espace de travail LiveCycle AEM Forms exposées pour la personnalisation et l’automatisation.
seo-description: API Public Java et JavaScript et méthodes de l’espace de travail LiveCycle AEM Forms exposées pour la personnalisation et l’automatisation.
uuid: 9602990e-8ac7-42eb-b507-50b3594055ba
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 4a73a973-fccf-466b-b4a0-47652a14a080
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# API utilisées dans l’espace de travail AEM Forms {#apis-used-in-aem-forms-workspace}

Les API suivantes sont utilisées dans l’espace de travail AEM Forms.

<table>
 <tbody>
  <tr>
   <td><strong>Méthode JavaScript</strong></td>
   <td><strong>Nom du service</strong></td>
   <td><strong>Nom de l’API</strong></td>
   <td><strong>Commentaires</strong></td>
  </tr>
  <tr>
   <td>getGroups</td>
   <td>ProcessManagementUserProxyService</td>
   <td>getGroups</td>
   <td>Elle recherche des groupes. Si aucune précision n’est fournie, elle renvoie une liste de tous les groupes. Sinon, elle renvoie les groupes portant le nom précisé.</td>
  </tr>
  <tr>
   <td>getUsersAndGroups</td>
   <td>ProcessManagementUserProxyService</td>
   <td>getUsersAndGroups</td>
   <td>Elle recherche des utilisateurs et des groupes. Si aucune précision n’est fournie, elle renvoie une liste de tous les utilisateurs et groupes. Sinon, elle renvoie les utilisateurs et les groupes portant le nom précisé.</td>
  </tr>
  <tr>
   <td>prepareForSubmit</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>prepareForSubmit</td>
   <td>Elle est appelée avant l’envoi du formulaire via DocumentSubmitServlet. Elle définit l’ID de la tâche dans une variable de session (avec le délai d’expiration) qui est récupérée lors de l’envoi réel.</td>
  </tr>
  <tr>
   <td>submitTask</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>submit</td>
   <td>Elle envoie l’objet document associé à la tâche (et soumet ainsi le processus).</td>
  </tr>
  <tr>
   <td>getRootEndpointCategories</td>
   <td>ProcessManagementStartpointService</td>
   <td>getRootEndpointCategories</td>
   <td>Elle récupère toutes les catégories racines présentes sur le serveur.</td>
  </tr>
  <tr>
   <td>getDirectChildCategories</td>
   <td>ProcessManagementStartpointService</td>
   <td>getDirectChildCategories2</td>
   <td>Elle récupère tous les enfants directs d’une catégorie.</td>
  </tr>
  <tr>
   <td>getAllStartpoints</td>
   <td>ProcessManagementStartpointService</td>
   <td>getAllStartpoints</td>
   <td>Elle récupère tous les points de départ présents sur le serveur sous toutes les catégories.</td>
  </tr>
  <tr>
   <td>invokeStartpoint</td>
   <td>ProcessManagementStartpointService</td>
   <td>invokeStartpoint</td>
   <td>Elle appelle un point de départ et crée une nouvelle tâche correspondant à ce point.</td>
  </tr>
  <tr>
   <td>getAllTasks</td>
   <td>ProcessManagementTaskService</td>
   <td>getAllActionableTasks</td>
   <td>Elle récupère toutes les tâches qui sont créées et transférées ou consultées, enregistrées, affectées, affectées et enregistrées pour un utilisateur connecté.</td>
  </tr>
  <tr>
   <td>getTask</td>
   <td>ProcessManagementTaskService</td>
   <td>getTask</td>
   <td>Elle récupère une tâche spécifique.</td>
  </tr>
  <tr>
   <td>renderTask</td>
   <td>ProcessManagementTaskService</td>
   <td>render</td>
   <td>Elle génère une tâche et renvoie les informations requises pour générer le formulaire comme l’URL du formulaire, le type de formulaire, l’URL des données si nécessaire, etc.</td>
  </tr>
  <tr>
   <td>submitWithPriorData</td>
   <td>ProcessManagementTaskService</td>
   <td>submitWithPriorData</td>
   <td>Elle renvoie le résultat de l’API d’envoi de TaskManager à l’aide de la clé de résultat.</td>
  </tr>
  <tr>
   <td>submitWithData</td>
   <td>ProcessManagementTaskService</td>
   <td>submitWithData</td>
   <td>Elle envoie les données du formulaire (transmises en tant que chaîne) associées à la tâche à l’aide de l’API d’envoi de TaskManager. Elle est utilisée pour les formulaires Flex qui n’appellent pas l’API d’envoi de TaskManager.</td>
  </tr>
  <tr>
   <td>save</td>
   <td>ProcessManagementTaskService</td>
   <td>save</td>
   <td>Elle enregistre une tâche sur le serveur.</td>
  </tr>
  <tr>
   <td>complete</td>
   <td>ProcessManagementTaskService</td>
   <td>complete</td>
   <td>Elle termine une tâche qui est transmise à l’étape suivante conformément à la conception du processus.</td>
  </tr>
  <tr>
   <td>getAttachment</td>
   <td>ProcessManagementTaskService</td>
   <td>getAttachment</td>
   <td>Elle renvoie l’URL d’une pièce jointe où la pièce jointe est disponible.</td>
  </tr>
  <tr>
   <td>getAllAttachments</td>
   <td>ProcessManagementTaskService</td>
   <td>getAllActionableAttachments</td>
   <td>Elle récupère toutes les pièces jointes et notes d’une tâche.</td>
  </tr>
  <tr>
   <td>réseau </td>
   <td>ProcessManagementTaskService</td>
   <td>réseau </td>
   <td>Elle partage une tâche avec un autre utilisateur. Un autre utilisateur peut demander la tâche et devient le propriétaire de la tâche.</td>
  </tr>
  <tr>
   <td>forward</td>
   <td>ProcessManagementTaskService</td>
   <td>forward</td>
   <td>Elle transfère une tâche à un autre utilisateur.</td>
  </tr>
  <tr>
   <td>consult</td>
   <td>ProcessManagementTaskService</td>
   <td>consult</td>
   <td>Elle consulte une tâche avec un autre utilisateur.</td>
  </tr>
  <tr>
   <td>claim</td>
   <td>ProcessManagementTaskService</td>
   <td>claim</td>
   <td>Elle demande une tâche disponible dans la file d’attente partagée.</td>
  </tr>
  <tr>
   <td>unlock</td>
   <td>ProcessManagementTaskService</td>
   <td>unlock</td>
   <td>Elle déverrouille une tâche.</td>
  </tr>
  <tr>
   <td>lock</td>
   <td>ProcessManagementTaskService</td>
   <td>lock</td>
   <td>Elle verrouille une tâche ; la tâche ne peut plus être demandée par un autre utilisateur si elle est partagée.</td>
  </tr>
  <tr>
   <td>de refuser ;</td>
   <td>ProcessManagementTaskService</td>
   <td>de refuser ;</td>
   <td>Elle renvoie la tâche au propriétaire précédent de la tâche.</td>
  </tr>
  <tr>
   <td>abandon</td>
   <td>ProcessManagementTaskService</td>
   <td>abandon</td>
   <td>Elle supprime une tâche.</td>
  </tr>
  <tr>
   <td>setVisibility</td>
   <td>ProcessManagementTaskService</td>
   <td>setVisibility</td>
   <td>Elle définit la visibilité d’une tâche. Si la visibilité est définie sur la valeur false, l’utilisateur ne pourra pas voir la tâche ultérieurement.</td>
  </tr>
  <tr>
   <td>getUsers</td>
   <td>ProcessManagementUserProxyService</td>
   <td>getUsers</td>
   <td>Elle est utilisée pour rechercher des utilisateurs. Elle renvoie tous les utilisateurs si aucun nom n’est spécifié, sinon, elle renvoie les utilisateurs avec le nom spécifié.</td>
  </tr>
  <tr>
   <td>getUsersInGroup</td>
   <td>ProcessManagementUserProxyService</td>
   <td>getUsersInGroupByName</td>
   <td>Elle renvoie tous les utilisateurs appartenant à un groupe.</td>
  </tr>
  <tr>
   <td>grantQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>grantQueueAccess</td>
   <td>Elle autorise l’accès de la file d’attente de l’utilisateur connecté à l’utilisateur spécifié. Il s’agit d’un partage de base de sa propre file d’attente avec un autre utilisateur.</td>
  </tr>
  <tr>
   <td>requestQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>requestQueueAccess</td>
   <td>Elle exécute une requête d’accès à la file d’attente de l’utilisateur spécifié pour un utilisateur connecté. Si l’utilisateur approuve la requête, la file d’attente de l’utilisateur est partagée avec l’utilisateur connecté.</td>
  </tr>
  <tr>
   <td>getGrantedUsers</td>
   <td>ProcessManagementQueueService</td>
   <td>getGrantedUsers</td>
   <td>Elle renvoie tous les utilisateurs qui ont accès à la file d’attente de l’utilisateur connecté.</td>
  </tr>
  <tr>
   <td>getUsersForAccessibleQueues</td>
   <td>ProcessManagementQueueService</td>
   <td>getUsersForAccessibleQueues</td>
   <td>Elle renvoie tous les utilisateurs dont la file d’attente est accessible à un utilisateur.</td>
  </tr>
  <tr>
   <td>revokeQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>revokeQueueAccess</td>
   <td>Elle supprime un utilisateur de la liste des utilisateurs qui ont accès à la file d’attente de l’utilisateur connecté.</td>
  </tr>
  <tr>
   <td>removeQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>removeQueueAccess</td>
   <td>Elle supprime l’utilisateur de la liste des utilisateurs dont la file d’attente est accessible à l’utilisateur connecté.</td>
  </tr>
  <tr>
   <td>getAllQueues<br /> </td>
   <td>ProcessManagementQueueService<br /> </td>
   <td>getAllQueues<br /> </td>
   <td>Elle octroie un accès à l’utilisateur connecté à toutes les files d’attente (propres, partagées et files d’attente de groupe).<br /> </td>
  </tr>
  <tr>
   <td>getOutOfOfficeSettings</td>
   <td>ProcessManagementOutOfOfficeService</td>
   <td>getOutOfOfficeSettings</td>
   <td>Elle récupère les paramètres d’absence du bureau d’un utilisateur.</td>
  </tr>
  <tr>
   <td>saveOutOfOfficeSettingsJson</td>
   <td>ProcessManagementOutOfOfficeService</td>
   <td>saveOutOfOfficeSettingsJson</td>
   <td>Elle enregistre les paramètres d’absence du bureau d’un utilisateur.</td>
  </tr>
  <tr>
   <td>getAllProcesses</td>
   <td>ProcessManagementProcessService</td>
   <td>getAllProcesses</td>
   <td>Elle renvoie la liste de tous les processus.</td>
  </tr>
  <tr>
   <td>getParticipatedProcesses</td>
   <td>ProcessManagementProcessService</td>
   <td>getParticipatedProcesses</td>
   <td>Elle renvoie la liste de tous les noms de processus auxquels participe l’utilisateur connecté.</td>
  </tr>
  <tr>
   <td>getProcessInstance<br /> </td>
   <td>ProcessManagementProcessService<br /> </td>
   <td>getProcessInstance<br /> </td>
   <td>Elle récupère les détails d’une instance de processus.<br /> </td>
  </tr>
  <tr>
   <td>getProcessInstances</td>
   <td>ProcessManagementQueryService</td>
   <td>getProcessInstances</td>
   <td>Elle récupère toutes les instances de processus d’un processus.</td>
  </tr>
  <tr>
   <td>getPendingTasksForProcessInstance</td>
   <td>ProcessManagementQueryService</td>
   <td>getPendingTasksForProcessInstance</td>
   <td>Elle récupère les tâches en attente d’une instance de processus.</td>
  </tr>
  <tr>
   <td>getTasksForProcessInstance</td>
   <td>ProcessManagementQueryService</td>
   <td>getTasksForProcessInstance</td>
   <td>Elle récupère toutes les tâches d’une instance de processus.</td>
  </tr>
  <tr>
   <td>getAllSearchTemplates</td>
   <td>ProcessManagementQueryService</td>
   <td>getAllSearchTemplates</td>
   <td>Elle renvoie la liste de tous les modèles de recherche.</td>
  </tr>
  <tr>
   <td>getTemplate</td>
   <td>ProcessManagementQueryService</td>
   <td>getTemplate</td>
   <td>Elle renvoie le contenu d’un modèle de recherche.</td>
  </tr>
  <tr>
   <td>findTasksJson<br /> </td>
   <td>ProcessManagementQueryService</td>
   <td>findTasksJson</td>
   <td>Elle recherche et renvoie toutes les tâches qui répondent à toutes les conditions d’un modèle de recherche.</td>
  </tr>
  <tr>
   <td>getAssignmentsForTask</td>
   <td>ProcessManagementTaskService</td>
   <td>getAssignmentsForTask</td>
   <td>Elle récupère toutes les affectations d’une tâche. Par ex. : si l’utilisateur transfère ou consulte une tâche d’un autre utilisateur, il s’agit de l’affectation d’une tâche.</td>
  </tr>
  <tr>
   <td>deleteAttachment </td>
   <td>TaskManagerService</td>
   <td>deleteAttachment</td>
   <td>Elle supprime une pièce jointe.</td>
  </tr>
  <tr>
   <td>initialize</td>
   <td>ProcessManagementClientSessionService</td>
   <td>initialize</td>
   <td>Elle renouvelle l’assertion, si nécessaire. L’utilisateur s’authentifie. Définit les paramètres de session des informations relatives au serveur/client. Renvoie les informations relatives à l’utilisateur et l’intervalle d’interrogation.</td>
  </tr>
  <tr>
   <td>getTasksForDirectReports</td>
   <td>ProcessManagementTeamTasksService</td>
   <td>getTasksForDirectReports</td>
   <td>Elle renvoie toutes les tâches de rapports directs du gestionnaire connecté.</td>
  </tr>
  <tr>
   <td>getTaskOfDirectReport<br /> </td>
   <td>ProcessManagementTeamTasksService</td>
   <td>getDirectReportTask</td>
   <td>Elle renvoie la tâche de rapport direct spécifié du gestionnaire connecté.</td>
  </tr>
  <tr>
   <td>forwardTaskOfDirectReport</td>
   <td>ProcessManagementTeamTasksService</td>
   <td>forwardTaskOfDirectReport</td>
   <td>Elle transfère une tâche d’un rapport direct à un autre utilisateur.</td>
  </tr>
  <tr>
   <td>rejectTaskOfDirectReport</td>
   <td>ProcessManagementTeamTasksService</td>
   <td>rejectTaskOfDirectReport</td>
   <td>Elle renvoie une tâche d’un rapport direct à l’utilisateur précédent.</td>
  </tr>
  <tr>
   <td>getProperty</td>
   <td>WorkspacePropertyService</td>
   <td>getProperty</td>
   <td>Elle récupère une propriété de l’espace de travail d’un utilisateur.</td>
  </tr>
  <tr>
   <td>removeProperty</td>
   <td>WorkspacePropertyService</td>
   <td>delete</td>
   <td>Elle supprime une propriété de l’espace de travail d’un utilisateur.</td>
  </tr>
  <tr>
   <td>getProperties</td>
   <td>WorkspacePropertyService</td>
   <td>getPropertiesAsMap</td>
   <td>Elle renvoie toutes les propriétés de l’espace de travail d’un utilisateur.</td>
  </tr>
  <tr>
   <td>setProperty</td>
   <td>WorkspacePropertyService</td>
   <td>setProperty</td>
   <td>Elle définit une propriété de l’espace de travail d’un utilisateur.</td>
  </tr>
  <tr>
   <td>getCurrentUserImageUrl</td>
   <td>ProcessManagementClientSessionService</td>
   <td>getCurrentUserImageUrl</td>
   <td>Elle récupère l’URL de l’image de l’utilisateur d’un utilisateur connecté.</td>
  </tr>
  <tr>
   <td>getUserImageUrl</td>
   <td>ProcessManagementClientSessionService</td>
   <td>getUserImageUrl</td>
   <td>Elle récupère l’URL de l’image de l’utilisateur pour l’utilisateur spécifié.</td>
  </tr>
  <tr>
   <td>uploadNote</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>uploadNote</td>
   <td>Elle télécharge une note sur le serveur pour une tâche.</td>
  </tr>
  <tr>
   <td>uploadRMAToServer (également appelée directement à partir d’un modèle HTML)<br /> </td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>uploadAttachment</td>
   <td>Elle télécharge une pièce jointe sur le serveur pour une tâche.</td>
  </tr>
  <tr>
   <td>getImageURL (également appelée directement à partir d’un modèle HTML)</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>getImage</td>
   <td>Elle récupère l’image d’un processus.</td>
  </tr>
 </tbody>
</table>
