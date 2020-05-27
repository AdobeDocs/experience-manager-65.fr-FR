---
title: Intégration à Adobe Campaign Standard
seo-title: Intégration à Adobe Campaign Standard
description: Intégration à Adobe Campaign Standard.
seo-description: Intégration à Adobe Campaign Standard.
uuid: ef31339e-d925-499c-b8fb-c00ad01e38ad
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 5c0fec99-7b1e-45d6-a115-e498d288e9e1
translation-type: tm+mt
source-git-commit: f951c195c581f770dcc87fdf4a89d40ee6dd9ec0
workflow-type: tm+mt
source-wordcount: '1322'
ht-degree: 69%

---


# Intégration à Adobe Campaign Standard{#integrating-with-adobe-campaign-standard}

>[!NOTE]
>
>Cette documentation décrit comment intégrer AEM à Adobe Campaign Standard, la solution par abonnement. Si vous utilisez Adobe Campaign 6.1, voir [Intégration à Adobe Campaign 6.1](/help/sites-administering/campaignonpremise.md) pour ces instructions.

Adobe Campaign permet de gérer le contenu et les formulaires d’envoi de courrier électronique directement dans Adobe Experience Manager.

Pour utiliser les deux solutions ensemble, vous devez d’abord les configurer pour les connecter l’une à l’autre. Cela implique certaines étapes de configuration à la fois dans Adobe Campaign et dans Adobe Experience Manager, qui sont décrites en détail dans ce document.

L’utilisation d’Adobe Campaign dans AEM comprend la possibilité d’envoyer du courrier électronique et des formulaires via Adobe Campaign et elle est décrite dans [Utilisation d’Adobe Campaign](/help/sites-authoring/campaign.md).

En outre, les rubriques suivantes peuvent être utiles lors de l’intégration d’AEM avec [Adobe Campaign](https://docs.campaign.adobe.com/doc/standard/fr/home.html) :

* [Meilleures pratiques des modèles de courrier électronique](/help/sites-administering/best-practices-for-email-templates.md)
* [Résolution des incidents liés à votre intégration Adobe Campaign](/help/sites-administering/troubleshooting-campaignintegration.md)

Si vous étendez votre intégration à Adobe Campaign, vous pouvez consulter les pages suivantes :

* [Création d’extensions personnalisées](/help/sites-developing/extending-campaign-extensions.md)
* [Création de mises en correspondance de formulaires personnalisés](/help/sites-developing/extending-campaign-form-mapping.md)

## Configuration d’Adobe Campaign {#configuring-adobe-campaign}

La configuration d’Adobe Campaign implique les tâches suivantes :

1. Configuration de l’utilisateur **aemserver**
1. Création d’un compte externe dédié
1. Vérification de l’option AEMResourceTypeFilter
1. Création d’un modèle de livraison dédié

>[!NOTE]
>
>To perform these operations, you must have the **administration** role in Adobe Campaign.

### Conditions préalables {#prerequisites}

Au préalable, assurez-vous de disposer des éléments suivants :

* [Une instance de création AEM](/help/sites-deploying/deploy.md#getting-started)
* [Une instance de publication AEM](/help/sites-deploying/deploy.md#author-and-publish-installs)
* [Une instance Adobe Campaign](https://docs.adobe.com/content/docs/fr/campaign/ACS.html)

>[!CAUTION]
>
>Operations detailed in the [Configuring Adobe Campaign](#configuring-adobe-campaign) and [Configuring Adobe Experience Manager](#configuring-adobe-experience-manager) sections are necessary for the integration functionalities between AEM and Adobe Campaign to work correctly.

### Configuration de l’utilisateur aemserver {#configuring-the-aemserver-user}

The **aemserver** user must be configured in Adobe Campaign. The **aemserver** is a technical user that will be used to connect the AEM server to Adobe Campaign.

Go to **Administration** >  **Users &amp; Security** >  **Users**, and select the **aemserver** user. Cliquez dessus pour ouvrir les paramètres utilisateur.

* Vous devez définir un mot de passe pour cet utilisateur. Cette opération ne peut pas être effectuée via l’interface utilisateur. Cette configuration doit être effectuée dans REST par un administrateur technique.
* You can assign specific roles to this user, such as **deliveryPrepare**, which allows the user to create and edit deliveries.

### Configuration d’un compte externe Adobe Experience Manager {#configuring-an-adobe-experience-manager-external-account}

Vous devez configurer un compte externe permettant de connecter Adobe Campaign à votre instance AEM.

>[!NOTE]
>
>Dans AEM, veillez à définir le mot de passe de l’utilisateur distant d’Adobe Campaign. Vous devez définir ce mot de passe pour connecter Adobe Campaign à AEM. Connectez-vous en tant qu’administrateur et, dans la console d’administration des utilisateurs, recherchez l’utilisateur à distance d’Adobe Campaign et cliquez sur **Définir le mot de passe**.

Pour configurer un compte externe AEM :

1. Go to **Administration** > **Application settings** > **External accounts**.

   ![chlimage_1-124](assets/chlimage_1-124a.png)

1. Select the default **aemInstance** external account or create a new one by clicking the **Create** button.
1. Select **Adobe Experience Manager** i n the **Type** field and enter the access parameters used for your AEM authoring instance: server address, account name and password.

   >[!NOTE]
   >
   >Veillez à ne pas ajouter de barre oblique **/** à la fin de l’URL ou la connexion ne fonctionnera pas.

1. Make sure that the **Enabled** checkbox is selected, then click **Save** to save your modifications.

### Vérification de l’option AEMResourceTypeFilter {#verifying-the-aemresourcetypefilter-option}

The **AEMResourceTypeFilter** option is used to filter types of AEM resources that can be used in Adobe Campaign. Cela permet à Adobe Campaign de récupérer le contenu AEM conçu spécifiquement pour n’être utilisé que dans Adobe Campaign.

Cette option est préconfigurée, cependant, si vous la modifiez, l’intégration risque de ne pas fonctionner.

Pour vérifier que l’option **AEMResourceTypeFilter** est configurée :

1. Accédez à **Administration** > **Paramètres d’application** > **Options**.
1. In the list, you can ensure that the **AEMResourceTypeFilter** option is listed and that the paths are correct.

### Création d’un modèle de livraison de courrier électronique spécifique à AEM {#creating-an-aem-specific-email-delivery-template}

Par défaut, la fonction AEM n’est pas activée dans les modèles de courrier électronique Adobe Campaign. Vous pouvez configurer un nouveau modèle de livraison de courrier électronique utilisable pour créer des courriers électroniques avec du contenu AEM.

Pour créer un modèle de livraison de courrier électronique spécifique à AEM :

1. Accédez à **Ressources** > **Modèles** > **Modèles de livraison**.
1. **Activez la sélection** en cliquant sur la coche dans la barre d’actions et en sélectionnant le modèle par défaut de courrier électronique **standard (courrier)** existant, puis en le duplicata en cliquant sur l’icône **Copier** et en cliquant sur **Confirmer**.
1. Disable the selection mode by clicking the **x** and open the newly created **Copy of Standard email (mail)** template, then select **Edit properties** from the action bar of the template dashboard.

   Vous pouvez modifier le libellé du modèle ****.

1. Dans la section **Contenu** des propriétés, modifiez la **source de contenu** en **Adobe Experience Manager**. Sélectionnez ensuite le compte externe qui a été créé auparavant, puis cliquez sur **Confirmer**.

   Enregistrez vos modifications en cliquant sur **Confirmer** et sur **Enregistrer.**

   La fonction de contenu AEM sera activée pour les livraisons de courrier électronique créées à partir de ce modèle.

   ![chlimage_1-125](assets/chlimage_1-125a.png)

## Configuration d’Adobe Experience Manager {#configuring-adobe-experience-manager}

Pour configurer AEM, vous devez procéder comme suit :

* Configurez la réplication entre les instances.
* Connectez-vous à Adobe Campaign.
* Configurez l’externaliseur.

### Configuration de la réplication entre les instances AEM {#configuring-replication-between-aem-instances}

Le contenu créé à partir de l’instance de création AEM est d’abord envoyé à l’instance de publication. Cette instance de publication transfère ensuite le contenu vers Adobe Campaign. L’agent de réplication doit donc être configuré pour répliquer à partir de l’instance de création AEM vers l’instance de publication AEM.

>[!NOTE]
>
>Si vous ne souhaitez pas utiliser l’URL de réplication, mais plutôt l’URL conviviale, vous pouvez définir l’**URL publique** dans le paramètre de configuration suivant dans OSGi (**Outils** > **Console web** > **Configuration OSGi > Intégration AEM Campaign – configuration**) :
**URL publique :** com.day.cq.mcm.campaign.impl.IntegrationConfigImpl#aem.mcm.campaign.publicUrl

Cette étape est également nécessaire pour répliquer certaines configurations d’instance de création dans l’instance de publication.

Pour configurer la réplication entre les instances AEM :

1. From the authoring instance, select **AEM logo**> **Tools** > **Deployment** > **Replication** > **Agents on author**, then click **Default Agent**.

   ![chlimage_1-126](assets/chlimage_1-126a.png)

   >[!NOTE]
   Évitez d’utiliser l’hôte local localhost (il s’agit d’une copie locale d’AEM) lors de la configuration de votre intégration avec Adobe Campaign, à moins que les instances de publication et de création se trouvent toutes deux sur le même ordinateur.

1. Click **Edit** then select the **Transport** tab.
1. Configurez l’URI en remplaçant **localhost** par l’adresse IP ou l’adresse de l’instance de publication AEM.

   ![chlimage_1-127](assets/chlimage_1-127a.png)

### Connexion d’AEM à Adobe Campaign {#connecting-aem-to-adobe-campaign}

Avant que vous puissiez utiliser AEM et Adobe Campaign ensemble, vous devez établir la liaison entre les deux solutions afin qu’elles puissent communiquer.

1. Connectez-vous à votre instance de création AEM.
1. Select **Tools** > **Operations** > **Cloud** > **Cloud Services**, then **Configure now** in the Adobe Campaign section.

   ![chlimage_1-128](assets/chlimage_1-128a.png)

1. Create a new configuration by entering a **Title** and click **Create**, or choose the existing configuration that you want to link with your Adobe Campaign instance.
1. Modifiez la configuration afin qu’elle corresponde aux paramètres de votre instance Adobe Campaign.

   * **Nom d&#39;utilisateur**: **aemserver**, l’opérateur de package d’intégration AEM Adobe Campaign utilisé pour établir le lien entre les deux solutions.
   * **Mot de passe** : mot de passe de l’opérateur aemserver Adobe Campaign. Vous devrez peut-être respécifier le mot de passe pour cet opérateur directement dans Adobe Campaign.
   * **Point de terminaison de l’API** : URL de l’instance Adobe Campaign.

1. Select **Connect to Adobe Campaign** and click **OK**.

   ![chlimage_1-129](assets/chlimage_1-129a.png)

   >[!NOTE]
   Après avoir [créé et publié votre courrier électronique](/help/sites-authoring/campaign.md), vous devez republier la configuration sur votre instance de publication.

   ![chlimage_1-130](assets/chlimage_1-130a.png)

>[!NOTE]
Si la connexion échoue, vérifiez les éléments suivants :
* Vous pouvez rencontrer un problème de certificat lorsque vous utilisez une connexion sécurisée sur une instance Adobe Campaign (https). Vous devrez ajouter le certificat d’instance Adobe Campaign au **cacerts **fichier de votre JDK.
* Voir également [Résolution des incidents liés à votre intégration AEM/Adobe Campaign](/help/sites-administering/troubleshooting-campaignintegration.md).



### Configuration de l’externaliseur {#configuring-the-externalizer}

Vous devez [configurer l’externaliseur](/help/sites-developing/externalizer.md) dans AEM sur votre instance de création. L’externaliseur est un service OSGi qui vous permet de transformer un chemin de ressources en une URL absolue externe. Ce service propose un emplacement centralisé pour configurer ces adresses URL externes et les créer.

Pour des instructions générales, voir [Configuration de l’externaliseur](/help/sites-developing/externalizer.md). For the Adobe Campaign integration, make sure you configure the publish server at `https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl` not point to `localhost:4503` but to a server that is reachable by the Adobe Campaign console.

S’il pointe vers `localhost:4503` ou un autre serveur auquel Adobe Campaign ne parvient pas à se connecter, les images ne s’affichent pas dans la console Adobe Campaign.

![chlimage_1-131](assets/chlimage_1-131a.png)

