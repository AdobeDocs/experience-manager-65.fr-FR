---
title: Répertoire de stockage global de documents
description: Le répertoire de stockage global de documents (GDS) est utilisé pour stocker les fichiers de longue durée utilisés dans un processus.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 7a64a643-808b-4644-8fd3-0dafe83e8dd9
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 7%

---

# Répertoire de stockage global de documents{#global-document-storage-directory}

La variable *stockage global de documents (GDS)* directory est un répertoire utilisé pour stocker les fichiers de longue durée utilisés dans un processus. Ces fichiers comprennent des PDF, des stratégies et des modèles de formulaire. Les fichiers de longue durée sont une partie essentielle de l’état global de nombreux déploiements d’AEM forms. Si certains ou tous les documents de longue durée sont perdus ou corrompus, le serveur Forms peut devenir instable. Les documents d’entrée pour les appels de tâches asynchrones sont également stockés dans le répertoire de stockage global de documents et doivent être disponibles pour traiter les demandes. Il est important de tenir compte de la fiabilité du système de fichiers qui héberge le répertoire de stockage global de documents. Utilisez une matrice redondante de disques indépendants (RAID) ou d’autres technologies adaptées à vos besoins en termes de qualité et de niveau de service.

Les fichiers de longue durée peuvent contenir des informations utilisateur sensibles. Ces informations peuvent nécessiter des informations d’identification spéciales lors de l’accès à l’aide des API d’AEM forms ou des interfaces utilisateur. Il est important que le répertoire de stockage global de documents soit correctement sécurisé par le biais du système d’exploitation. Seul le compte administrateur utilisé pour exécuter le serveur d’applications doit disposer d’un accès en lecture/écriture au répertoire de stockage global de documents.

Outre la sélection d’un répertoire de stockage global de documents sécurisé et hautement disponible, vous pouvez également activer le stockage de documents dans la base de données. Même si vous utilisez la base de données d’AEM forms pour le stockage de documents, AEM forms a toujours besoin du répertoire de stockage global de documents. (Voir [Options de sauvegarde lors de l’utilisation de la base de données pour le stockage de documents](/help/forms/using/admin-help/files-back-recover.md#backup-options-when-database-is-used-for-document-storage).)

Les données d’application d’AEM forms résident dans le répertoire de stockage global de documents et dans la base de données d’AEM forms. Le tableau suivant décrit les données et leur emplacement.

<table>
 <thead>
  <tr>
   <th><p>Données de formulaires AEM</p></th>
   <th><p>Base de données</p></th>
   <th><p>GDS</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Données de l’application (utilisateurs, rôles, processus, stratégies, points de fin, événements, etc.)</p></td>
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
   <td><p>Référentiel Forms</p></td>
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

## Configuration du répertoire de stockage global de documents {#configuring-the-gds-directory}

L’emplacement du répertoire de stockage global de documents peut être configuré manuellement pendant le processus d’installation d’AEM forms. Si le paramètre d’emplacement reste vide pendant l’installation, l’emplacement est défini par défaut sur un répertoire sous l’installation du serveur d’applications, comme suit :

* (JBoss) `[appserver root]/server/[type]/svcnative/DocumentStorage`
* (WebLo gic) `[appserverdomain]/'server'/adobe/DocumentServer/DocumentStorage`
* (WebSphere) `[appserver root]/installedApps/adobe/'server'/DocumentStorage`

## Modification de l’emplacement du répertoire de stockage global de documents par défaut {#change-the-default-gds-location}

Vous pouvez modifier l’emplacement du répertoire de stockage global de documents dans Administration Console une fois l’installation d’AEM forms terminée. Déplacez manuellement les données pour terminer le processus.

>[!NOTE]
>
>Effectuez la migration des données de la manière suivante, sans quoi vous risquez de perdre des données.

1. Connectez-vous à Administration Console et cliquez sur Paramètres > Paramètres de Core System > Configurations.
1. Dans la zone Répertoire de stockage global de documents, saisissez le chemin d’accès complet au nouveau répertoire de stockage global de documents, puis cliquez sur OK.
1. Arrêtez immédiatement le serveur d’applications.
1. Déplacez tous les fichiers de l’ancien répertoire de stockage global de documents vers le nouvel emplacement, en conservant la structure de répertoires interne.
1. Redémarrez le serveur d’applications.

## À propos des fichiers de déploiement {#about-deployment-files}

AEM forms se compose de deux types de fichiers de déploiement : les conteneurs de service et les fichiers EAR de Java 2 Platform Enterprise Edition (J2EE). Les fichiers EAR se composent de lots d’applications J2EE standard contenant les fonctionnalités de base d’AEM forms. Les fichiers EAR spécifiques au serveur d’applications sont les suivants :

* adobe-core-*[appserver]*.ear
* adobe-core-*[appserver]*-*[OS]*.ear

La mise en oeuvre d’AEM forms implique le déploiement des fichiers EAR assemblés et des fichiers de prise en charge sur le serveur d’applications sur lequel vous envisagez d’exécuter votre solution AEM forms. Si vous avez configuré et assemblé plusieurs modules, les modules déployables sont contenus dans les fichiers EAR déployables. Pour déployer ces fichiers, copiez-les dans le répertoire *[appserver home]*\server\all\deploy.

Les modules et les fichiers d’archive d’AEM forms sont compressés dans des fichiers JAR. Puisqu’il ne s’agit pas de fichiers de type J2EE, ils ne sont pas déployés sur le serveur d’applications. Ils sont copiés dans le répertoire de stockage global de documents et une référence à leur emplacement est stockée dans la base de données d’AEM forms. Pour cette raison, le répertoire de stockage global de documents doit être partagé entre tous les noeuds de la grappe. Tous les noeuds doivent avoir accès au répertoire de stockage central pour les DSC.

>[!NOTE]
>
>Avant de déployer les conteneurs de service, assurez-vous d’avoir créé et configuré le répertoire de stockage global de documents. (Voir [Configuration du répertoire de stockage global de documents](global-document-storage-directory.md#configuring-the-gds-directory))
