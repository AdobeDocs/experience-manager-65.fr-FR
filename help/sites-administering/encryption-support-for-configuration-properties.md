---
title: Prise en charge du chiffrement des propriétés de configuration
seo-title: Encryption Support for Configuration Properties
description: Prise en charge du chiffrement des propriétés de configuration
seo-description: null
uuid: 26dc5e46-9332-4d9b-8874-895b90391e8c
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: security
discoiquuid: 4e08c297-aa4b-44cf-84c8-1e11582d9ebb
exl-id: 3c3db1c8-5b22-45dd-aeaf-5cf830a9486b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '277'
ht-degree: 100%

---

# Prise en charge du chiffrement des propriétés de configuration{#encryption-support-for-configuration-properties}

##  du commerce électronique {#overview}

Cette fonction permet à toutes les propriétés de configuration OSGi d’être stockées sous une forme chiffrée et protégée, préférable au texte en clair. Le formulaire dans l’IU de la console Web permet de créer du texte chiffré à partir de texte en clair à l’aide de la clé principale de chiffrement du système.

La prise en charge du module de configuration OSGi a été ajoutée afin de déchiffrer la propriété avant qu’elle ne soit utilisée par un service.

>[!NOTE]
>
>Les services exigeant une valeur chiffrée doivent utiliser la vérification IsProtected pour vérifier si la valeur est chiffrée avant de tenter de la déchiffrer, car elle a peut-être déjà été déchiffrée.

## Activation de la prise en charge du chiffrement {#enabling-encryption-support}

Ces étapes indiquent comment chiffrer le mot de passe SMTP pour le service de messagerie. Vous pouvez effectuer ces étapes pour une propriété OSGI que vous souhaitez chiffrer.

1. Rendez-vous dans la console Web AEM sur *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*
1. Dans le coin supérieur gauche, accédez à **Prise en charge du chiffrement principal**.

   ![chlimage_1-325](assets/chlimage_1-325.png)

1. La page **Prise en charge du chiffrement de la console Web d’Adobe Experience Manager** s’affiche.

   ![screen_shot_2018-08-01at113417am](assets/screen_shot_2018-08-01at113417am.png)

1. Dans le champ **Texte brut**, saisissez le texte des données sensibles que vous souhaitez protéger.
1. Sélectionnez **Protéger**. Le texte protégé est affiché sous forme de texte chiffré.

   ![screen_shot_2018-08-01at113844am](assets/screen_shot_2018-08-01at113844am.png)

1. Copiez le texte protégé de l’étape 5 et collez-le dans la valeur du formulaire OSGI. Dans cet exemple, le **mot de passe SMTP** chiffré est ajouté au *Service de messagerie Day CQ*.

   ![screen_shot_2016-12-18at105809pm](assets/screen_shot_2016-12-18at105809pm.png)

1. Enregistrez les propriétés du Service de messagerie Day CQ. Le mot de passe SMTP est maintenant envoyé sous forme de valeur chiffrée.

## Prise en charge du déchiffrement {#decryption-support}

AEM fournit désormais un module de configuration pour déchiffrer les propriétés de configuration. Ce module AEM déchiffre et récupère automatiquement les propriétés de texte en clair.
