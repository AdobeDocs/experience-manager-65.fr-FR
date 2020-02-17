---
title: Configuration des polices de remplacement
seo-title: Configuration des polices de remplacement
description: Découvrez comment configurer des polices de remplacement.
seo-description: Découvrez comment configurer des polices de remplacement.
uuid: 2745541c-8c6d-4bb4-aa14-ec19afd6bc35
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d997a268-a40a-462d-badd-94f0731f7ba4
translation-type: tm+mt
source-git-commit: d3719a9ce2fbb066f99445475af8e1f1e7476f4e

---


# Configuration des polices de remplacement {#configuring-fallback-fonts}

Cette section explique comment configurer manuellement le fichier FontManagerResources.properties pour associer les polices par défaut d&#39;AEM forms à des polices de remplacement (ou de substitution), qui seront utilisées si les polices par défaut ne sont pas disponibles sur le serveur. Ce fichier de propriétés se trouve dans le fichier adobe-fontmanager.jar.

>[!NOTE]
>
>la configuration des polices de remplacement s’applique également au service d’assemblage.

1. Navigate to the adobe-livecycle-*`[appserver]`*.ear file in the *`[aem-forms root]`*/configurationManager/export directory, make a backup copy, and unpackage the original.
1. Recherchez le fichier adobe-fontmanager.jar et décompressez-le.
1. Recherchez le fichier FontManagerResources.properties et ouvrez-le dans un éditeur de texte.
1. Modifiez les emplacements et les noms des polices dans les sections Generic et Fallback de manière appropriée et enregistrez le fichier.

   The font entries in the FontManagerResources.properties file are relative to the *`[aem-forms root]`*/fonts directory. Si vous spécifiez des polices autres que les polices par défaut d&#39;AEM forms, vous devez les installer dans cette arborescence (dans un répertoire existant ou créé à cet effet).

   >[!NOTE]
   >
   >si la police spécifiée ou la police par défaut ne contient pas un caractère Unicode spécifique, ou si elle est indisponible, le caractère est extrait d’une police de remplacement, en respectant la priorité suivante :

   * police spécifique aux paramètres régionaux ;
   * police racine si les paramètres régionaux ne sont pas définis ;
   * police générique, la recherche étant effectuée dans l’ordre de la table de remplacement.

1. Recompressez le fichier adobe-fontmanager.jar.
1. Repackage the adobe-livecycle-*`[appserver]`*.ear file and then redeploy it either manually or by running Configuration Manager.

>[!NOTE]
>
>Do not use Configuration Manager to repackage the adobe-livecycle-`[appserver]`.ear file because it will overwrite your modifications with the AEM forms default values.

