---
title: Ajout de polices pour le rendu graphique
seo-title: Ajout de polices pour le rendu graphique
description: AEM vous permet de générer des objets graphiques incorporant du texte extrait dynamiquement de votre contenu
seo-description: AEM vous permet de générer des objets graphiques incorporant du texte extrait dynamiquement de votre contenu
uuid: 67d9b10f-e986-4d29-bde2-10e08075fe17
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 6af48ef5-75e6-4b66-bc0d-ecf254b1c4ef
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 69%

---


# Ajout de polices pour le rendu graphique{#adding-fonts-for-graphic-rendering}

AEM vous permet de générer des objets graphiques incorporant du texte extrait dynamiquement de votre contenu.

Pour ce faire, vous pouvez également charger et utiliser vos propres polices.

Actuellement, toutes les implémentations de la plate-forme Java prennent en charge les polices [TrueType](https://en.wikipedia.org/wiki/Truetype).

1. Ouvrez le CRXDE Lite et accédez au dossier de votre application de projet :

   `/apps/<your-project>/`

1. Under `/apps/<your-project>/` create a new node:

   * **Nom** : `fonts`
   * **Type** : `sling:Folder`

   Enregistrez toutes les modifications.

1. Copiez les fichiers de polices dans ce dossier, par exemple, au moyen de WebDAV.

   >[!NOTE]
   >
   >Font files in the repository must have the suffix `*.ttf` or `*.TTF`.

1. Mettez à jour la [configuration OSGi](/help/sites-deploying/configuring-osgi.md) de [Day Commons GFX Font Helper](/help/sites-deploying/osgi-configuration-settings.md). Add the path to your fonts folder; i.e. `/apps/<your-project>/fonts`.

1. Revenez à CRXDE Lite. You should now see a `.fontlist` node in your folder containing the name of the imported fonts.

   Ces polices sont désormais prêtes à être déployées dans l’API Java.

Pour plus d’informations sur l’utilisation des polices avec l’API Java, consultez la [documentation de la classe Font de l’API Java](https://download.oracle.com/javase/6/docs/api/java/awt/Font.html).

