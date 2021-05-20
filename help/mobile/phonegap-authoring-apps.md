---
title: Création d’applications mobiles
seo-title: Création d’applications mobiles
description: Le tableau de bord AEM Mobile vous permet de créer, de créer et de déployer votre application mobile, de créer, de supprimer et de modifier les métadonnées de l’application. Consultez cette page pour en savoir plus.
seo-description: Le tableau de bord AEM Mobile vous permet de créer, de créer et de déployer votre application mobile, de créer, de supprimer et de modifier les métadonnées de l’application. Consultez cette page pour en savoir plus.
uuid: 293b5d29-df7e-42dd-ae64-8c677317e7a5
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
discoiquuid: abfeea65-102d-4800-abeb-304d61afcc13
exl-id: 073daff7-0c1d-4715-bfd4-3e2336e4cb88
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1053'
ht-degree: 38%

---

# Création d’applications mobiles{#authoring-mobile-applications}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

Le tableau de bord AEM Mobile vous permet de créer, de créer et de déployer votre application mobile, de créer, de supprimer et de modifier les métadonnées de l’application. Une fois votre application activée, vous pouvez analyser les analyses de l’application, y compris les mesures de cycle de vie et d’utilisation, afin d’améliorer la conversion des clients et la fidélité à la marque.

Pour créer votre application AEM Mobile, consultez la page [Création d’applications mobiles](/help/mobile/building-app-mobile-phonegap.md) .

Pour configurer votre environnement et commencer, voir [Administration d’AEM pour utiliser AEM PhoneGap Enterprise](/help/mobile/administer-phonegap.md).

## Le catalogue d’applications AEM Mobile {#the-aem-mobile-apps-catalog}

Le [catalogue d’applications AEM Mobile](http://localhost:4502/aem/apps.html/content/phonegap) affiche toutes les applications mobiles gérées dans AEM.

Considérez ce catalogue comme la &quot;page d’entrée&quot; d’AEM Mobile, où les administrateurs peuvent démarrer une nouvelle application AEM Mobile en créant une application à partir d’un modèle ou en chargeant une application existante déjà lancée par un développeur mobile.

Pour accéder à la page d’entrée du catalogue d’applications, procédez comme suit :

1. Accédez à **Navigation**, puis sélectionnez **Mobile**.

1. Sélectionnez **Applications** pour ouvrir le catalogue d’applications.

![Catalogue d’applications AEM Mobile](assets/chlimage_1-135.png)

## Le tableau de bord Applications d’AEM Mobile {#the-aem-mobile-app-dashboard}

La sélection d’une application AEM Mobile dans le catalogue entraîne l’affichage de son tableau de bord. Il vous permet de gérer votre application, d’afficher ses statistiques, ainsi que de créer, de déployer et de gérer le contenu de votre application mobile.

Vous pouvez développer chaque mosaïque du tableau de bord AEM Mobile pour afficher ou modifier les détails en cliquant sur &quot;...&quot;. dans le coin inférieur droit.

![Centre de commande d’applications AEM Mobile](assets/chlimage_1-136.png)

### Mosaïque Gestion de l’application {#the-manage-app-tile}

La mosaïque Gestion de l’application présente l’icône de l’application, son nom, sa description, les plateformes prises en charge, l’URL de page d’appel pour les mises à jour et les informations relatives à la version. Vous pouvez voir les détails de cette mosaïque pour modifier et gérer la configuration d’applications PhoneGap (config.xml) et préparer votre application en vue de sa soumission et de sa diffusion sur les différentes boutiques d’applications.

Cliquez [ici](/help/mobile/phonegap-app-details-tile.md) pour plus de détails.

![chlimage_1-137](assets/chlimage_1-137.png)

### Mosaïque Gérer le contenu de la page {#the-manage-page-content-tile}

Le contenu peut être créé, mis à jour et supprimé dans AEM Mobile de la même manière que dans AEM Sites. La mosaïque **Gérer le contenu de la page** affiche le nombre de pages de contenu géré et la dernière modification. Vous pouvez voir le détail du contenu pour créer, copier, déplacer, supprimer et mettre à jour des pages en cliquant sur chaque enregistrement de la mosaïque. Une fois que le contenu a été mis à jour, vous pouvez envoyer une mise à jour de contenu à vos clients via la mosaïque **Gérer les modules de contenu.**

![Mosaïque Contenu](assets/chlimage_1-138.png)

### Mosaïque Gérer les packages de contenu {#the-manage-content-packages-tile}

Une fois que vous avez ajouté ou modifié votre contenu par le biais de la mosaïque Gérer le contenu de la page , vous pouvez envoyer ces modifications à vos clients avec une mise à jour de la version du contenu.

Le module de contenu permet à AEM’auteur d’applications de gérer le contenu des pages dans AEM et de demander à votre équipe de développement d’apporter des modifications à votre application Shell PhoneGap (c’est-à-dire la structure ou l’infrastructure de l’application), puis d’envoyer ces modifications rapidement à vos clients, sans avoir à enrôler un développeur pour qu’il les soumette à nouveau aux différentes boutiques pour distribution.

Le module de contenu crée un fichier ZIP, considéré comme un module de version de contenu, pour chaque mise à jour. Ces modules contiennent des ressources HTML et des pages HTML générées lors du rendu de l’application. Ils sont suffisamment intelligents pour ne compresser que les fichiers qui ont été modifiés depuis la dernière mise à jour.

La colonne **Type** de la mosaïque Gérer le module de contenu affiche &quot;Application&quot; pour désigner le contenu du shell d’application, par exemple la structure ou l’infrastructure de l’application gérée par un développeur ou &quot;Contenu&quot; qui représente le contenu de la page géré par l’auteur du contenu.

Le contenu peut être représenté sous la forme d’un langage ou d’une partie donnée de l’application dans laquelle les packages Version du contenu sont consommés par l’application. Le choix de la façon dont vous regroupez le contenu est censé être souple et dépendre entièrement de la manière dont vous souhaitez gérer le contenu de votre application.

La colonne **Modifié** indique la date de dernière modification des pages.

La colonne **Intermédiaire** indique la date de dernière création d’une mise à jour du contenu. Pour créer une mise à jour de contenu et définir une étape intermédiaire pour vos modifications, ouvrez un enregistrement dans la mosaïque et créez une mise à jour.

La colonne **Publié** indique la date de publication de la dernière mise à jour de contenu à laquelle vos utilisateurs ont pu accéder. Pour publier du contenu, vous devez d’abord en faire l’étape, puis publier la mise à jour en parcourant cette mosaïque et en la publiant à partir de la console Détails de la version de contenu .

![Package ](assets/chlimage_1-139.png) ![TileContentSync de la version de contenu pour l’interpréteur d’application](do-not-localize/chlimage_1-5.png)

Cette icône représente un package Version du contenu pour l’interpréteur d’application

![](do-not-localize/chlimage_1-6.png)

Cette icône représente un package Version du contenu pour le contenu de l’application

### Mosaïque PhoneGap Build {#the-phonegap-build-tile}

La **mosaïque PhoneGap Build** se connecte à [https://build.phonegap.com](https://build.phonegap.com) pour créer et héberger des buids distants. Une fois générée, la compilation est disponible sous forme de téléchargement ou est déployée directement sur votre appareil à l’aide d’un code QR.

Vous pouvez également télécharger la source de l’appareil à compiler en local dans la [ligne de commande de PhoneGap](https://docs.phonegap.com/en/3.5.0/guide_cli_index.md.html).

![Mosaïque PhoneGap Build](assets/chlimage_1-140.png)

### Mosaïque Mesures {#the-metrics-tile}

>[!CAUTION]
>
>La mosaïque Mesures s’affiche uniquement une fois que vous avez configuré le service cloud.
>
>Voir [Configuration de votre Cloud Service Mobile Services Adobe](/help/mobile/configure-adobe-mobile-cloud-service.md) pour plus d’informations.

AEM Mobile s’intègre à Adobe Analytics par le biais du [SDK Adobe Mobile Services](https://www.adobe.com/ca/solutions/digital-marketing/mobile-services/app-sdk.html) (AMS).

La mosaïque **Mesures** du centre de contrôle présente un récapitulatif des données analytiques issues d’AMS pour votre application. Vous pouvez parcourir le tableau de bord Analyses en cliquant sur « … » en bas à droite.

![Mosaïque Mesures](assets/chlimage_1-141.png)

### Mosaïque Gérer le contenu de l’entité {#the-manage-entity-content-tile}

La mosaïque Gérer le contenu des entités vous permet d’ajouter et de gérer des définitions d’application. Les définitions d’application permettent d’identifier les espaces (et autres configurations) appropriés à l’application. De cette manière, un nouvel espace peut être ajouté, sans avoir à recompiler l’application. La définition de l’application est mise à jour et inclut les informations de tous les nouveaux espaces.

Cliquez [ici](/help/mobile/phonegap-app-definitions.md) pour créer et gérer les définitions de votre application.

Vous pouvez accéder au tableau de bord de gestion du contenu des entités en cliquant sur &quot;...&quot;. en bas à droite.

![chlimage_1-142](assets/chlimage_1-142.png)

#### Ressources supplémentaires {#additional-resources}

Pour en savoir plus sur les rôles et les responsabilités d’un administrateur et d’un développeur, consultez les ressources ci-dessous :

* [Développement pour Adobe PhoneGap Enterprise avec AEM](/help/mobile/developing-in-phonegap.md)
* [Administration de contenu pour Adobe PhoneGap Enterprise avec AEM](/help/mobile/administer-phonegap.md)
