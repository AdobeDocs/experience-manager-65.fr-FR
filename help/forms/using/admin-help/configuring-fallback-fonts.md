---
title: Configuration des polices de réserve
description: Découvrez comment configurer les polices de secours pour AEM Forms. Vous pouvez utiliser le fichier FontManagerResources.properties pour mapper manuellement les polices par défaut aux polices de secours.
uuid: 2745541c-8c6d-4bb4-aa14-ec19afd6bc35
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d997a268-a40a-462d-badd-94f0731f7ba4
feature: PDF Generator
exl-id: 76dd2b0c-9f16-47bf-a565-99277be750fb
source-git-commit: 22d9b22a0fc0bc5f753f2e11ca66e2627e1a8405
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 51%

---

# Configuration des polices de réserve {#configuring-fallback-fonts}

Cette section explique comment configurer manuellement le fichier FontManagerResources.properties pour associer les polices par défaut d’AEM forms à des polices de remplacement (ou de substitution), qui seront utilisées si les polices par défaut ne sont pas disponibles sur le serveur. Ce fichier de propriétés se trouve dans le fichier adobe-fontmanager.jar .

>[!NOTE]
>
>La configuration des polices de secours s’applique également au service Assembler.

1. Accédez au fichier adobe-livecycle-*`[appserver]`*.ear dans le répertoire *`[aem-forms root]`*/configurationManager/export, faites une copie de sauvegarde et décompressez l’original.
1. Recherchez le fichier adobe-fontmanager.jar et décompressez-le.
1. Recherchez le fichier FontManagerResources.properties et ouvrez-le dans un éditeur de texte.
1. Modifiez les noms et emplacements des polices Generic et Fallback selon les besoins, puis enregistrez le fichier.

   Les entrées de polices dans le fichier FontManagerResources.properties sont relatives au répertoire *`[aem-forms root]`*/fonts. Si vous spécifiez des polices autres que les polices par défaut d’AEM forms, vous devez les installer dans cette arborescence (dans un répertoire existant ou créé à cet effet).

   >[!NOTE]
   >
   >Si la police spécifiée ou la police par défaut ne contient pas de caractère unicode spécifique ou si elle n’est pas disponible, le caractère est extrait d’une police de secours selon la priorité suivante :

   * Police spécifique aux paramètres régionaux
   * police RAOT si les paramètres régionaux ne sont pas définis ;
   * Police générique, recherchée par ordre défini dans la table de secours

1. Recompressez le fichier adobe-fontmanager.jar.
1. Recompressez le fichier adobe-livecycle-*`[appserver]`*.ear, puis redéployez-le manuellement ou en exécutant le Gestionnaire de configuration.

>[!NOTE]
>
>N’utilisez pas le Gestionnaire de configuration pour recompresser le fichier adobe-livecycle-`[appserver]`.ear, car cela entraînerait le remplacement de vos modifications par les valeurs par défaut des formulaires AEM.
