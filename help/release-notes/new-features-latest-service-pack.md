---
title: Nouveautés de Adobe Experience Manager 6.5 Service Pack 7
description: Nouveautés de Adobe Experience Manager 6.5 Service Pack 7
contentOwner: AK
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: a24b66506440eb2153d5589e8c79dbfafb24df66
workflow-type: tm+mt
source-wordcount: '2780'
ht-degree: 5%

---


# Nouveautés de Adobe Experience Manager 6.5 Service Pack 7 {#aem-whats-new-service-pack}

![Nouveautés](assets/whatsnew.jpeg)

[!DNL Adobe Experience Manager] Les Service Packs 6.5 offrent de nouvelles fonctionnalités, des améliorations demandées par les clients, ainsi que des améliorations des performances, de la stabilité et de la sécurité à tous les trimestres. La disponibilité trimestrielle facilite l&#39;accès et l&#39;adoption de nouvelles fonctionnalités et innovations.

Cet article présente les fonctionnalités incluses dans la dernière version du Service Pack 6.5, [les fonctionnalités clés incluses dans les Service Packs 6.5 précédents](#key-features-previous-service-packs) et les [principales AEM versions depuis la dernière version du Service Pack](#key-releases-since-last-sp).

## Adobe [!DNL Experience Manager Sites] {#aem-sites}

### Disponibilité des déplacements de page et des déploiements MSM en tant qu&#39;opérations asynchrones {#page-moves-msm-asynchronous}

Vous pouvez désormais effectuer les déplacements de page et les déploiements MSM en tant qu’opérations asynchrones afin de réduire leur impact sur les performances d’exécution. Vous pouvez planifier les opérations pour une exécution immédiate ou ultérieure. L’état des tâches et étapes de processus associées s’affiche dans une console, ce qui s’avère utile pour surveiller les déploiements MSM à grande échelle.

## [!DNL Adobe Experience Manager Assets] {#aem-assets}

* [!DNL Assets] et  [!DNL Dynamic Media] offrent plusieurs améliorations d’accessibilité. Les améliorations ont trait à la navigation au clavier, à l’utilisation de lecteurs d’écran, ainsi qu’à l’utilisation de technologies d’assistance (AT). Voir [[!DNL Assets] améliorations](/help/release-notes/sp-release-notes.md#assets-6570) et [[!DNL Dynamic Media] améliorations](/help/release-notes/sp-release-notes.md#dynamic-media-6570).

* Les utilisateurs peuvent trier les fichiers numériques dans les vues Carte et Colonne.

## [!DNL Adobe Experience Manager Forms] {#aem-forms}

>[!NOTE]
>
>[!DNL Experience Manager Forms] les packages de modules complémentaires sont rendus disponibles une semaine après la publication du  [!DNL Experience Manager] Service Pack planifié.

### Amélioration des performances {#performance-improvements-forms}

[!DNL Experience Manager] 6.5 Service Pack 7 Forms améliore les performances pour :

* Validation des valeurs de champ sur le serveur lors de l’envoi d’un formulaire adaptatif.

* Conversion d’un formulaire PDF en formulaire adaptatif à l’aide de [!DNL Automated Forms Conversion service].

### Modèle de données de formulaire configuration du client HTTP pour optimiser les performances {#fdm-http-client-config}

[!DNL Experience Manager Forms] modèle de données de formulaire lors de l’intégration avec les services Web RESTful en tant que source de données inclut désormais des configurations de client HTTP pour l’optimisation des performances. Voir [Configurer les sources de données](../../help/forms/using/configure-data-sources.md#fdm-http-client-configuration).

### Disponibilité de l&#39;option de réinitialisation pour chaque composant en mode Disposition {#reset-option-layout-mode}

Vous pouvez désormais utiliser l’option reset pour chaque composant en mode Mise en page d’un formulaire adaptatif. Lorsque vous définissez une mise en page à plusieurs colonnes pour un panneau, vous pouvez utiliser cette fonction pour réinitialiser des composants individuels dans le panneau. Voir [Utiliser le mode de mise en page pour redimensionner les composants](../../help/forms/using/resize-using-layout-mode.md#resize-components).

### Prise en charge de Microsoft SQL Server 2019

[!DNL Experience Manager Forms] prend désormais en charge Microsoft SQL Server 2019.

## Fonctions clés des Service Packs {#key-features-previous-service-packs} 6.5 précédents[!DNL Experience Manager]

### [!DNL Experience Manager Sites] {#aem-sites-previous-service-packs}

#### Disponibilité de l&#39;opération de déplacement de page en mode asynchrone (6.5.6.0) {#page-move-asynchronous}

L’opération de déplacement de page est désormais disponible en mode asynchrone. Outre l’exécution immédiate, vous pouvez également planifier l’opération Déplacement de page pour une exécution ultérieure.

#### Améliorations de l&#39;accessibilité (6.5.5.0) {#accessibility-sites}

* Rapports d&#39;erreur amélioré en ajoutant des informations sur le texte.

* Amélioration de la mise au point de l’interface utilisateur lors de la navigation au clavier.

* Amélioration du rapport de contraste pour divers éléments de l’interface utilisateur.

* Amélioration de la cohérence des attributs de remplacement pour les images de page.

* Amélioration de la cohérence des étiquettes des applications Internet enrichies accessibles (ARIA).

* Amélioration des fonctionnalités NVDA (Non Visual Desktop Access).

* Prise en charge du lecteur d’écran améliorée.

#### Autres améliorations clés (6.5.5.0) {#other-enhancements-sites}

* L&#39;accès anonyme au CRXDE Lite n&#39;est pas autorisé pour améliorer la sécurité. Les utilisateurs sont redirigés vers l’écran de connexion. Voir [Développement avec le CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

* Lors de la copie ou du collage d’une arborescence de page, vous avez désormais la possibilité de coller la page racine ou de coller la page racine avec les sous-pages de l’arborescence.

* [!DNL Adobe Experience Manager Experience Fragments] Les  [!DNL Adobe Target] espaces de travail exportés s’affichent désormais sous la forme de types d’offre uniques et de sources d’offre dans  [!DNL Target].

* Gestionnaire de sites multiples : le déclencheur de publication supprime désormais un composant de la page publiée si un composant est supprimé de la page source.

* Gestionnaire de sites multiples : lorsque le nom d&#39;un composant local d&#39;une [!UICONTROL Live Copy] est identique au nom d&#39;un composant du plan et que le composant est déployé à partir du plan directeur, le terme `_msm_moved` est maintenant ajouté au nom du composant local.

#### Améliorations du système de style (6.5.4.0) {#style-system-enhancements}

Vous pouvez désormais sélectionner des styles dans la boîte de dialogue du composant à l’aide du système de style amélioré.

#### Amélioration des performances dans divers domaines (6.5.4.0) {#performance-improvements}

* Réduction du temps de chargement et d’initialisation de ContextHub dans un site (`contexthub.kernel.js`). Le chargement des pages s’en trouve accéléré lors d’une visite du site.

* Réduction du temps d’actualisation d’une page après avoir fait glisser [!DNL Experience Fragments] vers [!DNL Sites] l’éditeur de page.

* Réduction du temps de chargement des entrées sur une page [!DNL Sites] avec plus de 200 copies dynamiques dans **[!UICONTROL Aperçu de la Live Copy]**.

* Amélioration de la gestion des URL incomplètes ou non valides. De telles URL peuvent ralentir l’éditeur de modèles.

### [!DNL Adobe Experience Manager Assets] {#aem-assets-previous-service-packs}

#### Améliorations de l’accessibilité (6.5.6.0) {#accessibility-assets-6560}

* **Amélioration de la mise au point de l’interface utilisateur lors de la navigation** au clavier, par exemple en mettant l’accent sur :

   * `x` dans la boîte de dialogue  [!UICONTROL Prévisualisation ] de version d’une ressource dans le  [!UICONTROL journal].

   * Options d’interface utilisateur utilisables.

   * Champ Courriel de la boîte de dialogue [!UICONTROL Partager le lien] et champ permettant d’ajouter un groupe d’utilisateurs fermé dans l’onglet [!UICONTROL Autorisation] du dossier [!UICONTROL Propriétés].

* **Fonctionnalité améliorée à l’aide des touches du clavier**

   Les utilisateurs peuvent utiliser les touches du clavier pour faire glisser des commandes dans l’éditeur de Schémas de métadonnées en mode de navigation du lecteur d’écran.

* **Amélioration de l’utilisation des lecteurs** d’écran en raison des éléments suivants :

   * Les lecteurs d’écran annoncent l’objectif des lecteurs vidéo et audio.

   * Les lecteurs d’écran annoncent l’objectif des options de l’interface utilisateur pour supprimer les balises sélectionnées à l’aide de la boîte de dialogue de sélection [!UICONTROL Balises] sur la ressource [!UICONTROL Propriétés].

   * Les lecteurs d’écran annoncent les en-têtes de ligne et les éléments de ligne des tableaux afin que les utilisateurs sachent quelles entrées appartiennent à la même ligne.

   * Titre de page significatif et descriptif de la page de recherche.

   * Les lecteurs d’écran annoncent les options du panneau de filtre de recherche sous forme d’accordéons extensibles.

#### Autres améliorations dans [!DNL Assets] (6.5.6.0) {#other-enhancements-assets-6560}

* Les groupes d’utilisateurs associés aux dossiers (privés et non privés) sont maintenant supprimés du référentiel lors de la [suppression de ces dossiers](/help/assets/private-folder.md#delete-private-folder). Toutefois, les groupes d’utilisateurs redondants, orphelins, inutilisés et générés automatiquement existants peuvent être supprimés du référentiel à l’aide de JMX.

#### Améliorations de l&#39;accessibilité dans [!DNL Assets] (6.5.5.0) {#assets-accessibility}

[!DNL Experience Manager Assets] est désormais plus accessible en conformité avec les Web Content Accessibility Guidelines (WCAG). L’accessibilité a été améliorée en raison des améliorations suivantes :

* De nombreux éléments, commandes, pages et boîtes de dialogue de l’interface utilisateur sont compatibles avec le lecteur d’écran.

* De nombreux éléments, contrôles et champs de formulaire d’entrée de l’interface utilisateur sont accessibles à l’aide du clavier.

* La couleur et le contraste de certains éléments de l’interface utilisateur ont été mis à jour afin que les utilisateurs disposant d’une vision limitée ou qui ne perçoivent pas les couleurs puissent distinguer ces éléments de l’interface utilisateur. Par exemple, la couleur des icônes d’évaluation des étoiles (par exemple, dans la section [!UICONTROL Évaluation] de l’onglet [!UICONTROL Avancé] de l’élément [!UICONTROL Propriétés] ou dans la vue de carte) est modifiée pour un contraste approprié.

   ![Icônes de classement avec contraste amélioré](assets/star-rating-icons.png)

#### Amélioration de la gestion des exceptions (6.5.5.0) {#exception-handling}

[!DNL Assets] le flux de l’interface utilisateur a une meilleure gestion des exceptions. Si un fichier n’a pas de type pour sa dimension, l’exception observée est enregistrée dans les fichiers journaux.

#### Prise en charge des ressources 3D dans [!DNL Dynamic Media] (6.5.5.0) {#support-for-3d}

La prise en charge des images 3D dans [!DNL Dynamic Media] permet aux clients de publier et d&#39;ajouter du contenu 3D aux pages Web et aux applications. Le soutien inclut :

* Publiez des formats de fichier 3D courants et générez une URL de fichier qui peut être utilisée dans des pages Web et d’autres applications.

* Lecteur Web 3D optimisé par [!DNL Adobe Dimension] pour la vue interactive des ressources 3D publiées.

* Publiez et vue des ressources 3D communes sur des pages [!DNL Experience Manager Sites] à l’aide du composant WCM [!DNL Sites].

#### Configurer [!DNL Experience Manager Assets] avec [!DNL Brand Portal] (6.5.4.0) {#configure-assets-bp}

Le canal d&#39;autorisation entre [!DNL Experience Manager Assets] et [!DNL Brand Portal] est modifié. Auparavant, [!DNL Brand Portal] était configuré dans l’interface utilisateur classique via la passerelle OAuth héritée, qui utilise l’échange de jetons JWT pour obtenir un Jeton d&#39;accès IMS pour l’autorisation. [!DNL Experience Manager Assets] est maintenant configuré avec  [!DNL Brand Portal] through  [!DNL Adobe I/O], qui achète un jeton IMS pour l&#39;autorisation de votre  [!DNL Brand Portal] client.

Les étapes de configuration de [!DNL Experience Manager Assets] avec [!DNL Brand Portal] diffèrent selon votre version [!DNL Experience Manager] et selon que vous configurez pour la première fois ou mettez à niveau les configurations existantes. Voir [Configuration des ressources du Experience Manager avec le portail de marque](https://docs.adobe.com/content/help/fr-FR/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html) pour plus d’informations.

#### Améliorations de l’accessibilité (6.5.4.0) {#accessibility-enhancements}

[!DNL Experience Manager Assets] comprend les améliorations d’accessibilité suivantes :

* Les touches fléchées du clavier permettent de déplacer et de faire défiler des zones dans les images agrandies. Pour plus d’informations, voir [Actifs de prévisualisation utilisant les touches du clavier uniquement](../assets/manage-assets.md#previewing-assets).

* Les cases à cocher d’état mixte (dans lesquelles, à moins que vous ne sélectionniez tous les prédicats imbriqués, les cases de premier niveau ne sont pas sélectionnées et sont enfoncées) dans le panneau Filtres sont lisibles par les lecteurs d’écran.

* Les contraintes de format de date et d’heure sont fournies dans les libellés de champs des champs de date, afin de permettre aux utilisateurs de saisir la date dans le format correct à l’aide du clavier.
Par exemple, `On Time (MM-DD-YYYY HH:mm)`. Ici MM est le mois en format à deux chiffres, AAAA est l&#39;année, JJ est le jour en format à deux chiffres, HH est l&#39;heure en format militaire à 24 heures et mm est la minute.

* Les lecteurs d’écran annoncent l’option de suppression des balises sélectionnées (`X` symbole) et le nombre de balises sélectionnées.

#### Colonne triable pour la date de création des actifs dans la vue de liste (6.5.3.0) {#sortable-date-created-column}

Une nouvelle colonne pouvant être triée pour la date de création des ressources est ajoutée dans la vue de liste DAM et dans les résultats de la recherche de ressources dans la vue de liste.

![Colonne triable pour la date créée](assets/asset-created-date.png)

#### Recherche visuelle pour [!DNL Adobe Experience Manager Assets] (6.5.2.0) {#visual-search}

[!DNL Assets] les utilisateurs peuvent rechercher des images visuellement similaires. Le Experience Manager affiche les images balisées intelligentes du référentiel DAM qui sont similaires à une image sélectionnée par l’utilisateur. Voir [Recherche visuelle](../assets/search-assets.md).

### Dynamic Media {#dynamic-media-previous-service-packs}

#### Invalider le contenu mis en cache du CDN (6.5.6.0) {#invalidate-cdn-cached-content}

Vous pouvez désormais utiliser l’interface utilisateur [!DNL Dynamic Media] pour invalider le contenu mis en cache du réseau de Diffusion de contenu (CDN). Par conséquent, les ressources mises à jour sont disponibles instantanément au lieu d’attendre l’expiration du cache. Vous pouvez invalider le CDN en procédant comme suit :

* Création d’un modèle d’invalidation CDN : Sélection de fichiers et d’URL associées à des modèles de formulaire

* Sélection de fichiers et de paramètres prédéfinis associés par le biais du sélecteur de fichiers

* Ajouter des URL de fichier complètes

#### Publication sélective d’actifs vers [!DNL Experience Manager] et [!DNL Dynamic Media] (6.5.6.0) {#selective-publishing}

Vous pouvez désormais choisir de publier ou d’annuler la publication de fichiers dans [!DNL Experience Manager] ou [!DNL Dynamic Media] à l’aide de l’assistant [!UICONTROL Publication rapide] ou [!UICONTROL Gérer la publication]. Vous pouvez également définir le mode `Publish` ou `Unpublish` au niveau du dossier.

#### Smart Imaging pour Dynamic Media {#smart-imaging}

L’imagerie intelligente utilise les caractéristiques d’affichage uniques de chaque utilisateur pour fournir automatiquement les images appropriées optimisées pour leur expérience, ce qui se traduit par de meilleures performances et un meilleur engagement. L’imagerie dynamique fonctionne avec vos paramètres d’image prédéfinis et utilise des informations à la dernière milliseconde de la diffusion pour réduire davantage encore la taille du fichier d’image en fonction de la vitesse de connexion du réseau et du navigateur. Voir [Smart Imaging](../assets/imaging-faq.md).

#### Recadrage intelligent dans les profils vidéo pour Dynamic Media (6.5.3.0) {#smart-crop-video}

Le recadrage intelligent pour la vidéo (une fonctionnalité en option dans les profils vidéo) est un outil qui utilise la puissance de l’intelligence artificielle d’Adobe Sensei pour détecter et rogner automatiquement le point focal dans toute vidéo adaptative ou progressive que vous avez chargée, quelle que soit sa taille. Voir [A propos de l’utilisation du recadrage intelligent dans les profils vidéo](../assets/video-profiles.md).

### Experience Manager Forms {#aem-forms-previous-service-packs}

#### Préremplir un formulaire adaptatif au client (6.5.6.0) {#prefill-merge-data-at-client}

Lorsque vous préremplissez un formulaire adaptatif, le serveur [!DNL Experience Manager Forms] fusionne les données avec un formulaire adaptatif et vous transmet le formulaire rempli. Par défaut, l’action de fusion des données a lieu sur le serveur.
Vous pouvez maintenant configurer le serveur [!DNL Experience Manager Forms] pour [exécuter l&#39;action de fusion des données sur le client](../../help/forms/using/prepopulate-adaptive-form-fields.md) au lieu du serveur. Il réduit considérablement le temps nécessaire pour préremplir et générer les formulaires adaptatifs.

#### Intégration du modèle de données de formulaire avec les API RESTful sur un serveur avec une implémentation SSL bidirectionnelle (6.5.6.0) {#fdm-integration-rest-apis-two-way-ssl}

[!DNL Experience Manager Forms] Le modèle de données de formulaire peut désormais  [s’intégrer aux API RESTful sur un serveur sur lequel un protocole SSL bidirectionnel est implémenté](../../help/forms/using/configure-data-sources.md).

#### Prise en charge Ajoutée des balises de texte [!DNL Adobe Sign] dans Automated forms conversion Service (6.5.6.0) {#sign-integration-acroform-afcs}

Si un AcroForm contient des balises de texte [!DNL Adobe Sign], ces champs sont maintenant reconnus et représentés comme champs [!DNL Adobe Sign] dans le formulaire adaptatif converti à l’aide de [!DNL Automated Forms Conversion service]. Un signataire peut remplir ces champs lors de la signature du formulaire adaptatif.

#### Prise en charge de la conversion des PDF forms colorés en formulaires adaptatifs (6.5.6.0) {#colored-PDF-forms}

Vous pouvez utiliser [!DNL Automated Forms Conversion service] pour convertir des PDF forms colorés en formulaires adaptatifs.

#### Prise en charge des protocoles SMB 2 et SMB 3 (6.5.6.0) {#smb-support}

[!DNL Experience Manager Forms] prend désormais en charge les protocoles SMB 2 et SMB 3.

#### Mise en cache améliorée pour les pages de formulaires adaptatifs converties (6.5.6.0) {#enhanced-caching-translated-adaptive-forms}

Vous pouvez désormais spécifier un paramètre régional [comme sélecteur dans l’URL du formulaire adaptatif au lieu d’un argument dans l’URL du formulaire adaptatif](../../help/forms/using/supporting-new-language-localization.md). Il permet de mettre en cache les formulaires adaptatifs convertis sur [!DNL Experience Manager Dispatcher]. La mise en cache des formulaires adaptatifs traduits n’était pas possible dans les versions précédentes. Pour plus d’informations sur la configuration de la mise en cache pour l’utilisation des paramètres régionaux en tant que sélecteur dans l’URL du formulaire adaptatif, voir [Configuration du cache de formulaire adaptatif à l’adresse dispatcher](../../help/forms/using/configure-adaptive-forms-cache.md).

#### Enregistrez la sortie du service de modèle de données de formulaire dans une variable (6.5.6.0) {#save-fdm-service-to-variable}

Le modèle de données de formulaire vous permet d’enregistrer la sortie d’un service de modèle de données de formulaire dans une variable. [!DNL Experience Manager Forms] mappe désormais automatiquement le type du service de modèle de données de formulaire au type de variable.

#### Joindre plusieurs fichiers pour le composant Pièce jointe (6.5.6.0) {#attach-multiple-files}

Vous pouvez désormais [joindre plusieurs fichiers](../../help/forms/using/introduction-forms-authoring.md) au composant [!UICONTROL Pièce jointe] des formulaires adaptatifs.

#### Personnaliser les colonnes de la boîte de réception Adobe Experience Manager (6.5.5.0) {#customize-aem-inbox-columns}

Vous pouvez personnaliser une boîte de réception [!DNL Experience Manager] pour modifier le titre par défaut d’une colonne, réorganiser la position d’une colonne et afficher d’autres colonnes en fonction des données d’un processus. Les membres du groupe `administrators` ou `workflow-administrators` peuvent personnaliser les colonnes. Pour plus d’informations, voir [Contrôle d’administration](../sites-authoring/inbox.md#inbox-admin-control).

![Personnalisation des colonnes de la boîte de réception des Experience Manager](assets/customize-columns.gif)

#### Enregistrer les communications interactives en tant que brouillon (6.5.5.0) {#save-as-draft}

Vous pouvez utiliser l’interface utilisateur de l’agent pour enregistrer un ou plusieurs brouillons pour chaque communication interactive et récupérer le brouillon ultérieurement pour continuer à travailler dessus. Vous pouvez spécifier un nom différent pour chaque brouillon afin de l’identifier. Pour plus d&#39;informations, voir [Enregistrer les communications interactives en tant que brouillon](../forms/using/prepare-send-interactive-communication.md#save-as-draft).

![Enregistrer en tant que brouillon](assets/save-as-draft.gif)

#### [!DNL Oracle WebLogic] prise en charge du serveur d’applications (6.5.5.0)  {#weblogic-support}

Adobe Experience Manager Forms a ajouté la prise en charge de [!DNL Oracle WebLogic 12] pour Adobe Experience Manager Forms on JEE. Vous pouvez effectuer une mise à niveau à partir d’une version précédente ou configurer un nouveau serveur Forms on JEE Experience Manager 6.5 sur [!DNL Oracle WebLogic] 12.2.1.4 et versions ultérieures. Plus tard correspond aux changements mineurs de version, où x dans 12.2.1.x est remplacé par un numéro de version.

#### Améliorations de l&#39;accessibilité (6.5.5.0) {#accessibility-improvements}

Adobe Experience Manager Forms comprend les améliorations d’accessibilité suivantes :

* Lorsqu’un utilisateur prévisualisation un formulaire adaptatif en tant que formulaire HTML, le champ [!UICONTROL Signature tactile] conserve la cible d’action.

* Les messages d’erreur affichés lors de l’envoi d’un formulaire adaptatif contiennent désormais l’attribut `aria-describedBy`. L’attribut est attaché aux champs référencés dans le message d’erreur. L&#39;attribut `aria-describedby` indique les ID des éléments qui décrivent l&#39;objet. Il permet d’établir une relation entre les widgets ou les groupes et le texte qui les décrit.

* Si un formulaire adaptatif comporte certains champs obligatoires, l’attribut obligatoire est défini sur `True` pour ces champs dans le schéma d’accessibilité ARIA.

#### Authentification par certificat X-509 pour les services Web SOAP dans le modèle de données de formulaire (6.5.5.0) {#x509-based-authentication-soap}

Le modèle de données de formulaire prend désormais en charge l’authentification par certificat X-509 lors de l’utilisation des services Web SOAP en tant que source de données. Pour plus d’informations, voir [Configuration des services Web SOAP](../forms/using/configure-data-sources.md#configure-soap-web-services).

#### Autres améliorations clés (6.5.5.0) {#other-improvements}

* La sécurité Document de la version 6.5 de Experience Manager Forms on JEE est désormais basée sur [!DNL Apache Struts 2].

* Prise en charge Ajoutée de [!DNL Oracle Real Applications Cluster (RAC) 19c].

#### Générer une sortie imprimable dans les workflows Forms Experience Manager (6.5.4.0) {#generate-printable-output}

L’étape de flux de travail Générer une sortie imprimable vous permet d’intégrer un fichier de modèle source à un fichier de données. Cette intégration vous permet d’imprimer ou d’enregistrer différentes copies du fichier de modèle. L’étape génère une sortie PCL, PostScript, ZPL, IPL, TPCL ou DPL. Pour plus d’informations sur cette fonctionnalité, voir [Processus centré sur Forms sur OSGi - Guide de référence des étapes](../forms/using/aem-forms-workflow-step-reference.md).

![Générer une sortie imprimable](assets/generate-print-output-step.gif)

#### Prise en charge de plusieurs colonnes pour les formulaires adaptatifs et les communications interactives en mode Mise en page (6.5.4.0) {#multi-column-adaptive-forms}

Vous pouvez désormais définir le nombre de colonnes pour un panneau dans les formulaires adaptatifs et les communications interactives. Passez en mode de mise en page pour utiliser la nouvelle option multi-colonne. Pour plus d’informations, voir [Utilisation du mode Mise en page pour redimensionner les composants](../forms/using/resize-using-layout-mode.md).

![Mise en page multi-colonnes](assets/multi-column-layout.gif)

#### Personnalisations de la boîte de réception Experience Manager (6.5.4.0) {#aem-inbox}

La nouvelle option de contrôle d’administration permet aux administrateurs d’effectuer les opérations suivantes :

* Personnalisez le texte et le logo de l’en-tête.

* Permet de contrôler l’affichage des liens de navigation disponibles dans l’en-tête.

L’option Contrôle d’administration n’est visible que pour les membres du groupe `administrators` ou `workflow-administrators`. Pour plus d’informations sur cette fonctionnalité, voir [Votre boîte de réception](../sites-authoring/inbox.md).

#### Prise en charge du texte enrichi dans les formulaires HTML5 (6.5.4.0) {#rich-text-support}

Convertissez un champ de texte d’un formulaire XFA en champ de texte enrichi dans un formulaire HTML5. Pour plus d’informations, voir [Conception de modèles de formulaire pour les formulaires HTML5](../forms/using/designing-form-template.md).

#### Améliorations de l’accessibilité (6.5.4.0) {#forms-accessibility-enhancements-6540}

Experience Manager Forms inclut les améliorations d’accessibilité suivantes :

* Les lecteurs d’écran annoncent correctement les cases à cocher, les liens, le sélecteur de date et les champs de saisie de date dans un formulaire adaptatif.

* Chaque page d’un formulaire adaptatif comprend désormais un titre et une étiquette de repère principale.

#### Partager et demander l&#39;accès aux éléments de boîte de réception d&#39;un utilisateur Forms Experience Manager (6.5.3.0) {#share-request-access}

Vous pouvez partager vos éléments de boîte de réception avec un autre utilisateur. Une fois qu&#39;un autre utilisateur a accès à vos éléments de boîte de réception, il peut demander et prendre les mesures appropriées sur les éléments partagés. De même, vous pouvez demander l’accès aux éléments de boîte de réception à d’autres utilisateurs. Voir [Partager et demander l&#39;accès aux éléments de boîte de réception d&#39;un utilisateur](../forms/using/configure-shared-queues-osgi.md).

#### Configurez les paramètres d’absence du bureau pour les éléments de boîte de réception d’un utilisateur Forms Experience Manager (6.5.3.0) {#configure-out-of-office}

Si vous prévoyez d’être absent du bureau, vous pouvez indiquer ce qui se passe pour les éléments qui vous sont affectés pour cette période.
Vous pouvez spécifier une date et une heure de début, ainsi qu’une date et une heure de fin, pour l’application de vos paramètres d’absence du bureau. Vous pouvez définir une personne par défaut à laquelle tous vos éléments sont envoyés. Voir [Configuration des paramètres d’absence du bureau](../forms/using/configure-out-of-office-settings.md).

#### Générer plusieurs communications interactives à l’aide de l’API Batch pour le Forms Experience Manager (6.5.3.0) {#generate-multiple-ic}

Vous pouvez utiliser l’API de traitement par lots pour produire plusieurs communications interactives à partir d’un modèle. Le modèle est une communication interactive sans données. L’API de traitement par lots combine les données avec un modèle pour produire une communication interactive. L&#39;API est utile pour la production de masse de communications interactives. Par exemple, factures de téléphone, relevés de carte de crédit pour plusieurs clients. Voir [Générer plusieurs communications interactives à l’aide de l’API de lot](../forms/using/generate-multiple-interactive-communication-using-batch-api.md).

## Principales versions depuis Adobe Experience Manager 6.5 SP6 {#key-releases-since-last-sp}

Entre le 3 septembre 2020 et le 26 novembre 2020, Adobe a publié ce qui suit, en plus des Service Packs et des Fix Packs cumulatifs :

* [!DNL Adobe Experience Manager] en tant que Cloud Service  [2020.9.0](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-2020-9-0.html?lang=en#release-notes) et  [2020.10.0](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-2020-10-0.html?lang=en#release-notes).

* [[!DNL Experience Manager] application de bureau 2.0 (2.0.3.2)](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html).

* [Site de référence WKND - 0.0.6](https://github.com/adobe/aem-guides-wknd/releases/tag/aem-guides-wknd-0.0.6)

* [Experience Manager Screens : Feature Pack 202011](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/release-notes/release-notes-fp-202011.html)

* [Adobe Asset Link v2.2](https://helpx.adobe.com/fr/enterprise/admin-guide.html/enterprise/using/adobe-asset-link.ug.html)

>[!MORELIKETHIS]
>
>* [[!DNL Adobe Experience Manager] 6.5 Documentation](../user-guide/home.md)
>* [Notes de mise à jour générales pour [!DNL Adobe Experience Manager]  la version 6.5](release-notes.md)
>* [Notes de mise à jour du Service Pack pour [!DNL Adobe Experience Manager]  la version 6.5](sp-release-notes.md)

