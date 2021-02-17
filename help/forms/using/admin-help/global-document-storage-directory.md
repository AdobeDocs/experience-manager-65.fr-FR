---
title: Répertoire de stockage global de documents
seo-title: Répertoire de stockage global de documents
description: Le répertoire de stockage global de documents est utilisé pour stocker les fichiers de longue durée utilisés dans un processus.
seo-description: Le répertoire de stockage global de documents est utilisé pour stocker les fichiers de longue durée utilisés dans un processus.
uuid: 7681672c-a0dc-4445-8004-1b1e2ed3d301
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a33b8834-6e39-47eb-a53b-0982d32e80ad
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f
workflow-type: tm+mt
source-wordcount: '700'
ht-degree: 97%

---


# Répertoire de stockage global de documents{#global-document-storage-directory}

Le répertoire de *stockage global de documents* est utilisé pour stocker les fichiers de longue durée utilisés dans un processus. Ces fichiers comprennent des PDF, des stratégies et des modèles de formulaires. Les fichiers de longue durée jouent un rôle capital la plupart des déploiements d’AEM. Si certains d’entre eux sont perdus ou corrompus, le serveur Forms peut devenir instable. Les documents d’entrée pour les appels de travaux asynchrones sont également stockés dans le répertoire de stockage global de documents et doivent être disponibles pour traiter les demandes. Il est donc important que vous preniez en compte la fiabilité du système de fichiers hébergeant le répertoire de stockage global de documents. Utilisez une technologie RAID (Redundant Array of Independent Disks) ou toute autre technologie appropriée pour répondre à vos besoins en termes de qualité et de niveau de service.

Les fichiers de longue durée peuvent contenir des informations utilisateur sensibles. Des informations d’identification spéciales peuvent être nécessaires pour y accéder en utilisant les API ou les interfaces utilisateur d’AEM forms. Il est important de sécuriser correctement le répertoire de stockage global de documents au niveau du système d’exploitation. Seul le compte administrateur chargé d’exécuter le serveur d’applications doit disposer des autorisations d’accès en lecture/écriture sur ce répertoire.

Outre la sélection d’un répertoire de stockage global de documents sécurisé et situé à un emplacement de haute disponibilité, vous pouvez également activer le stockage de documents dans la base de données. Même en utilisant la base de données AEM forms pour le stockage de documents, AEM forms requiert toujours le répertoire de stockage global de documents (voir [Options de sauvegarde dans le cas de l’utilisation de la base de données pour le stockage de documents](/help/forms/using/admin-help/files-back-recover.md#backup-options-when-database-is-used-for-document-storage)).

Les données d’application AEM forms résident dans le répertoire de stockage global de documents et dans la base de données AEM forms. Le tableau suivant décrit les données et leur emplacement.

<table>
 <thead>
  <tr>
   <th><p>Données AEM forms</p></th>
   <th><p>Base de données</p></th>
   <th><p>Répertoire de stockage global de documents</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Données d’application (utilisateurs, rôles, processus, stratégies, points de fin, événements, etc.)</p></td>
   <td><p>Oui</p></td>
   <td><p>Non</p></td>
  </tr>
  <tr>
   <td><p>Conteneurs de service déployés</p></td>
   <td><p>Oui</p></td>
   <td><p>Non</p></td>
  </tr>
  <tr>
   <td><p>Document Manager </p></td>
   <td><p>Non</p></td>
   <td><p>Oui</p></td>
  </tr>
  <tr>
   <td><p>Référentiel de formulaires</p></td>
   <td><p>Oui</p></td>
   <td><p>Non</p></td>
  </tr>
  <tr>
   <td><p>Configuration du système</p></td>
   <td><p>Oui</p></td>
   <td><p>Non</p></td>
  </tr>
  <tr>
   <td><p>Dossiers de contrôle</p></td>
   <td><p>Non</p></td>
   <td><p>Oui</p></td>
  </tr>
 </tbody>
</table>

## Configuration du répertoire de stockage global de document {#configuring-the-gds-directory}

L’emplacement du répertoire de stockage global de documents peut être configuré manuellement pendant la procédure d’installation d’AEM forms. Si le paramètre d’emplacement du stockage global de documents n’est pas défini pendant l’installation, l’emplacement par défaut utilisé est un sous-répertoire de l’emplacement d’installation du serveur d’applications :

* (JBoss) `[appserver root]/server/[type]/svcnative/DocumentStorage`
* (WebLo gic) `[appserverdomain]/'server'/adobe/DocumentServer/DocumentStorage`
* (WebSphere) `[appserver root]/installedApps/adobe/'server'/DocumentStorage`

## Modification de l’emplacement par défaut du stockage global de documents {#change-the-default-gds-location}

Vous pouvez modifier l’emplacement du répertoire de stockage global de documents dans Administration Console après l’installation d’AEM forms. Vous devez également déplacer les données manuellement pour terminer le processus.

>[!NOTE]
>
>procédez comme suit pour effectuer la migration des données, sinon vous risquez de perdre des données.

1. Connectez-vous à Administration Console et cliquez sur Paramètres > Paramètres de Core System > Configurations.
1. Dans la zone Répertoire de stockage global de documents, saisissez le chemin d’accès complet au nouveau répertoire, puis cliquez sur OK.
1. Juste après, arrêtez le serveur d’applications.
1. Déplacez tous les fichiers qui se trouvent dans l’ancien répertoire de stockage global de documents vers le nouvel emplacement, en conservant l’arborescence de répertoires internes.
1. Redémarrez le serveur d’applications.

## A propos des fichiers de déploiement  {#about-deployment-files}

AEM forms est constitué de deux types de fichiers de déploiement : les conteneurs de service et les fichiers EAR de la plateforme Java 2 Enterprise Edition (J2EE). Ce sont des modules d’application J2EE standard qui contiennent les principales fonctionnalités d’AEM forms. Les fichiers EAR propres à chaque serveur d’applications sont les suivants :

* adobe-core-*[appserver]*.ear
* adobe-core-*[appserver]*-*[OS]*.ear

L’implémentation d’AEM forms implique le déploiement des fichiers EAR assemblés et des fichiers de prise en charge sur le serveur d’applications sur lequel vous envisagez d’exécuter la solution AEM forms. Si vous avez configuré et assemblé plusieurs modules, les modules déployables sont contenus dans les fichiers EAR déployables. Pour déployer ces fichiers, copiez-les dans le répertoire d’accueil *[du serveur d’applications]*\server\all\deploy directory.

Les modules et les fichiers d’archive d’AEM forms sont compressés dans des fichiers JAR. Comme ce ne sont pas des fichiers J2EE, ils ne sont pas déployés sur le serveur d’applications. Ils sont copiés dans le répertoire de stockage global de documents et une référence à leur emplacement est stockée dans la base de données AEM forms. C’est pourquoi le répertoire de stockage global de documents doit être partagé par tous les nœuds de la grappe. Ces derniers doivent avoir accès au répertoire de stockage central des DSC.

>[!NOTE]
>
>avant de déployer les conteneurs de service, vérifiez que vous avez créé et configuré le répertoire de stockage global de documents (voir [Configuration du répertoire de stockage global de documents](global-document-storage-directory.md#configuring-the-gds-directory)).

