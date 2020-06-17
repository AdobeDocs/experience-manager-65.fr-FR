---
title: Types de nœuds personnalisés
seo-title: Types de nœuds personnalisés
description: AEM est architecturé autour de Sling et utilise un référentiel JCR avec des types de nœuds proposés par les deux plates-formes. Cependant, AEM fournit également un éventail de types de nœuds personnalisés.
seo-description: AEM est architecturé autour de Sling et utilise un référentiel JCR avec des types de nœuds proposés par les deux plates-formes. Cependant, AEM fournit également un éventail de types de nœuds personnalisés.
uuid: f2022504-e433-4b42-9cc1-eef41086483a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: aae186eb-e059-4a9d-b02d-86a86c86589d
translation-type: tm+mt
source-git-commit: 07eb53f19cf7c7c2799c95ba9df54f4673d72fdc
workflow-type: tm+mt
source-wordcount: '1918'
ht-degree: 61%

---


# Types de nœuds personnalisés{#custom-node-types}

AEM étant basé sur Sling et utilisant un référentiel JCR, les types de noeud proposés par ces deux solutions sont disponibles pour utilisation :

* [Types de nœuds JCR](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/3_Repository_Model.html#3.1.7-Node-Types)
* [Types de nœuds Sling](https://cwiki.apache.org/confluence/display/SLING/Sling+Node+Types)

De plus, AEM fournit une gamme de types de noeud personnalisés.

## Audit {#audit}

### cq:AuditEvent {#cq-auditevent}

**Description**

Définit le type d’un nœud d’événement d’audit.

* `@prop cq:time`
* `@prop cq:userid`
* `@prop cq:path`
* `@prop cq:type`
* `@prop cq:category`
* `@prop cq:properties`

**Définition**

* `[cq:AuditEvent]`
   * `- * (undefined)`
   * `- * (undefined) multiple`
   * `+ * (nt:base) = nt:base multiple version`
* `- cq:time (date)`
* `- cq:userid (string)`
* `- cq:path (string)`
* `- cq:type (string)`
* `- cq:category (string)`
* `- cq:properties (binary)`

## Commentaire {#comment}

### cq:Comment {#cq-comment}

**Description**

Définit le type d’un nœud de commentaire.

* `@prop userIdentifier`

**Définition**

* `[cq:Comment] > mix:title, mix:created, mix:language, nt:unstructured, cq:Taggable`
* `- email (string)`
* `- ip (string)`
* `- referer (string)`
* `- url (string)`
* `- userAgent (string)`
* `- userIdentifier (string)`
* `- authorizableId (string)`

### cq:CommentAttachment {#cq-commentattachment}

**Description**

Defines the nodetype of a `commentattachment` node

**Définition**

* `[cq:CommentAttachment] > nt:file`
   * `- * (undefined)`
   * `- * (undefined) multiple`

### cq:CommentContent {#cq-commentcontent}

**Description**

Définit le type d’un nœud de contenu du commentaire.

**Définition**

* `[cq:Comment] > mix:title, mix:created, mix:language, nt:unstructured, cq:Taggable`
* `- email (string)`
* `- ip (string)`
* `- referer (string)`
* `- url (string)`
* `- userAgent (string)`
* `- userIdentifier (string)`
* `- authorizableId (string)`

### cq:GeoLocation {#cq-geolocation}

**Description**

Mixin qui définit un emplacement géographique en degrés décimaux (DD).

* `@prop latitude` - latitude codée en tant que doublon à l&#39;aide de degrés décimaux
* `@prop longitude` - longitude codée en tant que doublon en degrés décimaux

**Définition**

* `[cq:GeoLocation] mixin`
* `- latitude (double)`
* `- longitude (double)`

### cq:Trackback {#cq-trackback}

**Description**

Définit le type d’un nœud de rétrolien.

**Définition**

* `[cq:Trackback] > mix:title, mix:created, mix:language, nt:unstructured`

## Base {#core}

### cq:Page {#cq-page}

**Description**

Définit la page CQ par défaut.

* `@node jcr:content` - Contenu du Principal de la page.

**Définition**

* `[cq:Page] > nt:hierarchyNode orderable`
   * `+ jcr:content (nt:base) = nt:unstructured copy primary`
   * `+ * (nt:base) = nt:base version`

### cq:PseudoPage {#cq-pseudopage}

**Description**

Définit un type de mixin qui marque les nœuds en tant que pseudo-pages. Cela signifie qu’elles peuvent être adaptées pour la prise en charge de l’édition de page et WCM.

**Définition**

* `[cq:PseudoPage] mixin`

### cq:PageContent {#cq-pagecontent}

**Description**

Définit le nœud par défaut du contenu de la page, avec les propriétés minimales telles qu’elles sont utilisées par WCM.

* `@prop jcr:title` - Titre de la page.
* `@prop jcr:description` - Description de cette page.
* `@prop cq:template` - Chemin d&#39;accès au modèle utilisé pour créer la page.
* `@prop cq:allowedTemplates` - Liste des expressions régulières utilisées pour déterminer le(s) chemin(s) d’accès au modèle autorisé.
* `@prop pageTitle` - Titre généralement affiché dans la `<title>` balise .
* `@prop navTitle` - Titre généralement utilisé dans la navigation.
* `@prop hideInNav` - Détermine si la page doit être masquée dans la navigation.
* `@prop onTime` - Heure à laquelle cette page devient valide.
* `@prop offTime` - Heure à laquelle cette page devient non valide.
* `@prop cq:lastModified` - Date de la dernière modification de la page (ou de ses paragraphes).
* `@prop cq:lastModifiedBy` - Dernier utilisateur à modifier la page (ou ses paragraphes).
* `@prop jcr:language` - Langue du contenu de la page.

>[!NOTE]
>
>Il n’est pas obligatoire pour le contenu de page d’utiliser ce type.

**Définition**
* `[cq:PageContent] > nt:unstructured, mix:title, mix:created, cq:OwnerTaggable, sling:VanityPath, cq:ReplicationStatus, sling:Resource orderable`
   * `- cq:template (string)`
   * `- cq:allowedTemplates (string) multiple`
   * `- pageTitle (string)`
   * `- navTitle (string)`
   * `- hideInNav (boolean)`
   * `- onTime (date)`
   * `- offTime (date)`
   * `- cq:lastModified (date)`
   * `- cq:lastModifiedBy (string)`
   * `- cq:designPath (string)`
   * `- jcr:language (string)`

### cq:Template {#cq-template}

**Description**

Définit un modèle CQ.

* `@node jcr:content` - Contenu par défaut pour les nouvelles pages.
* `@node icon.png` - Fichier contenant une icône caractéristique.
* `@node thumbnail.png` - Fichier contenant une miniature de caractéristique.
* `@node workflows` - Attribue automatiquement la configuration de processus. La configuration suit la structure ci-dessous :
   * `+ workflows`
      * `+ name1`
         * `- cq:path`
            * `- cq:workflowName`
* `@prop allowedParents` - Schémas d’expressions régulières utilisés pour déterminer le(s) chemin(s) d’accès aux modèles autorisés en tant que modèles parents.
* `@prop allowedChildren` - Schémas d’expressions régulières utilisés pour déterminer le(s) chemin(s) d’accès aux modèles autorisés en tant que modèles enfants.
* `@prop ranking` - Position au sein de la liste de modèles de la boîte de dialogue de création de page.

**Définition**

* `[cq:Template] > nt:hierarchyNode, mix:title`
   * `- * (undefined)`
   * `- * (undefined) multiple`
   * `+ * (nt:base) = nt:base multiple version`
   * `+ jcr:content (nt:base) copy`
   * `+ icon.png (nt:file) copy`
   * `+ thumbnail.png (nt:file) copy`
   * `+ workflows (nt:base) copy`
   * `- allowedParents (string) multiple`
   * `- allowedChildren (string) multiple`
   * `- ranking (long)`

### cq:Component {#cq-component}

**Description**

Définit un composant CQ.

* `@prop jcr:title` - Titre du composant.
* `@prop jcr:description` - Description du composant.
* `@node dialog` - Boîte de dialogue Principal.
* `@prop dialogPath` - chemin de la boîte de dialogue Principal (alternative à la boîte de dialogue).
* `@node design_dialog` - Boîte de dialogue de conception.
* `@prop cq:cellName` - Nom de la cellule de conception.
* `@prop cq:isContainer` - Indique s&#39;il s&#39;agit d&#39;un composant de conteneur. Cela oblige à utiliser les noms de cellule des composants enfants au lieu des noms de chemin d’accès. Par exemple, `parsys` est un composant de conteneur. Si cette valeur n’est pas définie, la vérification est effectuée sur la base de l’existence d’une propriété `cq:childEditConfig`.
* `@prop cq:noDecoration` - Si la valeur est true, aucune `div` balise de décoration n&#39;est dessinée lors de l&#39;inclusion de ce composant.
* `@node cq:editConfig` - Configuration qui définit les paramètres de la barre d&#39;édition.
* `@node cq:childEditConfig` - La configuration de modification héritée par les composants enfants.
* `@node cq:htmlTag` - Définit des attributs de balise supplémentaires qui sont ajoutés à la balise &quot;environnante&quot; `div` lorsque le composant est inclus.
* `@node icon.png`- Fichier contenant une icône caractéristique.
* `@node thumbnail.png` - Fichier contenant une miniature de caractéristique.
* `@prop allowedParents` - Schémas d’expressions régulières utilisés pour déterminer le(s) chemin(s) d’accès des composants autorisés en tant que composants parents.
* `@prop allowedChildren` - Modèles d&#39;expression réguliers pour déterminer le ou les chemins des composants autorisés en tant que composants enfants.
* `@node virtual` - Contient des sous-noeuds qui reflètent les composants virtuels utilisés pour le glisser-déposer des composants.
* `@prop componentGroup` - Nom du groupe de composants, utilisé pour le glisser-déposer du composant.
* `@node cq:infoProviders` - Contient des sous-noeuds dont chacun possède une propriété `className` faisant référence à un `PageInfoProvider`.

**Définition**

* `[cq:Component] > nt:folder, mix:title, sling:ResourceSuperType`
   * `- * (undefined)`
   * `- * (undefined) multiple`
   * `+ * (nt:base) = nt:base multiple version`
   * `+ dialog (nt:base) = nt:unstructured copy`
   * `- dialogPath (string)`
   * `+ design_dialog (nt:base) = nt:unstructured copy`
   * `- cq:cellName (string)`
   * `- cq:isContainer (boolean)`
   * `- cq:noDecoration (boolean)`
   * `+ cq:editConfig (cq:EditConfig) = cq:EditConfig copy`
   * `+ cq:childEditConfig (cq:EditConfig) = cq:EditConfig copy`
   * `+ cq:htmlTag (nt:base) = nt:unstructured copy`
   * `+ icon.png (nt:file) copy`
   * `+ thumbnail.png (nt:file) copy`
   * `- allowedParents (string) multiple`
   * `- allowedChildren (string) multiple`
   * `+ virtual (nt:base) = sling:Folder copy`
   * `- componentGroup (string)`
   * `+ cq:infoProviders (nt:base) = nt:unstructured copy`

### cq:ComponentMixin {#cq-componentmixin}

**Description**

Définit un composant CQ en tant que type de mixin.

**Définition**

`[cq:ComponentMixin] > cq:Component mixin`

### cq:EditConfig {#cq-editconfig}

**Description**

Définit la configuration de la barre d’édition.

* `@prop cq:dialogMode` - Mode de la boîte de dialogue :
   * `floating` - Pour une boîte de dialogue flottante normale
   * `inline` - édition intégrée
   * `auto` - Détection automatique (en fonction de l’espace disponible)
* `@node cq:inplaceEditing` - Inplace la configuration de modification pour ce composant.
* `@prop cq:layout`- Disposition de la barre d&#39;édition :
   * `editbar` - barre d&#39;édition
   * `rollover` - cadre de roulement
   * `auto` - détection automatique
* `@node cq:formParameters`- Paramètres supplémentaires à ajouter au formulaire de boîte de dialogue.
* `@prop cq:actions`- Liste des actions (boutons de la barre d&#39;édition ou éléments de menu).
* `@node cq:actionConfigs` - Configurations de widgets pour les éléments de barre d&#39;édition ou de menu.
* `@prop cq:emptyText` - Texte à afficher si aucun contenu visuel n&#39;est présent.
* `@node cq:dropTargets` - Collection de `{@link cq:DropTargetConfig}` noeuds.

**Définition**

* `[cq:EditConfig] > nt:unstructured, nt:hierarchyNode orderable`
   * `- cq:dialogMode (string) < 'auto', 'floating', 'inline'`
   * `- cq:layout (string) < 'editbar', 'rollover', 'auto' + cq:formParameters (nt:base) = nt:unstructured`
   * `- cq:actions (string) multiple`
   * `+ cq:actionConfigs (nt:base) = nt:unstructured`
   * `- cq:emptyText (string)`
   * `+ cq:dropTargets (nt:base) = nt:unstructured`
   * `+ cq:listeners (nt:base) = cq:EditListenersConfig`

### cq:DropTargetConfig {#cq-droptargetconfig}

**Description**

Configure une cible de dépôt d’un composant. Le nom de ce nœud est utilisé comme ID pour l’opération de glisser-déposer.

* `@prop accept` - Liste des types de mime acceptés par la présente cible de largage ; par ex. `["image/*"]`
* `@prop groups` - Liste des groupes de déplacement qui acceptent une source.
* `@prop propertyName` - Nom de la propriété utilisée pour stocker la référence.

**Définition**

* `[cq:DropTargetConfig] > nt:unstructured orderable`
   * `- accept (string) multiple`
   * `- groups (string) multiple`
   * `- propertyName (string)`
   * `+ parameters (nt:base) = nt:unstructured`

### cq:VirtualComponent {#cq-virtualcomponent}

**Description**

Définit un composant CQ virtuel. Actuellement, ces options sont uniquement utilisées pour le nouvel assistant de déplacement des composants par glisser-déposer.

* `@prop jcr:title` - Titre de ce composant.
* `@prop jcr:description` - Description de ce composant.
* `@node cq:editConfig` - Modifier la configuration qui définit les paramètres de la barre d&#39;édition.
* `@node cq:childEditConfig`- Modifier la configuration héritée par les composants enfants.
* `@node icon.png` - Fichier contenant une icône caractéristique.
* `@node thumbnail.png` - Fichier contenant une miniature de caractéristique.
* `@prop allowedParents` -  Schémas d’expressions régulières utilisés pour déterminer le(s) chemin(s) d’accès des composants autorisés en tant que composants parents.
* `@prop allowedChildren` - Des schémas d&#39;expression réguliers pour déterminer le ou les chemins d&#39;accès des composants autorisés en tant que composants enfants.
* `@prop componentGroup` - Nom du groupe de composants pour le glisser-déposer du composant.

**Définition**

`[cq:VirtualComponent] > nt:folder, mix:title`
`- * (undefined)`
`- * (undefined) multiple`
`+ * (nt:base) = nt:base multiple version`
`+ cq:editConfig (cq:EditConfig) = cq:EditConfig copy`
`+ icon.png (nt:file) copy`
`+ thumbnail.png (nt:file) copy`
`- allowedParents (string) multiple`
`- allowedChildren (string) multiple`
`- componentGroup (string)`

### cq:EditListenersConfig {#cq-editlistenersconfig}

**Description**

Définit les écouteurs (côté client) à exécuter sur un événement de modification. Les valeurs doivent soit faire référence à une fonction d’écoute côté client valide, soit contenir un raccourci prédéfini :

* `REFRESH_PAGE`
* `REFRESH_SELF`
* `REFRESH_PARENT`

* `@prop aftercreate` - Se déclenche après la création d&#39;un composant.
* `@prop afteredit` - Se déclenche après la modification (modification) d&#39;un composant.
* `@prop afterdelete` - Se déclenche après la suppression d&#39;un composant.
* `@prop afterinsert` - Se déclenche après l’ajout d’un composant à ce conteneur.
* `@prop afterremove` - Se déclenche après la suppression d’un composant de ce conteneur.
* `@prop aftermove` - Se déclenche après que des composants ont été déplacés dans ce conteneur.

**Définition**

* `[cq:EditListenersConfig]`
   * `- &ast; (undefined)`
   * `- &ast; (undefined) multiple`
   * `+ &ast; (nt:base) = nt:base multiple version`
   * `- aftercreate (string)`
   * `- afteredit (string)`
   * `- afterdelete (string)`
   * `- afterinsert (string)`
   * `- afterremove (string)`
   * `- aftermove (string)`

## Gestion des actifs numériques {#dam}

### dam:AssetContent {#dam-assetcontent}

**Description**

Contenu d’une ressource DAM.

**Définition**

* `[dam:AssetContent] > nt:unstructured`
   * `+ metadata (nt:unstructured)`
   * `+ renditions (nt:folder)`

### dam:Asset {#dam-asset}

**Description**

Ressource DAM.

**Définition**

`[dam:Asset] > nt:hierarchyNode`
`+ jcr:content (dam:AssetContent) = dam:AssetContent copy primary`
`+ * (nt:base) = nt:base version`

### dam:Thumbnail {#dam-thumbnail}

**Description**

Miniature représentant une ressource DAM.

**Définition**

* `[dam:Thumbnails]`
   * `mixin`
   * `+ dam:thumbnails (nt:folder)`

## Liste des conteneurs de diffusion {#delivery-container-list}

### cq:containerList {#cq-containerlist}

**Description**

Liste des conteneurs.

**Définition**

* `[cq:containerList]`
   * `mixin`

## Page de diffusion {#delivery-page}

### cq:Cq4PageAttributes {#cq-cq-pageattributes}

**Description**

`cq:attributes` est le type de nœud des balises de version ContentBus. Ce nœud comporte uniquement une série de propriétés, dont trois sont prédéfinies : « created », « CSD » et « timestampe ».

* `@prop created (long) mandatory copy` - Horodatage de création des informations de version. Il s’agit généralement de l’heure d’archivage de la version précédente ou de l’heure de création de la page.
* `@prop csd (string) mandatory copy` - attribut standard csd, copie de la propriété cq:csd du noeud de page
* `@prop timestamp (long) mandatory copy` - Horodatage de la dernière modification de version, généralement heure de consignation.
* `@prop * (string) copy` - Attributs supplémentaires, versionnés avec le noeud parent.

**Définition**

* `[cq:Cq4PageAttributes] > nt:base`
   * `- created (long) mandatory copy`
   * `- csd (string) mandatory copy`
   * `- timestamp (long) mandatory copy`
   * `- &ast; (string) copy`

### cq:Cq4ContentPage {#cq-cq-contentpage}

**Description**

Le type de nœud `cq:contentPage` contient les définitions de propriété et de nœud enfant pour les pages de contenu ContentBus. Only when this mixin type is added to a node of type `cq:page`, a node becomes a ContentBus content page.

The items in a `cq:Cq4ContentPage` are:

* `@prop cq:csd` - Le CSD ContentBus de la page.
* `@node cq:content` - Contenu de la page. Ce nœud enfant n’existe pas si l’état du nœud de page est défini sur « Existant sans contenu » ou « Supprimé ».
* `@node cq:attributes` - Liste d’attributs de page, connus précédemment sous le nom de balises de version. Ce nœud est obligatoire pour le type cq:contentPage. Le noeud d’attributs est versionné lorsque la page est un noeud est versionné.

**Définition**

* `[cq:Cq4ContentPage]`
   * `- cq:csd (string) mandatory copy`
   * `+ cq:attributes (cq:Cq4PageAttributes)`

## Importateur {#importer}

### cq:PollConfig {#cq-pollconfig}

**Description**

Configuration du sondage.

* `@prop source (String) mandatory` - URI de source de données, requis et ne doit pas être vide
* `@prop target (String)` - Emplacement cible où sont stockées les données récupérées de la source de données. Ce paramètre est facultatif et est défini par défaut sur le nœud cq:PollConfig.
* `@prop interval (Long)` - Intervalle, en secondes, entre deux recherches de nouvelles données ou de données mises à jour auprès de la source de données. Ce paramètre est facultatif et défini, par défaut, sur 30 minutes (1 800 secondes).
* [Création de services d’importation de données personnalisés pour Adobe Experience Manager](https://helpx.adobe.com/experience-manager/using/polling.html)

**Définition**

* `[cq:PollConfig]
   * `mixin`
   * `- source (String) mandatory`
   * `- target (String)`
   * `- interval (Long)`

### cq:PollConfigFolder {#cq-pollconfigfolder}

**Description**

Type de nœud principal permettant de créer facilement des nœuds de configuration de sondage.

**Définition**

`[cq:PollConfigFolder] > sling:Folder, cq:PollConfig`

## Emplacement {#location}

### cq:GeoLocation {#cq-geolocation-1}

**Description**

Mixin qui définit un emplacement géographique en degrés décimaux (DD).

* `@prop latitude` - Latitude codée en tant que doublon avec des degrés décimaux.
* `@prop longitude` - Longitude codée en tant que doublon avec des degrés décimaux.

**Définition**

* `[cq:GeoLocation]
   * `mixin`
   * `- latitude (double)`
   * `- longitude (double)`

## Mailer {#mailer}

### cq:mailerMessage {#cq-mailermessage}

**Description**

Types de nœuds MailerService (Service mailer). Le mailer utilise des nœuds contenant ce mixin comme nœuds racines de définitions de message.

**Définition**

* `[cq:mailerMessage]`
   * `mixin`
   * `- messageStatus (string)`
   * `= 'new'`
   * `mandatory autocreated`

## MSM {#msm}

### cq:LiveRelationship {#cq-liverelationship}

**Description**

Définit un mixin LiveRelationship (Relation en direct). Un noeud source principal (de contrôle) et un noeud de copie dynamique (contrôlé) peuvent être virtuellement liés via LiveRelationship.

**Définition**

* `[cq:LiveRelationship] mixin`
   * `- cq:lastRolledout (date)`
   * `- cq:lastRolledoutBy (string)`
   * `- cq:sourceUUID (string)`

### cq:LiveSync {#cq-livesync}

**Description**

Définit un mixin LiveSync (Synchronisation en direct). Si un noeud est impliqué dans une LiveRelationship avec un noeud source principal (contrôle) et un noeud de copie dynamique (contrôlé), il est marqué comme LiveSync.

* `@prop cq:master` - Chemin d&#39;accès de la source principale (contrôle) de LiveRelationship.
* `@prop cq:isDeep` - Définit si la relation est disponible pour les enfants.
* `@prop cq:syncTrigger` - Définit quand est déclenché la synchronisation.
* `@node * LiveSyncAction` - Actions à effectuer lors de la synchronisation

**Définition**

`[cq:LiveSync] > cq:LiveRelationship mixin orderable`
`+ * (cq:LiveSyncAction) = cq:LiveSyncAction`
`+ cq:LiveSyncConfig (nt:base) = cq:LiveSyncConfig`

### cq:LiveSyncCancelled {#cq-livesynccancelled}

**Description**

Définit un mixin LiveSyncCancelled (Dernière synchronisation annulée). Annuler le comportement LiveSync d’un noeud de copie dynamique (contrôlé) qui peut être impliqué dans une relation LiveRelationship en raison de l’un de ses parents.

* `@prop cq:isCancelledForChildren` - Définit si LiveSync est annulé ; également pour les enfants.

**Définition**

* `[cq:LiveSyncCancelled] > cq:LiveRelationship mixin`
   * `- cq:isCancelledForChildren (boolean)`

### cq:LiveSyncAction {#cq-livesyncaction}

**Description**

Définit une action de synchronisation en direct (LiveSyncAction) associée à une synchronisation en direct (LiveSync).

* `@prop name` - Nom de l&#39;action
* `@prop value` - Valeur de l&#39;action

**Définition**

* `[cq:LiveSyncAction] > nt:unstructured`

### cq:LiveSyncConfig {#cq-livesyncconfig}

**Description**

Configuration de la synchronisation en direct.

**Définition**

* `[cq:LiveSyncConfig]`
   * `- cq:master (string) mandatory`
   * `- cq:isDeep (boolean)`
   * `- cq:trigger (string) /** deprecated **/`

Pour AEM 5.4, ajoutez à la fin de la liste :

* `- cq:rolloutConfigs (string) multiple /** deprecated **/`

### cq:BlueprintAction {#cq-blueprintaction}

**Description**

Action du plan directeur

**Définition**

* `[cq:BlueprintAction] > nt:unstructured`

## Plate-forme {#platform}

### cq:Console {#cq-console}

**Description**

Définit le type d’un nœud de console.

**Définition**

* `[cq:Console] > sling:VanityPath, mix:title`
   * `mixin`

## Réplication {#replication}

### cq:ReplicationStatus {#cq-replicationstatus}

**Description**

Définit le mixin des informations relatives à l’état de réplication.

* `@prop cq:lastPublished`- date de la dernière publication de la page (non utilisée).
* `@prop cq:lastPublishedBy`- Utilisateur qui a publié la page en dernier (non utilisé).
* `@prop cq:lastReplicated` - date de la dernière réplication de la page.
* `@prop cq:lastReplicatedBy` - Utilisateur qui a répliqué la page en dernier.
* `@prop cq:lastReplicationAction` - Action de réplication : activer ou désactiver.
* `@prop cq:lastReplicationStatus` - Etat de réplication (non utilisé).

**Définition**

* `[cq:ReplicationStatus]
   * `mixin`
   * `- cq:lastPublished (date) ignore`
   * `- cq:lastPublishedBy (string) ignore`
   * `- cq:lastReplicated (date) ignore`
   * `- cq:lastReplicatedBy (string) ignore`
   * `- cq:lastReplicationAction (string) ignore`
   * `- cq:lastReplicationStatus (string) ignore`

## Sécurité {#security}

### cq:ApplicationPrivilege {#cq-applicationprivilege}

**Description**

Définit un privilège d’application.

**Définition**

* `[cq:ApplicationPrivilege] mixin`

### cq:PrivilegeAcl {#cq-privilegeacl}

**Description**

Définit un privilège d’application ACL.

* `@prop cq:isPathDependent`
* `@node * ACEs`

**Définition**

* `[cq:PrivilegeAcl] > cq:ApplicationPrivilege mixin orderable`
   * `- cq:isPathDependent (boolean)`
   * `+ * (cq:PrivilegeAce) = cq:PrivilegeAce`

### cq:PrivilegeAce {#cq-privilegeace}

**Description**

Définit un privilège d’application ACE.

* `@prop path`
* `@prop deny`

**Définition**

* `[cq:PrivilegeAce]`
   * `- path mandatory`
   * `- deny (boolean)`

### cq:ApplicationPrivilege {#cq-applicationprivilege-1}

**Description**

Définit un privilège d’application.

**Définition**

* `[cq:ApplicationPrivilege] mixin`

### cq:PrivilegeAcl {#cq-privilegeacl-1}

**Description**

Définit un privilège d’application ACL.

* `@prop cq:isPathDependent`
* `@node * ACEs`

**Définition**

* `[cq:PrivilegeAcl] > cq:ApplicationPrivilege mixin orderable`
   * `- cq:isPathDependent (boolean)`
   * `+ * (cq:PrivilegeAce) = cq:PrivilegeAce`

### cq:PrivilegeAce {#cq-privilegeace-1}

**Description**

Définit un privilège d’application ACE.

* `@prop path`
* `@prop deny`

**Définition**

* `[cq:PrivilegeAce]`
   * `- path mandatory`
   * `- deny (boolean)`

## Importateur de site {#site-importer}

### cq:ComponentExtractorSource {#cq-componentextractorsource}

**Description**

Définit un type de mixin qui marque les fichiers pouvant être ouverts avec l’extracteur de composants.

**Définition**

`[cq:ComponentExtractorSource] mixin`

## Balisage {#tagging}

### cq:Tag {#cq-tag}

**Description**

Définit une balise unique, mais peut également en contenir plusieurs, créant ainsi une taxonomie.

**Définition**

* `[cq:Tag] > nt:base, mix:title`
   * `- sling:resourceType (String)`
   * `- * (undefined) multiple`
   * `- * (undefined)`
   * `+ * (nt:base) = cq:Tag version`

### cq:Taggable {#cq-taggable}

**Description**

Résume le mixin de base pour le contenu pouvant être balisé.

* `@node cq:tags`

**Définition**

* `[cq:Taggable]`
   * `- cq:tags (string) multiple`

### cq:OwnerTaggable {#cq-ownertaggable}

**Description**

Seuls les auteurs/propriétaires sont autorisés à baliser le contenu (balisage modéré/administré).

**Définition**

* `[cq:OwnerTaggable] > cq:Taggable`

### cq:UserTaggable {#cq-usertaggable}

**Description**

Tout site web public/utilisateur peut baliser le contenu (style Web2.0), utilisé à l’intérieur de cq:userContent.

**Définition**

* `[cq:UserTaggable] > cq:Taggable`
   * `mixin`

### cq:AllowsUserContent {#cq-allowsusercontent}

**Description**

Ajoute un `cq:userContent` sous-noeud qui peut être modifié par les utilisateurs. Chaque utilisateur dispose de son propre `cq:userContent/<userid>` sous-noeud, qui possède généralement le mixin `cq:UserTaggable`.

**Définition**

* `[cq:AllowsUserContent]`
   * `mixin`
   * `+ cq:userContent (nt:unstructured)`

Extended variant, more explicitly defining the `cq:userContent` tree

* `[cq:AllowsUserContent]`
   * `mixin`
   * `+ cq:userContent (cq:UserContent)`

### cq:UserContent {#cq-usercontent}

**Description**

Peut être modifié par les utilisateurs.

**Définition**

* `[cq:UserContent] > nt:unstructured`
   * `// userids`
   * `+ * (cq:UserData)`
   * `// other content`
   * `+ * (nt:base)`

### cq:UserData {#cq-userdata}

**Description**

Données utilisateur

**Définition**

* `[cq:UserData] > nt:unstructured, cq:UserTaggable`

## Widgets {#widgets}

### cq:ClientLibraryFolder {#cq-clientlibraryfolder}

**Description**

Dossier de bibliothèques clientes

**Définition**

* `[cq:ClientLibraryFolder] > sling:Folder`
   * `- categories (string) multiple`
   * `- dependencies (string) multiple`

### cq:Widget {#cq-widget}

**Description**

Widget

**Définition**

* `[cq:Widget] > nt:unstructured orderable`
   * `- xtype (string)`
   * `- name (string)`
   * `- title (string)`
   * `+ items (nt:base) = cq:WidgetCollection copy`

### cq:WidgetCollection {#cq-widgetcollection}

**Description**

Collection de widgets

**Définition**

* `[cq:WidgetCollection] > nt:unstructured`
   * `orderable`
   * `+ * (cq:Widget) = cq:Widget copy`

### cq:Dialog {#cq-dialog}

**Description**

Boîte de dialogue

**Définition**

* `[cq:Dialog] > cq:Widget orderable`

### cq:Panel {#cq-panel}

**Description**

Panneau

**Définition**

`[cq:Panel] > cq:Widget orderable`

### cq:TabPanel {#cq-tabpanel}

**Description**

Panneau à onglets

**Définition**

* `[cq:TabPanel] > cq:Panel orderable``
   * `- activeTab (long)`

### cq:Field {#cq-field}

**Description**

Field (Champ)

**Définition**

* `[cq:Field] > cq:Widget orderable`
   * `- fieldLabel (string)`
   * `- value (string)`
   * `- ignoreData (boolean)`

## Wiki {#wiki}

### wiki:Topic {#wiki-topic}

**Description**

Rubrique Wiki

**Définition**

* `[wiki:Topic] > nt:unstructured, nt:hierarchyNode, mix:versionable, mix:lockable`
   * `+ * (wiki:Topic) version`
   * `+ wiki:attachments (nt:folder) = nt:folder version`
   * `+ wiki:properties (wiki:Properties) = wiki:Properties copy`
   * `- wiki:text (string) mandatory primary`
   * `- wiki:lastModified (date) mandatory`
   * `- wiki:lastModifiedBy (string) mandatory`
   * `- wiki:topicName`
   * `- wiki:topicTitle`
   * `- wiki:lockedBy`
   * `- wiki:logMessage (string)`
   * `- wiki:quietSave (boolean)`

### wiki:User {#wiki-user}

**Description**

Utilisateur Wiki

**Définition**

* `[wiki:User] mixin`
   * `- wiki:subscriptions (string) multiple`

### wiki:Properties {#wiki-properties}

**Description**

Propriétés Wiki

**Définition**

* `[wiki:Properties]`
   * `- wiki:isGlobal (boolean)`
   * `- * (undefined)`

## Workflow {#workflow}

### cq:Workflow {#cq-workflow}

**Description**

Représente une instance de processus.

**Définition**

* `[cq:Workflow] > nt:base, mix:referenceable`
   * `- modelId (String)`
   * `- modelVersion (String)`
   * `- startTime (Date)`
   * `- endTime (Date)`
   * `- initiator (String)`
   * `- &ast; (undefined)`
   * `- &ast; (undefined) multiple`
   * `- sling:resourceType (String) = "cq/workflow/components/instance" mandatory autocreated`
   * `+ workflowStack (nt:unstructured)`
   * `+ wait (nt:unstructured)`
   * `+ orTab (nt:unstructured)`
   * `+ data (cq:WorkflowData)`
   * `+ history (nt:unstructured)`
   * `+ metaData (nt:unstructured)`
   * `+ workItems (nt:unstructured)`

### cq:WorkItem {#cq-workitem}

**Description**

Élément de travail.

**Définition**

* `[cq:WorkItem]`
   * `- assignee (String)`
   * `- workflowId (String)`
   * `- nodeId (String)`
   * `- startTime (Date)`
   * `- endTime (Date)`
   * `- dueTime (Date)`
   * `- sling:resourceType (String) = "cq/workflow/components/workitem" mandatory autocreated`
   * `+ metaData (nt:unstructured)`

### cq:Payload {#cq-payload}

**Description**

Charge utile

**Définition**

* `[cq:Payload]`
   * `- path (Path)`
   * `- uuid (String)`
   * `- jcr:url (String)`
   * `- binary (Binary)`
   * `- javaObject (String)`
   * `- * (undefined)`
   * `- * (undefined) multiple`

### cq:WorkflowData {#cq-workflowdata}

**Description**

Données de processus

**Définition**

* `[cq:WorkflowData]`
   * `- * (undefined)`
   * `- * (undefined) multiple`
   * `+ payload (cq:Payload)`
   * `+ metaData (nt:unstructured) copy`

### cq:WorkflowModel {#cq-workflowmodel}

**Description**

Attribue automatiquement la configuration de processus. La configuration suit la structure suivante :
* `workflows`
   * `+ name1`
      * `- cq:path`
      * `- cq:workflowName`
   * `+ workflows (nt:base)`

**Définition**

* `[cq:WorkflowModel] > nt:base, mix:versionable`
   * `orderable`
   * `- title (String)`
   * `- description (String)`
   * `- sling:resourceType (String) = "cq/workflow/components/model" mandatory autocreated`
   * `+ nodes (nt:unstructured)`
      * `copy`
   * `+ transitions (nt:unstructured)`
      * `copy`
   * `+ metaData (nt:unstructured)`
      * `copy`

### cq:WorkflowNode {#cq-workflownode}

**Description**

Nœud de processus

**Définition**

* `[cq:WorkflowNode] orderable`
   * `- title (String)`
   * `- description (String)`
   * `- maxIdleTime (long)`
   * `- type (String)`
   * `- * (undefined)`
   * `- * (undefined) multiple`
   * `+ metaData (nt:unstructured)`
      * `copy`
   * `+ timeoutConfiguration (nt:unstructured)`
      * `copy`

### cq:WorkflowTransition {#cq-workflowtransition}

**Description**

Transition de processus

**Définition**

* `[cq:WorkflowTransition] orderable`
   * `- from (String)`
   * `- to (String)`
   * `- rule (String)`
   * `+ metaData (nt:unstructured)`
      * `copy`

### cq:OrTab {#cq-ortab}

**Description**

Onglet Ou

**Définition**

* `[cq:OrTab]`
   * `- workflowId (String) // not compulsory as this node will already be attached to the workflow node`
   * `- nodeId (String)`

### cq:Wait {#cq-wait}

**Description**

Attendre

**Définition**

* `[cq:Wait]`
   * `- workflowId (String) // not compulsory as this node will be already attached to the workflow node`
   * `- destNodeId (String)`
   * `- fromNodeId (String)`

### cq:WorkflowStack {#cq-workflowstack}

**Description**

Pile de processus

**Définition**

* `[cq:WorkflowStack]`
   * `- containeeInstanceId (String)`
   * `- parentInstanceId (String)`
   * `- nodeId (String)`

### cq:ProcessStack {#cq-processstack}

**Description**

Pile de processus

**Définition**

* `[cq:ProcessStack]`
   * `- workflowId (String) // not compulsory as this node will be already attached to the workflow node`
   * `- containerWorkflowModelId (String)`
   * `- containerWorkflowNodeId`
   * `- containerWorkflowEndNodeId // still needed (if name already defines that id)`

### cq:WorkflowLauncher {#cq-workflowlauncher}

**Description**

Lanceur de processus

**Définition**

* `[cq:WorkflowLauncher]`
   * `- nodetype (String)`
   * `- glob (String)`
   * `- eventType (Long)`
   * `- description (String)`
   * `- condition (String)`
   * `- workflow (String)`
   * `- * (undefined)`
   * `- * (undefined) multiple`
