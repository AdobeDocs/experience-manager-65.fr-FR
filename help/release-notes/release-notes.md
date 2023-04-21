---
title: Notes de mise à jour de la version 6.5 d’ [!DNL Adobe Experience Manager]
description: Consultez les informations sur la mise à jour, y compris les nouveautés, la procédure d’installation et une liste complète des modifications pour  [!DNL Adobe Experience Manager]  6.5.
mini-toc-levels: 3
exl-id: fc7d3727-7cd4-47a4-8e75-840f9f9c0e62
source-git-commit: b8c9e5cd3192b51954091b677d700c51617c9460
workflow-type: tm+mt
source-wordcount: '2986'
ht-degree: 85%

---

# Notes de mise à jour du dernier pack de services [!DNL Adobe Experience Manager] 6.5 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/Documents/issue_tracker_sp_cfp_updates.xlsx?d=w3ea81ae4e6054153b132f2698c86f84e&csf=1&web=1&e=WRAZ43&nav=MTVfezk2OTJDQTNFLUI4QTQtNDY2RS05NEVCLUQ5QjcyNEVENkJDNn0 -->

## Informations sur la version {#release-information}

| Produit | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Version | 6.5.16.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Type | Mise à jour du pack de services |
| Date | Jeudi 23 février 2023 <!-- UPDATE FOR EACH NEW RELEASE --> |
| URL de téléchargement | [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?pack[…]be/packages/cq650/servicepack/aem-service-pkg-6.5.16.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## Éléments compris dans [!DNL Experience Manager] 6.5.16.0 {#what-is-included-in-aem-6516}

[!DNL Experience Manager] 6.5.16.0 comprend de nouvelles fonctionnalités, des améliorations importantes demandées par les clients et les clientes, des correctifs ainsi que des améliorations en termes de performances, de stabilité et de sécurité, publiés depuis la version initiale 6.5 en avril 2019. [Installez ce Service Pack](#install) sur [!DNL Experience Manager] 6.5. <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- Some of the key features and improvements are the following:

* _REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

Parmi les améliorations clés apportées à Dynamic Media figure :

Prise en charge du nouveau protocole DASH (Dynamic Adaptive Streaming over HTTP) pour la diffusion en continu à débit adaptatif dans les diffusions vidéo Dynamic Media (avec CMAF, le [format d’application de média commun], activé).

* La diffusion en continu à débit adaptatif (DASH/HLS) garantit une meilleure expérience de visionnage des vidéos aux utilisateurs et utilisatrices finaux.
* Largement adopté dans le secteur, DASH est le protocole standard international pour la diffusion en continu à débit adaptatif de vidéos.
* Disponible désormais en Asie-Pacifique et en Amérique du Nord (qui pourra être activé au moyen d’un ticket de support); Bientôt en Europe, Moyen-Orient, Afrique.

Voir [Activer DASH sur votre compte](/help/assets/video.md#enable-dash).

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## [!DNL Assets] {#assets-6516}

* Ressources connectées : lorsque vous activez les options de recadrage intelligent pour les images sur DAM distant, chargez les images dans un dossier et synchronisez le dossier sur les sites locaux, le dossier ne s’ouvre pas sur le déploiement Sites local. (NPR-39912)
* Lors du tri d’une collection par nom, la vue de liste ne fonctionne pas correctement (ASSETS-19401).
* Lorsqu’un fichier multimédia volumineux (JPEG) est chargé dans les collections, Experience Manager cesse de répondre. (ASSETS-19387)
* Dans l’arborescence de contenu, le nom de la ressource affichée est incorrect, car l’emplacement de la ressource n’est pas rendu correctement. (ASSETS-18870)
* Lors du partage d’une collection à l’aide d’un lien, les données de l’URL ne correspondent pas entre le mélange du mode Carte et du mode Liste. (ASSETS-18758)
* Lorsque vous effectuez une omni-recherche en utilisant un filtre sur le type de dossier, les résultats de la recherche sont incohérents. (ASSETS-18227)
* La propriété `dam:size` n’est pas mise à jour après l’écriture différée XMP, ce qui entraîne le renvoi d’informations incorrectes à partir de l’API `/platform/path/to/asset.jpg;resource=metadata`. (ASSETS-17631)
* Résolveur de ressources non fermé sur toutes les instances d’Experience Manager. (ASSETS-16904)
* Impossible de créer une version d’une ressource même si les autorisations `create` et `modify` vous sont attribuées. (ASSETS-15956)
* Le bouton `move` est désactivé de manière aléatoire lors du déplacement d’une ressource d’un point à un autre. (ASSETS-14889)
* Les lecteurs d’écran ne peuvent pas identifier les en-têtes, car le texte n’est pas défini dans les balises d’en-tête mais comme texte général. (ASSETS-6924)
* Le texte secondaire sous l’image n’est pas obligatoire, mais le texte affiché sous l’image est répétitif avec un attribut `Type`. (ASSETS-6915)


## [!DNL Assets] - [!DNL Dynamic Media] {#dm-6516}

* L’élément de formulaire ne contient pas de libellé. Avec les lecteurs d’écran tels que NVDA et JAWS, les informations sur les libellés de formulaire ne s’annoncent pas correctement. (CQ-4344078)
* Les listes déroulantes ne se ferment pas en appuyant sur la touche `Escape` du clavier. (CQ-4344077)
* L’icône Informations, la lettre « i », qui s’affiche pour la suggestion d’erreur en ligne après la saisie d’une entrée non valide n’est pas accessible à l’aide du clavier. (CQ-4344076)
* `getManifestURI` renvoie la valeur null en raison de la lecture d’une propriété JCR en tant que `toString` au lieu de `getString`. (ASSETS-18674)
* Le composant vidéo de recadrage intelligent ne fonctionne pas correctement. Le composant exécute la lecture au lieu de la diffusion en continu, et les appels VTT échouent, provoquant une erreur 404. (ASSETS-18468)
* La sélection de **[!UICONTROL Propriétés]** sur la page Visionneuse d’une ressource entraîne une exception de pointeur null. (ASSETS-18420)
* L’interface utilisateur [!DNL Experience Manager] change pour la diffusion en continu DASH qui inclut les éléments suivants :
   * un champ CMAF (Common Media Application Format) visible dans l’éditeur de profil vidéo ;
   * un indicateur CMAF envoyé par le processus de chargement vidéo ;
   * les options **[!UICONTROL auto]**, **[!UICONTROL hls]**, et **[!UICONTROL dash]** sont désormais disponibles dans la liste déroulante de lecture dans l’onglet **[!UICONTROL Comportement]** de l’éditeur de paramètres prédéfinis de la visionneuse.
(ASSETS-17428)
* Dans Navigation, lorsque vous sélectionnez **[!UICONTROL Ressources]** > **[!UICONTROL Fichiers]** > **[!UICONTROL Créer]** > **[!UICONTROL Ensemble de carrousels]**, l’icône d’image est chevauchée par la chaîne de texte « Diapositive 1 ». (ASSETS-18578)
* Les ressources non publiées sont à nouveau publiées. (ASSETS-16428)
* L’instance de création d’Experience Manager tombe en panne en raison d’un problème de chargement, ce qui entraîne la création d’une alerte synthétique. (ASSETS-15937)
* Dans la page Paramètres généraux de Dynamic Media, un message d’erreur non traduit `Failed to fetch data` s’affiche. (ASSETS-15617)

## [!DNL Forms] {#forms-6516}

### Fonctions clés [!DNL Forms] {#forms-features-6516}

* Les [formulaires adaptatifs découplés](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html) permettent aux développeurs et développeuses de créer, publier et gérer des formulaires interactifs accessibles et interactifs via des API, plutôt que par le biais d’une interface utilisateur graphique classique.

* Les [composants principaux des formulaires adaptatifs](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=fr#features) sont un ensemble de 24 composants open source compatibles avec BEM qui sont conçus sur la base des composants principaux de la gestion de contenu web d’Adobe Experience Manager. Ces composants sont en open source et fournissent aux développeurs et développeuses la possibilité de les personnaliser et les étendre facilement pour répondre aux besoins spécifiques de leur entreprise. Toute personne disposant de compétences pour personnaliser les [composants principaux de gestion de contenu web](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/authoring.html?lang=fr) peut facilement personnaliser et mettre en forme ces composants.

* Le service Reader Extensions sur OSGi fournit désormais des options distinctes permettant d’importer et d’exporter des droits d’utilisation sur un PDF afin d’importer ou d’exporter des données dans Adobe Acrobat Reader. (NPR-39909)

### Correctifs [!DNL Forms] {#forms-fixes-6516}

* Lors de l’utilisation d’une **Affecter une tâche** pour envoyer une notification pour une tâche affectée, deux emails sont envoyés au lieu d’un à la personne affectée. (NPR-40078)
* Lorsqu’un utilisateur ou une utilisatrice masque les en-têtes de tableau, la largeur de colonne précédemment définie est désactivée et toutes les colonnes conservent la même largeur. (NPR-40063)
* Si vous modifiez le mot de passe par défaut de l’utilisateur administrateur ou de l’utilisatrice administratrice à partir de `admin`, lors de l’exécution de la vérification `Prepare Adobe Experience Manager Server For DSC deployment` sur l’AEM Forms JEE Service Pack, l’opération échoue. (NPR-40062), (NPR-39387)
* Les API OutputService et AssemblerService ne parviennent pas à convertir le formulaire PDF en PDF/A. (NPR-39990)
* AssemblerService ne peut pas convertir le PDF en PDF/A. Lorsqu’un utilisateur ou une utilisatrice convertit un PDF en PDF/A, l’erreur suivante se produit : `PDFAConformance isCompliant="false" compliance="PDF/A-1b" resultLevel="Summary" ignoreUnusedResources="true" allowCertificationSignatures="true"> <Violation count="6" key="PDFA_CS_001_NOT_DEVICE_INDEPENDENT" description="ColorSpace is not device independent`. (NPR-39956)
* Lorsque la validation côté serveur échoue pour un appel de l’API GuideSubmitServlet, les erreurs ne sont pas renvoyées dans la réponse envoyée au client ou à la cliente. (NPR-39925)
* Après la mise à niveau vers l’AEM 6.5.15.0 Service Pack sur le serveur Windows, l’utilisateur ou l’utilisatrice rencontre plusieurs messages d’erreur et le service de messagerie ne fonctionne pas.(NPR-39919)
* Lorsque vous effectuez une mise à niveau vers AEM 6.5.14.0 et que vous utilisez le service importData pour fusionner des PDF avec XML, l’erreur suivante se produit : `Caused by: java.lang.NoSuchMethodError: com.adobe.xfa.form.FormModel.isXFABarcode(Lcom/adobe/xfa/Node;)Ljava/lang/Boolean`.(NPR-39807)
* Lorsque l’utilisateur ou l’utilisatrice installe l’extension **Document Security Office**, les problèmes suivants se produisent :
   * Microsoft® Excel plante fréquemment.
   * Lors de l’ouverture d’un document sécurisé, l’extension **Document Security Office** n’est pas détectée comme installée sur une machine. Indique à l’utilisateur ou à l’utilisatrice de télécharger et d’installer l’extension de sécurité. (NPR-39768)
* Une fois qu’un utilisateur ou une utilisatrice a effectué la mise à niveau vers l’AEM 6.5.15.0 Service Pack, la conversion PostScript vers PDF ne fonctionne pas. (NPR-39765), (NPR-39764)
* Lorsque l’utilisateur ou une utilisatrice tente d’ouvrir l’écran de la visite après l’ouverture d’un formulaire adaptatif, l’opération échoue avec une exception de pointeur Null :`[172.17.0.1[1662032923933]GET/libs/fd/af/content/editors/form/tour/content.htmlHTTP/1.1]com.day.cq.wcm.core.impl.WCMDebugFilterException:org.apache.sling.api.scripting.ScriptEvaluationException:"`(NPR-39654)
* Sous Windows, lorsque l’utilisateur ou l’utilisatrice active des paramètres Noir à contraste élevé, le contenu de formulaires HTML5 devient flou lors du rendu en tant qu’aperçu HTML dans le navigateur. (NPR-39018)
* Lorsque l’utilisateur tente d’ajouter des métadonnées, le bouton Enregistrer devient non fonctionnel pour les composants Drafts and Submissions.(CQ-4349601)
* Après la mise à niveau vers AEM Service Pack 6.5.15.0, la redirection des URL relatives ne fonctionne plus dans Visual Editor. (NPR-39947)
* Lorsqu’un utilisateur effectue une mise à niveau vers AEM Service Pack 6.5.15.0, la redirection cesse de fonctionner avec Internet Explorer. (CQ-4351745)
* Une fois qu’un utilisateur a effectué la mise à niveau vers AEM Service Pack 6.5.15.0, la balise d’en-tête de HTML n’est pas reconnue. Le code de HTML de la balise d’en-tête s’affiche sous forme de texte dans le formulaire de HTML. (NPR-39915)
* Lorsque l’utilisateur tente d’envoyer un formulaire adaptatif, une erreur de type se produit : `ERROR [10.207.64.167 [1668589530607] POST /app/LS4/content/forms/af/revalidate/jcr:content/guideContainer.af.submit.jsp HTTP/1.1]`( NPR-39809)
* Lorsqu’un utilisateur prévisualise un document d’enregistrement à l’aide de la fonction **Envoyer un courrier électronique** action d’envoi, elle ne s’affiche pas correctement. Le modèle de courrier est incorporé dans l’aperçu du document d’enregistrement. (CQ-4352155)
* Lorsqu’un utilisateur prévisualise un formulaire adaptatif en tant que HTML sur le navigateur Microsoft Edge avec le mode de compatibilité IE, il ne s’affiche pas correctement.(CQ-4352216)
* Le dictionnaire doit inclure de nouveaux paramètres régionaux avec des caractères spéciaux, tels que des traits de soulignement ou des tirets, pour permettre la traduction. (NPR-40088)

Après avoir installé le Service Pack du module complémentaire Forms AEM 6.5.16.0, les clients étaient confrontés aux problèmes répertoriés ci-dessous. Par conséquent, une version mise à jour de [AEM 6.5.16.0 Service Pack du module complémentaire Forms - 6.0.914](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr) est publiée. Adobe recommande d’utiliser le Service Pack mis à jour :
* Lorsqu’un utilisateur tente de créer un formulaire adaptatif avec un utilisateur dans le groupe forms-users, l’option de sélection de modèle n’est pas présente et l’erreur similaire à celle-ci se produit : Erreur interne du serveur : java.lang.NullPointerException à com.adobe.aem.formsndocuments.servlet.ThemeClientLibraryDataSourceServlet.lambda$getThemeClientLibCategoryList$3(ThemeClientLibraryDataSourceServlet.java:76) à java.base/java.util.stream.ReferencePipeline$2$1.accept(ReferencePipeline.java:176) at java.base/java.util.Iterator.foreachRemaining(Iterator.java:133) (FORMS-7629)
* Les modifications apportées aux règles de l’éditeur de code ne sont pas enregistrées.(FORMS-7532)

## Intégrations {#integrations-6516}

* Supprimez le code et la dépendance Adobe Search&amp;Promote d’Experience Manager 6.5. La fin du service Adobe Search&amp;Promote a eu lieu en septembre 2022. Voir l’[annonce de fin de service d’Adobe Search&amp;Promote](https://experienceleague.adobe.com/docs/discontinued/using/search-promote.html?lang=fr). (NPR-39706)

## [!DNL Sites] {#sites-6516}

* La version artifactory actuelle `cq-wcm-core` ne comporte pas de POM. (SITES-10983)
* L’action d’aperçu du déploiement ne doit pas répertorier la page à créer. (SITES-10355, CQ-4266213)
* Le déploiement après le détachement MSM recrée la page détachée. (SITES-9841)
* La création d’un lancement expire. L’utilisateur ou l’utilisatrice doit attendre plusieurs minutes sur un écran de chargement avant que la requête n’expire. (SITES-9051)
* L’interface utilisateur de la page de déploiement affiche des chemins de page parente inexistants. Vous pouvez déployer la page avec un message de réussite, mais la page enfant n’est pas déployée, car la page parente n’a jamais été déployée en premier lieu. (SITES-8621)

### [!DNL Sites] - Composants principaux {#sites-core-components-6516}

* Centralisez le traitement des liens sur les pages d’e-mail afin que les personnalisations des modèles ne soient plus nécessaires. (SITES-9002)

### [!DNL Sites] - Interface utilisateur d’administration {#sites-adminui-6516}

* L’exportation CSV n’exporte pas toutes les pages sous la page sélectionnée. (SITES-9390)

### [!DNL Sites] - [!DNL Content Fragments] {#sites-contentfragments-6516}

* Impossible d’imprimer le fichier JSON d’un fragment de contenu. Cela est dû au fait que la requête GraphQL ne peut pas être générée lorsque vous ouvrez la page Aperçu du fragment de contenu. (SITES-8619)
* Lors de la réouverture de l’éditeur de modèle de fragment de contenu, tous les champs **[!UICONTROL Date et heure]** sont de type Date et heure par défaut. (SITES-8401)

### [!DNL Sites] - [!DNL Experience Fragments] {#sites-experiencefragments-6516}

* Vous ne pouvez pas déplacer un fragment d’expérience vers un autre dossier, même si le modèle est répertorié sous les modèles autorisés. (SITES-8601)
* (SITES-7989)


### [!DNL Sites] - Éditeur de page {#sites-pageeditor-6516}

* Mettez à jour les dépendances pour l’amélioration du résolveur de ressources apportée dans SITES-8464, où le rendu des pages en mode création a créé un grand nombre d’objets `TemplatedResourceImpl`. (SITES-9350)


## Sling {#sling-6516}

* Experience Manager est bloqué au démarrage. (NPR-39832)
* Lorsque de nombreux chemins de redirection sont présents dans le stockage de la version d’Experience Manager, ce dernier ne démarre pas. (NPR-38955)


## Projets de traduction {#translation-6516}

* Dans `MicrosoftTranslationServiceImpl`, le paramètre de chaîne de requête `Category` est incorrect. (NPR-39828)
* La création d’un projet de traduction affiche l’erreur *La ressource de gabarit de page n’existe pas*. Le projet de traduction n’est pas créé. (NPR-39762)
* Impossible de définir une date d’échéance sur un projet de traduction utilisant un connecteur de traduction humaine. (NPR-39593)

## Interface utilisateur {#ui-6516}

* Lorsque vous définissez une résolution plus petite, le sélecteur de date ne s’affiche pas et la sélection matin/après-midi ne s’affiche pas ou ne change visiblement pas. (NPR-39948)
* Lorsque la minimisation JavaScript est utilisée, elle ne traite pas la minimisation en raison d’une erreur d’analyse. (NPR-39650)
* Le champ de balise (`/libs/cq/gui/components/coral/common/form/tagfield`) est en conflit avec la chronologie. (CQ-4350751)


## Gestion de contenu web (WCM) {#wcm-6516}

* L’action d’aperçu du déploiement ne doit pas répertorier la page à créer. (CQ-4266213, SITES-10355)

## Workflow {#workflow-6516}

* La suppression manuelle du modèle de workflow modifiable de `/conf` laisse une instance de modèle d’exécution persistante sans modèle modifiable. (CQ-4349365)


## Installer [!DNL Experience Manager] 6.5.16.0 {#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.16.0 nécessite [!DNL Experience Manager] 6.5. Consultez la [documentation de mise à niveau](/help/sites-deploying/upgrade.md) pour des instructions détaillées. <!-- UPDATE FOR EACH NEW RELEASE -->
* Le téléchargement du Service Pack est disponible dans la [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) d’Adobe.
* Lors d’un déploiement avec MongoDB et plusieurs instances, installez [!DNL Experience Manager] 6.5.16.0 sur l’une des instances de création à l’aide du gestionnaire de modules.<!-- UPDATE FOR EACH NEW RELEASE -->

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

1. Le bundle OSGi `org.apache.jackrabbit.oak-core` est de la version 1.22.14 ou ultérieure (utiliser la console Web : `/system/console/bundles`). <!-- NPR-39939 for 6.5.16.0 --> <!-- NPR-39436 for 6.5.15.0 --> <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### Installer le Service Pack sur [!DNL Experience Manager] Forms {#install-aem-forms-add-on-package}

Pour obtenir des instructions sur l’installation du pack de services sur AEM Forms, voir les [instructions d’installation du pack de services AEM Forms](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

### Installation du package d’index GraphQL pour les fragments de contenu Experience Manager {#install-aem-graphql-index-add-on-package}

Les clients qui utilisent GraphQL doivent installer le [AEM de fragment de contenu avec le package d’index GraphQL 1.0.5](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fcfm-graphql-index-def-1.0.5.zip).

Cela vous permet d’ajouter la définition d’index requise en fonction des fonctionnalités qu’ils utilisent réellement.

L’échec de l’installation de ce package peut entraîner des requêtes GraphQL lentes ou en échec.

>[!NOTE]
>
>Ce package ne doit être installé qu&#39;une seule fois par instance ; il n’est pas nécessaire de le réinstaller avec chaque Service Pack.

### UberJar {#uber-jar}

UberJar pour [!DNL Experience Manager] 6.5.16.0 est disponible dans le [référentiel central Maven](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.15/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

>[!NOTE]
>
>Dans Experience Manager 6.5.16.0, la version d’UberJar (6.5.15.0) reste identique à la version précédente.


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

* Mettez à jour vos requêtes GraphQL qui peuvent avoir utilisé un nom d’API personnalisé pour votre modèle de contenu afin d’utiliser plutôt le nom par défaut du modèle de contenu.

* Une requête GraphQL peut utiliser la variable `damAssetLucene` plutôt que l’index `fragments` index. Il peut en résulter l’échec des requêtes GraphQL ou l’exécution de celles-ci peut prendre beaucoup de temps.

   Pour résoudre le problème, `damAssetLucene` doit être configuré pour inclure les deux propriétés suivantes :

   * `contentFragment`
   * `model`

   Une fois la définition d’index modifiée, une réindexation est requise (`reindex` = `true`).

   Après ces étapes, les requêtes GraphQL doivent être plus rapides.

* [!DNL Microsoft®® Windows Server 2019] ne prend pas en charge [!DNL MySQL 5.7] et [!DNL JBoss®® EAP 7.1], [!DNL Microsoft®® Windows Server 2019] ne prend donc pas en charge les installations clé en main pour [!DNL AEM Forms 6.5.10.0].

* Si vous mettez à niveau votre instance [!DNL Experience Manager] de 6.5.0 à 6.5.4, jusqu’au dernier Service Pack sur Java™ 11, les exceptions `RRD4JReporter` s’affichent dans le fichier `error.log`. Pour arrêter les exceptions, redémarrez votre instance d’[!DNL Experience Manager]. <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

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

* Dans AEM Forms, le protocole POP3 ne fonctionne pas avec les points d’entrée d’e-mail pour Microsoft® Office 365.
* Sur la plateforme JBoss® 7.1.4, lorsque l’utilisateur ou l’utilisatrice installe le Service Pack AEM 6.5.16.0, le déploiement de `adobe-livecycle-jboss.ear` échoue.

## Bundles OSGi et modules de contenu inclus {#osgi-bundles-and-content-packages-included}

Les documents texte suivants répertorient les bundles OSGi et les modules de contenu inclus dans [!DNL Experience Manager] 6.5.16.0 : <!-- UPDATE FOR EACH NEW RELEASE -->

* [Liste des bundles OSGi inclus dans Experience Manager 6.5.16.0](/help/release-notes/assets/65160_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
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

