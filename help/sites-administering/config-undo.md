---
title: Configuration de la commande Annuler pour la modification des pages
seo-title: Configuring Undo for Page Editing
description: Découvrez comment configurer la commande Annuler pour la modification des pages dans AEM.
seo-description: Learn how to configure Undo support for page editing in AEM.
uuid: e5a49587-a2a6-41d5-b449-f7a8f7e4cee6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 3cc7efc5-bcb2-41c9-b78b-308f6b7a298e
exl-id: 2cf3ac3f-ee17-480d-a32a-c57631502693
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 66%

---

# Configuration de la commande Annuler pour la modification des pages{#configuring-undo-for-page-editing}

Le [service OSGI](/help/sites-deploying/configuring-osgi.md) **Day CQ WCM Undo Configuration** (`com.day.cq.wcm.undo.UndoConfigService`) expose plusieurs propriétés qui contrôlent le comportement des commandes d’annulation et de restauration pour la modification des pages.

## Configuration par défaut {#default-configuration}

Dans une installation standard, les paramètres par défaut sont définis en tant que propriétés sur la `sling:OsgiConfig`node:

`/libs/wcm/core/config.author/com.day.cq.wcm.undo.UndoConfig`

Ce nœud contient les propriétés `cq.wcm.undo.whitelist` et `cq.wcm.undo.blacklist` ; pour les autres propriétés, les valeurs par défaut sont utilisées.

>[!CAUTION]
>
>Vous ne devez ***rien*** modifier dans le chemin `/libs`.
>
>En effet, le contenu de `/libs` est remplacé dès que vous mettez à niveau votre instance (et risque de l’être si vous appliquez un correctif ou un Feature Pack).

## Configuration des commandes d’annulation et de restauration {#configuring-undo-and-redo}

Vous pouvez configurer ces propriétés de service OSGI pour votre propre instance.

>[!NOTE]
>
>Lorsque vous utilisez AEM, plusieurs méthodes permettent de gérer les paramètres de configuration pour ces services. Voir [Configuration d’OSGi](/help/sites-deploying/configuring-osgi.md) pour plus de détails et connaître les pratiques recommandées.

La liste suivante répertorie les propriétés affichées dans la console web, suivies du nom du paramètre OSGi correspondant, ainsi qu’une description et la valeur par défaut (le cas échéant) :

* **Activer**
( 
`cq.wcm.undo.enabled`)

   * **Description** : détermine si les auteurs de page peuvent annuler et rétablir les modifications.
   * **Par défaut**: `Selected`
   * **Type** : `Boolean`

* **Chemin**
( 
`cq.wcm.undo.path`)

   * **Description :** chemin d’accès du référentiel pour conserver les données d’annulation binaires. Lorsque les auteurs modifient les données binaires telles que les images, la version originale des données est conservée ici. Lorsque les modifications apportées aux données binaires sont annulées, ces données d’annulation binaires sont restaurées dans la page.
   * **Par défaut**: `/var/undo`
   * **Type** : `String`

   >[!NOTE]
   >
   >Par défaut, seuls les administrateurs peuvent accéder au `/var/undo` noeud . Les auteurs peuvent effectuer des opérations d’annulation et de restauration sur du contenu binaire uniquement lorsqu’ils sont dotés de droits d’accès aux données d’annulation binaires.

* **Min. validity**
( 
`cq.wcm.undo.validity`)

   * **Description**: Durée minimale pendant laquelle les données d’annulation binaires sont stockées, en heures. Après cette période, les données binaires peuvent être supprimées, pour préserver l’espace disque.
   * **Par défaut**: `10`
   * **Type** : `Integer`

* **Étapes**
( 
`cq.wcm.undo.steps`)

   * **Description**: Nombre maximal d’actions de page qui sont stockées dans l’historique d’annulation.
   * **Par défaut**: `20`
   * **Type** : `Integer`

* **Persistance**
( 
`cq.wcm.undo.persistence`)

   * **Description**: La classe qui conserve l’historique d’annulation. Deux classes de persistance sont disponibles :

      * `CQ.undo.persistence.WindowNamePersistence` : conserve l’historique à l’aide de la propriété window.name.
      * `CQ.undo.persistence.CookiePersistance`: Conserve l’historique à l’aide de cookies.
   * **Par défaut**: `CQ.undo.persistence.WindowNamePersistence`
   * **Type** : `String`


* **Mode de persistance**
( 
`cq.wcm.undo.persistence.mode`)

   * **Description**: Détermine le moment où l’historique d’annulation est conservé. Sélectionnez cette option pour conserver un historique d’annulation après chaque modification de page. Désactivez cette option pour conserver uniquement lorsqu’un rechargement de page se produit (par exemple, l’utilisateur accède à une autre page).

        La conservation de l’historique d’annulation utilise les ressources du navigateur web. Si le navigateur de vos utilisateurs réagit lentement aux modifications de la page, essayez de conserver l’historique d’annulation lors du rechargement de la page.

   * **Par défaut**: `Selected`
   * **Type** : `Boolean`

* **Mode Marqueur**
( 
`cq.wcm.undo.markermode`)

   * **Description**: Indique le repère visuel à utiliser pour indiquer quels paragraphes sont affectés lorsqu’une opération d’annulation ou de rétablissement se produit. Les valeurs suivantes sont valides :

      * Clignotement : l’indicateur de sélection de paragraphe clignote temporairement.
      * Sélection : le paragraphe est sélectionné.
   * **Par défaut**: `flash`
   * **Type** : `String`


* **Bons composants**
( 
`cq.wcm.undo.whitelist`)

   * **Description** : liste des composants qui doivent être affectés par les opérations d’annulation et de restauration. Ajoutez les chemins d’accès de composant à cette liste lorsqu’ils fonctionnent correctement avec les commandes d’annulation/de restauration. Ajoutez un astérisque (&amp;ast;) pour spécifier un groupe de composants :

      * La valeur suivante spécifie le composant de texte de base :

         `foundation/components/text`

      * La valeur suivante spécifie tous les composants de base :

         `foundation/components/*`
   * Lorsqu’une commande d’annulation ou de restauration est émise sur un composant qui ne figure pas dans cette liste, un message s’affiche indiquant que la commande peut s’avérer non fiable.

   * **Par défaut**: La propriété est remplie avec de nombreux composants fournis par AEM.
   * **Type** : `String[]`


* **Composants incorrects**
( 
`cq.wcm.undo.blacklist`)

   * **Description**: Liste des composants et/ou des opérations de composant que vous ne souhaitez pas voir affectés par la commande d’annulation. Ajoutez les composants et les opérations de composant qui ne fonctionnent pas correctement avec la commande d’annulation :

      * Ajoutez un chemin d’accès de composant lorsque vous ne souhaitez aucune des opérations du composant dans l’historique d’annulation ; par exemple, `collab/forum/components/post`
      * Ajoutez un deux-points (:) et une opération au chemin d’accès lorsque vous souhaitez que cette opération spécifique soit omise de l’historique d’annulation (les autres opérations fonctionnent correctement). `collab/forum/components/post:insertParagraph.`

   >[!NOTE]
   >
   >Lorsqu’une opération figure dans cette liste, elle est toujours ajoutée à l’historique d’annulation. Les utilisateurs ne peuvent pas annuler des opérations qui existent antérieurement à une opération **Bad Component** dans l’historique d’annulation.

   * Les noms d’opération standard sont les suivants :

      * `insertParagraph` : le composant est ajouté à la page.
      * `removeParagraph`: Le composant est supprimé.
      * `moveParagraph` : ’e paragraphe est déplacé vers un autre emplacement.
      * `updateParagraph` : les propriétés du paragraphe sont modifiées.
   * **Valeur par défaut** : la propriété est renseignée avec plusieurs opérations de composant.
   * **Type** : `String[]`
