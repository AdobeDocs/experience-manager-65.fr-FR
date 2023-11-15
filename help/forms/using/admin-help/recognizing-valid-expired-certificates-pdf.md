---
title: Identifier les certificats valables et les certificats expirés dans les documents PDF
description: Découvrez comment reconnaître les certificats valides et expirés dans des documents de PDF.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: dfe2823a-3a0d-4e45-8765-f618529e22dd
source-git-commit: 7f35fdee9dbca9dfd3992b56579d6d06633f8dec
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 8%

---

# Identifier les certificats valables et les certificats expirés dans les documents PDF {#recognizing-valid-and-expired-certificates-in-pdf-documents}

Lorsqu’un document de PDF auquel des droits d’utilisation sont appliqués par Reader Extensions s’ouvre dans Adobe Reader, une barre d’état s’affiche, décrivant les droits d’utilisation spécifiques activés dans le document de PDF.

Lorsque le certificat numérique qui spécifie les droits d’utilisation d’un document de PDF expire et que le document de PDF est ouvert dans Adobe Reader, une boîte de dialogue indique à l’utilisateur que le document de PDF possède des droits d’utilisation, mais que ces droits sont désactivés. Bien que le message indique que le document du PDF a été modifié ou modifié, ce n’est pas nécessairement le cas. Adobe Reader affiche ce message lorsqu’un certificat expire ou qu’un document est modifié. Dans Adobe Reader 7.0.x ou version ultérieure, vous ne pouvez pas déterminer quel cas est actuellement le problème.

Une fois la boîte de dialogue fermée, Adobe Reader ouvre le document du PDF. Les droits d’utilisation appliqués à l’aide des extensions Acrobat Reader DC ne sont pas disponibles, comme prévu. Si le document du PDF est un formulaire interactif, les champs du formulaire sont verrouillés et l’utilisateur ne peut pas modifier les données du formulaire.
