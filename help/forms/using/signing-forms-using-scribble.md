---
title: Application de signatures électroniques à un formulaire à l’aide de signatures tactiles
description: Découvrez comment signer AEM Forms adaptatif à l’aide de la signature tactile. Vous pouvez utiliser l’étape signature tactile et signature pour tracer la signature sur un formulaire.
uuid: ffeba886-9b24-4ed1-95c0-e19356ff2f23
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 76d178d1-8e40-41b3-80d4-66b2f8d04211
docset: aem65
feature: Adaptive Forms
exl-id: 096f61b0-59f4-4699-9093-8fb1ed81fded
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 63%

---

# Application de signatures électroniques à un formulaire à l’aide de signatures tactiles{#apply-electronic-signatures-to-a-form-using-deprecated-scribble-signatures}

<span class="preview"> Adobe recommande d’utiliser la capture de données moderne et extensible. [Composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=fr) pour [création d’un Forms adaptatif](/help/forms/using/create-an-adaptive-form-core-components.md) ou [Ajout de Forms adaptatif à des pages AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Ces composants représentent une avancée significative dans la création de Forms adaptatif, ce qui garantit des expériences utilisateur impressionnantes. Cet article décrit l’approche plus ancienne de la création de Forms adaptatif à l’aide de composants de base. </span>


| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Cliquez ici](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-components-to-an-adaptive-form/signing-forms-using-scribble.html) |
| AEM 6.5 | Cet article |


Vous pouvez utiliser le composant **Signature tactile** et le composant **Étape de signature** pour tracer la signature (saisie tactile) sur un formulaire adaptatif. Le composant Étape de signature affiche une version PDF du formulaire adaptatif. Vous avez besoin de l’option Document d’enregistrement activée ou de formulaires adaptatifs basés sur un modèle de formulaire pour utiliser le composant Étape de signature.

![Boîte de dialogue de signature tactile](/help/forms/using/assets/scribble-signature.png)

## Diverses options disponibles dans la fenêtre de signature.

* **A :** cliquez sur l’icône **Pinceau** pour tracer votre signature sur la zone de travail.
* **B :** cliquez sur l’icône **Effacer** pour effacer la signature sur la zone de travail.
* **C :** cliquez sur l’icône **Géolocalisation** pour ajouter une géolocalisation avec la signature.
* **D :** cliquez sur l’icône **Clavier** pour saisir votre nom sur la zone de travail.

Une fois que vous avez sélectionné Terminé![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) dans la fenêtre de signature tactile, vous ne pouvez pas modifier la signature. Si vous souhaitez modifier la signature, vous devez ignorer la signature actuelle et la signer à nouveau à l’aide de l’option Pinceau/Clavier ci-dessus.

Vous pouvez sélectionner la variable **Configurer** ![configure](assets/configure.png) pour définir les proportions du canevas de signature tactile.
* Lorsque le rapport d’aspect de la zone de travail de signature tactile est inférieur à 1, les informations de géolocalisation sont ajoutées au bas de la zone de travail de signature tactile.

* Lorsque le rapport d’aspect de la zone de travail de signature tactile est supérieur à 1, les informations de géolocalisation sont ajoutées au côté droit de la zone de travail de signature tactile.

![Bas de la signature tactile](/help/forms/using/assets/scribble-signature-aspectratio.PNG)


>[!NOTE]
>
>Les signatures sont toujours enregistrées au format PNG.
>

## Configuration d’un formulaire adaptatif pour utiliser la signature tactile {#configure-an-adaptive-form-to-use-scribble-signature}

1. Créez une option Document d’enregistrement activée ou un formulaire adaptatif basé sur modèle de formulaire. Pour obtenir des informations détaillées, voir [Création d’un formulaire adaptatif](../../forms/using/creating-adaptive-form.md).
1. Faites glisser et déposez le composant **Signature tactile** du navigateur de composant vers le formulaire adaptatif.
1. Sélectionnez la variable **Configurer** ![configure](assets/configure.png) Icône Vous ouvrez ainsi le navigateur de propriétés qui affiche les propriétés du composant Signature tactile. Configurez les propriétés du composant Signature tactile.
1. Faites glisser et déposez le composant Étape de signature du navigateur de composant vers le formulaire adaptatif.

   >[!NOTE]
   >
   >Le composant Étape de signature prend toute la largeur disponible pour le formulaire. Il est recommandé de ne pas avoir d’autre composant sur la section contenant le composant Étape de signature. 
   >

1. Dans l’explorateur de contenu, sélectionnez **Conteneur de formulaires**, puis sélectionnez la variable **Configurer** ![configure](/help/forms/using/assets/configure.png) Icône L’explorateur de propriétés s’ouvre et affiche les propriétés du conteneur de formulaires adaptatifs. Accédez à **Conteneur de formulaires adaptatifs** > **Signature électronique** et désélectionnez l’option **Activer Adobe Sign** . Sélectionnez Terminé . ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) pour enregistrer les modifications.

   >[!NOTE]
   >
   >Lorsque vous ajoutez un composant Étape de signature à un formulaire adaptatif, l’option Activer Adobe Sign est sélectionnée automatiquement.
   >

1. Sélectionnez la variable **Configurer** ![configure](assets/configure.png) Icône Elle ouvre l’explorateur de propriétés et affiche les propriétés Étape de signature. Configurez les propriétés suivantes :

   * **Nom de l’élément** : spécifiez le nom du composant.

   * **Titre :** Spécifiez le titre unique du composant.
   * **Message du modèle :** Spécifiez le message à afficher pendant le chargement du PDF de signatures. Les services Adobe Sign prennent du temps pour préparer et charger le PDF de signatures.
   * **Service de signature :** sélectionnez l’option **Signature tactile**.

   * **Classe CSS** : spécifiez la classe CSS de la bibliothèque client, le cas échéant. Utilisation [thèmes](../../forms/using/themes.md) et [styles en ligne](../../forms/using/inline-style-adaptive-forms.md) au lieu de la classe CSS.

   Sélectionnez Terminé . ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) pour enregistrer les modifications. La signature est configurée correctement.

   Désormais, lorsque vous remplissez un formulaire, une version PDF du formulaire adaptatif s’affiche et des options pour signer le document du PDF sont fournies. Pour plus d’informations, voir [Signature d’un formulaire adaptatif en utilisant la signature tactile](../../forms/using/signing-forms-using-scribble.md#sign-an-adaptive-form-using-scribble-signature).

## Signature d’un formulaire adaptatif à l’aide de la signature tactile {#sign-an-adaptive-form-using-scribble-signature}

1. Une fois que vous avez rempli un formulaire adaptatif et atteint la page Étape de signature, l’écran de signature s’affiche.

   ![Boîte de dialogue de signature tactile](/help/forms/using/assets/esignscribblesign.jpg)

1. Cliquez sur **[!UICONTROL Sign]**. La boîte de dialogue de signature tactile s’affiche. Signez le formulaire et cliquez sur l’icône Terminé ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) pour enregistrer la signature.

   ![Boîte de dialogue de signature tactile](/help/forms/using/assets/scribblewidget.png)

1. Cliquez sur Terminer pour terminer le processus de signature.

   ![Terminer le processus de signature](/help/forms/using/assets/scribblecomplete.jpg)

Les signatures sont ajoutées au formulaire, et le contrôle de formulaire passe au panneau suivant.
