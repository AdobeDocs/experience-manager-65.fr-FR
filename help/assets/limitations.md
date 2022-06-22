---
title: Limites de Dynamic Media
description: 'Découvrez les bonnes pratiques et les limites appliquées lorsque vous créez une visionneuse d’images ou à 360° ou chargez un PDF. Découvrez également les combinaisons de navigateur web et de système d’exploitation non prises en charge pour les visionneuses Dynamic Media. '
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/Dynamic-Media-Classic
geptopics: SG_SCENESEVENONDEMAND_PK/categories/ecatalogs
feature: Dynamic Media Classic,Asset Management,Viewers,Image Sets,Spin Sets,eCatalog
role: User
source-git-commit: cd3dcd0232e1ecf69c79b03ab960cfbfc283ee76
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 3%

---

# Limites de Dynamic Media

Les sections suivantes décrivent les limites dans Dynamic Media.

Cette rubrique comprend les sections suivantes :

* Bonnes pratiques et limites appliquées par Dynamic Media sur les types de ressources

<!-- * Unsupported web browser and operating system combinations for Dynamic Media Viewers -->

## Bonnes pratiques et limites appliquées par Dynamic Media sur les types de ressources

Lorsque vous créez une visionneuse à 360° ou une visionneuse d’images, ou que vous chargez des PDF pour l’extraction de page, Adobe recommande les bonnes pratiques suivantes et applique les limites suivantes :

| Ressource - Type de limite | Bonne pratique | Limite implémentée | Modifications apportées à la limite du 31 décembre 2022 |
| --- | --- | --- | --- |
| **Image** - Nombre de recadrages intelligents par image | 5 | 100 |  |
| **Visionneuse d’images** - Nombre de ressources en double par ensemble | Aucun doublon | 100 | 20 |
| **Visionneuse d’images** - Nombre maximal d’images par visionneuse | 5 à 10 images par visionneuse | 1000 |
| **Visionneuse à 360°** - Nombre maximal de lignes/colonnes par jeu 2D | 12 à 18 images par visionneuse | 1000 |
| **PDF** - Nombre maximal de pages qu’un PDF doit prendre en compte pour l’extraction |  | 5000 (pour les nouveaux chargements) | 100 |

<!-- See also [Dynamic Media limitations](/help/assets/limitations.md). -->

<!-- ## Unsupported web browser and operating system combinations for Dynamic Media Viewers

Dynamic Media Viewers do not support following combinations of web browser and operating system.

* Internet Explorer 11 + Windows 7
* Internet Explorer 11 + Windows 8.1
* Internet Explorer 11 + Windows Phone 8.1
* Internet Explorer 11 + Windows Phone 8.1 Update
* Safari 6 + iOS 6.0.1
* Safari 7 + iOS 7.1
* Safari 7 + macOS X 10.9 Mavericks
* Safari 8 + iOS 8.4
* Safari 8 + macOS X 10.10 Yosemite -->