---
title: Intégration des données AEM Forms
description: L’intégration de données vous permet d’intégrer AEM Forms à des sources de données disparates et de créer un modèle de données de formulaire pour créer et utiliser des formulaires adaptatifs et des communications interactives.
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integration
docset: aem65
feature: Form Data Model
exl-id: dd1146e4-952d-4dfa-8084-46c6096c4177
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 94%

---

# Intégration de données [!DNL AEM Forms] {#aem-forms-data-integration}

![hero-image](do-not-localize/data-integration.png)

Les infrastructures d’entreprise comprennent des systèmes back-end ou des sources de données disparates comme des bases de données, des services web, des services REST, des services OData et des solutions CRM. Associés, ils constituent un système d’informations qui fournit des données aux applications d’entreprise pour effectuer les activités quotidiennes. En revanche, les applications capturent des données et les renvoient pour mettre à jour les sources de données.

Les applications telles [!DNL AEM Forms] que les formulaires adaptatifs et les communications interactives nécessitent l’intégration à des sources de données à des fins de récupération des données client lors du rendu des formulaires et la création de communications interactives. Il existe des cas d’utilisation dans lesquels les données sont extraites de sources de données en fonction des entrées utilisateur dans les formulaires adaptatifs. De plus, les données de formulaire adaptatif envoyées peuvent être réécrites pour mettre à jour les sources de données respectives.

Alors qu’un système modulaire distribué a des avantages propres, le défi consiste à intégrer et créer des associations de données dans plusieurs sources de données. L’intégration des données est essentielle au fonctionnement et à l’efficacité d’une infrastructure d’entreprise avec des sources de données distinctes connectées à des applications à des fins d’échange des données d’entreprise.

## Aperçu de l’intégration de données {#data-integration-overview}

![aem-forms-data-integeration](assets/aem-forms-data-integeration.png)

L’intégration de données [!DNL AEM Forms] permet de configurer et de connecter des sources de données disparates à [!DNL AEM Forms]. Elle fournit une interface utilisateur intuitive qui permet de créer un schéma de représentation de données unifiée des entités d’entreprise dans les sources de données connectées. La représentation unifiée est appelée modèle de données de formulaire, qui est une extension du schéma JSON. Les entités d’un modèle de données de formulaire sont appelées objets de modèle de données. Un modèle de données de formulaire permet d’effectuer les actions suivantes :

* Accéder aux objets de modèle de données, aux propriétés et aux services à partir de sources de données connectées.
* Créer des objets et des propriétés de modèle de données personnalisés.
* Créez des associations entre les objets de modèle de données dans et entre les sources de données.
* Appelez les services d’objet de modèle de données pour interroger ou écrire des données vers et depuis des sources de données.

Une fois que vous avez créé un modèle de données de formulaire, vous pouvez l’utiliser dans divers processus de formulaires adaptatifs et de communications interactives :

* Créer des formulaires adaptatifs et des communications interactives basés sur le modèle de données de formulaire
* Remplir des formulaires adaptatifs et des communications interactives à partir de sources de données configurées
* Appeler des services/opérations de source de données à l’aide de règles de formulaire adaptatif
* Écrire les données de formulaire adaptatif envoyées dans les sources de données

## Prise en main de l’intégration de données {#get-started-with-data-integration}

La première étape de l’implémentation de l’intégration de données consiste à identifier et configurer les sources de données qui stockent les informations que vous souhaitez utiliser dans les formulaires adaptatifs et les cas d’utilisation des communications interactives. Ensuite, vous créez un modèle de données de formulaire qui utilise un objet, des propriétés et des services de modèle de données provenant d’une ou de plusieurs sources de données. Vous pouvez créer des formulaires adaptatifs et des communications interactives en fonction d’un modèle de données de formulaire dans lequel les champs de formulaire adaptatif ou les espaces réservés dans les communications interactives sont liés aux propriétés de source de données respectives.

[!DNL AEM Forms] vous permet également de créer un modèle de données de formulaire indépendant des sources de données et d’associer ou de lier des objets et des propriétés de modèle de données dans le modèle de données de formulaire à la source de données ultérieurement. Il élimine les dépendances sur les sources de données lorsque vous travaillez sur un modèle de données de formulaire.

Examinez les éléments suivants pour commencer, comprendre et implémenter l’intégration de données.

* [Configuration des sources de données](../../forms/using/configure-data-sources.md)
* [Création d’un modèle de données de formulaire](../../forms/using/create-form-data-models.md)
* [Utilisation d’un modèle de données de formulaire](../../forms/using/work-with-form-data-model.md)
* [Utilisation d’un modèle de données de formulaire](../../forms/using/using-form-data-model.md)
