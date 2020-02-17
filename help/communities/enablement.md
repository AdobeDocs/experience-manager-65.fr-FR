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
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Fontionnalités Configuration de l’activation {#configuring-enablement-features}

## Présentation {#overview}

Les fonctions d’activation permettent de créer des communautés [d’](overview.md#enablement-community)activation.

* Cette fonctionnalité nécessite une licence supplémentaire pour être utilisée dans un environnement de production.

L’utilisation des fonctions d’activation requiert les éléments suivants :

Installation de :

* **SCORM** Sharable Content Object Reference Model (SCORM) est un ensemble de normes et de spécifications pour l’apprentissage en ligne. SCORM définit également la manière dont le contenu peut être compressé dans un fichier ZIP transférable.

* **MySQL** MySQL est une base de données relationnelle principalement utilisée pour le suivi SCORM et les données de création de rapports pour l’activation, ainsi que pour le suivi de la progression vidéo. Le pack de fonctionnalités SCORM pour l’activation requiert le pilote JDBC MySQL.

* **FFmpeg** FFmpeg est une solution pour la conversion et la diffusion audio et vidéo en flux continu et, lorsqu’elle est installée, elle est utilisée pour le transcodage approprié des fichiers [](../../help/sites-authoring/default-components-foundation.md#video)vidéo. Pour les communautés d’activation, elle est utilisée dans l’environnement de création pour obtenir des métadonnées pour les ressources téléchargées et générer une miniature à afficher lors de la liste de la ressource.

Configuration de :

* **Gestionnaires** de communauté Pour les communautés d’activation, seuls les membres du groupe d’ `Community Enablement Managers` utilisateurs peuvent se voir attribuer le rôle de `*Community Site* Enablement Manager`, dont les autorisations peuvent inclure la création de contenu, les affectations et la gestion des membres dans l’environnement de publication.

Configuration facultative de :

* **L’intégration d’Adobe Analytics**&#x200B;à Adobe Analytics ajoute des fonctionnalités de création de rapports complètes et prend en charge l’ajout de la pulsation vidéo à Analytics.

* **Répartiteur**

## Étapes de configuration {#configuration-steps}

Voici les étapes nécessaires pour activer les communautés.

Chaque étape renvoie à la documentation qui fournit les détails nécessaires.

**Sur toutes les instances d’auteur/de publication :**

1. **[installer le pilote JDBC pour MySQL](deploy-communities.md#jdbc-driver-for-mysql)**Utiliser la console Web (lots) :*http://localhost:4502/system/console/bundles*Installation *avant*l’installation du package SCORM

1. **[installer le package](deploy-communities.md#scorm-package)**SCORM Utiliser Package Manager :*http://localhost:4502/crx/packmgr/*

**Sur n’importe quel serveur :**

1. **[installation de MySQL, MySQL Workbench](mysql.md)**

1. **[installation des bases de données](mysql.md#database-setup)**MySQL Exécution des scripts SQL téléchargés à partir de l&#39;instance d&#39;auteur Utilisation des outils MySQL

**Sur la même instance d’auteur d’hébergement de serveur :**

1. **[installer FFmpeg](ffmpeg.md)**

**Sur toutes les instances d’auteur/de publication :**

1. **[configuration du pool](mysql.md#configure-jdbc-connections)**de connexions JDBC Utilisez la console Web (configMgr) :*http://localhost:4502/system/console/configMgr*

1. **[configuration du service](mysql.md#aem-communities-scormengine-service)**du moteur SCORM Utiliser la console Web (configMgr) :*http://localhost:4502/system/console/configMgr*

1. **[configurer les filtres](mysql.md#adobe-granite-csrf-filter)**CSRF Utiliser la console Web (configMgr) :*http://localhost:4502/system/console/configMgr*

**Sur l’instance d’auteur :**

1. (*facultatif*) **[configurez le service](analytics.md)**AnalyticsUse Tools, Deployment, Cloud Services Console :*http://localhost:4502/etc/cloudservices/sitecatalyst.html*

1. **[configuration de FFmpeg](ffmpeg.md#configure-ffmpeg-transcoding-service)**Utiliser la console Workflow/Modèles

1. **[activer le service](deploy-communities.md#tunnel-service-on-author)**Tunnel Utiliser la console Web (configMgr) :*http://localhost:4502/system/console/configMgr*

1. **[créer des administrateurs](users.md#creating-community-members)**de communauté Pour l’environnement de création, utilisez la console de sécurité classique-IU :*http://localhost:4502/useradmin*créer des utilisateurs avec chemin = /home/users/community

   * Ajoutez des membres aux groupes suivants :

      * Gestionnaires d’activation de la communauté
      * Administrateurs de communautés

## Répartiteur {#dispatcher}

Lorsque le déploiement inclut le répartiteur [d’](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html)AEM, pour que les fonctionnalités d’activation fonctionnent correctement, les sections `clientheader`et `filter`les sections doivent être modifiées. Voir [Configuration du répartiteur pour les communautés](dispatcher.md#enablement).
