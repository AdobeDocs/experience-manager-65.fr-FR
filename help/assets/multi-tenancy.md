---
title: Multilocation pour les collections, les extraits de code et les modèles de fragment de code
description: Découvrez comment la fonction de multi-bail permet de séparer le contenu dans le référentiel CRX en fonction de l’entreprise cliente afin d’empêcher un accès non autorisé.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Multi-tenancy for Collections, snippets, and snippet templates {#multi-tenancy-for-collections-snippets-and-snippet-templates}

La fonctionnalité de multi-bail permet de séparer le contenu dans CRX en fonction du préfixe et de l’ID d’organisation afin de protéger le contenu contre un accès non autorisé par les utilisateurs d’autres organisations.

Adobe Experience Manager (AEM) Assets stocke les données de chaque organisation à un chemin d’accès différent. Chaque chemin spécifique à l’organisation est identifié par le préfixe et l’ID d’organisation inclus dans l’emplacement traditionnel où différents types de ressources sont stockés dans CRX.

Par exemple, si vous créez un dossier nommé `Demo`, les ressources AEM stockent généralement le dossier à l’emplacement `../content/dam/Demo`. Avec l’option multi-tenancy activée, vous pouvez désormais stocker les données dans `../content/dam/<organization prefix>/<organization id>Demo`

For example, if for [!DNL Adobe Marketing Cloud] users of AEM Assets (on demand) that are assigned to the `aodpremium` organization, you can use the multi-tenancy feature to configure `../content/dam/<mac>/<aodpremium>Demo` path to segregate their content. Dans cet exemple, `mac` est le préfixe de l’organisation et `aodpremium` l’ID de l’organisation.

En fonction de l’organisation et de l’ID de l’utilisateur, ce chemin d’accès qualifié s’affiche dans l’interface des ressources AEM et dans divers assistants, y compris les assistants de création de déplacement et d’extrait de code pour appliquer la ségrégation.

La fonction Multi-bail vous permet de séparer les types de ressources et de composants suivants :

* Collections
* Collections publiques
* Catalogues (y compris l’assistant Ajouter/Sélectionner une page)
* Modèles
* Modèles de fragments de code
* Lightbox
