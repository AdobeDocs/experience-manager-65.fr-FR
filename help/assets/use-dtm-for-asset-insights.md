---
title: Activation des statistiques sur les ressources via DTM
description: Découvrez comment utiliser Adobe Dynamic Tag Management (DTM) pour activer Assets Insights.
contentOwner: AG
role: User, Admin
feature: Asset Insights,Asset Reports
exl-id: 80e8f84e-3235-4212-9dcd-6acdb9067893
source-git-commit: afc72fb6b324cf2e0ad8168f783d9c1a6f96c614
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 31%

---

# Activation des statistiques sur les ressources via DTM {#enable-asset-insights-through-dtm}

La gestion dynamique des balises Adobe est un outil permettant d’activer vos outils de marketing numérique. Il est fourni gratuitement aux clients d’Adobe Analytics. Vous pouvez personnaliser votre code de suivi pour permettre aux solutions CMS tierces d’utiliser Assets Insights ou utiliser la gestion dynamique des balises pour insérer des balises Assets Insights. Les statistiques sont uniquement prises en charge et fournies pour les images.

>[!CAUTION]
>
>Adobe DTM est obsolète au profit de [!DNL Adobe Experience Platform] et atteindra bientôt [fin de vie](https://medium.com/launch-by-adobe/dtm-plans-for-a-sunset-3c6aab003a6f). Adobe vous recommande de [use [!DNL Adobe Experience Platform] pour les informations sur les ressources](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/advanced/asset-insights-launch-tutorial.html).

Effectuez les étapes suivantes pour activer Assets Insights via DTM.

1. Cliquez sur le logo du Experience Manager, puis accédez à **[!UICONTROL Outils]** > **[!UICONTROL Ressources]** > **[!UICONTROL Configuration des statistiques]**.
1. [Configuration du déploiement Experience Manager avec le Cloud Service DTM](/help/sites-administering/dtm.md)

   Le jeton API doit être disponible une fois que vous vous connectez à [https://dtm.adobe.com](https://dtm.adobe.com/) et visite **[!UICONTROL Paramètres du compte]** dans le profil utilisateur. Cette étape n’est pas requise du point de vue d’Assets Insights, car l’intégration de Experience Manager Sites à Assets Insights est toujours en cours d’exécution.

1. Connectez-vous à [https://dtm.adobe.com](https://dtm.adobe.com/), puis sélectionnez une société, le cas échéant.
1. Création ou ouverture d’une propriété web existante

   * Sélectionnez la **[!UICONTROL Propriétés web]** puis cliquez sur **[!UICONTROL Ajouter une propriété]**.

   * Mettez les champs à jour selon les besoins, puis cliquez sur **[!UICONTROL Créer une propriété]**. Voir [documentation](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=fr).

   ![Créer une propriété web de modification](assets/Create-edit-web-property.png)

1. Dans le **[!UICONTROL Règles]** onglet, sélectionnez **[!UICONTROL Règles de chargement de page]** dans le volet de navigation, puis cliquez sur **[!UICONTROL Créer une règle]**.

   ![chlimage_1-58](assets/chlimage_1-194.png)

1. Développer **[!UICONTROL Balises JavaScript / tierces]**. Cliquez ensuite sur **[!UICONTROL Ajouter un nouveau script]** dans le **[!UICONTROL HTML séquentiel]** pour ouvrir la boîte de dialogue Script.

   ![chlimage_1-59](assets/chlimage_1-195.png)

1. Cliquez sur le logo du Experience Manager, puis accédez à **[!UICONTROL Outils]** > **[!UICONTROL Ressources]**.
1. Cliquez sur **[!UICONTROL Suivi de page Insights]**, copiez le code de suivi, puis collez-le dans la boîte de dialogue Script que vous avez ouverte à l’étape 6. Enregistrez les modifications.

   >[!NOTE]
   >
   >* `AppMeasurement.js` est supprimé. Il devrait être disponible via l’outil de gestion dynamique des balises Adobe Analytics.
   >* L’appel à `assetAnalytics.dispatcher.init()` est supprimé. Le système s’attend à ce que la fonction soit appelée une fois le chargement de l’outil de gestion dynamique des balises Adobe Analytics terminé.
   >* Selon l’emplacement d’hébergement du dispositif de suivi de la page de statistiques sur les ressources (par exemple, Experience Manager, CDN, etc.), l’origine de la source du script peut nécessiter des modifications.
   >* Pour le dispositif de suivi de page hébergé par le Experience Manager, la source doit pointer vers une instance de publication à l’aide du nom d’hôte de l’instance de Dispatcher.


1. Accédez à l’adresse `https://dtm.adobe.com`. Cliquez sur **[!UICONTROL Aperçu]** dans la propriété web et cliquez sur **[!UICONTROL Ajouter un outil]** ou ouvrez un outil Adobe Analytics existant. Lors de la création de l’outil, vous pouvez définir **[!UICONTROL Méthode de configuration]** to **[!UICONTROL Automatique]**.

   ![Ajout de l’outil Adobe Analytics](assets/Add-Adobe-Analytics-Tool.png)

   Sélectionnez des suites de rapports de production/intermédiaires, selon les besoins.

1. Développer **[!UICONTROL Gestion des bibliothèques]**, et assurez-vous que **[!UICONTROL Charger la bibliothèque à l’emplacement]** est défini sur **[!UICONTROL Haut de page]**.

   ![chlimage_1-61](assets/chlimage_1-197.png)

1. Développer **[!UICONTROL Personnalisation du code de page]**, puis cliquez sur **[!UICONTROL Ouvrir l’éditeur]**.

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

   * La règle de chargement de page dans la gestion dynamique des balises comprend uniquement la variable `pagetracker.js` code. Tous les champs `assetAnalytics` sont considérés comme des remplacements des valeurs par défaut. Ils ne sont pas requis par défaut.
   * Les appels de code `assetAnalytics.dispatcher.init()` après avoir vérifié que `_satellite.getToolsByType('sc')[0].getS()` est initialisé et `assetAnalytics,dispatcher.init` est disponible. Par conséquent, vous pouvez ignorer son ajout à l’étape 11.
   * Comme indiqué dans les commentaires dans le code de suivi de la page de statistiques (**[!UICONTROL Outils > Ressources > Dispositif de suivi de la page de statistiques]**), lorsque le dispositif de suivi de page ne crée pas une `AppMeasurement` , les trois premiers arguments (RSID, Serveur de suivi et Espace de noms du visiteur) ne sont pas pertinents. Des chaînes vides sont transmises à la place pour mettre ceci en évidence.\
      Les arguments restants correspondent à ce qui est configuré sur la page Configuration des statistiques (**[!UICONTROL Outils > Ressources > Configuration des statistiques]**).
   * L’objet AppMeasurement est récupéré en interrogeant `satelliteLib` pour tous les moteurs SiteCatalyst disponibles. Si plusieurs balises sont configurées, modifiez l’index du sélecteur de tableau de manière appropriée. Les entrées du tableau sont triées en fonction des outils SiteCatalyst disponibles dans l’interface de gestion dynamique des balises.

1. Enregistrez et fermez la fenêtre Éditeur de code, puis enregistrez les modifications dans la configuration de l’outil.
1. Dans le **[!UICONTROL Approbations]** , validez les deux validations en attente. La balise DTM est prête à être insérée sur votre page web.
