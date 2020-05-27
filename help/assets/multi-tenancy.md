---
title: Multi-tenanciation pour les collections, les extraits de code et les modèles de fragments de code
description: Découvrez comment la fonction de multipropriété vous permet de séparer le contenu dans le référentiel CRX en fonction de l’entreprise cliente afin d’empêcher tout accès non autorisé.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 3%

---


# Multi-tenancy for Collections, snippets, and snippet templates {#multi-tenancy-for-collections-snippets-and-snippet-templates}

La fonction de multipropriété vous permet de séparer le contenu dans CRX en fonction du préfixe et de l’ID d’organisation afin de protéger le contenu contre un accès non autorisé des utilisateurs d’autres organisations.

Adobe Experience Manager Assets stocke les données de chaque organisation dans un chemin d’accès différent. Chaque chemin d’accès spécifique à l’organisation est identifié par le préfixe et l’ID d’organisation inclus dans l’emplacement traditionnel où différents types de ressources sont stockés dans CRX.

Par exemple, si vous créez un dossier nommé `Demo`, les fichiers Experience Manager stockent généralement le dossier à `../content/dam/Demo`l’emplacement suivant. Avec l’option multi-tenancy activée, vous pouvez désormais stocker les données à l’adresse `../content/dam/<organization prefix>/<organization id>Demo`

For example, if for [!DNL Adobe Marketing Cloud] users of Assets (on demand) that are assigned to the `aodpremium` organization, you can use the multi-tenancy feature to configure `../content/dam/<mac>/<aodpremium>Demo` path to segregate their content. Dans cet exemple, `mac` est le préfixe d’organisation et `aodpremium` l’ID d’organisation.

En fonction de l’organisation et de l’ID de l’utilisateur, ce chemin d’accès qualifié s’affiche dans l’interface Ressources et dans divers assistants, y compris les assistants de création de déplacement et d’extrait de code pour appliquer la ségrégation.

La fonction de multilocation vous permet de séparer les types d’actifs et de composants suivants :

* Collections
* Collections publiques
* Catalogues (y compris l’assistant Ajouter/Sélectionner une page)
* Modèles
* Modèles de fragments de code
* Lightbox
