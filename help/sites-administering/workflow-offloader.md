---
title: Déchargeur de workflow de ressources
seo-title: Déchargeur de workflow de ressources
description: Familiarisez-vous avec le déchargeur de workflow de ressources.
seo-description: Familiarisez-vous avec le déchargeur de workflow de ressources.
uuid: d1c93ef9-a0e1-43c7-b591-f59d1ee4f88b
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: 91f0fd7d-4b49-4599-8f0e-fc367d51aeba
translation-type: tm+mt
source-git-commit: f24142064b15606a5706fe78bf56866f7f9a40ae

---


# Déchargeur de workflow de ressources{#assets-workflow-offloader}

Le déchargeur de workflow de ressources permet à plusieurs instances Adobe Experience Manager (AEM) Assets de réduire la charge de traitement sur l’instance principale. La charge de traitement est répartie entre l’instance principale et les différentes instances de déchargement (auxiliaires) que vous y ajoutez. La répartition de la charge de traitement des ressources augmente l’efficacité et la vitesse de traitement des ressources par AEM Assets. De plus, elle contribue à allouer des ressources dédiées pour traiter des ressources d’un type MIME particulier. Par exemple, vous pouvez réserver un nœud spécifique de votre topologie au traitement des ressources InDesign.

## Configuration de la topologie du déchargeur {#configure-offloader-topology}

Utilisez Configuration Manager pour ajouter l’URL de l’instance de filet de conduite et les noms d’hôte des instances de déchargement pour les demandes de connexion sur l’instance de filet de conduite.

1. Tap/click the AEM logo, and choose **Tools** > **Operations** > **Web Console** to open Configuration Manager.
1. From the Web Console, select **Sling** >  **Topology Management**.

   ![chlimage_1-44](assets/chlimage_1-44a.png)

1. In the Topology Management page, tap/click the **Configure Discovery.Oak Service** link.

   ![chlimage_1-45](assets/chlimage_1-45a.png)

1. In the Discovery Service Configuration page, specify the connector URL for the leader instance in the **Topology Connector URLs** field.

   ![chlimage_1-46](assets/chlimage_1-46a.png)

1. In the **Topology Connector Whitelist** field, specify IP address or host names of offloader instances that are allowed to connect with the leader instance. Appuyez/cliquez sur **Enregistrer**.

   ![chlimage_1-47](assets/chlimage_1-47a.png)

1. Pour afficher les instances de déchargement connectées à l’instance principale, sélectionnez **Tools** > **Deployment** > **Topology** et appuyez/cliquez sur la vue Cluster.

## Désactivation du déchargement {#disable-offloading}

1. Tap/click the AEM logo, and choose **Tools** > **Deployment** > **Offloading**. The **Offloading Browser** page displays topics and the server instances that can consume the topics.

   ![chlimage_1-48](assets/chlimage_1-48a.png)

1. Disable the *com/adobe/granite/workflow/offloading* topic on the leader instances with which users interact to upload or change AEM assets.

   ![chlimage_1-49](assets/chlimage_1-49a.png)

## Configuration des lanceurs de workflow sur l’instance principale {#configure-workflow-launchers-on-the-leader-instance}

Configure workflow launchers to use the [!UICONTROL DAM Update Asset Offloading] workflow on the leader instance instead of the **Dam Update Asset** workflow.

1. Tap/click the AEM logo, and choose, **Tools** > **Workflow** > **Launchers** to open the **Workflow Launchers** console.

   ![chlimage_1-50](assets/chlimage_1-50a.png)

1. Locate the two Launcher configurations with event type **Node Created** and **Node Modified** respectively, which run the **DAM Update Asset** workflow.
1. For each configuration, select the checkbox before it and tap/click the **View Properties** icon from the toolbar to display the **Launcher Properties** dialog.

   ![chlimage_1-51](assets/chlimage_1-51a.png)

1. From the **Workflow** list, choose [!UICONTROL DAM Update Asset Offloading] and tap/click **Save**.

   ![chlimage_1-52](assets/chlimage_1-52a.png)

1. Tap/click the AEM logo, and choose, **Tools** > **Workflow** > **Models** to open the **Workflow Models** page.
1. Select the [!UICONTROL DAM Update Asset Offloading] workflow, and tap/click **Edit** from the toolbar to display its details.

   ![chlimage_1-53](assets/chlimage_1-53a.png)

1. Display the context menu for the **DAM Workflow Offloading** step, and choose **Edit**. Vérifiez la saisie dans le champ **Rubrique de tâche** de l’onglet **Arguments génériques** de la boîte de dialogue de configuration.

   ![chlimage_1-54](assets/chlimage_1-54a.png)

## Désactivation des lanceurs de workflow sur les instances de déchargement {#disable-the-workflow-launchers-on-the-offloader-instances}

Disable the workflow launchers that run the **DAM Update Asset** workflow on the leader instance.

1. Tap/click the AEM logo, and choose, **Tools** > **Workflow** > **Launchers** to open the **Workflow Launchers** console.

   ![chlimage_1-55](assets/chlimage_1-55a.png)

1. Locate the two Launcher configurations with event type **Node Created** and **Node Modified** respectively, which run the **DAM Update Asset** workflow.
1. For each configuration, select the checkbox before it and tap/click the **View Properties** icon from the toolbar to display the **Launcher Properties** dialog.

   ![chlimage_1-56](assets/chlimage_1-56a.png)

1. In the **Activate** section, drag the slider to disable the workflow launcher and tap/click **Save** to disable it.

   ![chlimage_1-57](assets/chlimage_1-57a.png)

1. Téléchargez tout fichier de type image dans l’instance de filet de conduite. Vérifiez les miniatures générées et reportées pour le fichier par l’instance déchargée.

