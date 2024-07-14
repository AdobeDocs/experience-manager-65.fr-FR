---
title: Création de groupes imbriqués
description: Découvrez comment créer des groupes imbriqués pour un site de communautés Adobe Experience Manager.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: 55803b7a-9064-4392-9cc2-9f113fa8dc29
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 2%

---

# Création de groupes imbriqués{#authoring-nested-groups}

## Création de groupes sur l’instance de création {#creating-groups-on-author}

Sur l’instance d’auteur AEM, à partir de la navigation globale :

* Sélectionnez **[!UICONTROL Communautés]** > **[!UICONTROL Sites]**.
* Sélectionnez **[!UICONTROL dossier d&#39;engagement]** pour l&#39;ouvrir.
* Sélectionnez la carte du site anglais **[!UICONTROL Prise en main du tutoriel]**.

   * Sélectionnez l’image de la carte.
   * Ne *pas* sélectionnez une icône.

Le résultat est d’atteindre la [console Groupes](/help/communities/groups.md) :

![create-group](assets/create-group.png)

La fonction de groupes s’affiche sous la forme d’un dossier dans lequel des instances de groupes sont créées. Pour l’ouvrir, sélectionnez le dossier Groupes . Le groupe créé sur Publish est visible.

![create-new-group](assets/create-new-group.png)

## Créer un groupe d’arts principal {#create-main-arts-group}

Ce groupe peut être créé car la structure du site pour l’engagement inclut la fonction d’un groupe. La configuration de la fonction dans le `Reference Template` du site autorise par défaut la sélection de tout modèle de groupe activé. Ainsi, le modèle choisi pour ce nouveau groupe est le `Reference Group`.

Ces consoles sont similaires à la console Sites des communautés .

* Sélectionnez **[!UICONTROL Créer un groupe]**

* **Modèle de groupe de communautés** :

   * **[!UICONTROL Titre du groupe communautaire]** : Arts
   * **[!UICONTROL Groupe de communautés Description]** : groupe parent pour divers groupes d’arts
   * **[!UICONTROL Racine du groupe de communautés]** : *laisser comme valeur par défaut*
   * **[!UICONTROL Langue(s) de groupe de communautés disponible supplémentaire(s)]** : utilisez le menu déroulant pour sélectionner les langues de groupe de communautés disponibles. Le menu affiche toutes les langues dans lesquelles le site de la communauté parent est créé. Les utilisateurs peuvent sélectionner l’une de ces langues pour créer des groupes dans plusieurs paramètres régionaux au cours de cette seule étape. Le même groupe est créé dans plusieurs langues spécifiées dans la console Groupes des sites de communauté respectifs.
   * **[!UICONTROL Nom de groupe de la communauté]** : arts
   * **[!UICONTROL Modèle]** : liste déroulante pour sélectionner `Reference Group`
   * Sélectionnez **[!UICONTROL Suivant]**

![Groupes de communautés imbriqués](assets/parent-to-nestedgroup.png)

Passez aux autres panneaux avec les paramètres suivants :

* **[!UICONTROL Conception]**

   * Modifiez la conception ou autorisez la conception du site parent par défaut.
   * Sélectionnez **[!UICONTROL Suivant]**.

* **[!UICONTROL Paramètres]**

   * **[!UICONTROL Modération]**

      * Laissez vide (hériter du site parent).

   * **[!UICONTROL Adhésion]**

      * Utiliser la valeur par défaut `Optional Membership.`

      * **[!UICONTROL Miniature]**
         * `optional.*`

      * **[!UICONTROL Sélectionnez Suivant]**.

* Sélectionnez **[!UICONTROL Créer]**.

### Imbrication de groupes dans le groupe Arts {#nesting-groups-within-arts-group}

Le dossier `groups` contient désormais deux groupes (actualisez la page).

![Imbrication des groupes](assets/create-community-group.png)

#### Groupe Publish {#publish-group}

Avant de créer des groupes imbriqués dans le groupe `arts`, passez la souris sur la carte `arts` et sélectionnez l’icône de publication pour la publier.

![publish-site](assets/publish-site.png)

Attendez la confirmation de la publication du groupe.

![group-publish](assets/group-published.png)

Le groupe `arts` doit également contenir un dossier `groups`, mais un dossier vide dans lequel de nouveaux groupes peuvent être créés. Accédez au dossier du groupe d’arts et créez trois groupes imbriqués, chacun avec un paramètre d’adhésion différent :

1. **[!UICONTROL Visuel]**

   * Titre : `Visual Arts`
   * Nom : `visual`
   * Modèle : `Reference Group`
   * Adhésion : sélectionnez `Optional Membership`, un groupe public, ouvert à tous les membres.

1. **[!UICONTROL Auditoire]**

   * Titre : `Auditory Arts`
   * Nom : `auditory`
   * Modèle : `Reference Group`
   * Adhésion : sélectionnez `Required Membership`, un groupe ouvert, disponible pour la participation des membres.

1. **[!UICONTROL Historique]**

   * Titre : `Art History`
   * Nom : `history`
   * Modèle : `Reference Group`
   * Adhésion : sélectionnez `Restricted Membership`, un groupe secret, visible uniquement pour les membres invités. Par exemple, invitez [demo user](/help/communities/tutorials.md#demo-users) `emily.andrews@mailinator.com`.

Actualisez la page afin de voir les trois groupes imbriqués (sous-communautés).

Pour accéder aux groupes imbriqués à partir de la console Sites de communautés :

* Sélectionnez le dossier **[!UICONTROL engage]**
* Sélectionnez **[!UICONTROL Carte de didacticiel de prise en main]**
* Sélectionnez le dossier **[!UICONTROL Groups]**
* Sélectionnez **[!UICONTROL arts card]**
* Sélectionnez le dossier **[!UICONTROL Groups]**

![create-new-group2](assets/create-new-group2.png)

## Publication de groupes {#publishing-groups}

![publish-site](assets/publish-site.png)

Après avoir publié le site de la communauté principale :

* Publish individuellement chaque groupe :

   * En attente de confirmation de la publication du groupe.

* Publish le groupe parent avant de publier les groupes imbriqués dans :

   * Tous les groupes doivent être publiés de manière descendante.

![group-publish](assets/group-published.png)

## Expérience sur Publish {#experience-on-publish}

Il est possible d’expérimenter les différents groupes lorsqu’ils sont connectés, par exemple, avec les [utilisateurs de démonstration](/help/communities/tutorials.md#demo-users) utilisés pour :

* Membre du groupe Art/Historique : `emily.andrews@mailinator.com/password`
   * Le groupe restreint (secret), arts/histoire, est visible :
   * Possibilité d’afficher les groupes facultatifs (publics).
   * Peut rejoindre des groupes restreints (ouverts).

* Gestionnaire de groupe : `aaron.mcdonald@mailinator.com/password`

   * Possibilité d’afficher les groupes facultatifs (publics).
   * Peut rejoindre des groupes restreints (ouverts).
   * Impossible d’afficher les groupes restreints (secrets).

Accédez aux [consoles Membres et Groupes](/help/communities/members.md) de Communities sur l’instance de création pour ajouter d’autres utilisateurs à différents groupes de membres qui correspondent aux groupes de communautés.
