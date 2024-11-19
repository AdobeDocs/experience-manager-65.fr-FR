---
title: Article de dépannage pour résoudre le problème lorsque le service PaperCapture ne parvient pas à effectuer d’opérations OCR (reconnaissance optique de caractères) sur les PDF.
description: Voici les étapes pour résoudre le problème lorsque le service PaperCapture ne parvient pas à effectuer d’opérations OCR (reconnaissance optique de caractères) sur les PDF.
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 64e120ee-5f16-4cd3-9ae9-95b165169e47
source-git-commit: f9e98d7de24d516eab163d42f6c1c3155915856e
workflow-type: ht
source-wordcount: '196'
ht-degree: 100%

---


# Le service PaperCapture ne parvient pas à effectuer d’opérations OCR (reconnaissance optique de caractères) sur les PDF.

## Problème

Après la mise à niveau vers le pack de services AEM Forms 6.5.21.0, le service `PaperCapture` ne parvient pas à effectuer d’opérations OCR (reconnaissance optique de caractères) sur les PDF. Le service ne génère pas de sortie sous la forme d’un PDF ou d’un fichier journal.

## Application

Cette solution s’applique aux éléments suivants :
* AEM Forms sur tous les serveurs JEE (JBoss, Weblogic, Websphere)
* AEM Forms sur les serveurs OSGi

## Solution

1. Téléchargez le [correctif](https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&amp;reserved=0) à partir du portail de distribution de logiciels.
1. Extrayez et copiez le contenu du dossier téléchargé.
1. Accédez aux chemins d’accès ci-dessous pour les serveurs d’applications correspondants :
   * **jboss** :
     `..\Adobe\Adobe_Experience_Manager_Forms\jboss\standalone\svcnative\PaperCaptureSvc`
   * **weblogic** :
     `..\Adobe\Adobe_Experience_Manager_Forms\crx-repository\bedrock\svcnative\PaperCaptureSvc`
   * **websphere** :\
     `..\Adobe\Adobe_Experience_Manager_Forms\crx-repository\bedrock\svcnative\PaperCaptureSvc`
   * **Configuration OSGi** :\
     `..\quickstart\crx-quickstart\bedrock\svcnative\PaperCaptureSvc`
1. Arrêtez le serveur d’applications AEM Forms.
1. Remplacez le contenu existant du dossier `PaperCaptureSvc` par le contenu copié.
1. Redémarrez le serveur d’applications AEM.

   >[!NOTE]
   >
   > Il est recommandé d’utiliser la commande « Ctrl+C » pour redémarrer le SDK. Le redémarrage du SDK AEM à l’aide de méthodes alternatives, par exemple l’arrêt des processus Java, peut entraîner des incohérences dans l’environnement de développement AEM.
