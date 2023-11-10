---
title: Notes de mise à jour de la version 6.5 d’ [!DNL Adobe Experience Manager]
description: Consultez les informations sur la mise à jour, y compris les nouveautés, la procédure d’installation et une liste complète des modifications pour  [!DNL Adobe Experience Manager]  6.5.
mini-toc-levels: 4
source-git-commit: 6f45b0f8dad44e66570f6436a560060cbed56161
workflow-type: tm+mt
source-wordcount: '3432'
ht-degree: 48%

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
| Version | 6.5.19.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Type | Mise à jour du pack de services |
| Date | jeudi 23 novembre 2023 <!-- UPDATE FOR EACH NEW RELEASE --> |
| URL de téléchargement | [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.18.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## Éléments compris dans [!DNL Experience Manager] 6.5.19.0 {#what-is-included-in-aem-6519}

[!DNL Experience Manager] 6.5.19.0 comprend de nouvelles fonctionnalités, des améliorations importantes demandées par les clientes et les clients, des correctifs de bugs ainsi que des améliorations en termes de performances, de stabilité et de sécurité, publiées depuis la version initiale 6.5 en avril 2019. [Installez ce pack de services](#install) dans [!DNL Experience Manager] 6.5.

<!-- UPDATE FOR EACH NEW RELEASE -->

<!-- Some of the key features and improvements are the following:

* _REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

Voici quelques-unes des fonctionnalités et améliorations clés de cette version :

**Fonctions clés**

* A

**Améliorations clés**

* S

**Fonctionnalité obsolète**

* ActiveMQ dans AEM est obsolète. ActiveMQ a été utilisé pour la communication entre deux instances de publication AEM. Adobe recommande aux clientes et clients d’utiliser désormais un équilibreur de charge.

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## Correction de problèmes dans le pack de services 19 {#fixed-issues}

### [!DNL Sites]{#sites-6519}

* U

#### Accessibilité{#sites-accessibility-6519}

* Sur une page AEM Sites, lorsque vous effectuez un zoom avant de 200 %, les liens **[!UICONTROL Copie de la langue]** et **[!UICONTROL Rapport CSV]** dans le rail Références. (SITES-11011) NORMAL

#### Interface utilisateur d’administration{#sites-adminui-6519}

* Canal AEM Screens **[!UICONTROL Aperçu]** ne fonctionne pas ou ne s’affiche pas dans le tableau de bord. (SITES-15730) CRITIQUE
* Lors d’une opération de déplacement de page, si l’interface utilisateur ne peut pas afficher les références, mais indique qu’elles sont automatiquement republiées, elles le sont. *not* republiée. (SITES-16435) MAJOR
* Dans AEM 6.5 avec Service Pack 16 ou 17, lorsque la vue Liste des sites pour lesquels la colonne &quot;Workflow&quot; est activée est activée, vous ne pouvez pas trier la liste en fonction des éléments de cette colonne. Aucun tri n’est effectué. (SITES-15385) MAJOR
* Pour un modèle de page de redirection, le champ de redirection est devenu obligatoire. Cependant, la validation du champ requis n’est pas appliquée ni ne fonctionne dans ces deux scénarios : lorsqu’une page est créée sans valeur de redirection obligatoire ; ne peut pas créer de page de redirection. La validation ne fonctionne pas lors de la navigation à l’aide de raccourcis clavier. Lorsque le champ est marqué comme non valide, il ne se poursuit pas. (SITES-15903) NORMAL
* Certains **Liens entrants** n’étaient pas inclus dans le nombre affiché dans la variable **Références** du panneau. Par exemple, le panneau affichait **Liens entrants (6)** mais il y avait en fait neuf liens entrants. (SITES-14816) NORMAL

#### Interface utilisateur classique{#sites-classicui-6519}

* Après l’installation du correctif dans SITES-15827, les titres des boîtes de dialogue qui avaient un espace entre les mots étaient remplacés par `" "`. Les sauts de ligne étaient également supprimés. (SITES-16089) MAJOR
* Les titres des boîtes de dialogue codées entraînent désormais un double codage du titre. (SITES-15841) NORMAL
* La mise à jour des serveurs AEM du Service Pack 6.5.16 vers 6.5.17 entraînait un double codage des titres des boîtes de dialogue de l’interface utilisateur classique. (SITES-15634) NORMAL

#### [!DNL Content Fragments]{#sites-contentfragments-6519}

* Un message d’erreur de serveur interne s’affiche dans l’éditeur de fragments de contenu. (SITES-13550) CRITIQUE
* La mise à jour du `org.json` par le biais de NPR-41291 provoquait des conversions d’erreurs de données dans la variable `DefaultDataTypeConverter` de `cfm-impl` du lot. La conversion du type de données doit être plus flexible. (SITES-16473) NORMAL
* Obtention du message d’erreur contextuel, &quot;Cette version de fragment de contenu ne peut pas être comparée à la version actuelle en raison d’un contenu incompatible.&quot; Les fragments de contenu doivent être comparables, mais ce n’est pas le cas. (SITES-16317) NORMAL
* Modification de l’URL JS du sélecteur de ressources
  `https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/assets-selectors.js`vers .
  `https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/assets-selectors.js` (SITES-16068) NORMAL
* Adaptez le nouveau schéma de réponse de l’API de métadonnées Polaris à l’intégration CFM-Polaris. (SITES-15166) NORMAL
* Tous les fragments de contenu doivent être répertoriés là où le fragment de contenu sélectionné est référencé. Au lieu de cela, les références de ressources dans le panneau de référence des fragments de contenu affichent 0 (zéro) référence. (SITES-15036) NORMAL

#### Core Backend{#sites-core-backend-6519}

* Améliorer `StyleImpl`. (SITES-15164) NORMAL

<!--#### Core Components{#sites-core-components-6519}

* A -->

#### Intégration de Campaign{#sites-campaign-integration-6519}

* Sur le composant de signature (`/apps/fpl/components/campaign/signature`), l’externaliseur de liens ne fonctionnait pas. Le domaine n’était pas annexé à la source de l’image, si le commentaire de HTML situé au-dessus de la balise de l’image était supprimé. Ce problème a été détecté uniquement avec le composant de signature dans l’environnement de production, et non dans l’environnement d’évaluation. (SITES-16120) NORMAL

<!--#### Experience Fragments{#sites-experiencefragments-6519}

* A -->

#### Composants de base (hérités){#sites-foundation-components-legacy-6519}

* Le composant Recherche de sites Adobe Experience Manager (AEM) rompt l’interface utilisateur. (SITES-15087) NORMAL

#### Éditeur de requête GraphQL{#sites-graphql-query-editor-6519}

* L’interface utilisateur de l’éditeur de GraphQL ne vous permet pas de parcourir toutes les requêtes conservées lorsqu’il y a un nombre élevé de requêtes (plus de 25, par exemple). (SITES-16008) MAJOR
* L’éditeur GraphQL n’enregistre pas l’état de publication des requêtes persistantes. Le bouton Annuler la publication s’affiche dans l’éditeur de GraphQL, mais l’icône indiquant que la requête persistante est publiée n’apparaît pas. L’actualisation de la page affiche que la requête conservée n’est même pas publiée. (SITES-15858) MAJOR

#### Lancements{#sites-launches-6519}

* Les modifications du référentiel ne sont pas enregistrées en raison de `Oak0001` conflits lorsque plusieurs pages sont en cours de modification ou que du contenu est en cours de création. Il est normal d’effectuer une nouvelle tentative dans un tel événement, mais cela ne se produit pas. (SITES-14840) MAJOR

#### MSM - Live Copies{#sites-msm-live-copies-6519}

* Le bouton Déploiement MSM ne fonctionne pas dans l’interface utilisateur graphique tactile. (SITES-16991) MAJOR
* La référence de lien n’est pas mise à jour dans le fragment d’expérience lors de la création d’une Live Copy ou du déploiement d’un fragment d’expérience. (SITES-15460) NORMAL

#### Éditeur de page{#sites-pageeditor-6519}

* La sélection de plusieurs types de fichiers de document sur le filtre de type de ressource ne fonctionne pas sur la console de page. Aucun résultat n’est trouvé même si les résultats d’un type de fichier particulier sont disponibles. Par conséquent, les auteurs ne peuvent pas filtrer plusieurs documents. Ils doivent utiliser plusieurs types de documents et les filtrer un par un. (SITES-14047) MAJOR
* Après la mise à niveau d’une instance à partir d’AEM 6.5.17 et d’AEM 6.5.18, depuis l’éditeur de page, si vous sélectionnez **[!UICONTROL Publier la page]**, vous êtes redirigé vers une URL qui n’existe pas. L’utilisateur doit être redirigé vers l’assistant de publication. (SITES-15856) NORMAL
* (SITES-15704) NORMAL
* Copie redondante du Presse-papiers AEM lors d’un collage à partir du Presse-papiers du système d’exploitation. (SITES-15704) NORMAL
* Dans Assets, en sélectionnant **[!UICONTROL Documents]**, puis sous **[!UICONTROL Filtertype]**, sélection **[!UICONTROL Microsoft® Word]** ou **[!UICONTROL Microsoft® Excel]** n’affiche aucun résultat, même si des fichiers des deux types existent. (SITES-14837) NORMAL

### [!DNL Assets]{#assets-6519}

* Impossible de différencier les ressources de publication dans Experience Manager ou Brand Portal. [NPR-41320]
* Lorsque vous créez ou enregistrez un dossier public, trois groupes sont créés dans un tableau de bord d’administration. [ASSETS-26700]
* Dans le panneau de recherche, lorsque vous sélectionnez des cases à cocher et désélectionnez l’une d’elles, toutes les cases sont décochées. [ASSETS-26377]

#### [!DNL Dynamic Media]{#assets-dm-6519}

* Une fois qu’une ressource est chargée dans AEM, la variable `update_asset` le workflow est déclenché. Le workflow ne se termine jamais. En examinant les instances de workflow, le workflow se termine jusqu’à l’étape de chargement du produit. L’étape suivante est le téléchargement par lots de scene7. L’utilisateur peut constater que la ressource se trouve dans Scene7 à partir de l’application Dynamic Media Classic. (ASSETS-30443) CRITIQUE
* Un servlet personnalisé (point de terminaison de l’API) renvoie un nom de fichier Dynamic Media (Scene7) incorrect. Cela se produit lorsqu’une ressource est supprimée et remplacée par une ressource du même nom. Le servlet personnalisé renvoie l’ancien nom de fichier Dynamic Media (Scene7), tandis qu’un appel API &quot;jcr&quot; renvoie le nom de fichier correct. (ASSETS-29476) MAJOR
* Même après la désactivation de la synchronisation au niveau du dossier, les journaux affichent le déclencheur &quot;Scene7 ReplicateOnModifyListener&quot;. La variable `ReplicateOnModifyListener/Worker` doit ignorer le traitement des ressources de dossier et des fragments de contenu autres que Dynamic Media. (ASSETS-26705) MAJOR
* Les personnes malvoyantes sont affectées si le focus n’est pas visible dans les éléments de liste déroulante (Contenu uniquement, Affichage, Plus d’options) en modes noir et blanc à contraste élevé. (ASSETS-25759) NORMAL
* Les personnes à faible vision sont affectées si le rapport de contraste de luminosité du texte sur une page est inférieur à 4,5:1. (ASSETS-25756) NORMAL
* Les lecteurs d’écran ne narrent pas le message contextuel affiché après l’envoi des données. (ASSETS-25755) NORMAL
* Les lecteurs d’écran ne reconnaissent pas les repères dans la page (Dynamic Media ; création d’un profil de codage vidéo), lorsqu’ils sont navigués à l’aide de la touche de raccourci de repère/région. `D/R`. (ASSETS-25752) NORMAL
* Les lecteurs d’écran ne reconnaissent pas plusieurs points de repère dans la page (Dynamic Media ; création d’une vidéo interactive), lorsqu’ils sont navigués à l’aide de la touche de raccourci de repère/région. `D/R`. (ASSETS-25750) NORMAL
* Les lecteurs d’écran (NVDA/JAWS/Narrator) ne reconnaissent pas les repères dans **Modifier la ressource** lors de la navigation à l’aide des touches de raccourci `D/R`. (ASSETS-25744) NORMAL
* L’utilisateur obtient un message de tâche asynchrone vide/faux, mais la ressource connectée est publiée avec succès. (ASSETS-29342) TRIVIAL

### [!DNL Forms]{#forms-6519}

Correctifs de [!DNL Experience Manager] Forms est livré par le biais d’un module complémentaire distinct une semaine après la planification [!DNL Experience Manager] Date de publication du Service Pack. Dans ce cas, la publication du module complémentaire Forms AEM 6.5.19.0 est programmée pour le jeudi 30 novembre 2023. Une liste des correctifs et améliorations de Forms sera ajoutée à cette section après cette version.

* Ajout de la liste de contrôle d’accès pour `fd-cloudservice` pour pouvoir lire ou mettre à jour les configurations Microsoft® sous `cloudconfigs/microsoftoffice`. (FORMS-11142) NORMAL

<!--LEFT BULLET LIST HERE IN CASE OF REUSE BY FORMS IN THE FUTURE 
* **Document Services**
  * text
* **Adaptive Forms** 
  * text
* **Accessibility**
  * text
* **Interactive Communications**
  * text -->

<!--### Commerce{#commerce-6519}

* A -->

### Foundation{#foundation-6519}

* La création d’une copie de langue au niveau racine de la langue n’ajuste pas les chemins d’accès dans la page. Dans le cas où la copie de langue a été créée, pas pour la racine de langue, mais pour les pages qui la composent, le chemin d’accès a changé correctement. (NPR-41364) MAJOR
* L’info-bulle &quot;Présentation de la date relative&quot; ne peut être fermée qu’en appuyant sur Échap (ESC) sur le clavier. L’info-bulle doit se fermer lorsque l’utilisateur sélectionne une partie de l’interface utilisateur. (NPR-41394) NORMAL
* Chaîne non localisée `Something went wrong while adding the private key.` lors de l’ajout d’un fichier de clé privée incorrect dans **Modifier l’utilisateur** > **Keystore**. (NPR-41366) NORMAL
* Des icônes sont nécessaires pour Microsoft® SharePoint et Microsoft® One Drive dans l’environnement AEM 6.5. (NPR-41354) NORMAL
* Non localisé &quot;L’ID utilisateur/le mot de passe ne correspondent pas&quot;. chaîne dans **Sécurité** > **Utilisateur** > **Créer** de la boîte de dialogue (NPR-41245) NORMAL
* Le code de fenêtre contextuelle et les gestionnaires d’événements sont chargés deux fois, rompant les interfaces utilisateur créées par l’utilisateur à partir de Coral3. (NPR-41171) NORMAL
* La désélection ne fonctionne pas correctement après l’utilisation de &quot;Tout sélectionner&quot; dans la console AEM Sites. (NPR-41304) MINEUR

<!--#### Content distribution{#foundation-content-distribution-6519}

* T -->

#### Intégrations{#integrations-6519}

* Les liens SMS d’une campagne email AEM ne sont pas correctement écrits ; ils contiennent un élément d’ancre de HTML. (NPR-41211) MAJOR
* Les libellés utilisés sur l’écran de configuration du compte ne doivent pas utiliser de nouveau type d’informations d’identification. (NPR-41210) NORMAL
* Déplacement du planificateur d’importation de rapports Analytics depuis `ManagedPollConfig` aux tâches sling. Lorsque deux structures d’analyse différentes ont été associées à des suites de rapports différentes à deux sites différents, `ManagedPollConfig` les sondages n&#39;en font qu&#39;un. (NPR-41209) NORMAL
* Lorsque la valeur est réinitialisée sur la valeur par défaut, le bouton de période précédemment sélectionné reste activé. Dans le tableau de bord Content Insight d’AEM, la période est définie par défaut sur la semaine et affiche les informations sur le contenu sous forme de données hebdomadaires. Désormais, si l’utilisateur sélectionne d’autres options de période, telles que l’heure, le jour, le mois et l’année, les données changent en fonction de la valeur sélectionnée. Cependant, si les valeurs sont réinitialisées, par défaut, la période visible est la semaine, mais l’option de période précédemment sélectionnée est toujours sélectionnée. (NPR-41246) MINEUR

#### Oak{#oak-6519}

* Utilitaire de rétroportage permettant de comptabiliser les écritures de limite à AEM en cas de retard de l’indexation asynchrone. (NPR-40985) MAJOR

#### Platform{#foundation-platform-6519}

* Les requêtes QueryBuilder avec crochets sont incorrectement traduites en xpath . (NPR-41298) NORMAL

<!--#### Replication{#foundation-replication-6519}

* R -->

<!--#### Sling{#foundation-sling-6519}

* W -->

#### Projets de traduction{#foundation-translation-6519}

* Lors de la création de la copie de langue de la page &quot;A&quot;, elle doit automatiquement créer les copies de langue des pages, des fragments d’expérience, des fragments de contenu et des ressources référencés. En outre, la nouvelle copie de langue de la page &quot;A&quot; sur le nouveau chemin doit avoir ses références mises à jour aux nouvelles copies de langue respectives des pages, des fragments d’expérience, des fragments de contenu et des ressources. (NPR-41076) NORMAL

<!--#### User interface{#foundation-ui-6519}

* A -->

<!--#### WCM{#wcm-6519}

* A -->

#### Workflow{#foundation-workflow-6519}

* Impossible d’effectuer une tâche dans la boîte de réception. Seule une valeur &quot;non définie&quot; est observée dans le menu déroulant lorsque vous essayez d’effectuer la tâche et de sélectionner une action. Cela signifie que les utilisateurs ne peuvent pas appliquer le Service Pack AEM 6.5.18. (NPR-41402) MAJOR
* Impossible d’effectuer les tâches dans la boîte de réception. Il n’existe aucune valeur (uniquement &quot;non définie&quot;) dans la liste déroulante lorsque vous essayez d’exécuter la tâche pour les fichiers zip, les rapports de ressources, le déplacement (succès ou échec) ou l’expiration de la ressource. (NPR-41305) MAJOR
* Lorsqu’un utilisateur sélectionne **[!UICONTROL Outils]** > **[!UICONTROL Workflow]** > instances, puis sélectionne le workflow en cours d’exécution, puis sélectionnez **[!UICONTROL Afficher la charge utile]**, cela génère une page d’erreur 500. (NPR-41325) NORMAL


## Installer [!DNL Experience Manager] 6.5.18.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.19.0 nécessite [!DNL Experience Manager] 6.5. Consultez la [documentation de mise à niveau](/help/sites-deploying/upgrade.md) pour des instructions détaillées. <!-- UPDATE FOR EACH NEW RELEASE -->
* Le téléchargement du pack de services est disponible dans la [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.18.0.zip) d’Adobe.
* Lors d’un déploiement avec MongoDB et plusieurs instances, installez [!DNL Experience Manager] 6.5.19.0 sur l’une des instances de création à l’aide du gestionnaire de packages.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe ne recommande pas de supprimer ou de désinstaller le package [!DNL Experience Manager] 6.5.19.0. Par conséquent, avant d’installer le module, vous devez créer une sauvegarde du `crx-repository` au cas où vous auriez besoin de le restaurer. <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### Installation du pack de services sur [!DNL Experience Manager] 6.5{#install-service-pack}

1. Redémarrez l’instance avant l’installation si l’instance est en mode de mise à jour (lorsque l’instance a été mise à jour à partir d’une version antérieure). Adobe recommande un redémarrage si le temps de disponibilité actuel d’une instance est élevé.

1. Avant l’installation, prenez un instantané ou exécutez une sauvegarde récente de votre instance [!DNL Experience Manager].

1. Téléchargez le pack de services à partir de la [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.18.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Ouvrez le gestionnaire de modules et cliquez sur **[!UICONTROL Charger le module]** pour charger le module. Pour en savoir plus, consultez la section [Gestionnaire de modules](/help/sites-administering/package-manager.md).

1. Sélectionnez le module, puis sélectionnez **[!UICONTROL Installer]**.

1. Pour mettre à jour le connecteur S3, arrêtez l’instance après l’installation du pack de services, remplacez le connecteur existant par un nouveau fichier binaire fourni dans le dossier d’installation, puis redémarrez l’instance. Consultez la section [Entrepôt de données S3 Amazon](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>La boîte de dialogue de l’interface utilisateur du gestionnaire de packages se ferme parfois pendant l’installation du pack de services. Adobe recommande d’attendre que les journaux d’erreurs se stabilisent avant d’accéder au déploiement. Attendez les journaux spécifiques liés à la désinstallation de la mise à jour complète pour vous assurer que l’installation est réussie. En règle générale, ce problème se produit dans [!DNL Safari] mais peut se produire par intermittence sur n’importe quel navigateur.

**Installation automatique**

Vous pouvez utiliser deux méthodes différentes pour installer automatiquement [!DNL Experience Manager] 6.5.19.0.<!-- UPDATE FOR EACH NEW RELEASE -->

* Placez le package dans le dossier `../crx-quickstart/install` lorsque le serveur est disponible en ligne. Le package est automatiquement installé.
* Utilisez l’[API HTTP à partir du gestionnaire de packages](/help/sites-administering/package-manager.md#package-share). Utilisez `cmd=install&recursive=true` afin que les packages imbriqués soient installés.

>[!NOTE]
>
>Experience Manager 6.5.19.0 ne prend pas en charge l’installation en Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Validation de l’installation**

Pour connaître les plateformes certifiées pour travailler avec cette version, reportez-vous à la section des [exigences techniques](/help/sites-deploying/technical-requirements.md).

1. La page d’informations sur les produits (`/system/console/productinfo`) affiche la chaîne de version mise à jour `Adobe Experience Manager (6.5.19.0)` sous [!UICONTROL Produits installés]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. Tous les lots OSGi sont au statut **[!UICONTROL ACTIF]** ou **[!UICONTROL FRAGMENT]** dans la console OSGi (utilisez la console web : `/system/console/bundles`).

1. Le lot OSGi `org.apache.jackrabbit.oak-core` est de la version 1.22.16 ou ultérieure (utiliser la console web : `/system/console/bundles`). <!-- NPR-41010 for 6.5.18.0 --> <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### Installer le Pack de services pour [!DNL Experience Manager] Forms{#install-aem-forms-add-on-package}

Pour obtenir des instructions sur l’installation du Pack de services sur Experience Manager Forms, voir les [instructions d’installation du Pack de services Experience Manager Forms](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

>[!NOTE]
>
>La fonction AEM Forms, telle que Forms adaptatif, est disponible dans [AEM 6.5 QuickStart](https://experienceleague.corp.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html), à des fins d’exploration et d’évaluation uniquement. Pour une utilisation en production, il est essentiel d’obtenir une licence valide pour AEM Forms.


### Installer le package d’index GraphQL pour les fragments de contenu d’Experience Manager{#install-aem-graphql-index-add-on-package}

La clientèle qui utilise GraphQL doit installer le [fragment de contenu d’Experience Manager avec le package d’index GraphQL 1.1.1](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip).

Vous pouvez ainsi ajouter la définition d’index requise selon les fonctionnalités que vous utilisez réellement.

L’échec de l’installation de ce package peut entraîner des requêtes GraphQL lentes ou en échec.

>[!NOTE]
>
>N’installez ce package qu’une seule fois par instance ; il n’est pas nécessaire de le réinstaller avec chaque Pack de services.

### UberJar{#uber-jar}

UberJar pour [!DNL Experience Manager] 6.5.19.0 est disponible dans le [référentiel central Maven](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.18/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Pour utiliser UberJar dans un projet Maven, consultez la section [Utilisation d’UberJar](/help/sites-developing/ht-projects-maven.md) et incluez la dépendance suivante dans le POM de votre projet : <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.19</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar et les autres artefacts associés sont disponibles sur le référentiel central Maven au lieu du référentiel Maven public Adobe (`repo.adobe.com`). Le fichier UberJar principal est renommé `uber-jar-<version>.jar`. Il n’existe donc pas de `classifier` avec `apis` comme valeur pour la balise `dependency`.

## Fonctionnalités obsolètes et supprimées{#removed-deprecated-features}

Consultez les [Fonctionnalités obsolètes et supprimées](/help/release-notes/deprecated-removed-features.md/).

## Problèmes connus{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST.
 -->
<!-- REMOVED AS PER CQDOC-20022, JANUARY 23, 2023 * If you install [!DNL Experience Manager] 6.5 Service Pack 10 or a previous service pack on [!DNL Experience Manager] 6.5, the runtime copy of your assets custom workflow model (created in `/var/workflow/models/dam`) is deleted.
To retrieve your runtime copy, Adobe recommends to synchronize the design-time copy of the custom workflow model with its runtime copy using the HTTP API:
`<designModelPath>/jcr:content.generate.json`. -->

* **La publication de page ne fonctionne pas dans l’éditeur de page après la mise à niveau vers le pack de services 18 (6.5.19.0)**

  <!-- https://jira.corp.adobe.com/browse/SITES-15856 REMOVE FOR 6.5.19.0--> Après la mise à niveau d’une instance AEM 6.5.0.0-6.5.17.0 vers AEM 6.5.19.0, lorsque vous cliquez sur **Publier la page** dans l’éditeur de page, la redirection s’effectue vers une URL qui n’existe pas.

  Pour contourner ce problème, effectuez l’une des opérations suivantes :

   * Supprimez la propriété « path » suivante.

     `/libs/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/publish/granite:data`

   * Collez l’URL correcte directement dans le navigateur.

     `http://localhost:4504/editor.html/libs/wcm/core/content/sites/publishpagewizard.html?item=/content/we-retail/language-masters/en/about-us.html`



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

   1. Supprimez les deux dossiers suivants de `crx-quickstart/repository/`.

      * `cache`
      * `diff-cache`

   1. Installez le Pack de services ou redémarrez Experience Manager as a Cloud Service.
Les nouveaux dossiers `cache` et `diff-cache` sont automatiquement créés et vous ne voyez plus d’exception liée à `mvstore` dans `error.log`.

* Mettez à jour vos requêtes GraphQL qui peuvent avoir utilisé un nom d’API personnalisé pour votre modèle de contenu afin d’utiliser plutôt le nom par défaut du modèle de contenu.

* Une requête GraphQL peut utiliser l’index `damAssetLucene` plutôt que l’index `fragments`. Il peut en résulter l’échec des requêtes GraphQL ou l’exécution de celles-ci peut prendre beaucoup de temps.

  Pour résoudre le problème, `damAssetLucene` doit être configuré pour inclure les deux propriétés suivantes sous `/indexRules/dam:Asset/properties`:

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

* Les versions de JDK supérieures à 1.8.0_281 ne sont pas prises en charge pour le serveur WebLogic JEE. (FORMS-8498, CQDOC-20383)
* [!DNL Microsoft® Windows Server 2019] ne prend pas en charge [!DNL MySQL 5.7] et [!DNL JBoss® EAP 7.1], [!DNL Microsoft® Windows Server 2019] ne prend donc pas en charge les installations clé en main pour [!DNL Experience Manager Forms 6.5.10.0]. (CQDOC-18312)
* JDK 11.0.20 n’est pas pris en charge pour installer le programme d’installation AEM Forms on JEE. Seules la version JDK 11.0.19 ou les versions antérieures sont prises en charge pour installer le programme d’installation AEM Forms on JEE. (FORMS-10659)

#### Installation

* Sur la plateforme JBoss® 7.1.4, lorsque l’utilisateur ou l’utilisatrice installe le pack de services Experience Manager 6.5.16.0, le déploiement de `adobe-livecycle-jboss.ear` échoue. (CQ-4351522, CQDOC-20159)
* Après la mise à niveau vers l’environnement d’installation complet d’AEM Forms 6.5.18.0 JBoss® clé en main sur Windows Server 2022, lors de la compilation du code de l’application cliente Output à l’aide de Java™ 11, l’erreur de compilation suivante peut se produire :

  ```
  error: error reading [AEM_Forms_Installation_dir]\sdk\client-libs\common\adobe-output-client.jar; java.net.URISyntaxException: 
  Illegal character in path at index 70: file:/[AEM_Forms_Installation_dir]/sdk/client-libs/common/${clover.jar.name} 1 error
  ```

  Pour résoudre le problème, procédez comme suit :
   1. Accédez à `[AEM_Forms_Installation_dir]\sdk\client-libs\common\` et décompressez `adobe-output-client.jar` pour extraire le fichier `Manifest.mf`.
   1. Mettez à jour le fichier `Manifest.mf` en supprimant l’entrée `${clover.jar.name}` de l’attribut class-path.

      >[!NOTE]
      >
      > Vous pouvez également utiliser un outil de modification statique, par exemple 7-zip, pour mettre à jour le fichier `Manifest.mf`.

   1. Enregistrez la mise à jour de `Manifest.mf` dans l’archive `adobe-output-client.jar`.
   1. Enregistrer la modification `adobe-output-client.jar` et réexécutez la configuration. (CQDOC-20878)
* Après l’installation du programme d’installation complet du pack de services AEM 6.5.19.0, le déploiement EAR échoue sur JEE en utilisant l’installation clé en main de JBoss®.
Pour résoudre le problème, recherchez le fichier `<AEM_Forms_Installation_dir>\jboss\bin\standalone.bat` et mettez à jour `Adobe_Adobe_JAVA_HOME` vers `Adobe_JAVA_HOME` pour toutes les occurrences avant d’exécuter Configuration Manager. (CQDOC-20803)

#### Formulaires adaptatifs

* Lorsqu’un formulaire adaptatif est publié, toutes ses dépendances, y compris les stratégies, sont republiées, même si aucune modification ne leur a été apportée. (FORMS-10454)
* Lorsqu’un utilisateur ou une utilisatrice choisit de configurer un champ pour la première fois dans un formulaire adaptatif, l’option permettant d’enregistrer une configuration ne s’affiche pas dans l’explorateur de propriétés. Sélectionner un autre champ du formulaire adaptatif à configurer dans le même éditeur pour résoudre le problème.
* Lorsqu’une URL de redirection est définie dans le conteneur de guide d’un formulaire adaptatif, la signature en ligne cesse de fonctionner. (FORMS-10493)
* La publication de tous les modèles de document d’enregistrement (DoR) échoue. Seuls les modèles de document d’enregistrement basés sur des paramètres régionaux anglais et les modèles de document d’enregistrement Forms associés sont publiés. (FORMS-10535)

#### Communications interactives

* Après la mise à niveau vers AEM Service Pack 18, il n’est pas possible d’ouvrir la communication interactive avec des images intégrées volumineuses en mode d’édition. (FORMS-10578)
Pour résoudre le problème, procédez comme suit :

   1. Téléchargez [Hotfix-FORMS-10578](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr) à partir du lien SD.
   1. Procédez à l’extraction du fichier d’archive Hotfix pour obtenir un package Experience Manager (.zip) et des fichiers de lot (.jar).
   1. Chargez et installez le package (.zip) via le gestionnaire de packages.
   1. Ouvrez les lots Configuration Manager `https://server:host/system/console/bundles`, chargez et installez le lot (.jar).

## Lots OSGi et packages de contenu inclus{#osgi-bundles-and-content-packages-included}

Les documents texte suivants répertorient les lots OSGi et les packages de contenu inclus dans [!DNL Experience Manager] 6.5.19.0 : <!-- UPDATE FOR EACH NEW RELEASE -->

* [Liste des lots OSGi inclus dans Experience Manager 6.5.19.0](/help/release-notes/assets/65180_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Liste des packages de contenu inclus dans Experience Manager 6.5.19.0](/help/release-notes/assets/65180_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Sites web à accès limité{#restricted-sites}

Ces sites Web sont disponibles uniquement pour les clients. Si vous êtes client et avez besoin d’un accès, contactez votre responsable de compte Adobe.

* [Téléchargement du produit à l’adresse licensing.adobe.com](https://licensing.adobe.com/)
* [Contacter l’assistance clientèle Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=fr).

>[!MORELIKETHIS]
>
>* Page des produits [[!DNL Experience Manager] ](https://business.adobe.com/fr/products/experience-manager/adobe-experience-manager.html)
>* Documentation [[!DNL Experience Manager]  6.5](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=fr)
>* [Abonnement aux mises à jour prioritaires de produits d’Adobe](https://www.adobe.com/subscription/priority-product-update.html)
