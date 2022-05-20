---
title: 'Application d’un style à votre formulaire adaptatif '
seo-title: Style your adaptive form
description: 'Apprenez à créer un thème personnalisé, à appliquer un style à des composants individuels et à utiliser les polices web dans un thème. '
seo-description: Learn to create a custom theme, style individual components, and use web fonts in a theme
page-status-flag: de-activated
uuid: ffb2cc22-baaf-4525-a2e3-29f39271c670
topic-tags: introduction
discoiquuid: 655303a4-99bb-4ba3-9d50-a178f5edcf85
feature: Adaptive Forms
exl-id: 7742c3ca-1755-44c5-b70f-61309f09d1b8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '2037'
ht-degree: 100%

---

# Application d’un style à votre formulaire adaptatif {#do-not-publish-style-your-adaptive-form}

Apprenez à créer un thème personnalisé, à appliquer un style à des composants individuels et à utiliser les polices web dans un thème.

![](do-not-localize/08-style_your_adaptiveformmain.png)

Ce didacticiel est une étape de la série [Création de votre premier formulaire adaptatif](https://helpx.adobe.com/fr/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html). Il est recommandé de suivre la série dans l’ordre chronologique pour comprendre, exécuter et démontrer le cas d’utilisation complet du didacticiel.

## À propos du didacticiel  {#about-the-tutorial}

Vous pouvez utiliser des thèmes pour donner une apparence et un style uniques à un formulaire adaptatif. Vous pouvez appliquer des thèmes prêts à l’emploi fournis avec l’éditeur de formulaires adaptatifs ou créer vos propres thèmes. AEM [!DNL Forms] fournit un [éditeur de thème](https://helpx.adobe.com/fr/experience-manager/6-3/forms/using/themes.html) pour créer des thèmes personnalisés. Un seul thème peut conférer une apparence différente au même formulaire adaptatif ouvert sur un mobile, une tablette ou un ordinateur de bureau. Aucune connaissance préalable de CSS ou de LESS n’est nécessaire pour utiliser l’éditeur de thèmes, mais cela est préférable.

À la fin du didacticiel, vous découvrirez comment :

* Appliquer un thème prêt à l’emploi à un formulaire adaptatif
* Créer un thème pour formulaire adaptatif à l’aide de l’éditeur de thème
* Style des composants individuels
* Section bonus : utilisation des polices web dans un thème personnalisé

Lorsque vous aurez terminé le didacticiel, le modèle de données de formulaire se présentera comme ceci :

![Formulaire avec un thème personnalisé](assets/styled-adaptive-form.png)

## Avant de commencer {#before-you-start}

Téléchargez sur votre ordinateur local les images de style d’en-tête et de logo présentées ci-dessous. L’en-tête du formulaire adaptatif `shipping-address-add-update-form` utilise les images de style d’en-tête et de logo. L’image de style d’en-tête s’affiche à droite de l’en-tête.

[Obtenir le fichier](assets/header-style.png)

[Obtenir le fichier](assets/logo-1.png)

## Étape 1 : appliquer un thème à votre formulaire adaptatif {#step-apply-a-theme-to-your-adaptive-form}

L’éditeur de formulaires adaptatifs fournit plusieurs thèmes prêts à l’emploi. Si vous envisagez de ne pas utiliser de style personnalisé pour votre formulaire adaptatif, vous pouvez également publier vos formulaires adaptatifs avec un thème prêt à l’emploi. Les thèmes sont indépendants des formulaires adaptatifs. Vous pouvez appliquer le même thème à plusieurs formulaires adaptatifs. Pour appliquer un thème à un formulaire adaptatif :

1. Ouvrez le formulaire adaptatif pour le modifier.

   [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)

1. Ouvrez les propriétés du **[!UICONTROL conteneur de formulaires adaptatifs]**. Dans le navigateur de propriétés, accédez à **[!UICONTROL De base]** > **[!UICONTROL Thème de formulaire adaptatif]**. Le champ **[!UICONTROL Thème de formulaire adaptatif]** répertorie tous les thèmes prêts à l’emploi et personnalisés. Par défaut, le thème Zone de travail est appliqué.
1. Sélectionnez votre thème dans le champ **[!UICONTROL Thème de formulaire adaptatif]**. Par exemple, **Thème Enquête**. Cliquez sur ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) pour appliquer le thème sélectionné.

   ![Formulaire adaptatif avec le thème par défaut](assets/default-adaptive-form.png)

   **Illustration :** *formulaire adaptatif avec le thème par défaut*.

   ![Formulaire adaptatif avec le thème Enquête](assets/adaptive-form-with-survey-theme.png)

   **Illustration :** *formulaire adaptatif avec le thème Enquête*.

## Étape 2 : mettre à jour votre formulaire adaptatif {#step-update-your-adaptive-form}

La conception présentée ci-dessus nécessite des modifications du texte et du logo de l’espace réservé de votre formulaire adaptatif existant. Effectuez les étapes suivantes pour faire les changements nécessaires :

1. Modifiez le logo existant et le texte de l’en-tête. Pour supprimer le logo :

   1. Ouvrez le formulaire dans l’éditeur de formulaires.

      [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)

   1. Cliquez sur l’image du logo dans le composant d’[!UICONTROL en-tête], puis sur **[!UICONTROL Propriétés]** ![cmppr](assets/cmppr.png). Dans la propriété [!UICONTROL image], appuyez sur X pour supprimer l’image du logo existant.
   1. Cliquez sur **[!UICONTROL charger]**, sélectionnez le fichier logo.png, puis cliquez sur ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) pour enregistrer les modifications. L’image a été téléchargée dans la section [Avant de commencer](/help/forms/using/style-your-adaptive-form.md#before-you-start).
   1. Cliquez sur le texte de l’en-tête, `We.Retail`, puis sur ![aem_6_3_edit](assets/aem_6_3_edit.png) **[!UICONTROL modifier]**. Modifiez le texte de l’en-tête par `we retail`. Appliquez le format Gras uniquement à `we` dans `we retail`.

      ![we-retail-logo-text](assets/we-retail-logo-text.png)

1. Supprimez le titre et ajouter un texte d’espace réservé :

   1. Cliquez sur le champ identifiant de client et sur Propriétés ![cmppr](assets/cmppr.png).
   1. Copiez le contenu du champ **[!UICONTROL Titre]** dans le champ **[!UICONTROL Texte d’espace réservé]**.
   1. Supprimez le contenu du champ **[!UICONTROL Titre]** et cliquez sur ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).
   1. Répétez les trois étapes précédentes pour toutes les zones de texte, la zone numérique et le champ d’adresse électronique du formulaire.

      ![updated-adaptive-form](assets/updated-adaptive-form.png)

## Étape 3 : créer un thème personnalisé pour votre formulaire adaptatif {#step-create-a-custom-theme-for-your-adaptive-form}

Vous pouvez utiliser un [éditeur de thèmes](/help/forms/using/themes.md) pour créer des thèmes personnalisés. L’éditeur de thèmes est un éditeur WYSIWYG très puissant. Il s’agit d’une méthode visuelle permettant d’appliquer un style CSS à divers composants d’un formulaire adaptatif. Il fournit des commandes plus précises aux composants de style et aux panneaux d’un formulaire adaptatif.

Un thème est une entité distincte au même titre que les formulaires adaptatifs. Il contient des styles (CSS) pour les composants et les panneaux d’un formulaire adaptatif. Ces styles incluent des propriétés CSS telles que les couleurs d’arrière-plan, les couleurs d’état, la transparence, l’alignement et la taille. Lorsque vous appliquez un thème, le style spécifié est appliqué aux composants correspondants d’un formulaire adaptatif.

Dans ce didacticiel, vous allez appliquer un style aux en-têtes et aux pieds de page, aux composants texte et numériques, aux composants de pièces jointes et aux boutons. Commençons par la création d’ un thème :

### Création d’un thème {#create-a-theme}

1. Connectez vous à l’instance de création AEM et accédez à **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Thèmes]**. L’URL par défaut est [http://localhost:4502/aem/forms.html/content/dam/formsanddocuments-themes](http://localhost:4502/aem/forms.html/content/dam/formsanddocuments-themes).
1. Appuyez sur **[!UICONTROL Créer]** et sélectionnez **[!UICONTROL Thème]**. La page [!UICONTROL Créer un thème] s’affiche avec les champs requis pour créer un thème. Les champs **[!UICONTROL Titre]** et **[!UICONTROL Nom]** sont obligatoires :

   * **Titre :** spécifiez le titre du thème. Par exemple, **Thème global.** Le titre vous permet d’identifier le thème dans la liste des thèmes.
   * **Nom :** spécifiez le nom du thème. Par exemple, **Thème-global.** Un nœud portant le nom indiqué est alors créé dans le référentiel. Lorsque vous commencez à saisir un titre, une valeur pour le champ de nom est automatiquement générée. Vous pouvez modifier la valeur suggérée. Le champ de nom peut contenir uniquement des caractères alphanumériques, des traits d’union et des tirets bas. Toutes les entrées non valides sont remplacées par un tiret.

1. Appuyez sur **[!UICONTROL Créer]**. Un thème est créé et une boîte de dialogue pour ouvrir le formulaire à modifier s’affiche. Cliquez sur **[!UICONTROL Ouvrir]** pour ouvrir le thème créé dans un nouvel onglet. Le thème s’ouvre dans l’éditeur de thèmes. Pour le style, l’éditeur de thèmes utilise un formulaire adaptatif prêt à l’emploi fourni avec AEM [!DNL Forms].

   Pour plus d’informations sur l’utilisation de l’interface utilisateur de l’éditeur de thèmes, voir [À propos de l’éditeur de thèmes](/help/forms/using/themes.md#aboutthethemeeditor).

1. Appuyez sur **[!UICONTROL Options du thème]** ![theme-options](assets/theme-options.png) > **[!UICONTROL Configurer]**. Dans le champ **[!UICONTROL Prévisualisation du formulaire]**, sélectionnez le formulaire adaptatif **shipping-address-add-update-form**, cliquez sur ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) et sur **[!UICONTROL Enregistrer]**. L’éditeur de thème est maintenant configuré pour utiliser votre propre formulaire adaptatif au lieu du formulaire adaptatif par défaut. Appuyez sur **[!UICONTROL Annuler]** pour revenir à l’éditeur de thèmes.

   ![custom-theme](assets/custom-theme.png)

   **Illustration :** *éditeur de thèmes avec le formulaire adaptatif shipping-address-add-update-form*.

   ![create-a-theme](assets/create-a-theme.png)

   **Illustration :** *formulaire adaptatif avec le formulaire par défaut*.

### Application d’un style à l’en-tête et au pied de page {#style-header-and-footer}

L’en-tête et le pied de page donnent un aspect cohérent et distinctif à un formulaire adaptatif. En général, l’en-tête contient le logo et le nom de l’organisation, le pied de page contient des informations de copyright. Ces éléments restent identiques dans plusieurs formulaires d’une organisation. Pour appliquer un style à l’en-tête et au pied de page du formulaire adaptatif shipping-address-add-update-form :

1. Accédez à l’option **[!UICONTROL En-tête]** > **[!UICONTROL Texte]** dans le panneau Sélecteurs. Le panneau Sélecteurs se trouve à gauche de l’éditeur de thèmes. Si le panneau n’est pas visible, appuyez sur le panneau latéral Activer/désactiver ![toggle-side-panel](assets/toggle-side-panel.png).

1. Définissez les propriétés suivantes dans l’accordéon **[!UICONTROL Texte]** et cliquez sur ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | Propriété | Valeur |
   |---|---|
   | Famille de polices | Arial |
   | Couleur de la police | FFFFFF |
   | Taille de la police | 54px |

1. Cliquez sur le widget [!UICONTROL d’en-tête], puis sur **[!UICONTROL En-tête]**. Les options permettant d’appliquer un style au widget En-tête s’affichent à gauche. Développez l’accordéon **[!UICONTROL Dimensions et position]**, définissez la **[!UICONTROL Hauteur]** sur `120px`, puis cliquez sur ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).
1. Développez l’accordéon **[!UICONTROL Arrière-plan]** du widget d’en-tête, définissez la **[!UICONTROL couleur d’arrière-plan]** sur `F6921E.`.

   Pointez sur **[!UICONTROL Image et dégradé]** > **[!UICONTROL + Ajouter]** et cliquez sur **[!UICONTROL Image]**. Définissez les propriétés suivantes et cliquez sur ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | Propriété | Valeur |
   |---|---|
   | image | Téléchargez le fichier header-style.png. L’image a été téléchargée dans la section [Avant de commencer](/help/forms/using/style-your-adaptive-form.md#before-you-start). |
   | Position | En bas à droite |
   | Mosaïque | Pas de répétition |

1. Dans l’éditeur de thème, appuyez sur le logo dans l’en-tête puis appuyez sur **[!UICONTROL Logo de l’en-tête]**. Développez l’accordéon Dimensions et position, définissez les propriétés suivantes, puis cliquez sur ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   <table> 
    <tbody> 
     <tr> 
      <td><b>Marge</b></td> 
      <td><b>Valeur</b></td> 
     </tr> 
     <tr> 
      <td>Marge</td> 
      <td> 
       <ul> 
        <li>Haut : 1,5 rem</li> 
        <li>Bas : -35 px</li> 
        <li>Gauche : 1 rem<strong><br /> </strong></li> 
       </ul> <p><strong>Conseil :</strong> appuyez sur l’<img src="assets/link.png">icône de lien pour fournir une valeur différente à chaque champ.<br /> </p> </td> 
     </tr> 
     <tr> 
      <td>Hauteur</td> 
      <td>4,75 rem</td> 
     </tr> 
    </tbody> 
   </table>

1. Appuyez sur le widget de pied de page, puis sur **[!UICONTROL Pied de page]**. Développez l’accordéon **[!UICONTROL Arrière-plan]**, définissez la **[!UICONTROL Couleur d’arrière-plan]** sur `F6921E`, puis cliquez sur ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

### Application d’un style au composant de capture de données et application d’un arrière-plan au formulaire adaptatif {#style-the-data-capture-component-and-apply-a-background-to-the-adaptive-form}

Vous pouvez utiliser plusieurs composants dans un formulaire adaptatif pour capturer des données. Par exemple, zone de texte et zone numérique. Vous pouvez fournir un style identique à tous les composants de capture de données ou un style distinct pour chaque composant. Dans ce didacticiel, un style identique est appliqué aux zones numériques (ID client, Code postal) et aux zones de texte (ID client, Nom, Adresse de livraison, État, Adresse électronique). Pour appliquer un style aux composants de capture de données :

1. Cliquez sur le champ **[!UICONTROL ID de client]** et sur l’option **[!UICONTROL Widget de champ]**. Définissez les propriétés suivantes et cliquez sur ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   <table> 
    <tbody> 
     <tr> 
      <td><b>Accordéon</b></td> 
      <td><b>Propriété</b></td> 
      <td><b>Valeur</b></td> 
     </tr> 
     <tr> 
      <td>Bordure</td> 
      <td>Couleur de la bordure</td> 
      <td>A7A9AC</td> 
     </tr> 
     <tr> 
      <td>Bordure</td> 
      <td>Rayon de bordure </td> 
      <td> 
       <ul> 
        <li>Haut : 7 px<br /> </li> 
        <li>Droite : 7 px<br /> </li> 
        <li>Bas : 7 px<br /> </li> 
        <li>Gauche : 7 px<br /> </li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>Texte</td> 
      <td>Famille de polices</td> 
      <td>Arial</td> 
     </tr> 
     <tr> 
      <td>Texte</td> 
      <td>Couleur de la police</td> 
      <td>939598<br /> </td> 
     </tr> 
     <tr> 
      <td>Texte</td> 
      <td>Taille de la police</td> 
      <td>18px</td> 
     </tr> 
     <tr> 
      <td>Dimensions et position</td> 
      <td>Largeur</td> 
      <td>60%</td> 
     </tr> 
     <tr> 
      <td>Dimensions et position</td> 
      <td>Marge</td> 
      <td> 
       <ul> 
        <li>Gauche : 10 rem</li> 
       </ul> </td> 
     </tr> 
    </tbody> 
    </table>

1. Cliquez sur la zone vide au-dessus du champ **[!UICONTROL ID de client]**, puis sur **[!UICONTROL Conteneur de panneau en responsive design]**. Définissez **[!UICONTROL Arrière-plan]** > **[!UICONTROL Couleur d’arrière-plan]** sur F1F2F2. Cliquez sur ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   ![](do-not-localize/responsive-panel-container.png)

### Application d’un style aux boutons {#style-the-buttons}

Vous pouvez utiliser un thème personnalisé pour appliquer un style identique à tous les boutons du formulaire adaptatif et un [style en ligne](/help/forms/using/inline-style-adaptive-forms.md) pour appliquer un style à un bouton spécifique. Pour appliquer un style aux boutons :

1. Appuyez sur le bouton **[!UICONTROL Envoyer]** et appuyez sur l’option **[!UICONTROL Bouton]**. Définissez les propriétés suivantes et cliquez sur ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   <table> 
    <tbody> 
     <tr> 
      <td><b>Accordéon</b></td> 
      <td><b>Propriété</b></td> 
      <td><b>Valeur</b></td> 
     </tr> 
     <tr> 
      <td>Arrière-plan</td> 
      <td>Couleur d’arrière-plan</td> 
      <td>F6921E</td> 
     </tr> 
     <tr> 
      <td>Bordure<br /> </td> 
      <td>Couleur de la bordure</td> 
      <td>F6921E</td> 
     </tr> 
     <tr> 
      <td>Bordure</td> 
      <td>Rayon de bordure </td> 
      <td> 
       <ul> 
        <li>Haut : 7 px<br /> </li> 
        <li>Droite : 7 px<br /> </li> 
        <li>Bas : 7 px<br /> </li> 
        <li>Gauche : 7 px</li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>Texte<br /> </td> 
      <td>Famille de polices</td> 
      <td>Arial</td> 
     </tr> 
     <tr> 
      <td>Texte</td> 
      <td>Couleur de la police</td> 
      <td>FFFFFF</td> 
     </tr> 
     <tr> 
      <td>Texte</td> 
      <td>Taille de la police</td> 
      <td>18px</td> 
     </tr> 
    </tbody> 
   </table>

1. [Appliquez le thème personnalisé](/help/forms/using/style-your-adaptive-form.md#step-apply-a-theme-to-your-adaptive-form), Thème global, à votre formulaire adaptatif. Si le style ne se reflète pas sur le formulaire adaptatif, videz le cache du navigateur et réessayez.

   ![style-data-capture-components](assets/style-data-capture-components.png)

## Étape 4 : appliquer un style à des composants individuels {#step-style-individual-components}

Certains styles ne s’appliquent qu’à un composant spécifique. Un style est appliqué à ces composants dans l’éditeur de formulaires adaptatifs.

1. Ouvrez le formulaire adaptatif pour le modifier. [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html)
1. Dans la barre supérieure, sélectionnez l’option **[!UICONTROL Style]**.

   ![style-option](assets/style-option.png)

1. Cliquez sur le bouton **[!UICONTROL Joindre]** et sur l’icône ![aem_6_3_edit](assets/aem_6_3_edit.png). Définissez les propriétés suivantes dans l’accordéon **[!UICONTROL Dimensions et position]** :

   | Propriété | Valeur |
   |---|---|
   | Flottant | Gauche |
   | Largeur | 10% |

1. Cliquez sur l’option **[!UICONTROL Preuve d’adresse approuvée par le gouvernement]** et sur l’icône ![aem_6_3_edit](assets/aem_6_3_edit.png). Définissez les propriétés suivantes :

   <table> 
    <tbody> 
     <tr> 
      <td><b>Accordéon</b></td> 
      <td><b>Propriété</b></td> 
      <td><b>Valeur</b></td> 
     </tr> 
     <tr> 
      <td>Dimensions et position</td> 
      <td>Flottant</td> 
      <td>Gauche</td> 
     </tr> 
     <tr> 
      <td>Dimensions et position</td> 
      <td>Largeur</td> 
      <td>73%</td> 
     </tr> 
     <tr> 
      <td>Dimensions et position</td> 
      <td>Remplissage</td> 
      <td> 
       <ul> 
        <li>Gauche : 10 px</li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>Dimensions et position</td> 
      <td>Hauteur</td> 
      <td>40px</td> 
     </tr> 
     <tr> 
      <td>Dimensions et position<br /> </td> 
      <td>Marge</td> 
      <td><br /> 
       <ul> 
        <li>Droite : 2 rem</li> 
        <li>Gauche : 10 rem </li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>Arrière-plan</td> 
      <td>Couleur d’arrière-plan</td> 
      <td>FFFFFF</td> 
     </tr> 
     <tr> 
      <td>Bordure</td> 
      <td>Largeur de bordure</td> 
      <td>1px</td> 
     </tr> 
     <tr> 
      <td>Bordure</td> 
      <td>Style de la bordure</td> 
      <td>Pleine</td> 
     </tr> 
     <tr> 
      <td>Bordure</td> 
      <td>Couleur de la bordure</td> 
      <td>A7A9AC</td> 
     </tr> 
     <tr> 
      <td>Bordure</td> 
      <td>Rayon de bordure</td> 
      <td>7px</td> 
     </tr> 
     <tr> 
      <td>Texte</td> 
      <td>Famille de polices</td> 
      <td>Arial</td> 
     </tr> 
     <tr> 
      <td>Texte</td> 
      <td>Couleur de la police</td> 
      <td>BCBEC0</td> 
     </tr> 
     <tr> 
      <td>Texte</td> 
      <td>Taille de la police</td> 
      <td>18px</td> 
     </tr> 
     <tr> 
      <td>Texte</td> 
      <td>Hauteur de ligne</td> 
      <td>2</td> 
     </tr> 
     </tr> 
    </tbody> 
   </table>

1. Cliquez sur le bouton **[!UICONTROL Envoyer]**, puis sur l’icône ![aem_6_3_edit](assets/aem_6_3_edit.png). Définissez les propriétés suivantes :

   <table> 
    <tbody> 
     <tr> 
      <td><b>Accordéon</b></td> 
      <td><b>Propriété</b></td> 
      <td><b>Valeur</b></td> 
     </tr> 
     <tr> 
      <td>Dimensions et position</td> 
      <td>Flottant</td> 
      <td>Droite</td> 
     </tr> 
     <tr> 
      <td>Dimensions et position</td> 
      <td>Marge</td> 
      <td> 
       <ul> 
        <li>Haut : 5 rem</li> 
        <li>Droite : 14 rem</li> 
        <li>Bas : 20 px</li> 
        <li>Gauche : 20 px<br /> </li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>Arrière-plan</td> 
      <td>Couleur d’arrière-plan</td> 
      <td>F6921E</td> 
     </tr> 
     <tr> 
      <td>Bordure</td> 
      <td>Couleur de la bordure</td> 
      <td>F6921E</td> 
     </tr> 
    </tbody> 
   </table>

   ![styled-adaptive-form-1](assets/styled-adaptive-form-1.png)

## Étape 5 : section bonus : utilisation des polices web dans un thème personnalisé {#step-bonus-section-using-web-fonts-in-a-custom-theme}

Vous pouvez utiliser différentes polices pour concevoir un formulaire adaptatif. Tous les périphériques sur lesquels le formulaire adaptatif est visualisé peuvent ne pas utiliser les polices pour concevoir le formulaire adaptatif. Vous pouvez utiliser un service de polices web pour fournir les polices requises à lʼappareil cible.

[!DNL Adobe Fonts] est un service de polices web. Vous pouvez configurer et utiliser le service avec les formulaires adaptatifs. Pour utiliser [!DNL Adobe Fonts] dans un formulaire adaptatif, procédez comme suit :

>[!NOTE]
>
>![typekit-to-adobe-fonts](assets/typekit-to-adobe-fonts.png) [!DNL Typekit] s’appelle désormais Adobe Fonts et est inclus dans Creative Cloud et dʼautres abonnements. [En savoir plus](https://fonts.adobe.com/).

1. Créez un compte [Adobe Fonts](https://typekit.com/) ainsi quʼun kit, ajoutez la police Myriad Pro à ce dernier, puis publiez le kit et obtenez l’ID de kit. Il est nécessaire d’utiliser [!DNL Adobe Fonts] (polices web) dans un formulaire adaptatif.
1. Dans le serveur AEM [!DNL Forms], accédez à ![adobeexperiencemanager](assets/adobeexperiencemanager.png) **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Outils]** ![marteau](assets/hammer.png) > **[!UICONTROL Adobe Fonts]**. Ouvrez maintenant un dossier de configuration. Si une configuration est déjà disponible, cliquez sur le bouton **[!UICONTROL Créer]** pour créer une instance.

   Dans la boîte de dialogue Créer une configuration, donnez un **titre** à la configuration, puis cliquez sur **[!UICONTROL Créer]**. Vous êtes redirigé sur la page de configuration. Dans la boîte de dialogue [!UICONTROL Modifier le composant] qui s’affiche, indiquez votre **ID de kit**, puis cliquez sur **[!UICONTROL OK]**.

1. Configurez un thème de sorte qu’il utilise la configuration [!DNL Adobe Fonts]. Dans l’instance d’auteur, ouvrez un **[!UICONTROL thème global]** dans l’éditeur de thèmes. Dans l’éditeur de thèmes, cliquez sur **[!UICONTROL Options du thème]** ![theme-options](assets/theme-options.png) > **[!UICONTROL Configurer]**. Dans le champ **[!UICONTROL Configuration d’Adobe Fonts]**, sélectionnez le kit, puiscliquez sur **[!UICONTROL Enregistrer]**.

   Les polices ajoutées à **[!UICONTROL Adobe Fonts]** sont disponibles pour la sélection dans l’accordéon **[!UICONTROL Texte]** de tous les composants.
