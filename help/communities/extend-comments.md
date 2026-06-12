---
title: Composant Étendre les commentaires
description: Étendez le composant Commentaires pour modifier son apparence ou son comportement pour des utilisations spécifiques
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: e57198cb-8fd9-43e2-b416-e40e462561c8
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---

# Composant Étendre les commentaires  {#extend-comments-component}

L’objectif de l’extension [extension](client-customize.md#extensions) d’un composant par défaut est de modifier l’aspect ou le comportement d’un composant pour des utilisations spécifiques.

Le chemin d’accès au composant est unique et fait référence au composant par défaut en tant que type de super ressource. Le risque est moindre car la portée est limitée par rapport à la portée globale d’une superposition de composants.

>[!NOTE]
>
>L’extension d’un composant [recouvert](client-customize.md#overlays) n’est pas prise en charge.

## Exemple {#example}

Supposons que l’en-tête du composant Commentaire doive s’afficher avec une autre apparence sur un site de l’instance AEM, tout en s’affichant avec l’affichage par défaut sur un autre site. Au lieu de remplacer le commentaire par défaut, ce qui modifie le composant de commentaire pour toutes les instances, une meilleure solution consiste à s’assurer que plusieurs composants de commentaire sont disponibles pour une utilisation sur différents sites.

Pour implémenter cette solution, créez un composant qui étend (remplace) le composant existant et modifiez le script Handlebars. La zone du site qui utilise les nouveaux commentaires peut utiliser le commentaire étendu, tandis que les sites qui utilisent l&#39;apparence par défaut ne sont pas affectés.

Le composant « commentaire » est en fait l’un des deux composants qui composent le système de commentaires. Il existe donc deux composants à étendre : *commentaires* et *commentaire*. Le script à modifier se trouve dans le fichier `header.hbs` du composant *comment*, tandis que le composant parent *comments* (le système de commentaires) est ce qu’un auteur ajoute réellement à la page.

Pour étendre les commentaires, vous devez effectuer les opérations suivantes :

1. [Création des composants](extend-create-components.md)
1. [Ajouter un commentaire à l’exemple de page](extend-sample-page.md)
1. [Modifier l’apparence](extend-alter-appearance.md)
