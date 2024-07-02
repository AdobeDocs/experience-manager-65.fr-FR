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
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: ht
source-wordcount: '197'
ht-degree: 100%

---

# Identifier les certificats valables et les certificats expirés dans les documents PDF {#recognizing-valid-and-expired-certificates-in-pdf-documents}

Lorsqu’un document PDF dont les droits d’utilisation sont appliqués par Reader Extensions est ouvert dans Adobe Reader, une barre d’état décrivant les droits d’utilisation spécifiquement activés dans ce document PDF s’affiche.

Lorsque le certificat numérique qui spécifie les droits d’utilisation d’un document PDF expire et que le document PDF est ouvert dans Adobe Reader, une boîte de dialogue indique à l’utilisateur ou l’utilisatrice que le document PDF possède des droits d’utilisation, mais que ces droits sont désactivés. Bien que le message indique que le document PDF a été modifié, cela n’est pas forcément le cas. Adobe Reader affiche ce message lorsqu’un certificat expire ou qu’un document est modifié. Dans Adobe Reader 7.0.x ou version ultérieure, vous ne pouvez pas déterminer laquelle de ces deux situations a provoqué le problème.

Lorsque vous fermez la boîte de dialogue, Adobe Reader ouvre le document PDF. Les droits d’utilisation qui ont été appliqués en utilisant les extensions Acrobat Reader DC ne sont pas disponibles, comme prévu. Si le document PDF est un formulaire interactif, les champs du formulaire sont verrouillés et l’utilisateur ou l’utilisatrice ne peut pas modifier les données du formulaire.
