---
title: Principes de base de la configuration des formulaires
description: Découvrez les différents services de formulaires qui vous aident à créer des applications de capture de données interactives.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 169f3d94-ac00-41c7-853e-ecf0dbee559f
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 4%

---

# Principes de base de la configuration des formulaires {#basics-of-configuring-forms}

Le service Forms vous permet de créer des applications clientes interactives de capture de données qui valident, traitent, transforment et diffusent des formulaires généralement créés dans Designer. Les auteurs de formulaires développent une conception de formulaire unique que le service Forms effectue dans différents formats :

* comme PDF dans Adobe Reader ou dans un navigateur
* comme HTML dans divers environnements de navigateur, y compris le rendu conforme XHTML 1.0
* comme guides de formulaire dans divers environnements de navigateur qui prennent en charge le Flash Player des Adobes.

Pour plus d’informations sur le service Forms, voir [Référence des services](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

La page Forms d’Administration Console vous permet de configurer le comportement du service Forms. Ces paramètres s’appliquent à tous les appels du service. Tous les paramètres envoyés par l’intermédiaire du SDK d’AEM forms remplacent les paramètres définis dans la console d’administration ; toutefois, ils n’affectent que cet appel particulier.

Après avoir modifié les paramètres Forms dans Administration Console, cliquez sur Enregistrer. Vous n’avez pas besoin de redémarrer le serveur pour que les modifications soient prises en compte. Cependant, vous devrez peut-être arrêter et redémarrer le service Forms lors de la configuration des paramètres du mode de mise en cache. (Voir [Démarrage et arrêt des services](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services).)
