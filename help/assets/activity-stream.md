---
title: Flux d’activités des ressources numériques dans la vue de chronologie
description: Cet article décrit comment afficher les journaux d’activité pour les ressources de la chronologie.
contentOwner: AG
feature: Asset Management
role: User, Admin
exl-id: 28dc0aa5-f2be-4e27-b7d8-415569b7ecd4
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 72%

---

# Flux d’activité dans la chronologie {#activity-stream-in-timeline}

Cette fonctionnalité affiche les journaux d’activités correspondant aux ressources de la chronologie. Si vous effectuez l’une des opérations suivantes liées aux ressources dans [!DNL Adobe Experience Manager Assets], la fonction de flux d’activités met à jour la chronologie afin de refléter l’activité.

Les opérations suivantes sont consignées dans le flux d’activités :

* Créer
* Supprimer
* Téléchargement (rendus compris)
* Publication
* Annuler la publication
* Approuver
* Refuser
* Déplacer

Les journaux d’activité à afficher dans la chronologie sont récupérés à partir de l’emplacement `/var/audit/com.day.cq.dam/content/dam` dans CRX, où les fichiers journaux sont stockés. En outre, l’activité de la chronologie est consignée lorsque de nouvelles ressources sont chargées ou que des ressources existantes sont modifiées et archivées. [!DNL Experience Manager] via [Adobe d’un lien de ressource](https://helpx.adobe.com/fr/enterprise/admin-guide.html/enterprise/using/manage-assets-using-adobe-asset-link.ug.html) ou [application de bureau Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html?lang=fr).

>[!NOTE]
>
>Les workflows transitoires ne sont pas affichés dans la chronologie, car aucune information d’historique n’est enregistrée pour ces derniers.

Pour afficher le flux d’activités, effectuez une ou plusieurs des opérations sur la ressource, sélectionnez la ressource, puis sélectionnez **[!UICONTROL Chronologie]** dans la liste de navigation globale.

![chronologie-2](assets/timeline-2.png)

La chronologie affiche le flux d’activités des opérations que vous effectuez sur les ressources.

![activity_stream](assets/activity_stream.png)

>[!NOTE]
>
>L’emplacement de stockage par défaut pour les tâches **[!UICONTROL Publier]** et **[!UICONTROL Annuler la publication]** est `/var/audit/com.day.cq.replication/content`. Pour les tâches **[!UICONTROL Déplacer]**, l’emplacement par défaut est `/var/audit/com.day.cq.wcm.core.page`.
