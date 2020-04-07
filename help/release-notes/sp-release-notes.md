---
title: 'Notes de mise à jour d’AEM 6.5, Pack de services '
description: Notes de mise à jour spécifiques à Adobe Experience Manager 6.5 Service Pack 4.
uuid: c7bc3705-3d92-4e22-ad84-dc6002f6fa6c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: 25542769-84d1-459c-b33f-eabd8a535462
docset: aem65
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: fbe85c70ef993e4728bd76a327e1a27365cf1021

---


# Notes de mise à jour d’Adobe Experience Manager 6.5 Service Pack {#aem-service-pack-release-notes}

## Informations sur la version {#release-information}

| Produits | **Adobe Experience Manager 6.5** |
|---|---|
| Version | 6.5.4.0 |
| Type | Version du Service Pack |
| Date | 5 mars 2020 |
| URL de téléchargement | [PackageShare](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/AEM-6.5.4.0-Service-Pack), distribution [de logiciels (bêta)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.4.zip) |

## Eléments inclus dans Adobe Experience Manager 6.5.4.0 {#what-s-included-in-aem}

Adobe Experience Manager 6.5.4.0 est une mise à jour importante qui comprend de nouvelles fonctionnalités, les améliorations et les performances des clients clés, la stabilité et les améliorations de sécurité, publiées depuis la version 6.5 en **avril 2019**. Il peut être installé sur Adobe Experience Manager (AEM) 6.5.

Voici quelques-unes des principales fonctionnalités et améliorations introduites dans AEM 6.5.4.0 :

* AEM Assets est désormais configuré avec Brand Portal via la console d’E/S Adobe.

* Une nouvelle étape [Générer une sortie](../forms/using/aem-forms-workflow-step-reference.md) imprimable est désormais disponible pour les  de AEM Forms.

* [Prise en charge](../forms/using/resize-using-layout-mode.md) de plusieurs colonnes pour le mode de mise en page des formulaires adaptatifs et des communications interactives.

* Prise en charge du texte [](../forms/using/designing-form-template.md) enrichi dans les formulaires HTML5.

* [Améliorations](new-features-latest-service-pack.md#accessibility-enhancements) de l’accessibilité dans les ressources d’Experience Manager.

* Le référentiel intégré (Apache Jackrabbit Oak) a été mis à niveau vers la version 1.10.8.

* Vous pouvez désormais synchroniser des sous-arborescences de contenu sélectif avec le mode *Contenu* dynamique - Scene7 au lieu de toutes les sous-arborescences disponibles dans `content/dam`.

* L’intégration du modèle de données de formulaire avec le service Web SOAP prend désormais en charge les groupes de choix ou les attributs sur les éléments.

* L’entrée ou la sortie SOAP et les structures de données complexes prennent désormais en charge la substitution de groupe dynamique.

Pour une  complète des fonctionnalités, des points saillants clés et des fonctionnalités clés introduites dans les Service Packs AEM 6.5 précédents, reportez-vous à la page [Nouveautés d’Adobe Experience Manager 6.5 Service Pack 4](new-features-latest-service-pack.md).

### Sites {#sites-fixes}

* Lorsqu’une URL d’une page de sites AEM contient deux-points ( : ) ou symbole de pourcentage (%), le navigateur sous-jacent cesse de répondre et les cycles de l&#39;UC montrent un pic (NPR-32369, NPR-31918).

* Lorsqu’une page de sites AEM est ouverte pour modification et qu’un composant est copié, l’action de collage reste indisponible pour certains espaces réservés (NPR-32317).

* Lorsque l’assistant de gestion de la publication est ouvert, un fragment d’expérience lié à un composant principal ne s’affiche pas dans le  des références publiées (NPR-32233).

* L’aperçu de la copie en direct dans l’interface utilisateur tactile prend beaucoup plus de temps que l’interface utilisateur classique (NPR-32149).

* Lorsque l’heure du serveur et l’heure de la machine se trouvent dans des fuseaux horaires différents, l’heure de publication programmée affiche l’heure du serveur dans l’interface utilisateur tactile, tandis que l’heure de la machine s’affiche dans l’interface utilisateur classique (NPR-32077).

* Les sites AEM ne parviennent pas à ouvrir une page avec un suffixe dans l’URL (NPR-32072).

* Lorsqu’un utilisateur modifie un fragment de contenu, une variante supprimée du fragment de contenu est restaurée (NPR-32062).

* Les utilisateurs sont autorisés à enregistrer un fragment de contenu sans fournir d’informations dans les champs obligatoires (NPR-31988).

* kernel.js et ui.js ne sont pas pré-respectés ni mis en cache. Cela donne plus de temps aux pages de rendu (NPR-31891).

* Lorsque PageEventAuditListener est activé, la longueur de la file d&#39;attente de validation augmente. Elle influe sur les performances de nombreuses opérations, telles que la publication en masse, la navigation et le mouvement des ressources en vrac (NPR-31890).

* Lorsque vous faites glisser des fragments d’expérience, un temps de réponse élevé est observé (NPR-31878).

* Lorsque vous sélectionnez l’option Faire glisser le composant ici dans l’espace réservé d’une grille dynamique, une requête GET est envoyée et la requête génère une erreur HTTP 403 (NPR-31845).

* Lorsque vous déplacez le contenu dans le même dossier, l’option de déplacement de page est désactivée (NPR-31840).

* En mode de structure des modèles modifiables, le de composants autorisés dans le de mise en page  affiche des résultats incorrects. Seuls les composants avec boîte de dialogue de conception s’affichent dans le  de mise en page (NPR-31816).

* Lorsqu’une page dispose d’autorisations en lecture seule pour un utilisateur, l’option Ouvrir les propriétés est visible dans sites.html, mais pas dans editor.html (NPR-31770).

* Lorsqu’un utilisateur clique sur le bouton Créer, l’option de page n’est pas disponible (NPR-31756).

* Impossible de synchroniser la campagne dans la campagne Adobe contenant le composant d’importateur de conception prêtes à l’emploi (prêtes à l’emploi) (NPR-31728).

* Lorsque vous essayez de changer un à puces en numéroté, seuls les deux premiers éléments de l&#39; sont modifiés (NPR-31636).

* Lorsqu’une page n’est pas créée et que le noeud enfant est sélectionné, le dialogue de sélection affiche toujours le noeud initial. Lorsque la page est créée et que l’utilisateur clique sur Parcourir, la page est redirigée vers le noeud racine au lieu du noeud créé (NPR-31618).

* La boîte de dialogue de configuration des  du ne fonctionne pas correctement pour la fonctionnalité de flux de travail de personnalisation de la boîte de réception (NPR-32503 et NPR-32492).

* Un message d’erreur s’affiche lors de l’affichage des informations de flux de travail à l’aide de la boîte de réception (CQ-4282168).

### Ressources {#assets-6540-enhancements}

* Le bouton permettant de déclencher le processus sur la page de collecte des ressources est désactivé (NPR-32471).

* Un dossier sans nom est créé dans SPS (Scene7 Publishing System) lors du déplacement d’un fichier d’un dossier vers un autre dans Experience Manager avec la configuration de Dynamic Media Scene7 (NPR-32440).

* L’action de déplacement de toutes les ressources (à l’aide de Sélectionner tout, puis de déplacer) vers un dossier contenant les ressources publiées échoue avec erreur (NPR-32366).

* La génération de rendu pour les ressources avec ${extension} échoue (NPR-32294).

* Les URL d’historique des versions sont affichées sous le champ Référencé par sur la page de propriétés des ressources (NPR-31889).

* Impossible d&#39;ouvrir le fichier ZIP téléchargé à partir de DAM à l&#39;aide de WinZip (NPR-32293).

* Les autorisations d’origine d’un dossier sont mises à jour lorsque les paramètres du dossier sont ouverts pour modifier le titre du dossier ou l’image miniature, puis enregistrés (NPR-32292).

* L’icône de calendrier pour   planifié ne s’affiche pas dans la colonne État (dans l’interface utilisateur classique de la liste des ressources de la gestion des actifs numériques) pour les actifs dont le  est planifié pour une date et une heure ultérieures (NPR-32291).

* La création d’extraits de code à l’aide de modèles d’extraits de code génère une erreur lors de la recherche de collections au cours du processus de création d’extraits de code (NPR-32290).

* Plusieurs de recherche sont déclenchés lorsque plusieurs balises sont sélectionnées à partir du filtre de recherche (NPR-32143).

* L’interface utilisateur Ressources d’Experience Manager affiche les noms de fichier tronqués lorsque des fichiers comportant plus de 50 caractères dans le nom de fichier sont téléchargés (NPR-32054).

* Toutes les cases à cocher du panneau Filtre sont désactivées lorsque les première et deuxième cases sont désactivées, lorsque les cases de niveau 2 de l’arborescence des cases à cocher dans Adobe Stock étaient sélectionnées (NPR-31919).

* La recherche de fichiers et de dossiers à l&#39;aide des facettes Omnisearch donne une exception (NPR-31872).

* La mise en surbrillance des champs pour la sélection obligatoire des champs dans l’éditeur de métadonnées n’est pas supprimée, même après la sélection du champ requis, lorsque les règles de dépendance sont définies dans le formulaire de de métadonnées correspondant (NPR-31834).

* Les noms complets des balises de niveau feuille (issus de la hiérarchie des balises) ne s’affichent pas dans la page Propriétés de la ressource (NPR-31820).

* L’utilisation de la commande Précédent de la page Propriétés du fichier dans le navigateur Safari provoque une erreur (NPR-31753).

* La recherche tactile dans l&#39;interface utilisateur (effectuée par l&#39;intermédiaire d&#39;Omnisearch) fait défiler automatiquement la page de résultats vers le haut et perd la position de défilement de l&#39;utilisateur (NPR-31307).

* La page des détails des ressources des fichiers PDF n’affiche pas les boutons d’action, à l’exception des boutons A la collection et Ajouter Rendu dans Experience Manager s’exécutant sur le mode d’exécution Contenu multimédia dynamique Scene7 (CQ-4286705).

* Le traitement des fichiers prend trop de temps lors du processus de téléchargement par lot de Scene7 (CQ-4286445).

* Le bouton Enregistrer n’importe pas la visionneuse distante lorsque l’utilisateur n’a apporté aucune modification à l’éditeur de visionneuses dans le client de média dynamique (CQ-4285690).

* La miniature de fichier 3D n’est pas informative lorsqu’un modèle 3D pris en charge est assimilé à AEM (CQ-4283701).

* L’état non traité du paramètre prédéfini de la visionneuse de vidéos de recadrage dynamique s’affiche deux fois sur le texte de la bannière en regard du nom du paramètre prédéfini (CQ-4283517).

* La hauteur  d’un modèle 3D téléchargé prévisualisé dans la visionneuse 3D est incorrecte sur la page de détails de la ressource (CQ-4283309).

* L’éditeur de carrousel ne s’ouvre pas dans IE 11 en mode hybride Contenu multimédia dynamique Experience Manager (CQ-4255590).

* Le focus clavier est bloqué dans la liste déroulante Courrier électronique dans la boîte de dialogue Télécharger, dans les navigateurs Chrome et Safari (NPR-32067).

* La case à cocher Synchroniser tout le contenu n’est pas activée par défaut lors de l’ajout de la configuration du cloud DM sur AEM (CQ-4288533).

### Interface utilisateur de Foundation {#foundation-ui-6540}

* La commande de la souris passe au champ de filtre précédent au lieu de rester dans le champ de filtre existant lors de la recherche de fichiers à l’aide du panneau Filtre (NPR-32538).

* Balisage de plateforme : La recherche de balises en saisissant dans les champs de balise affiche les balises en dehors des limites racine et ne respecte pas la `rootPath` propriété des champs de balise (NPR-31895).

* Interface utilisateur de la plateforme : Le navigateur de chemins est rompu si un chemin non valide est ajouté dans le champ de texte (NPR-31884).

* La notification est masquée derrière un menu collant lors de la sélection de la page (NPR-31628).

### Plate-forme {#platform-sling-6540}

* (HTL) Les traits de soulignement remplacent les deux-points dans la section de chemin de l’URL (NPR-32231).

### Projets {#projects-6540}

* Le bouton Créer n’est pas visible pour l’utilisateur même s’il est autorisé à créer un projet dans le sous-dossier (NPR-31832).

### Traduction de projets {#projects-translation-6540}

* La création du projet de traduction rompt l’interface utilisateur lorsque l’option Raccorder les espaces est activée dans `Apache Sling JSP Script Handler` (NPR-32154).

* Une erreur dans l’interface utilisateur et une exception de point nul dans les journaux d’erreurs est observée lorsqu’une balise, à traduire, est ajoutée à un projet de traduction (NPR-31896).

### Intégrations {#integrations-6540}

* La génération d’URL de bibliothèque de lancement repose uniquement sur les `path` valeurs et les `library_name` valeurs de l’API de lancement et n’est pas basée sur `library_path` la valeur (NPR-31550).

* Un message d’erreur s’affiche lors du traitement des éléments associés à LiveJournal (FYR-12420).

### Editeur de modèles WCM {#wcm-template-editor-6540}

* En mode de structure des modèles modifiables, les composants autorisés  dans le de mise en page  ne s’affichent pas dans le composant de bouton de lien (CQ-4282099).

### WCM Page Editor {#wcm-page-editor-6540}

* Une erreur s’est produite lors de la sélection d’une incrustation, puis de la sélection des composants Glisser les éléments réactifs dans la grille (CQ-4283342).

### Campaign Targeting {#campaign-targeting-6540}

* Échec de la configuration du cloud  avec l’erreur d’obtention de la demande de mbox (CQ-4279880).

### Brand Portal {#assets-brand-portal}

* Les utilisateurs du portail de marque ne peuvent pas publier les ressources du dossier de contributions vers AEM Assets lors de la mise à niveau vers les E/S Adobe sur AEM 6.5.4 (CQDOC-15655).

   Ce problème sera corrigé dans le prochain Service Pack AEM 6.5.5.

   Pour un correctif immédiat sur AEM 6.5.4, il est recommandé de [télécharger le correctif](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/hotfix/cq-6.5.0-hotfix-33041) et de l’installer sur votre instance d’auteur.


* Les valeurs de la liste déroulante des  de métadonnées ne sont pas visibles dans les propriétés des ressources (CQ-4283287).

* Le sous-schéma de métadonnées n’affiche pas les onglets basés sur le mimetype dans les propriétés de la ressource (CQ-4283288).

* L’annulation de la publication d’un schéma de métadonnées renvoie un message d’erreur bien que le schéma soit supprimé du serveur principal.

* Les images  ne s’affichent pas pour un fichier publié (CQ-4285886).

* L’utilisateur ne peut pas publier ou annuler la publication de fichiers dont le nom contient un guillemet simple (CQ-4272686).

* Les termes et conditions ne s’affichent pas lors du téléchargement de plusieurs ressources (CQ-4281224).

* Des vulnérabilités mineures de sécurité ont été corrigées.

### Communities {#communities}

* Le formulaire Créer un membre s’affiche en tant que page vierge (NPR-31997).

* L’utilisateur ne peut pas  le rapport Analytics sur l’instance d’auteur (NPR-30913).

### Oak- Indexation et {#oak-indexing-6540}

* MS Word et MS Excel, contenant une image JPEG, quand l&#39;analyseur Tika échoue à analyser et une erreur de classe non trouvée est observée (NPR-31952).

### Forms {#forms-6530}

>[!NOTE]
>
>Le Service Pack AEM n’inclut pas de correctifs pour AEM Forms. Les correctifs sont fournis à l’aide d’un module complémentaire Forms distinct.  En outre, un programme d’installation cumulatif est publié, qui comprend des correctifs pour AEM Forms sur JEE. For more information, see [Install AEM Forms add-on](#install-aem-forms-add-on-package) and [Install AEM Forms on JEE](#install-aem-forms-jee-installer).

* Correspondence Management : Les lettres affichent des caractères supplémentaires après envoi vers les  post-traitement (NPR-32626).

* Correspondence Management : Les lettres affichent une balise d’emplacement de liste déroulante en tant que composant de texte après envoi vers le post-processus (NPR-32539).

* Correspondence Management : Les valeurs par défaut définies dans le modèle de lettre ne s’affichent pas en mode  (NPR-32511).

* Mobile Forms : Le bouton d’envoi s’affiche avec une taille agrandie lors du rendu d’un formulaire XDP dans une version HTML (NPR-32514).

* Services de  : Problèmes d’accès aux URL pour les lettres et d’autres pages après l’application du Service Pack 2 (NPR-32508, NPR-32509).

* Services de  : Si le nombre de transactions sur un serveur dépasse une limite spécifique, la conversion HTML vers PDF échoue et les paramètres de type de fichier sont supprimés du serveur AEM Forms (NPR-32204).

* Formulaires adaptatifs : L’outil d’accessibilité du navigateur signale les échecs dans les formulaires adaptatifs conformément aux directives WCAG2 Level AA (NPR-32312, NPR-32309, CQ-4285439).

* Formulaires adaptatifs : L’outil d’accessibilité du navigateur Chrome signale une erreur de bonne pratique (NPR-32310).

* Formulaires adaptatifs : Problèmes de traduction lors de la configuration d’un formulaire adaptatif incorporé dans une page de sites AEM (NPR-32168).

* Workbench : Un message d’erreur s’affiche lors de l’utilisation du service Get PDF Properties for PDF Utilities (NPR-32150).

* Sécurité  : Un fichier PDF protégé ne parvient pas à s’ouvrir hors ligne avec l’option DisableGlobalOfflineSynchronizationData définie sur True (NPR-32078).

* Designer : Si l’option de balisage est activée, la bordure du sous-formulaire disparaît dans la sortie PDF générée (NPR-32547, NPR-31983, NPR-31950).

* Designer : S’il existe des cellules fusionnées dans un tableau, le test d’accessibilité échoue pour le fichier PDF de sortie converti à partir d’un formulaire XDP à l’aide du service de sortie (CQ-4285372).

* Foundation JEE : Si un serveur AEM Forms est déconnecté d’une grappe, des problèmes de mise en cache l’empêchent de se reconnecter au serveur (NPR-32412).

## Install 6.5.4.0 {#install}

**Conditions requises**

* AEM 6.5.4.0 requires AEM 6.5. Check [upgrade documentation](/help/sites-deploying/upgrade.md) for detailed instructions.
* Le Service Pack peut être téléchargé sur Adobe Package Share, accessible directement depuis l’instance AEM 6.5.
* Lors d’un déploiement avec MongoDB et plusieurs instances, installez AEM 6.5.4.0 sur l’une des instances d’auteur à l’aide du gestionnaire de modules.
* Avant d’installer le pack de service, veillez à disposer d’un instantané ou d’une nouvelle sauvegarde de votre instance AEM.
* Redémarrez l’instance avant l’installation. Cela est nécessaire uniquement lorsque l’instance reste en mode de mise à jour (ce qui est le cas lorsque l’instance vient d’être mise à jour depuis une version antérieure). Toutefois, cela est recommandé si l’instance s’est exécutée pendant une longue durée.

>[!CAUTION]
>
>Adobe recommande de ne pas supprimer ni désinstaller le package AEM 6.5.4.0.

### Installation du Service Pack au moyen de Package Share {#install-service-pack-via-package-share}

Accomplissez les étapes suivantes pour installer le Service Pack sur une instance 6.5 existante :

1. Login to Package Share from within AEM or directly from your browser and download the [AEM 6.5.4.0 package](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/AEM-6.5.4.0-Service-Pack).

1. Installez le package téléchargé à l’aide du gestionnaire de modules.

>[!NOTE]
>
>**La boîte de dialogue sur l’interface utilisateur de Package Manager se ferme parfois de manière impromptue lors de l’installation de la version 6.5.4.0**
>
>Il est donc recommandé d’attendre que les journaux d’erreurs se stabilisent avant d’accéder à l’instance. L’utilisateur doit attendre les journaux spécifiques liés à la désinstallation du lot de mise à jour avant de s’assurer que les installations sont réussies. Cela se produit généralement sur Safari, mais peut se produire par intermittence sur n’importe quel navigateur.

**Installation automatique**

Il existe deux manières d’installer automatiquement AEM 6.5.4.0 dans une instance en cours d’exécution :

A. Placez le package dans le dossier ..*/crx-quickstart/install* alors que le serveur est disponible en ligne. Le package est automatiquement installé.

B. Use the [HTTP API from Package Manager](https://docs.adobe.com/content/docs/en/crx/2-3/how_to/package_manager.html) - make sure that you use cmd=install&amp;recursive=true - so the nested packages  are  installed.

>[!NOTE]
>
>AEM 6.5.4.0 ne prend pas en charge l’installation de Bootstrap.

**Validation de l’installation**

1. La page Informations sur le produit (/system/console/ productinfo) affiche la chaîne de version mise à jour `Adobe Experience Manager, Version 6.5.4.0` sous Produits installés.

1. All  OSGi  bundles are either **[!UICONTROL ACTIVE]** or **[!UICONTROL FRAGMENT]** in the OSGi Console (Use Web Console: /system/console/bundles).
1. Le lot OSGI org.apache.jackrabbit.oak-core est sur la version 1.10.6 ou ultérieure (utilisez la console Web : /system/console/bundles).

In order to see what platforms are certified to run with this release, please refer to the [Technical Requirements](/help/sites-deploying/technical-requirements.md).

### Installation du module complémentaire AEM Forms {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Passez cette étape si vous n’utilisez pas AEM Forms. Les correctifs dans AEM Forms sont fournis dans un module complémentaire distinct.

>[!NOTE]
>
>AEM 6.5.4.0 includes a new version of [AEM Forms Compatibility package](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/compatpack/AEM-FORMS-6.5.3.0-COMPAT). Si vous utilisez une ancienne version du package de compatibilité d’AEM Forms et que vous mettez à jour vers AEM 6.5.4.0, installez la dernière version du package de compatibilité d’AEM Forms après l’installation du package de module complémentaire de Forms.

1. Vérifiez que vous avez installé le Service Pack AEM.
1. Download the corresponding Forms add-on package listed at [AEM Forms releases](https://helpx.adobe.com/fr/aem-forms/kb/aem-forms-releases.html) for your operating system.
1. Install the Forms add-on package as described in [Installing AEM Forms add-on packages](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

### Install AEM Forms on JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Passez cette étape si vous n’utilisez pas AEM Forms sous JEE. Les correctifs d’AEM Forms sur JEE sont fournis par le biais d’un programme d’installation distinct.

For information about installing the cumulative installer for AEM Forms on JEE and post-deployment configuration, see the [release notes for patch 0011](https://helpx.adobe.com/aem-forms/quick-fixes/6-5/jee-patch-0011.html).

#### Programme d’installation de Workbench

Comme il s’agit d’un programme d’installation complet, la taille du fichier est plus grande que celle du correctif. Désinstallez la version précédente de Workbench avant d’installer la nouvelle version.

### UberJar {#uber-jar}

The UberJar for AEM 6.5.4.0 is available in the [Adobe Public Maven repository](https://repo.adobe.com/nexus/content/groups/public/com/adobe/aem/uber-jar/6.5.4/).

La version mise à jour d’UberJar pour la version 6.5.4.0, qui inclut le package **com.fasterxml.jackson.core.async** , est disponible dans le référentiel [](https://repo.adobe.com/nexus/content/groups/public/com/adobe/aem/uber-jar/6.5.4-1.0/)Adobe Public Maven.

To use UberJar in a Maven project, refer to the article, [How to use UberJar](/help/sites-developing/ht-projects-maven.md) and include the following dependency in your project POM:

```shell
<dependency>
      <groupId>com.adobe.aem</groupId>
      <artifactId>uber-jar</artifactId>
      <version>6.5.4</version>
      <classifier>apis</classifier>
      <scope>provided</scope>
</dependency>
```

## Fonctionnalités obsolètes {#removed-deprecated-features}

Cette section les fonctionnalités et fonctionnalités qui ont été marquées comme obsolètes avec AEM 6.5.4.0. Les fonctionnalités qui doivent être supprimées dans une version ultérieure sont d’abord désapprouvées, avec une autre option à utiliser.

Il est conseillé aux clients de vérifier s’ils utilisent la fonctionnalité ou la fonctionnalité dans leur déploiement actuel et de prévoir de modifier leur mise en oeuvre pour utiliser l’autre option.

| Zone | Fonctionnalité | Remplacement |
|---|---|---|
| Intégrations | The **[!UICONTROL AEM Cloud Services Opt-In]** screen has been deprecated. L’intégration d’AEM et de  ayant été mise à jour dans AEM 6.5 pour prendre en charge l’API  Standard, qui utilise l’authentification via Adobe IMS et les E/S, et le rôle croissant d’Adobe Launch pour l’instrumentation des pages AEM pour l’analyse et la personnalisation, l’assistant d’inclusion est devenu non pertinent du point de vue fonctionnel. | Configuration des connexions système, de l’authentification IMS Adobe et des intégrations d’E/S Adobe via les services cloud AEM respectifs |

## Problèmes connus {#known-issues}

* Si l’assistant de configuration **des ressources** connectées renvoie un message d’erreur 404 après l’installation, réinstallez manuellement les packages **cq-remotedam-client-ui-content** et **cq-remotedam-client-ui-components** à l’aide de Package Manager.
* Les erreurs et messages d’avertissement suivants peuvent s’afficher lors de l’installation d’AEM 6.5.x.x :
   * « Lorsque l’intégration de Target est configurée dans AEM à l’aide de l’API Target Standard (authentification IMS), l’exportation de fragments d’expérience vers Target entraîne la création de types d’offres incorrects. Au lieu du type « Fragment d’expérience » / source « Adobe Experience Manager », Target crée plusieurs offres avec le type « HTML » / source « Adobe Target Classic ».
   * com.adobe.granite.maintenance.impl.TaskScheduler : Aucune fenêtre de maintenance n&#39;a été trouvée sur le granite/operations/maintenance
   * La validation côté serveur du formulaire adaptatif échoue lorsque  fonctions  telles que SUM, MAX et MIN sont utilisées. CQ-4274424
   * com.adobe.granite.maintenance.impl.TaskScheduler - Aucune fenêtre de maintenance n’a été trouvée sur granite/operations/maintenance.
   * La zone réactive d’une image interactive de média dynamique n’est pas visible lors de la prévisualisation du fichier via la visionneuse de bannières modifiables.

## OSGi bundles and content packages included {#osgi-bundles-and-content-packages-included}

Les documents texte suivants répertorient les lots OSGi et les packages de contenu inclus dans AEM 6.5.4.0.

Liste des lots OSGi inclus dans AEM 6.5.4.0

[Obtenir le fichier](assets/6540_bundles.txt)

Liste des packages de contenu inclus dans AEM 6.5.4.0

[Obtenir le fichier](assets/6540_packages.txt)

## Restricted sites {#restricted-sites}

Ces sites sont réservés aux clients. Si vous êtes client et avez besoin d’un accès, contactez votre responsable de compte Adobe.

* [Téléchargement du produit à l’adresse licensing.adobe.com](https://licensing.adobe.com/)
* [Contactez l&#39;assistance](https://daycare.day.com/public/contact.html)clientèle Pour plus d&#39;informations sur l&#39;accès au portail d&#39;assistance, consultez [Accès au portail](https://helpx.adobe.com/fr/experience-manager/kb/accessing-aem-support-portal.html)d&#39;assistance.

>[!MORE COMME ÇA]
>
>* [Notes de mise à jour d’AEM 6.5](/help/release-notes/release-notes.md)
>* [Page de produits AEM ](https://www.adobe.com/solutions/web-experience-management.html)
>* [Documentation d’AEM 6.5](https://helpx.adobe.com/fr/support/experience-manager/6-5.html)
>* Subscribe to [Adobe priority product updates](https://www.adobe.com/subscription/priority-product-update.html)

