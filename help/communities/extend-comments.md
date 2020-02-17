---
title: Extension du composant Commentaires
seo-title: Extension du composant Commentaires
description: Etendre le composant Commentaires pour modifier son apparence ou son comportement pour des utilisations spécifiques
seo-description: Etendre le composant Commentaires pour modifier son apparence ou son comportement pour des utilisations spécifiques
uuid: 6f439097-b1d0-4e7d-afcf-01d8f43aa866
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a07a4690-0e47-4a76-84cb-96abdc70b835
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Extension du composant Commentaires {#extend-comments-component}

L’intention d’ [étendre](client-customize.md#extensions) un composant par défaut est de modifier l’aspect ou le comportement d’un composant pour des utilisations spécifiques.

Le chemin d’accès au composant est unique et référence le composant par défaut en tant que type de super ressource. Il y a moins de risque, car la portée est limitée par rapport à la portée globale d’une superposition de composant.

>[!NOTE]
>
>L’extension d’un composant [superposé](client-customize.md#overlays) n’est pas prise en charge.

## Exemple {#example}

Supposons que l’en-tête du composant de commentaire s’affiche avec un aspect alternatif sur un site de l’instance AEM, lors de l’affichage par défaut sur un autre site. Au lieu de superposer le commentaire par défaut, qui modifie le composant de commentaire pour toutes les instances, une meilleure solution consiste à s’assurer que plusieurs composants de commentaire sont disponibles pour être utilisés sur différents sites.

Pour implémenter cette solution, créez un nouveau composant qui étend (remplace) le composant existant et modifiez le script Handlebars. La zone du site qui utilise les nouveaux commentaires peut utiliser le commentaire étendu, tandis que les sites qui utilisent l’aspect par défaut restent inchangés.

Le composant de commentaire est en fait l&#39;un des deux composants qui composent le système de commentaires. Il y a donc deux composantes à étendre : *commentaires* et *commentaires*. Le script à modifier se trouve dans le `header.hbs` fichier du composant *comment *alors que le composant de *commentaires* parent (le système de commentaires) est ce qu’un auteur ajoute réellement à la page.

Pour étendre les commentaires, vous devez :

1. [Création des composants](extend-create-components.md)
1. [Ajouter un commentaire à l&#39;exemple de page](extend-sample-page.md)
1. [Modifier l’aspect](extend-alter-appearance.md)

