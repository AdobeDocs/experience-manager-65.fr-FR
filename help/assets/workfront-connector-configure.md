---
title: Configuration d’ [!DNL Workfront for Experience Manager enhanced connector]
description: Configuration d’ [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Integrations
source-git-commit: 468a8d96153c67232524eea6f180c9ceb364d60a
workflow-type: tm+mt
source-wordcount: '1635'
ht-degree: 0%

---


# Configuration d’[!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

Un utilisateur disposant d’un accès administrateur dans [!DNL Adobe Experience Manager] configure le connecteur amélioré après son installation. Pour obtenir des instructions d’installation, voir [Installation du connecteur](/help/assets/workfront-integrations.md).

>[!IMPORTANT]
>
>L’Adobe nécessite le déploiement et la configuration de [!DNL Adobe Workfront for Experience Manager enhanced connector] uniquement par le biais de partenaires certifiés ; [!DNL Adobe Professional Services]. Si elles sont déployées et configurées sans partenaire certifié ou [!DNL Adobe Professional Services], il n’est pas pris en charge par Adobe.
>
>Adobe peut mettre à jour les [!DNL Adobe Workfront] et [!DNL Adobe Experience Manager] qui rend ce connecteur redondant ; si cela se produit, les clients peuvent être tenus de passer de l’utilisation de ce connecteur.

## Configuration des abonnements aux événements {#event-subscriptions}

Les abonnements aux événements sont utilisés pour informer les AEM des événements qui se produisent dans [!DNL Adobe Workfront]. Il y a trois [!DNL Workfront for Experience Manager enhanced connector] fonctionnalités qui ont besoin d’abonnements à des événements pour fonctionner :

* Création automatique de dossiers liés au projet.
* Synchronisation des modifications dans Workfront documente les valeurs de formulaire personnalisées pour AEM métadonnées de ressource.
* Publication automatique des ressources dans Brand Portal à la fin du projet.

Pour utiliser ces fonctionnalités, activez les abonnements aux événements.

* Modifier [!UICONTROL Outils Workfront] Configuration de Cloud Services que vous avez créée à l’étape 5 et sélectionnez [!UICONTROL Abonnements à un événement] .
* Sélectionnez la [!UICONTROL Intégration personnalisée Workfront] vous avez créé dans la section 6.
* Cliquez sur [!UICONTROL Activation des abonnements à des événements Workfront].

   ![Inscription d’événement](/help/assets/assets/event-subs.png)

## Configuration des dossiers liés {#linked-folders}

Pour vous abonner aux événements, procédez comme suit :

1. Accédez au **[!UICONTROL Abonnements à un événement]** dans les services cloud.
1. Sélectionnez l’intégration personnalisée créée dans [!DNL Workfront].
1. Cliquez sur **[!UICONTROL Activation des abonnements à des événements Workfront]**.

### Configuration de la structure de dossiers liée {#linked-folder-structure}

1. Accédez à l’onglet Dossiers liés au projet dans les services cloud.
1. Chemin d’accès parent du dossier lié : Sélectionnez un dossier dans la gestion des actifs numériques où vous souhaitez créer les dossiers liés. Si ce paramètre n’est pas renseigné, il est défini par défaut sur /content/dam. Assurez-vous que le schéma de métadonnées des outils Workfront et le schéma de métadonnées du dossier lié Workfront ont été appliqués au dossier sélectionné.
1. Structure de dossiers liée : Entrez des valeurs séparées par des virgules. Chaque valeur doit être `DE:<some-project-custom-form-field>`, Portfolio, Programme, Année, Nom ou une &quot;valeur de chaîne littérale&quot; (cette dernière avec des guillemets). Elle est actuellement définie sur Portfolio,Program,Year,DE:Project Type,Name.
1. Créez le titre du dossier lié dans Workfront à l’aide de la case à cocher Noms de structure de dossiers doit être cochée si le titre du dossier dans Workfront doit inclure tous les dossiers de la structure. Sinon, il s’agira du titre du dernier dossier.
1. Le multichamp Sous-dossiers permet de spécifier une liste de dossiers à créer en tant que dossier enfant du dossier lié.
1. État du projet : Sélectionnez l’état sur lequel le projet doit être défini pour créer le dossier lié.
1. Créez un dossier lié dans les projets avec un portfolio : Liste des Portfolios auxquels le projet doit appartenir pour créer le dossier lié. Laissez cette liste vide pour créer le dossier lié pour l’ensemble du portefeuille de projets.
1. Créez un dossier lié dans les projets avec un champ de formulaire personnalisé : Champ de formulaire personnalisé et valeur correspondante que le projet doit avoir pour créer le dossier lié. Cette configuration sera ignorée si elle n’est pas renseignée. Sélectionner `CUSTOM FORMS: Create DAM Linked Folder` pour le champ et la saisie `Yes` pour la valeur .
1. Cliquez sur Activer la création automatique de dossiers liés. Si vous revenez à l’onglet Abonnements à l’événement , un événement de création est désormais disponible.

![configuration des dossiers liés](/help/assets/assets/wf-linked-folder-config.png)

## Mappage du schéma de métadonnées {#metadata-schema-mapping}

### Configuration du mappage des métadonnées de dossier {#folder-metadata-mapping}

Le mappage des métadonnées entre les projets Workfront et les dossiers AEM est défini dans AEM Schémas de métadonnées de dossier. Les schémas de métadonnées de dossier doivent être créés et configurés comme vous le faites habituellement dans AEM. Workfront Tools ajoute une liste déroulante de saisie automatique à l’onglet Configuration des paramètres de chaque champ de formulaire de schéma de métadonnées de dossier. Ce menu déroulant de saisie automatique vous permet de spécifier le champ Workfront auquel chaque propriété AEM dossier doit être mappée.

Pour configurer les mappages, procédez comme suit :

1. Accédez à **[!UICONTROL Outils]** > **[!UICONTROL Ressources]** > **[!UICONTROL Schémas de métadonnées de dossier]**.
1. Sélectionnez le formulaire de schéma de métadonnées de dossier à modifier, puis cliquez sur Modifier.
1. Sélectionnez le champ de formulaire de schéma de métadonnées de dossier que vous souhaitez modifier, puis sélectionnez l’onglet Paramètres dans le panneau de droite.
1. Dans [!UICONTROL Mappé à partir du champ Workfront] , sélectionnez le nom du champ Workfront que vous souhaitez mapper à la propriété de dossier AEM sélectionnée. Les options disponibles sont les suivantes :

   * Champs de formulaire personnalisé du projet
   * Champs de présentation du projet (ID, nom, description, numéro de référence, date d’achèvement prévue, propriétaire du projet, parrain du projet, Portfolio ou programme)

![configuration du mappage des métadonnées](/help/assets/assets/wf-metadata-mapping-config2.png)

### Configuration du mappage des métadonnées des ressources {#asset-metadata-mapping}

Le mappage des métadonnées entre les documents Adobe Workfront et les ressources est défini dans les schémas de métadonnées AEM. Les schémas de métadonnées doivent être créés et configurés comme vous le faites habituellement dans AEM. Les outils Workfront ajoutent des options de configuration à l’onglet Configuration des paramètres de chaque champ de formulaire de schéma de métadonnées. Ces options vous permettent de spécifier le champ Workfront auquel chaque propriété AEM doit être mappée.

Pour configurer les mappages, procédez comme suit :

1. Accédez à **Outils** > **Ressources** > **Schémas de métadonnées**.
1. Sélectionnez le formulaire de schéma de métadonnées à modifier, puis cliquez sur **Modifier** ou créer entièrement un nouveau schéma de métadonnées.
1. Sélectionnez le champ de formulaire de schéma de métadonnées que vous souhaitez modifier et sélectionnez **Paramètres** dans le panneau de droite.
1. Dans [!DNL Workfront] Champ de formulaire personnalisé : sélectionnez le nom du champ [!DNL Workfront] champ que vous souhaitez mapper à la propriété AEM sélectionnée. Les options disponibles sont les suivantes :

   * Document des champs de formulaire personnalisés
   * Champs de formulaire personnalisé du projet
   * Émission de champs de formulaire personnalisés
   * Tâche des champs de formulaire personnalisés
   * Champs de présentation du projet (ID, nom, description ou numéro de référence)

1. Dans le cas où la variable [!DNL Workfront] champ sélectionné dans [!UICONTROL Champ de formulaire personnalisé Workfront] est un champ de type Utilisateur Workfront , il sera nécessaire de spécifier le champ Utilisateur Workfront que vous souhaitez mapper. Pour ce faire, cochez la case Obtenir la valeur du champ d’objet référencé de Workfront , puis indiquez le nom de la variable [!UICONTROL Champ de formulaire personnalisé Workfront User] à partir de laquelle récupérer la valeur à mapper.

   ![configuration du mapping de métadonnées](/help/assets/assets/wf-metadata-mapping-config1.png)

## Propriété de mappage {#map-property}

Cette étape de processus permet à l’utilisateur de mapper une propriété à une [!DNL Workfront] formulaire personnalisé sur un projet, une tâche, un problème ou un document. Le [!DNL Workfront] artefact cette étape affecte est recherché à l’aide d’un chemin relatif à partir de la payload. Les propriétés à mapper sont contrôlées à partir de la configuration de la boîte de dialogue des étapes.

**Type**: Ce champ vous permet de sélectionner le type d’objet Workfront auquel les propriétés doivent être mappées.

**Propriété d’ID**: Ce champ vous permet de spécifier le chemin d’accès à l’identifiant de l’objet Workfront auquel les propriétés doivent être mappées. Le chemin spécifié dans ce champ doit être relatif à la charge utile du workflow.

**Attributs de propriété**: Ce multichamp permet de spécifier les mappages entre les propriétés AEM et les champs Workfront. Chaque élément du champ multiple spécifie un mappage. Chaque mappage doit avoir le format . `<workfront-field>=<aem-mapped-property>`.

* Le `workfront-field` peut être

   * Champ de formulaire personnalisé identifié par le préfixe `DE:`.
   * Champ modifiable identifié par son nom. Les noms des champs se trouvent dans [[!DNL Workfront] Explorateur d’API](https://experience.workfront.com/s/api-explorer).

* Le `aem-mapped-property` peut être :

   * Une valeur littérale. Ils doivent être entourés de guillemets.
   * Une propriété AEM. Cette référence doit être relative à la charge utile du workflow.
   * Une valeur nommée. Ils doivent être entourés de crochets.
   * Une concaténation des 3 éléments ci-dessus. Spécifiez-le à l’aide de `{+}`.
   * Modification des 3 éléments ci-dessus en entourant la valeur avec `{replace(<value>,”old-char”,”new-char”)}`.

* Voici quelques exemples :

   * `status="INP"`
   * `DE:Asset Type=jcr:content/metadata/assetType`
   * `DE:Path={path}`
   * `URL=”https://my-aem-author/assets.html”{+}{path}`

![Configuration de la propriété de mappage](/help/assets/assets/wf-map-property-config.png)

## Définir le statut {#set-status}

Dans l’éditeur de workflow, modifiez les propriétés de **[!UICONTROL Workfront - Définir l’état]** dans le **[!UICONTROL Arguments]** .

![Modifier le workflow pour définir le statut](/help/assets/assets/wf-set-status.png)

## Synchronisation des commentaires {#comments-sync}

1. Dans [!DNL Experience Manager], accès **[!UICONTROL Outils]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configuration des outils Workfront]**, sélectionnez la configuration, puis **[!UICONTROL Propriétés]**.

   ![synchronisation des commentaires](/help/assets/assets/comments-sync1.png)

1. Sélectionner **[!UICONTROL Abonnements à un événement]** , cliquez sur **[!UICONTROL Activation de la synchronisation des commentaires]** on **[!UICONTROL Envoi des commentaires effectués dans Workfront vers AEM]** .

   ![La synchronisation est activée](/help/assets/assets/wf-comment-sync-enabled.png)

Pour tester la synchronisation des commentaires de Workfront vers AEM, procédez comme suit :

1. Accédez à un document lié dans Workfront et ajoutez un commentaire dans l’onglet Mises à jour .

   ![laisser un commentaire dans Workfront](/help/assets/assets/comments-sync2.png)

1. Accédez au même document lié dans AEM, sélectionnez le document et ouvrez le [!UICONTROL Chronologie] dans le volet de navigation de gauche, puis sélectionnez [!UICONTROL Commentaires]. La barre latérale gauche affiche les commentaires synchronisés à partir de [!DNL Workfront].

## Versions des ressources {#asset-versions}

Pour conserver l’historique des versions des ressources dans AEM, configurez le contrôle de version des ressources dans AEM.

1. Dans Experience Manager, accédez à **[!UICONTROL Outils]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configuration des outils Workfront]**, puis ouvrez le **[!UICONTROL Avancé]** .

1. Option Sélectionner **[!UICONTROL Stocker les ressources portant le même nom que les versions de la ressource existante]**. Lorsque cette option est cochée, elle permet de stocker les ressources chargées avec le même nom et au même emplacement que la version de la ressource existante. Si cette option n’est pas cochée, une nouvelle ressource est créée avec un nom différent (par exemple, `asset-name.pdf` et `asset-name-1.pdf`).

1. Option Sélectionner **[!UICONTROL Mise à jour des métadonnées de ressource lors de la création d’une version]**. Lorsque cette option est cochée, les métadonnées de la ressource sont mises à jour chaque fois qu’une nouvelle version de la ressource est créée. Si cette option n’est pas cochée, la ressource conserve les métadonnées qu’elle possédait avant de créer la nouvelle version.

![configuration du contrôle de version des ressources](/help/assets/assets/wf-config-versioning.png)

>[!NOTE]
>
>Le contrôle de version n’est pas pris en charge dans les dossiers liés. Lors de la création d’un [!DNL Workfront] BAT avec un document dans un dossier lié, les commentaires et annotations de la version précédente de la ressource sont supprimés.

## Joindre des formulaires personnalisés {#attach-custom-forms}

Cette étape de processus permet aux utilisateurs de joindre un formulaire personnalisé à une [!DNL Workfront] artefact. Cette étape de workflow peut être ajoutée à n’importe quel modèle de workflow. Le [!DNL Workfront] artefact, cette étape affecte sera recherchée à l’aide d’un chemin relatif à partir de la payload.

Dans l’éditeur de workflow de Experience Manager, modifiez les propriétés de la variable [!UICONTROL Workfront - Joindre un formulaire personnalisé] workflow .

![formulaires personnalisés](/help/assets/assets/wf-custom-forms.png).

## Publication automatique de ressources {#auto-publish-assets}

1. Dans Experience Manager, accédez à **[!UICONTROL Outils]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configuration des outils Workfront]**, puis ouvrez le **[!UICONTROL Avancé]** .

1. Sélectionner **[!UICONTROL Publier automatiquement les ressources lorsqu’elles sont envoyées depuis Workfront]**. Cette option permet la publication automatique des ressources lorsqu’elles sont envoyées de Workfront vers AEM. Cette fonction peut être activée de manière conditionnelle en spécifiant un champ de formulaire personnalisé Workfront et la valeur sur laquelle elle doit être définie. Chaque fois qu’un document est envoyé à AEM, s’il satisfait à la condition, la ressource est automatiquement publiée.

1. Sélectionner **[!UICONTROL Publier toutes les ressources du projet sur Brand Portal à la fin du projet]**. Cette option permet la publication automatique des ressources sur [!DNL Brand Portal] lorsque l’état du projet Workfront auquel ils appartiennent est modifié en `Complete`.

![configuration de la publication automatique](/help/assets/assets/wf-auto-publish-config.png)

## Mises à jour de formulaires personnalisés du document Workfront {#subscribe-workfront-doc-custom-form-updates}

Pour vous abonner aux modifications de [!DNL Workfront] Document, formulaires personnalisés, sélectionnez l’option appropriée dans la **[!UICONTROL Avancé]** . Lorsque vous vous abonnez à ces mises à jour, elles mettent à jour votre mappage. [!DNL Experience Manager] les champs de métadonnées lorsque le champ correspondant dans [!DNL Workfront] Le formulaire personnalisé du document a été modifié.

![Configuration des mises à jour de formulaires personnalisées du document Workfront [!DNL Experience Manager]](/help/assets/assets/wf-custom-form-update.png)
