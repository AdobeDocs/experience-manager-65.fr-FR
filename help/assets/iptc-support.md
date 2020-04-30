---
title: Utilisez les métadonnées IPTC dans [!DNL Adobe Experience Manager Assets].
description: Découvrez comment [!DNL Adobe Experience Manager Assets] prend en charge les métadonnées IPTC, les évaluations créatives et les mots-clés ajoutés aux ressources via Adobe Bridge et d’autres applications Creative.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 90f9c0b60d4b0878f56eefea838154bb7627066d

---


# Utilisation des métadonnées IPTC {#support-for-iptc-metadata}

Learn how [!DNL Adobe Experience Manager Assets] supports the IPTC metadata, Creative ratings, and keywords added to assets through [!DNL Adobe Bridge] and other [!DNL Adobe Creative Cloud] apps.

[!DNL Adobe Experience Manager Assets] prend en charge la norme de métadonnées IPTC largement utilisée pour décrire les fichiers. This way, [!DNL Assets] enhances the acceptance of its images among various parties, including photographers, creative agencies, libraries, museums, and so on.

Le schéma de métadonnées utilisé pour les ressources intègre désormais IPTC Core et IPTC Extension, deux schémas permettant de définir des propriétés de métadonnées complètes, grâce auxquels les utilisateurs peuvent ajouter des données fiables et précises sur les personnes, les lieux et les produits illustrés dans une image. Il prend également en charge les dates, noms et identifiants relatifs à la création de l’image, ainsi qu’une méthode permettant d’exprimer les informations sur les droits avec une certaine souplesse.

La page des propriétés des ressources comprend maintenant des onglets distincts pour afficher les métadonnées IPTC Core et IPTC Extension dans des champs modifiables.

1. From the [!DNL Assets] user interface, select an image.
1. Cliquez sur **[!UICONTROL Propriétés]** dans la barre d’outils.
1. Click the **[!UICONTROL IPTC]** tab to view the IPTC metadata for the asset.
1. Modifiez les propriétés de métadonnées IPTC, le cas échéant.

   ![iptc_tab](assets/keywords-in-iptc-tab.png)

1. Click the **[!UICONTROL IPTC Extension]** tab to view IPTC Extension metadata for the asset.
1. Modifiez les propriétés de métadonnées de l’extension IPTC, le cas échéant.
1. Click **[!UICONTROL Save &amp; Close]** to save the changes.

## Creative rating support {#creative-rating-support}

Outre les évaluations individuelles et cumulées, la page Propriétés affiche désormais les évaluations affectées à des ressources par le biais d’Adobe Bridge et d’autres applications Creative.

Ces évaluations sont disponibles dans la section **[!UICONTROL Évaluation de la création]** de l’onglet **[!UICONTROL Avancé]**.

Cette évaluation est une propriété en lecture seule dont la valeur est comprise entre 1 et 5. Vous pouvez rechercher des ressources en fonction de leur évaluation de création dans le panneau Rechercher.

Notez toutefois que cette propriété n’est pas indexée pour l’instant et ce, afin d’éviter tout conflit avec les modifications personnalisées apportées par les utilisateurs.

## Keyword support {#keyword-support}

The **[!UICONTROL IPTC]** tab of the [!UICONTROL Properties] page also displays keywords added to assets through Adobe Bridge and other Adobe Creative Cloud apps. Vous pouvez aussi modifier ces mots-clés et en ajouter d’autres à partir de l’onglet **[!UICONTROL IPTC]**.

![mots-clés](assets/keywords-in-iptc-tab.png)
