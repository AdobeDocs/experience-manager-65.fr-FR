---
title: Installation de la version [!DNL Workfront for Experience Manager enhanced connector]
description: Installation de la version [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Integrations
exl-id: 087bc811-e8f8-4db5-b066-627a9b082f57
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 100%

---

# Installation de la version [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Cliquez ici](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/integrations/workfront-connector-install.html?lang=fr) |
| AEM 6.5 | Cet article |

Avec un accès administrateur dans [!DNL Adobe Experience Manager], vous pouvez installer le connecteur amélioré. Avant de procéder à l’installation, vérifiez la prise en charge de la plateforme et d’autres [conditions préalables pour le connecteur](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>* Adobe nécessite le déploiement et la configuration de [!DNL Adobe Workfront for Experience Manager enhanced connector] uniquement par le biais de partenaires certifiés ou [!DNL Adobe Professional Services]. S’il est déployé et configuré sans partenaire certifié ou sans [!DNL Adobe Professional Services], il n’est pas pris en charge par Adobe.
>
>* Adobe peut publier des mises à jour d’[!DNL Adobe Workfront] et d’[!DNL Adobe Experience Manager] qui rendent ce connecteur redondant ; si cela se produit, les clients peuvent être amenés à cesser d’utiliser ce connecteur.
>
>* Adobe prend en charge les versions 1.7.4 et supérieures du connecteur. Les versions précédentes et personnalisées ne sont pas prises en charge. Pour vérifier la version améliorée du connecteur, accédez au groupe `digital.hoodoo` disponible dans le volet de gauche du [Gestionnaire de packages](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=fr).
>
>* Consultez la section [Examen de certification des partenaires pour Workfront pour le connecteur amélioré Experience Manager Assets](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). Pour plus d’informations sur l’examen, consultez le [Guide d’examen](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).


Pour installer le connecteur, procédez comme suit :

1. Téléchargez le connecteur à partir du lien [[!DNL Software Distribution] ](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip).
1. [Configuration du pare-feu](https://one.workfront.com/s/document-item?bundleId=the-new-workfront-experience&amp;topicId=Content%2FAdministration_and_Setup%2FGet_started-WF_administration%2Fconfigure-your-firewall.html?lang=fr).
1. Sur le répartiteur, autorisez les en-têtes HTTP nommés `authorization`, `username`, et `apikey`. Autorisez les requêtes `GET`, `POST`, et `PUT` à `/bin/workfront-tools`.
1. Assurez-vous que les chemins d’accès suivants n’existent pas dans le référentiel [!DNL Experience Manager] :

   * `/apps/dam/gui/coral/components/admin/schemaforms/formbuilder`
   * `/apps/dam/gui/coral/components/admin/folderschemaforms/formbuilder`
   * `/apps/dam/gui/content/foldermetadataschemaeditor`
   * `/apps/dam/cfm/models/editor/components/datatypeproperties`
   * `/apps/settings/dam/cfm/models/formbuilderconfig`

1. Installez le package téléchargé à l’aide du [!UICONTROL gestionnaire de packages]. Pour savoir comment installer des packages, consultez la [Documentation du gestionnaire de packages](/help/sites-administering/package-manager.md).
1. Créez `wf-workfront-users` dans Groupe d’utilisateurs [!DNL Experience Manager] et attribuez l’autorisation `jcr:all` dans `/content/dam`.

Un utilisateur système `workfront-tools` est créé automatiquement et les autorisations requises sont gérées automatiquement. Toutes les personnes utilisant [!DNL Workfront] et le connecteur amélioré sont automatiquement ajoutées dans le cadre de ce groupe.

## Configuration de la connexion entre [!DNL Experience Manager] et [!DNL Workfront] {#configure-connection}

Pour créer une connexion avec Workfront, procédez comme suit :

1. Dans [!DNL Experience Manager], sélectionnez **[!UICONTROL Outils]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configuration des outils Workfront]**.

1. Sélectionnez `workfront-tools` dans le panneau de gauche et sélectionnez l’option **[!UICONTROL Créer]** dans la zone supérieure droite de la page.

1. Dans la boîte de dialogue **[!UICONTROL Connexion Workfront]**, fournissez les détails requis de votre déploiement [!DNL Workfront], et sélectionnez l’option **[!UICONTROL Connexion à Workfront]**. Une fois la connexion établie, l’intégration personnalisée du document [!DNL Workfront] est créée automatiquement dans l’environnement [!DNL Workfront].

   ![Connexion [!DNL Experience Manager] et [!DNL Workfront]](/help/assets/assets/wf-connection-config.png)

1. Pour vérifier la connexion, accédez-y dans [!DNL Workfront] et vérifiez que la clé API est la même et que la connexion est sur **[!UICONTROL Activé]**. Pour ce faire, sélectionnez **[!UICONTROL Configuration]** > **[!UICONTROL Documents]** > **[!UICONTROL Intégrations personnalisées]** dans [!DNL Workfront].

## Mise à jour de [!DNL Workfront for Experience Manager enhanced connector] {#update-enhanced-connector-for-workfront}

Experience Manager Assets vous permet de mettre à jour [!DNL Workfront for Experience Manager enhanced connector] d’une version précédente à la dernière version.

Pour mettre à jour [!DNL Workfront for Experience Manager enhanced connector] vers la dernière version :

1. Téléchargez la dernière version du connecteur amélioré à partir du lien [[!DNL Software Distribution] ](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip).
1. Installez le package téléchargé à l’aide du [!UICONTROL gestionnaire de packages]. Pour savoir comment installer des packages, consultez la [Documentation du gestionnaire de packages](/help/sites-administering/package-manager.md).
