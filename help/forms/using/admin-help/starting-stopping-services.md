---
title: Démarrage et arrêt des services
seo-title: Démarrage et arrêt des services
description: Découvrez comment démarrer et arrêter des services associés aux modules AEM Forms et au serveur d’applications et à la base de données.
seo-description: Découvrez comment démarrer et arrêter des services associés aux modules AEM Forms et au serveur d’applications et à la base de données.
uuid: 8c831cb2-4165-4118-8a09-764cec4e5e05
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_services
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b93060bd-c6e1-40d2-8acd-ccafb8ed56da
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 82%

---


# Démarrage et arrêt des services {#starting-and-stopping-services}

Il existe deux types de services faisant partie d’AEM Forms :

* Services qui contrôlent le serveur d’applications et la base de données AEM forms.
* Services qui contrôlent les modules AEM forms

## Démarrage ou arrêt des services associés aux modules AEM forms {#start-or-stop-the-services-associated-with-aem-forms-modules}

Les modules AEM forms (par exemple, Forms, Rights Management et Output) fonctionnent comme des services. Vous devrez parfois arrêter ou démarrer les services de ces modules AEM forms. Par exemple, vous devez arrêter puis redémarrer un service AEM forms après avoir procédé à une modification sur un paramètre de ce service.

1. Dans Administration Console, cliquez sur **Services** > **Applications et services** > **Gestion des services**.
1. Dans la page Gestion des services, cochez la case en regard du service à arrêter ou démarrer et cliquez sur Arrêter ou Démarrer.

## Démarrage ou arrêt des services pour le serveur d’applications et la base de données  {#start-or-stop-services-for-the-application-server-and-database}

Une implémentation complète d’AEM forms comprend des services de serveur d’applications et de base de données :

* *`[application server]`* pour les formulaires AEM
* *`[database]`* pour les formulaires AEM

Sous Windows, ces services sont accessibles via le **panneau** Outils d’administration > **Services**. Par exemple, si vous avez installé AEM forms sur JBoss à l’aide de la méthode clé en main, les services suivants sont disponibles :

* JBoss pour Adobe Experience Manager forms
* MySQL pour Adobe Experience Manager forms

Pour démarrer ou arrêter un service, sélectionnez-le dans la liste, puis cliquez sur le bouton approprié dans le panneau.

Sous UNIX® ou Linux, saisissez le texte suivant à partir d’une ligne de commande, où *`[service name]`* est le nom du service que vous vérifiez :

```java
     ps -A | grep [service name]
```

