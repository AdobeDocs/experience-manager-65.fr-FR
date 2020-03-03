---
title: 'Notes de mise à jour d’AEM 6.5, Pack de services '
description: Notes de mise à jour spécifiques à Adobe Experience Manager 6.5 Service Pack 3.
uuid: c7bc3705-3d92-4e22-ad84-dc6002f6fa6c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: 25542769-84d1-459c-b33f-eabd8a535462
docset: aem65
translation-type: tm+mt
source-git-commit: 9f4a460c7f64d86e35e950e512ed5b6cda1cbf2a

---


# Notes de mise à jour d’Adobe Experience Manager 6.5 Service Pack {#aem-service-pack-release-notes}

## Informations sur la version {#release-information}

| Produits | **Adobe Experience Manager 6.5** |
|---|---|
| Version | 6.5.3.0 |
| Type | Version du Service Pack |
| Date | 12 décembre 2019 |
| URL de téléchargement | [PackageShare](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/servicepack/AEM-6.5.3.0) |

## Eléments inclus dans Adobe Experience Manager 6.5.3.0 {#what-s-included-in-aem}

Adobe Experience Manager 6.5.3.0 is an important release that includes performance, stability, security, and key customer fixes and enhancements released since the general availability of 6.5 release in **April 2019**. Il peut être installé sur Adobe Experience Manager (AEM) 6.5.

Les principaux points forts de cette version du Service Pack incluent les éléments suivants :

* Le référentiel intégré (Apache Jackrabbit Oak) a été mis à niveau vers la version 1.10.6.

* Experience Manager Assets prend désormais en charge les archives ZIP créées à l’aide de l’algorithme Deflate 64.

* Une nouvelle colonne pour la date de création, qui peut être triée, a été ajoutée en mode Liste DAM et dans les résultats de la recherche de ressources en mode Liste.

* Le tri des ressources basé sur la colonne Nom a été activé en mode Liste.

* Les médias dynamiques prennent désormais en charge les fichiers vidéo de recadrage dynamique. Smart Crop est une fonction pilotée par l’apprentissage automatique qui recadre une vidéo tout en déplaçant le cadre pour suivre le point focal de la scène.

* Dynamic Media prend en charge l’imagerie dynamique.

* Possibilité de [définir des préférences d’absence du bureau](../forms/using/configure-out-of-office-settings.md) dans les processus AEM.

* Possibilité de [partager des éléments](../forms/using/configure-shared-queues-osgi.md) de boîte de réception ou de boîte de réception avec d’autres utilisateurs dans les processus AEM.

* Possibilité de [générer des communications interactives en mode](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)Batch.

* Mise à jour de la version de jQuery intégrée dans ContextHub vers la version 3.4.1.

### Liste des modifications     {#list-of-changes}

#### Assets {#assets-6530-enhancements}

**Améliorations apportées au produit**

* Experience Manager Assets prend désormais en charge les archives ZIP créées à l’aide de l’algorithme Deflate 64 (NPR-27573).

* Une nouvelle colonne pour la date de création, qui peut être triée, a été ajoutée en mode Liste DAM et dans les résultats de la recherche de ressources en mode Liste (NPR-31312).

* Le tri des ressources basé sur la colonne Nom a été autorisé en mode Liste (NPR-31299).

* Les fichiers GLB, GLTF, OBJ et STL prennent en charge l’aperçu des ressources dans la page Détails des ressources dans DAM (CQ-4282277).

* L’événement ReplicationOnModifyListener est déclenché pour les noeuds de blocs lors du transfert de blocs dans le contenu multimédia dynamique (CQ-4281279).

* Les médias dynamiques prennent désormais en charge les fichiers vidéo de recadrage dynamique. Smart Crop est une fonction pilotée par l’apprentissage automatique qui recadre une vidéo tout en déplaçant le cadre pour suivre le point focal de la scène (CQ-4278995).

* Dynamic Media prend en charge l’imagerie intelligente (CQ-4222249).

* La vue de recherche/navigation a été définie comme vue par défaut dans le sélecteur Foundation si les paramètres de requête sont transmis dans la requête (NPR-31601).

**Correctifs**

* Les métadonnées de certains documents PDF ne sont pas mises à jour et enregistrées dans le PDF lors de la modification de son titre (NPR-31629).

* Le partage des ressources ne fonctionne pas pour les ressources dont le nom contient le caractère &quot;+&quot; (NPR-31547).

* Les modifications dans le formulaire de recherche par défaut Administration des ressources * Rail de recherche ne fonctionnent pas comme prévu (NPR-31502).

* Les suggestions ne sont pas affichées lors de l&#39;utilisation d&#39;Omnisearch sur la vue des ressources pour la recherche de ressources (NPR-31496).

* Les références de ressources dans les collections ne sont pas mises à jour lorsque les ressources référencées sont déplacées vers un autre emplacement, dans les cas où les mêmes ressources sont référencées par une collection différente par différents utilisateurs (NPR-31486).

* Les balises IPTC en double sont ajoutées aux métadonnées de fichier (NPR-31328).

* Le nombre de résultats de la recherche dans le coin supérieur droit ne se met pas à jour correctement lorsque la recherche est déclenchée à partir du rail de filtre (NPR-31316).

* Toutes les cases à cocher sont désactivées lorsque vous décochez les cases du second niveau dans le filtre Type de fichier et le texte de la barre de recherche n’est pas synchronisé avec les propriétés sélectionnées/non sélectionnées (NPR-31287).

* Tous les membres (utilisateurs/groupes) ne peuvent pas être supprimés de la section Membres d’un dossier ; lors de la tentative de suppression de tous les utilisateurs, l’utilisateur connecté est ajouté à la liste (NPR-31171).

* Les fichiers dont le nom de fichier contient le symbole &quot;+&quot; ne peuvent pas être supprimés (NPR-31162).

* Le menu déroulant Créer, visible dans le menu supérieur lors de la sélection d&#39;un dossier, n&#39;affiche pas l&#39;option &quot;Dossier&quot; comme option de création (NPR-30877).

* La sélection de dossier Créer > FichierTélécharger élément d’action est manquante lorsque la liste de contrôle d’accès pour Deny jcr:removeChildNodes et jcr:removeNode sur le chemin d’accès est appliquée à un utilisateur (NPR-30840).

* Les flux de travaux de gestion des actifs numériques sont obsolètes lorsque certains fichiers mp4 sont téléchargés, ce qui entraîne l’obsolescence de tous les flux de travaux restants (NPR-30662).

* Une erreur de mémoire insuffisante est observée lorsqu’un fichier PDF volumineux (de plusieurs Go) est téléchargé vers la gestion des actifs numériques et que ses sous-ressources sont traitées (NPR-30614).

* Le mouvement en masse des ressources échoue et affiche un message d’avertissement (NPR-30610).

* Les noms des fichiers sont changés en minuscules lorsque vous déplacez des fichiers d’un dossier vers un autre dans AEM s’exécutant sur le mode d’exécution Contenu multimédia dynamique Scene7 (NPR-31630).

* Une erreur s’affiche lors de la modification d’un jeu d’images distant, pour l’image résidant dans le dossier portant le même nom que le nom de l’entreprise Scene7 (NPR-31340).

* Les fichiers de médias dynamiques contenant des références ne sont pas publiés (NPR-31180).

* Les téléchargements depuis le mode d’exécution AEM Dynamic Media - Scene7 vers Scene7 prennent trop de temps (NPR-31048).

* La zone réactive ajoutée à un fichier d’image n’est pas visible par le biais de la visionneuse d’images interactive dans la page des détails du fichier (NPR-30979).

* D’énormes tâches Sling sont créées et la bannière de traitement réapparaît lorsque les actions effectuées sur des ressources dans AEM Assets sont transmises à Scene7 (NPR-30947).

* Un conflit se produit lors de la création d’une copie de langue des fichiers et ceux-ci ne sont pas téléchargés vers Scene7 (NPR-30932).

* Les rendus dynamiques téléchargés à partir d’AEM s’exécutant en mode hybride Contenu multimédia dynamique sont rompus (ils sont de type texte avec un contenu &quot;impossible de trouver une image&quot; au lieu d’un type de contenu d’image) (NPR-30876).

* Le flux de travaux vidéo de codage de médias dynamiques ne parvient pas à générer la miniature de la vidéo migrée de Scene7 vers Contenu multimédia dynamique - Mode d’exécution Scene7 (CQ-4282011).

* IpsApiException a été observé lors de la migration de fichiers d’une instance vers une autre à l’aide d’identifiants d’entreprise Scene7 différents (CQ-4280548).

* La miniature des ressources 3D n’est pas informative lorsqu’un modèle 3D pris en charge est assimilé à AEM (CQ-4283701).

* Les boutons de défilement s’affichent dans la visionneuse, si un fichier 3D présente peu de vues de caméra (CQ-4283322).

* Hauteur de conteneur incorrecte d’un modèle 3D téléchargé prévisualisé dans DimensionalViewer sur la page Détails du fichier (CQ-4283309).

* Les vidéos ne peuvent pas être lues avec SmartCropVideoViewer sur Internet Explorer 11 et Safari (CQ-4281422).

* L’utilisation du bouton de déplacement pour déplacer plusieurs fichiers d’un dossier à un autre échoue dans AEM s’exécutant sur Contenu multimédia dynamique - mode d’exécution scene7 (CQ-4280384).

* Une vidéo déformée s’affiche sur les détails des ressources lorsque le type MIME est autre que MP4 (CQ-4279704).

* Les vidéos nouvellement assimilées dans des dossiers avec profil vidéo restent à l’état de traitement même après que le pourcentage de codage se termine à 100 % (CQ-4279389).

* Le déplacement de fichiers d’un dossier crée un grand nombre de tâches Sling (appels d’API Scene7) plus que nécessaire (CQ-4278664).

* Les noms des visionneuses d’images sont remplacés par des minuscules dans Scene7, lorsque des visionneuses d’images (ou des visionneuses de supports) sont créées et nommées selon la convention d’affectation de nom appropriée dans DAM (CQ-428112).

* Scene7 Migrator définit incorrectement l’état de publication (CQ-4263492).

* La recherche tactile dans l’interface utilisateur (effectuée par l’intermédiaire d’Omnisearch) fait défiler automatiquement la page de résultats vers le haut et perd la position de défilement de l’utilisateur dans les fragments de contenu (CQ-4282898).

* Les fichiers PDF ne sont pas indexés et le contenu au sein de ne peut pas faire l’objet de recherches (CQ-4278916).

* Une erreur &quot;Groupe non répertorié par le sélecteur d’utilisateurs : la valeur &quot;false&quot; est attendue pour la valeur &quot;true&quot; lors de l’ajout d’un groupe d’utilisateurs fermé avec des éléments différents `principalName` et `authorizableId` (CQ-4278177).

* L’affichage des colonnes de l’interface utilisateur des ressources affiche tous les chemins, quel que soit le chemin racine du barrage du client (CQ-4278175).

* La recherche du sélecteur de ressources ne fonctionne pas comme prévu (CQ-4275886).

* Les processus de rendu échouent (CQ-4271928).

* La purge d’événement DAM supprime les dernières données d’événement (maxSavedActivities) et conserve les données créées précédemment (NPR-31336).

* La recherche tactile dans l&#39;interface utilisateur (effectuée par l&#39;intermédiaire d&#39;Omnisearch) fait défiler automatiquement la page de résultats vers le haut et perd la position de défilement de l&#39;utilisateur (NPR-31307).

* La barre d’action et le nombre de ressources ne sont pas mis à jour lors de la sélection de tous les éléments, puis lors de la désélection de certains éléments (dossiers/fichiers individuels) dans l’interface utilisateur tactile (NPR-31118).

* Une exception s’affiche dans AEM lors de l’interrogation des détails d’une tâche d’une ressource (CQ-4283569).

* Vulnérabilité XSS dans DAM (NPR-31654).

#### Sites {#sites}

* Si l’héritage de LiveCopy est rompu, les pages de copie dynamique affichent des liens de copie de langue au lieu de liens LiveCopy (NPR-30980).
* Pour un nouveau plan directeur, si le nombre d&#39;enregistrements est supérieur à 40, seuls les 40 premiers enregistrements sont affichés. Le plan directeur affiche des lignes vierges pour le reste des enregistrements (NPR-31182).
* Lorsqu’un utilisateur ajoute des caractères japonais ou coréens dans la propriété description d’un menu, celui-ci affiche des caractères déformés pour le texte en japonais et en coréen. (NPR-31331).
* RTE (Rich Text Editor) ne permet pas d’insérer un tableau incorporé comme élément de liste (NPR-30879).
* Hors de la zone, l’éditeur de texte enrichi (RTE) s’adapte. applique la taille de police intégrée aux éléments de manière inattendue (NPR-31284).
* Lorsqu’un utilisateur se concentre sur les champs du rail gauche et utilise un raccourci clavier pour coller du contenu, il colle le le contenu du Presse-papiers de l’éditeur de page au lieu du contenu copié à partir des champs du rail gauche (NPR-31172).
* Lorsqu’un utilisateur ajoute un champ Téléchargement de fichier à un champ multichamp, le chemin d’accès à l’image est stocké dans le noeud de composant au lieu du noeud de champ multiple (NPR-30882).
* L’API ResponsiveGridExporter ne renvoie pas l’interface com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporter. Le package com.day.cq.wcm.foundation.model.impl est déclaré comme package privé (NPR-31398).
* Lorsqu’une page contenant des fragments d’expérience est ouverte en mode non éditeur (dans Auteur sans préfixe et `editor.html` `wcmmode=disabled`, ou dans Editeur)., la requête se termine par le code d’erreur d’état HTTP 500 (NPR-30743).
* Les utilisateurs ne peuvent pas modifier leur mot de passe ni accéder à leur page de profil (NPR-31161).
* Un fichier JavaScript contenant des données utilisateur est généré côté serveur (NPR-30822).
* L’interface utilisateur de création d’AEM permet le phishing à l’aide de contenu externe (NPR-29745).
* Vulnérabilité d’injection de langage d’expression dans l’éditeur de métadonnées AEM 6.5 (NPR-31017).

#### Interface utilisateur et de recherche {#search-ui-interface}

* Lorsque vous passez de la vue Carte à la vue Liste sur une page de résultats de recherche, il y a un décalage avant que la page puisse être défilée (NPR-31286).

* La case à cocher Tout sélectionner est masquée dans la vue Liste de l’interface utilisateur Sites (NPR-31614).

* Le nombre Sélectionner tout sur une page de résultats de recherche est incorrect (NPR-31120).

* L’éditeur de métadonnées affiche les balises qui n’existent pas (NPR-31119).

#### Traduction {#translation}

* Deux fenêtres contextuelles de calendrier s’affichent lorsque vous sélectionnez l’option Date d’échéance dans une tâche de traduction (NPR-31270).

#### Plate-forme {#platform}

* L&#39;option de type Mime dans la console Web ne fonctionne pas (NPR-31108).

* Le certificat client n’est pas accepté lors de la configuration de la connexion unique (NPR-31165).

* Les mises à jour de la configuration de la taille de la mémoire tampon pour le service HTTP basé sur Jetty ne sont pas enregistrées (NPR-30925).

* QueryBuilder prend désormais en charge orderby ``fn:name()`` dans les requêtes xpath (NPR-31322).

* Une arborescence d’activation en double est créée lors de la mise à niveau à partir d’AEM 6.3 (NPR-31513).

* Les requêtes transférées ne conservent pas les en-têtes de réponse définis lors de l’authentification sling (NPR-30013).

* La recherche dans les composants du sélecteur ne fonctionne pas (NPR-31692).

* Une erreur s’affiche lors de l’association d’un fichier ZIP à une publication des communautés AEM en raison de différentes versions du lot Apache POI et Apache Tika (NPR-31018).

* Le ``org.apache.sling.distribution.api`` lot est masqué dans le gestionnaire de configuration et n’est donc pas disponible pour les lots personnalisés (NPR-31720).

#### Projets {#projects}

* La permutation des vues du calendrier ne fonctionne pas (NPR-31271).

#### Brand Portal {#assets-brand-portal}

**Améliorations apportées au produit**

* Le processus d’importation d’origine des ressources dans les ressources AEM est modifié afin de récupérer uniquement les ressources nouvellement créées depuis le portail de marque vers AEM et d’ignorer les ressources qui existent déjà dans le dossier NEW pour éviter la réplication (CQ-4278527).

**Correctifs**

* Une icône incorrecte s’affiche lors de la création d’un dossier de contribution dans la fonction d’origine des ressources (CQ-4282825).
* Lors de la création d’un dossier de contribution, un ou les deux sous-dossiers (NOUVEAU et PARTAGÉ) n’apparaissent pas dans le dossier de contribution (CQ-4282424).
* Le système renvoie une exception si l’utilisateur tente de republier le dossier de contributions d’AEM vers le portail de marque après avoir reçu de nouveaux actifs dans le dossier de contributions de la fin du portail de marque (CQ-4279740).
* La création d’un dossier de contribution dans un dossier de contribution (dossier imbriqué) est interdite pour éviter toute complexité (CQ-4278391).
* Le système renvoie une exception lors du transfert de la liste des utilisateurs du portail de marque (fichier .csv) importée à partir de la console d’administration AEM. Seuls les champs Courriel, Prénom et Nom du fichier .csv sont obligatoires (CQ-4278390).

#### Communities {#communities}

**Correctifs**

* Les liens rapides permettant de gérer des groupes (Ouvrir/Modifier/Publier/Supprimer des groupes) ne sont pas visibles par les administrateurs de la communauté (administrateur du groupe/administrateur du site) (NPR-31627).
* Un blog envoyé ne s&#39;affiche pas, sauf si la page est manuellement actualisée/rechargée (NPR-31599).
* La requête JCR utilisée par la fonction &quot;Mentions&quot; est sensible à la casse et prend trop de temps pour renvoyer les résultats (NPR-31475).
* Le fichier UberJar AEM 6.5 renvoie une exception, `cq-social-translation` lot manquant du fichier UberJar AEM 6.5 (NPR-31186).
* Les bibliothèques Jackson Databind ont été mises à jour vers la version 2.9.9.3 pour corriger de nouvelles vulnérabilités (NPR-30967).
* Les titres des activités et des notifications sont contradictoires (NPR-30941).
* La pagination ne fonctionne pas correctement dans les blogs Communities (NPR-30914).
* Les rapports d&#39;analyse ne sont pas renseignés dans l’environnement de création AEM, une page vierge s’affiche (NPR-30913).

#### Oak {#oak}

* Les mises à jour de l’index Lucene provoquent un ralentissement du serveur d’auteur (NPR-31548).

#### Forms {#forms-6530}

>[!NOTE]
>
>Le Service Pack AEM n’inclut pas de correctifs pour AEM Forms. Les correctifs sont fournis à l’aide d’un module complémentaire Forms distinct.  En outre, un programme d’installation cumulatif est publié, qui comprend des correctifs pour AEM Forms sur JEE. For more information, see [Install AEM Forms add-on](#install-aem-forms-add-on-package) and [Install AEM Forms on JEE](#install-aem-forms-jee-installer).

##### Package de modules complémentaires Forms {#forms-add-on-package-6530}

**Formulaires adaptatifs**

* Les chaînes contiennent la clé du dictionnaire lors de la localisation des formulaires adaptatifs (NPR-31110).

**Communication interactive**

* **MissingNode.toString()** renvoie des résultats inexacts après la mise à niveau des bibliothèques Jackson vers la version 2.10.0 (NPR-31549).

* L’éditeur de texte supprime de manière aléatoire les caractères d’espace du texte copié à partir de Microsoft Word (NPR-31113).

**Correspondence Management**

* Les légendes et les info-bulles ne s’affichent pas lors de la migration des lettres de LiveCycle ES4SP1 vers AEM 6.5 (NPR-31615).

* **Le formatage de flux de texte n’est plus pris en charge** lorsque le message d’erreur s’affiche lors de l’enregistrement de lettres en tant que brouillons (NPR-30463).

**Processus**

* Le processus OSGi échoue en raison d’une utilisation à 100 % du processeur (NPR-31233).

**Formulaires HTML5**

* La génération de l’aperçu HTML5 d’un formulaire XDP affiche un scintillement lors de l’ajout d’instances d’un sous-formulaire (NPR-30909).

##### Programme d’installation de Forms sur JEE {#forms-jee-installer-6530}

**Forms - Document Services**

* Le service Web SOAP utilisant MTOM dans un projet .NET affiche des exceptions pour les méthodes AssemblerServiceClient invoke et HtmlToPDF2 (NPR-4281771).

**Foundation JEE**

* La configuration d’action ne charge pas les noms de processus pour l’action d’envoi Appel d’un flux de travail des formulaires (NPR-31478).
* Les utilisateurs d’AEM Forms sur JEE rencontrent des erreurs similaires à celles suivantes lors de l’importation de fichiers .lca ou de la configuration de LDAP dans la console d’administration :

   `com.ibm.ws.webcontainer.filter.FilterInstanceWrapper doFilter SRVE8109W: Uncaught exception thrown by filter um: java.lang.NoClassDefFoundError: org/apache/commons/io/IOUtils at org.apache.commons.fileupload.util.Streams.copy`

   `Error 500: javax.servlet.ServletException: java.lang.NoClassDefFoundError: org.apache.commons.io.IOUtils` (NPR-30931)


### Packs de fonctionnalités inclus {#feature-packs-included-6530}

>[!NOTE]
>
>Pour les clients AEM Forms, il est impératif d’installer le module complémentaire AEM Forms après l’installation de tout pack de service, pack de correctif cumulatif ou pack de fonctionnalités d’AEM.

#### Forms - Foundation JEE {#forms-foundation-jee-feature}

* Prise en charge d’AEM Forms pour Oracle 18c (NPR-29155).

## Install 6.5.3.0 {#install}

**Conditions requises**

* AEM 6.5.3.0 requires AEM 6.5. Check [upgrade documentation](/help/sites-deploying/upgrade.md) for detailed instructions.
* Le Service Pack peut être téléchargé sur Adobe Package Share, accessible directement depuis l’instance AEM 6.5.
* Lors d’un déploiement avec MongoDB et plusieurs instances, installez AEM 6.5.3.0 sur l’une des instances d’auteur à l’aide du gestionnaire de modules.
* Avant d’installer le pack de service, veillez à disposer d’un instantané ou d’une nouvelle sauvegarde de votre instance AEM.
* Redémarrez l’instance avant l’installation. Cela est nécessaire uniquement lorsque l’instance reste en mode de mise à jour (ce qui est le cas lorsque l’instance vient d’être mise à jour depuis une version antérieure). Toutefois, cela est recommandé si l’instance s’est exécutée pendant une longue durée.

>[!CAUTION]
>
>Adobe recommande de ne pas supprimer ni désinstaller le package AEM 6.5.3.0.

### Installation du Service Pack au moyen de Package Share {#install-service-pack-via-package-share}

Accomplissez les étapes suivantes pour installer le Service Pack sur une instance 6.5 existante :

1. Login to Package Share from within AEM or directly from your browser and download the [AEM 6.5.3.0 package](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/servicepack/AEM-6.5.3.0).

1. Installez le package téléchargé à l’aide du gestionnaire de modules.

>[!NOTE]
>
>**La boîte de dialogue sur l’interface utilisateur de Package Manager se ferme parfois de manière impromptue lors de l’installation de la version 6.5.3.0**
>
>Il est donc recommandé d’attendre que les journaux d’erreurs se stabilisent avant d’accéder à l’instance. L’utilisateur doit attendre les journaux spécifiques liés à la désinstallation du lot de mise à jour avant de s’assurer que les installations sont réussies. Cela se produit généralement sur Safari, mais peut se produire par intermittence sur n’importe quel navigateur.

**Installation automatique**

Il existe deux manières d’installer automatiquement AEM 6.5.3.0 dans une instance en cours d’exécution :

A. Placez le package dans le dossier ..*/crx-quickstart/install* alors que le serveur est disponible en ligne. Le package est automatiquement installé.

B. Use the [HTTP API from Package Manager](https://docs.adobe.com/content/docs/en/crx/2-3/how_to/package_manager.html) - make sure that you use cmd=install&amp;recursive=true - so the nested packages  are  installed.

>[!NOTE]
>
>AEM 6.5.3.0 ne prend pas en charge l’installation de Bootstrap.

**Validation de l’installation**

1. La page Informations sur le produit (/system/console/ productinfo) affiche la chaîne de version mise à jour `Adobe Experience Manager, Version 6.5.3.0` sous Produits installés.

1. All  OSGi  bundles are either **[!UICONTROL ACTIVE]** or **[!UICONTROL FRAGMENT]** in the OSGi Console (Use Web Console: /system/console/bundles).
1. Le lot OSGI org.apache.jackrabbit.oak-core est sur la version 1.10.6 ou ultérieure (utilisez la console Web : /system/console/bundles).

In order to see what platforms are certified to run with this release, please refer to the [Technical Requirements](/help/sites-deploying/technical-requirements.md).

### Installation du module complémentaire AEM Forms {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Passez cette étape si vous n’utilisez pas AEM Forms. Les correctifs dans AEM Forms sont fournis dans un module complémentaire distinct.

>[!NOTE]
>
>AEM 6.5.3.0 includes a new version of [AEM Forms Compatibility package](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/compatpack/AEM-FORMS-6.5.3.0-COMPAT). Si vous utilisez une ancienne version du package de compatibilité d’AEM Forms et que vous mettez à jour vers AEM 6.5.3.0, installez la dernière version du package de compatibilité d’AEM Forms après l’installation du package de module complémentaire de Forms.

1. Vérifiez que vous avez installé le Service Pack AEM.
1. Download the corresponding Forms add-on package listed at [AEM Forms releases](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) for your operating system.
1. Install the Forms add-on package as described in [Installing AEM Forms add-on packages](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

### Install AEM Forms on JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Passez cette étape si vous n’utilisez pas AEM Forms sous JEE. Les correctifs d’AEM Forms sur JEE sont fournis par le biais d’un programme d’installation distinct.

For information about installing the cumulative installer for AEM Forms on JEE and post-deployment configuration, see the [release notes for patch 0007](https://helpx.adobe.com/aem-forms/quick-fixes/6-5/jee-patch-0007.html).

#### Programme d’installation de Workbench

Comme il s’agit d’un programme d’installation complet, la taille du fichier est plus grande que celle du correctif. Désinstallez la version précédente de Workbench avant d’installer la nouvelle version.

## UberJar {#uber-jar}

The UberJar for AEM 6.5.3.0 is available in the [Adobe Public Maven repository](https://repo.adobe.com/nexus/content/groups/public/com/adobe/aem/uber-jar/6.5.3/).

To use UberJar in a Maven project, refer to the article, [How to use UberJar](/help/sites-developing/ht-projects-maven.md) and include the following dependency in your project POM:

```shell
<dependency>
      <groupId>com.adobe.aem</groupId>
      <artifactId>uber-jar</artifactId>
      <version>6.5.3.0</version>
      <classifier>apis</classifier>
      <scope>provided</scope>
</dependency>
```

## Fonctionnalités obsolètes {#removed-deprecated-features}

Cette section répertorie les fonctionnalités qui ont été marquées comme obsolètes avec AEM 6.5.3.0. Les fonctionnalités qui doivent être supprimées dans une version ultérieure sont d’abord désapprouvées, avec une autre option à utiliser.

Il est conseillé aux clients de vérifier s’ils utilisent la fonctionnalité ou la fonctionnalité dans leur déploiement actuel et de prévoir de modifier leur implémentation pour utiliser l’autre option.

| Zone | Fonctionnalité | Remplacement |
|---|---|---|
| Intégrations | The **[!UICONTROL AEM Cloud Services Opt-In]** screen has been deprecated. L’intégration d’AEM et de Target ayant été mise à jour dans AEM 6.5 pour prendre en charge l’API Target Standard, qui utilise l’authentification via Adobe IMS et les E/S, et le rôle croissant d’Adobe Launch pour l’instrumentation des pages AEM pour l’analyse et la personnalisation, l’assistant d’inclusion est devenu non pertinent du point de vue fonctionnel. | Configuration des connexions système, de l’authentification IMS Adobe et des intégrations d’E/S Adobe via les services cloud AEM respectifs |

## Problèmes connus {#known-issues}

* Si l’assistant de configuration **des ressources** connectées renvoie un message d’erreur 404 après avoir installé AEM 6.5.3.0, réinstallez manuellement les packages **cq-remotedam-client-ui-content** et **cq-remotedam-client-ui-components** à l’aide de Package Manager.
* Les erreurs et messages d’avertissement suivants peuvent s’afficher lors de l’installation d’AEM 6.5.x.x :
   * « Lorsque l’intégration de Target est configurée dans AEM à l’aide de l’API Target Standard (authentification IMS), l’exportation de fragments d’expérience vers Target entraîne la création de types d’offres incorrects. Au lieu du type « Fragment d’expérience » / source « Adobe Experience Manager », Target crée plusieurs offres avec le type « HTML » / source « Adobe Target Classic ».
   * com.adobe.granite.maintenance.impl.TaskScheduler : Aucune fenêtre de maintenance n&#39;a été trouvée sur le granite/operations/maintenance
   * La validation côté serveur du formulaire adaptatif échoue lorsque des fonctions d’agrégation telles que SUM, MAX et MIN sont utilisées. CQ-4274424
   * com.adobe.granite.maintenance.impl.TaskScheduler - Aucune fenêtre de maintenance n’a été trouvée sur granite/operations/maintenance.
   * La zone réactive d’une image interactive de média dynamique n’est pas visible lors de la prévisualisation du fichier via la visionneuse de bannières modifiables.

## Lots OSGi et packages de contenu inclus {#osgi-bundles-and-content-packages-included}

Les documents texte suivants répertorient les lots OSGi et les packages de contenu inclus dans AEM 6.5.3.0.

Liste des lots OSGi inclus dans AEM 6.5.3.0

[Obtenir le fichier](assets/6530_bundles.txt)

Liste des packages de contenu inclus dans AEM 6.5.3.0

[Obtenir le fichier](assets/sp_6530_packages.txt)

## Ressources utiles {#helpful-resources}

* [Notes de mise à jour d’AEM 6.5](/help/release-notes/release-notes.md)
* [Page de produits AEM ](https://www.adobe.com/marketing/experience-manager.html)
* [Documentation d’AEM 6.5](https://helpx.adobe.com/support/experience-manager/6-5.html)
* Subscribe to [Adobe priority product updates](https://www.adobe.com/subscription/priority-product-update.html)

## Sites restreints {#restricted-sites}

Ces sites sont réservés aux clients. Si vous êtes client et avez besoin d’un accès, contactez votre responsable de compte Adobe.

* [Téléchargement du produit à l’adresse licensing.adobe.com](https://licensing.adobe.com/)
* [Contactez l&#39;assistance](https://daycare.day.com/public/contact.html)clientèle Pour plus d&#39;informations sur l&#39;accès au portail d&#39;assistance, consultez [Accès au portail](https://helpx.adobe.com/experience-manager/kb/accessing-aem-support-portal.html)d&#39;assistance.
