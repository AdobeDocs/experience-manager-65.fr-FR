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
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: b26425d0-6fde-5e02-bfd6-e560e2fa86c9
    internal-label: PDF Generator
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 100%
---
# Configuration des polices de réserve {#configuring-fallback-fonts}

Vous pouvez configurer manuellement le fichier FontManagerResources.properties pour associer les polices par défaut d’AEM Forms à des polices de remplacement (ou de substitution) si les polices par défaut ne sont pas disponibles sur le serveur. Ce fichier de propriétés se trouve dans le fichier adobe-fontmanager.jar.

>[!NOTE]
>
>La configuration des polices de réserve s’applique également au service Assembler.

1. Accédez au fichier adobe-livecycle-*`[appserver]`*.ear dans le répertoire *`[aem-forms root]`*/configurationManager/export, faites une copie de sauvegarde et décompressez l’original.
1. Recherchez le fichier adobe-fontmanager.jar et décompressez-le.
1. Recherchez le fichier FontManagerResources.properties et ouvrez-le dans un éditeur de texte.
1. Modifiez les noms et emplacements des polices génériques (Generic) et des polices de réserve (Fallback) selon les besoins, puis enregistrez le fichier.

   Les entrées de polices dans le fichier FontManagerResources.properties sont relatives au répertoire *`[aem-forms root]`*/fonts. Si vous spécifiez des polices autres que les polices par défaut d’AEM Forms, vous devez les installer dans cette arborescence (dans un répertoire existant ou créé à cet effet).

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
