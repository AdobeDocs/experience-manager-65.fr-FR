---
title: Extension de  [!DNL Adobe Experience Manager] 6.5 à l’aide d’Adobe Developer App Builder.
description: Extension de  [!DNL Adobe Experience Manager] 6.5 à l’aide d’Adobe Developer App Builder.
source-git-commit: e6153e1a816bb9169f96fa75827593485a6ddbd4
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---


# Extension de [!DNL Adobe Experience Manager] à l’aide d’Adobe Developer App Builder {#extend-using-app-builder}

## Présentation d’App Builder pour AEM {#project-firefly}

Le nouveau créateur d’applications pour développeur Adobe fournit un cadre d’extensibilité permettant aux développeurs d’étendre facilement les fonctionnalités AEM.

App Builder fournit une structure d’extensibilité tierce unifiée pour l’intégration et la création d’expériences personnalisées qui étendent Adobe Experience Manager. Grâce à ce framework d’extensibilité complet, reposant sur l’infrastructure de l’Adobe, les développeurs peuvent créer des microservices personnalisés, étendre et intégrer Adobe Experience Manager à travers les solutions d’Adobe et le reste de la pile informatique.

App Builder permet aux clients d’étendre facilement Adobe Experience Manager dans divers cas d’utilisation :

* Extensibilité des middleware : connectez des systèmes externes à des applications Adobe qui créent des connecteurs personnalisés ou exploitent une suite d’intégrations préconfigurées.
* Extensibilité des services principaux - Étendez les fonctionnalités de l’application principale en étendant le comportement par défaut avec des fonctionnalités personnalisées et une logique métier.
* Extensibilité de l’expérience utilisateur : étendez l’expérience principale pour prendre en charge les besoins de l’entreprise ou créer des propriétés numériques, des storefronts et des applications back-office spécifiques aux clients.

Depuis l’été 2020, App Builder (précédemment appelé Project Firefly) est disponible pour les clients et les partenaires d’entreprise via notre Aperçu du développeur. La disponibilité générale d’App Builder est prévue pour décembre 2021. Nous invitons les développeurs à tester App Builder via notre [programme d’évaluation](http://adobe.ly/appbuilder-trial).

>[!NOTE]
>
> Pour les clients d’AEM en tant que Cloud Service qui souhaitent tirer parti du créateur d’applications, accédez à [Extension d’Adobe Experience Manager as a Cloud Service à l’aide du créateur d’applications du développeur d’Adobes](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/configuring-and-extending/app-builder.html).

## Architecture {#architecture}

Au lieu d’une solution prête à l’emploi, Adobe Developer App Builder fournit une plateforme de développement commune, cohérente et normalisée pour étendre les solutions Adobe Cloud, notamment les AEM :

* Adobe Developer Console : pour le développement de microservices et d’extensions personnalisés, permet aux développeurs de créer et de gérer des projets tout en accédant à tous les outils et API dont ils ont besoin pour créer des modules externes et des intégrations.
* Outils de développement : outils Open Source, SDK et bibliothèques pour permettre aux développeurs de créer facilement des extensions et des intégrations personnalisées. Utilisez React Spectrum (boîte à outils de l’interface utilisateur d’Adobe) pour disposer d’une interface utilisateur commune à toutes les applications d’Adobe.
* Services : I/O Runtime pour l’hébergement de l’infrastructure sur notre plateforme sans serveur et événements d’E/S pour les intégrations basées sur des événements. Nous fournissons également une prise en charge prête à l’emploi pour le stockage des données et des fichiers.
* Adobe Experience Cloud : les développeurs peuvent soumettre des extensions et des intégrations à publier dans leur organisation Experience Cloud. Les administrateurs système peuvent ensuite examiner, gérer et approuver ces extensions. Une fois la publication effectuée, vos extensions et outils App Builder personnalisés se trouvent aux côtés d’autres applications Adobe Experience Cloud.

Le diagramme suivant illustre la manière dont une application standard créée sur App Builder tire parti de ces fonctionnalités :

![Architecture](assets/firefly-architecture.jpg)

Pour plus d’informations sur l’architecture du générateur d’applications, consultez la section [Aperçu de l’architecture](https://www.adobe.io/app-builder/docs/guides/).

## Prise en main d’App Builder {#additional-resources}

Pour vous aider à prendre en main App Builder, nous avons créé une série de documents pour vous aider à commencer :

* [Prise en main d’App Builder](https://www.adobe.io/app-builder/docs/getting_started/)

## Poursuivre l’apprentissage avec la documentation {#appbuilder-documentation}

App Builder fournit des vidéos et de la documentation à l’intention des développeurs, notamment des guides et une documentation de référence pour vous aider à commencer à développer vos propres applications personnalisées :

* [Documentation du générateur d’applications](https://www.adobe.io/app-builder/docs/overview/)
* [Vidéos sur App Builder](https://www.youtube.com/playlist?list=PLcVEYUqU7VRfDij-Jbjyw8S8EzW073F_o)

## Essai d’une des applications d’exemple {#appbuilder-codesamples}

Prêts à se développer ? Nous avons de nombreux exemples d’applications pour vous aider à démarrer rapidement :

* [Labs de code du créateur d’applications sur le site web du développeur d’Adobes](https://www.adobe.io/app-builder/docs/resources/)

## Assistance {#support}

Pour les demandes d’assistance aux développeurs, nous encourageons les développeurs à utiliser notre [forum Experience League](https://experienceleaguecommunities.adobe.com/t5/project-firefly/ct-p/project-firefly).
