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
feature: PDF Generator
exl-id: 76dd2b0c-9f16-47bf-a565-99277be750fb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 72%

---

# Configuration des polices de remplacement {#configuring-fallback-fonts}

Cette section explique comment configurer manuellement le fichier FontManagerResources.properties pour associer les polices par défaut d&#39;AEM forms à des polices de remplacement (ou de substitution), qui seront utilisées si les polices par défaut ne sont pas disponibles sur le serveur. Ce fichier de propriétés se trouve dans le fichier adobe-fontmanager.jar.

>[!NOTE]
>
>la configuration des polices de remplacement s’applique également au service d’assemblage.

1. Accédez au fichier adobe-livecycle-*`[appserver]`*.ear dans le répertoire *`[aem-forms root]`*/configurationManager/export, effectuez une copie de sauvegarde et décompressez l’original.
1. Recherchez le fichier adobe-fontmanager.jar et décompressez-le.
1. Recherchez le fichier FontManagerResources.properties et ouvrez-le dans un éditeur de texte.
1. Modifiez les emplacements et les noms des polices dans les sections Generic et Fallback de manière appropriée et enregistrez le fichier.

   Les entrées de police du fichier FontManagerResources.properties sont relatives au répertoire *`[aem-forms root]`*/fonts. Si vous spécifiez des polices autres que les polices par défaut d&#39;AEM forms, vous devez les installer dans cette arborescence (dans un répertoire existant ou créé à cet effet).

   >[!NOTE]
   >
   >si la police spécifiée ou la police par défaut ne contient pas un caractère Unicode spécifique, ou si elle est indisponible, le caractère est extrait d’une police de remplacement, en respectant la priorité suivante :

   * police spécifique aux paramètres régionaux ;
   * police racine si les paramètres régionaux ne sont pas définis ;
   * police générique, la recherche étant effectuée dans l’ordre de la table de remplacement.

1. Recompressez le fichier adobe-fontmanager.jar.
1. Recompressez le fichier adobe-livecycle-*`[appserver]`*.ear, puis redéployez-le manuellement ou en exécutant Configuration Manager.

>[!NOTE]
>
>N’utilisez pas Configuration Manager pour recompresser le fichier adobe-livecycle-`[appserver]`.ear, car il remplacera vos modifications par les valeurs par défaut d’AEM forms.
