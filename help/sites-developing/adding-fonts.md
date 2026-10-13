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
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '184'
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
