---
title: Notes de mise à jour de la version 6.5 d’ [!DNL Adobe Experience Manager]
description: Consultez les informations sur la mise à jour, y compris les nouveautés, la procédure d’installation et une liste complète des modifications pour  [!DNL Adobe Experience Manager]  6.5.
mini-toc-levels: 3
exl-id: fed4e110-9415-4740-aba1-75da522039a9
source-git-commit: efd2a41b6b53a72b941ac23386b6aa4c41c9da15
workflow-type: tm+mt
source-wordcount: '2683'
ht-degree: 41%

---

# Notes de mise à jour du dernier pack de services [!DNL Adobe Experience Manager] 6.5 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/Documents/issue_tracker_sp_cfp_updates.xlsx?d=w3ea81ae4e6054153b132f2698c86f84e&csf=1&web=1&e=7yhrWb&nav=MTVfe0U0RjdDQUM3LTZCQ0EtNDk1Qy04Mjc1LTM2MUJEMzE1OEVGN30 -->

<!-- DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, June 1, 2023. In addition, a list of Forms fixes and enhancements is added to this section. -->

## Informations sur la version {#release-information}

| Produit | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Version | 6.5.17.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Type | Mise à jour du pack de services |
| Date | jeudi 25 mai 2023 <!-- UPDATE FOR EACH NEW RELEASE --> |
| URL de téléchargement | [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.17.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## Éléments compris dans [!DNL Experience Manager] 6.5.17.0 {#what-is-included-in-aem-6517}

[!DNL Experience Manager] 6.5.17.0 comprend de nouvelles fonctionnalités, des améliorations importantes demandées par les clients, des correctifs de bogues, ainsi que des améliorations des performances, de la stabilité et de la sécurité, publiées depuis la version initiale de 6.5 en avril 2019. [Installez ce Service Pack](#install) sur [!DNL Experience Manager] 6.5. <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- Some of the key features and improvements are the following:

* _REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

Certaines des fonctionnalités et améliorations clés de cette version sont les suivantes :

* **Améliorations de l’expérience de recherche** - Vous pouvez désormais effectuer rapidement les opérations suivantes sur les ressources qui s’affichent dans les résultats de recherche :
   * Créer un workflow
   * Création d’une version
   * Lier ou dissocier des ressources

   Vous n’avez pas besoin d’accéder à l’emplacement de la ressource et d’afficher ses propriétés pour effectuer ces opérations.
* **Dynamic Media _Instantané_**- Testez des images de test ou des URL Dynamic Media pour voir la sortie de différents modificateurs d’image et les optimisations de l’imagerie dynamique pour la taille de fichier (avec diffusion WebP et AVIF), la bande passante réseau et le rapport pixel du périphérique. Voir [Instantané Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot.html).
* **Diffusion DASH en continu avec Dynamic Media** - Nouvelle prise en charge du protocole (DASH - Dynamic Adaptive Streaming over HTTP) pour la diffusion en continu adaptative dans les diffusions vidéo Dynamic Media (avec CMAF activé). Disponible maintenant pour toutes les régions, [activé au moyen d’un ticket d’assistance](/help/assets/video.md#enable-dash-on-your-account-enable-dash).

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## [!DNL Assets]{#assets-6517}

* Lorsque vous publiez plus de 40 PDF simultanément, [!DNL Experience Manager] arrête de répondre et devient indisponible pendant un certain temps. (ASSETS-21789)
* Si vous êtes connecté en tant qu’utilisateur test, vous ne pouvez pas voir les ressources liées à une ressource spécifique lorsque vous cliquez sur les propriétés d’une ressource. (ASSETS-21648)
* Lors de la modification de ressources à l’aide de `Desktop Actions`, si vous essayez d’archiver plus de cinq ressources à la fois, `Limit Reached` s’affiche et les ressources sélectionnées sont extraites. (ASSETS-21121)
* Impossible de trier les ressources par nom dans une collection. (ASSETS-20924)
* Impossible de définir des dimensions sur les ressources d’un type de format d’image. (ASSETS-20835)
* Le texte de l’info-bulle et son arrière-plan dans le champ Rechercher/ajouter une adresse électronique n’affichent pas le rapport de contraste approprié lors du partage d’un lien. (ASSETS-17347)
* Lorsque vous développez `Notifications`, le texte ne s’affiche pas correctement en raison de l’espacement des paragraphes. (ASSETS-17345)
* Lorsque vous copiez une ressource dans la collection, `Public Collection` ne s’affiche pas correctement. (ASSETS-17343)
* Les éléments utilisent des attributs ARIA sans rôle. (ASSETS-17325, ASSETS-17323)
* Le lien n’est pas descriptif lorsque vous développez `Notifications`. (ASSETS-17283)
* Lorsque vous naviguez et développez l’événement [!DNL Smart Crop] , le contenu apparaît comme une liste, mais il n’est pas marqué comme une liste non ordonnée. Par conséquent, le lecteur d’écran ne reconnaît pas la liste non ordonnée et la lit comme du texte brut. (ASSETS-17247)
* Le `Sort By` n’est pas associé à la liste déroulante correspondante. Par conséquent, le lecteur d’écran ne reconnaît pas les options de liste déroulante. (ASSETS-17239)
* Impossible d’avancer ou de reculer à l’aide de l’onglet du clavier ou des touches fléchées lorsque vous essayez d’ajouter un utilisateur à l’aide de la fonction `Add user` liste déroulante. (ASSETS-17233)
* Le lecteur d’écran ne transmet pas correctement les informations de l’étape Workflows (ASSETS-17285).
* Lorsque vous accédez à `Saved Searches` liste modifiable, les noms et les rôles ne sont associés à aucun libellé. (ASSETS-17329)
* Lorsque vous naviguez `Collection` et passez la souris sur le texte. *Membres*, le texte n’apparaît pas comme marqué. Par conséquent, le lecteur d’écran ne reconnaît pas le texte du titre et le lit comme du texte brut. (ASSETS-17245)
* Impossible d’accéder à `View Settings` à l’aide de la touche de défilement du clavier vers le bas ou vers le haut. (ASSETS-17257)
* Impossible de déclencher un workflow pour plusieurs ressources sélectionnées qui se trouvent à l’aide de filtres de recherche. (ASSETS-7689)
* Lorsque vous sélectionnez une ressource (ou plusieurs ressources) dans les résultats de recherche, l’option Mettre en relation ou Ne plus mettre en relation n’est pas visible. Mais cette option est disponible, sinon. (ASSETS-7679)
* Le panneau Filtres de recherche ne s’ouvre qu’une seule fois après la connexion et ne s’ouvre pas si vous quittez la page de recherche et réexécutez la recherche. (ASSETS-7671)
* La liste déroulante des emails n’affiche pas le rapport de contraste approprié lors du partage d’un lien. (ASSETS-17349)

<!-- REMOVED BY ENGINEERING FROM TOTAL RELEASE CANDIDATE LIST 
* When you select any file in a Collection and click `Download`, and then navigate to the email checkbox and expand it, regular text and email link is not recognizable due to background color. (ASSETS-17349) 
* When you navigate to `Smart Crop` option, the screen reader does not announce the expand or collapse state of the button. (ASSETS-17335)-->

## [!DNL Assets] - [!DNL Dynamic Media]{#dm-6517}

* La connexion à Dynamic Media est interrompue lorsqu’une configuration de cloud Dynamic Media existe déjà. (ASSETS-23057)
* Les performances accrues lors de la navigation dans des dossiers contenant de nombreuses vidéos Dynamic Media et résolus ne parviennent pas à charger le problème en mode Carte de dossiers. (ASSETS-23016)
* Les jetons d’aperçu sont supprimés de `error.log` qui peut être utilisé pour demander du contenu sécurisé auprès des serveurs de test sécurisés. (ASSETS-22685)
* Le rendu des miniatures de PDF ajoute une ombre. Mise à niveau de la bibliothèque Gibson version 4.0.1680232194 pour résoudre le problème de rendu des miniatures de PDF. (ASSETS-22585)
* Le mode hybride de Dynamic Media est désormais compatible avec la version 8.0.1 de l’agent New Relic (ASSETS-22578).
* Les listes de contrôle d’accès de Experience Manager (Access Control List) sont désormais respectées lors de la prévisualisation de fichiers Dynamic Media sur Experience Manager. (ASSETS-21628)
* Les lecteurs d’écran ne naviguent pas vers un élément masqué lorsque l’utilisateur tente de naviguer à l’aide de la touche Flèche vers le bas ou de la touche de tabulation. (ASSETS-5617)
* Interface utilisateur du profil d’image limitée pour les recadrages intelligents portant le même nom, la même dimension ou les deux. (ASSETS-16997)
* La largeur et la hauteur par défaut sont désormais définies sur 50 pixels pour les recadrages intelligents sur l’interface utilisateur du profil d’image. (ASSETS-16997)

## [!DNL Commerce]{#commerce-6517}

* Les balises déplacées sont nettoyées mais sont toujours référencées par les produits sous `/var`. (CQ-4351337)

## [!DNL Forms]{#forms-6517}

>[!NOTE]
>
>Correctifs de [!DNL Experience Manager] Forms est livré par le biais d’un module complémentaire distinct une semaine après la planification de la [!DNL Experience Manager] Date de publication du Service Pack. Dans ce cas, les modules complémentaires sont publiés le jeudi 1er juin 2023. En outre, une liste des correctifs et améliorations de Forms est ajoutée à cette section.

## Intégrations{#integrations-6517}

* Lors de la conversion d’une configuration IMS Adobe Target en informations d’identification d’utilisateur dans les configurations cloud héritées, la variable `connectedWhen` ne change pas. Ce problème fait passer tous les appels comme si la configuration était toujours basée sur IMS. (CQ-4352810)
* Ajouter `modifyProperties` autorisation d’accès `fd-cloudservice` utilisateur système pour la configuration Adobe Sign. (FORMS-6164)
* Avec Experience Manager intégré à Adobe Target, lorsque vous créez une activité de test AB, elle ne synchronise pas les audiences qui lui sont associées, avec Target. (NPR-40085)

## Oak{#oak-6517}

Depuis le Service Pack 13 et les versions ultérieures, le journal d’erreur suivant a commencé à s’afficher, ce qui affecte le cache de persistance :

```shell
org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.0.202/5]
at org.h2.mvstore.DataUtils.newMVStoreException(DataUtils.java:1004)
    at org.h2.mvstore.MVStore.getUnsupportedWriteFormatException(MVStore.java:1059)
    at org.h2.mvstore.MVStore.readStoreHeader(MVStore.java:878)
    at org.h2.mvstore.MVStore.<init>(MVStore.java:455)
    at org.h2.mvstore.MVStore$Builder.open(MVStore.java:4052)
    at org.h2.mvstore.db.Store.<init>(Store.java:129)
```

OU

```shell
org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.1.214/5].
```

Pour résoudre cette exception, procédez comme suit :

1. Supprimez les deux dossiers suivants de `crx-quickstart/repository/`

   * `cache`
   * `diff-cache`

1. Installez le Service Pack ou redémarrez Experience Manager as a Cloud Service.
Nouveaux dossiers de `cache` et `diff-cache` sont automatiquement créés et vous ne voyez plus d’exception liée à `mvstore` dans le `error.log`.

## Plateforme{#platform-6517}

* Dans l’interface utilisateur de Experience Manager Tag Management (/aem/tags/), les espaces de noms et les balises s’affichent dans l’ordre dans lequel ils ont été créés. Cependant, lorsqu’il existe de nombreux espaces de noms et balises, la possibilité de les afficher et de les gérer est difficile. Ce problème est dû au fait qu’ils ne peuvent pas être triés d’une autre manière. (NPR-39620)
* La mise à jour de la version de fermeture de Google est nécessaire, car Minification js ne fonctionne pas pour certaines bibliothèques clientes. (NPR-40043)

## [!DNL Sites]{#sites-6517}

* Baisse des performances dans LinkCheckerTransformer. (SITES-11661)
* Les copies de langue d’une page n’étaient pas mises à jour comme prévu. (SITES-11191)
* Ouverture d’un appel de pages hors campagne `targeteditor.html` inutilement. Supprimez le `targeteditor` appelez lorsque cela n’est pas nécessaire. (SITES-12469)
* Les Live Copies ne peuvent pas être créées pour les pages avec des annotations. (SITES-12154)
* Le déploiement des pages fonctionne sur Experience Manager 6.5.16. (SITES-12008)
* Mémoire insuffisante; activité de nettoyage de la mémoire élevée en raison de `NotificationManagerImpl`. `NotificationManager` mise à niveau du lot vers AEM 6.5. (SITES-11440)
* Correction des tests WCM IT qui bloquaient le service pack 17. (SITES-13089)
* La récupération des références Sites échoue sur le servlet. (SITES-10901)

### [!DNL Sites] - Interface utilisateur d’administration{#sites-adminui-6517}

* La fenêtre d’aperçu du sélecteur d’images miniatures ne peut pas être fermée. (SITES-10459)

### [!DNL Sites] - [!DNL Content Fragments]{#sites-contentfragments-6517}

* Configuration pour la connexion à l’objet de service Polaris (URL, informations d’identification, rappel, etc.). (SITES-12149)
* Utilisation de `SemanticDataType.REFERENCE` doit prendre en charge &quot;Remote-Asset-IDs&quot;. (SITES-12127)
* Intégrez le sélecteur de ressources Polaris à l’éditeur de fragment de contenu. (SITES-12125)
* Un en-tête http obligatoire était nécessaire pour accéder au point d’entrée du service de métadonnées. (SITES-13068)
* La mise en oeuvre GraphQL de la version 6.5 n’était pas conforme avec Cloud Service (Principal); les problèmes identifiés ont été corrigés. (SITES-13096)
* La pagination/le tri GraphQL et le filtrage hybride doivent être disponibles sur AEM 6.5/AMS. (SITES-9154)

### [!DNL Sites] - Composants principaux{#sites-core-components-6517}

* La propriété `cq-msm-lockable` a une valeur de redirection incorrecte dans le composant de page Foundation. (SITES-10904)
* Le sélecteur de ressources distant redirige toujours vers l’environnement intermédiaire IMS. (SITES-13433)

### [!DNL Sites] - [!DNL Experience Fragments]{#sites-experiencefragments-6517}

* Lorsque vous sélectionnez une configuration Externalizer dans un fragment d’expérience lors de l’exportation vers Adobe Target, une URL externalisée incorrecte est envoyée. (SITES-12402)
* Supprimer les termes non inclusifs ; appliquez les directives relatives aux termes inclusifs. (SITES-11244)

### [!DNL Sites] - Éditeur de page{#sites-pageeditor-6517}

* Aucune miniature n’est affichée pour un ensemble de carrousel dans le rail latéral de l’outil de recherche de contenu du Experience Manager. (SITES-8593)

## Sling{#sling-6517}

* Sling `ResourceMerger` consomme une grande quantité de processeur lorsqu’il est fourni avec un chemin fictif, ce qui entraîne un déni de service. (NPR-40338)

## Projets de traduction{#translation-6517}

<!-- REMOVED BY ENGINEERING FROM TOTAL RELEASE CANDIDATE LIST * The `translationrules.xml` is sorted poorly when adding a rule to a property by way of the translation configuration user interface. (NPR-40431) -->
* La copie de langue n’est pas créée lorsque l’utilisateur ne configure pas de champs non obligatoires. (NPR-40036)

## Interface utilisateur{#ui-6517}

* Le bouton Annuler dans les propriétés de page est inactif ; vous devriez accéder à l’interface utilisateur Administration de sites . (NPR-40501)

<!-- ## WCM{#wcm-6517}

* TEXT -->

## Workflow{#workflow-6517}

* Modifications de la console Processus. (NPR-40502)
* `SegmentNotfound errors` dans les journaux d’une instance d’auteur de production, provoquée par le résolveur de ressources non fermé dans la classe . `com.day.cq.workflow.impl.email.EMailNotificationServic`. (NPR-40187)
* Une fermeture non fermée `ResourceResolver` l’exception est consignée. (ASSETS-22495)
* L’auteur Experience Manager se bloque lorsque PSD/PDF est énorme `DocumentAncestors` les attributs de métadonnées sont chargés. (ASSETS-22966)
* Fuite de session dans la classe `InboxSharingCache` avec `user-reader-service`. (CQ-4352513)
* La liste des utilisateurs et des groupes incomplète s’affiche lorsque l’étape &quot;Programme de sélection des participants de l’initiateur de workflow&quot; répertorie les utilisateurs et les groupes pour l’étape Participant. Ce problème se produisait lorsqu’un groupe était également membre d’un autre groupe. (NPR-40055)
* Purge améliorée des workflows. (NPR-40459)

## Installer [!DNL Experience Manager] 6.5.17.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.17.0 nécessite [!DNL Experience Manager] 6.5. Consultez la [documentation de mise à niveau](/help/sites-deploying/upgrade.md) pour des instructions détaillées. <!-- UPDATE FOR EACH NEW RELEASE -->
* Le téléchargement du Service Pack est disponible dans la [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.17.0.zip) d’Adobe.
* Lors d’un déploiement avec MongoDB et plusieurs instances, installez [!DNL Experience Manager] 6.5.17.0 sur l’une des instances de création à l’aide du gestionnaire de modules.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe ne recommande pas de supprimer ou de désinstaller le module [!DNL Experience Manager] 6.5.17.0. Par conséquent, avant d’installer le module, vous devez créer une sauvegarde de la variable `crx-repository` au cas où vous devriez le restaurer. <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for AEM Forms, see [AEM Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### Installation du pack de services sur [!DNL Experience Manager] 6.5{#install-service-pack}

1. Redémarrez l’instance avant l’installation si l’instance est en mode de mise à jour (lorsque l’instance a été mise à jour à partir d’une version antérieure). Adobe recommande un redémarrage si le temps de disponibilité actuel d’une instance est élevé.

1. Avant l’installation, prenez un instantané ou exécutez une sauvegarde récente de votre instance [!DNL Experience Manager].

1. Téléchargez le pack de services à partir de la [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.17.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Ouvrez le gestionnaire de modules et cliquez sur **[!UICONTROL Charger le module]** pour charger le module. Pour en savoir plus, consultez la section [Gestionnaire de modules](/help/sites-administering/package-manager.md).

1. Sélectionnez le module, puis sélectionnez **[!UICONTROL Installer]**.

1. Pour mettre à jour le connecteur S3, arrêtez l’instance après l’installation du pack de services, remplacez le connecteur existant par un nouveau fichier binaire fourni dans le dossier d’installation, puis redémarrez l’instance. Consultez la section [Entrepôt de données S3 Amazon](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>La boîte de dialogue de l’interface utilisateur du gestionnaire de packages se ferme parfois pendant l’installation du pack de services. Adobe recommande d’attendre que les journaux d’erreurs se stabilisent avant d’accéder au déploiement. Attendez les logs spécifiques liés à la désinstallation de la mise à jour complète avant de vous assurer que les installations sont réussies. En règle générale, ce problème se produit dans [!DNL Safari] mais peut se produire par intermittence sur n’importe quel navigateur.

**Installation automatique**

Vous pouvez utiliser deux méthodes différentes pour installer automatiquement [!DNL Experience Manager] 6.5.17.0.<!-- UPDATE FOR EACH NEW RELEASE -->

* Placez le package dans le dossier `../crx-quickstart/install` lorsque le serveur est disponible en ligne. Le package est automatiquement installé.
* Utilisez l’[API HTTP à partir du gestionnaire de packages](/help/sites-administering/package-manager.md#package-share). Utilisez `cmd=install&recursive=true` afin que les packages imbriqués soient installés.

>[!NOTE]
>
>Experience Manager 6.5.17.0 ne prend pas en charge l’installation en Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Validation de l’installation**

Pour connaître les plateformes certifiées pour travailler avec cette version, reportez-vous à la section des [exigences techniques](/help/sites-deploying/technical-requirements.md).

1. La page d’informations sur les produits (`/system/console/productinfo`) affiche la chaîne de version mise à jour `Adobe Experience Manager (6.5.17.0)` sous [!UICONTROL Produits installés]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. Tous les lots OSGi sont au statut **[!UICONTROL ACTIF]** ou **[!UICONTROL FRAGMENT]** dans la console OSGi (utilisez la console web : `/system/console/bundles`).

1. Le bundle OSGi `org.apache.jackrabbit.oak-core` est de la version 1.22.15 ou ultérieure (utiliser la console Web : `/system/console/bundles`). <!-- NPR-40398 for 6.5.17.0 --> <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### Installer le Service Pack sur [!DNL Experience Manager] Forms{#install-aem-forms-add-on-package}

Pour obtenir des instructions sur l’installation du pack de services sur AEM Forms, voir les [instructions d’installation du pack de services AEM Forms](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

### Installation du package d’index GraphQL pour les fragments de contenu Experience Manager{#install-aem-graphql-index-add-on-package}

Les clients qui utilisent GraphQL doivent installer la variable [AEM de fragment de contenu avec le package d’index GraphQL 1.1.1](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip).

Cela vous permet d’ajouter la définition d’index requise en fonction des fonctionnalités qu’ils utilisent réellement.

L’échec de l’installation de ce package peut entraîner des requêtes GraphQL lentes ou en échec.

>[!NOTE]
>
>N’installez ce package qu’une seule fois par instance ; il n’est pas nécessaire de le réinstaller avec chaque Service Pack.

### UberJar{#uber-jar}

UberJar pour [!DNL Experience Manager] 6.5.17.0 est disponible dans le [référentiel central Maven](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.17/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Pour utiliser UberJar dans un projet Maven, consultez la section [Utilisation d’UberJar](/help/sites-developing/ht-projects-maven.md) et incluez la dépendance suivante dans le POM de votre projet : <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.17</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar et les autres artefacts associés sont disponibles sur le référentiel central Maven au lieu du référentiel Maven public Adobe (`repo.adobe.com`). Le fichier UberJar principal est renommé `uber-jar-<version>.jar`. Il n’existe donc pas de `classifier` avec `apis` comme valeur pour la balise `dependency`.

## Fonctionnalités obsolètes{#removed-deprecated-features}

Vous trouverez ci-dessous une liste des fonctionnalités signalées comme obsolètes par [!DNL Experience Manager] 6.5.7.0. Ces fonctionnalités sont initialement marquées comme obsolètes et supprimées ultérieurement dans une version future. Une option alternative est fournie.

Vérifiez si vous utilisez une de ces fonctionnalités dans un déploiement. Envisagez également de changer de mise en œuvre et d’utiliser une autre option.

| Domaine | Fonctionnalité | Remplacement |
|---|---|---|
| Intégrations | L’écran **[!UICONTROL Accord préalable des services cloud AEM]** est obsolète, car la variable [!DNL Experience Manager] et [!DNL Adobe Target] l’intégration est mise à jour dans [!DNL Experience Manager] 6.5. L’intégration prend en charge l’API Adobe Target Standard. L’API utilise l’authentification au moyen d’Adobe IMS et d’[!DNL Adobe I/O Runtime]. Elle prend en charge le rôle croissant d’Adobe Launch pour utiliser les pages [!DNL Experience Manager] à des fins d’analyse et de personnalisation, l’assistant d’accord préalable n’a donc aucune utilité sur le plan fonctionnel. | Configurez des connexions système, l’authentification Adobe IMS et les intégrations d’[!DNL Adobe I/O Runtime] à l’aide des services cloud [!DNL Experience Manager] correspondants. |
| Connecteurs | Adobe JCR Connector for Microsoft® SharePoint 2010 et Microsoft® SharePoint 2013 est obsolète dans [!DNL Experience Manager] 6.5. | S/O |

## Problèmes connus{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST.
 -->
<!-- REMOVED AS PER CQDOC-20022, JANUARY 23, 2023 * If you install [!DNL Experience Manager] 6.5 Service Pack 10 or a previous service pack on [!DNL Experience Manager] 6.5, the runtime copy of your assets custom workflow model (created in `/var/workflow/models/dam`) is deleted.
To retrieve your runtime copy, Adobe recommends to synchronize the design-time copy of the custom workflow model with its runtime copy using the HTTP API:
`<designModelPath>/jcr:content.generate.json`. -->

* Mettez à jour vos requêtes GraphQL qui peuvent avoir utilisé un nom d’API personnalisé pour votre modèle de contenu afin d’utiliser plutôt le nom par défaut du modèle de contenu.

* Une requête GraphQL peut utiliser la variable `damAssetLucene` plutôt que l’index `fragments` index. Cette action peut entraîner l’échec des requêtes GraphQL ou un long délai d’exécution.

   Pour résoudre le problème, `damAssetLucene` doit être configuré pour inclure les deux propriétés suivantes :

   * `contentFragment`
   * `model`

   Une fois la définition d’index modifiée, une réindexation est requise (`reindex` = `true`).

   Après ces étapes, les requêtes GraphQL doivent être plus rapides.

* [!DNL Microsoft® Windows Server 2019] ne prend pas en charge [!DNL MySQL 5.7] et [!DNL JBoss® EAP 7.1], [!DNL Microsoft® Windows Server 2019] ne prend donc pas en charge les installations clé en main pour [!DNL AEM Forms 6.5.10.0].

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

* Lorsque vous tentez de déplacer, supprimer ou publier des fragments de contenu, des sites ou des pages, un problème se produit lorsque les références aux fragments de contenu sont récupérées, car la requête en arrière-plan échoue. En d’autres termes, la fonctionnalité ne fonctionne pas.
Pour garantir le bon fonctionnement de cette opération, vous devez ajouter les propriétés suivantes au nœud de définition d’index `/oak:index/damAssetLucene` (aucune réindexation n’est requise) :

   ```xml
   "tags": [
       "visualSimilaritySearch"
     ]
   "refresh": true
   ```

* Dans AEM Forms, le protocole POP3 ne fonctionne pas avec les points d’entrée d’e-mail pour Microsoft® Office 365.
* Sur la plateforme JBoss® 7.1.4, lorsque l’utilisateur installe AEM Service Pack 6.5.16.0, `adobe-livecycle-jboss.ear` échec du déploiement.

## Bundles OSGi et modules de contenu inclus{#osgi-bundles-and-content-packages-included}

Les documents texte suivants répertorient les bundles OSGi et les modules de contenu inclus dans [!DNL Experience Manager] 6.5.17.0 : <!-- UPDATE FOR EACH NEW RELEASE -->

* [Liste des bundles OSGi inclus dans Experience Manager 6.5.17.0](/help/release-notes/assets/65170_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Liste des modules de contenu inclus dans Experience Manager 6.5.17.0](/help/release-notes/assets/65170_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Sites web à accès limité{#restricted-sites}

Ces sites Web sont disponibles uniquement pour les clients. Si vous êtes client et avez besoin d’un accès, contactez votre responsable de compte Adobe.

* [Téléchargement du produit à l’adresse licensing.adobe.com](https://licensing.adobe.com/)
* [Contacter l’assistance clientèle Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=fr).

>[!MORELIKETHIS]
>
>* Page des produits [[!DNL Experience Manager] ](https://business.adobe.com/fr/products/experience-manager/adobe-experience-manager.html)
>* Documentation [[!DNL Experience Manager]  6.5](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=fr)
>* [Abonnement aux mises à jour prioritaires de produits d’Adobe](https://www.adobe.com/subscription/priority-product-update.html)

