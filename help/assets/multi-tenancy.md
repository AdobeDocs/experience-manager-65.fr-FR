---
title: Fonction multiclient pour les collections, les fragments de code et les modèles de fragments de code
description: Découvrez comment la fonction multiclient permet de séparer du contenu dans le référentiel CRX en fonction de l’organisation du client afin d’empêcher tout accès non autorisé.
contentOwner: AG
role: Developer, Admin, Leader
feature: Collections
exl-id: f95560c9-f1b9-4e86-94a7-70347d268d8f
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: ac365bec-0634-4744-9473-c42f47320593
    internal-label: Asset management and governance
subfeature_v2:
  - id: c73531c3-4c05-471e-beff-cefb35857910
    internal-label: Collections
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 87%
---
# Fonction multiclient pour les collections, les fragments de code et les modèles de fragments de code {#multi-tenancy-for-collections-snippets-and-snippet-templates}

La fonction multiclient permet de séparer du contenu dans CRX en fonction du préfixe et de l’identifiant d’organisation, de sorte à protéger le contenu contre tout accès non autorisé par les utilisateurs d’autres organisations.

[!DNL Adobe Experience Manager Assets] stocke les données de chaque organisation à un chemin d’accès différent. Le chemin d’accès propre à chaque organisation est identifié par le préfixe et l’ID d’organisation
est inclus à l’emplacement traditionnel où différents types de ressources sont stockés dans CRX.

Par exemple, si vous créez un dossier nommé `Demo`, [!DNL Experience Manager] Assets stocke généralement le dossier à l’adresse `../content/dam/Demo`. Lorsque le multiclient est activé, vous pouvez désormais stocker les données à l’adresse `../content/dam/<organization prefix>/<organization id>Demo`.

Par exemple, pour les utilisateurs d’[!DNL Adobe Marketing Cloud] d’[!DNL Assets] (à la demande) qui sont affectés à l’organisation `aodpremium`, vous pouvez utiliser la fonctionnalité multiclient afin de configurer le chemin d’accès `../content/dam/<mac>/<aodpremium>Demo` pour séparer leur contenu. Dans cet exemple, `mac` est le préfixe de l’organisation et `aodpremium` est l’ID d’organisation.

En fonction de l’organisation et de l’identifiant de l’utilisateur, ce chemin d’accès s’affiche dans l’interface d’[!DNL Assets] et dans différents assistants, notamment les assistants Déplacement et Création de fragment de code, pour appliquer la séparation.

La fonctionnalité multiclient vous permet de séparer les types de ressources et de composants suivants :

* Collections
* Collections publiques
* Catalogues (notamment l’assistant Ajouter/Sélectionner une page)
* Modèles
* Modèles d’extrait de code
* Lightbox
