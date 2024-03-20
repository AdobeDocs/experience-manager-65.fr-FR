---
title: Configuration d’une imprimante réseau PDFG Network Printer (Windows uniquement)
description: Découvrez comment configurer une imprimante réseau PDFG Network Printer ( Windows uniquement )
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: PDF Generator
exl-id: c3fc159e-2677-4b71-b0b2-2feaf69e1a32
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 11%

---

# Configuration d’une imprimante réseau PDFG Network Printer (Windows uniquement) {#setting-up-a-pdfg-network-printer-windows-only}

L’imprimante réseau PDFG Network Printer permet aux utilisateurs de générer un document de PDF à partir de n’importe quelle application prenant en charge l’impression. Lorsqu’un utilisateur installe PDFG Network Printer, une nouvelle imprimante nommée *PDF Generator* apparaît dans la section Imprimantes du Panneau de configuration de Windows. S’il existe déjà une imprimante portant le même nom, l’utilisateur est invité à saisir un autre nom.

L’impression vers cette imprimante à partir de n’importe quelle application envoie le document (au format PostScript) à PDF Generator, qui convertit le fichier PostScript en PDF. Selon la manière dont vous avez configuré PDF Generator, il envoie le document du PDF à l’utilisateur sous forme de pièce jointe à un message électronique, transmet le document du PDF à un service ou processus d’AEM spécifié, ou effectue les deux actions.

Pour configurer une imprimante réseau PDFG Network Printer, procédez comme suit :

1. Configurez les paramètres de courrier électronique. (Voir [Configuration des paramètres de courrier électronique de l’imprimante réseau PDFG Network Printer](setting-pdfg-network-printer-windows.md#configure-email-settings-for-pdfg-network-printer).)
1. Dans Administration Console, configurez les paramètres de l’imprimante réseau PDFG Network Printer. (Voir [Configuration des paramètres de l’imprimante réseau PDFG Network Printer](setting-pdfg-network-printer-windows.md#configure-the-pdfg-network-printer-settings).)
1. Assurez-vous que vos utilisateurs sont configurés avec une adresse électronique valide dans la base de données d’AEM forms et affectez le PDFGUserPermission à chaque utilisateur. <!-- Fix broken link See Setting up and organizing users -->
1. Vérifiez que JRE6 32 bits est installé sur les ordinateurs de vos utilisateurs.
1. Installez l’imprimante sur les ordinateurs de vos utilisateurs. (Voir [Installation de l’imprimante réseau PDFG sur l’ordinateur d’un utilisateur](setting-pdfg-network-printer-windows.md#install-pdfg-network-printer-on-a-user-s-computer).)

## Configuration des paramètres de courrier électronique de l’imprimante réseau PDFG Network Printer {#configure-email-settings-for-pdfg-network-printer}

1. Dans la console d’administration, cliquez sur Services > Applications et services > Gestion des services.
1. Sur la page Gestion des services, cliquez sur provider.email_sendmail_service, spécifiez les paramètres SMTP, puis cliquez sur Enregistrer.

## Configuration des paramètres de l’imprimante réseau PDFG Network Printer {#configure-the-pdfg-network-printer-settings}

1. Dans Administration Console, cliquez sur Services > PDF Generator > PDFG Network Printer
1. Dans les listes Paramètres Adobe PDF et Paramètres de protection , sélectionnez les options à appliquer au PDF généré. Pour plus d’informations sur ces paramètres, voir [Configuration des paramètres Adobe PDF](/help/forms/using/admin-help/configuring-pdf-settings.md#configuring-adobe-pdf-settings) et [Configuration des paramètres de sécurité](/help/forms/using/admin-help/configuring-security-settings.md#configuring-security-settings).
1. Pour renvoyer les PDF convertis aux utilisateurs, sélectionnez l’option Renvoyer par courrier électronique le fichier de PDF converti à l’utilisateur et indiquez les informations suivantes :

   * Adresse électronique à utiliser pour envoyer des PDF aux utilisateurs
   * Objet du message électronique
   * En-tête, corps et pied de page du message électronique. Dans le message électronique, &lt;receivername> est remplacé par le nom complet de l’utilisateur qui a imprimé le document.

1. Pour envoyer les PDF convertis à un service ou processus AEM forms, sélectionnez l’option Transférer le PDF converti vers le service ou processus AEM spécifié et indiquez les informations suivantes :

   * Nom du service à appeler
   * Nom de l’opération du service à appeler
   * Nom du paramètre d’entrée, tel que spécifié dans le fichier component.xml du service ou du processus. Le document du PDF est utilisé comme valeur pour ce paramètre d’entrée.

1. Cliquez sur Enregistrer.

Si vous souhaitez revenir au texte du courrier électronique par défaut d’origine, cliquez sur Restaurer le contenu du courrier électronique.

## Installation de l’imprimante réseau PDFG sur l’ordinateur d’un utilisateur {#install-pdfg-network-printer-on-a-user-s-computer}

Les utilisateurs disposant du rôle Administrateur PDFG ou Utilisateur PDFG peuvent installer une imprimante réseau PDFG Network Printer. Un JDK 32 bits doit être installé sur l’ordinateur.

1. (Administrateurs de PDFG) Dans Administration Console, cliquez sur Services > PDF Generator > PDFG Network Printer.

   (Utilisateurs PDFG) Accédez à lʼadresse `http(s)://[host]:'port'/pdfgui` et cliquez sur le lien sous Installation de l’imprimante réseau PDFG Network Printer.

1. Sous Installation de l’imprimante réseau PDFG, cliquez sur le lien. Lorsque vous y êtes invité, indiquez le nom d’utilisateur et le mot de passe utilisés à l’étape 1 pour vous connecter. Un message s’affiche, indiquant que l’imprimante a bien été installée.

   ***remarque **: si le mot de passe de l’utilisateur change, l’utilisateur doit réinstaller l’imprimante réseau PDFG Network Printer sur ses ordinateurs. Vous ne pouvez pas mettre à jour le mot de passe à partir d’Administration Console.*

1. Cliquez sur OK.
