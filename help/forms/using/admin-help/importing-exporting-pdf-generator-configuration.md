---
title: Importation et exportation des fichiers de configuration de PDF Generator
seo-title: Importation et exportation des fichiers de configuration de PDF Generator
description: Découvrez comment importer et exporter des fichiers de configuration PDF Generator.
seo-description: Découvrez comment importer et exporter des fichiers de configuration PDF Generator.
uuid: 3367253b-d222-4c5f-9455-a1810d96112e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e25c1b35-73eb-4353-8e39-a2d4cdccd101
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 98%

---


# Importation et exportation des fichiers de configuration de PDF Generator {#importing-and-exporting-pdf-generator-configuration-files}

Le fichier de configuration contient les informations de conversion de PDF Generator, y compris les paramètres de PDF, de type de fichier et de sécurité.

>[!NOTE]
>
>vous ne pouvez pas modifier le paramètre de délai d’expiration de PDF Generator en important un fichier native2pdfconfig.xml personnalisé. Le paramètre de délai d’expiration dans ce fichier est donné à titre purement indicatif et affiche le paramètre actuel dans PDF Generator. Pour le modifier, consultez la section Définition des paramètres de performance de PDF Generator dans [Installation et déploiement d’AEM forms](https://www.adobe.com/go/learn_aemforms_installJBoss_63).

## Exportation du fichier de configuration {#export-your-current-configuration-file}

1. Dans Administration Console, sélectionnez Services > PDF Generator > Fichiers de configuration > Exporter la configuration.
1. Pour exporter les paramètres, sélectionnez l’option appropriée :

   * Pour exporter tous les paramètres nommés, sélectionnez Télécharger la configuration complète.
   * Pour n’exporter qu’un seul paramètre Adobe PDF, de protection ou de type de fichier, sélectionnez Télécharger la configuration minimale.

      Si vous exportez une configuration minimale, sélectionnez les paramètres Adobe PDF, de sécurité et de type de fichier voulus.

1. Cliquez sur Télécharger, puis enregistrez le fichier XML à l’emplacement approprié.

## Importation d’un fichier de configuration  {#import-a-configuration-file}

>[!NOTE]
>
>votre système est reconfiguré en fonction des informations contenues dans le fichier importé.

1. Dans Administration Console, sélectionnez Services > PDF Generator > Fichiers de configuration > Importer la configuration.
1. Sélectionnez Importer un fichier de configuration existant.
1. Pour définir l’emplacement du fichier, dans le champ Fichier de configuration, cliquez sur Parcourir pour localiser et sélectionner le fichier, puis cliquez sur **Importer**.

## Conversion de tous les calques des fichiers AutoCAD  {#convert-all-layers-within-autocad-files}

Par défaut, PDF Generator ne convertit que le calque par défaut des fichiers AutoCAD au format PDF et non l’ensemble des calques des fichiers. Pour convertir l’ensemble des calques, suivez la procédure ci-dessous.

1. Dans Administration Console, sélectionnez Services > PDF Generator > Fichiers de configuration > Exporter la configuration.
1. Sélectionnez Télécharger la configuration complète et cliquez sur Télécharger.
1. Dans un éditeur de texte, ouvrez le fichier téléchargé, puis sous la balise `AutoCAD` de la balise `PDFMaker`, ajoutez le texte `convertAllPages="true"`.
1. Dans Administration Console, sélectionnez Services > PDF Generator > Fichiers de configuration > Importer la configuration.
1. Sélectionnez Importer un fichier de configuration existant, spécifiez le fichier mis à jour, puis cliquez sur Importer.

   Tous les calques d’un fichier AutoCAD converti à l’aide du fichier de configuration modifié seront traités.

## Rétablissement des paramètres de configuration d’origine installés avec PDF Generator  {#reset-your-configuration-to-the-original-settings-installed-with-pdf-generator}

1. Dans Administration Console, sélectionnez Services > PDF Generator > Fichiers de configuration > Importer la configuration.
1. Sélectionnez Réinitialiser la configuration pour rétablir les paramètres par défaut et cliquez sur Importer.

