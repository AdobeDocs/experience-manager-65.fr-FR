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
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '179'
ht-degree: 100%

---

# Gestion des listes de révocation des certificats{#managing-certificate-revocationlists}

>[!NOTE]
> 
> Vérifiez que l’utilisateur ou l’utilisatrice dispose de droits d’administration pour accéder à la console d’administration.

Trust Store Management vous permet d’importer, de modifier et de supprimer des listes de révocation des certificats (CRL). Les listes de révocation des certificats codées en Base64 et DER sont prises en charge.

## Importation d’une CRL {#import-a-crl}

1. Dans la console d’administration cliquez sur Paramètres > Trust Store Management > Listes de révocation des certificats, puis sur Importer.
1. Dans la zone Alias, saisissez un identifiant pour la liste CRL.
1. Cliquez sur Parcourir pour accéder à la CRL, puis sur OK.

## Exportation d’une CRL {#export-a-crl}

1. Dans la console d’administration cliquez sur Paramètres > Trust Store Management > Listes de révocation des certificats.
1. Cliquez sur le nom d’alias de la liste CRL, puis sur Exporter.
1. Suivez les instructions pour exporter la liste CRL. Les listes CRL sont exportées en encodage Base64.
1. Cliquez sur OK.

## Suppression d’une CRL {#delete-a-crl}

1. Dans la console d’administration cliquez sur Paramètres > Trust Store Management > Listes de révocation des certificats.
1. Cochez les cases des listes CRL à supprimer, cliquez sur Supprimer, puis sur OK.
