---
title: Notes de mise à jour générales de [!DNL Adobe Experience Manager] 6,5
description: '[!DNL Adobe Experience Manager]Notes relatives à  6.5 décrivant les informations de version, les nouveautés, la procédure d’installation et les listes de modifications détaillées.'
source-git-commit: 9b15215a68495a800e94a58b523e1b7baa0c0203
workflow-type: tm+mt
source-wordcount: '4696'
ht-degree: 58%

---

# Notes de mise à jour générales de [!DNL Adobe Experience Manager] 6,5{#general-release-notes-for-adobe-experience-manager}

## Informations sur la version {#release-information}

| Produit | [!DNL Adobe Experience Manager] |
|---|---|
| Version | 6.5 |
| Type | Version majeure |
| Date de disponibilité générale | 8 avril 2019 |
| Mises à jour recommandées | Voir [AEM mises à jour récentes](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=fr). |

### Trivia {#trivia}

Cycle de publication de cette version de [!DNL Adobe Experience Manager] a commencé le 4 avril 2018, a subi 23 itérations d’assurance qualité et de correction de bogues et s’est terminée le 28 mars 2019. Au total, 1 345 problèmes d’utilisateurs (y compris des améliorations et des nouvelles fonctionnalités) ont été corrigés dans cette version.

[!DNL Adobe Experience Manager] La version 6.5 est disponible depuis le 8 avril 2019.

![Écran de connexion AEM 6.5](/help/assets/assets/aem65-login-v4.png)

## Nouveautés {#what-s-new}

[!DNL Adobe Experience Manager] La version 6.5 est une version de mise à niveau vers la version [!DNL Adobe Experience Manager] Base de code 6.4. Cette version comporte de nouvelles fonctionnalités améliorées, des correctifs clés de bugs signalés par des clients, des améliorations prioritaires demandées par les clients et des correctifs de bugs généraux destinés à améliorer la stabilité du produit. Elle comprend également [!DNL Adobe Experience Manager] 6.4 Versions du Service Pack jusqu’à SP4.

La liste ci-dessous présente un aperçu, tandis que les pages suivantes répertorient tous les détails.

### [!DNL Experience Manager Foundation] {#experience-manager-foundation}

La plateforme de [!DNL Adobe Experience Manager] Version 6.5 reposant sur les versions mises à jour de la structure OSGi (Apache Sling et Apache Felix) et du référentiel de contenu Java : Apache Jackrabbit Oak 1.10.2.

Le démarrage rapide (Quickstart) utilise le moteur de servlet Eclipse Jetty 9.4.15.

#### Prise en charge de Java  {#java-support}

* Nouvelle prise en charge de Java 11, ainsi que de Java 8 déjà pris en charge.
* Pour des performances optimales, remplacez les valeurs par défaut du CPG par d’autres valeurs. Pour plus d’informations, voir [installation et mise à jour](/help/sites-deploying/custom-standalone-install.md) .
* Les mises à jour de maintenance Java 11 et Java 8 sont distribuées par Adobe pour que les clients puissent les utiliser dans les projets liés aux AEM, lorsqu’elles ne sont pas disponibles publiquement dans Oracle.

#### Développement Java {#java-development}

* Il y a maintenant [deux versions d’Uberjar](/help/sites-developing/ht-projects-maven.md#experience-manager-api-dependencies), une version recommandée avec des interfaces publiques qui ne sont pas marquées pour obsolescence, ainsi qu’une version qui inclut des interfaces marquées pour obsolescence.

#### Interface utilisateur {#user-interface}

Diverses améliorations ont été apportées à l’interface utilisateur pour la rendre plus productive et conviviale.

* Nouvelle interface utilisateur de gestion des autorisations pour les utilisateurs et les groupes.
* Les vues de colonnes ne chargent plus maintenant que les entrées visibles à l’écran et en chargent davantage lorsque l’utilisateur commence à faire défiler l’écran. Les vues de liste et de carte le faisaient déjà depuis la version 6.0 (amélioration dans la version 6.4).
* Les vues de colonne incluent désormais l’état du workflow pour les pages/ressources, le cas échéant.
* Le [Tout sélectionner](/help/sites-authoring/basic-handling.md#select-all) est un moyen rapide d’exécuter une action avec toutes les pages/ressources du même dossier.
* L’action [Sélectionner tout](/help/sites-authoring/basic-handling.md#select-all) tente d’exécuter l’action sur toutes les pages/ressources, pas seulement sur ce qui a été chargé. Une boîte de dialogue d’avertissement s’affiche si l’action n’est pas mise à niveau pour gérer les actions en bloc.

>[!CAUTION]
>
>Adobe ne prévoit pas d’apporter d’autres améliorations à l’interface utilisateur classique. AEM 6.5 comprend l’interface utilisateur classique, et les clients effectuant une mise à niveau à partir de versions antérieures peuvent continuer à l’utiliser en l’état. Notez que l’interface utilisateur classique reste complètement prise en charge alors qu’elle est en passe de devenir obsolète. [En savoir plus](/help/sites-deploying/ui-recommendations.md).

#### Recherche et indexation {#indexing-and-search}

* La recherche dans Oak prend désormais en charge les facettes dynamiques. Par exemple, le rail de filtrage dans la recherche de ressources affiche la quantité estimée de résultats.
* QueryBuilder a été étendu pour fournir des résultats avec des facettes dynamiques.

#### Mise à niveau {#upgrade}

* La mise à niveau directe sur place vers AEM 6.5 est prise en charge pour les clients exécutant AEM 6.2, 6.3 et 6.4. Les clients utilisant les versions 5.x ou 6.0/6.1 qui souhaitent utiliser une mise à niveau sur place doivent tout d’abord passer à la version 6.4, puis à la version 6.5, ou à la mise à niveau via le transfert du contenu entre les instances directement vers AEM 6.5.
* La procédure de mise à niveau reste en grande partie la même dans la version 6.5.
* Nous continuons à prendre en charge la compatibilité ascendante, l’évaluation de la complexité des mises à niveau et les fonctions de continuité mises à niveau ajoutées dans la version 6.4. Des mises à jour spécifiques à la version ont été apportées à ces domaines, le cas échéant.
* L’assemblage du détecteur de modèle a été simplifié et un seul package évaluera les mises à niveau vers la version 6.5 pour les versions sources disponibles.
* Pour plus d’informations sur la procédure de mise à niveau, voir [documentation de mise à niveau](/help/sites-deploying/upgrade.md).

#### Projets et workflows {#projects-and-workflows}

* Le nouvel éditeur de modèle de processus introduit dans la version 6.4 a été amélioré afin d’inclure davantage d’opérations telles que Copier et Publier, la prise en charge des variables dans les étapes de processus et une amélioration. `OR` et `AND` se sépare.

#### Référentiel {#repository}

* La base d’Adobe Experience Manager 6.5 repose sur les versions mises à jour de la structure OSGi (Apache Sling et Apache Felix) et du référentiel de contenu Java : Apache Jackrabbit Oak 1.10.2.
* Pour un aperçu des problèmes résolus, voir [Apache Jackrabbit Oak Jira v.1.10.0](https://archive.apache.org/dist/jackrabbit/oak/1.10.0/RELEASE-NOTES.txt), [Apache Jackrabbit Oak Jira v.1.10.1](https://archive.apache.org/dist/jackrabbit/oak/1.10.1/RELEASE-NOTES.txt) et [Apache Jackrabbit Oak Jira v.1.10.2](https://archive.apache.org/dist/jackrabbit/oak/1.10.2/RELEASE-NOTES.txt).

>[!CAUTION]
>
>La nouvelle version d’Oak Segment Tar présente depuis AEM 6.3 nécessite une migration de référentiel. Cette étape est obligatoire si vous effectuez une mise à niveau à partir d’une ancienne version de TarMK ou si vous souhaitez remplacer le nouveau Segment Tar par un autre type de persistance. Pour en savoir plus sur les avantages du nouveau Segment Tar, voir [FAQ sur la migration vers Oak Segment Tar](/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar).

#### OSGI {#osgi}

* Ajout des bibliothèques d’utilitaires OSGi Promises et Converter.

#### Sécurité {#security}

* Ajout de l’expiration du mot de passe pour l’utilisateur admin.

#### Serveur web {#web-server}

* La distribution Quickstart utilise Eclipse Jetty 9.4.15 comme moteur de servlet (AEM 6.4 fourni avec la version 9.3.22).

### [!DNL Experience Manager] Sites {#experience-manager-sites}

#### Applications monopages gérées {#managed-single-page-apps}

L’éditeur de page offre la possibilité de modifier le contenu et la composition/mise en page en contexte dans les expériences rendues côté client (également appelé [Editeur SPA](/help/sites-developing/spa-architecture.md)). Les applications monopages existantes créées avec l’infrastructure JavaScript React ou Angular peuvent être étendues avec le SDK AEM SJ afin d’être modifiables pour les professionnels.

Fourni d’abord dans le cadre d’AEM 6.4 SP2, la prise en charge de SPA dans AEM 6.5 propose les fonctionnalités suivantes :

* Utilisez l’éditeur de modèles pour modifier et configurer les parties modifiables AEM du SPA.
* Utilisez la gestion multisite pour créer des expériences SPA avec pays, franchise ou marque blanche.

#### Gestion de contenu découplé {#headless-content-management}

AEM a la capacité de servir le contenu dans divers formats et à différents niveaux de la pile. Certains existent depuis 2008 avec les [Sling GET](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) et les [Servlets POST](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html). Content Services ([exportateur de modèles Sling](https://docs.adobe.com/content/help/fr-FR/experience-manager-learn/foundation/development/develop-sling-model-exporter.html)) a été ajouté dans la version 6.3 et est la méthode utilisée par AEM SJ SDK pour hydrater les applications monopages. L’[API HTTP pour Assets](/help/assets/mac-api-assets.md) est une API CRUD, étendue pour AEM 6.5.

Nouvelles fonctionnalités de l’API HTTP :

* Ajout de la [prise en charge des fragments de contenu à l’API HTTP pour Assets](/help/assets/assets-api-content-fragments.md) pour créer, mettre à jour, lire et supprimer des fragments.
* Exposition des listes de fragments de contenu via Content Services avec le [composant principal de la liste de fragments de contenu](https://opensource.adobe.com/aem-core-wcm-components/library/content-fragment-list.html).
* [Bibliothèque de composants de principaux](https://opensource.adobe.com/aem-core-wcm-components/library.html) indiquant la sortie JSON par défaut de Content Services pour chaque composant

#### Module complémentaire Screens {#screens-add-on}

Concevez, diffusez et optimisez efficacement les expériences sur tous les écrans digitaux, depuis les kiosques interactifs jusqu’à la signalisation digitales.

* Unifiez les expériences et les contenus digitaux et en magasin avec une meilleure réutilisation des contenus
* Création simplifiée et workflows d’approbation/publication rationalisés avec prise en charge de Launches
* Éditez et diffusez des expériences interactives riches en utilisant SPA Editor
* Utilisation des lancements pour planifier les futures modifications de contenu pour le contenu de signalétique
* Lecture mesurée dans un canal de séquence
* Création automatique d’une structure de projet à l’aide d’un fichier source tel qu’une feuille Excel
* Prise en charge étendue des lecteurs multimédias avec un fonctionnement en ligne et hors ligne robuste (Smart Sync) capable de s’adapter aux réseaux de signalisation les plus vastes.
* Effectuez des personnalisations par emplacement ou configuration du contenu déclenché par les données en utilisant des espaces réservés dynamiques.
* Informations unifiées grâce à l’intégration d’Adobe Analytics dans le lecteur AEM Screens

Pour plus d’informations sur les modifications apportées à AEM Screens, voir les Notes de mise à jour dans la section [Guide de l’utilisateur d’AEM Screens](https://docs.adobe.com/content/help/fr-FR/experience-manager-screens/user-guide/aem-screens-introduction.html).

#### Développement de composants et de modèles {#component-amp-template-development}

* Maven Project Archetype 18+ pour les nouveaux projets, accédez à [Github pour les notes de mise à jour](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype/releases).
* Application monopage Maven Project Archetype 1.0.6+ pour les nouveaux projets, accédez à [Github pour les notes de mise à jour](https://github.com/adobe/aem-spa-project-archetype/releases).
* HTL version 1.4, accédez à [Github pour les notes de mise à jour](https://github.com/adobe/htl-spec/releases/tag/1.4).

   * Opérateur &quot;in&quot; pour les chaînes, les tableaux et les objets :

      ```html
      ${'a' in 'abc’}
      ${100 in myArray}
      ${'a' in myObject}
      ```

   * Déclarations de variables avec data-sly-set :
      `<sly data-sly-set.title="${currentPage.title}"/>${title}`

   * Paramètres de contrôle de liste et de répétition : début, étape, fin :
      `<h2 data-sly-repeat="${currentPage.listChildren @ begin = 1, step=2}">${item.title}</h2>`

   * Identifiants pour data-sly-unwrap :

      ```html
      <div data-sly-unwrap.isUnwrapped="${myCondition || myOtherCondition}">
      text <span data-sly-test="${isUnwrapped}>is unwrapped</code>
      </div>
      ```

   * Prise en charge des nombres négatifs

* Core Components 2.3.2+, accédez à [Github pour les notes de mise à jour](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/releases).
* Système de grille pour le conteneur de mises en page, voir [Github](https://github.com/Adobe-Marketing-Cloud/aem-responsivegrid).
* Gestionnaire de bibliothèques clientes : Le Compilateur de fermeture Google a été défini par défaut sur la minification des bibliothèques clientes JavaScript (l’ancienne valeur par défaut était Yahoo YUI) et le Compilateur de fermeture Google a été mis à jour vers la version v20190121.
* Éditeur de modèles et stratégies

   * Création et modification de modèles pour les applications monopages qui utilisent le SDK JS (également appelé éditeur de SPA)

* Pour le site de référence We.Retail 4.0, accédez à [Github pour les notes de mise à jour](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases).
* Kit d’outils pour mettre à niveau des sites existants afin d’exploiter les dernières fonctionnalités d’éditeur, voir [Référentiel Github](https://github.com/adobe/aem-modernize-tools)

>[!CAUTION]
>
>AEM inclut la version 1.12.4 de la bibliothèque jQuery afin de fournir une compatibilité maximale avec le code personnalisé existant. Adobe a procédé à des modifications de façon à résoudre les problèmes de sécurité connus.

#### Administration de sites {#site-administration}

* Le rail [Référence](/help/sites-authoring/author-environment-tools.md#references) comporte une nouvelle section permettant de répertorier les liens internes pointant vers la page sélectionnée. Cela s’avère utile lorsque vous envisagez de supprimer une page hors ligne ou de la supprimer, pour voir quelles pages doivent être ajustées avant de les mettre hors ligne.
* La [vue de liste](/help/sites-authoring/basic-handling.md#list-view) comporte une nouvelle colonne de workflow indiquant le statut de la page dans un workflow.
* Dans les [propriétés de la page](/help/sites-authoring/editing-page-properties.md), il est désormais possible de parcourir les ressources existantes en affectant une vignette à la page (onglet Vignette).

#### Éditeur de page {#page-editor}

* Autorisez l’édition en contexte et la composition d’expériences d’application monopage avec des composants côté client React et Angular utilisant le SDK JS (également appelé éditeur de SPA)
* Le mode Génération de modèles automatique s’affiche uniquement si la page possède une page de modèle automatique configurée.

#### Fragments de contenu et éditeur {#content-fragments-amp-editor}

* Nouveau rail [Annotations](/help/assets/content-fragments/content-fragments-variations.md#viewing-editing-deleting-annotations) dans l’éditeur de fragment de contenu permettant de faire des commentaires généraux et d’afficher des commentaires dans le texte (à afficher également dans le rail de la chronologie)
* Possibilité de définir le type de contenu par défaut d’un élément de texte multiligne dans une [Modèle de fragment de contenu](/help/assets/content-fragments/content-fragments-models.md) au texte simple, au texte enrichi ou au balisage
* Ajoutez des [commentaire/annotations](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment) en sélectionnant le texte dans l’éditeur de texte enrichi (vue plein écran)
* [Comparaison des différentes versions](/help/assets/content-fragments/content-fragments-managing.md#comparing-fragment-versions) d’un fragment de contenu côte à côte via le rail Référence
* Le rapport sur le téléchargement des ressources affiche désormais des fragments de contenu en conséquence
* Ajoutez [la prise en charge des fragments de contenu à l’API HTTP Assets](/help/assets/assets-api-content-fragments.md) par l’intermédiaire de /api.json. Il existe des API pour créer, mettre à jour, lire et supprimer des fragments de contenu.

#### Fragments d’expérience {#experience-fragments}

* Amélioration de l’indexation des [fragments d’expérience](/help/sites-authoring/experience-fragments.md) afin que leur contenu soit trouvé dans la recherche des pages où ils sont utilisés.
* L’option [Exporter vers la cible](/help/sites-administering/experience-fragments-target.md) permet désormais d’envoyer le fragment d’expérience sous forme de fichier JSON (HTML par défaut), ou les deux.

#### Traduction {#translation}

* Simplifiez la création de projets de traduction à l’aide de Project Masters
* Simplifiez l’exécution des projets de traduction en définissant les tâches de traduction sur l’état approuvé par défaut.
* Autorisez la mise à jour des pages traduites avec des modifications dans la mémoire de traduction tierce
* Autorisez l’exportation de travaux de traduction au format JSON
* Mise à jour de l’intégration de traduction Microsoft pour utiliser l’API V3

#### Gestion multisite (MSM, Multi-Site Management) {#multi-site-management-msm}

* Pour les configurations de déploiement qui utilisent PushOnModify, une meilleure gestion de l’opération de déplacement de page pour éviter des incohérences d’état
* La création d’une nouvelle page dans la structure de livecopy créera désormais par défaut une page autonome.
* Utilisation des fonctionnalités MSM dans les applications d’une seule page qui utilisent le SDK JS (également appelé Éditeur SPA)

#### Lancements {#launches}

* Nouveau workflow de révision et d’approbation pour les lancements et possibilité de promouvoir uniquement les pages de lancement approuvées
* Ajout d’une [ option dans l’interface utilisateur permettant de choisir la suppression du lancement juste après l’étape de promotion](/help/sites-authoring/launches-promoting.md#promoting-launch-pages)

#### Ciblage et simulation de contenu {#content-targeting-simulation}

* Le code JavaScript de la couche de données ContextHub et du moteur de règles côté client a été mis à jour pour utiliser jQuery 3 par défaut.

#### AEM et Adobe Target {#aem-amp-adobe-target}

>[!CAUTION]
>
>Actuellement :
>
>* Uniquement `at.js 1.x` est pris en charge si vous utilisez Adobe Target comme moteur de ciblage dans AEM console Activités.
>
>* Les `at.js. 1.x` et `at.js 2.x` sont pris en charge si vous utilisez l’exportation de fragments d’expérience vers Target et que vous exécutez des activités dans la console de Target.


* L’intégration Adobe Target peut désormais utiliser l’API Target Standard. Les versions précédentes d’AEM utilisent l’API HTTP Target Classic, désormais obsolète.
* Adobe Target `mbox.js` La version 63 est incluse. Adobe recommande vivement de passer de la mise en oeuvre à `at.js` v1.x.
* `at.js` La version 1.5.0 est désormais incluse. Adobe recommande d’utiliser [Adobe Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html) à configurer `at.js` v1.x sur le site.

#### AEM et Adobe Analytics {#aem-amp-adobe-analytics}

* `s_code.js` H.27.5 est inclus. Adobe recommande de passer de la mise en oeuvre à `AppMeasurement.js`
* `AppMeasurement.js` v1.8.0 est inclus. Adobe recommande d’utiliser [Adobe Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html) pour provisionner AppMeasurement.js dans le site.

#### AEM et commerce {#aem-commerce}

Les améliorations apportées à Commerce Integration Framework suivent un cycle de publication plus rapide depuis AEM 6.4. [En savoir plus ici](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/docs.html).

#### Module complémentaire Communities {#communities-add-on}

Pour obtenir la version la plus récente, consultez la section [Déploiement de Communities de la documentation.](/help/communities/deploy-communities.md)

##### Améliorations de l’engagement communautaire {#enhancements-to-community-engagement}

**@Mentions support**
AEM Communities permet désormais aux utilisateurs enregistrés de baliser (mentionner) d’autres membres enregistrés afin d’attirer leur attention, dans Contenu généré par l’utilisateur. Les membres balisés (mentionnés) sont ensuite notifiés, avec un lien profond vers le Contenu généré par l’utilisateur correspondant. Les utilisateurs peuvent toutefois choisir d’activer/de désactiver les notifications par e-mail et web.

![Prise en charge des mentions @](/help/release-notes/assets/at-mentions.png)

Les utilisateurs de la communauté n’ont pas besoin de rechercher leur prénom, leur nom ou leur nom d’utilisateur pour voir si quelqu’un les a contactés ou requiert leur attention. De plus, les auteurs de CGU peuvent demander une réponse à des utilisateurs enregistrés spécifiques pouvant résoudre le problème et ajouter des entrées.

Les administrateurs de la communauté doivent **Activer la mention** sur les composants de communauté pour permettre aux utilisateurs enregistrés d’utiliser la fonctionnalité sur ces composants.

**Messagerie de groupe** 

Les membres de la communauté enregistrés peuvent désormais envoyer des messages directs en masse aux groupes via un seul message e-mail, au lieu de renvoyer le même message à chaque membre du groupe. Pour autoriser [messagerie de groupe](/help/communities/configure-messaging.md), activez les deux instances de [Service des opérations de messagerie](/help/communities/messaging.md#group-messaging).

![Message de groupe](/help/release-notes/assets/group-messaging.png)

##### Améliorations apportées à la modération en bloc {#enhancements-to-bulk-moderation}

Filtres personnalisés dans la modération en bloc

[Filtres personnalisés](/help/communities/moderation.md#custom-filters) peut désormais être développé et ajouté à l’interface utilisateur de modération en bloc.

Un [exemple de projet](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter) illustrant le filtrage par balises est disponible dans [Github](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter). Ce projet peut être utilisé comme base pour développer des filtres personnalisés analogues.

![Filtres personnalisés](/help/release-notes/assets/custom-tag-filter.png)

**Vue de liste en modération en bloc** 

Une nouvelle vue de liste avec une interface utilisateur améliorée a été fournie dans la modération en bloc afin d’afficher les entrées de contenu généré par l’utilisateur.

![Modération en bloc en mode liste](/help/release-notes/assets/list-view-moderation.png)

##### Amélioration de la gestion des sites et des groupes {#enhancements-to-site-and-group-management}

**Administrateurs de sites côté Auteur et de groupes** 

Communities, à partir de la version AEM 6.5, permet une administration (et une gestion) décentralisée de différents sites et groupes/groupes imbriqués de communautés. Les organisations hébergeant plusieurs sites de communautés et groupes imbriqués peuvent désormais sélectionner des membres pour les rôles d’administrateur côté Auteur au moment de la création du site (et du groupe).

![Administrateur du site](/help/release-notes/assets/site-admin.png)

Les administrateurs de site peuvent créer un groupe à n’importe quel niveau de la hiérarchie et devenir les administrateurs par défaut. Ces administrateurs peuvent ensuite être supprimés par d’autres administrateurs de groupe. Les administrateurs de groupe peuvent gérer leur groupe G1 et créer un sous-groupe imbriqué sous G1.

##### Améliorations de l’activation {#enhancements-to-enablement}

**Prise en charge de SCORM 2017.1** 

La fonctionnalité d’activation d’AEM 6.5 Communities prend en charge le modèle de référence d’objet de contenu partageable. [(SCORM) 2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/) moteur.

* Prise en charge de la navigation au clavier sur les composants d’activation
* Les composants d’activation (par exemple, Lecture de catalogue et de cours, Affectations, Bibliothèque de fichiers) dans AEM Communities prennent en charge la navigation clavier pour une meilleure accessibilité.

##### Autres améliorations {#other-enhancements}

* Prise en charge de Solr 7
* AEM 6.5 Communities prend en charge la version Apache Solr 7.0 de la plateforme de recherche lors de la configuration de MSRP et DSRP.

### [!DNL Experience Manager Assets] {#experience-manager-assets}

AEM 6.5 propose les fonctionnalités et améliorations suivantes pour accroître la productivité des utilisateurs AEM, des rôles DAM et des rôles de création et de marketing associés.

#### Intégration avec [!DNL Adobe Creative Cloud] et workflows créatifs {#integration-with-adobe-creative-cloud-and-creative-workflows}

[!DNL Adobe Experience Manager] propose différentes manières de s’intégrer à et de partager des ressources à utiliser dans des workflows, où les équipes créatives et marketing ou les équipes d’entreprise collaborent étroitement.[!DNL Adobe Creative Cloud] [!DNL Experience Manager] 6.5 continue à améliorer l’intégration et à la rationaliser afin d’exposer davantage de possibilités et de rationaliser les méthodes existantes. 

Lisez ce qui suit pour connaître les fonctionnalités spécifiques et les intégrations de [!DNL Experience Manager] 6.5 que vous pouvez utiliser pour prendre en charge au mieux vos cas d’utilisation de vitesse du contenu.

##### Adobe Asset Link {#aal}

[!DNL Adobe Asset Link] renforce la collaboration entre les créatifs et les marketeurs dans le processus de création de contenu. Les créatifs peuvent accéder au contenu stocké dans [!DNL Experience Manager Assets], sans quitter les applications qui leur sont les plus familières. Les créatifs peuvent facilement parcourir, rechercher, extraire et archiver des ressources à l’aide du panneau intégré à l’application dans [!DNL Adobe Photoshop], [!DNL Adobe Illustrator], et [!DNL Adobe InDesign] applications.

[!DNL Adobe Asset Link] fait partie de [Creative Cloud pour entreprise](https://www.adobe.com/creativecloud/business/enterprise.html) offre. Pour plus d’informations à ce sujet, y compris la configuration nécessaire de votre [!DNL Experience Manager] déploiement, voir [Adobe d’un lien de ressource](https://helpx.adobe.com/fr/enterprise/using/adobe-asset-link.html).

![Recherche de ressources dans Adobe Photoshop](/help/release-notes/assets/asset_search_photoshop.png)

##### Intégration d’[!DNL Adobe Stock] {#stock}

Votre entreprise peut utiliser les [!DNL Adobe Stock] formule d’entreprise dans [!DNL Experience Manager Assets] pour vous assurer que les ressources sous licence sont largement disponibles pour vos projets de création et marketing. Vous pouvez rapidement rechercher, prévisualiser et obtenir une licence [!DNL Adobe Stock] ressources enregistrées dans Experience Manager, à l’aide des puissantes fonctionnalités de gestion des ressources numériques de [!DNL Experience Manager].

Le service [!DNL Adobe Stock] permet aux créateurs et aux entreprises d’accéder à des millions de photos, de vecteurs, d’illustrations, de vidéos, de modèles et de ressources 3D organisés, de haute qualité et libres de droits pour tous leurs projets de création. 

Pour plus d’informations, voir [Utilisation de ressources Adobe Stock dans Experience Manager Assets](/help/assets/aem-assets-adobe-stock.md).

![Aperçu d’une image et d’une licence Adobe Stock depuis Experience Manager Assets](/help/release-notes/assets/stock_image_preview_license_options.png)

*Figure : Aperçu [!DNL Adobe Stock] image et licence depuis l’intérieur [!DNL Experience Manager Assets].*

![Recherche et filtrage des images Adobe Stock sous licence dans Experience Manager](/help/release-notes/assets/aem-search-filters2.jpg)

*Figure : Recherchez et filtrez la licence [!DNL Adobe Stock] images dans [!DNL Experience Manager].*

##### Références dynamiques dans [!DNL Adobe InDesign] {#dynamic-references-in-indesign}

[!DNL Experience Manager Assets] utilisé dans [!DNL Adobe InDesign] sont dynamiques. Les références sont automatiquement mises à jour si les ressources référencées se déplacent dans le référentiel. Pour plus d’informations, voir [comment gérer des ressources composites](/help/assets/managing-linked-subassets.md).

#### Fonctionnalités de Brand Portal {#brand-portal-capabilities}

[!DNL Experience Manager Assets Brand Portal] vous permet d’acquérir facilement, de contrôler efficacement et de distribuer en toute sécurité les ressources approuvées aux fournisseurs/agences externes et aux utilisateurs professionnels internes sur tous les appareils. Il contribue à améliorer l’efficacité du partage des ressources, accélère la mise sur le marché des ressources et élimine le risque d’utilisation non conforme et d’accès non autorisé.

Pour plus d’informations, voir [Nouveautés de Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html?lang=fr).

#### Ressources connectées {#connectedassets}

Dans les grandes entreprises, l’infrastructure requise pour créer des sites web peut être distribuée. Parfois, les capacités de création de sites web et les ressources numériques requises résident dans différents silos.

[!DNL Experience Manager Sites] offre des fonctionnalités pour créer des pages web.  est le système de gestion des actifs numériques (DAM) qui fournit les ressources requises pour les sites web.[!DNL Experience Manager Assets] [!DNL Experience Manager] prend désormais en charge le cas d’utilisation ci-dessus en intégrant [!DNL Sites] et [!DNL Assets]. Voir [configuration et utilisation de la fonction Ressources connectées](/help/assets/use-assets-across-connected-assets-instances.md).

![Faites glisser une ressource depuis une [!DNL Experience Manager] déploiement sur un [!DNL Sites] d’une autre page [!DNL Experience Manager] déploiement](/help/release-notes/assets/connected-assets-drag-and-drop-only.gif)

*Figure : Faites glisser une ressource depuis une [!DNL Experience Manager] déploiement sur un [!DNL Sites] sur une autre page [!DNL Experience Manager] déploiement.*

#### Dynamic Media {#dynamic-media}

[!DNL Dynamic Media] fournit une création et une diffusion rich-media améliorées dans [!DNL Experience Manager Assets] pour générer des expériences de pointe immersives et personnalisées. En chargeant une seule ressource Principale de haute qualité et en utilisant les visionneuses et le rendu cloud avancé d’Adobe, vous pouvez diffuser n’importe quelle combinaison de rendus à la volée pour prendre en charge la stratégie multimédia de votre entreprise.

Pour plus d’informations sur les nouvelles [!DNL Dynamic Media] fonctions, voir [Notes de mise à jour de Dynamic Media](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/release-notes/s7rn2017.html).

##### Prise en charge vidéo 360 {#video-support}

Gérez vos fichiers vidéo 360 directement dans [!DNL Experience Manager] à l’aide des visionneuses de pointe pour diffuser des expériences VR sur les ordinateurs de bureau, les appareils mobiles et les casques VR. Pour plus d’informations, voir [Utilisation d’une vidéo 360](/help/assets/360-video.md).

##### Miniatures vidéo personnalisées {#custom-video-thumbnails}

Vous pouvez maintenant personnaliser les vignettes de vos ressources vidéo à l’aide d’images de la vidéo ou de tout autre contenu stocké dans DAM. Pour obtenir des instructions supplémentaires, voir [À propos des miniatures vidéo](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-scene-mode).

##### Amélioration de l’accessibilité {#accessibility-enhancements}

[!DNL Dynamic Media] Les visionneuses prennent désormais en charge les fonctionnalités d’accessibilité améliorées telles que la prise en charge d’Aria, les lecteurs d’écran et le texte de remplacement. Pour plus d’informations, voir [Guide de référence des visionneuses](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/homeviewers.html).

#### Amélioration de l’expérience de recherche {#experience-enhancement-for-searching}

[!DNL Experience Manager] À compter de la version 6.5, les marketeurs pourront découvrir plus rapidement les ressources souhaitées à partir de la page des résultats de recherche. Les facettes de recherche sont mises à jour avec le nombre de ressources avant même d’appliquer le filtre de recherche. L’affichage du nombre attendu par rapport au filtre aide les utilisateurs à naviguer efficacement dans les résultats de la recherche. Pour plus d’informations, voir [Recherche de ressources dans Experience Manager](/help/assets/search-assets.md).

![Afficher le nombre de ressources sans filtrer les résultats de la recherche dans les facettes de recherche](/help/assets/assets/asset_search_results_in_facets_filters.png)

*Figure : Afficher le nombre de ressources sans filtrer les résultats de la recherche dans les facettes de recherche.*

#### Amélioration de la convivialité {#usability-enhancement}

Vous pouvez désormais sélectionner toutes les ressources chargées dans un dossier ou à partir d’un résultat de recherche en une seule fois. Vous pouvez ainsi gérer plusieurs ressources rapidement. La case à cocher sélectionne toutes les ressources qui correspondent au scénario, par exemple un résultat de recherche, et pas seulement les ressources visibles dans la variable [!DNL Experience Manager] .

![Utilisez l’option Sélectionner tout pour sélectionner toutes les ressources chargées en un seul clic.](/help/release-notes/assets/select-all-in-aem-assets.gif)

*Figure : Utilisez l’option Sélectionner tout pour sélectionner toutes les ressources chargées en un seul clic.*

#### Améliorations des métadonnées {#metadata-enhancements}

[!DNL Assets] vous permet de créer des schémas de métadonnées pour les dossiers de ressources, qui définissent la mise en page et les métadonnées affichées dans les pages de propriétés du dossier. Vous pouvez désormais attribuer un schéma de métadonnées de dossier à un dossier existant ou lors de la création d’un dossier. Pour plus d’informations, consultez la section [Schéma de métadonnées de dossier](/help/assets/metadata-config.md#folder-metadata-schema).

Lors de la spécification des métadonnées en cascade, les options peuvent être chargées à partir d’un fichier JSON à l’exécution, au lieu de les saisir manuellement dans le formulaire. Pour plus d’informations, voir [métadonnées en cascade](/help/assets/metadata-schemas.md#cascading-metadata).

#### Amélioration des rapports {#reporting-enhancements}

Les fragments de contenu et les partages de lien sont désormais inclus dans le rapport téléchargé. Pour plus d’informations, consultez la section [Rapports d’Assets](/help/assets/asset-reports.md).

### [!DNL Adobe Experience Manager Forms] {#experience-manager-forms}

AEM Forms 6.5 comporte plusieurs nouvelles fonctionnalités et améliorations. En voici un aperçu :

* Rapports de transaction pour suivre le nombre de formulaires envoyés, de documents traités et de documents générés
* Amélioration de la convivialité des communications interactives
* Signatures numériques dans le cloud dans des formulaires adaptatifs
* Intégrez des formulaires adaptatifs et des communications interactives dans les applications monopages (SPA) d’AEM Sites.
* Prise en charge des variables dans les workflows AEM
* Prise en charge du modèle d’affichage des données dans les communications interactives
* Tri des formulaires adaptatifs et des tables de communication interactive
* Validation automatique des données d’entrée dans les modèles de données du formulaire

Voir [Résumé des nouvelles fonctionnalités et améliorations d’AEM 6.5 Forms](/help/forms/using/whats-new.md) pour plus d’informations sur les nouvelles fonctionnalités et les améliorations et les ressources de documentation.

### [!DNL Experience Manager Livefyre] {#experience-manager-livefyre}

Vous pouvez intégrer Livefyre à votre instance AEM 6.5. Voir [Comment intégrer Livefyre à AEM](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/livefyre.html).

### Exploitation du développement axé sur les clients {#leverage-customer-focused-development}

Adobe applique un modèle de développement axé sur les utilisateurs afin que ces derniers puissent contribuer à toutes les étapes du processus de développement, au cours des phases de spécification, de développement et de tests. Merci à tous les utilisateurs et partenaires qui contribuent à ce processus.

Adobe a mis en place les procédures et processus nécessaires à la collecte, à la hiérarchisation et au suivi de la résolution des bogues signalés par les utilisateurs et du développement des demandes d’amélioration. Le [Portail d’assistance pour les Experience Manager](https://experienceleague.adobe.com/?support-solution=Experience+Manager&amp;lang=fr#support) est intégré au système de suivi des défauts et des améliorations de l’Adobe. Si possible, les questions des clients sont identifiées et résolues par l’équipe du service clientèle. Lorsqu’elles sont transmises au service R&amp;D, toutes les informations client sont capturées et utilisées à des fins de hiérarchisation et de création de rapports. La priorité est donnée au développement à la prise en charge payante, aux problèmes de garantie et aux améliorations payantes du client.

Ce processus de hiérarchisation a généré plus de 750 modifications axées sur le client, corrigées dans AEM 6.5.

## Liste des fichiers faisant partie de la version {#list-of-files-that-are-part-of-the-release}

**Foundation**

* Démarrage rapide autonome : `cq-quickstart-6.5.0.jar`.
* Démarrage rapide du serveur d’applications : `cq-quickstart-6.5.0.war`.
* Dispatcher 4.3.2 ou version ultérieure pour les différents serveurs et plateformes web. Voir [lien de téléchargement](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/release-notes.html)
* Module externe pour Eclipse IDE ([plus d’infos et téléchargement](/help/sites-developing/aem-eclipse.md))

* Extension pour l’éditeur de code Brackets ([plus d’infos et téléchargement](/help/sites-developing/aem-brackets.md))
* Dépendances Maven/Gradle ([lien de téléchargement](https://repo1.maven.org/maven2/com/adobe/aem/uber-jar/6.5.0/))

**Sites**

* Composants de base ([projet GitHub](https://github.com/adobe/aem-core-wcm-components))
* Mise en œuvre de We.Retail Reference ([plus d’infos](/help/sites-developing/we-retail.md))
* Archétypes Maven Project :

   * pour les sites full-stack : [projet GitHub](https://github.com/adobe/aem-project-archetype) 
   * pour les applications monopages avec React / Angular : [projet GitHub](https://github.com/adobe/aem-spa-project-archetype) 

* Lecteurs AEM Screens pour différentes plateformes cibles ([téléchargement](https://download.macromedia.com/screens/))

* Modèles linguistiques pour le contenu dynamique. La version anglaise est préinstallée ; d’autres langues peuvent être téléchargées :

   * [Allemand](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html?lang=fr/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-fr)
   * [Espagnol](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html?lang=fr/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-fr)
   * [Italien](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html?lang=fr/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-fr)
   * [Français](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html?lang=fr/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-fr)

* AEM Modernize Tools Suite, par exemple. Outil de conversion de dialogue. ([Projet GitHub](https://github.com/adobe/aem-modernize-tools) )

**Ressources**

* Package permettant d’ajouter un rasteriseur PDF amélioré ([en savoir plus](/help/assets/aem-pdf-rasterizer.md))
* Module pour ajouter la prise en charge étendue des images RAW ([plus d’infos](/help/assets/camera-raw.md))

**Formulaires**

* [Packages pour les fonctionnalités AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)
* [SDK client AEM Forms OSGi](https://repo1.maven.org/maven2/com/adobe/aemfd/aemfd-client-sdk/)

## Langues {#languages}

L’interface utilisateur est disponible dans les langues suivantes :

* Anglais
* Allemand
* Français
* Espagnol
* Italien
* Portugais  brésilien
* Japonais
* Chinois simplifié
* Chinois traditionnel (prise en charge limitée)
* Coréen

[!DNL Experience Manager] 6.5 a été certifié dans le cadre de la norme GB18030-2005 CITS pour utiliser le codage des caractères chinois.

## Installation et mise à jour {#install-update}

Pour connaître les exigences de configuration, voir [instructions d’installation](/help/sites-deploying/custom-standalone-install.md).

Pour obtenir des instructions détaillées, voir [documentation de mise à niveau](/help/sites-deploying/upgrade.md).

## Plateformes prises en charge {#supported-platforms}

Recherchez la matrice complète des plateformes prises en charge, y compris le niveau de prise en charge sur [Exigences techniques AEM 6.5](/help/sites-deploying/technical-requirements.md).

>[!NOTE]
>
>Oracle est passé à un modèle de prise en charge à long terme (LTS) pour les produits Oracle Java SE. Java 9 et 10 sont des versions non-LTS par Oracle. Voir [Feuille de route du support Oracle Java SE](https://www.oracle.com/technetwork/java/eol-135779.html). Adobe prend en charge les versions LTS de Java pour exécuter uniquement les AEM en production. Java 11 est la version recommandée avec AEM 6.5.

## Fonctionnalités obsolètes et supprimées {#deprecated-and-removed-features}

Adobe évalue constamment les fonctionnalités du produit et prévoit au fil du temps de les remplacer par des versions plus puissantes ou de réimplémenter certains composants afin de mieux accommoder les futures attentes ou extensions.

Pour [!DNL Adobe Experience Manager] 6.5, [lire la liste des fonctionnalités obsolètes et supprimées](/help/release-notes/deprecated-removed-features.md). Cette page contient également une annonce préalable des modifications qui seront apportées dans un avenir proche et un avis important pour les clients qui mettent à jour des versions antérieures.

## Problèmes connus {#known-issues}

### Plateforme {#platform}

* Un problème est signalé lorsque le démarrage rapide CRX et son contenu sont supprimés.

   Sur chacune de ces actions, assurez-vous que la propriété `htmllibmanager.fileSystemOutputCacheLocation` n’est pas une chaîne vide :

   1. L’appel de la fonction `/libs/granite/ui/content/dumplibs.rebuild.html?invalidate=true`.
   2. Mise à niveau vers AEM 6.5.
   3. Exécution de la &quot;migration différée du contenu&quot; sur AEM 6.5.

   A [Base de connaissances](https://helpx.adobe.com/experience-manager/kb/avoid-crx-quickstart-deletion-in-aem-6-5.html) Cet article est disponible avec d’autres détails et la solution à ce problème.

* Si vous utilisez JDK 11 avec l’instance AEM 6.5, certaines pages peuvent s’afficher comme vides après le déploiement de certains modules. Le message d’erreur suivant s’affiche dans le fichier journal :

   ```java
   *ERROR* [OsgiInstallerImpl] org.apache.sling.scripting.sightly bundle org.apache.sling.scripting.sightly:1.1.2.1_4_0 (558)[org.apache.sling.scripting.sightly.impl.engine.extension.use.JavaUseProvider(3345)] : Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl)
   java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl
   ```

Pour résoudre cette erreur :

1. Désactivez l’instance AEM. Accédez à `<aem_server_path_on_server>crx-quickstart\conf` et ouvrez le `sling.properties` fichier . Adobe recommande de sauvegarder ce fichier.

1. Recherchez `org.osgi.framework.bootdelegation=`. Ajouter `jdk.internal.reflect,jdk.internal.reflect.*` pour afficher le résultat.

```java
org.osgi.framework.bootdelegation=sun.*,com.sun.*,jdk.internal.reflect,jdk.internal.reflect.*
```

1. Enregistrez le fichier et redémarrez l’instance AEM.

## Sites {#sites}

* **Utilisation des versions de page**: Si une page a été déplacée, vous ne pouvez plus effectuer d’aperçu sur les versions antérieures au déplacement.

### Ressources {#assets}

* **Rechercher :** La recherche ne renvoie aucun résultat si la chaîne de recherche contient des espaces au début ([OAK-4786](https://issues.apache.org/jira/browse/OAK-4786))
* **Schéma de métadonnées des dossiers** : après l’ajout d’un bouton de choix, les champs ID et Valeur ne sont pas restitués comme prévu et la fonctionnalité de suppression ne fonctionne pas. (CQ-4261144)
* Lors de l’attribution d’un nouveau nom à une ressource, il n’est pas possible d’utiliser un espace dans le nom. (CQ-4266403)

### Formulaires {#forms}

* Lorsque AEM Forms est installé sur un système d’exploitation Linux, la signature numérique avec le module de sécurité matérielle ne fonctionne pas. (CQ-4266721)
* (AEM Forms sur WebSphere uniquement) L’option **Forms Workflow**> **Recherche de tâche** ne renvoie aucun résultat si vous recherchez un **Administrateur** avec un **Nom d’utilisateur** comme critère de recherche. (CQ-4266457)

* AEM Forms ne parvient pas à convertir les fichiers TIF et de TIFF avec compression de JPEG en documents PDF. (CQ-4265972)
* Les options **Analyseur de ressources AEM Forms** et **Migration de la correspondance vers la communication interactive** ne fonctionnent pas sur la page **Migration d’AEM Forms**. (CQ-4266572)

* (JBoss 7 uniquement) Lorsque vous effectuez une mise à niveau d’une version précédente vers AEM 6.5 Forms et que la version précédente comporte des processus (.lca) qui ont créé et utilisé une copie du processus d’envoi ou de rendu par défaut, HTML5 Forms utilisant ces processus (.lca) ne parvient pas à effectuer les actions requises. (CQ-4243928)
* Dans une version adaptative, lorsqu’un service de modèle de données de formulaire est appelé à partir de l’éditeur de règle pour mettre à jour de manière dynamique les valeurs du composant de choix d’image, les valeurs du composant de choix d’image ne sont pas mises à jour. (CQ-4254754)
* Le programme d’installation d’AEM Forms Designer nécessite la version 32 bits de [Package d’exécution redistribuable Visual C++ 2012](https://support.microsoft.com/en-in/help/2977003/the-latest-supported-visual-c-downloads) et [Packages d’exécution redistribuables Visual C++ 2013](https://support.microsoft.com/en-in/help/3179560/update-for-visual-c-2013-and-visual-c-redistributable-package). Assurez-vous que les packages d’exécution redistribuables susmentionnés sont installés avant de démarrer l’installation. (CQ-4265668)

* PDF Generator ne prend pas en charge l’authentification par carte intelligente.  Lorsqu’un administrateur active la stratégie de groupe `Interactive Logon: Require Smart card` sur un serveur Windows, tous les utilisateurs de PDF Generator existants sont invalidés.

* Lorsqu’un formulaire adaptatif est configuré pour mettre à jour de manière dynamique les valeurs d’un composant et que l’instance de publication hébergeant le formulaire est accessible via le dispatcher, la fonctionnalité permettant de mettre à jour de manière dynamique les valeurs d’un champ cesse de fonctionner. Pour résoudre le problème, sur l’instance de publication, ouvrez CRXDE, accédez à `/libs/fd/af/runtime/clientlibs/guideChartReducer`et créez la propriété répertoriée ci-dessous.

   * Nom : allowProxy
   * Type : booléen
   * Valeur : vraie
   * Protégé : faux
   * Obligatoire : faux
   * Multiple : faux
   * Créé automatiquement : False

   La propriété permet aux bibliothèques clientes du dossier d’exécution d’accéder aux mandataires. (CQ-4268679)

* Au démarrage d’AEM Forms, la variable `SAX Security Manager could not be setup` s’affiche.
* Lorsque vous ouvrez un PDF protégé par AEM Forms Document Security sur un iOS Apple ou un iPadOS exécutant Adobe Acrobat Reader version 20.10.00.
* Lorsque vous envoyez un formulaire contenant un champ de chargement HTML standard d’un appareil iOS d’Apple, le contenu du fichier n’est parfois pas envoyé et un fichier de 0 octet est reçu à l’autre bout. Apple iOS 15.1 apporte un correctif pour le problème.

## Assistance technique et téléchargement du produit (sites à accès limité) {#product-download-and-support-restricted-sites}

Les sites suivants sont disponibles uniquement pour les clients . Si vous êtes client et avez besoin d’un accès, contactez votre responsable de compte Adobe.

* [Téléchargement du produit à l’adresse licensing.adobe.com](https://licensing.adobe.com/).

* Mises à jour de produit, correctifs et packages pour des fonctionnalités supplémentaires sur [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).

* [Service clientèle via Admin Console](https://adminconsole.adobe.com/). Pour plus d’informations, voir [Nouvelle expérience du service clientèle Adobe](https://docs.adobe.com/content/help/en/customer-one/using/home.html).
