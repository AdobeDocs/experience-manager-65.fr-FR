---
title: Notes de mise à jour d’ [!DNL Adobe Experience Manager] 6,5
description: '[!DNL Adobe Experience Manager]Notes relatives à  6.5 décrivant les informations de version, les nouveautés, la procédure d’installation et les listes de modifications détaillées.'
exl-id: 0288aa12-8d9d-4cec-9a91-7a4194dd280a
source-git-commit: 1cfa01544ad8bf0adafd55e696a6844a8edf1007
workflow-type: tm+mt
source-wordcount: '3894'
ht-degree: 5%

---

# [!DNL Adobe Experience Manager] 6.5 Dernières notes de mise à jour du Service Pack {#aem-service-pack-release-notes}

## Informations sur la version {#release-information}

| Produits | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Version | 6.5.11.0 |
| Type | Version du Service Pack |
| Date  | 25 novembre 2021 |
| URL de téléchargement | [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.11.zip) |

## Éléments compris dans [!DNL Adobe Experience Manager] 6.5.11.0 {#what-is-included-in-aem}

[!DNL Adobe Experience Manager] La version 6.5.11.0 comprend de nouvelles fonctionnalités, des améliorations importantes demandées par les clients, ainsi que des améliorations en termes de performances, de stabilité et de sécurité, publiées depuis la version 6.5 d’avril 2019. Le Service Pack est installé sur [!DNL Adobe Experience Manager] 6.5.

Les fonctionnalités et améliorations clés introduites dans [!DNL Adobe Experience Manager] 6.5.11.0 sont :

* Ajout de la prise en charge de champs multiples pour le type de données de texte multiligne.

* Amélioration pour sensibiliser les utilisateurs à la tâche asynchrone en cours d’exécution en arrière-plan afin de les empêcher de déclencher plusieurs opérations asynchrones sur le même chemin.

* La génération automatique du plan de site à des fins d’optimisation pour les moteurs de recherche est possible à l’aide de la variable [Package d’index SEO](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/sites-seo-index-content-1.0.0.zip). Il prend en charge les plans de site, les URL de remplacement, les balises de métadonnées de robot, etc. dans la variable [!DNL Core Components].

* Une amélioration de l’expérience utilisateur affiche le nombre de ressources présentes dans un dossier. Pour plus de 1 000 ressources dans un dossier, [!DNL Assets] affiche 1000+.

   ![Nombre de ressources dans un dossier](/help/assets/assets/browse-folder-number-of-assets.png)

* Les profils professionnels prennent en charge Adobe Asset Link.

* Vous pouvez désormais utiliser [!DNL Dynamic Media] pour configurer les paramètres généraux au lieu d’avoir à passer par l’ [!DNL Dynamic Media Classic] application de bureau. Voir [Configuration des paramètres généraux de Dynamic Media](/help/assets/dm-general-settings.md).

   ![Paramètres généraux de DM](/help/assets/assets-dm/dm-general-settings.png)

* Vous pouvez désormais utiliser [!DNL Dynamic Media] pour configurer la configuration de la publication au lieu d’avoir à passer par la [!DNL Dynamic Media Classic] application de bureau. Voir [Configuration de la publication Dynamic Media](/help/assets/dm-publish-settings.md).

   ![Paramètres de publication DM](/help/assets/assets-dm/dm-publish-setup.png)

* Le référentiel intégré (Apache Jackrabbit Oak) a été mis à niveau vers la  1.22.9.

Voici la liste des correctifs fournis dans [!DNL Experience Manager] Version 6.5.11.0.

### [!DNL Sites] {#sites-65110}

Pour accéder à la diffusion de contenu sans interface utilisateur graphique à l’aide de fragments de contenu avec GraphQL et utiliser les fonctionnalités améliorées de modèles de fragments de contenu et d’éditeur, installez le [package de définition d&#39;index](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.0.0.zip)et réindexez les définitions d’index d’AEM asynchrones suivantes :

* /oak:index/assetPrefixNodename

* /oak:index/fragments

* /oak:index/graphqlConfig


Les problèmes suivants ont été corrigés dans [!DNL Sites]:

* Le modèle de création d’un fragment de contenu n’est pas visible lors de la création d’un fragment de contenu (SITES-3365).

* Expressions régulières et [!UICONTROL Unique] les options de champ ne fonctionnent pas dans [!UICONTROL appsUrl] modèle dans l’éditeur de fragment de contenu (SITES-1823).

* Des configurations sont ajoutées dans `/apps/system` plutôt que de `/libs` lors de l’installation du service pack précédent (SITES-3203).

* Les fonctionnalités qui utilisent des fragments de contenu ne fonctionnent pas comme d’habitude lors de l’installation du Service Pack précédent (SITES-3151).

* Le tri ne fonctionne pas dans [!UICONTROL Modèles de fragment de contenu] console (SITES-2722).

* GraphiQL ne charge pas les modèles (schémas) et rencontre une erreur pour le point de terminaison JSON (SITES-2428).

* Types de champ d’énumération ajoutés à un [!UICONTROL Modèle de fragment de contenu] ne sont pas visibles dans [!UICONTROL Éditeur de modèle de fragment de contenu] (SITES-2391).

* Le type de données Balises ne prend pas en charge certains types de données (SITES-2390).

* [!UICONTROL API REST de fragment de contenu] exporte des valeurs de balise obsolètes (SITES-2386).

* La flèche dans le chemin de navigation n’est pas correctement alignée dans l’éditeur de fragments de contenu (SITES-2341).

* La recherche de références aux fragments de contenu est lente pour les jeux de données volumineux (SITES-2147).

* [!UICONTROL CopyUrl] n’est pas appropriée dans [!UICONTROL Éditeur de fragments de contenu] (SITES-2007).

* Aucun avertissement ne s’affiche lorsque le fragment de contenu est publié avec un modèle associé et que le modèle introduit des modifications de freinage (SITES-1988).

* La modification d’URL du modèle de fragment de contenu est différente pour différents cas d’utilisation de la modification des modèles de fragment de contenu (SITES-1980).

* Lors de la création de deux fragments de contenu avec le même titre à l’aide de la [!UICONTROL Nouveau fragment de contenu] , l’assistant renvoie le même chemin de fragment (SITES-1978).

* La saisie automatique ne fonctionne pas dans [!UICONTROL Modèle de fragment de contenu] facette de recherche (SITES-1976).

* Si un fragment de contenu contient une énorme hiérarchie de fragments imbriqués, la variable [!UICONTROL Éditeur de fragment de contenu] ne répond plus lors du chargement du panneau latéral (SITES-1974).

* La recherche globale dans le chemin du sélecteur de fragment ne fonctionne pas (SITES-1973).

* Les références sont mises à jour lors du déplacement d’un fragment de contenu (SITES-1897).

* L’option de création de page est manquante en mode Carte et Colonne (NPR-37549).

* Lors de la réorganisation des composants sur une page de lancement, la promotion de Launch ne conserve pas la réorganisation des composants (NPR-37539).

* L’option permettant de sélectionner tous les éléments d’une liste ne fonctionne pas sur la page de déploiement (NPR-37443).

* L’activation planifiée de plusieurs pages entraîne l’ouverture d’une nouvelle session JCR pour `wcm-workflow-service` utilisateur (NPR-37417).

* L’opération de déplacement sur les dossiers de la console Sites échoue avec un message d’erreur &quot;Échec de la récupération des informations de lancements pour l’élément sélectionné&quot; (NPR-37340).

* Lors de la génération d’une miniature pour le plan directeur et du déploiement sur des Live Copies, l’héritage pour les onglets après la miniature dans les Live Copies est rompu (NPR-37190).

* Le prédicat de filtre pour afficher la Live Copy n’affiche pas toutes les Live Copies (NPR-37126).

* L’événement de réplication ne renvoie pas la liste de toutes les pages parents et enfants qui ont été marqués pour suppression lorsque le gestionnaire d’événements de réplication est appelé sur l’auteur (NPR-37123).

* Lors de l’enregistrement d’une propriété à plusieurs valeurs à l’aide de l’éditeur en bloc, la chaîne séparée par des virgules est stockée en tant que premier élément du tableau (NPR-37089).

* Le redimensionnement de la mise en page des composants ne fonctionne pas dans la mise en page mobile (NPR-37086).

* Un nouveau noeud est incorrectement créé au niveau de la Live Copy lors de l’enregistrement des propriétés de page après l’ajout de configurations de déploiement (NPR-37084).

* L’utilisateur ne peut pas créer de Live Copies ni procéder au déploiement à l’aide des propriétés de page pour les nouveaux gabarits (SITES-3442).

* Les balises affichent les noms de balise au lieu du titre et l’option de fermeture ne supprime pas complètement les balises, car la propriété de balise ne fonctionne pas correctement lorsque l’héritage est annulé au niveau de la propriété (NPR-36831).

* L’option de désélection de tous les éléments ne fonctionne pas et l’en-tête chevauche la première ligne du tableau, de la page qui affiche une liste de Live Copies (NPR-37070).

* Dans une boîte de dialogue personnalisée utilisée dans un workflow, lors de la tentative de validation de la boîte de dialogue, Experience Manager échoue avec une erreur dans la console du navigateur (GRANITE-35049).

Les améliorations d’accessibilité suivantes sont disponibles dans [!DNL Adobe Experience Manager Sites]:

* Les lecteurs d’écran annoncent maintenant le rôle de [!UICONTROL Références du site] et [!UICONTROL Copies de langue] options (SITES-1791).

* L’ordre de focus du mode navigateur se déplace désormais de manière séquentielle sur diverses options de l’interface utilisateur (SITES-1791).

* Les lecteurs d’écran indiquent maintenant si l’élément d’arborescence sélectionné est à l’état sélectionné et annoncent également à l’utilisateur que la région d’action est affichée (SITES-2109).

* Les lecteurs d’écran indiquent maintenant quand un indicateur de chargement s’affiche lors de la sélection d’un filtre ou de la recherche d’une page (SITES-1790).

* Les lecteurs d’écran indiquent maintenant quand la variable [!UICONTROL Filtrer] ne renvoie aucun résultat de recherche dans le rail de gauche (SITES-1599).

* Lorsque vous naviguez en mode de navigation, les lecteurs d’écran indiquent le rôle de la page de contenu et l’état sélectionné d’une page lorsque la touche Entrée est enfoncée (SITES-1579).

* Les lecteurs d’écran indiquent maintenant quand [!UICONTROL Remarque : Ajouter] est sélectionnée (SITES-1573).

* Les champs de formulaire sont désormais séparés des libellés visuels des espaces réservés, de sorte que les utilisateurs de lecteurs d’écran sont correctement guidés lors de la saisie des valeurs de champ (SITES-1258).

### [!DNL Assets] {#assets-65110}

Les améliorations d’accessibilité suivantes sont disponibles dans [!DNL Assets]:

* En mode Carte dans le [!DNL Assets] référentiel, lors de l’utilisation de `Tab` pour déplacer la sélection vers le premier élément qui ouvre les actions rapides sur le focus, le lecteur d’écran annonce le nom de l’élément sélectionné.
* Dans [!DNL Dynamic Media] [!UICONTROL Éditeur de paramètres prédéfinis de la visionneuse], lorsque les couleurs de l’ombre et de la bordure ne sont pas présentes, les entrées sont désactivées à l’aide de la propriété disabled. Les utilisateurs du clavier ne sont pas en mesure de cibler l’entrée et les lecteurs d’écran n’annoncent pas l’état du contrôle comme désactivé.
* Dans [!DNL Dynamic Media], dans l’interface de création d’un profil de codage vidéo, la variable [!UICONTROL Rapport de recadrage intelligent] est étiquetée pour l’accessibilité, de sorte que les lecteurs d’écran l’annoncent correctement.

* Vous pouvez désormais accéder aux commandes de liste de référence dans [!DNL Experience Manager Assets] à l&#39;aide du clavier.

Les problèmes suivants ont été corrigés dans [!DNL Assets]:

* Lorsqu’un utilisateur du groupe de contributeurs accède au référentiel de ressources DAM, une `POST` est déclenchée pour créer une collection. Ceci `POST` la requête échoue et reflète une erreur dans les journaux (NPR-37171).

* Lors de la création d’une Live Copy du plan directeur ayant une structure de dossiers imbriquée, les propriétés modifiées du dossier source ne sont pas mises à jour dans le dossier Live Copy (NPR-37449).

* Lors de la sélection de plusieurs ressources et de la modification des valeurs de champ de métadonnées, l’enregistrement des ressources ne conserve pas les valeurs. En outre, les modifications apportées aux métadonnées ne sont pas appliquées (NPR-37341).

* Lors de la sélection de plusieurs ressources et de la modification des propriétés, les valeurs des propriétés personnalisées (listes déroulantes) sont remplacées par les valeurs par défaut (NPR-36437).

* Un rendu de PDF incorrect est généré pour la brochure, le prospectus et les modèles d’InDesign (NPR-36433).

* Enregistrement d’une [!DNL Adobe Target] activité avec [!DNL Experience Manager] le mode de ciblage échoue si un événement [!DNL Adobe Analytics] la mesure du rapport est référencée (NPR-37167).

* Lorsqu’un utilisateur qui dispose d’un courrier électronique avec un nom de domaine mixte extrait une ressource, la ressource n’est pas visible dans les ressources extraites de l’utilisateur dans [!DNL Asset Link] (CQ-4329266).

<!-- Add 
* [!DNL Adobe Asset Link] is not able to access the digital assets even when the [!DNL Creative Cloud] and [!DNL Experience Management] entitlements are provided by two different organizations. -->

* L’ajout d’une vidéo avec des métadonnées personnalisées générées lors du téléchargement vers une page affiche une erreur concernant l’espace de noms inconnu, même si l’espace de noms est enregistré (CQ-4331471).

* Dans [!DNL Assets], si [!DNL Launcher] est désactivée, l’écriture différée des métadonnées ne fonctionne pas lorsqu’elle est déclenchée manuellement (CQ-4329082).

### [!DNL Dynamic Media] {#dynamic-media-65110}

Les correctifs suivants sont disponibles dans [!DNL Dynamic Media]:

* La ressource n’est pas mise à jour dans [!DNL Dynamic Media] lors de la restauration d’une version de ressource dans [!DNL Experience Manager] (NPR-37421).

* Les catalogues électroniques ne sont pas publiés sur les fichiers de PDF de publication (CQ-4329886).

* Les ressources 3D ne se chargent pas lorsque la page publiée est ouverte au cas où le composant utilise un paramètre prédéfini prêt à l’emploi (CQ-4329205).

* Problèmes liés au traitement des ressources du PDF dans le cas de référentiels volumineux (CQ-4328711).

* L’erreur de traitement du PDF ne se propage pas vers [!DNL Experience Manager] en cas d’échec à [!DNL Scene7] (CQ-4331145).

* Les utilisateurs ne peuvent pas afficher les propriétés de métadonnées par défaut d’une ressource .MOV (CQ-4332546).

* Impossible de charger les fichiers vidéo .MXF dans [!DNL Dynamic Media] using [!DNL Experience Manager] (CQ-4329709).

* Problèmes de téléchargement lors de la configuration de la racine d’entreprise personnalisée (CQ-4332800).

* Dans [!DNL Experience Manager] configurations contenant un lanceur personnalisé avec `ActivationModel` au fur et à mesure que le workflow se bloque, le Experience Manager se bloque en raison de problèmes de mémoire lors du chargement des fichiers du PDF. (CQ-4330512).

* Problèmes de performance dans `DamEventRecorder` (CQ-4334072).

* Si un hyperlien de vidéo Shoppable (Linked-URL) contient des caractères spéciaux, l’URL cible est codée par la visionneuse et donne une page de produit incorrecte (CQ-4331639).

* Dans une page de profil vidéo, les options de la barre d’outils disparaissent si l’utilisateur sélectionne un profil vidéo immédiatement au chargement de la page (CQ-4308521).

* Échec du traitement des ressources DM en raison d’écritures simultanées JCR (CQ-4333489).

* L’accès à la page Profils vidéo échoue si la racine du profil vidéo de l’utilisateur comporte des stratégies d’accès personnalisées définies sur le noeud racine des profils vidéo (CQ-4332941).

* Dans une image agrandie, l’utilisation des touches de raccourci (&#39;+&#39;, &#39;-&#39;) ou la touche &quot;Échap&quot; piège le focus du lecteur d’écran (CQ-4290719).

* Lorsqu’un utilisateur clique sur la touche de raccourci du mode de formulaire (’F’), le lecteur d’écran ne mappe pas le libellé de la variable [!UICONTROL Taille d’incorporation] du menu [!UICONTROL Obtenir une incorporation] Boîte de dialogue de code (CQ-4290929).

* Lors de l’utilisation de la navigation au clavier pour ouvrir la fenêtre contextuelle de lien d’email, les suggestions d’erreur affichées dans l’interface utilisateur pour les champs &quot;A&quot; et &quot;De&quot; ne sont pas descriptives (CQ-4290930).

* Lorsque vous accédez à la boîte de dialogue de lien d’e-mail, le lecteur d’écran ne décrit pas les informations d’étiquette des champs d’édition nouvellement ajoutés à l’aide de la flèche vers le bas et de la touche de raccourci du mode de formulaire (’F’) (CQ-4290934).

* Lorsque vous accédez à la boîte de dialogue du lien du courrier électronique, le lecteur d’écran ne reflète pas l’astérisque visuel (*) associé aux champs obligatoires &quot;A&quot; et &quot;De&quot; (CQ-4290935).

* Les utilisateurs ne sont pas en mesure d’identifier le repère et la région à l’aide des raccourcis clavier (’D’, ’R’) (CQ-4312118).

<!-- Anuj to check if this section is required or not. We have an enh. in CIF area that is mentioned. It is added above and not part of this bug fix section.
-->

### Commerce {#commerce-65110}

* Lors de l’utilisation de la variable [!UICONTROL Publier ultérieurement] , l’interface utilisateur ne reflète pas l’état comme [!UICONTROL Publication en attente] (CQ-4334229).

* L’annulation de la publication d’un dossier n’annule pas complètement la publication des produits de ce dossier. Les produits sont supprimés de l’éditeur, mais existent toujours dans l’instance d’auteur (CQ-4332731).

### Plateforme {#platform-65110}

* Lorsqu’un utilisateur clique sur l’icône de réorganisation d’une option à plusieurs champs, la barre de défilement disparaît de l’interface utilisateur (CQ-4331100).

* Après la mise à niveau, lorsqu’un utilisateur ouvre le composant de conteneur de connexion au travail, l’en-tête de la boîte de dialogue n’est pas visible dans l’interface utilisateur (CQ-4316173).

### Intégrations {#integrations-65110}

* Enregistrement d’une [!DNL Adobe Target] activité avec [!DNL Experience Manager] le mode de ciblage échoue si un événement [!DNL Adobe Analytics] la mesure du rapport est référencée (NPR-37167).

### Projets {#projects-65110}

* Lors de la mise à niveau à partir de [!DNL Experience Manager] 6.5.8.0 à la version 6.5.9.0, l’installation remplace les propriétés sur `/content/dam/projects`. Il réinitialise le schéma de métadonnées et les propriétés attribués au dossier sur la valeur par défaut (NPR-37124).

### Interface utilisateur {#user-interface-65110}

* L’icône de dossier représentant le modèle est incorrecte (NPR-37176).

* Lorsqu’un utilisateur effectue une recherche ou navigue à l’aide du navigateur de champ de chemin d’accès, des noeuds incorrects sont affichés (NPR-37175).

* Sur l’instance de publication, les requêtes entrantes sont bloquées pendant plusieurs minutes (NPR-37169).

* Lors de l’ajout d’une propriété multifield dans une boîte de dialogue pour un workflow personnalisé, la boîte de dialogue ne se poursuit pas et l’utilisateur ne peut pas fermer la boîte de dialogue (NPR-37075).

### Projets de traduction {#translation-65110}

* La promotion automatique du lancement de traduction échoue avec une exception (NPR-37528).

* La traduction du fragment d’expérience ne met pas à jour les références de la copie de langue de l’URL (NPR-37522).

* Lorsqu’un fragment d’expérience est créé dans un chemin qui ne correspond pas au chemin d’accès de la structure racine de langue, l’ajout de cette page à un projet de traduction reflète un message d’erreur vide (NPR-37425).

* Lorsqu’une page (en anglais) contenant des fragments d’expérience est modifiée et envoyée pour traduction, les fragments d’expérience déjà traduits sont écrasés par le contenu anglais (NPR-37283).

* Le filtre du fournisseur de traduction ne fonctionne pas correctement (NPR-37186).

* Les composants Fragment d’expérience et Accordéon ne sont pas traduits d’usine pour l’exemple de contenu de site (NPR-37170).

* Après la mise à niveau vers [!DNL Experience Manager] 6.5.9.0, l’ajout d’une page au projet de traduction reflète un message d’erreur vide (NPR-37105).

* Lors de l’ajout de pages dans launch, les pages de traduction portant des noms similaires ne sont pas incluses dans le projet (NPR-37082).

* Lors de l’export d’un dictionnaire de formulaires sous la forme d’un fichier .xliff à l’aide de l’interface du traducteur, l’ordre des champs du fichier exporté est incorrect (NPR-37048).

* Lors du déploiement d’une page parente à partir d’un projet de traduction, les pages enfants spécifiques à une langue sont supprimées (NPR-36998).

* Lors de la création d’un projet de traduction, le référencement cyclique des pages déclenche un lancement, ce qui entraîne une erreur (CQ-4332982).

* Le lien du fragment d’expérience dans le fragment d’expérience et la page traduits contient la référence de lancement (NPR-37649).

### Sling {#sling-65110}

* Lors du chargement d’un nouveau package, l’alias de mémoire dans la carte MapEntries est supprimé (NPR-37067).

### Workflow {#workflow-65110}

* `Deactivate` dans `InboxOmniSearchHandler` affiche une exception de pointeur null (NPR-37533).

### [!DNL Communities] {#communities-65110}

* L’utilisateur ne peut pas ajouter de commentaire à la page, la variable `Post` échoue avec le code d’erreur 500 (NPR-37156).

* Lors du déploiement de l’application, une exception de segment introuvable est observée en raison de la session longue de SyncManager (NPR-37351).

* L&#39;utilisateur n&#39;est pas en mesure de voir les réponses de fil dans le post de discussion du forum (NPR-37083).




<!--
Need to verify with Engineering, the status is currently showing as Resolved
-->


<!--
### [!DNL Brand Portal] {#brandportal-65110}

*

-->

### [!DNL Forms] {#forms-65110}


>[!NOTE]
>
>* [!DNL Experience Manager Forms] publie les packages de modules complémentaires une semaine après la date de publication prévue du Service Pack [!DNL Experience Manager].


**Formulaires adaptatifs**

* Accessibilité : lorsque vous définissez la variable `Wizard` mise en page d’un panneau dans un formulaire adaptatif, les boutons de navigation n’ont pas de libellés Aria ni de rôle (NPR-37613).

* Les validations sur un champ date dans un formulaire adaptatif ne fonctionnent pas, comme prévu (NPR-37556).

* Lorsque le texte du libellé des composants Case à cocher et Bouton radio est long, il ne convient pas (NPR-37294).

* Lorsque vous appliquez des modifications de style au message de remerciement du composant Conteneur AEM Forms, les modifications ne sont pas répliquées dans le formulaire adaptatif source (NPR-37284).

* Différences dans la valeur de la variable `Switch` sur l’interface utilisateur et dans le serveur principal (NPR-37268).

* Lorsque vous utilisez les touches du clavier pour accéder au `Submit` et appuyez sur la touche `Enter` clé, vous pouvez envoyer le formulaire adaptatif plusieurs fois (CQ-4333993).

* L’opération Supprimer du composant Pièce jointe ne fonctionne pas comme prévu (NPR-37376).

* Lorsqu’un libellé d’un champ dépasse 1 000 caractères dans un formulaire adaptatif qui se traduit dans différentes langues, le dictionnaire ne parvient pas à récupérer la traduction du libellé (CQ-4329290).

**Services de document**

* Une erreur s’affiche lors de l’utilisation du service Assembler (NPR-37606) :

   ```TXT
     500 Internal Server Error
   ```

* Lorsque les pièces jointes du document sont transmises au service Assembler, l’exception suivante s’affiche (NPR-37582) :

   ```TXT
     com.adobe.livecycle.assembler.client.ProcessingException: ⁪: Failed to execute the DDX
   ```

* Parenthèse fermante manquante dans les données après la conversion d’un document de PDF en document de PDF PDF-A/1B (NPR-37608).

**Formulaires HTML5**

* Lorsque vous installez AEM 6.5.10.0, l’aperçu du HTML d’un formulaire XDP ne fonctionne pas (NPR-37503, CQ-4331926).

* Problèmes de chevauchement de texte lors de la migration des PDF forms vers les formulaires HTML 5 dans différentes langues (NPR-37173).

**Lettres**

* Lorsque vous envoyez une lettre et la rouvrez en mode HTML, la position des fragments de document texte ne reste pas la même (NPR-37307).

**Processus des formulaires**

* Dans le cas d’un workflow de conteneur incorporé, vous recevez plusieurs emails de fin de workflow même après avoir sélectionné la variable `Notify on Complete of Container Workflow` (NPR-37280).

**Foundation JEE**

* Après avoir installé AEM 6.5 Forms Service Pack 9, les URL du référentiel CRX ne sont plus disponibles (NPR-37592).

**Problèmes résolus dans AEM Forms 6.5.11.1**

>[!NOTE]
>
>Si vous n’avez pas effectué la mise à niveau vers AEM 6.5.11.0 Forms, installez directement le module complémentaire AEM Forms 6.5.11.1. Si vous avez installé AEM 6.5.11.0 Forms, Adobe recommande d’effectuer la mise à niveau vers AEM 6.5.11.1 Forms.

* Les actions Envoyer, Envoyer un courrier électronique et Appeler un workflow AEM ne fonctionnent plus après l’installation du module complémentaire Forms 6.5.11.0.
* L’opération CreatePDF cesse de convertir des documents Microsoft Word en documents PDF après l’installation du module complémentaire Forms 6.5.11.0.
* (JEE uniquement) Vulnérabilités de sécurité critiques (CVE-2021-44228 et CVE-2021-45046) signalées pour Apache Log4j2.
* (JEE uniquement) Le correctif Assembler DSC dans la version 6.5.11.0 contient des métadonnées incorrectes telles que la version des spécifications et la version impl.


Pour plus d’informations sur les mises à jour de sécurité, voir [[!DNL Experience Manager] page bulletins de sécurité](https://helpx.adobe.com/security/products/experience-manager.html).

## Installation de la version 6.5.11.0 {#install}

**Configuration des exigences et informations supplémentaires**

* Experience Manager 6.5.11.0 nécessite Experience Manager 6.5. Voir [documentation de mise à niveau](/help/sites-deploying/upgrade.md) pour obtenir des instructions détaillées.
* Le téléchargement du Service Pack est disponible sur Adobe [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
* Sur un déploiement avec MongoDB et plusieurs instances, installez Experience Manager 6.5.11.0 sur l’une des instances d’auteur à l’aide du gestionnaire de modules.

>[!NOTE]
>
>Adobe ne recommande pas de supprimer ou de désinstaller le [!DNL Adobe Experience Manager] Package 6.5.11.0.

### Installation du Service Pack {#install-service-pack}

Pour installer le Service Pack sur un [!DNL Adobe Experience Manager] 6.5, procédez comme suit :

1. Redémarrez l’instance avant l’installation si l’instance est en mode de mise à jour (lorsque l’instance a été mise à jour à partir d’une version antérieure). Adobe recommande un redémarrage si le temps de disponibilité actuel d’une instance est élevé.

1. Avant l’installation, prenez un instantané ou une nouvelle sauvegarde de votre [!DNL Experience Manager] instance.

1. Téléchargez le Service Pack à partir de [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.11.zip).

1. Ouvrez Package Manager et cliquez sur **[!UICONTROL Télécharger le package]** pour télécharger le package. Pour en savoir plus, voir [Gestionnaire de modules](/help/sites-administering/package-manager.md).

1. Sélectionnez le package et cliquez sur **[!UICONTROL Installer]**.

1. Pour mettre à jour le connecteur S3, arrêtez l’instance après l’installation du Service Pack, remplacez le connecteur existant par un nouveau fichier binaire fourni dans le dossier d’installation, puis redémarrez l’instance. Voir [Entrepôt de données Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>La boîte de dialogue de l’interface utilisateur de Package Manager se ferme parfois pendant l’installation du Service Pack. Adobe recommande d’attendre que les journaux d’erreurs se stabilisent avant d’accéder au déploiement. Attendez les logs spécifiques liés à la désinstallation du lot de mise à jour avant de vous assurer que les installations sont réussies. En règle générale, ce problème se produit dans [!DNL Safari] mais peut se produire par intermittence sur n’importe quel navigateur.

**Installation automatique**

Il existe deux manières d’installer automatiquement [!DNL Experience Manager] 6.5.11.0 sur une instance de travail :

A. Placez le package dans `../crx-quickstart/install` lorsque le serveur est disponible en ligne. Le package est automatiquement installé.

B. Utilisez la variable [API HTTP à partir de Package Manager](/help/sites-administering/package-manager.md#package-share). Utilisation `cmd=install&recursive=true` afin que les modules imbriqués soient installés.

>[!NOTE]
>
>Adobe Experience Manager 6.5.11.0 ne prend pas en charge l’installation de Bootstrap.

**Validation de l’installation**

1. la page d’informations sur les produits (`/system/console/productinfo`) affiche la chaîne de version mise à jour. `Adobe Experience Manager (6.5.11.0)` under [!UICONTROL Produits installés].

1. Tous les lots OSGi sont : **[!UICONTROL PRINCIPAL]** ou **[!UICONTROL FRAGMENT]** dans la console OSGi (Utiliser la console web : `/system/console/bundles`).

1. Le lot OSGi `org.apache.jackrabbit.oak-core` est version 1.22.3 ou ultérieure (Utiliser la console web : `/system/console/bundles`).

Pour connaître les plates-formes certifiées pour travailler avec cette version, voir [exigences techniques](/help/sites-deploying/technical-requirements.md).

<!-- 

### Install Adobe Experience Manager Forms add-on package {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Skip if you are not using Experience Manager Forms. Fixes in Experience Manager Forms are delivered through a separate add-on package a week after the scheduled [!DNL Experience Manager] Service Pack release.

1. Ensure that you have installed the Adobe Experience Manager Service Pack.
1. Download the corresponding Forms add-on package listed at [AEM Forms releases](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates) for your operating system.
1. Install the Forms add-on package as described in [Installing AEM Forms add-on packages](/help/forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

>[!NOTE]
>
>Experience Manager 6.5.10.0 includes a new version of [AEM Forms Compatibility Package](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#aem-65-forms-releases). If you are using an older version of AEM Forms Compatibility Package and updating to Experience Manager 6.5.10.0, install the latest version of the package post installation of Forms Add-On Package.

### Install Adobe Experience Manager Forms on JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Skip if you are not using AEM Forms on JEE. Fixes in Adobe Experience Manager Forms on JEE are delivered through a separate installer.

For information about installing the cumulative installer for Experience Manager Forms on JEE and post-deployment configuration, see the [release notes](jee-patch-installer-65.md).

>[!NOTE]
>
>After installing the cumulative installer for Experience Manager Forms on JEE, install the latest Forms add-on package, delete the Forms add-on package from the `crx-repository\install` folder, and restart the server.

-->

### UberJar {#uber-jar}

UberJar pour Experience Manager 6.5.11.0 est disponible dans la section [Référentiel Maven Central](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.11/).

Pour utiliser UberJar dans un projet Maven, voir [utilisation d’UberJar](/help/sites-developing/ht-projects-maven.md) et incluez la dépendance suivante dans le POM de votre projet :

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.11</version>
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
| Intégrations | Le **[!UICONTROL Accord préalable des services cloud AEM]** est obsolète, car la variable [!DNL Experience Manager] et [!DNL Adobe Target] L’intégration est mise à jour dans Experience Manager 6.5. L’intégration prend en charge l’API Adobe Target Standard. L’API utilise l’authentification via Adobe IMS et [!DNL Adobe I/O] et prend en charge le rôle croissant d’Adobe Launch pour l’instrumenter [!DNL Experience Manager] pour les analyses et la personnalisation, l’assistant de souscription n’a aucune utilité sur le plan fonctionnel. | Configuration des connexions système, de l’authentification Adobe IMS et [!DNL Adobe I/O] intégrations via les [!DNL Experience Manager] services cloud. |
| Connecteurs | Adobe JCR Connector for Microsoft® SharePoint 2010 et Microsoft® SharePoint 2013 est obsolète pour Experience Manager 6.5. | N/A |

## Problèmes connus {#known-issues}

* Lorsque vous installez AEM 6.5 Service Pack 11 et essayez de télécharger le fichier ZIP d’état, Experience Manager télécharge un fichier corrompu. Télécharger et installer [Package d’index SEO AEM Sites](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/sites-seo-index-content-1.0.0.zip) sur votre instance AEM avant de télécharger le fichier ZIP pour résoudre le problème.

* As [!DNL Microsoft Windows Server 2019] ne prend pas en charge [!DNL MySQL 5.7] et [!DNL JBoss EAP 7.1], [!DNL Microsoft Windows Server 2019] ne prend pas en charge les installations clé en main pour [!DNL AEM Forms 6.5.10.0].

* Si vous effectuez une mise à niveau de votre [!DNL Experience Manager] de la version 6.5 à la version 6.5.10.0, vous pouvez afficher `RRD4JReporter` exceptions dans la variable `error.log` fichier . Pour résoudre le problème, redémarrez l’instance.

* Si vous installez [!DNL Experience Manager] 6.5 Service Pack 10 ou un Service Pack précédent sur [!DNL Experience Manager] 6.5, la copie d’exécution du modèle de workflow personnalisé de vos ressources (créé dans `/var/workflow/models/dam`) est supprimé.
Pour récupérer votre copie d’exécution, Adobe recommande de synchroniser la copie d’heure de conception du modèle de workflow personnalisé avec sa copie d’exécution à l’aide de l’API HTTP :
   `<designModelPath>/jcr:content.generate.json`.

* Les utilisateurs peuvent renommer un dossier dans une hiérarchie de [!DNL Assets] et publier un dossier imbriqué dans [!DNL Brand Portal]. Toutefois, le titre du dossier n’est pas mis à jour dans [!DNL Brand Portal] jusqu’à ce que le dossier racine soit republié.

* Lorsqu’un utilisateur choisit de configurer un champ pour la première fois dans un formulaire adaptatif, l’option permettant d’enregistrer une configuration ne s’affiche pas dans l’explorateur de propriétés. Sélectionner pour configurer un autre champ du formulaire adaptatif dans le même éditeur résout le problème.

* Les erreurs et messages d’avertissement suivants peuvent s’afficher lors de l’installation de Experience Manager 6.5.x.x :
   * &quot;Lorsque l’intégration d’Adobe Target est configurée dans Experience Manager à l’aide de l’API Target Standard (authentification IMS), l’exportation de fragments d’expérience vers Target entraîne la création de types d’offres incorrects. Au lieu du type « Fragment d’expérience » / source « Adobe Experience Manager », Target crée plusieurs offres avec le type « HTML » / source « Adobe Target Classic ».
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: Aucune fenêtre de maintenance n’a été trouvée sur granite/operations/maintenance.
   * La validation côté serveur du formulaire adaptatif échoue lorsque des fonctions d’agrégat telles que SUM, MAX et MIN sont utilisées (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Aucune fenêtre de maintenance n’a été trouvée sur granite/operations/maintenance.
   * La zone réactive d’une image interactive Dynamic Media n’est pas visible lors de la prévisualisation de la ressource via la visionneuse de bannières Shoppable.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : Délai d’attente avant que la modification du reg ne soit terminée sans enregistrement.

* Lorsque vous tentez de déplacer/supprimer/publier des fragments de contenu ou des sites/pages, un problème se produit lorsque les références aux fragments de contenu sont récupérées, car la requête en arrière-plan échoue ; en d’autres termes, la fonctionnalité ne fonctionnera pas.
Pour garantir le bon fonctionnement, vous devez ajouter les propriétés suivantes au noeud de définition d’index. `/oak:index/damAssetLucene` (aucune réindexation n’est requise) :

   ```xml
   "tags": [
       "visualSimilaritySearch"
     ]
   "refresh": true
   ```

## Lots OSGi et packages de contenu inclus {#osgi-bundles-and-content-packages-included}

Les documents texte suivants répertorient les lots OSGi et les packages de contenu inclus dans [!DNL Experience Manager] 6.5.11.0 :

* [Liste des lots OSGi inclus dans Experience Manager 6.5.11.0](assets/65110_bundles.txt)

* [Liste des packages de contenu inclus dans Experience Manager 6.5.11.0](assets/65110_packages.txt)

## Sites web à accès limité {#restricted-sites}

Ces sites web ne sont disponibles que pour les clients. Si vous êtes client et avez besoin d’un accès, contactez votre responsable de compte Adobe.

* [Téléchargement du produit à l’adresse licensing.adobe.com](https://licensing.adobe.com/)
* Voir [Comment contacter le service clientèle d’Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

## Versions clés depuis [!DNL Adobe Experience Manager] 6.5 SP10{#key-releases-since-last-sp}

Entre le 26 août 2021 et le 25 novembre 2021, Adobe a publié les éléments suivants, en plus des Service Packs :

* [!DNL Adobe Experience Manager] as a Cloud Service [2021.9.0](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/2021/release-notes-2021-9-0.html) et [2021.10.0](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=fr).

* [[!DNL Experience Manager] application de bureau 2.1 (2.1.3.4)](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html?lang=fr).

* [Experience Manager Screens : Feature Pack 202109](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/release-notes/release-notes-fp-202109.html?lang=fr)


>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] page produit](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] Documentation 6.5](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=fr)
>* [Abonnement aux mises à jour de produits prioritaires d’Adobe](https://www.adobe.com/subscription/priority-product-update.html)

