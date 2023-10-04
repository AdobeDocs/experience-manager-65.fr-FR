---
title: Démarrer et arrêter des services
description: Découvrez comment démarrer et arrêter les services associés aux modules AEM Forms et au serveur applicatif et à la base de données.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_services
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 55bf5196-22c6-4286-8c92-ff44d81dde49
source-git-commit: 5bdf42d1ce7b2126bfb2670049deec4b6eaedba2
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 26%

---

# Démarrer et arrêter des services {#starting-and-stopping-services}

Il existe deux types de services faisant partie d’AEM Forms :

* Services qui contrôlent le serveur d’applications et la base de données d’AEM forms.
* Services qui contrôlent les modules d’AEM forms

## Démarrage ou arrêt des services associés aux modules d’AEM forms {#start-or-stop-the-services-associated-with-aem-forms-modules}

Les modules de formulaires AEM (par exemple, Forms, Rights Management, Output) fonctionnent comme des services. Parfois, vous devrez peut-être arrêter ou démarrer les services pour ces modules d’AEM forms. Par exemple, vous devez arrêter, puis redémarrer un service d’AEM forms après avoir modifié un paramètre du service.

1. Dans Console d’administration, cliquez sur **Services** > **Applications et services** > **Gestion des services**.
1. Sur la page Gestion des services, cochez la case en regard du service à arrêter ou à démarrer, puis cliquez sur Arrêter ou Démarrer.

## Démarrage ou arrêt des services pour le serveur d’applications et la base de données {#start-or-stop-services-for-the-application-server-and-database}

Une mise en oeuvre complète d’AEM forms comprend un serveur d’applications et des services de base de données :

* *`[application server]`* pour AEM Forms
* *`[database]`* pour AEM Forms

Sous Windows, ces services sont accessibles dans **Outils d’administration** > **Panneau de services**. Par exemple, si vous avez installé AEM forms on JBoss à l’aide de la méthode clé en main, les services suivants sont disponibles sur votre système :

* JBoss pour les formulaires Adobe Experience Manager
* MySQL pour les formulaires Adobe Experience Manager

Démarrez ou arrêtez ces services en les sélectionnant dans la liste du panneau Services , puis en cliquant sur le bouton d’action approprié dans le panneau.

Sous UNIX® ou Linux, saisissez le texte suivant à partir d’une ligne de commande, dans laquelle *`[service name]`* correspond au nom du service à vérifier :

```java
     ps -A | grep [service name]
```
