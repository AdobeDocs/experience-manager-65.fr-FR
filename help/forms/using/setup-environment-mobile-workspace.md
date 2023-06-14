---
title: Configurer l’environnement de l’application AEM Forms
description: Matériel, logiciels et licences pour créer et déployer l’application AEM Forms.
uuid: 4123a6b7-5766-476c-9afb-f57029b148ad
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: e6b01ade-7ea3-42a7-872d-cc35a3d2782a
docset: aem65
exl-id: 1d1f9db2-83cf-4612-ac8c-d2638c3bbaea
source-git-commit: 78c584db8c35ea809048580fe5b440a0b73c8eea
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 29%

---

# Configurer l’environnement de l’application AEM Forms{#set-up-environment-for-aem-forms-app}

Vous avez besoin du matériel, des logiciels et licences ci-dessous pour générer et déployer l’application AEM Forms :

## Pour les périphériques Windows {#for-windows-devices}

* Microsoft® Windows 10
* Microsoft® Visual Studio 2015
* Microsoft® Visual Studio Tools pour Apache Cordova

## Pour les appareils iOS {#for-ios-devices}

* Apple Mac Intel exécutant macOS X 10.9.5 ou version ultérieure
* SDK iOS 8.4 ou version supérieure
* Version Xcode : Xcode 6.4 pour OS X ou version ultérieure
* Adhésion au programme iOS Developer Enterprise
* Certificat d’entreprise pour la distribution d’applications iOS en interne
* Apple iPad avec iOS 8.4 ou version ultérieure

## Pour les appareils Android™ {#for-android-devices}

* Android™ Development Toolkit (lot ADT) peut être téléchargé à partir de [https://developer.android.com/studio](https://developer.android.com/studio)
* Si l’environnement est configuré sur un système Mac, ADT doit être installé dans le dossier Applications .
* Si ADT est installé à un autre emplacement sur Mac ou si l’environnement est configuré sur un système Windows, le chemin du SDK ADT doit être mis à jour dans `local.properties` fichier . Ce fichier est disponible dans la `src\android` dossier dans l’archive source extraite `mobileworkspace-src.zip`. Dans ce fichier, pointez la variable `sdk.dir` vers l’emplacement d’ADT SDK sur votre bureau.

>[!NOTE]
>
>Le fichier adobe-lc-mobileworkspace-src.zip contient le PhoneGAP SDK 5.0. Assurez-vous que le PhoneGap SDK n’est pas préinstallé.
