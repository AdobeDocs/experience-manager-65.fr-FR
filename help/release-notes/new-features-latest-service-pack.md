---
title: Nouveautés de  [!DNL Experience Manager] 6.5 Service Pack 8
description: Nouveautés de  [!DNL Experience Manager] 6.5 Service Pack 8
contentOwner: AK
mini-toc-levels: 1
exl-id: 32470e6e-8a66-4670-82da-2259f6e001c3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '3041'
ht-degree: 7%

---

# Nouveautés de [!DNL Adobe Experience Manager] 6.5 Service Pack 8 {#aem-whats-new-service-pack}

![Whats-new](assets/whatsnew.jpeg)

[!DNL Adobe Experience Manager] 6.5 Les Service Packs proposent, à intervalles trimestriels, de nouvelles fonctionnalités, des améliorations demandées par les clients, ainsi que des améliorations en termes de performances, de stabilité et de sécurité. La disponibilité trimestrielle facilite l’accès et l’adoption de nouvelles fonctionnalités et innovations.

Cet article met en évidence les fonctionnalités incluses dans le dernier Service Pack, [les fonctionnalités clés incluses dans les Service Packs version 6.5 précédente](#key-features-previous-service-packs), ainsi que les versions [clés depuis la dernière version du Service Pack](#key-releases-since-last-sp).

## [!DNL Adobe Experience Manager Sites] {#aem-sites}

### Tri des pages Live Copy disponibles pour le déploiement {#sort-livecopy-pages}

Vous pouvez désormais trier les pages Live Copy disponibles pour le déploiement à l’aide des propriétés [!UICONTROL Name], [!UICONTROL Date de dernière modification] et [!UICONTROL Date du dernier déploiement]. La [!UICONTROL date du dernier déploiement] d’une page est une nouvelle propriété introduite dans cette version.

## [!DNL Adobe Experience Manager Assets] {#aem-assets}

* Lors de l’utilisation de la fonction [Ressources connectées](/help/assets/use-assets-across-connected-assets-instances.md), vous pouvez désormais afficher la liste de toutes les pages [!DNL Sites] qui utilisent la ressource. Ces références à une ressource sont disponibles dans la page [!UICONTROL Propriétés] d’une ressource. Cela permet aux administrateurs, aux spécialistes du marketing et aux bibliothécaires d’avoir une vue complète de l’utilisation des ressources, ce qui permet un meilleur suivi, une meilleure gestion et une meilleure cohérence de la marque.

* Lors de la suppression d’une ressource référencée dans une page web, [!DNL Experience Manager] affiche un avertissement. Vous pouvez forcer la suppression d’une ressource référencée ou vérifier et modifier les références affichées dans la page [!DNL Properties] de la ressource. Cliquer sur les références ouvre les pages [!DNL Sites] locales et distantes.

## [!DNL Adobe Experience Manager Forms] {#aem-forms}

>[!NOTE]
>
>Le module complémentaire de [!DNL Experience Manager Forms] est rendu disponible une semaine après la publication du Service Pack [!DNL Experience Manager] programmée.

### Afficher ou masquer le composant CAPTCHA dans un formulaire adaptatif basé sur des règles {#show-hide-captcha}

Vous pouvez désormais valider CAPTCHA lors de l’envoi du formulaire adaptatif ou lors de l’action de l’utilisateur. Vous pouvez également ajouter des conditions pour valider CAPTCHA sur une action utilisateur et afficher ou masquer le composant CAPTCHA dans un formulaire adaptatif basé sur des règles.

### Ajout de services CAPTCHA personnalisés {#add-custom-captcha-services}

[!DNL Experience Manager Forms] fournit une prise en charge prête à l’emploi pour utiliser Google reCAPTCHA (une licence distincte des API reCAPTCHA de Google est requise) en tant que service de validation CAPTCHA. Vous pouvez également utiliser un service CAPTCHA personnalisé pour valider les CAPTCHA.

### Autres améliorations {#other-enhancements-forms-6580}

* Amélioration de l’accessibilité du composant [!DNL Experience Manager Forms] Sélecteur de date.

* Ajout de la prise en charge de la génération d’une communication interactive au format PCL à l’aide de l’API PrintChannel.

* Lors d’une conversion PDFG, vous pouvez désormais activer ou désactiver les modifications de registre [!DNL Experience Manager Forms] pour la génération de signets personnalisés.

## Fonctionnalités clés des Service Packs version [!DNL Experience Manager] 6.5 précédente {#key-features-previous-service-packs}

### [!DNL Experience Manager Sites] {#aem-sites-previous-service-packs}

#### Disponibilité des déplacements de page et des déploiements MSM en tant qu’opérations asynchrones (6.5.7.0) {#page-moves-msm-asynchronous}

Vous pouvez désormais effectuer les déplacements de page et les déploiements MSM sous la forme d’opérations asynchrones afin de réduire leur impact sur les performances d’exécution. Vous pouvez planifier les opérations pour une exécution immédiate ou ultérieure. L’état des tâches et des étapes de processus associées s’affiche dans une console, ce qui s’avère utile pour surveiller les déploiements MSM à grande échelle.

#### Disponibilité de l’opération de déplacement de page en mode asynchrone (6.5.6.0) {#page-move-asynchronous}

L’opération Déplacement de page est désormais disponible en mode asynchrone. Outre l’exécution immédiate, vous pouvez également planifier l’opération Déplacer la page pour une exécution ultérieure.

#### Améliorations de l’accessibilité (6.5.5.0) {#accessibility-sites}

* Amélioration des rapports d’erreurs en ajoutant des informations textuelles.

* Amélioration de la mise au point de l’interface utilisateur lors de la navigation au clavier.

* Amélioration du rapport de contraste pour divers éléments de l’interface utilisateur.

* Amélioration de la cohérence des attributs alt pour les images de page.

* Amélioration de la cohérence des étiquettes ARIA (Accessible Rich Internet Applications).

* Amélioration des fonctionnalités NVDA (Non Visual Desktop Access).

* Amélioration de la prise en charge des lecteurs d’écran.

#### Autres améliorations clés (6.5.5.0) {#other-enhancements-sites}

* L’accès anonyme à CRXDE Lite n’est pas autorisé pour améliorer la sécurité. Les utilisateurs sont redirigés vers l’écran de connexion. Voir [Développement avec CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

* Lorsque vous copiez ou collez une arborescence de page, vous avez désormais la possibilité de coller la page racine ou de coller la page racine avec les sous-pages de l’arborescence.

* [!DNL Adobe Experience Manager Experience Fragments] Les  [!DNL Adobe Target] espaces de travail exportés s’affichent désormais sous la forme de types d’offres et de sources d’offres uniques dans  [!DNL Target].

* Multi Site Manager : le déclencheur de publication supprime désormais un composant de la page publiée si un composant est supprimé de la page source.

* Multi Site Manager : lorsque le nom d’un composant local dans une [!UICONTROL Live Copy] est identique au nom d’un composant dans le plan directeur et que le composant est déployé à partir du plan directeur, le terme `_msm_moved` est maintenant ajouté au nom du composant local.

#### Améliorations du système de style (6.5.4.0) {#style-system-enhancements}

Vous pouvez désormais sélectionner des styles dans la boîte de dialogue du composant à l’aide du système de style amélioré.

#### Améliorations des performances dans divers domaines (6.5.4.0) {#performance-improvements}

* Réduction du temps de chargement et d’initialisation de ContextHub dans un site (`contexthub.kernel.js`). Cela entraîne un chargement de page plus rapide lors d’une visite du site.

* Réduction du temps d’actualisation d’une page après avoir fait glisser [!DNL Experience Fragments] vers [!DNL Sites] l’éditeur de page.

* Réduction du temps de chargement des entrées sur une page [!DNL Sites] avec plus de 200 Live Copies dans **[!UICONTROL Aperçu de la Live Copy]**.

* Amélioration de la gestion des URL incomplètes ou non valides. Ces URL peuvent ralentir l’éditeur de modèles.

### [!DNL Adobe Experience Manager Assets] {#aem-assets-previous-service-packs}

* [!DNL Assets] et  [!DNL Dynamic Media] fournissent plusieurs améliorations de l’accessibilité. Les améliorations ont été apportées à la navigation au clavier, à l’utilisation des lecteurs d’écran et à des améliorations similaires pour permettre l’utilisation des technologies d’assistance (AT). Voir [[!DNL Assets] améliorations](/help/release-notes/sp-release-notes.md#assets-6570) et [[!DNL Dynamic Media] améliorations](/help/release-notes/sp-release-notes.md#dynamic-media-6570) (6.5.7.0)

* Les utilisateurs peuvent trier les ressources numériques en mode Carte et Colonnes (6.5.7.0).

#### Améliorations de l’accessibilité (6.5.6.0) {#accessibility-assets-6560}

* **Amélioration de la mise au point de l’interface utilisateur lors de la navigation** clavier, par exemple en mettant l’accent sur :

   * `x` dans la  [!UICONTROL boîte de dialogue ] Aperçu de version d’une ressource dans la  [!UICONTROL chronologie].

   * Options d’interface utilisateur pratiques.

   * Champ Courrier électronique dans la boîte de dialogue [!UICONTROL Partager le lien] et champ pour ajouter un groupe d’utilisateurs fermé dans l’onglet [!UICONTROL Autorisation] du dossier [!UICONTROL Propriétés].

* **Amélioration des fonctionnalités à l’aide des touches de clavier**

   Les utilisateurs peuvent utiliser les touches du clavier pour faire glisser des commandes dans l’éditeur de formulaire de schéma de métadonnées en mode de navigation du lecteur d’écran.

* **Amélioration de la convivialité pour les utilisateurs** de lecteurs d’écran, grâce aux éléments suivants :

   * Les lecteurs d’écran annoncent l’objectif des lecteurs vidéo et audio.

   * Les lecteurs d’écran indiquent l’objectif des options de l’interface utilisateur pour supprimer les balises sélectionnées à l’aide de la [!UICONTROL boîte de dialogue de sélection des balises] sur la ressource [!UICONTROL Propriétés].

   * Les lecteurs d’écran annoncent les en-têtes de ligne et les éléments de ligne des tableaux, de sorte que les utilisateurs sachent quelles entrées appartiennent à la même ligne.

   * Titre descriptif et significatif de la page de recherche.

   * Les lecteurs d’écran annoncent les options du panneau des filtres de recherche sous forme d’accordéons extensibles.

#### Autres améliorations dans [!DNL Assets] (6.5.6.0) {#other-enhancements-assets-6560}

* Les groupes d’utilisateurs associés aux dossiers (privés et non privés) sont désormais supprimés du référentiel lors de la [suppression de ces dossiers](/help/assets/private-folder.md#delete-private-folder). Toutefois, les groupes d’utilisateurs redondants, orphelins, inutilisés et générés automatiquement existants peuvent être supprimés du référentiel à l’aide de JMX.

#### Améliorations de l’accessibilité dans [!DNL Assets] (6.5.5.0) {#assets-accessibility}

[!DNL Experience Manager Assets] est désormais plus accessible, conformément aux directives WCAG (Web Content Accessibility Guidelines). L’accessibilité a été améliorée en raison des améliorations suivantes :

* De nombreux éléments, commandes, pages et boîtes de dialogue de l’interface utilisateur sont compatibles avec les lecteurs d’écran.

* De nombreux éléments, contrôles et champs de formulaire de saisie de l’interface utilisateur sont accessibles à l’aide du clavier.

* La couleur et le contraste de certains éléments de l’interface utilisateur ont été mis à jour afin que les utilisateurs disposant d’une vision limitée ou qui ne perçoivent pas les couleurs puissent distinguer ces éléments de l’interface utilisateur. Par exemple, la couleur des icônes d’évaluation par étoiles (comme dans la section [!UICONTROL Évaluation] de l’onglet [!UICONTROL Avancé] dans la ressource [!UICONTROL Propriétés] ou en mode Carte) est modifiée pour un contraste approprié.

   ![Icônes de notation avec meilleur contraste](assets/star-rating-icons.png)

#### Amélioration de la gestion des exceptions (6.5.5.0) {#exception-handling}

[!DNL Assets] le flux de l’interface utilisateur a une meilleure gestion des exceptions. Si une ressource n’a pas de type pour sa dimension, l’exception observée est enregistrée dans les fichiers journaux.

#### Prise en charge des ressources 3D dans [!DNL Dynamic Media] (6.5.5.0) {#support-for-3d}

La prise en charge des images 3D dans [!DNL Dynamic Media] permet aux clients de publier et d’ajouter du contenu 3D aux pages web et aux applications. La prise en charge inclut :

* Publiez des formats de ressource 3D courants et générez une URL de ressource qui peut être utilisée dans des pages web et d’autres applications.

* Visionneuse web 3D optimisée par [!DNL Adobe Dimension] pour afficher de manière interactive les ressources 3D publiées.

* Publiez et affichez des ressources 3D courantes sur les pages [!DNL Experience Manager Sites] à l’aide du composant de gestion de contenu web [!DNL Sites].

#### Configurer [!DNL Experience Manager Assets] avec [!DNL Brand Portal] (6.5.4.0) {#configure-assets-bp}

Le canal d’autorisation entre [!DNL Experience Manager Assets] et [!DNL Brand Portal] a été modifié. Auparavant, [!DNL Brand Portal] était configuré dans l’interface utilisateur classique via la passerelle OAuth héritée, qui utilise l’échange de jetons JWT pour obtenir un jeton d’accès IMS en vue de l’autorisation. [!DNL Experience Manager Assets] est maintenant configuré avec  [!DNL Brand Portal] par  [!DNL Adobe I/O], qui fournit un jeton IMS pour autoriser votre  [!DNL Brand Portal] client.

Les étapes de configuration de [!DNL Experience Manager Assets] avec [!DNL Brand Portal] sont différentes selon votre version [!DNL Experience Manager] et selon que vous effectuez une configuration pour la première fois ou une mise à niveau des configurations existantes. Pour plus d’informations, voir [Configuration de ressources Experience Manager avec Brand Portal](https://docs.adobe.com/content/help/fr-FR/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html) .

#### Améliorations de l’accessibilité (6.5.4.0) {#accessibility-enhancements}

[!DNL Experience Manager Assets] comprend les améliorations d’accessibilité suivantes :

* Vous pouvez utiliser les touches fléchées du clavier pour déplacer et déplacer des zones dans les images agrandies. Pour plus d’informations, voir [aperçu des ressources à l’aide des touches du clavier uniquement](../assets/manage-assets.md#previewing-assets).

* Les cases à cocher d’état mixte (dans lesquelles, sauf si vous sélectionnez tous les prédicats imbriqués, les cases de premier niveau ne sont pas sélectionnées et sont enfoncées) du panneau Filtres sont lisibles par les lecteurs d’écran.

* Les contraintes de format de date et d’heure sont fournies dans les libellés de champ des champs de date, afin de permettre aux utilisateurs de saisir la date dans le bon format à l’aide du clavier.
Par exemple, `On Time (MM-DD-YYYY HH:mm)`. Ici MM est un mois à deux chiffres, AAAA est l’année, JJ est un jour à deux chiffres, HH est une heure au format militaire 24 heures et mm est une minute.

* Les lecteurs d’écran indiquent l’option permettant de supprimer les balises sélectionnées (`X` symbole ) et le nombre de balises sélectionnées.

#### Colonne Triable pour la date de création des ressources en mode Liste (6.5.3.0) {#sortable-date-created-column}

Une nouvelle colonne pouvant être triée pour la date de création des ressources est ajoutée en mode Liste de la gestion des actifs numériques et dans les résultats de recherche de ressources en mode Liste.

![Colonne Triable pour la date de création](assets/asset-created-date.png)

#### Recherche visuelle pour [!DNL Adobe Experience Manager Assets] (6.5.2.0) {#visual-search}

[!DNL Assets] les utilisateurs peuvent rechercher des images visuellement similaires. Experience Manager affiche les images balisées intelligentes du référentiel DAM qui sont similaires à une image sélectionnée par l’utilisateur. Voir [Recherche visuelle](../assets/search-assets.md).

### Dynamic Media {#dynamic-media-previous-service-packs}

#### Invalider le contenu CDN mis en cache (6.5.6.0) {#invalidate-cdn-cached-content}

Vous pouvez désormais utiliser l’interface utilisateur [!DNL Dynamic Media] pour invalider le contenu mis en cache du réseau de diffusion de contenu (CDN). Par conséquent, les ressources mises à jour sont disponibles instantanément au lieu d’attendre que le cache arrive à expiration. Vous pouvez invalider le réseau de diffusion de contenu en procédant comme suit :

* Création d’un modèle d’invalidation du réseau CDN : Sélection de ressources et d’URL basées sur des modèles associés à un formulaire

* Sélection de ressources et de paramètres prédéfinis associés via le sélecteur de ressources

* Ajout d’URL de ressource complètes

#### Publication sélective de ressources dans [!DNL Experience Manager] et [!DNL Dynamic Media] (6.5.6.0) {#selective-publishing}

Vous pouvez désormais choisir de publier ou d’annuler la publication de ressources de manière sélective sur [!DNL Experience Manager] ou [!DNL Dynamic Media] à l’aide de l’assistant [!UICONTROL Publication rapide] ou [!UICONTROL Gérer la publication] . Vous pouvez également définir le mode `Publish` ou `Unpublish` au niveau du dossier.

#### Imagerie dynamique pour Dynamic Media {#smart-imaging}

L’imagerie dynamique utilise les caractéristiques de visualisation uniques de chaque utilisateur pour diffuser automatiquement les images appropriées optimisées pour leur expérience, ce qui se traduit par de meilleures performances et un meilleur engagement. L’imagerie dynamique fonctionne avec vos paramètres d’image prédéfinis et utilise des informations à la dernière milliseconde de la diffusion pour réduire davantage encore la taille du fichier d’image en fonction de la vitesse de connexion du réseau et du navigateur. Voir la section [Imagerie dynamique](../assets/imaging-faq.md).

#### Recadrage intelligent dans les profils vidéo pour Dynamic Media (6.5.3.0) {#smart-crop-video}

Le recadrage intelligent pour la vidéo (une fonctionnalité en option dans les profils vidéo) est un outil qui utilise la puissance de l’intelligence artificielle d’Adobe Sensei pour détecter et rogner automatiquement le point focal dans toute vidéo adaptative ou progressive que vous avez chargée, quelle que soit sa taille. Voir [À propos de l’utilisation du recadrage intelligent dans les profils vidéo](../assets/video-profiles.md).

### Experience Manager Forms {#aem-forms-previous-service-packs}

#### Améliorations des performances (6.5.7.0) {#performance-improvements-forms}

[!DNL Experience Manager] 6.5 Service Pack 7 Forms améliore les performances pour :

* Validation des valeurs de champ sur le serveur lorsque vous envoyez un formulaire adaptatif.

* Conversion d’un formulaire PDF en formulaire adaptatif à l’aide de [!DNL Automated Forms Conversion service].

#### Prise en charge des groupes de disponibilité Always On pour Microsoft SQL Server 2016 pour la haute disponibilité (6.5.7.0) {#always-on-availability-groups}

[!DNL Experience Manager Forms] prend désormais en charge les groupes de disponibilité &quot;Toujours en disponibilité&quot;  [!DNL Microsoft] SQL Server 2016 pour les déploiements OSGi.

#### Configuration du client HTTP du modèle de données de formulaire pour optimiser les performances (6.5.7.0) {#fdm-http-client-config}

[!DNL Experience Manager Forms] le modèle de données de formulaire lors de l’intégration avec les services web RESTful en tant que source de données inclut désormais des configurations de client HTTP pour l’optimisation des performances. Voir [Configuration des sources de données](../../help/forms/using/configure-data-sources.md#fdm-http-client-configuration).

#### Disponibilité de l’option de réinitialisation pour chaque composant en mode Disposition (6.5.7.0) {#reset-option-layout-mode}

Vous pouvez désormais utiliser l’option de réinitialisation pour chaque composant en mode Mise en page d’un formulaire adaptatif. Lorsque vous définissez une mise en page à plusieurs colonnes pour un panneau, vous pouvez utiliser cette fonction pour réinitialiser des composants individuels dans le panneau. Voir [Utiliser le mode de mise en page pour redimensionner les composants](../../help/forms/using/resize-using-layout-mode.md#resize-components).

#### Préremplir un formulaire adaptatif au niveau du client (6.5.6.0) {#prefill-merge-data-at-client}

Lorsque vous préremplissez un formulaire adaptatif, le serveur [!DNL Experience Manager Forms] fusionne les données avec un formulaire adaptatif et vous envoie le formulaire rempli. Par défaut, l’action de fusion des données a lieu sur le serveur.
Vous pouvez maintenant configurer le serveur [!DNL Experience Manager Forms] pour [effectuer l’action de fusion de données sur le client](../../help/forms/using/prepopulate-adaptive-form-fields.md) au lieu du serveur. Cela réduit considérablement le temps nécessaire au préremplissage et au rendu des formulaires adaptatifs.

#### Intégration d’un modèle de données de formulaire avec des API RESTful sur un serveur avec une implémentation SSL bidirectionnelle (6.5.6.0) {#fdm-integration-rest-apis-two-way-ssl}

[!DNL Experience Manager Forms] Le modèle de données de formulaire peut désormais  [s’intégrer aux API RESTful sur un serveur sur lequel un protocole SSL bidirectionnel est implémenté](../../help/forms/using/configure-data-sources.md).

#### Ajout de la prise en charge des [!DNL Adobe Sign] balises de texte dans Automated forms conversion Service (6.5.6.0) {#sign-integration-acroform-afcs}

Si un AcroForm contient des [!DNL Adobe Sign] balises de texte, ces champs sont désormais reconnus et représentés sous la forme de champs [!DNL Adobe Sign] dans le formulaire adaptatif converti à l’aide de [!DNL Automated Forms Conversion service]. Un signataire peut remplir ces champs lors de la signature du formulaire adaptatif.

#### Prise en charge de la conversion de PDF forms colorés en formulaires adaptatifs (6.5.6.0) {#colored-PDF-forms}

Vous pouvez utiliser [!DNL Automated Forms Conversion service] pour convertir des PDF forms colorés en formulaires adaptatifs.

#### Prise en charge des protocoles SMB 2 et SMB 3 (6.5.6.0) {#smb-support}

[!DNL Experience Manager Forms] prend désormais en charge les protocoles SMB 2 et SMB 3.

#### Mise en cache améliorée pour les pages de formulaires adaptatifs convertis (6.5.6.0) {#enhanced-caching-translated-adaptive-forms}

Vous pouvez désormais spécifier le [paramètre régional en tant que sélecteur dans l’URL du formulaire adaptatif au lieu d’un argument dans l’URL du formulaire adaptatif](../../help/forms/using/supporting-new-language-localization.md). Il permet de mettre en cache les formulaires adaptatifs traduits sur [!DNL Experience Manager Dispatcher]. La mise en cache du formulaire adaptatif traduit n’était pas possible dans les versions précédentes. Pour plus d’informations sur la configuration de la mise en cache pour l’utilisation des paramètres régionaux en tant que sélecteur dans l’URL du formulaire adaptatif, voir [Configuration du cache de formulaire adaptatif à l’adresse dispatcher](../../help/forms/using/configure-adaptive-forms-cache.md).

#### Enregistrez la sortie du service de modèle de données de formulaire à une variable (6.5.6.0) {#save-fdm-service-to-variable}

Le modèle de données de formulaire vous permet d’enregistrer la sortie d’un service de modèle de données de formulaire dans une variable. [!DNL Experience Manager Forms] mappe désormais automatiquement le type du service de modèle de données de formulaire au type de variable .

#### Joindre plusieurs fichiers pour le composant Pièce jointe (6.5.6.0) {#attach-multiple-files}

Vous pouvez désormais [joindre plusieurs fichiers](../../help/forms/using/introduction-forms-authoring.md) au composant [!UICONTROL Pièce jointe] des formulaires adaptatifs.

#### Personnaliser les colonnes de la boîte de réception Adobe Experience Manager (6.5.5.0) {#customize-aem-inbox-columns}

Vous pouvez personnaliser une [!DNL Experience Manager] boîte de réception pour modifier le titre par défaut d’une colonne, réorganiser la position d’une colonne et afficher des colonnes supplémentaires en fonction des données d’un workflow. Les membres du groupe `administrators` ou `workflow-administrators` peuvent personnaliser les colonnes. Pour plus d’informations, voir [Contrôle d’administration](../sites-authoring/inbox.md#inbox-admin-control).

![Personnalisation des colonnes de la boîte de réception du Experience Manager](assets/customize-columns.gif)

#### Enregistrer les communications interactives en tant que brouillon (6.5.5.0) {#save-as-draft}

Vous pouvez utiliser l’interface utilisateur de l’agent pour enregistrer un ou plusieurs brouillons pour chaque communication interactive et récupérer le brouillon ultérieurement pour continuer à travailler dessus. Vous pouvez spécifier un nom différent pour chaque brouillon afin de l’identifier. Pour plus d’informations, voir [Enregistrer les communications interactives en tant que brouillon](../forms/using/prepare-send-interactive-communication.md#save-as-draft).

![Enregistrer en tant que brouillon](assets/save-as-draft.gif)

#### [!DNL Oracle WebLogic] Prise en charge des serveurs d’applications (6.5.5.0)  {#weblogic-support}

Adobe Experience Manager Forms a ajouté la prise en charge de [!DNL Oracle WebLogic 12] pour Adobe Experience Manager Forms on JEE. Vous pouvez effectuer une mise à niveau à partir d’une version précédente ou configurer un nouveau serveur Forms on JEE Experience Manager 6.5 sur [!DNL Oracle WebLogic] 12.2.1.4 et versions ultérieures. Plus tard correspond aux changements de version mineurs, où x dans la version 12.2.1.x est remplacé par un numéro de version.

#### Améliorations de l’accessibilité (6.5.5.0) {#accessibility-improvements}

Adobe Experience Manager Forms comprend les améliorations d’accessibilité suivantes :

* Lorsqu’un utilisateur prévisualise un formulaire adaptatif en tant que formulaire HTML, le champ [!UICONTROL Signature tactile] conserve la sélection de l’onglet.

* Les messages d’erreur affichés lors de l’envoi d’un formulaire adaptatif contiennent désormais l’attribut `aria-describedBy`. L&#39;attribut est attaché aux champs référencés dans le message d&#39;erreur. L&#39;attribut `aria-describedby` indique les identifiants des éléments qui décrivent l&#39;objet. Cela permet d’établir une relation entre les widgets ou les groupes et le texte qui les décrit.

* Si un formulaire adaptatif comporte des champs obligatoires, l’attribut obligatoire est défini sur `True` pour ces champs dans le schéma d’accessibilité ARIA.

#### Authentification par certificat X-509 pour les services web SOAP dans le modèle de données de formulaire (6.5.5.0) {#x509-based-authentication-soap}

Le modèle de données de formulaire prend désormais en charge l’authentification par certificat X-509 lors de l’utilisation des services web SOAP comme source de données. Pour plus d’informations, voir [Configuration des services Web SOAP](../forms/using/configure-data-sources.md#configure-soap-web-services).

#### Autres améliorations clés (6.5.5.0) {#other-improvements}

* Experience Manager 6.5 Forms on JEE Document Security est désormais basé sur [!DNL Apache Struts 2].

* Ajout de la prise en charge de [!DNL Oracle Real Applications Cluster (RAC) 19c].

#### Générer une sortie imprimable dans les workflows Forms Experience Manager (6.5.4.0) {#generate-printable-output}

L’étape de workflow Générer une sortie imprimable permet d’intégrer un fichier de modèle source à un fichier de données. Cette intégration permet d&#39;imprimer ou d&#39;enregistrer différentes copies du fichier de modèle. L’étape génère une sortie PCL, PostScript, ZPL, IPL, TPCL ou DPL. Pour plus d’informations sur cette fonctionnalité, voir [Workflow Forms sur OSGi - Référence des étapes](../forms/using/aem-forms-workflow-step-reference.md).

![Générer une sortie imprimable](assets/generate-print-output-step.gif)

#### Prise en charge de plusieurs colonnes pour les formulaires adaptatifs et les communications interactives en mode Disposition (6.5.4.0) {#multi-column-adaptive-forms}

Vous pouvez désormais définir le nombre de colonnes d’un panneau dans les formulaires adaptatifs et les communications interactives. Passez en mode de mise en page pour utiliser la nouvelle option à plusieurs colonnes. Pour plus d’informations, voir [Utilisation du mode Mise en page pour redimensionner les composants](../forms/using/resize-using-layout-mode.md).

![Disposition multi-colonnes](assets/multi-column-layout.gif)

#### Personnalisations de la boîte de réception du Experience Manager (6.5.4.0) {#aem-inbox}

La nouvelle option de contrôle d’administration permet aux administrateurs de :

* Personnalisez le texte et le logo de l’en-tête.

* Contrôle l’affichage des liens de navigation disponibles dans l’en-tête.

L’option Contrôle d’administration est visible uniquement pour les membres du groupe `administrators` ou `workflow-administrators` . Pour plus d’informations sur cette fonctionnalité, voir [Votre boîte de réception](../sites-authoring/inbox.md).

#### Prise en charge de texte enrichi dans les formulaires HTML5 (6.5.4.0) {#rich-text-support}

Convertissez un champ de texte d’un formulaire XFA en champ de texte enrichi dans un formulaire HTML5. Pour plus d’informations, voir [Conception de modèles de formulaire pour les formulaires HTML5](../forms/using/designing-form-template.md).

#### Améliorations de l’accessibilité (6.5.4.0) {#forms-accessibility-enhancements-6540}

Experience Manager Forms comprend les améliorations d’accessibilité suivantes :

* Les lecteurs d’écran annoncent correctement les cases à cocher, les liens, le sélecteur de date et les champs de saisie de date dans un formulaire adaptatif.

* Chaque page d’un formulaire adaptatif comprend désormais un titre et un libellé de repère principal.

#### Partage et demande l’accès aux éléments de boîte de réception d’un utilisateur Forms Experience Manager (6.5.3.0) {#share-request-access}

Vous pouvez partager vos éléments de boîte de réception avec un autre utilisateur. Une fois qu’un autre utilisateur a accès à vos éléments de boîte de réception, il peut demander et prendre les mesures appropriées sur les éléments partagés. De même, vous pouvez demander l’accès aux éléments de boîte de réception à d’autres utilisateurs. Voir [Partager et demander l’accès aux éléments de boîte de réception d’un utilisateur](../forms/using/configure-shared-queues-osgi.md).

#### Configuration des paramètres d’absence du bureau pour les éléments de boîte de réception d’un utilisateur Forms Experience Manager (6.5.3.0) {#configure-out-of-office}

Si vous envisagez de vous absenter du bureau, vous pouvez spécifier les actions à entreprendre pour les tâches qui vous sont affectées pendant cette période.
Vous pouvez spécifier une date et une heure de début, ainsi qu’une date et une heure de fin, pour l’application de vos paramètres d’absence du bureau. Vous pouvez définir une personne par défaut à qui tous vos éléments sont envoyés. Voir [Configuration des paramètres d’absence du bureau](../forms/using/configure-out-of-office-settings.md).

#### Générer plusieurs communications interactives à l’aide de l’API Batch pour Experience Manager Forms (6.5.3.0) {#generate-multiple-ic}

Vous pouvez utiliser l’API Batch pour produire plusieurs communications interactives à partir d’un modèle. Le modèle est une communication interactive sans données. L’API Batch combine des données à un modèle afin de produire une communication interactive. L’API est utile pour la production en masse de communications interactives. Par exemple, les factures de téléphone, les relevés de carte de crédit pour plusieurs clients. Voir [Générer plusieurs communications interactives à l’aide de l’API de lot](../forms/using/generate-multiple-interactive-communication-using-batch-api.md).

<!-- TBD: Check if the wider team released anything in FY21.
-->

## Versions clés depuis [!DNL Adobe Experience Manager] 6.5 SP7 {#key-releases-since-last-sp}

Entre le 26 novembre 2020 et le 25 février 2021, Adobe a publié les éléments suivants, en plus des Service Packs et des Cumulative Fix Packs :

* [!DNL Adobe Experience Manager] en tant que Cloud Service  [2020.11.0](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/2020/release-notes-2020-11-0.html),  [2020.12.0](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/2020/release-notes-2020-12-0.html) et  [2021.1.0](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=en#release-date).

* [[!DNL Experience Manager] application de bureau 2.1 (2.1.0.0)](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html).

* [Experience Manager Screens : Feature Pack 202011](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/release-notes/release-notes-fp-202011.html?lang=fr)

>[!MORELIKETHIS]
>
>* [[!DNL Adobe Experience Manager] Documentation 6.5](../user-guide/home.md)
* [Notes de mise à jour générales pour [!DNL Adobe Experience Manager] 6.5](release-notes.md)
* [Notes de mise à jour du Service Pack pour  [!DNL Adobe Experience Manager] 6.5](sp-release-notes.md)

