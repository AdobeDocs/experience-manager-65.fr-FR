---
title: Principes de base de la configuration des formulaires
description: Découvrez les différents services de formulaires qui vous permettent de créer des applications interactives de capture de données.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 169f3d94-ac00-41c7-853e-ecf0dbee559f
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
source-wordcount: '200'
ht-degree: 100%
---
# Principes de base de la configuration des formulaires {#basics-of-configuring-forms}

Le service Forms vous permet de créer des applications clientes interactives de capture de données assurant la validation, le traitement, la transformation et la transmission de formulaires généralement créés dans Designer. Les créateurs et créatrices de formulaires développent une conception de formulaire unique que le service Forms rend dans différents formats :

* au format PDF dans Adobe Reader ou dans un navigateur ;
* au format HTML dans une multitude d’environnements de navigation, notamment le rendu compatible XHTML 1.0 ;
* sous forme de guides de formulaire dans divers environnements de navigation prenant en charge Adobe Flash Player.

Pour plus d’informations sur le service Forms, consultez [Guide de référence des services](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

La page Forms de la console d’administration vous permet de configurer le comportement du service Forms. Ces paramètres s’appliquent à tous les appels du service. Tous les paramètres envoyés par l’intermédiaire du SDK d’AEM Forms remplacent les paramètres définis dans la console d’administration ; toutefois, ils ne s’appliquent qu’à cet appel en particulier.

Après avoir modifié les paramètres de Forms dans la console d’administration, cliquez sur Enregistrer. Vous n’avez pas besoin de redémarrer le serveur pour que les modifications soient prises en compte. Cependant, il peut être nécessaire d’arrêter et de redémarrer le service Forms lors de la configuration des paramètres du mode de mise en cache. (voir [Démarrage et arrêt des services](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services)).
