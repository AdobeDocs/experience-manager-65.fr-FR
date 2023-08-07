---
title: Incorporation d’Adobe Sign à AEM Forms
seo-title: Integrate Adobe Sign with AEM Forms
description: Découvrez comment configurer Adobe Sign pour AEM Forms.
seo-description: Learn how to configure Adobe Sign for AEM Forms
uuid: e5049775-fb6c-4228-9823-e6a2811460da
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 1f28b257-5419-4a21-a54a-b20bf35530ac
docset: aem65
feature: Adaptive Forms, Acrobat Sign
exl-id: 52146038-1582-41b8-aee0-215d04bb91d7
source-git-commit: e7a3558ae04cd6816ed73589c67b0297f05adce2
workflow-type: tm+mt
source-wordcount: '2055'
ht-degree: 96%

---

# Intégrer [!DNL Adobe Sign]avec AEM [!DNL Forms]{#integrate-adobe-sign-with-aem-forms}

<span class="preview"> Adobe recommande d’utiliser la capture de données moderne et extensible. [Composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=fr) pour [création d’un Forms adaptatif](/help/forms/using/create-an-adaptive-form-core-components.md) ou [Ajout de Forms adaptatif à des pages AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Ces composants représentent une avancée significative dans la création de Forms adaptatif, ce qui garantit des expériences utilisateur impressionnantes. Cet article décrit l’approche plus ancienne de la création de Forms adaptatif à l’aide de composants de base. </span>

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Cliquez ici](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/services/adobe-sign-integration-adaptive-forms.html?lang=en#adobe-acrobat-sign-for-government) |
| AEM 6.5 | Cet article |

[!DNL Adobe Sign] permet des processus de signature électronique pour les formulaires adaptatifs. Les signatures électroniques améliorent les processus de traitement des documents pour les services juridiques, commercial, des ressources humaines, et bien d’autres domaines.

Dans un scénario [!DNL Adobe Acrobat Sign] et de formulaires adaptatifs standard, un utilisateur remplit un formulaire adaptatif pour effectuer une demande de service. Par exemple, un formulaire de demande de carte bancaire et d’allocation. Lorsqu’un utilisateur ou une utilisatrice remplit, envoie et signe le formulaire de demande, le formulaire est envoyé au fournisseur de services pour qu’il effectue d’autres actions. Le prestataire de services passe en revue la demande et utilise [!DNL Adobe Acrobat Sign] pour marquer la demande comme approuvée. AEM Forms prend en charge Adobe Acrobat Sign et Adobe Acrobat Sign Solutions pour le gouvernement. En fonction de votre licence et de vos besoins, vous pouvez intégrer ou connecter AEM Forms à l’une des solutions suivantes :

* [Connecter AEM Forms à Adobe Acrobat Sign](#adobe-sign)
* [Connecter AEM Forms à Adobe Acrobat Sign Solutions pour le gouvernement](#adobe-acrobat-sign-for-government)

## Connecter AEM Forms à Adobe Acrobat Sign {#adobe-sign}

Pour connecter **[!DNL AEM Forms]** à **[!DNL Adobe Acrobat Sign]**, configurez le logiciel et les comptes répertoriés dans la section des prérequis et connectez Adobe Sign à toutes vos instances de création et de publication d’AEM Forms :

## Prérequis {#prerequisites}

Vous avez besoin des éléments suivants pour intégrer [!DNL Adobe Sign] à AEM :[!DNL Forms]

* Un compte de développeur [Adobe Sign actif.](https://acrobat.adobe.com/fr/fr/why-adobe/developer-form.html)
* Un serveur AEM [SSL](/help/sites-administering/ssl-by-default.md).[!DNL Forms]
* Une [application API Adobe Sign](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md).
* Les informations d’identification (ID client et clé secrète client) de l’application API [!DNL Adobe Sign].
* Lors de la reconfiguration, supprimez la configuration [!DNL Adobe Sign] à partir des instances de création et de publication.
* Une [crypto-clé identique](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed) pour les instances d’auteur et de publication.

## Configurer [!DNL Adobe Sign] avec AEM [!DNL Forms] {#configure-adobe-sign-with-aem-forms}

Une fois les conditions préalables en place, procédez comme suit pour configurer [!DNL Adobe Sign]avec AEM [!DNL Forms] sur l’instance de création :

1. Dans [!DNL Forms]l’instance de création AEM, accédez à **Outils** ![marteau](assets/hammer.png) > **[!UICONTROL Généralités]** > **[!UICONTROL Navigateur de configuration]**.
1. Sur la page du **[!UICONTROL navigateur de configuration]**, appuyez sur **[!UICONTROL Créer]**.
   * Pour plus d’informations, consultez la documentation relative au [Navigateur de configuration](/help/sites-administering/configurations.md).
1. Dans la boîte de dialogue **[!UICONTROL Créer une configuration]**, indiquez un **[!UICONTROL titre]** pour la configuration, activez **[!UICONTROL Configurations cloud]** et appuyez sur **[!UICONTROL Créer]**. Cela crée un conteneur de configuration.
1. Accédez à **Outils** ![marteau](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]** et sélectionnez le conteneur de configuration que vous avez créé à l’étape précédente.

   >[!NOTE]
   >
   >Vous pouvez exécuter les étapes 1 à 4 pour créer un nouveau conteneur de configuration et créer une configuration [!DNL Adobe Sign] dans le conteneur ou utiliser le dossier `global` dans **Outils** ![marteau](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]**. Si vous créez la configuration dans le nouveau conteneur de configuration, veillez à spécifier le nom du conteneur dans le champ **[!UICONTROL Conteneur de configuration]** lorsque vous créez un formulaire adaptatif.

   >[!NOTE]
   >
   Vérifiez que l’URL de la page de configuration des services cloud commence par **HTTPS**. Si ce n’est pas le cas, [activez SSL](/help/sites-administering/ssl-by-default.md) pour le serveur AEM [!DNL Forms]

1. Sur la page de configuration, appuyez sur **[!UICONTROL Créer]** pour créer [!DNL Adobe Sign] une configuration dans AEM [!DNL Forms].
1. Dans l’onglet **[!UICONTROL Généralités]** de la page **[!UICONTROL Créer une configuration Adobe Sign]**, spécifiez un **[!UICONTROL Nom]** de configuration et appuyez sur **[!UICONTROL Suivant]**. Vous avez la possibilité d’indiquer un titre et de rechercher et de sélectionner une vignette pour la configuration.

1. Copiez l’URL dans la fenêtre active du navigateur dans un bloc-notes. Vous en avez besoin pour configurer l’application [!DNL Adobe Sign] avec AEM [!DNL Forms].

1. Dans l’onglet **[!UICONTROL Paramètres]**, le champ **[!UICONTROL URL OAuth]** indique l’URL par défaut. Le format de l’URL est:

   `https://<shard>/public/oAuth/v2`

   Par exemple :
   `https://secure.na1.echosign.com/public/oauth/v2`

   où :

   **na1** fait référence au partitionnement de base de données par défaut. Vous pouvez modifier la valeur du partitionnement de base de données. Assurez-vous que les configurations cloud de [!DNL  Adobe Sign] pointent vers le [fragment correct](https://helpx.adobe.com/fr/sign/using/identify-account-shard.html).

   Si vous créez une autre configuration [!DNL Adobe Sign] pour une fonctionnalité ou un composant Adobe Experience Manager, assurez-vous que toutes les configurations cloud de [!DNL Adobe Sign] pointent vers le même fragment.

   >[!NOTE]
   >
   Gardez la page **Créer une configuration Adobe Sign** ouverte. Ne la fermez pas. Vous pouvez récupérer l’**ID client** et le **secret client** après la configuration des paramètres OAuth pour l’application [!DNL Adobe Sign] comme décrit dans les étapes à venir.


1. Configurez les paramètres OAuth pour l’application [!DNL Adobe Sign] :

   1. Ouvrez une fenêtre de navigateur et connectez-vous au compte de développeur [!DNL Adobe Sign].
   1. Sélectionnez l’application configurée pour AEM [!DNL Forms], puis appuyez sur **[!UICONTROL Configurer OAuth pour l’application]**.
   1. Copiez l’**[!UICONTROL ID client]** et le **[!UICONTROL Secret du client]** vers un bloc-notes.
   1. Dans la zone **[!UICONTROL URL de redirection]**, ajoutez l’URL HTTPS copiée à l’étape précédente.
   1. Activez les paramètres OAuth suivants pour l’application [!DNL Adobe Sign] et cliquez sur **[!UICONTROL Enregistrer]**.

   * agreement_read
   * agreement_write
   * agreement_send
   * widget_write
   * workflow_read

   Pour obtenir des informations détaillées sur la configuration des paramètres OAuth pour une application [!DNL Adobe Sign] et l’obtention des clés, voir [Configurer les paramètres oAuth pour l’application](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md) dans la documentation du développeur.

   ![Configuration OAuth](assets/oauthconfig_new.png)

1. Revenez à la page **[!UICONTROL Créer une configuration Adobe Sign]**. Dans l’onglet **[!UICONTROL Paramètres]**, le champ **[!UICONTROL URL OAuth]** indique l’URL par défaut. Le format de l’URL est:

   `https://<shard>/public/oAuth/v2`

   Par exemple :
   `https://secure.na1.echosign.com/public/oauth/v2`

   où :

   **na1** fait référence au partitionnement de base de données par défaut.

   Vous pouvez modifier la valeur du partitionnement de base de données. Redémarrez le serveur pour pouvoir utiliser la nouvelle valeur pour le partitionnement de base de données.

   >[!NOTE]
   >
   Assurez-vous que les configurations des instances d’auteur et de publication pointent vers la même partition. Si vous créez plusieurs configurations Adobe Sign pour une organisation, assurez-vous que toutes utilisent la même partition.

1. Revenez à la page **[!UICONTROL Créer une configuration Adobe Sign]**. Dans l’onglet **[!UICONTROL Paramètres]**, spécifiez l’**ID client** (également appelé ID de l’application) et le **secret client**. Utilisez l’[ID client et le secret client de l’application Adobe Sign](https://opensource.adobe.com/acrobat-sign/developer_guide/helloworld.html#get-the-app-id-and-secret) créés pour AEM Forms.

1. Sélectionnez l’option **[!UICONTROL Activer pour les pièces jointes également]** pour ajouter les fichiers joints à un formulaire adaptatif au document Adobe Sign correspondant envoyé à des fins de signature.[!DNL Adobe Sign]

1. Appuyez sur **[!UICONTROL Se connecter à Adobe Sign]**. Lorsque vous êtes invité à fournir vos informations d’identification, indiquez le nom d’utilisateur et le mot de passe du compte utilisé lors de la création de l’application [!DNL Adobe Sign]. 

1. Appuyez sur **[!UICONTROL Créer]** pour créer la configuration [!DNL Adobe Sign].

1. Ouvrez la console Web AEM. L’URL est `https://'[server]:[port]'/system/console/configMgr`
1. Ouvrez le **[!UICONTROL service de configuration commun aux formulaires].**
1. Dans le champ **[!UICONTROL Autoriser]**, **sélectionnez** Tous les utilisateurs : tous les utilisateurs, anonymes ou connectés, peuvent afficher un aperçu des pièces jointes, vérifier et signer des formulaires, puis cliquez sur **[!UICONTROL Enregistrer].** L’instance d’auteur est configurée pour utiliser [!DNL Adobe Sign].
1. Publiez la configuration.
1. Utilisez la [réplication](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/replication.html?lang=fr) pour créer une configuration identique sur les instances de publication correspondantes.

[!DNL Adobe Sign] est désormais intégré à AEM [!DNL Forms] et prêt à être utilisé dans les formulaires adaptatifs. Pour [utiliser le service Adobe Sign dans un formulaire adaptatif](../../forms/using/working-with-adobe-sign.md#configure-adobe-sign-for-an-adaptive-form), spécifiez le conteneur de configuration créé ci-dessus dans les propriétés du formulaire adaptatif.

## Connecter AEM Forms à Adobe Acrobat Sign Solutions pour le gouvernement {#adobe-acrobat-sign-for-government}

La connexion d’AEM Forms à Adobe Acrobat Sign Solutions pour le gouvernement est un processus en plusieurs étapes. Ce processus implique :

* la création de l’URL de redirection pour vos instances AEM ;
* le partage de l’URL de redirection et des champs d’application avec l’équipe Adobe Sign Solutions pour le gouvernement ;
* la réception des informations d’identification de l’équipe Adobe Sign ;
* l’utilisation des informations d’identification reçues pour connecter AEM Forms à Adobe Acrobat Sign Solutions pour le gouvernement.

![adobe-acrobat-sign-govt-workflow](/help/forms/using/assets/adobe-acrobat-sign-govt-workflow.png)

### Avant de commencer {#prerequisites-for-adobe-sign-for-acrobat-sign-for-government}

Avant de commencer à connecter AEM Forms à Adobe Acrobat Sign Solutions :

* assurez-vous que le compte [Adobe Acrobat Sign Solutions pour le gouvernement](https://opensource.adobe.com/acrobat-sign/signgov/gstarted.html#account-provisioning) est configuré ;
* vos serveurs AEM [!DNL Forms] sont [compatibles SSL](/help/sites-administering/ssl-by-default.md) ;
* vos serveurs AEM [!DNL Forms] utilisent une [clé cryptographique identique](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed) pour les instances de création et de publication.

### Connecter AEM Forms à Adobe Acrobat Sign Solutions pour le gouvernement {#connect-adobe-acrobat-sign-for-government}

#### Créer une URL de redirection pour votre instance AEM

1. Dans votre instance AEM Forms, accédez à **[!UICONTROL Outils]** ![marteau](assets/hammer.png) > **[!UICONTROL Général]** > **[!UICONTROL Navigateur de configurations]**.
1. Sur la page du **[!UICONTROL navigateur de configuration]**, appuyez sur **[!UICONTROL Créer]**.
1. Dans la boîte de dialogue **[!UICONTROL Créer une configuration]**, indiquez un **[!UICONTROL titre]** pour la configuration, activez **[!UICONTROL Configurations cloud]** et appuyez sur **[!UICONTROL Créer]**. Cela crée un conteneur de configuration. Vérifiez que le nom du conteneur/dossier ne contient aucun espace.

1. Accédez à **[!UICONTROL Outils]** ![marteau](assets/hammer.png) > **[!UICONTROL Services cloud]** > **[!UICONTROL Adobe Acrobat Sign]** et ouvrez le conteneur de configurations que vous avez créé à l’étape précédente. Lorsque vous créez un formulaire adaptatif, indiquez le nom du conteneur dans le champ **[!UICONTROL Conteneur de configurations]**.
1. Sur la page de configuration, appuyez sur **[!UICONTROL Créer]** pour créer une configuration [!DNL Adobe Acrobat Sign] dans AEM Forms.
1. Copiez l’URL de votre fenêtre de navigateur actuelle dans un bloc-notes à partir de l’URL. Cette URL est appelée `re-direct URL`. Dans la section suivante, partagez la `re-direct URL` et les `Scopes` avec l’équipe Adobe Sign et demandez des informations d’identification (identifiant client et secret client).

>[!NOTE]
>
>
* Une `re-direct URL` doit contenir un domaine de [niveau supérieur](https://fr.wikipedia.org/wiki/Domaine_de_premier_niveau). Par exemple, `https://adobe.com/libs/adobesign/cloudservices/adobesign/createcloudconfigwizard/cloudservices.html/conf/global`.
* N’utilisez pas d’URL locale en tant que `re-direct URL`. Par exemple, `https://localhost:4502/libs/adobesign/cloudservices/adobesign/createcloudconfigwizard/cloudservices.html/conf/global`.


#### Partager l’URL de redirection et les champs d’application avec l’équipe Adobe Sign et recevoir des informations d’identification

L’équipe Adobe Acrobat Sign Solutions pour le gouvernement exige que la `re-direct URL` et certains champs d’application soient activés pour votre application Adobe Acrobat Sign (répertoriés ci-dessous) afin de générer les informations d’identification (identifiant client et secret client) qui vous permettent de connecter AEM Forms à Adobe Acrobat Sign Solutions pour le gouvernement.

Partagez les `scopes` (répertoriés ci-dessous) et la `re-direct URL` créés et notés à la dernière étape de la section précédente avec votre personne représentante d’Adobe Acrobat Sign Solution pour le gouvernement [membre de l’équipe Adobe Professional Services](https://opensource.adobe.com/acrobat-sign/signgov/gstarted.html#password).

**_Portées_**

* [!DNL agreement_read]
* [!DNL agreement_write]
* [!DNL agreement_send]
* [!DNL widget_read]
* [!DNL widget_write]
* [!DNL workflow_read]
* [!DNL offline_access]

La personne représentante génère et partage alors les informations d’identification avec vous. Dans la section suivante, utilisez les informations d’identification (identifiant client et secret client) pour connecter AEM Forms à Adobe Acrobat Sign Solutions pour le gouvernement.

#### Utiliser des informations d’identification reçues pour connecter AEM Forms à Adobe Acrobat Sign Solutions pour le gouvenement

1. Ouvrez la `re-direct URL` dans votre navigateur. Vous avez créé et noté la `re-direct URL` dans la dernière étape de la section [création d’une URL de redirection sur votre instance AEM](#create-redirect-url).

1. Dans l’onglet **[!UICONTROL Général]** de la page **[!UICONTROL Créer une configuration Adobe Sign]**, spécifiez un **[!UICONTROL nom]** de configuration et appuyez sur **[!UICONTROL Suivant]**. Vous avez la possibilité d’indiquer un **[!UICONTROL titre]** et de rechercher et sélectionner une **[!UICONTROL vignette]** pour la configuration. Cliquez sur **[!UICONTROL Suivant]**.

1. Dans l’onglet **[!UICONTROL Paramètres]** de la page **[!UICONTROL Création d’une configuration Adobe Sign]**, pour l’option **[!UICONTROL Sélectionner une solution]**, sélectionnez [!DNL Adobe Acrobat Sign Solutions for Government].

   ![Adobe Acrobat Sign Solutions pour le gouvernement.](/help/forms/using/assets/adobe-sign-for-govt.png)

1. Dans le champ **[!UICONTROL E-mail]**, indiquez l’adresse e-mail associée à votre compte Adobe Acrobat Sign Solutions pour le gouvernement.

1. Le champ **[!UICONTROL URL OAuth]** spécifie le partitionnement de base de données Adobe Sign. Le champ contient l’URL par défaut. Ne modifiez pas l’URL.

1. Utilisez les informations d’identification partagées par le représentant ou la représentante Adobe Acrobat Sign Solution for Government ([membre de l’équipe Adobe Professional Services]) dans la section précédente en tant que [**[!UICONTROL ID client]** et **[!UICONTROL Secret client]**].

1. Sélectionnez l’option **[!UICONTROL Activer Adobe Acrobat Sign pour les pièces jointes]** pour ajouter les fichiers joints à un formulaire adaptatif au document [!DNL Adobe Acrobat Sign] correspondant envoyé à des fins de signature.

1. Appuyez sur **[!UICONTROL Se connecter à Adobe Sign]**. Lorsque vous êtes invité à fournir vos informations d’identification, indiquez le nom d’utilisateur et le mot de passe du compte utilisé lors de la création de l’application [!DNL Adobe Acrobat Sign]. Lorsque vous êtes invité.e à confirmer l’accès à `Adobe Acrobat Sign for Government Solutions`, cliquez sur **[!UICONTROL Autoriser l’accès]**. Si les informations d’identification sont correctes et que vous autorisez [!DNL AEM Forms] à accéder à votre compte de développement [!DNL Adobe Acrobat Sign], un message, semblable à celui ci-dessous, s’affiche pour vous notifier le succès de l’opération.

   ![Succès de la configuration Adobe Acrobat Sign Cloud](/help/forms/using/assets/adobe-sign-cloud-configuration-success.png)

   Lorsque vous êtes invité à fournir vos informations d’identification, indiquez le nom d’utilisateur et le mot de passe du compte utilisé lors de la création de l’application [!DNL Adobe Acrobat Sign]. Lorsque vous êtes invité.e à confirmer l’accès à `your account`, cliquez sur **[!UICONTROL Autoriser l’accès]**.

1. Appuyez sur **[!UICONTROL Créer]** pour créer la configuration .
1. Ouvrez la console Web AEM. L’URL est `https://'[server]:[port]'/system/console/configMgr`
1. Ouvrez le **[!UICONTROL service de configuration commun aux formulaires].**
1. Dans le champ **[!UICONTROL Autoriser]**, **sélectionnez** Tous les utilisateurs : tous les utilisateurs, anonymes ou connectés, peuvent afficher un aperçu des pièces jointes, vérifier et signer des formulaires, puis cliquez sur **[!UICONTROL Enregistrer].** L’instance d’auteur est configurée pour utiliser [!DNL Adobe Sign].

1. Publiez la configuration.
1. Utilisez la [réplication](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/replication.html?lang=fr) pour créer une configuration identique sur les instances de publication correspondantes.

Vous pouvez maintenant [utiliser l’ajout de champs Adobe Acrobat Sign dans un formulaire adaptatif](working-with-adobe-sign.md) ou dans un [Processus AEM](/help/forms/using/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step). Veillez à ajouter le conteneur de configurations utilisé pour la configuration du service cloud à tous les formulaires adaptatifs activés pour [!DNL Adobe Acrobat Sign]. Vous pouvez spécifier un conteneur de configurations à partir des propriétés d’un formulaire adaptatif.


## Configurer le planificateur [!DNL Adobe Sign] pour synchroniser l’état de signature {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

Un formulaire adaptatif avec activation d’[!DNL Adobe Sign] n’est envoyé que lorsque tous les signataires ont terminé le processus de signature. Par défaut, les services du planificateur [!DNL Adobe Sign] sont configurés pour vérifier (interroger) la réponse du signataire toutes les 24 heures. Vous pouvez modifier l’intervalle par défaut pour votre environnement. Procédez comme suit pour modifier l’intervalle par défaut :

1. Connectez-vous au serveur d’AEM [!DNL Forms] à l’aide de vos informations d’identification d’administrateur et accédez à **Outils** > **[!UICONTROL Opérations]** > **[!UICONTROL Console web]**.

   Vous pouvez également ouvrir l’URL suivante dans une fenêtre de navigateur :
   `https://[localhost]:'port'/system/console/configMgr`

1. Recherchez et ouvrez l’option **[!UICONTROL Service de configuration Adobe Sign]**. Spécifiez une [expression cron](https://en.wikipedia.org/wiki/Cron#CRON_expression) dans le champ **[!UICONTROL Expression du planificateur de mise à jour de l’état]** et cliquez sur **[!UICONTROL Enregistrer]**. Par exemple, pour exécuter le service de configuration tous les jours à minuit, indiquez `0 0 0 1/1 * ? *` dans le champ **[!UICONTROL Expression du planificateur de mise à jour de l’état]**.

L’intervalle par défaut pour synchroniser l’état d’[!DNL Adobe Sign] est désormais modifié.

## Articles connexes {#related-articles}

* [Utilisation d’Adobe Sign dans un formulaire adaptatif](../../forms/using/working-with-adobe-sign.md)
* [Adobe Sign avec des workflows axés sur les formulaires](/help/forms/using/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step)
* [Utiliser Adobe Sign avec AEM Forms (vidéo)](https://helpx.adobe.com/fr/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
