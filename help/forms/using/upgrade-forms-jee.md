---
title: Mettre à niveau vers AEM 6.5 Forms sur JEE
description: Vous pouvez effectuer une mise à niveau directe à partir d’AEM 6.1 Forms, AEM 6.2 Forms et LiveCycle ES4 SP1 vers AEM 6.3 Forms.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
role: Admin
exl-id: 722e75a0-bcb3-465e-bb74-ea94a3b99fd3
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 95%

---

# Mettre à niveau vers AEM 6.5 Forms on JEE {#upgrade-to-aem-forms-jee}

AEM 6.5.18.0 Forms on JEE fournit deux types d’installation : programme d’installation complet et programme d’installation des correctifs.

**Programme d’installation complet** : vous pouvez utiliser le [programme d’installation complet d’AEM 6.5.18.0 on JEE](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr) pour configurer de nouvelles instances AEM Forms ou effectuer des mises à niveau à partir d’AEM 6.5.x.x Forms on JEE vers AEM 6.5.18.0 Forms on JEE.

**Programme d’installation de correctifs** : le [programme d’installation de correctifs d’AEM 6.5.18.0 on JEE](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr) s’adresse aux personnes qui utilisent déjà les versions AEM 6.5.x.x. Vous pouvez utiliser le programme d’installation des correctifs pour effectuer la mise à niveau vers la dernière version d’AEM Forms.

Le tableau suivant illustre les scénarios d’utilisation du programme d’installation complet et de correctifs.

![Scénario de programme d’installation complet et de correctifs](assets/full-and-patch-installer.png)

Effectuez la procédure suivante pour utiliser le programme d’installation complet pour mettre à niveau AEM Forms 6.5.x.x on JEE vers AEM 6.5.18.0 Forms on JEE :

1. Téléchargez le programme d’installation d’AEM 6.5 Forms on JEE à partir de la [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). Pour télécharger le programme d’installation, vous devez disposer d’un contrat de Maintenance &amp; Support.
1. Voir [Aide-mémoire et planification de la mise à niveau](https://www.adobe.com/go/learn_aemforms_upgrade_checklist_65_fr) pour découvrir les vérifications à effectuer pour une mise à niveau réussie.
1. Voir [Préparation de la mise à niveau vers AEM Forms](https://www.adobe.com/go/learn_aemforms_prepareupgrade_65_fr) pour découvrir et exécuter les tâches permettant d’effectuer correctement la mise à niveau pour un temps d’arrêt du serveur minimal.
1. En fonction de votre environnement et de votre serveur d’application, sélectionnez l’un des documents suivants et suivez les instructions.

   * [Mise à niveau d’AEM 6.3 Forms ou d’AEM 6.4 Forms vers AEM 6.5 Forms pour JBoss](https://www.adobe.com/go/learn_aemforms_upgradeJBoss_65_fr)
   * [Mise à niveau d’AEM 6.3 Forms ou d’AEM 6.4 Forms vers AEM 6.5 Forms pour WebSphere](https://www.adobe.com/go/learn_aemforms_upgradeWebSphere_65_fr)
   * [Mise à niveau d’AEM 6.3 Forms ou d’AEM 6.4 Forms vers AEM 6.5 Forms pour JBoss clé en main](https://www.adobe.com/go/learn_aemforms_upgradeTurnkey_65_fr)

La mise à niveau directe de LiveCycle ES2, LiveCycle ES3, AEM 6.0 Forms, AEM 6.1 Forms et AEM 6.2 Forms vers AEM 6.5 Forms n’est pas disponible. Vous pouvez effectuer une mise à niveau intermédiaire vers une ou plusieurs versions de LiveCycle ou AEM Forms, puis effectuer une mise à niveau vers AEM 6.5 Forms. Pour la liste des versions intermédiaires et les instructions de mise à niveau correspondantes, voir [Sélectionner un chemin de mise à niveau](upgrade.md).
