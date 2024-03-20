---
title: Distribuer l’application AEM Forms
description: Les solutions MDM (Mobile Device Management) permettent le déploiement à grande échelle des applications sur des appareils mobiles.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: 375cfa95-ac6f-44c4-a736-f5dd55d24195
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 100%

---

# Distribuer l’application AEM Forms {#distribute-aem-forms-app}

Les solutions MDM (Mobile Device Management) permettent le déploiement à grande échelle des applications sur des appareils mobiles.

>[!NOTE]
>
>Cette distribution s’applique aux appareils iOS et Android™ uniquement.

## Principales fonctionnalités des solutions MDM : {#main-features-generally-provided-by-mdm-solutions}

* Enregistrement des appareils dans votre environnement d’entreprise
* Configuration et mise à jour des paramètres des appareils
* Application des normes de sécurité.
* Sécurisation de l’accès mobile aux ressources de l’entreprise

Une solution MDM doublée de fonctions MAM (Mobile Application Management) vous permet de gérer les applications internes, publiques et achetées via les appareils mobiles de votre entreprise.

L’administrateur ou administratrice MDM peut transférer des fichiers .ipa et .apk sur le serveur MDM et contrôler les utilisateurs et utilisatrices ayant accès à ces fichiers. L’administrateur ou administratrice peut également contrôler les paramètres de profil qui correspondent à chaque application.

## Paramètres de profil affectant l’application AEM Forms {#profile-settings-affecting-the-aem-forms-app-br}

Les paramètres de profil suivants sur votre appareil affecteront le fonctionnement de lʼapplication AEM Forms sur celui-ci :

* **Autoriser l’utilisation de l’appareil photo** dans la section **Fonctionnalité de l’appareil**

Si vous désactivez **Autoriser l’utilisation de l’appareil photo**, la fonction appareil photo de l’[Annotation photographique](/help/forms/using/add-attachments.md) ne fonctionnera pas. Activez cette option pour utiliser l’appareil photo dans l’application.

* **Mot de passe requis sur l’appareil** dans la section Politiques de mot de passe

Pour activer le **chiffrement des données d’application**, nous vous conseillons d’activer le **mot de passe** sur votre appareil. Si aucun mot de passe n’est défini sur l’appareil, les données d’application stockées sur l’appareil ne sont pas chiffrées.
