---
title: Configuration de la commande Annuler pour la modification des pages
seo-title: Configuration de la commande Annuler pour la modification des pages
description: Découvrez comment configurer la commande Annuler pour la modification des pages dans AEM.
seo-description: Découvrez comment configurer la commande Annuler pour la modification des pages dans AEM.
uuid: e5a49587-a2a6-41d5-b449-f7a8f7e4cee6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 3cc7efc5-bcb2-41c9-b78b-308f6b7a298e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 66%

---


# Configuration de la commande Annuler pour la modification des pages{#configuring-undo-for-page-editing}

Le [service OSGI](/help/sites-deploying/configuring-osgi.md) **Day CQ WCM Undo Configuration** (`com.day.cq.wcm.undo.UndoConfigService`) expose plusieurs propriétés qui contrôlent le comportement des commandes d’annulation et de restauration pour la modification des pages.

## Configuration par défaut {#default-configuration}

In a standard installation the default settings are defined as properties on the `sling:OsgiConfig`node:

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

Les listes suivantes indiquent les propriétés affichées dans la console Web, suivies du nom du paramètre OSGi correspondant, ainsi que d’une description et de la valeur par défaut (le cas échéant) :

* **Activer**
( 
`cq.wcm.undo.enabled`)

   * **Description** : détermine si les auteurs de page peuvent annuler et rétablir les modifications.
   * **Par défaut**: `Selected`
   * **Type** : `Boolean`

* **Chemin**
( 
`cq.wcm.undo.path`)

   * **Description :** chemin d’accès du référentiel pour conserver les données d’annulation binaires. Lorsque les auteurs modifient les données binaires telles que les images, la version originale des données est conservée ici. Lorsque les modifications apportées aux données binaires sont annulées, ces données d’annulation binaires sont restaurées sur la page.
   * **Par défaut**: `/var/undo`
   * **Type** : `String`

   >[!NOTE]
   >
   >By default, only administrators can access the `/var/undo` node. Les auteurs peuvent effectuer des opérations d’annulation et de restauration sur du contenu binaire uniquement lorsqu’ils sont dotés de droits d’accès aux données d’annulation binaires.

* **Min. validity**
( 
`cq.wcm.undo.validity`)

   * **Description**: durée minimale de stockage des données d’annulation binaires, en heures. Après cette période, les données binaires peuvent être supprimées, pour préserver l’espace disque.
   * **Par défaut**: `10`
   * **Type** : `Integer`

* **Étapes**
( 
`cq.wcm.undo.steps`)

   * **Description**: Nombre maximal d’actions de page stockées dans l’historique des annulations.
   * **Par défaut**: `20`
   * **Type** : `Integer`

* **Persistance**
( 
`cq.wcm.undo.persistence`)

   * **Description**: La classe qui persiste annule l&#39;historique. Deux classes de persistance sont disponibles :

      * `CQ.undo.persistence.WindowNamePersistence` : conserve l’historique à l’aide de la propriété window.name.
      * `CQ.undo.persistence.CookiePersistance`: Persiste l’historique à l’aide de cookies.
   * **Par défaut**: `CQ.undo.persistence.WindowNamePersistence`
   * **Type** : `String`


* **Mode** de persistance( 
`cq.wcm.undo.persistence.mode`)

   * **Description**: Détermine à quel moment l’historique des annulations est conservé. Sélectionnez cette option pour conserver un historique d’annulation après chaque modification de page. Désactivez cette option pour conserver uniquement lorsqu’un rechargement de page se produit (par exemple, l’utilisateur accède à une autre page).

        La conservation de l’historique d’annulation utilise les ressources du navigateur web. Si le navigateur de vos utilisateurs réagit lentement aux modifications de la page, essayez de conserver l’historique d’annulation lors du rechargement de la page.

   * **Par défaut**: `Selected`
   * **Type** : `Boolean`

* **Mode** Marque( 
`cq.wcm.undo.markermode`)

   * **Description**: Indique le repère visuel à utiliser pour indiquer quels paragraphes sont affectés lors d’une annulation ou d’un rétablissement. Les valeurs suivantes sont valides :

      * Clignotement : l’indicateur de sélection de paragraphe clignote temporairement.
      * Sélection : le paragraphe est sélectionné.
   * **Par défaut**: `flash`
   * **Type** : `String`


* **Bons composants**( 
`cq.wcm.undo.whitelist`)

   * **Description** : liste des composants qui doivent être affectés par les opérations d’annulation et de restauration. Ajoutez les chemins d’accès de composant à cette liste lorsqu’ils fonctionnent correctement avec les commandes d’annulation/de restauration. Ajoutez un astérisque (&amp;ast;) pour spécifier un groupe de composants :

      * La valeur suivante spécifie le composant de texte de base :

         `foundation/components/text`

      * La valeur suivante spécifie tous les composants de base :

         `foundation/components/*`
   * Lorsqu’une commande d’annulation ou de restauration est émise sur un composant qui ne figure pas dans cette liste, un message s’affiche indiquant que la commande peut s’avérer non fiable.

   * **Par défaut**: La propriété est renseignée avec de nombreux composants que AEM fournit.
   * **Type** : `String[]`


* **Composants** incorrects( 
`cq.wcm.undo.blacklist`)

   * **Description**: Liste de composants et/ou d&#39;opérations de composants que vous ne souhaitez pas voir affectés par la commande Annuler. Ajoutez les composants et les opérations de composant qui ne fonctionnent pas correctement avec la commande d’annulation :

      * Ajoutez un chemin d’accès de composant lorsque vous ne souhaitez aucune des opérations du composant dans l’historique d’annulation ; par exemple, `collab/forum/components/post`
      * Append a colon (:) and an operation to the path when you want that specific operation to be omitted from the undo history (other operations function correctly), for example `collab/forum/components/post:insertParagraph.`

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




