---
title: Configuration d’une imprimante réseau PDFG Network Printer (Windows uniquement)
seo-title: Configuration d’une imprimante réseau PDFG Network Printer (Windows uniquement)
description: Découvrez comment installer une imprimante réseau PDFG Network Printer (Windows uniquement)
seo-description: Découvrez comment installer une imprimante réseau PDFG Network Printer (Windows uniquement)
uuid: 13b8481e-5ef0-4a07-9602-7bc4d9e05dd4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7620e5e4-022e-49b2-8cfe-d5eec8ab99d7
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 97%

---


# Configuration d’une imprimante réseau PDFG Network Printer (Windows uniquement) {#setting-up-a-pdfg-network-printer-windows-only}

L’imprimante réseau PDFG Network Printer permet aux utilisateurs de générer un document PDF à partir de n’importe quelle application dotée de fonctions d’impression. Lorsqu’un utilisateur installe PDFG Network Printer, une nouvelle imprimante nommée *PDF Generator* apparaît dans la section Imprimantes du Panneau de configuration de Windows. S’il existe déjà une imprimante portant ce nom, l’utilisateur est invité à saisir un autre nom.

Lorsque vous imprimez un document à partir d’une application quelconque, vous envoyez ce document (au format PostScript) à PDF Generator qui convertit le fichier PostScript en PDF. Selon sa configuration, PDF Generator envoie le document PDF à l’utilisateur en pièce jointe à un courrier électronique, transmet le document PDF à un service ou processus AEM forms spécifié ou effectue les deux actions.

Pour configurer une imprimante réseau PDFG Network Printer, procédez comme suit :

1. Configurez les paramètres de courrier électronique (voir [Configuration des paramètres de courrier électronique pour l’imprimante réseau PDFG Network Printer](setting-pdfg-network-printer-windows.md#configure-email-settings-for-pdfg-network-printer)).
1. Dans Administration Console, configurez les paramètres de l’imprimante réseau PDFG Network Printer (voir [Configuration des paramètres de l’imprimante réseau PDFG Network Printer](setting-pdfg-network-printer-windows.md#configure-the-pdfg-network-printer-settings)).
1. Vérifiez que vos utilisateurs sont configurés avec une adresse électronique correcte dans la base de données AEM forms et affectez le droit PDFGUserPermission à chaque utilisateur <!-- Fix broken link See Setting up and organizing users -->
1. Assurez-vous que JRE6 32 est installé sur les ordinateurs de vos utilisateurs.
1. Installez l’imprimante sur les ordinateurs de vos utilisateurs (voir [Installation de l’imprimante réseau PDFG sur l’ordinateur d’un utilisateur](setting-pdfg-network-printer-windows.md#install-pdfg-network-printer-on-a-user-s-computer)).

## Configuration des paramètres de courrier électronique pour l’imprimante réseau PDFG Network Printer {#configure-email-settings-for-pdfg-network-printer}

1. Dans Administration Console, cliquez sur Services > Applications et services > Gestion des services.
1. Sur la page Gestion des services, cliquez sur provider.email_sendmail_service, spécifiez les paramètres SMTP et cliquez sur Enregistrer.

## Configuration des paramètres de l’imprimante réseau PDFG Network Printer  {#configure-the-pdfg-network-printer-settings}

1. Dans Administration Console, cliquez sur Services > PDF Generator > PDFG Network Printer.
1. Dans les listes Paramètres Adobe PDF et Paramètres de protection, sélectionnez les options à appliquer au PDF généré. Pour plus d’informations sur ces paramètres, voir [Configuration des paramètres Adobe PDF](/help/forms/using/admin-help/configuring-pdf-settings.md#configuring-adobe-pdf-settings) et [Configuration des paramètres de protection](/help/forms/using/admin-help/configuring-security-settings.md#configuring-security-settings).
1. Pour renvoyer les PDF convertis aux utilisateurs, sélectionnez l’option Renvoyez par courrier électronique le fichier PDF converti à l’utilisateur et spécifiez les informations suivantes :

   * l’adresse de courrier électronique à utiliser pour envoyer des fichiers PDF aux utilisateurs ;
   * le sujet du courrier électronique ;
   * l’en-tête, le corps du message et le pied de page de votre courrier électronique. Dans le courrier électronique, &lt;receiverName> est remplacé par le nom complet de l’utilisateur qui a imprimé le document.

1. Pour envoyer les PDF convertis à un service ou processus AEM forms, sélectionnez l’option Transférer le PDF converti vers le service ou processus AEM forms spécifié et indiquez les informations suivantes :

   * le nom du service à appeler ;
   * le nom de l’opération du service à appeler ;
   * le nom du paramètre d’entrée, tel qu’il figure dans le fichier component.xml du service ou processus. Le document PDF sera utilisé comme valeur de ce paramètre.

1. Cliquez sur Enregistrer.

Si vous souhaitez rétablir le message électronique par défaut, cliquez sur Rétablir le contenu du courrier électronique.

## Installation de l’imprimante réseau PDFG sur l’ordinateur d’un utilisateur  {#install-pdfg-network-printer-on-a-user-s-computer}

Les utilisateurs qui possèdent le rôle Administrateur de PDFG ou Utilisateur de PDFG peuvent installer une imprimante réseau PDFG. Vous devez disposer d’un JDK 32 bits installé sur l’ordinateur.

1. (Administrateurs de PDFG) Dans Administration Console, cliquez sur Services > PDF Generator > PDFG Network Printer.

   (Utilisateurs de PDFG) Accédez à `http(s)://[host]:'port'/pdfgui` et cliquez sur le lien sous Installation de l’imprimante réseau PDFG Network Printer.

1. Sous Installation de l’imprimante réseau PDFG, cliquez sur le lien. Lorsque vous êtes invité à saisir les informations de votre compte utilisateur, indiquez le nom d’utilisateur et le mot de passe utilisés à l’étape 1 pour vous connecter. Un message apparaît, indiquant que l’installation de l’imprimante est terminée.

   ***Remarque ** : si le mot de passe utilisateur est modifié, les utilisateurs devront réinstaller l’imprimante réseau PDFG Network Printer sur leurs ordinateurs. Vous ne pouvez pas mettre à jour le mot de passe à partir d’Administration Console.*

1. Cliquez sur OK.

