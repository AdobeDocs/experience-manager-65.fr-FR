---
title: Gestion des droits numériques dans AEM [!DNL Adobe Experience Manager Assets].
description: Découvrez comment gérer les informations d’expiration et d’état des ressources sous licence dans [!DNL Experience Manager].
contentOwner: AG
translation-type: tm+mt
source-git-commit: 20f337ea2e4f369eb6eb760d312199fa39556513
workflow-type: tm+mt
source-wordcount: '1428'
ht-degree: 55%

---


# Digital Rights Management for assets {#digital-rights-management-in-assets}

Les ressources numériques sont souvent associées à une licence qui spécifie les termes et la durée d’utilisation. Because [!DNL Adobe Experience Manager Assets] is fully integrated with the [!DNL Experience Manager] platform, you can efficiently manage asset expiration information and asset states. Vous pouvez également associer des informations de licence à des ressources.

## Expiration de ressources {#asset-expiration}

L’expiration des ressources est un moyen efficace de faire respecter les exigences de licence des ressources. Elle garantit que la ressource qui est publiée ne l’est plus lorsqu’elle arrive à expiration, ce qui évite tout risque de violation de licence. Un utilisateur ne disposant pas d’autorisations d’administrateur ne peut pas modifier, copier, déplacer, publier et télécharger une ressource arrivée à expiration.

You can view the expiration status of an asset in the [!DNL Assets] console in both the card and list views.

![expired_flag_card](assets/expired_flag_card.png)

*Figure : Dans la vue de carte, un indicateur sur la carte indique un fichier expiré.*

![expired_flag_liste](assets/expired_flag_list.png)

*Figure : Dans la vue de liste, la colonne[!UICONTROL Etat]affiche la bannière[!UICONTROL Expiré].*

You can view the expiration status of an asset in the [!UICONTROL Timeline] in left rail.

![chlimage_1-144](assets/chlimage_1-144.png)

>[!NOTE]
>
>La date d’expiration d’un fichier s’affiche différemment pour les utilisateurs de différents fuseaux horaires.

You can also view the expiration status of assets in the **[!UICONTROL References]** rail. Il gère les états d’expiration des ressources et les relations entre les ressources composites et les sous-ressources, les collections et les projets référencés.

1. Accédez à la ressource pour laquelle vous souhaitez voir les pages web de référencement et les ressources composites.
1. Sélectionnez le fichier, puis cliquez sur le [!DNL Experience Manager] logo.

1. Sélectionnez **[!UICONTROL Références]** dans le menu.

   ![chlimage_1-146](assets/chlimage_1-146.png)

   Pour les ressources arrivées à expiration, le rail Références affiche l’état d’expiration **[!UICONTROL La ressource est arrivée à expiration]** en haut.

   ![chlimage_1-147](assets/chlimage_1-147.png)

   Si la ressource contient des sous-ressources arrivées à expiration, le rail Références affiche l’état **[!UICONTROL La ressource contient des sous-ressources arrivées à expiration]**.

   ![chlimage_1-148](assets/chlimage_1-148.png)

### Recherche de ressources arrivées à expiration {#search-expired-assets}

Vous pouvez rechercher des ressources arrivées à expiration, y compris les sous-ressources expirées dans le panneau de recherche.

1. In the [!DNL Assets] console, click the **[!UICONTROL Search]** in the toolbar to display the Omnisearch box.

1. Avec le curseur dans la zone Omni-recherche, appuyez sur la touche Entrée pour afficher la page des résultats de la recherche.

   ![chlimage_1-150](assets/chlimage_1-150.png)

1. Cliquez sur [!DNL Experience Manager] le logo pour afficher le panneau de recherche.

   ![chlimage_1-151](assets/chlimage_1-151.png)

1. Click the **[!UICONTROL Expiry Status]** option to expand it.

   ![chlimage_1-152](assets/chlimage_1-152.png)

1. Sélectionnez **[!UICONTROL Expiré]**. Les ressources arrivées à expiration sont visibles dans les résultats de la recherche.

   ![chlimage_1-153](assets/chlimage_1-153.png)

When you choose the **[!UICONTROL Expired]** option, the [!DNL Assets] console only displays the expired assets and subassets that are referenced by compound assets. Les ressources composites qui référencent des sous-ressources expirées ne s’affichent pas immédiatement une fois que les sous-ressources arrivent à expiration. Instead, they are displayed after [!DNL Experience Manager] detects that they reference expired subassets the next time the scheduler runs.

Si vous modifiez la date d’expiration d’une ressource publiée à une date antérieure au cycle du planificateur en cours, la planification détecte toujours cette ressource en tant que ressource expirée lors de sa prochaine exécution et elle reflète son état en conséquence.

En outre, si un problème ou une erreur empêche le planificateur de détecter les ressources expirées dans le cycle en cours, le planificateur réexamine ces ressources lors du cycle suivant et identifie leur statut expiré.

To enable the [!DNL Assets] console to display the referencing compound assets along with the expired subassets, configure an **[!UICONTROL Adobe CQ DAM Expiry Notification]** workflow in [!DNL Experience Manager] Configuration Manager.

1. Open [!DNL Experience Manager] Configuration Manager.
1. Sélectionnez l’option de **[!UICONTROL notification d’expiration d’Adobe CQ DAM]**. Par défaut, le **[!UICONTROL planificateur basé temps]** est sélectionné. Il programme une tâche qui vérifie, à un moment précis, si une ressource contient des sous-ressources arrivées à expiration. Une fois la tâche terminée, les ressources qui possèdent des sous-ressources expirées et des ressources référencées sont affichées à l’état expiré dans les résultats de la recherche.

   ![chlimage_1-154](assets/chlimage_1-154.png)

1. Pour exécuter la tâche périodiquement, décochez l’option de **[!UICONTROL planificateur basé sur le temps]** et modifiez la périodicité en secondes dans le champ du **[!UICONTROL planificateur de périodicité]**. Par exemple, l’expression « 0 0 0 * * ? » déclenche la tâche à 00 heures.
1. Sélectionnez **[!UICONTROL Envoyer un courrier électronique]** pour être averti, par e-mail, de l’expiration d’une ressource.

   >[!NOTE]
   >
   >Only the asset creator (the person who uploads a particular asset to [!DNL Assets]) receives an email when the asset expires. See [how to configure email notification](/help/sites-administering/notification.md) for additional details around configuring email notifications at the overall [!DNL Experience Manager] level.

1. Dans le champ **[!UICONTROL Notification préalable en secondes]** indiquez l’intervalle de temps, en secondes, qui précède le moment auquel une ressource expire et pendant lequel vous souhaitez recevoir une notification concernant l’expiration. Si vous êtes administrateur ou l’auteur de la ressource, vous recevez un message avant son expiration vous informant qu’elle va expirer une fois le délai spécifié écoulé.

   Une fois la ressource arrivée à expiration, vous recevez une notification par courrier électronique qui confirme l’expiration. En outre, les ressources expirées sont désactivées.

1. Cliquez sur **[!UICONTROL Enregistrer]**.

## États d’une ressource {#asset-states}

La [!DNL Assets] console peut afficher divers états pour les ressources. En fonction de l’état actuel d’une ressource donnée, le mode Carte affiche un libellé décrivant son état (par exemple, expiré, modifié, approuvé, rejeté, etc.).

1. In the [!DNL Assets] user interface, select an asset.

   ![chlimage_1-155](assets/chlimage_1-155.png)

1. Click **[!UICONTROL Publish]** from the toolbar. If you don&#39;t see **Publish** on the toolbar, click **[!UICONTROL More]** on the toolbar and locate **[!UICONTROL Publish]** option.

   ![chlimage_1-156](assets/chlimage_1-156.png)

1. Sélectionnez **[!UICONTROL Publier]** dans le menu, puis fermez la boîte de dialogue de confirmation.
1. Quittez le mode de sélection. L’état de publication de la ressource s’affiche au bas de sa miniature en mode d’affichage Carte. En mode Liste, la colonne Publié indique le moment auquel la ressource a été publiée.

   ![chlimage_1-157](assets/chlimage_1-157.png)

1. Pour afficher sa page de détails sur les ressources, dans l’ [!DNL Assets] interface, sélectionnez une ressource et cliquez sur **[!UICONTROL Propriétés]**.

   ![chlimage_1-158](assets/chlimage_1-158.png)

1. In the Advanced tab, set an expiration date for the asset from the **[!UICONTROL Expires]** field.

   ![définir la date et l’heure d’expiration de l’actif dans le champ Expire](assets/asset-properties-advanced-tab.png)

   *Figure :[!UICONTROL Onglet Avancé]dans la page[!UICONTROL Propriétés]du fichier pour définir l’expiration du fichier.*

1. Cliquez sur **[!UICONTROL Enregistrer]**, puis sur **[!UICONTROL Fermer]** pour afficher la console Ressources.
1. L’état de publication de la ressource indique qu’elle a expiré au bas de sa miniature en mode d’affichage Carte. En mode Liste, l’état de la ressource s’affiche comme étant **[!UICONTROL arrivée à expiration]**.

   ![chlimage_1-160](assets/chlimage_1-160.png)

1. In the [!DNL Assets] console, select a folder and create a review task on the folder.
1. Recherchez et approuvez/rejetez les ressources dans la tâche de révision, puis cliquez sur **[!UICONTROL Terminé]**.
1. Accédez au dossier pour lequel vous avez créé la tâche de révision. L’état des ressources que vous avez approuvées/rejetées s’affiche en bas du mode Carte. En mode Liste, les états d’approbation et d’expiration sont affichés dans les colonnes correspondantes.

   ![chlimage_1-161](assets/chlimage_1-161.png)

1. To search for assets based on their status, click **[!UICONTROL Search]** to display the Omnisearch bar.

   ![chlimage_1-162](assets/chlimage_1-162.png)

1. Appuyez sur Retour et cliquez sur [!DNL Experience Manager] pour afficher le panneau de recherche.
1. In the search panel, click **[!UICONTROL Publish Status]** and select **[!UICONTROL Published]** to search for published assets in [!DNL Assets].

   ![chlimage_1-163](assets/chlimage_1-163.png)

1. Click **[!UICONTROL Approval Status]** and click the appropriate option to search for approved or rejected assets.

   ![chlimage_1-164](assets/chlimage_1-164.png)

1. Pour rechercher des ressources en fonction de leur état d’expiration, sélectionnez **[!UICONTROL État d’expiration]** dans le panneau de recherche et choisissez l’option appropriée.

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. Vous pouvez également rechercher des éléments en fonction de plusieurs états, sous diverses facettes de recherche. Par exemple, vous pouvez rechercher les ressources publiées qui ont été approuvées dans une tâche de révision et qui n’ont pas encore expiré, en sélectionnant les options correspondantes dans les facettes de recherche.

   ![chlimage_1-166](assets/chlimage_1-166.png)

## Digital Rights Management in [!DNL Assets] {#digital-rights-management-in-assets-1}

This feature enforces the acceptance of the license agreement before you can download a licensed asset from [!DNL Adobe Experience Manager Assets].

If you select a protected asset and click **[!UICONTROL Download]**, you are redirected to a license page to accept the license agreement. If you do not accept the license agreement, the **[!UICONTROL Download]** option is not available.

Si la sélection contient plusieurs ressources protégées, sélectionnez-en une à la fois, acceptez le contrat de licence et procédez au téléchargement de la ressource.

Une ressource est considérée comme protégée si l’une des conditions suivantes est remplie :

* La propriété de métadonnées de la ressource `xmpRights:WebStatement` pointe vers le chemin d’accès de la page  qui contient le contrat de licence approprié.
* La valeur de la propriété de métadonnées de la ressource `adobe_dam:restrictions` est un code HTML brut qui spécifie le contrat de licence.

>[!NOTE]
>
>The location `/etc/dam/drm/licenses` used for storing licenses in earlier releases of [!DNL Experience Manager] is deprecated.
>
>If you create or modify licence pages, or port them from previous [!DNL Experience Manager] releases, Adobe recommends that you store them under `/apps/settings/dam/drm/licenses` or `/conf/&ast;/settings/dam/drm/licenses`.

### Téléchargement de fichiers protégés par DRM {#downloading-drm-assets}

1. In the card view, select the assets you want to download and click **[!UICONTROL Download]**.
1. Dans la page **[!UICONTROL Gestion des droits d’auteur]**, sélectionnez la ressource à télécharger dans la liste.
1. In the [!UICONTROL License] pane, choose **[!UICONTROL Agree]**. Une coche s’affiche en regard du fichier. Click the **[!UICONTROL Download]** option.

   >[!NOTE]
   >
   >The **[!UICONTROL Download]** option is enabled only when you choose to agree to the license agreement for a protected asset. However, if your selection comprises both protected and unprotected assets, only the protected assets are listed in the pane and the **[!UICONTROL Download]** option is enabled to download the unprotected assets. Pour accepter le contrat de licence de plusieurs ressources protégées en même temps, sélectionnez-les dans la liste, puis cliquez sur **[!UICONTROL Accepter]**.

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. In the dialog, click **[!UICONTROL Download]** to download the asset or its renditions.
