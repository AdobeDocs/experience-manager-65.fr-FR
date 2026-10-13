---
title: Comment mettre en ligne votre application AEM découplé
description: Dans cette partie du Parcours de développement AEM découplé, apprenez à déployer une application découplée en production.
exl-id: ec3356ef-9e60-4151-984d-3ebdab593b96
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,GraphQL,Persisted Queries,Developing
role: Admin, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: bfd4bc52-c397-5127-8f86-8953ba9fc0a3
    internal-label: Headless
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
  - id: a642c50e-80eb-4fc1-a5d2-f3762d1f841d
    internal-label: Administration
  - id: d429a63e-ade4-4117-b04e-9b996d1c94ef
    internal-label: Integrations
  - id: c124fa01-25c5-42ec-adf6-21d1c114058b
    internal-label: Developer tools
subfeature_v2:
  - id: e9db7c79-8f65-4281-a439-c9049296d903
    internal-label: Content Fragments
  - id: a02b73a7-bdfc-4225-bdfd-69f7891ab55e
    internal-label: GraphQL
  - id: d781bc8f-52af-43f6-84d0-b73e59a130d5
    internal-label: Persisted queries
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '1930'
ht-degree: 99%
---
# Comment mettre en ligne votre application découplée {#go-live}

Dans cette partie du [Parcours de développement AEM découplé](overview.md), découvrez comment déployer une application découplée en direct.

## L’histoire jusqu’ici {#story-so-far}

Dans le document précédent du parcours découplé AEM, [Comment mettre à jour votre contenu grâce aux API d’AEM Assets](update-your-content.md) vous avez appris à mettre à jour votre contenu découplé dans AEM à l’aide de l’API et vous devriez maintenant :

* Comprendre l’API HTTP AEM Assets.

Cet article s’appuie sur ces principes de base pour que vous compreniez comment préparer votre propre projet AEM découplé pour une mise en ligne.

## Objectif {#objective}

Ce document vous aide à comprendre le pipeline de publication découplée AEM et les considérations que vous devez prendre en compte concernant les performances avant de mettre en ligne votre application.

* En savoir plus sur le SDK AEM et sur les outils de développement requis
* Configurez un environnement d’exécution de développement local pour simuler votre contenu avant la mise en ligne.
* Comprendre les notions de base de la réplication et de la mise en cache du contenu AEM
* Sécurisez et mettez à l’échelle votre application avant son lancement
* Surveillez les performances et déboguez les problèmes

## SDK AEM {#the-aem-sdk}

Le SDK AEM permet de créer et de déployer du code personnalisé. Il s’agit du principal outil dont vous avez besoin pour développer et tester votre application découplée avant sa mise en ligne. Il contient les artefacts suivants :

* Le jar Quickstart : fichier jar exécutable qui peut être utilisé pour configurer une instance d’auteur et une instance de publication.
* Les outils Dispatcher : module Dispatcher et ses dépendances pour les systèmes Windows et UNIX.
* Le jar de l’API Java™ : dépendance Jar/Maven Java™ qui expose toutes les API Java™ autorisées pouvant être utilisées en vue de développer pour AEM.
* Le jar Javadoc : javadocs du fichier jar de l’API Java™

## Outils de développement supplémentaires {#additional-development-tools}

Outre le SDK d’AEM, vous avez besoin d’outils supplémentaires qui facilitent le développement et le test local de votre code et de votre contenu :

* Java™
* Git
* Apache Maven
* La bibliothèque Node.js
* L’environnement de développement intégré (IDE) de votre choix

Comme AEM est une application Java™, vous devez installer Java™ et le SDK Java™ pour prendre en charge le développement d’AEM as a Cloud Service.

Utilisez Git pour gérer le contrôle de code source et pour valider les modifications apportées à Cloud Manager, puis les déployer sur une instance de production.

AEM utilise Apache Maven pour créer des projets générés à partir de l’archétype de projet AEM Maven. Tous les environnements de développement intégré majeurs prennent en charge l’intégration de Maven.

Node.js est un environnement d’exécution JavaScript utilisé pour fonctionner avec les ressources front-end du sous-projet `ui.frontend` d’un projet AEM. Node.js est distribué avec npm, qui est le gestionnaire de modules Node.js utilisé d’ordinaire pour gérer les dépendances JavaScript.

## Composants d’un système AEM en un coup d’œil {#components-of-an-aem-system-at-a-glance}

Regardons maintenant les éléments qui constituent un environnement AEM.

Un environnement d’AEM complet est constitué d’un auteur, d’une publication et d’un Dispatcher. Ces mêmes composants sont disponibles dans l’exécution de développement local afin de vous permettre de prévisualiser plus facilement votre code et votre contenu avant la mise en ligne.

* **Le service de création** permet aux utilisateurs et utilisatrices internes de créer, gérer et prévisualiser du contenu.

* **Le service de publication** est considéré comme l’environnement « actif » et c’est généralement avec lui que les utilisateurs et utilisatrices finaux interagissent. Le contenu, après avoir été modifié et approuvé sur le service Auteur, est distribué (répliqué) au service Publication. Le modèle de déploiement le plus courant avec les applications découplées d’AEM est de connecter la version de production de l’application à un service de publication d’AEM.

* **Le Dispatcher** est un serveur web statique qui est alimenté par le module Dispatcher d’AEM. Ce module met en cache les pages web produites par l’instance de publication pour améliorer les performances.

## Workflow de développement local {#the-local-development-workflow}

Le projet de développement local est basé sur Apache Maven et utilise Git pour la gestion du code source. Pour mettre à jour le projet, les développeurs et développeuses peuvent utiliser leur environnement de développement intégré préféré, tel qu’Eclipse, Visual Studio Code ou IntelliJ, entre autres.

Pour tester le code ou les mises à jour de contenu ingérés par votre application découplée, déployez les mises à jour sur l’exécution locale d’AEM. Il s’agit notamment des instances locales des services de création et de publication d’AEM.

Veillez à tenir compte des différences entre chaque composant dans l’exécution locale AEM, car il est important de tester vos mises à jour là où elles comptent le plus. Par exemple, testez les mises à jour du contenu sur l’instance de création ou testez le nouveau code sur l’instance de publication.

Dans un système de production, un Dispatcher et un serveur Apache http se trouvent toujours en face d’une instance de publication AEM. Ils fournissent des services de mise en cache et de sécurité pour le système AEM. Il est donc essentiel de tester le code et les mises à jour de contenu par rapport au Dispatcher.

## Prévisualisation locale de votre code et de votre contenu avec l’environnement de développement local {#previewing-your-code-and-content-locally-with-the-local-development-environment}

Pour préparer votre projet découplé AEM à son lancement, vous devez vous assurer que tous les éléments constituant votre projet fonctionnent correctement.

Pour ce faire, vous devez tout assembler (code, contenu et configuration), puis tester votre projet dans un environnement de développement local. Tout sera alors prêt pour la mise en ligne.

L’environnement de développement local se compose de trois principaux éléments :

1. Le projet AEM : il contient tout le code personnalisé, la configuration et le contenu sur lesquels les développeurs et développeuses d’AEM vont travailler.
1. L’exécution locale AEM : les versions locales des services de création et de publication AEM utilisés pour déployer le code du projet AEM.
1. L’exécution locale du Dispatcher – une version locale du serveur web Apache httpd qui comprend le module Dispatcher.

Une fois l’environnement de développement local configuré, vous pouvez simuler la diffusion de contenu vers l’application React en déployant localement un serveur Node statique.

Pour plus d’informations sur la configuration d’un environnement de développement local et sur toutes les dépendances nécessaires à la prévisualisation du contenu, consultez la section [Documentation sur le déploiement en production](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/deployments/overview.html?lang=fr).

## Préparez votre application AEM découplé pour la mise en ligne. {#prepare-your-aem-headless-application-for-golive}

<!-- Start of CDN Review -->

Il est temps maintenant de préparer votre application AEM Headless pour son lancement, en observant les bonnes pratiques décrites ci-dessous.

### Sécurisez votre application AEM découplé avant son lancement {#secure-and-scale-before-launch}

1. Préparez votre [Authentification](/help/sites-developing/headless/graphql-api/graphql-authentication-content-fragments.md) pour vos requêtes GraphQL.

### Structure du modèle par rapport à la sortie GraphQL {#structure-vs-output}

* Évitez de créer des requêtes qui génèrent plus de 15 ko de JSON (fichier compressé gzip). Les fichiers JSON trop longs consomment beaucoup de ressources pour l’analyse par l’application cliente.
* Évitez plus de cinq niveaux imbriqués dans les hiérarchies de fragments. Les niveaux supplémentaires rendent difficile la prise en compte de l’impact de leurs modifications par les auteurs de contenu.
* Utilisez des requêtes à plusieurs objets au lieu de modéliser des requêtes avec des hiérarchies de dépendance au sein des modèles. Cela permet une plus grande flexibilité à long terme pour restructurer la sortie JSON sans avoir à effectuer de nombreuses modifications de contenu.

### Maximiser le taux de réussite du cache CDN {#maximize-cdn}

* N’utilisez pas de requêtes GraphQL directes, sauf si vous demandez du contenu en direct depuis la surface.
  * Dans la mesure du possible, utilisez des requêtes persistantes.
  * Définissez la durée de vie par défaut (TTL) du réseau CDN à plus de 600 secondes afin que le réseau CDN puisse les mettre en cache.
  * AEM peut calculer l’impact d’une modification de modèle sur des requêtes existantes.
* Répartissez les fichiers JSON et les requêtes GraphQL entre un faible et un fort taux de modification de contenu afin de réduire le trafic client vers le CDN et d’attribuer un TTL plus élevé. Cela minimise la revalidation par le réseau CDN du fichier JSON avec le serveur d’origine.
* Pour invalider activement le contenu du réseau CDN, utilisez la fonction Purge progressive. Cela permet au réseau CDN de télécharger à nouveau le contenu sans provoquer d’échec de mise en cache.

>[!NOTE]
>
>Consultez les [Ressources supplémentaires](#additional-resources) pour plus d’informations sur le réseau de diffusion de contenu et la mise en cache.

### Amélioration du temps de téléchargement du contenu découplé {#improve-download-time}

* Assurez-vous que les clients HTTP utilisent HTTP/2.
* Assurez-vous que les clients HTTP demandent gzip dans les en-têtes Accept.
* Réduisez le nombre de domaines utilisés pour héberger les artefacts JSON et les artefacts référencés.
* Utilisez `Last-modified-since` pour actualiser les ressources.
* Utilisez la sortie `_reference` du fichier JSON pour commencer à télécharger des ressources sans avoir à analyser les fichiers JSON complets.

<!-- End of CDN Review -->

## Déploiement en environnement de production {#deploy-to-production}

Le déploiement en exploitation peut dépendre de l’existence ou non d’une instance AEM *traditionnelle* déployée à l’aide de Maven ou qui se trouve sur Adobe Managed Services (AMS) et qui, par conséquent, utilise Cloud Manager.

## Déploiement en exploitation à l’aide de Maven {#deploy-to-production-maven}

Concernant les déploiements *traditionnels* (non AMS) à l’aide de Maven, consultez le [Tutoriel WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/project-archetype/project-setup.html?lang=fr#build) pour obtenir une vue d’ensemble.

## Déployer en exploitation à l’aide de Cloud Manager {#deploy-to-production-cloud-manager}

Si vous êtes un client ou une cliente AMS utilisant Cloud Manager, une fois que vous avez vérifié que tout a été testé et fonctionne correctement, vous pouvez transmettre vos mises à jour de code au [référentiel Git centralisé dans Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/managing-code/git-integration.html?lang=fr).

Une fois les mises à jour transférées vers Cloud Manager, elles peuvent être déployées vers AEM à l’aide du [pipeline CI/CD de Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/code-deployment.html?lang=fr).

<!-- Cannot find a parallel link -->
<!--
You can start deploying your code by using the Cloud Manager CI/CD pipeline, which is covered extensively - see the [Overview](/help/implementing/deploying/overview.md) to start.
-->

## Surveillance des performances {#performance-monitoring}

Pour que les utilisateurs disposent de la meilleure expérience possible lorsqu’ils utilisent l’application découplée AEM, il est important de surveiller les mesures de performances clés, comme indiqué ci-dessous :

* Validez les versions d’aperçu et de production de l’application.
* Vérifiez les pages de statut AEM pour connaître le statut de disponibilité actuel du service.
* l’accès aux rapports de performance ;
  * Les performances de diffusion
    * Les serveurs d’origine : le nombre d’appels, les taux d’erreur, la charge du processeur, le trafic de charge utile
  * Les performances auteur
    * la vérification du nombre d’utilisateurs et d’utilisatrices, de requêtes et de chargements
* Accédez aux rapports de performances spécifiques à l’application et à la surface.
  * Une fois le serveur démarré, vérifiez si les mesures générales apparaissent en vert/orange/rouge, puis identifiez les problèmes spécifiques à l’application.
  * Ouvrez les rapports ci-dessus filtrés par application ou par espace (par exemple, la version bureau de Photoshop, un paywall).
  * Utilisez des API de journal Splunk pour accéder aux performances du service et de l’application.
  * Contactez le service client si d’autres problèmes se produisent.

## Résolution des problèmes {#troubleshooting}

### Débogage {#debugging}

Observez ces bonnes pratiques pour votre approche générale de débogage :

* Validez la fonctionnalité et les performances avec la version d’aperçu de l’application.
* Validez la fonctionnalité et les performances avec la version de production de l’application.
* Validez à l’aide de l’aperçu JSON de l’éditeur de fragment de contenu.
* Pour vérifier la présence de problèmes liés à l’application cliente ou à la diffusion, examinez le fichier JSON dans l’application cliente.
* Pour vérifier la présence de problèmes liés au contenu mis en cache ou à AEM, examinez le fichier JSON à l’aide de GraphQL.

### Enregistrement d’un bug auprès du support {#logging-a-bug-with-support}

Pour signaler un bug de manière efficace à l’assistance, si vous avez besoin d’aide supplémentaire, procédez comme suit :

* Si nécessaire, réalisez des captures d’écran du problème.
* Documentez une façon de reproduire le problème.
* Documentez le contenu à l’origine du problème.
* Consignez un problème à l’aide du portail d’assistance AEM avec la priorité appropriée.

## Serait-ce la fin de notre voyage ? {#journey-ends}

Félicitations ! Vous avez terminé le parcours du développeur découplé AEM. Vous devriez maintenant comprendre les éléments suivants :

* La différence entre la diffusion de contenu couplé et découplé.
* Les fonctionnalités découplées AEM
* Comment organiser un projet découplé AEM.
* Comment créer du contenu découplé dans AEM.
* Comment récupérer et mettre à jour du contenu découplé dans AEM.
* Comment mettre en ligne un projet découplé AEM.
* Les actions à réaliser une fois la mise en ligne effectuée.

Vous avez soit déjà lancé votre premier projet AEM découplé, soit vous disposez désormais de toutes les connaissances nécessaires pour le faire. Très bon travail.

### Découvrez les applications sur une seule page {#explore-spa}

Il n’est toutefois pas nécessaire d’arrêter les magasins découplés d’AEM. Dans la section [Prise en main d’une partie du parcours](getting-started.md#integration-levels), nous avons expliqué comment AEM peut non seulement prendre en charge la diffusion découplée et les modèles full-stack traditionnels, mais également les modèles hybrides, qui offrent le meilleur des deux mondes.

Si vous recherchez cette flexibilité pour votre projet, consultez la section facultative du parcours intitulée [Comment créer des applications monopages (SPA) avec AEM.](create-spa.md)

## Ressources supplémentaires {#additional-resources}

* [Guide de développement d’AEM](https://experienceleague.adobe.com/docs/experience-manager-65/developing/introduction/the-basics.html?lang=fr)

* [Tutoriel WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=fr)

* [Cloud Manager pour AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html?lang=fr)

* Cache CDN

  * [Contrôle d’un cache CDN](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=fr#controlling-a-cdn-cache)

  * Configuration du [CDN Rewriter](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/osgi-configuration-settings.html?lang=fr) (*recherchez « CDN Rewriter »*)

* [Présentation d’AEM en tant que CMS découplé](/help/sites-developing/headless/introduction.md)
* [Portail du développeur AEM](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=fr)
* [Tutoriels pour Headless dans AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=fr)
