---
title: Intégration d’URL à votre application web
description: Comment lier des URL à votre application web dans les médias dynamiques
uuid: cf599e66-b1f9-40c0-b572-cea19f2e6793
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: d12e6ea3-aaf4-4672-9679-3c16c76d7d5b
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# Intégration d’URL à votre application web {#linking-urls-to-your-web-application}

Vos sites Web et applications accèdent aux services Contenu multimédia dynamique par le biais d’appels d’URL. Une fois que vous avez publié une ressource, Dynamic Media active une chaîne d’URL qui fait référence à la ressource. Vous pouvez coller ces URL dans un navigateur web à des fins de test.

Vous ne pouvez lier à des URL que si vous *n’utilisez pas* AEM pour la gestion de contenu web. La liaison par rapport à l’incorporation est utilisée lorsque vous souhaitez diffuser un lecteur vidéo sous forme de fenêtre contextuelle ou modale. Dans le cas contraire, [vous pouvez ajouter les ressources directement à votre page.](adding-dynamic-media-assets-to-pages.md)

Pour placer ces chaînes URL dans vos pages et applications Web, copiez-les depuis Dynamic Media.

>[!NOTE]
>
>Les chaînes URL ne sont disponibles que pour les rendus dynamiques des ressources. Elles ne sont actuellement pas disponibles pour les ressources statiques qui résident dans la gestion des actifs numériques et non dans le serveur de média dynamique. Le bouton URL n’apparaît pas pour les rendus statiques.

Reportez-vous également à la section [Incorporation de la visionneuse de vidéos ou d’images dans une page web.](embed-code.md)

Voir aussi [Liaison d’URL YouTube à une application web](video.md).

Voir aussi [Diffusion d’images optimisées pour un site réactif](responsive-site.md).

Voir aussi [Téléchargement de ressources](managing-assets-touch-ui.md#uploading-assets).

## Obtention d’une URL pour une ressource {#obtaining-a-url-for-an-asset}

Vous pouvez obtenir une chaîne URL qui est générée par un paramètre d’image prédéfini ou un paramètre prédéfini de la visionneuse. Une fois que vous avez copié l’URL, elle se trouve dans le presse-papiers ce qui vous permet de la coller dans les pages de votre site Web ou de votre application.

>[!NOTE]
>
>Vous ne pouvez pas copier l’URL tant que la ressource sélectionnée n’a pas été publiée. En outre, vous devez également publier le paramètre de visionneuse prédéfini ou le paramètre d’image prédéfini.
>
>Voir [Publication de ressources](publishing-dynamicmedia-assets.md).
>
>Voir [Publication de paramètres de visionneuse prédéfinis](managing-viewer-presets.md#publishing-viewer-presets).
>
>Voir [Publication de paramètres d’image prédéfinis](managing-image-presets.md#publishing-image-presets).

Il existe différents moyens d’obtenir une chaîne URL. Néanmoins, les étapes ci-dessous ne vous présentent qu’une seule méthode.

**Pour obtenir une URL pour un fichier**

1. Navigate to the *published* asset whose image preset URL or viewer preset URL you want to copy, and tap the asset to open it.

   N’oubliez pas que les URL ne peuvent être copiées qu’*après* la *publication* des ressources. En outre, le paramètre de visionneuse prédéfini ou le paramètre d’image prédéfini doit également être publié.

   Voir [Publication de ressources](publishing-dynamicmedia-assets.md).

   Voir [Publication de paramètres de visionneuse prédéfinis](managing-viewer-presets.md#publishing-viewer-presets).

   Voir [Publication de paramètres d’image prédéfinis](managing-image-presets.md#publishing-image-presets).

1. Selon la ressource sélectionnée, procédez comme suit :

   * If you selected an image, in the drop-down menu, tap **[!UICONTROL Renditions]**.

      Sous l’en-tête **[!UICONTROL Dynamique]**, appuyez sur un nom de paramètre prédéfini afin d’afficher son rendu dans le cadre de droite. Il vous faudra peut-être faire défiler la liste Rendus pour afficher l’en-tête Dynamique.

      Dans la partie inférieure du rail gauche, appuyez sur **[!UICONTROL URL]**.

      ![chlimage_1-270](assets/chlimage_1-270.png)

   * If you selected a spin set, an image set, a carousel set, or a video, in the drop-down menu, tap **[!UICONTROL Viewers]**.

      Dans le rail de gauche, appuyez sur un nom de paramètre prédéfini de la visionneuse. Un aperçu de la visionneuse ou de la vidéo s’ouvre dans une page distincte.

      Dans le rail de gauche, dans la partie inférieure, appuyez sur **[!UICONTROL URL]**.

      ![chlimage_1-271](assets/chlimage_1-271.png)

1. Sélectionnez le texte et copiez-le dans le navigateur Web pour prévisualiser la ressource ou l’ajouter à la page de contenu Web.

   Pour quitter la fenêtre URL, appuyez sur le **[!UICONTROL X]** ou appuyez sur **[!UICONTROL Fermer]**.

## Obtention d’une URL pour une ressource statique {#obtaining-a-url-for-a-static-asset}

Dynamic Media prend en charge le déploiement de ressources statiques, qui sont des ressources supplémentaires au-delà des images et de la vidéo. Les formats de ressources statiques pris en charge pour la diffusion comprennent les formats suivants :

* GIF animé
* Fichiers audio
* CSS
* JavaScript (lorsque votre entreprise est configurée avec son propre domaine)
* PDF
* SVG
* XML
* ZIP

**Pour obtenir une URL pour un fichier statique**

1. Accédez au fichier *statique *publié dont vous souhaitez copier l’URL, puis appuyez sur le fichier pour l’ouvrir.

   N’oubliez pas que les URL ne peuvent être copiées qu’*après* la *publication* de la ressource statique.

   Voir [Publication de ressources](publishing-dynamicmedia-assets.md).

1. Utilisez l’une des méthodes suivantes pour obtenir l’URL de la ressource statique publiée :

   * `The URL of the published static is the following:`

      * `https://*<server_name>*/is/content/*<company_name>*/*<static_asset_filename>*.*<extension>*`

         Par exemple, `https://aem.com/is/content/adobe/image.gif`.
   * click **[!UICONTROL Asset > Dynamic Renditions]**, then tap a dynamic rendition of the static asset and copy the URL.

      Change the copied URL to use `is/content` in the path instead of `is/image/`.


## Obtention d’une URL de vidéo pour un rendu vidéo publié {#obtaining-a-video-url-for-a-published-video-rendition}

1. In AEM, navigate to **[!UICONTROL Tools > Deployment > Cloud > Cloud Services]**.
1. On the **[!UICONTROL Cloud Services]** page, scroll down to the **[!UICONTROL Dynamic Media Cloud Services]** heading, then tap **[!UICONTROL Show Configurations]**.
1. Under **[!UICONTROL Available Configurations]**, tap the name of the configuration you want.

1. On the **[!UICONTROL Dynamic Media Cloud Settings]** page, under **[!UICONTROL Video Service URL]**, copy down the entire URL path. Vous aurez besoin de l’URL copiée dans les étapes suivantes.

   Par exemple, le chemin URL est similaire au suivant :

   `https://s7athens.macromedia.com:9090/DMGateway/`

   (Le chemin ci-dessus est donné à titre d’illustration uniquement ; il ne s’agit pas de celui que vous allez copier.) 

1. Sous **[!UICONTROL ID d’enregistrement]**, copiez le nom du client dans la dernière partie de l’ID.

   For example, if the registration ID was `87654321|MyCompany`, the customer name would be `MyCompany`.

1. Près du coin supérieur gauche de la page, appuyez sur **[!UICONTROL Cloud Services**, puis appuyez sur le logo Experience Manager et accédez à **[!UICONTROL Général > CRXDE Lite]**.
1. Copiez le chemin URL du rendu vidéo à partir du référentiel JCR (Java Content Repository).

   Par exemple, le chemin URL du rendu vidéo est similaire au suivant :

   `/_renditions_/0bd/0bd28743-a616-4fe6-92aa-6eae7c2112f/avs/Momentum_1080-0x720-2600k.mp4`

   (Le chemin ci-dessus est donné à titre d’illustration uniquement ; il ne s’agit pas de celui que vous allez copier.) 

1. Organisez les informations copiées dans l’ordre suivant pour former un chemin URL complet :

   `<Video_Service_URL>/public/<Customer_name_from_Registration_ID>/<Video_rendition_path>`

   Par exemple, à l’aide des exemples de chemins et de l’exemple de nom de client des étapes ci-dessus, le chemin complet s’affiche comme suit :

   `https://s7athens.macromedia.com:9090/DMGateway/public/MyCompany/_renditions_/0bd/0bd28743-a616-4fe6-92aa-6eae7c2112ff/avs/Momentum_1080-0x720-2600k.mp4`

   Il s’agit de l’URL complet d’un rendu vidéo publié.

## Obtention d’une URL de vidéo pour la diffusion adaptative (TLS) {#obtaining-a-video-url-for-adaptive-streaming-hls}

1. In AEM, navigate to **[!UICONTROL Tools > Deployment > Cloud > Cloud Services]**.
1. On the **[!UICONTROL Cloud Services]** page, scroll down to the **[!UICONTROL Dynamic Media Cloud Services]** heading, then tap **[!UICONTROL Show Configurations]**.
1. Under **[!UICONTROL Available Configurations]**, tap the name of the configuration you want.
1. On the **[!UICONTROL Dynamic Media Cloud Services Settings]** page, do the following:

   * Sous **[!UICONTROL URL du service vidéo]**, copiez le chemin d’URL entier. Vous aurez besoin de l’URL copiée dans ces étapes. Par exemple, le chemin URL est similaire au suivant :
   `https://gateway-na.assetsadobe.com/DMGateway/`

   (Le chemin ci-dessus est donné à titre d’illustration uniquement ; il ne s’agit pas de celui que vous allez copier.) 

   * Sous **[!UICONTROL ID d’enregistrement]**, copiez le nom du client dans la dernière partie de l’ID. Vous aurez besoin du nom du client copié plus tard au cours de ces étapes.

      For example, if the registration ID was `87654321|demoCo`, the customer name you copy would be `demoCo`.


1. En fonction du protocole de diffusion vidéo que vous utilisez, copiez le sélecteur de protocole correspondant. Vous aurez besoin du sélecteur de protocole copié plus tard au cours de ces étapes.

   | Protocole de diffusion vidéo que vous utilisez | Sélecteur de protocole à utiliser |
   |---|---|
   | HTTP <br> Si vous utilisez HTTP (diffusion vidéo non sécurisée), veillez à remplacer https par http dans la valeur URL du service vidéo que vous avez copiée précédemment. | `public/` |
   | HTTPS | `public-ssl/` |

1. Copiez le chemin complet de la ressource vidéo dans AEM, tel qu’il est traité par Dynamic Media. Vous aurez besoin de ce chemin d’accès à la ressource vidéo copié dans ces étapes.

   Par exemple :

   `/content/dam/marketing/MyVideo.mp4`

1. Combinez tous les éléments copiés précédemment pour créer une chaîne dans l’ordre suivant :

   &lt; `video service URL`>&lt; `protocol selector`>&lt; `customer name`>&lt; `video asset path`>

   Par exemple, en utilisant les informations copiées à partir des exemples de ces étapes, la chaîne apparaît comme suit :

   `https://gateway-na.assetsadobe.com/DMGateway/public-ssl/demoCo/content/dam/marketing/MyVideo.mp4`

1. Complete the URL by appending `.m3u8` to the end of the string. For example, appending `.m3u8` to the string from the previous step, the complete URL path would appear as follows:

   `https://gateway-na.assetsadobe.com/DMGateway/public-ssl/demoCo/content/dam/marketing/MyVideo.mp4.m3u8`

## Utilisation de HTTP/2 pour diffuser vos ressources Dynamic Media {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2 est le nouveau protocole web qui améliore la manière dont les serveurs et les navigateurs communiquent. Il permet un transfert rapide d’informations et réduit la puissance de traitement nécessaire. Les ressources Dynamic Media peuvent désormais être diffusées sur HTTP/2, un protocole qui garantit de meilleurs temps de réponse et de chargement.

Voir [Diffusion du contenu sur HTTP/2](http2.md) pour tout savoir sur l’utilisation du protocole HTTP/2 avec votre compte Dynamic Media.
