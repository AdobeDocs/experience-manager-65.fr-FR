---
title: Utiliser l’API sendToPrinter
description: Utiliser le service sendToPrinter pour envoyer un document à l’imprimante.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
feature: Document Services,APIs & Integrations
exl-id: 585d4053-1056-4d2b-a9df-9516775afe50
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 516393bc-fa69-5e74-a04e-f7ec9ffe2c5e
    internal-label: APIs & Integrations
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: f19cff18-c8cc-4a4b-adad-85dd2fa3dbe2
    internal-label: Document Services
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 100%
---
# Utiliser l’API sendToPrinter {#using-the-sendtoprinter-api}

## Présentation {#overview}

Dans AEM Forms, vous pouvez utiliser le service SendToPrinter pour envoyer un document à l’imprimante. Le service SendToPrinter prend en charge les mécanismes d’accès à l’impression suivants :

* **Imprimante accessible directement** `: A printer that is installed on the same computer is called a direct accessible printer, and the computer is named printer host. This type of printer can be a local printer that is connected to the computer directly.`

* **Imprimante accessible indirectement** `: The printer that is installed on a print server is accessed from other computers. Technologies such as the common UNIX® printing system (CUPS) and the Line Printer Daemon (LPD) protocol are available to connect to a network printer. To access an indirect accessible printer, specify the print server’s IP or host name. Using this mechanism, you can send a document to an LPD URI when the network has an LPD running. The mechanism lets you route the document to any printer that is connected to the network that has an LPD running.`

  Lorsque vous envoyez un document à une imprimante, indiquez l’un des protocoles d’impression suivants :

  * **CUPS** `: A printing protocol named common UNIX printing system. This protocol is used for UNIX operating systems and enables a computer to function as a print server. The print server accepts print requests from client applications, processes them, and sends them to configured printers. On the IBM AIX® operating system, usage of CUPS is not recommended.`
  * ``**DirectIP** `: A standard protocol for remote printing and managing print jobs. This protocol can be used locally or remotely. Print queues are not required.`
  * ``**LPD** `: A printing protocol named Line Printer Daemon protocol or Line Printer Remote (LPR) protocol. This protocol provides network print server functionality for UNIX-based systems.`
  * **SharedPrinter** `: A printing protocol that enables a computer to use a printer that is configured for that computer.`
  * **CIFS** : le service Output prend en charge le protocole d’impression CIFS (Common Internet File System).

## Utilisation du service SendToPrinter {#using-sendtoprinter-service}

Le tableau ci-dessous répertorie les éléments suivants :

* Informations sur le nom de l’imprimante ou le serveur d’impression à utiliser pour différents protocoles.
* Valeur ou exception renvoyée par une imprimante pour diverses combinaisons d’URI du serveur d’imprimante et de nom de l’imprimante

| Protocole (mécanisme d’accès) | URI du serveur d’impression (PrinterSpec.printServer) | Nom de l’imprimante (PrinterSpec.printerName) | Résultat |
|--- |--- |--- |--- |
| SharedPrinter | N’importe lequel | Vide | Exception : l’argument requis sPrinterName ne peut pas être vide. |
| SharedPrinter | N’importe lequel | Non valide | Une exception indique que l’imprimante est introuvable. |
| SharedPrinter | N’importe lequel | Valide | Travail d’impression réussi. |
| LPD | Vide | N’importe lequel | une exception indiquant que l’argument requis sPrintServerUri ne peut pas être vide. |
| LPD | Non valide | Vide | une exception indiquant que l’argument requis sPrinterName ne peut pas être vide. |
| LPD | Non valide | Pas vide | une exception indiquant que sPrintServerUri est introuvable. |
| LPD | Valide | Non valide | une exception indiquant que l’imprimante est introuvable. |
| LPD | Valide | Valide | Travail d’impression réussi. |
| CUPS | Vide | N’importe lequel | une exception indiquant que l’argument requis sPrintServerUri ne peut pas être vide. |
| CUPS | Non valide | N’importe lequel | une exception indiquant que l’imprimante est introuvable. |
| CUPS | Valide | N’importe lequel | Travail d’impression réussi. |
| DirectIP | Vide | N’importe lequel | une exception indiquant que l’argument requis sPrintServerUri ne peut pas être vide. |
| DirectIP | Non valide | N’importe lequel | une exception indiquant que l’imprimante est introuvable. |
| DirectIP | Valide | N’importe lequel | Travail d’impression réussi. |
| CIFS | Valide | Vide | Travail d’impression réussi. |
| CIFS | Non valide | N’importe lequel | une erreur inconnue lors de l’impression à l’aide de CIFS. |
| CIFS | Vide | N’importe lequel | une exception indiquant que l’argument requis sPrintServerUri ne peut pas être vide. |

## Prise en charge de l’authentification {#authentication-support}

L’authentification est prise en charge uniquement pour l’impression CIFS. Pour authentifier, indiquez vos nom d’utilisateur, mot de passe et domaine dans PrinterSpec. Vous pouvez chiffrer un mot de passe à l’aide du service Granite CryptoSupport AEM en procédant de la manière suivante :

1. Accédez à https://&lt;server>:&lt;port>/system/console.

1. Accédez à **[!UICONTROL Général]** > **[!UICONTROL Crypto Support]**.

1. Entrez du texte brut puis cliquez sur **[!UICONTROL Protection]**.
