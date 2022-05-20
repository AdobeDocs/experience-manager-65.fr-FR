---
title: Démarrage et arrêt des services
seo-title: Starting and stopping services
description: Découvrez comment démarrer et arrêter des services associés aux modules AEM Forms et au serveur d’applications et à la base de données.
seo-description: Learn how to start and stop services associated with AEM Forms modules and the application server and database.
uuid: 8c831cb2-4165-4118-8a09-764cec4e5e05
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_services
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b93060bd-c6e1-40d2-8acd-ccafb8ed56da
exl-id: 55bf5196-22c6-4286-8c92-ff44d81dde49
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '265'
ht-degree: 100%

---

# Démarrage et arrêt des services {#starting-and-stopping-services}

Il existe deux types de services faisant partie d’AEM Forms :

* Services qui contrôlent le serveur d’applications et la base de données AEM forms.
* Services qui contrôlent les modules AEM forms

## Démarrage ou arrêt des services associés aux modules AEM forms {#start-or-stop-the-services-associated-with-aem-forms-modules}

Les modules AEM forms (par exemple, Forms, Rights Management et Output) fonctionnent comme des services. Vous devrez parfois arrêter ou démarrer les services de ces modules AEM forms. Par exemple, vous devez arrêter puis redémarrer un service AEM forms après avoir procédé à une modification sur un paramètre de ce service.

1. Dans Console d’administration, cliquez sur **Services** > **Applications et services** > **Gestion des services**.
1. Dans la page Gestion des services, cochez la case en regard du service à arrêter ou démarrer et cliquez sur Arrêter ou Démarrer.

## Démarrage ou arrêt des services pour le serveur d’applications et la base de données {#start-or-stop-services-for-the-application-server-and-database}

Une implémentation complète d’AEM forms comprend des services de serveur d’applications et de base de données :

* *`[application server]`* pour AEM Forms
* *`[database]`* pour AEM Forms

Sous Windows, ces services sont accessibles dans **Outils d’administration** > **Panneau de services**. Par exemple, si vous avez installé AEM forms sur JBoss à l’aide de la méthode clé en main, les services suivants sont disponibles :

* JBoss pour Adobe Experience Manager forms
* MySQL pour Adobe Experience Manager forms

Pour démarrer ou arrêter un service, sélectionnez-le dans la liste, puis cliquez sur le bouton approprié dans le panneau.

Sous UNIX® ou Linux, saisissez le texte suivant à partir d’une ligne de commande, dans laquelle *`[service name]`* correspond au nom du service à vérifier :

```java
     ps -A | grep [service name]
```
