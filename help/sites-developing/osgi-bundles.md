---
title: Bundles OSGi
description: Découvrez quelques conseils pour gérer vos lots OSGi dans Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: e18065c7-75b9-4b37-8294-cf94122a4dcf
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 30%

---

# Bundles OSGi{#osgi-bundles}

## Utilisation du contrôle de version sémantique {#use-semantic-versioning}

Les bonnes pratiques de numérotation de version sémantique sont disponibles à l’adresse [https://semver.org/](https://semver.org/).

## N’incorporez pas plus de classes et de fichiers JAR que nécessaire dans les lots OSGi. {#do-not-embed-more-classes-and-jars-than-strictly-needed-in-osgi-bundles}

Les bibliothèques courantes doivent être prises en compte dans des lots distincts. Cela permet de les réutiliser dans vos lots. Lors de l’encapsulation d’une *JAR* dans un lot OSGi, veillez à vérifier les sources en ligne pour voir si quelqu’un a déjà fait cela auparavant. Voici quelques emplacements courants pour trouver les wrappers de bundle existants : Apache Felix, Apache Sling, Apache Geronimo, Apache ServiceMix, Eclipse Bundle Recipes et le référentiel SpringSource Enterprise Bundle Repository.

## Dépendre des versions de lots les plus basses nécessaires {#depend-on-the-lowest-needed-bundle-versions}

Pour les dépendances au moment de la compilation dans les fichiers POM, dépendent toujours de la version la plus basse nécessaire qui expose l’API nécessaire. Cela permet une compatibilité descendante plus élevée et facilite les correctifs de rétroportage vers les versions plus anciennes.

## Exportez un ensemble restreint de packages à partir des lots OSGi. {#export-a-minimal-set-of-packages-from-osgi-bundles}

Lorsqu’un package a été exporté, une API a été créée pour que d’autres utilisateurs puissent en dépendre. Veillez à exporter le moins possible et à vérifier que ce qui est exporté est une API. Il est beaucoup plus facile de rendre publique une méthode/classe privée que de rendre privé un élément précédemment exporté.

Toujours placer les implémentations dans une *impl* module. Par défaut, la variable *maven-bundle-plugin* exporte tout élément du projet qui n’a pas de *impl* dans son nom.

## Définissez toujours explicitement une version sémantique pour chaque package exporté. {#always-explicitly-define-a-semantic-version-for-each-package-exported}

Cela permet aux consommateurs de votre API d’évoluer avec vous. Lorsque vous procédez de la sorte, respectez toujours les bonnes pratiques de contrôle de version sémantique. Cela permet aux clients de votre API de savoir quels types de modifications attendre dans une nouvelle version.

## Incluez les informations de métatype lorsqu’elles sont exposées. {#include-metatype-information-where-exposed}

En spécifiant des informations de métatype significatives, vous simplifiez la compréhension de vos services et composants dans la console Felix. La liste des attributs et annotations SCR peut être trouvée à l’adresse : [https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html](https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html).
