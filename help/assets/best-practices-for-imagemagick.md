---
title: Installation et configuration d’ImageMagick
description: Découvrez le logiciel ImageMagick, comment l’installer, configurer l’étape de processus de ligne de commande et l’utiliser pour modifier, composer et générer des miniatures à partir d’images.
contentOwner: AG
role: Admin
feature: Renditions,Developer Tools
exl-id: 6c149d31-1e64-4d29-a32a-58bd69e9fa98
source-git-commit: b2faf81983216bef9151548d90ae86f1c26a9f91
workflow-type: ht
source-wordcount: '693'
ht-degree: 100%

---

# Installation et configuration d’ImageMagick pour une utilisation avec [!DNL Experience Manager Assets] {#install-and-configure-imagemagick-to-work-with-aem-assets}

ImageMagick est un module externe logiciel servant à créer, modifier, composer ou convertir des images bitmap. Il peut lire et écrire des images dans plusieurs formats (plus de 200), dont PNG, JPEG, JPEG-2000, GIF, TIFF, DPX, EXR, WebP, Postscript, PDF et SVG. Utilisez ImageMagick pour redimensionner, réaliser une symétrie, effectuer un miroir, faire pivoter, déformer, cisailler et transformer des images. Vous pouvez également régler les couleurs des images, ainsi qu’appliquer divers effets spéciaux, ou tracer du texte, des lignes, des polygones, des ellipses et des courbes à l’aide d’ImageMagick.

Utilisez le gestionnaire de médias d’[!DNL Adobe Experience Manager] à partir de la ligne de commande afin de traiter les images via ImageMagick. Pour utiliser plusieurs formats de fichiers avec ImageMagick, voir [Meilleures pratiques relatives au format de fichier des ressources](/help/assets/assets-file-format-best-practices.md). Pour connaître tous les formats de fichiers pris en charge, voir [Formats de ressources pris en charge](/help/assets/assets-formats.md).

Pour traiter des fichiers volumineux à l’aide d’ImageMagick, veuillez tenir compte de besoins en mémoire plus élevés que d’habitude, des modifications potentielles requises pour les stratégies IM, ainsi que de l’impact global sur les performances. La mémoire requise dépend de divers facteurs tels que la résolution, la profondeur des couleurs, le profil colorimétrique et le format de fichier. Si vous envisagez de traiter des fichiers très volumineux à l’aide d’ImageMagick, effectuez correctement le test des performances du serveur [!DNL Experience Manager]. Certaines ressources utiles sont fournies à la fin.

>[!NOTE]
>
>Si vous utilisez [!DNL Experience Manager] dans [!DNL Adobe Managed Services] (AMS), contactez l’assistance clientèle d’Adobe si vous prévoyez de traiter de nombreux fichiers PSD ou PSB haute résolution. Il se peut qu’[!DNL Experience Manager] ne puisse pas traiter des fichiers PSB à très haute résolution, de plus de 30 000 x 23 000 pixels.

## Installation d’ImageMagick {#installing-imagemagick}

Plusieurs versions des fichiers d’installation d’ImageMagic sont disponibles pour les différents systèmes d’exploitation. Utilisez la version appropriée pour votre système d’exploitation.

1. Téléchargez les [fichiers d’installation d’ImageMagick](https://www.imagemagick.org/script/download.php) adaptés à votre système d’exploitation.
1. Pour installer ImageMagick sur le disque hébergeant le serveur [!DNL Experience Manager], lancez le fichier d’installation.

1. Définissez la variable de chemin d’environnement sur le répertoire d’installation d’ImageMagick.
1. Pour vérifier si l’installation est réussie, exécutez la commande `identify -version`.

## Configuration de l’étape de processus de ligne de commande {#set-up-the-command-line-process-step}

Vous pouvez configurer l’étape de processus de ligne de commande en fonction de votre cas d’utilisation. Effectuez les étapes suivantes pour générer une image inversée et des miniatures (140 x 100, 48 x 48, 319 x 319 et 1 280 x 1 280) chaque fois que vous ajoutez un fichier image JPEG dans `/content/dam` sur le serveur [!DNL Experience Manager] :

1. Sur le serveur [!DNL Experience Manager], accédez à la console Workflow (`https://[aem_server]:[port]/workflow`) et ouvrez le modèle de workflow **[!UICONTROL Ressource de mise à jour de la gestion des ressources numériques]**.
1. À partir du modèle de workflow **[!UICONTROL Ressource de mise à jour de la gestion des ressources numériques]**, ouvrez l’étape **[!UICONTROL Miniatures EPS (avec la technologie ImageMagick)]**.
1. Sous l’**[!UICONTROL onglet Arguments]**, ajoutez `image/jpeg` à la liste **[!UICONTROL Types MIME]**.

   ![mime_types_jpeg](assets/mime_types_jpeg.png)

1. Dans le champ **[!UICONTROL Commandes]**, saisissez la commande suivante :

   `convert ./${filename} -flip ./${basename}.flipped.jpg`

1. Sélectionnez les indicateurs **[!UICONTROL Supprimer le rendu généré]** et **[!UICONTROL Générer le rendu Web]**.

   ![select_flags](assets/select_flags.png)

1. Sous l’onglet **[!UICONTROL Image activée pour le Web]**, spécifiez les détails du rendu avec des dimensions de 1 280 x 1 280 pixels. En outre, entrez `image/jpeg` dans le champ **[!UICONTROL Mimetype]**.

   ![Web_enabled_image](assets/web_enabled_image.png)

1. Pour enregistrer les modifications, cliquez sur **[!UICONTROL OK]**.

   >[!NOTE]
   >
   >La commande `convert` peut ne pas s’exécuter avec certaines versions de Windows (par exemple, Windows SE), car elle entre en conflit avec l’utilitaire `convert` natif qui fait partie de l’installation de Windows. Dans ce cas, précisez le chemin complet de l’utilitaire ImageMagick. Par exemple, spécifiez :
   >
   >
   >`"C:\Program Files\ImageMagick-6.8.9-Q16\convert.exe" -define jpeg:size=319x319 ./${filename} -thumbnail 319x319 cq5dam.thumbnail.319.319.png`

1. Ouvrez l’étape **[!UICONTROL Miniatures des processus]** et ajoutez le type MIME `image/jpeg` sous **[!UICONTROL Types MIME ignorés]**.

   ![skip_mime_types](assets/skip_mime_types.png)

1. Sous l’onglet **[!UICONTROL Image activée pour le Web]**, ajoutez le type MIME `image/jpeg` sous **[!UICONTROL Liste à ignorer]**. Pour enregistrer les modifications, cliquez sur **[!UICONTROL OK]**.

   ![Web_enabled](assets/web_enabled.png)

1. Enregistrez le workflow.

1. Pour vérifier que le traitement est correct, chargez une image de JPG vers [!DNL Assets]. Une fois le traitement terminé, vérifiez si une image inversée et les rendus sont générés ou non.

## Réduction des vulnérabilités en matière de sécurité {#mitigating-security-vulnerabilities}

Il existe plusieurs vulnérabilités de sécurité liées à l’utilisation d’ImageMagick pour traiter les images. Par exemple, le traitement d’images envoyées par l’utilisateur entraîne un risque d’exécution de code à distance (RCE).

En outre, plusieurs modules externes de traitement d’images dépendent de la bibliothèque ImageMagick, y compris, sans s’y limiter, imagick de PHP, rmagick et paperclip de Ruby, et imagemagick de nodejs.

Si vous utilisez ImageMagick ou une bibliothèque affectée, Adobe vous recommande de limiter les vulnérabilités connues en réalisant au moins l’une des tâches suivantes (de préférence les deux) :

1. Vérifiez que tous les fichiers image commencent par les [« octets magiques »](https://en.wikipedia.org/wiki/List_of_file_signatures) attendus, correspondant aux types de fichier image que vous prenez en charge avant de les envoyer à ImageMagick pour le traitement.
1. Utilisez un fichier de régulation pour désactiver les codes vulnérables d’ImageMagick. La stratégie globale pour ImageMagick se trouve dans `/etc/ImageMagick`.
