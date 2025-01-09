---
title: Configuration des calendriers professionnels
description: Les calendriers professionnels définissent les jours ouvrés et non ouvrés de votre entreprise. Découvrez comment configurer les calendriers professionnels.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 4282718a-41f1-411a-9cd7-8c470005107d
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '1901'
ht-degree: 100%

---

# Configuration des calendriers professionnels {#configuring-business-calendars}

Les *calendriers professionnels* définissent les jours ouvrés et non ouvrés (par exemple, jours fériés, week-ends et jours de fermeture) de votre entreprise. Lors de l’utilisation de calendriers professionnels, AEM Forms ignore les jours non ouvrés lors de certains calculs de date. Dans Workbench, vous pouvez indiquer s’il faut utiliser des calendriers professionnels pour les événements associés à l’utilisateur ou l’utilisatrice, tels que les rappels, les échéances et les transmissions de tâches, ou pour les actions non associées aux utilisateurs et utilisatrices, telles que les événements de minuterie et le service d’attente.

Par exemple, un rappel de tâche est configuré pour se produire trois jours ouvrés après l’affectation de la tâche à un utilisateur ou une utilisatrice. La tâche est affectée le jeudi. Cependant, les trois jours suivants ne sont pas ouvrés car le vendredi est un jour férié et les deux jours suivants sont des jours de week-end. Le rappel est donc envoyé le mercredi de la semaine prochaine.

>[!NOTE]
>
>Lors du calcul des dates et heures à l’aide de calendriers professionnels, AEM Forms utilise la date et l’heure du serveur sur lequel il s’exécute et ne s’adapte pas à la différence entre les fuseaux horaires. Par exemple, si un rappel de tâche est planifié à 10 h 00 sur un serveur s’exécutant à Londres, mais que l’utilisateur ou l’utilisatrice recevant le rappel est à New York City, il ou elle recevra le rappel à 5 h 00 (heure locale).

## Utiliser le calendrier professionnel par défaut {#using-the-default-business-calendar}

AEM Forms fournit un calendrier professionnel par défaut (*le calendrier intégré*) qui désigne les samedis et dimanches en tant que jours non ouvrés. Si tous les utilisateurs et utilisatrices de votre entreprise ont les mêmes jours non ouvrés, vous pouvez mettre à jour le calendrier professionnel par défaut en fonction de votre entreprise. Lorsque vous utilisez uniquement le calendrier professionnel par défaut, vous n’avez pas besoin d’activer les calendriers professionnels dans User Management ni de fournir des mappages. Lorsqu’aucun autre calendrier professionnel n’est défini, AEM Forms utilise le calendrier professionnel par défaut.

## Configurer plusieurs calendriers professionnels {#setting-up-multiple-business-calendars}

Si certains utilisateurs ou utilisatrices de votre entreprise ont des jours non ouvrés différents, vous pouvez définir plusieurs calendriers professionnels et configurer des mappages qui permettent de définir l’exécution d’un calendrier professionnel pour un utilisateur ou une utilisatrice en particulier.

### Définir plusieurs calendriers professionnels {#define-multiple-business-calendars}

1. Choisissez comment vous associerez le calendrier professionnel approprié à un utilisateur ou une utilisatrice. Il existe deux manières d’associer un calendrier professionnel à un utilisateur ou une utilisatrice :

   **Appartenance à un groupe :** vous pouvez attribuer un calendrier professionnel à un utilisateur ou une utilisatrice selon son appartenance à un groupe. Dans ce cas, chaque utilisateur et utilisatrice du groupe utilisera le même calendrier professionnel.

   Si un utilisateur ou une utilisatrice est membre de deux groupes différents et que ces groupes sont mappés à deux calendriers professionnels différents, AEM Forms utilise le premier calendrier qui apparaît dans les résultats de recherche. Dans ce cas, pensez à utiliser des clés de calendrier professionnel pour associer des utilisateurs et utilisatrices à des calendriers professionnels.

   **Clés de calendrier professionnel :** vous pouvez affecter un calendrier professionnel à un utilisateur en fonction d’une clé de calendrier professionnel, paramètre à définir dans User Management. Associez ensuite la clé de calendrier professionnel à un calendrier professionnel dans Forms Workflow.

   Les clés de calendrier professionnel sont attribuées à des utilisateurs et des utilisatrices en fonction du domaine utilisé, tel que le domaine d’entreprise, local ou hybride. Pour plus d’informations sur la configuration des domaines, consultez [Ajouter des domaines](/help/forms/using/admin-help/adding-domains.md#adding-domains).

   Si vous utilisez un domaine local ou hybride, les informations relatives aux utilisateurs et utilisatrices ne sont stockées que dans la base de données User Management. Pour définir la clé de calendrier professionnel pour ces utilisateurs et utilisatrices, saisissez une chaîne de caractères dans le champ « Clé du calendrier professionnel » lors de l’ajout ou de la modification d’un utilisateur ou d’une utilisatrice dans User Management. (Voir [Ajout et configuration des utilisateurs et utilisatrices](/help/forms/using/admin-help/adding-configuring-users.md#adding-and-configuring-users).) Ensuite, mappez les clés de calendrier professionnel (les chaînes) aux calendriers professionnels dans Forms Workflow. (Voir [Associer des utilisateurs/utilisatrices et des groupes à un calendrier professionnel](configuring-business-calendars.md#mapping-users-and-groups-to-a-business-calendar).)

   Si vous utilisez un domaine d’entreprise, les informations sur les utilisateurs et utilisatrices résident dans un système de stockage tiers, tel qu’un répertoire LDAP, que User Management synchronise avec sa base de données. Cette fonction vous permet d’associer une clé de calendrier professionnel à un champ du répertoire LDAP. Par exemple, si chaque utilisateur ou utilisatrice enregistré(e) dans votre répertoire dispose d’un champ « pays » et que vous souhaitez attribuer des calendriers professionnels en fonction du pays où l’utilisateur ou l’utilisatrice se trouve, indiquez le nom du champ « pays » dans le champ « Clé » du calendrier professionnel lors de la spécification des paramètres de l’utilisateur ou utilisatrice pour l’annuaire. (Voir [Configuration des annuaires](/help/forms/using/admin-help/configuring-directories.md#configuring-directories).) Vous pouvez ensuite associer les clés de calendrier professionnel (valeurs définies pour le champ « pays » dans le répertoire LDAP) aux calendriers professionnels dans Forms Workflow. (Voir [Associer des utilisateurs/utilisatrices et des groupes à un calendrier professionnel](configuring-business-calendars.md#mapping-users-and-groups-to-a-business-calendar).)

1. Dans Forms Workflow, définissez un calendrier pour chaque groupe d’utilisateurs et utilisatrices qui partagent les mêmes jours non ouvrés. (Voir [Créer ou mettre à jour un calendrier professionnel](configuring-business-calendars.md#create-or-update-a-business-calendar).)
1. Dans Forms Workflow, mappez les clés de calendrier professionnel ou les appartenances à des groupes pour chaque calendrier. (Voir [Associer des utilisateurs/utilisatrices et des groupes à un calendrier professionnel](configuring-business-calendars.md#mapping-users-and-groups-to-a-business-calendar).)
1. Dans Workbench, le développeur ou la développeuse de processus choisit d’utiliser des calendriers professionnels pour les rappels, les échéances et les transmissions. (Voir [Aide de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63_fr).)

   Si le développeur ou la développeuse de processus choisit d’utiliser des calendriers professionnels, AEM Forms sélectionne dynamiquement le calendrier professionnel approprié en fonction du paramètre User Management et des mappages de calendrier professionnel définis dans la console d’administration. Si aucun mappage n’existe, le calendrier par défaut est utilisé.

   S’il ou elle choisit de ne pas utiliser de calendriers professionnels, le calcul de date de l’événement ne prend pas en compte les jours non ouvrés. Par exemple, une échéance de tâche est configurée pour se produire trois jours après l’attribution de la tâche à l’utilisateur ou l’utilisatrice. La tâche est affectée le jeudi. L’échéance de la tâche se produit le dimanche, même s’il s’agit d’un jour de week-end.

## Créer ou mettre à jour un calendrier professionnel {#create-or-update-a-business-calendar}

Si votre organisation comprend différents groupes d’utilisateurs et utilisatrices pour lesquels les jours non ouvrés diffèrent, vous pouvez définir plusieurs calendriers professionnels. Vous pouvez également modifier les calendriers existants, y compris le calendrier intégré par défaut fourni avec AEM Forms.

>[!NOTE]
>
> * Si vous ne créez pas de nouveau calendrier professionnel, le calendrier par défaut est utilisé.
> * Vérifiez que l’utilisateur ou l’utilisatrice dispose de droits d’administration pour accéder à la console d’administration.


1. Dans la console d’administration, cliquez sur Services > Forms Workflow > Calendriers professionnels.
2. Pour ajouter un nouveau calendrier professionnel, cliquez sur ![bus_cal_plus](assets/bus_cal_plus.png). Le texte *Nouveau calendrier* s’affiche dans la liste déroulante. Sélectionnez le texte et saisissez un autre nom pour votre calendrier.

   Pour modifier un calendrier professionnel existant, sélectionnez-le dans la liste déroulante.

3. Sous Jours non ouvrés par défaut, sélectionnez les jours non ouvrés par défaut de votre choix dans la semaine (week-ends, par exemple).
4. [Facultatif] Sélectionnez Utiliser les heures ouvrables et définissez les heures de début et de fin d’une journée de travail.

   Si vous sélectionnez cette option, un événement qui se produit avant la plage horaire définie est déplacé au début de la plage horaire et un événement qui se produit après est déplacé à l’heure de début du prochain jour ouvré.

   Par exemple, supposons qu’une personne soit affectée à une tâche à 2 h le mardi et que le rappel de cette tâche soit défini sur deux jours ouvrés. Sans les heures de bureau, le rappel a lieu à 2 h le jeudi. Si les heures de bureau sont définies de 8 h à 17 h, le rappel est déplacé à 8 h le jeudi. Sans les heures de bureau, si un rappel est créé pour 18 h le mardi, il aura lieu après les heures de bureau le jeudi. Si les heures de bureau sont définies de 8 h à 17 h, le rappel aura lieu à 8 h le vendredi.

5. Dans le calendrier de gauche, double-cliquez sur un autre jour non ouvré, comme congés. Vous ne pouvez pas sélectionner de jours sur des périodes antérieures. Les jours non ouvrés sélectionnés apparaissent dans une liste sur la droite et la date s’affiche deux fois sur une seule ligne. Sélectionnez la date sur la gauche pour pouvoir taper le nom ou la description du jour non ouvré.

   Pour supprimer un jour non ouvré de la liste, cliquez sur ![bus_cal_trash](assets/bus_cal_trash.png) près du jour concerné.

6. [Facultatif] Pour définir ce calendrier comme calendrier par défaut, sélectionnez Calendrier par défaut. Le calendrier par défaut est utilisé lorsqu’il n’existe aucune autre association de calendrier pour des événements utilisateur ou si aucun calendrier professionnel n’est spécifié pour l’événement de temporisation ou le service d’attente. Vous ne pouvez pas supprimer le calendrier par défaut.
7. La définition des jours non ouvrés terminée, sélectionnez Calendrier activé pour activer le calendrier, puis cliquez sur Enregistrer.

   Si vous mettez à jour un calendrier existant, la nouvelle version prend effet immédiatement et est utilisée pour tous les calculs de calendrier professionnel, y compris pour les tâches déjà en cours d’exécution.

   >[!NOTE]
   >
   >Si vous n’activez pas le calendrier, le calendrier par défaut est utilisé.

## Association d’utilisateurs, d’utilisatrices et de groupes à un calendrier professionnel {#mapping-users-and-groups-to-a-business-calendar}

Il existe deux méthodes pour associer un calendrier professionnel à un utilisateur ou une utilisatrice. Vous pouvez affecter des calendriers professionnels à des utilisateurs et utilisatrices en fonction d’une clé de calendrier professionnel ou d’un groupe d’annuaire auquel l’utilisateur ou l’utilisatrice appartient. Utilisez l’onglet Association pour indiquer la méthode qu’AEM Forms doit utiliser et pour associer les clés et les groupes de calendrier professionnel aux calendriers professionnels. Pour plus d’informations sur l’association de clés de calendrier professionnel à des utilisateurs et utilisatrices, consultez [Configuration de plusieurs calendriers professionnels](configuring-business-calendars.md#setting-up-multiple-business-calendars).

### Association de calendriers professionnels à des utilisateurs et utilisatrices à partir de clés de calendrier professionnel {#associate-business-calendars-with-users-based-on-business-calendar-keys}

1. Dans la console d’administration, cliquez sur Services > Processus des formulaires > Calendriers professionnels, puis cliquez sur l’onglet Association.
1. Dans la liste Le système va utiliser, sélectionnez Résolution de la clé du calendrier professionnel du gestionnaire des utilisateurs.
1. Sélectionnez Afficher la clé du calendrier professionnel du gestionnaire des utilisateurs. Une liste des clés de calendrier professionnel définies dans le gestionnaire des utilisateurs s’affiche.

   Pour les domaines locaux et hybrides, la liste affiche les valeurs entrées dans le champ Clé du calendrier professionnel de la gestion des utilisateurs. Pour les domaines d’entreprise (LDAP), la liste affiche l’ensemble unique provenant du champ LDAP (par exemple, « pays ») configuré dans les paramètres de domaine LDAP.

   Si l’administrateur ou administratrice de la gestion des utilisateurs n’a pas défini de clé de calendrier professionnel, la liste est vide.

1. Pour chaque élément de la liste Clé du calendrier professionnel GU, sélectionnez un Calendrier.
1. Cliquez sur Enregistrer.

### Association de calendriers professionnels à des utilisateurs, utilisatrices et des groupes à partir de groupes de services d’annuaires {#associate-business-calendars-with-users-and-groups-based-on-directory-service-groups}

1. Dans la console d’administration, cliquez sur Services > Processus des formulaires > Calendriers professionnels, puis cliquez sur l’onglet Association.
1. Dans la liste Le système va utiliser, sélectionnez Groupes définis par le serveur d’annuaires.
1. Dans l’onglet Association, sélectionnez Afficher les groupes de services d’annuaire. Une liste s’affiche, contenant les groupes définis dans la gestion des utilisateurs. (Voir [Paramètres d’annuaire](/help/forms/using/admin-help/configuring-directories.md#directory-settings).)

   >[!NOTE]
   >
   >Dans Workbench, si vous avez configuré un service Utilisateur pour qu’il utilise des calendriers professionnels et si le service est attribué à un groupe, AEM Forms utilise les associations du groupe indiquées pour créer le calendrier du groupe. AEM Forms utilise toujours les associations des groupes pour créer le calendrier des groupes, même lorsque vous utilisez des clés de calendrier professionnel pour créer le calendrier des utilisateurs et utilisatrices. Si aucun mappage de groupe n’est trouvé, le calendrier professionnel par défaut est utilisé.

1. Pour chaque élément de la liste Groupe de services d’annuaire, sélectionnez un calendrier.
1. Cliquez sur Enregistrer.

## Exportation et importation de calendriers professionnels {#exporting-and-importing-business-calendars}

AEM Forms vous permet d’exporter et d’importer vos calendriers professionnels sous forme de fichiers XML. Vous pouvez utiliser cette fonctionnalité pour déplacer des calendriers d’un système d’évaluation vers un système de production.

>[!NOTE]
>
>Cette fonctionnalité exporte et importe tous les calendriers professionnels définis, y compris le calendrier professionnel par défaut fourni par AEM Forms. Un calendrier professionnel importé portant le même nom qu’un calendrier existant remplace le calendrier existant.

### Exportation de calendriers professionnels {#export-business-calendars}

1. Dans la console d’administration, cliquez sur Services > Forms Workflow > Calendriers professionnels.
1. Cliquez sur Exporter et enregistrez le fichier XML.

### Importation de calendriers professionnels {#import-business-calendars}

1. Dans la console d’administration, cliquez sur Services > Forms Workflow > Calendriers professionnels.
1. Cliquez sur Importer.
1. Sélectionnez le fichier XML contenant les calendriers professionnels exportés et cliquez sur Ouvrir.

## Suppression d’un calendrier professionnel {#delete-a-business-calendar}

Vous pouvez supprimer les calendriers professionnels dont votre entreprise n’a plus besoin. Si vous supprimez un calendrier professionnel qui est toujours mappé à des personnes et à des groupes, le calendrier par défaut sera utilisé.

1. Dans la console d’administration, cliquez sur Services > Forms Workflow > Calendriers professionnels.
1. Sélectionnez le calendrier.
1. Cliquez sur Supprimer.
