---
title: Configuration des paramètres du serveur
seo-title: Configuration des paramètres du serveur
description: La page Paramètres du serveur fournit l’accès aux paramètres de messagerie électronique, de notification de tâche et de notification de l’administrateur.
seo-description: La page Paramètres du serveur fournit l’accès aux paramètres de messagerie électronique, de notification de tâche et de notification de l’administrateur.
uuid: 73b51ac0-56e5-4748-bb33-e3986c69eb2d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e047a95e-0acb-438a-8d27-f005c0adc508
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '2657'
ht-degree: 90%

---


# Configuration des paramètres du serveur {#configuring-server-settings}

La page Paramètres du serveur donne accès aux différents paramètres du processus des formulaires :

* Les **Paramètres du courrier électronique** permettent d’activer les messages électroniques sortants et entrants, ainsi que les paramètres du serveur de messagerie utilisé pour ces messages (voir [Configuration des paramètres de courrier électronique](configuring-server-settings.md#configuring-email-settings)).
* Les **Paramètres de notification de tâche** permettent d’activer, de désactiver ou de modifier les messages envoyés dans les notifications électroniques aux utilisateurs finaux et aux groupes concernant leurs tâches (voir [Configuration des notifications destinées aux utilisateurs et aux groupes](configuring-server-settings.md#configuring-notifications-for-users-and-groups)).
* Les **Paramètres de notification de l’administrateur** permettent d’activer, de désactiver ou de modifier les messages envoyés dans les notifications électroniques pour les tâches administratives (voir [Configuration des notifications destinées aux administrateurs](configuring-server-settings.md#configuring-notifications-for-administrators)).

## Configuration des paramètres de courrier électronique {#configuring-email-settings}

Vous pouvez indiquer un compte de courrier électronique pour le serveur Forms, par l’intermédiaire duquel il envoie des courriers électroniques aux utilisateurs et aux administrateurs et en reçoit de la part de ces mêmes utilisateurs et administrateurs. Ces courriers électroniques sont utilisés pour notifier aux utilisateurs les tâches qu’ils sont tenus d’exécuter, les leur rappeler, les notifier lorsque les tâches arrivées à échéance et notifier à l’administrateur toute erreur de processus survenue.

Pour permettre l’envoi de courriers électroniques entre AEM forms et les utilisateurs, vous devez configurer les paramètres de courrier électronique sortant dans la page Paramètres du courrier électronique. Le courrier électronique sortant doit utiliser un serveur SMTP.

Pour qu’AEM forms reçoive et traite le courrier électronique entrant envoyé par des utilisateurs, vous devez créer un point de fin de courrier électronique pour le service Complete Task (voir [Création d’un point de fin de courrier électronique pour le service Complete Task](/help/forms/using/admin-help/configuring-email-endpoints.md#create-an-email-endpoint-for-the-complete-task-service)).

Si les processus que vous utilisez sont conçus et implémentés sans avoir à utiliser le courrier électronique, il est inutile de configurer les options de la page Paramètres du courrier électronique.

### Configuration des paramètres du courrier électronique sortant {#configure-outgoing-email-settings}

1. Dans Administration Console, cliquez sur Services > Processus des formulaires > Paramètres du serveur > Paramètres du courrier électronique.
1. Sélectionnez Activer les messages sortants.
1. Dans le champ Serveur SMTP, saisissez le nom ou l’adresse IP du serveur de courrier électronique. Tous les courriers électroniques de notification provenant du processus des formulaires sont envoyés depuis ce serveur de courrier électronique.
1. Dans les champs Nom d’utilisateur et Mot de passe, saisissez le nom et le mot de passe d’ouverture de session à utiliser lorsque le serveur SMTP vous invite à vous authentifier. Si l’ouverture d’une session anonyme est autorisée, laissez ces champs vides.
1. Dans la zone Adresse électronique, saisissez l’adresse électronique à utiliser comme adresse de réponse pour le courrier électronique envoyé par le processus des formulaires.

   >[!NOTE]
   >
   >Si vous utilisez Microsoft Exchange Server et que l’adresse électronique n’est pas valide, Microsoft Exchange Server n’envoie pas de message électronique aux listes de distribution. Pour résoudre ce problème, sélectionnez l’option **Activer la communication externe** séparément pour chaque liste de distribution dans Microsoft Exchange Server.

1. Cliquez sur Enregistrer.

>[!NOTE]
>
>si les informations que vous entrez sont incorrectes, vous pouvez cliquer sur Annuler pour revenir à la page précédente.

### Configuration de modèles de courrier électronique pour utiliser l’espace de travail AEM Forms {#configuring-email-templates-to-use-html-workspace}

>[!NOTE]
>
>Flex Workspace est obsolète pour la version d’AEM Forms.

Par défaut, les courriers électroniques envoyés par AEM forms contiennent des liens vers Flex Workspace (obsolète pour AEM forms on JEE). Vous pouvez configurer AEM forms pour envoyer des courriers électroniques contenant des liens vers l’espace de travail AEM Forms. Pour en savoir plus sur les avantages de l’espace de travail AEM Forms par rapport à Flex Workspace (obsolète pour AEM forms on JEE), consultez [cet](/help/forms/using/features-html-workspace-available-flex.md) article.

1. Dans Administration Console, cliquez sur Accueil > Services > Processus des formulaires > Paramètres du serveur > Notifications de tâche.
1. Ouvrez un modèle d’affectation des tâches.
1. Définissez le modèle dans les notifications de tâche à l’adresse suivante : `https://@@notification-host@@:8080/lc/libs/ws/index.html?taskId=@@taskid@@`

   ```java
   https://@@notification-host@@:8080/lc/libs/ws/index.html?taskId=@@taskid@@
   ```

## Configuration des notifications destinées aux utilisateurs et aux groupes {#configuring-notifications-for-users-and-groups}

Dans la page Notification de tâche, vous pouvez configurer les modèles qui vont être utilisés par le processus des formulaires pour générer le courrier électronique de notification envoyés aux utilisateurs et aux groupes. Vous pouvez personnaliser et formater les notifications à l’aide de variables du processus des formulaires.

Vous pouvez configurer les types de notifications suivants pour les utilisateurs et les groupes :

* rappels
* affectations de tâches
* échéances

Pour générer des notifications électroniques pour un groupe, spécifiez une adresse électronique pour le groupe dans User Management <!--Fix broken link See Setting up and organizing users -->Lorsque le processus des formulaires envoie une notification électronique à un groupe, chaque membre du groupe qui possède une adresse électronique reçoit le courrier électronique de notification. Lorsqu’un membre du groupe reçoit une notification électronique et souhaite demander la tâche, il doit cliquer sur le lien de demande dans la notification, de façon à ouvrir la page des détails de la tâche dans Workspace. Le membre peut ensuite demander ou demander et ouvrir la tâche.

>[!NOTE]
>
>Flex Workspace est obsolète pour la version d’AEM forms.

### Configuration des rappels pour les utilisateurs ou les groupes {#configure-reminders-for-users-or-groups}

Vous pouvez choisir d’envoyer des notifications de rappel à l’utilisateur ou au groupe affecté à une tâche lorsque le délai d’exécution de cette tâche se rapproche. Les règles déterminant exactement quand une notification de rappel est envoyée sont décidées par le développeur du processus.

1. Dans Administration Console, cliquez sur Services > Processus des formulaires > Paramètres du serveur > Notifications de tâche.
1. Sous Type de notification, cliquez sur Rappel (pour les utilisateurs) ou sur Groupe : rappel (pour les groupes).
1. Sélectionnez Activer le rappel ou Activer le groupe - Rappel.
1. (Notifications utilisateur seulement) Pour inclure le formulaire et ses données en pièce jointe au courrier électronique de rappel, sélectionnez Inclure les données de formulaire.
1. Dans le champ Objet, saisissez le texte de l’objet du courrier électronique. Ce champ est prérenseigné avec un texte par défaut. Pour plus d’informations sur la personnalisation de ce champ, voir [Personnalisation du contenu des notifications](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Dans le champ Modèle de notification, saisissez le texte du corps du courrier électronique. Ce champ est prérenseigné avec un texte par défaut. Pour plus d’informations sur la personnalisation de ce champ, voir [Personnalisation du contenu des notifications](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Dans la liste Format de message, sélectionnez le format sous lequel envoyer le message électronique, à savoir HTML ou Texte. Le format par défaut est HTML.
1. Dans la liste Encodage du courrier électronique, sélectionnez le format d’encodage à utiliser pour le message électronique. Le format par défaut UTF-8 est utilisé par la plupart des utilisateurs, exception faite du Japon. Les utilisateurs japonais sélectionnent généralement le format ISO2022-JP.
1. Cliquez sur Enregistrer.

### Configuration des notifications d’affectation de tâche pour des utilisateurs ou des groupes {#configure-task-assignment-notifications-for-users-or-groups}

Vous pouvez envoyer des notifications d’affectation de tâche à un utilisateur ou à un groupe lorsqu’une tâche lui est affectée.

1. Dans Administration Console, cliquez sur Services > Processus des formulaires > Paramètres du serveur > Notifications de tâche.
1. Sous Type de notification, cliquez sur Affectation de tâche pour les utilisateurs ou sur Groupe - Affectation de tâche pour les groupes.
1. Sélectionnez Activer affectation de tâche pour les utilisateurs ou Activer Groupe - Affectation de tâche pour les groupes.
1. (Notifications utilisateur seulement) Pour inclure le formulaire et ses données en pièce jointe au courrier électronique d’affectation de tâche, sélectionnez Inclure les données de formulaire.
1. Dans le champ Objet, saisissez le texte de l’objet du courrier électronique. Ce champ est prérenseigné avec un texte par défaut. Pour plus d’informations sur la personnalisation de ce champ, voir [Personnalisation du contenu des notifications](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Dans le champ Modèle de notification, saisissez le texte du corps du courrier électronique. Ce champ est prérenseigné avec un texte par défaut. Pour plus d’informations sur la personnalisation de ce champ, voir [Personnalisation du contenu des notifications](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Dans la liste Format de message, sélectionnez le format sous lequel envoyer le message électronique, à savoir HTML ou Texte. Le format par défaut est HTML.
1. Dans la liste Encodage du courrier électronique, sélectionnez le format d’encodage à utiliser pour le message électronique. Le format par défaut UTF-8 est utilisé par la plupart des utilisateurs, exception faite du Japon. Les utilisateurs japonais sélectionnent généralement le format ISO2022-JP.
1. Cliquez sur Enregistrer.

### Configuration des notifications d’échéance pour des utilisateurs ou des groupes {#configure-deadline-notifications-for-users-or-groups}

Vous pouvez choisir d’envoyer des notifications d’échéance à des utilisateurs et à des groupes pour les informer que le délai d’exécution d’une tâche affectée est dépassé. En règle générale, une notification d’échéance n’est envoyée qu’à titre d’information, car l’utilisateur ne peut plus agir sur la tâche affectée.

1. Dans Administration Console, cliquez sur Services > Processus des formulaires > Paramètres du serveur > Notifications de tâche.
1. Sous Type de notification, cliquez sur Echéance (pour les utilisateurs) ou sur Groupe : délai (pour les groupes).
1. Sélectionnez Activer l’échéance ou Activer le groupe - Echéance.
1. Dans le champ Objet, saisissez le texte de l’objet du courrier électronique. Ce champ est prérenseigné avec un texte par défaut. Pour plus d’informations sur la personnalisation de ce champ, voir [Personnalisation du contenu des notifications](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Dans le champ Modèle de notification, saisissez le texte du corps du courrier électronique. Ce champ est prérenseigné avec un texte par défaut. Pour plus d’informations sur la personnalisation de ce champ, voir [Personnalisation du contenu des notifications](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Dans la liste Format de message, sélectionnez le format sous lequel envoyer le message électronique, à savoir HTML ou Texte. Le format par défaut est HTML.
1. Dans la liste Encodage du courrier électronique, sélectionnez le format d’encodage à utiliser pour le message électronique. Le format par défaut UTF-8 est utilisé par la plupart des utilisateurs, exception faite du Japon. Les utilisateurs japonais sélectionnent généralement le format ISO2022-JP.
1. Cliquez sur Enregistrer.

### Masquage de la balise DO NOT DELETE pour tous les courriers électroniques {#hide-the-do-not-delete-tag-for-all-emails}

Vous pouvez configurer le service de messagerie de façon à masquer la balise de suivi DO NOT DELETE dans tous les courriers électroniques envoyés par le biais d’un processus pour des intervenants humains. Pour plus d’informations, voir [Masquage des balises DO-NOT-DELETE en CSS](https://blogs.adobe.com/LiveCycleHelp/2013/09/how-to-hide-the-do-not-delete-tag-with-css.html)

## Configuration des notifications destinées aux administrateurs {#configuring-notifications-for-administrators}

Vous pouvez configurer les modèles auxquels le processus des formulaires fait appel pour générer les notifications électroniques envoyées aux administrateurs.

Vous pouvez configurer les types de notifications suivants pour les administrateurs :

* branche bloquée
* opération bloquée

### Configuration de notifications de branche bloquée {#configure-stalled-branch-notifications}

Si une branche bloque (l’exécution d’une opération est interrompue délibérément ou suite à une erreur), une notification peut être envoyée à un administrateur ou à un autre utilisateur, capable d’étudier le problème.

1. Dans Administration Console, cliquez sur Services > Processus des formulaires > Paramètres du serveur > Notifications de l’administrateur.
1. Sous Type de notification, cliquez sur Branche bloquée.
1. Sélectionnez Activer branche bloquée.
1. Dans le champ Adresses électronique, saisissez les adresses des utilisateurs à informer lorsqu’une branche bloque. Utilisez le format utilisateur@domaine.com et séparez les adresses par une virgule. En règle générale, il s’agit d’une adresse d’administrateur.
1. Dans le champ Objet, saisissez le texte de l’objet du courrier électronique. Ce champ est prérenseigné avec un texte par défaut. Pour plus d’informations sur la personnalisation de ce champ, voir [Personnalisation du contenu des notifications](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Dans le champ Modèle de notification, saisissez le texte du corps du courrier électronique. Ce champ est prérenseigné avec un texte par défaut. Pour plus d’informations sur la personnalisation de ce champ, voir [Personnalisation du contenu des notifications](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Dans la liste Format de message, sélectionnez le format sous lequel envoyer le message électronique, à savoir HTML ou Texte. Le format par défaut est HTML.
1. Dans la liste Encodage du courrier électronique, sélectionnez le format d’encodage à utiliser pour le message électronique. Le format par défaut UTF-8 est utilisé par la plupart des utilisateurs, exception faite du Japon. Les utilisateurs japonais sélectionnent généralement le format ISO2022-JP.
1. Cliquez sur Enregistrer.

### Configuration de notifications d’opération bloquée {#configure-stalled-operation-notifications}

Si une opération bloque (l’exécution d’une opération est interrompue délibérément ou suite à une erreur), une notification peut être envoyée à un administrateur ou à un autre utilisateur, capable d’étudier le problème.

1. Dans Administration Console, cliquez sur Services > Processus des formulaires > Paramètres du serveur > Notifications de l’administrateur.
1. Sous Type de notification, cliquez sur Opération bloquée.
1. Sélectionnez Activer opération bloquée.
1. Dans le champ Adresses électroniques, saisissez les adresses des utilisateurs à informer lorsqu’une opération bloque. Utilisez le format utilisateur@domaine.com et séparez les adresses par une virgule. En règle générale, il s’agit d’une adresse d’administrateur.
1. Dans le champ Objet, saisissez le texte de l’objet du courrier électronique. Ce champ est prérenseigné avec un texte par défaut. Pour plus d’informations sur la personnalisation de ce champ, voir [Personnalisation du contenu des notifications](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Dans le champ Modèle de notification, saisissez le texte du corps du courrier électronique. Ce champ est prérenseigné avec un texte par défaut. Pour plus d’informations sur la personnalisation de ce champ, voir [Personnalisation du contenu des notifications](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Cliquez sur Enregistrer.

## Personnalisation du contenu des notifications {#customizing-the-content-of-notifications}

Les pages Notifications de tâche et Notifications de l’administrateur offrent différentes fonctionnalités qui permettent de personnaliser les messages de notification :

* éditeur de texte enrichi
* sélecteur de variables
* Génération d’URL

### Editeur de texte enrichi {#rich-text-editor}

La zone Modèle de notification est un éditeur de texte enrichi qui vous permet de générer des pages HTML pour les messages de notification électronique. Elle offre des options de mise en forme des polices et des paragraphes, accessibles sous le champ Modèle de notification. Ces options permettent notamment d’intervenir sur le type, la taille, le style et la couleur des polices ainsi que sur les puces et l’alignement des paragraphes.

### Génération d’URL {#url-generation}

Pour les notifications de tâche uniquement, le processus des formulaires inclut deux configurations d’URL prédéfinies que vous pouvez faire glisser de la liste Génération d’URL vers le champ Modèle de notification, puis personnaliser :

* L’URL Ouvrir la tâche est disponible pour les notifications de type Rappel et Affectation de tâche. Cette URL fournit un lien vers la tâche dans Workspace, ce qui permet à l’utilisateur d’accéder rapidement à la tâche à partir du courrier électronique de notification. Lorsque vous faites glisser l’URL Ouvrir la tâche vers le champ Modèle de notification, l’URL est au format suivant :

   `https://@@notification-host@@:<PORT>/workpace/Main.html?taskId=@@taskid@@`

* L’URL Demander une tâche est disponible pour les notifications de type Groupe - Rappel et Groupe - Affectation de tâche. Cette URL fournit un lien vers la page des détails de la tâche dans Workspace, à partir de laquelle l’utilisateur peut demander ou demander et ouvrir la tâche. Lorsque vous faites glisser l’URL Demander une tâche vers le champ Modèle de notification, l’URL est au format suivant :

   `https://@@notification-host@@:<PORT>/workpace/Main.html?taskId=@@taskid@@`

>[!NOTE]
>
>Flex Workspace est obsolète pour la version d’AEM Forms.

If your solution is deployed in a clustered environment, replace `@@notification-host@@` with the cluster address.

`<`*PORT *`>`est le numéro de port de l’écouteur HTTP pour le serveur d’applications. Les ports d’écouteur HTTP par défaut pour les serveurs d’applications pris en charge sont les suivants :

**JBoss :** 8080

**Oracle WebLogic Server :** 7001

**IBM WebSphere :** 9080

To make these URLs function correctly, replace `<`*PORT *`>`with the port number that is appropriate for your environment.

>[!NOTE]
>
>si vous utilisez une application Web personnalisée autre que Forms pour permettre aux utilisateurs d’accéder aux tâches, vous devez utiliser le format d’URL approprié pour votre application personnalisée.

### Sélecteur de variables {#variable-picker}

La liste Sélectionneur de variables fournit des variables utiles que vous pouvez faire glisser vers les champs Objet ou Modèle de notification. When you drop a variable in the Subject or Notification Template boxes, it changes to the actual forms workflow variable name with two @ symbols on either side of it, for example, `@@taskid@@`.

Pour les rappels, affectations de tâche et échéances des utilisateurs et des groupes, vous pouvez utiliser les variables suivantes dans les champs Objet et Modèle de notification :

**description** Contenu de la propriété Description, tel que défini dans l’étape utilisateur (point de début, opération d’affectation de Tâche ou opération d’affectation de plusieurs Tâches) du processus dans Workbench.

**instructions** Contenu de la propriété Instructions de la Tâche, tel que défini dans l’étape utilisateur du processus dans Workbench.

**hôte** de notification Nom d’hôte du serveur d’applications AEM forms.

**process-name** Nom du processus.

**operation-name** Nom de l’étape.

**taskid** Identifiant unique de la tâche active.

**actions** Génère une liste numérotée de routes valides (par exemple, Approuver, Rejeter) sur lesquelles le destinataire peut cliquer.

De plus, pour les rappels, affectations de tâche et échéances de groupe, vous pouvez aussi utiliser les variables suivantes :

**nom** du groupe Nom du groupe auquel est affectée la tâche.

>[!NOTE]
>
>si une variable ne comporte aucune valeur, une valeur vide est renvoyée.

Pour les branches bloquées, vous pouvez utiliser les variables suivantes dans les champs Objet et Modèle de notification :

**id** -branche Identifiant de branche.

**process-id** Identifiant de l’instance de processus.

**hôte** de notification Nom d’hôte du serveur d’applications AEM forms.

Pour les opérations bloquées, vous pouvez utiliser les variables suivantes dans les champs Objet et Modèle de notification :

**action-id** Identifiant de l&#39;opération.

**id** -branche Identifiant de branche.

**process-id** Identifiant de l’instance de processus.

**hôte** de notification Nom d’hôte du serveur d’applications AEM forms.

### Utilisation d’une variable dans la zone Objet {#using-a-variable-in-the-subject-box}

Si vous saisissez le texte suivant dans le champ Objet pour les notifications d’affectation de tâches :

`Please complete task @@taskid@@`

L’utilisateur reçoit un courrier électronique avec l’objet suivant si la tâche 376 lui est affectée :

`Please complete task 376`

### Utilisation de variables dans le champ Modèle de notification {#using-variables-in-the-notification-template-box}

Si vous saisissez le texte suivant dans le champ Modèle de notification pour des notifications de branches bloquées :

`Branch @@branch-id@@ has stalled! You have received this notification from @@notification-host@@.`

The administrator receives an email message that contains the following content if the branch number is 4868 and the server name is `ServerXYZ`:

`Branch 4868 has stalled! You have received this notification from ServerXYZ.`

## Configuration de connexions Business Activity Monitoring {#configuring-business-activity-monitoring-connections}

Business Activity Monitoring, module proposé en option, présente plusieurs tableaux de bord opérationnels qui permettent de suivre en temps réel les opérations et des indicateurs de performances clés.

Dans la page Paramètres de configuration BAM, vous définissez les connexions au serveur qui exécute BAM afin qu’il soit possible d’assurer le suivi des événements liés aux processus et de transférer ces événements vers ce serveur.

1. Dans Administration Console, cliquez sur Services > Processus des formulaires > Paramètres du serveur > Paramètres de configuration BAM.
1. Dans le champ Hôte BAM, saisissez le nom du serveur qui exécute BAM. La valeur par défaut est localhost.
1. Dans le champ Port BAM, saisissez le numéro du port à utiliser pour établir la connexion au serveur qui exécute BAM. Le port BAM par défaut pour JBoss est 8080, 7001 pour WebLogic et 9080 pour WebSphere.
1. Dans le champ de serveur hôte, saisissez le nom ou l’adresse IP du serveur Forms hôte. la valeur par défaut est localhost.
1. Dans le champ Port du serveur, saisissez le numéro de port utilisé par le serveur Forms.
1. Dans les champs Nom d’utilisateur et Mot de passe, saisissez l’ID utilisateur et le mot de passe permettant d’accéder au serveur BAM. Le nom d’utilisateur par défaut est CognosNowAdmin et le mot de passe par défaut est manager.
1. Cliquez sur Enregistrer.

