---
title: Comment créer un formulaire adaptatif ?
seo-title: Learn how to create a Core Components based Adaptive Form on AEM 6.5 Forms.
description: Découvrez comment créer un formulaire adaptatif à l’aide de [!DNL Experience Manager Forms]. Les formulaires adaptatifs sont des formulaires HTML5 réactifs qui rationalisent la collecte et le traitement des informations. Découvrez comment créer un formulaire adaptatif basé sur un modèle de données de formulaire et un schéma XML ou JSON.
seo-description: Learn how to create an Adaptive Form using [!DNL Experience Manager Forms]. Adaptive Forms are responsive HTML5 forms that streamline information gathering and processing. Dig deeper on how to create an Adaptive Form based on a Form Data Model and XML or JSON schema.
Keywords: create adaptive form core component, create core component based adaptive form, creare adaptive form
products: SG_EXPERIENCEMANAGER/6.5/FORMS
contentOwner: Khushwant Singh
topic-tags: Adaptive Forms
docset: aem65
role: Admin, Developer
source-git-commit: daf97f3d5c5f3c92ff5caeccff583e54f3f57364
workflow-type: tm+mt
source-wordcount: '1869'
ht-degree: 37%

---


# Création d’un Forms adaptatif basé sur des composants principaux {#creating-an-adaptive-form-core-components}

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM 6.5 | Cet article |
| AEM as a Cloud Service | [Cliquez ici](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form-core-components.html?lang=fr) |

Les formulaires adaptatifs vous permettent de créer des formulaires attrayants, réactifs, dynamiques et adaptatifs. AEM Forms fournit une interface utilisateur conviviale pour les entreprises afin de créer rapidement un Forms adaptatif. L’interface utilisateur propose une navigation par onglets rapide pour sélectionner facilement un modèle, un style, des champs et des options d’envoi préconfigurés afin de créer un formulaire adaptatif.

Avant de commencer, découvrez les types de composants de formulaires disponibles :

* [Composants principaux de formulaires adaptatifs](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=fr) : il s’agit de composants de capture de données normalisés. Ces composants offrent des fonctionnalités de personnalisation, un délai de développement réduit et de plus bas coûts de maintenance pour vos expériences d’inscription numérique. Un développeur ou une développeuse peut facilement personnaliser et mettre en forme ces composants. Adobe recommande d’utiliser ces composants modernes et extensibles pour développer des formulaires adaptatifs.

* [Composants de base des formulaires adaptatifs](creating-adaptive-form.md) : il s’agit de composants de capture de données classiques (anciens). Vous pouvez continuer à les utiliser pour modifier votre formulaire adaptatif existant basé sur les composants de base. Si vous créez des formulaires, Adobe recommande d’utiliser  [Composants principaux de Forms adaptatif](/help/forms/using/create-adaptive-form.md) pour créer une Forms adaptative.

## Conditions préalables

Pour créer un formulaire adaptatif, vous devez disposer des éléments suivants :

* **Activation des composants principaux de Forms adaptatif pour votre environnement**: AEM projet Archetype version 41 ou ultérieure est requis pour [Activation des composants principaux pour votre environnement](/help/forms/using/enable-adaptive-forms-core-components.md). Lors de l’activation des composants principaux pour votre environnement, la variable **Forms adaptatif (composant principal)** modèle et thème Zone de travail sont ajoutés à votre environnement.

* **Un modèle de formulaire adaptatif** : un modèle fournit une structure de base et définit l’aspect, c’est-à-dire la mise en page et les styles, d’un formulaire adaptatif. Il comporte des composants pré-formatés contenant certaines propriétés et une certaine structure de contenu. Il fournit également les options permettant de définir un thème et une action d’envoi. Le thème définit l’aspect et l’action d’envoi définit l’action à entreprendre lors de l’envoi d’un formulaire adaptatif. Par exemple, l’envoi des données collectées à une source de données. Le modèle nommé `blank` est pris en charge :

   * Le `blank` modèle est inclus avec chaque nouvel environnement AEM Forms On-Premise et AMS.
   * Vous pouvez installer le package de référence, via Package Manager, pour ajouter le `blank` vers votre environnement AEM Forms On-Premise et AMS.
   * Vous pouvez également [créer un modèle de formulaire adaptatif (composants principaux)](template-editor.md) à partir de zéro.

  >[!NOTE]
  >
  > Si vous n’avez pas le modèle **Formulaires adaptatifs (composant principal)** sur votre environnement, vous devez [activer les composants principaux des formulaires adaptatifs pour votre environnement](/help/forms/using/enable-adaptive-forms-core-components.md). Quand vous activez des composants principaux pour votre environnement, le modèle **Formulaires adaptatifs (composant principal)** est ajouté à votre environnement.

* **Un thème de formulaire adaptatif** : un thème contient des détails de style pour les composants et les panneaux. Ces styles incluent les propriétés telles que les couleurs d’arrière-plan, les couleurs d’état, la transparence, l’alignement et la taille. Lorsque vous appliquez un thème, le style spécifié se reflète sur les composants correspondants.  Le `Canvas` est ajouté par défaut lorsque vous activez les composants principaux pour votre environnement. Vous pouvez également [télécharger et personnaliser les thèmes de référence](create-or-customize-themes-for-adaptive-forms-core-components.md).

* **Autorisations** : ajoutez vos utilisateurs et utilisatrices au groupe [!DNL forms-users]. Les membres du groupe [!DNL forms-users] ont les autorisations de créer un formulaire adaptatif. Pour obtenir la liste détaillée des groupes d’utilisateurs spécifiques aux formulaires, voir [Groupes et autorisations](forms-groups-privileges-tasks.md).

## Créer un formulaire adaptatif {#create-an-adaptive-form}

1. Connectez-vous à votre [AEM instance d’auteur](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html?lang=en#author-and-publish-installs).

1. Entrez vos informations d’identification dans la page de connexion d’Experience Manager. Une fois connecté, dans le coin supérieur gauche, appuyez sur **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Formulaires]** > **[!UICONTROL Formulaires et documents.]**.

1. Appuyer **[!UICONTROL Créer]**  > **[!UICONTROL Création d’un Forms adaptatif]**.

1. Sélectionnez un modèle de composants principaux de Forms adaptatif et cliquez sur **[!UICONTROL Suivant]**.

1. Le **[!UICONTROL Ajouter des propriétés]** apparaît. Spécifiez les valeurs des champs de propriété suivants. Les champs Titre et Nom sont obligatoires :

   * **[!UICONTROL Titre :]** Indique le nom d’affichage du formulaire. Le titre vous permet d’identifier le formulaire dans l’interface utilisateur [!DNL Experience Manager Forms] d’AEM Forms.
   * **[!UICONTROL Nom :]** indique le nom du formulaire. Un nœud portant le nom spécifié est créé dans le référentiel. Lorsque vous commencez à saisir un titre, la valeur du champ Nom est automatiquement générée. Vous pouvez modifier la valeur suggérée. Le champ Nom ne peut contenir que des caractères alphanumériques, des traits d’union et des traits de soulignement.
   * **[!UICONTROL Description :]** indique des informations détaillées relatives au formulaire.
   * **[!UICONTROL Bibliothèque cliente du thème]:** Indique le thème d’un formulaire adaptatif. Par défaut, la variable `adaptiveform.theme.canvas3` Le thème est sélectionné. Vous pouvez également choisir un thème différent dans la **[!UICONTROL Bibliothèque cliente du thème]** menu déroulant.
   * **[!UICONTROL Conteneur de configuration :]**  Définit un emplacement où sont stockés les fichiers de configuration pour le Forms adaptatif. Ces fichiers de configuration contiennent des paramètres et des propriétés liés au comportement et à l’aspect d’Adaptive Forms.
   * **[!UICONTROL Balises :]** indique les balises pour individualiser le formulaire adaptatif. Les balises aident à rechercher le formulaire. Pour créer des balises, saisissez les nouveaux noms de balise dans la boîte de dialogue **[!UICONTROL Balises.]**
1. Appuyez sur **[!UICONTROL Créer]**. Un formulaire adaptatif est créé et une boîte de dialogue pour ouvrir le formulaire à modifier s’affiche.


1. Appuyer **[!UICONTROL Modifier]** pour ouvrir le formulaire nouvellement créé dans un nouvel onglet. Le formulaire s’ouvre pour modification et affiche le contenu disponible dans le modèle. Il affiche également la barre latérale permettant de personnaliser le formulaire nouvellement créé.


## Utilisation des composants principaux de Forms adaptatif pour créer votre formulaire

Après avoir ouvert le formulaire pour le modifier, vous pouvez utiliser les composants principaux de Forms adaptatif disponibles pour ajouter des champs de formulaire à votre formulaire. Vous pouvez faire glisser et déposer ou utiliser le + [insérer le composant] pour ajouter ces composants à un formulaire. Pour en savoir plus sur les composants principaux disponibles, reportez-vous à la documentation AEM Composants principaux . [Composants principaux de Forms adaptatif](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=en#components). Vous pouvez également consulter [https://aemcomponents.dev/](https://aemcomponents.dev/) pour afficher les composants principaux disponibles en action.

## Configuration de l’action Envoyer pour un formulaire adaptatif {#configure-submit-action-for-form}

Une action Envoyer vous permet de choisir la destination des données capturées via un formulaire adaptatif. Elle est déclenchée lorsqu’un utilisateur clique sur le bouton Envoyer d’un formulaire adaptatif. Les formulaires adaptatifs incluent certaines actions d’envoi prêtes à l’emploi. Vous pouvez également étendre une action d’envoi par défaut pour créer votre propre action d’envoi personnalisée. Pour configurer une action Envoyer pour votre formulaire :

1. Ouvrez l’explorateur de contenu , puis sélectionnez l’option **[!UICONTROL Conteneur de guide]** du formulaire adaptatif.
1. Cliquez sur les propriétés du conteneur de guide. ![Propriétés du guide](/help/forms/using/assets/configure-icon.svg) icône . La boîte de dialogue Conteneur de formulaires adaptatifs s’ouvre.

1. Cliquez sur le bouton  **[!UICONTROL Envoi]** .

   ![Cliquez sur l’icône de clé à molette pour ouvrir la boîte de dialogue Conteneur de formulaires adaptatifs afin de configurer une action d’envoi.](/help/forms/using/assets/adaptive-forms-submit-message.png)

1. Sélectionnez et configurez un **[!UICONTROL Action Envoyer]**, en fonction de vos besoins. Pour plus d’informations sur les actions d’envoi, voir [Action d’envoi de formulaire adaptatif](/help/forms/using/configuring-submit-actions.md)

<!--
    
    ![Click the Wrench icon to open Adaptive Form Container dialog box to configure Data Models for the Adaptive Form Container component](/help/forms/assets/adaptive-forms-container.png)

-->

## Rediriger l’utilisateur vers une page ou afficher un message de remerciement lors de l’envoi du formulaire

Lors de l’envoi d’un formulaire, vous pouvez rediriger l’utilisateur vers une autre page web ou un message. Pour rediriger l’utilisateur ou configurer le message de remerciement :

1. Ouvrez l’explorateur de contenu , puis sélectionnez l’option **[!UICONTROL Conteneur de guide]** du formulaire adaptatif.
1. Cliquez sur les propriétés du conteneur de guide. ![Propriétés du guide](/help/forms/using/assets/configure-icon.svg) icône . La boîte de dialogue Conteneur de formulaires adaptatifs s’ouvre.
1. Ouvrez le **[!UICONTROL Envoi]** .

   ![Cliquez sur l’icône de clé à molette pour ouvrir la boîte de dialogue Conteneur de formulaires adaptatifs afin de configurer une page de redirection ou un message de remerciement.](/help/forms/using/assets/adaptive-forms-submit-message.png)

   * Pour configurer une URL de redirection, sélectionnez l’option Lors de l’envoi . **[!UICONTROL Rediriger vers l’URL]** et recherchez et sélectionnez une page AEM Sites, ou fournissez l’URL d’une page externe.

   * Pour configurer un message de remerciement ou personnalisé, sélectionnez l’option Envoyer . **[!UICONTROL Afficher le message]** et indiquez un message dans la variable **[!UICONTROL Contenu du message]** de la boîte. Il s’agit d’une zone de texte enrichi. Vous pouvez utiliser l’option Plein écran pour afficher tous les éléments de texte enrichi disponibles.

## Configuration d’un schéma ou d’un modèle de données de formulaire pour un formulaire adaptatif {#configure-schema-or-data-model-for-form}

Vous pouvez utiliser le modèle de données de formulaire pour connecter un formulaire à une source de données afin d’envoyer et de recevoir des données en fonction des actions de l’utilisateur. Vous pouvez également connecter un formulaire à un schéma JSON pour recevoir les données envoyées dans un format prédéfini. Selon les besoins, connectez votre formulaire à un schéma JSON ou à un modèle de données de formulaire :

* [Création d’un schéma JSON et chargement dans votre environnement](/help/forms/using/adaptive-form-json-schema-form-model.md)
* [Création d’un modèle de données de formulaire](/help/forms/using/create-form-data-models.md)

### Configuration d’un schéma JSON ou d’un modèle de données de formulaire pour votre formulaire

Pour configurer un schéma JSON ou un modèle de données de formulaire pour votre formulaire :

1. Ouvrez l’explorateur de contenu , puis sélectionnez l’option **[!UICONTROL Conteneur de guide]** du formulaire adaptatif.
1. Cliquez sur les propriétés du conteneur de guide. ![Propriétés du guide](/help/forms/using/assets/configure-icon.svg) icône . La boîte de dialogue Conteneur de formulaires adaptatifs s’ouvre.
1. Ouvrez le **[!UICONTROL Modèle de données]** .

   ![Cliquez sur l’icône de clé à molette pour ouvrir la boîte de dialogue Conteneur de formulaires adaptatifs afin de configurer un schéma JSON ou un modèle de données de formulaire.](/help/forms/using/assets/adaptive-forms-select-form-data-model-or-json-schema.png)

1. Sélectionnez et configurez un schéma JSON ou un modèle de données de formulaire, en fonction de vos besoins :

   * Lorsque vous sélectionnez la variable **[!UICONTROL Modèle de formulaire]** , utilisez l’option **[!UICONTROL Sélectionner un modèle de données de formulaire]** pour sélectionner un modèle de données de formulaire préconfiguré.
   * Lorsque vous sélectionnez la variable **[!UICONTROL Schéma]** , utilisez l’option **[!UICONTROL Schéma]** pour sélectionner un schéma JSON pour votre formulaire.

1. Cliquez sur **[!UICONTROL Terminé]**.

## Configuration d’un service de préremplissage  {#configure-prefill-service-for-form}

Vous pouvez utiliser le service de préremplissage pour remplir automatiquement les champs d’un formulaire adaptatif à l’aide de données existantes. Lorsqu’un utilisateur ouvre un formulaire, les valeurs de ces champs sont préremplies. Vous pouvez :

* [Création d’un service de préremplissage personnalisé](/help/forms/using/prepopulate-adaptive-form-fields.md)
* [Utilisation du service de préremplissage de modèle de données de formulaire](#fdm-prefill-service)

### Utiliser le service de préremplissage de modèle de données de formulaire pour préremplir les champs d’un formulaire adaptatif {#fdm-prefill-service}

Vous pouvez utiliser le service de préremplissage de modèle de données de formulaire pour préremplir les champs d’un formulaire adaptatif à l’aide d’un modèle de données de formulaire ou d’un service de préremplissage personnalisé. Le service Form Data Model Prefill utilise la méthode [Obtention du service du modèle de données de formulaire configuré](work-with-form-data-model.md#add-data-model-objects-and-services-add-data-model-objects-and-services) pour récupérer des données. Pour utiliser le service de préremplissage de modèle de données de formulaire pour un formulaire adaptatif :

1. Ouvrez l’explorateur de contenu , puis sélectionnez l’option **[!UICONTROL Conteneur de guide]** du formulaire adaptatif.
1. Cliquez sur les propriétés du conteneur de guide. ![Propriétés du guide](/help/forms/using/assets/configure-icon.svg) icône . La boîte de dialogue Conteneur de formulaires adaptatifs s’ouvre.
1. Cliquez sur les propriétés du conteneur de formulaires adaptatifs . ![Propriétés Adaptive Form Container](/help/forms/using/assets/configure-icon.svg) icône . La boîte de dialogue Conteneur de formulaires adaptatifs pour configurer les modèles de données s’ouvre.
   ![Cliquez sur l’icône de clé à molette pour ouvrir la boîte de dialogue Conteneur de formulaires adaptatifs afin de configurer une page de redirection ou un message de remerciement.](/help/forms/using/assets/adaptive-forms-container-prefill-service.png)
1. Sélectionner un modèle de données de formulaire. Ouvrez le **[!UICONTROL De base]** . Dans le service de préremplissage, sélectionnez **[!UICONTROL Service de préremplissage de modèle de données de formulaire]**.
1. Cliquez sur **[!UICONTROL Terminé]**. Votre formulaire adaptatif est maintenant configuré pour utiliser le préremplissage du modèle de données de formulaire. Vous pouvez désormais utiliser la variable [éditeur de règles](rule-editor.md) pour créer des règles afin de préremplir les champs du formulaire.

## Modifier les propriétés du modèle de formulaire d’un formulaire adaptatif {#edit-form-model}

1. Sélectionnez le formulaire adaptatif et appuyez sur ![Informations sur la page](/help/forms/using/assets/configure-icon.svg) > **[!UICONTROL Ouvrir les propriétés]**. La page Propriétés du formulaire s’ouvre.

1. Accédez à l’onglet **[!UICONTROL Modèle de formulaire]** et choisissez un modèle de formulaire. Si le formulaire adaptatif est dépourvu de modèle de formulaire, vous avez la possibilité de choisir un schéma JSON ou un modèle de données de formulaire. D’autre part, si le formulaire adaptatif est déjà basé sur un modèle de formulaire, vous avez la possibilité de passer à un autre modèle de formulaire du même type. Par exemple, si le formulaire utilise un schéma JSON, vous pouvez facilement passer à un autre schéma JSON. De même, si le formulaire utilise un modèle de données de formulaire, vous pouvez passer à un autre modèle de données de formulaire.

1. Appuyez sur **[!UICONTROL Enregistrer]** pour enregistrer les propriétés.

## Prochaines étapes

* [Utilisation de l’éditeur de règles pour ajouter un comportement dynamique au formulaire](rule-editor.md)
* [Création ou personnalisation de thèmes pour Forms adaptatif basé sur les composants principaux](create-or-customize-themes-for-adaptive-forms-core-components.md)
* Création d’un modèle pour le Forms adaptatif basé sur les composants principaux

## Voir également

* [Création d’un formulaire adaptatif basé sur des composants principaux](create-an-adaptive-form-core-components.md)
* [Création ou ajout d’un formulaire adaptatif à une page AEM Sites ou à un fragment d’expérience](create-or-add-an-adaptive-form-to-aem-sites-page.md)

