---
title: Configurer les paramètres du serveur
description: La page Paramètres du serveur permet d’accéder aux paramètres d’e-mail, de notification de tâche et de notification de l’administrateur ou de l’administratrice.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 362b7b91-c58b-4e47-a6ef-56a4b54a100c
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: ht
source-wordcount: '2631'
ht-degree: 100%

---

# Configurer les paramètres du serveur {#configuring-server-settings}

La page Paramètres du serveur permet d’accéder aux différents paramètres de Forms Workflow :

* Les **Paramètres d’e-mail** activent les e-mails sortants, ainsi que les paramètres du serveur de messagerie utilisés pour ces messages. (Voir [Configuration des paramètres d’e-mail](configuring-server-settings.md#configuring-email-settings).)
* Les **Paramètres de notification de tâche** permettent d’activer, de désactiver ou de modifier les messages envoyés dans les notifications électroniques aux utilisateurs finaux et aux groupes concernant leurs tâches (voir [Configuration des notifications destinées aux utilisateurs et aux groupes](configuring-server-settings.md#configuring-notifications-for-users-and-groups)).
* Les **Paramètres de notification de l’administrateur** permettent d’activer, de désactiver ou de modifier les messages envoyés dans les notifications électroniques pour les tâches administratives (Voir [Configuration des notifications destinées aux administrateurs et administratrices](configuring-server-settings.md#configuring-notifications-for-administrators).)

## Configuration des paramètres d’e-mail {#configuring-email-settings}

Vous pouvez indiquer un compte e-mail pour le serveur Forms, grâce auquel il envoie des e-mails aux utilisateurs et utilisatrices ainsi qu’aux administrateurs et administratrices d’AEM Forms. Ces e-mails servent à rappeler aux utilisateurs et utilisatrices les tâches qu’ils doivent effectuer, les informer des tâches qui ont atteint la date d’échéance et informer l’administrateur ou l’administratrice des erreurs de processus.

Pour activer l’envoi d’e-mails entre AEM Forms et les utilisateurs et utilisatrices, configurez les paramètres des e-mails sortants sur la page Paramètres d’e-mail. L’e-mail sortant doit utiliser un serveur SMTP.

Pour permettre à AEM Forms de recevoir et de traiter les e-mails entrants envoyés par les utilisateurs et utilisatrices, créez un point d’entrée d’e-mail pour le service Complete Task. (Voir [Création d’un point d’entrée d’e-mail pour le service Complete Task](/help/forms/using/admin-help/configuring-email-endpoints.md#create-an-email-endpoint-for-the-complete-task-service)).

Si vos processus sont conçus et mis en œuvre sans avoir besoin d’e-mail. Il n’est pas nécessaire de configurer les options de la page Paramètres d’e-mail.

### Configurer les paramètres d’e-mails sortants {#configure-outgoing-email-settings}

1. Dans la console d’administration, cliquez sur Services > Forms Workflow > Paramètres du serveur > Paramètres d’e-mail.
1. Sélectionnez Activer les messages sortants.
1. Dans la zone Serveur SMTP, saisissez le nom ou l’adresse IP du serveur de messagerie. Tous les e-mails de notification de Forms Workflow sont envoyés depuis ce serveur de messagerie.
1. Dans les zones Nom d’utilisateur et Mot de passe, saisissez l’identifiant de connexion et le mot de passe à utiliser lorsque le serveur SMTP requiert une authentification. Laissez les zones vides si la connexion anonyme est autorisée.
1. Dans la zone Adresse e-mail, saisissez l’adresse e-mail à utiliser comme adresse de retour pour les e-mails que Forms Workflow envoie.

   >[!NOTE]
   >
   >Si vous utilisez Microsoft Exchange Server et que l’adresse e-mail n’est pas valide, Microsoft Exchange Server ne parvient pas à envoyer d’e-mail aux listes de distribution. Pour résoudre ce problème, sélectionnez l’option **Activer la communication externe** séparément pour chaque liste de distribution dans Microsoft Exchange Server.

1. Cliquez sur Enregistrer.

>[!NOTE]
>
>Si vous saisissez des informations incorrectes, vous pouvez cliquer sur Annuler pour revenir à la page précédemment affichée.

### Configurer des modèles d’e-mail pour utiliser l’espace de travail AEM Forms {#configuring-email-templates-to-use-html-workspace}

>[!NOTE]
>
>Flex Workspace est obsolète pour la version d’AEM Forms.

Par défaut, les e-mails envoyés par AEM Forms contiennent des liens vers Flex Workspace (obsolète pour AEM Forms on JEE). Vous pouvez configurer AEM Forms pour envoyer des e-mails avec des liens vers l’espace de travail AEM Forms. Pour en savoir plus sur les avantages de l’espace de travail AEM Forms par rapport à l’espace de travail Flex (obsolète pour AEM Forms on JEE), consultez [cet](/help/forms/using/features-html-workspace-available-flex.md) article.

1. Dans la console d’administration, cliquez sur Accueil > Services > Forms Workflow > Paramètres du serveur > Notifications de tâche.
1. Ouvrez le modèle d’affectation des tâches.
1. Définissez le modèle dans les notifications de tâche sur ce qui suit : `https://@@notification-host@@:8080/lc/libs/ws/index.html?taskId=@@taskid@@`

   ```java
   https://@@notification-host@@:8080/lc/libs/ws/index.html?taskId=@@taskid@@
   ```

## Configurer les notifications pour les utilisateurs, les utilisatrices et les groupes {#configuring-notifications-for-users-and-groups}

Sur la page Notification de tâche, vous pouvez configurer les modèles que Forms Workflow utilisera pour générer les notifications par e-mail envoyées aux utilisateurs, aux utilisatrices et aux groupes. Vous pouvez personnaliser et mettre en forme les notifications à l’aide des variables de Forms Workflow.

Vous configurez les types de notifications suivants pour les utilisateurs, les utilisatrices et les groupes :

* rappels
* affectations de tâches
* dates d’échéance

Pour générer des notifications par e-mail pour un groupe, spécifiez une adresse e-mail pour le groupe dans User Management. <!--Fix broken link See Setting up and organizing users -->Lorsque le processus des formulaires envoie une notification électronique à un groupe, chaque membre du groupe qui possède une adresse électronique reçoit le courrier électronique de notification. Lorsqu’une personne du groupe reçoit une notification par e-mail et souhaite demander la tâche, elle doit cliquer sur le lien de demande dans la notification par e-mail, ce qui ouvre la page des détails de la tâche dans l’espace de travail. À partir de là, la personne peut demander ou demander et ouvrir la tâche.

>[!NOTE]
>
>L’espace de travail Flex est obsolète pour la version d’AEM Forms.

### Configuration des rappels pour les utilisateurs, les utilisatrices ou les groupes {#configure-reminders-for-users-or-groups}

Vous pouvez choisir d’envoyer des notifications de rappel à l’utilisateur, l’utilisatrice ou au groupe affecté à une tâche lorsque le délai d’exécution de cette tâche se rapproche. Les règles déterminant exactement quand une notification de rappel est envoyée sont décidées par l’équipe de développement du processus.

1. Dans la console d’administration, cliquez sur Services > Forms Workflow > Paramètres du serveur > Notifications de tâche.
1. Sous Type de notification, cliquez sur Rappel (pour les utilisateurs et utilisatrices) ou sur Groupe : rappel (pour les groupes).
1. Sélectionnez Activer le rappel ou Activer le groupe - Rappel.
1. (Notifications à l’utilisateur ou l’utilisatrice seulement) Pour inclure le formulaire et ses données en pièce jointe dans l’e-mail de rappel, sélectionnez Inclure les données de formulaire.
1. Dans le champ Objet, saisissez le texte de l’objet de l’e-mail. Ce champ est prérenseigné avec du texte par défaut. Pour plus d’informations sur la personnalisation de ce champ, consultez [Personnalisation du contenu des notifications](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Dans le champ Modèle de notification, saisissez le texte du corps de l’e-mail. Ce champ est prérenseigné avec du texte par défaut. Pour plus d’informations sur la personnalisation de ce champ, consultez [Personnalisation du contenu des notifications](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Dans la liste Format du message , sélectionnez le format d’envoi de l’e-mail, HTML ou Texte. Le format par défaut est HTML.
1. Dans la liste d’encodage des e-mails , sélectionnez le format d’encodage à utiliser pour l’e-mail. La valeur par défaut est UTF-8, que la plupart des utilisateurs et utilisatrices en dehors du Japon utiliseront. Les utilisateurs et utilisatrices japonais peuvent sélectionner ISO2022-JP.
1. Cliquez sur Enregistrer.

### Configurer les notifications d’affectation de tâche pour des utilisateurs, des utilisatrices ou des groupes {#configure-task-assignment-notifications-for-users-or-groups}

Vous pouvez envoyer des notifications d’affectation de tâche à un utilisateur, une utilisatrice ou à un groupe lorsqu’une tâche leur est affectée.

1. Dans la console d’administration, cliquez sur Services > Forms Workflow > Paramètres du serveur > Notifications de tâche.
1. Sous Type de notification, cliquez sur Affectation de tâche pour les utilisateurs, les utilisatrices ou le groupe - Affectation de tâche pour les groupes.
1. Sélectionnez Activer affectation de tâche pour les utilisateurs et les utilisatrices ou Activer  le groupe - Affectation de tâche pour les groupes.
1. (Notifications aux utilisateurs ou utilisatrices seulement) Pour inclure le formulaire et ses données en pièce jointe à l’e-mail d’affectation de tâche, sélectionnez Inclure les données de formulaire.
1. Dans le champ Objet, saisissez le texte de l’objet de l’e-mail. Ce champ est prérenseigné avec du texte par défaut. Pour plus d’informations sur la personnalisation de ce champ, consultez [Personnalisation du contenu des notifications](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Dans le champ Modèle de notification, saisissez le texte du corps de l’e-mail. Ce champ est prérenseigné avec du texte par défaut. Pour plus d’informations sur la personnalisation de ce champ, consultez [Personnalisation du contenu des notifications](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Dans la liste Format du message , sélectionnez le format d’envoi de l’e-mail, HTML ou Texte. Le format par défaut est HTML.
1. Dans la liste d’encodage des e-mails , sélectionnez le format d’encodage à utiliser pour l’e-mail. La valeur par défaut est UTF-8, que la plupart des utilisateurs et utilisatrices en dehors du Japon utiliseront. Les utilisateurs et utilisatrices japonais peuvent sélectionner ISO2022-JP.
1. Cliquez sur Enregistrer.

### Configurer les notifications d’échéance pour des utilisateurs, des utilisatrices ou des groupes {#configure-deadline-notifications-for-users-or-groups}

Vous pouvez envoyer des notifications d’échéance à des utilisateurs, à des utilisatrices et à des groupes pour les informer que le délai d’exécution d’une tâche affectée est dépassé. En règle générale, une notification d’échéance n’est envoyée qu’à titre d’information, car l’utilisateur ou l’utilisatrice ne peut plus agir sur la tâche affectée.

1. Dans la console d’administration, cliquez sur Services > Forms Workflow > Paramètres du serveur > Notifications de tâche.
1. Sous Type de notification, cliquez sur Échéance (pour les utilisateurs et les utilisatrices) ou sur Groupe : délai (pour les groupes).
1. Sélectionnez Activer l’échéance ou Activer le groupe - Échéance.
1. Dans le champ Objet, saisissez le texte de l’objet de l’e-mail. Ce champ est prérenseigné avec du texte par défaut. Pour plus d’informations sur la personnalisation de ce champ, consultez [Personnalisation du contenu des notifications](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Dans le champ Modèle de notification, saisissez le texte du corps de l’e-mail. Ce champ est prérenseigné avec du texte par défaut. Pour plus d’informations sur la personnalisation de ce champ, consultez [Personnalisation du contenu des notifications](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Dans la liste Format du message , sélectionnez le format d’envoi de l’e-mail, HTML ou Texte. Le format par défaut est HTML.
1. Dans la liste d’encodage des e-mails , sélectionnez le format d’encodage à utiliser pour l’e-mail. La valeur par défaut est UTF-8, que la plupart des utilisateurs et utilisatrices en dehors du Japon utiliseront. Les utilisateurs et utilisatrices japonais peuvent sélectionner ISO2022-JP.
1. Cliquez sur Enregistrer.

### Masquer la balise DO NOT DELETE pour tous les e-mails {#hide-the-do-not-delete-tag-for-all-emails}

Vous pouvez configurer le service de messagerie de façon à masquer la balise de suivi DO NOT DELETE dans tous les courriers électroniques envoyés par le biais d’un processus pour des intervenants humains.

<!-- 
For details, see [How to hide the 'DO-NOT-DELETE' tag with CSS](https://blogs.adobe.com/LiveCycleHelp/2013/09/how-to-hide-the-do-not-delete-tag-with-css.html) 
-->

## Configuration des notifications destinées aux administrateurs et aux administratrices {#configuring-notifications-for-administrators}

Vous pouvez configurer les modèles que Forms Workflow utilisera pour générer les notifications envoyées par e-mail aux administrateurs et administratrices.

Vous pouvez configurer les types de notifications suivants pour les administrateurs et administratrices :

* Branche bloquée
* Opération bloquée

### Configurer les notifications pour les branches bloquées {#configure-stalled-branch-notifications}

Si une branche se bloque (dont le fonctionnement s’arrête soit délibérément soit en raison d’une erreur), une notification peut être envoyée à un administrateur ou à une administratrice, ou à un autre utilisateur ou une autre utilisatrice, qui peuvent alors examiner le problème.

1. Dans la console d’administration, cliquez sur Services > Forms Workflow > Paramètres du serveur > Notifications de l’administrateur.
1. Sous Type de notification, cliquez sur Branche bloquée.
1. Sélectionnez Activer pour les branches bloquées.
1. Dans la zone adresse e-mail, saisissez les adresses des utilisateurs et utilisatrices à avertir lorsqu’une branche se bloque. Utilisez le format utilisateur@domaine.com et séparez chaque adresse par une virgule. En règle générale, cette adresse e-mail est destinée à un administrateur ou une administratrice.
1. Dans le champ Objet, saisissez le texte de l’objet de l’e-mail. Ce champ est prérenseigné avec du texte par défaut. Pour plus d’informations sur la personnalisation de ce champ, consultez [Personnalisation du contenu des notifications](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Dans le champ Modèle de notification, saisissez le texte du corps de l’e-mail. Ce champ est prérenseigné avec du texte par défaut. Pour plus d’informations sur la personnalisation de ce champ, consultez [Personnalisation du contenu des notifications](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Dans la liste Format du message , sélectionnez le format d’envoi de l’e-mail, HTML ou Texte. Le format par défaut est HTML.
1. Dans la liste d’encodage des e-mails , sélectionnez le format d’encodage à utiliser pour l’e-mail. La valeur par défaut est UTF-8, que la plupart des utilisateurs et utilisatrices en dehors du Japon utilisent. Les utilisateurs et utilisatrices japonais peuvent sélectionner ISO2022-JP.
1. Cliquez sur Enregistrer.

### Configurer les notifications pour les opérations bloquées {#configure-stalled-operation-notifications}

Si une opération se bloque (dont le fonctionnement s’arrête soit délibérément soit en raison d’une erreur), une notification peut être envoyée à un administrateur ou à une administratrice, ou à un autre utilisateur ou une autre utilisatrice, qui peuvent examiner le problème.

1. Dans la console d’administration, cliquez sur Services > Forms Workflow > Paramètres du serveur > Notifications de l’administrateur.
1. Sous Type de notification, cliquez sur Opération bloquée.
1. Sélectionnez Activer pour les opération bloquées.
1. Dans la zone e-mail, saisissez les adresses des utilisateurs et utilisatrices à avertir lorsqu’une opération se bloque. Utilisez le format utilisateur@domaine.com et séparez chaque adresse par une virgule. En règle générale, cette adresse e-mail est destinée à un administrateur ou une administratrice.
1. Dans le champ Objet, saisissez le texte de l’objet de l’e-mail. Ce champ est prérenseigné avec du texte par défaut. Pour plus d’informations sur la personnalisation de ce champ, reportez-vous à [Personnalisation du contenu des notifications](configuring-server-settings.md#customizing-the-content-of-notifications)
1. Dans le champ Modèle de notification, saisissez le texte du corps de l’e-mail. Ce champ est prérenseigné avec du texte par défaut. Pour plus d’informations sur la personnalisation de ce champ, reportez-vous à [Personnalisation du contenu des notifications](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Cliquez sur Enregistrer.

## Personnalisation du contenu des notifications {#customizing-the-content-of-notifications}

Les pages Notifications de tâche et Notifications de l’administrateur fournissent plusieurs fonctionnalités qui vous permettent de personnaliser les messages de notification :

* Éditeur de texte enrichi
* sélecteur de variable
* Génération d’URL

### Éditeur de texte enrichi {#rich-text-editor}

La zone Modèle de notification est un éditeur de texte enrichi qui vous permet de générer du code HTML pour les messages de notification par e-mail. Il fournit des options de mise en forme des polices et des paragraphes, qui se trouvent sous la zone Modèle de notification. Les options incluent le type, la taille, le style et la couleur de la police, ainsi que l’alignement du paragraphe et les puces.

### Génération d’URL {#url-generation}

Pour les notifications de tâche uniquement, Forms Workflow comprend deux configurations d’URL prédéfinies que vous pouvez faire glisser de la liste Génération d’URL vers la case Modèle de notification, puis personnaliser :

* OpenTask est disponible pour les types de notification Rappel et Affectation de tâche. Cette URL fournit un lien vers la tâche dans Workspace, ce qui permet à l’utilisateur ou l’utilisatrice d’y accéder rapidement à partir de la notification par e-mail. Lorsque vous faites glisser l’URL OpenTask vers la zone Modèle de notification, l’URL est au format suivant :

  `https://@@notification-host@@:<PORT>/workpace/Main.html?taskId=@@taskid@@`

* Demander la tâche est disponible pour les types de notification Groupe - Rappel et Groupe - Affectation de tâche. Cette URL fournit un lien vers la page des détails de la tâche dans Workspace, où l’utilisateur ou l’utilisatrice peut soit demander, soit demander et ouvrir l’élément de travail. Lorsque vous faites glisser l’URL Demander la tâche vers la zone Modèle de notification, l’URL est au format suivant :

  `https://@@notification-host@@:<PORT>/workpace/Main.html?taskId=@@taskid@@`

>[!NOTE]
>
>Flex Workspace est obsolète pour la version d’AEM Forms.

Si votre solution est déployée dans un environnement organisé en grappes, remplacez `@@notification-host@@` par l’adresse de la grappe.

`<`*PORT* `>` correspond au numéro de port d’écouteur HTTP du serveur d’applications. Les ports d’écouteur HTTP par défaut pour les serveurs d’applications pris en charge sont les suivants :

**JBoss :** 8080

**Oracle WebLogic Server :** 7001

**IBM WebSphere :** 9080

Pour permettre le fonctionnement normal de ces URL, remplacez `<`*PORT* `>` par le numéro de port approprié pour votre environnement.

>[!NOTE]
>
>Si vous utilisez une application web personnalisée autre que Forms pour permettre aux utilisateurs et utilisatrices d’accéder aux tâches, vous devez utiliser un format d’URL approprié pour votre application personnalisée.

### Sélecteur de variable {#variable-picker}

La liste Sélecteur de variables fournit des variables utiles que vous pouvez faire glisser dans les zones Objet ou Modèle de notification. Lorsque vous faites glisser une variable dans le champ Objet ou Modèle de notification, elle est remplacée par le nom réel de la variable Workflows des formulaires, encadrée par deux symboles @, par exemple `@@taskid@@`.

Pour les rappels, affectations de tâche et échéances des utilisateurs et des groupes, vous pouvez utiliser les variables suivantes dans les champs Objet et Modèle de notification :

**Description** Contenu de la propriété Description tel que défini dans l’opération Utilisateur (point de départ, opération d’affectation de tâche ou opération d’affectation de tâches multiples) du processus dans Workbench.

**Instructions** Contenu de la propriété Instructions de la tâche tel que défini dans l’opération Utilisateur du processus dans Workbench.

**notification-host** Nom d’hôte du serveur d’application AEM Forms.

**process-name** Nom du processus.

**operation-name** Nom de l’opération.

**taskid** Identifiant unique de la tâche en cours.

**Actions** Cette option génère une liste numérotée des itinéraires valides (par exemple, Approuver, Refuser) sur lesquels le destinataire peut cliquer.

De plus, pour les rappels, affectations de tâche et échéances de groupe, vous pouvez aussi utiliser les variables suivantes :

**group-name** Nom du groupe auquel la tâche est affectée.

>[!NOTE]
>
>Si une variable ne comporte aucune valeur, rien n’est renvoyé.

Pour les branches bloquées, vous pouvez utiliser les variables suivantes dans les champs Objet et Modèle de notification :

**branch-id** Identifiant de branche.

**process-id** Identifiant de l’instance du processus.

**notification-host** Nom d’hôte du serveur d’application AEM Forms.

Pour les opérations bloquées, vous pouvez utiliser les variables suivantes dans les champs Objet et Modèle de notification :

**action-id** Identifiant de l’opération.

**branch-id** Identifiant de branche.

**process-id** Identifiant de l’instance du processus.

**notification-host** Nom d’hôte du serveur d’application AEM Forms.

### Utilisation d’une variable dans la zone Objet {#using-a-variable-in-the-subject-box}

Si vous saisissez le texte suivant dans la zone Objet pour les notifications d’affectation de tâche :

`Please complete task @@taskid@@`

L’utilisateur reçoit un courrier électronique avec l’objet suivant si la tâche 376 lui est affectée :

`Please complete task 376`

### Utilisation des variables dans la zone Modèle de notification {#using-variables-in-the-notification-template-box}

Si vous saisissez le texte suivant dans la zone Modèle de notification pour les notifications de branches bloquées :

`Branch @@branch-id@@ has stalled! You have received this notification from @@notification-host@@.`

L’administrateur reçoit un courrier électronique avec le contenu suivant si 4868 est le numéro de la branche et le nom du serveur est `ServerXYZ` :

`Branch 4868 has stalled! You have received this notification from ServerXYZ.`

## Configuration des connexions Business Activity Monitoring {#configuring-business-activity-monitoring-connections}

Business Activity Monitoring, qui est un module facultatif, fournit un ensemble de tableaux de bord opérationnels qui offrent une visibilité en temps réel de vos opérations et des indicateurs de performances clés.

Sur la page Paramètres de configuration BAM, vous définissez les connexions au serveur qui exécute BAM, afin que les événements liés aux processus puissent être suivis et transmis à ce serveur.

1. Dans la console d’administration, cliquez sur Services > Forms Workflow > Paramètres du serveur > Paramètres de configuration BAM.
1. Dans la zone Hôte BAM, saisissez le nom du serveur exécutant BAM. Le paramètre par défaut est localhost.
1. Dans la zone Port BAM, saisissez le port à utiliser pour la connexion au serveur qui exécute BAM. Le port BAM par défaut pour JBoss est 8080, celui de WebLogic est 7001 et celui de WebSphere est 9080.
1. Dans la zone Hôte du serveur, saisissez le nom ou l’adresse IP du serveur Forms hôte. La valeur par défaut est localhost.
1. Dans la zone Port du serveur, saisissez le numéro de port utilisé par le serveur Forms.
1. Dans les zones Nom d’utilisateur et Mot de passe, saisissez l’identifiant et le mot de passe appropriés pour accéder au serveur BAM. Le nom d’utilisateur ou d’utilisatrice par défaut est CognosNowAdmin et le mot de passe par défaut est manager.
1. Cliquez sur Enregistrer.
