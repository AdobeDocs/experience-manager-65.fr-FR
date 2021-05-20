---
title: Groupes communautaires
seo-title: Groupes communautaires
description: Création de groupes communautaires
seo-description: Création de groupes communautaires
uuid: c677d23d-5edb-414c-9013-130c88c2ea52
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: d94708ee-ca6b-420c-9536-6889d752f9de
docset: aem65
exl-id: edcda6cb-df47-4afe-8a9a-82d8e386fe05
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 42%

---

# Groupes communautaires {#community-groups}

La fonctionnalité de groupes de communautés permet à une sous-communauté d’être créée dynamiquement dans un site de communauté par des utilisateurs autorisés (membres de la communauté et auteurs) à partir des environnements de publication et de création.

Cette fonctionnalité est présente lorsque la fonction [groups](/help/communities/functions.md#groups-function) est présente dans la structure [site communautaire](/help/communities/sites-console.md).

Un [modèle de groupe de communautés](/help/communities/tools-groups.md) fournit la conception de la page de groupe de communautés lorsqu’un groupe de communautés est créé dynamiquement.

Un ou plusieurs modèles de groupe sont sélectionnés pour la fonction de groupes lorsque la fonction est ajoutée à la structure d’un site de communauté ou à un modèle de site de communauté. Cette liste de modèles de groupe est présentée au membre ou à l’auteur qui crée dynamiquement un nouveau groupe sur le site de la communauté.

## Création d’un nouveau groupe {#creating-a-new-group}

La possibilité de créer un groupe de communautés dépend de l’existence d’un site de communauté qui inclut la fonction de groupes, comme un site créé à partir du [modèle de site de référence](/help/communities/sites.md).

Les exemples qui suivent utilisent le site de la communauté créé à partir de `Reference Site Template` comme décrit dans le tutoriel [Prise en main d’AEM Communities](/help/communities/getting-started.md) .

Il s’agit de la page qui se charge lors de la publication lorsque l’option de menu **Groupes** est sélectionnée :

![new-group](assets/new-group.png)

Lorsque vous sélectionnez l’icône **Nouveau groupe**, une boîte de dialogue de modification s’ouvre.

Dans l’onglet **Paramètres**, spécifiez les fonctionnalités de base du groupe :

![group-settings](assets/group-settings.png)

* **Nom du groupe**

   Titre du groupe à afficher sur le site de la communauté.

* **Description**

   Une description du groupe à afficher sur le site de la communauté.

* **Invitation**

   Liste des membres à inviter à rejoindre le groupe. La recherche par saisie anticipée suggère des membres de la communauté à inviter.

* **Nom de l’URL de groupe**

   Nom de la page de groupe qui devient une partie de l’URL.

* **Ouvrir un groupe**

   La sélection de `Open Group` indique que tout visiteur anonyme du site peut afficher le contenu et désélectionner `Member Only Group`.

* **Groupe de membres uniquement**

   La sélection de `Member Only Group` indique que seuls les membres du groupe peuvent afficher le contenu et désélectionne `Open Group`.

Sous l’onglet **Modèle** se trouve la possibilité de
sélectionnez dans la liste des modèles de groupe de communautés qui ont été spécifiés lorsque la fonction de groupes a été incluse dans la structure du site de la communauté ou dans un modèle de site de communauté.

![group-template](assets/group-template.png)

L’onglet **Image** permet de transférer une image à afficher pour le groupe sur la page Groupes du site de la communauté. La feuille de style par défaut dimensionne l’image à 170 x 90 pixels.

![group-image](assets/group-image.png)

Lorsque le bouton **Créer un groupe** est sélectionné, les pages du groupe sont créées selon le modèle sélectionné, un groupe d’utilisateurs est créé pour l’abonnement et la page Groupes est mise à jour pour afficher la nouvelle sous-communauté.

Par exemple, la page Groupes comportant une nouvelle sous-communauté nommée « Groupe d’orientation », pour laquelle une miniature a été transférée, a l’apparence suivante (l’utilisateur étant encore connecté en tant qu’administrateur de groupe de communautés) :

![group-page](assets/group-page.png)

Si vous sélectionnez le lien `Focus Group`, la page Groupe d’orientation s’ouvre dans le navigateur. Celui-ci a une apparence initiale basée sur le modèle sélectionné et comprend un sous-menu sous le menu du site de la communauté principale :

![open-group-page](assets/open-group-page.png)

### Composant Liste des membres de groupes de communautés {#community-group-member-list-component}

Le composant `Community Group Member List` est destiné aux développeurs de modèles de groupe.

### Informations supplémentaires {#additional-information}

Pour plus d’informations, reportez-vous à la page [Notions fondamentales sur les groupes communautaires](/help/communities/essentials-groups.md) pour les développeurs.

Pour plus d’informations sur les groupes de communautés, voir [Gestion des utilisateurs et des groupes d’utilisateurs](/help/communities/users.md).
