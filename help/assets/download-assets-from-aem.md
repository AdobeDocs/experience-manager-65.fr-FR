---
title: Téléchargement de ressources à partir d’AEM
description: Découvrez comment télécharger des ressources à partir d’AEM et activer ou désactiver la fonctionnalité de téléchargement.
contentOwner: AG
translation-type: tm+mt
source-git-commit: e71b87b12d45bf12f29af917fddebeddedb18056

---


# Téléchargement de ressources à partir d’AEM {#download-assets-from-aem}

Vous pouvez télécharger des ressources, dont des rendus statiques et dynamiques. Vous pouvez également envoyer des liens vers des ressources par courrier électronique, directement à partir d’AEM Assets. Les ressources téléchargées sont compressées dans un fichier ZIP. La taille maximale du fichier ZIP compressé est de 1 Go pour la tâche d’exportation. 500 ressources, au maximum, sont autorisées par tâche d’exportation.

>[!NOTE]
>
>Recipients of emails must be members of the `dam-users` group to access the ZIP download link in the email message. Pour télécharger les ressources, ils doivent disposer des autorisations de lancement des workflows qui déclenchent le téléchargement.

To download assets, navigate to an asset, select the asset, and tap **[!UICONTROL Download]** from the toolbar. Spécifiez vos options de téléchargement dans la boîte de dialogue qui s’affiche.

Les types de ressources Visionneuses d’images, Visionneuses à 360°, Visionneuses de supports variés et Visionneuses de carrousel ne peuvent pas être téléchargés.

![Options disponibles lors du téléchargement de ressources à partir d’AEM Assets](assets/asset_download_dialog.png)

*Figure : Options disponibles lors du téléchargement de fichiers à partir d’AEM Assets*

Vous trouverez ci-dessous les options d’exportation/de téléchargement disponibles. Les rendus dynamiques sont propres à Dynamic Media et vous permettent de générer des rendus à la volée, en plus de la ressource que vous avez sélectionnée (cette option est uniquement disponible lorsque Dynamic Media est activé).

| Options d’exportation ou de téléchargement | Descriptions |
|---|---|
| [!UICONTROL Assets] | Sélectionnez cette option pour télécharger la ressource dans son format d’origine sans aucun rendu. |
| [!UICONTROL Rendus] | Un rendu est une représentation binaire d’une ressource. Les ressources possèdent une représentation principale, à savoir celle du fichier transféré. Elles peuvent avoir un nombre illimité de représentations. <br> Avec cette option, vous pouvez sélectionner les rendus que vous souhaitez télécharger. Les rendus disponibles dépendent de la ressource sélectionnée. |
| [!UICONTROL Rendus dynamiques] | Un rendu dynamique génère d’autres rendus à la volée. When you select this option, you also select the renditions you want to create dynamically by selecting from the [Image Preset](image-presets.md) list. <br>De plus, vous pouvez sélectionner la taille, l’unité de mesure, le format, l’espace colorimétrique, la résolution, ainsi que les éventuels modificateurs d’image (pour inverser l’image, par exemple). |
| [!UICONTROL Courriel] | Une notification électronique est envoyée à l’utilisateur. Les modèles standard de courrier électronique sont disponibles aux emplacements suivants :<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`</li></ul> Les modèles que vous personnalisez lors du déploiement doivent se trouver à ces emplacements : <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`</li></ul>Vous pouvez stocker des modèles personnalisés spécifiques au client à ces emplacements :<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`</li></ul> |
| [!UICONTROL Créer un dossier distinct pour chaque ressource] | Sélectionnez cette option pour préserver la hiérarchie des dossiers lors du téléchargement des ressources. Par défaut, la hiérarchie des dossiers est ignorée et toutes les ressources sont téléchargées dans un dossier de votre système local. |

L’option des rendus d’option est disponible si la ressource comporte des rendus. L’option Sous-ressources est disponible si la ressource comporte des sous-ressources.

Lorsque vous sélectionnez un dossier à télécharger, l’ensemble de la hiérarchie des ressources sous ce dossier est téléchargé. Pour inclure chaque ressource que vous téléchargez (dont les ressources dans les dossiers enfants imbriqués sous le dossier parent) dans un dossier individuel, sélectionnez **[!UICONTROL Créer un dossier distinct pour chaque ressource]**.

## Enable asset download servlet {#enable-asset-download-servlet}

Le servlet par défaut d’AEM permet aux utilisateurs authentifiés d’émettre des demandes de téléchargement simultanées de grande taille pour créer des fichiers ZIP de ressources visibles, susceptibles de surcharger le serveur et le réseau. To mitigate potential DoS risks caused by this feature, `AssetDownloadServlet` OSGi component is disabled by default for publish instances.

Pour permettre le téléchargement de fichiers depuis votre DAM (par exemple, lorsque vous utilisez un élément comme Asset Share Commons ou une autre implémentation de type portail), activez manuellement le servlet via une configuration OSGi. Adobe recommande de définir la taille de téléchargement autorisée sur la valeur la plus basse possible sans affecter les exigences de téléchargement au quotidien. Une valeur élevée peut avoir une incidence sur les performances.

1. Create a folder with a naming convention that targets the publish runmode, that is, `config.publish`:

   `/apps/<your-app-name>/config.publish`

   Pour définir les propriétés de configuration d’un mode d’exécution, voir Modes d’ [exécution](/help/sites-deploying/configure-runmodes.md#defining-configuration-properties-for-a-run-mode) pour plus d’informations.

1. In the config folder, create a new file of type `nt:file` named `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`.
1. Populate `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` with the following. Définit une taille maximale (en octets) pour le téléchargement en tant que valeur de `asset.download.prezip.maxcontentsize`. L’exemple ci-dessous configure la taille maximale du téléchargement ZIP pour qu’il ne dépasse pas 100 Ko.

   ```
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

## Disable asset download servlet {#disable-asset-download-servlet}

The `Asset Download Servlet` can be disabled on an AEM Publish instances by updating the dispatcher configuration to block any asset download requests. Le servlet peut également être désactivé manuellement par l’intermédiaire de la console OSGi.

1. Pour bloquer les requêtes de téléchargement de ressources via une configuration de Dispatcher, modifiez la configuration `dispatcher.any` et ajoutez une nouvelle règle à la [section /filter](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#defining-a-filter).

   `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

1. You can manually disable the OSGi component on a Publish instance, by navigating to the OSGi Console at `<aem-host>/system/console/components`. Locate `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet` and click **[!UICONTROL Disable]**.

>[!MORELIKETHIS]
>
>* [Téléchargement de ressources protégées par DRM](drm.md)
>* [Téléchargement de fichiers à l’aide de l’application de bureau AEM sous Windows ou Mac](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html)
>* [Téléchargement de fichiers à l’aide d’Adobe Assets Link depuis les applications Adobe Creative Cloud prises en charge](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html)