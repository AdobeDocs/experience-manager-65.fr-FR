---
title: Gestion des listes de révocation des certificats
description: Découvrez comment gérer les listes de révocation des certificats.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 01e966f6-a650-4565-80d1-e2297f25da5c
source-git-commit: e33816b3b8d190e185d2b23dad3a05aca272f01c
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 6%

---

# Gestion des listes de révocation des certificats{#managing-certificate-revocationlists}

Trust Store Management vous permet d’importer, de modifier et de supprimer des listes de révocation des certificats (CRL). Les listes de révocation des certificats codées Base64 et DER sont prises en charge.

## Importation d’une CRL {#import-a-crl}

1. Dans Administration Console, cliquez sur Paramètres > Trust Store Management > Listes de révocation des certificats, puis sur Importer.
1. Dans la zone Alias, saisissez un identifiant pour la liste CRL.
1. Cliquez sur Parcourir pour localiser la CRL, puis sur OK.

## Exportation d’une CRL {#export-a-crl}

1. Dans Administration Console, cliquez sur Paramètres > Trust Store Management > Listes de révocation des certificats.
1. Cliquez sur le nom d’alias de la liste CRL afin de pouvoir l’exporter, puis cliquez sur Exporter.
1. Suivez les instructions pour exporter la CRL. Les listes CRL sont exportées en encodage Base64.
1. Cliquez sur OK.

## Suppression d’une CRL {#delete-a-crl}

1. Dans Administration Console, cliquez sur Paramètres > Trust Store Management > Listes de révocation des certificats.
1. Cochez les cases correspondant aux listes CRL à supprimer, cliquez sur Supprimer, puis sur OK.
