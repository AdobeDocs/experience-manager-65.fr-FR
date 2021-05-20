---
title: Fontionnalités Configuration de l’activation
seo-title: Fontionnalités Configuration de l’activation
description: Configuration des fonctionnalités d’activation dans Communities
seo-description: Configuration des fonctionnalités d’activation dans Communities
uuid: 27be3128-1a7d-412e-99a9-6e3b3b0aec1c
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 765a3d9b-4552-403e-872c-fdf684ac271d
role: Administrator
exl-id: b635e2ed-4637-4b2f-a746-ec8dc7541bab
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 4%

---

# Fontionnalités Configuration de l’activation {#configuring-enablement-features}

## Présentation {#overview}

Les fonctionnalités d’activation permettent de créer des [communautés d’activation](overview.md#enablement-community).

* Cette fonctionnalité nécessite des licences supplémentaires pour être utilisée dans un environnement de production.

L’utilisation des fonctionnalités d’activation requiert les éléments suivants :

Installation de :

* **SCORM**

   SCORM (Sharable Content Object Reference Model) est un ensemble de normes et de spécifications pour l’apprentissage en ligne. SCORM définit également la manière dont le contenu peut être compressé dans un fichier ZIP transférable.

* **MySQL**

   MySQL est une base de données relationnelle principalement utilisée pour le suivi SCORM et les données de création de rapports pour l’activation, ainsi que les tableaux pour le suivi de la progression vidéo. Le pack de fonctionnalités SCORM pour l’activation nécessite le pilote JDBC MySQL.

* **FFmpeg**

   FFmpeg est une solution pour la conversion et la diffusion en continu d’audio et de vidéo. Lorsqu’elle est installée, elle est utilisée pour le transcodage correct des [ressources vidéo](../../help/sites-authoring/default-components-foundation.md#video). Pour les communautés d’activation, elle est utilisée dans l’environnement de création pour obtenir des métadonnées pour les ressources chargées et générer une miniature à afficher lors de la mise en liste de la ressource.

Configuration de :

* **Gestionnaires de la communauté**

   Pour les communautés d’activation, seuls les membres du groupe d’utilisateurs `Community Enablement Managers` peuvent se voir attribuer le rôle `Community Site Enablement Manager`, dont les autorisations peuvent inclure la création de contenu, les affectations et la gestion des membres dans l’environnement de publication.

Configuration facultative de :

* **Adobe Analytics**

   L’intégration à Adobe Analytics ajoute des fonctions de création de rapports complètes et prend en charge l’ajout de la pulsation vidéo à Analytics.

* **Dispatcher**

## Étapes de configuration {#configuration-steps}

Vous trouverez ci-dessous les étapes nécessaires aux communautés d’activation.

Chaque étape renvoie à la documentation qui fournit les détails nécessaires.

**Sur toutes les instances d’auteur/de publication :**

1. **[Installation du pilote JDBC pour MySQL](deploy-communities.md#jdbc-driver-for-mysql)**

   Utiliser la console web (lots) : *http://localhost:4502/system/console/bundles*

   Installez *avant* d’installer le package SCORM.

1. **[Installer le package SCORM](deploy-communities.md#scorm-package)**


   Utilisation de Package Manager : *http://localhost:4502/crx/packmgr/*

**Sur n’importe quel serveur :**

1. **[Installer MySQL, MySQL Workbench](mysql.md)**

1. **[Installation des bases de données MySQL](mysql.md#database-setup)**

   Exécution des scripts SQL téléchargés à partir de l’instance d’auteur

   Utilisation de MySQL Workbench

**Sur la même instance d’auteur d’hébergement de serveur :**

1. **[Installation de FFmpeg](ffmpeg.md)**

**Sur toutes les instances d’auteur/de publication :**

1. **[Configuration du pool de connexions JDBC](mysql.md#configure-jdbc-connections)**

   Utiliser la console web (configMgr) : *http://localhost:4502/system/console/configMgr*

1. **[Configuration du service de moteur SCORM](mysql.md#aem-communities-scormengine-service)**

   Utiliser la console web (configMgr) : *http://localhost:4502/system/console/configMgr*

1. **[Configuration des filtres CSRF](mysql.md#adobe-granite-csrf-filter)**

   Utiliser la console web (configMgr) : *http://localhost:4502/system/console/configMgr*

**Sur l’instance d’auteur :**

1. (*Facultatif*) **[Configurer le service Analytics](analytics.md)**

   Utilisez la console Outils, Déploiement, Cloud Services : *http://localhost:4502/etc/cloudservices/sitecatalyst.html*

1. **[Configuration de FFmpeg](ffmpeg.md#configure-ffmpeg-transcoding-service)**

   Utilisation de la console Processus/Modèles

1. **[Activer le service de tunnel](deploy-communities.md#tunnel-service-on-author)**

   Utiliser la console web (configMgr) : *http://localhost:4502/system/console/configMgr*

1. **[Création d’administrateurs de communauté](users.md#creating-community-members)**

   Pour l’environnement de création, utilisez la console de sécurité de l’IU classique : *http://localhost:4502/useradmin*

   Créer un ou plusieurs utilisateurs avec le chemin d’accès = /home/users/community

   * Ajoutez des membres aux groupes suivants :

      * Chefs d’activation de la communauté
      * Administrateurs des communautés

## Dispatcher {#dispatcher}

Lorsque le déploiement comprend [AEM Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html), pour que les fonctionnalités d’activation fonctionnent correctement, les sections `clientheader` et `filter` doivent être modifiées. Voir [Configuration de Dispatcher pour Communities](dispatcher.md#enablement).
