---
title: 'Activation des statistiques sur les ressources via DTM  '
description: Découvrez comment utiliser la gestion dynamique des balises Adobe pour activer les statistiques sur les ressources.
contentOwner: AG
role: Business Practitioner, Administrator
feature: Asset Insights,Asset Reports
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 34%

---


# Activation des statistiques sur les ressources via DTM   {#enable-asset-insights-through-dtm}

La gestion dynamique des balises Adobe est un outil permettant d’activer vos outils de marketing numérique. Il est fourni gratuitement aux clients d’Adobe Analytics. Vous pouvez personnaliser votre code de suivi pour permettre aux solutions CMS tierces d’utiliser Asset Insights ou utiliser la gestion dynamique des balises pour insérer des balises Asset Insights. Les statistiques sont uniquement prises en charge et fournies pour les images.

>[!CAUTION]
>
>La gestion dynamique des balises de l’Adobe est abandonnée en faveur de [!DNL Adobe Experience Platform Launch] et atteindra bientôt [la fin de vie](https://medium.com/launch-by-adobe/dtm-plans-for-a-sunset-3c6aab003a6f). L’Adobe vous recommande [d’utiliser [!DNL Launch] pour obtenir des informations sur les ressources](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/advanced/asset-insights-launch-tutorial.html).

Effectuez les étapes ci-dessous pour activer les Statistiques sur les ressources grâce à DTM.

1. Cliquez sur le logo du Experience Manager et accédez à **[!UICONTROL Outils]** > **[!UICONTROL Ressources]** > **[!UICONTROL Configuration des connaissances]**.
1. [Configuration du déploiement des Experience Manager avec le Cloud Service de gestion dynamique des balises](/help/sites-administering/dtm.md)

   Le jeton API doit être disponible une fois que vous vous connectez à [https://dtm.adobe.com](https://dtm.adobe.com/) et que vous visitez **[!UICONTROL Paramètres du compte]** dans le Profil utilisateur. Cette étape n’est pas requise du point de vue des statistiques sur les ressources, car l’intégration de sites Experience Manager avec les statistiques sur les ressources est toujours en cours d’élaboration.

1. Connectez-vous à [https://dtm.adobe.com](https://dtm.adobe.com/) et sélectionnez une société, le cas échéant.
1. Créer ou ouvrir une propriété Web existante

   * Sélectionnez l&#39;onglet **[!UICONTROL Propriétés Web]**, puis cliquez sur **[!UICONTROL Ajouter la propriété]**.

   * Mettez à jour les champs selon vos besoins, puis cliquez sur **[!UICONTROL Créer une propriété]**. Voir [documentation](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html).

   ![Créer une propriété web d’édition](assets/Create-edit-web-property.png)

1. Dans l&#39;onglet **[!UICONTROL Règles]**, sélectionnez **[!UICONTROL Règles de chargement de page]** dans le volet de navigation et cliquez sur **[!UICONTROL Créer une règle]**.

   ![chlimage_1-58](assets/chlimage_1-194.png)

1. Développez **[!UICONTROL Balises JavaScript /tierces]**. Cliquez ensuite sur **[!UICONTROL Ajouter un nouveau script]** dans l’onglet **[!UICONTROL HTML séquentiel]** pour ouvrir la boîte de dialogue Script.

   ![chlimage_1-59](assets/chlimage_1-195.png)

1. Cliquez sur le logo du Experience Manager et accédez à **[!UICONTROL Outils]** > **[!UICONTROL Ressources]**.
1. Cliquez sur **[!UICONTROL Suivi de page d&#39;informations]**, copiez le code de suivi, puis collez-le dans la boîte de dialogue Script que vous avez ouverte à l&#39;étape 6. Enregistrez les modifications.

   >[!NOTE]
   >
   >* `AppMeasurement.js` est supprimée. Il devrait être disponible via l’outil de gestion dynamique des balises Adobe Analytics.
   >* L&#39;appel à `assetAnalytics.dispatcher.init()` est supprimé. Le système s’attend à ce que la fonction soit appelée une fois le chargement de l’outil de gestion dynamique des balises Adobe Analytics terminé.
   >* Selon l’emplacement d’hébergement du suivi de page des statistiques sur les ressources (Experience Manager, CDN, etc.), l’origine de la source du script peut nécessiter des modifications.
   >* Pour le suivi des pages hébergé par un Experience Manager, la source doit pointer vers une instance de publication à l’aide du nom d’hôte de l’instance de répartiteur.


1. Accédez à l’adresse `https://dtm.adobe.com`. Cliquez sur **[!UICONTROL Aperçu]** dans la propriété web et cliquez sur **[!UICONTROL Ajouter un outil]** ou ouvrez un outil Adobe Analytics existant. Lors de la création de l&#39;outil, vous pouvez définir **[!UICONTROL Méthode de configuration]** sur **[!UICONTROL Automatique]**.

   ![Outil Ajoute Adobe Analytics](assets/Add-Adobe-Analytics-Tool.png)

   Sélectionnez des suites de rapports de production/intermédiaires, selon les besoins.

1. Développez **[!UICONTROL Gestion des bibliothèques]** et assurez-vous que **[!UICONTROL Charger la bibliothèque à]** est défini sur **[!UICONTROL Haut de page]**.

   ![chlimage_1-61](assets/chlimage_1-197.png)

1. Développez **[!UICONTROL Personnaliser le code de page]**, puis cliquez sur **[!UICONTROL Ouvrir l’éditeur]**.

   ![chlimage_1-62](assets/chlimage_1-198.png)

1. Collez le code suivant dans la fenêtre :

   ```Java
   var sObj;
   
   if (arguments.length > 0) {
     sObj = arguments[0];
   } else {
     sObj = _satellite.getToolsByType('sc')[0].getS();
   }
   _satellite.notify('in assetAnalytics customInit');
   (function initializeAssetAnalytics() {
     if ((!!window.assetAnalytics) && (!!assetAnalytics.dispatcher)) {
       _satellite.notify('assetAnalytics ready');
       /** NOTE:
           Copy over the call to 'assetAnalytics.dispatcher.init()' from Assets Pagetracker
           Be mindful about changing the AppMeasurement object as retrieved above.
       */
       assetAnalytics.dispatcher.init(
             "",  /** RSID to send tracking-call to */
             "",  /** Tracking Server to send tracking-call to */
             "",  /** Visitor Namespace to send tracking-call to */
             "",  /** listVar to put comma-separated-list of Asset IDs for Asset Impression Events in tracking-call, e.g. 'listVar1' */
             "",  /** eVar to put Asset ID for Asset Click Events in, e.g. 'eVar3' */
             "",  /** event to include in tracking-calls for Asset Impression Events, e.g. 'event8' */
             "",  /** event to include in tracking-calls for Asset Click Events, e.g. 'event7' */
             sObj  /** [OPTIONAL] if the webpage already has an AppMeasurement object, include the object here. If unspecified, Pagetracker Core shall create its own AppMeasurement object */
             );
       sObj.usePlugins = true;
       sObj.doPlugins = assetAnalytics.core.updateContextData;
       assetAnalytics.core.optimizedAssetInsights();
     }
     else {
       _satellite.notify('assetAnalytics not available. Consider updating the Custom Page Code', 4);
     }
   })();
   ```

   * La règle de chargement de page dans DTM inclut uniquement le code `pagetracker.js`. Tous les champs `assetAnalytics` sont considérés comme des remplacements des valeurs par défaut. Ils ne sont pas requis par défaut.
   * Le code appelle `assetAnalytics.dispatcher.init()` après s&#39;être assuré que `_satellite.getToolsByType('sc')[0].getS()` est initialisé et que `assetAnalytics,dispatcher.init` est disponible. Par conséquent, vous pouvez ignorer son ajout à l’étape 11.
   * Comme indiqué dans les commentaires du code de suivi de page d&#39;informations (**[!UICONTROL Outils > Ressources > Suivi de page d&#39;informations]**), lorsque le suivi de page ne crée pas d&#39;objet `AppMeasurement`, les trois premiers arguments (RSID, Serveur de suivi et Espace de nommage Visiteur) ne sont pas pertinents. Des chaînes vides sont transmises à la place pour mettre ceci en évidence.\
      Les arguments restants correspondent à ce qui est configuré sur la page Configuration des statistiques (**[!UICONTROL Outils > Ressources > Configuration des statistiques]**).
   * L’objet AppMeasurement est récupéré en interrogeant `satelliteLib` pour tous les moteurs SiteCatalyst disponibles. Si plusieurs balises sont configurées, modifiez l’index du sélecteur de tableau de manière appropriée. Les entrées du tableau sont triées en fonction des outils SiteCatalyst disponibles dans l’interface de gestion dynamique des balises.

1. Enregistrez et fermez la fenêtre Editeur de code, puis enregistrez les modifications dans la configuration de l’outil.
1. Dans l&#39;onglet **[!UICONTROL Approbations]**, approuvez les deux approbations en attente. La balise DTM est prête à être insérée sur votre page web. Pour plus d’informations sur l’insertion de balises DTM dans les pages Web, voir [Intégration de la gestion dynamique des balises dans les modèles de page personnalisés](https://blogs.adobe.com/experiencedelivers/experience-management/integrating-dtm-custom-aem6-page-template/).
