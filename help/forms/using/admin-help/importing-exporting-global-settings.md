---
title: Importation et exportation des paramètres globaux
seo-title: Importation et exportation des paramètres globaux
description: Vous pouvez importer et exporter des définitions de modèles de recherche et des options globales pour Workspace.
seo-description: Vous pouvez importer et exporter des définitions de modèles de recherche et des options globales pour Workspace.
uuid: 8f1f210d-e850-4b2c-bb5a-942fa8299791
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_workspace
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 72fe5749-2fa2-442f-b679-7889faeafcac
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '1281'
ht-degree: 72%

---


# Importation et exportation des paramètres globaux {#importing-and-exporting-global-settings}

Vous pouvez importer et exporter des définitions de modèles de recherche et des options globales pour Workspace.

>[!NOTE]
>
>Flex Workspace est obsolète pour la version d’AEM Forms.

Il vous est possible, par exemple, de passer d’un environnement de développement à un environnement de production en exportant les définitions de modèles de recherche et les paramètres globaux d’un environnement et en les important dans l’autre.

Lorsque vous avez exporté le fichier de paramètres globaux, vous pouvez modifier les paramètres dans un éditeur XML ou de texte. Toutefois, les seuls paramètres que vous pouvez envisager de modifier sont JChannelConnectionProperties, formViewOnly et specialRoutes. Pour plus d’informations, voir [Paramètres globaux de Workspace](importing-exporting-global-settings.md#workspace-global-settings).


>[!NOTE]
>
>si vous modifiez les propriétés relatives à un événement dans le fichier des options globales, vous devez redémarrer le serveur.

## Importation d’une définition de modèle de recherche {#import-a-search-template-definition}

1. Dans Administration Console, cliquez sur Services > Workspace > Administration globale.
1. Dans le champ Importer une définition de modèle de recherche, cliquez sur le bouton Choisir fichier, puis sélectionnez le modèle de recherche. Seules les définitions de modèles de recherche initialement exportées à partir d’une instance de Workspace peuvent être importées.
1. Cliquez sur Importer.

## Exportation d’une définition de modèle de recherche {#export-a-search-template-definition}

1. Dans la page Administration globale, sous Exporter la définition du modèle de recherche, cliquez sur Répertorier tout.
1. Dans la liste des modèles de recherche, sélectionnez le modèle à exporter.

   >[!NOTE]
   >
   >vous pouvez sélectionner plusieurs modèles, mais seul le dernier modèle sélectionné sera exporté.

1. Cliquez sur Exporter, puis enregistrez le fichier sur l’ordinateur.

## Importation des paramètres globaux {#import-global-settings}

1. Dans la page Administration globale, sous Importation des paramètres globaux, cliquez sur le bouton Choisir fichier et sélectionnez le fichier de paramètres globaux. Le fichier de paramètres globaux doit être au format XML.
1. Cliquez sur Importer.

## Exportation des paramètres globaux {#export-global-settings}

1. Sur la page Administration globale, sous Exporter les paramètres globaux, cliquez sur Exporter.
1. Enregistrez le fichier sur l’ordinateur.

## Paramètres globaux de Workspace {#workspace-global-settings}

Vous pouvez modifier le fichier de paramètres globaux; toutefois, les seuls paramètres que vous devriez modifier sont JChannelConnectionProperties, formViewOnly et specialRoutes.

>[!NOTE]
>
>Flex Workspace est obsolète pour la version d’AEM Forms.

Le fichier de paramètres globaux de Workspace inclut les paramètres suivants :

### Paramètres specialRoutes {#specialroutes-settings}

Les paramètres *specialRoutes* spécifient les propriétés des itinéraires spéciaux, approbation et refus, dans Workspace. Dans certaines situations, les boutons de ces itinéraires s’affichent sur les cartes de tâches dans Workspace. L’utilisateur peut alors les sélectionner sans ouvrir le formulaire. Vous pouvez modifier le paramètre specialRoutes dans le fichier de paramètres globaux pour ajouter des noms personnalisés à approuver et à refuser, ou pour créer des itinéraires supplémentaires.

**client_specialRoutes_routes_approval_style :** Nom du style situé dans le thème Workspace, qui identifie les icônes de bouton d’approbation. Le style doit inclure des valeurs pour une icône activée et une icône désactivée. Pour définir un style pour un bouton personnalisé, vous devez utiliser le modèle suivant :
` .buttonApprove {  icon: Embed('images/LC_DirectApprove_Sm_N.png');  disabledIcon: Embed('images/LC_DirectApprove_Sm_D.png');  paddingLeft: 5;  }` Le fichier CSS de Workspace est incorporé au fichier workspace-theme.swf, qui est situé dans le fichier adobe-workspace-client.ear > adobe-workspace-client.war. Pour modifier l’aspect de Workspace, vous devez recompiler le fichier workspace-theme.swf.

**client_specialRoutes_routes_deny_names :** Diverses chaînes qu’un utilisateur de Workbench peut utiliser pour être interprétées comme &quot;refusant&quot;. Les chaînes respectent la casse. Par exemple, la valeur par défaut est deny. Si l’utilisateur de Workbench emploie le terme Deny (refuser) dans un processus, ce terme ne sera pas reconnu. Le terme Deny doit être ajouté à ce paramètre pour que le bouton d’itinéraire soit personnalisé et que le style lui soit appliqué.

**client_specialRoutes_routes_deny_style :** Nom du style situé dans le fichier de thème Workspace, qui identifie les icônes du bouton de refus. Le style doit inclure des valeurs pour une icône activée et une icône désactivée. Pour définir un style pour un bouton personnalisé, vous devez utiliser le modèle suivant :
`  .buttonDeny {   icon: Embed('images/LC_DirectDeny_Sm_N.png');   disabledIcon: Embed('images/LC_DirectDeny_Sm_D.png');   paddingLeft: 0;   }` **client_specialRoutes_routes_approval_names :** Diverses chaînes qu’un utilisateur de Workbench peut utiliser pour être interprétée comme &quot;Approuver&quot;. Les chaînes respectent la casse. Par exemple, la valeur par défaut est approve (approuver). Si l’utilisateur de Workbench emploie le terme Approve dans un processus, ce terme ne sera pas reconnu. Le terme Approve doit être ajouté à ce paramètre pour que le bouton d’itinéraire soit personnalisé et que le style lui soit appliqué.

**client_specialRoutes_names :** Clés utilisées pour localiser la valeur de chaîne personnalisée à partir des fichiers de ressources. Chaque entrée de ce paramètre doit inclure les valeurs de noms et de style.

### Paramètres JGroup {#jgroup-settings}

Ces paramètres s’affichent uniquement si vous avez effectué une mise à niveau depuis Adobe LiveCycle ES2.5 ou une version antérieure.

**server_remoteevents_ClientTimeoutMilliseconds :** durée maximale pendant laquelle JGroup attend les messages de événement. Ce paramètre doit rester inchangé.

**server_remoteevents_ServerTimeoutMilliseconds :** Délai d’attente pour la réception de messages JGroup sur le serveur. Cette option définit le délai pour l’envoi de messages du serveur au client.

**server_remoteevents_JChannelConnectionProperties:** Propriétés de connexion de JGroup utilisées pour communiquer entre le serveur (sur lequel un événement de service est traité par le service RemoteEvent) et toutes les instances de Workspace.

Il est possible que vous deviez modifier les valeurs UDP de l’adresse IP à diffusion multiple (mcast_addr), du port IP à diffusion multiple (mcast_port) et de TTL pour les paquets à diffusion multiple (ip_ttl). Par défaut, les valeurs de l’adresse et du port IP à diffusion multiple sont générées de manière aléatoire et, en règle générale, il est inutile de modifier ces valeurs. Toutefois, si votre société utilise des stratégies de réseau relatives à des plages de diffusion multiple pour les adresses IP à diffusion multiple, il peut s’avérer nécessaire de modifier ces valeurs.

>[!NOTE]
>
>TTL doit être supérieur au nombre de commutateurs réseau existant entre les serveurs et la grappe ; toutefois, si vous définissez une valeur trop élevée, des paquets à diffusion multiple risquent de se déplacer dans des sous-réseaux, où ils seront ignorés.

Les autres propriétés de ce paramètre doivent rester inchangées.

**server_remoteevents_JGroupName :** Nom du JGroup utilisé pour la communication par événement à distance. Pour éviter les conflits dans les grappes, cette valeur est générée de manière aléatoire. Cette valeur doit rester inchangée.

Pour plus d’informations sur JGroups et Workspace, consultez l’article [JGroups and AEM forms Workspace - Explained](https://blogs.adobe.com/livecycle/2011/03/jgroups-and-livecycle-workspace-explained.html) (en anglais).

### Paramètres formView {#formview-settings}

**client_formView_openFormInFullScreen :** Pour afficher tous les formulaires dans Workspace en mode plein écran, définissez cette option sur true. Par défaut, cette option est définie sur false, et les formulaires ne s’affichent pas en mode plein écran. Veuillez noter que le service Utilisateur comporte une option permettant d’ouvrir en mode plein écran le document associé à une tâche. Cela vous permet de contrôler l’affichage sur une base de processus individuel.

**client_routes_formViewOnly :** Lorsqu’elle est définie sur True, les itinéraires ne s’affichent pas dans la vue de carte ou la vue de liste dans Workspace. La valeur par défaut est False, ce qui signifie que les itinéraires sont affichés sous forme de carte ou de liste.

### Autres paramètres {#other-settings}

**client_mimeTypes_openOutsideBrowser :** Type MIME des documents qui s’ouvriront en dehors de l’instance du navigateur de Workspace. Si les processus de votre entreprise nécessitent un type MIME supplémentaire, indiquez-le ici. Les valeurs par défaut sont :

* `application/msword`
* `application/msexcel`
* `application/ms-powerpoint`

**client_customUI_caching:** met en cache une interface utilisateur de tâche personnalisée.

**server_debugLevel :** Ne modifiez pas ce paramètre.

**client_pollingInterval :** Définit l’intervalle d’interrogation (en secondes) utilisé sur l’espace de travail Flex (obsolète pour AEM forms on JEE) pour détecter les tâches nouvelles et modifiées. La valeur par défaut est de 3 secondes. Elle ne fonctionne pas pour l’espace de travail AEM Forms

**client_systemContext_name :** Indiquez un nom personnalisé (par exemple Citoyen) à afficher dans le champ Ajouté par (dans l’onglet Pièces jointes) pour les pièces jointes d’une tâche dans AEM Forms Workspace.

Pour définir le nom personnalisé :

`<client_systemContext_name>[custom name to display]</client_systemContext_name>`

>[!NOTE]
>
>pour l’application de démonstration, la valeur par défaut du nom d’affichage est **Citoyen**. Pour une application personnalisée que vous avez créée, le nom d’affichage par défaut est **Compte de contexte du système**.
>
>**client_idleTimeout :** Lorsqu’un utilisateur reste inactif pendant une durée spécifique, la session AEM Forms Workspace expire. Pour activer la fonction, ajoutez une entrée aux Paramètres généraux &lt;client_idleTimeout>*IDLE_TIMEOUT_IN_SECONDS*&lt;/client_idleTimeout>. Vous pouvez spécifier la valeur 0 pour désactiver le délai d’inactivité. La durée est spécifiée en secondes.
