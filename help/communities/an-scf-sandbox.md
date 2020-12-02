---
title: Création D’Un Sandbox SCF
seo-title: Création D’Un Sandbox SCF
description: Ce tutoriel s'adresse principalement aux développeurs, nouveaux et AEM, qui s'intéressent à l'utilisation des composants SCF.  Il passe en revue la création du site An SCF Sandbox
seo-description: Ce tutoriel s'adresse principalement aux développeurs, nouveaux et AEM, qui s'intéressent à l'utilisation des composants SCF.  Il passe en revue la création du site An SCF Sandbox
uuid: ee52e670-e1e6-4bcd-9548-c963142e6704
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: e1b5c25d-cbdd-421c-b81a-feb6039610a3
translation-type: tm+mt
source-git-commit: 548e19b0fc76ede8685ea938ed871fbdc8c3858f
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 1%

---



# Créer Un Sandbox SCF {#create-an-scf-sandbox}


AEM 6.1 Collectivités, le moyen le plus simple de créer rapidement un sandbox est de créer un site communautaire. Voir [Prise en main de AEM Communities](getting-started.md).

Un autre outil utile pour les développeurs est le [Guide des composants de la communauté](components-guide.md), qui permet d&#39;explorer et de prototyper rapidement les composants et fonctionnalités de la communauté.

L&#39;exercice de création d&#39;un site Web peut s&#39;avérer utile pour comprendre la structure d&#39;un site Web AEM qui peut inclure des fonctions de communautés, tout en fournissant des pages simples sur lesquelles explorer l&#39;utilisation du [cadre de composants sociaux (SCF)](scf.md).

Ce tutoriel s&#39;adresse principalement aux développeurs, nouveaux et AEM, qui s&#39;intéressent à l&#39;utilisation des composants SCF. Il passe en revue la création d&#39;un site de sandbox SCF, semblable au didacticiel de [Création d&#39;un site Web Internet à part entière](../../help/sites-developing/website.md) qui se concentre sur les structures du site, telles que la navigation, le logo, la recherche, la barre d&#39;outils et la liste des pages enfants.

Le développement a lieu sur une instance d’auteur, tandis que l’expérimentation du site est préférable sur une instance de publication.

Les étapes de ce didacticiel sont les suivantes :

* [Configurer la structure du site Web](setup-website.md)
* [Application Sandbox initiale](initial-app.md)
* [Contenu initial du sandbox](initial-content.md)
* [Développement d’une application Sandbox](develop-app.md)
* [Ajouter les bibliothèques clientes](add-clientlibs.md)
* [Développement du contenu du sandbox](develop-content.md)

>[!CAUTION]
>
>Ce didacticiel ne crée pas de site communautaire avec la fonctionnalité créée à l&#39;aide de la [console Sites communautaires](sites-console.md). Par exemple, ce didacticiel ne décrit pas comment configurer la connexion, l’auto-inscription, [la connexion sociale](social-login.md), la messagerie, les profils, etc.
>
>Si vous préférez un site communautaire simple, suivez le [didacticiel Créer un exemple de page](create-sample-page.md).

## Conditions préalables {#prerequisites}

Ce didacticiel suppose que vous avez installé un auteur AEM et une instance de publication AEM qui possède la [dernière version](deploy-communities.md#latest-releases) des communautés.

Voici quelques liens utiles pour les développeurs qui viennent d&#39;accéder à la plateforme AEM :

* [Prise en main](../../help/sites-deploying/deploy.md#getting-started) : pour déployer les instances AEM.

   * [Les bases](../../help/sites-developing/the-basics.md) : pour les développeurs de sites Web et de fonctionnalités.
   * [Premières étapes pour les auteurs](../../help/sites-authoring/first-steps.md) : pour la création de contenu de page.

## Utilisation de l’Environnement de développement CRXDE Lite {#using-crxde-lite-development-environment}

Les développeurs AEM passent la plupart de leur temps dans l’environnement de développement [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) sur une instance d’auteur. CRXDE Lite fournit un accès moins restreint au référentiel CRX. Les outils d’interface utilisateur classiques et les consoles d’interface utilisateur tactiles offrent un accès plus structuré à des portions spécifiques du référentiel CRX.

Une fois connecté avec des privilèges d’administration, vous pouvez accéder au CRXDE Lite de différentes manières :

1. Dans la navigation globale, sélectionnez navigation **[!UICONTROL Outils > CRXDE Lite]**.

   ![crxde-lite](assets/tools-crxde.png)

2. Dans la [page d’accueil classique de l’interface utilisateur](http://localhost:4502/welcome.html), faites défiler la page vers le bas et cliquez sur **[!UICONTROL CRXDE Lite]** dans le panneau de droite.

   ![classic-ui-crxde](assets/classic-ui-crxde.png)

3. Accédez directement à `CRXDE Lite` : `<server>:<port>/crx/de`

   Par exemple, sur une instance d’auteur locale : [http://localhost:4502/crx/de](http://localhost:4502/crx/de)

Pour travailler avec un CRXDE Lite, vous devez vous connecter avec des privilèges de développeur ou d’administrateur. Pour l’instance localhost par défaut, vous pouvez vous connecter avec

* `username: admin`
* `password: admin`


**Soyez** conscient que cette connexion va expirer et que vous devrez vous reconnecter régulièrement en utilisant la liste déroulante située à l’extrémité droite de la barre d’outils CRXDe Lite.

Si vous n’êtes pas connecté, vous ne pourrez pas parcourir le référentiel JCR ou effectuer des opérations de modification/enregistrement.

***En cas de doute, reconnectez-vous !***

![réouverture](assets/relogin.png)
