---
title: Modèles de groupe
seo-title: Modèles de groupe
description: Accès à la console Modèles de groupe
seo-description: Accès à la console Modèles de groupe
uuid: 4cf20c91-32b0-4051-a98d-44e4eb50a231
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: e9bfbbce-93fc-455c-a2f7-4ee44e63c03f
docset: aem65
role: Administrator
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 3%

---


# Modèles de groupe {#group-templates}

La console Modèles de groupe est similaire à la console [Modèles de site](/help/communities/sites.md) . Il s’agit de plans directeurs pour un ensemble de pages préconfigurées et de fonctionnalités qui forment un site communautaire. La différence est qu’un modèle de site est destiné à la communauté principale et qu’un modèle de groupe est destiné à un groupe de communauté, une sous-communauté imbriquée dans la communauté principale.

Un groupe de communautés est intégré dans un modèle de site en incluant la [fonction Groupes](/help/communities/functions.md#groups-function) (qui ne peut pas être la première fonction ou la seule dans le modèle).

À partir de Communities [Feature Pack 1](/help/communities/deploy-communities.md#latestfeaturepack), il est possible d’imbriquer des groupes en incluant la fonction Groupes dans un modèle de groupe.

Dès qu’une action est entreprise pour créer un nouveau groupe communautaire, le modèle (structure) du groupe est sélectionné. La sélection dépend de la manière dont la fonction Groupes a été configurée lorsqu’elle a été ajoutée au site ou au modèle de groupe.

>[!NOTE]
>
>Les consoles pour la création de [sites de communauté](/help/communities/sites-console.md), [modèles de site de communauté](/help/communities/sites.md), [modèles de groupe de communauté](/help/communities/tools-groups.md) et [fonctions de communauté](/help/communities/functions.md) ne peuvent être utilisées que dans l’environnement de création.

## Console Modèles de groupe {#group-templates-console}

Pour accéder à la console de modèles de groupes dans l’environnement de création AEM :

* Sélectionnez **Outils | Communautés | Modèles de groupe,** à partir de la navigation globale.

Cette console affiche les modèles à partir desquels un [site communautaire](/help/communities/sites-console.md) peut être créé et permet de créer des modèles de groupe.

![Modèle de groupes de communautés](assets/groups-template.png)

## Créer un modèle de groupe {#create-group-template}

Pour commencer à créer un modèle de groupe, sélectionnez `Create`.

Le panneau Éditeur de site s’affiche alors et contient trois sous-panneaux :

### Informations de base {#basic-info}

![site-basic-info](assets/site-basic-info.png)

Dans le panneau Informations de base , un nom, une description et si le modèle est activé ou désactivé sont configurés :

* **Nom du nouveau modèle de groupe**

   ID du nom du modèle.

* **Description**

   Description du modèle.

* **Désactivé/activé**

   Bascule contrôlant si le modèle est référencable.

#### Miniature  {#thumbnail}

![site-thumbnail](assets/site-thumbnail.png)

(Facultatif) Sélectionnez l’icône Télécharger l’image pour afficher une miniature ainsi que le nom et la description aux créateurs des sites de la communauté.

#### Structure {#structure}

>[!CAUTION]
>
>Si vous utilisez AEM 6.1 Communities FP4 ou une version antérieure, n’ajoutez pas de fonction de groupe à un modèle de groupe.
>
>La fonction Groupes imbriqués est disponible à partir de Communities [FP1](/help/communities/communities.md#latestfeaturepack).
>
>Il n’est toujours pas autorisé d’ajouter une fonction Groupes comme première ou seule fonction dans un modèle.

![Éditeur de modèle de groupe](assets/template-editor.png)

Pour ajouter des fonctions de communauté, faites glisser du côté droit vers la gauche dans l’ordre dans lequel doivent apparaître les liens du menu du site. Des styles seront appliqués au modèle lors de la création du site.

Par exemple, si vous souhaitez un forum, faites glisser la fonction de forum depuis la bibliothèque et déposez-la sous le créateur de modèles. La boîte de dialogue de configuration du forum s’ouvre alors. Voir la [console des fonctions](/help/communities/functions.md) pour plus d’informations sur les boîtes de dialogue de configuration.

Continuez à faire glisser et déposer toutes les autres fonctions de la communauté souhaitées pour un site (groupe) de sous-communauté basé sur ce modèle.

![déplacement de fonctions](assets/dragfunctions.png)

Une fois que toutes les fonctions souhaitées ont été déposées dans la zone du créateur de modèles et configurées, sélectionnez **Enregistrer** dans le coin supérieur droit.

## Modifier le modèle de groupe {#edit-group-template}

Lors de l’affichage de groupes de communautés dans la [console Modèles de groupe](#group-templates-console) principale, il est possible de sélectionner un modèle de groupe existant à modifier.

La modification d’un modèle de groupe n’affecte pas les sites de communauté déjà créés à partir du modèle. Il est possible de modifier directement [la structure d’un site communautaire](/help/communities/sites-console.md#modify-structure) à la place.

Ce processus fournit les mêmes panneaux que la [création d’un modèle de groupe](#create-group-template).
