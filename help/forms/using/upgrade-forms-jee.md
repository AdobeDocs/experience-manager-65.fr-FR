---
title: Mise à niveau vers AEM 6.5 Forms
seo-title: Upgrade to AEM 6.5 Forms
description: Vous pouvez effectuer une mise à niveau directe à partir d’AEM 6.1 Forms, AEM 6.2 Forms et LiveCycle ES4 SP1 vers AEM 6.3 Forms.
seo-description: You can perform a direct upgrade from AEM 6.1 Forms, AEM 6.2 Forms, and LiveCycle ES4 SP1 to AEM 6.3 Forms.
uuid: 1435246a-9215-4d88-b52c-59a5c329bb77
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: e745033f-8015-4fae-9d82-99d35802c0a6
role: Admin
exl-id: 722e75a0-bcb3-465e-bb74-ea94a3b99fd3
source-git-commit: 2e6d688818e9cc337444bcda2a49485e9167a113
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 54%

---

# Mettre à niveau vers AEM 6.5 Forms on JEE {#upgrade-to-aem-forms-jee}

AEM 6.5.12.0 Forms on JEE fournit deux types d’installation : Programme d’installation complet et programme d’installation de correctif.

**Programme d’installation complet**: Vous pouvez utiliser la variable [Programme d’installation complet d’AEM 6.5.12.0 on JEE](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr) pour configurer de nouvelles instances AEM Forms ou effectuer des mises à niveau à partir d’AEM 6.3 Forms on JEE, AEM 6.4 on JEE et une mise à niveau dynamique d’Forms on JEE vers 6.5.x.x vers Forms on JEE.

**Programme d’installation des correctifs**: [Programme d’installation du correctif d’AEM 6.5.12.0 on JEE](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) est destiné aux clients qui utilisent déjà AEM versions 6.5.x.x. Vous pouvez utiliser le programme d’installation de correctif pour effectuer la mise à niveau vers la dernière version d’AEM Forms.

Le tableau suivant illustre les scénarios d’utilisation du programme d’installation complet et des correctifs.

![](assets/full-and-patch-installer.png)

Procédez comme suit pour utiliser le programme d’installation complet afin de mettre à niveau AEM version 6.3 Forms on JEE ou AEM 6.4 Forms on JEE vers la version 6.5.12.0 Forms on JEE :

1. Téléchargez le programme d’installation d’AEM 6.5 Forms on JEE à partir du [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). Vous avez besoin d’un contrat de maintenance et d’assistance valide pour utiliser le programme d’installation.
1. Voir [Aide-mémoire et planification de la mise à niveau](https://www.adobe.com/go/learn_aemforms_upgrade_checklist_65_fr) pour découvrir les vérifications à effectuer pour une mise à niveau réussie.
1. Voir [Préparation de la mise à niveau vers AEM Forms](https://www.adobe.com/go/learn_aemforms_prepareupgrade_65_fr) pour découvrir et exécuter les tâches permettant d’effectuer correctement la mise à niveau pour un temps d’arrêt du serveur minimal.
1. En fonction de votre environnement et de votre serveur d’application, sélectionnez l’un des documents suivants et suivez les instructions.

   * [Mise à niveau d’AEM 6.3 Forms ou d’AEM 6.4 Forms vers AEM 6.5 Forms pour JBoss](http://www.adobe.com/go/learn_aemforms_upgradeJBoss_65_fr)
   * [Mise à niveau d’AEM 6.3 Forms ou d’AEM 6.4 Forms vers AEM 6.5 Forms pour WebSphere](http://www.adobe.com/go/learn_aemforms_upgradeWebSphere_65_fr)
   * [Mise à niveau d’AEM 6.3 Forms ou d’AEM 6.4 Forms vers AEM 6.5 Forms pour JBoss clé en main](http://www.adobe.com/go/learn_aemforms_upgradeTurnkey_65_fr)

La mise à niveau directe de LiveCycle ES2, LiveCycle ES3, AEM 6.0 Forms, AEM 6.1 Forms et AEM 6.2 Forms vers AEM 6.5 Forms n’est pas disponible. Vous pouvez effectuer une mise à niveau intermédiaire vers une ou plusieurs versions de LiveCycle ou AEM Forms, puis effectuer la mise à niveau vers AEM 6.5 Forms. Pour la liste des versions intermédiaires et les instructions de mise à niveau correspondantes, voir [Sélectionner un chemin de mise à niveau](upgrade.md).
