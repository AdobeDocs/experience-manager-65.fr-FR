---
title: Extension du composant Commentaires
description: Étendre le composant Commentaires afin de modifier son apparence ou son comportement pour des utilisations spécifiques
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

# Extension du composant Commentaires  {#extend-comments-component}

L’intention de [extension](client-customize.md#extensions) un composant par défaut consiste à modifier l’aspect ou le comportement d’un composant pour des utilisations spécifiques.

Le chemin d’accès au composant est unique et référence le composant par défaut comme type de super-ressource. Il y a moins de risque, car la portée est limitée par rapport à la portée globale d’une superposition de composant.

>[!NOTE]
>
>Extension d’une [superposé](client-customize.md#overlays) n’est pas pris en charge.

## Exemple {#example}

Supposons que l’en-tête du composant de commentaire s’affiche différemment sur un site de l’instance AEM, tout en s’affichant avec l’affichage par défaut sur un autre site. Au lieu de superposer le commentaire par défaut, qui modifie le composant de commentaire pour toutes les instances, une meilleure solution consiste à s’assurer que plusieurs composants de commentaire sont disponibles pour utilisation sur différents sites.

Pour mettre en oeuvre cette solution, créez un composant qui étend (remplace) le composant existant et modifiez le script Handlebars. La zone du site qui utilise les nouveaux commentaires peut utiliser le commentaire étendu, tandis que les sites qui utilisent l’aspect par défaut restent inchangés.

Le composant de commentaire est en fait l’un des deux composants qui composent le système de commentaires. Il existe donc deux composants à étendre : *commentaires* et *comment*. Le script à modifier se trouve dans la variable *comment* du composant `header.hbs` pendant que le fichier parent *commentaires* component (le système de commentaires) est ce qu’un auteur ajoute réellement à la page.

Pour étendre les commentaires, vous devez :

1. [Création des composants](extend-create-components.md)
1. [Ajouter un commentaire à un exemple de page](extend-sample-page.md)
1. [Modification de l’aspect](extend-alter-appearance.md)
