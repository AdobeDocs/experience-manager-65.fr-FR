---
title: Fontionnalités Configuration de l’activation
seo-title: Fontionnalités Configuration de l’activation
description: Configuration des fonctions d’activation dans les communautés
seo-description: Configuration des fonctions d’activation dans les communautés
uuid: 27be3128-1a7d-412e-99a9-6e3b3b0aec1c
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 765a3d9b-4552-403e-872c-fdf684ac271d
translation-type: tm+mt
source-git-commit: ce21755263a2e8a3f0e97acb7f586e32cedde83a
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 4%

---


# Fontionnalités Configuration de l’activation {#configuring-enablement-features}

## Présentation {#overview}

Les fonctions d’activation permettent de créer des communautés [d’](overview.md#enablement-community)activation.

* Cette fonction nécessite une licence supplémentaire pour être utilisée dans un environnement de production.

L’utilisation des fonctions d’activation requiert les éléments suivants :

Installation de :

* **SCORM**

   SCORM (Sharable Content Object Reference Model) est un ensemble de normes et de spécifications pour l&#39;apprentissage en ligne. SCORM définit également comment le contenu peut être inclus dans un fichier ZIP transférable.

* **MySQL**

   MySQL est une base de données relationnelle principalement utilisée pour le suivi SCORM et les données de rapports pour l’activation, ainsi que les tables pour le suivi de la progression vidéo. Le pack de fonctionnalités d’activation SCORM nécessite le pilote JDBC MySQL.

* **FFmpeg**

   FFmpeg est une solution de conversion et de diffusion audio et vidéo en flux continu et, lorsqu’elle est installée, elle est utilisée pour le transcodage approprié des fichiers [](../../help/sites-authoring/default-components-foundation.md#video)vidéo. Pour les communautés d’activation, elle est utilisée dans l’environnement d’auteur pour obtenir des métadonnées pour les ressources téléchargées et pour générer une miniature à afficher lors de la mise en liste de la ressource.

Configuration de :

* **Gestionnaires de la communauté**

   Pour les communautés d’activation, seuls les membres du groupe d’ `Community Enablement Managers` utilisateurs peuvent se voir attribuer le rôle de `Community Site Enablement Manager`, dont les autorisations peuvent inclure la création de contenu, les affectations et la gestion des membres dans l’environnement de publication.

Configuration facultative de :

* **Adobe Analytics**

   L’intégration à Adobe Analytics ajoute des fonctionnalités de rapports complètes et prend en charge l’ajout de la pulsation vidéo à Analytics.

* **Dispatcher**

## Étapes de configuration {#configuration-steps}

Voici les étapes nécessaires pour activer les communautés.

Chaque étape donne un lien vers la documentation qui fournit les détails nécessaires.

**Sur toutes les instances d’auteur/de publication :**

1. **[Installation du pilote JDBC pour MySQL](deploy-communities.md#jdbc-driver-for-mysql)**

   Utiliser la console Web (lots) : *http://localhost:4502/system/console/bundles*

   Installation *avant* l’installation du package SCORM

1. **[Installation du package SCORM](deploy-communities.md#scorm-package)**


   Utilisez Package Manager : *http://localhost:4502/crx/packmgr/*

**Sur n&#39;importe quel serveur :**

1. **[Installation de MySQL, MySQL Workbench](mysql.md)**

1. **[Installation des bases de données MySQL](mysql.md#database-setup)**

   Exécuter des scripts SQL téléchargés à partir de l’instance d’auteur

   Utiliser MySQL Workbench

**Sur le même serveur hébergeant l’instance d’auteur :**

1. **[Installation de FFmpeg](ffmpeg.md)**

**Sur toutes les instances d’auteur/de publication :**

1. **[Configuration du pool de connexions JDBC](mysql.md#configure-jdbc-connections)**

   Utiliser la console Web (configMgr) : *http://localhost:4502/system/console/configMgr*

1. **[Configuration du service du moteur SCORM](mysql.md#aem-communities-scormengine-service)**

   Utiliser la console Web (configMgr) : *http://localhost:4502/system/console/configMgr*

1. **[Configuration de filtres CSRF](mysql.md#adobe-granite-csrf-filter)**

   Utiliser la console Web (configMgr) : *http://localhost:4502/system/console/configMgr*

**Sur l’instance d’auteur :**

1. (*Facultatif*) **[Configuration du service Analytics](analytics.md)**

   Utiliser Outils, Déploiement, console Cloud Services : *http://localhost:4502/etc/cloudservices/sitecatalyst.html*

1. **[Configurer FFmpeg](ffmpeg.md#configure-ffmpeg-transcoding-service)**

   Utiliser la console Workflow/Modèles

1. **[Activer le service de tunnel](deploy-communities.md#tunnel-service-on-author)**

   Utiliser la console Web (configMgr) : *http://localhost:4502/system/console/configMgr*

1. **[Création d’administrateurs de communauté](users.md#creating-community-members)**

   Pour l’environnement auteur, utilisez la console de sécurité classique de l’interface utilisateur : *http://localhost:4502/useradmin*

   Créer des utilisateurs avec chemin = /home/users/community

   * Ajoutez les membres aux groupes suivants :

      * Gestionnaires d’activation de la communauté
      * Administrateurs des communautés

## Dispatcher {#dispatcher}

Lorsque le déploiement inclut [AEM Répartiteur](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html), pour que les fonctions d&#39;activation fonctionnent correctement, les `clientheader` sections et `filter` les sections doivent être modifiées. Voir [Configuration du répartiteur pour les communautés](dispatcher.md#enablement).
