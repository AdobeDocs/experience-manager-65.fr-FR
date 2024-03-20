---
title: Configurer la commande Annuler pour la modification des pages
description: Découvrez comment configurer la prise en charge de l’annulation pour la modification de pages dans AEM.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: 2cf3ac3f-ee17-480d-a32a-c57631502693
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 76%

---

# Configurer la commande Annuler pour la modification des pages{#configuring-undo-for-page-editing}

Le [service OSGI](/help/sites-deploying/configuring-osgi.md) de **configuration de l’annulation de la gestion de contenu Web Day CQ** (`com.day.cq.wcm.undo.UndoConfigService`) expose plusieurs propriétés qui contrôlent le comportement des commandes d’annulation et de restauration pour la modification des pages.

## Configuration par défaut {#default-configuration}

Dans une installation standard, les paramètres par défaut sont définis en tant que propriétés sur le nœud `sling:OsgiConfig` :

`/libs/wcm/core/config.author/com.day.cq.wcm.undo.UndoConfig`

Ce nœud contient les propriétés `cq.wcm.undo.whitelist` et `cq.wcm.undo.blacklist` ; pour les autres propriétés, les valeurs par défaut sont utilisées.

>[!CAUTION]
>
>Vous ne devez ***rien*** modifier dans le chemin `/libs`.
>
>En effet, le contenu de `/libs` est remplacé dès que vous mettez à niveau votre instance (et risque de l’être si vous appliquez un correctif ou un Feature Pack).

## Configuration des options Annuler et Rétablir {#configuring-undo-and-redo}

Vous pouvez configurer ces propriétés de service OSGi pour votre propre instance.

>[!NOTE]
>
>Lorsque vous utilisez AEM, plusieurs méthodes permettent de gérer les paramètres de configuration pour ces services. Consultez la section [Configuration d’OSGi](/help/sites-deploying/configuring-osgi.md) pour plus de détails et connaître les pratiques recommandées.

La liste suivante répertorie les propriétés affichées dans la console Web, suivies du nom du paramètre OSGi correspondant, avec une description et la valeur par défaut (le cas échéant) :

* **Activer**
( `cq.wcm.undo.enabled`)

   * **Description** : détermine si les auteurs de page peuvent annuler et rétablir les modifications.
   * **Valeur par défaut** : `Selected`
   * **Type** : `Boolean`

* **Chemin**
( `cq.wcm.undo.path`)

   * **Description :** chemin d’accès du référentiel pour conserver les données d’annulation binaires. Lorsque les auteurs modifient les données binaires telles que les images, la version originale des données est conservée ici. Lorsque des modifications apportées à des données binaires sont annulées, ces données d’annulation binaires sont restaurées sur la page.
   * **Valeur par défaut** : `/var/undo`
   * **Type** : `String`

  >[!NOTE]
  >
  >Par défaut, seuls les administrateurs peuvent accéder au nœud `/var/undo`. Les auteurs ne peuvent effectuer des opérations d’annulation et de rétablissement sur le contenu binaire qu’après avoir reçu les autorisations d’accès aux données d’annulation binaires.

* **Min. validity**
( `cq.wcm.undo.validity`)

   * **Description** : durée de stockage minimal des données d’annulation binaires, en heures. Après cette période, les données binaires peuvent être supprimées, pour préserver l’espace disque.
   * **Valeur par défaut** : `10`
   * **Type** : `Integer`

* **Étapes**
( `cq.wcm.undo.steps`)

   * **Description** : nombre maximal d’actions de page stockées dans l’historique d’annulation.
   * **Valeur par défaut** : `20`
   * **Type** : `Integer`

* **Persistance**
( `cq.wcm.undo.persistence`)

   * **Description** : classe qui conserve l’historique d’annulation. Deux classes de persistance sont disponibles :

      * `CQ.undo.persistence.WindowNamePersistence` : conserve l’historique à l’aide de la propriété window.name.
      * `CQ.undo.persistence.CookiePersistance` : conserve l’historique à l’aide de cookies.

   * **Valeur par défaut** : `CQ.undo.persistence.WindowNamePersistence`
   * **Type** : `String`

* **Mode de persistance**
( `cq.wcm.undo.persistence.mode`)

   * **Description** : détermine à quel moment l’historique d’annulation est conservé. Sélectionnez cette option pour conserver un historique d’annulation après chaque modification de page. Désactivez cette option pour qu’elle persiste uniquement lorsqu’une page se recharge (par exemple, l’utilisateur accède à une autre page).

     La conservation de l’historique d’annulation utilise les ressources du navigateur Web. Si le navigateur de vos utilisateurs réagit lentement aux modifications de la page, essayez de conserver l’historique d’annulation lors du rechargement de la page.

   * **Valeur par défaut** : `Selected`
   * **Type** : `Boolean`

* **Mode Marqueur**
( `cq.wcm.undo.markermode`)

   * **Description** : spécifie l’indice visuel à utiliser pour indiquer quels paragraphes sont affectés lorsqu’une opération d’annulation ou de restauration se produit. Les valeurs suivantes sont valides :

      * flash : l’indicateur de sélection des paragraphes clignote temporairement.
      * select : le paragraphe est sélectionné.

   * **Valeur par défaut** : `flash`
   * **Type** : `String`

* **Bons composants**
( `cq.wcm.undo.whitelist`)

   * **Description** : liste des composants qui doivent être affectés par les opérations d’annulation et de restauration. Ajoutez les chemins d’accès de composant à cette liste lorsqu’ils fonctionnent correctement avec les commandes d’annulation/de restauration. Ajoutez un astérisque (&amp;ast;) pour spécifier un groupe de composants :

      * La valeur suivante spécifie le composant de texte de base :

        `foundation/components/text`

      * La valeur suivante spécifie tous les composants de base :

        `foundation/components/*`

   * Lorsqu’une commande d’annulation ou de restauration est émise sur un composant qui ne figure pas dans cette liste, un message s’affiche indiquant que la commande peut s’avérer non fiable.

   * **Valeur par défaut** : la propriété est renseignée avec de nombreux composants que fournit AEM.
   * **Type** : `String[]`

* **Composants incorrects**
( `cq.wcm.undo.blacklist`)

   * **Description** : liste des composants et/ou des opérations de composant ne devant pas être affectés par les commandes d’annulation/de restauration. Ajoutez les composants et les opérations de composant qui ne fonctionnent pas correctement avec la commande d’annulation :

      * Ajoutez un chemin d’accès au composant lorsque vous ne souhaitez aucune des opérations du composant dans l’historique d’annulation, par exemple : `collab/forum/components/post`
      * Ajoutez un deux-points (:) et une opération au chemin d’accès lorsque vous souhaitez que cette opération spécifique soit omise de l’historique d’annulation (les autres opérations fonctionnent correctement), par exemple : `collab/forum/components/post:insertParagraph.`

  >[!NOTE]
  >
  >Lorsqu’une opération figure dans cette liste, elle est toujours ajoutée à l’historique d’annulation. Les utilisateurs ne peuvent pas annuler des opérations antérieures à une **Composant incorrect** dans l’historique d’annulation.

   * Les noms d’opération types sont les suivants :

      * `insertParagraph` : le composant est ajouté à la page.
      * `removeParagraph` : le composant est supprimé.
      * `moveParagraph` : le paragraphe est déplacé vers un autre emplacement.
      * `updateParagraph` : les propriétés du paragraphe sont modifiées.

   * **Valeur par défaut** : la propriété est renseignée avec plusieurs opérations de composant.
   * **Type** : `String[]`
