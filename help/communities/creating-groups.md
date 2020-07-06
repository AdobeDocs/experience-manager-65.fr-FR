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
translation-type: tm+mt
source-git-commit: 43663703a79b95ccdb83eb9b5730143bde101305
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 43%

---


# Groupes communautaires {#community-groups}

La fonction des groupes communautaires permet à une sous-communauté d’être créée dynamiquement dans un site communautaire par des utilisateurs autorisés (membres de la communauté et auteurs) à partir des environnements de publication et d’auteur.

This ability is present when the [groups function](/help/communities/functions.md#groups-function) is present in the [community site](/help/communities/sites-console.md) structure.

A [community group template](/help/communities/tools-groups.md) provides the design of the community group page when a community group is dynamically created.

Un ou plusieurs modèles de groupe sont sélectionnés pour la fonction de groupes lorsque la fonction est ajoutée à la structure d’un site de communauté ou à un modèle de site de communauté. Cette liste de modèles de groupe est présentée au membre ou à l’auteur qui crée dynamiquement un nouveau groupe sur le site de la communauté.

## Création d’un nouveau groupe {#creating-a-new-group}

The ability to create a new community group relies on the existence of a community site which includes the groups function, such as one created from the [Reference Site Template](/help/communities/sites.md).

The examples that follow use the community site created from the `Reference Site Template` as described in the [Getting Started with AEM Communities](/help/communities/getting-started.md) tutorial.

This is the page that loads on publish when the **Groups** menu item is selected:

![chlimage_1-236](assets/chlimage_1-236.png)

Lorsque vous sélectionnez l’icône **Nouveau groupe**, une boîte de dialogue de modification s’ouvre.

Dans l’onglet **Paramètres**, spécifiez les fonctionnalités de base du groupe :

![chlimage_1-237](assets/chlimage_1-237.png)

* **Nom du groupe**

   Titre du groupe à afficher sur le site de la communauté.

* **Description**

   Une description du groupe à afficher sur le site de la communauté.

* **Invitation**

   liste de membres à inviter à rejoindre le groupe. La recherche par saisie anticipée suggère des membres de la communauté à inviter.

* **Nom de l’URL de groupe**

   Nom de la page de groupe qui devient partie intégrante de l’URL.

* **Ouvrir un groupe**

   La sélection `Open Group` indique que tout visiteur de site anonyme peut vue le contenu et désélectionner `Member Only Group`.

* **Groupe de membres uniquement**

   La sélection `Member Only Group` indique que seuls les membres du groupe peuvent vue le contenu et désélectionne `Open Group`.

Under the **Template** tab is the ability to
select from the list of community group templates that were specified when the groups function was included in the community site&#39;s structure or in a community site template.

![chlimage_1-238](assets/chlimage_1-238.png)

L’onglet **Image** permet de transférer une image à afficher pour le groupe sur la page Groupes du site de la communauté. La feuille de style par défaut dimensionne l’image à 170 x 90 pixels.

![chlimage_1-239](assets/chlimage_1-239.png)

Lorsque le bouton **Créer un groupe** est sélectionné, les pages du groupe sont créées selon le modèle sélectionné, un groupe d’utilisateurs est créé pour l’abonnement et la page Groupes est mise à jour pour afficher la nouvelle sous-communauté.

Par exemple, la page Groupes comportant une nouvelle sous-communauté nommée « Groupe d’orientation », pour laquelle une miniature a été transférée, a l’apparence suivante (l’utilisateur étant encore connecté en tant qu’administrateur de groupe de communautés) :

![chlimage_1-240](assets/chlimage_1-240.png)

Selecting the `Focus Group` link will open the Focus Group page in the browser, which has an initial appearance based on the chosen template, and includes a submenu underneath the main community site&#39;s menu:

![chlimage_1-241](assets/chlimage_1-241.png)

### Composant Liste des membres de groupes de communautés {#community-group-member-list-component}

Le `Community Group Member List` composant est destiné aux développeurs de modèles de groupe.

### Informations supplémentaires {#additional-information}

More information may be found on the [Community Group Essentials](/help/communities/essentials-groups.md) page for developers.

For other information related to community groups, visit [Managing Users and User Groups](/help/communities/users.md).
