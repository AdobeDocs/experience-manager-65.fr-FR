---
title: Notes de mise à jour de la version 6.5 d’ [!DNL Adobe Experience Manager]
description: Consultez les informations sur la mise à jour, y compris les nouveautés, la procédure d’installation et une liste complète des modifications pour [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: 6bf2d6409a15be02a247fab84caa743e8542da13
workflow-type: tm+mt
source-wordcount: '3032'
ht-degree: 74%

---

# Notes de mise à jour du dernier pack de services [!DNL Adobe Experience Manager] 6.5 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in this release information, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!-- DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, November 30, 2023. In addition, a list of Forms fixes and enhancements is added to this section. -->

## Informations sur la version {#release-information}

| Produit | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Version | 6.5.21.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Type | Mise à jour du pack de services |
| Date | Jeudi 6 juin 2024 <!-- UPDATE FOR EACH NEW RELEASE --> |
| URL de téléchargement | [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.21.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## Éléments compris dans [!DNL Experience Manager] 6.5.21.0 {#what-is-included-in-aem-6521}

[!DNL Experience Manager] 6.5.21.0 comprend de nouvelles fonctionnalités, des améliorations importantes demandées par les clients et des correctifs. Elle comprend également des améliorations en termes de performances, de stabilité et de sécurité, publiées depuis la mise à disposition initiale de la version 6.5 en avril 2019. [Installez ce pack de services](#install) pour [!DNL Experience Manager] 6.5.

<!-- UPDATE FOR EACH NEW RELEASE -->

## Principales fonctionnalités et améliorations

<!-- * _6.5.21.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

Voici quelques-unes des fonctionnalités et améliorations clés de cette version :

* Un nouvel identifiant plus facile à utiliser pour l’authentification de serveur à serveur, remplaçant l’identifiant de compte de service (JWT) existant. (NPR-41994)

### [!DNL Assets]

#### Améliorations

Voici la liste des améliorations incluses dans cette version :

* L’onglet IPTC prend désormais en charge [!UICONTROL Texte de remplacement] et [!UICONTROL Description étendue] des champs de texte. (ASSETS-34918)

#### Correctifs d’accessibilité

Voici la liste des correctifs d’accessibilité inclus dans cette version :

* Si l’état de traitement d’une ressource est Échec ou Échec des métadonnées, l’interface utilisateur des sous-titres et du suivi audio ne fonctionne pas correctement. (ASSETS-37281)
* Lorsque vous enregistrez des métadonnées de ressource et tentez de les modifier, le nom de la langue ne s’affiche pas. (ASSETS-37281)

<!-- ### [!DNL Forms]
* A -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## Problèmes corrigés dans le pack de services 21 {#fixed-issues}

### [!DNL Sites]{#sites-6521}

#### Accessibilité {#sites-accessibility-6521}

* Le libellé **[!UICONTROL Recherches enregistrées]** n’est pas persistant. L’espace réservé est utilisé comme unique libellé visuel pour un champ de texte. (SITES-3050)

#### Interface utilisateur d’administration{#sites-adminui-6521}

* Quand vous cliquez sur **[!UICONTROL Sites]** > **[!UICONTROL Composants principaux]** > **[!UICONTROL Propriétés]** > onglet **[!UICONTROL Autorisations]** > **[!UICONTROL Autorisations en vigueur]**, la boîte de dialogue **Autorisations en vigueur** ne s’ouvre pas. (SITES-17378)

<!-- #### Classic UI{#sites-classicui-6521} 

* A -->

#### [!DNL Content Fragments]{#sites-contentfragments-6521}

* Correction de la double inclusion des éléments du formulaire. (SITES-21109)
* Lors de la création d’un fragment de contenu, il arrive que le bouton Fermer ne réponde plus, ce qui provoque un blocage de la page entière et nécessite une actualisation de la page pour fermer le fragment de contenu. En ce qui concerne le problème de création de version, le système crée une nouvelle version d’un fragment de contenu. Ce problème survient même lorsque l’utilisateur n’a apporté aucune modification, simplement en interagissant avec l’éditeur de texte enrichi ou avec un champ de texte. (SITES-21187)

#### [!DNL Content Fragments] - API GraphQL {#sites-graphql-api-6521}

* Lors de la mise à niveau d’Adobe Experience Manager de la version 6.5.19.0 vers la version 6.5.20.0, le chemin `/libs/cq/graphql/sites/graphiql` était supprimé. (SITES-20098)

<!-- #### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6521}

* W -->

<!-- #### [!DNL Content Fragments] - REST API{#sites-restapi-6521}

* W -->

<!-- #### Core Backend{#sites-core-backend-6521}

* W -->

<!-- #### Core Components{#sites-core-components-6521}

* I -->

<!-- #### Campaign integration{#sites-campaign-integration-6521}

* A -->

#### Fragments d’expérience{#sites-experiencefragments-6521}

* Le déploiement de fragments d’expérience de `masters/language` vers `country/language` ne met pas à jour les références croisées. (SITES-21172)
* Les modèles qui ne sont pas seulement spécifiés dans `cq:allowedTemplates`, mais qui ont le paramètre `allowedPaths` configuré au niveau du modèle, apparaissent comme des options lors de la création d’un fragment d’expérience. (SITES-20855)

<!-- #### Foundation Components (Legacy){#sites-foundation-components-legacy-6521}

* T -->

<!-- #### Launches{#sites-launches-6521} -->

<!-- DELETED MAY 22, 2024 FROM TOTAL RELEASE CANDIDATE ISSUES * The `sourceRootResource` configured in the Launch configuration within CRXDE Lite points to content that no longer exists, leading to a malfunction when attempts are made to delete launches. Delete launches even if the page is deleted or if the path is not the same. (SITES-20750) -->

#### MSM - Live Copies{#sites-msm-live-copies-6521}

* Recouvrement du composant Page pour ajouter des onglets dans les propriétés de page. L’un d’eux est la configuration de la page et possède une propriété permettant d’ajouter une URL de fragment d’expérience. Le lien configuré dans les propriétés de la page pour le fragment d’expérience ne change pas pour toute copie de langue créée pour cette page. Le lien configuré doit changer suivant l’URL de la copie de langue. (SITES-19580)

#### Éditeur de page{#sites-pageeditor-6521}

* Le mode d’édition applique un arrière-plan gris de manière irrégulière, qui ne respecte pas les normes WCAG de contraste des couleurs (normes pour l’accessibilité des contenus web). (SITES-20060)

### [!DNL Assets]{#assets-6521}

* Si une ressource est publiée sur Brand Portal, son état de publication reste incohérent. (ASSETS-36807)
* Les ressources ne sont pas supprimées lorsque vous les supprimez d’une instance à l’aide d’un appel API. (ASSETS-35131)
* Lorsque vous essayez d’importer des métadonnées, une `question mark (?)` remplace l&#39;insertion de caractères dans une autre langue que l&#39;anglais.  (ASSETS-35091)
* When `dc:title` est utilisée avec une chaîne de type de données, l’arborescence de contenu des ressources ne fonctionne pas correctement après l’installation du Service Pack 6.5.19. (ASSETS-34684)
* Une erreur s’affiche si le nom d’une ressource contient un caractère spécial. (ASSETS-33248)

#### [!DNL Dynamic Media]{#assets-dm-6521}

* Dans AEM version 6.5.18, toutes les zones réactives ajoutées à une ressource ne s’affichent pas lorsque vous modifiez les zones réactives. Cependant, toutes les zones réactives fonctionnent dans une ressource publiée, mais vous ne pouvez pas les modifier ultérieurement si nécessaire. (ASSETS-33609)
* Les derniers fichiers EPS chargés ne génèrent pas de miniatures après retraitement. (ASSETS-32617)
* Dans l’onglet Outils > Ressources > Configuration de la publication Dynamic Media > Attributs de requête, les entrées `Width(px)` et `Height(px)` en espagnol, en italien et en portugais. Ils ne sont pas alignés les uns avec les autres pour ces emplacements. (ASSETS-31896)
* À compter du 1er mai 2024, Adobe Dynamic Media a mis fin à la prise en charge des éléments suivants :
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

Les correctifs dans [!DNL Experience Manager] Forms sont fournis par le biais d’un package complémentaire distinct une semaine après la date de publication prévue du pack de services [!DNL Experience Manager]. Dans ce cas, la publication du package complémentaire AEM 6.5.21.0 Forms est planifiée pour le vendredi 13 juin 2024. Une liste des correctifs et améliorations de Forms est ajoutée à cette section après cette publication.

<!-- #### [!DNL Adaptive Forms]

* THIS BUG WAS ALREADY REPORTED IN THE 6.5.20.0 RELEASE NOTES. IS IT NEEDED AGAIN IN THE 6.5.21.0 RELEASE NOTES? (AEM Forms on JEE Only) The PDF Generator service fails to enumerate the fonts available on the server. Consequently, the font selection panel on the Adobe PDF Settings page in the PDFG Admin UI remains empty, effectively preventing (un)embedding of chosen fonts. (FORMS-12095) -->


<!-- #### [!DNL Forms Designer] {#forms-designer-6521}

* W -->

### Foundation {#foundation-6521}

#### Apache Felix {#foundation-apachefelix-6521}

* Problème de mise à niveau avec AEM 6.5 Service Pack 19 (SP19) dans lequel le chemin racine du contexte du serveur d’applications est absent pour les demandes non autorisées vers Apache Felix suite à l’installation de SP19. Mise à jour vers la console de gestion web Apache Felix 4.9.8. (NPR-41933)

#### Campaign{#foundation-campaign-6521}

* Le pack de service 15 d’AEM 6.5 produit des journaux d’erreurs continus avec des entrées majeures. Les problèmes suivants ont été signalés :

   * Erreur 404 (INFO) pour une ressource manquante dans le chemin `/libs/granite/ui/content/shell/start.html`.
   * Entrée dans le journal d’erreurs pour une SlingException non interceptée en raison d’une `NullPointerException` dans `CampaignsDataSourceServlet.java:147`.

  Les journaux d’erreurs ne doivent pas être remplis d’entrées d’erreurs fréquentes et volumineuses, et l’instance AEM doit fonctionner sans problèmes liés à des ressources manquantes ou à des exceptions. (CQ-4357064)

#### Services cloud{#foundation-cloudservices-6521}

* Supprimez Google Guava des Cloud Service AEM. (CQ-4356436)

<!-- #### Communities {#foundation-communities-6521}

* U -->

<!-- #### Content distribution{#foundation-content-distribution-6521}

* T -->

#### Granite{#foundation-granite-6521}

* Vous ne pouvez pas sélectionner **Supprimer** ou **Modifier** without **Parcourir** dans le navigateur Configuration. (GRANITE-51002)

#### Intégrations{#foundation-integrations-6521}

* Concernant `cq-target-integration`, il est nécessaire de retirer l’utilisation de Google Guava, excepté pour des tests. (CQ-4357101)
* Remplacement des informations d’identification du compte de service (JSON Web Token ou JWT) par les informations d’identification OAuth2 Server-to-Server (également appelées &quot;entités de service&quot;). (NPR-41994)
* La demande de création d’audience échoue avec une configuration IMS (système de gestion des identités). (NPR-41888)
* Lorsqu’un client ou une cliente tente de consulter la page Payload, le contenu ne s’affiche pas correctement en raison d’une URL mal formulée, et une erreur 404 s’affiche. Un symbole de point d’interrogation manquant dans l’URL, avant les paramètres de requête, provoquait l’erreur. Pour ce problème, le client doit insérer le symbole du point d’interrogation afin d’afficher correctement la page Payload. (NPR-41957)
* Supprimez le code et la dépendance d’Adobe Search &amp; Promote d’AEM 6.5, qui a atteint la fin de vie le [Septembre 2022 selon les avis](https://experienceleague.adobe.com/fr/docs/discontinued/using/search-promote). (NPR-41855)

#### Localisation{#foundation-localization-6521}

* Dans l’éditeur de modèles, la chaîne de texte *`No video available.`* n’est pas localisée. (SITES-13190)
* Les chaînes de caractères, après l’activation ou la désactivation d’un utilisateur ou d’une utilisatrice, ne sont pas localisées dans **Outils** > **Sécurité** > **Utilisateurs et utilisatrices** > *n’importe quel_nom_d’utilisateur_ou_utilisatrice* > **Activer** > **OK**, après la sélection de *n’importe quel_nom_d’utilisateur_ou_utilisatrice* > **Désactiver** > **OK**. (NPR-41737)

#### Plateforme{#foundation-platform-6521}

* L’erreur `Unclosed resource resolver` se produit pour `com.day.cq.mailer.impl.DefaultMailService`. La classe `MessageGatewayService`, prête à l’emploi, était utilisée sans résolveur de ressources. Le problème s’est produit sur n’importe quelle page avec un bouton d’envoi de formulaire qui envoie un courrier électronique à l’aide de cette classe. (NPR-41853)
* Dans le **À propos de Adobe Experience Manager** , l’année du copyright est toujours 2023. (CQ-4356349)


<!-- #### Sling{#foundation-sling-6521}

* T -->

#### Traduction{#foundation-translation-6521}

* Problème concernant le statut de la traduction prête à l’emploi d’AEM 6.5.19 qui ne se met pas à jour comme prévu pour un lancement. Après l’import d’un fichier traduit dans un traitement de traduction associé à un lancement AEM, le statut doit être modifié en `Approved`. Au lieu de cela, le statut devenait `Ready for Review`, ce qui n’est pas le comportement attendu. (NPR-41756)
* Lors de la création de plusieurs configurations et de l’accès aux configurations des services de traduction Cloud, certains éléments ne s’affichent pas dans l’interface d’utilisation. Seuls les 40 premiers éléments/dossiers s’affichent ; le chargement différé est déclenché mais n’ajoute pas de contenu supplémentaire. (NPR-41829)
* Des caractères altérés se produisent si la page Autorisations contient du japonais dans l’interface utilisateur tactile. (NPR-41794)
* AEM 6.5.14 et 6.5.9 n’envoient pas d’émoticône pour traduction. (CQ-4357000)

#### Interface utilisateur{#foundation-ui-6521}

* Dans Outils > Sécurité > Utilisateurs et utilisatrices > &lt;nom_utilisateur_ou_utilisatrice> > Profils, dans la boîte de dialogue **Modifier les paramètres de l’utilisateur ou de l’utilisatrice**, cliquer sur Annuler ne quitte pas la boîte de dialogue. (NPR-41793)
* Le composant Granite `pathfield` dans `/libs/granite/ui/components/coral/foundation/form/pathfield` ne parvient pas à activer le bouton **[!UICONTROL Sélectionner]** lorsqu’une ressource est sélectionnée. Une fois que le champ de chemin d’accès s’affiche et que l’utilisateur coche la case de la ressource, la variable **[!UICONTROL Sélectionner]** n’est pas activé ; il ne passe pas du gris au bleu. (NPR-41970)
* Il existe un problème avec le champ de référence du modèle de fragment de contenu dans AEM. Bien que le champ de référence du modèle de fragment de contenu soit défini comme obligatoire, le système permet aux utilisateurs et aux utilisatrices de cliquer sur Enregistrer pour enregistrer le contenu avec des valeurs non compatibles avec le modèle de fragment de contenu dans certains scénarios. Le bouton Enregistrer doit être grisé (inaccessible). (NPR-41894)
* Les boîtes de dialogue standard de l’interface d’utilisation de Coral qui utilisent l’action `successresponse` doivent déclencher une réponse de confirmation de réussite après l’action. Cependant, dans le pack de services 19 d’AEM 6.5, l’action de nouveau chargement n’est pas appelée et aucun message ne s’affiche. (NPR-41797)
* Les liens des notifications AEM ne fonctionnent pas dans le pack de services 18 d’AEM 6.5. Lors de la mise à niveau vers le pack de services 18, les liens des notifications AEM ne fonctionnent pas lors de la sélection de messages via le bouton des notifications. (NPR-41792)

<!-- #### WCM{#foundation-wcm-6521}

* T -->

#### Workflow{#foundation-workflow-6521}

* Dans AEM 6.5.18, des erreurs répétées se produisent lors de la suppression du cache des métadonnées des utilisateurs et des utilisatrices au cours d’une purge. (NPR-41762)

## Installer [!DNL Experience Manager] 6.5.21.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.21.0 nécessite [!DNL Experience Manager] 6.5. Consultez la [documentation de mise à niveau](/help/sites-deploying/upgrade.md) pour des instructions détaillées. <!-- UPDATE FOR EACH NEW RELEASE -->
* Le téléchargement du pack de services est disponible sur la [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.21.0.zip) d’Adobe.
* Lors d’un déploiement avec MongoDB et plusieurs instances, installez [!DNL Experience Manager] 6.5.21.0 sur l’une des instances de création à l’aide du gestionnaire de packages.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe ne recommande pas de supprimer ou de désinstaller le package [!DNL Experience Manager] 6.5.21.0. Par conséquent, avant d’installer le package, vous devez créer une sauvegarde du `crx-repository` au cas où vous auriez besoin de le restaurer. <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### Installer le pack de services dans [!DNL Experience Manager] 6.5{#install-service-pack}

1. Redémarrez l’instance avant l’installation si l’instance est en mode de mise à jour (lorsque l’instance a été mise à jour à partir d’une version antérieure). Adobe recommande un redémarrage si le temps de disponibilité actuel d’une instance est élevé.

1. Avant l’installation, prenez un instantané ou exécutez une sauvegarde récente de votre instance [!DNL Experience Manager].

1. Téléchargez le pack de services à partir de la [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.21.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Ouvrez le gestionnaire de modules et cliquez sur **[!UICONTROL Charger le module]** pour charger le module. Pour en savoir plus, consultez la section [Gestionnaire de modules](/help/sites-administering/package-manager.md).

1. Sélectionnez le module, puis sélectionnez **[!UICONTROL Installer]**.

1. Pour mettre à jour le connecteur S3, arrêtez l’instance après l’installation du pack de services, remplacez le connecteur existant par un nouveau fichier binaire fourni dans le dossier d’installation, puis redémarrez l’instance. Consultez la section [Entrepôt de données S3 Amazon](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>La boîte de dialogue de l’interface d’utilisation du gestionnaire de packages se ferme occasionnellement pendant l’installation du pack de services. Adobe recommande d’attendre que les journaux d’erreurs se stabilisent avant d’accéder au déploiement. Attendez les journaux spécifiques liés à la désinstallation de la mise à jour complète pour vous assurer que l’installation est réussie. En règle générale, ce problème se produit dans la variable [!DNL Safari] mais peut se produire par intermittence dans n’importe quel navigateur.

**Installation automatique**

Vous pouvez utiliser deux méthodes différentes pour installer [!DNL Experience Manager] 6.5.21.0.<!-- UPDATE FOR EACH NEW RELEASE -->

* Placez le package dans le dossier `../crx-quickstart/install` lorsque le serveur est disponible en ligne. Le package est automatiquement installé.
* Utilisez l’[API HTTP à partir du gestionnaire de packages](/help/sites-administering/package-manager.md#package-share). Utilisez `cmd=install&recursive=true` afin que les packages imbriqués soient installés.

>[!NOTE]
>
>Experience Manager 6.5.21.0 ne prend pas en charge l’installation en Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Validation de l’installation**

Pour connaître les plateformes certifiées pour travailler avec cette version, reportez-vous à la section des [exigences techniques](/help/sites-deploying/technical-requirements.md).

1. La page d’informations sur les produits (`/system/console/productinfo`) affiche le numéro de version mis à jour `Adobe Experience Manager (6.5.21.0)` sous [!UICONTROL Produits installés]. <!-- UPDATE FOR EACH NEW RELEASE -->.

1. Tous les bundles OSGi sont au statut **[!UICONTROL ACTIF]** ou **[!UICONTROL FRAGMENT]** dans la console OSGi (utilisez la console web : `/system/console/bundles`).

1. Le lot OSGi `org.apache.jackrabbit.oak-core` est version 1.22.20 ou ultérieure (Utiliser la console web : `/system/console/bundles`). <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### Installer le pack de services pour [!DNL Experience Manager] Forms{#install-aem-forms-add-on-package}

Pour obtenir des instructions sur l’installation du pack de services pour Experience Manager Forms, consultez les [instructions d’installation du pack de services Experience Manager Forms](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

>[!NOTE]
>
>La fonctionnalité de formulaires adaptatifs, disponible dans [AEM 6.5 QuickStart](https://experienceleague.adobe.com/fr/docs/experience-manager-65/content/implementing/deploying/deploying/deploy), est conçue à des fins d’exploration et d’évaluation uniquement. Pour une utilisation à des fins de production, il est essentiel d’obtenir une licence valide pour AEM Forms, car la fonctionnalité de formulaires adaptatifs nécessite une licence appropriée.

### Installer le package d’index GraphQL pour les fragments de contenu d’Experience Manager{#install-aem-graphql-index-add-on-package}

La clientèle qui utilise GraphQL doit installer le [fragment de contenu d’Experience Manager avec le package d’index GraphQL 1.1.1](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip).

Vous pouvez ainsi ajouter la définition d’index requise selon les fonctionnalités que vous utilisez réellement.

L’échec de l’installation de ce package peut entraîner des requêtes GraphQL lentes ou en échec.

>[!NOTE]
>
>N’installez ce package qu’une seule fois par instance ; il n’est pas nécessaire de le réinstaller avec chaque Pack de services.

### UberJar{#uber-jar}

UberJar pour [!DNL Experience Manager] 6.5.21.0 est disponible dans le [référentiel central Maven](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.21/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

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

* Lorsque vous tentez de déplacer, de supprimer ou de publier des fragments de contenu, des sites ou des pages, un problème se produit lorsque les références aux fragments de contenu sont récupérées. La requête en arrière-plan échoue. En d’autres termes, la fonctionnalité ne fonctionne pas.
Pour garantir le bon fonctionnement de cette opération, vous devez ajouter les propriétés suivantes au nœud de définition d’index `/oak:index/damAssetLucene` (aucune réindexation n’est requise) :

  ```xml
  "tags": [
      "visualSimilaritySearch"
    ]
  "refresh": true
  ```

* Si vous mettez à niveau votre instance [!DNL Experience Manager] de la version 6.5.0 - 6.5.4 au pack de services le plus récent sur Java™ 11, des exceptions `RRD4JReporter` s’affichent dans le fichier `error.log`. Pour arrêter les exceptions, redémarrez votre instance d’[!DNL Experience Manager]. <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* Les utilisateurs peuvent renommer un dossier dans une hiérarchie dans [!DNL Assets] et publier un dossier imbriqué dans [!DNL Brand Portal]. Toutefois, le titre du dossier n’est pas mis à jour dans [!DNL Brand Portal] jusqu’à ce que le dossier racine soit republié.

* Les erreurs et messages d’avertissement suivants peuvent s’afficher lors de l’installation d’[!DNL Experience Manager] 6.5.x.x :
   * « Lorsque l’intégration d’Adobe Target est configurée dans [!DNL Experience Manager] à l’aide de l’API Target Standard (authentification IMS), l’exportation de fragments d’expérience vers Target entraîne la création de types d’offres incorrects. » Au lieu du type « Fragment d’expérience » / source « Adobe Experience Manager », Target crée plusieurs offres avec le type « HTML » / source « Adobe Target Classic ».
   * `com.adobe.granite.maintenance.impl.TaskScheduler` : aucune fenêtre de maintenance n’a été trouvée sur granite/operations/maintenance.
   * La validation côté serveur du formulaire adaptatif échoue lorsque des fonctions d’agrégat telles que SUM, MAX et MIN sont utilisées (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` : aucune fenêtre de maintenance n’a été trouvée sur granite/operations/maintenance.
   * La zone réactive d’une image interactive de Dynamic Media n’est pas visible lors de la prévisualisation du fichier via la visionneuse de bannières avec achat.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : temporisation en attente de modification d’enregistrement pour terminer la désinscription.

* À partir de la version 6.5.15 d’AEM, le moteur JavaScript Rhino fourni par le lot ```org.apache.servicemix.bundles.rhino``` a un nouveau comportement d’hébergement. Scripts qui utilisent le mode strict (```use strict;```) doivent déclarer leurs variables correctes. Dans le cas contraire, elles ne sont pas exécutées et finissent par générer une erreur d’exécution.

* L’installation du balisage du contenu d’usine par le biais d’un package de mise à jour officiel réinitialise la propriété languages du `/content/cq:tags` par défaut. Cette action est vraie pour les Service Packs, les Service Packs de sécurité, les Feature Packs étendus, les Cumulative Feature Packs, les correctifs, etc. Il est donc nécessaire de l’ajouter à partir des propriétés avant l’installation.

### Problème connu pour AEM Sites {#known-issues-aem-sites-6521}

* SITES-17934 - Fragments de contenu - La prévisualisation échoue en raison de la protection DoS pour une grande arborescence de fragments. Voir l’[article de la base de connaissances sur les options de configuration par défaut de l’exécuteur de requêtes GraphQL](https://experienceleague.adobe.com/fr/docs/experience-cloud-kcs/kbarticles/ka-23945).

### Problèmes connus d’AEM Forms {#known-issues-aem-forms-6521}

* Dans un formulaire adaptatif basé sur un XDP avec des scripts intégrés sur des cases à cocher, les scripts ne sont pas exécutés pour les éléments après ces cases à cocher. (FORMS-14244)
* Il est alors impossible de créer une lettre Correspondence Management. Quand un utilisateur ou une utilisatrice crée une lettre, une erreur avec la description « `Object Object` » s’affiche et la lettre n’est pas créée. Les miniatures des dispositions ne se chargent pas non plus sur l’écran de création de lettre. Vous pouvez installer le [dernier pack de services 20 (6.5.20.0) d’AEM Forms (6.5)](https://experienceleague.adobe.com/fr/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases) pour résoudre le problème. (FORMS-13496)
* Le service de communications interactives crée le document du PDF, mais les données de l’utilisateur ne sont pas automatiquement renseignées dans les champs de formulaire. Le service de préremplissage ne fonctionne pas comme prévu. Vous pouvez installer le [dernier pack de services 20 (6.5.20.0) d’AEM Forms 6.5](https://experienceleague.adobe.com/fr/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases) pour résoudre le problème. (FORMS-13413, FORMS-13493)
* Le chargement de l’éditeur de vérification et de correction (RnC) d’un service automated forms conversion échoue. Vous pouvez installer le [dernier pack de services 20 (6.5.20.0) d’AEM Forms 6.5](https://experienceleague.adobe.com/fr/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases) pour résoudre le problème. (FORMS-13491)
* Après la mise à jour pack de services 18 (6.5.18.0) ou 19 (6.5.19.0) d’AEM Forms 6.5 vers le pack de services 20 (6.5.20.0) d’AEM Forms 6.5, une erreur de compilation JSP se produit. Il est impossible d’ouvrir ou de créer des formulaires adaptatifs et des erreurs se produisent avec d’autres interfaces d’AEM telles que l’éditeur de page, l’interface d’utilisation d’AEM Forms et l’éditeur de workflow d’AEM. Vous pouvez installer le [dernier pack de services 6.5.20.0 d’AEM Forms 6.5](https://experienceleague.adobe.com/fr/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases) pour résoudre le problème. (FORMS-13492)
* Les lignes du widget du sélecteur de date sont tronquées lors du parcours de plusieurs mois dans le widget de pop-up pour les champs suivant le modèle d’édition/d’affichage. (FORMS-13620)
* Les envois de formulaire échouent lors de la tentative d’utilisation du service DOR (Document d’enregistrement) dans le serveur principal. Le message d’erreur rencontré est : « L’action Envoyer n’a pas pu se terminer, car la ressource de formulaire n’a pas été correctement affectée. » (FORMS-13798)
* Lorsqu’un formulaire adaptatif est envoyé d’une instance de publication Adobe Experience Manager vers un workflow Adobe Experience Manager, le workflow ne parvient pas à enregistrer les pièces jointes. (FORMS-14209)
* Lors de l’installation du package Forms Service Pack 20 d’AEM 6.5 (package de module complémentaire AEM Forms pour SP20), l’interface utilisateur d’AEM Sites présente une dégradation significative des performances. (FORMS-13791)
* Le service de préremplissage échoue avec une exception de pointeur nulle dans les communications interactives. (CQDOC-21355)
* Le Forms adaptatif vous permet d’utiliser des fonctions personnalisées avec ECMAScript version 5 ou antérieure. Lorsqu’une fonction personnalisée utilise ECMAScript version 6 ou ultérieure, comme `let`, `const`ou fonctions de flèche, l’éditeur de règles peut ne pas s’ouvrir correctement.

## Lots OSGi et packages de contenu inclus{#osgi-bundles-and-content-packages-included}

Les documents texte suivants répertorient les lots OSGi et les packages de contenu inclus dans cette version du pack de services [!DNL Experience Manager] 6.5.

* [Liste des lots OSGi inclus dans Experience Manager 6.5.21.0](/help/release-notes/assets/65210-bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Liste des packages de contenu inclus dans Experience Manager 6.5.21.0](/help/release-notes/assets/65210-packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Sites web à accès limité{#restricted-sites}

Ces sites Web sont disponibles uniquement pour les clients. Si vous êtes client et avez besoin d’un accès, contactez votre responsable de compte Adobe.

* [Téléchargement du produit à l’adresse licensing.adobe.com](https://licensing.adobe.com/)
* [Contacter l’assistance clientèle Adobe](https://experienceleague.adobe.com/fr/docs/customer-one/using/home).

>[!MORELIKETHIS]
>
>* Page des produits [[!DNL Experience Manager] ](https://business.adobe.com/fr/products/experience-manager/adobe-experience-manager.html)
>* Documentation [[!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/fr/docs/experience-manager-65)
>* [Abonnez-vous aux mises à jour de produit Adobe Priority](https://www.adobe.com/subscription/priority-product-update.html)

