---
title: Configuration de l’environnement de l’application AEM Forms
seo-title: Configuration de l’environnement de l’application AEM Forms
description: Matériel, logiciels et licences permettant de générer et déployer l’application AEM Forms.
seo-description: Matériel, logiciels et licences permettant de générer et déployer l’application AEM Forms.
uuid: 4123a6b7-5766-476c-9afb-f57029b148ad
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: e6b01ade-7ea3-42a7-872d-cc35a3d2782a
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Configuration de l’environnement de l’application AEM Forms{#set-up-environment-for-aem-forms-app}

Vous avez besoin du matériel, des logiciels et licences ci-dessous pour générer et déployer l’application AEM Forms :

## Pour les périphériques Windows {#for-windows-devices}

* Microsoft Windows 10
* Microsoft Visual Studio 2015
* Outils Microsoft Visual Studio pour Apache Cordova

## Pour les périphériques iOS {#for-ios-devices}

* Ordinateur Apple Mac à processeur Intel avec Mac OS X 10.9.5 ou version supérieure
* SDK iOS 8.4 ou version ultérieure
* Version Xcode : Xcode 6.4 pour OS X ou version supérieure
* Adhésion au programme pour développeurs iOS en entreprise
* Certificat d’entreprise pour la distribution d’applications iOS en interne
* Apple iPad avec iOS 8.4 ou version ultérieure

## Pour périphériques Android {#for-android-devices}

* Android Development Toolkit (ADT bundle) that can be downloaded from [https://developer.android.com/sdk/index.html](https://developer.android.com/sdk/index.html)
* Si l’environnement est configuré sur un système MAC, ADT doit être installé dans le dossier Applications.
* If the ADT is installed in any other location on MAC, or if the environment is set up on a Windows system, the ADT SDK path needs to be updated in `local.properties` file that is available in `src\android` folder in the extracted the source archive `mobileworkspace-src.zip`. Dans ce fichier, pointez la variable `sdk.dir` vers l’emplacement de ADT SDK sur votre bureau.

>[!NOTE]
>
>Le fichier adobe-lc-mobileworkspace-src.zip contient le SDK PhoneGap 5.0. Assurez-vous que le SDK PhoneGap n’est pas préinstallé.
