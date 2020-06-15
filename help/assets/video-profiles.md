---
title: Profils vidéo
description: Dynamic Media est fourni avec un profil prédéfini de codage vidéo adaptatif. Les paramètres de ce profil prêt à l’emploi sont optimisés pour offrir à vos clients la meilleure expérience de visionnage possible. Vous pouvez également ajouter un recadrage intelligent à vos vidéos.
uuid: 26a20984-db63-41e9-b16c-6e164b7596a0
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
discoiquuid: 3b8791c8-2c97-42b7-b4a9-e1157ac9ea02
docset: aem65
translation-type: tm+mt
source-git-commit: df89d5cfd5060d493babb89e92a9a98e851b8879
workflow-type: tm+mt
source-wordcount: '3707'
ht-degree: 98%

---


# Profils vidéo {#video-profiles}

Dynamic Media est fourni avec un profil prédéfini de codage vidéo adaptatif. Les paramètres de ce profil prêt à l’emploi sont optimisés pour offrir à vos clients la meilleure expérience de visionnage possible. Lorsque vous codez vos vidéos sources principales à l’aide du profil de codage de vidéo adaptative, le lecteur vidéo ajuste automatiquement la qualité du flux vidéo en fonction de la vitesse de connexion Internet de vos clients pendant la lecture. Ce processus est appelé diffusion en continu adaptative.

Voici d’autres facteurs qui déterminent la qualité des vidéos :

* **Résolution de la vidéo source principale téléchargée**

   Si la vidéo MP4 a été enregistrée à une résolution moins élevée, telle que 240p ou 360p, elle ne peut pas être diffusée en haute définition en continu.

* **Taille du lecteur vidéo**

   Par défaut, la largeur du profil de codage de vidéo adaptative est définie sur Auto. Là encore, pendant la lecture, la meilleure qualité est utilisée en fonction de la taille du lecteur.

Voir [Bonnes pratiques en matière de codage vidéo](/help/assets/video.md#best-practices-for-encoding-videos).

Consultez également la section [Bonnes pratiques pour organiser vos ressources numériques en vue d’utiliser des profils de traitement](/help/assets/organize-assets.md).

>[!NOTE]
>
>Pour générer les métadonnées d’une vidéo et les miniatures associées, la vidéo doit passer par le processus de codage dans Dynamic Media. Dans AEM, le workflow **[!UICONTROL Vidéo de codage de média dynamique]** code la vidéo si vous avez activé les médias dynamiques et configuré des services cloud de vidéo. Ce workflow capture l’historique de traitement des workflows et les informations d’échec. Voir [Surveillance du codage vidéo et de la progression de la publication sur YouTube](/help/assets/video.md#monitoring-video-encoding-and-youtube-publishing-progress). Si vous avez activé Dynamic Media et configuré les services cloud vidéo, le workflow **[!UICONTROL vidéo d’encodage Dynamic Media]** prend automatiquement effet lorsque vous chargez une vidéo. (Si vous n’utilisez pas Dynamic Media, le workflow **[!UICONTROL Ressource de mise à jour DAM]** prend effet.)
>
>Les métadonnées sont utiles lorsque vous recherchez des ressources. Les miniatures sont des images vidéo statiques qui sont générées lors du codage. Elles sont requises par le système AEM et utilisées dans l’interface utilisateur pour vous aider à identifier visuellement des vidéos en mode Carte, dans les résultats de recherche et dans la liste des ressources. Vous pouvez consulter les miniatures générées en appuyant sur l’icône Rendus (palette de peintre) d’une vidéo codée.

Une fois le profil vidéo créé, vous l’appliquez à un ou à plusieurs dossiers. Voir [Application d’un profil vidéo à des dossiers.](#applying-a-video-profile-to-folders)

Pour définir des paramètres de traitement avancés pour d’autres types de ressources, voir [Configuration du traitement des ressources](/help/assets/config-dms7.md#configuring-asset-processing).

Voir également [Profils de traitement des métadonnées, des images et des vidéos](processing-profiles.md).

## Paramètres prédéfinis de codage vidéo adaptatif {#adaptive-video-encoding-presets}

Le tableau ci-après identifie les profils de codage recommandés pour la diffusion en continu de vidéo adaptative sur les appareils mobiles, les tablettes et les postes de travail. Vous pouvez utiliser ces paramètres prédéfinis pour n’importe quel rapport largeur/hauteur.

<table>
 <tbody>
  <tr>
   <td><strong>Codec du format vidéo</strong></td>
   <td><strong>Taille de la vidéo - Largeur (px)</strong></td>
   <td><strong>Taille de la vidéo - Hauteur (px)</strong></td>
   <td><strong>Conserver les proportions ?</strong></td>
   <td><strong>Débit vidéo (kbit/s)</strong></td>
   <td><strong>Taux de rafraîchissement vidéo (i/s)</strong></td>
   <td><strong>Codec audio</strong></td>
   <td><strong>Débit audio  (kbit/s)</strong></td>
  </tr>
  <tr>
   <td><p>MP4 H.264 (mp4)</p> </td>
   <td>auto</td>
   <td>360</td>
   <td>Oui</td>
   <td>730</td>
   <td>30</td>
   <td>Dolby HE-AAC</td>
   <td>128</td>
  </tr>
  <tr>
   <td><p>MP4 H.264 (mp4)</p> </td>
   <td>auto</td>
   <td>540</td>
   <td>Oui</td>
   <td>2000<br /> </td>
   <td>30</td>
   <td>Dolby HE-AAC</td>
   <td>128</td>
  </tr>
  <tr>
   <td><p>MP4 H.264 (mp4)</p> </td>
   <td>auto</td>
   <td>720<br /> </td>
   <td>Oui</td>
   <td>3000<br /> </td>
   <td>30</td>
   <td>Dolby HE-AAC</td>
   <td>128</td>
  </tr>
 </tbody>
</table>

## À propos de l’utilisation du recadrage intelligent dans les profils vidéo {#about-smart-crop-video}

Le recadrage intelligent pour la vidéo (une fonctionnalité en option dans les profils vidéo) est un outil qui utilise la puissance de l’intelligence artificielle d’Adobe Sensei pour détecter et rogner automatiquement le point focal dans toute vidéo adaptative ou progressive que vous avez chargée, quelle que soit sa taille.

Les formats vidéo pris en charge par le recadrage intelligent sont MP4, MKV, MOV, AVI, FLV et WMV.

La taille maximale de fichier vidéo prise en charge par le recadrage intelligent correspond aux critères suivants :

* Durée de cinq minutes
* 30 images par seconde (i/s)
* Taille de fichier de 300 Mo

Notez qu’Adobe Sensei est actuellement limité à 9 000 images. C’est-à-dire cinq minutes à 30 i/s. Si votre vidéo présente une fréquence d’images supérieure, la durée de vidéo maximale prise en charge diminue. Par exemple, une vidéo de 60 i/s doit durer deux minutes et demie pour être prise en charge par Adobe Sensei et par le recadrage intelligent.

![Recadrage intelligent de vidéo](assets/smart-crop-video.png)

>[!IMPORTANT]
>
>Pour que le recadrage intelligent de vidéo fonctionne, vous devez inclure au moins un paramètre prédéfini de codage vidéo dans votre profil vidéo.

Pour utiliser le recadrage intelligent de vidéo, vous créez un profil de codage de vidéo adaptative ou progressive. Dans votre profil, utilisez l’outil **[!UICONTROL Smart Crop Ratio]** pour sélectionner des proportions prédéfinies. Par exemple, après avoir défini vos paramètres prédéfinis de codage vidéo, vous pouvez ajouter une définition Paysage mobile avec des proportions de 16x9 et une définition Portrait mobile avec des proportions de 9x16. Les autres proportions ou rapports de recadrage que vous pouvez choisir sont 1x1, 4x3 et 4x5.

![Modification d’un profil de codage vidéo avec le recadrage intelligent](assets/edit-smart-crop-video2.png)

Notez que vous pouvez activer ou désactiver le recadrage intelligent de vidéo dans le profil vidéo à l’aide du curseur à l’extrémité droite de **[!UICONTROL Smart Crop Ratio]** dans l’interface utilisateur.

Après avoir créé et enregistré votre profil vidéo, vous pouvez l’appliquer aux dossiers de votre choix.

Voir [Application de profils vidéo à des dossiers spécifiques](#applying-video-profiles-to-specific-folders) ou [Application d’un profil vidéo à l’ensemble des ressources](#applying-a-video-profile-globally).

Voir aussi [Recadrage intelligent d’images](image-profiles.md).

## Création d’un profil vidéo pour la diffusion en continu adaptative {#creating-a-video-encoding-profile-for-adaptive-streaming}

Dynamic Media est fourni avec un profil prédéfini de codage de vidéo adaptative (groupe de paramètres de chargement vidéo pour MP4 H.264) qui est optimisé pour la visualisation. Vous pouvez utiliser ce profil lorsque vous chargez vos vidéos.

Cependant, si ce profil prédéfini ne répond pas à vos besoins, vous pouvez choisir de créer votre propre profil de codage de vidéo adaptative. Lorsque vous utilisez le paramètre **[!UICONTROL Coder pour la diffusion en continu adaptative]** (tel que recommandé), tous les paramètres prédéfinis de codage que vous ajoutez au profil sont validés afin de vous assurer que toutes les vidéos ont les mêmes proportions. En outre, les vidéos codées sont traitées comme un ensemble à débit multiple pour la diffusion en continu.

Lors de la création du profil de codage vidéo, vous pouvez remarquer que la plupart des options sont préremplies avec les paramètres par défaut recommandés. Si vous sélectionnez une valeur autre que celle par défaut recommandée, vous risquez d’obtenir une qualité vidéo médiocre pendant la lecture et de rencontrer d’autres problèmes de performances.

Pour tous les paramètres prédéfinis de codage vidéo MP4 H.264 du profil, les valeurs suivantes sont donc validées pour s’assurer qu’elles sont identiques dans chaque paramètre prédéfini, rendant ainsi possible la diffusion en continu adaptative :

* Codec de format vidéo - MP4 H.264 (.mp4)
* Codec audio
* Débit audio
* Conserver les proportions
* Codage à deux passages
* Débit constant
* Profil H264
* Taux d’échantillonnage audio

Si les valeurs ne sont pas identiques, vous pouvez continuer à créer le profil tel quel. Sachez toutefois que la diffusion en continu adaptative ne sera pas possible. Les utilisateurs vivront à la place une expérience de diffusion en continu à un seul débit. Il est recommandé de modifier les paramètres de codage afin d’utiliser les mêmes valeurs dans chaque paramètre prédéfini de codage du profil. (Notez que l’éditeur de profil vidéo/paramètre prédéfini doit appliquer la parité des paramètres de codage de vidéo adaptative si l’option « Coder pour la diffusion en continu adaptative » est activée.)

Voir aussi [Création d’un profil de codage vidéo pour la diffusion en continu progressive](#creating-a-video-encoding-profile-for-progressive-streaming).

Consultez également la section [Pratiques recommandées pour le codage vidéo](/help/assets/video.md#best-practices-for-encoding-videos).

Pour définir des paramètres de traitement avancés pour d’autres types de ressources, voir [Configuration du traitement des ressources](/help/assets/config-dms7.md#configuring-asset-processing).

**Pour créer un profil de codage vidéo en vue de la diffusion en continu adaptative** :

1. Appuyez sur le logo AEM et accédez à **[!UICONTROL Outils]** > **[!UICONTROL Ressources]** > **[!UICONTROL Profils vidéo]**.
1. Cliquez ou appuyez sur **[!UICONTROL Créer]** pour ajouter un nouveau profil vidéo.

1. Saisissez un nom et une description pour le profil.
1. Sur la page Créer/Modifier des paramètres prédéfinis de codage vidéo, appuyez sur **[!UICONTROL Ajouter un paramètre prédéfini de codage vidéo]**.
1. Définissez les options audio et vidéo dans l’onglet **[!UICONTROL De base]**.
Appuyez sur l’icône d’information en regard de chaque option pour accéder à des descriptions supplémentaires ou des paramètres recommandés en fonction du codec vidéo sélectionné.
1. Dans la section Taille de la vidéo, assurez-vous que la case **[!UICONTROL Conserver les proportions]** est cochée.
1. Définissez la résolution de l’image vidéo en pixels. Utilisez la valeur **[!UICONTROL Auto]** pour la mettre automatiquement à l’échelle en fonction des proportions de la source (rapport largeur/hauteur). Par exemple, Auto x 480 ou 640 x Auto.

1. Utilisez l’une des méthodes suivantes :

   * Dans le champ **[!UICONTROL Largeur]**, saisissez **[!UICONTROL auto]**. Dans le champ **[!UICONTROL Hauteur]**, saisissez une valeur en pixels.

   * Pour visualiser plus facilement la taille de la vidéo, appuyez sur l’icône Informations (i) située à droite de **[!UICONTROL Hauteur]** afin d’ouvrir la page Calcul de la taille. Utilisez la page **[!UICONTROL Calcul de la taille]** pour définir les dimensions vidéo (représentées par la zone bleue) souhaitées. Appuyez sur **[!UICONTROL X]** dans le coin supérieur droit lorsque vous avez terminé.

1. (Facultatif) Appuyez sur l’onglet **[!UICONTROL Avancé]** et assurez-vous que la case **[!UICONTROL Utiliser les valeurs par défaut]** est cochée (recommandé). Vous pouvez également modifier les paramètres vidéo et audio avancés.
1. Dans le coin supérieur droit de la page, appuyez sur **[!UICONTROL Enregistrer]** pour enregistrer le paramètre prédéfini.
1. Utilisez l’une des méthodes suivantes :
   * Répétez les étapes 4 à 10 pour créer d’autres paramètres de codage prédéfinis. (La diffusion vidéo adaptative en continu nécessite plusieurs paramètres prédéfinis vidéo.)
   * Passez à l’étape suivante.

1. (Facultatif) Pour ajouter un recadrage intelligent aux vidéos auxquelles ce profil sera appliqué, procédez comme suit :
   * Sur la page Modifier le profil vidéo, à droite de l’en-tête Smart Crop Ratio, appuyez sur **[!UICONTROL Ajouter]**.
   * Dans le champ Nom, entrez un nom qui vous aidera à identifier facilement le rapport de recadrage.
   * Dans la liste déroulante **[!UICONTROL Rapport de recadrage]**, sélectionnez le rapport à utiliser.

1. Utilisez l’une des méthodes suivantes :

   * Continuez à ajouter de nouveaux rapports de recadrage si nécessaire.
   * Passez à l’étape suivante.

1. Dans le coin supérieur droit de la page, appuyez à nouveau sur **[!UICONTROL Enregistrer]** pour enregistrer le profil.

Vous pouvez maintenant appliquer le profil aux dossiers contenant des vidéos. Voir [Application d’un profil vidéo à des dossiers](#applying-a-video-profile-to-folders) ou [Application d’un profil vidéo à l’ensemble des ressources](#applying-a-video-profile-globally).

## Création d’un profil vidéo pour la diffusion de vidéo progressive en continu {#creating-a-video-encoding-profile-for-progressive-streaming}

Si vous choisissez de ne pas utiliser l’option **[!UICONTROL Coder pour la diffusion en continu adaptative]**, sachez que tous les paramètres prédéfinis de codage que vous ajoutez au profil sont traités comme des rendus vidéo séparés pour la diffusion en continu à un seul débit ou progressive. De plus, aucune validation n’est effectuée pour s’assurer que tous les rendus vidéo ont le même rapport largeur/hauteur.

En fonction du mode que vous exécutez, les codecs de format vidéo pris en charge sont les suivants :

* Mode Dynamic Media-Scene7 : H.264 (.mp4)
* Mode Dynamic Media-hybride : H.264 (.mp4), WebM

Voir aussi [Création d’un profil de codage vidéo pour la diffusion en continu adaptative](#creating-a-video-encoding-profile-for-adaptive-streaming).

Consultez également la section [Pratiques recommandées pour le codage vidéo](/help/assets/video.md#best-practices-for-encoding-videos).

Pour définir des paramètres de traitement avancés pour d’autres types de ressources, voir [Configuration du traitement des ressources](/help/assets/config-dms7.md#configuring-asset-processing).

**Pour créer un profil vidéo en vue de la diffusion en continu progressive :**

1. Appuyez sur le logo AEM et accédez à **[!UICONTROL Outils]** > **[!UICONTROL Ressources]** > **[!UICONTROL Profils vidéo]**.
1. Appuyez sur **[!UICONTROL Créer]** pour ajouter un nouveau profil vidéo.
1. Saisissez un nom et une description pour le profil.
1. Sur la page Créer/Modifier des paramètres prédéfinis de codage vidéo, appuyez sur **[!UICONTROL Ajouter un paramètre prédéfini de codage vidéo]**.
1. Définissez les options audio et vidéo dans l’onglet **[!UICONTROL De base]**.
Appuyez sur l’icône d’information en regard de chaque option pour accéder à des descriptions supplémentaires ou des paramètres recommandés en fonction du codec vidéo sélectionné.
1. (Facultatif) Dans la section Taille de la vidéo, désélectionnez la case **[!UICONTROL Conserver les proportions]**.
1. Procédez comme suit :
   * Dans le champ **[!UICONTROL Largeur]**, saisissez **[!UICONTROL auto]**.
   * Dans le champ **[!UICONTROL Hauteur]**, saisissez une valeur en pixels.
Pour visualiser plus facilement la taille de la vidéo, appuyez sur l’icône d’informations de hauteur pour ouvrir la page **[!UICONTROL Calcul de la taille]**. Utilisez la page **[!UICONTROL Calcul de la taille]** pour définir les dimensions de votre choix pour la vidéo (encadré bleu). Lorsque vous avez terminé, dans le coin supérieur droit de la boîte de dialogue, appuyez sur **[!UICONTROL X]**.
1. (Facultatif) Effectuez l’une des opérations suivantes :

   * Appuyez sur l’onglet **[!UICONTROL Avancé]** et assurez-vous que la case **[!UICONTROL Utiliser les valeurs par défaut]** est cochée (recommandé).

   * Désélectionnez la case **[!UICONTROL Utiliser les valeurs par défaut]** et spécifiez les paramètres vidéo et audio de votre choix.
Appuyez sur l’icône d’information en regard de chaque option pour accéder à des descriptions supplémentaires ou des paramètres recommandés en fonction du codec vidéo sélectionné.

1. Dans le coin supérieur droit de la page, appuyez sur **[!UICONTROL Enregistrer]** pour enregistrer le paramètre prédéfini.
1. Utilisez l’une des méthodes suivantes :

   * Répétez les étapes 4 à 9 pour créer d’autres paramètres de codage prédéfinis.
   * Passez à l’étape suivante.

1. (Facultatif) Pour ajouter un recadrage intelligent aux vidéos auxquelles ce profil sera appliqué, procédez comme suit :

   * Sur la page Modifier le profil vidéo, à droite de l’en-tête Smart Crop Ratio, appuyez sur **[!UICONTROL Ajouter]**.
   * Dans le champ Nom, entrez un nom qui vous aidera à identifier facilement le rapport de recadrage.
   * Dans la liste déroulante **[!UICONTROL Rapport de recadrage]**, sélectionnez le rapport à utiliser.

1. Utilisez l’une des méthodes suivantes :

   * Continuez à ajouter de nouveaux rapports de recadrage si nécessaire.
   * Passez à l’étape suivante.

1. Dans le coin supérieur droit de la page, appuyez sur **[!UICONTROL Enregistrer]** pour enregistrer le profil.

Vous pouvez maintenant appliquer le profil aux dossiers contenant des vidéos. Voir [Application d’un profil vidéo à des dossiers](#applying-a-video-profile-to-folders) ou [Application d’un profil vidéo à l’ensemble des ressources](#applying-a-video-profile-globally).

## Utilisation de paramètres de codage vidéo personnalisés {#using-custom-added-video-encoding-parameters}

Vous pouvez modifier un profil de codage vidéo existant pour tirer parti de paramètres de codage vidéo avancés qui ne figurent pas dans l’interface utilisateur lors de la création ou de la modification d’un profil vidéo dans AEM. Vous pouvez ajouter un ou plusieurs paramètres avancés personnalisés à votre profil existant, comme minBitrate et maxBitrate.

**Pour utiliser des paramètres de codage vidéo personnalisés, procédez comme suit** :

1. Appuyez sur le logo AEM, puis accédez à **[!UICONTROL Outils]** > **[!UICONTROL Général]** > **[!UICONTROL CRXDE Lite]**.
1. À partir de la page CRXDE Lite, dans le panneau Explorateur à gauche, accédez au répertoire suivant :

   `/conf/global/settings/dam/dm/presets/video/*name_of_video_encoding_profile_to_edit`

1. Dans le panneau situé en bas à droite de la page, accédez à l’onglet Propriétés et spécifiez les champs **[!UICONTROL Nom]**, **[!UICONTROL Type]** et **[!UICONTROL Valeur]** du paramètre à utiliser.

   Les paramètres avancés suivants sont disponibles :

<table>
 <tbody>
  <tr>
   <td><strong>Nom</strong></td>
   <td><strong>Description</strong><br /> </td>
   <td><strong>Type</strong><br /> </td>
   <td><strong>Valeur</strong></td>
  </tr>
  <tr>
   <td><code>h264Level</code></td>
   <td>Niveau H.264 à utiliser pour le codage. Normalement, cette valeur est automatiquement déterminée en fonction des paramètres de codage que vous utilisez.</td>
   <td><code>String</code></td>
   <td><p>10 x niveau h264</p> <p>Par exemple, 3.0 = 30, 1.3 = 13)</p> <p>Pas de valeur par défaut.</p> </td>
  </tr>
  <tr>
   <td><code>keyframe</code></td>
   <td>Nombre cible d’images entre les images clés. Calculez cette valeur pour générer une image clé toutes les 2 à 10 secondes. Par exemple, à 30 images par seconde, l’intervalle d’images clé doit être compris entre 60 et 300.<br /> <br /> Les intervalles d’images clé moindres améliorent le comportement de recherche de flux et de changement de flux pour les codages vidéo adaptatifs et peuvent également améliorer la qualité des vidéos avec beaucoup de mouvement. Cependant, puisque les images clés augmentent la taille du fichier, un intervalle d’images clés moindre entraîne généralement une qualité de vidéo globalement moins bonne à un débit donné.</td>
   <td><code>String</code></td>
   <td><p>Numéro positif.</p> <p>La valeur par défaut est 300.</p> <p>La valeur recommandée pour HLS (HTTP Live Streaming) est comprise entre 60 et 90.</p> </td>
  </tr>
  <tr>
   <td><code>minBitrate</code></td>
   <td><p>Débit minimal pour permettre des codages à débit variable, en kbit/s (kilobits par seconde).</p> <p>Ce paramètre s’applique uniquement lorsque <strong>Utiliser le débit constant</strong> est désélectionné dans l’onglet Avancé quand vous créez ou modifiez un profil de codage vidéo.</p> <p>Voir aussi <a href="/help/assets/video.md#bitrate">Débit</a>.</p> </td>
   <td><code>String</code></td>
   <td><p>Nombre positif, en kbit/s.</p> <p>Pas de valeur par défaut.</p> </td>
  </tr>
  <tr>
   <td><code>maxBitrate</code></td>
   <td><p>Débit maximal pour permettre des codages à débit variable, en kbit/s.</p> <p>Ce paramètre s’applique uniquement lorsque <strong>Utiliser le débit constant</strong> est désélectionné dans l’onglet Avancé quand vous créez ou modifiez un profil de codage vidéo.</p> <p>Voir aussi <a href="/help/assets/video.md#bitrate">Débit</a>.</p> </td>
   <td><code>String</code></td>
   <td><p>Nombre positif, en kbit/s.</p> <p>Pas de valeur par défaut. Cependant, la valeur recommandée peut atteindre le double du débit de codage.</p> </td>
  </tr>
  <tr>
   <td><code>audioBitrateCustom</code></td>
   <td>Définissez la valeur sur <code>true</code> afin de forcer un débit constant pour le flux audio, si le codec audio le permet.</td>
   <td><code>String</code></td>
   <td><p><code>true</code>/<code>false</code></p> <p>La valeur par défaut est <code>false</code>.</p> <p>La valeur recommandée pour HLS (HTTP Live Streaming) est comprise entre et <code>false</code>.</p> <p> </p> </td>
  </tr>
 </tbody>
</table>

![chlimage_1-516](assets/chlimage_1-516.png)

1. Dans le coin inférieur droit de la page, appuyez sur **[!UICONTROL Ajouter]**.
1. Utilisez l’une des méthodes suivantes :

   * Répétez les étapes 3 et 4 pour ajouter un autre paramètre à votre profil de codage vidéo.
   * Dans le coin supérieur gauche de la page, appuyez sur **[!UICONTROL Tout enregistrer]**.

1. Dans le coin supérieur gauche de la page CRXDE Lite, appuyez sur l’icône **[!UICONTROL Retour à l’accueil]** pour revenir à AEM.

### Modification d’un profil vidéo {#editing-a-video-encoding-profile}

Vous pouvez modifier les profils vidéo que vous avez créés pour ajouter, modifier ou supprimer des paramètres vidéo prédéfinis.

Par défaut, vous ne pouvez pas modifier le profil **[!UICONTROL Codage vidéo adaptatif]** prédéfini prêt à l’emploi fourni avec Dynamic Media. Vous pouvez aussi facilement copier le profil et l’enregistrer sous un nouveau nom. Vous pouvez ensuite modifier les paramètres prédéfinis souhaités dans le profil copié.

Consultez également la section [Pratiques recommandées pour le codage vidéo](/help/assets/video.md#best-practices-for-encoding-videos).

Pour définir des paramètres de traitement avancés pour d’autres types de ressources, voir [Configuration du traitement des ressources](/help/assets/config-dms7.md#configuring-asset-processing).

**Pour modifier un profil vidéo** :

1. Appuyez sur le logo AEM et accédez à **[!UICONTROL Outils]** > **[!UICONTROL Ressources]** > **[!UICONTROL Profils vidéo]**.
1. Sur la page Profils vidéo, cochez un nom de profil vidéo.
1. Dans la barre d’outils, appuyez sur **[!UICONTROL Modifier]**.
1. Sur la page Profil de codage vidéo, modifiez le nom et la description, le cas échéant.
1. La bonne pratique consiste à vérifier que la case **[!UICONTROL Coder pour la diffusion en continu adaptative]** est cochée.
Appuyez sur l’icône d’information pour obtenir une description de la diffusion en continu adaptative. (Si vous modifiez un profil de vidéo progressive, ne cochez pas cette case.)
1. Sous le titre Paramètres prédéfinis de codage vidéo, ajoutez, modifiez ou supprimez des paramètres prédéfinis de codage vidéo qui constituent le profil.

   Appuyez sur l’icône d’information en regard de chaque option des onglets **[!UICONTROL De base]** et **[!UICONTROL Avancé]** pour accéder à des descriptions supplémentaires ou des paramètres recommandés en fonction du codec vidéo sélectionné.

1. Dans le coin supérieur droit de la page, appuyez sur **[!UICONTROL Enregistrer]**.

### Copie d’un profil vidéo {#copying-a-video-encoding-profile}

1. Appuyez sur le logo AEM et accédez à **[!UICONTROL Outils]** > **[!UICONTROL Ressources]** > **[!UICONTROL Profils vidéo]**.
1. Sur la page Profils vidéo, cochez un nom de profil vidéo.
1. Dans la barre d’outils, appuyez sur **[!UICONTROL Copier]**.
1. Sur la page Profil de codage vidéo, saisissez un nouveau nom pour le profil.
1. La bonne pratique consiste à vérifier que la case **[!UICONTROL Coder pour la diffusion en continu adaptative]** est cochée. Appuyez sur l’icône d’information pour obtenir une description de la diffusion en continu adaptative. (Si vous copiez un profil de vidéo progressive, ne cochez pas cette case.)

    Dans le mode hybride de Dynamic Media, si un paramètre prédéfini vidéo WebM fait partie du profil vidéo, l’option **[!UICONTROL Coder pour la diffusion en continu adaptative]** n’est pas disponible, car tous les paramètres prédéfinis doivent être des paramètres MP4.
1. Sous le titre Paramètres prédéfinis de codage vidéo, ajoutez, modifiez ou supprimez des paramètres prédéfinis de codage vidéo qui constituent le profil.

   Appuyez sur l’icône d’information en regard de chaque option dans les onglets De base et Avancé pour obtenir les paramètres recommandés et leurs descriptions.

1. Dans le coin supérieur droit de la page, appuyez sur **[!UICONTROL Enregistrer]**.

### Suppression d’un profil vidéo {#deleting-a-video-encoding-profile}

1. Appuyez sur le logo AEM et accédez à **[!UICONTROL Outils]** > **[!UICONTROL Ressources]** > **[!UICONTROL Profils vidéo]**.
1. Sur la page Profils vidéo, cochez un ou plusieurs noms de profil vidéo.
1. Dans la barre d’outils, appuyez sur **[!UICONTROL Supprimer]**.
1. Appuyez sur **[!UICONTROL OK]**.

## Application d’un profil vidéo à des dossiers  {#applying-a-video-profile-to-folders}

Lorsque vous affectez un profil vidéo à un dossier, tout sous-dossier hérite automatiquement du profil de son dossier parent. Cela signifie que vous ne pouvez affecter qu’un seul profil vidéo à un dossier. Nous vous conseillons donc de choisir avec la plus grande attention la structure du dossier dans lequel vous transférez, stockez, utilisez et archivez des ressources.

Si vous avez affecté un profil vidéo différent à un dossier, le nouveau profil remplace le précédent. Les ressources du dossier précédent restent inchangées. Le nouveau profil sera appliqué aux ressources ajoutées ultérieurement au dossier.

Les dossiers auxquels un profil est affecté sont indiqués dans l’interface utilisateur par le nom du profil apparaissant dans le nom de la carte.

![chlimage_1-517](assets/chlimage_1-517.png)

Vous pouvez appliquer des profils vidéo à des dossiers spécifiques ou à l’ensemble des ressources.

Vous pouvez retraiter des ressources dans un dossier qui comporte déjà un profil vidéo que vous avez modifié. Voir [Retraitement des ressources dans un dossier après avoir modifié son profil de traitement](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile).

### Application d’un profil vidéo à des dossiers spécifiques {#applying-video-profiles-to-specific-folders}

Vous pouvez appliquer un profil vidéo à un dossier depuis le menu **[!UICONTROL Outils]** ou, si vous vous trouvez dans le dossier, depuis **[!UICONTROL Propriétés]**. Cette section décrit comment appliquer des profils vidéo aux dossiers de deux manières.

Dans le cas des dossiers auxquels un profil est déjà affecté, le nom du profil est affiché directement sous celui du dossier.

Voir aussi [Retraitement des ressources dans un dossier après avoir modifié son profil de traitement](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile).

#### Application d’un profil vidéo à des dossiers à l’aide de l’interface utilisateur Profils {#applying-video-profiles-to-folders-by-way-of-the-profiles-user-interface}

1. Appuyez sur le logo AEM et accédez à **[!UICONTROL Outils]** > **[!UICONTROL Ressources]** > **[!UICONTROL Profils vidéo]**.
1. Sélectionnez le profil vidéo à appliquer à un ou plusieurs dossiers.
1. Appuyez sur **[!UICONTROL Appliquer le profil au(x) dossier(s)]** et sélectionnez le ou les dossiers que vous voulez voir recevoir les ressources récemment chargées, puis appuyez sur **[!UICONTROL Appliquer]**. Dans le cas des dossiers auxquels un profil est déjà affecté, le nom du profil est affiché directement sous celui du dossier en **[!UICONTROL mode Carte]**.
Vous pouvez [surveiller la progression d’une tâche de traitement de profil vidéo](#monitoring-the-progress-of-an-encoding-job).

#### Application d’un profil vidéo aux dossiers à partir des propriétés {#applying-video-profiles-to-folders-from-properties}

1. Appuyez ou cliquez sur le logo AEM, puis accédez à **[!UICONTROL Ressources]** et au dossier auquel vous souhaitez appliquer un profil vidéo.
1. Dans le dossier, appuyez sur la coche pour la sélectionner, puis sur **[!UICONTROL Propriétés]**.
1. Accédez à l’onglet **[!UICONTROL Profils vidéo]**, sélectionnez le profil dans le menu déroulant, puis cliquez sur **[!UICONTROL Enregistrer et fermer]**. Dans le cas des dossiers auxquels un profil est déjà affecté, le nom du profil est affiché directement sous celui du dossier.

   ![chlimage_1-518](assets/chlimage_1-518.png)
Vous pouvez [surveiller la progression d’une tâche de traitement de profil vidéo](#monitoring-the-progress-of-an-encoding-job).

### Application d’un profil vidéo à l’ensemble des ressources {#applying-a-video-profile-globally}

En plus d’appliquer un profil à un dossier, vous pouvez en appliquer un de façon globale, de sorte que tout contenu chargé dans AEM Assets soit traité par ce profil, indifféremment du dossier.

Voir aussi [Retraitement des ressources dans un dossier après avoir modifié son profil de traitement](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile).

**Pour appliquer un profil vidéo à l’ensemble des ressources :**

* Accédez au nœud suivant de CRXDE Lite : `/content/dam/jcr:content`. Ajoutez la propriété `videoProfile:/libs/settings/dam/video/dynamicmedia/<name of video encoding profile>` et appuyez sur **[!UICONTROL Tout enregistrer]**.

   ![chlimage_1-519](assets/chlimage_1-519.png)
* Vous pouvez [surveiller la progression d’une tâche de traitement de profil vidéo](#monitoring-the-progress-of-an-encoding-job).

## Surveillance de la progression d’une tâche de traitement de profil vidéo {#monitoring-the-progress-of-an-encoding-job}

Un indicateur (ou une barre) de progression s’affiche afin que vous puissiez surveiller visuellement la progression d’une tâche de codage vidéo.

Vous pouvez également consulter le fichier `error.log` pour contrôler la progression d’une tâche de codage, voir si le codage est terminé ou afficher les erreurs d’une tâche. Le fichier `error.log` se trouve dans le dossier `logs` où vous avez installé votre instance d’AEM.

## Suppression d’un profil vidéo des dossiers {#removing-a-video-profile-from-folders}

Lorsque vous supprimez un profil vidéo d’un dossier, les sous-dossiers héritent automatiquement de la suppression du profil de leur dossier parent. Cependant, le traitement des fichiers qui s’est produit dans les dossiers reste intact.

Vous pouvez supprimer un profil vidéo d’un dossier à partir du menu **[!UICONTROL Outils]** ou, si vous êtes dans le dossier, à partir de **[!UICONTROL Paramètres du dossier]**. Cette section explique comment supprimer des profils vidéo des dossiers de deux manières différentes.

### Suppression d’un profil vidéo des dossiers à l’aide de l’interface utilisateur Profils {#removing-video-profiles-from-folders-by-way-of-the-profiles-user-interface}

1. Appuyez sur le logo AEM et accédez à **[!UICONTROL Outils]** > **[!UICONTROL Ressources]** > **[!UICONTROL Profils vidéo]**.
1. Sélectionnez le profil vidéo à supprimer d’un ou plusieurs dossiers.
1. Appuyez sur **[!UICONTROL Supprimer le profil du ou des dossiers]** et sélectionnez le ou les dossiers desquels vous souhaitez supprimer le profil, puis appuyez sur **[!UICONTROL Supprimer]**.

   Le fait que le nom du profil n’apparaît plus sous celui du dossier indique que le profil vidéo n’est plus appliqué à un dossier.

### Suppression d’un profil vidéo des dossiers à l’aide des propriétés {#removing-video-profiles-from-folders-by-way-of-properties}

1. Appuyez ou cliquez sur le logo AEM, puis accédez à **[!UICONTROL Ressources]** et au dossier duquel vous souhaitez supprimer un profil vidéo.
1. Dans le dossier, appuyez ou cliquez sur la coche afin de le sélectionner, puis appuyez ou cliquez sur **Propriétés**.
1. Sélectionnez l’onglet **[!UICONTROL Profils vidéo]**, choisissez **[!UICONTROL Aucun]** dans le menu déroulant, puis cliquez sur **[!UICONTROL Enregistrer et fermer]**. Dans le cas des dossiers auxquels un profil est déjà affecté, le nom du profil est affiché directement sous celui du dossier.

