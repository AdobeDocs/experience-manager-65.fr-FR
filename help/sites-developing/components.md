---
title: Aperçu des composants
seo-title: Components
description: Les composants sont des unités modulaires qui exécutent des fonctionnalités spécifiques pour présenter du contenu sur votre site web.
seo-description: Components are modular units which realize specific functionality to present your content on your website
uuid: fb39aeb8-8f43-4091-8083-ebfab89e6e63
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 45efff93-2fe5-4313-83a0-0e23a540da93
exl-id: 9e30c969-2692-4380-943a-b022ee900ce8
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 77%

---

# Aperçu des composants{#components-overview}

Cette page donne un aperçu des composants AEM (Adobe Experience Manager), tels que ceux [utilisés pour la création de pages](/help/sites-authoring/default-components-foundation.md).

## Que sont les composants ?  {#what-exactly-is-a-component}

* sont des unités modulaires qui exécutent des fonctionnalités spécifiques pour présenter du contenu sur votre site web ;
* peuvent être réutilisés ;
* sont développés comme des unités autonomes dans un seul dossier du référentiel ;
* ne comportent aucun fichier de configuration masqué ;
* peuvent contenir d’autres composants ;
* Peut s’exécuter n’importe où dans n’importe quel système AEM. Elles peuvent également être limitées à l’exécution sous des composants spécifiques.
* possèdent une interface utilisateur standardisée ;
* sont associés à un comportement de modification qui peut être configuré ;
* utilisent des boîtes de dialogue créées à l’aide de sous-éléments basés sur les composants de l’interface utilisateur Granite ;
* peuvent être développés à l’aide de [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/using/overview.html?lang=fr) (recommandé) ou de JSP.
* peuvent être développés pour créer des composants personnalisés qui étendent les fonctionnalités par défaut.

Les composants étant modulaires, vous pouvez :

* Développez un nouveau composant sur votre instance locale.
* Déployer ce composant sur votre environnement de test.
* Déployer le composant sur votre environnement de création actif et permettre ainsi aux auteurs et/ou développeurs d’ajouter et de configurer du contenu.
* Déployer le composant sur votre (vos) environnement(s) de publication actif(s), où il est utilisé pour effectuer le rendu du contenu à l’intention des visiteurs de votre site Web. Certains composants, par exemple, pour Communities, acceptent également la saisie de vos utilisateurs.

Chaque composant AEM :

* est un type de ressource ;
* est un ensemble de scripts qui exécutent complètement une fonction spécifique ;
* peut fonctionner de manière *isolée*, c’est-à-dire soit dans AEM, soit dans un portail.

## Composants prêts à l’emploi dans AEM {#out-of-the-box-components-within-aem}

AEM est fourni avec une variété de [Composants prêts à l’emploi](/help/sites-authoring/default-components.md) qui offrent des fonctionnalités complètes, notamment :

* Système de paragraphes (`parsys`)
* Page (`responsivegrid` ; IU tactile uniquement)
* Texte
* Image, avec texte d’accompagnement
* Barre d’outils

Les composants fournis et leur utilisation dans la variable [exemples de sites web We.Retail](/help/sites-developing/we-retail.md) fournies illustrent la mise en oeuvre et l’utilisation des composants. Les composants sont fournis avec l’intégralité du code source et peuvent être utilisés tels quels ou comme points de départ pour des composants modifiés ou étendus.

### Composants principaux et composants de base {#core-components-and-foundation-components}

Deux ensembles de composants d’AEM fournis par l’Adobe sont disponibles :

* [Composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=fr)
* [Composants de base](/help/sites-authoring/default-components-foundation.md)

**Les composants principaux** ont été introduits dans AEM 6.3. Ils offrent des fonctionnalités de création à la fois souples et particulièrement puissantes. Le [site de référence We.Retail](/help/sites-developing/we-retail.md) illustre la manière dont ces composants peuvent être utilisés et présente les bonnes pratiques en termes de développement de composants.

Les **composants de base** sont fournis avec AEM depuis de nombreuses versions et sont disponibles prêts à l’emploi dans une installation AEM standard. Bien que ces composants soient toujours pris en charge, la plupart d’entre eux sont obsolètes, reposent sur des technologies plus anciennes et leur développement a été arrêté.

>[!NOTE]
>
>Les [composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=fr) représentent les méthodes recommandées en matière de conception et de développement de composants. Ils font également office d’implémentations de référence.
>
>Les [outils de modernisation d’AEM](modernization-tools.md) peuvent vous aider à migrer vers les composants principaux.

### Affichage des composants disponibles {#viewing-available-components}

Pour un aperçu de tous les composants disponibles dans votre instance AEM, utilisez la méthode [Console Composants](/help/sites-authoring/default-components-console.md).

Vous pouvez également utiliser CRXDE Lite pour obtenir la liste de tous les composants disponibles dans le référentiel.

1. Dans **[!UICONTROL CRXDE Lite]**, sélectionnez **[!UICONTROL Outils]** dans la barre d’outils, puis sélectionnez **[!UICONTROL Requête]** pour ouvrir l’onglet **[!UICONTROL Requête]**.

1. Dans l’onglet **[!UICONTROL Requête]**, sélectionnez `XPath` comme **[!UICONTROL Type]**.

1. Dans la zone de saisie **[!UICONTROL Requête]**, entrez la chaîne suivante :

   `//element(*, cq:Component)`

1. Cliquez sur **[!UICONTROL Exécuter]** pour répertorier les composants.

## Ressources supplémentaires {#further-reading}

Les pages suivantes fournissent des informations plus détaillées sur le développement de ces composants et d’autres :

* [Composants AEM – Notions de base](/help/sites-developing/components-basics.md)
* [Développement de composants AEM](/help/sites-developing/developing-components.md)
* [Développement de composants AEM – Échantillons de code](/help/sites-developing/developing-components-samples.md)
* [Configuration de plusieurs éditeurs statiques](/help/sites-developing/multiple-inplace-editors.md)
* [Mode Développeur](/help/sites-developing/developer-mode.md)
* [Tester votre IU](/help/sites-developing/hobbes.md)
* [Composants pour les fragments de contenu](/help/sites-developing/components-content-fragments.md)
* [Obtention d’informations sur la page au format JSON](/help/sites-developing/pageinfo.md)
* [Internationalisation de composants](/help/sites-developing/i18n.md)
* [Composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=fr)
* [Utilisation de conditions de masquage](/help/sites-developing/hide-conditions.md)
* Interface utilisateur classique

   * [Composants AEM (IU classique)](/help/sites-developing/developing-components-classic.md)
   * [Utilisation et extension de widgets (IU classique)](/help/sites-developing/widgets.md)
   * [Utilisation des xtypes (IU classique)](/help/sites-developing/xtypes.md)
   * [Développement de formulaires (IU classique)](/help/sites-developing/developing-forms.md)
