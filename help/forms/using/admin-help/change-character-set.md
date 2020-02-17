---
title: Modification du jeu de caractères
seo-title: Modification du jeu de caractères
description: Vous pouvez indiquer le jeu de caractères utilisé pour encoder le flux de sortie. Découvrez comment modifier le jeu de caractères.
seo-description: Vous pouvez indiquer le jeu de caractères utilisé pour encoder le flux de sortie. Découvrez comment modifier le jeu de caractères.
uuid: ecb0c3ff-368c-4553-80e4-aa35fc15af62
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 811b31f8-5465-4fb2-b1f9-513936041771
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Modification du jeu de caractères {#change-the-character-set}

Vous pouvez indiquer le jeu de caractères utilisé pour encoder le flux de sortie.

1. In administration console, click **[!UICONTROL Services > output]**.
1. Sous Internationalisation, dans la liste Jeu de caractères, sélectionnez un jeu de caractères. Ce paramètre dépend des paramètres `TransformationFormat` et `PrintFormat` spécifiés via l’API. Pour spécifier un jeu de caractères ne figurant pas dans la liste, sélectionnez Personnalisé et spécifiez la valeur d’encodage dans la zone qui s’affiche.

   Si le paramètre `TransformationFormat` prend la valeur PDF et PDF/A ou que le paramètre `PrintFormat` prend la valeur PCL, PostScript, Zebra label, IPL, DPL, TPCL, GenericColorPCL ou GenericPSLevel3, seuls des jeux de caractères spécifiques sont pris en charge.

   Le nom du jeu de caractères doit être un nom canonique valide. La valeur par défaut est ISO-8859-1.

1. Cliquez sur **[!UICONTROL Enregistrer]**.

