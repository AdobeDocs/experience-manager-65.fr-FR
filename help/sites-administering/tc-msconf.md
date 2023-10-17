---
title: Connexion à Microsoft® Translator
description: Découvrez comment connecter Adobe Experience Manager à Microsoft&reg; Translator.
contentOwner: Guillaume Carlino
feature: Language Copy
exl-id: ca575a30-fc3e-4f38-9aa7-dbecbc089f87
source-git-commit: eaffc71c23c18d26ec5cbb2bbb7524790c4826fe
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 98%

---

# Connexion à Microsoft® Translator{#connecting-to-microsoft-translator}

Créez une configuration afin que le service cloud Microsoft® Translator utilise votre compte Microsoft® Translator pour traduire le contenu de pages, le contenu de communauté ou de ressources d’AEM.

| Propriété | Description |
|---|---|
| Libellé de traduction | Nom d’affichage du service de traduction. |
| Attribution de traduction | (Facultatif) Pour le contenu créé par l’utilisateur, l’attribution qui apparaît à côté du texte traduit, par exemple `Translations by Microsoft`. |
| ID d’espace de travail | (Facultatif) ID de votre moteur Microsoft® Translator personnalisé à utiliser. |
| Clé d’abonnement | Votre clé d’abonnement Microsoft® pour Microsoft® Translator. |

Après avoir créé la configuration, vous devez [l’activer](/help/sites-administering/tc-msconf.md#activating-the-translator-service-configurations).

La procédure suivante utilise l’interface utilisateur optimisée pour les écrans tactiles afin de créer une configuration Microsoft® Translator.

1. Sur le rail, cliquez ou appuyez sur Outils > Services cloud.
1. Dans la zone Microsoft® Translator, sélectionnez Afficher les configurations.
1. Cliquez sur le lien + en regard de Configurations disponibles.

   ![chlimage_1-382](assets/chlimage_1-382.png)

1. Indiquez un titre pour votre configuration. Le titre identifie la configuration dans la console Services cloud, ainsi que dans les listes déroulantes de propriétés de la page. Le nom par défaut est dérivé du titre. Éventuellement, saisissez un nom à utiliser pour le nœud du référentiel qui stocke la configuration. Utilisez la valeur par défaut de la propriété de configuration parent qui est le chemin d’accès du nœud du référentiel.
1. Cliquez sur Créer.
1. Dans la boîte de dialogue qui s’affiche, saisissez les valeurs des propriétés, puis cliquez sur OK.

## Exemples de configurations du service cloud Microsoft® Translator {#sample-microsoft-translator-cloud-service-configurations}

Les configurations suivantes du service cloud Microsoft® Translator sont installées avec les exemples de Geometrixx. Certains exemples de configurations utilisent un compte d’évaluation de Microsoft® Translator qui permet de traduire gratuitement un maximum de 2 000 000 de caractères par mois.

### Licence d’évaluation de Microsoft® Translator {#microsoft-translator-trial-license}

La configuration Licence d’évaluation de Microsoft® Translator est un exemple de configuration installé avec le package d’exemple Geometrixx Outdoors. Cette configuration utilise un compte Microsoft® Translator titulaire d’un abonnement gratuit qui permet de traduire 2 000 000 de caractères par mois.

### Licence d’évaluation de Microsoft® Translator - Geometrixx-outdoors {#microsoft-translator-trial-license-geometrixx-outdoors}

La configuration Licence d’évaluation de Microsoft® Translator - Geometrixx-outdoors est un exemple de configuration qui est installé avec Geometrixx Outdoors. Cette configuration utilise le même compte Microsoft® Translator gratuit que la configuration Licence d’évaluation de Microsoft® Translator. Le compte dispose d’un abonnement gratuit qui permet de traduire 2 000 000 de caractères par mois.

Cette configuration de Microsoft® Translator est optimisée pour une utilisation avec le type de contenu de l’exemple de site de Geometrixx Outdoors.

### Mettre à niveau la configuration de licence d’évaluation de Microsoft® Translator {#upgrading-the-microsoft-translator-trial-license-configuration}

Les pages de configuration de Microsoft® Translator fournissent un lien pratique vers le site web Microsoft® pour obtenir un abonnement de compte adapté aux systèmes de production.

1. Sur le rail, cliquez ou appuyez sur Outils > Opérations > Cloud > Services cloud.
1. Dans la zone Microsoft® Translator, cliquez ou appuyez sur Afficher les configurations, puis cliquez ou appuyez sur Licence d’évaluation Microsoft® Translator (configuration de Microsoft® Translator).

   ![chlimage_1-383](assets/chlimage_1-383.png)

1. Sur la page de configuration, cliquez sur Mettre à niveau l’abonnement. Utilisez la page web de Microsoft® qui s’ouvre pour configurer votre compte.

   ![chlimage_1-384](assets/chlimage_1-384.png)

### Personnaliser votre moteur Microsoft® Translator {#customizing-your-microsoft-translator-engine}

Les pages de configuration de Microsoft® Translator fournissent un lien pratique vers le site web de Microsoft® pour personnaliser votre moteur Microsoft® Translator ([https://www.microsoft.com/en-us/research/project/microsoft-translator-hub/](https://www.microsoft.com/fr-fr/research/project/microsoft-translator-hub/)).

1. Sur le rail, cliquez ou appuyez sur Outils > Opérations > Cloud > Services cloud.
1. Dans la zone Microsoft® Translator, cliquez ou appuyez sur Afficher les configurations, puis cliquez ou appuyez sur la configuration que vous souhaitez personnaliser.
1. Sur la page de configuration, cliquez sur Personnaliser le traducteur. Utilisez la page web de Microsoft® qui s’affiche pour personnaliser votre service.

## Activer les configurations du service de Translator {#activating-the-translator-service-configurations}

Pour prendre en charge le contenu traduit répliqué vers l’instance de publication, activez les configurations de votre service cloud. Pour activer les nœuds du référentiel qui stockent les configurations du service cloud de Microsoft® Translator ou de tiers, utilisez la méthode d’[activation d’une section complète (arborescence)](/help/sites-authoring/publishing-pages.md#publishing-and-unpublishing-a-tree). Les nœuds se trouvent sous les nœuds parents suivants :

* Service de traduction de Microsoft® : /libs/settings/cloudconfigs/translation/msft-translation
* Service de traduction tiers : /etc/cloudservices/machine-translation
