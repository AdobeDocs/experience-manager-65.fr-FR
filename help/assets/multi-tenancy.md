---
title: Fonction multiclient pour les collections, les fragments de code et les modèles de fragments de code
description: Découvrez comment la fonction multiclient permet de séparer du contenu dans le référentiel CRX en fonction de l’organisation du client afin d’empêcher tout accès non autorisé.
contentOwner: AG
role: Architect, Admin, Leader
feature: Collections
exl-id: f95560c9-f1b9-4e86-94a7-70347d268d8f
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: ht
source-wordcount: '220'
ht-degree: 100%

---

# Fonction multiclient pour les collections, les fragments de code et les modèles de fragments de code {#multi-tenancy-for-collections-snippets-and-snippet-templates}

La fonction multiclient permet de séparer du contenu dans CRX en fonction du préfixe et de l’identifiant d’organisation, de sorte à protéger le contenu contre tout accès non autorisé par les utilisateurs d’autres organisations.

[!DNL Adobe Experience Manager Assets] stocke les données de chaque organisation à un chemin d’accès différent. Le chemin d’accès propre à chaque organisation est identifié par le préfixe d’organisation et l’identifiant d’organisation qui sont inclus à l’emplacement où différents types de ressources sont habituellement stockées dans CRX.

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
