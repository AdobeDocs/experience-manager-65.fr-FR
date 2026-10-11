---
title: Prise en charge du chiffrement des propriétés de configuration
description: Découvrez la prise en charge du chiffrement des propriétés de configuration fournie dans AEM.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: security
exl-id: 3c3db1c8-5b22-45dd-aeaf-5cf830a9486b
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: b1210526-416b-4ef6-bcc0-1692e99f30e9
    internal-label: Administration and security
subfeature_v2:
  - id: c35bc059-fd80-4a01-91a6-e48da3c76758
    internal-label: Security practices
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 100%
---
# Prise en charge du chiffrement des propriétés de configuration{#encryption-support-for-configuration-properties}

## du commerce électronique {#overview}

Cette fonction permet à toutes les propriétés de configuration OSGi d’être stockées sous une forme chiffrée et protégée, préférable au texte en clair. Le formulaire dans l’IU de la console Web permet de créer du texte chiffré à partir de texte en clair à l’aide de la clé principale de chiffrement du système.

La prise en charge du plug-in de configuration OSGi a été ajoutée pour déchiffrer la propriété avant qu’elle ne soit utilisée par un service.

>[!NOTE]
>
>Les services qui s’attendent à une valeur chiffrée doivent utiliser la vérification IsProtected pour voir si la valeur est chiffrée avant de tenter de la déchiffrer, car elle a peut-être déjà été déchiffrée.

## Activation de la prise en charge du chiffrement {#enabling-encryption-support}

Ces étapes indiquent comment chiffrer le mot de passe SMTP pour le service de messagerie. Vous pouvez effectuer ces étapes pour une propriété OSGI que vous souhaitez chiffrer.

1. Rendez-vous dans la console Web AEM sur *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*
1. Dans le coin supérieur gauche, accédez à **Prise en charge du chiffrement principal**.

   ![chlimage_1-325](assets/chlimage_1-325.png)

1. La page **Prise en charge du chiffrement de la console Web d’Adobe Experience Manager** s’affiche.

   ![screen_shot_2018-08-01at113417am](assets/screen_shot_2018-08-01at113417am.png)

1. Dans le champ **Texte brut**, saisissez le texte des données sensibles à protéger.
1. Sélectionnez **Protéger**. Le texte protégé s’affiche sous forme de texte chiffré.

   ![screen_shot_2018-08-01at113844am](assets/screen_shot_2018-08-01at113844am.png)

1. Copiez le texte protégé de l’étape 5 et collez-le dans la valeur du formulaire OSGI. Dans cet exemple, le **mot de passe SMTP** chiffré est ajouté au *service de messagerie Day CQ*.

   ![screen_shot_2016-12-18at105809pm](assets/screen_shot_2016-12-18at105809pm.png)

1. Enregistrez les propriétés du Service de messagerie Day CQ. Le mot de passe SMTP sera désormais envoyé sous forme de valeur chiffrée.

## Prise en charge du déchiffrement {#decryption-support}

AEM fournit désormais un module de configuration pour déchiffrer les propriétés de configuration. Ce plug-in AEM déchiffre et récupère automatiquement les propriétés en texte clair.
