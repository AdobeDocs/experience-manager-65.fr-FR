---
title: Incorporation d’Adobe Sign à AEM Forms
seo-title: Integrate Adobe Sign with AEM Forms
description: Découvrez comment configurer Adobe Sign pour AEM Forms
seo-description: Learn how to configure Adobe Sign for AEM Forms
uuid: e5049775-fb6c-4228-9823-e6a2811460da
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 1f28b257-5419-4a21-a54a-b20bf35530ac
docset: aem65
feature: Adaptive Forms, Adobe Sign
exl-id: 52146038-1582-41b8-aee0-215d04bb91d7
source-git-commit: e46d77caf831324f077315df43b8f3a0267bef9a
workflow-type: tm+mt
source-wordcount: '1091'
ht-degree: 92%

---

# Intégrer [!DNL Adobe Sign]avec AEM [!DNL Forms]{#integrate-adobe-sign-with-aem-forms}

[!DNL Adobe Sign] permet des processus de signature électronique pour les formulaires adaptatifs. Les signatures électroniques améliorent les processus de traitement des documents pour les services juridiques, commercial, des ressources humaines, et bien d’autres domaines.

Dans un scénario de formulaires typiques [!DNL Adobe Sign] et adaptatifs, un utilisateur remplit un formulaire adaptatif pour **effectuer une demande de service**. Par exemple, un formulaire de demande de carte de paiement et d’allocation. Lorsqu’un utilisateur remplit, envoie et signe le formulaire de demande, le formulaire est envoyé au prestataire de services qui décidera des actions à entreprise. Le prestataire de services passe en revue la demande et utilise [!DNL Adobe Sign] pour marquer la demande comme approuvée. Pour activer les processus de signature électronique similaires, vous pouvez intégrer [!DNL Adobe Sign] à AEM [!DNL Forms].

Pour utiliser [!DNL Adobe Sign] avec AEM[!DNL Forms], configurez [!DNL Adobe Sign] dans AEM Cloud Services :

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
1. Dans la boîte de dialogue **[!UICONTROL Créer une configuration]**, indiquez un **[!UICONTROL titre]** pour la configuration, activez **[!UICONTROL Configurations cloud]** et appuyez sur **[!UICONTROL Créer]**. Un conteneur de configuration pour les services cloud est créé.
1. Accédez à **Outils** ![marteau](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]** et sélectionnez le conteneur de configuration que vous avez créé à l’étape précédente.

   >[!NOTE]
   >
   >Vous pouvez exécuter les étapes 1 à 4 pour créer un nouveau conteneur de configuration et créer une configuration [!DNL Adobe Sign] dans le conteneur ou utiliser le dossier `global` dans **Outils** ![marteau](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]**. Si vous créez la configuration dans le nouveau conteneur de configuration, veillez à spécifier le nom du conteneur dans le champ **[!UICONTROL Conteneur de configuration]** lorsque vous créez un formulaire adaptatif.

   >[!NOTE]
   Vérifiez que l’URL de la page de configuration des services cloud commence par **HTTPS**. Si ce n’est pas le cas, [activez SSL](/help/sites-administering/ssl-by-default.md) pour le serveur AEM [!DNL Forms]

1. Sur la page de configuration, appuyez sur **[!UICONTROL Créer]** pour créer [!DNL Adobe Sign] une configuration dans AEM [!DNL Forms].
1. Dans l’onglet **[!UICONTROL Généralités]** de la page **[!UICONTROL Créer une configuration Adobe Sign]**, spécifiez un **[!UICONTROL Nom]** de configuration et appuyez sur **[!UICONTROL Suivant]**. Vous avez la possibilité d’indiquer un titre et de rechercher et de sélectionner une vignette pour la configuration.

1. Copiez l’URL dans la fenêtre active du navigateur dans un bloc-notes. Vous en avez besoin pour configurer l’application [!DNL Adobe Sign] avec AEM [!DNL Forms].

1. Dans le **[!UICONTROL Paramètres]** , **[!UICONTROL URL OAuth]** contient l’URL par défaut. Le format de l’URL est:

   `https://<shard>/public/oAuth/v2`

   Par exemple :
   `https://secure.na1.echosign.com/public/oauth/v2`

   où :

   **na1** fait référence au partitionnement de base de données par défaut. Vous pouvez modifier la valeur du partitionnement de base de données. Assurez-vous que les configurations cloud de [!DNL  Adobe Sign] pointent vers le [fragment correct](https://helpx.adobe.com/fr/sign/using/identify-account-shard.html).

   Si vous créez une autre configuration [!DNL Adobe Sign] pour une fonctionnalité ou un composant Adobe Experience Manager, assurez-vous que toutes les configurations cloud de [!DNL Adobe Sign] pointent vers le même fragment.

   >[!NOTE]
   Conserver la variable **Création d’une configuration Adobe Sign** s’ouvre. Ne le fermez pas. Vous pouvez récupérer **ID client** et **Secret du client** après la configuration des paramètres OAuth pour la variable [!DNL Adobe Sign] comme décrit dans les étapes à venir.


1. Configurez les paramètres OAuth pour l’application [!DNL Adobe Sign] :

   1. Ouvrez une fenêtre de navigateur et connectez-vous au compte de développeur [!DNL Adobe Sign].
   1. Sélectionnez l’application configurée pour AEM [!DNL Forms], puis appuyez sur **[!UICONTROL Configurer OAuth pour l’application]**.
   1. Copiez l’**[!UICONTROL ID client]** et le **[!UICONTROL Secret du client]** vers un bloc-notes.
   1. Dans la zone **[!UICONTROL URL de redirection]**, ajoutez l’URL HTTPS copiée à l’étape précédente.
   1. Activez les paramètres OAuth suivants pour l’application [!DNL Adobe Sign] et cliquez sur **[!UICONTROL Enregistrer]**.
   * aggrement_read
   * aggrement_write
   * aggrement_send
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
   Assurez-vous que les configurations des instances d’auteur et de publication pointent vers la même partition. Si vous créez plusieurs configurations Adobe Sign pour une organisation, assurez-vous que toutes utilisent la même partition.

1. Revenez à la page **[!UICONTROL Créer une configuration Adobe Sign]**. Dans le **[!UICONTROL Paramètres]** , spécifiez la variable **ID client** (également appelé ID d’application) et **Secret du client**. Utilisez la variable [ID client et secret client de l’application Adobe Sign](https://opensource.adobe.com/acrobat-sign/developer_guide/helloworld.html#get-the-app-id-and-secret) créé pour AEM Forms.

1. Sélectionnez l’option **[!UICONTROL Activer pour les pièces jointes également]** pour ajouter les fichiers joints à un formulaire adaptatif au document Adobe Sign correspondant envoyé à des fins de signature.[!DNL Adobe Sign]

1. Appuyez sur **[!UICONTROL Se connecter à Adobe Sign]**. Lorsque vous êtes invité à fournir vos informations d’identification, indiquez le nom d’utilisateur et le mot de passe du compte utilisé lors de la création de l’application [!DNL Adobe Sign]. 

1. Appuyez sur **[!UICONTROL Créer]** pour créer la configuration [!DNL Adobe Sign].

1. Ouvrez la console Web AEM. L’URL est `https://'[server]:[port]'/system/console/configMgr`
1. Ouvrez le **[!UICONTROL service de configuration commun aux formulaires].**
1. Dans le champ **[!UICONTROL Autoriser]**, **sélectionnez** Tous les utilisateurs : tous les utilisateurs, anonymes ou connectés, peuvent afficher un aperçu des pièces jointes, vérifier et signer des formulaires, puis cliquez sur **[!UICONTROL Enregistrer].** L’instance d’auteur est configurée pour utiliser [!DNL Adobe Sign].
1. Publiez la configuration.
1. Utilisez la [réplication](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/replication.html?lang=fr) pour créer une configuration identique sur les instances de publication correspondantes.

[!DNL Adobe Sign] est désormais intégré à AEM [!DNL Forms] et prêt à être utilisé dans les formulaires adaptatifs. Pour [utiliser le service Adobe Sign dans un formulaire adaptatif](../../forms/using/working-with-adobe-sign.md#configure-adobe-sign-for-an-adaptive-form), spécifiez le conteneur de configuration créé ci-dessus dans les propriétés du formulaire adaptatif.



## Configurer le planificateur [!DNL Adobe Sign] pour synchroniser l’état de signature {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

Un formulaire adaptatif avec activation d’[!DNL Adobe Sign] n’est envoyé que lorsque tous les signataires ont terminé le processus de signature. Par défaut, les services du planificateur [!DNL Adobe Sign] sont configurés pour vérifier (interroger) la réponse du signataire toutes les 24 heures. Vous pouvez modifier l’intervalle par défaut pour votre environnement. Procédez comme suit pour modifier l’intervalle par défaut :

1. Connectez-vous au serveur d’AEM [!DNL Forms] à l’aide de vos informations d’identification d’administrateur et accédez à **Outils** > **[!UICONTROL Opérations]** > **[!UICONTROL Console web]**.

   Vous pouvez également ouvrir l’URL suivante dans une fenêtre de navigateur :
   `https://[localhost]:'port'/system/console/configMgr`

1. Recherchez et ouvrez l’option **[!UICONTROL Service de configuration Adobe Sign]**. Spécifiez une [expression cron](https://en.wikipedia.org/wiki/Cron#CRON_expression) dans le champ **[!UICONTROL Expression du planificateur de mise à jour de l’état]** et cliquez sur **[!UICONTROL Enregistrer]**. Par exemple, pour exécuter le service de configuration tous les jours à minuit, indiquez `0 0 0 1/1 * ? *` dans le champ **[!UICONTROL Expression du planificateur de mise à jour de l’état]**.

L’intervalle par défaut pour synchroniser l’état d’[!DNL Adobe Sign] est désormais modifié.

## Articles connexes {#related-articles}

* [Utilisation d’Adobe Sign dans un formulaire adaptatif](../../forms/using/working-with-adobe-sign.md)
* [Utiliser Adobe Sign avec AEM Forms (vidéo)](https://helpx.adobe.com/fr/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
