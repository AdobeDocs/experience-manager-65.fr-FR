---
title: Notes de mise à jour générales d’Adobe Experience Manager 6.5
description: Notes relatives à Adobe Experience Manager 6.5 décrivant les informations de version, les nouveautés, la procédure d’installation et les listes de modifications détaillées.
uuid: b916624e-9486-4391-8c6f-cb4045e78490
contentOwner: chuesler
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: 7d3ceccb-4f00-4e11-9c9f-6de46a455e02
docset: aem65
translation-type: tm+mt
source-git-commit: 23dfcc944a83dd683078cfe00f85c4cc734e7752
workflow-type: tm+mt
source-wordcount: '2182'
ht-degree: 81%

---


# Notes de mise à jour générales d’Adobe Experience Manager 6.5{#general-release-notes-for-adobe-experience-manager}

## Informations sur la version {#release-information}

<table>
 <tbody>
  <tr>
   <th>Produit</th>
   <td>Adobe Experience Manager <br /> </td>
  </tr>
  <tr>
   <th>Version</th>
   <td>6.5</td>
  </tr>
  <tr>
   <th>Type</th>
   <td>Version majeure</td>
  </tr>
  <tr>
   <th>Date de disponibilité générale</th>
   <td>8 avril 2019<br /> </td>
  </tr>
  <tr>
   <th>Mises à jour recommandées</th>
   <td>See <a href="https://helpx.adobe.com/fr/experience-manager/aem-releases-updates.html">AEM Releases and Updates</a></td>
  </tr>
 </tbody>
</table>

### Trivia {#trivia}

Le cycle de publication de cette version d’Adobe Experience Manager a débuté le 4 avril 2018, a passé 23 itérations d’assurance qualité et de corrections de bugs et s’est terminé le 28 mars 2019. Au total, 1 345 problèmes d’utilisateurs (y compris des améliorations et des nouvelles fonctionnalités) ont été corrigés dans cette version.

Adobe Experience Manager 6.5 est disponible depuis le 8 avril 2019.

![Écran de connexion AEM 6.5](/help/assets/assets/aem65-login-v4.png)

## Nouveautés {#what-s-new}

Adobe Experience Manager 6.5 est une mise à niveau de la base de code d’Adobe Experience Manager 6.4. Cette version comporte de nouvelles fonctionnalités améliorées, des correctifs clés de bogues signalés par des clients, des améliorations prioritaires demandées par les clients et des correctifs de bogues généraux destinés à améliorer la stabilité du produit. Elle comprend également les versions du Service Pack jusqu’au SP4 d’Adobe Experience Manager 6.4.

La liste ci-dessous fournit un aperçu, tandis que les pages suivantes liste tous les détails.

### Experience Manager Foundation {#experience-manager-foundation}

Liste complète des modifications apportées à [AEM Foundation](/help/release-notes/wcm-platform.md).

La plateforme d’Adobe Experience Manager 6.5 repose sur les versions mises à jour de l’architecture OSGi (Apache Sling et Apache Felix), ainsi que sur Java Content Repository : Apache Jackrabbit Oak 1.10.2.

Le démarrage rapide (Quickstart) utilise le moteur de servlet Eclipse Jetty 9.4.15.

#### Prise en charge de Java  {#java-support}

* Nouvelle prise en charge de Java 11, ainsi que de Java 8 déjà pris en charge
* Pour des performances optimales, remplacez les valeurs par défaut du CPG par d’autres valeurs. Pour plus d’informations, consultez la section [Installation et mise à jour](/help/sites-deploying/custom-standalone-install.md).
* Les mises à jour de maintenance Java 11 et Java 8 seront distribuées par Adobe pour que les clients puissent les utiliser dans les projets liés à AEM, lorsqu’elles ne sont pas disponibles publiquement auprès d’Oracle.

#### Développement Java {#java-development}

* There are now [two versions of the Uberjar](/help/sites-developing/ht-projects-maven.md#experience-manager-api-dependencies), a recommended version with public interfaces that are not marked for deprecation, as well as a version that includes interfaces marked for deprecation.

#### Interface utilisateur {#user-interface}

Diverses améliorations ont été apportées à l’interface utilisateur pour la rendre plus productive et conviviale.

* Nouvelle interface utilisateur de gestion des autorisations pour les utilisateurs et les groupes
* Les vues de colonnes ne chargent plus maintenant que les entrées visibles à l’écran et en chargent davantage lorsque l’utilisateur commence à faire défiler l’écran. Les vues de liste et de carte le faisaient déjà depuis la version 6.0 (amélioration dans la version 6.4)
* Les vues de colonne incluent désormais l’état du workflow pour les pages/ressources, le cas échéant.
* L’action [Sélectionner tout](/help/sites-authoring/basic-handling.md#select-all) est un moyen rapide d’exécuter une action sur toutes les pages/tous les éléments d’un même dossier.
* L’action [Sélectionner tout](/help/sites-authoring/basic-handling.md#select-all) tente d’exécuter l’action sur toutes les pages/ressources, pas seulement sur ce qui a été chargé. Une boîte de dialogue d’avertissement s’affiche si l’action n’a pas été mise à niveau pour gérer les actions en bloc.

>[!CAUTION]
>
>Adobe ne prévoit pas d’apporter d’autres améliorations à l’interface utilisateur classique. AEM 6.5 comprend l’interface utilisateur classique, et les clients effectuant une mise à niveau à partir de versions antérieures peuvent continuer à l’utiliser en l’état. Notez que l’interface utilisateur classique reste complètement prise en charge alors qu’elle est en passe de devenir obsolète. [En savoir plus](/help/sites-deploying/ui-recommendations.md).

#### Recherche et indexation {#search-indexing}

* La recherche dans Oak prend désormais en charge les facettes dynamiques. Par exemple, le rail de filtrage dans la recherche de ressources affiche l’estimation du nombre de résultats.
* QueryBuilder a été étendu pour fournir des résultats avec des facettes dynamiques.

#### Mise à niveau {#upgrade}

* La mise à niveau directe sur place vers AEM 6.5 est prise en charge pour les clients exécutant AEM 6.2, 6.3 et 6.4. Les clients utilisant les versions 5.x ou 6.0/6.1 qui souhaitent utiliser une mise à niveau sur place doivent tout d’abord passer à la version 6.4, puis à la version 6.5, ou à la mise à niveau via le transfert du contenu entre les instances directement vers AEM 6.5.

#### Projets et workflows {#projects-and-workflows}

* Le nouvel éditeur de modèle de workflow ajouté à la version 6.4 a été amélioré afin d’inclure davantage d’opérations telles que la copie et la publication, la prise en charge des variables dans les étapes de workflow et les divisions OR et AND améliorées.

### Experience Manager Sites {#experience-manager-sites}

Liste complète des modifications apportées à [AEM Sites et aux modules complémentaires](/help/release-notes/sites.md).

#### Applications monopages gérées {#managed-single-page-apps}

L’éditeur de page offre la possibilité de modifier le contenu et la composition/mise en page en contexte dans les expériences rendues côté client (également appelé [Editeur SPA](/help/sites-developing/spa-architecture.md)). Les applications monopages existantes créées avec l’infrastructure JavaScript React ou Angular peuvent être étendues avec le SDK AEM SJ afin d’être modifiables pour les professionnels.

Fourni d’abord dans le cadre d’AEM 6.4 SP2, la prise en charge de SPA dans AEM 6.5 propose les fonctionnalités suivantes :

* Utilisez l’éditeur de modèles pour modifier et configurer les parties modifiables AEM du SPA.
* Utilisez la gestion multisite pour créer des expériences d’application monopage ou d’application d’une seule page

#### Gestion de contenu en mode sans affichage {#headless-content-management}

AEM a la capacité de servir le contenu dans divers formats et à différents niveaux de la pile. Certains existent depuis 2008 avec les [Sling GET](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) et les [Servlets POST](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html). Content Services ([exportateur de modèles Sling](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/sling-model-exporter-tutorial-develop.html)) a été ajouté dans la version 6.3 et est la méthode utilisée par AEM SJ SDK pour hydrater les applications monopages. L’[API HTTP pour Assets](/help/assets/mac-api-assets.md) est une API CRUD, étendue pour AEM 6.5.

Nouvelles fonctionnalités de l’API HTTP :

* Ajout de la [prise en charge des fragments de contenu à l’API HTTP pour Assets](/help/assets/assets-api-content-fragments.md) pour créer, mettre à jour, lire et supprimer des fragments.
* Exposition des listes de fragments de contenu via Content Services avec le [composant principal de la liste de fragments de contenu](https://opensource.adobe.com/aem-core-wcm-components/library/content-fragment-list.html).
* [Bibliothèque de composants de principaux](https://opensource.adobe.com/aem-core-wcm-components/library.html) indiquant la sortie JSON par défaut de Content Services pour chaque composant

#### Module complémentaire Screens {#screens-add-on}

Concevez, diffusez et optimisez efficacement les expériences sur tous les écrans digitaux, depuis les kiosques interactifs jusqu’à la signalisation digitales.

**Concevoir**

* Unifiez les expériences et les contenus digitaux et en magasin avec une meilleure réutilisation des contenus
* Création simplifiée et workflows d’approbation/publication rationalisés avec prise en charge de Launches
* Éditez et diffusez des expériences interactives riches en utilisant SPA Editor

**Diffuser**

* Prise en charge étendue des lecteurs multimédias avec un fonctionnement en ligne et hors ligne robuste (Smart Sync) capable de s’adapter aux réseaux de signalisation les plus vastes.

**Optimiser**

* Effectuez des personnalisations par emplacement ou configuration du contenu déclenché par les données en utilisant des espaces réservés dynamiques.
* Informations unifiées grâce à l’intégration d’Adobe Analytics dans le lecteur AEM Screens

For more details on changes to AEM Screens - see the Release Notes in the [AEM Screens User Guide](https://docs.adobe.com/content/help/fr-FR/experience-manager-screens/user-guide/aem-screens-introduction.html).

### Experience Manager Assets {#experience-manager-assets}

Full list of changes in [AEM 6.5 Assets release notes](/help/release-notes/assets.md).

AEM 6.5 propose les fonctionnalités et améliorations suivantes pour accroître la productivité des utilisateurs AEM, des rôles DAM et des rôles de création et de marketing associés.

#### Intégration avec Adobe Creative Cloud {#integration-with-adobe-creative-cloud}

L’ajout d’[Adobe Asset Link](https://helpx.adobe.com/fr/enterprise/using/adobe-asset-link.html), expérience intégrée pour les créatifs utilisant les applications Adobe Creative Cloud, notamment Photoshop, Illustrator et InDesign, simplifie la collaboration entre créatifs et marketeurs dans le processus de création de contenu. L’application de bureau AEM continue à prendre en charge les besoins des utilisateurs qui travaillent avec des ressources d’AEM sur un ordinateur de bureau, en utilisant n’importe quel type de fichier et toute application de bureau.

De plus, AEM s’intègre à Adobe Stock pour vous aider à rechercher, prévisualiser, concéder sous licence et enregistrer des ressources Adobe Stock directement à partir de l’interface utilisateur web d’AEM.

![Panneau Asset Link dans Photoshop](/help/assets/assets/aem65-assetlink-photoshop.png)

#### Ressources connectées {#connected-assets}

La fonctionnalité Ressources connectées est destinée aux déploiements plus importants avec un certain nombre de déploiements AEM Sites qui doivent exploiter les ressources d’un déploiement de gestion des actifs numériques AEM Assets central. Il permet d&#39;améliorer la gouvernance des actifs gérés de façon centralisée tout en permettant une grande efficacité de la fourniture des actifs aux divers déploiements de sites.

### Dynamic Media {#dynamic-media}

Dynamic Media permet la création et la diffusion de contenus multimédias enrichis améliorés dans AEM Assets afin de générer des expériences de pointe immersives et personnalisées. Avec une seule ressource principale de grande qualité, vous pouvez tirer parti de nos technologies avancées de rendu dans le cloud, de recadrage intelligent et de visionneuses hors pair pour offrir les expériences les plus attrayantes et les plus performantes du secteur.

Les nouvelles fonctionnalités sont les suivantes :

* Prise en charge des casques vidéo à 360° et VR
* Miniatures vidéo personnalisées
* Prise en charge améliorée de l’accessibilité
* Protection par liaison rapide

#### Expérience utilisateur et recherche {#user-experience-and-search}

Les principales améliorations permettent de trouver plus rapidement les ressources appropriées en fournissant des facettes de recherche dynamiques. Elles permettent aussi de gérer plus efficacement plusieurs ressources en offrant la possibilité de sélectionner toutes les ressources à partir de n’importe quel dossier ou résultat de recherche.

### Formulaires Adobe Experience Manager {#experience-manager-forms}

AEM Forms 6.5 comporte plusieurs nouvelles fonctionnalités et améliorations. En voici un aperçu :

* Rapports de transaction pour suivre le nombre de formulaires envoyés, de documents traités et de documents générés
* Amélioration de la convivialité des communications interactives
* Signatures numériques dans le cloud dans des formulaires adaptatifs
* Intégrez des formulaires adaptatifs et des communications interactives dans les applications monopages (SPA) d’AEM Sites.
* Prise en charge des variables dans les workflows AEM
* Prise en charge du modèle d’affichage des données dans les communications interactives
* Tri des formulaires adaptatifs et des tables de communication interactive
* Validation automatique des données d’entrée dans les modèles de données du formulaire

See the [Summary of new features and enhancements in AEM 6.5 Forms](/help/forms/using/whats-new.md) for information about new and improved features and documentation resources.

### Experience Manager Communities {#communitiesreleasenotes}

AEM 6.5 ajoute de nouvelles fonctionnalités et améliorations aux communautés. Les points forts de cette version sont :

* Le balisage des membres enregistrés (@mention) est pris en charge lors de la création du contenu généré par l’utilisateur.
* Les messages en bloc directs à un groupe de membres sont maintenant prise en charge.
* Filtres personnalisés développés et ajoutés en masse dans l’interface utilisateur de modération. A [sample project](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter) demonstrating filtering by tags can be used as a base to develop analogous custom filters.
* Nouvelle vue de liste fournie avec une interface utilisateur améliorée dans la modération en bloc.
* Au lieu d’un administrateur de communauté unique, il est possible d’attribuer des administrateurs distincts pour différents sites de communauté et groupes imbriqués.
* Enablement functionality of AEM 6.5 Communities supports [(SCORM) 2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/) engine.
* Prise en charge de la navigation au clavier sur les composants d’activation pour une meilleure accessibilité.
* Apache Solr 7.0 pris en charge lors de la configuration de MSRP et DSRP.

For detailed list of changes, see [AEM 6.5 Communities release notes](/help/release-notes/communities-release-notes.md).

### Experience Manager Livefyre {#experience-manager-livefyre}

Vous pouvez intégrer Livefyre à votre instance AEM 6.5. Vous trouverez des informations sur la façon d’intégrer Livefyre à AEM en suivant ce lien :

* [Intégration de Livefyre](https://helpx.adobe.com/experience-manager/6-4/help/sites-administering/livefyre.html)

### Tirer parti du développement axé sur le client {#leverage-customer-focused-development}

Adobe applique un modèle de développement axé sur les utilisateurs afin que ces derniers puissent contribuer à toutes les étapes du processus de développement, au cours des phases de spécification, de développement et de tests. Merci à tous les utilisateurs et partenaires qui contribuent à ce processus.

Adobe a mis en place les procédures et processus nécessaires à la collecte, à la hiérarchisation et au suivi de la résolution des bogues signalés par les utilisateurs et du développement des demandes d’amélioration. The [Adobe Marketing Cloud Support Portal](https://helpx.adobe.com/fr/marketing-cloud/contact-support.html) is integrated with the Adobe Enhancement &amp; Defect Tracking System. Les questions des utilisateurs sont identifiées et résolues par l’assistance clientèle dans la mesure du possible. Lorsqu’elles sont transmises au service R&amp;D, toutes les informations client sont capturées et utilisées à des fins de hiérarchisation et de création de rapports. Les problèmes entrant dans le cadre de l’assistance payante et de la garantie, ainsi que les demandes d’amélioration des utilisateurs détenant un compte payant sont prioritaires.

Ce processus de hiérarchisation a généré plus de 750 modifications axées sur le client, corrigées dans AEM 6.5.

## Liste des fichiers faisant partie de la version {#list-of-files-that-are-part-of-the-release}

**Foundation**

* Démarrage rapide autonome : cq-quickstart-6.5.0.jar
* Démarrage rapide du serveur d’applications : cq-quickstart-6.5.0.war
* Dispatcher 4.3.2 ou version ultérieure pour les différents serveurs et plateformes web ([lien de téléchargement](https://helpx.adobe.com/experience-manager/dispatcher/release-notes.html))
* Module externe pour Eclipse IDE ([plus d’infos et téléchargement](/help/sites-developing/aem-eclipse.md))

* Extension pour l’éditeur de code Brackets ([plus d’infos et téléchargement](/help/sites-developing/aem-brackets.md))
* Dépendances Maven/Gradle ([lien de téléchargement](https://repo.adobe.com/nexus/content/repositories/releases/com/adobe/aem/uber-jar/6.5.0))

**Sites**

* Composants de base ([projet GitHub](https://github.com/adobe/aem-core-wcm-components))
* Mise en œuvre de We.Retail Reference ([plus d’infos](/help/sites-developing/we-retail.md))
* Archétypes Maven Project :

   * pour les sites full-stack : [projet GitHub](https://github.com/adobe/aem-project-archetype) 
   * pour les applications monopages avec React / Angular : [projet GitHub](https://github.com/adobe/aem-spa-project-archetype) 

* Lecteurs AEM Screens pour différentes plateformes cibles ([téléchargement](https://download.macromedia.com/screens/))

* Modèles linguistiques pour le contenu dynamique. La version anglaise est préinstallée ; d’autres langues peuvent être téléchargées :

   * [Allemand](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-de)
   * [Espagnol](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-es)
   * [Italien](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-it)
   * [Français](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-fr)

* AEM Modernize Tools Suite, par exemple. Outil de conversion de dialogue. ([Projet GitHub](https://github.com/adobe/aem-modernize-tools) )

**Ressources**

* Package permettant d’ajouter un rasteriseur PDF amélioré ([en savoir plus](/help/assets/aem-pdf-rasterizer.md))
* Module pour ajouter la prise en charge étendue des images RAW ([plus d’infos](/help/assets/camera-raw.md))

**Formulaires**

* [Packages pour les fonctionnalités AEM Forms](https://helpx.adobe.com/fr/aem-forms/kb/aem-forms-releases.html)
* [SDK client OSGi AEM Forms](https://repo.adobe.com/nexus/content/repositories/public/com/adobe/aemfd/aemfd-client-sdk/6.0.80/)

## Langues {#languages}

L’interface utilisateur est disponible dans les langues suivantes :

* Anglais
* Allemand
* Français
* Espagnol
* Italien
* Brésilien       Portugais
* Japonais
* Chinois simplifié
* Chinois traditionnel (prise en charge limitée)
* Coréen

Experience Manager 6.5 a été certifié dans le cadre de la norme GB18030-2005 CITS pour utiliser le codage des caractères chinois.

## Installation et mise à jour {#install-update}

Reportez-vous aux [instructions d’installation](/help/sites-deploying/custom-standalone-install.md) pour connaître les exigences de configuration.

Reportez-vous à la [documentation de mise à niveau](/help/sites-deploying/upgrade.md) pour obtenir des instructions détaillées.

## Plateformes prises en charge {#supported-platforms}

Vous trouverez une matrice complète des plates-formes prises en charge, y compris le niveau de support dans [Exigences techniques d’AEM 6.5](/help/sites-deploying/technical-requirements.md)

MicroKernel Oak pour MicroKernel Oak pour

>[!NOTE]
>
>Oracle est passé à un modèle de support à long terme (LTS) pour les produits Oracle Java SE. Java 9 and 10 are non-LTS releases by Oracle (see [Oracle Java SE support roadmap](https://www.oracle.com/technetwork/java/eol-135779.html)). Adobe assure uniquement la prise en charge des versions LTS de Java pour exécuter AEM en production. La version 11 de Java est donc recommandée pour une utilisation avec AEM 6.5.

## Fonctionnalités obsolètes et supprimées {#deprecated-and-removed-features}

Adobe évalue constamment les fonctionnalités du produit et prévoit au fil du temps de les remplacer par des versions plus puissantes ou de réimplémenter certains composants afin de mieux accommoder les futures attentes ou extensions.

Dans le cas d’Adobe Experience Manager 6.5, [consultez la liste des fonctionnalités obsolètes et supprimées](/help/release-notes/deprecated-removed-features.md). Cette page contient également une annonce préalable des modifications qui seront apportées dans un avenir proche et un avis important pour les clients qui mettent à jour des versions antérieures.

## Problèmes connus {#known-issues}

[Liste des problèmes connus](/help/release-notes/known-issues.md)

### Assistance technique et téléchargement du produit (sites à accès limité) {#product-download-and-support-restricted-sites}

Seuls les clients peuvent accéder à ces sites. Si vous devez y accéder en tant que client, contactez votre gestionnaire de compte Adobe.

* [](https://daycare.day.com) [Téléchargement du produit à l’adresse licensing.adobe.com](https://licensing.adobe.com/)

* [Assistance clientèle sur daycare.day.com](https://daycare.day.com)

