---
title: Installation de la version [!DNL Workfront for Experience Manager enhanced connector]
description: Installation de la version [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Integrations
source-git-commit: 468a8d96153c67232524eea6f180c9ceb364d60a
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---


# Installation de la version [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

Un utilisateur disposant d’un accès administrateur dans [!DNL Adobe Experience Manager] installe le connecteur amélioré. Avant de procéder à l’installation, vérifiez la prise en charge de la plateforme et d’autres [conditions préalables pour le connecteur](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>L’Adobe nécessite le déploiement et la configuration de [!DNL Adobe Workfront for Experience Manager enhanced connector] uniquement par le biais de partenaires certifiés ; [!DNL Adobe Professional Services]. Si elles sont déployées et configurées sans partenaire certifié ou [!DNL Adobe Professional Services], il n’est pas pris en charge par Adobe.
>
>Adobe peut mettre à jour les [!DNL Adobe Workfront] et [!DNL Adobe Experience Manager] qui rend ce connecteur redondant ; si cela se produit, les clients peuvent être tenus de passer de l’utilisation de ce connecteur.

Pour installer le connecteur, procédez comme suit :

1. Téléchargez le connecteur à partir de [[!DNL Software Distribution] link](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip).

1. [Configuration du pare-feu](https://one.workfront.com/s/document-item?bundleId=the-new-workfront-experience&amp;topicId=Content%2FAdministration_and_Setup%2FGet_started-WF_administration%2Fconfigure-your-firewall.html).

1. Sur le dispatcher, autorisez les en-têtes HTTP nommés `authorization`, `username`, et `apikey`. Autoriser `GET`, `POST`, et `PUT` de `/bin/workfront-tools`.

1. Assurez-vous que les chemins suivants n’existent pas dans [!DNL Experience Manager] référentiel :

   * `/apps/dam/gui/coral/components/admin/schemaforms/formbuilder`
   * `/apps/dam/gui/coral/components/admin/folderschemaforms/formbuilder`
   * `/apps/dam/gui/content/foldermetadataschemaeditor`
   * `/apps/dam/cfm/models/editor/components/datatypeproperties`
   * `/apps/settings/dam/cfm/models/formbuilderconfig`

1. Installez le module à l’aide de [!UICONTROL Gestionnaire de modules]. Pour savoir comment installer des packages, voir [Documentation du gestionnaire de modules](/help/sites-administering/package-manager.md).

1. Créer `wf-workfront-users` in [!DNL Experience Manager] Groupe d’utilisateurs et attribuer l’autorisation `jcr:all` to `/content/dam`.

Un utilisateur système `workfront-tools` est créée automatiquement et les autorisations requises sont gérées automatiquement. Tous les utilisateurs de [!DNL Workfront] Les utilisateurs qui utilisent le connecteur sont automatiquement ajoutés dans le cadre de ce groupe.

## Configurer la connexion entre [!DNL Experience Manager] et [!DNL Workfront] {#configure-connection}

Pour créer une connexion avec Workfront, procédez comme suit :

1. Dans [!DNL Experience Manager], sélectionnez **[!UICONTROL Outils]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configuration des outils Workfront]**.

1. Sélectionner `workfront-tools` dans le panneau de gauche, puis sélectionnez **[!UICONTROL Créer]** dans la zone supérieure droite de la page.

1. Dans le **[!UICONTROL Connexion Workfront]** , fournissez les détails requis de votre [!DNL Workfront] déploiement, puis sélectionnez **[!UICONTROL Connexion à Workfront]** . Une fois la connexion établie, la variable [!DNL Workfront] l’intégration personnalisée du document est créée automatiquement dans la variable [!DNL Workfront] environnement.

   ![Connexion [!DNL Experience Manager] et [!DNL Workfront]](/help/assets/assets/wf-connection-config.png)

1. Pour vérifier la connexion, accédez-y [!DNL Workfront] et vérifiez que la clé API est la même et que la connexion est **[!UICONTROL Activé]**. Pour ce faire, sélectionnez **[!UICONTROL Configuration]** > **[!UICONTROL Documents]** > **[!UICONTROL Intégrations personnalisées]** in [!DNL Workfront].
