---
title: Nouveautés d’ [!DNL Experience Manager] 6.5 Service Pack 11
description: Nouveautés d’ [!DNL Experience Manager] 6.5 Service Pack 11
contentOwner: AK
mini-toc-levels: 1
exl-id: 32470e6e-8a66-4670-82da-2259f6e001c3
source-git-commit: 35260325b583bd047f22ffa88afb9469b2023e60
workflow-type: tm+mt
source-wordcount: '4391'
ht-degree: 6%

---

# Nouveautés d’ [!DNL Adobe Experience Manager] 6.5 Service Pack 11 {#aem-whats-new-service-pack}

<!-- TBD: Downsample this image. We do not need as big an image since customers don't use as big a screen to view. Also, having a 700+ KB decorative image is bad for page load time.
-->

![Whats-new](assets/whatsnew.jpeg)

[!DNL Adobe Experience Manager] 6.5 Les Service Packs proposent, à intervalles trimestriels, de nouvelles fonctionnalités, des améliorations demandées par les clients, ainsi que des améliorations en termes de performances, de stabilité et de sécurité. La disponibilité trimestrielle facilite l’accès et l’adoption de nouvelles fonctionnalités et innovations.

Cet article met en évidence les fonctionnalités incluses dans le dernier Service Pack. [fonctionnalités clés incluses dans les Service Packs de la version 6.5 précédente](#key-features-previous-service-packs), et la variable [mises à jour clés depuis le dernier Service Pack](#key-releases-since-last-sp) version .

## [!DNL Adobe Experience Manager Sites] {#aem-sites}

* La génération automatique du plan de site à des fins d’optimisation pour les moteurs de recherche est possible à l’aide de la variable [Package d’index SEO](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/sites-seo-index-content-1.0.0.zip). Il prend en charge les plans de site, les URL de remplacement, les balises de métadonnées de robot, etc. dans la variable [!DNL Core Components].

* Ajout de la prise en charge de champs multiples pour le type de données de texte multiligne.

* Amélioration pour sensibiliser les utilisateurs à la tâche asynchrone en cours d’exécution en arrière-plan afin de les empêcher de déclencher plusieurs opérations asynchrones sur le même chemin.

## [!DNL Adobe Experience Manager Assets] {#aem-assets}

* Une amélioration de l’expérience utilisateur affiche le nombre de ressources présentes dans un dossier. Pour plus de 1 000 ressources dans un dossier, [!DNL Assets] affiche 1000+.

   ![Nombre de ressources dans un dossier](/help/assets/assets/browse-folder-number-of-assets.png)

* Les améliorations d’accessibilité suivantes sont disponibles :

   * En mode Carte dans le [!DNL Assets] référentiel, lors de l’utilisation de `Tab` pour déplacer la sélection vers le premier élément qui ouvre les actions rapides sur le focus, le lecteur d’écran annonce le nom de l’élément sélectionné.
   * Dans [!DNL Dynamic Media] [!UICONTROL Éditeur de paramètres prédéfinis de la visionneuse], lorsque les couleurs de l’ombre et de la bordure ne sont pas présentes, les entrées sont désactivées à l’aide de la propriété disabled. Les utilisateurs du clavier ne sont pas en mesure de cibler l’entrée et les lecteurs d’écran n’annoncent pas l’état du contrôle comme désactivé.
   * Dans [!DNL Dynamic Media], dans l’interface de création d’un profil de codage vidéo, la variable [!UICONTROL Rapport de recadrage intelligent] est étiquetée pour l’accessibilité afin que les lecteurs d’écran l’annoncent correctement.

### [!DNL Dynamic Media] {#dynamic-media}

* Vous pouvez désormais utiliser [!DNL Dynamic Media] pour configurer les paramètres généraux au lieu d’avoir à passer par l’ [!DNL Dynamic Media Classic] application de bureau. Voir [Configuration des paramètres généraux de Dynamic Media](/help/assets/dm-general-settings.md).

   ![Paramètres généraux de DM](/help/assets/assets-dm/dm-general-settings.png)

* Vous pouvez désormais utiliser [!DNL Dynamic Media] pour configurer la configuration de la publication au lieu d’avoir à passer par la [!DNL Dynamic Media Classic] application de bureau. Voir [Configuration de la publication Dynamic Media](/help/assets/dm-publish-settings.md).

   ![Paramètres de publication DM](/help/assets/assets-dm/dm-publish-setup.png)

## [!DNL Adobe Experience Manager Forms] {#aem-forms}

>[!NOTE]
>
>* [!DNL Experience Manager Forms] publie les packages de modules complémentaires une semaine après la date de publication prévue du Service Pack [!DNL Experience Manager].


## Fonctionnalités clés de la version précédente [!DNL Experience Manager] 6.5 Service Packs {#key-features-previous-service-packs}

### [!DNL Experience Manager Sites] {#aem-sites-previous-service-packs}

#### Fonctionnalités incluses dans la version AEM 6.5.10.0 {#features-sites-65100}

* **Amélioré [!DNL Content Fragment] Modèles et éditeur**: Vous pouvez désormais créer des modèles complexes et personnalisés pour du contenu structuré à l’aide de modèles imbriqués. [!DNL Content Fragment] modèles. Les structures de contenu sont modulaires en éléments de base modélisés en sous-fragments. Les fragments de niveau supérieur référencent ces sous-fragments. D’autres améliorations de type de données telles que les règles de validation avancées améliorent davantage la flexibilité de la modélisation de contenu avec [!DNL Content Fragments]. Le [!DNL Experience Manager] [!DNL Content Fragment] l’éditeur prend en charge les structures de fragments imbriqués dans une session d’éditeur courante, avec des améliorations telles que l’arborescence de structure et la navigation par chemin de navigation à onglets dans les hiérarchies de fragments.

* **API GraphQL pour[!DNL Content Fragments]**: La nouvelle API GraphQL est la méthode standard pour diffuser du contenu structuré au format JSON. Les requêtes GraphQL permettent aux clients de demander uniquement les éléments de contenu appropriés pour effectuer le rendu d’une expérience. Une telle sélection élimine la sur-diffusion du contenu (possibilité avec les API HTTP REST) qui nécessite une analyse du contenu côté client. Les schémas GraphQL sont dérivés de [!DNL Content Fragment] Les modèles et les réponses de l’API sont effectués au format JSON. Dans [!DNL Experience Manager] as a [!DNL Cloud Service], [Requêtes GraphQL persistantes](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/graphql-api-content-fragments.html#persisted-queries-caching) et traiter les demandes de GET compatibles avec le cache. Cela n’est pas encore possible dans [!DNL Experience Manager] 6.5.

* **Gestion des hiérarchies et aperçu futur**: Les utilisateurs disposent désormais d’une interface pour accéder aux structures de contenu de leurs [!DNL Experience Manager] lancements, notamment la possibilité d’ajouter et de supprimer des pages dans un lancement. Cette fonctionnalité améliore la flexibilité de [!DNL Experience Manager] se lance pour créer des versions de contenu destinées à une publication ultérieure. [Fonctionnalité de déformation temporelle](/help/sites-authoring/working-with-page-versions.md#timewarp) permet aux utilisateurs de prévisualiser les lancements en tant qu’états de contenu futurs.

* [!DNL Experience Manager] affiche directement une liste de tous les modèles de contenu sous un dossier sans que les auteurs de contenu aient à parcourir la structure de fichiers. Cette fonctionnalité nécessite désormais moins de clics et améliore l’efficacité de la création.

* Champ de chemin dans [!DNL Sites] l’éditeur permet aux auteurs de faire glisser des ressources depuis [!DNL Content Finder].

* Platform fournit quelques améliorations de l’accessibilité. Voir [Mises à jour de plateforme](/help/release-notes/sp-release-notes.md#platform-65100).

#### Possibilité de restaurer l’arborescence et les pages supprimées (6.5.9.0) {#ability-to-restore-pages-tree}

Vous pouvez désormais restaurer les pages supprimées et l’intégralité de l’arborescence sur une [!DNL Experience Manager Sites] page.

#### Tri des pages Live Copy disponibles pour le déploiement (6.5.8.0) {#sort-livecopy-pages}

Vous pouvez désormais trier les pages Live Copy disponibles pour déploiement à l’aide de la variable [!UICONTROL Nom], [!UICONTROL Date de dernière modification], et [!UICONTROL Date du dernier déploiement] propriétés. Le [!UICONTROL Date du dernier déploiement] pour une page est une nouvelle propriété introduite dans cette version.

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

* [!DNL Adobe Experience Manager Experience Fragments] exporté vers [!DNL Adobe Target] les espaces de travail apparaissent désormais comme des types d’offres uniques et des sources d’offres dans [!DNL Target].

* Multi Site Manager : le déclencheur de publication supprime désormais un composant de la page publiée si un composant est supprimé de la page source.

* Multi Site Manager : nom d’un composant local dans une [!UICONTROL Live Copy] est identique au nom d’un composant dans le plan directeur et le composant est déployé à partir du plan directeur, puis le terme `_msm_moved` est maintenant ajouté au nom du composant local.

#### Améliorations du système de style (6.5.4.0) {#style-system-enhancements}

Vous pouvez désormais sélectionner des styles dans la boîte de dialogue du composant à l’aide du système de style amélioré.

#### Amélioration des performances dans divers domaines (6.5.4.0) {#performance-improvements}

* Réduction du temps de chargement et d’initialisation de ContextHub dans un site (`contexthub.kernel.js`). Cela entraîne un chargement de page plus rapide lors d’une visite du site.

* Réduction du temps d’actualisation d’une page après le glissement [!DNL Experience Fragments] to [!DNL Sites] Éditeur de page.

* Réduction du temps de chargement des entrées sur un [!DNL Sites] avec plus de 200 Live Copies dans **[!UICONTROL Présentation de la Live Copy]**.

* Amélioration de la gestion des URL incomplètes ou non valides. Ces URL peuvent ralentir l’éditeur de modèles.

### [!DNL Adobe Experience Manager Assets] {#aem-assets-previous-service-packs}

#### Fonctionnalités incluses dans la version AEM 6.5.10.0 {#features-assets-65100}

* [!DNL Experience Manager] étend la fonctionnalité Ressources connectées à l’utilisation de la fonction [!DNL Dynamic Media] images dans les composants principaux applicables. Voir [Utilisation des ressources connectées](/help/assets/use-assets-across-connected-assets-instances.md).

* Lors du partage de ressources et de collections individuelles en tant que lien (à l’aide de [!UICONTROL Partage de liens] ), les utilisateurs peuvent choisir de laisser le destinataire télécharger les ressources d’origine, leurs rendus ou les deux. Voir [Partage de ressources via un lien](/help/assets/link-sharing.md).

   ![option permettant d’autoriser le téléchargement uniquement des ressources d’origine, des rendus uniquement ou des deux](/help/release-notes/assets/share-assets-as-link.png)

* Lorsque les utilisateurs téléchargent des ressources partagées avec eux sous la forme d’un lien, ils peuvent choisir de télécharger les ressources d’origine, les rendus ou les deux.

* **Limiter les sous-ressources générées**: Les administrateurs peuvent limiter le nombre de sous-ressources qui [!DNL Experience Manager] génère pour les ressources composites telles que les fichiers PDF, PowerPoint, InDesign et Keynote.

   ![limiter la génération des sous-ressources ;](/help/assets/assets/sub-asset-limit.png)

* Une nouvelle [!DNL Camera Raw] module disponible qui prend en charge [!DNL Adobe Camera Raw] v10.4. Voir [traitement des images à l’aide de [!DNL Camera Raw]](/help/assets/camera-raw.md).

#### Versions précédentes {#previous-releases-assets}

* Mise à jour du nom des régions et paramètres régionaux chinois relatifs à Hong Kong, Macao et Taïwan, afin qu&#39;ils soient cohérents avec les opinions sociales et politiques chinoises (6.5.9.0).

* Une configuration facultative est introduite pour modifier la casse des ID d’email dans la réponse de l’API ACP. [!DNL Adobe Experience Manager] (6.5.9.0).

   ![configuration pour modifier les ID d’email en minuscules dans la réponse ACP de [!DNL Experience Manager]](assets/email-lowcase-config.png)

* Le contraste entre le texte et les icônes en arrière-plan est amélioré pour différentes fonctionnalités. Cette mise en oeuvre des directives WCAG (Web Content Accessibility Guidelines) crée des [!DNL Assets] plus accessibles pour les utilisateurs dont la vision et la perception des couleurs sont limitées. Voir [améliorations de l’accessibilité dans [!DNL Assets]](sp-release-notes.md#assets-accessibility-6590) (6.5.9.0).
* Lors de l’utilisation de [Fonctionnalité Ressources connectées](/help/assets/use-assets-across-connected-assets-instances.md), vous pouvez désormais afficher une liste de tous les [!DNL Sites] pages qui utilisent la ressource. Ces références à une ressource sont disponibles dans la variable [!UICONTROL Propriétés] page. Cela permet aux administrateurs, aux spécialistes du marketing et aux bibliothécaires d’avoir une vue complète de l’utilisation des ressources, ce qui permet un meilleur suivi, une meilleure gestion et une meilleure cohérence de la marque (6.5.8.0).

* Lors de la suppression d’une ressource référencée dans une page web, [!DNL Experience Manager] affiche un avertissement. Vous pouvez forcer la suppression d’une ressource référencée ou vérifier et modifier les références affichées dans la variable [!DNL Properties] de la ressource. Cliquer sur les références ouvre le fichier local et distant [!DNL Sites] (6.5.8.0).

* [!DNL Assets] et [!DNL Dynamic Media] proposent plusieurs améliorations de l’accessibilité. Les améliorations ont été apportées à la navigation au clavier, à l’utilisation des lecteurs d’écran et à des améliorations similaires pour permettre l’utilisation des technologies d’assistance (AT). Voir [[!DNL Assets] améliorations](/help/release-notes/sp-release-notes.md#assets-6570) et [[!DNL Dynamic Media] améliorations](/help/release-notes/sp-release-notes.md#dynamic-media-6570) (6.5.7.0)

* Les utilisateurs peuvent trier les ressources numériques en mode Carte et Colonnes (6.5.7.0).

#### Améliorations de l’accessibilité (6.5.6.0) {#accessibility-assets-6560}

* **Amélioration de la mise au point de l’interface utilisateur lors de la navigation clavier**, par exemple, concentrez-vous sur :

   * `x` dans [!UICONTROL Aperçu de la version] Boîte de dialogue d’une ressource dans [!UICONTROL Chronologie].

   * Options d’interface utilisateur pratiques.

   * Champ Email sur [!UICONTROL Partager le lien] et champ pour ajouter un groupe d’utilisateurs fermé dans [!UICONTROL Autorisation] onglet du dossier [!UICONTROL Propriétés].

* **Amélioration des fonctionnalités à l’aide des touches de clavier**

   Les utilisateurs peuvent utiliser les touches du clavier pour faire glisser des commandes dans l’éditeur de formulaire de schéma de métadonnées en mode de navigation du lecteur d’écran.

* **Utilisation améliorée pour les utilisateurs de lecteurs d’écran**, en raison des éléments suivants :

   * Les lecteurs d’écran annoncent l’objectif des lecteurs vidéo et audio.

   * Les lecteurs d’écran indiquent l’objectif des options de l’interface utilisateur pour supprimer les balises sélectionnées à l’aide de [!UICONTROL Boîte de dialogue de sélection des balises] sur la ressource [!UICONTROL Propriétés].

   * Les lecteurs d’écran annoncent les en-têtes de ligne et les éléments de ligne des tableaux, de sorte que les utilisateurs sachent quelles entrées appartiennent à la même ligne.

   * Titre descriptif et significatif de la page de recherche.

   * Les lecteurs d’écran annoncent les options du panneau des filtres de recherche sous forme d’accordéons extensibles.

#### Autres améliorations de la fonctionnalité [!DNL Assets] (6.5.6.0) {#other-enhancements-assets-6560}

* Les groupes d’utilisateurs associés aux dossiers (privés et non privés) sont désormais supprimés du référentiel sur [suppression de ces dossiers](/help/assets/private-folder.md#delete-private-folder). Toutefois, les groupes d’utilisateurs redondants, orphelins, inutilisés et générés automatiquement existants peuvent être supprimés du référentiel à l’aide de JMX.

#### Améliorations de l’accessibilité dans [!DNL Assets] (6.5.5.0) {#assets-accessibility}

[!DNL Experience Manager Assets] est désormais plus accessible, conformément aux directives WCAG (Web Content Accessibility Guidelines). L’accessibilité a été améliorée en raison des améliorations suivantes :

* De nombreux éléments, commandes, pages et boîtes de dialogue de l’interface utilisateur sont compatibles avec les lecteurs d’écran.

* De nombreux éléments, contrôles et champs de formulaire de saisie de l’interface utilisateur sont accessibles à l’aide du clavier.

* La couleur et le contraste de certains éléments de l’interface utilisateur ont été mis à jour afin que les utilisateurs disposant d’une vision limitée ou qui ne perçoivent pas les couleurs puissent distinguer ces éléments de l’interface utilisateur. Par exemple, la couleur des icônes d’évaluation des étoiles (comme dans [!UICONTROL Évaluation] section [!UICONTROL Avancé] onglet de la ressource [!UICONTROL Propriétés] ou en mode Carte) est modifié pour un contraste approprié.

   ![Icônes de notation avec meilleur contraste](assets/star-rating-icons.png)

#### Amélioration de la gestion des exceptions (6.5.5.0) {#exception-handling}

[!DNL Assets] le flux de l’interface utilisateur a une meilleure gestion des exceptions. Si une ressource n’a pas de type pour sa dimension, l’exception observée est enregistrée dans les fichiers journaux.

#### Configurer [!DNL Experience Manager Assets] avec [!DNL Brand Portal] (6.5.4.0) {#configure-assets-bp}

Le canal d’autorisation entre [!DNL Experience Manager Assets] et [!DNL Brand Portal] est modifiée. Plus tôt : [!DNL Brand Portal] a été configuré dans l’interface utilisateur classique via la passerelle OAuth héritée, qui utilise l’échange de jetons JWT pour obtenir un jeton d’accès IMS en vue de l’autorisation. [!DNL Experience Manager Assets] est maintenant configuré avec [!DNL Brand Portal] through [!DNL Adobe I/O], qui fournit un jeton IMS pour autoriser votre [!DNL Brand Portal] client.

Étapes de configuration [!DNL Experience Manager Assets] avec [!DNL Brand Portal] sont différents selon les [!DNL Experience Manager] et si vous effectuez une configuration pour la première fois, ou si vous mettez à niveau les configurations existantes. Voir [Configuration d’Experience Manager Assets avec Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html?lang=fr) pour plus de détails.

#### Améliorations de l’accessibilité (6.5.4.0) {#accessibility-enhancements-6540}

[!DNL Experience Manager Assets] comprend les améliorations d’accessibilité suivantes :

* Vous pouvez utiliser les touches fléchées du clavier pour déplacer et déplacer des zones dans les images agrandies. Pour plus d’informations, voir [prévisualisation de ressources à l’aide des touches du clavier uniquement](../assets/manage-assets.md#previewing-assets).

* Les cases à cocher d’état mixte (dans lesquelles, sauf si vous sélectionnez tous les prédicats imbriqués, les cases de premier niveau ne sont pas sélectionnées et sont enfoncées) du panneau Filtres sont lisibles par les lecteurs d’écran.

* Les contraintes de format de date et d’heure sont fournies dans les libellés de champ des champs de date, afin de permettre aux utilisateurs de saisir la date dans le bon format à l’aide du clavier.
Par exemple, `On Time (MM-DD-YYYY HH:mm)`. Ici MM est un mois à deux chiffres, AAAA est l’année, JJ est un jour à deux chiffres, HH est une heure au format militaire 24 heures et mm est une minute.

* Les lecteurs d’écran annoncent l’option de suppression des balises sélectionnées (`X` ) et le nombre de balises sélectionnées.

#### Colonne Triable pour la date de création des ressources en mode Liste (6.5.3.0) {#sortable-date-created-column}

Une nouvelle colonne pouvant être triée pour la date de création des ressources est ajoutée en mode Liste de la gestion des actifs numériques et dans les résultats de recherche de ressources en mode Liste.

![Colonne Triable pour la date de création](assets/asset-created-date.png)

#### Recherche visuelle pour [!DNL Adobe Experience Manager Assets] (6.5.2.0) {#visual-search}

[!DNL Assets] les utilisateurs peuvent rechercher des images visuellement similaires. Experience Manager affiche les images balisées intelligentes du référentiel DAM qui sont similaires à une image sélectionnée par l’utilisateur. Voir [Recherche visuelle](../assets/search-assets.md).

### Dynamic Media {#dynamic-media-previous-service-packs}

* De nombreuses améliorations de l’accessibilité sont apportées dans [!DNL Dynamic Media] afin qu’un lecteur d’écran puisse présenter une description plus appropriée et plus utile de l’action ou de l’interface utilisateur. Voir [[!DNL Dynamic Media] mises à jour](/help/release-notes/sp-release-notes.md#dynamic-media-65100) (6.5.10.0).

* [[!DNL Dynamic Media] est plus accessible](sp-release-notes.md#assets-accessibility-6590) en termes de :

   * Facilité d’utilisation avec les touches du clavier.
   * Contraste (avec arrière-plan) de texte, de texte d’espace réservé et de contrôles dans divers éditeurs.
   * Accessibilité et narration par les lecteurs d’écran.

* Diffusez efficacement des images de meilleure qualité sur les appareils dotés d’affichages haute résolution et d’une bande passante réseau limitée, grâce au RGPD (rapport de pixels de périphérique) d’imagerie dynamique et à l’optimisation de la bande passante du réseau. Voir [FAQ sur l’imagerie dynamique](/help/assets/imaging-faq.md) (6.5.9.0).

* [!DNL Dynamic Media] delivery (`fmt` Modificateur d’URL) prend désormais en charge le format d’image de nouvelle génération AVIF (format d’image AV1). Pour plus d’informations et de détails sur la chronologie, voir [fmt de l’API de diffusion d’images et de rendu](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-is-http-fmt.html) (6.5.9.0).

#### Prise en charge des ressources 3D dans [!DNL Dynamic Media] (6.5.5.0) {#support-for-3d}

Prise en charge des images 3D dans [!DNL Dynamic Media] permet aux clients de publier et d’ajouter du contenu 3D à des pages web et à des applications. La prise en charge inclut :

* Publiez des formats de ressource 3D courants et générez une URL de ressource qui peut être utilisée dans des pages web et d’autres applications.

* Visionneuse web 3D optimisée par [!DNL Adobe Dimension], pour afficher de manière interactive les ressources 3D publiées.

* Publication et affichage de ressources 3D courantes sur [!DNL Experience Manager Sites] à l’aide des [!DNL Sites] Composant WCM.

#### Invalider le contenu mis en cache du réseau de diffusion de contenu (6.5.6.0) {#invalidate-cdn-cached-content}

Vous pouvez désormais utiliser la variable [!DNL Dynamic Media] interface utilisateur pour invalider le contenu mis en cache du réseau de diffusion de contenu (CDN). Par conséquent, les ressources mises à jour sont disponibles instantanément au lieu d’attendre que le cache arrive à expiration. Vous pouvez invalider le réseau de diffusion de contenu en procédant comme suit :

* Création d’un modèle d’invalidation du réseau CDN : Sélection de ressources et d’URL basées sur des modèles associés à un formulaire

* Sélection de ressources et de paramètres prédéfinis associés via le sélecteur de ressources

* Ajout d’URL de ressource complètes

#### Publication sélective de ressources dans [!DNL Experience Manager] et [!DNL Dynamic Media] (6.5.6.0) {#selective-publishing}

Vous pouvez désormais choisir de publier des ressources de manière sélective ou d’en annuler la publication. [!DNL Experience Manager] ou [!DNL Dynamic Media] using [!UICONTROL Publication rapide] ou [!UICONTROL Gérer la publication] assistant. Vous pouvez également définir la variable `Publish` ou `Unpublish` au niveau du dossier.

#### Imagerie dynamique pour Dynamic Media {#smart-imaging}

L’imagerie dynamique utilise les caractéristiques de visualisation uniques de chaque utilisateur pour diffuser automatiquement les images appropriées optimisées pour leur expérience, ce qui se traduit par de meilleures performances et un meilleur engagement. L’imagerie dynamique fonctionne avec vos paramètres d’image prédéfinis et utilise des informations à la dernière milliseconde de la diffusion pour réduire davantage encore la taille du fichier d’image en fonction de la vitesse de connexion du réseau et du navigateur. Voir la section [Imagerie dynamique](../assets/imaging-faq.md).

#### Recadrage intelligent dans les profils vidéo pour Dynamic Media (6.5.3.0) {#smart-crop-video}

Le recadrage intelligent pour la vidéo (une fonctionnalité en option dans les profils vidéo) utilise Adobe Sensei pour détecter et recadrer automatiquement le point focal dans une vidéo adaptative ou progressive, quelle que soit sa taille. Voir [à propos de l’utilisation du recadrage intelligent dans les profils vidéo](../assets/video-profiles.md).

### Experience Manager Forms {#aem-forms-previous-service-packs}

#### Fonctionnalités incluses dans la version AEM 6.5.10.0 {#features-forms-65100}

>[!NOTE]
>
>Package de module complémentaire de [!DNL Experience Manager Forms] est rendu disponible une semaine après la planification [!DNL Experience Manager] Version du Service Pack.

* Vous pouvez désormais utiliser le service Automated forms conversion pour [Conversion de PDF forms en français, allemand, espagnol, italien et portugais](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html#language-specific-meta-model) aux formulaires adaptatifs.

* **Messages d’erreur dans le navigateur Propriétés** : ajout de messages d’erreur pour chaque propriété dans le navigateur Propriétés des formulaires adaptatifs. Ces messages aident à comprendre les valeurs autorisées pour un champ.

* **Prise en charge de l’utilisation de l’option littérale pour définir la valeur d’une variable de type JSON**: Vous pouvez utiliser l’option littérale pour définir la valeur d’une variable de type JSON à l’étape de définition de la variable d’un workflow AEM. L’option de littéral permet de spécifier un fichier JSON sous la forme d’une chaîne.

* [Mises à jour de la plateforme](../forms/using/aem-forms-jee-supported-platforms.md): [!DNL Adobe Experience Manager Forms] sur JEE a ajouté la prise en charge des plateformes suivantes :
   * [!DNL Adobe Acrobat 2020]
   * [!DNL Ubuntu 20.04]
   * [!DNL Open Office 4.1.10]
   * [!DNL Microsoft Office 2019]
   * [!DNL Microsoft Windows Server 2019]
   * [!DNL RHEL8]

* Ajout de la prise en charge de `GuideBridge#getGuidePath` API dans [!DNL AEM Forms].

#### Prise en charge de [!DNL Azul Zulu OpenJDK] (6.5.9.0) {#support-azul-zulu}

Vous pouvez désormais développer et exploiter des applications avec [!DNL Azul Zulu] versions de [!DNL OpenJDK] pour [!DNL Experience Manager Forms] sur les déploiements OSGi. Pour plus d’informations, voir [Notes de mise à jour de Experience Manager 6.5 Service Pack 9](sp-release-notes.md) et [Exigences techniques](../sites-deploying/technical-requirements.md).

#### Possibilité d’envoyer un email de notification à un groupe à l’aide de [!UICONTROL Assign Task] (6.5.9.0) {#group-notification-email}

Vous pouvez maintenant envoyer un email de notification à une adresse email de groupe à l’aide de l’étape de workflow Affecter une tâche .

#### Possibilité de récupérer un brouillon de communication interactive après modification de la communication interactive source (6.5.9.0) {#retrieve-draft-after-source-modifications}

Vous pouvez désormais récupérer une communication interactive enregistrée en tant que brouillon après avoir modifié la communication interactive source.

#### Définissez le nom de domaine personnalisé pour le chargement, le rendu et la validation du service reCAPTCHA (6.5.9.0). {#set-custom-domain-name-recaptcha}

Le service reCAPTCHA utilise `https://www.recaptcha.net/` comme domaine par défaut. Vous pouvez désormais modifier les paramètres à définir. `https://www.google.com/` ou tout nom de domaine personnalisé pour charger, générer et valider le service reCAPTCHA.

#### Améliorations des données d’entrée pour [!UICONTROL Invoquer le service de modèle de données de formulaire] étape de workflow (6.5.9.0) {#input-data-enhancements-fdm}

Lorsque vous sélectionnez un modèle de données de formulaire et un service dans [!UICONTROL Invoquer le service de modèle de données de formulaire] à l’étape du workflow, vous spécifiez des arguments de service pour les données d’entrée.

Si vous sélectionnez [!UICONTROL Relatif à la charge utile] pour joindre un fichier en tant qu’argument de service, vous pouvez maintenant spécifier le chemin du dossier contenant le fichier au lieu du nom réel du fichier. La définition du nom du dossier, au lieu du nom de la pièce jointe, vous permet de réutiliser les modèles de workflow. Vous ne limitez pas le modèle de workflow à un seul nom de pièce jointe.

#### Possibilité d’utiliser plusieurs gabarits dans un modèle de document d’enregistrement (6.5.9.0) {#use-multiple-master-pages-dor-template}

Vous pouvez désormais utiliser plusieurs gabarits dans un modèle de document d’enregistrement. Par conséquent, vous pouvez désormais disposer de différents en-tête, pied de page, polices, informations de logo sur la page de titre et sur d’autres pages du modèle.

#### Sauts de page de prise en charge dans le document d’enregistrement (6.5.9.0) {#support-page-breaks-dor}

Vous pouvez désormais ajouter des sauts de page à un document d’enregistrement. Par conséquent, si un panneau est coupé dans les pages, vous pouvez ajouter un saut de page pour déplacer le panneau vers une nouvelle page d’un document d’enregistrement.

#### Afficher ou masquer le composant CAPTCHA dans un formulaire adaptatif basé sur des règles (6.5.8.0) {#show-hide-captcha}

Vous pouvez désormais valider CAPTCHA lors de l’envoi du formulaire adaptatif ou lors de l’action de l’utilisateur. Vous pouvez également ajouter des conditions pour valider CAPTCHA sur une action utilisateur et afficher ou masquer le composant CAPTCHA dans un formulaire adaptatif basé sur des règles.

#### Ajout de services CAPTCHA personnalisés (6.5.8.0) {#add-custom-captcha-services}

[!DNL Experience Manager Forms] fournit une prise en charge prête à l’emploi pour utiliser Google reCAPTCHA (une licence distincte des API reCAPTCHA de Google est requise) en tant que service de validation CAPTCHA. Vous pouvez également utiliser un service CAPTCHA personnalisé pour valider les CAPTCHA.

#### Autres améliorations (6.5.8.0) {#other-enhancements-forms-6580}

* Amélioration de l’accessibilité du [!DNL Experience Manager Forms] Composant Sélecteur de date.

* Ajout de la prise en charge de la génération d’une communication interactive au format PCL à l’aide de l’API PrintChannel.

* Lors de l’exécution d’une conversion PDFG, vous pouvez désormais activer ou désactiver la variable [!DNL Experience Manager Forms] modifications du registre pour la génération de signets personnalisés.

#### Améliorations des performances (6.5.7.0) {#performance-improvements-forms}

[!DNL Experience Manager] 6.5 Service Pack 7 Forms améliore les performances pour :

* Validation des valeurs de champ sur le serveur lorsque vous envoyez un formulaire adaptatif.

* Conversion d’un formulaire de PDF en formulaire adaptatif à l’aide de la méthode [!DNL Automated Forms Conversion service].

#### Prise en charge des groupes de disponibilité Toujours active pour Microsoft SQL Server 2016 pour une haute disponibilité (6.5.7.0) {#always-on-availability-groups}

[!DNL Experience Manager Forms] prend désormais en charge [!DNL Microsoft] Groupes de disponibilité SQL Server 2016 toujours en service pour une haute disponibilité pour les déploiements OSGi.

#### Configuration du client HTTP du modèle de données de formulaire pour optimiser les performances (6.5.7.0) {#fdm-http-client-config}

[!DNL Experience Manager Forms] le modèle de données de formulaire lors de l’intégration avec les services web RESTful en tant que source de données inclut désormais des configurations de client HTTP pour l’optimisation des performances. Voir [Configuration des sources de données](../../help/forms/using/configure-data-sources.md#fdm-http-client-configuration).

#### Disponibilité de l’option de réinitialisation pour chaque composant en mode Disposition (6.5.7.0) {#reset-option-layout-mode}

Vous pouvez désormais utiliser l’option de réinitialisation pour chaque composant en mode Mise en page d’un formulaire adaptatif. Lorsque vous définissez une mise en page à plusieurs colonnes pour un panneau, vous pouvez utiliser cette fonction pour réinitialiser des composants individuels dans le panneau. Voir [Utilisation du mode de mise en page pour redimensionner les composants](../../help/forms/using/resize-using-layout-mode.md#resize-components).

#### Préremplir un formulaire adaptatif au niveau du client (6.5.6.0) {#prefill-merge-data-at-client}

Lorsque vous préremplissez un formulaire adaptatif, la variable [!DNL Experience Manager Forms] Le serveur fusionne les données avec un formulaire adaptatif et vous transmet le formulaire rempli. Par défaut, l’action de fusion des données a lieu sur le serveur.
Vous pouvez maintenant configurer la variable [!DNL Experience Manager Forms] serveur à [effectuer l’action de fusion de données au niveau du client ;](../../help/forms/using/prepopulate-adaptive-form-fields.md) au lieu du serveur. Cela réduit considérablement le temps nécessaire au préremplissage et au rendu des formulaires adaptatifs.

#### Intégration du modèle de données de formulaire avec les API RESTful sur un serveur avec une implémentation SSL bidirectionnelle (6.5.6.0) {#fdm-integration-rest-apis-two-way-ssl}

[!DNL Experience Manager Forms] Le modèle de données de formulaire peut maintenant [intégrer avec les API RESTful sur un serveur sur lequel est implémenté un protocole SSL bidirectionnel](../../help/forms/using/configure-data-sources.md).

#### Ajout de la prise en charge de [!DNL Adobe Sign] Balises de texte dans Automated forms conversion Service (6.5.6.0) {#sign-integration-acroform-afcs}

Si un AcroForm comprend [!DNL Adobe Sign] Balises de texte, ces champs sont désormais reconnus et représentés comme [!DNL Adobe Sign] champs du formulaire adaptatif converti à l’aide de [!DNL Automated Forms Conversion service]. Un signataire peut remplir ces champs lors de la signature du formulaire adaptatif.

#### Prise en charge de la conversion de PDF forms colorés en formulaires adaptatifs (6.5.6.0) {#colored-PDF-forms}

Vous pouvez utiliser [!DNL Automated Forms Conversion service] pour convertir des PDF forms colorés en formulaires adaptatifs.

#### Prise en charge des protocoles SMB 2 et SMB 3 (6.5.6.0) {#smb-support}

[!DNL Experience Manager Forms] prend désormais en charge les protocoles SMB 2 et SMB 3.

#### Mise en cache améliorée pour les pages de formulaires adaptatifs traduites (6.5.6.0) {#enhanced-caching-translated-adaptive-forms}

Vous pouvez désormais spécifier [locale comme sélecteur dans l’URL du formulaire adaptatif au lieu d’un argument dans l’URL du formulaire adaptatif](../../help/forms/using/supporting-new-language-localization.md). Cela permet de mettre en cache les formulaires adaptatifs traduits sur [!DNL Experience Manager Dispatcher]. La mise en cache du formulaire adaptatif traduit n’était pas possible dans les versions précédentes. Pour plus d’informations sur la configuration de la mise en cache pour l’utilisation des paramètres régionaux comme sélecteur dans l’URL du formulaire adaptatif, voir [Configuration du cache de formulaire adaptatif à Dispatcher](../../help/forms/using/configure-adaptive-forms-cache.md).

#### Enregistrer la sortie du service de modèle de données de formulaire dans une variable (6.5.6.0) {#save-fdm-service-to-variable}

Le modèle de données de formulaire vous permet d’enregistrer la sortie d’un service de modèle de données de formulaire dans une variable. [!DNL Experience Manager Forms] mappe désormais automatiquement le type du service de modèle de données de formulaire au type de variable .

#### Joindre plusieurs fichiers pour le composant Pièce jointe (6.5.6.0) {#attach-multiple-files}

Vous pouvez désormais [joindre plusieurs fichiers](../../help/forms/using/introduction-forms-authoring.md) au [!UICONTROL Pièce jointe] du composant des formulaires adaptatifs.

#### Personnalisation des colonnes de la boîte de réception Adobe Experience Manager (6.5.5.0) {#customize-aem-inbox-columns}

Vous pouvez personnaliser une [!DNL Experience Manager] Boîte de réception permettant de modifier le titre par défaut d’une colonne, de réorganiser la position d’une colonne et d’afficher des colonnes supplémentaires en fonction des données d’un workflow. Membres de `administrators` ou `workflow-administrators` peut personnaliser les colonnes. Pour plus d’informations, voir [Contrôle d’administration](../sites-authoring/inbox.md#inbox-admin-control).

![Personnalisation des colonnes de la boîte de réception du Experience Manager](assets/customize-columns.gif)

#### Enregistrement des communications interactives en tant que brouillon (6.5.5.0) {#save-as-draft}

Vous pouvez utiliser l’interface utilisateur de l’agent pour enregistrer un ou plusieurs brouillons pour chaque communication interactive et récupérer le brouillon ultérieurement pour continuer à travailler dessus. Vous pouvez spécifier un nom différent pour chaque brouillon afin de l’identifier. Pour plus d’informations, voir [Enregistrement des communications interactives en tant que brouillon](../forms/using/prepare-send-interactive-communication.md#save-as-draft).

![Enregistrer en tant que brouillon](assets/save-as-draft.gif)

#### [!DNL Oracle WebLogic] Prise en charge des serveurs d’applications (6.5.5.0) {#weblogic-support}

Adobe Experience Manager Forms a ajouté la prise en charge de [!DNL Oracle WebLogic 12] pour Adobe Experience Manager Forms on JEE. Vous pouvez effectuer une mise à niveau à partir d’une version précédente ou configurer un nouveau serveur Experience Manager 6.5 Forms on JEE sur [!DNL Oracle WebLogic] 12.2.1.4 et versions ultérieures. Plus tard correspond aux changements de version mineurs, où x dans la version 12.2.1.x est remplacé par un numéro de version.

#### Améliorations de l’accessibilité (6.5.5.0) {#accessibility-improvements}

Adobe Experience Manager Forms comprend les améliorations d’accessibilité suivantes :

* Lorsqu’un utilisateur prévisualise un formulaire adaptatif en tant que formulaire de HTML, la variable [!UICONTROL Signature tactile] conserve le focus de l’onglet.

* Les messages d’erreur affichés lors de l’envoi d’un formulaire adaptatif contiennent désormais le `aria-describedBy` attribut. L&#39;attribut est attaché aux champs référencés dans le message d&#39;erreur. Le `aria-describedby` indique les identifiants des éléments qui décrivent l’objet. Cela permet d’établir une relation entre les widgets ou les groupes et le texte qui les décrit.

* Si un formulaire adaptatif comporte des champs obligatoires, l’attribut obligatoire est défini sur `True` pour ces champs dans le schéma d’accessibilité ARIA.

#### Authentification par certificat X-509 pour les services web SOAP dans le modèle de données de formulaire (6.5.5.0) {#x509-based-authentication-soap}

Le modèle de données de formulaire prend désormais en charge l’authentification par certificat X-509 lors de l’utilisation des services web SOAP comme source de données. Pour plus d’informations, voir [Configuration des services Web SOAP](../forms/using/configure-data-sources.md#configure-soap-web-services).

#### Autres améliorations clés (6.5.5.0) {#other-improvements}

* Experience Manager 6.5 Forms on JEE Document Security est désormais basé sur [!DNL Apache Struts 2].

* Ajout de la prise en charge de [!DNL Oracle Real Applications Cluster (RAC) 19c].

#### Générer une sortie imprimable dans les workflows Experience Manager Forms (6.5.4.0) {#generate-printable-output}

L’étape de workflow Générer une sortie imprimable permet d’intégrer un fichier de modèle source à un fichier de données. Cette intégration permet d&#39;imprimer ou d&#39;enregistrer différentes copies du fichier de modèle. L’étape génère une sortie PCL, PostScript, ZPL, IPL, TPCL ou DPL. Pour plus d’informations sur cette fonctionnalité, voir [Processus basé sur l’utilisation de Forms sur OSGi - Référence des étapes](../forms/using/aem-forms-workflow-step-reference.md).

![Générer une sortie imprimable](assets/generate-print-output-step.gif)

#### Prise en charge de plusieurs colonnes pour les formulaires adaptatifs et les communications interactives en mode Disposition (6.5.4.0) {#multi-column-adaptive-forms}

Vous pouvez désormais définir le nombre de colonnes d’un panneau dans les formulaires adaptatifs et les communications interactives. Passez en mode de mise en page pour utiliser la nouvelle option à plusieurs colonnes. Pour plus d’informations, voir [Utilisation du mode Mise en page pour redimensionner les composants](../forms/using/resize-using-layout-mode.md).

![Disposition multi-colonnes](assets/multi-column-layout.gif)

#### Personnalisations de la boîte de réception du Experience Manager (6.5.4.0) {#aem-inbox}

La nouvelle option de contrôle d’administration permet aux administrateurs de :

* Personnalisez le texte et le logo de l’en-tête.

* Contrôle l’affichage des liens de navigation disponibles dans l’en-tête.

L’option Contrôle d’administration n’est visible que par les membres de la variable `administrators` ou `workflow-administrators` groupe. Pour plus d’informations sur cette fonctionnalité, voir [Votre boîte de réception](../sites-authoring/inbox.md).

#### Prise en charge de texte enrichi dans les formulaires HTML5 (6.5.4.0) {#rich-text-support}

Convertissez un champ de texte d’un formulaire XFA en champ de texte enrichi dans un formulaire HTML5. Pour plus d’informations, voir [Conception de modèles de formulaire pour les formulaires HTML5](../forms/using/designing-form-template.md).

#### Améliorations de l’accessibilité (6.5.4.0) {#forms-accessibility-enhancements-6540}

Experience Manager Forms comprend les améliorations d’accessibilité suivantes :

* Les lecteurs d’écran annoncent correctement les cases à cocher, les liens, le sélecteur de date et les champs de saisie de date dans un formulaire adaptatif.

* Chaque page d’un formulaire adaptatif comprend désormais un titre et un libellé de repère principal.

#### Partage et demande l’accès aux éléments de boîte de réception d’un utilisateur Experience Manager Forms (6.5.3.0) {#share-request-access}

Vous pouvez partager vos éléments de boîte de réception avec un autre utilisateur. Une fois qu’un autre utilisateur a accès à vos éléments de boîte de réception, il peut demander et prendre les mesures appropriées sur les éléments partagés. De même, vous pouvez demander l’accès aux éléments de boîte de réception à d’autres utilisateurs. Voir [Partage et demande l’accès aux éléments de boîte de réception d’un utilisateur](../forms/using/configure-shared-queues-osgi.md).

#### Configuration des paramètres d’absence du bureau pour les éléments de boîte de réception d’un utilisateur Experience Manager Forms (6.5.3.0) {#configure-out-of-office}

Si vous envisagez de vous absenter du bureau, vous pouvez spécifier les actions à entreprendre pour les tâches qui vous sont affectées pendant cette période.
Vous pouvez spécifier une date et une heure de début, ainsi qu’une date et une heure de fin, pour l’application de vos paramètres d’absence du bureau. Vous pouvez définir une personne par défaut à qui tous vos éléments sont envoyés. Voir [Configuration des paramètres d’absence du bureau](../forms/using/configure-out-of-office-settings.md).

#### Générer plusieurs communications interactives à l’aide de l’API Batch pour Experience Manager Forms (6.5.3.0) {#generate-multiple-ic}

Vous pouvez utiliser l’API Batch pour produire plusieurs communications interactives à partir d’un modèle. Le modèle est une communication interactive sans données. L’API Batch combine des données à un modèle afin de produire une communication interactive. L’API est utile pour la production en masse de communications interactives. Par exemple, les factures de téléphone, les relevés de carte de crédit pour plusieurs clients. Voir [Génération de plusieurs communications interactives à l’aide de l’API Batch](../forms/using/generate-multiple-interactive-communication-using-batch-api.md).

<!-- TBD: Check if the wider team released anything in FY21.
-->

## Versions clés depuis [!DNL Adobe Experience Manager] 6.5 SP10{#key-releases-since-last-sp}

Entre le 26 août 2021 et le 25 novembre 2021, Adobe a publié les éléments suivants, en plus des Service Packs :

* [!DNL Adobe Experience Manager] as a Cloud Service [2021.9.0](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/2021/release-notes-2021-9-0.html) et [2021.10.0](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=fr).

* [[!DNL Experience Manager] application de bureau 2.1 (2.1.3.4)](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html).

* [Experience Manager Screens : Feature Pack 202109](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/release-notes/release-notes-fp-202109.html?lang=fr)

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] Documentation 6.5](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=fr)
>* [Notes de mise à jour générales pour [!DNL Experience Manager] 6,5](release-notes.md)
>* [Notes de mise à jour du Service Pack pour [!DNL Experience Manager] 6,5](sp-release-notes.md)

