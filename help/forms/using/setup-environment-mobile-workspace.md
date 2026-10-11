---
title: Configurer l’environnement de l’application AEM Forms
description: Matériel, logiciels et licences pour créer et déployer l’application AEM Forms.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: 1d1f9db2-83cf-4612-ac8c-d2638c3bbaea
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
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
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 86%
---
# Configurer l’environnement de l’application AEM Forms{#set-up-environment-for-aem-forms-app}

>[!NOTE]
>
>L’application AEM Forms est actuellement obsolète. Pour toute question ou aide, contactez [](mailto:aemformsapp-android@adobe.com).

Vous avez besoin du matériel, des logiciels et licences ci-dessous pour générer et déployer l’application AEM Forms :

## Pour les périphériques Windows {#for-windows-devices}

* Microsoft® Windows 10
* Microsoft® Visual Studio 2015
* Outils Microsoft® Visual Studio pour Apache Cordova

## Pour les périphériques iOS {#for-ios-devices}

* Ordinateur Apple Mac à processeur Intel avec macOS X 10.9.5 ou version supérieure
* SDK iOS 8.4 ou version supérieure
* Version Xcode : Xcode 6.4 pour OS X ou version supérieure
* Abonnement au programme pour développeurs et développeuses iOS en entreprise
* Certificat d’entreprise pour la distribution d’applications iOS en interne
* Apple iPad avec iOS 8.4 ou version ultérieure

## Pour périphériques Android™ {#for-android-devices}

* Android™ Development Toolkit (lot ADT) peut être téléchargé depuis [https://developer.android.com/studio](https://developer.android.com/studio).
* Si l’environnement est configuré sur un système Mac, l’ADT doit être installé dans le dossier Applications.
* Si ADT est installé à un autre emplacement sur Mac ou si l’environnement est configuré sur un système Windows, le chemin du SDK ADT doit être mis à jour dans le fichier `local.properties`. Ce fichier est disponible dans le dossier `src\android` de l’archive source extraite `mobileworkspace-src.zip`. Dans ce fichier, pointez la variable `sdk.dir` vers l’emplacement d’ADT SDK sur votre bureau.

>[!NOTE]
>
>Le fichier adobe-lc-mobileworkspace-src.zip contient PhoneGap SDK 5.0. Assurez-vous que PhoneGap SDK n’est pas préinstallé.
