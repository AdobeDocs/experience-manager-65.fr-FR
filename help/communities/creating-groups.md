---
title: Groupes communautaires
description: Découvrez comment la fonction de groupes de communautés vous permet de créer dynamiquement une sous-communauté au sein d’un site de communauté par des utilisateurs autorisés dans Publier et créer.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: edcda6cb-df47-4afe-8a9a-82d8e386fe05
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 1%

---

# Groupes communautaires {#community-groups}

La fonctionnalité de groupes de communautés permet à une sous-communauté d’être créée dynamiquement dans un site de communauté par des utilisateurs autorisés (membres de la communauté et auteurs) à partir des environnements de publication et de création.

Cette fonctionnalité est présente lorsque la variable [fonction groups](/help/communities/functions.md#groups-function) est présent dans la variable [site communautaire](/help/communities/sites-console.md) structure.

A [modèle de groupe de communautés](/help/communities/tools-groups.md) fournit la conception de la page de groupe de communautés lorsqu’un groupe de communautés est créé dynamiquement.

Un ou plusieurs modèles de groupe sont sélectionnés pour la fonction de groupes lorsque la fonction est ajoutée à la structure d’un site de communauté ou à un modèle de site de communauté. Cette liste de modèles de groupe est présentée au membre ou à l’auteur qui crée dynamiquement un groupe à partir du site de la communauté.

## Création d’un groupe {#creating-a-new-group}

La possibilité de créer un groupe de communautés dépend de l’existence d’un site de communauté qui inclut la fonction de groupes, comme celui créé à partir de la fonction [Modèle de site de référence](/help/communities/sites.md).

Les exemples qui suivent utilisent le site de la communauté créé à partir du `Reference Site Template` comme décrit dans la section [Prise en main d’AEM Communities](/help/communities/getting-started.md) tutoriel .

Il s’agit de la page qui se charge lors de la publication lorsque la variable **Groupes** est sélectionnée :

![new-group](assets/new-group.png)

Lorsque vous sélectionnez la variable **Nouveau groupe** , une boîte de dialogue de modification s’ouvre.

Sous , **Paramètres** , vous fournissez les fonctions de base du groupe :

![group-settings](assets/group-settings.png)

* **Nom du groupe**

  Titre du groupe que vous souhaitez afficher sur le site de la communauté. Évitez d’utiliser des caractères de soulignement (_) et des mots-clés tels que des ressources et une configuration dans le nom du groupe.

* **Description**

  Description du groupe à afficher sur le site de la communauté.

* **Invitation**

  Liste des membres à inviter au groupe. La recherche par type fournit des suggestions aux membres de la communauté à inviter.

* **Nom de l’URL du groupe**

  Nom de la page de groupe qui devient une partie de l’URL.

* **Ouvrir le groupe**

  Sélection `Open Group` indique que tout visiteur anonyme du site peut afficher le contenu et désélectionne `Member Only Group`.

* **Groupe de membres uniquement**

  Sélection `Member Only Group` indique que seuls les membres du groupe peuvent afficher le contenu et désélectionne `Open Group`.

Sous , **Modèle** vous pouvez sélectionner dans la liste des modèles de groupe de communautés. Ces modèles ont été spécifiés lorsque la fonction de groupes a été incluse dans la structure du site de la communauté ou dans un modèle de site de la communauté.

![group-template](assets/group-template.png)

Sous , **Image** vous pouvez télécharger une image à afficher pour le groupe sur la page Groupes du site de la communauté. La feuille de style par défaut dimensionne l’image à 170 x 90 pixels.

![group-image](assets/group-image.png)

En sélectionnant **Créer un groupe**, les pages du groupe sont créées en fonction du modèle choisi, et un groupe d’utilisateurs est créé pour l’appartenance et la page Groupes est mise à jour afin d’afficher la nouvelle sous-communauté.

Par exemple, la page Groupes avec une nouvelle sous-communauté intitulée &quot;Groupe d’orientation&quot;, pour laquelle une miniature d’image a été téléchargée, apparaît comme suit (toujours connecté en tant qu’administrateur de groupe de communautés) :

![group-page](assets/group-page.png)

En sélectionnant le `Focus Group` Le lien ouvre la page Groupe d’orientation dans le navigateur, qui a une apparence initiale basée sur le modèle sélectionné et comprend un sous-menu sous le menu du site de la communauté principal :

![open-group-page](assets/open-group-page.png)

### Composant de liste de membres de groupe de communautés {#community-group-member-list-component}

La variable `Community Group Member List` est destiné aux développeurs de modèles de groupe.

### Informations supplémentaires {#additional-information}

Vous trouverez plus d’informations sur la [Notions fondamentales sur les groupes de communautés](/help/communities/essentials-groups.md) pour les développeurs.

Pour plus d’informations sur les groupes de communautés, consultez [Gestion des utilisateurs et des groupes d’utilisateurs](/help/communities/users.md).
