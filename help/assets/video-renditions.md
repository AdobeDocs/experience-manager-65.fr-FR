---
title: Rendus vidéo
description: Rendus vidéo
uuid: a02f9ec1-30d9-4cbb-8746-8391ac614f0a
contentOwner: rbrough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: 1601b473-7227-4a56-bb7c-289de2987e4b
exl-id: a644558e-5be9-4ba2-b560-fc300497fbdf
source-git-commit: 77687a0674b939460bd34011ee1b94bd4db50ba4
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 45%

---

# Rendus vidéo {#video-renditions}

Adobe Experience Manager Assets génère des rendus vidéo pour les ressources vidéo de différents formats, notamment OGG, FLV, etc.

Experience Manager Assets prend en charge les rendus statiques et dynamiques (rendus codés en MD) pour les ressources multimédias.

Les rendus statiques sont générés en mode natif à l’aide de FFMPEG (installé et disponible sur le chemin système) et stockés dans le référentiel de contenu.

Les rendus avec codage DM sont stockés dans le serveur proxy et diffusés au moment de l’exécution.

Les ressources Experience Manager prennent en charge la lecture de ces rendus côté client.

Pour afficher les rendus d’une ressource vidéo spécifique, ouvrez la page Ressource correspondante, puis sélectionnez l’icône Navigation globale . Choisissez ensuite **[!UICONTROL Rendus]** dans la liste.

![chlimage_1-478](assets/chlimage_1-478.png)

La liste des rendus vidéo s’affiche dans le panneau **[!UICONTROL Rendus]** .

![chlimage_1-479](assets/chlimage_1-479.png)

Pour configurer le serveur proxy des rendus codés en MD, [configurez les services cloud Dynamic Media](config-dynamic.md).

Pour générer des rendus vidéo avec les paramètres souhaités, [créez un profil vidéo correspondant](video-profiles.md).

Une fois que vous avez configuré le serveur proxy et créé les profils vidéo, vous pouvez inclure ce paramètre vidéo prédéfini dans un profil de traitement et appliquer le profil de traitement à un dossier.

>[!NOTE]
>
>La lecture audio ne fonctionne pas pour les fichiers OGG et WAV sur Microsoft® Internet Explorer 11. Une erreur `Invalid Source` s’affiche sur la page des détails de la ressource pour les ressources avec l’extension OGG ou WAV.
>
>Sur MS® Edge et iPad, les fichiers OGG ne sont pas lus et génèrent une erreur de format non prise en charge.
