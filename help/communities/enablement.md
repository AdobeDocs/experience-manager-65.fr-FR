---
title: Fontionnalités Configuration de l’activation
seo-title: Fontionnalités Configuration de l’activation
description: Configuration des fonctionnalités d’activation dans les communautés
seo-description: Configuration des fonctionnalités d’activation dans les communautés
uuid: 27be3128-1a7d-412e-99a9-6e3b3b0aec1c
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 765a3d9b-4552-403e-872c-fdf684ac271d
translation-type: tm+mt
source-git-commit: 0b25d956c19c5fc5d79f87b292a0c61a23e5d66a

---


# Fontionnalités Configuration de l’activation {#configuring-enablement-features}

## Présentation {#overview}

Les fonctions d’activation permettent de créer des communautés [d’](overview.md#enablement-community)activation.

* Cette fonctionnalité nécessite une licence supplémentaire pour une utilisation dans un  de production .

L’utilisation des fonctions d’activation requiert les éléments suivants :

Installation de :

* **SCORM**

   SCORM (Sharable Content Object Reference Model) est un ensemble de normes et de spécifications pour l’apprentissage en ligne. SCORM définit également la manière dont le contenu peut être compressé dans un fichier ZIP transférable.

* **MySQL**

   MySQL est une base de données relationnelle principalement utilisée pour le suivi SCORM et les données de  pour l’activation, ainsi que les tableaux pour le suivi de la progression vidéo. Le pack de fonctionnalités SCORM pour l’activation requiert le pilote JDBC MySQL.

* **FFmpeg**

   FFmpeg est une solution de conversion et de diffusion audio et vidéo en flux continu et, lorsqu’elle est installée, elle est utilisée pour le transcodage approprié des fichiers [](../../help/sites-authoring/default-components-foundation.md#video)vidéo. Pour les communautés d’activation, elle est utilisée dans le  de l’auteur  pour obtenir des métadonnées pour les ressources téléchargées et générer une miniature à afficher lors de la liste de la ressource.

Configuration de :

* **Gestionnaires de la communauté**

   Pour les communautés d’activation, seuls les membres du groupe `Community Enablement Managers` d’utilisateurs peuvent se voir attribuer le rôle de `Community Site Enablement Manager`, dont les autorisations peuvent inclure la création de contenu, les affectations et la gestion des membres dans le  de publication .

Configuration facultative de :

* **Adobe Analytics**

   L’intégration à Adobe Analytics ajoute des fonctionnalités  complètes et prend en charge l’ajout de la pulsation vidéo à Analytics.

* **Répartiteur**

## Étapes de configuration {#configuration-steps}

Voici les étapes nécessaires pour activer les communautés.

Chaque étape renvoie à la documentation qui fournit les détails nécessaires.

**Sur toutes les instances d’auteur/de publication :**

1. **[Installation du pilote JDBC pour MySQL](deploy-communities.md#jdbc-driver-for-mysql)**

   Utiliser la console Web (lots) : *http://localhost:4502/system/console/bundles* Installation *avant* l’installation du package SCORM

1. **[Installation du package](deploy-communities.md#scorm-package)**SCORM Utiliser Package Manager :*http://localhost:4502/crx/packmgr/*

**Sur n’importe quel serveur :**

1. **[Installation de MySQL, MySQL Workbench](mysql.md)**

1. **[Installation des bases de données MySQL](mysql.md#database-setup)**

   Exécuter des scripts SQL téléchargés à partir de l’instance d’auteurUtiliser MySQL Workbench

**Sur la même instance d’auteur d’hébergement de serveur :**

1. **[Installation de FFmpeg](ffmpeg.md)**

**Sur toutes les instances d’auteur/de publication :**

1. **[Configuration du pool de connexions JDBC](mysql.md#configure-jdbc-connections)**

   Utiliser la console Web (configMgr) : *http://localhost:4502/system/console/configMgr*

1. **[Configuration du service du moteur SCORM](mysql.md#aem-communities-scormengine-service)**

   Utiliser la console Web (configMgr) : *http://localhost:4502/system/console/configMgr*

1. **[Configuration du CSRF](mysql.md#adobe-granite-csrf-filter)**

   Utiliser la console Web (configMgr) : *http://localhost:4502/system/console/configMgr*

**Sur l’instance d’auteur :**

1. (*Facultatif*) **[Configuration du service Analytics](analytics.md)**

   Utilisez Outils, Déploiement, Console des services cloud : *http://localhost:4502/etc/cloudservices/sitecatalyst.html*

1. **[Configuration de FFmpeg](ffmpeg.md#configure-ffmpeg-transcoding-service)**

   Utiliser la console Workflow/Modèles

1. **[Activer le service de tunnel](deploy-communities.md#tunnel-service-on-author)**

   Utiliser la console Web (configMgr) : *http://localhost:4502/system/console/configMgr*

1. **[Création d’administrateurs de communauté](users.md#creating-community-members)**

   Pour les  de l&#39;auteur  utilisez la console de sécurité classique-IU : *http://localhost:4502/useradmin* créer des utilisateurs avec chemin = /home/users/community

   * Ajouter les membres aux groupes suivants :

      * Gestionnaires d’activation de la communauté
      * Administrateurs de communautés

## Répartiteur {#dispatcher}

Lorsque le déploiement inclut le répartiteur [d’](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html)AEM, pour que les fonctionnalités d’activation fonctionnent correctement, les sections `clientheader` et `filter` doivent être modifiées. Voir [Configuration du répartiteur pour les communautés](dispatcher.md#enablement).
