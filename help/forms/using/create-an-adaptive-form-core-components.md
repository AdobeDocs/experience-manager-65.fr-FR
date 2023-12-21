---
title: Comment créer un formulaire adaptatif ?
description: Découvrez comment créer un formulaire adaptatif à l’aide de [!DNL Experience Manager Forms]. Les formulaires adaptatifs sont des formulaires HTML5 réactifs qui rationalisent la collecte et le traitement des informations. Découvrez comment créer un formulaire adaptatif basé sur un modèle de données de formulaire et un schéma XML ou JSON.
Keywords: create adaptive form core component, create core component based adaptive form, creare adaptive form
products: SG_EXPERIENCEMANAGER/6.5/FORMS
contentOwner: Khushwant Singh
topic-tags: Adaptive Forms
docset: aem65
role: Admin, Developer
feature: Adaptive Forms, Core Components
exl-id: ee596672-b0b5-42e9-a139-72f90287bf3b
source-git-commit: d85fc98d9a31bc4014aef4311ba0f838c7ef619a
workflow-type: tm+mt
source-wordcount: '1743'
ht-degree: 97%

---

# Créer un formulaire adaptatif basé sur des composants principaux {#creating-an-adaptive-form-core-components}


<span class="preview"> Adobe recommande d’utiliser les composants principaux pour [ajouter des formulaires adaptatifs à une page AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md) ou [créer des formulaires adaptatifs autonomes](/help/forms/using/create-an-adaptive-form-core-components.md). </span>

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Cliquez ici](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form-core-components.html?lang=fr) |
| AEM 6.5 | Cet article |

**S’applique à :** ✅ Composants principaux de formulaire adaptatif ❎ [Composants de base de formulaires adaptatifs](/help/forms/using/create-adaptive-form.md).

Les formulaires adaptatifs vous permettent de créer des formulaires attrayants, réactifs, dynamiques et adaptatifs. AEM Forms fournit une interface utilisateur conviviale pour les entreprises permettant de créer rapidement des formulaires adaptatifs. L’interface utilisateur assure une navigation rapide par onglets pour sélectionner facilement un modèle, un style, des champs et des options d’envoi préconfigurés afin de créer un formulaire adaptatif.

Avant de commencer, découvrez les types de composants de formulaires disponibles :

* [Composants principaux de formulaires adaptatifs](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=fr) : il s’agit de composants de capture de données normalisés. Ces composants offrent des fonctionnalités de personnalisation, un délai de développement réduit et de plus bas coûts de maintenance pour vos expériences d’inscription numérique. Un développeur ou une développeuse peut facilement personnaliser et mettre en forme ces composants. Adobe recommande d’utiliser ces composants modernes et extensibles pour développer le Forms adaptatif.

* [Composants de base des formulaires adaptatifs](creating-adaptive-form.md) : il s’agit de composants de capture de données classiques (anciens). Vous pouvez continuer à les utiliser pour modifier votre formulaire adaptatif existant basé sur les composants de base. Si vous créez des formulaires adaptatifs, Adobe recommande d’utiliser les [composants principaux de formulaires adaptatifs](/help/forms/using/create-adaptive-form.md).

## Conditions préalables

Pour créer un formulaire adaptatif, vous devez disposer des éléments suivants :

* **Activer des composants principaux de formulaires adaptatifs pour votre environnement** : le projet AEM Archetype version 41 ou ultérieure est requis pour [activer des composants principaux pour votre environnement](/help/forms/using/enable-adaptive-forms-core-components.md). Lors de l’activation des composants principaux pour votre environnement, le modèle **Formulaires adaptatifs (composant principal)** et le thème de la zone de travail sont ajoutés à votre environnement.

* **Modèle de formulaire adaptatif** : un modèle fournit une structure de base et définit l’aspect, c’est-à-dire la mise en page et les styles, d’un formulaire adaptatif. Il comporte des composants pré-formatés contenant certaines propriétés et une certaine structure de contenu. Il fournit également les options permettant de définir un thème et une action d’envoi. Le thème définit l’aspect et l’action d’envoi définit l’action à entreprendre lors de l’envoi d’un formulaire adaptatif. Vous pouvez également déployer des [exemples de modèles](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html?lang=fr) dans votre environnement. Vous pouvez ainsi créer rapidement des formulaires.

  >[!NOTE]
  >
  > Si vous n’avez pas le modèle **Formulaires adaptatifs (composant principal)** sur votre environnement, vous devez [activer les composants principaux des formulaires adaptatifs pour votre environnement](/help/forms/using/enable-adaptive-forms-core-components.md). Quand vous activez des composants principaux pour votre environnement, le modèle **Formulaires adaptatifs (composant principal)** est ajouté à votre environnement.

* **Un thème de formulaire adaptatif** : un thème contient des détails de style pour les composants et les panneaux. Ces styles incluent les propriétés telles que les couleurs d’arrière-plan, les couleurs d’état, la transparence, l’alignement et la taille. Lorsque vous appliquez un thème, le style spécifié se reflète sur les composants correspondants.  Le thème `Canvas` est ajouté par défaut lorsque vous activez les composants principaux pour votre environnement. Vous pouvez [télécharger et personnaliser les thèmes standard](create-or-customize-themes-for-adaptive-forms-core-components.md). Pour les thèmes **prêts à l’emploi**, vous pouvez déployer des [exemples de thèmes](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html?lang=fr) pour votre environnement. Cela permet de commencer la mise en forme de vos formulaires et fournit une structure de base pour créer ou personnaliser un thème en fonction des besoins de votre entreprise.

* **Autorisations** : ajoutez vos utilisateurs et utilisatrices au groupe [!DNL forms-users]. Les membres du groupe [!DNL forms-users] ont les autorisations de créer un formulaire adaptatif. Pour obtenir une liste détaillée des groupes d’utilisateurs et d’utilisatrices spécifiques aux formulaires, voir [Groupes et autorisations](forms-groups-privileges-tasks.md).

<!--
>[!NOTE]
>
>
> In addition to the given themes and templates when you enable Core Components, you can also deploy the latest out-of-the box [sample themes and templates](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html) to your AEM environment for use in Core Components based Adaptive Forms.
-->

## Créer un formulaire adaptatif {#create-an-adaptive-form}

1. Connectez-vous à votre [instance de création AEM](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html?lang=fr#author-and-publish-installs) locale.

1. Entrez vos informations d’identification sur la page de connexion d’Experience Manager. Une fois connecté, dans le coin supérieur gauche, sélectionnez **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms et documents]**.

1. Sélectionner **[!UICONTROL Créer]**  > **[!UICONTROL Créer un Forms adaptatif]**.

1. Sélectionnez un modèle de composant principal de formulaire adaptatif et cliquez sur **[!UICONTROL Suivant]**.

1. **[!UICONTROL Ajouter des propriétés]** s’affiche. Spécifiez les valeurs des champs de propriété suivants. Les champs Titre et Nom sont obligatoires :

   * **[!UICONTROL Titre]** : indique le nom d’affichage du formulaire. Le titre vous permet d’identifier le formulaire dans l’interface utilisateur [!DNL Experience Manager Forms] d’AEM Forms.
   * **[!UICONTROL Nom :]** indique le nom du formulaire. Un nœud portant le nom spécifié est créé dans le référentiel. Lorsque vous commencez à saisir un titre, la valeur du champ Nom est automatiquement générée. Vous pouvez modifier la valeur suggérée. Le champ Nom ne peut contenir que des caractères alphanumériques, des traits d’union et des traits de soulignement.
   * **[!UICONTROL Description :]** indique des informations détaillées relatives au formulaire.
   * **[!UICONTROL Bibliothèque cliente de thèmes] :** indique le thème d’un formulaire adaptatif. Par défaut, le thème `adaptiveform.theme.canvas3` est sélectionné. Vous pouvez également choisir un thème différent dans le menu déroulant **[!UICONTROL Bibliothèque cliente de thèmes]**.
   * **[!UICONTROL Conteneur de configuration :]** définit un emplacement où sont stockés les fichiers de configuration des formulaires adaptatifs. Ces fichiers de configuration contiennent des paramètres et des propriétés liés au comportement et à l’apparence des formulaires adaptatifs.
   * **[!UICONTROL Balises :]** indique les balises pour individualiser le formulaire adaptatif. Les balises aident à rechercher le formulaire. Pour créer des balises, saisissez les nouveaux noms de balise dans la boîte de dialogue **[!UICONTROL Balises.]**
1. Sélectionnez **[!UICONTROL Créer]**. Un formulaire adaptatif est créé et une boîte de dialogue pour ouvrir le formulaire à modifier s’affiche.


1. Sélectionner **[!UICONTROL Modifier]** pour ouvrir le formulaire nouvellement créé dans un nouvel onglet. Le formulaire s’ouvre pour être modifié et affiche le contenu disponible dans le modèle. Il affiche également la barre latérale permettant de personnaliser le formulaire nouvellement créé.


## Utiliser des composants principaux des formulaires adaptatifs pour créer votre formulaire

Après avoir ouvert le formulaire pour le modifier, vous pouvez utiliser les composants principaux disponibles des formulaires adaptatifs pour ajouter des champs de formulaire à votre formulaire. Vous pouvez faire glisser les composants et les déposer ou utiliser l’option + [insérer le composant] pour ajouter ces composants à un formulaire. Pour en savoir plus sur les [composants principaux disponibles des formulaires adaptatifs](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=fr#components), reportez-vous à la documentation des composants principaux d’AEM. Vous pouvez également consulter [https://aemcomponents.dev/](https://aemcomponents.dev/) pour afficher les composants principaux disponibles en action.

## Configurer l’action Envoyer pour un formulaire adaptatif {#configure-submit-action-for-form}

Une action Soumettre vous permet de choisir la destination des données capturées via un formulaire adaptatif. Elle est déclenchée lorsqu’un utilisateur ou une utilisatrice clique sur le bouton Soumettre d’un formulaire adaptatif. Les formulaires adaptatifs incluent certaines actions de soumission prêtes à l’emploi. Vous pouvez également étendre les actions de soumission par défaut pour créer votre propre action de soumission. Pour configurer une action de soumission pour votre formulaire :

1. Ouvrez l’explorateur de contenu, puis sélectionnez le composant **[!UICONTROL Conteneur de guide]** de votre formulaire adaptatif.
1. Cliquez sur l’icône des propriétés du conteneur de guide ![Propriétés du guide](/help/forms/using/assets/configure-icon.svg). La fenêtre du conteneur de formulaires adaptatifs s’ouvre.

1. Cliquez sur l’onglet **[!UICONTROL Envoi]**.

   ![Cliquez sur l’icône de clé à molette pour ouvrir la boîte de dialogue Conteneur de formulaires adaptatifs afin de configurer une action d’envoi.](/help/forms/using/assets/adaptive-forms-submit-message.png)

1. Sélectionnez et configurez une **[!UICONTROL action d’envoi]** en fonction de vos besoins. Pour plus d’informations sur les actions d’envoi, voir [Action d’envoi de formulaire adaptatif](/help/forms/using/configuring-submit-actions.md)

<!--
    
    ![Click the Wrench icon to open Adaptive Form Container dialog box to configure Data Models for the Adaptive Form Container component](/help/forms/assets/adaptive-forms-container.png)

-->

## Rediriger l’utilisateur ou l’utilisatrice vers une page ou afficher un message de remerciement lors de l’envoi du formulaire

Lors de la soumission d’un formulaire, vous pouvez rediriger la personne utilisatrice vers une autre page web ou un message. Pour rediriger la personne utilisatrice ou configurer le message de remerciement :

1. Ouvrez l’explorateur de contenu, puis sélectionnez le composant **[!UICONTROL Conteneur de guide]** de votre formulaire adaptatif.
1. Cliquez sur l’icône des propriétés du conteneur de guide ![Propriétés du guide](/help/forms/using/assets/configure-icon.svg). La fenêtre du conteneur de formulaires adaptatifs s’ouvre.
1. Ouvrez l’onglet **[!UICONTROL Envoi]**.

   ![Cliquez sur l’icône de clé à molette pour ouvrir la boîte de dialogue Conteneur de formulaires adaptatifs afin de configurer une page de redirection ou un message de remerciement.](/help/forms/using/assets/adaptive-forms-submit-message.png)

   * Pour configurer une URL de redirection, pour l’option Lors de l’envoi, sélectionnez l’option **[!UICONTROL Rediriger vers l’URL]**, puis parcourez et sélectionnez une page AEM Sites, ou fournissez l’URL d’une page externe.

   * Pour configurer un message de remerciement ou personnalisé, sélectionnez l’option **[!UICONTROL Afficher le message]** et écrivez un message dans la zone **[!UICONTROL Contenu du message]** pour l’option Lors de l’envoi. Il s’agit d’une zone de texte enrichi. Vous pouvez utiliser l’option Plein écran pour afficher tous les éléments de texte enrichi disponibles.

## Configurer un schéma ou un modèle de données de formulaire pour un formulaire adaptatif {#configure-schema-or-data-model-for-form}

Vous pouvez utiliser le modèle de données de formulaire pour connecter un formulaire à une source de données afin d’envoyer et de recevoir des données en fonction des actions de l’utilisateur ou de l’utilisatrice. Vous pouvez également connecter un formulaire à un schéma JSON pour recevoir les données envoyées dans un format prédéfini. Selon les besoins, connectez votre formulaire à un schéma JSON ou à un modèle de données de formulaire :

* [Créer un schéma JSON et le charger dans votre environnement](/help/forms/using/adaptive-form-json-schema-form-model.md)
* [Créer un modèle de données de formulaire](/help/forms/using/create-form-data-models.md)

### Configurer un schéma JSON ou un modèle de données de formulaire pour votre formulaire

Pour configurer un schéma JSON ou un modèle de données de formulaire pour votre formulaire :

1. Ouvrez l’explorateur de contenu, puis sélectionnez le composant **[!UICONTROL Conteneur de guide]** de votre formulaire adaptatif.
1. Cliquez sur l’icône des propriétés du conteneur de guide ![Propriétés du guide](/help/forms/using/assets/configure-icon.svg). La fenêtre du conteneur de formulaires adaptatifs s’ouvre.
1. Ouvrez l’onglet **[!UICONTROL Modèle de données]**.

   ![Cliquez sur l’icône de clé à molette pour ouvrir la boîte de dialogue Conteneur de formulaires adaptatifs afin de configurer un schéma JSON ou un modèle de données de formulaire.](/help/forms/using/assets/adaptive-forms-select-form-data-model-or-json-schema.png)

1. Sélectionnez et configurez un schéma JSON ou un modèle de données de formulaire, en fonction de vos besoins :

   * Lorsque vous sélectionnez l’option **[!UICONTROL Modèle de formulaire]**, utilisez l’option **[!UICONTROL Sélectionner un modèle de données de formulaire]** pour sélectionner un modèle de données de formulaire préconfiguré.
   * Lorsque vous sélectionnez l’option **[!UICONTROL Schéma]**, utilisez l’option **[!UICONTROL Schéma]** pour sélectionner un schéma JSON pour votre formulaire.

1. Cliquez sur **[!UICONTROL Terminé]**.

>[!NOTE]
>
> Vous pouvez modifier le schéma JSON ou le modèle de données de formulaire pour un formulaire adaptatif à l’aide des propriétés du conteneur de guide.

## Configurer un service de préremplissage  {#configure-prefill-service-for-form}

Vous pouvez utiliser le service de préremplissage pour remplir automatiquement les champs d’un formulaire adaptatif à l’aide de données existantes. Lorsqu’un utilisateur ou une utilisatrice ouvre un formulaire, les valeurs de ces champs sont préremplies. Vous pouvez effectuer les actions suivantes :

* [Créer un service de préremplissage personnalisé](/help/forms/using/prepopulate-adaptive-form-fields.md)
* [Utiliser le service de préremplissage de modèle de données de formulaire](#fdm-prefill-service)

### Utiliser le service de préremplissage de modèle de données de formulaire pour préremplir les champs d’un formulaire adaptatif {#fdm-prefill-service}

Vous pouvez utiliser le service de préremplissage de modèle de données de formulaire pour préremplir les champs d’un formulaire adaptatif à l’aide d’un modèle de données de formulaire ou d’un service de préremplissage personnalisé. Le service de préremplissage de modèle de données de formulaire utilise la méthode [Obtenir le service du modèle de données de formulaire configuré](work-with-form-data-model.md#add-data-model-objects-and-services-add-data-model-objects-and-services) pour récupérer des données. Pour utiliser le service de préremplissage de modèle de données de formulaire pour un formulaire adaptatif :

1. Ouvrez l’explorateur de contenu, puis sélectionnez le composant **[!UICONTROL Conteneur de guide]** du formulaire adaptatif.
1. Cliquez sur l’icône des propriétés du conteneur de guide ![Propriétés du guide](/help/forms/using/assets/configure-icon.svg). La fenêtre du conteneur de formulaires adaptatifs s’ouvre.
1. Cliquez sur l’icône de propriétés de conteneur de formulaires adaptatifs ![propriétés de conteneur de formulaires adaptatifs](/help/forms/using/assets/configure-icon.svg). La boîte de dialogue Conteneur de formulaires adaptatifs pour configurer les modèles de données s’ouvre.
   ![Cliquez sur l’icône de clé à molette pour ouvrir la boîte de dialogue Conteneur de formulaires adaptatifs afin de configurer une page de redirection ou un message de remerciement.](/help/forms/using/assets/adaptive-forms-container-prefill-service.png)
1. Sélectionnez un modèle de données de formulaire. Ouvrez l’onglet **[!UICONTROL De base]**. Dans le service de préremplissage, sélectionnez **[!UICONTROL Service de préremplissage de modèle de données de formulaire]**.
1. Cliquez sur **[!UICONTROL Terminé]**. Votre formulaire adaptatif est maintenant configuré pour utiliser le préremplissage du modèle de données de formulaire. Vous pouvez désormais utiliser l’[éditeur de règles](rule-editor.md) pour créer des règles afin de préremplir les champs du formulaire.

<!--
## Edit Form Model properties of an Adaptive Form {#edit-form-model}

1. Select the Adaptive Form and select ![Page information](/help/forms/using/assets/configure-icon.svg) > **[!UICONTROL Open Properties]**. The Form Properties page opens. 

1. Go to the **[!UICONTROL Form Model]** tab and choose a form model. If the Adaptive Form is without a form model, you have the freedom to choose either a JSON schema or a form data model. On the other hand, if the Adaptive Form is already based on a form model, you have the option to switch to another form model of the same type. For instance, if the form is using a JSON schema, you can easily switch to another JSON schema, and similarly if the form is using a Form Data Model, you can switch to another Form Data Model. 

1. Select **[!UICONTROL Save]** to save the properties.
-->

## Prochaines étapes

* [Utiliser l’éditeur de règles pour ajouter un comportement dynamique au formulaire](rule-editor.md)
* [Créer ou personnaliser des thèmes pour les formulaires adaptatifs basés sur les composants principaux](create-or-customize-themes-for-adaptive-forms-core-components.md)


## Voir également

* [Création d’un formulaire adaptatif basé sur des composants principaux](create-an-adaptive-form-core-components.md)
* [Création ou ajout d’un formulaire adaptatif à une page AEM Sites ou à un fragment d’expérience](create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [Exemples de modèles de thèmes et de modèles de données de formulaire](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html?lang=fr)
