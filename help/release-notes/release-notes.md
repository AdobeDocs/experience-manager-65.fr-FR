---
title: Notes de mise à jour de la version 6.5 d’ [!DNL Adobe Experience Manager]
description: Consultez les informations sur la mise à jour, y compris les nouveautés, la procédure d’installation et une liste complète des modifications pour  [!DNL Adobe Experience Manager]  6.5.
mini-toc-levels: 3
source-git-commit: 72b3eaea279911569dbd6b9acf41527111e9e53c
workflow-type: tm+mt
source-wordcount: '2665'
ht-degree: 44%

---

# Notes de mise à jour du dernier pack de services [!DNL Adobe Experience Manager] 6.5 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/Documents/issue_tracker_sp_cfp_updates.xlsx?d=w3ea81ae4e6054153b132f2698c86f84e&csf=1&web=1&e=WRAZ43&nav=MTVfezk2OTJDQTNFLUI4QTQtNDY2RS05NEVCLUQ5QjcyNEVENkJDNn0 -->

## Informations sur la version {#release-information}

| Produit | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Version | 6.5.16.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Type | Mise à jour du pack de services |
| Date | jeudi 23 février 2023 <!-- UPDATE FOR EACH NEW RELEASE --> |
| URL de téléchargement | [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?pack[...]be/packages/cq650/servicepack/aem-service-pkg-6.5.16.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## Éléments compris dans [!DNL Experience Manager] 6.5.16.0 {#what-is-included-in-aem-6516}

[!DNL Experience Manager] 6.5.16.0 comprend de nouvelles fonctionnalités, des améliorations importantes demandées par les client(e)s, des correctifs ainsi que des améliorations en termes de performances, de stabilité et de sécurité, publiés depuis la version initiale de 6.5 en avril 2019. [Installez ce pack de services](#install) dans [!DNL Experience Manager] 6.5. <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- Some of the key features and improvements are the following:

* _REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

Les améliorations clés apportées à Dynamic Media sont les suivantes :

Nouveau protocole DASH (Dynamic Adaptive Streaming over HTTP) prise en charge de la diffusion en continu à débit adaptatif dans les diffusions vidéo Dynamic Media (avec CMAF) [Format d’application de média commun] activée).

* La diffusion en continu adaptative (DASH/HLS) garantit une meilleure expérience de visionnage des vidéos par les utilisateurs finaux.
* La DASH est le protocole standard international pour la diffusion en continu de vidéos adaptatives, qui est largement adopté dans le secteur.
* Disponible maintenant en Amérique du Nord (disponible via un ticket de support), bientôt disponible en Asie-Pacifique et Europe-Moyen-Orient-Afrique.

Voir [Activation de DASH sur votre compte](/help/assets/video.md#enable-dash).

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## [!DNL Assets] {#assets-6516}

* Ressources connectées : Lorsque vous activez les options de recadrage intelligent pour les images sur DAM distant, chargez les images dans un dossier et synchronisez le dossier sur les sites locaux, le dossier ne s’ouvre pas sur le déploiement Sites local. (NPR-39912)
* Lors du tri d’une collection par nom, la vue de liste ne fonctionne pas correctement (ASSETS-19401).
* Lorsqu’un fichier multimédia volumineux (JPEG) est chargé dans les collections, Experience Manager cesse de répondre. (ASSETS-19387)
* Dans l’arborescence de contenu, le nom de la ressource affichée est incorrect, car l’emplacement de la ressource n’est pas rendu correctement. (ASSETS-18870)
* Lors du partage d’une collection à l’aide d’un lien, les données de l’URL ne correspondent pas entre le mélange du mode Carte et du mode Liste. (ASSETS-18758)
* Lorsque vous effectuez une omni-recherche en utilisant un filtre sur le type de dossier, les résultats de la recherche sont incohérents. (ASSETS-18227)
* Le `dam:size` n’est pas mise à jour après XMP écriture différée, ce qui entraîne le renvoi d’informations incorrectes à partir de la propriété `/platform/path/to/asset.jpg;resource=metadata` API. (ASSETS-17631)
* Résolveur de ressources non fermé sur toutes les instances de Experience Manager. (ASSETS-16904)
* Impossible de créer une version d’une ressource même si la fonction `create` et `modify` autorisations. (ASSETS-15956)
* Le `move` est désactivé de manière aléatoire lors du déplacement d’une ressource d’un point à un autre. (ASSETS-14889)
* Les lecteurs d’écran ne peuvent pas identifier les en-têtes, car le texte n’est pas défini dans les balises d’en-tête mais comme texte général. (ASSETS-6924)
* Le texte secondaire sous l’image n’est pas obligatoire, mais le texte affiché sous l’image est répétitif avec une `Type` attribut. (ASSETS-6915)


## [!DNL Assets] - [!DNL Dynamic Media] {#dm-6516}

* L’élément de formulaire ne contient pas de libellé. Avec les lecteurs d’écran tels que NVDA et JAWS, les informations sur les étiquettes de formulaire ne s’annoncent pas correctement. (CQ-4344078)
* Les listes déroulantes ne sont pas fermées lorsque la variable `Escape` est utilisée sur un clavier. (CQ-4344077)
* L’icône Informations (la lettre &quot;i&quot;) qui s’affiche pour la suggestion d’erreur en ligne après qu’une entrée non valide a été saisie n’est pas accessible à l’aide du clavier. (CQ-4344076)
* `getManifestURI` renvoie null en raison de la lecture d’une propriété JCR en tant que `toString` au lieu de `getString`. (ASSETS-18674)
* Le composant vidéo de recadrage intelligent ne fonctionne pas correctement. Le composant exécute la lecture au lieu de la diffusion en continu, et les appels VTT échouent, provoquant une erreur 404. (ASSETS-18468)
* Sélection **[!UICONTROL Propriétés]** sur la page Visionneuse d’une ressource, une exception de pointeur null est générée. (ASSETS-18420)
* [!DNL Experience Manager] Modifications de l’interface utilisateur pour la diffusion en continu DASH qui incluent les éléments suivants :
   * disposer d’un champ CMAF (Common Media Application Format) visible dans l’éditeur de profil vidéo.
   * le processus de chargement vidéo envoie un indicateur CMAF.
   * les options **[!UICONTROL auto]**, **[!UICONTROL hls]**, et **[!UICONTROL dash]** sont désormais disponibles dans la liste déroulante de lecture de l’éditeur de paramètres prédéfinis de la visionneuse. **[!UICONTROL Comportement]** .
(ASSETS-17428)
* Dans la navigation, lorsque vous sélectionnez **[!UICONTROL Ressources]** > **[!UICONTROL Fichiers]** > **[!UICONTROL Créer]** > **[!UICONTROL Ensemble de carrousel]**, l’icône d’image est chevauchée par la chaîne de texte &quot;Diapositive 1&quot;. (ASSETS-18578)
* Les ressources non publiées sont à nouveau publiées. (ASSETS-16428)
* L’auteur du Experience Manager tombe en panne en raison d’un problème de chargement, ce qui entraîne la création d’une alerte synthétique. (ASSETS-15937)
* Dans la page Paramètres généraux de Dynamic Media, un message d’erreur non traduit s’affiche. `Failed to fetch data` apparaît. (ASSETS-15617)

## [!DNL Forms] {#forms-6516}

### [!DNL Forms] Fonctions clés {#forms-features-6516}

* [Forms adaptatif sans affichage](https://experienceleague.corp.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html) permettent aux développeurs de créer, publier et gérer des formulaires interactifs accessibles et interactifs via des API, plutôt que par le biais d’une interface utilisateur graphique classique.

* [Composants principaux de Forms adaptatif](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html#features) sont un ensemble de 24 composants Open Source compatibles avec BEM qui sont construits sur la base des composants principaux de la gestion de contenu web Adobe Experience Manager. Ces composants sont Open Source et permettent aux développeurs de personnaliser et d’étendre facilement ces composants en fonction des besoins spécifiques de leur entreprise. Toute personne disposant de compétences pour personnaliser [Composants principaux WCM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/authoring.html?lang=en) peuvent facilement personnaliser et mettre en forme ces composants.

* Le service Reader Extension sur OSGi fournit désormais des options distinctes permettant d’importer et d’exporter des droits d’utilisation sur un PDF afin d’importer ou d’exporter des données dans Adobe Acrobat Reader. (NPR-39909)

### [!DNL Forms] Correctifs {#forms-fixes-6516}

* Lorsque vous utilisez une étape Affecter une tâche** pour envoyer une notification pour une tâche affectée, deux emails sont envoyés au lieu d’un à la personne affectée. (NPR-40078)
* Lorsqu’un utilisateur masque les en-têtes de tableau, la largeur de colonne précédemment définie est désactivée et toutes les colonnes conservent la même largeur. (NPR-40063)
* Si vous modifiez le mot de passe par défaut de l’utilisateur administrateur à partir de `admin`, lors de l’exécution de la fonction `Prepare Adobe Experience Manager Server For DSC deployment` vérifiez le service pack AEM Forms JEE qui échoue. (NPR-40062), (NPR-39387)
* Les API OutputService et AssemblerService ne parviennent pas à convertir le formulaire du PDF en PDF/A. (NPR-39990)
* AssemblerService ne peut pas convertir le PDF en PDF/A. Lorsqu’un utilisateur convertit un PDF en PDF/A, l’erreur suivante se produit : `PDFAConformance isCompliant="false" compliance="PDF/A-1b" resultLevel="Summary" ignoreUnusedResources="true" allowCertificationSignatures="true"> <Violation count="6" key="PDFA_CS_001_NOT_DEVICE_INDEPENDENT" description="ColorSpace is not device independent`. (NPR-39956)
* Lorsque la validation côté serveur échoue pour un appel de l’API GuideSubmitServlet, les erreurs ne sont pas renvoyées dans la réponse envoyée au client. (NPR-39925)
* Après la mise à niveau vers AEM 6.5.15.0 Service Pack sur le serveur Windows, l’utilisateur rencontre plusieurs messages d’erreur et le service de messagerie ne fonctionne pas.(NPR-39919)
* Lorsque vous effectuez une mise à niveau vers AEM 6.5.14.0 et que vous utilisez le service importData pour fusionner des PDF avec XML, l’erreur suivante se produit : `Caused by: java.lang.NoSuchMethodError: com.adobe.xfa.form.FormModel.isXFABarcode(Lcom/adobe/xfa/Node;)Ljava/lang/Boolean`.(NPR-39807)
* Lorsque l’utilisateur installe **Document Security Office** , les problèmes suivants se produisent :
   * Microsoft® Excel se bloque fréquemment.
   * Lors de l’ouverture d’un document sécurisé, la variable **Bureau de sécurité des documents** n’est pas détecté comme installé sur une machine. Indique à l’utilisateur de télécharger et d’installer l’extension de sécurité. (NPR-39768)
* Une fois qu’un utilisateur a effectué la mise à niveau vers AEM Service Pack 6.5.15.0, la conversion PostScript vers Pdf ne fonctionne pas. (NPR-39765), (NPR-39764)
* Lorsque l’utilisateur tente d’ouvrir l’écran de la visite après l’ouverture d’un formulaire adaptatif, il échoue avec une exception NullPointer :`[172.17.0.1[1662032923933]GET/libs/fd/af/content/editors/form/tour/content.htmlHTTP/1.1]com.day.cq.wcm.core.impl.WCMDebugFilterException:org.apache.sling.api.scripting.ScriptEvaluationException:”` (NPR-39654)
* Sous Windows, lorsque l’utilisateur active des paramètres noirs à fort contraste, le contenu Forms HTML5 devient flou lors du rendu en tant qu’aperçu de HTML dans le navigateur. (NPR-39018)

## Intégrations {#integrations-6516}

* Supprimez le code de Search &amp; Promote d’Adobe et la dépendance de Experience Manager 6.5. Le Search &amp; Promote d’Adobe a atteint la fin de service en septembre 2022. Voir [Annonce de fin de service d’Adobe Search &amp; Promote](https://experienceleague.adobe.com/docs/discontinued/using/search-promote.html?lang=en). (NPR-39706)

## [!DNL Sites] {#sites-6516}

* Actuel `cq-wcm-core` La version d’artifactory ne comporte pas de POM. (SITES-10983)
* L’action d’aperçu du déploiement ne doit pas répertorier la page à créer. (SITES-10355, CQ-4266213)
* Déployer après la désolidarisation MSM recrée la page détachée. (SITES-9841)
* La création d’un lancement expire ; l’utilisateur doit attendre plusieurs minutes sur un écran de chargement avant que la requête ne soit expirée. (SITES-9051)
* L’interface utilisateur de la page de déploiement affiche les chemins de page parente inexistants. Vous pouvez déployer la page avec un message de réussite, mais la page enfant n’est pas déployée en raison du fait que la page parente n’a jamais été déployée en premier lieu. (SITES-8621)

### [!DNL Sites] - Composants principaux {#sites-core-components-6516}

* Centralisez le traitement des liens sur les pages de courrier électronique afin que les personnalisations des modèles ne soient plus nécessaires. (SITES-9002)

### [!DNL Sites] - Interface utilisateur de l’administrateur {#sites-adminui-6516}

* L’exportation CSV n’exporte pas toutes les pages sous la page sélectionnée. (SITES-9390)

### [!DNL Sites] - [!DNL Content Fragments] {#sites-contentfragments-6516}

* Impossible d’imprimer le fichier JSON d’un fragment de contenu. Cela est dû au fait que la requête GraphQL ne peut pas être générée lorsque vous ouvrez la page Aperçu du fragment de contenu. (SITES-8619)
* Lors de la réouverture de l’éditeur de modèle de fragment de contenu, tous les **[!UICONTROL Date et heure]** par défaut, les champs sont de type Date et heure . (SITES-8401)

### [!DNL Sites] - [!DNL Experience Fragments] {#sites-experiencefragments-6516}

* Vous ne pouvez pas déplacer un fragment d’expérience vers un autre dossier, même si le modèle est répertorié sous les modèles autorisés. (SITES-8601)
* (SITES-7989)


### [!DNL Sites] - Éditeur de page {#sites-pageeditor-6516}

* Mettez à jour les dépendances pour l’amélioration du résolveur de ressources effectuée dans SITES-8464, dans laquelle le rendu des pages en mode création a créé un grand nombre de `TemplatedResourceImpl` objets. (SITES-9350)


## Sling {#sling-6516}

* Experience Manager est bloqué au démarrage. (NPR-39832)
* Lorsque de nombreux chemins de redirection vers un microsite sont présents dans le stockage de la version du Experience Manager, Experience Manager ne démarre pas. (NPR-38955)


## Projets de traduction {#translation-6516}

* Dans `MicrosoftTranslationServiceImpl`, paramètre de chaîne de requête `Category` est incorrect. (NPR-39828)
* La création d’un projet de traduction affiche l’erreur *La ressource de page de Principal n’existe pas*; le projet de traduction n’est pas créé. (NPR-39762)
* Impossible de définir une date d’échéance sur un projet de traduction utilisant un connecteur de traduction humain. (NPR-39593)

## Interface utilisateur {#ui-6516}

* Lorsque vous définissez une résolution plus petite, le sélecteur de date ne s’affiche pas et la sélection matin/après-midi ne s’affiche pas ou ne change visiblement pas. (NPR-39948)
* Lorsque la minimisation de js (minimisation de JavaScript) est utilisée, elle ne traite pas la minimisation en raison d’une erreur d’analyse. (NPR-39650)
* Champ de balise (`/libs/cq/gui/components/coral/common/form/tagfield`) est en conflit avec la chronologie. (CQ-4350751)


## Gestion de contenu web (WCM) {#wcm-6516}

* L’action d’aperçu du déploiement ne doit pas répertorier la page à créer. (CQ-4266213, SITES-10355)

## Workflow {#workflow-6516}

* Suppression manuelle du modèle de workflow modifiable de `/conf` laisse une instance de modèle d’exécution persistante sans modèle modifiable. (CQ-4349365)


## Installer [!DNL Experience Manager] 6.5.16.0 {#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.16.0 nécessite [!DNL Experience Manager] 6.5. Consultez la [documentation de mise à niveau](/help/sites-deploying/upgrade.md) pour des instructions détaillées. <!-- UPDATE FOR EACH NEW RELEASE -->
* Le téléchargement du pack de services est disponible dans la [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) d’Adobe.
* Lors d’un déploiement avec MongoDB et plusieurs instances, installez [!DNL Experience Manager] 6.5.16.0 sur l’une des instances d’auteur à l’aide du gestionnaire de modules.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe ne recommande pas de supprimer ou de désinstaller le module [!DNL Experience Manager] 6.5.16.0. Par conséquent, avant d’installer le module, vous devez créer une sauvegarde du `crx-repository` au cas où vous auriez besoin de le restaurer. <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for AEM Forms, see [AEM Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### Installation du pack de services sur [!DNL Experience Manager] 6.5 {#install-service-pack}

1. Redémarrez l’instance avant l’installation si l’instance est en mode de mise à jour (lorsque l’instance a été mise à jour à partir d’une version antérieure). Adobe recommande un redémarrage si le temps de disponibilité actuel d’une instance est élevé.

1. Avant l’installation, prenez un instantané ou exécutez une sauvegarde récente de votre instance [!DNL Experience Manager].

1. Téléchargez le pack de services à partir de la [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Ouvrez le gestionnaire de modules et cliquez sur **[!UICONTROL Charger le module]** pour charger le module. Pour en savoir plus, consultez la section [Gestionnaire de modules](/help/sites-administering/package-manager.md).

1. Sélectionnez le module, puis sélectionnez **[!UICONTROL Installer]**.

1. Pour mettre à jour le connecteur S3, arrêtez l’instance après l’installation du pack de services, remplacez le connecteur existant par un nouveau fichier binaire fourni dans le dossier d’installation, puis redémarrez l’instance. Consultez la section [Entrepôt de données S3 Amazon](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>La boîte de dialogue de l’interface utilisateur du gestionnaire de packages se ferme parfois pendant l’installation du pack de services. Adobe recommande d’attendre que les journaux d’erreurs se stabilisent avant d’accéder au déploiement. Attendez les logs spécifiques liés à la désinstallation de la mise à jour complète avant de vous assurer que les installations sont réussies. En règle générale, ce problème se produit dans [!DNL Safari] mais peut se produire par intermittence sur n’importe quel navigateur.

**Installation automatique**

Vous pouvez utiliser deux méthodes différentes pour installer automatiquement [!DNL Experience Manager] 6.5.16.0.<!-- UPDATE FOR EACH NEW RELEASE -->

* Placez le package dans le dossier `../crx-quickstart/install` lorsque le serveur est disponible en ligne. Le package est automatiquement installé.
* Utilisez l’[API HTTP à partir du gestionnaire de packages](/help/sites-administering/package-manager.md#package-share). Utilisez `cmd=install&recursive=true` afin que les packages imbriqués soient installés.

>[!NOTE]
>
>Experience Manager 6.5.16.0 ne prend pas en charge l’installation en Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Validation de l’installation**

Pour connaître les plateformes certifiées pour travailler avec cette version, reportez-vous à la section des [exigences techniques](/help/sites-deploying/technical-requirements.md).

1. La page d’informations sur les produits (`/system/console/productinfo`) affiche la chaîne de version mise à jour `Adobe Experience Manager (6.5.16.0)` sous [!UICONTROL Produits installés]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. Tous les lots OSGi sont au statut **[!UICONTROL ACTIF]** ou **[!UICONTROL FRAGMENT]** dans la console OSGi (utilisez la console web : `/system/console/bundles`).

1. Le lot OSGi `org.apache.jackrabbit.oak-core` est de la version 1.22.14 ou ultérieure (utiliser la console Web : `/system/console/bundles`). <!-- NPR-39939 for 6.5.16.0 --> <!-- NPR-39436 for 6.5.15.0 --> <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### Installer le Service Pack pour [!DNL Experience Manager] Forms {#install-aem-forms-add-on-package}

Pour obtenir des instructions sur l’installation du pack de services sur AEM Forms, voir les [instructions d’installation du pack de services AEM Forms](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

### UberJar {#uber-jar}

UberJar pour [!DNL Experience Manager] 6.5.16.0 est disponible dans le [référentiel central Maven](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.15/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

>[!NOTE]
>
>Dans Experience Manager 6.5.16.0, la version d’UberJar (6.5.15.0) reste identique à la version précédente.


Pour utiliser UberJar dans un projet Maven, consultez la section [Utilisation d’UberJar](/help/sites-developing/ht-projects-maven.md) et incluez la dépendance suivante dans le POM de votre projet : <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.15</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar et les autres artefacts associés sont disponibles sur le référentiel central Maven au lieu du référentiel Maven public Adobe (`repo.adobe.com`). Le fichier UberJar principal est renommé `uber-jar-<version>.jar`. Il n’existe donc pas de `classifier` avec `apis` comme valeur pour la balise `dependency`.

## Fonctionnalités obsolètes {#removed-deprecated-features}

Vous trouverez ci-dessous une liste des fonctionnalités signalées comme obsolètes par [!DNL Experience Manager] 6.5.7.0. Ces fonctionnalités sont initialement marquées comme obsolètes et supprimées ultérieurement dans une version future. Une option alternative est fournie.

Vérifiez si vous utilisez une de ces fonctionnalités dans un déploiement. Envisagez également de changer de mise en œuvre et d’utiliser une autre option.

| Domaine | Fonctionnalité | Remplacement |
|---|---|---|
| Intégrations | L’**[!UICONTROL Accord préalable des services cloud AEM]** est obsolète car l’intégration d’[!DNL Experience Manager] et d’[!DNL Adobe Target] est mise à jour dans [!DNL Experience Manager] 6.5. L’intégration prend en charge l’API Adobe Target Standard. L’API utilise l’authentification au moyen d’Adobe IMS et d’[!DNL Adobe I/O Runtime]. Elle prend en charge le rôle croissant d’Adobe Launch pour utiliser les pages [!DNL Experience Manager] à des fins d’analyse et de personnalisation, l’assistant d’accord préalable n’a donc aucune utilité sur le plan fonctionnel. | Configurez des connexions système, l’authentification Adobe IMS et les intégrations d’[!DNL Adobe I/O Runtime] à l’aide des services cloud [!DNL Experience Manager] correspondants. |
| Connecteurs | Adobe JCR Connector for Microsoft® SharePoint 2010 et Microsoft® SharePoint 2013 est obsolète dans [!DNL Experience Manager] 6.5. | S/O |

## Problèmes connus {#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST.
 -->
<!-- REMOVED AS PER CQDOC-20022, JANUARY 23, 2023 * If you install [!DNL Experience Manager] 6.5 Service Pack 10 or a previous service pack on [!DNL Experience Manager] 6.5, the runtime copy of your assets custom workflow model (created in `/var/workflow/models/dam`) is deleted.
To retrieve your runtime copy, Adobe recommends to synchronize the design-time copy of the custom workflow model with its runtime copy using the HTTP API:
`<designModelPath>/jcr:content.generate.json`. -->

* [Fragment de contenu AEM avec le module d’index GraphQL 1.0.5](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fcfm-graphql-index-def-1.0.5.zip)
Ce module est nécessaire pour les client(e)s utilisant GraphQL. Il leur permet d’ajouter la définition d’index requise en fonction des fonctionnalités qu’ils ou elles utilisent réellement.

* Mettez à jour vos requêtes GraphQL qui peuvent avoir utilisé un nom d’API personnalisé pour votre modèle de contenu afin d’utiliser plutôt le nom par défaut du modèle de contenu.

* Une requête GraphQL peut utiliser la variable `damAssetLucene` plutôt que l’index `fragments` index. Il peut en résulter l’échec des requêtes GraphQL ou l’exécution de celles-ci peut prendre beaucoup de temps.

   Pour résoudre le problème, `damAssetLucene` doit être configuré pour inclure les deux propriétés suivantes :

   * `contentFragment`
   * `model`

   Une fois la définition d’index modifiée, une réindexation est requise (`reindex` = `true`).

   Après ces étapes, les requêtes GraphQL doivent être plus rapides.

* [!DNL Microsoft®® Windows Server 2019] ne prend pas en charge [!DNL MySQL 5.7] et [!DNL JBoss®® EAP 7.1], [!DNL Microsoft®® Windows Server 2019] ne prend donc pas en charge les installations clé en main pour [!DNL AEM Forms 6.5.10.0].

* Si vous mettez à niveau votre [!DNL Experience Manager] de 6.5.0 à 6.5.4, jusqu’au dernier Service Pack sur Java™ 11, vous pouvez voir `RRD4JReporter` exceptions dans la variable `error.log` fichier . Pour arrêter les exceptions, redémarrez votre instance de [!DNL Experience Manager]. <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* Les utilisateurs peuvent renommer un dossier dans une hiérarchie dans [!DNL Assets] et publier un dossier imbriqué dans [!DNL Brand Portal]. Toutefois, le titre du dossier n’est pas mis à jour dans [!DNL Brand Portal] jusqu’à ce que le dossier racine soit republié.

* Lorsqu’un utilisateur choisit de configurer un champ pour la première fois dans un formulaire adaptatif, l’option permettant d’enregistrer une configuration ne s’affiche pas dans l’explorateur de propriétés. Sélectionner un autre champ du formulaire adaptatif à configurer dans le même éditeur pour résoudre le problème.

* Les erreurs et messages d’avertissement suivants peuvent s’afficher lors de l’installation d’[!DNL Experience Manager] 6.5.x.x :
   * « Lorsque l’intégration d’Adobe Target est configurée dans [!DNL Experience Manager] à l’aide de l’API Target Standard (authentification IMS), l’exportation de fragments d’expérience vers Target entraîne la création de types d’offres incorrects. » Au lieu du type « Fragment d’expérience » / source « Adobe Experience Manager », Target crée plusieurs offres avec le type « HTML » / source « Adobe Target Classic ».
   * `com.adobe.granite.maintenance.impl.TaskScheduler` : aucune fenêtre de maintenance n’a été trouvée sur granite/operations/maintenance.
   * La validation côté serveur du formulaire adaptatif échoue lorsque des fonctions d’agrégat telles que SUM, MAX et MIN sont utilisées (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Aucune fenêtre de maintenance n’a été trouvée sur granite/operations/maintenance.
   * La zone réactive d’une image interactive de Dynamic Media n’est pas visible lors de la prévisualisation du fichier via la visionneuse de bannières modifiables.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : temporisation en attente de modification d’enregistrement pour terminer la désinscription.

* Lorsque vous tentez de déplacer, de supprimer ou de publier des fragments de contenu ou des sites ou des pages, un problème se produit lorsque les références aux fragments de contenu sont récupérées, car la requête en arrière-plan échoue ; en d’autres termes, la fonctionnalité ne fonctionne pas.
Pour garantir le bon fonctionnement de cette opération, vous devez ajouter les propriétés suivantes au nœud de définition d’index `/oak:index/damAssetLucene` (aucune réindexation n’est requise) :

   ```xml
   "tags": [
       "visualSimilaritySearch"
     ]
   "refresh": true
   ```

* Dans AEM Forms, le protocole POP3 ne fonctionne pas avec les points de fin de courrier électronique pour Microsoft® Office 365.
* Sur la plateforme JBoss® 7.1.4, lorsque l’utilisateur installe AEM Service Pack 6.5.16.0, `adobe-livecycle-jboss.ear` échec du déploiement.

## Lots OSGi et modules de contenu inclus {#osgi-bundles-and-content-packages-included}

Les documents texte suivants répertorient les lots OSGi et les modules de contenu inclus dans [!DNL Experience Manager] 6.5.16.0 : <!-- UPDATE FOR EACH NEW RELEASE -->

* [Liste des lots OSGi inclus dans Experience Manager 6.5.16.0](/help/release-notes/assets/65160_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Liste des modules de contenu inclus dans Experience Manager 6.5.16.0](/help/release-notes/assets/65160_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Sites web à accès limité {#restricted-sites}

Ces sites Web sont disponibles uniquement pour les clients. Si vous êtes client et avez besoin d’un accès, contactez votre responsable de compte Adobe.

* [Téléchargement du produit à l’adresse licensing.adobe.com](https://licensing.adobe.com/)
* [Contacter l’assistance clientèle Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=fr).

>[!MORELIKETHIS]
>
>* Page des produits [[!DNL Experience Manager] ](https://business.adobe.com/fr/products/experience-manager/adobe-experience-manager.html)
>* Documentation [[!DNL Experience Manager]  6.5](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=fr)
>* [Abonnement aux mises à jour prioritaires de produits d’Adobe](https://www.adobe.com/subscription/priority-product-update.html)

