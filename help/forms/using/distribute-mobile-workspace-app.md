---
title: Distribuer l’application AEM Forms
seo-title: Distribuer l’application AEM Forms
description: Les solutions MDM (Mobile Device Management) permettent le déploiement à grande échelle des applications sur des périphériques mobiles.
seo-description: Les solutions MDM (Mobile Device Management) permettent le déploiement à grande échelle des applications sur des périphériques mobiles.
uuid: 8a2ce42b-5e9b-42c1-a945-c069f6152f6e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 5756cb52-dd47-4277-981c-fd0af9a20638
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 92%

---


# Distribuer l’application AEM Forms {#distribute-aem-forms-app}

Les solutions MDM (Mobile Device Management) permettent le déploiement à grande échelle des applications sur des périphériques mobiles.

>[!NOTE]
>
>Cette distribution s’applique aux périphériques iOS et Android uniquement.

## Fonctions clés que proposent généralement les solutions MDM :  {#main-features-generally-provided-by-mdm-solutions}

* Enregistrement des périphériques dans votre environnement d’entreprise
* Configuration et mise à jour des paramètres des périphériques
* Application des normes de sécurité.
* Sécurisation de l’accès mobile aux ressources de l’entreprise

Une solution MDM doublée de fonctions MAM (Mobile Application Management) vous permet de gérer les applications internes, publiques et achetées via les périphériques mobiles de votre entreprise.

L’administrateur MDM peut transférer des fichiers .ipa et .apk sur le serveur MDM et contrôler les utilisateurs ayant accès à ces fichiers. Il peut également contrôler le paramètre de profil correspondant à chaque application.

## Paramètres de profil affectant l’application AEM Forms {#profile-settings-affecting-the-aem-forms-app-br}

Les paramètres de Profil suivants sur votre périphérique affecteront le fonctionnement de l’application AEM Forms sur votre périphérique :

* **Autiliser l’utilisation de l’appareil photo** dans la section **Fonctionnalité du périphérique**

Si vous désactivez **Autiliser l’utilisation de l’appareil photo**, la fonction appareil photo de [l’Annotation photographique](/help/forms/using/add-attachments.md) ne fonctionnera pas. Vous devez activer cette option pour utiliser l’appareil photo dans l’application.

* **Mot de passe requis sur le périphérique** dans la section Stratégies de mot de passe

Pour activer le **chiffrement des données d’application**, nous vous conseillons d’activer le **mot de passe** sur votre périphérique. Si aucun mot de passe n’est défini sur le périphérique, les données d’application stockées sur le périphérique ne sont pas chiffrées.
