---
title: Console web
seo-title: Web Console
description: Apprenez à utiliser le console web d’AEM.
seo-description: Learn how to use the AEM web console.
uuid: 7856b2b3-4216-421d-a315-cd9a55936362
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 4a33fddd-0399-40e4-8687-564fb6765b76
feature: Configuring
exl-id: 9acbf61f-73a8-4998-9421-dd933f30ac8a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '718'
ht-degree: 100%

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

Cette console est accessible à partir de `../system/console` ; par exemple :

`http://localhost:4502/system/console/components`

## Configuration {#configuration}

L’onglet **Configuration** est utilisé pour configurer les lots OSGi. Il s’agit donc du mécanisme sous-jacent pour configurer les paramètres du système AEM.

>[!NOTE]
>
>Pour plus d’informations, voir [Configuration OSGi avec la console web](/help/sites-deploying/configuring-osgi.md).

L’onglet **Configuration** est accessible soit via :

* Le menu déroulant :

   **OSGi >**

* L’URL ; par exemple :

   `http://localhost:4502/system/console/configMgr`

Une liste des configurations s’affiche : 

![screen_shot_2012-02-15at52308pm](assets/screen_shot_2012-02-15at52308pm.png)

Il existe deux types de configurations disponibles à partir des listes déroulantes de cet écran :

* **Configurations**
Vous permet de mettre à jour les configurations existantes. Elles ont une identité permanente (PID) et peuvent être :

   * standard et intégrales pa rapport à AEM ; elles sont nécessaires, car si on les supprime, leurs valeurs sont renvoyées aux paramètres par défaut.
   * des instances créées à partir des configurations d’usine ; ces instances sont créées par l’utilisateur. Leur suppression entraîne la suppression de l’instance. 

* **Configurations d’usine**
Vous permet de créer une instance de l’objet de la fonctionnalité requise. 

   Elles se verront attribuer une identité permanente, puis seront répertoriées dans les configurations de la liste déroulante.

En sélectionnant une entrée des listes, vous pourrez voir les paramètres associés à cette configuration :

![chlimage_1-21](assets/chlimage_1-21a.png)

Vous pouvez mettre à jour les paramètres selon vos besoins et : 

* **Enregistrer**

   Enregistrez les modifications apportées.

   Pour une configuration d’usine, cela crée une instance avec une identité permanente. La nouvelle instance est ensuite répertoriée sous Configurations. 

* **Réinitialiser**

   Réinitialise les paramètres affichés sur l’écran pour revenir à ceux enregistrés en dernier.

* **Supprimer**

   Supprime la configuration actuelle. S’il s’agit d’une configuration standard, les paramètres sont renvoyés aux paramètres par défaut. Si elle a été créée à partir d’une configuration d’usine, l’instance spécifiée est supprimée.

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

* **Actualiser des modules**

   Cette option permettra de vérifier les références de tous les modules et de les actualiser si besoin est.

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
>Après la **mise à jour**, il est recommandé d’**actualiser les modules**.

## Composants {#components}

L’onglet **Composants** vous permet d’activer et de désactiver divers composants. Il est accessible par les éléments suivants :

* Le menu déroulant :

   **Principal >**

* L’URL ; par exemple :

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
