---
title: Téléchargement de ressources
description: Découvrez comment télécharger des ressources à partir de [!DNL Adobe Experience Manager] et activez ou désactivez la fonctionnalité de téléchargement.
contentOwner: AG
role: User
feature: Asset Management,Asset Distribution
exl-id: 6bda9e52-5a6e-446e-99c7-96793482c190
source-git-commit: 068f6c1c2909c2840e9ad4c0ad295538e543d9c9
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 68%

---

# Téléchargement de ressources depuis [!DNL Adobe Experience Manager] {#download-assets-from-aem}

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Cliquez ici.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/download-assets-from-aem.html?lang=en) |
| AEM 6.5 | Cet article |
| AEM 6.4 | [Cliquez ici.](https://experienceleague.adobe.com/docs/experience-manager-64/assets/managing/download-assets-from-aem.html?lang=en) |

Vous pouvez télécharger des ressources, dont des rendus statiques et dynamiques. Vous pouvez également envoyer des liens vers des ressources par courrier électronique, directement depuis [!DNL Adobe Experience Manager Assets]. Les ressources téléchargées sont compressées dans un fichier ZIP. La taille maximale du fichier ZIP compressé est de 1 Go pour la tâche d’exportation. Un maximum de 500 ressources par tâche d’exportation est autorisé.

>[!NOTE]
>
>Tout utilisateur disposant d’autorisations de lecture sur `/var/dam/share` L’emplacement peut accéder au lien de téléchargement partagé dans le message électronique.
>
>Tout utilisateur disposant d’autorisations de lecture sur `/var/dam/jobs/download` L’emplacement peut télécharger des ressources.
>
>Les types de ressources (visionneuses d’images, visionneuses à 360°, visionneuses de médias mixtes et visionneuses de carrousel) ne peuvent pas être téléchargés.

<!--
OLD content of the above NOTE, changed wrt CQDOC-18661.
>The email recipients must be members of the `dam-users` group to access the ZIP download link in the email message.
>
-->

**Pour télécharger des ressources, procédez comme suit :**

1. Dans le coin supérieur gauche, cliquez sur le logo. Dans le rail de gauche, cliquez sur **[!UICONTROL Navigation]**.
1. Sur le [!UICONTROL Navigation] page, cliquez sur **[!UICONTROL Ressources]** > **[!UICONTROL Fichiers]**.
1. Accédez à un dossier contenant les ressources à télécharger.
1. Sélectionnez le dossier ou une ou plusieurs ressources qu’il contient.
1. Dans la barre d’outils, cliquez sur **[!UICONTROL Télécharger]**.
1. Dans la boîte de dialogue Télécharger, sélectionnez les options de téléchargement de votre choix.

   | Option d’exportation ou de téléchargement | Description |
   |---|---|
   | **[!UICONTROL Créer un dossier distinct pour chaque ressource]** | Sélectionnez cette option pour inclure chaque ressource que vous téléchargez (y compris les ressources dans des dossiers enfants imbriqués sous le dossier parent de la ressource) dans un dossier sur votre ordinateur local. Lorsque cette option n’est pas sélectionnée, par défaut, la hiérarchie de dossiers est ignorée et toutes les ressources sont téléchargées dans un dossier de votre ordinateur local. |
   | **[!UICONTROL Courrier électronique]** | Une notification électronique est envoyée à l’utilisateur. Les modèles standard d’email sont disponibles aux emplacements suivants :<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> Les modèles que vous personnalisez lors du déploiement sont disponibles aux emplacements suivants : <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul>Vous pouvez stocker des modèles personnalisés spécifiques au client à ces emplacements :<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> |
   | **[!UICONTROL Ressource(s)]** | Sélectionnez cette option pour télécharger la ressource dans son format d’origine sans aucun rendu.<br>L’option Sous-ressources est disponible si la ressource d’origine comporte des sous-ressources. |
   | **[!UICONTROL Rendu(s)]** | Un rendu est une représentation binaire d’une ressource. Les ressources possèdent une représentation principale, à savoir celle du fichier transféré. Elles peuvent avoir un nombre illimité de représentations. <br> Avec cette option, vous pouvez sélectionner les rendus que vous souhaitez télécharger. Les rendus disponibles dépendent de la ressource sélectionnée. L’option est disponible si la ressource comporte des rendus. |
   | **[!UICONTROL Recadrages intelligents]** | Sélectionnez cette option pour télécharger tous les rendus de recadrage intelligent de la ressource sélectionnée depuis AEM. Un fichier zip contenant les rendus de recadrage intelligent est créé et téléchargé sur votre ordinateur local. |
   | **[!UICONTROL Rendu(s) dynamique(s)]** | Sélectionnez cette option pour générer une série de rendus alternatifs en temps réel. Lorsque vous sélectionnez cette option, vous sélectionnez également les rendus à créer dynamiquement dans la liste [Paramètre d’image prédéfini](image-presets.md). <br>De plus, vous pouvez sélectionner la taille, l’unité de mesure, le format, l’espace colorimétrique, la résolution, ainsi que les éventuels modificateurs d’image (pour inverser l’image, par exemple). Cette option n’est disponible que si vous avez activé [!DNL Dynamic Media]. |

1. Dans la boîte de dialogue, cliquez sur **[!UICONTROL Télécharger]**.

Lorsque vous sélectionnez un dossier à télécharger, l’ensemble de la hiérarchie des ressources sous ce dossier est téléchargé. Pour inclure chaque ressource que vous téléchargez (dont les ressources dans les dossiers enfants imbriqués sous le dossier parent) dans un dossier individuel, sélectionnez **[!UICONTROL Créer un dossier distinct pour chaque ressource]**.

## Activation du servlet de téléchargement de ressources {#enable-asset-download-servlet}

Le servlet par défaut dans [!DNL Experience Manager] permet aux utilisateurs authentifiés d’émettre des demandes de téléchargement simultanées arbitrairement volumineuses pour créer des fichiers ZIP de ressources visibles qui peuvent surcharger le serveur et le réseau. Pour atténuer les risques d’attaques par déni de service, le composant OSGi `AssetDownloadServlet` est désactivé par défaut pour les instances de publication.

Pour permettre le téléchargement de fichiers depuis votre DAM (par exemple, lorsque vous utilisez un élément comme Asset Share Commons ou une autre implémentation de type portail), activez manuellement le servlet via une configuration OSGi. Adobe recommande de définir la taille de téléchargement autorisée sur la valeur la plus basse possible sans affecter les exigences de téléchargement au quotidien. Une valeur élevée peut avoir une incidence sur les performances.

1. Créez un dossier avec une convention d’affectation des noms qui cible le mode d’exécution de publication (`config.publish`) : `/apps/<your-app-name>/config.publish`. Pour définir les propriétés de configuration d’un mode d’exécution, voir [Modes d’exécution](/help/sites-deploying/configure-runmodes.md#defining-configuration-properties-for-a-run-mode).
1. Dans le dossier de configuration, créez un fichier de type `nt:file` named `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`.
1. Remplissez `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` avec les éléments suivants. Définit une taille maximale (en octets) pour le téléchargement en tant que valeur de `asset.download.prezip.maxcontentsize`. L’exemple ci-dessous configure la taille maximale du téléchargement ZIP pour qu’il ne dépasse pas 100 Ko.

   ```conf
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

Par défaut, pour `GET` demandes de téléchargement de fichiers, [!DNL Experience Manager] applique une limite de 50 Mo à la taille de téléchargement de l’archive ZIP. Téléchargements lancés via `POST` Les demandes ou l’interface utilisateur ne sont pas affectées par cette limite.

## Désactivation du servlet de téléchargement de ressources {#disable-asset-download-servlet}

Le `Asset Download Servlet` peut être désactivé sur les instances de publication [!DNL Experience Manager] en mettant à jour la configuration du Dispatcher afin de bloquer toute demande de téléchargement de ressources. Le servlet peut également être désactivé manuellement par l’intermédiaire de la console OSGi.

1. Pour bloquer les demandes de téléchargement de ressources via une configuration de Dispatcher, modifiez la variable `dispatcher.any` et ajoutez une règle à la [section filter](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#defining-a-filter). `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

1. Pour désactiver le composant OSGi sur une instance de publication, accédez à la console OSGi à l’adresse `http://[aem_server]:[port]/system/console/components`. Recherchez `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet` et cliquez ensuite sur **[!UICONTROL Désactiver]**.

>[!MORELIKETHIS]
>
>* [Téléchargement de ressources à l’aide de Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html?lang=fr)
>* [Téléchargement de ressources protégées par DRM](drm.md).
>* [Téléchargement de ressources à l’aide de l’appli de bureau Experience Manager sur un poste de travail Windows ou Mac](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=fr#download-assets).
>* [Téléchargement de ressources à l’aide d’Adobe Assets Link depuis les applications Adobe Creative Cloud prises en charge](https://helpx.adobe.com/fr/enterprise/using/manage-assets-using-adobe-asset-link.html).

