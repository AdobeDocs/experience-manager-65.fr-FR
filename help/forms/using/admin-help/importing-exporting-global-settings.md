---
title: Importation et exportation des paramètres globaux
seo-title: Importing and exporting global settings
description: Vous pouvez importer et exporter des définitions de modèles de recherche et des paramètres globaux pour Workspace.
seo-description: You can import and export search template definitions and global settings for Workspace.
uuid: 8f1f210d-e850-4b2c-bb5a-942fa8299791
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_workspace
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 72fe5749-2fa2-442f-b679-7889faeafcac
exl-id: cdb7ff54-7891-45b1-a921-10b01ef5188d
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1240'
ht-degree: 37%

---

# Importation et exportation des paramètres globaux {#importing-and-exporting-global-settings}

Vous pouvez importer et exporter des définitions de modèles de recherche et des paramètres globaux pour Workspace.

>[!NOTE]
>
>L’espace de travail Flex est obsolète pour la version d’AEM Forms.

Par exemple, vous pouvez passer d’un environnement de développement à un environnement de production en exportant les définitions de modèles de recherche et les paramètres globaux d’un environnement et en les important dans l’autre.

Après avoir exporté le fichier de paramètres globaux, vous pouvez modifier les paramètres dans un éditeur XML ou de texte. Toutefois, les seuls paramètres que vous pouvez modifier sont JChannelConnectionProperties, formViewOnly et specialRoutes . Pour plus d’informations, voir [Paramètres globaux de Workspace](importing-exporting-global-settings.md#workspace-global-settings).


>[!NOTE]
>
>Si vous modifiez les propriétés d’événement dans le fichier de paramètres globaux, vous devez redémarrer le serveur.

## Importation d’une définition de modèle de recherche {#import-a-search-template-definition}

1. Dans Administration Console, cliquez sur Services > Workspace > Administration globale.
1. Dans la zone Importer une définition de modèle de recherche, cliquez sur Choisir un fichier et sélectionnez le modèle de recherche. Vous ne pouvez importer que les définitions de modèle de recherche qui ont été exportées à l’origine à partir d’une instance de Workspace.
1. Cliquez sur Importer.

## Exporter une définition de modèle de recherche {#export-a-search-template-definition}

1. Sur la page Administration globale, sous Exporter la définition du modèle de recherche, cliquez sur Tout répertorier.
1. Dans la liste des modèles de recherche, sélectionnez le modèle à exporter.

   >[!NOTE]
   >
   >Vous pouvez sélectionner plusieurs modèles, mais seul le dernier modèle sélectionné est exporté.

1. Cliquez sur Exporter, puis enregistrez le fichier sur votre ordinateur.

## Importation des paramètres globaux {#import-global-settings}

1. Sur la page Administration globale, sous Importer les paramètres globaux, cliquez sur Choisir un fichier et sélectionnez le fichier de paramètres globaux. Le fichier de paramètres globaux doit être au format XML.
1. Cliquez sur Importer.

## Exportation des paramètres globaux {#export-global-settings}

1. Sur la page Administration globale, sous Exporter les paramètres globaux, cliquez sur Exporter.
1. Enregistrez le fichier sur votre ordinateur.

## Paramètres globaux de Workspace {#workspace-global-settings}

Vous pouvez modifier le fichier de paramètres globaux ; toutefois, les seuls paramètres que vous devriez modifier sont JChannelConnectionProperties, formViewOnly et specialRoutes.

>[!NOTE]
>
>L’espace de travail Flex est obsolète pour la version d’AEM Forms.

Le fichier de paramètres globaux de Workspace comprend les paramètres suivants :

### Paramètres specialRoutes {#specialroutes-settings}

La variable *specialRoutes* Les paramètres spécifient les propriétés des itinéraires spéciaux, approbation et refus, dans Workspace. Dans certains cas, les boutons de ces itinéraires apparaissent sur les cartes de tâches dans Workspace, et l’utilisateur peut les sélectionner sans ouvrir le formulaire. Vous pouvez modifier les paramètres specialRoutes dans le fichier de paramètres globaux pour ajouter des noms personnalisés à approuver et à refuser, ou pour créer des itinéraires supplémentaires.

**client_specialRoutes_routes_approve_style:** Nom du style qui se trouve dans le thème Workspace, qui identifie les icônes de bouton d’approbation. Le style doit inclure des valeurs pour une icône activée et une icône désactivée. Pour définir un style pour un bouton personnalisé, vous devez utiliser le modèle suivant :
` .buttonApprove {  icon: Embed('images/LC_DirectApprove_Sm_N.png');  disabledIcon: Embed('images/LC_DirectApprove_Sm_D.png');  paddingLeft: 5;  }` Le fichier CSS Workspace est incorporé dans le fichier workspace-theme.swf, qui se trouve dans le fichier adobe-workspace-client.ear > adobe-workspace-client.war . Pour modifier l’aspect de Workspace, vous devez recompiler le fichier workspace-theme.swf.

**client_specialRoutes_routes_deny_names :** diverses chaînes qu’un utilisateur de Workbench peut utiliser pour être interprétées comme « refuser ». Les chaînes respectent la casse. Par exemple, la valeur par défaut est deny. Si l’utilisateur de Workbench emploie le terme Deny (refuser) dans un processus, ce terme ne sera pas reconnu. Le terme Deny doit être ajouté à ce paramètre pour que le bouton d’itinéraire soit personnalisé et que le style lui soit appliqué.

**client_specialRoutes_routes_deny_style :** Nom du style qui se trouve dans le fichier de thème de Workspace, qui identifie les icônes du bouton d’opposition. Le style doit inclure des valeurs pour une icône activée et une icône désactivée. Pour définir un style pour un bouton personnalisé, vous devez utiliser le modèle suivant :
`  .buttonDeny {   icon: Embed('images/LC_DirectDeny_Sm_N.png');   disabledIcon: Embed('images/LC_DirectDeny_Sm_D.png');   paddingLeft: 0;   }` **client_specialRoutes_routes_approve_names :** Les différentes chaînes qu’un utilisateur de Workbench peut utiliser pour être interprétées comme &quot;Approbation&quot;. Les chaînes respectent la casse. Par exemple, la valeur par défaut est approve (approuver). Si l’utilisateur de Workbench emploie le terme Approve dans un processus, ce terme ne sera pas reconnu. Le terme Approve doit être ajouté à ce paramètre pour que le bouton d’itinéraire soit personnalisé et que le style lui soit appliqué.

**client_specialRoutes_names :** les clés utilisées pour localiser la valeur de chaîne personnalisée dans les fichiers ressource. Chaque entrée de ce paramètre doit inclure les valeurs des noms et du style.

### Paramètres JGroup {#jgroup-settings}

Ces paramètres s’affichent uniquement si vous avez effectué la mise à niveau à partir d’Adobe LiveCycle ES 2.5 ou d’une version antérieure.

**server_remoteevents_ClientTimeoutMilliseconds :** durée maximale pendant laquelle JGroup attend les messages d’événements. Ce paramètre doit rester inchangé.

**server_remoteevents_ServerTimeoutMilliseconds :** délai d’expiration pour la réception des messages JGroup sur le serveur. Cette option définit le délai pour l’envoi de messages du serveur au client.

**server_remoteevents_JChannelConnectionProperties :** propriétés de connexion de JGroup, utilisées à des fins de communication entre le serveur (sur lequel est traité un événement de service par le service RemoteEvent) et toutes les instances de Workspace.

Vous devrez peut-être modifier les valeurs UDP de l’adresse IP à diffusion multiple (mcast_addr), du port IP à diffusion multiple (mcast_port) et de la durée de vie pour les paquets à diffusion multiple (ip_ttl). Par défaut, les valeurs des adresses IP et des ports à diffusion multiple sont générées de manière aléatoire et, en règle générale, les valeurs n’ont pas besoin d’être modifiées. Toutefois, si votre entreprise applique des stratégies réseau concernant des plages de diffusion multiple spécifiques pour les adresses IP à diffusion multiple, vous devrez peut-être modifier les valeurs.

>[!NOTE]
>
>La durée de vie doit être supérieure au nombre de commutateurs réseau entre les serveurs de la grappe. Toutefois, si la valeur est définie sur une valeur trop élevée, des paquets à diffusion multiple peuvent se déplacer dans des sous-réseaux, où ils seront ignorés.

Les autres propriétés de ce paramètre ne doivent pas être modifiées.

**server_remoteevents_JGroupName :** nom JGroup utilisé pour la communication d’événements à distance. Cette valeur est générée de manière aléatoire afin d’éviter les conflits dans les grappes. Cette valeur ne doit pas être modifiée.

<!--

For additional information on JGroups and Workspace, see [JGroups and AEM forms Workspace - Explained](https://blogs.adobe.com/livecycle/2011/03/jgroups-and-livecycle-workspace-explained.html).

-->

### Paramètres formView {#formview-settings}

**client_formView_openFormInFullScreen :** pour afficher tous les formulaires de Workspace en mode plein écran, définissez cette option sur true. Par défaut, cette option est définie sur false, et les formulaires ne s’affichent pas en mode plein écran. Le service User contient une option pour ouvrir le document associé à une tâche en mode plein écran. Vous pouvez ainsi contrôler l’affichage par processus.

**client_routes_formViewOnly :** lorsqu’ils sont définis sur True, les itinéraires ne sont pas affichés dans la vue Carte ou Liste de Workspace. La valeur par défaut est False, ce qui signifie que les itinéraires sont affichés dans la vue Carte et dans la vue Liste.

### Autres paramètres {#other-settings}

**client_mimeTypes_openOutsideBrowser :** Type MIME des documents qui s’ouvre en dehors de l’instance du navigateur de Workspace. Si les processus de votre entreprise nécessitent un type MIME supplémentaire, indiquez-le ici. Les valeurs par défaut sont les suivantes :

* `application/msword`
* `application/msexcel`
* `application/ms-powerpoint`

**client_customUI_caching :** met en cache une interface utilisateur de tâche personnalisée.

**server_debugLevel :** ne modifiez pas ce paramètre.

**client_pollingInterval :** définit la fréquence des interrogations (en secondes) utilisée dans Flex Workspace (obsolète pour AEM Forms sur JEE) pour détecter les nouvelles tâches et les tâches modifiées. La valeur par défaut est de 3 secondes. Cela ne fonctionne pas pour AEM Forms Workspace.

**client_systemContext_name:** Spécifiez un nom personnalisé (par exemple, Citoyen) à afficher dans le champ Ajouté par (dans l’onglet Pièces jointes) pour les pièces jointes d’une tâche dans AEM Forms Workspace.

Pour définir le nom personnalisé :

`<client_systemContext_name>[custom name to display]</client_systemContext_name>`

>[!NOTE]
>
>Pour l’application de démonstration, le nom d’affichage par défaut est **Citoyen**. Pour une application personnalisée que vous créez, le nom d’affichage par défaut est **Compte de contexte du système**.
>
>**client_idleTimeout :** lorsqu’un utilisateur reste inactif pendant une durée spécifique, la session AEM Forms Workspace expire. Pour activer la fonction, ajoutez une entrée à Paramètres globaux &lt;client_idleTimeout>*IDLE_TIMEOUT_IN_SECONDS*&lt;/client_idleTimeout>. Vous pouvez définir la valeur 0 pour désactiver le délai d’inactivité. La durée est spécifiée en secondes.
