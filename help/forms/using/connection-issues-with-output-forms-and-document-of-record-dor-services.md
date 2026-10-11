---
title: Problèmes de connexion avec les services Output, Forms et de document de référence (DoR)
description: Résolvez les erreurs de connexion AEM Forms après le pack de services 19. Arrêtez le serveur, installez Microsoft Visual C++, puis redémarrez le serveur pour une solution transparente. Résolvez les problèmes liés aux services Output, Forms et de document de référence.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
role: Admin
exl-id: bd58099c-08cd-4056-afb6-a5935454429a
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
  - id: f19cff18-c8cc-4a4b-adad-85dd2fa3dbe2
    internal-label: Document Services
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 100%
---
# Impossible d’utiliser le service Output, le service Forms ou le service de document de référence (DoR) {#unable-to-use-output-service-forms-service-or-document-of-record-service}

## Problème

Après l’installation du pack de services 19 d’AEM Forms 6.5, toute tentative d’utilisation du service Output, du service Forms ou du service de document d’enregistrement (DoR) peut entraîner une erreur `Connection to failed service`.

## Solution

Pour résoudre le problème, procédez comme suit :

1. Arrêtez votre instance AEM 6.5 Forms.
1. Téléchargez et installez la [version 64 bits des packages Microsoft Visual C++ redistribuables pour Visual Studio 2015, 2017, 2019 et 2022](https://learn.microsoft.com/fr-fr/cpp/windows/latest-supported-vc-redist?view=msvc-170#visual-studio-2015-2017-2019-and-2022) sur l’ordinateur sur lequel AEM 6.5 Forms est installé.
1. Redémarrez le serveur AEM Forms.

   >[!NOTE]
   >
   > Il est recommandé d’utiliser la commande « Ctrl+C » pour redémarrer le SDK. Le redémarrage du SDK AEM à l’aide de méthodes alternatives, par exemple l’arrêt des processus Java, peut entraîner des incohérences dans l’environnement de développement AEM.


>[!NOTE]
>
>
> Assurez-vous d’installer le redistribuable, même si une version précédente est installée.
