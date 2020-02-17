---
title: Organisez vos ressources numériques.
description: Organisez vos fichiers numériques, images, fichiers, dossiers, etc. à l’aide d’Experience Manager.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Organisez vos ressources numériques.{#organize-digital-assets}

L’ensemble des ressources numériques, des métadonnées et du contenu des documents Microsoft Office et PDF sont extraits et rendus utilisables dans une requête. Les recherches permettent un filtrage élaboré des ressources et respectent entièrement les autorisations. Les métadonnées sont traitées en détail dans les métadonnées de la gestion des ressources numériques.

AEM Assets prend en charge plusieurs manières d’organiser le contenu. Vous pouvez les organiser de manière hiérarchique à l’aide de dossiers ou de manière ad hoc et non ordonnée, à l’aide de balises, par exemple. Les utilisateurs peuvent modifier les balises dans l’éditeur de ressources de gestion des actifs numériques où les sous-ressources, rendus et métadonnées sont affichés.

## Organisation des fichiers dans des dossiers {#organize-using-folders}

La méthode la plus élémentaire pour organiser les fichiers consiste à les enregistrer dans des dossiers. C&#39;est analogue à l&#39;organisation de fichiers dans des dossiers de notre système de fichiers local. Pour plus d’informations sur la création et la gestion des dossiers, voir [Gestion des fichiers](managing-assets-touch-ui.md). La manière dont vous nommez les fichiers et les dossiers, la manière dont vous organisez les sous-dossiers et dont vous traitez les fichiers dans ces dossiers peuvent avoir un impact significatif sur la manière dont ces fichiers sont traités. En appliquant des stratégies cohérentes et appropriées de nommage des fichiers et des dossiers, ainsi que de bonnes pratiques de métadonnées, vous pouvez tirer le meilleur parti de votre référentiel de ressources numériques.

* Dans la plupart des cas, votre référentiel de ressources numériques est toujours en croissance. Par conséquent, il est important de formaliser l’utilisation des métadonnées, la structure des dossiers et le nommage des fichiers au début du cycle de création de contenu.
* Utilisez les dossiers uniquement pour imposer une structure de stockage cohérente pour vos ressources numériques. Cette cohérence aide à traiter et à mieux gérer vos ressources. Par exemple, les fichiers placés dans les types de dossiers suivants peuvent vous aider à utiliser les [profils appropriés pour le traitement](processing-profiles.md)des fichiers :

   * **Dossiers** de développement : contient les ressources numériques sur lesquelles vous travaillez actuellement.
   * **Dossiers** clients : contient des ressources numériques basées sur les clients ou les noms de projet.
   * **Dossiers** principaux : contient les fichiers numériques source d’origine.
   * **Dossiers** de rendus : contient les rendus et les copies des fichiers numériques source d’origine.
   * **Dossiers** Taille de fichier : contient des fichiers numériques en fonction de la taille de fichier (petite, moyenne ou grande).
   * **Dossiers** d’évaluation : contient des ressources numériques prêtes à être publiées en direct sur votre site Web.
   * **Dossiers** de type MIME : contient des ressources numériques spécifiques aux types MIME tels que les images, les documents et les fichiers multimédia.
   * **Dossiers** d’archives : contient des ressources numériques à la retraite.
   * **Dossiers** basés sur des dates : contient des ressources numériques basées sur une date de création ou une date de dernière modification.

* Créez un répertoire de dossiers qui ne sont pas susceptibles d’être modifiés afin que toute personnalisation ou automatisation continue de fonctionner. Par exemple, les profils de traitement attribués continuent de fonctionner.
* If an asset is already published, then you use AEM to move the asset to another folder, and re-publish from its new location, the original published asset location is still available, along with the newly re-published asset. The original published asset, however, is *lost* to AEM and cannot be unpublished. Par conséquent, il est recommandé d’abord d’annuler la publication d’un fichier, puis de le déplacer vers un autre dossier.

## Organisation des fichiers à l’aide de balises {#use-tags-to-organize-assets}

Grâce aux balises, en tant que métadonnées, vous pouvez facilement rechercher des fichiers, créer des collections à l’aide des résultats de la recherche, améliorer le classement des recherches pour certains fichiers et tirer parti des algorithmes d’IA d’Adobe Sensei pour la découverte de fichiers.

Adobe Experience Manager Assets utilise un algorithme d’auto-apprentissage pour créer des balises hautement descriptives qui vous permettent de trouver la ressource appropriée en quelques clics seulement. Le balisage intelligent utilise Adobe Sensei, notre infrastructure d’intelligence artificielle et d’apprentissage automatique, qui peut être formé pour reconnaître et appliquer des balises standard et spécifiques à l’entreprise à l’imagerie. Les balises intelligentes peuvent également identifier le contenu, les mots individuels ou les expressions et appliquer automatiquement des balises descriptives aux ressources.

Pour plus d’informations, voir les articles suivants :

* [A propos des balises dans AEM](/help/sites-authoring/tags.md)
* [Modification des métadonnées d’un fichier](meta-edit.md)
* [Balises actives améliorées dans les ressources](enhanced-smart-tags.md)

## Organiser en tant que collections {#organize-as-collections}

Grâce aux collections de ressources d’Experience Manager Assets, vous pouvez rationaliser la capacité de créer, de modifier et de partager des ressources entre utilisateurs. Créez plusieurs types de collections en fonction de leur utilisation, y compris des collections qui contiennent une liste de référence statique de ressources, de dossiers et de collections, ainsi que des collections qui extraient des fichiers selon des critères de recherche.  Vous pouvez également créer des collections avec des fichiers provenant de différents emplacements et les partager avec plusieurs utilisateurs avec des privilèges d’accès, d’affichage et de modification différents.

For more information, see [manage collections](managing-collections-touch-ui.md)

<!-- TBD items: add screenshots where applicable
Any hints/recommendations of when to use what method of organizing? Some examples of how organizing helps towards a better taxonomy and improved content velocity.
Add back links to blog posts by marketing?
-->

## Organiser vos fichiers pour utiliser des profils {#organize-to-use-profiles}

Un profil de traitement contient des commandes de traitement des ressources qui s’appliquent aux fichiers qui sont téléchargés vers des dossiers prédéfinis. Les profils sont utilisés pour automatiser le traitement du contenu d’un dossier ou de fichiers nouvellement transférés. Vous pouvez tirer parti des profils pour mieux organiser vos ressources.

La normalisation de l’utilisation des métadonnées, de l’appellation des fichiers et de la structure des dossiers vous permet d’appliquer des profils de traitement aux dossiers avec plus de précision et de cohérence à mesure que votre pool de ressources numériques s’accroît.

Pour plus d’informations sur les différents profils que vous pouvez créer et gérer pour traiter des ressources, voir

* [Profils de traitement des métadonnées, images et vidéos](processing-profiles.md)
* [Profils de métadonnées](metadata-profiles.md)
* [Profils vidéo](video-profiles.md)
* [Profils d’image Contenu multimédia dynamique](image-profiles.md)
