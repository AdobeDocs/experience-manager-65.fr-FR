---
title: Identifier les certificats valables et les certificats expirés dans les documents PDF
description: Découvrez comment identifier les certificats valides et les certificats arrivés à expiration dans les documents PDF.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: dfe2823a-3a0d-4e45-8765-f618529e22dd
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
source-wordcount: '198'
ht-degree: 100%
---
# Identifier les certificats valables et les certificats expirés dans les documents PDF {#recognizing-valid-and-expired-certificates-in-pdf-documents}

Lorsqu’un document PDF dont les droits d’utilisation sont appliqués par Reader Extensions est ouvert dans Adobe Reader, une barre d’état décrivant les droits d’utilisation spécifiquement activés dans ce document PDF s’affiche.

Lorsque le certificat numérique qui spécifie les droits d’utilisation d’un document PDF expire et que le document PDF est ouvert dans Adobe Reader, une boîte de dialogue indique à l’utilisateur ou l’utilisatrice que le document PDF possède des droits d’utilisation, mais que ces droits sont désactivés. Bien que le message indique que le document PDF a été modifié ou falsifié, cela n’est pas forcément le cas. Adobe Reader affiche ce message lorsqu’un certificat expire ou qu’un document est modifié. Dans Adobe Reader 7.0.x ou version ultérieure, vous ne pouvez pas déterminer laquelle de ces deux situations a provoqué le problème.

Lorsque vous fermez la boîte de dialogue, Adobe Reader ouvre le document PDF. Les droits d’utilisation qui ont été appliqués en utilisant les extensions Acrobat Reader DC ne sont pas disponibles, comme prévu. Si le document PDF est un formulaire interactif, les champs du formulaire sont verrouillés et l’utilisateur ou l’utilisatrice ne peut pas modifier les données du formulaire.
