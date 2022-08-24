---
title: Organisez vos ressources numériques
description: Organisez vos ressources numériques, images, fichiers, dossiers, etc. à l’aide de Experience Manager.
contentOwner: AG
role: User
feature: Asset Management,Search
exl-id: d6f815b5-e4fc-4f8c-a6c1-9e50035ab9f2
source-git-commit: 068f6c1c2909c2840e9ad4c0ad295538e543d9c9
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 54%

---

# Organisez vos ressources numériques {#organize-digital-assets}

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Cliquez ici](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/organize-assets.html?lang=en) |
| AEM 6.5 | Cet article |
| AEM 6.4 | [Cliquez ici](https://experienceleague.adobe.com/docs/experience-manager-64/assets/managing/organize-assets.html?lang=en) |

L’ensemble des ressources numériques, des métadonnées et du contenu des documents Microsoft Office et PDF sont extraits et rendus utilisables dans une requête. Les recherches permettent un filtrage élaboré des ressources et respectent entièrement les autorisations. Les métadonnées sont décrites en détail dans la section Métadonnées de la gestion des ressources numériques.

[!DNL Experience Manager Assets] prend en charge plusieurs manières d’organiser le contenu. Vous pouvez les organiser de manière hiérarchique à l’aide de dossiers ou les organiser de manière ad hoc et non ordonnée à l’aide de balises, par exemple. Les utilisateurs peuvent modifier les balises dans l’éditeur de ressources de gestion des actifs numériques où les sous-ressources, rendus et métadonnées sont affichés.

## Organisation des ressources dans des dossiers {#organize-using-folders}

La méthode la plus simple pour organiser les ressources consiste à les enregistrer dans des dossiers. C’est analogue à l’organisation de fichiers dans des dossiers de notre système de fichiers local. Pour plus d’informations sur la création et la gestion des dossiers, consultez [Gestion des ressources](manage-assets.md). La manière dont vous nommez les fichiers et les dossiers, organisez les sous-dossiers et gérez les fichiers dans ces dossiers peut avoir un impact significatif sur la manière dont ces ressources sont traitées. Grâce à des stratégies d’attribution de noms de fichiers et de dossiers cohérentes et appropriées, ainsi qu’à de bonnes pratiques d’utilisation des métadonnées, vous pouvez tirer le meilleur parti de votre référentiel de ressources numériques.

* Dans la plupart des cas, votre référentiel de ressources numériques est toujours en croissance. Il est donc important de formaliser l’utilisation des métadonnées, la structure des dossiers et l’attribution de noms aux fichiers au début du cycle de création de contenu.
* Utilisez les dossiers uniquement pour imposer une structure de stockage cohérente pour vos ressources numériques. Cette cohérence aide votre processus et à mieux gérer vos ressources. Par exemple, les ressources placées dans les types de dossiers suivants peuvent vous aider à utiliser les [profils à utiliser pour le traitement des ressources](processing-profiles.md):

   * **Dossiers de développement** : contiennent les ressources numériques que vous utilisez actuellement.
   * **Dossiers de clients** : contiennent des ressources numériques en fonction des clients ou des noms de projet.
   * **Dossiers principaux** : contiennent les ressources numériques sources originales.
   * **Dossiers de rendus** : contiennent les rendus et les copies des ressources numériques sources originales.
   * **Dossiers de taille de fichier** : contiennent des ressources numériques en fonction des tailles de fichier petite, moyenne et volumineuse.
   * **Dossiers intermédiaires** : contiennent les ressources numériques qui sont prêtes à être publiées sur votre site web.
   * **Dossiers de type MIME** : contiennent des ressources numériques qui sont spécifiques à des types MIME tels que des images, des documents et des fichiers multimédias.
   * **Dossiers d’archives** : contiennent les ressources numériques retirées.
   * **Dossiers reposant sur une date** : contiennent des ressources numériques en fonction d’une date de création ou d’une date de dernière modification.

* Créez un répertoire de dossiers qui n’est pas susceptible de changer afin que les processus de personnalisation ou d’autonomisation puissent continuer à fonctionner. Par exemple, les profils de traitement affectés continuent à fonctionner.
* Si une ressource est déjà publiée, vous utilisez [!DNL Experience Manager] pour déplacer la ressource vers un autre dossier et la republier à partir de son nouvel emplacement, l’emplacement de la ressource publiée d’origine est toujours disponible, ainsi que la ressource republiée. Toutefois, la version d’origine de la ressource publiée est *« perdue »* pour [!DNL Experience Manager] et sa publication ne peut pas être annulée. Il est donc recommandé d’annuler d’abord la publication d’une ressource avant de la déplacer vers un autre dossier.

## Organisation de ressources à l’aide de balises {#use-tags-to-organize-assets}

À l’aide de balises, en tant que métadonnées, vous pouvez facilement rechercher des ressources, créer des collections à l’aide des résultats de recherche, améliorer le classement de certaines ressources et utiliser les algorithmes d’IA d’Adobe Sensei pour la découverte de ressources.

[!DNL Adobe Experience Manager Assets] utilise un algorithme d’auto-apprentissage pour créer des balises hautement descriptives qui vous permettent de trouver la ressource appropriée en quelques clics seulement. Le balisage intelligent utilise Adobe Sensei, notre intelligence artificielle et notre structure d’apprentissage automatique, qui peuvent être formés pour reconnaître et appliquer des balises standard et commerciales à l’imagerie. Les balises intelligentes peuvent également identifier le contenu, les mots ou les expressions et appliquer automatiquement des balises descriptives aux ressources.

Pour plus d’informations, consultez les articles suivants :

* [À propos des balises dans Experience Manager](/help/sites-authoring/tags.md)
* [Modification de métadonnées de ressource](metadata.md)
* [Balises intelligentes améliorées dans Assets](enhanced-smart-tags.md)

## Organisation en tant que collections {#organize-as-collections}

Avec les collections de ressources dans [!DNL Experience Manager Assets], vous pouvez rationaliser la possibilité de créer, modifier et partager des ressources entre les utilisateurs. Créez plusieurs types de collections en fonction de leur utilisation, y compris des collections contenant une liste de référence statique de ressources, dossiers et collections, ainsi que des collections qui extraient des ressources en fonction de critères de recherche.  Vous pouvez également créer des collections avec des ressources provenant de différents emplacements et les partager avec plusieurs utilisateurs disposant de différents niveaux d’accès, d’affichage et de modification des privilèges.

Pour plus d’informations, consultez [Gestion des collections](manage-collections.md).

<!-- TBD items: add screenshots where applicable
Any hints/recommendations of when to use what method of organizing? Some examples of how organizing helps towards a better taxonomy and improved content velocity.
Add back links to blog posts by marketing?
-->

## Organisation de vos ressources pour utiliser des profils {#organize-to-use-profiles}

Un profil de traitement contient les commandes de traitement [!DNL Assets] qui s’appliquent aux ressources chargées dans des dossiers prédéfinis. Les profils sont utilisés pour automatiser le traitement du contenu d’un dossier ou de ressources nouvellement chargées. Vous pouvez tirer parti des profils pour mieux organiser vos ressources.

Grâce à cette normalisation de l’utilisation des métadonnées, de l’attribution des noms et de la structure des dossiers, vous aurez l’assurance, au fur et à mesure que le nombre de vos ressources augmente, de pouvoir appliquer des profils de traitement aux dossiers avec une précision et une cohérence toujours plus grandes.

>[!MORELIKETHIS]
>
>* [Profils de traitement des métadonnées, des images et des vidéos](processing-profiles.md).
>* [Profils de métadonnées](/help/assets/metadata-config.md#metadata-profiles).
>* [Profils vidéo](video-profiles.md).
>* [Profils d’image Dynamic Media](image-profiles.md).

