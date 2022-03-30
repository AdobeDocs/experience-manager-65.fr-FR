---
title: Installation de la version [!DNL Workfront for Experience Manager enhanced connector]
description: Installation de la version [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Integrations
exl-id: 087bc811-e8f8-4db5-b066-627a9b082f57
source-git-commit: 679ad8f1fec1abe97dfc90b6318c3f3c4ab85b7f
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 47%

---

# Installation de la version [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

Un utilisateur disposant d’un accès administrateur dans [!DNL Adobe Experience Manager]  installe le connecteur amélioré. Avant de procéder à l’installation, vérifiez la prise en charge de la plateforme et d’autres [conditions préalables pour le connecteur](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!TIP]
>
>Recherchez-vous la variable [!DNL Workfront for Experience Manager enhanced connector] documentation pour AEM as a Cloud Service ? Cliquez sur [here](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/integrations/workfront-connector-install.html?lang=en).

>[!IMPORTANT]
>
>Adobe requiert le déploiement et la configuration du [!DNL Adobe Workfront for Experience Manager enhanced connector] uniquement par le biais de partenaires certifiés ou d’[!DNL Adobe Professional Services]. S’il est déployé et configuré sans partenaire certifié ou sans [!DNL Adobe Professional Services], il n’est pas pris en charge par Adobe.
>
>Adobe peut apporter des mises à jour à [!DNL Adobe Workfront] et [!DNL Adobe Experience Manager], lesquelles peuvent rendre ce connecteur inutile. Si cela se produit, les clients peuvent être amenés à abandonner l’utilisation de ce connecteur.

Pour installer le connecteur, procédez comme suit :

1. Téléchargez le connecteur à partir de [[!DNL Software Distribution] link](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip).
1. [Configuration du pare-feu](https://one.workfront.com/s/document-item?bundleId=the-new-workfront-experience&amp;topicId=Content%2FAdministration_and_Setup%2FGet_started-WF_administration%2Fconfigure-your-firewall.html?lang=fr).
1. Sur le répartiteur, autorisez les en-têtes HTTP nommés `authorization`, `username`, et `apikey`. Autorisez les requêtes `GET`, `POST`, et `PUT` à `/bin/workfront-tools`.
1. Assurez-vous que les chemins d’accès suivants n’existent pas dans le référentiel [!DNL Experience Manager] :

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

1. Dans [!DNL Experience Manager], sélectionnez **[!UICONTROL Outils]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configuration des outils Workfront]**.

1. Sélectionnez `workfront-tools` dans le panneau de gauche et sélectionnez l’option **[!UICONTROL Créer]** dans la zone supérieure droite de la page.

1. Dans la boîte de dialogue **[!UICONTROL Connexion Workfront]**, fournissez les détails requis de votre déploiement [!DNL Workfront], et sélectionnez l’option **[!UICONTROL Connexion à Workfront]**. Une fois la connexion établie, l’intégration personnalisée du document [!DNL Workfront] est créée automatiquement dans l’environnement [!DNL Workfront].

   ![Connexion [!DNL Experience Manager] et [!DNL Workfront]](/help/assets/assets/wf-connection-config.png)

1. Pour vérifier la connexion, accédez-y [!DNL Workfront] et vérifiez que la clé API est la même et que la connexion est **[!UICONTROL Activé]**. Pour ce faire, sélectionnez **[!UICONTROL Configuration]** > **[!UICONTROL Documents]** > **[!UICONTROL Intégrations personnalisées]** in [!DNL Workfront].

## Mettre à jour [!DNL Workfront for Experience Manager enhanced connector] {#update-enhanced-connector-for-workfront}

Experience Manager Assets vous permet de mettre à jour la variable [!DNL Workfront for Experience Manager enhanced connector] d’une version précédente à la dernière version.

Pour mettre à jour la variable [!DNL Workfront for Experience Manager enhanced connector] vers la dernière version :

1. Téléchargez la dernière version du connecteur amélioré à partir de [[!DNL Software Distribution] link](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip).
1. Installez le module à l’aide de [!UICONTROL Gestionnaire de modules]. Pour savoir comment installer des packages, voir [Documentation du gestionnaire de modules](/help/sites-administering/package-manager.md).
