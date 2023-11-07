---
title: Configuration des calendriers professionnels
seo-title: Configuring Business Calendars
description: Les calendriers professionnels définissent les jours ouvrés et non ouvrés de votre entreprise. Découvrez comment configurer les calendriers professionnels.
seo-description: Business calendars define business and non-business days for your organization. Learn how to configure the business calendars.
uuid: 0ba610b8-72a8-480c-8783-70d98cbe890a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7a85e13d-4800-47c4-812a-5c6e2355298a
exl-id: 4282718a-41f1-411a-9cd7-8c470005107d
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1901'
ht-degree: 10%

---

# Configuration des calendriers professionnels {#configuring-business-calendars}

*Calendriers professionnels* définissez les jours ouvrés et non ouvrés (par exemple, jours fériés, week-ends et jours de fermeture de la société) de votre entreprise. Lors de l’utilisation de calendriers professionnels, AEM forms ignore les jours non ouvrés lors de certains calculs de date. Dans Workbench, vous pouvez indiquer s’il faut utiliser des calendriers professionnels pour les événements associés à l’utilisateur, tels que les rappels, les échéances et les transmissions de tâches, ou pour les actions non associées aux utilisateurs, telles que les événements de minuteur et le service d’attente.

Par exemple, un rappel de tâche est configuré pour se produire trois jours ouvrés après l’affectation de la tâche à un utilisateur. La tâche est affectée le jeudi. Cependant, les trois jours suivants ne sont pas ouvrés car le vendredi est un jour férié et les deux jours suivants sont des jours de week-end. Le rappel est donc envoyé le mercredi de la semaine prochaine.

>[!NOTE]
>
>Lors du calcul des dates et heures à l’aide de calendriers professionnels, AEM forms utilise la date et l’heure du serveur sur lequel il s’exécute et ne s’adapte pas à la différence entre les fuseaux horaires. Par exemple, si un rappel de tâche est planifié à 10 h 00 sur un serveur s’exécutant à Londres, mais que l’utilisateur recevant le rappel se trouve à New York, l’utilisateur recevra le rappel à 5 h 00 (heure locale).

## Utilisation du calendrier professionnel par défaut {#using-the-default-business-calendar}

AEM Forms fournit un calendrier professionnel par défaut (*le calendrier intégré*) qui désigne les samedis et dimanches en tant que jours non ouvrés. Si tous les utilisateurs de votre entreprise ont les mêmes jours non ouvrés, vous pouvez mettre à jour le calendrier professionnel par défaut en fonction de votre entreprise. Lorsque vous utilisez uniquement le calendrier professionnel par défaut, vous n’avez pas besoin d’activer les calendriers professionnels dans User Management ni de fournir des mappages. Lorsqu’aucun autre calendrier professionnel n’est défini, AEM forms utilise le calendrier professionnel par défaut.

## Configuration de plusieurs calendriers professionnels {#setting-up-multiple-business-calendars}

Si certains utilisateurs de votre entreprise ont des jours non ouvrés différents, vous pouvez définir plusieurs calendriers professionnels et configurer des mappages qui permettent de définir l’exécution d’un calendrier professionnel pour un utilisateur.

### Définition de plusieurs calendriers professionnels {#define-multiple-business-calendars}

1. Choisissez comment vous associerez le calendrier professionnel approprié à un utilisateur. Il existe deux manières d’associer un calendrier professionnel à un utilisateur :

   **Appartenance à un groupe :** vous pouvez affecter un calendrier professionnel à un utilisateur selon son appartenance à un groupe. Dans ce cas, chaque utilisateur du groupe utilisera le même calendrier professionnel.

   Si un utilisateur est membre de deux groupes différents et que ces groupes sont mappés à deux calendriers professionnels différents, AEM forms utilise le premier calendrier qui apparaît dans les résultats de recherche. Dans ce cas, pensez à utiliser des clés de calendrier professionnel pour associer des utilisateurs à des calendriers professionnels.

   **Clés de calendrier professionnel :** vous pouvez affecter un calendrier professionnel à un utilisateur en fonction d’une clé de calendrier professionnel, paramètre à définir dans User Management. Vous mappez ensuite la clé de calendrier professionnel à un calendrier professionnel dans le processus des formulaires.

   Les clés de calendrier professionnel sont attribuées à des utilisateurs et des utilisatrices en fonction du domaine utilisé, tel que le domaine d’entreprise, local ou hybride Pour plus d’informations sur la configuration des domaines, voir [Ajout de domaines](/help/forms/using/admin-help/adding-domains.md#adding-domains).

   Si vous utilisez un domaine local ou hybride, les informations relatives aux utilisateurs et utilisatrices ne sont stockées que dans la base de données User Management. Pour définir la clé de calendrier professionnel pour ces utilisateurs, saisissez une chaîne dans le champ Clé du calendrier professionnel lors de l’ajout ou de la modification d’un utilisateur dans User Management. (Voir [Ajouter et configurer des utilisateurs](/help/forms/using/admin-help/adding-configuring-users.md#adding-and-configuring-users).) Vous mappez ensuite les clés de calendrier professionnel (les chaînes) aux calendriers professionnels dans le processus des formulaires. (Voir [Association d’utilisateurs et de groupes à un calendrier professionnel](configuring-business-calendars.md#mapping-users-and-groups-to-a-business-calendar).)

   Si vous utilisez un domaine d’entreprise, les informations sur les utilisateurs résident dans un système de stockage tiers, tel qu’un annuaire LDAP, que User Management synchronise avec la base de données User Management. Vous pouvez ainsi associer une clé de calendrier professionnel à un champ de l&#39;annuaire LDAP. Par exemple, si chaque utilisateur enregistré dans votre annuaire dispose d’un champ &quot;pays&quot; et que vous souhaitez attribuer des calendriers professionnels en fonction du pays où l’utilisateur se trouve, indiquez le nom du champ &quot;pays&quot; dans le champ Clé du calendrier professionnel lors de la spécification des paramètres de l’utilisateur pour l’annuaire. (Voir [Configuration des annuaires](/help/forms/using/admin-help/configuring-directories.md#configuring-directories).) Vous pouvez ensuite associer les clés de calendrier professionnel (valeurs définies pour le champ &quot;pays&quot; dans l’annuaire LDAP) aux calendriers professionnels dans le processus des formulaires. (Voir [Association d’utilisateurs et de groupes à un calendrier professionnel](configuring-business-calendars.md#mapping-users-and-groups-to-a-business-calendar).)

1. Dans le processus des formulaires, définissez un calendrier pour chaque groupe d’utilisateurs qui partagent les mêmes jours non ouvrés. (Voir [Création ou mise à jour d’un calendrier professionnel](configuring-business-calendars.md#create-or-update-a-business-calendar).)
1. Dans le processus des formulaires, mappez les clés de calendrier professionnel ou les appartenances à des groupes pour chaque calendrier. (Voir [Association d’utilisateurs et de groupes à un calendrier professionnel](configuring-business-calendars.md#mapping-users-and-groups-to-a-business-calendar).)
1. Dans Workbench, le développeur de processus choisit d’utiliser des calendriers professionnels pour les rappels, les échéances et les transmissions. (Voir [Aide de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63_fr).)

   Si le développeur de processus choisit d’utiliser des calendriers professionnels, AEM forms sélectionne dynamiquement le calendrier professionnel approprié en fonction du paramètre User Management et des mappages de calendrier professionnel définis dans Administration Console. Si aucun mappage n’existe, le calendrier par défaut est utilisé.

   Si le développeur de processus n’utilise pas de calendriers professionnels, le calcul de date de l’événement traite chaque jour comme un jour ouvré. Par exemple, une échéance de tâche est configurée pour se produire trois jours après l’affectation de la tâche à un utilisateur. La tâche est affectée le jeudi. L’échéance de la tâche se produit le dimanche, même s’il s’agit d’un week-end.

## Création ou mise à jour d’un calendrier professionnel {#create-or-update-a-business-calendar}

Si votre entreprise contient différents ensembles d’utilisateurs pour des jours non ouvrés différents, vous pouvez définir plusieurs calendriers professionnels. Vous pouvez également modifier les calendriers existants, y compris le calendrier intégré par défaut fourni avec AEM forms.

>[!NOTE]
>
>Si vous ne créez pas de calendrier professionnel, le calendrier par défaut est utilisé.

1. Dans Administration Console, cliquez sur Services > Processus Forms > Calendriers professionnels.
1. Pour ajouter un nouveau calendrier professionnel, cliquez sur ![bus_cal_plus](assets/bus_cal_plus.png). Le texte *Nouveau calendrier* apparaît dans la liste déroulante. Sélectionnez le texte et saisissez un autre nom pour votre calendrier.

   Pour modifier un calendrier professionnel existant, sélectionnez-le dans la liste déroulante.

1. Sous Jours non ouvrés par défaut, sélectionnez les jours non ouvrés hebdomadaires, tels que les week-ends.
1. [Facultatif] Sélectionnez Utiliser les heures ouvrables et définissez les heures de début et de fin d’une journée de travail.

   Si vous sélectionnez cette option, un événement qui se produit avant la période spécifiée est déplacé au début de la période et un événement qui se produit après la période est déplacé à l’heure de début du jour ouvré suivant.

   Supposons, par exemple, qu’un utilisateur se voie attribuer une tâche à 02h00 le mardi et que le rappel de cette tâche soit défini sur deux jours ouvrables. Sans les heures de bureau, le rappel se produirait à 2h00 le jeudi. Si les heures de bureau sont définies de 8 h 00 à 17 h 00, le rappel est envoyé à 8 h 00 le jeudi. Sans les heures de bureau, si un événement de rappel a été créé à 18h00 le mardi, le rappel se produit après les heures de bureau le jeudi. Les heures de bureau étant définies de 8 h 00 à 17 h 00, le rappel se produit à 8 h 00 le vendredi.

1. Dans le calendrier de gauche, double-cliquez sur les autres jours non ouvrés, tels que les jours fériés. Vous ne pouvez pas sélectionner de jours dans le passé. Les jours non ouvrés que vous sélectionnez apparaissent dans une liste à droite, la date apparaissant deux fois sur une même ligne. Sélectionnez la date sur la gauche pour saisir le nom ou la description du jour non ouvré.

   Pour supprimer un jour non ouvré de la liste, cliquez sur ![bus_cal_trash](assets/bus_cal_trash.png) près du jour concerné.

1. [Facultatif] Pour définir ce calendrier comme calendrier par défaut, sélectionnez Calendrier par défaut. Le calendrier par défaut est utilisé lorsqu’il n’existe aucun autre mappage de calendrier pour les événements associés à l’utilisateur ou qu’aucun calendrier professionnel n’est spécifié pour l’événement de minuteur ou le service d’attente. Vous ne pouvez pas supprimer le calendrier par défaut.
1. Une fois la définition des jours non ouvrés terminée, sélectionnez Calendrier activé pour l’activer, puis cliquez sur Enregistrer.

   Si vous mettez à jour un calendrier existant, la nouvelle version prend effet immédiatement et est utilisée pour tous les calculs de calendrier professionnel, y compris pour les tâches déjà en cours d’exécution.

   >[!NOTE]
   >
   >Si vous n’activez pas le calendrier, le calendrier par défaut est utilisé.

## Association d’utilisateurs et de groupes à un calendrier professionnel {#mapping-users-and-groups-to-a-business-calendar}

Vous pouvez utiliser deux méthodes pour associer un calendrier professionnel à un utilisateur. Vous pouvez affecter des calendriers professionnels aux utilisateurs en fonction d’une clé de calendrier professionnel ou du groupe d’annuaires auquel appartient l’utilisateur. Vous utilisez l’onglet Mappage pour spécifier la méthode que AEM forms utilisera, ainsi que pour mapper les clés de calendrier professionnel et les groupes aux calendriers professionnels. Pour plus d’informations sur l’association de clés de calendrier professionnel à des utilisateurs, voir [Configuration de plusieurs calendriers professionnels](configuring-business-calendars.md#setting-up-multiple-business-calendars).

### Association de calendriers professionnels à des utilisateurs à partir de clés de calendrier professionnel {#associate-business-calendars-with-users-based-on-business-calendar-keys}

1. Dans Administration Console, cliquez sur Services > Processus des formulaires > Calendriers professionnels, puis cliquez sur l’onglet Mappage .
1. Dans la liste Le système va utiliser, sélectionnez Résolution de la clé du calendrier professionnel du gestionnaire des utilisateurs.
1. Sélectionnez Afficher la clé du calendrier professionnel User Manager. Une liste s’affiche. Elle contient un ensemble unique de clés de calendrier professionnel qui ont été définies dans User Management.

   Pour les domaines locaux et hybrides, la liste affiche les valeurs entrées dans le champ Clé du calendrier professionnel de User Management. Pour les domaines d’entreprise (LDAP), la liste affiche l’ensemble unique renvoyé par le champ LDAP (par exemple, &quot;pays&quot;) configuré dans les paramètres du domaine LDAP.

   Si l’administrateur User Management n’a défini aucune clé de calendrier professionnel, la liste est vide.

1. Pour chaque élément de la liste Clé du calendrier professionnel de la UM, sélectionnez un calendrier.
1. Cliquez sur Enregistrer.

### Association de calendriers professionnels à des utilisateurs et à des groupes en fonction de groupes de services d’annuaire {#associate-business-calendars-with-users-and-groups-based-on-directory-service-groups}

1. Dans Administration Console, cliquez sur Services > Processus des formulaires > Calendriers professionnels, puis cliquez sur l’onglet Mappage .
1. Dans la liste Le système va utiliser, sélectionnez Groupes définis par le serveur d’annuaires.
1. Dans l’onglet Mappage, sélectionnez Afficher les groupes de services d’annuaire. Une liste s’affiche, contenant les groupes définis dans User Management. (Voir [Paramètres d’annuaire](/help/forms/using/admin-help/configuring-directories.md#directory-settings).)

   >[!NOTE]
   >
   >Dans Workbench, si vous avez configuré un service User pour utiliser des calendriers professionnels et que le service est affecté à un groupe, AEM forms utilise les mappages de groupe spécifiés ici pour résoudre le calendrier du groupe. AEM forms utilise toujours des mappages de groupes pour résoudre le calendrier des groupes, même lorsque vous utilisez des clés de calendrier professionnel pour créer le calendrier pour les utilisateurs. Si aucun mappage de groupe n’est trouvé, le calendrier professionnel par défaut est utilisé.

1. Pour chaque élément de la liste Groupe de services d’annuaire, sélectionnez un Calendrier.
1. Cliquez sur Enregistrer.

## Exportation et importation de calendriers professionnels {#exporting-and-importing-business-calendars}

AEM forms vous permet d’exporter et d’importer vos calendriers professionnels sous forme de fichiers XML. Vous pouvez utiliser cette fonction pour déplacer des calendriers d’un système d’évaluation vers un système de production.

>[!NOTE]
>
>Cette fonctionnalité exporte et importe tous les calendriers professionnels définis, y compris le calendrier professionnel par défaut fourni par AEM forms. Un calendrier professionnel importé portant le même nom qu’un calendrier existant remplace le calendrier existant.

### Exportation de calendriers professionnels {#export-business-calendars}

1. Dans Administration Console, cliquez sur Services > Processus des formulaires > Calendriers professionnels.
1. Cliquez sur Exporter et enregistrez le fichier XML.

### Importation de calendriers professionnels {#import-business-calendars}

1. Dans Administration Console, cliquez sur Services > Processus des formulaires > Calendriers professionnels.
1. Cliquez sur Importer.
1. Sélectionnez le fichier XML contenant les calendriers professionnels exportés et cliquez sur Ouvrir.

## Suppression d’un calendrier professionnel {#delete-a-business-calendar}

Vous pouvez supprimer les calendriers professionnels dont votre entreprise n’a plus besoin. Si vous supprimez un calendrier professionnel qui est toujours mappé à des utilisateurs et à des groupes, le calendrier par défaut est utilisé.

1. Dans Administration Console, cliquez sur Services > Processus Forms > Calendriers professionnels.
1. Sélectionnez le calendrier.
1. Cliquez sur Supprimer.
