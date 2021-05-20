---
title: Multi-location pour les collections, les fragments de code et les modèles de fragments de code
description: Découvrez comment la fonctionnalité multi-tenant vous permet de séparer le contenu dans le référentiel CRX en fonction de l’organisation du client afin d’empêcher tout accès non autorisé.
contentOwner: AG
role: Architect, Administrator, Leader
feature: Collections
exl-id: f95560c9-f1b9-4e86-94a7-70347d268d8f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 3%

---

# Multi-location pour les collections, les fragments de code et les modèles de fragments de code {#multi-tenancy-for-collections-snippets-and-snippet-templates}

La fonctionnalité multi-tenant vous permet de séparer le contenu dans CRX en fonction du préfixe de l’organisation et de l’ID d’organisation afin de protéger le contenu contre tout accès non autorisé par les utilisateurs d’autres organisations.

[!DNL Adobe Experience Manager Assets] stocke les données de chaque organisation dans un chemin d’accès différent. Chaque chemin spécifique à l’organisation est identifié par le préfixe de l’organisation et l’ID d’organisation.
qui est inclus dans l’emplacement traditionnel où différents types de ressources sont stockés dans CRX.

Par exemple, si vous créez un dossier nommé `Demo`, les ressources [!DNL Experience Manager] stockent traditionnellement le dossier à `../content/dam/Demo`. Lorsque la multi-location est activée, vous pouvez désormais stocker les données à l’adresse `../content/dam/<organization prefix>/<organization id>Demo`

Par exemple, si, pour [!DNL Adobe Marketing Cloud] utilisateurs de [!DNL Assets] (à la demande) affectés à l’organisation `aodpremium`, vous pouvez utiliser la fonction multi-location pour configurer le chemin `../content/dam/<mac>/<aodpremium>Demo` afin de séparer leur contenu. Dans cet exemple, `mac` est le préfixe de l’organisation et `aodpremium` est l’ID d’organisation.

En fonction de l’organisation et de l’identifiant de l’utilisateur, ce chemin d’accès qualifié est affiché dans l’interface [!DNL Assets] et dans divers assistants, y compris les assistants Déplacer et Création de fragments de code pour appliquer la ségrégation.

La fonctionnalité multiclient permet de séparer les types de ressources et de composants suivants :

* Collections
* Collections publiques
* Catalogues (y compris l’assistant Ajouter/Sélectionner une page)
* Modèles
* Modèles de fragments de code
* Lightbox
