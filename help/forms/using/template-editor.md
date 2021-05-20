---
title: Modèles de formulaires adaptatifs
seo-title: Modèles de formulaires adaptatifs
description: Créez des modèles de formulaires adaptatifs en définissant la structure de base et le contenu du formulaire initial à l’aide de l’éditeur de modèle.
seo-description: Créez des modèles de formulaires adaptatifs en définissant la structure de base et le contenu du formulaire initial à l’aide de l’éditeur de modèle.
uuid: 317ca3ab-f809-49a7-a063-9d0c17a35fe4
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: b21a48ba-eccd-4bb5-9b92-3039026ddf2a
docset: aem65
feature: Formulaires adaptatifs
exl-id: d7287ee7-fb4e-4d47-b37e-0a9260344070
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1986'
ht-degree: 97%

---

# Modèles de formulaires adaptatifs{#adaptive-form-templates}

Lorsque vous concevez un formulaire, vous ajoutez des champs et des composants pour définir la structure, le contenu et les actions de formulaire dans l’éditeur. Vous ajoutez des champs et des composants dans le `guideRootPanel` du conteneur de formulaires. Avec l’éditeur de modèles, vous pouvez créer un modèle contenant la structure de base et le contenu initial que les auteurs peuvent utiliser pour créer des formulaires.

Par exemple, vous souhaitez que tous les auteurs de formulaire disposent de certaines zones de texte, de boutons de navigation, ainsi qu’un bouton permettant de soumettre un formulaire d’inscription. Vous pouvez créer un modèle avec les composants que les auteurs peuvent utiliser pour créer un formulaire qui soit cohérent avec d’autres formulaires d’inscription. Lorsque les auteurs utilisent le modèle pour créer un formulaire adaptatif, le nouveau formulaire hérite de la structure et des composants que vous avez spécifiés dans le modèle. L’éditeur de modèles permet d’effectuer les opérations suivantes :

* Ajout de composants d’en-tête et de pied de page d’un formulaire dans le calque de structure.
* Fournissez le contenu initial pour le formulaire.
* Spécifiez un thème, des actions d’envoi.

## Utilisation de modèles {#working-with-templates}

Vous pouvez accéder à l’éditeur de modèles à partir du menu Outils en accédant à **Adobe Experience Manager> Outils> Modèles**. Ici, les modèles sont organisés dans des dossiers activés pour les modèles modifiables. AEM fournit un dossier global pour organiser les modèles. Cependant, il n’est pas activé par défaut. Vous pouvez demander à votre administrateur d’activer le dossier global ou de créer un nouveau dossier pour les modèles. Pour plus d’informations sur la création de dossiers, voir [Dossiers de modèles](/help/sites-developing/page-templates-editable.md).

Une fois que vous avez appuyé pour ouvrir un dossier, vous trouverez un bouton Créer qui permet de créer un modèle pour les formulaires adaptatifs.

### Création d’un modèle {#create-template}

Après avoir créé un dossier, ouvrez-le et suivez les étapes ci-après pour créer un modèle :

1. Dans la console Modèle, appuyez sur **Créer** à l’intérieur du dossier que vous avez créé.
1. Dans la section Choisir un type de modèle, sélectionnez **Modèle de formulaire adaptatif** et appuyez sur **Suivant**.

1. Dans la section Détails du modèle, indiquez un titre de modèle, puis appuyez sur **Créer**.
Vous pouvez indiquer une description et une miniature que vous pouvez afficher lorsque vous pouvez sélectionner le modèle créé au moment de la création de formulaire.

1. Appuyez sur **Terminé** pour revenir à la console, ou appuyez sur **Ouvrir** pour ouvrir le modèle dans l’éditeur.

### Interface utilisateur de l’éditeur de modèles {#template-editor-ui}

Lorsque vous ouvrez un modèle à des fins d’édition, vous pouvez voir les composants suivants de l’Éditeur AEM :

* **Barre d’outils de la page**
Contient les options suivantes :

   * **Activer/désactiver le panneau latéral** : permet d’afficher ou de masquer la barre latérale.
   * **Informations sur la page** : permet de spécifier des informations telles que l’heure de publication, les vignettes, les bibliothèques côté client, la stratégie de page et la bibliothèque côté client de conceptions de pages.
   * **Émulateur** : permet de simuler et de personnaliser l’aspect des différents dispositifs.
   * **Sélecteur de calques :** permet de modifier le calque.
Vous pouvez choisir le calque **Structure** ou le calque **Contenu initial**. Le calque Structure vous permet d’ajouter et de personnaliser l’en-tête et le pied de page. Le calque Contenu initial vous permet de personnaliser le contenu du formulaire.

   * **Aperçu** : permet de prévisualiser le modèle avant de le publier. Vous pouvez utiliser le sélecteur de calques et l’aperçu pour activer/désactiver les modes de modification et d’aperçu.

* **Barre latérale** : fournit les navigateurs de contenu, de propriétés, de ressources et de composants.
* **Barre d’outils de composant** : quand vous choisissez un composant, vous voyez une barre d’outils qui vous permet de personnaliser le composant.
* **Page** : la zone dans laquelle vous ajoutez le contenu pour créer le modèle.

Voir [Présentation de la création de formulaires adaptatifs](../../forms/using/introduction-forms-authoring.md) pour découvrir l’éditeur d’interface utilisateur tactile.

### Modification d’un modèle {#editing-a-template}

Un modèle de formulaire adaptatif est créé à l’aide de deux calques :

* Structure
* Contenu initial

Le sélecteur de calque est disponible en regard de l’option Aperçu dans le coin supérieur droit de l’écran.

### Structure {#structure}

Lorsque vous sélectionnez le calque de structure dans l’éditeur de modèles, vous pouvez voir les conteneurs de dispositions au-dessus et au-dessous du conteneur de formulaires adaptatifs. Les auteurs peuvent utiliser ces conteneurs de dispositions pour l’en-tête et le pied de page. Vous pouvez ajouter, modifier ou personnaliser l’en-tête et le pied de page. Faites glisser et déposez le composant d’en-tête de formulaire adaptatif dans le conteneur de dispositions au-dessus du conteneur de formulaires adaptatifs pour personnaliser l’en-tête de modèle. Faites glisser et déposez le composant de pied de page de formulaire adaptatif dans le conteneur de dispositions au-dessous du conteneur de formulaires adaptatifs pour personnaliser le pied de page de modèle.

![Conteneur de dispositions dans le calque de structure](assets/header-layer-selector.png)

Conteneurs de dispositions dans le calque de structure

**A.** Conteneur de dispositions pour le composant En-tête **B.** Conteneur de dispositions pour le composant Pied de page

Faites glisser et déposez le composant d’en-tête de formulaire adaptatif dans le conteneur de dispositions au-dessus du conteneur de formulaires adaptatifs. Une fois que vous avez ajouté le composant, vous pouvez spécifier les propriétés qui vous permettent d’ajouter un logo et d’indiquer un titre.

De même, lorsque vous faites glisser et déposez le composant de pied de page dans le conteneur de dispositions au-dessous du conteneur de formulaires adaptatifs, vous pouvez fournir les informations de copyright et les détails de l’entreprise.

![En-tête et pied de page ajoutés dans le calque de structure](assets/header-and-footer.png)

En-tête et pied de page ajoutés dans le calque de structure

#### Verrouillage/déverrouillage des composants dans le calque de structure {#locking-unlocking-components-in-the-structure-layer}

Lorsque vous modifiez le modèle avec le calque de structure sélectionné, vous pouvez déverrouiller l’en-tête et le pied de page du modèle. Si un composant est déverrouillé dans le modèle, les auteurs du formulaire peuvent modifier le composant dans le formulaire adaptatif qui utilise le modèle. Le verrouillage d’un composant empêche les auteurs du formulaire de le modifier dans le formulaire adaptatif. L’option de verrouillage est disponible dans la barre d’outils des composants.

Par exemple, vous pouvez ajouter le composant d’en-tête dans le modèle. Lorsque vous sélectionnez le composant, vous pouvez voir une option de verrouillage dans la barre d’outils de composant. En règle générale, l’en-tête comprend le nom et le logo de la société, et vous ne souhaitez pas que les auteurs du formulaire modifient ces informations dans un modèle. Dans un formulaire adaptatif créé à l’aide du modèle avec le composant d’en-tête verrouillé, les auteurs du formulaire ne peuvent pas changer le logo ni le nom de la société.

>[!NOTE]
>
>Le verrouillage ou déverrouillage de l’image ou du logo dans le composant d’en-tête, de manière individuelle, n’est pas recommandé. Vous pouvez déverrouiller le composant d’en-tête.

### Contenu initial {#initial-content}

Lorsque l’option Contenu initial est sélectionnée, le conteneur de formulaires adaptatifs du modèle s’affiche comme un formulaire adaptatif à des fins de modification. Comme lors de la création d’un formulaire adaptatif, vous pouvez spécifier des paramètres initiaux, par exemple en sélectionnant un thème et des actions d’envoi.

Les auteurs de formulaires l’utilisent comme base pour créer un formulaire. La structure de flux de contenu est spécifiée dans le calque Contenu initial du modèle. Pour passer à la modification du contenu initial du modèle de formulaire, avant Aperçu dans la barre d’outils de la page, appuyez sur ![canvas-drop-down](assets/canvas-drop-down.png) **> Contenu initial**.
![Calque Contenu initial dans l’éditeur de modèles](assets/initial-content-layer.png)

Calque Contenu initial dans l’éditeur de modèles affichant le conteneur de formulaires adaptatifs sélectionné pour la spécification des propriétés.

![contenu initial](assets/initial-content-layer-1.png)

Dans le calque Contenu initial, vous créez le modèle de formulaire adaptatif que les auteurs utilisent en tant que base. La création d’un modèle est semblable à la création d’un formulaire : vous utilisez les options disponibles dans la barre latérale. Celle-ci fournit les navigateurs de contenu, de propriétés, de ressources et de composants.

Voir [Barre latérale](../../forms/using/introduction-forms-authoring.md#sidebar).

>[!NOTE]
>
>Lorsque vous sélectionnez le stockage de contenu ou StorePDF en tant qu’action Envoyer, vous obtenez une option permettant de spécifier le chemin de stockage. Si vous spécifiez le chemin dans le modèle, tous les formulaires créés à partir de ce modèle ont le même chemin d’accès. Vous pouvez spécifier le chemin de stockage correct. Vous pouvez également veiller à ce que les auteurs de formulaires le mettent à jour pour empêcher que les données de chaque formulaire soient stockées au même emplacement.

#### Création d’un modèle de formulaire adaptatif avec des onglets et des panneaux   {#creating-an-adaptive-form-template-with-tabs-and-panels-nbsp}

Par exemple, si vous souhaitez créer un modèle avec les onglets suivants :

* Informations générales
* Informations professionnelle

Vous avez ajouté un logo, fourni un titre et ajouté un pied de page dans le calque de structure. Verrouillez l’en-tête et le pied de page pour empêcher les auteurs de formulaires de les modifier lorsqu’ils utilisent le modèle pour créer des formulaires.

Modifiez le type Structure en type Contenu initial pour le calque et commencez à ajouter du contenu au formulaire. Pour créer une structure à onglets, ajoutez un panneau enfant dans le guideRootPanel du conteneur de formulaires adaptatifs. Pour ajouter un panneau :

* Vous pouvez ajouter un panneau en appuyant sur le bouton **+** lorsque vous sélectionnez l’option **Faire glisser les composants ici.**

* Vous pouvez faire glisser le composant de panneau depuis le navigateur de composants et le déposer dans la barre latérale.
* Vous pouvez ajouter un panneau enfant du `guideRootPanel` depuis la barre d’outils de composant.

Pour créer les onglets Informations générales et Informations professionnelles, ajoutez deux panneaux au panneau enfant du `guideRootPanel`. Sélectionnez les panneaux et tapez sur ![cmppr](assets/cmppr.png) pour ouvrir les propriétés dans la barre latérale. Modifiez les noms d’élément en `general-info` et `professional-info`, et les titres en Informations générales et Informations professionnelle, respectivement. Dans la barre latérale, appuyez sur le contenu pour ouvrir l’explorateur de contenu. Dans l’onglet Objets de formulaire, sélectionnez `guideRootPanel`. Dans l’éditeur, le guideRootPanel est sélectionné. Tapez sur ![cmppr](assets/cmppr.png) dans la barre d’outils de composant pour ouvrir ses propriétés. Dans le champ Disposition de panneau, sélectionnez **Onglets supérieurs** et appuyez sur **Terminé**. La structure de modèle à onglets est appliquée.

#### Ajout de contenu dans les onglets {#adding-content-in-tabs}

![Ajout de champs dans le modèle de formulaire adaptatif](assets/template-edit-initial-content.png)

Une fois que vous avez ajouté les panneaux et que vous les avez structurés sous forme d’onglets, vous pouvez ajouter des champs dans les onglets. Lorsque vous sélectionnez un onglet dans l’éditeur, vous pouvez voir l’option **Faire glisser les composants** ici. Vous pouvez faire glisser et déposer les composants tels que les zones de texte, les éléments de liste et les boutons. Vous pouvez faire glisser les composants depuis le navigateur de composants et les déposer dans la barre latérale.

Chaque composant possède des propriétés qui améliorent la capture et la manipulation des données. Par exemple, vous pouvez activer la propriété **Champ obligatoire** d’un composant. Les auteurs peuvent définir un message que vos clients voient lorsqu’ils omettent de remplir un champ obligatoire. Spécifiez le message dans la propriété **Message de champ obligatoire**.

Dans l’exemple de modèle, les champs Nom, Numéro de téléphone et Date de naissance sont ajoutés dans l’onglet Informations générales. Dans l’onglet Informations professionnelles, les champs Employé actuellement, de type d’emploi et Formation ont été ajoutés.

Après avoir ajouté des champs, vous pouvez ajouter des boutons tels qu’Envoyer et Réinitialiser.

### Activation du modèle  {#enabling-the-template}

Lorsque vous créez un modèle, il est ajouté en tant que brouillon. Activez le modèle afin de l’utiliser pour créer des formulaires adaptatifs. Pour activer un formulaire :

1. Accédez à **Adobe Experience Manager > Outils > Modèles**, et ouvrez le dossier dans lequel vous avez créé le modèle.

1. Le modèle que vous avez créé est marqué comme Brouillon.
1. Sélectionnez le modèle, puis appuyez sur **Activer** dans la barre d’outils.
Lorsque vous créez un formulaire adaptatif, vous pouvez voir le modèle affiché lorsque vous êtes invité à choisir un modèle.

## Importation ou exportation d’un modèle {#importing-or-exporting-a-template}

Un formulaire fonctionne avec son modèle. Lorsque vous téléchargez un formulaire adaptatif créé à l’aide d’un modèle personnalisé, celui-ci n’est pas téléchargé. Lorsque vous importez le formulaire dans une autre instance AEM Forms, il est importé sans son modèle. Si le modèle d’un formulaire importé n’est pas disponible, le formulaire n’est pas rendu. Vous pouvez compresser le modèle personnalisé à partir du nœud `/conf` dans `https://<server>:<port>/crx/packmgr` et le transférer dans l’instance AEM Forms dans laquelle vous souhaitez charger le formulaire.

## Création d’un formulaire adaptatif à l’aide du formulaire {#creating-an-adaptive-form-using-the-template}

Une fois que vous avez créé et activé un modèle, il est disponible dans Form Manager lorsque vous créez un formulaire adaptatif. Pour utiliser un modèle et créer un formulaire adaptatif, voir [Création d’un formulaire adaptatif](../../forms/using/creating-adaptive-form.md).

## Modifier l’option d’affichage des modèles prêts à l’emploi  {#change-display-option-of-out-of-the-box-templates}

Vous pouvez créer des modèles personnalisés pour les formulaires adaptatifs afin de définir une structure de base et du contenu initial. AEM Forms fournit également un jeu de modèles prêts à l’emploi pour les formulaires adaptatifs. Vous pouvez afficher ou masquer les modèles.

Effectuez les étapes suivantes pour afficher et masquer les modèles :

1. Connectez-vous l’instance d’auteur AEM Forms et accédez à **Outils** > **Opérations** > **Console web**.

   >[!NOTE]
   >
   >L’URL de la console web d’AEM est https://&#39;[server]:[port]&#39;/system/console/configMgr

1. Recherchez et ouvrez les paramètres **FormsManagerConfiguration** :

   * Pour afficher ou masquer le modèle de formulaires adaptatifs, activez ou désactivez l’option **Inclure les modèles de formulaires et documents adaptatifs prêts à l’emploi**.
   * Pour afficher ou masquer les modèles de formulaires adaptatifs prêts à l’emploi qui ont été ajoutés dans les versions AEM 6.0 Forms ou AEM 6.1 Forms mais sont maintenant obsolètes, activez ou désactivez l’option **Inclure les modèles de formulaires adaptatifs AEM 6.0**. Si cette option est cochée, afin qu’elle prenne effet, il est nécessaire d’activer la configuration **Inclure les modèles de formulaires et documents adaptatifs prêts à l’emploi**.

1. Cliquez sur **Enregistrer**. Les options d’affichage des modèles prêts à l’emploi ont été modifiées.

## Recommandations {#recommendations}

* Lorsque vous modifiez les propriétés du formulaire dans l’éditeur de modèles, n’utilisez pas la propriété BindReference.
* Si vous souhaitez ajouter un point d’arrêt, créez-le lorsque vous rédigez un modèle de formulaire adaptatif.
Pour plus d’informations sur les points d’arrêt, voir [Mise en forme réactive](/help/sites-authoring/responsive-layout.md).
