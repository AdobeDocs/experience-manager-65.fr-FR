---
title: Extension du composant Commentaires
seo-title: Extension du composant Commentaires
description: Étendre le composant Commentaires afin de modifier son apparence ou son comportement pour des utilisations spécifiques
seo-description: Étendre le composant Commentaires afin de modifier son apparence ou son comportement pour des utilisations spécifiques
uuid: 6f439097-b1d0-4e7d-afcf-01d8f43aa866
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a07a4690-0e47-4a76-84cb-96abdc70b835
exl-id: e57198cb-8fd9-43e2-b416-e40e462561c8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# Étendre le composant Commentaires {#extend-comments-component}

L’intention de [étendre](client-customize.md#extensions) un composant par défaut est de modifier l’aspect ou le comportement d’un composant pour des utilisations spécifiques.

Le chemin d’accès au composant est unique et référence le composant par défaut comme type de super-ressource. Il y a moins de risque, car la portée est limitée par rapport à la portée globale d’une superposition de composant.

>[!NOTE]
>
>L’extension d’un composant [superposé](client-customize.md#overlays) n’est pas prise en charge.

## Exemple {#example}

Supposons que l’en-tête du composant de commentaire s’affiche différemment sur un site de l’instance AEM, tout en s’affichant avec l’affichage par défaut sur un autre site. Au lieu de superposer le commentaire par défaut, qui modifie le composant de commentaire pour toutes les instances, une meilleure solution consiste à s’assurer que plusieurs composants de commentaire sont disponibles pour utilisation sur différents sites.

Pour mettre en oeuvre cette solution, créez un composant qui étend (remplace) le composant existant et modifiez le script Handlebars. La zone du site qui utilise les nouveaux commentaires peut utiliser le commentaire étendu, tandis que les sites qui utilisent l’aspect par défaut restent inchangés.

Le composant de commentaire est en fait l’un des deux composants qui composent le système de commentaires. Il existe donc deux composants à étendre : *commentaires* et *commentaire*. Le script à modifier se trouve dans le fichier `header.hbs` du composant *comment*, tandis que le composant *commentaires* parent (le système de commentaires) est ce qu’un auteur ajoute réellement à la page.

Pour étendre les commentaires, vous devez :

1. [Création des composants](extend-create-components.md)
1. [Ajout d’un commentaire à un exemple de page](extend-sample-page.md)
1. [Modification de l’aspect](extend-alter-appearance.md)
