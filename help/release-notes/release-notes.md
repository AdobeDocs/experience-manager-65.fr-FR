---
title: Notes de mise à jour de la version 6.5 d’ [!DNL Adobe Experience Manager]
description: Consultez les informations sur la mise à jour, y compris les nouveautés, la procédure d’installation et une liste complète des modifications pour [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 4
exl-id: a52311b9-ed7a-432e-8f35-d045c0d8ea4c
source-git-commit: 7f150219bce3036c0e330b7349e679fdf19797d1
workflow-type: tm+mt
source-wordcount: '3688'
ht-degree: 65%

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
| Date | Jeudi 22 février 2024 <!-- UPDATE FOR EACH NEW RELEASE --> |
| URL de téléchargement | [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.20.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## Éléments compris dans [!DNL Experience Manager] 6.5.20.0 {#what-is-included-in-aem-6520}

[!DNL Experience Manager] 6.5.20.0 comprend de nouvelles fonctionnalités, des améliorations importantes demandées par les clientes et les clients, des correctifs de bugs ainsi que des améliorations en termes de performances, de stabilité et de sécurité, publiés depuis la version initiale 6.5 en avril 2019. [Installez ce pack de services](#install) dans [!DNL Experience Manager] 6.5.

<!-- UPDATE FOR EACH NEW RELEASE -->

## Principales fonctionnalités et améliorations

<!-- * _6.5.20.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

Voici quelques-unes des fonctionnalités et améliorations clés de cette version :

* Dynamic Media prend désormais en charge le format d’image HEIC sans perte pour les systèmes iOS et iPadOS d’Apple. Consultez également la section [fmt](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-is-http-fmt.html?lang=fr) dans l’API de diffusion et de rendu d’images Dynamic Media.

* Le gestionnaire de sites multiples (MSM) prend désormais en charge les structures de fragments d’expérience, y compris les dossiers et les sous-dossiers, pour un déploiement en masse efficace des fragments d’expérience sur des Live Copies.

### [!DNL Forms]

* **Reporting de transactions dans AEM Forms on JEE**: la fonctionnalité de création de rapports sur les transactions a été introduite pour AEM Forms on JEE, ce qui permet l’enregistrement complet des transactions de document telles que les conversions, les rendus et les envois. Cette amélioration améliore l’efficacité et facilite la conservation des données. La fonction est désactivée par défaut. Vous pouvez l’activer à partir de l’interface utilisateur d’administration.
* **Sécurité renforcée avec prise en charge d’ECDSA**: AEM Forms offre désormais une prise en charge robuste de l’algorithme de signature numérique (ECDSA) elliptic Curve pour les piles JEE et OSGi. Les utilisateurs peuvent désormais signer, certifier et vérifier des documents de PDF avec une sécurité renforcée. Les algorithmes de courbe EC pris en charge incluent :
   * Courbe elliptique ECDSA P256 avec algorithme de condensé SHA256
   * Courbe elliptique ECDSA P384 avec algorithme de condensé SHA384
   * Courbe elliptique ECDSA P512 avec algorithme de condensé SHA512
* **Compatibilité transparente avec Windows 11 pour Forms Designer**: AEM Forms Designer prend désormais en charge Windows 11, ce qui facilite l’installation et le fonctionnement. Les utilisateurs peuvent effectuer une mise à niveau en toute confiance vers Windows 11 sans avoir à réinstaller Forms Designer ou se soucier des problèmes de compatibilité, ce qui garantit un workflow ininterrompu.
* **Amélioration de l’accessibilité avec le rôle &quot;légende&quot; personnalisé dans AEM Forms Designer**: AEM Forms Designer inclut désormais un rôle d’accessibilité personnalisé appelé &quot;Légende&quot;, qui permet aux utilisateurs de créer des fichiers XDP avec des éléments de sous-titrage personnalisés. Cette fonctionnalité améliore l’accessibilité en permettant aux utilisateurs d’intégrer des sous-titres personnalisés dans leurs conceptions de document afin qu’ils puissent améliorer l’inclusion et l’expérience utilisateur.

<!-- ### [!DNL Forms]

* text -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## Problèmes corrigés dans le pack de services 20 {#fixed-issues}

### [!DNL Sites]{#sites-6520}

<!--#### Accessibility{#sites-accessibility-6520}

* text -->

#### Interface utilisateur d’administration{#sites-adminui-6520}

* Le champ `Workflow Title` est marqué par `*` selon les besoins, mais il n’y a aucune validation. (SITES-16491)

<!--#### Classic UI{#sites-classicui-6520}

* text -->

#### [!DNL Content Fragments]{#sites-contentfragments-6520}

* Les dossiers de configuration imbriqués n’étaient plus pris en charge et les dossiers de modèles de fragments de contenu n’étaient plus visibles après la mise à niveau vers AEM 6.5.18 ou vers AEM 6.5.19. (SITES-18110)
* Certains sous-dossiers ne peuvent pas effectuer de sélection à partir des modèles de fragment de contenu hérités. Les dossiers doivent être pris en charge sans avoir de propriété `jcr:content`, même si les dossiers DAM créés par le biais de l’interface utilisateur ont un tel nœud. (SITES-17943)

#### [!DNL Content Fragments] - API GraphQL {#sites-graphql-api-6520}

<!-- REMOVED AS PER EMAIL FROM SAMEER DHAWAN FEBRUARY 19, 2024 * When upgrading AEM from 6.5.19.0 to 6.5.20.0, the path `/libs/cq/graphql/sites/graphiql` was getting deleted. (SITES-19530) CRITICAL -->
* Lors de l’exécution d’une requête GraphQL pour [filtrer les résultats](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#filtering) à l’aide de variables facultatives, si une valeur spécifique n’est **pas** fournie pour la variable facultative, la variable est alors ignorée dans l’évaluation du filtre. (SITES-17051)

<!--#### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6520}

* text -->

#### [!DNL Content Fragments] - API REST{#sites-restapi-6520}

* Avec la mise à niveau de la bibliothèque `org.json`, il y a eu un changement dans la désérialisation des nombres décimaux. Auparavant, ils étaient convertis « par défaut » selon la classe Double, et maintenant selon la classe BigDecimal. Au lieu de cela, les valeurs de propriété de métadonnées, stockées par le biais de l’API REST, doivent être converties selon le type Double à partir de la classe BigDecimal. (SITES-16857)

#### Back-end principal{#sites-core-backend-6520}

* Lorsque la publication rapide d’un fragment de contenu est utilisée, le chargement se poursuit et la publication n’est pas effectuée. En d’autres termes, la publication rapide ne fonctionne pas pour les fragments de contenu après une mise à niveau de pack de services d’AEM 6.5.7 vers AEM 6.5.17. Lorsque l’utilisateur ou l’utilisatrice a essayé la publication gérée, cela a fonctionné. Cependant, lorsque la publication rapide a été essayée, la publication n’était pas effectuée. Plus précisément, `com.day.cq.wcm.core.impl.reference.ActivationReferenceSearchBuilder` a provoqué le blocage du système. (SITES-17311)
* Les fragments de contenu ne peuvent pas être sérialisés avec l’exporteur Jackson : le chargement de la page est interrompu lorsqu’un fragment de contenu est référencé dans une page (utilise le code de l’exporteur Jackson) et que toute balise est ajoutée à un fragment de contenu. (SITES-18096)

#### Composants principaux{#sites-core-components-6520}

* L’installation du package de composants principaux CIF sur AEM entraîne une modification de la valeur `:type` des composants existants. La modification signifie leur rendu n’est plus effectué sur les pages auxquelles ils ont été ajoutés. (SITES-17601)

#### Intégration de campagne{#sites-campaign-integration-6520}

* AEM utilisait une liste autorisée, également appelée `whitelist`, en raison d’un rapport de vulnérabilité. La liste autorisée empêchait les clientes et les clients d’utiliser les fonctionnalités nécessaires. (SITES-16822)

#### Fragments d’expérience{#sites-experiencefragments-6520}

* MSM pour les fragments d’expérience prend désormais en charge le déploiement en masse vers les structures de contenu des fragments d’expérience, y compris les dossiers et les sous-dossiers. (SITES-16004)

<!--#### Foundation Components (Legacy){#sites-foundation-components-legacy-6520}

* text

#### Launches{#sites-launches-6520}

* text -->

#### MSM - Live Copies{#sites-msm-live-copies-6520}

* Une exception « `Is not modifiable` » est générée lors du déploiement du composant. Plus précisément, une exception `org.apache.sling.servlets.post.impl.operations.ModifyOperation` survient lors du traitement de la réponse. (SITES-18809)
* Impossible de déployer les modifications sur des Live Copies spécifiques des fragments d’expérience. (SITES-17930)
* Lorsqu’un utilisateur ou une utilisatrice ajoute une annotation à un composant sur une page de plan directeur, puis la déploie, le nombre d’annotations sur la Live Copy s’affiche incorrectement. (SITES-17099)
* Le bouton de déploiement de MSM d’une page parente à une page enfant ne fonctionne pas dans l’interface utilisateur graphique tactile. Lorsque cette option est sélectionnée, l’erreur suivante s’affiche : `Uncaught TypeError: _g.shared is undefined`. (SITES-16991)

#### Éditeur de page{#sites-pageeditor-6520}

* L’aperçu de l’éditeur de thèmes Forms ne fonctionne pas. Lorsque l’option Aperçu est sélectionnée, seule une icône de chargement est visible. (SITES-17164)

### [!DNL Assets]{#assets-6520}

* Impossible de valider les champs basés sur des règles dans l’assistant de l’éditeur de métadonnées et affichage d’un message d’erreur « Champs obligatoires manquants ». (ASSETS-31396)
* Une fois qu’un PDF est déplacé vers un autre emplacement, l’option **[!UICONTROL Afficher la page]** disparaît. (ASSETS-30538)
* Impossible de sélectionner une image avec des autorisations de lecture. (ASSETS-32199)
* Impossible de modifier la taille de la carte dans les paramètres d’affichage. (ASSETS-31667)
* Échec du chargement du type de fichier .oft. (ASSETS-30109)
* Lorsque vous essayez d’ajouter un champ de métadonnées personnalisé en tant que colonne supplémentaire au rapport, les cases ne sont pas cochées. (ASSETS-31671)
* L’opération de déplacement de ressources ne fonctionne pas correctement dans le pack de services 16 d’Experience Manager. (ASSETS-30598)

#### [!DNL Dynamic Media]{#assets-dm-6520}

* Une fois qu’une ressource est chargée dans AEM, le workflow `Update_asset` est déclenché. Cependant, le workflow ne se termine jamais. Le workflow se termine uniquement à l’étape de chargement du produit. L’étape suivante est le chargement par lots de Scene7, mais ce processus n’est pas pris en compte dans AEM. (ASSETS-30443)
* Vous avez besoin d’un meilleur moyen de gérer les vidéos autres que Dynamic Media dans le composant Dynamic Media. Ce problème donnait une exception qui instanciait `dynamicmedia_sly.js`. (ASSETS-31301)
* L’aperçu fonctionne pour toutes les ressources, les visionneuses de vidéos adaptatives et les vidéos. Cependant, il renvoie une erreur 403 pour les fichiers `.m3u8` (qui, d’ailleurs, fonctionnent toujours par des liens publics). (ASSETS-31882)
* Correction du statut `scene7SmartCropProcessingStatus`. Les métadonnées vidéo de recadrage intelligent indiquaient un échec même en cas de réussite. (ASSETS-31255)

### [!DNL Forms]{#forms-6520}

<!--Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the AEM 6.5.20.0 Forms add-on package release is scheduled for Thursday, February 29, 2024. A list of Forms fixes and enhancements is added to this section post the release.-->

#### [!DNL Adaptive Forms]

* Lorsqu’un utilisateur tente d’intégrer AEM Forms à une plateforme de messagerie avec une URL publiée AEM, AEM Forms n’ajoute pas `method=post` lors du rendu de la page. Ce problème se produit même si `POST` est défini dans l’action d’envoi avec l’URL. Cela fait que la plateforme de messagerie ne reconnaît pas cela comme un formulaire. (FORMS-12614)
* Lorsqu’un utilisateur sélectionne le champ de date avec un modèle d’affichage dans AEM Form Service Pack 6.5.18.0, il ne peut pas sélectionner la date courante à l’aide du clavier. (FORMS-12736)
* Dans AEM Forms Service Pack 6.5.17.0 et Service Pack 6.5.18.0, lorsqu’un utilisateur bascule entre les mois dans le widget Calendrier, le composant Sélecteur de date affiche une ligne supplémentaire. (FORMS-11869)
* Lorsqu’un utilisateur clique sur une image à l’aide du composant &quot;Prendre une photo&quot; dans le composant Pièce jointe d’un appareil iOS, toutes les images sont ajoutées au dossier portant le même nom. (FORMS-12224)
* Lorsqu’un utilisateur met à jour une option existante dans un groupe de boutons radio, des valeurs de traduction incorrectes sont publiées. (FORMS-12575)
* Lorsqu’un utilisateur ajoute des caractères à un formulaire adaptatif sur un appareil Android™, il peut saisir plus de caractères que le nombre maximal de caractères défini dans le champ Texte sur les appareils Android™. Cependant, il fonctionne lorsqu’un utilisateur sélectionne le type d’entrée HTML5. (FORMS-12748)
* En raison des étiquettes Arial® et Arial® correspondantes, les lecteurs d’écran ne sont pas en mesure de faire la distinction entre ces deux étiquettes. Pour résoudre ce problème, l’étiquette &quot;aria-label-by&quot; est remplacée par &quot;aria-description-by&quot; pour les champs de formulaire. (FORMS-12436)
* Lorsqu’un auteur utilise le composant &quot;Forms adaptatif - Incorporer (v2)&quot; pour incorporer un formulaire adaptatif dans sa page de sites et que le formulaire incorporé contient un composant CAPTCHA (Service CAPTCHA -> reCAPTCHA, Paramètres -> reCAPTCHA-v2), la page du site n’est pas rendue lorsque l’utilisateur tente d’afficher la page du site à l’aide de l’option &quot;Afficher comme publié&quot; sur l’auteur. instance. L’erreur suivante s’affiche comme suit (FORMS-11859) :
  `Failed to construct 'URL': Invalid base URL at Object.renderRecaptcha`

* Lorsqu’un utilisateur tente de sélectionner la date à l’aide du composant de sélecteur de date, la valeur n’est pas mise à jour et affiche la valeur NULL. (FORMS-12742, FORMS-12736)

* Lorsqu’un utilisateur effectue la mise à niveau vers AEM Service Pack 6.5.19.0, après la mise à jour d’une nouvelle langue vers le dictionnaire existant, il n’est pas fusionné avec les lignes &quot;guideContainer&quot; pour ajouter un paramètre régional à un formulaire. (FORMS-12947)

* Sur AEM Forms Service Pack 6.5.19.0, l’opération webservice appelée sur Java™ 11 échoue avec l’erreur (FORMS-12329) :
  `java.lang.NoClassDefFoundError message:sun/misc/BASE64Decoder`

* Lorsqu’un utilisateur appelle l’opération &quot;receive&quot; pour &quot;EmailService&quot; sur AEM Forms Service Pack 6.5.18.0, une exception est générée (FORMS-12050) :
  `java.util.ServiceConfigurationError: javax.mail.Provider: Provider com.sun.mail.imap.IMAPProvider not a subtype`

* Lorsque le mode FIPS est activé sur AEM Forms Service Pack 6.5.18.0, la création d’un utilisateur sous le DOM par défaut échoue avec l’erreur (FORMS-11857) :
  `com.adobe.idp.cx.a: error seeding random number generator`

* Lorsqu’un utilisateur sélectionne des polices dans ADMINUI sous le chemin d’accès `Home>Services>PDF Generator>Adobe PDF Settings`, elle n’est pas sélectionnée. De plus, dans un profil standard ou personnalisé, la zone de liste des polices disponibles est vide. Il n’est donc pas possible de personnaliser la sous-liste de **Toujours incorporer** ou **Ne jamais incorporer**. L’utilisateur ne peut pas configurer la police de ses PDF avec PDF Generator. Les journaux n’affichent aucun message d’erreur pertinent. (FORMS-12095)

* Dans AEM Forms Service Pack 6.5.18.0, l’utilisateur ne peut pas créer de paramètres de sécurité, il ne voit aucune erreur ni journal du serveur, mais un message d’erreur contextuel s’affiche à l’écran. (FORMS-12212)

* Lorsqu’un utilisateur du Service Pack AEM Forms 6.5.18.0 envoie un formulaire adaptatif dans le processus JEE, la pièce jointe du formulaire adaptatif n’est pas envoyée au processus JEE, ce qui entraîne l’échec de l’application. (FORMS-12232, FORMS-12228)

* Lorsqu’un utilisateur convertit un PDF en PDF/A-2b ou PDF/A-3B, il ne parvient pas à le convertir, l’erreur s’affiche comme suit : (FORMS-12790)

  ```
  OCCD contains Order key that does not reference all layers.
  -> Optional content configuration dictionary has no Name entry.
  -> Font not embedded (and text rendering mode not 3).
  obj(65, 0)
  Page: 1
  -> Font not embedded (and text rendering mode not 3).
  obj(67, 0)
  Page: 1
  -> PDF/A entry missing. 
  -> PDF/A entry missing.
  ```

* Dans AEM Forms 6.5.18.0, lorsqu’un formulaire adaptatif est publié, toutes ses dépendances, y compris les stratégies, sont republiées, même si aucune modification ne leur a été apportée. (FORMS-10454)

* Lorsqu’un utilisateur sélectionne &quot;Microsoft SharePoint&quot; lors de l’exécution de Configuration Manager sur AEM Forms 6.5.19.1 avec la configuration clé en main de JBoss®, l’installation EAR de LiveCycle JBoss® échoue et affiche l’erreur suivante : (FORMS-12463)

  ` Caused by: org.jboss.as.server.deployment.DeploymentUnitProcessingException: WFLYEE0031: Unable to process modules in application.xml for EAR ["/C:/AEM/jboss/bin/content/ adobe-livecycle-jboss.ear "], module file adobe-connectorformssharepoint-config-ejb.jar not found.`

* Lorsqu’un utilisateur crée un fragment de document à l’aide du modèle de données de formulaire dans AEM Forms Service Pack 6.5.19.0, les noms de variable apparaissent non définis dans le panneau latéral, mais les noms de variable s’affichent lorsqu’ils sont déposés dans le panneau de formulaire ou lorsqu’ils font l’objet d’un clic. (FORMS-13238)


#### [!DNL Forms Designer] {#forms-designer-6520}


* Lorsqu’un utilisateur effectue la mise à niveau vers AEM Forms Service Pack 6.5.18.0, en raison d’une gestion des exceptions manquante, les fichiers XDP transmis par le service de sortie avec l’option de PDF balisé activée échouent. (LC-3921757)

* Lorsqu’un utilisateur génère un PDF à l’aide d’AEM Forms Designer, les niveaux d’en-tête sont balisés dans l’arborescence d’accessibilité avec l’élément graphique, par exemple une zone de rectangle. (LC-3921687)

* Sur AEM Forms Designer installé via Workbench, les informations de version ne sont pas explicites dans la variable `Control Panel/Programs/Programs and Features`. (LC-3921976)

<!--* When a user creates an XDP on AEM Forms Designer, the user is not able to add the custom Caption Tag. (LC-3921246)-->

* Lorsqu’un utilisateur crée un fichier XDP sur AEM Forms Designer, la balise Formulaire de bouton n’est pas imbriquée dans la balise de paragraphe parent (balise p) à la sortie du PDF. (LC-3921719)

* Lorsqu’un utilisateur crée un fichier XDP sur AEM Forms Designer, l’objet d’arrière-plan est également balisé lorsqu’il navigue dans les balises de formulaire à la sortie du PDF. (LC-3921687)

### Foundation {#foundation-6520}

#### Communities {#communities-6520}

* Échec des diagnostics de synchronisation des utilisateurs et des utilisatrices après la configuration de la synchronisation des utilisateurs et des utilisatrices. (NPR-41693)

<!-- #### Content distribution{#foundation-content-distribution-6520}

* text -->

#### Intégrations{#integrations-6520}

* Supprimez tout le code et les dépendances d’Adobe Search&amp;Promote d’AEM 6.5. (NPR-40856)

#### Localisation{#localization-6520}

* L’attribut aria-label « close » n’est pas localisé dans **[!UICONTROL Ressources]** > **[!UICONTROL Fichiers]**, sélectionnez un dossier, puis, sur la barre d’outils, sélectionnez l’onglet **[!UICONTROL Propriétés]** > **[!UICONTROL Autorisations]** > nom de la personne membre. (NPR-41705)
* Une info-bulle est tronquée pour le champ **[!UICONTROL Mot de passe du magasin de clés]** sur la page Configuration SSL pour les paramètres régionaux ENG, FRA, KOR, DEU et PTB. (NPR-41367)

#### Plateforme{#foundation-platform-6520}

* Problème lors de l’intégration de Campaign à AEM provoquée par le servlet /api ne renvoyant pas le modèle correct dans le json href. La raison en était qu’AEM ne recevait pas l’en-tête X-Forward-Proto, ce qui forçait la requête à répondre avec un modèle HTTP au lieu de HTTPS. Par conséquent, la possibilité d’activer et de désactiver la sélection de modèle en fonction d’une configuration OSGI doit être ajoutée. (GRANITE-48454)

#### Sling{#foundation-sling-6520}

* Le lot `org.apache.sling.resourceMerger` 1.4.2 renvoie une exception à partir d’AEM 6.5, pack de services 17 et versions ultérieures. Sling Resource Merger 1.4.4 doit être inclus dans le pack de services 20. (NPR-41630)

#### Traduction{#foundation-translation-6520}

* Suite au déploiement du pack de services 18 d’AEM 6.5, un problème s’est produit avec l’onglet Filtres de l’éditeur de règles de traduction. Lorsqu’un contexte est sélectionné, en cliquant sur Modifier > Enregistrer, un guillemet double en tant que caractère HTML apparaît la prochaine fois que vous ouvrez le même contexte. Essentiellement, les règles de traduction n’étaient pas correctement enregistrées. (NPR-41624)
* Problèmes liés aux traductions de fragments de contenu, où les chaînes traduites sont renvoyées par fournisseur de traduction vers AEM, mais sont bloquées au niveau `/content/projects` et les fragments de contenu ne sont pas mis à jour. (NPR-41516)
* Un message d’erreur s’affiche lors de la création d’une copie de langue. Cela se produit sur une page dont un fragment de contenu est référencé dans une propriété de page, à l’aide de modèles de fragment de contenu. (NPR-41441)
* Les liens dans les fragments d’expérience ne sont pas adaptés à la bonne langue lors de la copie de la langue. Au lieu de cela, le fragment d’expérience pointe vers le paramètre régional principal. (NPR-41343)

#### Interface utilisateur{#foundation-ui-6520}

* Une erreur de console se produit après une mise à niveau vers le pack de services 18 d’AEM 6.5. L’erreur se trouve dans le fichier `coralUI3.js` et cela se produit lorsque vous sélectionnez une liste déroulante dans AEM. Plus précisément, cela se produit avec un événement `onOverlayToggle`. L’erreur `Uncaught TypeError: Cannot read properties of null (reading 'innerText')` s’affiche. (NPR-41467)
* Dans AEM, **[!UICONTROL Outils]** > **[!UICONTROL Général]** > **[!UICONTROL Balisage]** > **[!UICONTROL Créer]** > **[!UICONTROL Créer une balise]**, la saisie de caractères non latins dans le champ **Titre** entraîne le remplissage du champ **Nom** par un trait d’union (`-`). (NPR-41623)
* L’année du copyright est incorrecte dans la la boîte de dialogue `About Adobe Experience Manager`. (NPR-41526)
* Des chaînes des **[!UICONTROL propriétés du profil]** non traduites apparaissent lors de la modification des paramètres de l’utilisateur ou de l’utilisatrice. Se produit pour tous les paramètres régionaux. (NPR-41365)

<!-- #### WCM{#wcm-6520}

* text

#### Workflow{#foundation-workflow-6520}

* text -->

## Installer [!DNL Experience Manager] 6.5.20.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.20.0 nécessite [!DNL Experience Manager] 6.5. Consultez la [documentation de mise à niveau](/help/sites-deploying/upgrade.md) pour des instructions détaillées. <!-- UPDATE FOR EACH NEW RELEASE -->
* Le téléchargement du pack de services est disponible dans la [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.20.0.zip) d’Adobe.
* Lors d’un déploiement avec MongoDB et plusieurs instances, installez [!DNL Experience Manager] 6.5.20.0 sur l’une des instances de création à l’aide du gestionnaire de packages.<!-- UPDATE FOR EACH NEW RELEASE -->

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


### Problèmes connus d’AEM Forms {#known-issues-aem-forms-6520}

* Le service de préremplissage échoue avec une exception de pointeur nulle dans les communications interactives. (CQDOC-21355)
* Le Forms adaptatif vous permet d’utiliser des fonctions personnalisées avec ECMAScript version 5 ou antérieure. Lorsqu’une fonction personnalisée utilise ECMAScript version 6 ou ultérieure, comme les fonctions &quot;let&quot;, &quot;const&quot; ou flèches, l’éditeur de règles peut ne pas s’ouvrir correctement.
* Les utilisateurs ne peuvent pas créer de lettre Correspondence Management. Lorsqu’un utilisateur crée une lettre, une erreur avec la description &quot;Objet d’objet&quot; s’affiche et la lettre n’est pas créée. Les miniatures pour les mises en page ne se chargent pas non plus sur l’écran de création de lettre. Vous pouvez installer le [dernier AEM 6.5 Form Service Pack 20 (6.5.20.0)](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr) pour résoudre le problème. (FORMS-13496)
* Le service de communication interactive crée le document du PDF, mais les données de l’utilisateur ne sont pas automatiquement renseignées dans les champs du formulaire. Le service de préremplissage ne fonctionne pas comme prévu. Vous pouvez installer le [dernier AEM 6.5 Form Service Pack 20 (6.5.20.0)](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr) pour résoudre le problème. (FORMS-13413, FORMS-13493)
* Le chargement de l’éditeur de vérification et de correction (RnC) du service automated forms conversion échoue. Vous pouvez installer le [dernier AEM 6.5 Form Service Pack 20 (6.5.20.0)](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr) pour résoudre le problème. (FORMS-13491)
* Après la mise à jour d’AEM 6.5 Forms Service Pack 18 (6.5.18.0) ou AEM 6.5 Forms Service Pack 19 (6.5.19.0) vers la version 6.5 Forms Service Pack 20 (6.5.20.0), les utilisateurs rencontrent une erreur de compilation JSP. Ils ne peuvent pas ouvrir ni créer de formulaires adaptatifs et ils rencontrent des erreurs avec d’autres interfaces d’AEM telles que l’éditeur de page, l’interface utilisateur d’AEM Forms et l’éditeur de processus d’AEM. Vous pouvez installer le [dernier AEM 6.5 Form Service Pack 20 (6.5.20.0)](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr) pour résoudre le problème. (FORMS-13492)

<!--Customers can install the  latest AEM 6.5 Forms Service Pack to resolve the aforementioned issues.  Here are the direct links for the supported operating systems:
* [AEM 6.5 Forms Service Pack 20 for Apple macOS](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/ADOBE-AEMFD-OSX-PKG-6.0.1192.zip)
* [AEM 6.5 Forms Service Pack 20 for Microsoft Windows](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/ADOBE-AEMFD-WIN-PKG-6.0.1192.zip)
* [AEM 6.5 Forms Service Pack 20 for Linux](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/ADOBE-AEMFD-LINUX-PKG-6.0.1192.zip)
-->

<!--Known issues in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the AEM 6.5.20.0 Forms add-on package release is scheduled for Thursday, February 29, 2024. A list of known issues for forms is added to this section post the release.-->

<!--
#### Install the servlet fragment (AEM Service Pack 6.5.14.0 or earlier)

* If you are upgrading to AEM Service Pack 6.5.15.0 or higher, and your AEM instance is operating on Tomcat 8.5.88, it is mandatory that you install the servlet fragment *before* you proceed with the installation of Service Pack 6.5.15.0 or higher.
* It is mandatory that you install the servlet fragment for all application servers except those running on JBoss&reg; EAP 7.4.0.

**To install the servlet fragment:**

1. Download the servlet fragment from [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar).
1. Start the application server. 
1. Wait for the logs to stabilize and check the bundle state.
1. Open Web Console Bundles. The default URL is `http://[Server]:[Port]/system/console/bundles`.
1. Select **[!UICONTROL Install]** or **[!UICONTROL Update]**. 
1. Select the downloaded fragment 
`org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar` 
1. Select **[!UICONTROL Install]** or **[!UICONTROL Update]**. 
1. Wait for the application server to stabilize.
1. Stop the application server.

-->

## Lots OSGi et packages de contenu inclus{#osgi-bundles-and-content-packages-included}

Les documents texte suivants répertorient les lots OSGi et les packages de contenu inclus dans cette version du pack de services [!DNL Experience Manager] 6.5.

* [Liste des lots OSGi inclus dans Experience Manager 6.5.20.0](/help/release-notes/assets/65200-bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
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
