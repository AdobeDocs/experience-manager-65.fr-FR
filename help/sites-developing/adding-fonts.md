---
title: Ajout de polices pour le rendu graphique
description: AEM vous permet de générer des graphiques incorporant du texte extrait dynamiquement de votre contenu.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: 725c81d0-0258-4118-8b01-29fd7bcaf9b3
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 100%

---

# Ajout de polices pour le rendu graphique{#adding-fonts-for-graphic-rendering}

AEM vous permet de générer des graphiques incorporant du texte extrait dynamiquement de votre contenu.

Pour ce faire, vous pouvez également charger et utiliser vos propres polices.

Actuellement, toutes les implémentations de la plateforme Java prennent en charge les polices [TrueType](https://fr.wikipedia.org/wiki/TrueType).

1. Ouvrez CRXDE Lite et accédez au dossier de votre application de projet :

   `/apps/<your-project>/`

1. Sous `/apps/<your-project>/`, créez un nœud :

   * **Nom** : `fonts`
   * **Type** : `sling:Folder`

   Enregistrez toutes les modifications.

1. Copiez les fichiers de polices dans ce dossier, par exemple, au moyen de WebDAV.

   >[!NOTE]
   >
   >Les fichiers de polices du référentiel doivent comporter le suffixe `*.ttf` ou `*.TTF`.

1. Mettez à jour la [configuration OSGi](/help/sites-deploying/configuring-osgi.md) de [Day Commons GFX Font Helper](/help/sites-deploying/osgi-configuration-settings.md). Ajoutez le chemin d’accès à votre dossier de polices, à savoir `/apps/<your-project>/fonts`.

1. Revenez à CRXDE Lite. Vous devez alors voir un nœud `.fontlist` dabs votre dossier contenant le nom des polices importées.

   Ces polices sont désormais prêtes à être déployées dans l’API Java.

Pour plus d’informations sur l’utilisation des polices avec l’API Java, consultez la [documentation de la classe Font de l’API Java](https://download.oracle.com/javase/6/docs/api/java/awt/Font.html).
