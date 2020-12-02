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
source-git-commit: 6337a57ea12f1e026f6c754a083307ce018a1c13
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 42%

---


# Groupes communautaires {#community-groups}

La fonction des groupes communautaires permet à une sous-communauté d’être créée dynamiquement dans un site communautaire par des utilisateurs autorisés (membres de la communauté et auteurs) à partir des environnements de publication et d’auteur.

Cette capacité est présente lorsque la fonction [groupes ](/help/communities/functions.md#groups-function) est présente dans la structure [site communautaire](/help/communities/sites-console.md).

Un [modèle de groupe de communauté](/help/communities/tools-groups.md) fournit la conception de la page de groupe de communauté lorsqu’un groupe de communauté est créé de manière dynamique.

Un ou plusieurs modèles de groupe sont sélectionnés pour la fonction de groupes lorsque la fonction est ajoutée à la structure d’un site de communauté ou à un modèle de site de communauté. Cette liste de modèles de groupe est présentée au membre ou à l’auteur qui crée dynamiquement un nouveau groupe sur le site de la communauté.

## Création d’un nouveau groupe {#creating-a-new-group}

La possibilité de créer un nouveau groupe communautaire repose sur l&#39;existence d&#39;un site communautaire qui inclut la fonction de groupes, tel que celui créé à partir du [Modèle de site de référence](/help/communities/sites.md).

Les exemples suivants utilisent le site communautaire créé à partir du `Reference Site Template` comme décrit dans le didacticiel [Prise en main de AEM Communities](/help/communities/getting-started.md).

Page chargée lors de la publication lorsque l&#39;option de menu **Groupes** est sélectionnée :

![nouveau groupe](assets/new-group.png)

Lorsque vous sélectionnez l’icône **Nouveau groupe**, une boîte de dialogue de modification s’ouvre.

Dans l’onglet **Paramètres**, spécifiez les fonctionnalités de base du groupe :

![group-settings](assets/group-settings.png)

* **Nom du groupe**

   Titre du groupe à afficher sur le site de la communauté.

* **Description**

   Une description du groupe à afficher sur le site de la communauté.

* **Invitation**

   Liste de membres à inviter à rejoindre le groupe. La recherche par saisie anticipée suggère des membres de la communauté à inviter.

* **Nom de l’URL de groupe**

   Nom de la page de groupe qui devient partie intégrante de l’URL.

* **Ouvrir un groupe**

   La sélection de `Open Group` indique que tout visiteur de site anonyme peut vue le contenu et désélectionner `Member Only Group`.

* **Groupe de membres uniquement**

   La sélection de `Member Only Group` indique que seuls les membres du groupe peuvent vue le contenu et désélectionne `Open Group`.

Sous l&#39;onglet **Modèle**, vous pouvez
sélectionnez parmi la liste des modèles de groupes de la communauté qui ont été spécifiés lorsque la fonction de groupes a été incluse dans la structure du site de la communauté ou dans un modèle de site de la communauté.

![group-template](assets/group-template.png)

L’onglet **Image** permet de transférer une image à afficher pour le groupe sur la page Groupes du site de la communauté. La feuille de style par défaut dimensionne l’image à 170 x 90 pixels.

![group-image](assets/group-image.png)

Lorsque le bouton **Créer un groupe** est sélectionné, les pages du groupe sont créées selon le modèle sélectionné, un groupe d’utilisateurs est créé pour l’abonnement et la page Groupes est mise à jour pour afficher la nouvelle sous-communauté.

Par exemple, la page Groupes comportant une nouvelle sous-communauté nommée « Groupe d’orientation », pour laquelle une miniature a été transférée, a l’apparence suivante (l’utilisateur étant encore connecté en tant qu’administrateur de groupe de communautés) :

![page de groupe](assets/group-page.png)

La sélection du lien `Focus Group` permet d&#39;ouvrir la page Groupe de discussion dans le navigateur, qui présente un aspect initial en fonction du modèle choisi et comprend un sous-menu sous le menu principal du site communautaire :

![open-group-page](assets/open-group-page.png)

### Composant Liste des membres de groupes de communautés {#community-group-member-list-component}

Le composant `Community Group Member List` est destiné aux développeurs de modèles de groupe.

### Informations supplémentaires {#additional-information}

Pour plus d&#39;informations, consultez la page [Community Group Essentials](/help/communities/essentials-groups.md) destinée aux développeurs.

Pour obtenir d&#39;autres informations sur les groupes communautaires, consultez [Gestion des utilisateurs et des groupes d&#39;utilisateurs](/help/communities/users.md).
