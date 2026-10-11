---
title: Gestion des listes de révocation des certificats
description: Découvrez comment gérer les listes de révocation des certificats. Vous pouvez importer, modifier et supprimer des listes de révocation des certificats (CRL) à l’aide de Trust Store Management.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 01e966f6-a650-4565-80d1-e2297f25da5c
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms
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
source-wordcount: '180'
ht-degree: 100%
---
# Gestion des listes de révocation des certificats{#managing-certificate-revocationlists}

>[!NOTE]
> 
> Vérifiez que l’utilisateur ou l’utilisatrice dispose de droits d’administration pour accéder à la console d’administration.

Trust Store Management vous permet d’importer, de modifier et de supprimer des listes de révocation des certificats (CRL). Les listes de révocation des certificats codées en Base64 et DER sont prises en charge.

## Importation d’une CRL {#import-a-crl}

1. Dans la console d’administration, cliquez sur Paramètres > Trust Store Management > Listes de révocation des certificats, puis sur Importer.
1. Dans la zone Alias, saisissez un identifiant pour la CRL.
1. Cliquez sur Parcourir pour localiser la CRL, puis sur OK.

## Exportation d’une CRL {#export-a-crl}

1. Dans la console d’administration, cliquez sur Paramètres > Trust Store Management > Listes de révocation des certificats.
1. Cliquez sur le nom d’alias de la liste CRL, puis sur Exporter.
1. Suivez les instructions pour exporter la liste CRL. Les listes CRL sont exportées en encodage Base64.
1. Cliquez sur OK.

## Suppression d’une CRL {#delete-a-crl}

1. Dans la console d’administration cliquez sur Paramètres > Trust Store Management > Listes de révocation des certificats.
1. Cochez les cases des listes CRL à supprimer, cliquez sur Supprimer, puis sur OK.
