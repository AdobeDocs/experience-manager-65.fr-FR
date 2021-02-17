---
title: Lots OSGi
seo-title: Lots OSGi
description: Conseils pour gérer vos lots OSGi.
seo-description: Conseils pour gérer vos lots OSGi.
uuid: 07af7089-a233-4e5b-928c-76ddc0af8839
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8d3374ac-51dd-4ff5-84c9-495c937ade12
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 89%

---


# Lots OSGi{#osgi-bundles}

## Utilisez le contrôle de version sémantique.{#use-semantic-versioning}

Les meilleures pratiques en matière de numérotation des versions sémantiques sont convenues à l’adresse [https://semver.org/](https://semver.org/).

## N’incorporez pas d’autres classes et fichiers JAR que ceux strictement nécessaires dans les lots OSGi.{#do-not-embed-more-classes-and-jars-than-strictly-needed-in-osgi-bundles}

Les bibliothèques courantes doivent être factorisées dans des lots distincts. Cela leur permet d’être réutilisées dans vos lots. Lorsque vous encapsulez un fichier *JAR* dans un lot OSGi, prenez soin de vérifier dans les sources en ligne si quelqu’un a effectué cette opération auparavant. Voici certains des principaux lieux dans lesquels vous pouvez trouver les wrappers de lots existants : Apache Felix, Apache Sling, Apache Geronimo, Apache ServiceMix, Eclipse Bundle Recipes et le référentiel SpringSource Enterprise Bundle Repository.

## Dépendez des plus anciennes versions de lots nécessaires. {#depend-on-the-lowest-needed-bundle-versions}

Pour les dépendances au moment de la compilation dans les fichiers POM, utilisez toujours la plus ancienne version nécessaire qui expose l’API requise. Cela permet davantage de compatibilité ascendante et facilite les correctifs de rétroportage des versions plus anciennes.

## Exportez un ensemble restreint de modules à partir des lots OSGi.{#export-a-minimal-set-of-packages-from-osgi-bundles}

Dès qu’un module a été exporté, nous avons créé une API dont les autres peuvent dépendre. Veillez à exporter le moins possible et à vérifier que ce qui est exporté est une API. Il est beaucoup plus facile de rendre publique une méthode/classe privée que de rendre privé un élément précédemment exporté.

Les mises en œuvre doivent toujours être placées dans un module *impl* distinct. Par défaut, *maven-bundle-plugin* exporte tout ce qui se trouve dans le projet et dont le nom ne contient pas *impl*.

## Définissez toujours explicitement une version sémantique pour chaque module exporté.  {#always-explicitly-define-a-semantic-version-for-each-package-exported}

Cela permet aux consommateurs de votre API d’évoluer avec vous. Lorsque vous procédez de la sorte, respectez toujours les meilleures pratiques de contrôle de version sémantique. Cela permet aux consommateurs de votre API de déterminer les types de modifications à attendre dans une nouvelle version.

## Incluez les informations de métatype lorsqu’elles sont exposées.{#include-metatype-information-where-exposed}

En spécifiant des informations de métatype pertinentes, vos services et composants sont plus faciles à comprendre dans la console Felix. Vous trouverez une liste des annotations et des attributs SCR à l&#39;adresse suivante : [https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html](https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html).
