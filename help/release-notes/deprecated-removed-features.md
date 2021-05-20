---
title: Fonctionnalités obsolètes et supprimées de la version 6.5 d’Adobe Experience Manager.
description: Notes de mise à jour dédiées aux fonctionnalités obsolètes et supprimées dans Adobe Experience Manager 6.5.
exl-id: d9b6140a-c37d-4b90-a60c-01f471d65621
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1719'
ht-degree: 43%

---

# Fonctionnalités obsolètes et supprimées {#deprecated-and-removed-features}

Adobe étudie constamment les fonctionnalités du produit de façon à les réinventer au fil du temps ou à remplacer les fonctions plus anciennes par des variantes plus modernes, pour améliorer la valeur client globale, le tout en faisant toujours attention à la compatibilité ascendante.

Pour signaler la suppression ou le remplacement imminent de fonctionnalités AEM, les règles suivantes s’appliquent :

1. L’annonce de la suppression arrive en premier. Bien qu’elles soient obsolètes, les fonctionnalités sont toujours disponibles, mais ne sont pas améliorées.
1. La suppression des fonctionnalités obsolètes se produit au plus tôt dans la version majeure suivante. La date de suppression sera annoncée.

Ce processus donne aux clients au moins un cycle de version afin d’adapter leur implémentation à une nouvelle version ou produit de remplacement d’une fonctionnalité obsolète, avant que la suppression ne soit effective.

## Fonctionnalités obsolètes {#deprecated-features}

Cette section répertorie les fonctionnalités qui ont été signalées comme étant obsolètes dans AEM 6.5. En général, les fonctionnalités qui seront supprimées dans une prochaine version sont d’abord annoncées comme obsolètes, et une solution de remplacement est fourni.

Il est conseillé aux clients de réfléchir à leur utilisation de la fonctionnalité dans leur déploiement actuel et de prévoir la modification de leur mise en œuvre de façon à utiliser l’alternative proposée.

| Zone | Fonctionnalité | Remplacement |
|---|---|---|
| Intégration de Creative Cloud | Le AEM au partage de dossiers Creative Cloud a été introduit dans AEM 6.2 afin de permettre aux utilisateurs créatifs d’accéder aux ressources d’, de sorte qu’ils puissent les ouvrir dans des applications CC et charger de nouveaux fichiers ou enregistrer les modifications apportées à. Adobe Asset Link, nouvelle fonctionnalité proposée dans l’application Creative Cloud, offre une expérience utilisateur améliorée et un accès plus puissant aux ressources d’AEM directement à partir de Photoshop, InDesign et Illustrator. Adobe n’envisage pas d’apporter d’autres améliorations à l’intégration du partage de dossiers d’AEM à Creative Cloud. Bien que cette fonctionnalité soit incluse dans AEM, il est vivement conseillé aux clients d’utiliser des solutions de remplacement. | Il est conseillé aux clients de passer à de nouvelles fonctionnalités d’intégration de Creative Cloud, notamment Adobe Asset Link ou l’appli de bureau AEM. Pour plus d’informations, voir Bonnes pratiques d’intégration d’AEM et de Creative Cloud . |
| Assets | `AssetDownloadServlet` est désactivé par défaut pour les instances de publication. Pour plus de détails, voir la [Liste de contrôle de sécurité AEM](/help/sites-administering/security-checklist.md). | Configuration décrite dans la [Liste de contrôle de sécurité AEM](/help/sites-administering/security-checklist.md). |
| Ressources | Si un utilisateur ne dispose pas des autorisations suffisantes (lecture et écriture) sur `/content/dam/collections`, il ne peut pas créer de collection. | Respectez la configuration du contrôle d’accès de l’utilisateur et assurez-vous que les autorisations sont appropriées. |
| Adobe Search &amp; Promote | L’intégration à Adobe Search &amp; Promote est obsolète. Adobe ne prévoit pas d’apporter d’autres améliorations à l’intégration Search &amp; Promote. Notez que l’intégration Search &amp; Promote reste entièrement prise en charge tout en étant obsolète. |  |
| DTM Tag Manager | L’intégration avec DTM (Dynamic Tag Manager) est obsolète. | Passez à Adobe Experience Platform Launch en tant que gestionnaire de balises. |
| Adobe Target | Avec l’ajout de la possibilité pour AEM de se connecter au service Adobe Target à l’aide de l’[!DNL Adobe I/O] API Adobe Target Standard (API REST) basée dans AEM 6.5, la méthode d’API Target Classic (XML) est obsolète. | Reconfigurez l’intégration en [utilisant la nouvelle API](https://helpx.adobe.com/fr/experience-manager/kt/sites/using/aem-sites-target-standard-technical-video-understand.html). |
| Adobe Target | L’utilisation de l’intégration `mbox.js` basée sur Adobe Target dans AEM est obsolète. | Passez à `at.js` 1.x. |
| Commerce | [CIF ](https://github.com/adobe/commerce-cif-api) RESTa été mis à disposition en 2018 sous la forme d’un ensemble de microservices permettant l’intégration entre AEM et les moteurs de commerce. Après l&#39;acquisition de Magento par Adobe mi-2018, l&#39;Adobe a décidé de changer d&#39;approche pour deux raisons. Magento possède son propre ensemble d’API de commerce (REST et GraphQL) et il n’est pas recommandé de gérer deux ensembles d’API. Les tendances du marché ont indiqué que les clients se dirigeaient vers GraphQL, car il s’agit d’une méthode d’interrogation des données plus efficace. En 2019, Adobe a publié la nouvelle structure d’intégration de commerce en utilisant les API GraphQL de Magento comme source de vérité. Adobe ne prévoit pas d’investir davantage dans CIF REST. Il est vivement conseillé aux clients d’utiliser la solution de remplacement. | Pour les intégrations AEM-Magento, passez à [AEM archétype CIF](https://github.com/adobe/aem-cif-project-archetype) et [aux composants principaux CIF ](https://github.com/adobe/aem-core-cif-components). Voir Intégration d’AEM et de Magento [à l’aide de Commerce Integration Framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md). La prise en charge des intégrations tierces (autres que Magento) avec la nouvelle approche figure sur notre feuille de route. |
| Composants (AEM Sites) | Adobe ne prévoit pas d’apporter d’autres améliorations à la plupart des composants de base (Foundation) stockés dans `/libs/foundation/components`. Recherchez les propriétés `cq:deprecated` et `cq:deprecatedReason` dans le dossier du composant. Les composants de base sont inclus dans AEM version 6.5. Les clients effectuant une mise à niveau à partir de versions antérieures peuvent continuer à les utiliser en l’état. De plus, les composants de base sont entièrement pris en charge, même s’ils sont obsolètes. | Adobe recommande d’utiliser les composants principaux pour les projets futurs. Les sites existants peuvent rester tels quels ou utiliser la [suite d’outils de modernisation AEM](https://github.com/adobe/aem-modernize-tools) pour refactoriser le site et utiliser les composants principaux. |
| Composants (AEM Sites) | Les composants de l’importateur de conception `/libs/wcm/designimporter/components` ont été marqués comme obsolètes à compter de la version 6.5. Adobe ne prévoit pas d’apporter d’autres améliorations à cette mise en oeuvre de l’importateur de conception. | Adobe prévoit de fournir une autre mise en oeuvre du cas d’utilisation dans les prochaines versions. |
| Foundation | Structure de déchargement Granite. Adobe ne prévoit pas d’apporter d’autres améliorations à la structure de déchargement introduite dans CQ 5.6.1 pour externaliser le traitement des ressources. | Adobe travaille sur une structure de déchargement native pour le cloud de nouvelle génération. |
| Développeurs | `Hobbes.js`. Adobe ne prévoit pas d’apporter d’autres améliorations à la structure de test de l’interface utilisateur `hobbes.js`. | Adobe recommande aux clients d’utiliser l’automatisation Selenium. |
| Développeurs | Bibliothèque cliente de l’interface utilisateur jQuery. Adobe ne prévoit pas de gérer ni de mettre à jour la bibliothèque cliente de l’interface utilisateur qui est fournie dans le cadre de la distribution (Quickstart) | Adobe recommande aux clients qui ont toujours besoin de l’interface utilisateur jQuery pour leur code de l’ajouter à leur base de code de projet. |
| Développeurs | Bibliothèque cliente jQuery Animation (`granite.jquery.animation`). Adobe ne prévoit pas de gérer ni de mettre à jour la bibliothèque cliente jQuery Animation fournie avec la distribution (Quickstart). | Adobe recommande aux clients qui ont encore besoin de jQuery Animations pour leur code de l’ajouter à leur base de code de projet. |
| Développeurs | Bibliothèque cliente Handlebars. Adobe ne prévoit pas de gérer ni de mettre à jour la bibliothèque cliente Handlebar fournie avec la distribution (Quickstart). | Adobe recommande aux clients qui ont toujours besoin de Handlebars pour leur code de l’ajouter à leur base de code de projet. |
| Développeurs | Bibliothèque cliente Lawnchair. Adobe ne prévoit pas de gérer ni de mettre à jour la bibliothèque cliente Lawnchair fournie avec la distribution (Quickstart). | Adobe recommande aux clients qui ont encore besoin de Lawnchair pour leur code de l’ajouter à leur base de code de projet. |
| Développeurs | `Granite.Sling.js` bibliothèque cliente. Adobe ne prévoit pas d’améliorer la bibliothèque cliente Granite.Sling.js fournie avec la distribution (Quickstart). | Adobe recommande aux clients qui comptent sur la capacité de la bibliothèque de refactoriser leur code pour ne plus l’utiliser. |
| Développeurs | Utilisation de YUI pour compresser/réduire les bibliothèques clientes JavaScript. Adobe ne prévoit pas de mettre à jour la bibliothèque YUI. Jusqu’à AEM 6.4, YUI était par défaut pour réduire JavaScript avec l’option permettant de passer à Google Closure Compiler (GCC). À partir d’AEM 6.5, GCC est l’option par défaut. | Adobe recommande aux clients qui effectuent la mise à niveau vers AEM 6.5 de passer à GCC pour leur mise en oeuvre. |
| Développeurs | Éditeur de boîte de dialogue pour l’interface utilisateur classique dans CRXDE Lite. Adobe ne prévoit pas d’améliorer l’éditeur de boîte de dialogue pour l’interface utilisateur classique fourni avec la distribution (Quickstart). | Aucun remplacement n’est disponible. |
| Formulaires | L’intégration d’AEM Forms à AEM Mobile est obsolète. | Aucun remplacement n’est disponible. |  | Développeurs | Éditeur de boîte de dialogue pour l’interface utilisateur classique dans CRXDE Lite. Adobe ne prévoit pas d’améliorer l’éditeur de boîte de dialogue pour l’interface utilisateur classique fourni avec la distribution (Quickstart). | Aucun remplacement n’est disponible. |
| Développeurs | Bibliothèque cliente Lodash/trait de soulignement. Adobe ne prévoit pas de gérer ni de mettre à jour la bibliothèque cliente Lodash/underscore fournie dans le cadre de la distribution (Quickstart). | Adobe recommande aux clients qui ont encore besoin de Lodash/underscore pour leur code de l’ajouter à leur base de code de projet. |

## Fonctionnalités supprimées {#removed-features}

Cette section répertorie les fonctionnalités qui ont été supprimées d’AEM 6.5. Ces fonctionnalités ont été marquées comme obsolètes dans les versions antérieures.

| Zone | Fonctionnalité | Remplacement |
|--- |--- |--- |
| Activity Map dans Analytics | Version d’Activity Map incluse dans AEM. | En raison de modifications de sécurité dans l’API Adobe Analytics, il n’est plus possible d’utiliser la version d’Activity Map incluse dans AEM. Utilisez le [module Activity Map fourni par Adobe Analytics](https://docs.adobe.com/content/help/fr-FR/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html). |
| Intégrations | L’intégration d’ExactTarget a été supprimée de la distribution par défaut (Quickstart) et elle n’est plus disponible. | Aucun remplacement. |
| Intégrations | L’intégration de l’API Salesforce Force a été supprimée de la distribution par défaut (Quickstart) et est désormais un module supplémentaire à installer à partir de [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). | Cette fonctionnalité est toujours disponible. |
| Formulaires | La prise en charge du service de passerelle d’Adobe Central Migration n’est plus assurée, car le produit Adobe Central n’est plus pris en charge. | Aucun remplacement. |
| Formulaires | `com.adobe.fd.df.fdinternal.model.ConfigurationInstance` | Aucun remplacement. |
| Formulaires | `com.adobe.fd.ccm.channels.print.fdinternal.api.service.PrintDataTransformer` | Aucun remplacement. |
| Formulaires | La mise à niveau en un seul bond de LiveCycle ES4 SP1 vers AEM 6.5 Forms on JEE n’est pas disponible | Voir [chemins de mise à niveau disponibles](../forms/using/upgrade.md) dans la documentation de mise à niveau d’AEM Forms. |
| Formulaires | Suppression de la prise en charge de la mise en grappe basée sur UPD d’AEM Forms on JEE | Vous ne pouvez utiliser que la mise en grappe basée sur TCP dans AEM Forms on JEE. Si vous mettez à niveau un serveur de multidiffusion UDP d’une version précédente vers AEM 5.5 Forms on JEE, effectuez des configurations manuelles pour passer à la mise en grappe de gemfire basée sur TCP. Pour obtenir des instructions détaillées, voir [Mise à niveau vers AEM 6.5 forms on JEE](../forms/using/upgrade-forms-jee.md) |
| Développeurs | Firebug Lite a été supprimé de la distribution par défaut (Quickstart). | Utilisez les consoles de développement intégrées au navigateur. |
| Développeurs | Supprimez la prise en charge de `customJavaScriptPath` dans le Gestionnaire de bibliothèques clientes HTML. | Aucun remplacement. |
| [!DNL Assets] | La fonction de déchargement des ressources est supprimée dans [!DNL Adobe Experience Manager] 6.5. | Aucun remplacement n’est disponible. |
| Cache | `system/console/slingjsp` n’est plus disponible dans AEM 6.5. | Les classes et le cache Slightly sont stockés sous le lot Apache Sling Commons FileSystem ClassLoader . Vous pouvez vérifier le numéro de lot dans la console web d’AEM et supprimer le dossier de cache directement du système de fichiers (`crx-quickstart/launchpad/felix/bundle<ID>`). |

## Annonce préalable de la prochaine version {#pre-announcement-for-next-release}

Cette section permet d’annoncer au préalable les modifications à venir dans les prochaines versions. Les modifications annoncées ne sont pas encore effectives, mais auront une incidence sur les clients. Par exemple, les fonctionnalités ne sont pas encore obsolètes, mais ont un impact sur les utilisateurs après l’obsolescence. Ces mises à jour sont fournies à des fins de planification.

| Zone | Fonctionnalité | Annonce |
|--- |--- |--- |
| Foundation | Structure de l’IU | Adobe prévoit de rendre obsolète les composants de l’interface utilisateur Coral 2 en 2019. L’interface utilisateur Coral 3 a été introduite avec AEM 6.2, et AEM 6.5 est entièrement basé sur Coral 3. Adobe recommande à ses clients et partenaires qui ont créé des interfaces utilisateur personnalisées avec Coral 2 de les restructurer avec Coral 3. Adobe fournit un outil permettant de convertir les boîtes de dialogue Coral 2 en Coral 3 - [En savoir plus](/help/sites-developing/modernization-tools.md). |
