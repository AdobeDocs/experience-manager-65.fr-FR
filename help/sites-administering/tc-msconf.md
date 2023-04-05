---
title: Connexion à Microsoft&reg; Traducteur
description: Découvrez comment se connecter AEM à Microsoft&reg ; Traducteur.
uuid: 5e3916ec-36a0-4d31-94ff-c340a462411a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: a7958411-b509-428e-bbe2-42efe8fd1add
feature: Language Copy
exl-id: ca575a30-fc3e-4f38-9aa7-dbecbc089f87
source-git-commit: 95638b6dd9527c567b38d8cd9da14633bd4142b5
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 18%

---

# Connexion à Microsoft® Translator{#connecting-to-microsoft-translator}

Créez une configuration pour le service cloud Microsoft® Translator afin d’utiliser votre compte de traduction Microsoft® pour traduire AEM contenu de page, le contenu de la communauté ou les ressources.

| Propriété | Description |
|---|---|
| Libellé de traduction | Nom d’affichage du service de traduction. |
| Attribution de traduction | (Facultatif) Pour le contenu créé par l’utilisateur, l’attribution qui apparaît à côté du texte traduit, par exemple `Translations by Microsoft`. |
| ID d’espace de travail | (Facultatif) L’identifiant de votre moteur Microsoft® Translator personnalisé à utiliser. |
| Clé d’abonnement | Votre clé d’abonnement Microsoft® pour le traducteur Microsoft®. |

Après avoir créé la configuration, vous devez [activer](/help/sites-administering/tc-msconf.md#activating-the-translator-service-configurations).

La procédure suivante utilise l’interface utilisateur optimisée pour les écrans tactiles pour créer une configuration Microsoft® Translator .

1. Sur le rail, cliquez ou appuyez sur Outils > Cloud Services.
1. Dans la zone Microsoft® Translator , sélectionnez Afficher les configurations.
1. Cliquez sur le lien + en regard de Configurations disponibles.

   ![chlimage_1-382](assets/chlimage_1-382.png)

1. Indiquez un titre pour votre configuration. Le titre identifie la configuration dans la console Cloud Services et dans les listes déroulantes des propriétés de page. Le nom par défaut est dérivé du titre. Éventuellement, saisissez un nom à utiliser pour le nœud du référentiel qui stocke la configuration. Utilisez la valeur par défaut de la propriété Parent Configuration qui est le chemin d’accès du noeud du référentiel.
1. Cliquez sur Créer.
1. Dans la boîte de dialogue qui s’affiche, saisissez les valeurs des propriétés, puis cliquez sur OK.

## Exemples de configurations du Cloud Service de traducteur Microsoft® {#sample-microsoft-translator-cloud-service-configurations}

Les configurations de service cloud Microsoft® Translator suivantes sont installées avec les exemples de Geometrixx. Certains exemples de configuration utilisent un compte de traduction Microsoft® d’évaluation qui permet de traduire gratuitement un maximum de 2 000 000 caractères par mois.

### Licence d’évaluation du traducteur Microsoft® {#microsoft-translator-trial-license}

La configuration de la licence d’évaluation du traducteur Microsoft® est un exemple de configuration qui est installé avec l’exemple de package Geometrixx Outdoors. Cette configuration utilise un compte de traducteur Microsoft® qui comporte un abonnement gratuit qui permet de traduire 2 000 000 caractères par mois.

### Licence d’évaluation du traducteur Microsoft® - Geometrixx-dehors {#microsoft-translator-trial-license-geometrixx-outdoors}

La configuration Licence d’évaluation du traducteur Microsoft® - Geometrixx-outdoors est un exemple de configuration qui est installé avec des Geometrixx Outdoors. Cette configuration utilise le même compte Microsoft® Translator gratuit que la configuration Licence d’évaluation du traducteur Microsoft®. Le compte dispose d’un abonnement gratuit qui permet de traduire 2 000 000 de caractères par mois.

Cette configuration du traducteur Microsoft® est optimisée pour une utilisation avec le type de contenu de l’exemple de site des Geometrixx Outdoors.

### Mise À Niveau De La Configuration De La Licence D’Évaluation De Microsoft® Translator {#upgrading-the-microsoft-translator-trial-license-configuration}

Les pages de configuration de traduction de Microsoft® fournissent un lien pratique vers le site web de Microsoft® pour obtenir un abonnement de compte adapté aux systèmes de production.

1. Sur le rail, cliquez ou appuyez sur Outils > Opérations > Cloud > Cloud Services.
1. Dans la zone Microsoft® Translator, cliquez ou appuyez sur Afficher les configurations, puis cliquez ou appuyez sur Microsoft® Translator Trial License (Microsoft® Translation Configuration).

   ![chlimage_1-383](assets/chlimage_1-383.png)

1. Sur la page de configuration, cliquez sur Mettre à niveau l’abonnement. Utilisez la page web Microsoft® qui s’ouvre pour configurer votre compte.

   ![chlimage_1-384](assets/chlimage_1-384.png)

### Personnalisation de votre moteur de traducteur Microsoft® {#customizing-your-microsoft-translator-engine}

Les pages de configuration de traduction de Microsoft® fournissent un lien pratique vers le site web de Microsoft® pour personnaliser votre moteur de traduction Microsoft®. ([https://www.microsoft.com/en-us/research/project/microsoft-translator-hub/](https://www.microsoft.com/en-us/research/project/microsoft-translator-hub/))

1. Sur le rail, cliquez ou appuyez sur Outils > Opérations > Cloud > Cloud Services.
1. Dans la zone Microsoft® Translator, cliquez ou appuyez sur Afficher les configurations, puis cliquez ou appuyez sur la configuration que vous souhaitez personnaliser.
1. Sur la page de configuration, cliquez sur Personnaliser le traducteur. Utilisez la page web Microsoft® qui s’ouvre pour personnaliser votre service.

## Activation des configurations du service de traducteur {#activating-the-translator-service-configurations}

Pour prendre en charge le contenu traduit répliqué vers l’instance de publication, activez les configurations de service cloud. Pour activer les noeuds du référentiel qui stockent les configurations du service cloud Microsoft® Translator ou de tiers, utilisez la méthode de [activation d’une section complète (arborescence)](/help/sites-authoring/publishing-pages.md#publishing-and-unpublishing-a-tree). Les nœuds se trouvent sous les nœuds parents suivants :

* Service de traduction Microsoft® : /libs/settings/cloudconfigs/translation/msft-translation
* Service de traduction tiers : /etc/cloudservices/machine-translation
