---
title: Problème d’installation du Service Pack d’AEM Forms JEE 6.5.15.0 dans l’environnement JBoss® Linux®
description: Le Service Pack d’AEM Forms JEE 6.5.15.0 n’est pas installé correctement dans l’environnement JBoss® Linux®. Aucune modification de correctif n’est appliquée au serveur d’applications. Ajoutez le fichier RUP_BOM.xml au répertoire XML.
SEO Description: AEM Forms JEE 6.5.15.0 service pack  is not installed properly on the JBoss Linux environment.
exl-id: 96ecbe58-a859-4432-a2d8-3d5dc0eaf989
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms on JEE
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 94663796-0ee7-58b9-84f4-b425ebb69e83
    internal-label: AEM Forms on JEE
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 45%
---
# Problème d’installation du pack de services AEM Forms 6.5.15.0 JEE dans l’environnement JBoss® {#aem-forms-installation-issue-environment}

## Problème {#issue}

Le Service Pack d’AEM Forms JEE 6.5.15.0 n’est pas installé correctement dans l’environnement JBoss® Linux®. Dans le fichier `PatchInstallerProcessing[1-9*].log`, l’entrée du journal, `[AEM_Forms_JEE_DIR]/patch/AEMForms-6.5.0-0057/xml/RUP_BOM.xml not found! Assuming this component is not in the installation. Skipping Processing`, est consignée. Cette entrée indique que l’installation du pack de services d’AEM Forms JEE 6.5.15.0 échoue.

## Application {#applies-to}

Cette solution s’applique aux éléments suivants :
* Environnement JBoss® Linux®

>[!NOTE]
>
> Assurez-vous que l’AEM Forms JEE 6.5.15.0 Service Pack est installé au moins une fois sur le serveur d’applications avant d’exécuter les étapes d’[ajout du fichier RUP_BOM.xml au répertoire XML](#solution-solution).

## Solution {#solution}

Pour résoudre le problème d’installation du pack de services 6.5.15.0 AEM Forms JEE, ajoutez le fichier `RUP_BOM.xml` au répertoire XML :
1. Accédez au dossier dans lequel vous avez extrait le correctif `AEMForms-6.5.0-0057_jboss_linux.tar.gz`.
1. Accédez à l’emplacement `/CDROM_Installers/Linux/Disk1/InstData` et localisez le fichier `Resource1.zip`.
1. Copiez le fichier `Resource1.zip` à un autre emplacement en dehors du dossier extrait et décompressez le fichier `Resource1.zip`.
1. Accédez à `/C_/builds/dev_releng/branches/rrt/aem6.5.0_rollup/tier1/install/patch/fileset_dir/xml` et copiez le fichier.`RUP_BOM.xml`.
1. Collez le fichier RUP_BOM.xml dans `[aem_forms_jee_installation_dir]/patch/AEMForms-6.5.0-0057/xml`.
1. Réinstallez le [pack de services 6.5.15.0 AEM Forms JEE](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr).
