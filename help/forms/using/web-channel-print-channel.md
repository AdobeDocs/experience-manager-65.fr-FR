---
title: Canal d’impression et canal web
description: Importation de modèles de canaux d’impression et création et activation de modèles de canaux web
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Interactive Communication
exl-id: cd7dbdac-dc76-4a1f-b850-0a9f47ae08de
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: ht
source-wordcount: '696'
ht-degree: 100%

---

# Canal d’impression et canal web{#print-channel-and-web-channel}

Les communications interactives peuvent être fournies par deux canaux : impression et web. Le canal d’impression est utilisé pour créer des documents PDF et des communications papier, comme une lettre imprimée comme rappel pour le paiement de primes d’assurance, tandis que le canal web est utilisé pour fournir des expériences en ligne, comme un relevé de carte de crédit sur un site web.

Les auteurs d’une communication interactive peuvent réutiliser des ressources telles que des fragments de document et des images pour créer des versions imprimées et web de communication interactive.

L’une des conditions préalables à la [Création d’une communication interactive](../../forms/using/create-interactive-communication.md) est de disposer de modèles d’impression et/ou d’un canal web disponible sur le serveur. Alors que les auteurs de modèles créent le modèle de canal web dans AEM, le modèle de canal d’impression XDP est créé dans Adobe Forms Designer et téléchargé sur le serveur.

## Canal d’impression {#printchannel}

Le canal d’impression d’une communication interactive utilise XDP, le modèle de formulaire XFA. Les XDP sont conçus dans Adobe Forms Designer. Pour plus d’informations sur la création de modèles de canaux d’impression, reportez-vous à [Conception de la mise en page](../../forms/using/layout-design-details.md). Pour utiliser un modèle de canal d’impression dans votre communication interactive, vous devez télécharger le modèle sur le serveur AEM Forms.

### Charger le modèle de canal d’impression Communication interactive {#upload-interactive-communication-print-channel-template}

Pour charger le modèle, vous devez être membre du groupe forms-user. Suivez les étapes ci-dessous pour charger le modèle de canal d’impression (XDP) vers AEM Forms :

1. Sélectionnez **[!UICONTROL Formulaires]** > **[!UICONTROL Formulaires et documents]**.

1. Sélectionnez **[!UICONTROL Créer]** > **[!UICONTROL Charger un fichier]**.

   Naviguez et sélectionnez le modèle de canal d’impression approprié (XDP). Sélectionnez ensuite **[!UICONTROL Ouvrir]**.

## Canal web {#web-channel}

Les créateurs et créatrices de modèles et les administrateurs et administratrices peuvent créer, modifier et activer des modèles web. Pour autoriser d’autres utilisateurs et utilisatrices à créer des modèles web, vous devez leur accorder des droits. Pour plus d’informations, voir [Administration des droits d’utilisateur, de groupe et d’accès](/help/sites-administering/user-group-ac-admin.md).

### Création de modèle de canal web {#authoring-web-channel-template}

Pour créer un modèle de canal web, vous devez d’abord créer un dossier modèle. Une fois que vous avez créé un modèle web dans un dossier de modèles, vous devez l’activer pour permettre aux utilisateurs de formulaires de créer le canal web d’une communication interactive en fonction du modèle.

Pour créer un modèle de canal web, effectuez les étapes suivantes : 

1. Créez un dossier Modèle pour conserver vos modèles web de communication interactive, si vous n’en avez pas déjà un. Pour plus d’informations, reportez-vous à Dossiers de modèles dans [Modèles de page modifiables](/help/sites-developing/page-templates-editable.md).

   1. Sélectionnez **[!UICONTROL Outils]** ![outils](assets/tools.png) > **[!UICONTROL Explorateur de configurations]**.
      * Pour plus d’informations, consultez la documentation relative à l’[Explorateur de configurations](/help/sites-administering/configurations.md).
   1. Sur la page de l’explorateur de configurations, sélectionnez **[!UICONTROL Créer]**.
   1. Dans la boîte de dialogue Créer une configuration, spécifiez un titre pour le dossier, cochez **[!UICONTROL Modèles modifiables]**, puis sélectionnez **[!UICONTROL Créer]**.

      Le dossier est créé et répertorié sur la page Navigateur de configuration.

1. Accédez au dossier de modèle approprié et créez un modèle web.

   1. Accédez au dossier du modèle approprié en sélectionnant **[!UICONTROL Outils]** > **[!UICONTROL Modèles]** > **`[Folder]`**.
   1. Sélectionnez **[!UICONTROL Créer]**.
   1. Sélectionnez **[!UICONTROL Communication interactive - Canal web]**, puis **[!UICONTROL Suivant]**.
   1. Entrez un titre et une description de modèle, puis sélectionnez **[!UICONTROL Créer]**.

      Le modèle est créé et une boîte de dialogue s’affiche.

   1. Sélectionnez **[!UICONTROL Ouvrir]** pour ouvrir le modèle que vous avez créé dans l’éditeur de modèles.

      L’Éditeur de modèles s’affiche.

      ![webchanneltemplate](assets/webchanneltemplate.png)

      Lors de la création ou de la modification d’un modèle, un auteur ou une autrice de modèles peut définir différents aspects. La création ou la modification d’un modèle est similaire à la création de pages. Pour plus d’informations, consultez la section Modification de modèles - Auteurs de modèles dans [Création de modèles de page](/help/sites-authoring/templates.md).

1. Pour permettre l’utilisation de ce modèle pour la création de communication interactive, activez le modèle.

   1. Sélectionnez **[!UICONTROL Outils]** ![outils](assets/tools.png) > **[!UICONTROL Modèles]**.
   1. Accédez au modèle approprié, sélectionnez-le, sélectionnez **[!UICONTROL Activer]** et dans le message d’alerte, sélectionnez **[!UICONTROL Activer]**.

      Le modèle est activé et son statut s’affiche comme Activé. Vous pouvez maintenant créer une communication interactive dans laquelle vous pouvez utiliser le modèle de canal web nouvellement créé.

### Canal d’impression en tant que base du canal web {#print-channel-as-master-for-web-channel}

Lors de la création d’une communication interactive, les auteurs et autrices peuvent sélectionner cette option pour créer le canal web en synchronisation avec le canal d’impression. L’utilisation du canal d’impression comme base pour le canal web garantit que le contenu, l’héritage et la liaison des données du canal web sont dérivés du canal d’impression et que les modifications apportées au canal d’impression peuvent être répercutées sur le canal web. Les auteurs et autrices de communication interactive sont toutefois autorisés à interrompre l’héritage pour des composants spécifiques dans le canal web, selon les besoins.

![Canal d’impression en tant que base](assets/create_ic_print_master_new.png) ![Canal web avec canal d’impression en tant que base](assets/create_ic_print_master_web_new.png)
