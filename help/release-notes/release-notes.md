---
title: Notes de mise à jour générales de [!DNL Adobe Experience Manager] 6.5
description: '[!DNL Adobe Experience Manager]Notes relatives à  6.5 décrivant les informations de version, les nouveautés, la procédure d’installation et les listes de modifications détaillées.'
exl-id: 0288aa12-8d9d-4cec-9a91-7a4194dd280a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2150'
ht-degree: 66%

---

# Notes de mise à jour générales de [!DNL Adobe Experience Manager] 6.5{#general-release-notes-for-adobe-experience-manager}

## Informations sur la version {#release-information}

| Produit | [!DNL Adobe Experience Manager] |
|---|---|
| Version | 6.5 |
| Type | Version majeure |
| Date de disponibilité générale | 8 avril 2019 |
| Mises à jour recommandées | Voir [AEM les mises à jour récentes](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=fr). |

### Trivia {#trivia}

Le cycle de publication de cette version de [!DNL Adobe Experience Manager] a commencé le 4 avril 2018, a subi 23 itérations d’assurance qualité et de correction de bogues, et s’est terminé le 28 mars 2019. Au total, 1 345 problèmes d’utilisateurs (y compris des améliorations et des nouvelles fonctionnalités) ont été corrigés dans cette version.

[!DNL Adobe Experience Manager] La version 6.5 est disponible depuis le 8 avril 2019.

![Écran de connexion AEM 6.5](/help/assets/assets/aem65-login-v4.png)

## Nouveautés {#what-s-new}

[!DNL Adobe Experience Manager] La version 6.5 est une mise à niveau de la base de code  [!DNL Adobe Experience Manager] 6.4. Cette version comporte de nouvelles fonctionnalités améliorées, des correctifs clés de bugs signalés par des clients, des améliorations prioritaires demandées par les clients et des correctifs de bugs généraux destinés à améliorer la stabilité du produit. Il inclut également les versions du Service Pack [!DNL Adobe Experience Manager] 6.4 jusqu’à SP4.

La liste ci-dessous présente un aperçu, tandis que les pages suivantes répertorient tous les détails.

### [!DNL Experience Manager Foundation] {#experience-manager-foundation}

Liste complète des modifications apportées à [AEM Foundation](/help/release-notes/wcm-platform.md).

La plate-forme de [!DNL Adobe Experience Manager] 6.5 repose sur les versions mises à jour de la structure OSGi (Apache Sling et Apache Felix) et du référentiel de contenu Java : Apache Jackrabbit Oak 1.10.2.

Le démarrage rapide (Quickstart) utilise le moteur de servlet Eclipse Jetty 9.4.15.

#### Prise en charge de Java  {#java-support}

* Nouvelle prise en charge de Java 11, ainsi que de Java 8 déjà pris en charge.
* Pour des performances optimales, remplacez les valeurs par défaut du CPG par d’autres valeurs. Pour plus d’informations, voir la section [installation et mise à jour](/help/sites-deploying/custom-standalone-install.md) .
* Les mises à jour de maintenance Java 11 et Java 8 sont distribuées par Adobe pour que les clients puissent les utiliser dans les projets liés aux AEM, lorsqu’elles ne sont pas disponibles publiquement dans Oracle.

#### Développement Java {#java-development}

* Il existe désormais [deux versions d’Uberjar](/help/sites-developing/ht-projects-maven.md#experience-manager-api-dependencies), une version recommandée avec des interfaces publiques qui ne sont pas marquées pour obsolescence, ainsi qu’une version qui inclut des interfaces marquées pour obsolescence.

#### Interface utilisateur {#user-interface}

Diverses améliorations ont été apportées à l’interface utilisateur pour la rendre plus productive et conviviale.

* Nouvelle interface utilisateur de gestion des autorisations pour les utilisateurs et les groupes.
* Les vues de colonnes ne chargent plus maintenant que les entrées visibles à l’écran et en chargent davantage lorsque l’utilisateur commence à faire défiler l’écran. Les vues de liste et de carte le faisaient déjà depuis la version 6.0 (amélioration dans la version 6.4).
* Les vues de colonne incluent désormais l’état du workflow pour les pages/ressources, le cas échéant.
* L’action [Sélectionner tout](/help/sites-authoring/basic-handling.md#select-all) permet d’exécuter rapidement une action avec toutes les pages/ressources du même dossier.
* L’action [Sélectionner tout](/help/sites-authoring/basic-handling.md#select-all) tente d’exécuter l’action sur toutes les pages/ressources, pas seulement sur ce qui a été chargé. Une boîte de dialogue d’avertissement s’affiche si l’action n’est pas mise à niveau pour gérer les actions en bloc.

>[!CAUTION]
>
>Adobe ne prévoit pas d’apporter d’autres améliorations à l’interface utilisateur classique. AEM 6.5 comprend l’interface utilisateur classique, et les clients effectuant une mise à niveau à partir de versions antérieures peuvent continuer à l’utiliser en l’état. Notez que l’interface utilisateur classique reste complètement prise en charge alors qu’elle est en passe de devenir obsolète. [En savoir plus](/help/sites-deploying/ui-recommendations.md).

#### Recherche et indexation {#indexing-and-search}

* La recherche dans Oak prend désormais en charge les facettes dynamiques. Par exemple, le rail de filtrage dans la recherche de ressources affiche la quantité estimée de résultats.
* QueryBuilder a été étendu pour fournir des résultats avec des facettes dynamiques.

#### Mise à niveau {#upgrade}

* La mise à niveau directe sur place vers AEM 6.5 est prise en charge pour les clients exécutant AEM 6.2, 6.3 et 6.4. Les clients utilisant les versions 5.x ou 6.0/6.1 qui souhaitent utiliser une mise à niveau sur place doivent tout d’abord passer à la version 6.4, puis à la version 6.5, ou à la mise à niveau via le transfert du contenu entre les instances directement vers AEM 6.5.

#### Projets et workflows {#projects-and-workflows}

* Le nouvel éditeur de modèle de workflow ajouté à la version 6.4 a été amélioré afin d’inclure davantage d’opérations telles que la copie et la publication, la prise en charge des variables dans les étapes de workflow et les divisions OR et AND améliorées.

### [!DNL Experience Manager] Sites {#experience-manager-sites}

Liste complète des modifications apportées à [AEM Sites et aux modules complémentaires](/help/release-notes/sites.md).

#### Applications monopages gérées {#managed-single-page-apps}

L’éditeur de page offre la possibilité de modifier le contenu et la composition/mise en page en contexte dans les expériences rendues côté client (également appelé [Editeur SPA](/help/sites-developing/spa-architecture.md)). Les applications monopages existantes créées avec l’infrastructure JavaScript React ou Angular peuvent être étendues avec le SDK AEM SJ afin d’être modifiables pour les professionnels.

Fourni d’abord dans le cadre d’AEM 6.4 SP2, la prise en charge de SPA dans AEM 6.5 propose les fonctionnalités suivantes :

* Utilisez l’éditeur de modèles pour modifier et configurer les parties modifiables AEM du SPA.
* Utilisez la gestion multisite pour créer des expériences SPA avec pays, franchise ou marque blanche.

#### Gestion de contenu découplé {#headless-content-management}

AEM a la capacité de servir le contenu dans divers formats et à différents niveaux de la pile. Certains existent depuis 2008 avec les [Sling GET](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) et les [Servlets POST](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html). Content Services ([exportateur de modèles Sling](https://docs.adobe.com/content/help/fr-FR/experience-manager-learn/foundation/development/develop-sling-model-exporter.html)) a été ajouté dans la version 6.3 et est la méthode utilisée par AEM SJ SDK pour hydrater les applications monopages. L’[API HTTP pour Assets](/help/assets/mac-api-assets.md) est une API CRUD, étendue pour AEM 6.5.

Nouvelles fonctionnalités de l’API HTTP :

* Ajout de la [prise en charge des fragments de contenu à l’API HTTP pour Assets](/help/assets/assets-api-content-fragments.md) pour créer, mettre à jour, lire et supprimer des fragments.
* Exposition des listes de fragments de contenu via Content Services avec le [composant principal de la liste de fragments de contenu](https://opensource.adobe.com/aem-core-wcm-components/library/content-fragment-list.html).
* [Bibliothèque de composants de principaux](https://opensource.adobe.com/aem-core-wcm-components/library.html) indiquant la sortie JSON par défaut de Content Services pour chaque composant

#### Module complémentaire Screens  {#screens-add-on}

Concevez, diffusez et optimisez efficacement les expériences sur tous les écrans digitaux, depuis les kiosques interactifs jusqu’à la signalisation digitales.

**Conception**

* Unifiez les expériences et les contenus digitaux et en magasin avec une meilleure réutilisation des contenus
* Création simplifiée et workflows d’approbation/publication rationalisés avec prise en charge de Launches
* Éditez et diffusez des expériences interactives riches en utilisant SPA Editor

**Diffuser**

* Prise en charge étendue des lecteurs multimédias avec un fonctionnement en ligne et hors ligne robuste (Smart Sync) capable de s’adapter aux réseaux de signalisation les plus vastes.

**Optimiser**

* Effectuez des personnalisations par emplacement ou configuration du contenu déclenché par les données en utilisant des espaces réservés dynamiques.
* Informations unifiées grâce à l’intégration d’Adobe Analytics dans le lecteur AEM Screens

Pour plus d’informations sur les modifications apportées à AEM Screens, voir les Notes de mise à jour du [Guide de l’utilisateur d’AEM Screens](https://docs.adobe.com/content/help/fr-FR/experience-manager-screens/user-guide/aem-screens-introduction.html).

### [!DNL Experience Manager Assets] {#experience-manager-assets}

Liste complète des modifications apportées aux [Notes de mise à jour d’AEM 6.5 Assets](/help/release-notes/assets.md).

AEM 6.5 propose les fonctionnalités et améliorations suivantes pour accroître la productivité des utilisateurs AEM, des rôles DAM et des rôles de création et de marketing associés.

#### Intégration avec Adobe Creative Cloud  {#integration-with-adobe-creative-cloud}

L’ajout d’[Adobe Asset Link](https://helpx.adobe.com/fr/enterprise/using/adobe-asset-link.html), expérience intégrée pour les créatifs utilisant les applications Adobe Creative Cloud, notamment Photoshop, Illustrator et InDesign, simplifie la collaboration entre créatifs et marketeurs dans le processus de création de contenu. L’appli de bureau AEM continue de prendre en charge les besoins des utilisateurs qui utilisent les ressources d’AEM sur le bureau, quel que soit le type de fichier et l’application de bureau.

De plus, AEM s’intègre à Adobe Stock pour vous aider à rechercher, prévisualiser, concéder sous licence et enregistrer des ressources Adobe Stock directement à partir de l’interface utilisateur web d’AEM.

![Panneau Asset Link dans Photoshop](/help/assets/assets/aem65-assetlink-photoshop.png)

#### Ressources connectées {#connected-assets}

La fonctionnalité Ressources connectées est destinée aux déploiements plus volumineux avec un certain nombre de déploiements AEM Sites qui doivent exploiter les ressources d’un déploiement DAM AEM Assets central. Il permet d’améliorer la gouvernance des ressources gérées de manière centralisée tout en permettant une grande efficacité de la fourniture des ressources aux différents déploiements Sites.

### Dynamic Media {#dynamic-media}

Dynamic Media permet la création et la diffusion de contenus multimédias enrichis améliorés dans AEM Assets afin de générer des expériences de pointe immersives et personnalisées. Avec une seule ressource principale de grande qualité, vous pouvez tirer parti de nos technologies avancées de rendu dans le cloud, de recadrage intelligent et de visionneuses hors pair pour offrir les expériences les plus attrayantes et les plus performantes du secteur.

Les nouvelles fonctionnalités sont les suivantes :

* Prise en charge des casques vidéo 360 et VR
* Miniatures vidéo personnalisées
* Prise en charge améliorée de l’accessibilité
* Protection contre les liens rapides

#### Expérience utilisateur et recherche {#user-experience-and-search}

Les principales améliorations permettent de trouver plus rapidement les ressources appropriées en fournissant des facettes de recherche dynamiques. Elles permettent aussi de gérer plus efficacement plusieurs ressources en offrant la possibilité de sélectionner toutes les ressources à partir de n’importe quel dossier ou résultat de recherche.

### [!DNL Adobe Experience Manager Forms] {#experience-manager-forms}

AEM Forms 6.5 comporte plusieurs nouvelles fonctionnalités et améliorations. En voici un aperçu :

* Rapports de transaction pour suivre le nombre de formulaires envoyés, de documents traités et de documents générés
* Amélioration de la convivialité des communications interactives
* Signatures numériques dans le cloud dans des formulaires adaptatifs
* Intégrez des formulaires adaptatifs et des communications interactives dans les applications monopages (SPA) d’AEM Sites.
* Prise en charge des variables dans les workflows AEM
* Prise en charge du modèle d’affichage des données dans les communications interactives
* Tri des formulaires adaptatifs et des tables de communication interactive
* Validation automatique des données d’entrée dans les modèles de données du formulaire

Pour plus d’informations sur les nouvelles fonctionnalités et les ressources de documentation, voir le [Résumé des nouvelles fonctionnalités et améliorations d’AEM 6.5 Forms](/help/forms/using/whats-new.md) .

### [!DNL Experience Manager Communities] {#communitiesreleasenotes}

AEM 6.5 ajoute de nouvelles fonctionnalités et améliorations aux communautés. Les points forts de cette version sont :

* Le balisage des membres enregistrés (@mention) est pris en charge lors de la création du contenu généré par l’utilisateur.
* Les messages en bloc directs à un groupe de membres sont maintenant prise en charge.
* Filtres personnalisés développés et ajoutés en masse dans l’interface utilisateur de modération. Un [exemple de projet](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter) présentant le filtrage par balises peut être utilisé comme base pour développer des filtres personnalisés analogues.
* Nouvelle vue de liste fournie avec une interface utilisateur améliorée dans la modération en bloc.
* Au lieu d’un administrateur de communauté unique, il est possible d’attribuer des administrateurs distincts pour différents sites de communauté et groupes imbriqués.
* La fonctionnalité d’activation d’AEM 6.5 Communities prend en charge le moteur [(SCORM) 2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/).
* Prise en charge de la navigation au clavier sur les composants d’activation pour une meilleure accessibilité.
* Apache Solr 7.0 pris en charge lors de la configuration de MSRP et DSRP.

Pour obtenir la liste détaillée des modifications, voir [Notes de mise à jour d’AEM 6.5 Communities](/help/release-notes/communities-release-notes.md).

### [!DNL Experience Manager Livefyre] {#experience-manager-livefyre}

Vous pouvez intégrer Livefyre à votre instance AEM 6.5. Voir [Comment intégrer Livefyre à AEM](https://docs.adobe.com/content/help/en/experience-manager-64/administering/integration/livefyre.html).

### Exploitation du développement axé sur le client {#leverage-customer-focused-development}

Adobe applique un modèle de développement axé sur les utilisateurs afin que ces derniers puissent contribuer à toutes les étapes du processus de développement, au cours des phases de spécification, de développement et de tests. Merci à tous les utilisateurs et partenaires qui contribuent à ce processus.

Adobe a mis en place les procédures et processus nécessaires à la collecte, à la hiérarchisation et au suivi de la résolution des bogues signalés par les utilisateurs et du développement des demandes d’amélioration. Le [portail d’assistance Adobe Marketing Cloud](https://helpx.adobe.com/fr/contact/enterprise-support.ec.html) est intégré au système de suivi des défauts et des améliorations de l’Adobe. Les questions des utilisateurs sont identifiées et résolues par l’assistance clientèle dans la mesure du possible. Lorsqu’elles sont transmises au service R&amp;D, toutes les informations client sont capturées et utilisées à des fins de hiérarchisation et de création de rapports. La priorité est donnée au développement à la prise en charge payante, aux problèmes de garantie et aux améliorations payantes du client.

Ce processus de hiérarchisation a généré plus de 750 modifications axées sur le client, corrigées dans AEM 6.5.

## Liste des fichiers faisant partie de la version {#list-of-files-that-are-part-of-the-release}

**Foundation**

* Démarrage rapide autonome : `cq-quickstart-6.5.0.jar`.
* Démarrage rapide du serveur d’applications : `cq-quickstart-6.5.0.war`.
* Dispatcher 4.3.2 ou version ultérieure pour les différents serveurs et plateformes web. Voir [lien de téléchargement](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/getting-started/release-notes.html)
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

**Forms**

* [Packages pour les fonctionnalités AEM Forms](https://helpx.adobe.com/fr/aem-forms/kb/aem-forms-releases.html)
* [SDK client AEM Forms OSGi](https://repo.adobe.com/nexus/content/repositories/public/com/adobe/aemfd/aemfd-client-sdk/6.0.80/)

## Langues {#languages}

L’interface utilisateur est disponible dans les langues suivantes :

* Anglais
* Allemand
* Français
* Espagnol
* Italien
* Portugais brésilien
* Japonais
* Chinois simplifié
* Chinois traditionnel (prise en charge limitée)
* Coréen

[!DNL Experience Manager] 6.5 a été certifié dans le cadre de la norme GB18030-2005 CITS pour utiliser le codage des caractères chinois.

## Installer et mettre à jour {#install-update}

Pour connaître les exigences de configuration, voir [instructions d’installation](/help/sites-deploying/custom-standalone-install.md).

Pour obtenir des instructions détaillées, voir [documentation de mise à niveau](/help/sites-deploying/upgrade.md).

## Plateformes prises en charge {#supported-platforms}

Recherchez la matrice complète des plateformes prises en charge, y compris le niveau de prise en charge sur [les exigences techniques AEM 6.5](/help/sites-deploying/technical-requirements.md).

>[!NOTE]
>
>Oracle est passé à un modèle de prise en charge à long terme (LTS) pour les produits Oracle Java SE. Java 9 et 10 sont des versions non-LTS par Oracle. Voir [Feuille de route de la prise en charge Oracle de Java SE](https://www.oracle.com/technetwork/java/eol-135779.html). Adobe prend en charge les versions LTS de Java pour exécuter uniquement les AEM en production. Java 11 est la version recommandée avec AEM 6.5.

## Fonctionnalités obsolètes et supprimées {#deprecated-and-removed-features}

Adobe évalue constamment les fonctionnalités du produit et prévoit au fil du temps de les remplacer par des versions plus puissantes ou de réimplémenter certains composants afin de mieux accommoder les futures attentes ou extensions.

Pour [!DNL Adobe Experience Manager] 6.5, [lisez la liste des fonctionnalités obsolètes et supprimées](/help/release-notes/deprecated-removed-features.md). Cette page contient également une annonce préalable des modifications qui seront apportées dans un avenir proche et un avis important pour les clients qui mettent à jour des versions antérieures.

## Problèmes connus {#known-issues}

[Liste des problèmes connus](/help/release-notes/known-issues.md)

### Assistance technique et téléchargement du produit (sites à accès limité) {#product-download-and-support-restricted-sites}

Les sites suivants sont disponibles uniquement pour les clients . Si vous êtes client et avez besoin d’un accès, contactez votre responsable de compte Adobe.

* [Téléchargement du produit à l’adresse licensing.adobe.com](https://licensing.adobe.com/).

* Mises à jour de produit, correctifs et packages pour des fonctionnalités supplémentaires sur [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).

* [Assistance clientèle via Admin Console](https://adminconsole.adobe.com/). Pour plus d’informations, voir [Nouvelle expérience du service clientèle Adobe](https://docs.adobe.com/content/help/en/customer-one/using/home.html).
