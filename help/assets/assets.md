---
title: A propos des ressources AEM
description: Découvrez ce qu’est la gestion des ressources numériques, ses cas d’utilisation et l’offre AEM Asset d’Adobe.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0ff23556444fcb161b0adf744bb72fdc50322d92

---


# Administration des fichiers {#administering-assets}

Assets est un outil de gestion des actifs numériques (DAM) entièrement intégré à la plate-forme AEM et permet à votre entreprise de partager et de distribuer des actifs numériques. Les utilisateurs au sein d’une organisation peuvent gérer, stocker et accéder à des images, des vidéos, des documents, des clips audio et des fichiers multimédias enrichis, tels que des fichiers Flash, en vue de les utiliser sur le web, les imprimer et effectuer une distribution numérique.

## What is Digital Asset Management? {#what-is-digital-asset-management}

Les ressources permettent le partage et la distribution des ressources numériques principales d’une organisation dans toute l’entreprise. Les utilisateurs d’une organisation peuvent stocker, gérer et accéder aux ressources numériques telles que les images, les graphiques, l’audio, la vidéo et les documents via une interface Web (ou un dossier CIFS ou WebDAV).

Bien intégré à AEM, AEM Assets vous permet d’effectuer les opérations suivantes :

* Ajouter et partager des images, des documents, ainsi que des fichiers audio et vidéo dans divers formats.
* Gérez les fichiers en les regroupant par balises, cadre lumineux ou étoiles (vos favoris). Annoter les ressources.
* Rechercher des ressources en recherchant des noms de fichier, le texte intégral des documents et en recherchant les dates, le type de document et les balises.
* Ajouter ou modifier des informations sur les métadonnées pour les ressources. Les métadonnées sont automatiquement versionnées avec la ressource correspondante. Vous pouvez importer ou exporter des métadonnées de ressources.
* Exercer des fonctions de retouche d’images, telles que la mise à l’échelle et l’ajout de filtres d’image. Importer et exporter simultanément des ressources numériques multiples à l’aide d’un dossier WebDAV ou CIFS.
* Utiliser les workflows et les notifications pour permettre le traitement et le téléchargement communs de n’importe quel groupe de ressources et gérer les droits d’accès aux ressources.

### AEM Assets est complètement intégré dans CQ WCM {#aem-assets-fully-integrated-in-cq-wcm}

AEM Assets est entièrement intégré à la gestion du contenu web CQ, et la fonctionnalité est disponible via l’icône DAM :

![screen_shot_2012-04-17at15946pm](assets/screen_shot_2012-04-17at15946pm.png) ![screen_shot_2012-04-17at20100pm](assets/screen_shot_2012-04-17at20100pm.png)

Les ressources gérées dans la gestion des actifs numériques CQ sont ensuite accessibles via l’outil de recherche de contenu de la gestion du contenu web :

![screen_shot_2012-04-17at20214pm](assets/screen_shot_2012-04-17at20214pm.png)

>[!NOTE]
>
>L’utilisation de l’interface utilisateur graphique est essentiellement identique au reste de la gestion du contenu web. Voir [Aperçu de la console d’interface utilisateur graphique](/help/sites-authoring/page-authoring.md) pour plus d’informations.

### Digital Asset Management versus image component {#digital-asset-management-versus-image-component}

Lorsque vous décidez de placer une image dans AEM Assets ou d’utiliser le composant Image AEM, tenez compte du cycle de vie de l’image :

* Si l’image a le même cycle de vie que la page, utilisez le composant Image.
* Si l’image a un cycle de vie distinct, par exemple, si vous utilisez l’image deux fois ou en dehors de la gestion de contenu web, utilisez AEM Assets.

## What are digital assets? {#what-are-digital-assets}

Un fichier est un document numérique, une image, une vidéo ou de l’audio (ou une partie de celui-ci) qui peut comporter plusieurs rendus et des sous-ressources (par exemple, des calques dans un fichier Photoshop, des diapositives dans un fichier PowerPoint, des pages dans un PDF, des fichiers dans un fichier ZIP).

Une ressource se compose principalement de données binaires + métadonnées + rendus + sous-ressources. Consultez le [Guide de performance DAM](/help/sites-deploying/assets-performance-sizing.md) pour plus d’informations.

>[!CAUTION]
>
>Le transfert et/ou la modification d’une grande quantité de ressources (en particulier des images) peuvent avoir une incidence sur les performances de votre instance CQ.

### AEM Assets terminology {#aem-assets-terminology}

Lorsque vous travaillez avec des ressources numériques dans AEM, vous devez connaître la terminologie suivante :

* **Collection** Collection de fichiers, selon l’emplacement physique (dossier), les propriétés courantes (dossier de recherche enregistré) ou la sélection d’utilisateurs (dossiers de cadre lumineux).

* **Les ressources de métadonnées** comportent des métadonnées ; par exemple, auteur, date d’expiration, informations DRM (Digital Rights Management), etc. Les métadonnées sont sous contrôle d’accès. AEM Assets prend en charge les schémas de métadonnées communs suivants :

   * Dublin Core : notamment l’auteur, la description, la date, l’objet, etc.
   * IPTC : notamment l’événement, le modèle, l’emplacement, etc.
   * WCM : y compris les propriétés de la page, [!UICONTROL Heure] d’activation et Heure [!UICONTROL de]désactivation, etc.

* **Le balisage** des ressources peut être balisé et classifié. Voir Utilisation des balises et Administration des balises.

* **Rendus** Un rendu est la représentation binaire d’un fichier. Une ressource possède toujours une représentation principale, à savoir celle du fichier téléchargé. Elle peut en avoir d’autres qui sont créées par des étapes de workflow personnalisées ou lors du téléchargement de la ressource, par exemple. Les rendus peuvent avoir différentes tailles, différentes résolutions et un filigrane ou d’autres caractéristiques modifiées.

* **Versions** Versioning crée un instantané des ressources numériques à un moment donné. Vous pouvez restaurer la version précédente des ressources. Voir Contrôle de version dans AEM Assets.

* **Sous-ressources** Les sous-ressources sont des ressources qui constituent une ressource, par exemple des calques dans un fichier Adobe Photoshop ou des pages dans un fichier PDF. Dans AEM Assets, vous pouvez gérer les sous-ressources comme les ressources.

### How to work with assets {#how-to-work-with-assets}

Vous effectuez une action sur une ressource ou une collection. Les actions peuvent créer ou modifier des ressources, des collections et des rendus. La plupart des actions de base que vous effectuez sur les ressources (transfert, suppression, mise à jour, enregistrement des sous-ressources) déclenchent des processus préconfigurés. Ils sont automatiquement activés dans AEM Assets et sont décrits en détail dans les gestionnaires de médias AEM Assets.

Tâches que vous pouvez effectuer avec ces processus préconfigurés :

* Enregistrer la ressource dans le référentiel ou la supprimer.
* Extraire et enregistrer des métadonnées pour la ressource ; les différents éléments de métadonnées sont enregistrés au format XMP.
* Générer des rendus et des vignettes pour la ressource ; notamment le redimensionnement et le recadrage automatiques si nécessaire.
* Transcoder la ressource si nécessaire. Par exemple, la vidéo pour l’utilisation mobile et Web est transcodée avec 24 images par seconde, la vidéo téléchargée avec 30 images par seconde. Un fichier audio pour utilisation sur appareils mobiles et sur le web est transcodé avec 128 Kbits/s et téléchargé avec 192 Kbits/s.

Vous pouvez bien sûr aussi appliquer des workflows manuellement. Voir [Gestionnaires de médias AEM Assets](/help/assets/media-handlers.md) pour obtenir une liste des workflows par défaut.

## AEM Assets and AEM MediaLibrary {#cq-dam-vs-cq-medialibrary}

Voir [AEM Assets et AEM MediaLibrary](/help/assets/medialibrary.md) pour en savoir plus sur les différences.
