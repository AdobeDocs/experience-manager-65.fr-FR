---
title: 'Notes de mise à jour de la version 6.5 d’ [!DNL Adobe Experience Manager] '
description: Consultez les informations sur la mise à jour, y compris les nouveautés, la procédure d’installation et une liste complète des modifications pour  [!DNL Adobe Experience Manager]  6.5.
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
exl-id: 811fccbc-6f63-4309-93c8-13b7ace07925
source-git-commit: 7e225038e925468f6e4dbdcf1d3dce6eceee9292
workflow-type: tm+mt
source-wordcount: '7156'
ht-degree: 22%

---

# Notes de mise à jour du dernier pack de services [!DNL Adobe Experience Manager] 6.5 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in this release information, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!--
DO NOT DELETE THIS HIDDEN NOTE!      DO NOT DELETE THIS HIDDEN NOTE!
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, May 29, 2025. In addition, a list of Forms fixes and enhancements is added to this section.
-->

## Résumé de la version {#release-information}

| Produit | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Version | 6.5.25.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Type | Mise à jour du pack de services |
| Date | 21 mai 2026 <!-- UPDATE FOR EACH NEW RELEASE --> |
| URL de téléchargement | [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.25.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

Experience Manager 6.5.25.0 comprend de nouvelles fonctionnalités, des améliorations importantes demandées par les clients et clientes, ainsi que des correctifs de bugs. Elle comprend également des améliorations en termes de performances, de stabilité et de sécurité, basées sur la version 6.5 disponible depuis avril 2019.

Cette version du pack de services fournit 275 ports dorsaux sur Sites, Assets et Foundation, y compris des correctifs de bugs critiques et un renforcement de la sécurité. Cette version améliore également l’accessibilité dans l’ensemble de la création de Sites grâce à une navigation au clavier complète, une gestion de la mise au point, une sémantique ARIA, des améliorations du contraste des couleurs et un dimensionnement de la cible tactile conformes aux normes WCAG.

Crosswalk est disponible par défaut dans cette version, ce qui élimine la nécessité d’un package distinct ou d’une configuration distincte après l’installation.

Les back-ports de sécurité corrigent les vulnérabilités XSS et améliorent la gestion des métadonnées de ressources partagées.

Les fragments de contenu et l’API GraphQL bénéficient également d’améliorations de la fiabilité, couvrant les références aux images incorporées, la gestion des requêtes persistantes et la localisation de l’éditeur.

<!-- UPDATE FOR EACH NEW RELEASE -->

<!-- ## Key features and enhancements -->


## Correction de problèmes dans le pack de services 25 {#fixed-issues}

<!-- 6.5.25.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE? -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->


### [!DNL Sites]{#sites-6525}

#### Accessibilité {#sites-accessibility-6525}

* Les commandes glisser-déposer des lignes de tableau dans la vue Liste Sites fonctionnent désormais avec la navigation au clavier. Les utilisateurs d’un lecteur d’écran ou d’un clavier peuvent réorganiser les lignes et recevoir des commentaires pendant l’action. (SITES-24946)

* La barre d’outils Modifier la disposition présente désormais des libellés d’écran et de tablette plus petits dans une séquence de lecteur d’écran significative. Les utilisateurs entendent les libellés avec les mesures de règle associées au lieu de les entendre dans le désordre. (SITES-25291)
* La fenêtre modale contextuelle Nuancier gère désormais correctement le focus lorsqu’elle s’ouvre dans la fenêtre modale d’annotation. Le focus commence au niveau de l’en-tête modal au lieu de se déplacer directement vers le bouton d’échantillon sélectionné. (SITES-25275)
* La boîte de dialogue modale du teaser offre désormais un moyen accessible de déplacer la boîte de dialogue à l’aide du clavier. Les utilisateurs n’ont plus besoin d’une souris pour repositionner la fenêtre modale sur la page. (SITES-25226)
* Le mode Carte améliore l’accessibilité en supprimant le comportement inutile de la grille ARIA. Les utilisateurs de lecteurs d’écran reçoivent des informations de carte plus claires sans contrôles de navigation de grille qui ne correspondent pas à la disposition visuelle. (SITES-24933)
* Les info-bulles de la boîte de dialogue modale Supprimer s’affichent désormais de manière cohérente après des actions de survol répétées. Les utilisateurs peuvent éloigner le pointeur et revenir à l’icône pour lire à nouveau l’info-bulle. (SITES-24778)
* Le rail de gauche reçoit désormais le focus dans l’ordre prévu une fois que les utilisateurs l’ont ouvert à partir de la page d’accueil de Sites. Les utilisateurs d’un clavier et d’un lecteur d’écran peuvent passer du bouton de configuration au contenu du rail sans ignorer la zone développée. (SITES-24754)
* La gestion de focus fonctionne désormais de manière cohérente dans la boîte de dialogue modale du carrousel. Les utilisateurs d’un clavier et d’un lecteur d’écran peuvent commencer à l’en-tête modal et revenir au contrôle d’origine après avoir fermé la boîte de dialogue. (SITES-24716)
* La boîte de dialogue Sélection de lien renvoie désormais le focus au contrôle qui l’a ouverte une fois que les utilisateurs ont fermé la boîte de dialogue. Les utilisateurs d’un clavier et d’un lecteur d’écran ne perdent plus leur place après avoir fermé la boîte de dialogue. (SITES-24707)
* La boîte de dialogue modale Image ne déplace plus le focus vers le premier onglet ou le repère de la page principale lorsque les auteurs ouvrent ou ferment la boîte de dialogue. Le focus se déplace d’abord vers l’en-tête de la boîte de dialogue, puis revient au contrôle qui a ouvert la boîte de dialogue. (SITES-24693)
* Le rail Références gère désormais correctement le focus lorsqu’une boîte de dialogue modale s’ouvre. Les utilisateurs du clavier et du lecteur d’écran restent dans la boîte de dialogue jusqu’à ce qu’ils la ferment, puis continuent la navigation sans perdre de contexte. (SITES-24683)
* La boîte de dialogue modale de sélection du chemin d’accès hyperlien ne déplace plus le focus vers le mauvais champ ou contrôle lorsque les auteurs l’ouvrent ou le ferment. Le focus commence au titre modal et revient au bouton qui a ouvert la boîte de dialogue modale. (SITES-24672)
* La boîte de dialogue modale Teaser ne déplace plus le focus vers le premier onglet ou haut de la page lorsque les auteurs l’ouvrent ou la ferment. Le focus suit désormais le flux de boîte de dialogue attendu et réduit les annonces inutiles de lecteur d’écran. (SITES-24522)

* Le bouton de verrouillage de l’éditeur de page fournit désormais des commentaires plus précis du lecteur d’écran. Les lecteurs d’écran utilisent l’attribut de titre lorsqu’il est disponible, ce qui réduit les annonces verbeuses pour les auteurs qui utilisent la technologie d’assistance. (SITES-41431)
* La navigation au clavier ignore désormais le contenu masqué. Les utilisateurs peuvent parcourir les éléments d’interface visibles sans déplacer le focus vers du contenu qu’ils ne peuvent pas voir. (SITES-41430)
* Le focus au clavier revient désormais à l’élément de déclenchement une fois que les utilisateurs ont fermé une superposition. L’éditeur de page ne renvoie plus le focus au recouvrement, ce qui améliore la navigation pour les utilisateurs qui utilisent un clavier. (SITES-40819)
* La barre d’outils de l’éditeur de page affiche désormais des libellés, tels que des info-bulles, lorsque les utilisateurs parcourent les éléments de la barre d’outils à l’aide du clavier. Les utilisateurs peuvent comprendre chaque action de la barre d’outils lorsque le focus passe d’un élément à l’autre. (SITES-40751)
* Le survol des éléments de l’explorateur de composants ne supprime plus le focus d’un composant de texte actif. Les auteurs peuvent modifier le texte sans interruption et le focus au clavier reste prévisible. (SITES-35370)
* Les lecteurs d’écran annoncent désormais plus clairement le bouton Rechercher le sens du tri modal . Le libellé du bouton ne répète plus la même direction et décrit mieux le comportement du bouton (bascule). (SITES-25534)
* La boîte de dialogue modale de recherche affiche désormais un indicateur visuel pour l’option sélectionnée dans la zone de liste Modifier le fichier ou le dossier. Les utilisateurs peuvent identifier l’option de chemin de navigation actuelle sans se fier uniquement à la sélection. (SITES-25532)
* La boîte de dialogue modale de recherche augmente désormais le contraste du libellé Trier par . Le texte répond aux exigences d’accessibilité et améliore la lisibilité pour les utilisateurs et utilisatrices malvoyants. (SITES-25531)
* Les boutons de sélection d’appareil affichent désormais les informations correctes d’état actuel dans la barre d’outils Modifier la disposition . Les utilisateurs de lecteurs d’écran peuvent identifier l’appareil actif sans entendre un état de basculement trompeur. (SITES-25524)
* La navigation au clavier et dans le lecteur d’écran ferme désormais le menu Boîte de réception lorsque le focus le quitte. Les utilisateurs et utilisatrices évitent l’état déroutant où le menu reste ouvert tandis que le focus se déplace ailleurs. (SITES-25518)
* La navigation au clavier et dans le lecteur d’écran ferme désormais le menu Aide lorsque le focus le quitte. Le focus ne passe plus au contenu en dehors du menu tant que le menu reste ouvert. (SITES-25517)
* La page d’accueil Fragments de contenu fournit désormais un libellé accessible cohérent pour les onglets de barre latérale. NVDA annonce correctement le libellé de l’onglet lorsque les utilisateurs parcourent les commandes d’onglet. (SITES-25509)
* Les options ciblées du menu Informations sur la page répondent désormais aux exigences minimales en matière de contraste. Le contraste amélioré permet aux utilisateurs malvoyants d’identifier l’élément de menu principal. (SITES-25321)
* La navigation au clavier ignore désormais les contrôles masqués dans la barre d’outils Démographique réduite. Le focus reste sur les éléments interactifs visibles, ce qui améliore l’ordre de navigation dans l’aperçu de la disposition. (SITES-25304)
* Le bouton Rotation de l’appareil fournit désormais des commentaires plus clairs sur le lecteur d’écran dans la barre d’outils Modifier la disposition . Les lecteurs d’écran annoncent l’orientation actuelle et l’action qui la modifie. (SITES-25292)
* La barre d’outils Modifier la mise en page affiche désormais un état sélectionné clair pour le bouton Bureau. L’option Bureau correspond aux autres boutons de l’appareil et facilite l’identification de la vue active. (SITES-25290)
* La barre d’outils Modifier la disposition affiche désormais les libellés de la zone de la règle pour les technologies d’assistance. Les utilisateurs de lecteurs d’écran ne rencontrent plus de valeurs de mesure sans libellé lors de la modification de disposition. (SITES-25287)
* La barre d’outils Modifier la mise en page affiche désormais l’étiquette complète du bouton iPhone 8 Plus à l’état décoché. Le libellé n’est plus tronqué lorsqu’il y a suffisamment d’espace autour du bouton. (SITES-25284)
* Le problème signalé décrit un indicateur de focus dans la barre d’outils Modifier la mise en page qui semblait couvrir plusieurs commandes d’appareil. L&#39;inquiétude se concentrait sur les utilisateurs du clavier qui pourraient perdre la trace du contrôle actif lorsque le contour de focus incluait des boutons adjacents. Le problème fonctionnait comme prévu. (SITES-25283)
* Le problème signalé décrit les boutons modaux d’annotation qui annonçaient Annotation avant chaque libellé de bouton. L’inquiétude portait sur la sortie floue du lecteur d’écran pour des actions telles que l’annotation, les nuanciers et la suppression. (SITES-25277)
* Le texte du bouton d’annotation utilise désormais un contraste suffisant dans la boîte de dialogue modale d’annotation. Cette mise à jour améliore la lisibilité pour les utilisateurs malvoyants et prend en charge les exigences de contraste WCAG. (SITES-25267)
* Les lecteurs d’écran reçoivent désormais des mises à jour de statut lorsque les utilisateurs filtrent la liste Insérer un nouveau composant . La boîte de dialogue modale annonce les modifications de résultat afin que les utilisateurs comprennent que la liste a changé lors de la saisie. (SITES-25251)
* Le problème consigné décrit la sémantique d’en-tête manquante pour le titre modal de l’annotation. La préoccupation portait sur la navigation dans les lecteurs d’écran et la capacité à comprendre la structure modale. (SITES-25248)
* Les niveaux d’en-tête du rail latéral de l’éditeur de page suivent désormais une hiérarchie de contenu plus claire. La section du rail de gauche n’apparaît plus comme en-tête de page principal pour les technologies d’assistance. (SITES-25222)
* Le bouton Modifier du rail de gauche d’Assets dispose désormais d’une cible tactile plus large. Les utilisateurs à mobilité réduite peuvent activer le bouton plus facilement et éviter les commandes à proximité. (SITES-25221)
* Le rail de gauche d’Assets identifie désormais le moment où le bouton Modifier ouvre un nouvel onglet du navigateur. Les utilisateurs peuvent anticiper la modification de navigation au lieu de perdre du contexte de manière inattendue. (SITES-25220)
* Les titres des composants s’affichent désormais correctement lorsque les utilisateurs augmentent l’espacement du texte. Le rail latéral conserve les libellés lisibles et prend en charge les exigences d’espacement du texte WCAG. (SITES-25219)
* Le champ de filtre dans les composants de rail latéral expose désormais un nom accessible approprié. Cette mise à jour permet aux utilisateurs de lecteurs d’écran d’identifier le champ sans dépendre du texte d’espace réservé. (SITES-25212)
* Le problème signalé décrit une séquence de focus illogique en mode annotation. Les utilisateurs du clavier auraient raté la barre d’outils d’annotation, sauf s’ils ont utilisé Maj+Tab après avoir activé le mode . (SITES-24996)
* La zone de travail de l’éditeur affiche son titre dans la barre supérieure sous la forme d’un en-tête. Les lecteurs d’écran peuvent annoncer le titre avec la structure appropriée, ce qui améliore la navigation et la compréhension de la page. (SITES-24993)
* Le rapport d’accessibilité a noté un contraste insuffisant pour le message de statut de chargement qui s’affiche lorsque les utilisateurs changent de vue. La préoccupation portait sur la lisibilité pour les utilisateurs souffrant de déficience visuelle ou de daltonisme. (SITES-24991)
* Le rapport sur l’accessibilité a noté que les liens des cartes comportaient du texte non descriptif. L’objectif était d’aider les utilisateurs de lecteurs d’écran à comprendre chaque destination de lien sans contexte supplémentaire. (SITES-24975)
* La vue Liste de sites affiche désormais le texte de la Live Copy avec un contraste plus prononcé. La mise à jour améliore la lisibilité pour les auteurs malvoyants et pour les utilisateurs travaillant dans des conditions d’écran lumineux. (SITES-24956)
* La navigation au clavier déplace désormais le focus dans le menu Émulateur une fois que les utilisateurs l’ont développé. Ce comportement permet aux utilisateurs d’un lecteur d’écran ou d’un clavier d’accéder aux options de menu dans l’ordre prévu. (SITES-24954)
* La vue Liste des sites améliore désormais la visibilité des boutons de glisser-déposer dans les lignes du tableau. Les auteurs peuvent identifier plus facilement le contrôle lorsqu’ils réorganisent le contenu. (SITES-24951)
* Une carte n’expose plus le lien de l’image et le lien de l’en-tête comme des liens distincts lorsqu’ils partagent la même destination. La mise à jour réduit la verbosité du lecteur d’écran et améliore l’efficacité de la navigation. (SITES-24947)
* Les boutons du menu d’en-tête utilisent désormais des attributs d’accessibilité plus précis. Les lecteurs d’écran annoncent les boutons comme des commandes extensibles au lieu des commandes d’ouverture de boîte de dialogue. (SITES-24742)
* La boîte de réception marque désormais les liens associés avec des balises de liste sémantique. Les utilisateurs de lecteurs d’écran peuvent comprendre plus facilement le nombre et le regroupement des liens de la boîte de réception. (SITES-24730)
* Les libellés des boutons d’en-tête évitent désormais les noms accessibles détaillés. Les utilisateurs de lecteurs d’écran reçoivent des annonces plus claires sans informations de rôle en double du texte de l’icône. (SITES-24715)
* Le bouton Rapport CSV fournit désormais des commentaires plus clairs sur le comportement du nouvel onglet. Les utilisateurs peuvent comprendre que le fait de sélectionner le bouton ouvre un nouvel onglet du navigateur avant de l’activer. (SITES-24704)
* Les boîtes de dialogue modales utilisent désormais un balisage d’accessibilité plus précis pour les contrôles d’en-tête. Les boutons Aide et Activer/désactiver le plein écran restent des contrôles interactifs et n’apparaissent plus comme des en-têtes pour les lecteurs d’écran. (SITES-24696)
* Le repère du rail de filtrage utilise désormais un libellé distinct qui identifie son objectif. Les utilisateurs de lecteurs d’écran peuvent parcourir des pages avec plusieurs repères similaires en toute confiance. (SITES-24686)
* Les messages du rail de références offrent désormais une meilleure lisibilité aux utilisateurs qui dépendent d’un contraste de texte suffisant. Le problème signalé concernait des messages de sélection et de sélection multiple qui semblaient trop légers par rapport à leur arrière-plan. (SITES-24666)
* La fenêtre modale de recherche fournit désormais des cibles tactiles plus grandes pour les boutons Supprimer l’emplacement et Fermer . Ce changement permet aux utilisateurs présentant des tremblements de main, des spasmes ou une baisse de vision d’activer le contrôle prévu. (SITES-24530)
* Le lien d’en-tête Adobe Experience Manager a été signalé comme utilisant un attribut ARIA incorrect. Les tests ont confirmé que le lien contrôle le contenu extensible, de sorte que le statut accessible existant reste approprié. (SITES-24528)
* L’indicateur de focus du bouton Signature n’apparaît plus coupé dans la liste Composants . Le contour visible permet aux utilisateurs d’un clavier de suivre leur position dans l’éditeur. (SITES-24503)
* Un problème signalé décrit un équivalent textuel manquant pour l’icône d’info-bulle d’informations dans le panneau Composants. Le problème ne s’est pas reproduit, mais l’examen a confirmé que les icônes informatives doivent exposer un nom accessible clair. (SITES-24500)
* L’éditeur de page n’expose plus plusieurs repères de région avec le même libellé. Chaque point de repère possède désormais un nom accessible unique, de sorte que les utilisateurs et utilisatrices de lecteurs d’écran peuvent identifier la région actuelle. (SITES-24497)
* La commande Modifier le fichier ou le dossier sépare désormais le libellé de contrôle de ses informations d&#39;état. Les utilisateurs de lecteurs d’écran entendent un nom plus court et plus clair lorsqu’ils parcourent la commande d’en-tête. (SITES-24496)
* Les commandes interactives du tableau Administration de fragments de contenu prennent désormais en charge la navigation au clavier standard. Utiliser un clavier uniquement pour accéder aux boutons et aux liens au lieu de les découvrir uniquement par le biais de la navigation à touches fléchées. (SITES-24285)
* L’interface utilisateur d’administration de Sites traite désormais correctement les icônes décoratives du globe pour les lecteurs d’écran. Les icônes utilisent un texte secondaire vide afin que les utilisateurs n’entendent que du contenu d’interface significatif. (SITES-3057)

#### Interface d’utilisation d’administration{#sites-adminui-6525}

La console Sites affiche désormais correctement les paramètres de colonne enregistrés **Vue Liste**. Les colonnes sélectionnées restent cochées lorsque les auteurs rouvrent la boîte de dialogue des paramètres et le nombre de colonnes actives reste exact. (SITES-38576)

#### Interface utilisateur classique{#sites-classicui-6525}

Les boîtes de dialogue classiques de composant Texte de l’interface utilisateur affichent désormais le contenu de l’éditeur de texte enrichi sous forme de texte formaté au lieu d’HTML brut. Les auteurs peuvent modifier du texte existant sans passer en mode Source ni supprimer manuellement les balises. (SITES-38709)

#### Console des composants{#sites-component-console-6525}

* Les utilisateurs peuvent désormais rechercher des caractères localisés ou à plusieurs octets dans la console Composants. La console affiche également un libellé **Remove** localisé au lieu de la chaîne en anglais non traduite. (SITES-39747)
* La page Propriétés du composant localise désormais les chaînes dans Outils > Composants > Propriétés du composant. Les utilisateurs ne voient plus les libellés anglais non traduits dans les interfaces de création localisées. (SITES-39745)

#### [!DNL Content Fragments]{#sites-contentfragments-6525}

La recherche Assets répond désormais correctement lorsque les utilisateurs sélectionnent ou modifient des filtres. Le jeu de résultats filtré se met à jour comme prévu, ce qui restaure un affinement de recherche fiable dans la console Assets. (SITES-38686)

#### [!DNL Content Fragments] - Admin{#sites-admin-6525}

* La vue Liste d’Assets affiche désormais une info-bulle localisée Extrait par pour les fragments de contenu verrouillés. Ce correctif améliore la cohérence de la localisation lorsque les auteurs examinent les lignes de workflow. (SITES-42531)

* AEM localise désormais le libellé Principal dans la boîte de dialogue de téléchargement du fragment de contenu. Le correctif permet de maintenir la cohérence du workflow de téléchargement entre les paramètres régionaux non anglais. (SITES-42534)
* AEM traduit désormais le libellé de statut `Later` lorsque les auteurs planifient la publication de fragments de contenu à partir d’Assets. Ce correctif maintient la cohérence de la colonne Publié sur toutes les interfaces localisées. (SITES-42532)
* La création de fragments de contenu affiche désormais un message de validation localisé lorsque les auteurs saisissent des caractères non valides dans le champ Titre . La boîte de dialogue n’affiche plus la chaîne « Nom non valide fourni » non localisée. (SITES-19796)
* La page Modifier le fragment de contenu utilise désormais des libellés localisés pour les balises et les collections. Les auteurs voient les noms de champ traduits au lieu de chaînes anglaises non localisées. (SITES-977)

#### [!DNL Content Fragments] - Éditeur de fragments{#sites-fragments-editor-6525}

* Le contenu associé dans l’éditeur de fragment de contenu affiche désormais la chaîne localisée correcte lorsque les auteurs suppriment du contenu d’une collection. La boîte de dialogue ne remplace plus le nom du contenu par indéfini. (SITES-33675)
* L’éditeur de fragment de contenu affiche désormais un libellé Général traduit pour les onglets sans espace réservé configuré. Les interfaces localisées n’affichent plus la chaîne anglaise non traduite dans cette zone de l’éditeur. (SITES-30715)
* Le sélecteur de référence de contenu de l’éditeur de fragment de contenu affiche désormais les libellés localisés pour les types de ressources autorisés. Les interfaces localisées n’affichent plus de noms de type anglais pour les catégories de ressources prises en charge. (SITES-29699)

#### [!DNL Content Fragments] - API GraphQL {#sites-graphql-api-6525}

* Les réponses JSON GraphQL incluent désormais des références d’image incorporées à partir des champs de texte enrichi de fragments de contenu lorsque les noms des fichiers DAM contiennent des espaces ou des caractères non-ASCII. Ce correctif permet aux applications de générer des images référencées sans nécessiter que les auteurs renomment les ressources. (SITES-42191)
* Les réponses GraphQL pour les fragments de contenu gèrent désormais plus facilement les requêtes persistantes. Les mises à jour corrigent les en-têtes de cache en double, améliorent la gestion des variables codées et renvoient des réponses plus claires en cas de contenu manquant ou de requêtes ayant échoué. (SITES-40159)
* Les requêtes persistantes de GraphQL s’exécutent désormais sans messages ERREUR et AVERTISSEMENT inutiles dans les journaux. AEM gère correctement les variables codées afin que les requêtes réussies ne créent plus d’entrées `PersistedQueryServlet` trompeuses. (SITES-39354)

* La boîte de dialogue Modifier le point d’entrée GraphQL localise désormais ses chaînes d’interface. Les utilisateurs ne voient plus le schéma GraphQL non traduit extrait du message de configuration dans les interfaces localisées. (SITES-34018)

#### [!DNL Content Fragments] - Requêteur GraphQL{#sites-graphql-query-editor-6525}

Les utilisateurs peuvent désormais ouvrir le Query Editor GraphQL lorsque le nom du navigateur de configurations sélectionné contient des caractères CJC ou cyrilliques. L’éditeur affiche des requêtes persistantes pour le point d’entrée au lieu d’afficher une erreur. (SITES-31616)

#### [!DNL Content Fragments] - Modèles et éditeur de modèles{#sites-models-model-editor-6525}

* Un message de validation localisé s’affiche désormais dans l’éditeur de modèles de fragments de contenu lorsqu’une valeur sélectionnée nécessite un type de modèle valide. L’éditeur n’affiche plus le message en anglais non traduit dans les interfaces localisées. (SITES-41117)
* Le panneau de filtrage Modèle de fragment de contenu localise désormais ses chaînes de statut et de titre. Les utilisateurs ne voient plus les libellés non traduits tels que Titre du modèle, Statut, Brouillon, Activé et Désactivé. (SITES-30863)

<!-- #### [!DNL Content Fragments] - REST API{#sites-restapi-6525} -->

#### ContextHub{#sites-contexthub-6525}

ContextHub se charge désormais sans erreur JavaScript qui a interrompu la personnalisation. Les teasers et autres expériences personnalisées peuvent s’afficher correctement sur les pages affectées. (SITES-38430)

<!-- #### Core Backend{#sites-core-backend-6525} -->

#### Composants principaux{#sites-core-components-6525}

* AEM ne génère plus d’erreurs ThumbnailServlet répétées lorsqu’une requête cible une ressource DAM manquante. Le servlet arrête le traitement après la redirection, ce qui empêche les entrées NullPointerException d’inonder le journal d’erreurs. (SITES-41238)
* AEM n’indique plus les champs de boîte de dialogue facultatifs comme requis lorsque les auteurs rouvrent les boîtes de dialogue de composant. La boîte de dialogue concentre la validation sur les champs qui nécessitent réellement une entrée, ce qui empêche les erreurs de niveau onglet trompeuses. (SITES-40449)

* AEM comprend plusieurs correctifs de sécurité rétroportés qui renforcent Sites et les composants Cloud Services associés. Ces correctifs réduisent le risque de cross-site scripting et améliorent la gestion des requêtes sur les chemins de création affectés. (SITES-38314)
* La boîte de dialogue de configuration du composant Image v3 localise désormais les chaînes dans l’éditeur de page. Les auteurs ne voient plus les libellés non traduits lorsqu’ils configurent les composants Image dans des interfaces localisées. (SITES-38726)

<!-- #### Campaign integration{#sites-campaign-integration-6525} -->

<!-- #### ContentHub {#sites-contenthub-6525} -->

#### Passage Piétons {#sites-crosswalk-6525}

* Crosswalk ne nécessite plus de package séparé et de configuration après l&#39;installation. AEM comprend les lots requis, les packages de contenu, les utilisateurs système, les mappages d’utilisateurs de services et les basculements de fonctionnalités dans le package prêt à l’emploi. (SITES-41417)
* Les workflows Crosswalk fonctionnent désormais avec la prise en charge cq-wcm-core requise dans AEM 6.5. Les auteurs peuvent utiliser les actions Créer un modèle et Ouvrir l’éditeur universel sans mettre à jour les lots principaux distincts. (SITES-37666)

#### Fragments d’expérience{#sites-experiencefragments-6525}

AEM charge désormais les modèles corrects lorsque les auteurs créent des variations de fragments d’expérience et font défiler les 40 premiers résultats. Le sélecteur de modèles conserve le chemin d’accès au fragment d’expérience sélectionné pendant la pagination. (SITES-41531)

<!-- #### Foundation Components (Legacy){#sites-foundation-components-legacy-6525} -->

#### Lancements{#sites-launches-6525}

* La chronologie Sites localise désormais le message qui s’affiche lorsqu’AEM crée une version avant de promouvoir un lancement. Les utilisateurs ne voient plus la chaîne anglaise non traduite dans les interfaces localisées. (SITES-39157)
* La liste Lancements affiche désormais la description correcte des lancements créés sans héritage de modèle ou de Live Copy. Les utilisateurs ne voient plus le libellé de modèle remplacé trompeur. (SITES-34229)

<!-- #### Link Checker{#sites-link-checker-6525} -->

#### Localisation{#sites-localization-6525}

* Les propriétés des composants de texte dans les fragments d’expérience utilisent désormais des libellés localisés. Le menu Format n’affiche plus de chaînes non localisées pour les choix de paragraphe, d’en-tête, de guillemet ou de texte préformaté. (SITES-15091)

* Le texte de statut du modèle s’aligne désormais correctement dans **Outils** > **Général** > **Modèles**. Les libellés de statut mis à jour, activé et publié s’affichent sur une ligne horizontale. (SITES-36797)
* La boîte de dialogue Déplacer la page affiche désormais le libellé Sélectionner la date et l’heure complet. Le libellé n’est plus tronqué dans les interfaces localisées telles que le français. (SITES-36795)
* La section Assets de l’éditeur de modèles affiche désormais un libellé Balises traduit. Les interfaces de création localisées présentent des libellés cohérents lors de la configuration du modèle. (SITES-33770)
* Les descriptions des politiques de page s’affichent désormais correctement dans l’éditeur de modèles. Les utilisateurs peuvent lire le guide complet des classes CSS par défaut sans texte tronqué dans l’onglet Styles . (SITES-29724)
* L’éditeur de modèles affiche désormais une erreur localisée lorsqu’un auteur tente de faire glisser un composant sur un modèle supprimé. Le message n’apparaît plus comme une chaîne « while processing » non traduite. (SITES-19313)
* Le libellé « Cible » dans la fenêtre Configuration du teaser s’affiche désormais avec du texte localisé. La section Lien hypertexte n’affiche plus la chaîne anglaise dans les paramètres régionaux non anglais. (SITES-18622)
* La boîte de dialogue Démarrer le workflow dans l’éditeur de page affiche désormais les libellés d’action de workflow localisés. Les auteurs ne voient plus les chaînes anglaises pour les options de workflow. Les options incluent les actions d’approbation, de publication, de demande et de dépublication. (SITES-18103)
* Le menu déroulant Parent dans le panneau de modification Séparateur affiche désormais les chaînes localisées sans troncature. Les auteurs peuvent consulter le libellé complet lorsqu’ils configurent le composant. (SITES-17480)
* L’éditeur de page affiche désormais des libellés localisés pour « Pleine largeur » et « Largeur fixe » dans le menu Styles des composants de conteneur. Les auteurs qui utilisent des paramètres régionaux pris en charge ne voient plus ces chaînes en anglais. (SITES-17478)
* Les auteurs peuvent désormais lire l’info-bulle complète dans la zone Propriétés de navigation de la console Modèles . L’interface utilisateur aligne l’info-bulle et empêche la troncature du texte lors de la modification du modèle. (SITES-15480)
* Les auteurs peuvent désormais lire l’intégralité du libellé « Forms et documents utilisant un modèle » dans le panneau latéral Références. La console Modèles ne coupe plus la chaîne pour les paramètres régionaux pris en charge. (SITES-13167)
* La vue Références utilise désormais du texte localisé pour le message d’erreur d’actualisation. Les auteurs voient les messages traduits lorsqu’AEM ne peut pas mettre à jour la liste de références. (SITES-13102)
* La validation du formulaire identifie désormais le champ qui contient une valeur temporelle non valide. La boîte de dialogue modale Distorsion du temps affiche un message d’erreur plus clair afin que les auteurs puissent corriger le champ Heures ou Minutes concerné. (SITES-10980)
* La console Modèles affiche désormais un libellé Assets localisé dans la boîte de dialogue Sélectionner une image . Le libellé s’affiche correctement lorsque les auteurs parcourent les ressources à partir des propriétés du modèle. (SITES-8113)

#### MSM - Live Copies{#sites-msm-live-copies-6525}

* L’aperçu de la Live Copy localise désormais les formats de date dans la vue État de la relation . Les champs **Dernière modification du Source de Live Copy**, **Dernière modification de la Live Copy** et **Dernier déploiement** affichent les dates qui correspondent aux paramètres régionaux de l’utilisateur. (SITES-40756)
* MSM consigne désormais plus de détails sur les événements de notification push-on-modify. Les informations d’événement ajoutées aident les équipes à suivre l’activité de déploiement et à identifier la source des modifications de page inattendues. (SITES-38029)

#### Éditeur de page{#sites-pageeditor-6525}

* Les auteurs peuvent désormais créer des balises qui incluent des majuscules ou des espaces et les appliquer lors du premier enregistrement des propriétés de page. AEM crée la balise et écrit la valeur correcte dans les métadonnées de la page au cours de la même opération. (SITES-42550)

* Les auteurs peuvent désormais créer des fragments de contenu dans des dossiers de gestion des ressources numériques dont les noms contiennent une apostrophe. AEM gère correctement le chemin du dossier codé et ne déclenche plus d’exception NullPointerException lors de la création. (SITES-38653)

* AEM prend désormais en charge les actions de copier-coller pour les composants de fragment de contenu configurés dans l’éditeur de page. Le composant conserve sa référence de fragment de contenu, de sorte que les auteurs et autrices puissent dupliquer du contenu sans avoir à le recréer manuellement. (SITES-41586)
* L’éditeur de page affiche désormais correctement les info-bulles de description du premier champ dans les boîtes de dialogue des composants. Les descriptions longues restent visibles, ce qui permet aux auteurs de consulter les instructions de champ sans perdre de texte en haut de l’info-bulle. (SITES-39937)
* Les auteurs peuvent désormais ouvrir la boîte de dialogue Lien de l’éditeur de texte enrichi lorsqu’ils utilisent AEM via HTTP. Le correctif restaure la modification des liens pour les environnements on-premise qui n’utilisent pas HTTPS. (SITES-39467)

<!-- #### Replication{#sites-replication-6525} -->

<!-- #### Rich Text Editor{#sites-rte-6525} -->

#### Éditeur universel {#sites-universal-editor-6525}

* L’éditeur universel ne s’ouvre plus en mode Aperçu par défaut. AEM envoie les utilisateurs dans l’environnement de production de l’éditeur universel, sauf s’ils demandent explicitement un comportement de prévisualisation. (SITES-37193)
* L’éditeur universel s’ouvre désormais en mode Aperçu pour les environnements de développement, de développement rapide et d’évaluation d’AEM. La commande Ouvrir utilise le comportement d’aperçu correct pour les instances hors production. (SITES-33839)

### [!DNL Assets] {#assets-6525}

* La bibliothèque cliente Mes partages gère désormais les données de titre des ressources partagées en toute sécurité avant de les ajouter au balisage de la page. Les pages de partage générées n’exposent plus les utilisateurs à l’injection de script via des métadonnées de ressources manipulées. (ASSETS-60898)

* Les licences Adobe Stock fonctionnent désormais correctement dans l’interface utilisateur d’Assets. Le bouton Licence ne reste plus désactivé une fois qu’AEM a chargé le profil de ressource stock et les données de droits. (ASSETS-62610)
* La notification d’expiration de ressource prête à l’emploi gère désormais correctement les dates de quasi-expiration. Les e-mails de rappel s’exécutent lorsque le temps restant atteint le seuil configuré au lieu d’ignorer les ressources avec un délai d’expiration de huit jours. (ASSETS-57857)

* AEM Assets restaure désormais la navigation au clavier une fois que les utilisateurs ont choisi une recherche enregistrée. L’interface permet aux utilisateurs de quitter la liste déroulante sans actualiser ni redémarrer la vue Assets. (ASSETS-52061)

* Le workflow de téléchargement Vue Administration conserve désormais correctement les noms des fichiers ZIP. Le téléchargement d’une ressource ZIP ne génère plus de nom de fichier avec une double extension .zip. (ASSETS-62207)
* Le workflow de référence d’Assets gère désormais correctement les espaces dans les noms de fichier. Les mises à jour des ressources associées n’échouent plus lorsqu’un nom de fichier sélectionné comprend un ou plusieurs espaces. (ASSETS-56418)

#### [!DNL Dynamic Media]{#assets-dm-6525}

Le menu déroulant Sous-titres et pistes audio affiche désormais l’arabe comme langue prise en charge dans Dynamic Media. Cette mise à jour permet aux utilisateurs d’ajouter des pistes de sous-titres en arabe sans solution personnalisée. (ASSETS-61771)

### [!DNL Forms]{#forms-6525}

>[!NOTE]
>
>Les correctifs d’[!DNL Experience Manager] Forms sont fournis par le biais d’un package complémentaire distinct une semaine après la date de publication prévue du pack de services [!DNL Experience Manager] . Dans ce cas, la publication du package complémentaire est prévue pour le jeudi 28 mai 2026. De plus, une liste des correctifs et améliorations de Forms est ajoutée à cette section.



<!-- ALL THE FORMS BUG FIXES LISTED BELOW GO WITH AEM 6.5.25 FORMS MAY 28 2026 RELEASE!! UNHIDE THEM!! -->




<!-- #### Forms Designer {#forms-designer-6525} -->

<!-- 
* The Output API now handles dynamic form content consistently when PDF generation uses client rendering. Generated PDFs retain scripted description text across affected sections instead of leaving some fields blank. (LC-3928858)
* Document of Record generation now handles repeated panel pagination correctly when parent and child panels use the same "Place Top of Next Page" configuration. Authors no longer lose child panel data during the first repeated panel instance in generated output documents. (LC-3923274)
* Long multiline text fields in PDF preview now flow correctly across pages. The generated PDF no longer duplicates page content or drops hidden text during printing. (LC-3924324)
* Fillable PDFs now reset accessibility data when users clear form fields. Screen readers announce the cleared state correctly instead of reading old field values that no longer appear in the form. (LC-3923872)
* The Accessibility Checker now handles Nepali text correctly during PDF validation. Users can check Nepali-language documents without false accessibility errors tied to character encoding. (LC-3922988) 
-->

<!-- #### XMLFM {#forms-xmlfm-6525} -->

<!-- 
* Generated PDFs now include proper tags for supported form fields that use borders in the template. Screen readers can identify numeric fields, date fields, text fields, and checkboxes more reliably. (LC-3923534)
* Document of Record output now applies the correct tag structure to supported fields that include borders in the template. Numeric, date, text, and checkbox fields remain accessible in the generated PDF. (LC-3923265)
-->

<!-- #### XTG {#forms-xtg-6525} -->

<!-- 
* Forms output now merges XML data correctly when generatePDFOutputBatch generates PDFs in batch mode. The batch process no longer creates documents with blank or missing merged fields. (LC-3924192) 
* Document of Record output now includes nested child panels in the first occurrence of a repeatable panel. Forms that use Top of Next Page pagination no longer drop child panel data from the generated output. (LC-3923923)
* Custom bullet characters in XDP templates now map correctly for accessible PDF output. PAC validation no longer reports that text object characters cannot map to Unicode. (LC-3923079) 
-->


### Foundation {#foundation-6525}

#### Apache Felix {#foundation-apachefelix-6525}

Le démarrage connecte désormais correctement le service CredentialsSupport pour l’authentification Felix. Cela évite les erreurs de dépendance qui peuvent affecter l’authentification des jetons au démarrage d’AEM. (GRANITE-63186)

<!-- #### Campaign{#foundation-campaign-6525} -->

<!-- #### Cloud Services{#foundation-cloudservices-6525} -->

<!-- #### Communities {#foundation-communities-6525} -->

<!-- #### Content distribution{#foundation-content-distribution-6525} -->

#### CRX {#foundation-crx-6525}

L’édition de fichiers JSP fonctionne désormais comme prévu dans CRXDE Lite après les mises à niveau d’AEM 6.5. L’éditeur CodeMirror charge le contenu du fichier au lieu de laisser l’onglet JSP vide. (GRANITE-64333)

<!-- #### Granite{#foundation-granite-6525} -->

<!-- #### Integrations{#foundation-integrations-6525} -->

<!-- #### Jetty{#foundation-jetty-6525} -->

#### Localisation{#foundation-localization-6525}

* La boîte de dialogue de chargement de certificat dans Sécurité > Trust Store affiche désormais les libellés de format de données localisés. Les utilisateurs ne voient plus les libellés anglais non localisés lorsqu’ils ajoutent un certificat. (NPR-43412)

* La boîte de dialogue Créer KeyStore aligne désormais le bouton Annuler sur les autres boutons de la boîte de dialogue. La mise en page du bouton reste cohérente et ne se déplace plus hors de l’alignement. (NPR-43291)
* La boîte de dialogue Vérifier dans **Sécurité** > Configurations **Adobe IMS** affiche désormais un texte de confirmation localisé. Les messages check et delete n&#39;apparaissent plus comme des chaînes anglaises non localisées. (NPR-43289)
* Les libellés d’interface utilisateur localisés apparaissent désormais correctement dans les boîtes de dialogue concernées et dans l’onglet Keystore . Les valeurs Aria-label utilisent des chaînes traduites et les libellés des champs de mot de passe s’affichent sans troncature. (NPR-43285)
* Le workflow Créer un nouvel utilisateur affiche désormais les erreurs de validation localisées pour les caractères non valides. Les utilisateurs reçoivent un message clair et traduit au lieu d’une chaîne IllegalArgumentException non localisée. (GRANITE-52920)

<!-- #### Oak {#foundation-oak-6525} -->

#### Plateforme{#foundation-platform-6525}

* Le bouton Afficher les références de balise affiche désormais le nombre de références de la balise sélectionnée. Cette mise à jour permet aux utilisateurs de comprendre l’utilisation des balises sans navigation supplémentaire. (CQ-4355509)
* La boîte de dialogue Déplacer du balisage positionne désormais correctement les messages de validation. Le texte d’erreur ne couvre plus l’icône du chemin de recherche lorsque les utilisateurs envoient la boîte de dialogue avec un champ obligatoire vide. (CQ-4353009)

#### Sécurité{#foundation-security-6525}

AEM place sur la liste autorisée désormais des mots-clés supplémentaires contenant le secret client. La création de configuration n’échoue plus lorsque les intégrations prises en charge utilisent ces modèles de dénomination client-secret. (GRANITE-66495)

<!-- #### Sling{#foundation-sling-6525} -->

<!-- #### SPA editor {#foundation-spa-editor-6525} -->

#### Traduction{#foundation-translation-6525}

Le statut des projets de traduction est désormais correctement mis à jour après la mise à niveau. Les auteurs peuvent réviser les valeurs de brouillon, en cours et terminées sans avoir à se fier aux métadonnées obsolètes du comportement du Service Pack précédent. (NPR-43418)

#### Interface d’utilisation{#foundation-ui-6525}

* Les URL de la console Sites saisies manuellement se résolvent désormais sur la page ou le chemin d’accès au dossier prévu. La hiérarchie du contenu reste cohérente après l’actualisation et ne retourne plus à l’URL de base. (NPR-43688)
* La suite de tests du gestionnaire de packages Adobe CRX n’échoue plus après la mise à niveau d’une instance AEM 6.5 LTS SP1 vers LTS SP2. Le test du servlet de liste de miniatures se termine désormais comme prévu. (NPR-43534)

* L’arborescence de contenu de la console Sites se charge désormais de manière cohérente après chaque actualisation du navigateur. Le rail de gauche vierge ou le message « Il n’y a aucun élément » disparaît lorsque le contenu existe. (NPR-43442)

<!-- #### WCM{#foundation-wcm-6525} -->

#### Workflow{#foundation-workflow-6525}

* L’éditeur de modèle de workflow valide désormais correctement les chemins de modèle de workflow spécifiques au client. Les clients qui stockent des modèles de workflow sous des chemins d’accès /conf au niveau du client peuvent modifier ces modèles sans les déplacer vers des chemins d’accès de configuration globaux. (GRANITE-65376)

* L’éditeur de modèle de workflow normalise désormais les chemins d’accès aux fichiers Windows lors de la validation du chemin. Les auteurs peuvent modifier les modèles de workflow sur les serveurs Windows sans erreurs d’accès bloquant les mises à jour des modèles. (GRANITE-63692)
* La création de tâche inclut désormais la validation côté serveur des dates d’échéance. Les utilisateurs ne peuvent pas créer de tâches dont l’échéance est antérieure à la date de début, ce qui permet de conserver la cohérence des données de tâche de la boîte de réception. (CQ-4362253)
* La création d’espace de noms gère désormais correctement le texte localisé. Les utilisateurs peuvent saisir des caractères non latins dans le champ Titre et créer l’espace de noms sans erreur de validation. (CQ-4355587)

## Installer [!DNL Experience Manager] 6.5.25.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.25.0 nécessite [!DNL Experience Manager] 6.5. Consultez la [documentation de mise à niveau](/help/sites-deploying/upgrade.md) pour obtenir des instructions détaillées. <!-- UPDATE FOR EACH NEW RELEASE -->
* Le téléchargement du pack de services est disponible dans la [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.25.0.zip) d’Adobe.
* Lors d’un déploiement avec MongoDB et plusieurs instances, installez [!DNL Experience Manager] 6.5.25.0 sur l’une des instances de création à l’aide du gestionnaire de modules.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe ne recommande pas de supprimer ou de désinstaller le package [!DNL Experience Manager] 6.5.25.0. Par conséquent, avant d’installer le module, vous devez créer une sauvegarde du `crx-repository` au cas où vous auriez besoin de le restaurer. <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- FORMS For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->

### Installer le pack de services dans [!DNL Experience Manager] 6.5{#install-service-pack}

1. Redémarrez l’instance avant l’installation si l’instance est en mode de mise à jour (lorsque l’instance a été mise à jour à partir d’une version antérieure). Adobe recommande un redémarrage si le temps de disponibilité actuel d’une instance est élevé.

1. Avant l’installation, prenez un instantané ou exécutez une sauvegarde récente de votre instance [!DNL Experience Manager].

1. Téléchargez le pack de services à partir de [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.25.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Ouvrez le gestionnaire de modules et cliquez sur **[!UICONTROL Charger le module]** pour charger le module. Pour en savoir plus, consultez la section [Gestionnaire de modules](/help/sites-administering/package-manager.md).

1. Sélectionnez le module, puis sélectionnez **[!UICONTROL Installer]**.

1. Pour mettre à jour le connecteur S3, arrêtez l’instance après l’installation du pack de services, remplacez le connecteur existant par un nouveau fichier binaire fourni dans le dossier d’installation, puis redémarrez l’instance. Consultez la section [Entrepôt de données S3 Amazon](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>La boîte de dialogue de l’interface d’utilisation du gestionnaire de modules se ferme occasionnellement pendant l’installation du pack de services. Adobe recommande d’attendre que les journaux d’erreurs se stabilisent avant d’accéder au déploiement. Attendez les journaux spécifiques liés à la désinstallation de la mise à jour complète pour vous assurer que l’installation est réussie. En règle générale, ce problème se produit dans [!DNL Safari], mais peut se produire par intermittence sur n’importe quel navigateur.

**Installation automatique**

Vous pouvez utiliser deux méthodes différentes pour installer automatiquement [!DNL Experience Manager] 6.5.25.0.<!-- UPDATE FOR EACH NEW RELEASE -->

* Placez le package dans le dossier `../crx-quickstart/install` lorsque le serveur est disponible en ligne. Le package est automatiquement installé.
* Utilisez l’[API HTTP à partir du gestionnaire de modules](/help/sites-administering/package-manager.md#package-share). Utilisez `cmd=install&recursive=true` afin que les packages imbriqués soient installés.

>[!NOTE]
>
>Experience Manager 6.5.25.0 ne prend pas en charge l’installation Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Validation de l’installation**

Pour connaître les plateformes certifiées pour travailler avec cette version, reportez-vous à la section des [exigences techniques](/help/sites-deploying/technical-requirements.md).

1. La page d’informations sur les produits (`/system/console/productinfo`) affiche le numéro de version mis à jour `Adobe Experience Manager (6.5.25.0)` sous [!UICONTROL Produits installés]. <!-- UPDATE FOR EACH NEW RELEASE -->.

1. Tous les bundles OSGi sont au statut **[!UICONTROL ACTIF]** ou **[!UICONTROL FRAGMENT]** dans la console OSGi (utilisez la console web : `/system/console/bundles`).

1. Le lot OSGi `org.apache.jackrabbit.oak-core` est de la version 1.22.20 ou ultérieure (utilisez la console web : `/system/console/bundles`). <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE. CHECK WITH SAMEER DHAWAN -->

### Installer le pack de services pour [!DNL Experience Manager] Forms{#install-aem-forms-add-on-package}

Pour obtenir des instructions sur l’installation du pack de services pour Experience Manager Forms, consultez les [instructions d’installation du pack de services Experience Manager Forms](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

>[!NOTE]
>
>La fonctionnalité de formulaires adaptatifs, disponible dans [AEM 6.5 QuickStart](https://experienceleague.adobe.com/fr/docs/experience-manager-65/content/implementing/deploying/deploying/deploy), est conçue à des fins d’exploration et d’évaluation uniquement. Pour une utilisation à des fins de production, il est essentiel d’obtenir une licence valide pour AEM Forms, car la fonctionnalité de formulaires adaptatifs nécessite une licence appropriée.

### Installer le package d’index GraphQL pour les fragments de contenu d’Experience Manager{#install-aem-graphql-index-add-on-package}

La clientèle qui utilise GraphQL doit installer le [fragment de contenu d’Experience Manager avec le package d’index GraphQL 1.1.1](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip).

Vous pouvez ainsi ajouter la définition d’index requise selon les fonctionnalités que vous utilisez réellement.

L’échec de l’installation de ce package peut entraîner des requêtes GraphQL lentes ou en échec.

>[!NOTE]
>
>N’installez ce package qu’une seule fois par instance ; il n’est pas nécessaire de le réinstaller avec chaque Pack de services.

### UberJar{#uber-jar}

UberJar pour [!DNL Experience Manager] 6.5.25.0 est disponible dans le [référentiel central Maven](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.25/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Pour utiliser UberJar dans un projet Maven, consultez la section [Utilisation d’UberJar](/help/sites-developing/ht-projects-maven.md) et incluez la dépendance suivante dans le POM de votre projet : <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
  <dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>uber-jar</artifactId>
  <version>6.5.25</version>
  <scope>provided</scope>          
  </dependency>
```

>[!NOTE]
>
>UberJar et les autres artefacts associés sont disponibles sur le référentiel central Maven au lieu du référentiel Maven public Adobe (`repo.adobe.com`). Le fichier UberJar principal est renommé `uber-jar-<version>.jar`. Il n’existe donc pas de `classifier` avec `apis` comme valeur pour la balise `dependency`.



## Fonctionnalités obsolètes et supprimées{#removed-deprecated-features}

Consultez [Fonctionnalités obsolètes et supprimées](/help/release-notes/deprecated-removed-features.md) pour obtenir une liste détaillée de toutes les fonctionnalités obsolètes ou supprimées pour AEM 6.5.

### Prise en charge des fragments de contenu dans l’API REST AEM Assets {#cf-support-assets-rest-api}

AEM 6.5 LTS SP2 fournit des API OpenAPI modernes pour la gestion des fragments de contenu et des modèles, de sorte que les anciens points d’entrée de la prise en charge des fragments de contenu dans l’API REST AEM Assets sont désormais obsolètes.

Adobe prévoit de conserver ces anciens points d’entrée disponibles jusqu’à une annonce de fin de vie. Adobe ne prévoit pas d’autres améliorations pour les points d’entrée obsolètes.

### Éditeur de SPA {#spa-editor}

[L’éditeur de SPA](/help/sites-developing/spa-overview.md) a été abandonné pour les nouveaux projets commençant par la version 6.5.25 d’AEM 6.5. L’éditeur de SPA reste pris en charge pour les projets existants, mais ne doit pas être utilisé pour de nouveaux projets.

Les éditeurs privilégiés pour la gestion du contenu découplé dans AEM sont désormais les suivants :

* [Éditeur universel](/help/sites-developing/universal-editor/introduction.md) pour la modification visuelle.
* [Éditeur de fragments de contenu](/help/sites-developing/universal-editor/introduction.md) pour la modification basée sur les formulaires.

## Problèmes connus{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST. -->

* **En rapport avec Oak**
À partir du pack de services 13 et versions ultérieures, le journal d’erreurs suivant a commencé à s’afficher, ce qui affecte le cache de persistance :

  ```shell
  org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.0.202/5]
  at org.h2.mvstore.DataUtils.newMVStoreException(DataUtils.java:1004)
      at org.h2.mvstore.MVStore.getUnsupportedWriteFormatException(MVStore.java:1059)
      at org.h2.mvstore.MVStore.readStoreHeader(MVStore.java:878)
      at org.h2.mvstore.MVStore.<init>(MVStore.java:455)
      at org.h2.mvstore.MVStore$Builder.open(MVStore.java:4052)
      at org.h2.mvstore.db.Store.<init>(Store.java:129)
  ```

  Ou

  ```shell
  org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.1.214/5].
  ```

  Pour résoudre cette exception, procédez comme suit :

   1. Supprimez les deux dossiers suivants de `crx-quickstart/repository/`

      * `cache`
      * `diff-cache`

   1. Installez le pack de services ou redémarrez Experience Manager as a Cloud Service.
Les nouveaux dossiers de `cache` et `diff-cache` sont automatiquement créés et vous ne rencontrez plus d’exception liée aux `mvstore` dans le `error.log`.

* Mettez à jour vos requêtes GraphQL qui peuvent avoir utilisé un nom d’API personnalisé pour votre modèle de contenu afin d’utiliser plutôt le nom par défaut du modèle de contenu.

* Une requête GraphQL peut utiliser l’index `damAssetLucene` plutôt que l’index `fragments`. Il peut en résulter l’échec des requêtes GraphQL ou l’exécution de celles-ci peut prendre beaucoup de temps.

  Pour résoudre le problème, `damAssetLucene` doit être configuré pour inclure les deux propriétés suivantes sous `/indexRules/dam:Asset/properties` :

   * `contentFragment`
      * `jcr:primaryType="nt:unstructured"`
      * `name="jcr:content/contentFragment"`
      * `propertyIndex="{Boolean}true"`
      * `type="Boolean"`
   * `model`
      * `jcr:primaryType="nt:unstructured"`
      * `name="jcr:content/data/cq:model"`
      * `ordered="{Boolean}true"`
      * `propertyIndex="{Boolean}true"`
      * `type="String"`

  Une fois la définition d’index modifiée, une réindexation est nécessaire (`reindex` = `true`).

  Après ces étapes, les requêtes GraphQL doivent être plus rapides.

* Lorsque vous tentez de déplacer, de supprimer ou de publier des fragments de contenu, des sites ou des pages, un problème se produit lorsque les références aux fragments de contenu sont récupérées. La requête en arrière-plan échoue ; la fonctionnalité ne fonctionne pas.
Pour garantir le bon fonctionnement de cette opération, vous devez ajouter les propriétés suivantes au nœud de définition d’index `/oak:index/damAssetLucene` (aucune réindexation n’est requise) :

  ```xml
  "tags": [
      "visualSimilaritySearch"
    ]
  "refresh": true
  ```

* Si vous mettez à niveau votre instance [!DNL Experience Manager] de la version 6.5.0 - 6.5.4 au pack de services le plus récent sur Java™ 11, des exceptions `RRD4JReporter` s’affichent dans le fichier `error.log`. Pour arrêter les exceptions, redémarrez votre instance d’[!DNL Experience Manager]. <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* Les utilisateurs peuvent renommer un dossier dans une hiérarchie dans [!DNL Assets] et publier un dossier imbriqué dans [!DNL Brand Portal]. Toutefois, le titre du dossier n’est pas mis à jour dans [!DNL Brand Portal] jusqu’à ce que le dossier racine soit republié.

* Les erreurs et messages d’avertissement suivants peuvent s’afficher lors de l’installation d’[!DNL Experience Manager] 6.5.x.x :
   * « Lorsque l’intégration d’Adobe Target est configurée dans [!DNL Experience Manager] à l’aide de l’API Target Standard (authentification IMS), l’exportation de fragments d’expérience vers Target entraîne la création de types d’offres incorrects. » Au lieu du type « Fragment d’expérience » / source « Adobe Experience Manager », Target crée plusieurs offres avec le type « HTML » / source « Adobe Target Classic ».
   * `com.adobe.granite.maintenance.impl.TaskScheduler` : aucune fenêtre de maintenance n’a été trouvée sur `granite/operations/maintenance`.
   * La validation côté serveur du formulaire adaptatif échoue lorsque des fonctions d’agrégat telles que SUM, MAX et MIN sont utilisées (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` : aucune fenêtre de maintenance n’a été trouvée sur `granite/operations/maintenance`.
   * La zone réactive d’une image interactive de Dynamic Media n’est pas visible lors de la prévisualisation du fichier via la visionneuse de bannières avec achat.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : temporisation en attente de modification d’enregistrement pour terminer la désinscription.

* À partir de la version 6.5.15 d’AEM, le moteur JavaScript Rhino fourni par le lot `org.apache.servicemix.bundles.rhino` a un nouveau comportement d’hébergement. Les scripts qui utilisent le mode strict (`use strict;`) doivent déclarer leurs variables correctes. Dans le cas contraire, elles ne sont pas exécutées et finissent par générer une erreur d’exécution.

* L’installation du balisage du contenu d’usine par le biais d’un package de mise à jour officiel réinitialise la propriété languages du nœud `/content/cq:tags` par défaut. Cette action est vraie pour les packs de services, les packs de services de sécurité, les packs de correctifs, les packs de correctifs cumulatifs, les correctifs, etc. Il est donc nécessaire de l’ajouter à partir des propriétés avant l’installation.

### Problèmes connus pour AEM Sites {#known-issues-aem-sites-6525}

Fragments de contenu : la prévisualisation échoue en raison de la protection DoS pour une arborescence de fragments volumineuse. Voir l’[article de la base de connaissances sur les options de configuration par défaut de l’exécuteur de requêtes GraphQL](https://experienceleague.adobe.com/fr/docs/experience-cloud-kcs/kbarticles/ka-23945) (SITES-17934).

### Problèmes connus d’AEM Forms {#known-issues-aem-forms-6525}

* **FORMS-14521** Si un utilisateur tente de prévisualiser un brouillon de lettre avec des données XML enregistrées, il est bloqué à l’état `Loading` pour certaines lettres spécifiques.
* **FORMS-16603** Dans l&#39;aperçu avant impression de l&#39;interface utilisateur de l&#39;agent de communication interactive, certaines valeurs calculées ne s&#39;affichent pas correctement.
* **FORMS-15681** Lorsque la lettre est affichée en aperçu avant impression, le contenu est modifié ; certains espaces disparaissent et certaines lettres sont remplacées par des `x`.
* **FORMS-15428** Après la mise à jour vers le Service Pack 20 d’AEM Forms (6.5.20.0) avec le module complémentaire Forms, les configurations reposant sur l’ancien service Adobe Analytics Cloud à l’aide de l’authentification basée sur les informations d’identification ne fonctionnent plus. Ce problème empêchait les règles d’analyse de s’exécuter correctement.
* **FORMS-16557** Dans l’aperçu avant impression de l’interface utilisateur de l’agent de communication interactive, le symbole de devise (tel que le signe dollar $) s’affiche de manière incohérente pour toutes les valeurs de champ. Il s’affiche pour les valeurs allant jusqu’à 999, mais il est absent pour les valeurs supérieures ou égales à 1 000.
* **FORMS-16575** Les modifications apportées au fichier XDP des fragments de disposition imbriqués dans une communication interactive ne sont pas répercutées dans l’éditeur IC.
* **FORMS-21378** Lorsque la validation côté serveur (SSV) est activée, les envois de formulaires peuvent échouer. Si vous rencontrez ce problème, contactez l’assistance Adobe pour obtenir de l’aide.
* **FORMS-23722** Lorsqu’un formulaire contenant un champ **Pièce jointe** qui utilise `bindref` est envoyé à un workflow AEM avec une étape **Affecter une tâche**, les pièces jointes ne s’affichent pas. Par conséquent, ils n’apparaissent pas lorsque la tâche est ouverte à partir de la boîte de réception. Les fichiers sont correctement enregistrés dans le référentiel, mais l’interface utilisateur de l’étape Affecter une tâche ne parvient pas à afficher les pièces jointes.
* **FORMS-23802** Les fonctions personnalisées ne parviennent pas à se charger dans l’aperçu ou la publication lorsqu’un formulaire adaptatif est incorporé dans une page Sites. Ce problème se produit lorsque la version de la bibliothèque **aem-forms-core-component** est antérieure à la version 1.1.76. Il se peut qu’une erreur telle que `InvalidFormContainerException: No form container found` s’affiche dans les journaux. Pour résoudre ce problème, [télécharger et installer le correctif](/help/release-notes/aem-forms-hotfix.md) pour AEM Forms SP24 (AddOn 6.0.1454).

#### Problèmes connus liés aux correctifs disponibles {#aem-forms-issues-with-hotfixes}

<!--
>[!NOTE]
>
>Avoid upgrading to Service Pack 6.5.25.0 for issues without an available hotfix. It may lead to unexpected errors. Upgrade to Service Pack 6.5.25.0 only after the required hotfixes are released.
-->

Un correctif logiciel peut être téléchargé et installé pour les problèmes suivants. Pour résoudre ces problèmes, vous pouvez [télécharger et installer le correctif](/help/release-notes/aem-forms-hotfix.md) :

* **FORMS-23881** Sur les déploiements AEM Forms JEE configurés à l’aide du programme d’installation complet 6.5.23.0, le service Output ne parvient pas à traiter les requêtes lorsqu’un fichier XCI personnalisé est fourni dans l’appel. Pour résoudre ce problème, installez le dernier pack de services AEM 6.5.25.0 Forms à partir du portail [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
* **FORMS-23789** (AEM Forms on JEE uniquement) : les utilisateurs ont rencontré des problèmes avec Log4j dans le SP24 d’AEM Forms on JEE, ce qui a entraîné des perturbations de la journalisation et de la surveillance pour les clients Grands comptes. Pour résoudre ce problème, [téléchargez et installez le correctif](/help/release-notes/aem-forms-hotfix.md) pour le pack de services d’AEM Forms sur JEE 6.5.25.0.
* **Les fonctions personnalisées de FORMS-23802** ne se chargent pas dans l’aperçu ou la publication lorsque le formulaire se trouve dans une page Sites avec une ancienne version du composant principal aem-forms (&lt;1.1.76). Pour résoudre ce problème, installez le [correctif complémentaire AEM Forms 6.0.1454](/help/release-notes/aem-forms-hotfix.md) pour SP24.
* **FORMS-23789** (AEM Forms on JEE uniquement) : les utilisateurs ont rencontré des problèmes avec Log4j dans le SP24 d’AEM Forms on JEE, ce qui a entraîné des perturbations de la journalisation et de la surveillance pour les clients Grands comptes. Pour résoudre ce problème, [téléchargez et installez le correctif](/help/release-notes/aem-forms-hotfix.md) pour le pack de services d’AEM Forms sur JEE 6.5.25.0.
* **Les fonctions personnalisées de FORMS-23802** ne se chargent pas dans l’aperçu ou la publication lorsque le formulaire se trouve dans une page Sites avec une ancienne version du composant principal aem-forms (&lt;1.1.76). Pour résoudre ce problème, installez le [correctif complémentaire AEM Forms 6.0.1454](/help/release-notes/aem-forms-hotfix.md) pour SP24.
* AEM Forms comprend désormais une mise à niveau de Struts, de la version 2.5.33 vers la version 6.x, pour le composant de formulaire. Cette mise à niveau fournit des modifications Struts précédemment manquantes qui n&#39;étaient pas incluses dans le SP24. La prise en charge a été ajoutée via un [correctif](/help/release-notes/aem-forms-hotfix.md) que vous pouvez télécharger et installer. La dernière version de Struts est alors prise en charge.
* **FORMS-14926** Après l’installation du pack de services 21 (6.5.21.0) d’AEM Forms JEE, si vous constatez des entrées en double de fichiers JAR Geode `(geode-*-1.15.1.jar and geode-*-1.15.1.2.jar)` dans le dossier `<AEM_Forms_Installation>/lib/caching/lib`, procédez comme suit pour résoudre le problème :

   1. Arrêtez les localisateurs s’ils sont en cours d’exécution.
   2. Arrêtez le serveur AEM.
   3. Accédez à `<AEM_Forms_Installation>/lib/caching/lib`.
   4. Supprimez tous les fichiers de correctifs Geode, à l’exception de `geode-*-1.15.1.2.jar`. Confirmez que seuls les fichiers JAR Geode avec `version 1.15.1.2` sont présents.
   5. Ouvrez l’invite de commande en mode administration.
   6. Installez le correctif Geode à l’aide du fichier `geode-*-1.15.1.2.jar`.

* **FORMS-15256** Lorsque les utilisateurs ont effectué la mise à niveau d&#39;AEM 6.5 Forms Service Pack 18 ou 19 vers Service Pack 20 ou 21, ils ont rencontré une erreur de compilation JSP. Cette erreur empêchait d’ouvrir ou de créer des formulaires adaptatifs. Cela provoquait également des problèmes avec d’autres interfaces AEM. Ces interfaces comprenaient l’éditeur de page, l’interface d’utilisation d’AEM Forms, l’éditeur de workflow et l’interface d’utilisation Présentation du système.

  Si vous rencontrez ce problème, procédez comme suit pour le résoudre :
   1. Accédez au répertoire `/libs/fd/aemforms/install/` dans CRXDE.
   2. Supprimez le lot dont le nom est `com.adobe.granite.ui.commons-5.10.26.jar`.
   3. Redémarrez votre serveur AEM.

* **FORMS-23703** Lorsque la règle `contains` est configurée sans valeur par défaut, la validation côté serveur d’un formulaire adaptatif échoue. Vous pouvez installer la dernière version du pack de services [AEM Forms 6.5.25.0](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases#aem-65-forms-releases) pour résoudre le problème.
* **GRANITE-63681** La configuration système par défaut bloque les mots-clés et les modèles RegEx requis, ce qui empêche les connecteurs de modèle de données de formulaire de s’authentifier. Pour résoudre ce problème, téléchargez et installez le correctif à partir du [lien](/help/release-notes/aem-forms-hotfix.md).
* **La conversion FORMS-23979** d’HTML en PDF (PDFG) peut connaître des délais d’expiration intermittents. Une version plus récente du module complémentaire Forms pour SP24 a ensuite été publiée, qui comprend le correctif. Si vous rencontrez ce problème, mettez à jour votre environnement vers la [dernière version du module complémentaire Forms pour 6.5.25.0](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases#aem-65-forms-releases).
* **FORMS-23717** Après la mise à niveau vers **AEM Forms6.5.25.0**, `server.log` et `error.log` peuvent être inondés de messages WARN répétés tels que *Échec de la création de la fabrique d&#39;analyseur sécurisé* ou *Attribut de sécurité... n&#39;est pas pris en charge*. Les journaux peuvent augmenter d’environ **5 à 10 lignes par seconde** (des centaines de Mo par heure), ce qui peut remplir le disque et bloquer le déploiement en production.

Pour réduire le volume de journalisation, définissez le niveau de journalisation des `com.adobe.util.XMLSecurityUtil` à `ERROR` dans la configuration du serveur d’applications ou au moyen de l’argument JVM `-Dlogging.level.com.adobe.util.XMLSecurityUtil=ERROR`. Cette fonctionnalité masque uniquement les messages et ne corrige pas la cause sous-jacente.

* **FORMS-23875** Dans la recherche de modèle de données de formulaire, l’interface utilisateur affiche une balise HTML même lorsqu’une entité pertinente est absente. Pour résoudre ce problème, téléchargez et installez le correctif à partir de [le lien](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/bb-expressionmanager-pkg-10.0.48.zip).

## Lots OSGi et modules de contenu inclus{#osgi-bundles-and-content-packages-included}

Les fichiers zip suivants contiennent les documents texte qui répertorient les lots OSGi et les packages de contenu inclus dans cette version du pack de services [!DNL Experience Manager] 6.5 :

* [Liste des lots OSGi inclus dans Experience Manager 6.5.25.0](/help/release-notes/assets/65250-bundles.zip)
<!-- UPDATE FOR EACH NEW RELEASE -->
* [Liste des packages de contenu inclus dans Experience Manager 6.5.25.0](/help/release-notes/assets/65250-packages.zip)
<!-- UPDATE FOR EACH NEW RELEASE -->

## Sites web à accès limité{#restricted-sites}

Ces sites web sont disponibles uniquement pour les clientes et clients. Si vous êtes client et avez besoin d’un accès, contactez votre responsable de compte Adobe.

* [Téléchargement du produit à l’adresse licensing.adobe.com](https://licensing.adobe.com/)
* [Contacter l’assistance clientèle Adobe](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-customer-support-experience#).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] page produit](https://business.adobe.com/fr/products/experience-manager/adobe-experience-manager.html)
>* Documentation [[!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/fr/docs/experience-manager-65)
>* [S’abonner aux mises à jour de produits prioritaires d’Adobe](https://www.adobe.com/subscription/priority-product-update.html)



