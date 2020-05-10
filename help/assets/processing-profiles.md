---
title: Profils de traitement des métadonnées, des images et des vidéos
description: Un profil est un jeu de règles concernant les options à appliquer aux ressources téléchargées dans un dossier. Spécifiez le profil de métadonnées et le profil de codage vidéo à appliquer aux ressources vidéo que vous chargez. Pour les ressources d’images, vous pouvez également spécifier le profil d’imagerie qui doit leur être appliqué afin de les recadrer correctement.
uuid: 6ded2a2f-a0d3-4f43-af97-02fbc0902c25
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
discoiquuid: b555bf0c-44cb-4fbf-abc4-15971663904d
docset: aem65
translation-type: tm+mt
source-git-commit: 5f3af7041029a1b4dd1cbb4c65bd488b62c7e10c
workflow-type: tm+mt
source-wordcount: '1369'
ht-degree: 97%

---


# Profils de traitement des métadonnées, des images et des vidéos{#profiles-for-processing-metadata-images-and-videos}

Un profil est une recette indiquant les options à appliquer aux ressources qui sont chargées dans un dossier. Par exemple, vous pouvez spécifier le profil de métadonnées et le profil de codage vidéo à appliquer aux ressources vidéo que vous chargez, ou le profil d’image à appliquer aux ressources image afin de les recadrer correctement.

Ces règles peuvent inclure l’ajout de métadonnées, le recadrage intelligent des images ou la mise en place de profils de codage vidéo. AEM vous permet de créer trois types de profils, qui sont abordés en détail sous les liens suivants :

* [Profils de métadonnées](/help/assets/metadata-profiles.md)
* [Profils d’image](/help/assets/image-profiles.md)
* [Profils vidéo](/help/assets/video-profiles.md)

Vous devez disposer de droits d’administrateur pour créer, modifier et supprimer des profils vidéo, de métadonnées ou d’image.

Une fois votre profil vidéo, de métadonnées ou d’image créé, vous pouvez l’affecter à un ou plusieurs dossiers utilisés comme destination des ressources qui viennent d’être chargées.

Un élément à connaître lorsque l’on utilise les profils dans AEM est qu’ils sont attribués aux dossiers. Un profil contient des paramètres sous la forme de profils de métadonnées, avec des profils vidéo ou des profils d’image. Ces paramètres traitent le contenu d’un dossier et de tous ses sous-dossiers. Aussi, la façon dont vous nommez les fichiers ou les dossiers, organisez les sous-dossiers ou gérez les fichiers au sein des dossiers a un impact significatif sur le traitement des ressources par les profils.
Grâce à des stratégies d’attribution de nom aux fichiers et dossiers cohérentes et adéquates et à une bonne pratique en matière de métadonnées, vous pouvez tirer pleinement parti de votre collection de ressources numériques et vous assurer que les bons fichiers sont traités par le profil adéquat.

>[!NOTE]
>
>Les ressources que vous déplacez d’un dossier à un autre ne sont pas retraitées. Par exemple, supposons que vous ayez un dossier 1 auquel le profil A est affecté et un dossier 2 auquel le profil B est affecté. Si vous déplacez des ressources du dossier 1 au dossier 2, les ressources déplacées conservent leur traitement d’origine du dossier 1.
>
>C’est également le cas lorsque vous déplacez des ressources entre deux dossiers auxquels le même profil est affecté.

## Retraitement des ressources dans un dossier {#reprocessing-assets}

>[!NOTE]
>
>S’applique au mode *Contenu multimédia* dynamique - Scene7 uniquement dans AEM 6.4.6.0 ou version ultérieure.

Vous pouvez retraiter des ressources dans un dossier qui comporte déjà un profil de traitement existant que vous avez modifié ultérieurement.

Supposons que vous ayez créé un profil Image et que vous l’ayez affecté à un dossier. Le profil Image a été automatiquement appliqué aux ressources d’image que vous avez chargées dans le dossier. Cependant, vous décidez par la suite d’ajouter un nouveau rapport de recadrage intelligent au profil. Désormais, au lieu de devoir sélectionner et charger à nouveau les ressources dans le dossier, il vous suffit d’exécuter le workflow *Scene7 : Retraiter les ressources*.

Vous pouvez exécuter le workflow de retraitement sur une ressource pour laquelle le traitement a échoué la première fois. Ainsi, même si vous n’avez ni modifié ni appliqué un profil de traitement, vous pouvez toujours exécuter, à tout moment, le workflow de retraitement sur un dossier de ressources.

Vous pouvez, au besoin, régler la taille de lot du workflow de retraitement sur une valeur comprise entre 50 (valeur par défaut) et 1 000 ressources. Lorsque vous exécutez le workflow _Scene7 : Retraiter les ressources_ sur un dossier, les ressources sont regroupées par lots, puis envoyées au serveur Dynamic Media en vue du traitement. Après le traitement, les métadonnées de chaque ressource de l’ensemble du jeu de lots sont mises à jour dans AEM. Si la taille du lot est très importante, le traitement peut être retardé. Si le lot est trop petit, cela peut entraîner un trop grand nombre d’allers-retours avec le serveur Dynamic Media.

Voir [Réglage de la taille du lot du workflow de retraitement](#adjusting-load).

>[!NOTE]
>
>Si vous effectuez une migration groupée des ressources de Dynamic Media Classic vers AEM, vous devez activer l’agent de réplication Migration sur le serveur Dynamic Media. Une fois la migration terminée, veillez à désactiver l’agent.
L’agent de publication Migration doit être désactivé sur le serveur Dynamic Media afin que le workflow de retraitement fonctionne comme prévu.

<!-- Batch size is the number of assets that are amalgamated into a single IPS (Dynamic Media’s Image Production System) job. When you run the Scene7: Reprocess Assets workflow, the job is triggered on IPS. The number of IPS jobs that are triggered is based on the total number of assets in the folder, divided by the batch size. For example, suppose you had a folder with 150 assets and a batch size of 50. In this case, three IPS jobs are triggered. The assets are updated when the entire batch size (50 in our example) is processed in IPS. The job then moves onto the next IPS job and so on until complete. If you increase the batch size, you may notice a longer delay with assets getting updated. -->

**Pour retraiter des ressources dans un dossier, procédez comme suit** :
1. Dans AEM, à partir de la page Assets, accédez à un dossier de ressources auquel un profil de traitement est affecté et pour lequel vous souhaitez appliquer le workflow **Scene7 : Retraiter les ressources**.

   Dans le cas des dossiers auxquels un profil de traitement est déjà affecté, le nom du profil est affiché directement sous celui du dossier en mode Carte.

1. Sélectionnez un dossier.

   * Le workflow prend en compte tous les fichiers du dossier sélectionné, de manière récursive.
   * Si le dossier principal sélectionné contient un ou plusieurs sous-dossiers avec des ressources, le workflow retraite chaque ressource de la hiérarchie de dossiers.
   * Il est conseillé d’éviter d’exécuter ce workflow sur une hiérarchie de dossiers contenant plus de 1 000 ressources.

1. Dans la liste déroulante située dans le coin supérieur gauche de la page, cliquez sur **[!UICONTROL Chronologie]**.
1. Dans le coin inférieur gauche de la page, à droite du champ Commentaire, cliquez sur l’icône représentant un signe d’insertion (**^**).

   ![Workflow de retraitement des ressources 1](/help/assets/assets/reprocess-assets1.png)

1. Cliquez sur **[!UICONTROL Démarrer le workflow]**.
1. Dans la liste déroulante **[!UICONTROL Démarrer le workflow]**, sélectionnez **[!UICONTROL Scene7 : Retraiter les ressources]**.
1. (Facultatif) Dans la zone de texte **Entrer le titre du processus**, saisissez le nom du workflow. Si nécessaire, vous pouvez utiliser le nom pour faire référence à l’instance de workflow.

   ![Retraiter les ressources 2](/help/assets/assets/reprocess-assets2.png)

1. Cliquez sur **[!UICONTROL Démarrer]**, puis sur **[!UICONTROL Confirmer]**.

   Pour surveiller le workflow ou vérifier sa progression, cliquez sur **[!UICONTROL Outils > Workflow]** dans la page de console principale d’AEM. Sélectionnez un workflow dans la page Instances de processus. Dans la barre de menus, cliquez sur **[!UICONTROL Ouvrir l’historique]**. Vous pouvez également arrêter, suspendre ou renommer un workflow sélectionné à partir de la même page Instances de processus.

### Réglage de la taille du lot du workflow de retraitement {#adjusting-load}

(Facultatif) La taille de lot par défaut dans le workflow de retraitement est de 50 ressources par tâche. Cette taille de lot optimale est régie par la taille moyenne des fichiers et les types MIME de fichiers sur lesquels le retraitement est exécuté. Une valeur plus élevée signifie qu’une seule tâche de retraitement comprendra de nombreux fichiers. Par conséquent, la bannière de traitement reste plus longtemps sur AEM Assets. Cependant, si la taille de fichier moyenne est inférieure ou égale à 1 Mo, Adobe recommande de définir cette valeur sur plusieurs centaines de Mo, mais de ne jamais dépasser 1 000 Mo. Si la taille de fichier moyenne est élevée (de l’ordre de quelques centaines de Mo), Adobe recommande de réduire la taille du lot jusqu’à 10.

**Pour régler, si nécessaire, la taille de lot du workflow de retraitement, procédez comme suit :**

1. Dans Experience Manager, appuyez sur **[!UICONTROL Adobe Experience Manager]** pour accéder à la console de navigation globale, puis appuyez sur l’icône **[!UICONTROL Outils]** (marteau) > **[!UICONTROL Workflow > Modèles]**.
1. Sur la page Modèles de workflow, en mode Carte ou Liste, sélectionnez **[!UICONTROL Scene7 : Retraiter les ressources]**.

   ![Page Modèles de workflow avec le workflow Scene7 : Retraiter les ressources sélectionné en mode Carte](/help/assets/assets-dm/reprocess-assets7.png)

1. Dans la barre d’outils, cliquez sur **[!UICONTROL Modifier]**. Un nouvel onglet de navigateur ouvre la page du modèle de workflow Scene7 : Retraiter les ressources.
1. Dans le coin supérieur droit de la page du modèle de workflow Scene7 : Retraiter les ressources, appuyez sur **[!UICONTROL Modifier]** pour « déverrouiller » le workflow.
1. Dans le workflow, sélectionnez le composant Transfert par lots Scene7 pour ouvrir la barre d’outils, puis appuyez sur l’icône **[!UICONTROL Configurer]** de cette barre d’outils.

   ![Composant Transfert par lots Scene7](/help/assets/assets-dm/reprocess-assets8.png)

1. Dans la boîte de dialogue **[!UICONTROL Transfert par lots vers Scene7 – Propriétés des étapes]**, définissez les éléments suivants :
   * Dans les zones de texte **[!UICONTROL Titre]** et **[!UICONTROL Description]**, saisissez un titre et une description pour la tâche, le cas échéant.
   * Sélectionnez **[!UICONTROL Avance du gestionnaire]** si votre gestionnaire doit passer à l’étape suivante.
   * Dans le champ **[!UICONTROL Délai d’expiration]**, saisissez le délai d’expiration du processus externe (en secondes).
   * Dans le champ **[!UICONTROL Période]**, indiquez un intervalle d’interrogation (en secondes) pour tester la fin du processus externe.
   * Dans le champ **[!UICONTROL Lot]**, saisissez le nombre maximum de ressources (entre 50 et 1 000) à traiter dans une tâche de chargement par lots du serveur Dynamic Media.
   * Sélectionnez **[!UICONTROL Avancer sur dépassement de délai]** si vous souhaitez avancer à l’expiration du délai. Désélectionnez cette option si vous souhaitez passer à la boîte de réception à l’expiration du délai.
   ![Boîte de dialogue des propriétés](/help/assets/assets-dm/reprocess-assets3.png)

1. Dans le coin supérieur droit de la boîte de dialogue **[!UICONTROL Transfert par lots vers Scene7 – Propriétés des étapes]**, appuyez sur **[!UICONTROL Terminé]**.

1. Dans le coin supérieur droit de la page du modèle de workflow Scene7 : Retraiter les ressources, appuyez sur **[!UICONTROL Synchroniser]**. Lorsque **[!UICONTROL Synchronisé]** est affiché, cela signifie que le modèle d’exécution du workflow est correctement synchronisé et prêt à retraiter les ressources dans un dossier.

   ![Synchronisation du modèle de workflow](/help/assets/assets-dm/reprocess-assets1.png)

1. Fermez l’onglet du navigateur qui affiche le modèle de workflow Scene7 : Retraiter les ressources.

<!--1. Return to the browser tab that has the open Workflow Models page, then press **Esc** to exit the selection.
1. In the upper-left corner of the page, tap **[!UICONTROL Adobe Experience Manager]** to access the global navigation console, then tap the **[!UICONTROL Tools]** (hammer) icon > **[!UICONTROL General > CRXDE Lite]**.
1. In the folder tree on the left side of the CRXDE Lite page, navigate to the following location:

   `/conf/global/settings/workflow/models/scene7_reprocess_assets/jcr:content/flow/reprocess/metaData`

   ![CRXDE Lite](/help/assets/assets/workflow-models9.png)

1. On the right side of the CRXDE Lite page, in the lower portion, enter the following name, type, and value in its respective field:
    * **[!UICONTROL Name]**: `reprocess-batch-size`
    * **[!UICONTROL Type]**: `Long`
    * **[!UICONTROL Value]**: enter a default value (50-1000) for the batch size
1. In the lower-right corner, tap **[!UICONTROL Add]**. The new property appears as the following:

    ![Saving the new property](/help/assets/assets/workflow-models10.png)

1. On the menu bar of the CRXDE Lite page, tap **[!UICONTROL Save All]**.
1. In the upper-left corner of the page, tap **[!UICONTROL CRXDE Lite]** to return to the main AEM console
1. Repeat steps 1-7 to re-synchronize the new batch size to the Scene7: Reprocess Assets workflow model.-->
