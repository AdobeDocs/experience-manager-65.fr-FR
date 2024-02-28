---
title: Problèmes de connexion avec les services Output, Forms et Document d’enregistrement
description: Résolvez les erreurs de connexion AEM Forms après SP19. Arrêtez, installez Microsoft Visual C++, redémarrez le serveur pour une solution transparente. Résolution des problèmes liés aux services Output, Forms et DoR.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
role: Admin
exl-id: bd58099c-08cd-4056-afb6-a5935454429a
source-git-commit: d195ac80ee59439bab5b1219a2c1f16e93e3d22b
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 19%

---

# Impossible d’utiliser le service Output, Forms ou Document d’enregistrement (DoR) {#unable-to-use-output-service-forms-service-or-document-of-record-service}

## Problème

Après l’installation du Service Pack 19 d’AEM Forms 6.5, toute tentative d’utilisation du service Output, du service Forms ou du service de document d’enregistrement (DoR) peut entraîner une erreur `Connection to failed service` erreur.

## Solution

Pour résoudre le problème :

1. Arrêtez votre instance Forms AEM 6.5.
1. Téléchargez et installez la [version 64 bits des packages Microsoft Visual C++ redistribuables pour Visual Studio 2015, 2017, 2019 et 2022](https://learn.microsoft.com/fr-fr/cpp/windows/latest-supported-vc-redist?view=msvc-170#visual-studio-2015-2017-2019-and-2022) sur l’ordinateur sur lequel AEM 6.5 Forms est installé.
1. Redémarrez le serveur AEM Forms.

   >[!NOTE]
   >
   > Il est recommandé d’utiliser la commande &quot;Ctrl + C&quot; pour redémarrer le SDK. Le redémarrage du SDK AEM à l’aide de méthodes alternatives, par exemple l’arrêt des processus Java, peut entraîner des incohérences dans l’environnement de développement AEM.


>[!NOTE]
>
>
> Assurez-vous d’installer le redistribuable, même si une version précédente est installée.
