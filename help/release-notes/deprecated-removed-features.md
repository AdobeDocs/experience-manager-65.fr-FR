---
title: Fonctionnalités obsolètes et supprimées de la version 6.5 de Adobe Experience Manager.
description: Notes de mise à jour dédiées aux fonctionnalités obsolètes et supprimées dans Adobe Experience Manager 6.5.
translation-type: tm+mt
source-git-commit: 1e6feac534fe990d614997c4bd3ab999a4a8d479
workflow-type: tm+mt
source-wordcount: '1722'
ht-degree: 45%

---


# Fonctionnalités obsolètes et supprimées {#deprecated-and-removed-features}

Adobe étudie constamment les fonctionnalités du produit de façon à les réinventer au fil du temps ou à remplacer les fonctions plus anciennes par des variantes plus modernes, pour améliorer la valeur client globale, le tout en faisant toujours attention à la compatibilité ascendante.

Pour communiquer la suppression ou le remplacement imminent des capacités AEM, les règles suivantes s&#39;appliquent :

1. L’annonce de la suppression arrive en premier. Bien qu&#39;abandonnées, les capacités sont toujours disponibles, mais ne sont pas encore améliorées.
1. La suppression des fonctionnalités obsolètes se produit dans la version majeure suivante au plus tôt. La date de suppression sera annoncée.

Ce processus donne aux clients au moins un cycle de version afin d’adapter leur implémentation à une nouvelle version ou produit de remplacement d’une fonctionnalité obsolète, avant que la suppression ne soit effective.

## Fonctionnalités obsolètes {#deprecated-features}

Cette section répertorie les fonctionnalités qui ont été signalées comme étant obsolètes dans AEM 6.5. En général, les fonctionnalités qui seront supprimées dans une prochaine version sont d’abord annoncées comme obsolètes, et une solution de remplacement est fourni.

Il est conseillé aux clients de réfléchir à leur utilisation de la fonctionnalité dans leur déploiement actuel et de prévoir la modification de leur mise en œuvre de façon à utiliser l’alternative proposée.

| Zone | Fonctionnalité | Remplacement |
|---|---|---|
| Intégration Creative Cloud | aem au partage de dossiers Creative Cloud a été introduit dans AEM 6.2 afin de permettre aux utilisateurs créatifs d’accéder aux ressources d’AEM, afin qu’ils puissent les ouvrir dans des applications CC et télécharger de nouveaux fichiers ou enregistrer des modifications dans des . Adobe Asset Link, nouvelle fonctionnalité proposée dans l’application Creative Cloud, offre une expérience utilisateur améliorée et un accès plus puissant aux ressources d’AEM directement à partir de Photoshop, InDesign et Illustrator. Adobe n’envisage pas d’apporter d’autres améliorations à l’intégration du partage de dossiers d’AEM à Creative Cloud. Bien que cette fonctionnalité soit incluse dans AEM, il est vivement conseillé aux clients d’utiliser des solutions de remplacement. | Il est conseillé aux clients de passer à de nouvelles fonctionnalités d’intégration des Creative Cloud, y compris Adobe Asset Link ou AEM application de bureau. Consultez les bonnes pratiques en matière d’intégration des Creative Cloud et des AEM pour en savoir plus. |
| Ressources | `AssetDownloadServlet` est désactivé par défaut pour les instances de publication. Pour plus de détails, voir la [Liste de contrôle de sécurité AEM](/help/sites-administering/security-checklist.md). | Configuration décrite dans la [Liste de contrôle de sécurité AEM](/help/sites-administering/security-checklist.md). |
| Ressources | If a user does not have sufficient (read and write) permissions on `/content/dam/collections`, the user cannot create a Collection. | Respectez la configuration du contrôle d’accès de l’utilisateur et assurez-vous que les autorisations sont appropriées. |
| Adobe Search &amp; Promote | L&#39;intégration avec Adobe Search &amp; Promote est obsolète. Adobe ne prévoit pas d’apporter d’autres améliorations à l’intégration Search &amp; Promote. Notez que l’intégration Search &amp; Promote reste entièrement prise en charge tout en étant obsolète. |  |
| DTM Tag Manager | L’intégration avec DTM (Dynamic Tag Manager) est obsolète. | Passez à Adobe Experience Platform Launch en tant que gestionnaire de balises. |
| Adobe Target | Lorsque vous ajoutez la possibilité pour AEM de se connecter au service Adobe Target à l’aide de l’API Standard d’Adobe Target basée sur Adobe I/O (API Rest) dans AEM 6.5, la méthode utilisant l’API Target Classic (XML) est obsolète. | Reconfigure the integration to [use the new API](https://helpx.adobe.com/experience-manager/kt/sites/using/aem-sites-target-standard-technical-video-understand.html). |
| Adobe Target | Using the `mbox.js` based integration with Adobe Target in AEM is deprecated. | Switch to use `at.js` 1.x. |
| Commerce | [CIF REST](https://github.com/adobe/commerce-cif-api) a été fourni en 2018 sous la forme d&#39;un ensemble de microservices permettant l&#39;intégration entre les moteurs AEM et commerciaux. Après l&#39;acquisition de Magento par l&#39;Adobe à la mi-2018, l&#39;Adobe a décidé de changer d&#39;approche pour deux raisons. Le Magento possède son propre ensemble d’API de commerce (REST et GraphQL) et il n’est pas recommandé de conserver deux jeux d’API. Les tendances du marché ont indiqué que les clients se dirigeaient vers GraphQL, parce que c&#39;est un moyen plus efficace d&#39;interroger des données. En 2019, l&#39;Adobe a publié le nouveau cadre d&#39;intégration commerciale en utilisant les API MagentoQL comme source de vérité. Adobe n&#39;a pas l&#39;intention d&#39;investir davantage dans CIF REST. Il est vivement conseillé aux clients d’utiliser la solution de remplacement. | Pour les intégrations AEM-Magento, passez à l’archétype [CIF](https://github.com/adobe/aem-cif-project-archetype) AEM et aux composants [principaux CIF](https://github.com/adobe/aem-core-cif-components)AEM. See AEM and Magento integration [using Commerce Integration Framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md). Le soutien aux intégrations tierces (autres que Magento) avec la nouvelle approche est sur notre feuille de route. |
| Composants (AEM Sites) | Adobe ne prévoit pas d’apporter d’autres améliorations à la plupart des composants de base (Foundation) stockés dans `/libs/foundation/components`. Look for the `cq:deprecated` and `cq:deprecatedReason` property in the component folder. aem version 6.5 inclut les composants Foundation, et les clients qui effectuent la mise à niveau à partir de versions antérieures peuvent continuer à les utiliser en l’état. En outre, les Composantes de base sont entièrement prises en charge, même si elles sont obsolètes. | Adobe recommande d&#39;utiliser les composants de base pour les projets futurs. Existing sites can remain as is or use the [AEM Modernize Tools Suite](https://github.com/adobe/aem-modernize-tools) to refactor the site to use Core Components. |
| Composants (AEM Sites) | Design Importer Components `/libs/wcm/designimporter/components` have been marked as deprecated starting 6.5. Adobe does not plan to make further enhancements to that implementation of the design importer. | L&#39;Adobe prévoit de proposer une autre mise en oeuvre du cas d&#39;utilisation dans les prochaines versions. |
| Foundation | Structure de déchargement Granite. L’Adobe ne prévoit pas d’apporter d’autres améliorations au cadre de déchargement introduit dans CQ 5.6.1 pour externaliser le traitement des actifs. | Adobe travaille sur une structure de déchargement native pour le cloud de nouvelle génération. |
| Développeurs | `Hobbes.js`. Adobe does not plan to make further enhancements to the `hobbes.js` user interface testing framework. | Adobe recommande aux clients d&#39;utiliser l&#39;automatisation du sélénium. |
| Développeurs | Bibliothèque cliente de l’interface utilisateur jQuery. Adobe ne prévoit pas de gérer ni de mettre à jour la bibliothèque cliente de l’interface utilisateur qui est fournie dans le cadre de la distribution (Quickstart) | Adobe recommande aux clients qui ont encore besoin de l’interface utilisateur jQuery pour leur code de l’ajouter à leur base de code de projet. |
| Développeurs | bibliothèque cliente jQuery Animation (`granite.jquery.animation`). Adobe ne prévoit pas de gérer ni de mettre à jour la bibliothèque cliente jQuery Animation fournie avec la distribution (Quickstart). | Adobe recommande aux clients qui ont encore besoin d&#39;animations jQuery pour leur code de l&#39;ajouter à leur base de code de projet. |
| Développeurs | Bibliothèque cliente Handlebars. Adobe ne prévoit pas de gérer ni de mettre à jour la bibliothèque cliente Handlebar fournie avec la distribution (Quickstart). | Adobe recommande aux clients qui ont encore besoin de barres de contrôle pour leur code de l&#39;ajouter à leur base de code de projet. |
| Développeurs | Bibliothèque cliente Lawnchair. Adobe ne prévoit pas de gérer ni de mettre à jour la bibliothèque cliente Lawnchair fournie avec la distribution (Quickstart). | Adobe recommande aux clients qui ont encore besoin de Lawnchair pour leur code de l&#39;ajouter à leur base de code de projet. |
| Développeurs | `Granite.Sling.js` bibliothèque cliente. Adobe ne prévoit pas d’améliorer la bibliothèque cliente Granite.Sling.js fournie avec la distribution (Quickstart). | Adobe recommande aux clients qui comptent sur la capacité de la bibliothèque de reformater leur code pour ne plus l’utiliser. |
| Développeurs | Utilisation de YUI pour compresser/réduire les bibliothèques clientes JavaScript. Adobe ne prévoit pas de mettre à jour la bibliothèque YUI. Jusqu’à AEM 6.4, YUI était par défaut en mesure de réduire JavaScript avec l’option permettant de passer au Compilateur de fermeture Google (GCC). À partir d’AEM 6.5, GCC est l’option par défaut. | Adobe recommande aux clients qui effectuent la mise à niveau vers AEM 6.5 pour passer à GCC pour leur mise en oeuvre |
| Développeurs | Éditeur de boîte de dialogue pour l’interface utilisateur classique dans CRXDE Lite. Adobe ne prévoit pas d’améliorer l’éditeur de boîte de dialogue pour l’interface utilisateur classique fourni avec la distribution (Quickstart). | Aucun remplacement n&#39;est disponible. |
| Formulaires | L&#39;intégration de AEM Forms avec AEM Mobile est obsolète. | Aucun remplacement n’est disponible. |  | Développeurs | Éditeur de boîte de dialogue pour l’interface utilisateur classique dans CRXDE Lite. Adobe ne prévoit pas d’améliorer l’éditeur de boîte de dialogue pour l’interface utilisateur classique fourni avec la distribution (Quickstart). | Aucun remplacement n&#39;est disponible. |
| Développeurs | Bibliothèque cliente de lodash/trait de soulignement. L&#39;Adobe ne prévoit pas de continuer à gérer et à mettre à jour la bibliothèque cliente Lodash/underscore fournie dans le cadre de la distribution (Quickstart). | Adobe recommande aux clients qui ont encore besoin de Lodash/trait de soulignement pour leur code de l&#39;ajouter à leur base de code de projet. |

## Fonctionnalités supprimées {#removed-features}

Cette section liste les fonctionnalités et les fonctionnalités qui ont été supprimées de AEM 6.5. Les versions antérieures indiquaient que ces fonctionnalités étaient obsolètes.

| Zone | Fonctionnalité | Remplacement |
|--- |--- |--- |
| Activity Map dans Analytics | Version d’Activity Map incluse dans AEM. | En raison de modifications de sécurité dans l’API Adobe Analytics, il n’est plus possible d’utiliser la version d’Activity Map incluse dans AEM. Utilisez le module externe [ActivityMap fourni par Adobe Analytics](https://docs.adobe.com/content/help/fr-FR/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html). |
| Intégrations | L’intégration ExactTarget a été supprimée de la distribution par défaut (Quickstart) et n’est plus disponible. | Aucun remplacement. |
| Intégrations | Salesforce Force API integration has been removed from the default distribution (Quickstart) and is now an extra package to install from [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). | La fonction est toujours disponible. |
| Formulaires | La prise en charge du service de passerelle d’Adobe Central Migration n’est plus assurée, car le produit Adobe Central n’est plus pris en charge. | Aucun remplacement. |
| Formulaires | `com.adobe.fd.df.fdinternal.model.ConfigurationInstance` | Aucun remplacement. |
| Formulaires | `com.adobe.fd.ccm.channels.print.fdinternal.api.service.PrintDataTransformer` | Aucun remplacement. |
| Formulaires | La mise à niveau à sauts simples de LiveCycle ES4 SP1 vers AEM 6.5 Forms on JEE n’est pas disponible | Reportez-vous aux chemins [de mise à niveau](../forms/using/upgrade.md) disponibles dans la documentation de mise à niveau AEM Forms. |
| Formulaires | Suppression de la prise en charge de la mise en grappe basée sur UPD d’AEM Forms on JEE | Vous pouvez uniquement utiliser la mise en grappe basée sur TCP dans AEM Forms on JEE. Si vous mettez à niveau un serveur de multidiffusion UDP d’une version précédente vers AEM 5.5 Forms on JEE, effectuez des configurations manuelles pour passer à la mise en grappe de gemfire basée sur TCP. Pour obtenir des instructions détaillées, voir [Mise à niveau vers AEM Forms 6.5 sur JEE.](../forms/using/upgrade-forms-jee.md) |
| Développeurs | Firebug Lite a été supprimé de la distribution par défaut (Quickstart). | Utilisez les consoles de développement intégrées au navigateur. |
| Développeurs | Remove `customJavaScriptPath` support in HTML Client Library Manager. | Aucun remplacement. |
| [!DNL Assets] | La fonction de déchargement des fichiers est supprimée dans la [!DNL Adobe Experience Manager] version 6.5. | Aucun remplacement n&#39;est disponible. |
| Cache | `system/console/slingjsp` n’est plus disponible dans AEM 6.5. | Classes et cache Légèrement est stocké sous le lot Apache Sling Commons FileSystem ClassLoader. Vous pouvez vérifier le numéro de lot dans la console Web AEM et supprimer directement le dossier de cache du système de fichiers (`crx-quickstart/launchpad/felix/bundle<ID>`). |

## Pre-announcement for next release {#pre-announcement-for-next-release}

Cette section permet de préannoncer les modifications à venir dans les prochaines versions. Les modifications annoncées ne sont pas encore efficaces, mais auront un impact sur les clients. Par exemple, les fonctionnalités ne sont pas encore obsolètes mais ont un impact sur les utilisateurs après leur désapprobation. Ces mises à jour sont fournies à des fins de planification.

| Zone | Fonctionnalité | Annonce |
|--- |--- |--- |
| Foundation | Structure de l’IU | Adobe prévoit de rendre obsolète les composants de l’interface utilisateur Coral 2 en 2019. L’interface utilisateur Coral 3 a été introduite avec AEM 6.2, et AEM 6.5 est entièrement basé sur Coral 3. Adobe recommande à ses clients et partenaires qui ont créé des interfaces utilisateur personnalisées avec Coral 2 de les restructurer avec Coral 3. Adobe fournit un outil permettant de convertir les boîtes de dialogue Coral 2 en Coral 3 - [En savoir plus](/help/sites-developing/dialog-conversion.md). |
