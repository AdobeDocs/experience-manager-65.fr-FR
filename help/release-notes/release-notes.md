---
title: Notes de mise à jour de la version 6.5 d’ [!DNL Adobe Experience Manager]
description: Recherchez des informations de mise à jour, les nouveautés, les procédures d’installation et une liste détaillée de modifications pour [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 3
exl-id: 38227a66-f2a9-4909-9297-1eced4ed6e8c
source-git-commit: ec9094f25cfbcd1497a6bbc87cce9754e247a770
workflow-type: tm+mt
source-wordcount: '3759'
ht-degree: 27%

---

# Notes de mise à jour du dernier pack de services [!DNL Adobe Experience Manager] 6.5 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession&cid=a915e87c-369a-480c-9daf-d13efc766798 -->

## Informations sur la version {#release-information}

| Produit | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Version | 6.5.15.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Type | Mise à jour du pack de services |
| Date | 24 novembre 2022 <!-- UPDATE FOR EACH NEW RELEASE --> |
| URL de téléchargement | [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## Éléments compris dans [!DNL Experience Manager] 6.5.15.0 {#what-is-included-in-aem-6515}

[!DNL Experience Manager] 6.5.15.0 comprend de nouvelles fonctionnalités, des améliorations importantes demandées par les clients, des correctifs de bogues, ainsi que des améliorations des performances, de la stabilité et de la sécurité, publiées depuis la version initiale de 6.5 en avril 2019. [Installez ce pack de services](#install) dans [!DNL Experience Manager] 6.5. <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- Some of the key features and improvements are the following:

* _REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS YOU WANT TO HIGHLIGHT IN THIS RELEASE?_

* Added support for password reset for Dynamic Media Classic users within Experience Manager. (ASSETS-10298) -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## [!DNL Assets] {#assets-6515}

* Si le déplacement d’une ressource dans Experience Manager échoue, la ressource peut toujours être renommée. (NPR-38753)
* Lors de l’affichage des ressources dans une [!UICONTROL Mode Liste], certains titres sont manquants. (CQ-4345746)
* Le lecteur d’écran n’annonce pas le sous-menu de [!UICONTROL Relate] sur l’onglet De base de la page Propriétés de la ressource. (ASSETS-6938)
* Le lecteur d’écran détecte incorrectement les icônes de dossier sur la page de navigation Ressources avec la liste des dossiers. (ASSETS-6936)
* Lors de la copie d’une collection, une balise vide est manquante dans l’image. `alt` attribute or role=&quot;présentation&quot;. Par conséquent, l’image est exposée aux utilisateurs du lecteur d’écran. (ASSETS-6932)
* Le texte affiché lors de l’annotation d’une ressource n’a pas de valeur 4:5:Rapport de contraste de 1 par rapport à la couleur d’arrière-plan. (ASSETS-6931)
* Dans l’onglet IPTC de la page Propriétés de la ressource, lorsque vous ajustez la largeur de page, le contenu de la page ne s’adapte pas correctement et donne lieu à un défilement horizontal. (ASSETS-6929)
* Lorsque vous filtrez des ressources, le texte de filtre dans la variable [!UICONTROL min] et [!UICONTROL max] disparaît après la saisie d’une valeur. (ASSETS-6925)
* Dans les collections de Experience Manager, le lecteur d’écran n’annonce pas la valeur [!UICONTROL email] dans l’écran Télécharger . (ASSETS-6923)
* Il manque un texte de remplacement lors de l’annotation des éléments. (ASSETS-6922)
* Si le texte est écrit dans les champs Heures et Minutes dans le sélecteur de date, aucun message d’erreur de texte ne s’affiche. L’erreur n’est identifiée qu’à l’aide de la couleur rouge. (ASSETS-6852, ASSETS-6921, ASSETS-6920, ASSETS-6907)
* Le texte de remplacement dans `[role='img']` dans le filtre Fichiers est manquant. (ASSETS-6919)
* Annonce incorrecte du lecteur d’écran pour la variable [!UICONTROL Créer] sous-menu. (ASSETS-6916)
* Dans les collections Experience Manager, bouton de suppression `X` ne comporte aucun texte à annoncer pour les lecteurs d’écran. (ASSETS-6912)
* Lors de l’utilisation de l’analyseur de contraste des couleurs dans Experience Manager, il n’existe aucune différence de couleur entre la date actuelle et la date choisie dans le sélecteur de date du widget Calendrier. Il manque un rapport de contraste d’au moins 3:1 par rapport à ses couleurs adjacentes. (ASSETS-6911)
* Dans les fichiers de Experience Manager, lors de la sélection de l’une des options de [!UICONTROL Planification] Bouton radio dans Gérer la publication, le nom et l’état des options du bouton radio sont annoncés par le lecteur d’écran. Toutefois, la variable **Planification** n’est pas annoncé. (ASSETS-6908, ASSETS-6906)
* Le texte de remplacement est absent de l’icône Tri . (ASSETS-6904)
* Sur la page Propriétés de l’élément, le nom du champ `Person` dans l’onglet Extension IPTC , les libellés ne sont pas annoncés par les lecteurs d’écran. Le lecteur d’écran annonce uniquement un champ modifiable et actuellement vide, mais pas le nom du libellé. (ASSETS-6903, ASSETS-6848)
* L’outil d’annotation ne peut pas être affiché à l’aide du clavier. Une souris est utilisée pour dessiner une image afin d’afficher l’outil Annotation. (ASSETS-6899)
* Dans les collections Experience Manager, un champ vide s’affiche sur la **Avancé** La tabulation affiche un rapport de contraste incorrect entre la bordure et la couleur adjacente. (ASSETS-6895)
* Valeurs d’attribut ARIA incorrectes pour certains éléments lors de la modification des ressources. (ASSETS-6894)
* Le lecteur d’écran n’identifie pas correctement l’en-tête lors de la création d’un workflow. (ASSETS-6892)
* Lors de la copie d’une collection, le bouton de suppression de l’image du SVG `X` avec role=&quot;img&quot; est absent role=&quot;présentation&quot;. Par conséquent, l’image est exposée aux utilisateurs du lecteur d’écran. (ASSETS-6890)
* Dans le **De base** dans les propriétés de la ressource, le lecteur d’écran n’annonce pas correctement l’état de développement ou de réduction du champ Balises. (ASSETS-6889)
* Le **De base** sous Propriétés de ressource , l’onglet contient des pages avec un ID en double. (ASSETS-6888)
* Le libellé du champ de texte pour définir un titre lors de la création d’un workflow disparaît lorsque vous spécifiez une valeur dans la zone de texte. (ASSETS-6887)
* La liste des destinataires lors du partage d’un lien s’affiche sous la forme d’un tableau de données avec des en-têtes, mais elle n’est pas sémantiquement identifiée en tant que tableau de données pour les utilisateurs de lecteur d’écran. (ASSETS-6886)
* Aucun message d’erreur pour représenter un champ vide ne s’affiche dans `Add Email Address` champ . L’erreur n’est représentée que par une couleur. (ASSETS-6885, ASSETS-6843)
* Les textes d’espace réservé, le chemin et le texte de remplacement n’ont pas au moins un rapport de contraste de 4,5:1 par rapport à leur couleur d’arrière-plan. (ASSETS-6884, ASSETS-6865)
* Valeurs non valides pour certains attributs ARIA lors de l’enregistrement d’une collection dynamique. (ASSETS-6882)
* Lorsque vous enregistrez une collection dynamique, certaines étiquettes ne sont pas correctement associées au lecteur d’écran. (ASSETS-6881)
* Dans l’onglet IPTC des propriétés des ressources, le lecteur d’écran n’annonce pas le libellé des champs de formulaire de mot-clé. (ASSETS-6879)
* Dans les collections Experience Manager, la variable [!UICONTROL Email] n’est pas identifié comme champ obligatoire et aucun message d’erreur ne s’affiche si vous ne spécifiez aucune valeur. (ASSETS-6877)
* Dans les fichiers Experience Manager, aucun message d’erreur n’apparaît dans **Partage de liens** s’affiche dans `Add Email Address`. L’erreur n’est identifiée que dans en utilisant une couleur. (ASSETS-6876, ASSETS-6875)
* [!UICONTROL Recadrage et mappage] Les options ne comportent pas de noms de programme lors de la modification d’une ressource. (ASSETS-6874)
* Le texte du filtre n’a pas de rapport du contrat 4.5:1 par rapport à la couleur d’arrière-plan. (ASSETS-6873)
* Le texte du nom du dossier sur la page de navigation principale ne présente pas de rapport de contraste de 4,5:1 par rapport à la couleur d’arrière-plan. (ASSETS-6872)
* Lors de l’exécution de la variable [!UICONTROL Copier] pour les collections, l’opération **[!UICONTROL Ajouter un utilisateur]** la commande de formulaire de zone de liste modifiable n’est pas correctement associée à son libellé visible. (ASSETS-6870)
* Le lecteur d’écran n’annonce pas le [!UICONTROL Créer] options du sous-menu Bouton. (ASSETS-6869)
* Les options Portée, Workflows et Fuseau horaire ne présentent pas de rapport de contraste de 4,5:1 par rapport à la couleur d’arrière-plan. (ASSETS-6868)
* Le lecteur d’écran annonce incorrectement l’état de réduction de la variable **Chronologie** colonne . (ASSETS-6864)
* Éléments enfants manquants pour certains rôles ARIA lors de l’enregistrement d’une collection dynamique. (ASSETS-6862)
* Lors du partage d’une ressource, nécessitait des attributs ARIA pour `Search/Add Email Address` ne sont pas spécifiées. (ASSETS-6860)
* Le **map** ne peut pas être affichée à l’aide du clavier. Pour afficher la boîte de dialogue de mappage, cliquez avec la souris. (ASSETS-6859)
* Éléments enfants manquants pour certains des rôles ARIA dans l’onglet De base de la page des propriétés des ressources. (ASSETS-6858)
* Les champs de saisie de texte vide, disponibles dans l’onglet IPTC des propriétés de la ressource, n’ont pas de rapport de contraste de 3:1 par rapport aux couleurs adjacentes. (ASSETS-6854, ASSETS-6847)
* Les icônes de profil dans le **Chronologie** sont incorrectement détectées par les lecteurs d’écran. (ASSETS-6850)
* Le lecteur d’écran n’indique pas que la zone combinée État de la révision, disponible dans l’onglet De base des propriétés de la ressource, est un champ en lecture seule. (ASSETS-6849)
* Le lecteur d’écran n’affiche pas correctement le libellé des cases à cocher Tout sélectionner et Annotation . (ASSETS-6846)
* La sélection au clavier ignore la variable `About Adobe Experience Manager` , disponible dans la variable **Afficher l’aide** . (ASSETS-6845)
* Les lecteurs d’écran n’annoncent pas correctement les dossiers sélectionnés lors de la navigation dans la liste de dossiers à l’aide des touches fléchées du clavier en mode Carte. (ASSETS-6844)
* Lors du chargement d’un PDF vers le Experience Manager, l’utilisation de la mémoire augmente constamment. (ASSETS-16889)
* Lorsqu’un workflow convertit un fichier .ZIP en nom de dossier dans Assets, il ne conserve pas la casse du nom de fichier .ZIP. (ASSETS-16712)
* Lors du passage de Brand Portal à Experience Manager 6.5, le filtre de prédicat utilisateur n’affiche pas les résultats appropriés lorsque vous appliquez le filtre pour la première fois. (ASSETS-15932)
* Impossible d’annoter une vidéo. (ASSETS-15217)
* **Gérer la publication** disparaît pour un utilisateur sans accès à réplication et `READ` et `WRITE` accès à `ETC` et `VAR`. (ASSETS-15007)
* Le temps de chargement de la page de propriétés augmente pour une ressource avec plusieurs références. (ASSETS-14182)
* Lorsqu’une image est dépubliée à partir de Brand Portal, Experience Manager la dépublie également à partir de Dynamic Media. Par conséquent, aucune image n’est affichée sur le site web en ligne. (ASSETS-14118)
* Problèmes XSS sur les cartes avec recadrage intelligent dans Dynamic Media. (ASSETS-14212, ASSETS-14208, ASSETS-13704)
* Problème XSS dans les paramètres prédéfinis de la visionneuse dans Dynamic Media. (ASSETS-13822)
* Validez l’accès utilisateur lors de la prévisualisation de ressources DM sur AEM. (CQ-4314757)


## Commerce {#commerce-6515}

* La création d’une page de magasin a échoué, ce qui a interrompu le processus de déploiement global du catalogue. (CQ-4347181)

## [!DNL Forms] {#forms-6515}

### Fonctionnalités clés {#keyfeatures}

* AEM Forms Designer est désormais disponible dans [Espagnol](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr). (LC-3920051)
* Vous pouvez désormais utiliser [OAuth2 pour l’authentification avec les protocoles de serveur de messagerie Microsoft® Office 365 (SMTP et IMAP)](/help/forms/using/oauth2-support-for-mail-service.md). (NPR-35177)
* Vous pouvez définir [Revalider sur le serveur](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-an-adaptive-form/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html#enabling-server-side-validation-br) sur true pour identifier les champs masqués à exclure d’un document d’enregistrement côté serveur. (NPR-38149)
* AEM Forms Designer nécessite une version 32 bits de Visual C++ 2019 Redistributable (x86).  (NPR-36690)

### Correctifs {#fixes}

* Lorsque la propriété data-disabled d’un formulaire adaptatif est activée, l’aspect des boutons radio et des groupes de cases à cocher ne change pas. (NPR-39368)
* Lorsqu’un formulaire adaptatif est traduit, certaines traductions sont manquantes et ne s’affichent pas correctement. (NPR-39367)
* Lorsque la propriété d’une page est définie sur masquée, la page n’est pas supprimée du jeu de formulaires. (NPR-39325)
* Dans un document d’enregistrement, la section de note de bas de page dynamique située à la fin de la page n’est pas présente. (NPR-39322)
* Lorsqu’un document d’enregistrement est généré pour un formulaire adaptatif, seul l’alignement vertical est autorisé pour les boutons radio et les cases à cocher. L’utilisateur ne peut pas définir l’alignement horizontal des boutons radio et des cases à cocher. (NPR-39321)
* Après le déploiement de Correspondence Management, si plusieurs utilisateurs tentent d’accéder à un formulaire, org.apache.sling.i18n.impl.JcrResourceBundle.loadPotentielLanguageRoots devient un goulot d’étranglement et la plupart des threads sont frappés. Le chargement de plusieurs requêtes de page de formulaires dure souvent plus d’une minute, même lorsque le serveur est à très faible charge. (NPR-39176, CQ-4347710)
* Dans un formulaire adaptatif, lorsque vous utilisez un champ de texte enrichi dans un fragment de formulaire adaptatif chargé en différé, certaines des erreurs suivantes se produisent :
   * Vous ne pouvez pas modifier le contenu ni ajouter quoi que ce soit au champ Texte enrichi.
   * Le modèle d’affichage appliqué au texte enrichi n’est pas respecté. 
   * Le message d’erreur correspondant à la longueur minimale du champ ne s’affiche pas lors de l’envoi du formulaire.
   * Le contenu de ce champ de texte enrichi est inclus plusieurs fois dans le fichier submit-XML produit. (NPR-39168)
* Lorsque l’option de sélecteur de date est utilisée dans un formulaire adaptatif, elle ne parvient pas à convertir la valeur au format correct. (NPR-39156)
* Lors de la prévisualisation d’un formulaire adaptatif en tant que formulaire de HTML, il n’est pas rendu correctement, car certains sous-formulaires se chevauchent avec le formulaire parent. (NPR-39046)
* Si le panneau comporte un tableau masqué et que le formulaire adaptatif est rendu à l’aide de la vue tabulaire, les champs du premier onglet ne s’affichent pas correctement. (NPR-39025)
* Le `Body` balise manquante pour le modèle prêt à l’emploi. (NPR-39022)
* Le document d’enregistrement n’est pas généré dans la langue du formulaire adaptatif. Il est toujours généré en anglais. (NPR-39020)
* Lorsqu’un formulaire adaptatif comporte plusieurs panneaux et que certains d’entre eux utilisent le panneau d’usine **Pièce jointe** , le composant `Error occurred while draft saving` s’affiche. (NPR-38978)
* When `=` Le signe est utilisé dans les champs de case à cocher, de liste déroulante ou de bouton radio d’un formulaire adaptatif et le document d’enregistrement est généré, puis `=` Le signe n’est pas visible dans le document d’enregistrement généré.(NPR-38859)
* Le nombre d’erreurs de traitement par lots de l’avis augmente de plusieurs façons après la mise à niveau du Service Pack 6.5.11.0. (NPR-39636)
* Lorsque vous ne fournissez pas de données de test, le chargement des lettres Correspondence Management échoue dans l’interface utilisateur de l’agent. (CQ-4348702)
* Lorsque l’utilisateur applique le Service Pack 14 (SP14) d’AEM Forms AEM Forms déployé à l’aide d’IBM® WebSphere®, l’amorçage échoue lors de l’initialisation d’une base de données et de la variable `java.lang.NoClassDefFoundError:org/apache/log4j/Logger` s’affiche.(NPR-39414)
* Sur un serveur OSGi de formulaire d’AEM, lorsque vous utilisez l’API Document Service pour certifier le PDF, il échoue avec une erreur : com.adobe.fd.signatures.truststore.errors.exception.CredentialRetrievalException : AEM-DSS-311-003. (NPR-38855)
* Lorsque l’utilisateur tente d’utiliser le service wrapper pour le rendu des lettres avec AEM 6.3 Forms, la variable `java.lang.reflect.UndeclaredThrowableException` s’affiche. (CQ-4347259)
* Lorsqu’un formulaire XDP est rendu en tant que formulaire HTML5, le contenu du gabarit est rendu en premier, quel que soit le positionnement des objets dans un formulaire adaptatif. (CQ-4345218)
* La configuration de l’application au niveau du serveur de destination modifie les paramètres définis au niveau du serveur source, même si la variable **Remplacer la configuration lorsque l’importation est terminée** n’est pas cochée au moment de l’importation de l’application. (NPR-39044)
* Lorsqu’un utilisateur tente de mettre à jour la configuration du connecteur à l’aide de Configuration Manager, cela échoue.(CQ-4347077)
* Lorsque l’utilisateur tente d’exécuter un correctif d’AEM de Form on JEE après avoir modifié le mot de passe par défaut de l’utilisateur administrateur, une exception s’affiche. `com.adobe.livecycle.lcm.core.LCMException[ALC-LCM-200-003]: Failed to whitelist the classes` survient. (CQ-4348277)
* Dans AEM Designer, les champs de formulaire sans légende sont placés dans des cellules de tableau, y compris des cases à cocher.(LC-3920410)
* Lorsque l’utilisateur tente d’ouvrir l’aide dans AEM Forms Designer, elle ne s’affiche pas correctement. (CQ-4341996)
* Les Forms adaptatives avec plusieurs paramètres régionaux sont lentes à charger. (NPR-39176)

## [!DNL Sites] {#sites-6515}

* La console Lancements Experience Manager Sites apparaissait vide. (NPR-39188)
* Les références n’ont pas été ajustées lorsque la page qui contenait la référence devait également être activée lors du déplacement de la page. (NPR-39061)
* Lorsqu’un conteneur de mises en page est démasqué à l’aide du conteneur parent, les modifications de mises en page ne sont pas appliquées à tous les composants du conteneur imbriqué. (NPR-39041)
* Le contenu ne chevauche désormais plus d’autres contenus à une largeur de 320 pixels. (SITES-8885)
* Ajout de la sélection après la fermeture d’une boîte de dialogue. (SITES-8885)

### Accessibilité {#access-6515}

<!-- REMOVED FROM TOTAL RELEASE CANDIDATE LIST * The scrollable region of the Page Editor did not have keyboard access. (SITES-2936) -->
<!-- REMOVED FROM TOTAL RELEASE CANDIDATE LIST * The color input field of the Page Editor is not labeled or visible on the screen. (SITES-2925) -->
<!-- REMOVED FROM TOTAL RELEASE CANDIDATE LIST * The iframe in the Page Editor is missing a title attribute; it must have an accessible name. (SITES-2894) -->
* Le **[!UICONTROL Annotation]** n’a pas son nom d’accessibilité. (SITES-2892)
* État d’un composant d’interface utilisateur PRINCIPAL (**[!UICONTROL Couper]**, **[!UICONTROL Copier]**, **[!UICONTROL Coller]**, **[!UICONTROL Insertion de composants]**, **[!UICONTROL Groupe]**, etc.) n’a pas au moins un rapport de contraste de luminosité de trois à un avec l’arrière-plan adjacent intérieur ou extérieur. (SITES-8889, SITES-8756, SITES-8885)
* Message d’état non annoncé automatiquement. (SITES-8889, SITES-8756, SITES-8885)
* Le contenu textuel manque d’un rapport de contraste de 4,5:1. (SITES-8756, SITES-8885)
* Le texte du lien ou du bouton n’a pas de rapport de contraste de 4,5:1 sur le survol ou la mise au point. (SITES-8756, SITES-8885)

### [!DNL Content Fragments] {#sites-contentfragments-6515}

* GraphQL soulève une exception. Par exemple, vous ne pouvez pas obtenir de balises de variation d’un fragment de contenu. Il n&#39;y a pas de variante avec le nom &quot;électrique&quot;. Ce problème est dû à l’appel de `getVariationTags` pour une variation non existante qui soulève une exception. (SITES-8898)
* Tri des ordres de titre en mode Liste, croissant ou décroissant, de la manière dont les titres sont triés par ordre A, C, B. (SITES-7585)
* Ajout de la prise en charge du balisage pour les variations de fragments de contenu. (SITES-8168)
* Identifié et supprimé du code spécifique à Odin de Experience Manager 6.5 qui était inutile. (SITES-3574)
* Lors de la publication d’un fragment de copie de langue à partir de l’interface utilisateur de l’éditeur de fragments de contenu, les références associées étaient publiées sous le dossier Anglais. (NPR-39182)
* Les champs de date sont préremplis avec une date. (NPR-39124)
* Les balises ont disparu la deuxième fois que vous avez sélectionné l’option de bouton radio. (NPR-39071)

### Fluid XP {#sites-fluidxp-6515}

* Activation de la prise en charge de la compilation ES6 pour la bibliothèque cliente `/libs/cq/gui/components/siteadmin/admin/restoretree/clientlibs/restoretree.js`. (NPR-39067)
* Le champ multiple d’un modèle de fragment de contenu ne peut pas être vidé et enregistré, car la validation a lieu même si **[!UICONTROL Obligatoire]** n’est pas sélectionnée. (NPR-39063)
* Dans **[!UICONTROL Copier]** ou **[!UICONTROL Livecopy]** les tâches, `cq:targetMetadata` Les informations étaient incorrectement dupliquées. Cette fonctionnalité entraînait l’pointage de plusieurs fragments d’expérience en Experience Manager vers la même offre exportée dans la cible. (NPR-38970)
* Suite à une action Restaurer l’arborescence, le message `Un-publication pending. #0 in the queue` s’affiche dans l’interface utilisateur d’une page qui n’a jamais été publiée. (NPR-38847)

### Éditeur de page {#sites-pageeditor-6515}

* Annuler n’a pas supprimé la dernière modification apportée au texte qui a été ajoutée au composant. Au lieu de cela, lorsque la page a été actualisée, le composant entier a été supprimé. (SITES-8597)
* Mise à niveau `jquery-ui` dans la dernière version, l’éditeur de page ne fonctionnait pas correctement. (NPR-38596)
* Le contenu ne chevauche désormais plus d’autres contenus à une largeur de 320 pixels. (SITES-8756)
* ajout de focus après la fermeture de la boîte de dialogue (SITES-8756)

## Sling {#sling-6515}

* `Repoinit` ne prenait pas en charge la création ou la gestion de groupes dont le nom principal contenait un espace, car le nom du groupe était traité comme une chaîne et ne prenait pas en charge les citations. (SLING-10952)
* Les journaux sont remplis par inadvertance par des messages d’erreur et des exceptions. (NPR-39024)

## Projets de traduction {#translation-6515}

* La page de destination était ajoutée à la tâche de traduction pour les copies de langue mises à jour via le panneau Projets ; La page source n’a pas été mise à jour. (NPR-39278)
* Le processus de traduction échouait lors de la génération d’un aperçu pour toutes les pages d’un projet de traduction. (NPR-39059)
* Si aucun paramètre régional de langue n’existe, il est toujours créé dans un dossier de paramètres régionaux lorsque des règles de référence sont configurées pour un événement. (NPR-39054)

## Interface utilisateur {#ui-6515}

* Des erreurs JavaScript se produisent dans le fichier `multifield.js` pour certains champs du modèle de fragment de contenu dans l’éditeur de modèles de fragment de contenu et également dans l’éditeur de fragments de contenu. (NPR-39350)

## Workflow {#workflow-6515}

* Les workflows qui s’exécutaient correctement sur Experience Manager 6.5.11 ne s’exécutaient pas de manière cohérente sur la version 6.5.13 de Experience Manager. (NPR-39023)

## Installation d’[!DNL Experience Manager] 6.5.15.0 {#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.15.0 nécessite [!DNL Experience Manager] 6.5. Voir [documentation de mise à niveau](/help/sites-deploying/upgrade.md) pour obtenir des instructions détaillées. <!-- UPDATE FOR EACH NEW RELEASE -->
* Le téléchargement du pack de services est disponible dans la [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) d’Adobe.
* Lors d’un déploiement avec MongoDB et plusieurs instances, installez [!DNL Experience Manager] 6.5.15.0 sur l’une des instances d’auteur à l’aide du gestionnaire de modules.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> * Adobe ne recommande pas de supprimer ou de désinstaller le [!DNL Experience Manager] Package 6.5.15.0. Par conséquent, avant d’installer le module, vous devez créer une sauvegarde de la variable `crx-repository` au cas où vous auriez besoin de la restaurer. <!-- UPDATE FOR EACH NEW RELEASE -->
> * Pour obtenir des instructions sur l’installation du Service Pack pour AEM Forms, voir [Instructions d’installation du Service Pack AEM Forms](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).


### Installation du pack de services sur [!DNL Experience Manager] 6.5 {#install-service-pack}

1. Redémarrez l’instance avant l’installation si l’instance est en mode de mise à jour (lorsque l’instance a été mise à jour à partir d’une version antérieure). Adobe recommande un redémarrage si le temps de disponibilité actuel d’une instance est élevé.

1. Avant l’installation, prenez un instantané ou exécutez une sauvegarde récente de votre instance [!DNL Experience Manager].

1. Téléchargez le pack de services à partir de la [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Ouvrez Package Manager, puis sélectionnez **[!UICONTROL Télécharger le module]** pour télécharger le module. Pour en savoir plus, consultez la section [Gestionnaire de modules](/help/sites-administering/package-manager.md).

1. Sélectionnez le module, puis sélectionnez **[!UICONTROL Installer]**.

1. Pour mettre à jour le connecteur S3, arrêtez l’instance après l’installation du pack de services, remplacez le connecteur existant par un nouveau fichier binaire fourni dans le dossier d’installation, puis redémarrez l’instance. Consultez la section [Entrepôt de données S3 Amazon](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>La boîte de dialogue de l’interface utilisateur du gestionnaire de modules se ferme parfois pendant l’installation du pack de services. Adobe recommande d’attendre que les journaux d’erreurs se stabilisent avant d’accéder au déploiement. Attendez les logs spécifiques liés à la désinstallation de la mise à jour complète avant de vous assurer que les installations sont réussies. En règle générale, ce problème se produit dans [!DNL Safari] mais peut se produire par intermittence sur n’importe quel navigateur.

**Installation automatique**

Vous pouvez utiliser deux méthodes différentes pour installer automatiquement [!DNL Experience Manager] 6.5.15.0.<!-- UPDATE FOR EACH NEW RELEASE -->

* Placez le module dans le dossier `../crx-quickstart/install` lorsque le serveur est disponible en ligne. Le module est automatiquement installé.
* Utilisez l’[API HTTP à partir du gestionnaire de modules](/help/sites-administering/package-manager.md#package-share). Utilisez `cmd=install&recursive=true` afin que les modules imbriqués soient installés.

>[!NOTE]
>
>Experience Manager 6.5.15.0 ne prend pas en charge l’installation de Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Validation de l’installation**

Pour connaître les plateformes certifiées pour travailler avec cette version, reportez-vous à la section des [exigences techniques](/help/sites-deploying/technical-requirements.md).

1. La page d’informations sur les produits (`/system/console/productinfo`) affiche la chaîne de version mise à jour `Adobe Experience Manager (6.5.15.0)` sous [!UICONTROL Produits installés]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. Tous les lots OSGi sont au statut **[!UICONTROL ACTIF]** ou **[!UICONTROL FRAGMENT]** dans la console OSGi (utilisez la console web : `/system/console/bundles`).

1. Le lot OSGi `org.apache.jackrabbit.oak-core` est version 1.22.13 ou ultérieure (Utiliser la console web : `/system/console/bundles`). <!-- NPR-39436 for 6.5.15.0 --> <!-- OAK VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### Installer le Service Pack sur [!DNL Experience Manager] Forms {#install-service-pack-on-aemforms}

Pour obtenir des instructions sur l’installation du Service Pack sur AEM Forms, voir [Instructions d’installation du Service Pack AEM Forms](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

### UberJar {#uber-jar}

UberJar pour [!DNL Experience Manager] 6.5.15.0 est disponible dans la [Référentiel Maven Central](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.15/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Pour utiliser UberJar dans un projet Maven, voir [utilisation d’UberJar](/help/sites-developing/ht-projects-maven.md) et incluez la dépendance suivante dans le POM de votre projet : <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.15</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar et les autres artefacts associés sont disponibles sur le référentiel central Maven au lieu du référentiel Maven public Adobe (`repo.adobe.com`). Le fichier UberJar principal est renommé `uber-jar-<version>.jar`. Il n’existe donc pas de `classifier` avec `apis` comme valeur pour la balise `dependency`.

## Fonctionnalités obsolètes {#removed-deprecated-features}

Vous trouverez ci-dessous une liste des fonctionnalités signalées comme obsolètes par [!DNL Experience Manager] 6.5.7.0. Ces fonctionnalités sont initialement marquées comme obsolètes et supprimées ultérieurement dans une version future. Une option alternative est fournie.

Vérifiez si vous utilisez une de ces fonctionnalités dans un déploiement. Envisagez également de changer de mise en œuvre et d’utiliser une autre option.

| Domaine | Fonctionnalité | Remplacement |
|---|---|---|
| Intégrations | L’**[!UICONTROL Accord préalable des services cloud AEM]** est obsolète car l’intégration d’[!DNL Experience Manager] et d’[!DNL Adobe Target] est mise à jour dans [!DNL Experience Manager] 6.5. L’intégration prend en charge l’API Adobe Target Standard. L’API utilise l’authentification au moyen d’Adobe IMS et d’[!DNL Adobe I/O Runtime]. Elle prend en charge le rôle croissant d’Adobe Launch pour utiliser les pages [!DNL Experience Manager] à des fins d’analyse et de personnalisation, l’assistant d’accord préalable n’a donc aucune utilité sur le plan fonctionnel. | Configurez des connexions système, l’authentification Adobe IMS et les intégrations d’[!DNL Adobe I/O Runtime] à l’aide des services cloud [!DNL Experience Manager] correspondants. |
| Connecteurs | Adobe JCR Connector for Microsoft® SharePoint 2010 et Microsoft® SharePoint 2013 est obsolète dans [!DNL Experience Manager] 6.5. | S/O |

## Problèmes connus {#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST.
 -->

* [AEM de fragment de contenu avec le package d’index GraphQL 1.0.5](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fcfm-graphql-index-def-1.0.5.zip)
Ce package est nécessaire pour les clients utilisant GraphQL ; cela leur permet d’ajouter la définition d’index requise en fonction des fonctionnalités qu’ils utilisent réellement.

* [!DNL Microsoft® Windows Server 2019] ne prend pas en charge [!DNL MySQL 5.7] et [!DNL JBoss® EAP 7.1], [!DNL Microsoft® Windows Server 2019] ne prend donc pas en charge les installations clé en main pour [!DNL AEM Forms 6.5.10.0].

* Si vous effectuez une mise à niveau de votre [!DNL Experience Manager] de la version 6.5 à la version 6.5.10.0, vous pouvez voir apparaître des exceptions `RRD4JReporter` dans le fichier `error.log`. Pour résoudre ce problème, redémarrez cette instance.

* Si vous installez le pack de services 10 d’[!DNL Experience Manager] 6.5 ou un pack de services précédent sur [!DNL Experience Manager] 6.5, la copie d’exécution du modèle de workflow personnalisé de vos ressources (créé dans `/var/workflow/models/dam`) est supprimée.
Pour récupérer votre copie d’exécution, Adobe recommande de synchroniser la copie d’heure de conception du modèle de workflow personnalisé avec sa copie d’exécution à l’aide de l’API HTTP :
   `<designModelPath>/jcr:content.generate.json`.

* Les utilisateurs peuvent renommer un dossier dans une hiérarchie dans [!DNL Assets] et publier un dossier imbriqué dans [!DNL Brand Portal]. Toutefois, le titre du dossier n’est pas mis à jour dans [!DNL Brand Portal] jusqu’à ce que le dossier racine soit republié.

* Lorsqu’un utilisateur choisit de configurer un champ pour la première fois dans un formulaire adaptatif, l’option permettant d’enregistrer une configuration ne s’affiche pas dans l’explorateur de propriétés. Sélectionner un autre champ du formulaire adaptatif à configurer dans le même éditeur pour résoudre le problème.

* Les erreurs et messages d’avertissement suivants peuvent s’afficher lors de l’installation d’[!DNL Experience Manager] 6.5.x.x :
   * &quot;Lorsque l’intégration Adobe Target est configurée dans [!DNL Experience Manager] l’utilisation de l’API Target Standard (authentification IMS), puis l’exportation de fragments d’expérience vers Target entraîne la création de types d’offres incorrects. Au lieu de saisir &quot;Fragment d’expérience&quot;/source &quot;Adobe Experience Manager&quot;, Target crée plusieurs offres avec le type &quot;HTML&quot;/la source &quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler` : aucune fenêtre de maintenance n’a été trouvée sur granite/operations/maintenance.
   * La validation côté serveur du formulaire adaptatif échoue lorsque des fonctions d’agrégat telles que SUM, MAX et MIN sont utilisées (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Aucune fenêtre de maintenance n’a été trouvée sur granite/operations/maintenance.
   * La zone réactive d’une image interactive de Dynamic Media n’est pas visible lors de la prévisualisation du fichier via la visionneuse de bannières modifiables.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : Délai d’attente avant que la modification de l’enregistrement ne soit terminée.

* Lorsque vous tentez de déplacer, de supprimer ou de publier des fragments de contenu ou des sites ou des pages, un problème se produit lorsque les références aux fragments de contenu sont récupérées, car la requête en arrière-plan échoue ; en d’autres termes, la fonctionnalité ne fonctionne pas.
Pour garantir le bon fonctionnement, vous devez ajouter les propriétés suivantes au noeud de définition d’index. `/oak:index/damAssetLucene` (aucune réindexation n’est requise) :

   ```xml
   "tags": [
       "visualSimilaritySearch"
     ]
   "refresh": true
   ```

## Lots OSGi et modules de contenu inclus {#osgi-bundles-and-content-packages-included}

Les documents texte suivants répertorient les lots OSGi et les packages de contenu inclus dans [!DNL Experience Manager] 6.5.15.0 : <!-- UPDATE FOR EACH NEW RELEASE -->

* [Liste des lots OSGi inclus dans Experience Manager 6.5.15.0](/help/release-notes/assets/65150_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Liste des modules de contenu inclus dans Experience Manager 6.5.15.0](/help/release-notes/assets/65150_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Sites web à accès limité {#restricted-sites}

Ces sites Web sont disponibles uniquement pour les clients. Si vous êtes client et avez besoin d’un accès, contactez votre responsable de compte Adobe.

* [Téléchargement du produit à l’adresse licensing.adobe.com](https://licensing.adobe.com/)
* [Contacter l’assistance clientèle Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=fr).

>[!MORELIKETHIS]
>
>* Page des produits [[!DNL Experience Manager] ](https://business.adobe.com/fr/products/experience-manager/adobe-experience-manager.html)
>* Documentation [[!DNL Experience Manager]  6.5](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=fr)
>* [Abonnement aux mises à jour prioritaires de produits d’Adobe](https://www.adobe.com/subscription/priority-product-update.html)

