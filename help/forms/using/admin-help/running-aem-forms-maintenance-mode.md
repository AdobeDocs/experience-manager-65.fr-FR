---
title: Exécuter AEM Forms en mode de maintenance
description: Le mode de maintenance est utile lorsque vous réalisez des tâches telles que l’application d’un correctif à un DSC, la mise à niveau d’AEM forms ou l’application d’un Pack de services. Découvrez comment exécuter AEM Forms en mode de maintenance.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 6f5ce18b-26b4-4c31-b48a-43ccbb3912f6
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
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
source-wordcount: '259'
ht-degree: 100%
---
# Exécuter AEM Forms en mode de maintenance {#running-aem-forms-in-maintenance-mode}

Le mode de maintenance est utile lorsque vous réalisez des tâches telles que l’application d’un correctif à un DSC, la mise à niveau d’AEM forms ou l’application d’un Pack de services.

Évitez d’appeler des processus lorsque le serveur est en mode de maintenance. Voici en effet ce qui se produirait :

* S’il s’agit d’un processus de longue durée, il est ajouté à la base de données des tâches, mais pas démarré. Lorsque vous quittez le mode de maintenance, AEM Forms traite les travaux de longue durée présents dans sa file d’attente, même si le serveur a été redémarré alors qu’il se trouvait en mode de maintenance.
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

   Un message « maintenant en cours d’exécution » s’affiche dans la fenêtre du navigateur.
