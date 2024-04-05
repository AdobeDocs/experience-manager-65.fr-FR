---
title: Console web dans Adobe Experience Manager
description: Découvrez comment utiliser la console web d’Adobe Experience Manager (AEM).
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
feature: Configuring
exl-id: 9acbf61f-73a8-4998-9421-dd933f30ac8a
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '706'
ht-degree: 100%

---

# Console web{#web-console}

La console web d’AEM est basée sur la [Console de gestion web Apache Felix](https://felix.apache.org/documentation/subprojects/apache-felix-web-console.html). Apache Felix est un travail de la communauté pour mettre en œuvre la plateforme de service OSGi R4, qui inclut le framework OSGi et les services standard.

>[!NOTE]
>
>Dans la console web, toute description qui mentionne les paramètres par défaut est liée aux valeurs par défaut de Sling.
>
>AEM ayant ses propres paramètres par défaut, ces derniers peuvent être différents de ceux répertoriés dans la console.

La console web propose une sélection d’onglets pour la maintenance des lots OSGi, notamment :

* [Configuration](#configuration) : utilisé pour configurer les lots OSGi. Il s’agit donc du mécanisme sous-jacent pour configurer les paramètres système d’AEM
* [Lots](#bundles) : utilisé pour installer des lots
* [Composants](#components) : utilisé pour contrôler le statut des composants requis pour AEM

Toutes les modifications apportées sont immédiatement appliquées au système en cours d’exécution. Aucun redémarrage n’est requis.

Cette console est accessible à partir de `../system/console` ; par exemple :

`http://localhost:4502/system/console/components`

## Configuration {#configuration}

L’onglet **Configuration** est utilisé pour configurer les lots OSGi. Il s’agit donc du mécanisme sous-jacent pour configurer les paramètres système d’AEM.

>[!NOTE]
>
>Voir [Configuration OSGi à l’aide de la console web](/help/sites-deploying/configuring-osgi.md) pour plus de détails.

L’onglet **Configuration** est accessible soit via :

* Le menu déroulant :

  **OSGi >**

* L’URL ; par exemple :

  `http://localhost:4502/system/console/configMgr`

Une liste des configurations s’affiche :

![screen_shot_2012-02-15at52308pm](assets/screen_shot_2012-02-15at52308pm.png)

Il existe deux types de configurations disponibles à partir des listes déroulantes de cet écran :

* **Configurations**
Vous permet de mettre à jour les configurations existantes. Elles possèdent une identité persistante (PID) et peuvent être :

   * standard ou intégrales pour AEM. Elles sont nécessaires ; si elles sont supprimées, les valeurs sont renvoyées aux paramètres par défaut.
   * les instances créées à partir des configurations d’usine ; ces instances sont créées par l’utilisateur ou l’utilisatrice et la suppression supprime l’instance.

* **Configurations d’usine**
Vous permet de créer une instance de l’objet de la fonctionnalité requise.

  Elle se verra attribuer une identité permanente, puis sera répertoriée dans la liste déroulante des configurations.

En sélectionnant une entrée quelconque dans la liste, vous pourrez voir les paramètres associés à cette configuration :

![chlimage_1-21](assets/chlimage_1-21a.png)

Vous pouvez mettre à jour les paramètres selon vos besoins et : 

* **Enregistrer**

  Enregistrez les modifications apportées.

  Pour une configuration d’usine, cela crée une instance avec une identité permanente. La nouvelle instance est ensuite répertoriée sous Configurations.

* **Réinitialiser**

  Réinitialisez les paramètres affichés sur l’écran pour revenir à ceux enregistrés en dernier.

* **Supprimer**

  Supprime la configuration actuelle. Si elle est standard, les paramètres sont renvoyés aux paramètres par défaut. Si elle est créée à partir d’une configuration d’usine, l’instance spécifique est supprimée.

* **Dissocier**

  Dissocie la configuration actuelle du lot.

* **Annuler**

  Annule toutes les modifications actuelles.

## Lots {#bundles}

L’onglet **Lots** correspond au mécanisme permettant d’installer les lots OSGi requis par AEM. Cet onglet est accessible via l’une des méthodes suivantes : 

* Le menu déroulant :

  **OSGi >**

* L’URL ; par exemple :

  `http://localhost:4502/system/console/bundles`

Une liste de lots s’affiche :

![screen_shot_2012-02-15at44740pm](assets/screen_shot_2012-02-15at44740pm.png)

En utilisant cet onglet vous pouvez réaliser les opérations suivantes :

* **Installer ou mettre à jour**

  Vous pouvez utiliser l’option **Parcourir** pour trouver le fichier contenant votre lot et spécifier s’il doit **commencer** immédiatement et à quel **niveau de départ**.

* **Recharger**

  Actualise la liste affichée.

* **Actualiser les packages**

  Cela permet de vérifier les références de tous les packages et de les actualiser au besoin.

  Par exemple, après une mise à jour, l’ancienne et la nouvelle version peuvent toujours être exécutées en raison de références antérieures. Cette option permettra de vérifier et de déplacer toutes les références vers la nouvelle version, afin d’arrêter l’ancienne version.

* **Démarrer**

  Lance un lot en fonction du niveau initial spécifié.

* **Arrêter**

  Arrête le lot.

* **Désinstaller**

  Permet de désinstaller le lot du système.

* **Afficher le statut**

  La liste indique le statut du lot. Cliquez sur le nom d’un lot spécifique pour obtenir des informations supplémentaires.

>[!NOTE]
>
>Après la **mise à jour**, Adobe vous recommande d’effectuer une **actualisation des packages**.

## Composants {#components}

L’onglet **Composants** vous permet d’activer et de désactiver divers composants. Il est accessible par les éléments suivants :

* Le menu déroulant :

  **Principal >**

* L’URL ; par exemple :

  `http://localhost:4502/system/console/components`

Une liste de composants s’affiche. Plusieurs icônes sont disponibles pour vous permettre d’activer, de désactiver ou (le cas échéant) d’ouvrir les détails de la configuration pour un composant spécifique.

![screen_shot_2012-02-15at52144pm](assets/screen_shot_2012-02-15at52144pm.png)

Cliquez sur le nom d’un composant spécifique pour afficher des informations supplémentaires sur son statut. Vous pouvez également activer, désactiver ou recharger le composant.

![chlimage_1-22](assets/chlimage_1-22a.png)

>[!NOTE]
>
>L’activation ou la désactivation d’un composant ne s’applique que jusqu’au redémarrage d’AEM/CRX.
>
>L’état de départ est défini dans le descripteur de composant, qui est généré pendant le développement et stocké dans le lot au moment de la création du lot.
