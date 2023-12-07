---
title: Application AEM Forms
description: L’application AEM Forms permet aux agents de terrain d’utiliser des formulaires adaptatifs sur leurs appareils mobiles.
contentOwner: sashanka
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: 171754a2-1ba5-42dc-b6d2-3d730807cc31
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '2410'
ht-degree: 42%

---

# Présentation de l’application AEM Forms {#aem-forms-app}

## Présentation {#overview}

L’application AEM Forms permet la synchronisation de formulaires adaptatifs, de formulaires mobiles et d’ensembles de formulaires sur des périphériques mobiles, en fonction de votre serveur. Vous pouvez définir des processus en tant que [Processus spécifiques à Forms on OSGi](/help/forms/using/aem-forms-workflow.md) ou Processus Forms on JEE. Par exemple, vous dirigez une société bancaire et utilisez AEM Forms pour gérer les applications et les communications client. Vos clients remplissent un formulaire et l’envoient pour vérification. Si vous activez le formulaire sur des périphériques mobiles, vos clients peuvent le remplir dans l’application AEM Forms. Vous pouvez également gérer le workflow de vérification en activant le formulaire de vérification sur les périphériques mobiles. Votre agent de terrain peut transporter un appareil mobile vers le client, vérifier les détails et envoyer le formulaire. L’application AEM Forms se synchronise avec le serveur AEM Forms et récupère les formulaires activés pour les périphériques mobiles. Si l’application est hors ligne, elle enregistre les données localement.

Le code source de l’application AEM Forms est accessible via la Distribution de logiciels. Le package du code source dans Distribution de logiciels est disponible sous : `adobe-aemfd-forms-app-src-pkg-<version>.zip`.

L’application AEM Forms est prise en charge sur les appareils iOS, Android, Windows. Vous pouvez installer l’application AEM Forms pour Android à partir de Google Play, pour iOS à partir d’App Store et pour Windows à partir de Windows Store.

    [ ![google_play](assets/google_play.png)](https://play.google.com/store/apps/details?id=com.adobe.aem.forms&amp;hl=fr)
    
    [ ![app_store](assets/app_store.png)](https://itunes.apple.com/fr/app/adobe-experience-manager-forms/id1129625976?ls=1&amp;mt=8)
    
    [ ![microsoft-badge-icon](assets/microsoft-badge-icon.png)](https://www.microsoft.com/fr-fr/store/p/adobe-experience-manager-forms/9nd12rlxtgtt)

Pour installer, personnaliser et distribuer l’application sur des appareils iOS, Android ou Windows, voir [Personnaliser, créer et distribuer l’application AEM Forms](#customize-build-distribute).

## Prérequis {#prerequisites}

L’application AEM Forms nécessite un serveur AEM Forms. Les utilisateurs peuvent générer les formulaires que vous créez dans le serveur AEM Forms, les remplir, les enregistrer sous forme de brouillons et les envoyer. L’application se connecte au serveur et récupère les formulaires activés. L’application AEM Forms se synchronise avec le serveur et dès que les formulaires sont chargés dans l’application, les utilisateurs peuvent travailler hors ligne. Si l’application est hors ligne, les données sont enregistrées sur l’appareil et les données sont synchronisées avec le serveur lorsque l’application est en ligne.

### Application AEM Forms avec des serveurs utilisant AEM Forms Workflow {#aem-forms-app-with-servers-using-aem-forms-workflow}

Si vous disposez d’un serveur AEM Forms Workflow, vous pouvez effectuer le rendu des formulaires en tant que tâches dans l’application AEM Forms. Par exemple, vous dirigez une société bancaire et un client remplit une demande d’utilisation de vos services. La demande est un formulaire adaptatif qui accepte les informations de vos clients et les stocke en tant qu’envoi pour révision. L’administrateur examine une demande et transfère une demande de vérification au programme de travail sur le terrain. La demande transférée active un formulaire de vérification dans l’application de l’agent de terrain en tant que tâche. Votre agent de terrain apporte l’appareil mobile auprès de votre client et vérifie les détails.

### Application AEM Forms avec serveurs utilisant un workflow basé sur Forms sur OSGi {#aem-forms-app-with-servers-using-forms-centric-workflow-on-osgi}

Si vous disposez d’un serveur AEM Forms, vous pouvez effectuer le rendu des formulaires adaptatifs comme application de boîte de réception AEM et des tâches dans l’application AEM Forms. Par exemple, vous dirigez une société bancaire et un client remplit une demande d’utilisation de vos services. La demande est associée à un formulaire adaptatif qui accepte les informations de vos clients et les stocke en tant qu’envoi pour révision. L’administrateur examine la tâche et valide la demande de vérification auprès du programme de travail sur le terrain. Votre agent de terrain apporte l’appareil mobile auprès de votre client et vérifie les détails.

### Formulaires autonomes ou application AEM Forms avec des serveurs sans processus AEM Forms {#standalone-forms-or-aem-forms-app-with-servers-without-aem-forms-workflow}

Un serveur AEM Forms n’utilisant pas AEM Forms Workflow est AEM Forms sur OSGi ou un formulaire mobile autonome ou un formulaire adaptatif. L’application AEM Forms fonctionne avec votre implémentation d’AEM Forms on [OSGi](/help/sites-deploying/configuring-osgi.md). Les formulaires que vous activez et publiez pour l’application AEM Forms sont disponibles dans votre application.

Les formulaires sont téléchargés sur votre application et sont disponibles hors ligne. Par exemple, vous dirigez un établissement bancaire et un client remplit une demande sur votre site. La demande est un formulaire adaptatif qui accepte les informations de vos clients et les stocke pour révision. L’administrateur examine le formulaire et crée un formulaire de vérification dans AEM instance d’auteur. L’administrateur active la synchronisation du formulaire avec l’application AEM Forms et le publie. Si le formulaire de vérification est disponible dans l’application AEM Forms, votre agent de terrain peut utiliser un appareil mobile pour vérifier les détails de votre client. L’appareil mobile se synchronise avec le serveur et le formulaire de vérification est chargé dans l’application. Votre agent de terrain peut rendre visite à votre client, vérifier les détails, enregistrer les données en tant que brouillon ou envoyer le formulaire de vérification. Le formulaire est synchronisé avec le serveur chaque fois que l’application est en ligne.

Pour synchroniser votre formulaire dans l’application AEM Forms :

1. Dans l’instance d’auteur, sélectionnez un formulaire, puis cliquez sur **[!UICONTROL Afficher les propriétés]**. 

1. Dans la page des propriétés, cliquez sur **[!UICONTROL Avancé]**.
1. Sous Avancé, activez l’option : **[!UICONTROL Synchronisation avec l’application AEM Forms]** et sélectionnez **[!UICONTROL Enregistrer]**.

Une fois le formulaire publié, l’application se synchronise avec le serveur et récupère le formulaire. Pour synchroniser plusieurs formulaires, dans l’instance d’auteur, sélectionnez plusieurs formulaires dans le gestionnaire de formulaires, puis sélectionnez **[!UICONTROL Synchronisation avec l’application AEM Forms]**.

## Prise en charge des périphériques mobiles {#mobile-device-support}

Voir [Application AEM Forms (précédemment connue sous le nom de Mobile Workspace)](/help/forms/using/aem-forms-jee-supported-platforms.md#aem-forms-workspace-app)

## Fonctionnalités clés de l’application AEM Forms {#key-features-of-aem-forms-app}

### Application AEM Forms avec serveurs AEM Forms {#aem-forms-app-with-aem-forms-servers}

Vous pouvez synchroniser votre application avec le serveur AEM Forms et utiliser les formulaires sur votre périphérique mobile.

Avec le serveur AEM Forms Workflow, un formulaire peut être associé à un point de départ dans un processus Workbench et une application de boîte de réception AEM. Une demande de boîte de réception AEM peut être associée à un formulaire adaptatif. Un point de départ peut être associé à un formulaire adaptatif, à un HTML5 ou à un jeu de formulaires. Un point de départ peut être envoyé en tant que tâche ou la tâche peut être enregistrée en tant que brouillon. Pour plus d’informations sur les différences entre une demande depuis la boîte de réception AEM et un point de départ voir [Actions et fonctionnalités des processus AEM basés sur l’utilisation de Forms on OSGi et des processus AEM Forms JEE](capabilities-osgi-jee-workflows.md).

Avec le serveur AEM Forms sans processus AEM Forms, un formulaire activé pour synchronisation dans l’application est rendu dans l’application AEM Forms. Les Forms sont disponibles dans l’onglet Forms de l’application et peuvent être envoyées ou enregistrées en tant que brouillon. Les formulaires adaptatifs et les formulaires mobiles sont pris en charge dans l’application.

1. **Enregistrement d’une tâche ou d’un formulaire en tant que brouillon**

   L’option Enregistrer en tant que brouillon enregistre un instantané d’une tâche ou d’un formulaire avec les données remplies et les fichiers joints dans le formulaire associé. Les brouillons sont enregistrés sur le périphérique mobile et synchronisés avec le serveur AEM Forms pour une récupération ultérieure.

   Voir [Enregistrement d’une tâche ou d’un formulaire en tant que brouillon](/help/forms/using/save-as-draft.md).

1. **Enregistrer le formulaire en tant que modèle**

   Parfois, lorsque les utilisateurs remplissent un formulaire, les entrées de quelques champs restent les mêmes. Pour de telles instances, vous pouvez remplir les champs nécessitant des valeurs identiques dans chaque instance et enregistrer le formulaire ou le brouillon comme modèle. Désormais, chaque fois que vous créez une instance du modèle, les champs spécifiés sont déjà remplis avec les valeurs spécifiées dans le modèle. Cela vous permet de gagner du temps et vous évite les efforts nécessaires pour remplir le formulaire.

   Voir [Enregistrer des formulaires en tant que modèles](/help/forms/using/save-forms-and-start-points-as-templates.md).

### Utilisation de tâches et de formulaires {#working-with-tasks-and-forms}

Vous pouvez synchroniser votre application avec le serveur AEM Forms Workflow et travailler sur les tâches et les formulaires sur votre périphérique mobile.

Une tâche sur l’appareil mobile contient un formulaire adaptatif, un formulaire HTML5, ou un ensemble de formulaires et peut également contenir des pièces jointes et [l’URL du résumé](/help/forms/using/getting-task-variables-summary-url.md). Par défaut, les tâches qui vous sont assignées sont placées dans le dossier **[!UICONTROL Tâches]**. Lorsque vous travaillez sur une tâche, vous pouvez modifier la tâche et enregistrer un brouillon sur le serveur AEM Forms.

Un formulaire sur le périphérique mobile peut être un formulaire adaptatif ou un formulaire mobile. Les Forms activées pour la synchronisation dans l’application de formulaires sont disponibles dans le dossier Forms. Vous pouvez synchroniser les formulaires activés dans le serveur AEM Forms sans processus AEM Forms (AEM Forms sur OSGi).

Voir :

* [Ouverture d’une tâche](/help/forms/using/open-task.md)
* [Utilisation d’un formulaire](/help/forms/using/working-with-form.md)

### Travail hors ligne {#working-offline}

Vous pouvez travailler sur votre appareil mobile en mode hors ligne. Vous pouvez vous connecter à l’application même s’il n’y a aucune connectivité réseau et travailler sur tous les formulaires qui ont été synchronisées avec l’appareil lors de votre dernière connexion. Pour plus d’informations sur les modalités de synchronisation de vos formulaires, consultez la section [Synchronisation de l’application](/help/forms/using/sync-app.md). Si vous choisissez de synchroniser les pièces jointes associées à un formulaire, vous pouvez également ouvrir les pièces jointes en mode hors connexion. Vous pouvez modifier le formulaire, ajouter des annotations et envoyer ou enregistrer un formulaire en mode hors connexion. Le formulaire est synchronisé avec le serveur AEM Forms lors de votre prochaine connexion.

Pour plus d’informations, voir [Utilisation en mode hors ligne](/help/forms/using/work-offline-mode.md).

### Ajout d’annotations {#adding-annotations}

Vous pouvez ajouter les pièces jointes suivantes à un formulaire sur votre périphérique mobile.

* **Notes :** vous pouvez employer la fonction Notes pour ajouter une annotation à main levée ou une note textuelle dans votre formulaire. Pour plus d’informations, consultez la section [Ajout d’une note](/help/forms/using/add-attachments.md#adding-a-note).

* **Image :** l’application AEM Forms a une fonction qui emploie la fonctionnalité de caméra ou la galerie de votre appareil mobile. En utilisant la pièce jointe de photo, vous pouvez ajouter une photo avec le formulaire associé. Pour plus d’informations, consultez la section [Ajout d’une photographie](/help/forms/using/add-attachments.md#adding-a-photograph).

### Enregistrement automatique {#autosave}

Lorsqu’un utilisateur saisit des données dans l’application AEM Forms, la fonction d’enregistrement automatique les enregistre à intervalles réguliers. La fonction d’enregistrement automatique de l’application AEM Forms vous permet d’éviter toute perte de données si l’application se ferme en raison de conditions telles qu’une batterie faible.

Voir [Utilisation de l’enregistrement automatique dans l’application AEM Forms](/help/forms/using/autosave-data-app.md).

## Différences entre les fonctionnalités de la boîte de réception AEM et l’application AEM Forms {#differences-between-aem-inbox-and-aem-forms-app-features}

Deux des moyens principaux de lancer un workflow basé sur l’utilisation de Forms sont la [boîte de réception AEM](/help/forms/using/manage-applications-inbox.md) et l’application AEM Forms. Les fonctionnalités de la boîte de réception AEM et de l’application AEM Forms sont cependant différentes. AEM boîte de réception fonctionne uniquement avec [Workflows basés sur l’utilisation de Forms](/help/forms/using/aem-forms-workflow.md) pendant que l’application AEM Forms fonctionne avec les processus Forms et la gestion des processus. Pour plus d’informations sur les différences entre les fonctionnalités de l’application AEM Forms et de la boîte de réception AEM, voir [Actions et fonctionnalités des workflows AEM basés sur l’utilisation de Forms on OSGi et des workflows AEM Forms on JEE](capabilities-osgi-jee-workflows.md).

## Formulaires pris en charge {#supported-forms}

Types de formulaire pris en charge par l’application AEM Forms :

### Formulaire adaptatif {#adaptive-form}

Un formulaire adaptatif qui s’adapte dynamiquement aux entrées utilisateur est pris en charge dans l’application AEM Forms. Les formulaires adaptatifs chargés en différé sont également pris en charge.

### Formulaire mobile {#mobile-form}

Vous pouvez créer des formulaires pour les périphériques mobiles dans AEM Forms. Les formulaires mobiles sont rendus sous forme de formulaires par HTML sur les périphériques mobiles qui s’adaptent en fonction des périphériques d’affichage.

### Jeu de formulaires {#formset}

Avec les jeux de formulaires, plusieurs formulaires associés à un service ou à un processus peuvent être regroupés pour automatiser un processus d’entreprise et présentés aux utilisateurs finaux. Dans ce cas, les utilisateurs peuvent remplir l’ensemble comme un seul et même ensemble et il n’est pas nécessaire de générer, d’envoyer et de suivre des formulaires ou processus individuels.

>[!NOTE]
>
>Requiert le processus AEM Forms (AEM Forms on JEE).

## Fonctionnement de l’application AEM Forms {#how-aem-forms-app-works}

L’application AEM Forms fournit une solution mobile aux agents de terrain qui leur permet de travailler sur les formulaires qui leur sont assignés. L’application met en cache les données complètes à partir du serveur et apporte une expérience utilisateur supérieure en enregistrant le travail en local. Les données du disque sont envoyées au serveur via des mises à jour de synchronisation opportunes.

L’application AEM Forms est une application basée sur PhoneGap 5.0 dans laquelle le modèle Backbone est utilisé efficacement pour présenter des données stockées dans les modèles par le biais de vues. Toutes les opérations natives sont effectuées par le biais des modules externes PhoneGap.

## Personnaliser, créer et distribuer l’application AEM Forms {#customize-build-distribute}

>[!NOTE]
>
>Applicable uniquement si vous utilisez le code source de l’application AEM Forms pour créer l’application.

L’application AEM Forms est facile à personnaliser en fonction des besoins spécifiques d’une organisation. Le code source de l’application est fourni avec AEM Forms. Vous pouvez modifier le code source et concevoir votre propre solution mobile destinée au personnel de terrain. Vous pouvez également signer l’application avec votre propre clé d’entreprise.

### Personnalisation {#customize}

Vous pouvez personnaliser votre application pour :

**Identité graphique** : modifiez l’icône de l’application, le nom de l’application, les images de lancement et les pages dans l’application AEM Forms. Vous pouvez également modifier le texte pour localiser l’application pour une région spécifique. Pour plus d’informations sur l’identité graphique de l’application AEM Forms, référez-vous à [Personnalisation de l’identité graphique](/help/forms/using/branding-customization.md).

**Thème** : modifiez les styles tels que couleurs, polices et espacements dans l’interface utilisateur de l’application AEM Forms. Pour plus d’informations, consultez [Personnalisation du thème](/help/forms/using/theme-customization.md).

**Gestes** : modifiez les gestes, comme le glissement vers la droite ou vers la gauche, dans l’interface utilisateur de l’application AEM Forms. Pour plus d’informations, voir [Personnalisation des gestes](/help/forms/using/gesture-customization.md).

Pour plus d’informations sur la configuration d’un projet d’application AEM Forms à des fins de personnalisation, voir :

* [Configuration de l’environnement de l’application AEM Forms](/help/forms/using/setup-environment-mobile-workspace.md)
* [Configuration d’un projet Visual Studio et création d’une application Windows](/help/forms/using/setup-visual-studio-project-build-installer.md)
* [Configuration d’un projet Xcode et création d’une application iOS ](/help/forms/using/setup-xcode-project-build-installer.md)
* [Configuration d’un projet Eclipse et création d’une application Android](/help/forms/using/setup-eclipse-project-build-installer.md)

### Créer et distribuer {#build-and-distribute}

Le code source de l’application AEM Forms peut être extrait à partir de `adobe-lc-mobileworkspace-src.zip`, disponible en tant que package source de l’application AEM Forms dans Distribution de logiciels.

Pour obtenir le code source de l’application AEM Forms, procédez comme suit :

1. Ouvrez la [Distribution de logiciels](https://experience.adobe.com/downloads). Vous avez besoin d’un Adobe ID pour vous connecter à la Distribution de logiciels.
1. Sélectionner **[!UICONTROL Adobe Experience Manager]** disponibles dans le menu d’en-tête.
1. Dans la section **[!UICONTROL Filtres]** :
   1. Sélectionnez **[!UICONTROL Forms]** dans la liste déroulante **[!UICONTROL Solution]**.
   2. Sélectionnez la version et le type du package. Vous pouvez également utiliser l’option **[!UICONTROL Rechercher des téléchargements]** pour filtrer les résultats.
1. Sélectionnez le nom du package correspondant à votre système d’exploitation, puis sélectionnez **[!UICONTROL Accepter les termes du contrat de licence de l’utilisateur]**, puis sélectionnez **[!UICONTROL Télécharger]**.
1. Ouvrez [Package Manager](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=fr) et cliquez sur **[!UICONTROL Télécharger le package]** pour télécharger le package.
1. Sélectionnez le package et cliquez sur **[!UICONTROL Installer]**.

**Pour iOS**:

Pour plus d’informations sur la création d’une application iOS (.ipa), voir [Configuration du projet Xcode et création de l’application iOS](/help/forms/using/setup-xcode-project-build-installer.md).

Pour plus d’informations sur la manière de signer l’application AEM Forms avec votre profil d’approvisionnement, consultez [Paramètres de signature de code iOS, processus et dépannage](https://developer.apple.com/support/code-signing/).

**Pour Android** :

Pour plus d’informations sur la création d’une application Android (.apk), consultez la page [Configurer un projet Eclipse et créer une application Android](/help/forms/using/setup-eclipse-project-build-installer.md).

Pour plus d’informations sur la manière de signer l’application AEM Forms, consultez [Signature de vos applications](https://developer.android.com/tools/publishing/app-signing.html).

**Pour Windows** :

Pour plus d’informations sur la création d’une application Windows (.appx), consultez la page [Configurer un projet Visual Studio et créer une application Windows](/help/forms/using/setup-visual-studio-project-build-installer.md).

Pour plus d’informations sur les modalités de distribution de l’application via MDM, consultez la page [Distribution de l’application AEM Forms](/help/forms/using/distribute-mobile-workspace-app.md). La distribution de l’application via MDM s’applique uniquement à iOS et Android.

## Recommendations pour mettre à niveau Mobile Workspace vers l’application AEM Forms {#recommendations-to-upgrade-mobile-workspace-to-aem-forms-app}

Si vous effectuez une mise à niveau vers la dernière version de l’application AEM Forms, veillez à lire les points suivants :

* **Si vous avez installé une version antérieure de l’application à partir du Play Store sur Android,** vous pouvez mettre à niveau l’application directement du Play Store.

* **Si une version antérieure de l’application est créée et installée à l’aide du code source (applicable pour iOS et Android)** :

  Avant d’installer la nouvelle application, synchronisez toutes vos données avec le serveur AEM Forms. Une fois les données synchronisées, désinstallez la version antérieure de l’application et installez la nouvelle application.
