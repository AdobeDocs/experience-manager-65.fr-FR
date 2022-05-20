---
title: Utilisation de l’API sendToPrinter
seo-title: Using the sendToPrinter API
description: Utilisation du service sendToPrinter pour envoyer un document vers l’imprimante.
seo-description: Using the sendToPrinter service to send a document to printer.
uuid: c6a3fe8d-ec19-4350-b4a6-4c3d1971b501
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: c2d564ba-fa5a-4130-b7fe-7e2c64d92170
exl-id: 5fb38afd-7517-494e-b084-1fdd4aef3ca4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '362'
ht-degree: 100%

---

# Utilisation de l’API sendToPrinter {#using-the-sendtoprinter-api}

## Présentation {#overview}

Dans AEM Forms, vous pouvez utiliser le service SendToPrinter pour envoyer un document vers l’imprimante. Le service SendToPrinter prend en charge les systèmes d’accès aux imprimantes suivants :

* **Imprimante accessible directement** `: A printer that is installed on the same computer is called a direct accessible printer, and the computer is named printer host. This type of printer can be a local printer that is connected to the computer directly.`

* **Imprimante accessible indirectement** `: The printer that is installed on a print server is accessed from other computers. Technologies such as the common UNIX® printing system (CUPS) and the Line Printer Daemon (LPD) protocol are available to connect to a network printer. To access an indirect accessible printer, specify the print server’s IP or host name. Using this mechanism, you can send a document to an LPD URI when the network has an LPD running. The mechanism lets you route the document to any printer that is connected to the network that has an LPD running.`

   Lorsque vous envoyez un document à une imprimante, indiquez l’un des protocoles d’impression suivants : 

   * **CUPS** `: A printing protocol named common UNIX printing system. This protocol is used for UNIX operating systems and enables a computer to function as a print server. The print server accepts print requests from client applications, processes them, and sends them to configured printers. On the IBM AIX® operating system, usage of CUPS is not recommended.`
   * ``**DirectIP** `: A standard protocol for remote printing and managing print jobs. This protocol can be used locally or remotely. Print queues are not required.`
   * ``**LPD** `: A printing protocol named Line Printer Daemon protocol or Line Printer Remote (LPR) protocol. This protocol provides network print server functionality for UNIX-based systems.`
   * **SharedPrinter** `: A printing protocol that enables a computer to use a printer that is configured for that computer.`
   * **CIFS** : le service Output prend en charge le protocole d’impression CIFS (Common Internet File System).

## Utilisation du service SendToPrinter {#using-sendtoprinter-service}

Le tableau ci-dessous répertorie :

* les informations sur le printerName ou le printServer à utiliser pour les différents protocoles ;
* la valeur ou l’exception qu’une imprimante renvoie pour différentes combinaisons de serveur d’imprimante URI et de Nom de l’imprimante.

| Protocole (système d’accès) | URI de serveur d’impression (PrinterSpec.printServer) | Nom de l’imprimante (PrinterSpec.printerName) | Résultat |
|--- |--- |--- |--- |
| SharedPrinter | N’importe lequel | Vide | Exception : l’argument requis sPrinterName ne peut pas être vide. |
| SharedPrinter | N’importe lequel | Invalid (non valide) : | Une exception indique que l’imprimante est introuvable. |
| SharedPrinter | N’importe lequel | Valide | Tâche d’impression réussie. |
| LPD | Vide | N’importe lequel | une exception indiquant que l’argument requis sPrintServerUri ne peut pas être vide. |
| LPD | Invalid (non valide) : | Vide | une exception indiquant que l’argument requis sPrinterName ne peut pas être vide. |
| LPD | Invalid (non valide) : | Pas vide | une exception indiquant que sPrintServerUri est introuvable. |
| LPD | Valide | Invalid (non valide) : | une exception indiquant que l’imprimante est introuvable. |
| LPD | Valide | Valide | Tâche d’impression réussie. |
| CUPS | Vide | N’importe lequel | une exception indiquant que l’argument requis sPrintServerUri ne peut pas être vide. |
| CUPS | Invalid (non valide) : | N’importe lequel | une exception indiquant que l’imprimante est introuvable. |
| CUPS | Valide | N’importe lequel | Tâche d’impression réussie. |
| DirectIP | Vide | N’importe lequel | une exception indiquant que l’argument requis sPrintServerUri ne peut pas être vide. |
| DirectIP | Invalid (non valide) : | N’importe lequel | une exception indiquant que l’imprimante est introuvable. |
| DirectIP | Valide | N’importe lequel | Tâche d’impression réussie. |
| CIFS | Valide | Vide | Tâche d’impression réussie. |
| CIFS | Invalid (non valide) : | N’importe lequel | une erreur inconnue lors de l’impression par CIFS. |
| CIFS | Vide | N’importe lequel | une exception indiquant que l’argument requis sPrintServerUri ne peut pas être vide. |

## Prise en charge de l’authentification {#authentication-support}

L’authentification est prise en charge uniquement pour l’impression CIFS. Pour authentifier, indiquez vos nom d’utilisateur, mot de passe et domaine dans PrinterSpec. Vous pouvez chiffrer un mot de passe à l’aide du service Granite CryptoSupport AEM en procédant de la manière suivante :

1. Accédez à https://&lt;server>:&lt;port>/system/console.

1. Accédez à **[!UICONTROL Général]** > **[!UICONTROL Crypto Support]**.

1. Entrez du texte brut puis cliquez sur **[!UICONTROL Protection]**.
