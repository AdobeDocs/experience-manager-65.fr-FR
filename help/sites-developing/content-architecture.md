---
title: Architecture de contenu
description: Quelques conseils pour la conception de votre contenu (un indice - tout est contenu)
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: bcebbdb4-20b9-4c2d-8a87-013549d686c1
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 45%

---

# Architecture de contenu{#content-architecture}

## Suivez le modèle de David {#follow-david-s-model}

David&#39;s Model a été écrit par David Nuescheler il y a des années, mais les idées sont vraies aujourd&#39;hui. Les principaux principes du modèle de David sont les suivants :

* D’abord les données, ensuite la structure. OK.
* Dirigez la hiérarchie du contenu, ne laissez pas cela se produire.
* Les espaces de travail sont destinés à `clone()`, `merge()` et `update()`.
* Attention aux frères et soeurs du même nom.
* Les références sont considérées comme dangereuses.
* Les fichiers sont des fichiers.
* Les identifiants, c’est le mal.

David&#39;s Model se trouve sur le wiki Jackrabbit à l&#39;adresse : [https://wiki.apache.org/jackrabbit/DavidsModel](https://wiki.apache.org/jackrabbit/DavidsModel).

### Tout est contenu {#everything-is-content}

Tout doit être stocké dans le référentiel plutôt que de s’appuyer sur des sources de données tierces distinctes, telles que des bases de données. Cela s’applique au contenu créé, aux données binaires telles que les images, le code et les configurations. Cela nous permet d’utiliser un seul ensemble d’API pour gérer tout le contenu et gérer la promotion de ce contenu par le biais de la réplication. Vous obtenez également une source unique de sauvegarde, de journalisation, etc.

### Utiliser le principe de conception &quot;d’abord le modèle de contenu&quot; {#use-the-content-model-first-design-principle}

Lors de la mise au point d’une fonctionnalité, commencez toujours par concevoir la structure du contenu JCR, puis tâchez de lire et d’écrire votre contenu à l’aide des servlets Sling par défaut. Cela vous permet de vous assurer que votre mise en oeuvre fonctionne bien avec les mécanismes de contrôle d’accès prêts à l’emploi et d’éviter de générer des servlets inutiles de type CRUD.

### Soyez RESTful {#be-restful}

Les servlets doivent être définis en fonction des types de ressource plutôt que des chemins d’accès. Ainsi, il est possible d’utiliser les contrôles d’accès JCR, de respecter les principes REST, ainsi que d’utiliser la ressource et le résolveur de ressources qui sont mis à notre disposition dans la requête. Cela nous permet également de modifier les scripts qui effectuent le rendu des URL du côté serveur, sans devoir modifier une quelconque URL du côté client et sans révéler au client les détails d’implémentation côté serveur, d’où une sécurité accrue.

### Évitez de définir de nouveaux types de nœud {#avoid-defining-new-node-types}

Les types de nœud fonctionnent à un niveau inférieur du calque d’infrastructure. Il est, en outre, possible de répondre à la plupart des exigences en utilisant une propriété sling:resourceType affectée à un type de nœud nt:unstructured, oak:Unstructured, sling:Folder ou cq:Page. Les types de noeuds correspondent au schéma dans le référentiel et la modification des types de noeuds peut s’avérer coûteuse à long terme.

### Respectez les conventions de nommage dans le JCR {#adhere-to-naming-conventions-in-the-jcr}

Le respect des conventions d’appellation ajoute de la cohérence à votre base de code, ce qui réduit le taux d’incidence des défauts et accroît la vitesse des développeurs travaillant dans le système. Adobe respecte les conventions suivantes dans le cadre du développement d’AEM :

* Noms des noeuds

   * Toutes les minuscules
   * Séparation des mots à l’aide de tirets

* Noms de propriété

   * casse Camel, commençant par une lettre minuscule

* Composants (JSP/HTML)

   * Toutes les minuscules
   * Séparation des mots à l’aide de tirets
