---
title: Principes de base des formulaires de configuration
seo-title: Principes de base des formulaires de configuration
description: Découvrez les différents services de formulaires qui vous aideront à créer des applications interactives de capture de données.
seo-description: Découvrez les différents services de formulaires qui vous aideront à créer des applications interactives de capture de données.
uuid: f495c170-2d17-45b0-b09d-22cce101131e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e87c7379-28ed-4fda-aef1-970d2b54f30d
exl-id: 169f3d94-ac00-41c7-853e-ecf0dbee559f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 97%

---

# Principes de base des formulaires de configuration {#basics-of-configuring-forms}

Le service Forms vous permet de créer des applications clientes interactives de capture de données assurant la validation, le traitement, la transformation et la transmission de formulaires généralement créés dans Designer. Les auteurs de formulaires développent une conception de formulaire simple que le service Forms rend sous diverses formes :

* au format PDF dans Adobe Reader ou dans un navigateur ;
* au format HTML dans une multitude d’environnements de navigation, notamment le rendu compatible XHTML 1.0 ;
* sous forme de guides de formulaire dans une multitude d’environnements de navigation prenant en charge Adobe Flash Player.

Pour plus d’informations sur le service Forms, voir le [Guide de référence des services](https://www.adobe.com/go/learn_aemforms_services_63).

A la page Forms d’Administration Console, vous pouvez configurer le comportement du service Forms. Ces paramètres s’appliquent à tous les appels du service. Tous les paramètres envoyés à l’aide du SDK d’AEM forms remplacent les paramètres définis dans Administration Console ; toutefois, ils s’appliquent uniquement à cet appel.

Après avoir modifié les paramètres de Forms dans Administration Console, cliquez sur Enregistrer. Vous n’avez pas besoin de redémarrer le serveur pour que les modifications prennent effet. Cependant, il est parfois nécessaire de redémarrer le service Forms lors de la configuration des paramètres du mode de mise en cache (voir [Démarrage et arrêt des services](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services)).
