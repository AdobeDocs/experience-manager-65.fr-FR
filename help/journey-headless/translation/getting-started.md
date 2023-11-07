---
title: Prise en main de la traduction découplée dans AEM
description: Découvrez comment organiser votre contenu découplé et comment fonctionnent les outils de traduction AEM.
exl-id: 764f78a7-1d3d-4406-85b1-b80dffae2350
source-git-commit: fc2f26a69c208947c14e8c6036825bb217901481
workflow-type: tm+mt
source-wordcount: '1489'
ht-degree: 92%

---

# Prise en main de la traduction découplée dans AEM {#getting-started}

Découvrez comment organiser votre contenu découplé et comment fonctionnent les outils de traduction AEM.

## Un peu d’histoire… {#story-so-far}

Dans le document précédent relatif au parcours de traduction découplée AEM, [Découvrir le contenu découplé et comment le traduire dans AEM](learn-about.md), vous avez appris la théorie de base d’un CMS découplé et vous devriez maintenant :

* comprendre les concepts de base de la diffusion de contenus en mode découplé ;
* être familiarisé avec la façon dont AEM prend en charge le découplage et la traduction.

Cet article s’appuie sur ces principes de base afin que vous compreniez comment AEM stocke et gère le contenu découplé et comment vous pouvez utiliser les outils de traduction AEM pour traduire ce contenu.

## Objectif {#objective}

Ce document vous aide à comprendre comment commencer à traduire le contenu découplé dans AEM. Après avoir lu ce document, vous devriez :

* comprendre l’importance de la structure de contenu pour la traduction ;
* savoir comment AEM stocke du contenu découplé ;
* être familiarisé avec les outils de traduction AEM.

## Exigences et conditions préalables {#requirements-prerequisites}

Avant de commencer à traduire votre contenu d’AEM sans interface utilisateur graphique, plusieurs exigences s’appliquent.

### Connaissances {#knowledge}

* Expérience de la traduction de contenu dans un CMS
* Expérience d’utilisation des fonctionnalités de base d’un CMS à grande échelle
* Connaissance pratique de la manipulation de base d’AEM
* Compréhension du service de traduction que vous utilisez
* Compréhension de base du contenu que vous traduisez

>[!TIP]
>
>Si vous n’êtes pas familier avec l’utilisation d’un CMS à grande échelle tel qu’AEM, pensez à consulter la documentation intitulée [Manipulation de base](/help/sites-authoring/basic-handling.md) avant de continuer. La documentation Manipulation de base ne fait pas partie du parcours. Vous pouvez donc revenir à cette page une fois l’opération terminée.

### Outils {#tools}

* Accès aux sandbox pour tester la traduction de votre contenu
* Informations d’identification pour vous connecter à votre service de traduction préféré
* Accréditation en tant que membre du groupe `projects-administrators` dans AEM

## La structure est la clé {#content-structure}

Le contenu AEM, qu’il s’agisse de pages web découplée ou traditionnelles, est piloté par sa structure. AEM impose peu d’exigences à la structure de contenu, mais une prise en compte attentive de votre hiérarchie de contenu dans le cadre de la planification du projet peut rendre la traduction beaucoup plus simple.

>[!TIP]
>
>Planifiez la traduction dès le début de votre projet découplé. Collaborez rapidement avec le chef de projet et les architectes de contenu.
>
>Il peut s’avérer nécessaire d’impliquer un gestionnaire de projets d’internationalisation en tant que personne distincte. Sa responsabilité consiste à définir les contenus à traduire et ceux qui ne doivent pas l’être, et les contenus traduits qui peuvent être modifiés par les producteurs de contenus régionaux ou locaux.

## Stockage du contenu découplé dans AEM {#headless-content-in-aem}

En tant que spécialiste de la traduction, il n’est pas nécessaire de comprendre en profondeur la manière dont AEM gère le contenu découplé. Toutefois, il sera utile de connaître les concepts de base et la terminologie lorsque vous utiliserez les outils de traduction AEM. Plus important encore, vous devez comprendre votre propre contenu et la manière dont il est structuré pour le traduire efficacement.

### Modèles de contenu {#content-models}

Pour que le contenu découplé puisse être diffusé de manière cohérente sur plusieurs canaux, régions et langues, il doit être parfaitement structuré. AEM utilise des modèles de contenu pour appliquer cette structure. Considérez les modèles de contenu comme une sorte de modèle ou de motif pour créer du contenu découplé. Chaque projet ayant ses propres besoins, chaque projet définit ses propres modèles de fragment de contenu. AEM ne dispose pas d’une configuration ou d’une structure fixe pour de tels modèles.

L’architecte de contenu travaille à définir cette structure dès le début du projet. En tant que spécialiste de la traduction, vous devez travailler en étroite collaboration avec l’architecte de contenu pour comprendre et organiser le contenu.

>[!NOTE]
>
>Il incombe à l’architecte de contenu de définir les modèles de contenu. Le spécialiste de la traduction ne doit connaître que sa structure, comme indiqué dans les étapes suivantes.

Comme les modèles de contenu définissent la structure de votre contenu, vous devez savoir quels champs de vos modèles doivent être traduits. En règle générale, vous travaillez avec l’architecte de contenu pour définir ces éléments. Pour parcourir les champs de vos modèles de contenu, procédez comme suit.

1. Accédez à **Outils**, **Ressources** -> **Modèles de fragment de contenu**.
1. Les modèles de fragment de contenu sont généralement stockés dans une structure de dossiers. Appuyez ou cliquez sur le dossier de votre projet.
1. Les modèles y sont répertoriés. Appuyez ou cliquez sur le modèle pour afficher les détails.
   ![Modèles de fragment de contenu](assets/content-fragment-models.png)
1. L’**Éditeur de modèle de fragment de contenu** s’ouvre.
   1. La colonne de gauche contient les champs du modèle. C’est cette colonne qui nous intéresse.
   1. La colonne de droite contient les champs qui peuvent être ajoutés au modèle. Nous pouvons ignorer cette colonne.
      ![Éditeur de modèles de fragment de contenu](assets/content-fragment-model-editor.png)
1. Appuyez ou cliquez sur l’un des champs du modèle. AEM le coche et les détails de ce champ s’affichent dans la colonne de droite.
   ![Détail de l’Éditeur de modèles de fragment de contenu](assets/content-fragment-model-editor-detail.png)

Notez le contenu du champ **Nom de la propriété** pour tous les champs qui doivent être traduits. Vous aurez besoin de ces informations plus tard dans le parcours. Ces **Noms de la propriété** sont nécessaires pour indiquer à AEM quels champs de votre contenu doivent être traduits.

>[!TIP]
>
>En règle générale, l’architecte de contenu met à la disposition du spécialiste de traduction les éléments suivants : **Nom de la propriété** de tous les champs requis pour la traduction. Ces noms de champ sont nécessaires pour les étapes suivantes du parcours. Les étapes précédentes sont détaillées pour une meilleure compréhension du spécialiste de la traduction.

### Fragments de contenu {#content-fragments}

Les modèles de contenu sont utilisés par les auteurs de contenu pour créer le véritable contenu découplé. Les auteurs de contenu sélectionnent le modèle sur lequel baser leur contenu, puis créent des fragments de contenu. Les fragments de contenu sont des instances de ces modèles et représentent le véritable contenu à diffuser en mode découplé.

Si les modèles de contenu correspondent aux motifs de contenu, les fragments de contenu correspondent au véritable contenu basé sur ces modèles. Les fragments de contenu représentent le contenu qui doit être traduit.

Les fragments de contenu sont gérés en tant que ressources dans AEM dans le cadre de la gestion des ressources numériques (DAM). Ce point est important, car ils se trouvent tous sous le chemin d’accès `/content/dam`.

## Structure de contenu recommandée {#recommended-structure}

Comme recommandé précédemment, travaillez avec votre architecte de contenu pour déterminer la structure de contenu appropriée pour votre projet. Cependant, vous trouverez ci-dessous une structure éprouvée, simple et intuitive, tout en étant assez efficace.

Définissez un dossier de base pour votre projet, sous `/content/dam`.

```text
/content/dam/<your-project>
```

La langue dans laquelle votre contenu est créé est appelée racine de langue. Dans notre exemple, il s’agit de l’anglais, et il doit se trouver sous ce chemin.

```text
/content/dam/<your-project>/en
```

Tout le contenu de projet qui pourrait être localisé doit être placé sous la racine de langue.

```text
/content/dam/<your-project>/en/<your-project-content>
```

Les traductions doivent être créées dans des dossiers frères à côté de la racine de langue avec leur nom de dossier représentant le code de langue ISO-2 de la langue. Par exemple, l’allemand correspondrait au chemin suivant.

```text
/content/dam/<your-project>/de
```

>[!NOTE]
>
>L’architecte de contenu est généralement chargé de créer ces dossiers de langue. Sans ces dossiers, AEM ne pourra pas créer ultérieurement de tâches de traduction.

La structure finale peut ressembler à ce qui suit.

```text
/content
    |- dam
        |- your-project
            |- en
                |- some
                |- exciting
                |- headless
                |- content
            |- de
            |- fr
            |- it
            |- ...
        |- another-project
        |- ...
```

Vous devez prendre note du chemin spécifique de votre contenu, car il sera ensuite nécessaire pour configurer votre traduction.

>[!NOTE]
>
>Il incombe généralement à l’architecte de contenu de définir la structure du contenu, mais il peut collaborer avec le spécialiste de traduction.
>
>Cette structure est présentée ici pour plus de clarté.

## Outils de traduction AEM {#translation-tools}

Maintenant que vous comprenez ce que sont les fragments de contenu et l’importance de la structure de contenu, nous pouvons examiner comment traduire ce contenu. Les outils de traduction AEM sont puissants, mais faciles à comprendre dans l’ensemble.

* **Connecteur de traduction** : le connecteur représente le lien entre AEM et le service de traduction que vous utilisez.
* **Règles de traduction** : les règles définissent quel contenu doit être traduit en fonction de chemins spécifiques.
* **Projets de traduction** : les projets de traduction rassemblent le contenu qui doit être traité comme une tâche de traduction unique et consignent l’avancement de la traduction, interagissent avec le connecteur pour transmettre le contenu à traduire et le recevoir du service de traduction.

En règle générale, vous ne configurez votre connecteur qu’une seule fois pour votre instance et les règles pour chaque projet découplé. Ensuite, vous utilisez des projets de traduction pour traduire votre contenu et conserver ses traductions à jour en permanence.

## Prochaines étapes {#what-is-next}

Maintenant que vous avez terminé cette partie du parcours de traduction découplée, vous devriez savoir :

* comprendre l’importance de la structure de contenu pour la traduction ;
* savoir comment AEM stocke du contenu découplé ;
* être familiarisé avec les outils de traduction AEM.

Tirez parti de ces connaissances et continuez votre parcours de traduction AEM sans interface utilisateur graphique en consultant le document. [Configuration de l’intégration de traduction](configure-connector.md) où vous apprendrez à connecter AEM à un service de traduction.|

## Ressources supplémentaires {#additional-resources}

Bien qu’il soit recommandé de passer à la partie suivante du parcours de traduction découplée en consultant le document [Configuration du connecteur de traduction](configure-connector.md), vous trouverez ci-après quelques ressources supplémentaires qui, bien que facultatives, vous aideront à approfondir un certain nombre de concepts mentionnés dans ce document, sans qu’ils soient obligatoires pour poursuivre votre parcours en mode découplé.

* [Manipulation de base d’AEM](/help/sites-authoring/basic-handling.md) : découvrez les principes de base de l’interface utilisateur d’AEM pour pouvoir naviguer facilement et effectuer les tâches essentielles, comme celles vous permettant de trouver votre contenu.
* [Identification du contenu à traduire](/help/sites-administering/tc-rules.md) : découvrez comment les règles de traduction identifient le contenu à traduire.
* [Configuration du framework d’intégration de la traduction](/help/sites-administering/tc-tic.md) : découvrez comment configurer le framework d’intégration de la traduction pour l’intégrer à des services de traduction tiers.
* [Gestion de projets de traduction](/help/sites-administering/tc-manage.md) : découvrez comment créer et gérer des projets de traduction automatique et humaine dans AEM.
* Un [Présentation d’AEM en tant que CMS sans affichage](/help/sites-developing/headless/introduction.md)
* La variable [AEM Developer Portal](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=fr)
* [Tutoriels pour Headless dans AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=fr)
