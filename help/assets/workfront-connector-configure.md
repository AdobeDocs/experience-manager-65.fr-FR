---
title: Configuration de  [!DNL Workfront for Experience Manager enhanced connector]
description: Configuration de  [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Integrations
exl-id: 2660de7c-0281-4884-98d9-e78f20cf571c
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '1737'
ht-degree: 100%

---

# Configuration de [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Cliquez ici](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/integrations/workfront-connector-configure.html?lang=fr) |
| AEM 6.5 | Cet article |

Un utilisateur disposant d’un accès administrateur dans [!DNL Adobe Experience Manager] configure le connecteur amélioré après son installation. Pour obtenir des instructions d’installation, consultez la section [Installation du connecteur](/help/assets/workfront-integrations.md).

>[!IMPORTANT]
>
>* Adobe nécessite le déploiement et la configuration de [!DNL Adobe Workfront for Experience Manager enhanced connector] uniquement par le biais de partenaires certifiés ou [!DNL Adobe Professional Services]. S’il est déployé et configuré sans partenaire certifié ou sans [!DNL Adobe Professional Services], il n’est pas pris en charge par Adobe.
>
>* Adobe peut publier des mises à jour d’[!DNL Adobe Workfront] et d’[!DNL Adobe Experience Manager] qui rendent ce connecteur redondant ; si cela se produit, les clients peuvent être amenés à cesser d’utiliser ce connecteur.
>
>* Adobe prend en charge les versions 1.7.4 et supérieures du connecteur. Les versions précédentes et personnalisées ne sont pas prises en charge. Pour vérifier la version améliorée du connecteur, accédez au groupe `digital.hoodoo` disponible dans le volet de gauche du [Gestionnaire de packages](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=fr).
>
>* Consultez la section [Examen de certification des partenaires pour Workfront pour le connecteur amélioré Experience Manager Assets](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). Pour plus d’informations sur l’examen, consultez le [Guide d’examen](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).


## Configuration des abonnements aux événements {#event-subscriptions}

Les abonnements aux événements sont utilisés pour informer AEM des événements qui se produisent dans [!DNL Adobe Workfront]. Il existe trois fonctionnalités [!DNL Workfront for Experience Manager enhanced connector] qui nécessitent des abonnements aux événements pour fonctionner :

* Création automatique de dossiers liés au projet.
* Synchronisation des modifications des valeurs des formulaires personnalisés du document Workfront avec les métadonnées des ressources AEM.
* Publication automatique des ressources dans Brand Portal à la fin du projet.

Pour utiliser ces fonctionnalités, activez les abonnements aux événements.

* Modifiez la configuration Cloud Services des [!UICONTROL outils Workfront] que vous avez créée à l’étape 5 et sélectionnez l’onglet [!UICONTROL Abonnements aux événements].
* Sélectionnez l’[!UICONTROL intégration personnalisée Workfront] que vous avez créée dans la section 6.
* Cliquez sur [!UICONTROL Activation des abonnements aux événements Workfront].

   ![Abonnement à un événement](/help/assets/assets/event-subs.png)

## Configuration des dossiers liés {#linked-folders}

Pour vous abonner aux événements, procédez comme suit :

1. Accédez à l’onglet **[!UICONTROL Abonnements aux événements]** dans les services cloud.
1. Sélectionnez l’intégration personnalisée créée dans [!DNL Workfront].
1. Cliquez sur **[!UICONTROL Activation des abonnements aux événements Workfront]**.

### Configuration de la structure de dossiers liés {#linked-folder-structure}

1. Accédez à l’onglet Dossiers liés au projet dans les services cloud.
1. Chemin d’accès parent du dossier lié : sélectionnez un dossier dans la gestion des ressources numériques (DAM) où vous souhaitez créer les dossiers liés. Si ce paramètre n’est pas renseigné, il est défini par défaut sur /content/dam. Assurez-vous que le schéma de métadonnées des outils Workfront et le schéma de métadonnées du dossier Dossier lié Workfront ont été appliqués au dossier sélectionné.
1. Structure de dossiers liés : entrez des valeurs séparées par des virgules. Chaque valeur doit être `DE:<some-project-custom-form-field>`, Portfolio, Programme, Année, Nom ou une « valeur de chaîne littérale » (cette dernière avec des guillemets). Elle est actuellement définie sur Portfolio,Program,Year,DE:Project Type,Name.
1. Créez le titre du dossier lié dans Workfront à l’aide de la case à cocher Noms de structure de dossiers doit être cochée si le titre du dossier dans Workfront doit inclure tous les dossiers de la structure. Sinon, il s’agira du titre du dernier dossier.
1. Le multichamp Sous-dossiers permet de spécifier une liste de dossiers à créer en tant que dossier enfant du dossier lié.
1. État du projet : sélectionnez l’état sur lequel le projet doit être défini pour créer le dossier lié.
1. Créez un dossier lié dans les projets avec un portfolio : liste des Portfolios auxquels le projet doit appartenir pour créer le dossier lié. Laissez cette liste vide pour créer le dossier lié pour l’ensemble du portefeuille de projets.
1. Créez un dossier lié dans les projets avec un champ de formulaire personnalisé : champ de formulaire personnalisé et valeur correspondante que le projet doit avoir pour créer le dossier lié. Cette configuration sera ignorée si elle n’est pas renseignée. Sélectionnez `CUSTOM FORMS: Create DAM Linked Folder` pour le champ et saisissez `Yes` pour la valeur.
1. Cliquez sur Activer la création automatique de dossiers liés. Si vous revenez à l’onglet Abonnements aux événements, un événement de création est désormais disponible.

![configuration des dossiers liés](/help/assets/assets/wf-linked-folder-config.png)

## Mappage du schéma de métadonnées {#metadata-schema-mapping}

### Configuration du mappage des métadonnées de dossier {#folder-metadata-mapping}

Le mappage des métadonnées entre les projets Workfront et les dossiers AEM est défini dans les schémas de métadonnées de dossier AEM. Les schémas de métadonnées de dossier doivent être créés et configurés comme vous le faites habituellement dans AEM. Les outils Workfront ajoutent une liste déroulante de saisie automatique à l’onglet Configuration des paramètres de chaque champ de formulaire de schéma de métadonnées de dossier. Ce menu déroulant de saisie automatique vous permet de spécifier le champ Workfront auquel chaque propriété de dossier AEM doit être mappée.

Pour configurer les mappages, procédez comme suit :

1. Accédez à **[!UICONTROL Outils]** > **[!UICONTROL Ressources]** > **[!UICONTROL Schémas de métadonnées de dossier]**.
1. Sélectionnez le formulaire de schéma de métadonnées de dossier que vous souhaitez modifier, puis cliquez sur Modifier.
1. Sélectionnez le champ de formulaire de schéma de métadonnées de dossier que vous souhaitez modifier, puis sélectionnez l’onglet Paramètres dans le panneau de droite.
1. Dans le champ [!UICONTROL Mappé depuis le champ Workfront], sélectionnez le nom du champ Workfront que vous souhaitez mapper à la propriété du dossier AEM sélectionné. Les options disponibles sont les suivantes :

   * Champs de formulaire personnalisé du projet
   * Champs de présentation du projet (ID, nom, description, numéro de référence, date d’achèvement prévue, propriétaire du projet, parrain du projet, Portfolio ou programme)

![configuration du mappage des métadonnées](/help/assets/assets/wf-metadata-mapping-config2.png)

### Configuration du mappage des métadonnées des ressources {#asset-metadata-mapping}

Le mappage des métadonnées entre les documents Adobe Workfront et les ressources est défini dans les schémas de métadonnées AEM. Les schémas de métadonnées doivent être créés et configurés comme vous le faites habituellement dans AEM. Les outils Workfront ajoutent des options de configuration à l’onglet Configuration des paramètres de chaque champ de formulaire de schéma de métadonnées. Ces options vous permettent de spécifier le champ Workfront auquel chaque propriété AEM doit être mappée.

Pour configurer les mappages, procédez comme suit :

1. Accédez à **Outils** > **Ressources** > **Schémas de métadonnées**.
1. Sélectionnez le formulaire du schéma de métadonnées que vous souhaitez modifier, puis cliquez sur **Modifier** ou créez un schéma de métadonnées entièrement nouveau.
1. Sélectionnez le champ de formulaire de schéma de métadonnées que vous souhaitez modifier, puis sélectionnez l’onglet **Paramètres** dans le panneau de droite.
1. Dans Champ de formulaire personnalisé [!DNL Workfront], sélectionnez le nom du champ [!DNL Workfront] que vous souhaitez mapper à la propriété AEM sélectionnée. Les options disponibles sont les suivantes :

   * Champs de formulaire personnalisé du document
   * Champs de formulaire personnalisé du projet
   * Champs de formulaire personnalisé du problème
   * Champs de formulaire personnalisé de la tâche
   * Champs de présentation du projet (ID, nom, description ou numéro de référence)

1. Dans le cas où le champ [!DNL Workfront] sélectionné dans le [!UICONTROL champ de formulaire personnalisé Workfront] est un champ de saisie semi-automatique des utilisateurs Workfront, il sera nécessaire de préciser quel champ Utilisateur Workfront vous souhaitez mapper. Pour ce faire, cochez la case Obtenir la valeur du champ d’objet référencé de Workfront, puis indiquez le nom du [!UICONTROL Champ de formulaire personnalisé Utilisateur Workfront] à partir duquel récupérer la valeur à mapper.

   ![configuration du mappage de métadonnées](/help/assets/assets/wf-metadata-mapping-config1.png)

## Propriété de mappage {#map-property}

Cette étape du workflow permet à l’utilisateur de mapper une propriété à une formulaire personnalisé [!DNL Workfront] sur un projet, une tâche, un problème ou un document. L’artefact [!DNL Workfront] concerné par cette étape est recherché à l’aide d’un chemin d’accès relatif à partir de la payload. Les propriétés à mapper sont contrôlées à partir de la configuration de la boîte de dialogue des étapes.

**Type** : ce champ vous permet de sélectionner le type d’objet Workfront auquel les propriétés doivent être mappées.

**Propriété d’ID** : ce champ vous permet de spécifier le chemin d’accès à l’identifiant de l’objet Workfront auquel les propriétés doivent être mappées. Le chemin d’accès spécifié dans ce champ doit être relatif à la payload du workflow.

**Affectations de propriété** : ce multichamp permet de spécifier les mappages entre les propriétés AEM et les champs Workfront. Chaque élément du champ multiple spécifie un mappage. Chaque mappage doit être au format `<workfront-field>=<aem-mapped-property>`.

* Le `workfront-field` peut être

   * Un champ de formulaire personnalisé identifié par le préfixe `DE:`.
   * Un champ modifiable identifié par son nom. Les noms des champs se trouvent dans l’[[!DNL Workfront] explorateur d’API](https://experience.workfront.com/s/api-explorer).

* Le `aem-mapped-property` peut être :

   * Une valeur littérale. Ils doivent être entourés de guillemets.
   * Une propriété AEM. Cette référence doit être relative à la payload du workflow.
   * Une valeur nommée. Ils doivent être entourés de crochets.
   * Une concaténation des 3 éléments ci-dessus. Spécifiez-la à l’aide de `{+}`.
   * Modification des 3 éléments ci-dessus en entourant la valeur avec `{replace(<value>,"old-char","new-char")}`.

* Voici quelques exemples :

   * `status="INP"`
   * `DE:Asset Type=jcr:content/metadata/assetType`
   * `DE:Path={path}`
   * `URL="https://my-aem-author/assets.html"{+}{path}`

![Configurer la propriété de mappage](/help/assets/assets/wf-map-property-config.png)

## Définir le statut {#set-status}

Dans l’éditeur de workflow, modifiez les propriétés de **[!UICONTROL Workfront - Définir le statut]** dans l’onglet **[!UICONTROL Arguments]**.

![Modifier le workflow pour définir le statut](/help/assets/assets/wf-set-status.png)

## Synchronisation des commentaires {#comments-sync}

1. Dans [!DNL Experience Manager], accédez à **[!UICONTROL Outils]** > **[!UICONTROL Services cloud]** > **[!UICONTROL Configuration des outils Workfront]**, sélectionnez la configuration, puis sélectionnez **[!UICONTROL Propriétés]**.

   ![synchronisation des commentaires](/help/assets/assets/comments-sync1.png)

1. Sélectionnez l’onglet **[!UICONTROL Abonnements aux événements]**, cliquez sur **[!UICONTROL Activer la synchronisation des commentaires]** dans l’option **[!UICONTROL Envoyer les commentaires de Workfront vers AEM]**.

   ![La synchronisation est activée](/help/assets/assets/wf-comment-sync-enabled.png)

Pour tester la synchronisation des commentaires de Workfront vers AEM, procédez comme suit :

1. Accédez à un document lié dans Workfront et ajoutez un commentaire dans l’onglet Mises à jour.

   ![laisser un commentaire dans Workfront](/help/assets/assets/comments-sync2.png)

1. Accédez au même document lié dans AEM, sélectionnez le document et ouvrez l’option [!UICONTROL Chronologie] dans le volet de navigation gauche, puis sélectionnez [!UICONTROL Commentaires]. La barre latérale gauche affiche les commentaires synchronisés à partir de [!DNL Workfront].

## Versions des ressources {#asset-versions}

Pour conserver l’historique des versions des ressources dans AEM, configurez le contrôle de version des ressources dans AEM.

1. Dans Experience Manager, accédez à **[!UICONTROL Outils]** > **[!UICONTROL Services cloud]** > **[!UICONTROL Configuration des outils Workfront]**, puis ouvrez l’onglet **[!UICONTROL Avancé]**.

1. Sélectionnez l’option **[!UICONTROL Stocker les ressources portant le même nom que les versions de la ressource existante]**. Lorsque cette option est cochée, elle permet de stocker les ressources chargées avec le même nom et au même emplacement que la version de la ressource existante. Si cette option n’est pas cochée, une nouvelle ressource est créée avec un nom différent (par exemple, `asset-name.pdf` et `asset-name-1.pdf`).

1. Sélectionnez l’option **[!UICONTROL Mise à jour des métadonnées de ressource lors de la création d’une version]**. Lorsque cette option est cochée, les métadonnées de la ressource sont mises à jour chaque fois qu’une nouvelle version de la ressource est créée. Si cette option n’est pas cochée, la ressource conserve les métadonnées qu’elle possédait avant de créer la nouvelle version.

![configurer le contrôle de version des ressources](/help/assets/assets/wf-config-versioning.png)

>[!NOTE]
>
>Le contrôle de version n’est pas pris en charge dans les dossiers liés. Lors de la création d’une BAT [!DNL Workfront] avec un document à l’intérieur d’un dossier lié, les commentaires et annotations de la version précédente de la ressource sont supprimés.

## Joindre des formulaires personnalisés {#attach-custom-forms}

Cette étape de workflow permet aux utilisateurs de joindre un formulaire personnalisé à un artefact [!DNL Workfront]. Cette étape de workflow peut être ajoutée à n’importe quel modèle de workflow. L’artefact [!DNL Workfront] concerné par cette étape sera recherché à l’aide d’un chemin d’accès relatif à partir de la payload.

Dans l’éditeur de workflow d’Experience Manager, modifiez les propriétés de l’étape de workflow [!UICONTROL Workfront - Joindre un formulaire personnalisé].

![formulaires personnalisés](/help/assets/assets/wf-custom-forms.png).

## Publication automatique de ressources {#auto-publish-assets}

1. Dans Experience Manager, accédez à **[!UICONTROL Outils]** > **[!UICONTROL Services cloud]** > **[!UICONTROL Configuration des outils Workfront]**, puis ouvrez l’onglet **[!UICONTROL Avancé]**.

1. Sélectionnez **[!UICONTROL Publier automatiquement les ressources lorsqu’elles sont envoyées depuis Workfront]**. Cette option permet la publication automatique des ressources lorsqu’elles sont envoyées de Workfront vers AEM. Cette fonctionnalité peut être activée de manière conditionnelle en spécifiant un champ de formulaire personnalisé Workfront et la valeur sur laquelle elle doit être définie. Chaque fois qu’un document est envoyé à AEM, s’il satisfait à la condition, la ressource est automatiquement publiée.

1. Sélectionnez **[!UICONTROL Publier toutes les ressources du projet sur Brand Portal à la fin du projet]**. Cette option permet la publication automatique des ressources sur [!DNL Brand Portal] lorsque le statut du projet Workfront auquel elles appartiennent passe sur `Complete`.

![configuration de la publication automatique](/help/assets/assets/wf-auto-publish-config.png)

## Mises à jour des formulaires personnalisés du document Workfront {#subscribe-workfront-doc-custom-form-updates}

Pour vous abonner aux modifications des formulaires personnalisés du document [!DNL Workfront], sélectionnez l’option correspondante dans l’onglet **[!UICONTROL Avancé]**. Lorsque vous vous abonnez à ces mises à jour, les champs de métadonnées [!DNL Experience Manager] mappés sont mis à jour lorsque le champ correspondant dans le formulaire personnalisé du document [!DNL Workfront] est modifié.

![Configuration des mises à jour des formulaires personnalisés du document Workfront dans [!DNL Experience Manager]](/help/assets/assets/wf-custom-form-update.png)
