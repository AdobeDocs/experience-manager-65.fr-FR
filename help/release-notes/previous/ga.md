---
title: Notes générales de mise à jour d’ [!DNL Adobe Experience Manager]  6.5
description: « Notes relatives à [!DNL Adobe Experience Manager] 6.5, décrivant les informations, les nouveautés, la procédure d’installation et les listes détaillées des modifications pour la version. »
exl-id: b3d4a527-44ca-4eb6-b393-f3e8117cf1a6
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: f30decf0e32a520dcda04b89c5c1f5b67ab6e028
workflow-type: ht
source-wordcount: '4493'
ht-degree: 100%

---

# Notes générales de mise à jour d’[!DNL Adobe Experience Manager] 6.5{#general-release-notes-for-adobe-experience-manager}

## Informations sur la version {#release-information}

| Produit | [!DNL Adobe Experience Manager] |
|---|---|
| Version | 6.5 |
| Type | Version majeure |
| Date de disponibilité générale | 8 avril 2019 |
| Mises à jour recommandées | Consultez les [mises à jour récentes d’AEM](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=fr). |

### Pour information {#trivia}

Le cycle de publication de cette version d’[!DNL Adobe Experience Manager] a débuté le 4 avril 2018, a passé 23 itérations d’assurance qualité et de correction de bugs et s’est terminé le 28 mars 2019. Au total, 1 345 problèmes d’utilisateurs et utilisatrices (y compris des améliorations et des nouvelles fonctionnalités) ont été corrigés dans cette version.

[!DNL Adobe Experience Manager] 6.5 est disponible depuis le 8 avril 2019.

![Écran de connexion à AEM 6.5](/help/assets/assets/aem65-login-v4.png)

## Nouveautés {#what-s-new}

[!DNL Adobe Experience Manager] 6.5 est une mise à niveau de la base de code d’[!DNL Adobe Experience Manager] 6.4. Cette version comporte de nouvelles fonctionnalités améliorées, des correctifs clés de bugs signalés par des client(e)s, des améliorations prioritaires demandées par les client(e)s et des correctifs de bugs généraux destinés à améliorer la stabilité du produit. Elle comprend également les mises à jour des packs de services d’[!DNL Adobe Experience Manager] 6.4 jusqu’au SP4.

Vous en trouverez un aperçu dans la liste ci-dessous, puis des détails complets dans les pages suivantes.

### [!DNL Experience Manager Foundation] {#experience-manager-foundation}

La plateforme d’[!DNL Adobe Experience Manager] 6.5 repose sur les versions mises à jour de l’architecture OSGi (Apache Sling et Apache Felix), ainsi que sur le référentiel de contenu Java™ : Apache Jackrabbit Oak 1.10.2.

Le démarrage rapide (Quickstart) utilise le moteur de servlet Eclipse Jetty 9.4.15.

#### Prise en charge de Java™  {#java-support}

* Nouvelle prise en charge de Java™ 11 et de Java™ 8 déjà pris en charge.
* Pour des performances optimales, remplacez les valeurs par défaut du CPG par d’autres valeurs. Pour plus d’informations, consultez la section [Installation et mise à jour](/help/sites-deploying/custom-standalone-install.md).
* Les mises à jour de maintenance Java™ 11 et Java™ 8 sont distribuées par Adobe pour que les client(e)s puissent les utiliser dans les projets liés à AEM, lorsqu’elles ne sont pas disponibles publiquement auprès d’Oracle.

#### Développement Java™ {#java-development}

* Il existe désormais [deux versions d’Uberjar](/help/sites-developing/ht-projects-maven.md#experience-manager-api-dependencies) : une version recommandée avec les interfaces publiques qui ne sont pas marquées comme obsolètes, ainsi qu’une version qui inclut les interfaces marquées comme obsolètes.

#### Interface utilisateur {#user-interface}

Diverses améliorations ont été apportées à l’UI pour qu’elle soit plus productive et plus facile à utiliser.

* Nouvelle interface utilisateur de gestion des autorisations pour les utilisateurs et les groupes.
* Les vues de colonnes ne chargent plus maintenant que les entrées visibles à l’écran et n’en chargent davantage que lorsque l’utilisateur ou l’utilisatrice commence à faire défiler l’écran. Les affichages en liste et en carte le faisaient déjà depuis la version 6.0 (amélioration dans la version 6.4).
* Les vues de colonne incluent désormais le statut du workflow pour les pages/ressources, le cas échéant.
* L’action [Sélectionner tout](/help/sites-authoring/basic-handling.md#select-all) est un moyen rapide d’exécuter une action sur toutes les pages ou tous les éléments d’un même dossier.
* L’action [Sélectionner tout](/help/sites-authoring/basic-handling.md#select-all) tente d’exécuter l’action sur toutes les pages/ressources, pas seulement sur ce qui a été chargé. Une boîte de dialogue d’avertissement s’affiche si l’action n’est pas mise à niveau pour gérer les actions en bloc.

>[!CAUTION]
>
>Adobe ne prévoit pas d’apporter d’autres améliorations à l’interface utilisateur classique. AEM 6.5 comprend l’interface utilisateur classique, et les clients effectuant une mise à niveau à partir de versions antérieures peuvent continuer à l’utiliser en l’état. L’interface utilisateur classique reste complètement prise en charge alors qu’elle est en passe de devenir obsolète. [En savoir plus](/help/sites-deploying/ui-recommendations.md).

#### Recherche et indexation {#indexing-and-search}

* La recherche dans Oak prend désormais en charge les facettes dynamiques. Par exemple, le rail de filtrage dans la recherche de ressources indique le nombre estimé de résultats.
* QueryBuilder a été étendu pour fournir des résultats avec des facettes dynamiques..

#### Mise à niveau {#upgrade}

* La mise à niveau statique directe vers AEM 6.5 est prise en charge pour les client(e)s exécutant AEM 6.2, 6.3 et 6.4. Les client(e)s utilisant les versions 5.x ou 6.0/6.1 qui souhaitent utiliser la mise à niveau statique doivent d’abord effectuer la mise à niveau vers la version 6.4. Ensuite, effectuez une mise à niveau vers la version 6.5 ou effectuez une mise à niveau par le biais du transfert du contenu entre les instances directement vers AEM 6.5.
* La procédure de mise à niveau reste en grande partie la même dans la version 6.5.
* Nous continuons à prendre en charge la compatibilité ascendante, l’évaluation de la complexité des mises à niveau et les fonctions de continuité des mises à niveau ajoutées dans la version 6.4. Des mises à jour spécifiques à la version ont été apportées à ces domaines, le cas échéant.
* Le package du détecteur de motifs est désormais simplifié. Il existe un package qui évalue les mises à niveau vers la version 6.5 pour les versions sources disponibles.
* Pour plus d’informations sur la procédure de mise à niveau, consultez la [documentation de mise à niveau](/help/sites-deploying/upgrade.md).

#### Projets et workflows {#projects-and-workflows}

* Le nouvel éditeur de modèle de workflow ajouté à la version 6.4 a été amélioré afin d’inclure davantage d’opérations telles que la copie et la publication, la prise en charge des variables dans les étapes de workflow et les divisions améliorées `AND` et `OR`.

#### Référentiel {#repository}

* La base d’Adobe Experience Manager 6.5 repose sur les versions mises à jour de la structure OSGi (Apache Sling et Apache Felix) et du référentiel de contenu Java™ : Apache Jackrabbit Oak 1.10.2.
* Pour obtenir un aperçu des problèmes résolus, consultez [Apache Jackrabbit Oak Jira v.1.10.0](https://archive.apache.org/dist/jackrabbit/oak/1.10.0/RELEASE-NOTES.txt), [Apache Jackrabbit Oak Jira v.1.10.1](https://archive.apache.org/dist/jackrabbit/oak/1.10.1/RELEASE-NOTES.txt) et [Apache Jackrabbit Oak Jira v.1.10.2](https://archive.apache.org/dist/jackrabbit/oak/1.10.2/RELEASE-NOTES.txt).

>[!CAUTION]
>
>La nouvelle version d’Oak Segment Tar présente depuis AEM 6.3 nécessite une migration de référentiel. Cette étape est obligatoire si vous effectuez une mise à niveau à partir d’une ancienne version de TarMK ou si vous souhaitez changer le nouveau Segment Tar à partir d’un autre type de persistance. Pour plus d’informations sur les avantages du nouveau Segment Tar, voir la section [FAQ sur la migration vers Oak Segment Tar](/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar).

#### OSGI {#osgi}

* Ajout de bibliothèques d’utilitaire Promises et Converter OSGi.

#### Sécurité {#security}

* Ajout de l’expiration du mot de passe pour l’utilisateur ou l’utilisatrice admin.

#### Serveur Web {#web-server}

* La distribution Quickstart utilise Eclipse Jetty 9.4.15 comme moteur de servlet (AEM 6.4 était fourni avec la version 9.3.22).

### [!DNL Experience Manager] Sites {#experience-manager-sites}

#### Applications d’une seule page gérées {#managed-single-page-apps}

L’éditeur de page offre la possibilité de modifier le contenu et la composition/mise en page en contexte dans les expériences rendues côté client (également appelé [Éditeur SPA](/help/sites-developing/spa-architecture.md)). Les applications d’une seule page existantes créées avec une structure JavaScript React ou Angular peuvent être étendues avec le SDK SJ AEM afin d’être modifiables pour les utilisateurs et utilisatrices.

D’abord fourni avec AEM 6.4 SP2, avec AEM 6.5, la prise en charge SPA permet d’accéder aux fonctionnalités suivantes :

* Utilisez l’éditeur de modèles pour modifier et configurer les parties AEM modifiables du SPA.
* Utilisez la gestion multisite pour créer des expériences d’applications monopages (SPA) par pays, en franchise ou sous marque blanche.

#### Gestion de contenu découplé {#headless-content-management}

AEM a la capacité de servir le contenu dans divers formats et à différents niveaux de la pile. Certains existent depuis 2008 avec les [Sling GET](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) et les [Servlets POST](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html). Content Services ([Exportateur de modèles Sling](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/develop-sling-model-exporter.html?lang=fr)), introduit dans AEM 6.3, est la méthode utilisée par le SDK SJ AEM pour hydrater les applications d’une seule page. L’[API HTTP pour Assets](/help/assets/mac-api-assets.md) est une API CRUD, qui a été étendue pour AEM 6.5.

Nouvelles fonctionnalités de l’API HTTP :

* Ajout de la [prise en charge des fragments de contenu à l’API HTTP pour Assets](/help/assets/assets-api-content-fragments.md) pour créer, mettre à jour, lire et supprimer des fragments.
* Exposition des listes de fragments de contenu via Content Services avec le [composant principal de la liste de fragments de contenu](https://www.aemcomponents.dev).
* [Bibliothèque de composants principaux](https://www.aemcomponents.dev) qui affiche la sortie JSON par défaut de Content Services pour chaque composant.

#### Add-on Screens {#screens-add-on}

Concevez, diffusez et optimisez efficacement les expériences sur tous les écrans numériques, depuis les kiosques interactifs jusqu’à l’affichage dynamique.

* Expériences et contenu unifiés sur les supports numériques et en magasin, grâce à une meilleure réutilisation du contenu
* Processus de création et d’approbation/publication rationalisés avec prise en charge des lancements
* Modification et diffusion d’expériences interactives riches à l’aide de l’éditeur de SPA
* Utilisation des lancements pour planifier les modifications futures du contenu de signalisation
* Lecture mesurée dans un canal de séquence
* Créez automatiquement une structure de projet à l’aide d’un fichier source, une feuille de calcul Excel par exemple.
* Prise en charge étendue des lecteurs multimédias avec un fonctionnement fiable en ligne et hors ligne (Smart Sync), capable de s’adapter aux réseaux de signalisation les plus vastes.
* Personnalisation selon l’emplacement ou la configuration du contenu déclenché par les données à l’aide d’espaces réservés dynamiques
* Informations unifiées générées par l’intégration d’Adobe Analytics dans le lecteur AEM Screens

Pour plus d’informations sur les modifications apportées à AEM Screens, consultez les notes de mises à jour dans le [Guide de l’utilisateur d’AEM Screens](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/aem-screens-introduction.html?lang=fr).

#### Développement de composants et de modèles {#component-amp-template-development}

* Archétype de projet Maven 18+ : pour les nouveaux projets, consultez la section [Github pour les notes de mise à jour](https://github.com/adobe/aem-project-archetype/releases).
* Application monopage d’archétype de projet Maven 1.0.6+ : pour les nouveaux projets, consultez la section [Github pour les notes de mise à jour](https://github.com/adobe/aem-spa-project-archetype/releases).
* HTL version 1.4, voir [Github pour les notes de mise à jour](https://github.com/adobe/htl-spec/releases/tag/1.4).

   * Opérateur « in » pour les chaînes, les tableaux et les objets :

     ```html
     ${'a' in 'abc'}
     ${100 in myArray}
     ${'a' in myObject}
     ```

   * Déclarations de variables avec data-sly-set :
     `<sly data-sly-set.title="${currentPage.title}"/>${title}`

   * Paramètres de contrôle de liste et de répétition : début, étape, fin :
     `<h2 data-sly-repeat="${currentPage.listChildren @ begin = 1, step=2}">${item.title}</h2>`

   * Identifiants pour data-sly-unwrap :

     ```html
     <div data-sly-unwrap.isUnwrapped="${myCondition || myOtherCondition}">
     text <span data-sly-test="${isUnwrapped}>is unwrapped</code>
     </div>
     ```

   * Prise en charge des nombres négatifs

* Composants principaux 2.3.2+ : consultez la section [Github pour les notes de mise à jour](https://github.com/adobe/aem-core-wcm-components/releases).
* Système de grille pour le conteneur de dispositions, voir [Github](https://github.com/Adobe-Marketing-Cloud/aem-responsivegrid).
* Manager Clientlib : définition par défaut de Google Closure Compiler pour la minimisation des bibliothèques client JavaScript (l’ancienne version par défaut était Yahoo YUI) et mise à jour de Google Closure Compiler vers la version v20190121.
* Éditeur de modèles et politiques

   * Création et modification de modèles pour les applications monopages qui utilisent le SDK JS (également appelé éditeur de SPA)

* Pour le site de référence We.Retail 4.0, voir [Github pour les notes de mise à jour](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases).
* Boîte à outils permettant de mettre à niveau les sites existants pour tirer parti des toutes dernières fonctionnalités d’éditeur, voir [référentiel Github](https://github.com/adobe/aem-modernize-tools).

>[!CAUTION]
>
>AEM comprend la version 1.12.4 de la bibliothèque jQuery pour fournir une compatibilité maximale avec le code personnalisé existant. Adobe a procédé à des modifications de façon à résoudre les problèmes de sécurité connus.

#### Administration de sites {#site-administration}

* Le rail [Référence](/help/sites-authoring/author-environment-tools.md#references) comporte une nouvelle section permettant de répertorier les liens internes pointant vers la page sélectionnée. Cela s’avère utile lorsque vous envisagez de mettre une page hors ligne ou de la supprimer, afin de déterminer les pages à ajuster avant de les mettre hors ligne.
* La vue [Liste](/help/sites-authoring/basic-handling.md#list-view) comporte une nouvelle colonne de workflow indiquant le statut de la page dans un workflow.
* Dans les [propriétés de page](/help/sites-authoring/editing-page-properties.md), il est désormais possible de rechercher des ressources existantes lors de l’attribution d’une miniature à la page (onglet Miniature).

#### Éditeur de page {#page-editor}

* Autorisez l’édition en contexte et la composition d’expériences d’application monopage avec des composants côté client React et Angular utilisant le SDK JS (également appelé éditeur de SPA).
* Le mode Génération de modèles automatique n’est affiché que si la page comporte une page de génération de modèles automatique configurée.

#### Fragments de contenu et éditeur {#content-fragments-amp-editor}

* Nouveau rail [Annotations](/help/assets/content-fragments/content-fragments-variations.md#viewing-editing-deleting-annotations) dans l’éditeur de fragment de contenu permettant de faire des commentaires généraux et d’afficher des commentaires dans le texte (à afficher également dans le rail Journal).
* Possibilité de définir le type de contenu par défaut d’un élément de texte multiligne dans [un modèle de contenu de fragments](/help/assets/content-fragments/content-fragments-models.md) sur : texte, texte enrichi ou markdown.
* Ajout de [commentaires/annotations](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment) en sélectionnant du texte dans l’éditeur de texte enrichi (affichage plein écran)
* [Comparaison de versions](/help/assets/content-fragments/content-fragments-managing.md#comparing-fragment-versions) d’un fragment de contenu côte à côte via le rail Référence
* Le rapport Téléchargement des ressources affiche désormais les fragments de contenu en conséquence.
* Ajoutez la [prise en charge des fragments de contenu à l’API HTTP Assets](/help/assets/assets-api-content-fragments.md) via /api.json Il existe des API pour créer, mettre à jour, lire et supprimer des fragments de contenu.

#### Fragments d’expérience {#experience-fragments}

* Amélioration de l’indexation des [fragments d’expérience](/help/sites-authoring/experience-fragments.md), afin que leur contenu soit trouvé dans la recherche de pages où ils sont utilisés.
* L’option [Exporter vers la cible](/help/sites-administering/experience-fragments-target.md) permet désormais d’envoyer le fragment d’expérience sous forme de fichier JSON (HTML par défaut), ou les deux.

#### Traduction {#translation}

* Simplifiez la création de projets de traduction à l’aide de Project Masters.
* Simplifiez l’exécution des projets de traduction en définissant les travaux de traduction sur le statut approuvé par défaut.
* Autorisez la mise à jour des pages traduites avec des modifications dans la mémoire de traduction tierce.
* Autorisez l’exportation de travaux de traduction au format JSON.
* Mettez à jour l’intégration de Microsoft® Translation pour utiliser l’API V3.

#### Gestion multisite (MSM, Multi-Site Management) {#multi-site-management-msm}

* Pour les configurations de déploiement utilisant PushOnModify : amélioration de la gestion de l’opération de déplacement de page pour éviter les incohérences.
* La création d’une page dans la structure de Live Copy crée une page autonome par défaut.
* Utilisez les fonctionnalités MSM dans les applications monopages utilisant le SDK JS (également appelé Editeur de SPA).

#### Lancements {#launches}

* Nouveau workflow de révision et d’approbation pour les lancements et possibilité de promouvoir uniquement les pages de lancement approuvées
* Ajout d’une [option dans l’interface utilisateur permettant de choisir la suppression du lancement juste après l’étape de promotion](/help/sites-authoring/launches-promoting.md#promoting-launch-pages)

#### Simulation et ciblage de contenu {#content-targeting-simulation}

* Mise à jour de la couche de données ContextHub et du moteur JavaScript de règles côté client pour utiliser jQuery 3 par défaut.

#### AEM et Adobe Target {#aem-amp-adobe-target}

>[!CAUTION]
>
>Actuellement :
>
>* Seul `at.js 1.x` est pris en charge si vous utilisez Adobe Target comme moteur de ciblage dans la console Activités d’AEM.
>
>* Les `at.js. 1.x` et `at.js 2.x` sont pris en charge si vous utilisez l’exportation de fragments d’expérience vers Target et que vous exécutez des activités dans la console de Target.

* L’intégration d’Adobe Target utilise désormais l’API Target Standard. Les versions antérieures d’AEM utilisent l’API HTTP Target Classic, désormais obsolète.
* La version 6.3 d’`mbox.js` Adobe Target est incluse. Adobe recommande vivement de passer l’implémentation à `at.js` v1.x.
* La version 1.5.0 de `at.js` est désormais incluse. Adobe recommande d’utiliser [Adobe Experience Platform Launch](https://business.adobe.com/products/experience-platform/launch.html) pour mettre en place de `at.js` 1.x sur le site.

#### AEM et Adobe Analytics {#aem-amp-adobe-analytics}

* `s_code.js` H.27.5 est inclus. Adobe recommande de passer à la mise en œuvre d’`AppMeasurement.js`.
* `AppMeasurement.js` v1.8.0 est inclus. Adobe recommande d’utiliser [Adobe Experience Platform Launch](https://business.adobe.com/products/experience-platform/launch.html) pour mettre en place AppMeasurement.js sur le site.

#### AEM et Commerce {#aem-commerce}

Les améliorations apportées au Commerce Integration Framework ont un cycle de publication de version plus rapide depuis AEM 6.4. Pour en savoir plus, consultez la section [Intégration d’AEM et d’Adobe Commerce à l’aide de Commerce Integration Framework](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/integrations/magento.html?lang=fr).

#### Module complémentaire Communities {#communities-add-on}

Pour obtenir la version la plus récente, consultez la section [Déploiement de communautés](/help/communities/deploy-communities.md) de la documentation.

##### Améliorations de l’engagement communautaire {#enhancements-to-community-engagement}

**Prise en charge des @Mentions**
AEM Communities permet désormais aux utilisateurs enregistrés de tagger (mentionner) d’autres membres inscrits pour attirer leur attention, dans le contenu créé par l’utilisateur. Les membres balisés (mentionnés) sont ensuite notifiés, avec un lien profond vers le contenu créé par l’utilisateur correspondant. Les utilisateurs peuvent toutefois choisir d’activer ou de désactiver les notifications par e-mail et Web.

![Prise en charge des mentions](/help/release-notes/assets/at-mentions.png)

Les utilisateurs et utilisatrices de la communauté n’ont pas besoin de rechercher leur prénom, leur nom ou leur nom d’utilisateur pour voir si quelqu’un les a contactés ou requiert leur attention. De plus, les auteurs et autrices de contenu créé par l’utilisateur peuvent demander une réponse à des utilisateurs et utilisatrices enregistrés spécifiques pouvant résoudre le problème et ajouter des entrées.

Les administrateurs de la communauté doivent **Activer la mention** sur les composants de la communauté pour permettre aux utilisateurs enregistrés d’utiliser la fonctionnalité de ces composants.

**Messages de groupe**

Les membres de la communauté enregistrés peuvent désormais envoyer des messages directs en masse à des groupes par le biais d’une seule composition d’e-mail, au lieu d’envoyer le même message individuellement aux membres du groupe. Pour autoriser la [messagerie de groupe](/help/communities/configure-messaging.md), activez les deux instances du [Service d’opérations de messagerie](/help/communities/messaging.md#group-messaging).

![Message de groupe](/help/release-notes/assets/group-messaging.png)

##### Améliorations apportées à la modération en bloc {#enhancements-to-bulk-moderation}

Filtres personnalisés dans la modération en bloc

Les [filtres personnalisés](/help/communities/moderation.md#custom-filters) peuvent désormais être développés et ajoutés à l’interface utilisateur de modération en bloc.

Un [exemple de projet](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter) illustrant le filtrage par balises est disponible dans [Github](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter). Ce projet peut être utilisé comme base pour développer des filtres personnalisés analogues.

![Filtres personnalisés](/help/release-notes/assets/custom-tag-filter.png)

**Vue Liste dans la modération en masse**

Une nouvelle vue Liste avec une UI améliorée a été fournie dans la modération en masse pour afficher les entrées de contenu généré par l’utilisateur ou l’utilisatrice.

![Modération en bloc dans la vue Liste](/help/release-notes/assets/list-view-moderation.png)

##### Améliorations de la gestion des sites et des groupes {#enhancements-to-site-and-group-management}

**Administrateurs ou administratrices de site côté auteur ou autrice, et de groupe**

Communities, à partir de la version AEM 6.5, permet une administration (et une gestion) décentralisée de différents sites et groupes/groupes imbriqués de communautés. Les organisations qui hébergent plusieurs sites de communauté et groupes imbriqués peuvent désormais sélectionner des membres pour les rôles d’administration côté auteur ou autrice au moment de la création du site (et du groupe).

![Administrateur de site](/help/release-notes/assets/site-admin.png)

Les administrateurs de site peuvent créer un groupe à n’importe quel niveau de la hiérarchie et en devenir les administrateurs par défaut. Ces administrateurs peuvent ensuite être supprimés par d’autres administrateurs du groupe. Les administrateurs et administratrices de groupe peuvent gérer leur groupe G1 et créer un sous-groupe imbriqué sous G1.

##### Améliorations de l’activation {#enhancements-to-enablement}

**Prise en charge de SCORM 2017.1**

La fonctionnalité d’activation d’AEM 6.5 Communities prend en charge le moteur de modèle de référence des objets de contenu partageables [(SCORM) 2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/).

* Prise en charge de la navigation au clavier sur les composants d’activation
* Les composants d’activation (par exemple, la lecture de catalogue et de cours, les affectations, la bibliothèque de fichiers) dans AEM Communities prennent en charge la navigation au clavier pour améliorer l’accessibilité.

##### Autres améliorations {#other-enhancements}

* Prise en charge de Solr 7
* AEM Communities 6.5 prend en charge la version Apache Solr 7.0 de la plateforme de recherche lors de la configuration de MSRP et de DSRP.

### [!DNL Experience Manager Assets] {#experience-manager-assets}

AEM 6.5 propose les fonctionnalités et améliorations suivantes pour accroître la productivité des utilisateurs AEM, des rôles de gestion des ressources numériques et des rôles de création et de marketing associés.

#### Intégration avec [!DNL Adobe Creative Cloud] et les workflows créatifs {#integration-with-adobe-creative-cloud-and-creative-workflows}

[!DNL Adobe Experience Manager] propose différentes manières de s’intégrer à [!DNL Adobe Creative Cloud] et de partager des ressources à utiliser dans des workflows, où les équipes créatives et marketing et les équipes d’entreprise collaborent étroitement. [!DNL Experience Manager] 6.5 continue à améliorer l’intégration et à la rationaliser afin d’exposer davantage de possibilités et de rationaliser les méthodes existantes.

Lisez ce qui suit pour connaître les fonctionnalités et intégrations spécifiques d’[!DNL Experience Manager] 6.5 que vous pouvez utiliser pour prendre en charge les cas d’utilisation de vélocité de contenu.

##### Adobe Asset Link {#aal}

[!DNL Adobe Asset Link]renforce la collaboration entre les créatifs et les spécialistes marketing dans le processus de création de contenu. Les créatifs peuvent accéder au contenu stocké dans [!DNL Experience Manager Assets], sans quitter les applications qu’ils connaissent le mieux. Ils peuvent parcourir, rechercher, extraire et archiver des ressources de manière transparente à l’aide du panneau intégré à l’application dans les applications [!DNL Adobe Photoshop], [!DNL Adobe Illustrator] et [!DNL Adobe InDesign].

[!DNL Adobe Asset Link] fait partie de l’offre [Creative Cloud abonnement Entreprise](https://www.adobe.com/creativecloud/business/enterprise.html). Pour plus d’informations à ce sujet, y compris sur la configuration nécessaire de votre déploiement d’[!DNL Experience Manager], consultez la section [Adobe Asset Link](https://helpx.adobe.com/fr/enterprise/using/adobe-asset-link.html).

![Recherche de ressources dans Adobe Photoshop](/help/release-notes/assets/asset_search_photoshop.png)

##### Intégration d’[!DNL Adobe Stock] {#stock}

Votre entreprise peut utiliser son offre d’entreprise [!DNL Adobe Stock] dans [!DNL Experience Manager Assets] pour s’assurer que les ressources sous licence sont disponibles pour les projets de création et de marketing. Vous pouvez rapidement rechercher, prévisualiser et utiliser sous licence les ressources [!DNL Adobe Stock] enregistrées dans Experience Manager, grâce aux puissantes fonctionnalités de gestion dynamique des ressources d’[!DNL Experience Manager].

Le service [!DNL Adobe Stock] permet aux concepteurs et aux entreprises d’accéder à des millions de photos, de vecteurs, d’illustrations, de vidéos, de modèles et de ressources 3D organisés, de grande qualité et libres de droits d’auteur pour tous leurs projets de création.

Pour plus d’informations, consultez la section [Utiliser des ressources Adobe Stock dans Experience Manager Assets](/help/assets/aem-assets-adobe-stock.md).

![Prévisualisez l’image et la licence Adobe Stock depuis Experience Manager Assets](/help/release-notes/assets/stock_image_preview_license_options.png)

*Image : aperçu d’images et de licence [!DNL Adobe Stock] depuis [!DNL Experience Manager Assets].*

![Rechercher et filtrer les images Adobe Stock sous licence dans Experience Manager](/help/release-notes/assets/aem-search-filters2.jpg)

*Image : rechercher et filtrer les images sous licence [!DNL Adobe Stock] dans [!DNL Experience Manager].*

##### Références dynamiques dans [!DNL Adobe InDesign] {#dynamic-references-in-indesign}

Les ressources [!DNL Experience Manager Assets] utilisées dans les fichiers [!DNL Adobe InDesign] sont dynamiques. Les références sont mises à jour automatiquement si les ressources référencées sont déplacées dans le référentiel. Pour plus d’informations, consultez la section [Gestion des ressources composites](/help/assets/managing-linked-subassets.md).

#### Fonctionnalités de Brand Portal {#brand-portal-capabilities}

[!DNL Experience Manager Assets Brand Portal] vous permet d’acquérir facilement, de contrôler efficacement et de distribuer en toute sécurité les ressources approuvées aux fournisseurs et aux agences externes, et aux utilisateurs professionnels internes, sur tous les appareils. Il contribue à améliorer l’efficacité du partage des ressources, accélère leur mise sur le marché et élimine le risque d’utilisation non conforme et d’accès non autorisé.

Pour plus d’informations, consultez [Nouveautés de Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html?lang=fr).

#### Ressources connectées {#connectedassets}

Dans les grandes entreprises, l’infrastructure requise pour créer des sites web peut être distribuée. Parfois, les fonctionnalités de création de site web et les ressources numériques requises résident dans différents silos.

[!DNL Experience Manager Sites] offre des fonctionnalités permettant de créer des pages Web et [!DNL Experience Manager Assets] est le système de gestion des ressources numériques (DAM) qui fournit les ressources requises pour les sites Web. [!DNL Experience Manager] prend désormais en charge le cas d’utilisation ci-dessus en intégrant [!DNL Sites] et [!DNL Assets]. Consultez la section [Configuration et utilisation de la fonction Ressources connectées](/help/assets/use-assets-across-connected-assets-instances.md).

![Faites glisser une ressource depuis un déploiement [!DNL Experience Manager] sur une page [!DNL Sites] d’un autre déploiement [!DNL Experience Manager]](/help/release-notes/assets/connected-assets-drag-and-drop-only.gif).

*Image : faites glisser une ressource depuis un déploiement [!DNL Experience Manager] sur une page [!DNL Sites] d’un déploiement [!DNL Experience Manager] différent.*

#### Dynamic Media {#dynamic-media}

[!DNL Dynamic Media] permet la création et la diffusion de contenus multimédias enrichis améliorés dans [!DNL Experience Manager Assets] afin de générer des expériences de pointe immersives et personnalisées. En chargeant une seule ressource principale de grande qualité et en utilisant le rendu et les visionneuses cloud avancés d’Adobe, vous pouvez diffuser n’importe quelle combinaison de rendus à la volée pour prendre en charge la stratégie multimédia de votre organisation.

Pour plus d’informations sur les nouvelles fonctionnalités de [!DNL Dynamic Media], consultez les [Notes de mise à jour de Dynamic Media](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/release-notes/s7rn2017.html?lang=fr).

##### Prise en charge de la vidéo à 360° {#video-support}

Gérez vos fichiers vidéo 360° directement dans [!DNL Experience Manager] à l’aide des visionneuses de pointe de Dynamic Media, pour diffuser des expériences en réalité virtuelle sur les postes de travail, les appareils mobiles et les casques VR. Pour plus d’informations, consultez la section [Utilisation de la vidéo à 360°](/help/assets/360-video.md).

##### Miniatures vidéo personnalisées {#custom-video-thumbnails}

Vous pouvez maintenant personnaliser les vignettes de vos ressources vidéo à l’aide d’images de la vidéo ou de tout autre contenu stocké dans la gestion des ressources numériques. Pour obtenir des instructions supplémentaires, consultez la section [Ȃ propos des miniatures vidéo](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-scene-mode).

##### Améliorations de l’accessibilité {#accessibility-enhancements}

Les visionneuses [!DNL Dynamic Media] assurent désormais la prise en charge de fonctionnalités d’accessibilité améliorées telles que la prise en charge Aria, les lecteurs d’écran et le texte de remplacement. Pour plus d’informations, consultez le [Guide de référence des visionneuses](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/homeviewers.html?lang=fr).

#### Amélioration de l’expérience de recherche {#experience-enhancement-for-searching}

À partir de[!DNL Experience Manager] 6.5, les spécialistes marketing peuvent découvrir plus rapidement les ressources souhaitées à partir de la page des résultats de recherche. Les facettes de recherche sont mises à jour avec le nombre de ressources avant même d’appliquer le filtre de recherche. L’affichage du nombre prévu en fonction du filtre aide les utilisateurs et utilisatrices à parcourir rapidement et efficacement les résultats de la recherche. Pour plus d’informations, consultez la section [Recherche de ressources dans Experience Manager](/help/assets/search-assets.md).

![Afficher le nombre de ressources sans filtrer les résultats de la recherche dans les facettes de recherche](/help/assets/assets/asset_search_results_in_facets_filters.png)

*Image : consultez le nombre approximatif des ressources sans filtrer les résultats de la recherche dans les facettes de recherche.*

#### Amélioration de la convivialité {#usability-enhancement}

Vous pouvez désormais sélectionner simultanément toutes les ressources chargées dans un fichier ou un résultat de recherche. Vous pouvez ainsi gérer plusieurs ressources rapidement. La case à cocher permet de sélectionner toutes les ressources correspondant au scénario, par exemple un résultat de recherche, et pas seulement les ressources visibles dans l’interface d’[!DNL Experience Manager].

![Utilisez l’option Sélectionner tout pour sélectionner toutes les ressources chargées en un seul clic.](/help/release-notes/assets/select-all-in-aem-assets.gif)

*Image : utilisez l’option Sélectionner tout pour sélectionner toutes les ressources en un seul clic.*

#### Améliorations des métadonnées {#metadata-enhancements}

[!DNL Assets] vous permet de créer des schémas de métadonnées pour des dossiers de ressources. Ces schémas définissent la disposition et les métadonnées affichées dans les pages de propriétés des dossiers. Vous pouvez désormais attribuer un schéma de métadonnées de dossier à un dossier existant ou lors de la création d’un dossier. Pour plus d’informations, voir [Schéma de métadonnées de dossier](/help/assets/metadata-config.md#folder-metadata-schema).

Lors de la spécification de métadonnées en cascade, les choix peuvent être chargés à partir d’un fichier JSON au moment de l’exécution, par exemple au lieu d’effectuer une saisie manuelle dans le formulaire. Pour plus d’informations, consultez la section [Métadonnées en cascade](/help/assets/metadata-schemas.md#cascading-metadata).

#### Améliorations des rapports {#reporting-enhancements}

Les fragments de contenu et les partages de liens sont maintenant inclus dans le rapport téléchargé. Pour plus d’informations, consultez la section [Rapports d’Assets](/help/assets/asset-reports.md).

### [!DNL Adobe Experience Manager Forms] {#experience-manager-forms}

AEM Forms 6.5 comporte plusieurs nouvelles fonctionnalités et améliorations. En voici un aperçu :

* Rapports de transaction pour suivre le nombre de formulaires envoyés, de documents traités et de documents rendus
* Améliorations de l’utilisation des communications interactives
* Signatures numériques basées sur le cloud dans les formulaires adaptatifs
* Intégrez des formulaires adaptatifs et des communications interactives dans les applications monopages (SPA) d’AEM Sites.
* Prise en charge des variables dans les workflows AEM
* Prise en charge du modèle d’affichage des données dans les communications interactives
* Tri des formulaires adaptatifs et des tableaux de communication interactive
* Validation automatisée des données d’entrée dans les modèles de données de formulaire

Consultez le [Résumé des nouvelles fonctionnalités et améliorations apportées à AEM 6.5 Forms](/help/forms/using/whats-new.md) pour plus d’informations sur les fonctionnalités nouvelles et améliorées et les ressources de documentation.

### Utiliser le développement axé sur le client {#use-customer-focused-development}

Adobe applique un modèle de développement axé sur les clients et clientes afin qu’ils puissent contribuer à toutes les étapes du processus de développement, au cours des phases de spécification, de développement et de tests. Merci à tous les utilisateurs, utilisatrices et partenaires qui contribuent à ce processus.

Adobe a mis en place les procédures et processus nécessaires à la collecte, à la hiérarchisation et au suivi de la résolution des bogues signalés par les utilisateurs et utilisatrices, et du développement des demandes d’amélioration. Le [portail d’assistance d’Experience Manager](https://experienceleague.adobe.com/fr?support-solution=Experience+Manager&amp;lang=fr#support) est intégré au système de suivi des défauts et des améliorations d’Adobe. Les questions des utilisateurs sont identifiées et résolues par l’assistance clientèle dans la mesure du possible. Lorsqu’elles sont transmises au service de R&amp;D, toutes les informations client sont capturées et utilisées à des fins de hiérarchisation et de création de rapports. Les problèmes entrant dans le cadre de l’assistance payante et de la garantie, ainsi que les demandes d’amélioration des utilisateurs détenant un compte payant sont prioritaires.

Ce processus de hiérarchisation a généré plus de 750 modifications axées sur les clients et clientes, et corrigées dans AEM 6.5.

## Liste des fichiers faisant partie de la version {#list-of-files-that-are-part-of-the-release}

**Foundation**

* Démarrage rapide autonome : `cq-quickstart-6.5.0.jar`.
* Démarrage rapide du serveur d’applications : `cq-quickstart-6.5.0.war`.
* Dispatcher 4.3.2 ou version ultérieure pour les différents serveurs et plateformes Web. Consultez le [lien de téléchargement](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/release-notes.html?lang=fr).
* Module externe pour Eclipse IDE ([plus d’infos et téléchargement](/help/sites-developing/aem-eclipse.md))

* Extension pour l’éditeur de code Brackets ([plus d’infos et téléchargement](/help/sites-developing/aem-brackets.md))
* Dépendances Maven/Gradle ([lien de téléchargement](https://repo1.maven.org/maven2/com/adobe/aem/uber-jar/6.5.0/))

**Sites**

* Composants principaux ([projet GitHub](https://github.com/adobe/aem-core-wcm-components))
* Implémentation de référence We.Retail ([en savoir plus](/help/sites-developing/we-retail.md))
* Archétypes Maven Project :

   * pour les sites full-stack : [projet GitHub](https://github.com/adobe/aem-project-archetype)
   * pour les applications monopages avec React/Angular : [projet GitHub](https://github.com/adobe/aem-spa-project-archetype)

* Lecteurs AEM Screens pour différentes plateformes cibles ([téléchargement](https://download.macromedia.com/screens/))

* Modèles linguistiques pour le contenu dynamique. L’anglais est préinstallé ; d’autres langues peuvent être téléchargées :

   * [Allemand](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?lang=fr?package=/content/software-distribution/en/details.html?lang=fr/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-de)
   * [Espagnol](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?lang=fr?package=/content/software-distribution/en/details.html?lang=fr/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-es)
   * [Italien](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?lang=fr?package=/content/software-distribution/en/details.html?lang=fr/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-it)
   * [Français](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?lang=fr?package=/content/software-distribution/en/details.html?lang=fr/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-fr)

* Suite d’outils de modernisation d’AEM, par exemple Outil de conversion de dialogue. ([Projet GitHub](https://github.com/adobe/aem-modernize-tools))

**Assets**

* Package pour l’ajout de l’outil de restérisation de PDF amélioré ([en savoir plus](/help/assets/aem-pdf-rasterizer.md))
* Package pour l’ajout de la prise en charge étendue des images RAW ([en savoir plus](/help/assets/camera-raw.md))

**Forms**

* [Packages pour les fonctionnalités AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr)
* [SDK OSGi client AEM Forms](https://repo1.maven.org/maven2/com/adobe/aemfd/aemfd-client-sdk/)

## Langues {#languages}

L’interface utilisateur de est disponible dans les langues suivantes :

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

## Installation et mise à jour {#install-update}

Pour connaître les exigences de configuration, consultez les [instructions d’installation](/help/sites-deploying/custom-standalone-install.md).

Pour obtenir des instructions détaillées, consultez la [documentation de mise à niveau](/help/sites-deploying/upgrade.md).

## Plateformes prises en charge {#supported-platforms}

Recherchez la matrice complète des plateformes prises en charge, y compris le niveau de prise en charge dans les [Exigences techniques AEM 6.5](/help/sites-deploying/technical-requirements.md).

>[!NOTE]
>
>Oracle est passé à un modèle de support à long terme (LTS) pour les produits Oracle Java™ SE. Java™ 9 et 10 sont des versions non-LTS par Oracle. Voir [Feuille de route du support Oracle Java™ SE](https://www.oracle.com/technetwork/java/eol-135779.html). Adobe assure uniquement la prise en charge des versions LTS de Java™ pour n’exécuter AEM qu’en exploitation. La version 11 de Java™ est recommandée pour une utilisation avec AEM 6.5.

## Fonctionnalités obsolètes et supprimées {#deprecated-and-removed-features}

Adobe évalue constamment les fonctionnalités du produit et prévoit au fil du temps de remplacer certaines d’entre elles par des versions plus puissantes, ou décide d’implémenter à nouveau certaines parties pour mieux se préparer aux attentes ou aux extensions futures.

Concernant [!DNL Adobe Experience Manager] 6.5, [consultez la liste des fonctionnalités obsolètes et supprimées](/help/release-notes/deprecated-removed-features.md). Cette page contient également une annonce préalable des modifications qui seront apportées dans un avenir proche et un avis important pour les client(e)s qui mettent à jour des versions antérieures.

## Problèmes connus {#known-issues}

### Plateforme {#platform}

* Un problème est signalé lorsque le démarrage rapide de CRX et son contenu sont supprimés.

  Pour chacune de ces actions, assurez-vous que la propriété `htmllibmanager.fileSystemOutputCacheLocation` n’est pas une chaîne vide :

   1. appelant la fonction `/libs/granite/ui/content/dumplibs.rebuild.html?invalidate=true`.
   2. Mise à niveau vers AEM 6.5.
   3. Exécution de la « migration différée du contenu » sur AEM 6.5.

  Cet article de la [Base de connaissances](https://helpx.adobe.com/fr/experience-manager/kb/avoid-crx-quickstart-deletion-in-aem-6-5.html) est disponible pour vous offrir plus d’informations et la solution à ce problème.

* Si vous utilisez le JDK 11 avec l’instance AEM 6.5, certaines pages peuvent s’afficher comme vides après le déploiement de certains packages. Le message d’erreur suivant s’affiche dans le fichier journal :

  ```java
  *ERROR* [OsgiInstallerImpl] org.apache.sling.scripting.sightly bundle org.apache.sling.scripting.sightly:1.1.2.1_4_0 (558)[org.apache.sling.scripting.sightly.impl.engine.extension.use.JavaUseProvider(3345)] : Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl)
  java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl
  ```

Pour résoudre cette erreur, suivez les étapes suivantes :

1. Désactivez l’instance AEM. Accédez à `<aem_server_path_on_server>crx-quickstart\conf` et ouvrez le fichier `sling.properties`. Adobe recommande de sauvegarder ce fichier.

1. Recherchez `org.osgi.framework.bootdelegation=`. Ajoutez les propriétés `jdk.internal.reflect,jdk.internal.reflect.*` pour afficher le résultat.

```java
org.osgi.framework.bootdelegation=sun.*,com.sun.*,jdk.internal.reflect,jdk.internal.reflect.*
```

1. Enregistrez le fichier et redémarrez l’instance AEM.

### Sites {#sites}

* **Utilisation des versions de page** : [si une page a été déplacée, vous ne pouvez plus afficher l’aperçu des versions antérieures au déplacement](/help/sites-authoring/working-with-page-versions.md#previewing-a-version).

### Assets {#assets}

* **Recherche :** la recherche ne renvoie aucun résultat si la chaîne de recherche contient des espaces au début ([OAK-4786](https://issues.apache.org/jira/browse/OAK-4786)).
* **Schéma de métadonnées des dossiers** : après l’ajout d’un bouton de choix, les champs ID et Valeur ne sont pas restitués comme prévu et la fonctionnalité de suppression ne fonctionne pas. (CQ-4261144)
* Lors de l’attribution d’un nouveau nom à une ressource, il n’est pas possible d’utiliser un espace dans le nom. (CQ-4266403)

### Forms {#forms}

* Lorsqu’AEM Forms est installé sous un système d’exploitation Linux, la signature numérique avec le module de sécurité matérielle ne fonctionne pas. (CQ-4266721)
* (AEM Forms sur WebSphere® uniquement) L’option **Forms Workflow** > **Recherche de tâche** ne renvoie aucun résultat si vous recherchez un **Administrateur** en utilisant le **Nom d’utilisateur** comme critère de recherche. (CQ-4266457)

* AEM Forms ne parvient pas à convertir les fichiers TIF et TIFF avec la compression JPEG en documents PDF. (CQ-4265972)
* Les options **Analyseur de ressources AEM Forms** et **Migration de la correspondance vers la communication interactive** ne fonctionnent pas sur la page **Migration d’AEM Forms**. (CQ-4266572)

* (JBoss® 7 uniquement) Lorsque vous mettez à niveau une version antérieure vers AEM Forms 6.5 et que la version antérieure comportait des processus (.lca) qui créaient et utilisaient une copie du processus d’envoi ou de rendu par défaut, HTML5 Forms, qui utilise de tels processus (.lca), ne parvient pas à effectuer les actions requises. (CQ-4243928)
* Dans une version adaptative, lorsqu’un service de modèle de données de formulaire est appelé à partir de l’éditeur de règle pour mettre à jour de manière dynamique les valeurs du composant de choix d’image, les valeurs du composant de choix d’image ne sont pas mises à jour. (CQ-4254754)
* Le programme d’installation d’AEM Forms Designer nécessite la version 32 bits des [packages d’exécution redistribuables Visual C++ 2012](https://docs.microsoft.com/fr-FR/cpp/windows/latest-supported-vc-redist?view=msvc-170) et des [packages d’exécution redistribuables Visual C++ 2013](https://support.microsoft.com/fr-fr/topic/update-for-visual-c-2013-and-visual-c-redistributable-package-5b2ac5ab-4139-8acc-08e2-9578ec9b2cf1). Assurez-vous que les packages d’exécution redistribuables susmentionnés sont installés avant de démarrer l’installation. (CQ-4265668)

* PDF Generator ne prend pas en charge l’authentification par carte intelligente. Lorsqu’un administrateur active la politique de groupe `Interactive Logon: Require Smart card` sur un serveur Windows, tous les utilisateurs et utilisatrices de PDF Generator existants sont invalidés.

* Lorsqu’un formulaire adaptatif est configuré pour mettre à jour de manière dynamique les valeurs d’un composant et que l’instance de publication hébergeant le formulaire est accessible via le dispatcher, la fonctionnalité permettant de mettre à jour de manière dynamique les valeurs d’un champ cesse de fonctionner. Pour résoudre le problème, ouvrez CRXDE sur l’instance de publication, accédez à `/libs/fd/af/runtime/clientlibs/guideChartReducer` et créez la propriété répertoriée ci-dessous.

   * Nom : allowProxy
   * Type : booléen
   * Valeur : true
   * Protégé : false
   * Obligatoire : false
   * Multiple : false
   * Créé automatiquement : faux

  La propriété permet aux bibliothèques clientes du dossier d’exécution d’accéder aux mandataires. (CQ-4268679)

* Au démarrage d’AEM Forms, l’avertissement `SAX Security Manager could not be setup` s’affiche.
* Lorsque vous ouvrez un PDF protégé par AEM Forms Document Security sur un appareil iOS ou iPadOS d’Apple exécutant la version 20.10.00 d’Adobe Acrobat Reader.
* Lorsque vous envoyez un formulaire contenant un champ de chargement HTML standard d’un appareil iOS d’Apple, le contenu du fichier n’est parfois pas envoyé et un fichier de 0 octet est reçu à l’autre bout. Apple iOS 15.1 apporte un correctif pour le problème.

## Assistance technique et téléchargement du produit (sites à accès limité) {#product-download-and-support-restricted-sites}

Les sites suivants sont disponibles uniquement pour les clients. Si vous êtes client et avez besoin d’un accès, contactez votre responsable de compte Adobe.

* [Téléchargement du produit à l’adresse licensing.adobe.com](https://licensing.adobe.com/).

* Mises à jour de produit, correctifs et packages pour des fonctionnalités supplémentaires dans la [distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).

* [Service clientèle via l’Admin Console](https://adminconsole.adobe.com/). Pour plus d’informations, consultez la section [Nouvelle expérience du service clientèle Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=fr).
