---
title: Description de l’objet JSON de l’espace de travail AEM Forms
description: Informations conceptuelles sur les objets JavaScript JSON utilisés dans l’espace de travail AEM Forms LiveCycle pour la personnalisation, l’extension, la modification et la réutilisation.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: f837a2b3-4650-4261-84c6-291bb2a46dc7
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '2144'
ht-degree: 100%

---

# Description de l’objet JSON de l’espace de travail AEM Forms {#aem-forms-workspace-json-object-description}

Les objets JSON utilisés dans l’espace de travail AEM Forms sont décrits ci-dessous.

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
   <td>Contient l’OID de la catégorie parente<br type="_moz" />. </td>
  </tr>
  <tr>
   <td>startPointsList<br type="_moz" /> </td>
   <td>T</td>
   <td>Contient la liste de tous les points de départ présents dans une catégorie.</td>
  </tr>
  <tr>
   <td>categoryList</td>
   <td>T</td>
   <td>Contient la liste des catégories enfants directes d’une catégorie<br type="_moz" />. </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Tous les points de départ et favoris sont des catégories qui sont définies côté client. La catégorie Favoris contient tous les points de départ qui sont marqués par l’utilisateur comme favoris. La catégorie Tous les points de départ contient tous les points de départ.

1. Point de départ

   Le point de départ permet de démarrer un processus à partir de l’espace de travail lors de l’appel.

   | **Propriété** | **Client uniquement** | **Commentaires** |
   |---|---|---|
   | categoryId | F | Contient l’identifiant de la catégorie à laquelle appartient le point de départ. |
   | description | F | Contient la description d’un point de départ. |
   | name | F | Contient le nom du point de départ. |
   | serializedImageTicket | F | Contient le ticket de l’image correspondant au point de départ. Le ticket de cette image est utilisé dans le champ imageUrl du point de départ, pour obtenir l’image pour le point de départ à partir du serveur. |
   | serviceName | F | Contient le nom du service pour le point de départ. |
   | startpointId | F | Contient l’identifiant du point de départ. |
   | isFavorite | T | Indique si le point de départ est un favori ou non. True si le point de départ est favori, sinon false. |
   | isDefaultImage | T | Indique s’il existe une image spécifiée pour le processus ou non. True si aucune image n’est associée au processus, sinon false. |
   | task | T | Contient la tâche créée lorsque le point de départ est appelé. |
   | imageUrl | T | Contient l’URL de l’image correspondant au point de départ. |

1. Tâche

   Les tâches sont attribuées aux utilisateurs/groupes et comprennent une interface utilisateur (un formulaire ou un guide - déconseillé) qui peut être renseignée avec des données. Lorsque des utilisateurs et des utilisatrices se voient attribuer une tâche, ils reçoivent le formulaire ou le guide à remplir et à envoyer.

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
   <td>La classe de tâche est « LC8 » lorsque la tâche est lc8, sinon « standard ».<br /> </td>
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
   <td>Contient l’identifiant de la personne qui a créé la tâche.<br /> </td>
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
   <td>Contient l’ID d’un groupe auquel la tâche peut être transmise. Il est défini lors de la conception du processus.<br /> </td>
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
   <td>True si le formulaire de tâche doit être ouvert pour terminer la tâche.<br /> </td>
  </tr>
  <tr>
   <td>isOpenFullScreen<br /> </td>
   <td>F</td>
   <td>Si la valeur est true, à l’ouverture de la tâche, le formulaire occupe l’écran tout entier la première fois.<br /> </td>
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
   <td>Horodatage pour le rappel suivant.<br /> </td>
  </tr>
  <tr>
   <td>priority<br /> </td>
   <td>F</td>
   <td>Contient la priorité de la tâche.<br /> 1 = priorité la plus élevée<br /> 2 = priorité élevée<br /> 3 = priorité normale<br /> 4 = faible priorité<br /> 5 = priorité la plus faible<br /> </td>
  </tr>
  <tr>
   <td>processInstanceId</td>
   <td>F</td>
   <td>ID de l’instance de processus dont la tâche fait partie.<br /> </td>
  </tr>
  <tr>
   <td>processusInstanceStatus<br /> </td>
   <td>F</td>
   <td>Statut de l’instance de processus de la tâche.<br /> </td>
  </tr>
  <tr>
   <td>reminderCount<br /> </td>
   <td>F</td>
   <td>Contient le nombre de rappels pour la tâche.<br /> </td>
  </tr>
  <tr>
   <td>routeList<br /> </td>
   <td>F</td>
   <td>Contient la liste des itinéraires associée à la tâche. L’utilisateur ou l’utilisatrice peut effectuer la tâche en sélectionnant l’un des itinéraires dans la liste des itinéraires.<br /> </td>
  </tr>
  <tr>
   <td>selectedRoute<br /> </td>
   <td>F</td>
   <td>Il contient le nom de l’itinéraire sélectionné une fois la tâche terminée.<br /> </td>
  </tr>
  <tr>
   <td>serializedImageTicket<br /> </td>
   <td>F</td>
   <td>Contient le ticket de l’image correspondant à la tâche. Le ticket de cette image est utilisé dans le champ imageUrl de la tâche, pour obtenir l’image pour la tâche à partir du serveur.<br /> <br /> </td>
  </tr>
  <tr>
   <td>serviceName<br /> </td>
   <td>F</td>
   <td>Il contient le nom du service pour la tâche.<br /> </td>
  </tr>
  <tr>
   <td>serviceTitle<br /> </td>
   <td>F</td>
   <td>Il contient le titre du service pour la tâche.<br /> </td>
  </tr>
  <tr>
   <td>status<br /> </td>
   <td>F</td>
   <td>1 = Créé (la tâche est créée à partir du point de départ.)<br /> 2 = Créé et enregistré (la tâche est créée à partir du point de départ et enregistrée.)<br /> 3 = Affecté (la tâche est affectée à l’utilisateur ou l’utilisatrice une fois le processus démarré.)<br /> 4 = Affecté et enregistré (la tâche est affectée et enregistrée.)<br /> 100 = Terminé (la tâche est terminée.)<br /> 101 = Date limite (la tâche a atteint la date limite.)<br /> 102 = Terminé<br /> </td>
  </tr>
  <tr>
   <td>stepName<br /> </td>
   <td>F</td>
   <td>Il contient le nom de la tâche définie lors de la conception du processus.<br /> </td>
  </tr>
  <tr>
   <td>summaryUrl<br /> </td>
   <td>F</td>
   <td>Il contient l’URL du résumé de la tâche.<br /> </td>
  </tr>
  <tr>
   <td>taskACL<br /> </td>
   <td>F</td>
   <td>Il s’agit d’une liste de contrôle d’accès pour une tâche.<br /> </td>
  </tr>
  <tr>
   <td>taskId<br /> </td>
   <td>F</td>
   <td>ID d’une tâche.<br /> </td>
  </tr>
  <tr>
   <td>updateTime<br /> </td>
   <td>F</td>
   <td>Horodatage de la dernière mise à jour de la tâche.<br /> </td>
  </tr>
  <tr>
   <td>formUrl<br /> </td>
   <td>T</td>
   <td>Il contient l’URL du formulaire d’une tâche.<br /> </td>
  </tr>
  <tr>
   <td>taskFormType<br /> </td>
   <td>T</td>
   <td>Contient un type de formulaire de tâche. En utilisant ce champ, la tâche est rendue sur le client sous forme de pdf, de formulaire swf, etc.<br /> </td>
  </tr>
  <tr>
   <td>showDirectActions<br /> </td>
   <td>T</td>
   <td>Si True, les actions d’itinéraire sont visibles dans l’espace de travail.<br /> </td>
  </tr>
  <tr>
   <td>showACLActions<br /> </td>
   <td>T</td>
   <td>Si True, les actions telles que transférer, consulter et partager sont visibles dans l’espace de travail.<br /> </td>
  </tr>
  <tr>
   <td>supportsOffline<br /> </td>
   <td>T</td>
   <td>Si la valeur est true, le formulaire peut être déconnecté. Ceci concerne uniquement les formulaires PDF.<br /> </td>
  </tr>
  <tr>
   <td>supportsSave<br /> </td>
   <td>T</td>
   <td>Si true, l’utilisateur ou l’utilisatrice peut enregistrer la tâche.<br /> </td>
  </tr>
  <tr>
   <td>readerSubmitOptions<br /> </td>
   <td>T</td>
   <td>Cet objet contient des options qui sont utilisées pour soumettre des formulaires PDF via un lecteur dans le cas où le formulaire PDF ne contient pas de bouton de soumission.<br /> </td>
  </tr>
  <tr>
   <td>isDefaultImage<br /> </td>
   <td>T</td>
   <td>Indique s’il existe une image spécifiée pour le processus ou non. True s’il n’y a pas d’image associée au processus, sinon false.<br /> </td>
  </tr>
  <tr>
   <td>historyTaskList<br /> </td>
   <td>T</td>
   <td>Contient la liste des tâches utilisées dans l’onglet historique des détails des tâches.<br /> </td>
  </tr>
  <tr>
   <td>isOwner<br /> </td>
   <td>T</td>
   <td>True si la personne connectée est propriétaire de la tâche.<br /> </td>
  </tr>
  <tr>
   <td>availableCommands<br /> </td>
   <td>T</td>
   <td>Contient toutes les actions qui peuvent être entreprises sur la tâche.<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.directCommands<br /> </td>
   <td>T</td>
   <td>Contient toutes les actions d’itinéraire disponibles pour une tâche.<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.taskACLCommands<br /> </td>
   <td>T</td>
   <td>Contient des commandes telles que transférer, partager et consulter si disponible pour une tâche.<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.otherCommands<br /> </td>
   <td>T</td>
   <td>Contient des commandes telles que verrouiller, déverrouiller, abandonner, retourner, réclamer, etc., selon leur disponibilité.<br /> </td>
  </tr>
  <tr>
   <td>processInstanceInfo<br /> </td>
   <td>T</td>
   <td>Contient des informations sur l’instance de processus de la tâche.<br /> </td>
  </tr>
  <tr>
   <td>processVariables<br /> </td>
   <td>T<br /> </td>
   <td>Contient un tableau d’objets de variables de processus, le cas échéant.<br /> </td>
  </tr>
  <tr>
   <td>pendingTasks<br /> </td>
   <td>T</td>
   <td>Contient la liste des tâches en attente pour l’instance de processus de la tâche.<br /> </td>
  </tr>
  <tr>
   <td>userActions<br /> </td>
   <td>T</td>
   <td>Tableau d’objets. Chaque objet contient des informations sur l’itinéraire et son message de confirmation correspondant, le cas échéant.<br /> </td>
  </tr>
  <tr>
   <td>dataUrl<br /> </td>
   <td>T</td>
   <td>URL des données du formulaire d’une tâche.<br /> </td>
  </tr>
  <tr>
   <td>externalAppConfig<br /> </td>
   <td>T</td>
   <td>Il s’agit d’une configuration pour les formulaires de candidature tiers.<br /> </td>
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

   Le filtre est en principe la file d’attente de l’utilisateur ou du groupe. Lorsqu’une tâche est attribuée à une personne/un groupe, celle-ci est ajoutée dans la file d’attente correspondante.

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
   <td>True si la file d'attente est la file d’attente par défaut de la personne connectée, sinon false.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>name<br type="_moz" /> </td>
   <td>F</td>
   <td>Nom du ou de la propriétaire de la file d'attente.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>qid</td>
   <td>F</td>
   <td>Identifiant de la file d’attente.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>type</td>
   <td>F</td>
   <td>Contient le type de file d’attente.<br />0 - File d’attente de l’utilisateur ou de l’utilisatrice.<br /> 1. File d’attente partagée.<br /> 2. File d’attente de groupe.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>query</td>
   <td>T</td>
   <td>Contient la requête associée à un filtre. Cette requête est utilisée pour rechercher des tâches dans une liste de tâches complète.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>tasks</td>
   <td>T</td>
   <td>Contient la liste de toutes les tâches appartenant à un filtre.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Absence du bureau

   Vous pouvez gérer votre planning d&#39;absence du bureau et contrôler le flux des tâches qui vous sont affectées en votre absence.

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
   <td>True s’il n’y a pas de désignation principale si l’utilisateur ou l’utilisatrice n’est pas au bureau.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isOutOfOffice<br type="_moz" /> </td>
   <td>F</td>
   <td>True si l’utilisateur ou l’utilisatrice n’est pas au bureau.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>outOfOfficeDesignate<br type="_moz" /> </td>
   <td>F</td>
   <td>Contient les informations sur l’utilisateur ou l’utilisatrice désignés comme responsable principal par l’utilisateur ou l’utilisatrice.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processSpecificDesignates<br type="_moz" /> </td>
   <td>F</td>
   <td>Contient un tableau d’objets pour la désignation d’absence du bureau propre à un processus. Dans chaque objet de désignation propre à un processus, processName contient le nom du processus, isNotDesignated est défini sur true si aucun utilisateur n’est affecté au processus correspondant, et userDesignated est défini sur null si aucun utilisateur n’a affecté de détails else de l’utilisateur affecté au processus correspondant.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processes<br type="_moz" /> </td>
   <td>T</td>
   <td>Contient une liste de tous les processus disponibles pour l’utilisateur ou l’utilisatrice.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>initialOutOfOfficeSettings<br type="_moz" /> </td>
   <td>T</td>
   <td>Contient les paramètres d’absence du bureau initiaux de l’utilisateur ou de l’utilisatrice qui sont récupérés au départ.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>outOfOfficeSettings<br type="_moz" /> </td>
   <td>T</td>
   <td>Contient les paramètres d’absence du bureau modifiés.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>userSearchHistory<br type="_moz" /> </td>
   <td>T</td>
   <td>Contient une liste d’utilisateurs et d’utilisatrices recherchés par un utilisateur ou une utilisatrice connecté jusqu’à ce jour.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Instance de processus

   Une instance de processus est créée lorsqu’un processus est appelé via un espace de travail ou un workbench.

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
   <td>initiator</td>
   <td>F</td>
   <td>Nom de l’initiateur ou de l’initiatrice d’une instance de processus.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>initiatorId</td>
   <td>F</td>
   <td>ID de l’initiateur ou de l’initiatrice de l’instance de processus.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processCompleteTime<br type="_moz" /> </td>
   <td>F</td>
   <td>Horodatage lorsque le processus est terminé.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processInstanceId<br type="_moz" /> </td>
   <td>F</td>
   <td>Identifiant de l’instance de processus.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processInstanceStatus<br type="_moz" /> </td>
   <td>F</td>
   <td>0 = initié<br /> 1 = en cours d’exécution<br /> 2 = terminé<br /> 3 = en cours d’achèvement <br /> 4 = interrompu<br /> 5 = en cours d’interruption<br /> 6 = suspendu<br /> 7 = en cours de suspension <br /> 8 = en cours d’annulation de la suspension<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processName<br type="_moz" /> </td>
   <td>F</td>
   <td>Nom du processus.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processStartTime<br type="_moz" /> </td>
   <td>F</td>
   <td>Horodatage du démarrage du processus.<br type="_moz" /> </td>
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

1. Objet d’affectation de tâches

   L’objet Affectation de tâche contient des informations sur l’affectation d’une tâche. Voici les propriétés de l’affectation de la tâche.

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
   <td>Horodatage de la création de cette affectation de tâche.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>assignmentType<br type="_moz" /> </td>
   <td>F</td>
   <td>0 = affectation initiale<br /> 1 = Transférer (la tâche a été transférée à la propriétaire ou au propriétaire actuel de la tâche.)<br /> 2 = Renvoyé (la tâche a été renvoyée à la propriétaire ou au propriétaire actuel de la tâche par la ou le propriétaire précédent de la tâche.)<br /> 3 = Réclamé (la tâche a été réclamée par la ou le propriétaire actuel de la tâche.)<br /> 4 = Réaffectation (la tâche a été affectée à la propriétaire ou au propriétaire actuel de la tâche après réaffectation.)<br /> 5 = Administrateur ou administratrice attribué (la tâche a été attribuée par l’administrateur ou l’administratrice à la propriétaire ou au propriétaire actuel de la tâche.)<br /> 6 = Consulté (la tâche a été consultée par la ou le propriétaire actuel de la tâche.)<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>assignmentUpdateTime<br type="_moz" /> </td>
   <td>F</td>
   <td>Horodatage de la mise à jour de cette affectation d’une tâche.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>queueId<br type="_moz" /> </td>
   <td>F</td>
   <td>ID de la file d’attente de la ou du propriétaire actuel de la tâche.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>queueOwner<br type="_moz" /> </td>
   <td>F</td>
   <td>Nom de la propriétaire ou du propriétaire actuel de la tâche.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>queueOwnerId<br type="_moz" /> </td>
   <td>F</td>
   <td>ID de la propriétaire ou du propriétaire actuel de la tâche.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Objet ACL de tâche

   L’objet ACL de tâche contient des informations sur les autorisations telles que le transfert, le partage, la consultation, etc., d’une tâche. Voici les propriétés de l’ACL de la tâche.

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
   <td>Si true, les pièces jointes peuvent être ajoutées à la tâche.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canAddNotes<br type="_moz" /> </td>
   <td>F</td>
   <td>Si true, des notes peuvent être ajoutées à la tâche.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canClaim<br type="_moz" /> </td>
   <td>F</td>
   <td>Si true, la tâche peut être réclamée.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canConsult<br type="_moz" /> </td>
   <td>F</td>
   <td>Si true, la tâche peut être consultée.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canForward<br type="_moz" /> </td>
   <td>F</td>
   <td>Si true, la tâche peut être transférée.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canShare<br type="_moz" /> </td>
   <td>F</td>
   <td>Si true, la tâche peut être partagée.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Pièce jointe de la tâche

   Des pièces jointes peuvent être ajoutées à une tâche. Une pièce jointe peut être de type pièce jointe et note. Voici les propriétés de l’objet de pièce jointe.

<table>
 <tbody>
  <tr>
   <td><strong>Propriété</strong></td>
   <td><strong>Client uniquement</strong></td>
   <td><strong>Commentaires</strong></td>
  </tr>
  <tr>
   <td>creationDate<br type="_moz" /> </td>
   <td>F</td>
   <td>Horodatage lors de la création de la pièce jointe.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>creatorId<br type="_moz" /> </td>
   <td>F</td>
   <td>ID de la personne qui a ajouté la pièce jointe.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>creatorName<br type="_moz" /> </td>
   <td>F</td>
   <td>Nom de la personne qui a ajouté la pièce jointe.<br type="_moz" /> </td>
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
   <td>Horodatage de la dernière modification de la pièce jointe.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>noteExtended<br type="_moz" /> </td>
   <td>F</td>
   <td>Si true, la note est une note étendue (longue).<br type="_moz" /> </td>
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
   <td>ID de la tâche à laquelle la pièce jointe est ajoutée.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>type<br type="_moz" /> </td>
   <td>F</td>
   <td>Le type est « attachment » pour les fichiers et « note » pour les notes.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedCreationDate<br type="_moz" /> </td>
   <td>T</td>
   <td>Contient la date de création de la pièce jointe en fonction des paramètres de l'interface utilisateur de la personne.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedDescription<br type="_moz" /> </td>
   <td>T</td>
   <td>Description de la pièce jointe formatée. Utilisé pour afficher les caractères spéciaux présents dans la description de la pièce jointe dans l’espace de travail AEM Forms.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedFileName<br type="_moz" /> </td>
   <td>T</td>
   <td>Nom de la pièce jointe formatée. Utilisé pour afficher les caractères spéciaux présents dans le nom de la pièce jointe dans l’espace de travail AEM Forms. Ceci est uniquement destiné aux notes.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. User

   Voici les propriétés de l’objet utilisateur.

<table>
 <tbody>
  <tr>
   <td><strong>Propriété</strong></td>
   <td><strong>Client uniquement</strong></td>
   <td><strong>Commentaires</strong></td>
  </tr>
  <tr>
   <td>address<br type="_moz" /> </td>
   <td>F</td>
   <td>Adresse de la personne.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>commonName<br type="_moz" /> </td>
   <td>F</td>
   <td>Nom commun de l’utilisateur ou de l’utilisatrice.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>description<br type="_moz" /> </td>
   <td>F</td>
   <td>Description de l’utilisateur ou de l’utilisatrice.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>directGroupMemberships<br type="_moz" /> </td>
   <td>F</td>
   <td>Liste du groupe de l’utilisateur ou de l’utilisatrice.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>displayName<br type="_moz" /> </td>
   <td>F</td>
   <td>Nom d’affichage de l’utilisateur ou de l’utilisatrice.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>email<br type="_moz" /> </td>
   <td>F</td>
   <td>Identifiant e-mail de l’utilisateur ou de l’utilisatrice.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isOutOfOffice<br type="_moz" /> </td>
   <td>F</td>
   <td>True si la personne est absente du bureau.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>lastName<br type="_moz" /> </td>
   <td>F</td>
   <td>Nom de famille de la personne.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>firstName<br type="_moz" /> </td>
   <td>F</td>
   <td>Prénom de la personne.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>oid<br type="_moz" /> </td>
   <td>F</td>
   <td>ID de l’utilisateur ou de l’utilisatrice.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>org<br type="_moz" /> </td>
   <td>F</td>
   <td>Nom de l’organisation de l’utilisateur ou de l’utilisatrice.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>postalAddress<br type="_moz" /> </td>
   <td>F</td>
   <td>Adresse postale de la personne.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>telephone<br type="_moz" /> </td>
   <td>F</td>
   <td>Numéro de contact de la personne.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>telephoneNumber<br type="_moz" /> </td>
   <td>F</td>
   <td>Numéro de contact de la personne.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>userid<br type="_moz" /> </td>
   <td>F</td>
   <td>Identifiant de connexion de l’utilisateur ou de l’utilisatrice.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>
