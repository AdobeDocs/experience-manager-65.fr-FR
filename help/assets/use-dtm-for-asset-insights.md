---
title: Activation d’Assets Insights via la gestion dynamique des balises
description: Découvrez comment utiliser la gestion dynamique des balises d’Adobe pour activer Assets Insights.
contentOwner: AG
role: User, Admin
feature: Asset Insights,Asset Reports
exl-id: 80e8f84e-3235-4212-9dcd-6acdb9067893
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '631'
ht-degree: 95%

---

# Activation d’Assets Insights via la gestion dynamique des balises {#enable-asset-insights-through-dtm}

La gestion dynamique des balises Adobe est un outil permettant d’activer vos outils de marketing numérique. Il est fourni gratuitement aux clients d’Adobe Analytics. Vous pouvez personnaliser votre code de suivi pour permettre aux solutions CMS tierces d’utiliser Assets Insights ou la gestion dynamique des balises pour insérer des balises Assets Insights. Les informations sont uniquement prises en charge et fournies pour les images.

>[!CAUTION]
>
>La gestion dynamique des balises d’Adobe est obsolète et remplacée par [!DNL Adobe Experience Platform]. Elle atteindra bientôt sa [fin de vie](https://medium.com/launch-by-adobe/dtm-plans-for-a-sunset-3c6aab003a6f). Adobe vous recommande d’[utiliser  [!DNL Adobe Experience Platform]  pour Assets Insights](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/advanced/asset-insights-launch-tutorial.html?lang=fr).

Effectuez ces étapes pour activer Assets Insights grâce à la gestion dynamique des balises.

1. Cliquez sur le logo Experience Manager, puis accédez à **[!UICONTROL Outils]** > **[!UICONTROL Ressources]** > **[!UICONTROL Configuration d’Insights]**.
1. [Configuration du déploiement d’Experience Manager avec la gestion dynamique des balises en service cloud](/help/sites-administering/dtm.md)

   Le jeton API devrait être disponible quand vous vous connectez à [https://dtm.adobe.com](https://dtm.adobe.com/) et que vous consultez les **[!UICONTROL Paramètres du compte]** via le profil utilisateur. Par rapport à Assets Insights, cette étape n’est pas nécessaire car l’intégration d’Experience Manager Sites à Assets Insights est encore en cours.

1. Connectez-vous à [https://dtm.adobe.com](https://dtm.adobe.com/) et sélectionnez une entreprise, comme approprié.
1. Créez ou ouvrez une propriété web existante.

   * Sélectionnez l’onglet **[!UICONTROL Propriétés web]**, puis cliquez sur **[!UICONTROL Ajouter une propriété]**.

   * Mettez les champs à jour selon vos besoins et cliquez sur **[!UICONTROL Créer une propriété]**. Consultez la [documentation](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=fr).

   ![Créer une propriété web de modification](assets/Create-edit-web-property.png)

1. Sous l’onglet **[!UICONTROL Règles]**, sélectionnez **[!UICONTROL Règles de chargement de page]** dans le volet de navigation et cliquez sur **[!UICONTROL Créer une nouvelle règle]**.

   ![chlimage_1-58](assets/chlimage_1-194.png)

1. Développez **[!UICONTROL Balises JavaScript/tierces]**. Cliquez ensuite sur **[!UICONTROL Ajouter un nouveau script]** sous l’onglet **[!UICONTROL HTML séquentiel]** pour ouvrir la boîte de dialogue Script.

   ![chlimage_1-59](assets/chlimage_1-195.png)

1. Cliquez sur le logo d’Experience Manager, puis accédez à **[!UICONTROL Outils]** > **[!UICONTROL Ressources]**.
1. Cliquez sur **[!UICONTROL Dispositif de suivi de la page d’informations]**, copiez le code de suivi, puis collez-le dans la boîte de dialogue Script que vous avez ouverte à l’étape 6. Enregistrez les modifications.

   >[!NOTE]
   >
   >* `AppMeasurement.js` est supprimé. Il devrait être disponible via l’outil de gestion dynamique des balises Adobe Analytics.
   >* L’appel à `assetAnalytics.dispatcher.init()` est supprimé. La fonction devrait être appelée une fois le chargement de l’outil de gestion dynamique des balises Adobe Analytics terminé.
   >* Selon l’emplacement d’hébergement du dispositif de suivi de la page de statistiques sur les ressources (par exemple, Experience Manager, CDN, etc.), l’origine de la source du script peut nécessiter des modifications.
   >* Pour le dispositif de suivi de la page hébergé sur Experience Manager, la source doit indiquer une instance de publication utilisant le nom d’hôte de l’instance du Dispatcher.

1. Accédez à l’adresse `https://dtm.adobe.com`. Cliquez sur **[!UICONTROL Aperçu]** dans la propriété web et cliquez sur **[!UICONTROL Ajouter un outil]**, ou ouvrez un outil Adobe Analytics existant. Pendant la création de l’outil, vous pouvez définir la **[!UICONTROL méthode de configuration]** sur **[!UICONTROL Automatique]**.

   ![Ajoutez l’outil Adobe Analytics](assets/Add-Adobe-Analytics-Tool.png)

   Sélectionnez des suites de rapports d’exploitation ou intermédiaires, selon vos besoins.

1. Développez **[!UICONTROL Gestion de la bibliothèque]** et assurez-vous que l’option **[!UICONTROL Charger la bibliothèque sur]** est définie sur **[!UICONTROL Haut de la page]**.

   ![chlimage_1-61](assets/chlimage_1-197.png)

1. Développez **[!UICONTROL Personnaliser le code de page]** et cliquez sur **[!UICONTROL Ouvrir l’Éditeur]**.

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
             "",  /** listVar to put comma-separated-list of Asset IDs for Asset Impression Events in tracking-call, for example, 'listVar1' */
             "",  /** eVar to put Asset ID for Asset Click Events in, for example, 'eVar3' */
             "",  /** event to include in tracking-calls for Asset Impression Events, for example, 'event8' */
             "",  /** event to include in tracking-calls for Asset Click Events, for example, 'event7' */
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

   * La règle de chargement de page dans la gestion dynamique des balises inclut uniquement le code `pagetracker.js`. Tous les champs `assetAnalytics` sont considérés comme des remplacements des valeurs par défaut. Ils ne sont pas requis par défaut.
   * Le code appelle `assetAnalytics.dispatcher.init()` après s’être assuré que `_satellite.getToolsByType('sc')[0].getS()` est initialisé et que `assetAnalytics,dispatcher.init` est disponible. Par conséquent, vous pouvez ignorer son ajout à l’étape 11.
   * Comme indiqué dans les commentaires dans le code du dispositif de suivi de la page d’informations (**[!UICONTROL Outils > Ressources > Dispositif de suivi de la page d’informations]**), lorsque le dispositif de suivi de la page ne crée pas d’objet `AppMeasurement`, les trois premiers arguments (RSID, Serveur de suivi et Espace de noms du visiteur) ne sont pas pertinents. Des chaînes vides sont transmises à la place pour mettre ceci en évidence.\
     Les arguments restants correspondent à ce qui est configuré sur la page Configuration d’Insights (**[!UICONTROL Outils > Ressources > Configuration d’Insights]**).
   * L’objet AppMeasurement est récupéré en interrogeant `satelliteLib` pour tous les moteurs SiteCatalyst disponibles. Si plusieurs balises sont configurées, modifiez l’index du sélecteur de tableau de manière appropriée. Les entrées du tableau sont classées selon les outils SiteCatalyst disponibles dans l’interface de DTM.

1. Enregistrez et fermez la fenêtre Éditeur de code, puis enregistrez les modifications dans la configuration Outil.
1. Dans l’onglet **[!UICONTROL Approbations]**, validez les deux approbations en attente. La balise DTM est prête à être insérée sur votre page web.
