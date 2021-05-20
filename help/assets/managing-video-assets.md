---
title: Gestion des ressources vidéo
description: Charger, prévisualiser, annoter et publier des ressources vidéo dans [!DNL Adobe Experience Manager].
contentOwner: AG
role: Business Practitioner
feature: Gestion des ressources
exl-id: 21d3e0bd-5955-470a-8ca2-4d995c17eb4c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '809'
ht-degree: 58%

---

# Gestion des ressources vidéo {#manage-video-assets}

Le format vidéo est un élément essentiel des ressources numériques d’une entreprise. [!DNL Adobe Experience Manager] propose des solutions et des fonctionnalités matures pour gérer l’ensemble du cycle de vie de vos ressources vidéo après leur création.

Découvrez comment gérer et modifier les ressources vidéo dans [!DNL Adobe Experience Manager Assets]. Le codage et le transcodage vidéo, par exemple, le transcodage FFmpeg, sont possibles à l’aide de l’intégration [!DNL Dynamic Media].

## Chargement et prévisualisation des ressources vidéo {#upload-and-preview-video-assets}

[!DNL Adobe Experience Manager Assets] génère des aperçus pour les contenus vidéo dotés de l’extension MP4. Si le format de la ressource n’est pas MP4, installez le pack FFmpeg pour générer un aperçu. FFmpeg crée des rendus vidéo de type OGG et MP4. Vous pouvez prévisualiser les rendus dans l’interface utilisateur [!DNL Assets].

1. Dans le dossier Ressources numériques ou ses sous-dossiers, accédez à l’emplacement où vous souhaitez ajouter les ressources numériques.
1. Pour charger le contenu, cliquez sur **[!UICONTROL Créer]** dans la barre d’outils, puis sélectionnez **[!UICONTROL Fichiers]**. Vous pouvez également faire glisser un fichier vers l’interface utilisateur. Voir [Ressources chargées](manage-assets.md#uploading-assets) pour plus d’informations.
1. Pour prévisualiser une vidéo en mode Carte, cliquez sur l’option **[!UICONTROL Lecture]** ![Lecture](assets/do-not-localize/play.png) de la ressource vidéo. Vous pouvez suspendre ou lire une vidéo en mode Carte uniquement. Les options [!UICONTROL Lecture] et [!UICONTROL Pause] ne sont pas disponibles dans la vue de liste.

1. Pour prévisualiser la vidéo dans la page des détails de la ressource, cliquez sur **[!UICONTROL Modifier]** sur la carte. La vidéo se joue dans le lecteur vidéo natif du navigateur. Vous pouvez lire, suspendre, afficher la vidéo en plein écran et en contrôler le volume.

   ![Contrôles de lecture vidéo](assets/video-playback-controls.png)

## Configuration pour télécharger des ressources d’une taille supérieure à 2 Go {#configuration-to-upload-assets-that-are-larger-than-gb}

Par défaut, [!DNL Assets] ne permet pas de charger des ressources dont la taille est supérieure à 2 Go en raison d’une limite de taille de fichier. Néanmoins, vous pouvez contourner cette limite en accédant à CRXDE Lite et en créant un nœud dans le répertoire `/apps`. Le nœud doit comporter le même nom, la même structure de répertoire et des propriétés comparables.

En plus de la configuration [!DNL Assets], modifiez les configurations suivantes pour charger des ressources volumineuses :

* Augmentez le délai d’expiration du jeton. Voir [!UICONTROL Adobe du servlet CSRF Granite] dans la console web à l’adresse `https://[aem_server]:[port]/system/console/configMgr`. Pour plus d’informations, voir [Protection CSRF](/help/sites-developing/csrf-protection.md).
* Augmentez la configuration `receiveTimeout` du répartiteur. Pour plus d’informations, voir [Configuration du répartiteur Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#renders-options).

>[!NOTE]
>
>[!DNL Experience Manager] L’interface utilisateur classique ne présente pas de limite de taille de fichier de 2 Go. Par ailleurs, le processus de bout en bout pour des vidéos volumineuses n’est pas entièrement pris en charge.

Pour configurer une limite de taille de fichier supérieure, procédez comme suit dans le répertoire `/apps`.

1. Dans [!DNL Experience Manager], cliquez sur **[!UICONTROL Outils]** > **[!UICONTROL Général]** > **[!UICONTROL CRXDE Lite]**.
1. Dans CRXDE Lite, accédez à `/libs/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`. Pour afficher la fenêtre du répertoire, cliquez sur `>>`.
1. Dans la barre d’outils, cliquez sur le **[!UICONTROL noeud de recouvrement]**. Vous pouvez également sélectionner **[!UICONTROL Nœud de recouvrement]** dans le menu contextuel.
1. Dans la boîte de dialogue **[!UICONTROL Noeud de recouvrement]**, cliquez sur **[!UICONTROL OK]**.

   ![Nœud de recouvrement](assets/overlay-node-path.png)

1. Actualisez le navigateur. Le nœud de recouvrement `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload` est sélectionné.
1. Dans l’onglet **[!UICONTROL Propriétés]**, saisissez la valeur appropriée en octets pour définir la taille maximale souhaitée. Par exemple, pour augmenter la taille limite à 30 Go, entrez la valeur `32212254720`.

1. Dans la barre d’outils, cliquez sur **[!UICONTROL Enregistrer tout]**.
1. Dans [!DNL Experience Manager], cliquez sur **[!UICONTROL Outils]** > **[!UICONTROL Opérations]** > **[!UICONTROL Console web]**.
1. Sur la page [!DNL Adobe Experience Manager] [!UICONTROL Lots de la console web], dans la colonne Nom de la table, recherchez et cliquez sur **[!UICONTROL Adobe Gestionnaire de tâches de processus externe de workflow Granite]**.
1. Sur la page [!UICONTROL Adobe du gestionnaire des tâches de processus externe de processus Granite] , définissez les secondes pour les champs **[!UICONTROL Délai d’expiration par défaut]** et **[!UICONTROL Délai d’expiration maximal]** sur `18000` (cinq heures). Cliquez sur **[!UICONTROL Enregistrer]**.
1. Dans [!DNL Experience Manager], cliquez sur **[!UICONTROL Outils]** > **[!UICONTROL Workflow]** > **[!UICONTROL Modèles]**.
1. Sur la page Modèles de processus, sélectionnez **[!UICONTROL Vidéo de codage Dynamic Media]**, puis cliquez sur **[!UICONTROL Modifier]**.
1. Sur la page du processus, double-cliquez sur le composant **[!UICONTROL Processus de service vidéo Dynamic Media]** .
1. Dans la boîte de dialogue [!UICONTROL Propriétés des étapes], sous l’onglet **[!UICONTROL Commun]**, développez **Paramètres avancés**.
1. Dans le champ **[!UICONTROL Délai d’expiration]** , spécifiez une valeur de `18000`, puis cliquez sur **[!UICONTROL OK]** pour revenir à la page de workflow **[!UICONTROL Vidéo de codage Dynamic Media]** .
1. Près de la partie supérieure de la page, sous le titre de la page [!UICONTROL Vidéo de codage Dynamic Media], cliquez sur **[!UICONTROL Enregistrer]**.

## Publication de ressources vidéo {#publish-video-assets}

Après la publication, vous pouvez inclure les ressources vidéo dans une page web sous la forme d’une URL ou les intégrer directement. Pour plus d’informations, voir [Publication de ressources Dynamic Media](/help/assets/publishing-dynamicmedia-assets.md).

## Annotation de ressources vidéo {#annotate-video-assets}

1. Dans la console [!DNL Assets], sélectionnez **[!UICONTROL Modifier]** sur la carte de ressources pour afficher la page de détails de la ressource.
1. Pour lire la vidéo, cliquez sur **[!UICONTROL Aperçu]**.
1. Pour annoter la vidéo, cliquez sur **[!UICONTROL Annoter]**. Une annotation est ajoutée à ce moment de la vidéo. Lorsque vous annotez, vous pouvez dessiner sur le canevas et inclure un commentaire avec le dessin. Les commentaires sont automatiquement enregistrés. Pour quitter l’assistant d’annotation, cliquez sur **[!UICONTROL Fermer]**.

   ![Dessin et annotation sur une image vidéo](assets/annotate-video.png)

1. Pour passer à un point spécifique de la vidéo, indiquez le moment en secondes dans le champ **texte** et cliquez sur **Aller**. Par exemple, pour sauter les 20 premières secondes de la vidéo, saisissez 20 dans le champ texte.

   ![Recherche d’une heure dans une vidéo à ignorer pendant les secondes spécifiées](assets/seek-in-video.png)

1. Pour l’afficher dans la chronologie, cliquez sur une annotation. Pour supprimer l’annotation de la chronologie, cliquez sur **[!UICONTROL Supprimer]**.

   ![Affichage des annotations et des détails dans la chronologie](assets/timeline-view-annotation.png)

>[!MORELIKETHIS]
>
>* [Gestion des ressources numériques dans Experience Manager Assets](/help/assets/manage-assets.md)
* [Gestion des collections dans Experience Manager Assets](/help/assets/manage-collections.md)
* [Documentation vidéo de Dynamic Media](/help/assets/video.md).

