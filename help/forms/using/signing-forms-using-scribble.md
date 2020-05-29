---
title: Application de signatures électroniques à un formulaire à l’aide de signatures tactiles
seo-title: Application de signatures électroniques à un formulaire à l’aide de signatures tactiles
description: Signature de formulaires à l’aide de la saisie tactile
seo-description: Signature de formulaires à l’aide de la saisie tactile
uuid: ffeba886-9b24-4ed1-95c0-e19356ff2f23
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 76d178d1-8e40-41b3-80d4-66b2f8d04211
docset: aem65
translation-type: tm+mt
source-git-commit: 68ea2335a8466c3c23b766efb1a04b6a38d7f670
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 83%

---


# Application de signatures électroniques à un formulaire à l’aide de signatures tactiles{#apply-electronic-signatures-to-a-form-using-deprecated-scribble-signatures}

Vous pouvez utiliser le composant **Signature tactile** et le composant **Étape de signature** pour tracer la signature (saisie tactile) sur un formulaire adaptatif. Le composant Étape de signature affiche une version PDF du formulaire adaptatif. Vous avez besoin de l’option Document d’enregistrement activée ou de formulaires adaptatifs basés sur un modèle de formulaire pour utiliser le composant Étape de signature.

Les deux composants présentent une fenêtre, comme illustré ci-dessous, pour signer un formulaire. You can also click the geolocation icon ![aem_6_3_geolocation](assets/aem_6_3_geolocation.png) to add geolocation to the signature.

![Boîte de dialogue de signature tactile](assets/scribble-signature.png)

## Configuration d’un formulaire adaptatif pour utiliser la signature tactile {#configure-an-adaptive-form-to-use-scribble-signature}

1. Créez une option Document d’enregistrement activée ou un formulaire adaptatif basé sur modèle de formulaire. Pour obtenir des informations détaillées, voir [Création d’un formulaire adaptatif](../../forms/using/creating-adaptive-form.md).
1. Drag-and-drop the **Scribble Signature** component from component browser to the adaptive form.
1. Tap the **Configure** ![configure](assets/configure.png) icon. Vous ouvrez ainsi le navigateur de propriétés et affiche les propriétés du composant Signature tactile. Configurez les propriétés du composant Signature tactile.
1. Faites glisser le composant Signature Step de l’explorateur de composants vers le formulaire adaptatif.

   >[!NOTE]
   >
   >Le composant Étape de signature prend toute la largeur disponible pour le formulaire. Il est recommandé de ne pas avoir d’autre composant sur la section contenant le composant Étape de signature.

1. Dans l’explorateur de contenu, appuyez sur **Conteneur de formulaires**, puis appuyez sur l’icône **Configurer**![](/help/forms/using/assets/configure.png). Il ouvre le navigateur de propriétés et affiche les propriétés de conteneur de formulaires adaptatifs. Accédez à **Conteneur de formulaires adaptatifs** > **Signature électronique** et décochez l’option **Activer Adobe Sign**. Appuyez sur l’icône Terminé ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) pour enregistrer les modifications.

   >[!NOTE]
   >
   >Lorsque vous ajoutez un composant Étape de signature à un formulaire adaptatif, l’option Activer Adobe Sign est sélectionnée automatiquement.

1. Tap the **Configure** ![configure](assets/configure.png) icon. Elle ouvre l’explorateur de propriétés et affiche les propriétés Étape de signature. Configurez les propriétés suivantes :

   * **Nom de l’élément** : spécifiez le nom du composant.

   * **Titre :** indiquez le titre unique du composant.
   * **Message du modèle :** indiquez le message à afficher lorsque la signature PDF est chargée. Les services Adobe Sign mettent un certain temps à préparer et charger la signature PDF.
   * **Service de signature :** sélectionnez l’option **Signature tactile**.

   * **Classe CSS** : spécifiez la classe CSS de la bibliothèque client, le cas échéant. Il est recommandé d’utiliser des [thèmes](../../forms/using/themes.md) et des [styles en ligne](../../forms/using/inline-style-adaptive-forms.md) au lieu de la classe CSS.
   Appuyez sur l’icône Terminé ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) pour enregistrer les modifications. La signature est configurée correctement.

   Désormais, lorsque vous remplissez un formulaire, une version PDF du formulaire adaptatif est affichée et les options pour signer le document PDF sont fournies. Pour plus d’informations, voir [Signature d’un formulaire adaptatif en utilisant la signature tactile](../../forms/using/signing-forms-using-scribble.md#sign-an-adaptive-form-using-scribble-signature).

## Signature d’un formulaire adaptatif en utilisant la signature tactile {#sign-an-adaptive-form-using-scribble-signature}

1. Une fois que vous avez renseigné le formulaire adaptatif et que vous avez atteint la page Étape de signature, l’écran de signature s’affiche.

   ![Écran de signature de la page EchoSign](assets/esignscribblesign.jpg)

1. Cliquez sur **[!UICONTROL Signer]**. La boîte de dialogue de signature tactile apparaît. Sign the form and click the Done ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) icon to save the signature.

   ![Boîte de dialogue de signature tactile](assets/scribblewidget.jpg)

1. Cliquez sur Terminer pour terminer le processus de signature.

   ![Terminer le processus de signature](assets/scribblecomplete.jpg)

Les signatures sont ajoutées au formulaire, et le contrôle de formulaire passe au panneau suivant.

