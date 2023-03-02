---
title: Problème d’installation du Service Pack AEM Forms JEE 6.5.15.0 dans l’environnement JBoss® Linux®
description: Le Service Pack d’AEM Forms JEE 6.5.15.0 n’est pas installé correctement dans l’environnement JBoss® Linux®. Aucune modification de correctif n’est appliquée au serveur d’applications. Ajoutez le fichier RUP_BOM.xml dans le répertoire XML.
source-git-commit: 76a3a87408ceb13023737379c20fb44ce5fb180a
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 7%

---


# Problème d’installation du Service Pack d’AEM Forms 6.5.15.0 JEE sur l’environnement JBoss® {#aem-forms-installation-issue-environment}

## Problème {#issue}

Le Service Pack d’AEM Forms JEE 6.5.15.0 n’est pas installé correctement dans l’environnement JBoss® Linux®. Dans `PatchInstallerProcessing[1-9*].log` enregistrer l&#39;entrée du journal, `[AEM_Forms_JEE_DIR]/patch/AEMForms-6.5.0-0057/xml/RUP_BOM.xml not found! Assuming this component isn't in the installation. Skipping Processing`, est consigné. Cette entrée indique que l’installation du Service Pack AEM Forms JEE 6.5.15.0 échoue.

## Application {#applies-to}

Cette solution s’applique aux éléments suivants :
* Environnement JBoss® Linux®

>[!NOTE]
>
> Assurez-vous que le Service Pack d’AEM Forms JEE 6.5.15.0 est installé au moins une fois sur le serveur d’applications avant d’exécuter les étapes de [Ajout du fichier RUP_BOM.xml dans le répertoire XML](#solution-solution).

## Solution {#solution}

Pour résoudre le problème d’installation, ajoutez le service pack AEM Forms JEE 6.5.15.0. `RUP_BOM.xml` dans le répertoire XML :
1. Accédez au dossier dans lequel vous avez extrait le correctif. `AEMForms-6.5.0-0057_jboss_linux.tar.gz`.
1. Accédez à `/CDROM_Installers/Linux/Disk1/InstData` emplacement et localisez la variable `Resource1.zip` fichier .
1. Copiez le `Resource1.zip` fichier à un autre emplacement en dehors du dossier extrait et décompressez-le. `Resource1.zip` fichier .
1. Accédez à `/C_/builds/dev_releng/branches/rrt/aem6.5.0_rollup/tier1/install/patch/fileset_dir/xml` et copiez la variable `RUP_BOM.xml` fichier .
1. Collez le fichier RUP_BOM.xml dans `[aem_forms_jee_installation_dir]/patch/AEMForms-6.5.0-0057/xml`.
1. Réinstallez les [Service Pack AEM Forms JEE 6.5.15.0](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr).