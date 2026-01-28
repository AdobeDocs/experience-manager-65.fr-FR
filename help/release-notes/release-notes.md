---
title: 'Notes de mise à jour de la version 6.5 d’ [!DNL Adobe Experience Manager] '
description: Consultez les informations sur la mise à jour, y compris les nouveautés, la procédure d’installation et une liste complète des modifications pour [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
exl-id: 811fccbc-6f63-4309-93c8-13b7ace07925
source-git-commit: 4305b4c7089fe4ac2b1bfe2dc6e4919181b3d892
workflow-type: tm+mt
source-wordcount: '9486'
ht-degree: 24%

---

# Notes de mise à jour du dernier pack de services [!DNL Adobe Experience Manager] 6.5 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in this release information, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!-- DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, May 29, 2025. In addition, a list of Forms fixes and enhancements is added to this section. -->

## Informations sur la version {#release-information}

| Produit | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Version | 6.5.24.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Type | Mise à jour du pack de services |
| Date | 26 novembre 2025 <!-- UPDATE FOR EACH NEW RELEASE --> |
| URL de téléchargement | [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.24.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

<!-- OLD DOWNLOAD URL
(https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.23.0.zip) -->

## Éléments compris dans [!DNL Experience Manager] 6.5.24.0 {#what-is-included-in-aem-6524}

[!DNL Experience Manager] 6.5.24.0 comprend de nouvelles fonctionnalités, des améliorations importantes demandées par la clientèle, ainsi que correctifs. Cette version comprend également des améliorations en termes de performances, de stabilité et de sécurité, publiées depuis la mise à disposition initiale de la version 6.5 en avril 2019. [Installez ce pack de services](#install) sur [!DNL Experience Manager] 6.5.

<!-- UPDATE FOR EACH NEW RELEASE -->


## Principales fonctionnalités et améliorations

### Formulaires

* **Prise en charge de la transmission de XCI personnalisés :** Ajout de la prise en charge de la transmission de XCI personnalisés dans les paramètres de l’application cmdline xmlformcmd. Cela permet aux utilisateurs de spécifier des fichiers XCI personnalisés à des fins de test, ce qui améliore la flexibilité et le contrôle du processus de test. (LC-3923248)


## Problèmes corrigés dans le pack de services 24 {#fixed-issues}

<!-- 6.5.24.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE? -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

### [!DNL Assets] {#assets-sp24}

* Après la mise à jour vers la version 6.5.23.0, le tri des dossiers par date de modification dans le mode Carte entraînait des difficultés à localiser les ressources récemment modifiées pour les déploiements On-Premise. (ASSETS-56946)
* Des entrées de journal d&#39;avertissement répétées sont générées lors des exécutions du planificateur. (ASSETS-52554)
* Le tri des titres ne fonctionne pas dans la vue Liste. (ASSETS-50716)
* La fenêtre Propriétés de la collection ne se ferme pas, même après avoir cliqué sur le bouton Annuler. (ASSETS-48504)

* Une erreur *URL non valide* se produit lors de la tentative d’annotation de ressources dans AEM 6.5.22. (NPR-42684)
* Le formulaire de l’éditeur de métadonnées d’Assets ne se réinitialise pas après avoir effectué des actions associées ou non. (ASSETS-52207)
* Lorsque des ressources du DAM distant sont resynchronisées avec le site local Sites, le statut publié des ressources est incorrectement mis à jour vers `Not published`. (ASSETS-48958)
* Problèmes rencontrés lors de la mise à niveau du SP23 vers la version 6.5 LTS. (ASSETS-50541)

### [!DNL Sites]{#sites-6524}

#### Accessibilité {#sites-accessibility-6524}

* La boîte de dialogue **Changer le format d’affichage** prend désormais en charge le fonctionnement complet du clavier. Le focus n’ignore plus le bouton **Afficher les paramètres** et les touches standard (`Tab`, `Enter` et `Space`) fonctionnent de manière cohérente. (SITES-24306)
* Utilisez le clavier pour supprimer les balises de statut publiées sans passer par la souris. Le focus se trouve sur chaque balise et l’activation fonctionne avec `Enter`/`Space` et Retour arrière/Suppression. Le contrôle de balise se comporte désormais comme un bouton, ce qui améliore les commentaires du lecteur d’écran et répond aux exigences du clavier WCAG 2.1.1. (SITES-24491)
* Le rail des filtres se repositionne de manière réactive dans les fenêtres étroites. Les contrôles de sélection et les résultats restent dans la fenêtre d’affichage avec un zoom de 400 %, ce qui élimine le défilement horizontal et la coupure du contenu. (SITES-24708)
* AEM restaure l’accès complet au clavier pour les boutons Réinitialisation de ContextHub, Persona et Appareil. Les touches de tabulation et les touches fléchées atteignent chaque commande, affichent un indicateur de focus visible et activent les actions avec `Enter` ou `Space`. Les lecteurs d’écran annoncent des libellés clairs. (SITES-24939)
* La saisie de date et le sélecteur restent entièrement visibles à 320 px. La boîte de dialogue modale Timewarp utilise un dimensionnement réactif afin que le contrôle ne soit plus clipé ou disparaisse dans la plus petite fenêtre d’affichage. (SITES-24962)
* Le rail Références prend désormais en charge un zoom de 400 % du navigateur sans perdre l’accès à son contenu. Le rail utilise un dimensionnement réactif au lieu d’une largeur fixe, de sorte que les éléments restent visibles et sélectionnables à 1 280 × 1 024. (SITES-24972)
* Le rail des filtres fonctionne désormais avec un zoom de 400 %. Le rail se redimensionne avec des unités relatives et ne bloque ni ne masque plus les contrôles de filtre. Les utilisateurs peuvent afficher et sélectionner chaque option de filtre sans faire défiler horizontalement ou couper les cibles d’accès. (SITES-24981)
* Utiliser un clavier uniquement pour afficher les menus de formatage dans la boîte de dialogue modale Teaser. Appuyez sur `Enter` ou `Space` sur **Liste** ou **Format de paragraphe** pour ouvrir le pop-up, accéder aux options de navigation à l’aide des touches fléchées et appliquer `Enter` la sélection. `Escape` ferme le menu et restaure le focus sur le contrôle de déclenchement, ce qui produit un workflow cohérent dans la barre d’outils. (SITES-25235)
* La fenêtre contextuelle du sélecteur de couleur d’échantillon reste désormais dans la fenêtre d’affichage à 320 px. La fenêtre contextuelle affiche toutes les lignes de couleur et prend en charge le défilement, de sorte que les auteurs peuvent sélectionner n’importe quel échantillon sur de petits écrans. (SITES-25274)
* Les menus déroulants de la barre d’outils démographique fonctionnent désormais entièrement avec le clavier. L’ouverture d’un menu déplace le focus vers la première option, les touches fléchées permettent de naviguer dans la liste et la touche Échap/Tabulation se ferme ou progresse sans vider le focus sur la barre d’outils. Les éléments interactifs utilisent la sémantique appropriée afin que NVDA et d’autres lecteurs annoncent correctement les options. (SITES-25310)
* L’option Ajouter un composant dans l’arborescence de contenu fonctionne comme prévu dans le pack de services 24 d’AEM 6.5. L’erreur initiale provient d’autorisations d’auteur manquantes dans une configuration locale, et non d’AEM. Les auteurs disposant de droits de modification peuvent activer le bouton et ajouter des composants à l’aide du clavier ou de la souris. (SITES-25312)
* L’accès au clavier et au lecteur d’écran dans la barre d’outils Démographique fonctionne désormais de manière fiable. Les auteurs qui utilisent NVDA peuvent parcourir **Commerce**, **Persona** et 88 avec des flèches, observer des commentaires de focus clairs et comprendre quel onglet est actif. (SITES-25326)

* Le lien **Passer au contenu** déplace désormais le focus au clavier vers l’en-tête de contenu principal. Le focus reste visible sur une cible identifiée de manière unique, de sorte que les lecteurs d’écran annoncent la section appropriée. La modification respecte les normes WCAG 2.4.1 et 2.4.3. (SITES-24061)
* La navigation au clavier dans l’arborescence de la page d’accueil de Sites suit une séquence logique après l’utilisation de **Tout sélectionner**. Le focus passe de **Tout sélectionner** au contrôle suivant (rail ouvrir à gauche) au lieu de revenir au début de la page. (SITES-24307)
* Les titres de section et les commandes de modification dans l’éditeur Sites répondent à la sélection et à l’activation du clavier. Utilisez le clavier pour afficher le même titre et les mêmes actions que ceux affichés précédemment uniquement lorsque vous pointez dessus. (SITES-24479)
* Les boutons de l’éditeur Sites affichent des noms descriptifs au lieu de libellés génériques ou manquants. Les technologies d’assistance annoncent la bonne action, ce qui améliore la clarté et réduit les clics erronés. (SITES-24480)
* Les lecteurs d’écran reçoivent un message « Chargement » vocal pendant l’actualisation de la vue Sites. La mise à jour ajoute une région active de statut dédiée et y écrit le message par programmation, ce qui confirme la progression sans déplacer le focus. (SITES-24481)
* Le rail latéral d’Assets comprend désormais un contrôle **Fermer** clair et renvoie la sélection au bouton de basculement. Les utilisateurs d’un clavier ou d’un lecteur d’écran ignorent immédiatement le panneau au lieu de parcourir toutes les commandes par tabulation. La modification réduit les frappes et correspond au comportement attendu du panneau. (SITES-24489)
* La liste d’onglets ARIA dans l’éditeur de page de Sites comprend un nom descriptif. Les lecteurs d’écran identifient désormais le contrôle comme une liste d’onglets et lisent le libellé correct, ce qui permet aux utilisateurs de trouver le bon ensemble d’onglets et de se déplacer de manière fiable entre eux. (SITES-24492)
* La recherche dans le rail latéral de l’éditeur annonce désormais les résultats aux lecteurs d’écran. Lorsque les utilisateurs saisissent du texte, un message de statut actif indique le nombre de correspondances et de mises à jour sans déplacer le focus. Utilisez le clavier pour découvrir immédiatement les résultats. (SITES-24506)
* La sélection de lignes dans la vue Liste s’améliore pour les utilisateurs et utilisatrices de technologies d’assistance. La case à cocher expose un nom significatif dérivé du titre de la ligne. De ce fait, les annonces restent brèves et décrivent correctement l’action. (SITES-24514)
* Correction des noms d’accessibilité de la vue Liste . Le tableau supprime les `aria-label` des éléments non interactifs et attribue le libellé au lien ou au bouton exploitable. Les utilisateurs de lecteurs d’écran entendent désormais des libellés précis et non dupliqués dans toute la colonne. (SITES-24515)
* L’en-tête adhésif ne masquait plus la boîte de dialogue modale du teaser lors d’une utilisation avec un zoom élevé. Le contenu reste lisible et utilisable avec un zoom de 200 % et de 400 %, avec un flux vertical et aucune section tronquée. (SITES-24523)
* La saisie dans le champ de recherche ne déclenche plus une annonce prématurée du premier résultat ou une activation accidentelle. L’expérience annonce désormais un message de statut concis avec le nombre de résultats, tandis que le focus reste dans le champ jusqu’à ce que l’utilisateur accède à la liste. (SITES-24658)
* Le champ Texte secondaire de la boîte de dialogue hyperlien de l’éditeur de texte expose désormais un libellé de programmation. Les lecteurs d’écran annoncent « Texte secondaire » pour le champ et le focus se trouve sur le contrôle correctement nommé. Ce correctif améliore la navigation pour les utilisateurs et utilisatrices de clavier et de reconnaissance vocale. (SITES-24675)
* Ajout d’un message de statut en direct au rail Références pour que les technologies d’assistance annoncent immédiatement les modifications. La sélection de plusieurs éléments déclenche un message clair sur la disponibilité de référence, ce qui empêche les changements d’état silencieux et réduit les actions répétées. (SITES-24678)
* La boîte de dialogue Image annonce désormais son état de chargement via une région active ARIA. Les lecteurs d’écran entendent un message « Chargement en cours, veuillez patienter » pendant que le composant déroulant s’affiche. Et une mise à jour prête lorsque le contenu se termine, afin que les utilisateurs sachent quand ils peuvent interagir. (SITES-24697)
* La boîte de dialogue Sélection de lien expose désormais une région active qui annonce les résultats de la recherche. Les lecteurs d’écran entendent le statut « résultats mis à jour » après chaque recherche sans déplacer la cible, de sorte que les utilisateurs et utilisatrices reçoivent une confirmation claire que la recherche a été terminée. (SITES-24700)
* La boîte de dialogue Sélection de lien se repositionne désormais à 320 px. Tous les champs et actions restent visibles et utilisables, et la barre de défilement horizontale ne s’affiche plus. (SITES-24709)
* La boîte de dialogue Sélection de lien utilise désormais le même libellé pour le texte à l’écran et le nom accessible sur chaque élément de l’arborescence. Les lecteurs d’écran annoncent chaque élément en se déplaçant à l’aide des touches fléchées, y compris le dernier niveau, ce qui élimine les nœuds silencieux et les noms incompatibles. (SITES-24710)
* Modifier les filtres indique désormais que son statut est développé ou réduit. Le bouton bascule `aria-expanded` en synchronisation avec le panneau de filtrage et expose un seul nom clair (« Modifier les filtres »), supprimant le « filtre » déroutant. annonce. Les utilisateurs de lecteurs d’écran peuvent prédire le résultat de l’activation du contrôle. (SITES-24713)
* Les en-têtes modaux ne couvrent plus le contenu à une largeur de 320 px. L’en-tête sort de son état contigu et le corps de la boîte de dialogue défile, de sorte que tous les champs et boutons d’action restent visibles et utilisables. Les utilisateurs du clavier peuvent accéder à chaque commande sans perte de focus. (SITES-24718)
* Les liens de navigation dans les applications exposent désormais une sémantique de lien appropriée. Les lecteurs d’écran annoncent chaque élément sous la forme d’un lien plutôt que d’un élément de liste, ce qui améliore la navigation au clavier et le contrôle vocal. Le conteneur de liste conserve la sémantique de la liste, tandis que les liens restent les cibles pouvant être ciblées. (SITES-24719)
* Le statut des résultats s’affiche désormais aux lecteurs d’écran lorsque les filtres changent. NVDA lit le nombre « X sur Y résultats » et le message « aucun résultat ». Le statut de pagination utilise une zone géographique active qui se met à jour sur place, de sorte que les utilisateurs et utilisatrices reçoivent une confirmation sans déplacer le focus. (SITES-24720)
* Le bouton de rotation de la boîte de dialogue Carrousel annonce désormais un nom unique et concis aux lecteurs d’écran. Le contrôle ne répète plus le libellé du groupe et le libellé d’entrée, ce qui réduit la verbosité et la confusion pour les utilisateurs NVDA. (SITES-24725)
* La liste de recherche du menu Aide expose la sémantique appropriée. Le conteneur présente une liste et chaque résultat reste un lien sans conflit de rôle. NVDA et JAWS annoncent les liens avec précision et la navigation reste cohérente. (SITES-24729)
* Adobe a corrigé le pop-up d’échantillon de couleur dans les Préférences utilisateur afin que le NVDA annonce l’échantillon ciblé, et non l’échantillon sélectionné précédemment. Les utilisateurs du clavier entendent des noms de couleurs précis lorsqu’ils se déplacent dans la liste et peuvent confirmer que la sélection est correcte. (SITES-24739)
* NVDA lit désormais la description complète dans le répertoire Tree. Le panneau Détails expose le texte multiligne comme une seule valeur et le lie au libellé du champ. Utilisez le clavier pour entendre le texte complet tout en parcourant les champs en lecture seule avec la touche tabulation. (SITES-24780)
* L’arborescence annonce maintenant la date de modification. Le NVDA lit la date à laquelle le focus se déplace dans la colonne Modifié. La grille lie chaque date au nom de l’élément afin que les utilisateurs entendent le fichier et sa dernière mise à jour. (SITES-24782)
* Le mode Aperçu respecte désormais les préférences d’espacement des textes des utilisateurs. La zone de travail reflète les modifications de la lettre, du mot et de la hauteur de ligne sur tout le contenu prévisualisé. Le texte ne reste plus fixe ou clips lorsque l’espacement augmente. Utiliser le clavier et les utilisateurs malvoyants pour lire le contenu sans sauts de disposition (SITES-24936)
* AEM corrige l’ordre de tabulation sur les pages de l’éditeur Assets. La touche de tabulation permet de passer des commandes d’en-tête aux boutons de concentrateur de contacts et, finalement, aux outils de la zone de travail, dans un ordre clair. Les lecteurs d’écran suivent le même ordre, ce qui supprime la confusion et accélère la navigation au clavier. (SITES-24937)
* AEM ajoute un nom de programme à la barre de menus Actions de la carte. Les lecteurs d’écran annoncent correctement le contrôle et les utilisateurs peuvent le cibler par nom. La navigation au clavier et la sélection restent inchangées. (SITES-24938)
* Les menus du mode Carte respectent l’espacement du texte. L’élément Plus d’actions grandit et ne tronque plus les libellés, y compris la publication rapide. Les utilisateurs qui lèvent des lettres, des mots ou des interlignes conservent les libellés complets et accèdent au clavier. (SITES-24941)
* Suppression du rôle « présentation » qui masquait le tableau de la page d’accueil de Sites dans l’arborescence d’accessibilité. Le tableau se lit à nouveau correctement. NVDA et JAWS détectent le tableau, reconnaissent les en-têtes et annoncent les relations d’en-tête lors de la navigation entre les lignes et les colonnes. (SITES-24942)
* Le tri des commentaires dans la vue Liste est explicite et cohérent. Après un tri, l’en-tête expose la commande par `aria-sort`. Il annonce la modification, tandis que les en-têtes non triés ne revendiquent plus un état, ce qui permet aux utilisateurs de lecteurs d’écran de suivre la colonne qui contrôle le tri. (SITES-24943)
* L’en-tête Modifier la disposition n’expose plus de bouton **Modifier** qui ne fonctionne pas. Le contrôle agit désormais comme un libellé d’état statique et reste en dehors de l’ordre de tabulation, de sorte que les utilisateurs d’un clavier ne perdent pas une frappe. Utilisez **Sélectionner un autre mode** pour changer de mode, avec des commentaires clairs sur le lecteur d’écran. (SITES-24950)
* La barre d’outils de l’émulateur affiche les noms complets des appareils par défaut. Le libellé n’est plus tronqué au chargement, de sorte que les utilisateurs et utilisatrices peuvent lire et sélectionner des appareils sans deviner. Le texte se met clairement à l’échelle sur les niveaux de zoom et les largeurs étroites. (SITES-24952)
* La barre d’outils de l’émulateur est adaptée aux petites fenêtres d’affichage. À 320 pixels, l’appareil répertorie et contrôle l’affichage sans écrêtage, de sorte que les utilisateurs puissent sélectionner le Galaxy S7 et les modèles plus récents. La mise en page met à l’échelle et recouvre pour éviter le défilement horizontal, même avec un zoom de 400 %. (SITES-24953)
* Les lecteurs d’écran annoncent l’appareil sélectionné et ses mesures dans l’émulateur. NVDA cesse de lire le flux de la règle ; le bouton de l’appareil utilise une description jointe pour le texte de l’info-bulle, ce qui réduit le bruit et guide la navigation. (SITES-24955)
* La barre de filtrage traite désormais chaque balise sélectionnée comme un bouton d’action. La clarté des noms accessibles et la gestion du focus améliorent les annonces et le contrôle du clavier. (SITES-24980)
* Les mises à jour de statut dans la vue Filtre de l’administrateur de sites sont annoncées aux lecteurs d’écran. Lorsque les utilisateurs changent de carte/liste pendant le chargement des éléments, le NVDA diffuse désormais le message « Veuillez patienter » dans une zone géographique active. Ces conseils évitent les clics supplémentaires et la confusion. (SITES-24992)
* Le focus au clavier se déplace désormais dans un ordre logique lorsque les utilisateurs développent le rail de gauche. Le focus se déplace directement du bouton du rail de gauche vers le contenu développé, ce qui élimine la nécessité de revenir en arrière ou d’ignorer des éléments. Cette modification améliore l’accessibilité pour les utilisateurs d’un lecteur d’écran ou d’un clavier. (SITES-24998)
* Les commentaires du lecteur d’écran du bouton **Modifier** correspondent désormais au contrôle. L’activation du bouton annonce l’action Modifier plutôt qu’un message de prévisualisation, ce qui améliore la clarté et réduit les erreurs de saisie pour les utilisateurs et utilisatrices qui ne disposent pas de la souris. (SITES-25208)
* L’action de confirmation dans la boîte de dialogue Teaser s’affiche correctement dans les lecteurs d’écran. Le contrôle indique « Confirmer », et non la description de l’icône, fournissant des conseils clairs aux utilisateurs du clavier et des lecteurs d’écran. (SITES-25223)
* Le bouton Aide propose désormais un nom accessible et clair. Les lecteurs d’écran annoncent « Aide » au lieu d’une description détaillée de l’icône. Les utilisateurs comprennent l’action et peuvent obtenir de l’aide plus rapidement. (SITES-25224)
* La boîte de dialogue modale Timewarp affiche un anneau de sélection clair sur les liens **`Set Date`** et **Quitter Timewarp**. Les utilisateurs qui accèdent à l’onglet voient exactement où se trouve le focus et évitent les actions inattendues. L&#39;anneau maintient au moins 3:1 de contraste par rapport au fond. (SITES-25232)
* Les lecteurs d’écran annoncent désormais avec précision les commandes Annoter et Fermer l’annotation dans la barre d’outils Annotation. Le NVDA ne dit plus « Bouton d’aperçu appuyé », ce qui induisait en erreur les auteurs et suggérait la mauvaise action. L’annonce correspond au bouton enfoncé et laisse le workflow clair. (SITES-25234)
* La navigation au clavier dans la barre d’outils d’annotation se comporte de manière cohérente. Le focus ne quitte plus lors de l’ouverture du mode et passe plutôt à la commande de démarrage pour l’ajout d’annotations. Les utilisateurs parcourent les commandes dans l’ordre sans inverser la tabulation. (SITES-25241)
* L’affichage en petit écran fonctionne comme prévu dans la boîte de dialogue modale Teaser . La boîte de dialogue ne crée plus de barre de défilement horizontale à 320 px et la barre d’outils reste accessible sans panoramique sur les côtés. Cette mise à jour est utile pour les utilisateurs et utilisatrices malvoyants qui zooment sur la page. (SITES-25242)
* L’affichage en petit écran fonctionne comme prévu dans la boîte de dialogue modale Image. La boîte de dialogue ne crée plus de barre de défilement horizontale à 320 px et les outils d’image restent accessibles sans panoramique sur les côtés. Cette mise à jour améliore la navigation pour les utilisateurs et utilisatrices malvoyants qui zooment la page. (SITES-25244)
* La boîte de dialogue modale de recherche respecte les paramètres d’espacement des textes utilisateur. L’augmentation de la hauteur des lignes, de l’espacement des paragraphes, des lettres ou des mots ne coupe plus le texte et ne chevauche plus l’arborescence. Le contenu est redistribué aux valeurs WCAG 1.4.12 et reste entièrement lisible. (SITES-25245)
* La boîte de dialogue modale de recherche s’adapte désormais aux petits écrans sans chevaucher le répertoire d’arborescence à 320 px. Le contenu est redistribué dans la boîte de dialogue, permet uniquement le défilement vertical et affiche les commandes. Ce correctif améliore la lisibilité et la navigation au clavier et s’aligne sur le reflux WCAG. (SITES-25246)
* Le débordement modal du carrousel ne force plus le défilement horizontal aux largeurs de téléphone. Le composant s’adapte à 320 px, conserve l’écoulement vertical et conserve les commandes en vue. Cette modification améliore la lisibilité et l’accès au clavier lors de la création. (SITES-25254)
* Les workflows d’annotation ne perdent plus le focus. La boîte de dialogue modale place le focus initial sur un en-tête significatif, empêche le focus de sortir de la boîte de dialogue et restaure le focus sur le déclencheur après le rejet. La sortie du lecteur d’écran reste concise et pertinente. (SITES-25257)
* La boîte de dialogue **Supprimer l’annotation** gère désormais correctement le focus au clavier. L’ouverture de la boîte de dialogue déplace le focus vers son en-tête pour le contexte du lecteur d’écran, et sa fermeture renvoie le focus au bouton **Supprimer l’annotation** qui l’a lancée. Les utilisateurs n’atterrissent plus sur des commandes non liées ou derrière la fenêtre modale. (SITES-25258)
* Le sélecteur de date Timewarp gère désormais correctement le focus. Appuyer sur `Esc` renvoie le focus au bouton **Sélecteur de date** et choisir une date déplace le focus vers le champ de saisie lié. Les utilisateurs d’un clavier ou d’un lecteur d’écran conservent le contexte et n’atterrissent pas derrière la fenêtre modale. (SITES-25264)
* Les lecteurs d’écran annoncent les actions correctes pour les boutons **Annoter** et **Fermer l’annotation**. Le NVDA ne dit plus « Bouton d’aperçu appuyé » ; il annonce le nom du bouton afin que les utilisateurs et utilisatrices sachent quand le mode d’annotation commence ou se termine. (SITES-25268)
* La boîte de dialogue modale Annotation affiche désormais une action **Envoyer** claire. Les auteurs peuvent ajouter un commentaire et l’envoyer à l’aide du bouton icône représentant un stylet ou ignorer la boîte de dialogue modale avec `Esc`, sans deviner le flux. (SITES-25269)
* L’entrée d’annotation comprend des boutons d’action explicites. La boîte de dialogue expose **Envoyer** pour enregistrer la note et **Annuler** pour la fermer, accessibles à l’aide du clavier et annoncés par la technologie d’assistance. Les auteurs n’ont plus besoin de cliquer en dehors de la boîte de dialogue ou d’appuyer uniquement sur `Esc` pour terminer. (SITES-25281)
* Le mode Annotation conserve désormais le focus au clavier sur la superposition et sa barre d’outils. La page derrière le recouvrement ne reçoit plus le focus lorsque les auteurs appuient sur la touche de tabulation. Les utilisateurs restent donc orientés et peuvent parcourir les annotations sans accéder au contenu sous-jacent. (SITES-25282)
* Le sélecteur d’appareil dans Modifier la disposition fonctionne comme prévu. Lorsque deux options d’appareil ont des largeurs similaires (par exemple, iPhone 8 Plus en regard de Galaxy 7), le bouton sélectionné affiche une info-bulle pour afficher le libellé complet tandis que les deux boutons restent visibles et accessibles. (SITES-25285)
* Avec un zoom de 200 %, l’option Modifier la disposition ne dépasse plus la page. La barre d’outils effectue un rendu complet et affiche un défilement horizontal si nécessaire, ce qui restaure l’accès aux contrôles précédemment masqués pour les utilisateurs malvoyants. (SITES-25288)
* L’ordre de tabulation dans l’aperçu de la mise en page passe désormais de la barre d’outils principale directement à la barre d’outils Démographique. Les utilisateurs d’un clavier ou d’un lecteur d’écran peuvent parcourir les commandes dans un ordre prévisible au lieu de passer à la barre d’outils secondaire. La modification s’aligne sur l’ordre de focus de WCAG 2.4.3. (SITES-25305)
* Le zoom de la page sur 200 % ne masque plus une partie de la barre d’outils Démographique. La section de la barre d’outils gère le débordement et fournit un défilement dans sa propre zone, ce qui permet de visualiser et de manipuler chaque commande avec un fort grossissement. (SITES-25309)
* Les entrées de texte dans la barre d’outils Démographie exposent désormais les noms accessibles appropriés. Chaque champ comprend un identifiant unique avec un libellé programmatique, de sorte que les lecteurs d’écran annoncent l’objectif du champ et que les utilisateurs peuvent naviguer par libellé. L’étiquette visible se trouve près de la commande pour améliorer la lisibilité à faible vision. (SITES-25316)
* Le bouton Modifier annonce désormais l’action correcte aux lecteurs d’écran dans la barre d’outils secondaire. Son activation indique « Modifier » au lieu du « Bouton Aperçu enfoncé » sans rapport, ce qui supprime la confusion lors de la navigation au clavier. (SITES-25320)
* Le curseur de panier de la barre d’outils Démographie expose désormais un nom accessible approprié. Les lecteurs d’écran annoncent un « total du panier » et les outils de saisie vocale peuvent cibler le contrôle par nom, améliorant ainsi la conformité au WCAG 4.1.2 (nom, rôle, valeur). (SITES-25322)
* Le curseur de la barre d’outils Démographie conserve désormais le focus lorsque les auteurs modifient la valeur à l’aide des touches fléchées. Le focus ne passe plus au bouton Panier, de sorte que les utilisateurs du clavier ajustent la valeur en continu et que les lecteurs d’écran annoncent chaque modification. (SITES-25324)
* Recherche Assets maintenant Redistribution propre à 320 px (environ 400 % de zoom). La boîte de dialogue modale permet de conserver les en-têtes, champs et actions lisibles et ne se chevauchant pas, de sorte que les auteurs puissent effectuer des recherches sans défilement horizontal. (SITES-25330)
* Le panneau Assets de l’éditeur suit une séquence de focus logique. Appuyez sur l’onglet de chaque miniature et accédez aux commandes de sortie du panneau. La modification supprime les sauts et améliore la conformité au WCAG 2.4.3. (SITES-25360)
* AEM met à jour les boutons **Listes** et **Paragraphes** dans l’éditeur de texte enrichi de la boîte de dialogue modale du teaser afin d’afficher leur statut développé et réduit. Les boutons permettent désormais de basculer entre les `aria-expanded` et d’annoncer le changement d’état aux lecteurs d’écran. Les auteurs obtiennent des commentaires clairs et évitent de faire des suppositions avant d&#39;ouvrir ou de fermer les menus de format. (SITES-25365)
* AEM annonce l’état de chargement dans la boîte de dialogue modale Teaser . La boîte de dialogue modale expose désormais un message de statut actif pendant le chargement du contenu, de sorte que NVDA et JAWS parlent « Chargement, veuillez patienter ». Les auteurs doivent recevoir des commentaires clairs et éviter d’interagir avec la boîte de dialogue avant qu’elle ne soit prête. (SITES-25366)
* Améliore les messages de statut dans l’onglet Ressource de la boîte de dialogue de sélection Lien. Lorsqu’une erreur se produit, le composant injecte une mise à jour de statut lisible et maintient le focus du clavier stable, ce qui permet à NVDA/JAWS d’informer immédiatement les utilisateurs. (SITES-25368)
* Correction du comportement de l’interface utilisateur dans le panneau Remarque pour les fenêtres très étroites. À 320 px, le titre et la commande Ajouter étaient précédemment en conflit ; la barre d’outils se repositionne et conserve une séparation nette entre les éléments. Les auteurs peuvent utiliser les commandes sans perdre d&#39;informations ni de fonctions. (SITES-25376)
* Correction d’un état d’erreur persistant dans l’onglet **Liens et actions** de la boîte de dialogue **Teaser**. Une fois que les auteurs ont activé **Call to action** et corrigé les champs vides ou non valides, l’onglet efface son style et son icône d’erreur et supprime `aria-invalid`. Les lecteurs d’écran n’annoncent plus d’erreur une fois les champs validés. (SITES-25527)
* La gestion des erreurs dans les formulaires d’administration Sites répond désormais aux attentes en matière d’accessibilité. Lorsque la validation échoue, la page affiche immédiatement l’erreur, déplace le focus vers une cible de message utilisable et expose le texte aux lecteurs d’écran tels que JAWS. (SITES-27138)
* La création d’un dossier dans Sites affiche désormais un toast de confirmation clair. JAWS annonce le message par le biais de la zone géographique active, de sorte que les auteurs et autrices reçoivent immédiatement des commentaires accessibles après l’action. (SITES-27141)
* Correction d’un problème d’accessibilité en raison duquel les images des boîtes de dialogue de création étaient rendues sans texte de remplacement. La boîte de dialogue fournit désormais un texte de remplacement descriptif si nécessaire et un texte de remplacement vide pour les éléments purement visuels, ce qui permet de restaurer un comportement conforme à JAWS et aux autres lecteurs d’écran. (SITES-27153)
* Amélioration de la gestion des erreurs dans les boîtes de dialogue de création. Lorsqu’une erreur de configuration se produit, l’interface utilisateur affiche du texte explicite et déclenche une annonce de lecteur d’écran par le biais d’une zone géographique d’alerte. Les auteurs reçoivent immédiatement des commentaires et peuvent corriger le problème sans perdre de vue le contexte. (SITES-27155)
* Correction d’un défaut d’accessibilité Reflow dans l’administration de sites. Avec un zoom de navigateur de 400 %, les commandes de la barre d’outils et de la grille se chevauchaient et poussaient les actions clés hors de l’écran, ce qui bloquait la navigation au clavier et l’utilisation du lecteur d’écran. La mise en page se repositionne désormais correctement, de sorte que les boutons de recherche, de filtrage et d’action restent visibles et puissent fonctionner avec un zoom de 400 %. (SITES-27238)
* Correction d’un faible contraste dans le message de statut du verrouillage affiché dans le workflow Verrouiller/déverrouiller de la page. Le message respecte désormais un ratio de 4,5 :1, ce qui améliore la lisibilité et la conformité ADA pour les auteurs. (SITES-27270)
* Ajout de noms accessibles aux icônes de coche dans la boîte de dialogue **Autorisations effectives**. JAWS annonce maintenant les icônes et leur signification, améliorant la navigation au clavier et la conformité ADA. (SITES-27272)
* La navigation dans l’en-tête masqué acceptait le focus et déroutait les utilisateurs voyants et lecteurs d’écran. La mise à jour désactive le focus sur les contrôles réduits et expose uniquement les éléments visibles. La navigation reste prévisible et répond aux exigences de WCAG 2.4.3. (SITES-35224)

* Correction des icônes de miniatures de dossier dans l’administration de sites afin qu’elles se comportent comme des images décoratives. La mise à jour supprime le rôle de l’image et applique un texte de remplacement vide. Par conséquent, la technologie d’assistance ignore les icônes et ne lit que les libellés significatifs. (SITES-2852)
* Adobe a augmenté le contraste des couleurs pour le texte Références dans la page d’accueil Sites. Le texte est désormais conforme à la norme WCAG 2.1 AA avec un ratio d’au moins 4,5:1 et se lit clairement sur les thèmes clairs et les écrans lumineux. (SITES-24755)
* Le repère du rail Références annonce désormais son nom aux lecteurs d’écran. La région présente un `aria-label` unique (« rail de références »), qui améliore la navigation des repères et la distingue des autres régions. (SITES-24973)
* L’éditeur de texte enrichi de description a bloqué la navigation vers l’onglet et interrompu le flux de dialogue. Le correctif restaure le mouvement standard du clavier. Les auteurs continuent au-delà du champ avec un seul onglet et préservent l’ordre de sélection prévisible. (SITES-35228)
* Les contrôles de création ne disposaient pas de noms accessibles et exposaient le texte de l’icône brute, ce qui déroutait JAWS. Le correctif ajoute des libellés ARIA explicites et des rôles standard. Les annonces semblent correctes et conformes aux attentes en matière d’accessibilité. (SITES-35227)
* Comme il manquait un libellé spécifique à la liste déroulante Catégories , JAWS utilisait un « menu bouton images » générique. La mise à jour nomme le contrôle « Catégories » et définit son rôle. Les utilisateurs de lecteurs d’écran entendent un libellé précis et comprennent les choix disponibles. (SITES-35226)
* La boîte de dialogue Propriétés affichait une grille de données que les lecteurs d’écran traitaient comme du texte brut. JAWS et NVDA ont manqué le focus et n’ont pas pu annoncer les lignes et les colonnes. Le correctif ajoute de la sémantique de tableau réelle et des rôles ARIA. Les lecteurs d’écran reconnaissent désormais le tableau et effectuent correctement le suivi de la mise au point. (SITES-35225)
* L’éditeur de texte de fragment de contenu est chargé avec une barre d’actions tronquée. Les icônes ont été tronquées et le menu de débordement est devenu inaccessible. La mise à jour corrige la mise en page afin que la barre d’outils complète reste visible et accessible. (SITES-33005)
* Les champs de formulaire d’onglet de base n’affichaient pas de texte d’erreur utile. Le formulaire affiche désormais des messages clairs et intégrés et les lie au champ pour les lecteurs d’écran. Les utilisateurs d’un clavier et d’une technologie d’assistance reçoivent des conseils immédiats pour corriger la saisie. (SITES-32480)
* Le champ multiple utilisé dans un composant personnalisé exposait des boutons d’icône sans libellé et un ordre de tabulation incohérent. JAWS/NVDA annonçait uniquement les commandes « button » ou ignorées, ce qui bloquait l’utilisation du clavier. La mise à jour fournit des noms descriptifs pour Ajouter, Supprimer et Déplacer, normalise les taquets de tabulation et annonce les mises à jour de liste pour répondre aux attentes d’ADA. (SITES-30660)
* La publication rapide renvoie désormais une notification de succès claire. La boîte de dialogue se ferme, un toast confirme l’action et les lecteurs d’écran annoncent le message afin que les auteurs ne manquent pas le résultat. (SITES-26912)
* Aucune modification n’est requise. Adobe a examiné l’affirmation selon laquelle l’icône de recherche chevauche le texte voisin. L’en-tête incluait un libellé ajouté par le client ou la cliente ; AEM classique effectue uniquement le rendu de l’icône. Une instance propre affiche la disposition correcte avec un zoom de 100 %. Le bogue a donc été résolu comme étant hors de portée. (SITES-26910)
* Les thèmes Créer une page ne masquent plus l’état de focus. Les styles Aquatique et Désert offrent une mise en surbrillance cohérente sur l’onglet **De base** et les onglets adjacents lors de la navigation au clavier. Cette modification restaure une rétroaction de focus prévisible et perceptible pour les utilisateurs malvoyants. (SITES-26907)



#### Interface d’utilisation d’administration{#sites-adminui-6524}

Les utilisateurs de lecteurs d’écran n’ont reçu aucune aide à la navigation dans la grille **Plan directeur du système de catalogue**. JAWS a seulement annoncé la position de la cellule, puis s’est tue. Cette version ajoute des conseils et des rôles accessibles, ce qui permet à JAWS de lire le contexte de la liste, l’élément sélectionné et les commandes de flèche/d’espace requises. (SITES-30661)

#### Interface d’utilisation classique{#sites-classicui-6524}

Les cases à cocher de l’interface utilisateur classique perdaient leurs libellés et affichaient des options vides. Les boîtes de dialogue affichaient également le code HTML, tel que `<br>`. La mise à jour restaure les libellés de case à cocher et décode le balisage, de sorte que les boîtes de dialogue lisent correctement. (SITES-31822)

<!--
#### [!DNL Content Fragments]{#sites-contentfragments-6524}
-->

#### [!DNL Content Fragments] - Admin{#sites-admin-6524}

Les parenthèses dans un nom de fragment de contenu entraînaient une utilisation incorrecte du panneau Références. Les auteurs ont vu 0 même lorsque d’autres fragments l’ont référencé. Le correctif corrige l’analyse du chemin d’accès pour « ( » et «) » et recouvre le nombre et les entrées corrects, qui ne sont pas nuls. (SITES-35078)


#### [!DNL Content Fragments] - Éditeur de fragments{#sites-fragments-editor-6524}

* Échec de la dépublication pour les fragments de contenu dont le chemin DAM contenait des parenthèses. L’assistant Gérer la publication a réécrit « ( » et «) » et a interrompu le chemin d’accès à la ressource. Le correctif conserve les caractères et résout l’élément correct, de sorte que l’action de dépublication se termine. (SITES-35077)
* La modification d’un fragment de contenu et le retour à la liste Assets ont masqué le fragment ou le dossier entier. Échec de l’actualisation de la liste après la fermeture de l’éditeur. Le correctif actualise désormais la liste de manière fiable et maintient le fragment modifié visible sans rechargement en dur. (SITES-35374)

* L’éditeur de fragment de contenu n’a pas pu ouvrir le sélecteur de ressources Polaris, car les portées IMS requises ont été supprimées. Le correctif restaure les portées minimales et rétablit la connexion à la diffusion. La navigation et la sélection de ressources fonctionnent à nouveau, sans erreurs HTTP 500. (SITES-35837)

#### [!DNL Content Fragments] - API GraphQL {#sites-graphql-api-6524}

Après chaque déploiement, des requêtes GraphQL valides ont commencé à renvoyer des `GraphQL_QueryValidationError`. Le point d’entrée a conservé un schéma obsolète jusqu’à ce que les équipes vident les caches ou redémarrent. Le correctif actualise le schéma GraphQL et le registre des requêtes persistantes pendant le déploiement, ce qui restaure immédiatement les réponses normales. (SITES-34301)

<!--
#### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6524}


#### [!DNL Content Fragments] - REST API{#sites-restapi-6524}


#### Component Console{#sites-component-console-6524}


#### Core Backend{#sites-core-backend-6524}


#### Core Components{#sites-core-components-6524}


#### Campaign integration{#sites-campaign-integration-6524}
-->


#### ContentHub {#sites-contenthub-6524}

ContextHub n’injecte plus de seconde copie jQuery sur les pages de publication. La bibliothèque cliente du moteur de segment supprime la dépendance cq.shared qui extrayait jQuery 1.12.4, de sorte que les sites chargent un fichier jQuery cohérent et que le code front-end fonctionne de manière fiable. (SITES-30404)

#### Fragments d’expérience{#sites-experiencefragments-6524}

* Les fragments d’expérience localisent désormais l’avertissement affiché lorsqu’il n’existe aucune configuration Adobe Target. Le message s’affiche dans les paramètres régionaux de l’auteur et non en anglais. Les étapes d’exportation et d’activation sont donc lues correctement pour les équipes internationales. (SITES-11868)
* La publication d’une variation de fragment d’expérience affiche désormais un message d’erreur localisé lorsqu’aucun service cloud ne se joint à la variation. Le message s’affiche dans l’interface utilisateur dans la langue de l’utilisateur au lieu d’une chaîne en anglais uniquement. (SITES-20293)
* L’exportation d’un fragment d’expérience vers Target s’est bloquée avec `Attempt to modify attribute at illegal index: -1`. L’instrumentation Web vitals était en conflit avec l’exportateur et la gestion des attributs corrompue. Le correctif renforce le traitement des attributs et supprime ce conflit. Les exportations réussissent et le fragment est rendu dans Target. (SITES-31891)

* Les propriétés des fragments d’expérience localisent désormais l’onglet **Références**. Les libellés et les en-têtes de colonne tels que « Page », « Chemin de page » et « Titre de la variation » s’affichent dans la langue de l’auteur. Cette modification supprime les chaînes en anglais uniquement et maintient la cohérence de l’affichage des propriétés pour les équipes internationales. (SITES-11203)
* Le workflow **Variations** > **Créer** affiche désormais le texte de traduction complet. La boîte de dialogue gère les longues chaînes de paramètres régionaux en encapsulant et en dimensionnant correctement le contenu, éliminant les libellés tronqués ou tronqués. (SITES-19304)
* Les propriétés des fragments d’expérience localisent désormais les libellés de statut des médias sociaux. Les auteurs voient les valeurs de statut telles que Publié et Non publié dans leur langue sélectionnée dans tous les paramètres régionaux. Cette modification supprime les chaînes en anglais uniquement qui provoquaient une confusion lors de la révision. (SITES-20014)

<!--
#### Foundation Components (Legacy){#sites-foundation-components-legacy-6524}
-->

#### Lancements{#sites-launches-6524}

* La suppression d’un lancement très volumineux a gelé le référentiel. Le traitement a mis en file d’attente un trop grand nombre de suppressions et a privé d’autres demandes. Le correctif effectue désormais des suppressions par lots et génère des rendements entre les blocs. Le nettoyage est donc terminé pendant que le système reste réactif. (SITES-32004)

* Configuration de Launch > Propriétés affiche les listes déroulantes Société et Propriété. **Enregistrer** et **Fermer** honore les champs remplis et la validation du titre ne déclenche plus d’erreurs sur la société ou la propriété. (CQ-4359853)
* Les vérifications requises dans la configuration IMS s’exécutent lors de la mise à jour et pas seulement lors de la création. Les valeurs vides dans des champs tels que ID client ou Secret client affichent une erreur et interrompent l’enregistrement jusqu’à ce qu’une valeur valide soit saisie, empêchant la réutilisation de la valeur précédente. (CQ-4359938)
* La création de Launch affiche les chaînes de validation et d’erreur traduites. Les messages en anglais uniquement pour les échecs de création et les pages source manquantes n’apparaissent plus. Les auteurs voient des commentaires clairs et adaptés aux paramètres régionaux lors de la configuration de Launch. (SITES-13085)
* La promotion de lancement met à jour les propriétés de page `jcr:title`, `jcr:description` et `cq:redirectTarget` sur la page source. La modification supprime les exclusions de propriété dans la configuration de déploiement MSM et la logique de workflow. Les campagnes, les traductions et l’optimisation du moteur de recherche conservent des titres, des descriptions et des redirections cohérents. (SITES-34509)
* L’action Launch a ignoré la portée et a inclus des pages qui partageaient le même parent que la section cible. La mise à jour applique les limites de la sous-arborescence et ne promeut que la page choisie et ses descendants. Les pages non liées conservent leur contenu existant. (SITES-34344)
* Correction de la promotion automatique de Launch imbriquée qui s’arrêtait au niveau Auteur et ignorait le niveau Publication. La promotion automatique pour un lancement enfant publie les pages mises à jour dans les éditeurs configurés et termine le lancement complet comme prévu. (SITES-30420)

<!--
#### Link Checker{#sites-link-checker-6524}
-->

#### MSM - Live Copies{#sites-msm-live-copies-6524}

* Un déploiement au niveau du dossier n’a pas pu créer de Live Copies pour les fragments d’expérience situés sous ce dossier. Les déploiements individuels ont fonctionné, ce qui a interrompu les workflows en bloc. La modification aligne le déploiement du dossier sur le comportement de la page et propage les relations et les références dans la sous-arborescence. (SITES-35161)
* Après la suppression d’un composant dans une Live Copy, la commande **Activer l’héritage** s’est interrompue avec une erreur JavaScript et le composant est resté manquant jusqu’à une seconde tentative. La mise à jour corrige le rechargement après suppression pour transmettre les paramètres appropriés et remplace l’appel d’alerte obsolète. La boîte de dialogue s’ouvre correctement et l’héritage est restauré à la première tentative. (SITES-31387)
* L’assistant de déploiement a accepté **Ultérieurement** sans date. Les auteurs ont avancé et créé un déploiement sans planification. La mise à jour applique la sélection de la date et affiche une invite claire. L’action **Continuer** reste désactivée jusqu’à ce qu’une date existe. (SITES-31374)


#### Éditeur de page{#sites-pageeditor-6524}

* L’ouverture de l’arborescence de contenu sur une page avec un conteneur Personalization a renvoyé un panneau vide et une erreur de référence NULL de la console. Les auteurs n’ont pas pu sélectionner ni configurer de composants. La mise à jour supprime l’erreur et réactive l’arborescence et les interactions de composant. (SITES-34336)
* Le SP23 d’AEM 6.5 a interrompu la commutation de mode dans l’éditeur de page. Cliquer sur **Disposition**, **Développeur** ou **Ciblage** a bloqué l’éditeur en mode **Modifier** et a généré une `TypeError` de console. La mise à jour restaure le mode de la barre d’outils et efface l’erreur. (SITES-34536)
* L’éditeur de page s’éloignait du point d’insertion lorsque les auteurs ajoutaient des composants dans des conteneurs longs. La mise à jour ajuste le minutage de la superposition et la gestion du défilement. La vue tient sa place et le nouveau composant reste en vue et prêt à être configuré. (SITES-32621)
* Échec des libellés de balise personnalisée dans l’éditeur de page et l’interface utilisateur affichait toujours « Balises ». Le prédicat évalue désormais `fieldLabel` première et `labelText` seconde, puis applique la valeur par défaut. Les auteurs voient le libellé qu’ils ont défini. (SITES-32278)
* L’annulation du filtre Emplacement dans Sites a désaligné l’icône OmniSearch et l’a chevauchée avec le texte de l’espace réservé. Il est devenu impossible de cliquer sur l’icône. Le correctif réaligne l’icône et restaure la zone d’accès, de sorte que la souris et le clavier déclenchent tous deux la recherche. (SITES-30946)
* L’option Développeur laissait la page en mauvais état et bloquait la création sur cette page. Le panneau a disparu et l’interface utilisateur a cessé de répondre. La mise à jour répare la logique de basculement de mode et la gestion du cache, en maintenant la page modifiable et en affichant immédiatement les données du développeur. (SITES-30922)
* Cliquer sur **Effacer** dans **Insérer un nouveau composant** n’a pas supprimé la requête de recherche et a laissé la liste filtrée sur un seul élément (accordéon). Le correctif réinitialise la requête et actualise la liste. Tous les composants autorisés s’affichent à nouveau. (SITES-30921)

<!--
#### Replication{#sites-replication-6524}
-->

#### Éditeur de texte enrichi{#sites-rte-6524}

* En plein écran, l’éditeur de texte enrichi a masqué le résultat de la vérification orthographique derrière la boîte de dialogue lorsqu’aucune erreur n’existait. La mise à jour place le panneau des résultats au premier plan et conserve les messages et les suggestions visibles. Les auteurs examinent et acceptent les corrections sans quitter le mode plein écran. (SITES-32366)
* Les images de l’éditeur de texte enrichi respectent désormais l’alignement sélectionné. Les créateurs définissent à gauche, au centre ou à droite dans la boîte de dialogue de l’image et l’éditeur applique ce choix de manière cohérente dans la sortie. La modification stabilise également la boîte de dialogue Texte de remplacement afin que le texte de remplacement et l’alignement soient enregistrés et conservés lors des modifications. (SITES-30634)

#### Éditeur universel {#sites-universal-editor-6524}

La configuration du gestionnaire d’authentification des jetons de requête a dérouté les utilisateurs, car les libellés ne correspondaient pas aux champs. L’interface utilisateur a extrait du texte du chemin d’accès et affiché les mauvais noms. Le correctif restaure des libellés clairs et précis pour le classement de service et les options de jeton de requête. (SITES-31305)


### [!DNL Assets]{#assets-6524}


#### [!DNL Dynamic Media]{#assets-dm-6524}

* L’option **Sélectionner une miniature** pour les vidéos se comporte désormais correctement dans AEM Assets - Dynamic Media. Le clic permet d’ouvrir la boîte de dialogue et de sélectionner une miniature dans Assets. Le comportement précédent de clic nul n’est alors appliqué et l’extraction d’images vidéo n’est plus limitée. (ASSETS-58926)


### [!DNL Forms]{#forms-6524}

<!--
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, December 4, 2025. In addition, a list of Forms fixes and enhancements is added to this section.
-->

#### Forms Designer

* Les utilisateurs et utilisatrices ont rencontré des problèmes liés au fait que les liens hypertexte n’étaient pas cliquables dans des cas de test spécifiques, ce qui affectait leur capacité à naviguer et à vérifier les liens dans l’application. (LC-3923505)
* Les utilisateurs ont rencontré des problèmes d’accessibilité avec les PDF générés à l’aide d’AEM Forms Designer 6.5.23 pour les langues non latines. Les balises de chemin n’étaient pas placées dans un conteneur d’artefacts, ce qui entraînait des échecs dans les contrôles PAC et les lecteurs d’écran. (LC-3923295)
* Des liens hypertexte ont été rompus dans les zones de texte Portable Document Format (PDF) après l’application de correctifs des versions 6.5.21 à 6.5.23 à l’aide du service Output. (LC-3923290)
* Les utilisateurs ont rencontré des problèmes d’accessibilité avec les formulaires de document d’enregistrement (DE). Lorsque les champs de saisie étaient vides, les lecteurs d’écran ne lisaient que les légendes des champs et non les valeurs, ce qui rendait difficile la navigation efficace des utilisateurs en situation de handicap dans les formulaires. (LC-3923234)
* Les utilisateurs rencontraient des problèmes d’accessibilité dans DoR PDF forms où le NVDA lisait incorrectement « indisponible » pour les cases à cocher, les boutons radio et les champs de texte, ce qui répétait souvent le message et semait la confusion chez les utilisateurs de lecteurs d’écran. (LC-3923201)
* Les utilisateurs et utilisatrices ont rencontré une incohérence d’ordre de tabulation dans le XDP lors de l’ajout de nouveaux champs. L’ordre de tabulation existant a changé de manière inattendue, ce qui a affecté la navigation dans les formulaires. (LC-3923183, LC-3922630)
* Les utilisateurs ont rencontré des problèmes de rendu HTML. Lors de l’utilisation de l’événement `docReady`, il ne se déclenchait pas correctement dans HTML, ce qui entraînait l’exécution inattendue des scripts. (LC-3923118)
* Les utilisateurs ont rencontré des problèmes avec les scripts de rendu PDF qui ne fonctionnaient pas dans l’environnement de production AEM Forms Cloud. (LC-3923082 )
* Les utilisateurs ont rencontré des problèmes avec les champs flottants dans les formulaires. Lors de l’utilisation de différents fichiers de données, les champs flottants s’affichaient correctement avec un fichier mais pas avec l’autre, malgré des différences mineures sans rapport avec les champs. (LC-3923056)
* Les utilisateurs ont vu une page maître espagnole vierge lorsque seul le contenu en anglais était sélectionné dans un XDP (XML Data Package) avec plusieurs pages maîtres. (LC-3923009)
* Les utilisateurs ont observé des informations obsolètes sur l’année de copyright dans AEM Designer. Cela s’est produit dans la zone pop-up au démarrage, dans la section « À propos » et dans la section « Informations juridiques », qui affichait « 2003-2024 » au lieu de « 2003-2025 ». (LC-3923005)
* Les utilisateurs ont rencontré une page PDF vierge lors de l’utilisation de la pagination dans AEM Forms Designer. Le problème s’est produit lors de la sélection de « Haut de la page suivante/Haut de la page » pour WireAdviceHeader, ce qui a perturbé la mise en page des itérations de données. (LC-3922997, LC-3922830)
* Les utilisateurs ont rencontré un problème en raison duquel la valeur filedigest pour la définition de schéma (XSD) XML (Extensible Markup Language) n’était pas conservée dans la version 64 bits d’AEM Forms Designer. (LC-3922924)
* Les utilisateurs ont rencontré une mise en forme de lien hypertexte instable dans AEM Designer 6.5.19, où les liens hypertexte d’une zone de texte adoptaient incorrectement des styles du texte environnant, tels que la mise en forme du premier caractère. (LC-3922376)
* Les utilisateurs ont rencontré des problèmes lors du rendu d’HTML forms via Mobile rendering sur MAC avec AEM Forms OSGI v6.5.22. (LC-3923058)
* Les utilisateurs ont rencontré des erreurs « path object not tagged » dans les fichiers Portable Document Format (PDF) lors de l’utilisation de champs avec bordure ou arrière-plan dans les modèles XDP créés avec Designer 6.5.23 et analysés avec PAC 2024. (LC-3923013)
* Les utilisateurs ont rencontré une erreur avec la couleur d’arrière-plan de l’en-tête « Dati Richiedente » dans Composant d’application portable (PAC), et ont reçu le message « objet de chemin non balisé ». (LC-3922912)
* Les utilisateurs ont rencontré un problème en raison duquel des modèles spécifiques ont remplacé la police prévue par une police condensée. (LC-3922330)

#### Formulaires adaptatifs

* Il manquait des options dans l’éditeur de règles pour les utilisateurs. Lorsque les auteurs écrivaient des règles sur des entrées de nombre, les options Requête, UTM et Détails du navigateur n’étaient pas disponibles. (FORMS-21660)
* Les utilisateurs ont subi des blocages de l’application lors de l’interaction avec OdataResponse en raison d’une exception de pointeur nul. (FORMS-20344)
* Les utilisateurs ont rencontré des problèmes lors de la création de règles pour afficher un panneau et définir la cible d’action sur un élément à l’intérieur. La règle setFocus exécutée avant la mise à jour de la visibilité, ce qui entraîne l’échec de l’action de focus. (FORMS-19563)
* Les utilisateurs ont rencontré des problèmes de sélection de composant dans l’instance de création AEM Forms. Lorsque vous naviguez entre les onglets en mode d’édition, certains conteneurs sont devenus insélectionnables, ce qui empêchait une identification et une interaction faciles. (FORMS-18525)
* Les utilisateurs ont rencontré une erreur « URL non valide » lors de l’annotation de ressources dans AEM 6.5.22. (NPR-42684)

### Foundation {#foundation-6524}


#### Apache Felix {#foundation-apachefelix-6524}

Mise à jour du lot de la console web Felix pour inclure FELIX-6747. Ce correctif corrige la gestion des réponses qui interrompait auparavant le rendu de page et l’authentification dans la console web OSGi. La console se charge de manière cohérente et ne lance plus d’entrées IllegalStateException dans les journaux. (NPR-42730)

<!--
#### Campaign{#foundation-campaign-6524}

#### Cloud Services{#foundation-cloudservices-6524}

#### Communities {#foundation-communities-6524}

#### Content distribution{#foundation-content-distribution-6524}

#### CRX {#foundation-crx-6524}
-->

#### Granite{#foundation-granite-6524}

* Les chaînes brutes ou en anglais uniquement n’apparaissent plus dans la boîte de dialogue **Supprimer le contrôle d’accès**. La boîte de dialogue présente un contenu entièrement localisé dans les langues prises en charge pour une accessibilité cohérente. (GRANITE-48479)
* L’icône d’aide expose désormais un libellé concis aux technologies d’assistance. JAWS lit le « bouton Aide » et n’ajoute plus de libellé « menu » superflu. Cette mise à jour apporte le contrôle à la conformité WCAG 4.1.2 et simplifie l’utilisation du clavier et du lecteur d’écran. (GRANITE-55360)
* Restaurez la fabrique de moteurs de script HTL après avoir éliminé une boucle de dépendance dans les services OSGi. Les environnements démarrent correctement, le rendu HTL fonctionne dans les capsules de création et les administrateurs ne rencontrent plus d’échecs de démarrage ni de services de script manquants. (GRANITE-58276)

* La zone de recherche d’en-tête ne recouvre plus l’icône de loupe sur le texte de l’espace réservé. L’espace réservé s’affiche avec une marge intérieure appropriée et reste entièrement lisible sur tous les navigateurs. (GRANITE-54391)
* Les auteurs voient les libellés lisibles dans les champs de saisie semi-automatique plutôt que les valeurs brutes dans la boîte de dialogue. L’implémentation conserve la valeur dans le JCR et améliore la clarté pour les configurations à sélection unique et multiple qui génèrent des options de manière dynamique. (GRANITE-57615)
* Le mode d’édition reste fonctionnel lorsque htmlLibraryManager.debug est défini sur true. La modification restaure la résolution et le chargement corrects de la bibliothèque cliente, ce qui permet aux développeurs d’utiliser les outils de débogage du gestionnaire de bibliothèque HTML lors de la création. (GRANITE-58002)
* La page de modification de l’agent de réplication ne renvoie plus d’erreur JavaScript dans l’interface utilisateur classique. La page s’ouvre, affiche tous les onglets et enregistre les paramètres de l’agent sans erreur de console. (GRANITE-58302)
* Correction de l’agrégation des statuts d’intégrité dans la vue d’ensemble du système. La vue est maintenant mise à jour après l’exécution des vérifications individuelles et affiche les nombres corrects. Les opérateurs voient « OK » lorsque les vérifications de sécurité et de maintenance réussissent, au lieu d’une bannière « 2 erreurs » incorrecte. (GRANITE-61482)
* a arrêté l’exécution de `CodeUpgradeTasks` pendant les mises à niveau du LTS (support à long terme) d’AEM 6.5. La mise à niveau se poursuit désormais sans modifications ni reconfigurations du référentiel déclenchées par une tâche. Ce correctif réduit les risques de mise à niveau et empêche les temps d’arrêt évitables. (GRANITE-61486)
* Dans les boîtes de dialogue de création, les champs obligatoires affichent désormais une seule erreur de validation précise. Le message utilise le libellé du champ lorsqu’il est présent, et retourne à une invite générique lorsqu’il n’existe aucun libellé. Les messages en double et incohérents entre les champs n’apparaissent plus. (GRANITE-59531)
* La boîte de dialogue de l’assistant de création de page revalide désormais les champs requis à chaque interaction, y compris les modifications d’onglet et les modifications de plusieurs champs. Le bouton **Créer** reste désactivé jusqu’à ce que les auteurs effectuent toutes les entrées requises et que l’assistant affiche les erreurs intégrées pour les valeurs manquantes. (GRANITE-58826)

#### Intégrations{#foundation-integrations-6524}

La publication d’activités AEM Target n’échoue plus lorsque les auteurs définissent des dates de début et de fin. L’intégration envoie des horodatages conformes aux normes qui incluent le fuseau horaire, de sorte que Target traite la payload de l’activité et effectue la synchronisation comme prévu. (CQ-4360733)

<!--
#### Jetty{#foundation-jetty-6524}
-->

#### Localisation{#foundation-localization-6524}

* La localisation dans zh-CN supprime une expression ambiguë dans le statut de collecte de références affiché lors des opérations sur les ressources telles que Déplacer. L’interface utilisateur affiche désormais `正在获取对 [[0]] 项的引用`, ce qui fournit une signification précise et une terminologie cohérente. (CQ-4354648)
* La création d’une collection dynamique ne traduit plus les mots-clés de recherche enregistrés lors de l’actualisation. Les auteurs qui saisissent des termes anglais constatent que ces mêmes termes sont conservés et que la collection continue à renvoyer des résultats cohérents. (NPR-43158)
* Correction du texte d’info-bulle tronqué dans le panneau Image. La description « Afficher la légende comme pop-up » s’affiche entièrement dans tous les paramètres régionaux pris en charge, ce qui améliore le guidage des auteurs non anglophones. (SITES-10490)
* L’affichage Colonne d’administration de sites a tronqué les libellés localisés en français et en espagnol. « Heure de fin » et « Heure de désactivation » sont apparus tronqués et n’ont affiché aucune info-bulle. Adobe a corrigé les traductions et restauré l’info-bulle au survol, de sorte que les libellés soient lus en entier. (SITES-31318)
* La boîte de dialogue **Déplacer** dans Sites affichait des clés i18n brutes au lieu de libellés lisibles. Des éléments tels que « Référencer des pages », « Créé le », « Créé par » et « Chemin d’accès » étaient confus. Le correctif relie la boîte de dialogue aux dictionnaires corrects et fournit les traductions, avec un secours en anglais. (SITES-30881)

<!--
#### Oak {#foundation-oak-6524}
-->

#### Plateforme{#foundation-platform-6524}

* Les erreurs de validation affichent désormais un texte clair et descriptif au lieu d’une seule icône. Les lecteurs d’écran annoncent automatiquement le message lorsqu’il s’affiche, de sorte que les utilisateurs n’ont pas besoin d’accéder à une icône pour savoir ce qui s’est passé. (CQ-4359152)


* Les libellés de survol de la barre de navigation ne restent plus à l’écran une fois que le curseur s’est déplacé hors du contrôle. L’interface utilisateur masque immédiatement ces info-bulles lorsque le flou ou la souris disparaît, ce qui évite l’encombrement visuel et les clics incorrects. (CQ-4360030)
* Dans Sites, les actions de la barre d’outils arrêtent la création d’un second pop-up lors de clics répétés. Le deuxième clic ferme le pop-up existant et ne laisse qu’une seule instance visible, ce qui élimine le chevauchement et la distraction. (CQ-4360038)
* Le texte obsolète de 2024 relatif aux droits d’auteur n’apparaît plus. La page de connexion et le pop-up **Aide** > **À propos d’AEM** 2025 et AEM lisent l’année par programmation pour éviter les modifications manuelles. (CQ-4360042)
* Cliquer sur une info-bulle de la barre d’en-tête d’AEM ne déclenche plus l’action sous-jacente. Les fenêtres contextuelles s’ouvrent uniquement lorsque les utilisateurs cliquent sur le bouton réel, ce qui empêche les boîtes de dialogue accidentelles d’interagir avec le texte de l’info-bulle. (CQ-4360105)
* Le survol de l’année ne laisse plus de texte obsolète concernant les droits d’auteur. L’écran de connexion et la boîte de dialogue **Aide** > **À propos d’AEM** dérivent l’année de l’horloge système et effectuent le rendu de la valeur actualisée à chaque chargement de l’interface utilisateur. (CQ-4360173)
* Les pop-ups de la barre d’en-tête basculent désormais correctement. Cliquez sur la même action (par exemple, **Rechercher** ou **Filtrer**) pour fermer le pop-up ouvert au lieu d’ouvrir un autre recouvrement. La modification empêche les pop-ups empilés et renvoie la sélection au contrôle d’en-tête. (NPR-42891)
* La vue Calendrier des projets et de la boîte de réception s’affiche correctement. Le fait de changer de vue n’efface plus la page ; le calendrier charge et affiche les éléments planifiés. (NPR-42968)

<!--
#### Security{#foundation-security-6524}
-->

#### Sling{#foundation-sling-6524}

* Correction d’une erreur inattendue de compilation JSP avec le lot `org.apache.sling.scripting.jsp:2.6.0`. (SLING-12442)
* La plateforme met à niveau le moteur Sling de base de la version 2.16.2 vers la version 2.16.6. Le nouveau moteur renforce la validation d’entrée et stabilise le traitement des requêtes en cas de forte charge. (NPR-43105)

#### Éditeur de SPA {#foundation-spa-editor-6524}

L’activation du servlet principal Sling **Vérifier le type de contenu** annule les exportations de `.model.json` dans AEM 6.5 SP21/22. Les demandes ont retourné HTML ou des erreurs car l’exportateur a retourné le type mid-chain. Le correctif émet JSON avec le type correct dès le départ, de sorte `.model.json` fonctionne sur les environnements de création et de publication. (SITES-32634)


#### Traduction{#foundation-translation-6524}

* Ajout d’une opération de réindexation pour le statut du projet de traduction. Les administrateurs peuvent recréer l’index de sauvegarde lorsque la vue d’état n’est plus synchronisée, ce qui permet de restaurer les résultats et d’éliminer les avertissements de traversée d’Oak. La page se charge plus rapidement et affiche les états actuels de la tâche. (NPR-42699)
* Correction d’une régression en raison de laquelle les imports XLIFF réussissaient, mais laissaient les fichiers de dictionnaire JSON inchangés. Les imports ciblent désormais le chemin i18n correct et conservent les traductions afin que les allers-retours de localisation soient terminés sans modifications manuelles. (NPR-42989)


* Les règles de traduction XML fonctionnent désormais comme configurées. La structure de traduction respecte les règles d’exception et s’applique correctement aux modèles de `include` et de `exclude` lors de la création de tâche. Les requêtes de traduction n’envoient plus de contenu exclu. (NPR-42761)



#### Interface d’utilisation{#foundation-ui-6524}

* Correction d’une régression de l’interface utilisateur qui désactivait les entrées de la boîte de dialogue Licence Adobe Stock . La boîte de dialogue se comporte désormais normalement, accepte le texte dans les champs obligatoires et termine le flux de licence des ressources Stock à partir de la vue Détails de la ressource . (NPR-42748)

* Correction de la visibilité du groupe dans l’environnement de création. La console Groupes ne s’arrête plus à environ 41 résultats et renvoie l’ensemble complet des appartenances pour chaque utilisateur. Ce correctif restaure le comportement cohérent après des correctifs cumulatifs et maintient le renforcement de la sécurité actuelle. (NPR-42749)


<!--
#### WCM{#foundation-wcm-6524}



#### Workflow{#foundation-workflow-6524}
-->




## Installer [!DNL Experience Manager] 6.5.24.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.24.0 nécessite [!DNL Experience Manager] 6.5. Consultez la [documentation de mise à niveau](/help/sites-deploying/upgrade.md) pour des informations détaillées. <!-- UPDATE FOR EACH NEW RELEASE -->
* Le téléchargement du pack de services est disponible dans la [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.24.0.zip) d’Adobe.
* Lors d’un déploiement avec MongoDB et plusieurs instances, installez [!DNL Experience Manager] 6.5.24.0 sur l’une des instances de création à l’aide du gestionnaire de modules.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe ne recommande pas de supprimer ou de désinstaller le package [!DNL Experience Manager] 6.5.24.0. Par conséquent, avant d’installer le package, vous devez créer une sauvegarde du `crx-repository` au cas où vous auriez besoin de le restaurer. <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- FORMS For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->

### Installer le pack de services dans [!DNL Experience Manager] 6.5{#install-service-pack}

1. Redémarrez l’instance avant l’installation si l’instance est en mode de mise à jour (lorsque l’instance a été mise à jour à partir d’une version antérieure). Adobe recommande un redémarrage si le temps de disponibilité actuel d’une instance est élevé.

1. Avant l’installation, prenez un instantané ou exécutez une sauvegarde récente de votre instance [!DNL Experience Manager].

1. Téléchargez le pack de services à partir de la [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.24.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Ouvrez le gestionnaire de modules et cliquez sur **[!UICONTROL Charger le module]** pour charger le module. Pour en savoir plus, consultez la section [Gestionnaire de modules](/help/sites-administering/package-manager.md).

1. Sélectionnez le module, puis sélectionnez **[!UICONTROL Installer]**.

1. Pour mettre à jour le connecteur S3, arrêtez l’instance après l’installation du pack de services, remplacez le connecteur existant par un nouveau fichier binaire fourni dans le dossier d’installation, puis redémarrez l’instance. Consultez la section [Entrepôt de données S3 Amazon](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>La boîte de dialogue de l’interface d’utilisation du gestionnaire de modules se ferme occasionnellement pendant l’installation du pack de services. Adobe recommande d’attendre que les journaux d’erreurs se stabilisent avant d’accéder au déploiement. Attendez les journaux spécifiques liés à la désinstallation de la mise à jour complète pour vous assurer que l’installation est réussie. En règle générale, ce problème se produit dans [!DNL Safari], mais peut se produire par intermittence sur n’importe quel navigateur.

**Installation automatique**

Vous pouvez utiliser deux méthodes différentes pour installer automatiquement [!DNL Experience Manager] 6.5.24.0.<!-- UPDATE FOR EACH NEW RELEASE -->

* Placez le package dans le dossier `../crx-quickstart/install` lorsque le serveur est disponible en ligne. Le package est automatiquement installé.
* Utilisez l’[API HTTP à partir du gestionnaire de modules](/help/sites-administering/package-manager.md#package-share). Utilisez `cmd=install&recursive=true` afin que les packages imbriqués soient installés.

>[!NOTE]
>
>Experience Manager 6.5.24.0 ne prend pas en charge l’installation Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Validation de l’installation**

Pour connaître les plateformes certifiées pour travailler avec cette version, reportez-vous à la section des [exigences techniques](/help/sites-deploying/technical-requirements.md).

1. La page d’informations sur les produits (`/system/console/productinfo`) affiche le numéro de version mis à jour `Adobe Experience Manager (6.5.24.0)` sous [!UICONTROL Produits installés]. <!-- UPDATE FOR EACH NEW RELEASE -->.

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

UberJar pour [!DNL Experience Manager] 6.5.24.0 est disponible dans le [référentiel central Maven](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.24/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Pour utiliser UberJar dans un projet Maven, consultez la section [Utilisation d’UberJar](/help/sites-developing/ht-projects-maven.md) et incluez la dépendance suivante dans le POM de votre projet : <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
  <dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>uber-jar</artifactId>
  <version>6.5.24</version>
  <scope>provided</scope>          
  </dependency>
```

>[!NOTE]
>
>UberJar et les autres artefacts associés sont disponibles sur le référentiel central Maven au lieu du référentiel Maven public Adobe (`repo.adobe.com`). Le fichier UberJar principal est renommé `uber-jar-<version>.jar`. Il n’existe donc pas de `classifier` avec `apis` comme valeur pour la balise `dependency`.



## Fonctionnalités obsolètes et supprimées{#removed-deprecated-features}

Consultez [Fonctionnalités obsolètes et supprimées](/help/release-notes/deprecated-removed-features.md) pour obtenir une liste détaillée de toutes les fonctionnalités obsolètes ou supprimées pour AEM 6.5.

### Éditeur de SPA {#spa-editor}

[L’éditeur de SPA](/help/sites-developing/spa-overview.md) a été abandonné pour les nouveaux projets commençant par la version 6.5.24 d’AEM 6.5. L’éditeur de SPA reste pris en charge pour les projets existants, mais ne doit pas être utilisé pour de nouveaux projets.

Les éditeurs privilégiés pour la gestion du contenu découplé dans AEM sont désormais les suivants :

* [Éditeur universel](/help/sites-developing/universal-editor/introduction.md) pour la modification visuelle.
* [Éditeur de fragments de contenu](/help/sites-developing/universal-editor/introduction.md) pour la modification basée sur les formulaires.

## Problèmes connus{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST. -->

* **Lié à Oak**
Depuis le pack de services 13 et les versions ultérieures, le journal d’erreur suivant a commencé à s’afficher, ce qui affecte le cache de persistance :

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

   1. Installez le Pack de services ou redémarrez Experience Manager as a Cloud Service.
Les nouveaux dossiers `cache` et `diff-cache` sont automatiquement créés et vous ne voyez plus d’exception liée à `mvstore` dans `error.log`.

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

* Lorsque vous tentez de déplacer, de supprimer ou de publier des fragments de contenu, des sites ou des pages, un problème se produit lorsque les références aux fragments de contenu sont récupérées. La requête en arrière-plan échoue. En d’autres termes, la fonctionnalité ne fonctionne pas.
Pour garantir le bon fonctionnement de cette opération, vous devez ajouter les propriétés suivantes au nœud de définition d’index `/oak:index/damAssetLucene` (aucune réindexation n’est requise) :

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

* À partir de la version 6.5.15 d’AEM, le moteur JavaScript Rhino fourni par le lot ```org.apache.servicemix.bundles.rhino``` a un nouveau comportement d’hébergement. Les scripts qui utilisent le mode strict (```use strict;```) doivent déclarer leurs variables correctes. Dans le cas contraire, elles ne sont pas exécutées et finissent par générer une erreur d’exécution.

* L’installation du balisage du contenu d’usine par le biais d’un package de mise à jour officiel réinitialise la propriété languages du nœud `/content/cq:tags` par défaut. Cette action est vraie pour les packs de services, les packs de services de sécurité, les packs de correctifs, les packs de correctifs cumulatifs, les correctifs, etc. Il est donc nécessaire de l’ajouter à partir des propriétés avant l’installation.

### Problèmes connus pour AEM Sites {#known-issues-aem-sites-6524}

Fragments de contenu : la prévisualisation échoue en raison de la protection DoS pour une arborescence de fragments volumineuse. Voir l’[article de la base de connaissances sur les options de configuration par défaut de l’exécuteur de requêtes GraphQL](https://experienceleague.adobe.com/fr/docs/experience-cloud-kcs/kbarticles/ka-23945) (SITES-17934).

### Problèmes connus d’AEM Forms {#known-issues-aem-forms-6524}

>[!NOTE]
>
>Évitez de mettre à niveau vers le pack de services 6.5.24.0 pour les problèmes sans correctif disponible. Cela peut entraîner des erreurs inattendues. Effectuez la mise à niveau vers le pack de services 6.5.24.0 uniquement après la publication des correctifs requis.

#### Problèmes avec des correctifs disponibles {#aem-forms-issues-with-hotfixes}

Un correctif logiciel peut être téléchargé et installé pour les problèmes suivants. Pour résoudre ces problèmes, vous pouvez [télécharger et installer le correctif](/help/release-notes/aem-forms-hotfix.md) :

* **FORMS-20203** : Lorsqu’un utilisateur ou une utilisatrice met à niveau le framework Struts de la version 2.5.x à la version 6.x, l’UI des politiques dans AEM Forms n’affiche pas toutes les configurations, telles que l’option d’ajout d’un filigrane.

* **FORMS-20360** : après la mise à niveau vers le pack de services 6.5.24.0 d’AEM Forms, le service de conversion ImageToPDF échoue avec l’erreur :
  ```17:15:44,468 ERROR [com.adobe.pdfg.GeneratePDFImpl] (default task-49) ALC-PDG-001-000-ALC-PDG-011-028-Error occurred while converting the input image file to PDF. com/adobe/internal/pdftoolkit/core/encryption/EncryptionImp```

* **FORMS-20478** : lors de la tentative de conversion de fichiers TIFF de type 7/8 en PDF, le processus de conversion échoue avec l’erreur « ALC-PDG-001-000-Échec de la conversion Image2Pdf, en raison de : com/sun/image/codec/jpeg/JPEGCodec » et « ALC-PDG-016-003-Une erreur inconnue/inattendue s’est produite lors du post-traitement PDF. ». Le système tente d’effectuer une nouvelle tentative d’utiliser le décodeur TIFF ImageIO de TM, mais ne parvient pas à terminer le traitement.

* **FORMS-14521** : si un utilisateur ou une utilisatrice tente de prévisualiser un brouillon de lettre avec des données XML enregistrées, certaines lettres spécifiques restent bloquées à l’état `Loading`.

* AEM Forms comprend désormais une mise à niveau de Struts, de la version 2.5.33 vers la version 6.x, pour le composant de formulaire. Cette mise à niveau fournit des modifications Struts précédemment manquantes qui n&#39;étaient pas incluses dans le SP24. La prise en charge a été ajoutée via un [correctif](/help/release-notes/aem-forms-hotfix.md) que vous pouvez télécharger et installer. La dernière version de Struts est alors prise en charge.

#### Autres problèmes connus {#aem-forms-other-known-issues}

* Après l’installation du pack de services AEM Forms JEE 21 (6.5.21.0), vous pouvez trouvez des entrées en double de fichiers JAR Geode `(geode-*-1.15.1.jar and geode-*-1.15.1.2.jar)` sous le dossier `<AEM_Forms_Installation>/lib/caching/lib` (FORMS-14926). Suivez ces étapes pour résoudre le problème :

   1. Arrêtez les localisateurs s’ils sont en cours d’exécution.
   2. Arrêtez le serveur AEM.
   3. Accédez à `<AEM_Forms_Installation>/lib/caching/lib`.
   4. Supprimez tous les fichiers de correctifs Geode, à l’exception de `geode-*-1.15.1.2.jar`. Confirmez que seuls les fichiers JAR Geode avec `version 1.15.1.2` sont présents.
   5. Ouvrez l’invite de commande en mode administration.
   6. Installez le correctif Geode à l’aide du fichier `geode-*-1.15.1.2.jar`.

* Après la mise à niveau du pack de services 18 ou 19 d’AEM Forms 6.5 vers le pack de services 20 ou 21, une erreur de compilation JSP s’affiche. Cette erreur empêchait d’ouvrir ou de créer des formulaires adaptatifs. Cela provoquait également des problèmes avec d’autres interfaces AEM. Ces interfaces comprenaient l’éditeur de page, l’interface d’utilisation d’AEM Forms, l’éditeur de workflow et l’interface d’utilisation Présentation du système. (FORMS-15256)

  Si vous rencontrez ce problème, procédez comme suit pour le résoudre :
   1. Accédez au répertoire `/libs/fd/aemforms/install/` dans CRXDE.
   2. Supprimez le lot dont le nom est `com.adobe.granite.ui.commons-5.10.26.jar`.
   3. Redémarrez votre serveur AEM.

* Dans l’aperçu avant impression de l’IU de l’agent de communication interactive, le symbole monétaire (comme le symbole du dollar « $ ») s’affiche de manière incohérente pour toutes les valeurs de champ. Il s’affiche pour les valeurs allant jusqu’à 999, mais il est absent pour les valeurs supérieures ou égales à 1 000. (FORMS-16557)
* Les modifications apportées au fichier XDP des fragments de mise en page imbriqués dans une communication interactive ne sont pas répercutées dans l’éditeur de communication interactive. (FORMS-16575)
* Dans l’aperçu avant impression de l’IU de l’agent de communication interactive, certaines valeurs calculées ne s’affichent pas correctement. (FORMS-16603)
* Lorsque la lettre est affichée dans l’aperçu avant impression, le contenu change. Certains espaces disparaissent et certaines lettres sont remplacées par `x`. (FORMS-15681)
* **FORMS-15428** : après la mise à jour vers le pack de services 20 (6.5.20.0) d’AEM Forms avec le module complémentaire Forms, les configurations reposant sur l’ancien service Adobe Analytics Cloud à l’aide de l’authentification basée sur les informations d’identification ne fonctionnent plus. Ce problème empêchait les règles d’analyse de s’exécuter correctement.

* Lorsqu’un utilisateur ou une utilisatrice configure une instance WebLogic 14c, le service PDFG dans le pack de services 21 d’AEM Forms sur JEE (6.5.21.0) s’exécutant sur JBoss® échoue en raison de conflits de chargeurs de classes impliquant la bibliothèque SLF4J. L’erreur s’affiche comme suit (CQDOC-22178) :

  ```java
  Caused by: java.lang.LinkageError: loader constraint violation: when resolving method "org.slf4j.impl.StaticLoggerBinder.getLoggerFactory()Lorg/slf4j/ILoggerFactory;"
  the class loader org.ungoverned.moduleloader.ModuleClassLoader @404a2f79 (instance of org.ungoverned.moduleloader.ModuleClassLoader, child of 'deployment.adobe-livecycle-jboss.ear'
  @7e313f80 org.jboss.modules.ModuleClassLoader) of the current class, org/slf4j/LoggerFactory, and the class loader 'org.slf4j.impl@1.1.0.Final-redhat-00001' @506ab52
  (instance of org.jboss.modules.ModuleClassLoader, child of 'app' jdk.internal.loader.ClassLoaders$AppClassLoader) for the method's defining class, org/slf4j/impl/StaticLoggerBinder,
  have different Class objects for the type org/slf4j/ILoggerFactory used in the signature.
  ```

* **FORMS-21378** : lorsque la validation côté serveur (SSV) est activée, les envois de formulaires peuvent échouer. Si vous rencontrez ce problème, contactez l’assistance Adobe pour obtenir de l’aide.

* **FORMS-23703** : lorsque la règle `contains` est configurée sans valeur par défaut, la validation côté serveur d’un formulaire adaptatif échoue. Vous pouvez installer la dernière version du pack de services [AEM Forms 6.5.24.0](https://experienceleague.adobe.com/fr/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases#aem-65-forms-releases) pour résoudre le problème.

## Lots OSGi et modules de contenu inclus{#osgi-bundles-and-content-packages-included}

Les documents texte suivants répertorient les lots OSGi et les modules de contenu inclus dans cette version du pack de services [!DNL Experience Manager] 6.5.

* [Liste des lots OSGi inclus dans Experience Manager 6.5.24.0](/help/release-notes/assets/65240-bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Liste des packages de contenu inclus dans Experience Manager 6.5.24.0](/help/release-notes/assets/65240-packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Sites web à accès limité{#restricted-sites}

Ces sites web sont disponibles uniquement pour les clientes et clients. Si vous êtes client et avez besoin d’un accès, contactez votre responsable de compte Adobe.

* [Téléchargement du produit à l’adresse licensing.adobe.com](https://licensing.adobe.com/)
* [Contacter l’assistance clientèle Adobe](https://experienceleague.adobe.com/fr/docs/customer-one/using/home).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] page produit](https://business.adobe.com/fr/products/experience-manager/adobe-experience-manager.html)
>* Documentation [[!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/fr/docs/experience-manager-65)
>* [S’abonner aux mises à jour de produits prioritaires d’Adobe](https://www.adobe.com/subscription/priority-product-update.html)
