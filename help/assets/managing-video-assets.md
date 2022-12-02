---
title: Gestion des ressources vidéo
description: Charger, prévisualiser, annoter et publier des ressources vidéo dans [!DNL Adobe Experience Manager].
contentOwner: AG
role: User
feature: Asset Management
exl-id: 21d3e0bd-5955-470a-8ca2-4d995c17eb4c
source-git-commit: 068f6c1c2909c2840e9ad4c0ad295538e543d9c9
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 100%

---

# Gestion des ressources vidéo {#manage-video-assets}

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Cliquez ici](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/manage-video-assets.html?lang=fr) |
| AEM 6.5 | Cet article |
| AEM 6.4 | [Cliquez ici](https://experienceleague.adobe.com/docs/experience-manager-64/assets/managing/managing-video-assets.html?lang=fr) |

Le format vidéo est un élément essentiel des ressources numériques d’une entreprise. [!DNL Adobe Experience Manager] propose des solutions et des fonctionnalités matures pour gérer l’ensemble du cycle de vie de vos ressources vidéo après leur création.

Découvrez comment gérer et modifier les ressources vidéo dans [!DNL Adobe Experience Manager Assets]. Le codage et le transcodage des vidéos, par exemple le transcodage FFmpeg, sont possibles à l’aide de l’intégration [!DNL Dynamic Media].

## Chargement et prévisualisation des ressources vidéo {#upload-and-preview-video-assets}

[!DNL Adobe Experience Manager Assets] génère des aperçus pour les contenus vidéo dotés de l’extension MP4. Si le format du contenu n’est pas MP4, installez le pack FFmpeg pour générer l’aperçu. FFmpeg crée des rendus vidéo du type OGG et MP4. Vous pouvez prévisualiser les rendus dans l’interface utilisateur [!DNL Assets].

1. Dans le dossier Ressources numériques ou ses sous-dossiers, accédez à l’emplacement où vous souhaitez ajouter les ressources numériques.
1. Pour charger le contenu, cliquez sur **[!UICONTROL Créer]** dans la barre d’outils, puis sélectionnez **[!UICONTROL Fichiers]**. Vous pouvez également faire glisser un fichier vers l’interface utilisateur. Voir [Ressources chargées](manage-assets.md#uploading-assets) pour plus d’informations.
1. Pour prévisualiser une vidéo en mode carte, cliquez sur l’option **[!UICONTROL Lecture]** ![option de lecture](assets/do-not-localize/play.png) de la ressource vidéo. Vous pouvez suspendre ou lire une vidéo en mode Carte uniquement. Les options [!UICONTROL Lecture] et [!UICONTROL Pause] ne sont pas disponibles dans la vue de liste.

1. Pour prévisualiser la vidéo dans la page des détails de la ressource, cliquez sur **[!UICONTROL Modifier]** sur la carte. La vidéo se joue dans le lecteur vidéo natif du navigateur. Vous pouvez lire, suspendre, afficher la vidéo en plein écran et en contrôler le volume.

   ![Contrôles de lecture vidéo](assets/video-playback-controls.png)

## Configuration pour charger des ressources d’une taille supérieure à 2 Go {#configuration-to-upload-assets-that-are-larger-than-gb}

Par défaut, [!DNL Assets] ne vous permet pas de charger des contenus dont le volume est supérieur à 2 Go en raison de la limitation de la taille des fichiers. Néanmoins, vous pouvez contourner cette limite en accédant à CRXDE Lite et en créant un nœud dans le répertoire `/apps`. Le nœud doit comporter le même nom, la même structure de répertoire et des propriétés comparables.

Outre la configuration d’[!DNL Assets], modifiez les configurations suivantes pour charger des fichiers volumineux :

* Augmentez le délai d’expiration du jeton. Consultez la section [!UICONTROL Servlet CSRF Granite Adobe] dans la console web à l’adresse `https://[aem_server]:[port]/system/console/configMgr`. Pour plus d’informations, consultez la section [Protection CSRF](/help/sites-developing/csrf-protection.md).
* Augmentez la configuration `receiveTimeout` du répartiteur. Pour plus d’informations, voir [Configuration du répartiteur Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=fr#renders-options).

>[!NOTE]
>
>L’interface utilisateur classique d’[!DNL Experience Manager] ne comporte pas de limite de taille de fichier à 2 Go. Par ailleurs, le workflow de bout en bout pour des vidéos volumineuses n’est pas entièrement pris en charge.

Pour configurer une limite de taille de fichier supérieure, procédez comme suit dans le répertoire `/apps`.

1. Dans [!DNL Experience Manager], cliquez sur **[!UICONTROL Outils]** > **[!UICONTROL Général]** > **[!UICONTROL CRXDE Lite]**.
1. Dans CRXDE Lite, accédez à `/libs/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`. Pour afficher la fenêtre du répertoire, appuyez sur `>>`.
1. Dans la barre d’outils, cliquez sur **[!UICONTROL Nœud de recouvrement]**. Vous pouvez également sélectionner **[!UICONTROL Nœud de recouvrement]** dans le menu contextuel.
1. Dans la boîte de dialogue **[!UICONTROL Nœud de recouvrement]**, cliquez sur **[!UICONTROL OK]**.

   ![Nœud de recouvrement](assets/overlay-node-path.png)

1. Actualisez le navigateur. Le nœud de recouvrement `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload` est sélectionné.
1. Dans l’onglet **[!UICONTROL Propriétés]**, saisissez la valeur appropriée en octets pour définir la taille maximale souhaitée. Par exemple, pour augmenter la taille limite à 30 Go, entrez la valeur `32212254720`.

1. Dans la barre d’outils, cliquez sur **[!UICONTROL Tout enregistrer]**.
1. Dans [!DNL Experience Manager], cliquez sur **[!UICONTROL Outils]** > **[!UICONTROL Opérations]** > **[!UICONTROL Console web]**.
1. Dans la page [!UICONTROL Bundles de la console web [!DNL Adobe Experience Manager]], dans la colonne Nom de la table, recherchez et cliquez sur **[!UICONTROL Gestionnaire des tâches du processus externe de workflow Adobe Granite]**.
1. Dans la page [!UICONTROL Gestionnaire des tâches du processus externe de workflow Adobe Granite], définissez les secondes pour les champs de **[!UICONTROL dépassement de délai par défaut]** et de **[!UICONTROL délai dépassé maximum]** sur `18000` (cinq heures). Cliquez sur **[!UICONTROL Enregistrer]**.
1. Dans [!DNL Experience Manager], cliquez sur **[!UICONTROL Outils]** > **[!UICONTROL Workflow]** > **[!UICONTROL Modèles]**.
1. Dans la page Modèles de workflow, sélectionnez **[!UICONTROL Vidéo de codage Dynamic Media]**, puis cliquez sur **[!UICONTROL Modifier]**.
1. Dans la page du workflow, appuyez deux fois sur le composant **[!UICONTROL Processus de service vidéo Dynamic Media]**.
1. Dans la boîte de dialogue [!UICONTROL Propriétés des étapes], sous l’onglet **[!UICONTROL Commun]**, développez les **Paramètres avancés**.
1. Dans le champ **[!UICONTROL Temporisation]**, spécifiez une valeur de `18000`, puis cliquez sur **[!UICONTROL OK]** pour revenir à la page de workflow **[!UICONTROL Vidéo de codage de Dynamic Media]**.
1. Dans la partie supérieure de la page, sous le titre de la page [!UICONTROL Vidéo de codage de Dynamic Media], appuyez sur **[!UICONTROL Enregistrer]**.

## Publication de ressources vidéo {#publish-video-assets}

Après la publication, vous pouvez inclure les ressources vidéo dans une page web sous la forme d’une URL ou les intégrer directement. Pour plus d’informations, voir [Publication de ressources Dynamic Media](/help/assets/publishing-dynamicmedia-assets.md).

## Annotation de ressources vidéo {#annotate-video-assets}

1. Dans la console [!DNL Assets], sélectionnez **[!UICONTROL Modifier]** sur la carte de ressources pour afficher la page de détails de la ressource.
1. Pour lire la vidéo, cliquez sur **[!UICONTROL Aperçu]**.
1. Pour annoter la vidéo, cliquez sur **[!UICONTROL Annoter]**. Une annotation est ajoutée à ce moment de la vidéo. Lorsque vous annotez, vous pouvez dessiner sur le canevas et inclure un commentaire avec le dessin. Les commentaires sont automatiquement enregistrés. Pour quitter l’assistant d’annotation, cliquez sur **[!UICONTROL Fermer]**.

   ![Dessin et annotation sur une image vidéo](assets/annotate-video.png)

1. Pour passer à un point spécifique de la vidéo, indiquez le moment en secondes dans le champ **texte** et cliquez sur **Aller**. Par exemple, pour sauter les 20 premières secondes de la vidéo, saisissez 20 dans le champ texte.

   ![Recherche d’une heure dans une vidéo à ignorer pendant les secondes spécifiées](assets/seek-in-video.png)

1. Pour l’afficher dans la chronologie, cliquez sur une annotation. Pour supprimer l’annotation de la chronologie, cliquez sur **[!UICONTROL Supprimer]**.

   ![Affichage des annotations et des détails dans la chronologie](assets/timeline-view-annotation.png)

>[!MORELIKETHIS]
>
>* [Gestion des ressources numériques dans Experience Manager Assets](/help/assets/manage-assets.md)
>* [Gestion des collections dans Experience Manager Assets](/help/assets/manage-collections.md)
>* [Documentation vidéo de Dynamic Media](/help/assets/video.md).

