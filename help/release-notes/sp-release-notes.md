---
title: '[!DNL Adobe Experience Manager] 6.5 Notes de mise à jour du Service Pack'
description: Release notes specific to [!DNL Adobe Experience Manager] 6.5 Service Pack 7.
docset: aem65
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 34e41cf5984f5f69ae0ccead137fe4f180bd84ad
workflow-type: tm+mt
source-wordcount: '3787'
ht-degree: 5%

---


# [!DNL Adobe Experience Manager]Notes de mise à jour de la version 6.5 du Service Pack {#aem-service-pack-release-notes}

## Informations sur la version {#release-information}

| Produits | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Version | 6.5.7.0 |
| Type | Version du Service Pack |
| Date | 26 novembre 2020 |
| URL de téléchargement | [Distribution de logiciels](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.7.zip) |

<!-- TBD: Update the SD link when SP7 is available. -->

## What&#39;s included in [!DNL Adobe Experience Manager] 6.5.7.0 {#what-s-included-in-aem}

[!DNL Adobe Experience Manager] La version 6.5.7.0 est une mise à jour importante qui comprend de nouvelles fonctionnalités, des améliorations clés demandées par les clients et des améliorations des performances, de la stabilité et de la sécurité, publiées depuis la version 6.5 d’avril 2019. Le Service Pack est installé sur la [!DNL Adobe Experience Manager] version 6.5.

Les principales fonctionnalités et améliorations introduites dans la [!DNL Adobe Experience Manager] version 6.5.7.0 comprennent :

* Tri des pages Live Copy disponibles pour le déploiement à l’aide des propriétés [!UICONTROL Name], [!UICONTROL Last Modified date,] and [!UICONTROL Last rollout date] .

* L’exécution des déplacements de page et des déploiements MSM en tant qu’opérations asynchrones afin de réduire leur impact sur les performances d’exécution.

* Les utilisateurs peuvent trier les fichiers numériques dans les vues Carte et Colonne.

* [!DNL Assets] et [!DNL Dynamic Media] offrent plusieurs améliorations d’accessibilité. Les améliorations concernent la navigation au clavier, l’utilisation de lecteurs d’écran et l’utilisation d’une technologie d’assistance similaire (AT). Voir [[!DNL Assets] Améliorations](#assets-6570) et [[!DNL Dynamic Media] améliorations](#dynamic-media-6570).

* Le référentiel intégré (Apache Jackrabbit Oak) a été mis à niveau vers la version 1.22.5.

Pour obtenir une liste complète des fonctionnalités et améliorations introduites dans la [!DNL Experience Manager] version 6.5.7.0, voir [Nouveautés de [!DNL Adobe Experience Manager] 6.5 Service Pack 7](new-features-latest-service-pack.md).

Voici la liste des correctifs fournis dans la [!DNL Experience Manager] version 6.5.7.0.

### [!DNL Sites] {#sites-6570}

* Lorsque vous ouvrez l&#39;option [!UICONTROL Dépassement de délai] pour une page, que vous gardez ouverte l&#39;option de rail latéral Chronologie et que vous accédez à la console [!UICONTROL Sites] , l&#39; `Failed to Load` erreur se produit (NPR-34951).

* L’option [!UICONTROL Retrait] temporel n’affiche pas les images pour la période et la période sélectionnées (NPR-34951).

* Lorsqu’un filtre appelle `getHeader()` à partir d’une page contenant un fragment de contenu, l’ `java.lang.AbstractMethodError` erreur se produit (NPR-34942).

* Lorsque le chemin d&#39;accès d&#39;une page contient plusieurs sous-chaînes de contenu, le rendu des prévisualisations échoue et la fonction de comparaison de version échoue également (NPR-34740).

* Lorsque vous définissez une valeur numérique pour la propriété d’étiquette de `String` type d’un composant, vous pouvez supprimer le composant et annuler l’opération de suppression. Cependant, après avoir annulé la suppression, la propriété label passe de `String` à `Long` (NPR-34739).

* L’exception suivante survient lors de l’ajout d’un fragment d’expérience basé sur un modèle avec une mise en page verrouillée à une page (NPR-34632) :

   ```TXT
   org.apache.sling.api.SlingException: Cannot get DefaultSlingScript: org.apache.sling.api.SlingException: Cannot get DefaultSlingScript: org.mozilla.javascript.EcmaError: TypeError: Cannot call method "getChildren" of null
   ```

* Lorsque vous déplacez un dossier, cela entraîne des problèmes de traversée et l&#39;erreur suivante se produit (NPR-34554) :

   ```TXT
   org.apache.sling.api.SlingException: Cannot get DefaultSlingScript. org.apache.jackrabbit.oak.query.RuntimeNodeTraversalException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped
   ```

* Lorsque de nouveaux actifs sont créés, publiés et déplacés vers un nouvel emplacement, le processus `Request to complete move operation` est créé et l’état Abandonné est généré. Le téléchargement d’une nouvelle ressource et l’exécution d’une `move` opération entraînent la création du `Request to complete move operation` flux de travaux dans l’état en attente (NPR-34543).

* Lorsque vous exportez un fragment d’expérience de [!DNL Experience Manager] 6.5.2 vers [!DNL Target] Standard, l’appel d’API échoue car la propriété workspace n’est pas disponible pour [!DNL Target] Standard (NPR-34557).

* Les utilisateurs ne peuvent pas publier de pages via l’option [!UICONTROL gérer la publication] , car l’option [!UICONTROL Publier] disparaît (NPR-34542).

* Lorsque vous ajoutez des styles au texte, une `<div>` balise est ajoutée au texte et le style ne peut plus être appliqué au texte (NPR-34531).

* Lorsque vous sélectionnez un élément dans un menu contextuel et mettez à jour les fichiers requis, il n&#39;est pas possible d&#39;enregistrer des valeurs de boîte de dialogue, car l&#39;autre menu comporte un champ obligatoire vide (NPR-34529).

* Lorsque vous créez une page à partir d&#39;un modèle personnalisé et que vous la déplacez dans la hiérarchie du plan, les composants supprimés précédemment des débuts de page s&#39;affichant sur la page dans la hiérarchie de la copie dynamique (NPR-34527).

* Une fois qu’un style d’article est appliqué à un contenu, il ne peut plus être supprimé (NPR-34486).

* Toutes les copies en direct et les copies d’un fragment d’expérience pointent vers le même ID d’ [!DNL Adobe Target] offre (NPR-34469).

* Les éléments de liste à puces s&#39;affichent en plus de la liste numérotée (NPR-34455).

* L&#39;option Comparer à la source n&#39;affiche pas la différence entre la page source et la version modifiée d&#39;une page (NPR-34285).

* Lorsque vous supprimez une page, les détails du contrôle de version ne sont pas configurables (NPR-34159).

* Lorsqu’un utilisateur sélectionne l’option de boîte de dialogue [!UICONTROL Ouvrir la sélection] , la sélection du clavier se déplace vers le contrôle masqué présent sur la page (CQ-4307779, CQ-4293601).

* Lorsque vous déplacez un dossier publié sur l’auteur, les chemins d’accès aux dossiers ne sont pas mis à jour en conséquence sur l’instance de publication (CQ-4305144).

* Lorsqu’un utilisateur sélectionne la `Enter` touche de l’option [!UICONTROL Sélectionner tout] , la sélection du clavier ne passe pas à l’option [!UICONTROL Créer un contrôle] (CQ-4293599).

* Lorsque vous sélectionnez la `Esc` clé, la cible d’action n’est pas restaurée dans le contrôle parent (CQ-4293593, CQ-4293590).

* Amélioration de la conformité WCAG pour l’ [!DNL Sites] interface utilisateur et les composants principaux (CQ-4293448).

* [!UICONTROL Les fonctions de zoom] et d’ [!UICONTROL échelle] sont désactivées pour la [!DNL Sites Editor] page (CQ-4282353).

* Après avoir utilisé l’option Pivoter à droite, le lecteur d’écran arrête de narrer la rotation ou l’état de retournement actuel (CQ-4282128).

* Les boutons de la boîte de dialogue Terminé et Annuler la configuration comportent plusieurs taquets de tabulation (CQ-4274601).

* Le déplacement de pages portant un nom similaire au même niveau n&#39;est pas autorisé (NPR-35041).

* Après avoir sélectionné l’option Effacer (x), la sélection du clavier ne passe pas au champ [!UICONTROL Filtre] (CQ-4293581).

* Lorsque vous effectuez la mise à niveau vers [!DNL Experience Manager] 6.5.6.0, le comportement du système de paragraphe hérité change et ne fonctionne pas correctement (NPR-35117).

* Les utilisateurs du clavier ne peuvent pas déplacer la mise au point de l’onglet dans un ordre approprié après avoir sélectionné la section [!UICONTROL Action] sur une [!DNL AEM Sites] page (CQ-4307786).

* Après avoir sélectionné une option dans la liste de menu de la cible de liens de la barre d’outils RTE lors de la modification d’un fragment de contenu, la boîte de dialogue de l’auteur du fragment de contenu s’début à clignoter (CQ-4305532).

* Les utilisateurs du clavier ne peuvent pas sélectionner les options de la liste déroulante Composant  Ajouté à l’aide de la touche Flèche vers le bas (CQ-4295097).

* La mise au point de l’onglet ne se déplace pas dans un ordre approprié lors de la sélection d’une date dans le menu Calendrier de l’onglet [!UICONTROL Ressources] d’une [!DNL Sites] page (CQ-4293600).

* L’onglet actif ne passe pas aux options suivantes ou précédentes pour les utilisateurs du clavier après la suppression des options de lien ou de texte disponibles lors de la modification d’une page de sites (CQ-4293597).

* Les utilisateurs du clavier ne peuvent pas revenir aux options Plus dans la section [!UICONTROL Actions] après avoir affiché les options disponibles et appuyé sur la `Esc` touche (CQ-4293592).

* Lorsque vous activez l’option [!UICONTROL Pivoter] pour une image en mode [!UICONTROL Edition] , la mise au point de l’onglet, au lieu de rester sur Pivoter, passe à l’option [!UICONTROL Rétablir] pour les utilisateurs du clavier (CQ-4293587).

* Dans la boîte de dialogue [!UICONTROL Ouvrir la sélection] disponible sur l’onglet [!UICONTROL Lien et actions] , la mise au point de l’onglet passe aux éléments masqués dans la page après l’option [!UICONTROL Annuler] (CQ-4293579).

* Lorsque les utilisateurs du clavier modifient une image, naviguent jusqu’à l’option [!UICONTROL Terminer] et appuient sur la touche Entrée, les lecteurs d’écran n’annoncent pas la fin (CQ-4282351).

* Les options Déplacer vers le haut et Déplacer vers le bas disponibles dans la boîte de dialogue [!UICONTROL Lien et Actions] ne sont pas disponibles pour le lecteur d’écran et les utilisateurs du clavier (CQ-4281120).

* Les utilisateurs du clavier ne peuvent pas restaurer la mise au point de l’onglet après avoir accédé à l’option Fermer (X) de la page [!UICONTROL Propriétés] (CQ-4293581, NPR-34653).

### [!DNL Assets] {#assets-6570}

[!DNL Adobe Experience Manager] La version 6.5.7.0 [!DNL Assets] résout les problèmes suivants et apporte les améliorations suivantes.

* Les améliorations suivantes ont été apportées à l’accessibilité dans [!DNL Experience Manager Assets]:

   * Lorsque vous naviguez dans la chronologie à l’aide du clavier, la `Esc` touche peut réduire l’option [!UICONTROL Afficher tout] sans perdre la cible d’action (CQ-4293598).
   * Lors de la navigation à l’aide de la touche de tabulation du clavier, après avoir supprimé la dernière balise des balises ajoutées, le champ de balise conserve la cible d’action (NPR-35109).
   * [!DNL Experience Manager] Les composants contiennent désormais les informations appropriées concernant le nom, le rôle et la valeur à utiliser par les lecteurs d’écran (NPR-34255).
   * Après avoir supprimé la zone de liste déroulante Type/Taille, la zone de liste déroulante Lien, la zone de liste déroulante Langue ou la zone d’édition Texte, la cible d’action du clavier revient aux éléments suivants ou précédents de l’interface utilisateur ou à un élément d’interface utilisateur plus pertinent (CQ-4293585).
   * Lorsque vous placez le pointeur de la souris sur diverses options, les conseils tels que Sélectionner et Télécharger s’affichent. Les utilisateurs qui utilisent un agrandissement de l’écran peuvent avoir des difficultés à afficher les miniatures de fichier en raison du contenu affiché en raison du survol. Il est maintenant possible de conserver la cible d’action, après avoir supprimé l’option à l’aide d’une `Escape` clé (CQ-4293554).
   * Lors de la sélection d’une cellule de grille dans la grille présente dans la page, la sélection se déplace vers la barre d’actions qui s’affiche à l’écran (CQ-4282127).
   * Les utilisateurs visuels peuvent faire la différence entre un texte normal et un lien, car des indices visuels (soulignement et icône en chevron) s’affichent pour les liens vers toutes les solutions de la [!DNL Experience Manager] page d&#39;accueil (CQ-4282072).

* L’amélioration de l’expérience utilisateur suivante est réalisée dans [!DNL Assets]:

   * Activez le tri des fichiers dans la vue de cartes et la vue de colonnes (NPR-35097).

* Après la mise à niveau vers la version 6.5, si un fichier JSON est généré à l’aide de l’API HTTP Assets, le codage utilisé dans le fichier (NPR-35129) pose problème.

* Les utilisateurs d’un groupe qui n’est pas autorisé à créer des collections (l’option Créer une collection n’est pas disponible) peuvent toujours créer des collections en accédant directement à l’URL `https://[aem_server]:[port]/mnt/overlay/dam/gui/content/collections/createcollectionwizard.html/content/dam/collections?contentPath=/content/dam/collections` (NPR-35115).

* Lorsqu’ils sont triés par nom, les fichiers recherchés sont triés en fonction de la casse. Cela crée deux listes triées distinctes en fonction de la casse qui apparaît de manière ordonnée dans les résultats de la recherche (NPR-35068).

* Lorsqu’un fragment de contenu est ouvert dans l’éditeur, les messages d’avertissement (`Invalid value specified for a metadata property`) sont consignés dans les journaux d’erreurs (NPR-35012).

* Les utilisateurs dépourvus de droits d’administrateur peuvent modifier des fichiers expirés à l’aide de l’application de bureau [Experience Manager] . (NPR-34993).

* Lorsque le même fichier est déplacé sur l’interface utilisateur Ressources et qu’une nouvelle version est créée, les modifications apportées aux métadonnées ne sont pas persistantes (NPR-34940).

* Lors de la modification de collections, un utilisateur peut supprimer le titre de la collection et enregistrer les modifications (NPR-34889).

* Lors du téléchargement d’une image de duplicata, une option de suppression est présentée. La sélection de la suppression permet de télécharger les images. Le processus de mise à jour des actifs de gestion des actifs est également déclenché (NPR-34744).

* Lorsque vous utilisez [!DNL Adobe Asset Link] avec [!DNL Adobe InDesign], les résultats de la recherche ne contiennent pas de dossiers et de collections, mais uniquement des fichiers (NPR-34699, CQ-4303666).

* Placer le pointeur sur la vue de la carte permet de faire défiler l’écran lorsque l’utilisateur se concentre (automatiquement) sur les actions rapides disponibles dans la carte (NPR-34514).

* Lors de la modification des propriétés de plusieurs fichiers en bloc, la sélection de l’option [!UICONTROL Enregistrer] ferme la vue d’éditeur en bloc et redirige vers la [!DNL Assets] page principale. Ce comportement est identique à celui de l’option [!UICONTROL Enregistrer et fermer] et n’est pas attendu (NPR-34546).

* La collection dynamique ne présente pas le paramètre d’interface utilisateur correct après l’enregistrement. La requête est enregistrée correctement, mais l&#39;interface affiche toujours le dernier prédicat d&#39;option ajouté (NPR-34539).

* Lors de l’ajout de fichiers à [!DNL Experience Manager], les métadonnées sans espace de nommage ne sont pas importées (NPR-34530).

* Lorsque vous faites glisser un fichier sur un dossier pour le déplacer, l’interface utilisateur affiche également l’option [!UICONTROL Déposer dans Lightbox] et [!UICONTROL Déposer dans la collection]. Même si l&#39;opération de déplacement est annulée, l&#39;interface utilisateur continue d&#39;afficher les deux dernières options (NPR-34526).

* Le symbole `%>` s’affiche sur la page des collections (NPR-34499).

* Dans la vue de colonne, [!DNL Assets] affiche les noms des dossiers et des fichiers du duplicata lorsque vous faites défiler vers le haut ou vers le bas avant que tous les fichiers ne s’affichent (NPR-34464).

* Si vous créez un dossier privé immédiatement après avoir créé un dossier public, ce dernier utilise les paramètres du dossier privé (NPR-34415).

* Dans la vue de carte, les cartes ne sont pas répertoriées par ordre alphabétique et les cartes ne peuvent pas être triées par ordre alphabétique (NPR-34234).

* Lors de la réouverture de règles en cascade, les choix ne sont pas conservés dans l’interface utilisateur (CQ-4301452).

#### [!DNL Dynamic Media] {#dynamic-media-6570}

* Les principales améliorations suivantes ont été apportées à l’accessibilité dans [!DNL Dynamic Media] (CQ-4290306). Pour plus d&#39;informations, reportez-vous à la page Fonctionnalités d&#39;accessibilité dans [!DNL Dynamic Media].  <!-- TBD: link to DM content post GA -->

   * Les lecteurs d’écran (JAWS, Narrateur) indiquent le nom, le rôle et l’état des éléments de menu dans l’option de menu Taille d’incorporation (CQ-4290927).
   * Les utilisateurs peuvent naviguer dans la boîte de dialogue Lien d’adresse électronique à l’aide de la `Tab` touche (CQ-4290926).
   * Le flux de travail permettant de créer des profils de codage vidéo est plus facile à utiliser en raison de l’amélioration du lecteur d’écran (CQ-4290623, CQ-4290622).
   * Lorsque vous naviguez à l’aide de `Tab` la touche, la cible d’action se déplace vers les éléments d’interface utilisateur appropriés dans le processus pour créer une vidéo interactive (CQ-4290621, CQ-4290620, CQ-4290619).
   * La page Publier, la page Modifier un fichier, la page Modifier les cultures dynamiques et la page Editeur de visionneuse d’images sont améliorées pour répondre aux normes Web. Les utilisateurs de la technologie d’assistance (AT) peuvent désormais naviguer facilement dans ces pages et prendre des mesures telles que recadrer des images (CQ-4290617, CQ-4290616, CQ-4290613, CQ-4290612, CQ-49 0610, CQ-4290614).
   * Les lecteurs sont améliorés pour permettre aux utilisateurs de naviguer à l’aide du clavier (CQ-4290615).
   * Les utilisateurs du clavier et des lecteurs d’écran peuvent utiliser la fonctionnalité de recadrage (CQ-4290609).
   * Les utilisateurs du clavier peuvent mieux gérer les zones réactives (CQ-4290604, CQ-4290603).

* Les jeux d&#39;images distants ne sont pas modifiables dans [!DNL Experience Manager] le cas où le nom de la société et le nom du dossier sont identiques (NPR-31340).

* L’ordre d’index z est incorrect lorsque vous tentez de prévisualisation la sortie après l’ajout d’une zone réactive à une [!DNL Dynamic Media] image ou après la modification d’une [!DNL Dynamic Media] vidéo ou [!DNL Experience Fragment] d’une image (CQ-4307267).

* [!DNL Dynamic Media] la synchronisation échoue lorsque des visionneuses de supports mixtes sont retraitées (CQ-4307184).

* Si une ressource est déplacée dans un dossier sur lequel la synchronisation automatique à [!DNL Dynamic Media] est configurée, la ressource ne se synchronise pas (CQ-4307122).

* [!DNL Dynamic Media] La lecture de la vidéo n’est pas effectuée sur les appareils iOS dotés des commandes vidéo HTML5 natives (CQ-4306977, CQ-4306727).

* Impossible de télécharger les images sur lesquelles SmartCrop est appliqué (CQ-4304558).

* Impossible de publier des dossiers de manière sélective dans Contenu multimédia dynamique (CQ-4304526).

* L’annulation de la publication d’un fichier vidéo [!DNL Experience Manager] n’annule pas la publication de la visionneuse de vidéos adaptative à partir d’un déploiement Scene7 configuré (CQ-4304405).

* Si vous Ajoutez un fichier d’image panoramique dans un composant de support panoramique et actualisez la page, une `Uncaught ReferenceError: $ is not defined` erreur se produit (CQ-4302810).

* Dans l’éditeur [!UICONTROL de paramètres prédéfinis de la]visionneuse, lors de la modification du paramètre prédéfini [!UICONTROL PanoramicImage/PanoramicImage_VR] , dans le `PanoramicView` composant, l’étiquette `PANORAMICVIEW_AUTOROTATE` de modificateur n’est pas disponible (CQ-4302443).

* Les légendes de vidéo ne s’affichent pas si la vidéo n’est pas la première d’une visionneuse de supports variés (CQ-4298161).

* La visionneuse de catalogue électronique HTML5 sur les périphériques mobiles iPhone ne peut pas tourner les pages ni retourner les pages (CQ-4296611).

* Lors du défilement de nuances sur un périphérique mobile, les nuances défilent vers la droite et hors de la zone visible pendant quelques secondes avant de revenir à la vue (CQ-4296439).

* Lorsqu’un enregistrement de Principal de paramètre prédéfini de visionneuse est créé, le fichier CSS et l’illustration ne sont pas publiés et seul le paramètre prédéfini de visionneuse est publié (CQ-4262205).

* Lorsque vous tentez de lier un fragment d’expérience pour une zone réactive donnée dans le composant Vidéo/Images  interactives, le chemin d’accès au fragment d’expérience sélectionné n’est pas affiché. Elle renvoie plutôt une valeur vide du champ de chemin (NPR-35146, CQ-4298136).

* Impossible de prévisualisation d’un fragment d’expérience dans l’éditeur IVV (CQ-4308560).

* Lors de l’ajout d’une zone réactive à une image et de la sélection d’un fragment d’expérience, il n’est pas possible de sélectionner les sous-dossiers et les variantes du fragment d’expérience (CQ-4307455).

* Les ressources autres que les images ne s’affichent pas comme publiées après le téléchargement (CQ-4306415).

#### [!DNL Experience Manager] Fichiers 3D {#three-d-assets-6570}

* `DAM CQ MIME Type` applique des types MIME incorrects aux actifs 3D, ce qui entraîne un rendu incorrect (NPR-34731).

### [!DNL Commerce] {#commerce-6570}

* L&#39;interface utilisateur de collecte de produits Commerce ne liste pas plus de 15 produits au sein d&#39;une collection (NPR-34502).

### Plate-forme {#platform-6570}

* Une session HTTP via HTTPS n&#39;est pas invalidée (NPR-35083).
* Un `NullPointerException` est renvoyé lors du démarrage de tâches de maintenance quotidiennes ou hebdomadaires à partir de l&#39;interface utilisateur (NPR-34953).
* Le validateur W3C signale des avertissements pour les fichiers JavaScript de bibliothèque client conformes (NPR-34898).
* La `AudienceOmniSearchHandler` fonction utilise un index obsolète (NPR-34870).
* La déconnexion du Experience Manager n&#39;efface pas les cookies (NPR-34743).
* La `findByTitle` fonction de l’ `TagManager` API ne fonctionne pas si le nom de balise contient un caractère spécial (NPR-34357).
* Le processus d&#39;importation du package de synchronisation des utilisateurs échoue (NPR-34399).
* Prise en charge Ajoutée du `ariaLabel` composant `ariaLabelledby` et des `Coral.Masonry` propriétés (GRANITE-29962).
* Le cache du répartiteur n’est pas actualisé pour les pages contenant des fragments de contenu après l’installation des derniers packages de composants principaux (CQ-4306788).
* Les noms de balises localisés avec guillemets (`"`) ne s’affichent pas correctement dans l’interface utilisateur (CQ-4305439).

### Interface utilisateur {#ui-6570}

* Le champ [!UICONTROL Lien vers] dans les propriétés du composant affiche des suggestions de saisie semi-automatique qui ne correspondent pas à la chaîne spécifiée (NPR-34865).

* aem affiche le message d&#39;erreur suivant lorsque vous planifiez une période de maintenance quotidienne distribuée entre 2 jours (NPR-35280) :

   ```TXT
   ERROR The start time must precede (be less than) the end time
   ```

### Intégrations {#integrations-6570}

* La modification d&#39;une [!DNL Adobe Launch] configuration existante échoue (NPR-35045).
* Impossible d&#39;exporter [!DNL Experience Fragments] vers [!DNL Adobe Target] si vous utilisez la configuration et l&#39; [!DNL Adobe Target Standard] environnement IMS (NPR-34555).
* L&#39;option [!UICONTROL Créer] apparaît sur la page [!UICONTROL Audiences] lors de la navigation d&#39;un dossier vers la page [!UICONTROL Audiences] (NPR-35151).

### Sling {#sling-6570}

* La vérification d&#39;intégrité de connexion par défaut valide les informations d&#39;identification d&#39;un utilisateur qui n&#39;existe pas (NPR-34686).

### Projets de traduction {#translation-6570}

* Lors de l&#39;annulation d&#39;un projet de traduction dans [!DNL Experience Manager], la demande d&#39;annulation n&#39;est pas envoyée au fournisseur de traduction (NPR-34433).

### [!DNL Communities] {#communities-6570}

* Tous les cas de terminologie inéquitable dans le produit sont remplacés par des équivalents acceptés (NPR-34311).
* [!DNL Google+] est supprimée de la liste des options de partage sur les réseaux sociaux (NPR-33877).

### [!DNL Brand Portal] {#brandportal-6570}

* L’interface utilisateur ne répond pas lors de la sélection des ressources dans la Vue [!UICONTROL de] Liste (NPR-34728).

### [!DNL Forms] {#forms-6570}

>[!NOTE]
>
>[!DNL Experience Manager Forms] libère les packages de modules complémentaires une semaine après la date de publication prévue du [!DNL Experience Manager] Service Pack.

Pour plus d&#39;informations sur les mises à jour de sécurité, consultez la page [Bulletins de sécurité des](https://helpx.adobe.com/security/products/experience-manager.html)Experience Manager.

## Install 6.5.7.0 {#install}

**Configuration requise et informations supplémentaires**

* AEM 6.5.7.0 requires AEM 6.5. See [upgrade documentation](/help/sites-deploying/upgrade.md) for detailed instructions.
* Le téléchargement du Service Pack est disponible sur Adobe [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
* Lors d’un déploiement avec MongoDB et plusieurs instances, installez AEM 6.5.7.0 sur l’une des instances d’auteur à l’aide du gestionnaire de modules.

>[!NOTE]
>
>Adobe does not recommend removing or uninstalling the [!DNL Adobe Experience Manager] 6.5.7.0 package.

### Installation du Service Pack {#install-service-pack}

Effectuez les étapes suivantes pour installer le Service Pack sur une instance Adobe Experience Manager 6.5 existante :

1. Redémarrez l’instance avant l’installation si l’instance est en mode de mise à jour (ce qui est le cas lorsque l’instance a été mise à jour à partir d’une version antérieure). L’Adobe recommande également un redémarrage si le temps de fonctionnement actuel d’une instance est élevé.

1. Avant l&#39;installation, effectuez un instantané ou une nouvelle sauvegarde de votre instance de [Experience Manager] .

1. Téléchargez le Service Pack depuis [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.7.zip).

1. Open Package Manager and click **[!UICONTROL Upload Package]** to upload the package. Pour en savoir plus, voir [Package Manager](/help/sites-administering/package-manager.md).

1. Select the package and click **[!UICONTROL Install]**.

1. Pour mettre à jour le connecteur S3, arrêtez l’instance après l’installation du Service Pack, remplacez le connecteur existant par un nouveau fichier binaire fourni dans le dossier d’installation, puis redémarrez l’instance. See [Amazon S3 Data Store](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>La boîte de dialogue de l’interface utilisateur de Package Manager se ferme parfois lors de l’installation du Service Pack. Adobe vous recommande d’attendre que les journaux d’erreurs se stabilisent avant d’accéder au déploiement. Attendez les journaux spécifiques liés à la désinstallation du lot de mise à jour avant de vous assurer que l&#39;installation est réussie. Typically, this happens on [!DNL Safari] but can intermittently happen on any browser.

**Installation automatique**

Il existe deux manières d’installer automatiquement Adobe Experience Manager 6.5.7.0 sur une instance de travail :

R. Placez le package dans `../crx-quickstart/install` un dossier lorsque le serveur est disponible en ligne. Le package est automatiquement installé.

B. Utilisez l’API [HTTP de Package Manager](https://docs.adobe.com/content/docs/en/crx/2-3/how_to/package_manager.html). Utilisez `cmd=install&recursive=true` pour installer les packages imbriqués.

>[!NOTE]
>
>Adobe Experience Manager 6.5.7.0 ne prend pas en charge l’installation des Bootstrap.

**Validation de l’installation**

1. La page d’informations sur le produit (`/system/console/productinfo`) affiche la chaîne de version mise à jour `Adobe Experience Manager (6.5.7.0)` sous Produits installés.

1. All OSGi bundles are either **[!UICONTROL ACTIVE]** or **[!UICONTROL FRAGMENT]** in the OSGi Console (Use Web Console: `/system/console/bundles`).

1. Le lot OSGi `org.apache.jackrabbit.oak-core` est de la version 1.22.3 ou ultérieure (Utilisez la console Web : `/system/console/bundles`).

Pour connaître les plates-formes certifiées pour fonctionner avec cette version, voir les exigences [](/help/sites-deploying/technical-requirements.md)techniques.

### Installation du module complémentaire Adobe Experience Manager Forms {#install-aem-forms-add-on-package}

>[!NOTE]
>
>[!DNL Experience Manager Forms] libère les packages de modules complémentaires une semaine après la date de publication prévue du [!DNL Experience Manager] Service Pack.

>[!NOTE]
>
>Passez cette étape si vous n’utilisez pas AEM Forms. Les correctifs dans Adobe Experience Manager Forms sont fournis par le biais d’un module complémentaire distinct.

1. Assurez-vous d’avoir installé le Service Pack de Adobe Experience Manager.
1. Download the corresponding Forms add-on package listed at [AEM Forms releases](https://helpx.adobe.com/fr/aem-forms/kb/aem-forms-releases.html) for your operating system.
1. Install the Forms add-on package as described in [Installing AEM Forms add-on packages](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

### Installation de Adobe Experience Manager Forms on JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Passez cette étape si vous n’utilisez pas AEM Forms sous JEE. Les correctifs d’Adobe Experience Manager Forms on JEE sont diffusés par le biais d’un programme d’installation distinct.

For information about installing the cumulative installer for Experience Manager Forms on JEE and post-deployment configuration, see the [release notes](jee-patch-installer-65.md).

### UberJar {#uber-jar}

UberJar pour Experience Manager 6.5.7.0 est disponible dans le référentiel [](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.7/)Maven Central.

Pour utiliser UberJar dans un projet Maven, voir [comment utiliser UberJar](/help/sites-developing/ht-projects-maven.md) et inclure la dépendance suivante dans le POM de votre projet :

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.7</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar et les autres artefacts associés sont disponibles dans le référentiel Maven Central au lieu du référentiel Adobe Public Maven (`repo.adobe.com`). Le fichier UberJar principal est renommé `uber-jar-<version>.jar`. Donc, il n&#39;y a pas `classifier`, avec `apis` comme valeur, de balise `dependency` .

## Fonctionnalités obsolètes {#removed-deprecated-features}

Vous trouverez ci-dessous une liste de fonctionnalités marquées comme obsolètes avec la version [!DNL Experience Manager] 6.5.7.0. Les fonctionnalités sont marquées comme obsolètes initialement et ultérieurement dans une version ultérieure. Une autre option est généralement fournie.

Vérifiez si vous utilisez une fonction ou une fonctionnalité dans un déploiement. Par ailleurs, prévoyez de modifier la mise en oeuvre pour utiliser une autre option.

| Zone | Fonctionnalité | Remplacement |
|---|---|---|
| Intégrations | L’écran d’inclusion **[!UICONTROL des services]** AEM Cloud est obsolète. L’intégration des AEM et des Cibles étant mise à jour dans AEM 6.5 pour prendre en charge l’API Target Standard, qui utilise l’authentification via l’Adobe IMS et E/S, et le rôle croissant du lancement d’Adobe pour l’instrumentalisation de pages de données d’analyse et de personnalisation, l’assistant d’inclusion est devenu non pertinent du point de vue fonctionnel. | Configurez les connexions système, l’authentification IMS Adobe et les intégrations d’E/S Adobe via les services cloud AEM correspondants. |
| Connecteurs | L’Adobe JCR Connector for Microsoft SharePoint 2010 et Microsoft SharePoint 2013 est obsolète pour AEM 6.5. | N/A |

## Problèmes connus {#known-issues}

* Ignorez les erreurs suivantes dans le `error.log` fichier lors de l’installation de Experience Manager 6.5.7.0 :

   ```TXT
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)[com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy] :  Cannot register component (org.osgi.service.component.ComponentException: The component name 'com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy' has already been registered by Bundle 331 (com.day.cq.dam.cq-dam-core) as Component of Class com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy)
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)[com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy(1314)] : Could not load implementation object class com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy (java.lang.ClassNotFoundException: com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy not found by com.day.cq.dam.cq-dam-core [331])
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)[com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy(1316)] : Could not load implementation object class com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy (java.lang.ClassNotFoundException: com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy not found by com.day.cq.dam.cq-dam-core [331])
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)[com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy(1315)] : Could not load implementation object class com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy (java.lang.ClassNotFoundException: com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy not found by com.day.cq.dam.cq-dam-core [331])
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)BundleComponentActivator : Unexpected failure enabling component holder com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy (java.lang.IllegalStateException: Could not load implementation object class com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy)
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)BundleComponentActivator : Unexpected failure enabling component holder com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy (java.lang.IllegalStateException: Could not load implementation object class com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy)
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)[com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy] :  Cannot register component (org.osgi.service.component.ComponentException: The component name 'com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy' has already been registered by Bundle 331 (com.day.cq.dam.cq-dam-core) as Component of Class com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy)
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)[com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy] :  Cannot register component (org.osgi.service.component.ComponentException: The component name 'com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy' has already been registered by Bundle 331 (com.day.cq.dam.cq-dam-core) as Component of Class com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy)
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)BundleComponentActivator : Unexpected failure enabling component holder com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy (java.lang.IllegalStateException: Could not load implementation object class com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy)
   ```

* Si vous effectuez une mise à niveau de votre [!DNL Experience Manager] instance de la version 6.5 à la version 6.5.7.0, vous pouvez vue `RRD4JReporter` des exceptions dans le `error.log` fichier. Redémarrez l’instance pour résoudre le problème.

* Si vous installez [!DNL Experience Manager] 6.5 Service Pack 5 ou un Service Pack précédent sur [!DNL Experience Manager] 6.5, la copie d’exécution du modèle de flux de travaux personnalisé de vos ressources (créée dans `/var/workflow/models/dam`) est supprimée.
Pour récupérer votre copie d’exécution, l’Adobe recommande de synchroniser la copie au moment de la conception du modèle de flux de travail personnalisé avec sa copie au moment de l’exécution à l’aide de l’API HTTP :
   `<designModelPath>/jcr:content.generate.json`.

* Contactez le service à la clientèle d’Adobe si vous rencontrez des problèmes lors de la modification et de la création de règles en cascade dans l’éditeur [!UICONTROL Forms de métadonnées] de dossiers et l’éditeur [!UICONTROL de Schéma de métadonnées à l’aide de la boîte de dialogue] Définir une règle  . Les règles déjà créées et enregistrées fonctionnent comme prévu.

* If a folder in the hierarchy is renamed in [!DNL Experience Manager Assets] and the nested folder containing an asset is published to [!DNL Brand Portal], the title of the folder is not updated in [!DNL Brand Portal] until the root folder is published again.

* Lorsqu’un utilisateur sélectionne pour la première fois un champ dans un formulaire adaptatif, l’option permettant d’enregistrer une configuration ne s’affiche pas dans le navigateur de propriétés. La sélection pour configurer un autre champ du formulaire adaptatif dans le même éditeur résout le problème.

* Si l’assistant de configuration [!UICONTROL des ressources] connectées renvoie un message d’erreur 404 après l’installation, réinstallez manuellement les `cq-remotedam-client-ui-content` packages et `cq-remotedam-client-ui-components` packages à l’aide de Package Manager.

* Les erreurs et messages d’avertissement suivants peuvent s’afficher lors de l’installation de AEM 6.5.x.x :
   * « Lorsque l’intégration de Target est configurée dans AEM à l’aide de l’API Target Standard (authentification IMS), l’exportation de fragments d’expérience vers Target entraîne la création de types d’offres incorrects. Au lieu du type « Fragment d’expérience » / source « Adobe Experience Manager », Target crée plusieurs offres avec le type « HTML » / source « Adobe Target Classic ».
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: Aucune fenêtre de maintenance n’a été trouvée sur granite/operations/maintenance.
   * La validation côté serveur du formulaire adaptatif échoue lorsque des fonctions d’agrégat telles que SUM, MAX et MIN sont utilisées. CQ-4274424
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Aucune fenêtre de maintenance n’a été trouvée sur granite/operations/maintenance.
   * La zone réactive d’une image interactive Contenu multimédia dynamique n’est pas visible lors de la prévisualisation du fichier via la visionneuse de bannières modifiables.

## OSGi bundles and content packages included {#osgi-bundles-and-content-packages-included}

Les documents de texte suivants liste les lots OSGi et les packages de contenu inclus dans AEM 6.5.7.0 :

* [Liste des lots OSGi inclus dans AEM 6.5.7.0](assets/6570_bundles.txt)

* [Liste des packages de contenu inclus dans AEM 6.5.7.0](assets/6570_packages.txt)

## Sites Web restreints {#restricted-sites}

Ces sites Web ne sont accessibles qu&#39;aux clients. Si vous êtes client et avez besoin d’un accès, contactez votre responsable de compte Adobe.

* [Téléchargement du produit à l’adresse licensing.adobe.com](https://licensing.adobe.com/)
* Voir [comment contacter le service d’assistance](https://experienceleague.adobe.com/docs/customer-one/using/home.html)clientèle.

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] Notes de mise à jour 6.5](/help/release-notes/release-notes.md)
>* [[!DNL Experience Manager] page de produits](https://www.adobe.com/fr/marketing/experience-manager.html)
>* [[!DNL Experience Manager] 6.5 Documentation](https://experienceleague.adobe.com/docs/experience-manager-65.html)
>* Subscribe to [Adobe priority product updates](https://www.adobe.com/subscription/priority-product-update.html)

