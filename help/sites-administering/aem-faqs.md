---
title: FAQ sur AEM
seo-title: Questions courantes sur AEM 6.4
description: Utilisez ces FAQ pour comprendre, configurer, et résoudre les problèmes ou les workflows courants dans AEM.
seo-description: Utilisez ces FAQ pour comprendre, configurer, et résoudre les problèmes ou les workflows courants dans AEM.
uuid: 17d34923-f1ce-463b-8e9d-a713edcce51b
contentOwner: jsyal
discoiquuid: a3bb5695-6593-413d-9c2f-4c164e663b15
docset: aem65
exl-id: 182c464a-ff7a-467b-9eb5-8ffac335a87a
source-git-commit: 68c36d4e3a14567a4d115ee64a4474bcaf9aa386
workflow-type: tm+mt
source-wordcount: '1114'
ht-degree: 65%

---

# FAQ sur AEM {#aem-faqs}

Découvrez les réponses à certains problèmes de configuration d’AEM.

## Sites {#sites}

### Comment configurer une distribution sans fichier binaire ? {#how-do-i-configure-binary-less-distribution}

La distribution sans fichier binaire est prise en charge pour les déploiements dans un entrepôt de données partagé et implique des agents qui exploitent le créateur de modules de l’exportateur de modules de distribution basé sur le coffre-fort (PID d’usine : `org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`).

Le mode sans fichier binaire étant activé, les modules de contenu distribués contiennent des références à des fichiers binaires plutôt que des fichiers binaires réels.

#### Comment activer la distribution sans fichier binaire ?  {#how-do-i-enable-binary-less-distribution}

Pour activer la distribution sans fichier binaire, déployez un entrepôt de grands objets binaires partagé.
Vérifiez la propriété `useBinaryReferences` dans la configuration OSGI avec le PID d’usine ( `org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`*)* que votre agent utilise.

#### Comment personnaliser les messages d’erreur lors de la navigation dans la hiérarchie des pages dans AEM console Sites ? {#how-can-i-customize-the-error-messages-while-navigating-page-hierarchy-in-aem-sites-console}

Vérifiez le panneau Réseau (du navigateur Chrome), qui contient une configuration personnelle (JavaScript n’a pas été compressé).

Affichez la colonne `Initiator` pour déterminer l’initiateur d’une requête. Elle indique les fichiers et les numéros de ligne correspondant aux appels AJAX effectués. Ensuite, vous pouvez suivre la fonction de gestion des erreurs et modifier le message d’erreur selon vos besoins.

#### Comment activer les autorisations tout en créant une copie de langue pour les créateurs de contenu dans AEM ?  {#how-to-enable-permissions-while-creating-language-copy-for-content-authors-in-aem}

Pour créer la fonction de copie de langue, les auteurs de contenu ont besoin d’autorisations à l’emplacement `/content/projects`.

Si les auteurs doivent également gérer des projets, la solution consiste à ajouter l’auteur au groupe `project-administrators`.

#### Comment modifier le format lors de la création d’une copie de langue pour un projet ? {#how-to-change-the-format-while-creating-language-copy-for-a-project}

Avant de créer un projet de traduction, créez une racine de langue et une copie de langue dans la racine.

Par exemple :
Créez une racine de langue à l’emplacement `/content/geometrixx` avec le nom `fr_LU` (et le titre en français (Luxembourg)). Par la suite, créez une copie de langue de la page à partir du panneau Références et accédez à l’option `Create structure only` dans `Create & Translate`. Enfin, créez un projet de traduction, puis ajoutez la copie de langue à la tâche de traduction.

Pour plus d’informations, reportez-vous aux ressources supplémentaires ci-dessous :

* [Préparation du contenu à traduire](/help/sites-administering/tc-prep.md)
* [Gestion des projets de traduction](/help/sites-administering/tc-manage.md)

#### Comment contrôler les fonctionnalités d’AEM telles que les tentatives de connexion et les modifications de liste de contrôle d’accès ou d’autorisation ? {#how-to-audit-aem-capabilities-such-as-login-attempts-and-acl-or-permission-changes}

AEM permet de consigner les modifications administratives pour améliorer les audits et la résolution des problèmes. Par défaut, les informations sont consignées dans le fichier `error.log`. Pour faciliter la surveillance, il est recommandé de les rediriger vers un fichier journal distinct.
Pour rediriger la sortie vers un fichier journal distinct, consultez [Comment auditer les opérations de gestion des utilisateurs dans AEM](/help/sites-administering/audit-user-management-operations.md).

#### Comment activer SSL par défaut ? {#how-to-enable-ssl-by-default}

Adobe Experience Manager (AEM) 6.4 contient un assistant SSL et propose une interface utilisateur pour configurer la prise en charge de Jetty et Granite Jetty SSL.

Pour activer SSL par défaut, voir [SSL par défaut](/help/sites-administering/ssl-by-default.md).

#### Quelle est l’architecture recommandée lors de l’utilisation des services de contenu d’AEM depuis une application mobile, idéalement React Native ?  {#what-is-the-recommended-architecture-when-using-aem-s-content-services-from-a-mobile-app-ideally-react-native}

Les services de contenu sont basés sur les modèles Sling et les développeurs d’AEM doivent fournir un graphique de modèle Sling pour chaque composant exporté.

Pour comprendre comment consommer des services de contenu d’AEM depuis une application React, consultez le tutoriel [Prise en main des services de contenu AEM](https://helpx.adobe.com/fr/experience-manager/kt/sites/using/content-services-tutorial-use.html).

En outre, si les développeurs souhaitent exporter une arborescence de composants, ils peuvent également implémenter les interfaces `ComponentExporter` et `ContainerExporter` et utiliser la balise `ModelFactory` pour itérer sur les composants enfants et renvoyer leur représentation de modèle. Consultez les ressources ci-dessous :

[1] [Adobe-Marketing-Cloud/aem-core-wcm-components](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/blob/master/bundles/core/src/main/java/com/adobe/cq/wcm/core/components/internal/models/v1/PageImpl.java#L245)

[2] [Apache Sling : Modèles Sling](https://sling.apache.org/documentation/bundles/models.html)

#### Comment désactiver la fenêtre contextuelle d&#39;enquête AEM 6.4 ? {#how-to-disable-aem-survey-pop-up}

Vous pouvez souscrire à la collecte de statistiques d’utilisation à l’aide de l’IU tactile ou de la console web. Pour des instructions détaillées, consultez [Souscription à la collecte de statistiques d’utilisation agrégées](/help/sites-deploying/opt-in-aggregated-usage-statistics.md).

#### Existe-t-il une bonne ressource qui explique les fonctionnalités clés dans le cas d’une mise à niveau vers AEM 6.4 ?  {#is-there-a-good-resource-that-highlights-the-key-features-for-upgrading-to-aem}

Reportez-vous à la section [Comprendre les raisons de la mise à niveau AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/upgrade-aem-article-understand.html) qui décrit la ventilation de haut niveau des fonctionnalités clés pour les clients qui envisagent d’effectuer une mise à niveau vers la dernière version d’Adobe Experience Manager.

## Ressources {#assets}

### Pourquoi le workflow des ressources se répète-t-il lors du chargement de fichiers MP4 (par exemple, par glisser-déposer) ?  {#why-the-assets-workflow-repeats-itself-while-uploading-mp-files-for-example-using-drag-and-drop-method}

Lorsqu’un utilisateur charge les fichiers vidéo, s’il ne dispose pas des autorisations de suppression sous le nœud des actifs, la suppression des nœuds de bloc échoue et le chargement recommence.

#### Quels sont les paramètres par défaut des configurations prêtes à l’emploi lors de la création d’une copie de la langue ? {#what-are-the-default-settings-for-ootb-configurations-while-creating-language-copy}

Lorsque vous créez une copie de langue via l’interface utilisateur tactile (**Références** -> **Mettre à jour la copie de langue**), un nouveau dossier DAM est créé sous la nouvelle langue et les ressources sont référencées à partir de là.

Il s’agit du paramètre par défaut pour les configurations prêtes à l’emploi. Vous pouvez définir **Traduire les ressources de page** sur **Ne pas traduire** dans les configurations de traduction.
Pour AEM 6.4, **Outils** > **Services cloud** > **Services cloud de traduction**.

#### Comment désactiver un composant AEM provoquant une croissance exponentielle pour AEM SegmentStore (6.3.1.1) ? {#how-to-disable-an-aem-component-causing-exponential-growth-for-the-aem-segmentstore-aem}

Vous pouvez désactiver OSGi Component Disabler. Pour utiliser ce service, voir [OSGi Component Disabler](https://adobe-consulting-services.github.io/acs-aem-commons/features/osgi-disablers/component-disabler/index.html).

Comme solution, vous pouvez également désactiver manuellement le composant via l’IU ou une commande `curl` (exemple ci-dessous) après chaque redémarrage d’AEM.

`curl -u admin:$(pass CQ_Admin) 'https://localhost:4502/system/console/components/com.day.cq.analytics.sitecatalyst.impl.importer.ReportImporter' --data 'action=disable'`

#### Comment personnaliser les consoles d’administration ? {#how-to-customize-admin-consoles}

AEM fournit divers mécanismes pour vous permettre de personnaliser les consoles et les fonctionnalités de création de page de votre instance de création. Pour savoir comment créer une console personnalisée et modifier l’affichage par défaut d’une console, veuillez consulter la section [Personnalisation des consoles](/help/sites-developing/customizing-consoles-touch.md).

#### Quelle est la différence entre les composants basés sur CoralUI 2 et CoralUI 3 ?  {#what-is-the-difference-between-coralui-and-coralui-based-components}

Un nouvel ensemble de composants Sling de Granite UI Foundation est créé pour Coral3 et se trouve sous [/libs/granite/ui/components/coral/foundation.](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/server.html) Un jeu est adapté aux composants basés sur CoralUI 2 et un autre à ceux basés sur CoralUI 3. Le nouveau jeu ne sera pas simplement un copier-coller de l’ancien, mais il sera nettoyé (par exemple en simplifiant et en supprimant les fonctionnalités abandonnées). Il est donc recommandé qu’une page utilise un jeu basé uniquement soit sur CoralUI 3 soit sur CoralUI 2.

Pour en savoir plus, veuillez consulter le [Guide de migration vers CoralUI 3](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/legacy/coral2/migration.html).

#### Comment personnaliser le composant de recherche dans AEM Assets ? {#how-to-customize-the-search-component-in-aem-assets}

Pour en savoir plus sur l’accélération et le classement de la recherche ainsi que pour recevoir des informations supplémentaires sur la mise en œuvre, consultez le [Guide de mise en œuvre de recherche simple](https://helpx.adobe.com/experience-manager/kt/sites/using/search-tutorial-develop.html).

La mise en œuvre de recherche simple est le matériel du Summit Lab AEM Search Demystified 2017.

#### Est-il possible de créer un module externe pour WordPress qui permet à un client d’accéder au sélecteur de ressources Adobe pour sélectionner des images ? {#is-it-possible-to-build-plugin-for-wordpress-that-allows-a-customer-to-access-adobe-asset-picker-to-select-images}

Oui, un client utilisant WordPress peut utiliser Adobe Asset Picker pour sélectionner des images de son serveur AEM Assets et les ajouter aux publications sur son site WordPress.

Pour plus d’informations, veuillez consulter la section [Sélecteur de ressources](../assets/search-assets.md#assetpicker).
