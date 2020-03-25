---
title: Notes de mise à jour d’AEM 6.5 Previous Service Pack
description: Notes de mise à jour spécifiques à Adobe Experience Manager 6.5 Service Pack 3 et aux versions antérieures.
uuid: c7bc3705-3d92-4e22-ad84-dc6002f6fa6c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: 25542769-84d1-459c-b33f-eabd8a535462
docset: aem65
translation-type: tm+mt
source-git-commit: 7345d629aa628c2e2e094a8194d9306d7c3d2d60

---


# Correctifs et packs de fonctionnalités inclus dans les packs de service précédents {#hotfixes-and-feature-packs-included-in-previous-service-packs}

## AEM 6.5.3.0

Adobe Experience Manager 6.5.3.0 is an important release that includes performance, stability, security, and key customer fixes and enhancements released since the general availability of 6.5 release in **April 2019**. Il peut être installé sur Adobe Experience Manager (AEM) 6.5.

Les principaux points forts de cette version du Service Pack incluent les éléments suivants :

* Le référentiel intégré (Apache Jackrabbit Oak) a été mis à niveau vers la version 1.10.6.

* Adobe Experience Manager Assets prend désormais en charge les archives ZIP créées à l’aide de l’algorithme Deflate64.

* Une nouvelle colonne pour la date de création, qui peut être triée, a été ajoutée dans le de gestion des actifs numériques  les résultats de la recherche de ressources dans lede la gestion des actifs.

* Le tri des ressources en fonction de la colonne Nom a été activé dans  .

* Les médias dynamiques prennent désormais en charge les fichiers vidéo de recadrage dynamique. Smart Crop est une fonction pilotée par l’apprentissage automatique qui recadre une vidéo tout en déplaçant le cadre pour suivre le point focal de la scène.

* Dynamic Media prend en charge l’imagerie dynamique.

* Possibilité de [définir les préférences d’absence du bureau](../forms/using/configure-out-of-office-settings.md) dans le AEM.

* Possibilité de [partager des éléments](../forms/using/configure-shared-queues-osgi.md) de boîte de réception ou de boîte de réception avec d’autres utilisateurs dans le  AEM.

* Possibilité de [générer des communications interactives en mode](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)Batch.

* Mise à jour de la version de jQuery intégrée dans ContextHub vers la version 3.4.1.

### Assets {#assets-6530-enhancements}

**Améliorations apportées au produit**

* Experience Manager Assets prend désormais en charge les archives ZIP créées à l’aide de l’algorithme Deflate 64 (NPR-27573).

* Une nouvelle colonne pour la date de création, qui peut être triée, a été ajoutée dans le DAM  les résultats de la recherche d’actifs dans lede l’ d’ (NPR-31312).

* Le tri des ressources en fonction de la colonne Nom a été autorisé dans   (NPR-31299).

* Les fichiers GLB, GLTF, OBJ et STL prennent en charge les  de ressources dans la page Détails des ressources dans DAM (CQ-4282277).

* Le ReplicationOnModifyListener est déclenché pour les noeuds de blocs lors du transfert de blocs dans le module Contenu multimédia dynamique (CQ-4281279).

* Les médias dynamiques prennent désormais en charge les fichiers vidéo de recadrage dynamique. Smart Crop est une fonction pilotée par l’apprentissage automatique qui recadre une vidéo tout en déplaçant le cadre pour suivre le point focal de la scène (CQ-4278995).

* Dynamic Media prend en charge l’imagerie intelligente (CQ-4222249).

* Le  de recherche/navigation a été défini comme par défaut  dans le sélecteur Foundation si les paramètres de l’ de la page de recherche/navigation sont transmis dans la requête (NPR-31601).

**Correctifs**

* Les métadonnées de certains PDF ne sont pas mises à jour et enregistrées dans le PDF lors de la modification de son titre (NPR-31629).

* Le partage des ressources ne fonctionne pas pour les ressources dont le nom contient le caractère &quot;+&quot; (NPR-31547).

* Les modifications dans le formulaire de recherche par défaut Administration des ressources * Rail de recherche ne fonctionnent pas comme prévu (NPR-31502).

* Les suggestions ne s&#39;affichent pas lors de l&#39;utilisation d&#39;Omnisearch sur le de ressources pour la recherche de ressources (NPR-31496).

* Les références de ressources dans les collections ne sont pas mises à jour lorsque les ressources référencées sont déplacées vers un autre emplacement, dans les cas où les mêmes ressources sont référencées par une collection différente par différents utilisateurs (NPR-31486).

*  balises IPTC sont ajoutées aux métadonnées de fichier (NPR-31328).

* Le nombre de résultats de la recherche dans le coin supérieur droit ne se met pas à jour correctement lorsque la recherche est déclenchée à partir du rail de filtre (NPR-31316).

* Toutes les cases à cocher sont désactivées lorsque vous décochez les cases du second niveau dans le filtre Type de fichier, et le texte de la barre de recherche n’est pas synchronisé avec les propriétés sélectionnées/non sélectionnées (NPR-31287).

* Tous les membres (utilisateurs/groupes) ne peuvent pas être supprimés de la section Membres d’un dossier ; lors de la tentative de suppression de tous les utilisateurs, l’utilisateur connecté est ajouté au (NPR-31171).

* Les fichiers dont le nom de fichier contient le symbole &quot;+&quot; ne peuvent pas être supprimés (NPR-31162).

* Le menu déroulant Créer, visible dans le menu supérieur lors de la sélection d&#39;un dossier, n&#39;affiche pas l&#39;option &quot;Dossier&quot; comme option de création (NPR-30877).

* La sélection de dossier Créer > FichierTélécharger élément d’action est manquante lorsque la liste de contrôle d’accès pour Deny jcr:removeChildNodes et jcr:removeNode sur le chemin d’accès est appliquée à un utilisateur (NPR-30840).

* Le DAM  dans l’état obsolète lorsque certains fichiers mp4 sont téléchargés, ce qui entraîne l’obsolescence de tous les restants (NPR-30662).

* Une erreur de mémoire insuffisante est observée lorsqu’un fichier PDF volumineux (de plusieurs Go) est téléchargé vers la gestion des actifs numériques et que ses sous-ressources sont traitées (NPR-30614).

* Le mouvement en masse des ressources échoue et affiche un message d’avertissement (NPR-30610).

* Les noms des fichiers sont changés en minuscules lorsque vous déplacez des fichiers d’un dossier vers un autre dans AEM s’exécutant sur le mode d’exécution Contenu multimédia dynamique Scene7 (NPR-31630).

* Une erreur s’affiche lors de la modification d’un jeu d’images distant, pour l’image résidant dans le dossier portant le même nom que le nom de l’ de Scene7 (NPR-31340).

* Les fichiers de médias dynamiques contenant des références ne sont pas publiés (NPR-31180).

* Les téléchargements depuis le mode d’exécution AEM Dynamic Media - Scene7 vers Scene7 prennent trop de temps (NPR-31048).

* La zone réactive ajoutée à un fichier d’image n’est pas visible par le biais de la visionneuse d’images interactive dans la page des détails du fichier (NPR-30979).

* D’énormes tâches Sling sont créées et la bannière de traitement réapparaît lorsque les actions effectuées sur des ressources dans AEM Assets sont transmises à Scene7 (NPR-30947).

* Un conflit se produit lors de la création d’une copie de langue des fichiers et ceux-ci ne sont pas téléchargés vers Scene7 (NPR-30932).

* Les rendus dynamiques téléchargés à partir d’AEM s’exécutant en mode hybride Contenu multimédia dynamique sont rompus (ils sont de type texte avec un contenu &quot;impossible de trouver une image&quot; au lieu d’un type de contenu d’image) (NPR-30876).

* Le flux de travaux vidéo de codage de médias dynamiques ne parvient pas à générer la miniature de la vidéo migrée de Scene7 vers Contenu multimédia dynamique - Mode d’exécution Scene7 (CQ-4282011).

* IpsApiException a été observé lors de la migration de fichiers d’une instance vers une autre à l’aide de différents ID de Scene7 (CQ-4280548).

* La miniature des ressources 3D n’est pas informative lorsqu’un modèle 3D pris en charge est assimilé à AEM (CQ-4283701).

* Les boutons de défilement s’affichent dans la visionneuse, si un fichier 3D comporte peu de  d’appareil photo (CQ-4283322).

* Hauteur de  de incorrecte d’un modèle 3D téléchargé prévisualisé dans DimensionalViewer sur la page Détails du fichier (CQ-4283309).

* Les vidéos ne peuvent pas être lues avec SmartCropVideoViewer dans Internet Explorer 11 et Safari (CQ-4281422).

* L’utilisation du bouton de déplacement pour déplacer plusieurs fichiers d’un dossier à un autre échoue dans AEM s’exécutant sur Contenu multimédia dynamique - mode d’exécution scene7 (CQ-4280384).

* Une vidéo déformée s’affiche sur les détails de la ressource lorsque le type MIME est autre que MP4 (CQ-4279704).

* Les vidéos nouvellement assimilées dans des dossiers avec des  vidéo restent à l’état de traitement même après que le pourcentage de codage se termine à 100 % (CQ-4279389).

* Le déplacement de fichiers d’un dossier crée un grand nombre de tâches Sling (appels d’API Scene7) plus que nécessaire (CQ-4278664).

* Les noms des visionneuses d’images sont remplacés par des minuscules dans Scene7, lorsque des visionneuses d’images (ou des visionneuses de supports) sont créées et nommées selon la convention d’affectation de nom appropriée dans DAM (CQ-428112).

* Scene7 Migrator définit incorrectement l’état de publication (CQ-4263492).

* La recherche tactile dans l’interface utilisateur (effectuée par l’intermédiaire d’Omnisearch) fait défiler automatiquement la page de résultats vers le haut et perd la position de défilement de l’utilisateur dans les fragments de contenu (CQ-4282898).

* Les fichiers PDF ne sont pas indexés et le contenu au sein de ne peut pas faire l’objet de recherches (CQ-4278916).

* Une erreur &quot;Groupe non répertorié par le sélecteur d’utilisateurs : la valeur &quot;false&quot; est attendue pour la valeur &quot;true&quot; lors de l’ajout d’un groupe d’utilisateurs fermé avec des éléments différents `principalName` et `authorizableId` (CQ-4278177).

* Le de colonnes de l’interface utilisateur des ressources affiche tous les chemins, quel que soit le chemin racine du barrage d’un client spécifique (CQ-4278175).

* La recherche du sélecteur de ressources ne fonctionne pas comme prévu (CQ-4275886).

* Les  de rendu échouent (CQ-4271928).

* DAM  purge supprime les données de les plus récentes (maxSavedActivities) et conserve les données créées précédemment (NPR-31336).

* La recherche tactile dans l&#39;interface utilisateur (effectuée par l&#39;intermédiaire d&#39;Omnisearch) fait défiler automatiquement la page de résultats vers le haut et perd la position de défilement de l&#39;utilisateur (NPR-31307).

* La barre d’action et le nombre de ressources ne sont pas mis à jour lors de la sélection de tous les éléments, puis lors de la désélection de certains éléments (dossiers/fichiers individuels) dans l’interface utilisateur tactile (NPR-31118).

* Une exception s’affiche dans AEM lors de l’interrogation des détails d’une tâche d’une ressource (CQ-4283569).

### Sites {#sites}

* Si l’héritage de LiveCopy est rompu, les pages de copie dynamique affichent des liens de copie de langue au lieu de liens LiveCopy (NPR-30980).
* Pour un nouveau plan directeur, si le nombre d&#39;enregistrements est supérieur à 40, seuls les 40 premiers enregistrements sont affichés. Le plan directeur affiche des lignes vierges pour le reste des enregistrements (NPR-31182).
* Lorsqu’un utilisateur ajoute des caractères japonais ou coréens dans la propriété description d’un menu, celui-ci affiche des caractères déformés pour le texte en japonais et en coréen. (NPR-31331).
* L’éditeur de texte enrichi (RTE) ne permet pas d’insérer un tableau incorporé comme élément de  (NPR-30879).
* Hors de la zone, l’éditeur de texte enrichi (RTE) s’adapte. applique la taille de police intégrée aux éléments de manière inattendue (NPR-31284).
* Lorsqu’un utilisateur se concentre sur les champs du rail gauche et utilise un raccourci clavier pour coller du contenu, il colle le le contenu du Presse-papiers de l’éditeur de page au lieu du contenu copié à partir des champs du rail gauche (NPR-31172).
* Lorsqu’un utilisateur ajoute un champ Téléchargement de fichier à un champ multichamp, le chemin d’accès à l’image est stocké dans le noeud de composant au lieu du noeud de champ multiple (NPR-30882).
* L’API ResponsiveGridExporter ne renvoie pas l’interface com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporter. Le package com.day.cq.wcm.foundation.model.impl est déclaré comme package privé (NPR-31398).
* Lorsqu’une page contenant des fragments d’expérience est ouverte en mode non éditeur (dans Auteur sans préfixe et `editor.html` `wcmmode=disabled`, ou dans Editeur)., la requête se termine par le code d’erreur d’état HTTP 500 (NPR-30743).
* Les utilisateurs ne peuvent pas modifier leur mot de passe ni accéder à leur page de  de (NPR-31161).

### Interface utilisateur et de recherche {#search-ui-interface}

* Lorsque vous passez du de cartes au de la page de résultats de recherche, il y a un décalage avant que la page ne puisse être parcourue (NPR-31286).

* La case à cocher Tout sélectionner est masquée dans le de  sur l’interface utilisateur des sites (NPR-31614).

* Le nombre Sélectionner tout sur une page de résultats de recherche est incorrect (NPR-31120).

* L’éditeur de métadonnées affiche les balises qui n’existent pas (NPR-31119).

### Traduction {#translation}

* Deux fenêtres contextuelles de calendrier s’affichent lors de la sélection de l’option Date d’échéance dans une tâche de traduction (NPR-31270).

### Plate-forme {#platform}

* L&#39;option de type Mime dans la console Web ne fonctionne pas (NPR-31108).

* Le certificat client n’est pas accepté lors de la configuration de la connexion unique (NPR-31165).

* Les mises à jour de la configuration de la taille de la mémoire tampon pour le service HTTP basé sur Jetty ne sont pas enregistrées (NPR-30925).

* QueryBuilder prend désormais en charge orderby ``fn:name()`` dans le xpath (NPR-31322).

*    arbre est créé lors de la mise à niveau à partir d’AEM 6.3 (NPR-31513).

* Les requêtes transférées ne conservent pas les en-têtes de réponse définis lors de l’authentification sling (NPR-30013).

* La recherche dans les composants du sélecteur ne fonctionne pas (NPR-31692).

* Une erreur s’affiche lors de l’association d’un fichier ZIP à une publication des communautés AEM en raison de différentes versions d’Apache POI et du lot Apache Tika (NPR-31018).

* Le ``org.apache.sling.distribution.api`` lot est masqué dans le gestionnaire de configuration et n’est donc pas disponible pour les lots personnalisés (NPR-31720).

### Projets {#projects}

* Le changement de  de calendrier ne fonctionne pas (NPR-31271).

### Brand Portal {#assets-brand-portal}

**Améliorations apportées au produit**

* Le processus d’importation d’origine des ressources dans les ressources AEM est modifié afin de récupérer uniquement les ressources nouvellement créées depuis le portail de marque vers AEM et d’ignorer les ressources qui existent déjà dans le dossier NEW pour éviter la réplication (CQ-4278527).

**Correctifs**

* Une icône incorrecte s’affiche lors de la création d’un dossier de contribution dans la fonction d’origine des ressources (CQ-4282825).
* Lors de la création d’un dossier de contribution, un ou les deux sous-dossiers (NOUVEAU et PARTAGÉ) n’apparaissent pas dans le dossier de contribution (CQ-4282424).
* Le système renvoie une exception si l’utilisateur tente de republier le dossier de contributions d’AEM vers le portail de marque après avoir reçu de nouveaux actifs dans le dossier de contributions à partir de la fin du portail de marque (CQ-4279740).
* La création d’un dossier de contribution dans un dossier de contribution (dossier imbriqué) est interdite pour éviter toute complexité (CQ-4278391).
* Le système renvoie une exception lors du transfert du utilisateur du portail de marque (fichier .csv) importé à partir de la console d’administration AEM. Seuls les champs Courriel, Prénom et Nom du fichier .csv sont obligatoires (CQ-4278390).

### Communities {#communities}

**Correctifs**

* Les liens rapides permettant de gérer des groupes (Ouvrir/Modifier/Publier/Supprimer des groupes) ne sont pas visibles par les administrateurs de la communauté (administrateur du groupe/administrateur du site) (NPR-31627).
* Un blog envoyé ne s&#39;affiche pas, sauf si la page est manuellement actualisée/rechargée (NPR-31599).
* Le  JCR utilisé par la fonction &quot;Mentions&quot; est sensible à la casse et prend trop de temps pour renvoyer les résultats (NPR-31475).
* Le fichier UberJar AEM 6.5 renvoie une exception, `cq-social-translation` lot manquant du fichier UberJar AEM 6.5 (NPR-31186).
* Les bibliothèques Jackson Databind ont été mises à jour vers la version 2.9.9.3 pour corriger de nouvelles vulnérabilités (NPR-30967).
* Les titres des activités et des notifications sont contradictoires (NPR-30941).
* La pagination ne fonctionne pas correctement dans les blogs Communities (NPR-30914).
* Les rapports d&#39;analyse ne sont pas renseignés dans l’environnement de création AEM, une page vierge s’affiche (NPR-30913).

### Oak {#oak}

* Les mises à jour de l’index Lucene provoquent un ralentissement du serveur d’auteur (NPR-31548).

### Forms {#forms-6530}

>[!NOTE]
>
>Le Service Pack AEM n’inclut pas de correctifs pour AEM Forms. Les correctifs sont fournis à l’aide d’un module complémentaire Forms distinct.  En outre, un programme d’installation cumulatif est publié, qui comprend des correctifs pour AEM Forms sur JEE. For more information, see [Install AEM Forms add-on](#install-aem-forms-add-on-package) and [Install AEM Forms on JEE](#install-aem-forms-jee-installer).

#### Package de modules complémentaires Forms {#forms-add-on-package-6530}

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

#### Programme d’installation de Forms sur JEE {#forms-jee-installer-6530}

**Forms - Document Services**

* Le service Web SOAP utilisant MTOM dans un projet .NET affiche des exceptions pour les méthodes AssemblerServiceClient invoke et HtmlToPDF2 (NPR-4281771).

**Foundation JEE**

* La configuration d’action ne charge pas les noms de processus pour l’action d’envoi Appel d’un flux de travail des formulaires (NPR-31478).

### Packs de fonctionnalités inclus {#feature-packs-included-6530}

>[!NOTE]
>
>Pour les clients AEM Forms, il est impératif d’installer le module complémentaire AEM Forms après l’installation de tout pack de service, pack de correctif cumulatif ou pack de fonctionnalités d’AEM.

#### Forms - Foundation JEE {#forms-foundation-jee-feature}

* Prise en charge d’AEM Forms pour Oracle 18c (NPR-29155).

## AEM 6.5.2.0

AEM 6.5.2.0 is an important release that includes performance, stability, security, and key customer fixes and enhancements released since the general availability of AEM 6.5 in **April 2019**. Elle peut être installée sur AEM 6.5.

Les principaux points forts de cette version du Service Pack incluent les éléments suivants :

* Le référentiel intégré (Apache Jackrabbit Oak) a été mis à niveau vers la version 1.10.3.
* Une propriété de configuration permettant d’exporter directement des fragments d’expérience vers des espaces de travail définis par l’utilisateur pour Adobe Target a été ajoutée.
* Les utilisateurs de ressources peuvent rechercher des images visuellement similaires. AEM affiche les images balisées intelligentes du référentiel DAM qui sont similaires à une image sélectionnée par l’utilisateur. Voir [Recherche visuelle](../assets/search-assets.md#visualsearch).

* La fonctionnalité Ressources connectées a été améliorée afin d’ajouter la prise en charge de la récupération de documents à partir de déploiements DAM distants. Les auteurs de site peuvent désormais rechercher et filtrer les types de documents pris en charge dans l’outil Recherche de contenu. Les documents distants peuvent être ajoutés au composant Télécharger sur les pages web. Voir [Utilisation des ressources connectées](../assets/use-assets-across-connected-assets-instances.md).

* Amélioration de type de document avec plus de types MIME pour prendre en charge les options à plusieurs valeurs.
* Un processus de retraitement externe pour la prise en charge de ressources multiples a été mis en place.
* Les performances de média dynamique ont été améliorées à l’aide des filtres de ressources par défaut pour la réplication.
* Les options de recadrage/rotation des fichiers ont été restaurées pour DMS7.
* Une option permettant de désactiver une vidéo au chargement dans VideoPlayer a été mise en œuvre.
* Une correction a été apportée pour assurer que la vue en colonne de l’interface utilisateur Asset affiche uniquement le contenu spécifique au client.
* Une correction a été apportée pour permettre aux modifications d’accordéon de style de se refléter dans les résultats de la recherche.

### Assets {#assets}

**Améliorations apportées au produit**

* La fonctionnalité Ressources connectées a été améliorée afin d’ajouter la prise en charge de la récupération de documents à partir de déploiements DAM distants. Les auteurs de site peuvent désormais rechercher et filtrer les types de documents pris en charge dans l’outil Recherche de contenu. Les documents distants peuvent être ajoutés au composant Télécharger sur les pages web. Correctif pour CQ-4270245. Voir [Utilisation des ressources connectées](/help/assets/use-assets-across-connected-assets-instances.md).

* Les utilisateurs de ressources peuvent rechercher des images visuellement similaires. AEM affiche les images balisées intelligentes du référentiel DAM qui sont similaires à une image sélectionnée par l’utilisateur. Voir [Recherche visuelle](../assets/search-assets.md#visualsearch).

**Correctifs**

* Les chemins d’accès aux ressources dans les URL et les métadonnées des dossiers générés par l’API ACP ne sont pas codés dans les URL. GRANITE-26198 : correctif pour CQ-4271814
* Il est impossible d’ouvrir une archive dont le nom contient un symbole de pourcentage (%) à l’aide de l’interface Ressources. NPR-29989 : correctif pour CQ-4270467
* Interface utilisateur tactile : Lors de l’assistant de gestion de publication, les références sont ajoutées après la page dans le corps de la demande de publication, ce qui entraîne la publication de tous les actifs après la page. Une fois la page rendue, certaines des ressources de l’instance de publication sont manquantes. NPR-29985 : correctif pour CQ-4270724
* La fonction Dissocier ne fonctionne pas pour les éléments associés dont le nom comporte des caractères spéciaux (caractères codés au format URI). NPR-30387 : correctif pour CQ-4274446
* Lors de la modification d’un fragment de contenu, la version est créée avec le mauvais utilisateur.
* Échec lors de la création de collections sur un système basé sur le client. NPR-30114 : correctif pour CQ-4272948
* L’affichage en colonne de l’interface utilisateur Asset ne respecte pas le chemin racine DAM du client actuel, mais l’accès à tous les chemins DAM du client. NPR-30636 : correctif pour CQ-4275481
* Attaque de XSS possible via une fenêtre d&#39;alerte de fichier restreinte, car l&#39;image injectée est visible. NPR-30617 : correctif pour CQ-4270133
* MultiTenant : Les clients qui enregistrent les propriétés du dossier observent à la fois l’invite de succès et le message d’erreur décrivant l’action a échoué : &quot;Impossible de modifier les propriétés. Autorisations insuffisantes. » et par conséquent, ils les confondent. NPR-30545 : correctif pour CQ-4275333
* La boîte de dialogue du sélecteur de ressources n’autorise pas la sélection de ressources, ce qui empêche la mise à jour de la source à l’aide de la fonctionnalité de remplacement de la source correspondante. NPR-30502 : correctif pour CQ-4275029
* Workflow Asset de mise à jour de la gestion des actifs numériques : état obsolète lors du téléchargement de fichiers mp4 de grande taille. NPR-30480 : correctif pour CQ-4271352
* La fonctionnalité Créer une tâche de révision ne fonctionne pas en raison d’une charge utile nulle qui entraîne l’échec de toutes les actions de révision suivantes liées à la tâche. NPR-30468 : correctif pour CQ-4274263
* Problème de connectivité d’Adobe Smart Tag via Datapower. NPR-30026 : correctif pour CQ-4269457
* L’affichage en colonne de l’interface utilisateur Assets renvoie une erreur lors de la tentative d’ouverture des filtres à gauche du rail. NPR-30501 : correctif pour CQ-4273862
* Lors de l’ajout de groupes synchronisés à partir du protocole LDAP dans les propriétés du groupe d’utilisateurs fermés (CUG) d’un dossier de ressources, le groupe n’est pas enregistré ni récupéré. NPR-30615 : correctif pour CQ-4274689
* Les champs d’orientation et de style de recherche de filtre n’appliquent pas la valeur auto-renseignée à la requête de recherche. NPR-30620 : correctif pour CQ-4275724
* Le lien de partage de ressources d’un dossier avec un espace et le caractère « &amp; » dans le nom affiche des cartes grises vides pour certains fichiers. NPR-30557 : correctif pour CQ-4270187
* Le formulaire de schéma de métadonnées de dossier ne détecte pas automatiquement le type de données et ne crée donc pas le TypeHint associé dans l’envoi du formulaire. NPR-30599 : correctif pour CQ-4275227
* Les options de recadrage et de rotation des fichiers sont désactivées dans l’interface utilisateur de création de DMS7. NPR-30118 : correctif pour CQ-4273221
* La fonction de partage de lien ne fonctionne pas sur l’instance AEM avec la configuration DMS7. NPR-30080, NPR-30492 : Correctif pour CQ-4273651
* L’ajout du composant Dynamic Media Scene7 à la page, puis la publication de la page, ne déclenche pas la configuration de Dmscene7 à chaque fois. NPR-30641 : correctif pour CQ-4275962
* Un IPSJobJournal a été ajouté dans AEM pour créer une seule tâche IPS (Intrusion Prevention Systems) par profil de traitement. NPR-30490 : correctif pour CQ-4273614
* Contenu multimédia dynamique : Ajout d’un par défaut pour exclure les ressources de la réplication sur le noeud de publication AEM. NPR-30538 : correctif pour CQ-4274678
* Un processus de retraitement externe a été mis en place pour la prise en charge de ressources multiples afin d’autoriser le dossier comme charge utile. Le workflow comporte deux étapes : retraitement des fichiers sans poignées via un mappage de métadonnées à l’étape suivante et retéléchargement de tous les fichiers sans poignée de ressources vers S7 dans une seule tâche IPS. Pour plus d’informations, voir Configuration des Services cloud Dynamic Media. NPR-30489 : correctif pour CQ-4272903
* Le téléchargement d’un fichier CSV incorrect après un fichier CSV correct efface le fichier CSV correct. Correctif pour CQ-4277694, CQ-4277814
* L’icône incorrecte spécifique aux dossiers de contribution est à supprimer. Correctif pour CQ-4277580
* Lors de la sélection d’un utilisateur dans le sélecteur d’utilisateur de l’onglet Contribution, le nom de l’utilisateur n’apparaît pas dans le tableau et la boîte de dialogue Supprimer l’utilisateur de la page de propriétés affiche un texte incorrect. Correctif pour CQ-4277875
* Les contributeurs ne peuvent pas être ajoutés au dossier de contribution à partir du sélecteur d’utilisateurs en sélectionnant l’utilisateur et en cliquant sur Ajouter. Correctif pour CQ-4277824, CQ-4278087
* La recherche par nom d’utilisateur en minuscules ne fonctionne pas dans le sélecteur d’utilisateurs. Correctif pour CQ-4277958, CQ-4277930
* Les non-administrateurs peuvent publier des fichiers dans un nouveau dossier d’un dossier de contribution. Correctif pour CQ-4278200
* Un utilisateur DAM (non-admin) n’a pas la possibilité d’ajouter des contributeurs au dossier de contribution. Correctif pour CQ-4278192
* Le bouton « Créer » est visible dans le dossier de contribution. Correctif pour CQ-4277560
* Le tri des requêtes par pertinence renvoie des documents InDesign ainsi que des modèles InDesign. Correctif pour CQ-4273864
* Si l’utilisateur dispose d’un ID de courrier électronique en majuscules, il n’est pas possible d’archiver les fichiers qui ont été précédemment extraits. Correctif pour CQ-4276575
* L’opération Supprimer s’applique uniquement aux paramètres prédéfinis sélectionnés. Si l’écran actualise automatiquement la liste après l’opération, elle affiche les autres paramètres prédéfinis qui ont déjà été actualisés. Correctif pour CQ-4261461
* La configuration des services Dynamic Media Cloud en mode DMHybrid entraîne la création de plusieurs suites de rapports vides dans Analytics et l’absence d’ID de suite de rapports stockée dans AEM, ce qui entraîne la duplication des suites de rapports. Correctif pour CQ-4249780
* La synchronisation vers Scene7 de l’opération de renommage dans AEM Asset en nom dupliqué échoue. Correctif pour CQ-4276763
* Le contenu créé par l’utilisateur s’affiche incorrectement dans le panneau du filtre de recherche. Correctif pour CQ-4273875
* L’option Rechercher des images similaires n’est pas disponible pour les images TIFF. Correctif pour CQ-4278238
* Une option permettant de mettre en sourdine la vidéo au chargement dans VideoPlayer a été mise en œuvre. Correctif pour CQ-4266465
* Visionneuses - Visionneuse vidéo : poster=none fonctionne incorrectement en cas d’utilisation d’une vidéo externe. Correctif pour CQ-4265536
* Une icône d’attente est visible pendant la lecture vidéo sur les navigateurs IE11 et MS Edge. Correctif pour CQ-4251539
* Les fichiers README du kit SDK 3.8 et des lecteurs 5.13 ne sont pas mis à jour et contiennent des informations provenant de versions précédentes. Correctif pour CQ-4273737
* Le fragment de contenu est versionné avant même d’enregistrer les modifications. NPR-30616 : correctif pour CQ-4273088
* Remplacez Asset#getMetadata(String) par Asset#getMetadataValueFromJcr(String) dans le traitement des miniatures. NPR-30491 : correctif pour CQ-4273067
* Le téléchargement de fichiers jpg entraîne plusieurs instances du message : « ReplicateOnModifyWorker Replicating UPDATED » pour chaque ressource, ce qui entraîne une dégradation des performances.
* La décompression de l’archive zip à l’aide de la fonctionnalité Extraction de l’archive entraîne des problèmes avec les dossiers dont le nom contient le signe pourcentage (%) dans leur titre. NPR-29990 : correctif pour CQ-4270467

### Sites {#sites-6520}

* Si l’héritage de LiveCopy est rompu, les pages de copie dynamique affichent des liens de copie de langue au lieu de liens LiveCopy. (NPR-30980)
* Pour un nouveau plan directeur, si le nombre d&#39;enregistrements est supérieur à 40, seuls les 40 premiers enregistrements sont affichés. Le plan directeur affiche des lignes vierges pour le reste des enregistrements. (NPR-31182)
* Le module RTE (Rich Text Editor) du composant de texte affiche des caractères déformés pour le japonais et le coréen. (NPR-31331)
* L’éditeur de texte enrichi (RTE) ne permet pas d’insérer un tableau incorporé en tant qu’élément . (NPR-30879)
* L’Editeur de texte enrichi (RTE) d’échafaudage prêt à l’emploi applique de manière inattendue la taille de police en ligne aux éléments. (NPR-31284)
* Lorsqu’un utilisateur se concentre sur les champs du rail gauche et utilise un raccourci clavier pour coller le contenu, il colle le le contenu du Presse-papiers de l’éditeur de page au lieu du contenu copié à partir des champs du rail gauche. (NPR-31172)
* Lorsqu’un utilisateur ajoute un champ Téléchargement de fichier à un champ à plusieurs champs, le chemin d’accès à l’image est stocké dans le noeud de composant au lieu du noeud à plusieurs champs. (NPR-30882)
* L’API ResponsiveGridExporter ne renvoie pas l’interface com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporter. Le package com.day.cq.wcm.fondation.model.impl est déclaré comme package privé. (NPR-31398)
* Lorsqu’une page contenant des fragments d’expérience est ouverte en mode non éditeur (dans Auteur sans préfixe et `editor.html` `wcmmode=disabled`, ou dans Editeur), la requête se termine par le code d’erreur d’état HTTP 500. (NPR-30743)

### WCM - Éditeur de page {#wcm-page-editor-6520}

**Améliorations apportées au produit**

* EnhanceType de document avec plus de types MIME pour prendre en charge les options à plusieurs valeurs. Correctif pour CQ-4270694

### Gestion des fragments de contenu {#content-fragment-management-6520}

* La requête utilisée par l’interface utilisateur des modèles de fragments de contenu est très lente et entraîne éventuellement une erreur. Correctif pour CQ-4270807

### IU - Fondation {#ui-foundation}

* Le déclencheur de raccourcis empêche l’utilisateur d’utiliser &#39;m,&#39; &#39;p,&#39; &#39;e&#39; dans des interfaces utilisateur spécifiques. NPR-30355 : correctif pour GRANITE-26346
* La fermeture de l’interface utilisateur de recherche de ressources ne réinitialise pas le rail de gauche sur la sélection de contenu, ce qui empêche l’utilisateur d’ouvrir le rail de filtre la deuxième fois par la suite. NPR-30509 : correctif pour CQ-4274716
* Environnement à clients multiples : La navigation supérieure de l’interface utilisateur Asset n’est pas disponible et renvoie une erreur JavaScript. NPR-30104 : correctif pour GRANITE-26344

### Traduction {#translation-6520}

* Problème de traduction : seuls quelques composants sont traduits à l’aide de la traduction automatique. NPR-30079 : correctif pour CQ-4273764

### Plate-forme {#platform-6520}

* AEM Default Mail Sender ne peut pas envoyer de courrier à un serveur SMTP distant via TLS v1.2. NPR-30476 : Correctif pour GRANITE-26605

### Projets {#projects-6520}

* Les valeurs dam:folderThumbnailPaths ne sont pas actualisées et n’affichent pas les anciennes miniatures, même après la suppression des fichiers dans le dossier. NPR-30424 : correctif pour CQ-4273667
* Lorsque vous terminez avec l’option « déplacer », le titre et le nom du fichier restent inchangés. NPR-30647 : correctif pour CQ-4276265

### Communities {#communities-6520}

* Les diagnostics de synchronisation des utilisateurs sont complètement rompus et ne fonctionnent pas. NPR-30004, NPR-29943 : correctif pour CQ-4270287, CQ-4271348

### Sling {#sling}

* L’instance mise à niveau de 6.3.3.2 vers 6.5 entraîne la duplication des configurations OSGi. NPR-30130 : correctif pour CQ-4274016

### Intégration {#integration}

* Le contenu personnalisé ne s’affiche pas correctement sur l’instance de publication tant que l’instance n’a pas été redémarrée. NPR-30377 : correctif pour CQ-4273706
* Lors de la configuration de Launch sur un site web, l’adresse de la bibliothèque comporte une barre oblique (/) pré-activée, ce qui entraîne une intervention manuelle à chaque fois. NPR-30694 : correctif pour CQ-4275501

### Forms {#forms-6520}

>[!NOTE]
>
>Le Service Pack AEM n’inclut pas de correctifs pour AEM Forms. Les correctifs sont fournis à l’aide d’un module complémentaire Forms distinct.  En outre, un programme d’installation cumulatif est publié, qui comprend des correctifs pour AEM Forms sur JEE. Pour obtenir plus d’informations, voir [Installation du module complémentaire AEM Forms](#install-aem-forms-add-on-package) et [Installation du programme d’installation AEM Forms JEE](#forms-jee-installer).

Les principaux points forts d&#39;AEM Forms 6.5.2.0 sont les suivants :

* Ajout du paramètre Auto à `RenderAtClient` dans l’API `PDFFormRenderOptions` pour l’OSGi AEM Forms.

#### Package de modules complémentaires Forms {#forms-add-on-package}

**Intégration dorsale**

* Impossible de configurer le modèle de données de formulaire à l’aide d’une URL équilibrée de charge hébergée par AWS. NPR-30123 : correctif pour CQ-4273359
* Lors de la création du modèle de données de formulaire (FDM) avec le langage WSDL (Web Service Definition Language), le message d’erreur `Caused by: com.adobe.aem.dermis.exception.DermisException: java.lang.Exception: Unable to handle content type` est renvoyé : NPR-30477 : Correctif pour CQ-4272921

**Correspondence Management**

* &quot;Le rendu de l’interface utilisateur de création de correspondance (CCR UI) échoue par intermittence avec l’erreur suivante dans la console :
   `- Uncaught Error: variable [object Object]is already known the letter`- NPR-30127

**Communication interactive**

* Un champ marqué comme obligatoire dans le modèle de données de formulaire s’affiche comme requis dans l’interface utilisateur de création de correspondance (CCR UI). NPR-30623 : correctif pour CQ-4274902

**Forms - Workflow**

* Les variables de sortie non mappées sur les dossiers de contrôle provoquent l’échec de l’appel. Correctif pour CQ-4264451

**Formulaires HTML5**

* Lorsque le code personnalisé ou le projet est déployé pour la deuxième fois, la page ne s’affiche pas et l’erreur suivante se produit :

   `org.apache.sling.scripting.sightly.SightlyException.`

   NPR-30539 : correctif pour CQ-4272509

* Lors de l’utilisation de l’option Accès aux ordinateurs de bureau non visuels en mode Navigation pour lire un formulaire HTML5, le navigateur Chrome affiche &quot;graphic&quot; avant chaque graphique vectoriel évolutif (SVG) dans la conception du formulaire. NPR-30449 : correctif pour CQ-4274732

#### Programme d’installation de Forms JEE {#forms-jee-installer}

**Forms - Document Security**

* L’application d’une signature avec horodatage échoue avec l’erreur : ALC-DSC-003-000: com.adobe.idp.dsc.DSCInvocationException : Erreur d&#39;appel. NPR-30820 : correctif pour CQ-4275852

**Forms - Document Services**

* Si &quot;SubmitURL&quot; contient une esperluette (&amp;), des erreurs d’analyse sont affichées dans le journal lorsque la demande POST est effectuée pour le rendu du servlet pdf. NPR-30865 : correctif pour CQ-4278232

**Forms - Foundation JEE**

* Le service HTMLtoPDF n’affiche pas maxReuseCount dans la console JMX. NPR-30134, NPR-30304 : correctif pour CQ-4273763
* L’ajout ou la modification d’une connexion à un service Web en appelant des services Web à partir d’AEM Forms Workbench renvoie une erreur : ClassNotFoundException org.apache.axis.message.SOAPBodyElement. NPR-30105 : correctif pour CQ-4273217

### Packs de fonctionnalités inclus {#feature-packs-included}

>[!NOTE]
>
>Pour les clients AEM Forms, il est impératif d’installer le module complémentaire AEM Forms après l’installation de tout pack de service, pack de correctif cumulatif ou pack de fonctionnalités d’AEM.

#### Sites {#sites-feature-packs-included}

* Une propriété de configuration permettant d’exporter directement des fragments d’expérience vers des espaces de travail définis par l’utilisateur pour Adobe Target a été ajoutée. NPR-29189 : correctif pour CQ-4249782

#### Forms - Document Services {#forms-document-services-1}

* Ajout du paramètre Auto à `RenderAtClient` dans l’API `PDFFormRenderOptions` pour l’OSGi AEM Forms. NPR-30759 : correctif pour CQ-4278193

## AEM 6.5.1.0 {#release-6510}

AEM 6.5.1.0 is an important release that includes performance, stability, security, and key customer fixes and enhancements released since the general availability of AEM 6.5 in *April 2019.* Elle peut être installée sur AEM 6.5.

Les principaux points forts de cette version du Service Pack incluent les éléments suivants :

* Activation de l’inclusion de l’état d’interface utilisateur dynamique dans le suivi des événements en tant qu’attributs personnalisés.
* Prise en charge de la diffusion de fichiers vidéo à 360 degrés dans Dynamic Media Scene7.
* Enabled *Japanese Word Wrap* feature via the styles plugin of Rich Text Editor. Pour plus d’informations, voir [Configuration du renvoi à la ligne de mots japonais](/help/sites-administering/configure-rich-text-editor-plug-ins.md#jpwordwrap)

### Assets

* Mise à jour de l&#39;interface DAM DMGGateway pour la prise en charge multipartie S3. NPR-29740 : correctif pour CQ-4226303
* Le de rendus génère une `Only empty tenantId is currently supported` erreur après la mise à niveau vers AEM 6.5\. NPR-29986 : correctif pour CQ-4272353
* La boîte de dialogue Supprimer n’est pas visible pour autoriser la suppression de tâches. NPR-29720 : correctif pour CQ-4271074
* Après avoir ajouté le titre du fichier dans la page de propriétés, lorsqu’un utilisateur tente de fermer la page, AEM ouvre à nouveau la page de propriétés. NPR-29627 : correctif pour CQ-4264929
* VersioningTimelineEventProvider doit fournir la version racine avec le nœud de type nt : version. Correctif pour GRANITE-26063
* Mise en œuvre de la capacité de télécharger et de lire des vidéos 360 sphériques en mode AEM DM-Scene7. Correctif pour CQ-4265131
* La Live Copy récupère un état incorrect si la source est modifiée. Correctif pour CQ-4265451
* Activation de la prise en charge du Gestionnaire de sites multiples pour les ressources. Correctif pour CQ-4271453, CQ-4268621, CQ-4257491
* L’interface AEM doit afficher une entrée supplémentaire pour la version actuelle de la ressource dans la chronologie, affichant le dernier commentaire d’arrivée à partir d’Adobe Asset Link. Correctif pour CQ-4262864
* Le Journal des fragments de contenu affiche un message d’erreur lorsque des propriétés sont manquantes. Correctif pour CQ-4272560
* Un problème survient avec le lecteur vidéo Scene7 lorsqu’il est agrandi en plein écran. Correctif pour CQ-4266700
* ZoomVerticalViewer : Les boutons de panoramique ne doivent pas être affichés si un seul fichier d’image est utilisé. Correctif pour CQ-4264795
* La suppression d’un nœud enfant dans la Live Copy doit détacher les informations liveRelationship. Correctif pour CQ-4270395
* Le schéma de métadonnées contient uniquement des éléments de la configuration globale et ne contient pas ceux du client actif. La valeur de l’URL formPath est rétablie par défaut, même en cas de modification. NPR-29945 : correctif pour CQ-4262898
* La publication des paramètres d’image prédéfinis sur Brand Portal échoue avec le code d’erreur 500. NPR-29510 : correctif pour CQ-4268659

### Sites

* Les propriétés vides et les propriétés multiples ne se propagent pas à partir du plan directeur lors du déploiement. La réinitialisation de la Live Copy avec le plan directeur ne fonctionne pas pour les composants. NPR-29253 : correctif pour CQ-4264928, CQ-4264926, CQ-4267722
* CoralUI, when used with `Multifield`, stores the `fileReferenceParameter` at the component level instead of multifield level. NPR-29537 : correctif pour CQ-4266129
* Amélioration du composant de texte AEM et de l’éditeur de texte en japonais. NPR-29785 : correctif pour CQ-4265090
* La page restaurée avec la distorsion du temps doit faire référence à l’image correcte au moment du contrôle de version. NPR-29431 : correctif pour CQ-4262638
* Problème d’héritage des noeuds du système de style du parent à l’enfant. NPR-29516 : correctif pour CQ-4270330
* Message d’erreur lors de la configuration de la publication sociale dans l’authentification Facebook. NPR-29211 : correctif pour CQ-4266630
* La miniature générée sur le fragment de contenu affiche une représentation de calendrier interne pour les champs Date et Heure. NPR-29531 : correctif pour CQ-4269362
* L’ouverture de l’onglet Autorisations dans l’implémentation Coral2 n’affiche pas les boutons. Correctif pour CQ-4269419

### Commerce

* ConstraintViolationException, lors de l’exécution d’une migration différée de contenu pour le commerce électronique. NPR-29247 : correctif pour CQ-4264383

### Gestion des fragments de contenu

* Parsing error when opening a Content Fragment which has characters dollar `($)` and open brace `({)`. Correctif pour CQ-4270266

### Fragments d’expérience

* Exportez des fragments d’expérience AEM vers Adobe Target. Correctif pour CQ-4265469
* L’exportation des fragments d’expérience vers le échoue avec l’image dynamique. Correctif pour CQ-4269606

* L’utilisateur atteint une impasse lorsqu’il tente de déplacer les fragments d’expérience dans Omnisearch en mode d’affichage Carte. Correctif pour CQ-4263848

### WCM - Éditeur de page

* Les scripts intersites (XSS) se reflètent lors de l’utilisation d’un sélecteur non valide. Correctif pour CQ-4270397

### Réplication

* Les données fournies par l’utilisateur ne sont pas ignorées lors de la sortie dans le composant `cq/replication/components/agent`, ce qui entraîne une vulnérabilité Cross-site scripting (XSS) par stockage. Correctif pour CQ-4266263

### Processus

* Le champ du sélecteur de calendrier du participant à la boîte de dialogue est rompu. NPR-29727 : correctif pour CQ-4270423

### WCM - Éditeur d’application monopage

* Activation de la récupération du contenu prérendu à partir d’un point de fin distant. Correctif pour CQ-4270238
* Avertissements dans les journaux lors de l’ouverture d’une page de modèle d’application monopage générée côté serveur. Correctif pour CQ-4270238

### WCM - MSM

* La mise à niveau vers AEM 6.4.3 fait que le déploiement de Multi-Site Manager prend du temps. Correctif pour CQ-4271410

### Intégration

* Échec des informations d’identification BrightEdge en cas d’erreur de connexion. NPR-29168 : correctif pour CQ-4265872

* Un message d’exception s’affiche lorsque vous tentez de modifier et d’enregistrer la configuration de lancement d’AEM. NPR-29176 : Correctif pour CQ-4265782 / CQ-4266153

### Interface utilisateur

* Ajout de la prise en charge du suivi des états de l’interface utilisateur dynamique en tant qu’attributs personnalisés lors du suivi de certains événements dans l’API de suivi des bases. Correctif pour GRANITE-26283
* Impossible de définir la fonction de suivi sur le bouton d&#39;envoi. Correctif pour GRANITE-26326
* L’assistant ne parvient pas à définir la fonction de suivi sur le bouton d’envoi. NPR-29995, NPR-30025 : correctif pour CQ-4264289

### Communities

* Impossible d&#39;aligner les nouveaux badges dans la liste déroulante de la page du profil du membre. NPR-29381 : correctif pour CQ-4267987
* Les visiteurs et les membres, sans privilèges de modérateur, peuvent voir les publications non approuvées / en attente en collant l’URL. NPR-29724 : correctif pour CQ-4271124, CQ-4271441
* Un temps de réponse élevé allant jusqu&#39;à 40-50 secondes est observé lors de la connexion de l&#39;utilisateur à la Communauté. NPR-29677 : correctif pour CQ-4269444

### Réplication

* Le composant Agent de réplication est exposé à une vulnérabilité qui divulgue des informations sensibles à des utilisateurs non autorisés. NPR-29611 : correctif pour GRANITE-25070

* Fuite de session pendant OAuth pour chaque réplication vers Brand Portal. NPR-30001 : correctif pour GRANITE-26196

### Projets

* La publication des ressources du dossier /content/dam/mac d’AEM Author vers Brand Portal ne fonctionne pas. NPR-29819 : correctif pour CQ-4271118

### Plate-forme

* HtmlLibraryManager supprime tout le contenu de crx-quickstart lors de l’invalidation du cache. NPR-29863 : correctif pour GRANITE-26197

### Felix

* Les détails d’utilisation de la mémoire ne s’affichent pas dans la console système lors de l’utilisation de Java11\. NPR-29669

### Forms

Les principaux points forts d&#39;AEM Forms 6.5.1.0 sont les suivants :

* OSGi only: Added a new attribute `PAGECOUNT` in Output and Forms Service.

* OSGI uniquement : Prise en charge de la création de fichiers PDF statiques à l’aide de Forms Service.
* Autorisations activées sur XMLForm.exe pour les administrateurs et les utilisateurs racines.
* Prise en charge d’ADFS v3.0 pour l’intégration de Dynamics sur site activée.

#### Package de module complémentaire Forms

**Intégration du serveur principal**

* Échec de récupération du WSDL (Web Service Definition Language) protégé. NPR-29944 : correctif pour CQ-4270777
* Lorsque AEM Forms est installé sur IBM WebSphere, la création d’un modèle de données de formulaire basé sur SOAP échoue. Correctif pour CQ-4251134
* Activation de la prise en charge d’Active Directory Federation Services (ADFS) v3.0 pour l’intégration sur site de Microsoft Dynamics. Correctif pour CQ-4270586
* Lorsque le titre d’une source de données est modifié, le modèle de données de formulaire n’affiche pas le titre mis à jour. Correctif pour CQ-4265599
* Si le nom d’une entité ou d’un attribut contient un trait d’union ou un espace,   ne parvient pas à évaluer ces entités et attributs. Correctif pour CQ-4225129

* Une sortie incorrecte est observée lorsqu’un deux-points est présent dans la sortie de chaîne primitive. Correctif pour CQ-4260825

* Même si aucun contenu n’est attendu de la sortie de l’API REST, l’opération d’appel du modèle de données de formulaire renvoie une erreur. Correctif pour CQ-4268828

**Formulaires adaptatifs**

* Impossible d’ajouter une nouvelle instance dans le fragment de formulaire adaptatif pendant le chargement différé. NPR-29818 : correctif pour CQ-4269875
* Le composant Vérifier ne consigne ni n’affiche d’erreur pour les modèles de document d’enregistrement. Correctif pour CQ-4272999
* Ajout de la prise en charge nécessaire à la désactivation de l’éditeur de mise en page pour les formulaires adaptatifs. Correctif pour CQ-4270810
* Restauration de l’étape de vérification pour les formulaires adaptatifs dans AEM 6.5\. Correctif pour CQ-4269583

* L’échec de validation du champ Formulaire adaptatif rompt Adobe Sign. Correctif pour CQ-4269463
* Lorsqu’une instance d’AEM Forms comporte plus de 20 fragments de formulaire adaptatif et que le nom de tous les fragments de formulaire commence par la même chaîne, la recherche renvoie au moins 20 fragments créés récemment. Correctif pour CQ-4264414, CQ-4264914

* Problèmes de performances lorsque l’application de formulaires adaptatifs est utilisée avec un jeu de données volumineux. . Correctif pour CQ-4235310

* Lorsqu’il est accessible via un compte anonyme sur une instance de publication, le script GuideRuntime ne charge pas. Correctif pour CQ-4268679

**Forms - Communication interactive**

* Le modèle de communication interactive ne répertorie pas les composants d’en-tête et de pied de page dans la liste des composants autorisés. Correctif pour CQ-4237895
* Lorsque vous créez un modèle d’impression de communication interactive contenant un champ d’image, le titre du graphique est défini sur vide. Correctif pour CQ-4264772
* La couleur de ligne d’un graphique, une fois supprimée, est paramétrée comme non définie. Correctif pour CQ-4264762
* Les modifications apportées au calque de mise en page lors de l’ du fragment disparaissent lors de l’exécution de la synchronisation des modifications. Correctif pour CQ-4266054
* L’élément de modèle de données de formulaire à l’intérieur d’un fragment de document lié à un champ de texte n’affiche pas d’icône d’héritage et permet la liaison. Correctif pour CQ-4261089
* L’API de rendu de canal d’impression n’a pas la possibilité de transmettre des données en tant que paramètre dans l’API. Correctif pour CQ-4263540
* Les paramètres de l’agent ne sont pas visibles, car la case à cocher Modifier par l’agent est décochée lorsque le type de liaison est modifié du fragment de texte en Aucun/Objet de modèle de données pour le champ/variable de chaîne. Correctif pour CQ-4261953
* Lors de l’envoi de l’interface utilisateur de l’agent, le fichier json de données Web résultant stocke des informations pour les champs non liés annulés par héritage. Correctif pour CQ-4265621

**Forms - Workflow**

* Lorsqu’un formulaire est renvoyé à partir de la boîte d’envoi de l’application de formulaires adaptatifs, cela entraîne une perte de données. NPR-28345 : correctif pour CQ-4260929
* Les documents ne sont pas fermés lors de l’enregistrement pour les cas non variables. Correctif pour CQ-4269784
* L&#39;application de formulaires adaptatifs a abandonné la prise en charge de Microsoft Windows 8.1\. Correctif pour CQ-4265274
* Lorsqu’une image de plus de 2 Mo est attachée en tant que pièce jointe au niveau du champ à un formulaire dans la version Android de l’application AEM Forms, l’application se bloque. Correctif pour CQ-4265578

* Activation des options de préremplissage pour le canal d’impression Communication interactive dans la tâche Attribuer. Correctif pour CQ-4265577
* Les utilisateurs ne peuvent pas afficher une tâche partagée tant qu’ils ne sont pas membres du groupe auquel la tâche est affectée. Correctif pour CQ-4248733
* L’enregistrement ou l’envoi d’applications JEE sur une application de formulaire adaptatif est bloqué sous Windows. Correctif pour CQ-4268704
* Le modèle de données de formulaire associé à la variable de modèle de données de formulaire n’est pas visible. Correctif pour CQ-4266554
* Aucune prise en charge de la variable de statut du symbole de document utilisant la prise en charge des variables n’existe. Correctif pour CQ-4266312
* Les envois à partir de l’espace de travail échouent avec un caractère d’umlaut. Correctif pour CQ-4263172
* Lors d’une configuration mise à niveau, si le processus est ouvert pour modification, une erreur s’affiche au lieu du nom du processus dans l’interface utilisateur du dossier de contrôle. Correctif pour CQ-4238579

**Forms - Gestion**

* Lorsqu’une extension autre que xsd ou schema.json est téléchargée, le téléchargement n’a pas lieu et aucun message d’erreur n’est généré. Correctif pour CQ-4266716

**Forms - Gestion de correspondance**

* L’interface utilisateur de création de correspondance d’AEM Forms 6.5 (CCR UI) ne parvient pas à ouvrir la correspondance créée avec AEM Forms 6.3. Correctif pour CQ-4266392
* La fonction Somme dans XDP ne fonctionne pas si le type de données DDE est un numéro. Correctif pour CQ-4227403
* La logique d’invalidation du cache de lettres en mémoire doit être mise à jour, car lorsqu’un fichier est publié, son heure de dernière modification n’est pas mise à jour. Correctif pour CQ-4250465
* Impossible de publier le fragment de document, DD et lettres. Correctif pour CQ-4272893

#### Programme d’installation de Forms JEE

**PDF Generator**

* La conversion des fichiers CAO en PDF échoue avec le JDK 64 bits. NPR-29924, NPR-29925 : Correctif pour CQ-4272113
* Remplacement du nom de PhantomJS en WebToPDF pour la conversion HTML vers PDF. NPR-29933 : correctif pour CQ-4234545
* Une erreur est générée lors de la conversion du fichier zip au format PDF. Correctif pour CQ-4268628

**Forms - Designer**

* Lorsqu’une vérification complète de l’accessibilité est effectuée sur le PDF statique créé à l’aide d’AEM Form Designer, la vérification de la langue principale échoue en raison de l’attribut de langue manquant. Correctif pour CQ-4272923, CQ-4271002

**Forms - Document Security**

* La signature numérique avec le module de sécurité matérielle (HSM) ne fonctionne pas sous OSGi Linux sur Java 11 et Java 8\. NPR-29838 : correctif pour CQ-4270441
* La signature numérique avec le module de sécurité matérielle (HSM) ne fonctionne pas sur JEE Linux ni tous les serveurs d’applications pris en charge, c’est-à-dire JBoss et Websphere. NPR-29839 : correctif pour CQ-4266721
* La vérification des signatures dans un PDF à l’aide de PDF Advanced Electronic Signatures (PAdES) génère InvalidOperationException. NPR-29842 : correctif pour CQ-4244837
* Ajout de la prise en charge de Document Security Extension pour Office 2019\. Correctif pour CQ-4254369, CQ-4259764

**Forms - Document Services**

* La conversion au format PDF échoue au format PDF/A-1b avec le champ Formulaire pour lequel l’apparence n’est pas définie. NPR-29940 : correctif pour CQ-4269618

* OSGi : Impossible de déterminer le nombre de pages générées pendant le rendu. NPR-28922 : correctif pour CQ-4270870
* Prise en charge des fichiers PDF statiques à l’aide de Forms Service dans AEM Forms OSGi activée. NPR-28572 : correctif pour CQ-4270869
* Impossible de modifier les autorisations sur XMLForm.exe. NPR-29828, NPR-29237 : Correctif pour le Q-4267080
* Le fichier PDF statique créé par le module de sortie du serveur AEM Forms ne renseigne pas l’attribut /  la balise de langue avec la langue du document créé. NPR-27332 : correctif pour CQ-4271002

**Forms - Foundation JEE**

* L’indisponibilité de pdfg_srt dans les artefacts finaux provoque l’échec du programme d’installation. NPR-29854 : correctif pour CQ-4270137
* LCBackupMode.sh ne fonctionne pas. NPR-29840 : correctif pour CQ-4269424
* La référence de port UDP doit être supprimée de l’interface utilisateur (IU) pour WebSphere. Correctif pour CQ-4264782

### Packs de fonctionnalités inclus

#### Ressources - Inclus

* Activation de la prise en charge du Gestionnaire de sites multiples pour les ressources. For more information, see [Reuse assets using MSM for Assets](https://helpx.adobe.com/experience-manager/6-5/help/assets/reuse-assets-using-msm.html). NPR-29199 : correctif pour CQ-4259922

#### Sites - Inclus

* Exportez des fragments d’expérience AEM vers Adobe Target. For more details, see [The Experience Fragment Link Rewriter Provider - HTML](https://helpx.adobe.com/experience-manager/6-5/help/sites-developing/experience-fragments.html#TheExperienceFragmentLinkRewriterProviderHTML). Correctif pour CQ-4265469

#### Forms - Document Services - Inclus

* OSGi uniquement : Ajout d’un nouvel attribut PAGECOUNT dans Output et Forms Service. NPR-28922 : correctif pour CQ-4270870
* OSGi uniquement : Prise en charge de la création de fichiers PDF statiques à l’aide de Forms Service. NPR-28572 : correctif pour CQ-4270869
* Autorisations activées sur XMLForm.exe pour les administrateurs et les utilisateurs racines. NPR-29237 : correctif pour CQ-4267080

### Lots OSGi et packages de contenu

Les documents texte suivants répertorient les lots OSGi et les packages de contenu inclus dans AEM 6.5.1.0.

Liste des lots OSGi inclus dans AEM 6.5.1.0

[Obtenir le fichier](assets/6_5-bundle-list.txt)

Liste des packages de contenu inclus dans AEM 6.5.1.0

[Obtenir le fichier](assets/6_5-content-package-list.txt)
