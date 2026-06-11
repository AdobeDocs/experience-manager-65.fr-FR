---
title: Mise à niveau de JBoss EAP de la version 7.4.10 vers la version 7.4.23 pour AEM Forms sur JEE
description: Étapes de mise à niveau de JBoss EAP de la version 7.4.10 vers la version 7.4.23 pour les environnements autonomes AEM Forms on JEE.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
exl-id: 8f4c2a91-6b3d-4e7f-9c12-5d8e1f0a2b34
solution: Experience Manager, Experience Manager Forms
feature: AEM Forms Upgrade,AEM Forms on JEE
role: User, Developer
source-git-commit: cb190feb41152d40c36ea2f152ee04cc8c8eba1d
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 1%

---

# Mise à niveau de JBoss EAP de la version 7.4.10 vers la version 7.4.23 pour AEM Forms sur JEE {#upgrade-jboss-eap-from-7-4-10-to-7-4-23}

## Vue d’ensemble {#overview}

Mettez à niveau JBoss EAP de la version 7.4.10 vers la version 7.4.23 sur un environnement autonome AEM Forms on JEE. La mise à niveau nécessite la migration des fichiers de configuration, des informations d’identification de la base de données et du référentiel CRX vers la nouvelle installation de JBoss, ainsi que l’exécution de Configuration Manager pour terminer la configuration.

## Application {#applies-to}

Cet article s’applique aux éléments suivants :

* AEM Forms on JEE s’exécutant sur JBoss EAP 7.4.10 dans un environnement autonome
* Modes d’installation clé en main et clé en main partielle sous Windows et Linux

## Conditions préalables {#prerequisites}

Avant de commencer :

* Téléchargez le package JBoss 7.4.23 à partir du portail de distribution de logiciels [](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fjboss-eap-7.4.23-1.0.17.zip).
* Vérifiez que vous disposez d’un accès administratif à l’environnement cible.
* Effectuez une sauvegarde complète de l’installation de JBoss existante.

## Étapes {#steps}

Pour mettre à niveau JBoss EAP de la version 7.4.10 vers la version 7.4.23, procédez comme suit :

### Télécharger et extraire JBoss {#download-and-extract-jboss}

1. Téléchargez le package JBoss 7.4.23 ZIP à partir du portail de distribution logicielle d’Adobe.
1. Extrayez le fichier ZIP dans un répertoire local.
1. Renommez le dossier JBoss extrait pour qu’il corresponde au nom exact du répertoire d’installation de JBoss existant.

### Sauvegarde de l’installation existante {#back-up-the-existing-installation}

1. Créez une sauvegarde complète du répertoire d’installation actuel de JBoss.
1. Vérifiez que la sauvegarde inclut tous les fichiers de configuration et personnalisations.

### Configuration des fichiers de base de données {#configure-database-files}

1. Accédez au répertoire de configuration :

   * Windows : `<JBoss_Home>\standalone\configuration`
   * Linux : `<JBoss_Home>/standalone/configuration`

1. Configurez les fichiers de base de données en fonction de votre mode d’installation :

   **Mode clé en main :**

   1. Renommez `lc_mysql.xml` en `lc_turnkey.xml`.
   1. Supprimez les fichiers suivants :

      * `lc_oracle.xml`
      * `lc_mssql.xml`

   **Mode clé en main partielle :**

   1. Conservez uniquement le fichier `lc_db.xml` correspondant à votre moteur de base de données.
   1. Supprimez les deux autres fichiers de configuration `lc_db.xml`.

### Mise à jour des informations d’identification de la base de données {#update-database-credentials}

1. Ouvrez le fichier `lc_turnkey.xml` à partir de l’installation JBoss sauvegardée.
1. Copiez les valeurs suivantes :

   * URL de la source de données
   * Nom d&#39;utilisateur de la base de données
   * Mot de passe de la base de données

1. Mettez à jour les entrées correspondantes dans le nouveau fichier `lc_turnkey.xml`.

### Migration du référentiel CRX {#migrate-crx-repository}

1. Accédez au répertoire suivant dans l’ancienne installation de JBoss :

   `<old_jboss>\bin\`

1. Copiez le dossier `crx-quickstart`.
1. Collez le dossier dans :

   `<new_jboss>\bin\`

### Exécuter Configuration Manager {#run-configuration-manager}

1. Démarrez l’environnement JBoss mis à niveau.
1. Lancez LiveCycle Configuration Manager (LCM).
1. Exécutez le workflow complet de Configuration Manager .
1. Vérifiez que toutes les tâches de configuration sont terminées.

### Validation après mise à niveau {#post-upgrade-validation}

Après la mise à niveau, confirmez les éléments suivants :

* Tous les services ont démarré avec succès.
* La connectivité de la base de données est vérifiée.
* La fonctionnalité de l’application est validée.
