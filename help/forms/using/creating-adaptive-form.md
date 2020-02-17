---
title: Création d’un formulaire adaptatif
seo-title: Création d’un formulaire adaptatif
description: Découvrez comment créer un formulaire adaptatif à l’aide d’AEM Forms. Les formulaires adaptatifs sont des formulaires HTML5 réactifs qui rationalisent la collecte et le traitement des informations.
seo-description: Découvrez comment créer un formulaire adaptatif à l’aide d’AEM Forms. Les formulaires adaptatifs sont des formulaires HTML5 réactifs qui rationalisent la collecte et le traitement des informations.
uuid: 444f461a-9e88-4385-b5ee-e985067ab7bc
content-type: reference
topic-tags: author
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: f06b8cb2-6f98-465f-beec-1e91e3f45707
translation-type: tm+mt
source-git-commit: 24728d320d46edc5e18385868ba92cb4292c8c5f

---


# Création d’un formulaire adaptatif {#creating-an-adaptive-form}

## <strong>Création d’un formulaire adaptatif</strong> {#strong-create-an-adaptive-form-strong}

Pour créer un formulaire adaptatif, suivez la procédure décrite ci-après.

1. Accédez à l’instance Auteur d’AEM Forms à l’adresse `https://[server]:[port]/<custom-context-if-any>.`

1. Entrez vos informations d’identification dans la page de connexion d’AEM.

   Une fois connecté, dans le coin supérieur gauche, appuyez sur **[!UICONTROL Adobe Experience Manager > Formulaires > Formulaires et documents]**.

   >[!NOTE]
   >
   >Dans le cadre d’une installation par défaut, l’identifiant est `admin` et le mot de passe est `admin`.

1. Appuyez sur **[!UICONTROL Créer]** et sélectionner le **[!UICONTROL Formulaire adaptatif]**.
1. Une option permettant de sélectionner un modèle s’affiche. For more information about templates, see [Adaptive form templates](/help/forms/using/creating-adaptive-form.md#p-adaptive-form-templates-p). Appuyez sur un modèle pour le sélectionner, puis appuyez sur Suivant.
1. Une option Ajouter des propriétés s’affiche. Spécifiez les valeurs des champs de propriété suivants. Les champs Titre et Nom sont obligatoires :

   * **[!UICONTROL Titre :]** spécifie le nom d’affichage du formulaire. Le titre vous permet d’identifier le formulaire dans l’interface utilisateur d’AEM Forms.
   * **** Nom : Indique le nom du formulaire. Un nœud portant le nom indiqué est alors créé dans le référentiel. Lorsque vous commencez à saisir un titre, une valeur pour le champ de nom est automatiquement générée. Vous pouvez modifier la valeur suggérée. Le champ de nom peut contenir uniquement des caractères alphanumériques, des traits d’union et des tirets bas. Toutes les entrées non valides sont remplacées par un tiret.
   * **** Description : Indique les informations détaillées sur le formulaire.
   * **[!UICONTROL Balises :]** indique les balises pour individualiser le formulaire adaptatif. Les balises aident à rechercher le formulaire. Pour créer des balises, saisissez les nouveaux noms de balise dans la boîte de dialogue **Balises.**

1. Vous pouvez créer un formulaire adaptatif basé sur l’un des modèles de formulaire suivants :

   * [Modèle de données de formulaire](#fdm)
   * [Modèle de formulaire XFA](/help/forms/using/creating-adaptive-form.md#p-create-an-adaptive-form-based-on-an-xfa-form-template-p)
   * [Schéma XML ou JSON](/help/forms/using/creating-adaptive-form.md#p-create-an-adaptive-form-based-on-xml-or-json-schema-p)
   * Aucun ou sans modèle de formulaire
   Vous pouvez configurer ces informations via l’onglet **[!UICONTROL Modèle de formulaire]** figurant sur la page **[!UICONTROL Ajouter des propriétés]**. Par défaut, le modèle de formulaire sélectionné est **[!UICONTROL Aucun]**.

1. Appuyez sur **Créer**. Un formulaire adaptatif est créé et une boîte de dialogue pour ouvrir le formulaire à modifier s’affiche.

   Once you have finished specifying all the properties, click **[!UICONTROL Create]**. Un formulaire adaptatif est créé et une boîte de dialogue pour ouvrir le formulaire à modifier s’affiche.

   Once you have finished specifying all the properties, click **[!UICONTROL Create]**. Un formulaire adaptatif est créé et une boîte de dialogue pour ouvrir le formulaire à modifier s’affiche.

1. Tap **[!UICONTROL Open]** to open the newly created form in a new tab. Le formulaire s’ouvre pour être modifié et affiche le contenu disponible dans le modèle. Il affiche également la barre latérale permettant de personnaliser le formulaire nouvellement créé selon vos besoins. 

   En fonction du type de formulaire adaptatif, les éléments de formulaire présents dans le modèle de formulaire XFA, le schéma XML ou le schéma JSON associé sont affichés dans l’onglet **[!UICONTROL Objets de modèle de données]** de l’**[!UICONTROL explorateur de contenu]** dans la barre latérale. Vous pouvez également faire glisser ces éléments pour créer votre formulaire adaptatif.

   Pour plus d’informations sur l’interface de création de formulaires adaptatifs et les composants disponibles, voir [Présentation de la création de formulaires adaptatifs](/help/forms/using/introduction-forms-authoring.md).

   >[!NOTE] {grayBox=&quot;true&quot;}
   >
   >Autorisez les fenêtres indépendantes dans votre navigateur pour ouvrir le formulaire créé dans un nouvel onglet.

## Créer un formulaire adaptatif basé sur un modèle de données de formulaire {#fdm}

[L’intégration de données AEM Forms](/help/forms/using/data-integration.md) vous permet d’intégrer plusieurs sources de données et de rassembler leurs entités et services pour créer un modèle de données de formulaire. Il s’agit d’une extension du schéma JSON. Vous pouvez utiliser un modèle de données du formulaire pour créer un formulaire adaptatif. Les entités ou les objets de modèle de données configurés dans un modèle de données de formulaire sont disponibles en tant qu’objets de modèle de données pour la création de formulaire. Ils sont associés à des sources de données respectives et utilisés pour pré-remplir un formulaire et écrire les données envoyées dans les sources de données respectives. Vous pouvez également appeler des services configurés dans un modèle de données de formulaire à l’aide des règles de formulaire adaptatif.

Pour utiliser un modèle de données de formulaire pour créer un formulaire adaptatif :

1. Dans l’onglet Modèle de formulaire de l’écran Ajouter des propriétés, sélectionnez **[!UICONTROL Modèle de données de formulaire]** dans la liste déroulante **[!UICONTROL Sélectionner à partir de]**.

   ![create-af-1-1](assets/create-af-1-1.png)

1. Appuyez pour développer le **[!UICONTROL modèle de données de formulaire sélectionné]**. Tous les modèles de données de formulaire disponibles sont répertoriés.

   Sélectionnez un modèle de données de formulaire.

   ![create-af-2-1](assets/create-af-2-1.png)

>[!NOTE]
>
>Vous pouvez également remplacer le modèle de données de formulaire par un formulaire adaptatif. For detailed steps, see [Edit Form Model properties of an adaptive form](#edit-form-model).

## Création d’un formulaire adaptatif basé sur un modèle de formulaire XFA {#create-an-adaptive-form-based-on-an-xfa-form-template}

Vous pouvez réutiliser vos modèles de formulaire XFA pour créer des formulaires adaptatifs. Pour ce faire, téléchargez et associez un modèle de formulaire XFA à un formulaire adaptatif. Les éléments du modèle de formulaire (formulaire XFA) sont disponibles dans l’outil de recherche de contenu au moment de la création de formulaires adaptatifs. Dans l’outil de recherche de contenu, vous pouvez faire glisser les éléments de modèle de formulaire jusqu’au formulaire.

>[!NOTE]
>
>[Téléchargez le modèle de formulaire XFA](/help/forms/using/get-xdp-pdf-documents-aem.md) vers AEM Forms avant de commencer à créer un formulaire adaptatif basé sur le modèle de formulaire.

Procédez comme suit pour utiliser un modèle de formulaire XFA en tant que modèle de formulaire pour votre formulaire adaptatif :

1. Sur la page **[!UICONTROL Ajouter des propriétés]**, ouvrez l’onglet **[!UICONTROL Modèle de formulaire]**.
1. In the Form Model tab, from the drop-down list, select **[!UICONTROL Form Templates]**. Tous les modèles de formulaire qui ont été chargés vers le référentiel via l’interface utilisateur d’AEM Forms sont répertoriés ici pour être sélectionnés. Sélectionnez un modèle dans la liste.

   ![Association d’un modèle de formulaire XFA à un formulaire adaptatif](assets/form_model_xfa_associate.png)
   **** Figure : *Sélection d’un modèle de formulaire*

   >[!NOTE]
   >
   >Vous pouvez également remplacer le modèle de formulaire par un formulaire adaptatif. For detailed steps, see [Edit Form Model properties of an adaptive form](#edit-form-model).

## Créer un formulaire adaptatif en fonction du schéma XML ou JSON {#create-an-adaptive-form-based-on-xml-or-json-schema}

Les schémas XML et JSON représentent la structure dans laquelle les données sont générées ou utilisées par le système principal de votre organisation. Vous pouvez associer un schéma à un formulaire adaptatif et utiliser ses éléments pour ajouter du contenu dynamique à un formulaire adaptatif. Les éléments du schéma sont disponibles dans l’onglet Objet du modèle de données du navigateur de contenu pour la création de formulaires adaptatifs. Vous pouvez faire glisser et déposer les éléments du schéma pour créer le formulaire.

Consultez les documents suivants pour découvrir comment concevoir un schéma XML ou JSON pour la création de formulaires adaptatifs.

* [Création de formulaires adaptatifs à l’aide d’un schéma XML](/help/forms/using/adaptive-form-xml-schema-form-model.md)
* [Création de formulaires adaptatifs à l’aide d’un schéma JSON](/help/forms/using/adaptive-form-json-schema-form-model.md)

Procédez comme suit pour utiliser un schéma XML ou JSON comme modèle de formulaire pour un formulaire adaptatif :

1. On the **[!UICONTROL Add Properties]** step of adaptive form creation page, tap on the **[!UICONTROL Form Model]** tab.
1. In the Form Model tab, select **[!UICONTROL Schema]** from the **[!UICONTROL Select From]** drop-down field.

1. Tap **[!UICONTROL Select Schema]** and do one of the following:

   * **[!UICONTROL Télécharger depuis un disque]** : sélectionnez cette option et appuyez sur Charger une définition de schéma pour parcourir et charger un schéma XML ou un schéma JSON à partir de votre système de fichiers. Le fichier de schéma chargé se trouve avec le formulaire et n’est pas accessible aux autres formulaires adaptatifs.
   * **[!UICONTROL Recherche dans le référentiel]** : sélectionnez cette option pour effectuer une sélection dans la liste fichiers de définition de schéma disponibles dans le référentiel. Sélectionnez le fichier de schéma XML ou JSON comme modèle de formulaire. Le schéma sélectionné sera associé au formulaire par référence et sera accessible pour une utilisation dans d’autres formulaires adaptatifs.
   >[!CAUTION] {grayBox=&quot;true&quot;}
   >
   >Assurez-vous que le nom du schéma JSON se termine par **.schema.json**. Par exemple : mySchema.schema.json

   ![Sélection du schéma XML ou JSON](assets/upload-schema.png)
   **** Figure : *Sélection d’un schéma XML ou JSON*

1. (Pour le schéma XML uniquement) Après avoir sélectionné ou chargé un schéma XML, spécifiez un élément racine du fichier XSD sélectionné à mapper avec le formulaire adaptatif.

   ![Sélection de l’élément racine de schéma XSD](assets/xsd-root-element.png)
   **** Figure : *Sélection de l’élément racine XSD*

>[!NOTE]
>
>Vous pouvez également remplacer le schéma par un formulaire adaptatif. For detailed steps, see [Edit Form Model properties of an adaptive form](#edit-form-model).

## Modèles de formulaires adaptatifs {#adaptive-form-templates}

Un modèle fournit une structure de base et définit l’aspect, c’est-à-dire la mise en page et les styles, d’un formulaire adaptatif. Il comporte des composants pré-formatés contenant certaines propriétés et une certaine structure de contenu. AEM Forms fournit des modèles de formulaire adaptatif prêts à l’emploi. Pour obtenir le package de modèles complet, notamment les modèles avancés, vous devez installer le package complémentaire AEM Forms. For more information, see [Installing AEM Forms add-on package](/help/forms/using/installing-configuring-aem-forms-osgi.md).

En outre, vous pouvez utiliser l’éditeur de modèle pour créer vos propres modèles. Pour plus d’informations sur l’utilisation de modèles, voir [Modèles de formulaires adaptatifs](/help/forms/using/template-editor.md).

>[!NOTE]
>
>Lorsque vous ouvrez un formulaire adaptatif créé à l’aide du modèle avancé pour l’édition, un message d’erreur s’affiche. Le modèle avancé comporte un composant Étape de signature et Adobe Sign est activé pour ce dernier par défaut. Créez et sélectionnez une [configuration de cloud Adobe Sign](/help/forms/using/adobe-sign-integration-adaptive-forms.md) et [configurez un signataire](/help/forms/using/working-with-adobe-sign.md#main-pars-header-1374317451) pour résoudre l’erreur.

## Modifier les propriétés du modèle de formulaire d’un formulaire adaptatif {#edit-form-model}

Les formulaires adaptatifs sont créés sans modèle de formulaire (en utilisant l’option Aucun pour le modèle de formulaire) ou en utilisant un modèle de formulaire tel qu’un schéma XML ou JSON ou un modèle de données de formulaire. Vous pouvez remplacer le modèle de formulaire par un formulaire adaptatif en remplaçant Aucun par un autre modèle de formulaire. Pour un formulaire adaptatif basé sur un modèle de formulaire, vous pouvez choisir un autre modèle de formulaire, un schéma XML, un schéma JSON ou un modèle de données de formulaire pour le même modèle de formulaire. Cependant, vous ne pouvez pas passer d’un modèle de formulaire à un autre.

1. Select the adaptive form and tap the **Properties** icon.
1. Open the **[!UICONTROL Form Model]** tab and do one the following.

   * Si le formulaire adaptatif ne dispose pas de modèle de formulaire, vous pouvez choisir un autre modèle de formulaire et, en conséquence, sélectionner un modèle de formulaire, un schéma XML ou JSON ou un modèle de données de formulaire.
   * Si le formulaire adaptatif est basé sur un modèle de formulaire, vous pouvez choisir un autre modèle de formulaire, un schéma XML ou JSON ou un modèle de données de formulaire pour le même modèle de formulaire.

1. Appuyez sur **[!UICONTROL Enregistrer]** pour enregistrer les propriétés.

## Enregistrement automatique d’un formulaire adaptatif {#auto-save-an-adaptive-form}

Par défaut, le contenu d’un formulaire adaptatif est enregistré sur une action utilisateur, telle que appuyer sur le bouton Enregistrer. Vous pouvez également configurer un formulaire adaptatif pour commencer automatiquement à enregistrer le contenu basé sur un événement ou un intervalle de temps. L’option d’enregistrement automatique est utile pour :

* Enregistrement automatique du contenu pour les utilisateurs anonymes et connectés
* Enregistrement du contenu d’un formulaire sans intervention ou une intervention minimale de l’utilisateur
* Commencer à enregistrer le contenu d’un formulaire en fonction d’un événement utilisateur
* Enregistrer le contenu d’un formulaire à plusieurs reprises après un intervalle de temps spécifié

### Activation de l’enregistrement automatique d’un formulaire adaptatif {#enable-auto-save-for-an-adaptive-form}

Par défaut, l’option d’enregistrement automatique n’est pas activée. Vous pouvez activer l’option d’enregistrement automatique depuis l’onglet automatique Enregistrement automatique d’un formulaire adaptatif. L’onglet Enregistrement automatique d’Adobe fournit également plusieurs autres options de configuration. Effectuez les étapes suivantes afin d’activer et de configurer l’option d’enregistrement automatique pour un formulaire adaptatif :

1. To access the auto-save section in the properties, select a component, then tap ![field-level](assets/field-level.png) > **[!UICONTROL Adaptive Form Container]**, and then tap ![cmppr](assets/cmppr.png).
1. Dans la section **[!UICONTROL Sauvegarde automatique]**, **[!UICONTROL activez]** l’option d’enregistrement automatique.
1. Dans la boîte de dialogue **[!UICONTROL Evénement de formulaire adaptatif]**, spécifiez 1 ou TRUE pour lancer automatiquement l’enregistrement du formulaire lorsque celui-ci est chargé dans le navigateur. Vous pouvez également spécifier une expression conditionnelle pour un événement qui, lorsqu’il est déclenché et renvoie true, commence l’enregistrement du contenu du formulaire.
1. Spécifiez le déclencheur. L’enregistrement automatique est déclenché en fonction de votre configuration. Vous avez le choix entre :

   * **[!UICONTROL Basé sur l’heure :]** sélectionnez l’option pour commencer à enregistrer le contenu selon un intervalle de temps spécifié.
   * **[!UICONTROL Basé sur les événements :]** sélectionnez l’option pour commencer à enregistrer le contenu sur la base d’un événement déclenché.
   Lorsque vous sélectionnez un déclencheur, la zone Configuration de la stratégie est activée. La zone Configuration de la stratégie vous permet d’effectuer les opérations suivantes :

   * Spécifiez un intervalle de temps si vous sélectionnez un déclencheur **[!UICONTROL basé sur l’heure]**.
   * Spécifiez un nom d’événement si vous sélectionnez un déclencheur **[!UICONTROL basé sur un événement.]**
   Vous pouvez également créer et ajouter à la liste votre propre stratégie personnalisée. Pour plus d’informations, reportez-vous à la section [Mise en œuvre d’une stratégie personnalisée pour enregistrer automatiquement les formulaires](/help/forms/using/auto-save-an-adaptive-form.md#p-implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms-p).

1. (Enregistrement automatique basé sur un moment uniquement) Exécutez les étapes suivantes pour configurer les options de l’enregistrement automatique basé sur un moment.

   1. Dans le champ **[!UICONTROL Enregistrement automatique sur cet intervalle]**, indiquez l’intervalle en secondes. Le formulaire est enregistré à plusieurs reprises après écoulement du nombre de secondes spécifié dans la zone d’intervalle.

1. (Enregistrement automatique basé sur un événement uniquement) Exécutez les étapes suivantes pour configurer les options d’enregistrement automatique basé sur un événement.

   1. Dans la zone **Enregistrement automatique après cet événement**, spécifiez un événement [GuideBridge](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html). Le formulaire est enregistré chaque fois que l’expression renvoie TRUE.

1. (Facultatif) Pour enregistrer automatiquement le contenu pour des utilisateurs anonymes, sélectionnez l’option **Activer l’enregistrement automatique pour les utilisateurs anonymes**, puis cliquez sur **[!UICONTROL OK]**.

   >[!NOTE]
   >
   >Pour que l’option d’enregistrement automatique fonctionne pour les utilisateurs anonymes, assurez-vous de configurer le service de configuration commun aux formulaires pour autoriser tous les utilisateurs à prévisualiser, vérifier et signer des formulaires.
   >
   >To configure the service, go to AEM Web Console configuration at `https://[server]:[host]/system/console/configMgr` and edit the **[!UICONTROL Forms Common Configuration Service]** to choose the **[!UICONTROL All Users]** option in the **[!UICONTROL Allow]** field, and save the configuration.