---
title: Configuration des polices de réserve
description: Découvrez comment configurer des polices de réserve pour AEM Forms. Vous pouvez utiliser le fichier FontManagerResources.properties pour mapper manuellement les polices par défaut aux polices de réserve.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: PDF Generator
exl-id: 76dd2b0c-9f16-47bf-a565-99277be750fb
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '264'
ht-degree: 100%

---

# Configuration des polices de réserve {#configuring-fallback-fonts}

Cette section explique comment configurer manuellement le fichier FontManagerResources.properties pour associer les polices par défaut d’AEM forms à des polices de remplacement (ou de substitution), qui seront utilisées si les polices par défaut ne sont pas disponibles sur le serveur. Ce fichier de propriétés se trouve dans le fichier adobe-fontmanager.jar.

>[!NOTE]
>
>La configuration des polices de réserve s’applique également au service Assembler.

1. Accédez au fichier adobe-livecycle-*`[appserver]`*.ear dans le répertoire *`[aem-forms root]`*/configurationManager/export, faites une copie de sauvegarde et décompressez l’original.
1. Recherchez le fichier adobe-fontmanager.jar et décompressez-le.
1. Recherchez le fichier FontManagerResources.properties et ouvrez-le dans un éditeur de texte.
1. Modifiez les noms et emplacements des polices génériques (Generic) et des polices de réserve (Fallback) selon les besoins, puis enregistrez le fichier.

   Les entrées de polices dans le fichier FontManagerResources.properties sont relatives au répertoire *`[aem-forms root]`*/fonts. Si vous spécifiez des polices autres que les polices par défaut d’AEM forms, vous devez les installer dans cette arborescence (dans un répertoire existant ou créé à cet effet).

   >[!NOTE]
   >
   >Si la police spécifiée ou la police par défaut ne contient pas de caractère Unicode spécifique ou si elle n’est pas disponible, le caractère est extrait d’une police de réserve, en respectant la priorité suivante :

   * police spécifique aux paramètres régionaux ;
   * police racine si les paramètres régionaux ne sont pas définis ;
   * police générique, la recherche étant effectuée selon l’ordre du tableau de réserve.

1. Recompressez le fichier adobe-fontmanager.jar.
1. Recompressez le fichier adobe-livecycle-*`[appserver]`*.ear, puis redéployez-le manuellement ou en exécutant le Gestionnaire de configuration.

>[!NOTE]
>
>N’utilisez pas le Gestionnaire de configuration pour recompresser le fichier adobe-livecycle-`[appserver]`.ear, car cela entraînerait le remplacement de vos modifications par les valeurs par défaut des formulaires AEM.
