---
title: Création d’applications mobiles
description: Le tableau de bord AEM Mobile vous permet de créer, de créer et de déployer votre application mobile, ainsi que de créer, supprimer et modifier les métadonnées de l'application. Consultez cette page pour en savoir plus.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
exl-id: 073daff7-0c1d-4715-bfd4-3e2336e4cb88
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '982'
ht-degree: 1%

---

# Création d’applications mobiles{#authoring-mobile-applications}

{{ue-over-mobile}}

Le tableau de bord AEM Mobile vous permet de créer, de créer et de déployer votre application mobile, ainsi que de créer, supprimer et modifier les métadonnées de l&#39;application. Une fois votre application activée, vous pouvez analyser les analyses d’applications, y compris les mesures de cycle de vie et d’utilisation, afin d’améliorer la conversion des clients et la fidélité à la marque.

Pour créer votre application AEM Mobile, reportez-vous à la page [Création d’applications mobiles](/help/mobile/building-app-mobile-phonegap.md).

Pour configurer votre environnement et commencer, reportez-vous à la section [Administration d’AEM pour utiliser AEM PhoneGap Enterprise](/help/mobile/administer-phonegap.md).

## Le Catalogue Des Applications AEM Mobile {#the-aem-mobile-apps-catalog}

Le [Catalogue des applications AEM Mobile](http://localhost:4502/aem/apps.html/content/phonegap) affiche toutes les applications mobiles gérées dans AEM.

Considérez ce catalogue comme la « page de destination » d’AEM Mobile, où les administrateurs peuvent démarrer une nouvelle application AEM Mobile en créant à partir d’un modèle ou en chargeant une application existante déjà démarrée par un développeur ou une développeuse mobile.

Pour accéder à la page de destination du catalogue d’applications, procédez comme suit :

1. Accédez à **Navigation** puis choisissez **Mobile**.

1. Sélectionnez **Applications** pour ouvrir le catalogue d’applications.

![Catalogue Des Applications AEM Mobile](assets/chlimage_1-135.png)

## Tableau de bord de l’application AEM Mobile {#the-aem-mobile-app-dashboard}

La sélection d’une application AEM Mobile dans le catalogue affiche son tableau de bord. Vous pouvez y gérer votre application, afficher des statistiques, créer, déployer et gérer le contenu de votre application mobile.

Vous pouvez développer chaque mosaïque du tableau de bord d’AEM Mobile pour afficher ou modifier des détails en cliquant sur le signe « ... » dans le coin inférieur droit.

![Centre de commande des applications AEM Mobile](assets/chlimage_1-136.png)

### La Mosaïque Gérer L’Application {#the-manage-app-tile}

La mosaïque Gérer l’application affiche l’icône de votre application, son nom, sa description, les plateformes prises en charge, l’URL d’appel de mise à jour et les informations de version. Vous pouvez accéder à cette mosaïque pour modifier et gérer la configuration de l’application PhoneGap (config.xml) et préparer votre application pour l’envoi aux différents magasins d’applications en vue de sa distribution.

Cliquez [ici](/help/mobile/phonegap-app-details-tile.md) pour plus de détails.

![chlimage_1-137](assets/chlimage_1-137.png)

### La Mosaïque Gérer Le Contenu De La Page {#the-manage-page-content-tile}

Vous pouvez créer, mettre à jour et supprimer du contenu dans AEM Mobile de la même manière que dans AEM Sites. La mosaïque **Gérer le contenu de la page** indique le nombre de pages de contenu géré et la date de leur dernière modification. Vous pouvez explorer le contenu pour créer, copier, déplacer, supprimer et mettre à jour des pages en cliquant sur chaque enregistrement de la mosaïque. Une fois le contenu mis à jour, vous pouvez envoyer une mise à jour de contenu à vos clients via la mosaïque **Gérer les packages de contenu**.

![Mosaïque de contenu](assets/chlimage_1-138.png)

### La Mosaïque Gérer Les Packages De Contenu {#the-manage-content-packages-tile}

Une fois que vous avez ajouté ou modifié votre contenu par l’intermédiaire de la mosaïque Gérer le contenu de la page, vous pouvez transmettre ces modifications à vos clients à l’aide d’une mise à jour de la version du contenu.

Le package de contenu permet à l’auteur de l’application AEM de gérer le contenu des pages dans AEM et de demander à votre équipe de développement de modifier votre application PhoneGap Shell (c’est-à-dire la structure ou l’infrastructure de l’application), puis d’envoyer ces modifications à vos clients rapidement et sans avoir à inviter un développeur à se soumettre à nouveau aux différents magasins pour distribution.

Le package de contenu crée un fichier ZIP, considéré comme un package de publication de contenu, pour chaque mise à jour. Ces packages contiennent des ressources et des pages HTML générées lors du rendu de l’application et sont suffisamment intelligents pour ne compresser que les fichiers qui ont été modifiés depuis la dernière mise à jour.

La colonne **Type** Gérer la mosaïque du package de contenu affiche « Application » pour indiquer le contenu Application Shell, par exemple, la structure ou l’infrastructure de l’application gérée par un développeur ou une développeuse, ou « Contenu » qui représente le contenu de la page géré par l’auteur du contenu.

Le contenu peut être représenté sous la forme d’une langue ou d’une partie spécifique de l’application où plusieurs packages de publication de contenu sont consommés par l’application. Le choix de la manière dont vous regroupez votre contenu est flexible et dépend entièrement de la manière dont vous souhaitez gérer le contenu pour votre application.

La colonne **Modifié** indique la date de la dernière modification des pages.

La colonne **En cours** indique la date de création de la dernière mise à jour du contenu. Pour créer une mise à jour de contenu et préparer vos modifications, ouvrez n’importe quel enregistrement de la mosaïque et créez une mise à jour.

La colonne **Publié** indique la date à laquelle la dernière mise à jour du contenu a été publiée et mise à la disposition de vos clients. Pour publier du contenu, vous devez d’abord préparer ce contenu, puis publier la mise à jour en accédant à cette mosaïque et en le publiant à partir de la console Détails de la publication du contenu .

![Mosaïque de mise à jour de contenu](assets/chlimage_1-139.png) ![package ContentSync pour le shell de l’application](do-not-localize/chlimage_1-5.png)

Cette icône représente un package de publication de contenu pour le shell de l’application

![Icône du package de publication de contenu indiquée par deux symboles carrés de package qui se chevauchent.](do-not-localize/chlimage_1-6.png)

Ces icônes représentent un package de publication de contenu pour le contenu de l’application

### La mosaïque PhoneGap Build {#the-phonegap-build-tile}

La vignette **PhoneGap Build** se connecte à `https://build.phonegap.com` pour créer et héberger des versions distantes. Une fois créée, la version est disponible soit sous la forme d’un téléchargement, soit directement sur votre appareil via un code QR.

Vous pouvez également télécharger la source de l’appareil pour créer localement via l’interface de ligne de commande PhoneGap (`https://docs.phonegap.com/en/3.5.0/guide_cli_index.md.html`).

![Vignette PhoneGap Build &#x200B;](assets/chlimage_1-140.png)

### La Mosaïque Mesures {#the-metrics-tile}

>[!CAUTION]
>
>La mosaïque Mesures s’affiche uniquement une fois que vous avez configuré le service cloud.
>
>Pour plus d’informations, voir [Configuration de votre Cloud Service Adobe Mobile Services](/help/mobile/configure-adobe-mobile-cloud-service.md).

AEM Mobile s’intègre à Adobe Analytics via [Adobe Mobile Services SDK](https://experienceleague.adobe.com/docs/mobile.html?lang=fr) (AMS).

Le Control Center **Mosaïque Mesures** affiche des analyses récapitulatives extraites d’AMS pour votre application. Vous pouvez accéder au tableau de bord Analytics en cliquant sur le signe « ... » en bas à droite.

![Mosaïque Mesures](assets/chlimage_1-141.png)

### Mosaïque Gérer le contenu de l’entité {#the-manage-entity-content-tile}

La mosaïque Gérer le contenu d’entité permet d’ajouter et de gérer des définitions d’application. Les définitions d’application sont un moyen d’identifier les espaces (et d’autres configurations) appropriés pour l’application. Ainsi, un nouvel espace peut être ajouté, sans avoir à recompiler l’application. La définition de l’application est mise à jour et inclut les informations de tout nouvel espace.

Cliquez [ici](/help/mobile/phonegap-app-definitions.md) pour créer et gérer vos définitions d’application.

Vous pouvez accéder au tableau de bord de gestion du contenu de l’entité en cliquant sur « ... » en bas à droite.

![chlimage_1-142](assets/chlimage_1-142.png)

#### Ressources supplémentaires {#additional-resources}

Pour en savoir plus sur les rôles et les responsabilités d’un administrateur et d’un développeur, consultez les ressources ci-dessous :

* [Développement pour Adobe PhoneGap Enterprise avec AEM](/help/mobile/developing-in-phonegap.md)
* [Administration de contenu pour Adobe PhoneGap Enterprise avec AEM](/help/mobile/administer-phonegap.md)
