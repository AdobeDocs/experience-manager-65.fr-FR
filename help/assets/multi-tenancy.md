---
title: Multi-tenanciation pour les collections, les extraits de code et les modèles de fragments de code
description: Découvrez comment la fonction de multipropriété vous permet de séparer le contenu dans le référentiel CRX en fonction de l’entreprise cliente afin d’empêcher tout accès non autorisé.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 3%

---


# Multi-tenanciation pour les collections, les extraits de code et les modèles de fragment de code {#multi-tenancy-for-collections-snippets-and-snippet-templates}

La fonction de multipropriété vous permet de séparer le contenu dans CRX en fonction du préfixe et de l’ID d’organisation afin de protéger le contenu contre un accès non autorisé des utilisateurs d’autres organisations.

[!DNL Adobe Experience Manager Assets] stocke les données de chaque organisation dans un chemin différent. Chaque chemin spécifique à l&#39;organisation est identifié par le préfixe et l&#39;ID d&#39;organisation de l&#39;organisation.
qui est inclus dans l’emplacement traditionnel où différents types de ressources sont stockés dans CRX.

Par exemple, si vous créez un dossier nommé `Demo`, les ressources [!DNL Experience Manager] stockent généralement le dossier à `../content/dam/Demo`. Avec l’option multi-tenancy activée, vous pouvez désormais stocker les données à `../content/dam/<organization prefix>/<organization id>Demo`

Par exemple, si, pour [!DNL Adobe Marketing Cloud] utilisateurs de [!DNL Assets] (sur demande) affectés à l&#39;organisation `aodpremium`, vous pouvez utiliser la fonction de multilocation pour configurer le chemin `../content/dam/<mac>/<aodpremium>Demo` afin de séparer leur contenu. Dans cet exemple, `mac` est le préfixe d&#39;organisation et `aodpremium` l&#39;ID d&#39;organisation.

En fonction de l&#39;organisation et de l&#39;ID de l&#39;utilisateur, ce chemin d&#39;accès qualifié s&#39;affiche dans l&#39;interface [!DNL Assets] et dans divers assistants, y compris les assistants de création de déplacement et d&#39;extrait de code pour appliquer la ségrégation.

La fonction de multilocation vous permet de séparer les types d’actifs et de composants suivants :

* Collections
* Collections publiques
* Catalogues (y compris l’assistant Ajouter/Sélectionner une page)
* Modèles
* Modèles de fragments de code
* Lightbox
