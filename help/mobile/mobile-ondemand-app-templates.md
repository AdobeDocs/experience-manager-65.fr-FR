---
title: Création et ajout de modèles et de composants
description: Consultez cette page pour en savoir plus sur la création et l’ajout de modèles et de composants à votre application. La page utilise l’application Geometrixx Unlimited comme application contenant un exemple de modèle d’application et des modèles de page.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
exl-id: 5f050baa-fe10-4acc-ad32-de20793edc13
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '1130'
ht-degree: 1%

---

# Création et ajout de modèles et de composants {#creating-and-adding-templates-and-components}

{{ue-over-mobile}}

AEM Mobile On-Demand fournit un modèle d’application entièrement configuré, un modèle d’article et des composants d’article.

L’application We.Unlimited est un exemple de modèle représentant le shell d’une application On-Demand AEM Mobile entièrement configurable et gérable.

La sélection de cet exemple de modèle lors de la création d’une application génère un tableau de bord riche en fonctionnalités AEM Mobile.

![chlimage_1-70](assets/chlimage_1-70.png)

>[!NOTE]
>
>Pour gérer le contenu de votre application et de votre application mobile à partir du Centre de contrôle des applications AEM Mobile, consultez le [Tableau de bord de l’application AEM Mobile](/help/mobile/mobile-apps-ondemand-application-dashboard.md).

## Création de modèles d’application {#creating-app-templates}

Un modèle d’application est utilisé pour créer une application et agit comme une collection de modèles de page et de composants qui représentent une ligne de base ou la base d’une application. Le modèle élimine certaines propriétés fondamentales pour diriger l’application de la manière appropriée. En règle générale, un client ne crée pas trop d’applications au total.

Les modèles d’application offrent un moyen facile d’utiliser les conceptions existantes créées par les développeurs et développeuses, utilisées pour la création de nouvelles applications au sein d’AEM.

Lors de la création d’une application basée sur le modèle d’une autre application, vous obtiendrez une application qui dispose d’un point de départ représentatif de l’application à partir de laquelle elle a été créée.

Étapes de création d’une application basée sur un modèle d’application :

1. Accédez au catalogue d’applications AEM Mobile : *&lt;server-url>/aem/apps.html/content/mobileapps*
1. Sélectionnez **Créer** > **App** comme illustré ci-dessous

Une fois que vous avez créé une application à l’aide de ce modèle, vous pouvez ajouter des articles, des bannières et des collections à votre application. Pour consulter à nouveau, créer des articles, des bannières et des collections, consultez la section [ Actions de gestion de contenu ](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md).

>[!NOTE]
>
>Vous pouvez également sélectionner un modèle d’application type, par exemple l’application **We.Unlimited**, mise à votre disposition par un développeur ou une développeuse AEM. Si vous utilisez ce modèle type pour votre application, vous obtenez des exemples d’articles et de collections sur lesquels travailler. Vous aurez la possibilité d’utiliser les exemples de modèles et de composants, de personnaliser les modèles existants ou d’en créer de nouveaux pour votre application.

>[!CAUTION]
>
>Définition de la propriété ***redirectTarget***
>
>Lors de l’utilisation de l’un des modèles d’application, le développeur définit le contenu de l’application. Cependant, le développeur doit savoir où l’application est créée dans le jcr et connaître la valeur de la propriété ***redirectTarget***.
>
>La valeur ***redirectTarget*** est calculée dans le cadre de l’opération de création d’application et tente de résoudre un chemin d’accès, si une propriété redirectTarget est disponible dans le modèle d’application et que la valeur de redirectTarget est définie comme relative. Lorsque le processus de création d’application trouve une valeur relative pour redirectTarget dans le modèle d’application, la valeur est ajoutée à l’emplacement résolu de l’emplacement où l’application a été créée.
>
>Par exemple, si un modèle d’application définit une ***redirectTarget*** avec une valeur de « *language-masters/en* » et que l’application a été créée dans « */content/mobileapps/fooApp* », la valeur finale de redirectTarget une fois l’application créée est « */content/mobileapps/fooApp/language-masters/en* ».
>

## Création de modèles de contenu {#creating-content-templates}

Chaque type d’entité comporte deux modèles prêts à l’emploi. Ces principes sont les suivants :

* **Modèles par défaut :** utilisés pour la création de contenu avec les propriétés/structures par défaut applicables
* **Modèles importés :** utilisé pour importer du contenu à partir d’AEM Mobile avec les propriétés/structures par défaut applicables

### Modèles d’article {#article-templates}

L’article Illimité est un exemple de modèle représentant une mise en page d’article On-Demand AEM Mobile type.

1. Dans **Gérer les articles**, sélectionnez **+** pour créer un article. Vous pouvez choisir un **Article illimité** ou un **Article de texte enrichi**. L’image ci-dessous montre l’option qui vous permet de choisir l’un de ces deux modèles d’article.

1. Cliquez sur **Suivant** pour définir les métadonnées de l’article telles que le nom/titre de l’article, la description, l’auteur, le résumé, le service, l’image miniature, l’accès à l’article, etc.
1. Cliquez sur **Suivant** pour renseigner les propriétés de la publicité.
1. Cliquez sur **Suivant** pour saisir l’image de l’article ou celle des médias sociaux
1. Cliquez sur **Suivant** pour choisir un lien de collection vers ce nouvel article.
1. Cliquez sur **Suivant** pour saisir les détails du partage sur les réseaux sociaux.
1. Cliquez sur **Créer** pour terminer la création d’un article à l’aide de l’exemple. Cliquez sur **Terminé** ou **Modifier l’article** pour modifier les propriétés de cet article.

![chlimage_1-71](assets/chlimage_1-71.png)

### Ajout de composants à l’article {#adding-components-to-article}

Une fois créé, un auteur peut modifier le contenu d’un article en ajoutant des composants tels que du texte et des images. Les articles sont une extension des modèles de page AEM.

Sélectionnez un article à modifier, puis cliquez sur **Modifier** pour ajouter des composants à l’article.

![chlimage_1-72](assets/chlimage_1-72.png) ![chlimage_1-73](assets/chlimage_1-73.png)

Sélectionnez « **+** » dans le panneau de gauche pour ajouter des composants à votre article.

![chlimage_1-74](assets/chlimage_1-74.png)

### Création de modèles prêts à l’emploi {#creating-out-of-the-box-templates}

Il n’existe aucun modèle d’article prêt à l’emploi, mais il existe un modèle par défaut que les modèles personnalisés doivent étendre. Consultez [Exemple de modèle d’article](http://localhost:4502/crx/de/index.jsp#/apps/geometrixx-unlimited-app/templates/article) de l’application Geometrixx Unlimited.

Les propriétés clés au-delà des propriétés requises normales du modèle AEM sont les suivantes :

***dps-resourceType=« dps:Article »***

Cette propriété garantit que la page AEM est reconnue en tant que page d’article ciblé AEM Mobile.

Selon les modèles AEM, vous pouvez ajouter n’importe quelle propriété par défaut ou n’importe quel nœud enfant au ***jcr:content*** du modèle.

### Modèles de bannière et de collection {#banner-and-collection-templates}

>[!CAUTION]
>
>Les bannières et les collections n’ayant pas de contenu, leur création ne prend pas en charge les modèles personnalisés.

## Création et ajout de composants {#creating-and-adding-components}

Les composants utilisent et permettent d’accéder aux widgets , qui sont utilisés pour le rendu du contenu.

Un simple composant est inclus dans le référentiel de code, dont la source se trouve dans AEM. Par la suite, il peut également être ouvert localement dans CRXDE Lite.

>[!NOTE]
>
>Il n’existe actuellement aucun composant prêt à l’emploi fourni pour AEM Mobile.
>

Vous pouvez ajouter des composants à votre page. Tout composant peut être utilisé dans une application AEM Mobile, mais son application peut ne pas s’afficher correctement.

Cependant, les composants personnalisés peuvent ne pas exporter et charger correctement vers AEM Mobile On-demand Services sans un gestionnaire de synchronisation de contenu d’exportation personnalisé qui s’affiche dans AEM.

Une fois que le composant a déjà été inclus dans une page AEM, avec quelques autres composants de bloc de création, vous pouvez ajouter un autre composant à la page ou modifier un composant existant.

**Pour ajouter un autre composant à la page :**

1. Sélectionnez cette page et assurez-vous que vous êtes en mode d’édition, via la liste déroulante en haut à droite de l’en-tête de l’éditeur
1. Activez le panneau latéral à l’aide de l’icône la plus à gauche de l’en-tête de l’éditeur
1. Sélectionnez l’onglet **Composants**
1. Faites glisser et déposez l’un des composants disponibles sur la page

![chlimage_1-75](assets/chlimage_1-75.png)

**Pour modifier un composant existant, procédez comme suit**

1. Sélectionnez cette page, vérifiez que vous êtes en mode **Modifier**, puis sélectionnez le composant
1. Sélectionnez l’icône clé à molette pour configurer le composant

>[!NOTE]
>
>Vous pouvez créer un composant dans AEM et le personnaliser à l’aide du [Développement avec CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md). Une fois que vous avez personnalisé le composant existant en fonction de vos besoins, vous pouvez l’ajouter dans votre page à l’aide de l’option **Modifier** sous **Gérer les articles**, comme illustré dans la figure ci-dessus.

>[!NOTE]
>
>Reportez-vous à la section [ Bonnes pratiques pour le développement de modèles et de composants ](/help/mobile/best-practices-aem-mobile.md) dans AEM Mobile.

### Les étapes suivantes {#the-next-steps}

* [Utilisation des propriétés de contenu pour exporter du contenu](/help/mobile/on-demand-content-properties-exporting.md)
* [Mobile avec synchronisation de contenu](/help/mobile/mobile-ondemand-contentsync.md)
