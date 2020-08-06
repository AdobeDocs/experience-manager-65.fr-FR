---
title: FAQ sur AEM
seo-title: Questions courantes sur AEM 6.4
description: Utilisez ces FAQ pour comprendre, configurer, et résoudre les problèmes ou les workflows courants dans AEM.
seo-description: Utilisez ces FAQ pour comprendre, configurer, et résoudre les problèmes ou les workflows courants dans AEM.
uuid: 17d34923-f1ce-463b-8e9d-a713edcce51b
contentOwner: jsyal
discoiquuid: a3bb5695-6593-413d-9c2f-4c164e663b15
docset: aem65
translation-type: tm+mt
source-git-commit: 1207cd54d9d605b7fbf606393cd33b5c19b603f4
workflow-type: tm+mt
source-wordcount: '1354'
ht-degree: 72%

---


# FAQ sur AEM {#aem-faqs}

Découvrez les réponses à certains problèmes de configuration d’AEM.

## Sites {#sites}

### How do I configure binary-less distribution? {#how-do-i-configure-binary-less-distribution}

La distribution sans fichier binaire est prise en charge pour les déploiements dans un entrepôt de données partagé et implique des agents qui exploitent le créateur de modules de l’exportateur de modules de distribution basé sur le coffre-fort (PID d’usine : `org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`).

Le mode sans fichier binaire étant activé, les modules de contenu distribués contiennent des références à des fichiers binaires plutôt que des fichiers binaires réels.

#### Comment activer la distribution sans fichier binaire ? {#how-do-i-enable-binary-less-distribution}

Pour activer la distribution sans fichier binaire, déployez un entrepôt de grands objets binaires partagé.
Check the `useBinaryReferences` property in the OSGI configuration with the factory PID ( `org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`*)*that your agent is using.

#### How can I customize the error messages while navigating page hierarchy in AEM sites console? {#how-can-i-customize-the-error-messages-while-navigating-page-hierarchy-in-aem-sites-console}

Vérifiez le panneau Réseau (du navigateur Chrome), qui contient une configuration personnelle (JavaScript n’a pas été compressé).

View the `Initiator` column to determine what the initiator of a request was. Elle indique les fichiers et les numéros de ligne correspondant aux appels AJAX effectués. Ensuite, vous pouvez suivre la fonction de gestion des erreurs et modifier le message d’erreur selon vos besoins.

#### Comment activer les autorisations tout en créant une copie de langue pour les créateurs de contenu dans AEM ? {#how-to-enable-permissions-while-creating-language-copy-for-content-authors-in-aem}

To create language copy feature, content-authors need permissions at `/content/projects` location.

If one requires the authors to manage projects as well, then the workaround is to add the author to `project-administrators` group.

#### How to change the format while creating Language Copy for a project? {#how-to-change-the-format-while-creating-language-copy-for-a-project}

Avant de créer un projet de traduction, créez une racine de langue et une copie de langue dans la racine.

For example,
Create a language root at `/content/geometrixx` with name as `fr_LU` (and title as French (Luxembourg)). Par la suite, créez une copie de langue de la page à partir du panneau des références et accédez à l’ `Create structure only` option dans `Create & Translate`. Enfin, créez un projet de traduction, puis ajoutez la copie de langue à la tâche de traduction.

Pour plus d’informations, reportez-vous aux ressources supplémentaires ci-dessous :

* [Préparation du contenu à traduire](/help/sites-administering/tc-prep.md)
* [Gestion des projets de traduction](/help/sites-administering/tc-manage.md)

#### Comment auditer les fonctionnalités d’AEM telles que les tentatives de connexion et ACL ou les modifications d’autorisation ? {#how-to-audit-aem-capabilities-such-as-login-attempts-and-acl-or-permission-changes}

AEM permet de consigner les modifications administratives pour améliorer les audits et la résolution des problèmes. By default, the information is logged in the `error.log` file. Pour faciliter la surveillance, il est recommandé de les rediriger vers un fichier journal distinct.
Pour rediriger la sortie vers un fichier journal distinct, consultez [Comment auditer les opérations de gestion des utilisateurs dans AEM](/help/sites-administering/audit-user-management-operations.md).

#### How to enable SSL by default? {#how-to-enable-ssl-by-default}

Adobe Experience Manager (AEM) 6.4 contient un assistant SSL et propose une interface utilisateur pour configurer la prise en charge de Jetty et Granite Jetty SSL.

Pour activer SSL par défaut, voir [SSL par défaut](/help/sites-administering/ssl-by-default.md).

#### Quelle est l’architecture recommandée lors de l’utilisation des services de contenu d’AEM depuis une application mobile, idéalement React Native ? {#what-is-the-recommended-architecture-when-using-aem-s-content-services-from-a-mobile-app-ideally-react-native}

Content Services est basé sur les modèles Sling et les développeurs AEM doivent fournir un profil de modèle Sling pour chaque composant exporté.

Pour comprendre comment consommer des services de contenu d’AEM depuis une application React, consultez le tutoriel [Prise en main des services de contenu AEM](https://helpx.adobe.com/fr/experience-manager/kt/sites/using/content-services-tutorial-use.html).

Also, if the developers want to export a tree of components they can also implement the `ComponentExporter` and `ContainerExporter` interfaces as well as use the `ModelFactory` to iterate over the child components and return their model representation. Consultez les ressources ci-dessous :

[1] [Adobe-Marketing-Cloud/aem-core-wcm-components](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/blob/master/bundles/core/src/main/java/com/adobe/cq/wcm/core/components/internal/models/v1/PageImpl.java#L245)

[2] [Apache Sling : Modèles Sling](https://sling.apache.org/documentation/bundles/models.html)

#### How to disable AEM 6.4 survey pop-up? {#how-to-disable-aem-survey-pop-up}

Vous pouvez souscrire à la collecte de statistiques d’utilisation à l’aide de l’IU tactile ou de la console web. Pour des instructions détaillées, consultez [Souscription à la collecte de statistiques d’utilisation agrégées](/help/sites-deploying/opt-in-aggregated-usage-statistics.md).

#### Existe-t-il une bonne ressource qui explique les fonctionnalités clés dans le cas d’une mise à niveau vers AEM 6.4 ? {#is-there-a-good-resource-that-highlights-the-key-features-for-upgrading-to-aem}

Please refer to [Understanding Reasons to Upgrade AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/upgrade-aem-article-understand.html) that describes high-level breakdown of key features for customers considering upgrading to the latest version of Adobe Experience Manager.

## Ressources {#assets}

### Why the Assets workflow repeats itself while uploading MP4 files (for example, using drag-and-drop method)? {#why-the-assets-workflow-repeats-itself-while-uploading-mp-files-for-example-using-drag-and-drop-method}

Lorsqu’un utilisateur charge les fichiers vidéo, s’il ne dispose pas des autorisations de suppression sous le nœud des actifs, la suppression des nœuds de bloc échoue et le chargement recommence.

#### Quel est le nombre maximal de ressources numériques pouvant être gérées simultanément par AEM 6.4 ? {#what-is-the-maximum-number-of-digital-assets-that-can-be-operated-with-aem-at-a-time}

Adobe Experience Manager (AEM) 6.5 permet actuellement de charger jusqu’à 2 Go de ressources à la fois.

Pour des informations supplémentaires sur le nombre maximal de ressources pouvant être gérées par AEM 6.5, voir le [guide des tailles Assets](/help/assets/assets-sizing-guide.md).

#### What are the default settings for OOTB configurations while creating Language Copy? {#what-are-the-default-settings-for-ootb-configurations-while-creating-language-copy}

Lors de la création de copies de langue par le biais de l’IU classique, les ressources ne sont pas déplacées sous la nouvelle hiérarchie de langue. Elles sont plutôt utilisées par le gabarit de langue.

En revanche, lorsque vous créez une copie de langue par le biais de l’IU optimisée pour les écrans tactiles (**Références** ->**Mettre à jour la copie de langue**), un nouveau dossier DAM est créé sous la nouvelle langue et les ressources sont référencées à partir de cet emplacement.

Il s’agit du paramètre par défaut pour les configurations prêtes à l’emploi. Vous pouvez définir **Traduire les ressources de page** sur **Ne pas traduire** dans les configurations de traduction.
Pour AEM 6.4, **Outils** > **Services cloud** > **Services cloud de traduction**.

#### How to disable an AEM component causing exponential growth for the AEM SegmentStore (AEM 6.3.1.1)? {#how-to-disable-an-aem-component-causing-exponential-growth-for-the-aem-segmentstore-aem}

Vous pouvez désactiver OSGi Component Disabler. Pour utiliser ce service, voir [OSGi Component Disabler](https://adobe-consulting-services.github.io/acs-aem-commons/features/osgi-disablers/component-disabler/index.html).

Comme solution, vous pouvez également désactiver manuellement le composant via l’IU ou une commande `curl` (exemple ci-dessous) après chaque redémarrage d’AEM.

`curl -u admin:$(pass CQ_Admin) 'https://localhost:4502/system/console/components/com.day.cq.analytics.sitecatalyst.impl.importer.ReportImporter' --data 'action=disable'`

#### How to configure Asset Insights with AEM 6.5 instance? {#how-to-configure-asset-insights-with-aem-instance}

Pour configurer la fonction Statistiques sur les ressources pour Experience Manager déployé via Adobe Activation (gestion dynamique des balises), veuillez consulter la section [Configuration de la fonction Statistiques sur les ressources avec AEM Assets](https://helpx.adobe.com/experience-manager/kt/assets/using/asset-insights-tutorial-setup.html).

#### Comment personnaliser les consoles d’administration ? {#how-to-customize-admin-consoles}

AEM fournit divers mécanismes permettant de personnaliser les consoles et les fonctionnalités de création de page de votre instance de création. Pour savoir comment créer une console personnalisée et modifier l’affichage par défaut d’une console, veuillez consulter la section [Personnalisation des consoles](/help/sites-developing/customizing-consoles-touch.md).

#### Quelle est la différence entre les composants basés sur CoralUI 2 et CoralUI 3 ? {#what-is-the-difference-between-coralui-and-coralui-based-components}

A new set of Sling components of Granite UI Foundation is created for Coral3 and is located under [/libs/granite/ui/components/coral/foundation.](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/server.html) Un jeu est adapté aux composants basés sur CoralUI 2 et un autre à ceux basés sur CoralUI 3. Le nouveau jeu ne sera pas simplement un copier-coller de l’ancien, mais il sera nettoyé (par exemple en simplifiant et en supprimant les fonctionnalités abandonnées). Il est donc recommandé qu’une page utilise un jeu basé uniquement soit sur CoralUI 3 soit sur CoralUI 2.

Pour en savoir plus, veuillez consulter le [Guide de migration vers CoralUI 3](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/legacy/coral2/migration.html).

#### How to customize the search component in AEM Assets? {#how-to-customize-the-search-component-in-aem-assets}

Pour en savoir plus sur l’accélération et le classement de la recherche ainsi que pour recevoir des informations supplémentaires sur la mise en œuvre, consultez le [Guide de mise en œuvre de recherche simple](https://helpx.adobe.com/experience-manager/kt/sites/using/search-tutorial-develop.html).

La mise en œuvre de recherche simple est le matériel du Summit Lab AEM Search Demystified 2017.

#### What is the difference between AEM Assets and AEM MediaLibrary? {#what-is-the-difference-between-aem-assets-and-aem-medialibrary}

AEM Assets est une application de la plateforme AEM qui permet à nos clients de gérer leurs ressources numériques (images, vidéos, documents et clips audio) dans un référentiel web, tandis que la bibliothèque multimédia AEM (AEM MediaLibrary) est une partie spécifique du référentiel de contenu appartenant à la gestion de contenu web d’AEM, où les images et d’autres ressources partagées sont stockées.

Pour plus d’informations, veuillez consulter la rubrique [AEM Assets vs. AEM MediaLibrary](/help/assets/medialibrary.md).

#### Est-il possible d’utiliser un plug-in pour WordPress afin de permettre à un client d’accéder à Adobe Asset Picker pour sélectionner des images ? {#is-it-possible-to-build-plugin-for-wordpress-that-allows-a-customer-to-access-adobe-asset-picker-to-select-images}

Oui, un client utilisant WordPress peut utiliser Adobe Asset Picker pour sélectionner des images de son serveur AEM Assets et les ajouter aux publications sur son site WordPress.

Pour plus d’informations, veuillez consulter la section [Sélecteur de ressources](../assets/search-assets.md#assetpicker).

#### Est-il possible d’étendre les facettes de recherche dans AEM Assets pour ajouter des prédicats supplémentaires ? {#is-it-possible-to-extend-the-search-facets-in-aem-assets-to-add-additional-predicates}

Un déploiement à l’échelle de l’entreprise d’Adobe Experience Manager (AEM) Assets permet de stocker des quantités importantes de ressources. Vous pouvez ajouter des prédicats au formulaire par défaut ou utiliser un formulaire personnalisé qui comprend les facettes de votre choix.

Pour en savoir plus, consultez la section [Facettes de recherche](/help/assets/search-facets.md).
