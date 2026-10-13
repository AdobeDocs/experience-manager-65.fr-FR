---
title: Activer et désactiver le mode de sauvegarde sécurisé
description: Sur la page Paramètres de sauvegarde, vous pouvez utiliser AEM Forms en mode de sauvegarde sécurisé afin de sauvegarder de manière fiable votre base de données et votre répertoire de stockage global de documents (GDS). Découvrez comment activer et désactiver le mode de sauvegarde sécurisé.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: f0ab712f-ecd9-4be8-a7a5-fd1a7a8c9a0b
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
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
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 100%
---
# Activer et désactiver le mode de sauvegarde sécurisé {#enabling-and-disabling-safe-backup-mode}

>[!NOTE]
> 
> Vérifiez que l’utilisateur ou l’utilisatrice dispose de droits d’administration pour accéder à la console d’administration.

Sur la page Paramètres de sauvegarde, vous pouvez utiliser AEM Forms en mode de sauvegarde sécurisé afin de sauvegarder de manière fiable votre base de données et votre répertoire de stockage global de documents (GDS).

AEM Forms fonctionne normalement en mode de sauvegarde sécurisé, mais il ne supprime pas activement les fichiers du répertoire GDS.

>[!NOTE]
>
>La définition de cette option ne sauvegarde pas le système, mais le prépare à cette opération.

## Activer le mode de sauvegarde sécurisé {#enable-safe-backup-mode}

1. Dans la console d’administration cliquez sur Paramètres > Paramètres de Core System > Paramètres de sauvegarde.
1. Sur la page Paramètres de sauvegarde, sélectionnez Fonctionner en mode de sauvegarde sécurisé et cliquez sur OK.

>[!NOTE]
>
>Si le système fonctionne déjà en mode de sauvegarde sécurisé, aucune réservation n’est créée lorsque vous cliquez sur OK.

## Désactiver le mode de sauvegarde sécurisé {#disable-safe-backup-mode}

1. Dans la console d’administration cliquez sur Paramètres > Paramètres de Core System > Paramètres de sauvegarde.
1. Sur la page Paramètres de sauvegarde, désactivez Fonctionner en mode de sauvegarde sécurisé et cliquez sur OK.
