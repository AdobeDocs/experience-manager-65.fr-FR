---
title: Composants Présentation
seo-title: Composants
description: Les composants sont des unités modulaires qui exécutent des fonctionnalités spécifiques pour présenter du contenu sur votre site web.
seo-description: Composants sont des unités modulaires qui offrent des fonctionnalités spécifiques pour présenter votre contenu sur votre site Web.
uuid: fb39aeb8-8f43-4091-8083-ebfab89e6e63
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 45efff93-2fe5-4313-83a0-0e23a540da93
translation-type: tm+mt
source-git-commit: 5597fb39500ac1f85d03263bfa1e5239d35d2a2c
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 64%

---


# Présentation des composants{#components-overview}

Cette page donne un aperçu des composants AEM (Adobe Experience Manager), tels que ceux [utilisés pour la création de pages](/help/sites-authoring/default-components-foundation.md).

## Que sont les composants ? {#what-exactly-is-a-component}

* Unités modulaires qui réalisent des fonctionnalités spécifiques pour présenter votre contenu sur votre site Web.
* Réutilisable.
* Développé en tant qu&#39;unités autonomes dans un dossier du référentiel.
* Ils ne comportent aucun fichier de configuration masqué.
* Ils peuvent contenir d’autres composants.
* Ils peuvent s’exécuter n’importe où dans n’importe quel système AEM ; leur exécution peut également être limitée à des composants spécifiques.
* Ils possèdent une interface utilisateur standardisée.
* Comportement de modification pouvant être configuré.
* Utiliser des boîtes de dialogue créées à l’aide de sous-éléments basés sur des composants de l’interface utilisateur Granite
* Are developed using [HTL](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html) (recommended) or JSP.
* Ils peuvent être développés pour créer des composants personnalisés qui étendent les fonctionnalités par défaut.

Compte tenu de la nature modulaire des composants, vous pouvez effectuer les opérations suivantes :

* Développer un nouveau composant sur votre instance locale.
* Déployez-le sur votre environnement de test.
* Déployer le composant sur votre environnement de création actif et permettre ainsi aux auteurs et/ou développeurs d’ajouter et de configurer du contenu.
* Déployez-le sur vos environnements de publication en direct, où il est utilisé pour générer du contenu pour des visiteurs sur votre site Web. Certains composants (c’est le cas de Communities, par exemple) acceptent la saisie de contenu de la part des utilisateurs.

Chaque composant AEM :

* Est un type de ressource.
* Collection de scripts qui réalisent complètement une fonction spécifique.
* Can function in *isolation*, meaning either within AEM or a portal.

## Composants prêts à l’emploi dans AEM {#out-of-the-box-components-within-aem}

AEM est fourni avec un éventail de [composants prêts à l’emploi](/help/sites-authoring/default-components.md) qui procurent des fonctionnalités complètes :

* Système de paragraphes ( `parsys`)
* Page ( `responsivegrid` - touch-enabled UI only)
* Text (Texte)
* Image, avec texte d’accompagnement
* Barre d’outils

Les composants fournis et leur utilisation dans les [exemples de sites web We.Retail](/help/sites-developing/we-retail.md) illustrent l’implémentation et l’utilisation des composants. Les composants sont fournis avec l’intégralité du code source et peuvent être utilisés tels quels ou comme points de départ pour des composants modifiés ou étendus.

### Composants principaux et composants de base {#core-components-and-foundation-components}

Il existe deux groupes de composants AEM fournis par Adobe :

* [Composants principaux](https://docs.adobe.com/content/help/fr-FR/experience-manager-core-components/using/introduction.html)
* [Composants de base](/help/sites-authoring/default-components-foundation.md)

**Les composants** principaux ont été introduits avec AEM 6.3 et l&#39;offre de fonctionnalités de création flexibles et riches en fonctionnalités. The [We.Retail reference site](/help/sites-developing/we-retail.md) illustrates how the core components can be used and represent the current best-practices of component development.

Les **composants de base** sont fournis avec AEM depuis de nombreuses versions et sont disponibles prêts à l’emploi dans une installation AEM standard. Bien qu’ils soient toujours pris en charge, la plupart d’entre eux ont été abandonnés, ne sont plus améliorés et reposent sur des technologies héritées.

>[!NOTE]
>
>Les [composants principaux](https://docs.adobe.com/content/help/fr-FR/experience-manager-core-components/using/introduction.html) représentent les méthodes recommandées en matière de conception et de développement de composants. Ils font également office d’implémentations de référence.
>
>[Les outils](modernization-tools.md) de modernisation AEM peuvent aider à migrer vers les composants principaux.

### Affichage des composants disponibles {#viewing-available-components}

Pour avoir un aperçu de tous les composants disponibles dans votre instance AEM, utilisez la [console Composants](/help/sites-authoring/default-components-console.md).

Une autre méthode consiste à utiliser CRXDE Lite pour obtenir la liste de tous les composants disponibles dans le référentiel.

1. In **[!UICONTROL CRXDE Lite]**, select **[!UICONTROL Tools]** from the toolbar, then **[!UICONTROL Query]**, which opens the **[!UICONTROL Query]** tab.

1. Dans l’onglet **[!UICONTROL Requête]**, sélectionnez `XPath` comme **[!UICONTROL Type]**.

1. Dans la zone de saisie **[!UICONTROL Requête]**, entrez la chaîne suivante :

   `//element(*, cq:Component)`

1. Click **[!UICONTROL Execute]** and the components are listed.

## Ressources supplémentaires {#further-reading}

Les pages suivantes fournissent des informations plus détaillées sur le développement de ces composants et d&#39;autres composants :

* [Composants AEM – Principes de base](/help/sites-developing/components-basics.md)
* [Développement de composants AEM](/help/sites-developing/developing-components.md)
* [Développement de composants AEM – Échantillons de code](/help/sites-developing/developing-components-samples.md)
* [Configuration de plusieurs éditeurs statiques](/help/sites-developing/multiple-inplace-editors.md)
* [Mode Développeur](/help/sites-developing/developer-mode.md)
* [Test de votre interface utilisateur](/help/sites-developing/hobbes.md)
* [Composants pour les fragments de contenu](/help/sites-developing/components-content-fragments.md)
* [Obtention des informations sur la page au format JSON](/help/sites-developing/pageinfo.md) 
* [Internationalisation des composants](/help/sites-developing/i18n.md)
* [Composants principaux](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html)
* [Utilisation de conditions de masquage](/help/sites-developing/hide-conditions.md)
* IU classique

   * [Composants AEM (IU classique)](/help/sites-developing/developing-components-classic.md)
   * [Utilisation et extension de widgets (IU classique)](/help/sites-developing/widgets.md)
   * [Utilisation de xtypes (IU classique)](/help/sites-developing/xtypes.md)
   * [Développement de formulaires (IU classique)](/help/sites-developing/developing-forms.md)

