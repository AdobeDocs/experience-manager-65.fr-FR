---
title: Canal d’impression et canal web
seo-title: Print channel and web channel
description: Importation de modèles de canal d’impression et création et activation de modèles de canal web
seo-description: Importing print channel templates and creating and enabling web channel templates
uuid: 2361b1ee-c789-4a5a-9575-8b62b603da1e
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 96d2b1cc-3252-4cc7-8b06-a897cbef8599
docset: aem65
feature: Interactive Communication
exl-id: cd7dbdac-dc76-4a1f-b850-0a9f47ae08de
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 44%

---

# Canal d’impression et canal web{#print-channel-and-web-channel}

Les communications interactives peuvent être diffusées par deux canaux : impression et web. Le canal d’impression est utilisé pour créer des PDF et des communications papier, telles qu’une lettre imprimée comme rappel pour le paiement des primes d’assurance, tandis que le canal web est utilisé pour offrir des expériences en ligne, telles qu’un relevé de carte de crédit sur un site web.

Les auteurs d’une communication interactive peuvent réutiliser des ressources telles que des fragments de document et des images pour créer des versions imprimées et web de communication interactive.

L’une des conditions préalables à la [Création d’une communication interactive](../../forms/using/create-interactive-communication.md) est de disposer de modèles d’impression et/ou d’un canal web disponible sur le serveur. Alors que les auteurs de modèles créent le modèle de canal web dans AEM, le modèle de canal d’impression XDP est créé dans Adobe Forms Designer et téléchargé sur le serveur.

## Canal d’impression {#printchannel}

Le canal d’impression d’une communication interactive utilise XDP, le modèle de formulaire XFA. Les XDP sont conçus dans Adobe Forms Designer. Pour plus d’informations sur la création de modèles de canaux d’impression, reportez-vous à [Conception de la mise en page](../../forms/using/layout-design-details.md). Pour utiliser un modèle de canal d’impression dans votre communication interactive, vous devez télécharger le modèle sur le serveur AEM Forms.

### Télécharger le modèle de canal d’impression Communication interactive {#upload-interactive-communication-print-channel-template}

Pour charger le modèle, vous devez être membre du groupe forms-user. Suivez les étapes ci-dessous pour télécharger le modèle de canal d’impression (XDP) vers AEM Forms :

1. Sélectionnez **[!UICONTROL Formulaires]** > **[!UICONTROL Formulaires et documents]**.

1. Sélectionner **[!UICONTROL Créer]** > **[!UICONTROL Téléchargement du fichier]**.

   Naviguez et sélectionnez le modèle de canal d’impression approprié (XDP), puis sélectionnez **[!UICONTROL Ouvrir]**.

## Canal web {#web-channel}

Les auteurs de modèles et les administrateurs peuvent créer, modifier et activer des modèles web. Pour permettre à d’autres utilisateurs de créer des modèles web, vous devez leur accorder des droits. Pour plus d’informations, voir [Administration des droits d’utilisateur, de groupe et d’accès](/help/sites-administering/user-group-ac-admin.md).

### Création d’un modèle de canal web {#authoring-web-channel-template}

Pour créer un modèle de canal web, vous devez d’abord créer un dossier Modèle . Une fois que vous avez créé un modèle web dans un dossier de modèles, vous devez l’activer pour permettre aux utilisateurs de formulaires de créer le canal web d’une communication interactive en fonction du modèle.

Pour créer un modèle de canal web, effectuez les étapes suivantes : 

1. Créez un dossier Modèle pour conserver vos modèles web de communication interactive, si vous n’en avez pas déjà un. Pour plus d’informations, reportez-vous à Dossiers de modèles dans [Modèles de page modifiables](/help/sites-developing/page-templates-editable.md).

   1. Sélectionner **[!UICONTROL Outils]** ![outils](assets/tools.png) > **[!UICONTROL Explorateur de configuration]**.
      * Pour plus d’informations, consultez la documentation relative au [Navigateur de configuration](/help/sites-administering/configurations.md).
   1. Dans la page du navigateur de configuration, sélectionnez **[!UICONTROL Créer]**.
   1. Dans la boîte de dialogue Créer une configuration, indiquez un titre pour le dossier, puis cochez la case **[!UICONTROL Modèles modifiables]**, puis sélectionnez **[!UICONTROL Créer]**.

      Le dossier est créé et répertorié sur la page Navigateur de configuration.

1. Accédez au dossier de modèle approprié et créez un modèle web.

   1. Accédez au dossier du modèle approprié en sélectionnant **[!UICONTROL Outils]** > **[!UICONTROL Modèles]** > **`[Folder]`**.
   1. Sélectionnez **[!UICONTROL Créer]**.
   1. Sélectionner **[!UICONTROL Communication interactive - Canal web]** et sélectionnez **[!UICONTROL Suivant]**.
   1. Saisissez un titre et une description de modèle, puis sélectionnez **[!UICONTROL Créer]**.

      Le modèle est créé et une boîte de dialogue s’affiche.

   1. Sélectionner **[!UICONTROL Ouvrir]** pour ouvrir le modèle que vous avez créé dans l’éditeur de modèles.

      L’éditeur de modèles s’affiche.

      ![webchanneltemplate](assets/webchanneltemplate.png)

      Lors de la création ou de la modification d’un modèle, un créateur de modèles peut définir différents aspects. La création ou la modification d’un modèle est similaire à la création de pages. Pour plus d’informations, consultez la section Modification de modèles - Auteurs de modèles dans [Création de modèles de page](/help/sites-authoring/templates.md).

1. Pour permettre l’utilisation de ce modèle pour la création de communication interactive, activez le modèle.

   1. Sélectionner **[!UICONTROL Outils]** ![outils](assets/tools.png) > **[!UICONTROL Modèles]**.
   1. Accédez au modèle approprié, sélectionnez-le, puis sélectionnez **[!UICONTROL Activer]** et dans le message d’alerte, sélectionnez **[!UICONTROL Activer]**.

      Le modèle est activé et son état s’affiche comme Activé. Vous pouvez maintenant créer une communication interactive dans laquelle vous pouvez utiliser le modèle de canal web nouvellement créé.

### Canal d’impression comme gabarit pour canal web {#print-channel-as-master-for-web-channel}

Lors de la création d’une communication interactive, les auteurs peuvent sélectionner cette option pour créer le canal web en synchronisation avec le canal d’impression. L’utilisation du canal d’impression comme gabarit pour le canal web garantit que le contenu, l’héritage et la liaison des données du canal web sont dérivés du canal d’impression et que les modifications apportées au canal d’impression peuvent être répercutées dans le canal web. Les auteurs de communication interactive sont toutefois autorisés à interrompre l’héritage pour des composants spécifiques du canal web, selon les besoins.

![Canal d’impression en tant que base](assets/create_ic_print_master_new.png) ![Canal web avec canal d’impression en tant que base](assets/create_ic_print_master_web_new.png)
