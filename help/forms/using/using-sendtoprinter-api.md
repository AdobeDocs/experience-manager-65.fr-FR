---
title: Utiliser l’API sendToPrinter
description: Utilisation du service sendToPrinter pour envoyer un document vers l’imprimante.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
exl-id: 5fb38afd-7517-494e-b084-1fdd4aef3ca4
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 58%

---

# Utiliser l’API sendToPrinter {#using-the-sendtoprinter-api}

## Présentation {#overview}

Dans AEM Forms, vous pouvez utiliser le service SendToPrinter pour envoyer un document vers l’imprimante. Le service SendToPrinter prend en charge les mécanismes d’accès aux imprimantes suivants :

* **Imprimante accessible directement** `: A printer that is installed on the same computer is called a direct accessible printer, and the computer is named printer host. This type of printer can be a local printer that is connected to the computer directly.`

* **Imprimante accessible indirectement** `: The printer that is installed on a print server is accessed from other computers. Technologies such as the common UNIX® printing system (CUPS) and the Line Printer Daemon (LPD) protocol are available to connect to a network printer. To access an indirect accessible printer, specify the print server’s IP or host name. Using this mechanism, you can send a document to an LPD URI when the network has an LPD running. The mechanism lets you route the document to any printer that is connected to the network that has an LPD running.`

  Lorsque vous envoyez un document à une imprimante, indiquez l’un des protocoles d’impression suivants : 

   * **CUPS** `: A printing protocol named common UNIX printing system. This protocol is used for UNIX operating systems and enables a computer to function as a print server. The print server accepts print requests from client applications, processes them, and sends them to configured printers. On the IBM AIX® operating system, usage of CUPS is not recommended.`
   * ``**DirectIP** `: A standard protocol for remote printing and managing print jobs. This protocol can be used locally or remotely. Print queues are not required.`
   * ``**LPD** `: A printing protocol named Line Printer Daemon protocol or Line Printer Remote (LPR) protocol. This protocol provides network print server functionality for UNIX-based systems.`
   * **SharedPrinter** `: A printing protocol that enables a computer to use a printer that is configured for that computer.`
   * **CIFS** : le service Output prend en charge le protocole d’impression CIFS (Common Internet File System).

## Utilisation du service SendToPrinter {#using-sendtoprinter-service}

Le tableau ci-dessous répertorie :

* Informations sur printerName ou printServer à utiliser pour différents protocoles.
* valeur ou exception qu’une imprimante renvoie pour différentes combinaisons de serveur d’imprimante URI et de nom de l’imprimante.

| Protocole (mécanisme d’accès) | URI du serveur d’impression (PrinterSpec.printServer) | Nom de l’imprimante (PrinterSpec.printerName) | Résultat |
|--- |--- |--- |--- |
| SharedPrinter | N’importe lequel | Vide | Exception : l’argument requis sPrinterName ne peut pas être vide. |
| SharedPrinter | N’importe lequel | Non valide | Une exception indique que l’imprimante est introuvable. |
| SharedPrinter | N’importe lequel | Valide | Tâche d’impression réussie. |
| LPD | Vide | N’importe lequel | une exception indiquant que l’argument requis sPrintServerUri ne peut pas être vide. |
| LPD | Non valide | Vide | une exception indiquant que l’argument requis sPrinterName ne peut pas être vide. |
| LPD | Non valide | Pas vide | une exception indiquant que sPrintServerUri est introuvable. |
| LPD | Valide | Non valide | une exception indiquant que l’imprimante est introuvable. |
| LPD | Valide | Valide | Tâche d’impression réussie. |
| CUPS | Vide | N’importe lequel | une exception indiquant que l’argument requis sPrintServerUri ne peut pas être vide. |
| CUPS | Non valide | N’importe lequel | une exception indiquant que l’imprimante est introuvable. |
| CUPS | Valide | N’importe lequel | Tâche d’impression réussie. |
| DirectIP | Vide | N’importe lequel | une exception indiquant que l’argument requis sPrintServerUri ne peut pas être vide. |
| DirectIP | Non valide | N’importe lequel | une exception indiquant que l’imprimante est introuvable. |
| DirectIP | Valide | N’importe lequel | Tâche d’impression réussie. |
| CIFS | Valide | Vide | Tâche d’impression réussie. |
| CIFS | Non valide | N’importe lequel | une erreur inconnue lors de l’impression à l’aide de CIF. |
| CIFS | Vide | N’importe lequel | une exception indiquant que l’argument requis sPrintServerUri ne peut pas être vide. |

## Prise en charge de l’authentification {#authentication-support}

L’authentification est prise en charge uniquement pour l’impression CIF. Pour authentifier, indiquez vos nom d’utilisateur, mot de passe et domaine dans PrinterSpec. Vous pouvez chiffrer un mot de passe à l’aide du service Granite CryptoSupport AEM en procédant de la manière suivante :

1. Accédez à https://&lt;server>:&lt;port>/system/console.

1. Accédez à **[!UICONTROL Général]** > **[!UICONTROL Crypto Support]**.

1. Entrez du texte brut puis cliquez sur **[!UICONTROL Protection]**.
