---
title: Comment mettre en ligne votre application découplée
description: Dans cette partie du Parcours de développement AEM découplé, apprenez à déployer une application découplée.
exl-id: ec3356ef-9e60-4151-984d-3ebdab593b96
source-git-commit: ad0f0bd8b0c230e002c734adca87da22bfa3a7cd
workflow-type: tm+mt
source-wordcount: '1903'
ht-degree: 100%

---

# Comment mettre en ligne votre application découplée {#go-live}

Dans cette partie du [Parcours de développement AEM découplé](overview.md), découvrez comment déployer une application découplée en direct.

## Un peu d’histoire...  {#story-so-far}

Dans le document précédent du parcours découplé AEM, [Comment mettre à jour votre contenu grâce aux API d’AEM Assets](update-your-content.md) vous avez appris à mettre à jour votre contenu découplé dans AEM à l’aide de l’API et vous devriez maintenant :

* comprendre comment fonctionne l’API HTTP d’AEM Assets.

Cet article s’appuie sur ces principes de base pour que vous compreniez comment préparer votre propre projet AEM découplé à être mis en ligne.

## Objectif {#objective}

Ce document vous aide à comprendre le pipeline de publication découplée AEM et les considérations que vous devez prendre en compte concernant les performances avant de mettre en ligne votre application.

* En savoir plus sur le SDK AEM et sur l’outil de développement requis
* Configuration d’un environnement d’exécution de développement local pour simuler votre contenu avant la mise en ligne
* Présentation des notions de base sur la réplication et la mise en cache du contenu AEM
* Sécurisez et mettez à l’échelle votre application avant son lancement
* Surveillance des performances et du débogage

## SDK AEM {#the-aem-sdk}

Le SDK AEM permet de créer et de déployer du code personnalisé. Il s’agit du principal outil dont vous avez besoin pour développer et tester votre application découplée avant sa mise en ligne. Il contient les artefacts suivants :

* Le jar Quickstart : fichier jar exécutable qui peut être utilisé pour configurer une instance d’auteur et une instance de publication.
* Les outils de dispatcher : module Dispatcher et ses dépendances pour les systèmes Windows et UNIX
* Le jar de l’API Java : dépendance Jar/Maven Java qui expose toutes les API Java autorisées pouvant être utilisées en vue de développer pour AEM.
* Le jar Javadoc : javadocs du fichier jar de l’API Java.

## Outils de développement supplémentaires {#additional-development-tools}

Outre le SDK AEM, vous avez besoin d’outils supplémentaires qui facilitent le développement et le test local de votre code et de votre contenu :

* Java
* Git
* Apache Maven
* La bibliothèque Node.js
* L’environnement de développement intégré (IDE) de votre choix

Comme AEM est une application Java, vous devez installer Java et le SDK Java pour prendre en charge le développement d’AEM as a Cloud Service.

Vous utiliserez Git pour gérer le contrôle de code source et pour archiver les modifications apportées à Cloud Manager, puis pour les déployer sur une instance de production.

AEM utilise Apache Maven pour créer des projets générés à partir de l’archétype de projet AEM Maven. Tous les environnements de développement intégré majeurs prennent en charge l’intégration de Maven.

Node.js est un environnement d’exécution JavaScript utilisé pour fonctionner avec les ressources front-end du sous-projet `ui.frontend` d’un projet AEM. Node.js est distribué avec npm, qui est le gestionnaire de packages Node.js utilisé de facto pour gérer les dépendances JavaScript.

## Composants d’un système AEM en un coup d’œil {#components-of-an-aem-system-at-a-glance}

Regardons ensuite les éléments qui constituent un environnement AEM.

Un environnement d’AEM complet est constitué d’un auteur, d’une publication et d’un Dispatcher. Ces mêmes composants seront disponibles dans l’exécution de développement local afin de vous permettre de prévisualiser plus facilement votre code et votre contenu avant la mise en ligne.

* **Le service Auteur** permet aux utilisateurs internes de créer, gérer et prévisualiser du contenu.

* **Le service de publication** est considéré comme l’environnement « En ligne » et est généralement celui avec lequel les utilisateurs finaux interagissent. Le contenu, après avoir été modifié et approuvé sur le service Auteur, est distribué (répliqué) au service Publication. Le modèle de déploiement le plus courant avec les applications découplées AEM est de connecter la version de production de l’application à un service de publication AEM.

* **Le Dispatcher** est un serveur web statique qui est alimenté par le module Dispatcher d’AEM. Ce module met en cache les pages web produites par l’instance de publication pour améliorer les performances.

## Workflow de développement local {#the-local-development-workflow}

Le projet de développement local est basé sur Apache Maven et utilise Git pour le contrôle de code source. Pour mettre à jour le projet, les développeurs peuvent utiliser leur environnement de développement intégré préféré, tel qu’Eclipse, Visual Studio Code ou IntelliJ, entre autres.

Pour tester le code ou les mises à jour de contenu qui seront ingérées par votre application découplée, vous devez déployer les mises à jour sur l’exécution locale AEM, qui inclut les instances locales des services de création et de publication AEM.

Veillez à tenir compte des différences entre chaque composant dans l’exécution locale AEM, car il est important de tester vos mises à jour là où elles comptent le plus. Par exemple, testez les mises à jour du contenu sur l’instance de création ou testez le nouveau code sur l’instance de publication.

Dans un système de production, un dispatcher et un serveur Apache http se trouvent toujours en face d’une instance de publication AEM. Ils fournissent des services de mise en cache et de sécurité pour le système AEM. Il est donc essentiel de tester le code et les mises à jour de contenu par rapport au dispatcher.

## Prévisualisation locale de votre code et de votre contenu avec l’environnement de développement local {#previewing-your-code-and-content-locally-with-the-local-development-environment}

Pour préparer votre projet découplé AEM à son lancement, vous devez vous assurer que tous les éléments constituant votre projet fonctionnent correctement.

Pour cela, vous devez tout assembler (code, contenu et configuration), puis le tester dans un environnement de développement local pour vous préparer en temps réel.

L’environnement de développement local se compose de trois principaux éléments :

1. Le projet AEM : contient tout le code personnalisé, la configuration et le contenu sur lesquels les développeurs AEM vont travailler.
1. L’exécution locale AEM : les versions locales des services d’auteur et de publication AEM qui seront utilisés pour déployer le code du projet AEM.
1. L’exécution locale du Dispatcher : la version locale du serveur web Apache httpd qui comprend le module de Dispatcher.

Une fois l’environnement de développement local configuré, vous pouvez simuler la diffusion de contenu vers l’application React en déployant localement un serveur de nœuds statique.

Pour plus d’informations sur la configuration d’un environnement de développement local et sur toutes les dépendances nécessaires à l’aperçu du contenu, consultez [Documentation sur le déploiement en production](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/production-deployment.html?lang=fr#prerequisites).

## Préparation de votre application découplée AEM pour la mise en ligne {#prepare-your-aem-headless-application-for-golive}

<!-- Start of CDN Review -->

Il est maintenant temps de préparer votre application découplée AEM pour son lancement, en observant les bonnes pratiques décrites ci-dessous.

### Sécurisation de votre application découplée avant son lancement {#secure-and-scale-before-launch}

1. Préparez votre [Authentification](/help/sites-developing/headless/graphql-api/graphql-authentication-content-fragments.md) pour vos requêtes GraphQL.

### Structure du modèle par rapport à l’output GraphQL {#structure-vs-output}

* Évitez de créer des requêtes qui génèrent plus de 15 ko de JSON (fichier compressé gzip). Les fichiers JSON trop longs consomment beaucoup de ressources que l’application cliente doit ensuite analyser.
* Évitez plus de cinq niveaux imbriqués dans les hiérarchies de fragments. Les niveaux supplémentaires rendent difficile la prise en compte de l’impact de leurs modifications par les auteurs de contenu.
* Utilisez des requêtes à plusieurs objets au lieu de modéliser des requêtes avec des hiérarchies de dépendances au sein des modèles. Vous obtiendrez grâce à cela une plus grande flexibilité à long terme pour restructurer la sortie JSON sans avoir à effectuer de nombreuses modifications de contenu.

### Maximiser le ratio cache-accès CDN {#maximize-cdn}

* N’utilisez pas de requêtes GraphQL directes, sauf si vous demandez du contenu en direct à la surface.
   * Dans la mesure du possible, utilisez des requêtes persistantes.
   * Fournissez un TTL CDN supérieur à 600 secondes pour que le CDN les mette en cache.
   * AEM peut calculer l’impact d’une modification de modèle sur des requêtes existantes.
* Partagez les requêtes de fichiers JSON et GraphQL entre un taux de changement de contenu faible et élevé afin de réduire le trafic client sur le réseau de diffusion de contenu et d’attribuer un TTL plus élevé. Vous minimiserez grâce à cela la revalidation par le CDN du fichier JSON avec le serveur d’origine.
* Pour invalider activement le contenu du réseau de diffusion de contenu, utilisez la fonction Purge progressive. Cela permet au réseau de diffusion de contenu de télécharger à nouveau le contenu sans provoquer l’échec du cache.

>[!NOTE]
>
>Consultez les [Ressources supplémentaires](#additional-resources) pour plus d’informations sur le réseau de diffusion de contenu et la mise en cache.

### Amélioration du temps de téléchargement du contenu découplé {#improve-download-time}

* Assurez-vous que les clients HTTP utilisent HTTP/2.
* Assurez-vous que les clients HTTP acceptent la requête d’en-têtes pour gzip.
* Réduisez le nombre de domaines utilisés pour héberger les artefacts JSON et les artefacts référencés.
* Utilisez `Last-modified-since` pour actualiser les ressources.
* Utilisez la sortie `_reference` du fichier JSON pour commencer à télécharger des ressources sans avoir à analyser les fichiers JSON complets.

<!-- End of CDN Review -->

## Déploiement en environnement de production {#deploy-to-production}

Le déploiement en exploitation peut dépendre de l’existence ou non d’une instance AEM *traditionnelle* déployée à l’aide de Maven ou qui se trouve sur Adobe Managed Services (AMS) et qui, par conséquent, utilise Cloud Manager.

## Déploiement en exploitation à l’aide de Maven {#deploy-to-production-maven}

Concernant les déploiements *traditionnels* (non AMS) à l’aide de Maven, vous pouvez consulter le [Tutoriel WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/project-archetype/project-setup.html?lang=fr#build) pour obtenir une vue d’ensemble.

## Déploiement en exploitation à l’aide de Cloud Manager {#deploy-to-production-cloud-manager}

Si vous êtes un client AMS utilisant Cloud Manager, une fois que vous avez vérifié que tout a été testé et fonctionne correctement, vous êtes prêt à transmettre vos mises à jour de code au [référentiel Git centralisé dans Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/setup-cloud-manager-git-integration.html?lang=fr).

Une fois les mises à jour transférées vers Cloud Manager, elles peuvent être déployées vers AEM à l’aide du [pipeline CI/CD de Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html?lang=fr).

<!-- Can't find a parallel link -->
<!--
You can start deploying your code by leveraging the Cloud Manager CI/CD pipeline, which is covered extensively [here](/help/implementing/deploying/overview.md).
-->

## Surveillance des performances {#performance-monitoring}

Pour que les utilisateurs disposent de la meilleure expérience possible lorsqu’ils utilisent l’application découplée AEM, il est important de surveiller les mesures de performances clés, comme indiqué ci-dessous :

* la validation des versions d’aperçu et de production de l’application ;
* la vérification des pages d’état AEM pour l’état de disponibilité actuelle du service ;
* l’accès aux rapports de performance ;
   * Les performances de diffusion
      * Les serveurs d’origine : le nombre d’appels, les taux d’erreur, la charge du processeur, le trafic de charge utile
   * Les performances auteur
      * Pour vérifier le nombre d’utilisateurs, de demandes et de chargements
* l’accès aux rapports de performances spécifiques à l’application et à la surface.
   * Une fois le serveur ouvert, vérifiez si les mesures générales apparaissent en vert/orange/rouge, puis identifiez les problèmes spécifiques à l’application.
   * Ouvrez les rapports ci-dessus filtrés par application ou par surface (par exemple, la version bureau de Photoshop, un paywall).
   * Utilisez des API de journal Splunk pour accéder aux performances du service et de l’application.
   * Contactez le service clientèle si d’autres problèmes se produisent.

## Résolution des problèmes {#troubleshooting}

### Débogage {#debugging}

Observez ces bonnes pratiques pour votre approche générale de débogage :

* Validez les fonctionnalités et les performances avec la version d’aperçu de l’application.
* Validez les fonctionnalités et les performances avec la version de production de l’application.
* Validez à l’aide de l’aperçu JSON de l’éditeur de fragment de contenu.
* Inspectez le JSON dans l’application cliente pour vérifier la présence de problèmes d’application cliente ou de diffusion.
* Inspectez le JSON à l’aide de GraphQL pour vérifier la présence de problèmes liés au contenu mis en cache ou à AEM.

### Journalisation d’un bogue avec prise en charge {#logging-a-bug-with-support}

Pour consigner efficacement un bogue avec l’assistance si vous avez besoin d’aide supplémentaire, procédez comme suit :

* Si nécessaire, réalisez des captures d’écran du problème.
* Documentez une façon de reproduire le problème.
* Documentez le contenu à l’origine du problème.
* Consignez un problème à l’aide du portail d’assistance AEM avec la priorité appropriée.

## Serait-ce la fin de notre voyage ?  {#journey-ends}

Félicitations ! Vous avez terminé le parcours de développement découplé AEM. Vous devriez maintenant comprendre les éléments suivants :

* La différence entre la diffusion de contenu couplé et découplé
* Les fonctionnalités découplées AEM
* Comment organiser un projet découplé AEM
* Comment créer du contenu découplé dans AEM
* Comment récupérer et mettre à jour du contenu découplé dans AEM
* La mise en ligne d’un projet découplé AEM
* Que faire après la mise en ligne

Vous avez peut-être déjà lancé votre premier projet découplé AEM, vous disposez en tout cas déjà de toutes les connaissances nécessaires pour le faire. Super boulot !

### Découvrez les applications sur une seule page {#explore-spa}

Les magasins découplés AEM n’ont pourtant pas besoin de s’arrêter à ça. Vous vous souvenez peut-être que dans la section [Prise en main du parcours](getting-started.md#integration-levels) nous avons brièvement expliqué comment AEM peut non seulement prendre en charge la diffusion découplée et les modèles complets traditionnels mais également les modèles hybrides qui combinent les avantages des deux.

Si ce type de flexibilité est nécessaire pour votre projet, passez à la section optionnelle du parcours intitulée [Comment créer des applications sur une seule page (SPA) avec AEM.](create-spa.md)

## Ressources supplémentaires {#additional-resources}

* [Guide de développement d’AEM](https://experienceleague.adobe.com/docs/experience-manager-65/developing/introduction/the-basics.html?lang=fr)

* [Tutoriel WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=fr)

* [Cloud Manager pour AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=fr)

* Cache CDN

   * [Contrôle d’un cache CDN ](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=fr#controlling-a-cdn-cache)

   * Configuration du [CDN Rewriter](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/osgi-configuration-settings.html?lang=fr) (*recherchez « CDN Rewriter »*)
