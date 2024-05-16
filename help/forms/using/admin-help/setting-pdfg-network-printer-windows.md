---
title: Configuration d’une imprimante réseau PDFG Network Printer (Windows uniquement)
description: Découvrez comment configurer une imprimante réseau PDFG Network Printer (Windows uniquement).
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: PDF Generator
exl-id: c3fc159e-2677-4b71-b0b2-2feaf69e1a32
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '604'
ht-degree: 100%

---

# Configuration d’une imprimante réseau PDFG Network Printer (Windows uniquement) {#setting-up-a-pdfg-network-printer-windows-only}

L’imprimante réseau PDFG Network Printer permet aux utilisateurs et utilisatrices de générer un document PDF à partir de n’importe quelle application dotée de fonctions d’impression. Lorsqu’un utilisateur installe PDFG Network Printer, une nouvelle imprimante nommée *PDF Generator* apparaît dans la section Imprimantes du Panneau de configuration de Windows. S’il existe déjà une imprimante portant le même nom, l’utilisateur ou l’utilisatrice doit saisir un autre nom.

Lorsque vous imprimez un document à partir d’une application quelconque, vous envoyez ce document (au format PostScript) à PDF Generator, qui convertit alors le fichier PostScript en PDF. Selon sa configuration, PDF Generator envoie le document PDF à l’utilisateur ou l’utilisatrice en pièce jointe à un e-mail, transmet le document PDF à un service ou processus AEM Forms spécifié ou effectue les deux actions.

Pour configurer une imprimante réseau PDFG Network Printer, procédez comme suit :

1. Configurez les paramètres d’e-mail. (Voir [Configuration des paramètres d’e-mail de l’imprimante réseau PDFG Network Printer](setting-pdfg-network-printer-windows.md#configure-email-settings-for-pdfg-network-printer)).
1. Dans la console d’administration, configurez les paramètres de l’imprimante réseau PDFG Network Printer. (Voir [Configuration des paramètres de l’imprimante réseau PDFG Network Printer](setting-pdfg-network-printer-windows.md#configure-the-pdfg-network-printer-settings)).
1. Vérifiez que vos utilisateurs et utilisatrices sont configurés avec un e-mail correct dans la base de données AEM Forms et affectez le droit PDFGUserPermission à chaque utilisateur et utilisatrice<!-- Fix broken link See Setting up and organizing users -->.
1. Vérifiez que JRE6 32 bits est installé sur les ordinateurs de vos utilisateurs et utilisatrices.
1. Installez l’imprimante sur les ordinateurs de vos utilisateurs et utilisatrices. (Voir [Installation de l’imprimante réseau PDFG Network Printer sur l’ordinateur d’un utilisateur ou d’une utilisatrice](setting-pdfg-network-printer-windows.md#install-pdfg-network-printer-on-a-user-s-computer)).

## Configuration des paramètres d’e-mail de l’imprimante réseau PDFG Network Printer {#configure-email-settings-for-pdfg-network-printer}

1. Dans la console d’administration, cliquez sur Services > Applications et services > Gestion des services.
1. Sur la page Gestion des services, cliquez sur provider.email_sendmail_service, spécifiez les paramètres SMTP puis cliquez sur Enregistrer.

## Configuration des paramètres de l’imprimante réseau PDFG Network Printer {#configure-the-pdfg-network-printer-settings}

1. Dans la console d’administration, cliquez sur Services > PDF Generator > PDFG Network Printer
1. Dans les listes Paramètres Adobe PDF et Paramètres de sécurité , sélectionnez les options à appliquer au PDF généré. Pour plus d’informations sur ces paramètres, voir [Configuration des paramètres Adobe PDF](/help/forms/using/admin-help/configuring-pdf-settings.md#configuring-adobe-pdf-settings) et [Configuration des paramètres de protection](/help/forms/using/admin-help/configuring-security-settings.md#configuring-security-settings).
1. Pour renvoyer les PDF convertis aux utilisateurs et utilisatrices, sélectionnez l’option Renvoyer par e-mail le fichier PDF converti à l’utilisateur et indiquez les informations suivantes :

   * L’e-mail à utiliser pour envoyer des PDF aux utilisateurs et utilisatrices.
   * L’objet de l’e-mail.
   * L’en-tête, le corps du message et le pied de page de l’e-mail. Dans l’e-mail, &lt;receiverName> est remplacé par le nom complet de l’utilisateur ou de l’utilisatrice qui a imprimé le document.

1. Pour envoyer les PDF convertis à un service ou processus AEM Forms, sélectionnez l’option Transférer le PDF converti vers le service ou processus AEM Forms spécifié et indiquez les informations suivantes :

   * Le nom du service à appeler.
   * Le nom de l’opération du service à appeler.
   * Le nom du paramètre d’entrée, tel que spécifié dans le fichier component.xml du service ou du processus. Le document PDF est utilisé comme valeur de ce paramètre d’entrée.

1. Cliquez sur Enregistrer.

Si vous souhaitez rétablir l’e-mail par défaut, cliquez sur Rétablir le contenu de l’e-mail.

## Installation de l’imprimante réseau PDFG Network Printer sur l’ordinateur d’un utilisateur ou d’une utilisatrice {#install-pdfg-network-printer-on-a-user-s-computer}

Les utilisateurs et utilisatrices disposant du rôle Administrateur ou administratrice PDFG ou Utilisateur ou utilisatrice PDFG peuvent installer une imprimante réseau PDFG Network Printer. Un JDK 32 bits doit être installé sur l’ordinateur.

1. (Administrateurs et administratrices PDFG) Dans la console d’administration, cliquez sur Services > PDF Generator  > PDFG Network Printer.

   (Utilisateurs PDFG) Accédez à lʼadresse `http(s)://[host]:'port'/pdfgui` et cliquez sur le lien sous Installation de l’imprimante réseau PDFG Network Printer.

1. Sous Installation de l’imprimante réseau PDFG Network Printer, cliquez sur le lien. Lorsque le système vous demande de saisir les informations de votre compte utilisateur, indiquez le nom d’utilisateur et le mot de passe utilisés à l’étape 1 pour vous connecter. Un message s’affiche, indiquant que l’imprimante a bien été installée.

   ***Remarque ** : si le mot de passe utilisateur est modifié, les utilisateurs et utilisatrices devront réinstaller l’imprimante réseau PDFG Network Printer sur leur ordinateur. Vous ne pouvez pas mettre à jour le mot de passe à partir de la console d’administration.*

1. Cliquez sur OK.
