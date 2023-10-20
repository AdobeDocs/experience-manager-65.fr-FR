---
title: Création de groupes imbriqués
description: Découvrez comment créer des groupes imbriqués pour un site de communautés Adobe Experience Manager.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: 55803b7a-9064-4392-9cc2-9f113fa8dc29
source-git-commit: f03d0ab9d0f491441378e16e1590d33651f064b5
workflow-type: tm+mt
source-wordcount: '600'
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

La fonction de groupes s’affiche sous la forme d’un dossier dans lequel des instances de groupes sont créées. Pour l’ouvrir, sélectionnez le dossier Groupes . Le groupe créé lors de la publication est visible.

![create-new-group](assets/create-new-group.png)

## Créer un groupe d’arts principal {#create-main-arts-group}

Ce groupe peut être créé car la structure du site pour l’engagement inclut la fonction d’un groupe. Configuration de la fonction dans le `Reference Template` autorise par défaut la sélection de tout modèle de groupe activé. Ainsi, le modèle choisi pour ce nouveau groupe est le `Reference Group`.

Ces consoles sont similaires à la console Sites des communautés .

* Sélectionner **[!UICONTROL Créer un groupe]**

* **Modèle de groupe de communautés**:

   * **[!UICONTROL Titre du groupe de communautés]**: Arts
   * **[!UICONTROL Description du groupe de communautés]**: groupe parent pour divers groupes d’arts
   * **[!UICONTROL Racine du groupe de communautés]**: *leave comme valeur par défaut*
   * **[!UICONTROL Langue(s) de groupe de communautés disponible(s) supplémentaire(s)]**: utilisez le menu déroulant pour sélectionner les langues de groupe de communautés disponibles. Le menu affiche toutes les langues dans lesquelles le site de la communauté parent est créé. Les utilisateurs peuvent sélectionner l’une de ces langues pour créer des groupes dans plusieurs paramètres régionaux au cours de cette seule étape. Le même groupe est créé dans plusieurs langues spécifiées dans la console Groupes des sites de communauté respectifs.
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

La variable `groups` contient désormais deux groupes (actualisez la page).

![Imbrication des groupes](assets/create-community-group.png)

#### Publier le groupe {#publish-group}

Avant de créer des groupes imbriqués dans `arts` , survolez le groupe avec la souris. `arts` et sélectionnez l’icône de publication pour la publier.

![publish-site](assets/publish-site.png)

Attendez la confirmation de la publication du groupe.

![group-publish](assets/group-published.png)

La variable `arts` Le groupe doit également contenir un `groups` , mais vide et dans lequel de nouveaux groupes peuvent être créés. Accédez au dossier du groupe d’arts et créez trois groupes imbriqués, chacun avec un paramètre d’adhésion différent :

1. **[!UICONTROL Visuel]**

   * Titre : `Visual Arts`
   * Nom : `visual`
   * Modèle: `Reference Group`
   * Adhésion : sélectionnez `Optional Membership`, un groupe public, ouvert à tous les membres.

1. **[!UICONTROL Auditoire]**

   * Titre : `Auditory Arts`
   * Nom : `auditory`
   * Modèle: `Reference Group`
   * Adhésion : sélectionnez `Required Membership`, un groupe ouvert, accessible aux membres.

1. **[!UICONTROL Historique]**

   * Titre : `Art History`
   * Nom : `history`
   * Modèle: `Reference Group`
   * Adhésion : sélectionnez `Restricted Membership`, un groupe secret, visible uniquement pour les membres invités. Par exemple, invitez [utilisateur de démonstration](/help/communities/tutorials.md#demo-users) `emily.andrews@mailinator.com`.

Actualisez la page afin de voir les trois groupes imbriqués (sous-communautés).

Pour accéder aux groupes imbriqués à partir de la console Sites de communautés :

* Sélectionnez la variable **[!UICONTROL dossier d’engagement]**
* Sélectionner **[!UICONTROL Carte du tutoriel Prise en main]**
* Sélectionnez la variable **[!UICONTROL Groupes]** folder
* Sélectionner **[!UICONTROL carte arts]**
* Sélectionnez la variable **[!UICONTROL Groupes]** folder

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

* Membre du groupe Art/Historique : `emily.andrews@mailinator.com/password`
   * Le groupe restreint (secret), arts/histoire, est visible :
   * Possibilité d’afficher les groupes facultatifs (publics).
   * Peut rejoindre des groupes restreints (ouverts).

* Gestionnaire de groupe : `aaron.mcdonald@mailinator.com/password`

   * Possibilité d’afficher les groupes facultatifs (publics).
   * Peut rejoindre des groupes restreints (ouverts).
   * Impossible d’afficher les groupes restreints (secrets).

Accès aux communautés [Consoles Membres et Groupes](/help/communities/members.md) sur l’auteur pour ajouter d’autres utilisateurs à différents groupes de membres qui correspondent aux groupes de la communauté.
