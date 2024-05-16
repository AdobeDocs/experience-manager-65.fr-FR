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
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '372'
ht-degree: 100%

---

# Importer et exporter des fichiers de configuration de PDF Generator {#importing-and-exporting-pdf-generator-configuration-files}

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
>Votre système est reconfiguré en fonction des informations contenues dans le fichier importé.

1. Dans la console d’administration, cliquez sur Services > PDF Generator > Fichiers de configuration > Importer la configuration.
1. Sélectionnez Importer un fichier de configuration existant.
1. Pour définir l’emplacement du fichier, dans le champ Fichier de configuration, cliquez sur Parcourir pour localiser et sélectionner le fichier, puis cliquez sur **Importer**.

## Conversion de tous les calques des fichiers AutoCAD {#convert-all-layers-within-autocad-files}

Par défaut, PDF Generator ne convertit que le calque par défaut des fichiers AutoCAD au format PDF et non l’ensemble des calques des fichiers. Pour convertir l’ensemble des calques, suivez la procédure ci-dessous.

1. Dans la console d’administration, cliquez sur Services > PDF Generator > Fichiers de configuration > Exporter la configuration.
1. Sélectionnez Télécharger la configuration complète, puis cliquez sur Télécharger.
1. Dans un éditeur de texte, ouvrez le fichier téléchargé, puis sous la balise `AutoCAD` de la balise `PDFMaker`, ajoutez le texte `convertAllPages="true"`.
1. Dans la console d’administration, cliquez sur Services > PDF Generator > Fichiers de configuration > Importer la configuration.
1. Sélectionnez Importer un fichier de configuration existant, spécifiez le fichier mis à jour, puis cliquez sur Importer.

   Tous les calques d’un fichier AutoCAD converti à l’aide du fichier de configuration modifié seront traités.

## Rétablissement des paramètres de configuration d’origine installés avec PDF Generator {#reset-your-configuration-to-the-original-settings-installed-with-pdf-generator}

1. Dans la console d’administration, cliquez sur Services > PDF Generator > Fichiers de configuration > Importer la configuration.
1. Sélectionnez Réinitialiser la configuration pour rétablir les paramètres par défaut et cliquez sur Importer.
