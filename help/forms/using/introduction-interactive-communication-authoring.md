---
title: Introduction à l’interface utilisateur de création d’une communication interactive
description: Introduction aux différents éléments de l’interface utilisateur permettant de créer une communication interactive
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: interactive-communications
docset: aem65
feature: Interactive Communication
exl-id: 3d15a723-df6c-4b4a-992e-a6636f4cf3dc
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1318'
ht-degree: 100%

---

# Introduction à l’interface utilisateur de création d’une communication interactive{#introduction-to-interactive-communication-authoring-ui}

L’interface utilisateur de création d’une [Communication interactive](/help/forms/using/interactive-communications-overview.md) est intuitive et fournit les éléments suivants pour la création de canaux d’impression et web de la communication interactive :

* Editeur de document glisser-déposer WYSIWYGM
* Référentiel intégré des resources : les ressources téléchargées et créées sur le serveur sont disponibles dans l’explorateur des ressources de l’interface de création des communications interactives.

Lorsque vous [créez une communication interactive ou en modifiez une existante](../../forms/using/create-interactive-communication.md), vous utilisez les éléments suivants de l’interface utilisateur :

* [Barre latérale](#sidebar)
* [Barre d’outils de la page](#page-toolbar)
* [Barre d’outils de composants](#component-toolbar)
* Zone de contenu

![Interface utilisateur de création de communication interactive](assets/form-editor.png)

**A.** Barre latérale **B.** Barre d’outils de la page **C.** Zone de contenu

## Barre latérale {#sidebar}

![Barre latérale](assets/sidebar-comps-2.png)

**A.** Explorateur de canaux **B.** Explorateur de contenu **C.** Explorateur de propriétés **D.** Explorateur de ressources **E.** Explorateur de composants **F.** Explorateur des sources de données - Modèle de données **G.** Explorateur des sources de données - Contenu Principal

<!-- Click to enlarge

![sidebar-comps-3](assets/sidebar-comps-3.png)-->

La barre latérale contient les éléments suivants :

* **Explorateur de canaux**

L’explorateur de canaux vous permet de basculer entre les canaux d’impression et les canaux Web de la communication interactive. En fonction du canal que vous avez sélectionné dans l’explorateur de canaux, les navigateurs, tels que Contenu et Composants, affichent les options.

* **Explorateur de contenu**
Dans l’explorateur de contenu, vous pouvez visualiser la hiérarchie des objets du document pour le canal sélectionné. L’auteur ou l’autrice peut accéder au composant spécifique en appuyant sur cet élément dans l’arborescence de l’objet de document. L’auteur ou l’autrice peut alors rechercher des objets dans le canal web et les réorganiser depuis l’arborescence.

* **Explorateur de propriétés**

  Permet de modifier les propriétés d’un composant. Les propriétés affichées varient en fonction du composant. Par exemple, pour afficher les propriétés du conteneur de documents :
sélectionnez un composant, sélectionnez ![field-level](assets/field-level.png) > **Conteneur de documents** puis ![cmppr](assets/cmppr.png).

* **L’explorateur de ressources**
isole différents types de contenu, tels que des fragments de disposition, des images, des documents, des pages ou des séquences vidéo. L’auteur peut glisser-déposer des actifs dans la communication interactive.

* **L’explorateur de composants** inclut les composants que vous pouvez utiliser pour créer les canaux d’impression et web d’un document. Vous pouvez faire glisser des composants dans la communication interactive afin d’ajouter des éléments, puis configurer les éléments ajoutés conformément aux exigences. Le tableau ci-dessous décrit les composants répertoriés dans l’explorateur de composants pour les canaux d’impression et web :

| **Composant** | **Canal d’impression** | **Canal web** | **Fonctionnalité** |
|---|---|---|---|
| Graphique | ✓ | ✓ | Ajoute un graphique que vous pouvez utiliser dans une communication interactive pour la représentation visuelle des données bidimensionnelles issues d’un élément de collection du modèle de données de formulaire. |
| Fragment de document | ✓ | ✓ | Vous permet d’ajouter un composant réutilisable, du texte, une liste ou une condition à une communication interactive. Le composant réutilisable que vous ajoutez à une communication interactive peut être basé sur modèle de données de formulaire ou sans modèle de données de formulaire. |
| Image | ✓ | ✓ | Permet d’insérer une image. |
| Panneau | - | ✓ | Le composant Panneau est un espace réservé pour regrouper d’autres composants et contrôle la disposition d’un groupe de composants dans une communication interactive. Un composant de panneau vous donne également la possibilité de permettre la répétition d’un groupe de composants pour l’utilisateur ou l’utilisatrice, par exemple dans plusieurs entrées requises pour remplir des informations d’identification pédagogiques. Il est également recommandé d’utiliser un panneau pour chaque onglet d’une communication interactive dotée de plusieurs onglets. |
| Tableau | &#42; | ✓ | Ajoute un tableau qui permet de classer les données par lignes et par colonnes. |
| Zone cible | &#42;&#42; | ✓ | Insère une zone cible dans un canal web pour organiser les composants spécifiques au canal web. |
| Texte | - | ✓ | Ajoute le texte au canal web d’une communication interactive. Le texte peut utiliser des objets de modèle de données de formulaire pour rendre le contenu dynamique. |

&#42; Utilisez les fragments de mise en page dans le canal d’impression pour ajouter des tableaux.

&#42;&#42; Dans le canal d’impression, les zones cibles sont prédéfinies dans le XDP/modèle d’impression. Vous ne pouvez pas ajouter de nouvelles zones cibles à l’aide de l’interface utilisateur de création de communication interactive.

* **Explorateur de sources de données** L’explorateur de sources de données affiche les sources de données disponibles dans le modèle de données de formulaire que vous avez sélectionné lors de la création de la communication interactive.

### Points clés pour l’utilisation de composants {#key-points-for-working-with-components}

Les points clés lorsque vous utilisez des composants de communication interactive sont les suivants :

* Chaque composant est associé à des propriétés qui contrôlent son apparence et ses fonctionnalités. Pour configurer les propriétés d’un composant, sélectionnez celui-ci et sélectionnez ![cmppr](assets/cmppr.png) pour ouvrir les propriétés du composant dans l’explorateur de propriétés.
* Un composant est identifié par son nom d’élément. Lorsque vous sélectionnez ![cmppr](assets/cmppr.png), vous pouvez changer le nom du composant en modifiant la valeur du champ Nom de l’élément dans l’explorateur de propriétés. Vous pouvez saisir uniquement des lettres, des chiffres, des traits d’union (-) et des traits de soulignement (_) dans le champ Nom de l’élément. D’autres caractères spéciaux ne sont pas autorisés et le nom de l’élément doit commencer par une lettre.
* Vous pouvez modifier la propriété de titre d’un composant de communication interactive en ligne dans l’éditeur sans ouvrir l’explorateur de propriétés tant que le titre est visible sur la communication interactive. Pour ce faire :

   1. Sélectionnez un composant qui a une propriété Titre et dont la propriété Masquer le titre est désactivée.
   1. Sélectionnez ![aem_6_3_edit](assets/aem_6_3_edit.png) pour rendre le titre modifiable.

   1. Modifiez le titre et sélectionnez la touche Retour ou sélectionnez un emplacement en dehors du composant pour enregistrer les modifications. Sélectionnez la touche Échap pour annuler les modifications.

## Barre d’outils de composants {#component-toolbar}

![Libellés de la barre d’outils des composants](do-not-localize/component_toolbar_labels_new.png)

Lorsque vous sélectionnez un composant, une barre d’outils s’affiche, vous permettant de l’utiliser. Vous avez la possibilité de couper, coller, déplacer et spécifier les propriétés des composants. Vous avez le choix entre :

A.**Configurer** : lorsque vous sélectionnez **Configurer**, les propriétés du composant s’affichent dans la barre latérale.

B.**Modifier les règles** : lorsque vous sélectionnez Modifier les règles, l’éditeur de règles apparaît dans lequel vous pouvez modifier et créer des règles pour le composant sélectionné. Dans l’éditeur de règles, vous pouvez également sélectionner d’autres objets de formulaire (composants) et modifier/créer des règles pour ces objets de formulaire.

C.** Copier** : permet de copier un composant et le coller ailleurs dans la communication interactive.

D.**Couper** : permet de déplacer un composant d’un endroit à un autre dans la communication interactive.

E. **Supprimer** : permet de supprimer le composant de la communication interactive.

F. **Insérer le composant** : permet d’insérer un composant au-dessus du composant sélectionné.

G. **Coller** : permet de coller le composant coupé ou copié à l’aide des options décrites ci-dessus.

H. **Groupe** : permet de sélectionner plusieurs composants permettant de couper, copier ou coller plusieurs composants ensemble.

I. **Parent** : permet de sélectionner le parent d’un composant.

J. **Afficher l’expression SOM :** permet d’afficher lʼ[expression SOM](../../forms/using/using-som-expressions-adaptive-forms.md) du composant.

K. **Regrouper les objets dans le panneau :** permet de regrouper les composants dans un panneau afin de pouvoir effectuer des opérations sur ces composants de manière simultanée. Pour plus d’informations, consultez la section [Regrouper les objets dans le panneau](create-interactive-communication.md#groupobjectspanel).

L. **Ajouter un panneau enfant** (pour les panneaux uniquement) : permet d’ajouter un panneau enfant au panneau.

M. **Ajouter une barre d’outils de panneau** (pour les panneaux uniquement) : permet d’ajouter la barre dʼoutils du composant Panneau. Vous pouvez ensuite effectuer d’autres actions sur la barre d’outils.

En outre, lʼoption **Remplacer** de la barre d’outils vous permet de remplacer le composant existant par un autre. L’option n’est pas disponible pour le composant Panneau.

## Barre d’outils Page {#page-toolbar}

La barre d’outils de la page, située en haut de l’écran, propose des options permettant de prévisualiser la communication interactive et d’en modifier les propriétés. Vous pouvez prévisualiser la communication interactive lors de sa création et apporter des modifications en conséquence. Dans la barre d’outils de la page, vous voyez :

* Activer/désactiver le panneau latéral![ toggle-side-panel](assets/toggle-side-panel.png) : affiche ou masque la barre latérale.
* Informations sur la page ![pageinformationad](assets/pageinformationad.png): vous permet d’afficher les propriétés de la page.
* Émulateur ![règle](assets/ruler.png): vous permet de simuler l’aspect de votre communication interactive pour différentes tailles d’affichage telles que des tablettes et des téléphones.
* Modifier : permet de sélectionner d’autres modes comme : Modifier, Style, Développeur et Conception.

   * Modifier : modifie les propriétés de la communication interactive et de ses composants. Exemple : l’ajout d’un composant, le dépôt d’une image et l’indication des champs obligatoires.
   * Style : définit l’aspect des composants de votre communication interactive. Par exemple, en mode Style, vous pouvez sélectionner un panneau et définir sa couleur d’arrière-plan.
   * Développeur : permet à un développeur de :

      * Découvrir en quoi consiste la communication interactive.
      * Déboguer en temps réel afin de mieux résoudre les problèmes.

   * Cible : permet d’activer ou de désactiver les composants personnalisés ou les composants prêts à l’emploi qui ne sont pas répertoriés dans la barre latérale.

* Aperçu : permet de prévisualiser la communication interactive avant de le publier.
