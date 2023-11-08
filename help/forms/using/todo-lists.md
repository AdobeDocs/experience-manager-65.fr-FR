---
title: Utilisation des listes de tâches
seo-title: Working with To-do lists
description: Comment ouvrir, travailler et effectuer les tâches selon les besoins, par exemple approuver ou rejeter une demande ou ajouter des informations supplémentaires.
seo-description: How to open, work on, and complete the tasks as required, such as approving or rejecting a request or adding more information.
uuid: f9cfad8e-5d0c-4a30-8153-2a03bf7dd986
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: d8546227-d78d-4fe2-a092-222482bb69c9
docset: aem65
exl-id: c80bf347-d1ed-488f-a41a-ceb05a6df9e4
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '4031'
ht-degree: 47%

---

# Utilisation des listes de tâches{#working-with-to-do-lists}

Lorsque vous affichez vos listes de tâches, vous pouvez visualiser les tâches d’un processus d’entreprise qui vous sont affectées, ou qui sont affectées à des groupes auxquels vous appartenez, ou qui sont les tâches partagées d’autres utilisateurs. Vous pouvez ouvrir, modifier et effectuer les tâches selon vos besoins, par exemple en approuvant ou en rejetant une demande ou en ajoutant davantage d’informations. Une fois la tâche terminée, elle est envoyée à la personne suivante du processus d’entreprise.

## A propos des listes de tâches {#about-todo-lists}

L’espace de travail AEM Forms comporte les trois types de listes de tâches suivants :

* Des listes individuelles, qui contiennent des tâches qui vous sont affectées directement.
* Listes de groupe, qui contiennent des tâches affectées à un groupe. Tout membre du groupe peut ouvrir et exécuter les tâches. Pour ouvrir une tâche, un membre d’un groupe doit d’abord demander la tâche.
* Listes partagées, qui contiennent des tâches affectées à un utilisateur ayant partagé sa liste de tâches avec vous et probablement avec d’autres utilisateurs. Tous les utilisateurs qui partagent une liste peuvent demander, ouvrir et terminer des tâches partagées.

Vous pouvez effectuer certaines actions sans ouvrir la tâche en cliquant sur les icônes qui apparaissent lorsque vous placez le pointeur sur une tâche.

>[!NOTE]
>
>Une icône d’exclamation indique que la tâche est prioritaire.

## Tâches standard {#typical-tasks}

Lors de l’ouverture et de l’utilisation d’une tâche, les outils disponibles dépendent de la tâche. Des tâches différentes nécessitent d’effectuer des actions différentes, par conséquent certains outils peuvent être disponibles ou non. Les tâches courantes que vous pouvez recevoir sont décrites ci-dessous.

* **Fournir des informations**: vous recevez une tâche qui nécessite de remplir et d’envoyer un formulaire.

* **Informations sur la révision**: vous recevez une tâche qui nécessite de consulter les informations et de valider le contenu.

* **Révision multi-utilisateurs** : vous recevez une tâche en même temps que d’autres utilisateurs. Vous devez, ainsi que les autres utilisateurs, fournir des informations, réviser le contenu ou les deux. Les outils suivants peuvent être disponibles avec ce type de tâche :

   * Affichage des instructions de la tâche
   * Affichage de l’état d’achèvement de tous les utilisateurs auxquels la tâche est affectée
   * Affichage des commentaires de tous les utilisateurs auxquels la tâche est affectée
   * Ajouter vous-même des commentaires à la tâche

Voici d’autres outils qui peuvent être disponibles avec l’une des tâches ci-dessus :

* Transférer
* Partager
* Consulter
* Retour
* Remarques
* Pièces jointes

## Ouverture de tâches {#opening-tasks}

Vous pouvez ouvrir et verrouiller des tâches à partir de votre liste de tâches ou demander et ouvrir des tâches à partir de la liste de tâches d’un groupe ou partagée. Lorsque vous ouvrez une tâche, elle s’affiche sur le panneau principal. Les autres tâches sont affichées dans la liste des tâches en regard de celle-ci.

S’il existe une URL Résumé de la tâche, la vue Résumé de la tâche s’ouvre par défaut, au lieu du formulaire associé à une tâche. Même lorsqu’un utilisateur active l’option &quot;Ouvrir le formulaire en mode agrandi&quot; dans Assign Task, le formulaire ne s’ouvre pas en mode agrandi.

>[!NOTE]
>
>Lorsque vous ouvrez une tâche, en fonction des paramètres par défaut de la tâche, le formulaire associé peut s’afficher en plein écran.

### Ouvrir et verrouiller une tâche de votre liste {#open-and-lock-a-task-from-your-list}

Lorsque vous ouvrez une tâche à partir de votre liste de tâches, si votre liste est partagée, vous pouvez verrouiller la tâche pour empêcher un autre utilisateur ayant accès à votre liste de travailler sur la tâche.

1. Sur la page des tâches, dans le volet de gauche, sélectionnez votre liste de tâches individuelle. Toutes vos tâches s’affichent dans le volet central.

   >[!NOTE]
   >
   >Vous pouvez filtrer les tâches en sélectionnant le type de processus dans la liste de tâches. Vous pouvez sélectionner votre liste de tâches pour afficher à nouveau toutes les tâches de la liste de tâches.

1. Si nécessaire, verrouillez votre tâche. Pour verrouiller une tâche, cliquez sur l’icône Toutes les options sur la tâche et sélectionnez Verrouiller. Placez le pointeur sur la tâche pour que l’option soit disponible.

   >[!NOTE]
   >
   >Vous pouvez également verrouiller ou déverrouiller une tâche sur n’importe quel onglet lorsque la tâche est ouverte.

   ![lock_task](assets/lock_task.png)

   Menu Toutes les options sur une tâche

1. Ouvrez la tâche en cliquant dessus.

### Ouvrir et demander une tâche à partir d’une liste partagée ou de groupe {#open-and-claim-a-task-from-a-shared-or-group-list}

Lorsque vous ouvrez et demandez une tâche à partir de la liste d’un groupe ou partagée, la tâche est déplacée de la liste du groupe ou de la liste partagée vers votre liste de tâches individuelle. Les autres utilisateurs ayant accès à la liste ne peuvent pas travailler sur la tâche.

1. Sur la page des tâches, dans le volet de gauche, sélectionnez la liste des tâches d’un groupe ou partagée. Toutes les tâches s’affichent dans le volet central.
1. Effectuez l’une des étapes suivantes :

   * Pour demander une tâche, sans l’ouvrir, à partir de la liste de tâches d’un groupe ou partagée, cliquez sur **Demander** en plaçant le pointeur de la souris sur la tâche. Lorsque la tâche est ouverte, le bouton Demander est disponible également dans la barre d’actions située sous le volet des tâches. Lors de la demande, une tâche passe de la liste de tâches du groupe ou partagée à votre liste.
   * Pour demander et ouvrir une tâche depuis une liste de tâches de groupe ou partagée, cliquez sur **Demander et ouvrir**.

## Utiliser les tâches {#working-with-tasks}

Après l’ouverture d’une tâche, les onglets qui s’affichent dans le volet principal et les outils disponibles dépendent de la tâche. Les onglets que vous pouvez voir sont décrits ci-dessous :

* **Résumé des tâches**: lorsqu’une tâche s’ouvre, le volet Résumé de la tâche vous permet d’afficher des informations sur la tâche, le cas échéant, à l’aide d’une URL spécifiée dans le processus à l’étape Affecter une tâche . Le volet Résumé de la tâche permet d’afficher des informations pertinentes supplémentaires, afin d’augmenter l’intérêt d’AEM Forms Workspace pour l’utilisateur final. Cet onglet n’est pas disponible si l’URL Résumé de la tâche n’existe pas.

* **Détails**: fournit des informations sur la tâche en cours et le processus auquel elle appartient.

* **Formulaire** : affiche le formulaire associé à la tâche. Le formulaire peut correspondre à de nombreux types de fichier, y compris PDF, HTML, Guide et fichier SWF. Le formulaire peut ressembler à un formulaire Web ou imprimable standard, ou peut vous guider à travers une série de panneaux de style assistant pour recueillir des informations.

* **Histoire**: répertorie les tâches qui font partie de l’instance de processus et le formulaire, les affectations de tâche et les pièces jointes associés à chaque tâche.

* **Pièces jointes**: affiche les pièces jointes existantes associées à la tâche et ajoute des pièces jointes, si nécessaire.

* **Remarques**: affiche les notes existantes associées à la tâche et ajoute des notes, si nécessaire.

Lorsque vous travaillez sur une tâche, les outils que vous pouvez voir et les actions que vous pouvez effectuer sont décrits ci-dessous.

### Transférer, partager ou consulter une tâche {#forward-share-or-consult-on-a-task}

Vous pouvez transférer une tâche accompagnée de notes ou de pièces jointes à un autre utilisateur, partager la tâche avec un autre utilisateur, ou consulter un autre utilisateur à propos de la tâche. Si vous modifiez les données de formulaire associées à une tâche, enregistrez le formulaire en tant que brouillon avant de transférer la tâche, de la partager ou de la consulter. Dans le cas contraire, la tâche sera envoyée sans le formulaire mis à jour. Après avoir transféré la tâche ou l’avoir partagée, l’utilisateur qui reçoit la tâche peut la demander et l’exécuter ou vous la renvoyer. Si vous consultez une tâche, l’utilisateur ne peut que vous renvoyer la tâche.

1. Si vous modifiez un formulaire associé à une tâche que vous souhaitez conserver, cliquez sur **Enregistrer**. L’option Enregistrer est disponible dans la barre d’action située dans la partie inférieure de chaque onglet. Dans le cas contraire, la tâche sera envoyée sans le formulaire mis à jour.

   >[!NOTE]
   >
   >Le bouton Enregistrer n’est pas disponible pour certains formulaires, selon la tâche sur laquelle vous travaillez.

1. Sur n’importe quel onglet, cliquez sur l’un des boutons suivants :

   * **Transférer**
   * **Partager**
   * **Consulter**

   >[!NOTE]
   >
   >Selon la tâche, vous pouvez également effectuer ces actions à partir de la liste de tâches sans ouvrir la tâche.

1. Dans la boîte de dialogue contextuelle, recherchez et sélectionnez le nom de l’utilisateur avec lequel transférer, partager ou consulter la tâche.

### Renvoie une tâche {#return-a-task}

1. Sur n’importe quel onglet, cliquez sur **Renvoyer**. La tâche est renvoyée à la liste des tâches de l’utilisateur qui vous a précédemment transféré la tâche, ou qui a partagé ou consulté la tâche avec vous.

### Mettre une tâche hors ligne {#take-a-task-offline}

Vous pouvez être autorisé à travailler sur une tâche hors ligne puis à envoyer ultérieurement son formulaire à partir d’Adobe® Reader® ou Adobe® Acrobat® Professional ou Adobe® Acrobat® Standard. L’envoi du formulaire déclenche le démarrage de votre client de messagerie avec l’adresse électronique de serveur appropriée. Vous pouvez ensuite envoyer le formulaire complété au serveur par courrier électronique.

1. Sur n’importe quel onglet, cliquez sur **Hors connexion**.
1. Spécifiez un nom de fichier pour l’enregistrement du formulaire et cliquez sur **Enregistrer**. Le formulaire associé à la tâche est enregistré localement et la tâche reste dans votre liste de tâches jusqu’à ce que le formulaire soit envoyé.

### Utilisation de pièces jointes {#work-with-attachments}

Vous pouvez être autorisé à ajouter, mettre à jour, supprimer ou enregistrer les pièces jointes localement.

**Ajouter une pièce jointe**

1. Dans le **Pièces jointes** Onglet Clic **Parcourir** pour sélectionner le fichier à joindre.
1. Sélectionnez le niveau des **Autorisations** relatives à la pièce jointe pour les autres utilisateurs participant au processus. Si vous sélectionnez **Lecture**, d’autres utilisateurs peuvent enregistrer le fichier localement. Si vous sélectionnez l’une des autorisations de modification, d’autres utilisateurs peuvent également charger un nouveau fichier pour remplacer votre pièce jointe.

   >[!NOTE]
   >
   >Vous pouvez également ajouter des commentaires avec vos pièces jointes.

1. Cliquez sur **Charger**. Le fichier est attaché au formulaire.

**Afficher une pièce jointe**

1. Sur le **Pièces jointes** cliquez sur le nom de fichier de la pièce jointe à afficher.

**Enregistrer une pièce jointe localement**

1. Cliquez sur une pièce jointe pour l’ouvrir. Enregistrez la pièce jointe ouverte localement.

**Mettre à jour une pièce jointe**

1. Cliquez sur **Modifier** pour la pièce jointe. Sélectionnez le fichier avec lequel remplacer la pièce jointe existante, en cliquant sur **Parcourir**.

**Supprimer une pièce jointe**

1. Cliquez sur **Supprimer** pour une pièce jointe.

### Enregistrez votre travail sans terminer la tâche {#save-your-work-without-completing-the-task}

1. Sur n’importe quel onglet, appuyez sur **Enregistrer**.

   La boîte de dialogue Enregistrer en tant que brouillon s’affiche. Le nom par défaut du brouillon est le nom de la tâche du modèle de tâche.

   ![saveasdraftdialog](assets/saveasdraftdialog.png)

   >[!NOTE]
   >
   >vous pouvez configurer l’espace de travail afin qu’il enregistre automatiquement les informations saisies par l’utilisateur en tant que brouillon. Si l’enregistrement automatique est activé et qu’un utilisateur travaille sur un brouillon, ce dernier est enregistré de manière périodique. En cas d’enregistrement automatique, le nom par défaut de la tâche est automatiquement renseigné.
   >
   >
   >Pour en savoir plus, consultez Enregistrer régulièrement le brouillon dans [Gestion des préférences](/help/forms/using/getting-started-livecycle-html-workspace.md).

1. Dans la boîte de dialogue Enregistrer comme brouillon, spécifiez un nom unique pour la tâche et appuyez sur **OK.**

   ![saveasdraftdialog_name](assets/saveasdraftdialog_name.png)

   Le brouillon est enregistré avec le nom spécifié. La tâche demeure dans votre liste de tâches et les modifications que vous avez effectuées dans le formulaire sont enregistrées dans le dossier Brouillons. De plus, dans votre liste de tâches, vous pouvez rechercher le brouillon à l’aide du nom du brouillon pour reprendre à travailler dessus.

   ![searchfortask](assets/searchfortask.png)

## Réalisation des tâches {#completing-tasks}

La manière dont vous exécutez une tâche dépend de la tâche et de votre rôle dans le processus. Il peut vous être demandé d’approuver ou de refuser une demande, de fournir du contenu, d’examiner et de vérifier des informations ou d’indiquer que vous avez agi.

Vous pouvez effectuer une tâche de différentes manières :

* Utilisation des actions disponibles dans l’un des onglets
* Utilisation des actions créées dans le formulaire lui-même
* Dans votre liste de tâches, sans ouvrir la tâche

>[!NOTE]
>
>Cette option est disponible si le champ `isMustOpenToComplete` n’est pas sélectionné à l’étape `Assign Task` dans Workbench, lors de la conception d’un processus.

* Par email, si vous recevez des notifications par email

Lorsque vous terminez une tâche, selon la tâche, une boîte de dialogue de confirmation peut apparaître pour confirmer votre action. Par exemple, une boîte de dialogue peut s’afficher vous invitant à confirmer la validité des informations que vous avez fournies.

>[!NOTE]
>
>Si vous avez modifié une tâche, mais que vous n’êtes pas prêt à la terminer, vous pouvez enregistrer votre travail en tant que brouillon en cliquant sur Enregistrer et y revenir ultérieurement.

### Fin d’une tâche {#complete-a-task}

1. Effectuez l’une des étapes suivantes :

   * Sélectionnez la tâche et cliquez sur le bouton correspondant à l’étape suivante requise dans le processus en bas de la liste.
   * Si le formulaire ne comporte aucun bouton et que le bouton Terminer de l’espace de travail d’AEM Forms est disponible, cliquez sur **Terminer**.
   * Si le formulaire comporte des boutons et que le bouton Terminer de l’espace de travail d’AEM Forms n’est pas disponible, cliquez sur le bouton approprié du formulaire pour passer à l’étape suivante du processus.

   Si le formulaire ne comporte aucun bouton et que le bouton Terminer de l’espace de travail d’AEM Forms n’est pas disponible, un message s’affiche, indiquant que le formulaire ne peut pas être envoyé.

1. Si une boîte de dialogue de confirmation s’affiche, effectuez l’une des opérations suivantes :

   * Cliquez sur **OK** si vous avez terminé la tâche et que vous êtes prêt à la valider.
   * Cliquez sur **Annuler** si vous souhaitez revenir à la tâche et n’êtes pas prêt à la valider.

>[!NOTE]
>
>Un bouton d’envoi peut s’afficher dans les HTMLS lorsque les propriétés de processus sont utilisées dans un formulaire. Ce bouton n’est pas visible lorsque le même formulaire est rendu en tant que PDF. Pour terminer une tâche, cliquez sur le bouton Envoyer disponible en bas de l’espace de travail AEM Forms, en dehors du formulaire et non sur le bouton Envoyer du formulaire.

### Approbation des tâches en bloc {#bulk-approve-tasks}

Vous pouvez envoyer plusieurs tâches depuis votre liste de tâches. Seules les tâches du même processus, avec les mêmes noms de tâche et les mêmes options d’itinéraire peuvent être envoyées ensemble.

>[!NOTE]
>
>Cette option est disponible si le champ isMustOpenToComplete n’est pas sélectionné à l’étape Affecter une tâche dans Workbench, lors de la conception d’un processus.

1. Sur la page des tâches, dans le volet de gauche, sélectionnez votre liste de tâches individuelle. Toutes vos tâches s’affichent dans le volet central.
1. Sélectionner **Activation du mode bloc**. Les cases à cocher s’affichent devant les tâches de la liste.

   >[!NOTE]
   >
   >Cette option n’est pas disponible pour les tâches pour lesquelles le champ isMustOpenToComplete est sélectionné à l’étape Affecter une tâche dans Workbench, lors de la conception d’un processus. Les cases ces tâches dans la LISTE DE TÂCHES restent toujours désactivées.

1. Sélectionnez des tâches pour approbation en bloc. Plusieurs tâches du même processus, avec les mêmes noms de tâche et les mêmes options d’itinéraire peuvent être sélectionnées. Une fois que vous sélectionnez une tâche à approuver, seules les tâches avec le même processus, les mêmes noms de tâche et les mêmes options de routage restent activées. Le reste est désactivé.

   ![1_bulkapproval](assets/1_bulkapproval.png)

1. Cliquez sur l’option Envoyer disponible. Les tâches sélectionnées sont envoyées.

   ![bulkapproval](assets/bulkapproval.png)

## Participation aux tâches par courrier électronique {#participating-in-tasks-through-email}

Vous pouvez recevoir et effectuer les tâches par courrier électronique. La participation à des tâches par courrier électronique évite d’avoir à vérifier régulièrement votre liste de tâches pour de nouvelles tâches ou à vérifier l’état d’une tâche dans la page Suivi .

Tout d’abord, configurez vos préférences d’espace de travail d’AEM Forms de façon à recevoir des notifications par e-mail. L’espace de travail d’AEM Forms peut envoyer des notifications par e-mail pour les tâches de votre liste de tâches ou de la liste de tout groupe auquel vous appartenez. L’administrateur détermine le moment où les messages de notification électronique sont envoyés et qui les reçoit.

Les courriers électroniques peuvent contenir un lien qui ouvre la tâche dans AEM Forms Workspace, une pièce jointe du formulaire utilisé pour la tâche, ou des actions pour exécuter la tâche par courrier électronique. Si un formulaire est inclus dans le courrier électronique, vous pouvez ouvrir le formulaire et exécuter la tâche si les boutons nécessaires sont intégrés dans le formulaire. Si les actions nécessaires à l’exécution de la tâche sont incluses dans le message électronique, vous pouvez terminer la tâche en cliquant sur les actions dans le courrier électronique ou en répondant à l’email avec l’action saisie comme première ligne dans le corps de l’email.

>[!NOTE]
>
>* Pour configurer l’espace de travail de façon à utiliser les modèles d’e-mail appropriés, consultez le [Guide de l’administrateur d’AEM Forms JEE](https://help.adobe.com/fr_FR/AEMForms/6.1/AdminHelp/index.html).
>
>* Si vous transférez des brouillons après l’envoi de la tâche dans l’espace de travail AEM Forms, des notifications par e-mail sont envoyées. Si vous transférez des brouillons à partir du point de départ de l’espace de travail AEM Forms, aucune notification par e-mail n’est envoyée.

Lorsque vous exécutez une tâche par courrier électronique, la tâche est supprimée de votre liste de tâches dans AEM Forms Workspace.

>[!NOTE]
>
>Si l’utilisateur n’est pas connecté à l’espace de travail AEM Forms dans le navigateur et qu’il ouvre un lien vers une tâche de la liste des tâches, le lien direct ne parvient pas à s’ouvrir et affiche une exception. Connectez-vous à l’espace de travail AEM Forms avant de cliquer sur des liens dans les e-mails.

>[!NOTE]
>
>Vous ne pouvez pas transférer une notification par courrier électronique pour affecter une tâche à une autre personne. Vous pouvez uniquement transférer des tâches à d’autres utilisateurs depuis l’espace de travail AEM Forms.

### Réception de messages de notification par e-mail {#receive-email-notification-messages}

1. Cliquez sur **Préférences**.
1. Dans le **Notifier les événements de tâche par courrier électronique** list, select **Oui**.
1. Pour inclure le formulaire et les données au message électronique, dans la variable **Joindre Forms dans un courrier électronique** list, select **Oui**.

## Participation aux tâches par le biais des périphériques mobiles {#participating-in-tasks-through-mobile-devices}

Vous pouvez utiliser l’application d’espace de travail AEM Forms pour participer aux tâches de votre périphérique mobile. Avant d’installer l’application, vérifiez auprès de votre administrateur système que votre entreprise prend en charge l’utilisation de l’application d’espace de travail AEM Forms.

## A propos des échéances et des rappels {#about-deadlines-and-reminders}

Une *échéance* détermine la date et l’heure à laquelle vous devez avoir terminé une tâche. Lorsqu’une échéance est passée, le serveur achemine la tâche vers l’étape suivante du processus (la liste de tâches d’un autre utilisateur, par exemple), puis l’icône d’échéance s’affiche sur la tâche. L’icône d’échéance s’affiche, quelles que soient les règles associées au processus.

Un *rappel* vous informe qu’une tâche requiert votre attention. Les rappels surviennent à un moment prédéterminé, puis à intervalles réguliers, jusqu’à ce que la tâche associée soit terminée. Lorsque vous recevez un rappel, l’icône de rappel s’affiche sur la tâche.

C’est le processus d’entreprise qui détermine le comportement et la durée des échéances et des rappels. Tous les processus ne possèdent pas d’échéances et de rappels. L’administrateur définit si des courriers électroniques de notification sont envoyés pour les échéances et les rappels. Vous pouvez définir vos préférences pour recevoir ou non des notifications par e-mail.

## Utilisation des tâches des files d’attente de groupe et partagées {#working-with-tasks-from-group-and-shared-queues}

Toutes les tâches qui vous sont affectées apparaissent dans votre liste de tâches (file d’attente).

Toutes les listes de tâches de groupe ou partagées auxquelles vous avez accès s’affichent également dans le volet gauche de la page des tâches. Vous pouvez effectuer des tâches à partir de n’importe quelle liste de tâches à laquelle vous avez accès.

Une liste de tâches de groupe peut comporter plusieurs membres. Un administrateur définit les listes de tâches de groupe en fonction des besoins spécifiques de votre entreprise. Les listes de tâches de groupe permettent de répartir le travail entre plusieurs personnes partageant des responsabilités similaires.

Par exemple, chaque membre de votre équipe traite des formulaires de demande de prêt. Toutes ces tâches sont envoyées à une liste de tâches de groupe accessible à chaque membre de votre groupe. Chaque membre de votre groupe peut accéder aux tâches de cette liste de tâches.

Une liste de tâches partagée s’affiche lorsqu’un autre utilisateur partage sa liste avec vous, ou partage de façon explicite une tâche avec vous. Vous pouvez alors afficher les tâches de la liste de tâches de cet utilisateur et les exécuter à sa place. Par exemple, si vous prenez des vacances, vous pouvez choisir de partager votre liste de tâches avec un collègue qui termine vos tâches pendant votre absence.

>[!NOTE]
>
>Vous pouvez également spécifier des paramètres d’absence du bureau pour transférer des tâches à d’autres utilisateurs lorsque vous n’êtes pas sur le site.

Pour travailler sur une tâche de la liste de tâches d’un groupe ou partagée, demandez d’abord la tâche. Vous devenez ensuite le propriétaire de la tâche jusqu’à ce que vous la terminiez ou que vous la transmettiez à un autre utilisateur.

### Files d&#39;attente de partage {#sharing-queues}

Vous pouvez partager votre liste de tâches avec un autre utilisateur, qui peut alors afficher les nouvelles tâches de votre liste de tâches et agir sur celles-ci pour vous. Si votre liste de tâches comporte des tâches avant son partage, l’autre utilisateur ne peut pas les afficher. L’utilisateur peut afficher et demander uniquement les tâches qui arrivent dans votre liste de tâches après avoir autorisé l’accès à votre liste de tâches.

Pour qu’un utilisateur puisse voir une tâche dans une file d’attente partagée, le concepteur de processus doit activer l’option Ajouter une liste de contrôle d’accès pour la file d’attente partagée dans l’onglet Liste de contrôle d’accès de tâche (ACL) du service utilisateur.

>[!NOTE]
>
>Si vous prévoyez de vous absenter du bureau, vous pouvez également spécifier des paramètres d’absence du bureau pour transférer des tâches à d’autres utilisateurs pendant que vous êtes absent au lieu de partager votre liste de tâches complète.

**Partage de votre file d’attente**

1. Dans le **Files d’attente** dans le **Préférences** Cliquez sur l’icône &quot;+&quot; pour &quot;Utilisateurs partageant actuellement ma file d’attente&quot;.
1. Recherchez et sélectionnez le nom de l’utilisateur.
1. Cliquez sur **Partager** pour partager votre file d’attente avec l’utilisateur sélectionné.
1. Sélectionnez le nom de l’utilisateur, puis cliquez sur **Partager**.

   >[!NOTE]
   >
   >Vous pouvez empêcher un utilisateur de partager votre liste de tâches en cliquant sur **X** à la fin de la ligne dans laquelle l’utilisateur est répertorié.

### Accès à d’autres files d’attente {#accessing-other-queues}

Vous pouvez demander l’accès à la liste de tâches d’un autre utilisateur pour afficher et demander toute nouvelle tâche dans la liste de tâches de l’utilisateur.

Dans ce cas, l’utilisateur reçoit une tâche dans sa liste de tâches pour approuver ou refuser votre demande. Une fois la tâche terminée, vous recevez une notification dans votre liste de tâches.

Si vous avez accès à la liste des tâches d’un autre utilisateur, vous ne pouvez pas afficher les tâches qui figuraient dans cette liste avant votre autorisation d’accès. Vous pouvez afficher uniquement les tâches qui apparaissent dans la liste de tâches de l’utilisateur une fois que vous avez accès à la liste de tâches.

**Accès à une autre file d’attente**

1. Dans l’onglet **Préférences**, ouvrez l’onglet **Files d’attente**.
1. Cliquez sur « + » pour les « Files d’attente d’utilisateurs auxquelles j’ai accès ». Recherchez le nom de l’utilisateur dans la boîte de dialogue pop-up.
1. Sélectionnez le nom de l’utilisateur, puis cliquez sur **Requête**.

   >[!NOTE]
   >
   >Vous pouvez supprimer votre accès à une autre liste de tâches en sélectionnant le nom d’utilisateur dans la liste Files d’attente d’utilisateurs auxquelles j’ai accès et en cliquant sur **X** au bout de la ligne mentionnant le nom de l’utilisateur. Vous ne pouvez pas supprimer votre accès à une autre liste de tâches lorsque la demande d’accès à la liste de tâches est toujours en attente.

## Configuration des préférences d’absence du bureau {#setting-out-of-office-preferences}

Si vous prévoyez d’être absent du bureau, vous pouvez spécifier ce qu’il advient des tâches qui vous sont affectées pour cette période.

Vous pouvez spécifier une date et une heure de début, ainsi qu’une date et une heure de fin, pour l’application de vos paramètres d’absence du bureau. Si vous vous trouvez dans un fuseau horaire différent du serveur, le fuseau horaire utilisé est celui du serveur.

Vous pouvez définir une personne par défaut à laquelle toutes vos tâches sont envoyées. Vous pouvez également spécifier des exceptions pour que des tâches issues de processus spécifiques soient envoyées à un utilisateur différent ou pour qu’elles restent dans votre liste de tâches jusqu’à votre retour. Si la personne désignée est également absente du bureau, la tâche passe à l’utilisateur qu’elle a désigné. Si la tâche ne peut pas être affectée à un utilisateur qui n’est pas absent du bureau, la tâche reste dans votre liste de tâches.

>[!NOTE]
>
>Lorsque vous êtes absent du bureau, toutes les tâches qui se trouvaient auparavant dans votre liste de tâches y restent et ne sont pas transférées à d’autres utilisateurs.

### Définition des préférences d’absence du bureau {#set-out-of-office-preferences}

1. Cliquez sur **Préférences** et cliquez sur **Absence du bureau**.
1. Pour indiquer le moment où vous êtes absent du bureau, effectuez l’une des opérations suivantes :

   * Pour indiquer que vous êtes actuellement absent du bureau, et ce pour une durée indéterminée, dans la liste **Je suis actuellement**, sélectionnez **Absence du bureau** mais n’ajoutez pas de plage de dates.
   * Pour spécifier une date et une heure de début auxquelles vous êtes absent du bureau, cliquez sur « + » pour **Programme d’absence du bureau**. Utilisez le calendrier et la liste des heures pour indiquer la date et l’heure de début. Si vous ne spécifiez aucune date et heure de fin, vous êtes considéré comme absent du bureau indéfiniment à partir de la date et de l’heure de début jusqu’à ce que vous changiez vos préférences.

1. Pour spécifier comment vos tâches seront gérées par défaut, sélectionnez l’une des options suivantes dans la liste **En cas d’absence du bureau : Utilisateur par défaut pour les tâches en cas d’absence du bureau** :

   * Sélectionner **Ne pas affecter** pour conserver les tâches dans votre liste de tâches jusqu’à votre retour.
   * Sélectionnez **Rechercher un utilisateur** pour rechercher un utilisateur à qui affecter vos tâches. Lorsque vous sélectionnez un utilisateur, vous pouvez également afficher son planning d’absence du bureau.

1. Pour définir les exceptions sur la valeur par défaut, cliquez sur + pour **Exceptions de processus**, sélectionnez le processus pour lequel créer une exception, puis sélectionnez un autre utilisateur ou sélectionnez **Ne pas affecter** de la **est affecté à** liste.

   >[!NOTE]
   >
   >Le concepteur de processus peut indiquer que les tâches de certains processus sont toujours privées et ne sont pas transférées à d’autres utilisateurs. Ce paramètre remplace tous les paramètres que vous définissez.

1. Lorsque vous avez terminé de définir les préférences, cliquez sur **Enregistrer**. Si vos paramètres indiquent que vous êtes actuellement absent du bureau, vos modifications prennent immédiatement effet. Sinon, elles prennent effet à la date et à l’heure de début spécifiées. Si vous vous connectez pendant que vous êtes absent du bureau, vous êtes toujours considéré comme absent du bureau jusqu’à ce que vous ayez modifié vos paramètres.
