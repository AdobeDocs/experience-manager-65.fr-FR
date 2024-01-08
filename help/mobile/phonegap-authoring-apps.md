---
title: Création d’applications mobiles
description: Le tableau de bord AEM Mobile vous permet de créer, de créer et de déployer votre application mobile, de créer, de supprimer et de modifier les métadonnées de l’application. Consultez cette page pour en savoir plus.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
exl-id: 073daff7-0c1d-4715-bfd4-3e2336e4cb88
source-git-commit: 3bcdbfc17efe1f4c6069fd97fd6a16ec41d0579e
workflow-type: tm+mt
source-wordcount: '1003'
ht-degree: 1%

---

# Création d’applications mobiles{#authoring-mobile-applications}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur de SPA pour les projets qui nécessitent un rendu côté client basé sur la structure d’application d’une seule page (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

Le tableau de bord AEM Mobile vous permet de créer, de créer et de déployer votre application mobile, de créer, de supprimer et de modifier les métadonnées de l’application. Une fois votre application activée, vous pouvez analyser les analyses de l’application, y compris les mesures de cycle de vie et d’utilisation, afin d’améliorer la conversion des clients et la fidélité à la marque.

Pour créer votre application AEM Mobile, voir [Création d’applications mobiles](/help/mobile/building-app-mobile-phonegap.md) page.

Pour configurer votre environnement et commencer, voir [Administration d’AEM pour utiliser AEM PhoneGap Enterprise](/help/mobile/administer-phonegap.md).

## Catalogue des applications AEM Mobile {#the-aem-mobile-apps-catalog}

La variable [Catalogue d’applications AEM Mobile](http://localhost:4502/aem/apps.html/content/phonegap) affiche l’ensemble de votre application mobile gérée dans AEM.

Considérez ce catalogue comme la &quot;page d’entrée&quot; d’AEM Mobile, où les administrateurs peuvent démarrer une nouvelle application AEM Mobile en créant une application à partir d’un modèle ou en chargeant une application existante déjà lancée par un développeur mobile.

Pour accéder à la page d’entrée du catalogue d’applications, procédez comme suit :

1. Accédez à **Navigation** puis choisissez **Mobile**.

1. Choisir **Applications** pour ouvrir le catalogue d’applications.

![Catalogue d’applications AEM Mobile](assets/chlimage_1-135.png)

## Tableau de bord de l’application AEM Mobile {#the-aem-mobile-app-dashboard}

La sélection d’une application AEM Mobile dans le catalogue affiche son tableau de bord. Vous pouvez y gérer votre application, afficher des statistiques, créer, déployer et gérer le contenu de votre application mobile.

Vous pouvez développer chaque mosaïque du tableau de bord AEM Mobile pour afficher ou modifier les détails en cliquant sur &quot;...&quot; dans le coin inférieur droit.

![Centre de commandes des applications AEM Mobile](assets/chlimage_1-136.png)

### Mosaïque Gérer l’application {#the-manage-app-tile}

La mosaïque Gérer l’application affiche l’icône, le nom, la description de votre application, les plateformes prises en charge, appelle la page d’accueil pour les mises à jour, l’URL et les informations de version. Vous pouvez accéder à cette mosaïque pour modifier et gérer la configuration de l’application PhoneGap (config.xml), puis préparer votre application pour envoi aux différentes boutiques d’applications en vue de sa distribution.

Cliquez sur [here](/help/mobile/phonegap-app-details-tile.md) pour plus d’informations.

![chlimage_1-137](assets/chlimage_1-137.png)

### Mosaïque Gérer le contenu de la page {#the-manage-page-content-tile}

Le contenu peut être créé, mis à jour et supprimé dans AEM Mobile de la même manière que vous le faites dans AEM Sites. La variable **Mosaïque Gestion du contenu de la page** affiche le nombre de pages de contenu géré et de la dernière modification. Vous pouvez analyser le contenu pour créer, copier, déplacer, supprimer et mettre à jour des pages en cliquant sur chaque enregistrement de la mosaïque. Une fois que le contenu a été mis à jour, vous pouvez envoyer une mise à jour de contenu à vos clients via le **Mosaïque Gestion des packages de contenu .**

![Mosaïque Contenu](assets/chlimage_1-138.png)

### Mosaïque Gestion des packages de contenu {#the-manage-content-packages-tile}

Une fois que vous avez ajouté ou modifié votre contenu par le biais de la mosaïque Gérer le contenu de la page , vous pouvez envoyer ces modifications à vos clients avec une mise à jour de la version du contenu.

Le module de contenu permet à AEM’auteur d’applications de gérer le contenu de la page dans AEM et de demander à votre équipe de développement de modifier votre application Shell PhoneGap (c’est-à-dire la structure ou l’infrastructure de l’application), puis d’envoyer ces modifications rapidement à vos clients, sans avoir à enrôler un développeur pour qu’il les soumette à nouveau aux divers magasins pour distribution.

Le module de contenu crée un fichier ZIP, considéré comme un module de version de contenu, pour chaque mise à jour. Ces modules contiennent des ressources HTML et des pages HTML générées lors du rendu de l’application. Ils sont suffisamment intelligents pour ne compresser que les fichiers qui ont été modifiés depuis la dernière mise à jour.

Mosaïque Gérer le module de contenu **Type** La colonne affiche soit &quot;Application&quot; pour désigner le contenu du shell d’application, par exemple la structure ou l’infrastructure de l’application gérée par un développeur, soit &quot;Contenu&quot; qui représente le contenu de la page géré par l’auteur du contenu.

Le contenu peut être représenté sous la forme d’une langue ou d’une partie particulière de l’application où plusieurs modules de publication de contenu sont utilisés par l’application. Le choix du mode de regroupement de votre contenu est flexible et dépend entièrement de la manière dont vous souhaitez gérer le contenu de votre application.

La variable **Modifié** indique le moment où les pages ont été modifiées le plus récemment.

La variable **Intermédiaire** affiche la date de la dernière mise à jour du contenu. Pour créer une mise à jour de contenu et préparer vos modifications, ouvrez n’importe quel enregistrement dans la mosaïque et créez une mise à jour.

La variable **Publié** La colonne indique le moment où la dernière mise à jour du contenu a été publiée et mise à la disposition de vos clients. Pour publier du contenu, vous devez d’abord en faire l’étape, puis publier la mise à jour en parcourant cette mosaïque et en la publiant à partir de la console Détails de la version de contenu .

![Mosaïque Version du contenu](assets/chlimage_1-139.png) ![Package ContentSync pour l’interpréteur d’application](do-not-localize/chlimage_1-5.png)

Cette icône représente un package Content Release pour le shell d’application.

![Icône du package de version de contenu indiquée par deux symboles de package qui se chevauchent.](do-not-localize/chlimage_1-6.png)

Ces icônes représentent un module de version du contenu pour le contenu de l’application.

### Mosaïque PhoneGap Build {#the-phonegap-build-tile}

La variable **Mosaïque PhoneGap Build** se connecte à `https://build.phonegap.com` pour créer et héberger des versions distantes. Une fois créée, la version est disponible en téléchargement ou directement sur votre appareil via un code QR.

Vous pouvez également télécharger la source du périphérique à créer localement via l’interface de ligne de commande PhoneGap (`https://docs.phonegap.com/en/3.5.0/guide_cli_index.md.html`).

![Mosaïque PhoneGap Build](assets/chlimage_1-140.png)

### Mosaïque Mesures {#the-metrics-tile}

>[!CAUTION]
>
>La mosaïque Mesures s’affiche uniquement une fois que vous avez configuré le service cloud.
>
>Voir [Configuration de votre Cloud Service Mobile Services Adobe](/help/mobile/configure-adobe-mobile-cloud-service.md) pour plus d’informations.

AEM Mobile s’intègre à Adobe Analytics via [SDK Adobe Mobile Services](https://experienceleague.adobe.com/docs/mobile.html) (AMS).

Le Centre de contrôle **Mosaïque Mesures** affiche les analyses récapitulatives extraites d’AMS pour votre application. Vous pouvez parcourir le tableau de bord des analyses en cliquant sur &quot;...&quot; en bas à droite.

![Mosaïque Mesures](assets/chlimage_1-141.png)

### Mosaïque Gérer le contenu de l’entité {#the-manage-entity-content-tile}

La mosaïque Gérer le contenu des entités vous permet d’ajouter et de gérer des définitions d’application. Les définitions d’application permettent d’identifier les espaces (et autres configurations) appropriés à l’application. De cette manière, un nouvel espace peut être ajouté, sans avoir à recompiler l’application. La définition de l’application est mise à jour et inclut les informations de tous les nouveaux espaces.

Cliquez sur [here](/help/mobile/phonegap-app-definitions.md) pour créer et gérer les définitions de votre application.

Vous pouvez accéder au tableau de bord de gestion du contenu des entités en cliquant sur &quot;...&quot; en bas à droite.

![chlimage_1-142](assets/chlimage_1-142.png)

#### Ressources supplémentaires {#additional-resources}

Pour en savoir plus sur les rôles et les responsabilités d’un administrateur et d’un développeur, consultez les ressources ci-dessous :

* [Développement pour Adobe PhoneGap Enterprise avec AEM](/help/mobile/developing-in-phonegap.md)
* [Administration de contenu pour Adobe PhoneGap Enterprise avec AEM](/help/mobile/administer-phonegap.md)
