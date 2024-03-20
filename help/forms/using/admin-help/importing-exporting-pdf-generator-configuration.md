---
title: Importer et exporter des fichiers de configuration de PDF Generator
description: Découvrez comment importer et exporter des fichiers de configuration de PDF Generator.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: PDF Generator
exl-id: b363b23a-29bb-4ea4-a8f2-5ba9fe3c7b27
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 14%

---

# Importer et exporter des fichiers de configuration de PDF Generator {#importing-and-exporting-pdf-generator-configuration-files}

Le fichier de configuration contient les informations de conversion du PDF Generator, y compris le PDF, le type de fichier et les paramètres de sécurité.

>[!NOTE]
>
>Vous ne pouvez pas modifier le délai d’expiration de PDF Generator en important un fichier native2pdfconfig.xml personnalisé. Le paramètre de délai d’expiration de ce fichier est fourni à titre d’information uniquement et affiche le paramètre actuel dans PDF Generator. Pour le réglage du délai d’expiration, reportez-vous à « Réglage des paramètres de performance de PDF Generator » dans [Installation et déploiement d’AEM Forms](https://www.adobe.com/go/learn_aemforms_installJBoss_63_fr).

## Exportation du fichier de configuration actuel {#export-your-current-configuration-file}

1. Dans Administration Console, cliquez sur Services > PDF Generator > Fichiers de configuration > Exporter la configuration.
1. Pour exporter les paramètres, sélectionnez l’option appropriée :

   * Pour exporter tous les paramètres nommés, sélectionnez Télécharger la configuration complète.
   * Pour n’exporter qu’un seul paramètre Adobe PDF, un seul paramètre de sécurité ou un seul paramètre de type de fichier, sélectionnez Télécharger la configuration minimale.

     Si vous exportez une configuration minimale, sélectionnez les paramètres Adobe PDF, sécurité et type de fichier à exporter.

1. Cliquez sur Télécharger , puis enregistrez le fichier XML à l’emplacement approprié.

## Importation d’un fichier de configuration {#import-a-configuration-file}

>[!NOTE]
>
>Votre système sera reconfiguré en fonction des informations contenues dans le fichier importé.

1. Dans Administration Console, cliquez sur Services > PDF Generator > Fichiers de configuration > Importer la configuration.
1. Sélectionnez Importer un fichier de configuration existant.
1. Pour spécifier l’emplacement du fichier dans la zone Fichier de configuration, cliquez sur Parcourir pour rechercher et sélectionner le fichier, puis cliquez sur **Importer**.

## Conversion de tous les calques des fichiers AutoCAD {#convert-all-layers-within-autocad-files}

Par défaut, PDF Generator convertit uniquement le calque par défaut des fichiers AutoCAD en PDF au lieu de tous les calques du fichier. Pour convertir tous les calques, procédez comme suit.

1. Dans Administration Console, cliquez sur Services > PDF Generator > Fichiers de configuration > Exporter la configuration.
1. Sélectionnez Télécharger la configuration complète, puis cliquez sur Télécharger.
1. Dans un éditeur de texte, ouvrez le fichier téléchargé, puis sous la balise `AutoCAD` de la balise `PDFMaker`, ajoutez le texte `convertAllPages="true"`.
1. Dans Administration Console, cliquez sur Services > PDF Generator > Fichiers de configuration > Importer la configuration.
1. Sélectionnez Importer un fichier de configuration existant, spécifiez le fichier mis à jour, puis cliquez sur Importer.

   Tous les calques sont convertis pour les fichiers AutoCAD convertis à l’aide du fichier de configuration modifié.

## Réinitialisez votre configuration aux paramètres d’origine installés avec PDF Generator. {#reset-your-configuration-to-the-original-settings-installed-with-pdf-generator}

1. Dans Administration Console, cliquez sur Services > PDF Generator > Fichiers de configuration > Importer la configuration.
1. Sélectionnez Reset Configuration To Default Settings , puis cliquez sur Importer.
