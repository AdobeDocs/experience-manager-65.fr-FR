---
title: Application de règles aux champs de formulaires adaptatifs
seo-title: Apply rules to adaptive form fields
description: Créez des règles pour ajouter de l’interactivité, une logique d’entreprise et des validations intelligentes à un formulaire adaptatif.
seo-description: Create rules to add interactivity, business logic, and smart validations to an adaptive form.
page-status-flag: de-activated
uuid: 60f142aa-81ca-4333-8614-85a01e23e917
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 982eddba-2350-40e7-8a42-db02d28cf133
exl-id: 0202ca65-21ef-4477-b704-7b52314a7d7b
source-git-commit: 63bc43bba88a42d62fb574bc8ce42470ac61d693
workflow-type: ht
source-wordcount: '1124'
ht-degree: 100%

---

# Didacticiel : application de règles aux champs de formulaires adaptatifs {#tutorial-apply-rules-to-adaptive-form-fields}

![06-apply-rules-to-adaptive-form_main](assets/06-apply-rules-to-adaptive-form_main.png)

Ce didacticiel est une étape de la série [Création de votre premier formulaire adaptatif](/help/forms/using/create-your-first-adaptive-form.md). Adobe recommande de suivre la série dans l’ordre chronologique pour comprendre, exécuter et démontrer le cas d’utilisation complet du didacticiel.

## À propos du didacticiel {#about-the-tutorial}

Vous pouvez utiliser des règles pour ajouter de l’interactivité, une logique d’entreprise et des validations intelligentes à un formulaire adaptatif. Les formulaires adaptatifs ont un éditeur de règles intégré. L’éditeur de règles offre une fonctionnalité de glisser-déposer, semblable aux visites guidées. L’option de glisser-déposer est la méthode la plus rapide et la plus simple pour créer des règles. L’éditeur de règles fournit également une fenêtre de code pour les utilisateurs intéressés par le test de leurs compétences de codage ou à par l’optimisation des règles.

Vous pouvez en savoir plus sur l’éditeur de règles dans [l’Éditeur de règles de formulaires adaptatifs](/help/forms/using/rule-editor.md).

À la fin du didacticiel, vous apprendrez à créer des règles pour :

* appeler un service de modèle de données de formulaire pour récupérer des données de la base de données ;
* appeler un service de modèle de données de formulaire pour ajouter des données à la base de données ;
* exécuter une vérification des validations et afficher les messages d’erreur.

Les images GIF interactives à la fin de chaque section du didacticiel vous aident à apprendre et à valider les fonctionnalités du formulaire que vous créez, à la volée. 

## Étape 1 : récupération d’un enregistrement client à partir de la base de données {#retrieve-customer-record}

Vous avez créé un modèle de données de formulaire en suivant l’article [Création d’un modèle de données de formulaire](/help/forms/using/create-form-data-model.md). Maintenant, vous pouvez utiliser l’éditeur de règles pour appeler les services de modèle de données de formulaire pour récupérer et ajouter des informations à la base de données.

Chaque client se voit attribuer un numéro d’ID de client unique, ce qui permet d’identifier les données client pertinentes dans une base de données. La procédure ci-dessous utilise l’ID de client pour récupérer les informations à partir de la base de données :

1. Ouvrez le formulaire adaptatif pour le modifier.

   [http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html](http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html)

1. Appuyez sur le champ **[!UICONTROL ID de client]** et appuyez sur l’icône **[!UICONTROL Modifier les règles]**. La fenêtre Éditeur de règles s’ouvre.
1. Appuyez sur l’icône **[!UICONTROL + Créer]** pour ajouter une règle. L’éditeur visuel s’ouvre.

   Dans l’éditeur visuel, l’instruction **[!UICONTROL QUAND]** est sélectionnée par défaut. En outre, l’objet de formulaire (dans ce cas, **[!UICONTROL ID de client]**) d’où vous avez lancé l’éditeur de règles est spécifié dans l’instruction **[!UICONTROL QUAND]**.

1. Cliquez sur le menu déroulant **[!UICONTROL Sélectionner un état]** et sélectionnez **[!UICONTROL a changé]**.

   ![whencustomeridischanged](assets/whencustomeridischanged.png)

1. Dans l’instruction **[!UICONTROL PUIS]**, sélectionnez **[!UICONTROL Appeler un service]** à partir du menu déroulant **[!UICONTROL Sélectionner une action.]**
1. Sélectionnez le service **[!UICONTROL Extraire l’adresse d’expédition]** dans le menu déroulant **[!UICONTROL Sélectionner]**.
1. Faites glisser et déposez le champ **[!UICONTROL ID du client]** de l’onglet Objets de formulaire vers le champ **[!UICONTROL Déposer l’objet ou sélectionner ici]** dans la zone **[!UICONTROL ENTREE]**.

   ![dropobjectstoinputfield-retrievedata](assets/dropobjectstoinputfield-retrievedata.png)

1. Faites glisser et déposez le champ **[!UICONTROL ID du client, Nom, Adresse d’expédition, État et Code postal]** de l’onglet Objets de formulaire vers le champ **[!UICONTROL Déposer l’objet ou sélectionner ici]** dans la zone **[!UICONTROL SORTIE]**.

   ![dropobjectstooutputfield-retrievedata](assets/dropobjectstooutputfield-retrievedata.png)

   Appuyez sur **[!UICONTROL Terminé]** pour enregistrer la règle. Dans la fenêtre Éditeur de règles, appuyez sur **[!UICONTROL Fermer]**.

1. Prévisualisez le formulaire adaptatif. Entrez un ID dans le champ **[!UICONTROL ID client]**. Le formulaire peut maintenant récupérer les détails du client à partir de la base de données.

   ![retrieve-information](assets/retrieve-information.gif)

## Étape 2 : insertion de l’adresse client mise à jour dans la base de données {#updated-customer-address}

Une fois les détails du client extraits de la base de données, vous pouvez mettre à jour l’adresse de livraison, l’État et le code postal. La procédure ci-dessous appelle un service de modèle de données de formulaire pour mettre à jour les informations client dans la base de données :

1. Sélectionnez le champ **[!UICONTROL Envoyer]** et appuyez sur l’icône **[!UICONTROL Modifier les règles]**. La fenêtre Éditeur de règles s’ouvre.
1. Sélectionnez la règle **[!UICONTROL Envoyer - Cliquer]** et appuyez sur l’icône **[!UICONTROL Modifier]**. Les options permettant de modifier la règle Envoi s’affichent.

   ![règle-envoi](assets/submit-rule.png)

   Dans l’option WHEN, les options **[!UICONTROL Envoi]** et **[!UICONTROL est activé]** sont déjà sélectionnées.

   ![envoi-est-activé](assets/submit-is-clicked.png)

1. Dans l’option **[!UICONTROL PUIS]**, appuyez sur l’option **[!UICONTROL + Ajoutez l’instruction]**. Sélectionnez **[!UICONTROL Appel du service]** à partir du menu déroulant **[!UICONTROL Sélectionner l’action]**.
1. Sélectionnez le service **[!UICONTROL Mettre à jour l’adresse de livraison]** dans le menu déroulant **[!UICONTROL Sélectionner]**.

   ![mettre-à-jour-l’adresse-de-livraison](assets/update-shipping-address.png)

   ![dropobjectstoinputfield-updatedata](assets/dropobjectstoinputfield-updatedata.png)

1. Faites glisser et déposez le champ **[!UICONTROL Adresse d’expédition, état et code postal]** de l’onglet [!UICONTROL Objets de formulaire] vers l’élément tablename.property correspondant (par exemple, customerdetails.shippingAddress) du champ **[!UICONTROL Déposer l’objet ou sélectionnez ici]** dans la zone **[!UICONTROL ENTRÉE]**. Tous les champs portant le préfixe tablename (par exemple, customerdetails dans ce cas d’utilisation) servent de données d’entrée pour le service de mise à jour. Tout le contenu fourni dans ces champs est mis à jour dans la source de données.

   >[!NOTE]
   >
   >Ne faites pas glisser les champs **[!UICONTROL Nom]** et **[!UICONTROL ID du client]** vers l’élément tablename.property correspondant (par exemple, customerdetails.name). Cela permet d’éviter de mettre à jour le nom et l’ID du client par erreur.

1. Glissez-déposez le champ **[!UICONTROL ID du client]** de l’onglet [!UICONTROL Objets de formulaire] vers le champ ID dans la zone **[!UICONTROL ENTREE]**. Les champs sans préfixe tablename (par exemple, customerdetails dans ce cas d’utilisation) servent de paramètre de recherche pour le service de mise à jour. Le champ **[!UICONTROL id]** dans ce cas d’utilisation identifie de manière unique un enregistrement dans la tableau **customerdetails**.
1. Appuyez sur **[!UICONTROL Terminé]** pour enregistrer la règle. Dans la fenêtre Éditeur de règles, appuyez sur **[!UICONTROL Fermer]**.
1. Prévisualisez le formulaire adaptatif. Récupérez les détails d’un client, mettez à jour l’adresse de livraison et envoyez le formulaire. Lorsque vous récupérez à nouveau les détails du même client, l’adresse de livraison mise à jour s’affiche.

## Étape 3 : (section bonus) utilisation de l’éditeur de code pour exécuter des validations et afficher les messages d’erreur {#step-bonus-section-use-the-code-editor-to-run-validations-and-display-error-messages}

Vous devez exécuter la validation sur le formulaire pour vous assurer que les données saisies dans le formulaire sont correctes et qu’un message d’erreur s’affiche en cas de données incorrectes. Par exemple, si un ID client non existant est entré dans le formulaire, un message d’erreur doit s’afficher.

Les formulaires adaptatifs fournissent plusieurs composants avec des validations intégrées, par exemple, des champs d’adresse électronique et des champs numériques que vous pouvez utiliser pour les cas d’utilisation courants. Utilisez l’éditeur de règles pour les cas d’utilisation avancés, par exemple, pour afficher un message d’erreur lorsque la base de données renvoie zéro (0) enregistrement (aucun enregistrement).

La procédure suivante montre comment créer une règle pour afficher un message d’erreur si l’ID du client entré dans le formulaire n’existe pas dans la base de données. La règle met également l’accent sur le champ **[!UICONTROL ID du client]** et le réinitialise. La règle utilise [l’API dataIntegrationUtils du service de modèle de données de formulaire](/help/forms/using/invoke-form-data-model-services.md) pour vérifier si l’ID du client existe dans la base de données.

1. Appuyez sur le champ **[!UICONTROL ID du client]** et sur l’icône `Edit Rules`. La fenêtre [!UICONTROL Éditeur de règles] s’ouvre.
1. Appuyez sur l’icône **[!UICONTROL + Créer]** pour ajouter une règle. L’éditeur visuel s’ouvre.

   Dans l’éditeur visuel, l’instruction **[!UICONTROL QUAND]** est sélectionnée par défaut. De même, l’objet du formulaire (dans ce cas, **[!UICONTROL ID du client]**) d’où vous avez lancé l’éditeur de règles est spécifié dans l’instruction **[!UICONTROL QUAND]**.

1. Appuyez sur la liste déroulante **[!UICONTROL Sélectionner un état]** et sélectionnez **[!UICONTROL est modifié]**.

   ![whencustomeridischanged](assets/whencustomeridischanged.png)

   Dans l’instruction **[!UICONTROL PUIS]**, sélectionnez **[!UICONTROL Appeler un service]** à partir du menu déroulant **[!UICONTROL Sélectionner une action.]**

1. Basculez de l’**[!UICONTROL éditeur visuel]** à l’**[!UICONTROL éditeur de code]**. Le contrôle du commutateur est sur le côté droit de la fenêtre. L’éditeur de code s’ouvre, affichant un code similaire à celui-ci :

   ![éditeur-de-code](assets/code-editor.png)

1. Remplacez la section de variable d’entrée par le code suivant :

   ```javascript
   var inputs = {
       "id" : this
   };
   ```

1. Remplacez la section `guidelib.dataIntegrationUtils.executeOperation (operationInfo, inputs, outputs)` par le code suivant :

   ```javascript
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, function (result) {
     if (result) {
         result = JSON.parse(result);
       customer_Name.value = result.name;
       customer_Shipping_Address = result.shippingAddress;
     } else {
       if(window.confirm("Invalid Customer ID. Provide a valid customer ID")) {
             customer_Name.value = " ";
            guideBridge.setFocus(customer_ID);
       }
     }
   });
   ```

1. Prévisualisez le formulaire adaptatif. Entrez un ID de client incorrect. Un message d’erreur s’affiche.

   ![display-validation-error](assets/display-validation-error.gif)
