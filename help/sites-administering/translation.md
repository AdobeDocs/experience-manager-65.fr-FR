---
title: Traduction de contenu pour les sites multilingues
seo-title: Traduction de contenu pour les sites multilingues
description: Découvrez comment traduire du contenu pour les sites multilingues.
seo-description: Découvrez comment traduire du contenu pour les sites multilingues.
uuid: 69b3e3a9-6773-4759-8178-aaa612e4c170
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 1e0a68c5-1583-4103-9dbb-7a53faa03c06
docset: aem65
legacypath: /content/docs/en/aem/6-0/administer/integration/third-party-services/machine-translation
feature: Copie de la langue
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 87%

---


# Traduction de contenu pour les sites multilingues {#translating-content-for-multilingual-sites}

Automatisez la traduction du contenu des pages, des ressources et du contenu créé par les utilisateurs pour créer et tenir à jour des sites web multilingues. Pour automatiser les processus de traduction, vous intégrez des fournisseurs de services de traduction à AEM et vous créez des projets pour traduire le contenu dans plusieurs langues. AEM prend en charge les workflows de traduction humaine et automatique.

* Traduction humaine : le contenu est envoyé à votre fournisseur de traduction et traduit par des traducteurs professionnels. Une fois la traduction terminée, le contenu traduit est renvoyé et importé dans AEM. Lorsque votre fournisseur de traduction est intégré à AEM, le contenu est automatiquement transféré entre AEM et le fournisseur de traduction.
* Traduction automatique : le service de traduction automatique traduit immédiatement votre contenu.

La traduction du contenu implique les étapes suivantes :

1. [Connectez AEM à votre fournisseur de service de traduction](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider) et [créez des configurations de structure d’intégration de traduction](/help/sites-administering/tc-tic.md).
1. [Associer les pages de votre gabarit de langue](/help/sites-administering/tc-tic.md#configuring-pages-for-translation) au service de traduction et aux configurations de structure.
1. [Identifiez le type de ](/help/sites-administering/tc-rules.md) contenu à traduire.
1. [Préparez le contenu à traduire](/help/sites-administering/tc-prep.md) en créant le gabarit de langue et les pages racine des copies de langue.
1. [Créez des ](/help/sites-administering/tc-manage.md) projets de traduction pour rassembler le contenu à traduire et préparer le processus de traduction.
1. Utiliser les projets de translation pour [gérer le processus de traduction du contenu](/help/sites-administering/tc-manage.md).

Si votre fournisseur de services de traduction ne fournit pas de connecteur pour l’intégration à AEM, AEM prend en charge l’extraction et la réinsertion manuelles du contenu de translation au format XML.

>[!NOTE]
>
>Votre utilisateur doit être membre du groupe des administrateurs de projet pour utiliser les fonctionnalités de copie de langue.

## Bonnes pratiques {#best-practices}

La page [Bonnes pratiques de traduction](/help/sites-administering/tc-bp.md) contient des informations importantes concernant votre implémentation.
