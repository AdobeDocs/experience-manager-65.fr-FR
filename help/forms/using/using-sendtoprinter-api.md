---
title: Utilisation de l’API sendToPrinter
seo-title: Utilisation de l’API sendToPrinter
description: Utilisation du service sendToPrinter pour envoyer un document vers l’imprimante.
seo-description: Utilisation du service sendToPrinter pour envoyer un document vers l’imprimante.
uuid: c6a3fe8d-ec19-4350-b4a6-4c3d1971b501
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: c2d564ba-fa5a-4130-b7fe-7e2c64d92170
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 70%

---


# Utilisation de l’API sendToPrinter {#using-the-sendtoprinter-api}

## Présentation {#overview}

Dans AEM Forms, vous pouvez utiliser le service SendToPrinter pour envoyer un document vers l’imprimante. Le service SendToPrinter prend en charge les systèmes d’accès aux imprimantes suivants :

* **Imprimante accessible directement** `: A printer that is installed on the same computer is called a direct accessible printer, and the computer is named printer host. This type of printer can be a local printer that is connected to the computer directly.`

* **Imprimante accessible indirectement** `: The printer that is installed on a print server is accessed from other computers. Technologies such as the common UNIX® printing system (CUPS) and the Line Printer Daemon (LPD) protocol are available to connect to a network printer. To access an indirect accessible printer, specify the print server’s IP or host name. Using this mechanism, you can send a document to an LPD URI when the network has an LPD running. The mechanism lets you route the document to any printer that is connected to the network that has an LPD running.`

     Lorsque vous envoyez un document à une imprimante, indiquez l’un des protocoles d’impression suivants : 

   * **CUPS** `: A printing protocol named common UNIX printing system. This protocol is used for UNIX operating systems and enables a computer to function as a print server. The print server accepts print requests from client applications, processes them, and sends them to configured printers. On the IBM AIX® operating system, usage of CUPS is not recommended.`
   * &quot;**DirectIP** `: A standard protocol for remote printing and managing print jobs. This protocol can be used locally or remotely. Print queues are not required.`
   * &quot;**LPD** `: A printing protocol named Line Printer Daemon protocol or Line Printer Remote (LPR) protocol. This protocol provides network print server functionality for UNIX-based systems.`
   * **SharedPrinter** `: A printing protocol that enables a computer to use a printer that is configured for that computer.`
   * **CIFS** : Le service Output prend en charge le protocole d’impression CIFS (Common Internet File System).

## Utilisation du service SendToPrinter {#using-sendtoprinter-service}

Le tableau ci-dessous répertorie :

* les informations sur le printerName ou le printServer à utiliser pour les différents protocoles ;
* la valeur ou l’exception qu’une imprimante renvoie pour différentes combinaisons de serveur d’imprimante URI et de Nom de l’imprimante.

| Protocole (système d’accès) | URI de serveur d’impression (PrinterSpec.printServer) | Nom de l’imprimante (PrinterSpec.printerName) | Résultat |
|--- |--- |--- |--- |
| SharedPrinter | Valeur nulle ou non nulle | Vide | Exception : L&#39;argument requis sPrinterName ne peut pas être vide. |
| SharedPrinter | Valeur nulle ou non nulle | Invalid (non valide) : | Une exception indique que l’imprimante est introuvable. |
| SharedPrinter | Valeur nulle ou non nulle | Valide | Tâche d’impression réussie. |
| LPD | Vide | Valeur nulle ou non nulle | une exception indiquant que l’argument requis sPrintServerUri ne peut pas être vide. |
| LPD | Invalid (non valide) : | Vide | une exception indiquant que l’argument requis sPrinterName ne peut pas être vide. |
| LPD | Invalid (non valide) : | Non vide | exception indiquant que sPrintServerUri est introuvable. |
| LPD | Valide | Invalid (non valide) : | une exception indiquant que l’imprimante est introuvable. |
| LPD | Valide | Valide | Tâche d’impression réussie. |
| CUPS | Vide | Valeur nulle ou non nulle | une exception indiquant que l’argument requis sPrintServerUri ne peut pas être vide. |
| CUPS | Invalid (non valide) : | Valeur nulle ou non nulle | une exception indiquant que l’imprimante est introuvable. |
| CUPS | Valide | Valeur nulle ou non nulle | Tâche d’impression réussie. |
| DirectIP | Vide | Valeur nulle ou non nulle | une exception indiquant que l’argument requis sPrintServerUri ne peut pas être vide. |
| DirectIP | Invalid (non valide) : | Valeur nulle ou non nulle | une exception indiquant que l’imprimante est introuvable. |
| DirectIP | Valide | Valeur nulle ou non nulle | Tâche d’impression réussie. |
| CIFS | Valide | Vide | Tâche d’impression réussie. |
| CIFS | Invalid (non valide) : | Valeur nulle ou non nulle | une erreur inconnue lors de l’impression par CIFS. |
| CIFS | Vide | Valeur nulle ou non nulle | une exception indiquant que l’argument requis sPrintServerUri ne peut pas être vide. |

## Prise en charge de l’authentification {#authentication-support}

L’authentification est prise en charge uniquement pour l’impression CIFS. Pour vous authentifier, indiquez le nom d’utilisateur/mot de passe/domaine dans PrinterSpec. Vous pouvez chiffrer un mot de passe à l’aide du service Granite CryptoSupport AEM en procédant de la manière suivante :

1. Accédez à https://&lt;serveur>:&lt;port>/system/console.

1. Accédez à **[!UICONTROL Général]** > **[!UICONTROL Crypto Support]**.

1. Entrez du texte brut puis cliquez sur **[!UICONTROL Protection]**.

