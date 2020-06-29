---
title: Création D’Un Sandbox SCF
seo-title: Création D’Un Sandbox SCF
description: Ce didacticiel s’adresse principalement aux développeurs, nouveaux utilisateurs d’AEM, qui souhaitent utiliser des composants SCF.  Il passe en revue la création du site An SCF Sandbox
seo-description: Ce didacticiel s’adresse principalement aux développeurs, nouveaux utilisateurs d’AEM, qui souhaitent utiliser des composants SCF.  Il passe en revue la création du site An SCF Sandbox
uuid: ee52e670-e1e6-4bcd-9548-c963142e6704
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: e1b5c25d-cbdd-421c-b81a-feb6039610a3
translation-type: tm+mt
source-git-commit: 342e148ba183782e4c8b0f08328b9d87685ca08e
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 2%

---



# Création D’Un Sandbox SCF  {#create-an-scf-sandbox}


Depuis les communautés AEM 6.1, le moyen le plus simple de créer rapidement un sandbox consiste à créer un site communautaire. See [Getting Started with AEM Communities](getting-started.md).

Un autre outil utile pour les développeurs est le guide [des composants](components-guide.md)communautaires, qui permet d&#39;explorer et de prototyper rapidement les composants et les fonctionnalités des communautés.

L’exercice de création d’un site Web peut s’avérer utile pour comprendre la structure d’un site Web AEM qui peut inclure des fonctionnalités de communautés, tout en fournissant des pages simples sur lesquelles explorer l’utilisation du cadre de composants [sociaux (SCF)](scf.md).

Ce didacticiel s’adresse principalement aux développeurs, nouveaux utilisateurs d’AEM, qui souhaitent utiliser des composants SCF. Il passe en revue la création d&#39;un site de sandbox SCF, semblable au tutoriel [How to Create a Fully Featured Internet Website](../../help/sites-developing/website.md) qui se concentre sur les structures du site, telles que la navigation, le logo, la recherche, la barre d&#39;outils et la liste des pages enfants.

Le développement a lieu sur une instance d’auteur, tandis que l’expérimentation du site est préférable sur une instance de publication.

Les étapes de ce didacticiel sont les suivantes :

* [Configurer la structure du site Web](setup-website.md)
* [Application Sandbox initiale](initial-app.md)
* [Contenu initial du sandbox](initial-content.md)
* [Développement d’une application Sandbox](develop-app.md)
* [Ajouter des bibliothèques clientes](add-clientlibs.md)
* [Développement du contenu du sandbox](develop-content.md)

>[!CAUTION]
>
>Ce didacticiel ne crée pas de site communautaire avec la fonctionnalité créée à l&#39;aide de la console [Sites](sites-console.md)communautés. Par exemple, ce didacticiel ne décrit pas comment configurer la connexion, l’auto-inscription, la connexion [](social-login.md)sociale, la messagerie, les profils, etc.
>
>Si vous préférez un site communautaire simple, suivez le didacticiel [Créer un exemple de page](create-sample-page.md) .

## Conditions préalables {#prerequisites}

Ce didacticiel suppose que vous avez installé un auteur AEM et une instance de publication AEM qui disposent de la [dernière version](deploy-communities.md#latest-releases) des communautés.

Voici quelques liens utiles pour les développeurs qui découvrent la plate-forme AEM :

* [Prise en main](../../help/sites-deploying/deploy.md#getting-started): pour le déploiement des instances AEM.

   * [Les bases](../../help/sites-developing/the-basics.md): pour les développeurs de sites Web et de fonctionnalités.
   * [Premières étapes pour les auteurs](../../help/sites-authoring/first-steps.md): pour la création de contenu de page.

## Utilisation de l’Environnement de développement CRXDE Lite {#using-crxde-lite-development-environment}

Les développeurs AEM passent la plupart de leur temps dans l’environnement de développement [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) sur une instance d’auteur. CRXDE Lite fournit un accès moins restreint au référentiel CRX. Les outils d’interface utilisateur classiques et les consoles d’interface utilisateur tactiles offrent un accès plus structuré à des portions spécifiques du référentiel CRX.

Après la connexion avec des droits d’administrateur, il existe plusieurs façons d’accéder à CRXDE Lite :

1. Dans la navigation globale, sélectionnez **[!UICONTROL Outils de navigation > CRXDE Lite]**.

   ![chlimage_1-350](assets/chlimage_1-350.png)

2. Dans la page [de bienvenue de l’interface utilisateur](http://localhost:4502/welcome.html)classique, faites défiler la page vers le bas et cliquez sur **[!UICONTROL CRXDE Lite]** dans le panneau de droite.

   ![chlimage_1-351](assets/chlimage_1-351.png)

3. Accédez directement à `CRXDE Lite`: `<server>:<port>/crx/de`

   Par exemple, sur une instance d’auteur locale : [http://localhost:4502/crx/de](http://localhost:4502/crx/de)

Pour travailler avec CRXDE Lite, vous devez vous connecter avec des privilèges de développeur ou d’administrateur. Pour l’instance localhost par défaut, vous pouvez vous connecter avec

* `username: admin`
* `password: admin`


**Sachez** que cette ouverture de session va expirer et que vous devrez vous reconnecter régulièrement à l’aide de la liste déroulante située à droite de la barre d’outils CRXDe Lite.

Si vous n’êtes pas connecté, vous ne pourrez pas parcourir le référentiel JCR ou effectuer des opérations de modification/enregistrement.

***En cas de doute, reconnectez-vous !***

![chlimage_1-352](assets/chlimage_1-352.png)
