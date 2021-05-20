---
title: Utilisation d’Adobe Sign dans un formulaire adaptatif
seo-title: Utilisation d’Adobe Sign dans un formulaire adaptatif
description: Activez les processus de signature électronique (Adobe Sign) pour un formulaire adaptatif afin d’automatiser les processus de signature, de simplifier les processus à signature unique et à signatures multiples et de signer électroniquement des formulaires à partir d’appareils mobiles.
seo-description: Activez les processus de signature électronique (Adobe Sign) pour un formulaire adaptatif afin d’automatiser les processus de signature, de simplifier les processus à signature unique et à signatures multiples et de signer électroniquement des formulaires à partir d’appareils mobiles.
uuid: cc3012ed-c318-4529-9adc-61aa5b5761a0
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: f79828d8-2230-4477-8ffa-eeb6a0413acd
docset: aem65
feature: Forms adaptatif, Adobe Sign
exl-id: a8decba9-229d-40a2-992a-3cc8ebefdd6d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '3863'
ht-degree: 56%

---

# Utilisation de [!DNL Adobe Sign] dans un formulaire adaptatif{#using-adobe-sign-in-an-adaptive-form}

[!DNL Adobe Sign] active les processus de signature électronique pour les formulaires adaptatifs. Les signatures électroniques améliorent les processus de traitement des documents pour les services juridiques, commerciaux, des ressources humaines, etc.

Dans un scénario de [!DNL Adobe Sign] type de formulaire adaptatif, un utilisateur remplit un formulaire adaptatif pour demander un service. Par exemple, une demande de prêt hypothécaire et de carte de crédit nécessite des signatures légales de tous les emprunteurs et codemandeurs. Pour activer les processus de signature électronique pour des scénarios similaires, vous pouvez intégrer [!DNL Adobe Sign] à l’AEM [!DNL Forms]. Voici quelques autres exemples d’utilisation d’[!DNL Adobe Sign] :

* Remportez des contrats à partir de tout appareil à l’aide de processus entièrement automatisés d’offre, de devis et de contrat.
* Terminez les processus de ressource humaine plus rapidement et offrez à vos employés une expérience numérique.
* Réduisez considérablement les durées des cycles en matière de contrat et intégrez plus rapidement vos fournisseurs.
* Créez des processus numériques pour automatiser les processus courants.

L’intégration d’[!DNL Adobe Sign][!DNL Forms] à AEM prend en charge les éléments suivants :

* Processus de signature d’utilisateur unique et multiutilisateur
* Processus de signature séquentiels et simultanés
* Expériences de signature dans le formulaire et hors du formulaire
* Signature de formulaires en tant qu’utilisateur anonyme ou connecté
* Processus de signature dynamique (intégration avec le workflow AEM [!DNL Forms])
* Authentification par le biais d’une base de connaissances, un téléphone et des profils de réseaux sociaux

Découvrez les [bonnes pratiques d’utilisation d’Adobe Sign avec des formulaires adaptatifs](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684) pour créer de meilleures expériences de signature.

## Prérequis {#prerequisites}

Avant d’utiliser [!DNL Adobe Sign] dans un formulaire adaptatif :

* Vérifiez que le service cloud [!DNL Forms] d’AEM est configuré pour utiliser [!DNL Adobe Sign]. Pour plus de détails, voir [Intégration d’Adobe Sign à AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).
* Gardez la liste des signataires prête. Vous devez disposer d’au moins une adresse électronique pour chaque signataire.

## Configurer [!DNL Adobe Sign] pour un formulaire adaptatif {#configure-adobe-sign-for-an-adaptive-form}

Effectuez les étapes suivantes pour configurer [!DNL Adobe Sign] pour un formulaire adaptatif :

1. [Modifier les propriétés du formulaire adaptatif pour le signe d’Adobe](../../forms/using/working-with-adobe-sign.md#enableadobesign)
1. [Ajouter des champs Adobe Sign à un formulaire adaptatif](../../forms/using/working-with-adobe-sign.md#addadobesignfieldstoanadaptiveform)
1. [Activer Adobe Sign pour un formulaire adaptatif](../../forms/using/working-with-adobe-sign.md#enableadobsignforanadaptiveform)
1. [Sélectionner un service cloud Adobe Sign pour un formulaire adaptatif](../../forms/using/working-with-adobe-sign.md#selectadobesigncloudserviceforanadaptiveform)

1. [Ajouter des signataires Adobe Sign à un formulaire adaptatif](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform)
1. [Sélectionner Envoyer l’action pour un formulaire adaptatif](../../forms/using/working-with-adobe-sign.md#selectsubmitactionforanadaptiveform)

![Détails du signataire](assets/signer_details_new.png)

### Modifier les propriétés du formulaire adaptatif pour [!DNL Adobe Sign] {#enableadobesign}

Configurez les propriétés du formulaire adaptatif pour [!DNL Adobe Sign] pour un formulaire adaptatif existant ou nouveau.

[La section Create an adaptive form for Adobe ](../../forms/using/working-with-adobe-sign.md#create-an-adaptive-form-for-adobe-sign) Signatures décrit les étapes de création d’un formulaire adaptatif de base. Voir [Création d’un formulaire adaptatif](../../forms/using/creating-adaptive-form.md) pour connaître les autres options disponibles lors de la création d’un formulaire adaptatif.

#### Créer un formulaire adaptatif pour [!DNL Adobe Sign] {#create-an-adaptive-form-for-adobe-sign}

Pour créer un formulaire adaptatif compatible, procédez comme suit :

1. Accédez à **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Formulaires]** > **[!UICONTROL Formulaires et documents]**.
1. Appuyez sur **[!UICONTROL Créer]** et sélectionner **[!UICONTROL Formulaire adaptatif]**. Une liste de modèles s’affiche. Sélectionnez le modèle et appuyez sur **[!UICONTROL Suivant]**.
1. Dans l’onglet **[!UICONTROL De base]** :

   1. Spécifiez le **[!UICONTROL nom]** et le **[!UICONTROL titre]** du formulaire adaptatif.

   1. Sélectionnez le [conteneur de configuration](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) créé lors de la configuration de [!DNL Adobe Sign] avec AEM [!DNL Forms].

      >[!NOTE]
      >
      >La liste déroulante **[!UICONTROL Cloud Service Adobe Sign]** affiche les services cloud configurés dans le conteneur de configuration que vous sélectionnez dans ce champ. La liste déroulante **[!UICONTROL Adobe Sign Cloud Service]** est disponible dans la section **[!UICONTROL Signature électronique]** des propriétés du formulaire adaptatif lorsque vous sélectionnez l’option **[!UICONTROL Activer Adobe Sign]**.

1. Dans l’onglet **[!UICONTROL Modèle de formulaire]**, sélectionnez l’une des options suivantes :

   * Sélectionnez l’option **[!UICONTROL Associer le modèle de formulaire comme modèle de document d’enregistrement]** et sélectionnez un modèle de document d’enregistrement. Si vous utilisez un formulaire adaptatif basé sur un modèle de formulaire, les documents envoyés pour signature affichent uniquement les champs basés sur le modèle de formulaire associé. Il n’affiche pas tous les champs du formulaire adaptatif.

   * Sélectionnez l’option **[!UICONTROL Générer un document d’enregistrement]** . Si vous utilisez un formulaire adaptatif activé avec l’option Document d’enregistrement, le document envoyé pour signature affiche tous les champs du formulaire adaptatif.

1. Appuyez sur **[!UICONTROL Créer.]** Un formulaire adaptatif compatible est créé, qui peut être utilisé pour ajouter  [!DNL Adobe Sign] des champs.

#### Modifier un formulaire adaptatif pour [!DNL Adobe Sign] {#editafsign}

Effectuez les étapes suivantes pour utiliser [!DNL Adobe Sign] dans un formulaire adaptatif existant :

1. Accédez à **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Formulaires]** > **[!UICONTROL Formulaires et documents]**.
1. Sélectionnez le formulaire adaptatif et appuyez sur **[!UICONTROL Propriétés]**.
1. Dans l&#39;onglet **[!UICONTROL De base]** , sélectionnez le [conteneur de configuration](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) créé lors de la configuration de [!DNL Adobe Sign] avec AEM [!DNL Forms].
1. Dans l’onglet **[!UICONTROL Modèle de formulaire]**, sélectionnez l’une des options suivantes :

   * Sélectionnez l’option **[!UICONTROL Associer le modèle de formulaire comme modèle de document d’enregistrement]** et sélectionnez un modèle de document d’enregistrement. Si vous utilisez un formulaire adaptatif basé sur un modèle de formulaire, les documents envoyés pour signature affichent uniquement les champs basés sur le modèle de formulaire associé. Il n’affiche pas tous les champs du formulaire adaptatif.

   * Sélectionnez l’option **[!UICONTROL Générer un document d’enregistrement]** . Si vous utilisez un formulaire adaptatif activé avec l’option Document d’enregistrement, le document envoyé pour signature affiche tous les champs du formulaire adaptatif.

1. Appuyez sur **[!UICONTROL Enregistrer et fermer]**. Le formulaire adaptatif est activé pour [!DNL Adobe Sign].

### Ajouter des champs Adobe Sign à un formulaire adaptatif {#addadobesignfieldstoanadaptiveform}

[!DNL Adobe Sign] dispose de plusieurs champs pouvant être placés sur un formulaire adaptatif. Ces champs acceptent divers types de données tels que les signatures, les initiales, la société ou le titre et aident à collecter des informations supplémentaires lors de la signature. Vous pouvez utiliser le composant Bloc [!DNL Adobe Sign] pour placer des champs [!DNL Adobe Sign] à différents emplacements dans un formulaire adaptatif.

Effectuez les étapes suivantes pour ajouter des champs à un formulaire adaptatif et personnaliser diverses options liées à ces champs :

1. Faites glisser et déposez le composant **[!UICONTROL Bloc Adobe Sign]** de l’explorateur de composants dans le formulaire adaptatif. Le composant Bloc [!DNL Adobe Sign] dispose de tous les champs [!DNL Adobe Sign] pris en charge. Par défaut, il ajoute un champ **Signature** au formulaire adaptatif.

   ![Bloc de signature](assets/sign_block_new.png)

   Par défaut, le bloc [!DNL Adobe Sign] n’est pas visible dans le formulaire adaptatif publié. Il est visible uniquement dans les documents de signature. Vous pouvez modifier la visibilité du bloc [!DNL Adobe Sign] dans les propriétés du composant Bloc [!DNL Adobe Sign].

   >[!NOTE]
   >
   >    * L’utilisation du bloc [!DNL Adobe Sign] n’est pas obligatoire pour utiliser [!DNL Adobe Sign] dans un formulaire adaptatif. Si vous n’utilisez pas le bloc [!DNL Adobe Sign] et ajoutez des champs pour les signataires, le champ de signature par défaut est affiché en bas des documents de signature.
   >    * Utilisez le bloc [!DNL Adobe Sign] uniquement pour les formulaires adaptatifs qui génèrent automatiquement un document d’enregistrement. Si vous utilisez un fichier XDP personnalisé pour générer un document d’enregistrement ou un formulaire adaptatif basé sur un modèle de formulaire, le bloc [!DNL Adobe Sign] n’est pas pris en charge.


1. Sélectionnez le composant **[!UICONTROL Bloc Adobe Sign]** et appuyez sur l’icône **Modifier** ![aem_6_3_edit](assets/aem_6_3_edit.png). Il affiche des options pour ajouter des champs et mettre en forme l’apparence d’un champ.

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **A.** Sélection et ajout de champs [!DNL Adobe Sign]. **B.** Développement du bloc [!DNL Adobe Sign] en mode plein écran

1. Appuyez sur l’icône **[!UICONTROL Adobe Sign] Field** ![aem_6_3_adagging](assets/aem_6_3_adobesign.png). Il affiche des options permettant de sélectionner et d’ajouter des champs [!DNL Adobe Sign].

   Développez le champ déroulant **[!UICONTROL Type]** pour sélectionner un champ [!DNL Adobe Sign] et appuyez sur l’icône Terminé ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) pour ajouter le champ sélectionné au bloc [!DNL Adobe Sign]. Le champ déroulant **[!UICONTROL Type]** comprend les types de champs Signature, Informations sur le signataire et Données. Intégration d’[!DNL Adobe Sign] aux champs de prise en charge [!DNL Forms] d’AEM répertoriés dans la liste déroulante [!UICONTROL Type] uniquement. Pour plus d’informations sur les champs [!DNL Adobe Sign], voir la [documentation Adobe Sign](https://helpx.adobe.com/fr/sign/help/field-types.html).

   ![adobe-sign-block-fields-options](assets/adobe-sign-block-fields-options.png)

   Il est obligatoire de fournir un nom unique pour un champ. Vous pouvez également sélectionner l’option requise pour marquer un champ comme obligatoire. En plus de l’option **[!UICONTROL Nom]** et **[!UICONTROL Obligatoire]**, certains champs [!DNL Adobe Sign] ont plus d’options. Par exemple, masque et multiligne. De plus, indiquez un nom unique pour chaque champ [!DNL Adobe Sign], que les champs résident dans le même bloc ou dans des [!DNL Adobe Sign] différents.

   Si vous sélectionnez **[!UICONTROL Signature numérique]** dans la liste déroulante, vous pouvez appliquer des signatures numériques au formulaire adaptatif :

   * En ligne, à l’aide de signatures cloud, vous pouvez signer avec un [ID numérique](https://helpx.adobe.com/fr/sign/kb/digital-certificate-providers.html) hébergé par un prestataire d’approbation.
   * Localement, en téléchargeant le document avec Adobe Acrobat ou Reader à l’aide d’une carte à puce, d’un jeton USB ou d’un ID numérique basé sur des fichiers.

### Activer [!DNL Adobe Sign] pour un formulaire adaptatif {#enableadobsignforanadaptiveform}

[!DNL Adobe Sign] n’est pas activé par défaut pour un formulaire adaptatif. Effectuez les étapes suivantes pour l’activer :

1. Dans l’explorateur de contenu, appuyez sur **[!UICONTROL Conteneur de formulaires]**, puis sur l’icône **[!UICONTROL Configurer]** ![configure](assets/configure.png). L’explorateur de propriétés s’ouvre et affiche les propriétés du conteneur de formulaires adaptatifs.
1. Dans l’explorateur de propriétés, développez l’accordéon **[!UICONTROL Signature électronique]** et sélectionnez l’option **[!UICONTROL Activer Adobe Sign]**. Il active [!DNL Adobe Sign] pour un formulaire adaptatif.

### Sélection d’[!DNL Adobe Sign] Cloud Service et d’un ordre de signature {#selectadobesigncloudserviceforanadaptiveform}

Vous pouvez configurer plusieurs services [!DNL Adobe Sign] pour une instance d’AEM [!DNL Forms]. Il est recommandé de disposer d’un ensemble distinct de services pour chaque fonction (ressources humaines, service financier, etc.). Cela facilite le suivi et la création de rapports sur les documents signés. Par exemple, une banque a plusieurs services. Vous pouvez avoir une configuration séparée pour chaque service pour un meilleur suivi des documents.

Un document peut également avoir plusieurs signataires. Par exemple, une demande de carte de crédit peut avoir plusieurs demandeurs. Une banque exige la signature de tous les demandeurs avant de commencer le traitement de la demande. Pour les scénarios multisignataires, vous pouvez choisir de signer le document dans un ordre séquentiel ou simultané.

Effectuez les étapes suivantes pour sélectionner un service cloud et un ordre de signature :

![service cloud](assets/cloud-service.png)

1. Dans l’explorateur de contenu, appuyez sur **[!UICONTROL Conteneur de formulaires]**, puis sur l’icône **[!UICONTROL Configurer]** ![configure](assets/configure.png). L’explorateur de propriétés s’ouvre et affiche les propriétés du conteneur de formulaires adaptatifs.
1. Dans l’explorateur de propriétés, développez l’accordéon **[!UICONTROL Signature électronique]** et sélectionnez l’option **[!UICONTROL Activer Adobe Sign]**. Il active [!DNL Adobe Sign] pour un formulaire adaptatif.
1. Sélectionnez un service cloud dans la liste déjà configurée des Cloud Services [!DNL Adobe Sign].

   Si la liste **[!UICONTROL Adobe Sign Cloud Service]** est vide, consultez l’article [Configuration d’Adobe Sign avec AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md) pour configurer le service.

   La liste déroulante répertorie les services cloud qui existent dans le dossier `global` dans Outils > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]**. En outre, la liste déroulante répertorie également les services cloud qui existent dans le dossier que vous sélectionnez dans le champ **[!UICONTROL Conteneur de configuration]** lorsque vous créez un formulaire adaptatif.

1. Sélectionnez l’ordre de signature dans la boîte de dialogue **[!UICONTROL Les signataires peuvent signer]**. [!DNL Adobe Sign]Les signataires peuvent signer un formulaire adaptatif de manière **[!UICONTROL séquentielle]** (l’un après l’autre) ou **[!UICONTROL simultanée]** (dans n’importe quel ordre).

   Dans un ordre séquentiel, un signataire à la fois reçoit le formulaire à signer. Une fois que le signataire a terminé la signature du document, le formulaire est envoyé au signataire suivant, et ainsi de suite.

   Dans l’ordre simultané, plusieurs signataires à la fois peuvent signer un formulaire.

1. [Ajoutez des signataires à un ](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform) formulaire adaptatif et appuyez sur l’icône Terminé  ![aem_6_3_forms_](assets/aem_6_3_forms_save.png)  pour enregistrer les modifications.


### Ajouter des signataires à un formulaire adaptatif {#addsignerstoanadaptiveform}

Vous ne pouvez avoir qu’un seul signataire ou plusieurs signataires pour un formulaire adaptatif. Lorsque vous ajoutez un signataire, vous pouvez également configurer les détails d’authentification pour le signataire. Vous pouvez également sélectionner si le remplisseur du formulaire et le signataire sont la même personne. Effectuez les étapes suivantes pour ajouter et fournir divers détails sur un signataire :

1. Dans l’explorateur de contenu, appuyez sur **[!UICONTROL Conteneur de formulaires]**, puis sur l’icône **[!UICONTROL Configurer]** ![configure](assets/configure.png). Il ouvre l’explorateur de propriétés avec les propriétés du conteneur de formulaires adaptatifs.
1. Dans l’explorateur de propriétés, développez l’accordéon **[!UICONTROL Signature électronique]** et sélectionnez l’option **[!UICONTROL Activer Adobe Sign]**. Il active [!DNL Adobe Sign] pour un formulaire adaptatif.
1. Appuyez sur **[!UICONTROL Ajouter un signataire]** sous **[!UICONTROL Configuration du signataire]**. Il ajoute un signataire au formulaire adaptatif. Vous pouvez ajouter plusieurs [!DNL Adobe Sign] signataires à un formulaire adaptatif.
   ![phone-details](assets/phone-details.png)

1. Cliquez sur l’icône **Modifier** ![aem_6_3_edit](assets/aem_6_3_edit.png) pour spécifier les informations suivantes sur le signataire :

   * **[!UICONTROL Titre] :** spécifiez un titre pour identifier de manière unique un signataire.

   * **[!UICONTROL Le signataire et la personne remplissant le formulaire sont-ils la même personne ?] :** sélectionnez **Oui** si le remplisseur du formulaire et le premier signataire sont la même personne. Si l’option est définie sur **Non,** n’utilisez pas le composant d’étape de signature dans le formulaire adaptatif. Si le formulaire contient un composant Étape de signature, le champ est automatiquement défini sur Oui.

   * **[!UICONTROL Adresse électronique du signataire] :** précisez l’adresse électronique du signataire. Le signataire reçoit les documents/formulaires à signer à l’adresse électronique indiquée. Vous pouvez choisir d’utiliser une adresse électronique fournie dans un champ de formulaire, dans le profil utilisateur AEM de l’utilisateur connecté ou d’entrer manuellement une adresse électronique. Il s’agit d’une étape obligatoire. Assurez-vous que l’adresse électronique du premier signataire ou du seul signataire (dans le cas d’un signataire unique) n’est pas identique au compte [!DNL Adobe Sign] utilisé pour configurer les services cloud AEM.

   * **[!UICONTROL Méthode d’authentification du signataire] :** spécifiez la méthode pour authentifier un utilisateur avant d’ouvrir un formulaire à des fins de signature. Vous pouvez choisir entre le téléphone, la base de connaissances et l’authentification basée sur l’identité de réseau social.
   >[!NOTE]
   >
   >    * Par défaut, l’authentification basée sur l’identité de réseau social offre une option d’authentification via Facebook, Google et LinkedIn. Vous pouvez contacter le service d’assistance [!DNL Adobe Sign] pour activer d’autres fournisseurs d’authentification sociale.


   * Champs **[!DNL Adobe Sign]à remplir ou à signer :** sélectionnez les champs [!DNL Adobe Sign] pour le signataire. Un formulaire adaptatif peut comporter plusieurs champs [!DNL Adobe Sign]. Vous pouvez choisir d’activer des champs spécifiques pour un signataire. Le champ affiche tous les blocs [!DNL Adobe Sign] disponibles. Lorsque vous sélectionnez un bloc, tous les champs du bloc sont sélectionnés. Vous pouvez utiliser l’icône X pour désélectionner un champ.

   ![signer-details](assets/signer-details.png)

   L’image ci-dessus a deux exemples de blocs [!DNL Adobe Sign] : Informations personnelles et Détails du bureau

   Appuyez sur l’icône Terminé ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) . Le signataire est ajouté et configuré.

### Sélectionner Envoyer l’action pour un formulaire adaptatif {#selectsubmitactionforanadaptiveform}

Après avoir ajouté des champs [!DNL Adobe Sign] à un formulaire adaptatif, activé [!DNL Adobe Sign] à partir du conteneur de formulaires, sélectionné [!DNL Adobe Sign] Cloud Service et ajouté des signataires [!DNL Adobe Sign], sélectionnez une action d’envoi appropriée pour le formulaire adaptatif. Pour plus d’informations sur les actions d’envoi de formulaires adaptatifs, voir [Configuration de l’action d’envoi](../../forms/using/configuring-submit-actions.md).

En outre, un formulaire adaptatif [!DNL Adobe Sign] activé n’est envoyé qu’une fois que tous les signataires ont signé le formulaire. Vous pouvez trouver un formulaire partiellement signé dans la section En attente de signature du portail des formulaires. [!DNL Adobe Sign] Configuration Service conserve le  [!DNL Adobe Sign] serveur d’interrogation à des  [intervalles ](../../forms/using/adobe-sign-integration-adaptive-forms.md) réguliers pour vérifier l’état des signatures. Si tous les signataires terminent la signature du formulaire, le service d’action d’envoi est démarré et le formulaire est envoyé. Si vous utilisez une action d’envoi personnalisée et que le formulaire utilise [!DNL Adobe Sign], mettez à jour votre action d’envoi personnalisée pour utiliser le service d’action d’envoi.

<!-- Remove when forms portal goes live
>[!NOTE]
>
>Data of the adaptive form is stored temporarily on Forms Portal. It is recommended to use [custom storage for Forms Portal](/help/forms/using/configuring-draft-submission-storage.md). It ensures that the PII (personally identifiable information) data is not stored on AEM servers. 
-->

Votre expérience de signature de formulaire est prête. Vous pouvez prévisualiser le formulaire pour vérifier l’expérience de signature. Sur le formulaire publié, les champs Bloc [!DNL Adobe Sign] sont affichés lorsqu’un signataire reçoit le formulaire à signer dans un e-mail. Cette expérience est également connue comme expérience de signature hors du formulaire. Vous pouvez également configurer une expérience de signature dans le formulaire pour le premier signataire. Pour les étapes détaillées, voir [Créer une expérience de signature dans le formulaire](../../forms/using/working-with-adobe-sign.md#create-in-form-signing-experience).

## Configuration des signatures cloud pour un formulaire adaptatif {#configure-cloud-signatures-for-an-adaptive-form}

Les signatures numériques basées sur le cloud ou les signatures distantes sont une nouvelle génération de signatures numériques qui fonctionnent sur les postes de travail, les appareils mobiles et le web, et qui répondent aux niveaux de conformité et d’assurance les plus élevés pour l’authentification des signataires. Vous pouvez signer un formulaire adaptatif avec des signatures numériques basées sur le cloud.

Après avoir [modifié les propriétés du formulaire adaptatif pour le signe d’Adobe](../../forms/using/working-with-adobe-sign.md#enableadobesign), effectuez les étapes suivantes pour ajouter le champ de signature cloud à un formulaire adaptatif :

1. Faites glisser et déposez le composant **[!UICONTROL Bloc Adobe Sign]** de l’explorateur de composants dans le formulaire adaptatif. Le composant [!UICONTROL Bloc Adobe Sign] dispose de tous les champs [!DNL Adobe Sign] pris en charge. Par défaut, il ajoute un champ **[!UICONTROL Signature]** au formulaire adaptatif.

   ![Bloc de signature](assets/sign-block-new.png)

1. Sélectionnez le composant **[!UICONTROL Bloc Adobe Sign]** et appuyez sur l’icône **Modifier** ![aem_6_3_edit](assets/aem_6_3_edit.png). Il affiche des options pour ajouter des champs et mettre en forme l’apparence d’un champ.

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **A.** Sélection et ajout de champs [!DNL Adobe Sign]. **B.** Développement du bloc [!DNL Adobe Sign] en mode plein écran

1. Appuyez sur l’icône **[!UICONTROL Adobe Sign Field]** ![aem_6_3_adagging](assets/aem_6_3_adobesign.png). Elle affiche des options permettant de sélectionner et d’ajouter des champs [!DNL Adobe Sign].

   Développez le champ déroulant **[!UICONTROL Type]** pour sélectionner **[!UICONTROL Signature numérique]**, puis appuyez sur l’icône **Terminé** pour ajouter le champ sélectionné au bloc [!DNL Adobe Sign].

   ![Signatures numériques](assets/digital_signatures_new.png)

   Il est obligatoire de fournir un nom unique pour un champ.

   Appliquez des signatures numériques au formulaire adaptatif à l’aide de :

   * Signatures cloud : signez avec un [ID numérique](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) hébergé par un prestataire de confiance.
   * Adobe Acrobat ou Reader : téléchargez et ouvrez le document avec Adobe Acrobat ou Reader pour le signer à l’aide d’une carte à puce, un jeton USB ou un ID numérique basé sur des fichiers.

   Après avoir ajouté le champ de signature cloud au formulaire adaptatif, procédez comme suit pour terminer le processus de configuration :

   * [Activer Adobe Sign pour un formulaire adaptatif](../../forms/using/working-with-adobe-sign.md#enableadobsignforanadaptiveform)
   * [Sélectionner un service cloud Adobe Sign pour un formulaire adaptatif](../../forms/using/working-with-adobe-sign.md#selectadobesigncloudserviceforanadaptiveform)
   * [Ajouter des signataires Adobe Sign à un formulaire adaptatif](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform)
   * [Sélectionner Envoyer l’action pour un formulaire adaptatif](../../forms/using/working-with-adobe-sign.md#selectsubmitactionforanadaptiveform)


## Créer une expérience de signature dans le formulaire {#create-in-form-signing-experience}

Un utilisateur peut également signer un formulaire adaptatif lors du remplissage du formulaire. Cette expérience est également connue comme expérience de signature dans le formulaire. L’expérience de signature dans le formulaire est disponible uniquement pour le premier signataire dans un environnement à plusieurs signataires. Effectuez les étapes suivantes pour créer une expérience de signature dans le formulaire pour un formulaire adaptatif :

1. Ajoutez et configurez le composant [Étape de signature](../../forms/using/working-with-adobe-sign.md#add-and-configure-the-signature-step-component).
1. Ajoutez le composant [Étape de résumé](../../forms/using/working-with-adobe-sign.md#configure-the-thank-you-page-or-summary-step-component).

![Expérience de signature dans le formulaire](assets/in_form_signing_experience_new.png)

### Ajouter et configurer le composant Étape de signature {#add-and-configure-the-signature-step-component}

Utilisez le composant Étape de signature pour fournir une zone pour signer électroniquement le formulaire rempli. Lorsque la section contenant le composant Étape de signature est générée, elle affiche une version PDF à signer du formulaire rempli. Le composant Étape de signature prend toute la largeur disponible pour le formulaire. Il est recommandé de ne pas avoir d’autre composant sur la section contenant le composant Étape de signature.

Effectuez les étapes suivantes pour configurer le composant Étape de signature :

1. Glissez et déposez le composant **[!UICONTROL Étape de signature]** dans le formulaire à partir de l’explorateur de composants.
1. Sélectionnez le nouveau composant d’étape Signature et appuyez sur l’icône **Configurer** ![configurer](assets/configure.png) . Elle ouvre l’explorateur de propriétés et affiche les propriétés Étape de signature. Configurez les propriétés suivantes :

   * **[!UICONTROL Nom]** : Indiquez le nom du composant.

   * **[!UICONTROL Titre] :** indiquez le titre unique du composant.
   * **[!UICONTROL Message du modèle] :** spécifiez le message à afficher pendant le chargement du PDF de signature. [!DNL Adobe Sign]Les services mettent un certain temps à préparer et charger la signature PDF.
   * **[!UICONTROL Service de signature] :** sélectionnez l’ **[!DNL Adobe Sign]** option.

   * **[!UICONTROL Utiliser le composant de signature électronique hérité]** : si vous utilisez le formulaire adaptatif respectif dans [l’espace de travail AEM ](../../forms/using/introduction-html-workspace.md)[!DNL Forms], l’application AEM Forms ou que le formulaire adaptatif sous-jacent a un composant de signature électronique hérité, sélectionnez l’option **Utiliser le composant de signature électronique hérité**.

   * **[!UICONTROL Configuration]** : Sélectionnez une configuration ([!DNL Adobe Sign] Cloud Service). La liste déroulante n’est disponible que si l’option **Utiliser le composant de signature électronique** est activée.

   * **[!UICONTROL Classe CSS]** : Spécifiez la classe CSS du composant.

   Appuyez sur l’icône Terminé ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) pour enregistrer les modifications.

   ![Étape de signature](assets/signature_step_new.png)

   >[!NOTE]
   >
   > * Lorsque vous faites glisser le composant **[!UICONTROL Étape de signature]** dans le formulaire, l’option **[!UICONTROL Le signataire et la personne remplissant le formulaire ne sont-ils qu’une seule et même personne ?]** est automatiquement définie sur **Oui**. Il est nécessaire pour que le formulaire fonctionne.
      >
      > 
   * Utilisez le composant Étape de résumé après le composant Étape de signature pour une expérience optimale. L’étape Résumé envoie automatiquement le formulaire après avoir signé un formulaire dans le composant Étape de signature. Si vous n’utilisez pas l’étape de résumé, un envoi automatique n’est déclenché qu’après l’intervalle défini à l’aide de [Adobe Sign Configuration Service](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-scheduler-to-sync-the-signing-status).
      > Voici quelques bonnes pratiques :
   > * Le panneau du formulaire adaptatif contenant l’étape Signature se trouve toujours dans le dernier ou le deuxième dernier panneau d’un formulaire adaptatif. Il peut s’agir du deuxième dernier panneau uniquement lorsque le dernier panneau contient l’étape Résumé .
   > * Le panneau contenant le composant d’étape Signature ou Résumé ne peut pas contenir d’autre composant.
   > * Les formulaires adaptatifs contenant l’étape de signature ne peuvent pas comporter de bouton d’envoi.
   > * L’envoi des formulaires adaptatifs contenant l’étape Signature est géré via un service en arrière-plan ou l’étape Résumé. Si un signataire configuré est également en train de remplir le formulaire, l’avantage de gérer l’envoi du formulaire adaptatif à l’aide de l’étape Résumé est qu’il évalue immédiatement que le signataire a signé le formulaire et appelle l’action d’envoi. Un service d’arrière-plan prend plus de temps pour évaluer si tous les signataires configurés ont signé le formulaire et retardent l’envoi du formulaire adaptatif.
   > * Concevez le formulaire de manière à ne pas permettre à l’utilisateur de revenir d’un panneau contenant l’étape Signature ou Résumé.



### Configuration de la page de remerciements ou du composant d’étape de résumé {#configure-the-thank-you-page-or-summary-step-component}

Le composant **Étape de résumé** envoie automatiquement le formulaire, indique les informations dans la page Résumé personnalisée et affiche le résumé du formulaire envoyé. Il obtient également les informations requises dans le mappage de retour. Il prend toute la largeur disponible pour le formulaire. Il est recommandé de ne pas avoir d’autre composant sur la section contenant le composant Étape de résumé.

Maintenant, l’expérience de signature dans le formulaire est prête. Vous pouvez prévisualiser le formulaire pour vérifier l’expérience de signature.

## Forum aux questions {#frequently-asked-questions}

**Q :** Vous pouvez incorporer un formulaire adaptatif dans un autre formulaire adaptatif. Le formulaire adaptatif incorporé peut-il être [!DNL Adobe Sign] activé ?
**Réponse :**[!DNL Forms] Non, AEM ne prend pas en charge l’utilisation d’un formulaire adaptatif incorporant un formulaire adaptatif activé pour à des fins de signature[!DNL Adobe Sign]

**Q :** Lorsque je crée un formulaire adaptatif à l’aide du modèle avancé et que je l’ouvre pour modification, un message d’erreur &quot;Signature électronique ou signataires non configurés correctement&quot; s’affiche. s’affiche. Comment résoudre le message d’erreur ?
**Réponse :** Le formulaire adaptatif créé à l’aide du modèle avancé est configuré pour utiliser [!DNL Adobe Sign]. Pour résoudre l’erreur, créez et sélectionnez une configuration de cloud [!DNL Adobe Sign] et configurez un signataire [!DNL Adobe Sign] pour le formulaire adaptatif.

**Q :** Puis-je utiliser des balises  [!DNL Adobe Sign] de texte dans un composant de texte statique d’un formulaire adaptatif ?
**Réponse :**[!DNL Adobe Sign] Oui, vous pouvez utiliser des balises de texte dans un composant de texte pour ajouter des champs à un formulaire adaptatif doté de l’option [Document d’enregistrement](../../forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md) (option de document d’enregistrement généré automatiquement uniquement). Pour en savoir plus sur la procédure et les règles de création d’une balise de texte, voir la [documentation d’Adobe Sign](https://helpx.adobe.com/fr/sign/using/text-tag.html). Notez également que les formulaires adaptatifs offre une prise en charge limitée des balises de texte. Vous pouvez utiliser les balises de texte pour créer uniquement les champs pris en charge par le [bloc Adobe Sign](../../forms/using/working-with-adobe-sign.md#configure-cloud-signatures-for-an-adaptive-form).

**Q :** AEM  [!DNL Forms] fournit les composants  [!UICONTROL bloc et étape Signature ] Adobe Sign. Peut-on les utiliser simultanément dans un formulaire adaptatif ?
**Réponse** : Vous pouvez utiliser simultanément les deux composants dans un formulaire. Voici quelques recommandations relatives à l’utilisation des composants suivants :

**Bloc Adobe Sign :** vous pouvez utiliser le  [!UICONTROL bloc Adobe Sign ] pour ajouter des champs de  [!UICONTROL signature d’] Adobe n’importe où dans le formulaire adaptatif. Il permet également d’attribuer des champs spécifiques aux signataires. Lorsqu’un formulaire adaptatif est prévisualisé ou publié, le bloc [!UICONTROL Adobe Sign] n’est pas visible par défaut. Ces blocs sont disponibles uniquement dans le document de signature. Dans le document de signature, seuls les champs affectés à un signataire sont activés. [!UICONTROL Le bloc Adobe Sign peut être utilisé avec les premiers et futurs signataires.]

**Composant d’étape de signature :** vous pouvez utiliser le composant d’étape de signature pour créer une expérience de signature dans le formulaire. Il permet uniquement au premier signataire de signer pendant que le formulaire est rempli. Lorsque la section contenant le composant Étape de signature est générée, elle affiche une version PDF à signer du formulaire. Il s’agit généralement de la dernière ou de l’avant-dernière section suivie du composant de résumé d’un formulaire.

## Résolution des problèmes {#troubleshoot}

### [!DNL Adobe Sign] Échecs des accords {#adobe-sign-agreement-failures}

****
Problème : lorsque  [!DNL Adobe Sign] le service est configuré pour un formulaire adaptatif, il ne parvient pas à créer un  [!DNL Adobe Sign] accord pour le formulaire adaptatif sous-jacent.

**Résolution**

* Vérifiez la [configuration du service cloud Adobe Sign](../../forms/using/adobe-sign-integration-adaptive-forms.md) utilisé dans le formulaire adaptatif.
* Assurez-vous que l’application API sur le serveur [!DNL Adobe Sign] utilisé pour configurer le service cloud [!DNL Adobe Sign] dispose des autorisations requises.
* Si vous utilisez plusieurs [!DNL Adobe Sign] services cloud, pointez la **[!UICONTROL URL oAuth]** de tous les services vers le même **[!UICONTROL partage Adobe Sign]**.

* Utilisez des adresses électroniques distinctes pour configurer le compte [!DNL Adobe Sign] et pour le premier signataire et le signataire unique. L’adresse électronique du premier signataire ou du seul signataire (dans le cas du signataire unique) ne peut pas être identique au compte [!DNL Adobe Sign] utilisé pour configurer les services cloud AEM.

### AEM processus [!DNL Forms] configuré pour un formulaire adaptatif [!DNL Adobe Sign] activé ne démarre pas {#adobe-sign-aem-form-workflow-failures}

****
ProblèmeLorsque  [!DNL Adobe Sign] est configuré pour un formulaire adaptatif, le processus configuré à l’aide de l’option Appeler le  [!DNL Forms] processus ne démarre pas.

**Résolution**

* Lorsque vous utilisez [!DNL Adobe Sign] sans l’étape Signature ou que le formulaire nécessite des signatures de plusieurs personnes, AEM serveur [!DNL Forms] attend que le planificateur confirme que toutes les personnes ont signé le formulaire. Le planificateur n’envoie le formulaire adaptatif qu’une fois que toutes les personnes ont terminé la signature et que le processus ne démarre qu’après un envoi réussi du formulaire adaptatif. Vous pouvez raccourcir l’intervalle du [planificateur](adobe-sign-integration-adaptive-forms.md) pour vérifier l’état de la signature du formulaire à intervalles rapides et accélérer l’envoi du formulaire.


## Articles connexes {#related-articles}

* [Incorporation d’Adobe Sign à AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md)
* [Bonnes pratiques relatives à l’utilisation d’Adobe Sign avec les formulaires adaptatifs](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684)
* [Utilisation d’Adobe Sign avec AEM Forms (vidéo)](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
