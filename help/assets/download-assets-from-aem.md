---
title: Téléchargez des ressources numériques depuis [!DNL Adobe Experience Manager].
description: Learn how to download assets from [!DNL Adobe Experience Manager] and enable or disable the download functionality.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 64c09e454960a40632059a85f0861deed1899b86
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 41%

---


# Download assets from [!DNL Adobe Experience Manager] {#download-assets-from-aem}

Vous pouvez télécharger des ressources, dont des rendus statiques et dynamiques. Alternatively, you can send emails with links to assets directly from [!DNL Adobe Experience Manager Assets]. Les ressources téléchargées sont compressées dans un fichier ZIP. La taille maximale du fichier ZIP compressé est de 1 Go pour la tâche d’exportation. Un maximum de 500 actifs par tâche d’exportation est autorisé.

>[!NOTE]
>
>Les destinataires du courrier électronique doivent être membres du groupe `dam-users` pour accéder au lien de téléchargement ZIP contenu dans le message. Pour télécharger les ressources, ils doivent disposer des autorisations de lancement des workflows qui déclenchent le téléchargement.

Les types de ressources Visionneuses d’images, Visionneuses à 360°, Visionneuses de supports variés et Visionneuses de carrousel ne peuvent pas être téléchargés.

**Pour télécharger des fichiers,**

1. In the upper-left corner of AEM, tap the AEM logo, then in the left rail, tap **[!UICONTROL Navigation]** (Compass icon).
1. On the Navigation page, tap **[!UICONTROL Assets > Files]**.
1. Accédez à un dossier contenant les fichiers à télécharger.
1. Sélectionnez le dossier ou un ou plusieurs fichiers qu’il contient.
1. On the toolbar, tap **[!UICONTROL Download]**.

   ![Options disponibles lors du téléchargement de fichiers à partir de ressources Experience Manager](/help/assets/assets/asset-download1.png)

   *Options de la boîte de dialogue Télécharger.*

1. Dans la boîte de dialogue Télécharger, sélectionnez les options de téléchargement de votre choix.

   | Option de téléchargement | Description |
   |---|---|
   | **[!UICONTROL Créer un dossier distinct pour chaque ressource]** | Sélectionnez cette option pour inclure chaque fichier que vous téléchargez, y compris les fichiers, dans des dossiers enfants imbriqués sous le dossier parent du fichier, dans un dossier sur votre ordinateur local. Lorsque cette option *n’est pas* sélectionnée, la hiérarchie des dossiers est ignorée par défaut et tous les fichiers sont téléchargés dans un dossier de votre ordinateur local. |
   | **[!UICONTROL Courrier électronique]** | Sélectionnez cette option pour envoyer une notification par courrier électronique au destinataire. Les modèles standard de courrier électronique sont disponibles aux emplacements suivants :<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> Les modèles que vous personnalisez lors du déploiement sont disponibles aux emplacements suivants : <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul>Vous pouvez stocker des modèles personnalisés spécifiques au client aux emplacements suivants :<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> |
   | **[!UICONTROL Ressource (s)]** | Sélectionnez cette option pour télécharger le fichier sous sa forme d’origine sans aucun rendu.<br>L’option sous-ressources est disponible si la ressource d’origine comporte des sous-ressources. |
   | **[!UICONTROL Rendu(s)]** | Un rendu est une représentation binaire d’une ressource. Les ressources possèdent une représentation principale, à savoir celle du fichier transféré. Elles peuvent avoir un nombre illimité de représentations. <br> Avec cette option, vous pouvez sélectionner les rendus que vous souhaitez télécharger. Les rendus disponibles dépendent de la ressource que vous avez sélectionnée. |
   | **[!UICONTROL Recadrages intelligents]** | Sélectionnez cette option pour télécharger tous les rendus de recadrage intelligent de la ressource sélectionnée depuis AEM. Un fichier zip contenant les rendus Smart Crop est créé et téléchargé sur votre ordinateur local. |
   | **[!UICONTROL Rendu(s) dynamique(s)]** | Sélectionnez cette option pour générer une série de rendus alternatifs en temps réel. When you select this option, you also select the renditions that you want to create dynamically by selecting from the [Image Preset](image-presets.md) list. <br>En outre, vous pouvez sélectionner la taille et l’unité de mesure, le format, l’espace colorimétrique, la résolution et tout modificateur d’image facultatif, tel que l’inversion de l’image. Cette option n’est disponible que si vous avez [!DNL Dynamic Media] activé. |

1. Dans la boîte de dialogue, appuyez sur **[!UICONTROL Télécharger]**.

## Activation du servlet de téléchargement de ressources {#enable-asset-download-servlet}

The default servlet in [!DNL Experience Manager] allows authenticated users to issue arbitrarily large, concurrent download requests for creating ZIP files of assets visible to them that can overload the server and the network. Pour atténuer les risques d’attaques par déni de service, le composant OSGi `AssetDownloadServlet` est désactivé par défaut pour les instances de publication.

Pour permettre le téléchargement de fichiers depuis votre DAM (par exemple, lorsque vous utilisez un élément comme Asset Share Commons ou une autre implémentation de type portail), activez manuellement le servlet via une configuration OSGi. Adobe recommande de définir la taille de téléchargement autorisée sur la valeur la plus basse possible sans affecter les exigences de téléchargement au quotidien. Une valeur élevée peut avoir une incidence sur les performances.

1. Create a folder with a naming convention that targets the publish runmode (`config.publish`): `/apps/<your-app-name>/config.publish`. Pour définir les propriétés de configuration d’un mode d’exécution, voir Modes d’ [exécution](/help/sites-deploying/configure-runmodes.md#defining-configuration-properties-for-a-run-mode).

1. In the configuration folder, create a file of type `nt:file` named `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`.
1. Remplissez `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` avec les éléments suivants. Définit une taille maximale (en octets) pour le téléchargement en tant que valeur de `asset.download.prezip.maxcontentsize`. L’exemple ci-dessous configure la taille maximale du téléchargement ZIP pour qu’il ne dépasse pas 100 Ko.

   ```conf
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

## Désactivation du servlet de téléchargement de ressources {#disable-asset-download-servlet}

Le `Asset Download Servlet` peut être désactivé sur une instance  Publish en mettant à jour la configuration du dispatcher afin de bloquer toute demande de téléchargement de ressources. [!DNL Experience Manager] Le servlet peut également être désactivé manuellement par l’intermédiaire de la console OSGi.

1. To block asset download requests via a dispatcher configuration, edit the `dispatcher.any` configuration and add a rule to the [filter section](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#defining-a-filter). `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

1. Disable the OSGi component on a Publish instance by navigating to the OSGi Console at `http://[aem_server]:[port]/system/console/components`. Recherchez `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet` et cliquez ensuite sur **[!UICONTROL Désactiver]**.

>[!MORELIKETHIS]
>
>* [Téléchargement de ressources protégées par DRM](drm.md).
>* [Téléchargez des fichiers à l’aide d’une application de bureau Experience Manager sur un ordinateur de bureau](https://helpx.adobe.com/fr/experience-manager/desktop-app/aem-desktop-app.html)Windows ou Mac.
>* [Téléchargement de ressources à l’aide d’Adobe Assets Link depuis les applications Adobe Creative Cloud prises en charge](https://helpx.adobe.com/fr/enterprise/using/manage-assets-using-adobe-asset-link.html).

