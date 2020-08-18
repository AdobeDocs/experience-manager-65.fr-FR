---
title: Incorporation d’Adobe Sign à AEM Forms
seo-title: Incorporation d’Adobe Sign à AEM Forms
description: Découvrez comment configurer Adobe Sign pour AEM Forms
seo-description: Découvrez comment configurer Adobe Sign pour AEM Forms
uuid: e5049775-fb6c-4228-9823-e6a2811460da
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 1f28b257-5419-4a21-a54a-b20bf35530ac
docset: aem65
translation-type: tm+mt
source-git-commit: 1148ac87ef6ff1afa77788e9cbd180d883290bfe
workflow-type: tm+mt
source-wordcount: '986'
ht-degree: 68%

---


# Incorporation d’Adobe Sign à AEM Forms{#integrate-adobe-sign-with-aem-forms}

Adobe Sign autorise les processus de signature électronique pour les formulaires adaptatifs. Les signatures électroniques améliorent les processus de traitement des documents pour les services juridiques, commercial, des ressources humaines, et bien d’autres domaines.

Dans un scénario Adobe Sign et de formulaires adaptatifs standard, un utilisateur remplit un formulaire adaptatif pour effectuer une **demande de service**. Par exemple, un formulaire de demande de carte de paiement et d’allocation. Lorsqu’un utilisateur remplit, envoie et signe le formulaire de demande, le formulaire est envoyé au prestataire de services qui décidera des actions à entreprise. Le prestataire de services passe en revue la demande et utilise Adobe Sign pour marquer la demande approuvée. Pour activer les processus de signature électronique similaires, vous pouvez intégrer Adobe Sign à AEM Forms.

Pour utiliser Adobe Sign avec AEM Forms, configurez Adobe Sign dans AEM Cloud Services :

## Conditions préalables {#prerequisites}

Vous avez besoin de ce qui suit pour intégrer Adobe Sign à AEM Forms :

* Un compte de développeur [Adobe Sign actif.](https://acrobat.adobe.com/fr/fr/why-adobe/developer-form.html)
* Un serveur AEM Forms [SSL](/help/sites-administering/ssl-by-default.md).
* Une [application API Adobe Sign](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md).
* Informations d’identification (ID client et secret client) de l’application API Adobe Sign.
* Lors de la reconfiguration, supprimez la configuration Adobe Sign existante des instances d’auteur et de publication.

## Configurer Adobe Sign avec AEM Forms {#configure-adobe-sign-with-aem-forms}

Une fois les conditions préalables en place, procédez comme suit pour configurer Adobe Sign avec AEM Forms sur l’instance d’auteur :

1. On AEM Forms author instance, navigate to **Tools** ![hammer](assets/hammer.png) > **General** > **Configuration Browser**.
1. On the **[!UICONTROL Configuration Browser]** page, tap **[!UICONTROL Create]**.
1. In the **[!UICONTROL Create Configuration]** dialog, specify a **[!UICONTROL Title]** for the configuration, enable **[!UICONTROL Cloud Configurations]**, and tap **[!UICONTROL Create]**. Un conteneur de configuration pour les services cloud est créé.
1. Navigate to **Tools** ![hammer](assets/hammer.png) > **Cloud Services** > **Adobe Sign** and select the configuration container you created in the above step.

   >[!NOTE]
   >
   >Vérifiez que l’URL de la page de configuration des services cloud commence par **HTTPS**. Si ce n’est pas le cas, [activez SSL](/help/sites-administering/ssl-by-default.md) pour le serveur AEM Forms.

1. On the configuration page, tap **[!UICONTROL Create]** to create Adobe Sign configuration in AEM Forms.
1. In the **[!UICONTROL General]** tab of the **[!UICONTROL Create Adobe Sign Configuration]** page, specify a **Name** for the configuration and tap **Next**. Vous avez la possibilité d’indiquer un titre et de rechercher et de sélectionner une vignette pour la configuration.

1. Copiez l’URL dans la fenêtre active du navigateur vers un bloc-notes. Vous en avez besoin pour configurer l’application Adobe Sign avec AEM Forms.

1. Configurez les paramètres OAuth pour l’application Adobe Sign :

   1. Ouvrez une fenêtre de navigateur et connectez-vous au compte de développeur Adobe Sign.
   1. Sélectionnez l’application configurée pour AEM Forms, puis appuyez sur Configurer OAuth pour l’application.
   1. Dans la zone **URL de redirection**, ajoutez l’URL HTTPS copiée à l’étape précédente et cliquez sur **Enregistrer**.
   1. Activez les paramètres OAuth suivants pour l’application Adobe Sign et cliquez sur **Enregistrer**.
   * aggrement_read
   * aggrement_write
   * aggrement_send
   * widget_write
   * workflow_read

   Pour obtenir des informations détaillées sur la configuration des paramètres OAuth pour une application Adobe Sign et l’obtention des clés, voir [Configurer les paramètres oAuth pour la documentation](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md) dans la documentation du développeur.

   ![Configuration OAuth](assets/oauthconfig_new.png)

1. Revenez à la page **Créer une configuration Adobe Sign**. Dans l’onglet **[!UICONTROL Paramètres]**, le champ **[!UICONTROL URL OAuth]** indique l’URL suivante par défaut :

   https://secure.na1.echosign.com/public/oauth

   où :

   **na1** fait référence au partitionnement de base de données par défaut.

   Vous pouvez modifier la valeur du partitionnement de base de données. Redémarrez le serveur pour pouvoir utiliser la nouvelle valeur pour le partitionnement de base de données.

1. Specify the **Client ID** (also referred to as Application ID) and **Client Secret**. Sélectionnez l’option **Activer Adobe Sign pour les pièces jointes également** pour ajouter les fichiers joints à un formulaire adaptatif au document Adobe Sign correspondant envoyé à des fins de signature.

   Tap **[!UICONTROL Connect to Adobe Sign]**. Lorsque vous êtes invité à fournir vos informations d’identification, indiquez le nom d’utilisateur et le mot de passe du compte utilisé lors de la création de l’application Adobe Sign.

   Appuyez sur **[!UICONTROL Créer]** pour créer la configuration Adobe Sign.

1. Ouvrez la console web AEM. The URL is `https://'[server]:[port]'/system/console/configMgr`
1. Ouvrez le **service de configuration commun aux formulaires.**
1. In the **Allow** field, **select** All users - All the users, anonymous or logged in, can preview attachments, verify and sign forms, and click **Save.** L’instance d’auteur est configurée pour utiliser Adobe Sign.
1. Sur l’instance [Publication](/help/sites-deploying/deploy.md), connectez-vous et ouvrez l’URL suivante :

   `https://<server-name>:<port>/libs/granite/configurations/content/view.html/conf`

1. Répétez les étapes 1 à 12 pour configurer Adobe Sign avec AEM Forms. Utilisez le même titre pour la configuration (comme indiqué à l’étape 3) et le même nom (comme indiqué à l’étape 6) pour répliquer les paramètres configurés sur l’instance d’auteur.

   Désormais, Adobe Sign est intégré à AEM Forms et prêt à être utilisé dans les formulaires adaptatifs. Pour [utiliser le service Adobe Sign dans un formulaire adaptatif](../../forms/using/working-with-adobe-sign.md#configure-adobe-sign-for-an-adaptive-form), spécifiez le conteneur de configuration créé ci-dessus dans les propriétés du formulaire adaptatif.

   >[!NOTE]
   > Si vous disposez d’un environnement durci et n’avez pas accès à l’URL `https://<server-name>:<port>/libs/granite/configurations/content/view.html/conf`, effectuez la configuration sur l’auteur et utilisez [la réplication](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/configuring/replication.html) pour créer une configuration identique sur les instances de publication correspondantes.

## Configurer le planificateur Adobe Sign pour synchroniser l’état de signature {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

Un formulaire adaptatif Adobe Sign est envoyé uniquement après que tous les signataires ont terminé le processus de signature. Par défaut, les services du planificateur Adobe Sign doivent vérifier (interroger) la réponse du signataire toutes les 24 heures. Vous pouvez modifier l’intervalle par défaut pour votre environnement. Effectuez les étapes suivantes pour modifier l’intervalle par défaut :

1. Connectez-vous au serveur AEM Forms avec les informations d’identification d’administrateur et accédez à **Outils**> **Opérations**> **Console Web**.

   Vous pouvez également ouvrir l’URL suivante dans une fenêtre de navigateur :
   `https://[localhost]:'port'/system/console/configMgr`

1. Recherchez et ouvrez l’option **Service de configuration Adobe Sign**. Spécifiez une [expression cron](https://en.wikipedia.org/wiki/Cron#CRON_expression) dans le champ **Expression du planificateur de mise à jour de l’état** et cliquez sur **Enregistrer**. Par exemple, pour exécuter le service de configuration tous les jours à 00:00, indiquez `0 0 0 1/1 * ? *` dans le champ Expression **de l’Planificateur** Status Update.

L’intervalle par défaut pour synchroniser l’état d’Adobe Sign est désormais modifié.

## Related Articles {#related-articles}

* [Utilisation d’Adobe Sign dans un formulaire adaptatif](../../forms/using/working-with-adobe-sign.md)
* [Utilisation de Adobe Sign avec AEM Forms (vidéo)](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
* [Incorporation d’Adobe Sign à AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md)

