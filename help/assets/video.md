---
title: Vidéo dans Dynamic Media
description: Découvrez comment utiliser la vidéo dans Dynamic Media, notamment les bonnes pratiques pour le codage vidéo, l’ajout de plusieurs sous-titres et pistes audio aux vidéos et les miniatures vidéo.
mini-toc-levels: 3
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
feature: Asset Management
role: User, Admin
exl-id: 28cf9e39-cab4-4278-b6c9-e84cc31964db
solution: Experience Manager, Experience Manager Assets
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '10481'
ht-degree: 99%

---

# Vidéo dans Dynamic Media {#video}

Cette section décrit l’utilisation de vidéos dans Dynamic Media.

## Démarrage rapide : vidéos {#quick-start-videos}

Le processus détaillé décrit ci-après vise à vous aider à maîtriser rapidement les opérations liées aux visionneuses de vidéos adaptatives dans Dynamic Media. Chaque étape comporte des renvois à des rubriques contenant de plus amples informations.

>[!IMPORTANT]
>
>Assurez-vous que votre administrateur ou administratrice Adobe Experience Manager a activé et configuré les services cloud Dynamic Media en mode Dynamic Media - Scene7 ou hybride avant d’utiliser des vidéos dans Dynamic Media.
>
>* Consultez la section [Configuration des services cloud Dynamic Media](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services) dans Configuration de Dynamic Media en mode Scene7 et [Dépannage de Dynamic Media en mode Scene7](/help/assets/troubleshoot-dms7.md).
>
>* Consultez la section [Configuration des services cloud Dynamic Media](/help/assets/config-dynamic.md#configuring-dynamic-media-cloud-services) dans Configuration de Dynamic Media en mode hybride.
>
>Problème de lecture vidéo actuellement connu dans Dynamic Media *sur Experience Manager 6.5.9.0 uniquement* :
>
>* Si une vidéo publiée est mise à jour, elle doit être publiée à nouveau pour refléter les modifications apportées à la diffusion.
>

1. **Chargez les vidéos Dynamic Media** en procédant comme suit :

   * Créez votre propre profil de codage vidéo. Vous pouvez également utiliser le profil _Codage vidéo adaptif_ prédéfini fourni avec Dynamic Media.

      * [Création d’un profil de codage vidéo](/help/assets/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming).
      * La résolution maximale du codage vidéo de sortie est de 8 192 × 4 320 ou de 4 320 × 8 192.md.
      * En savoir plus sur les [bonnes pratiques relatives au codage vidéo](#best-practices-for-encoding-videos).

   * Associez le profil de traitement vidéo à un ou plusieurs dossiers dans lequel vous allez charger les vidéos issues de sources originales.

      * [Application d’un profil vidéo à des dossiers](/help/assets/video-profiles.md#applying-a-video-profile-to-folders).
      * En savoir plus sur les [bonnes pratiques relatives à l’organisation des ressources numériques en vue de l’utilisation de profils de traitement](/help/assets/organize-assets.md).
      * En savoir plus sur l’[organisation des ressources numériques](/help/assets/organize-assets.md).

   * Chargez les vidéos issues de sources originales dans les dossiers. Lorsque vous ajoutez des vidéos au dossier, elles sont codées selon le profil de traitement vidéo affecté au dossier.

      * Dynamic Media prend principalement en charge les vidéos courtes avec une durée maximale de 30 minutes et une résolution minimale supérieure à 25 x 25.
      * La résolution vidéo d’entrée maximale prise en charge est de 16 384 × 16 384.
      * Vous pouvez charger des fichiers vidéo d’une taille de 15 Go chacun au maximum.
      * [Chargement des vidéos](/help/assets/managing-video-assets.md#upload-and-preview-video-assets).
      * En savoir plus sur les [formats de fichiers d’entrée pris en charge](/help/assets/assets-formats.md#supported-multimedia-formats).

   * Surveillez [la progression du codage vidéo](#monitoring-video-encoding-and-youtube-publishing-progress) depuis la vue de la ressource ou du workflow.

1. Pour **gérer les vidéos Dynamic Media**, effectuez l’une des opérations suivantes :

   * Organisez, parcourez et recherchez des ressources vidéo

      * [Organisation des ressources numériques](/help/assets/organize-assets.md)
En savoir plus sur les [bonnes pratiques relatives à l’organisation des ressources numériques en vue de l’utilisation de profils de traitement](organize-assets.md)

      * [Recherche de ressources vidéo](search-assets.md#custompredicates) ou [Recherche de ressources](/help/assets/search-assets.md)

   * Prévisualisez et publiez des ressources vidéo

      * Affichez la vidéo source et les rendus codés de la vidéo avec les miniatures associées :
        [Prévisualisation de vidéos](managing-video-assets.md#upload-and-preview-video-assets) ou [Prévisualisation de ressources](previewing-assets.md)
        [Affichage des rendus vidéo](video-renditions.md)
        [Gestion des rendus vidéo](manage-assets.md#managing-renditions)

      * [Gestion des paramètres prédéfinis de visionneuse](managing-viewer-presets.md)
      * [Publication de ressources](publishing-dynamicmedia-assets.md)

   * Utilisation des métadonnées vidéo

      * Affichez les propriétés d’un rendu vidéo codé telles que la fréquence d’image, le débit vidéo et audio et le codec :
        [Affichage des propriétés de rendu vidéo](video-renditions.md)

      * Modifiez les propriétés vidéo telles que le titre, la description, les balises et les champs de métadonnées personnalisées :
        [Modification des propriétés vidéo](manage-assets.md#editing-properties)

      * [Gestion des métadonnées des ressources numériques](metadata.md)
      * [Schémas de métadonnées](metadata-schemas.md)

   * Examen, approbation et annotation des vidéos, et conservation le contrôle total des versions

      * [Annotation de vidéos](managing-video-assets.md#annotate-video-assets) ou [Annotation de ressources](manage-assets.md#annotating)

      * [Créer une version](manage-assets.md#asset-versioning)
      * [Application de workflows aux ressources](assets-workflow.md) ou [Démarrage d’un workflow sur une ressource](manage-assets.md#starting-a-workflow-on-an-asset)

      * [Examen des ressources des dossiers](bulk-approval.md)
      * [Projets](../sites-authoring/projects.md)

1. Pour **publier les vidéos Dynamic Media**, effectuez l’une des opérations suivantes :

   * Si vous utilisez Adobe Experience Manager en tant que système de gestion de contenu web, vous pouvez ajouter directement des vidéos à vos pages web.

      * [Ajout de vidéos à des pages web](adding-dynamic-media-assets-to-pages.md).

   * Si vous utilisez un système de gestion de contenu web tiers, vous pouvez lier ou incorporer des vidéos dans vos pages web.

      * Intégrez une vidéo à l’aide d’une URL :
        [Liaison d’URL à votre application web](linking-urls-to-yourwebapplication.md).

      * Intégrez une vidéo à l’aide du code intégré dans la page web :
        [Incorporation de la visionneuse de vidéos dans une page web](embed-code.md).

   * [Génération de rapports vidéo](#viewing-video-reports).

   * [Ajout de sous-titres à une vidéo](#adding-captions-to-video).

## Utilisation de vidéo dans Dynamic Media {#working-with-video-in-dynamic-media}

Video in Dynamic Media est une solution complète qui facilite la publication de vidéos adaptatives haute qualité pour la diffusion sur plusieurs écrans, notamment les postes de travail et les appareils mobiles iOS, Android™, BlackBerry® et Windows. Une visionneuse de vidéos adaptative regroupe les versions d’une même vidéo codées dans des débits et des formats différents, par exemple 400 kbit/s, 800 kbit/s et 1 000 kbit/s. Le poste de travail ou l’appareil mobile détecte la bande passante disponible.

Par exemple, sur un appareil mobile iOS, il détecte une bande passante telle que 3G, 4G ou une connexion Wi-Fi, puis sélectionne automatiquement la vidéo codée selon le débit correspondant parmi ceux disponibles dans la visionneuse de vidéos adaptative. La vidéo est diffusée en continu sur les postes de travail, les appareils mobiles ou les tablettes.

En outre, la qualité de la vidéo s’adapte de manière automatique et dynamique aux fluctuations des conditions du réseau sur le poste de travail ou sur l’appareil mobile. De même, si un client ou une cliente passe en mode plein écran sur un bureau, la visionneuse de vidéos adaptative réagit en utilisant une meilleure résolution, améliorant ainsi l’expérience de visionnage. Les visionneuses de vidéos adaptatives garantissent une lecture optimale pour les clientes et clients qui regardent des vidéos Dynamic Media sur plusieurs écrans et appareils.

La logique utilisée par un lecteur vidéo pour déterminer la vidéo codée à lire ou à sélectionner au cours de la lecture repose sur l’algorithme suivant :

1. Le lecteur vidéo charge le fragment vidéo initial en fonction du débit le plus proche de la valeur définie pour le « débit initial » dans le lecteur.
1. Le lecteur vidéo change en fonction des modifications de la vitesse de bande passante à l’aide des critères suivants :

   1. Le lecteur sélectionne la bande passante la plus élevée, inférieure ou égale à la bande passante estimée.
   1. Le lecteur prend uniquement en compte 80 % de la bande passante disponible. Cependant, s’il change, il est préférable que ce taux soit seulement de 70 % pour éviter toute surestimation et que le lecteur ne repasse au taux précédent.

Pour obtenir des informations techniques détaillées sur l’algorithme, consultez la page [https://android.googlesource.com/platform/frameworks/av/+/master/media/libstagefright/httplive/LiveSession.cpp](https://android.googlesource.com/platform/frameworks/av/+/master/media/libstagefright/httplive/LiveSession.cpp)

Pour la gestion des visionneuses de vidéos à débit adaptatif et uniques, les fonctions suivantes sont prises en charge :

* Chargez des vidéos dans divers formats pris en charge et codez-les au format MP4 H.264 pour les lire sur plusieurs écrans. Vous pouvez utiliser des paramètres prédéfinis de vidéo adaptative, des paramètres prédéfinis de codage vidéo unique ou personnaliser votre propre codage pour contrôler la qualité et la taille de la vidéo.

   * Lorsqu’une visionneuse de vidéos adaptative est générée, elle comprend des vidéos MP4.
   * **Remarque** : Les vidéos originales/sources ne sont pas ajoutées à la visionneuse de vidéos adaptative.

* Sous-titrage vidéo dans toutes les visionneuses de vidéos HTML5.
* Organisez, parcourez et recherchez des vidéos avec une prise en charge complète des métadonnées pour une gestion efficace des ressources vidéo.
* Proposez des visionneuses de vidéos adaptatives en ligne ainsi que sur des postes de travail et des appareils mobiles (iPhone, iPad, Android™, BlackBerry® et Windows Phone notamment).

La diffusion de vidéo adaptative en continu est prise en charge sur différentes plateformes iOS. Voir [Guide de référence des visionneuses de médias dynamiques](https://experienceleague.adobe.com/fr/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/c-html5-video-reference#video).

Dynamic Media prend en charge la lecture vidéo mobile pour la vidéo MP4 H.264. <!-- LINK IS 404 WITH NO SUITABLE REPLACEMENT You can find BlackBerry&reg; devices that support this video format at the following: [Supported video formats on BlackBerry&reg;](https://support.blackberry.com/kb/articleDetail?ArticleNumber=000005482). -->

Les appareils Windows qui prennent en charge ce format vidéo sont répertoriés dans la liste : [Médias pris en charge sur Windows Phone 8](https://learn.microsoft.com/fr-fr/windows/uwp/audio-video-camera/supported-codecs)

* Lecture de la vidéo à l’aide des paramètres prédéfinis de la visionneuse Dynamic Media Video, tels que :

   * Visionneuses de vidéos uniques.
   * des visionneuses de médias mixtes combinant du contenu vidéo et des images.

* Configurez les lecteurs vidéo pour répondre à vos besoins en matière de branding.
* Intégrez la vidéo à votre site Web ou mobile, ou à votre application mobile à l’aide d’une simple URL ou d’un code intégré.

<!-- See [Dynamic video playback](https://s7d9.scene7.com/s7/uvideo.jsp?asset=GeoRetail/Mop_AVS&config=GeoRetail/Universal_Video1&stageSize=640,480) sample. -->

Consultez également la section [Visionneuses pour Experience Manager Assets et Dynamic Media Classic](https://experienceleague.adobe.com/fr/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/c-html5-s7-aem-asset-viewers#viewers-aem-assets-dmc) et [Visionneuses pour Experience Manager Assets uniquement](https://experienceleague.adobe.com/fr/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/c-html5-aem-asset-viewers#viewers-for-aem-assets-only).

## Bonne pratique : utilisation de la visionneuse de vidéos HTML5 {#best-practice-using-the-html-video-viewer}

Les paramètres prédéfinis de la visionneuse de vidéos Dynamic Media HTML5 sont des lecteurs vidéo fiables. Vous pouvez les utiliser pour éviter de nombreux problèmes courants liés à la lecture des vidéos HTML5. De plus, ils minimisent également les problèmes liés aux appareils mobiles, comme l’absence de diffusion en continu à débit adaptatif et une portée limitée du navigateur de bureau.

En ce qui concerne la conception du lecteur, vous pouvez créer des fonctionnalités à l’aide d’outils de développement Web standard. Par exemple, vous pouvez concevoir les boutons, les commandes et l’arrière-plan personnalisé de l’image d’affiche en utilisant HTML5 et CSS pour vous aider à atteindre vos clients et vos clientes à l’aide d’une apparence personnalisée.

En ce qui concerne la relecture, la visionneuse détecte automatiquement les fonctionnalités vidéo du navigateur. Elle diffuse ensuite la vidéo en utilisant HLS (HTTP Live Streaming) ou DASH (Dynamic Adaptive Streaming over HTTP), également appelé diffusion en continu à débit adaptatif. Si ces méthodes de distribution n’existent pas, la diffusion progressive HTML5 est utilisée à la place.

En combinant dans un seul lecteur, vous avez accès aux les éléments suivants :

* La possibilité de concevoir des composants de lecture à l’aide de HTML5 et CSS
* Disposer de lecteurs incorporés
* Utiliser la diffusion en continu à débit adaptatif et progressive adaptée aux fonctionnalités du navigateur

Vous pouvez étendre la portée de votre contenu multimédia aux utilisateurs et utilisatrices d’ordinateurs de bureau et d’appareils mobiles et garantir ainsi une expérience vidéo fluide.

Consultez également la section [A propos des visionneuses HTML5](https://experienceleague.adobe.com/fr/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/c-html5-aem-asset-viewers#viewers-for-aem-assets-only).

### Lecture vidéo sur les ordinateurs de bureau et les appareils mobiles à l’aide de la visionneuse de vidéos HTML5 {#playback-of-video-on-desktop-computers-and-mobile-devices-using-the-html-video-viewer}

Pour la diffusion en flux continu de la vidéo à débit adaptatif sur un poste de travail et un appareil mobile, les vidéos utilisées pour le changement de débit reposent sur toutes les vidéos MP4 dans la visionneuse de vidéos à débit adaptatif.

La lecture vidéo se produit à l’aide d’un téléchargement vidéo DASH, HLS ou progressif. Dans les versions antérieures d’Experience Manager, telles que 6.0, 6.1 et 6.2, les vidéos étaient diffusées via HTTP.

Toutefois, dans la version 6.3 et les versions ultérieures d’Experience Manager, les vidéos sont diffusées en continu via HTTPS (c’est-à-dire, DASH ou HLS), car l’URL du service de la passerelle DM utilise toujours HTTPS également. Il n’y a aucun impact pour le client ou la cliente dans ce comportement par défaut. La diffusion en continu de vidéo s’effectue toujours via HTTPS, sauf lorsque le navigateur ne la prend pas en charge. (Voir le tableau ci-dessous). Par conséquent :

* Si vous disposez d’un site Web HTTPS avec streaming vidéo HTTPS, le streaming est correct.
* Si vous disposez d’un site Web HTTP avec streaming vidéo HTTPS, le streaming est correct et il n’y a aucun problème de contenu mixte à partir du navigateur Web.

DASH est la norme internationale et HLS est une norme Apple. Les deux sont utilisés pour la diffusion en continu de vidéo adaptative. De plus, les deux technologies ajustent automatiquement la relecture en fonction de la capacité de bande passante du réseau. Elle permet aussi au client ou à la cliente de « rechercher » n’importe quel point de la vidéo sans avoir à attendre que le reste de la vidéo soit téléchargé.

La vidéo progressive est fournie grâce au téléchargement et à l’enregistrement de la vidéo en local sur le système du poste de travail ou de l’appareil mobile de l’utilisateur ou de l’utilisatrice.

Le tableau ci-dessous décrit l’appareil, le navigateur et la méthode de lecture des vidéos sur les ordinateurs de bureau et les appareils mobiles à l’aide de la visionneuse de vidéos Dynamic Media.

<table>
 <tbody>
  <tr>
   <td><strong>Appareil</strong></td>
   <td><strong>Navigateur</strong></td>
   <td><strong>Mode lecture vidéo</strong></td>
  </tr>
  <tr>
   <td>Poste de travail</td>
   <td>Internet Explorer 9 et 10</td>
   <td>Téléchargement progressif.</td>
  </tr>
  <tr>
   <td>Poste de travail</td>
   <td>Internet Explorer 11+</td>
   <td>Sous Windows 8 et Windows 10 – Forcer l’utilisation de HTTPS chaque fois que DASH* ou HLS est demandé. Limites connues : HTTP sur DASH* ou HLS ne fonctionne pas avec cette combinaison de navigateur/système d’exploitation<br /> <br /> Sous Windows 7 - Téléchargement progressif. Utilise la logique standard pour sélectionner le protocole HTTP ou HTTPS.</td>
  </tr>
  <tr>
   <td>Poste de travail</td>
   <td>Firefox 23-44</td>
   <td>Téléchargement progressif.</td>
  </tr>
  <tr>
   <td>Poste de travail</td>
   <td>Firefox 45 ou version ultérieure</td>
   <td>Diffusion en continu à débit adaptatif DASH* ou HLS.</td>
  </tr>
  <tr>
   <td>Poste de travail</td>
   <td>Chrome</td>
   <td>Diffusion en continu à débit adaptatif DASH* ou HLS.</td>
  </tr>
  <tr>
   <td>Poste de travail</td>
   <td>Safari (Mac)</td>
   <td>Diffusion en continu à débit adaptatif HLS.</td>
  </tr>
  <tr>
   <td>Mobile</td>
   <td>Chrome (Android™ 6 ou version antérieure)</td>
   <td>Téléchargement progressif.</td>
  </tr>
  <tr>
   <td>Mobile</td>
   <td>Chrome (Android™ 7 ou version ultérieure)</td>
   <td>Diffusion en continu à débit adaptatif DASH* ou HLS.</td>
  </tr>
  <tr>
   <td>Mobile</td>
   <td>Android™ (navigateur par défaut)</td>
   <td>Téléchargement progressif.</td>
  </tr>
  <tr>
   <td>Mobile</td>
   <td>Safari (iOS)</td>
   <td>Diffusion en continu à débit adaptatif HLS.</td>
  </tr>
  <tr>
   <td>Mobile</td>
   <td>Chrome (iOS)</td>
   <td>Diffusion en continu à débit adaptatif HLS.</td>
  </tr>
  <tr>
   <td>Mobile</td>
   <td>BlackBerry®</td>
   <td>Diffusion en continu à débit adaptatif DASH* ou HLS./td&gt;
  </tr>
 </tbody>
</table>

## Architecture de la solution vidéo Dynamic Media {#architecture-of-dynamic-media-video-solution}

Le graphique suivant montre le workflow global de création de vidéos qui sont chargées et codées par le biais de DMGateway (dans le mode Hybride Dynamic Media) et mises à disposition pour une consommation publique.

![Architecture de la solution vidéo Dynamic Media.](assets/chlimage_1-427.png)

## Architecture de publication hybride des vidéos {#hybrid-publishing-architecture-for-videos}

![Architecture de publication hybride des vidéos.](assets/chlimage_1-428.png)

## Bonnes pratiques en matière de codage de vidéos {#best-practices-for-encoding-videos}

Le processus **Vidéo d’encodage Dynamic Media** encode la vidéo si vous avez activé Dynamic Media et configuré les services cloud vidéo. Ce workflow capture l’historique de traitement des workflows et les informations d’échec. Si vous avez activé Dynamic Media et configuré les services cloud vidéo, le workflow **[!UICONTROL Vidéo d’encodage Dynamic Media]** prend automatiquement effet lorsque vous chargez une vidéo. (Si vous n’utilisez pas Dynamic Media, le workflow **[!UICONTROL Ressource de mise à jour DAM]** prend effet.)

<!-- DEAD The following are best-practice tips for encoding source video files.

For advice about video encoding, see [Video Encoding Basics](https://www.adobe.com/go/learn_s7_encoding_en).

* [Streaming 101: The Basics — Codecs, Bandwidth, Data Rate, and Resolution](https://www.adobe.com/go/learn_s7_streaming101_en). -->

### Fichiers vidéo source {#source-video-files}

Lorsque vous codez un fichier vidéo, utilisez un fichier vidéo source de la plus haute qualité possible. Évitez d’utiliser des fichiers vidéo déjà codés, car ces fichiers sont déjà compressés, et un codage supplémentaire crée une vidéo de qualité inférieure.

* Dynamic Media prend principalement en charge les vidéos courtes avec une durée maximale de 30 minutes et une résolution minimale supérieure à 25 x 25.
* Vous pouvez charger des fichiers vidéo de source principale d’une taille de 15 Go chacun au maximum.

Le tableau ci-dessous décrit la taille recommandée, le format et le débit minimal requis pour vos fichiers vidéo sources au moment de leur codage :

| Taille | Format | Débit minimal |
|--- |--- |--- |
| 1 024 × 768 | 4:3 | 4 500 Kbit/s pour la plupart des vidéos. |
| 1 280 × 720 | 16 :9 | 3 000 à 6 000 Kbit/s, selon la quantité de mouvement dans la vidéo. |
| 1 920 × 1 080 | 16 :9 | 6 000 à 8 000 kbit/s, selon la quantité de mouvement dans la vidéo. |

### Obtention des métadonnées d’un fichier {#obtaining-a-file-s-metadata}

Vous pouvez récupérer les métadonnées d’un fichier à l’aide d’un outil de montage vidéo ou d’une application dédiée. Vous trouverez ci-dessous les instructions pour récupérer les métadonnées d’un fichier vidéo à l’aide de l’application tierce MediaInfo :

1. Accédez à [Téléchargement MediaInfo](https://mediaarea.net/fr/MediaInfo/Download).
1. Sélectionnez et téléchargez le programme d’installation pour la version avec l’interface graphique utilisateur, puis suivez les instructions d’installation.
1. Après l’installation, cliquez avec le bouton droit sur le fichier vidéo (Windows uniquement) et sélectionnez MediaInfo, ou bien ouvrez MediaInfo et faites glisser votre fichier vidéo dans l’application. Toutes les métadonnées de votre fichier vidéo, telles que sa largeur, sa hauteur et le nombre d’images par seconde, sont alors visibles à l’écran.

### Format {#aspect-ratio}

Lors de la sélection ou de la création d’un paramètre prédéfini de codage vidéo pour votre fichier vidéo principal, assurez-vous que le format du paramètre prédéfini correspond à celui du fichier vidéo principal. Le format fait référence au rapport largeur/hauteur de la vidéo.

Pour déterminer le format d’un fichier vidéo, récupérez les métadonnées de ce fichier et notez les valeurs de largeur et de hauteur. Voir Obtention des métadonnées d’un fichier ci-dessus. Utilisez ensuite cette formule pour déterminer le format :

largeur/hauteur = format

Le tableau suivant décrit comment les résultats de la formule se traduisent par des choix de format courants :

| Résultat de la formule | Format |
|--- |--- |
| 1,33 | 4:3 |
| 0,75 | 3:4 |
| 1,78 | 16 :9 |
| 0,56 | 9:16 |

Par exemple, une vidéo d’une largeur de 1 440 × d’une hauteur de 1 080 a un format de 1 440/1 080, soit 1,33. Dans ce cas, vous choisissez un paramètre prédéfini de codage vidéo avec un format de 4:3 pour coder le fichier vidéo.

### Débit binaire {#bitrate}

Le débit correspond à la quantité de données encodées pour produire une seule seconde de lecture vidéo. Le débit de données est mesuré en kilobits par seconde (kbit/s).

>[!NOTE]
>
>Du fait que tous les codecs utilisent la compression avec perte, le débit de données est le facteur le plus important de la qualité vidéo. Quand vous utilisez la compression avec perte, plus vous compressez la vidéo, plus la qualité de l’image se dégrade. Pour cette raison, toutes les autres caractéristiques étant égales (résolution, débit d’image et codec), plus le débit est faible, plus la qualité du fichier compressé est faible.

Lors de la sélection d’une vitesse de transmission, vous pouvez choisir deux types :

* **[!UICONTROL Encodage à débit constant]** (CBR) : pendant l’encodage CBR, le débit ou le nombre de bits par seconde est conservé pendant tout le processus d’encodage. L’encodage CBR maintient le débit défini selon votre configuration sur l’intégralité de la vidéo. En outre, le codage CBR n’optimise pas la qualité des fichiers multimédias, mais économise de l’espace de stockage.
Utilisez le codage CBR si votre vidéo présente globalement un niveau de mouvement similaire. Le codage CBR est le plus souvent utilisé pour diffuser le contenu vidéo en continu. Voir également [Utilisation de paramètres de codage vidéo personnalisés](/help/assets/video-profiles.md#using-custom-added-video-encoding-parameters).

* **[!UICONTROL Codage à débit variable]** (VBR) - le codage VBR règle le débit en le diminuant et en l’augmentant selon la limite supérieure que vous avez définie, en fonction des données demandées par le compresseur. Cette fonctionnalité implique que lors d’un processus de codage VBR, le débit du fichier multimédia augmente ou diminue de manière dynamique en fonction des besoins du débit de fichiers multimédias.
Le VBR prend plus de temps au codage, mais garantit de meilleurs résultats, avec une qualité de fichier multimédia supérieure. Le codage VBR est couramment utilisé pour la diffusion http progressive de contenu vidéo.

Dans quels cas utilisez-vous le VBR ou le CBR ?
Lorsque vous devez choisir entre VBR et CBR, il est presque toujours recommandé d’utiliser le VBR pour vos fichiers multimédias. Le VBR vous garantit des fichiers de meilleure qualité à des débits compétitifs. Lorsque vous utilisez le VBR, assurez-vous d’utiliser le codage à deux passages, et définissez le débit maximal afin qu’il soit 1,5 fois supérieur au débit vidéo cible.

Lorsque vous choisissez un paramètre prédéfini de codage vidéo, tenez compte de la vitesse de connexion de votre audience. Choisissez un paramètre prédéfini avec un débit de données correspondant à 80 % de cette vitesse. Par exemple, si la vitesse de connexion de l’utilisateur ou de l’utilisatrice finale est de 1 000 kbit/s, le meilleur paramètre prédéfini est celui qui comprend un débit vidéo de 800 kbit/s.

Ce tableau décrit le débit de données associé à des vitesses de connexion courantes.

| Vitesse (kbit/s) | Type de connexion |
|--- |--- |
| 256 | Connexion d’accès à distance. |
| 800 | Connexion mobile standard. Pour cette connexion, visez un débit de données de 400 à 800 kbit/s pour les expériences 3G. |
| 2000 | Connexion haut débit standard de bureau. Pour cette connexion, visez un débit de données de 800 à 2 000 kbit/s, bien qu’un débit de 1 200 à 1 500 kbit/s convienne à la plupart des cibles. |
| 5000 | Connexion haut débit standard. Il est déconseillé de coder dans la plage supérieure, car la diffusion vidéo à cette vitesse n’est pas disponible pour la plupart des consommateurs et des consommatrices. |

### Résolution {#resolution}

La **résolution** décrit la hauteur et la largeur d’un fichier vidéo, exprimée en pixels. La plupart des vidéos sources sont stockées en haute résolution (par exemple, 1 920 × 1 080). À des fins de diffusion en continu, la vidéo source est compressée à une résolution inférieure (640 × 480 ou moins).

La résolution et le débit de données sont deux facteurs étroitement liés qui déterminent la qualité de la vidéo. Pour maintenir la même qualité vidéo, plus il y a de pixels dans un fichier vidéo (plus la résolution est élevée), plus le débit de données doit être élevé. Prenons l’exemple du nombre de pixels par image dans un fichier vidéo de résolution 320 x 240 et de résolution 640 x 480 :

| Résolution | Pixels par image |
|--- |--- |
| 320 x 240 | 76 800 |
| 640 × 480 | 307 200 |

Le fichier 640 x 480 a quatre fois plus de pixels par image. Pour obtenir le même débit de données pour ces deux exemples de résolution, vous compressez quatre fois le fichier 640 x 480, ce qui peut réduire la qualité de la vidéo. Par conséquent, un débit de données vidéo de 250 kbit/s produit un affichage de haute qualité à une résolution de 320 x 240 pixels, mais pas à une résolution de 640 x 480 pixels.

En général, plus le débit de données que vous utilisez est élevé, plus la qualité de votre vidéo est bonne, et plus vous utilisez une résolution élevée, plus de débit de données dont vous avez besoin est élevé pour conserver la qualité de visionnage (en comparaison avec des résolutions plus basses).

Du fait que la résolution et le débit de données sont liés, vous avez le choix entre deux options lors du codage vidéo :

* Choisissez un débit de données, puis codez à la résolution la plus haute pour obtenir une vidéo de bonne qualité.
* Choisir une résolution, puis coder au débit de données nécessaire pour que la qualité vidéo soit optimale à la résolution choisie.

Lorsque vous choisissez (ou créez) un paramètre prédéfini de codage vidéo pour votre fichier vidéo source original, utilisez ce tableau pour choisir la résolution cible appropriée :

| Résolution | Hauteur (pixels) | Taille de l’écran |
|--- |--- |--- |
| 240p | 240 | Tout petit écran |
| 300p | 300 | Petit écran (appareils mobiles, le plus souvent) |
| 360p | 360 | Petit écran |
| 480p | 480 | Écran moyen |
| 720p | 720 | Grand écran |
| 1 080p | 1080 | Grand écran haute définition |

La résolution vidéo d’entrée maximale prise en charge est de 16 384 × 16 384. La résolution maximale du codage vidéo de sortie est de 8 192 × 4 320 ou de 4 320 × 8 192.

### Images par seconde {#fps-frames-per-second}

Aux États-Unis et au Japon, la plupart des vidéos sont enregistrées à 29,97 images par seconde (i/s). En Europe, la norme est de 25 i/s. Un film, en revanche, est généralement tourné à 24 i/s.

Choisissez un paramètre prédéfini de codage vidéo correspondant au nombre d’images par seconde de votre vidéo issue de sources originales. Par exemple, si le débit est de 25 ips pour la vidéo issue de sources originales, choisissez un paramètre prédéfini de 25 ips pour le codage. Par défaut, tous les codages personnalisés utilisent le nombre d’images par seconde de la vidéo issue de sources originales. C’est pourquoi il est inutile d’indiquer le nombre d’images par seconde lorsque vous créez un paramètre prédéfini de codage vidéo.

### Dimensions du codage vidéo {#video-encoding-dimensions}

Pour des résultats optimaux, sélectionnez des dimensions de codage de manière à ce que la vidéo source soit un multiple entier de toutes vos vidéos codées.

Pour ce faire, il suffit de diviser la largeur de la source par la largeur codée pour obtenir le rapport de largeur, Ensuite, vous divisez la hauteur source par la hauteur codée pour obtenir le rapport de hauteur.

Si le résultat est un nombre entier, cela signifie que la mise à l’échelle de la vidéo est optimale. Si le résultat n’est pas un nombre entier, la qualité vidéo s’en ressentira en raison de la présence d’artefacts vidéo (pixels résiduels). Cet effet est plus visible lorsque la vidéo comporte du texte.

Par exemple, supposons que la vidéo source soit en 1 920 x 1 080. Dans le tableau suivant, les trois vidéos codées fournissent les paramètres de codage optimaux à utiliser.

| Type de vidéo | Largeur/Hauteur | Rapport largeur | Rapport de hauteur |
|--- |--- |--- |--- |
| Source | 1 920 × 1 080 | 1 | 1 |
| Codé | 960 × 540 | 2 | 2 |
| Codé | 640 × 360 | 3 | 3 |
| Codé | 480 × 270 | 4 | 4 |

### Format de fichier vidéo codé {#encoded-video-file-format}

Dynamic Media recommande d’utiliser les paramètres prédéfinis MP4 H.264 de codage vidéo. Comme les fichiers MP4 utilisent le codec vidéo H.264, une vidéo de haute qualité est obtenue, mais avec une taille de fichier compressée.

## Affichage des rapports vidéo {#viewing-video-reports}

>[!NOTE]
>
>Les rapports vidéo sont disponibles uniquement lorsque vous exécutez Dynamic Media en mode Hybride.

Les rapports vidéo affichent plusieurs mesures agrégées sur une heure spécifiée pour vous permettre de vérifier que les vidéos individuelles et agrégées *publiées* ont les performances attendues. Les données des mesures principales suivantes sont agrégées pour toutes les vidéos publiées sur l’ensemble de votre site web :

* Lancements de vidéo
* Taux d’achèvement
* Durée moyenne de visionnage
* Durée totale de visionnage
* Vidéos par visite

Un tableau de toutes les vidéos *publiées* est également fourni pour vous permettre de suivre les vidéos les plus visionnées sur votre site web en fonction du total des lancements de vidéo.

Lorsque vous sélectionnez le nom d’une vidéo dans la liste, le rapport sur la rétention de l’audience (taux de déperdition) de la vidéo s’affiche sous la forme d’un graphique linéaire. Le graphique présente le nombre de vues à un moment donné de la lecture vidéo. Lorsque vous lisez la vidéo, la barre verticale effectue un suivi en synchronisation avec l’indicateur temporel du lecteur. Les baisses des données du graphique linéaire indiquent le moment où votre audience perd son intérêt.

Si la vidéo a été codée en dehors d’Adobe Experience Manager Dynamic Media, le graphique sur la rétention de l’audience (taux de déperdition) et les données de pourcentage de lecture du tableau ne sont pas disponibles.

Consultez également la section [Configuration des Services cloud Dynamic Media](/help/assets/config-dynamic.md).

>[!NOTE]
>
>Le suivi et les données de rapport reposent exclusivement sur l’utilisation du lecteur vidéo Dynamic Media et du paramètre prédéfini du lecteur vidéo associé. Vous ne pouvez donc pas effectuer le suivi et créer de rapports sur des vidéos qui sont lues par d’autres lecteurs vidéo.

Par défaut, la première fois que vous utilisez l’option Rapports vidéo, le rapport affiche des données vidéo du premier jour du mois en cours jusqu’à la date du mois en cours. Vous pouvez toutefois remplacer la période par défaut par la vôtre. La prochaine fois que vous utiliserez l’option Rapports vidéo, la période que vous avez spécifiée sera utilisée.

Pour que les rapports vidéo fonctionnent correctement, un identifiant de suite de rapports est automatiquement créé lors de la configuration des services cloud Dynamic Media. Dans le même temps, l’identifiant de suite de rapports est transmis au serveur de publication pour qu’il soit disponible pour la fonctionnalité de copie d’URL lors de la prévisualisation de ressources. Cette fonctionnalité nécessite toutefois que le serveur de publication soit déjà configuré. Si le serveur de publication n’est pas configuré, vous pouvez tout de même lancer la publication pour afficher le rapport vidéo. Cependant, vous devez revenir à la configuration du cloud Dynamic Media et sélectionner **[!UICONTROL OK]**.

**Pour afficher un rapport vidéo, procédez comme suit :**

1. Dans le coin supérieur gauche d’Experience Manager, sélectionnez le logo Experience Manager, puis, dans le rail de gauche, cliquez sur **[!UICONTROL Outils]** (icône de marteau) > **[!UICONTROL Ressources]** > **[!UICONTROL Rapports vidéo]**.
1. Dans la page Rapport vidéo, effectuez l’une des opérations suivantes :

   * Dans le coin supérieur droit, sélectionnez l’icône **Actualiser le rapport vidéo**.
N’utilisez la commande d’actualisation que si la date de fin du rapport correspond à la date du jour. Cette exigence vous garantit de voir le suivi vidéo qui a eu lieu depuis la dernière exécution du rapport.

   * Dans le coin supérieur droit, sélectionnez l’icône **Sélecteur de date**.
Indiquez la période de début et de fin pour laquelle vous souhaitez obtenir les données vidéo, puis sélectionnez **[!UICONTROL Exécuter le rapport]**.

   Le groupe Mesures principales identifie diverses mesures agrégées pour toutes les vidéos *publiées* sur votre site.

1. Dans le tableau qui répertorie les principales vidéos publiées, sélectionnez le nom d’une vidéo pour la lire et afficher également le rapport sur la rétention de l’audience (taux de déperdition) de celle-ci.

### Affichage de rapports vidéo reposant sur une visionneuse de vidéos créée à l’aide du SDK de visionneuse HTML5 Dynamic Media {#viewing-video-reports-based-on-a-video-viewer-that-you-created-using-the-scene-hmtl-viewer-sdk}

Si vous utilisez une visionneuse de vidéos prête à l’emploi fournie par Dynamic Media ou si vous avez créé un paramètre prédéfini de visionneuse personnalisée reposant sur une visionneuse de vidéos prête à l’emploi, aucune autre étape n’est nécessaire pour afficher les rapports vidéo. En revanche, si vous avez créé votre propre visionneuse de vidéos en vous reposant sur l’API de SDK de visionneuse HTML5, suivez les étapes ci-après pour vous assurer que votre visionneuse de vidéos envoie des événements de suivi aux rapports vidéo Dynamic Media.

Utilisez le [guide de référence des visionneuses Adobe Dynamic Media](https://experienceleague.adobe.com/fr/docs/dynamic-media-developer-resources) et l’[API de SDK de visionneuse HTML5](https://s7d1.scene7.com/s7sdk/3.10/docs/jsdoc/index.html) pour créer vos propres visionneuses de vidéos.

**Pour afficher des rapports vidéo reposant sur une visionneuse de vidéos créée à l’aide du SDK de visionneuse HTML5 Dynamic Media, procédez comme suit :**

1. Accédez à n’importe quelle ressource vidéo publiée.
1. Près du coin supérieur gauche de la page du fichier, sélectionnez **[!UICONTROL Visionneuses]** dans la liste déroulante.
1. Sélectionnez un paramètre prédéfini de visionneuse de vidéos et copiez le code intégré.
1. Dans le code intégré, recherchez la ligne suivante :

   `videoViewer.setParam("config2", "<value>");`

   Le paramètre `config2` active le suivi dans les visionneuses HTML5. Il s’agit également d’un paramètre prédéfini spécifique à l’entreprise qui contient des informations de configuration pour les rapports vidéo et pour les configurations Adobe Analytics propres au client.

   La valeur correcte du paramètre config2 figure dans le **[!UICONTROL code intégré]** et la fonction Copier l’**[!UICONTROL URL]**. Dans l’URL provenant de la commande Copier l’**[!UICONTROL URL]**, le paramètre à rechercher est `&config2=<value>`. La valeur est pratiquement toujours `companypreset`, mais dans certains cas elle peut également être `companypreset-1`, `companypreset-2`, etc.

1. Dans le code de la visionneuse de vidéos personnalisée, ajoutez le fichier AppMeasurementBridge.jsp à la page de la visionneuse en procédant comme suit :

   * Tout d’abord, déterminez si vous avez besoin du paramètre `&preset`.

     Si le paramètre `config2` est `companypreset`, vous n’avez *pas* besoin de `&preset=parameter`.

     Si le paramètre `config2` a une autre valeur, attribuez au paramètre preset la même valeur que le paramètre `config2`. Par exemple, si `config2=companypreset-2`, ajoutez `&param2=companypreset-2` à l’URL d’AppMeasurmentBridge.jsp.

   * Ajoutez ensuite le script AppMeasurementBridge.jsp :

     `<script language="javascript" type="text/javascript" src="https://s7d1.scene7.com/s7viewers/AppMeasurementBridge.jsp?company=robindallas&preset=companypreset-2"></script>`

1. Créez le composant TrackingManager en effectuant les opérations suivantes :

   * Après avoir appelé `s7sdk.Util.init();`, créez une instance TrackingManager pour suivre les événements en ajoutant le code suivant :

     `var trackingManager = new s7sdk.TrackingManager();`

   * Connectez les composants à TrackingManager en procédant comme suit :

     Dans le gestionnaire d’événements `s7sdk.Event.SDK_READY`, attachez le composant à suivre à TrackingManager.

     Par exemple, si le composant est `videoPlayer`, ajoutez

     `trackingManager.attach(videoPlayer);`

     pour joindre le composant à TrackingManager. Pour suivre plusieurs visionneuses sur une page, utilisez plusieurs composants de gestionnaire de suivi.

   * Créez l’objet AppMeasurementBridge en ajoutant ce qui suit :

     ```
     var appMeasurementBridge = new AppMeasurementBridge(); appMeasurementBridge.setVideoPlayer(videoPlayer);
     ```

   * Ajoutez la fonction de suivi en ajoutant le code suivant :

     ```
     trackingManager.setCallback(appMeasurementBridge.track, 
      appMeasurementBridge);
     ```

   L’objet appMeasurementBridge dispose d’une fonction de suivi intégrée. Vous pouvez toutefois fournir votre propre fonction pour prendre en charge plusieurs systèmes de suivi ou d’autres fonctionnalités.

<!--    For more information, see *Using the TrackingManager Component* in the *Scene7 HTML5 Viewer SDK User Guide* available for download from [Adobe Developer Connection](https://help.adobe.com/en_US/scene7/using/WSef8d5860223939e2-43dedf7012b792fc1d5-8000.html). -->



## À propos de la prise en charge de plusieurs sous-titres et pistes audio pour les vidéos dans Dynamic Media{#about-msma}

Grâce à la fonctionnalité de prise en charge de plusieurs sous-titres et pistes audio de Dynamic Media, vous pouvez facilement ajouter plusieurs sous-titres et pistes audio à une vidéo principale. Cette fonctionnalité signifie que vos vidéos sont accessibles à une audience mondiale. Vous pouvez personnaliser une seule vidéo principale publiée pour une audience mondiale dans plusieurs langues et respecter les directives d’accessibilité pour différentes régions géographiques. Les auteurs et autrices peuvent également gérer les sous-titres et les pistes audio à partir d’un seul onglet de l’interface utilisateur.

![Onglet Sous-titres et pistes audio dans Dynamic Media, ainsi qu’un tableau présentant les fichiers de sous-titres `.vtt` et les fichiers audio .MP3 chargés pour une vidéo.](assets-dm/msma-subtitle-audiotracks-tab2.png)

Voici quelques-uns des cas d’utilisation à prendre en compte pour l’ajout de plusieurs sous-titres et pistes audio à votre vidéo principale :

| Type | Cas d’utilisation |
|--- |--- |
| **Sous-titres** | Prise en charge de plusieurs langues |
|  | Texte descriptif pour l’accessibilité |
| **Pistes audio** | Prise en charge de plusieurs langues |
|  | Pistes de commentaires |
|  | Audio descriptif |

Tous les [formats vidéo pris en charge par Dynamic Media](/help/assets/assets-formats.md) et toutes les visionneuses de vidéos Dynamic Media, à l’exception de Dynamic Media *Video_360* sont pris en charge pour une utilisation avec plusieurs sous-titres et pistes audio.

### Ajouter plusieurs sous-titres et pistes audio à votre vidéo {#add-msma}

Avant d’ajouter plusieurs sous-titres et plusieurs pistes audio à votre vidéo, assurez-vous que vous disposez déjà des éléments suivants :

* Dynamic Media est configuré dans un environnement AEM.
* Un [profil vidéo Dynamic Media est appliqué au dossier dans lequel vos vidéos sont ingérées](/help/assets/video-profiles.md#applying-a-video-profile-to-folders).

Les sous-titres et légendes ajoutés sont pris en charge avec les formats WebVTT et Adobe `.vtt`. Les fichiers des pistes audio ajoutés sont pris en charge au format MP3.

>[!IMPORTANT]
>
>Toutes les vidéos que vous avez chargées *avant* l’activation de la prise en charge de plusieurs sous-titres et pistes audio sur votre compte Dynamic Media [doivent être retraitées](/help/assets/processing-profiles.md#reprocessing-assets). Cette étape de retraitement vidéo est nécessaire afin que les fonctionnalités de prise en charge de plusieurs sous-titres et pistes audio soient disponibles. Après retraitement, les URL de la vidéo continuent à fonctionner et à être lues normalement.

**Pour ajouter plusieurs sous-titres et plusieurs pistes audio à votre vidéo :**

1. [Chargez la vidéo principale dans un dossier](/help/assets/managing-video-assets.md#upload-and-preview-video-assets) qui comporte déjà un profil vidéo qui lui est affecté.
1. Accédez à la ressource vidéo chargée à laquelle ajouter plusieurs sous-titres et pistes audio.
1. En mode de sélection des ressources, en vue Liste ou Carte, sélectionnez la ressource vidéo.
1. Dans la barre d’outils, sélectionnez l’icône Propriétés (cercle contenant un « i »).
   ![Ressource vidéo sélectionnée avec une coche sur l’image de la miniature vidéo et l’option Afficher les propriétés surlignée sur la barre d’outils.](assets-dm/msma-selectedasset-propertiesbutton.png)*Ressource vidéo sélectionnée en vue Carte.*
1. Sur la page Propriétés de la vidéo, sélectionnez l’onglet **[!UICONTROL Sous-titres et pistes audio]**.

   >[!TIP]
   >Si vous ne voyez pas l’onglet **[!UICONTROL Sous-titres et pistes audio]**, cela signifie l’une des deux choses suivantes :
   >
   >* Aucun profil vidéo n’est affecté au dossier dans lequel se trouve la vidéo sélectionnée. Dans ce cas, voir [Appliquer un profil vidéo au dossier](/help/assets/video-profiles.md#applying-video-profiles-to-specific-folders).
   >* Sinon, Dynamic Media doit retraiter la vidéo. Dans ce cas, voir [Retraiter les ressources dans un dossier](/help/assets/processing-profiles.md#reprocessing-assets).
   >
   >Une fois l’une des tâches ci-dessus terminée, reprenez cette procédure.

   ![Onglet Sous-titres et pistes audio dans la page Propriétés.](assets-dm/msma-audiotracks2.png)*Onglet Sous-titres et pistes audio de la page Propriétés de la vidéo.*

1. (Facultatif) Pour ajouter un ou plusieurs fichiers de sous-titres à une vidéo, procédez comme suit :
   * Sélectionnez **[!UICONTROL Charger des sous-titres]**.
   * Accédez à un ou plusieurs fichiers `.vtt` (Video Text Tracks), sélectionnez-les, puis ouvrez-les.
   * Pour que les sous-titres soient visibles sur le lecteur multimédia, vous *devez* ajouter les détails (métadonnées) requis à propos de *chaque* fichier de sous-titres que vous avez chargé. Sélectionnez l’icône représentant un crayon à droite du nom du fichier de sous-titres. Dans la boîte de dialogue **Modifier les sous-titres**, saisissez les détails requis suivants sur le fichier, puis sélectionnez **[!UICONTROL Enregistrer]**. Répétez cette procédure pour chaque fichier de sous-titres que vous avez chargé :

     | Métadonnées de sous-titres | Description |
     |--- |--- |
     | Nom de fichier | Le nom de fichier par défaut est dérivé du nom de fichier d’origine. Le nom du fichier ne peut être modifié que lors du chargement et ne peut pas l’être plus tard. Les exigences relatives aux caractères de nom de fichier sont les mêmes que pour AEM Assets.<br>Le même nom de fichier ne peut pas être utilisé pour des fichiers de sous-titres et de pistes audio supplémentaires. |
     | Langue | Sélectionnez la langue des sous-titres. |
     | Type | Sélectionnez le type de sous-titres que vous utilisez.<br>**Sous-titres** : texte des sous-titres affichés dans la vidéo qui traduit ou transcrit les dialogues.<br>**Légende** : le texte de la légende comprend les bruits de fond, la différenciation des locuteurs et locutrices et d’autres détails pertinents. Il fournit également la traduction ou la transcription du dialogue. Tous ces aspects rendent le contenu plus accessible aux personnes sourdes ou malentendantes. |
     | Libellé | Texte affiché pour le nom du sous-titre dans la liste de fenêtres contextuelles **[!UICONTROL Sélectionner l’audio ou les sous-titres]** du lecteur multimédia. Le libellé correspond à ce qu’un client ou une cliente voit et à une piste de sous-titre ou de légende. Par exemple, `English (CC)`. |

     Vous pouvez modifier les métadonnées de sous-titres ultérieurement, si nécessaire. Lorsque la vidéo est publiée, ces informations sont reflétées dans les URL publiques des vidéos publiées.

1. (Facultatif) Pour ajouter une ou plusieurs pistes audio à une vidéo, procédez comme suit :
   * Sélectionnez **[!UICONTROL Charger des pistes audio]**.
   * Accédez à un ou plusieurs fichiers .mp3 et sélectionnez-les, puis ouvrez-les.
   * Pour que les pistes audio apparaissent dans la liste contextuelle **[!UICONTROL Sélectionner l’audio ou la légende]** du lecteur multimédia, vous *devez* fournir les détails requis. Ces détails sont nécessaires pour *chaque* fichier de piste audio que vous avez ajouté. Sélectionnez l’icône représentant un crayon à droite du nom d’un fichier de piste audio. Dans la boîte de dialogue **Modifier la piste audio**, saisissez les informations requises suivantes, puis sélectionnez **[!UICONTROL Enregistrer]**. Répétez cette procédure pour chaque fichier de piste audio que vous avez chargé.

     | Métadonnées de piste audio | Description |
     |--- |--- |
     | Nom de fichier | Le nom de fichier par défaut est dérivé du nom de fichier d’origine. Le nom du fichier ne peut être modifié que lors du chargement et ne peut pas l’être plus tard. Les exigences relatives aux caractères de nom de fichier sont les mêmes que pour AEM Assets.<br>Le même nom de fichier ne peut pas être utilisé pour des fichiers de piste audio ou de sous-titres supplémentaires. |
     | Langue | Sélectionnez la langue de la piste audio. |
     | Type | Sélectionnez le type de piste audio que vous utilisez.<br>**Original** : piste audio initialement jointe à la vidéo et représentée comme `[Original]` dans le libellé avec la langue `English` sélectionnée par défaut. Bien que **[!UICONTROL Libellé]** et **[!UICONTROL Langue]** peuvent être modifiés dans la boîte de dialogue **[!UICONTROL Modifier la piste audio]**, les valeurs d’origine sont utilisées par défaut si la vidéo principale est retraitée.<br>**Standard** : piste audio complémentaire pour une langue autre que la langue originale.<br>**Audio-description** : piste audio qui comprend également une narration descriptive des actions non verbales et des gestes dans la vidéo, rendant le contenu plus accessible pour les personnes malvoyantes. |
     | Libellé | Texte affiché comme nom de la piste audio dans la liste de fenêtres contextuelles **[!UICONTROL Sélectionner l’audio ou le sous-titre]** du lecteur multimédia. Le libellé correspond à ce qu’un client ou une cliente voit et à une piste audio. Par exemple, `English [Original]`. Le libellé de l’audio associé à une vidéo est défini sur `[Original]` par défaut. |

     Vous pouvez modifier ces métadonnées de piste audio ultérieurement, si nécessaire. Lorsque la vidéo est publiée, ces informations sont reflétées dans les URL publiques des vidéos publiées.

1. Dans le coin supérieur droit de la page, dans la liste déroulante **[!UICONTROL Enregistrer et fermer]**, sélectionnez **[!UICONTROL Enregistrer]**. Les fichiers sont chargés et le traitement des métadonnées commence, comme le montre la colonne **Statut** de l’interface.

   >[!NOTE]
   >
   >Selon les paramètres de mise en cache de votre instance, le traitement des métadonnées peut prendre plusieurs minutes avant qu’elles ne soient reflétées dans l’aperçu et dans les URL publiées.

1. (Facultatif) Si vous avez sélectionné **[!UICONTROL Enregistrer et fermer]** à l’étape précédente au lieu de **[!UICONTROL Enregistrer]**, vous pouvez toujours afficher le statut du traitement des fichiers chargés. Consultez [Afficher le statut du cycle de vie des fichiers de sous-titres et de pistes audio chargés](#lifecycle-status-video).
1. (Facultatif) Prévisualisez la vidéo avant de la publier pour vous assurer que les sous-titres et le son fonctionnent comme prévu. Consultez [Prévisualiser une vidéo comportant plusieurs sous-titres et pistes audio](#preview-video-audio-subtitle).
1. Publiez la vidéo. Consultez la section [Publication de ressources](publishing-dynamicmedia-assets.md).

#### À propos de l’ajout de fichiers de sous-titres et de pistes audio à une vidéo déjà publiée

Le chargement de fichiers de sous-titres ou de pistes audio supplémentaires dans une vidéo déjà publiée entraîne l’attribution d’un statut `Processed` à ces fichiers. Ce statut est appliqué une fois les fichiers préparés après le chargement. À ce stade, vous pouvez prévisualiser la vidéo dans Dynamic Media pour afficher ou entendre les fichiers qui viennent d’être chargés.

Toutefois, après l’aperçu, vous devez *publier* la vidéo à nouveau pour que les fichiers de sous-titres ou de pistes audio nouvellement ajoutés soit également publiés. Après la publication, les sous-titres ou le contenu audio sont disponibles avec l’URL Dynamic Media publique.

>[!NOTE]
>
>En fonction des paramètres de mise en cache de votre instance, les mises à jour de métadonnées peuvent prendre plusieurs minutes avant d’être répercutées dans la prévisualisation et dans les URL publiées.

Dans le cas où vous avez configuré Dynamic Media pour une publication immédiate, le chargement des fichiers de sous-titres ou de pistes audio supplémentaires déclenche immédiatement la publication de la vidéo une fois le chargement terminé.

>[!CAUTION]
>
>Lorsque vous chargez des fichiers de sous-titres ou de pistes audio sur une vidéo publiée ou non, les fichiers sont supprimés si vous [*retraitez*](/help/assets/processing-profiles.md#reprocessing-assets) la vidéo. Seul l’audio d’origine de la vidéo reste intact. Dans ce cas, vous devez recharger les fichiers de sous-titres et de pistes audio dans la vidéo.

#### Ajouter plusieurs sous-titres à une vidéo ayant une URL existante avec le modificateur de sous-titres

Dynamic Media prend en charge l’ajout de sous-titres uniques à une vidéo au moyen d’un modificateur d’URL. Consultez [Ajouter des légendes à une vidéo](#adding-captions-to-video).

Plusieurs modifications de légende ont la priorité sur une légende ajoutée par l’intermédiaire d’un modificateur d’URL pour les vidéos publiées.

**Pour ajouter plusieurs légendes à une vidéo ayant une URL existante avec le modificateur de légende :**

1. Chargez le fichier de légende déjà ajouté comme modificateur à la vidéo afin de pouvoir le gérer explicitement.
1. Chargez d’autres fichiers de sous-titres, si nécessaire.
1. Publiez la vidéo comme vous le faites habituellement.
L’URL existante avec le modificateur de légende peut désormais charger plusieurs légendes.

### Afficher le statut du cycle de vie des fichiers de sous-titres et de pistes audio chargés{#lifecycle-status-video}

Vous pouvez observer le statut du cycle de vie des sous-titres ou des fichiers de piste audio chargés sur votre vidéo principale. Vous pouvez le faire à partir de l’onglet **Sous-titres et pistes audio** de **Propriétés**.

**Pour afficher le statut du cycle de vie d’une vidéo :**

1. Accédez à la ressource vidéo dont vous souhaitez afficher le statut du cycle de vie.
1. En mode de sélection des ressources, en vue Liste ou Carte, sélectionnez la ressource vidéo.
1. Dans la barre d’outils, sélectionnez l’icône Propriétés (cercle contenant un « i »).
1. Sur la page Propriétés, sélectionnez l’onglet **[!UICONTROL Sous-titres et pistes audio]**. Dans la colonne Statut, notez l’état de chaque fichier de sous-titres ou audio.

| Statut des sous-titres ou des pistes audio | Description |
| --- | --- |
| Traitement | Lorsqu’un nouveau fichier de sous-titres ou de pistes audio est ajouté et enregistré, il passe à l’état « Traitement ». Dynamic Media traite le fichier en joignant le manifeste de streaming à la vidéo principale. |
| Traité | Une fois le traitement terminé, le fichier de sous-titres ou de pistes audio, ou la piste audio d’origine associée à la vidéo principale, s’affiche à l’état « Traité ». Vous pouvez prévisualiser les fichiers de sous-titres et de pistes audio qui apparaissent à l’état « Traité » *avant* de publier la vidéo en direct. |
| Publié | Un état « Publié » représente un état similaire à « Publié » pour une vidéo principale. Les ressources sont publiées lorsque la vidéo principale est publiée et sont disponibles sur l’URL Dynamic Media publique. |
| Échec | Un état « Échec » signifie que le traitement d’un fichier de sous-titre ou de pistes audio n’a pas été terminé. Supprimez le fichier de sous-titres ou de pistes audio, puis chargez-le à nouveau. |
| Dépublié | Lorsqu’une vidéo principale publiée est explicitement dépubliée, tout fichier de sous-titres ou de piste audio que vous avez ajouté à la vidéo est également dépublié. |

![Colonne Statut mise en surbrillance pour les champs Sous-titres et Pistes audio.](assets-dm/msma-lifecycle-status2.png)*Statut du cycle de vie de chaque fichier de sous-titres et de pistes audio chargé.*

### Définir l’audio par défaut pour une vidéo comportant plusieurs pistes audio

Par défaut, l’audio d’origine d’une vidéo est défini comme l’audio par défaut à lire.

Cependant, tout fichier de piste audio chargé peut être défini comme l’audio par défaut à lire après le chargement d’une vidéo dans la visionneuse. Dans l’interface d’utilisation des propriétés, sous l’onglet **Sous-titres et pistes audio**, le libellé `Default` est appliqué à droite du fichier de piste audio pour la lecture vidéo.

>[!NOTE]
>
>La lecture du contenu audio par défaut peut également dépendre de ce qui est défini dans les navigateurs suivants :
>
>* Chrome : le contenu audio par défaut défini dans la vidéo est lu.
>* Safari : si la langue par défaut est définie dans Safari, l’audio est lu avec la langue par défaut définie si elle est disponible avec le manifeste de la vidéo. Sinon, le contenu audio par défaut défini dans les propriétés d’une vidéo est lu.

**Pour définir l’audio par défaut d’une vidéo comportant plusieurs pistes audio :**

1. Accédez à la ressource vidéo dont vous souhaitez définir la piste audio par défaut.
1. En mode de sélection des ressources, en vue Liste ou Carte, sélectionnez la ressource vidéo.
1. Dans la barre d’outils, sélectionnez l’icône Propriétés (cercle contenant un « i »).
1. Sur la page Propriétés, sélectionnez l’onglet **[!UICONTROL Sous-titres et pistes audio]**.
1. Sous l’en-tête **Pistes audio**, sélectionnez le fichier de piste audio à définir comme fichier par défaut pour la vidéo.
1. Sélectionnez **[!UICONTROL Définir par défaut]**.
Dans la boîte de dialogue **Définir comme valeur par défaut**, sélectionnez **[!UICONTROL Remplacer]**.

   ![En-tête « Pistes audio » avec un nom de fichier de piste audio sélectionné et le bouton « Définir par défaut » mis en surbrillance.](assets-dm/msma-defaultaudiotrack2.png)*Définition de la piste audio par défaut pour une vidéo.*

1. Dans le coin supérieur droit, sélectionnez **[!UICONTROL Enregistrer et fermer]**.
1. Publiez la vidéo. Consultez la section [Publication de ressources](publishing-dynamicmedia-assets.md).

### Prévisualiser une vidéo comportant plusieurs sous-titres et pistes audio{#preview-video-audio-subtitle}

Une fois les fichiers de sous-titres et de pistes audio chargés dans une vidéo et traités, vous pouvez utiliser la visionneuse de vidéos Dynamic Media (ou d’autres types de visionneuses) pour prévisualiser toutes les différentes pistes. La prévisualisation vous permet de voir à quoi ressemble votre vidéo pour les clientes et clients et d’en écouter le son afin de vous assurer qu’elle se comporte comme prévu.

Lorsque la vidéo vous satisfait, vous pouvez [la publier](publishing-dynamicmedia-assets.md) en utilisant l’une des méthodes suivantes.

Consultez [Incorporation de la visionneuse de vidéos ou d’images dans une page web](/help/assets/embed-code.md).
Consultez [Liaison d’URL à une application web](/help/assets/linking-urls-to-yourwebapplication.md). La méthode de liaison basée sur une URL n’est pas possible si votre contenu interactif contient des liens avec des URL relatives, en particulier des liens vers des pages Experience Manager Sites.
Voir [Ajout de ressources Dynamic Media aux pages](/help/assets/adding-dynamic-media-assets-to-pages.md).

>[!NOTE]
>
>L’onglet Prévisualisation par défaut d’Experience Manager n’affiche pas plusieurs pistes audio et sous-titres. Cela est dû au fait que ces pistes sont associées à Dynamic Media et ne peuvent être affichées qu’à l’aide de la prévisualisation de la visionneuse Dynamic Media.

**Pour prévisualiser une vidéo comportant plusieurs sous-titres et pistes audio, procédez comme suit :**

1. Dans **[!UICONTROL Ressources]**, accédez à une vidéo existante à laquelle vous avez ajouté plusieurs sous-titres et pistes audio.
1. Cliquez sur la ressource vidéo afin de pouvoir l’ouvrir en mode aperçu.
1. Dans la page d’aperçu, dans le coin supérieur gauche de la page, sélectionnez la liste déroulante, puis sélectionnez **[!UICONTROL Visionneuses]**.

   ![Liste déroulante présentant l’option Visionneuses.](assets-dm/msma-selectviewers.png)

1. Dans la liste Visionneuses, sélectionnez une visionneuse à utiliser pour l’aperçu vidéo. Par exemple, la capture d’écran suivante illustre la visionneuse **[!UICONTROL Vidéo]** sélectionnée.

   ![Sélection de la visionneuse Vidéo dans la liste déroulante Visionneuses.](assets-dm/msma-dmviewerselected.png)

1. Près du coin inférieur droit, à gauche de l’icône de volume, sélectionnez l’icône en forme de phylactère, puis sélectionnez l’audio ou le sous-titre que vous souhaitez entendre et/ou ou voir. Si vous le souhaitez, sous Sous-titres, vous pouvez sélectionner **[!UICONTROL Désactivé]** pour ne pas afficher les sous-titres.

   ![Liste de fenêtres contextuelles (pop-up) Audio et sous-titres dans la visionneuse de vidéos.](assets-dm/msma-selectaudiosubtitle.png)*Simulation d’un utilisateur ou d’une utilisatrice sélectionnant le contenu audio et les sous-titres pour la lecture vidéo.*

1. Pour commencer la lecture, sélectionnez le bouton **[!UICONTROL Lecture]** de la vidéo.
Remarquez les boutons **[!UICONTROL URL]** et **[!UICONTROL Incorporer]** en bas à gauche. Utilisez ces boutons pour [lier l’URL de la vidéo à votre application web](/help/assets/linking-urls-to-yourwebapplication.md) ou [incorporer la vidéo dans une page web](/help/assets/embed-code.md), respectivement.
1. Près du coin supérieur droit de la page d’aperçu, sélectionnez **[!UICONTROL Fermer]**.

### Supprimer des fichiers de sous-titres ou de pistes audio d’une vidéo

Vous pouvez supprimer des fichiers de sous-titres ou de pistes audio d’une vidéo. La suppression de fichiers de sous-titres ou de pistes audio publiés est automatiquement répercutée dans l’URL publiée de la vidéo.

La piste audio d’origine extraite d’une vidéo principale ne peut pas être supprimée.

**Pour supprimer des fichiers de sous-titres ou de pistes audio d’une vidéo, procédez comme suit :**

1. Accédez à la ressource vidéo dont vous souhaitez définir la piste audio par défaut.
1. En mode de sélection des ressources, en vue Liste ou Carte, sélectionnez la ressource vidéo.
1. Dans la barre d’outils, sélectionnez l’icône Propriétés (cercle contenant un « i »).
1. Sur la page Propriétés, sélectionnez l’onglet **[!UICONTROL Sous-titres et pistes audio]**.
1. Effectuez l’une des opérations suivantes :

   * Sous-titres : sous l’en-tête **Sous-titres**, sélectionnez un ou plusieurs fichiers de sous-titres à supprimer de la vidéo, puis sélectionnez **[!UICONTROL Supprimer]**.
   * Pistes audio : sous l’en-tête **Pistes audio**, sélectionnez un ou plusieurs fichiers de pistes audio à supprimer de la vidéo, puis sélectionnez **[!UICONTROL Supprimer]**.

1. Dans la boîte de dialogue Supprimer, sélectionnez **[!UICONTROL OK]**.
1. Publiez la vidéo.

### Téléchargez des fichiers de sous-titres ou de pistes audio chargés dans une vidéo.

Vous pouvez télécharger un ou plusieurs fichiers de sous-titres ou de pistes audio que vous avez chargés pour les utiliser avec une vidéo. Vous avez la possibilité de télécharger tous les fichiers sélectionnés au format .zip ou de créer un dossier de téléchargement distinct pour chaque fichier.

La piste audio d’origine extraite d’un fichier principal ne peut pas être téléchargée.

**Pour télécharger des fichiers de sous-titres ou de pistes audio à partir d’une vidéo, procédez comme suit :**

1. Accédez à la ressource vidéo dont vous souhaitez définir la piste audio par défaut.
1. En mode de sélection des ressources, en vue Liste ou Carte, sélectionnez la ressource vidéo.
1. Dans la barre d’outils, sélectionnez l’icône Propriétés (cercle contenant un « i »).
1. Sur la page Propriétés, sélectionnez l’onglet **[!UICONTROL Sous-titres et pistes audio]**.
1. Effectuez l’une des opérations suivantes :

   * Sous-titres : sous l’en-tête **Sous-titres**, sélectionnez un ou plusieurs fichiers de sous-titres à télécharger à partir de la vidéo, puis sélectionnez **[!UICONTROL Télécharger]**.
   * Pistes audio : sous l’en-tête **Pistes audio**, sélectionnez un ou plusieurs fichiers de pistes audio à télécharger à partir de la vidéo, puis sélectionnez **[!UICONTROL Télécharger]**.

1. Dans la boîte de dialogue Télécharger, définissez les options suivantes :

   | Option | Description |
   |--- |--- |
   | Enregistrer sous | Utilisez le nom de fichier par défaut, spécifié dans le champ de texte Enregistrer sous ou indiquez votre propre nom. |
   | Créer un dossier distinct pour chaque ressource | Créez un dossier pour chaque fichier de sous-titres ou de pistes audio que vous avez sélectionné pour téléchargement. |
   | E-mail | Utilisez votre programme de messagerie par défaut pour envoyer le fichier .zip à une adresse e-mail spécifique. |
   | Ressources | Indique le nombre de fichiers à télécharger et la taille totale combinée de tous les fichiers sélectionnés. La désélection de cette option ternit (désactive) le bouton **[!UICONTROL Télécharger]** et vous empêche de télécharger un fichier. |

1. Sélectionnez **[!UICONTROL Télécharger]**.
1. Publiez la vidéo. Consultez la section [Publication de ressources](publishing-dynamicmedia-assets.md).






## Ajouter des sous-titres à une vidéo {#adding-captions-to-video}

Vous pouvez étendre la portée de vos vidéos aux marchés mondiaux en ajoutant des sous-titres aux vidéos uniques ou aux ensembles de vidéos adaptatives. En ajoutant des sous-titrages, vous évitez d’avoir à réenregistrer le son ou de recourir à des locuteurs natifs pour réenregistrer la partie audio dans les différentes langues. La lecture de la vidéo s’effectue dans la langue dans laquelle elle a été enregistrée. Les sous-titres en langues étrangères s’affichent afin que les personnes de différentes nationalités puissent comprendre la partie audio.

Les légendes permettent également une plus grande accessibilité pour les personnes sourdes ou malentendantes.

>[!NOTE]
>
>Le lecteur vidéo utilisé doit prendre en charge l’affichage des sous-titres.

Consultez également la section [Accessibilité dans Dynamic Media](/help/assets/accessibility-dm.md).

Dynamic Media convertit les fichiers de légende au format JSON (JavaScript Object Notation). Cette conversion signifie que vous pouvez incorporer le texte JSON dans une page web sous forme de transcription masquée complète de la vidéo. Les moteurs de recherche peuvent ensuite analyser et indexer le contenu pour permettre de trouver plus facilement les vidéos et fournir aux clients et clientes des informations supplémentaires sur le contenu des vidéos.

Voir [Diffuser du contenu statique (sans image)](https://experienceleague.adobe.com/fr/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/c-serving-static-nonimage-contents#image-serving-api) pour plus d’informations sur l’utilisation de la fonction JSON dans une URL.

**Pour ajouter des sous-titres à une vidéo :**

1. Utilisez une application ou un service tiers pour créer votre fichier de sous-titres vidéo.

   Assurez-vous que le fichier que vous créez est conforme à la norme WebVTT (Web Video Text Tracks). L’extension de nom de fichier pour les sous-titres est `.vtt`. D’autres informations sur la norme de sous-titrage WebVTT sont disponibles.

   Reportez-vous à la section [WebVTT : The web video text tracks format](https://w3c.github.io/webvtt/).

   De nombreux sites web proposent des outils et des services gratuits et payants que vous pouvez utiliser pour créer des fichiers de sous-titres WebVTT en dehors de Dynamic Media. <!-- THE FOLLOWING LINK IS NO LONGER LIVE. CHECKED DECEMBER 13, 2023 For example, to create a simple video caption file with no styling, you can use the following free online caption authoring and editing tool: -->

   <!--[WebVTT Caption Maker](https://testdrive-archive.azurewebsites.net/Graphics/CaptionMaker/Default.html)

   For best results, use the tool in Internet Explorer 9 or above, Google Chrome, or Safari.

   In the tool, in the **[!UICONTROL Enter URL of video file]** field, paste the copied URL of your video file and then click **[!UICONTROL Load]**. See [Obtain a URL for an Asset](/help/assets/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset) to get the URL to the video file itself which you can then paste into the **[!UICONTROL Enter URL of video file field]**. Internet Explorer, Chrome, or Safari can then natively play back the video. -->

   Suivez maintenant les instructions à l’écran pour créer et enregistrer votre fichier WebVTT. Lorsque vous avez terminé, copiez le contenu du fichier de sous-titres et collez-le dans un éditeur de texte brut, puis enregistrez-le avec une extension de fichier `.vtt`.

   >[!NOTE]
   >
   >Pour la bonne prise en charge internationale des sous-titres vidéo dans différentes langues, la norme WebVTT implique de créer des fichiers `.vtt` distincts et des appels pour chaque langue à prendre en charge.

   En règle générale, vous devez attribuer au fichier de sous-titres `.vtt` le même nom qu’au fichier vidéo et vous lui ajoutez l’indicateur de paramètres régionaux, comme -EN, -FR ou -DE. Ainsi, vous pouvez automatiser aisément la génération des URL de vidéo avec le système de gestion de contenu web existant.

1. Dans Experience Manager, chargez votre fichier de sous-titres WebVTT dans le DAM.
1. Accédez à la ressource vidéo *publiée* à associer au fichier de sous-titres que vous avez chargé.

   N’oubliez pas que les URL ne peuvent être copiées qu’*après* la *publication* des ressources.

   Voir [Publication de ressources](/help/assets/publishing-dynamicmedia-assets.md).

1. Utilisez l’une des méthodes suivantes :

   * Pour une expérience de visionneuse de vidéos pop-up, cliquez sur l’**[!UICONTROL URL]**. Dans la boîte de dialogue URL, sélectionnez l’URL et copiez-la dans le Presse-papiers, puis collez-la dans un éditeur de texte simple. Ajoutez l’URL copiée de la vidéo avec la syntaxe suivante :

     `&caption=<server_path>/is/content/<path_to_caption.vtt_file,1>`

     Notez le « `,1` » à la fin du chemin du fichier de sous-titres. Juste après l’extension de fichier `.vtt` dans le chemin d’accès, vous avez la possibilité d’activer ou de désactiver le bouton de sous-titres dans la barre de lecteur vidéo en définissant la valeur respectivement sur « `,1` » ou « `,0` ».

   * Pour une expérience de visionneuse de vidéos intégrée, sélectionnez **[!UICONTROL Code intégré]**. Dans la boîte de dialogue Code intégré, sélectionnez le code intégré et copiez-le dans le Presse-papiers, puis collez-le dans un simple éditeur de texte. Ajoutez le code intégré copié avec la syntaxe suivante :

     `videoViewer.setParam("caption","<path_to_caption.vtt_file,1>");`

     Notez le « `,1` » à la fin du chemin du fichier de sous-titres. Juste après l’extension de fichier `.vtt` dans le chemin d’accès, vous avez la possibilité d’activer ou de désactiver le bouton de sous-titres dans la barre de lecteur vidéo en définissant la valeur respectivement sur « `,1` » ou « `,0` ».

## Ajout de marques de chapitre à la vidéo {#adding-chapter-markers-to-video}

Vous pouvez faciliter la lecture et la consultation de vos vidéos les plus longues en ajoutant des marques de chapitre aux vidéos uniques ou aux ensembles de vidéos adaptatives. Lorsqu’une personne lit la vidéo, elle peut cliquer sur les marqueurs de chapitre dans la chronologie de la vidéo (également appelée défilement vidéo) pour accéder facilement à son point ciblé. Il peut également accéder immédiatement à de nouveaux contenus, à des démonstrations et à des tutoriels.

>[!NOTE]
>
>Le lecteur vidéo utilisé doit prendre en charge l’utilisation des marqueurs de chapitre. Les lecteurs vidéo Dynamic Media prennent en charge les marqueurs de chapitre, mais l’utilisation de lecteurs vidéo tiers ne le permet pas.

Si vous le souhaitez, vous pouvez créer votre propre visionneuse personnalisée et lui donner le nom de votre marque, en utilisant des chapitres au lieu d’utiliser le paramètre prédéfini de la visionneuse de vidéos. Pour obtenir des instructions sur la création de votre propre visionneuse HTML5 avec une navigation par chapitre, dans l’API de SDK de la visionneuse HTML5 d’Adobe, reportez-vous à la section « Personnalisation du comportement à l’aide de modificateurs » sous les classes `s7sdk.video.VideoPlayer` et `s7sdk.video.VideoScrubber`. Consultez la documentation [API du SDK de la visionneuse HTML5](https://s7d1.scene7.com/s7sdk/3.10/docs/jsdoc/index.html).

<!-- If desired, you can create and brand your own custom video viewer with chapters instead of using a video viewer preset. For instructions on creating your own HTML5 viewer with chapter navigation, in the Adobe Scene7 Viewer SDK for HTML5 guide, reference the heading "Customizing Behavior Using Modifiers" under the classes `s7sdk.video.VideoPlayer` and `s7sdk.video.VideoScrubber`. The Adobe Scene7 Viewer SDK is available as a download from [Adobe Developer Connection](https://help.adobe.com/en_US/scene7/using/WSef8d5860223939e2-43dedf7012b792fc1d5-8000.html). -->

Vous créez une liste de chapitres pour votre vidéo un peu de la même façon que vous créez des sous-titres. Autrement dit, vous créez un fichier WebVTT. Notez toutefois que ce fichier doit être distinct de tout autre fichier de sous-titrage WebVTT que vous utilisez ; vous ne pouvez pas combiner les sous-titres et les chapitres dans un fichier WebVTT.

Vous pouvez utiliser l’exemple suivant comme un exemple du format que vous pouvez utiliser pour créer un fichier WebVTT avec une navigation par chapitre :

### Fichier WebVTT avec navigation par chapitre vidéo {#webvtt-file-with-video-chapter-navigation}

```xml
WEBVTT
Chapter 1
00:00.000 --> 01:04.364
The bicycle store behind it all.
Chapter 2
01:04.364 --> 02:00.944
Creative Cloud.
Chapter 3
02:00.944 --> 03:02.937
Ease of management for a working solution.
Chapter 4
03:02.937 --> 03:35.000
Cost-efficient access to rapidly evolving technology.
```

Dans l’exemple ci-dessus, le `Chapter 1` est l’identifiant de repère et il est facultatif. La période de repère `00:00:000 --> 01:04:364` indique l’heure de début et l’heure de fin du chapitre au format `00:00:000`. Les trois derniers chiffres sont les millisecondes et peuvent être laissés sur `000`, selon vos préférences. Le titre du chapitre « `The bicycle store behind it all` » est la description réelle du contenu du chapitre. L’identifiant du repère, l’heure de début du repère, ainsi que le titre du chapitre s’affichent tous dans une fenêtre contextuelle du lecteur vidéo lorsque vous pointez la souris sur un point de repère visuel dans la chronologie de la vidéo.

Étant donné que vous utilisez une visionneuse de vidéos HTML5, assurez-vous que le fichier de chapitres que vous créez est conforme à la norme WebVTT (Web Video Text Tracks). L’extension de nom de fichier de chapitres est `.vtt`. D’autres informations sur la norme de sous-titrage WebVTT sont disponibles.

Reportez-vous à la section [WebVTT : The web video text tracks format](https://w3c.github.io/webvtt/)

**Pour ajouter une navigation par chapitre vidéo, procédez comme suit :**

1. Enregistrez le fichier `.vtt` en codage UTF8 pour éviter tout problème de rendu des caractères dans le texte des titres de chapitres.

   En règle générale, vous attribuez au fichier de chapitres `.vtt` le même nom que celui du fichier vidéo et lui ajoutez le mot « chapitres ». Ainsi, vous pouvez automatiser aisément la génération des URL de vidéo avec le système de gestion de contenu web existant.
1. Dans Experience Manager, chargez votre fichier de chapitres WebVTT.

   Voir la section [Chargement des ressources](/help/assets/manage-assets.md#uploading-assets).

1. Utilisez l’une des méthodes suivantes :

   <table>
     <tbody>
      <tr>
       <td>Pour une expérience de visionneuse de vidéos pop-up</td>
       <td>
       <ol>
       <li>Accédez à la ressource vidéo <i>publiée</i> à associer au fichier de chapitres que vous avez chargé. N’oubliez pas que les URL ne peuvent être copiées qu’<i>après</i> la <i>publication</i> des ressources. Voir <a href="/help/assets/publishing-dynamicmedia-assets.md">Publication de ressources</a>.</li>
       <li>Dans le menu déroulant, cliquez sur <strong>Visionneuses</strong>.</li>
       <li>Dans le rail de gauche, cliquez sur le nom du paramètre prédéfini de la visionneuse de vidéos. Un aperçu de la vidéo s’ouvre dans une page distincte.</li>
       <li>Dans le rail de gauche, dans la partie inférieure, cliquez sur <strong>URL</strong>.</li>
       <li>Dans la boîte de dialogue URL, sélectionnez l’URL et copiez-la dans le Presse-papiers, puis collez-la dans un simple éditeur de texte.</li>
       <li>Ajoutez l’URL copiée de la vidéo avec la syntaxe suivante pour l’associer à l’URL copiée dans votre fichier de chapitres :<br /> <br /> <code>&navigation=<<i>full_copied_URL_path_to_chapter_file</i>.vtt></code><br /> </li>
       </ol> </td>
      </tr>
      <tr>
       <td>Pour une expérience de visionneuse de vidéos incorporée<br /> </td>
       <td>
       <ol>
       <li>Accédez à la ressource vidéo <i>publiée</i> à associer au fichier de chapitres que vous avez chargé. N’oubliez pas que les URL ne peuvent être copiées qu’<i>après</i> la <i>publication</i> des ressources. Voir <a href="/help/assets/publishing-dynamicmedia-assets.md">Publication de ressources</a>.</li>
       <li>Dans le menu déroulant, cliquez sur <strong>Visionneuses</strong>.</li>
       <li>Dans le rail de gauche, cliquez sur le nom du paramètre prédéfini de la visionneuse de vidéos. Un aperçu de la vidéo s’ouvre dans une page distincte.</li>
       <li>En bas du rail gauche, cliquez sur <strong>Incorporer</strong>.</li>
       <li>Dans la boîte de dialogue Code intégré, sélectionnez et copiez le code entier dans le Presse-papiers, puis collez-le dans un simple éditeur de texte.</li>
       <li>Ajoutez le code intégré de la vidéo avec la syntaxe suivante pour l’associer à l’URL copiée dans votre fichier de chapitres :<br /> <br /> <code>videoViewer.setParam("navigation","&lt;<i>full_copied_URL_path_to_chapter_file</i>.vtt&gt;"</code></li>
       </ol> </td>
      </tr>
     </tbody>
   </table>

## À propos des miniatures vidéo dans Dynamic Media en mode Scene7 {#about-video-thumbnails-in-dynamic-media-scene-mode}

Une miniature vidéo est une version en taille réduite d’une image vidéo ou d’une ressource d’image présentant la vidéo au client. La miniature sert à inciter un client ou une cliente à sélectionner la vidéo.

Toutes les vidéos dans Experience Manager doivent être associées à une miniature, et la suppression d’une miniature nécessite son remplacement. Par défaut, lorsque vous chargez une vidéo sur Experience Manager, la première image est utilisée comme miniature. Cependant, vous pouvez personnaliser la miniature à des fins de valorisation de marque ou de recherche visuelle, par exemple. Lorsque vous personnalisez une miniature vidéo, vous pouvez lire la vidéo et la mettre en pause sur l’image que vous souhaitez utiliser. Vous pouvez également sélectionner une ressource d’image que vous avez déjà chargée et *publiée* dans votre gestionnaire de ressources numériques.

Une image de miniature vidéo personnalisée que vous sélectionnez dans une vidéo n’est pas extraite et enregistrée dans la gestion des DAM sous la forme d’une ressource séparée et distincte. Toutefois, une miniature vidéo personnalisée que vous sélectionnez dans une ressource d’image existante est enregistrée dans le JCR. Le chemin d’accès de la ressource sélectionnée est stocké sous le nœud de la ressource vidéo, comme dans l’exemple de chemin d’accès suivant :

`/content/dam/*<folder_name*>/<*video_name*>/jcr:content/manualThumbnail`

La possibilité de personnaliser une miniature vidéo n’est disponible qu’après avoir appliqué un profil vidéo au dossier où se trouve la vidéo.

Consultez également [À propos des miniatures vidéo dans Dynamic Media en mode hybride](#about-video-thumbnails-in-dynamic-media-hybrid-mode).

### Ajout d’une miniature vidéo personnalisée {#adding-a-custom-video-thumbnail}

Ces étapes s’appliquent uniquement à Dynamic Media s’exécutant en mode « Dynamicmedia_Scene7 ».

**Pour ajouter une miniature vidéo personnalisée, procédez comme suit :**

1. Assurez-vous que vous avez déjà :

   * Créé un dossier pour vos ressources vidéo.
   * [attribué un profil vidéo au dossier](/help/assets/video-profiles.md#applying-a-video-profile-to-folders) ;

   * [Téléchargé vos vidéos dans le dossier](/help/assets/managing-video-assets.md#upload-and-preview-video-assets).

1. Accédez à une ressource vidéo chargée pour laquelle vous souhaitez modifier l’image miniature.
1. En mode de sélection de ressources, soit **[!UICONTROL Vue liste]** soit **[!UICONTROL Vue carte]**, sélectionnez la ressource vidéo.
1. Dans la barre d’outils, sélectionnez l’icône **[!UICONTROL Propriétés]** (cercle contenant un « i »).
1. Sur la page Propriétés de la vidéo, sélectionnez **[!UICONTROL Modifier la miniature]**.
1. Sur la page Modifier la miniature, effectuez l’une des opérations suivantes :

   * Pour utiliser une image de la vidéo comme nouvelle miniature :

      * Dans la barre d’outils, choisissez **[!UICONTROL Sélectionner une image dans la vidéo]**.
      * Sélectionnez le bouton Lecture, puis le bouton Pause sur l’image à capturer comme nouvelle miniature de la vidéo.

   * Pour utiliser une ressource image comme nouvelle miniature :

      * Dans la barre d’outils, choisissez **[!UICONTROL Sélectionner une miniature dans Ressources]**.
      * Choisissez **[!UICONTROL Sélectionner la miniature]**.
      * Accédez à une ressource d’image téléchargée et publiée précédemment que vous souhaitez utiliser. La ressource est automatiquement redimensionnée afin de servir d’image miniature pour la vidéo.
      * Sélectionnez la ressource image, puis choisissez **[!UICONTROL Sélectionner]**.

1. Sur la page Modifier la miniature, sélectionnez **[!UICONTROL Enregistrer la modification]**.
1. Sur la page Propriétés de la vidéo, dans le coin supérieur droit, sélectionnez **[!UICONTROL Enregistrer et fermer]**.

## À propos des miniatures vidéo dans Dynamic Media en mode hybride {#about-video-thumbnails-in-dynamic-media-hybrid-mode}

Vous pouvez choisir l’une des dix images miniatures générées automatiquement par Dynamic Media pour l’ajouter à votre vidéo. Le lecteur vidéo affiche votre miniature sélectionnée lorsqu’une ressource vidéo est utilisée avec le composant Dynamic Media dans l’environnement de création d’Experience Manager Sites, Experience Manager Mobile ou Experience Manager Screens. La miniature sert d’image statique pour représenter au mieux le contenu de votre vidéo complète et encourage davantage les utilisateurs à cliquer sur le bouton Lecture.

En fonction de la durée totale de la vidéo, Dynamic Media capture dix images miniatures (par défaut). Le système capture les images selon les intervalles vidéo suivants :

* 1¹%
* 11 %
* 21 %
* 31 %
* 41 %
* 51 %
* 61 %
* 71 %
* 81 %
* 91 %

Les dix miniatures restent, ce qui signifie que si vous décidez de sélectionner une miniature différente ultérieurement, vous n’avez pas besoin de générer de nouveau une série de miniatures. Vous prévisualisez les dix images miniatures, puis choisissez celle que vous souhaitez utiliser pour votre vidéo. Si vous souhaitez modifier cette option par défaut, vous pouvez utiliser CRXDE Lite pour configurer l’intervalle pour lequel les miniatures sont générées. Par exemple, si vous souhaitez uniquement générer une série de quatre miniatures à espacement égal à partir de votre vidéo, vous pouvez configurer l’intervalle à 24 %, 49 %, 74 % et 99 %.

Idéalement, vous pouvez ajouter une miniature vidéo à tout moment après avoir téléchargé votre vidéo, mais avant de la publier sur votre site web.

Si vous préférez, vous pouvez charger une miniature personnalisée pour représenter votre vidéo au lieu d’en utiliser une générée par Dynamic Media. Par exemple, vous pouvez créer une miniature personnalisée qui porte le titre de votre vidéo, une image d’ouverture attrayante ou une image bien spécifique capturée dans votre vidéo. La miniature de vidéo personnalisée que vous chargez doit avoir une résolution maximale de 1 280 x 720 pixels (largeur minimale de 640 pixels) et ne pas dépasser 2 Mo.

Consultez également la section [À propos des miniatures vidéo dans le mode Scene7 de Dynamic Media](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-scene-mode).

### Ajout d’une miniature vidéo {#adding-a-video-thumbnail}

Ces étapes s’appliquent uniquement à Dynamic Media s’exécutant en mode hybride.

**Pour ajouter une miniature vidéo, procédez comme suit :**

1. Accédez à une ressource vidéo téléchargée à laquelle vous souhaitez ajouter une miniature.
1. En mode de sélection des ressources, en vue Liste ou Carte, sélectionnez la ressource vidéo.
1. Dans la barre d’outils, sélectionnez l’icône **[!UICONTROL Afficher les propriétés]** (cercle contenant un « i »).
1. Sur la page Propriétés de la vidéo, sélectionnez **[!UICONTROL Modifier la miniature]**.
1. Sur la page Modifier la miniature, dans la barre d’outils, choisissez **[!UICONTROL Sélectionner une image]**.

   Dynamic Media génère une série de miniatures de votre vidéo, en fonction de l’intervalle par défaut ou personnalisé.

1. Prévisualisez les images miniatures générées, puis sélectionnez celle que vous souhaitez ajouter à votre vidéo.
1. Sélectionnez **[!UICONTROL Enregistrer la modification]**.

   La miniature de la vidéo est mise à jour afin d’utiliser la miniature que vous avez sélectionnée. Si vous décidez par la suite de modifier la miniature, vous pouvez revenir à la page **[!UICONTROL Modifier la miniature]** et en sélectionner une nouvelle.

   Si vous définissez de nouveaux intervalles par défaut ou chargez une nouvelle vidéo pour remplacer l’existante, assurez-vous que Dynamic Media régénère les miniatures.

   Consultez la section [Configuration de l’intervalle par défaut pour la création des miniatures de vidéo](#configuring-the-default-time-interval-that-video-thumbnails-are-generated).

#### Configuration de l’intervalle par défaut pour la génération des miniatures de vidéo {#configuring-the-default-time-interval-that-video-thumbnails-are-generated}

Lorsque vous configurez et enregistrez le nouvel intervalle par défaut, votre modification s’applique automatiquement et uniquement aux vidéos que vous chargerez par la suite. Il n’applique pas automatiquement le nouveau paramètre par défaut aux vidéos que vous avez précédemment chargées. Pour les vidéos existantes, vous devez régénérer les miniatures.

Consultez la section [Ajout d’une miniature de vidéo](#adding-a-video-thumbnail).

**Pour configurer l’intervalle par défaut auquel les miniatures vidéo sont créées, procédez comme suit :**

1. Dans Experience Manager, sélectionnez **[!UICONTROL Outils]** > **[!UICONTROL Général]** > **[!UICONTROL CRXDE Lite]**.

1. Dans la page CRXDE Lite, dans le panneau de répertoire à gauche, accédez à `o etc/dam/imageserver/configuration/jcr:content/settings.`.

   Si le panneau des répertoires n’est pas visible, sélectionnez l’icône >> à gauche de l’onglet Accueil.

1. Sur le panneau en bas à droite, dans l’onglet Propriétés, double-cliquez sur `thumbnailtime`.
1. Dans la boîte de dialogue **[!UICONTROL Modifier thumbnailtime]**, utilisez les champs de texte pour saisir des valeurs d’intervalle sous la forme de pourcentages.

   * Sélectionnez l’icône plus (+) pour ajouter un ou plusieurs champs de valeur d’intervalle. Si nécessaire, faites défiler la page jusqu’en bas de la boîte de dialogue pour afficher l’icône.
   * Sélectionnez l’icône du signe moins (-) à droite du champ de valeur d’intervalle si vous souhaitez le supprimer de la liste.
   * Sélectionnez la flèche vers le haut ou vers le bas si vous souhaitez réorganiser les valeurs d’intervalle.

1. Sélectionnez **[!UICONTROL OK]** pour retourner à l’onglet Propriétés.
1. Près du coin supérieur gauche de la page CRXDE Lite, sélectionnez **[!UICONTROL Enregistrer tout]**, puis l’icône Retour à l’accueil dans le coin supérieur gauche pour revenir à Experience Manager.

   Consultez la section [Ajout d’une miniature de vidéo](#adding-a-video-thumbnail).

### Ajout d’une miniature vidéo personnalisée {#adding-a-custom-video-thumbnail-1}

Ces étapes s’appliquent uniquement à Dynamic Media s’exécutant en mode hybride.

**Pour ajouter une miniature vidéo personnalisée, procédez comme suit :**

1. Accédez à une ressource vidéo chargée à laquelle vous souhaitez ajouter une miniature vidéo personnalisée.
1. En mode de sélection des ressources, en vue Liste ou Carte, sélectionnez la ressource vidéo.
1. Dans la barre d’outils, sélectionnez l’icône **[!UICONTROL Afficher les propriétés]** (cercle contenant un « i »).
1. Sur la page Propriétés de la vidéo, sélectionnez **[!UICONTROL Modifier la miniature]**.
1. Sur la page Modifier la miniature, dans la barre d’outils, sélectionnez **[!UICONTROL Charger une nouvelle miniature]**.
1. Naviguez jusqu’à la miniature que vous souhaitez utiliser, sélectionnez-la, puis sélectionnez **[!UICONTROL Ouvrir]** pour commencer à charger l’image dans Experience Manager. Après le chargement, veillez à publier l’image.
1. Une fois l’image chargée et publiée, sur la page Modifier la miniature, sélectionnez **[!UICONTROL Enregistrer les modifications]**.

   La miniature personnalisée est ajoutée à votre vidéo.

## Modifier l’URL Dynamic Media pour les ressources Dynamic Media {#manifest-urls}

Les vidéos traitées dans Dynamic Media peuvent être utilisées avec des visionneuses prêtes à l’emploi ou, en accédant aux URL de manifeste et en les lisant dans des visionneuses personnalisées. Voici l’API permettant de récupérer les URL de manifeste d’une vidéo.

### À propos de l’API getVideoManifestURI

L’API `getVideoManifestURI` est exposée via c`q-scene7-api:com.day.cq.dam.scene7.api` et peut être utilisée pour générer les URL de manifeste suivantes :

```java
/**   
* Returns the manifest url for videos 
* @param resource video resource 
* @param manifestType type of video streaming manifest being requested 
* @param onlyIfPublished return a manifest only if the video is published 
* @return the manifest url for videos 
* 
* @throws Exception 
*/
@Nullable 
String getVideoManifestURI(Resource resource, ManifestType manifestType, boolean onlyIfPublished) throws Exception;
```

#### Paramètres de l’API getVideoManifestURI

Cette API utilise les trois paramètres suivants :

| Paramètre | Description |
| --- | --- |
| `resource` | Ressource correspondant à la vidéo ingérée par Dynamic Media. |
| `manifestType` | Peut être `ManifestType.DASH` ou `ManifestType.HLS` |
| `onlyIfPublished` | Définissez cette variable sur true au cas où l’uri de manifeste n’est générée que si elle est publiée et disponible au niveau de la diffusion. |

Pour récupérer les URL de manifeste des vidéos à l’aide de la méthode ci-dessus, ajoutez un [profil de codage vidéo](/help/assets/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming) dans un dossier « charger des vidéos ». Dynamic Media traite ces vidéos en fonction des encodages trouvés dans le fichier de codage vidéo qui a été affecté au dossier. Vous pouvez maintenant appeler l’API ci-dessus pour récupérer les URL de manifeste pour les vidéos chargées.

### Scénarios d’erreur

L’API renvoie la valeur null en cas d’erreur. Les exceptions sont consignées dans les journaux d’erreurs d’Experience Manager. Toutes ces erreurs consignées commencent par `Could not generate Video Manifest URI`. Les scénarios suivants peuvent provoquer de telles erreurs :

* Une `IllegalArgumentException` est consignée pour l’un des éléments suivants :

   * Le paramètre `resource` transmis est une valeur null.
   * Le paramètre `resource` transmis n’est pas une vidéo.
   * Le paramètre `manifestType` transmis est une valeur null.
   * Le paramètre `onlyIfPublished` transmis est réel, mais la vidéo n’est pas publiée.
   * La vidéo n’a pas été ingérée à l’aide d’une visionneuse de vidéos adaptative provenant de Dynamic Media.

* `IOException` est consignée lorsqu’un problème de connexion à Dynamic Media se produit.
* `UnsupportedOperationException` est consignée lorsqu’un paramètre `manifestType` transmis est `ManifestType.DASH`, alors que la vidéo n’a pas été traitée au format DASH.

Voici un exemple de l’API ci-dessus utilisant des servlets écrits dans la spécification *HTTPWhiteBoard*. Sélectionnez chaque onglet pour la syntaxe du code.

>[!BEGINTABS]

>[!TAB Ajouter une dépendance dans pom.xml]

+++**Ajouter une dépendance dans pom.xml** 

```java
dependency> 
     <groupId>com.day.cq.dam</groupId> 
     <artifactId>cq-scene7-api</artifactId> 
     <version>5.12.64</version> 
     <scope>provided</scope> 
</dependency> 
```

+++

>[!TAB Exemple de servlet]

+++**Exemple de servlet** 

```java
@Component
        service = Servlet.class 
) 
@HttpWhiteboardServletPattern(value = ManifestServlet.SERVLET_PATTERN) 
@HttpWhiteboardContextSelect(value = Constants.SERVLET_CONTEXT_SELECTOR) 
public class ManifestServlet extends HttpServlet { 

   private static final Logger LOGGER = LoggerFactory.getLogger(ManifestServlet.class); 

   private final ObjectMapper objectMapper; 

    @Reference 
    private Scene7Service scene7Service; 

   public static final String SERVLET_PATTERN = Constants.VIDEO_API_PREFIX + "/manifestUrl"; 

   public ManifestServlet() {
         this.objectMapper = new ObjectMapper(); 
         objectMapper.setSerializationInclusion(JsonInclude.Include.NON_NULL); 
   }

   @Override 

   protected void doGet(HttpServletRequest request, HttpServletResponse response) throws IOException {
        final ResourceResolver resolver = getResourceResolver(request); 
        String assetPath = request.getParameter("assetPath"); 
        String manifest = request.getParameter("manifestType"); 
        String onlyIfPublished = request.getParameter("onlyIfPublished"); 
        Resource resource = resolver.getResource(assetPath); 
        response.setCharacterEncoding(StandardCharsets.UTF_8.toString()); 
        response.setContentType("application/json"); 
        if(resource == null) { 
            LOGGER.info("could not retrieve the resource from JCR"); 
            error("could not retrieve the resource from JCR", response); 
            return; 
        }

        String manifestUri = null; 

        try{ 
            ManifestType manifestType =  ManifestType.DASH; 
            if(manifest != null) { 
                manifestType = ManifestType.valueOf(manifest); 
            } 
            manifestUri = scene7Service.getVideoManifestURI(resource, manifestType, onlyIfPublished != null); 
            objectMapper.writeValue(response.getWriter(), new ManifestUrl(manifestUri)); 
            response.setContentType("application/json"); 
        } catch (Exception e) { 
            LOGGER.error(e.getMessage(), e); 
            error(String.format("Unable to get the manifest url for %s. %s", assetPath, e.getMessage()), response); 
        } 
    } 

    private ResourceResolver getResourceResolver(HttpServletRequest request) { 
        Object rr = request.getAttribute(AuthenticationSupport.REQUEST_ATTRIBUTE_RESOLVER); 
        if (!(rr instanceof ResourceResolver)) { 
            throw new IllegalStateException( 
                    "The request does not seem to have been created via Apache Sling's authentication mechanism."); 
        } else { 
            return (ResourceResolver) rr; 
        } 
    } 

    private void error(String errorMessage, HttpServletResponse response) throws IOException { 
        ManifestUrl errorManifest = new ManifestUrl(null); 
        errorManifest.setErrorMessage(errorMessage); 
        response.setStatus(HttpServletResponse.SC_INTERNAL_SERVER_ERROR); 
        objectMapper.writeValue(response.getWriter(), errorManifest); 
    } 
} 
```

+++

>[!TAB Classe de réponse pour le servlet]

+++**Classe de réponse pour le servlet** 

```java
public class ManifestUrl extends VideoResponse { 
     String manifestUrl; 
     public ManifestUrl(String manifestUrl) { 
         this.manifestUrl = manifestUrl; 
     } 
     public String getManifestUrl() { 
         return manifestUrl; 
     } 
} 

public abstract class VideoResponse { 
     String errorString; 

     public String getErrorString() { 
         return errorString; 
     } 

     public void setErrorMessage(String errorString) { 
         this.errorString = errorString; 
     } 
} 
```

+++

>[!TAB Fichier des constantes référencé dans le servlet]

+++**Fichier des constantes référencé dans le servlet** 

```java
public final class Constants { 

     private Constants() { 
     } 

     public static final String VIDEO_API_PREFIX = "/dynamicmedia/video"; 
     public static final String SERVLET_CONTEXT_SELECTOR = "(" + HttpWhiteboardConstants.HTTP_WHITEBOARD_CONTEXT_NAME + "=" + 
             DMSampleApiHttpContext.CONTEXT_NAME + ")"; 

 } 
```

+++

>[!TAB ServletContext]

+++**ServletContext** 

Montez le servlet ci-dessus à l’aide d’un `servletContext`. Voici un exemple de `servletContext`.

```java
public class DMSampleApiHttpContext extends ServletContextHelper { 

 public static final String CONTEXT_NAME = "com.adobe.dmSample"; 
 public static final String CONTEXT_PATH = "/dmSample"; 

 private final MimeTypeService mimeTypeService; 

 private final AuthenticationSupport authenticationSupport; 

 /** 
  * Constructs a new context that will use the given dependencies. 
  * 
  * @param mimeTypeService Used when providing mime type of requests. 
  * @param authenticationSupport Used to authenticate requests with sling. 
  */ 
 @Activate 
 public DMSampleApiHttpContext(@Reference final MimeTypeService mimeTypeService, 
                               @Reference final AuthenticationSupport authenticationSupport) { 
     this.mimeTypeService = mimeTypeService; 
     this.authenticationSupport = authenticationSupport; 
 } 

 // ---------- HttpContext interface ---------------------------------------- 
 /** 
  * Returns the MIME type as resolved by the <code>MimeTypeService</code> or 
  * <code>null</code> if the service is not available. 
  */ 
 @Override 
 public String getMimeType(String name) { 
     MimeTypeService mtservice = mimeTypeService; 
     if (mtservice != null) { 
         return mtservice.getMimeType(name); 
     } 
     return null; 
 } 

 /** 
  * Returns the real context path that is used to mount this context. 
  * @param req servlet request 
  * @return the context path 
  */ 
 public static String getRealContextPath(HttpServletRequest req) { 
     final String path = req.getContextPath(); 
     if (path.equals(CONTEXT_PATH)) { 
         return ""; 
     } 
     return path.substring(CONTEXT_PATH.length()); 
 } 

 /** 
  * Returns a request wrapper that transforms the context path back to the original one 
  * @param req request 
  * @return the request wrapper 
  */ 
 public static HttpServletRequest createContextPathAdapterRequest(HttpServletRequest req) { 
     return new HttpServletRequestWrapper(req) { 

         @Override 
         public String getContextPath() { 
             return getRealContextPath((HttpServletRequest) getRequest()); 
         } 

     }; 

 } 

 /** 
  * Always returns <code>null</code> because resources are all provided 
  * through individual endpoint implementations. 
  */ 
 @Override 
 public URL getResource(String name) { 
     return null; 
 } 

 /** 
  * Tries to authenticate the request using the 
  * <code>SlingAuthenticator</code>. If the authenticator or the Repository 
  * is missing this method returns <code>false</code> and sends a 503/SERVICE 
  * UNAVAILABLE status back to the client. 
  */ 
 @Override 
 public boolean handleSecurity(HttpServletRequest request, 
                               HttpServletResponse response) throws IOException { 

     final AuthenticationSupport authenticator = this.authenticationSupport; 
     if (authenticator != null) { 
         return authenticator.handleSecurity(createContextPathAdapterRequest(request), response); 
     } 

     // send 503/SERVICE UNAVAILABLE, flush to ensure delivery 
     response.sendError(HttpServletResponse.SC_SERVICE_UNAVAILABLE, 
             "AuthenticationSupport service missing. Cannot authenticate request."); 
     response.flushBuffer(); 

     // terminate this request now 
     return false; 
 } 
}
```

+++

>[!ENDTABS]

### Utiliser l’exemple de servlet

Vous appelez le servlet en effectuant une opération `GET` sur `/dmSample/dynamicmedia/video/manifestUrl`. Les paramètres de requête suivants sont transmis :

| Paramètre de requête | Description |
| --- | --- |
| `assetPath` | Obligatoire. Chemin d’accès à la vidéo pour laquelle `manifestUrl` est générée. |
| `manifestType` | Facultatif. Le paramètre peut être DASH ou HLS. S’il n’est pas transmis, la valeur par défaut est DASH. |
| `onlyIfPublished` | Facultatif. S’il est transmis, l’`manifestUrl` est renvoyée uniquement si la vidéo est publiée. |

Dans cet exemple, prenons la configuration suivante :

* La société est `samplecompany`.
* L’instance de création est `http://sample-aem-author.com`.
* Le dossier `/content/dam/video-example` est associé à un profil de codage vidéo.
* La vidéo `scenery.mp4` est chargée dans le dossier `/content/dam/video-example`.

Vous pouvez appeler le servlet des façons suivantes :

| Type | Description |
| :--- | --- |
| HLS | `http://sample-aem-author.com/dmSample/dynamicmedia/video/manifestUrl?manifestType=HLS&assetPath=/content/dam/video-example/scenery.mp4`<br><br>Si la diffusion DASH est activée :<br>`{"manifestUrl":"https://s7d1.scene7.com/is/content/samplecompany/scenery-AVS.m3u8?packagedStreaming=true"}`<br><br>Si la diffusion DASH est désactivée :<br>`{"manifestUrl":"https://s7d1.scene7.com/is/content/samplecompany/scenery-AVS.m3u8"}` |
| DASH | `http://sample-aem-author.com/dmSample/dynamicmedia/video/manifestUrl?manifestType=DASH&assetPath=/content/dam/video-example/scenery.mp4`<br><br>Si la diffusion DASH est activée :<br>`{"manifestUrl":"https://s7d1.scene7.com/is/content/samplecompany/scenery-AVS.mpd"}`<br><br>Si la diffusion DASH est désactivée :<br>`{}` |
| Erreur : chemin d’accès à la ressource incorrect | `http://sample-aem-author.com/dmSample/dynamicmedia/video/manifestUrl?manifestType=DASH&assetPath=/content/dam/video-example/scennnnnnery.mp4`<br><br>`{"errorString":"could not retrieve the resource from JCR"}` |




<!-- OBSOLETE. REMOVED AS PER EMAIL FROM RIYA MIDHA ON WEDNESDAY, MARCH 5, 2025

### Enable DASH, multiple caption and audio track support on your Dynamic Media account {#enable-dash}

**About enabling DASH on your account**
DASH (Digital Adaptive Streaming over HTTP) is the international standard for video streaming and is widely adopted across different video viewers. When DASH is enabled on your account, you get the option to choose from either DASH or HLS for adaptive video streaming. Or, you can opt for both with automatic switching between players when **[!UICONTROL auto]** is selected as the playback type in the Viewer preset.

Some key benefits from enabling DASH on your account include the following:
     
* Package DASH stream video for adaptive bitrate streaming. This method leads to higher efficiency of delivery. Adaptive streaming ensures the best viewing experience for your customers.
* Browser optimized streaming with Dynamic Media players switches between HLS and DASH streaming to ensure the best quality of service. The video player auto-switches to HLS when a Safari browser is used.
* You can configure your preferred streaming method (HLS or DASH) by editing the video viewer preset.
* Optimized video encoding ensures that no additional storage is used while enabling DASH capability. A single set of video encodings are created for both HLS and DASH to optimize video storage costs.
* Helps make video delivery more accessible for your customers.
* Get the streaming URL by way of APIs, too.

Enabling DASH on your account requires two steps: 

* Configuring Dynamic Media to use DASH, which you can easily do yourself.
* Configuring Experience Manager 6.5 to use DASH which is done by way of an Adobe Customer Support case that you create and submit.

When you create an Adobe Support case to enable DASH on your account, multiple caption and audio track support is automatically enabled as well. Once activated, all newly uploaded videos are processed using an updated backend architecture that supports adding multiple caption and audio tracks.

>[!IMPORTANT]
>
>Any videos that you uploaded *before* enabling multiple caption and audio track support on your Dynamic Media account, [must be reprocessed](/help/assets/processing-profiles.md#reprocessing-assets). This video reprocessing step is necessary so that multiple caption and audio track capability is available to them. The video URLs continue to work and play as usual, after reprocessing.

**To enable DASH, multiple caption and multiple audio track support on your Dynamic Media account:**

<!-- 1. **Configure Dynamic Media for DASH** - In Dynamic Media on Experience Manager 6.5, navigate to [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).

1. Search for **AEM Assets Dynamic Media Video Advanced Streaming** feature flag.
1. To enable (turn on) DASH, select the checkbox.
1. Begin by **configuring Dynamic Media for DASH** - From Experience Manager, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.

1. From the **[!UICONTROL Adobe Experience Manager Web Console Configuration]** page, scroll to the name *AEM Assets Dynamic Media Video Advanced Streaming Feature Flag*.

1. To the left of the name, select the checkbox to enable (turn on) DASH.

1. Select **[!UICONTROL Save]**.

1. Now, use the Admin Console to start the [creation of a new support case](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html).
1. To create a support case, follow the instructions while ensuring you provide the following information:

    * Primary contact name, email, phone.
    * Name of your Dynamic Media account.
    * Specify that you want DASH, multiple caption and multiple audio track support enabled on your Dynamic Media account, on Experience Manager 6.5.
   
1. Adobe Customer Support adds you to the Customer Wait List based on the order in which requests are submitted.
1. When Adobe is ready to handle your request, Customer Support contacts you to coordinate and set a target date for enablement.
1. Customer support notifies you after completion.
1. Now, you can do either one of the following:

    * Create your [video viewer preset](/help/assets/managing-viewer-presets.md#creating-a-new-viewer-preset) as usual.
    * [Add multiple caption and audio tracks](#add-msma) to your video. -->




