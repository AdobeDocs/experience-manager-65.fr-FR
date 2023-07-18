---
title: Création de groupes imbriqués
seo-title: Authoring Nested Groups
description: Création de groupes imbriqués
seo-description: Create nested groups
uuid: b377dc1b-bbb6-41c9-b0fc-8281e1410685
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 752235d2-21ac-46d2-82ed-5fec09c645e9
docset: aem65
exl-id: 55803b7a-9064-4392-9cc2-9f113fa8dc29
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 4%

---

# Création de groupes imbriqués{#authoring-nested-groups}

## Création de groupes sur l’instance de création {#creating-groups-on-author}

Sur l’instance d’auteur AEM, à partir de la navigation globale :

* Sélectionner **[!UICONTROL Communautés]** > **[!UICONTROL Sites]**.
* Sélectionner **[!UICONTROL dossier d’engagement]** pour l’ouvrir.
* Sélectionnez la carte correspondant au **[!UICONTROL Tutoriel de prise en main]** Site en anglais.

   * Sélectionnez l’image de la carte.
   * Do *not* sélectionnez une icône.

Le résultat est d’atteindre la variable [Console Groupes](/help/communities/groups.md):

![create-group](assets/create-group.png)

La fonction de groupes s’affiche sous la forme d’un dossier dans lequel des instances de groupes sont créées. Sélectionnez le dossier Groupes pour l’ouvrir. Le groupe créé lors de la publication est visible.

![create-new-group](assets/create-new-group.png)

## Créer un groupe d’arts principal {#create-main-arts-group}

Ce groupe peut être créé car la structure du site pour la participation inclut une fonction de groupe. Configuration de la fonction dans le `Reference Template` autorise par défaut la sélection de tout modèle de groupe activé. Ainsi, le modèle choisi pour ce nouveau groupe est le `Reference Group`.

Ces consoles sont similaires à la console Sites des communautés .

* Sélectionner **[!UICONTROL Créer un groupe]**

* **Modèle de groupe de communautés**:

   * **[!UICONTROL Titre du groupe de communautés]**: Arts
   * **[!UICONTROL Description du groupe de communautés]**: Un groupe parent pour divers groupes d’arts
   * **[!UICONTROL Racine du groupe de communautés]**: *leave comme valeur par défaut*
   * **[!UICONTROL Langue(s) de groupe de communautés disponible(s) supplémentaire(s)]**: utilisez le menu déroulant pour sélectionner la ou les langues des groupes de communautés disponibles. Le menu affiche toutes les langues dans lesquelles le site de la communauté parent est créé. Les utilisateurs peuvent sélectionner l’une de ces langues pour créer des groupes dans plusieurs paramètres régionaux au cours de cette seule étape. Un même groupe est créé dans plusieurs langues spécifiées dans la console Groupes des sites de communauté respectifs.
   * **[!UICONTROL Nom du groupe de communautés]**: arts
   * **[!UICONTROL Modèle]**: menu déroulant à sélectionner `Reference Group`
   * Sélectionnez **[!UICONTROL Suivant]**

![Groupes de communautés imbriqués](assets/parent-to-nestedgroup.png)

Passez aux autres panneaux avec les paramètres suivants :

* **[!UICONTROL Conception]**

   * Modifiez la conception ou autorisez la conception du site parent par défaut.
   * Sélectionnez **[!UICONTROL Suivant]**.

* **[!UICONTROL Paramètres]**

   * **[!UICONTROL Modération]**

      * Laissez vide (hériter du site parent).

   * **[!UICONTROL Abonnement]**

      * Utiliser la valeur par défaut `Optional Membership.`

      * **[!UICONTROL Miniature]**
         * `optional.*`

      * **[!UICONTROL Sélectionnez Suivant]**.

* Sélectionnez **[!UICONTROL Créer]**.

### Imbrication de groupes dans le groupe Arts {#nesting-groups-within-arts-group}

Le `groups` contient désormais deux groupes (actualisez la page).

![Imbrication des groupes](assets/create-community-group.png)

#### Publier le groupe {#publish-group}

Avant de créer des groupes imbriqués dans `arts` , survolez le groupe avec la souris. `arts` et sélectionnez l’icône de publication pour la publier.

![publish-site](assets/publish-site.png)

Attendez la confirmation de la publication du groupe.

![group-publish](assets/group-published.png)

Le `arts` Le groupe doit également contenir un `groups` , mais vide et dans lequel de nouveaux groupes peuvent être créés. Accédez au dossier du groupe d’arts et créez trois groupes imbriqués, chacun avec un paramètre d’adhésion différent :

1. **[!UICONTROL Visuel]**

   * Titre : `Visual Arts`
   * Nom : `visual`
   * Modèle: `Reference Group`
   * Adhésion : select `Optional Membership`, un groupe public, ouvert à tous les membres.

1. **[!UICONTROL Auditoire]**

   * Titre : `Auditory Arts`
   * Nom : `auditory`
   * Modèle: `Reference Group`
   * Adhésion : select `Required Membership`, un groupe ouvert, accessible aux membres.

1. **[!UICONTROL Historique]**

   * Titre : `Art History`
   * Nom : `history`
   * Modèle: `Reference Group`
   * Adhésion : select `Restricted Membership`, un groupe secret, visible uniquement pour les membres invités. Par exemple, invitez [utilisateur de démonstration](/help/communities/tutorials.md#demo-users) `emily.andrews@mailinator.com`.

Actualisez la page pour afficher les trois groupes imbriqués (sous-communautés).

Pour accéder aux groupes imbriqués à partir de la console Sites de communautés :

* Sélectionner **[!UICONTROL dossier d’engagement]**
* Sélectionner **[!UICONTROL Carte du tutoriel Prise en main]**
* Sélectionner **[!UICONTROL Groupes]** folder
* Sélectionner **[!UICONTROL carte arts]**
* Sélectionner **[!UICONTROL Groupes]** folder

![create-new-group2](assets/create-new-group2.png)

## Publication de groupes {#publishing-groups}

![publish-site](assets/publish-site.png)

Après avoir publié le site de la communauté principale :

* Publiez chaque groupe individuellement :

   * En attente de confirmation de la publication du groupe.

* Publiez le groupe parent avant de publier les groupes imbriqués dans :

   * Tous les groupes doivent être publiés de manière descendante.

![group-publish](assets/group-published.png)

## Expérience sur publication {#experience-on-publish}

Il est possible d’expérimenter les différents groupes lorsqu’ils sont connectés, par exemple avec le [utilisateurs de démonstration](/help/communities/tutorials.md#demo-users) utilisé pour :

* Membre du groupe Art/Historique : emily.andrews@mailinator.com/password
   * Le groupe restreint (secret), arts/histoire, est visible :
   * Peuvent afficher les groupes facultatifs (publics).
   * Peut rejoindre des groupes restreints (ouverts).

* Gestionnaire de groupe : aaron.mcdonald@mailinator.com/password

   * Peuvent afficher les groupes facultatifs (publics).
   * Peut rejoindre des groupes restreints (ouverts).
   * Impossible de voir les groupes restreints (secrets).

Accès aux communautés [Consoles Membres et Groupes](/help/communities/members.md) sur l’auteur pour ajouter d’autres utilisateurs à différents groupes de membres qui correspondent aux groupes de la communauté.
