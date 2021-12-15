---
title: Découvrez les bases de la modélisation de contenu
description: Découvrez la base de la modélisation du contenu pour votre CMS sans affichage à l’aide de fragments de contenu.
index: true
hide: false
hidefromtoc: false
source-git-commit: 99e7bb800da659fb8494eef2d9b9b87a6f263c21
workflow-type: tm+mt
source-wordcount: '905'
ht-degree: 46%

---

# Découvrez les bases de la modélisation de contenu pour sans affichage avec AEM {#content-modeling-headless-basics}

## L&#39;histoire jusqu&#39;à présent {#story-so-far}

Au début du [AEM Parcours d’architecture de contenu sans affichage](overview.md) la valeur [Introduction](introduction.md) couvrait les concepts de base et la terminologie relatifs à la modélisation du contenu pour les sans-tête.

Cet article s’appuie sur ces éléments afin que vous compreniez comment modéliser votre contenu pour votre projet AEM sans interface.

## Objectif {#objective}

* **Audience** : débutant
* **Objectif**: Découvrez les concepts de la modélisation de contenu pour un CMS sans affichage.

## Modélisation de contenu avec des modèles de fragment de contenu {#architect-content-fragment-models}

La modélisation de contenu (données) est un ensemble de techniques établies, souvent utilisées lors de bases de données de relations développées. Que signifie la modélisation de contenu pour AEM sans affichage ?

### Pourquoi ? {#why}

Pour que votre application puisse demander et recevoir le contenu requis d’AEM de manière cohérente et efficace, ce contenu doit être structuré.

Votre application connaît donc à l’avance la forme de réponse et, donc, comment la traiter. Cette approche est plus simple à traiter que de recevoir du contenu sous forme libre, qui doit être analysé pour déterminer ce qu’il contient et, donc, comment l’utiliser.

### Comment ? {#how}

AEM utilise des fragments de contenu pour fournir les structures nécessaires pour une diffusion en mode découplé de votre contenu vers vos applications.

La structure de votre modèle de contenu possède les caractéristiques suivantes :

* Elle est réalisée par la définition de votre modèle de fragment de contenu,
* Elle est utilisée comme base des fragments de contenu utilisés pour la génération de votre contenu.

>[!NOTE]
>
>Les modèles de fragment de contenu sont également utilisés comme base des schémas GraphQL d’AEM, utilisés pour récupérer votre contenu - pour en savoir plus à ce sujet dans le Parcours des développeurs.

Les demandes de contenu sont effectuées à l’aide de l’API AEM GraphQL, une mise en œuvre personnalisée de l’API GraphQL standard. L’API GraphQL AEM permet aux applications d’exécuter des requêtes (complexes) sur vos fragments de contenu, chaque requête étant en fonction d’un type de modèle spécifique.

Le contenu renvoyé peut alors être utilisé par vos applications.

## Création de la structure à l’aide de modèles de fragment de contenu {#create-structure-content-fragment-models}

Les modèles de fragment de contenu offrent divers mécanismes qui vous permettent de définir la structure de votre contenu.

Un modèle de fragment de contenu décrit une entité.

>[!NOTE]
>La fonctionnalité de fragment de contenu doit être activée dans l’explorateur de configurations afin que vous puissiez créer des modèles.

>[!TIP]
>
>Le modèle doit être nommé de sorte que l’auteur du contenu sache quel modèle sélectionner lors de la création d’un fragment de contenu.

Dans un modèle :

1. **Types de données** vous permet de définir les attributs individuels.
Par exemple, définissez le champ portant le nom d’un enseignant comme **Texte** et ses années de service comme **Nombre**.
1. Les types de données **Référence de contenu** et **Référence du fragment** permettent de créer des relations avec d’autres contenus dans AEM.
1. Le type de données **Référence du fragment** vous permet de réaliser plusieurs niveaux de structure en imbriquant vos fragments de contenu (en fonction du type de modèle). Ceci est essentiel pour la modélisation de contenu.

Par exemple :

![Modélisation de contenu avec des fragments de contenu](assets/headless-modeling-01.png "Modélisation de contenu avec des fragments de contenu")

## Types de données {#data-types}

AEM fournit les types de données suivants pour que vous puissiez modéliser votre contenu :

* Une seule ligne de texte
* Plusieurs lignes de texte
* Nombre
* Booléen
* Date et heure
* Énumération
* Balises
* Référence de contenu
* Référence du fragment
* Objet JSON

>[!NOTE]
>
>Pour plus d’informations, reportez-vous à la section Modèles de fragment de contenu - Types de données .

## Références et contenu imbriqué {#references-nested-content}

Deux types de données fournissent des références au contenu en dehors d’un fragment spécifique :

* **Référence de contenu**
Il s’agit d’une référence simple à tout autre contenu de n’importe quel type.
Par exemple, vous pouvez référencer une image à un emplacement spécifié.

* **Référence du fragment**
Cette section fournit des références à d’autres fragments de contenu.
Ce type de référence est utilisé pour créer du contenu imbriqué, présentant les relations nécessaires au modèle de votre contenu.
Le type de données peut être configuré pour permettre aux auteurs de fragments de procéder aux opérations suivantes :
   * Modifier directement le fragment référencé.
   * Créer un fragment de contenu, en fonction du modèle approprié.

>[!NOTE]
>
>Vous pouvez également créer des références ad hoc à l’aide de liens dans des blocs de texte.

## Niveaux de structure (fragments imbriqués) {#levels-of-structure-nested-fragments}

Pour la modélisation de contenu, le **Référence de fragment** Le type de données vous permet de créer plusieurs niveaux de structure et de relations.

Avec cette référence, vous pouvez *connect* divers modèles de fragment de contenu pour représenter les interrelations. Cela permet à l’application sans interface de suivre les connexions et d’accéder au contenu si nécessaire.

>[!NOTE]
>
>Cette méthode doit être utilisée avec précaution. La bonne pratique peut être définie comme *imbriquez autant que nécessaire, mais le moins possible.*.

C’est exactement ce que font les Références de fragment : elles vous permettent de référencer un autre fragment.

Par exemple, les modèles de fragment de contenu suivants peuvent être définis :

* Ville
* Société
* Personne
* Distinctions

Cela semble assez simple, mais bien sûr, une entreprise a à la fois un PDG et des employés....et ce sont tous des gens, chacun défini comme une Personne.

Et une Personne peut recevoir un Prix (ou peut-être deux).

* Mon entreprise - Société
   * PDG - Personne
   * Employé(s) - Personne
      * Prix(s) personnel(s) - Prix

Et c&#39;est juste pour commencer. En fonction de la complexité, une récompense peut être propre à une entreprise ou son siège social dans une ville donnée.

Vous pouvez représenter ces interrelations avec les Références de fragment, car elles sont comprises par vous (l’architecte), votre auteur de contenu et les applications sans interface.

## Et après ? {#whats-next}

Maintenant que vous avez appris les principes de base, l’étape suivante consiste à [En savoir plus sur la création de modèles de fragment de contenu dans AEM](model-structure.md). Cette section présente et discute les différentes références disponibles, ainsi que de la manière de créer des niveaux de structure avec les références de fragments, un élément clé de la modélisation pour les sans-tête.

## Ressources supplémentaires {#additional-resources}

* [Modèles de fragment de contenu](/help/assets/content-fragments/content-fragments-models.md)

   * [Modèles de fragment de contenu - Types de données](/help/assets/content-fragments/content-fragments-models.md#data-types)

* [Concepts de création](/help/sites-authoring/author.md)

* [Manipulation de base](/help/sites-authoring/basic-handling.md) - cette page est principalement basée sur la variable **Sites** console, mais de nombreuses fonctionnalités/la plupart sont également pertinentes pour la création **Fragments de contenu** sous le **Ressources** console.

* [Utilisation de fragments de contenu](/help/assets/content-fragments/content-fragments.md)
