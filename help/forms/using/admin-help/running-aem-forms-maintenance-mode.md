---
title: Exécution d’AEM Forms en mode de maintenance
seo-title: Exécution d’AEM Forms en mode de maintenance
description: Le mode de maintenance est utile lorsque vous réalisez des tâches telles que l’application d’un correctif à un DSC, la mise à niveau d’AEM forms ou l’application d’un Service Pack. Découvrez comment exécuter AEM Forms en mode de maintenance.
seo-description: Le mode de maintenance est utile lorsque vous réalisez des tâches telles que l’application d’un correctif à un DSC, la mise à niveau d’AEM forms ou l’application d’un Service Pack. Découvrez comment exécuter AEM Forms en mode de maintenance.
uuid: 9aa3be20-f17e-4384-b4ce-daaee2898c96
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 94047c12-ba3d-457a-954f-e035c7cc3ecd
exl-id: 6f5ce18b-26b4-4c31-b48a-43ccbb3912f6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 100%

---

# Exécution d’AEM Forms en mode de maintenance {#running-aem-forms-in-maintenance-mode}

Le mode de maintenance est utile lorsque vous réalisez des tâches telles que l’application d’un correctif à un DSC, la mise à niveau d&#39;AEM forms ou l’application d’un Service Pack.

Evitez d’appeler des processus lorsque le serveur est en mode de maintenance. Voici en effet ce qui se produirait :

* S’il s’agit d’un processus de longue durée, il est ajouté à la base de données des travaux, mais pas démarré. Lorsque vous quittez le mode de maintenance, AEM forms traite les travaux de longue durée présents dans sa file d’attente, même si le serveur a été redémarré alors qu’il se trouvait en mode de maintenance.
* S’il s’agit d’un processus de courte durée, il est immédiatement traité.

**Activation d’AEM Forms en mode de maintenance**

1. Dans un navigateur Web, entrez :

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=pause&user=[administrator username]&password=[password]`

   Un message de pause s’affiche dans la fenêtre du navigateur.

   >[!NOTE]
   >
   >Si vous arrêtez le serveur alors qu’il se trouve en mode de maintenance, il conservera ce mode au redémarrage. Vous devez désactiver le mode de maintenance une fois vos tâches de maintenance terminées.

**Vérifiez si AEM forms fonctionne en mode de maintenance**

1. Dans un navigateur Web, entrez :

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=isPaused&user=[administrator username]&password=[password]`

   L’état s’affiche dans la fenêtre du navigateur. L’état « true » indique que le serveur s’exécute en mode de maintenance et « false » que le serveur ne s’exécute pas dans ce mode.

**Désactivation du mode de maintenance**

1. Dans un navigateur Web, entrez :

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=resume&user=[administrator username]&password=[password]`

   Un message d’exécution s’affiche dans la fenêtre du navigateur.
