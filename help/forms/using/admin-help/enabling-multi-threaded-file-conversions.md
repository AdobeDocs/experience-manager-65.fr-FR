---
title: Activer les conversions de fichiers multithreads
description: Découvrez comment activer des conversions de fichiers multithreads.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: PDF Generator
exl-id: 402c1fd4-c6c8-494e-b452-b56a91c4a397
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 4a55f87d3b8aa9944f0b32760aa645c42efd93e8
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 3%
---
# Activer les conversions de fichiers multithreads {#enabling-multi-threaded-file-conversions}

PDF Generator peut exécuter plusieurs conversions de fichiers simultanément pour améliorer le débit de conversion. Choisissez le mode de conversion applicable :

| Mode de conversion | Applications prenant en charge les conversions simultanées | Modèle de compte d’utilisateur |
|---|---|---|
| Mode multi-utilisateur | OpenOffice | Un compte utilisateur distinct exécute chaque instance OpenOffice. |
| Mode Utilisateur unique | ® Word et Microsoft® Excel | Un compte utilisateur exécute plusieurs instances Word et Excel. Les conversions PowerPoint restent sérialisées. |

Avant d’activer l’un ou l’autre mode, effectuez la configuration de préinstallation de [&#128279;](/help/forms/using/install-configure-document-services.md#preinstallationconfigurations) pour les applications et le système d’exploitation que vous utilisez. Pour connaître les versions d’application prises en charge, voir [Prise en charge logicielle de PDF Generator](/help/forms/using/aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator).

## Mode multi-utilisateur {#multi-user-mode}

En mode multi-utilisateur, PDF Generator lance chaque instance OpenOffice sous un compte utilisateur distinct. Configurez un nombre suffisant de comptes d’utilisateur d’administration valides pour le nombre de conversions simultanées dont vous avez besoin. Dans un cluster, configurez les mêmes comptes sur chaque nœud.

Sous Windows, assurez-vous que les utilisateurs de PDF Generator disposent du privilège [Remplacer un jeton de niveau processus](/help/forms/using/install-configure-document-services.md#grant-the-replace-a-process-level-token-privilege) et effectuez la configuration du contrôle de compte d’utilisateur applicable décrite dans [Configurer les services de document](/help/forms/using/install-configure-document-services.md#disable-user-account-control-uac).

### Conversions OpenOffice {#openoffice-conversions}

Configurez un compte utilisateur PDF Generator pour chaque instance OpenOffice pouvant s’exécuter simultanément. Installez OpenOffice à un emplacement accessible à chaque utilisateur configuré et fermez les boîtes de dialogue d’activation OpenOffice initiales pour chaque utilisateur.

Pour les systèmes UNIX, remplissez les conditions d’installation et d’autorisation des utilisateurs OpenOffice dans [Configurer les services de document](/help/forms/using/install-configure-document-services.md#preinstallationconfigurations).

## Mode Utilisateur unique sous Windows {#single-user-mode-on-windows}

Le mode Utilisateur unique permet à PDF Generator d’exécuter des conversions simultanées sous un compte utilisateur configuré.

Dans ce mode, plusieurs instances de ® Word (DOC et DOCX) et Excel (XLS et XLSX) s’exécutent sous le même utilisateur. ® PowerPoint (PPT et PPTX) ne prend pas en charge le mode mono-utilisateur. PDF Generator ne lance qu’une seule instance PowerPoint à la fois. Les conversions PowerPoint sont donc sérialisées.

Pour activer le mode utilisateur unique pour les conversions Word et Excel :

1. Dans Administration Console, accédez à **Accueil > Services > Applications et services > Gestion des services**.
1. Filtrez pour **&#x200B;**&#x200B;et sélectionnez **GeneratePDFService**.
1. Dans l’onglet **Configuration**, configurez les options suivantes :

   * Définissez **Activer le mode Utilisateur unique pour PDFMaker** sur **true**.
   * Définissez **Taille du pool PDFMaker** sur le nombre maximal d’instances Word pouvant exécuter des conversions simultanément.
   * Définissez **Activer le mode Utilisateur unique pour Native2PDF** sur **true**.
   * Définissez **Native2PDF Pool Size** sur le nombre maximal d’instances Excel qui peuvent exécuter des conversions simultanément.

1. Redémarrez le serveur AEM Forms.
