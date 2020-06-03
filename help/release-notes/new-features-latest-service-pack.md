---
title: Nouveautés d’Adobe Experience Manager 6.5 Service Pack 5
description: Nouveautés d’Adobe Experience Manager 6.5 Service Pack 5
contentOwner: AK
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: cc423a199e860429e85895690f6c1a81c20d1a19
workflow-type: tm+mt
source-wordcount: '1853'
ht-degree: 12%

---


# What&#39;s new in AEM 6.5 Service Pack 5 {#aem-whats-new-service-pack-5}

Les Service Packs Adobe Experience Manager 6.5 vous offrent de nouvelles fonctionnalités, les améliorations demandées par les clients, les performances et les améliorations liées à la stabilité à tous les trimestres. Le modèle de diffusion trimestriel facilite l&#39;accès et l&#39;adoption de nouvelles fonctionnalités et innovations.

Cet article présente les fonctionnalités incluses dans le dernier Service Pack 6.5, les fonctionnalités [clés incluses dans les Service Packs](#key-features-previous-service-packs)6.5 précédents et certaines des versions [clés depuis la version 6.5.4.0](#key-features-sice-sp3) d’Experience Manager.

## AEM Sites {#aem-sites}

### Améliorations de l’accessibilité {#accessibility-sites}

* Amélioration du rapports d&#39;erreur en ajoutant des informations sur le texte

* Amélioration de la mise au point de l’interface utilisateur lors de la navigation au clavier

* Amélioration du contraste du texte (rapport de luminosité)

* Amélioration de la cohérence des attributs de remplacement pour les images de page

* Amélioration de la cohérence des étiquettes des applications Internet enrichies accessibles (ARIA)

* Amélioration des fonctionnalités NVDA (Non Visual Desktop Access)

* Amélioration de la prise en charge des lecteurs d’écran

### Autres améliorations clés {#other-enhancements-sites}

* Lors de la copie ou du collage d’une arborescence de page, vous avez désormais la possibilité de coller la page racine ou de coller la page racine avec les sous-pages de l’arborescence.

* Les fragments d’expérience AEM exportés vers les espaces de travail Cible Adobe apparaissent désormais sous la forme de types d’offre uniques et de sources d’offre dans [!DNL Target].

* Gestionnaire de sites multiples : le déclencheur de publication supprime désormais un composant de la page publiée si un composant est supprimé de la page source.

* Gestionnaire de sites multiples : lorsque le nom d&#39;un composant local dans une LiveCopy est identique au nom d&#39;un composant dans le plan et que le composant est déployé à partir du plan, le terme _msm_move est maintenant ajouté avec succès au nom du composant local.

## AEM Assets {#aem-assets}

### Améliorations de l’accessibilité dans les ressources {#assets-accessibility}

[!DNL Adobe Experience Manager] Les fonctionnalités des ressources sont désormais plus accessibles conformément aux directives WCAG (Web Content Accessibility Guidelines). L&#39;accessibilité s&#39;est améliorée dans les domaines suivants :

* Les éléments, commandes, pages et boîtes de dialogue de l’interface utilisateur sont faciles à lire.

* Les éléments, les contrôles et les champs de formulaire d’entrée de l’interface utilisateur sont accessibles à l’aide du clavier.

* Changement de couleur et de contraste de certains graphiques à distinguer par les utilisateurs avec une vision limitée et sans perception de couleur. Par exemple, la couleur des icônes d’évaluation des étoiles (par exemple, dans la section [!UICONTROL Évaluation] de l’onglet [!UICONTROL Avancé] dans [!UICONTROL Propriétés] de la ressource ou dans la vue de la carte) est modifiée pour un contraste approprié.

![changement de la couleur des icônes d’évaluation des étoiles pour améliorer le contraste](assets/star-rating-icons.png)

### Amélioration de la gestion des exceptions {#exception-handling}

Le flux de l’interface utilisateur des ressources permet une meilleure gestion des exceptions. Auparavant, si un fichier n’avait pas le type approprié pour sa dimension, une exception a été observée qui a été interceptée en silence sans trace dans les journaux. Ce comportement a changé et toutes les exceptions sont prises en compte dans les journaux.

## [!DNL Dynamic Media] {#dynamic-media}

### Prise en charge 3D dans [!DNL Dynamic Media] {#support-for-3d}

La prise en charge 3D permet [!DNL Dynamic Media] désormais aux clients de publier et d&#39;ajouter du contenu 3D aux pages Web et aux applications. Il comprend :

* Publication de formats de fichier 3D courants pour générer une URL de fichier.

* Affichage interactif des ressources 3D publiées à l’aide d’un nouveau lecteur Web 3D disponible dans la bibliothèque du [!DNL Dynamic Media] lecteur, optimisé par Adobe Dimension.

* Publication et affichage 3D sur [!DNL Experience Manager Sites] la page à l’aide du composant [!DNL Sites] WCM.

## AEM Forms {#aem-forms}

### Personnalisation des colonnes de la boîte de réception AEM {#customize-aem-inbox-columns}

Vous pouvez personnaliser une boîte de réception AEM pour modifier le titre par défaut d’une colonne, réorganiser la position d’une colonne et afficher des colonnes supplémentaires en fonction des données d’un processus. Vous devez être membre de `administrators` ou de `workflow-administrators` groupe pour personnaliser les colonnes.

![Personnalisation des colonnes de la boîte de réception AEM](assets/customize-columns.gif)

### Enregistrer les communications interactives en tant que brouillon {#save-as-draft}

Vous pouvez utiliser l’interface utilisateur de l’agent pour enregistrer un ou plusieurs brouillons pour chaque communication interactive et récupérer le brouillon ultérieurement pour continuer à travailler dessus. Vous pouvez spécifier un nom différent pour chaque brouillon pour une identification plus facile.

![Enregistrer en tant que brouillon](assets/save-as-draft.gif)

### [!DNL Oracle WebLogic] prise en charge du serveur d’applications {#weblogic-support}

AEM Forms a ajouté la prise en charge [!DNL Oracle WebLogic 12] d’AEM Forms sur JEE. Vous pouvez effectuer une mise à niveau à partir d’une version précédente ou configurer un nouveau serveur AEM Forms 6.5 sur JEE sur [!DNL Oracle WebLogic] 12.2.1.4 et versions ultérieures. Plus tard correspond aux changements mineurs de version, où x dans 12.2.1.x est remplacé par un numéro de version.

### Améliorations de l’accessibilité {#accessibility-improvements}

AEM Forms comprend les améliorations d’accessibilité suivantes :

* Lorsqu’un utilisateur prévisualisation un formulaire adaptatif sous la forme d’un formulaire HTML, le champ Signature  tactile conserve la cible d’action de l’onglet.

* Les messages d’erreur affichés lors de l’envoi d’un formulaire adaptatif contiennent désormais l’ `aria-describedBy` attribut. L’attribut est attaché aux champs référencés dans le message d’erreur. L’ `aria-describedby` attribut indique les identifiants des éléments qui décrivent l’objet. Il permet d’établir une relation entre les widgets ou les groupes et le texte qui les décrit.

* Si un formulaire adaptatif comporte certains champs obligatoires, l’attribut obligatoire est défini sur `True` pour ces champs dans le schéma d’accessibilité ARIA.

### Authentification par certificat X-509 pour les services Web SOAP dans le modèle de données de formulaire {#x509-based-authentication-soap}

Le modèle de données de formulaire prend désormais en charge l’authentification par certificat X-509 lors de l’utilisation des services Web SOAP en tant que source de données.

### Autres améliorations clés {#other-improvements}

* La sécurité du Document d’AEM Forms 6.5 sur JEE est désormais basée sur [!DNL Apache Struts 2].

* Prise en charge Ajoutée pour [!DNL Oracle Real Applications Cluster (RAC) 19c].

## Principales fonctionnalités des Service Packs AEM 6.5 précédents {#key-features-previous-service-packs}

### AEM Sites {#aem-sites-previous-service-packs}

#### Améliorations du système de style (6.5.4.0) {#style-system-enhancements}

Vous pouvez désormais sélectionner des styles dans la boîte de dialogue du composant à l’aide du système de style amélioré.

#### Amélioration des performances dans divers domaines (6.5.4.0) {#performance-improvements}

* Réduction du temps de chargement et d’initialisation de ContextHub au sein d’un site (`contexthub.kernel.js`). Le chargement des pages s’en trouve accéléré lors d’une visite du site.

* Réduction du temps d’actualisation d’une page après avoir fait glisser des fragments d’expérience vers l’éditeur de page Sites.

* Réduction du temps de chargement des entrées sur une page Sites avec plus de 200 copies dynamiques dans la Présentation **[!UICONTROL de la]** Live Copy.

* Amélioration de la gestion des URL incomplètes ou non valides. De telles URL peuvent ralentir l’éditeur de modèles.

### AEM Assets {#aem-assets-previous-service-packs}

#### Configure AEM Assets with Brand Portal (6.5.4.0) {#configure-assets-bp}

Le canal d’autorisation entre les ressources AEM et le portail de marque est modifié. Auparavant, Brand Portal était configuré dans l’interface utilisateur classique via la passerelle OAuth héritée, qui fait appel à l’échange de jetons JWT pour obtenir un jeton d’accès IMS en vue de l’autorisation. AEM Assets est désormais configuré avec Brand Portal via Adobe I/O, qui fournit un jeton IMS pour autoriser votre client Brand Portal.

Les étapes de configuration des ressources AEM avec le portail de marque sont différentes selon votre version d’AEM et selon que vous effectuez une configuration pour la première fois ou une mise à niveau des configurations existantes. Voir [Configuration d’AEM Assets avec Brand Portal](https://docs.adobe.com/content/help/fr-FR/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html) pour plus de détails.

#### Accessibility enhancements (6.5.4.0) {#accessibility-enhancements}

Experience Manager Assets comprend les améliorations d’accessibilité suivantes :

* Les touches fléchées du clavier permettent de déplacer et de faire défiler des zones dans les images agrandies. Pour plus d’informations, voir Fichiers de [prévisualisation utilisant uniquement](../assets/managing-assets-touch-ui.md#previewing-assets)les touches du clavier.

* Les cases à cocher d’état mixte (dans lesquelles, à moins que vous ne sélectionniez tous les prédicats imbriqués, les cases de premier niveau ne sont pas sélectionnées et sont enfoncées) dans le panneau Filtres sont lisibles par les lecteurs d’écran.

* Les contraintes de format de date et d’heure sont fournies dans les libellés de champs des champs de date, afin de permettre aux utilisateurs de saisir la date dans le format correct à l’aide du clavier.

   Par exemple, `On Time (MM-DD-YYYY HH:mm)`. Ici MM est le mois en format à deux chiffres, AAAA est l&#39;année, JJ est le jour en format à deux chiffres, HH est l&#39;heure en format militaire à 24 heures et mm est la minute.

* Le `X` symbole du bouton permettant de supprimer les balises actuellement sélectionnées est maintenant annoncé par les lecteurs d’écran, ainsi que le nombre de balises sélectionnées.

#### Recherche visuelle des ressources AEM (6.5.2.0) {#visual-search}

Les utilisateurs de ressources peuvent rechercher des images visuellement similaires. AEM affiche les images balisées intelligentes du référentiel DAM qui sont similaires à une image sélectionnée par l’utilisateur. See [Visual search](../assets/search-assets.md).

### Dynamic Media {#dynamic-media-previous-service-packs}

#### Smart Imaging for Dynamic Media {#smart-imaging}

L’imagerie intelligente utilise les caractéristiques d’affichage uniques de chaque utilisateur pour fournir automatiquement les images appropriées optimisées pour leur expérience, ce qui se traduit par de meilleures performances et un meilleur engagement. L’imagerie dynamique fonctionne avec vos paramètres d’image prédéfinis et utilise des informations à la dernière milliseconde de la diffusion pour réduire davantage encore la taille du fichier d’image en fonction de la vitesse de connexion du réseau et du navigateur. Voir [Smart Imaging](../assets/imaging-faq.md).

#### Recadrage intelligent dans les profils vidéo pour les médias dynamiques (6.5.3.0) {#smart-crop-video}

Le recadrage intelligent pour la vidéo (une fonctionnalité en option dans les profils vidéo) est un outil qui utilise la puissance de l’intelligence artificielle d’Adobe Sensei pour détecter et rogner automatiquement le point focal dans toute vidéo adaptative ou progressive que vous avez chargée, quelle que soit sa taille. See [About using smart crop in video profiles](../assets/video-profiles.md).

### AEM Forms {#aem-forms-previous-service-packs}

#### Générer une sortie imprimable dans les workflows AEM Forms (6.5.4.0) {#generate-printable-output}

L’étape de flux de travail Générer une sortie imprimable vous permet d’intégrer un fichier de modèle source à un fichier de données. Cette intégration vous permet d’imprimer ou d’enregistrer différentes copies du fichier de modèle. L’étape génère une sortie PCL, PostScript, ZPL, IPL, TPCL ou DPL. Pour plus d’informations sur cette fonctionnalité, voir Flux de travaux [Forms sur OSGi - Guide de référence](../forms/using/aem-forms-workflow-step-reference.md)des étapes.

![Générer une sortie imprimable](assets/generate-print-output-step.gif)

#### Prise en charge de plusieurs colonnes pour les formulaires adaptatifs et les communications interactives en mode Mise en page (6.5.4.0) {#multi-column-adaptive-forms}

Vous pouvez désormais définir le nombre de colonnes pour un panneau dans les formulaires adaptatifs et les communications interactives. Passez en mode de mise en page pour utiliser la nouvelle option à colonnes multiples. Pour plus d’informations, voir [Utilisation du mode Mise en page pour redimensionner des composants](../forms/using/resize-using-layout-mode.md).

![Mise en page multi-colonnes](assets/multi-column-layout.gif)

#### Personnalisations de la boîte de réception AEM (6.5.4.0) {#aem-inbox}

La nouvelle option de contrôle d’administration permet aux administrateurs d’effectuer les opérations suivantes :

* Personnaliser le texte et le logo de l&#39;en-tête

* Contrôler l&#39;affichage des liens de navigation disponibles dans l&#39;en-tête

L’option Contrôle d’administration n’est visible que pour les membres des administrateurs ou du groupe d’administrateurs de processus. Pour plus d’informations sur cette fonctionnalité, voir [Votre boîte de réception](../sites-authoring/inbox.md).

#### Prise en charge du texte enrichi dans les formulaires HTML5 (6.5.4.0) {#rich-text-support}

Convertissez un champ de texte d’un formulaire XFA en champ de texte enrichi dans un formulaire HTML5. Pour plus d’informations, voir [Conception de modèles de formulaire pour les formulaires](../forms/using/designing-form-template.md)HTML5.

#### Accessibility enhancements (6.5.4.0) {#forms-accessibility-enhancements-6540}

Experience Manager Forms comprend les améliorations d’accessibilité suivantes :

* Les lecteurs d’écran annoncent correctement les cases à cocher, les liens, le sélecteur de date et les champs de saisie de date dans un formulaire adaptatif.

* Chaque page d’un formulaire adaptatif comprend désormais un titre et une étiquette de repère principale.

#### Partage et demande l’accès aux éléments de boîte de réception d’un utilisateur AEM Forms (6.5.3.0) {#share-request-access}

Vous pouvez partager vos éléments de boîte de réception avec un autre utilisateur. Une fois qu&#39;un autre utilisateur a accès à vos éléments de boîte de réception, il peut demander et prendre les mesures appropriées sur les éléments partagés. De même, vous pouvez demander l’accès aux éléments de boîte de réception à d’autres utilisateurs. Voir [Partage et demande d’accès aux éléments de boîte de réception d’un utilisateur](../forms/using/configure-shared-queues-osgi.md).

#### Configuration des paramètres d’absence du bureau pour les éléments de boîte de réception d’un utilisateur AEM Forms (6.5.3.0) {#configure-out-of-office}

Si vous prévoyez d’être absent du bureau, vous pouvez indiquer ce qui se passe pour les éléments qui vous sont affectés pour cette période.
Vous pouvez spécifier une date et une heure de début, ainsi qu’une date et une heure de fin, pour l’application de vos paramètres d’absence du bureau. Vous pouvez définir une personne par défaut à laquelle tous vos éléments sont envoyés. Voir [Configuration des paramètres](../forms/using/configure-out-of-office-settings.md)d’absence du bureau.

#### Générer plusieurs communications interactives à l’aide de l’API de lot pour AEM Forms (6.5.3.0) {#generate-multiple-ic}

Vous pouvez utiliser l’API de traitement par lots pour produire plusieurs communications interactives à partir d’un modèle. Le modèle est une communication interactive sans données. L’API de traitement par lots combine les données avec un modèle pour produire une communication interactive. L&#39;API est utile pour la production de masse de communications interactives. Par exemple, factures de téléphone, relevés de carte de crédit pour plusieurs clients. Voir [Générer plusieurs communications interactives à l’aide de l’API](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)de traitement par lot.

## Principales versions depuis AEM 6.5 SP4 {#key-releases-since-last-sp}

Entre le 05 mars 2020 et le 04 juin 2020, Adobe a publié les fonctionnalités suivantes qui ne sont pas du livrable principal d’AEM :

* AEM Cloud Manager [2020.3.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-2020-3-0.html), [2020.4.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-2020-4-0.html)et [2020.5.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-current.html)

* [AEM Assets : Application de bureau 2.0.2.0](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/release-notes.html)

* [AEM Screens : Feature Pack 202004](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/release-notes/release-notes-fp-202004.html)

## Ressources utiles

* [Guides d’utilisation d’AEM 6.5](../user-guide/home.md)

* [Notes de mise à jour générales d’Adobe Experience Manager 6.5](release-notes.md)

* [Notes de mise à jour du Service Pack pour Adobe Experience Manager 6.5](sp-release-notes.md)
