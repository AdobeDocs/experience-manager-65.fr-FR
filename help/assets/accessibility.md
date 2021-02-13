---
title: Accessibilité dans  [!DNL Experience Manager Assets]
description: Découvrez comment les fonctionnalités d’accessibilité d’ [!DNL Adobe Experience Manager] 6.5 [!DNL Assets]  aident les utilisateurs en situation de handicap.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 863d1bd3f0f188153fcbbb7256d3ac2e3b247f59
workflow-type: tm+mt
source-wordcount: '1919'
ht-degree: 90%

---


<!--
Possible topics to cover in this article are below.

* Compile a list of enhancements done in the last ~1 year.
* Showcase a few prominent use cases (search?) in a screencast.
* Top-level actions supported, such as clickable UI elements, keyboard shortcuts, popup dialogs, etc.
* List all UIs that are keyboard navigable.
* Unified list of the product tasks supported, such as, search assets, download assets, add or editing metadata, use DM Viewers, etc.
* Do we need to add support matrix of user tasks with browser and screen reader combinations. Everything may not work in all browsers and/or using all screen readers.
* Any exceptions that users should be aware of. It may help to call out (it may be done in ACR) what tasks are NOT supported.
* CTAs – what's next and more info from AEM team:
  * Link to ACRs on a.com.
  * Generic a11y info by Adobe to begin with.
  * Link to a11y-specific online methods to report issues, seek support, or request enhancements, if any. Asked the a11y team on Slack.
-->

# Fonctionnalités d&#39;accessibilité dans [!DNL Adobe Experience Manager Assets] {#accessibility-in-aem-assets}

[!DNL Adobe Experience Manager] permet aux créateurs et aux éditeurs de contenu de proposer des expériences étonnantes sur le web. Adobe s’efforce d’inclure les créateurs en situation de handicap en améliorant l’accessibilité d’[!DNL Experience Manager]. Le logiciel est continuellement amélioré pour répondre aux besoins de tous les types d’utilisateurs et appliquer les normes internationales afin d’inclure les personnes atteintes d’une déficience visuelle, auditive, de mobilité ou autre.

[!DNL Experience Manager] publie des informations sur la conformité qui décrivent les normes auxquelles il adhère, mettent en avant les fonctionnalités d’accessibilité du produit et définissent le niveau de conformité. Les rapports de conformité pour l’accessibilité aident les utilisateurs d’[!DNL Experience Manager] à comprendre le niveau d’adhésion à diverses normes. Les améliorations apportées à [!DNL Assets] permettent à tous les utilisateurs d’accéder facilement aux interfaces à l’aide d’un clavier, d’un lecteur d’écran, de loupes et d’autres technologies d’assistance.

[!DNL Experience Manager] offre divers niveaux de prise en charge des normes suivantes :

* [Web Content Accessibility Guidelines (WCAG) 2.1](https://www.w3.org/TR/WCAG/).
* [Révision de l’article 508 de la loi sur la réadaptation](https://www.access-board.gov/guidelines-and-standards/communications-and-it/about-the-ict-refresh/final-rule/text-of-the-standards-and-guidelines).
* [Initiative relative à l’accessibilité – Applications Internet riches et accessibles (WAI-ARIA) par W3C](https://www.w3.org/WAI/standards-guidelines/aria/).
* [EN 301 549](https://en.wikipedia.org/wiki/EN_301_549).

Pour lire un rapport contenant des détails sur le niveau de conformité, voir la page [Rapport de conformité pour l’accessibilité](https://www.adobe.com/accessibility/compliance.html) (ACR).

Pour savoir comment [!DNL Dynamic Media] est accessible, voir [accessibilité dans [!DNL Dynamic Media]](/help/assets/accessibility-dm.md).

## Technologies d’assistance {#at-support}

Les utilisateurs en situation de handicap font fréquemment appel au matériel et aux logiciels pour accéder au contenu web et utiliser des produits logiciels. Ces outils sont connus sous le nom de technologies d’assistance. [!DNL Experience Manager Assets] peut fonctionner avec les types suivants de technologies d’assistance (AT) pour l’utilisation des fonctionnalités de base du logiciel :

* Lecteurs d’écran et loupe d’écran.
* Logiciel de reconnaissance vocale.
* Utilisation du clavier – navigation et raccourcis.
* Matériel d’assistance, y compris commandes de commutation, affichages en braille actualisables et autres périphériques d’entrée sur ordinateur.
* Outils d’agrandissement de l’interface utilisateur.

## Cas d’utilisation d’[!DNL Experience Manager Assets] accessibles {#accessible-assets-use-cases}

Dans [!DNL Experience Manager], les fonctionnalités d’accessibilité répondent à deux exigences clés des utilisateurs de [!DNL Experience Manager] et de leurs clients.

* Pour les concepteurs et les créateurs de contenu, il existe des fonctionnalités permettant de créer et de publier du contenu accessible, qui est ensuite utilisé par leurs clients et les visiteurs du site web. Les personnes handicapées utilisent le contenu à l&#39;aide de technologies d&#39;assistance. Pour plus d’informations, reportez-vous aux [Directives d’accessibilité web](/help/managing/web-accessibility.md).
* [!DNL Experience Manager] permet de plus à ses utilisateurs et à ses administrateurs en situation de handicap d’accéder à l’interface utilisateur et aux contrôles pour créer et gérer du contenu. La personne présentant un handicap peut faire appel aux technologies d’assistance pour naviguer, utiliser et gérer les fonctionnalités d’[!DNL Assets].

Les principales fonctionnalités d’[!DNL Assets] sont plus accessibles qu’auparavant et sont régulièrement mises à jour afin d’améliorer la conformité aux normes mondiales. Les opérations CRUD d’[!DNL Assets] intègrent un certain degré d’accessibilité Les workflows DAM tels que l’ajout, la gestion, la recherche et la distribution de ressources sont accessibles à l’aide de raccourcis clavier, d’un texte de lecteur d’écran, d’un contraste de couleur, etc.

## Prise en charge de l’utilisation du clavier {#keyboard-use}

De nombreux éléments de l’interface utilisateur exploitables ou sur lesquels l’utilisateur peut cliquer peuvent également fonctionner avec un clavier. À l’aide du clavier, les utilisateurs peuvent se concentrer sur les éléments de l’interface et prendre les mesures appropriées. Les utilisateurs peuvent directement utiliser des raccourcis clavier pour déclencher une commande ou une action sans avoir à se concentrer sur les éléments de l’interface utilisateur et la déclencher via le clavier. Par exemple, les utilisateurs peuvent ouvrir la chronologie d’un fichier dans la partie gauche de l’interface utilisateur en accédant au contrôle d’interface utilisateur à l’aide d’un clavier et en sélectionnant `Return` raccourci clavier, puis `Alt + 2`.

<!-- TBD items:

* The option to toggle between list view and card view exposes relevant info to the screen readers. What about column view option? This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’.
* How to open and browse through the profile popup dialog in [!DNL Experience Manager] UI using a keyboard? The navigation does not match the order of visual display of options on the UI. This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’. What about setting preferences and impersonating a user?
* Using the [!DNL Experience Manager] tag browser and operating the options like delete tag? This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’.
* Read-only form fields can be focused with the keyboard. Can users tab to these fields to understand the contents and are they able to copy text from the fields?
-->

### Raccourcis clavier dans [!DNL Assets] {#keyboard-shortcuts}

Les actions suivantes d’[!DNL Assets] fonctionnent avec les raccourcis clavier répertoriés. La plupart des raccourcis clavier qui s’appliquent aux consoles [!DNL Experience Manager] s’appliquent également à [!DNL Assets]. Voir la section [Raccourcis clavier pour les consoles](/help/sites-authoring/keyboard-shortcuts.md#keyboard-shortcuts). Découvrez comment [activer ou désactiver les raccourcis clavier](/help/sites-authoring/keyboard-shortcuts.md#deactivating-keyboard-shortcuts).

| Interface utilisateur ou scénario | Raccourci clavier | Action |
|---|---|---|
| Mode Colonnes de l’interface utilisateur d’[!DNL Assets] | Touches fléchées Haut et Bas | Accéder aux fichiers et aux dossiers dans la même hiérarchie. |
| Mode Colonnes de l’interface utilisateur d’[!DNL Assets] | Touches fléchées gauche et droite | Accéder aux fichiers et aux dossiers situés au-dessus ou au-dessous du dossier en cours. |
| Navigation dans les dossiers d’[!DNL Assets] | `/` | Lancer la recherche en ouvrant la zone Omni-recherche. |
| Console [!DNL Assets] | ` | Activer/désactiver les rails |
| Console [!DNL Assets] | `Alt + 1` | Ouvrir l’arborescence de contenu. |
| Console [!DNL Assets] | `Alt + 2` | Ouvrez le rail de gauche [!UICONTROL Navigation]. |
| Console [!DNL Assets] | `Alt + 3` | Afficher la [!UICONTROL Chronologie] d’une ressource sélectionnée. |
| Console [!DNL Assets] | `Alt + 4` | Ouvrir les références Live Copy de la ressource sélectionnée. |
| Console [!DNL Assets] | `Alt + 5` | Recherche et recherche début dans le dossier sélectionné. |
| Ressource ou dossier sélectionné | Retour arrière | Supprimer la ressource ou le dossier sélectionné. |
| Ressource ou dossier sélectionné | `p` | Ouvrir la page Propriétés de la ressource sélectionnée. |
| Ressource ou dossier sélectionné | `e` | Modifier la ressource sélectionnée. |
| Ressource ou dossier sélectionné | `m` | Déplacer la ressource sélectionnée. |
| Ressource ou dossier sélectionné | `Ctrl + c` | Copier la ressource sélectionnée. |
| Ressource ou dossier sélectionné | `Esc` | Désélectionner la sélection. |
| La boîte de dialogue s’ouvre et est active | `Esc` | Fermer la boîte de dialogue. |
| Dans un dossier dans DAM | `Ctrl + v` | Coller la ressource copiée. |
| Console [!DNL Assets] | `Ctrl + A` | Sélectionner tous les fichiers. |
| Pages de propriétés d’Assets | `Ctrl + S` | Enregistrer les modifications. |
| Console [!DNL Assets] | `?` | Afficher la liste de raccourcis clavier. |

## Connexion à l’interface utilisateur d’[!DNL Assets] et navigation {#login}

Les utilisateurs peuvent se servir du clavier pour accéder au champ de connexion et le renseigner afin de se connecter. Les messages d’erreur dus à des combinaisons de nom d’utilisateur et de mot de passe incorrectes sur la page de connexion sont annoncés par les lecteurs d’écran chaque fois que l’erreur se produit.

Une fois connectés, les utilisateurs de DAM peuvent accéder à l’interface utilisateur d’[!DNL Assets] à l’aide du clavier. Le clavier permet d’accéder aux éléments de l’interface utilisateur, tels que le rail de gauche, les menus, le profil utilisateur, la barre de recherche, les fichiers et les dossiers, ainsi que les paramètres d’administration et de configuration. L’ordre de navigation via le clavier est de gauche à droite et de haut en bas. Lorsque vous naviguez à l’aide du clavier, une option exploitable sélectionnée est mise en évidence par un contraste accentué des couleurs et est annoncée par un lecteur d’écran. Le cas échéant, un lecteur d’écran annonce l’état (étendu, réduit et mixte, par exemple) des options de menu sélectionnées. En outre, le lecteur d’écran annonce l’objectif de l’option utilisable, au lieu de, par exemple, l’aspect ou l’emplacement de l’interface.

Si un utilisateur développe l’option d’aide ou de profil d’utilisateur à partir du menu, le lecteur d’écran annonce l’option ou l’état approprié. Si un utilisateur développe l’option de profil utilisateur, les options disponibles peuvent être sélectionnées à l’aide du clavier. Par exemple, un utilisateur peut emprunter l’identité d’un autre utilisateur. Si un utilisateur recherche une chaîne à partir de l’option [!UICONTROL Aide], un narrateur annonce « Recherche de l’aide » pour indiquer qu’une recherche est en cours.

<!-- TBD: Removing for now. Add a more informative video later. Host it on tv.adobe

![Keyboard navigation of top options in [!DNL Experience Manager] user interface](assets/keyboard-navigation-in-aem.gif)

*Figure: Navigating through the options at the top of [!DNL Experience Manager] user interface using `Tab` key.*
-->

## Parcourir les ressources et afficher les informations associées {#browse}

Dans l’interface utilisateur d’[!DNL Assets], les utilisateurs peuvent se servir du clavier pour parcourir la liste des ressources numériques existantes dans le référentiel DAM, prévisualiser ou télécharger une ressource, afficher les rendus générés, changer de vue, afficher la chronologie et l’historique des versions, afficher les commentaires et les références, et afficher et gérer les métadonnées.

<!-- TBD: Not sure about the following list items mean:

In [!DNL Experience Manager] header section, when navigating in browse mode, screen reader now announces,
  
  * Suggestions to search in Omnisearch.
  * The state as expanded or collapsed for Solutions, Help, Inbox and User options.
  * The Searching Help status message that is displayed when user enters a search string in Search for Help field under Help option
  * The error message if incorrect value is entered in Impersonate as field under User option and focus correctly moves to the text field (NPR-33804).

Review CQ-4282133 before adding - Close option in a coral-dialog wasn't accessible through keyboard, due to which user cannot trigger close option through keyboard press in version preview dialog. After fix, user can close dialog through close option using keyboard.

* CQ-4273122 - Assets of video/audio type will have aria-label in format "Multimedia player: <Title>" so users relying on screen-reader will get to know that they are video/audio assets.
-->

Lors de la navigation dans le référentiel de ressources, les fonctionnalités suivantes améliorent l’accessibilité :

* Le lecteur d’écran indique des alternatives textuelles qui décrivent l’objectif ou la fonctionnalité des icônes et non pas leur nom.
* Les utilisateurs peuvent accéder aux options de l’interface utilisateur interactive et les sélectionner dans la liste Références des ressources à l’aide des touches du clavier.
* Les éléments figurant dans chaque ligne en mode Liste sont annoncés comme éléments de la même ligne par les lecteurs d’écran.
* Lorsque vous naviguez à l’aide de la touche `Tab`, la sélection peut passer à l’option de fermeture dans l’aperçu de version.
* Lorsque vous utilisez le clavier pour naviguer, les options exploitables mises en surbrillance dans l’interface utilisateur s’affichent de manière plus visible par un contraste amélioré. L’utilisateur peut ainsi identifier plus facilement la zone sélectionnée.
* Utiliser la touche `Esc` pour supprimer les icônes d’action rapide du mode Miniature ne supprime pas la sélection via le clavier du dernier élément sélectionné.
* Une fois une ressource sélectionnée, le raccourci clavier `Alt + 4` ouvre la liste [!UICONTROL Références] dans le rail de gauche. À l’aide de la touche `Tab`, les utilisateurs peuvent parcourir les entrées de référence non nulles. En parcourant uniquement les entrées de référence non nulles, vous réduisez également les efforts nécessaires et les touches actionnées.
* Les commentaires relatifs à une ressource sont disponibles dans la chronologie de cette ressource, Elle est accessible grâce au rail gauche à l’aide d’un clavier ou d’un raccourci clavier.
* Les [!UICONTROL Paramètres d’affichage] d’[!DNL Experience Manager] sont accessibles à l’aide du clavier. L’utilisateur peut parcourir les tailles de carte disponibles à l’aide des touches fléchées, naviguer parmi ces tailles via les touches de tabulation et définir d’autres éléments dans la vue Paramètres d’affichage existante.

<!-- TBD: Gradually, as more enhancements are done in these categories, add more content.

## Add and upload digital assets {#upload}

## Configure and administer [!DNL Assets] {#config-admin}

* List the a11y fixes in workflows to configure and administer [!DNL Experience Manager Assets]?
* Some enhancements in Processing profiles creation or application to a folder?
* Some enhancements to metadata properties UI?
-->

## Gestion des ressources numériques {#manage-assets}

De nombreuses tâches de gestion des ressources, telles que les opérations CRUD, le téléchargement d’une ressource et l’ajout de métadonnées, sont accessibles à divers degrés. [!DNL Assets] vous permet d’accomplir les tâches à l’aide de diverses technologies d’assistance, telles qu’un lecteur d’écran et un clavier.

Regardez une démonstration vidéo indiquant comment utiliser un clavier pour [parcourir le référentiel et télécharger une ressource](https://youtu.be/K3dgqMRQJys).

Pour les opérations de métadonnées généralement effectuées par des rôles tels que les rôles d’administrateur et de spécialiste du marketing, les fonctionnalités suivantes améliorent l’accessibilité :

* L’option [!UICONTROL Enregistrer et fermer] de la page [!UICONTROL Propriétés] d’une ressource est désormais accessible à l’aide du clavier.
* Les lecteurs d’écran annoncent les options permettant de supprimer les balises sélectionnées dans l’onglet [!UICONTROL De base] des [!UICONTROL Propriétés] de ressource.
* Les utilisateurs peuvent utiliser la boîte de dialogue contextuelle du sélecteur de données à l’aide du clavier. L’élément d’interface utilisateur sélecteur de date est utilisé pour définir les heures d’ouverture et de fermeture, et pour sélectionner la date.
* La fonctionnalité glisser à l’aide du clavier s’exécute correctement dans l’[!UICONTROL éditeur de schéma de métadonnées] dans le mode de navigation du lecteur d’écran.
* Un utilisateur peut déplacer la sélection à l’aide du clavier vers le champ Ajouter un utilisateur ou Groupe sous [!UICONTROL Groupe d’utilisateurs fermé] dans l’onglet [!UICONTROL Autorisations] du dossier [!UICONTROL Propriétés].

## Recherche de ressources numériques {#search-assets}

Une recherche rapide et transparente de ressource décuple la vitesse du contenu. Les cas d’utilisation de la vitesse du contenu font partie des principales fonctionnalités d’[!DNL Assets]. Pour lancer une recherche à partir de la barre Omni-recherche, les utilisateurs peuvent se servir du raccourci clavier `/` ou de la touche `Tab` parallèlement aux lecteurs d’écran afin de localiser rapidement l’option de recherche. Le lecteur d’écran indique le nom de l’option avec la mention « Bouton de recherche » lorsque la sélection porte sur l’option de recherche ![option de recherche](assets/do-not-localize/search_icon.png). Les utilisateurs peuvent sélectionner `Return` pour ouvrir la boîte de dialogue Omni-recherche. Le lecteur d’écran indique non seulement le mot-clé saisi dans la zone de recherche, mais également les suggestions proposées par [!DNL Experience Manager Assets]. Les utilisateurs peuvent utiliser une combinaison de touches fléchées, la touche `Return` et la touche `Tab` pour accéder aux différentes options permettant de déclencher une recherche.

Les fonctionnalités suivantes permettent d’accéder à l’option de recherche :

* Le titre de la page, tel qu’il est disponible pour un lecteur d’écran, permet d’identifier la page comme page de recherche de ressources.
* Les utilisateurs recherchent des ressources dans le champ Omni-recherche. Les utilisateurs peuvent ouvrir l’option de recherche à l’aide du clavier ou d’un raccourci clavier `/`.
* Les utilisateurs peuvent commencer la saisie d’un mot-clé de recherche, puis sélectionner les suggestions automatiques à l’aide des touches fléchées. Il est possible de sélectionner la suggestion mise en évidence à l’aide de la touche `Return` et la suggestion sélectionnée fait l’objet d’une recherche dans les ressources.
* Les lecteurs d’écran peuvent identifier et indiquer les cases à cocher à l’état mixte (dans lesquelles, sauf si vous sélectionnez tous les prédicats imbriqués, les cases de premier niveau ne sont pas cochées et sont barrées) dans le panneau Filtres lors du filtrage des résultats de recherche.
* La sélection de l’utilisateur passe aux options de recherche une fois la zone Omni-recherche fermée.

Lors du filtrage des résultats de recherche :

* La page des résultats de recherche comporte un titre informatif améliorant la compréhension des utilisateurs du lecteur d’écran.
* Un lecteur d’écran affiche les options du filtre de recherche sous forme d’accordéons extensibles.
* Les prédicats comportant des options d’état mixte sont annoncés par les lecteurs d’écran.

## Partage de ressources {#share-assets}

<!-- TBD: Anything about accessibility in DA, BP? AAL team confirmed that there's no content for AAL a11y on helpx.
-->

Lors du partage de ressources, les fonctionnalités suivantes améliorent l’accessibilité :

* Un utilisateur peut déplacer la sélection à l’aide du clavier dans les champs Rechercher et Ajouter l’adresse électronique de la boîte de dialogue de partage de liens.

* Dans la boîte de dialogue de partage de liens, lorsque vous naviguez en mode de navigation, le lecteur d’écran :

   * Ne narrez pas les informations du tableau lorsque la boîte de dialogue est chargée.
   * Peut accéder à toutes les suggestions répertoriées.
   * Indique les suggestions affichées pour les champs Ajouter l’adresse électronique et Rechercher.

## Documentation accessible {#accessible-docs}

[!DNL Experience Manager] fournit une documentation accessible pour les personnes en situation de handicap. Les éléments suivants permettent de rendre l’offre de contenu accessible, tandis qu’Adobe continue d’améliorer le modèle et le contenu :

* Les lecteurs d’écran peuvent lire le texte.
* Un texte alternatif est disponible pour les images et les illustrations.
* La navigation au clavier est possible.
* Les ratios de contraste permettent de mettre en évidence certaines parties du site web de documentation.

## Rédiger des commentaires {#a11y-feedback}

Pour rédiger des commentaires, poser des questions et demander des améliorations du produit liées à l’accessibilité, utilisez les méthodes suivantes :

* Complétez le formulaire à l’adresse [www.adobe.com/accessibility/feedback.html](https://www.adobe.com/accessibility/feedback.html).
* Envoyez-nous un courrier électronique à l’adresse access@adobe.com.

>[!MORELIKETHIS]
>
>* [Fonctionnalités d’accessibilité dans [!DNL Dynamic Media]](/help/assets/accessibility-dm.md).
>* [Notes de mise à jour des améliorations apportées à chaque version](/help/release-notes/new-features-latest-service-pack.md) du Service Pack.
>* Conseils en matière d’accessibilité d’[[!DNL Adobe Experience Manager] ](/help/managing/web-accessibility.md)
>* [Rapports de conformité (ACR) et liste VPAT (Modèle volontaire d’accessibilité des produits) pour les solutions d’Adobe](https://www.adobe.com/accessibility/compliance.html).

