---
title: Organisez vos ressources numériques.
description: Organisez vos fichiers numériques, images, fichiers, dossiers, etc. à l’aide du Experience Manager.
contentOwner: AG
translation-type: tm+mt
source-git-commit: cec6c4f9a1a75eb049dd4b8461c36c8d58d46f79
workflow-type: tm+mt
source-wordcount: '780'
ht-degree: 8%

---


# Organisez vos ressources numériques.{#organize-digital-assets}

L’ensemble des ressources numériques, des métadonnées et du contenu des documents Microsoft Office et PDF sont extraits et rendus utilisables dans une requête. Les recherches permettent un filtrage élaboré des ressources et respectent entièrement les autorisations. Les métadonnées sont traitées en détail dans les métadonnées de la gestion des ressources numériques.

[!DNL Experience Manager Assets] prend en charge plusieurs méthodes d’organisation du contenu. Vous pouvez les organiser de manière hiérarchique à l’aide de dossiers ou vous pouvez les organiser de manière ad hoc et non ordonnée, à l’aide de balises, par exemple. Les utilisateurs peuvent modifier les balises dans l’éditeur de ressources de gestion des actifs numériques où les sous-ressources, rendus et métadonnées sont affichés.

## Organisation des fichiers dans des dossiers {#organize-using-folders}

La méthode la plus élémentaire pour organiser les fichiers consiste à les enregistrer dans des dossiers. Il est analogue à l&#39;organisation de fichiers dans des dossiers de notre système de fichiers local. Pour plus d’informations sur la création et la gestion des dossiers, voir [Gestion des fichiers](manage-assets.md). La manière dont vous nommez les fichiers et les dossiers, dont vous disposez les sous-dossiers et dont vous traitez les fichiers dans ces dossiers peut avoir un impact significatif sur la manière dont ces fichiers sont traités. En appliquant des stratégies cohérentes et appropriées de nommage de fichiers et de dossiers, ainsi que de bonnes pratiques de métadonnées, vous pouvez tirer le meilleur parti de votre référentiel de ressources numériques.

* Dans la plupart des cas, votre référentiel de ressources numériques est toujours en croissance. Par conséquent, il est important de formaliser l’utilisation des métadonnées, la structure des dossiers et le nommage des fichiers au début du cycle de création de contenu.
* Utilisez les dossiers uniquement pour imposer une structure de stockage cohérente pour vos ressources numériques. Cette cohérence permet de mieux traiter et gérer vos ressources. Par exemple, les fichiers placés dans les types de dossiers suivants peuvent vous aider à utiliser les [profils appropriés pour le traitement](processing-profiles.md)des fichiers :

   * **Dossiers** de développement : contient des ressources numériques sur lesquelles vous travaillez actuellement.
   * **Dossiers** client : contient des ressources numériques basées sur les noms de clients ou de projets.
   * **Dossiers** Principal : contient des ressources numériques source d’origine.
   * **Dossiers** de rendu : contient des rendus et des copies des ressources numériques sources d’origine.
   * **Dossiers** Taille du fichier : contient des ressources numériques en fonction de tailles de fichier petites, moyennes ou grandes.
   * **Dossiers** intermédiaires : contient des ressources numériques prêtes à être publiées en direct sur votre site Web.
   * **Dossiers** de type MIME : contient des ressources numériques spécifiques aux types MIME tels que les images, les documents et les contenus multimédia.
   * **Dossiers** d&#39;archivage : contient des ressources numériques à la retraite.
   * **Dossiers** basés sur les dates : contient des ressources numériques basées sur une date de création ou une date de dernière modification.

* Créez un répertoire de dossiers qui ne sont pas susceptibles d’être modifiés de sorte que toute personnalisation ou automatisation continue de fonctionner. Par exemple, les profils de traitement affectés continuent de fonctionner.
* If an asset is already published, then you use [!DNL Experience Manager] to move the asset to another folder, and re-publish from its new location, the original published asset location is still available, along with the newly re-published asset. The original published asset, however, is *lost* to [!DNL Experience Manager] and cannot be unpublished. Par conséquent, il est recommandé d’abord d’annuler la publication d’un fichier, puis de le déplacer vers un autre dossier.

## Organisation des fichiers à l’aide de balises {#use-tags-to-organize-assets}

Grâce aux balises, en tant que métadonnées, vous pouvez facilement rechercher des ressources, créer des collections à l’aide des résultats de la recherche, augmenter le classement des recherches pour certains fichiers et utiliser les algorithmes d’IA d’Adobe Sensei pour la découverte de fichiers.

[!DNL Adobe Experience Manager Assets] utilise un algorithme d’auto-apprentissage pour créer des balises hautement descriptives qui vous permettent de trouver la ressource appropriée en quelques clics seulement. Le balisage intelligent utilise Adobe Sensei, notre intelligence artificielle et notre système d&#39;apprentissage automatique, qui peut être formé pour reconnaître et appliquer des balises standard et commerciales à l&#39;imagerie. Les balises actives peuvent également identifier le contenu, les mots individuels ou les expressions et appliquer automatiquement des balises descriptives aux ressources.

Pour plus d’informations, reportez-vous aux articles suivants :

* [A propos des balises dans le Experience Manager](/help/sites-authoring/tags.md)
* [Modification des métadonnées de fichier](metadata.md)
* [Amélioration des balises actives dans les ressources](enhanced-smart-tags.md)

## Organiser en tant que collections {#organize-as-collections}

Avec les collections de ressources intégrées [!DNL Experience Manager Assets], vous pouvez rationaliser la possibilité de créer, de modifier et de partager des ressources entre utilisateurs. Créez plusieurs types de collections en fonction de leur utilisation, y compris des collections qui contiennent une liste de référence statique de ressources, de dossiers et de collections, ainsi que des collections qui extraient des ressources en fonction de critères de recherche.  Vous pouvez également créer des collections avec des ressources provenant de différents emplacements et les partager avec plusieurs utilisateurs avec différents niveaux d’accès, d’affichage et de modification des privilèges.

For more information, see [manage collections](manage-collections.md)

<!-- TBD items: add screenshots where applicable
Any hints/recommendations of when to use what method of organizing? Some examples of how organizing helps towards a better taxonomy and improved content velocity.
Add back links to blog posts by marketing?
-->

## Organiser vos ressources pour utiliser des profils {#organize-to-use-profiles}

Un profil de traitement contient des commandes [!DNL Assets] de traitement qui s’appliquent aux fichiers qui sont téléchargés vers des dossiers prédéfinis. Les profils sont utilisés pour automatiser le traitement du contenu d’un dossier ou des ressources fraîchement téléchargées. Vous pouvez tirer parti des profils pour mieux organiser vos ressources.

La normalisation de l’utilisation des métadonnées, du nommage de fichiers et de la structure des dossiers permet d’appliquer des profils de traitement aux dossiers avec plus de précision et de cohérence à mesure que votre pool de ressources numériques s’accroît.

>[!MORELIKETHIS]
>
>* [Profils de traitement des métadonnées, des images et des vidéos](processing-profiles.md).
>* [Profils de métadonnées](/help/assets/metadata-config.md#metadata-profiles).
>* [Profils vidéo](video-profiles.md).
>* [Profils](image-profiles.md)d’image Contenu multimédia dynamique.

