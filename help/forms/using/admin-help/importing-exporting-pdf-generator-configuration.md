---
title: Importer et exporter des fichiers de configuration de PDF Generator
description: Découvrez comment importer et exporter des fichiers de configuration PDF Generator.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: PDF Generator
exl-id: b363b23a-29bb-4ea4-a8f2-5ba9fe3c7b27
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
source-wordcount: '390'
ht-degree: 100%
---
# Importer et exporter des fichiers de configuration de PDF Generator {#importing-and-exporting-pdf-generator-configuration-files}

>[!NOTE]
> 
> Vérifiez que l’utilisateur ou l’utilisatrice dispose de droits d’administration pour accéder à la console d’administration.

Le fichier de configuration contient les informations de conversion de PDF Generator, y compris les paramètres de PDF, de type de fichier et de sécurité.

>[!NOTE]
>
>Vous ne pouvez pas modifier le paramètre de délai d’expiration de PDF Generator en important un fichier native2pdfconfig.xml personnalisé. Le paramètre de délai d’expiration dans ce fichier est donné à titre purement indicatif et affiche le paramètre actuel dans PDF Generator. Pour le réglage du délai d’expiration, reportez-vous à « Réglage des paramètres de performance de PDF Generator » dans [Installation et déploiement d’AEM Forms](https://www.adobe.com/go/learn_aemforms_installJBoss_63_fr).

## Exportation du fichier de configuration {#export-your-current-configuration-file}

1. Dans la console d’administration, cliquez sur Services > PDF Generator > Fichiers de configuration > Exporter la configuration.
1. Pour exporter les paramètres, sélectionnez l’option appropriée :

   * Pour exporter tous les paramètres nommés, sélectionnez Télécharger la configuration complète.
   * Pour n’exporter qu’un seul paramètre Adobe PDF, de sécurité ou de type de fichier, sélectionnez Télécharger la configuration minimale.

     Si vous exportez une configuration minimale, sélectionnez les paramètres Adobe PDF, de sécurité et de type de fichier voulus.

1. Cliquez sur Télécharger, puis enregistrez le fichier XML à l’emplacement approprié.

## Importation d’un fichier de configuration {#import-a-configuration-file}

>[!NOTE]
>
>Votre système sera reconfiguré en fonction des informations contenues dans le fichier importé.

1. Dans la console d’administration, cliquez sur Services > PDF Generator > Fichiers de configuration > Importer la configuration.
1. Sélectionnez Importer un fichier de configuration existant.
1. Pour définir l’emplacement du fichier, dans le champ Fichier de configuration, cliquez sur Parcourir pour localiser et sélectionner le fichier, puis cliquez sur **Importer**.

## Conversion de tous les calques des fichiers AutoCAD {#convert-all-layers-within-autocad-files}

Par défaut, PDF Generator ne convertit que le calque par défaut des fichiers AutoCAD au format PDF et non l’ensemble des calques du fichier. Pour convertir l’ensemble des calques, suivez la procédure ci-dessous.

1. Dans la console d’administration, cliquez sur Services > PDF Generator > Fichiers de configuration > Exporter la configuration.
1. Sélectionnez Télécharger la configuration complète, puis cliquez sur Télécharger.
1. Dans un éditeur de texte, ouvrez le fichier téléchargé, puis sous la balise `AutoCAD` de la balise `PDFMaker`, ajoutez le texte `convertAllPages="true"`.
1. Dans la console d’administration, cliquez sur Services > PDF Generator > Fichiers de configuration > Importer la configuration.
1. Sélectionnez Importer un fichier de configuration existant, spécifiez le fichier mis à jour, puis cliquez sur Importer.

   Tous les calques d’un fichier AutoCAD converti à l’aide du fichier de configuration modifié seront traités.

## Rétablissement des paramètres de configuration d’origine installés avec PDF Generator {#reset-your-configuration-to-the-original-settings-installed-with-pdf-generator}

1. Dans la console d’administration, cliquez sur Services > PDF Generator > Fichiers de configuration > Importer la configuration.
1. Sélectionnez Réinitialiser la configuration aux paramètres par défaut et cliquez sur Importer.
