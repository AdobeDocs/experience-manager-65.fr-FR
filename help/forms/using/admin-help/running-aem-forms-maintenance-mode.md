---
title: Exécuter AEM Forms en mode de maintenance
description: Le mode de maintenance est utile lorsque vous réalisez des tâches telles que l’application d’un correctif à un DSC, la mise à niveau d’AEM forms ou l’application d’un pack de services. En savoir plus sur l’exécution AEM forms en mode de maintenance.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 6f5ce18b-26b4-4c31-b48a-43ccbb3912f6
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 24%

---

# Exécuter AEM Forms en mode de maintenance {#running-aem-forms-in-maintenance-mode}

Le mode de maintenance est utile lorsque vous réalisez des tâches telles que l’application d’un correctif à un DSC, la mise à niveau d’AEM forms ou l’application d’un Service Pack.

Évitez d’appeler des processus lorsque le serveur est en mode de maintenance. Voici ce qui se passe si un processus est appelé alors que le serveur est en mode de maintenance :

* Si le processus est de longue durée, il est ajouté à la base de données de tâches, mais n’est pas démarré. Lorsque vous quittez le mode de maintenance, AEM forms traite les tâches de longue durée dans sa file d’attente, même si le serveur a été redémarré en mode de maintenance.
* Si le processus est de courte durée, il est traité immédiatement.

**Activation des AEM forms en mode de maintenance**

1. Dans un navigateur web, saisissez :

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=pause&user=[administrator username]&password=[password]`

   Un message &quot;maintenant en pause&quot; s’affiche dans la fenêtre du navigateur.

   >[!NOTE]
   >
   >Si vous arrêtez le serveur alors qu’il est en mode de maintenance, il reste en mode de maintenance au redémarrage. Désactivez le mode de maintenance lorsque vous avez terminé vos tâches de maintenance.

**Vérifiez si AEM forms s’exécute en mode de maintenance**

1. Dans un navigateur web, saisissez :

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=isPaused&user=[administrator username]&password=[password]`

   L’état s’affiche dans la fenêtre du navigateur. L’état &quot;true&quot; indique que le serveur s’exécute en mode de maintenance et &quot;false&quot; que le serveur n’est pas en mode de maintenance.

**Désactivation du mode de maintenance**

1. Dans un navigateur web, saisissez :

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=resume&user=[administrator username]&password=[password]`

   Un message d’exécution s’affiche dans la fenêtre du navigateur.
