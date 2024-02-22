---
title: Notes de mise à jour de la version 6.5 d’ [!DNL Adobe Experience Manager]
description: Consultez les informations sur la mise à jour, y compris les nouveautés, la procédure d’installation et une liste complète des modifications pour [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 4
source-git-commit: 19fe527ce44d8ec5be50ebd32b46f13df96c52cc
workflow-type: tm+mt
source-wordcount: '2928'
ht-degree: 57%

---

# Notes de mise à jour du dernier pack de services [!DNL Adobe Experience Manager] 6.5 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!-- DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, November 30, 2023. In addition, a list of Forms fixes and enhancements is added to this section. -->

## Informations sur la version {#release-information}

| Produit | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Version | 6.5.20.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Type | Mise à jour du pack de services |
| Date | Vendredi 22 février 2024 <!-- UPDATE FOR EACH NEW RELEASE --> |
| URL de téléchargement | [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.20.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## Éléments compris dans [!DNL Experience Manager] 6.5.20.0 {#what-is-included-in-aem-6520}

[!DNL Experience Manager] 6.5.20.0 comprend de nouvelles fonctionnalités, des améliorations importantes demandées par les clientes et les clients, des correctifs de bugs ainsi que des améliorations en termes de performances, de stabilité et de sécurité, publiées depuis la version initiale 6.5 en avril 2019. [Installez ce pack de services](#install) dans [!DNL Experience Manager] 6.5.

<!-- UPDATE FOR EACH NEW RELEASE -->

## Principales fonctionnalités et améliorations

<!-- * _6.5.20.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

Voici quelques-unes des fonctionnalités et améliorations clés de cette version :

* Dynamic Media prend désormais en charge le format d’image HEIC sans perte pour Apple iOS/iPadOS. Voir [fmt](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-is-http-fmt.html?lang=en) dans l’API Dynamic Media Image Serving and Rendering.

* Multisite Manager (MSM) prend désormais en charge les structures de fragments d’expérience, y compris les dossiers et les sous-dossiers, pour un déploiement en masse efficace des fragments d’expérience sur Live Copies.

<!-- ### [!DNL Forms]

* text -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## Problèmes corrigés dans le Pack de services 20 {#fixed-issues}

### [!DNL Sites]{#sites-6520}

<!--#### Accessibility{#sites-accessibility-6520}

* text -->

#### Interface utilisateur d’administration{#sites-adminui-6520}

* La variable `Workflow Title` est marqué par `*` selon les besoins, mais il n’y a aucune validation. (SITES-16491) NORMAL

<!--#### Classic UI{#sites-classicui-6520}

* text -->

#### [!DNL Content Fragments]{#sites-contentfragments-6520}

* Les dossiers de configuration imbriqués n’étaient plus pris en charge et les dossiers de modèles de fragments de contenu n’étaient plus visibles après la mise à niveau vers AEM 6.5.18 ou vers AEM 6.5.19. (SITES-18110) MAJEUR
* Certains sous-dossiers ne peuvent pas effectuer de sélection à partir des modèles de fragment de contenu hérités. Il doit prendre en charge les dossiers sans avoir à `jcr:content` , même si les dossiers DAM créés par le biais de l’interface utilisateur en possèdent un. (SITES-17943) NORMAL

#### [!DNL Content Fragments] - API GRAPHQL {#sites-graphql-api-6520}

<!-- REMOVED AS PER EMAIL FROM SAMEER DHAWAN FEBRUARY 19, 2024 * When upgrading AEM from 6.5.19.0 to 6.5.20.0, the path `/libs/cq/graphql/sites/graphiql` was getting deleted. (SITES-19530) CRITICAL -->
* Lors de l’exécution d’une requête GraphQL vers [résultats de filtre](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#filtering) utilisation de variables facultatives, si une valeur spécifique est **not** fourni pour la variable facultative, la variable est alors ignorée dans l’évaluation du filtre. (SITES-17051) NORMAL

<!--#### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6520}

* text -->

#### [!DNL Content Fragments] - API REST{#sites-restapi-6520}

* Avec la mise à niveau de la `org.json` , il y a eu un changement dans la désérialisation des nombres décimaux. Avant d’être convertis &quot;par défaut&quot; en Doublons, puis en BigDecimals. Au lieu de cela, les valeurs de propriété de métadonnées, stockées par le biais de l’API REST, doivent être converties en Double à partir de BigDecimal. (SITES-16857) NORMAL

#### Back-end principal{#sites-core-backend-6520}

* Lorsque la publication rapide d’un fragment de contenu est utilisée, le chargement se poursuit et n’est pas publié. En d’autres termes, la publication rapide ne fonctionne pas pour les fragments de contenu après une mise à niveau du Service Pack d’AEM 6.5.7 vers AEM 6.5.17. Lorsque l’utilisateur a essayé la publication gérée, cela a fonctionné. Cependant, lorsqu’ils tentaient la publication rapide, elle n’était pas publiée. Plus précisément : `com.day.cq.wcm.core.impl.reference.ActivationReferenceSearchBuilder` le système était à la corbeille. (SITES-17311) MAJEUR
* Les fragments de contenu ne peuvent pas être sérialisés avec l’exportateur Jackson : le chargement de la page se déclenche lorsqu’un fragment de contenu est référencé dans une page (utilise le code de l’exportateur Jackson) et que toute balise est ajoutée à un fragment de contenu. (SITES-18096) NORMAL

#### Composants principaux{#sites-core-components-6520}

* Installation CIF package des composants principaux sur AEM causes `:type` valeur des composants existants à modifier. La modification signifie qu’ils ne sont plus rendus sur les pages auxquelles ils ont été ajoutés. (SITES-17601) MAJEUR

#### Intégration de campagne{#sites-campaign-integration-6520}

* AEM utilisait une liste autorisée également appelée `whitelist`-en raison d’un rapport de vulnérabilité. La liste autorisée empêchait les clients d’utiliser les fonctionnalités nécessaires. (SITES-16822) CRITIQUE

#### Fragments d’expérience{#sites-experiencefragments-6520}

* MSM pour les fragments d’expérience prend désormais en charge le déploiement en masse vers les structures de contenu des fragments d’expérience, y compris les dossiers et les sous-dossiers. (SITES-16004) MAJEUR

<!--#### Foundation Components (Legacy){#sites-foundation-components-legacy-6520}

* text

#### Launches{#sites-launches-6520}

* text -->

#### MSM - Live Copies{#sites-msm-live-copies-6520}

* Un &quot;`Is not modifiable`&quot; exception est générée lors du déploiement du composant. Plus précisément, un `org.apache.sling.servlets.post.impl.operations.ModifyOperation` exception survient lors du traitement de la réponse. (SITES-18809) MAJEUR
* Impossible de déployer les modifications sur des Live Copies spécifiques des fragments d’expérience. (SITES-17930) MAJEUR
* Lorsqu’un utilisateur ajoute une annotation à un composant sur une page de plan directeur, puis la déploie, le nombre d’annotations sur Live Copy s’affiche incorrectement. (SITES-17099) MAJEUR
* Le bouton Déployer MSM d’une page parente à l’autre de la page enfant est rompu dans l’interface utilisateur graphique tactile. Lorsque cette option est sélectionnée, l’erreur suivante s’affiche : `Uncaught TypeError: _g.shared is undefined`. (SITES-16991) MAJEUR

#### Éditeur de page{#sites-pageeditor-6520}

* L’aperçu de l’éditeur de thème Forms est interrompu. Lorsque l’option Aperçu est sélectionnée, seule une icône de chargement est visible. (SITES-17164) BLOQUEUR

### [!DNL Assets]{#assets-6520}

* Impossible de valider les champs basés sur des règles dans l’assistant de l’éditeur de métadonnées et affiche un message d’erreur &quot;Champs obligatoires manquants&quot;. (ASSETS-31396) MAJEUR
* Une fois qu’un PDF est déplacé vers un autre emplacement, la variable **[!UICONTROL Afficher la page]** disparaît. (ASSETS-30538) MAJEUR
* Impossible de sélectionner une image avec des autorisations de lecture. (ASSETS-32199) NORMAL
* Impossible de modifier la taille de la carte dans les paramètres d’affichage. (ASSETS-31667) NORMAL
* Le téléchargement échoue lors du téléchargement du type de fichier .oft. (ASSETS-30109) NORMAL
* Lorsque vous essayez d’ajouter un champ de métadonnées personnalisé en tant que colonne supplémentaire au rapport, les cases à cocher ne sont pas sélectionnées. (ASSETS-31671) MINEUR
* L’opération de déplacement de ressources ne fonctionne pas correctement dans le Service Pack 16 de Experience Manager. (ASSETS-30598) MINEUR

#### [!DNL Dynamic Media]{#assets-dm-6520}

* Lorsqu’une ressource est chargée dans AEM, la variable `Update_asset` le workflow est déclenché. Cependant, le workflow ne se termine jamais. Le workflow se termine uniquement jusqu’à l’étape de chargement du produit. L’étape suivante est le chargement par lots Scene7, mais ce processus n’est pas extrait dans AEM. (ASSETS-30443) CRITIQUE
* Vous avez besoin d’un meilleur moyen de gérer les vidéos non-Dynamic Media avec élégance dans le composant Dynamic Media. Ce problème donnait une exception qui instanciait `dynamicmedia_sly.js`. (ASSETS-31301) MAJEUR
* L’aperçu fonctionne pour toutes les ressources, les visionneuses de vidéos adaptatives et les vidéos. Cependant, il renvoie une erreur 403 pour `.m3u8` les fichiers (qui, soit dit en passant, fonctionnent toujours par des liens publics). (ASSETS-31882) MAJEUR
* La variable `scene7SmartCropProcessingStatus` correction de l’état. Recadrage intelligent des métadonnées vidéo utilisées pour afficher l’échec même en cas de réussite. (ASSETS-31255) MINEUR

### [!DNL Forms]{#forms-6520}

Les correctifs dans [!DNL Experience Manager] Forms sont fournis par le biais d’un package complémentaire distinct une semaine après la date de publication prévue du Pack de services [!DNL Experience Manager]. Dans ce cas, la publication du package complémentaire AEM 6.5.20.0 Forms est planifiée pour le vendredi 29 février 2024. Une liste des correctifs et améliorations de Forms est ajoutée à cette section après cette version.

<!-- #### [!DNL Adaptive Forms] -->

<!--LEFT BULLET LIST HERE IN CASE OF REUSE BY FORMS IN THE FUTURE 
* **Document Services**
  * text
* **Adaptive Forms** 
  * text
* **Accessibility**
  * text
* **Interactive Communications**
  * text -->

<!--### Commerce{#commerce-6520}

* text -->

#### [!DNL Forms Designer]{#forms-designer-6520}

* texte

<!-- ### Foundation{#foundation-6520}

* text -->

#### Communities {#communities-6520}

* Les diagnostics de synchronisation des utilisateurs échouent après la configuration de la synchronisation des utilisateurs. (NPR-41693) NORMAL

<!-- #### Content distribution{#foundation-content-distribution-6520}

* text -->

#### Intégrations{#integrations-6520}

* Supprimez tout le code et les dépendances d’Adobe Search &amp; Promote d’AEM 6.5. (NPR-40856) NORMAL

#### Localisation{#localization-6520}

* Le libellé Aria &quot;close&quot; n’est pas localisé dans **[!UICONTROL Ressources]** > **[!UICONTROL Fichiers]**, sélectionnez un dossier, puis, sur la barre d’outils, sélectionnez **[!UICONTROL Propriétés]** > **[!UICONTROL Autorisations]** onglet > nom du membre. (NPR-41705) MAJEUR
* Il existe une info-bulle tronquée pour la variable **[!UICONTROL Mot de passe du Key Store]** sur la page Configuration SSL pour les paramètres régionaux ENG, FRA, KOR, DEU et PTB. (NPR-41367) NORMAL

<!-- #### Oak{#oak-6520}

* text -->

#### Plateforme{#foundation-platform-6520}

* Problème lors de l’intégration de Campaign avec AEM provoquée par le servlet /api ne renvoyant pas le schéma correct dans le href json. La raison en était que AEM ne recevait pas l’en-tête X-Forward-Proto, ce qui forçait la demande à répondre avec un modèle HTTP au lieu de HTTPS. Par conséquent, la possibilité d’activer/désactiver la sélection de schéma en fonction d’une configuration OSGI doit être ajoutée. (GRANITE-48454) MAJOR

<!-- #### Replication{#foundation-replication-6520}

* text -->

#### Sling{#foundation-sling-6520}

* La variable `org.apache.sling.resourceMerger` Le lot 1.4.2 renvoie une exception à partir d’AEM 6.5, Service Pack 17 et versions ultérieures. La fusion des ressources Sling 1.4.4 doit être incluse dans le Service Pack 20. (NPR-41630) NORMAL

#### Traduction{#foundation-translation-6520}

* Suite au déploiement d’AEM 6.5 Service Pack 18, un problème s’est produit avec l’onglet Filtres de l’éditeur de règles de traduction. Lorsqu’un contexte est sélectionné, en cliquant sur Modifier > Enregistrer, un guillemet double apparaît comme caractère de HTML la prochaine fois que vous ouvrirez le même contexte. Essentiellement, les règles de traduction n’étaient pas correctement enregistrées. (NPR-41624) MAJEUR
* Problèmes liés aux traductions de fragments de contenu, où les chaînes traduites sont renvoyées du fournisseur de traduction vers AEM, mais sont bloquées au niveau de la fonction `/content/projects` et ne pas mettre à jour les fragments de contenu. (NPR-41516) MAJEUR
* Un message d’erreur s’affiche lors de la création d’une copie de langue. Elle se produit sur une page dont un fragment de contenu est référencé dans une propriété de page, à l’aide de modèles de fragment de contenu. (NPR-41441) MAJEUR
* Les liens dans les fragments d’expérience ne sont pas ajustés à la langue correcte lors de la copie de la langue. Le fragment d’expérience pointe plutôt vers le paramètre régional principal. (NPR-41343) NORMAL

#### Interface utilisateur{#foundation-ui-6520}

* Une erreur de console se produit après une mise à niveau vers AEM 6.5, Service Pack 18. L’erreur se trouve dans la variable `coralUI3.js` et cela se produit lorsque vous sélectionnez une liste déroulante dans AEM. Plus précisément, cela se produit avec une `onOverlayToggle` . L&#39;erreur `Uncaught TypeError: Cannot read properties of null (reading 'innerText')` s’affiche. (NPR-41467) MAJEUR
* Dans AEM, **[!UICONTROL Outils]** > **[!UICONTROL Général]** > **[!UICONTROL Balisage]** > **[!UICONTROL Créer]** > **[!UICONTROL Créer une balise]**, saisie de caractères non latins dans la variable **Titre** entraîne la création du champ **Nom** champ à remplir uniquement avec le trait d’union ( `-` ). (NPR-41623) NORMAL
* L’année du copyright est incorrecte dans la variable `About Adobe Experience Manager` de la boîte de dialogue (NPR-41526) NORMAL
* Il n’y a pas de traduction **[!UICONTROL Propriétés du profil]** chaînes lors de la modification des paramètres utilisateur. Se produit dans tous les paramètres régionaux. (NPR-41365) NORMAL

<!-- #### WCM{#wcm-6520}

* text

#### Workflow{#foundation-workflow-6520}

* text -->

## Installer [!DNL Experience Manager] 6.5.20.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.20.0 nécessite [!DNL Experience Manager] 6.5. Consultez la [documentation de mise à niveau](/help/sites-deploying/upgrade.md) pour des instructions détaillées. <!-- UPDATE FOR EACH NEW RELEASE -->
* Le téléchargement du Pack de services est disponible dans la [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.20.0.zip) d’Adobe.
* Lors d’un déploiement avec MongoDB et plusieurs instances, installez [!DNL Experience Manager] 6.5.20.0 sur l’une des instances de création à l’aide du gestionnaire de modules.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe ne recommande pas de supprimer ou de désinstaller le package [!DNL Experience Manager] 6.5.20.0. Par conséquent, avant d’installer le module, vous devez créer une sauvegarde du `crx-repository` au cas où vous auriez besoin de le restaurer. <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### Installation du pack de services sur [!DNL Experience Manager] 6.5{#install-service-pack}

1. Redémarrez l’instance avant l’installation si l’instance est en mode de mise à jour (lorsque l’instance a été mise à jour à partir d’une version antérieure). Adobe recommande un redémarrage si le temps de disponibilité actuel d’une instance est élevé.

1. Avant l’installation, prenez un instantané ou exécutez une sauvegarde récente de votre instance [!DNL Experience Manager].

1. Téléchargez le pack de services à partir de la [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.20.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Ouvrez le gestionnaire de modules et cliquez sur **[!UICONTROL Charger le module]** pour charger le module. Pour en savoir plus, consultez la section [Gestionnaire de modules](/help/sites-administering/package-manager.md).

1. Sélectionnez le module, puis sélectionnez **[!UICONTROL Installer]**.

1. Pour mettre à jour le connecteur S3, arrêtez l’instance après l’installation du pack de services, remplacez le connecteur existant par un nouveau fichier binaire fourni dans le dossier d’installation, puis redémarrez l’instance. Consultez la section [Entrepôt de données S3 Amazon](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>La boîte de dialogue de l’interface utilisateur du gestionnaire de packages se ferme parfois pendant l’installation du pack de services. Adobe recommande d’attendre que les journaux d’erreurs se stabilisent avant d’accéder au déploiement. Attendez les journaux spécifiques liés à la désinstallation de la mise à jour complète pour vous assurer que l’installation est réussie. En règle générale, ce problème se produit dans [!DNL Safari] mais peut se produire par intermittence sur n’importe quel navigateur.

**Installation automatique**

Vous pouvez utiliser deux méthodes différentes pour installer automatiquement [!DNL Experience Manager] 6.5.20.0.<!-- UPDATE FOR EACH NEW RELEASE -->

* Placez le package dans le dossier `../crx-quickstart/install` lorsque le serveur est disponible en ligne. Le package est automatiquement installé.
* Utilisez l’[API HTTP à partir du gestionnaire de packages](/help/sites-administering/package-manager.md#package-share). Utilisez `cmd=install&recursive=true` afin que les packages imbriqués soient installés.

>[!NOTE]
>
>Experience Manager 6.5.20.0 ne prend pas en charge l’installation en Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Validation de l’installation**

Pour connaître les plateformes certifiées pour travailler avec cette version, reportez-vous à la section des [exigences techniques](/help/sites-deploying/technical-requirements.md).

1. La page d’informations sur les produits (`/system/console/productinfo`) affiche le numéro de version mis à jour `Adobe Experience Manager (6.5.20.0)` sous [!UICONTROL Produits installés]. <!-- UPDATE FOR EACH NEW RELEASE -->.

1. Tous les bundles OSGi sont au statut **[!UICONTROL ACTIF]** ou **[!UICONTROL FRAGMENT]** dans la console OSGi (utilisez la console web : `/system/console/bundles`).

1. Le lot OSGi `org.apache.jackrabbit.oak-core` est version 1.22.18 ou ultérieure (Utiliser la console web : `/system/console/bundles`). <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### Installer le Pack de services pour [!DNL Experience Manager] Forms{#install-aem-forms-add-on-package}

Pour obtenir des instructions sur l’installation du Pack de services sur Experience Manager Forms, voir les [instructions d’installation du Pack de services Experience Manager Forms](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

>[!NOTE]
>
>La fonctionnalité de formulaires adaptatifs, disponible dans [AEM 6.5 QuickStart](https://experienceleague.adobe.com/docs/experience-manager-65/content/implementing/deploying/deploying/deploy.html), est conçue à des fins d’exploration et d’évaluation uniquement. Pour une utilisation à des fins de production, il est essentiel d’obtenir une licence valide pour AEM Forms, car la fonctionnalité de formulaires adaptatifs nécessite une licence appropriée.

### Installer le package d’index GraphQL pour les fragments de contenu d’Experience Manager{#install-aem-graphql-index-add-on-package}

La clientèle qui utilise GraphQL doit installer le [fragment de contenu d’Experience Manager avec le package d’index GraphQL 1.1.1](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip).

Vous pouvez ainsi ajouter la définition d’index requise selon les fonctionnalités que vous utilisez réellement.

L’échec de l’installation de ce package peut entraîner des requêtes GraphQL lentes ou en échec.

>[!NOTE]
>
>N’installez ce package qu’une seule fois par instance ; il n’est pas nécessaire de le réinstaller avec chaque Pack de services.

### UberJar{#uber-jar}

UberJar pour [!DNL Experience Manager] 6.5.20.0 est disponible dans le [référentiel central Maven](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.20/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Pour utiliser UberJar dans un projet Maven, consultez la section [Utilisation d’UberJar](/help/sites-developing/ht-projects-maven.md) et incluez la dépendance suivante dans le POM de votre projet : <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.20</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar et les autres artefacts associés sont disponibles sur le référentiel central Maven au lieu du référentiel Maven public Adobe (`repo.adobe.com`). Le fichier UberJar principal est renommé `uber-jar-<version>.jar`. Il n’existe donc pas de `classifier` avec `apis` comme valeur pour la balise `dependency`.

## Fonctionnalités obsolètes et supprimées{#removed-deprecated-features}

Consultez les [fonctionnalités obsolètes et supprimées](/help/release-notes/deprecated-removed-features.md/).

## Problèmes connus{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST.-->

<!-- * **Page publishing not working in Page Editor after upgrading to Service Pack 18 (6.5.18.0)** -->

<!-- https://jira.corp.adobe.com/browse/SITES-15856 REMOVE FOR 6.5.19.0 -->
<!-- After you upgrade an instance of AEM 6.5.0.0&mdash;6.5.17.0 to AEM 6.5.19.0, when you click **Publish Page** inside the Page Editor, you are redirected to a URL that does not exist.

  To work around this issue, do one of the following:

  * Remove the following "path" property.

       `/libs/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/publish/granite:data`

  * Paste the correct URL directly into the browser.

       `http://localhost:4504/editor.html/libs/wcm/core/content/sites/publishpagewizard.html?item=/content/we-retail/language-masters/en/about-us.html` -->



* **Lié à Oak**
Depuis le pack de services 13 et les versions ultérieures, le journal d’erreur suivant a commencé à s’afficher, ce qui affecte le cache de persistance :

  ```shell
  org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.0.202/5]
  at org.h2.mvstore.DataUtils.newMVStoreException(DataUtils.java:1004)
      at org.h2.mvstore.MVStore.getUnsupportedWriteFormatException(MVStore.java:1059)
      at org.h2.mvstore.MVStore.readStoreHeader(MVStore.java:878)
      at org.h2.mvstore.MVStore.<init>(MVStore.java:455)
      at org.h2.mvstore.MVStore$Builder.open(MVStore.java:4052)
      at org.h2.mvstore.db.Store.<init>(Store.java:129)
  ```

  Ou

  ```shell
  org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.1.214/5].
  ```

  Pour résoudre cette exception, procédez comme suit :

   1. Supprimez les deux dossiers suivants de `crx-quickstart/repository/`

      * `cache`
      * `diff-cache`

   1. Installez le Pack de services ou redémarrez Experience Manager as a Cloud Service.
Les nouveaux dossiers `cache` et `diff-cache` sont automatiquement créés et vous ne voyez plus d’exception liée à `mvstore` dans `error.log`.

* Mettez à jour vos requêtes GraphQL qui peuvent avoir utilisé un nom d’API personnalisé pour votre modèle de contenu afin d’utiliser plutôt le nom par défaut du modèle de contenu.

* Une requête GraphQL peut utiliser l’index `damAssetLucene` plutôt que l’index `fragments`. Il peut en résulter l’échec des requêtes GraphQL ou l’exécution de celles-ci peut prendre beaucoup de temps.

  Pour résoudre le problème, `damAssetLucene` doit être configuré pour inclure les deux propriétés suivantes sous `/indexRules/dam:Asset/properties` :

   * `contentFragment`
      * `jcr:primaryType="nt:unstructured"`
      * `name="jcr:content/contentFragment"`
      * `propertyIndex="{Boolean}true"`
      * `type="Boolean"`
   * `model`
      * `jcr:primaryType="nt:unstructured"`
      * `name="jcr:content/data/cq:model"`
      * `ordered="{Boolean}true"`
      * `propertyIndex="{Boolean}true"`
      * `type="String"`

  Une fois la définition d’index modifiée, une réindexation est nécessaire (`reindex` = `true`).

  Après ces étapes, les requêtes GraphQL doivent être plus rapides.

* Lorsque vous tentez de déplacer, de supprimer ou de publier des fragments de contenu, des sites ou des pages, un problème se produit lorsque les références aux fragments de contenu sont récupérées, car la requête en arrière-plan échoue. En d’autres termes, la fonctionnalité ne fonctionne pas.
Pour garantir le bon fonctionnement de cette opération, vous devez ajouter les propriétés suivantes au nœud de définition d’index `/oak:index/damAssetLucene` (aucune réindexation n’est requise) :

  ```xml
  "tags": [
      "visualSimilaritySearch"
    ]
  "refresh": true
  ```

* Si vous mettez à niveau votre instance [!DNL Experience Manager] de 6.5.0 à 6.5.4, jusqu’au dernier Service Pack sur Java™ 11, les exceptions `RRD4JReporter` s’affichent dans le fichier `error.log`. Pour arrêter les exceptions, redémarrez votre instance d’[!DNL Experience Manager]. <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* Les utilisateurs peuvent renommer un dossier dans une hiérarchie dans [!DNL Assets] et publier un dossier imbriqué dans [!DNL Brand Portal]. Toutefois, le titre du dossier n’est pas mis à jour dans [!DNL Brand Portal] jusqu’à ce que le dossier racine soit republié.

* Les erreurs et messages d’avertissement suivants peuvent s’afficher lors de l’installation d’[!DNL Experience Manager] 6.5.x.x :
   * « Lorsque l’intégration d’Adobe Target est configurée dans [!DNL Experience Manager] à l’aide de l’API Target Standard (authentification IMS), l’exportation de fragments d’expérience vers Target entraîne la création de types d’offres incorrects. » Au lieu du type « Fragment d’expérience » / source « Adobe Experience Manager », Target crée plusieurs offres avec le type « HTML » / source « Adobe Target Classic ».
   * `com.adobe.granite.maintenance.impl.TaskScheduler` : aucune fenêtre de maintenance n’a été trouvée sur granite/operations/maintenance.
   * La validation côté serveur du formulaire adaptatif échoue lorsque des fonctions d’agrégat telles que SUM, MAX et MIN sont utilisées (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Aucune fenêtre de maintenance n’a été trouvée sur granite/operations/maintenance.
   * La zone réactive d’une image interactive de Dynamic Media n’est pas visible lors de la prévisualisation du fichier via la visionneuse de bannières avec achat.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : temporisation en attente de modification d’enregistrement pour terminer la désinscription.

* À partir de la version 6.5.15 d’AEM, le moteur JavaScript Rhino fourni par le lot ```org.apache.servicemix.bundles.rhino``` a un nouveau comportement d’hébergement. Les scripts qui utilisent le mode strict (```use strict;```) doivent déclarer correctement leurs variables, sinon ils ne seront pas exécutés et génèreront une erreur d’exécution.

### Problèmes connus d’AEM Forms

#### Plateformes prises en charge

* JDK 11.0.20 n’est pas pris en charge pour installer le programme d’installation AEM Forms on JEE. Seules la version JDK 11.0.19 ou les versions antérieures sont prises en charge pour installer le programme d’installation AEM Forms on JEE. (FORMS-10659)

#### Installation

* Sur la plateforme JBoss® 7.1.4, lorsque l’utilisateur ou l’utilisatrice installe le pack de services Experience Manager 6.5.16.0, le déploiement de `adobe-livecycle-jboss.ear` échoue. (CQ-4351522, CQDOC-20159)

<!-- 
* After upgrading to AEM Forms 6.5.18.0 JBoss&reg; Turnkey full installer environment on Windows Server 2022, when compiling Output client application code using Java&trade; 11, the following compilation error may occur:
  
  ```
  error: error reading [AEM_Forms_Installation_dir]\sdk\client-libs\common\adobe-output-client.jar; java.net.URISyntaxException: 
  Illegal character in path at index 70: file:/[AEM_Forms_Installation_dir]/sdk/client-libs/common/${clover.jar.name} 1 error
  
  ```
  
  To resolve the issue, perform the following steps:
    1. Navigate to `[AEM_Forms_Installation_dir]\sdk\client-libs\common\` and unzip `adobe-output-client.jar` to extract the `Manifest.mf` file.
    1. Update the `Manifest.mf` file by removing the entry `${clover.jar.name}` from the class-path attribute. 

        >[!NOTE]
        >
        > You can also use an in-place editing tool, for example, 7-zip, to update the `Manifest.mf` file.  

    1. Save the updated the `Manifest.mf` in the `adobe-output-client.jar` archive. 
    1. Save the modified `adobe-output-client.jar` file and rerun the setup. (CQDOC-20878) -->

* Après l’installation du programme d’installation complet AEM Service Pack 6.5.20.0, le déploiement EAR échoue sur JEE à l’aide de JBoss® clé en main. <!-- UPDATE FOR EACH NEW RELEASE -->

Pour résoudre le problème, recherchez le fichier `<AEM_Forms_Installation_dir>\jboss\bin\standalone.bat` et mettez à jour `Adobe_Adobe_JAVA_HOME` vers `Adobe_JAVA_HOME` pour toutes les occurrences avant d’exécuter Configuration Manager. (CQDOC-20803)

#### Installer le fragment de servlet (Pack de services AEM 6.5.14.0 ou version antérieure)

* Si vous effectuez une mise à niveau vers AEM Service Pack 6.5.15.0 ou version ultérieure et que votre instance AEM fonctionne sur Tomcat 8.5.88, il est obligatoire d’installer le fragment de servlet. Procédez à cette installation *before* vous procédez à l&#39;installation du Service Pack 6.5.15.0 ou supérieur.
* Il est obligatoire d’installer le fragment de servlet pour tous les serveurs d’applications, à l’exception de ceux qui s’exécutent sur JBoss® EAP 7.4.0.

**Pour installer le fragment de servlet :**

1. Téléchargez le fragment de servlet à partir de la [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar).
1. Démarrez le serveur d’applications.
1. Attendez que les journaux se stabilisent et vérifiez l’état du bundle.
1. Ouvrez les lots de la console web. L’URL par défaut est `http://[Server]:[Port]/system/console/bundles`.
1. Cliquez sur **[!UICONTROL Installer]** ou **[!UICONTROL Mettre à jour]**.
1. Sélectionner le fragment téléchargé
   `org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar`
1. Cliquez sur **[!UICONTROL Installer]** ou **[!UICONTROL Mettre à jour]**.
1. Attendez que le serveur d’applications se stabilise.
1. Arrêtez le serveur d’applications.

#### Formulaires adaptatifs

* Lorsqu’un formulaire adaptatif est publié, toutes ses dépendances, y compris les stratégies, sont republiées, même si aucune modification ne leur a été apportée. (FORMS-10454)
* Lorsqu’un utilisateur ou une utilisatrice choisit de configurer un champ pour la première fois dans un formulaire adaptatif, l’option permettant d’enregistrer une configuration ne s’affiche pas dans l’explorateur de propriétés. Sélectionner un autre champ du formulaire adaptatif à configurer dans le même éditeur pour résoudre le problème.
* Lorsque des utilisateurs ou des utilisatrices exécutent l’action d’envoi, l’envoi échoue avec une erreur :
  `javax.servlet.ServletException: java.lang.NoSuchMethodError`
Pour résoudre le problème, [recompilez les scripts Sling tels que JSP, Java™ et Sightly](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-16543.html?lang=fr#resolution). (FORMS-8542)
* Après avoir installé le Pack de services AEM 6.5.14.0 et versions ultérieures, les utilisateurs et utilisatrices ne peuvent pas sélectionner de police dans l’interface utilisateur d’administration de JEE pour les documents PDF lorsqu’ils accèdent à `Home` > `Services` > `PDF Generator` > `Adobe PDF Settings`, car la liste des polices s’affiche vide. (FORMS-12095)
<!-- When a form is signed using the OOTB Scribble Signature component, it appears in the image dialogue but does not preview and appears blank when you click on it. (FORMS-12073). A hotfix is available for this issue. To download and install the hotfix, see [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md) -->
* Dans AEM Forms on JEE, le rendu de HTML5 Forms qui utilise le chemin d’accès au contexte échoue. (FORMS-12485, FORMS-12691) Un correctif est disponible pour ce problème. Pour télécharger et installer le correctif, voir [Correctifs Adobe Experience Manager Forms](/help/release-notes/aem-forms-hotfix.md).
* Le Forms adaptatif vous permet d’utiliser des fonctions personnalisées avec ECMAScript version 5 ou antérieure. Lorsqu’une fonction personnalisée utilise ECMAScript version 6 ou ultérieure, comme les fonctions &quot;let&quot;, &quot;const&quot; ou flèches, l’éditeur de règles peut ne pas s’ouvrir correctement.

#### d’AEM Forms on JEE

* Des vulnérabilités de sécurité critiques ont été signalées pour Struts 2 RCE, un framework d’applications web populaire et open source pour le développement d’applications web Java™ EE. Adobe a publié le [pack de services 19.1 (6.5.19.1) pour AEM 6.5](/help/forms/using/mitigating-struts-2-rce-vulnerabilities-for-experience-manager-manager-form.md) afin de résoudre la vulnérabilité dans AEM Forms on JEE.

<!--The font enumeration fails due to the missing Ps2Pdf service file.-->

## Bundles OSGi et packages de contenu inclus{#osgi-bundles-and-content-packages-included}

Les documents texte suivants répertorient les lots OSGi et les packages de contenu inclus dans ce [!DNL Experience Manager] Version 6.5 du Service Pack :

* [Liste des bundles OSGi inclus dans Experience Manager 6.5.20.0](/help/release-notes/assets/65200-bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Liste des packages de contenu inclus dans Experience Manager 6.5.20.0](/help/release-notes/assets/65200-packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Sites web à accès limité{#restricted-sites}

Ces sites Web sont disponibles uniquement pour les clients. Si vous êtes client et avez besoin d’un accès, contactez votre responsable de compte Adobe.

* [Téléchargement du produit à l’adresse licensing.adobe.com](https://licensing.adobe.com/)
* [Contacter l’assistance clientèle Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=fr).

>[!MORELIKETHIS]
>
>* Page des produits [[!DNL Experience Manager] ](https://business.adobe.com/fr/products/experience-manager/adobe-experience-manager.html)
>* Documentation [[!DNL Experience Manager]  6.5](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=fr)
>* [Abonnement aux mises à jour prioritaires de produits d’Adobe](https://www.adobe.com/subscription/priority-product-update.html)
