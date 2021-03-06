---
title: Application AEM Forms
seo-title: AEM Forms app
description: L’application AEM Forms permet aux agents de terrain d’utiliser les formulaires adaptatifs sur leurs appareils mobiles.
seo-description: AEM Forms app enables your field workers to use adaptive forms on their mobile devices.
uuid: fac976c8-b713-4492-b153-f567e7a11ceb
contentOwner: sashanka
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: e18aa345-034c-473b-b4c2-01678bb10616
exl-id: 171754a2-1ba5-42dc-b6d2-3d730807cc31
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '2452'
ht-degree: 100%

---

# Présentation de l’application AEM Forms {#aem-forms-app}

## Présentation {#overview}

L’application AEM Forms permet de synchroniser des formulaires adaptatifs, des formulaires mobiles et des jeux de formulaires sur les périphériques mobiles, en fonction de votre serveur. Vous pouvez définir des processus en tant que [Processus spécifiques à Forms on OSGi](/help/forms/using/aem-forms-workflow.md) ou Processus Forms on JEE. Par exemple, vous dirigez un établissement bancaire et utilisez AEM Forms pour gérer les demandes et les communications de vos clients. Vos clients remplissent un formulaire et le soumettent pour vérification. Si vous activez le formulaire sur des périphériques mobiles, vos clients peuvent remplir le formulaire dans l’application AEM Forms. Vous pouvez également gérer le processus de vérification en activant le formulaire de vérification sur les périphériques mobiles. Votre agent de terrain peut apporter un périphérique mobile au client, vérifier les détails et envoyer le formulaire. L’application AEM Forms se synchronise avec le serveur AEM Forms et récupère les formulaires compatibles avec les périphériques mobiles. Si l’application est hors ligne, elle enregistre les données localement.

Le code source de l’application AEM Forms est accessible via la Distribution de logiciels. Le package du code source dans Distribution de logiciels est disponible sous : `adobe-aemfd-forms-app-src-pkg-<version>.zip`.

L’application AEM Forms est prise en charge sur les périphériques iOS, Android, Windows. Vous pouvez installer l’application AEM Forms pour Android à partir de Google Play, pour iOS à partir d’App Store et pour Windows à partir de Windows Store.

    [ ![google_play](assets/google_play.png)](https://play.google.com/store/apps/details?id=com.adobe.aem.forms&amp;hl=fr)
    
    [ ![app_store](assets/app_store.png)](https://itunes.apple.com/fr/app/adobe-experience-manager-forms/id1129625976?ls=1&amp;mt=8)
    
    [ ![microsoft-badge-icon](assets/microsoft-badge-icon.png)](https://www.microsoft.com/fr-fr/store/p/adobe-experience-manager-forms/9nd12rlxtgtt)

Pour installer, personnaliser et distribuer l’application sur les périphériques iOS, Android ou Windows, consultez [Personnaliser, créer et distribuer l’application AEM Forms](#customize-build-distribute).

## Prérequis {#prerequisites}

L’application AEM Forms nécessite un serveur AEM Forms. Les utilisateurs peuvent générer les formulaires que vous créez dans le serveur AEM Forms, les remplir, les enregistrer sous forme de brouillons et les envoyer. L’application se connecte au serveur et y récupère les formulaires activés. L’application AEM Forms se synchronise avec le serveur et dès que les formulaires sont chargés dans l’application, les utilisateurs peuvent travailler hors ligne. Si l’application est hors ligne, les données sont enregistrées sur le périphérique, et les données sont synchronisées avec le serveur lorsque l’application est en ligne.

### Application AEM Forms avec des serveurs utilisant AEM Forms Workflow {#aem-forms-app-with-servers-using-aem-forms-workflow}

Si vous avez un serveur AEM Forms Workflow, vous pouvez générer des formulaires en tant que tâches au sein de l’application AEM Forms. Par exemple, vous dirigez un établissement bancaire et un client remplit une demande d’utilisation de vos services. La demande est un formulaire adaptatif qui accepte les informations de vos clients, puis les stocke en tant qu’envoi pour révision. L’administrateur examine la demande et transfère une demande de vérification à l’agent de terrain. La demande transférée active un formulaire de vérification dans l’application de l’agent de terrain en tant que tâche. Votre agent de terrain apporte le périphérique mobile auprès de votre client et vérifie les détails.

### Application AEM Forms avec des serveurs utilisant des processus basés sur l’utilisation de Forms on OSGi {#aem-forms-app-with-servers-using-forms-centric-workflow-on-osgi}

Si vous avez un serveur AEM Forms, vous pouvez générer des formulaires adaptatifs en tant que demande depuis la boîte de réception AEM et tâches au sein de l’application AEM Forms. Par exemple, vous dirigez un établissement bancaire et un client remplit une demande d’utilisation de vos services. La demande est associée à un formulaire adaptatif qui accepte les informations de vos clients, puis les stocke en tant qu’envoi pour révision. L’administrateur examine la tâche et approuve la demande de vérification à l’agent de terrain. Votre agent de terrain apporte le périphérique mobile auprès de votre client et vérifie les détails.

### Formulaires autonomes ou application AEM Forms avec des serveurs sans le serveur AEM Forms Workflow {#standalone-forms-or-aem-forms-app-with-servers-without-aem-forms-workflow}

Un serveur AEM Forms qui n’utilise pas AEM Forms Workflow est un serveur AEM Forms on OSGi ou un formulaire adaptatif ou mobile autonome. L’application AEM Forms fonctionne avec votre implémentation d’AEM Forms on [OSGi](/help/sites-deploying/configuring-osgi.md). Les formulaires que vous activez et publiez pour l’application AEM Forms sont disponibles dans votre application.

Les formulaires sont téléchargés sur votre application et sont disponibles hors ligne. Par exemple, vous dirigez un établissement bancaire et un client remplit une demande sur votre site. L’application est un formulaire adaptatif qui accepte les informations de vos clients, puis les stocke en vue d’une révision. L’administrateur examine le formulaire et crée un formulaire de vérification dans l’instance d’auteur AEM. L’administrateur active la synchronisation du formulaire avec l’application AEM Forms, et le publie. Si le formulaire de vérification est disponible dans l’application AEM Forms, votre agent de terrain peut utiliser un périphérique mobile pour vérifier les détails de votre client. Le périphérique mobile se synchronise avec le serveur et le formulaire de vérification est chargés dans l’application. Votre agent de terrain peut rendre visite à votre client, vérifier les détails, enregistrer les données en tant que brouillon ou envoyer le formulaire de vérification. Le formulaire est synchronisé avec le serveur dès que l’application est en ligne.

Pour synchroniser votre formulaire dans l’application AEM Forms :

1. Dans l’instance d’auteur, sélectionnez un formulaire, puis cliquez sur **[!UICONTROL Afficher les propriétés]**. 

1. Dans la page des propriétés, cliquez sur **[!UICONTROL Avancé]**.
1. Dans la section Avancé, activez l’option : **[!UICONTROL Synchroniser avec l’application AEM Forms]** et appuyez sur **[!UICONTROL Enregistrer]**.

Lorsque le formulaire est publié, l’application se synchronise avec le serveur et récupère le formulaire. Pour synchroniser plusieurs formulaires, dans l’instance d’auteur, sélectionnez plusieurs formulaires dans le gestionnaire de formulaires et appuyez sur **[!UICONTROL Synchroniser avec l’application AEM Forms]**.

## Prise en charge des périphériques mobiles {#mobile-device-support}

Consultez [Application AEM Forms (précédemment connue sous le nom de Mobile Workspace)](/help/forms/using/aem-forms-jee-supported-platforms.md#aem-forms-workspace-app)

## Fonctions clés de l’application AEM Forms {#key-features-of-aem-forms-app}

### Application AEM Forms avec les serveurs AEM Forms {#aem-forms-app-with-aem-forms-servers}

Vous pouvez synchroniser votre application avec le serveur AEM Forms et manipuler des formulaires sur votre périphérique mobile.

Avec le serveur AEM Forms Workflow, un formulaire peut être associé à un point de départ dans un processus Workbench et une demande depuis la boîte de réception AEM. Une demande depuis la boîte de réception AEM peut avoir un formulaire adaptatif qui lui est associé. Un point de départ peut avoir un formulaire adaptatif, un formulaire HTML5 ou un jeu de formulaires qui lui est associé. Un point de départ peut être envoyé comme tâche ou la tâche peut être enregistrée en tant que brouillon. Pour plus d’informations sur les différences entre une demande depuis la boîte de réception AEM et un point de départ voir [Actions et fonctionnalités des processus AEM basés sur l’utilisation de Forms on OSGi et des processus AEM Forms JEE](capabilities-osgi-jee-workflows.md).

Avec le serveur AEM Forms sans AEM Forms workflow, un formulaire activé pour synchronisation dans l’application est rendu dans l’application AEM Forms. Les formulaires sont disponibles dans l’onglet Formulaires de l’application ; ils peuvent être envoyés ou enregistrés en tant que brouillon. Les formulaires adaptatifs et les formulaires mobiles sont pris en charge dans l’application.

1. **Enregistrement d’une tâche ou d’un formulaire en tant que brouillon**

   L’option Enregistrer en tant que brouillon enregistre un instantané d’une tâche ou d’un formulaire avec les données remplies et les fichiers joints dans le formulaire associé. Les brouillons sont enregistrés sur le périphérique mobile, et synchronisés avec le serveur AEM Forms pour une récupération ultérieure.

   Reportez-vous à la section [Enregistrement d’une tâche ou d’un formulaire en tant que brouillon](/help/forms/using/save-as-draft.md).

1. **Enregistrer un formulaire en tant que modèle** 

   Parfois, lorsque les utilisateurs remplissent un formulaire, les entrées à certains champs restent les mêmes. Pour ces instances, vous pouvez remplir les champs nécessitant des valeurs identiques dans chaque instance et enregistrer le formulaire ou le brouillon en tant que modèle. Désormais, chaque fois que vous créez une instance du modèle, les champs spécifiés sont déjà remplis avec les valeurs spécifiées dans le modèle. Cela vous aide à gagner du temps et les efforts requis pour remplir le formulaire.

   Consultez la section [Enregistrer des formulaires en tant que modèles](/help/forms/using/save-forms-and-start-points-as-templates.md).

### Utilisation des tâches et des formulaires {#working-with-tasks-and-forms}

Vous pouvez synchroniser votre application avec le serveur AEM Forms Workflow et travailler avec des tâches et des formulaires sur votre périphérique mobile.

Une tâche sur le périphérique mobile contient un formulaire adaptatif, un formulaire HTML5, ou un ensemble de formulaires et peut également contenir des pièces jointes et [l’URL du résumé](/help/forms/using/getting-task-variables-summary-url.md). Par défaut, les tâches qui vous sont assignées sont placées dans le dossier **[!UICONTROL Tâches]**. Lorsque vous travaillez sur une tâche, vous pouvez modifier la tâche et enregistrer un brouillon sur le serveur AEM Forms.

Un formulaire sur le périphérique mobile peut être un formulaire adaptatif ou un formulaire mobile. Les formulaires activés pour synchronisation dans l’application de formulaires sont disponibles dans le dossier Formulaires. Vous pouvez synchroniser des formulaires activés dans le serveur AEM Forms sans AEM Forms Workflow (AEM Forms on OSGi).

Voir :

* [Ouverture d’une tâche](/help/forms/using/open-task.md)
* [Utilisation d’un formulaire](/help/forms/using/working-with-form.md)

### Travail hors connexion {#working-offline}

Vous pouvez travailler sur votre périphérique mobile en mode hors connexion. Vous pouvez vous connecter à l’application même s’il n’y a aucune connectivité réseau et travailler sur tous les formulaires qui ont été synchronisées avec le périphérique lors de votre dernière connexion. Pour plus d’informations sur les modalités de synchronisation de vos formulaires, consultez la section [Synchronisation de l’application](/help/forms/using/sync-app.md). Si vous choisissez de synchroniser les pièces jointes associées à un formulaire, vous pouvez également ouvrir les pièces jointes en mode hors connexion. Vous pouvez modifier le formulaire, ajouter des annotations et envoyer ou enregistrer un formulaire en mode hors connexion. Le formulaire sera synchronisé avec le serveur AEM Forms lors de votre prochaine connexion.

Pour plus d’informations, consultez la section [Utilisation en mode hors connexion](/help/forms/using/work-offline-mode.md).

### Ajout d’annotations {#adding-annotations}

Vous pouvez ajouter les pièces jointes suivantes à un formulaire sur votre périphérique mobile

* **Notes :** vous pouvez employer la fonction Notes pour ajouter une annotation à main levée ou une note textuelle dans votre formulaire. Pour plus d’informations, consultez la section [Ajout d’une note](/help/forms/using/add-attachments.md#adding-a-note).

* **Image :** l’application AEM Forms a une fonction qui emploie la fonctionnalité de caméra ou la galerie de votre équipement mobile. En utilisant la pièce jointe de photo, vous pouvez ajouter une photo avec le formulaire associé. Pour plus d’informations, consultez la section [Ajout d’une photographie](/help/forms/using/add-attachments.md#adding-a-photograph).

### Enregistrement auto {#autosave}

Lorsqu’un utilisateur saisit des données dans l’application AEM Forms, la fonction d’enregistrement automatique l’enregistre à intervalles réguliers. La fonction d’enregistrement automatique dans l’application AEM Forms vous permet d’éviter la perte de données si l’application se ferme en raison de conditions comme une batterie faible.

Référez-vous à la section [Utilisation de l’enregistrement automatique dans l’application AEM Forms](/help/forms/using/autosave-data-app.md).

## Différences entre les fonctionnalités de la boîte de réception AEM et l’application AEM Forms {#differences-between-aem-inbox-and-aem-forms-app-features}

Deux des moyens principaux de lancer un workflow basé sur l’utilisation de Forms sont la [boîte de réception AEM](/help/forms/using/manage-applications-inbox.md) et l’application AEM Forms. Les fonctionnalités de la boîte de réception AEM et de l’application AEM Forms sont cependant différentes. La boîte de réception AEM fonctionne uniquement avec des [workflows basés sur l’utilisation de Forms](/help/forms/using/aem-forms-workflow.md) tandis que l’application AEM Forms fonctionne avec des workflows basés sur l’utilisation de Forms ainsi que la gestion des processus. Pour plus d’informations sur les différences entre les fonctionnalités de l’application AEM Forms et de la boîte de réception AEM, voir [Actions et fonctionnalités des workflows AEM basés sur l’utilisation de Forms on OSGi et des workflows AEM Forms on JEE](capabilities-osgi-jee-workflows.md).

## Formulaires pris en charge {#supported-forms}

Types de formulaire pris en charge par l’application AEM Forms :

### Formulaire adaptatif {#adaptive-form}

Un formulaire adaptatif qui s’adapte de façon dynamique aux entrées utilisateur est pris en charge par l’application AEM Forms. Les formulaires adaptatifs chargés en différé sont également pris en charge.

### Formulaire pour périphérique mobile {#mobile-form}

Vous pouvez créer des formulaires pour les périphériques mobiles dans AEM Forms. Les formulaires pour périphériques mobiles sont rendus en tant que formulaires HTML sur des périphériques mobiles qui s’adaptent en fonction des périphériques d’affichage.

### Jeu de formulaires {#formset}

Avec les jeux de formulaires, plusieurs formulaires associés à un service ou processus peuvent être regroupés pour automatiser un processus d’entreprise et présentés aux utilisateurs finaux. Dans ce cas, les utilisateurs peuvent remplir le jeu entier comme un seul et il n’est pas nécessaire de classer, envoyer et suivre des processus ou des formulaires individuels.

>[!NOTE]
>
>Nécessite AEM Forms Workflow (AEM Forms sous JEE).

## Fonctionnement de l’application AEM Forms {#how-aem-forms-app-works}

L’application AEM Forms fournit une solution mobile aux agents de terrain qui leur permet de travailler sur les formulaires qui leur sont assignés. L’application met en cache les données complètes à partir du serveur et apporte une expérience utilisateur supérieure en enregistrant le travail en local. Les données du disque sont envoyées au serveur via les mises à jour régulières de synchronisation.

L’application AEM Forms est une application basée sur PhoneGap 5.0 dans laquelle le modèle Backbone est utilisé efficacement pour présenter des données stockées dans les modèles par le biais de vues. Toutes les opérations natives sont exécutées via des modules externes PhoneGap.

## Personnaliser, créer et distribuer l’application AEM Forms {#customize-build-distribute}

>[!NOTE]
>
>Applicable uniquement si vous utilisez le code source de l’application AEM Forms pour créer l’application.

L’application AEM Forms est facile à personnaliser en fonction des besoins spécifiques d’une organisation. Le code source de l’application est fourni avec AEM Forms. Vous pouvez modifier le code source et concevoir votre propre solution mobile destinée au personnel de terrain. Vous pouvez également signer l’application avec votre propre clé d’entreprise.

### Personnalisation {#customize}

Vous pouvez personnaliser votre application aux fins suivantes :

**Identité graphique** : modifiez l’icône de l’application, le nom de l’application, les images de lancement et les pages dans l’application AEM Forms. Vous pouvez également modifier le texte pour adapter l’application à une région particulière. Pour plus d’informations sur l’identité graphique de l’application AEM Forms, référez-vous à [Personnalisation de l’identité graphique](/help/forms/using/branding-customization.md).

**Thème** : modifiez les styles tels que couleurs, polices et espacements dans l’interface utilisateur de l’application AEM Forms. Pour plus d’informations, consultez [Personnalisation du thème](/help/forms/using/theme-customization.md).

**Gestes** : modifiez les gestes, comme le glissement vers la droite ou vers la gauche, dans l’interface utilisateur de l’application AEM Forms. Pour plus d’informations, consultez [Personnalisation des gestes](/help/forms/using/gesture-customization.md).

Pour plus d’informations sur la configuration d’un projet d’application AEM Forms à des fins de personnalisation, consultez :

* [Configuration de l’environnement de l’application AEM Forms](/help/forms/using/setup-environment-mobile-workspace.md)
* [Configuration d’un projet Visual Studio et création d’une application Windows](/help/forms/using/setup-visual-studio-project-build-installer.md)
* [Configuration d’un projet Xcode et création d’une application iOS ](/help/forms/using/setup-xcode-project-build-installer.md)
* [Configuration d’un projet Eclipse et création d’une application Android](/help/forms/using/setup-eclipse-project-build-installer.md)

### Créer et distribuer {#build-and-distribute}

Le code source de l’application AEM Forms peut être extrait à partir de `adobe-lc-mobileworkspace-src.zip`, disponible en tant que package source de l’application AEM Forms dans Distribution de logiciels.

Pour obtenir le code source de l’application AEM Forms, procédez comme suit :

1. Ouvrez la [Distribution de logiciels](https://experience.adobe.com/downloads). Vous avez besoin d’un Adobe ID pour vous connecter à la Distribution de logiciels.
1. Appuyez sur **[!UICONTROL Adobe Experience Manager]** disponible dans le menu d’en-tête.
1. Dans la section **[!UICONTROL Filtres]** :
   1. Sélectionnez **[!UICONTROL Formulaires]** dans la liste déroulante **[!UICONTROL Solution]**.
   2. Sélectionnez la version et le type du package. Vous pouvez également utiliser l’option **[!UICONTROL Rechercher des téléchargements]** pour filtrer les résultats.
1. Appuyez sur le nom de package applicable à votre système d’exploitation, sélectionnez **[!UICONTROL Accepter les conditions du CLUF]**, puis appuyez sur **[!UICONTROL Télécharger]**.
1. Ouvrez [Package Manager](https://docs.adobe.com/content/help/fr/experience-manager-65/administering/contentmanagement/package-manager.html) et cliquez sur **[!UICONTROL Télécharger le package]** pour télécharger le package.
1. Sélectionnez le package et cliquez sur **[!UICONTROL Installer]**.

**Pour iOS** :

Pour plus d’informations sur la création d’une application iOS (.ipa), référez-vous à [Configuration d’un projet Xcode et création d’une application iOS](/help/forms/using/setup-xcode-project-build-installer.md).

Pour plus d’informations sur la manière de signer l’application AEM Forms avec votre profil d’approvisionnement, consultez [Paramètres de signature de code iOS, processus et dépannage](https://developer.apple.com/support/code-signing/).

**Pour Android** :

Pour plus d’informations sur la création d’une application Android (.apk), consultez la page [Configurer un projet Eclipse et créer une application Android](/help/forms/using/setup-eclipse-project-build-installer.md).

Pour plus d’informations sur la manière de signer l’application AEM Forms, consultez [Signature de vos applications](https://developer.android.com/tools/publishing/app-signing.html).

**Pour Windows** :

Pour plus d’informations sur la création d’une application Windows (.appx), consultez la page [Configurer un projet Visual Studio et créer une application Windows](/help/forms/using/setup-visual-studio-project-build-installer.md).

Pour plus d’informations sur les modalités de distribution de l’application via MDM, consultez la page [Distribution de l’application AEM Forms](/help/forms/using/distribute-mobile-workspace-app.md). La distribution de l’application via MDM s’applique uniquement à iOS et Android.

## Recommandations de mise à niveau de Mobile Workspace vers l’application à l’application AEM Forms {#recommendations-to-upgrade-mobile-workspace-to-aem-forms-app}

Si vous effectuez une mise à niveau vers la dernière version de l’application AEM Forms, veillez à lire les points suivants :

* **Si vous avez installé une version antérieure de l’application à partir du Play Store sur Android,** vous pouvez mettre à niveau l’application directement du Play Store.

* **Si une version antérieure de l’application est créée et installée à l’aide du code source (applicable pour iOS et Android)** :

   Avant d’installer la nouvelle application, synchronisez toutes vos données avec le serveur AEM Forms. Une fois les données synchronisées, désinstallez la version antérieure de l’application et installez la nouvelle application.
