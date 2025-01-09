---
title: Démarrer et arrêter des services
description: Découvrez comment démarrer et arrêter des services associés aux modules AEM Forms et au serveur d’applications et à la base de données.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_services
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 55bf5196-22c6-4286-8c92-ff44d81dde49
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '311'
ht-degree: 100%

---

# Démarrer et arrêter des services {#starting-and-stopping-services}

>[!NOTE]
> 
> Vérifiez que l’utilisateur ou l’utilisatrice dispose de droits d’administration pour accéder à la console d’administration.

Il existe deux types de services faisant partie d’AEM Forms :

* Services qui contrôlent le serveur d’applications et la base de données AEM Forms.
* Services qui contrôlent les modules AEM Forms.

## Démarrer ou arrêter des services associés aux modules AEM Forms {#start-or-stop-the-services-associated-with-aem-forms-modules}

Les modules AEM Forms (par exemple, Forms, Rights Management et Output) fonctionnent comme des services. Vous devrez parfois arrêter ou démarrer les services de ces modules AEM Forms. Par exemple, vous devez arrêter puis redémarrer un service AEM Forms après avoir procédé à une modification sur un paramètre de ce service.

>[!NOTE]
>
> Il est recommandé d’utiliser la commande « Ctrl+C » pour redémarrer le SDK. Le redémarrage du SDK AEM à l’aide de méthodes alternatives, par exemple l’arrêt des processus Java, peut entraîner des incohérences dans l’environnement de développement AEM.

1. Dans Console d’administration, cliquez sur **Services** > **Applications et services** > **Gestion des services**.
1. Dans la page Gestion des services, cochez la case en regard du service à arrêter ou à démarrer et cliquez sur Arrêter ou Démarrer.

## Démarrer ou arrêter des services pour le serveur d’applications et la base de données {#start-or-stop-services-for-the-application-server-and-database}

Une implémentation complète d’AEM Forms comprend des services de serveur d’applications et de base de données :

* *`[application server]`* pour AEM Forms
* *`[database]`* pour AEM Forms

Sous Windows, ces services sont accessibles dans **Outils d’administration** > **Panneau de services**. Par exemple, si vous avez installé AEM Forms sur JBoss à l’aide de la méthode clé en main, les services suivants sont disponibles :

* JBoss pour Adobe Experience Manager Forms
* MySQL pour Adobe Experience Manager Forms

Pour démarrer ou arrêter un service, sélectionnez-le dans la liste, puis cliquez sur le bouton approprié dans le panneau.

Sous UNIX® ou Linux, saisissez le texte suivant à partir d’une ligne de commande, dans laquelle *`[service name]`* correspond au nom du service à vérifier :

```java
     ps -A | grep [service name]
```
