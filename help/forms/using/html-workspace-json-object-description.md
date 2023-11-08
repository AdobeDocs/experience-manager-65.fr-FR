---
title: Description de l’objet JSON de l’espace de travail AEM Forms
description: Informations conceptuelles sur les objets JavaScript JSON utilisés dans l’espace de travail AEM Forms LiveCycle pour la personnalisation, l’extension, la modification et la réutilisation.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: f837a2b3-4650-4261-84c6-291bb2a46dc7
source-git-commit: 941e5d7574d31622f50e50e717c21cd2eba2e602
workflow-type: tm+mt
source-wordcount: '2115'
ht-degree: 25%

---

# Description de l’objet JSON de l’espace de travail AEM Forms {#aem-forms-workspace-json-object-description}

Les objets JSON utilisés dans l’espace de travail AEM Forms sont décrits ci-dessous.

1. Catégorie

   Les catégories sont présentes dans l’onglet Démarrer le processus de Workspace. Ces catégories sont utilisées pour classer les points de départ.

<table>
 <tbody>
  <tr>
   <td><strong>Propriété</strong></td>
   <td><strong>Client uniquement</strong></td>
   <td><strong>Commentaires</strong></td>
  </tr>
  <tr>
   <td>name</td>
   <td>F</td>
   <td>Nom de catégorie</td>
  </tr>
  <tr>
   <td>id</td>
   <td>F</td>
   <td>ID de catégorie<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>description<br type="_moz" /> </td>
   <td>F</td>
   <td>Description de la catégorie<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>parentOid<br type="_moz" /> </td>
   <td>F</td>
   <td>Contient l’ID de la catégorie parente<br type="_moz" /> </td>
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

1. Point de départ

   Startpoint permet de démarrer un processus à partir de l’espace de travail lors de l’appel.

   | **Propriété** | **Client uniquement** | **Commentaires** |
   |---|---|---|
   | categoryId | F | Il contient l’identifiant de la catégorie à laquelle appartient le point de départ. |
   | description | F | Contient la description d’un point de départ. |
   | name | F | Contient le nom du point de départ. |
   | serializedImageTicket | F | Contient le ticket de l’image correspondant au point de départ. Le ticket de cette image est utilisé dans le champ imageUrl du point de départ, pour obtenir l’image pour le point de départ à partir du serveur. |
   | serviceName | F | Contient le nom du service pour le point de départ. |
   | startpointId | F | Contient l’identifiant du point de départ. |
   | isFavorite | T | Indique si le point de départ est un favori ou non. True si le point de départ est favori, sinon false. |
   | isDefaultImage | T | Indique s’il existe une image spécifiée pour le processus ou non. True si aucune image n’est associée au processus, sinon false. |
   | tâche | T | Contient la tâche créée lorsque le point de départ est appelé. |
   | imageUrl | T | Contient l’URL de l’image correspondant au point de départ. |

1. Tâche

   Les tâches sont attribuées aux utilisateurs/groupes et comprennent une interface utilisateur (un formulaire ou un guide - déconseillé) qui peut être renseignée avec des données. Lorsque des utilisateurs se voient attribuer une tâche, ils reçoivent le formulaire ou le guide à remplir et à envoyer.

<table>
 <tbody>
  <tr>
   <td>Propriété<br /> </td>
   <td>Client uniquement<br /> </td>
   <td>Commentaires<br /> </td>
  </tr>
  <tr>
   <td>classOfTask</td>
   <td>F</td>
   <td>La classe de tâche est « LC8 » lorsque la tâche est lc8 else « standard ».<br /> </td>
  </tr>
  <tr>
   <td>completeTime<br /> </td>
   <td>F</td>
   <td>Contient l’horodatage de fin de la tâche.<br /> </td>
  </tr>
  <tr>
   <td>consultGroupId<br /> </td>
   <td>F</td>
   <td>Contient l’ID d’un groupe dont la tâche peut être consultée. Il est défini lors de la conception du processus.<br /> </td>
  </tr>
  <tr>
   <td>createTime<br /> </td>
   <td>F</td>
   <td>Contient l’horodatage de création de la tâche.<br /> </td>
  </tr>
  <tr>
   <td>createdId<br /> </td>
   <td>F</td>
   <td>Il contient l’identifiant de l’utilisateur qui a créé la tâche.<br /> </td>
  </tr>
  <tr>
   <td>currentAssignment<br /> </td>
   <td>F</td>
   <td>Il contient des détails sur l’affectation actuelle de la tâche.<br /> </td>
  </tr>
  <tr>
   <td>échéance<br /> </td>
   <td>F</td>
   <td>Il contient l’horodatage qui indique quand une tâche atteindra son délai d’expiration.<br /> </td>
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
   <td>Contient l’ID d’un groupe auquel la tâche peut être transmise. Il est défini lors de la conception du processus.<br /> </td>
  </tr>
  <tr>
   <td>instructions<br /> </td>
   <td>F</td>
   <td>Il contient des instructions pour une tâche.<br /> </td>
  </tr>
  <tr>
   <td>isLocked<br /> </td>
   <td>F</td>
   <td>True si la tâche est verrouillée.<br /> </td>
  </tr>
  <tr>
   <td>isMustOpenToComplete<br /> </td>
   <td>F</td>
   <td>True si le formulaire de tâche doit être ouvert pour terminer la tâche.<br /> </td>
  </tr>
  <tr>
   <td>isOpenFullScreen<br /> </td>
   <td>F</td>
   <td>Si la valeur est true, lors de l’ouverture de la tâche, le formulaire s’exécute à l’écran la première fois.<br /> </td>
  </tr>
  <tr>
   <td>isRouteSelectionRequired<br /> </td>
   <td>F</td>
   <td>Si la valeur est true, l’itinéraire doit être sélectionné pour terminer la tâche.<br /> </td>
  </tr>
  <tr>
   <td>isShowAttachments<br /> </td>
   <td>F</td>
   <td>Les pièces jointes s’affichent si la valeur est true.<br /> </td>
  </tr>
  <tr>
   <td>isStartTask<br /> </td>
   <td>F</td>
   <td>Si la valeur est true, la tâche est créée à partir du point de départ.<br /> </td>
  </tr>
  <tr>
   <td>isVisible<br /> </td>
   <td>F</td>
   <td>True si la tâche est visible dans l’espace de travail.<br /> </td>
  </tr>
  <tr>
   <td>nextReminder<br /> </td>
   <td>F</td>
   <td>Horodatage du prochain rappel.<br /> </td>
  </tr>
  <tr>
   <td>priorité<br /> </td>
   <td>F</td>
   <td>Contient la priorité de la tâche.<br /> 1 = Priorité la plus élevée<br /> 2 = Priorité élevée<br /> 3 = Priorité normale<br /> 4 = Priorité faible<br /> 5 = Priorité la plus faible<br /> </td>
  </tr>
  <tr>
   <td>processInstanceId</td>
   <td>F</td>
   <td>Identifiant de l’instance de processus dont la tâche fait partie.<br /> </td>
  </tr>
  <tr>
   <td>processInstanceStatus<br /> </td>
   <td>F</td>
   <td>État de l’instance de processus de la tâche.<br /> </td>
  </tr>
  <tr>
   <td>rappderCount<br /> </td>
   <td>F</td>
   <td>Contient le nombre de rappels pour la tâche.<br /> </td>
  </tr>
  <tr>
   <td>routeList<br /> </td>
   <td>F</td>
   <td>Contient la liste des itinéraires associée à la tâche. L’utilisateur peut terminer la tâche en sélectionnant l’un des itinéraires de la liste.<br /> </td>
  </tr>
  <tr>
   <td>selectedRoute<br /> </td>
   <td>F</td>
   <td>Contient le nom de l’itinéraire sélectionné lorsque la tâche a été terminée.<br /> </td>
  </tr>
  <tr>
   <td>serializedImageTicket<br /> </td>
   <td>F</td>
   <td>Contient le ticket de l’image correspondant à la tâche. Ce ticket d’image est utilisé dans le champ imageUrl de la tâche, pour obtenir l’image de la tâche à partir du serveur.<br /> <br /> </td>
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
   <td>1 = Créée (la tâche est créée à partir du point de départ.)<br /> 2 = Créée et enregistrée (la tâche est créée à partir du point de départ et enregistrée.)<br /> 3 = Affectée (la tâche est affectée à l’utilisateur une fois le processus démarré.)<br /> 4 = Affectée et enregistrée (la tâche est affectée et enregistrée.)<br /> 100 = Terminée (la tâche est terminée.)<br /> 101 = Arrivée à échéance (la tâche a atteint la date limite.)<br /> 102 = Interrompu<br /> </td>
  </tr>
  <tr>
   <td>stepName<br /> </td>
   <td>F</td>
   <td>Contient le nom du jeu de tâches lors de la conception du processus.<br /> </td>
  </tr>
  <tr>
   <td>summaryUrl<br /> </td>
   <td>F</td>
   <td>Contient l’URL de résumé de la tâche.<br /> </td>
  </tr>
  <tr>
   <td>taskACL<br /> </td>
   <td>F</td>
   <td>Il s’agit de la liste de contrôle d’accès d’une tâche.<br /> </td>
  </tr>
  <tr>
   <td>taskId<br /> </td>
   <td>F</td>
   <td>Identifiant d’une tâche.<br /> </td>
  </tr>
  <tr>
   <td>updateTime<br /> </td>
   <td>F</td>
   <td>Horodatage de la dernière mise à jour de la tâche.<br /> </td>
  </tr>
  <tr>
   <td>formUrl<br /> </td>
   <td>T</td>
   <td>Contient l’URL du formulaire pour une tâche.<br /> </td>
  </tr>
  <tr>
   <td>taskFormType<br /> </td>
   <td>T</td>
   <td>Contient un type de formulaire de tâche. À l’aide de ce champ, la tâche est rendue sur le client au format pdf pour, swf form, etc.<br /> </td>
  </tr>
  <tr>
   <td>showDirectActions<br /> </td>
   <td>T</td>
   <td>Si la valeur est true, les actions d’itinéraire sont visibles dans Workspace.<br /> </td>
  </tr>
  <tr>
   <td>showACLActions<br /> </td>
   <td>T</td>
   <td>Si la valeur est true, des actions telles que transférer, consulter, partager sont visibles dans Workspace.<br /> </td>
  </tr>
  <tr>
   <td>supportsOffline<br /> </td>
   <td>T</td>
   <td>Si la valeur est true, le formulaire peut être déconnecté. Il s’agit uniquement de formulaires PDF.<br /> </td>
  </tr>
  <tr>
   <td>supportsSave<br /> </td>
   <td>T</td>
   <td>Si la valeur est true, l’utilisateur peut enregistrer la tâche.<br /> </td>
  </tr>
  <tr>
   <td>readerSubmitOptions<br /> </td>
   <td>T</td>
   <td>Cet objet contient des options qui sont utilisées pour envoyer des formulaires pdf par lecteur lorsque le formulaire pdf ne contient pas de bouton d’envoi.<br /> </td>
  </tr>
  <tr>
   <td>isDefaultImage<br /> </td>
   <td>T</td>
   <td>Indique s’il existe une image spécifiée pour le processus ou non. True si aucune image n’est associée au processus, sinon false.<br /> </td>
  </tr>
  <tr>
   <td>historyTaskList<br /> </td>
   <td>T</td>
   <td>Elle contient la liste des tâches utilisées dans l’onglet Historique des détails de la tâche.<br /> </td>
  </tr>
  <tr>
   <td>isOwner<br /> </td>
   <td>T</td>
   <td>True si l’utilisateur connecté est propriétaire de la tâche.<br /> </td>
  </tr>
  <tr>
   <td>availableCommands<br /> </td>
   <td>T</td>
   <td>Il contient toutes les actions qui peuvent être entreprises sur tâche.<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.directCommands<br /> </td>
   <td>T</td>
   <td>Elle contient toutes les actions d’itinéraire disponibles pour une tâche.<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.taskACLCommands<br /> </td>
   <td>T</td>
   <td>Il contient des commandes telles que transférer, partager et consulter si elles sont disponibles pour une tâche.<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.otherCommands<br /> </td>
   <td>T</td>
   <td>Il contient des commandes telles que verrouiller, déverrouiller, abandonner, revenir, demander, etc., si possible.<br /> </td>
  </tr>
  <tr>
   <td>processInstanceInfo<br /> </td>
   <td>T</td>
   <td>Il contient des informations sur l’instance de processus de la tâche.<br /> </td>
  </tr>
  <tr>
   <td>processVariables<br /> </td>
   <td>T<br /> </td>
   <td>Il contient un tableau d’objets de variables de processus, le cas échéant.<br /> </td>
  </tr>
  <tr>
   <td>pendingTasks<br /> </td>
   <td>T</td>
   <td>Contient la liste des tâches en attente pour l’instance de processus de la tâche.<br /> </td>
  </tr>
  <tr>
   <td>userActions<br /> </td>
   <td>T</td>
   <td>Tableau d’objets. Chaque objet contient des détails sur l’itinéraire et son message de confirmation correspondant, le cas échéant.<br /> </td>
  </tr>
  <tr>
   <td>dataUrl<br /> </td>
   <td>T</td>
   <td>Il s’agit de l’URL pour les données du formulaire d’une tâche.<br /> </td>
  </tr>
  <tr>
   <td>externalAppConfig<br /> </td>
   <td>T</td>
   <td>Il s’agit de la configuration des formulaires d’application tiers.<br /> </td>
  </tr>
  <tr>
   <td>submit<br /> </td>
   <td>T</td>
   <td>True si la tâche est envoyée.<br /> </td>
  </tr>
  <tr>
   <td>attachments<br /> </td>
   <td>T</td>
   <td>Liste des pièces jointes pour une tâche.<br /> </td>
  </tr>
  <tr>
   <td>affectations<br /> </td>
   <td>T</td>
   <td>Liste des affectations d’une tâche.<br /> </td>
  </tr>
 </tbody>
</table>

1. Filtrer

   Le filtre est en principe la file d’attente de l’utilisateur ou du groupe. Lorsqu’une tâche est assignée à un utilisateur/groupe, la tâche est ajoutée dans la file d’attente correspondante.

<table>
 <tbody>
  <tr>
   <td><strong>Propriété</strong></td>
   <td><strong>Client uniquement</strong></td>
   <td><strong>Commentaires</strong></td>
  </tr>
  <tr>
   <td>isDefault <br type="_moz" /> </td>
   <td>F</td>
   <td>True si la file d’attente est la file d’attente par défaut de l’utilisateur connecté, sinon false.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>name<br type="_moz" /> </td>
   <td>F</td>
   <td>Nom du propriétaire de la file d’attente.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>qid</td>
   <td>F</td>
   <td>Identifiant de la file d’attente.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>type</td>
   <td>F</td>
   <td>Contient le type de la file d’attente.<br /> 0 - File d’attente de l’utilisateur.<br /> 1. File d’attente partagée.<br /> 2. File d’attente du groupe.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>query</td>
   <td>T</td>
   <td>Contient la requête associée à un filtre. Cette requête est utilisée pour rechercher des tâches à partir d’une liste de tâches complète.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>tâches</td>
   <td>T</td>
   <td>Elle contient la liste de toutes les tâches appartenant à un filtre.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Absence du bureau

   Vous pouvez gérer votre planning d’absence du bureau et contrôler le flux des tâches qui vous sont affectées en votre absence.

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
   <td>Contient des objets de tableau des plannings d’absences du bureau d’un utilisateur. Dans chaque objet de planning, le champ startDate contient la date de début du planning et le champ endDate contient la date de fin du planning. Si endDate est null dans le planning, cela implique que l’utilisateur n’a pas planifié la date de fin du planning d’absences du bureau.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isNoPrimaryDesignate<br type="_moz" /> </td>
   <td>F</td>
   <td>True s’il n’existe aucune désignation principale en cas d’absence du bureau de l’utilisateur.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isOutOfOffice<br type="_moz" /> </td>
   <td>F</td>
   <td>True si l’utilisateur est absent du bureau.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>outOfOfficeDesignate<br type="_moz" /> </td>
   <td>F</td>
   <td>Contient les détails de l’utilisateur désigné comme principal par l’utilisateur.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processSpecificDesignates<br type="_moz" /> </td>
   <td>F</td>
   <td>Contient un tableau d’objets pour la désignation d’absence du bureau propre à un processus. Dans chaque objet de désignation propre à un processus, processName contient le nom du processus, isNotDesignated est défini sur true si aucun utilisateur n’est affecté au processus correspondant, et userDesignated est défini sur null si aucun utilisateur n’a affecté de détails else de l’utilisateur affecté au processus correspondant.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processus<br type="_moz" /> </td>
   <td>T</td>
   <td>Elle contient la liste de tous les processus disponibles pour l’utilisateur.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>initialOutOfOfficeSettings<br type="_moz" /> </td>
   <td>T</td>
   <td>Il contient les paramètres d’absence du bureau initiaux de l’utilisateur, qui sont récupérés initialement.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>outOfOfficeSettings<br type="_moz" /> </td>
   <td>T</td>
   <td>Contient les paramètres d’absence du bureau modifiés.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>userSearchHistory<br type="_moz" /> </td>
   <td>T</td>
   <td>Il contient la liste des utilisateurs qui sont recherchés par un utilisateur connecté jusqu’à la date indiquée.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Instance de processus

   Une instance de processus est créée lorsqu’un processus est appelé via workspace ou workbench.

<table>
 <tbody>
  <tr>
   <td><strong>Propriété</strong></td>
   <td><strong>Client uniquement</strong></td>
   <td><strong>Commentaires</strong></td>
  </tr>
  <tr>
   <td>description<br type="_moz" /> </td>
   <td>F</td>
   <td>Description de l’instance de processus<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>initiateur</td>
   <td>F</td>
   <td>Nom de l’initiateur d’une instance de processus.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>initiatorId</td>
   <td>F</td>
   <td>ID de l’initiateur de l’instance de processus.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processCompleteTime<br type="_moz" /> </td>
   <td>F</td>
   <td>Horodatage à la fin du processus.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processInstanceId<br type="_moz" /> </td>
   <td>F</td>
   <td>ID de l’instance de processus.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processInstanceStatus<br type="_moz" /> </td>
   <td>F</td>
   <td>0 = Lancé<br /> 1 = En cours<br /> 2 = Terminé<br /> 3 = Fin<br /> 4 = Interrompu<br /> 5 = Interruption<br /> 6 = Suspendu<br /> 7 = Suspendre<br /> 8 = Sans suspension<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processName<br type="_moz" /> </td>
   <td>F</td>
   <td>Nom du processus.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processStartTime<br type="_moz" /> </td>
   <td>F</td>
   <td>Horodatage au début du processus.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processVariables<br type="_moz" /> </td>
   <td>F</td>
   <td>Tableau d’objets de variables de processus. Chaque objet de variable de processus contient les paramètres Nom (nom de la variable de processus), Valeur (valeur de variable de processus) et Type (type de variable de processus).<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>tasklist<br type="_moz" /> </td>
   <td>T</td>
   <td>Tâches générées par cette instance de processus.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Nom du processus

<table>
 <tbody>
  <tr>
   <td><strong>Propriété</strong></td>
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
   <td>Titre du processus.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processInstanceList<br type="_moz" /> </td>
   <td>T</td>
   <td>Liste des instances de processus pour ce processus.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Objet d’affectation de tâche

   L’objet Affectation de tâche contient des informations sur l’affectation d’une tâche. Vous trouverez ci-dessous les propriétés de l’affectation de la tâche.

<table>
 <tbody>
  <tr>
   <td><strong>Propriété</strong></td>
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
   <td>0 = Attribution initiale<br /> 1 = Transférer (la tâche a été transférée au propriétaire actuel de la tâche.)<br /> 2 = Renvoyée (la tâche a été renvoyée au propriétaire actuel de la tâche par le propriétaire précédent de la tâche.)<br /> 3 = Demandée (la tâche a été demandée par le propriétaire actuel de la tâche.)<br /> 4 = Réaffectation (la tâche a été affectée au propriétaire actuel de la tâche après la réaffectation.)<br /> 5 = Administrateur affecté (la tâche a été affectée par l’administrateur au propriétaire actuel de la tâche.)<br /> 6 = Consultée (la tâche a été consultée pour le propriétaire actuel de la tâche.)<br type="_moz" /> </td>
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
   <td>Identifiant du propriétaire actuel de la tâche.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Objet ACL de la tâche

   L’objet ACL de tâche contient des informations sur les autorisations telles que transférer, partager, consulter, etc., d’une tâche. Vous trouverez ci-dessous les propriétés de l’ACL de la tâche.

<table>
 <tbody>
  <tr>
   <td><strong>Propriété</strong></td>
   <td><strong>Client uniquement</strong></td>
   <td><strong>Commentaires</strong></td>
  </tr>
  <tr>
   <td>canAddAttachments<br type="_moz" /> </td>
   <td>F</td>
   <td>Si la valeur est true, des pièces jointes peuvent être ajoutées à la tâche.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canAddNotes<br type="_moz" /> </td>
   <td>F</td>
   <td>Si la valeur est true, des notes peuvent être ajoutées à la tâche.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canClaim<br type="_moz" /> </td>
   <td>F</td>
   <td>Si la valeur est true, la tâche peut être demandée.<br type="_moz" /> </td>
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

1. Pièce jointe de tâche

   Des pièces jointes peuvent être ajoutées à une tâche. Une pièce jointe peut être de type pièce jointe et note. Vous trouverez ci-dessous les propriétés de l’objet attachment.

<table>
 <tbody>
  <tr>
   <td><strong>Propriété</strong></td>
   <td><strong>Client uniquement</strong></td>
   <td><strong>Commentaires</strong></td>
  </tr>
  <tr>
   <td>createdDate<br type="_moz" /> </td>
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
   <td>Identifiant de la pièce jointe.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>lastModifiedDate<br type="_moz" /> </td>
   <td>F</td>
   <td>Horodatage de la dernière modification de la pièce jointe.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>noteExtended<br type="_moz" /> </td>
   <td>F</td>
   <td>Si la valeur est true, la note est une note étendue (longue).<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>autorisations ;<br type="_moz" /> </td>
   <td>F</td>
   <td>Autorisations associées à une pièce jointe. Le champ allowRead représente l’autorisation de lire, allowWrite l’autorisation d’écrire et allowDelete l’autorisation de supprimer.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>size<br type="_moz" /> ; </td>
   <td>F</td>
   <td>Taille de la pièce jointe en octets.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>taskId<br type="_moz" /> </td>
   <td>F</td>
   <td>Identifiant de la tâche à laquelle la pièce jointe est ajoutée.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>type<br type="_moz" /> </td>
   <td>F</td>
   <td>Le type est « attachment » pour les fichiers et « note » pour les notes.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedCreationDate<br type="_moz" /> </td>
   <td>T</td>
   <td>Il contient la date de création des pièces jointes en fonction des paramètres de l’interface utilisateur de l’utilisateur.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedDescription<br type="_moz" /> </td>
   <td>T</td>
   <td>Description de la pièce jointe formatée. Utilisé pour afficher les caractères spéciaux présents dans la description de la pièce jointe dans l’espace de travail AEM Forms.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedFileName<br type="_moz" /> </td>
   <td>T</td>
   <td>Nom de la pièce jointe formatée. Utilisé pour afficher les caractères spéciaux présents dans le nom de la pièce jointe dans l’espace de travail AEM Forms. Cette option est réservée aux notes.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. User

   Vous trouverez ci-dessous les propriétés de l’objet utilisateur.

<table>
 <tbody>
  <tr>
   <td><strong>Propriété</strong></td>
   <td><strong>Client uniquement</strong></td>
   <td><strong>Commentaires</strong></td>
  </tr>
  <tr>
   <td>adresse<br type="_moz" /> </td>
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
   <td>Liste du groupe de l’utilisateur.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>displayName<br type="_moz" /> </td>
   <td>F</td>
   <td>Nom de l’utilisateur.<br type="_moz" /> </td>
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
   <td>Nom de l’utilisateur.<br type="_moz" /> </td>
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
   <td>Nom de l’organisation de l’utilisateur.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>postalAddress<br type="_moz" /> </td>
   <td>F</td>
   <td>Adresse postale de l’utilisateur.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>téléphone<br type="_moz" /> </td>
   <td>F</td>
   <td>Numéro de contact de l’utilisateur.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>telephoneNumber<br type="_moz" /> </td>
   <td>F</td>
   <td>Numéro de contact de l’utilisateur.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>userid<br type="_moz" /> </td>
   <td>F</td>
   <td>Identifiant de connexion de l’utilisateur.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>
