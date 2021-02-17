---
title: Configuration des calendriers professionnels
seo-title: Configuration des calendriers professionnels
description: Les calendriers professionnels définissent les jours ouvrables et non ouvrables pour votre entreprise. Découvrez comment configurer les calendriers des jours ouvrables.
seo-description: Les calendriers professionnels définissent les jours ouvrables et non ouvrables pour votre entreprise. Découvrez comment configurer les calendriers des jours ouvrables.
uuid: 0ba610b8-72a8-480c-8783-70d98cbe890a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7a85e13d-4800-47c4-812a-5c6e2355298a
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d
workflow-type: tm+mt
source-wordcount: '1928'
ht-degree: 93%

---


# Configuration des calendriers professionnels {#configuring-business-calendars}

*Les calendriers professionnels* définissent les jours ouvrés et non ouvrés de votre entreprise (par exemple, jours fériés, week-ends et jours de fermeture de la société). Lorsque vous utilisez des calendriers professionnels, AEM Forms ignore les jours non ouvrés lors des calculs de dates. Dans Workbench, vous pouvez indiquer si vous souhaitez utiliser des calendriers professionnels pour les événements liés à l’utilisateur (rappels, échéances et transmissions de tâches, par exemple) ou pour les actions non liées aux utilisateurs (événements de temporisation et service d’attente, par exemple).

Par exemple, un rappel de tâche est configuré pour se produire trois jours ouvrés après l’attribution de la tâche à l’utilisateur. La tâche est attribuée le jeudi. Toutefois, les trois jours qui suivent ne sont pas ouvrés puisque le vendredi est un jour de fête nationale et que les deux jours suivants sont des jours de week-end. Le rappel est donc envoyé le mercredi de la semaine suivante.

>[!NOTE]
>
>Lors du calcul des dates et heures à l’aide des calendriers professionnels, AEM Forms utilise la date et l’heure de la zone géographique dans laquelle se trouve le serveur et n’effectue aucune modification en fonction des fuseaux horaires. Par exemple, si un rappel de tâche est planifié pour 10 h 00 sur un serveur situé à Londres et si le destinataire du rappel se trouve à New York, celui-ci reçoit le rappel à 5 h 00, heure locale.

## Utilisation du calendrier professionnel par défaut {#using-the-default-business-calendar}

AEM Forms fournit un calendrier professionnel par défaut (*le calendrier intégré*) qui désigne les samedis et dimanches en tant que jours non ouvrés. Si les jours non ouvrés sont identiques pour l’ensemble des utilisateurs de votre organisation, vous pouvez mettre le calendrier professionnel par défaut à jour pour l’adapter à vos besoins. Si seul le calendrier professionnel par défaut est utilisé, il est inutile d’activer les calendriers professionnels dans User Management et de définir des associations. Lorsqu’aucun autre calendrier professionnel n’est défini, AEM Forms utilise le calendrier professionnel par défaut.

## Configuration de plusieurs calendriers professionnels  {#setting-up-multiple-business-calendars}

Si certains utilisateurs de votre entreprise ont des jours non ouvrés différents, vous pouvez créer plusieurs calendriers professionnels et configurer des associations permettant de définir l’exécution du calendrier professionnel d’un utilisateur.

### Définition de plusieurs calendriers professionnels  {#define-multiple-business-calendars}

1. Choisissez la méthode appropriée d’association du calendrier professionnel à un utilisateur, parmi les deux suivantes :

   **Appartenance à un groupe :** vous pouvez affecter un calendrier professionnel à un utilisateur en fonction de son appartenance à un groupe. Dans ce cas, chaque utilisateur du groupe utilise le même calendrier professionnel. 

   Si un utilisateur est membre de deux groupes et si ces groupes sont associés à deux calendriers professionnels différents, AEM Forms utilise le premier calendrier qui s’affiche dans les résultats de recherche. Vous devez alors envisager d’utiliser des clés de calendriers professionnels pour associer les utilisateurs aux calendriers professionnels.

   **Clés de calendrier professionnel :** vous pouvez affecter un calendrier professionnel à un utilisateur en fonction d’une clé de calendrier professionnel, paramètre défini dans User Management. Associez ensuite la clé de calendrier professionnel à un calendrier professionnel dans le processus des formulaires. 

    Les clés de calendrier professionnel sont attribuées à des utilisateurs en fonction du domaine utilisé, tel que le domaine d’entreprise, local ou hybride Pour plus d’informations sur la configuration de domaines, voir [Ajout de domaines](/help/forms/using/admin-help/adding-domains.md#adding-domains). 

    Si vous utilisez un domaine local ou hybride, les informations relatives aux utilisateurs ne sont stockées que dans la base de données User Management. Pour définir la clé de calendrier professionnel pour ces utilisateurs, entrez une chaîne dans le champ Clé du calendrier professionnel lors de la création ou de la modification de l’utilisateur dans User Management (voir [Ajout et configuration d’utilisateurs](/help/forms/using/admin-help/adding-configuring-users.md#adding-and-configuring-users)). Associez ensuite les clés de calendrier professionnel (les chaînes) aux calendriers professionnels dans le processus des formulaires (voir [Association d’utilisateurs ou de groupes à un calendrier professionnel](configuring-business-calendars.md#mapping-users-and-groups-to-a-business-calendar)). 

    Si vous utilisez un domaine d’entreprise, les informations relatives aux utilisateurs résident dans un système de stockage tiers, comme un annuaire LDAP, que User Management synchronise avec la base de données User Management. Ceci vous permet d’associer une clé de calendrier professionnel à un champ de l’annuaire LDAP. Par exemple, si chaque utilisateur enregistré dans votre annuaire dispose d’un champ « pays » et si vous souhaitez affecter des calendriers professionnels en fonction du pays dans lequel l’utilisateur se trouve, indiquez le nom du champ « pays » dans le champ Clé du calendrier professionnel lors du paramétrage de l’utilisateur dans l’annuaire (voir [Configuration des annuaires](/help/forms/using/admin-help/configuring-directories.md#configuring-directories)). Vous pouvez ensuite associer les clés de calendrier professionnel (valeurs définies pour le champ « pays » dans l’annuaire LDAP) aux calendriers professionnels dans le processus des formulaires (voir [Association d’utilisateurs ou de groupes à un calendrier professionnel](configuring-business-calendars.md#mapping-users-and-groups-to-a-business-calendar)).

1. Dans le processus des formulaires, définissez un calendrier pour chaque ensemble d’utilisateurs disposant des mêmes jours non ouvrés (voir [Création ou mise à jour d’un calendrier professionnel](configuring-business-calendars.md#create-or-update-a-business-calendar)).
1. Dans le processus des formulaires, associez les clés de calendrier professionnel ou les appartenances aux groupes pour chaque calendrier (voir [Association d’utilisateurs ou de groupes à un calendrier professionnel](configuring-business-calendars.md#mapping-users-and-groups-to-a-business-calendar)).
1. Dans Workbench, la décision d’utiliser des calendriers professionnels pour les rappels, les échéances et les transmissions appartient au développeur de processus (Voir l’[Aide de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)).

   Si le développeur de processus choisit d’utiliser des calendriers professionnels, AEM Forms sélectionne le calendrier professionnel approprié de façon dynamique en fonction du paramétrage de Gestion des utilisateurs et des associations de calendriers professionnels définies dans Administration Console ; en l’absence d’associations, le calendrier par défaut est utilisé.

   S’il choisit de ne pas utiliser de calendriers professionnels, le calcul de date de l’événement ne prend pas en compte les jours non ouvrés. Par exemple, une échéance de tâche est configurée pour se produire trois jours après l’attribution de la tâche à l’utilisateur. La tâche est attribuée le jeudi. L’échéance de la tâche se produit le dimanche, même s’il s’agit d’un jour de week-end.

## Création ou mise à jour d’un calendrier professionnel  {#create-or-update-a-business-calendar}

Si votre organisation comprend différents groupes d’utilisateurs pour lesquels les jours non ouvrés diffèrent, vous pouvez définir plusieurs calendriers professionnels. Vous pouvez également apporter des modifications aux calendriers existants, y compris au calendrier intégré par défaut fourni avec AEM Forms.

>[!NOTE]
>
>si vous ne créez pas de nouveau calendrier professionnel, le calendrier par défaut est utilisé.

1. Dans Administration Console, cliquez sur Services > Processus des formulaires > Calendriers professionnels.
1. Pour ajouter un nouveau calendrier professionnel, cliquez sur ![bus_cal_plus](assets/bus_cal_plus.png). Le texte *Nouveau calendrier* s’affiche dans la liste déroulante. Sélectionnez le texte et saisissez un autre nom pour votre calendrier.

   Pour modifier un calendrier professionnel existant, sélectionnez-le dans la liste déroulante.

1. Sous Jours non ouvrés par défaut, sélectionnez les jours non ouvrés par défaut de votre choix dans la semaine (week-ends, par exemple).
1. [] FacultatifSélectionnez Utiliser les heures de bureau et spécifiez les heures de début et de fin pour les jours ouvrés.

   Si vous sélectionnez cette option, un événement qui se produit avant la plage horaire définie est déplacé au début de la plage horaire et un événement qui se produit après est déplacé à l’heure de début du prochain jour ouvré.

   Par exemple, supposons qu’un utilisateur soit affecté à une tâche à 2 h 00 le mardi et que le rappel de cette tâche soit défini sur deux jours ouvrés. Sans les heures de bureau, le rappel se produit à 2 h 00 le jeudi. Si les heures de bureau sont définies de 8 h 00 à 17 h 00, le rappel est déplacé à 8 h 00 le jeudi. Sans les heures de bureau, si un rappel est créé pour 18 h 00 le mardi, il se produira après les heures de bureau le jeudi. Si les heures de bureau sont définies de 8 h 00 à 17 h 00, le rappel se produira à 8 h 00 le vendredi.

1. Dans le calendrier de gauche, cliquez deux fois sur un autre jour non ouvré, comme congés. Vous ne pouvez pas sélectionner de jours sur des périodes antérieures. Les jours non ouvrés sélectionnés apparaissent dans une liste sur la droite et la date s’affiche deux fois sur une seule ligne. Sélectionnez la date sur la gauche pour pouvoir taper le nom ou la description du jour non ouvré.

   Pour retirer un jour non ouvré de la liste, cliquez sur ![bus_cal_trash](assets/bus_cal_trash.png) en regard de ce jour.

1. [] FacultatifSi ce calendrier doit être le calendrier par défaut, sélectionnez Calendrier par défaut. Le calendrier par défaut est utilisé lorsqu’il n’existe aucune autre association de calendrier pour des événements utilisateur ou si aucun calendrier professionnel n’est spécifié pour l’événement de temporisation ou le service d’attente. Vous ne pouvez pas supprimer le calendrier par défaut.
1. La définition des jours non ouvrés terminée, sélectionnez Calendrier activé pour activer le calendrier, puis cliquez sur Enregistrer.

   Si vous mettez à jour un calendrier existant, la nouvelle version prend effet immédiatement et est utilisée pour tous les calculs de calendrier professionnel, y compris pour les tâches déjà en cours d’exécution.

   >[!NOTE]
   >
   >si vous n’activez pas le calendrier, le calendrier par défaut est utilisé.

## Association d’utilisateurs ou de groupes à un calendrier professionnel  {#mapping-users-and-groups-to-a-business-calendar}

Il existe deux méthodes pour associer un calendrier professionnel à un utilisateur. Vous pouvez affecter des calendriers professionnels à des utilisateurs en fonction d’une clé de calendrier professionnel ou d’un groupe d’annuaire auquel l’utilisateur appartient. Utilisez l’onglet Association pour indiquer la méthode qu’AEM Forms doit utiliser et pour mapper les clés et les groupes de calendrier professionnel aux calendriers professionnels. Pour plus d’informations sur l’association de clés de calendrier professionnel à des utilisateurs, voir [Configuration de plusieurs calendriers professionnels](configuring-business-calendars.md#setting-up-multiple-business-calendars).

### Association de calendriers professionnels à des utilisateurs à partir de clés de calendrier professionnel  {#associate-business-calendars-with-users-based-on-business-calendar-keys}

1. Dans Administration Console, cliquez sur Services > Processus des formulaires > Calendriers professionnels, puis cliquez sur l’onglet Association.
1. IntheSystem Will Use liste, sélectionnez User Manager Business Calendar Key Resolution.
1. Sélectionnez Afficher la clé du calendrier professionnel du gestionnaire des utilisateurs. Une liste des clés de calendrier professionnel définies dans User Management s’affiche.

   Pour les domaines locaux et hybrides, la liste affiche les valeurs entrées dans le champ Clé du calendrier professionnel de User Management. Pour les domaines d’entreprise (LDAP), la liste affiche l’ensemble unique provenant du champ LDAP (par exemple, « pays ») configuré dans les paramètres de domaine LDAP.

   Si l’administrateur de User Management n’a pas défini de clé de calendrier professionnel, la liste est vide.

1. Pour chaque élément de la liste Clé du calendrier professionnel GU, sélectionnez un Calendrier.
1. Cliquez sur Enregistrer.

### Association de calendriers professionnels à des utilisateurs et des groupes à partir de groupes de services d’annuaires  {#associate-business-calendars-with-users-and-groups-based-on-directory-service-groups}

1. Dans Administration Console, cliquez sur Services > Processus des formulaires > Calendriers professionnels, puis cliquez sur l’onglet Association.
1. IntheSystem Utilisera la liste, sélectionnez Groupes définis par le serveur d&#39;annuaire.
1. Dans l’onglet Association, sélectionnez Afficher les groupes de services d’annuaire. Une liste des groupes définis dans User Management s’affiche (voir [Paramètres d’annuaire](/help/forms/using/admin-help/configuring-directories.md#directory-settings)).

   >[!NOTE]
   >
   >Dans Workbench, si vous avez configuré un service Utilisateur pour qu’il utilise des calendriers professionnels et si le service est attribué à un groupe, AEM Forms utilise les associations du groupe indiquées pour créer le calendrier du groupe. AEM Forms utilise toujours les associations des groupes pour créer le calendrier des groupes, même lorsque vous utilisez des clés de calendrier professionnel pour créer le calendrier des utilisateurs. Si aucune association de groupe n’est trouvée, le calendrier professionnel par défaut est utilisé.

1. Pour chaque élément de la liste Groupe de services d’annuaire, sélectionnez un Calendrier.
1. Cliquez sur Enregistrer.

## Exportation et importation de calendriers professionnels  {#exporting-and-importing-business-calendars}

AEM Forms permet d’exporter et d’importer vos calendriers professionnels sous forme de fichiers XML. Cette fonction vous permet de faire passer des calendriers d’un système intermédiaire vers un système de production.

>[!NOTE]
>
>Elle exporte et importe l’ensemble des calendriers professionnels définis, y compris le calendrier professionnel par défaut d’AEM Forms. Si un calendrier professionnel importé porte le même nom qu’un calendrier existant, il remplace le calendrier existant.

### Exportation de calendriers professionnels  {#export-business-calendars}

1. Dans Administration Console, cliquez sur Services > Processus des formulaires > Calendriers professionnels.
1. Cliquez sur Exporter et enregistrez le fichier XML.

### Importation de calendriers professionnels  {#import-business-calendars}

1. Dans Administration Console, cliquez sur Services > Processus des formulaires > Calendriers professionnels.
1. Cliquez sur Importer.
1. Sélectionnez le fichier XML qui contient les calendriers professionnels exportés et cliquez sur Ouvrir.

## Suppression d’un calendrier professionnel  {#delete-a-business-calendar}

Vous pouvez supprimer tous les calendriers professionnels devenus inutiles. Si vous supprimez un calendrier professionnel qui est associé à des utilisateurs et à des groupes, le calendrier par défaut est utilisé.

1. Dans Administration Console, cliquez sur Services > Processus des formulaires > Calendriers professionnels.
1. Sélectionnez le calendrier.
1. Cliquez sur Supprimer.

