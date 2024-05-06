---
title: Notes de mise à jour de la version 6.5 d’ [!DNL Adobe Experience Manager]
description: Consultez les informations sur la mise à jour, y compris les nouveautés, la procédure d’installation et une liste complète des modifications pour [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: d6435255835d91729519f7822b9677608b6b9f1e
workflow-type: tm+mt
source-wordcount: '2063'
ht-degree: 66%

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
| Version | 6.5.21.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Type | Mise à jour du pack de services |
| Date | Vendredi 23 mai 2024 <!-- UPDATE FOR EACH NEW RELEASE --> |
| URL de téléchargement | [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/fr/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.20.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## Éléments compris dans [!DNL Experience Manager] 6.5.21.0 {#what-is-included-in-aem-6521}

[!DNL Experience Manager] 6.5.21.0 comprend de nouvelles fonctionnalités, des améliorations importantes demandées par les clientes et les clients, des correctifs de bugs ainsi que des améliorations en termes de performances, de stabilité et de sécurité, publiés depuis la version initiale 6.5 en avril 2019. [Installez ce pack de services](#install) dans [!DNL Experience Manager] 6.5.

<!-- UPDATE FOR EACH NEW RELEASE -->

## Principales fonctionnalités et améliorations

<!-- * _6.5.21.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

Voici quelques-unes des fonctionnalités et améliorations clés de cette version :

* Nouvelle méthode plus simple d’utilisation des informations d’identification pour l’authentification serveur à serveur, remplaçant les informations d’identification du compte de service (JWT) existantes. (NPR-41994) MAJOR

### [!DNL Forms]

* A

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## Problèmes corrigés dans le pack de services 21 {#fixed-issues}

### [!DNL Sites]{#sites-6521}

#### Accessibilité {#sites-accessibility-6521}

* La variable **[!UICONTROL Recherches enregistrées]** n’est pas persistante. L’espace réservé est utilisé comme seul libellé visuel pour un champ de texte.(SITES-3050)

#### Interface utilisateur d’administration{#sites-adminui-6521}

* Lorsque vous cliquez **[!UICONTROL Sites]** > **[!UICONTROL Composants principaux]** > **[!UICONTROL Propriétés]** > **[!UICONTROL Autorisations]** onglet > **[!UICONTROL Autorisation effective]**, la variable **Autorisations effectives** ne s’ouvre pas dans . (SITES-17378)

#### Interface utilisateur classique{#sites-classicui-6521}

* T

#### [!DNL Content Fragments]{#sites-contentfragments-6521}

* Correction de la double inclusion des éléments de formulaire. (SITES-21109) BLOQUEUR
* Lors de la création d’un fragment de contenu, le bouton Fermer ne répond parfois pas, entraînant le gel de la page entière et nécessitant une actualisation de la page pour fermer le fragment de contenu. En ce qui concerne le problème de création de version, le système crée une nouvelle version d’un fragment de contenu même lorsque l’utilisateur n’a apporté aucune modification, simplement en interagissant avec l’éditeur de texte enrichi ou un champ de texte. (SITES-21187) MAJOR


#### [!DNL Content Fragments] - API GraphQL {#sites-graphql-api-6521}

* Lors de la mise à niveau de Adobe Experience Manager de 6.5.19.0 vers 6.5.20.0, le chemin d’accès `/libs/cq/graphql/sites/graphiql` était supprimé. (SITES-20098) CRITIQUE




#### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6521}

* M

#### [!DNL Content Fragments] - API REST{#sites-restapi-6521}

* M

#### Back-end principal{#sites-core-backend-6521}

* M

#### Composants principaux{#sites-core-components-6521}

* I

#### Intégration de campagne{#sites-campaign-integration-6521}

* A

#### Fragments d’expérience{#sites-experiencefragments-6521}

* Déploiement des fragments d’expérience depuis `masters/language` to `country/language` ne met pas à jour les références croisées. (SITES-20559) BLOQUEUR
* Modèles non seulement spécifiés dans la variable `cq:allowedTemplates`, mais les modèles qui ont `allowedPaths` configurés au niveau du modèle, apparaissent sous la forme d’options lors de la création d’un fragment d’expérience. (SITES-20855) MAJOR

#### Composants de base (hérités){#sites-foundation-components-legacy-6521}

* T

#### Lancements{#sites-launches-6521}

* La variable `sourceRootResource` configuré dans la configuration de Launch dans CRXDE Lite pointe vers du contenu qui n’existe plus, ce qui entraîne un dysfonctionnement lorsque des tentatives de suppression sont effectuées. Vous devriez pouvoir supprimer les lancements même si la page est supprimée ou si le chemin d’accès n’est pas le même. (SITES-20750)

#### MSM - Live Copies{#sites-msm-live-copies-6521}

* Recouvrement du composant Page pour ajouter des onglets dans les propriétés de page. L’une d’elles est la configuration de page et possède une propriété permettant d’ajouter une URL de fragment d’expérience. Le lien configuré dans les propriétés de page pour le fragment d’expérience ne change pour aucune copie de langue créée pour cette page. Le lien configuré doit changer avec l’URL de la copie de langue. (SITES-19580) MAJOR

#### Éditeur de page{#sites-pageeditor-6521}

* Le mode d’édition applique de manière incohérente un arrière-plan gris, qui ne respecte pas les normes de contraste des couleurs WCAG (Web Content Accessibility Guidelines). (SITES-20060)

### [!DNL Assets]{#assets-6521}

* u

#### [!DNL Dynamic Media]{#assets-dm-6521}

* À compter du 1er mai 2024, Adobe Dynamic Media ne prendra plus en charge les éléments suivants :
   * SSL (Secure Socket Layer) 2.0
   * SSL 3.0
   * TLS (Transport Layer Security) 1.0 et 1.1
   * Les chiffrements faibles suivants dans TLS 1.2 :
      * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384`
      * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA`
      * `TLS_RSA_WITH_AES_256_GCM_SHA384`
      * `TLS_RSA_WITH_AES_256_CBC_SHA256`
      * `TLS_RSA_WITH_AES_256_CBC_SHA`
      * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256`
      * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA`
      * `TLS_RSA_WITH_AES_128_GCM_SHA256`
      * `TLS_RSA_WITH_AES_128_CBC_SHA256`
      * `TLS_RSA_WITH_AES_128_CBC_SHA`
      * `TLS_RSA_WITH_CAMELLIA_256_CBC_SHA`
      * `TLS_RSA_WITH_CAMELLIA_128_CBC_SHA`
      * `TLS_ECDHE_RSA_WITH_3DES_EDE_CBC_SHA`
      * `TLS_RSA_WITH_SDES_EDE_CBC_SHA`

### [!DNL Forms]{#forms-6521}

<!--Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the AEM 6.5.21.0 Forms add-on package release is scheduled for Thursday, May 30, 2024. A list of Forms fixes and enhancements is added to this section post the release.-->

#### [!DNL Adaptive Forms]

* 
  <!-- THIS BUG WAS ALREADY REPORTED IN 6.5.20.0 RELEASE NOTES. IS IT NEEDED AGAIN IN THE 6.5.21.0 RELEASE NOTES? (AEM Forms on JEE Only) The PDF Generator service fails to enumerate the fonts available on the server. Consequently, the font selection panel on the Adobe PDF Settings page in the PDFG Admin UI remains empty, effectively preventing (un)embedding of chosen fonts. (FORMS-12095) -->


#### [!DNL Forms Designer] {#forms-designer-6521}

* M


### Foundation {#foundation-6521}



#### Apache Felix {#felix-6521}

* Problème de mise à niveau avec AEM 6.5 Service Pack 19 (SP19) dans lequel le chemin racine du contexte du serveur d’applications est absent pour les demandes non autorisées vers Apache Felix suite à l’installation de SP19. Mise à jour vers la console de gestion web Apache Felix 4.9.8. (NPR-41933)

* u

#### Communities {#communities-6521}

* T

#### Distribution de contenu{#foundation-content-distribution-6521}

* T

#### Intégrations{#integrations-6521}

* Remplacement des informations d’identification du compte de service (JSON Web Token ou JWT) par les informations d’identification OAuth2 Server-to-Server (également appelées &quot;entités de service&quot;).(NPR-41994) MAJOR
* Échec de la création de la demande d’audience avec la configuration IMS (Identity Management System). (NPR-41888) MAJOR
* Lorsqu’un client tente d’afficher la page Payload, le contenu ne s’affiche pas correctement en raison d’une URL incorrecte ; une erreur 404 s’affiche. L’erreur est provoquée par l’absence d’un symbole de point d’interrogation dans l’URL, devant les paramètres de la requête. Pour ce problème, le client doit insérer manuellement le symbole du point d’interrogation afin d’afficher correctement la page Payload. (NPR-41957)
* Supprimez le code et la dépendance de l’Search &amp; Promote d’Adobe d’AEM 6.5 qui a atteint [fin de vie Septembre 2022 selon les avis](https://experienceleague.adobe.com/en/docs/discontinued/using/search-promote). (NPR-41855)


#### Localisation{#localization-6521}

* Dans l’éditeur de modèles, la chaîne de texte *`No video available.`* n’est pas localisé. (SITES-13190)

#### Plateforme{#foundation-platform-6521}

* La variable `Unclosed resource resolver` est en cours d’expérience pour `com.day.cq.mailer.impl.DefaultMailService`. La variable `MessageGatewayService` , qui est prête à l’emploi, était utilisée sans résolveur de ressources. Le problème s’est produit sur n’importe quelle page avec un bouton d’envoi de formulaire qui envoie un courrier électronique à l’aide de cette classe. (NPR-41853)

#### Sling{#foundation-sling-6521}

* T

#### Traduction{#foundation-translation-6521}

* Lors de la création de plusieurs configurations et de l’accès aux configurations de Cloud Service de traduction, tous les éléments ne s’affichent pas dans l’interface utilisateur. Seuls les 40 premiers éléments/dossiers s’affichent, le chargement différé est déclenché mais n’ajoute pas de contenu supplémentaire. (NPR-41829)

#### Interface utilisateur{#foundation-ui-6521}

* Le Granite `pathfield` component at `/libs/granite/ui/components/coral/foundation/form/pathfield` ne parvient pas à activer la variable **[!UICONTROL Sélectionner]** lorsqu’une ressource est sélectionnée. Une fois que le champ de chemin d’accès s’affiche et que l’utilisateur coche la case de la ressource, la variable **[!UICONTROL Sélectionner]** n’est pas activé ; il ne passe pas du gris au bleu. (NPR-41970)
* Il existe un problème avec le champ de référence CFM (Content Fragment Model) dans AEM. Bien que le champ de référence CFM soit défini comme obligatoire, le système permet aux utilisateurs de cliquer sur Enregistrer pour enregistrer le contenu avec des valeurs non CFM dans certains scénarios. Le bouton Enregistrer doit être grisé (indisponible). (NPR-41894)

#### Gestion de contenu web (WCM){#wcm-6521}

* T

#### Workflow{#foundation-workflow-6521}

* T

## Installer [!DNL Experience Manager] 6.5.21.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.21.0 nécessite [!DNL Experience Manager] 6.5. Consultez la [documentation de mise à niveau](/help/sites-deploying/upgrade.md) pour des instructions détaillées. <!-- UPDATE FOR EACH NEW RELEASE -->
* Le téléchargement du pack de services est disponible dans la [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/fr/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.20.0.zip) d’Adobe.
* Lors d’un déploiement avec MongoDB et plusieurs instances, installez [!DNL Experience Manager] 6.5.21.0 sur l’une des instances de création à l’aide du gestionnaire de packages.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe ne recommande pas de supprimer ou de désinstaller le package [!DNL Experience Manager] 6.5.21.0. Par conséquent, avant d’installer le module, vous devez créer une sauvegarde du `crx-repository` au cas où vous auriez besoin de le restaurer. <!-- UPDATE FOR EACH NEW RELEASE -->
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

Vous pouvez utiliser deux méthodes différentes pour installer automatiquement [!DNL Experience Manager] 6.5.21.0.<!-- UPDATE FOR EACH NEW RELEASE -->

* Placez le package dans le dossier `../crx-quickstart/install` lorsque le serveur est disponible en ligne. Le package est automatiquement installé.
* Utilisez l’[API HTTP à partir du gestionnaire de packages](/help/sites-administering/package-manager.md#package-share). Utilisez `cmd=install&recursive=true` afin que les packages imbriqués soient installés.

>[!NOTE]
>
>Experience Manager 6.5.21.0 ne prend pas en charge l’installation en Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Validation de l’installation**

Pour connaître les plateformes certifiées pour travailler avec cette version, reportez-vous à la section des [exigences techniques](/help/sites-deploying/technical-requirements.md).

1. La page d’informations sur les produits (`/system/console/productinfo`) affiche le numéro de version mis à jour `Adobe Experience Manager (6.5.21.0)` sous [!UICONTROL Produits installés]. <!-- UPDATE FOR EACH NEW RELEASE -->.

1. Tous les bundles OSGi sont au statut **[!UICONTROL ACTIF]** ou **[!UICONTROL FRAGMENT]** dans la console OSGi (utilisez la console web : `/system/console/bundles`).

1. Le lot OSGi `org.apache.jackrabbit.oak-core` est de version 1.22.18 ou ultérieure (utilisez la console web : `/system/console/bundles`). <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### Installer le Pack de services pour [!DNL Experience Manager] Forms{#install-aem-forms-add-on-package}

Pour obtenir des instructions sur l’installation du Pack de services sur Experience Manager Forms, voir les [instructions d’installation du Pack de services Experience Manager Forms](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

>[!NOTE]
>
>La fonctionnalité de formulaires adaptatifs, disponible dans [AEM 6.5 QuickStart](https://experienceleague.adobe.com/docs/experience-manager-65/content/implementing/deploying/deploying/deploy.html?lang=fr), est conçue à des fins d’exploration et d’évaluation uniquement. Pour une utilisation à des fins de production, il est essentiel d’obtenir une licence valide pour AEM Forms, car la fonctionnalité de formulaires adaptatifs nécessite une licence appropriée.

### Installer le package d’index GraphQL pour les fragments de contenu d’Experience Manager{#install-aem-graphql-index-add-on-package}

La clientèle qui utilise GraphQL doit installer le [fragment de contenu d’Experience Manager avec le package d’index GraphQL 1.1.1](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip).

Vous pouvez ainsi ajouter la définition d’index requise selon les fonctionnalités que vous utilisez réellement.

L’échec de l’installation de ce package peut entraîner des requêtes GraphQL lentes ou en échec.

>[!NOTE]
>
>N’installez ce package qu’une seule fois par instance ; il n’est pas nécessaire de le réinstaller avec chaque Pack de services.

### UberJar{#uber-jar}

UberJar pour [!DNL Experience Manager] 6.5.21.0 est disponible dans le [référentiel central Maven](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.20/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Pour utiliser UberJar dans un projet Maven, consultez la section [Utilisation d’UberJar](/help/sites-developing/ht-projects-maven.md) et incluez la dépendance suivante dans le POM de votre projet : <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
  <dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>uber-jar</artifactId>
  <version>6.5.21</version>
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

* L’installation du balisage du contenu prêt à l’emploi par le biais d’un package de mise à jour officiel (y compris les packs de services, les packs de services de sécurité, les packs de fonctionnalités étendues, les packs de fonctionnalités cumulatives, les correctifs et autres) réinitialise la propriété languages du nœud `/content/cq:tags` par défaut. Il est donc nécessaire de l’ajouter à partir des propriétés avant l’installation.

### Problèmes connus pour AEM Sites {#known-issues-aem-sites-6521}

* SITES-17934 - Fragments de contenu - La prévisualisation échoue en raison de la protection DoS pour une grande arborescence de fragments. Voir [Article de la base de connaissances sur les options de configuration de l’exécuteur de requête GraphQL par défaut](https://experienceleague.adobe.com/fr/docs/experience-cloud-kcs/kbarticles/ka-23945)

### Problèmes connus d’AEM Forms {#known-issues-aem-forms-6521}

* T

## Lots OSGi et packages de contenu inclus{#osgi-bundles-and-content-packages-included}

Les documents texte suivants répertorient les lots OSGi et les packages de contenu inclus dans cette version du pack de services [!DNL Experience Manager] 6.5.

* [Liste des lots OSGi inclus dans Experience Manager 6.5.21.0](/help/release-notes/assets/65200-bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Liste des packages de contenu inclus dans Experience Manager 6.5.21.0](/help/release-notes/assets/65200-packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Sites web à accès limité{#restricted-sites}

Ces sites Web sont disponibles uniquement pour les clients. Si vous êtes client et avez besoin d’un accès, contactez votre responsable de compte Adobe.

* [Téléchargement du produit à l’adresse licensing.adobe.com](https://licensing.adobe.com/)
* [Contacter l’assistance clientèle Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=fr).

>[!MORELIKETHIS]
>
>* Page des produits [[!DNL Experience Manager] ](https://business.adobe.com/fr/products/experience-manager/adobe-experience-manager.html)
>* Documentation [[!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=fr)
>* [Abonnement aux mises à jour prioritaires de produits d’Adobe](https://www.adobe.com/subscription/priority-product-update.html)
