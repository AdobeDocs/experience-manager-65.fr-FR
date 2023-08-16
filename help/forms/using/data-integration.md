---
title: Intégration des données AEM Forms
seo-title: AEM Forms Data Integration
description: L’intégration de données vous permet d’intégrer AEM Forms à des sources de données disparates et de créer un modèle de données de formulaire pour créer et utiliser des formulaires adaptatifs et des communications interactives.
seo-description: Data Integration lets you integrate AEM Forms with disparate data sources and create form data model to create and work with adaptive forms and interactive communications.
uuid: 01df045e-1b26-437c-9674-fd223ecd5097
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integration
discoiquuid: e397c6ce-d73f-4183-8445-1897a8906960
docset: aem65
feature: Form Data Model
exl-id: dd1146e4-952d-4dfa-8084-46c6096c4177
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 26%

---

# Intégration de données [!DNL AEM Forms] {#aem-forms-data-integration}

![hero-image](do-not-localize/data-integration.png)

Les infrastructures d’entreprise comprennent des systèmes principaux ou des sources de données disparates comme des bases de données, des services web, des services REST, des services OData et des solutions de gestion de la relation client. Ensemble, ils créent un système d’information qui fournit des données aux applications d’entreprise pour effectuer des tâches quotidiennes. D’un autre côté, les applications capturent les données et les renvoient pour mettre à jour les sources de données.

Les applications telles [!DNL AEM Forms] que les formulaires adaptatifs et les communications interactives nécessitent l’intégration à des sources de données à des fins de récupération des données client lors du rendu des formulaires et la création de communications interactives. Il existe des cas d’utilisation où les données sont récupérées à partir de sources de données en fonction des entrées utilisateur dans les formulaires adaptatifs. En outre, les données de formulaire adaptatif envoyées peuvent être réécrites pour mettre à jour les sources de données respectives.

Bien qu’un système modulaire et distribué présente ses propres avantages, le défi consiste à intégrer et à créer des associations de données entre les sources de données. L’intégration des données est la clé d’une infrastructure d’entreprise fonctionnelle et efficace avec des sources de données disparates connectées aux applications d’échange de données commerciales.

## Aperçu de l’intégration de données {#data-integration-overview}

![aem-forms-data-integeration](assets/aem-forms-data-integeration.png)

L’intégration de données [!DNL AEM Forms] permet de configurer et de connecter des sources de données disparates à [!DNL AEM Forms]. Elle fournit une interface utilisateur intuitive qui permet de créer un schéma de représentation de données unifiée des entités d’entreprise dans les sources de données connectées. La représentation unifiée est appelée modèle de données de formulaire, qui est une extension du schéma JSON. Les entités d’un modèle de données de formulaire sont appelées objets de modèle de données. Un modèle de données de formulaire permet :

* Accédez aux objets, propriétés et services de modèle de données à partir de sources de données connectées.
* Création d’objets et de propriétés de modèle de données personnalisés
* Créez des associations entre les objets de modèle de données dans et entre les sources de données.
* Appelez les services d’objet de modèle de données pour interroger ou écrire des données vers et depuis des sources de données.

Une fois que vous avez créé un modèle de données de formulaire, vous pouvez l’utiliser dans divers processus de formulaires adaptatifs et de communications interactives, tels que :

* Créer des formulaires adaptatifs et des communications interactives basés sur le modèle de données de formulaire
* Remplir des formulaires adaptatifs et des communications interactives à partir de sources de données configurées
* Appeler des services/opérations de source de données à l’aide de règles de formulaire adaptatif
* Écrire les données de formulaire adaptatif envoyées aux sources de données

## Prise en main de l’intégration de données {#get-started-with-data-integration}

La première étape de l’implémentation de l’intégration de données consiste à identifier et configurer les sources de données qui stockent les informations que vous souhaitez exploiter dans les formulaires adaptatifs et les cas d’utilisation des communications interactives. Ensuite, vous créez un modèle de données de formulaire qui utilise un objet de modèle de données, des propriétés et des services à partir d’une ou de plusieurs sources de données. Vous pouvez créer des formulaires adaptatifs et des communications interactives basés sur un modèle de données de formulaire dans lequel les champs de formulaire adaptatif ou les espaces réservés dans les communications interactives sont liés aux propriétés de source de données respectives.

[!DNL AEM Forms] vous permet également de créer un modèle de données de formulaire indépendant des sources de données et d’associer ou de lier ultérieurement des objets et des propriétés de modèle de données dans le modèle de données de formulaire à la source de données. Cela élimine toute dépendance aux sources de données lorsque vous travaillez sur un modèle de données de formulaire.

Consultez les sections suivantes pour commencer, comprendre et mettre en oeuvre l’intégration des données.

* [Configuration des sources de données](../../forms/using/configure-data-sources.md)
* [Création d’un modèle de données de formulaire](../../forms/using/create-form-data-models.md)
* [Utilisation d’un modèle de données de formulaire](../../forms/using/work-with-form-data-model.md)
* [Utilisation d’un modèle de données de formulaire](../../forms/using/using-form-data-model.md)
