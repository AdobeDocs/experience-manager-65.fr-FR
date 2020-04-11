---
title: Description de l’objet JSON de l’espace de travail AEM Forms
seo-title: Description de l’objet JSON de l’espace de travail AEM Forms
description: Informations conceptuelles sur les objets JavaScript JSON utilisés dans l’espace de travail LiveCycle AEM Forms pour la personnalisation, l’extension, la modification et la réutilisation.
seo-description: Informations conceptuelles sur les objets JavaScript JSON utilisés dans l’espace de travail LiveCycle AEM Forms pour la personnalisation, l’extension, la modification et la réutilisation.
uuid: 91c923c8-144a-4453-ba91-6a5193f1c4c4
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 61b7246d-ed28-4470-a0a2-a4aaf1a061a4
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Description de l’objet JSON de l’espace de travail AEM Forms {#aem-forms-workspace-json-object-description}

Les objets JSON utilisés dans l’espace de travail AEM Forms sont décrits ci-dessous.

1. Catégorie

   Les catégories sont présentes dans l’onglet Démarrer le processus de Workspace. Ces catégories sont utilisées pour classer les points de départ.

<table>
 <tbody>
  <tr>
   <td><strong>Propriétés</strong></td>
   <td><strong>Client uniquement</strong></td>
   <td><strong>Commentaires</strong></td>
  </tr>
  <tr>
   <td>nom est</td>
   <td>F</td>
   <td>Nom de la catégorie</td>
  </tr>
  <tr>
   <td>id</td>
   <td>F</td>
   <td>ID de la catégorie<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>description<br type="_moz" /> </td>
   <td>F</td>
   <td>Description de la catégorie<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>parentOid<br type="_moz" /> </td>
   <td>F</td>
   <td>Contient l’OID de la catégorie parent<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>startPointsList<br type="_moz" /> </td>
   <td>T</td>
   <td>Contient la liste de tous les points de départ présents dans une catégorie</td>
  </tr>
  <tr>
   <td>categoryList</td>
   <td>T</td>
   <td>Contient la liste des catégories enfants directes d’une catégorie<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Tous les points de départ et favoris sont des catégories qui sont définies côté client. La catégorie Favoris contient tous les points de départ qui sont marqués par l’utilisateur comme favoris. La catégorie Tous les points de départ contient tous les points de départ.

1. Startpoint

   Startpoint est utilisé pour démarrer un processus à partir de Workspace en cas d’appel.

   | **Propriété** | **Client uniquement** | **Commentaires** |
   |---|---|---|
   | categoryId | F | Contient l’ID de la catégorie à laquelle appartient le point de départ. |
   | description | F | Contient une description pour un point de départ. |
   | nom est | F | Contient le nom du point de départ. |
   | serializedImageTicket | F | Contient le ticket de l’image correspondant au point de départ. Le ticket de cette image est utilisé dans le champ imageUrl du point de départ, pour obtenir l’image pour le point de départ à partir du serveur. |
   | serviceName | F | Contient le nom du service pour le point de départ. |
   | startpointId | F | Contient l’ID du point de départ. |
   | isFavorite | T | Indique si le point de départ est un favori ou non. True si le point de départ est un favori, sinon false. |
   | isDefaultImage | T | Indique s’il existe une image spécifiée pour le processus ou non. True si aucune image n’est associée au processus, sinon false. |
   | task | T | Contient la tâche créée lorsque le point de départ est appelé. |
   | imageUrl | T | Contient l’URL de l’image correspondant au point de départ. |

1. Tâche

   Les tâches sont attribuées aux utilisateurs/groupes et comprennent une interface utilisateur (un formulaire ou un guide - déconseillé) qui peut être renseignée avec des données. Lorsqu’une tâche est affectée aux utilisateurs, le formulaire ou le Guide permettant de la terminer et de l’envoyer leur est fourni.

<table>
 <tbody>
  <tr>
   <td>Propriétés<br /> </td>
   <td>Client uniquement<br /> </td>
   <td>Commentaires<br /> </td>
  </tr>
  <tr>
   <td>classOfTask</td>
   <td>F</td>
   <td>La classe de tâche est « LC8 » lorsque la tâche est lc8 else «  standard ».<br /> </td>
  </tr>
  <tr>
   <td>completeTime<br /> </td>
   <td>F</td>
   <td>Contient l’horodatage de fin de la tâche.<br /> </td>
  </tr>
  <tr>
   <td>consultGroupId<br /> </td>
   <td>F</td>
   <td>Contient l’ID d’un groupe dont la tâche peut être consultée. Défini lors de la conception du processus.<br /> </td>
  </tr>
  <tr>
   <td>createTime<br /> </td>
   <td>F</td>
   <td>Contient l’horodatage de création de la tâche.<br /> </td>
  </tr>
  <tr>
   <td>creationId<br /> </td>
   <td>F</td>
   <td>Contient l’ID de l’utilisateur qui a créé la tâche.<br /> </td>
  </tr>
  <tr>
   <td>currentAssignment<br /> </td>
   <td>F</td>
   <td>Contient des informations sur l’affectation actuelle de la tâche.<br /> </td>
  </tr>
  <tr>
   <td>deadline<br /> </td>
   <td>F</td>
   <td>Contient l’horodatage d’échéance d’une tâche.<br /> </td>
  </tr>
  <tr>
   <td>description<br /> </td>
   <td>F</td>
   <td>Contient la description de la tâche.<br /> </td>
  </tr>
  <tr>
   <td>displayName<br /> </td>
   <td>F</td>
   <td>Contient le nom d’affichage de la tâche.<br /> </td>
  </tr>
  <tr>
   <td>forwardGroupId<br /> </td>
   <td>F</td>
   <td>Contient l’ID d’un groupe auquel la tâche peut être transmise. Défini lors de la conception du processus.<br /> </td>
  </tr>
  <tr>
   <td>instructions<br /> </td>
   <td>F</td>
   <td>Contient des instructions pour une tâche.<br /> </td>
  </tr>
  <tr>
   <td>isLocked<br /> </td>
   <td>F</td>
   <td>True si la tâche est verrouillée.<br /> </td>
  </tr>
  <tr>
   <td>isMustOpenToComplete<br /> </td>
   <td>F</td>
   <td>True si le formulaire de la tâche doit être ouvert pour terminer la tâche.<br /> </td>
  </tr>
  <tr>
   <td>isOpenFullScreen<br /> </td>
   <td>F</td>
   <td>Si la valeur est true, à l’ouverture de la tâche, le formulaire prend l’écran entier la première fois.<br /> </td>
  </tr>
  <tr>
   <td>isRouteSelectionRequired<br /> </td>
   <td>F</td>
   <td>Si la valeur est true, l’itinéraire doit être sélectionné pour terminer la tâche.<br /> </td>
  </tr>
  <tr>
   <td>isShowAttachments<br /> </td>
   <td>F</td>
   <td>Les pièces jointes sont affichées si la valeur est true.<br /> </td>
  </tr>
  <tr>
   <td>isStartTask<br /> </td>
   <td>F</td>
   <td>Si la valeur est true, la tâche est créée à partir du point de départ.<br /> </td>
  </tr>
  <tr>
   <td>isVisible<br /> </td>
   <td>F</td>
   <td>True si la tâche est visible dans Workspace.<br /> </td>
  </tr>
  <tr>
   <td>nextReminder<br /> </td>
   <td>F</td>
   <td>Horodatage pour le rappel suivant.<br /> </td>
  </tr>
  <tr>
   <td>priority<br /> </td>
   <td>F</td>
   <td>Contient la priorité de la tâche.<br /> 1 = priorité la plus élevée<br />2 = priorité élevée<br /> 3 = priorité normale<br /> 4 = faible priorité<br /> 5 = priorité la plus faible<br /> </td>
  </tr>
  <tr>
   <td>processInstanceId</td>
   <td>F</td>
   <td>ID de l’instance du processus dont la tâche fait partie.<br /> </td>
  </tr>
  <tr>
   <td>processInstanceStatus<br /> </td>
   <td>F</td>
   <td>Etat de l’instance de processus d’une tâche.<br /> </td>
  </tr>
  <tr>
   <td>reminderCount<br /> </td>
   <td>F</td>
   <td>Contient le nombre de rappels pour la tâche.<br /> </td>
  </tr>
  <tr>
   <td>routeList<br /> </td>
   <td>F</td>
   <td>Contient la liste des itinéraires associée à la tâche. L’utilisateur peut terminer la tâche en sélectionnant l’un des itinéraires dans la liste.<br /> </td>
  </tr>
  <tr>
   <td>selectedRoute<br /> </td>
   <td>F</td>
   <td>Contient le nom de l’itinéraire sélectionné lorsque la tâche a été terminée.<br /> </td>
  </tr>
  <tr>
   <td>serializedImageTicket<br /> </td>
   <td>F</td>
   <td>Contient le ticket de l’image correspondant à la tâche.  Le ticket de cette image est utilisé dans le champ imageUrl de la tâche, pour obtenir l’image pour la tâche à partir du serveur.<br /> <br /> </td>
  </tr>
  <tr>
   <td>serviceName<br /> </td>
   <td>F</td>
   <td>Contient le nom du service pour la tâche.<br /> </td>
  </tr>
  <tr>
   <td>serviceTitle<br /> </td>
   <td>F</td>
   <td>Contient le titre du service pour la tâche.<br /> </td>
  </tr>
  <tr>
   <td>status<br /> </td>
   <td>F</td>
   <td>1 = Créée (la tâche est créée à partir du point de départ.)<br /> 2 = Créée et enregistrée (la tâche est créée à partir du point de départ et enregistrée.)<br /> 3 = Affectée (la tâche est affectée à l’utilisateur après le démarrage du processus.)<br /> 4 = Affectée et enregistrée (la tâche est affectée et enregistrée.)<br /> 100 = Terminée (la tâche est terminée.)<br /> 101 = Arrivée à échéance (la tâche a atteint l’échéance.)<br /> 102 = Interrompu<br /> </td>
  </tr>
  <tr>
   <td>stepName<br /> </td>
   <td>F</td>
   <td>Contient le nom de la tâche défini lors de la conception du processus.<br /> </td>
  </tr>
  <tr>
   <td>summaryUrl<br /> </td>
   <td>F</td>
   <td>Contient l’URL du résumé de la tâche.<br /> </td>
  </tr>
  <tr>
   <td>taskACL<br /> </td>
   <td>F</td>
   <td>Liste de contrôle d’accès pour une tâche.<br /> </td>
  </tr>
  <tr>
   <td>taskId<br /> </td>
   <td>F</td>
   <td>ID d’une tâche.<br /> </td>
  </tr>
  <tr>
   <td>updateTime<br /> </td>
   <td>F</td>
   <td>Horodatage de dernière mise à jour de la tâche.<br /> </td>
  </tr>
  <tr>
   <td>formUrl<br /> </td>
   <td>T</td>
   <td>Contient l’URL de formulaire pour une tâche.<br /> </td>
  </tr>
  <tr>
   <td>taskFormType<br /> </td>
   <td>T</td>
   <td>Contient un type de formulaire de tâche. Grâce à ce champ, la tâche est rendue sur le client en tant que formulaire PDF, formulaire SWF, etc.<br /> </td>
  </tr>
  <tr>
   <td>showDirectActions<br /> </td>
   <td>T</td>
   <td>Si la valeur est true, les actions d’itinéraire sont visibles dans Workspace.<br /> </td>
  </tr>
  <tr>
   <td>showACLActions<br /> </td>
   <td>T</td>
   <td>Si la valeur est true, les actions comme transmettre, consulter partager, sont visibles dans Workspace.<br /> </td>
  </tr>
  <tr>
   <td>supportsOffline<br /> </td>
   <td>T</td>
   <td>Si la valeur est true, le formulaire peut être déconnecté. Pour les formulaires PDF uniquement.<br /> </td>
  </tr>
  <tr>
   <td>supportsSave<br /> </td>
   <td>T</td>
   <td>Si la valeur est true, l’utilisateur peut enregistrer la tâche.<br /> </td>
  </tr>
  <tr>
   <td>readerSubmitOptions<br /> </td>
   <td>T</td>
   <td>Cet objet contient des options qui sont utilisées pour envoyer des formulaires PDF via Reader lorsque le formulaire PDF ne contient aucun bouton d’envoi.<br /> </td>
  </tr>
  <tr>
   <td>isDefaultImage<br /> </td>
   <td>T</td>
   <td>Indique s’il existe une image spécifiée pour le processus ou non. True si aucune image n’est associée au processus, sinon false.<br /> </td>
  </tr>
  <tr>
   <td>historyTaskList<br /> </td>
   <td>T</td>
   <td>Contient la liste des tâches qui sont utilisées dans l’onglet Historique des détails de la tâche.<br /> </td>
  </tr>
  <tr>
   <td>isOwner<br /> </td>
   <td>T</td>
   <td>True si l’utilisateur connecté est propriétaire de la tâche.<br /> </td>
  </tr>
  <tr>
   <td>availableCommands<br /> </td>
   <td>T</td>
   <td>Contient toutes les actions qui peuvent être prises sur la tâche.<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.directCommands<br /> </td>
   <td>T</td>
   <td>Contient toutes les actions d’itinéraire disponibles pour une tâche.<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.taskACLCommands<br /> </td>
   <td>T</td>
   <td>Contient des commandes telles que transmettre, partager et consulter si elles sont disponibles pour une tâche.<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.otherCommands<br /> </td>
   <td>T</td>
   <td>Contient des commandes telles que verrouiller, déverrouiller, abandonner, renvoyer, demander, etc. si elles sont disponibles.<br /> </td>
  </tr>
  <tr>
   <td>processInstanceInfo<br /> </td>
   <td>T</td>
   <td>Contient des informations sur l’instance de processus de la tâche.<br /> </td>
  </tr>
  <tr>
   <td>processVariables<br /> </td>
   <td>T<br /> </td>
   <td>Contient un tableau d’objets des variables de processus, le cas échéant.<br /> </td>
  </tr>
  <tr>
   <td>pendingTasks<br /> </td>
   <td>T</td>
   <td>Contient la liste des tâches en attente pour l’instance de processus d’une tâche.<br /> </td>
  </tr>
  <tr>
   <td>userActions<br /> </td>
   <td>T</td>
   <td>Tableau d’objets. Chaque objet contient des détails sur l’itinéraire et son message de confirmation correspondant, le cas échéant.<br /> </td>
  </tr>
  <tr>
   <td>dataUrl<br /> </td>
   <td>T</td>
   <td>URL pour les données du formulaire d’une tâche.<br /> </td>
  </tr>
  <tr>
   <td>externalAppConfig<br /> </td>
   <td>T</td>
   <td>Configuration pour les formulaires de l’application tierce.<br /> </td>
  </tr>
  <tr>
   <td>submitted<br /> </td>
   <td>T</td>
   <td>True si la tâche est envoyée.<br /> </td>
  </tr>
  <tr>
   <td>attachments<br /> </td>
   <td>T</td>
   <td>Liste des pièces jointes pour une tâche.<br /> </td>
  </tr>
  <tr>
   <td>assignments<br /> </td>
   <td>T</td>
   <td>Liste des affectations d’une tâche.<br /> </td>
  </tr>
 </tbody>
</table>

1. Filtrer

   Le filtre est en principe la file d’attente de l’utilisateur ou du groupe. Quand une tâche est affectée à l’utilisateur/au groupe, la tâche est ajoutée dans la file d’attente correspondante.

<table>
 <tbody>
  <tr>
   <td><strong>Propriétés</strong></td>
   <td><strong>Client uniquement</strong></td>
   <td><strong>Commentaires</strong></td>
  </tr>
  <tr>
   <td>isDefault <br type="_moz" /> </td>
   <td>F</td>
   <td>True si la file d’attente est la file d’attente par défaut de l’utilisateur connecté, sinon false.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>nom est<br type="_moz" /> </td>
   <td>F</td>
   <td>Nom du propriétaire de la file d’attente.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>qid</td>
   <td>F</td>
   <td>ID de la file d’attente.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>type</td>
   <td>F</td>
   <td>Contient le type de la file d’attente.<br /> 0 - File d’attente de l’utilisateur.<br /> 1. File d’attente partagée.<br /> 2. File d’attente du groupe.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>query</td>
   <td>T</td>
   <td>Contient la requête associée à un filtre. Cette requête est utilisée pour rechercher des tâches dans la liste de tâches complète.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>tasks</td>
   <td>T</td>
   <td>Contient la liste de toutes les tâches qui appartiennent à un filtre.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Absence du bureau

   Vous pouvez gérer votre planning d’absences du bureau et contrôler le flux des tâches qui vous sont affectées pendant votre absence.

<table>
 <tbody>
  <tr>
   <td><strong>Propriété</strong><br type="_moz" /> </td>
   <td><strong>Client uniquement</strong><br type="_moz" /> </td>
   <td><strong>Commentaires</strong><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>dateRanges<br type="_moz" /> </td>
   <td>F</td>
   <td>Contient des objets de tableau des plannings d’absences du bureau d’un utilisateur. Dans chaque objet de planification, le champ startDate contient la date de  de planification et le champ endDate contient la date de fin de la planification. If endDate is null in schedule, it implies that user has not scheduled the end date of out-of-office schedule.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isNoPrimaryDesignate<br type="_moz" /> </td>
   <td>F</td>
   <td>True s’il n’y a pas de désignation principale en cas d’absence du bureau de l’utilisateur.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isOutOfOffice<br type="_moz" /> </td>
   <td>F</td>
   <td>True si l’utilisateur est absent du bureau.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>outOfOfficeDesignate<br type="_moz" /> </td>
   <td>F</td>
   <td>Contient des informations sur l’utilisateur affecté comme désignation principale par l’utilisateur.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processSpecificDesignates<br type="_moz" /> </td>
   <td>F</td>
   <td>Contient un tableau d’objets pour la désignation d’absence du bureau propre à un processus. In each process-specific designate object, processName contains the name of the process, isNotDesignated is true if no user is assigned for corresponding process, and userDesignated is null if no user assigned else details of the user assigned for corresponding process.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processus<br type="_moz" /> </td>
   <td>T</td>
   <td>Contient la liste de tous les processus disponibles pour l’utilisateur.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>initialOutOfOfficeSettings<br type="_moz" /> </td>
   <td>T</td>
   <td>Contient les paramètres d’absence du bureau initiaux de l’utilisateur, qui sont récupérés au départ.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>outOfOfficeSettings<br type="_moz" /> </td>
   <td>T</td>
   <td>Contient les paramètres d’absence du bureau modifiés.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>userSearchHistory<br type="_moz" /> </td>
   <td>T</td>
   <td>Contient la liste des utilisateurs recherchés par l’utilisateur jusqu’à la date.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Instance de processus

   Une instance de processus est créée lorsqu’un processus est appelé par le biais de workspace ou workbench.

<table>
 <tbody>
  <tr>
   <td><strong>Propriétés</strong></td>
   <td><strong>Client uniquement</strong></td>
   <td><strong>Commentaires</strong></td>
  </tr>
  <tr>
   <td>description<br type="_moz" /> </td>
   <td>F</td>
   <td>Description de l’instance de processus<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>initiator</td>
   <td>F</td>
   <td>Nom de l’initiateur d’une instance de processus.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>initiatorId</td>
   <td>F</td>
   <td>Identifiant de l’initiateur de l’instance de processus.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processCompleteTime<br type="_moz" /> </td>
   <td>F</td>
   <td>Horodatage indiquant quand le processus s’est achevé.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processInstanceId<br type="_moz" /> </td>
   <td>F</td>
   <td>Identifiant de l’instance de processus.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processInstanceStatus<br type="_moz" /> </td>
   <td>F</td>
   <td>0 = Initié<br /> 1 = En cours d’exécution<br /> 2 = Terminé<br /> 3 = En cours d’achèvement<br /> 4 = Interrompu<br /> 5 = En cours d’interruption<br /> 6 = Suspendu<br /> 7 = En cours de suspension<br /> 8 = En cours d’annulation de suspension<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processName<br type="_moz" /> </td>
   <td>F</td>
   <td>Nom du processus.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processStartTime<br type="_moz" /> </td>
   <td>F</td>
   <td>Horodatage indiquant quand le processus a commencé.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processVariables<br type="_moz" /> </td>
   <td>F</td>
   <td>Tableau d’objets de variables de processus. Each process variable object contains name which is name of process variable, value which is value of process variable and type which is type of process variable.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>tasklist<br type="_moz" /> </td>
   <td>T</td>
   <td>Tâches générées par cette instance du processus.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Nom du processus

<table>
 <tbody>
  <tr>
   <td><strong>Propriétés</strong></td>
   <td><strong>Client uniquement</strong></td>
   <td><strong>Commentaires</strong></td>
  </tr>
  <tr>
   <td>processMajorVersion<br type="_moz" /> </td>
   <td>F</td>
   <td>Version majeure d’un processus.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processMinorVersion<br type="_moz" /> </td>
   <td>F</td>
   <td>Version mineure d’un processus.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processName<br type="_moz" /> </td>
   <td>F</td>
   <td>Nom du processus.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processTitle<br type="_moz" /> </td>
   <td>F</td>
   <td>Nom du processus.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processInstanceList<br type="_moz" /> </td>
   <td>T</td>
   <td>Liste des instances de processus pour ce processus.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Object Affectation de tâche

   L’objet Affectation de tâche contient des informations sur l’affectation d’une tâche. Vous trouverez ci-dessous les propriétés de l’affectation d’une tâche.

<table>
 <tbody>
  <tr>
   <td><strong>Propriétés</strong></td>
   <td><strong>Client uniquement</strong></td>
   <td><strong>Commentaires</strong></td>
  </tr>
  <tr>
   <td>assignmentCreateTime<br type="_moz" /> </td>
   <td>F</td>
   <td>Horodatage de création de cette affectation de tâche.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>assignmentType<br type="_moz" /> </td>
   <td>F</td>
   <td>0 = Affectation initiale<br /> 1 = Transférer (la tâche a été transférée au propriétaire actuel de la tâche.)<br /> 2 = Renvoyée (la tâche a été renvoyée au propriétaire actuel de la tâche par le propriétaire précédent de la tâche.)<br /> 3 = Demandée (la tâche a été demandée par le propriétaire actuel de la tâche.)<br /> 4 = Transmission (la tâche a été affectée au propriétaire actuel de la tâche après transmission.)<br /> 5 = Administrateur affecté (la tâche a été affectée par l’administrateur au propriétaire actuel de la tâche.)<br /> 6 = Consultée (la tâche a été consultée pour le propriétaire actuel de la tâche.)<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>assignmentUpdateTime<br type="_moz" /> </td>
   <td>F</td>
   <td>Horodatage de mise à jour de cette affectation de tâche.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>queueId<br type="_moz" /> </td>
   <td>F</td>
   <td>ID de la file d’attente du propriétaire actuel de la tâche.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>queueOwner<br type="_moz" /> </td>
   <td>F</td>
   <td>Nom du propriétaire actuel de la tâche.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>queueOwnerId<br type="_moz" /> </td>
   <td>F</td>
   <td>ID du propriétaire actuel de la tâche.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Objet ACL de la tâche

   L’objet ACL de la tâche contient des informations sur les autorisations telles que transférer, partager, consulter, etc. d’une tâche. Vous trouverez ci-dessous les propriétés de l’ACL de la tâche.

<table>
 <tbody>
  <tr>
   <td><strong>Propriétés</strong></td>
   <td><strong>Client uniquement</strong></td>
   <td><strong>Commentaires</strong></td>
  </tr>
  <tr>
   <td>canAddAttachments<br type="_moz" /> </td>
   <td>F</td>
   <td>Si la valeur est true, des pièces jointes peuvent être ajoutées à une tâche.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canAddNotes<br type="_moz" /> </td>
   <td>F</td>
   <td>Si la valeur est true, des notes peuvent être ajoutées à une tâche.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canClaim<br type="_moz" /> </td>
   <td>F</td>
   <td>Si la valeur est true, la tâche ne peut pas être demandée.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canConsult<br type="_moz" /> </td>
   <td>F</td>
   <td>Si la valeur est true, la tâche peut être consultée.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canForward<br type="_moz" /> </td>
   <td>F</td>
   <td>Si la valeur est true, la tâche peut être transférée.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canShare<br type="_moz" /> </td>
   <td>F</td>
   <td>Si la valeur est true, la tâche peut être partagée.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Pièce jointe de la tâche

   Des pièces jointes peuvent être ajoutées à une tâche. Une pièce jointe peut être de type pièce jointe et note. Vous trouverez ci-dessous les propriétés de l’objet pièce jointe.

<table>
 <tbody>
  <tr>
   <td><strong>Propriétés</strong></td>
   <td><strong>Client uniquement</strong></td>
   <td><strong>Commentaires</strong></td>
  </tr>
  <tr>
   <td>creationDate<br type="_moz" /> </td>
   <td>F</td>
   <td>Horodatage de création de la pièce jointe.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>creatorId<br type="_moz" /> </td>
   <td>F</td>
   <td>ID de l’utilisateur qui a ajouté la pièce jointe.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>creatorName<br type="_moz" /> </td>
   <td>F</td>
   <td>Nom de l’utilisateur qui a ajouté la pièce jointe.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>description<br type="_moz" /> </td>
   <td>F</td>
   <td>Description de la pièce jointe.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>fileName<br type="_moz" /> </td>
   <td>F</td>
   <td>Nom de la pièce jointe.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>id<br type="_moz" /> </td>
   <td>F</td>
   <td>ID de la pièce jointe.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>lastModifiedDate<br type="_moz" /> </td>
   <td>F</td>
   <td>Horodatage de dernière modification de la pièce jointe.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>noteExtended<br type="_moz" /> </td>
   <td>F</td>
   <td>Si la valeur est true, la note est une note étendue (longue).<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>autorisations ;<br type="_moz" /> </td>
   <td>F</td>
   <td>Autorisations associées à une pièce jointe. allowRead field is for read permission, allowWrite is for write permission, allowDelete is for delete permission.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>size<br type="_moz" /> ; </td>
   <td>F</td>
   <td>Taille de la pièce jointe en octets.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>taskId<br type="_moz" /> </td>
   <td>F</td>
   <td>ID de la tâche à laquelle la pièce jointe est ajoutée.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>type<br type="_moz" /> </td>
   <td>F</td>
   <td>Type is attachment for files and Type is note for notes.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedCreationDate<br type="_moz" /> </td>
   <td>T</td>
   <td>Contient la date de création de la pièce jointe en fonction des paramètres de l’interface utilisateur de l’utilisateur.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedDescription<br type="_moz" /> </td>
   <td>T</td>
   <td>Description de la pièce jointe formatée. Utilisé pour afficher les caractères spéciaux présents dans la description de la pièce jointe dans l’espace de travail AEM Forms.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedFileName<br type="_moz" /> </td>
   <td>T</td>
   <td>Nom de la pièce jointe formatée. Utilisé pour afficher les caractères spéciaux présents dans le nom de la pièce jointe dans l’espace de travail AEM Forms. Pour les notes uniquement.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Utilisateur

   Vous trouverez ci-dessous les propriétés de l’objet utilisateur.

<table>
 <tbody>
  <tr>
   <td><strong>Propriétés</strong></td>
   <td><strong>Client uniquement</strong></td>
   <td><strong>Commentaires</strong></td>
  </tr>
  <tr>
   <td>address<br type="_moz" /> </td>
   <td>F</td>
   <td>Adresse de l’utilisateur.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>commonName<br type="_moz" /> </td>
   <td>F</td>
   <td>Nom commun de l’utilisateur.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>description<br type="_moz" /> </td>
   <td>F</td>
   <td>Description de l’utilisateur.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>directGroupMemberships<br type="_moz" /> </td>
   <td>F</td>
   <td>Liste des groupes de l’utilisateur.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>displayName<br type="_moz" /> </td>
   <td>F</td>
   <td>Nom d’affichage de l’utilisateur.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>email<br type="_moz" /> </td>
   <td>F</td>
   <td>ID de courrier électronique de l’utilisateur.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isOutOfOffice<br type="_moz" /> </td>
   <td>F</td>
   <td>True si l’utilisateur est absent du bureau.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>lastName<br type="_moz" /> </td>
   <td>F</td>
   <td>Nom de famille de l’utilisateur.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>firstName<br type="_moz" /> </td>
   <td>F</td>
   <td>Prénom de l’utilisateur.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>oid<br type="_moz" /> </td>
   <td>F</td>
   <td>ID de l’utilisateur.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>org<br type="_moz" /> </td>
   <td>F</td>
   <td>Nom de l’entreprise de l’utilisateur.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>postalAddress<br type="_moz" /> </td>
   <td>F</td>
   <td>Adresse postale de l’utilisateur.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>telephone<br type="_moz" /> </td>
   <td>F</td>
   <td>Numéro du contact de l’utilisateur.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>telephoneNumber<br type="_moz" /> </td>
   <td>F</td>
   <td>Numéro du contact de l’utilisateur.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>userid<br type="_moz" /> </td>
   <td>F</td>
   <td>ID de connexion de l’utilisateur.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>
