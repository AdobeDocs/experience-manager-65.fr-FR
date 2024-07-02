---
title: Exécuter AEM Forms en mode de maintenance
description: Le mode de maintenance est utile lorsque vous réalisez des tâches telles que l’application d’un correctif à un DSC, la mise à niveau d’AEM forms ou l’application d’un pack de services. Découvrez comment exécuter AEM Forms en mode de maintenance.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 6f5ce18b-26b4-4c31-b48a-43ccbb3912f6
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: ht
source-wordcount: '256'
ht-degree: 100%

---

# Exécuter AEM Forms en mode de maintenance {#running-aem-forms-in-maintenance-mode}

Le mode de maintenance est utile lorsque vous réalisez des tâches telles que l’application d’un correctif à un DSC, la mise à niveau d’AEM forms ou l’application d’un Service Pack.

Évitez d’appeler des processus lorsque le serveur est en mode de maintenance. Voici en effet ce qui se produirait :

* S’il s’agit d’un processus de longue durée, il est ajouté à la base de données des travaux, mais pas démarré. Lorsque vous quittez le mode de maintenance, AEM Forms traite les travaux de longue durée présents dans sa file d’attente, même si le serveur a été redémarré alors qu’il se trouvait en mode de maintenance.
* S’il s’agit d’un processus de courte durée, il est immédiatement traité.

**Activation d’AEM Forms en mode de maintenance**

1. Dans un navigateur web, saisissez :

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=pause&user=[administrator username]&password=[password]`

   Un message de pause s’affiche dans la fenêtre du navigateur.

   >[!NOTE]
   >
   >Si vous arrêtez le serveur alors qu’il se trouve en mode de maintenance, il reste en mode de maintenance au redémarrage. Désactivez le mode de maintenance lorsque vous avez terminé vos tâches de maintenance.

**Vérification de l’exécution d’AEM Forms en mode de maintenance**

1. Dans un navigateur web, saisissez :

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=isPaused&user=[administrator username]&password=[password]`

   Le statut s’affiche dans la fenêtre du navigateur. Le statut « true » indique que le serveur s’exécute en mode de maintenance et « false » que le serveur n’est pas en mode de maintenance.

**Désactivation du mode de maintenance**

1. Dans un navigateur web, saisissez :

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=resume&user=[administrator username]&password=[password]`

   Un message d’exécution s’affiche dans la fenêtre du navigateur.
