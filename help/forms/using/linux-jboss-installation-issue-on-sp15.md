---
title: Problème d’installation de l’AEM Forms JEE 6.5.15.0 Service Pack dans l’environnement JBoss® Linux®
description: L’AEM Forms JEE 6.5.15.0 Service Pack n’est pas installé correctement dans l’environnement JBoss® Linux®. Aucune modification de correctif n’est appliquée au serveur d’applications. Ajoutez le fichier RUP_BOM.xml au répertoire XML.
exl-id: 96ecbe58-a859-4432-a2d8-3d5dc0eaf989
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms on JEE
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 100%

---

# Problème d’installation de l’AEM Forms 6.5.15.0 JEE Service Pack sur l’environnement JBoss® {#aem-forms-installation-issue-environment}

## Problème {#issue}

L’AEM Forms JEE 6.5.15.0 Service Pack n’est pas installé correctement dans l’environnement JBoss® Linux®. Dans le fichier `PatchInstallerProcessing[1-9*].log`, l’entrée du journal, `[AEM_Forms_JEE_DIR]/patch/AEMForms-6.5.0-0057/xml/RUP_BOM.xml not found! Assuming this component is not in the installation. Skipping Processing`, est consignée. Cette entrée indique que l’installation de l’AEM Forms JEE 6.5.15.0 Service Pack échoue.

## Application {#applies-to}

Cette solution s’applique aux éléments suivants :
* Environnement JBoss® Linux®

>[!NOTE]
>
> Assurez-vous que l’AEM Forms JEE 6.5.15.0 Service Pck est installé au moins une fois sur le serveur d’applications avant d’exécuter les étapes d’[ajout du fichier RUP_BOM.xml au répertoire XML](#solution-solution).

## Solution {#solution}

Pour résoudre le problème d’installation de l’AEM Forms JEE 6.5.15.0 Service Pack, ajoutez le fichier `RUP_BOM.xml` au répertoire XML :
1. Accédez au dossier dans lequel vous avez extrait le correctif `AEMForms-6.5.0-0057_jboss_linux.tar.gz`.
1. Accédez à l’emplacement `/CDROM_Installers/Linux/Disk1/InstData` et localisez le fichier `Resource1.zip`.
1. Copiez le fichier `Resource1.zip` à un autre emplacement en dehors du dossier extrait et décompressez le fichier `Resource1.zip`.
1. Accédez à `/C_/builds/dev_releng/branches/rrt/aem6.5.0_rollup/tier1/install/patch/fileset_dir/xml` et copiez le fichier.`RUP_BOM.xml`.
1. Collez le fichier RUP_BOM.xml dans `[aem_forms_jee_installation_dir]/patch/AEMForms-6.5.0-0057/xml`.
1. Réinstallez l’[AEM Forms JEE 6.5.15.0 Service Pack](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr).
