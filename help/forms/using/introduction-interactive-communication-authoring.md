---
title: Introduction à l’interface utilisateur de création d’une communication interactive
seo-title: Introduction aux différents éléments de l’interface utilisateur permettant de créer une communication interactive
description: Introduction aux différents éléments de l’interface utilisateur permettant de créer une communication interactive
seo-description: Introduction aux différents éléments de l’interface utilisateur permettant de créer une communication interactive
uuid: e8c5b1e8-b2bb-46b4-b42e-1f343192641a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: interactive-communications
discoiquuid: 5855d21b-340c-4139-aabe-c3a534cedb98
docset: aem65
translation-type: tm+mt
source-git-commit: 726163106ddb80600eaa7cc09b1a2e9b035a223e

---


# Introduction à l’interface utilisateur de création d’une communication interactive{#introduction-to-interactive-communication-authoring-ui}

The user interface for authoring [Interactive Communication](/help/forms/using/interactive-communications-overview.md) is intuitive and provides the following for authoring print and web channel of the Interactive Communication:

* Editeur de document glisser-déposer WYSIWYGM
* Référentiel intégré pour les ressources : les ressources transférées et créées sur le serveur sont disponibles dans l’explorateur d’actifs de l’interface de création Interactive Communication.

Lorsque vous [créez une communication interactive ou en modifiez une existante](../../forms/using/create-interactive-communication.md), vous utilisez les éléments suivants de l’interface utilisateur :

* [Barre latérale](#sidebar)
* [Barre d’outils Page](#page-toolbar)
* [Barre d’outils de composants](#component-toolbar)
* Zone de contenu

![Interface utilisateur de création de communication interactive](assets/form-editor.png)

**A.** Barre latérale **B.** Barre d’outils **C.** Zone de contenu

## Barre latérale {#sidebar}

![Barre latérale](assets/sidebar-comps-2.png)

**A.**  navigateur **B.** Explorateur de contenu **C.** Explorateur de propriétés **D.** Explorateur de ressources **E.** Explorateur de composants **F.** Navigateur des sources de données - Modèle de données **G.** Explorateur de sources de données - Contenu principal

<!-- Click to enlarge

![sidebar-comps-3](assets/sidebar-comps-3.png)-->

La barre latérale contient les éléments suivants :

* **Explorateur de canaux**

L’explorateur de canaux vous permet de basculer entre les canaux d’impression et les canaux Web de la communication interactive. En fonction du canal que vous avez sélectionné dans l’explorateur de canaux, les navigateurs, tels que Contenu et Composants, affichent les options.

* **Explorateur** de contenu Dans l’explorateur de contenu, vous pouvez voir la hiérarchie d’objets du  pour le sélectionné. L’auteur peut accéder au composant spécifique en appuyant sur cet élément dans l’arborescence de l’objet de document. L’auteur peut alors rechercher des objets dans le canal web et les réorganiser depuis l’arborescence.

* **Explorateur de propriétés**

   Permet de modifier les propriétés d’un composant. Les propriétés affichées varient en fonction du composant. For example, to see properties of the document container:
Select a component, then tap ![field-level](assets/field-level.png) > **Document Container**, and then tap ![cmppr](assets/cmppr.png).

* **Explorateur** de ressources Sépare différents types de contenu, tels que des fragments de mise en page, des images, des , des pages et des vidéos. L’auteur peut glisser-déposer des actifs dans la communication interactive.

* **L’explorateur de composants** inclut les composants que vous pouvez utiliser pour créer les canaux d’impression et web d’un document. Vous pouvez faire glisser des composants vers Interactive Communication pour ajouter des éléments et configurer l’élément ajouté selon les exigences. Le tableau ci-dessous décrit les composants répertoriés dans l’explorateur de composants pour les canaux d’impression et web :

| **Composant** | **Canal d’impression** | **Canal web** | **Fonctionnalité** |
|---|---|---|---|
| Graphique | ✓ | ✓ | Ajoute un graphique que vous pouvez utiliser dans une communication interactive pour la représentation visuelle des données bidimensionnelles extraites d’un élément de collection du modèle de données de formulaire. |
| Fragment de document | ✓ | ✓ | Permet d’ajouter un composant, un texte, un  ou une condition réutilisable à une communication interactive. Le composant réutilisable que vous ajoutez à une communication interactive peut être basé sur un modèle de données de formulaire ou sans modèle de données de formulaire. |
| Image | ✓ | ✓ | Permet d’insérer une image. |
| Panneau | - | ✓ | Le composant Panneau est un espace réservé pour regrouper d’autres composants et contrôle la disposition d’un groupe de composants dans une communication interactive. Un composant de panneau vous permet également de permettre la répétition d’un groupe de composants pour l’utilisateur final, par exemple dans plusieurs entrées requises pour remplir les informations d’identification. Il est également recommandé d’utiliser un panneau pour un onglet d’une communication interactive avec plusieurs onglets. |
| Tableau | * | ✓ | Ajoute un tableau qui permet de classer les données par lignes et par colonnes. |
| Zone cible | ** | ✓ | Insère une zone cible dans un canal web pour organiser les composants spécifiques au canal web. |
| Text (Texte) | - | ✓ | Ajoute le texte au canal web d’une communication interactive. Le texte peut utiliser des objets de modèle de données de formulaire pour rendre le contenu dynamique. |

* Utilisez les fragments de mise en page dans le canal d’impression pour ajouter des tableaux.

** Dans le canal d’impression, les zones cibles sont prédéfinies dans le XDP/modèle d’impression. Vous ne pouvez pas ajouter de nouvelles zones cibles à l’aide de l’interface utilisateur de création de communication interactive.

* **Explorateur de sources de données** L’explorateur de sources de données affiche les sources de données disponibles dans le modèle de données de formulaire que vous avez sélectionné lors de la création de la communication interactive.

### Points clés pour l’utilisation de composants {#key-points-for-working-with-components}

Les points clés lorsque vous utilisez des composants de communication interactive sont les suivants :

* Chaque composant est associé à des propriétés qui contrôlent son apparence et ses fonctionnalités. To configure the properties of a component, tap the component and tap ![cmppr](assets/cmppr.png) to open the component properties in the Properties browser.
* Un composant est identifié par son nom d’élément. When you tap ![cmppr](assets/cmppr.png), you can change the name of the component by changing the Element Name field value in the properties browser. Vous pouvez saisir uniquement des lettres, des chiffres, des traits d’union (-) et des traits de soulignement (_) dans le champ Nom de l’élément. D’autres caractères spéciaux ne sont pas autorisés et le nom de l’élément doit commencer par une lettre.
* Vous pouvez modifier la propriété Title d’un composant Interactive Communication en ligne dans l’éditeur sans ouvrir le navigateur Propriétés tant que le titre est visible dans Interactive Communication. Pour ce faire :

   1. Appuyez pour sélectionner un composant qui a une propriété Titre et dont la propriété Masquer le titre est désactivée.
   1. Appuyez sur ![aem_6_3_edit](assets/aem_6_3_edit.png) pour rendre le titre modifiable.

   1. Modifiez le titre et appuyez sur la touche Retour ou appuyez n’importe où en dehors du composant pour enregistrer les modifications. Appuyez sur la touche Échap pour annuler les modifications.

## Barre d’outils de composants {#component-toolbar}

![Libellés de la barre d’outils de composants](do-not-localize/component_toolbar_labels_new.png)

Lorsque vous sélectionnez un composant, une barre d’outils s’affiche, vous permettant de l’utiliser. Vous avez la possibilité de couper, coller, déplacer et spécifier les propriétés des composants. Vous avez le choix entre :

A.**Configurer** : Permet d’afficher les propriétés du composant dans la barre latérale. ****,

B.**Edit Rules**: When you tap Edit Rules, Rule Editor appears in which you can edit and create rules for the selected component. Dans l’éditeur de règles, vous pouvez également sélectionner d’autres objets de formulaire (composants) et modifier/créer des règles pour ces objets de formulaire.

C.** Copier** : permet de copier un composant et le coller ailleurs dans la communication interactive.

D.**Cut**: You can use the cut option to move a component from one place to another in the Interactive Communication.

E. **Delete**: Lets you delete the component from the Interactive Communication.

F. **Insert Component**: Lets you insert a component above the selected component.

G. **Paste**: Lets you paste the component you cut or copied using the options described above.

H. **Groupe** : permet de sélectionner plusieurs composants permettant de couper, copier ou coller plusieurs composants ensemble.

I.**Parent** : Permet de sélectionner le parent d’un composant.

J.  **SOM  :** Vous permet de  l’de  [SOM](../../forms/using/using-som-expressions-adaptive-forms.md) pour le composant.

K : Associer des objets **dans le panneau :** Vous permet de grouper les composants d’un panneau afin de pouvoir effectuer des opérations simultanément sur ces composants. Pour plus d’informations, voir [Associer des objets dans le panneau](create-interactive-communication.md#groupobjectspanel).

L. Panneau **enfant** Ajouter (pour les panneaux uniquement) : Vous permet d’ajouter un panneau enfant au panneau.

M : Barre d’outils **du panneau** Ajouter (pour les panneaux uniquement) : vous permet d’ajouter la barre d’outils pour le composant Panneau. Vous pouvez ensuite exécuter d’autres actions sur la barre d’outils.

En outre, l’option **Remplacer** de la barre d’outils vous permet de remplacer le composant existant par un autre composant. Cette option n’est pas disponible pour le composant Panneau.

## Barre d’outils Page {#page-toolbar}

La barre d’outils Page en haut de la page propose des options qui vous permettent de  la communication interactive et de modifier ses propriétés. Vous pouvez  la communication interactive lorsque vous la concevez et apporter les modifications nécessaires. Dans la barre d’outils de la page, vous voyez :

* Toggle Side Panel ![toggle-side-panel](assets/toggle-side-panel.png): Lets you show or hide Sidebar.
* Page information ![pageinformationad](assets/pageinformationad.png): Lets you view page properties.
* Emulator ![ruler](assets/ruler.png): Lets you emulate the look of your Interactive Communication for different display sizes such as tablets and phones.
* Modifier : Sélectionne d’autres modes comme Modifier, Style, Développeur et Conception.

   * Modifier : Permet de modifier les propriétés de la communication interactive et de ses composants. Exemple : l’ajout d’un composant, le dépôt d’une image et l’indication des champs obligatoires.
   * Style : définit l’aspect des composants de votre communication interactive. Par exemple, en mode Style, vous pouvez sélectionner un panneau et définir sa couleur d’arrière-plan.
   * Développeur : Permet aux développeurs de :

      * Découvrez la composition d&#39;Interactive Communication.
      * Déboguer en temps réel afin de mieux résoudre les problèmes.
   *  : Permet d’activer ou de désactiver les composants personnalisés ou les composants prêts à l’emploi qui ne sont pas répertoriés dans la barre latérale.


*  : Vous permet de  l’aspect de la communication interactive lorsque vous la publiez.

