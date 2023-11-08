---
title: Configurer les paramètres du serveur
seo-title: Configuring Server Settings
description: La page Paramètres du serveur permet d’accéder aux paramètres de courrier électronique, de notification de tâche et de notification de l’administrateur.
seo-description: The Server Settings page provides access to email, task notification and administrator notification settings.
uuid: 73b51ac0-56e5-4748-bb33-e3986c69eb2d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e047a95e-0acb-438a-8d27-f005c0adc508
exl-id: 362b7b91-c58b-4e47-a6ef-56a4b54a100c
source-git-commit: c4cd9a61a226ace2a72d60b5b7b7432de12cb873
workflow-type: tm+mt
source-wordcount: '2623'
ht-degree: 18%

---

# Configurer les paramètres du serveur {#configuring-server-settings}

La page Paramètres du serveur permet d’accéder aux différents paramètres du processus des formulaires :

* **Paramètres des emails** qui activent les emails sortants, ainsi que les paramètres du serveur de messagerie utilisés pour ces messages. (Voir [Configuration des paramètres de courrier électronique](configuring-server-settings.md#configuring-email-settings).)
* Les **Paramètres de notification de tâche** permettent d’activer, de désactiver ou de modifier les messages envoyés dans les notifications électroniques aux utilisateurs finaux et aux groupes concernant leurs tâches (voir [Configuration des notifications destinées aux utilisateurs et aux groupes](configuring-server-settings.md#configuring-notifications-for-users-and-groups)).
* Les **Paramètres de notification de l’administrateur** permettent d’activer, de désactiver ou de modifier les messages envoyés dans les notifications électroniques pour les tâches administratives (Voir [Configuration des notifications destinées aux administrateurs](configuring-server-settings.md#configuring-notifications-for-administrators).)

## Configuration des paramètres de courrier électronique {#configuring-email-settings}

Vous pouvez spécifier un compte de messagerie pour le serveur Forms, par l’intermédiaire duquel il envoie des messages électroniques aux utilisateurs et administrateurs d’AEM forms. Ces courriers électroniques sont utilisés pour avertir et rappeler aux utilisateurs les tâches qu’ils doivent effectuer, informer l’utilisateur des tâches qui ont atteint un délai et informer l’administrateur des erreurs de processus qui se produisent.

Pour activer l’envoi de courriers électroniques entre AEM forms et les utilisateurs, configurez les paramètres de courrier électronique sortant sur la page Paramètres de courrier électronique. L&#39;email sortant doit utiliser un serveur SMTP.

Pour permettre aux AEM forms de recevoir et de traiter les courriers électroniques entrants envoyés par les utilisateurs, créez un point de fin de courrier électronique pour le service Complete Task. (Voir [Création d’un point de fin de courrier électronique pour le service Complete Task](/help/forms/using/admin-help/configuring-email-endpoints.md#create-an-email-endpoint-for-the-complete-task-service)).

Si vos processus sont conçus et mis en oeuvre sans avoir besoin d’adresse électronique, il n’est pas nécessaire de configurer aucune des options de la page Paramètres de l’adresse électronique.

### Configuration des paramètres de courrier électronique sortant {#configure-outgoing-email-settings}

1. Dans Administration Console, cliquez sur Services > Processus des formulaires > Paramètres du serveur > Paramètres de courrier électronique.
1. Sélectionnez Activer les messages sortants.
1. Dans la zone Serveur SMTP, saisissez le nom ou l’adresse IP du serveur de messagerie. Tous les emails de notification du processus des formulaires sont envoyés depuis ce serveur de messagerie.
1. Dans les zones User Name (Nom d’utilisateur) et Password (Mot de passe), saisissez le nom de connexion et le mot de passe à utiliser lorsque le serveur SMTP requiert une authentification. Laissez-les vides si la connexion anonyme est autorisée.
1. Dans la zone Email Address (Adresse électronique), saisissez l’adresse électronique à utiliser comme adresse de retour pour les messages électroniques que le processus des formulaires envoie.

   >[!NOTE]
   >
   >Si vous utilisez le serveur Microsoft Exchange et que l’adresse électronique est une adresse électronique incorrecte, le serveur Microsoft Exchange ne parvient pas à envoyer un courrier électronique aux listes de distribution. Pour résoudre ce problème, sélectionnez l’option **Activer la communication externe** séparément pour chaque liste de distribution dans Microsoft Exchange Server.

1. Cliquez sur Enregistrer.

>[!NOTE]
>
>Si vous saisissez des informations incorrectes, vous pouvez cliquer sur Annuler pour revenir à la page précédemment affichée.

### Configuration de modèles de courrier électronique pour utiliser AEM Forms Workspace {#configuring-email-templates-to-use-html-workspace}

>[!NOTE]
>
>Flex Workspace est obsolète pour la version d’AEM Forms.

Par défaut, les courriers électroniques envoyés par AEM forms contiennent des liens vers Flex Workspace (obsolète pour AEM forms on JEE). Vous pouvez configurer AEM forms pour envoyer des emails avec des liens vers AEM Forms Workspace. Pour en savoir plus sur les avantages d’AEM Forms Workspace par rapport à Flex Workspace (obsolète pour AEM forms on JEE), voir [this](/help/forms/using/features-html-workspace-available-flex.md) article.

1. Dans Administration Console, cliquez sur Accueil > Services > Processus des formulaires > Paramètres du serveur > Notifications de tâche.
1. Ouvrez le modèle d’affectation de tâche.
1. Définissez le modèle dans les notifications de tâche sur ce qui suit : `https://@@notification-host@@:8080/lc/libs/ws/index.html?taskId=@@taskid@@`

   ```java
   https://@@notification-host@@:8080/lc/libs/ws/index.html?taskId=@@taskid@@
   ```

## Configuration des notifications destinées aux utilisateurs et aux groupes {#configuring-notifications-for-users-and-groups}

Sur la page Notification de tâche, vous pouvez configurer les modèles que le processus des formulaires utilisera pour générer les notifications électroniques envoyées aux utilisateurs et aux groupes. Vous pouvez personnaliser et formater les notifications à l’aide des variables de processus de formulaires.

Vous configurez les types de notifications suivants pour les utilisateurs et les groupes :

* rappels
* affectations de tâches
* échéances

Pour générer des notifications électroniques pour un groupe, spécifiez une adresse électronique pour le groupe dans User Management. <!--Fix broken link See Setting up and organizing users -->Lorsque le processus des formulaires envoie une notification électronique à un groupe, chaque membre du groupe qui possède une adresse électronique reçoit le courrier électronique de notification. Lorsqu’un membre du groupe reçoit une notification par e-mail et souhaite demander la tâche, il doit cliquer sur le lien de demande dans la notification par e-mail, ce qui ouvre la page des détails de la tâche dans Workspace. À partir de là, le membre peut demander ou demander et ouvrir l’élément de travail.

>[!NOTE]
>
>L’espace de travail Flex est obsolète pour la version d’AEM Forms.

### Configuration de rappels pour les utilisateurs ou les groupes {#configure-reminders-for-users-or-groups}

Vous pouvez envoyer des notifications de rappel à l’utilisateur ou au groupe affecté lorsqu’une échéance pour terminer une tâche approche. Les règles permettant de déterminer exactement quand une notification de rappel est envoyée sont déterminées par le développeur du processus.

1. Dans Administration Console, cliquez sur Services > Processus Forms > Paramètres du serveur > Notifications de tâche.
1. Sous Type de notification, cliquez sur Rappel (pour les utilisateurs) ou sur Groupe - Rappel (pour les groupes).
1. Sélectionnez Activer le rappel ou Activer le groupe - Rappel .
1. (Notifications utilisateur uniquement) Pour inclure une pièce jointe du formulaire et de ses données avec le message électronique de rappel, sélectionnez Inclure les données de formulaire.
1. Dans la zone Objet, saisissez le texte de l’objet du message électronique. Ce champ est prérenseigné avec le texte par défaut. Pour plus d’informations sur la personnalisation de ce champ, voir [Personnalisation du contenu des notifications](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Dans la zone Modèle de notification, saisissez le texte du corps du message électronique. Ce champ est prérenseigné avec le texte par défaut. Pour plus d’informations sur la personnalisation de ce champ, voir [Personnalisation du contenu des notifications](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Dans la liste Format du message , sélectionnez le format d’envoi du message électronique, HTML ou Texte. Le format par défaut est HTML.
1. Dans la liste Codage des emails , sélectionnez le format de codage à utiliser pour le message électronique. La valeur par défaut est UTF-8, que la plupart des utilisateurs en dehors du Japon utiliseront. Les utilisateurs japonais peuvent sélectionner ISO2022-JP.
1. Cliquez sur Enregistrer.

### Configuration des notifications d’affectation de tâche pour les utilisateurs ou les groupes {#configure-task-assignment-notifications-for-users-or-groups}

Vous pouvez envoyer des notifications d’affectation de tâche à un utilisateur ou à un groupe lorsqu’une tâche lui est affectée.

1. Dans Administration Console, cliquez sur Services > Processus Forms > Paramètres du serveur > Notifications de tâche.
1. Sous Type de notification, cliquez sur Affectation de tâche pour les utilisateurs ou Groupe - Affectation de tâche pour les groupes.
1. Sélectionnez Activer l’affectation de tâche pour les utilisateurs ou Activer le groupe - Affectation de tâche pour les groupes.
1. (Notifications utilisateur uniquement) Pour inclure une pièce jointe du formulaire et de ses données avec le message électronique d’affectation de tâche, sélectionnez Inclure les données de formulaire.
1. Dans la zone Objet, saisissez le texte de l’objet du message électronique. Ce champ est prérenseigné avec le texte par défaut. Pour plus d’informations sur la personnalisation de ce champ, voir [Personnalisation du contenu des notifications](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Dans la zone Modèle de notification, saisissez le texte du corps du message électronique. Ce champ est prérenseigné avec le texte par défaut. Pour plus d’informations sur la personnalisation de ce champ, voir [Personnalisation du contenu des notifications](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Dans la liste Format du message , sélectionnez le format d’envoi du message électronique, HTML ou Texte. Le format par défaut est HTML.
1. Dans la liste Codage des emails , sélectionnez le format de codage à utiliser pour le message électronique. La valeur par défaut est UTF-8, que la plupart des utilisateurs en dehors du Japon utiliseront. Les utilisateurs japonais peuvent sélectionner ISO2022-JP.
1. Cliquez sur Enregistrer.

### Configuration des notifications d’échéance pour les utilisateurs ou les groupes {#configure-deadline-notifications-for-users-or-groups}

Vous pouvez envoyer des notifications d’échéance aux utilisateurs et aux groupes lorsque la date limite d’action pour une tâche affectée est dépassée. Une notification d’échéance est généralement informative, car l’utilisateur ne peut plus agir sur la tâche affectée.

1. Dans Administration Console, cliquez sur Services > Processus Forms > Paramètres du serveur > Notifications de tâche.
1. Sous Type de notification, cliquez sur Date limite (pour les utilisateurs) ou sur Groupe - Date limite (pour les groupes).
1. Sélectionnez Activer l’échéance ou Activer le groupe - Date limite.
1. Dans la zone Objet, saisissez le texte de l’objet du message électronique. Ce champ est prérenseigné avec le texte par défaut. Pour plus d’informations sur la personnalisation de ce champ, voir [Personnalisation du contenu des notifications](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Dans la zone Modèle de notification, saisissez le texte du corps du message électronique. Ce champ est prérenseigné avec le texte par défaut. Pour plus d’informations sur la personnalisation de ce champ, voir [Personnalisation du contenu des notifications](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Dans la liste Format du message , sélectionnez le format d’envoi du message électronique, HTML ou Texte. Le format par défaut est HTML.
1. Dans la liste Codage des emails , sélectionnez le format de codage à utiliser pour le message électronique. La valeur par défaut est UTF-8, que la plupart des utilisateurs en dehors du Japon utiliseront. Les utilisateurs japonais peuvent sélectionner ISO2022-JP.
1. Cliquez sur Enregistrer.

### Masquer la balise DO NOT DELETE pour tous les emails {#hide-the-do-not-delete-tag-for-all-emails}

Vous pouvez configurer le service de messagerie de façon à masquer la balise de suivi DO NOT DELETE dans tous les courriers électroniques envoyés par le biais d’un processus pour des intervenants humains.

<!-- 
For details, see [How to hide the 'DO-NOT-DELETE' tag with CSS](https://blogs.adobe.com/LiveCycleHelp/2013/09/how-to-hide-the-do-not-delete-tag-with-css.html) 
-->

## Configuration des notifications destinées aux administrateurs {#configuring-notifications-for-administrators}

Vous pouvez configurer les modèles que le processus des formulaires utilisera pour générer les notifications électroniques envoyées aux administrateurs.

Vous configurez les types de notifications suivants pour les administrateurs :

* branche bloquée
* opération bloquée

### Configuration des notifications de branche bloquée {#configure-stalled-branch-notifications}

Si une branche bloque (arrête de continuer délibérément ou en raison d’une erreur), une notification peut être envoyée à un administrateur ou à un autre utilisateur, qui peut alors examiner le problème.

1. Dans Administration Console, cliquez sur Services > Processus Forms > Paramètres du serveur > Notifications de l’administrateur.
1. Sous Type de notification, cliquez sur Branche bloquée.
1. Sélectionnez Activer la branche bloquée.
1. Dans la zone Email Address (Adresse électronique), saisissez les adresses des utilisateurs à avertir lorsqu’une branche bloque. Utilisez le format user@domain.com et séparez chaque adresse par une virgule. En règle générale, cette adresse électronique est destinée à un administrateur.
1. Dans la zone Objet, saisissez le texte de l’objet du message électronique. Ce champ est prérenseigné avec le texte par défaut. Pour plus d’informations sur la personnalisation de ce champ, voir [Personnalisation du contenu des notifications](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Dans la zone Modèle de notification, saisissez le texte du corps du message électronique. Ce champ est prérenseigné avec le texte par défaut. Pour plus d’informations sur la personnalisation de ce champ, voir [Personnalisation du contenu des notifications](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Dans la liste Format du message , sélectionnez le format d’envoi du message électronique, HTML ou Texte. Le format par défaut est HTML.
1. Dans la liste Codage des emails , sélectionnez le format de codage à utiliser pour le message électronique. La valeur par défaut est UTF-8, que la plupart des utilisateurs en dehors du Japon utilisent. Les utilisateurs japonais peuvent sélectionner ISO2022-JP.
1. Cliquez sur Enregistrer.

### Configuration des notifications d’opération bloquée {#configure-stalled-operation-notifications}

Si une opération bloque (arrête de se dérouler délibérément ou en raison d’une erreur), une notification peut être envoyée à un administrateur ou à un autre utilisateur, qui peut enquêter sur le problème.

1. Dans Administration Console, cliquez sur Services > Processus Forms > Paramètres du serveur > Notifications de l’administrateur.
1. Sous Type de notification, cliquez sur Opération bloquée.
1. Sélectionnez Activer l’opération bloquée.
1. Dans la zone Adresses électroniques , saisissez les adresses des utilisateurs à avertir lorsqu’une opération bloque. Utilisez le format user@domain.com et séparez chaque adresse par une virgule. En règle générale, cette adresse électronique est destinée à un administrateur.
1. Dans la zone Objet, saisissez le texte de l’objet du message électronique. Ce champ est prérenseigné avec le texte par défaut. Pour plus d’informations sur la personnalisation de ce champ, voir [Personnalisation du contenu des notifications](configuring-server-settings.md#customizing-the-content-of-notifications)
1. Dans la zone Modèle de notification, saisissez le texte du corps du message électronique. Ce champ est prérenseigné avec le texte par défaut. Pour plus d’informations sur la personnalisation de ce champ, voir [Personnalisation du contenu des notifications](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Cliquez sur Enregistrer.

## Personnalisation du contenu des notifications {#customizing-the-content-of-notifications}

Les pages Notifications de tâche et Notifications de l’administrateur fournissent plusieurs fonctionnalités qui vous permettent de personnaliser les messages de notification :

* éditeur de texte enrichi
* sélecteur de variable
* Génération d’URL

### Éditeur de texte enrichi {#rich-text-editor}

La zone Modèle de notification est un éditeur de texte enrichi qui vous permet de générer un HTML pour les messages de notification électronique. Il fournit des options de mise en forme des polices et des paragraphes, qui se trouvent sous la zone Modèle de notification. Les options incluent le type, la taille, le style et la couleur de la police, ainsi que l’alignement et les puces du paragraphe.

### Génération d’URL {#url-generation}

Pour les notifications de tâche uniquement, le workflow Forms comprend deux configurations d’URL prédéfinies que vous pouvez faire glisser de la liste Génération d’URL vers le champ Modèle de notification, puis personnaliser :

* OpenTask est disponible pour les types de notification Reminder et Task Assignment . Cette URL fournit un lien vers la tâche dans Workspace, ce qui permet à l’utilisateur d’accéder rapidement à la tâche à partir de la notification électronique. Lorsque vous faites glisser l’URL OpenTask vers le champ Modèle de notification, l’URL est au format suivant :

  `https://@@notification-host@@:<PORT>/workpace/Main.html?taskId=@@taskid@@`

* Demander la tâche est disponible pour les types de notification Groupe - Rappel et Groupe - Affectation de tâche . Cette URL fournit un lien vers la page des détails de la tâche dans Workspace, où l’utilisateur peut demander ou demander et ouvrir l’élément de travail. Lorsque vous faites glisser l’URL Demander la tâche vers le champ Modèle de notification, l’URL est au format suivant :

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
>Si vous utilisez une application web personnalisée autre que Forms pour permettre aux utilisateurs d’accéder aux tâches, vous devez utiliser un format d’URL approprié pour votre application personnalisée.

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

Pour les branches bloquées, vous pouvez utiliser les variables suivantes dans les champs Objet et Modèle de notification :

**branch-id** Identifiant de branche.

**process-id** Identifiant de l’instance du processus.

**notification-host** Nom d’hôte du serveur d’application AEM Forms.

Pour les opérations bloquées, vous pouvez utiliser les variables suivantes dans les champs Objet et Modèle de notification :

**action-id** Identifiant de l’opération.

**branch-id** Identifiant de branche.

**process-id** Identifiant de l’instance du processus.

**notification-host** Nom d’hôte du serveur d’application AEM Forms.

### Utilisation d’une variable dans la zone Objet {#using-a-variable-in-the-subject-box}

Si vous saisissez le texte suivant dans la zone Objet pour les notifications d’affectation de tâche :

`Please complete task @@taskid@@`

L’utilisateur reçoit un courrier électronique avec l’objet suivant si la tâche 376 lui est affectée :

`Please complete task 376`

### Utilisation de variables dans la zone Modèle de notification {#using-variables-in-the-notification-template-box}

Si vous saisissez le texte suivant dans la zone Modèle de notification pour les notifications de branches bloquées :

`Branch @@branch-id@@ has stalled! You have received this notification from @@notification-host@@.`

L’administrateur reçoit un courrier électronique avec le contenu suivant si 4868 est le numéro de la branche et le nom du serveur est `ServerXYZ` :

`Branch 4868 has stalled! You have received this notification from ServerXYZ.`

## Configuration des connexions Business Activity Monitoring {#configuring-business-activity-monitoring-connections}

Business Activity Monitoring, module facultatif, fournit un ensemble de tableaux de bord opérationnels qui permettent une visibilité en temps réel de vos opérations et des indicateurs de performances clés.

Sur la page Paramètres de configuration BAM, vous définissez les connexions au serveur qui exécute BAM afin que les événements liés aux processus puissent être suivis et transmis à ce serveur.

1. Dans Administration Console, cliquez sur Services > Processus Forms > Paramètres du serveur > Paramètres de configuration BAM.
1. Dans la zone Hôte BAM, saisissez le nom du serveur exécutant BAM. La valeur par défaut est localhost.
1. Dans la zone BAM Port, saisissez le port à utiliser pour la connexion au serveur qui exécute BAM. Le port BAM par défaut pour JBoss est 8080, WebLogic 7001 et WebSphere 9080.
1. Dans la zone Server Host, saisissez le nom ou l’adresse IP du serveur Forms hôte. la valeur par défaut est localhost.
1. Dans la zone Server Port, saisissez le numéro de port utilisé par le serveur Forms.
1. Dans les zones User Name (Nom d’utilisateur) et Password (Mot de passe), saisissez l’identifiant utilisateur et le mot de passe appropriés pour accéder au serveur BAM. Le nom d’utilisateur par défaut est CognosNowAdmin et le mot de passe par défaut est manager.
1. Cliquez sur Enregistrer.
