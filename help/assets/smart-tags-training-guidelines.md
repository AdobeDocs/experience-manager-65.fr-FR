---
title: Instructions de formation à Smart Content Service
description: Formation du service AI d’Adobe Sensei à l’application de balises actives aux ressources
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Smart Content Service training guidelines {#smart-content-service-training-guidelines}

Pour pouvoir marquer efficacement vos images de marque, le service de contenu dynamique exige que les images de formation soient conformes à certaines directives.

## Instructions d’entraînement {#guidelines-for-training}

Pour un résultat optimal, les images de votre corpus d’entraînement doivent respecter les instructions suivantes :

**** Quantité et taille : Minimum 30 images par balise. Avec un minimum de 500 pixels pour le côté le plus long.

**Cohérence** : les images pour une balise doivent être visuellement similaires.

For example, it is not a good idea to tag all of these images as `my-party` (for training) because they are not visually similar.

![Images d’illustration donnant un exemple d’instructions d’entraînement](/help/assets/assets/do-not-localize/coherence.png)

**Couverture** : les images d’entraînement doivent être suffisamment variées. L’idée est de fournir quelques exemples raisonnablement différents pour apprendre à AEM à se concentrer sur les bons éléments. Si vous appliquez la même balise sur des images visuellement différentes, incluez au moins cinq exemples de chaque type.

Par exemple, pour la balise *pose-tête-baissée-mannequin*, incluez davantage d’images d’entraînement similaires à l’image mise en évidence ci-dessous pour que le service reconnaisse les images similaires avec plus de précision lors du balisage.

![Images d’illustration donnant un exemple d’instructions d’entraînement](/help/assets/assets/do-not-localize/coverage_1.png)

**Distraction/obstruction** : l’entraînement du service donne de meilleurs résultats sur les images qui ont moins de distractions (telles que des arrière-plans importants ou des objets/personnes sans lien avec le sujet principal).

Par exemple, pour la balise *chaussure-décontractée*, la seconde image n’est pas un bon candidat pour l’entraînement.

![Images d’illustration donnant un exemple d’instructions d’entraînement](/help/assets/assets/do-not-localize/distraction.png)

**** Complétude : Si une image est admissible pour plusieurs balises, ajoutez toutes les balises applicables avant d’inclure l’image à des fins de formation. For example, for tags, such as `raincoat` and `model-side-view`, add both the tags on the eligible asset before including it for training.

![Images d’illustration donnant un exemple d’instructions d’entraînement](/help/assets/assets/do-not-localize/completeness.png)

## Restrictions {#limitations}

Les balises actives améliorées reposent sur des modèles d’apprentissage des images et de leurs balises. Ces modèles ne sont pas toujours parfaits pour identifier les balises. La version actuelle du service de contenu dynamique présente les limites suivantes :

* Impossibilité d’identifier des différences subtiles dans les images. Par exemple, les chemises à l&#39;air mince et les chemises ordinaires.
* Impossibilité d’identifier des balises basées sur des motifs/éléments minuscules d’une image. Par exemple, des logos sur des T-shirts.
* Le balisage est pris en charge dans les paramètres régionaux gérés par AEM. Pour obtenir la liste des langues, voir [Notes de mise à jour du service de contenu dynamique](https://docs.adobe.com/content/help/en/experience-manager-64/release-notes/smart-content-service-release-notes.html).

Pour rechercher des fichiers avec des balises actives (normales ou améliorées), utilisez la recherche de ressources Omnisearch (recherche de texte intégral). Il n’y a aucun prédicat de recherche distinct pour les balises intelligentes.

>[!NOTE]
>
>La capacité du service de contenu dynamique à s’entraîner à partir de vos balises et à les appliquer à d’autres images dépend de la qualité des images que vous utilisez pour l’entraînement. Pour obtenir des résultats optimaux, Adobe recommande d’utiliser des images visuellement similaires afin d’entraîner le service pour chaque balise.
