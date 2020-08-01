---
title: Instructions de formation de Smart Content Service
description: Former le service Adobe Sensei AI à l’application de balises actives aux ressources
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 77%

---


# Smart Content Service training guidelines {#smart-content-service-training-guidelines}

Pour pouvoir marquer efficacement vos images de marque, Smart Content Service exige que les images de formation soient conformes à certaines directives.

## Instructions d’entraînement {#guidelines-for-training}

Pour un résultat optimal, les images de votre corpus d’entraînement doivent respecter les instructions suivantes :

**Quantité et taille :** minimum 30 images par balise. Minimum 500 pixels sur le côté le plus long.

**Cohérence** : les images associées à une même balise doivent être visuellement similaires.

Par exemple, il est déconseillé d’incorporer une balise `my-party` pour toutes ces images (en situation d’entraînement), car elles ne sont pas similaires visuellement.

![Images d’illustration donnant un exemple d’instructions d’entraînement](/help/assets/assets/do-not-localize/coherence.png)

**Couverture** : les images d’entraînement doivent être suffisamment variées. L&#39;idée est de fournir quelques exemples, mais raisonnablement variés, pour que le Experience Manager apprenne à se concentrer sur les bonnes choses. Si vous appliquez la même balise sur des images visuellement différentes, incluez au moins cinq exemples de chaque type.

Par exemple, pour la balise *mannequin-pose-tête-baissée*, incluez davantage d’images d’entraînement similaires à l’image mise en évidence ci-dessous pour que le service reconnaisse les images similaires avec plus de précision lors du balisage.

![Images d’illustration donnant un exemple d’instructions d’entraînement](/help/assets/assets/do-not-localize/coverage_1.png)

**Distraction/obstruction** : l’entraînement du service donne de meilleurs résultats sur les images qui ont moins de distractions (telles que des arrière-plans importants ou des objets/personnes sans lien avec le sujet principal).

Par exemple, pour la balise *chaussure-décontractée*, la seconde image n’est pas un bon candidat pour l’entraînement.

![Images d’illustration donnant un exemple d’instructions d’entraînement](/help/assets/assets/do-not-localize/distraction.png)

**Complétude :** si une image est admissible pour plusieurs balises, ajoutez toutes les balises applicables avant d’inclure l’image à des fins de formation. Par exemple, pour les balises telles que `raincoat` et `model-side-view`, ajoutez les deux balises sur la ressource éligible avant de l’inclure pour la formation.

![Images d’illustration donnant un exemple d’instructions d’entraînement](/help/assets/assets/do-not-localize/completeness.png)

## Restrictions {#limitations}

Les balises actives améliorées reposent sur les modèles d’apprentissage des images et de leurs balises. Ces modèles ne sont pas toujours parfaits pour identifier les balises. La version actuelle du service de contenu dynamique présente les limites suivantes :

* Impossibilité d’identifier des différences subtiles dans les images. Par exemple, des chemises coupe droite ou ajustée.
* Impossibilité d’identifier des balises basées sur des motifs/éléments minuscules d’une image. Par exemple, des logos sur des T-shirts.
* Tagging is supported in the locales that [!DNL Experience Manager] is supported in. Pour obtenir la liste des langues, voir [Notes de mise à jour du service de contenu dynamique](https://docs.adobe.com/content/help/fr-FR/experience-manager-64/release-notes/smart-content-service-release-notes.html).

To search for assets with smart tags (regular or enhanced), use the [!DNL Assets] Omnisearch (full-text search). Il n’y a aucun prédicat de recherche distinct pour les balises intelligentes.

>[!NOTE]
>
>La capacité du service de contenu dynamique à s’entraîner à partir de vos balises et à les appliquer à d’autres images dépend de la qualité des images que vous utilisez pour l’entraînement. Pour obtenir des résultats optimaux, Adobe recommande d’utiliser des images visuellement similaires afin d’entraîner le service pour chaque balise.
