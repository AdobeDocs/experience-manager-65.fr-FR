---
title: Canal d’impression et canal web
seo-title: Canal d’impression et canal web
description: Importation de modèles de canaux d’impression et création et activation de modèles de canaux web
seo-description: Importation de modèles de canaux d’impression et création et activation de modèles de canaux web
uuid: 2361b1ee-c789-4a5a-9575-8b62b603da1e
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 96d2b1cc-3252-4cc7-8b06-a897cbef8599
docset: aem65
translation-type: tm+mt
source-git-commit: a326e508a781b3afaba8b5e371aa862a30536740

---


# Canal d’impression et canal web{#print-channel-and-web-channel}

Les communications interactives peuvent être fournies par deux canaux : impression et web. Le canal d’impression est utilisé pour créer des documents PDF et des communications papier, comme une lettre imprimée comme rappel pour le paiement de primes d’assurance, tandis que le canal web est utilisé pour fournir des expériences en ligne, comme un relevé de carte de crédit sur un site Web.

Les auteurs de communications interactives peuvent réutiliser des ressources telles que des fragments de document et des images pour créer des versions papier et Web d’Interactive Communication.

One of the prerequisites for [Creating an Interactive Communication](../../forms/using/create-interactive-communication.md) is to have the templates for print and/or web channel available on the server. Alors que les auteurs de modèles créent le modèle de canal web dans AEM, le modèle de canal d’impression XDP est créé dans Adobe Forms Designer et téléchargé sur le serveur.

## Canal d’impression {#printchannel}

Le canal d’impression d’une communication interactive utilise le modèle de formulaire XFA, XDP. Les XDP sont conçus dans Adobe Forms Designer. For more information on creating print channel templates, see [Layout Design](../../forms/using/layout-design-details.md). Pour utiliser un modèle de canal d’impression dans votre communication interactive, vous devez télécharger le modèle sur le serveur AEM Forms.

### Télécharger le modèle de canal d’impression Communication interactive {#upload-interactive-communication-print-channel-template}

Pour télécharger le modèle, vous devez être membre du groupe forms-user. Suivez les étapes ci-dessous pour télécharger le modèle de canal d’impression (XDP) vers AEM Forms :

1. Sélectionnez **[!UICONTROL Formulaires]** > **[!UICONTROL Formulaires et documents]**.

1. Appuyez sur **[!UICONTROL Créer]**>**[!UICONTROL Chargement de fichier]**.

   Naviguez et sélectionnez le modèle de canal d’impression approprié (XDP), puis appuyez sur **[!UICONTROL Ouvrir]**.

## Canal web {#web-channel}

Les auteurs de modèles et les administrateurs peuvent créer, modifier et activer des modèles web. Pour autoriser d’autres utilisateurs à créer des modèles web, vous devez leur accorder des droits. For more information, see [User, Group and Access Rights Administration](/help/sites-administering/user-group-ac-admin.md).

### Création de modèle de canal web {#authoring-web-channel-template}

Pour créer un modèle de canal web, vous devez d’abord créer un dossier modèle. Une fois que vous avez créé un modèle Web dans un dossier de modèles, vous devez activer le modèle pour permettre aux utilisateurs de formulaires de créer un canal Web d’une communication interactive basée sur le modèle.

Pour créer un modèle de canal Web, procédez comme suit :

1. Créez un dossier Modèle pour conserver vos modèles Web de communication interactive, si vous n’en avez pas déjà un. For more information, see Template Folders in [Page Templates - Editable](/help/sites-developing/page-templates-editable.md).

   1. Tap **[!UICONTROL Tools]** ![tools](assets/tools.png) > **[!UICONTROL Configuration Browser]**.
   1. In the Configuration Browser page, tap **[!UICONTROL Create]**.
   1. In the Create Configuration dialog, specify a title for the folder, check **[!UICONTROL Editable Templates]**, and tap **[!UICONTROL Create]**.

      Le dossier est créé et répertorié dans la page du navigateur de configuration.

1. Accédez au dossier de modèle approprié et créez un modèle web.

   1. Navigate to the appropriate template folder by selecting **[!UICONTROL Tools]** > **[!UICONTROL Templates]** > **`[Folder]`**.
   1. Appuyez sur **[!UICONTROL Créer]**.
   1. Select **[!UICONTROL Interactive Communication - Web Channel]** and tap **[!UICONTROL Next]**.
   1. Entrez un titre et une description de modèle, puis appuyez sur **[!UICONTROL Créer]**.

      Le modèle est créé et une boîte de dialogue s’affiche.

   1. Appuyez sur **[!UICONTROL Ouvrir]** pour ouvrir le modèle que vous avez créé dans l’éditeur de modèles.

      L’Éditeur de modèle s’affiche.

      ![webchannel eltemplate](assets/webchanneltemplate.png)

      Lors de la création ou de la modification d’un modèle, un auteur de modèles peut définir différents aspects. La création ou la modification d’un modèle est similaire à la création de pages. For more information, see Editing Templates - Template Authors in [Creating Page Templates](/help/sites-authoring/templates.md).

1. Pour permettre l’utilisation de ce modèle pour la création de communication interactive, activez le modèle.

   1. Tap **[!UICONTROL Tools]** ![tools](assets/tools.png) > **[!UICONTROL Templates]**.
   1. Navigate to the appropriate template, select it, and tap **[!UICONTROL Enable]** and in the alert message, tap **[!UICONTROL Enable]**.

      Le modèle est activé et son statut s’affiche comme Activé. Vous pouvez maintenant créer une communication interactive dans laquelle vous pouvez utiliser le modèle de canal web nouvellement créé.

### Canal d’impression en tant que base du canal web {#print-channel-as-master-for-web-channel}

Lors de la création d’une communication interactive, les auteurs peuvent sélectionner cette option pour créer le canal web en synchronisation avec le canal d’impression. L’utilisation du canal d’impression comme base pour le canal web garantit que le contenu, l’héritage et la liaison des données du canal web sont dérivés du canal d’impression et que les modifications apportées au canal d’impression peuvent être répercutées sur le canal web. Les auteurs de communication interactive sont toutefois autorisés à interrompre l’héritage pour des composants spécifiques dans le canal web, selon les besoins.

![Canal d&#39;impression en tant que canal](assets/create_ic_print_master_new.png) Web maître ![avec canal d&#39;impression en tant que canal maître](assets/create_ic_print_master_web_new.png)

