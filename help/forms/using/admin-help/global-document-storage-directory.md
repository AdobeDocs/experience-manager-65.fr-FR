---
title: Répertoire de stockage global de documents
description: Le répertoire de stockage global de documents (GDS) est un répertoire utilisé pour stocker les fichiers de longue durée utilisés dans un processus.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 7a64a643-808b-4644-8fd3-0dafe83e8dd9
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 100%

---

# Répertoire de stockage global de documents{#global-document-storage-directory}

Le répertoire de *stockage global de documents (GDS)* est un répertoire utilisé pour stocker les fichiers de longue durée utilisés dans un processus. Ces fichiers incluent des fichiers PDF, des politiques et des modèles de formulaire. Les fichiers de longue durée constituent un élément essentiel de l’état général de nombreux déploiements d’AEM Forms. Si une partie ou la totalité de ces documents est perdue ou corrompue, le serveur Forms peut devenir instable. Les documents d’entrée pour les appels de tâches asynchrones sont également stockés dans le répertoire GDS et doivent être disponibles pour traiter les requêtes. Il est important de prendre en compte la fiabilité du système de fichiers qui héberge le répertoire GDS. Utilisez la technologie RAID ou une autre technologie adaptée à vos besoins en matière de qualité et de niveau de service.

Les fichiers de longue durée peuvent contenir des informations utilisateur sensibles. Ces informations peuvent nécessiter des informations d’identification spéciales lorsqu’elles sont accessibles à l’aide des API ou des interfaces utilisateur d’AEM Forms. Il est important que le répertoire GDS soit correctement sécurisé via le système d’exploitation. Seul le compte d’administrateur ou d’administratrice utilisé pour exécuter le serveur d’applications doit disposer d’un accès en lecture/écriture au répertoire GDS.

En plus de sélectionner un répertoire sécurisé et hautement disponible pour GDS, vous pouvez également choisir d’activer le stockage de documents dans la base de données. Notez que même en utilisant la base de données AEM Forms pour le stockage de documents, AEM Forms nécessite toujours le répertoire GDS. (Voir [Options de sauvegarde lorsque la base de données est utilisée pour le stockage de documents](/help/forms/using/admin-help/files-back-recover.md#backup-options-when-database-is-used-for-document-storage).)

Les données de l’application AEM Forms résident dans le répertoire GDS et dans la base de données AEM Forms. Le tableau suivant décrit les données et leurs emplacements.

<table>
 <thead>
  <tr>
   <th><p>Données AEM Forms</p></th>
   <th><p>Base de données</p></th>
   <th><p>GDS</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Données d’application (utilisateurs et utilisatrices, rôles, processus, politiques, points d’entrée, événements, etc.)</p></td>
   <td><p>Oui</p></td>
   <td><p>Non</p></td>
  </tr>
  <tr>
   <td><p>Conteneurs de services déployés</p></td>
   <td><p>Oui</p></td>
   <td><p>Non</p></td>
  </tr>
  <tr>
   <td><p>Gestionnaire de documents </p></td>
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

## Configurer le répertoire GDS {#configuring-the-gds-directory}

L’emplacement du répertoire GDS peut être configuré manuellement pendant le processus d’installation d’AEM Forms. Si le paramètre d’emplacement reste vide pendant l’installation, l’emplacement est par défaut un répertoire sous l’installation du serveur d’applications :

* (JBoss) `[appserver root]/server/[type]/svcnative/DocumentStorage`
* (WebLo gic) `[appserverdomain]/'server'/adobe/DocumentServer/DocumentStorage`
* (WebSphere) `[appserver root]/installedApps/adobe/'server'/DocumentStorage`

## Modifier l’emplacement GDS par défaut {#change-the-default-gds-location}

Vous pouvez modifier l’emplacement GDS dans la console d’administration une fois l’installation d’AEM Forms terminée. Déplacez manuellement les données pour terminer le processus.

>[!NOTE]
>
>Migrez les données de la manière suivante, sinon une perte de données se produira.

1. Connectez-vous à la console d’administration et cliquez sur Paramètres > Paramètres de Core System > Configurations.
1. Dans la zone Répertoire de stockage global de documents, entrez le chemin complet du nouveau répertoire GDS, puis cliquez sur OK.
1. Arrêtez immédiatement le serveur d’applications.
1. Déplacez tous les fichiers de l’ancien répertoire GDS vers le nouvel emplacement, en conservant la structure de répertoire interne.
1. Redémarrez le serveur d’applications.

## À propos des fichiers de déploiement {#about-deployment-files}

AEM Forms se compose de deux types de fichiers de déploiement, les conteneurs de services et les fichiers EAR Java 2 Platform, Enterprise Edition (J2EE). Les fichiers EAR sont constitués de lots d’applications J2EE standard qui contiennent les fonctionnalités de base d’AEM Forms. Les fichiers EAR spécifiques au serveur d’applications sont les suivants :

* adobe-core-*[appserver]*.ear
* adobe-core-*[appserver]*-*[OS]*.ear

L’implémentation d’AEM Forms implique le déploiement des fichiers EAR assemblés et des fichiers de prise en charge sur le serveur d’applications sur lequel vous prévoyez d’exécuter votre solution AEM Forms. Si vous avez configuré et assemblé plusieurs modules, les modules déployables sont regroupés dans les fichiers EAR déployables. Pour déployer ces fichiers, copiez-les dans le répertoire *[appserver home]*\server\all\deploy.

Les modules et les fichiers d’archives AEM Forms sont regroupés dans des fichiers JAR. Comme il ne s’agit pas de fichiers de type J2EE, ils ne sont pas déployés sur le serveur d’applications. Au lieu de cela, ils sont copiés dans le répertoire GDS et une référence à leur emplacement est stockée dans la base de données AEM Forms. Pour cette raison, le répertoire GDS doit être partagé entre tous les nœuds du cluster. Tous les nœuds doivent avoir accès au répertoire de stockage central des DSC.

>[!NOTE]
>
>Avant de déployer les conteneurs de services, assurez-vous d’avoir créé et configuré le répertoire GDS. (Voir [Configuration du répertoire GDS](global-document-storage-directory.md#configuring-the-gds-directory))
