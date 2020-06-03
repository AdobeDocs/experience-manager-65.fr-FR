---
title: 'Notes de mise à jour d’AEM 6.5, Pack de services '
description: Notes de mise à jour spécifiques à Adobe Experience Manager 6.5 Service Pack 5.
docset: aem65
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: d51577195e969ff8af31be49159ff575e3654cc9
workflow-type: tm+mt
source-wordcount: '4476'
ht-degree: 11%

---


# Notes de mise à jour de Adobe Experience Manager 6.5 Service Pack {#aem-service-pack-release-notes}

## Informations sur la version {#release-information}

| Produits | **Adobe Experience Manager 6.5** |
|---|---|
| Version | 6.5.5.0 |
| Type | Version du Service Pack |
| Date  | 4 juin 2020 |
| URL de téléchargement | [Package Share](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/AEM-6.5.5.0-Service-Pack), distribution [de logiciels ](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.5.zip) |

## Éléments inclus dans Adobe Experience Manager 6.5.5.0 {#what-s-included-in-aem}

Adobe Experience Manager 6.5.5.0 est une mise à jour importante qui comprend de nouvelles fonctionnalités, les améliorations et les performances des clients clés, la stabilité et les améliorations de sécurité, publiée depuis la version 6.5 d’ **avril 2019**. Il peut être installé sur la version 6.5 d’Adobe Experience Manager (AEM).

Voici quelques-unes des principales fonctionnalités et améliorations introduites dans AEM 6.5.5.0 :

* Personnalisation des noms de colonne qui s’affichent dans la boîte de réception AEM.

* Amélioration de l’accessibilité dans diverses zones de la Gestion de contenu Web AEM (WCM), telles que l’éditeur de page, les composants principaux, RTE et l’interface utilisateur d’administration.

* Enregistrement d’une communication interactive en tant que brouillon.

* Prise en charge [!DNL Oracle WebLogic 12] d’AEM Forms sur JEE.

* La gestion des exceptions est maintenant améliorée dans le flux de l’interface utilisateur [!DNL Adobe Experience Manager] Ressources.

* Une nouvelle méthode `getRemoteAssetPublishURL` est ajoutée à `com.day.cq.dam.api.s7dam.scene7.ImageUrlApi` l’interface pour obtenir l’URL de publication pour les médias dynamiques Scene7.

* [Améliorations](#assets-6550-changes) de l’accessibilité dans [!DNL Adobe Experience Manager] les ressources en conformité avec les directives WCAG (Web Content Accessibility Guidelines).

* Suppression de l’intégration Package Share avec Adobe Experience Manager.

* Le référentiel intégré (Apache Jackrabbit Oak) a été mis à niveau vers la version 1.22.3.

Pour une liste complète des fonctionnalités, des points saillants et des principales fonctionnalités introduites dans AEM 6.5 Service Pack 5, reportez-vous à la page [Nouveautés d’Adobe Experience Manager 6.5 Service Pack 5](new-features-latest-service-pack.md) .

Voici la liste des correctifs fournis dans la [!DNL Experience Manager] version 6.5.5.0.

### Sites {#sites-6550}

* Les sites AEM offrent une option pour publier ou annuler la publication d’une page de son alias. L&#39;option ne fonctionne pas (NPR-33415).
* Lorsqu’un conteneur de mise en page est supprimé d’un modèle contenant plusieurs modèles, le rendu du modèle n’est pas correct (NPR-33347).
* Lorsqu’une page de sites AEM fait partie d’un ensemble de contenu volumineux avec plusieurs copies en direct, la prévisualisation d’historique des versions de page ne se charge pas (NPR-33311).
* Lorsque vous utilisez la commande Déplacer pour renommer une page Sites AEM, le titre de la page n’est pas mis à jour (NPR-33264).
* Lorsque vous déplacez des pages à travers la vue des colonnes, les colonnes disparaissent (NPR-33216).
* Lorsque le nom d&#39;un composant local dans une copie de langue est identique au nom d&#39;un composant dans le plan et que le composant est déployé à partir du plan, le terme _msm_move n&#39;est pas ajouté au nom du composant local (NPR-33208).
* La servlet Redirection de page ajoute .html à une URL de sites AEM où ResourceType n’est pas cq:Page (NPR-33176).
* Lorsque vous collez une sous-arborescence, vous n’avez pas la possibilité de décider si les sous-pages correspondantes doivent être collées ou non (NPR-33149).
* Le nombre de résultats dans les utilisations réelles d&#39;un composant est limité au nombre 49 (NPR-33058).
* Lorsque vous basez un fragment de contenu sur un schéma et qu’il contient une zone de texte obligatoire ou un champ de chemin, l’enregistrement du fragment de contenu échoue (NPR-33007).
* Lorsque vous créez un composant personnalisé à l’aide du composant de fragment d’expérience prêt à l’emploi et que vous l’utilisez dans les pages de sites AEM, AEM n’affiche pas les références (utilisation) du composant personnalisé (NPR-32852).
* Lorsque vous renommez un dossier avec un grand nombre de références, de nombreuses références au dossier ne sont pas mises à jour (NPR-32765).
* Lorsque vous activez l’option d’édition source, elle devient disponible pour les options d’affichage plein écran en ligne, mais reste absente pour les options de boîte de dialogue d’édition et d’affichage plein écran de l’éditeur de texte enrichi (NPR-32763).
* Si vous disposez d’un champ à plusieurs champs et qu’il contient un champ obligatoire (tel qu’une liste déroulante ou un champ de chemin) dans les propriétés de page d’un plan directeur, lorsqu’une page contenant un tel champ à plusieurs champs est déployée, les propriétés de page de la copie dynamique ne sont pas enregistrées. (NPR-32751)
* Les lecteurs d’écran ne peuvent pas utiliser la structure d’en-tête pour parcourir une page. En outre, l&#39;onglet Composants a un libellé incorrect (NPR-32648).
* Lors des débuts de pagination, le sélecteur de fragments d’expérience ne charge pas tous les éléments (NPR-32605).
* Les autorisations d’auteur pour lire, modifier, créer et supprimer des copies en direct sont révoquées. Chaque auteur devait fournir explicitement des autorisations de lecture et de modification pour déplacer des pages dans un plan directeur (NPR-32550).
* Les auteurs de contenu ne parviennent pas à créer le lancement d’une page qui est intégrée à Adobe Analytics (NPR-32548).
* Lorsqu&#39;un utilisateur reprend l&#39;héritage avec la synchronisation, la copie dynamique de la page parente ne se synchronise pas avec le plan et affiche un état incorrect (NPR-32500).
* Le chargement de la page de l’éditeur de sites AEM prend plus de 15 secondes (NPR-32413).
* Certains champs n&#39;affichent pas l&#39;option Annuler l&#39;héritage (NPR-32362).
* Lorsque vous sélectionnez un chemin pour un composant Fragment d’expérience et cochez la case Ouvrir la boîte de dialogue de sélection, vous n’accédez pas au chemin sélectionné dans le navigateur de chemins (NPR-32308).
* Lorsque vous effectuez une mise à niveau d’AEM 6.2 vers AEM 6.5, le composant Parsys des modèles statiques ne s’affiche pas correctement. La hauteur du composant Parsys est définie sur 0 et les composants qu&#39;il contient ne sont pas visibles. (NPR-33663).
* Lorsqu’un utilisateur copie et colle un Conteneur de mise en page sur la même page, les composants d’un Conteneur de mise en page ne s’affichent pas (NPR-33648).
* La vérification d&#39;intégrité du répartiteur affiche un message d&#39; `Invalid cookie header` avertissement dans les fichiers journaux (NPR-33629).

### Ressources {#assets-6550-changes}

**Améliorations de l’accessibilité dans les ressources d’Experience Manager**

* Il est désormais possible d’activer l’option [!UICONTROL Commentaires] au clavier et d’activer l’option de clic pour [!UICONTROL Créer] des commentaires de version sous [!UICONTROL Créer une nouvelle version] dans le panneau de ressources [!UICONTROL Chronologie (NPR-33424).]

* Il est désormais possible d’accéder à l’option Paramètres [!UICONTROL de] Vue pour les ressources et de modifier les paramètres dans la boîte de dialogue Paramètres [!UICONTROL de] Vue à l’aide des touches du clavier (NPR-33420).

* La liste déroulante de la zone de liste de la zone combinée (dans divers champs sur différentes pages) affiche désormais les entrées en tant que liste d’options qui peuvent être annoncées par les lecteurs d’écran (NPR-33516).

* Les lecteurs d’écran annoncent maintenant la fonctionnalité de tri des en-têtes pouvant être triés (dans la vue de liste, la vue de [!UICONTROL chronologie] et la page [!UICONTROL Gérer la publication] ) et les commandes de tri des en-têtes de colonne sont accessibles à l’aide du clavier (NPR-32979).

* Les éléments cliquables (tels que les cartes de commentaires, les mises à jour de version, les zones de liste modifiable et les icônes de chevron des menus) peuvent désormais être activés et exploitables à l’aide du clavier (NPR-33514).

* La fonctionnalité (ou l’objectif de l’action) des icônes d’informations (pour l’utilisation, les impressions et les clics) sur la Vue  Insights est maintenant correctement annoncée par les lecteurs d’écran (NPR-33513).

* Les champs de formulaire en lecture seule (par exemple, les champs désactivés dans l’onglet  Simple des [!UICONTROL propriétés]de la ressource) peuvent désormais être activés à l’aide du clavier (NPR-33493, CQ-4273031).

* Les étiquettes des différents champs d&#39;entrée sont maintenant des étiquettes permanentes (donc accessibles) et pas seulement des étiquettes d&#39;espace réservé, qui ont disparu au moment de la saisie du texte (NPR-33475).

* Différents niveaux d’en-tête (tels que les titres de page et les en-têtes de section) sont maintenant perçus comme des en-têtes avec des niveaux différents pour les utilisateurs de lecteurs d’écran (NPR-33471).

* Les éléments interactifs de l’interface utilisateur, tels que les liens et les options (sur l’en-tête et les options de zoom de la page des ressources, la navigation dans les dossiers), sont désormais accessibles à l’aide d’un clavier (NPR-33468, CQ-4271412).

* Les indicateurs de progression [!UICONTROL Options], [!UICONTROL Portée]et [!UICONTROL Workflows] de la page [!UICONTROL Gérer la publication sont désormais correctement lus par les lecteurs d’écran comme des indicateurs de progression, plutôt que comme des onglets (NPR-33416).]

* La couleur des icônes d’évaluation des étoiles (par exemple dans la section [!UICONTROL Notation] de l’onglet [!UICONTROL Avancé] dans [!UICONTROL Propriétés] de la ressource ou dans la vue de la carte) est modifiée pour que le contraste approprié soit visible pour les utilisateurs ayant une vision limitée et sans perception de couleur (NPR-33414).

* La flèche pointant vers le haut en regard du champ [!UICONTROL Commentaire] sur la page des détails des ressources est désormais accessible à l’aide des touches du clavier (NPR-33397).

* Les états développés et réduits de la boîte de dialogue [!UICONTROL Balises] sur les [!UICONTROL propriétés] de la ressource et la navigation ferroviaire de gauche (dans l’interface utilisateur des ressources) sont maintenant correctement annoncés par les lecteurs d’écran (NPR-33396).

* Les titres de toutes les pages consultées sur [!DNL Adobe Experience Manager] Assets sont désormais uniques (NPR-33343).

* Lors de la navigation dans la structure de l&#39;arbre, divers éléments du contrôle de la vue de l&#39;arbre sont maintenant annoncés correctement par les lecteurs d&#39;écran (NPR-33304).

* Différentes versions des ressources de la vue de [!UICONTROL chronologie] sur la page des détails des ressources sont désormais accessibles à l’aide des touches du clavier (NPR-33283).

* Les noms des suggestions de recherche apparaissant dans la zone de liste modifiable d&#39;Omnisearch sont maintenant annoncés par les lecteurs d&#39;écran lors de l&#39;utilisation de la fonctionnalité de recherche (NPR-33280).

* Les éléments cliquables et [!UICONTROL Atteindre le lien] dans le rail  Références sont maintenant annoncés par les lecteurs d’écran comme éléments cliquables (NPR-33278).

* Les informations relatives à la structure des tableaux (comme la ligne 1, la cellule 1, le tableau) de la boîte de dialogue [!UICONTROL Partager le lien] ne sont plus annoncées par les lecteurs d’écran lorsque la boîte de dialogue s’ouvre (NPR-33268).

* Les lecteurs d’écran (NPR-33235) ont maintenant correctement annoncé l’objectif de divers éléments de la zone de liste modifiable (tels que le champ Chemin et l’option permettant d’ouvrir la boîte de dialogue Sélection dans l’onglet Simple des Propriétés du fichier).

* Les informations indiquant que les lignes du tableau de la vue de liste peuvent être sélectionnées sont maintenant communiquées aux utilisateurs de lecteurs d’écran lorsque le clavier est activé sur ces lignes. Ces informations sont annoncées lorsque la souris survole les lignes (NPR-33234).

* Les options (comportant [!UICONTROL x]) permettant de supprimer chacune des balises sélectionnées sous le champ [!UICONTROL Balises] de l’onglet [!UICONTROL Réglages de base] de [!UICONTROL Propriétés sont désormais accessibles aux lecteurs d’écran (NPR-33206).]

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

* L’objectif de l’icône [!UICONTROL x] sur l’option de suppression des balises actuellement sélectionnées est également annoncé, ainsi que le nombre de balises sélectionnées (CQ-4273017).

* Les icônes et images décoratives sont désormais ignorées par les lecteurs d’écran, afin d’éviter toute confusion pour les utilisateurs non voyants utilisant un lecteur d’écran (CQ-4272944).

**Problèmes résolus dans les ressources d’Experience Manager**

[!DNL Adobe Experience Manager] 6.5.5.0 Le module Ressources résout les problèmes suivants :

* [!UICONTROL L’option Début] de la boîte de dialogue [!UICONTROL Créer un flux de travail] pour les ressources d’une collection est désactivée, ce qui empêche le déclenchement du flux de travail (NPR-32471).

* Lors de l’utilisation d’une liste déroulante en cascade dans les schémas de métadonnées, lors de la sélection et de l’enregistrement d’une option déroulante contenant une apostrophe (dans la liste déroulante enfant), l’option d’apostrophe sélectionnée disparaît après la réouverture des [!UICONTROL propriétés] de la ressource (NPR-32649).

* [!UICONTROL La tâche] de synchronisation d’Asset Insights s’arrête et échoue si elle rencontre des entrées non valides (côté Analytics) au lieu de passer à l’entrée suivante (NPR-32674).

* Le gyroscope n’est pas fonctionnel, car les capteurs de mouvements sont désactivés par défaut sur les navigateurs mobiles dans la visionneuse panoramique (CQ-4272937).

* [!UICONTROL L&#39;Assistant Configuration] des ressources connectées ne fonctionne pas avec l&#39;erreur 404 lors de l&#39;installation de la version 6.5.3 sur la version 6.5.1 (NPR-32730).

* Au cours du processus d’écriture différée XMP, toutes les propriétés de métadonnées d’espace de nommage personnalisé remplacent le préfixe d’espace de nommage personnalisé par ns2, contrairement au préfixe d’espace de nommage configuré (NPR-32748).

* Le chargement différé n&#39;est pas déclenché et seules 100 ressources s&#39;affichent lors de la sélection pour consulter les tâches de la boîte de réception des notifications (NPR-32750).

* `NullPointerException` est observé en raison de l’absence de préférences de noeud dans le nouveau profil utilisateur (SAML/SSO). Cette erreur empêche les utilisateurs nouvellement connectés d’utiliser [!DNL Adobe Experience Manager Stock] l’intégration (NPR-32777).

* Des avertissements de tendance sont observés dans les journaux lors de l’ouverture d’une collection dynamique contenant plus de 10 000 actifs (NPR-32980).

* Les noms des fichiers sont changés en minuscules lorsque vous déplacez des fichiers d’un dossier à un autre dans [!DNL Adobe Experience Manager] le mode d’exécution Contenu multimédia dynamique Scene7 (NPR-32995).

* Une ressource recherchée ne peut pas être supprimée après avoir accédé à ses propriétés à partir des résultats de la recherche, puis être revenue aux résultats de la recherche pour la supprimer (NPR-32998).

* [!UICONTROL L&#39;option Suivant] reste désactivée lors de la sélection du dossier de destination dans l&#39;interface [!UICONTROL Déplacer les actifs] (NPR-33356).

* [!UICONTROL L’option Suivant] n’est pas activée lors de la sélection du noeud parent (où un dossier enfant unique est visible), puis lors de la sélection du dossier enfant (NPR-33275).

* Les autorisations d&#39;archivage et d&#39;extraction sont désactivées sur Adobe Asset Link (AAL) pour les utilisateurs disposant d&#39;autorisations de suppression, même si d&#39;autres autorisations telles que la lecture, la création ou la modification leur sont autorisées (NPR-33272).

* Les rendus de recadrage dynamique ne sont pas disponibles dans la boîte de dialogue de téléchargement de fichier (NPR-33167).

* Une exception est observée dans les journaux à l’ouverture du rail de rendus pour un fichier PDF sous un dossier avec un profil de recadrage intelligent (CQ-4294201).

* Les paramètres d’image prédéfinis ne sont pas publiés si le mode [!UICONTROL de synchronisation Contenu multimédia] dynamique est désactivé par défaut sur AEM avec le mode d’exécution Contenu multimédia dynamique Scene7 (CQ-4294200).

* Le traitement des ressources pendant le chargement en masse est bloqué et l’instance de workflow affiche les instances bloquées de la ressource de mise à jour de gestion des actifs numériques (CQ-4293916).

* La création d’une configuration Contenu multimédia dynamique sur AEM fonctionne, mais dans l’interface utilisateur, rien ne se passe lorsque vous sélectionnez Enregistrer (CQ-4292442).

* La Prévisualisation des fichiers vidéo f4v ne fonctionne pas dans la lecture progressive sur Safari/Mac (CQ-4289844).

* Un dossier supplémentaire est créé lors du recadrage intelligent d’un fichier se trouvant dans un dossier parent dont le nom contient un caractère point `.` (CQ-4289337).

* La miniature est rompue et la bannière de traitement vidéo n’est pas affichée lorsqu’une vidéo est copiée (CQ-4284125).

* La visionneuse de dimensions affiche incorrectement les vignettes vides dans Firefox pour certains modèles avec des vues d’appareil photo vides (CQ-4283447).

* Les problèmes de performances corrigés dans la version 6.5.5.0 sont (CQ-4279206) :

   * Le téléchargement de fichiers binaires volumineux sur des serveurs de traitement d’images de médias dynamiques prend trop de temps.

   * Le temps de génération des miniatures sur AEM augmente en raison de l’architecture de Contenu multimédia dynamique Scene7.

* Les problèmes de migration de Dynamic Media Scene7 échouent pour les clients disposant d’un grand nombre de ressources (CQ-4279206).

* La mise en page de la visionneuse de vidéos 360 est interrompue si `setVideo` elle est utilisée et la vidéo est décalée vers le bas sur `video= modifier` (CQ-4263201).

* Un message d’erreur s’affiche lors de l’installation du package AEM SDL (NPR-33175).

### Plate-forme {#platform-6550}

* Le [!DNL Sling] filtre n’est pas appelé si l’entrée de `sling:match` mappage est créée sous `/etc/maps` (NPR-33362).
* AEM se bloque en raison d’une erreur de segmentation avec [!DNL Apache Lucene] (NPR-32988).
* [!DNL Jackson] package principal manquant dans le fichier jar uber d’AEM (NPR-32848).
* CRXDE Lite ne charge pas le contenu pour les utilisateurs sans l’autorisation READ sur la `jcr:primaryType` propriété d’un noeud (NPR-32611).
* [!DNL Granite] le Planificateur de la tâche de maintenance se réinitialise trop souvent lors des déploiements d’AEM (CQ-4294627).
* Lorsqu’une requête SQL s’exécute pendant une période plus longue, par exemple 7 heures, AEM arrête de répondre (NPR-33044).

### Interface utilisateur {#ui-6550}

* La sélection des boutons radio n’est pas conservée dans un champ multiple (NPR-33309).
* La limite de chargement différé ne fonctionne pas pour la vue de liste (NPR-33124).
* La page de résultats d&#39;Omnisearch n&#39;affiche pas de message s&#39;il n&#39;y a pas de correspondance (NPR-32974).
* Le filtre Omnisearch renvoie toutes les correspondances sous le `/content` noeud ignorant l&#39;emplacement sélectionné (NPR-32849).

### Intégrations {#integrations-6550}

* Le cache interne est effacé lorsqu’une page avec un composant Adobe Cible est publiée (NPR-33162).
* L&#39;intégration à Adobe Cible ne fonctionne pas le [!DNL Windows Internet Explorer] 11 (NPR-33111).
* Lors de la configuration de la Cible Adobe, les champs [!UICONTROL Société] et Suite [!UICONTROL de] rapports n’apparaissent pas lors de la sélection d’une source de rapports (NPR-32502).
* Lors de l’exportation de fragments d’expérience à l’aide des E/S Adobe, des métadonnées telles que le produit source ne sont pas exportées dans la Cible Adobe (NPR-32159).
* Les utilisateurs IMS autorisés du groupe d’administrateurs AEM local ne peuvent pas créer ni modifier de configurations IMS (NPR-33045).
* La page des configurations de lancement Adobe n&#39;affiche pas tous les enregistrements (NPR-33011).
* Les utilisateurs du groupe d’auteurs de contenu ne peuvent pas modifier les propriétés d’un composant de Cible Adobe en raison d’une erreur JavaScript (NPR-32996).

### Projets de traduction {#translation-6550}

* Les balises traduites ne sont pas importées dans AEM à partir de services de traduction tiers (NPR-33154).
* La page de configuration de traduction affiche un fournisseur de traduction incorrect par rapport à celui utilisé pour la traduction (NPR-32971).
* Ajouter un dossier de fragments d’expérience à un projet de traduction existant crée un nouveau projet (NPR-32843).
* Une `NullPointerException` erreur s&#39;affiche dans les journaux d&#39;exécution d&#39;une tâche de traduction (NPR-32628).

### WCM {#wcm-6550}

* Editeur de page : [!DNL Sites] l’éditeur de page ne permet pas aux utilisateurs utilisant uniquement le clavier d’accéder au contenu principal au lieu de déplacer la sélection de l’onglet dans toutes les options disponibles dans l’en-tête (CQ-4293883).
* Editeur de page : les panneaux qui utilisent le composant Well et incluent des données enregistrées ne s’affichent pas en raison de mises à jour dans [!DNL Chrome] et [!DNL Firefox] versions (CQ-4292995).
* MSM - La suppression d&#39;un composant de la page ne supprime pas le composant de la version publiée de la page (CQ-4292360).

### Brand Portal {#assets-brand-portal-6550}

* La suppression d’un schéma de métadonnées publié [!DNL Brand Portal] provoque une erreur (CQ-4292063).
* Si un administrateur configure [!DNL Experience Manager Assets] 6.5.4 avec Brand Portal via Adobe Developer Console, l’ [!DNL Brand Portal] utilisateur ne peut pas publier le fichier d’un dossier de contribution de [!DNL Brand Portal] à [!DNL Experience Manager]. (NPR-33046).
* Réplication Duplicata des dossiers parents à l’origine de conflits (NPR-33001).

### Communities {#communities-6550}

* Impossible de supprimer une carte dans la console de modération à l&#39;aide de l&#39;option de menu Edition rapide (NPR-33117).
* Une erreur se produit lors de l&#39;accès à la page [!UICONTROL Activité Stream] (NPR-33146).
* Les groupes supprimés sur l’instance d’auteur ne sont pas supprimés de toutes les instances de publication (NPR-33199).
* Les auteurs, après avoir créé un nouveau groupe, ne sont pas redirigés vers la section Groupe  communautaire le [!DNL Internet Explorer] 11 (NPR-33205).
* L’accès à un message dans la boîte de réception AEM ne modifie pas l’état du message en Lecture (NPR-32764).
* La modification d’un [!DNL Communities] groupe et de l’image miniature ne met pas à jour l’image miniature du groupe (NPR-32599).
* Un utilisateur ne peut pas envoyer de courrier électronique à un autre utilisateur d&#39;une communauté (NPR-32598).
* Un blog envoyé ne s&#39;affiche pas tant que l&#39;utilisateur n&#39;a pas actualisé la page (NPR-32391).
* Lors de la création d’une version de notifications et d’abonnements de contenu généré par l’utilisateur (UGC), un ID incorrect de la page source est stocké (CQ-4279355, CQ-4289703).

### Workflow {#workflow-6550}

* Le chargement de l’option [!UICONTROL Chronologie] dans le rail de gauche prend plus de temps que prévu (NPR-32851).
* Après le redémarrage d’une instance AEM, le courrier électronique de la tâche de révision d’une collection contient un lien de charge utile incorrect (NPR-32774).

### Forms {#forms-6550}

>[!NOTE]
>
>Le Service Pack AEM n’inclut pas de correctifs pour AEM Forms. Les correctifs sont fournis à l’aide d’un module complémentaire Forms distinct.  En outre, un programme d’installation cumulatif est publié, qui comprend des correctifs pour AEM Forms sur JEE. For more information, see [Install AEM Forms add-on](#install-aem-forms-add-on-package) and [Install AEM Forms on JEE](#install-aem-forms-jee-installer).

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

* AEM 6.5.5.0 requires AEM 6.5. Check [upgrade documentation](/help/sites-deploying/upgrade.md) for detailed instructions.
* Le Service Pack peut être téléchargé sur Adobe Package Share, accessible directement depuis l’instance AEM 6.5.
* Lors d’un déploiement avec MongoDB et plusieurs instances, installez AEM 6.5.5.0 sur l’une des instances d’auteur à l’aide du gestionnaire de modules.
* Avant l’installation, effectuez un instantané ou une nouvelle sauvegarde de votre instance AEM.
* Redémarrez l’instance avant l’installation. Cela est nécessaire uniquement lorsque l’instance reste en mode de mise à jour (ce qui est le cas lorsque l’instance vient d’être mise à jour depuis une version antérieure). Toutefois, cela est recommandé si l’instance s’est exécutée pendant une longue durée.

>[!NOTE]
>
>Adobe recommande de ne pas supprimer ni désinstaller le package AEM 6.5.5.0.

### Installation du Service Pack {#install-service-pack}

Accomplissez les étapes suivantes pour installer le Service Pack sur une instance 6.5 existante :

1. Cliquez sur le lien Partage [de](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/AEM-6.5.5.0-Service-Pack) package ou Distribution [de](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.5.zip) logiciels pour télécharger le package.

1. Ouvrez [Package Manager](http://localhost:4502/crx/packmgr/index.jsp) et cliquez sur **Télécharger le package** pour télécharger le package.

1. Sélectionnez le nom du package et cliquez sur **Installer**.

>[!NOTE]
>
>**La boîte de dialogue sur l’interface utilisateur de Package Manager se ferme parfois de manière impromptue lors de l’installation de la version 6.5.5.0**
>
>Il est donc recommandé d’attendre que les journaux d’erreurs se stabilisent avant d’accéder à l’instance. L’utilisateur doit attendre les journaux spécifiques liés à la désinstallation du lot de mise à jour avant de s’assurer que les installations sont réussies. Cela se produit généralement sur Safari, mais peut se produire par intermittence sur n’importe quel navigateur.

**Installation automatique**

Il existe deux manières d’installer automatiquement AEM 6.5.5.0 dans une instance en cours d’exécution :

R. Placez le package dans `../crx-quickstart/install ` un dossier pendant que le serveur est disponible en ligne. Le package est automatiquement installé.

B. Use the [HTTP API from Package Manager](https://docs.adobe.com/content/docs/en/crx/2-3/how_to/package_manager.html) - make sure that you use `cmd=install&recursive=true` - so the nested packages  are  installed.

>[!NOTE]
>
>AEM 6.5.5.0 ne prend pas en charge l’installation de Bootstrap.

**Validation de l’installation**

1. La page Informations sur le produit (/system/console/ productinfo) affiche la chaîne de version mise à jour `Adobe Experience Manager, Version 6.5.5.0` sous Produits installés.

1. All  OSGi  bundles are either **[!UICONTROL ACTIVE]** or **[!UICONTROL FRAGMENT]** in the OSGi Console (Use Web Console: /system/console/bundles).
1. The OSGI bundle `org.apache.jackrabbit.oak-core` is on version 1.10.6 or higher (Use Web Console: `/system/console/bundles`).

In order to see what platforms are certified to run with this release, please refer to the [Technical Requirements](/help/sites-deploying/technical-requirements.md).

### Installation du module complémentaire AEM Forms {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Passez cette étape si vous n’utilisez pas AEM Forms. Les correctifs dans AEM Forms sont fournis dans un module complémentaire distinct.

1. Vérifiez que vous avez installé le Service Pack AEM.
1. Download the corresponding Forms add-on package listed at [AEM Forms releases](https://helpx.adobe.com/fr/aem-forms/kb/aem-forms-releases.html) for your operating system.
1. Install the Forms add-on package as described in [Installing AEM Forms add-on packages](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

### Install AEM Forms on JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Passez cette étape si vous n’utilisez pas AEM Forms sous JEE. Les correctifs d’AEM Forms sur JEE sont diffusés par le biais d’un programme d’installation distinct.

For information about installing the cumulative installer for AEM Forms on JEE and post-deployment configuration, see the [release notes for patch 0014](https://helpx.adobe.com/aem-forms/quick-fixes/6-5/jee-patch-0014.html).

### UberJar {#uber-jar}

The UberJar for AEM 6.5.5.0 is available in the [Adobe Public Maven repository](https://repo.adobe.com/nexus/content/groups/public/com/adobe/aem/uber-jar/6.5.5/).

To use UberJar in a Maven project, refer to the article, [How to use UberJar](/help/sites-developing/ht-projects-maven.md) and include the following dependency in your project POM:

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
| Intégrations | The **[!UICONTROL AEM Cloud Services Opt-In]** screen has been deprecated. Avec l’intégration d’AEM et de Cible mise à jour dans AEM 6.5 pour la prise en charge de l’API Cible Standard, qui utilise l’authentification via Adobe IMS et E/S, et le rôle croissant de Adobe Launch pour l’instrumentation des pages AEM pour l’analyse et la personnalisation, l’assistant d’inclusion est devenu fonctionnellement inapproprié. | Configurez les connexions système, l’authentification Adobe IMS et les intégrations d’E/S Adobe via les services cloud AEM correspondants. |

## Problèmes connus {#known-issues}

* Si vous installez [!DNL Experience Manager] 6.5.5.0 avec [!DNL Java] 11, redémarrez le serveur après avoir installé le Service Pack. Aucun redémarrage n&#39;est nécessaire si vous installez le Service Pack avec [!DNL Java] 8.

* Si un dossier de la hiérarchie est renommé dans [!DNL Experience Manager Assets] et que le dossier imbriqué contenant une ressource est publié dans [!DNL Brand Portal], le titre du dossier n’est pas mis à jour dans [!DNL Brand Portal] le dossier racine tant que celui-ci n’a pas été republié.

* La mise à jour de [!DNL chrome] la version 83 pose un problème lors de la création de packs. Utilisez d’autres navigateurs disponibles, tels que [!DNL Internet Explorer] et [!DNL Firefox], ou d’autres options d’installation de package standard d’AEM pour résoudre le problème.

* Impossible d&#39;envoyer un courrier électronique au serveur SMTP distant à l&#39;aide de l&#39;expéditeur de courrier par défaut d&#39;AEM, car il permet uniquement la communication à l&#39;aide de TLS v1.2. Supprimez le lot `javax.mail:mail:1.5.0-b01` de `system/console` et actualisez les lots pour résoudre le problème.

* Lorsqu’un utilisateur sélectionne pour la première fois un champ dans un formulaire adaptatif, l’option permettant d’enregistrer une configuration ne s’affiche pas dans le navigateur de propriétés. La sélection pour configurer un autre champ du formulaire adaptatif dans le même éditeur résout le problème.

* Si l’assistant de configuration [!UICONTROL des ressources] connectées renvoie un message d’erreur 404 après l’installation, réinstallez manuellement les `cq-remotedam-client-ui-content` packages et `cq-remotedam-client-ui-components` packages à l’aide de Package Manager.

* Les erreurs et messages d’avertissement suivants peuvent s’afficher lors de l’installation d’AEM 6.5.x.x :
   * « Lorsque l’intégration de Target est configurée dans AEM à l’aide de l’API Target Standard (authentification IMS), l’exportation de fragments d’expérience vers Target entraîne la création de types d’offres incorrects. Au lieu du type « Fragment d’expérience » / source « Adobe Experience Manager », Target crée plusieurs offres avec le type « HTML » / source « Adobe Target Classic ».
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: Aucune fenêtre de maintenance n’a été trouvée sur granite/operations/maintenance.
   * La validation côté serveur du formulaire adaptatif échoue lorsque des fonctions d’agrégat telles que SUM, MAX et MIN sont utilisées. CQ-4274424
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Aucune fenêtre de maintenance n’a été trouvée sur granite/operations/maintenance.
   * La zone réactive d’une image interactive de média dynamique n’est pas visible lors de la prévisualisation du fichier via la visionneuse de bannières modifiables.

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

