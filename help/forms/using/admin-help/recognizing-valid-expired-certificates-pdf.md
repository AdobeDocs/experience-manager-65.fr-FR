---
title: Identification des certificats valables et des certificats expirés dans les documents PDF
seo-title: Identification des certificats valables et des certificats expirés dans les documents PDF
description: Découvrez comment identifier les certificats valides et les certificats arrivés à expiration dans les documents PDF.
seo-description: Découvrez comment identifier les certificats valides et les certificats arrivés à expiration dans les documents PDF.
uuid: ceeff57a-586f-4f7b-852f-2a637f003d7e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4559218a-65ba-4577-ad26-7721e28971bc
exl-id: dfe2823a-3a0d-4e45-8765-f618529e22dd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 100%

---

# Identification des certificats valables et des certificats expirés dans les documents PDF {#recognizing-valid-and-expired-certificates-in-pdf-documents}

Lorsqu’un document PDF dont les droits d’utilisation sont appliqués par Reader Extensions est ouvert dans Adobe Reader, une barre d’état décrivant les droits d’utilisation spécifiquement activés dans ce document PDF s’affiche.

Si le certificat numérique qui spécifie les droits d’utilisation d’un document PDF expire et que l’utilisateur ouvre le document dans Adobe Reader, une boîte de dialogue s’affiche pour signaler que ce document PDF a des droits d’utilisation et que ceux-ci sont désactivés. Bien que le message indique que le document PDF a été modifié, cela n’est pas forcément le cas. Adobe Reader affiche ce message lorsqu’un certificat expire ou qu’un document est modifié. Dans Adobe Reader 7.0.x ou version ultérieure, vous ne pouvez pas déterminer laquelle de ces deux situations a provoqué le problème.

Lorsque vous fermez la boîte de dialogue, Adobe Reader ouvre le document PDF. Les droits d’utilisation qui ont été appliqués en utilisant les extensions d’Acrobat Reader DC ne sont pas disponibles, comme prévu. Si le document PDF est un formulaire interactif, les champs du formulaire sont verrouillés et l’utilisateur ne peut pas modifier les données du formulaire.
