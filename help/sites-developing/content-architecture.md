---
title: Architecture de contenu
description: Quelques conseils pour la conception de votre contenu (un indice - tout est contenu)
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: bcebbdb4-20b9-4c2d-8a87-013549d686c1
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 97%

---

# Architecture de contenu{#content-architecture}

## Suivre le modèle de David {#follow-david-s-model}

Le modèle de David a été élaboré par David Nuescheler il y a quelques années. Cependant, ses principes sont toujours valables aujourd’hui. Voici les principes fondamentaux du modèle de David :

* D’abord les données, ensuite la structure. OK.
* Dirigez la hiérarchie du contenu, ne la laissez pas se produire.
* Les espaces de travail sont destinés à `clone()`, `merge()` et `update()`.
* Attention aux parents portant le même nom.
* Les références sont considérées comme dangereuses.
* Les fichiers sont des fichiers.
* Les identifiants sont diaboliques.

Pour consulter le modèle de David, accédez au wiki Jackrabbit à l’adresse [https://wiki.apache.org/jackrabbit/DavidsModel](https://wiki.apache.org/jackrabbit/DavidsModel).

### Tout est du contenu. {#everything-is-content}

Tout doit être stocké dans le référentiel plutôt que de s’appuyer sur des sources de données tierces distinctes, telles que des bases de données. Cela s’applique au contenu créé, aux données binaires telles que les images, le code et les configurations. Cela nous permet d’utiliser un seul ensemble d’API pour gérer tout le contenu et gérer la promotion de ce contenu par le biais de la réplication. Vous obtenez également une source unique de sauvegarde, de journalisation, etc.

### Utiliser le principe de conception « priorité au modèle de contenu » {#use-the-content-model-first-design-principle}

Lors de la mise au point d’une fonctionnalité, commencez toujours par concevoir la structure du contenu JCR, puis tâchez de lire et d’écrire votre contenu à l’aide des servlets Sling par défaut. Vous pouvez ainsi vous assurer que votre implémentation fonctionne bien avec des mécanismes de contrôle d’accès standard. Cela vous évite également de générer des servlets de type CRUD inutiles.

### Soyez RESTful {#be-restful}

Les servlets doivent être définis en fonction des types de ressource plutôt que des chemins d’accès. Ainsi, il est possible d’utiliser les contrôles d’accès JCR, de respecter les principes REST, ainsi que d’utiliser la ressource et le résolveur de ressources qui sont mis à notre disposition dans la requête. Cela nous permet également de modifier les scripts qui effectuent le rendu des URL du côté serveur, sans devoir modifier une quelconque URL du côté client et sans révéler au client les détails d’implémentation côté serveur, d’où une sécurité accrue.

### Évitez de définir de nouveaux types de nœud {#avoid-defining-new-node-types}

Les types de nœud fonctionnent à un niveau inférieur du calque d’infrastructure. Il est, en outre, possible de répondre à la plupart des exigences en utilisant une propriété sling:resourceType affectée à un type de nœud nt:unstructured, oak:Unstructured, sling:Folder ou cq:Page. Les types de nœud correspondent au schéma dans le référentiel. Changer de type de nœud peut s’avérer coûteux à terme.

### Respect des conventions de nommage dans le JCR {#adhere-to-naming-conventions-in-the-jcr}

Le respect des conventions de nommage ajoute de l’homogénéité à votre codebase en réduisant le taux d’incidence des défauts et en augmentant la vitesse de l’équipe de développement qui travaille sur le système. Adobe respecte les conventions suivantes dans le cadre du développement d’AEM :

* Noms des nœuds

   * Tout en minuscules
   * Séparation des mots à l’aide de tirets

* Noms des propriétés

   * Camel case, commençant par une lettre minuscule

* Composants (JSP/HTML)

   * Tout en minuscules
   * Séparation des mots à l’aide de tirets
