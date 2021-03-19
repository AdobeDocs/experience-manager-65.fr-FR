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
feature: Forms adaptatif, Adobe Sign
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 32%

---


# Intégrer [!DNL Adobe Sign] avec AEM [!DNL Forms]{#integrate-adobe-sign-with-aem-forms}

[!DNL Adobe Sign] active les workflows de signature électronique pour les formulaires adaptatifs. Les signatures électroniques améliorent les processus de traitement des documents pour les services juridiques, commercial, des ressources humaines, et bien d’autres domaines.

Dans un scénario typique de [!DNL Adobe Sign] et de formulaires adaptatifs, un utilisateur remplit un formulaire adaptatif à **demander un service**. Par exemple, un formulaire de demande de carte de paiement et d’allocation. Lorsqu’un utilisateur remplit, envoie et signe le formulaire de demande, le formulaire est envoyé au prestataire de services qui décidera des actions à entreprise. Le prestataire examine la demande et utilise [!DNL Adobe Sign] pour marquer la demande approuvée. Pour activer des workflows de signature électronique similaires, vous pouvez intégrer [!DNL Adobe Sign] à l&#39;AEM [!DNL Forms].

Pour utiliser [!DNL Adobe Sign] avec AEM [!DNL Forms], configurez [!DNL Adobe Sign] dans AEM Cloud Services :

## Conditions préalables {#prerequisites}

Pour intégrer [!DNL Adobe Sign] à l&#39;AEM [!DNL Forms], vous devez disposer des éléments suivants :

* Un compte de développeur [Adobe Sign actif.](https://acrobat.adobe.com/fr/fr/why-adobe/developer-form.html)
* Un serveur AEM [SSL](/help/sites-administering/ssl-by-default.md).[!DNL Forms]
* Une [application API Adobe Sign](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md).
* Informations d’identification (ID client et clé secrète client) de l’application API [!DNL Adobe Sign].
* Lors de la reconfiguration, supprimez la configuration [!DNL Adobe Sign] existante des instances d’auteur et de publication.
* Utilisez [un crypto-clé identique](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed) pour les instances d’auteur et de publication.

## Configurer [!DNL Adobe Sign] avec AEM [!DNL Forms] {#configure-adobe-sign-with-aem-forms}

Une fois les conditions préalables en place, effectuez les étapes suivantes pour configurer [!DNL Adobe Sign] avec AEM [!DNL Forms] sur l’instance d’auteur :

1. Sur l’AEM [!DNL Forms] instance d’auteur, accédez à **Outils** ![marteau](assets/hammer.png) > **[!UICONTROL Général]** > **[!UICONTROL Navigateur de configuration]**.
1. Sur la page **[!UICONTROL Navigateur de configuration]**, appuyez sur **[!UICONTROL Créer]**.
   * Pour plus d’informations, consultez la documentation de [Navigateur de configuration](/help/sites-administering/configurations.md).
1. Dans la boîte de dialogue **[!UICONTROL Créer une configuration]**, spécifiez un **[!UICONTROL Titre]** pour la configuration, activez **[!UICONTROL Configurations du cloud]** et appuyez sur **[!UICONTROL Créer]**. Un conteneur de configuration pour les services cloud est créé.
1. Accédez à **Outils** ![marteau](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]** et sélectionnez le conteneur de configuration que vous avez créé à l’étape ci-dessus.

   >[!NOTE]
   >
   >Vous pouvez exécuter les étapes 1 à 4 pour créer un conteneur de configuration et créer une configuration [!DNL Adobe Sign] dans le conteneur ou utiliser le dossier `global` existant dans **Outils** ![marteau](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]**. Si vous créez la configuration dans le nouveau conteneur de configuration, veillez à spécifier le nom du conteneur dans le champ **[!UICONTROL Conteneur de configuration]** lorsque vous créez un formulaire adaptatif.

   >[!NOTE]
   Vérifiez que l’URL de la page de configuration des services cloud commence par **HTTPS**. Si ce n’est pas le cas, [activez SSL](/help/sites-administering/ssl-by-default.md) pour le serveur AEM [!DNL Forms]

1. Sur la page de configuration, appuyez sur **[!UICONTROL Créer]** pour créer la configuration [!DNL Adobe Sign] dans AEM [!DNL Forms].
1. Dans l’onglet **[!UICONTROL Général]** de la page **[!UICONTROL Créer une configuration Adobe Sign]**, spécifiez un **[!UICONTROL Nom]** pour la configuration et appuyez sur **[!UICONTROL Suivant]**. Vous avez la possibilité d’indiquer un titre et de rechercher et de sélectionner une vignette pour la configuration.

1. Copiez l’URL dans la fenêtre active du navigateur vers un bloc-notes. Il est nécessaire de configurer l&#39;application [!DNL Adobe Sign] avec AEM[!DNL Forms].

1. Configurez les paramètres OAuth pour l&#39;application [!DNL Adobe Sign] :

   1. Ouvrez une fenêtre de navigateur et connectez-vous au compte de développeur [!DNL Adobe Sign].
   1. Sélectionnez l’application configurée pour l’AEM [!DNL Forms], puis appuyez sur **[!UICONTROL Configurer OAuth pour l’application]**.
   1. Copiez les **[!UICONTROL ID client]** et **[!UICONTROL Secret client]** dans un bloc-notes.
   1. Dans la zone **[!UICONTROL URL de redirection]**, ajoutez l’URL HTTPS copiée à l’étape précédente.
   1. Activez les paramètres OAuth suivants pour l&#39;application [!DNL Adobe Sign] et cliquez sur **[!UICONTROL Enregistrer]**.
   * aggrement_read
   * aggrement_write
   * aggrement_send
   * widget_write
   * workflow_read

   Pour obtenir des informations détaillées sur la configuration des paramètres OAuth pour une application [!DNL Adobe Sign] et l&#39;obtention des clés, voir [Configuration des paramètres Auth pour la documentation destinée aux développeurs de l&#39;application](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md).

   ![Configuration OAuth](assets/oauthconfig_new.png)

1. Revenez à la page **[!UICONTROL Créer une configuration Adobe Sign]**. Dans l’onglet **[!UICONTROL Paramètres]**, le champ **[!UICONTROL URL OAuth]** indique l’URL suivante par défaut :

   https://secure.na1.echosign.com/public/oauth

   où :

   **na1** fait référence au partitionnement de base de données par défaut.

   Vous pouvez modifier la valeur du partitionnement de base de données. Redémarrez le serveur pour pouvoir utiliser la nouvelle valeur pour le partitionnement de base de données.

   >[!NOTE]
   Assurez-vous que les configurations des instances d’auteur et de publication pointent vers le même partage. Si vous créez plusieurs configurations Adobe Sign pour une organisation, assurez-vous que toutes les configurations utilisent le même partage.

1. Spécifiez l’**ID client** (également appelé ID de l&#39;application) et la **clé secrète client** copiée à l’étape 8. Sélectionnez l’option **[!UICONTROL Activer pour les pièces jointes également]** pour ajouter les fichiers joints à un formulaire adaptatif au document Adobe Sign correspondant envoyé à des fins de signature.[!DNL Adobe Sign]

   Appuyez sur **[!UICONTROL Se connecter à Adobe Sign]**. Lorsque vous êtes invité à entrer des informations d’identification, indiquez le nom d’utilisateur et le mot de passe du compte utilisé lors de la création de l’application [!DNL Adobe Sign].

   Appuyez sur **[!UICONTROL Créer]** pour créer la configuration [!DNL Adobe Sign].

1. Ouvrez la console web AEM. L’URL est `https://'[server]:[port]'/system/console/configMgr`
1. Ouvrez le **[!UICONTROL service de configuration commun aux formulaires].**
1. Dans le champ **[!UICONTROL Autoriser]**, **sélectionnez** Tous les utilisateurs - Tous les utilisateurs, anonymes ou connectés, peuvent prévisualisation des pièces jointes, vérifier et signer des formulaires, puis cliquer sur **[!UICONTROL Enregistrer].** L’instance d’auteur est configurée pour être utilisée  [!DNL Adobe Sign].
1. Publiez la configuration.
1. Utilisez [réplication](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/configuring/replication.html) pour créer une configuration identique sur les instances de publication correspondantes.

Désormais, [!DNL Adobe Sign] est intégré à AEM [!DNL Forms] et prêt à l’emploi dans les formulaires adaptatifs. Pour [utiliser le service Adobe Sign dans un formulaire adaptatif](../../forms/using/working-with-adobe-sign.md#configure-adobe-sign-for-an-adaptive-form), spécifiez le conteneur de configuration créé ci-dessus dans les propriétés du formulaire adaptatif.



## Configurer le Planificateur [!DNL Adobe Sign] pour synchroniser l’état de signature {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

Un formulaire adaptatif [!DNL Adobe Sign] activé n’est envoyé qu’une fois que tous les signataires ont terminé le processus de signature. Par défaut, les services de Planificateur [!DNL Adobe Sign] sont programmés pour vérifier (sondage) la réponse du signataire toutes les 24 heures. Vous pouvez modifier l’intervalle par défaut pour votre environnement. Effectuez les étapes suivantes pour modifier l’intervalle par défaut :

1. Connectez-vous à AEM serveur [!DNL Forms] avec les informations d’identification d’administrateur et accédez à **Outils** > **[!UICONTROL Opérations]** > **[!UICONTROL Console Web]**.

   Vous pouvez également ouvrir l’URL suivante dans une fenêtre de navigateur :
   `https://[localhost]:'port'/system/console/configMgr`

1. Recherchez et ouvrez l’option **[!UICONTROL Service de configuration Adobe Sign]**. Spécifiez une [expression cron](https://en.wikipedia.org/wiki/Cron#CRON_expression) dans le champ **[!UICONTROL Expression du planificateur de mise à jour de l’état]** et cliquez sur **[!UICONTROL Enregistrer]**. Par exemple, pour exécuter le service de configuration tous les jours à 00:00, spécifiez `0 0 0 1/1 * ? *` dans le champ **[!UICONTROL Expression de l’Planificateur de mise à jour d’état]**.

L’intervalle par défaut pour l’état de synchronisation de [!DNL Adobe Sign] est maintenant modifié.

## Articles connexes {#related-articles}

* [Utilisation d’Adobe Sign dans un formulaire adaptatif](../../forms/using/working-with-adobe-sign.md)
* [Utilisation de Adobe Sign avec AEM Forms (vidéo)](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)


