---
title: Traduction de contenu pour les sites multilingues
description: Découvrez comment traduire du contenu pour des sites multilingues.
contentOwner: Guillaume Carlino
feature: Language Copy
exl-id: 6ccfe612-8cfd-4ca2-ad01-8e4af36d44fa
solution: Experience Manager, Experience Manager Sites
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: d9d38edd-df1b-480c-8f5e-72b62576f390
    internal-label: Site and page features
subfeature_v2:
  - id: e15a4109-ae5d-497d-b301-31149e35aed4
    internal-label: Language Copy Wizard
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 100%
---
# Traduction de contenu pour les sites multilingues {#translating-content-for-multilingual-sites}

Automatisez la traduction du contenu des pages, des ressources et du contenu créé par les utilisateurs pour créer et tenir à jour des sites web multilingues. Pour automatiser les processus de traduction, vous intégrez des fournisseurs de services de traduction à AEM et vous créez des projets pour traduire le contenu dans plusieurs langues. AEM prend en charge les workflows de traduction humaine et automatique.

* Traduction humaine : le contenu est envoyé à votre fournisseur de traduction et traduit par des traducteurs professionnels. Une fois la traduction terminée, le contenu traduit est renvoyé et importé dans AEM. Lorsque votre fournisseur de traduction est intégré à AEM, le contenu est automatiquement transféré entre AEM et le fournisseur de traduction.
* Traduction automatique : le service de traduction automatique traduit immédiatement votre contenu.

La traduction du contenu implique les étapes suivantes :

1. [Connectez AEM à votre fournisseur de service de traduction](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider) et [créez des configurations de structure d’intégration de traduction](/help/sites-administering/tc-tic.md).
1. [Associer les pages de votre gabarit de langue](/help/sites-administering/tc-tic.md#configuring-pages-for-translation) au service de traduction et aux configurations de structure.
1. [Identifier le type de contenu](/help/sites-administering/tc-rules.md) à traduire.
1. [Préparez le contenu à traduire](/help/sites-administering/tc-prep.md) en créant le gabarit de langue et les pages racine des copies de langue.
1. [Créez des projets de traduction](/help/sites-administering/tc-manage.md) pour collecter le contenu à traduire et préparer le processus de traduction.
1. Utilisez les projets de translation pour [gérer le processus de traduction du contenu](/help/sites-administering/tc-manage.md).

Si votre fournisseur de services de traduction ne fournit pas de connecteur pour l’intégration avec AEM, AEM prend en charge l’extraction et la réinsertion manuelles du contenu de traduction au format XML.

>[!NOTE]
>
>L’utilisateur ou l’utilisatrice doit être membre du groupe projects-administrators pour utiliser les fonctionnalités de copie linguistique.

## Bonnes pratiques {#best-practices}

La page [Bonnes pratiques de traduction](/help/sites-administering/tc-bp.md) fournit des informations importantes concernant votre mise en œuvre.
