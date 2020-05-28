---
title: Conversion de fichiers à l’aide de PDF Generator
seo-title: Conversion de fichiers à l’aide de PDF Generator
description: Découvrez comment convertir des fichiers à l’aide de PDF Generator.
seo-description: Découvrez comment convertir des fichiers à l’aide de PDF Generator.
uuid: 295afb8f-130a-44f5-b0ab-e4c93c0c9e52
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 999ae2be-56ba-48c1-861b-8d4c991a0206
translation-type: tm+mt
source-git-commit: 68ea2335a8466c3c23b766efb1a04b6a38d7f670
workflow-type: tm+mt
source-wordcount: '1180'
ht-degree: 91%

---


# Conversion de fichiers à l’aide de PDF Generator{#converting-files-using-pdf-generator}

Vous pouvez utiliser les pages Web de PDF Generator pour convertir des fichiers.

## Création d’un fichier PDF {#create-a-pdf-file}

1. Dans Administration Console, cliquez sur Services > PDF Generator > Créer un fichier PDF.
1. Cliquez sur Parcourir pour rechercher et sélectionner le fichier.

   >[!NOTE]
   >
   >PDF Generator peut automatiquement détecter le type de fichier des documents .doc, .xls, .ppt et .rtf, même lorsque l’extension de ces derniers n’apparaît pas dans le nom du fichier. Cette fonctionnalité ne s’applique pas aux fichiers .docx, .xlsx et .pptx.

1. Sous Paramètres de configuration, sélectionnez Utiliser des paramètres personnalisés ou Télécharger le fichier de paramètres.

   * Si vous utilisez des paramètres personnalisés, sélectionnez un paramètre Adobe PDF, un paramètre de sécurité et un paramètre de type de fichier, puis spécifiez un délai d’expiration.

      Les paramètres Adobe PDF s’appliquent uniquement à des conversions PS/EPS/PRN en PDF, Image en PDF avec la reconnaissance optique des caractères activée et Natif en PDF. Le paramètre de délai d’expiration définit la durée maximale de la conversion. La valeur par défaut est de 270 secondes. Ces paramètres ne sont pas utilisés dans les conversions Image en PDF et OpenOffice en PDF.

   * Si vous téléchargez un fichier de paramètres, saisissez son chemin d’accès et son nom dans la zone ou cliquez sur Parcourir pour le rechercher et le sélectionner.

1. (Facultatif) Sous Fichier de métadonnées XMP, saisissez le chemin d’accès et le nom du fichier XMP ou cliquez sur Parcourir pour rechercher et sélectionner le fichier. Il est possible d’utiliser un fichier XMP pour y inclure des métadonnées standard (voir [A propos des fichiers XMP](converting-files-using-pdf-generator.md#about-xmp-files)).
1. Cliquez sur Créer. Lorsque le fichier est créé, un lien vers celui-ci s’affiche. Si une erreur survient lors de la conversion, un avertissement s’affiche. Si vous créez un fichier Postscript, cet avertissement contient également un lien vers le fichier journal.
1. Cliquez sur le lien correspondant au fichier PDF. Le fichier s’ouvre dans Acrobat.

### A propos des fichiers XMP {#about-xmp-files}

Les documents créés par PDF Generator dans Acrobat 5.0 ou versions ultérieures contiennent les métadonnées de ceux-ci au format XML. Les *métadonnées* comprennent des informations relatives au document et à son contenu, comme le nom de l’auteur, les mots-clés et les droits d’auteurs, que les utilitaires de recherche peuvent utiliser.

Les métadonnées contiennent (sans s’y limiter) des informations qui s’affichent également dans l’onglet Description de la boîte de dialogue Propriétés du document dans Acrobat. Les modifications apportées dans l’onglet Description sont répercutées sur les métadonnées du document. Il est possible d’étendre et de modifier ces dernières à l’aide de produits tiers.

La plateforme XMP (Extensible Metadata Platform, plateforme de métadonnées extensible) offre aux applications Adobe une structure XML commune qui normalise la création, le traitement et l’échange des métadonnées d’un document dans les flux de travail de publication. Vous pouvez enregistrer et importer le code source XML des métadonnées du document au format XMP, ce qui facilite le partage des métadonnées entre différents documents. Pour plus de détails sur les fichiers XMP, consultez le document sur la plate-forme XMP [(Extensible Metadata Platform)](https://www.adobe.com/products/xmp/) et le [centre des développeurs Adobe XMP](https://www.adobe.com/devnet/xmp.html).

Vous pouvez créer des fichiers XMP dans Acrobat.

## Conversion d’un fichier HTML ou ZIP au format PDF {#convert-an-html-file-or-zip-file-to-pdf}

PDF Generator permet de convertir les types de fichiers suivants au format Adobe PDF :

* fichiers HTML, que vous pouvez convertir en téléchargeant un fichier HTML ou en spécifiant l’URL d’une page ou d’un site Web ;
* fichiers d’archive (ZIP), qui peuvent contenir des fichiers HTML, des fichiers image, ou les deux.

Si le fichier ZIP contient plusieurs fichiers HTML au niveau le plus bas de son arborescence, il doit également contenir un fichier index.htm ou index.html.

>[!NOTE]
>
>* la conversion de fichiers HTML au format PDF requiert certaines polices dans le répertoire des polices système. Sur les systèmes Linux, Solaris et AIX, le répertoire des polices système doit contenir la police Courier. Sur les systèmes Windows, le répertoire des polices système doit contenir Times New Roman.
   >
   > 
* (Système UNIX uniquement) L’une des polices japonaises suivantes doit être disponible sur le serveur AEM Forms pour convertir une page Web contenant une police japonaise en document PDF.
   >
   >   
   * &quot;Sazanami Gothic&quot;
   >   * &quot;Kozuka Gothic Pro-VI&quot;
   >   * &quot;Kozuka Mincho Pro-VI&quot;
   >   * &quot;Sazanami Gothic&quot;
   >   * &quot;Kozuka Mincho Pr6N&quot;
   >   * &quot;Sazanami Mincho&quot;
   >   * &quot;Adobe Heiti Std&quot;
   >   * &quot;Adobe Song Std&quot;
>* Pour télécharger un fichier à partir du système de fichiers local, utilisez l’option Télécharger le fichier de la page HTML en PDF.


1. Dans Administration Console, cliquez sur Services > PDF Generator > HTML en PDF.
1. Spécifiez le fichier à convertir en exécutant l’une des tâches suivantes :

   * Dans le champ Télécharger, saisissez le chemin d’accès et le nom du fichier HTML ou ZIP, ou cliquez sur Parcourir pour le rechercher et le sélectionner.
   * Dans le champ Spécifier l’URL, saisissez l’URL de la page ou du site Web à convertir.
   >[!NOTE]
   >
   >le fichier que vous convertissez doit porter l’extension .html, .htm ou .zip.

1. Définissez les paramètres de configuration :

   * Pour utiliser des paramètres personnalisés, sélectionnez Utiliser des paramètres personnalisés, indiquez les paramètres de type de fichier et de protection, et définissez un délai d’expiration. La valeur par défaut est de 270 secondes.
   >[!NOTE]
   >
   >si vous avez configuré le service Generate PDF pour utiliser Acrobat WebCapture, les paramètres de type de fichier que vous sélectionnez sur cette page n’ont aucune incidence sur le PDF produit. Au lieu de cela, apportez les modifications appropriées à la version d’Acrobat installée sur le serveur.

   * Pour utiliser un fichier de paramètres existant, sélectionnez Télécharger le fichier de paramètres et cliquez sur Parcourir pour accéder au fichier.


1. Pour télécharger un fichier XMP, cliquez sur Parcourir et accédez à l’emplacement du fichier. Il est possible d’utiliser un fichier XMP pour y inclure des métadonnées standard (voir [A propos des fichiers XMP](converting-files-using-pdf-generator.md#about-xmp-files)).
1. Cliquez sur Créer. Lorsque le fichier est créé, un lien vers le fichier PDF s’affiche.
1. Cliquez sur le lien pour afficher le document PDF dans Acrobat.

## Exportation d’un fichier PDF dans un autre format de fichier (Windows uniquement) {#export-a-pdf-file-to-another-file-format-windows-only}

Vous pouvez exporter des fichiers PDF dans différents formats de fichiers, comme décrit dans le chapitre consacré au service Generate PDF du [Guide de référence des services](https://www.adobe.com/go/learn_aemforms_services_63).

1. Dans Administration Console, cliquez sur Services > PDF Generator > Exporter un PDF.
1. Cliquez sur Parcourir pour déterminer l’emplacement du fichier PDF à exporter.
1. Dans la liste Exporter le fichier PDF vers, sélectionnez le format vers lequel exporter le fichier PDF.
1. Dans la zone Spécifier un délai d’expiration, saisissez le délai d’expiration de l’application. La valeur par défaut est de 270 secondes.

   La durée de conversion affichée une fois le fichier converti peut être supérieure à la valeur spécifiée ici. En effet, elle inclut le temps passé à attendre le thread ou le processus, la durée de conversion du fichier et le temps pris par le convertisseur de secours (le cas échéant). time. La valeur du paramètre Spécifier un délai d’expiration ne reflète que le temps de conversion du fichier.

1. (Optional) In the **Specify custom Preflight profile** option, click Browse, and select a [custom Preflight profile](https://helpx.adobe.com/acrobat/using/preflight-profiles-acrobat-pro.html). Les profils de contrôle en amont ne sont utilisés que lors de la conversion de documents au format d’archive PDF (PDF/A).
1. Cliquez sur Exporter. Lorsque la conversion est terminée, un lien renvoyant au fichier exporté s’affiche.
1. Cliquez sur ce lien pour afficher le fichier converti.

## Optimisation d’un fichier PDF (Windows Only) {#optimize-a-pdf}

PDF Generator permet de réduire la taille des fichiers PDF.

>[!NOTE]
>
>l’optimisation d’un document numériquement signé supprime et invalide les signatures numériques.

1. Dans Administration Console, cliquez sur Services > PDF Generator > Optimiser un PDF.
1. Cliquez sur Parcourir pour localiser le fichier PDF à optimiser.
1. Définissez les paramètres de configuration :

   * Pour utiliser des paramètres personnalisés, sélectionnez Utiliser des paramètres personnalisés, indiquez les paramètres de protection et de type de fichier, et définissez un délai d’expiration. La valeur par défaut est de 270 secondes.
   * Pour utiliser un fichier de paramètres existant, sélectionnez Télécharger le fichier de paramètres et cliquez sur Parcourir pour accéder au fichier.

1. Cliquez sur Créer.

