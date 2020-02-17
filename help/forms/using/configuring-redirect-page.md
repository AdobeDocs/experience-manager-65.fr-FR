---
title: Configuration de la page de redirection
seo-title: Configuration de la page de redirection
description: Après avoir complété un formulaire adaptatif, les utilisateurs peuvent être redirigés vers une page Web que les auteurs de formulaires peuvent configurer lors de la phase de création.
seo-description: Après avoir complété un formulaire adaptatif, les utilisateurs peuvent être redirigés vers une page Web que les auteurs de formulaires peuvent configurer lors de la phase de création.
uuid: f9d304b4-920d-4e50-a674-40eca48c530c
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 0ffbb4d3-9371-4705-8496-f98e22d9c4a6
docset: aem65
translation-type: tm+mt
source-git-commit: 8e724af4d69cb859537dd088119aaca652ea3931

---


# Configuration de la page de redirection{#configuring-redirect-page}

Pour chaque formulaire, les auteurs peuvent configurer une page vers laquelle les utilisateurs seront redirigés après l’envoi du formulaire.

1. In the edit mode, select a component, then click ![field-level](assets/field-level.png) > **Adaptive Form Container**, and then click ![cmppr](assets/cmppr.png).

1. Dans la barre latérale, cliquez sur **Envoi**. 

1. Indiquez L’URL de la page de redirection sous Page de remerciement dans la section Envoyer. 
1. Sous Action Envoyer, vous pouvez éventuellement configurer le paramètre à transmettre à la page de redirection pour l’action Envoyer vers le point de fin REST.

![Configuration de la page de redirection](assets/thank-you-setting-1.png)

Configuration de la page de redirection

Les auteurs de formulaires peuvent utiliser les paramètres suivants qui sont transmis à la page de remerciement. For all the available submit actions, `status` and `owner` parameters are passed. Outre ces deux paramètres, des paramètres supplémentaires sont transmis pour les actions d’envoi suivantes :

* **Action** Stocker le contenu (obsolète) : `contentPath`(chemin d’accès du noeud dans le référentiel où sont stockées les données envoyées) est transmis.

* **Action** Stocker le PDF (obsolète) : `contentPath`(des données envoyées et du chemin d’accès au noeud stockant le fichier PDF dans le référentiel) est transmis.

* **Flux de travail Envoyer aux formulaires** : les paramètres de sortie renvoyés à partir du flux de travail des formulaires sont transmis.

* **Envoyer vers le point de fin REST** : les paramètres ajoutés pour la correspondance entre le champ et le paramètre sont transmis. Les paramètres `status` et `owner` ne sont pas transmis à cette action d’envoi. Pour en savoir plus, consultez [Configuration de l’action d’envoi Envoyer vers le point de fin REST](../../forms/using/configuring-submit-actions.md). 

