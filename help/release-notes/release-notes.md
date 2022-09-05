---
title: Notes de mise à jour d’ [!DNL Adobe Experience Manager] 6,5
description: Recherchez des informations de mise à jour, les nouveautés, les procédures d’installation et une liste détaillée de modifications pour [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 3
exl-id: 0288aa12-8d9d-4cec-9a91-7a4194dd280a
source-git-commit: 081b0c70ceca0502cb84d7e1b68b0b12dc45a4e7
workflow-type: tm+mt
source-wordcount: '3237'
ht-degree: 5%

---

# [!DNL Adobe Experience Manager] 6.5 Dernières notes de mise à jour du Service Pack {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession&cid=a915e87c-369a-480c-9daf-d13efc766798 -->

## Informations sur la version {#release-information}

| Produit | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Version | 6.5.14.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Type | Version du Service Pack |
| Date | 25 août 2022 <!-- UPDATE FOR EACH NEW RELEASE --> |
| URL de téléchargement | [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.14.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## Éléments compris dans [!DNL Experience Manager] 6.5.14.0 {#what-is-included-in-aem-6514}

[!DNL Experience Manager] 6.5.14.0 comprend de nouvelles fonctionnalités, des améliorations importantes demandées par les clients, des correctifs de bogues, ainsi que des améliorations des performances, de la stabilité et de la sécurité, publiées depuis la version initiale de 6.5 en avril 2019. [Installer ce Service Pack](#install) on [!DNL Experience Manager] 6.5. <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- Some of the key features and improvements are the following:

* _REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS YOU WANT TO HIGHLIGHT IN THIS RELEASE?_

* Added support for password reset for Dynamic Media Classic users within Experience Manager. (ASSETS-10298) -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## [!DNL Assets] {#assets-6514}

* Impossible d’ajouter ou d’afficher des balises pour les fichiers de PDF. (NPR-38452)
* Lorsque vous configurez les ressources connectées, enregistrez la configuration, rouvrez la page de configuration et testez la configuration déjà enregistrée, le test de la connexion échoue. (NPR-38507)
* Impossible d’ajouter des utilisateurs avec un ID utilisateur numérique aux collections. (NPR-38538)
* Experience Manager ne parvient pas à traiter le FFmpeg installé sur l’instance d’auteur. (NPR-38568)
* Le traitement du PDF échoue avec un `NoClassDefFoundError` message d’erreur. (NPR-38741)
* Le bouton Ajouter sous Colonnes personnalisées ne s’affiche pas correctement lors de la création d’un rapport de ressources pour `de_DE` locale. (ASSETS-10641)
* Lorsque vous chargez une ressource en double dans le référentiel de gestion des ressources numériques et que Experience Manager détecte et fournit une option pour supprimer la ressource en double, la ressource d’origine est également supprimée du référentiel. (ASSETS-10826)
* Experience Manager n’enregistre pas correctement les métadonnées du dossier lorsque vous spécifiez des caractères spéciaux dans plusieurs champs. (ASSETS-10721)
* Impossible d’enregistrer les propriétés de la ressource tant que vous n’avez pas cliqué sur **[!UICONTROL Enregistrer et fermer]** deux fois. (ASSETS-12040)
* Le lecteur d’écran n’affiche que la variable `Relate` bouton . Toutefois, la variable `Relate` contient également un sous-menu et peut être développé et réduit. (ASSETS-6938)
* Attributs ARIA requis (applications Internet enrichies accessibles) `aria-expanded` pour `role="combo box"` est manquante. (ASSETS-6928)
* En mode Carte, dans la zone de navigation du fichier principal, le contenu du texte **[!UICONTROL Tri par]** ne présente pas au moins un rapport de contraste de 4,5:1 par rapport à leur couleur d’arrière-plan. (ASSETS-6926)
* Le Experience Manager n’identifie pas **[!UICONTROL Sélectionner un modèle de workflow]** liste déroulante en tant que champ obligatoire lors de la création d’un modèle de workflow. (ASSETS-6871)

>[!NOTE]
>
>À compter du 1er septembre 2022, les nouveaux clients Experience Manager Assets On-Premise ne pourront plus utiliser les services de contenu dynamique. Aucun impact sur les clients On-Premise et Adobe Managed Services existants qui ont déjà activé cette fonctionnalité.

### [!DNL Dynamic Media] {#dynamic-media-6514}

* Ajout de la prise en charge de la réinitialisation du mot de passe pour l’utilisateur Dynamic Media Classic dans Experience Manager. (ASSETS-10298)
* Les recadrages intelligents générés pour les images avec arrière-plan transparent ont un arrière-plan blanc. (ASSETS-13148)
* Dynamic Media ne génère pas de miniatures pour les fichiers EPS. (ASSETS-10959)
* Les ressources ne sont pas transférées vers le compte Dynamic Media en raison d’un paramètre de chargement manquant. (ASSETS-13165)
* Permet de charger dans Dynamic Media des ressources dont le nom est supérieur à 127 caractères. (ASSETS-9991)
* Activation de JavaScript ES6 (ECMAScript 6) pour les visionneuses Dynamic Media sur Experience Manager 6.5.14.0. (NPR-38393)
* Configuration des options dans Dynamic Media **[!UICONTROL Paramètres généraux]** et **[!UICONTROL Configuration de la publication]** ne doivent pas être accessibles aux utilisateurs qui ne sont pas administrateurs. (ASSETS-8628)
* Dynamic Media **[!UICONTROL Paramètres généraux]** n’affiche pas correctement les paramètres de chargement déjà configurés. (ASSETS-10245)
* L’interface utilisateur du Experience Manager n’affiche aucun message d’échec en cas d’échec de la création/mise à jour de l’ensemble. (ASSETS-10264)
* Impossible d’appliquer une stratégie enregistrée à l’un des conteneurs d’un modèle modifiable pour vous permettre d’ajouter des composants Dynamic Media. (ASSETS-11044)
* Les ressources ne sont pas chargées dans le compte Dynamic Media après l’exécution du workflow Retraiter les ressources de Dynamic Media sur les ressources dont le traitement de tâche est incorrect. (ASSETS-12084, ASSETS-9877)
* Les utilisateurs de lecteurs d’écran sont affectés par la variable `title` n’est pas fourni pour `<frame>` et `<iframe>` dans le **[!UICONTROL Type à rechercher]** de la boîte de dialogue (ASSETS-5483)
* Dans les lecteurs d’écran, connexes et significatives `alt=` doit être fournie pour plusieurs images présentes sous **[!UICONTROL Ressources]** dans le volet de gauche. (ASSETS-5644)
* Lecteur d’écran non lu **[!UICONTROL Mode muet]** et **[!UICONTROL Unmute]** sur la vidéo à l’aide du composant Dynamic Media. (ASSETS-10169)

## Commerce  {#commerce-6514}

* Les produits commerciaux ne sont pas triés à l’aide de l’en-tête de colonne et ils utilisent _remote_ le mode tri; à la place, les produits Commerce doivent être triés à l’aide d’en-têtes de colonne avec _local_ mode de tri. (CQ-4343750, NPR-38498)



## [!DNL Forms] {#forms-6514}

<!--

>[!NOTE]
>
> Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package a week after the scheduled [!DNL Experience Manager] Service Pack release.

>[!NOTE]
>
>* [!DNL Experience Manager Forms] releases the add-on packages one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages will release Thursday, September 1, 2022. In addition, a list of Forms fixes and enhancements will also be added to this section.

-->

* Lorsqu’un fichier est joint à un formulaire adaptatif à plusieurs panneaux et qu’un brouillon du formulaire adaptatif est enregistré, une erreur se produit. (NPR-38978)
* Lorsqu’un utilisateur convertit un profil de RGB en profil CMJN à l’aide de l’API Java createPDF2 avec les paramètres AdobePDF, l’option ne fonctionne pas avec l’API Java. Cette option fonctionne correctement avec l’application DistillerClient autonome. (NPR-38858, CQ-4346181)
* Après l’installation d’AEM Service Pack 12 Forms 6.5 (6.5.12.0), toutes les options, à l’exception de la fermeture de la tâche, ne sont plus disponibles à l’étape Affecter une tâche d’AEM Workflows. (NPR-38743)
* Dans un document d’enregistrement, certaines valeurs d’un tableau sont tronquées. (NPR-38657)
* Lors de la prévisualisation d’un jeu de formulaires avec des données XML, lorsque le fichier XDP contient un champ flottant, lors de la prévisualisation d’un jeu de formulaires, aucune donnée n’est affichée, mais les données sont affichées lorsque l’option Preview PDF est utilisée.
* Dans les Forms adaptatives, les boutons radio et les cases à cocher ne sont pas dans l’ordre de tabulation. (NPR-38645)
* Lorsque vous utilisez la variable `Summary Step` pour générer un document d’enregistrement (DE) pour un formulaire adaptatif traduit après envoi, n’est pas traduit dans la langue localisée. (NPR-38567)
* L’option désactiver la reprise dans les étapes AEM workflow ne fonctionne pas comme prévu. Le problème apparaît par intermittence. (NPR-38547)
* Lorsque le formulaire adaptatif est envoyé avec le champ de texte enrichi, la variable `an Internal Error while Submitting a Form` se produit. Lorsque l’utilisateur met l’accent sur le champ de texte enrichi, l’erreur ne se produit pas avant l’envoi du formulaire. (NPR-38542)
* Une erreur `sling-default-3-AdobeSignRefreshTokenScheduleJob com.adobe.forms.foundation.oauth.model.OAuthConfigSlingModel Refresh Token not present for: /conf/gws-eform/cashlite/settings/cloudconfigs/fdm/cashlite/jcr:content occurs` est consignée. (NPR-38541)
* Lorsqu’un utilisateur charge un PDF dans un formulaire adaptatif, le serveur AEM Forms ne répond plus. (NPR-38398)
* Sur un serveur AEM Forms on OSGi, lorsque vous utilisez l’API Document Service pour certifier le PDF, il échoue avec une erreur : com.adobe.fd.signatures.truststore.errors.exception.CredentialRetrievalException : AEM-DSS-311. (CQ-4346252)
* Lors de l’envoi des brouillons de lettres, la variable `Could not upload asset from xml input` s’affiche. Cela n’a aucun impact sur les fonctionnalités. Une fois un brouillon ouvert, la lettre s’affiche correctement. (CQ-4345979, CQ-4344418)
* Lorsqu’une date est saisie au format allemand et que la variable `Preview with Data` est utilisée pour une lettre, le champ Date n’est pas rendu. (CQ-4345783)
* Lorsque vous créez un portail web et générez des codes à barres basés sur des données, certains codes à barres ne sont pas décodés correctement. (CQ-4345743)
* La conversion Postscript vers le PDF ne génère pas de document de sortie avec les couleurs attendues. (CQ-4345074)
* Le résolveur de ressources entraîne des échecs d’envoi intermittents et entraîne l’affichage multiple d’une même trace de pile pour un seul envoi. (CQ-4344764)
* Les utilisateurs ne peuvent pas ouvrir les brouillons de lettres modifiés qui utilisent le `cmDataUrl` . Les brouillons s’ouvrent normalement pour la première fois. Les problèmes commencent à s’afficher lors des tentatives suivantes. (CQ-4344418)
* Lorsque l’utilisateur saisit la variable `&` dans une communication interactive (IC), le brouillon de la communication interactive ne parvient pas à se charger complètement. (CQ-4343969)
* Lorsque vous utilisez des options de style dans AEM Forms Designer pour générer des fichiers PCL, le style spécifié n’est pas appliqué aux fichiers générés. (CQ-4339573)
* Lorsque le nombre de pages est supérieur à 15, la conversion automatisée des formulaires XDP dynamiques en formulaires adaptatifs échoue. Cela fonctionne correctement lorsque le nombre de pages est inférieur à 15. (NPR-35337)
* Lorsque l’option Ajouter aux favoris est utilisée, elle n’indique pas l’état du basculement vers le lecteur d’écran. (NPR-37137)
* Dans le modèle de données de formulaire, les valeurs après la valeur décimale dans le modèle de données de formulaire soutenu par la base de données sont tronquées pour le type de données &quot;argent faible&quot; et &quot;argent faible&quot;. . (CQDOC-19509)
* Lorsque vous sélectionnez un lien de navigation pour le workflow dans HTML Workspace, il n’est pas indiqué que le lien de navigation est sélectionné. (NPR-37138)
* La fonction Signature tactile n’est pas compatible avec les consignes d’accessibilité. (NPR-37596)
* AEM Forms utilise log4j 1.x. La prise en charge de log4j 1.x a atteint sa fin de vie. (NPR-38273)
* Lorsque vous utilisez la base de données MSSQL comme source de données dans un modèle de données de formulaire et que vous récupérez des valeurs, les nombres après la décimale dans les valeurs de récupération sont activés. (CQ-4346190)
* Dans Forms 6.5 Designer, lorsque vous ouvrez un formulaire créé avec Forms 6.1 Designer et modifiez une zone de texte, l’espacement des paragraphes dépasse l’espace spécifié. Tous les paramètres précédents de l’espace sont supprimés et un reformatage manuel de la zone de texte est requis. (CQ-4341899)
* Une valeur incorrecte s’affiche pour le code à barres SSCC-18. Les serveurs Forms omettent la valeur dans la partie droite du code à barres. (CQ-4342400)
* Pour les PDF forms statiques créés avec Forms 6.5 Designer, l’accessibilité du PDF échoue en cas d’erreur. `Tab order entry in page with annotations not set to "S"`. (CQ-4343117)
* Possibilité de spécifier du texte de Reader d’écran pour les hyperliens dans Forms Designer.(NPR-36221)

## Intégrations {#integrations-6514}

* Activez la prise en charge de la compilation JavaScript ES6 (mode ECMAScript6 ou version ultérieure) pour la minimisation de la variable `/libs/cq/analytics/widgets.js` bibliothèque . (NPR-38433)
* Activez la prise en charge de la compilation JavaScript ES6 (mode ESMAScript6 ou version ultérieure) pour la minimisation de la variable `/libs/cq/testandtarget/clientlibs/testandtarget/util.js` bibliothèque . (NPR-38435)
* Plus il y a de contenu dans `/content/campaigns`, plus l’appel à la fonction `targeteditor.html` (`/libs/cq/personalization/touch-ui/content/targeteditor.html`) prend lorsque vous ouvrez l’éditeur de page. (NPR-38663)

## Plateforme {#platform-6514}

* Impossible de se connecter au gestionnaire de modules pour déployer les mises à jour. (NPR-38646)
* Dans l’interface utilisateur du sélecteur de balises de ressources, les balises s’affichent dans l’ordre dans lequel elles ont été créées. Cependant, lorsqu’il y a de nombreuses balises, l’affichage et la gestion des balises sont difficiles, car elles ne peuvent pas être triées. (CQ-4344279)
* Créez une notification dans l’interface utilisateur lorsqu’un utilisateur est emprunté à l’identité d’un administrateur ou d’une autre personne utilisant la variable **[!UICONTROL Se faire passer pour]** champ . (CQ-4345288)
* Dans une collection dynamique, toutes les ressources étaient affichées lors du filtrage à l’aide d’une recherche enregistrée. (CQ-4345326)
* Un nombre de ressources sélectionné incorrect est affiché pour **[!UICONTROL Ajouter à la collection]** when **[!UICONTROL Tout sélectionner]** est sélectionnée. (CQ-4345424)
* Un message d’exception s’est produit lors de l’utilisation de la variable **[!UICONTROL Se faire passer pour]** avec un groupe ou un utilisateur inexistant. (CQ-4346098)

## [!DNL Sites] {#sites-6514}

* Des suppressions de chemin inattendues se sont produites lors de la mise à niveau de Experience Manager de 6.5.12.0 vers 6.5.13.0. (NPR-38532)

### Accessibilité {#access-6514}

* Dans Experience Manager Sites, lorsque vous développez l’objet **[!UICONTROL Changer le format d’affichage et ajuster le paramètre d’affichage]** , puis sélectionnez **[!UICONTROL Mode Liste]**, la variable **[!UICONTROL Glisser-déposer]** n’a pas de nom accessible. (SITES-2863, NPR-38760)
* Le lecteur d’écran doit annoncer le nom accessible, tel que `Show description for Archive` ou `Show description for mini shopping cart`. Cependant, le nom accessible actuel est annoncé comme `Info Circle button show description` pour _all_ les boutons d’informations sur l’info-bulle. (SITES-3104)
* Améliorez l’annulation pour les composants qui n’ont pas de fonctionnalité intégréeEditing ou dropTarget dans `cq:editConfig`. (NPR-38361) <!-- version 2 (old) of the description above * When out of the box components that don't have inlineEditing or dropTarget feature in the _cq_editConfig file (navigation, breadcrumb, embed) are deleted > undeleted (by way of Undo), all configurations are lost and empty placeholder reappears. Component must be reconfigured from scratch. (NPR-38361) -->
* La liste déroulante Système de style peut avoir été positionnée en haut de la page au lieu de dans le contexte du composant, pour les composants qui utilisent `cq:editConfig` &quot;afteredit: REFRESH_PAGE&quot;. (NPR-38384) <!-- version 2 (old) of description above* When selecting a style option on a component, the Styles box shifts to the upper left corner of the screen, rather than staying put below the style icon. Happens for components that have  cq:editConfig "afteredit: REFRESH_PAGE". (NPR-38384) -->
* Le composant Texte n’est pas aligné lorsqu’il est ajouté aux conteneurs de mise en page imbriqués. (NPR-38193)
* Un onglet de style vide s’affichait lorsqu’il n’y avait aucune configuration de système de style pour un composant. L’onglet est maintenant masqué lorsqu’aucune configuration n’est présente. (NPR-38218) <!-- version 2 (old) of description above * Style tab is blank on components without styles/policies. (NPR-38218) -->
* La propriété `useLegacyResponsiveBehaviour` fonctionne uniquement lors de l’authentification. (NPR-37996)
* La mise à niveau de jquery-ui vers la dernière version entraînait la rupture de l’éditeur. (SITES-5647)

### [!DNL Content Fragments] {#sites-contentfragments-6514}

* La validation du champ de l’énumération Fragments de contenu est problématique la première fois que le fragment de contenu est chargé. (SITES-7140)
* Vous devez ajouter des champs de personnalisation Campaign dans l’éditeur de texte enrichi de l’éditeur Fragments de contenu. (NPR-38526)
* Lors de la création ou de la modification d’un fragment de contenu dans l’éditeur de fragment de contenu, le modèle de fragment de contenu n’est pas enregistré au moyen de Dispatcher. De plus, l’éditeur de fragments de contenu n’est pas fermé et une erreur s’affiche dans le journal du navigateur. (NPR-38691)
* Erreur de validation de requête persistante. (NPR-38523)
* Dans la boîte de dialogue Fragment de contenu, sous **[!UICONTROL Propriétés]**, la variable **[!UICONTROL Fragment de contenu]** ne conserve pas le chemin enregistré dans la fenêtre contextuelle de sélection. (NPR-38632)
* Lorsque vous créez un modèle de fragment de contenu et ajoutez un champ d’énumération du type de liste déroulante, la validation correcte de _`is required`_échoue. (NPR-38237)

### Composants principaux {#sites-corecomponents-6514}

* Le nouveau composant Courrier électronique de page ne doit pas vous forcer à accéder à l’interface utilisateur classique lors de la modification `/etc`. (NPR-38648)

### Éditeur de page {#sites-pageeditor-6514}

* L’utilisateur ne peut pas redimensionner le composant au nombre de colonnes souhaité. (NPR-38688)

### Éditeur de modèles {#sites-templateeditor-6514}

* Absente **[!UICONTROL Supprimer]** et **[!UICONTROL Couper]** des boutons de la barre de menus dans un modèle modifiable après un événement `cq:actions` a été personnalisée. (NPR-38521)
* Si un composant comprend un autre composant, il n’est pas possible de le supprimer dans la structure du modèle, car la variable **[!UICONTROL Supprimer]** est absent de la barre de menus. (NPR-38585)

## Sling {#sling-6514}

* Une augmentation du nombre de fichiers ouverts en production a été enregistrée en raison d’une fuite de mémoire dans le module . `DiscoveryLiteDescriptor` in `org.apache.sling.discovery.commons`, version 1.0.20. (NPR-38288)
* En Experience Manager, à partir de **[!UICONTROL Opérations]** > **[!UICONTROL Diagnostic]**, une erreur se produit lorsque vous sélectionnez **[!UICONTROL ZIP du statut de téléchargement]** > **[!UICONTROL Télécharger]**. (NPR-38514)

## Projets de traduction {#translation-6514}

* Le lancement des sous-pages ajoutées comme référence dans une page parente n’était pas converti lorsque la variable `isDeep` a été définie sur `false`. (NPR-38531)

## Interface utilisateur {#ui-6514}

* Lors de l’utilisation de **[!UICONTROL Tout sélectionner]** > **[!UICONTROL Publication rapide]**, Experience Manager ne publiait pas toutes les ressources ou n’affichait pas le nombre de ressources publiées dans **[!UICONTROL Carte]** afficher ou **[!UICONTROL Liste]** vue. (NPR-38546)
* Le nombre de ressources sélectionnées incorrectes s’affiche pour **[!UICONTROL Ajouter à la collection]** in **[!UICONTROL Tout sélectionner]** cas. (NPR-38633)
* Les utilisateurs désactivés peuvent toujours être ajoutés aux collections et aux projets. (NPR-38651)
* La suppression d’un filtre sans enregistrer le formulaire de recherche crée une erreur. (NPR-38698)
* La session d’un utilisateur ne peut pas obtenir un `ModifiableValueMap` pour les groupes afin d’établir l’appartenance directe au groupe. (NPR-38710)

## Workflow {#workflow-6514}

* Activez la prise en charge de la compilation JavaScript ES6 (mode ESMAScript6 ou version ultérieure) pour la minimisation de la variable `/libs/cq/inbox/gui/components/inbox/clientlibs/commons.js` bibliothèque . (NPR-38304)
* Une fois le workflow exécuté et les étapes du processus terminées, le même commentaire est répété plusieurs fois. (NPR-38364)

## Installer [!DNL Experience Manager] 6.5.14.0 {#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.14.0 nécessite [!DNL Experience Manager] 6.5. Voir [documentation de mise à niveau](/help/sites-deploying/upgrade.md) pour obtenir des instructions détaillées. <!-- UPDATE FOR EACH NEW RELEASE -->
* Le téléchargement du Service Pack est disponible sur Adobe [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
* Sur un déploiement avec MongoDB et plusieurs instances, installez [!DNL Experience Manager] 6.5.14.0 sur l’une des instances d’auteur à l’aide du gestionnaire de modules.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!NOTE]
>
>Adobe ne recommande pas de supprimer ou de désinstaller le [!DNL Experience Manager] Package 6.5.14.0. <!-- UPDATE FOR EACH NEW RELEASE -->

### Installez le Service Pack sur [!DNL Experience Manager] 6,5 {#install-service-pack}

1. Redémarrez l’instance avant l’installation si l’instance est en mode de mise à jour (lorsque l’instance a été mise à jour à partir d’une version antérieure). Adobe recommande un redémarrage si le temps de disponibilité actuel d’une instance est élevé.

1. Avant l’installation, prenez un instantané ou une nouvelle sauvegarde de votre [!DNL Experience Manager] instance.

1. Téléchargez le Service Pack à partir de [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.14.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Ouvrez Package Manager, puis sélectionnez **[!UICONTROL Télécharger le module]** pour télécharger le module. Pour en savoir plus, voir [Gestionnaire de modules](/help/sites-administering/package-manager.md).

1. Sélectionnez le module, puis sélectionnez **[!UICONTROL Installer]**.

1. Pour mettre à jour le connecteur S3, arrêtez l’instance après l’installation du Service Pack, remplacez le connecteur existant par un nouveau fichier binaire fourni dans le dossier d’installation, puis redémarrez l’instance. Voir [Entrepôt de données Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>La boîte de dialogue de l’interface utilisateur de Package Manager se ferme parfois pendant l’installation du Service Pack. Adobe recommande d’attendre que les journaux d’erreurs se stabilisent avant d’accéder au déploiement. Attendez les logs spécifiques liés à la désinstallation du lot de mise à jour avant de vous assurer que les installations sont réussies. En règle générale, ce problème se produit dans [!DNL Safari] mais peut se produire par intermittence sur n’importe quel navigateur.

**Installation automatique**

Vous pouvez utiliser deux méthodes différentes pour installer automatiquement [!DNL Experience Manager] 6.5.14.0.<!-- UPDATE FOR EACH NEW RELEASE -->

* Placez le module dans `../crx-quickstart/install` lorsque le serveur est disponible en ligne. Le package est automatiquement installé.
* Utilisez la variable [API HTTP à partir de Package Manager](/help/sites-administering/package-manager.md#package-share). Utilisation `cmd=install&recursive=true` afin que les modules imbriqués soient installés.

>[!NOTE]
>
>Experience Manager 6.5.14.0 ne prend pas en charge l’installation de Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Validation de l’installation**

Pour connaître les plates-formes certifiées pour travailler avec cette version, reportez-vous à la section [exigences techniques](/help/sites-deploying/technical-requirements.md).

1. la page d’informations sur les produits (`/system/console/productinfo`) affiche la chaîne de version mise à jour. `Adobe Experience Manager (6.5.14.0)` under [!UICONTROL Produits installés]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. Tous les lots OSGi sont : **[!UICONTROL PRINCIPAL]** ou **[!UICONTROL FRAGMENT]** dans la console OSGi (Utiliser la console web : `/system/console/bundles`).

1. Le lot OSGi `org.apache.jackrabbit.oak-core` est version 1.22.12 ou ultérieure (Utiliser la console web : `/system/console/bundles`). <!-- NPR-38747 -->

### Installer [!DNL Experience Manager] Package de module complémentaire Forms {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Ignorer si vous n’utilisez pas [!DNL Experience Manager] Forms.

<!-- 

Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package a week after the scheduled [!DNL Experience Manager] Service Pack release.

-->

1. Assurez-vous que vous avez installé le [!DNL Experience Manager] Service Pack.
1. Téléchargez le module complémentaire Forms correspondant répertorié dans les [versions AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates) pour votre système d’exploitation.
1. Installez le module complémentaire Forms comme décrit dans [Installation des packages de modules complémentaires AEM Forms](/help/forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).
1. Si vous utilisez des lettres dans Experience Manager 6.5 Forms, installez la variable [dernier package de compatibilité AEMFD](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates).

### Installer [!DNL Experience Manager] Forms on JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Passez cette étape si vous n’utilisez pas AEM Forms sous JEE. Correctifs de [!DNL Experience Manager] Forms on JEE est fourni via un programme d’installation distinct.

Pour plus d’informations sur l’installation du programme d’installation cumulatif pour [!DNL Experience Manager] Configuration de Forms on JEE et post-déploiement, voir la section [notes de mise à jour](jee-patch-installer-65.md).

>[!NOTE]
>
>Après l’installation du programme d’installation cumulatif pour [!DNL Experience Manager] Forms on JEE, installez le dernier module complémentaire Forms, supprimez le module complémentaire Forms du `crx-repository\install` et redémarrez le serveur.

### UberJar {#uber-jar}

UberJar pour [!DNL Experience Manager] 6.5.13.0 est disponible dans la [Référentiel Maven Central](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.13/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

>[!NOTE]
>
>Dans Experience Manager 6.5.14.0, sachez que la version d’UberJar (6.5.13.0) reste identique à la version précédente.

Pour utiliser UberJar dans un projet Maven, voir [utilisation d’UberJar](/help/sites-developing/ht-projects-maven.md) et incluez la dépendance suivante dans le POM de votre projet : <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.13</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar et les autres artefacts associés sont disponibles sur le référentiel central Maven au lieu du référentiel Maven public Maven Adobe (`repo.adobe.com`). Le fichier UberJar principal est renommé `uber-jar-<version>.jar`. Il n&#39;y a donc pas de `classifier`, avec `apis` comme valeur, pour la propriété `dependency` balise .

## Fonctionnalités obsolètes {#removed-deprecated-features}

Vous trouverez ci-dessous une liste des fonctionnalités signalées comme obsolètes par [!DNL Experience Manager] 6.5.7.0. Les fonctionnalités sont initialement marquées comme obsolètes et supprimées ultérieurement dans une version ultérieure. Une autre option est fournie.

Vérifiez si vous utilisez une fonctionnalité ou une fonctionnalité dans un déploiement. En outre, envisagez de modifier la mise en oeuvre afin d’utiliser une autre option.

| Zone | Fonctionnalité | Remplacement |
|---|---|---|
| Intégrations | Le **[!UICONTROL Accord préalable des services cloud AEM]** est obsolète, car la variable [!DNL Experience Manager] et [!DNL Adobe Target] l’intégration est mise à jour dans [!DNL Experience Manager] 6.5. L’intégration prend en charge l’API Adobe Target Standard. L’API utilise l’authentification au moyen d’Adobe IMS et [!DNL Adobe I/O Runtime]. Il prend en charge le rôle croissant d’Adobe Launch pour l’instrumenter. [!DNL Experience Manager] pour les analyses et la personnalisation, l’assistant de souscription n’a aucune utilité sur le plan fonctionnel. | Configuration des connexions système, de l’authentification Adobe IMS et [!DNL Adobe I/O Runtime] intégrations via les [!DNL Experience Manager] services cloud. |
| Connecteurs | Adobe JCR Connector for Microsoft® SharePoint 2010 et Microsoft® SharePoint 2013 est obsolète pour [!DNL Experience Manager] 6.5. | S/O |

## Problèmes connus {#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THE LIST.
 -->

* [AEM du fragment de contenu avec le package d’index GraphQL 1.0.3](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fcfm-graphql-index-def-1.0.3.zip)

* As [!DNL Microsoft® Windows Server 2019] ne prend pas en charge [!DNL MySQL 5.7] et [!DNL JBoss® EAP 7.1], [!DNL Microsoft® Windows Server 2019] ne prend pas en charge les installations clé en main pour [!DNL AEM Forms 6.5.10.0].

* Si vous effectuez une mise à niveau de votre [!DNL Experience Manager] de la version 6.5 à la version 6.5.10.0, vous pouvez afficher `RRD4JReporter` exceptions dans la variable `error.log` fichier . Pour résoudre le problème, redémarrez l’instance.

* Si vous installez [!DNL Experience Manager] 6.5 Service Pack 10 ou un Service Pack précédent sur [!DNL Experience Manager] 6.5, la copie d’exécution du modèle de workflow personnalisé de vos ressources (créé dans `/var/workflow/models/dam`) est supprimé.
Pour récupérer votre copie d’exécution, Adobe recommande de synchroniser la copie d’heure de conception du modèle de workflow personnalisé avec sa copie d’exécution à l’aide de l’API HTTP :
   `<designModelPath>/jcr:content.generate.json`.

* Les utilisateurs peuvent renommer un dossier dans une hiérarchie de [!DNL Assets] et publier un dossier imbriqué dans [!DNL Brand Portal]. Toutefois, le titre du dossier n’est pas mis à jour dans [!DNL Brand Portal] jusqu’à ce que le dossier racine soit republié.

* Lorsqu’un utilisateur choisit de configurer un champ pour la première fois dans un formulaire adaptatif, l’option permettant d’enregistrer une configuration ne s’affiche pas dans l’explorateur de propriétés. Sélectionner pour configurer un autre champ du formulaire adaptatif dans le même éditeur résout le problème.

* Les erreurs et messages d’avertissement suivants peuvent s’afficher lors de l’installation : [!DNL Experience Manager] 6.5.x.x :
   * &quot;Lorsque l’intégration Adobe Target est configurée dans [!DNL Experience Manager] l’utilisation de l’API Target Standard (authentification IMS), puis l’exportation de fragments d’expérience vers Target entraîne la création de types d’offres incorrects. Au lieu de saisir &quot;Fragment d’expérience&quot;/source &quot;Adobe Experience Manager&quot;, Target crée plusieurs offres avec le type &quot;HTML&quot;/la source &quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: Aucune fenêtre de maintenance n’a été trouvée sur granite/operations/maintenance.
   * La validation côté serveur du formulaire adaptatif échoue lorsque des fonctions d’agrégat telles que SUM, MAX et MIN sont utilisées (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Aucune fenêtre de maintenance n’a été trouvée sur granite/operations/maintenance.
   * La zone réactive d’une image interactive Dynamic Media n’est pas visible lors de la prévisualisation de la ressource via la visionneuse de bannières Shoppable.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : Délai d’attente avant que la modification de l’enregistrement ne soit terminée.

* Lorsque vous tentez de déplacer/supprimer/publier des fragments de contenu ou des sites/pages, un problème se produit lorsque les références aux fragments de contenu sont récupérées, car la requête en arrière-plan échoue ; c’est-à-dire que la fonctionnalité ne fonctionne pas.
Pour garantir le bon fonctionnement, vous devez ajouter les propriétés suivantes au noeud de définition d’index. `/oak:index/damAssetLucene` (aucune réindexation n’est requise) :

   ```xml
   "tags": [
       "visualSimilaritySearch"
     ]
   "refresh": true
   ```

## Lots OSGi et packages de contenu inclus {#osgi-bundles-and-content-packages-included}

Les documents texte suivants répertorient les lots OSGi et les packages de contenu inclus dans [!DNL Experience Manager] 6.5.14.0 : <!-- UPDATE FOR EACH NEW RELEASE -->

* [Liste des lots OSGi inclus dans Experience Manager 6.5.14.0](/help/release-notes/assets/65140_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Liste des packages de contenu inclus dans Experience Manager 6.5.14.0](/help/release-notes/assets/65140_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Sites web à accès limité {#restricted-sites}

Ces sites web ne sont disponibles que pour les clients. Si vous êtes client et avez besoin d’un accès, contactez votre responsable de compte Adobe.

* [Téléchargement du produit à l’adresse licensing.adobe.com](https://licensing.adobe.com/)
* [Contacter le service clientèle d’Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] page produit](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] Documentation 6.5](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=fr)
>* [Abonnement aux mises à jour de produits prioritaires d’Adobe](https://www.adobe.com/subscription/priority-product-update.html)

