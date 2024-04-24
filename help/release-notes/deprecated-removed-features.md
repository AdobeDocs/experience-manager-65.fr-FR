---
title: Fonctionnalités obsolètes et supprimées de la version 6.5 d’Adobe Experience Manager.
description: Notes de mise à jour dédiées aux fonctionnalités obsolètes et supprimées dans Adobe Experience Manager 6.5
exl-id: d9b6140a-c37d-4b90-a60c-01f471d65621
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: ht
source-wordcount: '1715'
ht-degree: 100%

---

# Fonctionnalités obsolètes et supprimées {#deprecated-and-removed-features}

<!-- Search&Promote is end-of-life September 1, 2022 | Assets | If a user does not have sufficient (read and write) permissions on `/content/dam/collections`, the user cannot create a Collection. | Honor the access control setup of user and ensure appropriate permissions. ||
|Adobe Search & Promote|The integration with Adobe Search & Promote is deprecated. Adobe does not plan to make further enhancements to the Search & Promote integration. Adobe Search & Promote integration remains fully supported while being deprecated.||| -->

Adobe étudie constamment les fonctionnalités du produit de façon à les réinventer au fil du temps ou à remplacer les fonctions plus anciennes par des variantes plus modernes, pour améliorer la valeur client globale, le tout en faisant toujours attention à la compatibilité ascendante.

Pour communiquer la suppression ou le remplacement imminent(e) de fonctionnalités d’Adobe Experience Manager (AEM), les règles suivantes s’appliquent :

1. L’annonce de la suppression arrive en premier. Bien qu’elles soient obsolètes, les fonctionnalités sont toujours disponibles, mais ne sont pas améliorées.
1. La suppression des fonctionnalités obsolètes se produit au plus tôt dans la version majeure suivante. La date précise de suppression sera annoncée plus tard.

Ce processus donne aux clients au moins un cycle de version pour adapter leur implémentation à une nouvelle version ou à un produit de remplacement pour une fonctionnalité obsolète, avant que la suppression ne soit effective.

## Fonctionnalités obsolètes {#deprecated-features}

Cette section répertorie les fonctionnalités qui ont été signalées comme étant obsolètes dans AEM 6.5. En général, les fonctionnalités qui seront supprimées dans une prochaine version sont d’abord annoncées comme obsolètes, et une solution de remplacement est fournie.

Il est conseillé aux clients de réfléchir à leur utilisation de la fonctionnalité dans leur déploiement actuel et de prévoir la modification de leur mise en œuvre de façon à utiliser l’alternative proposée.

| Domaine | Fonctionnalité | Remplacement | Version (SP) |
|---|---|---|---|
|   |   |   |   |
| Sites | Le service **Configuration des interrogations gérées par Adobe AEM** : `com.day.cq.polling.importer.impl.ManagedPollConfigImpl` | Le service **Importateur Sling de rapports Adobe AEM Analytics**. Voir Connexion à Adobe Analytics et création de frameworks - [Configurer l’intervalle d’import](/help/sites-administering/adobeanalytics-connect.md#configuring-the-import-interval) | 6.5.19.0 |
| Screens | ActiveMQ dans Adobe Experience Manager (AEM). ActiveMQ a été utilisé pour la communication entre deux instances de publication AEM. | Adobe recommande aux clientes et clients d’utiliser désormais un équilibreur de charge. | 6.5.18.0 |
| Propriétés des fragments d’expérience pour l’**État des médias sociaux**. |   | 6.5.11.0 |
| [!DNL Sites] | Modèles de fragment de contenu, pour la création de fragments de contenu simples. | [Fragments de contenu structuré basés sur des modèles](/help/assets/content-fragments/content-fragments-models.md) maintenant. | 6.5.11.0 |
| Intégration de Creative Cloud | Le partage de dossiers d’AEM vers Creative Cloud a été ajouté dans AEM 6.2. Il permet aux personnes créatives d’accéder aux ressources d’AEM pour qu’elles puissent les ouvrir dans les applications [!DNL Creative Cloud], charger de nouveaux fichiers ou enregistrer les modifications apportées à AEM. Adobe Asset Link, une nouvelle fonctionnalité proposée dans l’application Creative Cloud, offre une meilleure expérience utilisateur et un accès plus puissant aux ressources d’AEM directement à partir de Photoshop, InDesign et Illustrator. Adobe n’envisage pas d’apporter d’autres améliorations à l’intégration du partage de dossiers d’AEM à Creative Cloud. Bien que cette fonctionnalité soit incluse dans AEM, nous recommandons aux client(e)s d’utiliser des solutions de remplacement. | Il est conseillé aux clients de passer à de nouvelles fonctionnalités d’intégration de Creative Cloud, notamment Adobe Asset Link ou l’application de bureau AEM. |  |
| Assets | `AssetDownloadServlet` est désactivé par défaut pour les instances de publication. Pour plus de détails, consultez la [Liste de contrôle de sécurité AEM](/help/sites-administering/security-checklist.md). | Configuration décrite dans la [Liste de contrôle de sécurité AEM](/help/sites-administering/security-checklist.md). |  |
| Intégrations | L’écran **[!UICONTROL Accord préalable des services cloud Experience Manager]** est obsolète car l’intégration d’[!DNL Experience Manager] et d’[!DNL Adobe Target] est mise à jour dans [!DNL Experience Manager] 6.5. L’intégration prend en charge l’API Adobe Target Standard. L’API utilise l’authentification au moyen d’Adobe IMS et d’[!DNL Adobe I/O Runtime]. Elle prend en charge le rôle croissant d’Adobe Launch pour utiliser les pages [!DNL Experience Manager] à des fins d’analyse et de personnalisation, l’assistant d’accord préalable n’a donc aucune utilité sur le plan fonctionnel. | Configurez des connexions système, l’authentification Adobe IMS et les intégrations d’[!DNL Adobe I/O Runtime] à l’aide des services cloud [!DNL Experience Manager] correspondants. | 6.5.7.0 |
| Connecteurs | Adobe JCR Connector for Microsoft® SharePoint 2010 et Microsoft® SharePoint 2013 est obsolète dans [!DNL Experience Manager] 6.5. | S/O |  |
| Gestionnaire dynamique de balises (DTM) | L’intégration au DTM est obsolète. | Passez à Adobe Experience Platform Launch en tant que gestionnaire de balises. |   |
| Adobe Target | Lorsque vous ajoutez la possibilité pour AEM de se connecter au service Adobe Target à l’aide de l’API Standard d’Adobe Target basée sur [!DNL Adobe I/O] (API Rest) dans AEM 6.5, la méthode utilisant l’API Target Classic (XML) est obsolète. | [Reconfigurez l’intégration pour utiliser la nouvelle API](/help/sites-administering/target.md). |  |
| Adobe Target | L’utilisation de l’intégration basée sur `mbox.js` avec Adobe Target dans AEM est obsolète. | Passez à `at.js` 1.x.. |  |
| Commerce | Le [CIF REST](https://github.com/adobe/commerce-cif-api) a été fourni en 2018 sous la forme d’un ensemble de microservices permettant l’intégration entre AEM et les moteurs de commerce. Après l’acquisition d’Adobe Commerce (anciennement, Magento) par Adobe en mi-2018, Adobe a décidé de changer d’approche pour deux raisons. Commerce possède son propre ensemble d’API Commerce (REST et GraphQL) et il n’est pas recommandé de gérer deux ensembles d’API. Les tendances du marché ont indiqué que les clientes et clients se dirigeaient vers GraphQL, car il s’agit d’une méthode d’interrogation des données plus efficace. En 2019, Adobe a publié le nouveau framework d’intégration de Commerce en utilisant les API GraphQL de Commerce comme source de vérité. Adobe ne prévoit pas d’investir davantage dans CIF REST. Nous recommandons aux client(e)s d’utiliser la solution de remplacement. | Pour les intégrations AEM-Commerce, passez à [l’archétype CIF AEM](https://github.com/adobe/aem-cif-project-archetype) et [aux composants principaux CIF AEM](https://github.com/adobe/aem-core-cif-components). Consultez l’intégration d’AEM et d’Adobe Commerce [à l’aide d framework d’intégration de Commerce](/help/commerce/cif/integrating/magento.md). La prise en charge des intégrations tierces (autres que Commerce) avec la nouvelle approche figure sur la feuille de route d’Adobe. |  |
| Composants (AEM Sites) | Adobe ne prévoit pas d’apporter d’autres améliorations à la plupart des composants de base (Foundation) stockés dans `/libs/foundation/components`. Recherchez les propriétés `cq:deprecated` et `cq:deprecatedReason` dans le dossier des composants. AEM 6.5 inclut les composants de base, et les clients effectuant une mise à niveau à partir de versions antérieures peuvent continuer à les utiliser en l’état. De plus, les composants de base sont entièrement pris en charge, même s’ils sont obsolètes. | Adobe recommande d’utiliser les composants principaux pour les projets futurs. Les sites existants peuvent rester tels quels ou utiliser [la Suite d’outils de modernisation d’AEM](https://github.com/adobe/aem-modernize-tools) pour restructurer les sites afin d’utiliser les composants principaux. |  |
| Composants (AEM Sites) | Les composants de l’importateur de conception `/libs/wcm/designimporter/components` ont été marqués comme obsolètes depuis la version 6.5. Adobe ne prévoit pas d’apporter d’autres améliorations à cette implémentation de l’importateur de conception. | Adobe prévoit de fournir une alternative d’implémentation pour ce cas d’utilisation dans les prochaines versions. |  |
| Foundation | Framework de déchargement Granite. Adobe n’envisage pas d’apporter d’autres améliorations au framework de déchargement ajouté à la version CQ 5.6.1 pour externaliser le traitement des ressources. | Adobe travaille sur un framework de déchargement natif pour le cloud de nouvelle génération. |  |
| Développeurs | `Hobbes.js`. Adobe ne prévoit pas apporter d’autres améliorations au framework de test de l’interface utilisateur `hobbes.js`. | Adobe recommande aux clients d’utiliser l’automatisation Selenium. |  |
| Développeurs | Bibliothèque cliente de l’interface utilisateur jQuery. Adobe ne prévoit pas de continuer à gérer ni de mettre à jour la bibliothèque client de l’interface utilisateur jQuery fournie avec la distribution (Quickstart). | Adobe recommande aux clients qui ont encore besoin de l’interface utilisateur jQuery pour leur code de l’ajouter à leur base de code de projet. |  |
| Développeurs | Bibliothèque cliente jQuery Animation (`granite.jquery.animation`). Adobe ne prévoit pas de continuer à gérer ni de mettre à jour la bibliothèque client d’animations jQuery fournie avec la distribution (Quickstart). | Adobe recommande aux clients qui ont toujours besoin d’animations jQuery pour leur code de l’ajouter à leur base de code de projet. |  |
| Développeurs | Bibliothèque cliente Handlebars. Adobe ne prévoit pas de continuer à gérer ni de mettre à jour la bibliothèque client Handlebar fournie avec la distribution (Quickstart). | Adobe recommande aux clientes et clients qui ont toujours besoin de `Handlebars` pour leur code de l’ajouter à leur base de code de projet. |  |
| Développeurs | Bibliothèque cliente Lawnchair. Adobe ne prévoit pas de continuer à gérer ni de mettre à jour la bibliothèque client Lawnchair fournie avec la distribution (Quickstart). | Adobe recommande aux clients qui ont toujours besoin de Lawnchair pour leur code de l’ajouter à leur base de code de projet. |  |
| Développeurs | `Granite.Sling.js`Bibliothèque cliente. Adobe ne prévoit pas de continuer à améliorer la bibliothèque client Granite.Sling.js fournie avec la distribution (Quickstart). | Adobe recommande aux clients qui dépendent de la capacité de la bibliothèque de restructurer leur code de ne plus l’utiliser. |  |
| Développeurs | Utilisation de YUI pour compresser/réduire les bibliothèques clientes JavaScript. Adobe ne prévoit pas de mettre à jour la bibliothèque YUI. Jusqu’à la version AEM 6.4, YUI était l’option par défaut pour réduire les bibliothèques JavaScript avec l’option permettant de basculer vers Google Closure Compiler (GCC). À partir d’AEM 6.5, GCC est l’option par défaut. | Adobe recommande aux clients qui effectuent une mise à niveau vers AEM 6.5 de passer à GCC pour leur implémentation. |  |
| Développeurs | Éditeur de boîte de dialogue pour l’interface utilisateur classique dans CRXDE Lite. Adobe ne prévoit pas d’améliorer l’éditeur de boîte de dialogue pour l’interface utilisateur classique fourni avec la distribution (Quickstart) | Aucun remplacement n’est disponible. |  |
| Forms | L’intégration d’AEM Forms à AEM Mobile est obsolète. | Aucun remplacement n’est disponible. |
| Développeurs | Éditeur de boîte de dialogue pour l’interface utilisateur classique dans CRXDE Lite. Adobe ne prévoit pas d’améliorer l’éditeur de boîte de dialogue pour l’interface utilisateur classique fourni avec la distribution (Quickstart) | Aucun remplacement n’est disponible. |  |
| Développeurs | Bibliothèque cliente Lodash / Underscore. Adobe ne prévoit pas de continuer à gérer ni de mettre à jour la bibliothèque client Lodash/Underscore fournie avec la distribution (Quickstart). | Adobe recommande aux clients qui ont toujours besoin de Lodash/Underscore pour leur code de l’ajouter à leur base de code de projet. |  |

## Fonctionnalités supprimées {#removed-features}

Cette section répertorie les fonctionnalités qui ont été supprimées d’AEM 6.5. Ces fonctionnalités ont été signalées comme étant obsolètes dans les versions antérieures.

| Domaine | Fonctionnalité | Remplacement | Version (SP) |
|--- |--- |--- |--- |
| Intégration à [!DNL Experience Cloud] | Vous pouvez synchroniser vos ressources avec [!DNL Experience Cloud] en utilisant un paramétrage à l’aide d’[!DNL Adobe I/O]. [!DNL Adobe Experience Cloud] était précédemment appelé [!DNL Adobe Experience Cloud]. | Si vous avez des questions, [contactez le service clientèle d’Adobe](https://experienceleague.adobe.com/?support-solution=General&amp;lang=fr#support). |  |
| Activity Map Analytics | Version de l’Activity Map incluse dans AEM. | En raison de modifications de sécurité dans l’API Adobe Analytics, il n’est plus possible d’utiliser la version d’Activity Map incluse dans AEM. Utilisez le [Plug-in d’Activity Map fourni par Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html?lang=fr). |  |
| Intégrations | L’intégration d’ExactTarget a été supprimée de la distribution par défaut (Quickstart) et elle n’est plus disponible. | Aucun remplacement. |  |
| Intégrations | L’intégration de l’API Salesforce a été supprimée de la distribution par défaut (Quickstart) et est désormais proposée dans un package supplémentaire à installer à partir de la [distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). | La fonctionnalité est toujours disponible. |
| Forms | La prise en charge du service Adobe Central Migration Bridge a été supprimée, car le produit Adobe Central n’est plus pris en charge. | Aucun remplacement. |  |
| Forms | `com.adobe.fd.df.fdinternal.model.ConfigurationInstance` | Aucun remplacement. |  |
| Forms | `com.adobe.fd.ccm.channels.print.fdinternal.api.service.PrintDataTransformer` | Aucun remplacement |  |
| Forms | La mise à niveau en un seul bond de LiveCycle ES4 SP1 vers AEM 6.5 Forms on JEE n’est pas disponible. | Consultez les [chemins de mise à niveau disponibles](../forms/using/upgrade.md) dans la documentation de mise à niveau d’AEM Forms. |  |
| Forms | Suppression de la prise en charge de la mise en grappe basée sur UPD d’AEM Forms on JEE | Vous ne pouvez utiliser que la mise en grappe basée sur TCP dans AEM Forms on JEE. Si vous mettez à niveau un serveur de multidiffusion UDP d’une version précédente vers AEM 5.5 Forms on JEE, effectuez des configurations manuelles pour passer à la mise en grappe de GemFire basée sur TCP. Pour obtenir des instructions détaillées, consultez [Mise à niveau vers AEM Forms 6.5 sous JEE](../forms/using/upgrade-forms-jee.md). |  |
| Développeurs | Firebug Lite a été supprimé de la distribution par défaut (Quickstart) | Utiliser des consoles de développement intégrées au navigateur |
| Développeurs | Supprimez la prise en charge de `customJavaScriptPath` dans le gestionnaire de bibliothèque client HTML. | Aucun remplacement |  |
| [!DNL Assets] | La fonction de déchargement des ressources est supprimée dans [!DNL Adobe Experience Manager] 6.5. | Aucun remplacement n’est disponible. |  |
| Cache | `system/console/slingjsp` a été supprimé et n’est plus disponible dans AEM 6.5. | Les classes et le cache Slightly sont stockés sous le lot Apache Sling Commons FileSystem ClassLoader. Vous pouvez vérifier le numéro de lot dans la console Web d’AEM et supprimer le dossier de cache directement du système de fichiers (`crx-quickstart/launchpad/felix/bundle<ID>`). |  |
| Screens | Suppression de la prise en charge du lot activemq et de ses configurations associées. |  |  |

<!-- ## Pre-announcement for next release {#pre-announcement-for-next-release}

This section is used to pre-announce the upcoming changes in the future releases. The announced changes are not yet effective but will impact customers. For example, the features are not yet deprecated but impacts the users after deprecation. These updates are provided for planning purpose.

|Area|Feature|Announcement|
|--- |--- |--- |
|Foundation|UI Framework|Adobe is planning to deprecate the Coral UI 2 components in 2019. Coral UI 3 was introduced with AEM 6.2, and AEM 6.5 is fully based on Coral 3. Adobe recommends customers and partners that have build custom UIs with Coral 2 to refactored them to Coral 3. Adobe is providing a tool to convert Coral 2 dialogs to Coral 3 - [Read more](/help/sites-developing/modernization-tools.md).|
-->
