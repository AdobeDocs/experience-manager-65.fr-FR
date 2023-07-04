---
title: Console web dans AEM
description: Découvrez comment utiliser la console web dans AEM.
uuid: 047274ff-4d7d-4c7d-95be-06f363beae2e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: f934eb02-1f84-44f2-9f14-3f17250c9a90
exl-id: bdfeaf85-e832-40c1-8769-7d027cdb021e
source-git-commit: a17b25e55a0bf16a0df42a7ba4768503618a19e2
workflow-type: ht
source-wordcount: '724'
ht-degree: 100%

---

# Console Web{#web-console}

La console web dans AEM (Adobe Experience Manager) est basée sur la [console de gestion web Apache Felix](https://felix.apache.org/documentation/subprojects/apache-felix-web-console.html). Apache Felix est un travail de la communauté pour mettre en œuvre la plateforme de service OSGi R4, qui inclut le cadre OSGi et les services standard.

>[!NOTE]
>
>Dans la console web, toutes les descriptions qui mentionnent les paramètres par défaut sont liées aux valeurs Sling par défaut.
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
>Voir [Configuration OSGi à l’aide de la console web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) pour plus de détails.

L’onglet **Configuration** est accessible soit via :

* Le menu déroulant :

   **OSGi >**

* L’URL ; par exemple :

   `http://localhost:4502/system/console/configMgr`

Une liste des configurations s’affiche : 

![screen_shot_2012-02-15at52308pm-1](assets/screen_shot_2012-02-15at52308pm-1.png)

Il existe deux types de configurations disponibles à partir des listes déroulantes de cet écran :

* **Configurations**

    Vous permet de mettre à jour les configurations existantes. Elles possèdent une identité persistante (PID) et peuvent être :

   * standard ou intégrales pour AEM. Elles sont nécessaires ; si elles sont supprimées, les valeurs sont renvoyées aux paramètres par défaut.
   * les instances créées à partir des configurations d’usine ; ces instances sont créées par l’utilisateur ou l’utilisatrice et la suppression supprime l’instance.

* **Configurations d’usine**

   Vous permettent de créer une instance de l’objet de la fonctionnalité requise.

   Elles se verront attribuer une identité permanente, puis seront répertoriées dans les configurations de la liste déroulante.

En sélectionnant une entrée des listes, vous pourrez voir les paramètres associés à cette configuration :

![chlimage_1-61](assets/chlimage_1-61.png)

Vous pouvez mettre à jour les paramètres selon vos besoins et : 

* **Enregistrer**

   Enregistrez les modifications apportées.

   Pour une configuration d’usine, cela crée une instance avec une identité permanente. La nouvelle instance est ensuite répertoriée sous Configurations.

* **Réinitialiser**

   Réinitialise les paramètres affichés sur l’écran pour revenir à ceux enregistrés en dernier.

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

![screen_shot_2012-02-15at44740pm-1](assets/screen_shot_2012-02-15at44740pm-1.png)

En utilisant cet onglet vous pouvez :

* **Installer ou mettre à jour**

   Vous pouvez utiliser l’option **Parcourir** pour trouver le fichier contenant votre lot et spécifier s’il doit **commencer** immédiatement et à quel **niveau de départ**.

* **Recharger**

   Actualise la liste affichée.

* **Actualiser les packages**

   Cela permettra de vérifier les références de tous les packages et de les actualiser au besoin.

   Par exemple, après une mise à jour, l’ancienne et la nouvelle version peuvent toujours être exécutées en raison de références antérieures. Cette option permettra de vérifier et de déplacer toutes les références vers la nouvelle version, ce qui permettra d’arrêter l’ancienne version.

* **Démarrer**

   Lance un lot en fonction du niveau initial spécifié.

* **Arrêter**

   Arrête le lot.

* **Désinstaller**

   Permet de désinstaller le lot du système.

* **Afficher le statut**

   La liste indique le statut actuel du lot ; en cliquant sur le nom d’un lot spécifique, vous obtenez des informations supplémentaires.

>[!NOTE]
>
>Après la **mise à jour**, il est recommandé d’effectuer une **actualisation des packs**.

## Composants {#components}

L’onglet **Composants** vous permet d’activer et de désactiver divers composants. Il est accessible par les éléments suivants :

* Le menu déroulant :

   **Principal >**

* L’URL ; par exemple :

   `http://localhost:4502/system/console/components`

Une liste de composants s’affiche. Plusieurs icônes sont disponibles pour vous permettre d’activer, de désactiver ou (le cas échéant) d’ouvrir les détails de la configuration pour un composant spécifique.

![screen_shot_2012-02-15at52144pm-1](assets/screen_shot_2012-02-15at52144pm-1.png)

Cliquer sur le nom d’un composant spécifique affiche des informations supplémentaires sur son statut. Vous pouvez également activer, désactiver ou recharger le composant.

![chlimage_1-62](assets/chlimage_1-62.png)

>[!NOTE]
>
>L’activation ou la désactivation d’un composant ne s’applique que jusqu’au redémarrage d’AEM/CRX.
>
>L’état de départ est défini dans le descripteur de composant, qui est généré pendant le développement et stocké dans le lot au moment de la création du lot.
