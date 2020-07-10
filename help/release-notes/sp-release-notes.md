---
title: Notes de mise à jour de Adobe Experience Manager 6.5 Service Pack
description: Notes de mise à jour spécifiques à Adobe Experience Manager 6.5 Service Pack 5.
docset: aem65
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 6686c10f1af24cc4fbdcf6d4e8b07f7dc0e2a8bb
workflow-type: tm+mt
source-wordcount: '4529'
ht-degree: 7%

---


# Notes de mise à jour de Adobe Experience Manager 6.5 Service Pack {#aem-service-pack-release-notes}

## Informations sur la version {#release-information}

| Produits | Adobe Experience Manager 6.5 |
| -------- | ---------------------------- |
| Version | 6.5.5.0 |
| Type | Version du Service Pack |
| Date  | 4 juin 2020 |
| URL de téléchargement | [Package Share](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/AEM-6.5.5.0-Service-Pack), distribution [de logiciels](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.5.zip) |

## Éléments inclus dans l’Adobe Experience Manager 6.5.5.0 {#what-s-included-in-aem}

L’Adobe Experience Manager 6.5.5.0 est une mise à jour importante qui comprend de nouvelles fonctionnalités, des améliorations client clés et des améliorations de performances, de stabilité et de sécurité, publiées depuis la version 6.5 d’ **avril 2019**. Il peut être installé sur l&#39;Adobe Experience Manager 6.5.

Voici quelques-unes des principales fonctionnalités et améliorations introduites dans l’Adobe Experience Manager 6.5.5.0 :

* Personnalisez les noms des colonnes qui s&#39;affichent dans la boîte de réception des Adobes Experience Manager.

* Amélioration de l’accessibilité dans diverses zones de la Gestion de contenu Web Experience Manager (WCM), telles que l’éditeur de page, les composants principaux, RTE et l’interface utilisateur d’administration.

* Enregistrez une [!DNL Interactive Communication] version préliminaire.

* Prise en charge [!DNL Oracle WebLogic 12] de Experience Manager Forms sur JEE.

* Amélioration de la gestion des exceptions dans le flux de l’interface [!DNL Adobe Experience Manager Assets] utilisateur.

* Pour obtenir l’URL de publication pour Dynamic Media Scene7, une nouvelle méthode `getRemoteAssetPublishURL` est ajoutée à `com.day.cq.dam.api.s7dam.scene7.ImageUrlApi` l’interface.

* [Améliorations](#assets-6550) de l&#39;accessibilité en [!DNL Adobe Experience Manager Assets] conformité avec les directives WCAG (Web Content Accessibility Guidelines).

* Suppression de l’intégration Package Share de l’Adobe Experience Manager.

* Le référentiel intégré (Apache Jackrabbit Oak) a été mis à niveau vers la version 1.22.3.

Pour une liste complète des fonctionnalités, des points saillants, des fonctionnalités clés introduites dans Experience Manager 6.5 Service Pack 5, voir [Nouveautés de l’Adobe Experience Manager 6.5 Service Pack 5](new-features-latest-service-pack.md) .

Voici la liste des correctifs fournis dans la [!DNL Experience Manager] version 6.5.5.0.

### [!DNL Sites] {#sites-6550}

* Les sites Experience Manager offrent la possibilité de publier ou d’annuler la publication d’une page à partir de son alias. L&#39;option ne fonctionne pas (NPR-33415).
* Lorsqu’un conteneur de mise en page est supprimé d’un modèle contenant plusieurs modèles, le rendu du modèle n’est pas correct (NPR-33347).
* Lorsqu&#39;une page Sites Experience Manager fait partie d&#39;un vaste ensemble de contenus comportant plusieurs copies en direct, la prévisualisation d&#39;historique des versions de page ne se charge pas (NPR-33311).
* Lorsque vous utilisez la commande Déplacer pour renommer une page Sites Experience Manager, le titre de la page n&#39;est pas mis à jour (NPR-33264).
* Lorsque vous déplacez des pages à travers la vue des colonnes, les colonnes disparaissent (NPR-33216).
* Lorsque le nom d&#39;un composant local d&#39;une copie de langue est identique au nom d&#39;un composant du plan et que le composant est déployé à partir du plan, le terme `_msm_moved` n&#39;est pas ajouté au nom du composant local (NPR-33208).
* La servlet Redirection de page ajoute .html à une URL de sites Experience Manager où ResourceType n&#39;est pas `cq:Page` (NPR-33176).
* Lorsque vous collez une sous-arborescence, vous n’avez pas la possibilité de décider si les sous-pages correspondantes doivent être collées ou non (NPR-33149).
* Le nombre de résultats dans les utilisations réelles d&#39;un composant est limité au nombre 49 (NPR-33058).
* Lorsque vous basez un fragment de contenu sur un schéma et qu’il contient une zone de texte obligatoire ou un champ de chemin, l’enregistrement du fragment de contenu échoue (NPR-33007).
* Lorsque vous créez un composant personnalisé à l’aide du composant Fragment d’expérience par défaut et que vous l’utilisez dans les pages Sites du Experience Manager, le Experience Manager n’affiche pas les références (utilisation) du composant personnalisé (NPR-32852).
* Lorsque vous renommez un dossier avec un grand nombre de références, de nombreuses références au dossier ne sont pas mises à jour (NPR-32765).
* Lorsque vous activez l’option d’édition source, elle devient disponible pour les options d’affichage plein écran en ligne, mais reste absente pour les options de boîte de dialogue d’édition et d’affichage plein écran de l’éditeur de texte enrichi (NPR-32763).
* Si vous disposez d’un champ à plusieurs champs et qu’il contient un champ obligatoire (tel qu’une liste déroulante ou un champ de chemin) dans les propriétés de page d’un plan directeur, lorsqu’une page contenant un tel champ à plusieurs champs est déployée, les propriétés de page de la copie dynamique ne sont pas enregistrées (NPR-32751).
* Les lecteurs d’écran ne peuvent pas utiliser la structure d’en-tête pour parcourir une page. En outre, l&#39;onglet Composants a un libellé incorrect (NPR-32648).
* Lors des débuts de pagination, le sélecteur de fragments d’expérience ne charge pas tous les éléments (NPR-32605).
* Les autorisations d’auteur pour lire, modifier, créer et supprimer des copies en direct sont révoquées. Chaque auteur devait fournir explicitement des autorisations de lecture et de modification pour déplacer des pages dans un plan directeur (NPR-32550).
* Les auteurs de contenu ne parviennent pas à créer le lancement d’une page qui est intégrée à Adobe Analytics (NPR-32548).
* Lorsqu&#39;un utilisateur reprend l&#39;héritage avec la synchronisation, la copie dynamique de la page parente ne se synchronise pas avec le plan et affiche un état incorrect (NPR-32500).
* Le chargement de la page de l&#39;éditeur de sites Experience Manager prend plus de 15 secondes (NPR-32413).
* Certains champs n&#39;affichent pas l&#39;option Annuler l&#39;héritage (NPR-32362).
* Lorsque vous sélectionnez un chemin pour un composant Fragment d’expérience et cochez la case Ouvrir la boîte de dialogue de sélection, vous n’accédez pas au chemin sélectionné dans le navigateur de chemins (NPR-32308).
* Lorsque vous effectuez une mise à niveau de Experience Manager 6.2 vers Experience Manager 6.5, le composant Parsys des modèles statiques ne s’affiche pas correctement. La hauteur du composant Parsys est définie sur 0 et les composants qu&#39;il contient ne sont pas visibles (NPR-33663).
* Lorsqu’un utilisateur copie et colle un Conteneur de mise en page sur la même page, les composants d’un Conteneur de mise en page ne s’affichent pas (NPR-33648).
* La vérification de l&#39;intégrité du Dispatcher affiche un message d&#39; `Invalid cookie header` avertissement dans les fichiers journaux (NPR-33629).

### [!DNL Assets] {#assets-6550}

**Améliorations de l’accessibilité dans les ressources des Experience Manager**

* Il est désormais possible d’activer l’option [!UICONTROL Commentaires] au clavier et d’activer l’option de clic pour [!UICONTROL Créer] des commentaires de version sous [!UICONTROL Créer une nouvelle version] dans le panneau de ressources [!UICONTROL Chronologie (NPR-33424).]

* Il est désormais possible d’accéder à l’option Paramètres [!UICONTROL de] Vue pour les ressources et de modifier les paramètres dans la boîte de dialogue Paramètres [!UICONTROL de] Vue à l’aide des touches du clavier (NPR-33420).

* La fenêtre contextuelle de la zone de liste de la zone combinée (dans divers champs sur différentes pages) affiche désormais les entrées en tant que liste d’options pouvant être annoncées par les lecteurs d’écran (NPR-33516).

* Les lecteurs d’écran annoncent maintenant la fonctionnalité de tri des en-têtes pouvant être triés (dans la vue de liste, la vue de [!UICONTROL chronologie] et la page [!UICONTROL Gérer la publication] ) et les commandes de tri des en-têtes de colonne sont accessibles à l’aide du clavier (NPR-32979).

* Les éléments cliquables, tels que les cartes de commentaires, les mises à jour de version, les zones de liste modifiable et les icônes de menus chevron, peuvent désormais être ciblés et interactifs à l’aide d’un clavier (NPR-33514).

* La fonctionnalité (ou l’objectif de l’action) des icônes d’informations (pour l’utilisation, les impressions et les clics) sur la Vue  Insights est maintenant correctement annoncée par les lecteurs d’écran (NPR-33513).

* Read-only form fields (for example disabled fields on [!UICONTROL Basic tab] of asset [!UICONTROL Properties]) are now focusable using keyboard (NPR-33493, CQ-4273031).

* Les étiquettes des différents champs d&#39;entrée sont maintenant des étiquettes permanentes (donc accessibles) et pas seulement des étiquettes d&#39;espace réservé, qui ont disparu au moment de la saisie du texte (NPR-33475).

* Différents niveaux d’en-tête (tels que les titres de page et les en-têtes de section) sont maintenant perçus comme des en-têtes avec des niveaux différents pour les utilisateurs de lecteurs d’écran (NPR-33471).

* Les éléments interactifs de l’interface utilisateur, tels que les liens et les options (sur l’en-tête et les options de zoom de la page des ressources, la navigation dans les dossiers), sont désormais accessibles à l’aide d’un clavier (NPR-33468, CQ-4271412).

* Les indicateurs de progression [!UICONTROL Options], [!UICONTROL Portée]et [!UICONTROL Workflows] de la page [!UICONTROL Gérer la publication sont désormais correctement lus par les lecteurs d’écran comme des indicateurs de progression, plutôt que comme des onglets (NPR-33416).]

* La couleur des icônes d’évaluation des étoiles (par exemple dans la section [!UICONTROL Notation] de l’onglet [!UICONTROL Avancé] dans [!UICONTROL Propriétés] de la ressource ou dans la vue de la carte) est modifiée pour que le contraste approprié soit visible pour les utilisateurs ayant une vision limitée et sans perception de couleur (NPR-33414).

* La flèche pointant vers le haut en regard du champ [!UICONTROL Commentaire] sur la page des détails des ressources est désormais accessible à l’aide des touches du clavier (NPR-33397).

* Les états développés et réduits de la boîte de dialogue [!UICONTROL Balises] sur les [!UICONTROL propriétés] de la ressource et la navigation ferroviaire de gauche (dans l’interface utilisateur des ressources) sont maintenant correctement annoncés par les lecteurs d’écran (NPR-33396).

* Titles of all the browsed pages on [!DNL Adobe Experience Manager] Assets are now unique (NPR-33343).

* Lors de la navigation dans la structure de l&#39;arbre, divers éléments du contrôle de la vue de l&#39;arbre sont maintenant annoncés correctement par les lecteurs d&#39;écran (NPR-33304).

* Différentes versions des ressources de la vue de [!UICONTROL chronologie] sur la page des détails des ressources sont désormais accessibles à l’aide des touches du clavier (NPR-33283).

* Les noms des suggestions de recherche apparaissant dans la zone de liste modifiable d&#39;Omnisearch sont maintenant annoncés par les lecteurs d&#39;écran lors de l&#39;utilisation de la fonctionnalité de recherche (NPR-33280).

* Les éléments cliquables et [!UICONTROL Atteindre le lien] dans le rail  Références sont maintenant annoncés par les lecteurs d’écran comme éléments cliquables (NPR-33278).

* Les informations relatives à la structure des tableaux (comme la ligne 1, la cellule 1, le tableau) de la boîte de dialogue [!UICONTROL Partager le lien] ne sont plus annoncées par les lecteurs d’écran lorsque la boîte de dialogue s’ouvre (NPR-33268).

* Les lecteurs d’écran (NPR-33235) ont maintenant correctement annoncé l’objectif de divers éléments de la zone de liste modifiable (tels que le champ Chemin et l’option permettant d’ouvrir la boîte de dialogue Sélection dans l’onglet Simple des Propriétés du fichier).

* Les informations indiquant que les lignes du tableau de la vue de liste peuvent être sélectionnées sont maintenant communiquées aux utilisateurs de lecteurs d’écran lorsque le clavier est activé sur ces lignes. Lorsqu’un pointeur survole les rangées, les lecteurs d’écran annoncent les informations (NPR-33234).

* Options (having [!UICONTROL x]) to remove each of the selected tags below the [!UICONTROL Tags] field in [!UICONTROL Basic] tab of [!UICONTROL Properties] are now accessible to screen readers (NPR-33206).

* Le sélecteur de dates du calendrier peut désormais être activé et activé à l’aide du clavier par les utilisateurs de lecteurs d’écran et les utilisateurs de clavier voyants (NPR-33200).

* La bascule entre la vue de liste et la vue de carte expose désormais correctement sa fonctionnalité (d&#39;ajustement des vues) au lecteur d&#39;écran (NPR-33069).

* Le menu du rail de gauche est maintenant accessible. Les lecteurs d&#39;écran annoncent à juste titre la fonctionnalité et l&#39;objectif de l&#39;extension du menu (NPR-33068).

* La zone de Liste et de nombreux autres éléments de l’interface utilisateur sont désormais accessibles aux utilisateurs de lecteurs d’écran non voyants. Les lecteurs d’écran annoncent les informations suivantes (NPR-33040) :

   * si la saisie de l’utilisateur est requise sur un élément avant l’envoi du formulaire.
   * si un élément n’est pas modifiable.
   * si un widget est sélectionné ou non.

* L’option d’ouverture de la barre latérale du filtre est désormais accessible à l’aide du clavier (NPR-32842, CQ-4273018).

* Le contrôle de case à cocher dans l&#39;en-tête de colonne de la vue de liste est maintenant accessible et le but de l&#39;utilisation du contrôle est annoncé par les lecteurs d&#39;écran (NPR-32722, NPR-33005).

* Les libellés des champs Heures (HH) et Minutes (mm) du sélecteur de date de calendrier sont désormais des libellés permanents au lieu des libellés d’espace réservé et ne disparaissent pas lorsque l’utilisateur saisit du texte dans ces champs (NPR-32720).

* Le texte des liens des notifications (qui s&#39;affichent après avoir cliqué sur l&#39;icône représentant une cloche) est maintenant annoncé aux utilisateurs de lecteurs d&#39;écran, qui utilisent l&#39;onglet pour accéder à chaque lien (NPR-32645).

* [!UICONTROL Les options Sélectionner], [!UICONTROL Télécharger], [!UICONTROL Propriétés]et Autres actions  sur les cartes de ressources dans Insights Vue sont désormais accessibles à l’aide du clavier (NPR-32609).

* Le contenu masqué visuellement (tel que le contenu de la barre de menus de l&#39;en-tête dans les résultats de la recherche) n&#39;est plus annoncé par les lecteurs d&#39;écran lorsqu&#39;on y accède à l&#39;aide du clavier (NPR-32606).

* Les lecteurs d’écran annoncent maintenant l’objectif des étiquettes sur les commandes pour passer aux mois suivants et aux mois précédents dans le sélecteur de dates du calendrier (NPR-32604).

* Les icônes d&#39;évaluation des étoiles peuvent désormais être activées et activées à l&#39;aide des touches du clavier (NPR-32513).

* La fonctionnalité de contrôle du volume vidéo est désormais accessible via la tabulation (pour mettre l&#39;accent sur le curseur de volume) et les touches fléchées (pour régler le volume) sur le clavier (NPR-32065).

* L’objectif des champs d’entrée Limité inférieure ([!UICONTROL De]) et Limite supérieure ([!UICONTROL À]) du filtre Taille du fichier est maintenant annoncé aux utilisateurs de lecteurs d’écran non voyants (NPR-32064).

* Le menu [!UICONTROL Langues] du formulaire [!UICONTROL Créer et Traduire] est désormais accessible aux lecteurs d’écran en mode de navigation (CQ-4293906).

* Le panneau [!UICONTROL Références] est maintenant accessible avec les améliorations suivantes (NPR-33261, CQ-4293798) :

   * En mode Parcourir, le lecteur d’écran n’affiche plus les champs de modification multiligne masqués sous Références du site, Références de ressources, [!UICONTROL Copies]et Références de [!UICONTROL formulaire.]

   * Les lecteurs d’écran annoncent maintenant le rôle des éléments Références [!UICONTROL du] site et Copies [!UICONTROL de] langue.

   * La cible des lecteurs d’écran en mode de navigation se déplace, dans une séquence significative, vers divers éléments.

* [!UICONTROL La page Editeur] de Schéma de métadonnées et ses éléments sont désormais accessibles à l’aide du clavier et sont compatibles avec les lecteurs d’écran (CQ-4290962, CQ-4272953).

* L’objectif du `X` symbole de suppression des balises sélectionnées est maintenant annoncé par les lecteurs d’écran, ainsi que le nombre de balises sélectionnées (CQ-4273017).

* Pour éviter toute confusion pour les utilisateurs non voyants utilisant un lecteur d’écran, les icônes et images décoratives sont désormais ignorées par les lecteurs d’écran (CQ-4272944).

**Problèmes résolus dans les ressources Experience Manager**

[!DNL Adobe Experience Manager] 6.5.5.0 Le module Ressources résout les problèmes suivants :

* [!UICONTROL L’option Début] de la boîte de dialogue [!UICONTROL Créer un flux de travail] pour les ressources d’une collection est désactivée, ce qui empêche le déclenchement du flux de travail (NPR-32471).

* Lors de l’utilisation d’une fenêtre contextuelle en cascade dans des schémas de métadonnées, lors de la sélection et de l’enregistrement d’une option déroulante contenant une apostrophe (dans la liste déroulante enfant), l’option d’apostrophe sélectionnée disparaît après la réouverture des [!UICONTROL propriétés] de la ressource (NPR-32649).

* [!UICONTROL La tâche] de synchronisation d’Asset Insights s’arrête et échoue si elle rencontre des entrées non valides (côté Analytics) au lieu de passer à l’entrée suivante (NPR-32674).

* Le gyroscope n’est pas fonctionnel, car les capteurs de mouvements sont désactivés par défaut sur les navigateurs mobiles dans la visionneuse panoramique (CQ-4272937).

* [!UICONTROL L&#39;Assistant Configuration] des ressources connectées ne fonctionne pas avec l&#39;erreur 404 lors de l&#39;installation de la version 6.5.3 sur la version 6.5.1 (NPR-32730).

* Au cours du processus d’écriture différée XMP, toutes les propriétés de métadonnées d’espace de nommage personnalisé remplacent le préfixe d’espace de nommage personnalisé par ns2, contrairement au préfixe d’espace de nommage configuré (NPR-32748).

* Le chargement différé n&#39;est pas déclenché et seules 100 ressources s&#39;affichent lors de la sélection pour consulter les tâches de la boîte de réception des notifications (NPR-32750).

* `NullPointerException` est observé en raison de l’absence de préférences de noeud dans le nouveau profil utilisateur (SAML/SSO). Cette erreur empêche les utilisateurs nouvellement connectés d’utiliser [!DNL Adobe Experience Manager Stock] l’intégration (NPR-32777).

* Des avertissements de tendance sont observés dans les journaux lors de l’ouverture d’une collection dynamique contenant plus de 10 000 actifs (NPR-32980).

* Les noms des fichiers sont changés en minuscules lorsque vous déplacez des fichiers d’un dossier à un autre en [!DNL Adobe Experience Manager] mode d’exécution Dynamic Media Scene7 (NPR-32995).

* Une ressource recherchée ne peut pas être supprimée après avoir accédé à ses propriétés à partir des résultats de la recherche, puis être revenue aux résultats de la recherche pour la supprimer (NPR-32998).

* [!UICONTROL L&#39;option Suivant] reste désactivée lors de la sélection du dossier de destination dans l&#39;interface [!UICONTROL Déplacer les actifs] (NPR-33356).

* [!UICONTROL L’option Suivant] n’est pas activée lors de la sélection du noeud parent (où un dossier enfant unique est visible), puis lors de la sélection du dossier enfant (NPR-33275).

* Les autorisations d&#39;archivage et d&#39;extraction sont désactivées sur Adobe Asset Link (AAL) pour les utilisateurs disposant d&#39;autorisations de suppression, même si d&#39;autres autorisations telles que la lecture, la création ou la modification sont accordées (NPR-33272).

* Les rendus de recadrage dynamique ne sont pas disponibles dans la boîte de dialogue de téléchargement de fichier (NPR-33167).

* Une exception est observée dans les journaux à l’ouverture du rail de rendus pour un fichier PDF sous un dossier avec un profil de recadrage intelligent (CQ-4294201).

* Les paramètres d’image prédéfinis ne sont pas publiés si le mode [!UICONTROL de synchronisation] Dynamic Media est désactivé par défaut sur le Experience Manager en mode d’exécution Dynamic Media Scene7 (CQ-4294200).

* Le traitement des ressources pendant le chargement en masse est bloqué et l’instance de workflow affiche les instances bloquées de la ressource de mise à jour de gestion des actifs numériques (CQ-4293916).

* La création d’une configuration Dynamic Media sur un Experience Manager fonctionne, mais dans l’interface utilisateur, rien ne se passe lorsque vous sélectionnez Enregistrer (CQ-4292442).

* La Prévisualisation des fichiers vidéo F4V ne fonctionne pas dans la lecture progressive sur Safari/Mac (CQ-4289844).

* Un dossier supplémentaire est créé lors du recadrage intelligent d’un fichier se trouvant dans un dossier parent dont le nom contient un caractère point `.` (CQ-4289337).

* La miniature est rompue et la bannière de traitement vidéo n’est pas affichée lorsqu’une vidéo est copiée (CQ-4284125).

* La visionneuse de dimensions affiche incorrectement les vignettes vides dans Firefox pour certains modèles avec des vues d’appareil photo vides (CQ-4283447).

* Les problèmes de performances corrigés dans la version 6.5.5.0 sont (CQ-4279206) :

   * Le téléchargement de fichiers binaires volumineux sur les serveurs de traitement des images Dynamic Media prend trop de temps.

   * Le temps de génération des miniatures sur le Experience Manager augmente en raison de l’architecture Dynamic Media Scene7.

* Les problèmes de migration vers Dynamic Media Scene7 échouent pour les clients disposant d’un grand nombre de ressources (CQ-4279206).

* La mise en page de la visionneuse de vidéos 360 est interrompue si `setVideo` elle est utilisée et la vidéo est décalée vers le bas sur `video= modifier` (CQ-4263201).

* Un message d&#39;erreur s&#39;affiche lors de l&#39;installation du package SDL Experience Manager (NPR-33175).

### Plate-forme {#platform-6550}

* Le [!DNL Sling] filtre n’est pas appelé si l’entrée de `sling:match` mappage est créée sous `/etc/maps` (NPR-33362).
* Le Experience Manager se bloque en raison d’une erreur de segmentation avec [!DNL Apache Lucene] (NPR-32988).
* [!DNL Jackson] package principal manquant dans le fichier uberjar Experience Manager (NPR-32848).
* CRXDE Lite ne charge pas le contenu pour les utilisateurs sans autorisation de lecture sur la `jcr:primaryType` propriété d’un noeud (NPR-32611).
* [!DNL Granite] le Planificateur de la tâche de maintenance se réinitialise trop souvent lors de déploiements Experience Manager (CQ-4294627).
* Lorsqu&#39;une requête SQL s&#39;exécute pendant longtemps, par exemple pendant 7 heures, le Experience Manager cesse de répondre (NPR-33044).

### Interface utilisateur {#ui-6550}

* La sélection des boutons radio n’est pas conservée dans un champ multiple (NPR-33309).
* La limite de chargement différé ne fonctionne pas pour la vue de liste (NPR-33124).
* La page de résultats d&#39;Omnisearch n&#39;affiche pas de message s&#39;il n&#39;y a pas de correspondance (NPR-32974).
* Le filtre Omnisearch renvoie toutes les correspondances sous le `/content` noeud ignorant l&#39;emplacement sélectionné (NPR-32849).

### Intégrations {#integrations-6550}

* Le cache interne est effacé lorsqu&#39;une page avec un composant d&#39;Adobe Target est publiée (NPR-33162).
* L&#39;intégration à l&#39;Adobe Target ne fonctionne pas le [!DNL Windows Internet Explorer] 11 (NPR-33111).
* Lors de la configuration de l&#39;Adobe Target, les champs [!UICONTROL Société] et Suite de [!UICONTROL rapports] n&#39;apparaissent pas lors de la sélection d&#39;une source de rapports (NPR-32502).
* Lors de l’exportation [!DNL Experience Fragments] à l’aide des E/S Adobe, les métadonnées telles que le produit source ne sont pas exportées dans l’Adobe Target (NPR-32159).
* Les utilisateurs IMS autorisés du groupe d&#39;administrateurs de Experience Manager locaux ne peuvent pas créer ni modifier de configurations IMS (NPR-33045).
* La page des configurations de lancement Adobe n&#39;affiche pas tous les enregistrements (NPR-33011).
* Les utilisateurs du groupe d’auteurs de contenu ne peuvent pas modifier les propriétés d’un composant d’Adobe Target en raison d’une erreur JavaScript (NPR-32996).

### Projets de traduction {#translation-6550}

* Les balises traduites ne sont pas importées en Experience Manager à partir de services de traduction tiers (NPR-33154).
* La page de configuration de traduction affiche un fournisseur de traduction incorrect par rapport à celui utilisé pour la traduction (NPR-32971).
* Ajouter un dossier de fragments d’expérience à un projet de traduction existant crée un nouveau projet (NPR-32843).
* Une `NullPointerException` erreur s&#39;affiche dans les journaux d&#39;exécution d&#39;une tâche de traduction (NPR-32628).

### WCM {#wcm-6550}

* Editeur de page : [!DNL Sites] l’éditeur de page ne permet pas aux utilisateurs utilisant uniquement le clavier d’accéder au contenu principal au lieu de déplacer la sélection de l’onglet dans toutes les options disponibles dans l’en-tête (CQ-4293883).
* Editeur de page : les panneaux qui utilisent le composant Well et incluent des données enregistrées ne s’affichent pas en raison de mises à jour dans [!DNL Chrome] et [!DNL Firefox] versions (CQ-4292995).
* MSM - La suppression d&#39;un composant de la page ne supprime pas le composant de la version publiée de la page (CQ-4292360).

### [!DNL Brand Portal] {#assets-brand-portal-6550}

* Removing a published metadata schema from [!DNL Brand Portal] results in an error (CQ-4292063).
* Si un administrateur configure [!DNL Experience Manager Assets] 6.5.4 avec Brand Portal via Adobe Developer Console, l’ [!DNL Brand Portal] utilisateur ne peut pas publier la ressource d’un dossier de contribution de [!DNL Brand Portal] à [!DNL Experience Manager] (NPR-33046).
* Réplication Duplicata des dossiers parents à l’origine de conflits (NPR-33001).

### [!DNL Communities] {#communities-6550}

* Impossible de supprimer une carte dans la console de modération à l&#39;aide de l&#39;option de menu Edition rapide (NPR-33117).
* Une erreur se produit lors de l&#39;accès à la page [!UICONTROL Activité Stream] (NPR-33146).
* Les groupes supprimés sur l’instance d’auteur ne sont pas supprimés de toutes les instances de publication (NPR-33199).
* Les auteurs, après avoir créé un nouveau groupe, ne sont pas redirigés vers la section Groupe  communautaire le [!DNL Internet Explorer] 11 (NPR-33205).
* L&#39;accès à un message dans la boîte de réception du Experience Manager ne modifie pas l&#39;état du message en Lecture (NPR-32764).
* La modification d’un [!DNL Communities] groupe et de l’image miniature ne met pas à jour l’image miniature du groupe (NPR-32599).
* Un utilisateur ne peut pas envoyer de courrier électronique à un autre utilisateur d&#39;une communauté (NPR-32598).
* Un blog envoyé ne s&#39;affiche pas tant que l&#39;utilisateur n&#39;a pas actualisé la page (NPR-32391).
* Lors de la création d’une version de notifications et d’abonnements de contenu généré par l’utilisateur (UGC), un ID incorrect de la page source est stocké (CQ-4279355, CQ-4289703).

### Workflow {#workflow-6550}

* Le chargement de l’option [!UICONTROL Chronologie] dans le rail de gauche prend plus de temps que prévu (NPR-32851).
* Après le redémarrage d’une instance de Experience Manager, le courrier électronique de la tâche de révision d’une collection contient un lien de charge utile incorrect (NPR-32774).

### [!DNL Forms] {#forms-6550}

>[!NOTE]
>
>Experience Manager Service Pack n’inclut pas de correctifs pour [!DNL Forms]. Les correctifs sont fournis à l’aide d’un module complémentaire Forms distinct.  En outre, un programme d’installation cumulatif est publié, qui comprend des correctifs pour AEM Forms on JEE. For more information, see [Install AEM Forms add-on](#install-aem-forms-add-on-package) and [Install AEM Forms on JEE](#install-aem-forms-jee-installer).

* Correspondence Management : L’ordre des actifs dans une zone de cible varie après avoir envoyé une lettre (NPR-33359, NPR-33153).
* Formulaires adaptatifs : Lorsqu’un utilisateur modifie un formulaire adaptatif, l’option Processus [!UICONTROL de] Début disponible dans le menu Informations [!UICONTROL sur la] page ne fonctionne pas (NPR-33004).
* Formulaires adaptatifs : L’utilisateur ne peut pas enregistrer de formulaire adaptatif contenant plusieurs pièces jointes (NPR-32997).
* Formulaires adaptatifs : La modification de la disposition du panneau dans un formulaire adaptatif entraîne une erreur (CQ-4293880).
* Formulaires adaptatifs : Une nouvelle ligne d’une chaîne dans un dictionnaire de formulaires adaptatifs ajoute `&#xa;` des caractères au dictionnaire (NPR-33266).
* Accessibilité des formulaires adaptatifs : Lorsqu’un utilisateur prévisualisation un formulaire adaptatif en tant que formulaire HTML, le champ de signature  tactile n’est pas en mesure de conserver le focus de tabulation (NPR-33159).
* Accessibilité des formulaires adaptatifs : Les messages d’erreur qui s’affichent lors de l’envoi d’un formulaire adaptatif ne sont pas liés à un `aria-describedBy` attribut (NPR-33071).
* Accessibilité des formulaires adaptatifs : L’attribut obligatoire des champs marqués comme obligatoires dans un formulaire adaptatif n’est pas défini sur True dans le schéma d’accessibilité ARIA (NPR-33070).
* Service PDFG : Lorsqu’un utilisateur convertit un fichier texte au format PDF, les caractères japonais ne s’affichent pas correctement (NPR-33238).
* Service PDFG : `CreatePDF` ne parvient pas à convertir un fichier PDF au format OCR PDF (NPR-32994).
* Service PDFG : La conversion PDF échoue pour la 200e instance d’un [!DNL OpenOffice] document (NPR-32766).
* BackendIntegration : Les demandes de modèle de données de formulaire échouent lorsque le jeton d’actualisation expire en raison d’un état inactif incorrect (NPR-33169).
* Designer : Les lecteurs d’écran exécutent l’ordre de tabulation en fonction de l’ordre géographique par défaut au lieu de l’ordre de tabulation personnalisé défini dans le fichier XDP (NPR-32160).
* Designer : Si l’option de balisage est activée, la bordure du sous-formulaire disparaît dans la sortie PDF générée (NPR-32778).

## Install 6.5.5.0 {#install}

**Conditions requises**

* AEM 6.5.5.0 requires AEM 6.5. See [upgrade documentation](/help/sites-deploying/upgrade.md) for detailed instructions.
* Le téléchargement du Service Pack est disponible sur Adobe [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
* Lors d’un déploiement avec MongoDB et plusieurs instances, installez AEM 6.5.5.0 sur l’une des instances d’auteur à l’aide du gestionnaire de modules.
* Avant l’installation, effectuez un instantané ou une nouvelle sauvegarde de votre instance AEM.
* Redémarrez l’instance avant l’installation. Cela est nécessaire uniquement lorsque l’instance reste en mode de mise à jour (ce qui est le cas lorsque l’instance vient d’être mise à jour depuis une version antérieure). Toutefois, cela est recommandé si l’instance s’est exécutée pendant une longue durée.

>[!NOTE]
>
>Adobe ne recommande pas de supprimer ou de désinstaller le package Adobe Experience Manager 6.5.5.0.

### Installation du Service Pack {#install-service-pack}

Effectuez les étapes suivantes pour installer le Service Pack sur une instance d’Adobe Experience Manager 6.5 existante :

1. Téléchargez le Service Pack depuis [Package Share](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/AEM-6.5.5.0-Service-Pack) ou Distribution [de](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.5.zip)logiciels.

1. Ouvrez Package Manager et cliquez sur **[!UICONTROL Télécharger le package]** pour télécharger le package. Pour savoir comment l’utiliser, voir [Package Manager](https://docs.adobe.com/content/help/fr-FR/experience-manager-65/administering/contentmanagement/package-manager.html).

1. Select the package and click **[!UICONTROL Install]**.

>[!NOTE]
>
>La boîte de dialogue de l’interface utilisateur de Package Manager se ferme parfois lors de l’installation du Service Pack. Adobe recommande d’attendre que les journaux d’erreurs se stabilisent avant d’accéder au déploiement. Attendez les journaux spécifiques liés à la désinstallation du lot de mise à jour avant de vous assurer que l&#39;installation est réussie. Typically, this happens on [!DNL Safari] but can intermittently happen on any browser.

**Installation automatique**

Il existe deux manières d’installer automatiquement l’Adobe Experience Manager 6.5.5.0 sur une instance de travail :

R. Placez le package dans `../crx-quickstart/install` un dossier lorsque le serveur est disponible en ligne. Le package est automatiquement installé.

B. Utilisez l’API [HTTP de Package Manager](https://docs.adobe.com/content/docs/en/crx/2-3/how_to/package_manager.html). Utilisez `cmd=install&recursive=true` pour installer les packages imbriqués.

>[!NOTE]
>
>L’Adobe Experience Manager 6.5.5.0 ne prend pas en charge l’installation de Bootstrap.

**Validation de l’installation**

1. La page d’informations sur le produit (`/system/console/productinfo`) affiche la chaîne de version mise à jour `Adobe Experience Manager (6.5.5.0)` sous Produits installés.

1. All OSGi bundles are either **[!UICONTROL ACTIVE]** or **[!UICONTROL FRAGMENT]** in the OSGi Console (Use Web Console: `/system/console/bundles`).

1. The OSGI bundle `org.apache.jackrabbit.oak-core` is version 1.10.6 or higher (Use Web Console: `/system/console/bundles`).

Pour connaître les plates-formes certifiées pour fonctionner avec cette version, voir les exigences [](/help/sites-deploying/technical-requirements.md)techniques.

### Installation du module complémentaire Adobe Experience Manager Forms {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Passez cette étape si vous n’utilisez pas AEM Forms. Les correctifs dans les Adobes Experience Manager Forms sont diffusés par le biais d’un module complémentaire distinct.

1. Vérifiez que vous avez installé le Service Pack Adobe Experience Manager.
1. Download the corresponding Forms add-on package listed at [AEM Forms releases](https://helpx.adobe.com/fr/aem-forms/kb/aem-forms-releases.html) for your operating system.
1. Install the Forms add-on package as described in [Installing AEM Forms add-on packages](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

### Installation de Adobe Experience Manager Forms sur JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Passez cette étape si vous n’utilisez pas AEM Forms sous JEE. Les correctifs d’Adobe Experience Manager Forms sur JEE sont diffusés par le biais d’un programme d’installation distinct.

For information about installing the cumulative installer for Experience Manager Forms on JEE and post-deployment configuration, see the [release notes for patch 0014](https://helpx.adobe.com/aem-forms/quick-fixes/6-5/jee-patch-0014.html).

### UberJar {#uber-jar}

UberJar pour Experience Manager 6.5.5.0 est disponible dans le référentiel [](https://repo.adobe.com/nexus/content/groups/public/com/adobe/aem/uber-jar/6.5.5/)Adobe Public Maven.

Pour utiliser UberJar dans un projet Maven, voir [comment utiliser UberJar](/help/sites-developing/ht-projects-maven.md) et inclure la dépendance suivante dans le POM de votre projet :

```shell
<dependency>
      <groupId>com.adobe.aem</groupId>
      <artifactId>uber-jar</artifactId>
      <version>6.5.5</version>
      <classifier>apis</classifier>
      <scope>provided</scope>
</dependency>
```

## Fonctionnalités obsolètes {#removed-deprecated-features}

Cette section liste les fonctionnalités et fonctionnalités qui ont été marquées comme obsolètes avec AEM 6.5.5.0. Les fonctionnalités qui doivent être supprimées dans une version ultérieure sont définies comme obsolètes en premier, avec une autre option à utiliser.

Il est conseillé aux clients de vérifier s’ils utilisent la fonctionnalité ou la fonctionnalité dans leur déploiement actuel et de planifier la modification de leur mise en oeuvre pour utiliser l’autre option.

| Zone | Fonctionnalité | Remplacement |
|---|---|---|
| Intégrations | L’écran d’inscription **[!UICONTROL des]** AEM cloud services est obsolète. Avec l’intégration d’AEM et de Cible mise à jour dans AEM 6.5 pour la prise en charge de l’API du Target Standard, qui utilise l’authentification via Adobe IMS et E/S, et le rôle croissant de Adobe Launch pour l’instrumentation des pages AEM pour l’analyse et la personnalisation, l’assistant d’inclusion est devenu non pertinent du point de vue fonctionnel. | Configurez les connexions système, l&#39;authentification Adobe IMS et les intégrations d&#39;E/S Adobe via les AEM cloud services respectifs. |
| Connecteurs | Adobe JCR Connector for Microsoft SharePoint 2010 et Microsoft SharePoint 2013 est obsolète pour AEM 6.5. | N/A |

## Problèmes connus {#known-issues}

* Si vous installez [!DNL Experience Manager] 6.5.5.0 avec [!DNL Java] 11, redémarrez le serveur après avoir installé le Service Pack. Aucun redémarrage n&#39;est nécessaire si vous installez le Service Pack avec [!DNL Java] 8.

* If a folder in the hierarchy is renamed in [!DNL Experience Manager Assets] and the nested folder containing an asset is published to [!DNL Brand Portal], the title of the folder is not updated in [!DNL Brand Portal] until the root folder is published again.

* Lors de l’installation d’AEM 6.5.5.0, la mise à jour de [!DNL Chrome] la version 83 entraîne un problème lors de la création de packages. Utilisez d’autres navigateurs disponibles, tels que [!DNL Internet Explorer] et [!DNL Firefox], ou d’autres options d’installation de package standard d’AEM pour résoudre le problème. Le problème est résolu après l’installation d’AEM 6.5.5.0.

* Impossible d&#39;envoyer un courrier électronique au serveur SMTP distant à l&#39;aide de l&#39;expéditeur de courrier par défaut d&#39;AEM, car il permet uniquement la communication à l&#39;aide de TLS v1.2. Supprimez le lot `javax.mail:mail:1.5.0-b01` de `system/console` et actualisez les lots pour résoudre le problème.

* Lorsqu’un utilisateur sélectionne pour la première fois un champ dans un formulaire adaptatif, l’option permettant d’enregistrer une configuration ne s’affiche pas dans le navigateur de propriétés. La sélection pour configurer un autre champ du formulaire adaptatif dans le même éditeur résout le problème.

* Si l’assistant de configuration [!UICONTROL des ressources] connectées renvoie un message d’erreur 404 après l’installation, réinstallez manuellement les `cq-remotedam-client-ui-content` packages et `cq-remotedam-client-ui-components` packages à l’aide de Package Manager.

* Les erreurs et messages d’avertissement suivants peuvent s’afficher lors de l’installation d’AEM 6.5.x.x :
   * « Lorsque l’intégration de Target est configurée dans AEM à l’aide de l’API Target Standard (authentification IMS), l’exportation de fragments d’expérience vers Target entraîne la création de types d’offres incorrects. Au lieu du type « Fragment d’expérience » / source « Adobe Experience Manager », Target crée plusieurs offres avec le type « HTML » / source « Adobe Target Classic ».
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: Aucune fenêtre de maintenance n’a été trouvée sur granite/operations/maintenance.
   * La validation côté serveur du formulaire adaptatif échoue lorsque des fonctions d’agrégat telles que SUM, MAX et MIN sont utilisées. CQ-4274424
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Aucune fenêtre de maintenance n’a été trouvée sur granite/operations/maintenance.
   * La zone réactive d’une image interactive Dynamic Media n’est pas visible lors de la prévisualisation du fichier via la visionneuse de bannières modifiables.

## OSGi bundles and content packages included {#osgi-bundles-and-content-packages-included}

Les documents de texte suivants liste les lots OSGi et les packages de contenu inclus dans AEM 6.5.5.0 :

* [Liste des lots OSGi inclus dans AEM 6.5.5.0](assets/6550_bundles.txt)

* [Liste des packages de contenu inclus dans AEM 6.5.5.0](assets/6550_packages.txt)

## Restricted sites {#restricted-sites}

Ces sites sont réservés aux clients. Si vous êtes client et avez besoin d’un accès, contactez votre responsable de compte Adobe.

* [Téléchargement du produit à l’adresse licensing.adobe.com](https://licensing.adobe.com/)
* [Contactez l&#39;assistance](https://docs.adobe.com/content/help/en/customer-one/using/home.html)clientèle Pour plus d&#39;informations sur l&#39;accès au portail d&#39;assistance, consultez [Accès au portail](https://helpx.adobe.com/fr/experience-manager/kb/accessing-aem-support-portal.html)d&#39;assistance.

>[!MORELIKETHIS]
>
>* [Notes de mise à jour d’AEM 6.5](/help/release-notes/release-notes.md)
>* [Page de produits AEM ](https://www.adobe.com/solutions/web-experience-management.html)
>* [Documentation d’AEM 6.5](https://helpx.adobe.com/fr/support/experience-manager/6-5.html)
>* Subscribe to [Adobe priority product updates](https://www.adobe.com/subscription/priority-product-update.html)

