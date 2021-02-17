---
title: 'Application d’un style à votre formulaire adaptatif '
seo-title: 'Application d’un style à votre formulaire adaptatif '
description: 'Apprenez à créer un thème personnalisé, à appliquer un style à des composants individuels et à utiliser les polices web dans un thème. '
seo-description: 'Apprenez à créer un thème personnalisé, à appliquer un style à des composants individuels et à utiliser les polices web dans un thème. '
page-status-flag: de-activated
uuid: ffb2cc22-baaf-4525-a2e3-29f39271c670
topic-tags: introduction
discoiquuid: 655303a4-99bb-4ba3-9d50-a178f5edcf85
translation-type: tm+mt
source-git-commit: 263a25b70fe4a3e7de65b47f07932d2e5f3d0197
workflow-type: tm+mt
source-wordcount: '2057'
ht-degree: 66%

---


# Application d’un style à votre formulaire adaptatif {#do-not-publish-style-your-adaptive-form}

Apprenez à créer un thème personnalisé, à appliquer un style à des composants individuels et à utiliser les polices web dans un thème.

![](do-not-localize/08-style_your_adaptiveformmain.png)

Ce didacticiel est une étape de la série [Création de votre premier formulaire adaptatif](https://helpx.adobe.com/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html). Il est recommandé de suivre la série dans l’ordre chronologique pour comprendre, exécuter et démontrer le cas d’utilisation complet du didacticiel.

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
1. Sélectionnez votre thème dans le champ **[!UICONTROL Thème de formulaire adaptatif]**. Par exemple, **Thème Enquête**. Appuyez sur ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) pour appliquer le thème sélectionné.

   ![Formulaire adaptatif avec le thème par défaut](assets/default-adaptive-form.png)

   **Figure:formulaire** *adaptatif avec le thème par défaut*

   ![Formulaire adaptatif avec le thème Enquête](assets/adaptive-form-with-survey-theme.png)

   **Figure : formulaire** *adaptatif avec le thème Questionnaire*

## Étape 2 : mettre à jour votre formulaire adaptatif {#step-update-your-adaptive-form}

La conception présentée ci-dessus nécessite des modifications du texte et du logo de l’espace réservé de votre formulaire adaptatif existant. Effectuez les étapes suivantes pour faire les changements nécessaires :

1. Modifiez le logo existant et le texte de l’en-tête. Pour supprimer le logo :

   1. Ouvrez le formulaire dans l’éditeur de formulaires.

      [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)

   1. Appuyez sur l’image du logo dans le composant [!UICONTROL header] et appuyez sur ![cmppr](assets/cmppr.png) **[!UICONTROL properties]**. Dans la propriété [!UICONTROL image], appuyez sur X pour supprimer l’image de logo existante.
   1. Appuyez sur **[!UICONTROL upload]**, sélectionnez logo.png, puis appuyez sur ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) pour enregistrer les modifications. L&#39;image a été téléchargée dans la section [Avant votre début](/help/forms/using/style-your-adaptive-form.md#before-you-start).
   1. Appuyez sur le texte de l’en-tête `We.Retail`, puis sur ![aem_6_3_edit](assets/aem_6_3_edit.png) **[!UICONTROL edit]**. Remplacez le texte de l’en-tête par `we retail`. Applique la mise en forme en gras uniquement à `we`dans `we retail`.

      ![nous-vente-détail-logo-texte](assets/we-retail-logo-text.png)

1. Supprimez le titre et ajouter un texte d’espace réservé :

   1. Appuyez sur le champ ID de client et sur les propriétés ![cmppr](assets/cmppr.png).
   1. Copiez le contenu du champ **[!UICONTROL Titre]** dans le champ **[!UICONTROL Texte d’espace réservé]**.
   1. Supprimez le contenu du champ **[!UICONTROL Titre]** et appuyez sur ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).
   1. Répétez les trois étapes précédentes pour toutes les zones de texte, la zone numérique et le champ d’adresse électronique du formulaire.

      ![update-adaptive-form](assets/updated-adaptive-form.png)

## Étape 3 : créer un thème personnalisé pour votre formulaire adaptatif {#step-create-a-custom-theme-for-your-adaptive-form}

Vous pouvez utiliser un [éditeur de thèmes](/help/forms/using/themes.md) pour créer des thèmes personnalisés. L’éditeur de thèmes est un éditeur WYSIWYG très puissant. Il s’agit d’une méthode visuelle permettant d’appliquer un style CSS à divers composants d’un formulaire adaptatif. Il fournit des commandes plus précises aux composants de style et aux panneaux d’un formulaire adaptatif.

Un thème est une entité distincte au même titre que les formulaires adaptatifs. Il contient des styles (CSS) pour les composants et les panneaux d’un formulaire adaptatif. Ces styles incluent des propriétés CSS telles que les couleurs d’arrière-plan, les couleurs d’état, la transparence, l’alignement et la taille. Lorsque vous appliquez un thème, le style spécifié est appliqué aux composants correspondants d’un formulaire adaptatif.

Dans ce didacticiel, vous allez appliquer un style aux en-têtes et aux pieds de page, aux composants texte et numériques, aux composants de pièces jointes et aux boutons. Commençons par la création d’ un thème :

### Création d’un thème {#create-a-theme}

1. Connectez-vous à l’instance d’auteur AEM et accédez à **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Thèmes]**. L’URL par défaut est [http://localhost:4502/aem/forms.html/content/dam/formsanddocuments-themes](http://localhost:4502/aem/forms.html/content/dam/formsanddocuments-themes).
1. Appuyez sur **[!UICONTROL Créer]** et sélectionnez **[!UICONTROL Thème]**. La page [!UICONTROL Créer un thème] contenant les champs requis pour créer un thème s&#39;affiche. Les champs **[!UICONTROL Titre]** et **[!UICONTROL Nom]** sont obligatoires :

   * **Titre :** indiquez le titre du thème. Par exemple, **Thème global.** Le titre vous permet d’identifier le thème dans la liste des thèmes.
   * **Nom :** indiquez le nom du thème. Par exemple, **Thème-global.** Un nœud portant le nom indiqué est alors créé dans le référentiel. Lorsque vous commencez à saisir un titre, une valeur pour le champ de nom est automatiquement générée. Vous pouvez modifier la valeur suggérée. Le champ de nom peut contenir uniquement des caractères alphanumériques, des traits d’union et des tirets bas. Toutes les entrées non valides sont remplacées par un tiret.

1. Appuyez sur **[!UICONTROL Create]** (Créer). Un thème est créé et une boîte de dialogue pour ouvrir le formulaire à modifier s’affiche. Appuyez sur **[!UICONTROL Ouvrir]** pour ouvrir le thème nouvellement créé dans un nouvel onglet. Le thème s’ouvre dans l’éditeur de thèmes. Pour le style, l’éditeur de thèmes utilise un formulaire adaptatif prêt à l’emploi fourni avec AEM [!DNL Forms].

   Pour plus d’informations sur l’utilisation de l’interface utilisateur de l’éditeur de thème, voir [A propos de l’éditeur de thème](/help/forms/using/themes.md#aboutthethemeeditor).

1. Appuyez sur **[!UICONTROL Options de thème]** ![options de thème](assets/theme-options.png) > **[!UICONTROL Configurer]**. Dans le champ **[!UICONTROL Formulaire de Prévisualisation]**, sélectionnez le **formulaire adaptatif**, appuyez sur ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png), appuyez sur **[!UICONTROL Enregistrer]**. L’éditeur de thème est maintenant configuré pour utiliser votre propre formulaire adaptatif au lieu du formulaire adaptatif par défaut. Appuyez sur **[!UICONTROL Annuler]** pour revenir à l’éditeur de thèmes.

   ![thème personnalisé](assets/custom-theme.png)

   **Figure : éditeur de** *thème avec le formulaire adaptatif expédition-address-add-update-form*

   ![créer un thème](assets/create-a-theme.png)

   **Figure:formulaire** *adaptatif avec le formulaire par défaut*

### Application d’un style à l’en-tête et au pied de page {#style-header-and-footer}

L’en-tête et le pied de page donnent un aspect cohérent et distinctif à un formulaire adaptatif. En général, l’en-tête contient le logo et le nom de l’organisation, le pied de page contient des informations de copyright. Ces éléments restent identiques dans plusieurs formulaires d’une organisation. Pour appliquer un style à l’en-tête et au pied de page du formulaire adaptatif shipping-address-add-update-form :

1. Accédez à l’option **[!UICONTROL En-tête]** > **[!UICONTROL Texte]** dans le panneau Sélecteurs. Le panneau Sélecteurs se trouve à gauche de l’éditeur de thèmes. Si le panneau n’est pas visible, appuyez sur ![bascule-côté-panneau](assets/toggle-side-panel.png) Basculer le panneau latéral.

1. Définissez les propriétés suivantes dans l’accordéon **[!UICONTROL Texte]** et appuyez sur ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | Propriétés | Valeur |
   |---|---|
   | Famille de polices | Arial |
   | Couleur de la police | FFFFFF |
   | Taille de la police | 54px |

1. Appuyez sur le widget [!UICONTROL header] et appuyez sur **[!UICONTROL En-tête]**. Les options permettant d’appliquer un style au widget En-tête s’affichent à gauche. Développez l’accordéon **[!UICONTROL Dimensions et position]**, définissez **[!UICONTROL Hauteur]** sur `120px`, puis appuyez sur ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).
1. Développez l’accordéon **[!UICONTROL Arrière-plan]** du widget d’en-tête, définissez la **[!UICONTROL Couleur d’arrière-plan]** sur `F6921E.`.

   Passez la souris sur **[!UICONTROL Image et dégradé]** > **[!UICONTROL + Ajoute]**, puis appuyez sur **[!UICONTROL Image]**. Définissez les propriétés suivantes et appuyez sur ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | Propriétés | Valeur |
   |---|---|
   | image | Téléchargez le fichier header-style.png. L&#39;image a été téléchargée dans la section [Avant votre début](/help/forms/using/style-your-adaptive-form.md#before-you-start). |
   | Position | En bas à droite |
   | Mosaïque | Pas de répétition |

1. Dans l’éditeur de thème, appuyez sur le logo dans l’en-tête puis appuyez sur **[!UICONTROL Logo de l’en-tête]**. Développez l’accordéon Dimensions &amp; Position, définissez les propriétés suivantes et appuyez sur ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

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

1. Appuyez sur le widget de pied de page, puis sur **[!UICONTROL Pied de page]**. Développez l’accordéon **[!UICONTROL Arrière-plan]**, définissez la **[!UICONTROL Couleur d’arrière-plan]** sur `F6921E`, puis appuyez sur ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

### Application d’un style au composant de capture de données et application d’un arrière-plan au formulaire adaptatif {#style-the-data-capture-component-and-apply-a-background-to-the-adaptive-form}

Vous pouvez utiliser plusieurs composants dans un formulaire adaptatif pour capturer des données. Par exemple, zone de texte et zone numérique. Vous pouvez fournir un style identique à tous les composants de capture de données ou un style distinct pour chaque composant. Dans ce didacticiel, un style identique est appliqué aux zones numériques (ID client, Code postal) et aux zones de texte (ID client, Nom, Adresse de livraison, État, Adresse électronique). Pour mettre en forme les composants de capture de données :

1. Appuyez sur le champ **[!UICONTROL ID de client]** et appuyez sur l’option **[!UICONTROL Widget de champ]**. Définissez les propriétés suivantes et appuyez sur ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   <table> 
    <tbody> 
     <tr> 
      <td><b>Accordéon</b></td> 
      <td><b>Propriétés</b></td> 
      <td><b>Valeur</b></td> 
     </tr> 
     <tr> 
      <td> de la bordure</td> 
      <td>Couleur de la bordure</td> 
      <td>A7A9AC</td> 
     </tr> 
     <tr> 
      <td> de la bordure</td> 
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
      <td>Text (Texte)</td> 
      <td>Famille de polices</td> 
      <td>Arial</td> 
     </tr> 
     <tr> 
      <td>Text (Texte)</td> 
      <td>Couleur de la police</td> 
      <td>939598<br /> </td> 
     </tr> 
     <tr> 
      <td>Text (Texte)</td> 
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

1. Appuyez sur la zone vide située au-dessus du champ **[!UICONTROL ID de client]** et appuyez sur **[!UICONTROL Conteneur de panneau réactif]**. Définissez **[!UICONTROL Arrière-plan]** > **[!UICONTROL Couleur d’arrière-plan]** sur F1F2F2. Appuyez sur ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   ![](do-not-localize/responsive-panel-container.png)

### Application d’un style aux boutons {#style-the-buttons}

Vous pouvez utiliser un thème personnalisé pour appliquer un style identique à tous les boutons du formulaire adaptatif et [le style intégré](/help/forms/using/inline-style-adaptive-forms.md) pour appliquer un style à un bouton spécifique. Pour appliquer un style aux boutons :

1. Appuyez sur le bouton **[!UICONTROL Envoyer]** et appuyez sur l’option **[!UICONTROL Bouton]**. Définissez les propriétés suivantes et appuyez sur ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   <table> 
    <tbody> 
     <tr> 
      <td><b>Accordéon</b></td> 
      <td><b>Propriétés</b></td> 
      <td><b>Valeur</b></td> 
     </tr> 
     <tr> 
      <td>Arrière-plan</td> 
      <td>Couleur d’arrière-plan</td> 
      <td>F6921E</td> 
     </tr> 
     <tr> 
      <td> de la bordure<br /> </td> 
      <td>Couleur de la bordure</td> 
      <td>F6921E</td> 
     </tr> 
     <tr> 
      <td> de la bordure</td> 
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
      <td>Text (Texte)</td> 
      <td>Couleur de la police</td> 
      <td>FFFFFF</td> 
     </tr> 
     <tr> 
      <td>Text (Texte)</td> 
      <td>Taille de la police</td> 
      <td>18 px</td> 
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

1. Appuyez sur le bouton **[!UICONTROL Joindre]** et appuyez sur l’icône ![aem_6_3_edit](assets/aem_6_3_edit.png). Définissez les propriétés suivantes dans les Dimensions **[!UICONTROL et Position]** en accordéon :

   | Propriétés | Valeur |
   |---|---|
   | Flottant | Gauche |
   | Largeur | 10% |

1. Appuyez sur l&#39;option **[!UICONTROL BAT d&#39;adresse approuvé par le gouvernement]** et appuyez sur l&#39;icône ![aem_6_3_edit](assets/aem_6_3_edit.png). Définissez les propriétés suivantes :

   <table> 
    <tbody> 
     <tr> 
      <td><b>Accordéon</b></td> 
      <td><b>Propriétés</b></td> 
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
      <td> de la bordure</td> 
      <td>Largeur de bordure</td> 
      <td>1px</td> 
     </tr> 
     <tr> 
      <td> de la bordure</td> 
      <td>Style de la bordure</td> 
      <td>Pleine</td> 
     </tr> 
     <tr> 
      <td> de la bordure</td> 
      <td>Couleur de la bordure</td> 
      <td>A7A9AC</td> 
     </tr> 
     <tr> 
      <td> de la bordure</td> 
      <td>Rayon de bordure</td> 
      <td>7px</td> 
     </tr> 
     <tr> 
      <td>Text (Texte)</td> 
      <td>Famille de polices</td> 
      <td>Arial</td> 
     </tr> 
     <tr> 
      <td>Text (Texte)</td> 
      <td>Couleur de la police</td> 
      <td>BCBEC0</td> 
     </tr> 
     <tr> 
      <td>Text (Texte)</td> 
      <td>Taille de la police</td> 
      <td>18 px</td> 
     </tr> 
     <tr> 
      <td>Text (Texte)</td> 
      <td>Hauteur de ligne</td> 
      <td>2</td> 
     </tr> 
     </tr> 
    </tbody> 
   </table>

1. Appuyez sur le bouton **[!UICONTROL Envoyer]** et appuyez sur l&#39;icône ![aem_6_3_edit](assets/aem_6_3_edit.png). Définissez les propriétés suivantes :

   <table> 
    <tbody> 
     <tr> 
      <td><b>Accordéon</b></td> 
      <td><b>Propriétés</b></td> 
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
      <td> de la bordure</td> 
      <td>Couleur de la bordure</td> 
      <td>F6921E</td> 
     </tr> 
    </tbody> 
   </table>

   ![styled-adaptive-form-1](assets/styled-adaptive-form-1.png)

## Étape 5 : section bonus : utilisation des polices web dans un thème personnalisé {#step-bonus-section-using-web-fonts-in-a-custom-theme}

Vous pouvez utiliser différentes polices pour concevoir un formulaire adaptatif. Tous les périphériques sur lesquels le formulaire adaptatif est visualisé peuvent ne pas utiliser les polices pour concevoir le formulaire adaptatif. Vous pouvez utiliser un service de polices Web pour fournir les polices requises au périphérique de la cible.

[!DNL Adobe Fonts] est un service de polices web. Vous pouvez configurer et utiliser le service avec les formulaires adaptatifs. Pour utiliser [!DNL Adobe Fonts] dans un formulaire adaptatif :

>[!NOTE]
>
>![typekit-to-adobe-](assets/typekit-to-adobe-fonts.png) [!DNL Typekit] fontsis est désormais appelé Adobe Fonts et est inclus dans le Creative Cloud et les autres abonnements. [En savoir plus](https://fonts.adobe.com/).

1. Créez un compte [Adobe Fonts](https://typekit.com/), créez un kit, ajoutez la police Myriad Pro au kit, publiez le kit et obtenez l’identifiant du kit. Vous devez utiliser [!DNL Adobe Fonts] (polices Web) dans un formulaire adaptatif.
1. Dans le serveur [!DNL Forms] AEM, accédez à ![adobeexperience emanager](assets/adobeexperiencemanager.png) **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Outils]** ![marteau](assets/hammer.png) > **[!UICONTROL Adobe Fonts]**. Ouvrez maintenant un dossier de configuration. Si une configuration est déjà disponible, cliquez sur le bouton **[!UICONTROL Créer]** pour créer une instance.

   Dans la boîte de dialogue Créer une configuration, spécifiez un **Titre** pour la configuration, puis cliquez sur **[!UICONTROL Créer]**. Vous êtes redirigé sur la page de configuration. Dans la boîte de dialogue [!UICONTROL Modifier le composant] qui s&#39;affiche, fournissez votre **ID de kit** et cliquez sur **[!UICONTROL OK]**.

1. Configurez votre thème pour utiliser la configuration [!DNL Adobe Fonts]. Sur l’instance d’auteur, ouvrez **[!UICONTROL Thème global]** dans l’éditeur de thème. Dans l’éditeur de thème, accédez à **[!UICONTROL Options de thème]** ![options de thème](assets/theme-options.png) > **[!UICONTROL Configurer]**. Dans le champ **[!UICONTROL Configuration Adobe Fonts]**, sélectionnez le kit, puis cliquez sur **[!UICONTROL Enregistrer]**.

   Les polices ajoutées à l&#39;**[!UICONTROL Adobe Fonts]** peuvent être sélectionnées dans l&#39;accordéon **[!UICONTROL Texte]** de tous les composants.

