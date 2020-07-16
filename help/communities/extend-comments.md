---
title: Étendre le composant Commentaires
seo-title: Étendre le composant Commentaires
description: Etendre le composant Commentaires pour modifier son apparence ou son comportement pour des utilisations spécifiques
seo-description: Etendre le composant Commentaires pour modifier son apparence ou son comportement pour des utilisations spécifiques
uuid: 6f439097-b1d0-4e7d-afcf-01d8f43aa866
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a07a4690-0e47-4a76-84cb-96abdc70b835
translation-type: tm+mt
source-git-commit: 230c700d87d82d248b7d0bbc45c69c5c2b0e3ff8
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---


# Étendre le composant Commentaires  {#extend-comments-component}

L’intention d’ [étendre](client-customize.md#extensions) un composant par défaut est de modifier l’aspect ou le comportement d’un composant pour des utilisations spécifiques.

Le chemin d&#39;accès au composant est unique et référence le composant par défaut comme un type de super-ressource. Il y a moins de risques, car la portée est limitée par rapport à la portée globale d’une incrustation de composant.

>[!NOTE]
>
>L’extension d’un composant [superposé](client-customize.md#overlays) n’est pas prise en charge.


## Exemple {#example}

Supposons que l’en-tête du composant de commentaire s’affiche avec un autre aspect sur un site de l’instance AEM, tout en s’affichant avec l’affichage par défaut sur un autre site. Au lieu de superposer le commentaire par défaut, qui modifie le composant de commentaire pour toutes les instances, une meilleure solution consiste à s’assurer que plusieurs composants de commentaire sont disponibles pour l’utilisation sur divers sites.

Pour mettre en oeuvre cette solution, créez un nouveau composant qui étend (remplace) le composant existant et modifiez le script Handlebars. La zone du site qui utilise les nouveaux commentaires peut utiliser le commentaire étendu, tandis que les sites qui utilisent l&#39;apparence par défaut restent inchangés.

Le composant de commentaire est en fait l&#39;un des deux composants qui composent le système de commentaires. Il y a donc deux composantes à étendre : *commentaires* et *commentaires*. Le script à modifier se trouve dans le *fichier du composant de* commentaire `header.hbs` , tandis que le composant de commentaires ** parent (le système de commentaires) est ce qu’un auteur ajoute effectivement à la page.

Pour ajouter des commentaires, vous devez :

1. [Création des composants](extend-create-components.md)
1. [Ajouter le commentaire à l&#39;exemple de page](extend-sample-page.md)
1. [Modification de l’aspect](extend-alter-appearance.md)

