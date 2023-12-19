---
title: '« Didacticiel : créer un formulaire adaptatif »'
description: Apprenez à créer, à mettre en page et à prévisualiser un formulaire adaptatif. Découvrez également comment configurer les actions d’envoi.
feature: Adaptive Forms
exl-id: c0a2adcd-528a-41af-99b5-d8b423cd6605
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '1313'
ht-degree: 85%

---

# Didacticiel : création d’un formulaire adaptatif {#do-not-publish-tutorial-create-an-adaptive-form}

![02-create-adaptive-form-main-image](assets/02-create-adaptive-form-main-image.png)

Ce tutoriel fait partie de la série [Création de votre premier formulaire adaptatif](/help/forms/using/create-your-first-adaptive-form.md). Il est recommandé de suivre la série dans l’ordre chronologique pour comprendre, exécuter et accomplir le cas d’utilisation complet du tutoriel.

## À propos du tutoriel {#about-the-tutorial}

Les formulaires adaptatifs sont des formulaires dynamiques et réactifs de nouvelle génération. Vous pouvez utiliser des formulaires adaptatifs pour offrir des expériences personnalisées. Vous pouvez également intégrer des formulaires adaptatifs à [!DNL Adobe Analytics] à des fins d’utilisation des statistiques et à [!DNL Adobe Campaign] pour la gestion des campagnes. Pour plus d’informations sur les fonctionnalités des formulaires adaptatifs, consultez la section [Présentation de la création de formulaires adaptatifs](/help/forms/using/introduction-forms-authoring.md).

Il est plus facile de créer et de gérer des formulaires en suivant un processus approprié. Dans cet article, vous apprenez à :

* [Créer un formulaire adaptatif permettant à un client d’ajouter une adresse de livraison](/help/forms/using/create-adaptive-form.md#step-create-the-adaptive-form)

* [Disposition des champs d’un formulaire adaptatif pour afficher et accepter les informations d’un client](/help/forms/using/create-adaptive-form.md#step-add-header-and-footer)

* [Créer une action d’envoi pour envoyer un courrier électronique contenant du contenu de formulaire](/help/forms/using/create-adaptive-form.md#step-add-components-to-capture-and-display-information)
* [Prévisualiser et envoyer un formulaire adaptatif](/help/forms/using/create-adaptive-form.md)

À la fin de l’article, vous disposerez d’un formulaire similaire au suivant :\
[![Aperçu du formulaire sur mobile](do-not-localize/form-preview-mobile.gif)](do-not-localize/form-preview-mobile.gif)

## Étape 1 : création du formulaire adaptatif {#step-create-the-adaptive-form}

1. Connectez-vous à l’instance d’auteur AEM et accédez à **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Formulaires]** > **[!UICONTROL Formulaires et documents]**. L’URL par défaut est [http://localhost:4502/aem/forms.html/content/dam/formsanddocuments](http://localhost:4502/aem/forms.html/content/dam/formsanddocuments).
1. Sélectionner **[!UICONTROL Créer]** et sélectionnez **[!UICONTROL Formulaire adaptatif]**. Une option permettant de sélectionner un modèle s’affiche. Sélectionnez la variable **[!UICONTROL Vide]** modèle pour le sélectionner et le sélectionner **[!UICONTROL Suivant]**.

1. L’option **[!UICONTROL Ajouter des propriétés]** s’affiche. Les champs **[!UICONTROL Titre]** et **[!UICONTROL Nom]** sont obligatoires :

   * **Titre :** spécifiez `Add new or update shipping address` dans le champ **[!UICONTROL Titre]**. Le champ Titre spécifie le nom d’affichage du formulaire. Le titre vous permet d’identifier le formulaire dans l’interface utilisateur d’AEM [!DNL Forms].
   * **Nom :** spécifiez `shipping-address-add-update-form` dans le champ **[!UICONTROL Nom]**. Le champ Nom indique le nom du formulaire. Un nœud portant le nom spécifié est créé dans le référentiel. Lorsque vous commencez à saisir un titre, la valeur du champ Nom est automatiquement générée. Vous pouvez modifier la valeur suggérée. Le champ Nom ne peut contenir que des caractères alphanumériques, des traits d’union et des traits de soulignement. Toutes les entrées non valides sont remplacées par un trait d’union.

1. Sélectionnez **[!UICONTROL Créer]**. Un formulaire adaptatif est créé et une boîte de dialogue pour ouvrir le formulaire à modifier s’affiche. Sélectionner **[!UICONTROL Ouvrir]** pour ouvrir le formulaire nouvellement créé dans un nouvel onglet. Le formulaire s’ouvre pour modification. Il affiche également la barre latérale permettant de personnaliser le formulaire nouvellement créé selon vos besoins.

   Pour plus d’informations sur l’interface de création de formulaires adaptatifs et les composants disponibles, consultez [Présentation de la création de formulaires adaptatifs](/help/forms/using/creating-adaptive-form.md).

   ![Un formulaire adaptatif nouvellement créé.](assets/newly-created-adaptive-form.png)

## Étape 2 : ajout d’un en-tête et d’un pied de page {#step-add-header-and-footer}

AEM [!DNL Forms] fournit de nombreux composants pour l’affichage d’informations sur un formulaire adaptatif. Les composants d’en-tête et de pied de page contribuent à une apparence cohérente du formulaire. Un en-tête comprend généralement le logo d’une entreprise, le titre du formulaire et un résumé. Un pied de page contient généralement des informations de copyright, ainsi que des liens vers d’autres pages.

1. Sélectionner ![bouton bascule-côté-panneau](assets/toggle-side-panel.png) > ![treeextenall](assets/treeexpandall.png). L’explorateur de composants s’affiche. Faites glisser et déposez le composant **[!UICONTROL En-tête]** de l’explorateur de composants vers le formulaire adaptatif.
1. Sélectionner **[!UICONTROL Logo]**. La barre d’outils s’affiche. Sélectionner ![aem_6_3_edit](assets/aem_6_3_edit.png) dans la barre d’outils, saisissez **We.Retail**, puis sélectionnez ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

1. Sélectionnez Image. La barre d’outils s’affiche. Sélectionner ![cmppr](assets/cmppr.png). L’explorateur de propriétés s’ouvre sur la partie gauche de l’écran. **[!UICONTROL Recherchez]** et téléchargez l’image du logo. Sélectionner ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png). L’image apparaît dans l’en-tête.

   Si vous n’en avez pas, vous pouvez sélectionner Obtenir un fichier pour télécharger le logo utilisé dans cet article.

[Obtenir le fichier](assets/logo.png)

1. Faites glisser le composant **[!UICONTROL Pied de page]** de ![treeexpandall](assets/treeexpandall.png) vers le formulaire adaptatif. À ce stade, le formulaire a l’apparence suivante :

   ![adaptive-form-with-headers-and-footers](assets/adaptive-form-with-headers-and-footers.png)

## Étape 3 : ajout de composants pour capturer et afficher les informations {#step-add-components-to-capture-and-display-information}

Les composants sont les blocs de construction d’un formulaire adaptatif. AEM [!DNL Forms]fournit de nombreux composants pour la capture et l’affichage d’informations dans un formulaire adaptatif. Vous pouvez faire glisser les composants de ![treeexpandall](assets/treeexpandall.png) vers un formulaire. Pour en savoir plus sur les composants disponibles et les fonctionnalités correspondantes, voir [Présentation de la création de formulaires adaptatifs](/help/forms/using/introduction-forms-authoring.md).

1. Faites glisser le **[!UICONTROL composant de zone numérique]** vers le formulaire adaptatif. Placez-le avant le composant de pied de page. Ouvrez les propriétés du composant, modifiez **[!UICONTROL Titre]** du composant à **`Customer ID`**, modifier **[!UICONTROL Nom de l’élément]** to **`customer_ID`**, activez la variable **[!UICONTROL Champ obligatoire]** , activez l’option **[!UICONTROL Use HTML5 Number Input Type]** et sélectionnez ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).
1. Faites glisser trois composants de la zone de texte vers le formulaire adaptatif. Placez-les avant le pied de page. Définissez les propriétés suivantes pour ces zones de texte. :

   <table> 
    <tbody> 
     <tr> 
      <td><b>Propriété</b></td> 
      <td><b>Zone de texte 1<br/></b></td> 
      <td><b>Zone de texte 2<br/></b></td> 
      <td><b>Zone de texte 3</b></td> 
     </tr> 
     <tr> 
      <td>Titre</td> 
      <td>Nom<br /> </td> 
      <td>Adresse d’expédition</td> 
      <td>État</td> 
     </tr> 
     <tr> 
      <td>Nom de l’élément</td> 
      <td>customer_Name<br /> </td> 
      <td>customer_Shipping_Address</td> 
      <td>customer_State</td> 
     </tr> 
     <tr> 
      <td>Champ obligatoire</td> 
      <td>Activé</td> 
      <td>Activé</td> 
      <td>Activé</td> 
     </tr> 
     <tr> 
      <td>Permettre des lignes multiples<br /> </td> 
      <td>Désactivé</td> 
      <td>Activé</td> 
      <td>Désactivé</td> 
     </tr> 
    </tbody> 
   </table>

1. Faites glisser un composant de **[!UICONTROL Zone numérique]** avant le composant de pied de page. Ouvrez les propriétés du composant, définissez les valeurs répertoriées dans le tableau ci-dessous, puis sélectionnez ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | Propriété | Valeur |
   |---|---|
   | Titre | Code postal |
   | Nom de l’élément | customer_ZIPCode |
   | Nombre maximal de chiffres | 6 |
   | Champ obligatoire | Activé |
   | Type de modèle d’affichage | Aucun modèle |

1. Faites glisser un composant **[!UICONTROL Courrier électronique]** avant le composant de pied de page. Ouvrez les propriétés du composant, définissez les valeurs répertoriées dans le tableau ci-dessous, puis sélectionnez ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | Propriété | Valeur |
   |---|---|
   | Titre | E-mail |
   | Nom de l’élément | customer_Email |
   | Champ obligatoire | Activé |

1. Faites glisser un composant **[!UICONTROL Pièce jointe]** avant le composant de pied de page. Ouvrez les propriétés du composant, définissez les valeurs répertoriées dans le tableau ci-dessous, puis sélectionnez ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   <table> 
    <tbody> 
     <tr> 
      <td><b>Propriété</b></td> 
      <td><b>Valeur</b></td> 
     </tr> 
     <tr> 
      <td>Titre</td> 
      <td>Preuve d’adresse approuvée par le gouvernement<br /> </td> 
     </tr> 
     <tr> 
      <td>Nom de l’élément</td> 
      <td>customer_Address_Proof</td> 
     </tr> 
     <tr> 
      <td>Champ obligatoire</td> 
      <td>Activé</td> 
     </tr> 
    </tbody> 
   </table>

1. Faites glisser un composant **[!UICONTROL Bouton Envoyer]** vers le formulaire adaptatif. Placez-le avant le composant de pied de page. Ouvrez les propriétés du composant, remplacez Nom de l’élément par `address_addition_update_submit`, sélectionnez ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png). La mise en page du formulaire est complète et le formulaire a l’apparence suivante :

   ![adaptive-form-with-all-the-components](assets/adaptive-form-with-all-the-components.png)

## Étape 4 : configuration de l’action d’envoi du formulaire adaptatif {#step-configure-submit-action-for-the-adaptive-form}

Une action d’envoi est déclenchée lorsqu’un utilisateur ou une utilisatrice clique sur le bouton Envoyer d’un formulaire adaptatif. Vous pouvez utiliser une action d’envoi pour enregistrer des données de formulaire dans le référentiel local, envoyer des données de formulaire vers un point d’entrée REST, envoyer des données de formulaire par e-mail, et plus encore. Les formulaires adaptatifs fournissent quelques autres actions d’envoi prêtes à l’emploi. Pour plus de détails, consultez [Configuration de l’action Envoyer](/help/forms/using/configuring-submit-actions.md).

Les étapes suivantes vous permettent de configurer les actions d’envoi dʼe-mail et d’envoi de démonstration du formulaire :

1. Configurez le serveur de courrier électronique. Pour plus d’informations, reportez-vous à la section [Configuration des notifications par courrier électronique](/help/sites-administering/notification.md).


1. Sélectionner **[!UICONTROL Conteneur de formulaires]** dans l’explorateur de contenu et sélectionnez ![cmppr](assets/cmppr.png). L’explorateur de propriétés s’ouvre sur la partie gauche de l’écran.
1. Accédez à **[!UICONTROL Envoi]** > **[!UICONTROL Action d’envoi]**. Sélectionnez **[!UICONTROL Envoyer un courrier électronique]**. Spécifiez les valeurs suivantes et sélectionnez ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | Propriété | Valeur |
   |--- |--- |
   | Origine | `donotreply@weretail.com` |
   | To | `${customer_Email}` |
   | Objet | Accusé de réception : vous avez ajouté l’adresse de livraison sur le site web de We.Retail. |
   | Modèle d’e-mail | Bonjour `${customer_Name}`, l’adresse suivante est ajoutée comme adresse de livraison pour votre compte : <br>`${customer_Name}`, `${customer_Shipping_Address}`, `${customer_State}` et `${customer_ZIPCode}`<br>. Cordialement, We.Retail |
   | Inclure les pièces jointes | Activé |

   Votre formulaire est prêt. Vous pouvez à présent prévisualiser le formulaire et tester la fonctionnalité. Si vous avez utilisé le nom mentionné dans le tutoriel et avez accédé au formulaire sur la machine qui exécute le serveur AEM [!DNL Forms], le formulaire est disponible à l’adresse [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html).

## Étape 5 : prévisualisation et envoi du formulaire adaptatif {#step-preview-and-submit-the-adaptive-form}

Vous pouvez utiliser l’option **[!UICONTROL Aperçu]** pour évaluer l’apparence et le comportement d’un formulaire. Vous pouvez envoyer un formulaire en mode aperçu et vérifier les validations appliquées à un formulaire. Si une erreur s’affiche lorsqu’un champ obligatoire est laissé vide, par exemple.

Les formulaires adaptatifs permettent également d’émuler l’expérience d’un formulaire pour différents appareils. Par exemple, pour iPhone, iPad et appareils de bureau. Vous pouvez utiliser les options **[!UICONTROL Prévisualisation]** et **[!UICONTROL Gestionnaire de]** ![l’émulateur](assets/ruler.png) conjointement pour prévisualiser un formulaire pour les appareils dotés de tailles d’écran différentes.

1. Sélectionnez la variable **[!UICONTROL Aperçu]** sur le côté droit de l’éditeur de formulaire. Le formulaire s’ouvre en mode aperçu. Si vous avez utilisé le nom mentionné dans le didacticiel, l’URL de l’aperçu du formulaire est [http://localhost:4502/content/dam/formsanddocuments/shipping-address-add-update-form/jcr:content?wcmmode=disabled](http://localhost:4502/content/dam/formsanddocuments/shipping-address-addition-updation-form/jcr:content?wcmmode=disabled)
1. Utilisez ![gestionnaire](assets/ruler.png) pour visualiser l’apparence du formulaire sur différents appareils.
1. Renseignez les champs du formulaire et sélectionnez **[!UICONTROL Envoyer]**. Le formulaire est envoyé et vous êtes redirigé(e) vers la **page de remerciement** par défaut. Vous pouvez également spécifier une page de remerciement personnalisée. Pour plus de détails, voir [Configuration de la page de redirection](/help/forms/using/configuring-redirect-page.md).

Le formulaire adaptatif pour l’ajout d’une adresse est prêt. Si vous avez utilisé le nom mentionné dans le tutoriel et avez accédé au formulaire sur la machine qui exécute le serveur AEM Forms, le formulaire est alors disponible à l’adresse [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html).
