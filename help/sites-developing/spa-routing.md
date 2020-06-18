---
title: Routage de modèle SPA
seo-title: Routage de modèle SPA
description: Pour les applications d’une seule page dans AEM, l’application est responsable du routage. Ce document décrit le mécanisme de routage, le contrat et les options disponibles.
seo-description: Pour les applications d’une seule page dans AEM, l’application est responsable du routage. Ce document décrit le mécanisme de routage, le contrat et les options disponibles.
uuid: 93b4f85a-a240-42d4-95e2-e8b790df7723
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: d9f1e24e-51a9-4f28-b2cd-2e97aed63a24
translation-type: tm+mt
source-git-commit: 4ea1bad1fb76142be7f6d564ecf30ed85a6da694
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 4%

---


# Routage de modèle SPA{#spa-model-routing}

Pour les applications d’une seule page dans AEM, l’application est responsable du routage. Ce document décrit le mécanisme de routage, le contrat et les options disponibles.

>[!NOTE]
>
>L’éditeur d’applications monopages est la solution recommandée pour les projets qui nécessitent un rendu côté client basé sur la structure d’applications monopages (par exemple, Réagir ou Angular).

## Routage du projet {#project-routing}

L’application est propriétaire du routage et est ensuite implémentée par les développeurs frontaux du projet. Ce document décrit le routage spécifique au modèle renvoyé par le serveur AEM. La structure des données du modèle de page expose l&#39;URL de la ressource sous-jacente. Le projet frontal peut utiliser toute bibliothèque personnalisée ou tierce fournissant des fonctionnalités de routage. Une fois qu&#39;un itinéraire attend un fragment de modèle, un appel à la `PageModelManager.getData()` fonction peut être effectué. Lorsqu’un itinéraire de modèle a été modifié, un événement doit être déclenché pour avertir les bibliothèques d’écoute telles que l’éditeur de page.

## Architecture {#architecture}

Pour une description détaillée, reportez-vous à la section [PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager) du document de plan d&#39;application d&#39;une seule page.

## ModelRouter {#modelrouter}

Lorsque cette option est activée, `ModelRouter` - encapsule les fonctions de l’API d’historique HTML5 `pushState` et `replaceState` garantit qu’un fragment donné du modèle est prérécupéré et accessible. Il informe ensuite le composant frontal enregistré que le modèle a été modifié.

## Routage de modèle manuel ou automatique {#manual-vs-automatic-model-routing}

Le `ModelRouter` système automatise la récupération des fragments du modèle. Mais comme tout outil automatisé vient avec des limites. Si nécessaire, `ModelRouter` vous pouvez désactiver ou configurer le paramètre pour ignorer les chemins d’accès à l’aide des propriétés de métadonnées (voir la section Meta Properties du document de composants [de page](/help/sites-developing/spa-page-component.md) SPA). Les développeurs frontaux peuvent alors mettre en oeuvre leur propre couche de routage de modèle en demandant `PageModelManager` à la fonction de charger tout fragment de modèle donné à l&#39;aide de la `getData()` fonction.

>[!NOTE]
>
>Actuellement, le projet d&#39;exemple de Journal We.Retail React illustre l&#39;approche automatisée tandis que le projet Angular illustre l&#39;approche manuelle. Une approche semi-automatisée serait également un cas d&#39;utilisation valable.

>[!CAUTION]
>
>La version actuelle du modèle `ModelRouter` ne prend en charge que l&#39;utilisation d&#39;URL pointant vers le chemin de ressource réel des points d&#39;entrée du modèle Sling. Il ne prend pas en charge l&#39;utilisation d&#39;URL ou d&#39;alias Vanity.

## Contrat de routage {#routing-contract}

L’implémentation actuelle repose sur l’hypothèse que le projet d’application d’une seule page utilise l’API d’historique HTML5 pour le routage des différentes pages de l’application.

### Configuration {#configuration}

Le `ModelRouter` prend en charge le concept de routage de modèle lorsqu’il écoute `pushState` et `replaceState` appelle à prérécupérer les fragments de modèle. En interne, il déclenche le chargement `PageModelManager` du modèle correspondant à une URL donnée et déclenche un `cq-pagemodel-route-changed` événement que d’autres modules peuvent écouter.

Par défaut, ce comportement est automatiquement activé. Pour le désactiver, l’application sur une seule page doit effectuer le rendu de la propriété meta suivante :

```
<meta property="cq:pagemodel_router" content="disable"\>
```

Note that every route of the SPA should correspond to an accessible resource in AEM (e.g., &quot; `/content/mysite/mypage"`) since the `PageModelManager` will automatically try to load the corresponding page model once the route is selected. Though, if needed, the SPA can also define a &quot;block list&quot; of routes that should be ignored by the `PageModelManager`:

```
<meta property="cq:pagemodel_route_filters" content="route/not/found,^(.*)(?:exclude/path)(.*)"/>
```
