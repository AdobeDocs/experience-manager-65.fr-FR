---
title: Accessibilité des fonctionnalités et des interfaces  [!DNL Adobe Experience Manager Assets]
description: Découvrez comment les fonctionnalités d’accessibilité d’ [!DNL Adobe Experience Manager]  6.5 [!DNL Assets]  aident les utilisateurs en situation de handicap.
contentOwner: AG
feature: Asset Management
role: User, Developer, Leader
exl-id: 15555941-99a2-4586-8d7b-b22f3ec17805
solution: Experience Manager, Experience Manager Assets
source-git-commit: 3524c1e6d299576ac9691292fb29eb0cf8a48bc2
workflow-type: tm+mt
source-wordcount: '1881'
ht-degree: 56%

---

<!--
Possible topics to cover in this article are below.

* Compile a list of enhancements done in the last ~1 year.
* Showcase a few prominent use cases (search?) in a screencast.
* Top-level actions supported, such as clickable UI elements, keyboard shortcuts, popup dialogs, and so on.
* List all UIs that are keyboard navigable.
* Unified list of the product tasks supported, such as, search assets, download assets, add or editing metadata, use DM Viewers, and so on.
* Do we need to add support matrix of user tasks with browser and screen reader combinations. Everything may not work in all browsers and/or using all screen readers.
* Any exceptions that users should be aware of. It may help to call out (it may be done in ACR) what tasks are NOT supported.
* CTAs – what's next and more info from AEM team:
  * Link to ACRs on a.com.
  * Generic a11y info by Adobe to begin with.
  * Link to a11y-specific online methods to report issues, seek support, or request enhancements, if any. Asked the a11y team on Slack.
-->

# Fonctionnalités d’accessibilité d’[!DNL Adobe Experience Manager Assets] {#accessibility-in-aem-assets}

[!DNL Adobe Experience Manager] permet aux créateurs et aux éditeurs de contenu de proposer des expériences étonnantes sur le web. Adobe s’efforce d’inclure les créateurs et créatrices en situation de handicap en améliorant l’accessibilité des [!DNL Experience Manager]. Le logiciel est continuellement amélioré pour répondre aux besoins de tous les types d&#39;utilisateurs. Il est conforme aux normes mondiales qui s’appliquent aux personnes atteintes de déficiences visuelles, auditives, de mobilité ou autres.

[!DNL Experience Manager] publie des informations sur la conformité qui décrivent les normes auxquelles il adhère, mettent en avant les fonctionnalités d’accessibilité du produit et définissent le niveau de conformité. Les rapports de conformité pour l’accessibilité aident les utilisateurs d’[!DNL Experience Manager] à comprendre le niveau d’adhésion à diverses normes. Les améliorations apportées à [!DNL Assets] permettent à tous les utilisateurs d’accéder facilement aux interfaces à l’aide d’un clavier, d’un lecteur d’écran, de loupes et d’autres technologies d’assistance.

[!DNL Experience Manager] offre divers niveaux de prise en charge des normes suivantes :

* [Web Content Accessibility Guidelines (WCAG) 2.1](https://www.w3.org/TR/wcag/).
* [Révision de l’article 508 de la loi sur la réadaptation](https://www.access-board.gov/guidelines-and-standards/communications-and-it/about-the-ict-refresh/final-rule/text-of-the-standards-and-guidelines).
* [Initiative relative à l’accessibilité – Applications Internet riches et accessibles (WAI-ARIA) par W3C](https://www.w3.org/WAI/standards-guidelines/aria/).
* [EN 301 549](https://en.wikipedia.org/wiki/EN_301_549).

Pour lire un rapport contenant des détails sur le niveau de conformité, voir la page [Rapport de conformité pour l’accessibilité](https://www.adobe.com/accessibility/compliance.html) (ACR).

Pour en savoir plus sur l’accessibilité de [!DNL Dynamic Media], consultez [accessibilité dans  [!DNL Dynamic Media]](/help/assets/accessibility-dm.md).

## Technologies d’assistance {#at-support}

Les utilisateurs en situation de handicap font fréquemment appel au matériel et aux logiciels pour accéder au contenu web et utiliser des produits logiciels. Ces outils sont connus sous le nom de technologies d’assistance. [!DNL Experience Manager Assets] peut fonctionner avec les types suivants de technologies d’assistance (AT) pour l’utilisation des fonctionnalités de base du logiciel :

* Lecteurs d’écran et loupe d’écran.
* Logiciel de reconnaissance vocale.
* Utilisation du clavier – navigation et raccourcis.
* Matériel d’assistance, y compris commandes de commutation, affichages en braille actualisables et autres appareils d’entrée sur ordinateur.
* Outils d’agrandissement de l’interface utilisateur.

## Cas d’utilisation d’[!DNL Experience Manager Assets] accessibles  {#accessible-assets-use-cases}

Dans [!DNL Experience Manager], les fonctionnalités d’accessibilité répondent à deux exigences clés des utilisateurs de [!DNL Experience Manager] et de leurs clients.

* Pour les concepteurs et les créateurs de contenu, il existe des fonctionnalités permettant de créer et de publier du contenu accessible, qui est ensuite utilisé par leurs clients et les visiteurs du site web. Les personnes en situation un handicap peuvent utiliser le contenu à l’aide des technologies d’assistance. Pour plus d’informations, consultez [Directives d’accessibilité Web](/help/managing/web-accessibility.md).
* [!DNL Experience Manager] permet également à ses utilisateurs et administrateurs en situation de handicap d’accéder à l’interface utilisateur et aux contrôles de création et de gestion de contenu. La personne présentant un handicap peut faire appel aux technologies d’assistance pour naviguer, utiliser et gérer les fonctionnalités d’[!DNL Assets].

Les principales fonctionnalités d’[!DNL Assets] sont plus accessibles qu’auparavant et sont régulièrement mises à jour afin d’améliorer la conformité aux normes mondiales. Les opérations de CRUD en [!DNL Assets] sont dotées d&#39;un certain degré d&#39;accessibilité. Les workflows DAM tels que l’ajout, la gestion, la recherche et la distribution de ressources sont accessibles à l’aide de raccourcis clavier, d’un texte de lecteur d’écran, d’un contraste de couleur, etc.

## Prise en charge de l’utilisation du clavier {#keyboard-use}

De nombreux éléments de l’interface utilisateur cliquables ou exploitables à l’aide d’un pointeur peuvent également être utilisés à l’aide d’un clavier. À l’aide du clavier, les utilisateurs peuvent se concentrer sur les éléments de l’interface et prendre les mesures appropriées. Les utilisateurs peuvent directement utiliser des raccourcis clavier pour déclencher une commande ou une action sans avoir à se concentrer sur les éléments de l’interface utilisateur et la déclencher à l’aide du clavier. Par exemple, les utilisateurs peuvent ouvrir la chronologie d’une ressource dans la partie gauche de l’interface utilisateur. Accédez à la commande de l’interface utilisateur à l’aide du clavier, puis sélectionnez `Return` et `Alt + 2` raccourci clavier.

<!-- TBD items:

* The option to toggle between list view and card view exposes relevant info to the screen readers. What about column view option? This info can go into 'basic handling' info aka article to 'understand and use the workspace'.
* How to open and browse through the profile popup dialog in [!DNL Experience Manager] UI using a keyboard? The navigation does not match the order of visual display of options on the UI. This info can go into 'basic handling' info aka article to 'understand and use the workspace'. What about setting preferences and impersonating a user?
* Using the [!DNL Experience Manager] tag browser and operating the options like delete tag? This info can go into 'basic handling' info aka article to 'understand and use the workspace'.
* Read-only form fields can be focused with the keyboard. Can users tab to these fields to understand the contents and are they able to copy text from the fields?
-->

### Raccourcis clavier dans [!DNL Assets] {#keyboard-shortcuts}

Les actions suivantes d’[!DNL Assets] fonctionnent avec les raccourcis clavier répertoriés. La plupart des raccourcis clavier qui s’appliquent aux consoles [!DNL Experience Manager] s’appliquent également à [!DNL Assets]. Voir la section [Raccourcis clavier pour les consoles](/help/sites-authoring/keyboard-shortcuts.md#keyboard-shortcuts). Découvrez comment [activer ou désactiver les raccourcis clavier](/help/sites-authoring/keyboard-shortcuts.md#deactivating-keyboard-shortcuts).

| Interface utilisateur ou scénario | Raccourci clavier | Action |
|---|---|---|
| Mode Colonnes de l’interface utilisateur d’[!DNL Assets] | Touches fléchées Haut et Bas | Accédez aux fichiers et aux dossiers dans la même hiérarchie. |
| Mode Colonnes de l’interface utilisateur d’[!DNL Assets] | Touches fléchées gauche et droite | Accédez aux fichiers et aux dossiers situés au-dessus ou au-dessous du dossier en cours. |
| Navigation dans les dossiers d’[!DNL Assets] | `/` | Appelez une recherche en ouvrant la zone Omnisearch. |
| Console [!DNL Assets] | &grave; | Activer/désactiver les rails |
| Console [!DNL Assets] | `Alt + 1` | Ouvrir l’arborescence de contenu. |
| Console [!DNL Assets] | `Alt + 2` | Ouvrez le rail de gauche [!UICONTROL Navigation]. |
| Console [!DNL Assets] | `Alt + 3` | Afficher la [!UICONTROL Chronologie] d’une ressource sélectionnée. |
| Console [!DNL Assets] | `Alt + 4` | Ouvrir les références Live Copy de la ressource sélectionnée. |
| Console [!DNL Assets] | `Alt + 5` | Lance la recherche et effectue une recherche dans le dossier sélectionné. |
| Ressource ou dossier sélectionné | Retour arrière | Supprimer la ressource ou le dossier sélectionné. |
| Ressource ou dossier sélectionné | `p` | Ouvrez la page Propriétés de la ressource sélectionnée. |
| Ressource ou dossier sélectionné | `e` | Modifier la ressource sélectionnée. |
| Ressource ou dossier sélectionné | `m` | Déplacer la ressource sélectionnée. |
| Ressource ou dossier sélectionné | `Ctrl + c` | Copier la ressource sélectionnée. |
| Ressource ou dossier sélectionné | `Esc` | Annule la sélection. |
| La boîte de dialogue s’ouvre et reçoit le focus | `Esc` | Fermez la boîte de dialogue. |
| Dans un dossier dans DAM | `Ctrl + v` | Coller la ressource copiée. |
| Console [!DNL Assets] | `Ctrl + A` | Sélectionner tous les fichiers. |
| Pages de propriétés d’Assets | `Ctrl + S` | Enregistrer les modifications. |
| Console [!DNL Assets] | `?` | Afficher la liste de raccourcis clavier. |

## Connexion et navigation dans l’interface utilisateur [!DNL Assets] {#login}

Les utilisateurs peuvent utiliser le clavier pour accéder au champ de connexion et le renseigner afin de se connecter. Les lecteurs d’écran annoncent des messages d’erreur sur la page de connexion chaque fois qu’un utilisateur saisit une combinaison de nom d’utilisateur et de mot de passe incorrecte.

Une fois connectés, les utilisateurs de la gestion des ressources numériques peuvent naviguer dans l’interface utilisateur [!DNL Assets] à l’aide du clavier. Le clavier permet d’accéder aux éléments de l’interface utilisateur, tels que le rail de gauche, les menus, le profil utilisateur, la barre de recherche, les fichiers et les dossiers, ainsi que les paramètres d’administration et de configuration. L’ordre de navigation via le clavier est de gauche à droite et de haut en bas. Lorsque les utilisateurs naviguent à l’aide du clavier, l’interface utilisateur met en surbrillance l’option active avec un contraste des couleurs amélioré et les lecteurs d’écran la lisent. Le cas échéant, les lecteurs d’écran annoncent le statut (par exemple, développé, réduit ou mixte) des options de menu sélectionné. En outre, le lecteur d’écran annonce l’objectif de l’option utilisable, au lieu de, par exemple, l’aspect ou l’emplacement de l’interface.

Si un utilisateur développe l’option d’aide ou de profil utilisateur à partir du menu, le lecteur d’écran annonce l’option ou le statut approprié. Si un utilisateur développe l’option de profil utilisateur, les options disponibles peuvent être sélectionnées à l’aide du clavier. Par exemple, un utilisateur peut emprunter l’identité d’un autre utilisateur. Si un utilisateur recherche une chaîne à partir de l’option [!UICONTROL Aide], un narrateur annonce « Recherche de l’aide » pour indiquer qu’une recherche est en cours.

<!-- TBD: Removing for now. Add a more informative video later. Host it on tv.adobe

![Keyboard navigation of top options in [!DNL Experience Manager] user interface](assets/keyboard-navigation-in-aem.gif)

*Figure: Navigating through the options at the top of [!DNL Experience Manager] user interface using `Tab` key.*
-->

## Parcourir les ressources et afficher les informations associées {#browse}

Dans l’interface utilisateur d’[!DNL Assets], les utilisateurs peuvent utiliser le clavier pour parcourir les ressources numériques dans le référentiel de gestion des ressources numériques et prévisualiser ou télécharger une ressource. Les utilisateurs peuvent également afficher les rendus générés, changer de vue et consulter la chronologie, l’historique des versions, les commentaires et les références. En outre, les utilisateurs peuvent afficher et gérer les métadonnées.

<!-- TBD: Not sure about the following list items mean:

In [!DNL Experience Manager] header section, when navigating in browse mode, screen reader now announces,
  
  * Suggestions to search in Omnisearch.
  * The state as expanded or collapsed for Solutions, Help, Inbox and User options.
  * The Searching Help status message that is displayed when user enters a search string in Search for Help field under Help option
  * The error message if incorrect value is entered in Impersonate as field under User option and focus correctly moves to the text field (NPR-33804).

Review CQ-4282133 before adding - Close option in a coral-dialog was not accessible through keyboard, due to which user cannot trigger close option through keyboard press in version preview dialog. After fix, user can close dialog through close option using keyboard.

* CQ-4273122 - Assets of video/audio type will have aria-label in format "Multimedia player: <Title>" so users relying on screen-reader will get to know that they are video/audio assets.
-->

Lors de la navigation dans le référentiel de ressources, les fonctionnalités suivantes améliorent l’accessibilité :

* Un lecteur d’écran annonce des alternatives textuelles qui décrivent l’objectif ou la fonctionnalité des icônes au lieu de leurs noms.
* Les utilisateurs peuvent accéder aux options de l’interface utilisateur interactive et en placer le focus dans la liste des ressources Références à l’aide des touches du clavier.
* Les éléments figurant dans chaque ligne dans la vue Liste sont annoncés comme éléments de la même ligne par les lecteurs d’écran.
* Lorsque vous naviguez à l’aide de la touche `Tab`, la sélection peut passer à l’option de fermeture dans l’aperçu de version.
* Lorsque vous utilisez le clavier pour naviguer, les options d’interface utilisateur activables mises en surbrillance ont une orientation visuelle plus nette avec un contraste amélioré. L’utilisateur peut ainsi identifier plus facilement la zone sélectionnée.
* Utiliser la touche `Esc` pour supprimer les icônes d’action rapide du mode Miniature ne supprime pas la sélection via le clavier du dernier élément sélectionné.
* Une fois une ressource sélectionnée, le raccourci clavier `Alt + 4` ouvre la liste [!UICONTROL Références] dans le rail de gauche. À l’aide de la touche `Tab`, les utilisateurs peuvent parcourir les entrées de référence non nulles. En parcourant uniquement les entrées de référence non nulles, vous réduisez également les efforts nécessaires et les touches actionnées.
* Les commentaires relatifs à une ressource sont disponibles dans la chronologie de cette ressource, Il est accessible si vous accédez au rail de gauche à l’aide d’un clavier ou d’un raccourci clavier.
* Les [!UICONTROL Paramètres d’affichage] d’[!DNL Experience Manager] sont accessibles à l’aide du clavier. L’utilisateur peut parcourir les tailles de carte disponibles à l’aide des touches fléchées, naviguer parmi ces tailles via les touches de tabulation et définir d’autres éléments dans la vue Paramètres d’affichage existante.

<!-- TBD: Gradually, as more enhancements are done in these categories, add more content.

## Add and upload digital assets {#upload}

## Configure and administer [!DNL Assets] {#config-admin}

* List the a11y fixes in workflows to configure and administer [!DNL Experience Manager Assets]?
* Some enhancements in Processing profiles creation or application to a folder?
* Some enhancements to metadata properties UI?
-->

## Gestion des ressources numériques {#manage-assets}

De nombreuses tâches de gestion des ressources, telles que les opérations CRUD, le téléchargement d’une ressource et l’ajout de métadonnées, sont accessibles à divers degrés. [!DNL Assets] vous permettent d’accomplir les tâches à l’aide de diverses technologies d’assistance, telles qu’un lecteur d’écran et un clavier.

Pour les opérations de métadonnées généralement effectuées par des rôles, tels que les spécialistes marketing et les administrateurs, les fonctionnalités suivantes améliorent l’accessibilité :

* L’option [!UICONTROL Enregistrer et fermer] de la page Ressource [!UICONTROL Propriétés] est désormais accessible à l’aide du clavier.
* Les lecteurs d’écran annoncent les options permettant de supprimer les balises sélectionnées dans l’onglet [!UICONTROL  De base ] de la ressource [!UICONTROL Propriétés].
* Les utilisateurs peuvent utiliser la boîte de dialogue pop-up du sélecteur de date à l’aide du clavier. L’élément d’interface utilisateur du sélecteur de date permet de définir les heures d’activation et les heures de désactivation, puis de sélectionner une date.
* La fonctionnalité glisser à l’aide du clavier fonctionne correctement dans l’[!UICONTROL Éditeur de schéma de métadonnées] en mode de navigation du lecteur d’écran.
* Un utilisateur peut utiliser le clavier pour déplacer la sélection vers le champ **Ajouter un utilisateur ou un groupe**.

## Recherche de ressources numériques {#search-assets}

Une recherche rapide et transparente de ressource décuple la vitesse du contenu. Les cas d’utilisation de la vitesse du contenu font partie des principales fonctionnalités d’[!DNL Assets]. Pour lancer une recherche à partir de la barre Omnisearch, les utilisateurs peuvent utiliser des `/` de raccourci clavier ou des `Tab` ainsi que des lecteurs d’écran pour localiser rapidement l’option de recherche. Le lecteur d’écran indique le nom de l’option avec la mention « Bouton de recherche » lorsque la sélection porte sur l’option de recherche ![option de recherche](assets/do-not-localize/search_icon.png). Les utilisateurs peuvent sélectionner `Return` pour ouvrir la boîte de dialogue Omni-recherche. Le lecteur d’écran annonce non seulement le mot-clé saisi dans la zone de recherche, mais également les suggestions proposées par [!DNL Experience Manager Assets]. Les utilisateurs peuvent utiliser une combinaison de touches fléchées, la touche `Return` et la touche `Tab` pour accéder aux différentes options permettant de déclencher une recherche.

Les fonctionnalités suivantes permettent d’accéder à l’option de recherche :

* Le titre de la page, disponible pour un lecteur d’écran, permet d’identifier la page en tant que page de recherche de ressources.
* Les utilisateurs recherchent des ressources dans le champ Omni-recherche. Les utilisateurs peuvent ouvrir l’option de recherche à l’aide du clavier ou d’un raccourci clavier `/`.
* Les utilisateurs peuvent commencer la saisie d’un mot-clé de recherche, puis sélectionner les suggestions automatiques à l’aide des touches fléchées. Il est possible de sélectionner la suggestion mise en évidence à l’aide de la touche `Return` et la suggestion sélectionnée fait l’objet d’une recherche dans les ressources.
* Les lecteurs d’écran peuvent identifier et annoncer les cases à cocher de statut mixte dans le panneau Filtres lorsque les utilisateurs filtrent les résultats de la recherche. En mode mixte, la case à cocher de premier niveau est activée jusqu’à ce que les utilisateurs sélectionnent tous les prédicats imbriqués.
* Le focus de l’utilisateur se déplace vers les options de recherche une fois la zone Omnisearch fermée.

Lors du filtrage des résultats de recherche :

* La page des résultats de recherche comporte un titre informatif pour une meilleure compréhension des utilisateurs de lecteurs d’écran.
* Un lecteur d’écran annonce les options du filtre de recherche sous forme d’accordéons extensibles.
* Les lecteurs d’écran annoncent des prédicats qui incluent des options d’état mixte.

## Partage de ressources {#share-assets}

<!-- TBD: Anything about accessibility in DA, BP? AAL team confirmed that there's no content for AAL a11y on helpx.
-->

Lors du partage de ressources, les fonctionnalités suivantes améliorent l’accessibilité :

* Un utilisateur peut déplacer le focus à l’aide du clavier dans le champ Rechercher et ajouter une adresse électronique de la boîte de dialogue partage de liens.

* Dans la boîte de dialogue Partage de liens, lorsque vous naviguez en mode de navigation, les lecteurs d’écran :

   * N’indique pas les informations du tableau lorsque la boîte de dialogue est chargée.
   * Accédez à toutes les suggestions répertoriées.
   * Indique les suggestions affichées pour les champs Ajouter l’adresse électronique et Rechercher.

## Documentation accessible {#accessible-docs}

[!DNL Experience Manager] fournit une documentation accessible pour les personnes en situation de handicap. Les éléments suivants permettent de rendre l’offre de contenu accessible, tandis qu’Adobe continue d’améliorer le modèle et le contenu :

* Les lecteurs d’écran peuvent lire le texte.
* Le texte secondaire des images et illustrations est disponible.
* La navigation au clavier est possible.
* Les ratios de contraste permettent de mettre en évidence certaines parties du site web de documentation.

## Rédiger des commentaires {#a11y-feedback}

Pour fournir des commentaires, poser des questions et demander des améliorations du produit liées à l’accessibilité, utilisez les méthodes suivantes, envoyez-nous un e-mail à l’adresse `access@adobe.com`.

>[!MORELIKETHIS]
>
>* [Fonctionnalités d’accessibilité d’ [!DNL Dynamic Media]](/help/assets/accessibility-dm.md).
>* [Notes de mise à jour des améliorations apportées à chaque version de service pack](/help/release-notes/release-notes.md).
>* Conseils en matière d’accessibilité d’[[!DNL Adobe Experience Manager] ](/help/managing/web-accessibility.md)
>* [Rapports de conformité (ACR) et liste VPAT (Modèle volontaire d’accessibilité des produits) pour les solutions d’Adobe](https://www.adobe.com/accessibility/compliance.html).
