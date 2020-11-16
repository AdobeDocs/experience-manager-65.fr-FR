---
title: Console web
seo-title: Console web
description: Apprenez à utiliser le console web d’AEM.
seo-description: Apprenez à utiliser le console web d’AEM.
uuid: 7856b2b3-4216-421d-a315-cd9a55936362
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 4a33fddd-0399-40e4-8687-564fb6765b76
translation-type: tm+mt
source-git-commit: 1f7a45adc73b407c402a51b061632e72d97ca306
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 75%

---


# Console web{#web-console}

Le console web d’AEM est basée sur la [Console de gestion web Apache Felix](https://felix.apache.org/documentation/subprojects/apache-felix-web-console.html). Apache Felix est une initiative communautaire pour mettre en œuvre le plateforme de service OSGi R4 qui comprend la structure et les services standards OSGi.

>[!NOTE]
>
>Sur la console web, toutes les descriptions qui mentionnent les paramètres par défaut sont relatives aux paramètres Sling par défaut.
>
>AEM ayant ses propres paramètres par défaut, ces derniers peuvent être différents de ceux répertoriés dans la console. 

Le console web offre une sélection d’onglets pour le maintien les lots OSGi dont les suivants :

* [Configuration :](#configuration) utilisé pour configurer les lots OSGi, il s’agit donc du mécanisme sous-jacent pour configurer les paramètres du système AEM
* [Lots](#bundles) : utilisé pour installer les lots
* [Composants](#components) : utilisé pour contrôler l’état des composants requis pour AEM

Toutes les modifications apportées sont immédiatement appliquées au système en cours d’exécution. Le redémarrage n’est pas requis.

The console can be accessed from `../system/console`; for example:

`http://localhost:4502/system/console/components`

## Configuration {#configuration}

L’onglet **Configuration** est utilisé pour configurer les lots OSGi. Il s’agit donc du mécanisme sous-jacent pour configurer les paramètres du système AEM.

>[!NOTE]
>
>Pour plus d’informations, voir [Configuration OSGi avec la console web](/help/sites-deploying/configuring-osgi.md).

L’onglet **Configuration** est accessible soit via :

* Le menu déroulant :

   **les lots OSGi >**

* L&#39;URL ; par exemple :

   `http://localhost:4502/system/console/configMgr`

Une liste des configurations s’affiche : 

![screen_shot_2012-02-15at52308pm](assets/screen_shot_2012-02-15at52308pm.png)

Il existe deux types de configurations disponibles à partir des listes déroulantes de cet écran :

* **Configurations** Vous permet de mettre à jour les configurations existantes. Elles ont une identité permanente (PID) et peuvent être :

   * standard et intégrales pa rapport à AEM ; elles sont nécessaires, car si on les supprime, leurs valeurs sont renvoyées aux paramètres par défaut.
   * des instances créées à partir des configurations d’usine ; ces instances sont créées par l’utilisateur. Leur suppression entraîne la suppression de l’instance. 

* **Configurations d’usine** Vous permet de créer une instance de l’objet de la fonctionnalité requise. 

   Elles se verront attribuer une identité permanente, puis seront répertoriées dans les configurations de la liste déroulante.

En sélectionnant une entrée des listes, vous pourrez voir les paramètres associés à cette configuration :

![chlimage_1-21](assets/chlimage_1-21a.png)

Vous pouvez mettre à jour les paramètres selon vos besoins et : 

* **Enregistrer**

   Enregistrez les modifications apportées.

   Pour une configuration d’usine, cela crée une instance avec une identité permanente. La nouvelle instance est ensuite répertoriée sous Configurations. 

* **Réinitialiser**

   Réinitialisez les paramètres affichés à l&#39;écran à ceux enregistrés en dernier.

* **Supprimer**

   Supprimez la configuration actuelle. S’il s’agit d’une configuration standard, les paramètres sont renvoyés aux paramètres par défaut. Si elle a été créée à partir d’une configuration d’usine, l’instance spécifiée est supprimée.

* **Annuler**

   Déliez la configuration actuelle du lot.

* **Annuler**

   Annule les modifications en cours.

## Lots {#bundles}

The **Bundles** tab is the mechanism for installing the OSGi bundles required for AEM. Cet onglet est accessible via l’une des méthodes suivantes : 

* Le menu déroulant :

   **les lots OSGi >**

* L&#39;URL ; par exemple :

   `http://localhost:4502/system/console/bundles`

Une liste de lots s’affiche :

![screen_shot_2012-02-15at44740pm](assets/screen_shot_2012-02-15at44740pm.png)

En utilisant cet onglet vous pouvez :

* **Installation ou mise à jour**

   You can **Browse** to find the file containing your bundle and specify whether it should **Start** immediately and at which **Start Level**.

* **Recharger**

   Actualise la liste affichée.

* **Actualiser les packages**

   Ceci vérifiera les références de tous les paquets et actualisera si nécessaire.

   Par exemple, après une mise à jour, l’ancienne et la nouvelle version peuvent toujours être exécutées en raison de références antérieures. Cette option permettra de vérifier et de déplacer toutes les références vers la nouvelle version, ce qui permettra d’arrêter l’ancienne version.

* **Début**

   Début un lot en fonction du niveau de début spécifié.

* **Arrêter**

   Arrête le lot.

* **Désinstaller**

   Désinstalle le lot du système.

* **voir le statut**

   La liste spécifie l&#39;état actuel de l&#39;offre groupée ; cliquez sur le nom d&#39;un lot spécifique et affichez d&#39;autres informations.

>[!NOTE]
>
>Après la **mise à jour**, il est recommandé d’**actualiser les modules**.

## Composants {#components}

The **Components** tab allows you to Enable and/or Disable the various components. Il est accessible soit par :

* Le menu déroulant :

   **Principal >**

* L&#39;URL ; par exemple :

   `http://localhost:4502/system/console/components`

Une liste de composants s’affiche. Plusieurs icônes sont disponibles pour vous permettre d’activer, de désactiver ou (le cas échéant) d’ouvrir les détails de la configuration pour un composant spécifique. 

![screen_shot_2012-02-15at52144pm](assets/screen_shot_2012-02-15at52144pm.png)

En cliquant sur le nom d’un composant spécifique, vous obtenez plus d’informations sur son état. Cela vous permet également d’activer, de désactiver ou de recharger le composant.

![chlimage_1-22](assets/chlimage_1-22a.png)

>[!NOTE]
>
>L’activation ou la désactivation d’un composant n’est effective qu’une fois qu’AEM/CRX est redémarré.
>
>L’état de démarrage est défini dans le descripteur du composant, qui est généré lors du développement et stocké dans le lot lors de la création du lot. 

