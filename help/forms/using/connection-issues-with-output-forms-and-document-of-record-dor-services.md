---
title: Problèmes de connexion avec les services Output, Forms et de document d’enregistrement
description: Résolvez les erreurs de connexion AEM Forms après le pack de services 19. Arrêtez le serveur, installez Microsoft Visual C++, puis redémarrez le serveur pour une solution transparente. Résolvez les problèmes liés aux services Output, Forms et de document d’enregistrement.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
role: Admin
exl-id: bd58099c-08cd-4056-afb6-a5935454429a
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: ht
source-wordcount: '168'
ht-degree: 100%

---

# Impossible d’utiliser les services de sortie, de formulaires ou de document d’enregistrement (DoR) {#unable-to-use-output-service-forms-service-or-document-of-record-service}

## Problème

Après l’installation du pack de services 19 d’AEM Forms 6.5, toute tentative d’utilisation du service Output, du service Forms ou du service de document d’enregistrement (DoR) peut entraîner une erreur `Connection to failed service`.

## Solution

Pour résoudre le problème, procédez comme suit :

1. Arrêtez votre instance AEM 6.5 Forms.
1. Téléchargez et installez la [version 64 bits des packages Microsoft Visual C++ redistribuables pour Visual Studio 2015, 2017, 2019 et 2022](https://learn.microsoft.com/fr-fr/cpp/windows/latest-supported-vc-redist?view=msvc-170#visual-studio-2015-2017-2019-and-2022) sur l’ordinateur sur lequel AEM 6.5 Forms est installé.
1. Redémarrez le serveur AEM Forms.

   >[!NOTE]
   >
   > Il est recommandé d’utiliser la commande « Ctrl + C » pour redémarrer le SDK. Le redémarrage du SDK AEM à l’aide de méthodes alternatives, par exemple l’arrêt des processus Java, peut entraîner des incohérences dans l’environnement de développement AEM.


>[!NOTE]
>
>
> Assurez-vous d’installer le redistribuable, même si une version précédente est installée.
