---
title: FAQ sur AEM
description: Utilisez ces FAQ pour comprendre, configurer et résoudre les problèmes ou workflows courants dans AEM.
exl-id: 182c464a-ff7a-467b-9eb5-8ffac335a87a
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '1011'
ht-degree: 40%

---

# FAQ sur AEM {#aem-faqs}

Découvrez les réponses à certains problèmes AEM de dépannage et de configuration.

## Sites {#sites}

### Comment configurer une distribution sans fichier binaire ? {#how-do-i-configure-binary-less-distribution}

La distribution sans fichier binaire est prise en charge pour les déploiements sur un entrepôt de données partagé et implique les agents qui utilisent l’exportateur de package de distribution basé sur le coffre-fort (PID d’usine) : `org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`) du créateur de modules.

Lorsque le mode sans fichier binaire est activé, les modules de contenu distribués contiennent des références à des fichiers binaires plutôt que des fichiers binaires réels.

#### Comment activer la distribution sans fichier binaire ? {#how-do-i-enable-binary-less-distribution}

Pour activer la distribution sans fichier binaire, déployez un entrepôt de grands objets binaires partagé.
Vérifiez la propriété `useBinaryReferences` dans la configuration OSGI avec le PID d’usine (`org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`*)* utilisé par votre agent.

#### Comment personnaliser les messages d’erreur lors de la navigation dans la hiérarchie des pages dans AEM console Sites ? {#how-can-i-customize-the-error-messages-while-navigating-page-hierarchy-in-aem-sites-console}

Vérifiez le panneau Réseau (du navigateur Chrome) dans lequel une configuration personnelle (JS n’a pas été réduite).

Pour déterminer l’initiateur d’une demande, consultez la colonne `Initiator`. Il fournit les fichiers et les numéros de ligne à partir desquels les appels d’AJAX sont effectués. Vous pouvez ensuite suivre la fonction de gestion des erreurs et modifier le message d’erreur selon vos besoins.

#### Comment activer les autorisations lors de la création d’une copie de langue pour les auteurs de contenu dans AEM ? {#how-to-enable-permissions-while-creating-language-copy-for-content-authors-in-aem}

Pour utiliser la fonctionnalité Créer une copie de langue, les créateurs de contenu doivent disposer d’autorisations pour l’emplacement `/content/projects`.

Si les créateurs doivent également gérer des projets, la solution consiste à ajouter le créateur au groupe des `projects-administrators`.

#### Comment modifier le format lors de la création d’une copie de langue pour un projet ? {#how-to-change-the-format-while-creating-language-copy-for-a-project}

Créez une racine de langue et une copie de langue à l’intérieur de la racine, avant de créer un projet de traduction.

Par exemple,
Créez une racine de langue dans `/content/geometrixx` avec le nom `fr_LU` (et le titre « Français (Luxembourg) »). Ensuite, créez une copie de langue de la page à partir du panneau Références et accédez à l’option `Create structure only` dans `Create & Translate`. Enfin, créez un projet de traduction, puis ajoutez la copie de langue à la tâche de traduction.

Pour plus d’informations, voir les ressources supplémentaires ci-dessous :

* [Préparation du contenu à traduire](/help/sites-administering/tc-prep.md)
* [Gestion des projets de traduction](/help/sites-administering/tc-manage.md)

#### Comment auditer les fonctionnalités d’AEM telles que les tentatives de connexion et ACL ou les modifications d’autorisation ? {#how-to-audit-aem-capabilities-such-as-login-attempts-and-acl-or-permission-changes}

AEM permet de consigner les modifications administratives pour améliorer les audits et la résolution des problèmes. Par défaut, les informations sont consignées dans le fichier `error.log`. Pour faciliter la surveillance, il est recommandé de les rediriger vers un fichier journal distinct.
Pour rediriger la sortie vers un fichier journal distinct, consultez [Comment auditer les opérations de gestion des utilisateurs dans AEM](/help/sites-administering/audit-user-management-operations.md).

#### Comment activer SSL par défaut ? {#how-to-enable-ssl-by-default}

Adobe Experience Manager (AEM) 6.4 est fourni avec l’assistant SSL et offre une interface utilisateur pour configurer la prise en charge de Jetty et Granite Jetty SSL.

Pour activer SSL par défaut, voir [SSL par défaut](/help/sites-administering/ssl-by-default.md).

#### Quelle est l’architecture recommandée lors de l’utilisation AEM Content Services à partir d’une application mobile, idéalement React Native ? {#what-is-the-recommended-architecture-when-using-aem-s-content-services-from-a-mobile-app-ideally-react-native}

Les services de contenu reposent sur les modèles Sling. Les développeurs AEM doivent fournir un pojo de modèle Sling pour chaque composant qui est exporté.

Pour comprendre comment consommer des services de contenu d’AEM depuis une application React, consultez le tutoriel [Prise en main des services de contenu AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=fr).

En outre, si les développeurs souhaitent exporter une arborescence de composants, ils peuvent également mettre en oeuvre la variable `ComponentExporter` et `ContainerExporter` et utilisez la fonction `ModelFactory` pour effectuer une itération sur les composants enfants et renvoyer leur représentation de modèle. Consultez les ressources ci-dessous :

[1] [Adobe-Marketing-Cloud/aem-core-wcm-components](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/blob/master/bundles/core/src/main/java/com/adobe/cq/wcm/core/components/internal/models/v1/PageImpl.java#L245)

[2] [Apache Sling :: Sling Models](https://sling.apache.org/documentation/bundles/models.html)

#### Comment désactiver la fenêtre contextuelle d&#39;enquête AEM 6.4 ? {#how-to-disable-aem-survey-pop-up}

Vous pouvez souscrire à la collecte de statistiques d’utilisation à l’aide de l’interface utilisateur tactile ou de la console web. Pour obtenir des instructions détaillées, voir [Souscription à la collecte de statistiques d’utilisation agrégées](/help/sites-deploying/opt-in-aggregated-usage-statistics.md).

#### Existe-t-il une bonne ressource qui met en évidence les fonctionnalités clés de la mise à niveau vers AEM 6.4 ? {#is-there-a-good-resource-that-highlights-the-key-features-for-upgrading-to-aem}

Voir [Comprendre les raisons de la mise à niveau AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/upgrade-aem-article-understand.html) qui décrit la ventilation de haut niveau des fonctionnalités clés pour les clients qui envisagent d’effectuer une mise à niveau vers la dernière version de Adobe Experience Manager.

## Assets {#assets}

### Pourquoi le workflow Ressources se répète-t-il lors du chargement de fichiers MP4 (par exemple, à l’aide de la méthode glisser-déposer) ? {#why-the-assets-workflow-repeats-itself-while-uploading-mp-files-for-example-using-drag-and-drop-method}

Si l’utilisateur, le téléchargement des fichiers de film ne dispose pas des autorisations de suppression sous le noeud de ressource, la suppression des noeuds de bloc échoue et le chargement redémarre.

#### Quels sont les paramètres par défaut pour les configurations prêtes à l’emploi lors de la création d’une copie de langue ? {#what-are-the-default-settings-for-ootb-configurations-while-creating-language-copy}

Lorsque vous créez une copie de langue via l’interface utilisateur tactile (**Références** > **Mettre à jour la copie de la langue**), un nouveau dossier DAM est créé sous la nouvelle langue et les ressources y sont référencées.

Il s’agit du paramètre par défaut pour les configurations prêtes à l’emploi. Vous pouvez définir **Traduire les ressources de page** sur **Ne pas traduire** dans les configurations de traduction.
Pour AEM 6.4, **Outils** > **Services cloud** > **Services cloud de traduction**.

#### Comment désactiver un composant AEM entraînant la croissance exponentielle de SegmentStore AEM (AEM 6.3.1.1) ? {#how-to-disable-an-aem-component-causing-exponential-growth-for-the-aem-segmentstore-aem}

Vous pouvez désactiver le désactivateur de composants OSGi. Pour utiliser ce service, voir [Désactivation des composants OSGi](https://adobe-consulting-services.github.io/acs-aem-commons/features/osgi-disablers/component-disabler/index.html).

Comme solution, vous pouvez également désactiver manuellement le composant via l’IU ou une commande `curl` (exemple ci-dessous) après chaque redémarrage d’AEM.

`curl -u admin:$(pass CQ_Admin) 'https://localhost:4502/system/console/components/com.day.cq.analytics.sitecatalyst.impl.importer.ReportImporter' --data 'action=disable'`

#### Comment personnaliser les consoles d’administration ? {#how-to-customize-admin-consoles}

AEM comporte plusieurs mécanismes pour vous permettre de personnaliser les consoles et la fonctionnalité de création de pages de votre instance de création. Pour savoir comment créer une console personnalisée et personnaliser une vue par défaut pour une console, voir [Personnalisation des consoles](/help/sites-developing/customizing-consoles-touch.md).

#### Quelle est la différence entre les composants basés sur CoralUI 2 et CoralUI 3 ? {#what-is-the-difference-between-coralui-and-coralui-based-components}

Un nouvel ensemble de composants Sling de Granite UI Foundation est créé pour Coral3 et se trouve sous [/libs/granite/ui/components/coral/foundation.](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/server.html) Un jeu est adapté aux composants basés sur CoralUI 2 et un autre à ceux basés sur CoralUI 3. Le nouveau jeu ne sera pas simplement un copier-coller de l’ancien jeu, mais il sera nettoyé (par exemple, la rationalisation et la suppression de la fonctionnalité obsolète). Il est donc recommandé qu’une page utilise uniquement un ensemble basé sur CoralUI 3 ou sur CoralUI 2.

Pour en savoir plus en détail, voir [Guide de migration vers CoralUI 3](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/legacy/coral2/migration.html).

#### Comment personnaliser le composant de recherche dans AEM Assets ? {#how-to-customize-the-search-component-in-aem-assets}

Pour en savoir plus sur l’amplification/le classement des recherches et d’autres informations de mise en oeuvre, voir [Guide de mise en oeuvre de recherche simple](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/developing/search-tutorial-develop.html?lang=fr).

La mise en œuvre de recherche simple est le thème du Summit Lab AEM Search Demystified 2017.

#### Est-il possible de créer un module externe pour WordPress qui permet à un client d’accéder au sélecteur de ressources d’Adobe pour sélectionner des images ? {#is-it-possible-to-build-plugin-for-wordpress-that-allows-a-customer-to-access-adobe-asset-picker-to-select-images}

Oui, un client utilisant WordPress peut utiliser le sélecteur de ressources Adobe pour sélectionner des images de son serveur AEM Assets à ajouter aux publications sur son site WordPress.

Voir [Sélecteur de ressources](../assets/search-assets.md#assetpicker) pour plus d’informations.
