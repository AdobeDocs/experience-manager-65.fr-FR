---
title: Création de groupes imbriqués
seo-title: Création de groupes imbriqués
description: Création de groupes imbriqués
seo-description: Création de groupes imbriqués
uuid: b377dc1b-bbb6-41c9-b0fc-8281e1410685
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 752235d2-21ac-46d2-82ed-5fec09c645e9
docset: aem65
translation-type: tm+mt
source-git-commit: 22e853ecaf2696c7329a81bb9d375b1dbc74452c

---


# Création de groupes imbriqués{#authoring-nested-groups}

## Création de groupes sur l’auteur {#creating-groups-on-author}

Sur l’instance d’auteur AEM, à partir de la navigation globale :

* Sélectionnez **[!UICONTROL Communautés] > **[!UICONTROL Sites]**.
* Sélectionnez **[!UICONTROL engager le dossier]** pour l’ouvrir.
* Sélectionnez la carte du site **[!UICONTROL de didacticiel]** anglais de mise en route.

   * Sélectionnez l’image de la carte.
   * Ne *sélectionnez pas* d’icône.

Le résultat est d’accéder à la console [](/help/communities/groups.md)Groupes :

![chlimage_1-91](assets/chlimage_1-91.png)

La fonction groups s’affiche sous la forme d’un dossier dans lequel des instances de groupes sont créées. Sélectionnez le dossier Groupes pour l’ouvrir. Le groupe créé lors de la publication est visible.

![chlimage_1-92](assets/chlimage_1-92.png)

## Créer un groupe d&#39;arts principaux {#create-main-arts-group}

Ce groupe peut être créé, car la structure du site pour engager inclut une fonction de groupes. La configuration de la fonction dans le site permet `Reference Template` par défaut la sélection de tout modèle de groupe activé. Ainsi, le modèle choisi pour ce nouveau groupe est le `Reference Group`.

Ces consoles sont similaires à la console Sites des communautés.

* Sélectionnez **[!UICONTROL Créer un groupe]**.

* **Modèle de groupe de communautés**:

   * **[!UICONTROL Titre]** du groupe de la communauté : Arts.
   * **[!UICONTROL Groupe de communautés Description]**: Groupe parent pour divers groupes artistiques.
   * **[!UICONTROL Racine]** du groupe de communautés : *laisser comme valeur par défaut*.
   * **[!UICONTROL Langue(s)]** de groupe(s) communautaire(s) disponible(s) supplémentaire(s) : utilisez le menu déroulant pour sélectionner la ou les langues des groupes communautaires disponibles. Le menu affiche toutes les langues dans lesquelles le site de la communauté parent est créé. Les utilisateurs peuvent sélectionner l’une de ces langues pour créer des groupes dans plusieurs paramètres régionaux au cours de cette seule étape. Un même groupe est créé dans plusieurs langues spécifiées dans la console Groupes des sites de communauté respectifs.
   * **[!UICONTROL Nom]** du groupe de la communauté : art.
   * **[!UICONTROL Modèle]**: déposer pour sélectionner `Reference Group.`
   * Sélectionnez **[!UICONTROL Suivant]**.

![Groupes de communautés imbriqués](assets/parent-to-nestedgroup.png)

Passez ensuite aux autres panneaux avec les paramètres suivants :

* **[!UICONTROL Concevoir]**

   * Modifiez la conception ou autorisez la conception du site parent par défaut.
   * Sélectionnez **[!UICONTROL Suivant]**.

* **[!UICONTROL Paramètres]**

   * **[!UICONTROL Modération]**

      * Laissez vide (hériter du site parent).
   * **[!UICONTROL Abonnement]**

      * Use default `Optional Membership.`

      * **[!UICONTROL Miniature]**
         * `optional.*`
      * **[!UICONTROL Sélectionnez Suivant]**.



* Sélectionnez **[!UICONTROL Créer]**.

### Groupes imbriqués dans le groupe Arts {#nesting-groups-within-arts-group}

Le `groups` dossier contient désormais deux groupes (actualisez la page).

![Imbrication des groupes](assets/create-community-group.png)

#### Publier le groupe {#publish-group}

Avant de créer des groupes imbriqués dans le `arts` groupe, passez la souris sur la `arts` carte et sélectionnez l’icône de publication pour la publier.

![chlimage_1-93](assets/chlimage_1-93.png)

Attendez la confirmation de la publication du groupe.

![chlimage_1-94](assets/chlimage_1-94.png)

Le `arts` groupe doit également contenir un `groups` dossier, mais vide et dans lequel de nouveaux groupes peuvent être créés. Accédez au dossier du groupe artistique et créez 3 groupes imbriqués, chacun avec un paramètre d’adhésion différent :

1. **[!UICONTROL Visuel]**

   * Titre: `Visual Arts`
   * Nom: `visual`
   * Modèle: `Reference Group`
   * Adhésion : select `Optional Membership`, groupe public, ouvert à tous les membres.

1. **[!UICONTROL Auditoire]**

   * Titre: `Auditory Arts`
   * Nom: `auditory`
   * Modèle: `Reference Group`
   * Adhésion : select `Required Membership`, un groupe ouvert, accessible aux membres.

1. **[!UICONTROL Historique]**

   * Titre: `Art History`
   * Nom: `history`
   * Modèle: `Reference Group`
   * Adhésion : select `Restricted Membership`, groupe secret, visible uniquement pour les membres invités. Par exemple, invitez l’utilisateur [de](/help/communities/tutorials.md#demo-users) démonstration `emily.andrews@mailinator.com`.

Actualisez la page pour afficher les trois groupes imbriqués (sous-communautés).

Pour accéder aux groupes imbriqués à partir de la console Sites des communautés :

* Sélectionner le dossier **[!UICONTROL d’engagement]**
* Sélectionner la carte **[!UICONTROL Didacticiel de prise en main]**
* Sélectionner le dossier **[!UICONTROL Groupes]**
* Sélectionner une carte **[!UICONTROL artistique]**
* Sélectionner le dossier **[!UICONTROL Groupes]**

![chlimage_1-95](assets/chlimage_1-95.png)

## Publication de groupes {#publishing-groups}

![chlimage_1-96](assets/chlimage_1-96.png)

Après avoir publié le site de la communauté principale :

* Publiez chaque groupe individuellement :

   * En attente de confirmation de la publication du groupe.

* Publiez le groupe parent avant de publier les groupes imbriqués dans :

   * Tous les groupes doivent être publiés de manière descendante.

![chlimage_1-97](assets/chlimage_1-97.png)

## Expérience sur la publication {#experience-on-publish}

Il est possible d’expérimenter les différents groupes lorsqu’ils sont connectés, par exemple avec les utilisateurs [de](/help/communities/tutorials.md#demo-users) démonstration utilisés pour :

* Membre du groupe Art/Historique : emily.andrews@mailinator.com/password
   * Le groupe restreint (secret), arts/histoire, est visible :
   * Peut afficher les groupes facultatifs (publics).
   * Peut rejoindre des groupes restreints (ouverts).

* Gestionnaire de groupe : aaron.mcdonald@mailinator.com/password

   * Peut afficher les groupes facultatifs (publics).
   * Peut rejoindre des groupes restreints (ouverts).
   * Impossible d&#39;afficher les groupes restreints (secrets).

Accédez aux consoles [Membres et Groupes des communautés](/help/communities/members.md) sur l’auteur pour ajouter d’autres utilisateurs aux différents groupes de membres qui correspondent aux groupes de la communauté.

