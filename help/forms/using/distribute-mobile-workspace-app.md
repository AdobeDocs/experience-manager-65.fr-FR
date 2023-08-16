---
title: Distribuer l’application AEM Forms
seo-title: Distribute AEM Forms app
description: Utilisez la gestion des périphériques mobiles (MDM) pour le déploiement à grande échelle des applications sur les périphériques mobiles.
seo-description: Use Mobile Device Management (MDM) for the large-scale deployment of apps on mobile devices.
uuid: 8a2ce42b-5e9b-42c1-a945-c069f6152f6e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 5756cb52-dd47-4277-981c-fd0af9a20638
exl-id: 375cfa95-ac6f-44c4-a736-f5dd55d24195
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 30%

---

# Distribuer l’application AEM Forms {#distribute-aem-forms-app}

La gestion des périphériques mobiles (MDM) permet le déploiement à grande échelle d’applications sur des périphériques mobiles.

>[!NOTE]
>
>Cette distribution s’applique uniquement aux appareils iOS et Android.

## Fonctionnalités principales généralement fournies par les solutions MDM : {#main-features-generally-provided-by-mdm-solutions}

* Enregistrement des appareils dans votre environnement d’entreprise
* Configuration et mise à jour des paramètres des appareils
* Application des normes de sécurité.
* Sécurisation de l’accès mobile aux ressources de l’entreprise

Une solution MDM accompagnée de la gestion des applications mobiles vous permet de gérer les applications internes, publiques et achetées sur les périphériques mobiles de votre entreprise.

L’administrateur MDM peut charger des fichiers ipa et apk sur le serveur MDM et contrôler les utilisateurs qui peuvent accéder aux fichiers ipa ou apk. L’administrateur peut également contrôler le paramètre de profil correspondant à chaque application.

## Paramètres de profil affectant l’application AEM Forms {#profile-settings-affecting-the-aem-forms-app-br}

Les paramètres de profil suivants sur votre appareil affecteront le fonctionnement de lʼapplication AEM Forms sur celui-ci :

* **Utilisation autorisée de l’appareil photo** dans le **Fonctionnalité du périphérique** section

Si vous désactivez **Utilisation autorisée de l’appareil photo**, la fonction de caméra de la fonction [Annotation photo](/help/forms/using/add-attachments.md) ne fonctionnera pas. Vous devez activer cette option pour utiliser l’appareil photo dans l’application.

* **Requiert un code de passe sur l’appareil** dans la section Stratégies de code de passe

Pour activer le **chiffrement des données d’application**, nous vous conseillons d’activer le **mot de passe** sur votre appareil. Si le code de passe n’est pas défini sur l’appareil, les données de l’application stockées sur l’appareil ne sont pas chiffrées.
