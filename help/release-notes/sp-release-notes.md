---
title: '[!DNL Adobe Experience Manager]Notes de mise à jour de la version 6.5 du Service Pack '
description: Notes de mise à jour spécifiques à  [!DNL Adobe Experience Manager] 6.5 Service Pack 7
docset: aem65
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: a24b66506440eb2153d5589e8c79dbfafb24df66
workflow-type: tm+mt
source-wordcount: '4308'
ht-degree: 7%

---


# [!DNL Adobe Experience Manager]Notes de mise à jour de la version 6.5 du Service Pack {#aem-service-pack-release-notes}

## Informations sur la version {#release-information}

| Produits | [!DNL Adobe Experience Manager] 6,5 |
| -------- | ---------------------------- |
| Version | 6.5.7.0 |
| Type | Version du Service Pack |
| Date | 26 novembre 2020 |
| URL de téléchargement | [Distribution de logiciels](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.7.zip) |

<!-- TBD: Update the SD link when SP7 is available. -->

## Éléments inclus dans [!DNL Adobe Experience Manager] 6.5.7.0 {#what-s-included-in-aem}

[!DNL Adobe Experience Manager] La version 6.5.7.0 est une mise à jour importante qui comprend de nouvelles fonctionnalités, des améliorations clés demandées par les clients et des améliorations des performances, de la stabilité et de la sécurité, publiées depuis la version 6.5 d’avril 2019. Le Service Pack est installé sur [!DNL Adobe Experience Manager] 6.5.

Les principales fonctionnalités et améliorations introduites dans [!DNL Adobe Experience Manager] 6.5.7.0 comprennent :

* L’exécution des déplacements de page et des déploiements MSM en tant qu’opérations asynchrones afin de réduire leur impact sur les performances d’exécution.

* Les utilisateurs peuvent trier les fichiers numériques dans les vues Carte et Colonne.

* [!DNL Assets] et  [!DNL Dynamic Media] offrent plusieurs améliorations d’accessibilité. Les améliorations concernent la navigation au clavier, l’utilisation de lecteurs d’écran et l’utilisation d’une technologie d’assistance similaire (AT). Voir [[!DNL Assets] améliorations](#assets-6570) et [[!DNL Dynamic Media] améliorations](#dynamic-media-6570).

* [Modèle de données de formulaire ](../../help/forms/using/configure-data-sources.md#fdm-http-client-configuration) configuration du client HTTP pour optimiser les performances.

* [Disponibilité de l’option de réinitialisation pour chaque ](../../help/forms/using/resize-using-layout-mode.md#resize-components) composant en mode Disposition

* [!DNL Experience Manager] 6.5 Service Pack 7 Forms améliore les performances pour :

   * Validation des valeurs de champ sur le serveur lors de l’envoi d’un formulaire adaptatif.

   * Conversion d’un formulaire PDF en formulaire adaptatif à l’aide de [!DNL Automated Forms Conversion service].

* Prise en charge de Microsoft SQL Server 2019 dans [!DNL Experience Manager Forms].

* Le référentiel intégré (Apache Jackrabbit Oak) a été mis à niveau vers la version 1.22.5.

Pour une liste complète des fonctionnalités et améliorations introduites dans [!DNL Experience Manager] 6.5.7.0, voir [Nouveautés de  [!DNL Adobe Experience Manager] 6.5 Service Pack 7](new-features-latest-service-pack.md).

Voici la liste des correctifs fournis dans la version [!DNL Experience Manager] 6.5.7.0.

### [!DNL Sites] {#sites-6570}

* Lorsque vous ouvrez l&#39;option [!UICONTROL Timewrap] pour une page, que vous gardez ouverte l&#39;option de rail latéral Timeline et que vous accédez à la console [!UICONTROL Sites], l&#39;erreur `Failed to Load` se produit (NPR-34951).

* L’option [!UICONTROL Retenue du temps] n’affiche pas les images pour la période et la période sélectionnées (NPR-34951).

* Lorsqu&#39;un filtre appelle `getHeader()` à partir d&#39;une page contenant un fragment de contenu, l&#39;erreur `java.lang.AbstractMethodError` se produit (NPR-34942).

* Lorsque le chemin d&#39;accès d&#39;une page contient plusieurs sous-chaînes de contenu, le rendu des prévisualisations échoue et la fonction de comparaison de version échoue également (NPR-34740).

* Lorsque vous définissez une valeur numérique pour la propriété d&#39;étiquette de type `String` d&#39;un composant, vous pouvez supprimer le composant et annuler l&#39;opération de suppression. Cependant, après avoir annulé la suppression, la propriété d’étiquette passe de `String` à `Long` (NPR-34739).

* L’exception suivante survient lors de l’ajout d’un fragment d’expérience basé sur un modèle avec une mise en page verrouillée à une page (NPR-34632) :

   ```TXT
   org.apache.sling.api.SlingException: Cannot get DefaultSlingScript: org.apache.sling.api.SlingException: Cannot get DefaultSlingScript: org.mozilla.javascript.EcmaError: TypeError: Cannot call method "getChildren" of null
   ```

* Lorsque vous déplacez un dossier, cela entraîne des problèmes de traversée et l&#39;erreur suivante se produit (NPR-34554) :

   ```TXT
   org.apache.sling.api.SlingException: Cannot get DefaultSlingScript. org.apache.jackrabbit.oak.query.RuntimeNodeTraversalException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped
   ```

* Lorsque de nouveaux actifs sont créés, publiés et déplacés vers un nouvel emplacement, le flux de travaux `Request to complete move operation` est créé et le résultat est un état Abandonné. Le téléchargement d&#39;une nouvelle ressource et l&#39;exécution d&#39;une opération `move` entraînent la création du flux de travaux `Request to complete move operation` dans l&#39;état en attente (NPR-34543).

* Lorsque vous exportez un fragment d’expérience de [!DNL Experience Manager] environnement 6.5.2 vers [!DNL Target] Standard, l’appel d’API échoue car la propriété workspace n’est pas disponible pour [!DNL Target] Standard (NPR-34557).

* Les utilisateurs ne peuvent pas publier de pages via l&#39;option [!UICONTROL gérer la publication], car l&#39;option [!UICONTROL Publier] disparaît (NPR-34542).

* Lorsque vous ajoutez des styles au texte, une balise `<div>` est ajoutée au texte et le style ne peut plus être appliqué au texte (NPR-34531).

* Lorsque vous sélectionnez un élément dans un menu contextuel et mettez à jour les fichiers requis, il n&#39;est pas possible d&#39;enregistrer des valeurs de boîte de dialogue, car l&#39;autre menu comporte un champ obligatoire vide (NPR-34529).

* Lorsque vous créez une page à partir d&#39;un modèle personnalisé et que vous la déplacez dans la hiérarchie du plan, les composants supprimés précédemment des débuts de page s&#39;affichant sur la page dans la hiérarchie de la copie dynamique (NPR-34527).

* Une fois qu’un style d’article est appliqué à un contenu, il ne peut plus être supprimé (NPR-34486).

* Toutes les copies en direct et les copies d’un fragment d’expérience pointent vers le même [!DNL Adobe Target] ID d’offre (NPR-34469).

* Les éléments de liste à puces s&#39;affichent en plus de la liste numérotée (NPR-34455).

* L&#39;option Comparer à la source n&#39;affiche pas la différence entre la page source et la version modifiée d&#39;une page (NPR-34285).

* Lorsque vous supprimez une page, les détails du contrôle de version ne sont pas configurables (NPR-34159).

* Lorsqu’un utilisateur sélectionne l’option de boîte de dialogue [!UICONTROL Ouvrir la sélection], la sélection au clavier se déplace vers le contrôle masqué présent sur la page (CQ-4307779, CQ-4293601).

* Lorsque vous déplacez un dossier publié sur l’auteur, les chemins d’accès aux dossiers ne sont pas mis à jour en conséquence sur l’instance de publication (CQ-4305144).

* Lorsqu’un utilisateur sélectionne la touche `Enter` dans l’option [!UICONTROL Sélectionner tout], la sélection au clavier ne passe pas à l’option [!UICONTROL Créer un contrôle] (CQ-4293599).

* Lorsque vous sélectionnez la clé `Esc`, la cible d’action n’est pas restaurée dans le contrôle parent (CQ-4293593, CQ-4293590).

* Amélioration de la conformité WCAG pour l’interface utilisateur et les composants principaux [!DNL Sites] (CQ-4293448).

* [!UICONTROL Les fonctions de ] zoom et de   mise à l’échelle sont désactivées pour la  [!DNL Sites Editor] page (CQ-4282353).

* Après avoir utilisé l’option Pivoter à droite, le lecteur d’écran arrête de narrer la rotation ou l’état de retournement actuel (CQ-4282128).

* Les boutons de la boîte de dialogue Terminé et Annuler la configuration comportent plusieurs taquets de tabulation (CQ-4274601).

* Le déplacement de pages portant un nom similaire au même niveau n&#39;est pas autorisé (NPR-35041).

* Après avoir sélectionné l’option Effacer (x), la sélection du clavier ne passe pas au champ [!UICONTROL Filtre] (CQ-4293581).

* Lorsque vous effectuez la mise à niveau vers [!DNL Experience Manager] 6.5.6.0, le comportement du système de paragraphe hérité change et ne fonctionne pas correctement (NPR-35117).

* Les utilisateurs du clavier ne peuvent pas déplacer la mise au point de l’onglet dans l’ordre approprié après avoir sélectionné la section [!UICONTROL Action] sur une page [!DNL AEM Sites] (CQ-4307786).

* Après avoir sélectionné une option dans la liste de menu de la cible de liens de la barre d’outils RTE lors de la modification d’un fragment de contenu, la boîte de dialogue de l’auteur du fragment de contenu s’début à clignoter (CQ-4305532).

* Les utilisateurs du clavier ne peuvent pas sélectionner les options de la liste déroulante [!UICONTROL Ajouter le composant] à l’aide de la touche Flèche vers le bas (CQ-4295097).

* La mise au point de l’onglet ne se déplace pas dans un ordre approprié lors de la sélection d’une date dans le menu Calendrier sous l’onglet [!UICONTROL Ressources] d’une page [!DNL Sites] (CQ-4293600).

* L’onglet actif ne passe pas aux options suivantes ou précédentes pour les utilisateurs du clavier après la suppression des options de lien ou de texte disponibles lors de la modification d’une page de sites (CQ-4293597).

* Les utilisateurs du clavier ne peuvent pas revenir aux options Plus dans la section [!UICONTROL Actions] après avoir affiché les options disponibles et appuyé sur la touche `Esc` (CQ-4293592).

* Lorsque vous activez l’option [!UICONTROL Rotation] d’une image en mode [!UICONTROL Modifier], la mise au point de l’onglet, au lieu de rester sur Pivoter, passe à l’option [!UICONTROL Rétablir] pour les utilisateurs du clavier (CQ-4293587).

* Dans la boîte de dialogue [!UICONTROL Ouvrir la sélection] disponible sur l&#39;onglet [!UICONTROL Lien et actions], la mise au point de l&#39;onglet passe aux éléments masqués de la page après l&#39;option [!UICONTROL Annuler] (CQ-4293579).

* Lorsque les utilisateurs du clavier modifient une image, naviguent jusqu’à l’option [!UICONTROL Terminer] et appuient sur la touche Entrée, les lecteurs d’écran n’annoncent pas l’achèvement (CQ-4282351).

* Les options Déplacer vers le haut et Déplacer vers le bas disponibles dans la boîte de dialogue [!UICONTROL Lien et actions] ne sont pas disponibles pour le lecteur d’écran et les utilisateurs du clavier (CQ-4281120).

* Les utilisateurs du clavier ne peuvent pas restaurer la mise au point de l’onglet après avoir accédé à l’option Fermer (X) de la page [!UICONTROL Propriétés] (CQ-4293581, NPR-34653).

### [!DNL Assets] {#assets-6570}

[!DNL Adobe Experience Manager] La version 6.5.7.0  [!DNL Assets] corrige les problèmes suivants et apporte les améliorations suivantes.

* Les améliorations suivantes ont été apportées à l’accessibilité d’[!DNL Experience Manager Assets] grâce à cette version. Pour plus d’informations, voir [Fonctionnalités d’accessibilité d’ [!DNL Assets]](/help/assets/accessibility.md).

   * Lorsque vous naviguez dans la chronologie à l’aide d’un clavier, la touche `Esc` peut réduire l’option [!UICONTROL Afficher tout] sans perdre la cible d’action (CQ-4293598).
   * Lors de la navigation à l’aide de la touche de tabulation du clavier, après avoir supprimé la dernière balise des balises ajoutées, le champ de balise conserve la cible d’action (NPR-35109).
   * [!DNL Experience Manager] Les composants contiennent désormais les informations appropriées concernant le nom, le rôle et la valeur à utiliser par les lecteurs d’écran (NPR-34255).
   * Après avoir supprimé la zone de liste déroulante Type/Taille, la zone de liste déroulante Lien, la zone de liste déroulante Langue ou la zone d’édition Texte, la cible d’action du clavier revient aux éléments suivants ou précédents de l’interface utilisateur ou à un élément d’interface utilisateur plus pertinent (CQ-4293585).
   * Lorsque vous placez le pointeur de la souris sur des options, des conseils concernant par exemple les fonctions Sélectionner et Télécharger s’affichent. Il est possible que les utilisateurs de la loupe ne voient pas les miniatures des fichiers en raison de ces conseils. Il est désormais possible de conserver la sélection après avoir supprimé l’option à l’aide de la touche `Escape`. (CQ-4293554).
   * Lors de la sélection d’une cellule de grille dans la grille présente dans la page, la sélection se déplace vers la barre d’actions qui s’affiche à l’écran (CQ-4282127).
   * Les utilisateurs visuels peuvent faire la différence entre un texte normal et un lien, car des indices visuels (soulignement et icône en chevron) s’affichent pour les liens vers toutes les solutions dans la page d&#39;accueil [!DNL Experience Manager] (CQ-4282072).

* L’amélioration de l’expérience utilisateur suivante est réalisée dans [!DNL Assets] :

   * Activez le tri des fichiers dans la vue de cartes et la vue de colonnes (NPR-35097).

* Après la mise à niveau vers la version 6.5, si un fichier JSON est généré à l’aide de l’API HTTP Assets, le codage utilisé dans le fichier (NPR-35129) pose problème.

* Les utilisateurs d’un groupe qui n’est pas autorisé à créer des collections (l’option Créer une collection n’est pas disponible) peuvent toujours créer des collections en accédant directement à l’URL `https://[aem_server]:[port]/mnt/overlay/dam/gui/content/collections/createcollectionwizard.html/content/dam/collections?contentPath=/content/dam/collections` (NPR-35115).

* Lorsqu’ils sont triés par nom, les fichiers recherchés sont triés en fonction de la casse. Cela crée deux listes triées distinctes en fonction de la casse qui apparaît de manière ordonnée dans les résultats de la recherche (NPR-35068).

* Lorsqu’un fragment de contenu est ouvert dans l’éditeur, les messages d’avertissement (`Invalid value specified for a metadata property`) sont consignés dans les journaux d’erreurs (NPR-35012).

* Les utilisateurs dépourvus de droits d’administrateur peuvent modifier des actifs expirés à l’aide de l’application de bureau [Experience Manager]. (NPR-34993).

* Lorsque le même fichier est déplacé sur l’interface utilisateur Ressources et qu’une nouvelle version est créée, les modifications apportées aux métadonnées ne sont pas persistantes (NPR-34940).

* Lors de la modification de collections, un utilisateur peut supprimer le titre de la collection et enregistrer les modifications (NPR-34889).

* Lors du téléchargement d’une image de duplicata, une option de suppression est présentée. La sélection de la suppression permet de télécharger les images. Le processus de mise à jour des actifs de gestion des actifs est également déclenché (NPR-34744).

* Si vous utilisez [!DNL Adobe Asset Link] avec [!DNL Adobe InDesign], les résultats de la recherche ne contiennent pas de dossiers et de collections, mais uniquement des ressources (NPR-34699, CQ-4303666).

* Placer le pointeur sur la vue de la carte permet de faire défiler l’écran lorsque l’utilisateur se concentre (automatiquement) sur les actions rapides disponibles dans la carte (NPR-34514).

* Lors de la modification des propriétés de plusieurs actifs en bloc, la sélection de l&#39;option [!UICONTROL Enregistrer] ferme la vue d&#39;éditeur en bloc et redirige vers la page principale [!DNL Assets]. Ce comportement est identique à celui de l’option [!UICONTROL Enregistrer et fermer] et n’est pas attendu (NPR-34546).

* La collection dynamique ne présente pas le paramètre d’interface utilisateur correct après l’enregistrement. La requête est enregistrée correctement, mais l&#39;interface affiche toujours le dernier prédicat d&#39;option ajouté (NPR-34539).

* Lors de l’ajout de fichiers à [!DNL Experience Manager], les métadonnées sans espace de nommage ne sont pas importées (NPR-34530).

* Lorsque vous faites glisser un fichier sur un dossier pour le déplacer, l’interface utilisateur affiche également l’option [!UICONTROL Déposer dans Lightbox] et [!UICONTROL Déposer dans Collection]. Même si l&#39;opération de déplacement est annulée, l&#39;interface utilisateur continue d&#39;afficher les deux dernières options (NPR-34526).

* Le symbole `%>` s’affiche sur la page des collections (NPR-34499).

* Dans la vue de colonne, [!DNL Assets] affiche les noms de dossier et de fichier du duplicata lorsque vous faites défiler vers le haut et vers le bas avant que tous les fichiers ne s&#39;affichent (NPR-34464).

* Si vous créez un dossier privé immédiatement après avoir créé un dossier public, ce dernier utilise les paramètres du dossier privé (NPR-34415).

* Dans la vue de carte, les cartes ne sont pas répertoriées par ordre alphabétique et les cartes ne peuvent pas être triées par ordre alphabétique (NPR-34234).

* Lors de la réouverture de règles en cascade, les choix ne sont pas conservés dans l’interface utilisateur (CQ-4301452).

#### [!DNL Dynamic Media] {#dynamic-media-6570}

* Les améliorations suivantes ont été apportées à l’accessibilité dans [!DNL Dynamic Media] (CQ-4290306). Pour plus d&#39;informations, reportez-vous à la section [fonctionnalités d&#39;accessibilité dans  [!DNL Dynamic Media]](/help/assets/accessibility-dm.md).

   * Les lecteurs d’écran (JAWS, Narrateur) indiquent le nom, le rôle et l’état des éléments de menu dans l’option de menu Taille d’incorporation (CQ-4290927).
   * Les utilisateurs peuvent naviguer dans la boîte de dialogue Lien d’adresse électronique à l’aide de la clé `Tab` (CQ-4290926).
   * Le flux de travail permettant de créer des profils de codage vidéo est plus facile à utiliser en raison de l’amélioration du lecteur d’écran (CQ-4290623, CQ-4290622).
   * Lorsque vous naviguez à l’aide de la touche `Tab`, la cible d’action se déplace vers les éléments d’interface utilisateur appropriés dans le processus pour créer une vidéo interactive (CQ-4290621, CQ-4290620, CQ-4290619).
   * Les pages Publier, Modifier ressource, Modifier les recadrages intelligents et Éditeur de visionneuse d’images ont été améliorées pour répondre aux références standard du web. Les utilisateurs de la technologie d’assistance (AT) peuvent désormais naviguer facilement dans ces pages et prendre des mesures telles que recadrer des images (CQ-4290617, CQ-4290616, CQ-4290613, CQ-4290612, CQ-49 0610, CQ-4290614).
   * Les lecteurs sont améliorés pour permettre aux utilisateurs de naviguer à l’aide du clavier (CQ-4290615).
   * Les utilisateurs du clavier et des lecteurs d’écran peuvent utiliser la fonctionnalité de recadrage (CQ-4290609).
   * Les utilisateurs du clavier peuvent mieux gérer les zones réactives (CQ-4290604, CQ-4290603).

* Les jeux d&#39;images distants ne sont pas modifiables dans [!DNL Experience Manager] si le nom de la société et le nom du dossier sont identiques (NPR-31340).

* L’ordre d’index z est incorrect lorsque vous tentez de prévisualisation la sortie après avoir ajouté une zone réactive à une image [!DNL Dynamic Media] ou après avoir modifié une vidéo [!DNL Dynamic Media] ou une [!DNL Experience Fragment] avec une image (CQ-4307267).

* [!DNL Dynamic Media] la synchronisation échoue lorsque des visionneuses de supports mixtes sont retraitées (CQ-4307184).

* Si une ressource est déplacée dans un dossier sur lequel la synchronisation automatique vers [!DNL Dynamic Media] est configurée, la ressource ne se synchronise pas (CQ-4307122).

* [!DNL Dynamic Media] La lecture de la vidéo n’est pas effectuée sur les appareils iOS dotés des commandes vidéo HTML5 natives (CQ-4306977, CQ-4306727).

* Impossible de télécharger les images sur lesquelles SmartCrop est appliqué (CQ-4304558).

* Impossible de publier des dossiers de manière sélective sur Dynamic Media (CQ-4304526).

* L’annulation de la publication d’un fichier vidéo à partir de [!DNL Experience Manager] n’annule pas la publication de la visionneuse de vidéos adaptative à partir d’un déploiement Scene7 configuré (CQ-4304405).

* Si vous Ajoutez un fichier d’image panoramique dans un composant de support panoramique et actualisez la page, une erreur `Uncaught ReferenceError: $ is not defined` s’affiche (CQ-4302810).

* Dans l’[!UICONTROL éditeur de paramètres prédéfinis de la visionneuse], lors de la modification du paramètre prédéfini [!UICONTROL PanoramicImage/PanoramicImage_VR], dans le composant `PanoramicView`, l’étiquette de modificateur `PANORAMICVIEW_AUTOROTATE` n’est pas disponible (CQ-430243).

* Les légendes de vidéo ne s’affichent pas si la vidéo n’est pas la première d’une visionneuse de supports variés (CQ-4298161).

* La visionneuse de catalogue électronique HTML5 sur les périphériques mobiles iPhone ne peut pas tourner les pages ni retourner les pages (CQ-4296611).

* Lors du défilement de nuances sur un périphérique mobile, les nuances défilent vers la droite et hors de la zone visible pendant quelques secondes avant de revenir à la vue (CQ-4296439).

* Lorsqu’un enregistrement de Principal de paramètre prédéfini de visionneuse est créé, le fichier CSS et l’illustration ne sont pas publiés et seul le paramètre prédéfini de visionneuse est publié (CQ-4262205).

* Lorsque vous tentez de lier un fragment d’expérience pour une zone réactive donnée dans le composant [!UICONTROL Vidéo/Images interactives], le chemin d’accès au fragment d’expérience sélectionné n’est pas affiché. Elle renvoie plutôt une valeur vide du champ de chemin (NPR-35146, CQ-4298136).

* Impossible de prévisualisation d’un fragment d’expérience dans l’éditeur IVV (CQ-4308560).

* Lors de l’ajout d’une zone réactive à une image et de la sélection d’un fragment d’expérience, il n’est pas possible de sélectionner les sous-dossiers et les variantes du fragment d’expérience (CQ-4307455).

* Les ressources autres que les images ne s’affichent pas comme publiées après le téléchargement (CQ-4306415).

#### [!DNL Experience Manager] Fichiers 3D  {#three-d-assets-6570}

* `DAM CQ MIME Type` applique des types MIME incorrects aux actifs 3D, ce qui entraîne un rendu incorrect (NPR-34731).

### [!DNL Commerce] {#commerce-6570}

* L&#39;interface utilisateur de collecte de produits Commerce ne liste pas plus de 15 produits au sein d&#39;une collection (NPR-34502).

### Plate-forme {#platform-6570}

* Une session HTTP via HTTPS n&#39;est pas invalidée (NPR-35083).
* Un `NullPointerException` est renvoyé lors du démarrage de tâches de maintenance quotidiennes ou hebdomadaires à partir de l&#39;interface utilisateur (NPR-34953).
* Le validateur W3C signale des avertissements pour les fichiers JavaScript de bibliothèque client conformes (NPR-34898).
* La fonction `AudienceOmniSearchHandler` utilise un index obsolète (NPR-34870).
* La déconnexion du Experience Manager n&#39;efface pas les cookies (NPR-34743).
* La fonction `findByTitle` de l&#39;API `TagManager` ne fonctionne pas si le nom de la balise contient un caractère spécial (NPR-34357).
* Le processus d&#39;importation du package de synchronisation des utilisateurs échoue (NPR-34399).
* Prise en charge Ajoutée des propriétés `ariaLabel` et `ariaLabelledby` pour le composant `Coral.Masonry` (GRANITE-29962).
* Le cache du répartiteur n’est pas actualisé pour les pages contenant des fragments de contenu après l’installation des derniers packages de composants principaux (CQ-4306788).
* Les noms de balise localisés avec des guillemets (`"`) ne s’affichent pas correctement dans l’interface utilisateur (CQ-4305439).

### Interface utilisateur {#ui-6570}

* Le champ [!UICONTROL Lien vers ] des propriétés du composant affiche des suggestions de saisie automatique qui ne correspondent pas à la chaîne spécifiée (NPR-34865).

* aem affiche le message d&#39;erreur suivant lorsque vous planifiez une période de maintenance quotidienne distribuée entre 2 jours (NPR-35280) :

   ```TXT
   ERROR The start time must precede (be less than) the end time
   ```

### Intégrations {#integrations-6570}

* La modification d&#39;une configuration [!DNL Adobe Launch] existante échoue (NPR-35045).
* Impossible d&#39;exporter [!DNL Experience Fragments] vers [!DNL Adobe Target] si vous utilisez la configuration IMS et l&#39;environnement [!DNL Adobe Target Standard] (NPR-34555).
* L&#39;option [!UICONTROL Créer] apparaît sur la page [!UICONTROL Audiences] lors de la navigation entre un dossier et la page [!UICONTROL Audiences] (NPR-35151).

### Sling {#sling-6570}

* La vérification d&#39;intégrité de connexion par défaut valide les informations d&#39;identification d&#39;un utilisateur qui n&#39;existe pas (NPR-34686).

### Projets de traduction {#translation-6570}

* Lors de l&#39;annulation d&#39;un projet de traduction dans [!DNL Experience Manager], la demande d&#39;annulation n&#39;est pas envoyée au fournisseur de traduction (NPR-34433).

### [!DNL Communities] {#communities-6570}

* Tous les cas de terminologie inéquitable dans le produit sont remplacés par des équivalents acceptés (NPR-34311).
* [!DNL Google+] est supprimée de la liste des options de partage sur les réseaux sociaux (NPR-33877).

### [!DNL Brand Portal] {#brandportal-6570}

* L’interface utilisateur ne répond pas lors de la sélection des actifs dans la [!UICONTROL Liste Vue] (NPR-34728).

### [!DNL Forms] {#forms-6570}

>[!NOTE]
>
>[!DNL Experience Manager Forms] libère les packages de modules complémentaires une semaine après la date de publication prévue du  [!DNL Experience Manager] Service Pack.

>[!NOTE]
>
>[!DNL Experience Manager] Le Service Pack n’inclut pas de correctifs pour  [!DNL Forms]. Ils sont livrés à l’aide d’un module complémentaire [!DNL Forms] distinct. En outre, un programme d’installation cumulatif est publié, qui comprend des correctifs pour [!DNL Experience Manager Forms] sur JEE. Pour plus d’informations, voir [Installer le module complémentaire AEM Forms](#install-aem-forms-add-on-package) et [Installer AEM Forms on JEE](#install-aem-forms-jee-installer).

**Formulaires adaptatifs**

* Impossible de modifier un formulaire adaptatif à l’aide de l’interface utilisateur classique après l’application de [!DNL Experience Manager] Service Pack 6 (NPR-35126).

* Lorsque vous convertissez un fichier PDF en formulaire adaptatif, vous ne pouvez pas définir de valeur pour un panneau imbriqué à l’aide d’un modèle de données de formulaire sur la disposition à onglets. En outre, il existe des problèmes lors de la définition dynamique d’une valeur pour les groupes de boutons radio à l’aide d’un tableau statique à l’aide de l’éditeur de code (NPR-35062).

* Lorsque vous saisissez des caractères japonais dans un composant de champ de texte d’un formulaire adaptatif, vous pouvez spécifier plus de caractères que la limite maximale de 35 caractères (NPR-35039).

* Le formulaire adaptatif affiche des paramètres indésirables, tels que `owner` et `status`, sur la page **[!UICONTROL Merci]** affichée après l’envoi du formulaire (NPR-34989).

* La boîte de dialogue [!UICONTROL Sélection de fichier] du composant [!UICONTROL Pièce jointe] affiche également les types de fichier non pris en charge pour la sélection, ce qui entraîne une erreur lors de l’envoi du formulaire adaptatif (NPR-34970).

* Lorsque vous insérez un formulaire adaptatif dans une page [!DNL Experience Manager Sites] contenant du texte avant le formulaire, le curseur se déplace directement vers le formulaire au lieu du texte avant le formulaire (NPR-34947).

* [!UICONTROL La prévisualisation avec l’option ] Données pour préremplir un formulaire adaptatif à l’aide d’un fichier XML de données  [!DNL Experience Manager] 6.2 ne fonctionne pas correctement (NPR-35087).

* Lorsque vous mettez à jour le dictionnaire de données d’un formulaire adaptatif, le formulaire n’est pas traduit car le formulaire adaptatif renvoie des valeurs mises en cache (NPR-34845).

* Le chargement des fragments prend plus de temps dans un formulaire adaptatif en raison de l’invalidation du cache (NPR-34567).

* La navigation par onglets ne fonctionne pas correctement pour les lecteurs d’écran dans un formulaire adaptatif (NPR-34544).

**Correspondence Management**

* Impossible d&#39;enregistrer les valeurs des balises XML avec des données numériques, qui incluent le type flottant, en tant que brouillon (NPR-35050).

* Lorsque vous migrez les ressources à partir d’ES3, elles incluent deux conditions par défaut non modifiables (NPR-34972).

* Lorsque vous modifiez un dictionnaire de données dans une lettre, la section [!UICONTROL Contenu prêté] affiche des rectangles tournants au lieu d&#39;informations utiles (NPR-34853).

**Communication interactive**

* Le nom de configuration de déploiement pour Interactive Communication, disponible après l&#39;installation du module complémentaire [!DNL Forms], duplicata le nom de configuration de déploiement standard (NPR-34976).

**Document Security**

* Lorsque vous enregistrez une nouvelle stratégie de sécurité de document, Experience Manager Forms affiche le message d&#39;erreur `Relative validity period is required` (NPR-34679).

* Document Security ne peut pas protéger le document PDF 2.0 (CQ-4305851).

Pour plus d’informations sur les mises à jour de sécurité, voir [Experience Manager security bulletins page](https://helpx.adobe.com/security/products/experience-manager.html).

## Installer 6.5.7.0 {#install}

**Configuration requise et informations supplémentaires**

* aem 6.5.7.0 requiert AEM 6.5. Voir [documentation de mise à niveau](/help/sites-deploying/upgrade.md) pour obtenir des instructions détaillées.
* Le téléchargement du Service Pack est disponible sur l&#39;Adobe [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
* Lors d’un déploiement avec MongoDB et plusieurs instances, installez AEM 6.5.7.0 sur l’une des instances d’auteur à l’aide du gestionnaire de modules.

>[!NOTE]
>
>Adobe ne recommande pas de supprimer ou de désinstaller le package [!DNL Adobe Experience Manager] 6.5.7.0.

### Installation du Service Pack {#install-service-pack}

Effectuez les étapes suivantes pour installer le Service Pack sur une instance Adobe Experience Manager 6.5 existante :

1. Redémarrez l’instance avant l’installation si l’instance est en mode de mise à jour (ce qui est le cas lorsque l’instance a été mise à jour à partir d’une version antérieure). L’Adobe recommande également un redémarrage si le temps de fonctionnement actuel d’une instance est élevé.

1. Avant l&#39;installation, effectuez un instantané ou une nouvelle sauvegarde de votre instance [Experience Manager].

1. Téléchargez le Service Pack à partir de [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.7.zip).

1. Ouvrez Package Manager et cliquez sur **[!UICONTROL Télécharger le package]** pour télécharger le package. Pour en savoir plus, voir [Package Manager](/help/sites-administering/package-manager.md).

1. Sélectionnez le package et cliquez sur **[!UICONTROL Installer]**.

1. Pour mettre à jour le connecteur S3, arrêtez l’instance après l’installation du Service Pack, remplacez le connecteur existant par un nouveau fichier binaire fourni dans le dossier d’installation, puis redémarrez l’instance. Voir [Banque de données Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>La boîte de dialogue de l’interface utilisateur de Package Manager se ferme parfois lors de l’installation du Service Pack. Adobe vous recommande d’attendre que les journaux d’erreurs se stabilisent avant d’accéder au déploiement. Attendez les journaux spécifiques liés à la désinstallation du lot de mise à jour avant de vous assurer que l&#39;installation est réussie. En règle générale, cela se produit sur [!DNL Safari] mais peut se produire par intermittence sur n’importe quel navigateur.

**Installation automatique**

Il existe deux manières d’installer automatiquement Adobe Experience Manager 6.5.7.0 sur une instance de travail :

R. Placez le package dans le dossier `../crx-quickstart/install` lorsque le serveur est disponible en ligne. Le package est automatiquement installé.

B. Utilisez l’API [HTTP de Package Manager](https://docs.adobe.com/content/docs/en/crx/2-3/how_to/package_manager.html). Utilisez `cmd=install&recursive=true` pour installer les packages imbriqués.

>[!NOTE]
>
>Adobe Experience Manager 6.5.7.0 ne prend pas en charge l’installation des Bootstrap.

**Validation de l’installation**

1. La page d&#39;informations sur le produit (`/system/console/productinfo`) affiche la chaîne de version mise à jour `Adobe Experience Manager (6.5.7.0)` sous [!UICONTROL Produits installés].

1. Tous les lots OSGi sont soit **[!UICONTROL PRINCIPAL]** soit **[!UICONTROL FRAGMENT]** dans la console OSGi (Utiliser la console Web : `/system/console/bundles`).

1. Le lot OSGi `org.apache.jackrabbit.oak-core` est de la version 1.22.3 ou ultérieure (Utilisez la console Web : `/system/console/bundles`).

Pour connaître les plates-formes certifiées pour fonctionner avec cette version, voir les [exigences techniques](/help/sites-deploying/technical-requirements.md).

### Installer le module complémentaire Adobe Experience Manager Forms {#install-aem-forms-add-on-package}

>[!NOTE]
>
>[!DNL Experience Manager Forms] libère les packages de modules complémentaires une semaine après la date de publication prévue du  [!DNL Experience Manager] Service Pack.

>[!NOTE]
>
>Passez cette étape si vous n’utilisez pas AEM Forms. Les correctifs dans Adobe Experience Manager Forms sont fournis par le biais d’un module complémentaire distinct.

1. Assurez-vous d’avoir installé le Service Pack de Adobe Experience Manager.
1. Téléchargez le module complémentaire Forms correspondant figurant dans les [versions AEM Forms](https://helpx.adobe.com/fr/aem-forms/kb/aem-forms-releases.html) de votre système d’exploitation.
1. Installez le module complémentaire Forms comme décrit dans [Installation des modules complémentaires AEM Forms](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

>[!NOTE]
>
>aem 6.5.7.0 inclut une nouvelle version du [package de compatibilité AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en#aem-65-forms-releases). Si vous utilisez une ancienne version du package de compatibilité AEM Forms et que vous mettez à jour vers AEM 6.5.7.0, installez la dernière version du package après l&#39;installation du package Forms-Ajoute-On.

### Installer Adobe Experience Manager Forms on JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Passez cette étape si vous n’utilisez pas AEM Forms sous JEE. Les correctifs d’Adobe Experience Manager Forms on JEE sont diffusés par le biais d’un programme d’installation distinct.

Pour plus d’informations sur l’installation cumulative du programme d’installation pour Experience Manager Forms on JEE et sur la configuration après le déploiement, voir les [notes de mise à jour](jee-patch-installer-65.md).

### UberJar {#uber-jar}

UberJar pour Experience Manager 6.5.7.0 est disponible dans le [référentiel Maven Central](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.7/).

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
>UberJar et les autres artefacts associés sont disponibles dans le référentiel Maven Central au lieu du référentiel Adobe Public Maven (`repo.adobe.com`). Le fichier UberJar principal est renommé `uber-jar-<version>.jar`. Il n’existe donc pas de valeur `classifier`, avec `apis`, pour la balise `dependency`.

## Fonctionnalités obsolètes {#removed-deprecated-features}

Vous trouverez ci-dessous une liste de fonctionnalités marquées comme obsolètes avec [!DNL Experience Manager] 6.5.7.0. Les fonctionnalités sont marquées comme obsolètes initialement et ultérieurement supprimées dans une prochaine version. Une autre option est généralement fournie.

Vérifiez si vous utilisez une fonction ou une fonctionnalité dans un déploiement. Par ailleurs, prévoyez de modifier la mise en oeuvre pour utiliser une autre option.

| Zone | Fonctionnalité | Remplacement |
|---|---|---|
| Intégrations | L’écran **[!UICONTROL souscription aux services Cloud AEM]** est obsolète. L’intégration des AEM et des Cibles étant mise à jour dans AEM 6.5 pour prendre en charge l’API Target Standard, qui utilise l’authentification via l’Adobe IMS et E/S, et le rôle croissant du lancement d’Adobe pour l’instrumentalisation de pages de données d’analyse et de personnalisation, l’assistant d’inclusion est devenu non pertinent du point de vue fonctionnel. | Configurez les connexions système, l’authentification IMS Adobe et les intégrations [!DNL Adobe I/O] via les services cloud AEM correspondants. |
| Connecteurs | L’Adobe JCR Connector for Microsoft SharePoint 2010 et Microsoft SharePoint 2013 est obsolète pour AEM 6.5. | N/A |

## Problèmes connus {#known-issues}

* Si vous rencontrez des problèmes dans la réponse [!DNL Experience Manager] en raison du minuteur de Registre des composants verrouillé, [installez ce package](https://mvnrepository.com/artifact/org.apache.felix/org.apache.felix.scr/2.1.20). La résolution de ces problèmes devrait être incluse dans la prochaine [version du Service Pack Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=en#aem-on-prem-managed-services).

* Ignorez les erreurs suivantes dans le fichier `error.log` lors de l&#39;installation du Experience Manager 6.5.7.0 :

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

* Si vous effectuez une mise à niveau de votre instance [!DNL Experience Manager] de la version 6.5 à la version 6.5.7.0, vous pouvez vue `RRD4JReporter` exceptions dans le fichier `error.log`. Redémarrez l’instance pour résoudre le problème.

* Si vous installez [!DNL Experience Manager] 6.5 Service Pack 5 ou un Service Pack précédent sur [!DNL Experience Manager] 6.5, la copie d&#39;exécution du modèle de flux de travaux personnalisé de vos ressources (créée dans `/var/workflow/models/dam`) est supprimée.
Pour récupérer votre copie d’exécution, l’Adobe recommande de synchroniser la copie au moment de la conception du modèle de flux de travail personnalisé avec sa copie au moment de l’exécution à l’aide de l’API HTTP :
   `<designModelPath>/jcr:content.generate.json`.

* Contactez le service à la clientèle d’Adobe si vous rencontrez des problèmes lors de la modification et de la création de règles en cascade dans [!UICONTROL éditeur Forms de Schéma de métadonnées de dossiers] et [!UICONTROL éditeur de Schéma de métadonnées] à l’aide de la boîte de dialogue [!UICONTROL Définir la règle]. Les règles déjà créées et enregistrées fonctionnent comme prévu.

* Si un dossier de la hiérarchie est renommé [!DNL Experience Manager Assets] et que le dossier imbriqué contenant une ressource est publié dans [!DNL Brand Portal], le titre du dossier n’est pas mis à jour dans [!DNL Brand Portal] tant que le dossier racine n’a pas été publié à nouveau.

* Lorsqu’un utilisateur sélectionne pour la première fois un champ dans un formulaire adaptatif, l’option permettant d’enregistrer une configuration ne s’affiche pas dans le navigateur de propriétés. La sélection pour configurer un autre champ du formulaire adaptatif dans le même éditeur résout le problème.

* Si [!UICONTROL l&#39;Assistant Configuration des ressources connectées] renvoie un message d&#39;erreur 404 après l&#39;installation, réinstallez manuellement les packages `cq-remotedam-client-ui-content` et `cq-remotedam-client-ui-components` à l&#39;aide de Package Manager.

* Les erreurs et messages d’avertissement suivants peuvent s’afficher lors de l’installation de AEM 6.5.x.x :
   * « Lorsque l’intégration de Target est configurée dans AEM à l’aide de l’API Target Standard (authentification IMS), l’exportation de fragments d’expérience vers Target entraîne la création de types d’offres incorrects. Au lieu du type « Fragment d’expérience » / source « Adobe Experience Manager », Target crée plusieurs offres avec le type « HTML » / source « Adobe Target Classic ».
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: Aucune fenêtre de maintenance n’a été trouvée sur granite/operations/maintenance.
   * La validation côté serveur du formulaire adaptatif échoue lorsque des fonctions d’agrégat telles que SUM, MAX et MIN sont utilisées. CQ-4274424
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Aucune fenêtre de maintenance n’a été trouvée sur granite/operations/maintenance.
   * La zone réactive d’une image interactive Dynamic Media n’est pas visible lors de la prévisualisation du fichier via la visionneuse de bannières modifiables.

## bundles OSGi et packages de contenu inclus {#osgi-bundles-and-content-packages-included}

Les documents de texte suivants liste les lots OSGi et les packages de contenu inclus dans AEM 6.5.7.0 :

* [Liste des lots OSGi inclus dans AEM 6.5.7.0](assets/6570_bundles.txt)

* [Liste des packages de contenu inclus dans AEM 6.5.7.0](assets/6570_packages.txt)

## Sites Web restreints {#restricted-sites}

Ces sites Web ne sont accessibles qu&#39;aux clients. Si vous êtes client et avez besoin d’un accès, contactez votre responsable de compte Adobe.

* [Téléchargement du produit à l’adresse licensing.adobe.com](https://licensing.adobe.com/)
* Voir [comment contacter l&#39;assistance clientèle](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] Notes de mise à jour 6.5](/help/release-notes/release-notes.md)
>* [[!DNL Experience Manager] page de produits](https://www.adobe.com/fr/marketing/experience-manager.html)
>* [[!DNL Experience Manager] 6.5 Documentation](https://experienceleague.adobe.com/docs/experience-manager-65.html)
>* S’abonner aux [mises à jour de produits prioritaires par Adobe](https://www.adobe.com/subscription/priority-product-update.html)

