---
title: Résolution des problèmes liés à l’article lorsque le service PaperCapture ne parvient pas à effectuer des opérations de reconnaissance optique des caractères (OCR) sur les PDF.
description: Découvrez les étapes à suivre pour résoudre le problème de l’échec du service PaperCapture à effectuer des opérations OCR (reconnaissance optique des caractères) sur les PDF.
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 18005ba060954151df126789496c81f7238e32f6
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 1%

---


# Le service PaperCature ne parvient pas à effectuer la reconnaissance optique des caractères sur les PDF.

## Problème

Après la mise à niveau vers AEM Forms Service Pack 6.5.21.0, la variable `PaperCapture` ne parvient pas à effectuer d’opérations OCR (Optical Character Reconnaissance) sur les PDF. Le service ne génère pas de sortie sous la forme d’un PDF ou d’un fichier journal.

## Solution

1. Téléchargez la [correctif](https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Ca285aedf27094c9e8d9b08dc91e26aa7%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545648843177070%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=uWk0PsSSDjLRxqEMGMW%2BbD%2Fv4egR4vWL%2B0mfKpXdrKQ%3D&amp;reserved=0) à partir du portail de distribution de logiciels.
1. Extrayez et copiez le contenu du dossier téléchargé.
1. Accédez aux chemins d’accès ci-dessous pour les serveurs d’applications correspondants :
   * **jboss**:
     `..\Adobe\Adobe_Experience_Manager_Forms\jboss\standalone\svcnative\PaperCaptureSvc`
   * **weblogic**:
     `..\Adobe\Adobe_Experience_Manager_Forms\crx-repository\bedrock\svcnative\PaperCaptureSvc`
   * **websphere**:\
     `..\Adobe\Adobe_Experience_Manager_Forms\crx-repository\bedrock\svcnative\PaperCaptureSvc`
   * **Configuration OSGi**:\
     `..\quickstart\crx-quickstart\bedrock\svcnative\PaperCaptureSvc`
1. Remplacez le contenu existant de la fonction `PaperCaptureSvc` avec le contenu copié.
1. [Redémarrer l’instance AEM](/help/forms/using/restart-aem-sdk.md).


