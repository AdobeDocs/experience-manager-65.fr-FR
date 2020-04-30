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
translation-type: tm+mt
source-git-commit: 77d00c1d6e94b257aa0533ca88b5f9a12dba0054

---


# Modèles de groupe {#group-templates}

La console Modèles de groupe est similaire à la console Modèles [de](/help/communities/sites.md) site. Ces deux éléments sont des plans pour un ensemble de pages préprogrammées et de fonctionnalités qui forment un site communautaire. La différence est qu&#39;un modèle de site est destiné à la communauté principale et qu&#39;un modèle de groupe est destiné à un groupe communautaire, une sous-communauté imbriquée dans la communauté principale.

Un groupe de communauté est incorporé dans un modèle de site en incluant la fonction [](/help/communities/functions.md#groups-function) Groupes (qui peut ne pas être la première ou la seule fonction dans le modèle).

Depuis le Pack de [fonctionnalités 1](/help/communities/deploy-communities.md#latestfeaturepack)Collectivités, il est possible d’imbriquer des groupes en incluant la fonction Groupes dans un modèle de groupe.

Au moment où une action est entreprise pour créer un nouveau groupe communautaire, le modèle (structure) du groupe est sélectionné. La sélection dépend de la manière dont la fonction Groupes a été configurée lorsqu’elle a été ajoutée au site ou au modèle de groupe.

>[!NOTE]
>
>Les consoles pour la création de sites [](/help/communities/sites-console.md)communautaires, de modèles [de sites](/help/communities/sites.md)communautaires, de modèles [de groupes](/help/communities/tools-groups.md) communautaires et de fonctions de [communauté ne sont utilisées que dans le  de l&#39;auteur.](/help/communities/functions.md)


## Console Modèles de groupe {#group-templates-console}

Pour accéder à la console des modèles de groupes dans l’ Auteur AEM  :

* Sélectionner les **outils| Communautés| Modèles de groupe,** à partir de la navigation globale.

Cette console affiche les modèles à partir desquels un site [](/help/communities/sites-console.md) communautaire peut être créé et permet de créer de nouveaux modèles de groupe.

![Modèle de groupes de communautés](assets/groups-template.png)

## Créer un modèle de groupe {#create-group-template}

Pour commencer à créer un modèle de groupe, sélectionnez `Create`.

Le panneau Editeur de site qui contient 3 sous-panneaux s’affiche alors :

### Informations de base {#basic-info}

![chlimage_1-137](assets/chlimage_1-137.png)

Dans le panneau Informations de base, un nom, une description et si le modèle est activé ou désactivé sont configurés :

* **Nom du nouveau modèle de groupe**

   ID du nom du modèle.

* **Description**

   Description du modèle.

* **Désactivé/Activé**

   Bascule contrôlant si le modèle peut être référencé.

#### Miniature   {#thumbnail}

![chlimage_1-138](assets/chlimage_1-138.png)

(Facultatif) Sélectionnez l’icône Télécharger l’image pour afficher une miniature ainsi que le nom et la description aux créateurs des sites de la communauté.

#### Structure {#structure}

>[!CAUTION]
>
>Si vous travaillez avec AEM 6.1 Communities FP4 ou version antérieure, n’ajoutez pas de fonction de groupes à un modèle de groupe.
>
>La fonction Groupes imbriqués est disponible à partir du [FP1](/help/communities/communities.md#latestfeaturepack)Communautés.
>
>Il n’est toujours pas autorisé d’ajouter une fonction Groupes en tant que première ou seule fonction dans un modèle.


![Éditeur de modèle de groupe](assets/template-editor.png)

Pour ajouter des fonctions de communauté, faites glisser le curseur de droite vers la gauche dans l&#39;ordre d&#39;affichage des liens du menu du site. Les styles seront appliqués au modèle lors de la création du site.

Par exemple, si vous souhaitez un forum, faites glisser la fonction de forum de la bibliothèque et déposez-la sous le créateur de modèles. La boîte de dialogue de configuration du forum s’ouvre alors. Pour plus d&#39;informations sur les boîtes de dialogue de configuration, consultez la console [des fonctions](/help/communities/functions.md) .

Continuez à faire glisser toutes les autres fonctions de la communauté souhaitées pour un site (groupe) de sous-communauté en fonction de ce modèle.

![faire glisser des fonctions](assets/dragfunctions.png)

Une fois que toutes les fonctions souhaitées ont été déposées dans la zone du créateur de modèles et configurées, sélectionnez **Enregistrer** dans le coin supérieur droit.

## Modifier le modèle de groupe {#edit-group-template}

Lors de l’affichage des groupes de la communauté dans la console [principale Modèles de](#group-templates-console)groupe, il est possible de sélectionner un modèle de groupe existant à modifier.

La modification d’un modèle de groupe n’affecte pas les sites de la communauté déjà créés à partir du modèle. Il est possible de [modifier directement la structure d&#39;un site](/help/communities/sites-console.md#modify-structure)communautaire.

Ce processus fournit les mêmes panneaux que la [création d’un modèle](#create-group-template)de groupe.
