---
title: Création et Ajoute de modèles et de composants
seo-title: Création et Ajoute de modèles et de composants
description: Suivez cette page pour en savoir plus sur la création et l’ajout de modèles et de composants à votre application. La page utilise l’application Geometrixx Unlimited comme application contenant un exemple de modèle d’application et de modèles de page.
seo-description: Suivez cette page pour en savoir plus sur la création et l’ajout de modèles et de composants à votre application. La page utilise l’application Geometrixx Unlimited comme application contenant un exemple de modèle d’application et de modèles de page.
uuid: 3a93017c-8094-413f-a01c-9b72025a2b20
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: ec4ada04-e429-4ad4-a060-2dccac847cf0
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1198'
ht-degree: 2%

---


# Création et Ajoute de modèles et de composants {#creating-and-adding-templates-and-components}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

AEM Mobile On-Demand fournit un modèle d’application entièrement configuré, un modèle d’article et des composants d’article.

L&#39;application We.Unlimited est un exemple de modèle représentant l&#39;interpréteur de commandes d&#39;une application AEM Mobile On-Demand entièrement configurable et gérable.

La sélection de cet exemple de modèle lors de la création d’une application fournit un tableau de bord riche en fonctionnalités AEM Mobile.

![chlimage_1-70](assets/chlimage_1-70.png)

>[!NOTE]
>
>Pour gérer le contenu de votre application et de votre application mobile à partir du Centre de contrôle des applications AEM Mobile, consultez le [Tableau de bord d’application AEM Mobile](/help/mobile/mobile-apps-ondemand-application-dashboard.md).

## Création de modèles d’application {#creating-app-templates}

Un modèle d’application est utilisé pour créer une nouvelle application et agit comme un ensemble de modèles de page et de composants qui représentent une base ou une base d’application. Le modèle estampille certaines propriétés fondamentales pour diriger l’application de la manière appropriée. En général, un client ne créerait pas trop d’applications au total.

Les modèles d’application offrent un moyen facile d’exploiter les conceptions existantes créées par les développeurs, utilisées pour la création de nouvelles applications dans AEM.

Lors de la création d’une application basée sur le modèle d’une autre application, vous obtenez une application dont le point de départ est représentatif de l’application à partir de laquelle elle a été créée.

Procédure de création d’une application à partir d’un modèle d’application :

1. Accédez au catalogue de l’application AEM Mobile : *&lt;URL-serveur>/aem/apps.html/content/mobileapps*
1. Sélectionnez **Créer** —> **App** comme illustré ci-dessous.

Une fois que vous avez créé une application à l’aide de ce modèle, vous pouvez ajouter des articles, des bannières et des collections à votre application. Pour passer de nouveau en revue la création d’articles, de bannières et de collections, voir [Actions de Gestion de contenu](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md).

>[!NOTE]
>
>Vous pouvez également sélectionner un exemple de modèle d’application, par exemple **Application We.Unlimited**, mise à votre disposition par un développeur AEM. Si vous utilisez cet exemple de modèle pour votre application, vous obtenez des exemples d’articles et de collections sur lesquels travailler. Vous aurez la possibilité d’utiliser les exemples de modèles et de composants, de personnaliser les modèles existants ou de créer de nouveaux modèles pour votre application.

>[!CAUTION]
>
>Définition de la propriété ***redirectTarget***
>
>Lors de l’utilisation de l’un des modèles d’application, le développeur définit le contenu de l’application. Cependant, le développeur doit savoir où l’application est créée dans le fichier jcr et la valeur de la propriété ***redirectTarget***.
>
>***redirectTarget*** est calculé dans le cadre de l’opération de création d’application et tente de résoudre un chemin d’accès, s’il existe une propriété redirectTarget disponible dans le modèle d’application, et si la valeur de redirectTarget est définie comme relative. Lorsque le processus de création d’application détecte une valeur relative pour redirectTarget dans le modèle d’application, la valeur est ajoutée à l’emplacement résolu où l’application a été créée.
>
>Par exemple, si un modèle d’application définit un ***redirectTarget*** avec la valeur &quot;*lanugage-masters/en*&quot; et que l’application a été créée dans &quot;*/content/mobileapps/fooApp*&quot;, la valeur finale de redirectTarget après la création de l’application sera &quot;&lt;a6/&lt;a>/content/mobileapps/fooApp/language-masters/fr *&quot;.*


## Création de modèles de contenu {#creating-content-templates}

Chaque type d’entité comporte deux modèles prêts à l’emploi. à savoir :

* **Modèles par défaut:** utilisés pour la création de contenu avec les propriétés/structures par défaut applicables
* **Modèles importés:** utilisés pour importer du contenu à partir d’AEM Mobile avec les propriétés/structures par défaut applicables

### Modèles d’article {#article-templates}

L’article illimité est un exemple de modèle représentant une mise en page d’article à la demande AEM Mobile standard.

1. Cliquez sur **+** dans **Gérer les articles** pour créer un nouvel article. Vous pouvez choisir un **article illimité** ou un **article de texte enrichi**. L’image ci-dessous présente l’option qui vous permet de choisir parmi ces deux modèles d’article.

1. Cliquez sur **Suivant** pour définir les métadonnées d’article telles que le nom/titre de l’article, la description, l’auteur, l’extrait, le département, l’image miniature, l’accès à l’article, etc.
1. Cliquez sur **Suivant** pour renseigner les propriétés de la publicité.
1. Cliquez sur **Suivant** pour entrer l’image de l’article ou l’image des réseaux sociaux.
1. Cliquez sur **Suivant** pour choisir un lien de collection vers lequel ce nouvel article sera associé.
1. Cliquez sur **Suivant** pour entrer les détails du partage sur les réseaux sociaux.
1. Cliquez sur **Créer** pour terminer le processus de création d’un article à l’aide de l’exemple. Pour modifier les propriétés de cet article, cliquez sur **Terminé** ou **Modifier l’article**.

![chlimage_1-71](assets/chlimage_1-71.png)

### Ajouter les composants à l&#39;article {#adding-components-to-article}

Une fois créé, l’auteur peut modifier le contenu d’un article en ajoutant des composants tels que du texte et des images. Les articles sont une extension des modèles de page AEM.

Sélectionnez un article, vous souhaitez le modifier et cliquez sur **Modifier** pour ajouter des composants à l&#39;article.

![chlimage_1-72](assets/chlimage_1-72.png) ![chlimage_1-73](assets/chlimage_1-73.png)

Sélectionnez &quot;**+**&quot; dans le panneau de gauche pour ajouter des composants à votre article.

![chlimage_1-74](assets/chlimage_1-74.png)

### Création de modèles prêts à l’emploi {#creating-out-of-the-box-templates}

Il n’existe pas de modèles d’article prêts à l’emploi. Cependant, il existe un modèle par défaut que les modèles personnalisés doivent étendre, voir l’[exemple de modèle d’article ](http://localhost:4502/crx/de/index.jsp#/apps/geometrixx-unlimited-app/templates/article) de l’application Geometrixx Unlimited.

Les propriétés clés au-delà du modèle d&#39;AEM normal requises sont les suivantes :

***dps-resourceType=&quot;dps:Article&quot;***

Cette propriété garantit que la page AEM est reconnue comme une page d’article ciblée AEM Mobile.

Selon les modèles AEM, vous pouvez ajouter n’importe quelle propriété par défaut ou noeud enfant au ***jcr:content*** du modèle.

### Modèles de bannière et de collection {#banner-and-collection-templates}

>[!CAUTION]
>
>Les bannières et les collections ne comportent pas de contenu et leur création ne prend donc pas en charge les modèles personnalisés.

## Création et Ajoute de composants {#creating-and-adding-components}

Les composants utilisent et autorisent l’accès aux widgets et ceux-ci sont utilisés pour générer le contenu.

Un composant simple est inclus dans le référentiel de code, dont la source se trouve dans AEM. Par la suite, il peut également être ouvert localement en CRXDE Lite.

>[!NOTE]
>
>Il n&#39;existe actuellement aucun composant prêt à l&#39;emploi fourni pour AEM Mobile.


Vous pouvez ajouter des composants à votre page. N’importe quel composant peut être utilisé dans une application AEM Mobile, mais lorsqu’il est appliqué, le rendu peut ne pas être correct.

Cependant, il se peut que les composants personnalisés n’exportent pas et ne téléchargent pas correctement vers AEM Mobile On-demand Services sans un gestionnaire de synchronisation de contenu d’exportation personnalisé qui effectue le rendu dans AEM.

Une fois que le composant a déjà été inclus dans une page AEM, ainsi que quelques autres composants de bloc de construction, vous pouvez ajouter un autre composant à la page ou en modifier un existant.

**Pour ajouter un autre composant à la page :**

1. Sélectionnez cette page et assurez-vous que vous êtes en mode d’édition, via la liste déroulante en haut à droite de l’en-tête de l’éditeur.
1. Active/désactive le panneau latéral à l’aide de l’icône située le plus à gauche dans l’en-tête de l’éditeur
1. Sélectionnez l&#39;onglet **Composants**
1. Faire glisser et déposer l’un des composants disponibles sur la page

![chlimage_1-75](assets/chlimage_1-75.png)

**Pour modifier un composant existant :**

1. Sélectionnez cette page et assurez-vous que vous êtes en mode **Modifier** et sélectionnez le composant.
1. Appuyez sur l’icône de clé à molette pour configurer le composant.

>[!NOTE]
>
>Vous pouvez créer un composant dans AEM et en personnaliser un en utilisant [Développement avec CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md). Une fois que vous avez personnalisé le composant existant en fonction de vos besoins, vous pouvez l’ajouter dans votre page à l’aide de l’option **Modifier** sous **Gérer les articles**, comme illustré dans la figure ci-dessus.

>[!NOTE]
>
>Reportez-vous à [Bonnes pratiques pour le développement de modèles et de composants](/help/mobile/best-practices-aem-mobile.md) en AEM Mobile.

### Étapes suivantes {#the-next-steps}

* [Utilisation des propriétés de contenu pour exporter du contenu](/help/mobile/on-demand-content-properties-exporting.md)
* [Mobile avec Content Sync](/help/mobile/mobile-ondemand-contentsync.md)