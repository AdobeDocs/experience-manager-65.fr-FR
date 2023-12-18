---
title: Structure de l’interface utilisateur tactile d’Adobe Experience Manager
description: L’IU optimisée pour les écrans tactiles, telle qu’elle est implémentée dans Adobe Experience Manager, comporte plusieurs principes sous-jacents et se compose de plusieurs éléments clés.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
exl-id: e562b289-5d8b-4fa8-ad1c-fff5f807a45e
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: ht
source-wordcount: '855'
ht-degree: 100%

---

# Structure de l’interface utilisateur tactile d’Adobe Experience Manager{#structure-of-the-aem-touch-enabled-ui}

L’IU tactile d’Adobe Experience Manager (AEM) s’accompagne de plusieurs principes sous-jacents et se compose d’une série d’éléments clés :

## Consoles {#consoles}

### Redimensionnement et mise en page de base {#basic-layout-and-resizing}

L’interface utilisateur convient à la fois aux appareils mobiles et aux ordinateurs de bureau. Cependant, au lieu de créer deux styles distincts, Adobe a décidé d’utiliser un seul style qui fonctionne pour tous les écrans et terminaux.

Tous les modules utilisent la même disposition de base. Dans AEM, cela se traduit visuellement comme suit :

![chlimage_1-142](assets/chlimage_1-142.png)

La disposition adhère au style Responsive Design et s’adapte à la taille de l’appareil ou de la fenêtre que vous utilisez.

Par exemple, si la résolution passe sous 1 024 pixels (comme c’est le cas sur un appareil mobile), l’affichage est adapté en conséquence :

![chlimage_1-143](assets/chlimage_1-143.png)

### Barre d’en-tête {#header-bar}

![chlimage_1-144](assets/chlimage_1-144.png)

La barre d’en-tête affiche des éléments globaux, parmi lesquels :

* Le logo et le produit ou la solution spécifique en cours d’utilisation. Pour AEM, cela constitue également un lien vers la navigation globale.
* Rechercher
* Icône d’accès aux ressources d’aide.
* Icône d’accès à d’autres solutions.
* Un indicateur pour les alertes ou les éléments de boîte de réception en attente (ainsi que la possibilité d’y accéder).
* L’icône de l’utilisateur, ainsi qu’un lien vers la gestion de votre profil

### Barre d’outils {#toolbar}

Cet élément varie en fonction de votre emplacement et des outils de surface permettant de contrôler la vue ou des ressources dans la page en dessous. La barre d’outils est propre au produit, mais elle contient des éléments communs.

Quel que soit l’emplacement, la barre d’outils affiche les actions actuellement disponibles :

![chlimage_1-145](assets/chlimage_1-145.png)

Le contenu dépend également de la sélection ou non d’une ressource :

![chlimage_1-146](assets/chlimage_1-146.png)

### Rail de gauche {#left-rail}

Le rail de gauche peut être ouvert/masqué suivant les besoins afin d’afficher les éléments suivants :

* **Chronologie**
* **Références**
* **Filtrer**

La valeur par défaut est **Contenu uniquement** (rail masqué).

![chlimage_1-147](assets/chlimage_1-147.png)

## Création de pages {#page-authoring}

Lors de la création de pages, les zones structurelles sont les suivantes.

### Cadre de contenu {#content-frame}

Le contenu de la page est rendu dans le cadre de contenu. Le cadre de contenu est indépendant de l’éditeur, afin de s’assurer qu’il n’existe aucun conflit dû aux CSS ou à JavaScript.

Le cadre de contenu se situe dans la partie droite de la fenêtre, sous la barre d’outils.

![chlimage_1-148](assets/chlimage_1-148.png)

### Cadre d’éditeur {#editor-frame}

Le cadre d’éditeur exécute les fonctions d’édition.

Le cadre d’éditeur est un conteneur (abstrait) pour l’ensemble des *éléments de création de pages*. Il se situe au-dessus du cadre de contenu et comprend les éléments suivants :

* la barre d’outils supérieure
* le panneau latéral
* tous les recouvrements
* tout autre élément de création de page, comme la barre d’outils des composants, par exemple

![chlimage_1-149](assets/chlimage_1-149.png)

### Panneau latéral {#side-panel}

Il contient deux onglets par défaut qui vous permettent de sélectionner des ressources et des composants. Ils peuvent être déplacés à partir d’ici pour être déposés sur la page.

Par défaut, le panneau latéral est masqué. Lorsqu’il est sélectionné, soit il est affiché sur le côté gauche, soit il recouvre l’intégralité de la fenêtre lorsque la largeur de la fenêtre est inférieure à 1 024 pixels (par exemple, sur un appareil mobile).

![chlimage_1-150](assets/chlimage_1-150.png)

### Panneau latéral – Ressources {#side-panel-assets}

Dans l’onglet Ressources, vous pouvez effectuer un choix parmi une sélection de ressources. Vous pouvez également filtrer selon un terme spécifique ou sélectionner un groupe.

![chlimage_1-151](assets/chlimage_1-151.png)

### Panneau latéral – Groupes de ressources {#side-panel-asset-groups}

L’onglet Ressources comprend un menu déroulant que vous pouvez utiliser pour sélectionner les groupes de ressources spécifiques.

![chlimage_1-152](assets/chlimage_1-152.png)

### Panneau latéral – Composants {#side-panel-components}

Dans l’onglet Composants, vous pouvez effectuer un choix parmi une sélection de composants. Vous pouvez également filtrer selon un terme spécifique ou sélectionner un groupe.

![chlimage_1-153](assets/chlimage_1-153.png)

### Recouvrements {#overlays}

Ils recouvrent le cadre de contenu et sont utilisés par les [calques](#layer) pour appliquer le mécanisme d’interaction (de manière transparente) avec les composants et leur contenu.

Les recouvrements résident dans le cadre d’éditeur (avec tous les autres éléments de création de pages) même si, en fait, ils recouvrent les composants appropriés dans le cadre de contenu.

![chlimage_1-154](assets/chlimage_1-154.png)

### Calque {#layer}

Un calque est un groupe indépendant de fonctionnalités pouvant être activées pour :

* fournir une vue différente de la page ;
* vous permettre de manipuler une page et/ou d’interagir avec celle-ci.

Les calques fournissent des fonctionnalités sophistiquées pour toute la page, par opposition aux actions spécifiques sur un composant individuel.

AEM s’accompagne de plusieurs calques qui sont déjà implémentés pour la création de pages. Il s’agit notamment de l’édition, de la prévisualisation et de l’annotation.

>[!NOTE]
>
>Les calques sont un concept puissant qui affecte la vue de l’utilisateur ou de l’utilisatrice et son interaction avec le contenu de la page. Lorsque vous développez vos propres calques, vous devez vous assurer que le calque est nettoyé à sa sortie.

### Sélecteur de calques {#layer-switcher}

Le sélecteur de calques vous permet de choisir le calque à utiliser. Lorsqu’il est fermé, il indique le calque en cours d’utilisation.

Le sélecteur de calques se présente sous la forme d’un menu déroulant dans la barre d’outils (dans la partie supérieure de la fenêtre, à l’intérieur du cadre d’éditeur).

![chlimage_1-155](assets/chlimage_1-155.png)

### Barre d’outils des composants {#component-toolbar}

Lorsque vous cliquez sur une instance d’un composant (simple clic ou double-clic lent), sa barre d’outils est affichée. La barre d’outils contient les actions spécifiques (par exemple, copier, coller, ouvrir l’éditeur) qui sont disponibles pour l’instance du composant (modifiable) sur la page.

En fonction de l’espace disponible, les barres d’outils de composant sont placées dans le coin supérieur ou inférieur droit du composant approprié.

![chlimage_1-156](assets/chlimage_1-156.png)

## Informations supplémentaires {#further-information}

Pour plus d’informations sur les concepts relatifs à l’IU tactile, reportez-vous à [Concepts de l’interface utilisateur tactile d’AEM](/help/sites-developing/touch-ui-concepts.md).

Pour plus d’informations techniques, consultez la [documentation JS](https://helpx.adobe.com/fr/experience-manager/6-5/sites/developing/using/reference-materials/jsdoc/ui-touch/editor-core/index.html) relative à l’éditeur de page tactile.
